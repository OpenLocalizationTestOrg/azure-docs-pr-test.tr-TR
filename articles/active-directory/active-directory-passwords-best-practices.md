---
title: "Kullanıma Sunma: Azure AD SSPR | Microsoft Docs"
description: "Azure AD self servis parola sıfırlama özelliğinin başarıyla kullanıma sunulması için ipuçları"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: f8cd7e68-2c8e-4f30-b326-b22b16de9787
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 73d31679b38ff009a767335adaebc49fbc5a75b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="roll-out-password-reset-for-users"></a>Kullanıcılar için parola sıfırlamayı kullanıma sunma

Çoğu müşteri tooensure SSPR işlevlerin kesintisiz bir sunum izleyin hello adımları izleyin.

1. [Dizininizde parola sıfırlamayı etkinleştirin](active-directory-passwords-getting-started.md)
2. [Parola geri yazma için şirket içi AD izinlerini yapılandırın](active-directory-passwords-how-it-works.md#active-directory-permissions)
3. [Parola geri yazma yapılandırma](active-directory-passwords-writeback.md#configuring-password-writeback) toowrite parolaları Azure AD alanından geri tooyour şirket içi dizin
4. [Gerekli lisansları atayıp doğrulayın](active-directory-passwords-licensing.md)
5. Yavaş yavaş, çıkışı tooroll istiyorsanız, isteğe bağlı olarak sınırı parola kullanıcılar tooroll hello özelliği çıkışı tooa grubunun yavaş zamanla sıfırlayabilirsiniz. toodo hello ayarlamanız **Self Servis parola sıfırlama etkin** gelen geçiş **herkes** çok**bir grup** ve parola sıfırlama için güvenlik grubu tooenable seçin. Merhaba bu grubun üyeleri tüm lisansları atanmış toothem varsa gerekir ve mükemmel şekilde tooenable [grup tabanlı lisans](active-directory-passwords-licensing.md#enable-group-or-user-based-licensing).
6. Merhaba düşük kümesini doldurmak [kimlik doğrulama verileri](active-directory-passwords-data.md), ilkenize göre.
7. Kullanıcılarınızı nasıl öğretmek yönergeleri tooshow göndererek toouse SSPR, bunları nasıl tooregister ve nasıl tooreset.
    > [!NOTE]
    > Microsoft, Azure yönetici hesapları için güçlü kimlik doğrulama gereksinimleri uyguladığından, SSPR özelliğini yönetici olmayan bir kullanıcıyla test edin. Hello Yöneticisi parola ilkesi hakkında daha fazla bilgi için bkz: bizim [derinlemesine makale](active-directory-passwords-how-it-works.md).

8. Herhangi bir noktada tooenforce kaydı seçin ve kullanıcıların tooreconfirm belirli bir süre sonra kendi kimlik doğrulama bilgileri gerektirir. Kullanıcıların toohave tooregister istemiyorsanız, şunları yapabilirsiniz [parola sıfırlama son kullanıcı kayıt gerektirmeden dağıtma](active-directory-passwords-data.md).
9. Zamanla, kaydetme ve hello görüntüleyerek kullanarak kullanıcıların gözden [Azure AD tarafından sağlanan raporlama](active-directory-passwords-reporting.md).

## <a name="email-based-rollout"></a>E-posta tabanlı kullanıma sunma

Birçok müşteri hello en kolay yolu tooget kullanıcılar toouse SSPR basit toouse yönergeleri içeren bir e-posta kampanya olduğunu bulur. [Şablonları toohelp, sunum kullanabileceğiniz üç basit e-postaları oluşturduk.](https://onedrive.live.com/?authkey=%21AD5ZP%2D8RyJ2Cc6M&id=A0B59A91C740AB16%2125063&cid=A0B59A91C740AB16)

* **Çok yakında** hello hafta veya gün sunum toolet kullanıcıların ihtiyaç duydukları toodo bir şey bilmesi önce kullanılan şablon toobe e-posta.
* **Şu anda kullanılabilir** e-posta şablonu kullanılan toobe hello başlatma toodrive kullanıcılar tooregister gününü ve bunlar gerektiğinde SSPR kullanabilmeniz için kendi kimlik doğrulama verilerini onaylayın.
* **Anımsatıcı oturum** birkaç gün tooweeks için şablon dağıtımını tooremind kullanıcılar tooregister sonra e-posta ve kimlik doğrulama verilerini onaylayın.

## <a name="creating-your-own-password-portal"></a>Kendi parola portalınızı oluşturma

Birçok büyük müşterilerimizin toohost Web sayfası seçin ve bir kök https://passwords.contoso.com gibi DNS girişi oluşturun. Bu sayfayı bağlantılar toohello Azure AD parola sıfırlama ile doldurmak, parola sıfırlama kaydı, parola değişikliği portalları ve diğer kuruluşa özgü bilgileri. Tüm e-posta iletişimini veya ilanları çıkışı, ardından dahil edebileceğiniz markalı, gönderdiğiniz etkileyici, kullanıcıların ihtiyaç duydukları toouse hello Hizmetleri toowhen gidebilirsiniz URL.

* Parola sıfırlama portalı - https://passwordreset.microsoftonline.com/
* Parola sıfırlama kayıt portalı - http://aka.ms/ssprsetup
* Parola değiştirme portalı - https://account.activedirectory.windowsazure.com/ChangePassword.aspx

## <a name="using-enforced-registration"></a>Zorunlu kayıt kullanma

Parola sıfırlama için kullanıcıların tooregister istiyorsanız, Azure AD kullanarak oturum açtığınızda, bunları tooregister zorlayabilirsiniz. Dizininizden 's bu seçeneği etkinleştirebilirsiniz **parola sıfırlama** hello etkinleştirerek dikey **oturum açarken gerektiren kullanıcılar tooRegister** hello seçeneği **kayıt** sekmesini tıklatın.

Yöneticiler gerektirebilirsiniz kullanıcılar toore kaydını bir süre sonra ayarı hello tarafından **sayısı kullanıcılar önce gün sorulan tooreconfirm kendi kimlik doğrulama bilgilerini** 0-730 arasında gün.

Bu seçeneği etkinleştirdikten sonra oturum kullanıcılar kendi yönetici gerekli bunları tooverify bildiren bir ileti görürsünüz, kimlik doğrulama bilgileri.

## <a name="populate-authentication-data"></a>Kimlik doğrulama verilerini doldurma

Varsa, [kullanıcılarınız için kimlik doğrulama verilerini doldurmak](active-directory-passwords-data.md), sonra da kullanıcılar parola sıfırlama mümkün toouse SSPR olan önce tooregister gerekmez. Tanımladığınız hello parolası sıfırlama ilkesini karşılayan tanımlanan hello kimlik doğrulama verileri kullanıcıların sahip olduğu sürece, mümkün tooreset kullanıcılardır parolalarını.

## <a name="disabling-self-service-password-reset"></a>Self servis parola sıfırlamayı devre dışı bırakma

Self Servis parola sıfırlama devre dışı bırakma Azure AD kiracınıza açarak ve çok giderek olarak basit**parola sıfırlama**, **özellikleri**ve seçme **hiç kimse** altında **Self Servis parola sıfırlama etkin**

## <a name="next-steps"></a>Sonraki adımlar

bağlantılar aşağıdaki hello parola sıfırlama ve Azure AD kullanma ile ilgili ek bilgiler sağlar

* [**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın 
* [**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın
* [**Veri** ](active-directory-passwords-data.md) - gereklidir hello verileri anlamak ve nasıl kullanıldığı için parola yönetimi
* [**Özelleştirme** ](active-directory-passwords-customize.md) -hello görünümüne hello SSPR deneyimi, şirketiniz için özelleştirebilirsiniz.
* [**İlke**](active-directory-passwords-policy.md) - Azure AD parola ilkelerini anlayın ve ayarlayın
* [**Parola Geri Yazma**](active-directory-passwords-writeback.md) - Şirket içi dizininizde parola geri yazma özelliğinin nasıl çalıştığını anlayın
* [**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin
* [**Teknik derinlemesine** ](active-directory-passwords-how-it-works.md) -hello perdenin toounderstand nasıl çalıştığını gidin
* [**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl? Neden? Ne? Nerede? Kim? Ne zaman? -Her zaman tooask istediğinizi tooquestions yanıtlar
* [**Sorun giderme** ](active-directory-passwords-troubleshoot.md) -nasıl biz SSPR ile bkz tooresolve ortak sorunları öğrenin
