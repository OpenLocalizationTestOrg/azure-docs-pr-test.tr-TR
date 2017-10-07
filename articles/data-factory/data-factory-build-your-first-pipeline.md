---
title: "Veri Fabrikası Öğreticisi: ilk veri ardışık | Microsoft Docs"
description: "Bu Azure Data Factory öğretici nasıl Hadoop kümesinde toocreate ve zamanlama Hive kullanarak verileri işleyen bir veri fabrikası'komut dosyası gösterir."
services: data-factory
keywords: "Azure veri fabrikası Öğreticisi, hadoop kümesi, hadoop hive"
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.assetid: 81f36c76-6e78-4d93-a3f2-0317b413f1d0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: ed9c0ade4500d4ac1f7c2c2312c1fa675e0b1f02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-pipeline-tootransform-data-using-hadoop-cluster"></a>Öğretici: Hadoop kümesi kullanarak ilk ardışık düzen tootransform verilerinizi derleme
> [!div class="op_single_selector"]
> * [Genel bakış ve önkoşullar](data-factory-build-your-first-pipeline.md)
> * [Azure portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager Şablonu](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)

Bu öğreticide, veri ardışık ile ilk Azure data factory'nizi derleme. Merhaba ardışık düzen giriş verileri bir Azure Hdınsight (Hadoop) küme tooproduce çıktı verilerini Hive betiğini çalıştırarak dönüştürür.  

Bu makalede, genel bakış ve başlangıç öğreticisi için Önkoşullar sağlar. Merhaba önkoşulları tamamladıktan sonra yapabileceğiniz Araçlar/SDK'ları aşağıdaki hello birini kullanarak hello Öğreticisi: Azure portal, Visual Studio, PowerShell, Resource Manager şablonu, REST API. Merhaba seçeneklerden birini hello aşağı açılan listesinden hello başındaki (veya) bağlantıları hello bu seçeneklerden birini kullanarak bu makale toodo hello öğreticinin sonunda seçin.    

## <a name="tutorial-overview"></a>Öğreticiye genel bakış
Bu öğreticide, hello aşağıdaki adımları gerçekleştirin:

1. Oluşturma bir **veri fabrikası**. Veri Fabrikası taşıyın ve veri dönüştürme bir veya daha fazla veri ardışık düzen içerebilir. 

    Bu öğreticide hello data factory'de bir işlem hattı oluşturacaksınız. 
2. Oluşturma bir **ardışık düzen**. İşlem hattında bir veya daha fazla etkinlik bulunabilir (Örnek: Kopya Etkinliği, HDInsight Hive Etkinliği). Bu örnek hello Hdınsight Hadoop kümesinde bir Hive betiği çalıştıran Hdınsight Hive etkinliği kullanır. Merhaba betiği ilk başvuruları ham web günlüğü verileri Azure blob storage'da depolanan hello bir tablo oluşturur ve ardından bölümleri yıl ve ay tarafından ham verileri hello.

    Bu öğreticide, Azure Hdınsight Hadoop kümesinde bir Hive sorgusu çalıştırarak hello ardışık düzen hello Hive etkinliği tootransform verileri kullanır. 
3. Oluşturma **bağlantılı Hizmetleri**. Bağlantılı hizmet toolink bir veri deposu veya bir işlem hizmeti toohello veri fabrikası oluşturun. Bir veri deposu Azure depolama gibi hello ardışık düzeninde etkinlik girdi/çıktı verilerini tutar. Hdınsight Hadoop kümesi gibi işlem hizmeti işlemleri/veri dönüşümler.

    Bu öğreticide, iki bağlı hizmet oluşturacaksınız: **Azure Storage** ve **Azure Hdınsight**. Hello Azure depolama hizmeti bağlantıları hello girdi/çıktı verilerini toohello veri fabrikası tutan Azure Storage hesabını bağlı. Azure Hdınsight, hizmet bağlantıları kullanılan tootransform veri toohello veri fabrikası olan Azure Hdınsight kümesi bağlı. 
3. Girdi ve çıktı **veri kümeleri** oluşturun. Bir giriş veri kümesi hello giriş hello ardışık düzeninde bir etkinliğin temsil eder ve bir çıkış veri kümesi hello çıktı hello etkinliği temsil eder.

    Bu öğretici, hello giriş ve çıkış veri kümeleri giriş konumları belirtin ve çıktı verileri Azure Blob Storage hello. Hello Azure Storage bağlı hizmeti belirtir Azure depolama hesabı nedir kullanılır. Bir giriş veri kümesi burada hello giriş dosyaları bulunan bir çıkış veri kümesi hello çıktı dosyaları yerleştirildiği belirtir. 


