# Design System — Color · Typography · Spacing

> **이 문서는 AI(LLM, Cursor, Copilot 등)가 읽기 위한 디자인 컨텍스트 문서입니다.**
> 컴포넌트를 생성하거나 색상을 선택할 때 토큰 값보다 이 문서의 **의도(intent)**를 우선적으로 참고하세요.

---

## 브랜드 철학

이 제품은 혈당·수면·혈압·식단 등 사용자의 건강 데이터를 실시간으로 보여주는 헬스케어 앱입니다.

색상 시스템의 핵심 원칙은 **"신뢰감과 안정감"**입니다.

- 사용자는 민감한 건강 수치를 마주합니다. 색상이 불필요한 불안을 유발해서는 안 됩니다.
- 위험 수치(혈당 매우 높음, 혈압 초과)는 명확히 구분되어야 하지만, **경고보다는 정보 전달**의 톤을 유지합니다.
- Primary 색상인 **Yellow(`#FFCA00`)**는 따뜻하고 긍정적인 에너지를 상징합니다. 어두운 배경 위에서 높은 가시성을 확보하며, 사용자의 액션을 유도하는 CTA에만 사용됩니다.
- 배경은 깊은 블랙(`#000000`, Dark 모드 기본)을 사용해 데이터 시각화가 중심이 되도록 합니다.

---

## 테마 모드

이 시스템은 **3가지 테마 모드**를 지원합니다. 기본값은 `Dark`입니다.

| 모드 | 특징 | 배경색 |
|------|------|--------|
| `Dark` | 기본 모드. 어두운 환경(야간, CGM 모니터링)에 최적화 | `#000000` |
| `Light` | 밝은 환경 사용. 텍스트 대비를 반전해 가독성 확보 | `#F4F3F3` |


> **AI 규칙:** 모드를 명시하지 않으면 항상 `Dark` 기준으로 색상을 선택하세요.

---

## 색상 구조

토큰은 3계층으로 구성됩니다.

```
base      →  원시 팔레트 (gray, yellow, red, blue, green, orange, pink)
core      →  브랜드 핵심 색상 (primary, error, white, black + opacity variants)
semantic  →  사용 목적별 토큰 (background, onSurface, button, glucose, PGHD 등)
```

> **AI 규칙:** 컴포넌트 코드에서는 반드시 `semantic` 토큰을 사용하세요. `base` 토큰을 직접 참조하지 마세요.

---

## Core 색상

### Primary — `#FFCA00` (Yellow)

브랜드의 핵심 색상입니다. **CTA 버튼, 탭 선택 상태, 주요 강조**에만 사용합니다.

| 토큰 | Dark | Light | 용도 |
|------|------|-------|------|
| `core/primary` | `#FFCA00` | `#DB9800` | 주요 액션, 탭 활성 |
| `core/primaryT20` | `#FFCA00` @ 20% | `#FFCA00` @ 20% | 비활성 강조, 오버레이 |
| `core/primaryBright` | `#FEE500` | `#FEE500` | 밝은 강조, 뱃지 |

> **AI 규칙:** Primary yellow는 배경에 절대 사용하지 마세요. CTA와 선택 상태에만 사용합니다.
> `onPrimary`(버튼 위 텍스트)는 Dark 모드에서 `#3F0000`(매우 어두운 갈색)을 사용합니다 — 흰색이 아닙니다.

### Error — `#FF4E32`

오류, 입력 실패, 시스템 에러에만 사용합니다. 혈당 위험 수치와 혼동하지 마세요 (혈당은 `glucose` 토큰 사용).

---

## Background 색상

배경은 **콘텐츠 계층 구조**를 표현합니다. elevation 숫자가 높을수록 위에 떠 있는 레이어입니다.

| 토큰 | Dark | Light | 설명 |
|------|------|-------|------|
| `background/bg` | `#000000` | `#F4F3F3` | 최하단 앱 배경 |
| `background/surface` | `#000000` | `#F4F3F3` | 기본 컨텐츠 영역 |
| `background/elevation1` | `#1A1919` | `#FAFAFA` | 카드, 시트 레이어 1 |
| `background/elevation2` | `#2A2828` | `#FFFFFF` | 모달, 팝업 레이어 2 |
| `background/dim` | `#000000` @ 60% | `#000000` @ 60% | 모달 뒤 딤 처리 |
| `background/alwaysDarkBg` | `#000000` | `#000000` | 테마 무관 항상 다크 |
| `background/alwaysLightBg` | `#F4F3F3` | `#F4F3F3` | 테마 무관 항상 라이트 |
| `background/invertBg` | `#F4F3F3` | `#000000` | 테마와 반전되는 배경 |

