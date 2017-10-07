---
title: "oturum açma aaaSingle tooapps Azure AD uygulama proxy'si ile | Microsoft Docs"
description: "Yayımlanan şirket içi uygulamalarınızı hello Azure portalında Azure AD uygulama proxy'si için çoklu oturum açmayı etkinleştirin."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5ff288d36163b74215677d9e34c93c985ac33d54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a>Çoklu oturum açma için uygulama proxy'si ile vaulting parola

Azure Active Directory Uygulama proxy'si uzak çalışanlar güvenli bir şekilde bunları çok erişebilmesi için şirket içi uygulamaları yayımlama üretkenlik geliştirmenize yardımcı olur. Hello Azure portalı, çoklu oturum açma (SSO) toothese uygulamaları de ayarlayabilirsiniz. Kullanıcılarınızın Azure AD ile tooauthenticate yeterlidir ve toosign yeniden vermeden kuruluş uygulamanız erişebilir.

Uygulama proxy'si destekleyen birkaç [tek oturum açma modları](application-proxy-sso-overview.md). Parola tabanlı oturum açma kimlik doğrulaması için bir kullanıcı adı/parola bileşimi kullanan uygulamalar için tasarlanmıştır. Uygulamanız için parola tabanlı oturum açma yapılandırdığınızda, kullanıcılarınızın bir kez toohello şirket içi uygulama toosign sahip. Bundan sonra Azure Active Directory hello oturum açma bilgileri depolar ve kullanıcılarınızın, uzaktan erişim otomatik olarak toohello uygulama sağlar. 

Zaten varsa yayımlanan ve uygulama proxy'si ile uygulamanızı test. Aksi takdirde, başlangıç adımları [Azure AD uygulama proxy'si ile uygulama yayımlama](application-proxy-publish-azure-portal.md) tekrar buraya gelin. 

## <a name="set-up-password-vaulting-for-your-application"></a>Uygulamanız için vaulting parola ayarlama

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) yönetici olarak.
2. Seçin **Azure Active Directory** > **kurumsal uygulamalar** > **tüm uygulamaları**.
3. Merhaba listeden hello uygulama SSO tooset yedeklemek istediğinizi seçin.  
4. Seçin **çoklu oturum açma**.

   ![Çoklu oturum açma seçin](./media/application-proxy-sso-azure-portal/select-sso.png)

5. Merhaba SSO modunu seçin **parola tabanlı oturum açma**.
6. Merhaba URL'Sİ'ın oturum açma, burada kullanıcılar kendi kullanıcı adı ve parola toosign tooyour uygulama hello şirket ağı dışında girin, başlangıç sayfası için hello URL'sini girin. Bu hello uygulama proxy'si aracılığıyla hello uygulama yayımlandığında oluşturduğunuz dış URL olabilir. 

   ![Parola tabanlı oturum açma seçin ve URL'nizi girin](./media/application-proxy-sso-azure-portal/password-sso.png)

7. **Kaydet**’i seçin.

<!-- Need toorepro?
7. hello page should tell you that a sign-in form was successfully detected at hello provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow hello instructions toopoint out where hello sign-in credentials go. 
-->

## <a name="test-your-app"></a>Uygulamanızı test etme

Uzaktan erişim tooyour uygulama için yapılandırılan tooexternal URL'ye gidin. Bu uygulama için kimlik bilgileri (veya hello hesabının kimlik bilgilerini erişimle ayarladığınız bir test) oturum açın. Başarıyla oturum açtıktan sonra mümkün tooleave hello uygulama ve kimlik bilgilerinizi tekrar girmeden geri dönün. 

## <a name="next-steps"></a>Sonraki adımlar

- Diğer yolları tooimplement hakkında okuyun [uygulama proxy'si ile çoklu oturum açma](application-proxy-sso-overview.md)
- Hakkında bilgi edinin [uygulamaları Azure AD uygulama proxy'si ile uzaktan erişim için güvenlik konuları](application-proxy-security-considerations.md)