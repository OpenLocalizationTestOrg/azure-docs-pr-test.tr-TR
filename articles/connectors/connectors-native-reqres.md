---
title: "aaaUse istek ve yanıt eylemleri | Microsoft Docs"
description: "Merhaba istek ve yanıt tetikleyici ve bir Azure mantıksal uygulama eylemde genel bakış"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 566924a4-0988-4d86-9ecd-ad22507858c0
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: 24c378cc12d5f3f65116d5e59278236186a99662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-request-and-response-components"></a>Merhaba istek ve yanıt bileşenleriyle çalışmaya başlayın
Merhaba istek ve yanıt bileşenlerinde ile bir mantıksal uygulama, gerçek zamanlı tooevents yanıt verebilir.

Örneğin, şunları yapabilirsiniz:

* Bir mantıksal uygulama yoluyla şirket içi veritabanından verilerle tooan HTTP isteğine yanıt.
* Bir mantıksal uygulama bir dış Web kancası olaydan tetikler.
* İstek ve yanıt eylemi başka bir mantıksal uygulama içinde ile bir mantıksal uygulama çağırın.

bir mantıksal uygulama Hello istek ve yanıt eylemleri kullanmaya tooget bkz [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-http-request-trigger"></a>Merhaba HTTP isteği tetikleyici kullanın
Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır. [Tetikleyiciler hakkında daha fazla bilgi](connectors-overview.md).

Burada, örnek dizisi nasıl tooset oluşturan bir HTTP isteği hello mantığı Uygulama Tasarımcısı verilmiştir.

1. Merhaba tetikleyici eklemek **isteği - olduğunda bir HTTP isteği alındığında** mantığı uygulamanıza. İsteğe bağlı olarak bir JSON şeması sağlayın (gibi bir araç kullanarak [JSONSchema.net](http://jsonschema.net)) hello istek gövdesi için. Bu özellikler için hello Tasarımcı toogenerate belirteçleri hello HTTP istek sağlar.
2. Başka bir eylem ekleyebilirsiniz, böylece hello mantıksal uygulama kaydedebilirsiniz.
3. Merhaba mantıksal uygulama kaydedildikten sonra hello isteği kartından hello HTTP istek URL'si elde edebilirsiniz.
4. Bir HTTP POST (gibi bir araç kullanabilirsiniz [Postman](https://www.getpostman.com/)) toohello URL Tetikleyicileri hello mantıksal uygulama.

> [!NOTE]
> Bir yanıt eylemi tanımlarsanız olmayan bir `202 ACCEPTED` yanıt toohello çağıran hemen döndürülür. Merhaba yanıt eylem toocustomize yanıt kullanabilirsiniz.
> 
> 

![Yanıt tetikleyici](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-hello-http-response-action"></a>Merhaba HTTP yanıtının eylem kullanın
Merhaba HTTP yanıtının eylem, yalnızca bir HTTP isteğiyle tetiklenen bir iş akışında kullanıldığında geçerlidir. Bir yanıt eylemi tanımlarsanız olmayan bir `202 ACCEPTED` yanıt toohello çağıran hemen döndürülür.  Merhaba iş akışı içindeki tüm adımda bir yanıt eylemi ekleyebilirsiniz. Merhaba mantıksal uygulama yalnızca hello gelen istek açık bir yanıt için bir dakika için tutar.  Bir yanıt hello akışından gönderilen (ve bir yanıt eylemi hello tanımında varsa) dakika sonra bir `504 GATEWAY TIMEOUT` toohello arayan döndürülür.

İşte nasıl tooadd bir HTTP yanıtının eylem:

1. Select hello **yeni adım** düğmesi.
2. Seçin **Eylem Ekle**.
3. Merhaba eylem arama kutusuna yazın **yanıt** toolist hello yanıt eylem.
   
    ![Merhaba yanıt eylemi seçin](./media/connectors-native-reqres/using-action-1.png)
4. Merhaba HTTP yanıt iletisi için gerekli olan parametreleri ekleyin.
   
    ![Tam hello yanıt eylemi](./media/connectors-native-reqres/using-action-2.png)
5. Merhaba sol üst köşesindeki hello araç toosave ve, logic app kazandırır hem'ı tıklatın ve yayımlama (etkinleştirin).

## <a name="request-trigger"></a>Tetikleyici isteği
Burada, bu bağlayıcıyı destekler hello tetikleyici hello ayrıntılarını bulunmaktadır. Bir tek istek tetikleyici yoktur.

| Tetikleyici | Açıklama |
| --- | --- |
| İstek |Bir HTTP isteği alındığında gerçekleşir |

## <a name="response-action"></a>Yanıt eylemi
Aşağıda, bu bağlayıcıyı destekler hello eylemin hello Ayrıntılar verilmiştir. Bir istek tetikleyicisini eşlik yükleyen yalnızca kullanılabilir tek yanıt eylemi yok.

| Eylem | Açıklama |
| --- | --- |
| Yanıt |HTTP isteğinin yanıtı toohello bağıntılı döndürür |

### <a name="trigger-and-action-details"></a>Tetikleyici ve eylem ayrıntıları
Merhaba aşağıdaki tablolarda hello tetikleyici ve eylem için girdi alanlarının hello açıklar ve karşılık gelen çıkış ayrıntıları hello.

#### <a name="request-trigger"></a>Tetikleyici isteği
Merhaba, bir gelen HTTP istek hello tetikleyici için giriş alanını aşağıdadır.

| Görünen ad | Özellik adı | Açıklama |
| --- | --- | --- |
| JSON şeması |Şema |Merhaba HTTP isteği gövdesinin Hello JSON şeması |

<br>

**Çıkış Ayrıntıları**

Merhaba, hello istek için çıkış ayrıntıları verilmiştir.

| Özellik adı | Veri türü | Açıklama |
| --- | --- | --- |
| Üstbilgileri |Nesne |İstek üstbilgileri |
| Gövde |Nesne |İstek nesnesi |

#### <a name="response-action"></a>Yanıt eylemi
Merhaba, hello HTTP yanıtının eylem için girdi alanlarının verilmiştir. A * gerekli bir alan olduğu anlamına gelir.

| Görünen ad | Özellik adı | Açıklama |
| --- | --- | --- |
| Durum kodu * |statusCode |Merhaba HTTP durum kodu |
| Üstbilgileri |Üstbilgileri |Tüm yanıt üstbilgileri tooinclude JSON nesnesinin |
| Gövde |Gövde |Merhaba yanıt gövdesi |

## <a name="next-steps"></a>Sonraki adımlar
Şimdi, hello platform deneyin ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md). Keşfedebilirsiniz bakarak logic apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).

