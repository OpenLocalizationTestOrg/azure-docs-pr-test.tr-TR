---
title: "Azure Service Bus kaynaklarını yönetmek için PowerShell kullanma | Microsoft Docs"
description: "PowerShell modülü oluşturun ve Service Bus kaynaklarını yönetmek için kullanın"
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
ms.openlocfilehash: 1205f9fcabf5788c970fbce257aa5ad04f32cddc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-manage-service-bus-resources"></a><span data-ttu-id="851a2-103">Service Bus kaynaklarını yönetmek için PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="851a2-103">Use PowerShell to manage Service Bus resources</span></span>

<span data-ttu-id="851a2-104">Microsoft Azure PowerShell denetlemek ve dağıtımını ve Azure Hizmetleri yönetimini otomatikleştirmek için kullanabileceğiniz bir komut dosyası ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="851a2-104">Microsoft Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of Azure services.</span></span> <span data-ttu-id="851a2-105">Bu makalede nasıl kullanılacağını açıklar [Service Bus Resource Manager PowerShell Modülü](/powershell/module/azurerm.servicebus) sağlamak ve hizmet veri yolu varlıklarını (ad alanları, kuyruklar, konular ve abonelikler) yönetmek için yerel Azure PowerShell konsolunda veya komut dosyası kullanarak.</span><span class="sxs-lookup"><span data-stu-id="851a2-105">This article describes how to use the [Service Bus Resource Manager PowerShell module](/powershell/module/azurerm.servicebus) to provision and manage Service Bus entities (namespaces, queues, topics, and subscriptions) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="851a2-106">Hizmet veri yolu varlıklarını Azure Resource Manager şablonları kullanarak da yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="851a2-106">You can also manage Service Bus entities using Azure Resource Manager templates.</span></span> <span data-ttu-id="851a2-107">Daha fazla bilgi için bkz: [oluşturma Service Bus kaynaklarını Azure Resource Manager şablonları kullanarak](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="851a2-107">For more information, see the article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="851a2-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="851a2-108">Prerequisites</span></span>

<span data-ttu-id="851a2-109">Başlamadan önce aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="851a2-109">Before you begin, you'll need the following:</span></span>

* <span data-ttu-id="851a2-110">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="851a2-110">An Azure subscription.</span></span> <span data-ttu-id="851a2-111">Bir aboneliği edinme hakkında daha fazla bilgi için bkz: [satın alma seçeneği][purchase options], [üye teklifleri][member offers], veya [boş Hesap][free account].</span><span class="sxs-lookup"><span data-stu-id="851a2-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="851a2-112">Azure PowerShell ile bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="851a2-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="851a2-113">Yönergeler için bkz: [Azure PowerShell cmdlet'leri kullanmaya başlama](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="851a2-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="851a2-114">PowerShell komut dosyaları, NuGet paketlerini ve .NET Framework genel anlama.</span><span class="sxs-lookup"><span data-stu-id="851a2-114">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="851a2-115">başlarken</span><span class="sxs-lookup"><span data-stu-id="851a2-115">Get started</span></span>

<span data-ttu-id="851a2-116">İlk adım, Azure hesabınızı ve Azure abonelik oturum açmak için PowerShell kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="851a2-116">The first step is to use PowerShell to log in to your Azure account and Azure subscription.</span></span> <span data-ttu-id="851a2-117">' Ndaki yönergeleri izleyin [Azure PowerShell cmdlet'leri kullanmaya başlama](/powershell/azure/get-started-azureps) Azure hesabınızda oturum açın ve almak ve Azure aboneliğinizde kaynaklara erişmek için.</span><span class="sxs-lookup"><span data-stu-id="851a2-117">Follow the instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) to log in to your Azure account, and retrieve and access the resources in your Azure subscription.</span></span>

## <a name="provision-a-service-bus-namespace"></a><span data-ttu-id="851a2-118">Bir hizmet veri yolu ad alanı sağlama</span><span class="sxs-lookup"><span data-stu-id="851a2-118">Provision a Service Bus namespace</span></span>

