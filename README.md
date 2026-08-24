# ED2 Interop Patch Pack

한국 DOS판 **《Dragon Slayer: The Legend of Heroes II / 영웅전설 II》**를 대상으로 하는 종합 개선 패치 프로젝트입니다.

현재 기준 버전은 **v1.4.50**이며, 대사·표시·밸런스·오디오·QoL·바이너리 버그 수정을 하나의 상호운용 가능한 패치 세트로 관리합니다. 버전별 변경 이력 문서는 별도로 유지하지 않으며, 변경 기록은 Git 커밋과 GitHub Releases를 사용합니다.

## 주요 기능

- PC-98 원문을 기준으로 한 한국어 대사 복원·자연화
- 34셀 표시 폭, 자동 줄바꿈, 페이지 전환을 고려한 대사 표시 보정
- UI·아이템·전투 메시지 및 각종 바이너리 버그 수정
- 몬스터·전투 편성·EXP/Gold·레벨 요구 EXP 밸런스 조정
- M_504 다다르카·악토스 전투 복원
- 지하동굴 맵 간소화 프리셋
- 일반 필드·던전 심볼 인카운트 밀도 완화(선택 가능, 기본 활성)
- Shift 고속 이동 등 QoL 기능
- 교체 VGM / 원본 MUS 선택형 BGM 모드, 22,050 Hz 효과음, 전사의 피리 BGM 보정
- PC-98 기반 오프닝, 엔딩, 장 제목 및 최종전 연출 보정
- ED2 Mod Studio, Map Editor, Raw OPL Converter 등 보조 도구 포함

## 설치

가장 간단한 방법은 `ED2_All_In_One_Patcher_v1.4.50` 폴더의 `run_all_in_one.bat`를 실행하는 것입니다.

1. 패치할 한국 DOS판 영웅전설 II 게임 폴더를 선택합니다.
2. 기본 구성요소 전체 적용 또는 필요한 항목만 선택합니다.
3. 패처가 입력 상태와 대상 파일을 검증한 뒤 트랜잭션 방식으로 적용합니다.
4. 적용 후 실제 DOSBox/실기에서 플레이 상태를 확인합니다.

Python으로 직접 실행할 수도 있습니다.

```text
python ED2_All_In_One_Patcher_v1.4.50/ed2_all_in_one_patcher.py
```

CLI 예시:

```text
python ED2_All_In_One_Patcher_v1.4.50/ed2_all_in_one_patcher.py "C:\ED2" --apply-all --no-gui
python ED2_All_In_One_Patcher_v1.4.50/ed2_all_in_one_patcher.py "C:\ED2" --apply-all --music-mode original --no-gui
python ED2_All_In_One_Patcher_v1.4.50/ed2_all_in_one_patcher.py "C:\ED2" --components dialogue,text,vgm_bgm --no-gui
python ED2_All_In_One_Patcher_v1.4.50/ed2_all_in_one_patcher.py "C:\ED2" --validate --no-gui
```

Python **3.10 이상**을 권장합니다. Windows에서는 `run_all_in_one.bat`가 `py -3`을 먼저 사용하고, 실패하면 `python`을 사용합니다.

## BGM 모드

AIO에서는 두 가지 BGM 소스를 선택할 수 있습니다.

- **교체 VGM BGM (기본)**: 프로젝트의 YM3812 VGM 편곡/교체곡을 사용합니다.
- **원본 BGM**: 한국 DOS판의 순정 `DS2_02~DS2_27`, `DS2_29` MUS와 순정 곡 매핑을 사용합니다. BGM hard-stop, 전투 종료 정지, 설정 ON/OFF 같은 제어 수정은 그대로 유지합니다.

이미 교체 VGM을 적용한 뒤 원본 BGM으로 전환할 때는 최초 패치 전에 AIO가 만든 `*_STOCK_BACKUP`이 필요합니다. 기본 설정에서는 자동 생성됩니다. 원본 BGM에서 교체 VGM으로 다시 전환하는 것도 지원합니다.

## 중요 정책

- **SAVE 파일은 패치 범위 밖입니다.** 검색·수정·백업·마이그레이션 대상으로 사용하지 않습니다.
- 알 수 없는 바이너리 상태를 추측해서 수정하지 않습니다. 지원되는 순정/이전 정본 또는 명시된 manifest와 일치해야 합니다.
- PC-98 바이너리를 한국 DOS NE 실행 파일/DLL에 그대로 복사하지 않습니다. 구조와 호출 규약을 확인한 뒤 필요한 의미만 이식합니다.
- 실제 게임에서 확인하지 않은 사항은 정적 검증과 런타임 검증을 구분합니다.
- M_504 복원과 숫자 밸런스는 별도 책임으로 유지하며, 기본 적용 순서는 **M_504 복원 → 몬스터 밸런스**입니다.

## 문서

- [`docs/COMPONENTS_KO.md`](docs/COMPONENTS_KO.md) — 기본 구성요소와 적용 순서
- [`docs/DEVELOPMENT_KO.md`](docs/DEVELOPMENT_KO.md) — 패치 개발·검증 원칙과 핵심 바이너리 규칙

독립적으로 직접 사용하는 도구에는 해당 폴더에 짧은 `README.md`를 남겼습니다.

## 저장소 구성

- `ED2_All_In_One_Patcher_v1.4.50/` — 권장 통합 설치기
- `ED2_Text_and_Dialogue_Revision_Pack_v4.1R52/` — 대사/텍스트 정본 및 패처
- `ED2-MOD-Studio-v0.13.1/` — 데이터 분석·편집 GUI/CLI
- `ED2_Map_Editor_v0.5.7/` — 맵·지하동굴 편집기
- `ED2_VGM_BGM_Engine_v0.5.49_Combined/` — VGM BGM 엔진 및 Raw OPL 도구
- 기타 `ED2_*` 폴더 — AIO가 조합해 적용하는 개별 패치 구성요소

패치용 CSV/JSON은 **현재 코드가 실제로 읽는 실행 데이터만** 유지합니다. AIO baseline은 `baselines.json` 하나로 통합했고, 과거 검증 snapshot·리포트 JSON은 저장소에서 제외합니다.

## 라이선스

프로젝트 소스와 문서는 루트 `LICENSE`의 MIT License를 따릅니다. 하위 도구에 별도 `LICENSE`/`LICENSE.txt`가 있는 경우 해당 라이선스도 함께 적용됩니다.

게임 원본 파일은 별도로 준비해야 합니다.
