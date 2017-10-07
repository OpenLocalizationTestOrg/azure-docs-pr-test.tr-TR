---
title: "aaaAzure güvenlik özellikleri Kimlik Yönetimi ile ilgili Yardım | Microsoft Docs"
description: " Bu makalede Identity management ile Yardım hello çekirdek Azure güvenlik özelliklerine genel bakış sağlar. Microsoft kimlik ve erişim yönetimi çözümlerini Yardım BT erişim tooapplications ve kaynakları hello kurumsal veri merkezi genelinde ve hello buluta doğrulama çok faktörlü kimlik doğrulama ve koşullu gibi ek düzeylerini etkinleştirme koruma erişim ilkeleri. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 5aa0a7ac-8f18-4ede-92a1-ae0dfe585e28
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: terrylan
ms.openlocfilehash: f08e4f6cf2e48e455a16858b7fee08b53d5aa585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-identity-management-security-overview"></a>Azure Kimlik Yönetimi güvenliğine genel bakış
Microsoft kimlik ve erişim yönetimi çözümlerini Yardım BT erişim tooapplications ve kaynakları hello kurumsal veri merkezi genelinde ve hello buluta doğrulama çok faktörlü kimlik doğrulama ve koşullu gibi ek düzeylerini etkinleştirme koruma erişim ilkeleri. Raporlama, Denetim ve yardımcı olası güvenlik sorunlarını azaltmak uyarı Gelişmiş Güvenlik ile izleme şüpheli etkinlik. [Azure Active Directory Premium](../active-directory/active-directory-editions.md) bulut (SaaS) uygulamaların ve şirket içi çalıştırdığınız erişim tooweb uygulamaların tek oturum açma toothousands sağlar.

Güvenlik, Azure Active Directory (AD) hello yeteneği yararları:

* Oluşturma ve kullanıcılara, gruplara ve cihazlara eşitlenmiş şekilde kalmasının, karma kuruluşunuzda her kullanıcı için tek bir kimliği yönetme
* Önceden tümleştirilmiş SaaS uygulamaları binlerce dahil olmak üzere tooyour uygulamalar tek oturum açma erişim sağlamak
* Uygulama erişimi güvenliğini kural tabanlı çok faktörlü kimlik doğrulamasını hem şirket içi zorlayarak etkinleştirmek ve bulut uygulamalarında
* Sağlama güvenli uzaktan erişim tooon içi web uygulamaları Azure AD uygulama proxy'si aracılığıyla

Merhaba, bu makalenin tooprovide Identity management ile Yardım hello çekirdek Azure güvenlik özelliklerine genel bakış hedeftir. Daha fazla bilgi için her bir özelliğin ayrıntılarını veren bağlantılar tooarticles de sunuyoruz.  

Merhaba makale çekirdek Azure kimlik yönetimi özelliklerini aşağıdaki hello üzerinde odaklanır:

* Çoklu oturum açma
* Ters proxy
* Multi-factor authentication
* Güvenlik İzleme, uyarılar ve makine öğrenme tabanlı raporlar
* Tüketici kimliği ve erişim yönetimi
* Cihaz kaydı
* Ayrıcalıklı Kimlik Yönetimi
* Kimlik koruması
* Karma Kimlik Yönetimi

## <a name="single-sign-on"></a>Çoklu oturum açma
Çoklu oturum açma (SSO) mümkün tooaccess olan tüm hello uygulamaları ve yalnızca bir kez tek bir kullanıcı hesabı kullanarak oturum açma tarafından toodo iş ihtiyacınız kaynakları anlamına gelir. Oturum açıldıktan sonra tüm gerekli tooauthenticate olmadan gereksinim duyduğunuz hello uygulamaları erişebilirsiniz (örneğin, bir parola yazın) ikinci kez.

Birçok kuruluş yazılım için son kullanıcı üretkenliğini Office 365, kutusunu ve Salesforce gibi bir hizmet (SaaS) uygulamaları olarak kullanır. Tarihsel olarak, BT personeli gerekli tooindividually oluşturun ve her SaaS uygulamasının kullanıcı hesaplarında güncelleştirin ve kullanıcıların her SaaS uygulaması için bir parola tooremember gerekiyordu.

