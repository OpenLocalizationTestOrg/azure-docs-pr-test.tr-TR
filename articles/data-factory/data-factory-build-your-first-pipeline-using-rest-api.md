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
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a>Öğretici: Data Factory REST API kullanarak ilk Azure data factory’nizi derleme
> [!div class="op_single_selector"]
> * [Genel bakış ve önkoşullar](data-factory-build-your-first-pipeline.md)
> * [Azure portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager Şablonu](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


Bu makalede, ilk Azure data factory'nizi veri fabrikası REST API toocreate kullanın. diğer araçlar/SDK, kullanarak toodo hello öğretici seçin hello seçeneklerden birini hello aşağı açılan listeden.

Bu öğreticide Hello ardışık bir etkinlik vardır: **Hdınsight Hive etkinliği**. Bu etkinlik dönüşümler veri tooproduce çıkış veri girişi bir Azure Hdınsight kümesinde bir hive betiği çalıştırır. Başlangıç ve bitiş zamanlarını hello arasında bir ay belirtilen sonra hello ardışık düzen zamanlanmış toorun ' dir.

> [!NOTE]
> Bu makalede, tüm hello REST API kapsamaz. REST API ile ilgili kapsamlı belgeler için bkz. [Data Factory REST API Başvurusu](/rest/api/datafactory/).
> 
> Bir işlem hattında birden fazla etkinlik olabilir. Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir. Daha fazla bilgi için bkz. [Data Factory'de zamanlama ve yürütme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).


## <a name="prerequisites"></a>Ön koşullar
* Okuyun [öğreticiye genel bakış](data-factory-build-your-first-pipeline.md) makale ve tam hello **önkoşul** adımları.
* [Curl](https://curl.haxx.se/dlwiz/) aracını makinenize yükleyin. REST komutları toocreate data factory hello CURL aracını kullanın.
* Aşağıdakileri yapmak için [bu makaledeki](../azure-resource-manager/resource-group-create-service-principal-portal.md) yönergeleri izleyin:
  1. Azure Active Directory’de **ADFGetStartedApp** adlı bir Web uygulaması oluşturun.
  2. **İstemci kimliği** ve **gizli anahtarı** alın.
  3. **İstemci kimliğini** alın.
  4. Merhaba atamak **ADFGetStartedApp** uygulama toohello **veri fabrikası katkıda bulunan** rol.
* [Azure PowerShell](/powershell/azure/overview)'i yükleyin.
* Başlatma **PowerShell** ve çalışma hello aşağıdaki komutu. Bu öğreticide hello sonuna kadar Azure PowerShell'i açık tutun. Kapatıp yeniden açın, toorun hello komutları yeniden gerekir.
  1. Çalıştırma **Login-AzureRmAccount** hello kullanıcı adı ve toosign toohello Azure portal kullanın parolayı girin.
  2. Çalıştırma **Get-AzureRmSubscription** tooview tüm abonelikler için bu hesabı hello.
  3. Çalıştırma **Get-AzureRmSubscription - varlığıyla SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** toowork ile istediğiniz tooselect hello abonelik. Değiştir **NameOfAzureSubscription** , Azure aboneliğinizin hello adı.
* Adlı bir Azure kaynak grubu oluşturma **ADFTutorialResourceGroup** hello PowerShell komutunda aşağıdaki hello çalıştırarak:

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   Merhaba bu öğreticideki adımlardan bazıları ADFTutorialResourceGroup adlı hello kaynak grubunu kullandığınızı varsayar. Farklı bir kaynak grubu kullanıyorsanız, bu öğreticide ADFTutorialResourceGroup yerine, kaynak grubunun toouse hello adı gerekir.

## <a name="create-json-definitions"></a>JSON tanımları oluşturma
JSON dosyaları curl.exe bulunduğu hello klasöründe aşağıdaki oluşturun.

### <a name="datafactoryjson"></a>datafactory.json
> [!IMPORTANT]
> Tooprefix/sonek ADFCopyTutorialDF toomake isteyebilirsiniz adı genel olarak benzersiz olmalıdır, benzersiz bir ad.
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a>azurestoragelinkedservice.json
> [!IMPORTANT]
> **accountname** ve **accountkey** sözcüklerini Azure depolama hesabınızın adı ve anahtarıyla değiştirin. toolearn tooget depolama alanınızın erişim nasıl anahtar, hello bilgi nasıl tooview, kopyalama ve yeniden oluşturma depolama erişim anahtarları içinde hakkında [depolama hesabınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
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

### <a name="hdinsightondemandlinkedservicejson"></a>hdinsightondemandlinkedservice.JSON

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

Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:

| Özellik | Açıklama |
|:--- |:--- |
| ClusterSize |Merhaba Hdınsight küme boyutu. |
| TimeToLive |Silinmeden önce hello Hdınsight kümesi, o hello boşta kalma süresini belirtir. |
| linkedServiceName |Hdınsight tarafından oluşturulan kullanılan toostore hello günlükleri olan hello depolama hesabını belirtir |

Hello aşağıdaki noktaları göz önünde bulundurun:

* Merhaba Data Factory oluşturur bir **Linux tabanlı** hello yukarıdaki JSON ile sizin için Hdınsight kümesi. Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).
* İsteğe bağlı HDInsight kümesi yerine **kendi HDInsight kümenizi** kullanabilirsiniz. Ayrıntılar için bkz. [HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).
* Merhaba Hdınsight kümesi oluşturur bir **varsayılan kapsayıcı** hello JSON belirtilen hello blob depolamada (**linkedServiceName**). Hdınsight Hello küme silindiğinde bu kapsayıcıyı silmez. Bu davranış tasarım gereğidir. Mevcut canlı bir küme olmadıkça bir dilim işlenen her zaman isteğe bağlı Hdınsight bağlı hizmetiyle, Hdınsight kümesi oluşturulur (**timeToLive**) ve hello işlem bittiğinde silinir.

    Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz. Bunları hello işlerin sorunları giderilmesi için ihtiyacınız yoksa, toodelete isteyebilirsiniz bunları tooreduce hello depolama maliyeti. Bu kapsayıcıların Hello adları izleyen bir desen: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Gibi araçlar kullanın [Microsoft Storage Gezgini](http://storageexplorer.com/) toodelete kapsayıcılarında Azure blob depolama.

Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).

### <a name="inputdatasetjson"></a>inputdataset.json

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

Merhaba JSON adlı veri kümesini tanımlayan **Azureblobınput**, hello ardışık düzeninde bir etkinliğin girdi verilerini temsil eder. Ayrıca, hello giriş verisi adlı hello blob kapsayıcısında bulunur belirtir **adfgetstarted** ve adlı hello klasör **inputdata**.

Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:

| Özellik | Açıklama |
|:--- |:--- |
| type |verileri Azure blob depolamada yer aldığından hello type özelliği tooAzureBlob ayarlanır. |
| linkedServiceName |daha önce oluşturduğunuz StorageLinkedService toohello başvuruyor. |
| fileName |Bu özellik isteğe bağlıdır. Bu özelliği atarsanız, hello folderPath tüm hello dosyalarından çekilir. Bu durumda, yalnızca hello input.log işlenir. |
| type |Merhaba günlük dosyaları metin biçiminde olduğundan TextFormat kullanacağız. |
| columnDelimiter |Merhaba günlük dosyalarındaki Sütunlar virgül karakteriyle (,) tarafından ayrılır |
| frequency/interval |tooMonth sıklığını ve aralığı hello girdi dilimlerinin aylık olarak kullanılabileceğini 1. |
| external |Merhaba giriş verisi hello Data Factory hizmetiyle oluşturulmadıysa, bu özellik tootrue ayarlanır. |

### <a name="outputdatasetjson"></a>outputdataset.json

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

Merhaba JSON adlı veri kümesini tanımlayan **AzureBlobOutput**, hello ardışık düzeninde bir etkinliğin çıktı verilerini temsil eder. Ayrıca, hello sonuçları adlı hello blob kapsayıcısında depolanır belirtir **adfgetstarted** ve adlı hello klasör **partitioneddata**. Merhaba **kullanılabilirlik** bölümü belirtiyor bu hello çıktı veri kümesi, aylık olarak oluşturulur.

### <a name="pipelinejson"></a>pipeline.json
> [!IMPORTANT]
> **storageaccountname**’i Azure depolama hesabınızın adıyla değiştirin.
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

Merhaba JSON parçacığında, Hdınsight kümesinde Hive tooprocess verilerini kullanan tek bir etkinlik oluşan bir işlem hattı oluşturuyorsunuz.

Merhaba Hive betik dosyası **partitionweblogs.hql**, hello Azure depolama hesabı depolanır (adlı hello scriptLinkedService tarafından belirtilen **StorageLinkedService**) ve **komut dosyası ** hello kapsayıcı klasöründe **adfgetstarted**.

Merhaba **tanımlar** bölüm toohello hive betiğini Hive yapılandırma değerleri olarak geçirilir çalışma zamanı ayarları belirtir (örn., ${hiveconf: inputtable}, ${hiveconf}).

Merhaba **Başlat** ve **son** hello ardışık düzen özelliklerini hello etkin dönem hello ardışık belirtir.

Bu hello Hive betiğini hello tarafından belirtilen hello işlem üzerinde çalıştığı belirtin Hello JSON etkinliğinde **linkedServiceName** – **Hdınsightondemandlinkedservice**.

> [!NOTE]
> "Ardışık düzen JSON" bölümüne bakın [işlem hatlarının ve etkinliklerin Azure Data Factory](data-factory-create-pipelines.md) hello önceki örnekte kullanılan JSON özellikleri hakkında ayrıntılı bilgi için.
>
>

## <a name="set-global-variables"></a>Genel değişkenleri ayarlama
Azure PowerShell'de komutları hello değerleri kendi değerlerinizle değiştirerek sonra aşağıdaki hello yürütün:

> [!IMPORTANT]
> İstemci kimliği, istemci parolası, kiracı kimliği ve abonelik kimliğini edinme konusunda yönergeler için [Önkoşullar](#prerequisites) bölümüne bakın.
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


## <a name="authenticate-with-aad"></a>AAD ile kimlik doğrulama

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a>Veri fabrikası oluşturma
Bu adımda, **FirstDataFactoryREST** adlı bir Azure Data Factory oluşturursunuz. Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir. İşlem hattında bir veya daha fazla etkinlik olabilir. Örneğin, bir kopyalama etkinliği toocopy verilerinden bir kaynak tooa hedef veri deposu ve Hdınsight Hive etkinliği toorun bir Hive betiği tootransform veri. Aşağıdaki komutları toocreate hello veri fabrikası hello çalıştırın:

1. Adlı hello komutu toovariable Ata **cmd**.

    Burada belirttiğiniz (ADFCopyTutorialDF) eşleşmeleri hello hello belirtilen adı hello veri fabrikası bu hello adını onaylayın **datafactory.json**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Merhaba sonuçları görüntüleyin. Merhaba veri fabrikası başarıyla oluşturuldu, hello JSON hello hello veri fabrikasında için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.

    ```PowerShell
    Write-Host $results
    ```

Hello aşağıdaki noktaları göz önünde bulundurun:

* Merhaba hello Azure Data Factory adı küresel olarak benzersiz olmalıdır. Sonuçları hello hata görürseniz: **veri fabrikası adı "FirstDataFactoryREST" kullanılabilir değil**, adımları hello:
  1. Merhaba değişiklik hello adı (örneğin, yournameFirstDataFactoryREST) **datafactory.json** dosya. Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.
  2. Merhaba ilk komutta burada hello **$cmd** değişken değeri atanır, FirstDataFactoryREST hello yeni adıyla değiştirin ve hello komutunu çalıştırın.
  3. Merhaba sonraki iki komutları tooinvoke hello REST API toocreate hello veri fabrikası ve yazdırma hello sonuçlarını hello işlemi çalıştırın.
* toocreate Data Factory örnekleri toobe katılımcı/yönetici rolünüz hello Azure aboneliği gerekir
* hello veri fabrikası Hello adı hello gelecekte bir DNS adı olarak kayıtlı ve bu nedenle herkese görünür hale gelir.
* Merhaba hatayı alırsanız: "**Bu abonelik, Microsoft.DataFactory kayıtlı toouse ad değil**" Merhaba aşağıdakilerden birini yapın ve yeniden yayımlamayı deneyin:

  * Azure PowerShell'de komut tooregister hello Data Factory sağlayıcısının aşağıdaki hello çalıştırın:

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      Bu Data Factory sağlayıcısının kayıtlı hello komutu tooconfirm aşağıdaki hello çalıştırabilirsiniz:
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Oturum açma kullanılarak hello hello Azure aboneliğinize [Azure portal](https://portal.azure.com) ve tooa Data Factory dikey penceresine gidin (veya) hello Azure portalında bir data factory oluşturun. Bu eylemin hello sağlayıcıyı sizin için otomatik olarak kaydeder.

Bir işlem hattı oluşturmadan önce toocreate birkaç Data Factory varlıklarını önce gerekir. Bağlı hizmetler toolink veri depolarını/işlemlerini tooyour veri depolamak, giriş tanımlayın ve çıktı veri kümeleri toorepresent verilerini bağlı veri depolarında ilk oluşturduğunuzda.

## <a name="create-linked-services"></a>Bağlı hizmetler oluşturma
Bu adımda, Azure Storage hesabınızı ve bir isteğe bağlı Azure Hdınsight küme tooyour data factory bağlayın. Azure depolama hesabı bu örnekteki hello ardışık düzeni için girdi ve çıktı verilerini ayrı tutma hello hello. Merhaba Hdınsight bağlı hizmeti kullanılan toorun hello ardışık bu örnekteki hello etkinliğinde belirtilen Hive betiği ' dir.

### <a name="create-azure-storage-linked-service"></a>Azure Storage bağlı hizmeti oluşturma
Bu adımda, Azure depolama hesabı tooyour veri fabrikanıza bağlayın. Bu öğretici ile kullandığınız hello toostore girdi/çıktı verilerin ve HQL hello komut dosyasını aynı Azure depolama hesabı.

1. Adlı hello komutu toovariable Ata **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Merhaba sonuçları görüntüleyin. Merhaba bağlı hizmet başarıyla oluşturuldu, hello JSON hello hello bağlantılı hizmeti için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a>Azure HDInsight bağlı hizmeti oluşturma
Bu adımda, bir isteğe bağlı Hdınsight kümesi tooyour data factory bağlayın. Merhaba Hdınsight küme otomatik olarak çalışma zamanında oluşturulur ve hello belirtilen süre boyunca işlem yapma ve boşta bittikten sonra silinir. İsteğe bağlı HDInsight kümesi yerine kendi HDInsight kümenizi kullanabilirsiniz. Ayrıntılar için bkz. [İşlem Bağlı Hizmetleri](data-factory-compute-linked-services.md).

1. Adlı hello komutu toovariable Ata **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Merhaba sonuçları görüntüleyin. Merhaba bağlı hizmet başarıyla oluşturuldu, hello JSON hello hello bağlantılı hizmeti için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a>Veri kümeleri oluşturma
Bu adımda, veri kümeleri toorepresent hello girişi oluşturun ve Hive işlenmesi için verileri çıktı. Bu veri kümeleri toohello başvuran **StorageLinkedService** Bu öğreticide daha önce oluşturduğunuz. bağlantılı hizmet noktaları tooan Azure depolama hesabı hello ve veri kümeleri, giriş tutan hello depolamada kapsayıcı, klasör, dosya adı belirtin ve çıktı verilerini.

### <a name="create-input-dataset"></a>Girdi veri kümesi oluşturma
Bu adımda, hello girdi veri kümesi toorepresent giriş verisi hello Azure Blob depolamada depolanan oluşturun.

1. Adlı hello komutu toovariable Ata **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Merhaba sonuçları görüntüleyin. Merhaba veri kümesi başarıyla oluşturuldu, hello JSON hello hello kümesinde için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a>Çıktı veri kümesi oluşturma
Bu adımda, hello Azure Blob Depolama depolanan hello çıkış veri kümesi toorepresent çıktı verileri oluşturun.

1. Adlı hello komutu toovariable Ata **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Merhaba sonuçları görüntüleyin. Merhaba veri kümesi başarıyla oluşturuldu, hello JSON hello hello kümesinde için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a>İşlem hattı oluşturma
Bu adımda, **HDInsightHive** etkinliğiyle ilk işlem hattınızı oluşturursunuz. Girdi dilimi kullanılabilir aylık (sıklığı: Month, interval: 1), çıktı diliminin ayda bir oluşturulduğunu ve hello etkinlik hello Zamanlayıcı özelliğinin de toomonthly ayarlayın. Merhaba çıktı veri kümesi ve hello etkinlik Zamanlayıcı Hello ayarlarının eşleşmesi gerekir. Şu anda, çıktı veri kümesi hello etkinlik herhangi bir çıktı üretmez olsa bile bir çıkış veri kümesi oluşturmanız gerekir böylece hangi sürücüleri zamanlama, hello değil. Merhaba etkinlik herhangi bir girdi almazsa oluşturma hello girdi veri kümesi atlayabilirsiniz.

Merhaba gördüğünüzü onaylayın **input.log** hello dosyasında **adfgetstarted/inputdata** hello Azure blob depolama ve komut toodeploy hello ardışık aşağıdaki çalışma hello klasöründe. Merhaba itibaren **Başlat** ve **son** hello son kez ayarlanır ve **isPaused** dağıtıldıktan hemen sonra kümesi toofalse, hello ardışık düzen (Merhaba ardışık düzeninde etkinlik) çalışması olduğu.

1. Adlı hello komutu toovariable Ata **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Merhaba sonuçları görüntüleyin. Merhaba veri kümesi başarıyla oluşturuldu, hello JSON hello hello kümesinde için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.

    ```PowerShell
    Write-Host $results
    ```
4. Tebrikler, Azure PowerShell kullanarak ilk işlem hattınızı başarıyla oluşturdunuz.

## <a name="monitor-pipeline"></a>İşlem hattını izleme
Bu adımda, veri fabrikası REST API toomonitor dilimler hello ardışık düzen tarafından üretilen kullanın.

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
> İsteğe bağlı HDInsight kümesinin oluşturulması genellikle biraz zaman alır (yaklaşık 20 dakika). Bu nedenle, hello ardışık düzen tootake beklediğiniz **yaklaşık olarak 30 dakika** tooprocess hello dilim.
>
>

Merhaba dilimi görene kadar bir sonraki hello Invoke-Command ve hello çalıştıran **hazır** durumu veya **başarısız** durumu. Merhaba dilim hazır durumunda olduğunda hello denetleyin **partitioneddata** hello klasöründe **adfgetstarted** hello için blob depolama alanınızın kapsayıcısında çıkış verileri.  İsteğe bağlı Hdınsight kümesinin Hello oluşturulması genellikle biraz zaman alır.

![çıktı verileri](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> Merhaba dilim başarıyla işlendiğinde hello girdi dosyası silinir. Bu nedenle, toorerun hello dilim istediğiniz veya öğreticiyi yeniden Merhaba, hello adfgetstarted kapsayıcısının hello girdi dosyasını (input.log) toohello inputdata klasörüne yükleyin.
>
>

Ayrıca, Azure portal toomonitor dilimler kullanabilir ve ilgili sorunları giderin. Ayrıntılar için bkz. [Azure Portal’ı kullanarak işlem hatlarını izleme](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline).

## <a name="summary"></a>Özet
Bu öğreticide, bir Hdınsight hadoop kümesindeki Hive betiği çalıştıran bir Azure data factory tooprocess veri oluşturuldu. Hello Data Factory Düzenleyici'hello Azure portal toodo hello aşağıdaki adımları kullanılır:

1. Oluşturulan Azure **data factory**.
2. Oluşturulan iki **bağlı hizmet**:
   1. **Azure depolama** hizmet toolink toohello veri fabrikası girdi/çıktı dosyalarını tutan Azure blob depolama alanınızın bağlı.
   2. **Azure Hdınsight** isteğe bağlı bir isteğe bağlı Hdınsight Hadoop küme toohello data factory hizmeti toolink bağlı. Azure Data Factory Hdınsight Hadoop küme yalnızca zaman tooprocess giriş verileri hem de üretim çıktı verilerini oluşturur.
3. Oluşturulan iki **veri kümeleri**, hello ardışık düzende Hdınsight Hive etkinliğiyle ilgili girdi ve çıktı verilerini açıklayan.
4. **HDInsight Hive** etkinliğine sahip oluşturulan bir **işlem hattı**.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, isteğe bağlı Azure HDInsight kümesinde bir Hive betiği çalıştıran dönüştürme etkinliğine (HDInsight Etkinliği) sahip işlem hattı oluşturdunuz. toouse Azure Blob tooAzure SQL, bir kopyalama etkinliği toocopy verileri nasıl görürüm toosee [öğretici: bir Azure Blob tooAzure SQL veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="see-also"></a>Ayrıca Bkz.
| Konu | Açıklama |
|:--- |:--- |
| [Data Factory REST API Başvurusu](/rest/api/datafactory/) |Data Factory cmdlet'leri hakkında kapsamlı belgelere bakma |
| [İşlem hatları](data-factory-create-pipelines.md) |Bu makalede, işlem hatlarının ve etkinliklerin Azure Data Factory anlamanıza yardımcı olur ve nasıl toouse bunları tooconstruct uçtan uca veri odaklı iş akışlarının senaryo veya iş. |
| [Veri kümeleri](data-factory-create-datasets.md) |Bu makale, Azure Data Factory’deki veri kümelerini anlamanıza yardımcı olur. |
| [Zamanlama ve Yürütme](data-factory-scheduling-and-execution.md) |Bu makalede Azure Data Factory uygulama modelinin hello zamanlama ve yürütme yönleri açıklanmaktadır. |
| [İzleme Uygulaması kullanılarak işlem hatlarını izleme ve yönetme](data-factory-monitor-manage-app.md) |Bu makalede nasıl toomonitor, yönetme ve hatalarını ayıklama işlem hatlarını izleme ve yönetim uygulaması hello kullanarak. |
