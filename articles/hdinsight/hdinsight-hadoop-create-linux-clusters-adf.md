---
title: "Data Factory - Azure Hdınsight kullanarak isteğe bağlı Hadoop kümelerini aaaCreate | Microsoft Docs"
description: "Nasıl toocreate Azure Data Factory kullanarak Hdınsight'ta isteğe bağlı Hadoop kümeleri hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: spelluru
ms.openlocfilehash: c869776ac270e37dec710b5fc8d2a792d9263129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a>Azure Data Factory kullanarak Hdınsight'ta isteğe bağlı Hadoop kümeleri oluşturma
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

[Azure Data Factory](../data-factory/data-factory-introduction.md) düzenler ve hello taşınmasını ve dönüştürülmesini veri otomatikleştiren bir bulut tabanlı veri tümleştirme hizmetidir. Bu bir Hdınsight Hadoop kümesi yalnızca zaman tooprocess bir giriş veri dilimi oluşturma ve hello işlem tamamlandığında hello küme silme. Bir isteğe bağlı Hdınsight Hadoop kümesi kullanarak hello avantajlarından bazıları şunlardır:

- Yalnızca ödeme hello süresi işi için Hdınsight Hadoop küme (bir kısa yapılandırılabilir boşta kalma süresi) hello çalışıyor. Hdınsight kümeleri için Hello fatura pro-dakika başına, bunları veya kullanıp kullanmadığınızı derecelendirilir. Veri fabrikasında bir isteğe bağlı Hdınsight bağlı hizmeti kullandığınızda, isteğe bağlı hello kümeleri oluşturulur. Ve hello işleri tamamlandığında hello kümeleri otomatik olarak silinir. Bu nedenle, yalnızca süresi ve hello kısa boşta kalma süresi (yaşam süresi ayarı) çalıştıran hello işi için ödeme yaparsınız.
- Data Factory işlem hattı kullanarak bir iş akışı oluşturabilirsiniz. Örneğin, bir şirket içi SQL Server tooan Azure blob depolama, bir isteğe bağlı Hdınsight Hadoop kümesinde bir Hive betiği ve Pig betiği çalıştırarak işlem hello verileri hello ardışık düzen toocopy verileri olabilir. Ardından, BI uygulamaları tooconsume için hello sonuç veri tooan Azure SQL Data Warehouse kopyalayın.
- Merhaba iş akışı toorun düzenli aralıklarla (saatlik, günlük, haftalık, aylık, vb.) zamanlayabilirsiniz.

Azure Data Factory'de veri fabrikası bir veya daha fazla veri işlem hattı olabilir. Veri ardışık bir veya daha fazla etkinlikler içeriyor. İki tür etkinlik vardır: [veri taşıma etkinlikleri](../data-factory/data-factory-data-movement-activities.md) ve [veri dönüştürme etkinlikleri](../data-factory/data-factory-data-transformation-activities.md). Bir kaynak veri deposu tooa hedef veri deposundan veri taşıma etkinlikleri (şu anda, yalnızca kopyalama etkinliği) toomove verileri kullanın. Veri dönüştürme etkinlikleri tootransform/işlem verileri kullanın. Hdınsight Hive etkinliği Data Factory ile desteklenen hello dönüştürme etkinlikleri biridir. Bu öğreticide hello Hive dönüşüm etkinliği kullanın.

Hive etkinliği toouse kendi Hdınsight Hadoop kümesi veya bir isteğe bağlı Hdınsight Hadoop kümesi yapılandırabilirsiniz. Bu öğreticide, hello hello data factory işlem hattı Hive etkinliğiyle yapılandırılmış toouse isteğe bağlı Hdınsight kümesi olur. Bu nedenle, hello etkinlik veri dilimi tooprocess çalıştırıldığında, şunlar olur:

1. Hdınsight Hadoop kümesi, yalnızca zaman tooprocess hello dilim için otomatik olarak oluşturulur.  
2. Merhaba giriş verisi hello kümede HiveQL betiğini çalıştırarak işlenir.
3. Merhaba Hdınsight Hadoop kümesi hello işlem tamamlandıktan sonra hello küme yapılandırılmış hello süreyi (timeToLive ayarını) için boşta silinir. Merhaba sonraki veri dilimi varsa bu timeToLive boşta kalma süresi ile işlemek için hello aynı kümede kullanılan tooprocess hello dilim olur.  

