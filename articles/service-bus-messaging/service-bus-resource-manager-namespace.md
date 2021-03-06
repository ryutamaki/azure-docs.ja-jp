---
title: Resource Manager テンプレートを使用した Service Bus 名前空間の作成 | Microsoft Docs
description: Azure Resource Manager テンプレートを使用して Service Bus 名前空間を作成します。
services: service-bus
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: ''

ms.service: service-bus
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 10/04/2016
ms.author: sethm;shvija

---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a>Azure Resource Manager テンプレートを使用した Service Bus 名前空間の作成
この記事では、Azure Resource Manager テンプレートを使用し、Standard/Basic の SKU で **Messaging** タイプの Service Bus 名前空間を作成する方法について説明します。 また、デプロイの実行用に指定するパラメーターについても取り上げます。 このテンプレートは、独自のデプロイに使用することも、要件に合わせてカスタマイズすることもできます。

テンプレートの作成の詳細については、「 [Azure Resource Manager のテンプレートの作成][Azure Resource Manager のテンプレートの作成]」を参照してください。

完全なテンプレートについては、GitHub の [Service Bus 名前空間テンプレート][Service Bus 名前空間テンプレート] を参照してください。

> [!NOTE]
> 次の Azure Resource Manager テンプレートは、ダウンロードしてデプロイすることができます。 
> 
> * [イベント ハブとコンシューマー グループを含んだ Event Hubs 名前空間を作成する](../event-hubs/event-hubs-resource-manager-namespace-event-hub.md)
> * [キューを含んだ Service Bus 名前空間を作成する](service-bus-resource-manager-namespace-queue.md)
> * [トピックとサブスクリプションを含んだ Service Bus 名前空間を作成する](service-bus-resource-manager-namespace-topic.md)
> * [キューと承認規則を含んだ Service Bus 名前空間を作成する](service-bus-resource-manager-namespace-auth-rule.md)
> 
> 最新のテンプレートを確認する場合は、「 [Azure クイックスタート テンプレート][Azure クイックスタート テンプレート] 」ギャラリーで "Service Bus" を検索してください。
> 
> 

## <a name="what-will-you-deploy?"></a>デプロイの対象
このテンプレートでは、[Basic、Standard、または Premium](https://azure.microsoft.com/pricing/details/service-bus/) の SKU で Service Bus 名前空間をデプロイします。

デプロイメントを自動的に実行するには、次のボタンをクリックします。

[![Azure へのデプロイ](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)

## <a name="parameters"></a>パラメーター
Azure リソース マネージャーを使用して、テンプレートのデプロイ時に値を指定するパラメーターを定義します。 テンプレートには、すべてのパラメーター値を含む `Parameters` という名前のセクションがあります。 これらの値のパラメーターを定義する必要があります。これらの値は、デプロイするプロジェクトやデプロイ先の環境に応じて異なります。 常に同じ値に対してはパラメーターを定義しないでください。 テンプレート内のそれぞれのパラメーターの値は、デプロイされるリソースを定義するために使用されます。

このテンプレートでは、次のパラメーターを定義します。

### <a name="servicebusnamespacename"></a>serviceBusNamespaceName
作成する Service Bus 名前空間の名前。

```
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of the Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a>serviceBusSKU
作成する Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) の名前。

```
"serviceBusSku": { 
    "type": "string", 
    "allowedValues": [ 
        "Basic", 
        "Standard",
        "Premium" 
    ], 
    "defaultValue": "Standard", 
    "metadata": { 
        "description": "The messaging tier for service Bus namespace" 
    } 

```

テンプレートには、このパラメーターに指定できる値 (Basic、Standard、または Premium) を定義します。値が指定されない場合は既定値 (Standard) が割り当てられます。

Service Bus の料金の詳細については、[「Service Bus の料金と課金」][]を参照してください。

### <a name="servicebusapiversion"></a>serviceBusApiVersion
テンプレートの Service Bus API バージョン。

```
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by the template" 
       } 
```

## <a name="resources-to-deploy"></a>デプロイ対象のリソース
### <a name="service-bus-namespace"></a>Service Bus 名前空間
**Messaging**タイプの標準的な Service Bus 名前空間を作成します。

```
"resources": [
    {
        "apiVersion": "[parameters('serviceBusApiVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "properties": {
        }
    }
]
```

## <a name="commands-to-run-deployment"></a>デプロイを実行するコマンド
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
```
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a>Azure CLI
```
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a>次のステップ
Azure Resource Manager を使ってリソースを作成し、デプロイしたら、それらのリソースの管理方法を次の記事で確認してください。

* [PowerShell で Service Bus を管理する](../service-bus/service-bus-powershell-how-to-provision.md)
* [Service Bus リソースを Service Bus Explorer で管理する](https://code.msdn.microsoft.com/Service-Bus-Explorer-f2abca5a)

[Azure Resource Manager のテンプレートの作成]: ../resource-group-authoring-templates.md
[Service Bus 名前空間テンプレート]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure クイックスタート テンプレート]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus の料金と課金]: https://azure.microsoft.com/documentation/articles/service-bus-pricing-billing/
[Azure リソース マネージャーでの Azure PowerShell の使用]: ../powershell-azure-resource-manager.md
[Azure リソース管理での、Mac、Linux、および Windows 用 Azure CLI の使用]: ../xplat-cli-azure-resource-manager.md



<!--HONumber=Oct16_HO2-->


