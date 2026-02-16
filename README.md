# Launchrail Operator Dashboard — Phase 1.2

**STEP 3 합성 보고서 무결성 감시기**

---

## 📌 이 대시보드는 무엇인가?

**STEP 3 합성 보고서 검수기입니다.**

완성된 STEP 3 보고서의 구조 무결성을 검증하고, 자동 Gate 판정으로 PASS/REWORK/DROP을 결정하며, 판정 기록을 누적하는 도구입니다.

### 명확한 역할 분리

```
설계 생성 (외부) → STEP 3 합성 (외부) → 대시보드 검수 (여기) → 기록 누적
```

**이 대시보드가 하는 일:**
- ✅ STEP 3 보고서 구조 형식 검사 (PART 0~4)
- ✅ 6대 심사축 존재 확인
- ✅ FINAL VERDICT / 영향 추적 / Sealing 검사
- ✅ Minimal Gate 자동 판정 (PASS/REWORK/DROP)
- ✅ Preview 출력 자동 판정
- ✅ 판정 기록 누적 + JSON 백업

**이 대시보드가 하지 않는 일:**
- ❌ 설계 생성
- ❌ 설계 수정 제안
- ❌ 수동 점수 기반 판정 (제거됨)

---

## 🎯 Phase 1.2 범위

**작동:**
- ✅ Infinity 검수 → Minimal Gate 5-Gate 자동 판정
- ✅ Preview 검수 → 3-Gate 자동 판정
- ✅ Pre-build 신호 감지
- ✅ Boundary Log (검수 기록)

**미구축:**
- ❌ Compiler: NOT BUILT
- ❌ Execution OS: NOT BUILT

---

## 🚀 빠른 시작

1. **dashboard.html** 파일을 더블클릭
2. 브라우저에서 자동 실행
3. 바로 검수 시작

---

## 📝 사용 방법

### 1️⃣ STEP 3 합성 보고서 완성 (외부 작업)

```
STEP 3 프롬프트로 합성 보고서 생성
→ PART 0~4, FINAL VERDICT 포함
→ 복사
```

### 2️⃣ Infinity 검수 (STEP 3 무결성)

```
1. STEP 3 합성 보고서 붙여넣기
2. "검수 시작" 클릭
3. 자동 형식 검사 5개 영역 확인
4. Minimal Gate 자동 판정 확인: PASS / REWORK / DROP
```

### 3️⃣ Preview 검수

```
1. Preview JSON 붙여넣기
2. "검수 시작" 클릭
3. 자동 3-Gate 판정: PASS / REWORK
```

### 4️⃣ 기록 추가

```
"현재 검수 기록 추가" 버튼
→ localStorage 자동 저장
→ JSON 파일 자동 다운로드
```

---

## 🔍 Infinity 자동 형식 검사 (5개 영역)

### ① PART 구조 (엄격)
- PART 0~4 존재 여부 (정규식)
- PART 0: Mandatory Injection Block 확인
- 대괄호/콜론/하이픈/공백 변형 모두 허용
- **1개라도 없으면 → 구조 FAIL**

### ② 6대 심사축 (PART 1)
- JJO 7-Layer 무결성
- No-Employee Operation Test
- Pre-built 반복판매 적합성
- 리스크 구조
- 운영자 관점 적합성
- 최악 시나리오/스트레스 테스트
- **4개 미만 → FAIL**

### ③ FINAL VERDICT (엄격)
- PASS / REWORK / CUSTOM-ONLY / DROP 중 정확히 1개
- **0개 또는 2개 이상 → FAIL**

### ④ 영향 추적 블록 (경고 수준)
- STEP 2 반영, Slot A/B, 제거/축소/강화, 책임 경계 태그
- **1개 이상 존재 → Gate 통과**

### ⑤ Sealing 영역 (경고 수준)
- v1.0 동결, v1.x 실험, v2.0 변경, 변경 불가, 조건부 변경, 승인 필수
- **1개 이상 존재 → Gate 통과**

---

## 🚦 Infinity Minimal Gate 판정

| 판정 | 조건 |
|------|------|
| **PASS** | 5개 Gate 전부 통과 |
| **REWORK** | 1개 이상 미통과 (단, PART/VERDICT는 있음) |
| **DROP** | PART 구조 누락 또는 FINAL VERDICT 미존재 |

수동 체크 없음. 자동 검사 결과만으로 즉시 판정.

---

## 🖥️ Preview 자동 판정

### 3개 Gate
1. **5개 섹션** — Global Status, One Thing, Signal, History, Reasoning
2. **5개 필드** — status, headline, one_thing, signals, reasoning
3. **상태코드** — OK/Warning/Action만 허용 (Error/Fail 금지)

| 판정 | 조건 |
|------|------|
| **PASS** | 3개 Gate 전부 통과 |
| **REWORK** | 1개라도 미통과 |

---

## 💾 저장 방식

### 1. 자동 저장 (실시간)
- localStorage — 입력/검수 시 자동 저장, 새로고침 복구

### 2. 개별 백업 (기록 추가 시)
- JSON 파일 자동 다운로드 → `backups/` 폴더로 이동 권장

### 3. 전체 백업 (수동)
- "JSON 저장" 버튼 → 전체 데이터 + 모든 기록 포함

### 4. GitHub 저장 (주간)
- `backups/` 폴더째로 주 1회 push 권장

---

## 📂 폴더 구조

```
launchrail-operator-dashboard/
├── dashboard.html
├── README.md
└── backups/
    ├── launchrail_log_2026-02-15_LR-01.json
    └── launchrail_전체백업_2026-02-15.json
```

---

## ⚠️ 주의사항

### 구조 FAIL 기준
- PART + VERDICT = 엄격 (없으면 DROP)
- 심사축 = 4개 이상 필요
- 영향 추적 + Sealing = 1개 이상이면 Gate 통과

### localStorage 주의
- 브라우저 캐시 삭제 시 데이터 소실
- 반드시 JSON 백업 유지
- 다른 브라우저는 데이터 공유 안 됨

### 별도 저장소
- Preview Engine: `launchrail-preview-engine` 저장소
- Operator Dashboard: `launchrail-operator-dashboard` 저장소 (여기)

---

## 🎯 핵심 원칙

**1. 대시보드는 검수만 한다** — 생성 ❌ / 수정 제안 ❌

**2. 판정은 자동 Gate** — 수동 체크 제거, 5개/3개 Gate로 즉시 판정

**3. 최종 판단 권한은 운영자** — Gate는 참고, 최종 결정은 Jiyu

**4. 기록이 자산이다** — 매 검수마다 JSON 백업, 장기 패턴 분석 준비

---

## 🔄 변경 이력

| 버전 | 날짜 | 내용 |
|------|------|------|
| Phase 1.0 | 2026-02-13 | 초기 버전. PART 0~9 + JJO 7-Layer + Tier 검사 + 수동 12개 체크 |
| Phase 1.1 | 2026-02-15 | STEP 3 무결성 감시기로 전환. PART 0~4, 6대 심사축, FINAL VERDICT, 영향 추적, Sealing 검사 추가 |
| Phase 1.2 | 2026-02-15 | Minimal Gate Logic 전환. Infinity 5-Gate + Preview 3-Gate 자동 판정. 수동 체크박스 전량 제거. global 섹션 인식 수정. 판정 순서 버그 수정 |

---

**Made with JJO System™ — Launchrail 2026**
