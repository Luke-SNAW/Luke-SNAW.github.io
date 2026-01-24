---
id: 1jbyrcnsgfw6d1xkiw5kfjr
title: Tools
desc: ""
updated: 1769208409598
created: 1769205888208
published: false
---

## CLI snippet - install

> python -m pip install torch==2.6 torchvision==0.21 torchaudio==2.6

python -m pip 명령어 사용: pip를 직접 실행하는 대신, 올바른 Python 인터프리터를 사용하도록 python -m pip install [패키지] 명령어를 시도하세요. 이는 임시 해결책으로 작동하며, 올바른 Python 버전을 보장합니다.

가상 환경 사용 추천: 앞으로 유사한 문제를 방지하기 위해, 프로젝트별로 가상 환경(예: venv)을 생성하고 사용하세요. 예: python -m venv myenv 후 myenv\Scripts\activate로 활성화.

## Use virtual environment (recommended)

```bash
python -m venv comfyui_env
source comfyui_env/bin/activate  # Linux/Mac
comfyui_env\Scripts\activate     # Windows
```

### PyTouch

CUDA 버전별 호환되는 torch 버전을 확인

- https://pytorch.org/get-started/previous-versions/

```
python -m pip install torch==2.9.1 torchvision==0.24.1 torchaudio==2.9.1 --index-url https://download.pytorch.org/whl/cu128 --cache-dir ./_cache
```

> --index-url https://download.pytorch.org/whl/cu128

- CUDA 12.8용 GPU 가속 버전의 PyTorch를 다운로드
- 기본 PyPI 대신 PyTorch 전용 저장소 사용
- cu128 = CUDA 12.8 지원

> --cache-dir ./\_cache

- 다운로드한 패키지를 현재 디렉토리의 \_cache 폴더에 임시 저장
- 재설치 시 다시 다운로드하지 않고 캐시 사용 가능

> --target D:\r\framepack_cu128_torch28\system\python

- 패키지를 시스템 기본 위치가 아닌 지정된 디렉토리에 설치
- 격리된 환경이나 포터블 설치에 유용

WARNING: The scripts torchfrtrace.exe and torchrun.exe are installed in 'D:\r\ComfyUI_windows_portable\python_embeded\Scripts' which is not on PATH.
Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.

### nunchaku

https://nunchaku.tech/docs/nunchaku/installation/installation.html

python -m pip install https://github.com/nunchaku-ai/nunchaku/releases/download/v1.2.0/nunchaku-1.2.0+torch2.9-cp312-cp312-win_amd64.whl
