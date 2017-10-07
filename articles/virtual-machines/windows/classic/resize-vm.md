---
title: "aaaResize hello Klasik dağıtım modelinde - Azure Windows VM | Microsoft Docs"
description: "Azure Powershell kullanarak hello Klasik dağıtım modelinde oluşturulmuş bir Windows sanal makine yeniden boyutlandırın."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 39fab14431e2351c9515b0611e850eccfec7a798
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm-created-in-hello-classic-deployment-model"></a><span data-ttu-id="67a42-103">Windows hello Klasik dağıtım modelinde oluşturulan bir VM'yi yeniden boyutlandırın</span><span class="sxs-lookup"><span data-stu-id="67a42-103">Resize a Windows VM created in hello classic deployment model</span></span>
<span data-ttu-id="67a42-104">Bu makalede nasıl tooresize bir Windows VM oluşturulan Azure Powershell kullanarak hello Klasik dağıtım modelinde gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="67a42-104">This article shows you how tooresize a Windows VM, created in hello classic deployment model using Azure Powershell.</span></span>

<span data-ttu-id="67a42-105">Merhaba özelliği tooresize VM değerlendirirken denetlemenize hello boyutları kullanılabilir tooresize hello sanal makine iki kavram vardır.</span><span class="sxs-lookup"><span data-stu-id="67a42-105">When considering hello ability tooresize a VM, there are two concepts which control hello range of sizes available tooresize hello virtual machine.</span></span> <span data-ttu-id="67a42-106">Merhaba ilk kavram, VM dağıtıldığı hello bölgedir.</span><span class="sxs-lookup"><span data-stu-id="67a42-106">hello first concept is hello region in which your VM is deployed.</span></span> <span data-ttu-id="67a42-107">Merhaba bölgede kullanılabilir VM boyutları hello Hizmetleri sekmesinde hello Azure bölgeleri web sayfasının altında listesidir.</span><span class="sxs-lookup"><span data-stu-id="67a42-107">hello list of VM sizes available in region is under hello Services tab of hello Azure Regions web page.</span></span> <span data-ttu-id="67a42-108">Merhaba ikinci hello fiziksel donanım şu anda, VM barındırma kavramdır.</span><span class="sxs-lookup"><span data-stu-id="67a42-108">hello second concept is hello physical hardware currently hosting your VM.</span></span> <span data-ttu-id="67a42-109">sanal makineleri barındıran hello fiziksel sunucuları ortak fiziksel donanım kümelerde birlikte gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="67a42-109">hello physical servers hosting VMs are grouped together in clusters of common physical hardware.</span></span> <span data-ttu-id="67a42-110">Merhaba istenen yeni VM boyutu şu anda hello VM barındırma hello donanım küme tarafından desteklenip desteklenmediğini VM boyutunu değiştirme hello yöntemi bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="67a42-110">hello method of changing a VM size differs depending on if hello desired new VM size is supported by hello hardware cluster currently hosting hello VM.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="67a42-111">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="67a42-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="67a42-112">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="67a42-112">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="67a42-113">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="67a42-113">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="67a42-114">Ayrıca [hello Resource Manager dağıtım modelinde oluşturulan bir VM'yi yeniden boyutlandırın](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="67a42-114">You can also [resize a VM created in hello Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="add-your-account"></a><span data-ttu-id="67a42-115">Hesabınızı ekleme</span><span class="sxs-lookup"><span data-stu-id="67a42-115">Add your account</span></span>
<span data-ttu-id="67a42-116">Klasik Azure kaynakları ile Azure PowerShell toowork yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="67a42-116">You must configure Azure PowerShell toowork with classic Azure resources.</span></span> <span data-ttu-id="67a42-117">Tooconfigure Azure PowerShell toomanage Klasik kaynakları Hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="67a42-117">Follow hello steps below tooconfigure Azure PowerShell toomanage classic resources.</span></span>

1. <span data-ttu-id="67a42-118">Merhaba PowerShell isteminde `Add-AzureAccount` tıklatıp **Enter**.</span><span class="sxs-lookup"><span data-stu-id="67a42-118">At hello PowerShell prompt, type `Add-AzureAccount` and click **Enter**.</span></span> 
2. <span data-ttu-id="67a42-119">Azure aboneliğinizle ilişkili hello e-posta adresini yazın ve tıklatın **devam**.</span><span class="sxs-lookup"><span data-stu-id="67a42-119">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="67a42-120">Merhaba hesabınızın parolasını yazın.</span><span class="sxs-lookup"><span data-stu-id="67a42-120">Type in hello password for your account.</span></span> 
4. <span data-ttu-id="67a42-121">Tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="67a42-121">Click **Sign in**.</span></span> 

