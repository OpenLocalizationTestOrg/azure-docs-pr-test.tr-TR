---
title: Azure Active Directory ile aaaHow tooIntegrate | Microsoft Docs
description: "Kılavuzu toobenefits ve Azure Active Directory ile tümleştirme için kaynaklar."
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: d13bba54-96bd-4b81-bee9-c8025ffa1648
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 4542965ae4a7756eda9f57e9e895f8044892f20e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-with-azure-active-directory"></a>Azure Active Directory ile tümleştirme
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure Active Directory, bulut uygulamaları için kurumsal düzeyde kimlik yönetimi kuruluşlarla sağlar.  Azure AD tümleştirme, kullanıcılarınızın kolaylaştırılmış bir oturum açma deneyimi sağlar ve uygulamanızı tooIT İlkesi uygun yardımcı olur.

## <a name="how-toointegrate"></a>Nasıl tooIntegrate
Azure AD ile uygulama toointegrate için birkaç yolu vardır.  Birçok veya uygulamanız için uygun olduğu şekilde bu senaryoların az sayıda olarak yararlanın.

### <a name="support-azure-ad-as-a-way-toosign-in-tooyour-application"></a>Bir şekilde tooSign olarak Azure AD tooYour uygulama desteği
**Oturum açma uyuşmazlık ve destek maliyetlerini azaltmak.** Azure AD toosign tooyour uygulamada kullanarak, kullanıcılarınızın daha fazla bir adı ve parola tooremember olmayacaktır.  Bir geliştirici olarak, daha az bir parola toostore sahip ve koruyun.  Unutulan toohandle parola sıfırlama olmaması önemli tasarruf tek başına olabilir.  Azure AD oturum açma bazı Office 365 ve Microsoft Azure gibi hello dünyanın en popüler bulut uygulamaları için çalıştırır.  Milyonlarca yüzlerce kuruluşlar milyonlarca kullanıcılardan, olasılığı olan kullanıcı tooAzure AD zaten oturum.  Daha fazla bilgi edinmek [Azure AD oturum açma için destek ekleyen](active-directory-authentication-scenarios.md).

**Oturum, uygulamanız için yukarı basitleştirin.**  Böylece form kaydolma önceden doldurun veya tamamen ortadan kaydolma sırasında uygulamanız için Azure AD kullanıcı hakkındaki temel bilgileri gönderebilirsiniz.  Kullanıcılar kendi Azure AD hesabının sosyal medya ve mobil uygulamaları bulunan tanıdık onayı deneyimi benzer bir toothose aracılığıyla kullanarak uygulamanız için kaydolabilirsiniz.  Herhangi bir kullanıcı, kaydolma ve BT katılımı gerek kalmadan Azure AD ile tümleşik tooan uygulamada oturum açma.  Daha fazla bilgi edinmek [uygulamanızı Azure AD hesabının oturum açma için kaydolduğunuz](../../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).

### <a name="browse-for-users-manage-user-provisioning-and-control-access-tooyour-application"></a>Kullanıcılar, kullanıcı sağlama yönetmek ve erişimi denetleme tooYour uygulama Gözat
**Merhaba dizin kullanıcılar için göz atın.**  Hello grafik API'si toohelp kullanıcıları arama ve göz atma kuruluşlarındaki diğer kişiler için başkalarının davet olduğunda kullanın veya bunları gerektirmek yerine, tootype erişim e-posta adresi.  Kullanıcılar hello kuruluş hiyerarşisi hello ayrıntılarını görüntüleme dahil olmak üzere bir bilinen adres defteri stili arabirimini kullanarak göz atabilir.  Merhaba hakkında daha fazla bilgi [grafik API'si](active-directory-graph-api.md).

**Active Directory grupları ve dağıtım listeleri müşteri zaten yönetme yeniden kullanır.**  Azure AD müşteri zaten e-posta dağıtım için kullanarak ve erişim yönetimi hello gruplarını içerir.  Merhaba grafik API'sini kullanarak, müşteri toocreate gerektirmek yerine bu grupları yeniden kullanma ve grupları, uygulamanızda ayrı bir dizi yönetin.  Grup bilgileri oturum açma simgeleri ın tooyour uygulama da gönderilebilir.  Merhaba hakkında daha fazla bilgi [grafik API'si](active-directory-graph-api.md).

**Access tooyour uygulaması olan Azure AD toocontrol kullanın.**  Yöneticiler ve uygulama sahipleri Azure AD'de erişim tooapplications toospecific kullanıcıları ve grupları atayabilirsiniz.  Merhaba grafik API'sini kullanarak, bu liste okuyabilir ve toocontrol sağlama ve kaynakları sağlamayı kaldırma özelliklerini kullanın ve uygulamanızdaki erişim.

