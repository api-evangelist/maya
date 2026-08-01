---
title: "Automation API：キュー可視化を導入"
url: "https://blog.autodesk.io/introducing-queue-visibility-automation-api/"
date: "2026-07-29"
author: "Toshiaki Isezaki"
feed_url: "https://blog.autodesk.io/feed/"
---
Automation API がキューの可視化機能を追加しています。システム全体のキューのヘルスメトリクス（健全性の指標）を公開して、WorkItem 毎のキュー ポジション フィールドも 2 週間後の 2026年8月10日 を目途に配信される予定です。 現在、WorkItem を提出して GET /workitems/{id}でエンドポイントでポーリングすると、pending ステータスだけが返されます。システムが Busy 状態なのか、WorkItem がスタックしているのか、遅延がオートデスク側に起因するものなのか、あるいはアプリ側にあるのかを判断することが出来ません。 キューの可視化機能は、この問題に対して2段階で情報を提供します。 （Automation API を使用すると、開発者は Revit®、AutoCAD®、Inventor、3ds Max、および Fusion のアドイン/プラグインやワークフローを、クラウド上でプログラムによって実行して成果に応じた従量課金制で利用することが出来ます。） 何を意味するのか? キューの可視化機能導入の理由 Automation API は多くのチームのミッション クリティカルなワークフローを担っているため、キューの可視化はお客様からの頻繁に寄せられていた要望でした。ジョブが pending 状態のまま前述のような追加情報が得られ
