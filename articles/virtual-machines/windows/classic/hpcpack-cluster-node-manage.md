---
title: "işlem düğümleri aaaManage HPC Pack kümesi | Microsoft Docs"
description: "PowerShell komut dosyası araçları tooadd, Kaldır, başlangıç hakkında bilgi edinin ve HPC Pack 2012 R2 küme işlem düğümlerine Azure Durdur"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 5ac1142cc5da984020779434fbb7cba5ad7c14bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="73457-103">Merhaba numarası ve Azure HPC Pack kümede işlem düğümlerine kullanılabilirliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="73457-103">Manage hello number and availability of compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="73457-104">Azure Vm'lerinde bir HPC Pack 2012 R2 kümesi oluşturduysanız, küme düğümü Vm'lerde tooeasily ekleyin, kaldırın, (sağlayamaz) Başlat veya (deprovision) bazı Durdur yolları işlem isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73457-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways tooeasily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span></span> <span data-ttu-id="73457-105">Bu görevleri toodo hello baş düğümünde VM yüklü olan Azure PowerShell komut dosyalarını çalıştır.</span><span class="sxs-lookup"><span data-stu-id="73457-105">toodo these tasks, run Azure PowerShell scripts that are installed on hello head node VM.</span></span> <span data-ttu-id="73457-106">Bu maliyetleri denetimi hello numarası ve HPC paketi küme kaynaklarınızın kullanılabilirliğini denetlemenize yardımcı olur komutlar.</span><span class="sxs-lookup"><span data-stu-id="73457-106">These scripts help you control hello number and availability of your HPC Pack cluster resources so you can control costs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="73457-107">Bu makale yalnızca tooHPC Pack 2012 R2 kümeleri hello Klasik dağıtım modeli kullanılarak oluşturulmuş Azure içinde geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="73457-107">This article applies only tooHPC Pack 2012 R2 clusters in Azure created using hello classic deployment model.</span></span> <span data-ttu-id="73457-108">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="73457-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="73457-109">Ayrıca, bu makalede açıklanan hello PowerShell betikleri HPC Pack 2016'da kullanılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="73457-109">In addition, hello PowerShell scripts described in this article are not available in HPC Pack 2016.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73457-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="73457-110">Prerequisites</span></span>
* <span data-ttu-id="73457-111">**Azure VM'de HPC Pack 2012 R2 küme**: hello Klasik dağıtım modelinde bir HPC Pack 2012 R2 kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="73457-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in hello classic deployment model.</span></span> <span data-ttu-id="73457-112">Örneğin, hello dağıtım hello Azure Marketi hello HPC Pack 2012 R2 VM görüntüsünde ve bir Azure PowerShell komut dosyası kullanarak otomatikleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73457-112">For example, you can automate hello deployment by using hello HPC Pack 2012 R2 VM image in hello Azure Marketplace and an Azure PowerShell script.</span></span> <span data-ttu-id="73457-113">Bilgi ve Önkoşullar için bkz: [hello HPC Pack Iaas dağıtım betiği ile bir HPC kümesi oluşturma](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="73457-113">For information and prerequisites, see [Create an HPC Cluster with hello HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span></span>
  
    <span data-ttu-id="73457-114">Dağıtımdan sonra hello düğümü yönetim komut dosyaları hello % CCP bulur\_giriş % bin klasörü hello baş düğüm üzerinde.</span><span class="sxs-lookup"><span data-stu-id="73457-114">After deployment, find hello node management scripts in hello %CCP\_HOME%bin folder on hello head node.</span></span> <span data-ttu-id="73457-115">Her hello komut dosyalarının, yönetici olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="73457-115">Run each of hello scripts as an administrator.</span></span>
