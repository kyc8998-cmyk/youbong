# youbong

## 한글(HWP/HWPX) 문서 연동

이 저장소에는 Claude Code가 HWP/HWPX 파일을 다룰 수 있도록 두 가지 연동이 설정되어 있습니다.
저장소를 열고 Claude Code를 시작하면 설정 승인 안내가 나옵니다.

### 1. HWP-MCP (`.mcp.json`)

```bash
claude mcp add hwp-mcp -- uvx --from hwp-mcp --with "mcp<2" hwp-mcp
```

위 명령을 프로젝트 범위(`--scope project`)로 실행한 것과 같습니다.

- 필요 조건: [uv](https://docs.astral.sh/uv/) (`uvx`)
- `--with "mcp<2"`가 필요한 이유: `hwp-mcp` 0.1.1은 `mcp>=1.0.0`만 지정하고 있어 mcp 2.x가 설치되는데,
  2.x에서는 `mcp.server.fastmcp`가 없어져 서버가 `ModuleNotFoundError`로 시작하지 못합니다.
- 제공 도구: `read_hwp`, `read_hwp_text`, `read_hwp_tables`, `list_hwp_images`,
  `extract_hwp_images`, `fill_hwp_template`, `replace_hwp_text`, `create_hwpx_document`

### 2. kordoc 플러그인 (`.claude/settings.json`)

```
/plugin marketplace add chrisryugj/kordoc
/plugin install kordoc@kordoc
```

위 두 명령에 해당하는 설정(`extraKnownMarketplaces`, `enabledPlugins`)이 들어 있어,
저장소를 신뢰(trust)하면 마켓플레이스 추가와 플러그인 설치 안내가 나옵니다.

- 필요 조건: Node.js 20+ (kordoc 플러그인은 npm `kordoc` CLI/MCP를 사용)
- 한컴오피스 없이 HWP 3.x/5.x, HWPX, HWPML, PDF, DOCX, XLS/XLSX 파싱·생성·서식 채우기 지원
