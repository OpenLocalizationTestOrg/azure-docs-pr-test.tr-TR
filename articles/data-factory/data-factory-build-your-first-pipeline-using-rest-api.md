---
title: aaaBuild ilk data factory'nizi (REST) | Microsoft Docs
description: "Bu öğreticide Data Factory REST API’sini kullanarak örnek bir Azure Data Factory işlem hattı oluşturursunuz."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7e0a2465-2d85-4143-a4bb-42e03c273097
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 5d8e39bd598cca35f91d501bad74e8a8436f8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a><span data-ttu-id="c56cc-103">Öğretici: Data Factory REST API kullanarak ilk Azure data factory’nizi derleme</span><span class="sxs-lookup"><span data-stu-id="c56cc-103">Tutorial: Build your first Azure data factory using Data Factory REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c56cc-104">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="c56cc-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="c56cc-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="c56cc-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="c56cc-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c56cc-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="c56cc-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c56cc-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="c56cc-108">Resource Manager Şablonu</span><span class="sxs-lookup"><span data-stu-id="c56cc-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="c56cc-109">REST API</span><span class="sxs-lookup"><span data-stu-id="c56cc-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


<span data-ttu-id="c56cc-110">Bu makalede, ilk Azure data factory'nizi veri fabrikası REST API toocreate kullanın.</span><span class="sxs-lookup"><span data-stu-id="c56cc-110">In this article, you use Data Factory REST API toocreate your first Azure data factory.</span></span> <span data-ttu-id="c56cc-111">diğer araçlar/SDK, kullanarak toodo hello öğretici seçin hello seçeneklerden birini hello aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="c56cc-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="c56cc-112">Bu öğreticide Hello ardışık bir etkinlik vardır: **Hdınsight Hive etkinliği**.</span><span class="sxs-lookup"><span data-stu-id="c56cc-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="c56cc-113">Bu etkinlik dönüşümler veri tooproduce çıkış veri girişi bir Azure Hdınsight kümesinde bir hive betiği çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="c56cc-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="c56cc-114">Başlangıç ve bitiş zamanlarını hello arasında bir ay belirtilen sonra hello ardışık düzen zamanlanmış toorun ' dir.</span><span class="sxs-lookup"><span data-stu-id="c56cc-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span>

