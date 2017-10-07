---
title: "aaaAutoscale HPC paketi küme düğümleri | Microsoft Docs"
description: "Otomatik olarak Büyüt ve HPC paketi küme işlem düğümleri azure'da hello sayısı Daralt"
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
ms.openlocfilehash: 0bdf55625d337a2bbfe05677682d645a584798d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a><span data-ttu-id="27e86-103">Otomatik olarak Büyüt ve toohello küme iş yükü göre azure'da hello HPC paketi küme kaynaklarını Daralt</span><span class="sxs-lookup"><span data-stu-id="27e86-103">Automatically grow and shrink hello HPC Pack cluster resources in Azure according toohello cluster workload</span></span>
<span data-ttu-id="27e86-104">HPC Pack kümenizdeki Azure "veri bloğu" düğümlerini dağıtmak ya da Azure Vm'lerde bir HPC paketi küme oluşturmak, bir şekilde otomatik olarak büyütür veya düğümleri veya çekirdek hello küme hello iş yüküne göre gibi hello küme kaynaklarını küçültmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27e86-104">If you deploy Azure “burst” nodes in your HPC Pack cluster, or you create an HPC Pack cluster in Azure VMs, you may want a way to automatically grow or shrink hello cluster resources such as nodes or cores according to hello workload on hello cluster.</span></span> <span data-ttu-id="27e86-105">Bu şekilde Hello küme kaynaklarını ölçeklendirme sağlar toouse Azure kaynaklarınızı daha etkili ve bunların maliyetlerini denetlemenize.</span><span class="sxs-lookup"><span data-stu-id="27e86-105">Scaling hello cluster resources in this way allows you toouse your Azure resources more efficiently and control their costs.</span></span>

<span data-ttu-id="27e86-106">Bu makalede HPC Pack tooautoscale işlem kaynakları sağlayan iki yolunu gösterir:</span><span class="sxs-lookup"><span data-stu-id="27e86-106">This article shows you two ways that HPC Pack provides tooautoscale compute resources:</span></span>

* <span data-ttu-id="27e86-107">Merhaba HPC paketi küme özelliği **AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="27e86-107">hello HPC Pack cluster property **AutoGrowShrink**</span></span>

* <span data-ttu-id="27e86-108">Merhaba **AzureAutoGrowShrink.ps1** HPC PowerShell Betiği</span><span class="sxs-lookup"><span data-stu-id="27e86-108">hello **AzureAutoGrowShrink.ps1** HPC PowerShell script</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="27e86-109">Şu anda, yalnızca otomatik olarak Büyüt ve Windows Server işletim sistemi çalıştırılan HPC Pack işlem düğümleri daraltma.</span><span class="sxs-lookup"><span data-stu-id="27e86-109">Currently you can only automatically grow and shrink HPC Pack compute nodes that are running a Windows Server operating system.</span></span>


## <a name="set-hello-autogrowshrink-cluster-property"></a><span data-ttu-id="27e86-110">Merhaba AutoGrowShrink küme özelliğini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="27e86-110">Set hello AutoGrowShrink cluster property</span></span>
### <a name="prerequisites"></a><span data-ttu-id="27e86-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="27e86-111">Prerequisites</span></span>

