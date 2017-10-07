---
title: "Azure mantıksal uygulamaları için aaaWebhook Bağlayıcısı | Microsoft Docs"
description: "Nasıl toouse Web kancası eylemleri ve Tetikleyicileri tooperform Eylemler mantığı uygulamalardan filtre dizisi gibi"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 71775384-6c3a-482c-a484-6624cbe4fcc7
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: b2dee12750f3f20f10e7b257da05a79f28f90f43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-webhook-connector"></a>Merhaba Web kancası Bağlayıcısı ile çalışmaya başlama

Merhaba Web kancası eylem ve tetikleyici ile başlatmak, duraklatmak ve bu görevleri akışları tooperform Sürdür:

* Gelen tetikleyen bir [Azure olay hub'ı](https://github.com/logicappsio/EventHubAPI) öğeyi alındığında
* Bir iş akışı devam etmeden önce bir onay beklemek

Daha fazla bilgi edinmek [nasıl toocreate bir Web kancası destekleyen özel API'leri](../logic-apps/logic-apps-create-api-app.md).

## <a name="use-hello-webhook-trigger"></a>Merhaba Web kancası tetikleyici kullanın

A [ *tetikleyici* ](connectors-overview.md) mantığı uygulama akışı başlar bir olaydır. Bir Web kancası tetikleyici olay tabanlı ve yeni öğeler için yoklama kullanmaz. Hello gibi [isteği tetikleyici](connectors-native-reqres.md), hello mantıksal uygulama hello bir olay gerçekleştiğinde anlık ateşlenir. Merhaba Web kancası tetikleyici kaydeder bir *geri çağırma URL'si* tooa hizmet ve kullanır, URL toofire hello mantıksal uygulama olarak gereklidir.

Burada, nasıl bir HTTP yukarı tooset tetiklemek hello mantığı Uygulama Tasarımcısı gösteren bir örnek verilmiştir. Merhaba adımları zaten dağıttıysanız veya hello izleyen bir API erişme varsayın [Web kancası abone olma ve logic apps desende aboneliği](../logic-apps/logic-apps-create-api-app.md#webhook-triggers). Merhaba abone çağrısı her bir mantıksal uygulama sahip yeni bir Web kancası kaydedildi veya devre dışı tooenabled geçiş yapılır. Merhaba aboneliği çağrısı logic app Web kancası tetikleyici kaldırıldı ve kaydedildiğinde veya etkin toodisabled geçiş yapılır.

**tooadd hello Web kancası tetikleyici**

1. Merhaba eklemek **HTTP Web kancası** tetikleyici hello bir mantıksal uygulama ilk adımı olarak.
2. Merhaba Web kancası abone olma ve çağrıları aboneliği için hello parametrelerinde doldurun.

   Bu adım aynı desen hello hello izleyen [HTTP eylemi](connectors-native-http.md) biçimi.

     ![HTTP tetikleyici](./media/connectors-native-webhook/using-trigger.png)

3. En az bir eylem ekleyin.
4. Tıklatın **kaydetmek** toopublish hello mantıksal uygulama. Bu adım çağrıları hello hello geri çağırma URL'si gerekli tootrigger noktayla bu mantıksal uygulama abone olun.
5. Her değiştiğinde, hizmet yapar hello bir `HTTP POST` toohello geri çağırma URL'si, hello mantığı uygulama etkinleşir ve hello isteği geçirilen tüm verileri içerir.

## <a name="use-hello-webhook-action"></a>Merhaba Web kancası eylemini kullanın

Bir [ *eylem* ](connectors-overview.md) bir işlem bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilir. Bir Web kancası eylemi kaydeder bir *geri çağırma URL'si* bir hizmet ve devam etmeden önce hello URL çağrılıncaya kadar bekler. Merhaba ["Onay e-posta Gönder"](connectors-create-api-office365-outlook.md) bu deseni izler bir bağlayıcı örneğidir. Bu desen hello Web kancası eylem aracılığıyla herhangi bir hizmeti içine genişletebilirsiniz. 

Aşağıda, bir Web kancası Eylemler tooset hello mantığı Uygulama Tasarımcısı nasıl oluşturulduğunu gösteren bir örnek verilmiştir. Zaten dağıttıysanız veya hello izleyen bir API'sine erişim bu adımları varsayın [Web kancası abone olma ve logic apps içinde kullanılan Düzen aboneliği](../logic-apps/logic-apps-create-api-app.md#webhook-actions). Merhaba abone çağrısı bir mantıksal uygulama hello Web kancası eylem yürüttüğünde yapılır. Merhaba aboneliği çağrısı için bir yanıt beklenirken bir çalıştırma iptal ya da uygulama hello mantığı önce zaman aşımına uğruyor yapılır.

**tooadd bir Web kancası eylemi**

1. Seçin **yeni adım** > **Eylem Ekle**.

2. "Web kancası" toofind hello Hello arama kutusuna yazın **HTTP Web kancası** eylem.

    ![Sorgu eylemi seçin](./media/connectors-native-webhook/using-action-1.png)

3. Merhaba Web kancası abone olma ve çağrıları aboneliği için hello parametrelerinde doldurun

   Bu adım aynı desen hello hello izleyen [HTTP eylemi](connectors-native-http.md) biçimi.

     ![Tam bir sorgu eylemi](./media/connectors-native-webhook/using-action-2.png)
   
   Çalışma zamanında hello mantığı uygulama çağrıları hello abone uç noktası bu adımı eriştikten sonra.

4. Tıklatın **kaydetmek** toopublish hello mantıksal uygulama.

## <a name="technical-details"></a>Teknik Ayrıntılar

Daha fazla ayrıntı aşağıdadır hello tetikleyiciler ve eylemler hakkında Web kancası destekler.

## <a name="webhook-triggers"></a>Web kancası Tetikleyicileri

| Eylem | Açıklama |
| --- | --- |
| HTTP Web kancası |Gerektiği şekilde hello URL toofire mantıksal uygulama çağırabilirsiniz bir geri çağırma URL'si tooa hizmeti abone olun. |

### <a name="trigger-details"></a>Tetikleyici ayrıntıları

#### <a name="http-webhook"></a>HTTP Web kancası

Gerektiği şekilde hello URL toofire mantıksal uygulama çağırabilirsiniz bir geri çağırma URL'si tooa hizmeti abone olun.
Bir * gerekli alan anlamına gelir.

| Görünen ad | Özellik adı | Açıklama |
| --- | --- | --- |
| Abone yöntemi * |Yöntemi |Abone ol isteği için HTTP yöntemini toouse |
| Abone URI * |URI |Abone ol isteği için HTTP URI toouse |
| Aboneliği yöntemi * |Yöntemi |HTTP yöntemi toouse aboneliği kaldırma isteği |
| Aboneliği URI * |URI |Aboneliği kaldırma isteği için HTTP URI toouse |
| Gövde abone olma |Gövde |Abonelik için HTTP istek gövdesi |
| Üstbilgiler abone olma |Üstbilgileri |Abonelik için HTTP isteği üstbilgileri |
| Kimlik doğrulama abone olma |Kimlik doğrulaması |HTTP kimlik doğrulaması toouse abone için. [HTTP Bağlayıcısı bakın](connectors-native-http.md#authentication) Ayrıntılar için |
| Gövde aboneliği |Gövde |HTTP isteği gövdesinin abonelikten için |
| Üstbilgiler aboneliği |Üstbilgileri |HTTP istek üstbilgilerinin abonelikten için |
| Kimlik doğrulama aboneliği |Kimlik doğrulaması |HTTP kimlik doğrulaması toouse abonelikten için. [HTTP Bağlayıcısı bakın](connectors-native-http.md#authentication) Ayrıntılar için |

**Çıkış Ayrıntıları**

Web kancası isteği

| Özellik adı | Veri türü | Açıklama |
| --- | --- | --- |
| Üstbilgileri |Nesne |Web kancası istek üstbilgileri |
| Gövde |Nesne |Web kancası istek nesnesi |
| Durum kodu |Int |Web kancası isteği durum kodu |

## <a name="webhook-actions"></a>Web kancası eylemleri

| Eylem | Açıklama |
| --- | --- |
| HTTP Web kancası |Merhaba URL tooresume gerektiği gibi bir iş akışı adımı çağırabilirsiniz bir geri çağırma URL'si tooa hizmeti abone olun. |

### <a name="action-details"></a>Eylem ayrıntıları

#### <a name="http-webhook"></a>HTTP Web kancası

Merhaba URL tooresume gerektiği gibi bir iş akışı adımı çağırabilirsiniz bir geri çağırma URL'si tooa hizmeti abone olun.
Bir * gerekli alan anlamına gelir.

| Görünen ad | Özellik adı | Açıklama |
| --- | --- | --- |
| Abone yöntemi * |Yöntemi |Abone ol isteği için HTTP yöntemini toouse |
| Abone URI * |URI |Abone ol isteği için HTTP URI toouse |
| Aboneliği yöntemi * |Yöntemi |HTTP yöntemi toouse aboneliği kaldırma isteği |
| Aboneliği URI * |URI |Aboneliği kaldırma isteği için HTTP URI toouse |
| Gövde abone olma |Gövde |Abonelik için HTTP istek gövdesi |
| Üstbilgiler abone olma |Üstbilgileri |Abonelik için HTTP isteği üstbilgileri |
| Kimlik doğrulama abone olma |Kimlik doğrulaması |HTTP kimlik doğrulaması toouse abone için. [HTTP Bağlayıcısı bakın](connectors-native-http.md#authentication) Ayrıntılar için |
| Gövde aboneliği |Gövde |HTTP isteği gövdesinin abonelikten için |
| Üstbilgiler aboneliği |Üstbilgileri |HTTP istek üstbilgilerinin abonelikten için |
| Kimlik doğrulama aboneliği |Kimlik doğrulaması |HTTP kimlik doğrulaması toouse abonelikten için. [HTTP Bağlayıcısı bakın](connectors-native-http.md#authentication) Ayrıntılar için |

**Çıkış Ayrıntıları**

Web kancası isteği

| Özellik adı | Veri türü | Açıklama |
| --- | --- | --- |
| Üstbilgileri |Nesne |Web kancası istek üstbilgileri |
| Gövde |Nesne |Web kancası istek nesnesi |
| Durum kodu |Int |Web kancası isteği durum kodu |

## <a name="next-steps"></a>Sonraki adımlar

* [Mantıksal uygulama oluşturun.](../logic-apps/logic-apps-create-a-logic-app.md)
* [Diğer bağlayıcıları Bul](apis-list.md)