---
title: "SSA Manager によるアクセストークンの取得"
url: "https://blog.autodesk.io/retrieving-access-token-with-ssa-manager/"
date: "2026-07-22"
author: "Toshiaki Isezaki"
feed_url: "https://blog.autodesk.io/feed/"
---
Secure Service Account（SSA）API サンプルに、手動で SSA をテストする際に役立つ SSA Manager サンプル があります。SSA は秘密鍵から JWT アサーションを経て、 3-legged 認証フローのアクセス トークンを取得するソリューションですが、SSA API の使用方法を公開するだけでなく、生成するロボット アカウントを手動でテストする目的にも利用することが出来ます。 少し冗長な気もしますが、ここでは、SSA Manager（SSA Management Tool）の Live デモでもある https://ssa-manager.autodesk.io/ にアクセスして、アクセストークンを得る手順についてご紹介しておきたいと思います。 [Copy Token] >> [Open on jwt.io] の順でボタンをクリックすると、https://www.jwt.io/ が開いてデコードされたトークン情報を確認することが出来ます。 SSA API でロボットアカウント作成の自動化をする場合には、MCP サーバー サンプル aps-mcp-app-example の https://github.com/autodesk-platform-services/aps-mcp-app-example/blob/develop/auth.js
