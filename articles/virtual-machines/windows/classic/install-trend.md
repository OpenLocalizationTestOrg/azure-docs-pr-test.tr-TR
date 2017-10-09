---
title: "aaaInstall eğilim mikro derin güvenlik bir VM'de | Microsoft Docs"
description: "Bu makalede nasıl tooinstall ve eğilim mikro güvenlik Azure hello Klasik dağıtım modelinde oluşturulan VM yapılandırın."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a><span data-ttu-id="7c50e-103">Nasıl tooinstall ve bir Windows VM bir hizmet olarak eğilimi mikro derin güvenliği yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7c50e-103">How tooinstall and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7c50e-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7c50e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7c50e-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="7c50e-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="7c50e-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="7c50e-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="7c50e-107">Bu makale size nasıl gösterir tooinstall ve eğilim mikro derin güvenlik bir yeni veya var olan Windows Server çalıştıran sanal makine (VM) bir hizmet olarak yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7c50e-107">This article shows you how tooinstall and configure Trend Micro Deep Security as a Service on a new or existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="7c50e-108">Bir hizmet olarak derin güvenlik kötü amaçlı yazılımdan koruma, bir güvenlik duvarı, bir yetkisiz erişim önleme sisteminin ve bütünlüğü izleme içerir.</span><span class="sxs-lookup"><span data-stu-id="7c50e-108">Deep Security as a Service includes anti-malware protection, a firewall, an intrusion prevention system, and integrity monitoring.</span></span>

<span data-ttu-id="7c50e-109">Merhaba istemcisi bir güvenlik uzantısı hello VM Aracısı aracılığıyla olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="7c50e-109">hello client is installed as a security extension via hello VM Agent.</span></span> <span data-ttu-id="7c50e-110">Yeni bir sanal makine üzerinde VM Aracısı'hello Azure portal tarafından otomatik olarak oluşturulan hello olarak hello derin güvenlik aracısı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="7c50e-110">On a new virtual machine, you install hello Deep Security Agent, as hello VM Agent is created automatically by hello Azure portal.</span></span>

<span data-ttu-id="7c50e-111">Mevcut bir VM'yi Hello Klasik portal, hello Azure CLI veya PowerShell kullanılarak oluşturulan VM Aracısı sahip olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="7c50e-111">An existing VM created using hello classic portal, hello Azure CLI, or PowerShell might not have a VM agent.</span></span> <span data-ttu-id="7c50e-112">Merhaba VM aracısı yüklü olmayan mevcut sanal makineyi için toodownload gerekir ve ilk yükleyin.</span><span class="sxs-lookup"><span data-stu-id="7c50e-112">For an existing virtual machine that doesn't have hello VM Agent, you need toodownload and install it first.</span></span> <span data-ttu-id="7c50e-113">Bu makalede her iki durumlarda kapsar.</span><span class="sxs-lookup"><span data-stu-id="7c50e-113">This article covers both situations.</span></span>

<span data-ttu-id="7c50e-114">Geçerli bir eğilim mikro abonelikten bir şirket içi çözüm varsa, kullanabilirsiniz toohelp Azure sanal makinelerinizi koruma.</span><span class="sxs-lookup"><span data-stu-id="7c50e-114">If you have a current subscription from Trend Micro for an on-premises solution, you can use it toohelp protect your Azure virtual machines.</span></span> <span data-ttu-id="7c50e-115">Bir müşteri henüz değilseniz, deneme aboneliği için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c50e-115">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="7c50e-116">Bu çözüm hakkında daha fazla bilgi için bkz: hello eğilimi mikro blog gönderisi [Microsoft Azure VM Aracısı uzantısı için ayrıntılı güvenlik](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span><span class="sxs-lookup"><span data-stu-id="7c50e-116">For more information about this solution, see hello Trend Micro blog post [Microsoft Azure VM Agent Extension For Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span></span>

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a><span data-ttu-id="7c50e-117">Merhaba derin güvenlik aracısı yeni bir VM'e yükleyin</span><span class="sxs-lookup"><span data-stu-id="7c50e-117">Install hello Deep Security Agent on a new VM</span></span>

