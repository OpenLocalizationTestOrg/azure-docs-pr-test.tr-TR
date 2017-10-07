---
title: "aaaUpgrade bir Azure sanal makine ölçek kümesi | Microsoft Docs"
description: "Bir Azure sanal makine ölçek kümesini yükseltme"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a><span data-ttu-id="b0463-103">Bir sanal makine ölçek kümesini yükseltme</span><span class="sxs-lookup"><span data-stu-id="b0463-103">Upgrade a virtual machine scale set</span></span>
<span data-ttu-id="b0463-104">Bu makalede nasıl herhangi kesinti olmadan ayarlanmış bir işletim sistemi güncelleştirme tooan Azure sanal makine ölçek genişletme dönebilirsiniz açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b0463-104">This article describes how you can roll out an OS update tooan Azure virtual machine scale set without any downtime.</span></span> <span data-ttu-id="b0463-105">Bu bağlamda bir işletim sistemi güncelleştirme hello sürümü veya hello işletim sistemi SKU'su değiştirme veya özel bir görüntü URI'sini hello değiştirme içerir.</span><span class="sxs-lookup"><span data-stu-id="b0463-105">In this context, an OS update involves changing hello version or SKU of hello OS or changing hello URI of a custom image.</span></span> <span data-ttu-id="b0463-106">Sanal makineleri birer birer birer veya gruplar (örneğin, bir seferde bir hata etki alanı) tüm aynı anda yerine güncelleştirme kapalı kalma süresi anlamına gelir olmadan güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="b0463-106">Updating without downtime means updating virtual machines one at a time or in groups (such as one fault domain at a time) rather than all at once.</span></span> <span data-ttu-id="b0463-107">Bunu yaparak, değil yükseltilen tüm sanal makineleri çalışmaya devam.</span><span class="sxs-lookup"><span data-stu-id="b0463-107">By doing so, any virtual machines that are not being upgraded can keep running.</span></span>

<span data-ttu-id="b0463-108">tooavoid belirsizlik şimdi isteyebileceğiniz işletim sistemi güncelleştirme dört tür ayırt tooperform:</span><span class="sxs-lookup"><span data-stu-id="b0463-108">tooavoid ambiguity, let’s distinguish four types of OS update you might want tooperform:</span></span>

* <span data-ttu-id="b0463-109">Merhaba sürümü veya SKU platform görüntüsünün değiştirme.</span><span class="sxs-lookup"><span data-stu-id="b0463-109">Changing hello version or SKU of a platform image.</span></span> <span data-ttu-id="b0463-110">Örneğin, Ubuntu değiştirme 14.04.201506100 14.04.2-LTS sürümünden too14.04.201507060 veya hello Ubuntu 15.10/son SKU too16.04.0-LTS/latest değiştirme.</span><span class="sxs-lookup"><span data-stu-id="b0463-110">For example, changing Ubuntu 14.04.2-LTS version from 14.04.201506100 too14.04.201507060, or changing hello Ubuntu 15.10/latest SKU too16.04.0-LTS/latest.</span></span> <span data-ttu-id="b0463-111">Bu senaryo, bu makalede ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="b0463-111">This scenario is covered in this article.</span></span>
* <span data-ttu-id="b0463-112">Merhaba tooa yeni oluşturulan özel bir görüntü sürümü işaret URI değiştirme (**özellikleri** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **görüntü** > **URI**).</span><span class="sxs-lookup"><span data-stu-id="b0463-112">Changing hello URI that points tooa new version of a custom image you built (**properties** > **virtualMachineProfile** > **storageProfile** > **osDisk** > **image** > **uri**).</span></span> <span data-ttu-id="b0463-113">Bu senaryo, bu makalede ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="b0463-113">This scenario is covered in this article.</span></span>
* <span data-ttu-id="b0463-114">Azure yönetilen diskleri kullanılarak oluşturulmuş bir ölçek kümesinin Hello resim başvurusu değiştirme.</span><span class="sxs-lookup"><span data-stu-id="b0463-114">Changing hello image reference of a scale set that was created using Azure Managed Disks.</span></span>
* <span data-ttu-id="b0463-115">Bir sanal makine içinde hello OS düzeltme eki uygulama (Bu örnekleri arasında bir güvenlik düzeltme eki yükleme ve Windows Update çalıştıran).</span><span class="sxs-lookup"><span data-stu-id="b0463-115">Patching hello OS from within a virtual machine (examples of this include installing a security patch and running Windows Update).</span></span> <span data-ttu-id="b0463-116">Bu senaryo desteklenir, ancak bu makalede ele alınan değil.</span><span class="sxs-lookup"><span data-stu-id="b0463-116">This scenario is supported but not covered in this article.</span></span>

<span data-ttu-id="b0463-117">Bir parçası olarak dağıtılan sanal makine ölçek kümeleri bir [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) küme ele alınmamıştır burada.</span><span class="sxs-lookup"><span data-stu-id="b0463-117">Virtual machine scale sets that are deployed as part of an [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) cluster are not covered here.</span></span> <span data-ttu-id="b0463-118">Bkz: [düzeltme eki Windows işletim sisteminde, Service Fabric kümesi](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) Service Fabric düzeltme eki uygulama hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="b0463-118">See [Patch Windows OS in your Service Fabric cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) for more information about patching Service Fabric.</span></span>

