---
type: facts
project: finbridge-mcp
updated: 2026-09-24
---

# 사실 카드 — finbridge-mcp(공식 레지스트리 게시)

> 규약: [[decisions/2026-09-24 볼트 3층 구조와 사실 카드 규약]]. 값은 원천에서 한 번만 꺼내 적고, 원천이 진실이다. 서명 개인키는 값 대신 위치만.

| 키 | 값 | 출처 | 위치 | 확인일 | 민감 |
|---|---|---|---|---|---|
| 레지스트리 리스팅명 | `kr.gronox/finbridge` | PLAN.md | 서두 | 2026-09-24 | 아니오 |
| 최신 버전 | 0.1.4(active, 2026-09-09) | PLAN.md | 지금 상태 | 2026-09-24 | 아니오 |
| MCP 엔드포인트 | `https://mcp.gronox.kr/mcp` | README.md | 서두 | 2026-09-24 | 아니오 |
| REST API | `https://mcp.gronox.kr/api/v1`, OpenAPI `https://mcp.gronox.kr/api/v1/openapi.json` | README.md | 서두 | 2026-09-24 | 아니오 |
| 웹 도메인 | `https://www.gronox.kr`(제품/키/요금), `/ko`, `/ja` | README.md | Links | 2026-09-24 | 아니오 |
| 상태 페이지 | `https://mcp.gronox.kr/status` | README.md | Links | 2026-09-24 | 아니오 |
| 게시 CLI | `mcp-publisher.exe`(1.8.1로 검증, 2026-09-09) | WORKLOG.md | 2026-09-09 | 2026-09-24 | 아니오 |
| 서명 개인키 파일 | `mcp-registry-key.hex`(폴더 밖 반출 금지) | PLAN.md | 운영 메모 | 2026-09-24 | 예(경로만) |
| 서명 공개키 파일 | `mcp-registry-pub.hex` | 디렉토리 목록 | 루트 | 2026-09-24 | 아니오 |
| 도메인 인증 방식 | apex well-known(HTTP), GET만 200·HEAD는 302 | PLAN.md | 운영 메모 | 2026-09-24 | 아니오 |
| 무료 플랜 한도 | 하루 200회, 전 도구, 최근 4개 회계연도·130거래일 | README.md | 서두 | 2026-09-24 | 아니오(판매 조건) |
| 연락처 | 4y.changemaker@gmail.com | README.md | Notes | 2026-09-24 | 아니오 |
| 저장소 라이선스 | 리스팅·문서는 MIT(호스팅 서비스 본체는 별도 ToS) | README.md | License | 2026-09-24 | 아니오 |
| 타 등재처 | Smithery `red0920/finbridge`, mcp.so | README.md | Links | 2026-09-24 | 아니오 |
