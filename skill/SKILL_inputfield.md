---
name: input-component
description: Generate input field components that strictly follow the healthcare app design system. Use this skill whenever the user asks to create, design, or code any input field, text field, search bar, or form input — even if they just say "make an input" or "add a text field". Always consult this skill before generating any input-related UI.
---

# Input Component

이 스킬은 디자인 시스템(`design.md`)을 기반으로 인풋 컴포넌트를 생성합니다.
토큰 값을 직접 하드코딩하지 말고, 아래 규칙과 토큰 이름을 그대로 사용하세요.

> 색상·스페이싱·타이포그래피 전체 토큰은 `design.md`를 참조하세요.
> 이 파일은 인풋 컴포넌트의 **구조·상태·변형·규칙**만 정의합니다.

---

## 컴포넌트 구조

```
[ Label ]  [ * ]                                    <- Required일 때만 asterisk 표시
+---------------------------------------------------+
|  [ Input Text / Placeholder ]         [ x ] [ eye ]|  <- Trailing Icons (상태별 조건부)
+---------------------------------------------------+
[ Helper Message ]                        [ 999/999 ] <- 각각 선택적
```

---

## 상태별 토큰 전체 정의

### Default

| 역할 | 토큰 |
|------|------|
| 배경 | background/elevation1 |
| 테두리 | onSurface/tertiaryLine 1px |
| 플레이스홀더 | onSurface/fourth |
| 레이블 | onSurface/secondary |
| Required asterisk(*) | core/error |
| Trailing 아이콘 | 없음 |

### Focused

| 역할 | 토큰 |
|------|------|
| 배경 | background/elevation1 |
| 테두리 | onSurface/primary 1px |
| 입력값 텍스트 | onSurface/primary |
| 레이블 | onSurface/secondary |
| Required asterisk(*) | core/error |
| 커서(caret) | core/primary |
| Trailing 아이콘 | onSurface/tertiary (clear + eye, iconSize/20) |

### Focused-error

| 역할 | 토큰 |
|------|------|
| 배경 | background/elevation1 |
| 테두리 | core/error 1px |
| 입력값 텍스트 | onSurface/primary |
| 레이블 | onSurface/secondary |
| Required asterisk(*) | core/error |
| 커서(caret) | core/primary |
| Trailing 아이콘 | onSurface/tertiary (clear + eye, iconSize/20) |
| 에러 메시지 | core/error |

### Success

| 역할 | 토큰 |
|------|------|
| 배경 | background/elevation1 |
| 테두리 | onSurface/tertiaryLine 1px |
| 입력값 텍스트 | onSurface/primary |
| 레이블 | onSurface/secondary |
| Required asterisk(*) | core/error |
| Trailing 아이콘 | 없음 |

### Disabled

| 역할 | 토큰 |
|------|------|
| 컴포넌트 전체 | opacity 30% (개별 색상 토큰 변경 없음) |
| Trailing 아이콘 | 없음 |

### Readonly

| 역할 | 토큰 |
|------|------|
| 배경 | background/elevation1 |
| 테두리 | onSurface/tertiaryLine 1px |
| 입력값 텍스트 | onSurface/primary |
| 레이블 | onSurface/secondary |
| Required asterisk(*) | core/error |
| Trailing 아이콘 | 없음 |

> **규칙:** Readonly는 Success와 토큰 구성이 동일합니다. 차이는 상호작용 불가 여부뿐입니다.

---

## 변형 (Variants)

각 상태는 아래 옵션의 조합으로 변형됩니다.

| 옵션 | 설명 |
|------|------|
| `required` | 레이블 옆에 core/error 색상 asterisk(*) 표시 |
| `counter` | 인풋 하단 오른쪽에 현재/최대 글자 수 표시 (onSurface/tertiary, footnote Regular) |
| `message` | 인풋 하단 왼쪽에 Helper(onSurface/tertiary) 또는 Error(core/error) 메시지 표시 |
| `single-icon` | focused / focused-error에서 Trailing Icon을 clear(x) 1개로 제한 |

---

## 타이포그래피

| 역할 | 토큰 |
|------|------|
| 레이블 | subHead Regular (15px) |
| 입력값 / 플레이스홀더 | body Regular (17px) |
| 헬퍼 / 에러 메시지 | footnote Regular (13px) |
| 글자 수 카운터 | footnote Regular (13px) |

---

## 스페이싱

| 위치 | 토큰 |
|------|------|
| 인풋 내부 좌우 패딩 | static-16 (16px) |
| 인풋 내부 상하 패딩 | static-12 (12px) |
| 레이블 ↔ 인풋 간격 | static-8 (8px) |
| 인풋 ↔ 하단 영역 간격 | static-4 (4px) |
| 아이콘 ↔ 아이콘 간격 | static-8 (8px) |
| 아이콘 ↔ 텍스트 간격 | static-8 (8px) |

- border-radius: static-8 (8px)

---

## 하단 영역 레이아웃

Helper Message와 Counter가 동시에 존재할 때 같은 라인에 배치합니다.
- 메시지: 왼쪽 정렬
- 카운터: 오른쪽 정렬

---

## AI 규칙 요약

1. **테마 미명시 시 Dark 기준** — 항상 Dark 모드 토큰 우선 적용
2. **Focused 테두리는 onSurface/primary(흰색)** — Primary yellow(#FFCA00) 절대 사용 금지
3. **커서(caret)만 core/primary(yellow)** — 테두리·레이블·아이콘에 yellow 사용 금지
4. **Focused-error 테두리는 core/error, 값 텍스트는 onSurface/primary 유지**
5. **에러 메시지는 core/error** — glucose/* 토큰과 혼용 금지
6. **`filled` 상태 없음** — 값 입력 후 포커스 해제 = success 상태
7. **Readonly는 Success와 토큰 동일** — 상호작용만 불가할 뿐 시각적으로 동일
8. **Disabled는 opacity 30%만** — 개별 색상 토큰 변경 금지
9. **Trailing 아이콘은 focused / focused-error에만** — 다른 상태에 아이콘 추가 금지
10. **스페이싱은 토큰 외 값 금지** — 6px, 10px, 14px 등 미정의 값 사용 불가
11. **아이콘 크기는 iconSize/20** — 임의 크기 사용 금지

---

## 크기

| 속성 | 값 |
|------|-----|
| 최소 높이 | 73px |
| border-radius | 20px |

> **규칙:** border-radius는 static-8(8px)이 아닌 20px 고정값입니다. spacing 토큰에 없는 예외값이므로 하드코딩합니다.
