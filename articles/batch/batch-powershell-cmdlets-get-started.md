---
title: "aaaGet için Azure Batch PowerShell ile başlatılan | Microsoft Docs"
description: "Hızlı Giriş toohello Azure PowerShell cmdlet'lerini toomanage Batch kaynaklarını kullanabilirsiniz."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: f9ad62c5-27bf-4e6b-a5bf-c5f5914e6199
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: powershell
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3e4d12e9c1e52a5b2db2dd44346edda93b7ef92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a><span data-ttu-id="f9086-103">Batch kaynaklarını PowerShell cmdlet'leriyle yönetme</span><span class="sxs-lookup"><span data-stu-id="f9086-103">Manage Batch resources with PowerShell cmdlets</span></span>

<span data-ttu-id="f9086-104">Hello Azure Batch PowerShell cmdlet'leri gerçekleştirebilir ve çoğu hello komut dosyası, yürütmek hello Batch API'leri ile aynı görevleri hello Azure portalı ve Azure komut satırı arabirimi (CLI) hello.</span><span class="sxs-lookup"><span data-stu-id="f9086-104">With hello Azure Batch PowerShell cmdlets, you can perform and script many of hello same tasks you carry out with hello Batch APIs, hello Azure portal, and hello Azure Command-Line Interface (CLI).</span></span> <span data-ttu-id="f9086-105">Batch hesaplarınızın toomanage kullanın ve havuzlar, işler ve görevler gibi Batch kaynaklarınızla iş bir hızlı giriş toohello cmdlet'leri budur.</span><span class="sxs-lookup"><span data-stu-id="f9086-105">This is a quick introduction toohello cmdlets you can use toomanage your Batch accounts and work with your Batch resources such as pools, jobs, and tasks.</span></span>

<span data-ttu-id="f9086-106">Batch cmdlet'leri ve ayrıntılı cmdlet sözdizimi tam listesi için bkz: Merhaba [Azure Batch cmdlet başvurusu](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="f9086-106">For a complete list of Batch cmdlets and detailed cmdlet syntax, see hello [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>

<span data-ttu-id="f9086-107">Bu makale, Azure PowerShell 3.0.0 sürümündeki cmdlet’leri temel almaktadır.</span><span class="sxs-lookup"><span data-stu-id="f9086-107">This article is based on cmdlets in Azure PowerShell version 3.0.0.</span></span> <span data-ttu-id="f9086-108">Azure PowerShell güncelleştirmenizi öneririz sık tootake avantajlarından hizmet güncelleştirmeleri ve geliştirmeleri.</span><span class="sxs-lookup"><span data-stu-id="f9086-108">We recommend that you update your Azure PowerShell frequently tootake advantage of service updates and enhancements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9086-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f9086-109">Prerequisites</span></span>
<span data-ttu-id="f9086-110">Aşağıdaki işlemleri toouse Azure PowerShell toomanage hello Batch kaynaklarınız gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="f9086-110">Perform hello following operations toouse Azure PowerShell toomanage your Batch resources.</span></span>

* [<span data-ttu-id="f9086-111">Azure PowerShell'i yükleme ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f9086-111">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* <span data-ttu-id="f9086-112">Merhaba çalıştırmak **Login-AzureRmAccount** cmdlet tooconnect tooyour abonelik (Merhaba hello Azure Resource Manager modülündeki Azure Batch cmdlet'leri sevk):</span><span class="sxs-lookup"><span data-stu-id="f9086-112">Run hello **Login-AzureRmAccount** cmdlet tooconnect tooyour subscription (hello Azure Batch cmdlets ship in hello Azure Resource Manager module):</span></span>
  
    `Login-AzureRmAccount`
