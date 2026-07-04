# 나니 분기 스튜디오 (Nani Branch Studio)

비주얼노벨 분기를 블록(노드)으로 설계하고, **Naninovel 1.18.1 문법의 `.nani` 코드로 자동 변환**해 주는 정적 웹 도구.
수업용 — 서버 없음, 설치 없음, `index.html` 파일 하나가 전부입니다.

## 사용법

1. `index.html`을 브라우저로 열기 (더블클릭)
2. **① API 키** — [aistudio.google.com/apikey](https://aistudio.google.com/apikey)에서 무료 발급한 Gemini 키 입력 (카드 등록 불필요, 키는 내 브라우저에만 저장)
3. **② AI 뼈대 생성(선택)** — 시나리오 줄글을 쓰면 AI가 장면/선택지 구조로 변환
4. **③ 장면 편집** — 블록(= `# 라벨`) 단위로 대사·선택지·연결 편집
5. **④ 분기도 & 코드** — 실시간 분기도 확인, `.nani` 다운로드 → 유니티에 넣기
6. **⑤ 이미지 생성** — 키 없이 되는 무료 API(Pollinations)로 배경/캐릭터 시안 생성

## 블록 → 코드 변환 규칙 (Naninovel 1.18.1)

| 블록에서 | 생성되는 코드 |
|---|---|
| 블록 하나 | `# 라벨` |
| 선택지 있음 | `@choice "문구" set:... goto:.라벨` × N + **`@stop` 자동 추가** |
| 선택지 없음 + 다음 장면 지정 | `@goto .라벨` |
| 선택지 없음 + 다음 없음 (엔딩) | `@stop` 자동 추가 |
| 조건 판정 블록 | `@if` / `@elseif` / `@else` + `@goto` + **`@endif` 자동 닫기** |
| 선택지의 set | 사용된 변수 전부 스크립트 맨 위에 `@set 변수=0` 자동 초기화 |

`@shake` 같은 1.18.1에 없는 명령어는 생성하지 않습니다 (흔들기 = `@spawn ShakeCamera`).

## 배포

GitHub Pages: 저장소 Settings → Pages → Branch `main` / root 선택 → 생성된 주소를 학생들에게 공유.
