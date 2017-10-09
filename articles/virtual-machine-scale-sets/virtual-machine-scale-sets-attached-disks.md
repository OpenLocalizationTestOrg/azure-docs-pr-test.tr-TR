---
title: "Sanal makine ölçek kümeleri eklenen veri disklerini aaaAzure | Microsoft Docs"
description: "Veri diskleri sanal makine ölçek kümeleri ile nasıl toouse bağlı öğrenin"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 77b66f80934c0aaf7bb1ad0de00a738052a878ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a><span data-ttu-id="b2d10-103">Azure VM ölçek kümeleri ve bağlı veri diskleri</span><span class="sxs-lookup"><span data-stu-id="b2d10-103">Azure VM scale sets and attached data disks</span></span>
<span data-ttu-id="b2d10-104">Azure [sanal makine ölçek kümeleri](/azure/virtual-machine-scale-sets/), bağlı veri diskleri olan sanal makineleri artık desteklemektedir.</span><span class="sxs-lookup"><span data-stu-id="b2d10-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) now support virtual machines with attached data disks.</span></span> <span data-ttu-id="b2d10-105">Veri diskleri hello depolama profilinde yönetilen Azure disklerle oluşturulan ölçek kümeleri için tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="b2d10-105">Data disks can be defined in hello storage profile for scale sets that have been created with Azure Managed Disks.</span></span> <span data-ttu-id="b2d10-106">Daha önce hello yalnızca doğrudan bağlı depolama seçenekleri ölçek kümesi VM ile birlikte kullanılabilir hello işletim sistemi sürücüsü ve geçici sürücüleri yoktu.</span><span class="sxs-lookup"><span data-stu-id="b2d10-106">Previously hello only directly attached storage options available with VMs in scale sets were hello OS drive and temp drives.</span></span>

