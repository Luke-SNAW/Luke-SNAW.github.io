
# 목적

특정 시간에 배포하기 했을 때 주기적으로 시간 체크하는 번거로움을 없애기 위해

# 사용 툴 - at

`at`을 활용.

> [At Command in Linux](https://linuxize.com/post/at-command-in-linux/)

## 활성화

최근 MacOS는 atd (at용 daemon) 비활성화가 기본인 걸로 보임. 다음 shell command로 활성화

```bash
sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.atrun.plist
```

## 테스트

### 예약 script 작성

```bash
at now + 1 minute
ls > t.txt
^D # 작성 도중 취소는 ^C
```

### 리스트 확인

```bash
atq
```

실행 이전이면 atq 결과에 나타나고 실행됐으면 없어진다.

### 테스트 결과 확인

```bash
ls t.txt
```

## 예약 배포 script

```bash
at 10:30
./dp # deploy용 script. 각 프로젝트에 작성되어 있을 것. deploy product
^D
```

## 결과

제대로 실행되면 slack channel로 이동할 것임 (deploy용 script에 배포용 slack 채널로 이동하는 command가 포함)

이후 deploy 관련 message 갱신을 확인

# 주의

main branch **merge는 미리** 해놔야 함.

# 참고

## at

```bash
at now
# command
^D
```

로 예약하면 대충 1분 이내 실행 됨.

시간 예약은 10:30, 22:30, 10:30pm, now + 1 hour 등으로 가능

예약 걸어놓은 환경(실행 directory 등)에서 실행되니 다른 directory에서 작업해도 무방.

## atrm

예약 task 삭제

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0dce449f-5f47-49c8-9fe9-8ce19e788d96/Untitled.png)

```bash
atrm 33
```

## 예약 시간

각 project마다 build에 소모되는 시간이 다르므로 역산해서 예약을 걸 것.

- www2018: 3분
- biz-admin: 2분
- desk-api-nodejs: 6분

외우기 귀찮으면 5분 전으로 걸면 대충 OK...

---

# script

```bash
# deploy product. for MacOS (open URL)
git push origin main;open https://gpkor.slack.com/archives/...
```
