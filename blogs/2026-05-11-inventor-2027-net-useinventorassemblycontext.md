---
title: "Inventor 2027 における .NET アドインの依存関係管理 ～ UseInventorAssemblyContext の追加"
url: "https://blog.autodesk.io/inventor-2027-dotnet-addin-dependency-isolation/"
date: "Mon, 11 May 2026 04:26:51 +0000"
author: "Takehiro Kato"
feed_url: "https://blog.autodesk.io/feed/"
---
Inventor 2025 以降、Inventor アドイン開発は .NET Framework ベースから .NET ベースへ移行しました。 これにより、最新の .NET ライブラリや NuGet パッケージを利用しやすくなった一方で、複数のアドイン間で依存 DLL や依存ライブラリのバージョン競合が発生しやすくなるケースも見られるようになりました。 例えば、 といった場合に、意図しない DLL が読み込まれたり、実行時エラーが発生したりする可能性があります。 Inventor 2027 では、このような .NET アドインの依存関係管理に関して改善が行われています。 本記事では、Inventor 2027 に追加された UseInventorAssemblyContext 設定と、依存関係分離の考え方について紹介します。 DLL Hell と依存関係管理の歴史 Windows アプリケーション開発では、以前から DLL の依存関係管理が課題になることがありました。 特に、異なるバージョンの DLL を複数のアプリケーションやプラグインが共有する場合、 といった問題が発生することがあります。 こうした問題は、一般的に “DLL Hell” と呼ばれてきました。 Inventor のアドイン開発も、長い間 COM ベースで行われてきました。 COM ベースの Add-in…
