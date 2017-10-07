---
title: "HTTP - Azure Logic Apps üzerinden herhangi bir uç nokta ile aaaCommunicate | Microsoft Docs"
description: "İletişim kurabilir logic apps ile herhangi bir uç nokta HTTP üzerinden oluşturun."
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: 9793601839437a2b880bdb81e15881270cacc963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http-action"></a>HTTP eylemi Hello ile çalışmaya başlama

Merhaba HTTP eylemi, kuruluşunuz için iş akışları genişletmek ve tooany uç noktası, HTTP iletişim kurar.

Şunları yapabilirsiniz:

* Yönettiğiniz bir Web sitesi azaldığında (tetikleyici) etkinleştirme uygulama iş akışları mantığı oluşturun.
* Tooany uç nokta, iş akışlarınızı diğer Hizmetleri içine HTTP tooextend iletişim kurar.

bir mantıksal uygulama Hello HTTP eylem kullanmaya tooget bkz [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-http-trigger"></a>Merhaba HTTP tetikleyicisi kullanın
Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır. [Tetikleyiciler hakkında daha fazla bilgi](connectors-overview.md).

Burada, nasıl tooset hello HTTP yukarı tetiklemek hello mantığı Uygulama Tasarımcısı bir örnek sırası verilmiştir.

1. Merhaba HTTP tetikleyicisini mantıksal uygulamanızı ekleyin.
2. Toopoll istediğiniz hello HTTP uç noktası için hello parametrelerini doldurun.
3. Ne sıklıkta yoklanacağını üzerinde hello yinelenme aralığını değiştirin.

   Merhaba mantıksal uygulama artık her denetimi sırasında döndürülen herhangi bir içerik ile ateşlenir.

   ![HTTP tetikleyicisi](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a>Merhaba HTTP tetikleyicisini nasıl çalışır?

Merhaba HTTP tetikleyicisini çağrısı tooHTTP uç yinelenen bir aralıkta gönderir. Varsayılan olarak, 300'den düşük olduğu herhangi bir HTTP yanıt kodu mantığı uygulama toorun neden olur. toospecify hello mantıksal uygulama yangın olup olmadığını hello mantıksal uygulama kod görünümünde düzenleyin ve sonra hello HTTP çağrısıyla değerlendiren bir koşul ekleyin. Merhaba çok eşit veya daha fazla durum kodu döndürdüğünde tetiklenen bir HTTP tetikleyicisi bir örneği burada verilmiştir`400`.

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

Merhaba HTTP trigger parametreleri ilgili tam ayrıntılar bulunur [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).

## <a name="use-hello-http-action"></a>Merhaba HTTP eylemi kullanın

Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir. 
[Eylemler hakkında daha fazla bilgi](connectors-overview.md).

1. Seçin **yeni adım** > **Eylem Ekle**.
3. Merhaba eylem arama kutusuna yazın **http** toolist hello HTTP eylemler.
   
    ![Merhaba HTTP eylemi seçin](./media/connectors-native-http/using-action-1.png)

4. Merhaba HTTP çağrısı için gerekli parametreleri ekleyin.
   
    ![Tam hello HTTP eylemi](./media/connectors-native-http/using-action-2.png)

5. Merhaba designer araç çubuğundan, **kaydetmek**. Mantıksal uygulamanızı kaydedilir ve hello (etkin) yayımlanan aynı anda.

## <a name="http-trigger"></a>HTTP tetikleyicisi
Burada, bu bağlayıcıyı destekler hello tetikleyici hello ayrıntılarını bulunmaktadır. bir tetikleyici Hello HTTP bağlayıcısı vardır.

| Tetikleyici | Açıklama |
| --- | --- |
| HTTP |Bir HTTP çağrı yapar ve hello yanıt içeriği döndürür. |

## <a name="http-action"></a>HTTP eylemi
Aşağıda, bu bağlayıcıyı destekler hello eylemin hello Ayrıntılar verilmiştir. bir olası eylemin Hello HTTP bağlayıcısı vardır.

| Eylem | Açıklama |
| --- | --- |
| HTTP |Bir HTTP çağrı yapar ve hello yanıt içeriği döndürür. |

## <a name="http-details"></a>HTTP ayrıntıları
Merhaba aşağıdaki tablolar hello gerekli ve isteğe bağlı giriş alanları hello eylem ve hello eylemini kullanarak ile ilişkili hello karşılık gelen çıkış ayrıntıları için açıklamaktadır.

#### <a name="http-request"></a>HTTP isteği
Merhaba, HTTP giden isteğinde hello eylemi için girdi alanlarının verilmiştir.
A * gerekli bir alan olduğu anlamına gelir.

| Görünen ad | Özellik adı | Açıklama |
| --- | --- | --- |
| Yöntemi * |Yöntemi |Merhaba HTTP fiili toouse |
| URI * |URI |Merhaba URI hello HTTP isteği için |
| Üstbilgileri |Üstbilgileri |HTTP üstbilgileri tooinclude JSON nesnesinin |
| Gövde |Gövde |Merhaba HTTP istek gövdesi |
| Kimlik Doğrulaması |Kimlik doğrulaması |Merhaba ayrıntılarında [kimlik doğrulaması](#authentication) bölümü |

<br>

#### <a name="output-details"></a>Çıkış Ayrıntıları
Merhaba, hello HTTP yanıtının çıkış ayrıntıları verilmiştir.

| Özellik adı | Veri türü | Açıklama |
| --- | --- | --- |
| Üstbilgileri |Nesne |Yanıt Üstbilgileri |
| Gövde |Nesne |Yanıt nesnesi |
| Durum kodu |Int |HTTP durum kodu |

## <a name="authentication"></a>Kimlik Doğrulaması
Merhaba Logic Apps özelliği toouse farklı tür HTTP uç noktaları karşı kimlik doğrulaması sağlar. Bu kimlik doğrulama ile Merhaba kullanabilirsiniz **HTTP**, ** [HTTP + Swagger](connectors-native-http-swagger.md)**, ve ** [HTTP Web kancası](connectors-native-webhook.md) ** bağlayıcılar. şu kimlik doğrulama türlerini hello yapılandırılabilir:

* [Temel kimlik doğrulaması](#basic-authentication)
* [İstemci sertifikası kimlik doğrulaması](#client-certificate-authentication)
* [Azure Active Directory (Azure AD) OAuth kimlik doğrulaması](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a>Temel kimlik doğrulaması

kimlik doğrulaması nesne aşağıdaki hello temel kimlik doğrulaması için gereklidir.
A * gerekli bir alan olduğu anlamına gelir.

| Özellik adı | Veri türü | Açıklama |
| --- | --- | --- |
| Türü * |type |Kimlik doğrulama türünü (olmalıdır `Basic` temel kimlik doğrulaması için) |
| Kullanıcı adı * |kullanıcı adı |Kullanıcı adı tooauthenticate |
| Parola * |password |Parola tooauthenticate |

> [!TIP]
> Toouse hello tanımından geri alınamaz bir parola istiyorsanız kullanın bir `securestring` parametre ve hello `@parameters()`  
>  [iş akışı tanımı işlevi](http://aka.ms/logicappdocs).

Örneğin:

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a>İstemci sertifikası kimlik doğrulaması

Merhaba aşağıdaki kimlik doğrulama nesnesi için istemci sertifikası kimlik doğrulaması gereklidir. A * gerekli bir alan olduğu anlamına gelir.

| Özellik adı | Veri türü | Açıklama |
| --- | --- | --- |
| Türü * |type |Merhaba kimlik doğrulama türünü (olmalıdır `ClientCertificate` SSL istemci sertifikaları için) |
| PFX * |PFX |Merhaba Base64 ile kodlanmış içeriğini hello kişisel bilgi değişimi (PFX) dosyası |
| Parola * |password |PFX dosyası Hello parola tooaccess hello |

> [!TIP]
> kullanabileceğiniz toouse hello mantıksal uygulama kaydetme sonra hello tanımında okunamaz bir parametre, bir `securestring` parametre ve hello `@parameters()`  
>  [iş akışı tanımı işlevi](http://aka.ms/logicappdocs).

Örneğin:

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a>Azure AD OAuth kimlik doğrulaması
kimlik doğrulaması nesne aşağıdaki hello Azure AD OAuth kimlik doğrulaması için gereklidir. A * gerekli bir alan olduğu anlamına gelir.

| Özellik adı | Veri türü | Açıklama |
| --- | --- | --- |
| Türü * |type |Merhaba kimlik doğrulama türünü (olmalıdır `ActiveDirectoryOAuth` Azure AD OAuth için) |
| Kiracı * |Kiracı |hello Azure AD Kiracı için Hello Kiracı tanımlayıcı |
| Hedef kitle * |Hedef kitle |Merhaba kaynak yetkilendirme toouse isteme. Örneğin, `https://management.core.windows.net/` |
| İstemci kimliği * |istemci kimliği |Merhaba Azure AD uygulaması için istemci tanımlayıcı hello |
| Gizli * |Gizli |Merhaba belirteç isteme hello istemci Hello gizliliği |

> [!TIP]
> Kullanabileceğiniz bir `securestring` parametre ve hello `@parameters()` [iş akışı tanımı işlevi](http://aka.ms/logicappdocs) toouse kaydettikten sonra hello tanımında okunamaz bir parametre.
> 
> 

Örneğin:

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a>Sonraki adımlar
Şimdi, hello platform deneyin ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md). Keşfedebilirsiniz bakarak Logic Apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).