**Tabanlı erişim denetimi rolleri için Azure AD kullanın.**  Yöneticiler ve uygulama sahipleri, kullanıcılar ve Azure AD içinde uygulamanızı kaydederken tanımladığınız grupları tooroles atayabilirsiniz.  Rol bilgilerini tooyour uygulama oturum açma belirteçleri gönderilir ve ayrıca hello grafik API'sini kullanarak okunabilir.  Daha fazla bilgi edinmek [yetkilendirme için Azure AD kullanarak](http://blogs.technet.com/b/ad/archive/2014/12/18/azure-active-directory-now-with-group-claims-and-application-roles.aspx).

### <a name="get-access-toousers-profile-calendar-email-contacts-files-and-more"></a>Erişim tooUser'ın profili, takvim, e-posta, kişiler, dosyaları ve daha fazla bilgi alın
**Azure AD, Office 365 için hello yetkilendirme sunucusu ve diğer Microsoft iş Hizmetleri ' dir.**  Oturum açma tooyour uygulama veya OAuth 2.0 kullanan geçerli kullanıcı hesapları tooAzure AD kullanıcı hesaplarınızı bağlama desteği için Azure AD destekliyorsa, okuma ve yazma erişimi tooa kullanıcının profili, takvim, e-posta, kişiler, dosyaları ve diğer bilgileri isteyebilir.  Sorunsuz bir şekilde olayları toouser'ın takvim, yazma ve da okuma veya yazma dosyaları tootheir OneDrive.  Daha fazla bilgi edinmek [erişme hello Office 365 API'leri](https://msdn.microsoft.com/office/office365/howto/platform-development-overview).

### <a name="promote-your-application-in-hello-azure-and-office-365-marketplaces"></a>Hello Azure uygulamanız ve Office 365 Pazar Yükselt
**Azure AD zaten kullanan kuruluşların, uygulama toohello milyonlarca yükseltin.**  Arama ve bu Pazar Gözat kullanıcılar bir zaten kullanıyor veya Bulut hizmeti müşteriler bunları yaparak daha fazla bulut hizmeti yetkili.  Uygulamanızda yükseltme hakkında daha fazla bilgi [Azure Marketi hello](https://azure.microsoft.com/marketplace/partner-program/).

**Kullanıcılar, uygulamanız için kaydolduğunuzda, kendi Azure AD erişim paneli ve Office 365 uygulama Başlatıcı görünür.**  Kullanıcıların mümkün tooquickly ve kolayca dönüş tooyour uygulamayı daha sonra kullanıcı etkileşimini geliştirme olacaktır.  Merhaba hakkında daha fazla bilgi [Azure AD erişim paneli](../active-directory-saas-access-panel-introduction.md).

### <a name="secure-device-to-service-and-service-to-service-communication"></a>Aygıt hizmeti ve hizmet iletişimin güvenliğini sağlama
**Azure AD için Kimlik Yönetimi Hizmetleri ve cihazların kullanarak toowrite gerekir ve BT toomanage erişim sağlayan hello kodu azaltır.**  Hizmetler ve cihazlar, OAuth kullanan Azure AD'den belirteçleri almak ve bu belirteçleri tooaccess web API'leri kullanın.  Azure AD kullanarak karmaşık kimlik doğrulama kodu yazma önleyebilirsiniz.  Azure AD'de hello Hizmetleri ve cihazların Merhaba kimlikleri depolandığından BT anahtarları ve iptal etmeyi toodo bu ayrı olarak uygulamanızda sahip olmak yerine tek bir yerde yönetebilirsiniz.

## <a name="benefits-of-integration"></a>Tümleştirme yararları
Azure AD ile tümleştirme toowrite ek kod gerektirmeyen yararları ile birlikte gelir.

### <a name="integration-with-enterprise-identity-management"></a>Kurumsal kimlik yönetimi ile tümleştirme
**BT ilkelerine uygun uygulamanızı yardımcı olur.**  Kuruluşlar, Kurumsal kimlik yönetimi sistemlerini Azure AD ile tümleştirmek bir kişi bir kuruluş ayrıldığında, otomatik olarak erişim tooyour uygulama BT tootake gerek olmadan ek adımlar kaybederler şekilde.  BT, uygulamanızın erişebilecek ve hangi erişim ilkeleri - örnek çok faktörlü kimlik doğrulama, gerek toowrite kod toocomply karmaşık şirket ilkeleriyle azaltma - gerektiğini belirlemek yönetebilirsiniz.  Azure AD kimin tooyour uygulamada şekilde imzalanmış, ayrıntılı denetim günlüğü yöneticilerine sağlar BT kullanımını izleyebilirsiniz.

**Böylece uygulamanız AD ile tümleştirebilirsiniz azure AD Active Directory toohello bulut genişletir.**  Merhaba Dünya birçok kuruluş kendi asıl oturum açma ve kimlik yönetimi sistemi Active Directory'yi kullanmak ve bunların uygulamaları toowork AD ile gerektirir.  Azure AD ile tümleştirme, uygulamanızın Active Directory ile tümleştirir.

### <a name="advanced-security-features"></a>Gelişmiş güvenlik özellikleri
**Çok faktörlü kimlik doğrulaması.**  Azure AD yerel çok faktörlü kimlik doğrulaması sağlar.  Böylece toocode Bu destek kendiniz elinizde BT yöneticileri, uygulamanızın çok faktörlü kimlik doğrulaması tooaccess gerektirebilir.  Daha fazla bilgi edinmek [çok faktörlü kimlik doğrulaması](https://azure.microsoft.com/documentation/services/multi-factor-authentication/).

**Anormal oturum açma algılama.**  Azure AD işleyen bir milyardan fazla oturum açma işlemleri makine kullanırken günde algoritmaları toodetect şüpheli etkinlik öğrenme ve olası sorunları, BT yöneticilerinin uyar.  Azure AD oturum açma destekleyerek, uygulamanız bu koruma hello yararı alır. Daha fazla bilgi edinmek [Azure Active Directory erişimi raporu görüntüleme](../active-directory-view-access-usage-reports.md).

**Koşullu erişim.**  Ayrıca toomulti faktörlü kimlik doğrulaması, yöneticiler gerektirebilir belirli koşullar, kullanıcıların oturum açma önce getirilmesi tooyour uygulama.  Ayarlanabilir koşullar hello IP adresi aralığı, istemci cihazlar, üyelik belirtilen grupların ve erişim için kullanılan hello aygıt hello durumunu içerir.  Daha fazla bilgi edinmek [Azure Active Directory koşullu erişim](../active-directory-conditional-access.md).

### <a name="easy-development"></a>Kolay geliştirme
**Endüstri standardı protokoller.**  Microsoft kaydedilmiş toosupporting endüstri standartları ' dir.  Azure AD hello SAML 2.0, Openıd Connect 1.0, OAuth 2.0 ve WS-Federasyon 1.2 kimlik doğrulama protokollerini destekler.  Merhaba grafik API'si OData 4.0 uyumlu değil.  Uygulamanız zaten hello SAML 2.0 veya Openıd Connect 1.0 protokollerini federe oturum açma için destekliyorsa, Azure AD için destek ekleyen basit olabilir.  Daha fazla bilgi edinmek [Azure AD kimlik doğrulama protokolleri desteklenen](active-directory-authentication-protocols.md).

**Açık kaynak kitaplıkları.**  Microsoft, popüler diller ve platformlar toospeed geliştirme için tam olarak desteklenen açık kaynak kitaplıkları sağlar.  Merhaba kaynak kodu Apache 2.0 altında lisanslanmıştır ve ücretsiz toofork olan ve geri toohello projeleri katkıda.  Daha fazla bilgi edinmek [Azure AD kimlik doğrulama kitaplıkları](active-directory-authentication-libraries.md).

### <a name="worldwide-presence-and-high-availability"></a>Dünya çapında varlığı ve yüksek kullanılabilirlik
**Azure AD Merhaba Dünya veri merkezlerinde dağıtılır ve yönetilen ve başlangıç saati izlenen.**  Azure AD, Microsoft Azure ve Office 365 için hello Kimlik Yönetimi sistemidir ve Merhaba Dünya 28 veri merkezlerinde dağıtılır.  Dizin verilerini çoğaltılan toobe tooat en az üç veri merkezleri garanti edilmez.  Genel yük dengeleyici hello en yakın Azure AD verilerini içeren kopyasını kullanıcıların erişim ve bir sorun algılandığında, otomatik olarak yeniden yönlendirmek tooother veri merkezleri istekleri emin olun.

## <a name="next-steps"></a>Sonraki Adımlar
[Kod yazmaya başlamak](active-directory-developers-guide.md#get-started).

[Azure AD kullanarak kullanıcıların oturumunu](active-directory-authentication-scenarios.md)

