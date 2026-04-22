# Results

## 1. 실험 요약
- 저장소: bench-runtime-shootout
- 커밋 해시: b9359b1
- 실험 일시: 2026-04-22T06:14:20.229Z -> 2026-04-22T06:14:20.229Z
- 담당자: ai-webgpu-lab
- 실험 유형: `benchmark`
- 상태: `success`

## 2. 질문
- 동일 prompt/output budget에서 runtime profile별 상대 우위를 단일 benchmark draft로 고정할 수 있는가
- winner selection과 비교 메모가 raw JSON과 RESULTS.md 양쪽에 일관되게 남는가
- 실제 runtime 교체 전 fixed-scenario benchmark protocol이 재현 가능한가

## 3. 실행 환경
### 브라우저
- 이름: Chrome
- 버전: 147.0.7727.15

### 운영체제
- OS: Linux
- 버전: unknown

### 디바이스
- 장치명: Linux x86_64
- device class: `desktop-high`
- CPU: 16 threads
- 메모리: 16 GB
- 전원 상태: `unknown`

### GPU / 실행 모드
- adapter: profile-driven
- backend: `mixed`
- fallback triggered: `false`
- worker mode: `mixed`
- cache state: `warm`
- required features: []
- limits snapshot: {}

## 4. 워크로드 정의
- 시나리오 이름: Runtime Benchmark Winner: ORT WebGPU-style
- 입력 프로필: prompt-17-output-54
- 데이터 크기: ort-webgpu-style:ttft=20.1,decode=146.98,turn=460.8; webllm-style:ttft=22.2,decode=133.9,turn=522.1; transformersjs-style:ttft=17.2,decode=115.04,turn=552.7; automation=playwright-chromium
- dataset: -
- model_id 또는 renderer: ort-webgpu-style
- 양자화/정밀도: -
- resolution: -
- context_tokens: 17
- output_tokens: 54

## 5. 측정 지표
### 공통
- time_to_interactive_ms: 1627.4 ms
- init_ms: 72.6 ms
- success_rate: 1
- peak_memory_note: 16 GB reported by browser
- error_type: -

### LLM / Benchmark
- ttft_ms: 20.1 ms
- prefill_tok_per_sec: 817.31 tok/s
- decode_tok_per_sec: 146.98 tok/s
- turn_latency_ms: 460.8 ms

## 6. 결과 표
| Run | Scenario | Backend | Cache | Mean | P95 | Notes |
|---|---|---:|---:|---:|---:|---|
| 1 | Runtime Benchmark Winner: ORT WebGPU-style | mixed | warm | 146.98 | 20.1 | winner=Runtime Benchmark Winner: ORT WebGPU-style, metric=decode tok/s / TTFT ms |

## 7. 관찰
- benchmark draft winner는 Runtime Benchmark Winner: ORT WebGPU-style였고 decode_tok_per_sec=146.98였다.
- 비교 세부값은 raw JSON meta.notes에 profile별 TTFT/decode/turn latency로 함께 남겼다.
- playwright-chromium로 수집된 automation baseline이며 headless=true, browser=Chromium 147.0.7727.15.
- 실제 runtime/model/renderer 교체 전 deterministic harness 결과이므로, 절대 성능보다 보고 경로와 재현성 확인에 우선 의미가 있다.

## 8. 결론
- fixed-scenario runtime benchmark draft가 raw artifact와 summary 문서 양쪽에서 재현 가능해졌다.
- 다음 단계는 synthetic profile을 실제 runtime implementation으로 바꾸되 동일한 prompt/output budget을 유지하는 것이다.
- benchmark summary v1을 만들려면 추가 브라우저와 cache-state 반복 측정이 필요하다.

## 9. 첨부
- 스크린샷: ./reports/screenshots/01-runtime-benchmark.png
- 로그 파일: ./reports/logs/01-runtime-benchmark.log
- raw json: ./reports/raw/01-runtime-benchmark.json
- 배포 URL: https://ai-webgpu-lab.github.io/bench-runtime-shootout/
- 관련 이슈/PR: -
