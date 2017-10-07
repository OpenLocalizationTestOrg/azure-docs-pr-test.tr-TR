---
title: "Azure yönetilen yukarı yedekleme için Disk aaaCopy | Microsoft Docs"
description: "Azure yönetilen diski toouse geri yukarı veya sorun giderme disk için bir kopyasını toocreate nasıl sorunları hakkında bilgi edinin."
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: 41b91c2d68eb5be9c493a66be5f7d085a70450d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="8c650-103">Yönetilen bir Azure diski yönetilen anlık görüntülerini kullanarak tarafından depolanan VHD bir kopyasını oluşturun</span><span class="sxs-lookup"><span data-stu-id="8c650-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="8c650-104">Yönetilen disk yedekleme için bir anlık görüntüsünü veya yönetilen bir Disk hello anlık görüntüden oluşturmak ve tooa test sanal makinesi tootroubleshoot ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8c650-104">Take a snapshot of a Managed disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="8c650-105">Yönetilen bir anlık görüntü yönetilen bir VM Disk noktası zaman tam kopyasıdır.</span><span class="sxs-lookup"><span data-stu-id="8c650-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="8c650-106">Bu, VHD salt okunur bir kopyasını oluşturur ve isteğe bağlı olarak varsayılan olarak, standart yönetilen Disk olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="8c650-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> 

<span data-ttu-id="8c650-107">Fiyatlandırma hakkında daha fazla bilgi için bkz: [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="8c650-107">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> <!--Add link tootopic or blog post that explains managed disks. -->

<span data-ttu-id="8c650-108">Her iki hello Azure portal veya hello Azure CLI 2.0 tootake hello yönetilen Disk görüntüsünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="8c650-108">Use either hello Azure portal or hello Azure CLI 2.0 tootake a snapshot of hello Managed Disk.</span></span>

## <a name="use-azure-cli-20-tootake-a-snapshot"></a><span data-ttu-id="8c650-109">Azure CLI 2.0 tootake bir anlık görüntü kullanın</span><span class="sxs-lookup"><span data-stu-id="8c650-109">Use Azure CLI 2.0 tootake a snapshot</span></span>

> [!NOTE] 
> <span data-ttu-id="8c650-110">Merhaba aşağıdaki örnek hello Azure CLI 2.0 yüklü ve Azure hesabınızda oturum gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8c650-110">hello following example requires hello Azure CLI 2.0 installed and logged into your Azure account.</span></span>

<span data-ttu-id="8c650-111">Merhaba aşağıdaki adımları nasıl tooobtain Al yönetilen bir işletim sistemi görüntüsünü hello kullanarak disk ve Göster `az snapshot create` hello komutunu `--source-disk` parametresi.</span><span class="sxs-lookup"><span data-stu-id="8c650-111">hello following steps show how tooobtain and take a snapshot of a managed OS disk using hello `az snapshot create` command with hello `--source-disk` parameter.</span></span> <span data-ttu-id="8c650-112">Merhaba aşağıdaki örneği adlı bir VM olduğunu varsayar `myVM` hello olarak yönetilen bir işletim sistemi diski ile oluşturulan `myResourceGroup` kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="8c650-112">hello following example assumes that there is a VM called `myVM` created with a managed OS disk in hello `myResourceGroup` resource group.</span></span>

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

<span data-ttu-id="8c650-113">Merhaba çıktı gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="8c650-113">hello output should look something like:</span></span>

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="8c650-114">Azure portal tootake bir anlık görüntü kullanın</span><span class="sxs-lookup"><span data-stu-id="8c650-114">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="8c650-115">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8c650-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8c650-116">Merhaba sol üst köşede başlayarak, tıklatın **yeni** arayın ve **anlık görüntü**.</span><span class="sxs-lookup"><span data-stu-id="8c650-116">Starting in hello upper-left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="8c650-117">Başlangıç anlık görüntü dikey penceresinde tıklayın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="8c650-117">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="8c650-118">Girin bir **adı** hello anlık görüntü için.</span><span class="sxs-lookup"><span data-stu-id="8c650-118">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="8c650-119">Var olan seçin [kaynak grubu](../../azure-resource-manager/resource-group-overview.md#resource-groups) veya yeni bir hello adını yazın.</span><span class="sxs-lookup"><span data-stu-id="8c650-119">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="8c650-120">Azure veri merkezi konum seçin.</span><span class="sxs-lookup"><span data-stu-id="8c650-120">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="8c650-121">İçin **kaynak disk**, hello yönetilen Disk toosnapshot seçin.</span><span class="sxs-lookup"><span data-stu-id="8c650-121">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="8c650-122">Select hello **hesap türü** toouse toostore hello anlık görüntü.</span><span class="sxs-lookup"><span data-stu-id="8c650-122">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="8c650-123">Öneririz **Standard_LRS** yüksek performanslı bir diskte depolanan gerekmedikçe.</span><span class="sxs-lookup"><span data-stu-id="8c650-123">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="8c650-124">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c650-124">Click **Create**.</span></span>

<span data-ttu-id="8c650-125">Yönetilen bir Disk toouse hello anlık görüntü toocreate planlamak ve toobe yüksek performanslı gereken VM ekleme, hello parametresini kullanmanız `--sku Premium_LRS` hello ile `az snapshot create` komutu.</span><span class="sxs-lookup"><span data-stu-id="8c650-125">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `--sku Premium_LRS` with hello `az snapshot create` command.</span></span> <span data-ttu-id="8c650-126">Bu hello anlık görüntü oluşturur, böylece yönetilen bir Premium Disk depolanır.</span><span class="sxs-lookup"><span data-stu-id="8c650-126">This creates hello snapshot so that it is stored as a Premium Managed Disk.</span></span> <span data-ttu-id="8c650-127">Katı hal sürücüleri (SSD) olan ancak birden çok standart diskler (HDD'ler) maliyet premium yönetilen diskleri daha iyi gerçekleştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="8c650-127">Premium Managed Disks perform better because they are solid-state drives (SSDs), but cost more than Standard disks (HDDs).</span></span>


