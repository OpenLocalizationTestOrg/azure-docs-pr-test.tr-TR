---
title: "Hızlı Başlangıç: Azure AD SSPR | Microsoft Docs"
description: "Azure AD self servis parola sıfırlamayı hızlıca dağıtma"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: bde8799f-0b42-446a-ad95-7ebb374c3bec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4fed3a1c690fd6423ee5d3e5baef690d8896fbe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-azure-ad-self-service-password-reset"></a>Hızlı Başlangıç: Azure AD self servis parola sıfırlama

> [!IMPORTANT]
> **Oturum açmada sorun yaşadığınız için mi buradasınız?** Sorun yaşıyorsanız bkz. [kendi parolanızı değiştirme ve sıfırlama](active-directory-passwords-update-your-own-password.md).

## <a name="rapidly-deploy-self-service-password-reset"></a>Self servis parola sıfırlamayı hızlıca dağıtma

Basit bir BT yöneticileri tooempower kullanıcılar tooreset anlamına gelir veya bunların parolaları veya hesaplarının kilidini (SSPR) teklifleri Self Servis parola sıfırlama. Kullanıcıların hello sistem bildirimleri tooalert birlikte kullandığınızda hello sistem ayrıntılı raporlama tootrack içerir, toomisuse veya Uygunsuz kullanım.

