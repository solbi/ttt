# Repository Guidelines

이 저장소는 아직 초기 스캐폴딩 단계이며 루트에는 `abcd.txt`, `bbbb.txt`, `cccc.txt`, `note.txt` 같은 플레이스홀더가 있습니다. 향후 구조 작업도 아래 기준을 따라 일관성과 리뷰 효율을 유지해 주세요.

## Project Structure & Module Organization
- 정식 문서는 `docs/`에 정리하고(예: `docs/overview.md`), 임시 메모는 안정화되면 `notes/`로 이동합니다.
- 실행 코드는 기능별로 `src/` 아래에 배치하고(`src/game/board.ts`, `src/game/state.ts`), 공용 헬퍼는 `src/shared/`에서 노출합니다.
- 테스트는 동일한 경로 구조로 `tests/`에 미러링합니다(`tests/game/board.test.ts`); 이미지·픽스처 같은 정적 자산은 `assets/`에 둡니다.

## Build, Test, and Development Commands
- 의존성이 변경되면 `npm install`로 `package-lock.json`과 환경을 동기화합니다.
- `npm run lint`는 ESLint와 Prettier를 실행합니다. 두 스크립트와 설정 파일(`.eslintrc.cjs`, `.prettierrc`)을 `package.json`에 연결해 둡니다.
- 모든 푸시 전에 `npm test`(Vitest)를 실행하고, 로컬 반복 작업에는 `npm run test:watch`를 활용합니다.
- 문서 변경이 많다면 `npx markdownlint "**/*.md"`로 마크다운 규칙 위반을 미리 잡습니다.

## Coding Style & Naming Conventions
- 기본 언어는 ES 모듈 기반 TypeScript이며, 들여쓰기는 2칸과 Prettier 기본값을 사용합니다.
- 디렉터리·모듈은 `kebab-case`, React 컴포넌트는 `PascalCase`, 테스트 파일은 대상과 함께 `.test.ts` 접미사를 사용합니다.
- 함수는 가능하면 순수하게 유지하고, 의도가 바로 드러나지 않는 복잡한 블록 위에는 짧은 설명 주석을 추가합니다.

## Testing Guidelines
- 새로운 로직 경로마다 `tests/` 아래에 대응 테스트(`*.test.ts`)를 추가하며, 기능별로 함께 위치시킵니다.
- Vitest 커버리지 리포터로 분기 커버리지 85% 이상을 유지하고, 디렉터리가 늘어나면 `vitest.config.ts`의 include/exclude를 갱신합니다.
- 테스트 스위트는 의미 있는 설명(`describe('game/board', ...)`)을 사용하고, 외부 의존성은 목 처리하며 네트워크 의존 테스트는 피합니다.

## Commit & Pull Request Guidelines
- 히스토리에서 보이는 짧고 명령형 톤을 따르세요(`abcd`, `bbbb` ⇒ `add board reducer`처럼). 커밋 제목은 72자 이내, 본문은 100자 단위로 줄바꿈합니다.
- 작업은 리뷰 가능한 단위로 스쿼시하고, 이슈 번호는 제목이 아닌 본문에 `Refs #123` 형태로 남깁니다.
- PR에는 간결한 요약, 수행한 테스트 명령, 연관 이슈, 사용자 인터페이스 변화가 있다면 스크린샷 또는 GIF를 포함합니다.

## Security & Configuration Tips
- 비밀 정보는 커밋하지 말고 `.env.example`에 필요한 변수를 문서화한 뒤 런타임 설정 헬퍼로 로드합니다.
- 셸 스크립트는 macOS와 Linux에서 모두 동작하도록 작성하고, 셋업 과정에 `chmod +x scripts/*.sh`를 포함하며 이식성 높은 POSIX 셸을 우선 사용합니다.
