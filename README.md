# DIHEIR 예약 유도 랜딩페이지 (diheir_landing)

HTML5 + CSS3 + 순수 JavaScript로 만든 정적 페이지입니다. React·TypeScript·Tailwind 같은 프레임워크나 라이브러리는 쓰지 않았고, npm 설치나 빌드도 필요 없습니다.
작업 규칙은 `rule.md`에 정리되어 있습니다. 수정 작업을 시작하기 전에 꼭 먼저 읽어 주세요.

## 1. 실행 방법
- `index.html`을 브라우저에서 바로 열거나, 폴더 전체를 정적 서버에 올리면 됩니다. 예: `python3 -m http.server`
- CSS는 `<head>`의 `<style>`에, JS는 `</body>` 바로 앞의 `<script>`에 모두 들어 있습니다. 별도 CSS·JS 파일은 없습니다.
- 메이크샵에 넣을 때는 `<div class="diheir-wrap" id="diheir-landing"> … </div>` 영역과 `<style>`, `<script>`를 옮기면 됩니다. `<body style="margin:0">`은 단독 실행용이므로 메이크샵에서는 빼도 됩니다.

## 2. 폴더 구조
```
diheir_landing/
├─ index.html
├─ README.md
├─ rule.md
└─ component/
   ├─ font/
   │  ├─ DreamAvenue/          ← font.woff2, font.woff 미제공 (아래 7번 참고)
   │  └─ NotoSerifKR/NotoSerifKR-VF.ttf
   └─ img/
      ├─ 01_section_introNcustom/
      │  ├─ 25.11.17_디에르_제품_모션_1.gif
      │  └─ olive_Group_01~05_pc.svg / olive_Group_01~05_mo.svg
      ├─ 03_Section_Difference/bg.png, diff-1.png, diff-2.png, diff-3.png, diff-4.jpg
      ├─ 04_Section_Secret_Benefits/Frame_92.jpg, Frame_99.png, Frame_100.jpg, Frame_101.jpg
      ├─ 05_Section_Reservation/05_Section_Reservation.jpg, diheirspace01~03.jpg
      ├─ 06_Section_brand/img.png, olive_Group_01~05.svg
      ├─ diheir_floating/diheir_floating_1.png
      ├─ icon/menu_pc.svg, menu_mo.svg, teenyicons_left-outline.svg, teenyicons_right-outline.svg, dropdown_icon.svg
      └─ logo/Diheir_Logo_og.png, logp_Vector_01~09_pc.svg / _mo.svg
```
- 파일명은 피그마 레이어명을 따랐습니다. 경로에서 문제가 될 수 있는 공백만 `_`로 바꿨고, 이름이 같은 레이어(Group, Vector)에는 순번을 붙였습니다.
- 확장자는 실제 파일 포맷에 맞췄습니다. 피그마에서 받은 PNG 중 실제로는 JPEG나 GIF인 파일은 `.jpg`·`.gif`로 바꿨습니다.
- PC와 모바일에서 벡터 좌표나 선 두께가 다른 에셋은 `_pc`/`_mo`로 나눴습니다. 해당 에셋은 olive(01), logp, menu입니다.

