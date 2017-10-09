---
title: "aaaInstall Azure Windows VM üzerinde Symantec Endpoint Protection | Microsoft Docs"
description: "Bilgi nasıl tooinstall hello Symantec Endpoint Protection güvenlik uzantısı yeni yapılandırma ve mevcut Azure VM hello Klasik dağıtım modeliyle oluşturulan."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: iainfou
ms.openlocfilehash: cb6083366185c26c9f43ff94d835cd90725de5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a><span data-ttu-id="34372-103">Nasıl tooinstall ve Symantec Endpoint Protection bir Windows VM yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34372-103">How tooinstall and configure Symantec Endpoint Protection on a Windows VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="34372-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="34372-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="34372-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="34372-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="34372-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="34372-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="34372-107">Bu makale size nasıl gösterir tooinstall hello Symantec Endpoint Protection istemci ve var olan sanal Windows Server çalıştıran bir makineyi (VM) yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="34372-107">This article shows you how tooinstall and configure hello Symantec Endpoint Protection client on an existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="34372-108">Bu tam istemci virüs ve casus yazılımdan koruma, güvenlik duvarı ve izinsiz giriş önleme gibi hizmetleri içerir.</span><span class="sxs-lookup"><span data-stu-id="34372-108">This full client includes services such as virus and spyware protection, firewall, and intrusion prevention.</span></span> <span data-ttu-id="34372-109">Merhaba istemci hello VM Aracısı'nı kullanarak bir güvenlik uzantısı olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="34372-109">hello client is installed as a security extension by using hello VM Agent.</span></span>

