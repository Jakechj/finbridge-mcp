# finbridge-mcp — 개요 (60줄 이내)

**한 줄:** 공식 MCP 레지스트리(`kr.gronox/finbridge`) 게시용 저장소 — MCP 서버 본체가 아니라 리스팅 메타데이터·게시 도구. 상태: ops. 담당: 등재 관리 세션.

## 현황 (3줄)
- 공식 레지스트리 0.1.4 active(2026-09-09, HTTP 도메인 인증), Glama가 자동 수집 중
- 다음 액션: Registry 0.1.4의 하위 디렉토리 수집 반영 여부를 기존 점검 일정에서 확인
- 사용자 결정 대기 없음

## 구조
- 코드/문서 위치: `work/finbridge-mcp/` — **자체 git 저장소**(볼트 git 추적 대상 아님), 공개 저장소이므로 내부 운영 문서(PLAN/WORKLOG)는 이 폴더 `.gitignore`로 공개 제외
- `server.json` — 공식 레지스트리 리스팅 정의(이름·endpoint·website·repository·icon)
- `mcp-publisher.exe` — 레지스트리 게시 CLI(현재 1.8.1로 검증)
- `home_server.py` — 도메인 인증용 사본
- `README.md` — 공개 리스팅 설명(제품 소개·연결 방법), MIT 라이선스로 공개
- `mcp-registry-key.hex` / `mcp-registry-pub.hex` — 게시 서명 키 쌍
- MCP 서버 본체는 별도 프로젝트 stock-mcp, 디렉토리 등재 전체 현황은 [[finbridge-launch/PLAN]] 참조(둘 다 이 볼트의 다른 폴더)

## 운영 (세션이 서버를 뒤지지 않게)
| 항목 | 값 |
|---|---|
| 호스트 | 없음(이 저장소 자체는 정적 메타데이터, 실 서버는 stock-mcp 소유) |
| 서비스 | 공식 MCP 레지스트리 `kr.gronox/finbridge`, 실제 엔드포인트는 `https://mcp.gronox.kr/mcp` |
| env·비밀 위치 | `mcp-registry-key.hex`(게시 서명 개인키, 이 폴더 밖 복사·공유 금지) |
| 배포 | `mcp-publisher.exe`로 `server.json` 검증 후 게시(HTTP 도메인 인증 방식) |
| 로그 | 공식 레지스트리 공개 API로 active/latest 상태 확인(별도 로그 명령 미확인) |

## 함정 (겪어서 안 것만)
- ⚠ apex 도메인 well-known 인증은 **GET만 200을 반환하고 HEAD는 302** — HEAD로 확인하면 실패로 오판한다
- ⚠ `mcp-registry-key.hex`는 게시 서명 개인키이므로 이 폴더 밖으로 절대 복사·공유하지 않는다
- ⚠ 이 폴더는 자체 git 저장소라 볼트 커밋에 잡히지 않는다 — 변경 후 이 저장소 안에서 별도 커밋 필요
- ⚠ 도구 수 등 변동 가능한 수치는 `server.json`/GitHub About에 하드코딩하지 않고 현재 문서 링크로 연결(과거 수치가 실제 도구 목록과 어긋난 전례로 제거함)
- ⚠ `README.md`는 공개 리스팅용이라 stock-mcp의 최신 피벗(2026-09-20 한국 공시 전용, 도구 26종)을 아직 반영하지 않았을 수 있다 — 도구 범위 문구를 고칠 땐 stock-mcp/finbridge-launch 현황과 대조할 것

## 관련 문서
[[finbridge-mcp/PLAN]] · [[finbridge-mcp/WORKLOG]] · [[finbridge-mcp/FACTS]] · [[finbridge-mcp/README]] · [[stock-mcp/PLAN]] · [[finbridge-launch/PLAN]]