> [!NOTE]
> <span data-ttu-id="c56cc-115">Bu makalede, tüm hello REST API kapsamaz.</span><span class="sxs-lookup"><span data-stu-id="c56cc-115">This article does not cover all hello REST API.</span></span> <span data-ttu-id="c56cc-116">REST API ile ilgili kapsamlı belgeler için bkz. [Data Factory REST API Başvurusu](/rest/api/datafactory/).</span><span class="sxs-lookup"><span data-stu-id="c56cc-116">For comprehensive documentation on REST API, see [Data Factory REST API Reference](/rest/api/datafactory/).</span></span>
> 
> <span data-ttu-id="c56cc-117">Bir işlem hattında birden fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="c56cc-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="c56cc-118">Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir.</span><span class="sxs-lookup"><span data-stu-id="c56cc-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="c56cc-119">Daha fazla bilgi için bkz. [Data Factory'de zamanlama ve yürütme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="c56cc-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="c56cc-120">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c56cc-120">Prerequisites</span></span>
* <span data-ttu-id="c56cc-121">Okuyun [öğreticiye genel bakış](data-factory-build-your-first-pipeline.md) makale ve tam hello **önkoşul** adımları.</span><span class="sxs-lookup"><span data-stu-id="c56cc-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="c56cc-122">[Curl](https://curl.haxx.se/dlwiz/) aracını makinenize yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c56cc-122">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="c56cc-123">REST komutları toocreate data factory hello CURL aracını kullanın.</span><span class="sxs-lookup"><span data-stu-id="c56cc-123">You use hello CURL tool with REST commands toocreate a data factory.</span></span>
* <span data-ttu-id="c56cc-124">Aşağıdakileri yapmak için [bu makaledeki](../azure-resource-manager/resource-group-create-service-principal-portal.md) yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="c56cc-124">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span>
  1. <span data-ttu-id="c56cc-125">Azure Active Directory’de **ADFGetStartedApp** adlı bir Web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c56cc-125">Create a Web application named **ADFGetStartedApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="c56cc-126">**İstemci kimliği** ve **gizli anahtarı** alın.</span><span class="sxs-lookup"><span data-stu-id="c56cc-126">Get **client ID** and **secret key**.</span></span>
  3. <span data-ttu-id="c56cc-127">**İstemci kimliğini** alın.</span><span class="sxs-lookup"><span data-stu-id="c56cc-127">Get **tenant ID**.</span></span>
  4. <span data-ttu-id="c56cc-128">Merhaba atamak **ADFGetStartedApp** uygulama toohello **veri fabrikası katkıda bulunan** rol.</span><span class="sxs-lookup"><span data-stu-id="c56cc-128">Assign hello **ADFGetStartedApp** application toohello **Data Factory Contributor** role.</span></span>
* <span data-ttu-id="c56cc-129">[Azure PowerShell](/powershell/azure/overview)'i yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c56cc-129">Install [Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="c56cc-130">Başlatma **PowerShell** ve çalışma hello aşağıdaki komutu.</span><span class="sxs-lookup"><span data-stu-id="c56cc-130">Launch **PowerShell** and run hello following command.</span></span> <span data-ttu-id="c56cc-131">Bu öğreticide hello sonuna kadar Azure PowerShell'i açık tutun.</span><span class="sxs-lookup"><span data-stu-id="c56cc-131">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="c56cc-132">Kapatıp yeniden açın, toorun hello komutları yeniden gerekir.</span><span class="sxs-lookup"><span data-stu-id="c56cc-132">If you close and reopen, you need toorun hello commands again.</span></span>
  1. <span data-ttu-id="c56cc-133">Çalıştırma **Login-AzureRmAccount** hello kullanıcı adı ve toosign toohello Azure portal kullanın parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="c56cc-133">Run **Login-AzureRmAccount** and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
  2. <span data-ttu-id="c56cc-134">Çalıştırma **Get-AzureRmSubscription** tooview tüm abonelikler için bu hesabı hello.</span><span class="sxs-lookup"><span data-stu-id="c56cc-134">Run **Get-AzureRmSubscription** tooview all hello subscriptions for this account.</span></span>
  3. <span data-ttu-id="c56cc-135">Çalıştırma **Get-AzureRmSubscription - varlığıyla SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** toowork ile istediğiniz tooselect hello abonelik.</span><span class="sxs-lookup"><span data-stu-id="c56cc-135">Run **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="c56cc-136">Değiştir **NameOfAzureSubscription** , Azure aboneliğinizin hello adı.</span><span class="sxs-lookup"><span data-stu-id="c56cc-136">Replace **NameOfAzureSubscription** with hello name of your Azure subscription.</span></span>
* <span data-ttu-id="c56cc-137">Adlı bir Azure kaynak grubu oluşturma **ADFTutorialResourceGroup** hello PowerShell komutunda aşağıdaki hello çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="c56cc-137">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   <span data-ttu-id="c56cc-138">Merhaba bu öğreticideki adımlardan bazıları ADFTutorialResourceGroup adlı hello kaynak grubunu kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="c56cc-138">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="c56cc-139">Farklı bir kaynak grubu kullanıyorsanız, bu öğreticide ADFTutorialResourceGroup yerine, kaynak grubunun toouse hello adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="c56cc-139">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="c56cc-140">JSON tanımları oluşturma</span><span class="sxs-lookup"><span data-stu-id="c56cc-140">Create JSON definitions</span></span>
<span data-ttu-id="c56cc-141">JSON dosyaları curl.exe bulunduğu hello klasöründe aşağıdaki oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c56cc-141">Create following JSON files in hello folder where curl.exe is located.</span></span>

### <a name="datafactoryjson"></a><span data-ttu-id="c56cc-142">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="c56cc-142">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c56cc-143">Tooprefix/sonek ADFCopyTutorialDF toomake isteyebilirsiniz adı genel olarak benzersiz olmalıdır, benzersiz bir ad.</span><span class="sxs-lookup"><span data-stu-id="c56cc-143">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span>
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="c56cc-144">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="c56cc-144">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c56cc-145">**accountname** ve **accountkey** sözcüklerini Azure depolama hesabınızın adı ve anahtarıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c56cc-145">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="c56cc-146">toolearn tooget depolama alanınızın erişim nasıl anahtar, hello bilgi nasıl tooview, kopyalama ve yeniden oluşturma depolama erişim anahtarları içinde hakkında [depolama hesabınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="c56cc-146">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
>
>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="hdinsightondemandlinkedservicejson"></a><span data-ttu-id="c56cc-147">hdinsightondemandlinkedservice.JSON</span><span class="sxs-lookup"><span data-stu-id="c56cc-147">hdinsightondemandlinkedservice.json</span></span>

```JSON
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

<span data-ttu-id="c56cc-148">Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:</span><span class="sxs-lookup"><span data-stu-id="c56cc-148">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="c56cc-149">Özellik</span><span class="sxs-lookup"><span data-stu-id="c56cc-149">Property</span></span> | <span data-ttu-id="c56cc-150">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c56cc-150">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c56cc-151">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="c56cc-151">ClusterSize</span></span> |<span data-ttu-id="c56cc-152">Merhaba Hdınsight küme boyutu.</span><span class="sxs-lookup"><span data-stu-id="c56cc-152">Size of hello HDInsight cluster.</span></span> |
| <span data-ttu-id="c56cc-153">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="c56cc-153">TimeToLive</span></span> |<span data-ttu-id="c56cc-154">Silinmeden önce hello Hdınsight kümesi, o hello boşta kalma süresini belirtir.</span><span class="sxs-lookup"><span data-stu-id="c56cc-154">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
| <span data-ttu-id="c56cc-155">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c56cc-155">linkedServiceName</span></span> |<span data-ttu-id="c56cc-156">Hdınsight tarafından oluşturulan kullanılan toostore hello günlükleri olan hello depolama hesabını belirtir</span><span class="sxs-lookup"><span data-stu-id="c56cc-156">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

<span data-ttu-id="c56cc-157">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="c56cc-157">Note hello following points:</span></span>

* <span data-ttu-id="c56cc-158">Merhaba Data Factory oluşturur bir **Linux tabanlı** hello yukarıdaki JSON ile sizin için Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="c56cc-158">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="c56cc-159">Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="c56cc-159">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
* <span data-ttu-id="c56cc-160">İsteğe bağlı HDInsight kümesi yerine **kendi HDInsight kümenizi** kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c56cc-160">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="c56cc-161">Ayrıntılar için bkz. [HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).</span><span class="sxs-lookup"><span data-stu-id="c56cc-161">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="c56cc-162">Merhaba Hdınsight kümesi oluşturur bir **varsayılan kapsayıcı** hello JSON belirtilen hello blob depolamada (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="c56cc-162">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="c56cc-163">Hdınsight Hello küme silindiğinde bu kapsayıcıyı silmez.</span><span class="sxs-lookup"><span data-stu-id="c56cc-163">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="c56cc-164">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="c56cc-164">This behavior is by design.</span></span> <span data-ttu-id="c56cc-165">Mevcut canlı bir küme olmadıkça bir dilim işlenen her zaman isteğe bağlı Hdınsight bağlı hizmetiyle, Hdınsight kümesi oluşturulur (**timeToLive**) ve hello işlem bittiğinde silinir.</span><span class="sxs-lookup"><span data-stu-id="c56cc-165">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

    <span data-ttu-id="c56cc-166">Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c56cc-166">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="c56cc-167">Bunları hello işlerin sorunları giderilmesi için ihtiyacınız yoksa, toodelete isteyebilirsiniz bunları tooreduce hello depolama maliyeti.</span><span class="sxs-lookup"><span data-stu-id="c56cc-167">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="c56cc-168">Bu kapsayıcıların Hello adları izleyen bir desen: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="c56cc-168">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="c56cc-169">Gibi araçlar kullanın [Microsoft Storage Gezgini](http://storageexplorer.com/) toodelete kapsayıcılarında Azure blob depolama.</span><span class="sxs-lookup"><span data-stu-id="c56cc-169">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="c56cc-170">Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="c56cc-170">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="c56cc-171">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="c56cc-171">inputdataset.json</span></span>

```JSON
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

<span data-ttu-id="c56cc-172">Merhaba JSON adlı veri kümesini tanımlayan **Azureblobınput**, hello ardışık düzeninde bir etkinliğin girdi verilerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c56cc-172">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="c56cc-173">Ayrıca, hello giriş verisi adlı hello blob kapsayıcısında bulunur belirtir **adfgetstarted** ve adlı hello klasör **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="c56cc-173">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

<span data-ttu-id="c56cc-174">Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:</span><span class="sxs-lookup"><span data-stu-id="c56cc-174">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="c56cc-175">Özellik</span><span class="sxs-lookup"><span data-stu-id="c56cc-175">Property</span></span> | <span data-ttu-id="c56cc-176">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c56cc-176">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c56cc-177">type</span><span class="sxs-lookup"><span data-stu-id="c56cc-177">type</span></span> |<span data-ttu-id="c56cc-178">verileri Azure blob depolamada yer aldığından hello type özelliği tooAzureBlob ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="c56cc-178">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
| <span data-ttu-id="c56cc-179">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c56cc-179">linkedServiceName</span></span> |<span data-ttu-id="c56cc-180">daha önce oluşturduğunuz StorageLinkedService toohello başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="c56cc-180">refers toohello StorageLinkedService you created earlier.</span></span> |
| <span data-ttu-id="c56cc-181">fileName</span><span class="sxs-lookup"><span data-stu-id="c56cc-181">fileName</span></span> |<span data-ttu-id="c56cc-182">Bu özellik isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="c56cc-182">This property is optional.</span></span> <span data-ttu-id="c56cc-183">Bu özelliği atarsanız, hello folderPath tüm hello dosyalarından çekilir.</span><span class="sxs-lookup"><span data-stu-id="c56cc-183">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="c56cc-184">Bu durumda, yalnızca hello input.log işlenir.</span><span class="sxs-lookup"><span data-stu-id="c56cc-184">In this case, only hello input.log is processed.</span></span> |
| <span data-ttu-id="c56cc-185">type</span><span class="sxs-lookup"><span data-stu-id="c56cc-185">type</span></span> |<span data-ttu-id="c56cc-186">Merhaba günlük dosyaları metin biçiminde olduğundan TextFormat kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="c56cc-186">hello log files are in text format, so we use TextFormat.</span></span> |
| <span data-ttu-id="c56cc-187">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="c56cc-187">columnDelimiter</span></span> |<span data-ttu-id="c56cc-188">Merhaba günlük dosyalarındaki Sütunlar virgül karakteriyle (,) tarafından ayrılır</span><span class="sxs-lookup"><span data-stu-id="c56cc-188">columns in hello log files are delimited by a comma character (,)</span></span> |
| <span data-ttu-id="c56cc-189">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="c56cc-189">frequency/interval</span></span> |<span data-ttu-id="c56cc-190">tooMonth sıklığını ve aralığı hello girdi dilimlerinin aylık olarak kullanılabileceğini 1.</span><span class="sxs-lookup"><span data-stu-id="c56cc-190">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
| <span data-ttu-id="c56cc-191">external</span><span class="sxs-lookup"><span data-stu-id="c56cc-191">external</span></span> |<span data-ttu-id="c56cc-192">Merhaba giriş verisi hello Data Factory hizmetiyle oluşturulmadıysa, bu özellik tootrue ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="c56cc-192">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |

### <a name="outputdatasetjson"></a><span data-ttu-id="c56cc-193">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="c56cc-193">outputdataset.json</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="c56cc-194">Merhaba JSON adlı veri kümesini tanımlayan **AzureBlobOutput**, hello ardışık düzeninde bir etkinliğin çıktı verilerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c56cc-194">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="c56cc-195">Ayrıca, hello sonuçları adlı hello blob kapsayıcısında depolanır belirtir **adfgetstarted** ve adlı hello klasör **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="c56cc-195">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="c56cc-196">Merhaba **kullanılabilirlik** bölümü belirtiyor bu hello çıktı veri kümesi, aylık olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c56cc-196">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="c56cc-197">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="c56cc-197">pipeline.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c56cc-198">**storageaccountname**’i Azure depolama hesabınızın adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c56cc-198">Replace **storageaccountname** with name of your Azure storage account.</span></span>
>
>

```JSON
{
    "name": "MyFirstPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [{
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                "scriptLinkedService": "AzureStorageLinkedService",
                "defines": {
                    "inputtable": "wasb://adfgetstarted@<stroageaccountname>.blob.core.windows.net/inputdata",
                    "partitionedtable": "wasb://adfgetstarted@<stroageaccountname>t.blob.core.windows.net/partitioneddata"
                }
            },
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "policy": {
                "concurrency": 1,
                "retry": 3
            },
            "scheduler": {
                "frequency": "Month",
                "interval": 1
            },
            "name": "RunSampleHiveActivity",
            "linkedServiceName": "HDInsightOnDemandLinkedService"
        }],
        "start": "2017-07-10T00:00:00Z",
        "end": "2017-07-11T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="c56cc-199">Merhaba JSON parçacığında, Hdınsight kümesinde Hive tooprocess verilerini kullanan tek bir etkinlik oluşan bir işlem hattı oluşturuyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="c56cc-199">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess data on a HDInsight cluster.</span></span>

<span data-ttu-id="c56cc-200">Merhaba Hive betik dosyası **partitionweblogs.hql**, hello Azure depolama hesabı depolanır (adlı hello scriptLinkedService tarafından belirtilen **StorageLinkedService**) ve **komut dosyası ** hello kapsayıcı klasöründe **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="c56cc-200">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

<span data-ttu-id="c56cc-201">Merhaba **tanımlar** bölüm toohello hive betiğini Hive yapılandırma değerleri olarak geçirilir çalışma zamanı ayarları belirtir (örn., ${hiveconf: inputtable}, ${hiveconf}).</span><span class="sxs-lookup"><span data-stu-id="c56cc-201">hello **defines** section specifies runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

<span data-ttu-id="c56cc-202">Merhaba **Başlat** ve **son** hello ardışık düzen özelliklerini hello etkin dönem hello ardışık belirtir.</span><span class="sxs-lookup"><span data-stu-id="c56cc-202">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

<span data-ttu-id="c56cc-203">Bu hello Hive betiğini hello tarafından belirtilen hello işlem üzerinde çalıştığı belirtin Hello JSON etkinliğinde **linkedServiceName** – **Hdınsightondemandlinkedservice**.</span><span class="sxs-lookup"><span data-stu-id="c56cc-203">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

> [!NOTE]
> <span data-ttu-id="c56cc-204">"Ardışık düzen JSON" bölümüne bakın [işlem hatlarının ve etkinliklerin Azure Data Factory](data-factory-create-pipelines.md) hello önceki örnekte kullanılan JSON özellikleri hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="c56cc-204">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello preceding example.</span></span>
>
>

## <a name="set-global-variables"></a><span data-ttu-id="c56cc-205">Genel değişkenleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="c56cc-205">Set global variables</span></span>
<span data-ttu-id="c56cc-206">Azure PowerShell'de komutları hello değerleri kendi değerlerinizle değiştirerek sonra aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="c56cc-206">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c56cc-207">İstemci kimliği, istemci parolası, kiracı kimliği ve abonelik kimliğini edinme konusunda yönergeler için [Önkoşullar](#prerequisites) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="c56cc-207">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>
>
>

```PowerShell
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
$adf = "FirstDataFactoryREST"
```


## <a name="authenticate-with-aad"></a><span data-ttu-id="c56cc-208">AAD ile kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="c56cc-208">Authenticate with AAD</span></span>

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a><span data-ttu-id="c56cc-209">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="c56cc-209">Create data factory</span></span>
<span data-ttu-id="c56cc-210">Bu adımda, **FirstDataFactoryREST** adlı bir Azure Data Factory oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="c56cc-210">In this step, you create an Azure Data Factory named **FirstDataFactoryREST**.</span></span> <span data-ttu-id="c56cc-211">Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c56cc-211">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="c56cc-212">İşlem hattında bir veya daha fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="c56cc-212">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="c56cc-213">Örneğin, bir kopyalama etkinliği toocopy verilerinden bir kaynak tooa hedef veri deposu ve Hdınsight Hive etkinliği toorun bir Hive betiği tootransform veri.</span><span class="sxs-lookup"><span data-stu-id="c56cc-213">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform data.</span></span> <span data-ttu-id="c56cc-214">Aşağıdaki komutları toocreate hello veri fabrikası hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c56cc-214">Run hello following commands toocreate hello data factory:</span></span>

1. <span data-ttu-id="c56cc-215">Adlı hello komutu toovariable Ata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="c56cc-215">Assign hello command toovariable named **cmd**.</span></span>

    <span data-ttu-id="c56cc-216">Burada belirttiğiniz (ADFCopyTutorialDF) eşleşmeleri hello hello belirtilen adı hello veri fabrikası bu hello adını onaylayın **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="c56cc-216">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. <span data-ttu-id="c56cc-217">Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="c56cc-217">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="c56cc-218">Merhaba sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="c56cc-218">View hello results.</span></span> <span data-ttu-id="c56cc-219">Merhaba veri fabrikası başarıyla oluşturuldu, hello JSON hello hello veri fabrikasında için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c56cc-219">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

<span data-ttu-id="c56cc-220">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="c56cc-220">Note hello following points:</span></span>

* <span data-ttu-id="c56cc-221">Merhaba hello Azure Data Factory adı küresel olarak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c56cc-221">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="c56cc-222">Sonuçları hello hata görürseniz: **veri fabrikası adı "FirstDataFactoryREST" kullanılabilir değil**, adımları hello:</span><span class="sxs-lookup"><span data-stu-id="c56cc-222">If you see hello error in results: **Data factory name “FirstDataFactoryREST” is not available**, do hello following steps:</span></span>
  1. <span data-ttu-id="c56cc-223">Merhaba değişiklik hello adı (örneğin, yournameFirstDataFactoryREST) **datafactory.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="c56cc-223">Change hello name (for example, yournameFirstDataFactoryREST) in hello **datafactory.json** file.</span></span> <span data-ttu-id="c56cc-224">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="c56cc-224">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
  2. <span data-ttu-id="c56cc-225">Merhaba ilk komutta burada hello **$cmd** değişken değeri atanır, FirstDataFactoryREST hello yeni adıyla değiştirin ve hello komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c56cc-225">In hello first command where hello **$cmd** variable is assigned a value, replace FirstDataFactoryREST with hello new name and run hello command.</span></span>
  3. <span data-ttu-id="c56cc-226">Merhaba sonraki iki komutları tooinvoke hello REST API toocreate hello veri fabrikası ve yazdırma hello sonuçlarını hello işlemi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c56cc-226">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span>
* <span data-ttu-id="c56cc-227">toocreate Data Factory örnekleri toobe katılımcı/yönetici rolünüz hello Azure aboneliği gerekir</span><span class="sxs-lookup"><span data-stu-id="c56cc-227">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="c56cc-228">hello veri fabrikası Hello adı hello gelecekte bir DNS adı olarak kayıtlı ve bu nedenle herkese görünür hale gelir.</span><span class="sxs-lookup"><span data-stu-id="c56cc-228">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="c56cc-229">Merhaba hatayı alırsanız: "**Bu abonelik, Microsoft.DataFactory kayıtlı toouse ad değil**" Merhaba aşağıdakilerden birini yapın ve yeniden yayımlamayı deneyin:</span><span class="sxs-lookup"><span data-stu-id="c56cc-229">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="c56cc-230">Azure PowerShell'de komut tooregister hello Data Factory sağlayıcısının aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c56cc-230">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      <span data-ttu-id="c56cc-231">Bu Data Factory sağlayıcısının kayıtlı hello komutu tooconfirm aşağıdaki hello çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c56cc-231">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="c56cc-232">Oturum açma kullanılarak hello hello Azure aboneliğinize [Azure portal](https://portal.azure.com) ve tooa Data Factory dikey penceresine gidin (veya) hello Azure portalında bir data factory oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c56cc-232">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="c56cc-233">Bu eylemin hello sağlayıcıyı sizin için otomatik olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="c56cc-233">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="c56cc-234">Bir işlem hattı oluşturmadan önce toocreate birkaç Data Factory varlıklarını önce gerekir.</span><span class="sxs-lookup"><span data-stu-id="c56cc-234">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="c56cc-235">Bağlı hizmetler toolink veri depolarını/işlemlerini tooyour veri depolamak, giriş tanımlayın ve çıktı veri kümeleri toorepresent verilerini bağlı veri depolarında ilk oluşturduğunuzda.</span><span class="sxs-lookup"><span data-stu-id="c56cc-235">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent data in linked data stores.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="c56cc-236">Bağlı hizmetler oluşturma</span><span class="sxs-lookup"><span data-stu-id="c56cc-236">Create linked services</span></span>
<span data-ttu-id="c56cc-237">Bu adımda, Azure Storage hesabınızı ve bir isteğe bağlı Azure Hdınsight küme tooyour data factory bağlayın.</span><span class="sxs-lookup"><span data-stu-id="c56cc-237">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="c56cc-238">Azure depolama hesabı bu örnekteki hello ardışık düzeni için girdi ve çıktı verilerini ayrı tutma hello hello.</span><span class="sxs-lookup"><span data-stu-id="c56cc-238">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="c56cc-239">Merhaba Hdınsight bağlı hizmeti kullanılan toorun hello ardışık bu örnekteki hello etkinliğinde belirtilen Hive betiği ' dir.</span><span class="sxs-lookup"><span data-stu-id="c56cc-239">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="c56cc-240">Azure Storage bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="c56cc-240">Create Azure Storage linked service</span></span>
<span data-ttu-id="c56cc-241">Bu adımda, Azure depolama hesabı tooyour veri fabrikanıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="c56cc-241">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="c56cc-242">Bu öğretici ile kullandığınız hello toostore girdi/çıktı verilerin ve HQL hello komut dosyasını aynı Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="c56cc-242">With this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="c56cc-243">Adlı hello komutu toovariable Ata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="c56cc-243">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="c56cc-244">Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="c56cc-244">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="c56cc-245">Merhaba sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="c56cc-245">View hello results.</span></span> <span data-ttu-id="c56cc-246">Merhaba bağlı hizmet başarıyla oluşturuldu, hello JSON hello hello bağlantılı hizmeti için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c56cc-246">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="c56cc-247">Azure HDInsight bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="c56cc-247">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="c56cc-248">Bu adımda, bir isteğe bağlı Hdınsight kümesi tooyour data factory bağlayın.</span><span class="sxs-lookup"><span data-stu-id="c56cc-248">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="c56cc-249">Merhaba Hdınsight küme otomatik olarak çalışma zamanında oluşturulur ve hello belirtilen süre boyunca işlem yapma ve boşta bittikten sonra silinir.</span><span class="sxs-lookup"><span data-stu-id="c56cc-249">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="c56cc-250">İsteğe bağlı HDInsight kümesi yerine kendi HDInsight kümenizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c56cc-250">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="c56cc-251">Ayrıntılar için bkz. [İşlem Bağlı Hizmetleri](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="c56cc-251">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="c56cc-252">Adlı hello komutu toovariable Ata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="c56cc-252">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. <span data-ttu-id="c56cc-253">Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="c56cc-253">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="c56cc-254">Merhaba sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="c56cc-254">View hello results.</span></span> <span data-ttu-id="c56cc-255">Merhaba bağlı hizmet başarıyla oluşturuldu, hello JSON hello hello bağlantılı hizmeti için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c56cc-255">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="c56cc-256">Veri kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="c56cc-256">Create datasets</span></span>
<span data-ttu-id="c56cc-257">Bu adımda, veri kümeleri toorepresent hello girişi oluşturun ve Hive işlenmesi için verileri çıktı.</span><span class="sxs-lookup"><span data-stu-id="c56cc-257">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="c56cc-258">Bu veri kümeleri toohello başvuran **StorageLinkedService** Bu öğreticide daha önce oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="c56cc-258">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="c56cc-259">bağlantılı hizmet noktaları tooan Azure depolama hesabı hello ve veri kümeleri, giriş tutan hello depolamada kapsayıcı, klasör, dosya adı belirtin ve çıktı verilerini.</span><span class="sxs-lookup"><span data-stu-id="c56cc-259">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="c56cc-260">Girdi veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c56cc-260">Create input dataset</span></span>
<span data-ttu-id="c56cc-261">Bu adımda, hello girdi veri kümesi toorepresent giriş verisi hello Azure Blob depolamada depolanan oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c56cc-261">In this step, you create hello input dataset toorepresent input data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="c56cc-262">Adlı hello komutu toovariable Ata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="c56cc-262">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="c56cc-263">Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="c56cc-263">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="c56cc-264">Merhaba sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="c56cc-264">View hello results.</span></span> <span data-ttu-id="c56cc-265">Merhaba veri kümesi başarıyla oluşturuldu, hello JSON hello hello kümesinde için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c56cc-265">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="c56cc-266">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c56cc-266">Create output dataset</span></span>
<span data-ttu-id="c56cc-267">Bu adımda, hello Azure Blob Depolama depolanan hello çıkış veri kümesi toorepresent çıktı verileri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c56cc-267">In this step, you create hello output dataset toorepresent output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="c56cc-268">Adlı hello komutu toovariable Ata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="c56cc-268">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="c56cc-269">Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="c56cc-269">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="c56cc-270">Merhaba sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="c56cc-270">View hello results.</span></span> <span data-ttu-id="c56cc-271">Merhaba veri kümesi başarıyla oluşturuldu, hello JSON hello hello kümesinde için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c56cc-271">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a><span data-ttu-id="c56cc-272">İşlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c56cc-272">Create pipeline</span></span>
<span data-ttu-id="c56cc-273">Bu adımda, **HDInsightHive** etkinliğiyle ilk işlem hattınızı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="c56cc-273">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="c56cc-274">Girdi dilimi kullanılabilir aylık (sıklığı: Month, interval: 1), çıktı diliminin ayda bir oluşturulduğunu ve hello etkinlik hello Zamanlayıcı özelliğinin de toomonthly ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c56cc-274">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="c56cc-275">Merhaba çıktı veri kümesi ve hello etkinlik Zamanlayıcı Hello ayarlarının eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c56cc-275">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="c56cc-276">Şu anda, çıktı veri kümesi hello etkinlik herhangi bir çıktı üretmez olsa bile bir çıkış veri kümesi oluşturmanız gerekir böylece hangi sürücüleri zamanlama, hello değil.</span><span class="sxs-lookup"><span data-stu-id="c56cc-276">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="c56cc-277">Merhaba etkinlik herhangi bir girdi almazsa oluşturma hello girdi veri kümesi atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c56cc-277">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span>

<span data-ttu-id="c56cc-278">Merhaba gördüğünüzü onaylayın **input.log** hello dosyasında **adfgetstarted/inputdata** hello Azure blob depolama ve komut toodeploy hello ardışık aşağıdaki çalışma hello klasöründe.</span><span class="sxs-lookup"><span data-stu-id="c56cc-278">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="c56cc-279">Merhaba itibaren **Başlat** ve **son** hello son kez ayarlanır ve **isPaused** dağıtıldıktan hemen sonra kümesi toofalse, hello ardışık düzen (Merhaba ardışık düzeninde etkinlik) çalışması olduğu.</span><span class="sxs-lookup"><span data-stu-id="c56cc-279">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

1. <span data-ttu-id="c56cc-280">Adlı hello komutu toovariable Ata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="c56cc-280">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="c56cc-281">Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="c56cc-281">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="c56cc-282">Merhaba sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="c56cc-282">View hello results.</span></span> <span data-ttu-id="c56cc-283">Merhaba veri kümesi başarıyla oluşturuldu, hello JSON hello hello kümesinde için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c56cc-283">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```
4. <span data-ttu-id="c56cc-284">Tebrikler, Azure PowerShell kullanarak ilk işlem hattınızı başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="c56cc-284">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="c56cc-285">İşlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="c56cc-285">Monitor pipeline</span></span>
<span data-ttu-id="c56cc-286">Bu adımda, veri fabrikası REST API toomonitor dilimler hello ardışık düzen tarafından üretilen kullanın.</span><span class="sxs-lookup"><span data-stu-id="c56cc-286">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

```PowerShell
$ds ="AzureBlobOutput"

$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=1970-01-01T00%3a00%3a00.0000000Z"&"end=2016-08-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};

$results2 = Invoke-Command -scriptblock $cmd;

IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

> [!IMPORTANT]
> <span data-ttu-id="c56cc-287">İsteğe bağlı HDInsight kümesinin oluşturulması genellikle biraz zaman alır (yaklaşık 20 dakika).</span><span class="sxs-lookup"><span data-stu-id="c56cc-287">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="c56cc-288">Bu nedenle, hello ardışık düzen tootake beklediğiniz **yaklaşık olarak 30 dakika** tooprocess hello dilim.</span><span class="sxs-lookup"><span data-stu-id="c56cc-288">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
>

<span data-ttu-id="c56cc-289">Merhaba dilimi görene kadar bir sonraki hello Invoke-Command ve hello çalıştıran **hazır** durumu veya **başarısız** durumu.</span><span class="sxs-lookup"><span data-stu-id="c56cc-289">Run hello Invoke-Command and hello next one until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="c56cc-290">Merhaba dilim hazır durumunda olduğunda hello denetleyin **partitioneddata** hello klasöründe **adfgetstarted** hello için blob depolama alanınızın kapsayıcısında çıkış verileri.</span><span class="sxs-lookup"><span data-stu-id="c56cc-290">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="c56cc-291">İsteğe bağlı Hdınsight kümesinin Hello oluşturulması genellikle biraz zaman alır.</span><span class="sxs-lookup"><span data-stu-id="c56cc-291">hello creation of an on-demand HDInsight cluster usually takes some time.</span></span>

![çıktı verileri](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="c56cc-293">Merhaba dilim başarıyla işlendiğinde hello girdi dosyası silinir.</span><span class="sxs-lookup"><span data-stu-id="c56cc-293">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="c56cc-294">Bu nedenle, toorerun hello dilim istediğiniz veya öğreticiyi yeniden Merhaba, hello adfgetstarted kapsayıcısının hello girdi dosyasını (input.log) toohello inputdata klasörüne yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c56cc-294">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

<span data-ttu-id="c56cc-295">Ayrıca, Azure portal toomonitor dilimler kullanabilir ve ilgili sorunları giderin.</span><span class="sxs-lookup"><span data-stu-id="c56cc-295">You can also use Azure portal toomonitor slices and troubleshoot any issues.</span></span> <span data-ttu-id="c56cc-296">Ayrıntılar için bkz. [Azure Portal’ı kullanarak işlem hatlarını izleme](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline).</span><span class="sxs-lookup"><span data-stu-id="c56cc-296">See [Monitor pipelines using Azure portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) details.</span></span>

## <a name="summary"></a><span data-ttu-id="c56cc-297">Özet</span><span class="sxs-lookup"><span data-stu-id="c56cc-297">Summary</span></span>
<span data-ttu-id="c56cc-298">Bu öğreticide, bir Hdınsight hadoop kümesindeki Hive betiği çalıştıran bir Azure data factory tooprocess veri oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="c56cc-298">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="c56cc-299">Hello Data Factory Düzenleyici'hello Azure portal toodo hello aşağıdaki adımları kullanılır:</span><span class="sxs-lookup"><span data-stu-id="c56cc-299">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="c56cc-300">Oluşturulan Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="c56cc-300">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="c56cc-301">Oluşturulan iki **bağlı hizmet**:</span><span class="sxs-lookup"><span data-stu-id="c56cc-301">Created two **linked services**:</span></span>
   1. <span data-ttu-id="c56cc-302">**Azure depolama** hizmet toolink toohello veri fabrikası girdi/çıktı dosyalarını tutan Azure blob depolama alanınızın bağlı.</span><span class="sxs-lookup"><span data-stu-id="c56cc-302">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="c56cc-303">**Azure Hdınsight** isteğe bağlı bir isteğe bağlı Hdınsight Hadoop küme toohello data factory hizmeti toolink bağlı.</span><span class="sxs-lookup"><span data-stu-id="c56cc-303">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="c56cc-304">Azure Data Factory Hdınsight Hadoop küme yalnızca zaman tooprocess giriş verileri hem de üretim çıktı verilerini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c56cc-304">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="c56cc-305">Oluşturulan iki **veri kümeleri**, hello ardışık düzende Hdınsight Hive etkinliğiyle ilgili girdi ve çıktı verilerini açıklayan.</span><span class="sxs-lookup"><span data-stu-id="c56cc-305">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="c56cc-306">**HDInsight Hive** etkinliğine sahip oluşturulan bir **işlem hattı**.</span><span class="sxs-lookup"><span data-stu-id="c56cc-306">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c56cc-307">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c56cc-307">Next steps</span></span>
<span data-ttu-id="c56cc-308">Bu makalede, isteğe bağlı Azure HDInsight kümesinde bir Hive betiği çalıştıran dönüştürme etkinliğine (HDInsight Etkinliği) sahip işlem hattı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="c56cc-308">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="c56cc-309">toouse Azure Blob tooAzure SQL, bir kopyalama etkinliği toocopy verileri nasıl görürüm toosee [öğretici: bir Azure Blob tooAzure SQL veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c56cc-309">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="c56cc-310">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="c56cc-310">See Also</span></span>
| <span data-ttu-id="c56cc-311">Konu</span><span class="sxs-lookup"><span data-stu-id="c56cc-311">Topic</span></span> | <span data-ttu-id="c56cc-312">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c56cc-312">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="c56cc-313">Data Factory REST API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="c56cc-313">Data Factory REST API Reference</span></span>](/rest/api/datafactory/) |<span data-ttu-id="c56cc-314">Data Factory cmdlet'leri hakkında kapsamlı belgelere bakma</span><span class="sxs-lookup"><span data-stu-id="c56cc-314">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="c56cc-315">İşlem hatları</span><span class="sxs-lookup"><span data-stu-id="c56cc-315">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="c56cc-316">Bu makalede, işlem hatlarının ve etkinliklerin Azure Data Factory anlamanıza yardımcı olur ve nasıl toouse bunları tooconstruct uçtan uca veri odaklı iş akışlarının senaryo veya iş.</span><span class="sxs-lookup"><span data-stu-id="c56cc-316">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="c56cc-317">Veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="c56cc-317">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="c56cc-318">Bu makale, Azure Data Factory’deki veri kümelerini anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="c56cc-318">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="c56cc-319">Zamanlama ve Yürütme</span><span class="sxs-lookup"><span data-stu-id="c56cc-319">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="c56cc-320">Bu makalede Azure Data Factory uygulama modelinin hello zamanlama ve yürütme yönleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c56cc-320">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="c56cc-321">İzleme Uygulaması kullanılarak işlem hatlarını izleme ve yönetme</span><span class="sxs-lookup"><span data-stu-id="c56cc-321">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="c56cc-322">Bu makalede nasıl toomonitor, yönetme ve hatalarını ayıklama işlem hatlarını izleme ve yönetim uygulaması hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c56cc-322">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
