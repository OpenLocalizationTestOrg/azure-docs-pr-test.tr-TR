---
title: "aaaAzure sanal makine Aracısı genel bakış | Microsoft Docs"
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
ms.openlocfilehash: 178766925673419cd661dbb460b8427bbfaf54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="cb1bc-103">Azure sanal makine aracısını genel bakış</span><span class="sxs-lookup"><span data-stu-id="cb1bc-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="cb1bc-104">Merhaba Microsoft Azure sanal makine Aracısı (VM Aracısı) hello Azure yapı denetleyicisi VM etkileşim yöneten güvenli ve basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-104">hello Microsoft Azure Virtual Machine Agent (VM Agent) is a secured, lightweight process that manages VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="cb1bc-105">Merhaba VM Aracısı etkinleştirme ve Azure sanal makine uzantıları yürütme birincil bir rolü var.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-105">hello VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="cb1bc-106">VM uzantıları etkinleştirme, yükleme ve yazılım yapılandırma gibi sanal makine dağıtım yapılandırması gönderin.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="cb1bc-107">Sanal makine uzantıları gibi bir sanal makinenin hello yönetici parolasını sıfırlama kurtarma özellikleri de sağlar.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-107">Virtual machine extensions also enable recovery features such as resetting hello administrative password of a virtual machine.</span></span> <span data-ttu-id="cb1bc-108">Azure VM Aracısı Hello, sanal makine uzantıları çalıştırılamaz.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-108">Without hello Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="cb1bc-109">Bu belge yükleme, algılama ve hello Azure sanal makine Aracısı kaldırılmasını ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-109">This document details installation, detection, and removal of hello Azure Virtual Machine Agent.</span></span>

## <a name="install-hello-vm-agent"></a><span data-ttu-id="cb1bc-110">Merhaba VM Aracısı yükleme</span><span class="sxs-lookup"><span data-stu-id="cb1bc-110">Install hello VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="cb1bc-111">Azure galeri görüntüsü</span><span class="sxs-lookup"><span data-stu-id="cb1bc-111">Azure gallery image</span></span>

<span data-ttu-id="cb1bc-112">Hello Azure VM Aracısı, Azure Galerisi görüntüden dağıtılmış tüm Windows sanal makine üzerinde varsayılan olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-112">hello Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="cb1bc-113">Azure galerisinde görüntüden hello Portal, PowerShell, komut satırı arabirimini veya bir Azure Resource Manager şablonu dağıtırken de Azure VM Aracısı olduğunu hello yüklenmesi.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-113">When deploying an Azure gallery image from hello Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, hello Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="cb1bc-114">El ile yükleme</span><span class="sxs-lookup"><span data-stu-id="cb1bc-114">Manual installation</span></span>

<span data-ttu-id="cb1bc-115">Merhaba Windows VM Aracısı el ile bir Windows Installer paketi kullanılarak yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-115">hello Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="cb1bc-116">Bir özel sanal makine görüntüsü oluşturma Azure'da dağıtılacak zaman el ile yükleme gerekli olabilir.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="cb1bc-117">toomanually yükleme hello Windows VM Aracısı, bu konumdan hello VM Aracısı yükleyicisi karşıdan [Windows Azure VM Aracısı indirme](http://go.microsoft.com/fwlink/?LinkID=394789).</span><span class="sxs-lookup"><span data-stu-id="cb1bc-117">toomanually install hello Windows VM Agent, download hello VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="cb1bc-118">Merhaba VM Aracısı hello windows Installer dosyasını çift tıklatarak yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-118">hello VM Agent can be installed by double-clicking hello windows installer file.</span></span> <span data-ttu-id="cb1bc-119">Bir otomatik olarak veya katılımsız yükleme hello VM Aracısı'nın için komutu aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-119">For an automated or unattended installation of hello VM agent, run hello following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a><span data-ttu-id="cb1bc-120">Merhaba VM Aracısı Algıla</span><span class="sxs-lookup"><span data-stu-id="cb1bc-120">Detect hello VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="cb1bc-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb1bc-121">PowerShell</span></span>

<span data-ttu-id="cb1bc-122">Hello Azure Resource Manager PowerShell modülü kullanılan tooretrieve bilgiler hakkında Azure sanal makineler olabilir.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-122">hello Azure Resource Manager PowerShell module can be used tooretrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="cb1bc-123">Çalışan `Get-AzureRmVM` oldukça biraz sağlama durumu hello Azure VM aracısı için hello bilgilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-123">Running `Get-AzureRmVM` returns quite a bit of information including hello provisioning state for hello Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="cb1bc-124">Merhaba yalnızca bir alt kümesini hello aşağıdadır `Get-AzureRmVM` çıktı.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-124">hello following is just a subset of hello `Get-AzureRmVM` output.</span></span> <span data-ttu-id="cb1bc-125">Bildirim hello `ProvisionVMAgent` içe özelliği içinde `OSProfile`, bu özellik, dağıtılan toohello sanal makine hello VM Aracısı yüklediyse kullanılan toodetermine olabilir.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-125">Notice hello `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used toodetermine if hello VM agent has been deployed toohello virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="cb1bc-126">komut dosyası izleyen hello kullanılan tooreturn sanal makine adları ve hello VM Aracısı hello durumunu kısa listesini olabilir.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-126">hello following script can be used tooreturn a concise list of virtual machine names and hello state of hello VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="cb1bc-127">El ile algılama</span><span class="sxs-lookup"><span data-stu-id="cb1bc-127">Manual Detection</span></span>

<span data-ttu-id="cb1bc-128">Tooa Windows Azure VM oturum açıldığında, Görev Yöneticisi'ni çalışan işlemlerin kullanılan tooexamine olabilir.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-128">When logged in tooa Windows Azure VM, task manager can be used tooexamine running processes.</span></span> <span data-ttu-id="cb1bc-129">toocheck hello Azure VM aracısı için Görev Yöneticisi'ni açın > merhaba Ayrıntılar sekmesini tıklatın ve bir işlem adı arayın `WindowsAzureGuestAgent.exe`.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-129">toocheck for hello Azure VM Agent, open Task Manager > click hello details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="cb1bc-130">Bu işlemin Hello varlığı bu hello VM aracısının yüklü olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-130">hello presence of this process indicates that hello VM agent is installed.</span></span>

## <a name="upgrade-hello-vm-agent"></a><span data-ttu-id="cb1bc-131">Yükseltme hello VM Aracısı</span><span class="sxs-lookup"><span data-stu-id="cb1bc-131">Upgrade hello VM Agent</span></span>

<span data-ttu-id="cb1bc-132">Hello Azure VM Aracısı Windows'için otomatik olarak yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-132">hello Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="cb1bc-133">Yeni sanal makineler dağıtılan tooAzure olduğu gibi hello son VM Aracısı alırlar.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-133">As new virtual machines are deployed tooAzure, they receive hello latest VM agent.</span></span> <span data-ttu-id="cb1bc-134">Özel VM görüntüleri manuel olarak güncelleştirilen tooinclude hello yeni VM Aracısı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cb1bc-134">Custom VM images should be manually updated tooinclude hello new VM agent.</span></span>