Bu öğreticide, hello hello hive etkinliği ile ilişkili HiveQL betiğini hello aşağıdaki eylemleri gerçekleştirir:

1. Bir Azure Blob depolamada depolanan ham web günlüğü verilerini başvuruları hello bir dış tablo oluşturur.
2. Yıl ve ay tarafından bölümleri hello ham verileri.
3. Depoları hello Azure blob depolama bölümlenmiş verilerde hello.

Bu öğreticide, hello hello hive etkinliği ile ilişkili HiveQL betiğini başvuruları hello Azure Blob Storage depolanan ham web günlüğü verilerini hello bir dış tablo oluşturur. Merhaba girdi dosyasında her ay hello örnek satırları şunlardır.

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

Merhaba HiveQL betiğini bölümleri, ay ve yıl ham verileri hello. Merhaba önceki girişinize göre üç çıkış klasör oluşturur. Her klasör her ay girişlerinden sahip bir dosya içerir.

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

Data Factory veri dönüştürme etkinlikleri toplama tooHive etkinliğinde bir listesi için bkz: [dönüştürme ve Azure Data Factory kullanarak Analiz](../data-factory/data-factory-data-transformation-activities.md).

> [!NOTE]
> Şu anda, Azure veri fabrikası'ndan yalnızca Hdınsight kümesi sürüm 3.2 oluşturabilirsiniz.

## <a name="prerequisites"></a>Ön koşullar
Bu makaledeki yönergeleri hello başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:

* [Azure aboneliği](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Azure PowerShell.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a>Depolama hesabını hazırlama
Bu senaryoda toothree depolama hesaplarını kullanabilirsiniz:

- Merhaba Hdınsight kümesi için varsayılan depolama hesabı
- Merhaba giriş verileri için depolama hesabı
- Merhaba çıktı verileri için depolama hesabı

toosimplify hello öğretici, bir depolama hesabı tooserve hello üç amacıyla kullanın. Bu bölümde bulunan hello Azure PowerShell örnek betiği hello aşağıdaki görevleri gerçekleştirir:

1. TooAzure oturum açın.
2. Bir Azure kaynak grubu oluşturun.
3. Bir Azure depolama hesabı oluşturun.
4. Merhaba depolama hesabında Blob kapsayıcısı oluşturma
5. İki dosyaları toohello Blob kapsayıcısı aşağıdaki hello kopyalayın:

   * Giriş veri dosyasını: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)
   * HiveQL betiğini: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)

     Her iki dosyaları bir ortak Blob kapsayıcısında depolanır.


**Azure PowerShell kullanarak tooprepare hello depolama ve kopyalama hello dosyalar:**
> [!IMPORTANT]
> Hello Azure kaynak grubu ve hello komut dosyası tarafından oluşturulacak hello Azure depolama hesabı adlarını belirtin.
> Yazma **kaynak grubu adı**, **depolama hesabı adı**, ve **depolama hesabı anahtarı** hello komut dosyası tarafından yüzdelik. Merhaba sonraki bölümde gereksinim duyarsınız.

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect tooAzure
####################################
#region - Connect tooAzure subscription
Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use hello following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

