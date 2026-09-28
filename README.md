# My Dashboard — Next.js / Vercel 버전

기존 Google Apps Script 대시보드를 **Next.js App Router + TypeScript**로 변환한 버전입니다. Vercel에 그대로 연결해서 배포할 수 있습니다.

## 반영된 요청

- 기존 홈, 랜덤 뽑기, 노트, 숙제, 스케줄러, 학교, 메일 화면 구조 유지
- 붉은색을 자연스럽게 섞은 배경 글로우와 포인트 컬러 추가
- 라이트 모드 / 다크 모드 전환
- 사이드바에서 **북마크와 달력 메뉴 제거**
  - 홈 화면의 북마크 위젯과 달력 위젯은 기존 기능 보존을 위해 유지
- Next.js + TypeScript + React로 재작성
- Vercel 정적 배포 호환

## 실행

```bash
npm install
npm run dev
```

브라우저에서 `http://localhost:3000`을 엽니다.

프로덕션 빌드 확인:

```bash
npm run build
npm start
```

## Vercel 배포

1. 이 폴더를 GitHub 저장소에 올립니다.
2. Vercel에서 `Add New Project`로 저장소를 import 합니다.
3. Framework Preset은 `Next.js` 그대로 둡니다.
4. 별도 환경변수 없이 Deploy 할 수 있습니다.

## 저장 방식과 외부 연동 안내

Google Apps Script의 `google.script.run`, Spreadsheet, GmailApp은 Vercel에서 직접 실행되지 않으므로, 이 변환본은 개인 데이터(숙제, 노트, 시간표, 일정, 북마크)를 브라우저 `localStorage`에 저장하도록 바꾸었습니다. 따라서 별도 백엔드 없이 바로 동작하며, 브라우저·기기별로 데이터가 분리됩니다.

- 날씨: 클라이언트에서 `wttr.in`을 호출하며 실패 시 기본 표시를 유지합니다.
- 학교 급식·학사일정·공지: 기존 화면 영역과 UI를 유지한 로컬 배포용 플레이스홀더입니다. 실제 데이터를 연결하려면 Next.js Route Handler 또는 별도 API를 추가하면 됩니다.
- 메일: Gmail 연동은 별도 Google OAuth/API 설정이 필요하므로 Gmail 열기 버튼으로 대체했습니다.

멀티 디바이스 동기화가 필요하면 Supabase, Neon/Postgres, Firebase 중 하나를 연결하고 `localStorage` 저장 함수만 서버 저장 함수로 교체하면 됩니다.
