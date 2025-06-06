# 변경 내역

## 20240121

1. `config`에 `is_share`를 추가했습니다. Colab과 같은 시나리오에서는 이 값을 `True`로 설정하여 WebUI를 공개 네트워크에 매핑할 수 있습니다.
2. WebUI에 영어 시스템 번역 지원을 추가했습니다.
3. `cmd-asr`이 FunASR 모델이 포함되어 있는지 자동으로 감지합니다; 기본 디렉토리에서 찾을 수 없으면 ModelScope에서 다운로드됩니다.
4. [Issue 79](https://github.com/RVC-Boss/GPT-SoVITS/issues/79)에서 보고된 SoVITS 훈련의 ZeroDivisionError를 필터링 샘플 등으로 해결하려고 시도했습니다.
5. `TEMP` 폴더의 캐시된 오디오 파일 및 기타 파일을 정리했습니다.
6. 참조 오디오의 끝이 포함된 합성 오디오 문제를 크게 줄였습니다.

## 20240122

1. 지나치게 짧은 출력 파일로 인해 참조 오디오가 반복되는 문제를 수정했습니다.
2. 영어 및 일본어 훈련의 네이티브 지원을 테스트했습니다 (일본어 훈련 시 루트 디렉토리에 비영어 특수 문자가 없어야 합니다).
3. 오디오 경로 확인을 개선했습니다. 잘못된 입력 경로에서 읽으려는 시도가 있을 경우, ffmpeg 오류 대신 경로가 존재하지 않는다고 보고합니다.

## 20240123

1. Hubert 추출로 인해 NaN 오류가 발생하여 SoVITS/GPT 훈련에서 ZeroDivisionError가 발생하는 문제를 해결했습니다.
2. 추론 WebUI에서 빠른 모델 전환 지원을 추가했습니다.
3. 모델 파일 정렬 로직을 최적화했습니다.
4. 중국어 단어 분할을 위해 `jieba`를 `jieba_fast`로 교체했습니다.

## 20240126

1. 중국어-영어 혼합 및 일본어-영어 혼합 출력 텍스트를 지원합니다.
2. 출력에 대한 선택적 분할 모드를 추가했습니다.
3. UVR5 읽기 문제 및 디렉토리 자동 탈출 문제를 수정했습니다.
4. 추론 오류를 일으키는 여러 줄 바꿈 문제를 수정했습니다.
5. 추론 WebUI 에서 중복 로그를 제거했습니다.
6. Mac에서 훈련 및 추론을 지원합니다.
7. 절반 정밀도를 지원하지 않는 GPU에 대해 자동으로 단정밀도를 강제하며, CPU 추론 시 단정밀도를 적용합니다.

## 20240128

1. 숫자의 발음이 중국어 문자로 변환되는 문제를 수정했습니다.
2. 문장 시작 부분에서 몇 개의 문자가 누락되는 문제를 수정했습니다.
3. 비합리적인 참조 오디오 길이를 설정하여 제외했습니다.
4. GPT 훈련 시 체크포인트가 저장되지 않는 문제를 수정했습니다.
5. Dockerfile 에서 모델 다운로드 프로세스를 완료했습니다.

## 20240129

1. 절반 정밀도 훈련에 문제가 있는 16 시리즈와 같은 GPU의 훈련 구성을 단정밀도로 변경했습니다.
2. 사용 가능한 Colab 버전을 테스트하고 업데이트했습니다.
3. 이전 버전의 FunASR 로 인해 인터페이스 정렬 오류가 발생하는 ModelScope FunASR 저장소의 git 클로닝 문제를 수정했습니다.

## 20240130

1. 모든 경로 관련 항목에서 이중 따옴표를 자동으로 제거하여 초보자가 이중 따옴표가 포함된 경로를 복사하는 오류를 방지했습니다.
2. 중국어 및 영어 문장 부호 분할 문제를 수정하고 문장 시작과 끝에 부호를 추가했습니다.
3. 부호에 의한 분할을 추가했습니다.

## 20240201

1. 분리 실패를 일으킨 UVR5 형식 읽기 오류를 수정했습니다.
2. 혼합된 중국어-일본어-영어 텍스트에 대한 자동 분할 및 언어 인식을 지원합니다.

## 20240202

1. `/` 로 끝나는 ASR 경로가 파일 이름 저장 시 오류를 발생시키는 문제를 수정했습니다.
2. [PR 377](https://github.com/RVC-Boss/GPT-SoVITS/pull/377) 에서는 PaddleSpeech 의 Normalizer 를 도입하여 "xx.xx%" (백분율 기호)와 "元/吨"이 "元吨"으로 읽히는 문제를 "元每吨"으로 수정하고, 밑줄 오류를 수정했습니다.

## 20240207

1. [Issue 391](https://github.com/RVC-Boss/GPT-SoVITS/issues/391) 에서 보고된 중국어 추론 품질 저하를 일으킨 언어 매개변수 혼동을 수정했습니다.
2. [PR 403](https://github.com/RVC-Boss/GPT-SoVITS/pull/403) 에서는 UVR5 를 높은 버전의 librosa에 맞게 조정했습니다.
3. [Commit 14a2851](https://github.com/RVC-Boss/GPT-SoVITS/commit/14a285109a521679f8846589c22da8f656a46ad8)에서는 `is_half` 매개변수가 불리언으로 변환되지 않아 발생한 UVR5 `inf` 오류를 수정했습니다. 이로 인해 16 시리즈 GPU에서 `inf` 가 발생했습니다.
4. 영어 텍스트 프론트엔드를 최적화했습니다.
5. Gradio 종속성 문제를 수정했습니다.
6. 데이터셋 준비 시 루트 디렉토리를 비워두면 `.list` 전체 경로를 자동으로 읽도록 지원합니다.
7. 일본어와 영어에 대한 Faster Whisper ASR을 통합했습니다.

## 20240208

1. [Commit 59f35ad](https://github.com/RVC-Boss/GPT-SoVITS/commit/59f35adad85815df27e9c6b33d420f5ebfd8376b)에서는 Windows 10 1909와 [Issue 232](https://github.com/RVC-Boss/GPT-SoVITS/issues/232) (전통 중국어 시스템 언어)에서 GPT 훈련 멈춤 문제를 수정하려고 했습니다.

## 20240212

1. Faster Whisper와 FunASR의 로직을 최적화하고, Faster Whisper를 미러 다운로드로 전환하여 Hugging Face 연결 문제를 피했습니다.
2. [PR 457](https://github.com/RVC-Boss/GPT-SoVITS/pull/457)은 DPO Loss 실험적 훈련 옵션을 활성화하여 GPT의 반복 및 문자 누락 문제를 완화하고, 훈련 중 부정 샘플을 구성하며 여러 추론 매개변수를 추론 WebUI에서 사용할 수 있게 했습니다.

## 20240214

1. 훈련 시 중국어 실험 이름을 지원합니다 (이전에는 오류가 발생했습니다).
2. DPO 훈련을 필수 기능 대신 선택적 기능으로 변경했습니다. 선택 시, 배치 크기가 자동으로 절반으로 줄어듭니다. 추론 WebUI에서 새로운 매개변수가 전달되지 않는 문제를 수정했습니다.

## 20240216

1. 참조 텍스트 없이 입력을 지원합니다.
2. [Issue 475](https://github.com/RVC-Boss/GPT-SoVITS/issues/475)에서 보고된 중국어 프론트엔드의 버그를 수정했습니다.

## 20240221

1. 데이터 처리 중 노이즈 감소 옵션을 추가했습니다 (노이즈 감소는 16kHz 샘플링 비율만 남깁니다; 배경 노이즈가 심한 경우에만 사용하십시오).
2. [PR 559](https://github.com/RVC-Boss/GPT-SoVITS/pull/559), [PR 556](https://github.com/RVC-Boss/GPT-SoVITS/pull/556), [PR 532](https://github.com/RVC-Boss/GPT-SoVITS/pull/532), [PR 507](https://github.com/RVC-Boss/GPT-SoVITS/pull/507), [PR 509](https://github.com/RVC-Boss/GPT-SoVITS/pull/509) 중국어 및 일본어 프론트엔드 처리를 최적화했습니다.
3. Mac CPU 추론을 MPS 대신 CPU를 사용하도록 전환하여 성능을 향상시켰습니다.
4. Colab 공개 URL 문제를 수정했습니다.

## 20240306

1. [PR 672](https://github.com/RVC-Boss/GPT-SoVITS/pull/672)는 추론 속도를 50% 가속화했습니다 (RTX3090 + PyTorch 2.2.1 + CU11.8 + Win10 + Py39에서 테스트됨).
2. Faster Whisper의 비중국어 ASR을 사용할 때 중국어 FunASR 모델을 먼저 다운로드할 필요가 없습니다.
3. [PR 610](https://github.com/RVC-Boss/GPT-SoVITS/pull/610)은 UVR5 리버브 제거 모델에서 설정이 반대로 되어 있는 문제를 수정했습니다.
4. [PR 675](https://github.com/RVC-Boss/GPT-SoVITS/pull/675)는 CUDA가 없는 경우 Faster Whisper의 자동 CPU 추론을 가능하게 했습니다.
5. [PR 573](https://github.com/RVC-Boss/GPT-SoVITS/pull/573)은 Mac에서 올바른 CPU 추론을 보장하기 위해 `is_half` 체크를 수정했습니다.

## 202403/202404/202405

### 사소한 수정:

1. 참조 텍스트 없는 모드의 문제를 수정했습니다.
2. 중국어 및 영어 텍스트 프론트엔드를 최적화했습니다.
3. API 형식을 개선했습니다.
4. CMD 형식 문제를 수정했습니다.
5. 훈련 데이터 처리 중 지원되지 않는 언어에 대한 오류 프롬프트를 추가했습니다.
6. Hubert 추출의 버그를 수정했습니다.

### 주요 수정:

1. VQ를 고정하지 않고 SoVITS 훈련의 문제를 수정했습니다(품질 저하를 일으킬 수 있음).
2. 빠른 추론 분기를 추가했습니다.

## 20240610

### 사소한 수정:

1. [PR 1168](https://github.com/RVC-Boss/GPT-SoVITS/pull/1168) & [PR 1169](https://github.com/RVC-Boss/GPT-SoVITS/pull/1169) 순수 구두점 및 다중 구두점 텍스트 입력 로직을 개선했습니다.
2. [Commit 501a74a](https://github.com/RVC-Boss/GPT-SoVITS/commit/501a74ae96789a26b48932babed5eb4e9483a232) UVR5에서 MDXNet 디러버브를 위한 CMD 형식을 수정하고 공백이 있는 경로를 지원했습니다.
3. [PR 1159](https://github.com/RVC-Boss/GPT-SoVITS/pull/1159) `s2_train.py`에서 SoVITS 훈련을 위한 진행률 표시줄 로직을 수정했습니다.

### 주요 수정:

4. [Commit 99f09c8](https://github.com/RVC-Boss/GPT-SoVITS/commit/99f09c8bdc155c1f4272b511940717705509582a) WebUI의 GPT 미세 조정이 중국어 입력 텍스트의 BERT 기능을 읽지 않아 추론과 불일치 및 잠재적 품질 저하를 일으키는 문제를 수정했습니다.
   **주의: 이전에 많은 양의 데이터로 미세 조정한 경우 품질을 향상시키기 위해 모델을 다시 조정하는 것이 좋습니다.**

## 20240706

### 사소한 수정:

1. [Commit 1250670](https://github.com/RVC-Boss/GPT-SoVITS/commit/db50670598f0236613eefa6f2d5a23a271d82041) CPU 추론에서 기본 배치 크기 소수점 문제를 수정했습니다.
2. [PR 1258](https://github.com/RVC-Boss/GPT-SoVITS/pull/1258), [PR 1265](https://github.com/RVC-Boss/GPT-SoVITS/pull/1265), [PR 1267](https://github.com/RVC-Boss/GPT-SoVITS/pull/1267) 노이즈 제거 또는 ASR이 예외를 만나면 모든 보류 중인 오디오 파일이 종료되는 문제를 수정했습니다.
3. [PR 1253](https://github.com/RVC-Boss/GPT-SoVITS/pull/1253) 구두점으로 분할할 때 소수점 분할 문제를 수정했습니다.
4. [Commit a208698](https://github.com/RVC-Boss/GPT-SoVITS/commit/a208698e775155efc95b187b746d153d0f2847ca) 다중 GPU 훈련을 위한 다중 프로세스 저장 로직을 수정했습니다.
5. [PR 1251](https://github.com/RVC-Boss/GPT-SoVITS/pull/1251) 불필요한 `my_utils`를 제거했습니다.

### 주요 수정:

6. [PR 672](https://github.com/RVC-Boss/GPT-SoVITS/pull/672)의 가속 추론 코드가 검증되어 메인 브랜치에 병합되었으며, 기본과 일관된 추론 효과를 보장합니다.
   또한 참조 텍스트 없는 모드에서 가속 추론을 지원합니다.

**향후 업데이트에서는 `fast_inference` 브랜치의 변경 사항의 일관성을 계속 검증할 것입니다**.

## 20240727

### 사소한 수정:

1. [PR 1298](https://github.com/RVC-Boss/GPT-SoVITS/pull/1298) 불필요한 i18n 코드를 정리했습니다.
2. [PR 1299](https://github.com/RVC-Boss/GPT-SoVITS/pull/1299) 사용자 파일 경로의 후행 슬래시가 명령줄 오류를 일으키는 문제를 수정했습니다.
3. [PR 756](https://github.com/RVC-Boss/GPT-SoVITS/pull/756) GPT 훈련의 단계 계산 로직을 수정했습니다.

### 주요 수정:

4. [Commit 9588a3c](https://github.com/RVC-Boss/GPT-SoVITS/commit/9588a3c52d9ebdb20b3c5d74f647d12e7c1171c2) 합성을 위한 음성 속도 조절을 지원했습니다.
   음성 속도만 조절하면서 무작위성을 고정할 수 있습니다.

- 2024.07.27 [PR#1306](https://github.com/RVC-Boss/GPT-SoVITS/pull/1306), [PR#1356](https://github.com/RVC-Boss/GPT-SoVITS/pull/1356): BS-RoFormer 보컬 분리 모델 지원 추가.
  - 유형: 신규 기능
  - 기여자: KamioRinn
- 2024.07.27 [PR#1351](https://github.com/RVC-Boss/GPT-SoVITS/pull/1351): 중국어 텍스트 프론트엔드 개선.
  - 유형: 신규 기능
  - 기여자: KamioRinn

## 202408 (V2 버전)

- 2024.08.01 [PR#1355](https://github.com/RVC-Boss/GPT-SoVITS/pull/1355): WebUI에서 파일 처리 시 경로 자동 입력 기능 추가.
  - 유형: 정리 작업
  - 기여자: XXXXRT666
- 2024.08.01 [Commit#e62e9653](https://github.com/RVC-Boss/GPT-SoVITS/commit/e62e965323a60a76a025bcaa45268c1ddcbcf05c): BS-Roformer FP16 추론 지원 활성화.
  - 유형: 성능 최적화
  - 기여자: RVC-Boss
- 2024.08.01 [Commit#bce451a2](https://github.com/RVC-Boss/GPT-SoVITS/commit/bce451a2d1641e581e200297d01f219aeaaf7299), [Commit#4c8b7612](https://github.com/RVC-Boss/GPT-SoVITS/commit/4c8b7612206536b8b4435997acb69b25d93acb78): GPU 인식 로직 최적화, 사용자 입력 GPU 인덱스 처리 로직 추가.
  - 유형: 정리 작업
  - 기여자: RVC-Boss
- 2024.08.02 [Commit#ff6c193f](https://github.com/RVC-Boss/GPT-SoVITS/commit/ff6c193f6fb99d44eea3648d82ebcee895860a22)~[Commit#de7ee7c7](https://github.com/RVC-Boss/GPT-SoVITS/commit/de7ee7c7c15a2ec137feb0693b4ff3db61fad758): **GPT-SoVITS V2 모델 추가.**
  - 유형: 신규 기능
  - 기여자: RVC-Boss
- 2024.08.03 [Commit#8a101474](https://github.com/RVC-Boss/GPT-SoVITS/commit/8a101474b5a4f913b4c94fca2e3ca87d0771bae3): FunASR을 이용한 광둥어 ASR 지원 추가.
  - 유형: 신규 기능
  - 기여자: RVC-Boss
- 2024.08.03 [PR#1387](https://github.com/RVC-Boss/GPT-SoVITS/pull/1387), [PR#1388](https://github.com/RVC-Boss/GPT-SoVITS/pull/1388): UI 및 타이밍 로직 최적화.
  - 유형: 정리 작업
  - 기여자: XXXXRT666
- 2024.08.06 [PR#1404](https://github.com/RVC-Boss/GPT-SoVITS/pull/1404), [PR#987](https://github.com/RVC-Boss/GPT-SoVITS/pull/987), [PR#488](https://github.com/RVC-Boss/GPT-SoVITS/pull/488): 다중 발음 문자 처리 로직 최적화 (V2 전용).
  - 유형: 수정, 신규 기능
  - 기여자: KamioRinn, RVC-Boss
- 2024.08.13 [PR#1422](https://github.com/RVC-Boss/GPT-SoVITS/pull/1422): 참조 오디오 1개만 업로드 가능한 버그 수정; 누락 파일 경고 팝업 추가.
  - 유형: 수정, 정리 작업
  - 기여자: XXXXRT666
- 2024.08.20 [Issue#1508](https://github.com/RVC-Boss/GPT-SoVITS/issues/1508): 상위 LangSegment 라이브러리에서 SSML 태그로 숫자, 전화번호, 날짜, 시간 최적화 지원.
  - 유형: 신규 기능
  - 기여자: juntaosun
- 2024.08.20 [PR#1503](https://github.com/RVC-Boss/GPT-SoVITS/pull/1503): API 수정 및 최적화.
  - 유형: 수정
  - 기여자: KamioRinn
- 2024.08.20 [PR#1490](https://github.com/RVC-Boss/GPT-SoVITS/pull/1490): `fast_inference` 브랜치를 메인 브랜치로 병합.
  - 유형: 리팩토링
  - 기여자: ChasonJiang
- 2024.08.21 **GPT-SoVITS V2 버전 정식 출시.**

## 202502 (V3 버전)

- 2025.02.11 [Commit#ed207c4b](https://github.com/RVC-Boss/GPT-SoVITS/commit/ed207c4b879d5296e9be3ae5f7b876729a2c43b8)~[Commit#6e2b4918](https://github.com/RVC-Boss/GPT-SoVITS/commit/6e2b49186c5b961f0de41ea485d398dffa9787b4): **GPT-SoVITS V3 모델 추가, 파인튜닝 시 14GB VRAM 필요.**
  - 유형: 신규 기능 ([위키 참조](https://github.com/RVC-Boss/GPT-SoVITS/wiki/GPT%E2%80%90SoVITS%E2%80%90v3%E2%80%90features-(%E6%96%B0%E7%89%B9%E6%80%A7)))
  - 기여자: RVC-Boss
- 2025.02.12 [PR#2032](https://github.com/RVC-Boss/GPT-SoVITS/pull/2032): 다국어 프로젝트 문서 업데이트.
  - 유형: 문서화
  - 기여자: StaryLan
- 2025.02.12 [PR#2033](https://github.com/RVC-Boss/GPT-SoVITS/pull/2033): 일본어 문서 업데이트.
  - 유형: 문서화
  - 기여자: Fyphen
- 2025.02.12 [PR#2010](https://github.com/RVC-Boss/GPT-SoVITS/pull/2010): 어텐션 계산 로직 최적화.
  - 유형: 성능 최적화
  - 기여자: wzy3650
- 2025.02.12 [PR#2040](https://github.com/RVC-Boss/GPT-SoVITS/pull/2040): 파인튜닝 시 그래디언트 체크포인팅 지원 추가, 12GB VRAM 필요.
  - 유형: 신규 기능
  - 기여자: Kakaru Hayate
- 2025.02.14 [PR#2047](https://github.com/RVC-Boss/GPT-SoVITS/pull/2047), [PR#2062](https://github.com/RVC-Boss/GPT-SoVITS/pull/2062), [PR#2073](https://github.com/RVC-Boss/GPT-SoVITS/pull/2073): 새로운 언어 분할 도구 전환, 다국어 혼합 텍스트 분할 전략 개선, 숫자 및 영어 처리 로직 최적화.
  - 유형: 신규 기능
  - 기여자: KamioRinn
- 2025.02.23 [Commit#56509a17](https://github.com/RVC-Boss/GPT-SoVITS/commit/56509a17c918c8d149c48413a672b8ddf437495b)~[Commit#514fb692](https://github.com/RVC-Boss/GPT-SoVITS/commit/514fb692db056a06ed012bc3a5bca2a5b455703e): **GPT-SoVITS V3 모델 LoRA 학습 지원 추가, 파인튜닝 시 8GB GPU 메모리 필요.**
  - 유형: 신규 기능
  - 기여자: RVC-Boss
- 2025.02.23 [PR#2078](https://github.com/RVC-Boss/GPT-SoVITS/pull/2078): 보컬 및 악기 분리를 위한 Mel Band Roformer 모델 지원 추가.
  - 유형: 신규 기능
  - 기여자: Sucial
- 2025.02.26 [PR#2112](https://github.com/RVC-Boss/GPT-SoVITS/pull/2112), [PR#2114](https://github.com/RVC-Boss/GPT-SoVITS/pull/2114): 중국어 경로에서 MeCab 오류 수정 (일본어/한국어 또는 다국어 텍스트 분할 전용).
  - 유형: 수정
  - 기여자: KamioRinn
- 2025.02.27 [Commit#92961c3f](https://github.com/RVC-Boss/GPT-SoVITS/commit/92961c3f68b96009ff2cd00ce614a11b6c4d026f)~[Commit#250b1c73](https://github.com/RVC-Boss/GPT-SoVITS/commit/250b1c73cba60db18148b21ec5fbce01fd9d19bc): **24kHz에서 48kHz 오디오 초해상도 모델 추가** (V3 모델로 24K 오디오 생성 시 "뭉개지는" 현상 완화).
  - 유형: 신규 기능
  - 기여자: RVC-Boss
  - 관련: [Issue#2085](https://github.com/RVC-Boss/GPT-SoVITS/issues/2085), [Issue#2117](https://github.com/RVC-Boss/GPT-SoVITS/issues/2117)
- 2025.02.28 [PR#2123](https://github.com/RVC-Boss/GPT-SoVITS/pull/2123): 다국어 프로젝트 문서 업데이트.
  - 유형: 문서화
  - 기여자: StaryLan
- 2025.02.28 [PR#2122](https://github.com/RVC-Boss/GPT-SoVITS/pull/2122): 모델이 인식하지 못하는 짧은 CJK 문자에 대해 규칙 기반 검출 적용.
  - 유형: 수정
  - 기여자: KamioRinn
  - 관련: [Issue#2116](https://github.com/RVC-Boss/GPT-SoVITS/issues/2116)
- 2025.02.28 [Commit#c38b1690](https://github.com/RVC-Boss/GPT-SoVITS/commit/c38b16901978c1db79491e16905ea3a37a7cf686), [Commit#a32a2b89](https://github.com/RVC-Boss/GPT-SoVITS/commit/a32a2b893436fad56cc82409121c7fa36a1815d5): 음성 속도 제어 매개변수 추가.
  - 유형: 수정
  - 기여자: RVC-Boss
- 2025.02.28 **GPT-SoVITS V3 정식 출시**.

## 202503

- 2025.03.31 [PR#2236](https://github.com/RVC-Boss/GPT-SoVITS/pull/2236): 의존성 버전 오류로 인한 문제 수정.
  - 유형: 수정
  - 기여자: XXXXRT666
  - 관련:
    - PyOpenJTalk: [Issue#1131](https://github.com/RVC-Boss/GPT-SoVITS/issues/1131), [Issue#2231](https://github.com/RVC-Boss/GPT-SoVITS/issues/2231), [Issue#2233](https://github.com/RVC-Boss/GPT-SoVITS/issues/2233).
    - ONNX: [Issue#492](https://github.com/RVC-Boss/GPT-SoVITS/issues/492), [Issue#671](https://github.com/RVC-Boss/GPT-SoVITS/issues/671), [Issue#1192](https://github.com/RVC-Boss/GPT-SoVITS/issues/1192), [Issue#1819](https://github.com/RVC-Boss/GPT-SoVITS/issues/1819), [Issue#1841](https://github.com/RVC-Boss/GPT-SoVITS/issues/1841).
    - Pydantic: [Issue#2230](https://github.com/RVC-Boss/GPT-SoVITS/issues/2230), [Issue#2239](https://github.com/RVC-Boss/GPT-SoVITS/issues/2239).
    - PyTorch-Lightning: [Issue#2174](https://github.com/RVC-Boss/GPT-SoVITS/issues/2174).
- 2025.03.31 [PR#2241](https://github.com/RVC-Boss/GPT-SoVITS/pull/2241): **SoVITS v3 병렬 추론 지원 활성화.**
  - 유형: 신규 기능
  - 기여자: ChasonJiang

- 기타 사소한 버그 수정.

- ONNX 런타임 GPU 추론 지원을 위한 패키지 통합 수정:
  - 유형: 수정
  - 상세:
    - G2PW 내 ONNX 모델이 CPU에서 GPU 추론으로 전환, CPU 병목 현상 크게 감소;
    - foxjoy dereverberation 모델이 GPU 추론 지원.

## 202504 (V4 버전)

- 2025.04.01 [Commit#6a60e5ed](https://github.com/RVC-Boss/GPT-SoVITS/commit/6a60e5edb1817af4a61c7a5b196c0d0f1407668f): SoVITS v3 병렬 추론 잠금 해제; 비동기 모델 로딩 로직 수정.
  - 유형: 수정
  - 기여자: RVC-Boss
- 2025.04.07 [PR#2255](https://github.com/RVC-Boss/GPT-SoVITS/pull/2255): Ruff를 이용한 코드 포맷팅; G2PW 링크 업데이트.
  - 유형: 스타일
  - 기여자: XXXXRT666
- 2025.04.15 [PR#2290](https://github.com/RVC-Boss/GPT-SoVITS/pull/2290): 문서 정리; Python 3.11 지원 추가; 설치 프로그램 업데이트.
  - 유형: 정리 작업
  - 기여자: XXXXRT666
- 2025.04.20 [PR#2300](https://github.com/RVC-Boss/GPT-SoVITS/pull/2300): Colab, 설치 파일 및 모델 다운로드 업데이트.
  - 유형: 정리 작업
  - 기여자: XXXXRT666
- 2025.04.20 [Commit#e0c452f0](https://github.com/RVC-Boss/GPT-SoVITS/commit/e0c452f0078e8f7eb560b79a54d75573fefa8355)~[Commit#9d481da6](https://github.com/RVC-Boss/GPT-SoVITS/commit/9d481da610aa4b0ef8abf5651fd62800d2b4e8bf): **GPT-SoVITS V4 모델 추가.**
  - 유형: 신규 기능
  - 기여자: RVC-Boss
- 2025.04.21 [Commit#8b394a15](https://github.com/RVC-Boss/GPT-SoVITS/commit/8b394a15bce8e1d85c0b11172442dbe7a6017ca2)~[Commit#bc2fe5ec](https://github.com/RVC-Boss/GPT-SoVITS/commit/bc2fe5ec86536c77bb3794b4be263ac87e4fdae6), [PR#2307](https://github.com/RVC-Boss/GPT-SoVITS/pull/2307): V4 병렬 추론 지원 활성화.
  - 유형: 신규 기능
  - 기여자: RVC-Boss, ChasonJiang
- 2025.04.22 [Commit#7405427a](https://github.com/RVC-Boss/GPT-SoVITS/commit/7405427a0ab2a43af63205df401fd6607a408d87)~[Commit#590c83d7](https://github.com/RVC-Boss/GPT-SoVITS/commit/590c83d7667c8d4908f5bdaf2f4c1ba8959d29ff), [PR#2309](https://github.com/RVC-Boss/GPT-SoVITS/pull/2309): 모델 버전 매개변수 전달 오류 수정.
  - 유형: 수정
  - 기여자: RVC-Boss, ChasonJiang
- 2025.04.22 [Commit#fbdab94e](https://github.com/RVC-Boss/GPT-SoVITS/commit/fbdab94e17d605d85841af6f94f40a45976dd1d9), [PR#2310](https://github.com/RVC-Boss/GPT-SoVITS/pull/2310): Numpy와 Numba 버전 불일치 문제 수정; librosa 버전 업데이트.
  - 유형: 수정
  - 기여자: RVC-Boss, XXXXRT666
  - 관련: [Issue#2308](https://github.com/RVC-Boss/GPT-SoVITS/issues/2308)
- **2024.04.22 GPT-SoVITS V4 정식 출시**.
- 2025.04.22 [PR#2311](https://github.com/RVC-Boss/GPT-SoVITS/pull/2311): Gradio 매개변수 업데이트.
  - 유형: 정리 작업
  - 기여자: XXXXRT666
- 2025.04.25 [PR#2322](https://github.com/RVC-Boss/GPT-SoVITS/pull/2322): Colab/Kaggle 노트북 스크립트 개선.
  - 유형: 정리 작업
  - 기여자: XXXXRT666

## 202505

- 2025.05.26 [PR#2351](https://github.com/RVC-Boss/GPT-SoVITS/pull/2351): Docker 및 Windows 자동 빌드 스크립트 개선; pre-commit 포맷팅 추가.
  - 유형: 정리 작업
  - 기여자: XXXXRT666
- 2025.05.26 [PR#2408](https://github.com/RVC-Boss/GPT-SoVITS/pull/2408): 다국어 텍스트 분할 및 인식 로직 최적화.
  - 유형: 수정
  - 기여자: KamioRinn
  - 관련: [Issue#2404](https://github.com/RVC-Boss/GPT-SoVITS/issues/2404)
- 2025.05.26 [PR#2377](https://github.com/RVC-Boss/GPT-SoVITS/pull/2377): 캐싱 전략 구현으로 SoVITS V3/V4 추론 속도 10% 향상.
  - 유형: 성능 최적화
  - 기여자: Kakaru Hayate
- 2025.05.26 [Commit#4d9d56b1](https://github.com/RVC-Boss/GPT-SoVITS/commit/4d9d56b19638dc434d6eefd9545e4d8639a3e072), [Commit#8c705784](https://github.com/RVC-Boss/GPT-SoVITS/commit/8c705784c50bf438c7b6d0be33a9e5e3cb90e6b2), [Commit#fafe4e7f](https://github.com/RVC-Boss/GPT-SoVITS/commit/fafe4e7f120fba56c5f053c6db30aa675d5951ba): 어노테이션 인터페이스를 업데이트하여 안내 문구를 추가했습니다: 각 페이지 편집 후 반드시 'Submit Text'를 클릭해 주세요. 그렇지 않으면 변경 사항이 저장되지 않습니다.
  - 유형: 수정
  - 기여자: RVC-Boss
- 2025.05.29 [Commit#1934fc1e](https://github.com/RVC-Boss/GPT-SoVITS/commit/1934fc1e1b22c4c162bba1bbe7d7ebb132944cdc): UVR5 및 ONNX dereverberation 모델에서 FFmpeg이 공백 포함 원본 경로로 MP3/M4A 파일 인코딩 시 오류 수정.
  - 유형: 수정
  - 기여자: RVC-Boss

**미리보기: 단오절 이후 V2 버전 기반 대규모 최적화 업데이트 예정!**