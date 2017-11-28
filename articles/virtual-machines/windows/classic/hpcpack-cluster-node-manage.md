---
title: "HPC Pack küme bilgi işlem düğümleri yönetme | Microsoft Docs"
description: "Ekle, Kaldır, başlatmak ve HPC Pack 2012 R2 küme işlem düğümlerine Azure durdurmak için PowerShell komut dosyası araçları hakkında bilgi edinin"
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
ms.openlocfilehash: dc9f354191b9e80ff6a01bd401a874c6998bda79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-the-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="b66fa-103">Azure’da bir HPC Pack kümesindeki işlem düğümlerinin sayısını ve kullanılabilirliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="b66fa-103">Manage the number and availability of compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="b66fa-104">Azure Vm'lerinde bir HPC Pack 2012 R2 kümesi oluşturduysanız, kolayca eklemek, kaldırmak, (sağlayamaz) Başlat veya Durdur (deprovision) yolları isteyebilirsiniz bazı kümedeki düğüm Vm'lerle işlem.</span><span class="sxs-lookup"><span data-stu-id="b66fa-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways to easily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span></span> <span data-ttu-id="b66fa-105">Bu görevleri gerçekleştirmek için VM baş düğümünde yüklü olan Azure PowerShell betikleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b66fa-105">To do these tasks, run Azure PowerShell scripts that are installed on the head node VM.</span></span> <span data-ttu-id="b66fa-106">Bu komut dosyaları sayısı ve HPC paketi küme kaynaklarınızın kullanılabilirliğini maliyetleri denetimi denetlemenize yardımcı.</span><span class="sxs-lookup"><span data-stu-id="b66fa-106">These scripts help you control the number and availability of your HPC Pack cluster resources so you can control costs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="b66fa-107">Bu makale, yalnızca Azure Klasik dağıtım modeli kullanılarak oluşturulan kümelerde HPC Pack 2012 R2 için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b66fa-107">This article applies only to HPC Pack 2012 R2 clusters in Azure created using the classic deployment model.</span></span> <span data-ttu-id="b66fa-108">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="b66fa-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> <span data-ttu-id="b66fa-109">Ayrıca, bu makalede açıklanan PowerShell betikleri HPC Pack 2016'da kullanılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="b66fa-109">In addition, the PowerShell scripts described in this article are not available in HPC Pack 2016.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b66fa-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b66fa-110">Prerequisites</span></span>
* <span data-ttu-id="b66fa-111">**Azure VM'de HPC Pack 2012 R2 küme**: Klasik dağıtım modelinde bir HPC Pack 2012 R2 kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b66fa-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in the classic deployment model.</span></span> <span data-ttu-id="b66fa-112">Örneğin, Azure Marketi ve bir Azure PowerShell Betiği HPC Pack 2012 R2 VM görüntüsünü kullanarak dağıtım otomatikleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b66fa-112">For example, you can automate the deployment by using the HPC Pack 2012 R2 VM image in the Azure Marketplace and an Azure PowerShell script.</span></span> <span data-ttu-id="b66fa-113">Bilgi ve Önkoşullar için bkz: [HPC Kümesi ile HPC Pack Iaas dağıtım komut dosyası oluşturma](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="b66fa-113">For information and prerequisites, see [Create an HPC Cluster with the HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span></span>
  
    <span data-ttu-id="b66fa-114">Dağıtımdan sonra düğümü yönetim komut dosyaları % CCP bulun\_giriş % bin klasörü baş düğüm.</span><span class="sxs-lookup"><span data-stu-id="b66fa-114">After deployment, find the node management scripts in the %CCP\_HOME%bin folder on the head node.</span></span> <span data-ttu-id="b66fa-115">Her komut dosyalarının, yönetici olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b66fa-115">Run each of the scripts as an administrator.</span></span>
