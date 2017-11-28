---
title: "Azure Data Factory aaaTroubleshoot sorunları"
description: "Azure Data Factory kullanarak tootroubleshoot nasıl sorunlar hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 38fd14c1-5bb7-4eef-a9f5-b289ff9a6942
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: cf65bcf3e1c3f061d3ac1dbf32e99cc7b014f9dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-data-factory-issues"></a><span data-ttu-id="cd994-103">Data Factory'de sorun giderme</span><span class="sxs-lookup"><span data-stu-id="cd994-103">Troubleshoot Data Factory issues</span></span>
<span data-ttu-id="cd994-104">Bu makalede Azure Data Factory kullanırken sorunlarıyla ilgili sorun giderme ipuçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="cd994-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span></span> <span data-ttu-id="cd994-105">Bu makalede tüm hello olası sorunları hello hizmetini kullanırken listelenmez, ancak bazı sorunlar ve genel sorun giderme ipuçları kapsar.</span><span class="sxs-lookup"><span data-stu-id="cd994-105">This article does not list all hello possible issues when using hello service, but it covers some issues and general troubleshooting tips.</span></span>   

## <a name="troubleshooting-tips"></a><span data-ttu-id="cd994-106">Sorun giderme ipuçları</span><span class="sxs-lookup"><span data-stu-id="cd994-106">Troubleshooting tips</span></span>
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a><span data-ttu-id="cd994-107">Hata: hello abonelik 'Microsoft.DataFactory' kayıtlı toouse ad değil.</span><span class="sxs-lookup"><span data-stu-id="cd994-107">Error: hello subscription is not registered toouse namespace 'Microsoft.DataFactory'</span></span>
<span data-ttu-id="cd994-108">Bu hata iletisini alırsanız hello Azure Data Factory kaynak sağlayıcısı makinenizde kayıtlı değil.</span><span class="sxs-lookup"><span data-stu-id="cd994-108">If you receive this error, hello Azure Data Factory resource provider has not been registered on your machine.</span></span> <span data-ttu-id="cd994-109">Aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="cd994-109">Do hello following:</span></span>

1. <span data-ttu-id="cd994-110">Azure PowerShell’i çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cd994-110">Launch Azure PowerShell.</span></span>
2. <span data-ttu-id="cd994-111">Tooyour içinde Azure hesabı komutu aşağıdaki hello kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="cd994-111">Log in tooyour Azure account using hello following command.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="cd994-112">Komut tooregister hello Azure Data Factory sağlayıcısının aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cd994-112">Run hello following command tooregister hello Azure Data Factory provider.</span></span>

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a><span data-ttu-id="cd994-113">Sorun: bir Data Factory cmdlet çalıştırıldığında yetkisiz hata</span><span class="sxs-lookup"><span data-stu-id="cd994-113">Problem: Unauthorized error when running a Data Factory cmdlet</span></span>
<span data-ttu-id="cd994-114">Merhaba sağ Azure hesabı veya abonelik hello Azure PowerShell ile kullanmakta olduğunuz olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="cd994-114">You are probably not using hello right Azure account or subscription with hello Azure PowerShell.</span></span> <span data-ttu-id="cd994-115">Cmdlet'leri tooselect hello sağ hello Azure PowerShell ile Azure hesabınızı ve aboneliğinizi toouse aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="cd994-115">Use hello following cmdlets tooselect hello right Azure account and subscription toouse with hello Azure PowerShell.</span></span>

1. <span data-ttu-id="cd994-116">Login-AzureRmAccount - kullanım hello doğru kullanıcı kimliği ve parolası</span><span class="sxs-lookup"><span data-stu-id="cd994-116">Login-AzureRmAccount - Use hello right user ID and password</span></span>
2. <span data-ttu-id="cd994-117">Get-AzureRmSubscription - tüm hello hello hesabı için abonelik görünümü.</span><span class="sxs-lookup"><span data-stu-id="cd994-117">Get-AzureRmSubscription - View all hello subscriptions for hello account.</span></span>
3. <span data-ttu-id="cd994-118">Select-AzureRmSubscription &lt;abonelik adı&gt; -hello doğru abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="cd994-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select hello right subscription.</span></span> <span data-ttu-id="cd994-119">Kullanım hello aynı toocreate data factory hello Azure portalı üzerinde kullanın.</span><span class="sxs-lookup"><span data-stu-id="cd994-119">Use hello same one you use toocreate a data factory on hello Azure portal.</span></span>

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a><span data-ttu-id="cd994-120">Sorun: Azure portalından toolaunch veri yönetimi ağ geçidi hızlı kurulum başarısız</span><span class="sxs-lookup"><span data-stu-id="cd994-120">Problem: Fail toolaunch Data Management Gateway Express Setup from Azure portal</span></span>
<span data-ttu-id="cd994-121">Merhaba hızlı kurulum hello veri yönetimi ağ geçidi için Internet Explorer veya Microsoft ClickOnce uyumlu bir web tarayıcısı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="cd994-121">hello Express setup for hello Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span> <span data-ttu-id="cd994-122">Toostart Hello hızlı kurulum başarısız olursa hello aşağıdakilerden birini yapın:</span><span class="sxs-lookup"><span data-stu-id="cd994-122">If hello Express Setup fails toostart, do one of hello following:</span></span>

