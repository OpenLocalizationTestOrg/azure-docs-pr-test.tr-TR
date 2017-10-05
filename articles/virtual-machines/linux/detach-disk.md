---
title: "Bir Linux VM - Azure bir veri diski kullanımdan çıkarın | Microsoft Docs"
description: "Bir veri diskini CLI 2.0 ya da Azure portal kullanarak azure'da bir sanal makineden öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: azurecli
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 3f29547e1da6028b1e4b91d9e29fd3bcdfe08d50
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-detach-a-data-disk-from-a-linux-virtual-machine"></a><span data-ttu-id="939bd-103">Nasıl bir Linux sanal makine veri diski kullanımdan çıkarın</span><span class="sxs-lookup"><span data-stu-id="939bd-103">How to detach a data disk from a Linux virtual machine</span></span>

<span data-ttu-id="939bd-104">Sanal makineye bağlı bir veri diskine ihtiyacınız olmadığında bunu kolayca ayırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="939bd-104">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="939bd-105">Bu diski sanal makineden kaldırır, ancak depolama biriminden kaldırmaz.</span><span class="sxs-lookup"><span data-stu-id="939bd-105">This removes the disk from the virtual machine, but doesn't remove it from storage.</span></span> 

> [!WARNING]
> <span data-ttu-id="939bd-106">Bir disk ayırırsanız otomatik olarak silinmez.</span><span class="sxs-lookup"><span data-stu-id="939bd-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="939bd-107">Premium depolama alanına aboneliğiniz varsa, disk depolama ücretleri uygulanmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="939bd-107">If you have subscribed to Premium storage, you will continue to incur storage charges for the disk.</span></span> <span data-ttu-id="939bd-108">Daha fazla bilgi için bkz [fiyatlandırma ve faturalama Premium depolama kullanırken](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="939bd-108">For more information refer to [Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span> 
> 
> 

<span data-ttu-id="939bd-109">Disk üzerinde var olan verileri yeniden kullanmak isterseniz bu verileri aynı sanal makineye veya başka birine yeniden ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="939bd-109">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>  

## <a name="detach-a-data-disk-using-cli-20"></a><span data-ttu-id="939bd-110">CLI 2.0 kullanan bir veri diskini</span><span class="sxs-lookup"><span data-stu-id="939bd-110">Detach a data disk using CLI 2.0</span></span>

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

<span data-ttu-id="939bd-111">Disk depolama alanında kalır, ancak artık bir sanal makineye bağlı değildir.</span><span class="sxs-lookup"><span data-stu-id="939bd-111">The disk remains in storage but is no longer attached to a virtual machine.</span></span>


## <a name="detach-a-data-disk-using-the-portal"></a><span data-ttu-id="939bd-112">Portalı kullanarak veri diski çıkarma</span><span class="sxs-lookup"><span data-stu-id="939bd-112">Detach a data disk using the portal</span></span>
1. <span data-ttu-id="939bd-113">Portal hub seçin **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="939bd-113">In the portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="939bd-114">Önce ayırmak istediğiniz veri diskine sahip bir sanal makineyi seçin **durdurmak** VM ayırması kaldırılacak.</span><span class="sxs-lookup"><span data-stu-id="939bd-114">Select the virtual machine that has the data disk you want to detach and click **Stop** to deallocate the VM.</span></span>
3. <span data-ttu-id="939bd-115">Sanal makine dikey penceresinde, seçin **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="939bd-115">In the virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="939bd-116">Üstündeki **diskleri** dikey penceresinde, select **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="939bd-116">At the top of the **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="939bd-117">İçinde **diskleri** ayırmak için istediğiniz veri diski en sağdaki dikey ![ayırma düğme görüntüsü](./media/detach-disk/detach.png) düğmesi ayırın.</span><span class="sxs-lookup"><span data-stu-id="939bd-117">In the **Disks** blade, to the far right of the data disk that you would like to detach, click the ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="939bd-118">Disk kaldırıldıktan sonra dikey pencerenin üst kısmında Kaydet'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="939bd-118">After the disk has been removed, click Save on the top of the blade.</span></span>
6. <span data-ttu-id="939bd-119">Sanal makine dikey penceresinde tıklayın **genel bakış** ve ardından **Başlat** VM'yi yeniden başlatmak için dikey pencerenin üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="939bd-119">In the virtual machine blade, click **Overview** and then click the **Start** button at the top of the blade to restart the VM.</span></span>

<span data-ttu-id="939bd-120">Disk depolama alanında kalır, ancak artık bir sanal makineye bağlı değildir.</span><span class="sxs-lookup"><span data-stu-id="939bd-120">The disk remains in storage but is no longer attached to a virtual machine.</span></span>








## <a name="next-steps"></a><span data-ttu-id="939bd-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="939bd-121">Next steps</span></span>
<span data-ttu-id="939bd-122">Veri diski yeniden kullanmak istiyorsanız, yeni [başka bir VM'e ekleyin](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="939bd-122">If you want to reuse the data disk, you can just [attach it to another VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

