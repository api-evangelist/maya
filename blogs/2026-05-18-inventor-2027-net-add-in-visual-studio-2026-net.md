---
title: "Inventor 2027 の .NET Add-in 開発と Visual Studio 2026 ～.NET プロジェクトテンプレート"
url: "https://blog.autodesk.io/inventor-2027-dotnet-addin-visualstudio-2026/"
date: "2026-05-18"
author: "Takehiro Kato"
feed_url: "https://blog.autodesk.io/feed/"
---
Inventor 2027 では、.NET ベースの Add-in 開発環境が更新され、.NET 10 ベースでの開発へ移行しています。 これに伴い、Inventor Add-in 開発でも Visual Studio 2026 を利用するケースが増えてくると考えられます。 一方で、現時点では Inventor SDK に含まれる一部ツールについて、まだ Visual Studio 2026 への対応が完全ではない状況が確認されています。 今回は、その中でも DeveloperTools.msi に関する現状について共有したいと思います。 現在確認されている状況 Inventor 2027 SDK に含まれるDeveloperTools.msiを Visual Studio 2026 環境で実行した場合、 “Could not find any version of Microsoft Visual Studio” というメッセージが表示され、正常にセットアップを進めることができません。 これは、現在のところDeveloperTools.msiの Visual Studio 検出処理が VS2026 に対応していないためです。 背景 Inventor 2027 は […]