* <span data-ttu-id="73457-116">**Azure yayımlama ayarları dosyası veya yönetim sertifikası**: toodo hello aşağıdakilerden birini hello baş düğümünde gerekir:</span><span class="sxs-lookup"><span data-stu-id="73457-116">**Azure publish settings file or management certificate**: You need toodo one of hello following on hello head node:</span></span>
  
  * <span data-ttu-id="73457-117">**İçeri aktarma hello Azure yayımlama ayarları dosyası**.</span><span class="sxs-lookup"><span data-stu-id="73457-117">**Import hello Azure publish settings file**.</span></span> <span data-ttu-id="73457-118">toodo hello baş düğümünde Azure PowerShell cmdlet'lerini aşağıdaki Bu, çalışma hello:</span><span class="sxs-lookup"><span data-stu-id="73457-118">toodo this, run hello following Azure PowerShell cmdlets on hello head node:</span></span>
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * <span data-ttu-id="73457-119">**Merhaba baş düğümünde Hello Azure yönetim sertifikası yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="73457-119">**Configure hello Azure management certificate on hello head node**.</span></span> <span data-ttu-id="73457-120">Merhaba .cer dosyanız varsa, hello CurrentUser\My sertifika deposuna içeri aktarın ve ardından Azure ortamınıza (AzureCloud veya AzureChinaCloud) için Azure PowerShell cmdlet'i aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="73457-120">If you have hello .cer file, import it in hello CurrentUser\My certificate store and then run hello following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span></span>
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a><span data-ttu-id="73457-121">İşlem düğümü sanal makineleri ekleyin</span><span class="sxs-lookup"><span data-stu-id="73457-121">Add compute node VMs</span></span>
<span data-ttu-id="73457-122">İşlem düğümleri hello ile ekleme **Ekle HpcIaaSNode.ps1** komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="73457-122">Add compute nodes with hello **Add-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="73457-123">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="73457-123">Syntax</span></span>
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a><span data-ttu-id="73457-124">Parametreler</span><span class="sxs-lookup"><span data-stu-id="73457-124">Parameters</span></span>
* <span data-ttu-id="73457-125">**ServiceName**: yeni düğümü VM'ler işlem hello bulut hizmeti adını eklenir.</span><span class="sxs-lookup"><span data-stu-id="73457-125">**ServiceName**: Name of hello cloud service that new compute node VMs are added to.</span></span>
* <span data-ttu-id="73457-126">**Görüntü adı**: hello Azure Klasik portalında veya Azure PowerShell cmdlet'i aracılığıyla alınabilir Azure VM görüntü adı **Get-AzureVMImage**.</span><span class="sxs-lookup"><span data-stu-id="73457-126">**ImageName**: Azure VM image name, which can be obtained through hello Azure classic portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span></span> <span data-ttu-id="73457-127">Hello görüntü hello aşağıdaki gereksinimleri karşılamalıdır:</span><span class="sxs-lookup"><span data-stu-id="73457-127">hello image must meet hello following requirements:</span></span>
  
  1. <span data-ttu-id="73457-128">Bir Windows işletim sistemi yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="73457-128">A Windows operating system must be installed.</span></span>
  2. <span data-ttu-id="73457-129">HPC Pack Merhaba bilgi işlem düğümü rolü yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="73457-129">HPC Pack must be installed in hello compute node role.</span></span>
  3. <span data-ttu-id="73457-130">Merhaba görüntü hello kullanıcı kategorisi, ortak bir Azure VM görüntüsü değil, özel bir görüntü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="73457-130">hello image must be a private image in hello User category, not a public Azure VM image.</span></span>
