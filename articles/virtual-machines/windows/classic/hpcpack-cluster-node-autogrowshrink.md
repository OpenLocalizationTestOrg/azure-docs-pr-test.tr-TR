---
title: "Otomatik ölçeklendirme HPC paketi küme düğümleri | Microsoft Docs"
description: "Otomatik olarak Büyüt ve azure'da HPC paketi küme işlem düğümü sayısını Daralt"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0dc0d15c64d8951c3c457df73588c37418a3c8a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="automatically-grow-and-shrink-the-hpc-pack-cluster-resources-in-azure-according-to-the-cluster-workload"></a><span data-ttu-id="7cd19-103">Otomatik olarak Büyüt ve Azure HPC paketi küme kaynaklarında göre küme iş yükü küçültme</span><span class="sxs-lookup"><span data-stu-id="7cd19-103">Automatically grow and shrink the HPC Pack cluster resources in Azure according to the cluster workload</span></span>
<span data-ttu-id="7cd19-104">HPC Pack kümenizdeki Azure "veri bloğu" düğümlerini dağıtmak ya da Azure Vm'lerde bir HPC paketi küme oluşturmak, bir şekilde otomatik olarak büyütür veya küme kaynaklarını düğümleri veya çekirdek küme iş yüküne göre gibi küçültmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7cd19-104">If you deploy Azure “burst” nodes in your HPC Pack cluster, or you create an HPC Pack cluster in Azure VMs, you may want a way to automatically grow or shrink the cluster resources such as nodes or cores according to the workload on the cluster.</span></span> <span data-ttu-id="7cd19-105">Bu şekilde küme kaynaklarını ölçeklendirme, Azure kaynaklarınızı daha verimli şekilde kullanabilir ve bunların maliyetlerini denetlemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="7cd19-105">Scaling the cluster resources in this way allows you to use your Azure resources more efficiently and control their costs.</span></span>

<span data-ttu-id="7cd19-106">Bu makalede, HPC Pack sağlayan iki otomatik ölçeklendirme yolları işlem kaynaklarını gösterir:</span><span class="sxs-lookup"><span data-stu-id="7cd19-106">This article shows you two ways that HPC Pack provides to autoscale compute resources:</span></span>

* <span data-ttu-id="7cd19-107">HPC Pack küme özelliği **AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="7cd19-107">The HPC Pack cluster property **AutoGrowShrink**</span></span>

* <span data-ttu-id="7cd19-108">**AzureAutoGrowShrink.ps1** HPC PowerShell Betiği</span><span class="sxs-lookup"><span data-stu-id="7cd19-108">The **AzureAutoGrowShrink.ps1** HPC PowerShell script</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="7cd19-109">Şu anda, yalnızca otomatik olarak Büyüt ve Windows Server işletim sistemi çalıştırılan HPC Pack işlem düğümleri daraltma.</span><span class="sxs-lookup"><span data-stu-id="7cd19-109">Currently you can only automatically grow and shrink HPC Pack compute nodes that are running a Windows Server operating system.</span></span>


## <a name="set-the-autogrowshrink-cluster-property"></a><span data-ttu-id="7cd19-110">AutoGrowShrink küme özelliğini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="7cd19-110">Set the AutoGrowShrink cluster property</span></span>
### <a name="prerequisites"></a><span data-ttu-id="7cd19-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7cd19-111">Prerequisites</span></span>

* <span data-ttu-id="7cd19-112">**HPC Pack 2012 R2 güncelleştirme 2 veya sonraki bir küme** -küme baş düğümüne olabilir ya da şirket içi dağıtılan veya bir Azure VM.</span><span class="sxs-lookup"><span data-stu-id="7cd19-112">**HPC Pack 2012 R2 Update 2 or later cluster** - The cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="7cd19-113">Bkz: [HPC paketi ile karma küme ayarlama](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) bir şirket içi baş düğüm ve Azure "veri bloğu" düğümleri ile çalışmaya başlamak için.</span><span class="sxs-lookup"><span data-stu-id="7cd19-113">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) to get started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="7cd19-114">Bkz: [HPC Pack Iaas dağıtım betiği](hpcpack-cluster-powershell-script.md) hızlı bir şekilde Azure VM'de HPC paketi küme dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="7cd19-114">See the [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) to quickly deploy an HPC Pack cluster in Azure VMs.</span></span>

