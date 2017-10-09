---
title: "aaaUse PowerShell toomanage Azure Event Hubs kaynakları | Microsoft Docs"
description: "PowerShell modülü toocreate kullanma ve olay hub'ları yönetme"
services: event-hubs
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: d79cb307c2b4a031d059ce6ca67117ffc0b4600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-event-hubs-resources"></a><span data-ttu-id="9f950-103">PowerShell toomanage olay hub'ları kaynakları kullanın</span><span class="sxs-lookup"><span data-stu-id="9f950-103">Use PowerShell toomanage Event Hubs resources</span></span>

<span data-ttu-id="9f950-104">Microsoft Azure PowerShell toocontrol kullanın ve hello dağıtımını ve Azure Hizmetleri yönetimini otomatikleştirmek bir komut dosyası ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="9f950-104">Microsoft Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of Azure services.</span></span> <span data-ttu-id="9f950-105">Bu makalede nasıl toouse hello [olay hub'ları Resource Manager PowerShell Modülü](/powershell/module/azurerm.eventhub) tooprovision ve Event Hubs varlıkları (ad, tek tek olay hub'ları ve tüketici grupları) yönetmek yerel bir Azure PowerShell konsolunu kullanarak veya komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="9f950-105">This article describes how toouse hello [Event Hubs Resource Manager PowerShell module](/powershell/module/azurerm.eventhub) tooprovision and manage Event Hubs entities (namespaces, individual event hubs, and consumer groups) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="9f950-106">Olay hub'ları kaynakları Azure Resource Manager şablonları kullanarak da yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f950-106">You can also manage Event Hubs resources using Azure Resource Manager templates.</span></span> <span data-ttu-id="9f950-107">Daha fazla bilgi için hello makalesine bakın [bir Azure Resource Manager şablonu kullanarak olay hub'ı ve tüketici grubu ile bir olay hub'ları ad alanı oluşturma](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="9f950-107">For more information, see hello article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f950-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9f950-108">Prerequisites</span></span>

<span data-ttu-id="9f950-109">Başlamadan önce hello aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="9f950-109">Before you begin, you'll need hello following:</span></span>