Bu kılavuz, çalışan bir deneme sürümü ya da lisanslı bir Azure AD kiracısına zaten sahip olduğunuzu varsayar. Azure AD ayarı yardıma gereksinim duyarsanız, hello makalesine bakın [Azure AD ile çalışmaya başlama](https://azure.microsoft.com/trial/get-started-active-directory/).

1. Var olan Azure AD kiracınızda **"Parola sıfırlama"** öğesini seçin

2. Merhaba gelen **"Özellikler"** "Self Servis parola sıfırlama etkin" Merhaba aşağıdakilerden birini hello seçeneği altında ekranı
    * Kimse - herhangi bir mümkün toouse SSPR işlevdir
    * Bir - belirli bir Azure AD yalnızca üyeleri, seçtiğiniz grubu mümkün toouse SSPR işlevselliği olan
    * Herkes - tüm kullanıcılar Azure AD kiracınıza hesaplarıyla olan mümkün toouse SSPR işlevi

3. Merhaba gelen **"Kimlik doğrulama yöntemleri"** ekran'ı seçin
    * Birkaç yöntem tooreset gerekli - en az bir ya da en az iki destekliyoruz
    * Yöntemleri kullanılabilir toousers - en az bir ihtiyacımız ancak hiçbir zaman toohave kullanılabilir bir ek seçim hurts
        * **E-posta** bir e-posta kodu toohello kullanıcı kimlik doğrulama e-posta adresi yapılandırılmış gönderir
        * **Cep telefonu** verir hello kullanıcı hello seçim tooreceive bir çağrı veya metin kodu tootheir ile yapılandırılmış mobil telefon numarası
        * **Ofis telefonu** çağrıları hello kullanıcı kodu tootheir ile yapılandırılan ofis telefon numarası
        * **Güvenlik soruları** toochoose gerektirir
            * Soru sayısı tooregister gerekli - başarılı kaydı, yani bir kullanıcı için hello en az bir havuzu toopull gelen sorulara daha fazla toocreate tooanswer seçebilirsiniz. Bu seçenek 3-5'ten ayarlanabilir ve daha büyük veya gerekir soruları gerekli tooreset toohello sayısı eşit.
                * Özel soru güvenlik soruları seçerken hello "Özel" düğmesine tıklayarak eklenebilir.
            * Gereken soru sayısını tooreset - 3-5 soruları toobe sıfırlama veya kilidi kullanıcıların parola toobe izin vermeden önce doğru yanıtların gelen ayarlanabilir.

4. Önerilen: **"Özelleştirme"** tanımladığınız toochange hello "yöneticinize başvurun" bağlantı toopoint tooa sayfa veya e-posta adresi izin verir

5. İsteğe bağlı: Merhaba **"Kayıt"** ekran Yöneticiler için başlangıç seçeneklerini sağlar:
    * Oturum açarken kullanıcıların tooregister gerektirir
    * Sayısı kullanıcılar önce gün sorulan tooreconfirm kendi kimlik doğrulama bilgileri

6. İsteğe bağlı: Merhaba **"Bildirim"** ekran Yöneticiler için hello seçenekleri sağlar:
    * Parola sıfırlamayı kullanıcılara bildir
    * Diğer yöneticiler parolalarını sıfırladığında tüm yöneticilere bildir

**Bu noktada Azure AD kiracınız için SSPR’ı yapılandırdınız**. Burada durdurun ya da üzerinde tooconfigure devam parolaları tooan eşitlemesini şirket içi AD etki alanı.

> [!NOTE]
> Microsoft, Azure yönetici hesapları için güçlü kimlik doğrulama gereksinimleri uyguladığından, SSPR özelliğini yönetici olmayan bir kullanıcıyla test edin. Hello Yöneticisi parola ilkesi hakkında daha fazla bilgi için bkz: bizim [parola ilkesi makale](active-directory-passwords-policy.md#administrator-password-policy-differences).

## <a name="configure-synchronization-tooexisting-identity-source"></a>Eşitleme tooexisting kimlik kaynağı yapılandırın

tooenable şirket içi kimlik eşitleme tooAzure AD, yapılandırmak ve tooinstall gereksinim [Azure AD Connect](./connect/active-directory-aadconnect.md) kuruluşunuzdaki bir sunucuda. Bu uygulama, eşitleme üzerinden kullanıcıların ve grupların varolan kimlik kaynak tooyour Azure AD kiracınıza işler.

* [DirSync veya Azure AD eşitleme tooAzure AD Connect yükseltme](./connect/active-directory-aadconnect-dirsync-deprecated.md)
* [Hızlı ayarları kullanarak Azure AD Connect ile çalışmaya başlama](./connect/active-directory-aadconnect-get-started-express.md)
* [Parola geri yazma yapılandırma](active-directory-passwords-writeback.md#configuring-password-writeback) toowrite parolaları Azure AD alanından geri tooyour şirket içi dizin.

## <a name="disabling-self-service-password-reset"></a>Self servis parola sıfırlamayı devre dışı bırakma

Self Servis parola sıfırlama devre dışı bırakma Azure AD kiracınıza açarak ve çok giderek olarak basit**parola sıfırlama > Özellikler** > seçin **hiçbiri** altında **Self Servis parola sıfırlama Etkin**

### <a name="learn-more"></a>Daha fazla bilgi edinin
bağlantılar aşağıdaki hello parola sıfırlama ve Azure AD kullanma ile ilgili ek bilgiler sağlar

* [**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın
* [**Veri** ](active-directory-passwords-data.md) - gereklidir hello verileri anlamak ve nasıl kullanıldığı için parola yönetimi
* [**Sunum** ](active-directory-passwords-best-practices.md) -planlama ve burada bulunan hello kılavuzu kullanarak SSPR tooyour kullanıcılara dağıtma
* [**Özelleştirme** ](active-directory-passwords-customize.md) -hello görünümüne hello SSPR deneyimi, şirketiniz için özelleştirebilirsiniz.
* [**İlke**](active-directory-passwords-policy.md) - Azure AD parola ilkelerini anlayın ve ayarlayın
* [**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin
* [**Teknik derinlemesine** ](active-directory-passwords-how-it-works.md) -hello perdenin toounderstand nasıl çalıştığını gidin
* [**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl? Neden? Ne? Nerede? Kim? Ne zaman? -Her zaman tooask istediğinizi tooquestions yanıtlar
* [**Sorun giderme** ](active-directory-passwords-troubleshoot.md) -nasıl biz SSPR ile bkz tooresolve ortak sorunları öğrenin

## <a name="next-steps"></a>Sonraki adımlar

Bu Hızlı Başlangıç, kullanıcılarınız için nasıl tooconfigure Self Servis parola sıfırlama öğrendiniz. Merhaba toohello portal bağlantıya toocontinue toohello Azure portal toocomplete şu adımları izleyin.

> [!div class="nextstepaction"]
> [Self servis parola sıfırlamayı etkinleştirme](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset)

