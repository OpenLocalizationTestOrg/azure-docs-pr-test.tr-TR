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
# <a name="manage-batch-resources-with-powershell-cmdlets"></a>Batch kaynaklarını PowerShell cmdlet'leriyle yönetme

Hello Azure Batch PowerShell cmdlet'leri gerçekleştirebilir ve çoğu hello komut dosyası, yürütmek hello Batch API'leri ile aynı görevleri hello Azure portalı ve Azure komut satırı arabirimi (CLI) hello. Batch hesaplarınızın toomanage kullanın ve havuzlar, işler ve görevler gibi Batch kaynaklarınızla iş bir hızlı giriş toohello cmdlet'leri budur.

Batch cmdlet'leri ve ayrıntılı cmdlet sözdizimi tam listesi için bkz: Merhaba [Azure Batch cmdlet başvurusu](/powershell/module/azurerm.batch/#batch).

Bu makale, Azure PowerShell 3.0.0 sürümündeki cmdlet’leri temel almaktadır. Azure PowerShell güncelleştirmenizi öneririz sık tootake avantajlarından hizmet güncelleştirmeleri ve geliştirmeleri.

## <a name="prerequisites"></a>Ön koşullar
Aşağıdaki işlemleri toouse Azure PowerShell toomanage hello Batch kaynaklarınız gerçekleştirin.

