---
title: "Resource Manager でテンプレートを使用して内部ロード バランサーを作成する | Microsoft Docs"
description: "リソース マネージャーでテンプレートを使用して、内部ロード バランサーを作成する方法について説明します"
services: load-balancer
documentationcenter: na
author: sdwheeler
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 64150862-6ced-42de-85dc-89d323257d7c
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: sewhee
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: 482c9cd46902d9e3f4e1e0f001182fdb43ce9367


---
# <a name="create-an-internal-load-balancer-using-a-template"></a>テンプレートを使用した内部ロード バランサーの作成
[!INCLUDE [load-balancer-get-started-ilb-arm-selectors-include.md](../../includes/load-balancer-get-started-ilb-arm-selectors-include.md)]

<BR>
[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/learn-about-deployment-models-rm-include.md)]

[クラシック デプロイメント モデル](load-balancer-get-started-ilb-classic-ps.md)。

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-the-template-by-using-click-to-deploy"></a>[クリックしてデプロイ] を使用してテンプレートをデプロイする
パブリック リポジトリで使用できるサンプル テンプレートは、上記のシナリオの生成に使用した既定値を含むパラメーター ファイルを使用します。 "クリックしてデプロイ" を使用してこのテンプレートをデプロイするには、 [このリンク](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer)に従って、 **[Azure へのデプロイ]**をクリックし、必要に応じて既定のパラメーター値を置き換えて、ポータルの指示に従います。

## <a name="deploy-the-template-by-using-powershell"></a>PowerShell を使用してテンプレートをデプロイする
PowerShell を使用してダウンロードしたテンプレートをデプロイするには、次の手順に従います。

1. Azure PowerShell を初めて使用する場合は、 [Azure PowerShell のインストールおよび構成方法](../powershell-install-configure.md) を参照し、このページにある手順をすべて最後まで実行し、Azure にサインインしてサブスクリプションを選択します。
2. パラメーター ファイルをローカル ディスクにダウンロードします。
3. ファイルを編集し、保存します。
4. テンプレートを使用してリソース グループを作成するには、 **New-AzureRmResourceGroupDeployment** コマンドレットを実行します。
   
        New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
            -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
            -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'

## <a name="deploy-the-template-by-using-the-azure-cli"></a>Azure CLI を使用してテンプレートをデプロイする
Azure CLI を使用してテンプレートをデプロイするには、次の手順に従います。

1. Azure CLI を初めて使用する場合は、「 [Azure CLI のインストール](../xplat-cli-install.md) 」を参照して、Azure のアカウントとサブスクリプションを選択する時点までの指示に従います。
2. 次に示すように、 **azure config mode** コマンドを実行してリソース マネージャー モードに切り替えます。
   
        azure config mode arm
   
    上記のコマンドで想定される出力を次に示します。
   
        info:    New mode is arm
3. パラメーター ファイルを開いて内容を選択し、コンピューター内のファイルに保存します。 この例では、パラメーター ファイルを *parameters.json*に保存しました。
4. 上記でダウンロードして変更したテンプレート ファイルとパラメーター ファイルを使用し、 **azure group deployment create** コマンドを実行して、新しい内部ロード バランサーをデプロイします。 出力の後に表示される一覧では、使用されたパラメーターについて説明されています。
   
        azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json

## <a name="next-steps"></a>次のステップ
[ソース IP アフィニティを使用したロード バランサー分散モードの構成](load-balancer-distribution-mode.md)

[ロード バランサーのアイドル TCP タイムアウト設定の構成](load-balancer-tcp-idle-timeout.md)




<!--HONumber=Nov16_HO2-->