* <span data-ttu-id="7cd19-115">**Bir küme baş düğümü Azure (Resource Manager dağıtım modeli) bulunan** - HPC Pack 2016'dan itibaren sertifika kimlik doğrulaması Azure Active Directory uygulamada otomatik olarak artan için kullanılır ve küçültme küme VM'ler dağıtılabilir kullanma Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7cd19-115">**For a cluster with a head node in Azure (Resource Manager deployment model)** - Starting in HPC Pack 2016, certificate authentication in an Azure Active Directory application is used for automatically growing and shrinking cluster VMs deployed using Azure Resource Manager.</span></span> <span data-ttu-id="7cd19-116">Bir sertifika aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="7cd19-116">Configure a certificate as follows:</span></span>

  1. <span data-ttu-id="7cd19-117">Küme dağıtıldıktan sonra Uzak Masaüstü tarafından bir baş düğümüne bağlanmak.</span><span class="sxs-lookup"><span data-stu-id="7cd19-117">After cluster deployment, connect by Remote Desktop to one head node.</span></span>

  2. <span data-ttu-id="7cd19-118">Her baş düğümüne (özel anahtarı olan PFX biçimi) sertifikasını yükleyin ve Cert: \LocalMachine\My ve Cert: \LocalMachine\Root yükleyin.</span><span class="sxs-lookup"><span data-stu-id="7cd19-118">Upload the certificate (PFX format with private key) to each head node and install to Cert:\LocalMachine\My and Cert:\LocalMachine\Root.</span></span>

  3. <span data-ttu-id="7cd19-119">Azure PowerShell'i yönetici olarak başlatın ve bir baş düğüm üzerinde aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7cd19-119">Start Azure PowerShell as an administrator and run the following commands on one head node:</span></span>

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    <span data-ttu-id="7cd19-120">Hesabınızın birden fazla Azure Active Directory kiracısı veya Azure aboneliği varsa, doğru Kiracı ve aboneliği seçmek için aşağıdaki komutu çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7cd19-120">If your account is in more than one Azure Active Directory tenant or Azure subscription, you can run the following command to select the correct tenant and subscription:</span></span>
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    <span data-ttu-id="7cd19-121">Şu anda seçili Kiracı ve abonelik görüntülemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7cd19-121">Run the following command to view the currently selected tenant and subscription:</span></span>
    
    ```powershell
        Get-AzureRMContext
    ```

  4. <span data-ttu-id="7cd19-122">Aşağıdaki betiği çalıştırın</span><span class="sxs-lookup"><span data-stu-id="7cd19-122">Run the following script</span></span>

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    <span data-ttu-id="7cd19-123">Burada</span><span class="sxs-lookup"><span data-stu-id="7cd19-123">where</span></span>

    <span data-ttu-id="7cd19-124">**DisplayName** -Azure Active uygulama görünen adı.</span><span class="sxs-lookup"><span data-stu-id="7cd19-124">**DisplayName** - Azure Active Application display name.</span></span> <span data-ttu-id="7cd19-125">Uygulama yok, Azure Active Directory içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7cd19-125">If the application does not exist, it is created in Azure Active Directory.</span></span>

    <span data-ttu-id="7cd19-126">**Giriş sayfası** -uygulama giriş sayfası.</span><span class="sxs-lookup"><span data-stu-id="7cd19-126">**HomePage** - The home page of the application.</span></span> <span data-ttu-id="7cd19-127">Önceki örnekte olduğu gibi bir kukla URL yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7cd19-127">You can configure a dummy URL, as in the preceding example.</span></span>

    <span data-ttu-id="7cd19-128">**IdentifierUri** -uygulama tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="7cd19-128">**IdentifierUri** - Identifier of the application.</span></span> <span data-ttu-id="7cd19-129">Önceki örnekte olduğu gibi bir kukla URL yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7cd19-129">You can configure a dummy URL, as in the preceding example.</span></span>

    <span data-ttu-id="7cd19-130">**CertificateThumbprint** -baş düğüm 1. adımda yüklediğiniz sertifikanın parmak izi.</span><span class="sxs-lookup"><span data-stu-id="7cd19-130">**CertificateThumbprint** - Thumbprint of the certificate you installed on the head node in Step 1.</span></span>

    <span data-ttu-id="7cd19-131">**Tenantıd** -Kiracı kimliği, Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7cd19-131">**TenantId** - Tenant ID of your Azure Active Directory.</span></span> <span data-ttu-id="7cd19-132">Kiracı kimliği Azure Active Directory Portalı'ndan elde edebilirsiniz **özellikleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="7cd19-132">You can get the Tenant ID from the Azure Active Directory portal **Properties** page.</span></span>

    <span data-ttu-id="7cd19-133">Hakkında daha fazla ayrıntı için **ConfigARMAutoGrowShrinkCert.ps1**, çalışma `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="7cd19-133">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span></span>


* <span data-ttu-id="7cd19-134">**Bir küme baş düğümü Azure (Klasik dağıtım modeli) bulunan** - HPC Pack Iaas dağıtım komut dosyası kullanırsanız Klasik dağıtım modelinde küme oluşturma, etkinleştirme için **AutoGrowShrink** küme özelliği tarafından AutoGrowShrink seçeneği küme yapılandırma dosyasında ayarlama.</span><span class="sxs-lookup"><span data-stu-id="7cd19-134">**For a cluster with a head node in Azure (classic deployment model)** - If you use the HPC Pack IaaS deployment script to create the cluster in the classic deployment model, enable the **AutoGrowShrink** cluster property by setting the AutoGrowShrink option in the cluster configuration file.</span></span> <span data-ttu-id="7cd19-135">Belge eşlik Ayrıntılar için bkz [komut dosyası indirme](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="7cd19-135">For details, see the documentation accompanying the [script download](https://www.microsoft.com/download/details.aspx?id=44949).</span></span>

    <span data-ttu-id="7cd19-136">Alternatif olarak, etkinleştirme **AutoGrowShrink** aşağıdaki bölümde açıklanan HPC PowerShell komutlarını kullanarak küme dağıttıktan sonra özellik kümesi.</span><span class="sxs-lookup"><span data-stu-id="7cd19-136">Alternatively, enable the **AutoGrowShrink** cluster property after you deploy the cluster by using HPC PowerShell commands described in the following section.</span></span> <span data-ttu-id="7cd19-137">Bunun için hazırlamak için önce aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="7cd19-137">To prepare for this, first complete the following steps:</span></span>

  1. <span data-ttu-id="7cd19-138">Azure yönetim sertifikası baş düğüm ve Azure aboneliğini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7cd19-138">Configure an Azure management certificate on the head node and in the Azure subscription.</span></span> <span data-ttu-id="7cd19-139">Bir sınama dağıtımı için HPC Pack baş düğümüne yükleyen varsayılan Microsoft HPC Azure otomatik olarak imzalanan sertifika kullan ve Azure aboneliğinize bu sertifikayı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="7cd19-139">For a test deployment, you can use the Default Microsoft HPC Azure self-signed certificate that HPC Pack installs on the head node, and then upload that certificate to your Azure subscription.</span></span> <span data-ttu-id="7cd19-140">Seçenekler ve adımları için bkz: [TechNet Kitaplığı Kılavuzu](https://technet.microsoft.com/library/gg481759.aspx).</span><span class="sxs-lookup"><span data-stu-id="7cd19-140">For options and steps, see the [TechNet Library guidance](https://technet.microsoft.com/library/gg481759.aspx).</span></span>

  2. <span data-ttu-id="7cd19-141">Çalıştırma **regedit** baş düğüm için HKLM\SOFTWARE\Micorsoft\HPC\IaasInfo gidin ve bir dize değeri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7cd19-141">Run **regedit** on the head node, go to HKLM\SOFTWARE\Micorsoft\HPC\IaasInfo, and add a string value.</span></span> <span data-ttu-id="7cd19-142">Değer adı "Parmak izi" olarak ayarlayın ve sertifikanın parmak izi 1. adımda veri değer.</span><span class="sxs-lookup"><span data-stu-id="7cd19-142">Set the Value name to “ThumbPrint”, and Value data to the thumbprint of the certificate in Step 1.</span></span>

### <a name="hpc-powershell-commands-to-set-the-autogrowshrink-property"></a><span data-ttu-id="7cd19-143">HPC PowerShell komutlarını AutoGrowShrink özelliğini ayarlamak için</span><span class="sxs-lookup"><span data-stu-id="7cd19-143">HPC PowerShell commands to set the AutoGrowShrink property</span></span>
<span data-ttu-id="7cd19-144">Şunlardır ayarlamak için örnek HPC PowerShell komutları **AutoGrowShrink** ve ek parametrelerle davranışını ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="7cd19-144">Following are sample HPC PowerShell commands to set **AutoGrowShrink** and to tune its behavior with additional parameters.</span></span> <span data-ttu-id="7cd19-145">Bkz: [AutoGrowShrink parametreleri](#AutoGrowShrink-parameters) ayarlarının tam listesi için bu makalede daha sonra.</span><span class="sxs-lookup"><span data-stu-id="7cd19-145">See [AutoGrowShrink parameters](#AutoGrowShrink-parameters) later in this article for the complete list of settings.</span></span>

<span data-ttu-id="7cd19-146">Bu komutları çalıştırmak için yönetici olarak küme baş düğümünde HPC PowerShell'i başlatın.</span><span class="sxs-lookup"><span data-stu-id="7cd19-146">To run these commands, start HPC PowerShell on the cluster head node as an administrator.</span></span>

<span data-ttu-id="7cd19-147">**AutoGrowShrink özelliğini etkinleştirmek için**</span><span class="sxs-lookup"><span data-stu-id="7cd19-147">**To enable the AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

<span data-ttu-id="7cd19-148">**AutoGrowShrink özelliği devre dışı bırakmak için**</span><span class="sxs-lookup"><span data-stu-id="7cd19-148">**To disable the AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

<span data-ttu-id="7cd19-149">**Dakika cinsinden Büyüt aralığını değiştirmek için**</span><span class="sxs-lookup"><span data-stu-id="7cd19-149">**To change the grow interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

<span data-ttu-id="7cd19-150">**Dakika cinsinden küçültme aralığını değiştirmek için**</span><span class="sxs-lookup"><span data-stu-id="7cd19-150">**To change the shrink interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

<span data-ttu-id="7cd19-151">**AutoGrowShrink geçerli yapılandırmasını görüntülemek için**</span><span class="sxs-lookup"><span data-stu-id="7cd19-151">**To view the current configuration of AutoGrowShrink**</span></span>

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

<span data-ttu-id="7cd19-152">**Düğüm grupları AutoGrowShrink dışlamak için**</span><span class="sxs-lookup"><span data-stu-id="7cd19-152">**To exclude node groups from AutoGrowShrink**</span></span>

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> <span data-ttu-id="7cd19-153">Bu parametre HPC Pack 2016'dan itibaren desteklenir</span><span class="sxs-lookup"><span data-stu-id="7cd19-153">This parameter is supported starting in HPC Pack 2016</span></span>
>

### <a name="autogrowshrink-parameters"></a><span data-ttu-id="7cd19-154">AutoGrowShrink parametreleri</span><span class="sxs-lookup"><span data-stu-id="7cd19-154">AutoGrowShrink parameters</span></span>
<span data-ttu-id="7cd19-155">Kullanarak değiştirebilirsiniz AutoGrowShrink Parametreler şunlardır **kümesi HpcClusterProperty** komutu.</span><span class="sxs-lookup"><span data-stu-id="7cd19-155">The following are AutoGrowShrink parameters that you can modify by using the **Set-HpcClusterProperty** command.</span></span>

* <span data-ttu-id="7cd19-156">**EnableGrowShrink** -etkinleştirmek veya devre dışı bırakmak için anahtar **AutoGrowShrink** özelliği.</span><span class="sxs-lookup"><span data-stu-id="7cd19-156">**EnableGrowShrink** - Switch to enable or disable the **AutoGrowShrink** property.</span></span>
* <span data-ttu-id="7cd19-157">**ParamSweepTasksPerCore** -bir çekirdek büyümeye parametrik tarama görev sayısı.</span><span class="sxs-lookup"><span data-stu-id="7cd19-157">**ParamSweepTasksPerCore** - Number of parametric sweep tasks to grow one core.</span></span> <span data-ttu-id="7cd19-158">Görev başına bir çekirdek büyümeye varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="7cd19-158">The default is to grow one core per task.</span></span>

  > [!NOTE]
  > <span data-ttu-id="7cd19-159">HPC Pack QFE KB3134307 değişiklikleri **ParamSweepTasksPerCore** için **TasksPerResourceUnit**.</span><span class="sxs-lookup"><span data-stu-id="7cd19-159">HPC Pack QFE KB3134307 changes **ParamSweepTasksPerCore** to **TasksPerResourceUnit**.</span></span> <span data-ttu-id="7cd19-160">İş kaynak türüne göre ve düğüm, yuva veya çekirdek olabilir.</span><span class="sxs-lookup"><span data-stu-id="7cd19-160">It is based on the job resource type and can be node, socket, or core.</span></span>
  >
  >
* <span data-ttu-id="7cd19-161">**GrowThreshold** -otomatik büyüme tetiklemek için kuyruğa alınmış görevlerin eşiği.</span><span class="sxs-lookup"><span data-stu-id="7cd19-161">**GrowThreshold** - Threshold of queued tasks to trigger automatic growth.</span></span> <span data-ttu-id="7cd19-162">Sıraya alınmış durumda 1 veya daha fazla görev varsa, otomatik olarak düğümleri Büyüt anlamına gelir 1 varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="7cd19-162">The default is 1, which means that if there are 1 or more tasks in the queued state, automatically grow nodes.</span></span>
* <span data-ttu-id="7cd19-163">**GrowInterval** -otomatik büyüme tetiklemek için zaman aralığını dakika cinsinden.</span><span class="sxs-lookup"><span data-stu-id="7cd19-163">**GrowInterval** - Interval in minutes to trigger automatic growth.</span></span> <span data-ttu-id="7cd19-164">Varsayılan aralığı 5 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="7cd19-164">The default interval is 5 minutes.</span></span>
* <span data-ttu-id="7cd19-165">**ShrinkInterval** -otomatik küçültme tetiklemek için zaman aralığını dakika cinsinden.</span><span class="sxs-lookup"><span data-stu-id="7cd19-165">**ShrinkInterval** - Interval in minutes to trigger automatic shrinking.</span></span> <span data-ttu-id="7cd19-166">Varsayılan aralığı 5 dakikadır. |</span><span class="sxs-lookup"><span data-stu-id="7cd19-166">The default interval is 5 minutes.|</span></span>
* <span data-ttu-id="7cd19-167">**ShrinkIdleTimes** -düğümleri göstermek için daraltmak için sürekli denetimlerinin sayısının boş.</span><span class="sxs-lookup"><span data-stu-id="7cd19-167">**ShrinkIdleTimes** - Number of continuous checks to shrink to indicate the nodes are idle.</span></span> <span data-ttu-id="7cd19-168">3 kez varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="7cd19-168">The default is 3 times.</span></span> <span data-ttu-id="7cd19-169">Örneğin, varsa **ShrinkInterval** 5 dakika, HPC Pack her 5 dakikada bir düğüm boş olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="7cd19-169">For example, if the **ShrinkInterval** is 5 minutes, HPC Pack checks whether the node is idle every 5 minutes.</span></span> <span data-ttu-id="7cd19-170">3 sürekli (15 dakika) denetledikten sonra düğümler boşta durumunda ise, HPC Pack bu düğüme küçültür.</span><span class="sxs-lookup"><span data-stu-id="7cd19-170">If the nodes are in the idle state after 3 continuous checks (15 minutes), then HPC Pack shrinks that node.</span></span>
* <span data-ttu-id="7cd19-171">**ExtraNodesGrowRatio** -ileti geçirme arabirimi (MPI) işleri büyümeye düğümleri ek yüzdesi.</span><span class="sxs-lookup"><span data-stu-id="7cd19-171">**ExtraNodesGrowRatio** - Additional percentage of nodes to grow for Message Passing Interface (MPI) jobs.</span></span> <span data-ttu-id="7cd19-172">HPC Pack %1 MPI işlerini için düğümleri büyür anlamına gelir 1 varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="7cd19-172">The default value is 1, which means that HPC Pack grows nodes 1% for MPI jobs.</span></span>
* <span data-ttu-id="7cd19-173">**GrowByMin** -otomatik büyüme İlkesi iş için gereken en düşük kaynaklardaki dayalı olup olmadığını belirtmek için anahtar.</span><span class="sxs-lookup"><span data-stu-id="7cd19-173">**GrowByMin** - Switch to indicate whether the autogrow policy is based on the minimum resources required for the job.</span></span> <span data-ttu-id="7cd19-174">HPC Pack işleri için gereken en fazla kaynakları göre işleri için düğümleri büyür başka bir deyişle, false, varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="7cd19-174">The default is false, which means that HPC Pack grows nodes for jobs based on the maximum resources required for the jobs.</span></span>
* <span data-ttu-id="7cd19-175">**SoaJobGrowThreshold** -otomatik tetiklemek için gelen SOA istekleri eşiğinin büyümesine işlemi.</span><span class="sxs-lookup"><span data-stu-id="7cd19-175">**SoaJobGrowThreshold** - Threshold of incoming SOA requests to trigger the automatic grow process.</span></span> <span data-ttu-id="7cd19-176">Varsayılan değer 50000 ' dir.</span><span class="sxs-lookup"><span data-stu-id="7cd19-176">The default value is 50000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="7cd19-177">Bu parametre, HPC Pack 2012 R2 güncelleştirme 3'te itibaren desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="7cd19-177">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
  >
* <span data-ttu-id="7cd19-178">**SoaRequestsPerCore** -bir çekirdek büyümeye istekleri Gelen SOA sayısı.</span><span class="sxs-lookup"><span data-stu-id="7cd19-178">**SoaRequestsPerCore** -Number of incoming SOA requests to grow one core.</span></span> <span data-ttu-id="7cd19-179">20000 varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="7cd19-179">The default value is 20000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="7cd19-180">Bu parametre, HPC Pack 2012 R2 güncelleştirme 3'te itibaren desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="7cd19-180">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
* <span data-ttu-id="7cd19-181">**ExcludeNodeGroups** – belirtilen düğümün gruplardaki düğümler otomatik olarak Büyüt ve daraltma.</span><span class="sxs-lookup"><span data-stu-id="7cd19-181">**ExcludeNodeGroups** – Nodes in the specified node groups do not automatically grow and shrink.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="7cd19-182">Bu parametre, HPC Pack 2016'dan itibaren desteklenir.</span><span class="sxs-lookup"><span data-stu-id="7cd19-182">This parameter is supported starting in HPC Pack 2016.</span></span>
  >

### <a name="mpi-example"></a><span data-ttu-id="7cd19-183">MPI örneği</span><span class="sxs-lookup"><span data-stu-id="7cd19-183">MPI example</span></span>
<span data-ttu-id="7cd19-184">Varsayılan olarak, %1 HPC Pack büyür MPI işlerini için ek düğümleri (**ExtraNodesGrowRatio** 1 olarak ayarlayın).</span><span class="sxs-lookup"><span data-stu-id="7cd19-184">By default HPC Pack grows 1% extra nodes for MPI jobs (**ExtraNodesGrowRatio** is set to 1).</span></span> <span data-ttu-id="7cd19-185">, Birden çok düğüm MPI gerektirebilir ve tüm düğümler hazır olduğunuzda, iş yalnızca çalıştırabilirsiniz nedenidir.</span><span class="sxs-lookup"><span data-stu-id="7cd19-185">The reason is that MPI may require multiple nodes, and the job can only run when all nodes are ready.</span></span> <span data-ttu-id="7cd19-186">Zaman zaman Azure düğümleri başladığında, tek bir düğüm diğerlerinden, diğer düğümler hazır hale getirmek bu düğümü için beklenirken boşta olması neden başlatmak için daha fazla süre gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="7cd19-186">When Azure starts nodes, occasionally one node might need more time to start than others, causing other nodes to be idle while waiting for that node to get ready.</span></span> <span data-ttu-id="7cd19-187">Ek düğümler büyüyen HPC Pack bu kaynak bekleme süresini azaltır ve maliyetleri potansiyel olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="7cd19-187">By growing extra nodes, HPC Pack reduces this resource waiting time, and potentially saves costs.</span></span> <span data-ttu-id="7cd19-188">MPI işlerini (örneğin, % 10) için ek düğümleri artırmak için benzer bir komutu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="7cd19-188">To increase the percentage of extra nodes for MPI jobs (for example, to 10%), run a command similar to</span></span>

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a><span data-ttu-id="7cd19-189">SOA örneği</span><span class="sxs-lookup"><span data-stu-id="7cd19-189">SOA example</span></span>
<span data-ttu-id="7cd19-190">Varsayılan olarak, **SoaJobGrowThreshold** 50000 için ayarlanır ve **SoaRequestsPerCore** 200000 için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="7cd19-190">By default, **SoaJobGrowThreshold** is set to 50000 and **SoaRequestsPerCore** is set to 200000.</span></span> <span data-ttu-id="7cd19-191">Bir SOA işi 70000 isteği göndermek, bir Sıraya alınan görev olduğunu ve gelen istekleri 70000.</span><span class="sxs-lookup"><span data-stu-id="7cd19-191">If you submit one SOA job with 70000 requests, there is one queued task and incoming requests are 70000.</span></span> <span data-ttu-id="7cd19-192">Bu durumda HPC Pack 1 çekirdek kuyruğa alınmış görev için ve gelen istekleri büyüdükçe, (70000-50000) büyür / 20000 = 1 çekirdek, bu nedenle, toplam bu SOA işi için 2 Çekirdek büyür.</span><span class="sxs-lookup"><span data-stu-id="7cd19-192">In this case HPC Pack grows 1 core for the queued task, and for incoming requests, grows (70000 - 50000)/20000 = 1 core, so in total grows 2 cores for this SOA job.</span></span>

## <a name="run-the-azureautogrowshrinkps1-script"></a><span data-ttu-id="7cd19-193">AzureAutoGrowShrink.ps1 komut dosyasını çalıştır</span><span class="sxs-lookup"><span data-stu-id="7cd19-193">Run the AzureAutoGrowShrink.ps1 script</span></span>
### <a name="prerequisites"></a><span data-ttu-id="7cd19-194">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7cd19-194">Prerequisites</span></span>

* <span data-ttu-id="7cd19-195">**HPC Pack 2012 R2 güncelleştirme 1 veya sonraki bir küme** - **AzureAutoGrowShrink.ps1** komut dosyası, % CCP_HOME % bin klasörüne yüklenir.</span><span class="sxs-lookup"><span data-stu-id="7cd19-195">**HPC Pack 2012 R2 Update 1 or later cluster** - The **AzureAutoGrowShrink.ps1** script is installed in the %CCP_HOME%bin folder.</span></span> <span data-ttu-id="7cd19-196">Küme baş düğümüne olabilir ya da şirket içi dağıtılan veya bir Azure VM.</span><span class="sxs-lookup"><span data-stu-id="7cd19-196">The cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="7cd19-197">Bkz: [HPC paketi ile karma küme ayarlama](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) bir şirket içi baş düğüm ve Azure "veri bloğu" düğümleri ile çalışmaya başlamak için.</span><span class="sxs-lookup"><span data-stu-id="7cd19-197">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) to get started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="7cd19-198">Bkz: [HPC Pack Iaas dağıtım betiği](hpcpack-cluster-powershell-script.md) hızlı bir şekilde Azure VM'de HPC paketi Küme dağıtımı veya kullanmak için bir [Azure Hızlı Başlangıç şablonu](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span><span class="sxs-lookup"><span data-stu-id="7cd19-198">See the [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) to quickly deploy an HPC Pack cluster in Azure VMs, or use an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span></span>
* <span data-ttu-id="7cd19-199">**Azure PowerShell 1.4.0** -komut dosyası şu anda bu belirli Azure PowerShell sürümüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="7cd19-199">**Azure PowerShell 1.4.0** - The script currently depends on this specific version of Azure PowerShell.</span></span>
* <span data-ttu-id="7cd19-200">**Azure ile bir küme düğümleri veri bloğu** -HPC Pack yüklü olduğu bir istemci bilgisayarı veya baş düğüm komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7cd19-200">**For a cluster with Azure burst nodes** - Run the script on a client computer where HPC Pack is installed, or on the head node.</span></span> <span data-ttu-id="7cd19-201">Bir istemci bilgisayarda çalışıyorsa $env değişken Ayarla olun: baş düğümüne işaret edecek şekilde CCP_SCHEDULER.</span><span class="sxs-lookup"><span data-stu-id="7cd19-201">If running on a client computer, ensure that you set the variable $env:CCP_SCHEDULER to point to the head node.</span></span> <span data-ttu-id="7cd19-202">Azure "veri bloğu" düğümler kümeye eklenmesi gerekir, ancak değil dağıtılan bir durumda olabilir.</span><span class="sxs-lookup"><span data-stu-id="7cd19-202">The Azure “burst” nodes must be added to the cluster, but they may be in the Not-Deployed state.</span></span>
* <span data-ttu-id="7cd19-203">**Azure VM'ler (Resource Manager dağıtım modeli) dağıtılan bir küme için** -Azure Resource Manager dağıtım modelinde dağıtılan VM'ler küme için komut dosyası Azure kimlik doğrulaması için iki yöntemi destekler: Azure hesabınızda oturum çalıştırmak için Her komut dosyası (çalıştırarak `Login-AzureRmAccount`, veya bir sertifika ile kimlik doğrulaması için bir hizmet sorumlusu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7cd19-203">**For a cluster deployed in Azure VMs (Resource Manager deployment model)** - For a cluster of Azure VMs deployed in the Resource Manager deployment model, the script supports two methods for Azure authentication: sign in to your Azure account to run the script every time (by running `Login-AzureRmAccount`, or configure a service principal to authenticate with a certificate.</span></span> <span data-ttu-id="7cd19-204">HPC Pack komut dosyası sağlar **ConfigARMAutoGrowShrinkCert.ps** sertifikayla bir hizmet sorumlusu oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="7cd19-204">HPC Pack provides the script **ConfigARMAutoGrowShrinkCert.ps** to create a service principal with certificate.</span></span> <span data-ttu-id="7cd19-205">Komut dosyasını bir Azure Active Directory (Azure AD) uygulama ve hizmet sorumlusu oluşturur ve hizmet sorumlusu katılımcı rolü atar.</span><span class="sxs-lookup"><span data-stu-id="7cd19-205">The script creates an Azure Active Directory (Azure AD) application and a service principal, and assigns the Contributor role to the service principal.</span></span> <span data-ttu-id="7cd19-206">Komut dosyasını çalıştırmak için Azure PowerShell'i yönetici olarak başlatın ve aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7cd19-206">To run the script, start Azure PowerShell  as administrator and run the following commands:</span></span>

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    <span data-ttu-id="7cd19-207">Hakkında daha fazla ayrıntı için **ConfigARMAutoGrowShrinkCert.ps1**, çalışma `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span><span class="sxs-lookup"><span data-stu-id="7cd19-207">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span></span>

