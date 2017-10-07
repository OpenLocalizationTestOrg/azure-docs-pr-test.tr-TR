---
title: "Azure Data Lake Store için tanılama günlüklerini aaaViewing | Microsoft Docs"
description: "Anlamak nasıl toosetup ve erişim Azure Data Lake Store için tanılama günlükleri "
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 11fbf7f517f97abdcaf809c1ebeeb51424ab2c1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a>Azure Data Lake Store için tanılama günlüklerine erişme
Hesabınız için nasıl tooenable tanılama günlük Data Lake Store hesabınızı ve nasıl tooview hello günlükleri için toplanan hakkında bilgi edinin.

Kuruluşlar hello verileri, hello verileri ne sıklıkta erişildiğine, ne kadar veri erişen kullanıcılar listesi gibi bilgiler sağlayan hesap toocollect veri erişimi denetim izleri hello depolanan kendi Azure Data Lake Store için tanılama günlük kaydını etkinleştirebilirsiniz Hesap, vs.

## <a name="prerequisites"></a>Ön koşullar
* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).
* **Azure Data Lake Store hesabı**. Merhaba yönergeleri izleyin [Azure Data Lake hello Azure Portal kullanarak Store ile çalışmaya başlama](data-lake-store-get-started-portal.md).

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a>Data Lake Store hesabınız için tanılama günlük kaydını etkinleştir
1. Yeni toohello oturum [Azure Portal](https://portal.azure.com).
2. Data Lake Store hesabınızı açın ve Data Lake Store hesabı dikey penceresinden tıklayın **ayarları**ve ardından **tanılama günlükleri**.
3. Merhaba, **tanılama günlükleri** dikey penceresinde tıklatın **tanılamayı açın**.

    ![Tanılama günlük kaydını etkinleştir](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "tanılama günlüklerini etkinleştirme")

3. Merhaba, **tanılama** dikey penceresinde hello değişiklikleri tooconfigure tanılama günlük kaydını aşağıdaki olun.
   
    ![Tanılama günlük kaydını etkinleştir](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "tanılama günlüklerini etkinleştirme")
   
   * Ayarlama **durum** çok**üzerinde** tooenable tanılama günlük.
   * Farklı şekillerde toostore/işlem hello veri seçebilirsiniz.
     
        * Çok olarak Hello seçeneğini**arşiv tooa depolama hesabı** toostore tooan Azure depolama hesabı günlüğe kaydeder. Daha sonraki bir tarihte toplu işlenen tooarchive hello veri istiyorsanız bu seçeneği kullanın. Bu seçeneği belirlerseniz toosave hello günlükleri için bir Azure Storage hesabı sağlamanız gerekir.
        
        * Çok olarak Hello seçeneğini**tooan event hub'ı akış** toostream günlük veri tooan Azure olay hub'ı. Büyük olasılıkla bir aşağı akış işleme varsa bu seçeneği kullanacağı gerçek zamanlı tooanalyze gelen günlüklerine kanalı. Bu seçeneği belirlerseniz, hello Azure Event Hub'ın toouse istediğiniz hello ayrıntılarını sağlamanız gerekir.

        * Çok olarak Hello seçeneğini**tooLog Analytics Gönder** toouse hello Azure günlük analizi hizmeti tooanalyze oluşturulan hello günlük verileri. Bu seçeneği seçerseniz, kullanım hello Günlük çözümlemesi gerçekleştireceği hello hello Operations Management Suite çalışma alanı için ayrıntıları sağlamanız gerekir.
     
   * Tooget denetim günlüklerini veya istek günlüklerini ya da hem isteyip istemediğinizi belirtin.
   * Merhaba hello veri korunması gereken gün sayısını belirtin. Bekletme, yalnızca Azure depolama hesabı tooarchive günlük verileri kullanıyorsanız geçerlidir.
   * **Kaydet** düğmesine tıklayın.

Tanılama ayarları etkinleştirildiğinde, hello günlüklerini hello izleyebilirsiniz **tanılama günlüklerini** sekmesi.

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a>Data Lake Store hesabınız için tanılama günlüklerini görüntüle
Data Lake Store hesabınız için tooview hello günlük verileri iki yolu vardır.

* Merhaba Data Lake Store hesabından ayarlarını görüntüleme
* Merhaba verilerinin depolandığı hello Azure depolama hesabından

### <a name="using-hello-data-lake-store-settings-view"></a>Hello kullanarak Data Lake deposu ayarları görüntüleyin
1. Data Lake Store hesabınızdaki **ayarları** dikey penceresinde tıklatın **tanılama günlükleri**.
   
    ![Görünüm tanılama günlük](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "tanılama günlükleri görüntüleme") 
2. Merhaba, **tanılama günlükleri** dikey penceresinde hello günlükleri tarafından kategorilere görmelisiniz **denetim günlüklerini** ve **isteği günlükleri**.
   
   * İstek günlüklerini hello Data Lake Store hesabı üzerinde yapılan her API isteği yakalayın.
   * Denetim günlüklerini benzer toorequest günlüklerin ancak hello Data Lake Store hesabında gerçekleştirilen hello işlemler çok daha ayrıntılı bir dökümünü sağlar. Örneğin, bir istek günlüklerini tek karşıya yükleme API çağrısında hello denetim günlüklerini "Ekle" işlemlerinde neden olabilir.
3. Merhaba tıklatın **karşıdan** her karşı bağlantı günlüğü girişi toodownload hello günlükleri.

### <a name="from-hello-azure-storage-account-that-contains-log-data"></a>Azure depolama hesabı Hello günlük verilerini içeren
1. Hello Azure depolama hesabı için günlük kaydını Data Lake Store ile ilişkili dikey penceresini açın ve Bloblar'a tıklayın. Merhaba **Blob hizmeti** iki kapsayıcı dikey penceresinde listelenir.
   
    ![Görünüm tanılama günlük](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "tanılama günlükleri görüntüleme")
   
   * Merhaba kapsayıcı **Öngörüler günlükleri denetim** hello denetim günlüklerini içerir.
   * Merhaba kapsayıcı **Öngörüler günlükleri istekleri** hello isteği günlükleri içerir.
2. Bu kapsayıcılara hello günlükleri yapı izlenerek hello altında depolanır.
   
    ![Görünüm tanılama günlük](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "tanılama günlükleri görüntüleme")
   
    Örnek olarak, hello tam yolunu tooan denetim günlüğü olabilir`https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`
   
    Merhaba tam yolunu tooa istek günlüğü similary, olabilir`https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`

## <a name="understand-hello-structure-of-hello-log-data"></a>Merhaba günlük verilerini Hello yapısını anlama
Denetim hello ve günlüklerin bir JSON biçiminde isteyin. Bu bölümde, istek için JSON hello yapısı bakın ve Denetim günlükleri.

### <a name="request-logs"></a>İstek günlükleri
Merhaba JSON biçimli istek günlüğünde örnek girişi İşte. Her bir blob olarak adlandırılan bir kök nesnesi vardır **kayıtları** günlük nesnelerinin bir dizisi içerir.

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a>İstek günlüğü şeması
| Ad | Tür | Açıklama |
| --- | --- | --- |
| time |Dize |Merhaba günlüğünün Hello zaman damgası (UTC) cinsinden |
| resourceId |Dize |Merhaba işlemi sürdü hello kaynak Kimliğini yerleştirin |
| category |Dize |Merhaba günlük kategorisi. Örneğin, **istekleri**. |
| operationName |Dize |Oturum hello işlemin adı. Örneğin, getfilestatus. |
| resultType |Dize |Merhaba işlemi, örneğin, 200 Hello durumu. |
| callerIpAddress |Dize |Merhaba istekte hello istemcinin Hello IP adresi |
| correlationId |Dize |toogroup bir dizi ilgili günlük girişlerini birlikte kullanılabilecek hello günlük Hello kimliği |
| identity |Nesne |Merhaba günlük oluşturulan hello kimliği |
| properties |JSON |Ayrıntılar için aşağıya bakın |

#### <a name="request-log-properties-schema"></a>İstek günlüğü özellikleri şeması
| Ad | Tür | Açıklama |
| --- | --- | --- |
| HttpMethod |Dize |Merhaba HTTP hello işlemi için kullanılan yöntem. Örneğin, alın. |
| Yol |Dize |Merhaba yolu hello işlem üzerinde gerçekleştirildi |
| RequestContentLength |Int |Merhaba HTTP isteğinin Hello içerik uzunluğu |
| ClientRequestId |Dize |Merhaba bu istek benzersiz olarak tanıtan kimliği |
| StartTime |Dize |hangi hello alınan sunucu hello isteği Hello zaman |
| EndTime |Dize |Merhaba zaman hangi hello sunucu bir yanıt gönderdi. |

### <a name="audit-logs"></a>Denetim günlükleri
Merhaba JSON biçimli Denetim günlüğüne örnek girişi İşte. Her bir blob olarak adlandırılan bir kök nesnesi vardır **kayıtları** günlük nesnelerinin bir dizisi içerir

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a>Denetim günlüğü şeması
| Ad | Tür | Açıklama |
| --- | --- | --- |
| time |Dize |Merhaba günlüğünün Hello zaman damgası (UTC) cinsinden |
| resourceId |Dize |Merhaba işlemi sürdü hello kaynak Kimliğini yerleştirin |
| category |Dize |Merhaba günlük kategorisi. Örneğin, **denetim**. |
| operationName |Dize |Oturum hello işlemin adı. Örneğin, getfilestatus. |
| resultType |Dize |Merhaba işlemi, örneğin, 200 Hello durumu. |
| correlationId |Dize |toogroup bir dizi ilgili günlük girişlerini birlikte kullanılabilecek hello günlük Hello kimliği |
| identity |Nesne |Merhaba günlük oluşturulan hello kimliği |
| properties |JSON |Ayrıntılar için aşağıya bakın |

#### <a name="audit-log-properties-schema"></a>Denetim günlüğü özellikleri şeması
| Ad | Tür | Açıklama |
| --- | --- | --- |
| StreamName |Dize |Merhaba yolu hello işlem üzerinde gerçekleştirildi |

## <a name="samples-tooprocess-hello-log-data"></a>Örnekleri tooprocess hello günlük verileri
Azure Data Lake Store hakkında bir örnek sağlar tooprocess ve hello günlük verilerini çözümleyin. Merhaba örneğini şurada bulabilirsiniz [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample). 

## <a name="see-also"></a>Ayrıca bkz.
* [Azure Data Lake Store'a Genel Bakış](data-lake-store-overview.md)
* [Data Lake Store'da verilerin güvenliğini sağlama](data-lake-store-secure-data.md)

