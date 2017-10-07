---
title: "aaaAzure Active Directory B2B işbirliği ile ilgili SSS | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği hakkında sorular yanıtlar toofrequently alın."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 4412bbc65274ff01782db81dfcc8818a6362ea7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-faqs"></a>Azure Active Directory B2B işbirliği ile ilgili SSS

Bu Azure Active Directory (Azure AD) işletmeden işletmeye (B2B) işbirliği hakkında sık sorulan sorular (SSS) düzenli aralıklarla güncelleştirilen tooinclude yeni konulardır.

### <a name="is-azure-ad-b2b-collaboration-available-in-hello-azure-classic-portal"></a>Azure AD B2B işbirliği hello Klasik Azure portalı var mı?
Hayır. Azure AD B2B işbirliği özellikleri yalnızca hello kullanılabilir [Azure portal](https://portal.azure.com) ve hello [erişim paneli](https://myapps.microsoft.com/). 

### <a name="can-we-customize-our-sign-in-page-so-it-is-more-intuitive-for-our-b2b-collaboration-guest-users"></a>Bizim B2B işbirliği Konuk kullanıcılar için daha sezgisel böylece biz oturum açma sayfamızı özelleştirebilir miyim?
Kesinlikle! Bkz: bizim [blog gönderisi bu özellik hakkında](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/07/improving-the-branding-logic-of-azure-ad-login-pages/). Hakkında daha fazla bilgi için nasıl oturum açma, kuruluşunuzun toocustomize sayfasında, bkz: [içinde toosign ve erişim paneli sayfasında şirket markası ekleme](active-directory-add-company-branding.md).

### <a name="can-b2b-collaboration-users-access-sharepoint-online-and-onedrive"></a>B2B işbirliği kullanıcılar SharePoint Online ve OneDrive erişebilir mi?
Evet. Ancak, hello özelliği toosearch hello Kişi Seçici kullanarak mevcut Konuk kullanıcılar için SharePoint Online olan **kapalı** varsayılan olarak. var olan konuk kullanıcılar hello seçeneği toosearch üzerinde tooturn ayarlamak **ShowPeoplePickerSuggestionsForGuestUsers** çok**üzerinde**. Bu ayar hello Kiracı düzeyinde veya hello site koleksiyonu düzeyinde açabilirsiniz. Merhaba kümesi SPOTenant ve Set-SPOSite cmdlet'leri kullanarak bu ayarı değiştirebilirsiniz. Bu cmdlet ile üyeleri tüm mevcut Konuk kullanıcılar hello dizinde arama yapabilirsiniz. Değişiklikler hello Kiracı kapsamda zaten sağlanmış SharePoint Online siteleri etkilemez.

### <a name="is-hello-csv-upload-feature-still-supported"></a>Hello CSV karşıya özellik hala destekleniyor mu?
Evet. Merhaba .csv dosyasını karşıya yükleme özelliğini kullanma hakkında daha fazla bilgi için bkz: [bu PowerShell örnek](active-directory-b2b-code-samples.md).

### <a name="how-can-i-customize-my-invitation-emails"></a>My davet e-postaları nasıl özelleştirebilir miyim?
Merhaba davet eden işlemiyle ilgili neredeyse her şeyi hello kullanarak özelleştirebileceğiniz [B2B davet API'leri](active-directory-b2b-api.md).

### <a name="can-an-invited-external-user-leave-hello-organization-after-being-invited"></a>Davet edilen bir dış kullanıcı davet edilen sonra hello kuruluş bırakabilirsiniz?
Hello davet kuruluş yönetici kullanıcıların dizinden B2B işbirliği Konuk kullanıcı silebilir, ancak hello Konuk kullanıcı kuruluş dizin başlarına davet hello bırakamazsınız. 

### <a name="can-guest-users-reset-their-multi-factor-authentication-method"></a>Konuk kullanıcılar kendi çok faktörlü kimlik doğrulama yöntemini sıfırlayabilir?
Evet. Konuk kullanıcılar aynı şekilde normal kullanıcıların yapın, çok faktörlü kimlik doğrulama yöntemi hello sıfırlayabilirsiniz.

### <a name="which-organization-is-responsible-for-multi-factor-authentication-licenses"></a>Hangi bir kuruluş için çok faktörlü kimlik doğrulaması lisans sorumlu mu?
Merhaba davet kuruluş çok faktörlü kimlik doğrulaması gerçekleştirir. Kuruluş davet hello hello kuruluş çok faktörlü kimlik doğrulaması kullanan kendi B2B kullanıcıları için yeterince lisansa sahip olduğundan emin olmanız gerekir.

### <a name="what-if-a-partner-organization-already-has-multi-factor-authentication-set-up-can-we-trust-their-multi-factor-authentication-and-not-use-our-own-multi-factor-authentication"></a>Ne zaten bir iş ortağı kuruluşta çok faktörlü kimlik doğrulamasını ayarlamak var? Biz, çok faktörlü kimlik doğrulama güven ve kullanabilirsiniz kendi çok faktörlü kimlik doğrulamasını kullanmamak?
Bu özellik, sonra da, belirli iş ortakları tooexclude (Merhaba davet kuruluşunuzun) çok faktörlü kimlik doğrulamasını seçebilmeniz için gelecekteki bir sürümde planlanmaktadır.

### <a name="how-can-i-use-delayed-invitations"></a>Gecikmeli davetleri nasıl kullanabilir miyim?
Bir kuruluş tooadd B2B işbirliği kullanıcıların istediğiniz, onları gerektiği şekilde tooapplications sağlamak ve Davetleri Gönder. Merhaba B2B işbirliği davet API toocustomize hello ekleme iş akışı kullanabilirsiniz.

### <a name="can-i-make-a-guest-user-a-limited-administrator"></a>Konuk kullanıcı sınırlı bir yönetici hale getirebilir?
Kesinlikle. Daha fazla bilgi için bkz: [ekleme Konuk kullanıcılar tooa rolü](active-directory-users-assign-role-azure-portal.md).

### <a name="does-azure-ad-b2b-collaboration-allow-b2b-users-tooaccess-hello-azure-portal"></a>Azure AD B2B işbirliği B2B kullanıcılar tooaccess hello Azure portal izin veriyor mu?
Merhaba sınırlı Yöneticisi veya genel Yönetici rolüne atanmış bir kullanıcı sürece, B2B işbirliği kullanıcıların erişim toohello Azure portal gerektiren olmaz. Ancak, hello sınırlı Yöneticisi veya genel Yönetici rolüne atanan B2B işbirliği kullanıcıların hello portala erişebilirsiniz. Bu yönetici rollerini atanmadı bir Konuk kullanıcı hello portal erişirse, ayrıca, hello kullanıcı mümkün tooaccess belirli bölümlerini olabilir hello deneyimi. Merhaba Konuk kullanıcı rolü hello Directory'de bazı izinlere sahip.

### <a name="can-i-block-access-toohello-azure-portal-for-guest-users"></a>Erişim toohello Konuk kullanıcılar için Azure portalı engelleyebilir miyim?
Evet! Bu ilkeyi yapılandırırken dikkatli tooavoid yanlışlıkla engelleme erişim toomembers ve yöneticileri olabilir.
tooblock Konuk kullanıcıya ait toohello erişim [Azure portal](https://portal.azure.com), koşullu erişim ilkesi hello Windows Azure Klasik dağıtım modeli API kullanın:
1. Merhaba değiştirme **tüm kullanıcılar** yalnızca üyeleri içeren grup.
  ![Merhaba Grup ekran değiştirme](media/active-directory-b2b-faq/modify-all-users-group.png)
2. Konuk kullanıcılar içeren dinamik bir grup oluşturun.
  ![Grup ekran oluşturma](media/active-directory-b2b-faq/group-with-guest-users.png)
3. Merhaba portal erişimini bir koşullu erişim ilkesi tooblock Konuk kullanıcılar video hello aşağıda gösterildiği gibi ayarlayın:
  
  > [!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-block-guest-user/Player] 

### <a name="does-azure-ad-b2b-collaboration-support-multi-factor-authentication-and-consumer-email-accounts"></a>Azure AD B2B işbirliği, çok faktörlü kimlik doğrulaması ve tüketici e-posta hesaplarına destekliyor mu?
Evet. Çok faktörlü kimlik doğrulama ve tüketici e-posta hesaplarına hem de Azure AD B2B işbirliği için desteklenir.

### <a name="do-you-plan-toosupport-password-reset-for-azure-ad-b2b-collaboration-users"></a>Toosupport parola sıfırlama için Azure AD B2B işbirliği kullanıcılar planlıyor musunuz?
Evet. Bir iş ortağı kuruluştan davet B2B kullanıcı için Self Servis parola sıfırlama (SSPR) için hello önemli ayrıntıları aşağıdadır:
 
* SSPR yalnızca hello kimlik kiracısında hello B2B kullanıcının oluşur.
* Merhaba kimlik Kiracı bir Microsoft hesabı ise, Microsoft hesabı SSPR mekanizması hello kullanılır.
* Merhaba kimlik Kiracı bir tam zamanında (JIT) veya "viral" Kiracı, bir parola sıfırlama e-posta gönderilir.
* Diğer kiracıları için B2B kullanıcılar için hello standart SSPR süreç izlenir. Üye SSPR hello kaynak hello bağlamında B2B kullanıcılar gibi Kiracı engellendi. 

### <a name="is-password-reset-available-for-guest-users-in-a-just-in-time-jit-or-viral-tenant-who-accepted-invitations-with-a-work-or-school-email-address-but-who-didnt-have-a-pre-existing-azure-ad-account"></a>Parolayı bir tam zamanında (JIT) Konuk kullanıcılar için kullanılabilir sıfırlamak veya "viral" Kiracı kabul davetleri bir iş veya Okul e-posta adresi, ancak önceden var olan bir Azure AD hesabının sahip oldu?
Evet. Bir kullanıcı tooreset hello JIT Kiracı parolalarını izin veren bir parola sıfırlama posta gönderilebilir.

### <a name="does-microsoft-dynamics-crm-provide-online-support-for-azure-ad-b2b-collaboration"></a>Microsoft Dynamics CRM online desteği için Azure AD B2B işbirliği sağlar?
Şu anda, Microsoft Dynamics CRM, Azure AD B2B işbirliği için çevrimiçi destek sağlamaz. Ancak, biz toosupport bu hello gelecekteki planlayın.

### <a name="what-is-hello-lifetime-of-an-initial-password-for-a-newly-created-b2b-collaboration-user"></a>Yeni oluşturulan B2B işbirliği kullanıcı için bir başlangıç parolası hello ömrü nedir?
Azure AD sabit dizi karakter, parola gücünü ve eşit olarak tooall Azure AD bulut kullanıcı hesapları geçerli hesap kilitleme gereksinimleri vardır. Bulut kullanıcı hesaplarıdır başka bir kimlik sağlayıcısıyla gibi Federasyon olmayan hesaplar 
* Microsoft hesabı
* Facebook
* Active Directory Federasyon Hizmetleri
* Başka bir bulut Kiracı (için B2B işbirliği)

Federasyon hesaplar için parola ilkesi hello şirket içi kiralama ve hello kullanıcının Microsoft hesap ayarlarını uygulanan hello İlkesi bağlıdır.

### <a name="an-organization-might-want-toohave-different-experiences-in-their-applications-for-tenant-users-and-guest-users-is-there-standard-guidance-for-this-is-hello-presence-of-hello-identity-provider-claim-hello-correct-model-toouse"></a>Bir kuruluş, Kiracı ve Konuk kullanıcılar için kendi uygulamalarında toohave farklı karşılaştığında isteyebilirsiniz. Bu standart yönergeler var mı? Merhaba kimlik sağlayıcısı talep hello doğru model toouse Hello varlığını mi?
 Konuk kullanıcı bir kimlik sağlayıcısı tooauthenticate kullanabilirsiniz. Daha fazla bilgi için bkz: [B2B işbirliği kullanıcının özelliklerini](active-directory-b2b-user-properties.md). Kullanım hello **UserType** özelliği toodetermine kullanıcı deneyimi. Merhaba **UserType** talep şu anda eklenmedi hello belirteç. Uygulamaları hello grafik API'si tooquery hello dizin hello kullanıcı ve tooget hello UserType için kullanmanız gerekir.

### <a name="where-can-i-find-a-b2b-collaboration-community-tooshare-solutions-and-toosubmit-ideas"></a>Çözümleri B2B işbirliği topluluk tooshare nereden bulabilirim ve toosubmit fikirler?
Biz sürekli tooyour geri bildirim, tooimprove B2B işbirliği dinliyor. Kullanıcı, tooshare davet ediyoruz senaryoları, en iyi yöntemler ve Azure AD B2B işbirliği hakkında ister. Merhaba tartışma hello katılma [Microsoft teknik topluluk](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).
 
Ayrıca, toosubmit fikir ve oy gelecekteki özellikleri için davet ediyoruz [B2B işbirliği fikirleri](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B-Ideas/idb-p/AzureAD_B2B_Ideas).

### <a name="can-we-send-an-invitation-that-is-automatically-redeemed-so-that-hello-user-is-just-ready-toogo-or-does-hello-user-always-have-tooclick-through-toohello-redemption-url"></a>Otomatik olarak kullanılan, kullanıcı hello kitabıdır, yalnızca toogo "hazır" davetiye gönderebiliriz? Veya hello kullanıcı her zaman toohello kullanım URL yoluyla tooclick sahip mi?
Merhaba da hello ortağı kuruluştaki bir üyesi olan Kuruluş davet bir kullanıcı tarafından gönderilen davetleri hello B2B kullanıcı tarafından kullanım gerektirmez.

Bir kullanıcıdan hello iş ortağı kuruluş toojoin hello kuruluş davet davet öneririz. [Bu kullanıcı toohello Konuk davet eden rolünü hello kaynak kuruluşta eklemek](active-directory-b2b-add-guest-to-role.md). Merhaba oturum açma kullanarak hello iş ortağı kuruluştaki diğer kullanıcılar bu kullanıcı davet edebilirsiniz UI, PowerShell komut dosyaları veya API'leri. Ardından, B2B işbirliği kullanıcıların belirli bir kuruluş kendi davetleri gerekli tooredeem değil.

### <a name="how-does-b2b-collaboration-work-when-hello-invited-partner-is-using-federation-tooadd-their-own-on-premises-authentication"></a>Davet hello iş ortağı Federasyon tooadd kendi şirket içi kimlik doğrulaması kullanılırken, B2B işbirliğinin nasıl çalışır?
Merhaba iş ortağı Federasyon bir Azure AD kiracısı varsa toohello şirket içi kimlik doğrulaması altyapısı, şirket içi çoklu oturum açma (SSO) otomatik olarak sağlanır. Merhaba ortak bir Azure AD Kiracı yoksa, yeni kullanıcılar için bir Azure AD hesabı oluşturulur. 

### <a name="i-thought-azure-ad-b2b-didnt-accept-gmailcom-and-outlookcom-email-addresses-and-that-b2c-was-used-for-those-kinds-of-accounts"></a>I, Azure AD B2B gmail.com ve outlook.com e-posta adresleri kabul etmediğiniz ve B2C bu hesap türü için kullanılan zorlayıcı?
Biz hello farklarını B2B ve iş şirket (B2C) işbirliği açısından kimlikleri desteklenen kaldırmış olursunuz. kullanılan hello kimliği B2B veya B2C kullanarak arasında iyi neden toochoose değil. İşbirliği seçeneğinizi seçme hakkında daha fazla bilgi için bkz: [karşılaştırmak B2B işbirliği ve Azure Active Directory B2C](active-directory-b2b-compare-b2c.md).

### <a name="what-applications-and-services-support-azure-b2b-guest-users"></a>Hangi uygulamaların ve hizmetlerin Azure B2B Konuk kullanıcılar destekliyor?
Tüm Azure AD ile tümleşik uygulamalar Azure B2B Konuk kullanıcılar destekler. 

### <a name="can-we-force-multi-factor-authentication-for-b2b-guest-users-if-our-partners-dont-have-multi-factor-authentication"></a>Çok faktörlü kimlik doğrulaması ortaklarımızın yoksa biz B2B Konuk kullanıcılar için çok faktörlü kimlik doğrulamasını zorlayabilir miyim?
Evet. Daha fazla bilgi için bkz: [B2B işbirliği kullanıcılar için koşullu erişim](active-directory-b2b-mfa-instructions.md).

### <a name="in-sharepoint-you-can-define-an-allow-or-deny-list-for-external-users-can-we-do-this-in-azure"></a>SharePoint'te dış kullanıcılar için bir "izin ver" veya "Reddet" listesi tanımlayabilirsiniz. Azure'da biz bunu yapabilirsiniz?
Evet. Azure AD B2B işbirliği destekler listeleri izin verme ve reddetme listelerini. 

### <a name="what-licenses-do-we-need-toouse-azure-ad-b2b"></a>Lisansları ne toouse Azure AD B2B ihtiyacımız var?
Azure AD B2B toouse ne kuruluşunuz lisansları hakkında bilgi gerekiyor için bkz: [Kılavuzu lisans Azure Active Directory B2B işbirliği](active-directory-b2b-licensing.md).

### <a name="next-steps"></a>Sonraki adımlar

Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:

* [Azure AD B2B işbirliği nedir?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Yöneticileri Azure AD B2B işbirliği kullanıcıların nasıl eklenir?](active-directory-b2b-admin-add-users.md)
* [Bilgi çalışanları B2B işbirliği kullanıcıların nasıl eklenir?](active-directory-b2b-iw-add-users.md)
* [Merhaba B2B işbirliği davet e-posta Hello öğeleri](active-directory-b2b-invitation-email.md)
* [B2B işbirliği davet kullanım](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B işbirliği lisanslama](active-directory-b2b-licensing.md)
* [Azure AD B2B işbirliği sorunlarını giderme](active-directory-b2b-troubleshooting.md)
* [Azure AD B2B işbirliği API ve özelleştirme](active-directory-b2b-api.md)
* [B2B işbirliği kullanıcıları için çok faktörlü kimlik doğrulaması](active-directory-b2b-mfa-instructions.md)
* [B2B işbirliği kullanıcıları davet olmadan ekleme](active-directory-b2b-add-user-without-invite.md)
* [Azure AD'de uygulama yönetimi için makale dizini](active-directory-apps-index.md)
