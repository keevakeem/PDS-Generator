---
name: record-input-screen
description: "Generate a health record input screen layout. Use this skill whenever the user asks to create a data entry screen, measurement input screen, or health recording screen — such as '혈압 입력 화면', '혈당 기록 화면', '체중 측정 화면', or any screen where the user enters health data with a title, input fields, and a CTA button. The user will provide: a title, the number of input fields, and label/placeholder info for each field."
---

# Record Input Screen (건강 기록 입력 화면)

이 스킬은 건강 데이터 입력 화면을 생성합니다.
사용자가 제공하는 정보: **타이틀**, **인풋박스 목록(라벨 + 플레이스홀더)**, **선택 옵션**만으로 화면을 구성합니다.

> 색상·스페이싱·타이포그래피 토큰은 design.md를 참조하세요.
> 인풋박스 상세 규칙은 SKILL_inputfueld.md 를 참조하세요.
> 버튼 규칙은 SKILL_button.md 를 참조하세요.

---

## 화면 구조 (고정)

```
[ Status Bar ]                     ← 시스템 영역, 항상 포함
[ X 닫기 버튼 ]                     ← 좌상단 고정
[ 타이틀 ]                          ← 사용자 지정
─────────────────────────────────
[ 인풋박스 1 ]                      ← 사용자 지정 (1개 이상)
[ 인풋박스 2 ]
[ 인풋박스 N ]
─────────────────────────────────
[ 텍스트 링크 ]                     ← 선택적 (우측 정렬, 화살표 포함)
[ 사진 추가 영역 ]                  ← 선택적
[ 텍스트에어리어 + 글자수 카운터 ]    ← 선택적
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

### 인풋박스
- input-component 스킬의 Default 상태 적용
- 라벨: 인풋박스 상단 (subHead Regular)
- 플레이스홀더: onSurface/fourth
- 각 인풋박스 사이 간격: static-8 (8px)
- border-radius: 20px (input-component 스킬 참조)
- 최소 높이: 73px

### 텍스트 링크 (선택적)
- 우측 정렬
- 텍스트 + 화살표 아이콘(>) 조합
- 색상: onSurface/secondary
- 타이포그래피: footnote 또는 body Regular

### 사진 추가하기 버튼 (선택적)

비주얼:
- 배경: background/elevation1
- 테두리: **점선(dashed)**, onSurface/tertiaryLine, 1px
- border-radius: 20px
- 내부 콘텐츠: 카메라 아이콘 + "사진 추가하기" 텍스트 **세로 중앙 정렬**
- 아이콘 크기: iconSize/24 (24px)
- 아이콘 색상: onSurface/secondary (Dark: #D7D5D5)
- 텍스트 색상: onSurface/secondary (Dark: #D7D5D5)
- 텍스트 타이포그래피: body Regular
- 아이콘 ↔ 텍스트 간격: static-8 (8px)
- 버튼 높이: 최소 100px (내용에 따라 유동)
- 전체 너비: 화면 좌우 패딩 제외한 전체 폭

### 텍스트에어리어 (선택적)
- 배경: background/elevation1
- border-radius: 20px
- 플레이스홀더: onSurface/fourth
- 글자수 카운터: 우하단, onSurface/tertiary, footnote Regular
- 형식: 현재글자수/최대글자수 (예: 0/1,000자)

### CTA 버튼
- button-component 스킬의 solid + large(53px) + round(500px) 적용
- 색상: button/inactive/primary (기본값, 입력 전)
- 화면 하단 고정
- 좌우 패딩: static-16 (16px)

---

## 사용자 입력 형식

아래 정보를 입력받아 화면을 생성합니다.

```
타이틀: [화면 타이틀]
인풋박스:
  1. 라벨: [라벨명], 플레이스홀더: [안내 텍스트]
  2. 라벨: [라벨명], 플레이스홀더: [안내 텍스트]
  ...
옵션:
  - 텍스트 링크: [링크 텍스트] (있으면)
  - 사진 추가: 있음/없음
  - 메모: 있음/없음, 최대 글자수: [숫자]
CTA 버튼 텍스트: [버튼명]
```

---

## 실제 예시 — 혈압 측정 화면

```
타이틀: 혈압 측정
인풋박스:
  1. 라벨: 측정 시간, 플레이스홀더: 12.31 오전 12:35 (드롭다운)
  2. 라벨: 수축기 혈압 (mmHg), 플레이스홀더: 혈압값(SYS)을 입력해주세요.
  3. 라벨: 이완기 혈압 (mmHg), 플레이스홀더: 혈압값(DIA)을 입력해주세요.
  4. 라벨: 심박수 (bpm), 플레이스홀더: 심박수(PULSE)를 입력해주세요.
옵션:
  - 텍스트 링크: 혈압 측정 방법
  - 사진 추가: 있음
  - 메모: 있음, 최대 글자수: 1,000
CTA 버튼 텍스트: 기록완료
```

---

## 스페이싱

| 위치 | 값 |
|------|-----|
| 화면 좌우 패딩 | static-16 (16px) |
| 타이틀 ↔ 첫 인풋박스 | static-24 (24px) |
| 인풋박스 간 간격 | static-8 (8px) |
| 마지막 인풋박스 ↔ 텍스트 링크 | static-16 (16px) |
| 섹션 간 간격 | static-16 (16px) |
| CTA 버튼 하단 여백 | static-16 (16px) |

---

## AI 규칙 요약

1. **타이틀, 인풋박스 목록, CTA 버튼 텍스트는 필수** — 이 3가지 없으면 생성 불가
2. **인풋박스는 input-component 스킬 규칙 그대로** — 별도 스타일 임의 적용 금지
3. **CTA 버튼은 기본적으로 inactive 상태** — 입력 완료 전까지 비활성
4. **텍스트 링크, 사진 추가, 메모는 선택적** — 사용자가 명시한 경우에만 포함
5. **배경은 background/surface (black)** — 임의 배경색 사용 금지
6. **인풋박스 순서는 사용자가 지정한 순서 유지**