## 3. 피그마 섹션과 에셋 경로 대응 (위에서 아래 순서)
| 피그마 프레임 | 에셋 |
|---|---|
| diheir_bene_az (상단 배너) | 없음 (내부 컴포넌트 미제공) |
| nav | icon/menu_pc.svg, menu_mo.svg |
| 01_section_introNcustom | 01_section_introNcustom/*, logo/logp_Vector_* |
| 02_section_collection | icon/teenyicons_* (컬렉션 카드 이미지 미제공) |
| 03_Section_Difference | 03_Section_Difference/bg.png, diff-1.png~diff-4.jpg |
| 04_Section_Secret_Benefits | 04_Section_Secret_Benefits/Frame_92·99·100·101 |
| 05_Section_Reservation | 05_Section_Reservation/* , icon/dropdown_icon.svg |
| 06_Section_brand | 06_Section_brand/* |
| 07_Section_deheirVideo | 없음 (영상 미제공) |
| diheir_floating | diheir_floating/diheir_floating_1.png |
| 08_Section_footer | logo/Diheir_Logo_og.png |

## 4. 반응형 기준
- 1024px 이상은 PC 시안(1920 프레임), 1023px 이하는 모바일 시안(768 프레임)을 따릅니다. 미디어쿼리 `max-width: 1023px`를 씁니다.
- 디자인 1px은 CSS 변수 `--u`로 정의했습니다. 값은 `min(1px, 컨테이너너비/1920)`이고, 모바일에서는 `/768`입니다. 그래서 1920px 이상에서는 시안 크기 그대로, 그보다 작은 화면에서는 비율대로 줄어듭니다. transform: scale은 쓰지 않았습니다.
- 768px 이상 휴대폰 크기로 고정하지 않았기 때문에, 360px 화면에서는 768 시안 비율대로 줄어듭니다.
- **최소 폰트 크기 12px 보장**: PC 및 모바일 전 구간에서 어떤 텍스트도 12px 미만으로 축소되지 않도록 CSS `max(12px, calc(var(--u) * N))` 방어 설계를 일괄 적용했습니다. 띠배너, 드롭다운 메뉴, 슬라이드 설명글, 혜택 카드 본문/안내문구, 예약폼 레이블/입력창/에러/개인정보 안내문, 달력 팝업, 매장 안내, 브랜드 스토리 영문/국문 본문, 푸터 정보 등 모든 텍스트가 280px 초소형 모바일(Galaxy Fold 등)부터 2560px 대형 화면까지 12px 이상의 완벽한 가독성을 유지합니다.
- 예외: PC 플로팅(`.diheir-floating__pc`)은 반응형으로 줄어들지 않고 시안 크기(180×418px)로 고정됩니다. 카드 안에서 가장 작은 글자(`.diheir-floating__bene-text--s`, 12px)가 12px보다 작아지지 않게 하기 위해서입니다. 위치는 오른쪽 끝을 기준으로 잡았습니다(시안 기준 중앙 +880). 그래서 작은 PC 화면에서도 카드가 화면 밖으로 넘치지 않습니다.
- 레이아웃은 Flex와 Grid로 잡았습니다. 큰 장식 영문 타이틀과 겹치는 요소에만 absolute를 썼습니다.
- 헤드리스 Chromium 및 자동 검증 스크립트로 280·320·360·375·390·412·480·600·768·820·1024·1280·1440·1920·2560px 전 뷰포트에서 12px 미만 위반 0건(Violations: 0), 문서 가로 스크롤 없음, 깨진 이미지 없음, JS 오류 없음을 확인했습니다.

## 5. 폰트
- 영문(제목, 버튼, 숫자 01~04·80+·3200, 영문 문구)에는 `DreamAvenue`를 쓰고 클래스는 `.diheir-en`입니다. 굵기는 400만 쓰고 `font-synthesis: none`으로 합성 볼드를 막았습니다.
- 한글에는 `Noto Serif KR` 가변 폰트(200~900)를 씁니다. 피그마 기준 굵기는 ExtraLight 200, Light 300, Regular 400, Medium 500입니다.
- 두 폰트 모두 `@font-face`에 `font-display: swap`을 적용했습니다.
- Noto Serif KR 파일은 TTF로 약 13MB입니다. 운영 환경에서는 woff2 서브셋으로 바꾸는 것을 권장합니다. 바꿀 때는 `@font-face`의 src와 format도 함께 수정해야 합니다.

## 6. 이미지·영상 교체
- 같은 경로에 같은 파일명으로 덮어쓰면 됩니다. 비율이 바뀌면 `<img>`의 width/height와 CSS `aspect-ratio`도 함께 맞춰 주세요.
- 첫 화면의 링 모션은 로컬 영상 파일(`component/img/01_section_introNcustom/25.11.17_디에르 제품_모션_1-2.mp4`)을 `<video>` 태그(자동재생, 반복, 음소거, 인라인 재생)로 연결했습니다.
- 피그마 원본 사진은 용량이 큽니다. diheirspace01은 약 15MB입니다. 운영 전에 WebP나 JPG로 압축하는 것을 권장합니다.
- 영상(07 하단)은 제공된 Vimeo 링크로 재생 중입니다.

## 7. 구현한 인터랙션
피그마 프로토타입·모션 데이터를 조회했지만 정의된 모션이 없었습니다(`get_motion_context` 결과가 비어 있음). 그래서 자동 모션, 등장 효과, 패럴랙스는 넣지 않았습니다.
- 예약 이동 및 브랜드 링크: nav의 "디에르 예약 / 상담" 버튼이 `#reservation`으로 이동합니다. 마우스 호버 시 "디에르 예약 / 상담" CTA 버튼 아래에 동일한 너비의 오렌지 하이라이트 박스(`background: #C56220`, "지금 바로 시크릿 혜택 받기")가 부드럽게 나타나며, 클릭 시 예약 영역으로 부드럽게 스크롤됩니다. PC 플로팅 하단 CTA 버튼(`.diheir-floating__cta`, diheir.com) 및 모바일 플로팅 배너(`.diheir-floating__mo`)는 공식 브랜드 사이트(`https://www.diheir.com/?utm_source=diheir_landing&utm_medium=referral&utm_campaign=brand_page`)로 새 탭에서 연결되며, 유입 추적용 UTM 파라미터가 온전히 유지됩니다.
- 컬렉션 슬라이더(02): 4개 컬렉션(`LOV Collection` [01~03], `Heirbound Collection` [04~05], `CONCORE Collection` [06~07], `SPIRAL Collection` [08~09]) 단위의 **무한 순환(Infinite Loop) 컴포넌트 페이지 슬라이더**로 동작합니다. 하단 좌우 화살표 버튼 클릭 또는 마우스/터치 좌우 스와이프 시 40px 임계치에서 마우스에 붙지 않고 한 번에 다음/이전 컬렉션 페이지로 슉 전환(0.5초 가로 슬라이드)됩니다. 첫 번째(LOV)에서 이전 이동 시 마지막(SPIRAL)으로, 마지막(SPIRAL)에서 다음 이동 시 처음(LOV)으로 매끄럽게 무한 루프 순환하며, 좌우 버튼 모두 항상 활성화 상태를 유지하고 4단계 진행 바(progress)가 위치에 맞게 연동됩니다.
  - **PC 환경**: 각 컬렉션 카드에 마우스 호버(또는 포커스) 시 `::after` 가상 요소로 `#000` 60%(`opacity: 0.6`) 반투명 오버레이가 부드럽게 깔리며, 카드 중앙에 `<p class="diheir-collection__name diheir-en">ProductName</p>` 텍스트가 흰색으로 나타납니다.
  - **모바일 환경**: 호버 인터랙션 대신 카드 하단에 영문 프로덕트네임(`bottom: 60px`, 좌우 패딩 `20px`)이 상시 고정 노출되며, `::after` 가상 요소에 상시 그라디언트(`linear-gradient(180deg, rgba(0, 0, 0, 0) 75%, rgba(0, 0, 0, 0.6) 100%), linear-gradient(0deg, rgba(0, 0, 0, 0.2) 0%, rgba(0, 0, 0, 0.2) 100%)`)를 적용해 카드 배경과 텍스트의 가독성을 우아하게 확보합니다.
- Difference(03) 슬라이더: 4개의 슬라이드(`01 명장의 세공`, `02 GIA · IGI 인증`, `03 디자인 · 커스터마이징`, `04 평생 A/S`)로 구성된 **무한 순환(Infinite Loop) 슬라이더**로 구현되었습니다. 좌우 화살표 버튼 클릭 및 마우스 드래그 / 터치 스와이프(40px 임계치)로 부드럽게 1장씩 순환 이동하며, 첫 번째/마지막 슬라이드 사이에서도 끊김 없이 무한 루프가 이어집니다.
- 혜택 카드(04): 모바일에서는 4장을 세로로 쌓습니다. PC에서는 가로 아코디언 형태로 배치되어, 마우스가 빠르게 스쳐 지나갈 때 불필요하게 통통 튀지 않도록 약 90ms의 미세 지연(Hover Intent) 후 0.65초 완만한 감속 곡선(`cubic-bezier(0.25, 1, 0.35, 1)`)으로 우아하고 부드럽게 가로 확장(width: 307px → 664px) 및 이미지 투명도/타이틀/본문 페이드인 인터랙션이 활성화(`.is-active`)됩니다.
- 플로팅 배너: `position: sticky`로 화면 오른쪽 아래에 고정됩니다. 푸터에 들어서면 푸터 위에서 멈춥니다.
- PC 플로팅 혜택 카드(`.diheir-floating__slide` 4장) 및 상단 띠배너(`.diheir-bene`): 좌우 화살표 버튼을 누르면 이전/다음 카드로 가로 이동합니다(0.5초). 마우스 드래그나 터치 스와이프로 가로 40px을 넘기면 바로 다음/이전 카드로 넘어갑니다. 슬라이드 카드나 상단 띠배너를 클릭하면 04 Secret Benefits 섹션으로 부드럽게 스크롤 이동하며, 클릭한 해당 혜택 카드(`01 상담 고객`, `02 계약 고객`, `03 당일 계약 고객`, `04 제휴사 혜택`)가 즉시 활성화(`.is-active`)되어 펼쳐집니다.
- 약관보기: `<dialog class="diheir-dialog">` 모달이 열리며, 개인정보 수집·이용(목적, 항목, 보유기간) 안내 내용이 적용되어 있습니다. ESC 키 또는 닫기 버튼 클릭 시 닫힙니다.
- **텍스트 줄바꿈 및 영역 최적화**:
  - 시크릿 혜택 안내문구(`.diheir-benefits__notice`): 모바일에서 영역 밖으로 텍스트가 삐져나가지 않도록 `white-space: normal; word-break: keep-all; overflow-wrap: break-word;` 및 좌우 여백을 주어 자연스럽게 줄바꿈 처리.
  - 푸터 영역(`.diheir-footer`): 고정 높이와 절대위치를 제거하고 내용물에 맞춰 높이가 늘어나는 **hug 레이아웃(`height: auto`)**으로 개편. 주소 등 긴 안내 텍스트(`.diheir-footer__info`)의 잘림 방지 줄바꿈 적용 및 하단 로고(Diheir Logo)가 잘리지 않고 온전히 노출되도록 패딩 및 반응형 최적화.

## 8. 예약폼 범위, UTM 광고 유입 추적 및 메이크샵 연동 가이드
- **예약 항목 순서 및 라벨 정렬**: 이름 → 연락처 → 방문일(날짜, 시간) → 관심분야 → 개인정보 동의. 가장 긴 라벨인 **"관심분야"**의 너비에 맞춰 모든 컨트롤(`class="diheir-field__ctrl"`)의 시작 위치를 일관되게 정렬하여 텍스트 겹침을 원천 방지. 모든 항목에 `<label>` 및 접근성 속성 연결.
- **유효성 검사**: 필수값 체크, 이름 2자 이상, 휴대전화 형식(`010-XXXX-XXXX`), 방문일 유효성(오늘 이전 날짜 방지, 유효한 날짜 검증), 시간·관심분야 선택 필수, 개인정보 수집·이용 동의 필수.
- **방문일(날짜) 입력 및 반응형 달력 팝업**:
  - 연도·월·일 직접 타이핑 지원: 숫자 입력 시 자동으로 `YYYY-MM-DD` 포맷팅(예: `20261020` 입력 시 `2026-10-20` 완성, 백스페이스 및 구분자 유연 처리).
  - 커스텀 달력 팝업(`diheir-calendar-pop`): 달력 아이콘 버튼 클릭 시 열림. 이전/다음 월 탐색, 오늘 날짜 빠른 선택, 날짜 클릭 시 자동 입력 및 유효성 실시간 갱신.
  - 입력창 폰트 최적화: `YYYY-MM-DD` 영문 플레이스홀더 텍스트가 잘리지 않도록 모바일 인풋 및 셀렉트박스 폰트 크기를 `max(10px, calc(var(--u) * 16))`으로 지정하여 시인성과 여백 확보.
  - 달력 팝업 모바일 반응형: 기본 모바일(421~768px)에서는 38px 터치 영역을 유지하며, 420px 이하 좁은 화면(`@media (max-width: 420px)`)에서는 날짜 셀(`.diheir-cal__day`)을 `width: 34px; height: 34px; font-size: 12px;`로 자동 반응형 전환하여 우측 토요일("토") 열이 잘리는 현상을 완벽하게 방지. 최소 12px 폰트 기준 준수.
- **광고 유입 UTM 파라미터 자동 수집 및 보존**:
  - 수집 항목: `utm_source`, `utm_medium`, `utm_campaign`, `utm_term`, `utm_content`, `utm_id` (총 6종).
  - 방문자가 광고 URL(`?utm_source=...`)을 통해 첫 진입 시 즉시 URL 파라미터를 읽어 `sessionStorage`(`diheir_utm_data`)에 보존합니다.
  - 사용자가 페이지 내부를 스크롤하거나, 다른 영역을 둘러본 뒤 예약폼으로 이동하거나, 새로고침하더라도 유입 파라미터가 유실되지 않고 폼의 `<input type="hidden">` 필드에 자동 주입됩니다.
  - 검색이나 즐겨찾기 등 직접 방문 시에는 빈 문자열(`""`)로 안전하게 처리되며 예약 절차는 정상 진행됩니다.
  - 방문자 UI 화면에는 전혀 노출되지 않는 Hidden 필드로 구현되어 있습니다.
- **실제 데이터 저장 상태 안내**:
  - 현재 랜딩페이지는 정적 HTML 파일로 메이크샵 백엔드(CGI/API/게시판) 엔드포인트(`action`)가 연결되기 전 단계입니다.
  - 따라서 브라우저 클라이언트 검증 및 접수 데이터 패키징(`FormData`)까지 완료되며, 임의로 거짓 "예약 완료" 메시지를 띄우지 않고 안내 문구("온라인 예약 저장 기능은 아직 연동 전입니다. 예약은 전화(0507-1339-2520)로 문의해 주세요.")가 노출됩니다.
  - 콘솔창(`console.log("[DIHEIR 예약 접수 데이터 전송 시도]", formDataObj)`) 및 전역 변수(`window.__diheir_last_reservation__`)에서 수집된 UTM 파라미터와 입력값이 온전히 포함되어 있음을 실시간 확인할 수 있습니다.
- **메이크샵 관리자 연동 및 확인 요청 가이드**:
  1. **방식 A (메이크샵 상담/게시판 추가항목 매핑 - 가장 권장)**:
     - 메이크샵 관리자 > `게시판/메일 > 상담/문의 관리 > 추가 입력 필드(추가항목)` 설정에서 UTM 항목용 필드(예: `etc1` ~ `etc6` 또는 `utm_source` 등)를 생성합니다.
     - `index.html` 내 `<form id="diheir-reservation-form">`의 hidden input `name` 속성을 메이크샵에서 지정한 파라미터명과 일치시키고, 메이크샵 접수 처리 URL을 `action="접수_URL"` `method="POST"`로 지정합니다.
     - 메이크샵 관리자 상담 접수 상세 내역에서 각 유입 항목이 개별 열/필드로 깔끔하게 표시됩니다.
  2. **방식 B (상담 내용/메모란에 유입경로 자동 병합)**:
     - 메이크샵 게시판에 추가 필드 생성이 제한되는 경우, `submitReservation(data)` 함수 내에서 전송 직전 상담 내용(content/memo) 필드 끝에 `\n[유입경로] naver / cpc / diheir_landing / reservation` 형태로 텍스트를 자동 추가하여 전송합니다.
     - 별도의 메이크샵 필드 설정이나 커스텀 개발 없이도 관리자가 접수 상세글 본문에서 즉시 광고 유입 출처를 확인할 수 있습니다.
  3. **방식 C (메이크샵 REST API / 스마트 웹훅 연동)**:
     - 메이크샵 OpenAPI를 사용할 경우 `submitReservation()` 내에서 `fetch('/api/reservation', { method: 'POST', body: JSON.stringify(formDataObj) })` 형태로 비동기 통신 처리합니다.
- 모든 클래스에는 `diheir-` 접두사를 붙였고, 스타일은 `.diheir-wrap` 내부에서만 적용됩니다.

## 9. 미제공 에셋과 추가 확인 사항
**미제공 에셋** (임의 이미지로 대체하지 않았습니다)
- `component/font/DreamAvenue/font.woff2`, `font.woff`: 이 Make 파일에서 Dream Avenue Regular를 가져오지 못했습니다(`not_found`). 파일을 넣기 전까지는 브라우저 기본 serif로 표시되고, 이 경로에서 404가 발생합니다. 그래서 영문 제목의 폭이 시안과 다를 수 있습니다.
- 02 컬렉션 카드 이미지: `component/img/02_section_collection/01.png` ~ `09.png` 9종 적용 완료.
  - PC 환경: 4개 컬렉션 바디 단위(LOV, Heirbound, CONCORE, SPIRAL) 무한 슬라이더 및 호버 인터랙션(오버레이 및 제품명 표시).
  - 모바일 환경: 01~09 총 9개 카드가 연속해서 흐르는 단일 무한 가로 슬라이더/스크롤 트랙. 터치 스와이프 및 드래그, 하단 좌우 컨트롤 버튼(`<`, `>`)과 9단계 프로그레스 바 연동. 카드 하단에 제품명 및 그라디언트 오버레이 상시 고정.
  - 컬렉션명 스크롤 실시간 연동: 가로 스크롤 X위치(현재 화면에 노출 중인 이미지 구간)에 맞춰 상단 컬렉션명이 실시간으로 자동 변경 (01~03: LOV Collection / 04~05: Heirbound Collection / 06~07: CONCORE Collection / 08~09: SPIRAL Collection).
- 03 Difference 이미지: `component/img/03_Section_Difference/diff-1.png` ~ `diff-4.jpg` 4종 적용 완료.
- 07 영상과 포스터 이미지.
- 상단 배너 diheir_bene_az 내부 콘텐츠(1:705 / 1:1256), PC 플로팅 내부 요소(1:696, 1:697), PC 혜택 카드 영역(1:509): 피그마에서 "missing" 컴포넌트로 비어 있습니다.

**확인이 필요한 사항**
- PC 혜택 카드: PC 시안 슬롯이 비어 있어서 모바일 카드 디자인을 그대로 가져와 가로 스크롤로 배치했습니다. "혜택 카드 전환" 방식을 확정해 주세요.
- PC 플로팅 배너 및 모바일 플로팅 배너: 클릭 시 공식 브랜드 사이트(UTM 파라미터 유지)로 새 탭 연결됩니다.
- 메뉴 버튼: 클릭 및 마우스 호버(PC 환경) 시 드롭다운 메뉴(Drop_Menu)가 열리고 닫힙니다. `.diheir-resv__box`와 동일한 글라스 효과(`backdrop-filter: blur`, 반투명 배경 및 보더)가 적용되어 있으며, 텍스트는 좌측 정렬되어 있습니다. Custom, Collection, Difference, Benefits, Reservation, Brand 각 섹션으로 부드럽게 이동하며, 외부 클릭 및 ESC 키 입력 시 자동으로 닫힙니다. 텍스트 크기는 반응형으로 조절되되 최소 12px 아래로 내려가지 않도록 설정되어 있습니다.
- 관심분야 옵션: '웨딩밴드', '리셋팅', '다이아몬드 및 유색보석', '데일리주얼리' 4개 항목 적용 완료. 방문 시간(10:30~19:00, 30분 단위)은 임시값입니다. 필드별 필수 여부도 시안에 표시가 없어 모두 필수로 두었습니다.
- 개인정보 동의 체크박스는 시안에 보이지 않지만, 동의를 받으려면 필요해서 넣었습니다.
- 푸터의 메뉴 링크와 SNS 아이콘은 PC 시안에서 프레임 밖에 있어 보이지 않는 요소라 넣지 않았습니다.
- **피그마 댓글:** 지금 쓸 수 있는 도구로는 댓글을 조회할 수 없어서 확인하지 못했습니다. 반영할 댓글이 있으면 텍스트나 캡처로 전달해 주세요.