* <span data-ttu-id="b66fa-116">**Azure yayımlama ayarları dosyası veya yönetim sertifikası**: baş düğüm aşağıdakilerden birini yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="b66fa-116">**Azure publish settings file or management certificate**: You need to do one of the following on the head node:</span></span>
  
  * <span data-ttu-id="b66fa-117">**Yayımlama ayarları dosyasını içeri aktar Azure**.</span><span class="sxs-lookup"><span data-stu-id="b66fa-117">**Import the Azure publish settings file**.</span></span> <span data-ttu-id="b66fa-118">Bunu yapmak için baş düğümünde aşağıdaki Azure PowerShell cmdlet'lerini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b66fa-118">To do this, run the following Azure PowerShell cmdlets on the head node:</span></span>
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * <span data-ttu-id="b66fa-119">**Azure yönetim sertifikası baş düğümünde yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="b66fa-119">**Configure the Azure management certificate on the head node**.</span></span> <span data-ttu-id="b66fa-120">.Cer dosyanız varsa, CurrentUser\My sertifika deposuna içeri aktarın ve ardından Azure ortamınıza (AzureCloud veya AzureChinaCloud) için aşağıdaki Azure PowerShell cmdlet'ini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b66fa-120">If you have the .cer file, import it in the CurrentUser\My certificate store and then run the following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span></span>
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a><span data-ttu-id="b66fa-121">İşlem düğümü sanal makineleri ekleyin</span><span class="sxs-lookup"><span data-stu-id="b66fa-121">Add compute node VMs</span></span>
<span data-ttu-id="b66fa-122">İşlem düğümleri eklemek **Ekle HpcIaaSNode.ps1** komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="b66fa-122">Add compute nodes with the **Add-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="b66fa-123">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="b66fa-123">Syntax</span></span>
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a><span data-ttu-id="b66fa-124">Parametreler</span><span class="sxs-lookup"><span data-stu-id="b66fa-124">Parameters</span></span>
* <span data-ttu-id="b66fa-125">**ServiceName**: yeni düğümü VM'ler işlem bulut hizmeti adını eklenir.</span><span class="sxs-lookup"><span data-stu-id="b66fa-125">**ServiceName**: Name of the cloud service that new compute node VMs are added to.</span></span>
* <span data-ttu-id="b66fa-126">**Görüntü adı**: Klasik Azure portalında veya Azure PowerShell cmdlet'i aracılığıyla alınabilir Azure VM görüntü adı **Get-AzureVMImage**.</span><span class="sxs-lookup"><span data-stu-id="b66fa-126">**ImageName**: Azure VM image name, which can be obtained through the Azure classic portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span></span> <span data-ttu-id="b66fa-127">Görüntünün aşağıdaki gereksinimleri karşılamalıdır:</span><span class="sxs-lookup"><span data-stu-id="b66fa-127">The image must meet the following requirements:</span></span>
  
  1. <span data-ttu-id="b66fa-128">Bir Windows işletim sistemi yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="b66fa-128">A Windows operating system must be installed.</span></span>
  2. <span data-ttu-id="b66fa-129">HPC Pack ise bilgi işlem düğümü rolü yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b66fa-129">HPC Pack must be installed in the compute node role.</span></span>
  3. <span data-ttu-id="b66fa-130">Görüntüyü özel görüntü kullanıcı kategori, ortak bir Azure VM görüntüsü değil olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b66fa-130">The image must be a private image in the User category, not a public Azure VM image.</span></span>
