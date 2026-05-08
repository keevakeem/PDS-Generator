---
name: dashboard-card
description: Generate dashboard record cards for health data categories. Use this skill whenever the user asks to create a dashboard card, health record card, or data summary card — such as "식사 카드", "수면 카드", "혈당 카드", "대시보드 카드 만들어줘". Always consult this skill AND import tokens.css before generating any dashboard card UI.
---

# Dashboard Card Component (대시보드 기록 카드)

이 스킬은 디자인 시스템(design.md)을 기반으로 대시보드의 기록 카드 컴포넌트를 생성합니다. 토큰 값을 직접 하드코딩하지 말고, 아래 규칙과 토큰 이름을 그대로 사용하세요.

> 색상·스페이싱·타이포그래피 토큰은 `design.md`를 참조하세요.
> 임의의 hex 값, px 값, gray 계열 색상을 하드코딩하지 마세요.

---

## 카드 공통 구조

모든 카드는 아래 구조를 따릅니다.

```
┌─────────────────────────────┐
│ [아이콘]  카테고리명   [뱃지] │  ← Header
│                             │
│ 수치 또는 횟수               │  ← Value
│ 보조 정보 (시간, 단위 등)    │  ← Sub info
│                             │
│ [━━━━━━━━━━━━━━━━━━━━━━━━] │  ← Progress bar
└─────────────────────────────┘
```

---

## 카드 스펙

| 속성 | 값 |
|------|-----|
| 배경 | `var(--bg-elevation1)` |
| border-radius | 16px |
| 내부 패딩 | `var(--sp-16)` (16px) |
| 카드 간 간격 | `var(--sp-8)` (8px) |
| 최소 높이 | 120px |

---

## 영역별 토큰 적용

### Header 영역

| 요소 | 토큰 | 비고 |
|------|------|------|
| 카테고리 아이콘 | `var(--onSurface-tertiary)` | iconSize/24 (24px) |
| 카테고리명 | `var(--onSurface-tertiary)` | subHead Regular |
| 아이콘 ↔ 텍스트 간격 | `var(--sp-4)` | |

### 뱃지 (valueScore)

뱃지는 카드 우상단에 위치합니다. valueScore 토큰을 사용합니다.

| 뱃지 상태 | 배경 토큰 | 텍스트 토큰 | 텍스트 |
|----------|----------|------------|--------|
| 좋음 (5점) | `var(--vs-excellentBg)` | `var(--vs-excellent)` | 좋음 |
| 양호 (4점) | `var(--vs-goodBg)` | `var(--vs-good)` | 양호 |
| 보통 (3점) | `var(--vs-averageBg)` | `var(--vs-average)` | 보통 |
| 미흡 (2점) | `var(--vs-poorBg)` | `var(--vs-poor)` | 미흡 |
| 나쁨 (1점) | `var(--vs-badBg)` | `var(--vs-bad)` | 나쁨 |
| 없음 | 표시 안 함 | — | — |

뱃지 스펙:
- 폰트: caption Bold (11px)
- 패딩: `var(--sp-4)` 상하, `var(--sp-8)` 좌우
- border-radius: 999px (pill)
- 아이콘: 카테고리 아이콘과 동일 색상, iconSize/16 (16px), 뱃지 텍스트 앞

### Value 영역

| 요소 | 토큰 | 비고 |
|------|------|------|
| 주요 수치 | `var(--onSurface-primary)` | title2 Bold (22px) |
| 단위 | `var(--onSurface-tertiary)` | subHead Regular |
| 보조 정보 (시간, 마지막 기록 등) | `var(--onSurface-fourth)` | caption Regular (11px) |
| 미입력 상태 (`--`) | `var(--onSurface-fourth)` | title2 Bold |

### Progress Bar

| 요소 | 토큰 | 비고 |
|------|------|------|
| 트랙 (배경) | `var(--onSurface-secondaryLine)` | 높이 4px, border-radius 999px |
| 채워진 부분 | 카테고리별 색상 (아래 참조) | 높이 4px |
| 횟수 텍스트 (N/N회) | `var(--onSurface-fourth)` | caption Regular |

---

## 카테고리별 스펙

### 식사 (Food)