> [!NOTE]
>  <span data-ttu-id="b2d10-107">Ölçeği ekli veriler diskler tanımlı Ayarla oluşturduğunuzda, yine de toomount gerekir ve biçiminde hello gelen VM toouse içinde bunları (tek başına Azure VM'ler için olduğu gibi) diskler.</span><span class="sxs-lookup"><span data-stu-id="b2d10-107">When you create a scale set with attached data disks defined, you still need toomount and format hello disks from within a VM toouse them (just like for standalone Azure VMs).</span></span> <span data-ttu-id="b2d10-108">Uygun bir yol toodo toouse standart betik toopartition çağırır ve VM üzerindeki tüm hello veri diskleri Biçimlendir bir özel betik uzantısı budur.</span><span class="sxs-lookup"><span data-stu-id="b2d10-108">A convenient way toodo this is toouse a custom script extension which calls a standard script toopartition and format all hello data disks on a VM.</span></span>

## <a name="create-a-scale-set-with-attached-data-disks"></a><span data-ttu-id="b2d10-109">Bağlı veri diskleri olan ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2d10-109">Create a scale set with attached data disks</span></span>
<span data-ttu-id="b2d10-110">Bir ölçek kümesi bağlı diskler ile basit yol toocreate toouse hello olan [Azure CLI](https://github.com/Azure/azure-cli) _vmss oluşturma_ komutu.</span><span class="sxs-lookup"><span data-stu-id="b2d10-110">A simple way toocreate a scale set with attached disks is toouse hello [Azure CLI](https://github.com/Azure/azure-cli) _vmss create_ command.</span></span> <span data-ttu-id="b2d10-111">Aşağıdaki örneğine hello sırasıyla bir Azure kaynak grubu ve 10 Ubuntu VM, 50 GB ve 100 GB 2 eklenen veri disklerini hepsiyle VM ölçek kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b2d10-111">hello following example creates an Azure resource group, and a VM scale set of 10 Ubuntu VMs, each with 2 attached data disks, of 50 GB and 100 GB respectively.</span></span>
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
<span data-ttu-id="b2d10-112">Bu hello Not _vmss oluşturma_ bunları belirtmezseniz, komut Varsayılanları bazı yapılandırma değerleri.</span><span class="sxs-lookup"><span data-stu-id="b2d10-112">Note that hello _vmss create_ command defaults certain configuration values if you do not specify them.</span></span> <span data-ttu-id="b2d10-113">try kılabilirsiniz toosee hello mevcut Seçenekler:</span><span class="sxs-lookup"><span data-stu-id="b2d10-113">toosee hello available options that you can override try:</span></span>
```bash
az vmss create --help
```
<span data-ttu-id="b2d10-114">Başka bir şekilde toocreate ölçeği ile eklenen veri disklerini Ayarla olan bir ölçek kümesi bir Azure Resource Manager şablonu toodefine içeren bir _dataDisks_ hello bölümünde _storageProfile_ve hello dağıtma Şablon.</span><span class="sxs-lookup"><span data-stu-id="b2d10-114">Another way toocreate a scale set with attached data disks is toodefine a scale set in an Azure Resource Manager template, include a _dataDisks_ section in hello _storageProfile_, and deploy hello template.</span></span> <span data-ttu-id="b2d10-115">Merhaba 50 GB ve 100 GB disk yukarıdaki örnekte bu gibi hello şablonda tanımlanan:</span><span class="sxs-lookup"><span data-stu-id="b2d10-115">hello 50 GB and 100 GB disk example above would be defined like this in hello template:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
<span data-ttu-id="b2d10-116">Burada tanımlanan bağlı bir diskte ile ölçek kümesi şablonu tam, hazır toodeploy örnek görebilirsiniz: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span><span class="sxs-lookup"><span data-stu-id="b2d10-116">You can see a complete, ready toodeploy example of a scale set template with an attached disk defined here: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span></span>

## <a name="adding-a-data-disk-tooan-existing-scale-set"></a><span data-ttu-id="b2d10-117">Bir veri diski tooan varolan ölçek eklemeden ayarlayın</span><span class="sxs-lookup"><span data-stu-id="b2d10-117">Adding a data disk tooan existing scale set</span></span>
> [!NOTE]
>  <span data-ttu-id="b2d10-118">İle oluşturulan veri diskleri tooa ölçek kümesi yalnızca iliştirebilirsiniz [Azure yönetilen diskleri](./virtual-machine-scale-sets-managed-disks.md).</span><span class="sxs-lookup"><span data-stu-id="b2d10-118">You can only attach data disks tooa scale set which has been created with [Azure Managed Disks](./virtual-machine-scale-sets-managed-disks.md).</span></span>

<span data-ttu-id="b2d10-119">Azure CLI kullanarak bir veri diski tooa VM ölçek ekleyebilirsiniz _az vmss diskini_ komutu.</span><span class="sxs-lookup"><span data-stu-id="b2d10-119">You can add a data disk tooa VM scale set using Azure CLI _az vmss disk attach_ command.</span></span> <span data-ttu-id="b2d10-120">Henüz kullanımda olmayan bir mantıksal birim numarası belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="b2d10-120">Make sure you specify a lun which is not already in use.</span></span> <span data-ttu-id="b2d10-121">Aşağıdaki CLI örneğine hello 50 GB Sürücü toolun 3 ekler:</span><span class="sxs-lookup"><span data-stu-id="b2d10-121">hello following CLI example adds a 50 GB drive toolun 3:</span></span>
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

<span data-ttu-id="b2d10-122">Aşağıdaki PowerShell örneğine hello 50 GB Sürücü toolun 3 ekler:</span><span class="sxs-lookup"><span data-stu-id="b2d10-122">hello following PowerShell example adds a 50 GB drive toolun 3:</span></span>
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> <span data-ttu-id="b2d10-123">Farklı VM boyutları hello destekledikleri bağlı sürücüler numaralarında farklı sınırlara sahiptir.</span><span class="sxs-lookup"><span data-stu-id="b2d10-123">Different VM sizes have different limits on hello numbers of attached drives they support.</span></span> <span data-ttu-id="b2d10-124">Merhaba denetleyin [sanal makine boyutu özellikleri](../virtual-machines/windows/sizes.md) yeni bir disk eklemeden önce.</span><span class="sxs-lookup"><span data-stu-id="b2d10-124">Check hello [virtual machine size characteristics](../virtual-machines/windows/sizes.md) before adding a new disk.</span></span>

<span data-ttu-id="b2d10-125">Yeni bir giriş toohello ekleyerek bir disk ekleyebilmeniz _dataDisks_ hello özelliğinde _storageProfile_ tanımı ve hello değişiklik uygulama ölçeğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b2d10-125">You can also add a disk by adding a new entry toohello _dataDisks_ property in hello _storageProfile_ of a scale set definition and applying hello change.</span></span> <span data-ttu-id="b2d10-126">tootest Bu, bulma hello var olan bir ölçek kümesi tanımında [Azure kaynak Gezgini](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b2d10-126">tootest this, find an existing scale set definition in hello [Azure Resource Explorer](https://resources.azure.com/).</span></span> <span data-ttu-id="b2d10-127">Seçin _Düzenle_ ve veri diskleri yeni bir disk toohello listesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b2d10-127">Select _Edit_ and add a new disk toohello list of data disks.</span></span> <span data-ttu-id="b2d10-128">Örneğin</span><span class="sxs-lookup"><span data-stu-id="b2d10-128">E.g.</span></span> <span data-ttu-id="b2d10-129">Yukarıdaki Hello örneği kullanarak:</span><span class="sxs-lookup"><span data-stu-id="b2d10-129">using hello example above:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

<span data-ttu-id="b2d10-130">Ardından _PUT_ tooapply hello tooyour ölçek kümesini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="b2d10-130">Then select _PUT_ tooapply hello changes tooyour scale set.</span></span> <span data-ttu-id="b2d10-131">Bu örnek, ikiden fazla bağlı veri diskini destekleyen bir VM boyutu kullandığınız sürece işe yarar.</span><span class="sxs-lookup"><span data-stu-id="b2d10-131">This example would work as long as you are using a VM size which supports more than two attached data disks.</span></span>

> [!NOTE]
> <span data-ttu-id="b2d10-132">Yaptığınızda ekleyerek veya kaldırarak bir veri diski gibi tanımı bir değişiklik tooa ölçek kümesi, yeni oluşturulan tooall VM'ler geçerlidir, ancak yalnızca tooexisting VM'ler hello geçerlidir _upgradePolicy_ özelliği çok "Otomatik" olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b2d10-132">When you make a change tooa scale set definition such as adding or removing a data disk, it applies tooall newly created VMs, but only applies tooexisting VMs if hello _upgradePolicy_ property is set too"Automatic".</span></span> <span data-ttu-id="b2d10-133">"Manual" çok ayarlı ise, toomanually gereken hello yeni model tooexisting VM'ler uygulayın.</span><span class="sxs-lookup"><span data-stu-id="b2d10-133">If it is set too"Manual", you need toomanually apply hello new model tooexisting VMs.</span></span> <span data-ttu-id="b2d10-134">Merhaba Portalı'nda hello kullanarak bunu yapabilirsiniz _güncelleştirme AzureRmVmssInstance_ PowerShell komut veya hello kullanarak _az vmss güncelleştirme-örnekleri_ CLI komutu.</span><span class="sxs-lookup"><span data-stu-id="b2d10-134">You can do this in hello portal, using hello _Update-AzureRmVmssInstance_ PowerShell command, or using hello _az vmss update-instances_ CLI command.</span></span>

## <a name="adding-pre-populated-data-disks-tooan-existent-scale-set"></a><span data-ttu-id="b2d10-135">Ekleme önceden doldurulmuş haldedir veri diskleri tooan mevcut ölçek kümesi</span><span class="sxs-lookup"><span data-stu-id="b2d10-135">Adding pre-populated data disks tooan existent scale set</span></span> 
> <span data-ttu-id="b2d10-136">Diskleri tooan mevcut eklediğinizde tasarım modeli, Ölçek kümesi, hello disk her zaman boş oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b2d10-136">When you add disks tooan existent scale set model, by design, hello disk will always be created empty.</span></span> <span data-ttu-id="b2d10-137">Bu senaryo ayrıca hello ölçek kümesi tarafından oluşturulan yeni örnekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b2d10-137">This scenario also includes new instances created by hello scale set.</span></span> <span data-ttu-id="b2d10-138">Bu davranışa Hello scaleset tanımı bir boş veri diskine sahip olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="b2d10-138">This behaviour is because hello scaleset definition has an empty data disk.</span></span> <span data-ttu-id="b2d10-139">Sipariş toocreate önceden doldurulmuş haldedir veri sürücülerinde mevcut ölçek kümesi modeli için sonraki iki seçenekten birini seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b2d10-139">In order toocreate pre-populated data drives for an existent scale set model, you can choose either of next two options:</span></span>

* <span data-ttu-id="b2d10-140">Verileri hello örnek 0 VM toohello veri diskleri hello diğer VM'ler özel bir komut dosyası çalıştırarak kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="b2d10-140">Copy data from hello instance 0 VM toohello data disk(s) in hello other VMs by running a custom script.</span></span>
* <span data-ttu-id="b2d10-141">Merhaba işletim sistemi disk artı veri diski (gerekli hello verilerle) ile yönetilen bir görüntü oluşturun ve yeni scaleset hello görüntüsüyle oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b2d10-141">Create a managed image with hello OS disk plus data disk (with hello required data) and create a new scaleset with hello image.</span></span> <span data-ttu-id="b2d10-142">Bu şekilde oluşturulan her yeni VM bir verilere sahip olur, hello scaleset hello tanımında belirtilen disk.</span><span class="sxs-lookup"><span data-stu-id="b2d10-142">This way every new VM created will have a data disk that that is provided in hello definition of hello scaleset.</span></span> <span data-ttu-id="b2d10-143">Bu tanım tooan görüntü veri özelleştirilmiş bir veri diski başvuruda bulunacak olduğundan, bu değişikliklerle hello scaleset her sanal makineye otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="b2d10-143">Since this definition will refer tooan image with a data disk that has customized data, every virtual machine on hello scaleset will automatically come up with these changes.</span></span>

> <span data-ttu-id="b2d10-144">özel görüntü şurada bulunabilir yolu toocreate hello: [yönetilen bir genelleştirilmiş bir VM görüntüsü oluşturma](/azure/virtual-machines/windows/capture-image-resource/)</span><span class="sxs-lookup"><span data-stu-id="b2d10-144">hello way toocreate a custom image can be found here: [Create a managed image of a generalized VM in Azure](/azure/virtual-machines/windows/capture-image-resource/)</span></span> 

> <span data-ttu-id="b2d10-145">Merhaba kullanıcının ihtiyacı toocapture hello gerekli verileri hello sahip 0 VM örneği ve daha sonra bu vhd için hello görüntü tanımı kullanın.</span><span class="sxs-lookup"><span data-stu-id="b2d10-145">hello user needs toocapture hello instance 0 VM which has hello required data, and then use that vhd for hello image definition.</span></span>

## <a name="removing-a-data-disk-from-a-scale-set"></a><span data-ttu-id="b2d10-146">Bir ölçek kümesinden veri diski kaldırma</span><span class="sxs-lookup"><span data-stu-id="b2d10-146">Removing a data disk from a scale set</span></span>
<span data-ttu-id="b2d10-147">Azure CLI _az vmss disk detach_ komutunu kullanarak bir VM ölçek kümesinden veri diski kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2d10-147">You can remove a data disk from a VM scale set using Azure CLI _az vmss disk detach_ command.</span></span> <span data-ttu-id="b2d10-148">Örneğin hello aşağıdaki komut hello diski lun 2 tanımlı kaldırır.</span><span class="sxs-lookup"><span data-stu-id="b2d10-148">For example hello following command removes hello disk defined at lun 2:</span></span>
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
<span data-ttu-id="b2d10-149">Benzer şekilde, aynı zamanda bir diski bir ölçeği hello bir giriş kaldırarak Ayarla kaldırabilirsiniz _dataDisks_ hello özelliğinde _storageProfile_ ve hello değişiklik uygulama.</span><span class="sxs-lookup"><span data-stu-id="b2d10-149">Similarly you can also remove a disk from a scale set by removing an entry from hello _dataDisks_ property in hello _storageProfile_ and applying hello change.</span></span> 

## <a name="additional-notes"></a><span data-ttu-id="b2d10-150">Ek notlar</span><span class="sxs-lookup"><span data-stu-id="b2d10-150">Additional notes</span></span>
<span data-ttu-id="b2d10-151">Destek eklenen veri disklerini Azure yönetilen diskleri ve ölçek kümesi için kullanılabilir'API sürümünde [ _2016-04-30-Önizleme_ ](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) veya daha sonraki hello Microsoft.Compute API sürümü.</span><span class="sxs-lookup"><span data-stu-id="b2d10-151">Support for Azure Managed disks and scale set attached data disks is available in API version [_2016-04-30-preview_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) or later of hello Microsoft.Compute API.</span></span>

<span data-ttu-id="b2d10-152">Merhaba ilk uygulamasında ölçek kümeleri bağlı disk desteğinin iliştiremezsiniz ya da veri diskleri için/ölçek kümesindeki tek tek sanal makineleri ayırma.</span><span class="sxs-lookup"><span data-stu-id="b2d10-152">In hello initial implementation of attached disk support for scale sets, you cannot attach or detach data disks to/from individual VMs in a scale set.</span></span>

<span data-ttu-id="b2d10-153">Ölçek kümelerindeki bağlı veri diskleri için Azure portalı desteği başlangıçta sınırlıydı.</span><span class="sxs-lookup"><span data-stu-id="b2d10-153">Azure portal support for attached data disks in scale sets is initially limited.</span></span> <span data-ttu-id="b2d10-154">Azure şablonları kullanabilirsiniz gereksinimlerinize bağlı olarak, CLI, PowerShell, SDK'ları ve REST API toomanage diskleri bağlı.</span><span class="sxs-lookup"><span data-stu-id="b2d10-154">Depending on your requirements you can use Azure templates, CLI, PowerShell, SDKs, and REST API toomanage attached disks.</span></span>


