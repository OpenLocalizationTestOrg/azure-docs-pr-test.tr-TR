---
title: "aaaManage Azure uç noktası erişim denetim listeleri | PowerShell | Klasik | Microsoft Docs"
description: "Bilgi nasıl toomanage PowerShell ile ACL"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a><span data-ttu-id="ddcd8-103">Uç noktası erişim denetim listeleri hello Klasik dağıtım modelinde PowerShell kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="ddcd8-103">Manage endpoint access control lists using PowerShell in hello classic deployment model</span></span>
<span data-ttu-id="ddcd8-104">Oluşturun ve ağ erişim denetimi listeleri (ACL'ler) uç noktaları için Azure PowerShell kullanarak veya hello Yönetim Portalı yönetin.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-104">You can create and manage Network Access Control Lists (ACLs) for endpoints by using Azure PowerShell or in hello Management Portal.</span></span> <span data-ttu-id="ddcd8-105">Bu konuda, PowerShell kullanarak tamamlayabilirsiniz ACL ortak görevler için yordamlar bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-105">In this topic, you'll find procedures for ACL common tasks that you can complete using PowerShell.</span></span> <span data-ttu-id="ddcd8-106">Cmdlet'leri Azure PowerShell Hello listesi için bkz [Azure Yönetimi cmdlet'leri](http://go.microsoft.com/fwlink/?LinkId=317721).</span><span class="sxs-lookup"><span data-stu-id="ddcd8-106">For hello list of Azure PowerShell cmdlets see [Azure Management Cmdlets](http://go.microsoft.com/fwlink/?LinkId=317721).</span></span> <span data-ttu-id="ddcd8-107">ACL'ler hakkında daha fazla bilgi için bkz: [bir ağ erişim denetimi listesi (ACL) nedir?](virtual-networks-acl.md).</span><span class="sxs-lookup"><span data-stu-id="ddcd8-107">For more information about ACLs, see [What is a Network Access Control List (ACL)?](virtual-networks-acl.md).</span></span> <span data-ttu-id="ddcd8-108">Hello yönetim portalını kullanarak, ACL'ler toomanage istiyorsanız, bkz: [nasıl tooSet yukarı uç noktaları tooa sanal makine](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ddcd8-108">If you want toomanage your ACLs by using hello Management Portal, see [How tooSet Up Endpoints tooa Virtual Machine](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="manage-network-acls-by-using-azure-powershell"></a><span data-ttu-id="ddcd8-109">Ağ ACL'leri Azure PowerShell kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="ddcd8-109">Manage Network ACLs by using Azure PowerShell</span></span>
<span data-ttu-id="ddcd8-110">Azure PowerShell cmdlet'leri toocreate kullanabileceğiniz kaldırın ve yapılandırın (küme) ağ erişimi denetim listeleri (ACL'ler).</span><span class="sxs-lookup"><span data-stu-id="ddcd8-110">You can use Azure PowerShell cmdlets toocreate, remove, and configure (set) Network Access Control Lists (ACLs).</span></span> <span data-ttu-id="ddcd8-111">Biz, PowerShell kullanarak bir ACL yapılandırmak hello yollardan bazılarını birkaç örnekleri dahil ettiğiniz.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-111">We've included a few examples of some of hello ways you can configure an ACL using PowerShell.</span></span>

<span data-ttu-id="ddcd8-112">tooretrieve hello ACL PowerShell cmdlet'lerinin tam bir listesi, hello aşağıdakilerden herhangi birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ddcd8-112">tooretrieve a complete list of hello ACL PowerShell cmdlets, you can use either of hello following:</span></span>

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a><span data-ttu-id="ddcd8-113">Uzak bir alt ağ üzerinden erişime kurallarla ağ ACL oluşturma</span><span class="sxs-lookup"><span data-stu-id="ddcd8-113">Create a Network ACL with rules that permit access from a remote subnet</span></span>
<span data-ttu-id="ddcd8-114">Merhaba örneği aşağıdaki şekilde toocreate kuralları içeren yeni bir ACL gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-114">hello example below illustrates a way toocreate a new ACL that contains rules.</span></span> <span data-ttu-id="ddcd8-115">Bu ACL sonra uygulanan tooa sanal makine uç noktası.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-115">This ACL is then applied tooa virtual machine endpoint.</span></span> <span data-ttu-id="ddcd8-116">Aşağıdaki hello örnek Hello ACL kuralları, uzak bir alt ağdan erişimi izin verir.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-116">hello ACL rules in hello example below will allow access from a remote subnet.</span></span> <span data-ttu-id="ddcd8-117">Uzak bir alt ağ için toocreate izin ile yeni bir ağ ACL kuralları bir Azure PowerShell ISE açın.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-117">toocreate a new Network ACL with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="ddcd8-118">Kopyalama ve aşağıda kendi değerlerinizle hello komut dosyasını yapılandırarak hello betiğini yapıştırın ve hello betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-118">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="ddcd8-119">Merhaba yeni ağ ACL nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-119">Create hello new network ACL object.</span></span>
   
        $acl1 = New-AzureAclConfig
