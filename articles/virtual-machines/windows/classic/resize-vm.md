---
title: "Klasik dağıtım modelinde - Azure Windows VM yeniden boyutlandırmak | Microsoft Docs"
description: "Azure Powershell kullanarak Klasik dağıtım modelinde oluşturulmuş bir Windows sanal makine yeniden boyutlandırın."
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
ms.openlocfilehash: 4277bc8394c7ba140291e9dc776162e87deab96b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-windows-vm-created-in-the-classic-deployment-model"></a><span data-ttu-id="20519-103">Windows Klasik dağıtım modelinde oluşturulan bir VM'yi yeniden boyutlandırın</span><span class="sxs-lookup"><span data-stu-id="20519-103">Resize a Windows VM created in the classic deployment model</span></span>
<span data-ttu-id="20519-104">Bu makalede Windows Azure Powershell kullanarak Klasik dağıtım modelinde oluşturulan bir VM'yi yeniden boyutlandırın gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="20519-104">This article shows you how to resize a Windows VM, created in the classic deployment model using Azure Powershell.</span></span>

<span data-ttu-id="20519-105">Bir VM yeniden boyutlandırma yeteneği değerlendirirken, sanal makine yeniden boyutlandırmak kullanılabilir boyutları denetlemenize iki kavram vardır.</span><span class="sxs-lookup"><span data-stu-id="20519-105">When considering the ability to resize a VM, there are two concepts which control the range of sizes available to resize the virtual machine.</span></span> <span data-ttu-id="20519-106">İlk VM dağıtıldığı bölge kavramdır.</span><span class="sxs-lookup"><span data-stu-id="20519-106">The first concept is the region in which your VM is deployed.</span></span> <span data-ttu-id="20519-107">Azure bölgeleri web sayfası Hizmetleri sekmesi altında bölgede kullanılabilir VM boyutları listesidir.</span><span class="sxs-lookup"><span data-stu-id="20519-107">The list of VM sizes available in region is under the Services tab of the Azure Regions web page.</span></span> <span data-ttu-id="20519-108">Şu anda, VM barındıran fiziksel donanımı ikinci kavramdır.</span><span class="sxs-lookup"><span data-stu-id="20519-108">The second concept is the physical hardware currently hosting your VM.</span></span> <span data-ttu-id="20519-109">Sanal makineleri barındıran fiziksel sunucuları ortak fiziksel donanım kümelerde birlikte gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="20519-109">The physical servers hosting VMs are grouped together in clusters of common physical hardware.</span></span> <span data-ttu-id="20519-110">İstenen yeni VM boyutu şu anda VM barındırma donanım küme tarafından desteklenip desteklenmediğini VM boyutunu değiştirme yöntemi bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="20519-110">The method of changing a VM size differs depending on if the desired new VM size is supported by the hardware cluster currently hosting the VM.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="20519-111">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="20519-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="20519-112">Bu makalede, Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="20519-112">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="20519-113">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="20519-113">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="20519-114">Ayrıca [Resource Manager dağıtım modelinde oluşturulan bir VM'yi yeniden boyutlandırın](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="20519-114">You can also [resize a VM created in the Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="add-your-account"></a><span data-ttu-id="20519-115">Hesabınızı ekleme</span><span class="sxs-lookup"><span data-stu-id="20519-115">Add your account</span></span>
<span data-ttu-id="20519-116">Klasik Azure kaynakları ile çalışmak için Azure PowerShell yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="20519-116">You must configure Azure PowerShell to work with classic Azure resources.</span></span> <span data-ttu-id="20519-117">Azure Klasik kaynakları yönetmek için PowerShell yapılandırmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="20519-117">Follow the steps below to configure Azure PowerShell to manage classic resources.</span></span>

1. <span data-ttu-id="20519-118">PowerShell komut isteminde yazın `Add-AzureAccount` tıklatıp **Enter**.</span><span class="sxs-lookup"><span data-stu-id="20519-118">At the PowerShell prompt, type `Add-AzureAccount` and click **Enter**.</span></span> 
2. <span data-ttu-id="20519-119">Azure aboneliğinizle ilişkili e-posta adresini yazın ve tıklatın **devam**.</span><span class="sxs-lookup"><span data-stu-id="20519-119">Type in the email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="20519-120">Hesabınızın parolasını yazın.</span><span class="sxs-lookup"><span data-stu-id="20519-120">Type in the password for your account.</span></span> 
4. <span data-ttu-id="20519-121">Tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="20519-121">Click **Sign in**.</span></span> 

