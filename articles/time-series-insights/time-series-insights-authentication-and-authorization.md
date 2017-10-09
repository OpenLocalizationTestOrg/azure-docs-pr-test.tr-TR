---
title: "aaaConfigure kimlik doğrulama ve yetkilendirme çağıran özel bir uygulama için hello Azure zaman serisi Insights API'si | Microsoft Docs"
description: "Bu öğretici Azure zaman serisi Insights API'si tooconfigure kimlik doğrulama ve yetkilendirme çağıran özel bir uygulama için nasıl hello açıklar"
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a>Kimlik doğrulama ve yetkilendirme Azure zaman serisi Insights API'si

Bu makalede nasıl tooconfigure çağıran özel bir uygulama hello Azure zaman serisi Insights API'si açıklanmaktadır.

## <a name="service-principal"></a>Hizmet sorumlusu

Bu bölümde, nasıl tooconfigure bir uygulama tooaccess hello zaman serisi Insights API'si hello uygulama adına açıklanmaktadır. Merhaba uygulaması sonra verileri sorgulamak veya uygulama kimlik bilgilerini ve değil hello kullanıcı kimlik bilgileri ile Merhaba zaman serisi Öngörüler ortamda başvuru veri yayımlama.

Zaman serisi Öngörüler tooaccess gerektiren bir uygulamanız varsa, Azure Active Directory Uygulama ayarlama ve hello veri erişimi ilkelerini hello zaman serisi Öngörüler ortamında atamanız gerekir. Bu yaklaşım tercih toorunning hello uygulama kendi kimlik bilgileri altında nedeni:

* Kendi izinlerden farklıdır toohello uygulama kimliği izinleri atayabilirsiniz. Genellikle, bu kısıtlı tooexactly hangi hello uygulamanın toodo ihtiyacı izinlerdir. Örneğin, belirli bir zaman serisi Öngörüler ortamda veri hello uygulama tooonly okuma izin verebilirsiniz.
* Sizin Sorumluluklarınız değiştirirseniz toochange hello uygulamanın kimlik bilgileri yok.
* Katılımsız betik çalıştırılırken bir sertifika veya bir uygulamanın anahtar tooautomate kimlik doğrulaması kullanabilirsiniz.

Bu makalede, bu adımları aracılığıyla tooperform hello Azure portalına nasıl gösterir. Merhaba uygulaması yalnızca bir kuruluştaki hedeflenen toorun olduğu bir tek kiracılı uygulama odaklanır. Genellikle, kuruluşunuzda çalıştırmak satır iş kolu uygulamaları için tek Kiracı uygulamaları kullanın.

Merhaba Kurulum akışında üç üst düzey adımları içerir:

1. Azure Active Directory'de bir uygulama oluşturun.
2. Bu uygulama tooaccess hello zaman serisi Öngörüler ortamı yetkilendirin.
3. Merhaba uygulama kimliği ve anahtarı tooacquire belirteci toohello kullanma `"https://api.timeseries.azure.com/"` İzleyici veya kaynak. Merhaba belirteci sonra kullanılan toocall hello zaman serisi Insights API'si olabilir.

Ayrıntılı adımlar hello şunlardır:

1. Hello Azure portal, seçin **Azure Active Directory** > **uygulama kayıtlar** > **yeni uygulama kaydı**.

   ![Azure Active Directory'de yeni uygulama kaydı](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. Merhaba uygulama adı, select hello türü toobe vermek **Web uygulaması / API**, için geçerli bir URI seçin **oturum açma URL'si**, tıklatıp **oluşturma**.

   ![Azure Active Directory'de Merhaba uygulaması oluşturma](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. Yeni oluşturulan uygulamanızı seçin ve kendi uygulama kimliği tooyour sık kullandığınız metin Düzenleyicisi'ni kopyalayın.

   ![Merhaba uygulama Kimliğini kopyalayın](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. Seçin **anahtarları**, hello anahtar adı, select hello sona erme girin ve tıklayın **kaydetmek**.

   ![Uygulama anahtarı seçin](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Merhaba anahtar adını ve sona erme girin ve Kaydet'e tıklayın.](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. Merhaba anahtar tooyour sık kullandığınız metin düzenleyiciyi kopyalayın.

   ![Merhaba uygulama anahtarı kopyalayın](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. Merhaba zaman serisi Öngörüler ortamı için seçin **veri erişimi ilkelerini** tıklatıp **Ekle**.

   ![Yeni veri erişim ilkesi toohello zaman serisi Öngörüler ortama ekleyin](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. Merhaba, **Kullanıcı Seç** iletişim kutusunda, Yapıştır hello uygulama adını (2. adım) veya uygulama Kimliğinden (3. adım).

   ![Bir uygulama Bul hello Kullanıcı Seç iletişim kutusu](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. Select hello rolü (**okuyucu** veri sorgulama için **katkıda bulunan** veri sorgulama ve başvuru verileri değiştirme) tıklatıp **Tamam**.

   ![Okuyucu ve katkıda bulunan hello rolü Seç iletişim kutusunda seçin](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. Tıklayarak Hello ilkeyi kaydetmek **Tamam**.

10. Merhaba uygulama kimliği (3. adım) ve uygulama (Başlangıç 5. adım) anahtar tooacquire hello belirteci hello uygulama adına kullanın. Merhaba belirteci sonra hello geçirilebilir `Authorization` zaman serisi Insights API'si hello uygulama çağrıları hello zaman üstbilgi.

    C# kullanıyorsanız, kod tooacquire hello belirteci hello uygulama adına aşağıdaki hello kullanabilirsiniz. Tam bir örnek için bkz: [C# kullanarak veri sorgulama](time-series-insights-query-data-csharp.md).

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a>Sonraki adımlar

Merhaba uygulama kimliği ve anahtarı uygulamanızda kullanın. Merhaba zaman serisi Öngörüler API çağrıları örnek kod için bkz: [C# kullanarak veri sorgulama](time-series-insights-query-data-csharp.md).

## <a name="see-also"></a>Ayrıca bkz.

* [Sorgu API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) hello tam sorgu API Başvurusu için
* [Bir hizmet sorumlusu hello Azure portal oluşturma](../azure-resource-manager/resource-group-create-service-principal-portal.md)
