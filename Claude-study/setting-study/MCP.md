# MCP란?
- Model context protocol
- 외부 시스템과 AI 애플리케이션을 연결하기 위한 오픈 소스 표준
- Claude, ChatGPT 등과 같은 AI 애플리케이션과 Notion, Slack 등과 같은 외부 시스템을 연결하기 위한 표준 규칙을 의미함.
- 이러한 표준에 따라서 AI 애플리케이션과 연결하기 위해서 만들어놓은 외부 시스템 서버를 MCP 서버라고 함.

## Context7 MCP 연결
- 개발에 활용되는 프레임워크들의 공식 문서를 연결할 수 있도록 모아둔 mcp server.
- `claude mcp add --scope user context7 -- npx -y @upstash/context7-mcp --api-key YOUR_API_KEY` 명령어를 CLI에서 실행하여 mcp 서버를 설치할 수 있음.
- 설치 후에는 claude code를 실행하여, mcp 서버 허용 혹은 인증을 수행해야 함.

## MCP server 모음 사이트
- [공식 MCP server 저장소](https://github.com/modelcontextprotocol/servers)
- [Awesome MCP servers](https://github.com/punkpeye/awesome-mcp-servers)
- [MCP server hub](https://mcpserverhub.com/)
- [Glama MCP directory](https://glama.ai/mcp/servers)
- [smithery.ai](https://smithery.ai/)