## <a name="resize-in-the-same-hardware-cluster"></a><span data-ttu-id="20519-122">Aynı donanım kümeye yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="20519-122">Resize in the same hardware cluster</span></span>
<span data-ttu-id="20519-123">VM VM barındırma donanım kümedeki kullanılabilir boyut yeniden boyutlandırmak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="20519-123">To resize a VM to a size available in the hardware cluster hosting the VM, perform the following steps.</span></span>

1. <span data-ttu-id="20519-124">VM içeren bulut hizmeti barındırma donanım kümedeki kullanılabilir VM boyutları listelemek için aşağıdaki PowerShell komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="20519-124">Run the following PowerShell command to list the VM sizes available in the hardware cluster hosting the cloud service which contains the VM.</span></span>
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. <span data-ttu-id="20519-125">VM yeniden boyutlandırmak için aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="20519-125">Run the following commands to resize the VM.</span></span>
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a><span data-ttu-id="20519-126">Yeni bir donanım kümede yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="20519-126">Resize on a new hardware cluster</span></span>
<span data-ttu-id="20519-127">VM VM, bulut barındırma donanım kümede kullanılamaz bir boyuta yeniden boyutlandırmak için hizmet ve bulut hizmetindeki tüm sanal makineleri yeniden oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="20519-127">To resize a VM to a size not available in the hardware cluster hosting the VM, the cloud service and all VMs in the cloud service must be recreated.</span></span> <span data-ttu-id="20519-128">Bulut hizmetindeki tüm sanal makineleri bir donanım kümesine desteklenen bir boyutta olması gerekir böylece her bir bulut hizmeti bir tek bir donanım kümesine barındırılır.</span><span class="sxs-lookup"><span data-stu-id="20519-128">Each cloud service is hosted on a single hardware cluster so all VMs in the cloud service must be a size that is supported on a hardware cluster.</span></span> <span data-ttu-id="20519-129">Aşağıdaki adımlar, silme ve bulut hizmeti yeniden VM yeniden boyutlandırmak nasıl anlatmaktadır.</span><span class="sxs-lookup"><span data-stu-id="20519-129">The following steps will describe how to resize a VM by deleting and then recreating the cloud service.</span></span>

1. <span data-ttu-id="20519-130">Bölgede VM boyutları listelemek için aşağıdaki PowerShell komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="20519-130">Run the following PowerShell command to list the VM sizes available in the region.</span></span> 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. <span data-ttu-id="20519-131">VM yeniden boyutlandırılıp içeren bulut hizmeti her VM için tüm yapılandırma ayarlarını not edin.</span><span class="sxs-lookup"><span data-stu-id="20519-131">Make note of all configuration settings for each VM in the cloud service which contains the VM to be resized.</span></span> 
3. <span data-ttu-id="20519-132">Her VM için diskleri korumak için bu seçenek belirlendiğinde bulut hizmetindeki tüm sanal makineleri silin.</span><span class="sxs-lookup"><span data-stu-id="20519-132">Delete all VMs in the cloud service selecting the option to retain the disks for each VM.</span></span>
4. <span data-ttu-id="20519-133">İstenen VM boyutu kullanarak yeniden boyutlandırılıp VM yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="20519-133">Recreate the VM to be resized using the desired VM size.</span></span>
5. <span data-ttu-id="20519-134">Şimdi bulut hizmetini barındıran donanım kümede bir VM boyutu kullanarak bulut hizmeti olan diğer tüm VM'ler yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="20519-134">Recreate all other VMs which were in the cloud service using a VM size available in the hardware cluster now hosting the cloud service.</span></span>

<span data-ttu-id="20519-135">Silme ve yeni bir VM boyutu kullanarak bir bulut hizmeti yeniden oluşturmak için örnek betik bulunabilir [burada](https://github.com/Azure/azure-vm-scripts).</span><span class="sxs-lookup"><span data-stu-id="20519-135">A sample script for deleting and recreating a cloud service using a new VM size can be found [here](https://github.com/Azure/azure-vm-scripts).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="20519-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="20519-136">Next steps</span></span>
* <span data-ttu-id="20519-137">[Resource Manager dağıtım modelinde oluşturulan bir VM'yi yeniden boyutlandırın](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="20519-137">[Resize a VM created in the Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