> **AI 규칙:** 카드 컴포넌트는 `elevation1`, 그 위에 뜨는 모달/드로어는 `elevation2`를 사용하세요.

---

## onSurface — 텍스트 & 아이콘 색상

배경 위에 올라오는 텍스트/아이콘의 계층을 정의합니다. 숫자는 회색 팔레트 기준 명도값입니다.

| 토큰 | 용도 | Dark | Light |
|------|------|------|-------|
| `onSurface/primary` | 제목, 주요 텍스트 | `#F4F3F3` | `#1A1919` |
| `onSurface/secondary` | 본문, 설명 텍스트 | `#D7D5D5` | `#3E3C3C` |
| `onSurface/tertiary` | 보조 아이콘, 힌트 | `#A6A1A1` | `#8A8585` |
| `onSurface/fourth` | 비활성, 플레이스홀더 | `#757171` | `#BEBBBB` |
| `onSurface/line` | 구분선 (primary) | `#F4F3F3` @ 20% | `#1A1919` @ 20% |
| `onSurface/secondaryLine` | 구분선 (secondary) | `#F4F3F3` @ 10% | `#1A1919` @ 10% |
| `onSurface/tertiaryLine` | 구분선 (tertiary, 미세) | `#F4F3F3` @ 5% | `#1A1919` @ 5% |
| `onSurface/invertPrimary` | invertBg 위에 표현되는 텍스트에 사용 | `#1A1919` | `#F4F3F3` |

> **AI 규칙:** 텍스트 계층은 반드시 이 4단계를 따르세요. 임의의 gray 값을 사용하지 마세요.

---

## Button 색상

버튼은 **3종류(primary / secondary / tertiary) × 3상태(active / press / inactive)**로 정의됩니다.

### Active 상태

| 토큰 | Dark | Light | 역할 |
|------|------|-------|------|
| `button/active/primary` | `#FFCA00` | `#FFCA00` | 주요 CTA 버튼 배경 |
| `button/active/onPrimary` | `#3F0000` | `#5D1100` | 주요 CTA 버튼 위 텍스트 |
| `button/active/secondary` | `#FFE6B4` | `#FFE7AA` | 보조 버튼 배경 |
| `button/active/tertiary` | `#565252` | `#E4E2E2` | 3차 버튼 배경 |
| `button/active/opacity` | `#FFCA00` @ 20% | `#FFCA00` @ 20% | 투명 강조 버튼 배경 |

> **AI 규칙:** Primary 버튼 위 텍스트는 흰색(`#FFFFFF`)이 아닌 `onPrimary`(`#3F0000`)를 사용합니다. 이는 yellow 배경 대비 가독성을 위한 의도적 선택입니다.

### Press / Inactive 상태

Press 상태는 active 대비 약간 어두운 yellow를 사용합니다 (`#FFB300`). Inactive 상태는 gray 계열로 전환되어 비활성임을 표현합니다.

---

## Glucose (혈당) 색상

혈당 수치 시각화에 사용되는 의미론적 색상입니다. 위험도에 따라 명확히 구분됩니다.

| 상태 | 토큰 | Dark | Light | 의미 |
|------|------|------|-------|------|
| Very High | `glucose/veryHigh` | `#FF003E` | `#FF2E22` | 심각한 고혈당 |
| High | `glucose/high` | `#FF7444` | `#FF9350` | 주의 필요 고혈당 |
| Target Range | `glucose/targetRange` | `#95DEFF` | `#008AFF` | 정상 범위 (파랑) |
| Low | `glucose/low` | `#FF007B` | `#FF0C95` | 저혈당 |
| Very Low | `glucose/veryLow` | `#FF6399` | `#FF84BF` | 심각한 저혈당 |

각 상태에 대응하는 `*Bg` 토큰(예: `glucose/veryHighBg`)은 배경 오버레이(opacity 16%)로 사용됩니다.