* <span data-ttu-id="f9086-113">**Merhaba Batch sağlayıcı ad alanıyla kaydetme**.</span><span class="sxs-lookup"><span data-stu-id="f9086-113">**Register with hello Batch provider namespace**.</span></span> <span data-ttu-id="f9086-114">Bu işlem yalnızca gerçekleştirilen toobe gereken **abonelik başına bir kez**.</span><span class="sxs-lookup"><span data-stu-id="f9086-114">This operation only needs toobe performed **once per subscription**.</span></span>
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a><span data-ttu-id="f9086-115">Batch hesaplarını ve anahtarlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="f9086-115">Manage Batch accounts and keys</span></span>
### <a name="create-a-batch-account"></a><span data-ttu-id="f9086-116">Batch hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9086-116">Create a Batch account</span></span>
<span data-ttu-id="f9086-117">**New-AzureRmBatchAccount**, belirtilen kaynak grubunda bir Batch hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f9086-117">**New-AzureRmBatchAccount** creates a Batch account in a specified resource group.</span></span> <span data-ttu-id="f9086-118">Bir kaynak grubu zaten yoksa, hello çalıştırarak oluşturmak [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="f9086-118">If you don't already have a resource group, create one by running hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span> <span data-ttu-id="f9086-119">Hello Azure birini belirtin hello bölgelerde **konumu** "Orta ABD" gibi bir parametre.</span><span class="sxs-lookup"><span data-stu-id="f9086-119">Specify one of hello Azure regions in hello **Location** parameter, such as "Central US".</span></span> <span data-ttu-id="f9086-120">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f9086-120">For example:</span></span>

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

<span data-ttu-id="f9086-121">Ardından, hello kaynak grubunda hello hesap için bir adı belirterek, bir toplu işlem hesabı oluşturun <*account_name*> ve hello konumunu, hem de kaynak grubunuzun adını.</span><span class="sxs-lookup"><span data-stu-id="f9086-121">Then, create a Batch account in hello resource group, specifying a name for hello account in <*account_name*> and hello location and name of your resource group.</span></span> <span data-ttu-id="f9086-122">Merhaba Batch hesabı oluşturma bazı zaman toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="f9086-122">Creating hello Batch account can take some time toocomplete.</span></span> <span data-ttu-id="f9086-123">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f9086-123">For example:</span></span>

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> <span data-ttu-id="f9086-124">Merhaba toplu işlem hesabı adı benzersiz toohello hello kaynak grubunun Azure bölgesinde olmalıdır 3 ile 24 karakter arasında içerir ve yalnızca küçük harf ve sayı kullanın.</span><span class="sxs-lookup"><span data-stu-id="f9086-124">hello Batch account name must be unique toohello Azure region for hello resource group, contain between 3 and 24 characters, and use lowercase letters and numbers only.</span></span>
> 
> 

### <a name="get-account-access-keys"></a><span data-ttu-id="f9086-125">Hesap erişim anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="f9086-125">Get account access keys</span></span>
<span data-ttu-id="f9086-126">**Get-AzureRmBatchAccountKeys** bir Azure Batch hesabıyla ilişkili hello erişim anahtarlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f9086-126">**Get-AzureRmBatchAccountKeys** shows hello access keys associated with an Azure Batch account.</span></span> <span data-ttu-id="f9086-127">Örneğin, oluşturduğunuz hello hesabının tooget hello birincil ve ikincil anahtarları aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f9086-127">For example, run hello following tooget hello primary and secondary keys of hello account you created.</span></span>

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a><span data-ttu-id="f9086-128">Yeni erişim anahtarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9086-128">Generate a new access key</span></span>
<span data-ttu-id="f9086-129">**New-AzureRmBatchAccountKey**, Azure Batch hesabı için yeni bir birincil ya da ikincil hesap anahtarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f9086-129">**New-AzureRmBatchAccountKey** generates a new primary or secondary account key for an Azure Batch account.</span></span> <span data-ttu-id="f9086-130">Örneğin, Batch hesabınıza yeni bir birincil anahtar toogenerate yazın:</span><span class="sxs-lookup"><span data-stu-id="f9086-130">For example, toogenerate a new primary key for your Batch account, type:</span></span>

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> <span data-ttu-id="f9086-131">Yeni bir ikincil anahtar toogenerate belirtin "Secondary" Merhaba **KeyType** parametresi.</span><span class="sxs-lookup"><span data-stu-id="f9086-131">toogenerate a new secondary key, specify "Secondary" for hello **KeyType** parameter.</span></span> <span data-ttu-id="f9086-132">Tooregenerate hello birincil ve ikincil anahtarları ayrı olarak sahip.</span><span class="sxs-lookup"><span data-stu-id="f9086-132">You have tooregenerate hello primary and secondary keys separately.</span></span>
> 
> 