Bkz: [giriş tooAzure Data Factory](data-factory-introduction.md) Azure Data Factory için ayrıntılı bir genel bakış makalesi.
  
Merhaba işte **diyagram görünümü** Bu öğreticide yapı hello örnek veri fabrikasının. **MyFirstPipeline** tüketir Hive türünde bir etkinlik sahip **Azureblobınput** veri kümesi oluşturur ve bir girdi olarak **AzureBlobOutput** olarak bir çıkış veri kümesi. 

![Data Factory öğreticisinde diyagram görünümü](media/data-factory-build-your-first-pipeline/data-factory-tutorial-diagram-view.png)


Bu öğreticide **inputdata** hello klasörünü **adfgetstarted** Azure blob kapsayıcısı input.log adlı bir dosya içerir. Bu günlük dosyası üç ay girişlerinden vardır: Ocak, Şubat ve Mart 2016. Merhaba girdi dosyasında her ay hello örnek satırları şunlardır. 

```
2016-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871 
2016-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2016-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

Hello dosyası Hdınsight Hive etkinliğiyle hello ardışık düzen tarafından işlendiğinde hello etkinlik bölümleri yıl ve ay tarafından veri girişi hello Hdınsight kümesinde bir Hive betiği çalıştırır. Hello komut dosyası, her ay girişlerinden sahip bir dosya içeren üç çıkış klasörler oluşturur.  

```
adfgetstarted/partitioneddata/year=2016/month=1/000000_0
adfgetstarted/partitioneddata/year=2016/month=2/000000_0
adfgetstarted/partitioneddata/year=2016/month=3/000000_0
```

Yukarıda gösterilen hello örnek satırlarından hello ilk (biriyle 2016-01-01) toohello 000000_0 hello ay içinde yazılırken = 1 klasör. Benzer şekilde, hello ikincisi toohello hello ay içinde yazılırken = 2 klasörü ve hello üçüncü bir toohello hello ay içinde yazılırken = 3 klasör.  

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce aşağıdaki önkoşullar hello sahip olmanız gerekir:

1. **Azure aboneliği**: Aboneliğiniz yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Merhaba bkz [ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/) makale üzerinde nasıl ücretsiz bir deneme hesabı alabilirsiniz.
2. **Azure depolama** – Bu öğreticide hello verileri depolamak için genel amaçlı standart Azure depolama hesabı kullanın. Genel amaçlı standart Azure depolama hesabınız yoksa, hello bkz [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) makalesi. Merhaba depolama hesabı oluşturduktan sonra hello Not **hesap adı** ve **erişim tuşu**. Bkz. [Depolama erişim tuşlarını görüntüleme, kopyalama ve yeniden oluşturma](../storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).
3. Karşıdan yükle ve hello Hive sorgusu dosyasını gözden geçirin (**HQL**) konumunda bulunan: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql](https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql). Bu sorgu giriş verisi tooproduce çıktı verilerini dönüştürür. 
4. Karşıdan yükle ve hello örnek giriş dosyasını gözden geçirin (**input.log**) konumunda bulunan: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log](https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log)
5. Adlı bir blob kapsayıcı oluşturun **adfgetstarted** Azure Blob Depolama. 
6. Karşıya yükleme **partitionweblogs.hql** toohello dosya **betik** hello klasöründe **adfgetstarted** kapsayıcı. Gibi araçlar kullanın [Microsoft Azure Storage Gezgini](http://storageexplorer.com/). 
7. Karşıya yükleme **input.log** toohello dosya **inputdata** hello klasöründe **adfgetstarted** kapsayıcı. 

Merhaba önkoşulları tamamladıktan sonra Araçlar/SDK'ları toodo hello öğreticiyi izleyerek hello birini seçin: 

- [Azure portal](data-factory-build-your-first-pipeline-using-editor.md)
- [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
- [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
- [Resource Manager Şablonu](data-factory-build-your-first-pipeline-using-arm.md)
- [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)

Azure portalı ve Visual Studio, veri fabrikaları oluşturmanın GUI yolunu sağlar. Ancak, veri fabrikaları oluşturmanın scripting programlama yolu PowerShell, Resource Manager şablonu ve REST API seçeneklerini sağlar.

> [!NOTE]
> Bu öğreticide Hello veri ardışık giriş verisi tooproduce çıktı verilerini dönüştürür. Bir kaynak veri deposu tooa hedef veri deposundan veri kopyalamaz. Nasıl bir öğretici için Azure Data Factory kullanarak toocopy verileri görmek [Öğreticisi: Blob Storage tooSQL veritabanı ' veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Merhaba çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir. Ayrıntılı bilgi için bkz. [Data Factory’de zamanlama ve yürütme](data-factory-scheduling-and-execution.md). 





  
