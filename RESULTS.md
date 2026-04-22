# Results

## 1. 실험 요약
- 저장소: bench-runtime-shootout
- 커밋 해시: bb48657
- 실험 일시: 2026-04-22T07:25:23.219Z -> 2026-04-22T07:25:27.551Z
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
- adapter: synthetic-webgpu-profile, wasm-fallback-simulated
- backend: `webgpu, wasm`
- fallback triggered: `false, true`
- worker mode: `mixed, main`
- cache state: `warm`
- required features: ["shader-f16"], []
- limits snapshot: {}

## 4. 워크로드 정의
- 시나리오 이름: Runtime Benchmark Winner: ORT WebGPU-style / WebGPU, Runtime Benchmark Winner: ORT WebGPU-style / Fallback
- 입력 프로필: prompt-17-output-54
- 데이터 크기: ort-webgpu-style:ttft=20.1,decode=148.56,turn=456.2; webllm-style:ttft=22.3,decode=134.87,turn=519.2; transformersjs-style:ttft=17.2,decode=115.51,turn=550.2; executionMode=webgpu; backend=webgpu; automation=playwright-chromium, ort-webgpu-style:ttft=47.2,decode=63.34,turn=1025.1; webllm-style:ttft=52.2,decode=57.44,turn=1163.6; transformersjs-style:ttft=40.3,decode=49.72,turn=1240.7; executionMode=fallback; backend=wasm; automation=playwright-chromium
- dataset: -
- model_id 또는 renderer: ort-webgpu-style
- 양자화/정밀도: -
- resolution: -
- context_tokens: 17
- output_tokens: 54

## 5. 측정 지표
### 공통
- time_to_interactive_ms: 1688.2 ~ 3496.8 ms
- init_ms: 72.2 ~ 130.1 ms
- success_rate: 1
- peak_memory_note: 16 GB reported by browser
- error_type: -

### LLM / Benchmark
- ttft_ms: 20.1 ~ 47.2 ms
- prefill_tok_per_sec: 400 ~ 829.27 tok/s
- decode_tok_per_sec: 63.34 ~ 148.56 tok/s
- turn_latency_ms: 456.2 ~ 1025.1 ms
- backends: webgpu, wasm
- fallback states: false, true

## 6. 결과 표
| Run | Scenario | Backend | Cache | Mean | P95 | Notes |
|---|---|---:|---:|---:|---:|---|
| 1 | Runtime Benchmark Winner: ORT WebGPU-style / WebGPU | webgpu | warm | 148.56 | 20.1 | winner=Runtime Benchmark Winner: ORT WebGPU-style / WebGPU, metric=decode tok/s / TTFT ms |
| 2 | Runtime Benchmark Winner: ORT WebGPU-style / Fallback | wasm | warm | 63.34 | 47.2 | winner=Runtime Benchmark Winner: ORT WebGPU-style / Fallback, metric=decode tok/s / TTFT ms |

## 7. 관찰
- benchmark draft winner는 Runtime Benchmark Winner: ORT WebGPU-style / WebGPU였고 decode_tok_per_sec=148.56였다.
- 비교 세부값은 raw JSON meta.notes에 profile별 TTFT/decode/turn latency로 함께 남겼다.
- playwright-chromium로 수집된 automation baseline이며 headless=true, browser=Chromium 147.0.7727.15.
- 실제 runtime/model/renderer 교체 전 deterministic harness 결과이므로, 절대 성능보다 보고 경로와 재현성 확인에 우선 의미가 있다.

## 8. WebGPU vs Fallback
- fixed benchmark: webgpu winner=Runtime Benchmark Winner: ORT WebGPU-style / WebGPU, fallback winner=Runtime Benchmark Winner: ORT WebGPU-style / Fallback
- decode tok/s: webgpu=148.56, fallback=63.34, delta=+85.22
- TTFT: webgpu=20.1 ms, fallback=47.2 ms, delta=-27.1 ms

## 9. 결론
- fixed-scenario runtime benchmark draft가 raw artifact와 summary 문서 양쪽에서 재현 가능해졌다.
- fixed benchmark 한 벌에 대해 WebGPU vs fallback 비교 draft도 함께 누적할 수 있게 됐다.
- 다음 단계는 synthetic profile을 실제 runtime implementation으로 바꾸되 동일한 prompt/output budget을 유지하는 것이다.

## 10. 첨부
- 스크린샷: ./reports/screenshots/01-runtime-benchmark-webgpu.png, ./reports/screenshots/02-runtime-benchmark-fallback.png
- 로그 파일: ./reports/logs/01-runtime-benchmark-webgpu.log, ./reports/logs/02-runtime-benchmark-fallback.log
- raw json: ./reports/raw/01-runtime-benchmark-webgpu.json, ./reports/raw/02-runtime-benchmark-fallback.json
- 배포 URL: https://ai-webgpu-lab.github.io/bench-runtime-shootout/
- 관련 이슈/PR: -
