---
title: "Powershell komut dosyalarıyla Azure Search aaaManage | Microsoft Docs"
description: "PowerShell komut dosyalarıyla Azure Search hizmetinizi yönetme. Oluşturma veya güncelleştirme bir Azure Search hizmeti ve Azure Search yönetici anahtarları Yönet"
services: search
documentationcenter: 
author: seansaleh
manager: mblythe
editor: 
tags: azure-resource-manager
ms.assetid: 9b3dc1f2-3619-4235-ba1f-d2d6f5c45dd5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: powershell
ms.date: 08/15/2016
ms.author: seasa
ms.openlocfilehash: fc7fb4b025340c77717601e0aaee938be3e9230f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-search-service-with-powershell"></a>PowerShell ile Azure Search hizmetinizi yönetme
> [!div class="op_single_selector"]
> * [Portal](search-manage.md)
> * [PowerShell](search-manage-powershell.md)
> 
> 

Bu konuda hello PowerShell komutları tooperform birçok hello Azure arama hizmetleri için yönetim görevleri açıklar. Bir arama hizmeti oluşturma, ölçeklendirme ve API anahtarını yönetme size yol gösterir.
Bu komutlar hello yönetim seçenekleri hello paralel [Azure Search Yönetimi REST API'si](http://msdn.microsoft.com/library/dn832684.aspx).

## <a name="prerequisites"></a>Ön koşullar
* Azure PowerShell 1.0 veya daha büyük olmalıdır. Yönergeler için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview).
* Tooyour aşağıda açıklandığı gibi PowerShell'de Azure aboneliği içindeki oturum açmanız gerekir.

İlk olarak, şunları yapmalısınız oturum açma tooAzure bu komutla:

    Login-AzureRmAccount

Merhaba Microsoft Azure oturum açma iletişim kutusunda Azure hesabınızı ve kendi parolasını Hello e-posta adresini belirtin.

Alternatif olarak [bir hizmet sorumlusu ile etkileşimli oturum açma](../azure-resource-manager/resource-group-authenticate-service-principal.md).

Birden çok Azure aboneliğiniz varsa, Azure aboneliğinizin tooset gerekir. toosee geçerli aboneliklerinizi listesini bu komutu çalıştırın.

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

toospecify hello abonelik, komutu aşağıdaki hello çalıştırın. Aşağıdaki örneğine hello hello abonelik adıdır `ContosoSubscription`.

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-toohelp-you-get-started"></a>Komutları toohelp kullanmaya başlama
    $serviceName = "your-service-name-lowercase-with-dashes"
    $sku = "free" # or "basic" or "standard" for paid services
    $location = "West US"
    # You can get a list of potential locations with
    # (Get-AzureRmResourceProvider -ListAvailable | Where-Object {$_.ProviderNamespace -eq 'Microsoft.Search'}).Locations
    $resourceGroupName = "YourResourceGroup" 
    # If you don't already have this resource group, you can create it with 
    # New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Register hello ARM provider idempotently. This must be done once per subscription
    Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Search"

    # Create a new search service
    # This command will return once hello service is fully created
    New-AzureRmResourceGroupDeployment `
        -ResourceGroupName $resourceGroupName `
        -TemplateUri "https://gallery.azure.com/artifact/20151001/Microsoft.Search.1.0.9/DeploymentTemplates/searchServiceDefaultTemplate.json" `
        -NameFromTemplate $serviceName `
        -Sku $sku `
        -Location $location `
        -PartitionCount 1 `
        -ReplicaCount 1

    # Get information about your new service and store it in $resource
    $resource = Get-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # View your resource
    $resource

    # Get hello primary admin API key
    $primaryKey = (Invoke-AzureRmResourceAction `
        -Action listAdminKeys `
        -ResourceId $resource.ResourceId `
        -ApiVersion 2015-08-19).PrimaryKey

    # Regenerate hello secondary admin API Key
    $secondaryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/regenerateAdminKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action secondary).SecondaryKey

    # Create a query key for read only access tooyour indexes
    $queryKeyDescription = "query-key-created-from-powershell"
    $queryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/createQueryKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action $queryKeyDescription).Key

    # View your query key
    $queryKey

    # Delete query key
    Remove-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices/deleteQueryKey/$($queryKey)" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # Scale your service up
    # Note that this will only work if you made a non "free" service
    # This command will not return until hello operation is finished
    # It can take 15 minutes or more tooprovision hello additional resources
    $resource.Properties.ReplicaCount = 2
    $resource | Set-AzureRmResource

    # Delete your service
    # Deleting your service will delete all indexes and data in hello service
    $resource | Remove-AzureRmResource

## <a name="next-steps"></a>Sonraki Adımlar
Hizmetiniz oluşturulur, hello sonraki adımlar alabilir: derleme bir [dizin](search-what-is-an-index.md), [dizin sorgu](search-query-overview.md), son olarak oluşturulur ve Azure Search kullanan kendi arama uygulamasını Yönet.

* [Hello Azure portalında bir Azure Search dizini oluşturma](search-create-index-portal.md)
* [Arama Gezgini hello Azure portal kullanarak Azure Search dizini sorgulama](search-explorer.md)
* [Bir dizin oluşturucu tooload verileri diğer hizmetlerden Kurulumu](search-indexer-overview.md)
* [Azure toouse arama nasıl .NET](search-howto-dotnet-sdk.md)
* [Azure Search trafiğini analiz](search-traffic-analytics.md)