Merhaba PowerShell Betiği yardıma gereksinim duyarsanız, bkz: [kullanma hello Azure PowerShell'i Azure Storage ile](../storage/common/storage-powershell-guide-full.md). Azure CLI toouse gibi bunun yerine, hello görürseniz [ek](#appendix) hello Azure CLI komut dosyası için bölüm.

**tooexamine, hello depolama hesabı ve hello içeriği**

1. Toohello üzerinde oturum [Azure portal](https://portal.azure.com).
2. Tıklatın **kaynak grupları** hello sol bölmedeki.
3. PowerShell komut dosyasında oluşturulan hello kaynak grubu adı çift tıklatın. Listelenen çok fazla kaynak grupları varsa hello filtresini kullanın.
4. Merhaba üzerinde **kaynakları** kutucuğu, diğer projelerle hello kaynak grubu paylaşmak sürece listelenen bir kaynak sahip. Bu kaynak hello depolama hesabını daha önce belirtilen hello ada sahip değil. Merhaba depolama hesabının adına tıklayın.
5. Merhaba tıklatın **BLOB'lar** döşeme.
6. Merhaba tıklatın **adfgetstarted** kapsayıcı. İki klasör bkz: **inputdata** ve **betik**.
7. Merhaba klasörünü açın ve hello klasörlerdeki hello dosyaları denetleyin. Merhaba inputdata girdi verileriyle hello input.log dosya ve hello betik klasörü hello HiveQL komut dosyası içerir.

## <a name="create-a-data-factory-using-resource-manager-template"></a>Resource Manager şablonu kullanarak bir veri fabrikası oluşturun
Merhaba depolama hesabı, hello giriş verileri ve hello hazırlanmış HiveQL betiğini ile hazır toocreate bir Azure data factory değildir. Veri Fabrikası oluşturmaya yönelik birkaç yöntem vardır. Bu öğreticide, veri fabrikası hello Azure portal kullanarak bir Azure Resource Manager şablonu dağıtarak oluşturun. Kullanarak bir Resource Manager şablonu dağıtabilirsiniz [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) ve [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template). Diğer veri fabrikası oluşturma yöntemleri için bkz: [Öğreticisi: ilk data factory'nizi derleme](../data-factory/data-factory-build-your-first-pipeline.md).

1. Görüntü toosign tooAzure olarak ve açık hello Resource Manager şablonu hello Azure Portalı'nda aşağıdaki hello'ı tıklatın. Merhaba şablon https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json bulunur. Merhaba bkz [Data Factory varlıklarını hello şablonunda](#data-factory-entities-in-the-template) hello şablonda tanımlanan varlıklar hakkında ayrıntılı bilgi için bölüm. 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Seçin **kullanım varolan** hello seçeneği **kaynak grubu** ayarı ve select hello (PowerShell Betiği kullanılarak) hello önceki adımda oluşturduğunuz hello kaynak grubunun adını.
3. Merhaba veri fabrikası için bir ad girin (**veri fabrikası adı**). Bu ad genel olarak benzersiz olmalıdır.
4. Merhaba girin **depolama hesabı adı** ve **depolama hesabı anahtarı** hello önceki adımda yazdığınız.
5. Seçin **toohello hüküm ve koşulları kabul ediyorum** okuma sonra yukarıda belirtilen **hüküm ve koşullar**.
6. Seçin **PIN toodashboard** seçeneği.
6. Tıklatın **satın alma ve oluşturma**. Pano adlı hello üzerinde bir kutucuk gördüğünüz **dağıtma şablon dağıtımı**. Merhaba kadar bekleyin **kaynak grubu** kaynak grubunuz için bir dikey pencere açılır. Kaynak grubu adı tooopen hello kaynak grubu dikey pencerenizi başlıklı hello kutucuk de tıklayabilirsiniz.
6. Merhaba kaynak grubu dikey zaten açık değilse hello döşeme tooopen hello kaynak grubunu tıklatın. Göreceksiniz artık bir daha fazla veri fabrikası kaynak ayrıca toohello depolama hesabı kaynak listelenir.
7. Veri fabrikanızın Hello adına tıklayın (hello için belirtilen değer **veri fabrikası adı** parametresi).
8. Merhaba Data Factory dikey penceresinde hello tıklayın **diyagramı** döşeme. bir etkinliği bir girdi veri kümesi ve bir çıkış veri kümesi ile Merhaba diyagramda gösterilmiştir:

    ![Azure veri fabrikası Hdınsight isteğe bağlı Hive etkinlik ardışık düzeni diyagramı](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    Merhaba adları hello Resource Manager şablonunda tanımlanır.
9. Çift **AzureBlobOutput**.
10. Merhaba üzerinde **son güncelleştirilen dilimler**, bir dilim göreceksiniz. Merhaba durumundaysa **devam eden**, çok değiştirilmesini bekleyin**hazır**. Genellikle hakkında sürdüğünü **20 dakika** toocreate Hdınsight kümesi.

### <a name="check-hello-data-factory-output"></a>Merhaba veri fabrikası çıktısını denetleyin

1. Kullanım hello aynı hello son oturum toocheck Merhaba kapsayıcılara hello adfgetstarted kapsayıcısının yordamda. Var olan iki yeni kapsayıcılar ayrıca çok**adfgetsarted**:

   * Bir kapsayıcı adıyla hello deseni izler: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`. Merhaba varsayılan kapsayıcı hello Hdınsight kümesi için kapsayıcıdır.
   * adfjobs: Bu kapsayıcı hello ADF iş günlükleri için hello kapsayıcıdır.

     Merhaba veri fabrikası çıkış depolanır **afgetstarted** hello Resource Manager şablonunda yapılandırıldığı şekilde.
2. Tıklatın **adfgetstarted**.
3. Çift **partitioneddata**. Gördüğünüz bir **yıl 2014 =** klasörü tüm hello web günlüklerini yıl 2014 tarihli olduğundan.

    ![Azure veri fabrikası Hdınsight isteğe bağlı Hive etkinliği ardışık düzeni çıkış](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    Merhaba listede aşağı doğru ayrıntıya, Ocak, Şubat ve Mart için üç klasörleri göreceksiniz. Ve her ay için bir günlük yok.

    ![Azure veri fabrikası Hdınsight isteğe bağlı Hive etkinliği ardışık düzeni çıkış](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-hello-template"></a>Data Factory varlıklarını hello şablonunda
Veri Fabrikası için üst düzey Resource Manager şablonu hello benzer nasıl aşağıda verilmiştir:

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```

### <a name="define-data-factory"></a>Veri fabrikası tanımlama
Hello örnek aşağıdaki gösterildiği gibi bir veri fabrikası hello Resource Manager şablonunda tanımlayın:  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
Merhaba dataFactoryName hello şablonu dağıttığınızda belirttiğiniz hello veri fabrikası hello adıdır. Veri Fabrikası şu anda yalnızca hello Doğu ABD, Batı ABD ve Kuzey Avrupa bölgelerde desteklenir.

### <a name="defining-entities-within-hello-data-factory"></a>Merhaba veri fabrikası varlıkları tanımlama
Merhaba aşağıdaki Data Factory varlıklarını hello JSON şablonunda tanımlanmıştır:

* [Azure Storage bağlı hizmeti](#azure-storage-linked-service)
* [İsteğe bağlı HDInsight bağlı hizmeti](#hdinsight-on-demand-linked-service)
* [Azure Blob girdi veri kümesi](#azure-blob-input-dataset)
* [Azure Blob çıktı veri kümesi](#azure-blob-output-dataset)
* [Kopyalama etkinliği içeren bir veri işlem hattı](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Azure Storage bağlı hizmeti
Hello Azure depolama hizmeti Azure depolama hesabı toohello data factory'nizi bağlı. Bu öğreticide, hello aynı depolama hesabındaki hello varsayılan Hdınsight depolama hesabı, giriş veri depolama ve çıktı veri depolama kullanılır. Bu nedenle, bir Azure Storage bağlı hizmeti yalnızca tanımlayın. Merhaba bağlantılı hizmet tanımında hello adı ve Azure depolama hesabınızın anahtarı belirtin. Bkz: [Azure depolama bağlantılı hizmeti](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) JSON kullanılan özellikler toodefine hakkında ayrıntılı bilgi için bir Azure Storage bağlı hizmeti.

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
Merhaba **connectionString** hello storageAccountName ve storageAccountKey parametrelerini kullanır. Merhaba şablonu dağıtırken bu parametrelerin değerlerini belirtin.  

#### <a name="hdinsight-on-demand-linked-service"></a>İsteğe bağlı HDInsight bağlantılı hizmeti
Hello hizmet tanımı isteğe bağlı Hdınsight bağlı olarak bir Hdınsight Hadoop kümesi çalışma zamanında hello Data Factory hizmeti toocreate tarafından kullanılan yapılandırma parametreleri için değerleri belirtin. Bkz: [işlem bağlı Hizmetleri](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) bir Hdınsight isteğe bağlı hizmet makalesi JSON kullanılan özellikler toodefine hakkında ayrıntılı bilgi için.  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
Hello aşağıdaki noktaları göz önünde bulundurun:

* Merhaba Data Factory oluşturur bir **Linux tabanlı** , Hdınsight kümesi.
* Merhaba Hdınsight Hadoop kümesi hello aynı oluşturulan hello depolama hesabı bölgeye.
* Bildirim hello *timeToLive* ayarı. Merhaba küme 30 dakika boşta kaldıktan sonra hello veri fabrikası hello küme otomatik olarak siler.
* Merhaba Hdınsight kümesi oluşturur bir **varsayılan kapsayıcı** hello JSON belirtilen hello blob depolamada (**linkedServiceName**). Hdınsight Hello küme silindiğinde bu kapsayıcıyı silmez. Bu davranış tasarım gereğidir. Mevcut canlı bir küme olmadıkça işlenen toobe bir dilim gerekir her zaman isteğe bağlı Hdınsight bağlı hizmetiyle, Hdınsight kümesi oluşturulur (**timeToLive**) ve hello işlem bittiğinde silinir.

Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).

> [!IMPORTANT]
> Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz. Bunları hello işlerin sorunları giderilmesi için ihtiyacınız yoksa, toodelete isteyebilirsiniz bunları tooreduce hello depolama maliyeti. Bu kapsayıcıların Hello adları izleyen bir desen: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Gibi araçlar kullanın [Microsoft Storage Gezgini](http://storageexplorer.com/) toodelete kapsayıcılarında Azure blob depolama.

#### <a name="azure-blob-input-dataset"></a>Azure blob girdi veri kümesi
Merhaba girdi veri kümesi tanımında blob kapsayıcı, klasör ve hello giriş verisi içeren dosya hello adlarını belirtin. Bkz: [Azure Blob veri kümesi özellikleri](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) JSON kullanılan özellikler toodefine bir Azure Blob dataset hakkında ayrıntılı bilgi için.

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
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

Merhaba JSON tanımında belirli ayarları aşağıdaki hello dikkat edin:

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a>Azure Blob çıktı veri kümesi
Merhaba çıkış veri kümesi tanımında blob kapsayıcısı ve hello çıktı verilerini tutan klasör hello adlarını belirtin. Bkz: [Azure Blob veri kümesi özellikleri](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) JSON kullanılan özellikler toodefine bir Azure Blob dataset hakkında ayrıntılı bilgi için.  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

Merhaba folderPath hello çıktı verilerini tutan hello yolu toohello klasörü belirtir:

```json
"folderPath": "adfgetstarted/partitioneddata",
```

Merhaba [dataset kullanılabilirliği](../data-factory/data-factory-create-datasets.md#dataset-availability) ayarı aşağıdaki gibidir:

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

Azure Data Factory'de dataset kullanılabilirliği sürücüleri hello ardışık düzeni çıkış. Bu örnekte, hello dilim aylık (EndOfInterval) ayın son günü hello üzerinde oluşturulur. Daha fazla bilgi için bkz: [veri fabrikası zamanlama ve yürütme](../data-factory/data-factory-scheduling-and-execution.md).

#### <a name="data-pipeline"></a>Veri işlem hattı
İsteğe bağlı Azure Hdınsight kümesinde bir Hive betiği çalıştırılarak verileri dönüştüren bir ardışık düzen tanımlayın. Bkz: [ardışık düzen JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) JSON kullanılan öğeleri toodefine bu örnekteki işlem hattı açıklamaları için.

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

Merhaba ardışık bir etkinlik, Hdınsighthive etkinliğini içerir. Yalnızca bir ay (bir dilim) işlenir için Ocak 2016'da, veri hem de başlangıç ve bitiş tarihleri gibi. Her ikisi de *Başlat* ve *son* hello etkinliğini hello Data Factory hemen hello ay için verileri işleyen için geçmiş bir tarihe sahip. Merhaba son gelecekteki bir tarih ise, başlangıç zamanı geldiğinde hello veri fabrikası başka bir dilim oluşturur. Daha fazla bilgi için bkz: [veri fabrikası zamanlama ve yürütme](../data-factory/data-factory-scheduling-and-execution.md).

## <a name="clean-up-hello-tutorial"></a>Merhaba öğreticiyi silme

### <a name="delete-hello-blob-containers-created-by-on-demand-hdinsight-cluster"></a>İsteğe bağlı Hdınsight kümesi tarafından oluşturulan hello blob kapsayıcıları Sil
Mevcut canlı bir küme (timeToLive); olmadıkça işlenen toobe bir dilim gerekir her zaman isteğe bağlı Hdınsight bağlı hizmetiyle, Hdınsight kümesi oluşturulur ve hello küme hello işlem bittiğinde silinir. Her küme için Azure Data Factory hello Azure blob depolama hello varsayılan stroage hesap olarak hello kümesi için kullanılan bir blob kapsayıcısını oluşturur. Hdınsight kümesi silindi olsa bile, hello varsayılan blob depolama kapsayıcısını ve ilişkili hello depolama hesabı silinmez. Bu davranış tasarım gereğidir. Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz. Bunları hello işlerin sorunları giderilmesi için ihtiyacınız yoksa, toodelete isteyebilirsiniz bunları tooreduce hello depolama maliyeti. Bu kapsayıcıların Hello adları izleyen bir desen: `adfyourdatafactoryname-linkedservicename-datetimestamp`.

Merhaba silme **adfjobs** ve **adfyourdatafactoryname linkedservicename datetimestamp** klasörler. Merhaba adfjobs kapsayıcısı Azure Data Factory iş günlükleri içerir.

### <a name="delete-hello-resource-group"></a>Merhaba kaynak grubunu silme
[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) kullanılan toodeploy olan yönetebilir ve çözümünüzün bir grup olarak izleyebilirsiniz.  Bir kaynak grubunu silme hello grup içindeki tüm hello bileşenleri siler.  

1. Toohello üzerinde oturum [Azure portal](https://portal.azure.com).
2. Tıklatın **kaynak grupları** hello sol bölmedeki.
3. PowerShell komut dosyasında oluşturulan hello kaynak grubu adı'ı tıklatın. Listelenen çok fazla kaynak grupları varsa hello filtresini kullanın. Merhaba kaynak grubu yeni bir dikey pencerede açar.
4. Merhaba üzerinde **kaynakları** kutucuğu elinizde hello varsayılan depolama hesabı ve diğer projelerle hello kaynak grubu paylaşmak sürece listelenen hello veri fabrikası.
5. Tıklatın **silmek** hello dikey hello üstte. Bunun yapılması, hello depolama hesabı ve hello depolama hesabında depolanan hello verileri siler.
6. Merhaba kaynak grubu adı tooconfirm silme girin ve ardından **silmek**.

Merhaba kaynak grubunu sildiğinizde toodelete hello depolama hesabı istemediğiniz durumda hello varsayılan depolama hesabından hello iş verilerini ayırarak mimarisi aşağıdaki hello göz önünde bulundurun. Bu durumda, hello iş verileriyle hello depolama hesabı için bir kaynak grubuna sahip ve diğer kaynak grubu hello varsayılan depolama hesabı Hdınsight bağlantılı hizmeti ve hello veri fabrikası için hello. Merhaba ikinci kaynak grubu sildiğinizde, hello iş veri depolama hesabı etkilemez. toodo için:

* Merhaba, Resource Manager şablonu Microsoft.DataFactory/datafactories kaynağında birlikte toohello en üst düzey kaynak grubu aşağıdaki hello ekleyin. Bir depolama hesabı oluşturur:

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* Yeni bağlı hizmet noktası toohello yeni bir depolama hesabı ekleyin:

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* Merhaba Hdınsight bağlantılı ondemand hizmeti ek dependsOn ve bir additionalLinkedServiceNames yapılandırın:

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, öğrendiğiniz nasıl toouse Azure Data Factory toocreate isteğe bağlı Hdınsight kümesi tooprocess Hive işleri. Daha fazla tooread:

* [Hadoop Öğreticisi: Hdınsight'ta Linux tabanlı Hadoop ile çalışmaya başlamak](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Hdınsight'ta Linux tabanlı Hadoop kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md)
* [Hdınsight belgeleri](https://azure.microsoft.com/documentation/services/hdinsight/)
* [Veri Fabrikası belgeleri](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a>Ek

### <a name="azure-cli-script"></a>Azure CLI komut dosyası
Azure PowerShell toodo hello öğretici kullanmak yerine, Azure CLI kullanabilirsiniz. Azure CLI toouse yönergeleri izleyerek hello göredir önce Azure CLI yükleyin:

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-tooprepare-hello-storage-and-copy-hello-files"></a>Azure CLI tooprepare hello depolama kullanan ve hello dosyaları kopyalayın

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

Merhaba kapsayıcı adı *adfgetstarted*. Olduğu gibi tutun. Aksi takdirde tooupdate hello Resource Manager şablonu gerekir. Bu CLI betik yardıma gereksinim duyarsanız, bkz: [kullanma hello Azure Storage ile Azure CLI](../storage/common/storage-azure-cli.md).