* <span data-ttu-id="7cd19-208">**Azure VM'ler (Klasik dağıtım modeli) dağıtılan bir küme için** -bağımlı olduğundan dolayı VM baş düğümünde komut dosyasını çalıştırmak **başlangıç HpcIaaSNode.ps1** ve **Stop-HpcIaaSNode.ps1** yüklü komutlar.</span><span class="sxs-lookup"><span data-stu-id="7cd19-208">**For a cluster deployed in Azure VMs (classic deployment model)** - Run the script on the head node VM, because it depends on the **Start-HpcIaaSNode.ps1** and **Stop-HpcIaaSNode.ps1** scripts that are installed there.</span></span> <span data-ttu-id="7cd19-209">Bu komut ayrıca bir Azure yönetim sertifikası gerektirir veya yayımlama ayarları dosyası (bkz [bir HPC Pack Yönet işlem düğümleri küme Azure'da](hpcpack-cluster-node-manage.md)).</span><span class="sxs-lookup"><span data-stu-id="7cd19-209">Those scripts additionally require an Azure management certificate or publish settings file (see [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md)).</span></span> <span data-ttu-id="7cd19-210">Tüm işlem düğümü ihtiyacınız VM'ler zaten kümeye eklenmiş olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7cd19-210">Make sure all the compute node VMs you need are already added to the cluster.</span></span> <span data-ttu-id="7cd19-211">Bunlar durdurulmuş durumda olabilir.</span><span class="sxs-lookup"><span data-stu-id="7cd19-211">They may be in the Stopped state.</span></span>



