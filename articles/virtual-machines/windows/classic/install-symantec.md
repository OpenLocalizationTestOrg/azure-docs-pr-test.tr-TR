---
title: "Windows Azure VM Symantec Endpoint Protection yükle | Microsoft Docs"
description: "Yükleme ve Symantec Endpoint Protection güvenlik uzantısı bir yeni veya var olan Azure Klasik dağıtım modeli kullanılarak oluşturulmuş VM'deki yapılandırın öğrenin."
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
ms.openlocfilehash: 1603ebc7ee3c29277f30fbb802bdd8205b92d648
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a><span data-ttu-id="f2c37-103">Bir Windows VM’de Symantec Uç Nokta Koruması yükleme ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f2c37-103">How to install and configure Symantec Endpoint Protection on a Windows VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="f2c37-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f2c37-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f2c37-105">Bu makalede, Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="f2c37-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="f2c37-106">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="f2c37-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="f2c37-107">Bu makalede yükleme ve Symantec Endpoint Protection istemcisini bir mevcut Windows Server çalıştıran sanal makine üzerinde (VM) yapılandırma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f2c37-107">This article shows you how to install and configure the Symantec Endpoint Protection client on an existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="f2c37-108">Bu tam istemci virüs ve casus yazılımdan koruma, güvenlik duvarı ve izinsiz giriş önleme gibi hizmetleri içerir.</span><span class="sxs-lookup"><span data-stu-id="f2c37-108">This full client includes services such as virus and spyware protection, firewall, and intrusion prevention.</span></span> <span data-ttu-id="f2c37-109">İstemci, VM Aracısı'nı kullanarak bir güvenlik uzantısı olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="f2c37-109">The client is installed as a security extension by using the VM Agent.</span></span>