2. <span data-ttu-id="ddcd8-120">Uzak bir alt ağdan erişimi veren bir kural kümesi.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-120">Set a rule that permits access from a remote subnet.</span></span> <span data-ttu-id="ddcd8-121">Merhaba aşağıdaki örnekte, kural kümesi *100* (olan öncelik kuralına göre 200 ve üzeri) tooallow hello uzak alt *10.0.0.0/8* toohello sanal makine uç noktası erişim.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-121">In hello example below, you set rule *100* (which has priority over rule 200 and higher) tooallow hello remote subnet *10.0.0.0/8* access toohello virtual machine endpoint.</span></span> <span data-ttu-id="ddcd8-122">Merhaba değerleri kendi yapılandırma gereksinimlerine göre değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-122">Replace hello values with your own configuration requirements.</span></span> <span data-ttu-id="ddcd8-123">Merhaba adı "SharePoint ACL yapılandırma" Merhaba kolay adı bu kuralın toocall istediğiniz ile değiştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-123">hello name "SharePoint ACL config" should be replaced with hello friendly name that you want toocall this rule.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. <span data-ttu-id="ddcd8-124">Ek kurallar için kendi yapılandırma gereksinimlerine göre hello değerleri değiştirerek hello cmdlet'ini tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-124">For additional rules, repeat hello cmdlet, replacing hello values with your own configuration requirements.</span></span> <span data-ttu-id="ddcd8-125">Uygulanan hello kuralları toobe istediğiniz emin toochange hello kuralı numara tooreflect hello sipariş olması.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-125">Be sure toochange hello rule number Order tooreflect hello order in which you want hello rules toobe applied.</span></span> <span data-ttu-id="ddcd8-126">Merhaba alt kural numarası daha büyük bir sayı hello önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-126">hello lower rule number takes precedence over hello higher number.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. <span data-ttu-id="ddcd8-127">Ardından, yeni bir uç noktası (Ekle) oluşturmak veya mevcut bir uç noktası (küme) için ACL hello ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-127">Next, you can either create a new endpoint (Add) or set hello ACL for an existing endpoint (Set).</span></span> <span data-ttu-id="ddcd8-128">Bu örnekte, yeni bir sanal makine uç noktası güncelleştirmesi ile "web" Merhaba sanal makine uç noktası ile Merhaba ACL ayarları adlı ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-128">In this example, we will add a new virtual machine endpoint called "web" and update hello virtual machine endpoint with hello ACL settings.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. <span data-ttu-id="ddcd8-129">Ardından, hello cmdlet'leri birleştirmek ve hello komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-129">Next, combine hello cmdlets and run hello script.</span></span> <span data-ttu-id="ddcd8-130">Bu örnekte, hello birleşik cmdlet'leri şöyle olabilir:</span><span class="sxs-lookup"><span data-stu-id="ddcd8-130">For this example, hello combined cmdlets would look like this:</span></span>
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a><span data-ttu-id="ddcd8-131">Uzak bir alt ağdan erişimi veren bir ağ ACL kuralını Kaldır</span><span class="sxs-lookup"><span data-stu-id="ddcd8-131">Remove a Network ACL rule that permits access from a remote subnet</span></span>
<span data-ttu-id="ddcd8-132">Merhaba örneği aşağıdaki şekilde tooremove ağ ACL kuralı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-132">hello example below illustrates a way tooremove a network ACL rule.</span></span>  <span data-ttu-id="ddcd8-133">tooremove izin ile ağ ACL kuralı için bir uzak alt ağ, kuralları bir Azure PowerShell ISE açın.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-133">tooremove a Network ACL rule with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="ddcd8-134">Kopyalama ve aşağıda kendi değerlerinizle hello komut dosyasını yapılandırarak hello betiğini yapıştırın ve hello betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-134">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="ddcd8-135">Tooget hello ağ ACL nesne hello sanal makine uç noktası için ilk adımdır.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-135">First step is tooget hello Network ACL object for hello virtual machine endpoint.</span></span> <span data-ttu-id="ddcd8-136">Ardından hello ACL kuralı kaldırırsınız.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-136">You'll then remove hello ACL rule.</span></span> <span data-ttu-id="ddcd8-137">Bu durumda, biz bu kural kimliğine göre kaldırıyorsunuz</span><span class="sxs-lookup"><span data-stu-id="ddcd8-137">In this case, we are removing it by rule ID.</span></span> <span data-ttu-id="ddcd8-138">Bu gibi durumlarda bu hello kural kimliği 0 yalnızca hello ACL ' kaldırır.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-138">This will only remove hello rule ID 0 from hello ACL.</span></span> <span data-ttu-id="ddcd8-139">Merhaba ACL nesne hello sanal makine uç noktasından kaldırmaz.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-139">It does not remove hello ACL object from hello virtual machine endpoint.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. <span data-ttu-id="ddcd8-140">Ardından, hello ağ ACL nesne toohello sanal makine uç noktası uygulamak ve hello sanal makine güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-140">Next, you must apply hello Network ACL object toohello virtual machine endpoint and update hello virtual machine.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a><span data-ttu-id="ddcd8-141">Bir sanal makine uç noktasından bir ağ ACL Kaldır</span><span class="sxs-lookup"><span data-stu-id="ddcd8-141">Remove a Network ACL from a virtual machine endpoint</span></span>
<span data-ttu-id="ddcd8-142">Bazı senaryolarda, bir sanal makine uç noktası bir ağ ACL nesneden tooremove isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-142">In certain scenarios, you might want tooremove a Network ACL object from a virtual machine endpoint.</span></span> <span data-ttu-id="ddcd8-143">bir Azure PowerShell ISE açın, toodo.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-143">toodo that, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="ddcd8-144">Kopyalama ve aşağıda kendi değerlerinizle hello komut dosyasını yapılandırarak hello betiğini yapıştırın ve hello betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ddcd8-144">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="ddcd8-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ddcd8-145">Next steps</span></span>
[<span data-ttu-id="ddcd8-146">Bir ağ erişim denetimi listesi (ACL) nedir?</span><span class="sxs-lookup"><span data-stu-id="ddcd8-146">What is a Network Access Control List (ACL)?</span></span>](virtual-networks-acl.md)