### <a name="syntax"></a><span data-ttu-id="7cd19-212">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="7cd19-212">Syntax</span></span>
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="7cd19-213">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7cd19-213">Parameters</span></span>
* <span data-ttu-id="7cd19-214">**NodeTemplates** -düğüm şablonlarının adlarını büyür ve daraltmak için düğümlerini kapsamını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7cd19-214">**NodeTemplates** - Names of the node templates to define the scope for the nodes to grow and shrink.</span></span> <span data-ttu-id="7cd19-215">Belirtilmezse, (varsayılan değer: @()), tüm düğümlerde **AzureNodes** düğüm grubu içinde olduğunda kapsam olan **NodeType** AzureNodes ve tüm düğümleri değerine sahip **ComputeNodes**düğüm grubu içinde olduğunda kapsam olan **NodeType** ComputeNodes değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="7cd19-215">If not specified (the default value is @()), all nodes in the **AzureNodes** node group are in scope when **NodeType** has a value of AzureNodes, and all nodes in the **ComputeNodes** node group are in scope when **NodeType** has a value of ComputeNodes.</span></span>
* <span data-ttu-id="7cd19-216">**JobTemplates** -büyümeye düğümlerin kapsamını tanımlamak için proje şablonları adları.</span><span class="sxs-lookup"><span data-stu-id="7cd19-216">**JobTemplates** - Names of the job templates to define the scope for the nodes to grow.</span></span>
* <span data-ttu-id="7cd19-217">**NodeType** -büyür ve küçültme düğümünün türü.</span><span class="sxs-lookup"><span data-stu-id="7cd19-217">**NodeType** - The type of node to grow and shrink.</span></span> <span data-ttu-id="7cd19-218">Desteklenen değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7cd19-218">Supported values are:</span></span>

  * <span data-ttu-id="7cd19-219">**AzureNodes** – bir şirket içi Azure PaaS (veri bloğu) düğümler için ya da Azure Iaas küme.</span><span class="sxs-lookup"><span data-stu-id="7cd19-219">**AzureNodes** – for Azure PaaS (burst) nodes in an on-premises or Azure IaaS cluster.</span></span>
  * <span data-ttu-id="7cd19-220">**ComputeNodes** - işlem düğümünde VM'ler yalnızca bir Azure Iaas kümesi.</span><span class="sxs-lookup"><span data-stu-id="7cd19-220">**ComputeNodes** - for compute node VMs only in an Azure IaaS cluster.</span></span>