<span data-ttu-id="851a2-119">Hizmet veri yolu ad alanları ile çalışırken, kullanabileceğiniz [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [yeni AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), ve [kümesi AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlet'leri.</span><span class="sxs-lookup"><span data-stu-id="851a2-119">When working with Service Bus namespaces, you can use the [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), and [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span></span>

<span data-ttu-id="851a2-120">Bu örnek komut dosyasında birkaç yerel değişkenler oluşturur; `$Namespace` ve `$Location`.</span><span class="sxs-lookup"><span data-stu-id="851a2-120">This example creates a few local variables in the script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="851a2-121">`$Namespace`Biz birlikte çalışmak istediğiniz hizmet veri yolu ad alanı adıdır.</span><span class="sxs-lookup"><span data-stu-id="851a2-121">`$Namespace` is the name of the Service Bus namespace with which we want to work.</span></span>
* <span data-ttu-id="851a2-122">`$Location`hangi veri merkezinde tanımlayan ad sağlamak.</span><span class="sxs-lookup"><span data-stu-id="851a2-122">`$Location` identifies the data center in which will we provision the namespace.</span></span>
* <span data-ttu-id="851a2-123">`$CurrentNamespace`Biz alınamıyor (veya oluşturma) başvuru ad alanını depolar.</span><span class="sxs-lookup"><span data-stu-id="851a2-123">`$CurrentNamespace` stores the reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="851a2-124">Gerçek bir betik içinde `$Namespace` ve `$Location` parametre olarak geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="851a2-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="851a2-125">Bu komut dosyasının parçası şunları yapar:</span><span class="sxs-lookup"><span data-stu-id="851a2-125">This part of the script does the following:</span></span>

1. <span data-ttu-id="851a2-126">Belirtilen ada sahip bir hizmet veri yolu ad alanı almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="851a2-126">Attempts to retrieve a Service Bus namespace with the specified name.</span></span>
2. <span data-ttu-id="851a2-127">Ad alanı bulunursa, bulunanları bildirir.</span><span class="sxs-lookup"><span data-stu-id="851a2-127">If the namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="851a2-128">Ad alanı bulunmazsa, ad alanı oluşturur ve yeni oluşturulan ad alanı alır.</span><span class="sxs-lookup"><span data-stu-id="851a2-128">If the namespace is not found, it creates the namespace and then retrieves the newly created namespace.</span></span>
   
    ``` powershell
    # Query to see if the namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if the namespace already exists or needs to be created
    if ($CurrentNamespace)
    {
        Write-Host "The namespace $Namespace already exists in the $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "The $Namespace namespace does not exist."
        Write-Host "Creating the $Namespace namespace in the $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "The $Namespace namespace in Resource Group $ResGrpName in the $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a><span data-ttu-id="851a2-129">Ad alanı yetkilendirme kuralı oluştur</span><span class="sxs-lookup"><span data-stu-id="851a2-129">Create a namespace authorization rule</span></span>

<span data-ttu-id="851a2-130">Aşağıdaki örnek ad alanı yetkilendirme kurallarını kullanarak yönetmek nasıl gösterir [yeni AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Kümesi AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), ve [Kaldır AzureRmServiceBusNamespaceAuthorizationRule cmdlet'leri](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span><span class="sxs-lookup"><span data-stu-id="851a2-130">The following example shows how to manage namespace authorization rules using the [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), and [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span></span>

```powershell
# Query to see if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if the rule already exists or needs to be created
if ($CurrentRule)
{
    Write-Host "The $AuthRule rule already exists for the namespace $Namespace."
}
else
{
    Write-Host "The $AuthRule rule does not exist."
    Write-Host "Creating the $AuthRule rule for the $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "The $AuthRule rule for the $Namespace namespace has been successfully created."

    Write-Host "Setting rights on the namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights to the namespace"
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

## <a name="create-a-queue"></a><span data-ttu-id="851a2-131">Bir kuyruk oluşturma</span><span class="sxs-lookup"><span data-stu-id="851a2-131">Create a queue</span></span>

<span data-ttu-id="851a2-132">Bir kuyruk veya konu oluşturmak için önceki bölümde komut dosyası kullanarak bir ad alanı denetimi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="851a2-132">To create a queue or topic, perform a namespace check using the script in the previous section.</span></span> <span data-ttu-id="851a2-133">Ardından, sıranın oluşturun:</span><span class="sxs-lookup"><span data-stu-id="851a2-133">Then, create the queue:</span></span>

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "The queue $QueueName already exists in the $Location region:"
}
else
{
    Write-Host "The $QueueName queue does not exist."
    Write-Host "Creating the $QueueName queue in the $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "The $QueueName queue in Resource Group $ResGrpName in the $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a><span data-ttu-id="851a2-134">Sıra özelliklerini değiştir</span><span class="sxs-lookup"><span data-stu-id="851a2-134">Modify queue properties</span></span>

<span data-ttu-id="851a2-135">Kullanabileceğiniz önceki bölümde komut dosyası yürütme sonrasında [kümesi AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet'i aşağıdaki örnekteki gibi bir sıranın özelliklerini güncelleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="851a2-135">After executing the script in the preceding section, you can use the [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet to update the properties of a queue, as in the following example:</span></span>

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a><span data-ttu-id="851a2-136">Diğer hizmet veri yolu varlıklarını sağlama</span><span class="sxs-lookup"><span data-stu-id="851a2-136">Provisioning other Service Bus entities</span></span>

<span data-ttu-id="851a2-137">Kullanabileceğiniz [Service Bus PowerShell modülünü](/powershell/module/azurerm.servicebus) konu başlıkları ve abonelikler gibi diğer varlıklar sağlayacak.</span><span class="sxs-lookup"><span data-stu-id="851a2-137">You can use the [Service Bus PowerShell module](/powershell/module/azurerm.servicebus) to provision other entities, such as topics and subscriptions.</span></span> <span data-ttu-id="851a2-138">Bu cmdlet, önceki bölümde gösterilen kuyruk oluşturma cmdlet'leri sözdizimsel olarak benzerdir.</span><span class="sxs-lookup"><span data-stu-id="851a2-138">These cmdlets are syntactically similar to the queue creation cmdlets demonstrated in the previous section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="851a2-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="851a2-139">Next steps</span></span>

- <span data-ttu-id="851a2-140">Tam Service Bus Resource Manager PowerShell modülü belgelerine bakın [burada](/powershell/module/azurerm.servicebus).</span><span class="sxs-lookup"><span data-stu-id="851a2-140">See the complete Service Bus Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.servicebus).</span></span> <span data-ttu-id="851a2-141">Bu sayfa, tüm kullanılabilir cmdlet'leri listeler.</span><span class="sxs-lookup"><span data-stu-id="851a2-141">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="851a2-142">Azure Resource Manager şablonları kullanma hakkında daha fazla bilgi için bkz: [oluşturma Service Bus kaynaklarını Azure Resource Manager şablonları kullanarak](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="851a2-142">For information about using Azure Resource Manager templates, see the article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>
- <span data-ttu-id="851a2-143">Hakkında bilgi [Service Bus .NET Yönetim kitaplıklarını](service-bus-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="851a2-143">Information about [Service Bus .NET management libraries](service-bus-management-libraries.md).</span></span>

<span data-ttu-id="851a2-144">Bu Web günlüğü postaları açıklandığı gibi hizmet veri yolu varlıklarını yönetmek için bazı alternatif yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="851a2-144">There are some alternate ways to manage Service Bus entities, as described in these blog posts:</span></span>

* [<span data-ttu-id="851a2-145">Service Bus kuyrukları, konuları ve abonelikleri bir PowerShell Betiği kullanılarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="851a2-145">How to create Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="851a2-146">Hizmet veri yolu Namespace ve bir PowerShell komut dosyası kullanarak bir Event Hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="851a2-146">How to create a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [<span data-ttu-id="851a2-147">Hizmet veri yolu PowerShell betikleri</span><span class="sxs-lookup"><span data-stu-id="851a2-147">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
