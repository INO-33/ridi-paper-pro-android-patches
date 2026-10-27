# RIDI PAPER PRO · Android 수정 통합

RIDI Android 8에서 수정한 프레임워크, HAL 및 시스템 앱 변경을 **하나의 저장소**로
관리합니다. 커널과 기기 설정은 전용 저장소에 유지하고, 나머지 Android 변경은
고정된 AOSP/NXP 원본에 적용하는 바이너리 보존 패치로 보관합니다.

**전체 프로젝트:** [메인 manifest 저장소](https://github.com/INO-33/ridi-paper-pro)

처음 시작할 때에는 메인의 [개발환경 안내](https://github.com/INO-33/ridi-paper-pro/blob/checkpoint-20261016/DEVELOPMENT.md)를
따릅니다. 바이너리 보존 패치에 포함된 이미지 자산의 공개 전 검토 대상은
[공개 자산 목록](https://github.com/INO-33/ridi-paper-pro/blob/checkpoint-20261016/PUBLIC_ASSETS.md)에 있습니다.

## 구성

| 파일/폴더 | 내용 |
|---|---|
| `projects.json` | 프로젝트 경로, 원본 커밋, 패치 해시와 목표 소스 트리 |
| `patches/` | Android 프로젝트별 누적 변경 |
| `apply.py` | 원본 확인, 패치 적용, 결과 트리 검증 |

주요 범위는 `frameworks/base`의 절전·종료 화면/시스템 UI,
`frameworks/native`의 SurfaceFlinger, NXP gralloc/HWC,
Settings·DocumentsUI·Browser2·입력기, Wi-Fi 및 호스트 빌드 호환성입니다.
현재 실제 프로젝트 목록은 `projects.json`이 기준입니다.

## 적용

메인 저장소의 `prepare.sh`가 원본 동기화 뒤 자동 적용합니다. 수동 진단 시:

```sh
python3 apply.py /absolute/path/to/android-source
python3 apply.py /absolute/path/to/android-source --verify
```

원본 커밋과 패치 SHA256을 먼저 검사하고, 적용 결과를 Git 트리 해시로 확인합니다.
소스와 바이너리 자산, 삭제된 파일과 실행 권한까지 검증 대상입니다. 이미 같은
결과가 적용된 경우 재적용을 생략합니다. 수정된 프로젝트는 덮어쓰지 않습니다.

복원 과정은 각 프로젝트에 로컬 체크포인트 커밋을 만들고 upstream 참조를
보존합니다. 전체 Android 빌드나 기기 설치는 실행하지 않습니다.

## 변경 관리

원본 기준 커밋과 결과 트리를 함께 관리해야 합니다. 패치를 갱신할 때는
`projects.json`의 해시/결과 트리와 메인 manifest의 이 저장소 커밋도 함께 갱신합니다.
과거 개별 프로젝트 저장소는 통합 후 삭제했으며 현재 복원에는 필요하지 않습니다.

체크포인트: **2026-10-27**. 통합 패치 복원 검증과 새 환경의 전체 제품 빌드 검증은
서로 구분합니다. 전체 빌드·실기기 상태는 메인 README를 참고하세요.


## 사용 대상과 라이선스

기존 **리디 페이퍼 프로 사용자**를 위한 프로젝트입니다. 새 자체 앱·보조 코드는
Apache 2.0이며 기존 파일은 원래 라이선스를 유지합니다. 기기 유래 파일에는 재사용
허락을 부여하지 않으며 타 기기 포팅에서는 해당 자료를 제외합니다.
[LICENSING.md](LICENSING.md), [DEVICE_ASSETS.md](DEVICE_ASSETS.md)를 확인하세요.