* [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azure/overview)
* Merhaba çalıştırmak **Login-AzureRmAccount** cmdlet tooconnect tooyour abonelik (Merhaba hello Azure Resource Manager modülündeki Azure Batch cmdlet'leri sevk):
  
    `Login-AzureRmAccount`
* **Merhaba Batch sağlayıcı ad alanıyla kaydetme**. Bu işlem yalnızca gerçekleştirilen toobe gereken **abonelik başına bir kez**.
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a>Batch hesaplarını ve anahtarlarını yönetme
### <a name="create-a-batch-account"></a>Batch hesabı oluşturma
**New-AzureRmBatchAccount**, belirtilen kaynak grubunda bir Batch hesabı oluşturur. Bir kaynak grubu zaten yoksa, hello çalıştırarak oluşturmak [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet'i. Hello Azure birini belirtin hello bölgelerde **konumu** "Orta ABD" gibi bir parametre. Örneğin:

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

Ardından, hello kaynak grubunda hello hesap için bir adı belirterek, bir toplu işlem hesabı oluşturun <*account_name*> ve hello konumunu, hem de kaynak grubunuzun adını. Merhaba Batch hesabı oluşturma bazı zaman toocomplete alabilir. Örneğin:

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> Merhaba toplu işlem hesabı adı benzersiz toohello hello kaynak grubunun Azure bölgesinde olmalıdır 3 ile 24 karakter arasında içerir ve yalnızca küçük harf ve sayı kullanın.
> 
> 

### <a name="get-account-access-keys"></a>Hesap erişim anahtarı alma
**Get-AzureRmBatchAccountKeys** bir Azure Batch hesabıyla ilişkili hello erişim anahtarlarını gösterir. Örneğin, oluşturduğunuz hello hesabının tooget hello birincil ve ikincil anahtarları aşağıdaki hello çalıştırın.

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a>Yeni erişim anahtarı oluşturma
**New-AzureRmBatchAccountKey**, Azure Batch hesabı için yeni bir birincil ya da ikincil hesap anahtarı oluşturur. Örneğin, Batch hesabınıza yeni bir birincil anahtar toogenerate yazın:

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> Yeni bir ikincil anahtar toogenerate belirtin "Secondary" Merhaba **KeyType** parametresi. Tooregenerate hello birincil ve ikincil anahtarları ayrı olarak sahip.
> 
> 

### <a name="delete-a-batch-account"></a>Batch hesabını silme
**Remove-AzureRmBatchAccount** Batch hesabını siler. Örneğin:

    Remove-AzureRmBatchAccount -AccountName <account_name>

İstendiğinde, tooremove hello hesap istediğinizi onaylayın. Hesabınızın kaldırılması bazı zaman toocomplete alabilir.

## <a name="create-a-batchaccountcontext-object"></a>BatchAccountContext nesnesi oluşturma
tooauthenticate kullanarak hello Batch PowerShell cmdlet'leri oluşturmak ve Batch havuzları, işleri, görevleri, yönetmek ve diğer kaynakları hesap adınızı ve anahtarları bir BatchAccountContext nesnesi toostore ilk oluştururken:

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

Merhaba BatchAccountContext nesnesi cmdlet'lere bu kullanım hello geçirdiğiniz **BatchContext** parametresi.

> [!NOTE]
> Varsayılan olarak, hello hesabın birincil anahtarı kimlik doğrulaması için kullanılır, ancak açıkça hello anahtar toouse BatchAccountContext nesnenizin değiştirerek seçebileceğiniz **Keyınuse** özelliği: `$context.KeyInUse = "Secondary"`.
> 
> 

## <a name="create-and-modify-batch-resources"></a>Batch kaynaklarını oluşturma ve değiştirme
Cmdlet'leri kullanın **New-AzureBatchPool**, **New-AzureBatchJob**, ve **New-AzureBatchTask** toocreate kaynakları Batch hesabı altında. Cmdlet'leri vardır **Get -** ve **Set -** cmdlet'leri tooupdate hello var olan kaynakların özelliklerini ve **Remove -** cmdlet'leri tooremove kaynakları Batch hesabı altında.

Bu cmdlet'lerin çoğu toplama toopassing BatchContext nesne kullanırken, toocreate gerekir veya hello aşağıdaki örnekte gösterildiği gibi ayrıntılı kaynak ayarlarını içeren nesneleri geçirin. Bkz: hello ayrıntılı ek örnekler için her cmdlet için Yardım.

### <a name="create-a-batch-pool"></a>Batch havuzu oluşturma
Merhaba hello işletim sisteminde işlem için düğümleri oluştururken veya güncelleştirirken bir Batch havuzu hello bulut hizmet yapılandırması veya hello sanal makine yapılandırması seçmeniz (bkz [Batch özelliklerine genel bakış](batch-api-basics.md#pool)). Merhaba bulut hizmeti yapılandırması belirtirseniz, işlem düğümleriniz hello biriyle görüntüsü [Azure konuk işletim sistemi sürümleri](../cloud-services/cloud-services-guestos-update-matrix.md#releases). Merhaba sanal makine yapılandırması belirtirseniz, ya da hello birini desteklenen Linux veya Windows VM görüntüleri listelenen hello belirtebilirsiniz [Azure Virtual Machines Marketi][vm_marketplace], ya da özel bir sağlayın hazırladığınız resim.

Çalıştırdığınızda **New-AzureBatchPool**, hello işletim sistemi ayarlarını bir PSCloudServiceConfiguration veya PSVirtualMachineConfiguration nesnesine geçirin. Örneğin, hello aşağıdaki cmdlet'i yeni bir Batch havuzu boyutu küçük işlem düğümlerine hello bulut hizmeti yapılandırması, hello en son işletim sisteminin aile 3 sürümüyle (Windows Server 2012) ile görüntüsü oluşturur. Burada, hello **CloudServiceConfiguration** parametresi belirtir hello *$configuration* hello PSCloudServiceConfiguration nesne değişkeni. Merhaba **BatchContext** parametresi, önceden tanımlanmış bir değişken belirtir *$context* hello BatchAccountContext nesnesi olarak.

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

Merhaba hedef hello yeni havuzdaki işlem düğümleri sayısı ölçeklendirmeyle belirlenir. Bu durumda, hello yalnızca formülüdür **$TargetDedicated = 4**, hello hello havuzdaki işlem düğümleri sayısını gösteren: 4 en fazla.

## <a name="query-for-pools-jobs-tasks-and-other-details"></a>Havuzlar, işler, görevler ve diğer ayrıntılar için sorgulama
Cmdlet'leri kullanın **Get-AzureBatchPool**, **Get-AzureBatchJob**, ve **Get-AzureBatchTask** bir Batch hesabı altında oluşturulan varlıkların tooquery.

### <a name="query-for-data"></a>Verileri sorgulama
Bir örnek olarak kullanabilirsiniz **Get-AzureBatchPools** toofind havuzlarınızı. Varsayılan olarak, hesabınız altındaki tüm havuzlarla ilgili bu sorgular zaten hello BatchAccountContext nesnesinde depolanır *$context*:

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a>OData filtresini kullanma
Hello kullanarak bir OData filtresi sağlayabilirsiniz **filtre** parametresi toofind yalnızca ilgilendiğiniz nesneleri hello. Örneğin, kimlikleri “myPool” ile başlayan tüm havuzları bulabilirsiniz.

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

Bu yöntem, yerel bir işlem hattında "Where-Object" kullanmak kadar esnek değildir. Ancak, böylece tüm filtreleme Internet bant genişliği korunarak hello sunucu tarafında gerçekleşir hello sorgu toohello Batch hizmeti doğrudan gönderilir.

### <a name="use-hello-id-parameter"></a>Merhaba kimlik parametresini kullanma
Toouse hello alternatif tooan OData filtredir **kimliği** parametresi. "myPool" kimliğine sahip belirli bir havuzu tooquery:

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

Merhaba **kimliği** parametresi, yalnızca tam kimlik aramasını, joker karakter veya OData stili filtreleri destekler.

### <a name="use-hello-maxcount-parameter"></a>Merhaba MaxCount parametresini kullanma
Varsayılan olarak, her cmdlet en çok 1000 nesne döndürür. Bu sınıra ulaştıysanız, daha az nesne filtre toobring daraltın veya hello kullanarak en açık olarak ayarlanıp **MaxCount** parametresi. Örneğin:

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

tooremove hello üst sınır ayarlayın **MaxCount** too0 veya daha az.

### <a name="use-hello-powershell-pipeline"></a>Merhaba PowerShell işlem hattını kullanma
Batch cmdlet'leri hello PowerShell ardışık düzen toosend verileri cmdlet'ler arasında yararlanabilirsiniz. Bu, aynı olarak belirten bir parametre ancak birden çok varlık ile daha kolay çalışma yapar efekt hello sahiptir.

Örneğin, hesabınızın altındaki tüm görevleri bulup görüntüleyin:

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

Havuzdaki her işlem düğümünü yeniden başlatın:

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a>Uygulama paketi yönetimi
Uygulama paketleri toodeploy uygulamaları toohello işlem düğümlerine basitleştirilmiş bir yolunu sağlar. Hello Batch PowerShell cmdlet'leri ile karşıya yükleme ve uygulama paketleri Batch hesabınızı yönetmek ve paketi sürümleri toocompute düğümlerini dağıtmak.

Bir uygulama **oluşturun**:

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

Bir uygulama paketi **ekleyin**:

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

Set hello **varsayılan sürüm** hello uygulama için:

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

Uygulamanın paketlerini **listeleme**

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

Uygulama paketini **silme**

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

Uygulamayı **silme**

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> Merhaba uygulaması silmeden önce tüm uygulamanın uygulama paketi sürümleri silmeniz gerekir. Şu anda uygulama paketleri olan bir uygulama toodelete çalışırsanız 'Çakışma' hata alırsınız.
> 
> 

### <a name="deploy-an-application-package"></a>Uygulama paketi dağıtma
Bir havuz oluşturduğunuzda dağıtım için bir veya daha fazla uygulama paketi belirtebilirsiniz. Havuz oluşturma sırasında bir paket belirtmeniz hello düğümü birleştirmeler havuzu olarak dağıtılan tooeach düğümü olur. Paketler ayrıca bir düğüm yeniden başlatıldığında veya yeniden görüntüsü oluşturulduğunda dağıtılır.

Merhaba belirtin `-ApplicationPackageReference` hello havuzuna Katıl gibi bir uygulama paketi toohello havuzun düğümleri havuzu toodeploy oluştururken seçeneği. İlk olarak, oluşturma bir **PSApplicationPackageReference** nesne ve istediğiniz toodeploy toohello havuzunun işlem düğümlerini hello uygulama kimliği ve Paket sürümü ile yapılandırın:

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

Şimdi hello havuzu oluşturun ve bağımsız değişkeni toohello hello gibi hello paket başvuru nesnesi belirtmeniz `ApplicationPackageReferences` seçeneği:

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

Uygulama paketleri hakkında daha fazla bilgi bulabilirsiniz [Batch uygulama paketleriyle uygulama toocompute düğümlerini dağıtmak](batch-application-packages.md).

> [!IMPORTANT]
> Yapmanız gerekenler [bir Azure depolama hesabı bağlantı](#linked-storage-account-autostorage) tooyour Batch uygulama paketleri toouse hesap.
> 
> 

### <a name="update-a-pools-application-packages"></a>Bir havuzun uygulama paketlerini güncelleştirme
tooan var olan bir havuzu, atanan tooupdate hello uygulamaları (uygulama kimliği ve Paket sürümü) istenen hello özelliklerle ilk PSApplicationPackageReference nesnesi oluşturun:

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

Ardından, yığın hello havuzu almak, herhangi bir varolan paket temizleyin bizim yeni paketi Başvurusu Ekle ve hello Batch hizmeti hello yeni havuz ayarlarla güncelleştirmek:

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

Şimdi hello Batch hizmeti hello havuzunun özelliklerinde güncelleştirdik. tooactually hello yeni uygulama paketi toocompute havuzdaki düğümlerin hello dağıtabilir, ancak yeniden başlatın veya gerekir düğümleri yeniden görüntü oluşturma. Bu komutla havuzdaki her düğümü yeniden başlatabilirsiniz:

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> Birden çok uygulama paketleri toohello işlem düğümleri havuzunda dağıtabilirsiniz. Çok isterseniz*ekleme* şu anda dağıtılan hello paketleri değiştirerek yerine bir uygulama paketi atlayın hello `$pool.ApplicationPackageReferences.Clear()` yukarıdaki satır.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* Ayrıntılı cmdlet sözdizimi ve örnekleri için bkz. [Azure Batch cmdlet başvurusu](/powershell/module/azurerm.batch/#batch).
* Uygulamalar ve Batch uygulama paketleri hakkında daha fazla bilgi için bkz: [Batch uygulama paketleriyle uygulama toocompute düğümlerini dağıtmak](batch-application-packages.md).

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/