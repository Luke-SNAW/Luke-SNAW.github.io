
# Node 패치 버전 업그레이드 (Lightsail · Bitnami · nvm · pm2 · pnpm)

같은 메이저(24.x) 안에서 Node 패치 버전을 올리는 절차. 같은 메이저라 `node_modules`, Prisma 엔진 재설치는 필요 없다.

## 서버 환경

| 항목 | 값 |
|------|-----|
| 사용자 | `bitnami` |
| 앱 경로 | `/home/bitnami/htdocs` (CodeDeploy 배포 대상) |
| Node | nvm (`/home/bitnami/.nvm`), `default` alias를 정확한 버전으로 고정 |
| 전역 패키지 | pnpm 11.28.8, pm2 7.1.0 (nvm Node 버전별로 따로 설치됨) |
| pm2 | id 0 `index`, fork 모드, `dist/api/index.js` |
| 부팅 자동시작 | systemd `pm2-bitnami.service` (`pm2 startup`으로 생성) |
| 앱 환경변수 | `.env` 파일 (앱이 dotenv로 시작 시마다 읽음) |
| Bitnami 기본 Node | `/opt/bitnami/node` v18.12.1, pm2 5.2.2. 사용하지 않음 |

배포 스크립트 [code-deploy/after-install.sh](../../code-deploy/after-install.sh)는 `nvm.sh`를 source한 뒤 `pm2 restart 0`을 실행한다. 따라서 nvm `default` alias와 pm2 id 0이 유지되어야 한다.

## 알아둘 동작

- **nvm 전역 패키지는 Node 버전별로 분리된다.** 새 버전을 설치하면 pnpm, pm2를 다시 설치해야 한다.
- **pm2 데몬은 시작 시점의 Node 바이너리로 계속 돈다.** `pm2 restart`만으로는 데몬의 Node가 바뀌지 않는다. `pm2 update`(save → kill → resurrect)가 필요하다.
- **pm2는 프로세스를 처음 띄울 때의 환경변수(PATH 포함)를 저장해 두고 재사용한다.** PATH가 이전 Node 경로를 가리키면 앱이 이전 Node로 뜰 수 있다. `--update-env`로 현재 셸 환경을 반영한다.
- **`pm2 save`는 현재 프로세스 목록과 pm2가 가진 환경변수를 `~/.pm2/dump.pm2`에 저장한다.** 재부팅 시 systemd가 `pm2 resurrect`로 이 파일을 읽는다. `.env` 내용은 저장되지 않는다.
- **dotenv는 이미 있는 환경변수를 덮어쓰지 않는다.** `--update-env` 실행 셸에 `.env`와 같은 이름의 변수가 export되어 있으면 그 값이 pm2에 저장되어 `.env`보다 우선한다. 깨끗한 셸에서 실행한다.
- **systemd 유닛에는 nvm Node 버전 경로가 박힌다.** Node 버전을 바꿀 때마다 유닛을 다시 생성해야 한다.

## 절차

아래에서 `<OLD>`는 현재 버전(예: 24.22.1), `<NEW>`는 올릴 버전(예: 24.22.3).

### 0. 사전 확인

작업 전 Lightsail 스냅샷을 만든다.

```bash
node -v && pnpm -v && pm2 -v && nvm alias default && which node
```

```bash
pm2 ls && pm2 describe 0 | grep -E "node.js version|interpreter"
```

```bash
systemctl cat pm2-bitnami.service
```

- `which node`가 `~/.nvm/...`을 가리키는지 확인한다.
- pnpm, pm2 버전을 기록한다.
- 유닛의 `Environment=PATH`, `ExecStart`가 nvm `<OLD>` 경로인지 확인한다. `/opt/bitnami/node`를 가리키면 3단계에서 함께 바로잡힌다.

설치할 버전을 확인한다.

```bash
nvm ls-remote 24 | tail -3
```

### 1. 새 Node 설치, 전역 패키지 재설치

```bash
nvm install <NEW>
```

```bash
nvm alias default <NEW>
```

```bash
npm i -g pnpm@11.28.8 pm2@7.1.0
```

