---
title: "Azure AD: SSPR kaydı | Microsoft Docs"
description: "Kimlik doğrulama verileri için Azure AD Self Servis parola kaydı Sıfırla"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: end-user
ms.openlocfilehash: dfcd0106616218c84d23920b124bed5b202cdd6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="register-for-self-service-password-reset"></a>Self servis parola sıfırlama için kaydolma

> [!IMPORTANT]
> **Oturum açmada sorun yaşadığınız için mi buradasınız?** Sorun yaşıyorsanız bkz. [kendi parolanızı değiştirme ve sıfırlama](active-directory-passwords-update-your-own-password.md).

Bir son kullanıcı parolanızı sıfırlama veya Self Servis parola sıfırlama (SSPR) kullanan toospeak tooa kişi gerek kalmadan hesabınızın kilidini açın. Bu işlevi kullanabilmek için tooregister kimlik doğrulama yöntemleri veya yöneticinize doldurulmuş önceden tanımlanmış hello kimlik doğrulama yöntemleri onaylayın.

## <a name="register-or-confirm-authentication-data-with-sspr"></a>SSPR ile kimlik doğrulama verilerini kaydetme veya onaylama

1. Cihaz ve Git toohello açık hello web tarayıcısını [parola sıfırlama kayıt sayfası](http://aka.ms/ssprsetup)
2. Yöneticiniz tarafından sağlanan kullanıcı adınızı ve parolanızı girin
3. BT personeliniz şey, bir veya daha fazlasını hello nasıl yapılandırdığınıza bağlı olarak seçenekler, tooconfigure için kullanılabilir ve doğrulayın. İzni toouse hello bilgileriniz varsa, yöneticiniz bu bazıları sizin için doldurmak.
    * Ofis telefonu yalnızca yöneticiniz tarafından ayarlanan mümkün toobe olduğu
    * Kimlik doğrulama telefon bir metin veya arama alabileceği bir cep telefonu erişim toolike olurdu tooanother telefon numarası olarak ayarlanmalıdır.
    * Kimlik doğrulama e-posta erişebilirsiniz tooan alternatif e-posta adresi ayarlanmalıdır hello parola olmadan tooreset gerekir.
    * Güvenlik soruları yöneticiniz size tooanswer onayladı soruların listesini sağlar. Aynı soru veya birden çok kez yanıt hello kullanamazsınız.
4. Yöneticiniz tarafından gerekli hello bilgilerini doğrulayın ve sağlar. Birden fazla seçeneği kullanılabilir durumdaysa, başka bir yöntem kullanılamaz duruma geldiğinde, birden çok yöntem tooprovide esneklik kaydetmeniz öneririz (örnek: seyahat ediyor ve tooaccess ofis telefonunuza)

    ![Kimlik doğrulama yöntemlerini kaydedin ve Son’a tıklayın][Register]

5. Adım 4 ile işiniz bittiğinde seçin **son** ve artık mümkün toouse Self Servis parola sıfırlama tooin hello gelecekteki gerektiğinde olacaktır.

Merhaba kimlik doğrulama telefon veya kimlik doğrulama e-posta veri girerseniz, hello genel dizininde görünür değil. Bu veriler görebilen hello yalnızca siz ve yöneticilerinizi kişilerdir. Yalnızca, hello tooyour güvenlik soruları yanıtlar görebilirsiniz.

Yöneticiler, tooconfirm zaman toomake hala hello uygun yöntemleri kayıtlı olduğundan emin bir süre sonra kimlik doğrulama yöntemleri gerektirebilir.

## <a name="common-problems-and-their-solutions"></a>Ortak sorunlar ve çözümleri

 Bazı ortak hata durumları ve bunların çözümleri şunlardır:

| Hata durumu| Hangi hata görürüm?| Çözüm |
| --- | --- | --- |
| Kullanıcı Kimliğimi girdikten sonra "Lütfen sistem yöneticinize başvurun" sayfası alıyorum | Lütfen sistem yöneticinize başvurun <br> <br> Kullanıcı hesabı parolanızı Microsoft tarafından yönetilmediğini algıladık. Sonuç olarak, bağlanamıyoruz tooautomatically parolanızı sıfırlayın. <br> <br> Daha fazla yardım için BT personeliniz toocontact gerekir. | BT personeliniz parolanızı, şirket içi ortamınızda yönetir ve tooreset izin vermiyor bu iletiyi görüyorsunuz parolanızı gelen hesap bağlantısı erişemiyor. <br> <br> BT personel doğrudan için parolanızı kişi Yardım ve bildirmek tooreset bunlar bu özellik sizin için etkinleştirebileceğiniz şekilde tooreset parolanızı istediğiniz bilirsiniz.|
| Kullanıcı Kimliğimi girdikten sonra bir "hesabınız parola sıfırlama için etkin değil" hatası alıyorum | Hesabınız parola sıfırlama için etkinleştirilmedi <br> <br> Üzgünüz, ancak, BT personeliniz hesabınız bu hizmeti kullanacak şekilde ayarlama değil. <br> <br> İsterseniz, biz kuruluş tooreset içinde bir Yönetici parolanızı sizin için başvurabilirsiniz. | BT personeliniz parola sıfırlama kuruluşunuzdan için etkin değil çünkü bu iletiyi görüyorsunuz hesap bağlantısı erişilemiyor veya toouse hello özelliği lisanslı kurmadı. <br> <br> tooreset parolanızı, bir yönetici bağlantı toosend bir e-posta tooyour şirket kişiyi tıklatın BT personeli, adı ve istediğiniz tooreset parolanızı bunlar bu özellik sizin için etkinleştirebileceğiniz şekilde bildirmek. |
| Kullanıcı Kimliğimi girdikten sonra bir "biz hesabınızı doğrulanamadı" hatası alıyorum | Hesabınız doğrulanamıyor <br> <br> İsterseniz, biz kuruluş tooreset içinde bir Yönetici parolanızı sizin için başvurabilirsiniz. | Parola sıfırlama için etkinleştirilir, ancak toouse hello hizmet kayıtlı değil çünkü bu iletiyi görüyorsunuz. tooregister parola sıfırlama, erişim tooyour hesabı artık sonra toohttp://aka.ms/ssprsetup gidin. <br> <br> tooreset parolanızı, bir yönetici bağlantı toosend bir e-posta tooyour şirket 's kişiyi tıklatın BT personeli. |

## <a name="next-steps"></a>Sonraki Adımlar

* [Nasıl toochange Self Servis parola kullanarak parolanızı sıfırlayın](active-directory-passwords-update-your-own-password.md)
* [Parola sıfırlama kayıt sayfası](http://aka.ms/ssprsetup)
* [Parola sıfırlama portalı](https://passwordreset.microsoftonline.com/)
* [Tooyour Microsoft hesabı oturum açılamıyor](https://support.microsoft.com/help/12429/microsoft-account-sign-in-cant)

[Register]: ./media/active-directory-passwords-reset-register/register-2-methods.png "Kayıtlı yöntemleri ve son düğmesini gösteren parola sıfırlama kayıt sayfası"

