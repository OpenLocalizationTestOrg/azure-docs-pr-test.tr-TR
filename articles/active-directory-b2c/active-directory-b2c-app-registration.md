---
title: "Azure Active Directory B2C: Uygulama kaydı | Microsoft Belgeleri"
description: "Nasıl tooregister uygulamanız Azure Active Directory B2C ile"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: PatAltimore
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: parakhj
ms.openlocfilehash: bd58e123751db387d6c8f16bd010291ba698b1a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a>Azure Active Directory B2C: Uygulamanızı kaydetme

Bu Hızlı Başlangıç, bir Microsoft Azure Active Directory (Azure AD) B2C Kiracısında bir uygulamayı birkaç dakika içinde kaydetmenize yardımcı olur. İşiniz bittiğinde, uygulamanızı hello Azure B2C Kiracı kullanmak için kayıtlı.

## <a name="prerequisites"></a>Ön koşullar

toobuild tüketicinin kaydolmasını ve oturum açma kabul eden bir uygulama, ilk Azure Active Directory B2C kiracısı ile tooregister Merhaba uygulaması gerekir. Kendi Kiracı özetlenen hello adımları kullanarak alma [bir Azure AD B2C kiracısı oluşturma](active-directory-b2c-get-started.md).

Hello hello Azure AD B2C dikey penceresinde hello Azure portalında oluşturulan uygulamaları yönetilen aynı konumu. PowerShell veya başka bir portal kullanarak hello B2C uygulamaları düzenlerseniz, desteklenmeyen haline gelir ve Azure AD B2C ile çalışmaz. Merhaba ayrıntıları görmek [hatalı uygulamaları](#faulted-apps) bölümü. 

## <a name="navigate-toob2c-settings"></a>TooB2C ayarları gidin

İçinde toohello oturum [Azure portal](https://portal.azure.com/) hello B2C kiracısının genel Yöneticisi hello gibi. 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

Sonraki adımlar kaydettirmekte olduğunuz hello uygulama türüne göre seçin:

* [Web uygulaması kaydetme](#register-a-web-app)
* [Web API’si kaydetme](#register-a-web-api)
* [Mobil veya yerel bir uygulamayı kaydetme](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a>Web uygulaması kaydetme

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

Web uygulamanız Azure AD B2C tarafından güvence altına alınmış bir web API'sini çağırıyorsa, aşağıdaki adımları gerçekleştirin:
   1. Giden toohello tarafından bir uygulama gizli anahtarı oluşturmak **anahtarları** dikey ve hello tıklayarak **anahtarı oluştur** düğmesi. Merhaba Not **uygulama anahtarı** değeri. Uygulamanızın kodda hello uygulama gizli anahtarı olarak hello değerini kullanın.
   2. **API Erişimi**’ne ve **Ekle**’ye tıklayıp web API’si ve kapsamlarınızı (izinler) seçin.

> [!NOTE]
> **Uygulama Gizli Anahtarı** önemli bir güvenlik kimlik bilgisidir ve güvenliği uygun şekilde sağlanmalıdır.
> 

[Çok atlama**sonraki adımlar**](#next-steps)

## <a name="register-a-web-api"></a>Web API’si kaydetme

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

Tıklatın **kapsamları yayımlanan** tooadd daha kapsamları gerektiğinde. Varsayılan olarak, hello "user_impersonation" kapsam tanımlanır. Merhaba user_impersonation kapsam diğer uygulamaları hello özelliği tooaccess hello oturum açmış kullanıcı adına bu API sağlar. İsterseniz, hello user_impersonation kapsam kaldırılabilir.

[Çok atlama**sonraki adımlar**](#next-steps)

## <a name="register-a-mobile-or-native-app"></a>Mobil veya yerel bir uygulamayı kaydetme

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[Çok atlama**sonraki adımlar**](#next-steps)

## <a name="limitations"></a>Sınırlamalar

### <a name="choosing-a-web-app-or-api-reply-url"></a>Bir web uygulaması veya api yanıt URL'si seçme

Şu anda Azure AD B2C ile kayıtlı uygulamalar sınırlı kısıtlı tooa yanıt URL değerler kümesidir. Merhaba web uygulamaları ve Hizmetleri için URL hello düzeniyle başlamalıdır yanıt `https`, ve URL değerler, tek bir DNS etki alanı paylaşması Tümünü Yanıtla. Örneğin, şu yanıt URL'lerinden birine sahip bir web uygulamasını kaydedemezsiniz:

`https://login-east.contoso.com`

`https://login-west.contoso.com`

Merhaba kayıt sistem hello tam DNS adını hello varolan yanıt URL toohello DNS adını eklemekte olduğunuz hello yanıt URL'si karşılaştırır. Aşağıdakilerden hello aşağıdaki koşullar doğruysa hello isteği tooadd hello DNS adı başarısız olur:

* Merhaba tam DNS adını hello yeni yanıt URL'si hello varolan yanıt URL'si hello DNS adı eşleşmiyor.
* Merhaba yeni yanıt URL'si Hello tam DNS adı bir alt etki alanı hello varolan yanıt URL'si değil.

Örneğin, hello uygulama bu yanıt URL'si sahipse:

`https://login.contoso.com`

Bu gibi tooit ekleyebilirsiniz:

`https://login.contoso.com/new`

Bu durumda, hello DNS adı tam olarak eşleşir. Ya da şunu yapabilirsiniz:

`https://new.login.contoso.com`

Bu durumda, login.contoso.com tooa DNS alt etki başvuran. Toohave east.contoso.com oturum açma ve oturum açma-west.contoso.com URL'leri yanıt olarak bir uygulama isterseniz bu sırada bu yanıt URL'leri eklemeniz gerekir:

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

Yanıt URL'si ilk Merhaba, alt etki alanlarına olduklarından hello ikinci iki ekleyebilirsiniz contoso.com.

### <a name="choosing-a-native-app-redirect-uri"></a>Yerel uygulama yeniden yönlendirme URI'si seçme

Mobil/yerel uygulamalar için bir yeniden yönlendirme URI’si seçerken dikkat edilmesi gereken iki önemli nokta şunlardır:

* **Benzersiz**: hello yeniden yönlendirme URI'si hello düzenini her uygulama için benzersiz olmalıdır. Bizim örneğimizde (com.onmicrosoft.contoso.appname://redirect/path) hello şema olarak com.onmicrosoft.contoso.appname kullanırız. Bu örneği izlemeniz önerilir. İki uygulama hello paylaşıyorsanız aynı, hello Düzen kullanıcı bir "uygulama Seç" iletişim kutusu görür. Merhaba kullanıcı yanlış bir seçim yaparsa hello oturum açma başarısız olur.
* **Tam**: Yeniden yönlendirme URI’sinin bir şeması ve yolu olmalıdır. Merhaba yolunu en az bir eğik hello etki (örneğin, //contoso/ çalışır ve //contoso başarısız) içermelidir.

Yeniden yönlendirme URI'si Merhaba, alt çizgi gibi özel karakterler olmadığına olduğundan emin olun.

### <a name="faulted-apps"></a>Hatalı uygulamalar

B2C uygulamaları şu durumlarda DÜZENLENMEMELİDİR:

* [Klasik Azure portalı](https://manage.windowsazure.com/) ve [Uygulama Kayıt Portalı](https://apps.dev.microsoft.com/) gibi diğer uygulama yanıt portallarında.
* Grafik API'si veya PowerShell kullanılarak

Yukarıda açıklandığı gibi hello B2C uygulaması düzenleyin ve tooedit deneyin, bunu yeniden hello Azure AD B2C özellikleri dikey penceresinde hello Azure portal, hatalı bir uygulama olur ve uygulamanız artık Azure AD B2C ile kullanılamaz. Toodelete hello uygulamasına sahip ve yeniden oluşturun.

toodelete hello uygulama, Git toohello [uygulama kayıt portalı](https://apps.dev.microsoft.com/) ve Merhaba uygulaması silin. Merhaba uygulama toobe görünür için sırayla Merhaba uygulaması toobe hello sahibi (ve yalnızca hello Kiracı Yöneticisi) gerekir.

## <a name="next-steps"></a>Sonraki adımlar

Azure AD B2C ile kayıtlı bir uygulamaya sahip olduğunuza göre aşağıdakilerden birini tamamlayabilirsiniz [hızlı başlangıç öğreticilerimizden](active-directory-b2c-overview.md#get-started) tooget çalışır.

> [!div class="nextstepaction"]
> [Kaydolma, oturum açma ve parola sıfırlama seçenekleriyle bir ASP.NET web uygulaması oluşturma](active-directory-b2c-devquickstarts-web-dotnet-susi.md)