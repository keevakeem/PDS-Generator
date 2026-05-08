---
name: snackbar-color
description: Apply snackbar and toast color tokens when generating snackbar or toast UI components. Use this skill whenever the user asks to create, design, or code a snackbar, toast, notification bar, or any floating message UI — even if they just say "make a snackbar" or "add a toast". Always consult this skill before generating snackbar or toast UI. appVersionName 3.0.0 이상부터 적용.
---

# pastaColor / snackbar

이 스킬은 디자인 시스템(`design.md`)을 기반으로 snackbar 및 toast 컴포넌트를 생성합니다.
토큰 값을 직접 하드코딩하지 말고, 아래 규칙과 토큰 이름을 그대로 사용하세요.

> 색상·스페이싱·타이포그래피 전체 토큰은 `design.md`를 참조하세요.
> 이 파일은 인풋 컴포넌트의 **구조·상태·변형·규칙**만 정의합니다.
> 해당 컬러 토큰은 snackbar와 toast 컴포넌트에 공통으로 사용됩니다.

---

## 색상 토큰 정의

| Key Name | Dark | Light | Base 참조 | 용도 |
|----------|------|-------|-----------|------|
| surface | #EDEBEB | #3E3C3C | Base/gray/850 | 배경 (bg) |
| onSurface | #8A8585 | #BEBBB | Base/gray/400 | 텍스트, 아이콘 |
| action | #BF6F00 | #FFC200 | Base/yellow/300 (Dark) / Base/yellow/500 (Light) | Action 텍스트 버튼 |

---

## 컴포넌트 구조

snackbar와 toast는 동일한 색상 토큰을 사용하며, 아래 변형을 가집니다.

### 변형 (Variants)

| 변형 | 설명 |
|------|------|
| Single-line | 아이콘 없음, 텍스트 한 줄 |
| Single-line + icon | 왼쪽 아이콘 + 텍스트 한 줄 |
| Multi-line | 아이콘 없음, 텍스트 두 줄 |
| Multi-line + icon | 왼쪽 아이콘 + 텍스트 두 줄 |

### Action 버튼 유무

- **snackbar**: Action 텍스트 버튼 + 화살표 아이콘(>) 포함 가능
- **toast**: Action 버튼 없음

---

## 토큰 적용 규칙

| 역할 | 토큰 |
|------|------|
| 컴포넌트 배경 | surface |
| 본문 텍스트 | onSurface |
| 아이콘 | onSurface |
| Action 텍스트 + 아이콘 | action |

---

## snackbar vs toast 차이

| 속성 | snackbar | toast |
|------|----------|-------|
| Action 버튼 | 있음 (선택적) | 없음 |
| 색상 토큰 | 동일 | 동일 |

---

## AI 규칙 요약

1. **appVersionName 3.0.0 미만이면 이 토큰 사용 금지**
2. **테마 미명시 시 Dark 기준** — Dark 값 우선 적용
3. **배경은 반드시 surface 토큰** — 임의 gray 값 사용 금지
4. **Action 텍스트/아이콘은 action 토큰만** — onSurface나 primary 혼용 금지
5. **toast에는 Action 버튼 없음** — toast에 action 색상 사용 금지
6. **onSurface는 텍스트와 아이콘에만** — 배경에 사용 금지