* <span data-ttu-id="b66fa-131">**Miktar**: işlem düğümü sanal makinelerin eklenmesi sayısı.</span><span class="sxs-lookup"><span data-stu-id="b66fa-131">**Quantity**: Number of compute node VMs to be added.</span></span>
* <span data-ttu-id="b66fa-132">**InstanceSize**: işlem düğümü VM'ler boyutu.</span><span class="sxs-lookup"><span data-stu-id="b66fa-132">**InstanceSize**: Size of the compute node VMs.</span></span>
* <span data-ttu-id="b66fa-133">**DomainUserName**: yeni VM'ler etki alanına katılmak için kullanılan etki alanı kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="b66fa-133">**DomainUserName**: Domain user name, which is used to join the new VMs to the domain.</span></span>
* <span data-ttu-id="b66fa-134">**DomainUserPassword**: etki alanı kullanıcı parolası.</span><span class="sxs-lookup"><span data-stu-id="b66fa-134">**DomainUserPassword**: Password of the domain user.</span></span>
* <span data-ttu-id="b66fa-135">**NodeNameSeries** (isteğe bağlı): işlem düğümlerini için desen adlandırma.</span><span class="sxs-lookup"><span data-stu-id="b66fa-135">**NodeNameSeries** (optional): Naming pattern for the compute nodes.</span></span> <span data-ttu-id="b66fa-136">Biçimi olmalıdır &lt; *kök\_adı*&gt;&lt;*Başlat\_numarası*&gt;%.</span><span class="sxs-lookup"><span data-stu-id="b66fa-136">The format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span></span> <span data-ttu-id="b66fa-137">Örneğin, MyCN11 başlayan işlem düğümü adları dizi bir MyCN % %10 anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b66fa-137">For example, MyCN%10% means a series of the compute node names starting from MyCN11.</span></span> <span data-ttu-id="b66fa-138">Belirtilmezse, betik HPC küme serisinde adlandırma yapılandırılan düğüm kullanır.</span><span class="sxs-lookup"><span data-stu-id="b66fa-138">If not specified, the script uses the configured node naming series in the HPC cluster.</span></span>

### <a name="example"></a><span data-ttu-id="b66fa-139">Örnek</span><span class="sxs-lookup"><span data-stu-id="b66fa-139">Example</span></span>
<span data-ttu-id="b66fa-140">Aşağıdaki örnek, bulut hizmeti 20 boyutu büyük işlem düğümü VM'ler ekler *hpcservice1*bağlı olarak VM görüntüsü *hpccnimage1*.</span><span class="sxs-lookup"><span data-stu-id="b66fa-140">The following example adds 20 size Large compute node VMs in the cloud service *hpcservice1*, based on the VM image *hpccnimage1*.</span></span>

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a><span data-ttu-id="b66fa-141">İşlem düğümü VM'ler Kaldır</span><span class="sxs-lookup"><span data-stu-id="b66fa-141">Remove compute node VMs</span></span>
<span data-ttu-id="b66fa-142">İşlem düğümleri kaldırma **Kaldır HpcIaaSNode.ps1** komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="b66fa-142">Remove compute nodes with the **Remove-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="b66fa-143">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="b66fa-143">Syntax</span></span>
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="b66fa-144">Parametreler</span><span class="sxs-lookup"><span data-stu-id="b66fa-144">Parameters</span></span>
* <span data-ttu-id="b66fa-145">**Ad**: küme düğümlerinin adlarını kaldırılacak.</span><span class="sxs-lookup"><span data-stu-id="b66fa-145">**Name**: Names of cluster nodes to be removed.</span></span> <span data-ttu-id="b66fa-146">Joker karakterleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b66fa-146">Wildcards are supported.</span></span> <span data-ttu-id="b66fa-147">Parametre kümesi adı adıdır.</span><span class="sxs-lookup"><span data-stu-id="b66fa-147">The parameter set name is Name.</span></span> <span data-ttu-id="b66fa-148">Her ikisini birden belirtemezsiniz **adı** ve **düğümü** parametreleri.</span><span class="sxs-lookup"><span data-stu-id="b66fa-148">You can't specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="b66fa-149">**Düğüm**: HpcNode nesne HPC PowerShell cmdlet'i alınabilir kaldırılacak, düğümler için [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="b66fa-149">**Node**: The HpcNode object for the nodes to be removed, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="b66fa-150">Parametre kümesi adı düğümdür.</span><span class="sxs-lookup"><span data-stu-id="b66fa-150">The parameter set name is Node.</span></span> <span data-ttu-id="b66fa-151">Her ikisini birden belirtemezsiniz **adı** ve **düğümü** parametreleri.</span><span class="sxs-lookup"><span data-stu-id="b66fa-151">You can't specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="b66fa-152">**DeleteVHD** (isteğe bağlı): kaldırılır VM'ler için ilişkili diskler silmek için ayarı.</span><span class="sxs-lookup"><span data-stu-id="b66fa-152">**DeleteVHD** (optional): Setting to delete the associated disks for the VMs that are removed.</span></span>
* <span data-ttu-id="b66fa-153">**Zorla** (isteğe bağlı): kaldırmadan önce çevrimdışı HPC düğümleri zorlamak için ayarı.</span><span class="sxs-lookup"><span data-stu-id="b66fa-153">**Force** (optional): Setting to force HPC nodes offline before removing them.</span></span>
* <span data-ttu-id="b66fa-154">**Onayla** (isteğe bağlı): komutu çalıştırmadan önce onaylamanız için komut istemi.</span><span class="sxs-lookup"><span data-stu-id="b66fa-154">**Confirm** (optional): Prompt for confirmation before executing the command.</span></span>
* <span data-ttu-id="b66fa-155">**WhatIf**: komutu çalıştırmadan komut çalıştırıldığında ne olacağını açıklamak için ayarı.</span><span class="sxs-lookup"><span data-stu-id="b66fa-155">**WhatIf**: Setting to describe what would happen if you executed the command without actually executing the command.</span></span>

