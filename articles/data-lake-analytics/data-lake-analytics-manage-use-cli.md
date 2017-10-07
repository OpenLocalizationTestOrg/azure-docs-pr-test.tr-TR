---
title: "Azure komut satırı arabirimi kullanarak Azure Data Lake Analytics aaaManage | Microsoft Docs"
description: "Toomanage Data Lake Analytics hesaplarını, veri kaynakları, işlerin nasıl ve Azure CLI kullanarak kullanıcıların bilgi edinin"
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 0af1f89080739b39f6980989b7694734cc135715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a>Azure komut satırı arabirimi (CLI) kullanarak Azure Data Lake Analytics yönetme
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Azure CLI toomanage Azure Data Lake Analytics hesaplarını, veri kaynakları, kullanıcılar ve işleri kullanarak nasıl hello öğrenin. diğer araçları kullanarak toosee yönetimi konuları yukarıdaki hello sekme seçimine tıklayın.


**Önkoşullar**

Bu öğreticiye başlamadan önce hello şunlara sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/pricing/free-trial/).
* **Azure CLI**. Bkz. [Azure CLI'yı yükleme ve yapılandırma](../cli-install-nodejs.md).
  * Merhaba yükleyip **yayın öncesi** [Azure CLI araçlarını](https://github.com/MicrosoftBigData/AzureDataLake/releases) içinde bu demo toocomplete sipariş.
* **Kimlik doğrulama**kullanarak hello komutu:
  
        azure login
    Bir iş veya Okul hesabı kullanarak kimlik doğrulaması ile ilgili daha fazla bilgi için bkz: [tooan Azure aboneliği hello Azure CLI ' bağlanma](../xplat-cli-connect.md).
* **Anahtar toohello Azure Resource Manager moduna**kullanarak hello komutu:
  
        azure config mode arm

**Data Lake Store ve Data Lake Analytics toolist hello komutlar:**

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a>Hesapları yönetme
Herhangi bir Data Lake Analytics işi çalıştırmadan önce bir Data Lake Analytics hesabınızın olması gerekir. Azure Hdınsight, bir iş çalışmadığı zaman Analytics hesabı için ödemeniz gerekmez.  Yalnızca bir iş çalışırken hello zaman için ödeme yaparsınız.  Daha fazla bilgi için bkz: [Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md).  

### <a name="create-accounts"></a>Hesapları oluşturma
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a>Güncelleştirme hesapları
Merhaba aşağıdaki komutu güncelleştirmeleri varolan bir Data Lake Analytics hesabı hello özellikleri

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a>Hesapları listeleme
Liste Data Lake Analytics hesapları 

    azure datalake analytics account list

Belirli bir kaynak grubunun içinde listesi Data Lake Analytics hesapları

    azure datalake analytics account list -g "<Azure Resource Group Name>"

Belirli bir Data Lake Analytics hesabı ayrıntılarını alma

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a>Data Lake Analytics hesapları silme
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a>Hesabı veri kaynaklarını yönet
Data Lake Analytics şu anda aşağıdaki veri kaynaklar hello destekler:

* [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)
* [Azure Depolama](../storage/common/storage-introduction.md)

Analytics hesabı oluşturduğunuzda, bir Azure Data Lake Storage hesabı toobe hello varsayılan depolama hesabı atamanız gerekir. Merhaba varsayılan ADL depolama hesabı kullanılan toostore işi meta verileri ve iş denetim günlükleri. Analytics hesabı oluşturduktan sonra ek Data Lake Storage hesaplarını ve/veya Azure Storage hesabı ekleyebilirsiniz. 

### <a name="find-hello-default-adl-storage-account"></a>Merhaba varsayılan ADL depolama hesabı bulunamadı
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

Merhaba değer özellikler: datalakeStoreAccount:name altında listelenir.

### <a name="add-additional-azure-blob-storage-accounts"></a>Ek Azure Blob storage hesapları ekleme
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> Yalnızca Blob Depolama kısa adları desteklenir.  FQDN, örneğin "myblob.blob.core.windows.net" kullanmayın.
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a>Ek Data Lake Store hesapları ekleme
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

[-d] hello eklenmekte olan Data Lake hello varsayılan Data Lake hesabı olup bir isteğe bağlı bir anahtar tooindicate değil. 

### <a name="update-existing-data-source"></a>Güncelleştirme mevcut veri kaynağı
Mevcut bir Data Lake Store hesabı toobe hello varsayılan tooset:

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

tooupdate mevcut bir Blob Depolama hesabı anahtarı:

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a>Liste veri kaynakları:
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Data Lake Analytics veri kaynağı listesi](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a>Veri kaynaklarını silin:
bir Data Lake Store hesabı toodelete:

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

toodelete bir Blob Depolama hesabı:

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a>İşleri yönetme
Bir proje oluşturmadan önce bir Data Lake Analytics hesabı olması gerekir.  Daha fazla bilgi için bkz: [yönetmek Data Lake Analytics hesapları](#manage-accounts).

### <a name="list-jobs"></a>Liste işleri
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Data Lake Analytics veri kaynağı listesi](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a>İş ayrıntılarını almak
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a>İşlerini gönderme
> [!NOTE]
> bir işin Hello varsayılan öncelik 1000'dir ve hello varsayılan paralellik derecesi bir iş için 1'dir.
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a>İşlerini iptal edin
Merhaba listesi komutu toofind hello iş kimliği kullanın ve daha sonra iptal toocancel hello işlemini kullanın.

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a>Katalog Yönetimi
U-SQL komut dosyaları tarafından paylaşılabilmesi hello U-SQL kullanılan toostructure veri ve kod kataloğudur. başlangıç kataloğu hello Azure Data Lake verilerle olası en yüksek performansı sağlar. Daha fazla bilgi için bkz. [U-SQL kataloğunu kullanma](data-lake-analytics-use-u-sql-catalog.md).

### <a name="list-catalog-items"></a>Liste katalog öğeleri
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

Veritabanı, şema, derleme, dış veri kaynağı, tablo, tablo değerli fonksiyon veya tablo istatistikleri Hello türleri içerir.

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a>ARM grupları kullanma
Uygulamalar genellikle web uygulaması, veritabanı, veritabanı sunucusu, depolama alanı ve 3. taraf hizmetleri gibi birçok bileşenden oluşur. Azure Resource Manager (ARM), bir grup, başvurulan tooas Azure kaynak grubu olarak hello kaynaklarla toowork sağlar. Dağıtma, güncelleştirme, izlemek veya hello kaynakların tümünü tek ve eşgüdümlü bir işlemle uygulamanızda için silin. Dağıtım için bir şablon kullanabilirsiniz. Üstelik bu şablon test, hazırlık ve üretim gibi farklı ortamlarda da çalışabilir. Merhaba hello tüm grup için aktarılmış maliyetleri görüntüleyerek kuruluşunuzun fatura açıklık getirebilir. Daha fazla bilgi için bkz. [Azure Resource Manager'a Genel Bakış](../azure-resource-manager/resource-group-overview.md). 

Bir Data Lake Analytics hizmeti aşağıdaki bileşenleri hello içerebilir:

* Azure Data Lake Analytics hesabı
* Gerekli varsayılan Azure Data Lake Storage hesabı
* Ek Azure Data Lake Storage hesapları
* Ek Azure depolama hesapları

Tüm bu bileşenlerin bir ARM Grup toomake altında oluşturabilirsiniz onları daha kolay toomanage.

![Azure Data Lake Analytics hesabı ve depolama](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

Bir Data Lake Analytics hesabı ve hello bağımlı depolama hesapları hello aynı yerleştirilmelidir Azure veri merkezi.
Merhaba ARM Grup ancak farklı veri merkezinde yer alabilir.  

## <a name="see-also"></a>Ayrıca bkz.
* [Microsoft Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md)
* [Azure Portal'ı kullanarak Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-portal.md)
* [Azure Data Lake Analytics'i Azure Portal'ı kullanarak yönetme](data-lake-analytics-manage-use-portal.md)
* [Azure Portal'ı kullanarak Azure Data Lake Analytics işlerini izleme ve sorun giderme](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