<span data-ttu-id="b0463-119">Merhaba sırasını değiştirmek için işletim sistemi sürümü/SKU'su platform görüntüsü hello veya hello özel görüntü URI'sini aşağıdaki gibi görünür temel:</span><span class="sxs-lookup"><span data-stu-id="b0463-119">hello basic sequence for changing hello OS version/SKU of a platform image or hello URI of a custom image looks as follows:</span></span>

1. <span data-ttu-id="b0463-120">Merhaba sanal makine ölçek kümesi modelinde alın.</span><span class="sxs-lookup"><span data-stu-id="b0463-120">Get hello virtual machine scale set model.</span></span>
2. <span data-ttu-id="b0463-121">Merhaba sürüm, SKU, görüntü başvuru ya da hello modelinde URI değeri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b0463-121">Change hello version, SKU, image reference, or URI value in hello model.</span></span>
3. <span data-ttu-id="b0463-122">Merhaba modeli güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="b0463-122">Update hello model.</span></span>
4. <span data-ttu-id="b0463-123">Yapmak bir *manualUpgrade* hello hello ölçek kümesindeki sanal makinelerde çağırın.</span><span class="sxs-lookup"><span data-stu-id="b0463-123">Do a *manualUpgrade* call on hello virtual machines in hello scale set.</span></span> <span data-ttu-id="b0463-124">Bu adım yalnızca ilgili değilse *upgradePolicy* çok ayarlanır**el ile** , Ölçek kümesi.</span><span class="sxs-lookup"><span data-stu-id="b0463-124">This step is only relevant if *upgradePolicy* is set too**Manual** in your scale set.</span></span> <span data-ttu-id="b0463-125">Çok ayarlanırsa**otomatik**, böylece kapalı kalma süresi neden olan tüm hello sanal makineleri aynı anda yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="b0463-125">If it is set too**Automatic**, all hello virtual machines are upgraded at once, thus causing downtime.</span></span>

<span data-ttu-id="b0463-126">Aklınızda bu bilgi ile PowerShell ve hello REST API kullanarak bir ölçek hello sürümünü nasıl güncelleştirebilir görelim.</span><span class="sxs-lookup"><span data-stu-id="b0463-126">With this information in mind, let’s see how you could update hello version of a scale set in PowerShell, and by using hello REST API.</span></span> <span data-ttu-id="b0463-127">Bu örnekler bir platform görüntüsü hello durumunun kapak, ancak bu makale, bu işlem tooa özel görüntü, tooadapt için yeterli bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0463-127">These examples cover hello case of a platform image, but this article provides enough information for you tooadapt this process tooa custom image.</span></span>