<span data-ttu-id="7c50e-118">Merhaba [Azure portal](http://portal.azure.com) , hello görüntüden kullandığınızda hello eğilimi mikro güvenlik uzantısı yüklemenize olanak tanıyan **Market** toocreate hello sanal makine.</span><span class="sxs-lookup"><span data-stu-id="7c50e-118">hello [Azure portal](http://portal.azure.com) lets you install hello Trend Micro security extension when you use an image from hello **Marketplace** toocreate hello virtual machine.</span></span> <span data-ttu-id="7c50e-119">Tek bir sanal makine oluşturuyorsanız, hello portal eğilimi mikro kolay bir yolu tooadd korumadan kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="7c50e-119">If you're creating a single virtual machine, using hello portal is an easy way tooadd protection from Trend Micro.</span></span>

<span data-ttu-id="7c50e-120">Bir giriş hello kullanarak **Market** yardımcı olan bir Sihirbazı'nı Ayarla hello sanal makineyi açar.</span><span class="sxs-lookup"><span data-stu-id="7c50e-120">Using an entry from hello **Marketplace** opens a wizard that helps you set up hello virtual machine.</span></span> <span data-ttu-id="7c50e-121">Merhaba kullandığınız **ayarları** dikey penceresinde, hello üçüncü Pano hello sihirbazının tooinstall hello eğilimi mikro güvenlik uzantısı.</span><span class="sxs-lookup"><span data-stu-id="7c50e-121">You use hello **Settings** blade, hello third panel of hello wizard, tooinstall hello Trend Micro security extension.</span></span>  <span data-ttu-id="7c50e-122">Genel yönergeler için bkz: [Windows hello Azure portalı çalıştıran bir sanal makine oluşturma](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="7c50e-122">For general instructions, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>

<span data-ttu-id="7c50e-123">Toohello ulaştıklarında **ayarları** dikey penceresinde hello Sihirbazı, adımları hello:</span><span class="sxs-lookup"><span data-stu-id="7c50e-123">When you get toohello **Settings** blade of hello wizard, do hello following steps:</span></span>

1. <span data-ttu-id="7c50e-124">Tıklatın **uzantıları**, ardından **uzantısı Ekle** hello sonraki bölmesinde.</span><span class="sxs-lookup"><span data-stu-id="7c50e-124">Click **Extensions**, then click **Add extension** in hello next pane.</span></span>

   ![Merhaba uzantı eklemeye başlayın][1]

2. <span data-ttu-id="7c50e-126">Seçin **derin güvenlik aracısı** hello içinde **yeni kaynak** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="7c50e-126">Select **Deep Security Agent** in hello **New resource** pane.</span></span> <span data-ttu-id="7c50e-127">Merhaba derin güvenlik aracısı bölmesinde **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="7c50e-127">In hello Deep Security Agent pane, click **Create**.</span></span>

   ![Derin güvenlik aracısı tanımlama][2]

3. <span data-ttu-id="7c50e-129">Merhaba girin **Kiracı tanımlayıcı** ve **Kiracı etkinleştirme parola** hello uzantısı.</span><span class="sxs-lookup"><span data-stu-id="7c50e-129">Enter hello **Tenant Identifier** and **Tenant Activation Password** for hello extension.</span></span> <span data-ttu-id="7c50e-130">İsteğe bağlı olarak, girebilirsiniz bir **güvenlik ilkesi tanımlayıcısı**.</span><span class="sxs-lookup"><span data-stu-id="7c50e-130">Optionally, you can enter a **Security Policy Identifier**.</span></span> <span data-ttu-id="7c50e-131">Ardından **Tamam** tooadd hello istemci.</span><span class="sxs-lookup"><span data-stu-id="7c50e-131">Then, click **OK** tooadd hello client.</span></span>

   ![Uzantı ayrıntılarını sağlayın][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a><span data-ttu-id="7c50e-133">Var olan bir VM Hello derin güvenlik Aracısı yükleme</span><span class="sxs-lookup"><span data-stu-id="7c50e-133">Install hello Deep Security Agent on an existing VM</span></span>
<span data-ttu-id="7c50e-134">Mevcut bir VM'yi tooinstall hello aracısını, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7c50e-134">tooinstall hello agent on an existing VM, you need hello following items:</span></span>

* <span data-ttu-id="7c50e-135">Hello Azure PowerShell modülü, sürüm 0.8.2 veya daha yeni, yerel bilgisayarınızda yüklü.</span><span class="sxs-lookup"><span data-stu-id="7c50e-135">hello Azure PowerShell module, version 0.8.2 or newer, installed on your local computer.</span></span> <span data-ttu-id="7c50e-136">Hello kullanarak yüklediyseniz Azure PowerShell hello sürümü kontrol edebilirsiniz **Get-Module azure | Tablo Biçimlendir sürüm** komutu.</span><span class="sxs-lookup"><span data-stu-id="7c50e-136">You can check hello version of Azure PowerShell that you have installed by using hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="7c50e-137">Yönergeler ve bir bağlantı toohello en son sürüm için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7c50e-137">For instructions and a link toohello latest version, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="7c50e-138">Azure aboneliği tooyour kullanarak oturum `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="7c50e-138">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="7c50e-139">Merhaba VM Aracısı hello hedef sanal makinede yüklü.</span><span class="sxs-lookup"><span data-stu-id="7c50e-139">hello VM Agent installed on hello target virtual machine.</span></span>

<span data-ttu-id="7c50e-140">İlk olarak, VM aracısının yüklü olduğundan bu hello doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7c50e-140">First, verify that hello VM Agent is already installed.</span></span> <span data-ttu-id="7c50e-141">Merhaba bulut hizmeti adı ve sanal makine adı girin ve ardından komutlar bir yönetici düzeyi Azure PowerShell komut isteminde aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7c50e-141">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="7c50e-142">Merhaba < ve > karakterleri dahil olmak üzere hello tırnak içindeki her şeyi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7c50e-142">Replace everything within hello quotes, including hello < and > characters.</span></span>

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

<span data-ttu-id="7c50e-143">Merhaba bulut hizmeti ve sanal makine adını bilmiyorsanız, çalıştırmak **Get-AzureVM** bilgiyi tüm geçerli aboneliğinizde sanal makineler hello toodisplay.</span><span class="sxs-lookup"><span data-stu-id="7c50e-143">If you don't know hello cloud service and virtual machine name, run **Get-AzureVM** toodisplay that information for all hello virtual machines in your current subscription.</span></span>

<span data-ttu-id="7c50e-144">Merhaba, **write-host** komutu döndürür **doğru**, VM aracısının yüklü hello.</span><span class="sxs-lookup"><span data-stu-id="7c50e-144">If hello **write-host** command returns **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="7c50e-145">Döndürürse **False**, hello yönergeler ve hello Azure blog gönderisi indirme bağlantısı toohello bkz [VM aracısı ve uzantılar - 2. parça](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span><span class="sxs-lookup"><span data-stu-id="7c50e-145">If it returns **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span></span>

<span data-ttu-id="7c50e-146">Merhaba VM Aracısı yüklüyse, bu komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7c50e-146">If hello VM Agent is installed, run these commands.</span></span>

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="7c50e-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7c50e-147">Next steps</span></span>
<span data-ttu-id="7c50e-148">Merhaba Aracısı toostart yüklendiğinde çalıştıran birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="7c50e-148">It takes a few minutes for hello agent toostart running when it is installed.</span></span> <span data-ttu-id="7c50e-149">Derin bir güvenlik yöneticisi tarafından yönetilecek şekilde bundan sonra hello sanal makine üzerinde derin güvenlik tooactivate gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c50e-149">After that, you need tooactivate Deep Security on hello virtual machine so it can be managed by a Deep Security Manager.</span></span> <span data-ttu-id="7c50e-150">Merhaba makaleler ek yönergeler için bkz:</span><span class="sxs-lookup"><span data-stu-id="7c50e-150">See hello following articles for additional instructions:</span></span>

* <span data-ttu-id="7c50e-151">Bu çözümle ilgili eğilim'ın makale [Instant-On Cloud Security Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span><span class="sxs-lookup"><span data-stu-id="7c50e-151">Trend's article about this solution, [Instant-On Cloud Security for Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span></span>
* <span data-ttu-id="7c50e-152">A [örnek Windows PowerShell komut dosyası](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure hello sanal makine</span><span class="sxs-lookup"><span data-stu-id="7c50e-152">A [sample Windows PowerShell script](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure hello virtual machine</span></span>
* <span data-ttu-id="7c50e-153">[Yönergeler](http://go.microsoft.com/fwlink/?LinkId=404099) hello örnek</span><span class="sxs-lookup"><span data-stu-id="7c50e-153">[Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) for hello sample</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7c50e-154">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7c50e-154">Additional resources</span></span>
<span data-ttu-id="7c50e-155">[Nasıl tooa sanal makineye Windows Server çalıştıran toolog]</span><span class="sxs-lookup"><span data-stu-id="7c50e-155">[How toolog on tooa virtual machine running Windows Server]</span></span>

<span data-ttu-id="7c50e-156">[Azure VM uzantıları ve özellikleri]</span><span class="sxs-lookup"><span data-stu-id="7c50e-156">[Azure VM Extensions and features]</span></span>

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[Nasıl tooa sanal makineye Windows Server çalıştıran toolog]:connect-logon.md
[Azure VM uzantıları ve özellikleri]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