Azure AD şirket içi Active Directory hello bulut ortamlarına kullanıcılar toouse etkinleştirme birincil kuruluş hesabı kendi toonot yalnızca oturum açma tootheir etki alanına katılmış aygıtlar ve şirket kaynaklarına genişletir, ancak aynı zamanda tüm web ve SaaS uygulamaları hello işlerini için gerekli.

Yalnızca kullanıcıların birden çok kullanıcı adları ve parolalar kümesini toomanage sahip değilse, uygulama erişimini otomatik olarak sağlanan veya XML'deki sağlanan dayalı olarak kuruluş grupları ve durumlarını çalışan olarak olabilir. Azure AD güvenlik tanıtır ve, toocentrally etkinleştirmek erişim İdaresi denetimleri SaaS uygulamaları arasında kullanıcıların erişimini yönetin.

Daha fazla bilgi edinin:

* [Çoklu oturum açma genel bakış](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](../active-directory/active-directory-appssoaccess-whatis.md)
* [Azure Active Directory çoklu oturum açma SaaS uygulamaları ile tümleştirme](../active-directory/active-directory-sso-integrate-saas-apps.md)

## <a name="reverse-proxy"></a>Ters proxy
Azure AD uygulama proxy'si sağlar, şirket içi uygulamalar gibi yayımlama [SharePoint](https://support.office.com/article/What-is-SharePoint-97b915e6-651b-43b2-827d-fb25777f446f?ui=en-US&rs=en-US&ad=US) siteler, [Outlook Web App](https://technet.microsoft.com/library/jj657718.aspx), ve [IIS](http://www.iis.net/)-tabanlı uygulamalar özel ağınızdan ve ağınızın dışından güvenli erişim toousers sağlar. Uygulama Ara sunucusu, uzaktan erişim sağlar ve çoklu oturum açma (SSO) birçok türden hello binlerce ile web uygulamaları Azure AD destekleyen SaaS uygulamalarının şirket. Çalışanlar tooyour uygulamalardan oturum açabildiğinden ev kendi cihazlarda ve bu bulut tabanlı proxy üzerinden kimlik doğrulaması.

Daha fazla bilgi edinin:

