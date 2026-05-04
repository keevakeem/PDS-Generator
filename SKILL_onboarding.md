---
name: onboarding-input-screen
description: Generate an onboarding or profile setup screen where users enter personal information through accordion-style input fields. Use this skill whenever the user asks to create a profile setup screen, onboarding input screen, or basic info collection screen — such as "기본 정보 설정 화면", "프로필 입력 화면", "온보딩 화면". Each field expands to show a picker or selector when tapped.
---

# Onboarding Input Screen (기본 정보 설정 화면)

이 스킬은 사용자의 기본 정보를 수집하는 온보딩/프로필 설정 화면을 생성합니다.
각 인풋은 **아코디언 방식**으로 동작합니다 — 탭하면 펼쳐지고, 다시 탭하면 접힙니다.

> 색상·스페이싱·타이포그래피 토큰은 `design.md`를 참조하세요.
> 인풋박스 상세 규칙은 `SKILL_inputfueld.md` 를 참조하세요.
> 버튼 규칙은 `SKILL_button.md` 를 참조하세요.

---



## 화면 구조 (고정)

```
[ Status Bar ]                     ← 시스템 영역, 항상 포함
[ X 닫기 버튼 ]                     ← 좌상단 고정
[ 타이틀 ]                          ← 사용자 지정
─────────────────────────────────
[ 인풋 아이템 1 ] ← collapsed / expanded
[ 인풋 아이템 2 ] ← collapsed / expanded
[ 인풋 아이템 N ]
─────────────────────────────────
[ CTA 버튼 ]                        ← 하단 고정, 사용자 지정 텍스트
```

---
## 각 영역 스펙

### X 닫기 버튼
- 좌상단 배치
- 아이콘: ic_24_close
- 색상: onSurface/primary

### 타이틀
- 타이포그래피: H2 또는 Large Title Bold
- 색상: onSurface/primary
- 위치: X 버튼 아래, 좌측 정렬

### CTA 버튼
- button-component 스킬의 solid + large(53px) + round(500px) 적용
- 색상: button/inactive/primary (기본값, 입력 전)
- 화면 하단 고정
- 좌우 패딩: static-16 (16px)


## 공통 인풋 아이템 구조

### Collapsed 상태 (접힌 상태)
```
┌──────────────────────────────────────┐
│  라벨                          ∨     │
│  현재 선택값                         │
└──────────────────────────────────────┘
```
- 배경: background/elevation1
- border-radius: 16px
- 라벨: onSurface/tertiary, footnote Regular
- 선택값: onSurface/primary, body Regular (or subHead)
- 화살표: ∨ (onSurface/tertiary, 우측)

### Expanded 상태 (펼쳐진 상태)
```
┌──────────────────────────────────────┐
│  라벨                          ∧     │
│  현재 선택값                         │
│  ─────────────────────────────────   │
│  [ picker 영역 ]                     │
└──────────────────────────────────────┘
```
- 배경: 동일
- 화살표: ∧ (방향 전환)
- picker 영역이 카드 내부에 인라인으로 펼쳐짐

---

## 인풋 타입 3가지

### Type 1: Date Picker (날짜/시간 스크롤 휠)

사용 예: 생년월일, 측정 시간

```
      1982년    8월    14일
   → 1983년    7월    15일  ← 선택된 행
      1984년    9월    16일
```