* <span data-ttu-id="27e86-112">**HPC Pack 2012 R2 güncelleştirme 2 veya sonraki bir küme** -hello küme baş düğümüne olabilir ya da şirket içi dağıtılan veya bir Azure VM.</span><span class="sxs-lookup"><span data-stu-id="27e86-112">**HPC Pack 2012 R2 Update 2 or later cluster** - hello cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="27e86-113">Bkz: [HPC paketi ile karma küme ayarlama](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget bir şirket içi baş düğüm ve Azure "veri bloğu" düğümleri ile başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="27e86-113">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="27e86-114">Merhaba bkz [HPC Pack Iaas dağıtım betiği](hpcpack-cluster-powershell-script.md) tooquickly Azure VM'de HPC paketi küme dağıtın.</span><span class="sxs-lookup"><span data-stu-id="27e86-114">See hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) tooquickly deploy an HPC Pack cluster in Azure VMs.</span></span>

* <span data-ttu-id="27e86-115">**Bir küme baş düğümü Azure (Resource Manager dağıtım modeli) bulunan** - HPC Pack 2016'dan itibaren sertifika kimlik doğrulaması Azure Active Directory uygulamada otomatik olarak artan için kullanılır ve küçültme küme VM'ler dağıtılabilir kullanma Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="27e86-115">**For a cluster with a head node in Azure (Resource Manager deployment model)** - Starting in HPC Pack 2016, certificate authentication in an Azure Active Directory application is used for automatically growing and shrinking cluster VMs deployed using Azure Resource Manager.</span></span> <span data-ttu-id="27e86-116">Bir sertifika aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="27e86-116">Configure a certificate as follows:</span></span>

  1. <span data-ttu-id="27e86-117">Küme dağıtıldıktan sonra Uzak Masaüstü tooone baş düğümü tarafından bağlayın.</span><span class="sxs-lookup"><span data-stu-id="27e86-117">After cluster deployment, connect by Remote Desktop tooone head node.</span></span>

  2. <span data-ttu-id="27e86-118">Merhaba (PFX biçimi özel anahtara sahip) sertifika tooeach baş düğüm karşıya yükleme ve tooCert:\LocalMachine\My ve Cert: \LocalMachine\Root yükleyin.</span><span class="sxs-lookup"><span data-stu-id="27e86-118">Upload hello certificate (PFX format with private key) tooeach head node and install tooCert:\LocalMachine\My and Cert:\LocalMachine\Root.</span></span>

  3. <span data-ttu-id="27e86-119">Azure PowerShell'i yönetici olarak başlatın ve komutları bir baş düğüm üzerinde aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="27e86-119">Start Azure PowerShell as an administrator and run hello following commands on one head node:</span></span>

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    <span data-ttu-id="27e86-120">Hesabınızın birden fazla Azure Active Directory kiracısı veya Azure aboneliği varsa, hello aşağıdaki çalıştırabilirsiniz komutu tooselect hello doğru Kiracı ve abonelik:</span><span class="sxs-lookup"><span data-stu-id="27e86-120">If your account is in more than one Azure Active Directory tenant or Azure subscription, you can run hello following command tooselect hello correct tenant and subscription:</span></span>
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    <span data-ttu-id="27e86-121">Komut tooview aşağıdaki hello hello şu anda Kiracı ve abonelik Seçileni çalıştır:</span><span class="sxs-lookup"><span data-stu-id="27e86-121">Run hello following command tooview hello currently selected tenant and subscription:</span></span>
    
    ```powershell
        Get-AzureRMContext
    ```

  4. <span data-ttu-id="27e86-122">Komut dosyası izleyen hello çalıştırın</span><span class="sxs-lookup"><span data-stu-id="27e86-122">Run hello following script</span></span>

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    <span data-ttu-id="27e86-123">Burada</span><span class="sxs-lookup"><span data-stu-id="27e86-123">where</span></span>

    <span data-ttu-id="27e86-124">**DisplayName** -Azure Active uygulama görünen adı.</span><span class="sxs-lookup"><span data-stu-id="27e86-124">**DisplayName** - Azure Active Application display name.</span></span> <span data-ttu-id="27e86-125">Merhaba uygulaması yoksa, Azure Active Directory içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="27e86-125">If hello application does not exist, it is created in Azure Active Directory.</span></span>

    <span data-ttu-id="27e86-126">**Giriş sayfası** -hello uygulamasının hello giriş sayfası.</span><span class="sxs-lookup"><span data-stu-id="27e86-126">**HomePage** - hello home page of hello application.</span></span> <span data-ttu-id="27e86-127">Hello önceki örnekte olduğu gibi bir kukla URL yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27e86-127">You can configure a dummy URL, as in hello preceding example.</span></span>

    <span data-ttu-id="27e86-128">**IdentifierUri** -hello uygulama tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="27e86-128">**IdentifierUri** - Identifier of hello application.</span></span> <span data-ttu-id="27e86-129">Hello önceki örnekte olduğu gibi bir kukla URL yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27e86-129">You can configure a dummy URL, as in hello preceding example.</span></span>

    <span data-ttu-id="27e86-130">**CertificateThumbprint** -1. adımda hello baş düğümünde yüklü hello sertifikanın parmak izi.</span><span class="sxs-lookup"><span data-stu-id="27e86-130">**CertificateThumbprint** - Thumbprint of hello certificate you installed on hello head node in Step 1.</span></span>

    <span data-ttu-id="27e86-131">**Tenantıd** -Kiracı kimliği, Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="27e86-131">**TenantId** - Tenant ID of your Azure Active Directory.</span></span> <span data-ttu-id="27e86-132">Merhaba Kiracı kimliği hello Azure Active Directory Portalı'ndan elde edebilirsiniz **özellikleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="27e86-132">You can get hello Tenant ID from hello Azure Active Directory portal **Properties** page.</span></span>

    <span data-ttu-id="27e86-133">Hakkında daha fazla ayrıntı için **ConfigARMAutoGrowShrinkCert.ps1**, çalışma `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="27e86-133">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span></span>


* <span data-ttu-id="27e86-134">**Bir küme baş düğümü Azure (Klasik dağıtım modeli) bulunan** - hello Klasik dağıtım modeli etkinleştir hello hello HPC Pack Iaas dağıtım komut dosyası toocreate hello kümesi kullanıyorsanız **AutoGrowShrink** küme Merhaba küme yapılandırma dosyasında hello AutoGrowShrink seçeneği ayarlayarak özelliği.</span><span class="sxs-lookup"><span data-stu-id="27e86-134">**For a cluster with a head node in Azure (classic deployment model)** - If you use hello HPC Pack IaaS deployment script toocreate hello cluster in hello classic deployment model, enable hello **AutoGrowShrink** cluster property by setting hello AutoGrowShrink option in hello cluster configuration file.</span></span> <span data-ttu-id="27e86-135">Ayrıntılar için hello eşlik hello belgelerine bakın [komut dosyası indirme](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="27e86-135">For details, see hello documentation accompanying hello [script download](https://www.microsoft.com/download/details.aspx?id=44949).</span></span>

    <span data-ttu-id="27e86-136">Alternatif olarak, hello etkinleştirmek **AutoGrowShrink** HPC PowerShell'i kullanarak hello küme dağıttıktan sonra küme özelliği komutları açıklanan bölümden hello.</span><span class="sxs-lookup"><span data-stu-id="27e86-136">Alternatively, enable hello **AutoGrowShrink** cluster property after you deploy hello cluster by using HPC PowerShell commands described in hello following section.</span></span> <span data-ttu-id="27e86-137">Aşağıdaki ilk tam hello tooprepare Bu adımlar:</span><span class="sxs-lookup"><span data-stu-id="27e86-137">tooprepare for this, first complete hello following steps:</span></span>

  1. <span data-ttu-id="27e86-138">Azure yönetim sertifikası hello baş düğüm ve hello Azure aboneliği yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="27e86-138">Configure an Azure management certificate on hello head node and in hello Azure subscription.</span></span> <span data-ttu-id="27e86-139">Bir sınama dağıtımı için HPC Pack Merhaba baş düğümüne yükleyen hello varsayılan Microsoft HPC Azure otomatik olarak imzalanan sertifika kullan ve bu sertifikayı tooyour Azure aboneliği karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="27e86-139">For a test deployment, you can use hello Default Microsoft HPC Azure self-signed certificate that HPC Pack installs on hello head node, and then upload that certificate tooyour Azure subscription.</span></span> <span data-ttu-id="27e86-140">Merhaba seçenekleri ve adımlar için bkz: [TechNet Kitaplığı Kılavuzu](https://technet.microsoft.com/library/gg481759.aspx).</span><span class="sxs-lookup"><span data-stu-id="27e86-140">For options and steps, see hello [TechNet Library guidance](https://technet.microsoft.com/library/gg481759.aspx).</span></span>

  2. <span data-ttu-id="27e86-141">Çalıştırma **regedit** hello baş düğümünde tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo gidin ve bir dize değeri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="27e86-141">Run **regedit** on hello head node, go tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo, and add a string value.</span></span> <span data-ttu-id="27e86-142">Merhaba değer adı çok Ayarla "Parmak izi" ve değer veri toohello sertifikanın parmak izini hello 1. adımda.</span><span class="sxs-lookup"><span data-stu-id="27e86-142">Set hello Value name too“ThumbPrint”, and Value data toohello thumbprint of hello certificate in Step 1.</span></span>

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a><span data-ttu-id="27e86-143">HPC PowerShell komutları tooset hello AutoGrowShrink özelliği</span><span class="sxs-lookup"><span data-stu-id="27e86-143">HPC PowerShell commands tooset hello AutoGrowShrink property</span></span>
<span data-ttu-id="27e86-144">Aşağıdaki örnek HPC PowerShell komutları tooset olan **AutoGrowShrink** ve tootune davranışını ek parametrelere sahip.</span><span class="sxs-lookup"><span data-stu-id="27e86-144">Following are sample HPC PowerShell commands tooset **AutoGrowShrink** and tootune its behavior with additional parameters.</span></span> <span data-ttu-id="27e86-145">Bkz: [AutoGrowShrink parametreleri](#AutoGrowShrink-parameters) hello ayarlarının tam listesi için bu makalede daha sonra.</span><span class="sxs-lookup"><span data-stu-id="27e86-145">See [AutoGrowShrink parameters](#AutoGrowShrink-parameters) later in this article for hello complete list of settings.</span></span>

<span data-ttu-id="27e86-146">toorun Bu komutlar, başlangıç HPC PowerShell'i hello küme baş düğümünde yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="27e86-146">toorun these commands, start HPC PowerShell on hello cluster head node as an administrator.</span></span>

<span data-ttu-id="27e86-147">**tooenable hello AutoGrowShrink özelliği**</span><span class="sxs-lookup"><span data-stu-id="27e86-147">**tooenable hello AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

<span data-ttu-id="27e86-148">**toodisable hello AutoGrowShrink özelliği**</span><span class="sxs-lookup"><span data-stu-id="27e86-148">**toodisable hello AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

<span data-ttu-id="27e86-149">**toochange hello aralığı dakika cinsinden Büyüt**</span><span class="sxs-lookup"><span data-stu-id="27e86-149">**toochange hello grow interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

<span data-ttu-id="27e86-150">**toochange hello aralığı dakika cinsinden Daralt**</span><span class="sxs-lookup"><span data-stu-id="27e86-150">**toochange hello shrink interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

<span data-ttu-id="27e86-151">**tooview hello geçerli yapılandırmasını AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="27e86-151">**tooview hello current configuration of AutoGrowShrink**</span></span>

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

<span data-ttu-id="27e86-152">**tooexclude düğüm AutoGrowShrink gruplarından**</span><span class="sxs-lookup"><span data-stu-id="27e86-152">**tooexclude node groups from AutoGrowShrink**</span></span>

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> <span data-ttu-id="27e86-153">Bu parametre HPC Pack 2016'dan itibaren desteklenir</span><span class="sxs-lookup"><span data-stu-id="27e86-153">This parameter is supported starting in HPC Pack 2016</span></span>
>

### <a name="autogrowshrink-parameters"></a><span data-ttu-id="27e86-154">AutoGrowShrink parametreleri</span><span class="sxs-lookup"><span data-stu-id="27e86-154">AutoGrowShrink parameters</span></span>
<span data-ttu-id="27e86-155">Merhaba hello kullanarak değiştirebilirsiniz AutoGrowShrink Parametreler şunlardır **kümesi HpcClusterProperty** komutu.</span><span class="sxs-lookup"><span data-stu-id="27e86-155">hello following are AutoGrowShrink parameters that you can modify by using hello **Set-HpcClusterProperty** command.</span></span>

* <span data-ttu-id="27e86-156">**EnableGrowShrink** - geçiş tooenable veya hello devre dışı **AutoGrowShrink** özelliği.</span><span class="sxs-lookup"><span data-stu-id="27e86-156">**EnableGrowShrink** - Switch tooenable or disable hello **AutoGrowShrink** property.</span></span>
* <span data-ttu-id="27e86-157">**ParamSweepTasksPerCore** -parametrik tarama sayısı toogrow bir çekirdek görevler.</span><span class="sxs-lookup"><span data-stu-id="27e86-157">**ParamSweepTasksPerCore** - Number of parametric sweep tasks toogrow one core.</span></span> <span data-ttu-id="27e86-158">Merhaba, görev başına bir çekirdek toogrow varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="27e86-158">hello default is toogrow one core per task.</span></span>

  > [!NOTE]
  > <span data-ttu-id="27e86-159">HPC Pack QFE KB3134307 değişiklikleri **ParamSweepTasksPerCore** çok**TasksPerResourceUnit**.</span><span class="sxs-lookup"><span data-stu-id="27e86-159">HPC Pack QFE KB3134307 changes **ParamSweepTasksPerCore** too**TasksPerResourceUnit**.</span></span> <span data-ttu-id="27e86-160">Merhaba iş kaynak türüne göre ve düğüm, yuva veya çekirdek olabilir.</span><span class="sxs-lookup"><span data-stu-id="27e86-160">It is based on hello job resource type and can be node, socket, or core.</span></span>
  >
  >
* <span data-ttu-id="27e86-161">**GrowThreshold** -kuyruğa alınmış görevlerin tootrigger otomatik büyüme eşiği.</span><span class="sxs-lookup"><span data-stu-id="27e86-161">**GrowThreshold** - Threshold of queued tasks tootrigger automatic growth.</span></span> <span data-ttu-id="27e86-162">Merhaba varsayılan 1, 1 veya daha fazla görevlerinde sıraya alınan durum hello anlamına gelir, düğümlerin otomatik olarak büyütün.</span><span class="sxs-lookup"><span data-stu-id="27e86-162">hello default is 1, which means that if there are 1 or more tasks in hello queued state, automatically grow nodes.</span></span>
* <span data-ttu-id="27e86-163">**GrowInterval** -dakika tootrigger otomatik büyüme aralığı.</span><span class="sxs-lookup"><span data-stu-id="27e86-163">**GrowInterval** - Interval in minutes tootrigger automatic growth.</span></span> <span data-ttu-id="27e86-164">Merhaba varsayılan aralığı 5 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="27e86-164">hello default interval is 5 minutes.</span></span>
* <span data-ttu-id="27e86-165">**ShrinkInterval** -dakika tootrigger otomatik küçültme içinde aralığı.</span><span class="sxs-lookup"><span data-stu-id="27e86-165">**ShrinkInterval** - Interval in minutes tootrigger automatic shrinking.</span></span> <span data-ttu-id="27e86-166">Merhaba varsayılan zaman aralığı olan 5 dakika. |</span><span class="sxs-lookup"><span data-stu-id="27e86-166">hello default interval is 5 minutes.|</span></span>
* <span data-ttu-id="27e86-167">**ShrinkIdleTimes** -sürekli denetimleri tooshrink tooindicate hello düğüm sayısını boş.</span><span class="sxs-lookup"><span data-stu-id="27e86-167">**ShrinkIdleTimes** - Number of continuous checks tooshrink tooindicate hello nodes are idle.</span></span> <span data-ttu-id="27e86-168">Merhaba, 3 kez varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="27e86-168">hello default is 3 times.</span></span> <span data-ttu-id="27e86-169">Örneğin, hello **ShrinkInterval** 5 dakika, HPC Pack Merhaba düğümü 5 dakikada bir boş olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="27e86-169">For example, if hello **ShrinkInterval** is 5 minutes, HPC Pack checks whether hello node is idle every 5 minutes.</span></span> <span data-ttu-id="27e86-170">3 sürekli (15 dakika) denetledikten sonra hello düğümleri hello boşta durumunda ise, HPC Pack bu düğüme küçültür.</span><span class="sxs-lookup"><span data-stu-id="27e86-170">If hello nodes are in hello idle state after 3 continuous checks (15 minutes), then HPC Pack shrinks that node.</span></span>
* <span data-ttu-id="27e86-171">**ExtraNodesGrowRatio** -ileti geçirme arabirimi (MPI) işleri için düğümleri toogrow ek yüzdesi.</span><span class="sxs-lookup"><span data-stu-id="27e86-171">**ExtraNodesGrowRatio** - Additional percentage of nodes toogrow for Message Passing Interface (MPI) jobs.</span></span> <span data-ttu-id="27e86-172">HPC Pack %1 MPI işlerini için düğümleri büyür anlamına gelir 1 Hello varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="27e86-172">hello default value is 1, which means that HPC Pack grows nodes 1% for MPI jobs.</span></span>
* <span data-ttu-id="27e86-173">**GrowByMin** -hello minimum kaynaklardaki hello iş için gereken hello otomatik büyüme İlkesi tabanlı olup olmadığını tooindicate geçin.</span><span class="sxs-lookup"><span data-stu-id="27e86-173">**GrowByMin** - Switch tooindicate whether hello autogrow policy is based on hello minimum resources required for hello job.</span></span> <span data-ttu-id="27e86-174">Merhaba varsayılan HPC Pack Merhaba en fazla kaynak hello işleri için gerekli temel işleri için düğümleri büyür başka bir deyişle, false değeridir.</span><span class="sxs-lookup"><span data-stu-id="27e86-174">hello default is false, which means that HPC Pack grows nodes for jobs based on hello maximum resources required for hello jobs.</span></span>
* <span data-ttu-id="27e86-175">**SoaJobGrowThreshold** -eşiğini gelen SOA istekleri tootrigger hello otomatik büyüme işlemi.</span><span class="sxs-lookup"><span data-stu-id="27e86-175">**SoaJobGrowThreshold** - Threshold of incoming SOA requests tootrigger hello automatic grow process.</span></span> <span data-ttu-id="27e86-176">50000 Hello varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="27e86-176">hello default value is 50000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="27e86-177">Bu parametre, HPC Pack 2012 R2 güncelleştirme 3'te itibaren desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="27e86-177">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
  >
* <span data-ttu-id="27e86-178">**SoaRequestsPerCore** -toogrow bir çekirdek istekleri Gelen SOA sayısı.</span><span class="sxs-lookup"><span data-stu-id="27e86-178">**SoaRequestsPerCore** -Number of incoming SOA requests toogrow one core.</span></span> <span data-ttu-id="27e86-179">20000 Hello varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="27e86-179">hello default value is 20000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="27e86-180">Bu parametre, HPC Pack 2012 R2 güncelleştirme 3'te itibaren desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="27e86-180">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
* <span data-ttu-id="27e86-181">**ExcludeNodeGroups** – hello düğümler belirtilen düğüm grupları otomatik olarak Büyüt ve daraltma.</span><span class="sxs-lookup"><span data-stu-id="27e86-181">**ExcludeNodeGroups** – Nodes in hello specified node groups do not automatically grow and shrink.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="27e86-182">Bu parametre, HPC Pack 2016'dan itibaren desteklenir.</span><span class="sxs-lookup"><span data-stu-id="27e86-182">This parameter is supported starting in HPC Pack 2016.</span></span>
  >

### <a name="mpi-example"></a><span data-ttu-id="27e86-183">MPI örneği</span><span class="sxs-lookup"><span data-stu-id="27e86-183">MPI example</span></span>
<span data-ttu-id="27e86-184">Varsayılan olarak, %1 HPC Pack büyür MPI işlerini için ek düğümleri (**ExtraNodesGrowRatio** too1 ayarlanır).</span><span class="sxs-lookup"><span data-stu-id="27e86-184">By default HPC Pack grows 1% extra nodes for MPI jobs (**ExtraNodesGrowRatio** is set too1).</span></span> <span data-ttu-id="27e86-185">Merhaba MPI birden çok düğüm gerektirebilir ve tüm düğümleri hazır olduğunuzda hello işi yalnızca çalıştırabilirsiniz nedenidir.</span><span class="sxs-lookup"><span data-stu-id="27e86-185">hello reason is that MPI may require multiple nodes, and hello job can only run when all nodes are ready.</span></span> <span data-ttu-id="27e86-186">Zaman zaman Azure düğümleri başladığında, tek bir düğüm o düğümü tooget için hazır beklerken boşta diğer düğümleri toobe neden diğerlerine göre daha fazla zaman toostart gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="27e86-186">When Azure starts nodes, occasionally one node might need more time toostart than others, causing other nodes toobe idle while waiting for that node tooget ready.</span></span> <span data-ttu-id="27e86-187">Ek düğümler büyüyen HPC Pack bu kaynak bekleme süresini azaltır ve maliyetleri potansiyel olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="27e86-187">By growing extra nodes, HPC Pack reduces this resource waiting time, and potentially saves costs.</span></span> <span data-ttu-id="27e86-188">tooincrease hello yüzdesi ek düğümleri MPI işlerini (örneğin, too10%) için benzer bir komutu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="27e86-188">tooincrease hello percentage of extra nodes for MPI jobs (for example, too10%), run a command similar to</span></span>

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a><span data-ttu-id="27e86-189">SOA örneği</span><span class="sxs-lookup"><span data-stu-id="27e86-189">SOA example</span></span>
<span data-ttu-id="27e86-190">Varsayılan olarak, **SoaJobGrowThreshold** too50000 ayarlanır ve **SoaRequestsPerCore** too200000 ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="27e86-190">By default, **SoaJobGrowThreshold** is set too50000 and **SoaRequestsPerCore** is set too200000.</span></span> <span data-ttu-id="27e86-191">Bir SOA işi 70000 isteği göndermek, bir Sıraya alınan görev olduğunu ve gelen istekleri 70000.</span><span class="sxs-lookup"><span data-stu-id="27e86-191">If you submit one SOA job with 70000 requests, there is one queued task and incoming requests are 70000.</span></span> <span data-ttu-id="27e86-192">Bu durumda Hello görev sıraya alındı ve (70000-50000) gelen istekler için büyür HPC Pack 1 çekirdek büyür / 20000 = 1 çekirdek, bu nedenle, toplam bu SOA işi için 2 Çekirdek büyür.</span><span class="sxs-lookup"><span data-stu-id="27e86-192">In this case HPC Pack grows 1 core for hello queued task, and for incoming requests, grows (70000 - 50000)/20000 = 1 core, so in total grows 2 cores for this SOA job.</span></span>

## <a name="run-hello-azureautogrowshrinkps1-script"></a><span data-ttu-id="27e86-193">Merhaba AzureAutoGrowShrink.ps1 komut dosyasını çalıştır</span><span class="sxs-lookup"><span data-stu-id="27e86-193">Run hello AzureAutoGrowShrink.ps1 script</span></span>
### <a name="prerequisites"></a><span data-ttu-id="27e86-194">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="27e86-194">Prerequisites</span></span>

* <span data-ttu-id="27e86-195">**HPC Pack 2012 R2 güncelleştirme 1 veya sonraki bir küme** - hello **AzureAutoGrowShrink.ps1** betik hello % CCP_HOME % bin klasörüne yüklenir.</span><span class="sxs-lookup"><span data-stu-id="27e86-195">**HPC Pack 2012 R2 Update 1 or later cluster** - hello **AzureAutoGrowShrink.ps1** script is installed in hello %CCP_HOME%bin folder.</span></span> <span data-ttu-id="27e86-196">Merhaba küme baş düğümüne olabilir ya da şirket içi dağıtılan veya bir Azure VM.</span><span class="sxs-lookup"><span data-stu-id="27e86-196">hello cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="27e86-197">Bkz: [HPC paketi ile karma küme ayarlama](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget bir şirket içi baş düğüm ve Azure "veri bloğu" düğümleri ile başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="27e86-197">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="27e86-198">Merhaba bkz [HPC Pack Iaas dağıtım betiği](hpcpack-cluster-powershell-script.md) tooquickly Azure VM'de HPC paketi küme dağıtın veya kullanın bir [Azure Hızlı Başlangıç şablonu](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span><span class="sxs-lookup"><span data-stu-id="27e86-198">See hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) tooquickly deploy an HPC Pack cluster in Azure VMs, or use an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span></span>
* <span data-ttu-id="27e86-199">**Azure PowerShell 1.4.0** -hello komut dosyası şu anda Azure PowerShell belirli bu sürümünde bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="27e86-199">**Azure PowerShell 1.4.0** - hello script currently depends on this specific version of Azure PowerShell.</span></span>
* <span data-ttu-id="27e86-200">**Azure ile bir küme düğümleri veri bloğu** -HPC Pack yüklü olduğu bir istemci bilgisayarı veya hello baş düğüm hello komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="27e86-200">**For a cluster with Azure burst nodes** - Run hello script on a client computer where HPC Pack is installed, or on hello head node.</span></span> <span data-ttu-id="27e86-201">Bir istemci bilgisayarda çalışıyorsa, değişken $env hello ayarlamak emin olun: CCP_SCHEDULER toopoint toohello baş düğüm.</span><span class="sxs-lookup"><span data-stu-id="27e86-201">If running on a client computer, ensure that you set hello variable $env:CCP_SCHEDULER toopoint toohello head node.</span></span> <span data-ttu-id="27e86-202">Hello Azure "veri bloğu" düğümleri toohello küme eklenmesi gerekir, ancak hello değil dağıtılan durum olabilir.</span><span class="sxs-lookup"><span data-stu-id="27e86-202">hello Azure “burst” nodes must be added toohello cluster, but they may be in hello Not-Deployed state.</span></span>
* <span data-ttu-id="27e86-203">**Azure VM'ler (Resource Manager dağıtım modeli) dağıtılan bir küme için** -Azure hello Resource Manager dağıtım modelinde dağıtılan VM'ler küme için hello komut dosyası Azure kimlik doğrulaması için iki yöntemi destekler: tooyour Azure hesabı oturum toorun hello komut dosyası her zaman (çalıştırarak `Login-AzureRmAccount`, veya bir hizmet asıl tooauthenticate bir sertifika ile yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="27e86-203">**For a cluster deployed in Azure VMs (Resource Manager deployment model)** - For a cluster of Azure VMs deployed in hello Resource Manager deployment model, hello script supports two methods for Azure authentication: sign in tooyour Azure account toorun hello script every time (by running `Login-AzureRmAccount`, or configure a service principal tooauthenticate with a certificate.</span></span> <span data-ttu-id="27e86-204">HPC Pack Merhaba komut dosyası sağlar **ConfigARMAutoGrowShrinkCert.ps** toocreate sertifika ile bir hizmet sorumlusu.</span><span class="sxs-lookup"><span data-stu-id="27e86-204">HPC Pack provides hello script **ConfigARMAutoGrowShrinkCert.ps** toocreate a service principal with certificate.</span></span> <span data-ttu-id="27e86-205">Merhaba betik bir Azure Active Directory (Azure AD) uygulama ve hizmet sorumlusu oluşturur ve hello katkıda bulunan rolü toohello hizmet sorumlusu atar.</span><span class="sxs-lookup"><span data-stu-id="27e86-205">hello script creates an Azure Active Directory (Azure AD) application and a service principal, and assigns hello Contributor role toohello service principal.</span></span> <span data-ttu-id="27e86-206">toorun hello komut dosyası, Azure PowerShell'i yönetici olarak başlatın ve hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="27e86-206">toorun hello script, start Azure PowerShell  as administrator and run hello following commands:</span></span>

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    <span data-ttu-id="27e86-207">Hakkında daha fazla ayrıntı için **ConfigARMAutoGrowShrinkCert.ps1**, çalışma `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span><span class="sxs-lookup"><span data-stu-id="27e86-207">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span></span>

* <span data-ttu-id="27e86-208">**Azure VM'ler (Klasik dağıtım modeli) dağıtılan bir küme için** -hello üzerinde bağımlı olduğundan dolayı hello baş düğümünde VM hello komut dosyasını çalıştırmak **başlangıç HpcIaaSNode.ps1** ve **Stop-HpcIaaSNode.ps1**yüklü komut dosyaları.</span><span class="sxs-lookup"><span data-stu-id="27e86-208">**For a cluster deployed in Azure VMs (classic deployment model)** - Run hello script on hello head node VM, because it depends on hello **Start-HpcIaaSNode.ps1** and **Stop-HpcIaaSNode.ps1** scripts that are installed there.</span></span> <span data-ttu-id="27e86-209">Bu komut ayrıca bir Azure yönetim sertifikası gerektirir veya yayımlama ayarları dosyası (bkz [bir HPC Pack Yönet işlem düğümleri küme Azure'da](hpcpack-cluster-node-manage.md)).</span><span class="sxs-lookup"><span data-stu-id="27e86-209">Those scripts additionally require an Azure management certificate or publish settings file (see [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md)).</span></span> <span data-ttu-id="27e86-210">İşlem düğümü ihtiyacınız VM'ler zaten toohello küme eklenen tüm hello emin olun.</span><span class="sxs-lookup"><span data-stu-id="27e86-210">Make sure all hello compute node VMs you need are already added toohello cluster.</span></span> <span data-ttu-id="27e86-211">Bunlar hello durduruldu durumunda olabilir.</span><span class="sxs-lookup"><span data-stu-id="27e86-211">They may be in hello Stopped state.</span></span>