<span data-ttu-id="f2c37-110">Symantec'ten bir şirket içi çözüm için mevcut bir aboneliğiniz varsa, Azure sanal makinelerinizi korumak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2c37-110">If you have an existing subscription from Symantec for an on-premises solution, you can use it to protect your Azure virtual machines.</span></span> <span data-ttu-id="f2c37-111">Bir müşteri henüz değilseniz, deneme aboneliği için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2c37-111">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="f2c37-112">Bu çözüm hakkında daha fazla bilgi için bkz: [Symantec Endpoint Protection Microsoft'un Azure platformunda][Symantec].</span><span class="sxs-lookup"><span data-stu-id="f2c37-112">For more information about this solution, see [Symantec Endpoint Protection on Microsoft's Azure platform][Symantec].</span></span> <span data-ttu-id="f2c37-113">Bu sayfa Ayrıca lisans bilgileri ve Symantec müşteri zaten iseniz istemcisini yüklemeye yönelik yönergeleri için bağlantıları vardır.</span><span class="sxs-lookup"><span data-stu-id="f2c37-113">This page also has links to licensing information and instructions for installing the client if you're already a Symantec customer.</span></span>

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a><span data-ttu-id="f2c37-114">Var olan bir VM Symantec Endpoint Protection yükle</span><span class="sxs-lookup"><span data-stu-id="f2c37-114">Install Symantec Endpoint Protection on an existing VM</span></span>
<span data-ttu-id="f2c37-115">Başlamadan önce aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="f2c37-115">Before you begin, you need the following:</span></span>

* <span data-ttu-id="f2c37-116">Azure PowerShell modülü, sürüm 0.8.2 veya daha sonra iş bilgisayarınızın.</span><span class="sxs-lookup"><span data-stu-id="f2c37-116">The Azure PowerShell module, version 0.8.2 or later, on your work computer.</span></span> <span data-ttu-id="f2c37-117">İle yüklenen Azure PowerShell sürümü kontrol edebilirsiniz **Get-Module azure | Tablo Biçimlendir sürüm** komutu.</span><span class="sxs-lookup"><span data-stu-id="f2c37-117">You can check the version of Azure PowerShell that you have installed with the **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="f2c37-118">Yönergeler ve en son sürüme bir bağlantı için bkz: [yükleme ve yapılandırma Azure PowerShell][PS].</span><span class="sxs-lookup"><span data-stu-id="f2c37-118">For instructions and a link to the latest version, see [How to Install and Configure Azure PowerShell][PS].</span></span> <span data-ttu-id="f2c37-119">Oturum açma kullanarak Azure aboneliği `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="f2c37-119">Log in to your Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="f2c37-120">Azure sanal makinede çalışan VM Aracısı.</span><span class="sxs-lookup"><span data-stu-id="f2c37-120">The VM Agent running on the Azure Virtual Machine.</span></span>

<span data-ttu-id="f2c37-121">İlk olarak, VM aracısının sanal makinede zaten yüklü olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f2c37-121">First, verify that the VM Agent is already installed on the virtual machine.</span></span> <span data-ttu-id="f2c37-122">Bulut hizmeti adı ve sanal makine adı girin ve ardından bir yönetici düzeyi Azure PowerShell komut isteminde aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f2c37-122">Fill in the cloud service name and virtual machine name, and then run the following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="f2c37-123">Dahil olmak üzere tırnak işaretleri içindeki her şeyi değiştirin < ve > karakterleri.</span><span class="sxs-lookup"><span data-stu-id="f2c37-123">Replace everything within the quotes, including the < and > characters.</span></span>

> [!TIP]
> <span data-ttu-id="f2c37-124">Sanal makine adları ve bulut hizmeti bilmiyorsanız, çalıştırmak **Get-AzureVM** geçerli aboneliğiniz tüm sanal makinelerin adlarını listelemek için.</span><span class="sxs-lookup"><span data-stu-id="f2c37-124">If you don't know the cloud service and virtual machine names, run **Get-AzureVM** to list the names for all virtual machines in your current subscription.</span></span>

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="f2c37-125">Varsa **write-host** komutu görüntüler **doğru**, VM aracısının yüklü olduğundan.</span><span class="sxs-lookup"><span data-stu-id="f2c37-125">If the **write-host** command displays **True**, the VM Agent is installed.</span></span> <span data-ttu-id="f2c37-126">Bunu görüntülerse **False**, yönergeler ve Azure blog postası karşıdan yükleme bağlantısı bkz [VM aracısı ve uzantılar - 2. parça][Agent].</span><span class="sxs-lookup"><span data-stu-id="f2c37-126">If it displays **False**, see the instructions and a link to the download in the Azure blog post [VM Agent and Extensions - Part 2][Agent].</span></span>

<span data-ttu-id="f2c37-127">VM Aracısı yüklüyse, Symantec Endpoint Protection aracısını yüklemek için şu komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f2c37-127">If the VM Agent is installed, run these commands to install the Symantec Endpoint Protection agent.</span></span>

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

<span data-ttu-id="f2c37-128">Symantec güvenlik uzantısı yüklendikten ve güncel durumda olduğunu doğrulamak için:</span><span class="sxs-lookup"><span data-stu-id="f2c37-128">To verify that the Symantec security extension has been installed and is up-to-date:</span></span>

1. <span data-ttu-id="f2c37-129">Sanal makinede oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f2c37-129">Log on to the virtual machine.</span></span> <span data-ttu-id="f2c37-130">Yönergeler için bkz: [nasıl bir sanal makine çalıştıran Windows Server oturum][Logon].</span><span class="sxs-lookup"><span data-stu-id="f2c37-130">For instructions, see [How to Log on to a Virtual Machine Running Windows Server][Logon].</span></span>
2. <span data-ttu-id="f2c37-131">Windows Server 2008 R2 için tıklatın **Başlat > Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="f2c37-131">For Windows Server 2008 R2, click **Start > Symantec Endpoint Protection**.</span></span> <span data-ttu-id="f2c37-132">Windows Server 2012 veya Windows Server 2012 R2, başlangıç ekranından yazın **Symantec**ve ardından **Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="f2c37-132">For Windows Server 2012 or Windows Server 2012 R2, from the start screen, type **Symantec**, and then click **Symantec Endpoint Protection**.</span></span>
3. <span data-ttu-id="f2c37-133">Gelen **durum** sekmesinde **durum Symantec Endpoint Protection** penceresinde, güncelleştirmeleri uygulamak veya gerektiğinde yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="f2c37-133">From the **Status** tab of the **Status-Symantec Endpoint Protection** window, apply updates or restart if needed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f2c37-134">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f2c37-134">Additional resources</span></span>
<span data-ttu-id="f2c37-135">[Nasıl yapılır Windows Server çalıştıran bir sanal makinede oturum açın][Logon]</span><span class="sxs-lookup"><span data-stu-id="f2c37-135">[How to Log on to a Virtual Machine Running Windows Server][Logon]</span></span>

<span data-ttu-id="f2c37-136">[Azure VM uzantıları ve özellikleri][Ext]</span><span class="sxs-lookup"><span data-stu-id="f2c37-136">[Azure VM Extensions and Features][Ext]</span></span>

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