## <a name="powershell"></a><span data-ttu-id="b0463-128">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0463-128">PowerShell</span></span>
<span data-ttu-id="b0463-129">Bu örnek bir Windows sanal makine ölçek kümesi (oluşturma toohello yeni sürüm 4.0.20160229. güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="b0463-129">This example updates a Windows virtual machine scale set (creating toohello new version 4.0.20160229.</span></span> <span data-ttu-id="b0463-130">Merhaba modeli güncelleştirdikten sonra bunu aynı anda bir güncelleştirme bir sanal makine örneğini yapar.</span><span class="sxs-lookup"><span data-stu-id="b0463-130">After updating hello model, it does an update one virtual machine instance at a time.</span></span>

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

<span data-ttu-id="b0463-131">Platform görüntü sürümü değiştiğinde yerine özel bir görüntü için URI hello güncelleştiriyorsanız hello "kümesi hello yeni sürümü" yerine güncelleştirecek bir komut satırıyla hello kaynak görüntü URI.</span><span class="sxs-lookup"><span data-stu-id="b0463-131">If you are updating hello URI for a custom image instead of changing a platform image version, replace hello “set hello new version” line with a command that will update hello source image URI.</span></span> <span data-ttu-id="b0463-132">Azure yönetilen diskleri kullanmadan Hello ölçek kümesini oluşturulduysa, örneğin, hello güncelleştirme şöyle olabilir:</span><span class="sxs-lookup"><span data-stu-id="b0463-132">For example, if hello scale set was created without using Azure Managed Disks, hello update would look like this:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

<span data-ttu-id="b0463-133">Özel görüntü ölçek kümesini geliyorsa hello resim başvurusu güncelleştirilmiş sonra yönetilen Azure diskleri kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="b0463-133">If a custom image based scale set was created using Azure Managed Disks, then hello image reference would be updated.</span></span> <span data-ttu-id="b0463-134">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b0463-134">For example:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a><span data-ttu-id="b0463-135">Merhaba REST API'si</span><span class="sxs-lookup"><span data-stu-id="b0463-135">hello REST API</span></span>
<span data-ttu-id="b0463-136">Burada, birkaç hello Azure REST API tooroll bir işletim sistemi sürümü güncelleştirme çıkışı kullanmak Python örnekler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b0463-136">Here are a couple of Python examples that use hello Azure REST API tooroll out an OS version update.</span></span> <span data-ttu-id="b0463-137">Her ikisini de hello basit kullanmanız [azurerm](https://pypi.python.org/pypi/azurerm) Azure REST API sarmalayıcı işlevleri toodo hello ölçekte bir GET kitaplığının modeli, güncelleştirilmiş bir modelle PUT arkasından ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b0463-137">Both use hello lightweight [azurerm](https://pypi.python.org/pypi/azurerm) library of Azure REST API wrapper functions toodo a GET on hello scale set model, followed by a PUT with an updated model.</span></span> <span data-ttu-id="b0463-138">Bunlar, ayrıca sanal makine örnekleri görünümlerde tooidentify hello sanal makineler güncelleştirme etki alanı tarafından arayın.</span><span class="sxs-lookup"><span data-stu-id="b0463-138">They also look at virtual machine instances views tooidentify hello virtual machines by update domain.</span></span>

### <a name="vmssupgrade"></a><span data-ttu-id="b0463-139">Vmssupgrade</span><span class="sxs-lookup"><span data-stu-id="b0463-139">Vmssupgrade</span></span>
 <span data-ttu-id="b0463-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) tooroll sanal makine ölçek çalışan bir işletim sistemi yükseltme tooa çıkışı kullanılmış bir Python komut dosyası, aynı anda tek bir güncelleştirme etki alanı kümesi.</span><span class="sxs-lookup"><span data-stu-id="b0463-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) is a Python script that's used tooroll out an OS upgrade tooa running virtual machine scale set one update domain at a time.</span></span>

![Sanal makine ya da bir güncelleştirme etki alanı seçme Vmssupgrade komut dosyası](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

<span data-ttu-id="b0463-142">Bu komut, belirli sanal makinelerin tooupdate seçin veya bir güncelleştirme etki alanı belirtirseniz olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="b0463-142">This script lets you choose specific virtual machines tooupdate or specify an update domain.</span></span> <span data-ttu-id="b0463-143">Platform görüntü sürümü değiştirme veya özel bir görüntü URI'sini hello değiştirme destekler.</span><span class="sxs-lookup"><span data-stu-id="b0463-143">It supports changing a platform image version or changing hello URI of a custom image.</span></span>

### <a name="vmsseditor"></a><span data-ttu-id="b0463-144">Vmsseditor</span><span class="sxs-lookup"><span data-stu-id="b0463-144">Vmsseditor</span></span>
<span data-ttu-id="b0463-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) sanal gösterir sanal makine ölçek kümeleri heatmap Durum makinesi için bir genel amaçlı bir güncelleştirme etki alanı bir satır temsil ettiği düzenleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="b0463-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) is a general-purpose editor for virtual machine scale sets that shows virtual machine status as a heatmap where one row represents one update domain.</span></span> <span data-ttu-id="b0463-146">Bunun yanı sıra, hello modeli ölçek kümesi için bir yeni sürümü, SKU veya özel görüntü URI'si ile güncelleştirin ve sonra hata etki alanları tooupgrade seçin.</span><span class="sxs-lookup"><span data-stu-id="b0463-146">Among other things, you can update hello model for a scale set with a new version, SKU, or custom image URI, and then pick fault domains tooupgrade.</span></span> <span data-ttu-id="b0463-147">Bunu yaptığınızda, bu güncelleştirme etki alanındaki tüm hello sanal makineler yükseltilen toohello yeni modeli vardır.</span><span class="sxs-lookup"><span data-stu-id="b0463-147">When you do so, all hello virtual machines in that update domain are upgraded toohello new model.</span></span> <span data-ttu-id="b0463-148">Alternatif olarak, tercih ettiğiniz hello toplu boyutuna göre çalışırken yükseltme yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0463-148">Alternatively, you can do a rolling upgrade based on hello batch size of your choice.</span></span>  

<span data-ttu-id="b0463-149">Merhaba aşağıdaki ekran görüntüsü ölçeği Ubuntu 14.04-2LTS için sürüm 14.04.201507060 Ayarla modelinin gösterir.</span><span class="sxs-lookup"><span data-stu-id="b0463-149">hello following screenshot shows a model of a scale set for Ubuntu 14.04-2LTS version 14.04.201507060.</span></span> <span data-ttu-id="b0463-150">Bu ekran alındıktan sonra pek çok seçenek toothis Aracı eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="b0463-150">Many more options have been added toothis tool since this screenshot was taken.</span></span>

![Ubuntu 14.04-2LTS için ayarlanmış bir ölçek Vmsseditor modeli](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

<span data-ttu-id="b0463-152">Tıklattıktan sonra **yükseltme** ve ardından **ayrıntıları alma**, sanal makinelerinizde UD 0 tooupdate Başlat.</span><span class="sxs-lookup"><span data-stu-id="b0463-152">After you click **Upgrade** and then **Get Details**, virtual machines in UD 0 start tooupdate.</span></span>

![Vmsseditor gösteren güncelleştirmesi devam ediyor](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