* <span data-ttu-id="cd994-123">Internet Explorer veya Microsoft ClickOnce uyumlu bir web tarayıcısı kullanın.</span><span class="sxs-lookup"><span data-stu-id="cd994-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>

    <span data-ttu-id="cd994-124">Chrome kullanıyorsanız, toohello Git [Chrome web mağazası](https://chrome.google.com/webstore/), arama "ClickOnce" sözcüğünü, hello ClickOnce uzantıları birini seçin ve yükleyin.</span><span class="sxs-lookup"><span data-stu-id="cd994-124">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>

    <span data-ttu-id="cd994-125">Firefox (yükleme eklenti) aynı hello.</span><span class="sxs-lookup"><span data-stu-id="cd994-125">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="cd994-126">Merhaba araç çubuğu (Merhaba sağ üst köşedeki üç yatay çizgi) menü Aç düğmesini tıklatın, eklentiler'i tıklatın, "ClickOnce" sözcüğünü arama, hello ClickOnce uzantıları birini seçin ve yükleyin.</span><span class="sxs-lookup"><span data-stu-id="cd994-126">Click Open Menu button on hello toolbar (three horizontal lines in hello top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
* <span data-ttu-id="cd994-127">Kullanım hello **el ile Kurulum** hello üzerinde gösterilen bağlantı aynı dikey penceresinde hello portal.</span><span class="sxs-lookup"><span data-stu-id="cd994-127">Use hello **Manual Setup** link shown on hello same blade in hello portal.</span></span> <span data-ttu-id="cd994-128">Bu yaklaşım toodownload yükleme dosyasını kullanın ve el ile çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cd994-128">You use this approach toodownload installation file and run it manually.</span></span> <span data-ttu-id="cd994-129">Merhaba yükleme başarılı olduktan sonra hello veri yönetimi ağ geçidi yapılandırması iletişim kutusu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cd994-129">After hello installation is successful, you see hello Data Management Gateway Configuration dialog box.</span></span> <span data-ttu-id="cd994-130">Kopya hello **anahtar** hello portal ekran ve hello hizmeti ile Merhaba configuration manager toomanually içinde kaydetmek hello ağ geçidi kullanın.</span><span class="sxs-lookup"><span data-stu-id="cd994-130">Copy hello **key** from hello portal screen and use it in hello configuration manager toomanually register hello gateway with hello service.</span></span>  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a><span data-ttu-id="cd994-131">Sorun: Başarısız tooconnect tooon içi SQL Server</span><span class="sxs-lookup"><span data-stu-id="cd994-131">Problem: Fail tooconnect tooon-premises SQL Server</span></span>
<span data-ttu-id="cd994-132">Başlatma **veri yönetimi ağ geçidi Yapılandırma Yöneticisi** hello ağ geçidi makinesi ve hello kullan **sorun giderme** hello ağ geçidi makineden tootest hello bağlantı tooSQL sunucu sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="cd994-132">Launch **Data Management Gateway Configuration Manager** on hello gateway machine and use hello **Troubleshooting** tab tootest hello connection tooSQL Server from hello gateway machine.</span></span> <span data-ttu-id="cd994-133">Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) ilgili sorunlar bağlantı/ağ geçidi sorun giderme ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="cd994-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a><span data-ttu-id="cd994-134">Sorun: Durumu için herhangi bir zamanda bekleyen giriş dilimler olur</span><span class="sxs-lookup"><span data-stu-id="cd994-134">Problem: Input slices are in Waiting state for ever</span></span>
<span data-ttu-id="cd994-135">Merhaba dilimler olabilir **bekleyen** toovarious nedeniyle son durum.</span><span class="sxs-lookup"><span data-stu-id="cd994-135">hello slices could be in **Waiting** state due toovarious reasons.</span></span> <span data-ttu-id="cd994-136">Bu hello hello yaygın nedenlerinden biridir **dış** özelliği çok ayarlanmamışsa**doğru**.</span><span class="sxs-lookup"><span data-stu-id="cd994-136">One of hello common reasons is that hello **external** property is not set too**true**.</span></span> <span data-ttu-id="cd994-137">Azure Data Factory üretilen dış hello kapsamı herhangi bir veri kümesi ile işaretlenmelidir **dış** özelliği.</span><span class="sxs-lookup"><span data-stu-id="cd994-137">Any dataset that is produced outside hello scope of Azure Data Factory should be marked with **external** property.</span></span> <span data-ttu-id="cd994-138">Bu özellik hello veri dış ve hello veri fabrikası içinde herhangi bir ardışık düzen tarafından yedeklenen olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="cd994-138">This property indicates that hello data is external and not backed by any pipelines within hello data factory.</span></span> <span data-ttu-id="cd994-139">Merhaba veri dilimi olarak işaretlenmiş **hazır** hello veri hello ilgili deposunda kullanılabilir olduğunda.</span><span class="sxs-lookup"><span data-stu-id="cd994-139">hello data slices are marked as **Ready** once hello data is available in hello respective store.</span></span>