### <a name="delete-a-batch-account"></a><span data-ttu-id="f9086-133">Batch hesabını silme</span><span class="sxs-lookup"><span data-stu-id="f9086-133">Delete a Batch account</span></span>
<span data-ttu-id="f9086-134">**Remove-AzureRmBatchAccount** Batch hesabını siler.</span><span class="sxs-lookup"><span data-stu-id="f9086-134">**Remove-AzureRmBatchAccount** deletes a Batch account.</span></span> <span data-ttu-id="f9086-135">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f9086-135">For example:</span></span>

    Remove-AzureRmBatchAccount -AccountName <account_name>

<span data-ttu-id="f9086-136">İstendiğinde, tooremove hello hesap istediğinizi onaylayın.</span><span class="sxs-lookup"><span data-stu-id="f9086-136">When prompted, confirm you want tooremove hello account.</span></span> <span data-ttu-id="f9086-137">Hesabınızın kaldırılması bazı zaman toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="f9086-137">Account removal can take some time toocomplete.</span></span>

## <a name="create-a-batchaccountcontext-object"></a><span data-ttu-id="f9086-138">BatchAccountContext nesnesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9086-138">Create a BatchAccountContext object</span></span>
<span data-ttu-id="f9086-139">tooauthenticate kullanarak hello Batch PowerShell cmdlet'leri oluşturmak ve Batch havuzları, işleri, görevleri, yönetmek ve diğer kaynakları hesap adınızı ve anahtarları bir BatchAccountContext nesnesi toostore ilk oluştururken:</span><span class="sxs-lookup"><span data-stu-id="f9086-139">tooauthenticate using hello Batch PowerShell cmdlets when you create and manage Batch pools, jobs, tasks, and other resources, first create a BatchAccountContext object toostore your account name and keys:</span></span>

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

<span data-ttu-id="f9086-140">Merhaba BatchAccountContext nesnesi cmdlet'lere bu kullanım hello geçirdiğiniz **BatchContext** parametresi.</span><span class="sxs-lookup"><span data-stu-id="f9086-140">You pass hello BatchAccountContext object into cmdlets that use hello **BatchContext** parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="f9086-141">Varsayılan olarak, hello hesabın birincil anahtarı kimlik doğrulaması için kullanılır, ancak açıkça hello anahtar toouse BatchAccountContext nesnenizin değiştirerek seçebileceğiniz **Keyınuse** özelliği: `$context.KeyInUse = "Secondary"`.</span><span class="sxs-lookup"><span data-stu-id="f9086-141">By default, hello account's primary key is used for authentication, but you can explicitly select hello key toouse by changing your BatchAccountContext object’s **KeyInUse** property: `$context.KeyInUse = "Secondary"`.</span></span>
> 
> 

## <a name="create-and-modify-batch-resources"></a><span data-ttu-id="f9086-142">Batch kaynaklarını oluşturma ve değiştirme</span><span class="sxs-lookup"><span data-stu-id="f9086-142">Create and modify Batch resources</span></span>
<span data-ttu-id="f9086-143">Cmdlet'leri kullanın **New-AzureBatchPool**, **New-AzureBatchJob**, ve **New-AzureBatchTask** toocreate kaynakları Batch hesabı altında.</span><span class="sxs-lookup"><span data-stu-id="f9086-143">Use cmdlets such as **New-AzureBatchPool**, **New-AzureBatchJob**, and **New-AzureBatchTask** toocreate resources under a Batch account.</span></span> <span data-ttu-id="f9086-144">Cmdlet'leri vardır **Get -** ve **Set -** cmdlet'leri tooupdate hello var olan kaynakların özelliklerini ve **Remove -** cmdlet'leri tooremove kaynakları Batch hesabı altında.</span><span class="sxs-lookup"><span data-stu-id="f9086-144">There are corresponding **Get-** and **Set-** cmdlets tooupdate hello properties of existing resources, and  **Remove-** cmdlets tooremove resources under a Batch account.</span></span>

