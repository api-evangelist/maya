---
title: "MCP Inspector"
url: "https://blog.autodesk.io/mcp-inspector/"
date: "2026-07-15"
author: "Toshiaki Isezaki"
feed_url: "https://blog.autodesk.io/feed/"
---
MCP サーバーは AI エージェントによってのみ使用されるツール集のようなもので、MCP（Model Context Protocol）インタフェースによって AI エージェントと接続されます。あいにく、AI エージェントからの呼び出し以外で、MCP サーバー単体を外部から利用することは出来ません。 ただ、この状態だと MCP サーバーの単体テストやデバッグ作業に支障が出てしまうため、MCP 公式のツールとして、MCP Inspector（MCP インスペクター）が用意されています。 MCP Inspector を利用して Autodesk MCP サーバーを評価することも出来るので、ここでは APS でよく利用する Node.js 環境を前提に Autodesk Help MCP サーバー を MCP Inspector に接続してテストする例をご紹介したいと思います。
