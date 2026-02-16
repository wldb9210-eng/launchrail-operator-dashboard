# Launchrail Operator Dashboard — Phase 1.1

**STEP 3 합성 보고서 무결성 감시기**

---

## 📌 이 대시보드는 무엇인가?

**STEP 3 합성 보고서 검수기입니다.**

완성된 STEP 3 보고서의 구조 무결성을 검증하고, 합성 품질 이탈을 감지하며, 판정 기록을 누적하는 도구입니다.

### 명확한 역할 분리

```
설계 생성 (외부) → STEP 3 합성 (외부) → 대시보드 검수 (여기) → 기록 누적
```

**이 대시보드가 하는 일:**
- ✅ STEP 3 보고서 구조 형식 검사 (PART 0~4)
- ✅ 6대 심사축 존재 확인
- ✅ FINAL VERDICT / 영향 추적 / Sealing 검사
- ✅ 합성 품질 이탈 감지 (수동 12개 항목)
- ✅ Preview 출력 동결 검수
- ✅ 판정 기록 누적 + JSON 백업

**이 대시보드가 하지 않는 일:**
- ❌ 설계 생성
- ❌ 설계 수정 제안
- ❌ 자동 점수 기반 최종 판정

---

## 🎯 Phase 1.1 범위

**작동:**
- ✅ Infinity 검수 → STEP 3 무결성 감시로 전환 완료
- ✅ Preview 검수 (출력 동결) — 기존 유지
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

### 2️⃣ 대시보드 검수

**① 기본 정보 입력**
```
작업 ID: LR-2026-02-15-01
설계 타입: No-show prevention
반복 횟수: 1
커스텀 레벨: LOW
```

**② Infinity 검수 (STEP 3 무결성)**
```
1. STEP 3 합성 보고서 붙여넣기
2. "검수 시작" 클릭
3. 자동 형식 검사 5개 영역 확인:
   ① PART 0~4 구조
   ② 6대 심사축
   ③ FINAL VERDICT
   ④ 영향 추적 블록
   ⑤ Sealing 영역
4. 수동 이탈 감지 12개 체크
5. 판정 확인: PASS / REWORK / DROP
```

**③ Preview 검수 (Infinity PASS 후)**
```
1. Preview 결과물 붙여넣기
2. "검수 시작" 클릭
3. 5개 섹션 + 필드명 + 상태코드 검사
4. 판정 확인
```

**④ 기록 추가**
```
"현재 검수 기록 추가" 버튼
→ localStorage 자동 저장
→ JSON 파일 자동 다운로드
```

---

## 🔍 자동 형식 검사 (5개 영역)

### ① PART 구조 (엄격)

- PART 0~4 존재 여부 (정규식)
- PART 0: Mandatory Injection Block 확인
- **1개라도 없으면 → 구조 FAIL**
- 오타 변형 허용 (Part 0, PART0: 등)

### ② 6대 심사축 (PART 1)

- JJO 7-Layer 무결성
- No-Employee Operation Test
- Pre-built 반복판매 적합성
- 리스크 구조
- 운영자 관점 적합성
- 최악 시나리오/스트레스 테스트
- **4개 미만 → FAIL / 4~5개 → OK / 6개 → 완전**

### ③ FINAL VERDICT (엄격)

- PASS / REWORK / CUSTOM-ONLY / DROP 중 정확히 1개
- **0개 → FAIL**
- **2개 이상 → FAIL**

### ④ 영향 추적 블록 (경고 수준)

- STEP 2 반영 항목
- Slot A / Slot B 영향
- 제거/축소/강화 내역
- 합성 책임 경계 태그
- **없어도 FAIL 아님, 경고 표시**

### ⑤ Sealing 영역 (경고 수준)

- v1.0 동결 영역
- v1.x 실험 가능 영역
- v2.0에서만 변경 가능 영역
- 변경 불가 영역
- 조건부 변경 가능 영역
- 승인 필수 영역
- **없어도 FAIL 아님, 경고 표시**

---

## ✋ 수동 판단 영역 (합성 품질 감시 12개)

```
[ ] 심사축 간 결론 충돌 존재
[ ] FINAL VERDICT와 심사축 결론 불일치
[ ] Slot A/B 영향 범위 누락 또는 과장
[ ] 제거/축소 내역의 근거 불명확
[ ] Sealing 영역 분류 기준 모호
[ ] 합성 책임 경계 태그 누락
[ ] STEP 2 반영 항목과 실제 반영 불일치
[ ] 운영자 관점 적합성 검토 부실
[ ] 최악 시나리오 깊이 부족
[ ] No-Employee Operation 위반 구간 존재
[ ] 리스크가 명시되었으나 대응 없음
[ ] Pre-built 반복판매 구조 훼손
```

**판정 기준:**
```
구조 OK + 이탈 0개 = PASS
구조 OK + 이탈 1-2개 = REWORK
구조 OK + 이탈 3개 이상 = DROP

구조 FAIL = 최소 REWORK (PASS 불가)
```

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
    ├── launchrail_log_2026-02-15_LR-02.json
    └── launchrail_전체백업_2026-02-15.json
```

---

## ⚠️ 주의사항

### 구조 FAIL 기준
- PART + VERDICT = 엄격 (없으면 FAIL)
- 영향 추적 + Sealing = 느슨 (없으면 경고)
- 오타 한 개로 FAIL 안 남 (변형 허용)

### localStorage 주의
- 브라우저 캐시 삭제 시 데이터 소실
- 반드시 JSON 백업 유지
- 다른 브라우저는 데이터 공유 안 됨

### 별도 저장소
- 이 대시보드는 Preview Engine과 별개
- Preview Engine: `launchrail-preview-engine` 저장소
- Operator Dashboard: `launchrail-operator-dashboard` 저장소 (여기)

---

## 🎯 핵심 원칙

**1. 대시보드는 검수만 한다** — 생성 ❌ / 수정 제안 ❌

**2. 최종 판단은 항상 운영자** — 자동 검사는 형식만, 판정 권한은 Jiyu

**3. 기록이 자산이다** — 매 검수마다 JSON 백업, 장기 패턴 분석 준비

---

## 🔄 변경 이력

| 버전 | 날짜 | 내용 |
|------|------|------|
| Phase 1.0 | 2026-02-13 | 초기 버전. PART 0~9 + JJO 7-Layer + Tier 검사 |
| Phase 1.1 | 2026-02-15 | STEP 3 무결성 감시기로 전환. PART 0~4, 6대 심사축, FINAL VERDICT, 영향 추적, Sealing 검사 추가. 수동 체크박스 12개 합성 품질 감시용으로 교체 |

---

**Made with JJO System™ — Launchrail 2026**
