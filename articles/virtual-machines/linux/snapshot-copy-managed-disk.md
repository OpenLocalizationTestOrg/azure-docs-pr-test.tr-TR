---
title: "Yönetilen bir Azure diski geri için yukarı kopyalama | Microsoft Docs"
description: "Yedekleme için kullanılacak bir Azure yönetilen Disk veya disk sorunlarını giderme bir kopyasını oluşturmayı öğrenin."
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
ms.openlocfilehash: c91367ef11c9d531bebac7c069d2df586607ec29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="f8870-103">Yönetilen bir Azure diski yönetilen anlık görüntülerini kullanarak tarafından depolanan VHD bir kopyasını oluşturun</span><span class="sxs-lookup"><span data-stu-id="f8870-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="f8870-104">Yönetilen disk yedekleme için bir anlık görüntüsünü veya yönetilen bir Disk anlık görüntüden oluşturabilir ve sorun giderme için test sanal makineye Ekle.</span><span class="sxs-lookup"><span data-stu-id="f8870-104">Take a snapshot of a Managed disk for backup or create a Managed Disk from the snapshot and attach it to a test virtual machine to troubleshoot.</span></span> <span data-ttu-id="f8870-105">Yönetilen bir anlık görüntü yönetilen bir VM Disk noktası zaman tam kopyasıdır.</span><span class="sxs-lookup"><span data-stu-id="f8870-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="f8870-106">Bu, VHD salt okunur bir kopyasını oluşturur ve isteğe bağlı olarak varsayılan olarak, standart yönetilen Disk olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="f8870-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> 

<span data-ttu-id="f8870-107">Fiyatlandırma hakkında daha fazla bilgi için bkz: [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="f8870-107">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> <!--Add link to topic or blog post that explains managed disks. -->

<span data-ttu-id="f8870-108">Azure portalında veya Azure CLI 2.0 yönetilen diskin anlık görüntüsünü almak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8870-108">Use either the Azure portal or the Azure CLI 2.0 to take a snapshot of the Managed Disk.</span></span>

## <a name="use-azure-cli-20-to-take-a-snapshot"></a><span data-ttu-id="f8870-109">Bir anlık görüntü almak için Azure CLI 2.0 kullanın</span><span class="sxs-lookup"><span data-stu-id="f8870-109">Use Azure CLI 2.0 to take a snapshot</span></span>

> [!NOTE] 
> <span data-ttu-id="f8870-110">Aşağıdaki örnek, Azure CLI yüklenmiş ve Azure hesabınızda oturum 2.0 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f8870-110">The following example requires the Azure CLI 2.0 installed and logged into your Azure account.</span></span>

<span data-ttu-id="f8870-111">Aşağıdaki adımlar nasıl elde edilir ve yönetilen bir işletim sistemi diski kullanarak, bir anlık görüntüsünü gösterir `az snapshot create` komutunu `--source-disk` parametresi.</span><span class="sxs-lookup"><span data-stu-id="f8870-111">The following steps show how to obtain and take a snapshot of a managed OS disk using the `az snapshot create` command with the `--source-disk` parameter.</span></span> <span data-ttu-id="f8870-112">Aşağıdaki örnek olarak adlandırılan bir VM olduğunu varsayar `myVM` bir yönetilen işletim sistemi diski ile oluşturulan `myResourceGroup` kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="f8870-112">The following example assumes that there is a VM called `myVM` created with a managed OS disk in the `myResourceGroup` resource group.</span></span>

```azure-cli
# take the disk id with which to create a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

<span data-ttu-id="f8870-113">Çıktı aşağıdakine benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="f8870-113">The output should look something like:</span></span>

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

## <a name="use-azure-portal-to-take-a-snapshot"></a><span data-ttu-id="f8870-114">Bir anlık görüntüsünü için Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="f8870-114">Use Azure portal to take a snapshot</span></span> 

1. <span data-ttu-id="f8870-115">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f8870-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f8870-116">Sol üst köşede başlayarak, tıklatın **yeni** arayın ve **anlık görüntü**.</span><span class="sxs-lookup"><span data-stu-id="f8870-116">Starting in the upper-left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="f8870-117">Anlık görüntü dikey penceresinde tıklayın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="f8870-117">In the Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="f8870-118">Girin bir **adı** anlık görüntü için.</span><span class="sxs-lookup"><span data-stu-id="f8870-118">Enter a **Name** for the snapshot.</span></span>
5. <span data-ttu-id="f8870-119">Varolan [Kaynak grubunu](../../azure-resource-manager/resource-group-overview.md#resource-groups) seçin veya yenisi için adı yazın.</span><span class="sxs-lookup"><span data-stu-id="f8870-119">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span> 
6. <span data-ttu-id="f8870-120">Azure veri merkezi konum seçin.</span><span class="sxs-lookup"><span data-stu-id="f8870-120">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="f8870-121">İçin **kaynak disk**, anlık görüntü için yönetilen diski seçin.</span><span class="sxs-lookup"><span data-stu-id="f8870-121">For **Source disk**, select the Managed Disk to snapshot.</span></span>
8. <span data-ttu-id="f8870-122">Seçin **hesap türü** anlık görüntü deposu için kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="f8870-122">Select the **Account type** to use to store the snapshot.</span></span> <span data-ttu-id="f8870-123">Öneririz **Standard_LRS** yüksek performanslı bir diskte depolanan gerekmedikçe.</span><span class="sxs-lookup"><span data-stu-id="f8870-123">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="f8870-124">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f8870-124">Click **Create**.</span></span>

<span data-ttu-id="f8870-125">Yönetilen bir Disk oluşturmak ve yüksek performanslı olması gereken bir VM eklemek için anlık görüntü kullanmayı planlıyorsanız, parametresini kullanın `--sku Premium_LRS` ile `az snapshot create` komutu.</span><span class="sxs-lookup"><span data-stu-id="f8870-125">If you plan to use the snapshot to create a Managed Disk and attach it a VM that needs to be high performing, use the parameter `--sku Premium_LRS` with the `az snapshot create` command.</span></span> <span data-ttu-id="f8870-126">Bu anlık görüntü oluşturur, böylece yönetilen bir Premium Disk depolanır.</span><span class="sxs-lookup"><span data-stu-id="f8870-126">This creates the snapshot so that it is stored as a Premium Managed Disk.</span></span> <span data-ttu-id="f8870-127">Katı hal sürücüleri (SSD) olan ancak birden çok standart diskler (HDD'ler) maliyet premium yönetilen diskleri daha iyi gerçekleştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="f8870-127">Premium Managed Disks perform better because they are solid-state drives (SSDs), but cost more than Standard disks (HDDs).</span></span>