* <span data-ttu-id="73457-131">**Miktar**: işlem düğümü VM'ler toobe eklenen sayısı.</span><span class="sxs-lookup"><span data-stu-id="73457-131">**Quantity**: Number of compute node VMs toobe added.</span></span>
* <span data-ttu-id="73457-132">**InstanceSize**: hello boyutunu işlem düğümü VM'ler.</span><span class="sxs-lookup"><span data-stu-id="73457-132">**InstanceSize**: Size of hello compute node VMs.</span></span>
* <span data-ttu-id="73457-133">**DomainUserName**: kullanılan toojoin hello yeni VM'ler toohello etki alanında etki alanı kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="73457-133">**DomainUserName**: Domain user name, which is used toojoin hello new VMs toohello domain.</span></span>
* <span data-ttu-id="73457-134">**DomainUserPassword**: hello etki alanı kullanıcı parolası.</span><span class="sxs-lookup"><span data-stu-id="73457-134">**DomainUserPassword**: Password of hello domain user.</span></span>
* <span data-ttu-id="73457-135">**NodeNameSeries** (isteğe bağlı): deseni Merhaba işlem düğümleri adlandırma.</span><span class="sxs-lookup"><span data-stu-id="73457-135">**NodeNameSeries** (optional): Naming pattern for hello compute nodes.</span></span> <span data-ttu-id="73457-136">Merhaba biçiminde olmalıdır &lt; *kök\_adı*&gt;&lt;*Başlat\_numarası*&gt;%.</span><span class="sxs-lookup"><span data-stu-id="73457-136">hello format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span></span> <span data-ttu-id="73457-137">Örneğin, MyCN11 başlangıç düğümü adlarını MyCN % %10 anlamına gelir hello bir dizi işlem.</span><span class="sxs-lookup"><span data-stu-id="73457-137">For example, MyCN%10% means a series of hello compute node names starting from MyCN11.</span></span> <span data-ttu-id="73457-138">Belirtilmezse, hello komut dosyası kullanan hello düğümü adlandırma serisi hello HPC kümede yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="73457-138">If not specified, hello script uses hello configured node naming series in hello HPC cluster.</span></span>