| 속성 | 값 |
|------|-----|
| 아이콘 | ic_fork_knife |
| Progress 색상 | `var(--pghd-food-carbs)` (#FFCD75, yellow) |
| Value 표시 | 칼로리 또는 N / 3회 |
| 뱃지 | valueScore 사용 |
| 보조 정보 | 마지막 식사 시간 (아침/점심/저녁/간식) |

### 체중 (Weight)

| 속성 | 값 |
|------|-----|
| 아이콘 | ic_scale |
| Progress 색상 | `var(--onSurface-tertiary)` |
| Value 표시 | N.N kg |
| 뱃지 | 목표 대비 피드백 (감소/유지/증가, valueScore 매핑) |
| 보조 정보 | 마지막 기록 시간 |

### 운동 (Exercise)

| 속성 | 값 |
|------|-----|
| 아이콘 | ic_figure_walk |
| Progress 색상 | `var(--vs-good)` (#4CDC42, green) |
| Value 표시 | N / 1회 |
| 뱃지 | 도전 / 진행 / 달성 / 없음 |
| 보조 정보 | — |

뱃지 색상 예외 (운동은 valueScore 대신 별도):

| 상태 | 배경 | 텍스트 |
|------|------|--------|
| 도전 | `var(--vs-poorBg)` | `var(--vs-poor)` |
| 진행 | `var(--vs-averageBg)` | `var(--vs-average)` |
| 달성 | `var(--vs-goodBg)` | `var(--vs-good)` |

### 수면 (Sleep)

| 속성 | 값 |
|------|-----|
| 아이콘 | ic_moon |
| Progress 색상 | `var(--pghd-sleep-regular)` (#00B6FF, blue) |
| Value 표시 | N / 8시간 |
| 뱃지 | 좋음 / 보통 / 아이쪽 (valueScore 매핑) |
| 보조 정보 | — |

> **규칙:** 수면이 n개일 경우, 수면 카드 오른쪽 상단의 뱃지는 수면 총점을 기준으로 표현됩니다.

### 복약 (Medication)

| 속성 | 값 |
|------|-----|
| 아이콘 | ic_pill |
| Progress 색상 | `var(--onSurface-tertiary)` |
| Value 표시 | N회 + 마지막 기록 시간 |
| 뱃지 | 없음 |

### 인슐린 (Insulin)

| 속성 | 값 |
|------|-----|
| 아이콘 | ic_syringe |
| Progress 색상 | `var(--onSurface-tertiary)` |
| Value 표시 | N U + 투약량 |
| 보조 정보 | 마지막 기록 시간 |
| 뱃지 | 없음 |

### 비만 주사 (Obesity Injection)

| 속성 | 값 |
|------|-----|
| 아이콘 | ic_syringe |
| Progress 색상 | `var(--onSurface-tertiary)` |
| Value 표시 | DD일 후 / MM.DD PM 01:41 |
| 보조 정보 | 예정된 주사 일정 / 이전에 맞은 주사 일정 |
| MEMO | 키는 null일 때 unit만 등장할 수 있도록 |
| 뱃지 | 없음 |

### 혈당 (Glucose) — 수동 PGHD only

| 속성 | 값 |
|------|-----|
| 아이콘 | ic_drop |
| Progress 색상 | `var(--glucose-targetRange)` (#95DEFF, blue) |
| Value 표시 | N mg/dL |
| 보조 정보 | 마지막 기록 시간 |
| 뱃지 | 없음 (수동 입력 데이터만) |

> **규칙:** 이 카드는 PGHD(수동) 혈당 기록 카드입니다. CGM(수동) 데이터는 별도입니다.

### 스트레스 (Stress)

| 속성 | 값 |
|------|-----|
| 아이콘 | ic_brain |
| Progress 색상 | `var(--pghd-food-fat)` (#FF6399, pink) |
| Value 표시 | N / 1회 |
| 뱃지 | 없음 |

### 혈압 (Pressure)

| 속성 | 값 |
|------|-----|
| 아이콘 | ic_heart |
| Progress 색상 | `var(--pghd-pressure-pulseLine)` (#4CDC42, green) |
| Value 표시 | NNN/NN mmHg + N mmHg (pulse) |
| 보조 정보 | 마지막 기록 시간 |
| 뱃지 | 없음 |

---

## 미입력 상태

값이 없는 경우:
- 수치: `--` (onSurface/fourth)
- 보조 정보: `--`
- Progress bar: 트랙만 표시, 채워진 부분 없음
- 뱃지: 표시 안 함

---

## 대시보드 공통 정책

- **서비스 기준 횟수는 유지**: 사용자가 서비스 기준 횟수 이상을 남겼을 경우 그대로 표기
- **우선 적용 카드**: 식사, 체중, 운동, 수면 (항상 상단 노출)
- **추후 진행 카드**: 복약, 인슐린, 비만주사, 혈당, 스트레스, 혈압

---

## AI 규칙 요약

1. **카드 배경은 `var(--bg-elevation1)`** — surface나 elevation2 사용 금지
2. **뱃지는 valueScore 토큰** — 임의 색상으로 상태 표현 금지
3. **Progress bar 높이는 4px 고정** — 임의 조정 금지
4. **미입력 수치는 `--`** — null, 0, N/A 등 다른 표현 사용 금지
5. **혈당 정상 범위는 blue** — green으로 표현하지 말 것
6. **운동 뱃지는 valueScore 토큰 재활용** — 별도 색상 정의 금지
7. **카드 간 간격은 `var(--sp-8)`** — 임의 간격 사용 금지
