---
title: "aaaUse PowerShell toomanage Azure Service Bus kaynaklarını | Microsoft Docs"
description: "PowerShell modülü toocreate kullanma ve Service Bus kaynaklarını yönetme"
services: service-bus-messaging
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: sethm
ms.openlocfilehash: 737044def913c5798e7e05fc4f1aeece76c8f4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-service-bus-resources"></a><span data-ttu-id="d854d-103">PowerShell toomanage Service Bus kaynaklarını kullanma</span><span class="sxs-lookup"><span data-stu-id="d854d-103">Use PowerShell toomanage Service Bus resources</span></span>

<span data-ttu-id="d854d-104">Microsoft Azure PowerShell toocontrol kullanın ve hello dağıtımını ve Azure Hizmetleri yönetimini otomatikleştirmek bir komut dosyası ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="d854d-104">Microsoft Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of Azure services.</span></span> <span data-ttu-id="d854d-105">Bu makalede nasıl toouse hello [Service Bus Resource Manager PowerShell Modülü](/powershell/module/azurerm.servicebus) tooprovision ve hizmet veri yolu varlıklarını (ad alanları, kuyruklar, konular ve abonelikler) yönetmek yerel bir Azure PowerShell konsolunu kullanarak veya komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="d854d-105">This article describes how toouse hello [Service Bus Resource Manager PowerShell module](/powershell/module/azurerm.servicebus) tooprovision and manage Service Bus entities (namespaces, queues, topics, and subscriptions) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="d854d-106">Hizmet veri yolu varlıklarını Azure Resource Manager şablonları kullanarak da yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d854d-106">You can also manage Service Bus entities using Azure Resource Manager templates.</span></span> <span data-ttu-id="d854d-107">Daha fazla bilgi için hello makalesine bakın [oluşturma Service Bus kaynaklarını Azure Resource Manager şablonları kullanarak](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d854d-107">For more information, see hello article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d854d-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d854d-108">Prerequisites</span></span>

<span data-ttu-id="d854d-109">Başlamadan önce hello aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="d854d-109">Before you begin, you'll need hello following:</span></span>