## <a name="resize-in-hello-same-hardware-cluster"></a><span data-ttu-id="67a42-122">Hello aynı yeniden boyutlandırma donanım küme</span><span class="sxs-lookup"><span data-stu-id="67a42-122">Resize in hello same hardware cluster</span></span>
<span data-ttu-id="67a42-123">tooresize hello VM, barındırma hello donanım kümede kullanılabilir VM tooa boyutunu hello aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="67a42-123">tooresize a VM tooa size available in hello hardware cluster hosting hello VM, perform hello following steps.</span></span>

1. <span data-ttu-id="67a42-124">Aşağıdaki PowerShell komutunu toolist hello VM boyutlarını içeren hello bulut hizmetini barındıran hello donanım kümede kullanılabilir VM hello hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="67a42-124">Run hello following PowerShell command toolist hello VM sizes available in hello hardware cluster hosting hello cloud service which contains hello VM.</span></span>
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. <span data-ttu-id="67a42-125">Aşağıdaki komutları tooresize hello VM hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="67a42-125">Run hello following commands tooresize hello VM.</span></span>
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a><span data-ttu-id="67a42-126">Yeni bir donanım kümede yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="67a42-126">Resize on a new hardware cluster</span></span>
<span data-ttu-id="67a42-127">tooresize VM tooa boyut hello donanım küme barındırma kullanılamıyor Merhaba VM, hello bulut hizmeti ve hello bulut hizmetindeki tüm sanal makineleri yeniden oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="67a42-127">tooresize a VM tooa size not available in hello hardware cluster hosting hello VM, hello cloud service and all VMs in hello cloud service must be recreated.</span></span> <span data-ttu-id="67a42-128">Merhaba bulut hizmetindeki tüm sanal makineleri bir donanım kümesine desteklenen bir boyutta olması gerekir böylece her bir bulut hizmeti bir tek bir donanım kümesine barındırılır.</span><span class="sxs-lookup"><span data-stu-id="67a42-128">Each cloud service is hosted on a single hardware cluster so all VMs in hello cloud service must be a size that is supported on a hardware cluster.</span></span> <span data-ttu-id="67a42-129">Merhaba aşağıdaki adımları nasıl tooresize VM silerek ve sonra yeniden hello bulut anlatmaktadır hizmet.</span><span class="sxs-lookup"><span data-stu-id="67a42-129">hello following steps will describe how tooresize a VM by deleting and then recreating hello cloud service.</span></span>

1. <span data-ttu-id="67a42-130">PowerShell komut toolist hello VM boyutları kullanılabilir hello bölgede aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="67a42-130">Run hello following PowerShell command toolist hello VM sizes available in hello region.</span></span> 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. <span data-ttu-id="67a42-131">Yeniden boyutlandırılabilir hello VM toobe içeren hello bulut hizmetinde her VM için tüm yapılandırma ayarlarını not edin.</span><span class="sxs-lookup"><span data-stu-id="67a42-131">Make note of all configuration settings for each VM in hello cloud service which contains hello VM toobe resized.</span></span> 
3. <span data-ttu-id="67a42-132">Her VM için hello seçeneği tooretain hello diskleri seçerek hello bulut hizmetindeki tüm sanal makineleri silin.</span><span class="sxs-lookup"><span data-stu-id="67a42-132">Delete all VMs in hello cloud service selecting hello option tooretain hello disks for each VM.</span></span>
4. <span data-ttu-id="67a42-133">Merhaba istenen VM boyutu kullanarak yeniden boyutlandırılabilir hello VM toobe yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="67a42-133">Recreate hello VM toobe resized using hello desired VM size.</span></span>
5. <span data-ttu-id="67a42-134">Şimdi hello bulut hizmetini barındıran hello donanım kümede bir VM boyutu kullanarak hello bulut hizmeti olan diğer tüm VM'ler yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="67a42-134">Recreate all other VMs which were in hello cloud service using a VM size available in hello hardware cluster now hosting hello cloud service.</span></span>

<span data-ttu-id="67a42-135">Silme ve yeni bir VM boyutu kullanarak bir bulut hizmeti yeniden oluşturmak için örnek betik bulunabilir [burada](https://github.com/Azure/azure-vm-scripts).</span><span class="sxs-lookup"><span data-stu-id="67a42-135">A sample script for deleting and recreating a cloud service using a new VM size can be found [here](https://github.com/Azure/azure-vm-scripts).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="67a42-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="67a42-136">Next steps</span></span>
* <span data-ttu-id="67a42-137">[Merhaba Resource Manager dağıtım modelinde oluşturulan bir VM'yi yeniden boyutlandırın](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="67a42-137">[Resize a VM created in hello Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