### <a name="syntax"></a><span data-ttu-id="27e86-212">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="27e86-212">Syntax</span></span>
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
### <a name="parameters"></a><span data-ttu-id="27e86-213">Parametreler</span><span class="sxs-lookup"><span data-stu-id="27e86-213">Parameters</span></span>
* <span data-ttu-id="27e86-214">**NodeTemplates** -hello düğümü şablonları toodefine adlarını hello hello düğümleri toogrow için kapsam ve daraltma.</span><span class="sxs-lookup"><span data-stu-id="27e86-214">**NodeTemplates** - Names of hello node templates toodefine hello scope for hello nodes toogrow and shrink.</span></span> <span data-ttu-id="27e86-215">Belirtilmezse, (hello varsayılan değer: @()) hello tüm düğümlerde **AzureNodes** düğüm grubu içinde olduğunda kapsam olan **NodeType** hello AzureNodes ve tüm düğümleri değerine sahip **ComputeNodes** düğüm grubu içinde olduğunda kapsam olan **NodeType** ComputeNodes değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="27e86-215">If not specified (hello default value is @()), all nodes in hello **AzureNodes** node group are in scope when **NodeType** has a value of AzureNodes, and all nodes in hello **ComputeNodes** node group are in scope when **NodeType** has a value of ComputeNodes.</span></span>
* <span data-ttu-id="27e86-216">**JobTemplates** -hello adlarını proje şablonları toodefine hello hello düğümleri toogrow kapsamın.</span><span class="sxs-lookup"><span data-stu-id="27e86-216">**JobTemplates** - Names of hello job templates toodefine hello scope for hello nodes toogrow.</span></span>
* <span data-ttu-id="27e86-217">**NodeType** - hello düğümü toogrow türünü ve daraltma.</span><span class="sxs-lookup"><span data-stu-id="27e86-217">**NodeType** - hello type of node toogrow and shrink.</span></span> <span data-ttu-id="27e86-218">Desteklenen değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="27e86-218">Supported values are:</span></span>

  * <span data-ttu-id="27e86-219">**AzureNodes** – bir şirket içi Azure PaaS (veri bloğu) düğümler için ya da Azure Iaas küme.</span><span class="sxs-lookup"><span data-stu-id="27e86-219">**AzureNodes** – for Azure PaaS (burst) nodes in an on-premises or Azure IaaS cluster.</span></span>
  * <span data-ttu-id="27e86-220">**ComputeNodes** - işlem düğümünde VM'ler yalnızca bir Azure Iaas kümesi.</span><span class="sxs-lookup"><span data-stu-id="27e86-220">**ComputeNodes** - for compute node VMs only in an Azure IaaS cluster.</span></span>