> **AI 규칙:**
> - 혈당 정상 범위는 `blue` 계열입니다. "정상 = 초록"으로 가정하지 마세요.
> - 위험 수치 표시에는 반드시 `glucose/*` 토큰을 사용하세요. `error` 토큰과 혼용 금지.
> - 배경 영역은 반드시 `*Bg` 토큰을 사용하고, 수치 텍스트/아이콘은 `*` 토큰을 사용하세요.

---

## PGHD (Patient Generated Health Data) 색상

사용자가 직접 기록한 건강 데이터 카테고리별 색상입니다.

### 식단 (Food)

| 상태 | 토큰 | Dark | Light | 의미 |
|------|------|------|-------|------|
| 탄수화물 | `PGHD/food/carbs` | `#FFCD75` (yellow) | `#FFCE5A` (yellow) |탄수화물 섭취량 그래프에 사용 |
| 단백질 | `PGHD/food/protein` | `#FF926A` (orange) | `#FF9350` (orange) |단백질 섭취량 그래프에 사용 |
| 지방 | `PGHD/food/fat` | `#FF6399` (pink) | `#FF84BF` (pink) |지방 섭취량 그래프에 사용 |

### 수면 (Sleep)

| 상태 | 토큰 | Dark | Light | 의미 |
|------|------|------|-------|------|
| 깨어있음 | `PGHD/sleep/awake` | `#FFCD75` (yellow) | `#FFCE5A` (yellow) |자다 깬 상태 |
| REM 수면 | `PGHD/sleep/rem` | `#ABE7FF` (light blue) |`#9FD3FF` (light blue) |렘수면 상태 |
| 일반 수면 | `PGHD/sleep/regular` | `#00B6FF` (blue) |`#4CA3FF` (blue) |일반 수면 상태 |
| 깊은 수면 | `PGHD/sleep/deep` | `#0067A8` (dark blue) |`#0061CD` (dark blue) |깊은 수면 상태 |

> **AI 규칙:** 수면 단계는 blue 계열 명도 차이로 깊이를 표현합니다. 임의로 다른 색상 계열을 추가하지 마세요.

### 혈압 (Pressure)

| 상태 | 토큰 | Dark |Light | 의미 |
|------|------|------|------|------|
| 맥박 라인 | `PGHD/pressure/pulseLine` | `#4CDC42` (green) |`#5FDA6B` (green) | BPM Line |
| 정상 범위 | `PGHD/pressure/targetRange` | `#95DEFF` (blue) |`#008AFF` (blue) |혈압 기준 이내|
| 수축기 초과 | `PGHD/pressure/rangeOver` | `#FF003E` (red) |`##FF2E22` (red) |혈압 기준 초과|
| 이완기 초과 | `PGHD/pressure/rangeOverT50` | `#FF003E` @ 50% |`##FF2E22` @ 50% |혈압 기준 초과|

---

## Tab 색상

> **이 섹션은 iOS 버전에 따라 렌더링 방식이 달라집니다. 반드시 버전 분기를 확인하세요.**

앱 버전 3.0.0 이후부터 파스타 컬러 시스템(pastaColor)을 적용합니다.

### iOS 26 미만 — 아이콘 + 배경 커스텀

선택된 탭에 **아이콘 색상 + 배경 색상** 두 가지를 모두 적용합니다.

| 토큰 | Dark | Light | 용도 |
|------|------|-------|------|
| `tab/focusedIcon` | `#3F0000` (Base/yellow/100) | `#5D1100` (Base/yellow/950) | 선택된 탭의 아이콘 색상 |
| `tab/focusedBack` | `#FFE6B4` (Base/yellow/800) | `#FFEEBA` (Base/yellow/150) | 선택된 탭의 배경 색상 |

선택된 탭: 아이콘은 매우 어두운 갈색(`#3F0000`)으로, 배경은 밝은 yellow(`#FFE6B4`)로 채워집니다. 비선택 탭은 gray 계열의 비활성 색상을 사용합니다.

### iOS 26 이상 — 아이콘 색상만 커스텀

iOS 26부터는 시스템이 탭바 배경을 자체 렌더링합니다. **아이콘 색상만 커스텀 가능**합니다.

| 토큰 | Dark | Light | 용도 |
|------|------|-------|------|
| `tab/glassSelect` | `#FFCA00` (core/primary) | `#DB9800` (Base/yellow/600) | 선택된 탭의 아이콘 색상 |