* [Azure AD uygulama ara sunucusunu etkinleştirme](../active-directory/active-directory-application-proxy-enable.md)
* [Azure AD uygulama proxy'si ile uygulama yayımlama](../active-directory/active-directory-application-proxy-publish.md)
* [Çoklu oturum açma uygulama proxy'si ile uygulama](../active-directory/active-directory-application-proxy-sso-using-kcd.md)
* [Koşullu erişim ile çalışma](../active-directory/active-directory-application-proxy-conditional-access.md)

## <a name="multi-factor-authentication"></a>Multi-factor authentication
Azure çok faktörlü kimlik doğrulaması (MFA) hello birden fazla doğrulama yöntemi kullanılmasını gerektiren ve güvenlik toouser oturum açmalarına ve işlemlerine önemli bir ikinci katmanı ekleyen kimlik doğrulama yöntemidir. MFA basit bir oturum açma işlemi için kullanıcı talebine buluştururken koruma erişim toodata ve uygulamaları yardımcı olur. Güçlü kimlik doğrulama seçeneklerini çeşitli aracılığıyla sunar — telefon araması, SMS mesajı veya mobil uygulama bildirimi veya doğrulama kodu ve üçüncü taraf OAuth belirteçleri.

Daha fazla bilgi edinin:

* [Multi-Factor Authentication](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [Azure Multi-Factor Authentication nedir?](../multi-factor-authentication/multi-factor-authentication.md)
* [Azure multi-Factor Authentication nasıl çalışır](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="security-monitoring-alerts-and-machine-learning-based-reports"></a>Güvenlik İzleme, uyarılar ve makine öğrenme tabanlı raporlar
Güvenlik İzleme ve uyarılar ve tutarsız erişim desenlerini tanımlamak makine öğrenme tabanlı raporlar, işinizin korunmasına yardımcı olabilir. Azure Active Directory'nin erişim ve kullanım raporları toogain görünürlük hello bütünlüğü ve güvenlik kuruluşunuzun dizininin kullanabilirsiniz. Bu bilgileri kullanarak bir dizin yönetici böylece bunlar yeterli bu riskleri toomitigate planlayabilirsiniz olası güvenlik riskleri burada bulunan daha iyi belirleyebilirsiniz.

Hello Klasik Azure portalı, raporları hello yolları aşağıdaki kategorilere ayrılır:

* Anomali raporları – oturum açma olayları toobe anormal bulduk olduğunu içerir. Amacımız toomake olduğundan, bu tür etkinliğini kullanan ve toobe mümkün toomake bir olay şüpheli olup olmadığı hakkında bir belirleme etkinleştirin.
* Tümleşik uygulama raporları – bulut uygulamalarını, kuruluşunuzda nasıl kullanıldığını içine Öngörüler sağlar. Azure Active Directory bulut uygulamalarını binlerce ile tümleştirme sağlar.
* Hata raporlarını – hesapları tooexternal uygulamaları sağlamada oluşabilecek hatalar gösterir.
* Kullanıcıya özgü raporları – belirli bir kullanıcı için etkinlik verilerdeki aygıt/oturum görüntüler.
* Etkinlik günlükleri – son 24 saat hello içindeki tüm Denetlenen olayları kaydını içermediğinden, son 7 gün veya son 30 gün ve Grup etkinlik değişikliklerini ve parola sıfırlama ve kayıt etkinliği.

Daha fazla bilgi edinin:

* [Erişim ve kullanım raporlarınızı görüntüleme](../active-directory/active-directory-view-access-usage-reports.md)
* [Azure Active Directory Raporlama ile çalışmaya başlama](../active-directory/active-directory-reporting-getting-started.md)
* [Azure Active Directory raporlama Kılavuzu](../active-directory/active-directory-reporting-guide.md)

## <a name="consumer-identity-and-access-management"></a>Tüketici kimliği ve erişim yönetimi
Azure Active Directory B2C kimlikleri milyonlarca toohundreds ölçeklendirilebilen bir yüksek oranda kullanılabilir, genel kimlik yönetimi tüketiciye yönelik uygulamalar için hizmetidir. Bu hizmet mobil platformlar ve web platformlarıyla tümleştirilebilir. Tüketicileriniz üzerinde tooall uygulamalarınızı özelleştirilebilir deneyimler aracılığıyla var olan sosyal hesaplarını kullanarak veya yeni kimlik bilgileri oluşturarak oturum açabilir.

Hello son, Yukarı toosign ve oturum açma tüketicilerin uygulamalarına isteyen uygulama geliştiricileri kendi kodlarını yazardı. Ve şirket içi veritabanlarını veya sistemleri toostore kullanıcı adları ve parolalar kullandığı. Azure Active Directory B2C, kuruluşunuzun bir daha iyi şekilde toointegrate tüketici kimlik yönetimini uygulamalarına hello Yardım güvenli, standartlara dayalı bir platform ve bir büyük Genişletilebilir ilke kümesi sunar.

Azure Active Directory B2C kullandığınızda tüketicileriniz uygulamalarınız için var olan sosyal hesaplarını (Facebook, Google, Amazon, LinkedIn) kullanarak veya yeni kimlik bilgileri (e-posta adresi ve parola veya kullanıcı adı ve parola) oluşturarak kaydolabilir.

Daha fazla bilgi edinin:

* [Azure Active Directory B2C nedir?](https://azure.microsoft.com/services/active-directory-b2c/)
* [Azure Active Directory B2C önizlemesi: oturum ayarlama ve tüketicilerinizin uygulamanıza oturum](../active-directory-b2c/active-directory-b2c-overview.md)
* [Azure Active Directory B2C önizlemesi: Uygulama türleri](../active-directory-b2c/active-directory-b2c-apps.md)

## <a name="device-registration"></a>Cihaz kaydı
Azure AD cihaz kaydı hello temeli olan aygıt tabanlı [koşullu erişim](../active-directory/active-directory-conditional-access-device-registration-overview.md) senaryoları. Bir cihaz kaydedildiğinde Azure Active Directory cihaz kaydı hello kullanıcı oturum açtığında kullanılan tooauthenticate hello aygıt olan bir kimliğe sahip hello cihazı sağlar. Kimliği doğrulanmış hello cihaz ve hello cihazın hello öznitelikleri hello bulutta ve şirket içi barındırılan uygulamalar için kullanılan tooenforce koşullu erişim ilkeleri olabilir.

Intune gibi bir mobil cihaz Yönetimi (MDM) çözümü ile birleştirildiğinde Azure Active Directory'de hello cihaz öznitelikleri hello cihaz hakkındaki ek bilgilerle güncelleştirilir. Bu, cihazları toomeet erişimden zorunlu toocreate koşullu erişim kuralları, güvenlik ve uyumluluğa yönelik standartlarınızı sağlar.

Daha fazla bilgi edinin:

* [Azure Active Directory cihaz kaydını kullanmaya başlama](../active-directory/active-directory-conditional-access-device-registration-overview.md)
* [Azure Active Directory için Windows etki alanına katılmış aygıtlar ile otomatik cihaz kaydı](../active-directory/active-directory-conditional-access-automatic-device-registration.md)
* [Windows otomatik kayıt Azure Active Directory ile etki alanına katılmış cihazları ayarlama](../active-directory/active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="privileged-identity-management"></a>Ayrıcalıklı Kimlik Yönetimi
Azure Active Directory (AD) Privileged Identity Management yönetmenize, denetlemenize ve Office 365 veya Microsoft Intune gibi diğer Microsoft online services yanı sıra ayrıcalıklı kimliklerinizi ve Azure ad erişim tooresources izlemenize olanak sağlar.

Bazen kullanıcıların Azure veya Office 365 kaynakları veya diğer SaaS uygulamaları ayrıcalıklı işlemleri çıkışı toocarry gerekir. Bu, genellikle kuruluşlar sahip toogive anlamına bunları kalıcı ayrıcalıklı erişim Azure AD'de. Kuruluşlar, yeterince yönetici ayrıcalıklarını bu kullanıcıların ne yaptıklarını izleyemez bulutta barındırılan kaynaklar için büyüyen bir güvenlik riski olmasıdır. Ayrıca, ayrıcalıklı erişimi olan bir kullanıcı hesabı ihlal edilmesi durumunda, bir ihlali, genel bulutun güvenlik etkileyebilir. Azure AD Privileged Identity Management tooresolve bu riski yardımcı olur.

Azure AD Privileged Identity Management sağlar:

* Hangi kullanıcıların Azure AD admins olduğuna bakın
* İsteğe bağlı, "Office 365 ve Intune yönetim erişimi tooMicrosoft çevrimiçi hizmetler gibi tam zamanında" etkinleştirme
* Yönetici erişim geçmişine ve değişiklikler hakkında raporlar yönetici atamaları alma
* Erişim tooa ayrıcalıklı rol hakkında uyarı alın

Daha fazla bilgi edinin:

* [Azure AD Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-configure.md)
* [Azure AD Privileged Identity Management rollerinde](../active-directory/active-directory-privileged-identity-management-roles.md)
* [Azure AD Privileged Identity Management: Nasıl tooadd veya bir kullanıcı rolünü kaldır](../active-directory/active-directory-privileged-identity-management-how-to-add-role-to-user.md)

## <a name="identity-protection"></a>Kimlik koruması
Azure AD kimlik koruması risk olaylarına ve olası güvenlik açıklarını kuruluşunuzdaki kimlikleri etkileyen birleştirilmiş bir görünüm sağlayan bir güvenlik hizmetidir. Kimlik koruma, var olan Azure Active Directory'nin (Azure AD anormal etkinlik raporları kullanılabilir) anomali algılama özelliklerinden yararlanır ve anormallikleri gerçek zamanlı olarak algılayabilir yeni risk olayı türleri sunar.

Daha fazla bilgi edinin:

* [Azure Active Directory kimlik koruması](../active-directory/active-directory-identityprotection.md)
* [Kanal 9: Azure AD ve kimlik göster: kimlik koruması Önizleme](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="hybrid-identity-management"></a>Karma Kimlik Yönetimi
Microsoft'un yaklaşımı tooidentity yayılma şirket içi ve hello bulut, tek bir kullanıcı kimliği kimlik doğrulama ve yetkilendirme için konum bağımsız olarak tooall kaynakları oluşturma.

Daha fazla bilgi edinin:

* [Karma kimlik teknik incelemesi](http://download.microsoft.com/download/D/B/A/DBA9E313-B833-48EE-998A-240AA799A8AB/Hybrid_Identity_White_Paper.pdf)
* [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)
* [Active Directory ekip blogu](https://blogs.technet.microsoft.com/ad/)
