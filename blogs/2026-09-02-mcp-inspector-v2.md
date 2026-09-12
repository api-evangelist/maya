---
title: "MCP Inspector v2"
url: "https://blog.autodesk.io/mcp-inspector-v2/"
date: "2026-09-02"
author: "Toshiaki Isezaki"
feed_url: "https://blog.autodesk.io/feed/"
---
MCP Inspector の記事をご案内した後で、7月後半に MCP 2026-07-28 仕様更新と同時に MCP Inspector が更新されて、ルック＆フィールが大きく変わっています。 ここでは、Autodesk Help MCP サーバー の接続例を題材に、改めて新しい MCP Inspector と補足情報をご紹介しておきたいと思います。 リモート接続（Streamable HTTP） ローカル接続（STDIO） MCP Inspector はローカル MCP サーバーに接続してテストすることも出来ます。C:\Program Files\Autodesk\Revit 2027 MCP Server Read-Tools Technical Preview にインストールされた Revit MCP サーバーの場合、「Transport」に STDIO、「Command」に C:\Program Files\Autodesk\Revit 2027 MCP Server Read-Tools Technical Preview\Autodesk.RevitMcpServer.Stdio.exe を指定することで、MCP サーバに接続してツールを一覧し、実行することが出来ます。 VS Code で実装中の MCP サーバーを接続してテストする際、VS Code の「ターミナル