```bash
node -v && pnpm -v && pm2 -v && which node
```

### 2. pm2 데몬과 앱 교체

몇 초간 서비스가 중단된다.

```bash
pm2 update
```

```bash
pm2 describe 0 | grep -E "node.js version|interpreter"
```

`node.js version`이 아직 `<OLD>`이면 현재 셸 환경(PATH)을 반영해 재시작한다. id 0이 유지되므로 `delete` 대신 이 방법을 쓴다.

```bash
pm2 restart 0 --update-env
```

pm2 데몬이 새 Node로 도는지 확인한다. 결과가 `<NEW>` 경로여야 한다.

```bash
ps -o args= -p $(cat ~/.pm2/pm2.pid)
```

재부팅 후에도 유지되도록 저장한다.

```bash
pm2 save
```

### 3. 부팅 자동시작(systemd) 유닛 재생성

`which pm2`가 nvm 경로인 셸에서 실행한다. 두 명령은 각각 sudo 명령을 출력하므로, 출력된 명령을 그대로 실행한다.

```bash
pm2 unstartup systemd
```

```bash
pm2 startup systemd
```

```bash
grep -E "PATH|ExecStart" /etc/systemd/system/pm2-bitnami.service
```

`PATH`에 `/home/bitnami/.nvm/versions/node/v<NEW>/bin`이 있고 `ExecStart`가 `.../v<NEW>/lib/node_modules/pm2/bin/pm2 resurrect`이면 된다. 프로세스 목록은 2단계에서 저장했으므로 `pm2 save`를 다시 할 필요는 없다.

### 4. 검증과 정리

#### 4-1. pm2 부팅 경로 시험 (OS 재부팅 없이)

systemd가 부팅 때 실행하는 경로(`pm2 resurrect`)만 먼저 시험한다. 몇 초간 서비스가 중단되므로 트래픽이 적은 시간에 한다.

```bash
systemctl is-active pm2-bitnami
```

`inactive`(데몬을 수동으로 띄운 상태)이면:

```bash
pm2 kill
```

```bash
sudo systemctl start pm2-bitnami
```

`active`이면:

```bash
sudo systemctl restart pm2-bitnami
```

확인한다. 앱이 `online`이고 `node.js version`이 `<NEW>`이면 된다.

```bash
pm2 ls && pm2 describe 0 | grep -E "node.js version|interpreter"
```

실패하면 원인을 확인하고 수동으로 복구한다. dump는 그대로 남아 있다.

```bash
journalctl -u pm2-bitnami -n 50 --no-pager
```

```bash
pm2 resurrect
```

#### 4-2. 재부팅 테스트

4-1 통과 후, Lightsail 스냅샷을 만들고 여유 있는 시간대에 한다.

```bash
sudo reboot
```

```bash
pm2 ls && pm2 describe 0 | grep -E "node.js version|interpreter"
```

#### 4-3. 정리

API 응답과 로그를 확인한다.

```bash
pm2 logs 0 --lines 50
```

다음 CodeDeploy 배포까지 정상이면 이전 버전을 지운다.

```bash
nvm uninstall <OLD>
```

## 롤백

이전 버전과 그 전역 패키지는 `nvm uninstall` 전까지 남아 있다.

```bash
nvm alias default <OLD>
```

```bash
pm2 update
```

3단계를 진행했다면 `<OLD>`가 잡힌 셸에서 `pm2 unstartup systemd` → `pm2 startup systemd`를 다시 실행한다.

## 적용 기록

### 24.22.1 → 24.22.3

- 1~3단계 완료. 앱과 pm2 데몬이 24.22.3으로 동작함을 확인했다.
- systemd 유닛이 Bitnami 기본 Node(v18.12.1, pm2 5.2.2)를 가리키고 있었다. 3단계에서 nvm v24.22.3 경로로 다시 생성했다.
- 남은 작업:
  - [x] pm2 부팅 경로 시험 (4-1)
  - [ ] 재부팅 테스트 (4-2)
  - [ ] 다음 CodeDeploy 배포 확인 후 `nvm uninstall 24.22.1`