* <span data-ttu-id="d854d-110">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="d854d-110">An Azure subscription.</span></span> <span data-ttu-id="d854d-111">Bir aboneliği edinme hakkında daha fazla bilgi için bkz: [satın alma seçeneği][purchase options], [üye teklifleri][member offers], veya [boş Hesap][free account].</span><span class="sxs-lookup"><span data-stu-id="d854d-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="d854d-112">Azure PowerShell ile bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="d854d-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="d854d-113">Yönergeler için bkz: [Azure PowerShell cmdlet'leri kullanmaya başlama](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="d854d-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="d854d-114">PowerShell komut dosyaları, NuGet paketlerini ve hello .NET Framework genel anlama.</span><span class="sxs-lookup"><span data-stu-id="d854d-114">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="d854d-115">başlarken</span><span class="sxs-lookup"><span data-stu-id="d854d-115">Get started</span></span>

<span data-ttu-id="d854d-116">Merhaba ilk toouse PowerShell toolog tooyour Azure hesabı olarak ve Azure aboneliğine adımdır.</span><span class="sxs-lookup"><span data-stu-id="d854d-116">hello first step is toouse PowerShell toolog in tooyour Azure account and Azure subscription.</span></span> <span data-ttu-id="d854d-117">Merhaba yönergeleri izleyin [Azure PowerShell cmdlet'leri kullanmaya başlama](/powershell/azure/get-started-azureps) toolog tooyour Azure hesabı ve Azure aboneliğinizde almak ve erişim hello kaynakları.</span><span class="sxs-lookup"><span data-stu-id="d854d-117">Follow hello instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure account, and retrieve and access hello resources in your Azure subscription.</span></span>

## <a name="provision-a-service-bus-namespace"></a><span data-ttu-id="d854d-118">Bir hizmet veri yolu ad alanı sağlama</span><span class="sxs-lookup"><span data-stu-id="d854d-118">Provision a Service Bus namespace</span></span>

<span data-ttu-id="d854d-119">Hizmet veri yolu ad alanları ile çalışırken hello kullanabilirsiniz [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [yeni AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), ve [kümesi AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlet'leri.</span><span class="sxs-lookup"><span data-stu-id="d854d-119">When working with Service Bus namespaces, you can use hello [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), and [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span></span>

<span data-ttu-id="d854d-120">Bu örnek, birkaç yerel değişkenler hello komut dosyasında oluşturur; `$Namespace` ve `$Location`.</span><span class="sxs-lookup"><span data-stu-id="d854d-120">This example creates a few local variables in hello script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="d854d-121">`$Namespace`Merhaba Service Bus ad alanı toowork ile istiyoruz Hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="d854d-121">`$Namespace` is hello name of hello Service Bus namespace with which we want toowork.</span></span>
* <span data-ttu-id="d854d-122">`$Location`Merhaba veri merkezinde hangi tanımlayan hello ad sağlamak.</span><span class="sxs-lookup"><span data-stu-id="d854d-122">`$Location` identifies hello data center in which will we provision hello namespace.</span></span>
* <span data-ttu-id="d854d-123">`$CurrentNamespace`Biz almak (veya oluşturduğunuz) hello başvuru ad alanı depolar.</span><span class="sxs-lookup"><span data-stu-id="d854d-123">`$CurrentNamespace` stores hello reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="d854d-124">Gerçek bir betik içinde `$Namespace` ve `$Location` parametre olarak geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="d854d-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="d854d-125">Merhaba komut dosyasının bu bölümü, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="d854d-125">This part of hello script does hello following:</span></span>

1. <span data-ttu-id="d854d-126">Deneme tooretrieve hello ile Service Bus ad alanı adı belirtildi.</span><span class="sxs-lookup"><span data-stu-id="d854d-126">Attempts tooretrieve a Service Bus namespace with hello specified name.</span></span>
2. <span data-ttu-id="d854d-127">Merhaba ad bulunursa, bulunanları bildirir.</span><span class="sxs-lookup"><span data-stu-id="d854d-127">If hello namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="d854d-128">Merhaba ad alanı bulunmazsa hello ad alanı oluşturur ve sonra yeni ad alanı oluşturulan hello alır.</span><span class="sxs-lookup"><span data-stu-id="d854d-128">If hello namespace is not found, it creates hello namespace and then retrieves hello newly created namespace.</span></span>
   
    ``` powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a><span data-ttu-id="d854d-129">Ad alanı yetkilendirme kuralı oluştur</span><span class="sxs-lookup"><span data-stu-id="d854d-129">Create a namespace authorization rule</span></span>

<span data-ttu-id="d854d-130">Merhaba aşağıdaki örnekte nasıl toomanage ad alanı yetkilendirme kurallarını kullanarak hello gösterir [yeni AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Kümesi AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), ve [Kaldır AzureRmServiceBusNamespaceAuthorizationRule cmdlet'leri](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span><span class="sxs-lookup"><span data-stu-id="d854d-130">hello following example shows how toomanage namespace authorization rules using hello [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), and [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span></span>

```powershell
# Query toosee if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if hello rule already exists or needs toobe created
if ($CurrentRule)
{
    Write-Host "hello $AuthRule rule already exists for hello namespace $Namespace."
}
else
{
    Write-Host "hello $AuthRule rule does not exist."
    Write-Host "Creating hello $AuthRule rule for hello $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "hello $AuthRule rule for hello $Namespace namespace has been successfully created."

    Write-Host "Setting rights on hello namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights toohello namespace"
    $authRuleObj.Rights.Add("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj
    $authRuleObj.Rights.Add("Manage")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Show value of primary key"
    $CurrentKey = Get-AzureRmServiceBusNamespaceKey -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
        
    Write-Host "Remove this authorization rule"
    Remove-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
}
```

## <a name="create-a-queue"></a><span data-ttu-id="d854d-131">Bir kuyruk oluşturma</span><span class="sxs-lookup"><span data-stu-id="d854d-131">Create a queue</span></span>

<span data-ttu-id="d854d-132">toocreate bir kuyruk veya konu hello önceki bölümde hello komut dosyası kullanarak bir ad alanı denetimi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="d854d-132">toocreate a queue or topic, perform a namespace check using hello script in hello previous section.</span></span> <span data-ttu-id="d854d-133">Ardından, hello kuyruk oluşturun:</span><span class="sxs-lookup"><span data-stu-id="d854d-133">Then, create hello queue:</span></span>

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "hello queue $QueueName already exists in hello $Location region:"
}
else
{
    Write-Host "hello $QueueName queue does not exist."
    Write-Host "Creating hello $QueueName queue in hello $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "hello $QueueName queue in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a><span data-ttu-id="d854d-134">Sıra özelliklerini değiştir</span><span class="sxs-lookup"><span data-stu-id="d854d-134">Modify queue properties</span></span>

<span data-ttu-id="d854d-135">Önceki bölümde hello Hello betiği yürüttükten sonra hello kullanabilirsiniz [kümesi AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet tooupdate hello aşağıdaki örneğine hello gibi bir sıranın özelliklerini:</span><span class="sxs-lookup"><span data-stu-id="d854d-135">After executing hello script in hello preceding section, you can use hello [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet tooupdate hello properties of a queue, as in hello following example:</span></span>

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a><span data-ttu-id="d854d-136">Diğer hizmet veri yolu varlıklarını sağlama</span><span class="sxs-lookup"><span data-stu-id="d854d-136">Provisioning other Service Bus entities</span></span>

<span data-ttu-id="d854d-137">Merhaba kullanabilirsiniz [Service Bus PowerShell modülünü](/powershell/module/azurerm.servicebus) tooprovision konu başlıkları ve abonelikler gibi diğer varlıklar.</span><span class="sxs-lookup"><span data-stu-id="d854d-137">You can use hello [Service Bus PowerShell module](/powershell/module/azurerm.servicebus) tooprovision other entities, such as topics and subscriptions.</span></span> <span data-ttu-id="d854d-138">Bu cmdlet'ler sözdizimsel olarak benzer toohello kuyruk oluşturma cmdlet'leri hello önceki bölümde gösterilen ' dir.</span><span class="sxs-lookup"><span data-stu-id="d854d-138">These cmdlets are syntactically similar toohello queue creation cmdlets demonstrated in hello previous section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d854d-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d854d-139">Next steps</span></span>

- <span data-ttu-id="d854d-140">Merhaba tam Service Bus Resource Manager PowerShell modülü belgelerine bakın [burada](/powershell/module/azurerm.servicebus).</span><span class="sxs-lookup"><span data-stu-id="d854d-140">See hello complete Service Bus Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.servicebus).</span></span> <span data-ttu-id="d854d-141">Bu sayfa, tüm kullanılabilir cmdlet'leri listeler.</span><span class="sxs-lookup"><span data-stu-id="d854d-141">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="d854d-142">Azure Resource Manager şablonları kullanma hakkında daha fazla bilgi için hello makalesine bakın [oluşturma Service Bus kaynaklarını Azure Resource Manager şablonları kullanarak](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d854d-142">For information about using Azure Resource Manager templates, see hello article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>
- <span data-ttu-id="d854d-143">Hakkında bilgi [Service Bus .NET Yönetim kitaplıklarını](service-bus-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="d854d-143">Information about [Service Bus .NET management libraries](service-bus-management-libraries.md).</span></span>

<span data-ttu-id="d854d-144">Bazı alternatif yolu vardır toomanage Service Bus varlıklar, bu Web günlüğü postaları açıklandığı gibi:</span><span class="sxs-lookup"><span data-stu-id="d854d-144">There are some alternate ways toomanage Service Bus entities, as described in these blog posts:</span></span>

* [<span data-ttu-id="d854d-145">Nasıl toocreate Service Bus kuyrukları, konuları ve abonelikleri bir PowerShell Betiği kullanılarak</span><span class="sxs-lookup"><span data-stu-id="d854d-145">How toocreate Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="d854d-146">Nasıl toocreate Service Bus Namespace ve bir Event Hub'ın bir PowerShell komut dosyası kullanma</span><span class="sxs-lookup"><span data-stu-id="d854d-146">How toocreate a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [<span data-ttu-id="d854d-147">Hizmet veri yolu PowerShell betikleri</span><span class="sxs-lookup"><span data-stu-id="d854d-147">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
