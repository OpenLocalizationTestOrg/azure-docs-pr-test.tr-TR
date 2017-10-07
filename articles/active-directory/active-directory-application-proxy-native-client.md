---
title: "aaaPublish yerel istemci uygulamaları - Azure AD | Microsoft Docs"
description: "Nasıl tooenable yerel istemci uygulamaları toocommunicate Azure AD uygulama ara sunucusu Bağlayıcısı tooprovide güvenli uzaktan erişim tooyour ile uygulamaları şirket içi kapsar."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 0ed2be217bf992f034d8321d5e66569b4cace24f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-native-client-apps-toointeract-with-proxy-applications"></a>Nasıl tooenable yerel istemci uygulamaları toointeract proxy uygulamaları ile

Toplama tooweb uygulamalarda, Azure Active Directory Uygulama proxy'si kullanılan toopublish yerel istemci uygulamaları da olabilir. Web uygulamaları bir tarayıcı erişilen sırada bir aygıtta yüklü olmadığından yerel istemci uygulamaları, web uygulamaları farklılık gösterir. 

Uygulama proxy'si yerel istemci uygulamalar tarafından verilen standart yetkilendirmek HTTP üstbilgilerinde gönderilen belirteçler kabul Azure AD destekler.

![Son kullanıcılar, Azure Active Directory ve yayımlanmış uygulamalar arasındaki ilişki](./media/active-directory-application-proxy-native-client/richclientflow.png)

Merhaba mvc'deki kimlik doğrulama ve birçok istemci ortamları, toopublish yerel uygulamaları destekler Azure AD kimlik doğrulama kitaplığı, kullanın. Uygulama proxy'si uygun hello [yerel uygulama tooWeb API senaryo](develop/active-directory-authentication-scenarios.md#native-application-to-web-api). Bu makalede hello dört adım toopublish uygulama proxy'si ve hello Azure AD kimlik doğrulama kitaplığı ile yerel bir uygulamaya anlatılmaktadır. 

## <a name="step-1-publish-your-application"></a>1. adım: uygulamanızı yayımlama
Başka bir uygulama gibi proxy uygulamanızı yayımlamak ve uygulamanız kullanıcıların tooaccess atayın. Daha fazla bilgi için bkz: [uygulama proxy'si ile uygulama yayımlama](active-directory-application-proxy-publish.md).

## <a name="step-2-configure-your-application"></a>2. adım: uygulamanızı yapılandırma
Yerel uygulamanız aşağıdaki gibi yapılandırın:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Çok gidin**Azure Active Directory** > **uygulama kayıtlar**.
3. Seçin **yeni uygulama kaydı**.
4. Select, uygulamanız için bir ad belirtin **yerel** hello uygulama türü olarak ve uygulamanız için hello yeniden yönlendirme URI'sini belirtin. 

   ![Yeni bir uygulama kaydı oluşturma](./media/active-directory-application-proxy-native-client/create.png)
5. **Oluştur**’u seçin.

Yeni bir uygulama kaydı oluşturma hakkında daha ayrıntılı bilgi için bkz: [uygulamaları Azure Active Directory ile tümleştirme](.//develop/active-directory-integrating-applications.md).


## <a name="step-3-grant-access-tooother-applications"></a>3. adım: Grant erişim tooother uygulamaları
Merhaba yerel uygulama açığa toobe tooother uygulamalar dizininizde etkinleştirin:

1. Hala **uygulama kayıtlar**, hello az önce oluşturduğunuz yeni yerel uygulama seçin.
2. Seçin **gerekli izinleri**.
3. **Add (Ekle)** seçeneğini belirleyin.
4. Açık hello ilk adım, **bir API seçin**.
5. Hello ilk bölümünde yayınlanan hello arama çubuğu toofind hello uygulama proxy'si uygulamayı kullanın. Bu uygulama seçin ve ardından **seçin**. 

   ![Merhaba proxy uygulamayı arayın](./media/active-directory-application-proxy-native-client/select_api.png)
6. Açık hello ikinci adım, **seçin izinleri**.
7. Yerel uygulama erişim tooyour proxy uygulamanızın Hello onay kutusunu toogrant kullanın ve ardından **seçin**.

   ![GRANT erişim tooproxy uygulama](./media/active-directory-application-proxy-native-client/select_perms.png)
8. Seçin **Bitti**.


## <a name="step-4-edit-hello-active-directory-authentication-library"></a>4. adım: hello Active Directory kimlik doğrulama kitaplığı Düzenle
Merhaba yerel uygulama kodunu metin aşağıdaki hello Active Directory Authentication Library (ADAL) tooinclude hello hello kimlik doğrulaması bağlamında düzenleyin:

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of hello Native app>",
        new Uri("<Redirect Uri of hello Native App>"),
        PromptBehavior.Never);

//Use hello Access Token tooaccess hello Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

Merhaba değişkenleri hello örnek kodda şu şekilde değiştirilmelidir:

* **Kiracı kimliği** hello Azure portalında bulunabilir. Çok gidin**Azure Active Directory** > **özellikleri** ve kopyalama hello dizin kimliği. 
* **Dış URL** hello Proxy Uygulama girdiğiniz hello ön uç URL'si. toofind bu değer, toohello gidin **uygulama proxy'si** hello proxy uygulama bölümü.
* **Uygulama Kimliği** Merhaba yerel uygulama hello üzerinde bulunabilir **özellikleri** hello yerel uygulama sayfası.
* **Merhaba yerel uygulamasının URI'sini yeniden yönlendir** hello üzerinde bulunabilir **yeniden yönlendirme URI'ler** hello yerel uygulama sayfası.


## <a name="see-also"></a>Ayrıca bkz.

Merhaba yerel uygulama akışı hakkında daha fazla bilgi için bkz: [yerel uygulama tooweb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)

Merhaba en son haberler ve güncelleştirmeler için hello denetleyin [uygulama ara sunucusu bloguna](http://blogs.technet.com/b/applicationproxyblog/)
