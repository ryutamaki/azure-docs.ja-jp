---
title: Azure Security Center のデータ収集を有効にする | Microsoft Docs
description: " Azure Security Center のデータ収集を有効にする方法について説明します。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''

ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/29/2016
ms.author: terrylan

---
# Azure Security Center のデータ収集を有効にする
Azure Security Center では、脅威に対する防御と検出、対応を支援するために、構成情報、メタデータ、イベント ログなど、Azure 仮想マシンに関するさまざまなデータを収集、処理しています。最初に Security Center にアクセスするときは、サブスクリプション内のすべての仮想マシンに対してデータ収集が有効になっています。データ収集は有効にしておくことをお勧めしますが、Security Center のポリシーでデータ収集をオフにして、オプトアウトすることもできます ([データ収集の無効化](#disabling-data-collection)を参照)。データ収集を無効にすると、そのサブスクリプションのセキュリティ ポリシーでデータ収集を有効にするよう Security Center から提案されます。

> [!NOTE]
> このドキュメントでは、サンプルのデプロイを使用してサービスについて紹介します。ステップ バイ ステップ ガイドではありません。
> 
> 

## 推奨事項の実装
1. **[セキュリティ センター]** ブレードの **[推奨事項]** タイルを選択します。**[推奨事項]** ブレードが表示されます。 ![[セキュリティ センター] ブレード][1]
2. **[推奨事項]** ブレードの **[Enable data collection for subscriptions (サブスクリプションのデータ収集の有効化)]** を選択します。**[Turn on data collection (データ収集の有効化)]** ブレードが表示されます。 ![Recommendations blade][2]
3. **[Turn on data collection (データ収集の有効化)]** ブレードで、該当するサブスクリプションを選択します。対応するサブスクリプションの **[セキュリティ ポリシー]** ブレードが表示されます。
4. **[セキュリティ ポリシー]** ブレードで、**[データ収集]** の下の **[オン]** を選択すると、自動的にログが収集されます。また、データの収集をオンにすると、サブスクリプションの既存の VM と、サポートされる新しい VM のすべてで、監視拡張機能がプロビジョニングされるようになります。 ![Security policy blade][3]
5. [**保存**] を選択します。
6. **[Choose a storage account per region (リージョンごとにストレージ アカウントを選択)]** を選択します。実行している仮想マシンがある各リージョンに対し、これらの仮想マシンから収集されたデータが格納されているストレージ アカウントを選択します。リージョンごとにストレージ アカウントを選択しないと、自動的に作成されます。この例では、**[newstoracct]** を選択します。ストレージ アカウントは後から変更できます。変更する場合は、該当するサブスクリプションのセキュリティ ポリシーに戻り、別のストレージ アカウントを選択してください。 ![Choose a storage account][4]
7. **[OK]** を選択します。

> [!NOTE]
> データ収集を有効にして、最初にサブスクリプション レベルでストレージ アカウントを選択することをお勧めします。セキュリティ ポリシーは Azure サブスクリプション レベルとリソース グループ レベルで設定できますが、データ収集とストレージ アカウントの構成はサブスクリプション レベルでのみ発生します。
> 
> 

## データ収集の有効化後
データ収集は、Azure Monitoring Agent と Azure セキュリティの監視拡張機能を使用して有効にします。Azure セキュリティの監視拡張機能は、さまざまなセキュリティ関連の構成をスキャンして、[Windows イベント トレーシング](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) トレースに送信します。さらに、オペレーティング システムでは、イベント ログ エントリが作成されます。Azure Monitoring Agent は、イベント ログ エントリと ETW トレースを読み取り、分析のためにそれらをストレージ アカウントにコピーします。またストレージ アカウントには、監視エージェントによってクラッシュ ダンプ ファイルがコピーされます。これは、セキュリティ ポリシーで構成したストレージ アカウントです。

## データ収集の無効化
データ収集はいつでも無効にすることができます。データ収集を無効にすると、Security Center によってインストールされていた監視エージェントが削除されます。データ収集を無効にするサブスクリプションを選択してください。

> [!NOTE]
> セキュリティ ポリシーは Azure サブスクリプション レベルとリソース グループ レベルで設定できますが、データの収集をオフにするには、サブスクリプションを選択する必要があります。
> 
> 

1. **[セキュリティ センター]** ブレードに戻り、**[ポリシー]** タイルを選択します。**[セキュリティ ポリシー - サブスクリプションまたはリソース グループごとにポリシーを定義する]** ブレードが表示されます。![Select the policy tile][5]
2. **[セキュリティ ポリシー - サブスクリプションまたはリソース グループごとにポリシーを定義する]** ブレードで、データ収集を無効にするサブスクリプションを選択します。 ![Select subscription to disable data collection][6]
3. 対応するサブスクリプションの **[セキュリティ ポリシー]** ブレードが表示されます。[データ収集] の下の **[オフ]** を選択します。
4. 上部のリボンで **[保存]** を選択します。
5. 上部のリボンにある **[エージェントを削除]** を選択し、既存の仮想マシンからエージェントを削除します。

## 関連項目
この記事では、"データ収集の有効化" という Security Center の推奨事項を実践する方法について説明しました。 セキュリティ センターの詳細については、次を参照してください。

* 「[Azure セキュリティ センターでのセキュリティ ポリシーの設定](security-center-policies.md)」 -- Azure サブスクリプションとリソース グループに対するセキュリティ ポリシーの構成方法について説明しています。
* 「[Azure セキュリティ センターでのセキュリティに関する推奨事項の管理](security-center-recommendations.md)」 -- 推奨事項に従って Azure リソースを保護する方法について説明しています。
* 「[Azure セキュリティ センターでのセキュリティ ヘルスの監視](security-center-monitoring.md)」-- Azure リソースの正常性を監視する方法について説明しています。
* 「[Azure セキュリティ センターでのセキュリティの警告の管理と対応](security-center-managing-and-responding-alerts.md)」-- セキュリティ警告の管理および対応方法について説明しています。
* 「[Azure Security Center を使用したパートナー ソリューションの監視](security-center-partner-solutions.md)」 -- パートナー ソリューションの正常性状態を監視する方法について説明しています。
* 「[Azure セキュリティ センターのよく寄せられる質問 (FAQ)](security-center-faq.md)」-- このサービスの使用に関してよく寄せられる質問を確認できます。
* [Azure セキュリティ ブログ](http://blogs.msdn.com/b/azuresecurity/) -- Azure のセキュリティに関する最新のニュースと情報を入手できます。

<!--Image references-->
[1]: ./media/security-center-enable-data-collection/security-center-blade.png
[2]: ./media/security-center-enable-data-collection/recommendations.png
[3]: ./media/security-center-enable-data-collection/data-collection.png
[4]: ./media/security-center-enable-data-collection/storage-account.png
[5]: ./media/security-center-enable-data-collection/policy.png
[6]: ./media/security-center-enable-data-collection/disable-data-collection.png

<!---HONumber=AcomDC_0803_2016-->