- 컬럼 수: 데이터에 따라 2~3개 (년/월/일, 시/분 등)
- 선택된 행: core/primary (#FFCA00) Bold + 배경 강조 바 (onSurface/tertiaryLine, 둥근 모서리)
- 비선택 행: onSurface/tertiary Regular
- 스크롤 방식: 무한 스크롤 휠
- 각 컬럼 가운데 정렬
- 컬럼 사이 구분선 없음

### Type 2: Radio Selector (라디오 버튼 선택)

사용 예: 성별

```
  ● 남자     ○ 여자
```

- 라디오 선택 전 placeholder: onSurface/fourth
- 선택된 옵션: core/primary 라디오 버튼 + onSurface/primary 텍스트
- 미선택 옵션: onSurface/tertiaryLine 라디오 버튼 + onSurface/secondary 텍스트
- 옵션 간격: static-24 (24px)
- 라디오 크기: 20px

### Type 3: Number Picker (숫자 스크롤 휠)

사용 예: 키(cm), 체중(kg)

```
컬럼1 (정수)   컬럼2 (소수)
    174           .9
  → 175           .0  ← 선택된 행
    176           .1
```

- 컬럼 수: 2개 (정수부 / 소수부) 또는 1개 (정수만)
- 선택된 행: core/primary (#FFCA00) Bold + 배경 강조 바 (onSurface/tertiaryLine, 둥근 모서리)
- 비선택 행: onSurface/tertiary Regular
<!-- - 단위 표시: 컬럼 헤더 또는 선택값 옆에 표기 -->

---

## 선택값 표시 형식 (Collapsed 상태)

| 타입 | 표시 예시 |
|------|----------|
| Date Picker | 82.07.15 / 12.31 오전 12:35 |
| Radio Selector | 남자 / 여자 / 선택해주세요. |
| Number Picker | 175.0cm / 75.0kg |

미선택 상태: "선택해주세요." — onSurface/fourth

---

## 타이틀 영역

- 타이틀: H1 Bold, onSurface/primary, 최대 2줄
- 서브타이틀: body Regular, onSurface/secondary
- 타이틀 ↔ 서브타이틀 간격: static-8 (8px)
- 서브타이틀 ↔ 첫 인풋 간격: static-24 (24px)

---

## 스페이싱

| 위치 | 값 |
|------|-----|
| 화면 좌우 패딩 | static-16 (16px) |
| 인풋 아이템 간 간격 | static-8 (8px) |
| 인풋 내부 상하 패딩 | static-16 (16px) |
| 인풋 내부 좌우 패딩 | static-16 (16px) |
| CTA 버튼 하단 여백 | static-16 (16px) |

---

## 사용자 입력 형식 (최소 입력)

아래 정보를 입력받아 화면을 생성합니다.

```
타이틀: [화면 타이틀]
서브타이틀: [화면 서브 타이틀]
인풋: 인풋 목록 (라벨 + 타입 + 옵션)
CTA 버튼 텍스트: [버튼명]
```

타입(`date` / `radio` / `number`)은 Claude가 자동 추론하므로 명시하지 않아도 됩니다.
옵션도 라벨명으로 유추 가능한 경우 생략 가능합니다 (예: "생년월일" → 년/월/일 자동 적용).

**생성 방식:** HTML 또는 React로 실제 렌더링되는 화면을 만듭니다. 아코디언 동작(클릭 시 expand/collapse)과 picker UI를 포함합니다.

**타입 자동 추론:** 사용자가 타입을 명시하지 않아도 라벨명으로 추론합니다.
- 생년월일, 날짜, 시간 → `date`
- 남자/여자, 성별, A/B 선택 → `radio`
- 키, 체중, 숫자 단위(cm/kg/bpm 등) → `number`

---

## 실제 예시 — 기본 정보 설정 화면

```
타이틀: 기본 정보를\n설정해 주세요
서브타이틀: 보다 나은 건강 분석을 위해 입력해 주세요.
인풋 목록:
  1. 라벨: 생년월일, 타입: date, 옵션: 년/월/일
  2. 라벨: 성별, 타입: radio, 옵션: 남자/여자
  3. 라벨: 키, 타입: number, 옵션: cm, 소수 1자리
  4. 라벨: 체중, 타입: number, 옵션: kg, 소수 1자리
CTA 버튼 텍스트: 다음
```

---

## AI 규칙 요약

1. **타이틀, 인풋 아이템 목록, CTA 버튼 텍스트는 필수** — 이 3가지 없으면 생성 불가
2. **인풋박스는 SKILL_inputfueld.md 스킬 규칙 그대로** — 별도 스타일 임의 적용 금지
2. **한 번에 하나만 expanded** — 다른 항목 탭 시 이전 항목은 자동으로 collapsed
3. **선택된 picker 값은 core/primary(#FFCA00)** — 임의 색상 사용 금지
4. **Number Picker 선택 행은 배경 강조 바 포함** — Date Picker는 배경 강조 없음
5. **미선택 상태 텍스트는 "선택해주세요."** — onSurface/fourth 색상
3. **CTA 버튼은 기본적으로 inactive 상태** — 입력 완료 전까지 비활성
7. **인풋 아이템 간격은 static-8** — 더 넓거나 좁게 임의 조정 금지
6. **인풋 아이템 순서는 사용자가 지정한 순서 유지**
