---
title: "aaaUsing yönetilen diskler ile Azure sanal makine ölçek kümeleri | Microsoft Docs"
description: "Neden ve nasıl toouse diskler sanal makine ölçek kümesi ile yönetilen öğrenin"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/01/2017
ms.author: negat
ms.openlocfilehash: 0e2a21e9f8b114ae1c8b81e1e6124621366f5643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a><span data-ttu-id="5a05e-103">Azure VM ölçek kümeleri ve yönetilen diskler</span><span class="sxs-lookup"><span data-stu-id="5a05e-103">Azure VM scale sets and managed disks</span></span>

<span data-ttu-id="5a05e-104">Azure [sanal makine ölçek kümeleri](/azure/virtual-machine-scale-sets/), yönetilen disklere sahip sanal makineleri destekler.</span><span class="sxs-lookup"><span data-stu-id="5a05e-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) supports virtual machines with managed disks.</span></span> <span data-ttu-id="5a05e-105">Ölçek kümeleri ile birlikte yönetilen disklerin kullanılması aşağıdakiler gibi birçok avantaj sunar:</span><span class="sxs-lookup"><span data-stu-id="5a05e-105">Using managed disks with scale sets has several benefits, including:</span></span>

* <span data-ttu-id="5a05e-106">Toopre artık ihtiyaç duymadığınız-oluşturun ve VM'ler hello ölçek kümesi için depolama hesapları toostore hello OS diskleri yönetme.</span><span class="sxs-lookup"><span data-stu-id="5a05e-106">You no longer need toopre-create and manage storage accounts toostore hello OS disks for hello scale set VMs.</span></span>

* <span data-ttu-id="5a05e-107">Yönetilen veri diskleri toohello ölçek kümesi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a05e-107">You can attach managed data disks toohello scale set.</span></span>

* <span data-ttu-id="5a05e-108">Yönetilen diskler sayesinde ölçek kümesinin kapasitesi, platform görüntüsü tabanlıysa 1.000 VM'e veya özel bir görüntü tabanlıysa 100 VM'e kadar çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="5a05e-108">With managed disk, a scale set can have capacity as high as 1,000 VMs if based on a platform image or 100 VMs if based on a custom image.</span></span>

## <a name="get-started"></a><span data-ttu-id="5a05e-109">başlarken</span><span class="sxs-lookup"><span data-stu-id="5a05e-109">Get started</span></span>

<span data-ttu-id="5a05e-110">Basit bir yol yönetilen disk ölçek kümeleri ile başlatılan tooget hello Azure Portalı'ndan toodeploy değil.</span><span class="sxs-lookup"><span data-stu-id="5a05e-110">A simple way tooget started with managed disk scale sets is toodeploy one from hello Azure portal.</span></span> <span data-ttu-id="5a05e-111">Daha fazla bilgi için [bu makaleye](./virtual-machine-scale-sets-portal-create.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="5a05e-111">For more information, see [this article](./virtual-machine-scale-sets-portal-create.md).</span></span> <span data-ttu-id="5a05e-112">Başka bir basit yol başlatılan tooget olan toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy bir ölçek kümesi.</span><span class="sxs-lookup"><span data-stu-id="5a05e-112">Another simple way tooget started is toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy a scale set.</span></span> <span data-ttu-id="5a05e-113">Merhaba aşağıdaki örnekte nasıl toocreate bir Ubuntu ölçeği her bir 50 GB ve 100 GB veri diski 10 VM'ler ile Ayarla dayalı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="5a05e-113">hello following example shows how toocreate an Ubuntu based scale set with 10 VMs, each with a 50-GB and 100-GB data disk:</span></span>

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

<span data-ttu-id="5a05e-114">Alternatif olarak, hello görünebilir [Azure hızlı başlangıç şablonlarını GitHub deposuna](https://github.com/Azure/azure-quickstart-templates) içeren klasörleri için `vmss` toosee ölçek kümeleri dağıtmak şablonları örnekleri önceden oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="5a05e-114">Alternatively, you could look in hello [Azure Quickstart Templates GitHub repo](https://github.com/Azure/azure-quickstart-templates) for folders that contain `vmss` toosee pre-built examples of templates that deploy scale sets.</span></span> <span data-ttu-id="5a05e-115">Hangi şablonları zaten yönetilen diskleri kullanarak tootell başvurabilirsiniz çok[bu listeyi](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span><span class="sxs-lookup"><span data-stu-id="5a05e-115">tootell which templates are already using managed disks, you can refer too[this list](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a05e-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5a05e-116">Next steps</span></span>

<span data-ttu-id="5a05e-117">Yönetilen diskler hakkında daha fazla genel bilgi edinmek için [bu makaleye](../virtual-machines/windows/managed-disks-overview.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="5a05e-117">For more information on managed disks in general, see [this article](../virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="5a05e-118">diskler, Resource Manager şablonu tooprovision ölçek ayarlar ile tooconvert yönetilen nasıl toosee bkz [bu makalede](./virtual-machine-scale-sets-convert-template-to-md.md).</span><span class="sxs-lookup"><span data-stu-id="5a05e-118">toosee how tooconvert a Resource Manager template tooprovision scale sets with managed disks, see [this article](./virtual-machine-scale-sets-convert-template-to-md.md).</span></span> <span data-ttu-id="5a05e-119">Merhaba aynı değişiklikleri toohello Resource Manager şablonları toohello Azure REST API de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="5a05e-119">hello same modifications toohello Resource Manager templates apply toohello Azure REST API as well.</span></span>

<span data-ttu-id="5a05e-120">yönetilen veri diskleri ölçek kümeleri ile kullanma hakkında daha fazla toolearn bkz [bu makalede](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="5a05e-120">toolearn more about using managed data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="5a05e-121">büyük ölçekli kümeleriyle çalışmak toobegin başvurmak çok[bu makalede](./virtual-machine-scale-sets-placement-groups.md).</span><span class="sxs-lookup"><span data-stu-id="5a05e-121">toobegin working with large scale sets, refer too[this article](./virtual-machine-scale-sets-placement-groups.md).</span></span>


