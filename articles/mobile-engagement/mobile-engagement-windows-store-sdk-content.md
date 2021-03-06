---
title: Windows ユニバーサル アプリ SDK コンテンツ
description: Azure Mobile Engagement 向け Windows ユニバーサル アプリ SDK の内容詳細
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: dwrede
editor: ''

ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo

---
# Windows ユニバーサル アプリ SDK コンテンツ
このドキュメントでは、アプリケーションで SDK により展開されるコンテンツについて説明します。

## `/Resources` フォルダー
このフォルダーには、Mobile Engagement が必要とするすべてのリソースが含まれています。アプリに適合するように、これらをカスタマイズすることもできます。

* `EngagementConfiguration.xml`: Mobile Engagement の構成ファイルであり、エンゲージメントの設定をカスタマイズできます (Mobile Engagement 接続文字列、クラッシュ レポートなど)。

### /html フォルダー
* `EngagementNotification.html`: アプリ内バナー用の `Notification` Web ビュー html デザイン。
* `EngagementAnnouncement.html`: アプリ内スポット ビュー用の `Announcement` Web ビュー html デザイン。

### /images フォルダー
* `EngagementIconNotification.png`: 通知の左側に表示されるブランド アイコン。これは自分のブランド アイコンに換えます。
* `EngagementIconOk.png` : Reach コンテンツ ページの [`Ok`] アイコン (アクション ボタンまたは検証ボタンとして使用)。
* `EngagementIconNOK.png` : Reach コンテンツ ページの検証ボタンが無効の場合に使用する [`NOK`] アイコン。
* `EngagementIconClose.png` : Reach 通知やコンテンツの [`Close`] アイコン (閉じるボタンとして使用)。

### /overlay フォルダー
* `EngagementPageOverlay.cs`: Engagement Reach アプリ内 UI を子に追加するためのオーバーレイ ページ。

<!---HONumber=AcomDC_0824_2016-->