<span data-ttu-id="cd994-140">Merhaba hello kullanım için örneği aşağıdaki hello bkz **dış** özelliği.</span><span class="sxs-lookup"><span data-stu-id="cd994-140">See hello following example for hello usage of hello **external** property.</span></span> <span data-ttu-id="cd994-141">İsteğe bağlı olarak belirtebilirsiniz **externalData*** dış tootrue ayarlandığında.</span><span class="sxs-lookup"><span data-stu-id="cd994-141">You can optionally specify **externalData*** when you set external tootrue.</span></span>

<span data-ttu-id="cd994-142">Bkz: [veri kümeleri](data-factory-create-datasets.md) bu özellik hakkında daha fazla ayrıntı için makale.</span><span class="sxs-lookup"><span data-stu-id="cd994-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span></span>

```json
{
  "name": "CustomerTable",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "MyLinkedService",
    "typeProperties": {
      "folderPath": "MyContainer/MySubFolder/",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      }
    }
  }
}
```

<span data-ttu-id="cd994-143">tooresolve Merhaba hata, hello eklemek **dış** özelliği ve isteğe bağlı hello **externalData** bölümünde toohello JSON hello giriş tablosu tanımını ve hello tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd994-143">tooresolve hello error, add hello **external** property and hello optional **externalData** section toohello JSON definition of hello input table and recreate hello table.</span></span>

### <a name="problem-hybrid-copy-operation-fails"></a><span data-ttu-id="cd994-144">Sorun: Karma kopyalama işlemi başarısız</span><span class="sxs-lookup"><span data-stu-id="cd994-144">Problem: Hybrid copy operation fails</span></span>
<span data-ttu-id="cd994-145">Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) adımları tootroubleshoot sorunlar kopyalama/şirket içi veri depolama kullanarak veri yönetimi ağ geçidi hello için.</span><span class="sxs-lookup"><span data-stu-id="cd994-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps tootroubleshoot issues with copying to/from an on-premises data store using hello Data Management Gateway.</span></span>

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a><span data-ttu-id="cd994-146">Sorun: başarısız sağlama isteğe bağlı Hdınsight</span><span class="sxs-lookup"><span data-stu-id="cd994-146">Problem: On-demand HDInsight provisioning fails</span></span>
<span data-ttu-id="cd994-147">Bağlı hizmet türü HDInsightOnDemand kullanırken toospecify tooan Azure Blob Storage işaret eden bir linkedServiceName gerekir.</span><span class="sxs-lookup"><span data-stu-id="cd994-147">When using a linked service of type HDInsightOnDemand, you need toospecify a linkedServiceName that points tooan Azure Blob Storage.</span></span> <span data-ttu-id="cd994-148">Data Factory Hizmeti'ne isteğe bağlı Hdınsight kümeniz için bu depolama toostore günlüklerine ve Destek dosyalarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="cd994-148">Data Factory service uses this storage toostore logs and supporting files for your on-demand HDInsight cluster.</span></span>  <span data-ttu-id="cd994-149">Bazen isteğe bağlı Hdınsight kümesi sağlama hello aşağıdaki hata ile başarısız olur:</span><span class="sxs-lookup"><span data-stu-id="cd994-149">Sometimes provisioning of an on-demand HDInsight cluster fails with hello following error:</span></span>

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

<span data-ttu-id="cd994-150">Bu hata genellikle hello linkedServiceName belirtilen hello depolama hesabı hello konumunu hello olmadığını gösterir aynı veri merkezi nerede Hdınsight hello sağlama gerçekleştiği konum.</span><span class="sxs-lookup"><span data-stu-id="cd994-150">This error usually indicates that hello location of hello storage account specified in hello linkedServiceName is not in hello same data center location where hello HDInsight provisioning is happening.</span></span> <span data-ttu-id="cd994-151">Örnek: varsa, veri fabrikası Batı ABD ve hello Azure depolama Doğu ABD, Batı ABD isteğe bağlı sağlama başarısız hello.</span><span class="sxs-lookup"><span data-stu-id="cd994-151">Example: if your data factory is in West US and hello Azure storage is in East US, hello on-demand provisioning fails in West US.</span></span>

