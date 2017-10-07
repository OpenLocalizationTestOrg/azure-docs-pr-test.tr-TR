---
title: bir Linux VM - Azure veri diskten aaaDetach | Microsoft Docs
description: "Toodetach CLI 2.0 veya hello Azure portal kullanarak azure'da bir sanal makineden bir veri diski öğrenin."
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
ms.openlocfilehash: 1c6145fc97f13179457225e93e0fb7adc261a65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-linux-virtual-machine"></a><span data-ttu-id="279d1-103">Nasıl toodetach bir veri diski bir Linux sanal makineden</span><span class="sxs-lookup"><span data-stu-id="279d1-103">How toodetach a data disk from a Linux virtual machine</span></span>

<span data-ttu-id="279d1-104">Ekli tooa sanal makine veri diski artık ihtiyacınız olduğunda, kolayca ayırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="279d1-104">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="279d1-105">Bu hello disk hello sanal makineden kaldırır, ancak depolama biriminden kaldırmaz.</span><span class="sxs-lookup"><span data-stu-id="279d1-105">This removes hello disk from hello virtual machine, but doesn't remove it from storage.</span></span> 

> [!WARNING]
> <span data-ttu-id="279d1-106">Bir disk ayırırsanız otomatik olarak silinmez.</span><span class="sxs-lookup"><span data-stu-id="279d1-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="279d1-107">TooPremium depolama abone hello disk için tooincur depolama ücretleri devam eder.</span><span class="sxs-lookup"><span data-stu-id="279d1-107">If you have subscribed tooPremium storage, you will continue tooincur storage charges for hello disk.</span></span> <span data-ttu-id="279d1-108">Daha fazla bilgi için çok başvurun[fiyatlandırma ve faturalama Premium depolama kullanırken](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="279d1-108">For more information refer too[Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span> 
> 
> 

<span data-ttu-id="279d1-109">Merhaba disk üzerindeki toouse hello mevcut verileri yeniden istiyorsanız, toohello iliştirebilirsiniz aynı sanal makine ya da başka bir.</span><span class="sxs-lookup"><span data-stu-id="279d1-109">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

## <a name="detach-a-data-disk-using-cli-20"></a><span data-ttu-id="279d1-110">CLI 2.0 kullanan bir veri diskini</span><span class="sxs-lookup"><span data-stu-id="279d1-110">Detach a data disk using CLI 2.0</span></span>

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

<span data-ttu-id="279d1-111">Merhaba disk depolama alanında kalır, ancak artık ekli tooa sanal makine değil.</span><span class="sxs-lookup"><span data-stu-id="279d1-111">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>


## <a name="detach-a-data-disk-using-hello-portal"></a><span data-ttu-id="279d1-112">Merhaba portalı kullanarak bir veri diskini</span><span class="sxs-lookup"><span data-stu-id="279d1-112">Detach a data disk using hello portal</span></span>
1. <span data-ttu-id="279d1-113">Merhaba portal hub, seçin **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="279d1-113">In hello portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="279d1-114">Toodetach istediğiniz hello veri diski Hello sanal makine seçin **durdurmak** toodeallocate hello VM.</span><span class="sxs-lookup"><span data-stu-id="279d1-114">Select hello virtual machine that has hello data disk you want toodetach and click **Stop** toodeallocate hello VM.</span></span>
3. <span data-ttu-id="279d1-115">Merhaba sanal makine dikey penceresinde, seçin **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="279d1-115">In hello virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="279d1-116">Merhaba hello üstündeki **diskleri** dikey penceresinde, select **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="279d1-116">At hello top of hello **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="279d1-117">Merhaba, **diskleri** dikey, sağda hello veri diski toodetach, istediğiniz toohello tıklayın hello ![ayırma düğme görüntüsü](./media/detach-disk/detach.png) düğmesi ayırma.</span><span class="sxs-lookup"><span data-stu-id="279d1-117">In hello **Disks** blade, toohello far right of hello data disk that you would like toodetach, click hello ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="279d1-118">Merhaba disk kaldırıldıktan sonra hello dikey penceresinde hello üstündeki Kaydet.</span><span class="sxs-lookup"><span data-stu-id="279d1-118">After hello disk has been removed, click Save on hello top of hello blade.</span></span>
6. <span data-ttu-id="279d1-119">Merhaba sanal makine dikey penceresinde tıklayın **genel bakış** ve hello ardından **Başlat** hello dikey toorestart hello VM hello üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="279d1-119">In hello virtual machine blade, click **Overview** and then click hello **Start** button at hello top of hello blade toorestart hello VM.</span></span>

<span data-ttu-id="279d1-120">Merhaba disk depolama alanında kalır, ancak artık ekli tooa sanal makine değil.</span><span class="sxs-lookup"><span data-stu-id="279d1-120">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>








## <a name="next-steps"></a><span data-ttu-id="279d1-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="279d1-121">Next steps</span></span>
<span data-ttu-id="279d1-122">Tooreuse hello veri diski istiyorsanız, yeni [tooanother VM ekleme](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="279d1-122">If you want tooreuse hello data disk, you can just [attach it tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