### <a name="example"></a><span data-ttu-id="b66fa-156">Örnek</span><span class="sxs-lookup"><span data-stu-id="b66fa-156">Example</span></span>
<span data-ttu-id="b66fa-157">Aşağıdaki örnek düğümleri başlayan adlarla çevrimdışı zorlar *HPCNode-CN -* düğümleri ve bunların ilişkili diskler kaldırır.</span><span class="sxs-lookup"><span data-stu-id="b66fa-157">The following example forces offline the nodes with names beginning *HPCNode-CN-* and them removes the nodes and their associated disks.</span></span>

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a><span data-ttu-id="b66fa-158">İşlem düğümü sanal makineleri Başlat</span><span class="sxs-lookup"><span data-stu-id="b66fa-158">Start compute node VMs</span></span>
<span data-ttu-id="b66fa-159">Başlangıç işlem düğümleriyle **başlangıç HpcIaaSNode.ps1** komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="b66fa-159">Start compute nodes with the **Start-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="b66fa-160">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="b66fa-160">Syntax</span></span>
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="b66fa-161">Parametreler</span><span class="sxs-lookup"><span data-stu-id="b66fa-161">Parameters</span></span>
* <span data-ttu-id="b66fa-162">**Ad**: küme düğümlerinin adlarını başlatılacak.</span><span class="sxs-lookup"><span data-stu-id="b66fa-162">**Name**: Names of the cluster nodes to be started.</span></span> <span data-ttu-id="b66fa-163">Joker karakterleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b66fa-163">Wildcards are supported.</span></span> <span data-ttu-id="b66fa-164">Parametre kümesi adı adıdır.</span><span class="sxs-lookup"><span data-stu-id="b66fa-164">The parameter set name is Name.</span></span> <span data-ttu-id="b66fa-165">Her ikisini birden belirtemezsiniz **adı** ve **düğümü** parametreleri.</span><span class="sxs-lookup"><span data-stu-id="b66fa-165">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="b66fa-166">**Düğüm**-HpcNode nesne HPC PowerShell cmdlet'i alınabilir başlatılacak düğümler için [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="b66fa-166">**Node**- The HpcNode object for the nodes to be started, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="b66fa-167">Parametre kümesi adı düğümdür.</span><span class="sxs-lookup"><span data-stu-id="b66fa-167">The parameter set name is Node.</span></span> <span data-ttu-id="b66fa-168">Her ikisini birden belirtemezsiniz **adı** ve **düğümü** parametreleri.</span><span class="sxs-lookup"><span data-stu-id="b66fa-168">You cannot specify both the **Name** and **Node** parameters.</span></span>

