---
id: yfwyqbsh63xjsd0zr52q16v
title: Uv
desc: ""
updated: 1769302193647
created: 1769302172276
---

# uv 사용 가이드 (Windows PowerShell)

## 목차

- [설치](#설치)
- [기본 사용법](#기본-사용법)
- [Python 버전 관리](#python-버전-관리)
- [문제 해결](#문제-해결)

---

## 설치

### 방법 1: 공식 설치 스크립트 (권장)

```powershell
# PowerShell에서 실행
irm https://astral.sh/uv/install.ps1 | iex
```

### 설치 확인

```powershell
uv --version
```

---

## 기본 사용법

### 패키지 관리

```powershell
# Python 패키지 설치
uv pip install requests

# requirements.txt에서 설치
uv pip install -r requirements.txt

# 패키지 동기화
uv pip sync requirements.txt

# 설치된 패키지 목록
uv pip list

# requirements.txt 형식으로 출력
uv pip freeze
```

### 가상환경

```powershell
# 가상환경 생성
uv venv

# 가상환경 활성화
.venv\Scripts\Activate.ps1

# 비활성화
deactivate
```

### 스크립트 실행

```powershell
# 기본 실행
uv run script.py

# 특정 Python 버전으로 실행
uv run --python 3.12 script.py
```

---

## Python 버전 관리

### 설치된 Python 확인

```powershell
# 설치된 Python 버전 목록 보기
uv python list

# 다운로드된 Python 위치 확인
uv python dir
```

### 특정 버전 설치

```powershell
# Python 3.12 설치
uv python install 3.12

# 구체적인 버전 설치
uv python install 3.12.8
uv python install 3.11.9
uv python install 3.10.15
```

### 버전 삭제

```powershell
# 특정 버전 삭제
uv python uninstall 3.14.2

# 또는 전체 이름으로
uv python uninstall cpython-3.14.2
```

### 프로젝트에서 특정 버전 사용

#### 방법 1: .python-version 파일

프로젝트 루트에 `.python-version` 파일 생성:

```
3.12.8
```

또는 PowerShell에서:

```powershell
echo "3.12" > .python-version
```

#### 방법 2: 실행 시 버전 지정

```powershell
# 특정 Python 버전으로 실행
uv run --python 3.12 script.py
uv run --python 3.12.8 script.py
```

#### 방법 3: pyproject.toml

프로젝트에 `pyproject.toml` 파일 생성:

```toml
[project]
requires-python = ">=3.12,<3.13"
```

---

## 문제 해결

### 실행 정책 오류

설치 스크립트 실행 시 오류가 발생하면:

```powershell
# 현재 정책 확인
Get-ExecutionPolicy

# 현재 사용자에 대해 정책 변경 (권장)
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser

# 또는 현재 세션에만 임시 적용
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
```

그 후 다시 설치 스크립트 실행:

```powershell
irm https://astral.sh/uv/install.ps1 | iex
```

### PATH 문제

설치 후 `uv`를 찾을 수 없다면:

1. PowerShell 재시작
2. 또는 수동으로 PATH 새로고침:

```powershell
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User")
```

### 캐시 정리

```powershell
# 캐시 정리
uv cache clean

# 모든 다운로드된 Python 삭제
uv python uninstall --all
```

---

## 유용한 명령어

```powershell
uv --help                    # 도움말
uv pip --help                # pip 명령어 도움말
uv python --help             # python 관리 도움말
uv cache clean               # 캐시 정리
uv version                   # 버전 확인
```

---

## 성능

`uv`는 Rust로 작성되어 `pip`보다 **10-100배 빠른 성능**을 제공합니다.

---

## 참고 링크

- 공식 문서: https://docs.astral.sh/uv/
- GitHub: https://github.com/astral-sh/uv
