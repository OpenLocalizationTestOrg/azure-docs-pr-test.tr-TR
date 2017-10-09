---
title: "aaaCall REST uç HTTP + Swagger ile Azure Logic Apps bağlayıcı | Microsoft Docs"
description: "Swagger aracılığıyla logic apps Merhaba HTTP + Swagger bağlayıcı ile tooREST uç noktaları bağlayın"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: baaa57689ff41fcd052f9d86086e36619ddec46e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http--swagger-action"></a>Merhaba HTTP + Swagger eylem ile başlayın

İlk sınıf bağlayıcı tooany REST uç noktası aracılığıyla oluşturabileceğiniz bir [Swagger belgesinin](https://swagger.io) kullandığınızda Merhaba HTTP + Swagger eylem mantığı uygulama akışınızda. Logic apps toocall birinci sınıf bir mantıksal Uygulama Tasarımcısı deneyim herhangi bir REST uç nokta da genişletebilirsiniz.

toocreate logic apps, bağlayıcılar ile nasıl görürüm toolearn [yeni bir mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a>HTTP kullan + tetikleyicinin veya bir eylem olarak Swagger

Merhaba HTTP + Swagger tetikleyici ve eylem iş hello aynı hello [HTTP eylemi](connectors-native-http.md) ancak hello API yapısı ve hello çıkışlarından göstererek mantığı Uygulama Tasarımcısı'nda daha iyi bir deneyim sağlamak [Swagger meta verileri](https://swagger.io) . Tetikleyici olarak da hello HTTP + Swagger Bağlayıcısı'nı da kullanabilirsiniz. Tooimplement yoklama tetikleyicinin isterseniz, açıklanan hello yoklama desenler izleyen [özel API'leri toocall mantığı uygulamalardan diğer API'leri, hizmetleri ve sistemleri oluşturmak](../logic-apps/logic-apps-create-api-app.md#polling-triggers).

Daha fazla bilgi edinmek [mantığı uygulama tetikleyiciler ve Eylemler](connectors-overview.md).

Toouse nasıl hello HTTP + Swagger örneği İşte işlem olarak bir mantıksal uygulama bir iş akışında bir eylemi.

1. Select hello **yeni adım** düğmesi.
2. Seçin **Eylem Ekle**.
3. Merhaba eylem arama kutusuna yazın **swagger** toolist Merhaba HTTP + Swagger eylem.
   
    ![HTTP + Swagger seçin eylemi](./media/connectors-native-http-swagger/using-action-1.png)
4. Merhaba Swagger belgesinin URL'sini yazın:
   
   * CORS etkinleştirdiyseniz ve toowork hello mantığı Uygulama Tasarımcısı hello URL gelen bir HTTPS uç noktası olmalıdır.
   * Merhaba Swagger belgesinin bu gereksinimi karşılamıyorsa, kullanabileceğiniz [Azure Storage ile CORS'yi](#hosting-swagger-from-storage) toostore hello belge.
5. Tıklatın **sonraki** tooread ve işleme gelen hello Swagger belgesinin.
6. Merhaba HTTP çağrısı için gerekli olan parametreleri ekleyin.
   
    ![Tam HTTP eylemi](./media/connectors-native-http-swagger/using-action-2.png)
7. toosave ve mantıksal uygulamanızı yayımlamak için tıklayın **kaydetmek** tasarımcı araç.

### <a name="host-swagger-from-azure-storage"></a>Azure depolama biriminden konak Swagger
Tooreference değil barındırılan veya hello Tasarımcısı için hello güvenlik ve çıkış noktaları arası gereksinimlerini karşılamıyor Swagger belgesinin isteyebilirsiniz. tooresolve Bu sorun, Azure depolama alanına hello Swagger belgesinin depolar ve CORS tooreference hello belge etkinleştirin.  

Hello adımları toocreate şunlardır, yapılandırma ve Azure depolama alanına Swagger belgeleri depolar:

1. [Azure Blob storage ile Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md). tooperform Bu adım, izinleri ayarlama çok**genel erişim**.

2. CORS hello blob üzerindeki etkinleştirin. 

   tooautomatically bu ayarı yapılandırmak için kullanabileceğiniz [bu PowerShell Betiği](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).

3. Merhaba Swagger dosyası toohello blob karşıya yükleyin. 

   Bu adımı hello gerçekleştirebilirsiniz [Azure portal](https://portal.azure.com) veya gibi bir araçtan [Azure Storage Gezgini](http://storageexplorer.com/).

4. Azure Blob Depolama bir HTTPS bağlantısı toohello belgesinde başvuru. 

   Merhaba bağlantı bu biçimi kullanır:

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a>Teknik Ayrıntılar
Aşağıda verilmiştir hello ayrıntıları hello tetikleyiciler ve Eylemler için bu HTTP + Swagger bağlayıcısını destekler.

## <a name="http--swagger-triggers"></a>HTTP + Swagger Tetikleyicileri
Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır. [Tetikleyiciler hakkında daha fazla bilgi edinin.](connectors-overview.md) Merhaba HTTP + Swagger Bağlayıcısı bir tetikleyici vardır.

| Tetikleyici | Açıklama |
| --- | --- |
| HTTP + Swagger |Bir HTTP çağrısı yapmak ve hello yanıt içeriği döndürür |

## <a name="http--swagger-actions"></a>HTTP + Swagger Eylemler
Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir. [Eylemler hakkında daha fazla bilgi edinin.](connectors-overview.md) Merhaba HTTP + Swagger bağlayıcının bir olası eylem.

| Eylem | Açıklama |
| --- | --- |
| HTTP + Swagger |Bir HTTP çağrısı yapmak ve hello yanıt içeriği döndürür |

### <a name="action-details"></a>Eylem ayrıntıları
Merhaba HTTP + Swagger bağlayıcı olası bir eylem ile birlikte gelir. Aşağıda, her hello Eylemler, gerekli ve isteğe bağlı giriş alanları ve bunların kullanımıyla ilişkili çıkış ayrıntıları karşılık gelen hello hakkında bilgi verilmektedir.

#### <a name="http--swagger"></a>HTTP + Swagger
Giden HTTP isteğinden Swagger meta verileri Yardım olun.
Bir yıldız işareti (*) gerekli bir alan anlamına gelir.

| Görünen ad | Özellik adı | Açıklama |
| --- | --- | --- |
| Yöntemi * |Yöntemi |HTTP fiili toouse. |
| URI * |URI |Merhaba HTTP isteği için URI. |
| Üstbilgileri |Üstbilgileri |HTTP üstbilgileri tooinclude JSON nesnesinin. |
| Gövde |Gövde |Merhaba HTTP istek gövdesi. |
| Kimlik Doğrulaması |Kimlik doğrulaması |İstek için kimlik doğrulama toouse. Daha fazla bilgi için bkz: Merhaba [HTTP Bağlayıcısı](connectors-native-http.md#authentication). |

**Çıkış Ayrıntıları**

HTTP yanıtı

| Özellik adı | Veri türü | Açıklama |
| --- | --- | --- |
| Üstbilgileri |Nesne |Yanıt Üstbilgileri |
| Gövde |Nesne |Yanıt nesnesi |
| Durum kodu |Int |HTTP durum kodu |

### <a name="http-responses"></a>HTTP yanıtları
Çağrıları toovarious Eylemler yaparken, belirli yanıtları alabilirsiniz. Karşılık gelen yanıtları ve açıklamaları özetleyen tablosu aşağıdadır.

| Ad | Açıklama |
| --- | --- |
| 200 |TAMAM |
| 202 |Kabul edildi |
| 400 |Hatalı istek |
| 401 |Yetkilendirilmemiş |
| 403 |Yasak |
| 404 |Bulunamadı |
| 500 |İç sunucu hatası. Bilinmeyen bir hata oluştu. |

- - -
## <a name="next-steps"></a>Sonraki adımlar

* [Mantıksal uygulama oluşturun.](../logic-apps/logic-apps-create-a-logic-app.md)
* [Diğer bağlayıcıları Bul](apis-list.md)