* <span data-ttu-id="27e86-221">**NumOfQueuedJobsPerNodeToGrow** -sıraya alınmış işlerin sayısı gerekli toogrow bir düğümü.</span><span class="sxs-lookup"><span data-stu-id="27e86-221">**NumOfQueuedJobsPerNodeToGrow** - Number of queued jobs required toogrow one node.</span></span>
* <span data-ttu-id="27e86-222">**NumOfQueuedJobsToGrowThreshold** -hello eşik sıraya alınan işleri toostart hello sayısı büyümesine işlemi.</span><span class="sxs-lookup"><span data-stu-id="27e86-222">**NumOfQueuedJobsToGrowThreshold** - hello threshold number of queued jobs toostart hello grow process.</span></span>
* <span data-ttu-id="27e86-223">**NumOfActiveQueuedTasksPerNodeToGrow** -etkin kuyruğa alınmış görevlerin hello sayısı gerekli toogrow bir düğümü.</span><span class="sxs-lookup"><span data-stu-id="27e86-223">**NumOfActiveQueuedTasksPerNodeToGrow** - hello number of active queued tasks required toogrow one node.</span></span> <span data-ttu-id="27e86-224">Varsa **NumOfQueuedJobsPerNodeToGrow** belirtilen 0'dan büyük bir değer ile bu parametre yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="27e86-224">If **NumOfQueuedJobsPerNodeToGrow** is specified with a value greater than 0, this parameter is ignored.</span></span>
* <span data-ttu-id="27e86-225">**NumOfActiveQueuedTasksToGrowThreshold** -hello eşik etkin kuyruğa alınmış görevlerin toostart hello sayısı büyümesine işlemi.</span><span class="sxs-lookup"><span data-stu-id="27e86-225">**NumOfActiveQueuedTasksToGrowThreshold** - hello threshold number of active queued tasks toostart hello grow process.</span></span>
* <span data-ttu-id="27e86-226">**NumOfInitialNodesToGrow** - hello kapsamdaki tüm hello düğüm gerekirse düğümleri toogrow en az sayıda ilk **değil dağıtılan** veya **durduruldu (Deallocated)**.</span><span class="sxs-lookup"><span data-stu-id="27e86-226">**NumOfInitialNodesToGrow** - hello initial minimum number of nodes toogrow if all hello nodes in scope are **Not-Deployed** or **Stopped (Deallocated)**.</span></span>
* <span data-ttu-id="27e86-227">**GrowCheckIntervalMins** -hello aralığı dakika arasında toogrow denetler.</span><span class="sxs-lookup"><span data-stu-id="27e86-227">**GrowCheckIntervalMins** - hello interval in minutes between checks toogrow.</span></span>
* <span data-ttu-id="27e86-228">**ShrinkCheckIntervalMins** -hello aralığı dakika arasında tooshrink denetler.</span><span class="sxs-lookup"><span data-stu-id="27e86-228">**ShrinkCheckIntervalMins** - hello interval in minutes between checks tooshrink.</span></span>
* <span data-ttu-id="27e86-229">**ShrinkCheckIdleTimes** -hello sürekli küçültme denetimlerinin sayısının (ayırarak **ShrinkCheckIntervalMins**) tooindicate hello düğümler boşta.</span><span class="sxs-lookup"><span data-stu-id="27e86-229">**ShrinkCheckIdleTimes** - hello number of continuous shrink checks (separated by **ShrinkCheckIntervalMins**) tooindicate hello nodes are idle.</span></span>
* <span data-ttu-id="27e86-230">**UseLastConfigurations** -hello bağımsız değişkeni dosyasında kaydedilen önceki yapılandırmaların hello.</span><span class="sxs-lookup"><span data-stu-id="27e86-230">**UseLastConfigurations** - hello previous configurations saved in hello argument file.</span></span>
* <span data-ttu-id="27e86-231">**ArgFile**- hello hello bağımsız değişkeni kullanılan dosyası toosave adını ve güncelleştirmek hello yapılandırmaları toorun hello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="27e86-231">**ArgFile**- hello name of hello argument file used toosave and update hello configurations toorun hello script.</span></span>
* <span data-ttu-id="27e86-232">**LogFilePrefix** -hello günlük dosyasının hello ön ek adı.</span><span class="sxs-lookup"><span data-stu-id="27e86-232">**LogFilePrefix** - hello prefix name of hello log file.</span></span> <span data-ttu-id="27e86-233">Bir yolu belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27e86-233">You can specify a path.</span></span> <span data-ttu-id="27e86-234">Varsayılan olarak hello günlüğü yazılı toohello geçerli çalışma dizini bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="27e86-234">By default hello log is written toohello current working directory.</span></span>