### <a name="example"></a><span data-ttu-id="73457-139">Örnek</span><span class="sxs-lookup"><span data-stu-id="73457-139">Example</span></span>
<span data-ttu-id="73457-140">Merhaba aşağıdaki örnek 20 boyutu büyük işlem düğümü VM'ler hello bulut hizmetinde, *hpcservice1*bağlı hello VM görüntüsü olarak *hpccnimage1*.</span><span class="sxs-lookup"><span data-stu-id="73457-140">hello following example adds 20 size Large compute node VMs in hello cloud service *hpcservice1*, based on hello VM image *hpccnimage1*.</span></span>

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a><span data-ttu-id="73457-141">İşlem düğümü VM'ler Kaldır</span><span class="sxs-lookup"><span data-stu-id="73457-141">Remove compute node VMs</span></span>
<span data-ttu-id="73457-142">İşlem düğümleri hello ile Kaldır **Kaldır HpcIaaSNode.ps1** komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="73457-142">Remove compute nodes with hello **Remove-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="73457-143">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="73457-143">Syntax</span></span>
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="73457-144">Parametreler</span><span class="sxs-lookup"><span data-stu-id="73457-144">Parameters</span></span>
* <span data-ttu-id="73457-145">**Ad**: küme düğümleri toobe adlarını kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="73457-145">**Name**: Names of cluster nodes toobe removed.</span></span> <span data-ttu-id="73457-146">Joker karakterleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="73457-146">Wildcards are supported.</span></span> <span data-ttu-id="73457-147">Merhaba parametre kümesi adı adıdır.</span><span class="sxs-lookup"><span data-stu-id="73457-147">hello parameter set name is Name.</span></span> <span data-ttu-id="73457-148">Her iki hello belirtemezsiniz **adı** ve **düğümü** parametreleri.</span><span class="sxs-lookup"><span data-stu-id="73457-148">You can't specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="73457-149">**Düğüm**: hello HPC PowerShell cmdlet'i alınabilir hello HpcNode nesne kaldırılmış hello düğümleri toobe için [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="73457-149">**Node**: hello HpcNode object for hello nodes toobe removed, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="73457-150">Merhaba parametre kümesi adı düğümdür.</span><span class="sxs-lookup"><span data-stu-id="73457-150">hello parameter set name is Node.</span></span> <span data-ttu-id="73457-151">Her iki hello belirtemezsiniz **adı** ve **düğümü** parametreleri.</span><span class="sxs-lookup"><span data-stu-id="73457-151">You can't specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="73457-152">**DeleteVHD** (isteğe bağlı): toodelete ilişkili hello diskler hello kaldırılır VM'ler için ayarlama.</span><span class="sxs-lookup"><span data-stu-id="73457-152">**DeleteVHD** (optional): Setting toodelete hello associated disks for hello VMs that are removed.</span></span>
* <span data-ttu-id="73457-153">**Zorla** (isteğe bağlı): kaldırmadan önce çevrimdışı HPC düğümleri tooforce ayarlama.</span><span class="sxs-lookup"><span data-stu-id="73457-153">**Force** (optional): Setting tooforce HPC nodes offline before removing them.</span></span>
* <span data-ttu-id="73457-154">**Onayla** (isteğe bağlı): hello komutu çalıştırmadan önce onaylamanız için komut istemi.</span><span class="sxs-lookup"><span data-stu-id="73457-154">**Confirm** (optional): Prompt for confirmation before executing hello command.</span></span>
* <span data-ttu-id="73457-155">**WhatIf**: toodescribe ne ayarı durum hello komutu çalıştırmadan hello komut yürütülürse.</span><span class="sxs-lookup"><span data-stu-id="73457-155">**WhatIf**: Setting toodescribe what would happen if you executed hello command without actually executing hello command.</span></span>

### <a name="example"></a><span data-ttu-id="73457-156">Örnek</span><span class="sxs-lookup"><span data-stu-id="73457-156">Example</span></span>
<span data-ttu-id="73457-157">Merhaba aşağıdaki örnek çevrimdışı hello düğümleri başlayan adlarla zorlar *HPCNode-CN -* hello düğümler ve bunların ilişkili diskler kaldırır.</span><span class="sxs-lookup"><span data-stu-id="73457-157">hello following example forces offline hello nodes with names beginning *HPCNode-CN-* and them removes hello nodes and their associated disks.</span></span>

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a><span data-ttu-id="73457-158">İşlem düğümü sanal makineleri Başlat</span><span class="sxs-lookup"><span data-stu-id="73457-158">Start compute node VMs</span></span>
<span data-ttu-id="73457-159">Başlangıç işlem düğümlerini hello ile **başlangıç HpcIaaSNode.ps1** komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="73457-159">Start compute nodes with hello **Start-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="73457-160">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="73457-160">Syntax</span></span>
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="73457-161">Parametreler</span><span class="sxs-lookup"><span data-stu-id="73457-161">Parameters</span></span>
* <span data-ttu-id="73457-162">**Ad**: hello küme düğümleri toobe adlarını başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="73457-162">**Name**: Names of hello cluster nodes toobe started.</span></span> <span data-ttu-id="73457-163">Joker karakterleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="73457-163">Wildcards are supported.</span></span> <span data-ttu-id="73457-164">Merhaba parametre kümesi adı adıdır.</span><span class="sxs-lookup"><span data-stu-id="73457-164">hello parameter set name is Name.</span></span> <span data-ttu-id="73457-165">Her iki hello belirtemezsiniz **adı** ve **düğümü** parametreleri.</span><span class="sxs-lookup"><span data-stu-id="73457-165">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="73457-166">**Düğüm**-hello HPC PowerShell cmdlet'i alınabilir hello HpcNode nesne hello düğümleri toobe başlamak için [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="73457-166">**Node**- hello HpcNode object for hello nodes toobe started, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="73457-167">Merhaba parametre kümesi adı düğümdür.</span><span class="sxs-lookup"><span data-stu-id="73457-167">hello parameter set name is Node.</span></span> <span data-ttu-id="73457-168">Her iki hello belirtemezsiniz **adı** ve **düğümü** parametreleri.</span><span class="sxs-lookup"><span data-stu-id="73457-168">You cannot specify both hello **Name** and **Node** parameters.</span></span>

### <a name="example"></a><span data-ttu-id="73457-169">Örnek</span><span class="sxs-lookup"><span data-stu-id="73457-169">Example</span></span>
<span data-ttu-id="73457-170">Merhaba aşağıdaki örnek düğümleri başlayan adlarla başlatır *HPCNode-CN -*.</span><span class="sxs-lookup"><span data-stu-id="73457-170">hello following example starts nodes with names beginning *HPCNode-CN-*.</span></span>

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a><span data-ttu-id="73457-171">İşlem düğümü VM'ler Durdur</span><span class="sxs-lookup"><span data-stu-id="73457-171">Stop compute node VMs</span></span>
<span data-ttu-id="73457-172">İşlem düğümleri hello ile Durdur **Stop-HpcIaaSNode.ps1** komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="73457-172">Stop compute nodes with hello **Stop-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="73457-173">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="73457-173">Syntax</span></span>
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="73457-174">Parametreler</span><span class="sxs-lookup"><span data-stu-id="73457-174">Parameters</span></span>
* <span data-ttu-id="73457-175">**Ad**-hello küme düğümleri toobe adlarını durduruldu.</span><span class="sxs-lookup"><span data-stu-id="73457-175">**Name**- Names of hello cluster nodes toobe stopped.</span></span> <span data-ttu-id="73457-176">Joker karakterleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="73457-176">Wildcards are supported.</span></span> <span data-ttu-id="73457-177">Merhaba parametre kümesi adı adıdır.</span><span class="sxs-lookup"><span data-stu-id="73457-177">hello parameter set name is Name.</span></span> <span data-ttu-id="73457-178">Her iki hello belirtemezsiniz **adı** ve **düğümü** parametreleri.</span><span class="sxs-lookup"><span data-stu-id="73457-178">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="73457-179">**Düğüm**: hello HPC PowerShell cmdlet'i alınabilir hello HpcNode nesne durduruldu, hello düğümleri toobe için [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="73457-179">**Node**: hello HpcNode object for hello nodes toobe stopped, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="73457-180">Merhaba parametre kümesi adı düğümdür.</span><span class="sxs-lookup"><span data-stu-id="73457-180">hello parameter set name is Node.</span></span> <span data-ttu-id="73457-181">Her iki hello belirtemezsiniz **adı** ve **düğümü** parametreleri.</span><span class="sxs-lookup"><span data-stu-id="73457-181">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="73457-182">**Zorla** (isteğe bağlı): durdurmadan önce çevrimdışı HPC düğümleri tooforce ayarlama.</span><span class="sxs-lookup"><span data-stu-id="73457-182">**Force** (optional): Setting tooforce HPC nodes offline before stopping them.</span></span>

### <a name="example"></a><span data-ttu-id="73457-183">Örnek</span><span class="sxs-lookup"><span data-stu-id="73457-183">Example</span></span>
<span data-ttu-id="73457-184">Merhaba aşağıdaki örnek çevrimdışı düğümleri başlayan adlarla zorlar *HPCNode-CN -* ve ardından düğümler durakları hello.</span><span class="sxs-lookup"><span data-stu-id="73457-184">hello following example forces offline nodes with names beginning *HPCNode-CN-* and then stops hello nodes.</span></span>

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a><span data-ttu-id="73457-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="73457-185">Next steps</span></span>
* <span data-ttu-id="73457-186">tooautomatically arttıkça ya da küçültmek hello küme düğümleri, işler ve görevleri hello kümede hello geçerli iş yükü göre bkz: [otomatik olarak Büyüt ve Küçült Azure according toohello küme iş yükühelloHPCpaketikümekaynaklarında](hpcpack-cluster-node-autogrowshrink.md).</span><span class="sxs-lookup"><span data-stu-id="73457-186">tooautomatically grow or shrink hello cluster nodes according to hello current workload of jobs and tasks on hello cluster, see [Automatically grow and shrink hello HPC Pack cluster resources in Azure according toohello cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span></span>

