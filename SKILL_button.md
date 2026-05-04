---
name: button-component
description: Generate button components that strictly follow the healthcare app design system. Use this skill whenever the user asks to create, design, or code any button, CTA, action element, or clickable control — even if they just say "make a button" or "add a CTA". Always consult this skill before generating any button-related UI.
---

# Button Component

이 스킬은 헬스케어 앱 디자인 시스템(`design.md`)을 기반으로 버튼 컴포넌트를 생성합니다.
토큰 값을 직접 하드코딩하지 말고, 아래 규칙과 토큰 이름을 그대로 사용하세요.

> 색상·스페이싱·타이포그래피 전체 토큰은 `design.md`를 참조하세요.
> 이 파일은 버튼 컴포넌트의 **구조·변형·상태·색상·규칙**만 정의합니다.

제품 전반에서 일관된 사용자 경험을 제공하기 위해 버튼 컴포넌트의 사용 기준, 상태, 스타일 규칙을 정의합니다.

---

## 컴포넌트 구조 (Anatomy)

버튼은 4가지 속성으로 구성됩니다.

| 속성 | 설명 |
|------|------|
| Base | 아이콘(L) + 텍스트 + 아이콘(R)의 조합. 각각 선택적으로 표시 |
| Size | 버튼 높이 (small / default / large) |
| Round | 버튼 모서리 형태 (round / square) |
| Type | 버튼 스타일 (solid / line / text) |

### Base 조합 규칙

| L-icon | Text | R-icon | 구성 |
|--------|------|--------|------|
| true | true | true | L아이콘 + 텍스트 + R아이콘 |
| true | true | false | L아이콘 + 텍스트 (default) |
| false | true | true | 텍스트 + R아이콘 |
| false | true | false | 텍스트만 |
| true | false | false | 아이콘만 (20px 정사각형) |

> **규칙:** 텍스트는 한 줄 유지, 가운데 정렬. L-icon은 기본 아이콘 슬롯, R-icon은 보조 아이콘 슬롯.

---

## Size (크기)

| 이름 | 높이 | 텍스트 크기 | 용도 |
|------|------|------------|------|
| small | 32px | footnote (13px) | 밀집 UI |
| default | 44px | subHead (15px) | 일반 UI (기본값) |
| large | 53px | body (17px) | 주요 CTA |

> **규칙:** 한 화면에서 최대 2개의 사이즈만 혼용합니다.

---

## Round (모서리)

| 이름 | radius | 용도 |
|------|--------|------|
| round | 500px (pill) | 기본 Radius 타입 (default) |
| square | 8px | 서브 Radius 타입 |

---

## Type (스타일)

| 이름 | 설명 | 용도 |
|------|------|------|
| solid | 채워진 배경 버튼 (default) | 가장 중요한 액션. 화면당 1~2개 권장 |
| line | 테두리만 있는 버튼 | Solid와 함께 사용 가능. 시각적 강조 낮을 때 |
| text | 배경 없는 텍스트 버튼 | 보조 기능, 링크성 행동, 반복 리스트 |

---

## 색상 토큰 — 상태별 전체 정의

### Solid 버튼 — Active

| 종류 | 배경 토큰 | 텍스트 토큰 | Dark 배경 | Dark 텍스트 |
|------|-----------|------------|-----------|------------|
| primary | button/active/primary | button/active/onPrimary | #FFCA00 | #3F0000 |
| secondary | button/active/secondary | button/active/onSecondary | #FFE6B4 | #3F0000 |
| tertiary | button/active/tertiary | button/active/onTertiary | #565252 | #E4E2E2 |
| opacity | button/active/opacity | button/active/onOpacity | #FFCA00 @ 20% | #FFCA00 |

Light 모드: onPrimary / onSecondary = #5D1100, onTertiary = #565252

### Solid 버튼 — Press

| 종류 | 배경 토큰 | Dark 배경 |
|------|-----------|-----------|
| primary | button/press/primary | #FFB300 |
| secondary | button/press/secondary | #FFCD75 |

### Solid 버튼 — Inactive

| 종류 | 배경 토큰 | 텍스트 토큰 | Dark 배경 | Dark 텍스트 |
|------|-----------|------------|-----------|------------|
| primary | button/inactive/primary | button/inactive/onPrimary | #8A8585 | #565252 |
| opacity | button/inactive/opacity | button/inactive/onOpacity | #8A8585 @ 20% | #565252 |

Light 모드: inactive/primary = #BEBBBB, 텍스트 = #757171

### Line 버튼

| 상태 | 테두리 | 배경 | 텍스트 |
|------|--------|------|--------|
| active | onSurface/line | 없음 | onSurface/tertiary |
| press | onSurface/line | onSurface/secondaryLine | onSurface/tertiary |
| inactive | onSurface/line | 없음 | onSurface/fourth |
| opacity-active | button/active/onOpacity | button/active/opacity | button/active/onOpacity |

### Text 버튼

| 상태 | 배경 | 텍스트 |
|------|------|--------|
| active | 없음 | onSurface/tertiary |
| press | onSurface/secondaryLine | onSurface/tertiary |
| inactive | 없음 | onSurface/fourth |

---

## 공통 스펙

- 좌우 내부 패딩: Padding-fixed (16px)
- 아이콘 크기: iconSize/20 (20px)
- 텍스트 weight: Bold
- 텍스트 정렬: 가운데

---

## AI 규칙 요약

1. **테마 미명시 시 Dark 기준** — 항상 Dark 모드 토큰 우선 적용
2. **Primary 버튼 텍스트는 onPrimary(#3F0000)** — 흰색 절대 사용 금지
3. **한 화면에 Solid 버튼은 1~2개** — 남용 금지
4. **사이즈는 최대 2가지 혼용** — 3가지 이상 혼용 금지
5. **Type 기본값 solid, Round 기본값 round, Size 기본값 default(44px)**
6. **inactive는 색상 토큰으로 처리** — opacity 처리 금지 (인풋 disabled와 다름)
7. **텍스트는 한 줄, 가운데 정렬** — 줄바꿈 없음
8. **아이콘 크기는 iconSize/20** — 임의 크기 사용 금지
9. **텍스트 크기는 size에 따라** — small=13px, default=15px, large=17px
10. **figma에서 생성 시 🎃button 컴포넌트 하위의 텍스트 레이어에 CTA 내용 적용** 
