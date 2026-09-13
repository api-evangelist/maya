---
title: "Nearing your API quota 警告について"
url: "https://blog.autodesk.io/about-nearing-your-api-quota-warning/"
date: "2026-09-09"
author: "Toshiaki Isezaki"
feed_url: "https://blog.autodesk.io/feed/"
---
APS の割り当て量通知による更なる可視性とコントロール でご案内している APS の割り当て量通知機能によって、デベロッパーハブの表示時に「Nearing your API quota Your team is approaching its quota for some APIs. Apps that depend on these services may be affected.」の警告がバナー表示されたり、警告メールが送信される場合があります。 バナー表示右手にある View affected APIs をクリックすると、直近の使用状況から推測された影響が出そうな API が表示されます。 この通知は、チームにトークン残高がある場合にもバナー表示、またはメール送信されます。これは、APS 通知が 現在現時点（2026年8月）で警告の指標である API 毎の合計割り当て量（システム内部使用）を元にで送信されるよう設計されているためです。 違った説明を用いると、APS 使用状況レポート の方法で確認できる値とは別の指標（API 毎のクォータ、割り当て量）を用いて、チームに割り当てられたトークンが無くなってしまう前に通知がおこなわれています。 現在、このクォータ（割り当て量）の値や具体的な算出方法を確認するレポート機能がない状態です。一点、念頭に置いていただきたいのは、通知が消