선택된 탭 아이콘이 Yellow(`#FFCA00`)로 표시됩니다. 배경은 시스템 기본값을 따릅니다.

> **AI 규칙:**
> - iOS 26 미만: `focusedIcon` + `focusedBack` 두 토큰 모두 적용하세요.
> - iOS 26 이상: `glassSelect` 하나만 적용하세요. `focusedBack` 배경을 임의로 추가하지 마세요.
> - 두 경우 모두 `core/primary`를 직접 참조하지 말고 `tab/*` 토큰을 사용하세요.
> - `focusedIcon`(`#3F0000`)과 `glassSelect`(`#FFCA00`)는 완전히 다른 색입니다. 버전 분기 없이 혼용하지 마세요.

---

## ValueScore 색상

수치 점수(건강 점수, 수면 점수 등)의 등급 표현에 사용됩니다. 필요에 따라 척도에 관련된 컬러를 사용합니다.
예: 5점 척도인 경우 1~5점 색상을 모두 사용, 3점 척도인 경우 1, 3, 5점 색상만 사용합니다.

## valueScore 토큰 정의
 
| Key Name | Dark | Light | 용도 |
|----------|------|-------|------|
| excellent | #00B6FF (Base/blue/500) | #008AFF (Base/blue/500) | 5점 척도 중 5점 |
| excellentBg | #00B6FF @ 16% | #008AFF @ 16% | 5점 척도 중 5점 |
| good | #4CDC42 (Base/green/500) | #1FA644 (Base/green/600) | 5점 척도 중 4점 |
| goodBg | #4CDC42 @ 16% | #1FA644 @ 16% | 5점 척도 중 4점 |
| average | #FFC04F (Base/yellow/500) | #DB9800 (Base/yellow/600) | 5점 척도 중 3점 |
| averageBg | #FFC04F @ 16% | #FFC200 @ 16% | 5점 척도 중 3점 |
| poor | #FF7444 (Base/orange/500) | #FF7600 (Base/orange/500) | 5점 척도 중 2점 |
| poorBg | #FF7444 @ 16% | #FF7600 @ 16% | 5점 척도 중 2점 |
| bad | #FF515D (Base/red/500) | #FF2E22 (Base/red/500) | 5점 척도 중 1점 |
| badBg | #FF515D @ 16% | #FF2E22 @ 16% | 5점 척도 중 1점 |
| none | #A6A1A1 (onSurface/tertiary) | #8A8585 (onSurface/tertiary) | 가치 판단 하지 않음 |
| noneBg | #A6A1A1 @ 16% | #8A8585 @ 16% | 가치 판단 하지 않음 |
 
---
 
## 점수 → 토큰 매핑
 
| 점수 | 텍스트 토큰 | 배경 토큰 | 레이블 |
|------|------------|----------|--------|
| 5점 | excellent | excellentBg | 좋음 |
| 4점 | good | goodBg | 양호 |
| 3점 | average | averageBg | 보통 |
| 2점 | poor | poorBg | 미흡 |
| 1점 | bad | badBg | 나쁨 |
| 없음 | none | noneBg | 표준 / 판단없음 |
 
---
 
## 척도별 사용 규칙
 
| 척도 | 사용 토큰 |
|------|----------|
| 5점 척도 | bad / poor / average / good / excellent 전체 사용 |
| 3점 척도 | bad(1점) / average(3점) / excellent(5점) 만 사용 |
| 그 외 | 척도 수에 맞게 균등 분배 |


