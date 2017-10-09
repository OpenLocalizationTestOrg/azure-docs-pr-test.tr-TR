---
title: aaaMove azure'da bir Linux VM | Microsoft Docs
description: "Bir Linux VM tooanother Azure abonelik veya kaynak grubu hello Resource Manager dağıtım modelinde taşıyın."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d635f0a5-4458-4b95-a5f8-eed4f41eb4d4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 938d04234059111912f03e72d14dabd338bc0678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-linux-vm-tooanother-subscription-or-resource-group"></a><span data-ttu-id="ff3fd-103">Bir Linux VM tooanother abonelik veya kaynak grubu taşıma</span><span class="sxs-lookup"><span data-stu-id="ff3fd-103">Move a Linux VM tooanother subscription or resource group</span></span>
<span data-ttu-id="ff3fd-104">Bu makalede nasıl anlatılmaktadır toomove bir Linux VM kaynak grupları veya abonelikler arasında.</span><span class="sxs-lookup"><span data-stu-id="ff3fd-104">This article walks you through how toomove a Linux VM between resource groups or subscriptions.</span></span> <span data-ttu-id="ff3fd-105">Bir VM abonelikler arasında taşıma kişisel bir abonelikte VM oluşturduysanız elinizin altında kullanılabilir ve şimdi toomove istediğiniz onu tooyour şirketin abonelik.</span><span class="sxs-lookup"><span data-stu-id="ff3fd-105">Moving a VM between subscriptions can be handy if you created a VM in a personal subscription and now want toomove it tooyour company's subscription.</span></span>

> [!IMPORTANT]
><span data-ttu-id="ff3fd-106">Şu anda yönetilen diskleri taşınamıyor.</span><span class="sxs-lookup"><span data-stu-id="ff3fd-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="ff3fd-107">Yeni kaynak kimlikleri hello taşıma bir parçası olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ff3fd-107">New resource IDs are created as part of hello move.</span></span> <span data-ttu-id="ff3fd-108">Merhaba VM taşındıktan sonra Araçlar ve komut dosyaları toouse hello yeni kaynak kimlikleri tooupdate gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff3fd-108">Once hello VM has been moved, you need tooupdate your tools and scripts toouse hello new resource IDs.</span></span> 
> 
> 

## <a name="use-hello-azure-cli-toomove-a-vm"></a><span data-ttu-id="ff3fd-109">Hello Azure CLI toomove VM kullanın</span><span class="sxs-lookup"><span data-stu-id="ff3fd-109">Use hello Azure CLI toomove a VM</span></span>
<span data-ttu-id="ff3fd-110">toosuccessfully VM taşımak, toomove hello VM ve tüm destekleyici kaynakları gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff3fd-110">toosuccessfully move a VM, you need toomove hello VM and all its supporting resources.</span></span> <span data-ttu-id="ff3fd-111">Kullanım hello **azure Grup Göster** toolist tüm hello kaynaklar bir kaynak grubu ve kimlikleri komutu.</span><span class="sxs-lookup"><span data-stu-id="ff3fd-111">Use hello **azure group show** command toolist all hello resources in a resource group and their IDs.</span></span> <span data-ttu-id="ff3fd-112">Böylece kopyalayıp hello kimlikleri Yapıştır sonraki komutları toopipe hello bu komut tooa dosyasını çıkışını yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ff3fd-112">It helps toopipe hello output of this command tooa file so you can copy and paste hello IDs into later commands.</span></span>

    azure group show <resourceGroupName>

<span data-ttu-id="ff3fd-113">toomove VM ve kendi kaynakları tooanother kaynak grubu kullanmak hello **azure kaynak taşıma** CLI komutu.</span><span class="sxs-lookup"><span data-stu-id="ff3fd-113">toomove a VM and its resources tooanother resource group, use hello **azure resource move** CLI command.</span></span> <span data-ttu-id="ff3fd-114">Aşağıdaki örneğine hello nasıl toomove VM ve hello en yaygın kaynakları gerektirdiği gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff3fd-114">hello following example shows how toomove a VM and hello most common resources it requires.</span></span> <span data-ttu-id="ff3fd-115">Merhaba kullanırız **-i** parametre ve bir virgülle ayrılmış listesi (boşluksuz) kimlikleri için hello kaynakları toomove geçirin.</span><span class="sxs-lookup"><span data-stu-id="ff3fd-115">We use hello **-i** parameter and pass in a comma-separated list (without spaces) of IDs for hello resources toomove.</span></span>

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

<span data-ttu-id="ff3fd-116">Toomove istiyorsanız, VM ve kaynakları tooa farklı aboneliğini Merhaba, hello eklemek **--hedef-Subscriptionıd &#60; destinationSubscriptionID &#62;** parametresi toospecify hello hedef abonelik.</span><span class="sxs-lookup"><span data-stu-id="ff3fd-116">If you want toomove hello VM and its resources tooa different subscription, add hello **--destination-subscriptionId &#60;destinationSubscriptionID&#62;** parameter toospecify hello destination subscription.</span></span>

<span data-ttu-id="ff3fd-117">Bir Windows bilgisayarda bir komut istemi hello çalışıyorsanız, tooadd gereken bir  **$**  bunları bildirirken değişken adları Merhaba öne.</span><span class="sxs-lookup"><span data-stu-id="ff3fd-117">If you are working from hello Command Prompt on a Windows computer, you need tooadd a **$** in front of hello variable names when you declare them.</span></span> <span data-ttu-id="ff3fd-118">Bu Linux gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="ff3fd-118">This isn't needed in Linux.</span></span>

<span data-ttu-id="ff3fd-119">Bunu Sorduğunuza toomove hello istediğiniz tooconfirm belirtilen kaynak.</span><span class="sxs-lookup"><span data-stu-id="ff3fd-119">You are asked tooconfirm that you want toomove hello specified resource.</span></span> <span data-ttu-id="ff3fd-120">Tür **Y** tooconfirm toomove hello kaynakları istiyor.</span><span class="sxs-lookup"><span data-stu-id="ff3fd-120">Type **Y** tooconfirm that you want toomove hello resources.</span></span>

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="ff3fd-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ff3fd-121">Next steps</span></span>
<span data-ttu-id="ff3fd-122">Birçok farklı türdeki kaynakların kaynak grupları ve abonelikler arasında taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff3fd-122">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="ff3fd-123">Daha fazla bilgi için bkz: [kaynakları toonew kaynak grubuna veya aboneliğe taşıma](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="ff3fd-123">For more information, see [Move resources toonew resource group or subscription](../../resource-group-move-resources.md).</span></span>    