### <a name="example-1"></a><span data-ttu-id="27e86-235">Örnek 1</span><span class="sxs-lookup"><span data-stu-id="27e86-235">Example 1</span></span>
<span data-ttu-id="27e86-236">Merhaba aşağıdaki örnek Azure ile varsayılan AzureNode şablonu toogrow dağıtılan düğümleri bloğu ve otomatik olarak küçültme hello yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="27e86-236">hello following example configures hello Azure burst nodes deployed with the Default AzureNode Template toogrow and shrink automatically.</span></span> <span data-ttu-id="27e86-237">Tüm düğümleri başlangıçta hello varsa **değil dağıtılan** durumunda, en az 3 düğümleri başlatılacağı.</span><span class="sxs-lookup"><span data-stu-id="27e86-237">If all the nodes are initially in hello **Not-Deployed** state, at least 3 nodes are started.</span></span> <span data-ttu-id="27e86-238">Merhaba sıraya alınmış işlerin sayısı 8 aşarsa, kuyruğa alınmış işleri hello oranını kendi sayıyı aşıyor kadar hello komut dosyasını düğümleri başlatır **NumOfQueuedJobsPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="27e86-238">If hello number of queued jobs exceeds 8, hello script starts nodes until their number exceeds hello ratio of queued jobs to **NumOfQueuedJobsPerNodeToGrow**.</span></span> <span data-ttu-id="27e86-239">Bir düğüm 3 ardışık boşta zamanlarında boşta toobe bulunursa durdurulur.</span><span class="sxs-lookup"><span data-stu-id="27e86-239">If a node is found toobe idle in 3 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a><span data-ttu-id="27e86-240">Örnek 2</span><span class="sxs-lookup"><span data-stu-id="27e86-240">Example 2</span></span>
<span data-ttu-id="27e86-241">Merhaba aşağıdaki örnek Azure hello varsayılan ComputeNode şablonu toogrow ile dağıtılan düğümü VM'ler işlem ve otomatik olarak küçültme hello yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="27e86-241">hello following example configures hello Azure compute node VMs deployed with hello Default ComputeNode Template toogrow and shrink automatically.</span></span>
<span data-ttu-id="27e86-242">Merhaba varsayılan proje şablonu tarafından yapılandırılan hello işleri hello kümede iş yükü hello kapsamını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="27e86-242">hello jobs configured by hello Default job template define hello scope of the workload on hello cluster.</span></span> <span data-ttu-id="27e86-243">Tüm hello düğümleri başlangıçta durdurduysanız, en az 5 düğümleri başlatılır.</span><span class="sxs-lookup"><span data-stu-id="27e86-243">If all hello nodes are initially stopped, at least 5 nodes are started.</span></span> <span data-ttu-id="27e86-244">Etkin kuyruğa alınmış görevlerin Hello sayısı 15 aşarsa, kendi sayıyı aşıyor active kuyruğa alınmış görevlerin hello oranı çok kadar hello komut dosyasını düğümleri başlatır**NumOfActiveQueuedTasksPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="27e86-244">If hello number of active queued tasks exceeds 15, hello script starts nodes until their number exceeds hello ratio of active queued tasks too**NumOfActiveQueuedTasksPerNodeToGrow**.</span></span> <span data-ttu-id="27e86-245">Bir düğüm 10 ardışık boşta zamanlarında boşta toobe bulunursa durdurulur.</span><span class="sxs-lookup"><span data-stu-id="27e86-245">If a node is found toobe idle in 10 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