<span data-ttu-id="34372-110">Symantec'ten bir şirket içi çözüm için mevcut bir aboneliğiniz varsa, tooprotect kullanabilirsiniz, Azure sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="34372-110">If you have an existing subscription from Symantec for an on-premises solution, you can use it tooprotect your Azure virtual machines.</span></span> <span data-ttu-id="34372-111">Bir müşteri henüz değilseniz, deneme aboneliği için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34372-111">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="34372-112">Bu çözüm hakkında daha fazla bilgi için bkz: [Symantec Endpoint Protection Microsoft'un Azure platformunda][Symantec].</span><span class="sxs-lookup"><span data-stu-id="34372-112">For more information about this solution, see [Symantec Endpoint Protection on Microsoft's Azure platform][Symantec].</span></span> <span data-ttu-id="34372-113">Bu sayfa ayrıca bağlantı toolicensing bilgileri ve Symantec müşteri zaten iseniz hello istemcisini yüklemeye yönelik yönergeleri sahiptir.</span><span class="sxs-lookup"><span data-stu-id="34372-113">This page also has links toolicensing information and instructions for installing hello client if you're already a Symantec customer.</span></span>

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a><span data-ttu-id="34372-114">Var olan bir VM Symantec Endpoint Protection yükle</span><span class="sxs-lookup"><span data-stu-id="34372-114">Install Symantec Endpoint Protection on an existing VM</span></span>
<span data-ttu-id="34372-115">Başlamadan önce hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="34372-115">Before you begin, you need hello following:</span></span>

* <span data-ttu-id="34372-116">Hello Azure PowerShell modülü, sürüm 0.8.2 veya daha sonra iş bilgisayarınızın.</span><span class="sxs-lookup"><span data-stu-id="34372-116">hello Azure PowerShell module, version 0.8.2 or later, on your work computer.</span></span> <span data-ttu-id="34372-117">Merhaba ile yüklediğiniz Azure PowerShell hello sürümü kontrol edebilirsiniz **Get-Module azure | Tablo Biçimlendir sürüm** komutu.</span><span class="sxs-lookup"><span data-stu-id="34372-117">You can check hello version of Azure PowerShell that you have installed with hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="34372-118">Yönergeler ve bir bağlantı toohello en son sürüm için bkz: [nasıl tooInstall ve yapılandırma Azure PowerShell][PS].</span><span class="sxs-lookup"><span data-stu-id="34372-118">For instructions and a link toohello latest version, see [How tooInstall and Configure Azure PowerShell][PS].</span></span> <span data-ttu-id="34372-119">Azure aboneliği tooyour kullanarak oturum `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="34372-119">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="34372-120">Merhaba VM üzerinde çalışan Aracısı hello Azure sanal makine.</span><span class="sxs-lookup"><span data-stu-id="34372-120">hello VM Agent running on hello Azure Virtual Machine.</span></span>

<span data-ttu-id="34372-121">İlk olarak, VM aracısının hello sanal makinede zaten yüklü olduğundan bu hello doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="34372-121">First, verify that hello VM Agent is already installed on hello virtual machine.</span></span> <span data-ttu-id="34372-122">Merhaba bulut hizmeti adı ve sanal makine adı girin ve ardından komutlar bir yönetici düzeyi Azure PowerShell komut isteminde aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="34372-122">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="34372-123">Merhaba < ve > karakterleri dahil olmak üzere hello tırnak içindeki her şeyi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="34372-123">Replace everything within hello quotes, including hello < and > characters.</span></span>

> [!TIP]
> <span data-ttu-id="34372-124">Merhaba bulut hizmeti ve sanal makine adları bilmiyorsanız, çalıştırmak **Get-AzureVM** toolist hello adları geçerli aboneliğinizde tüm sanal makineler için.</span><span class="sxs-lookup"><span data-stu-id="34372-124">If you don't know hello cloud service and virtual machine names, run **Get-AzureVM** toolist hello names for all virtual machines in your current subscription.</span></span>

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="34372-125">Merhaba, **write-host** komutu görüntüler **doğru**, VM aracısının yüklü hello.</span><span class="sxs-lookup"><span data-stu-id="34372-125">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="34372-126">Bunu görüntülerse **False**, hello yönergeler ve hello Azure blog gönderisi indirme bağlantısı toohello bkz [VM aracısı ve uzantılar - 2. parça][Agent].</span><span class="sxs-lookup"><span data-stu-id="34372-126">If it displays **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2][Agent].</span></span>

<span data-ttu-id="34372-127">Merhaba VM Aracısı yüklüyse, bu komutları tooinstall hello Symantec Endpoint Protection Aracısı'nı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="34372-127">If hello VM Agent is installed, run these commands tooinstall hello Symantec Endpoint Protection agent.</span></span>

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

<span data-ttu-id="34372-128">Symantec güvenlik uzantısı hello tooverify yüklü ve güncel durumda:</span><span class="sxs-lookup"><span data-stu-id="34372-128">tooverify that hello Symantec security extension has been installed and is up-to-date:</span></span>

1. <span data-ttu-id="34372-129">Toohello sanal makinede oturum açın.</span><span class="sxs-lookup"><span data-stu-id="34372-129">Log on toohello virtual machine.</span></span> <span data-ttu-id="34372-130">Yönergeler için bkz: [nasıl tooa sanal makine çalıştıran Windows Server üzerinde tooLog][Logon].</span><span class="sxs-lookup"><span data-stu-id="34372-130">For instructions, see [How tooLog on tooa Virtual Machine Running Windows Server][Logon].</span></span>
2. <span data-ttu-id="34372-131">Windows Server 2008 R2 için tıklatın **Başlat > Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="34372-131">For Windows Server 2008 R2, click **Start > Symantec Endpoint Protection**.</span></span> <span data-ttu-id="34372-132">Windows Server 2012 veya hello başlangıç ekranından Windows Server 2012 R2 için yazın **Symantec**ve ardından **Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="34372-132">For Windows Server 2012 or Windows Server 2012 R2, from hello start screen, type **Symantec**, and then click **Symantec Endpoint Protection**.</span></span>
3. <span data-ttu-id="34372-133">Merhaba gelen **durum** hello sekmesinde **durum Symantec Endpoint Protection** penceresinde, güncelleştirmeleri uygulamak veya gerektiğinde yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="34372-133">From hello **Status** tab of hello **Status-Symantec Endpoint Protection** window, apply updates or restart if needed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="34372-134">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="34372-134">Additional resources</span></span>
<span data-ttu-id="34372-135">[Nasıl tooLog tooa sanal makine çalıştıran Windows Server üzerinde][Logon]</span><span class="sxs-lookup"><span data-stu-id="34372-135">[How tooLog on tooa Virtual Machine Running Windows Server][Logon]</span></span>

<span data-ttu-id="34372-136">[Azure VM uzantıları ve özellikleri][Ext]</span><span class="sxs-lookup"><span data-stu-id="34372-136">[Azure VM Extensions and Features][Ext]</span></span>

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
