---
{"dg-publish":true,"permalink":"/ai-technique/mcp/mcp-model-context-protocol/","dg-note-properties":{}}
---

Claude같은 AI 서비스에서 특정 Appliance을 MCP로 연결하면 AI 서비스(예, Cluade)에게 어떤 작업을 요청하면 MCP로 연결된 특정 Appliance가 동작한다.

이것이 동작하게 된 배경은 특정 Application이 MCP Server를 개발하고 내장했기 때문에 가능하다.

예를 들어 Notion은 MCP Server를 만들어서 내장했기 때문에
사용자는 Notion의 MCP를 Claude에 연결하면,
사용자가 Claude에게 요청한 작업을 결과물이 Notion에서 실행되게 됩니다.

> [!note] Claude에서 connector
> Claude에서 `커넥터`는 그래픽 설정 흐름을 갖춘 MCP 서버이다.




