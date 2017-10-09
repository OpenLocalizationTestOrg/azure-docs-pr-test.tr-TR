---
title: aaaMove Azure Windows VM kaynak | Microsoft Docs
description: "Bir Windows VM tooanother Azure abonelik veya kaynak grubu hello Resource Manager dağıtım modelinde taşıyın."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 859e78dce9acf1168780d4ee8e9f6dac0e3c11cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-tooanother-azure-subscription-or-resource-group"></a><span data-ttu-id="5cc8c-103">Bir Windows VM tooanother Azure abonelik veya kaynak grubu taşıma</span><span class="sxs-lookup"><span data-stu-id="5cc8c-103">Move a Windows VM tooanother Azure subscription or resource group</span></span>
<span data-ttu-id="5cc8c-104">Bu makalede nasıl anlatılmaktadır toomove bir Windows VM kaynak grupları veya abonelikler arasında.</span><span class="sxs-lookup"><span data-stu-id="5cc8c-104">This article walks you through how toomove a Windows VM between resource groups or subscriptions.</span></span> <span data-ttu-id="5cc8c-105">Abonelikler arasında taşıma kişisel bir abonelikte ilk olarak bir VM oluşturduysanız, kullanışlı ve şimdi toomove istiyorsanız bunu tooyour şirketin abonelik toocontinue çalışmanızı.</span><span class="sxs-lookup"><span data-stu-id="5cc8c-105">Moving between subscriptions can be handy if you originally created a VM in a personal subscription and now want toomove it tooyour company's subscription toocontinue your work.</span></span>

> [!IMPORTANT]
><span data-ttu-id="5cc8c-106">Şu anda yönetilen diskleri taşınamıyor.</span><span class="sxs-lookup"><span data-stu-id="5cc8c-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="5cc8c-107">Yeni kaynak kimlikleri hello taşıma bir parçası olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5cc8c-107">New resource IDs are created as part of hello move.</span></span> <span data-ttu-id="5cc8c-108">Merhaba VM taşındıktan sonra Araçlar ve komut dosyaları toouse hello yeni kaynak kimlikleri tooupdate gerekir.</span><span class="sxs-lookup"><span data-stu-id="5cc8c-108">Once hello VM has been moved, you need tooupdate your tools and scripts toouse hello new resource IDs.</span></span> 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-toomove-a-vm"></a><span data-ttu-id="5cc8c-109">PowerShell toomove VM kullanın</span><span class="sxs-lookup"><span data-stu-id="5cc8c-109">Use Powershell toomove a VM</span></span>
<span data-ttu-id="5cc8c-110">bir sanal makine tooanother kaynak grubu toomove, toomake, ayrıca tüm hello bağımlı kaynakları taşıdığınızdan emin gerekir.</span><span class="sxs-lookup"><span data-stu-id="5cc8c-110">toomove a virtual machine tooanother resource group, you need toomake sure that you also move all of hello dependent resources.</span></span> <span data-ttu-id="5cc8c-111">toouse hello taşıma AzureRMResource cmdlet hello kaynak adı ve kaynak hello türü gerekir.</span><span class="sxs-lookup"><span data-stu-id="5cc8c-111">toouse hello Move-AzureRMResource cmdlet, you need hello resource name and hello type of resource.</span></span> <span data-ttu-id="5cc8c-112">Merhaba Bul AzureRMResource cmdlet'i her ikisini de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5cc8c-112">You can get both from hello Find-AzureRMResource cmdlet.</span></span>

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


<span data-ttu-id="5cc8c-113">birden fazla kaynak toomove ihtiyacımız VM toomove.</span><span class="sxs-lookup"><span data-stu-id="5cc8c-113">toomove a VM we need toomove multiple resources.</span></span> <span data-ttu-id="5cc8c-114">Yalnızca her kaynak için ayrı değişkeni oluşturun ve bunları listeleyin.</span><span class="sxs-lookup"><span data-stu-id="5cc8c-114">We can just create separate variables for each resource and then list them.</span></span> <span data-ttu-id="5cc8c-115">Bu örnek, bir VM için hello temel kaynakların çoğunu içerir, ancak gerektiğinde daha fazla ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5cc8c-115">This example includes most of hello basic resources for a VM, but you can add more as needed.</span></span>

    $sourceRG = "<sourceResourceGroupName>"
    $destinationRG = "<destinationResourceGroupName>"

    $vm = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Compute/virtualMachines" -ResourceName "<vmName>"
    $storageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<storageAccountName>"
    $diagStorageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<diagnosticStorageAccountName>"
    $vNet = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/virtualNetworks" -ResourceName "<vNetName>"
    $nic = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkInterfaces" -ResourceName "<nicName>"
    $ip = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/publicIPAddresses" -ResourceName "<ipName>"
    $nsg = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkSecurityGroups" -ResourceName "<nsgName>"

    Move-AzureRmResource -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId

<span data-ttu-id="5cc8c-116">toomove Merhaba kaynakları toodifferent abonelik, hello dahil **- DestinationSubscriptionId** parametresi.</span><span class="sxs-lookup"><span data-stu-id="5cc8c-116">toomove hello resources toodifferent subscription, include hello **-DestinationSubscriptionId** parameter.</span></span> 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



<span data-ttu-id="5cc8c-117">Sizden istenir toomove hello istediğiniz tooconfirm belirtilen kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="5cc8c-117">You will be asked tooconfirm that you want toomove hello specified resources.</span></span> <span data-ttu-id="5cc8c-118">Tür **Y** tooconfirm toomove hello kaynakları istiyor.</span><span class="sxs-lookup"><span data-stu-id="5cc8c-118">Type **Y** tooconfirm that you want toomove hello resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cc8c-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5cc8c-119">Next steps</span></span>
<span data-ttu-id="5cc8c-120">Birçok farklı türdeki kaynakların kaynak grupları ve abonelikler arasında taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5cc8c-120">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="5cc8c-121">Daha fazla bilgi için bkz: [kaynakları toonew kaynak grubuna veya aboneliğe taşıma](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="5cc8c-121">For more information, see [Move resources toonew resource group or subscription](../../resource-group-move-resources.md).</span></span>    