### <a name="example"></a><span data-ttu-id="b66fa-169">Örnek</span><span class="sxs-lookup"><span data-stu-id="b66fa-169">Example</span></span>
<span data-ttu-id="b66fa-170">Aşağıdaki örnek düğümleri başlayan adlarla başlatır *HPCNode-CN -*.</span><span class="sxs-lookup"><span data-stu-id="b66fa-170">The following example starts nodes with names beginning *HPCNode-CN-*.</span></span>

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a><span data-ttu-id="b66fa-171">İşlem düğümü VM'ler Durdur</span><span class="sxs-lookup"><span data-stu-id="b66fa-171">Stop compute node VMs</span></span>
<span data-ttu-id="b66fa-172">İşlem düğümleriyle Durdur **Stop-HpcIaaSNode.ps1** komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="b66fa-172">Stop compute nodes with the **Stop-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="b66fa-173">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="b66fa-173">Syntax</span></span>
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="b66fa-174">Parametreler</span><span class="sxs-lookup"><span data-stu-id="b66fa-174">Parameters</span></span>
* <span data-ttu-id="b66fa-175">**Ad**-durdurulacak küme düğümlerinin adlarını.</span><span class="sxs-lookup"><span data-stu-id="b66fa-175">**Name**- Names of the cluster nodes to be stopped.</span></span> <span data-ttu-id="b66fa-176">Joker karakterleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b66fa-176">Wildcards are supported.</span></span> <span data-ttu-id="b66fa-177">Parametre kümesi adı adıdır.</span><span class="sxs-lookup"><span data-stu-id="b66fa-177">The parameter set name is Name.</span></span> <span data-ttu-id="b66fa-178">Her ikisini birden belirtemezsiniz **adı** ve **düğümü** parametreleri.</span><span class="sxs-lookup"><span data-stu-id="b66fa-178">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="b66fa-179">**Düğüm**: HpcNode nesne HPC PowerShell cmdlet'i alınabilir durdurulacak düğümler için [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="b66fa-179">**Node**: The HpcNode object for the nodes to be stopped, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="b66fa-180">Parametre kümesi adı düğümdür.</span><span class="sxs-lookup"><span data-stu-id="b66fa-180">The parameter set name is Node.</span></span> <span data-ttu-id="b66fa-181">Her ikisini birden belirtemezsiniz **adı** ve **düğümü** parametreleri.</span><span class="sxs-lookup"><span data-stu-id="b66fa-181">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="b66fa-182">**Zorla** (isteğe bağlı): durdurmadan önce çevrimdışı HPC düğümleri zorlamak için ayarı.</span><span class="sxs-lookup"><span data-stu-id="b66fa-182">**Force** (optional): Setting to force HPC nodes offline before stopping them.</span></span>

### <a name="example"></a><span data-ttu-id="b66fa-183">Örnek</span><span class="sxs-lookup"><span data-stu-id="b66fa-183">Example</span></span>
<span data-ttu-id="b66fa-184">Aşağıdaki örnek çevrimdışı düğümleri başlayan adlarla zorlar *HPCNode-CN -* ve ardından düğümler durdurur.</span><span class="sxs-lookup"><span data-stu-id="b66fa-184">The following example forces offline nodes with names beginning *HPCNode-CN-* and then stops the nodes.</span></span>

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a><span data-ttu-id="b66fa-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b66fa-185">Next steps</span></span>
* <span data-ttu-id="b66fa-186">Otomatik olarak büyütür veya küme düğümleri, işler ve görevleri küme üzerinde geçerli iş yükü göre daraltmak için bkz: [otomatik olarak Büyüt ve Azure HPC paketi küme kaynaklarında göre küme iş yükü küçültme](hpcpack-cluster-node-autogrowshrink.md).</span><span class="sxs-lookup"><span data-stu-id="b66fa-186">To automatically grow or shrink the cluster nodes according to the current workload of jobs and tasks on the cluster, see [Automatically grow and shrink the HPC Pack cluster resources in Azure according to the cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span></span>

