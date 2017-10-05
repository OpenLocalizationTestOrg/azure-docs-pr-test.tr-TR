---
title: "Azure sanal makine Aracısı genel bakış | Microsoft Docs"
description: "Azure sanal makine Aracısı genel bakış"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: nepeters
ms.openlocfilehash: accfd5f0fec69175e584528ff9f6db66402cb89e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="bf4a6-103">Azure sanal makine aracısını genel bakış</span><span class="sxs-lookup"><span data-stu-id="bf4a6-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="bf4a6-104">Microsoft Azure sanal makine Aracısı (VM Aracısı) Azure yapı denetleyicisi VM etkileşim yöneten güvenli ve basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-104">The Microsoft Azure Virtual Machine Agent (VM Agent) is a secured, lightweight process that manages VM interaction with the Azure Fabric Controller.</span></span> <span data-ttu-id="bf4a6-105">VM Aracısı'nı etkinleştirme ve Azure sanal makine uzantıları yürütme birincil bir rolü var.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-105">The VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="bf4a6-106">VM uzantıları etkinleştirme, yükleme ve yazılım yapılandırma gibi sanal makine dağıtım yapılandırması gönderin.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="bf4a6-107">Sanal makine uzantıları gibi bir sanal makine yönetici parolasını sıfırlama kurtarma özellikleri de sağlar.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-107">Virtual machine extensions also enable recovery features such as resetting the administrative password of a virtual machine.</span></span> <span data-ttu-id="bf4a6-108">Azure VM Aracısı sanal makine uzantıları çalıştırılamaz.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-108">Without the Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="bf4a6-109">Bu belge yükleme, algılama ve kaldırma Azure sanal makine Aracısı'nın ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-109">This document details installation, detection, and removal of the Azure Virtual Machine Agent.</span></span>

## <a name="install-the-vm-agent"></a><span data-ttu-id="bf4a6-110">VM Aracısı yükleme</span><span class="sxs-lookup"><span data-stu-id="bf4a6-110">Install the VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="bf4a6-111">Azure galeri görüntüsü</span><span class="sxs-lookup"><span data-stu-id="bf4a6-111">Azure gallery image</span></span>

<span data-ttu-id="bf4a6-112">Azure VM Aracısı, Azure Galerisi görüntüden dağıtılmış tüm Windows sanal makine üzerinde varsayılan olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-112">The Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="bf4a6-113">Azure galerisinde görüntüden Portal, PowerShell, komut satırı arabirimini veya bir Azure Resource Manager şablonu dağıtırken Azure VM aracısı olan de yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-113">When deploying an Azure gallery image from the Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, the Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="bf4a6-114">El ile yükleme</span><span class="sxs-lookup"><span data-stu-id="bf4a6-114">Manual installation</span></span>

<span data-ttu-id="bf4a6-115">Windows VM Aracısı'nı el ile bir Windows Installer paketi kullanılarak yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-115">The Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="bf4a6-116">Bir özel sanal makine görüntüsü oluşturma Azure'da dağıtılacak zaman el ile yükleme gerekli olabilir.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="bf4a6-117">Windows VM Aracısı'nı el ile yüklemek için bu konumdan VM aracı yükleyicisini indirin [Windows Azure VM Aracısı indirme](http://go.microsoft.com/fwlink/?LinkID=394789).</span><span class="sxs-lookup"><span data-stu-id="bf4a6-117">To manually install the Windows VM Agent, download the VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="bf4a6-118">VM Aracısı, windows Installer dosyasını çift tıklatarak yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-118">The VM Agent can be installed by double-clicking the windows installer file.</span></span> <span data-ttu-id="bf4a6-119">Bir otomatik olarak veya katılımsız yükleme VM Aracısı'nın için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-119">For an automated or unattended installation of the VM agent, run the following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-the-vm-agent"></a><span data-ttu-id="bf4a6-120">VM Aracısı Algıla</span><span class="sxs-lookup"><span data-stu-id="bf4a6-120">Detect the VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="bf4a6-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf4a6-121">PowerShell</span></span>

<span data-ttu-id="bf4a6-122">Azure Resource Manager PowerShell modülü, Azure sanal makineler hakkında bilgi almak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-122">The Azure Resource Manager PowerShell module can be used to retrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="bf4a6-123">Çalışan `Get-AzureRmVM` oldukça biraz Azure VM aracısı için sağlama durumu bilgilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-123">Running `Get-AzureRmVM` returns quite a bit of information including the provisioning state for the Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="bf4a6-124">Yalnızca bir alt kümesini aşağıdadır `Get-AzureRmVM` çıktı.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-124">The following is just a subset of the `Get-AzureRmVM` output.</span></span> <span data-ttu-id="bf4a6-125">Bildirim `ProvisionVMAgent` içe özelliği içinde `OSProfile`, bu özellik, VM Aracısı sanal makineye dağıtılıp dağıtılmadığını belirlemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-125">Notice the `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used to determine if the VM agent has been deployed to the virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="bf4a6-126">Aşağıdaki komut dosyası, sanal makine adları ve VM aracısının durumunu kısa listesini almak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-126">The following script can be used to return a concise list of virtual machine names and the state of the VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="bf4a6-127">El ile algılama</span><span class="sxs-lookup"><span data-stu-id="bf4a6-127">Manual Detection</span></span>

<span data-ttu-id="bf4a6-128">Bir Windows Azure VM oturum açıldığında, Görev Yöneticisi'ni çalışan işlemler incelemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-128">When logged in to a Windows Azure VM, task manager can be used to examine running processes.</span></span> <span data-ttu-id="bf4a6-129">Azure VM aracısı için denetlemek için Görev Yöneticisi'ni açın > Ayrıntılar sekmesini tıklatın ve bir işlem adı arayın `WindowsAzureGuestAgent.exe`.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-129">To check for the Azure VM Agent, open Task Manager > click the details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="bf4a6-130">VM aracısının yüklü olduğundan bu işlem varlığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-130">The presence of this process indicates that the VM agent is installed.</span></span>

## <a name="upgrade-the-vm-agent"></a><span data-ttu-id="bf4a6-131">VM Aracısı yükseltme</span><span class="sxs-lookup"><span data-stu-id="bf4a6-131">Upgrade the VM Agent</span></span>

<span data-ttu-id="bf4a6-132">Windows için Azure VM Aracısı otomatik olarak yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-132">The Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="bf4a6-133">Yeni sanal makineleri Azure'da dağıtılan gibi en son VM Aracısı alırlar.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-133">As new virtual machines are deployed to Azure, they receive the latest VM agent.</span></span> <span data-ttu-id="bf4a6-134">Özel VM görüntüleri el ile yeni VM Aracısı içerecek şekilde güncelleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="bf4a6-134">Custom VM images should be manually updated to include the new VM agent.</span></span>