> **AI 규칙:** Bg 토큰은 배경에만 — 텍스트/아이콘에 Bg 토큰 사용 금지
> **AI 규칙:** none은 가치 판단이 없는 경우에만 — 낮은 점수를 none으로 표현하지 말 것
> **AI 규칙:** 임의 색상 사용 금지 — 항상 위 토큰 이름으로 참조
> **AI 규칙:** glucose/* 토큰과 혼용 금지— valueScore와 glucose 컬러는 별개 시스템
---

## Typography

### 철학

이 앱은 건강 수치를 빠르게 인식해야 하는 환경에서 사용됩니다. 타이포그래피는 **정보의 위계를 명확히** 하고, 작은 화면에서도 가독성을 잃지 않는 것을 목표로 합니다.

weight는 Bold(B) · Medium(M) · Regular(R) 3종만 사용합니다. 제목류는 Bold, 본문 강조는 Medium, 일반 텍스트는 Regular가 기본입니다.

### 타입 스케일

| 토큰 | weight | size (Default) | line-height | 용도 |
|------|--------|----------------|-------------|------|
| `largeTitle` | Bold | 34px / 2.125rem | 2.625rem | 화면 최상단 타이틀, 수치 대형 표시 |
| `title1` | Bold | 28px / 1.75rem | 2.25rem | 섹션 대표 제목 |
| `title2` | Bold | 22px / 1.375rem | 2.0625rem | 카드 제목, 주요 헤딩 |
| `title3` | Bold / Regular | 20px / 1.25rem | 1.625rem | 서브 헤딩, 리스트 제목 |
| `body` | Bold / Medium / Regular | 17px / 1rem | 1.5rem | 일반 본문, 입력값 |
| `subHead` | Bold / Medium / Regular | 15px / 0.875rem | 1.25rem | 보조 설명, 레이블 |
| `footnote` | Bold / Regular | 13px / 0.8125rem | 1.125rem | 단위, 부가 정보 |
| `caption` | Bold / Regular | 11px / 0.6875rem | 0.875rem | 타임스탬프, 범례 |
| `graphIndex` | Regular | 8px / 0.5rem | 0.7rem | 차트 축 레이블 전용 |

### 플랫폼별 폰트 크기 스케일

타이포그래피 토큰은 플랫폼별로 자동으로 스케일됩니다. `graphIndex`(8px)는 **모든 플랫폼에서 고정**입니다 — 차트 레이아웃 안정성을 위한 의도적 예외입니다.

| 토큰 | Default | Limit (1.2x) | iOS (1.6x) | Android (1.8x) |
|------|---------|--------------|------------|----------------|
| `largeTitle` | 34 | 41 | 54 | 61 |
| `title1` | 28 | 33 | 44 | 50 |
| `title2` | 22 | 26 | 35 | 40 |
| `title3` | 20 | 24 | 32 | 36 |
| `body` | 17 | 20 | 27 | 31 |
| `subHead` | 15 | 18 | 24 | 27 |
| `footnote` | 13 | 15 | 21 | 23 |
| `caption` | 11 | 13 | 18 | 20 |
| `graphIndex` | 8 | **8 (고정)** | **8 (고정)** | **8 (고정)** |

> **AI 규칙:**
> - 폰트 크기는 반드시 위 토큰을 사용하세요. 임의의 px/rem 값을 하드코딩하지 마세요.
> - `graphIndex`는 차트 축에만 사용하세요. 일반 UI 텍스트에 사용하지 마세요.
> - 플랫폼을 명시하지 않으면 `Default` 스케일을 기준으로 하세요.
> - `title3`는 Bold(B)와 Regular(R) 두 weight가 존재합니다. 계층 강조가 필요할 때는 Bold, 일반 나열에는 Regular를 사용하세요.

---

## Spacing

### 철학

간격 시스템은 **static(고정)** 단일 체계로 구성됩니다. 타이포그래피와 달리 spacing은 플랫폼(iOS/Android/Limit)에 따라 스케일되지 않고 **모든 환경에서 동일한 값**을 사용합니다. 이는 레이아웃 그리드의 안정성을 유지하기 위한 의도적 설계입니다.

`Padding-fixed`(16px)는 화면 좌우 기본 여백으로, 전체 앱에서 일관되게 적용됩니다.

### 스페이싱 스케일

| 토큰 | 값 (전 플랫폼 동일) | 주요 용도 |
|------|---------------------|-----------|
| `static-0` | 0px | 간격 없음, 밀착 배치 |
| `static-2` | 2px | 아이콘-텍스트 최소 간격, 미세 조정 |
| `static-4` | 4px | 인라인 요소 간격, 뱃지 내부 패딩 |
| `static-8` | 8px | 컴포넌트 내부 요소 간격 |
| `static-12` | 12px | 버튼 내부 패딩, 입력 필드 간격 |
| `static-16` | 16px | 카드 내부 패딩, 섹션 내 항목 간격 |
| `static-24` | 24px | 카드 간 간격, 섹션 내 그룹 간격 |
| `static-32` | 32px | 섹션 간 간격, 대형 컴포넌트 여백 |
| `static-36` | 36px | 섹션 간 여유 있는 간격 |
| `static-40` | 40px | 화면 상단/하단 여백, 대형 섹션 구분 |
| `Padding-fixed` | 16px | 화면 좌우 기본 여백 (전 플랫폼 고정) |

### 간격 논리

스케일은 **2 → 4 → 8 → 12 → 16 → 24 → 32 → 36 → 40** 순서로 구성됩니다. 8px을 기준 단위로, 작은 값(2, 4)은 미세 조정용, 큰 값(24 이상)은 섹션/레이아웃 구조용으로 사용합니다.

> **AI 규칙:**
> - 간격 값은 반드시 위 토큰에서 선택하세요. 토큰에 없는 값(예: 6px, 10px, 20px)은 사용하지 마세요.
> - `Padding-fixed`(16px)는 화면 가장자리 여백에만 사용하세요. 컴포넌트 내부 패딩과 혼용하지 마세요.
> - spacing은 플랫폼별 조건 분기 없이 동일하게 적용합니다.

---

## Icon Size

### 철학

아이콘 크기는 spacing과 동일하게 **플랫폼 무관 고정값**입니다. typography처럼 iOS/Android 배율을 따르지 않습니다. 이는 아이콘이 터치 영역(touch target) 및 레이아웃 그리드와 직접 연결되기 때문입니다 — 배율이 적용되면 레이아웃이 깨질 수 있습니다.

### 아이콘 크기 스케일

| 토큰 | 값 | 주요 용도 |
|------|-----|-----------|
| `iconSize/16` | 16px | 인라인 아이콘, 텍스트 옆 소형 아이콘 |
| `iconSize/20` | 20px | 보조 아이콘, 리스트 아이템 아이콘 |
| `iconSize/24` | 24px | 기본 아이콘 (탭바, 네비게이션) |
| `iconSize/32` | 32px | 강조 아이콘, 카드 내 중형 아이콘 |
| `iconSize/40` | 40px | 대형 아이콘, 빈 상태(empty state) |
| `iconSize/48` | 48px | 최대 아이콘, 온보딩·스플래시 등 |

> **AI 규칙:**
> - 아이콘 크기는 반드시 위 6단계 중 하나를 사용하세요. 임의의 크기(예: 18px, 28px) 사용 금지.
> - 아이콘은 플랫폼별 배율 분기 없이 동일하게 적용합니다.
> - 탭바·네비게이션 기본 아이콘은 `24px`을 사용하세요.

---

## AI 사용 시 핵심 규칙 요약

### Color
1. **semantic 토큰만 사용** — `base/*` 직접 참조 금지
2. **Primary yellow는 CTA/탭에만** — 배경, 텍스트, 아이콘에 임의 사용 금지
3. **onPrimary는 `#3F0000`** — Primary 버튼 위 텍스트는 흰색이 아님
4. **혈당 정상 = blue** — green으로 가정하지 말 것
5. **glucose vs error 구분** — 혈당 위험 표시에 `error` 토큰 사용 금지
6. **수면은 blue 명도 그라데이션** — 단계별 다른 색 계열 추가 금지
7. **모드 미명시 시 Dark 기준** — 항상 Dark 모드 토큰을 우선 참조
8. **텍스트 색 계층은 4단계** — `primary / secondary / tertiary / fourth` 외 임의 gray 사용 금지

### Typography
9. **폰트 크기는 토큰으로** — 임의의 px/rem 하드코딩 금지
10. **graphIndex(8px)는 차트 축 전용** — 일반 UI에 사용 금지, 플랫폼 무관 고정값
11. **플랫폼 미명시 시 Default 스케일** — iOS/Android 배율 자동 적용 가정 금지

### Spacing
12. **토큰 외 간격 값 금지** — 6px, 10px, 20px 등 미정의 값 사용 금지
13. **spacing은 플랫폼 무관 고정** — 플랫폼별 조건 분기 불필요
14. **Padding-fixed는 화면 가장자리 전용** — 컴포넌트 내부 패딩과 구분

### Icon Size
15. **6단계 외 크기 금지** — 18px, 28px 등 미정의 값 사용 금지
16. **아이콘도 플랫폼 무관 고정** — spacing과 동일, 배율 분기 불필요
17. **탭바/네비 기본은 24px** — 임의로 20px이나 32px 사용 금지