* <span data-ttu-id="7cd19-221">**NumOfQueuedJobsPerNodeToGrow** -tek bir düğüm büyümeye gerekli sıraya alınmış işlerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="7cd19-221">**NumOfQueuedJobsPerNodeToGrow** - Number of queued jobs required to grow one node.</span></span>
* <span data-ttu-id="7cd19-222">**NumOfQueuedJobsToGrowThreshold** -Büyüt işlemini başlatmak üzere sıraya alınan iş eşik sayısı.</span><span class="sxs-lookup"><span data-stu-id="7cd19-222">**NumOfQueuedJobsToGrowThreshold** - The threshold number of queued jobs to start the grow process.</span></span>
* <span data-ttu-id="7cd19-223">**NumOfActiveQueuedTasksPerNodeToGrow** - sayı etkin bir düğümün ulaşması için gereken görevler sıraya.</span><span class="sxs-lookup"><span data-stu-id="7cd19-223">**NumOfActiveQueuedTasksPerNodeToGrow** - The number of active queued tasks required to grow one node.</span></span> <span data-ttu-id="7cd19-224">Varsa **NumOfQueuedJobsPerNodeToGrow** belirtilen 0'dan büyük bir değer ile bu parametre yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="7cd19-224">If **NumOfQueuedJobsPerNodeToGrow** is specified with a value greater than 0, this parameter is ignored.</span></span>
* <span data-ttu-id="7cd19-225">**NumOfActiveQueuedTasksToGrowThreshold** -Büyüt işlemini başlatmak için etkin kuyruğa alınmış görevlerin eşik sayısı.</span><span class="sxs-lookup"><span data-stu-id="7cd19-225">**NumOfActiveQueuedTasksToGrowThreshold** - The threshold number of active queued tasks to start the grow process.</span></span>
* <span data-ttu-id="7cd19-226">**NumOfInitialNodesToGrow** -ilk düğüm sayısı alt sınırı kapsamdaki tüm düğümler varsa büyümeye **değil dağıtılan** veya **durduruldu (Deallocated)**.</span><span class="sxs-lookup"><span data-stu-id="7cd19-226">**NumOfInitialNodesToGrow** - The initial minimum number of nodes to grow if all the nodes in scope are **Not-Deployed** or **Stopped (Deallocated)**.</span></span>
* <span data-ttu-id="7cd19-227">**GrowCheckIntervalMins** -büyümeye denetimleri arasındaki dakika aralığında.</span><span class="sxs-lookup"><span data-stu-id="7cd19-227">**GrowCheckIntervalMins** - The interval in minutes between checks to grow.</span></span>
* <span data-ttu-id="7cd19-228">**ShrinkCheckIntervalMins** -daraltma için denetimler arasındaki dakika aralığında.</span><span class="sxs-lookup"><span data-stu-id="7cd19-228">**ShrinkCheckIntervalMins** - The interval in minutes between checks to shrink.</span></span>
* <span data-ttu-id="7cd19-229">**ShrinkCheckIdleTimes** -sürekli sayısını Küçült denetimleri (ayırarak **ShrinkCheckIntervalMins**) düğümler boşta olduğunu belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="7cd19-229">**ShrinkCheckIdleTimes** - The number of continuous shrink checks (separated by **ShrinkCheckIntervalMins**) to indicate the nodes are idle.</span></span>
* <span data-ttu-id="7cd19-230">**UseLastConfigurations** -bağımsız değişken dosyasında kaydedilen önceki yapılandırmaları.</span><span class="sxs-lookup"><span data-stu-id="7cd19-230">**UseLastConfigurations** - The previous configurations saved in the argument file.</span></span>
* <span data-ttu-id="7cd19-231">**ArgFile**-kaydetmek ve komut dosyasını çalıştırmak üzere yapılandırmaları güncelleştirmek için kullanılan bağımsız değişken dosya adı.</span><span class="sxs-lookup"><span data-stu-id="7cd19-231">**ArgFile**- The name of the argument file used to save and update the configurations to run the script.</span></span>
* <span data-ttu-id="7cd19-232">**LogFilePrefix** -günlük dosyası ön ek adı.</span><span class="sxs-lookup"><span data-stu-id="7cd19-232">**LogFilePrefix** - The prefix name of the log file.</span></span> <span data-ttu-id="7cd19-233">Bir yolu belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7cd19-233">You can specify a path.</span></span> <span data-ttu-id="7cd19-234">Varsayılan olarak, geçerli çalışma dizini günlüğüne yazılır.</span><span class="sxs-lookup"><span data-stu-id="7cd19-234">By default the log is written to the current working directory.</span></span>

