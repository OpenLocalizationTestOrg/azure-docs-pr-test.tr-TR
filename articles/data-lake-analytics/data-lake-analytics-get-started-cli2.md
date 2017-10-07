---
title: "aaaGet kullanarak Azure Data Lake Azure CLI 2.0 Analytics ile çalışmaya | Microsoft Docs"
description: "Toouse hello Azure komut satırı arabirimi 2.0 toocreate Data Lake Analytics hesabı, U-SQL'yi kullanarak Data Lake Analytics işi oluşturma ve hello işi göndermek öğrenin. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: jgao
ms.openlocfilehash: c4e91c0d3526e4932c2948c0a326d4cedc985791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a>Azure CLI 2.0 aracını kullanarak Azure Data Lake Analytics ile çalışmaya başlama
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Bu öğreticide, sekmeyle ayrılmış değerler (TSV) dosyasını okuyan ve bu dosyayı virgülle ayrılmış değerler (CSV) dosyasına dönüştüren bir iş geliştireceksiniz. aynı öğreticiyi diğer kullanarak desteklenen hello aracılığıyla toogo araçları, bu bölümün hello üstte hello açılır listesi kullan.

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).
* **Azure CLI 2.0**. Bkz. [Azure CLI'yı yükleme ve yapılandırma](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="log-in-tooazure"></a>İçinde tooAzure oturum

toolog tooyour Azure abonelik içinde:

```
azurecli
az login
```

İstenen toobrowse tooa URL olan ve bir kimlik doğrulaması kodunu girin.  Ve ardından kimlik bilgilerinizi hello yönergeleri tooenter izleyin.

Oturum açtıktan sonra hello oturum açma komut aboneliklerinizi listeler.

belirli bir aboneliği toouse:

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a>Data Lake Analytics hesabı oluşturma
Herhangi bir işi çalıştırmadan önce bir Data Lake Analytics hesabına sahip olmanız gerekir. toocreate Data Lake Analytics hesabı, aşağıdaki öğelerindeki hello belirtmeniz gerekir:

* **Azure Kaynak Grubu**. Azure Kaynak Grubu'nda bir Data Lake Analytics hesabı oluşturulmalıdır. [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) toowork hello kaynaklarla bir grup olarak sağlar. Dağıtma, güncelleştirme veya hello kaynakların tümünü tek ve eşgüdümlü bir işlemle uygulamanızda için silme.  

toolist hello varolan kaynak gruplarını aboneliğinizi altında:

```
az group list
```

Yeni bir kaynak grubu toocreate:

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* **Data Lake Analytics hesap adı**. Her Data Lake Analytics hesabının bir adı vardır.
* **Konum**. Data Lake Analytics destekleyen hello Azure veri merkezlerinde birini kullanın.
* **Varsayılan Data Lake Store hesabı**: Her Data Lake Analytics hesabı, bir varsayılan Data Lake Store hesabına sahiptir.

toolist hello varolan Data Lake Store hesabı:

```
az dls account list
```

toocreate yeni bir Data Lake Store hesabı:

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

Sözdizimi toocreate Data Lake Analytics hesabı aşağıdaki hello kullan:

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

Bir hesap oluşturduktan sonra aşağıdaki komutları toolist hello hesapları hello kullanın ve hesap ayrıntıları göster:

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a>Veri tooData Lake deposu karşıya yükle
Bu eğiticide, bazı arama günlüklerini işleyeceksiniz.  Merhaba arama günlüğü, Data Lake store veya Azure Blob storage ' depolanabilir.

Hello Azure portal, bir arama günlüğü dosyası içeren bazı örnek veri dosyalarını toohello varsayılan Data Lake Store hesabı, kopyalamak için bir kullanıcı arabirimi sağlar. Bkz: [kaynak verileri hazırlama](data-lake-analytics-get-started-portal.md) tooupload hello veri toohello varsayılan Data Lake Store hesabı.

CLI 2.0 kullanarak tooupload dosyaları hello aşağıdaki komutları kullanın:

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

Data Lake Analytics ayrıca Azure Blob depolama alanına da erişebilir.  Veri tooAzure Blob Depolama yüklemek için bkz: [kullanma hello Azure Storage ile Azure CLI](../storage/common/storage-azure-cli.md).

## <a name="submit-data-lake-analytics-jobs"></a>Data Lake Analytics işlerini gönderme
Hello Data Lake Analytics işleri, U-SQL dili hello yazılır. U-SQL hakkında daha fazla toolearn bkz [U-SQL dili ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md) ve [U-SQL dili eence](http://go.microsoft.com/fwlink/?LinkId=691348).

**toocreate bir Data Lake Analytics işi betiği**

Aşağıdaki U-SQL betiği ile bir metin dosyası oluşturun ve hello metin dosyası tooyour iş istasyonu kaydedin:

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

Bu U-SQL betiği hello kullanarak kaynak veri dosyasını okur **Extractors.Tsv()**ve ardından bir csv dosyası kullanarak oluşturan **Outputters.Csv()**.

Merhaba kaynak dosyayı farklı bir konuma kopyalayın sürece hello iki yolu değiştirmeyin.  Yoksa, data Lake Analytics hello çıkış klasörü oluşturur.

Daha basit toouse varsayılan Data Lake Store hesaplarında depolanan dosyalar için göreli yolların olur. Mutlak yol da kullanabilirsiniz.  Örneğin:

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

Mutlak yollar tooaccess dosyaları, bağlı Storage hesaplarındaki kullanmanız gerekir.  bağlı Azure Storage hesabında depolanan dosyalar için Hello sözdizimi aşağıdaki gibidir:

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> Genel bloblar ile Azure Blob kapsayıcısı desteklenmiyor.      
> Genel kapsayıcılar ile Azure Blob kapsayıcısı desteklenmiyor.      
>

**toosubmit işleri**

Sözdizimi toosubmit bir işi aşağıdaki hello kullanın.

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

Örneğin:

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

**toolist işler ve iş ayrıntıları göster**

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

**toocancel işleri**

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a>İş sonuçlarını alma

Bir işi tamamlandıktan sonra aşağıdaki komutları toolist hello çıktı dosyaları hello kullanın ve hello dosyalarını yükleyin:

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

Örneğin:

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a>İşlem hatları ve tekrarlar

**İşlem hatları ve tekrarlar hakkında bilgi edinin**

Kullanım hello `az dla job pipeline` toosee hello ardışık düzen bilgi işleri daha önce gönderilen komutları.

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

Kullanım hello `az dla job recurrence` daha önce gönderilen işlerinin toosee hello yinelenme bilgilerini komutları.

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a>Sonraki adımlar

* toosee hello Data Lake Analytics CLI 2.0 başvuru belgesini bkz [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).
* toosee hello Data Lake deposu CLI 2.0 başvuru belgesini bkz [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).
* toosee daha karmaşık bir sorgu görmek [Web sitesi günlüklerini çözümleme Azure Data Lake Analytics'i kullanarak](data-lake-analytics-analyze-weblogs.md).