<span data-ttu-id="cd994-152">Buna ek olarak, isteğe bağlı HDInsight içinde ek depolama hesaplarının belirlenebileceği ikinci bir JSON özelliği (additionalLinkedServiceNames) bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cd994-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span></span> <span data-ttu-id="cd994-153">Bu ek bağlantılı depolama hesapları hello ile Merhaba hello Hdınsight kümesi veya aynı konumda başarısız olması gerektiğini aynı hata.</span><span class="sxs-lookup"><span data-stu-id="cd994-153">Those additional linked storage accounts should be in hello same location as hello HDInsight cluster, or it fails with hello same error.</span></span>

### <a name="problem-custom-net-activity-fails"></a><span data-ttu-id="cd994-154">Sorun: Özel .NET etkinliği başarısız</span><span class="sxs-lookup"><span data-stu-id="cd994-154">Problem: Custom .NET activity fails</span></span>
<span data-ttu-id="cd994-155">Bkz: [özel etkinliği ile işlem hattı Debug](data-factory-use-custom-activities.md#troubleshoot-failures) ayrıntılı adımlar için.</span><span class="sxs-lookup"><span data-stu-id="cd994-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span></span>

## <a name="use-azure-portal-tootroubleshoot"></a><span data-ttu-id="cd994-156">Azure portal tootroubleshoot kullanın</span><span class="sxs-lookup"><span data-stu-id="cd994-156">Use Azure portal tootroubleshoot</span></span>
### <a name="using-portal-blades"></a><span data-ttu-id="cd994-157">Portal dikey penceresi kullanılarak</span><span class="sxs-lookup"><span data-stu-id="cd994-157">Using portal blades</span></span>
<span data-ttu-id="cd994-158">Bkz: [işlem hattını izleme](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) adımlar için.</span><span class="sxs-lookup"><span data-stu-id="cd994-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span></span>

### <a name="using-monitor-and-manage-app"></a><span data-ttu-id="cd994-159">İzleme ve Yönetme Uygulamasını kullanma</span><span class="sxs-lookup"><span data-stu-id="cd994-159">Using Monitor and Manage App</span></span>
<span data-ttu-id="cd994-160">Bkz: [İzleyici ve data factory işlem hatlarını izleme ve yönetme uygulaması kullanarak yönetmek](data-factory-monitor-manage-app.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="cd994-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span></span>

## <a name="use-azure-powershell-tootroubleshoot"></a><span data-ttu-id="cd994-161">Azure PowerShell tootroubleshoot kullanın</span><span class="sxs-lookup"><span data-stu-id="cd994-161">Use Azure PowerShell tootroubleshoot</span></span>
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a><span data-ttu-id="cd994-162">Azure PowerShell tootroubleshoot hata kullanın</span><span class="sxs-lookup"><span data-stu-id="cd994-162">Use Azure PowerShell tootroubleshoot an error</span></span>
<span data-ttu-id="cd994-163">Bkz: [İzleyicisi veri fabrikasında ardışık düzenleri Azure PowerShell kullanarak](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="cd994-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span></span>

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456
[json-scripting-reference]: http://go.microsoft.com/fwlink/?LinkId=516971

[azure-portal]: https://portal.azure.com/

[image-data-factory-troubleshoot-with-error-link]: ./media/data-factory-troubleshoot/DataFactoryWithErrorLink.png

[image-data-factory-troubleshoot-datasets-with-errors-blade]: ./media/data-factory-troubleshoot/DatasetsWithErrorsBlade.png

[image-data-factory-troubleshoot-table-blade-with-problem-slices]: ./media/data-factory-troubleshoot/TableBladeWithProblemSlices.png

[image-data-factory-troubleshoot-activity-run-with-error]: ./media/data-factory-troubleshoot/ActivityRunDetailsWithError.png

[image-data-factory-troubleshoot-dataslice-blade-with-active-runs]: ./media/data-factory-troubleshoot/DataSliceBladeWithActivityRuns.png

[image-data-factory-troubleshoot-walkthrough2-with-errors-link]: ./media/data-factory-troubleshoot/Walkthrough2WithErrorsLink.png

[image-data-factory-troubleshoot-walkthrough2-datasets-with-errors]: ./media/data-factory-troubleshoot/Walkthrough2DataSetsWithErrors.png

[image-data-factory-troubleshoot-walkthrough2-table-with-problem-slices]: ./media/data-factory-troubleshoot/Walkthrough2TableProblemSlices.png

[image-data-factory-troubleshoot-walkthrough2-slice-activity-runs]: ./media/data-factory-troubleshoot/Walkthrough2DataSliceActivityRuns.png

[image-data-factory-troubleshoot-activity-run-details]: ./media/data-factory-troubleshoot/Walkthrough2ActivityRunDetails.png