<span data-ttu-id="f9086-145">Bu cmdlet'lerin çoğu toplama toopassing BatchContext nesne kullanırken, toocreate gerekir veya hello aşağıdaki örnekte gösterildiği gibi ayrıntılı kaynak ayarlarını içeren nesneleri geçirin.</span><span class="sxs-lookup"><span data-stu-id="f9086-145">When using many of these cmdlets, in addition toopassing a BatchContext object, you need toocreate or pass objects that contain detailed resource settings, as shown in hello following example.</span></span> <span data-ttu-id="f9086-146">Bkz: hello ayrıntılı ek örnekler için her cmdlet için Yardım.</span><span class="sxs-lookup"><span data-stu-id="f9086-146">See hello detailed help for each cmdlet for additional examples.</span></span>

### <a name="create-a-batch-pool"></a><span data-ttu-id="f9086-147">Batch havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9086-147">Create a Batch pool</span></span>
<span data-ttu-id="f9086-148">Merhaba hello işletim sisteminde işlem için düğümleri oluştururken veya güncelleştirirken bir Batch havuzu hello bulut hizmet yapılandırması veya hello sanal makine yapılandırması seçmeniz (bkz [Batch özelliklerine genel bakış](batch-api-basics.md#pool)).</span><span class="sxs-lookup"><span data-stu-id="f9086-148">When creating or updating a Batch pool, you select either hello cloud service configuration or hello virtual machine configuration for hello operating system on hello compute nodes (see [Batch feature overview](batch-api-basics.md#pool)).</span></span> <span data-ttu-id="f9086-149">Merhaba bulut hizmeti yapılandırması belirtirseniz, işlem düğümleriniz hello biriyle görüntüsü [Azure konuk işletim sistemi sürümleri](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span><span class="sxs-lookup"><span data-stu-id="f9086-149">If you specify hello cloud service configuration, your compute nodes are imaged with one of hello [Azure Guest OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span></span> <span data-ttu-id="f9086-150">Merhaba sanal makine yapılandırması belirtirseniz, ya da hello birini desteklenen Linux veya Windows VM görüntüleri listelenen hello belirtebilirsiniz [Azure Virtual Machines Marketi][vm_marketplace], ya da özel bir sağlayın hazırladığınız resim.</span><span class="sxs-lookup"><span data-stu-id="f9086-150">If you specify hello virtual machine configuration, you can either specify one of hello supported Linux or Windows VM images listed in hello [Azure Virtual Machines Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span>

<span data-ttu-id="f9086-151">Çalıştırdığınızda **New-AzureBatchPool**, hello işletim sistemi ayarlarını bir PSCloudServiceConfiguration veya PSVirtualMachineConfiguration nesnesine geçirin.</span><span class="sxs-lookup"><span data-stu-id="f9086-151">When you run **New-AzureBatchPool**, pass hello operating system settings in a PSCloudServiceConfiguration or PSVirtualMachineConfiguration object.</span></span> <span data-ttu-id="f9086-152">Örneğin, hello aşağıdaki cmdlet'i yeni bir Batch havuzu boyutu küçük işlem düğümlerine hello bulut hizmeti yapılandırması, hello en son işletim sisteminin aile 3 sürümüyle (Windows Server 2012) ile görüntüsü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f9086-152">For example, hello following cmdlet creates a new Batch pool with size Small compute nodes in hello cloud service configuration, imaged with hello latest operating system version of family 3 (Windows Server 2012).</span></span> <span data-ttu-id="f9086-153">Burada, hello **CloudServiceConfiguration** parametresi belirtir hello *$configuration* hello PSCloudServiceConfiguration nesne değişkeni.</span><span class="sxs-lookup"><span data-stu-id="f9086-153">Here, hello **CloudServiceConfiguration** parameter specifies hello *$configuration* variable as hello PSCloudServiceConfiguration object.</span></span> <span data-ttu-id="f9086-154">Merhaba **BatchContext** parametresi, önceden tanımlanmış bir değişken belirtir *$context* hello BatchAccountContext nesnesi olarak.</span><span class="sxs-lookup"><span data-stu-id="f9086-154">hello **BatchContext** parameter specifies a previously defined variable *$context* as hello BatchAccountContext object.</span></span>

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

<span data-ttu-id="f9086-155">Merhaba hedef hello yeni havuzdaki işlem düğümleri sayısı ölçeklendirmeyle belirlenir.</span><span class="sxs-lookup"><span data-stu-id="f9086-155">hello target number of compute nodes in hello new pool is determined by an autoscaling formula.</span></span> <span data-ttu-id="f9086-156">Bu durumda, hello yalnızca formülüdür **$TargetDedicated = 4**, hello hello havuzdaki işlem düğümleri sayısını gösteren: 4 en fazla.</span><span class="sxs-lookup"><span data-stu-id="f9086-156">In this case, hello formula is simply **$TargetDedicated=4**, indicating hello number of compute nodes in hello pool is 4 at most.</span></span>

## <a name="query-for-pools-jobs-tasks-and-other-details"></a><span data-ttu-id="f9086-157">Havuzlar, işler, görevler ve diğer ayrıntılar için sorgulama</span><span class="sxs-lookup"><span data-stu-id="f9086-157">Query for pools, jobs, tasks, and other details</span></span>
<span data-ttu-id="f9086-158">Cmdlet'leri kullanın **Get-AzureBatchPool**, **Get-AzureBatchJob**, ve **Get-AzureBatchTask** bir Batch hesabı altında oluşturulan varlıkların tooquery.</span><span class="sxs-lookup"><span data-stu-id="f9086-158">Use cmdlets such as **Get-AzureBatchPool**, **Get-AzureBatchJob**, and **Get-AzureBatchTask** tooquery for entities created under a Batch account.</span></span>

### <a name="query-for-data"></a><span data-ttu-id="f9086-159">Verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="f9086-159">Query for data</span></span>
<span data-ttu-id="f9086-160">Bir örnek olarak kullanabilirsiniz **Get-AzureBatchPools** toofind havuzlarınızı.</span><span class="sxs-lookup"><span data-stu-id="f9086-160">As an example, use **Get-AzureBatchPools** toofind your pools.</span></span> <span data-ttu-id="f9086-161">Varsayılan olarak, hesabınız altındaki tüm havuzlarla ilgili bu sorgular zaten hello BatchAccountContext nesnesinde depolanır *$context*:</span><span class="sxs-lookup"><span data-stu-id="f9086-161">By default this queries for all pools under your account, assuming you already stored hello BatchAccountContext object in *$context*:</span></span>

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a><span data-ttu-id="f9086-162">OData filtresini kullanma</span><span class="sxs-lookup"><span data-stu-id="f9086-162">Use an OData filter</span></span>
<span data-ttu-id="f9086-163">Hello kullanarak bir OData filtresi sağlayabilirsiniz **filtre** parametresi toofind yalnızca ilgilendiğiniz nesneleri hello.</span><span class="sxs-lookup"><span data-stu-id="f9086-163">You can supply an OData filter using hello **Filter** parameter toofind only hello objects you’re interested in.</span></span> <span data-ttu-id="f9086-164">Örneğin, kimlikleri “myPool” ile başlayan tüm havuzları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9086-164">For example, you can find all pools with ids starting with “myPool”:</span></span>

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

<span data-ttu-id="f9086-165">Bu yöntem, yerel bir işlem hattında "Where-Object" kullanmak kadar esnek değildir.</span><span class="sxs-lookup"><span data-stu-id="f9086-165">This method is not as flexible as using “Where-Object” in a local pipeline.</span></span> <span data-ttu-id="f9086-166">Ancak, böylece tüm filtreleme Internet bant genişliği korunarak hello sunucu tarafında gerçekleşir hello sorgu toohello Batch hizmeti doğrudan gönderilir.</span><span class="sxs-lookup"><span data-stu-id="f9086-166">However, hello query gets sent toohello Batch service directly so that all filtering happens on hello server side, saving Internet bandwidth.</span></span>

### <a name="use-hello-id-parameter"></a><span data-ttu-id="f9086-167">Merhaba kimlik parametresini kullanma</span><span class="sxs-lookup"><span data-stu-id="f9086-167">Use hello Id parameter</span></span>
<span data-ttu-id="f9086-168">Toouse hello alternatif tooan OData filtredir **kimliği** parametresi.</span><span class="sxs-lookup"><span data-stu-id="f9086-168">An alternative tooan OData filter is toouse hello **Id** parameter.</span></span> <span data-ttu-id="f9086-169">"myPool" kimliğine sahip belirli bir havuzu tooquery:</span><span class="sxs-lookup"><span data-stu-id="f9086-169">tooquery for a specific pool with id "myPool":</span></span>

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

<span data-ttu-id="f9086-170">Merhaba **kimliği** parametresi, yalnızca tam kimlik aramasını, joker karakter veya OData stili filtreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="f9086-170">hello **Id** parameter supports only full-id search, not wildcards or OData-style filters.</span></span>

### <a name="use-hello-maxcount-parameter"></a><span data-ttu-id="f9086-171">Merhaba MaxCount parametresini kullanma</span><span class="sxs-lookup"><span data-stu-id="f9086-171">Use hello MaxCount parameter</span></span>
<span data-ttu-id="f9086-172">Varsayılan olarak, her cmdlet en çok 1000 nesne döndürür.</span><span class="sxs-lookup"><span data-stu-id="f9086-172">By default, each cmdlet returns a maximum of 1000 objects.</span></span> <span data-ttu-id="f9086-173">Bu sınıra ulaştıysanız, daha az nesne filtre toobring daraltın veya hello kullanarak en açık olarak ayarlanıp **MaxCount** parametresi.</span><span class="sxs-lookup"><span data-stu-id="f9086-173">If you reach this limit, either refine your filter toobring back fewer objects, or explicitly set a maximum using hello **MaxCount** parameter.</span></span> <span data-ttu-id="f9086-174">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f9086-174">For example:</span></span>

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

<span data-ttu-id="f9086-175">tooremove hello üst sınır ayarlayın **MaxCount** too0 veya daha az.</span><span class="sxs-lookup"><span data-stu-id="f9086-175">tooremove hello upper bound, set **MaxCount** too0 or less.</span></span>

### <a name="use-hello-powershell-pipeline"></a><span data-ttu-id="f9086-176">Merhaba PowerShell işlem hattını kullanma</span><span class="sxs-lookup"><span data-stu-id="f9086-176">Use hello PowerShell pipeline</span></span>
<span data-ttu-id="f9086-177">Batch cmdlet'leri hello PowerShell ardışık düzen toosend verileri cmdlet'ler arasında yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9086-177">Batch cmdlets can leverage hello PowerShell pipeline toosend data between cmdlets.</span></span> <span data-ttu-id="f9086-178">Bu, aynı olarak belirten bir parametre ancak birden çok varlık ile daha kolay çalışma yapar efekt hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f9086-178">This has hello same effect as specifying a parameter, but makes working with multiple entities easier.</span></span>

<span data-ttu-id="f9086-179">Örneğin, hesabınızın altındaki tüm görevleri bulup görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="f9086-179">For example, find and display all tasks under your account:</span></span>

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

<span data-ttu-id="f9086-180">Havuzdaki her işlem düğümünü yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="f9086-180">Restart (reboot) every compute node in a pool:</span></span>

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a><span data-ttu-id="f9086-181">Uygulama paketi yönetimi</span><span class="sxs-lookup"><span data-stu-id="f9086-181">Application package management</span></span>
<span data-ttu-id="f9086-182">Uygulama paketleri toodeploy uygulamaları toohello işlem düğümlerine basitleştirilmiş bir yolunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="f9086-182">Application packages provide a simplified way toodeploy applications toohello compute nodes in your pools.</span></span> <span data-ttu-id="f9086-183">Hello Batch PowerShell cmdlet'leri ile karşıya yükleme ve uygulama paketleri Batch hesabınızı yönetmek ve paketi sürümleri toocompute düğümlerini dağıtmak.</span><span class="sxs-lookup"><span data-stu-id="f9086-183">With hello Batch PowerShell cmdlets, you can upload and manage application packages in your Batch account, and deploy package versions toocompute nodes.</span></span>

<span data-ttu-id="f9086-184">Bir uygulama **oluşturun**:</span><span class="sxs-lookup"><span data-stu-id="f9086-184">**Create** an application:</span></span>

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

<span data-ttu-id="f9086-185">Bir uygulama paketi **ekleyin**:</span><span class="sxs-lookup"><span data-stu-id="f9086-185">**Add** an application package:</span></span>

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

<span data-ttu-id="f9086-186">Set hello **varsayılan sürüm** hello uygulama için:</span><span class="sxs-lookup"><span data-stu-id="f9086-186">Set hello **default version** for hello application:</span></span>

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

<span data-ttu-id="f9086-187">Uygulamanın paketlerini **listeleme**</span><span class="sxs-lookup"><span data-stu-id="f9086-187">**List** an application's packages</span></span>

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

<span data-ttu-id="f9086-188">Uygulama paketini **silme**</span><span class="sxs-lookup"><span data-stu-id="f9086-188">**Delete** an application package</span></span>

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

<span data-ttu-id="f9086-189">Uygulamayı **silme**</span><span class="sxs-lookup"><span data-stu-id="f9086-189">**Delete** an application</span></span>

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> <span data-ttu-id="f9086-190">Merhaba uygulaması silmeden önce tüm uygulamanın uygulama paketi sürümleri silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9086-190">You must delete all of an application's application package versions before you delete hello application.</span></span> <span data-ttu-id="f9086-191">Şu anda uygulama paketleri olan bir uygulama toodelete çalışırsanız 'Çakışma' hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="f9086-191">You will receive a 'Conflict' error if you try toodelete an application that currently has application packages.</span></span>
> 
> 

### <a name="deploy-an-application-package"></a><span data-ttu-id="f9086-192">Uygulama paketi dağıtma</span><span class="sxs-lookup"><span data-stu-id="f9086-192">Deploy an application package</span></span>
<span data-ttu-id="f9086-193">Bir havuz oluşturduğunuzda dağıtım için bir veya daha fazla uygulama paketi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9086-193">You can specify one or more application packages for deployment when you create a pool.</span></span> <span data-ttu-id="f9086-194">Havuz oluşturma sırasında bir paket belirtmeniz hello düğümü birleştirmeler havuzu olarak dağıtılan tooeach düğümü olur.</span><span class="sxs-lookup"><span data-stu-id="f9086-194">When you specify a package at pool creation time, it is deployed tooeach node as hello node joins pool.</span></span> <span data-ttu-id="f9086-195">Paketler ayrıca bir düğüm yeniden başlatıldığında veya yeniden görüntüsü oluşturulduğunda dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="f9086-195">Packages are also deployed when a node is rebooted or reimaged.</span></span>

<span data-ttu-id="f9086-196">Merhaba belirtin `-ApplicationPackageReference` hello havuzuna Katıl gibi bir uygulama paketi toohello havuzun düğümleri havuzu toodeploy oluştururken seçeneği.</span><span class="sxs-lookup"><span data-stu-id="f9086-196">Specify hello `-ApplicationPackageReference` option when creating a pool toodeploy an application package toohello pool's nodes as they join hello pool.</span></span> <span data-ttu-id="f9086-197">İlk olarak, oluşturma bir **PSApplicationPackageReference** nesne ve istediğiniz toodeploy toohello havuzunun işlem düğümlerini hello uygulama kimliği ve Paket sürümü ile yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="f9086-197">First, create a **PSApplicationPackageReference** object, and configure it with hello application Id and package version you want toodeploy toohello pool's compute nodes:</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

<span data-ttu-id="f9086-198">Şimdi hello havuzu oluşturun ve bağımsız değişkeni toohello hello gibi hello paket başvuru nesnesi belirtmeniz `ApplicationPackageReferences` seçeneği:</span><span class="sxs-lookup"><span data-stu-id="f9086-198">Now create hello pool, and specify hello package reference object as hello argument toohello `ApplicationPackageReferences` option:</span></span>

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

<span data-ttu-id="f9086-199">Uygulama paketleri hakkında daha fazla bilgi bulabilirsiniz [Batch uygulama paketleriyle uygulama toocompute düğümlerini dağıtmak](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="f9086-199">You can find more information on application packages in [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9086-200">Yapmanız gerekenler [bir Azure depolama hesabı bağlantı](#linked-storage-account-autostorage) tooyour Batch uygulama paketleri toouse hesap.</span><span class="sxs-lookup"><span data-stu-id="f9086-200">You must [link an Azure Storage account](#linked-storage-account-autostorage) tooyour Batch account toouse application packages.</span></span>
> 
> 

### <a name="update-a-pools-application-packages"></a><span data-ttu-id="f9086-201">Bir havuzun uygulama paketlerini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="f9086-201">Update a pool's application packages</span></span>
<span data-ttu-id="f9086-202">tooan var olan bir havuzu, atanan tooupdate hello uygulamaları (uygulama kimliği ve Paket sürümü) istenen hello özelliklerle ilk PSApplicationPackageReference nesnesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="f9086-202">tooupdate hello applications assigned tooan existing pool, first create a PSApplicationPackageReference object with hello desired properties (application Id and package version):</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

<span data-ttu-id="f9086-203">Ardından, yığın hello havuzu almak, herhangi bir varolan paket temizleyin bizim yeni paketi Başvurusu Ekle ve hello Batch hizmeti hello yeni havuz ayarlarla güncelleştirmek:</span><span class="sxs-lookup"><span data-stu-id="f9086-203">Next, get hello pool from Batch, clear out any existing packages, add our new package reference, and update hello Batch service with hello new pool settings:</span></span>

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

<span data-ttu-id="f9086-204">Şimdi hello Batch hizmeti hello havuzunun özelliklerinde güncelleştirdik.</span><span class="sxs-lookup"><span data-stu-id="f9086-204">You've now updated hello pool's properties in hello Batch service.</span></span> <span data-ttu-id="f9086-205">tooactually hello yeni uygulama paketi toocompute havuzdaki düğümlerin hello dağıtabilir, ancak yeniden başlatın veya gerekir düğümleri yeniden görüntü oluşturma.</span><span class="sxs-lookup"><span data-stu-id="f9086-205">tooactually deploy hello new application package toocompute nodes in hello pool, however, you must restart or reimage those nodes.</span></span> <span data-ttu-id="f9086-206">Bu komutla havuzdaki her düğümü yeniden başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f9086-206">You can restart every node in a pool with this command:</span></span>

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> <span data-ttu-id="f9086-207">Birden çok uygulama paketleri toohello işlem düğümleri havuzunda dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9086-207">You can deploy multiple application packages toohello compute nodes in a pool.</span></span> <span data-ttu-id="f9086-208">Çok isterseniz*ekleme* şu anda dağıtılan hello paketleri değiştirerek yerine bir uygulama paketi atlayın hello `$pool.ApplicationPackageReferences.Clear()` yukarıdaki satır.</span><span class="sxs-lookup"><span data-stu-id="f9086-208">If you'd like too*add* an application package instead of replacing hello currently deployed packages, omit hello `$pool.ApplicationPackageReferences.Clear()` line above.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f9086-209">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f9086-209">Next steps</span></span>
* <span data-ttu-id="f9086-210">Ayrıntılı cmdlet sözdizimi ve örnekleri için bkz. [Azure Batch cmdlet başvurusu](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="f9086-210">For detailed cmdlet syntax and examples, see [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>
* <span data-ttu-id="f9086-211">Uygulamalar ve Batch uygulama paketleri hakkında daha fazla bilgi için bkz: [Batch uygulama paketleriyle uygulama toocompute düğümlerini dağıtmak](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="f9086-211">For more information about applications and application packages in Batch, see [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/