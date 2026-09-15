
## Collections

- [The Art of Command Line](https://github.com/jlevy/the-art-of-command-line)
- 🤖 [just](https://github.com/casey/just) is a handy way to save and run project-specific commands.
- [Structured text tools](https://github.com/dbohdan/structured-text-tools) - The following is a list of text-based file formats and command line tools for manipulating each.
- [ls-lint](https://github.com/loeffel-io/ls-lint) - An extremely fast directory and filename linter - Bring some structure to your project filesystem
- [mise-en-place](https://github.com/jdx/mise) - dev tools, env vars, task runner
- [Flox](https://github.com/flox/flox/) is a virtual environment and package manager all in one.
- [Terminal Text Effects](https://github.com/ChrisBuilds/terminaltexteffects)
- [chezmoi](https://github.com/twpayne/chezmoi) - Manage your dotfiles across multiple diverse machines, securely.
- [dotenvx](https://github.com/dotenvx/dotenvx) - _a better dotenv_–from the creator of [`dotenv`](https://github.com/motdotla/dotenv).
  - run anywhere (cross-platform)
  - multi-environment
  - encrypted envs
- [Solarized](https://ethanschoonover.com/solarized/) - Precision colors for machines and people

## Shell

- [try](https://github.com/binpash/try) lets you run a command and inspect its effects before changing your live system. `try` uses Linux's [namespaces (via `unshare`)](https://docs.kernel.org/userspace-api/unshare.html) and the [overlayfs](https://docs.kernel.org/filesystems/overlayfs.html) union filesystem.
- [atuin](https://github.com/atuinsh/atuin) - ✨ Magical shell history
- [fish](https://fishshell.com/) - the friendly interactive shell
  - [pure.fish](https://github.com/pure-fish/pure) - Pretty, minimal, and fast prompt for Fish shell

## Script

- [zx](https://github.com/google/zx) - A tool for writing better scripts using javascript

## Features

- [Fig](https://github.com/withfig/autocomplete) adds autocomplete to your terminal
- [Watchexec](https://github.com/watchexec/watchexec) - Executes commands in response to file modifications

### [Reflex](https://github.com/cespare/reflex)

Run a command when files change

> I have been using reflex https://github.com/cespare/reflex for the same thing in some of our docker projects

> +1 for reflex, love being able to have a config for development  
> Example .reflex.conf to run one command when an openapi spec changes and another when any go files change:

```shell
-g "spec.yaml" -- bash -c 'make'
-sr "\.go$" -- go run cmd/app/main.go
```

Then run it with:

```shell
reflex -d fancy -c .reflex.conf
```

#### Why you should use reflex instead

- Reflex has no dependencies. No need to install Ruby or anything like that.
- Reflex uses an appropriate file watching mechanism to watch for changes efficiently on your platform.
- Reflex gives your command the name of the file that changed.
- No DSL to learn -- just give it a shell command.
- No plugins.
- Not tied to any language, framework, workflow, or editor.

## Viewer

- [fx](https://github.com/antonmedv/fx) - Terminal JSON viewer
- Write reducers in your favorite language: [JavaScript](https://github.com/antonmedv/fx/blob/master/doc/js.md) (default), [Python](https://github.com/antonmedv/fx/blob/master/doc/python.md), or [Ruby](https://github.com/antonmedv/fx/blob/master/doc/ruby.md).

## [절대 Cron에서 표준 출력을 사용하지 마세요 - root 볼륨 포화 괴담](https://velog.io/@skynet/%EC%A0%88%EB%8C%80-Cron%EC%97%90%EC%84%9C-%ED%91%9C%EC%A4%80-%EC%B6%9C%EB%A0%A5%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%98%EC%A7%80-%EB%A7%88%EC%84%B8%EC%9A%94-root-%EB%B3%BC%EB%A5%A8-%ED%8F%AC%ED%99%94-%EA%B4%B4%EB%8B%B4)

### 아침을 깨운 root disk 사용량 알림

오전 6시 40분, 운영 서버 중 하나의 루트 디스크 사용률이 90%가 넘는다는 알림이 발생했다. Critical 레벨 알림이었기 때문에 모든 팀원에게 전화가 발신됐다.

이 서버는 모니터링 데이터를 저장하는 용도로 사용한다. 당연히 모든 데이터는 별도로 마운트한 데이터 볼륨에 저장된다. 루트 볼륨이 이 정도로 가득차는 것은 잘 일어나지 않는 이상한 일이다. 게다가 모니터링 데이터를 확인해보니 하루만에 디스크 용량이 5GiB 가량 증가했고 지금도 빠른 속도로 증가하고 있었다.

디스크 사용량이 빠르게 증가하고 있었으므로 우선 루트 볼륨을 확장해 장애 발생을 막았다. 그러나 원인을 밝히지는 못했다.

### 유령 파일 사건

`/var/log` 등 데이터를 많이 차지할만한 공간을 확인해보았으나 허사였다. 결국 `du` 명령어로 루트 볼륨의 모든 서브 디렉토리를 전수조사 하였지만 디스크 사용량이 증가한 원인을 찾을 수 없었다. du 로 확인한 루트 볼륨의 사용량은 10GB 정도였는데 알 수 없는 5GB가 더 사용되고 있었다.

(참고: du 명령어를 재귀적으로 사용하는 건 I/O 부하가 상당하기 때문에 운영 서버에서 수행하기는 부담스러운 작업이다. nice와 ionice를 이용해 우선순위를 최하로 설정한 뒤 서브 디렉토리를 순차적으로 하나씩 검증하는 등의 방식으로 부하를 분산하였다.)

처음 검증한 가설은 ext4의 예약 공간(Reserved space)가 5GiB를 사용한다는 것이었다. 그러나 예약 공간의 점유율이 전체 디스크 공간의 5% 가량이고 루트 볼륨의 크기가 20GB에 불과하다는 점을 감안하면 가능성이 거의 없었다.

다음 가설은 마운트로 인한 루트 볼륨 파일 누락이었다. 루트 볼륨에서 이미 사용하던 디렉토리에 다른 디스크를 마운트 했을 때, 기존에 디렉토리에 있던 파일들은 여전히 디스크를 점유하지만 du 결과에서는 나타나지 않는다고 한다. 그러나 기존에 사용하던 데이터 볼륨 외에 다른 디스크를 마운트한 적은 없었다.

그 다음으론 삭제 파일이 디스크를 점유하고 있을 가능성이다. 기존 프로세스가 열어 둔 파일은 rm 명령어 등을 이용해 삭제하더라도 디스크를 점유한다고 한다. 파일이 삭제된 사실을 알지 못하는 프로세스가 더 이상 존재하지 않는 파일의 내용을 읽는 것을 방지하기 위함이다. 프로세스가 파일을 닫아야 완전히 디스크에서 제거한다.

그럼 현재 실행되는 프로세스 중 삭제된 파일을 열고 있는 것이 있는지를 검증하면 된다. 사용한 명령어는 다음과 같다.

```shell
# nice: CPU 우선순위 최하로 설정
# ionice: I/O 우선순위 최하로 설정
# +L1: 링크 수가 1보다 작은 파일
nice -n19 ionice -c3 sudo lsof +L1
```

결과를 확인해보니 rsync를 이용해 핫 스토리지에서 웜 스토리지로 파일을 옮기는 cron 프로세스(이하 warmer로 표기)가 `/tmp` 디렉토리의 삭제된 파일을 열어두고 있었다. 크기도 사라진 5GB와 엇비슷했다. 디스크 사용량이 계속 증가하고 있었으므로 파일의 크기와 디스크 증가량을 면밀히 대조해 볼 여유는 없었다. 직감이 말하는대로 이 프로세스를 kill 하자 즉시 디스크 사용량이 감소했다.

(참고: 핫 스토리지는 조회와 쓰기 부하가 상대적으로 높은, 즉 '뜨거운' 저장소이다. 반면 warm 스토리지는 부하가 상대적으로 낮은 '미지근한' 저장소이다. 일반적으로 웜 스토리지는 핫 스토리지보다 저렴한 타입을 사용한다. 모니터링 데이터는 최근 데이터의 조회 빈도가 훨씬 높기 때문에 hot/warm 구분의 근거가 명확하다.)

### 범인 검거

warmer를 다시 실행하자 디스크 사용량이 다시 증가하기 시작했다. lsof 결과도 전과 유사했다. `/tmp` 디렉토리에 존재했으나 지금은 삭제된 파일을 열어두고 있다는 것이다. 보안 로그를 통해 모든 사용자의 명령어를 검색해보았으나 삭제 명령어를 수행한 사람은 없었다. 결국 사람이 아닌 프로세스가 지운 것이 명확했다.

`ionotifywait` 명령어를 이용해 `/tmp` 디렉토리를 모니터링 해보니 확실히 변경이 일어나곤 있었다. 그러나 이 명령어로는 어떤 프로세스가 파일을 만들고 삭제하는지 알 수 없었다.

나는 범인으로 rsync를 의심했다. warmer의 주요 업무가 rsync를 실행이었기 때문이다. 조사 결과 rsync는 파일을 복사할 때 임시 파일을 생성한다고 했다. 확신을 얻은 나는 상황을 재현하기 위해 여러 테스트를 했다. 그러나 소득은 내가 틀렸다는 사실을 알았다는 것 뿐이었다. rsync는 임시 파일을 `/tmp`가 아니라 목적지 디렉토리에 생성했다. 임시 파일을 저장할 디렉토리를 플래그로 따로 지정하면 그렇지 않을수도 있지만, 우리는 디폴트 값을 사용하고 있었다.

그래도 warmer에 대한 의심을 져버릴 수 없었던 나는 `/proc` 디렉토리에 접근해 파일 디스크립터를 조회했다. 그런데 warmer의 1,2 번 파일 디스크립터가 `/tmp` 디렉토리의 삭제된 파일을 지시하는 심볼릭 링크였다.

즉 stdout과 stderr가 `/tmp` 디렉토리에 출력되고 있으나, 파일은 남아있지 않고 삭제되고 있었다. 그러면서도 warmer 디렉토리가 그 삭제된 파일을 계속 열어두고 있는 상황이었다.

warmer는 crontab으로 실행되고 있었고 stdout과 stderr를 따로 리다이렉트하진 않았다. cron은 터미널을 통해 접속한 사용자가 아니므로 로그를 찍을 곳이 없긴 하다. 그런데 널 디바이스(`/dev/null`)로 출력을 버리지 않고, '출력을 임시 파일에 저장한 뒤 삭제하되 닫지는 않는다.' 라는 이상한 선택을 한 것이었다.

재현 테스트를 거친 결과 cron이 내가 추측한 방식대로 동작한다는 것을 확신할 수 있었다. 표준 출력에 무의미한 로그를 남기는 shell script를 cron으로 실행한 뒤, 앞서 이야기 한 `lsof` 명령어 결과와 `/proc` 디렉토리의 파일 디스크립터를 조회해보면 동일한 현상이 재현되는 것을 확인할 수 있다.

```shell
#!/bin/bash

while true; do
  head -c $((50 * 1024 * 1024)) < /dev/zero | tr '\0' 'A'
  sleep 10
done
```

(실험 환경: Ubuntu 24.04)

### 마치며

아직도 cron이 왜 표준 출력을 디스크에 저장하고 추적까지 어렵게 만드는 행동을 하는진 모르겠다. 그러나 cron을 직접 고쳐 쓰기는 현실적으로 어려우니 사용법을 바꿔야 한다. 사실 cron의 실행 결과를 로그로 남기지 않고 버리는 것은 작업의 성공, 실패 여부를 알기 어렵게 만드는 방식이다. 게다가 디버깅 뿐만 아니라 root 디스크 포화를 유발할 수 있는 아주 위험한 방식임이 실험을 통해 검증되었다. cron을 안전하게 수행하려면 다음의 방침을 따라야 한다.

- 파일에 로그를 남긴다.
- 로그 파일은 루트 볼륨이 아니라 데이터 볼륨에 위치시켜야 한다
- logrotate 등의 수단을 이용해 크기가 무한정 커지지 않도록 제어해야 한다.