### <a name="example-1"></a><span data-ttu-id="7cd19-235">Örnek 1</span><span class="sxs-lookup"><span data-stu-id="7cd19-235">Example 1</span></span>
<span data-ttu-id="7cd19-236">Aşağıdaki örnek varsayılan AzureNode büyür ve otomatik olarak küçültmek için şablonla dağıtılan Azure veri bloğu düğümleri yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="7cd19-236">The following example configures the Azure burst nodes deployed with the Default AzureNode Template to grow and shrink automatically.</span></span> <span data-ttu-id="7cd19-237">Tüm düğüm başlangıçta giriş gerekirse **değil dağıtılan** durumunda, en az 3 düğümleri başlatılacağı.</span><span class="sxs-lookup"><span data-stu-id="7cd19-237">If all the nodes are initially in the **Not-Deployed** state, at least 3 nodes are started.</span></span> <span data-ttu-id="7cd19-238">Sıraya alınmış işlerin sayısı 8 aşarsa, kuyruğa alınmış işleri oranını kendi sayıyı aşıyor kadar komut dosyasını düğümleri başlatır **NumOfQueuedJobsPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="7cd19-238">If the number of queued jobs exceeds 8, the script starts nodes until their number exceeds the ratio of queued jobs to **NumOfQueuedJobsPerNodeToGrow**.</span></span> <span data-ttu-id="7cd19-239">Bir düğüm ardışık 3 boşta kalma sürelerini boşta bulunursa durdurulur.</span><span class="sxs-lookup"><span data-stu-id="7cd19-239">If a node is found to be idle in 3 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a><span data-ttu-id="7cd19-240">Örnek 2</span><span class="sxs-lookup"><span data-stu-id="7cd19-240">Example 2</span></span>
<span data-ttu-id="7cd19-241">Aşağıdaki örnek, Azure işlem düğümü varsayılan ComputeNode büyür ve otomatik olarak küçültmek için şablonu ile dağıtılan VM'ler yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="7cd19-241">The following example configures the Azure compute node VMs deployed with the Default ComputeNode Template to grow and shrink automatically.</span></span>
<span data-ttu-id="7cd19-242">Varsayılan proje şablonu tarafından yapılandırılan işleri, küme üzerinde iş yükü kapsamını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="7cd19-242">The jobs configured by the Default job template define the scope of the workload on the cluster.</span></span> <span data-ttu-id="7cd19-243">Tüm düğümleri başlangıçta durdurduysanız, en az 5 düğümleri başlatılır.</span><span class="sxs-lookup"><span data-stu-id="7cd19-243">If all the nodes are initially stopped, at least 5 nodes are started.</span></span> <span data-ttu-id="7cd19-244">15 etkin kuyruğa alınmış görevlerin sayısını aşarsa, kendi sayıyı aşıyor active sıraya alınan görevlere oranını kadar komut dosyasını düğümleri başlatır **NumOfActiveQueuedTasksPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="7cd19-244">If the number of active queued tasks exceeds 15, the script starts nodes until their number exceeds the ratio of active queued tasks to **NumOfActiveQueuedTasksPerNodeToGrow**.</span></span> <span data-ttu-id="7cd19-245">Bir düğüm 10 ardışık boşta kalma sürelerini boşta bulunursa durdurulur.</span><span class="sxs-lookup"><span data-stu-id="7cd19-245">If a node is found to be idle in 10 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