* <span data-ttu-id="9f950-110">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="9f950-110">An Azure subscription.</span></span> <span data-ttu-id="9f950-111">Bir aboneliği edinme hakkında daha fazla bilgi için bkz: [satın alma seçeneği][purchase options], [üye teklifleri][member offers], veya [boş Hesap][free account].</span><span class="sxs-lookup"><span data-stu-id="9f950-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="9f950-112">Azure PowerShell ile bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="9f950-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="9f950-113">Yönergeler için bkz: [Azure PowerShell cmdlet'leri kullanmaya başlama](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="9f950-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="9f950-114">PowerShell komut dosyaları, NuGet paketlerini ve hello .NET Framework genel anlama.</span><span class="sxs-lookup"><span data-stu-id="9f950-114">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="9f950-115">başlarken</span><span class="sxs-lookup"><span data-stu-id="9f950-115">Get started</span></span>

<span data-ttu-id="9f950-116">Merhaba ilk toouse PowerShell toolog tooyour Azure hesabı olarak ve Azure aboneliğine adımdır.</span><span class="sxs-lookup"><span data-stu-id="9f950-116">hello first step is toouse PowerShell toolog in tooyour Azure account and Azure subscription.</span></span> <span data-ttu-id="9f950-117">Merhaba yönergeleri izleyin [Azure PowerShell cmdlet'leri kullanmaya başlama](/powershell/azure/get-started-azureps) tooyour Azure hesabı toolog sonra almak ve Azure aboneliğinizde hello kaynaklarına erişim.</span><span class="sxs-lookup"><span data-stu-id="9f950-117">Follow hello instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure account, then retrieve and access hello resources in your Azure subscription.</span></span>

## <a name="provision-an-event-hubs-namespace"></a><span data-ttu-id="9f950-118">Bir olay hub'ları ad alanı sağlama</span><span class="sxs-lookup"><span data-stu-id="9f950-118">Provision an Event Hubs namespace</span></span>

<span data-ttu-id="9f950-119">Olay hub'ları ad alanları ile çalışırken hello kullanabilirsiniz [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [yeni AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Kaldır AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) , ve [kümesi AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlet'leri.</span><span class="sxs-lookup"><span data-stu-id="9f950-119">When working with Event Hubs namespaces, you can use hello [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace), and [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.</span></span>

<span data-ttu-id="9f950-120">Bu örnek, birkaç yerel değişkenler hello komut dosyasında oluşturur; `$Namespace` ve `$Location`.</span><span class="sxs-lookup"><span data-stu-id="9f950-120">This example creates a few local variables in hello script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="9f950-121">`$Namespace`Merhaba toowork ile istiyoruz hello olay hub'ları ad alanının adıdır.</span><span class="sxs-lookup"><span data-stu-id="9f950-121">`$Namespace` is hello name of hello Event Hubs namespace with which we want toowork.</span></span>
* <span data-ttu-id="9f950-122">`$Location`Merhaba veri merkezinde hangi tanımlayan hello ad sağlamak.</span><span class="sxs-lookup"><span data-stu-id="9f950-122">`$Location` identifies hello data center in which will we provision hello namespace.</span></span>
* <span data-ttu-id="9f950-123">`$CurrentNamespace`Biz almak (veya oluşturduğunuz) hello başvuru ad alanı depolar.</span><span class="sxs-lookup"><span data-stu-id="9f950-123">`$CurrentNamespace` stores hello reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="9f950-124">Gerçek bir betik içinde `$Namespace` ve `$Location` parametre olarak geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="9f950-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="9f950-125">Merhaba komut dosyasının bu bölümü, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="9f950-125">This part of hello script does hello following:</span></span>

1. <span data-ttu-id="9f950-126">Deneme tooretrieve hello bir olay hub'ları ad alanı adı belirtildi.</span><span class="sxs-lookup"><span data-stu-id="9f950-126">Attempts tooretrieve an Event Hubs namespace with hello specified name.</span></span>
2. <span data-ttu-id="9f950-127">Merhaba ad bulunursa, bulunanları bildirir.</span><span class="sxs-lookup"><span data-stu-id="9f950-127">If hello namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="9f950-128">Merhaba ad alanı bulunmazsa hello ad alanı oluşturur ve sonra yeni ad alanı oluşturulan hello alır.</span><span class="sxs-lookup"><span data-stu-id="9f950-128">If hello namespace is not found, it creates hello namespace and then retrieves hello newly created namespace.</span></span>

    ```powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
    }
    ```

## <a name="create-an-event-hub"></a><span data-ttu-id="9f950-129">Olay hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9f950-129">Create an event hub</span></span>

<span data-ttu-id="9f950-130">toocreate bir event hub hello önceki bölümde hello komut dosyası kullanarak bir ad alanı denetimi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="9f950-130">toocreate an event hub, perform a namespace check using hello script in hello previous section.</span></span> <span data-ttu-id="9f950-131">Ardından hello kullanın [yeni AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet toocreate hello olay hub'ı:</span><span class="sxs-lookup"><span data-stu-id="9f950-131">Then, use hello [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet toocreate hello event hub:</span></span>

```powershell
# Check if event hub already exists
$CurrentEH = Get-AzureRMEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName

if($CurrentEH)
{
    Write-Host "hello event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $EventHubName event hub does not exist."
    Write-Host "Creating hello $EventHubName event hub in hello $Location region..."
    New-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -Location $Location -MessageRetentionInDays 3
    $CurrentEH = Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $EventHubName event hub in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="create-a-consumer-group"></a><span data-ttu-id="9f950-132">Bir tüketici grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="9f950-132">Create a consumer group</span></span>

<span data-ttu-id="9f950-133">toocreate bir event hub tüketici grubunda hello önceki bölümde hello komut dosyalarını kullanarak hello ad alanı ve olay hub'ı denetimleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="9f950-133">toocreate a consumer group within an event hub, perform hello namespace and event hub checks using hello scripts in hello previous section.</span></span> <span data-ttu-id="9f950-134">Ardından hello kullanın [yeni AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet toocreate hello tüketici grubu hello olay hub'ı içinde.</span><span class="sxs-lookup"><span data-stu-id="9f950-134">Then, use hello [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet toocreate hello consumer group within hello event hub.</span></span> <span data-ttu-id="9f950-135">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="9f950-135">For example:</span></span>

```powershell
# Check if consumer group already exists
$CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -ErrorAction Ignore

if($CurrentCG)
{
    Write-Host "hello consumer group $ConsumerGroupName in event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $ConsumerGroupName consumer group does not exist."
    Write-Host "Creating hello $ConsumerGroupName consumer group in hello $Location region..."
    New-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
    $CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $ConsumerGroupName consumer group in event hub $EventHubName in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

#### <a name="set-user-metadata"></a><span data-ttu-id="9f950-136">Set kullanıcı meta verileri</span><span class="sxs-lookup"><span data-stu-id="9f950-136">Set user metadata</span></span>

<span data-ttu-id="9f950-137">Önceki bölümlerde hello Hello betikleri yürüttükten sonra hello kullanabilirsiniz [kümesi AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet tooupdate hello aşağıdaki örneğine hello gibi bir tüketici grubu özelliklerini:</span><span class="sxs-lookup"><span data-stu-id="9f950-137">After executing hello scripts in hello preceding sections, you can use hello [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet tooupdate hello properties of a consumer group, as in hello following example:</span></span>

```powershell
# Set some user metadata on hello CG
Write-Host "Setting hello UserMetadata field too'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a><span data-ttu-id="9f950-138">Olay hub'ı kaldırma</span><span class="sxs-lookup"><span data-stu-id="9f950-138">Remove event hub</span></span>

<span data-ttu-id="9f950-139">oluşturduğunuz tooremove hello olay hub'ları, kullanabileceğiniz hello `Remove-*` aşağıdaki örneğine hello olduğu gibi cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9f950-139">tooremove hello event hubs you created, you can use hello `Remove-*` cmdlets, as in hello following example:</span></span>

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a><span data-ttu-id="9f950-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9f950-140">Next steps</span></span>

- <span data-ttu-id="9f950-141">Merhaba tam olay hub'ları Resource Manager PowerShell modülü belgelerine bakın [burada](/powershell/module/azurerm.eventhub).</span><span class="sxs-lookup"><span data-stu-id="9f950-141">See hello complete Event Hubs Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.eventhub).</span></span> <span data-ttu-id="9f950-142">Bu sayfa, tüm kullanılabilir cmdlet'leri listeler.</span><span class="sxs-lookup"><span data-stu-id="9f950-142">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="9f950-143">Azure Resource Manager şablonları kullanma hakkında daha fazla bilgi için bkz: hello makale [bir Azure Resource Manager şablonu kullanarak olay hub'ı ve tüketici grubu ile bir olay hub'ları ad alanı oluşturma](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="9f950-143">For information about using Azure Resource Manager templates, see hello article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>
- <span data-ttu-id="9f950-144">Hakkında bilgi [olay hub'ları .NET Yönetim kitaplıklarını](event-hubs-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="9f950-144">Information about [Event Hubs .NET management libraries](event-hubs-management-libraries.md).</span></span>

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
