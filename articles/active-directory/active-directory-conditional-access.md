---
title: "Merhaba Klasik Azure portalı aaaConditional Access'te | Microsoft Docs"
description: "Koşullu erişim denetimi için erişim tooapplications doğrulanırken için belirli koşullar hello Azure Klasik portalı toocheck kullanın."
services: active-directory
keywords: "koşullu erişim tooapps, Azure AD ile koşullu erişim toocompany kaynaklarına, koşullu erişim ilkeleri güvenli erişim"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: da3f0a44-1399-4e0b-aefb-03a826ae4ead
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.custom: oldportal
ms.openlocfilehash: 049bd3f6ec9e35479319ee7608b007b9a1e16647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-hello-azure-classic-portal"></a>Merhaba Klasik Azure portalı koşullu erişim

Bu konu, koşullu erişim hello Klasik Azure portalı hakkındadır. Merhaba en son hello Azure Active Directory içinde koşullu erişim hakkında bilgi için [Azure Active Directory'de koşullu erişim](active-directory-conditional-access-azure-portal.md).


Azure Active Directory (Azure AD) koşullu erişim denetimi özelliklerinden Hello hello Bulut ve şirket içi güvenli kaynaklarında toohelp basit yollar sunar. Çok faktörlü kimlik doğrulaması hello riskini karşı korunmasına yardımcı olabilirsiniz gibi koşullu erişim ilkeleri çalınması ve phished kimlik bilgileri. Diğer koşullu erişim ilkeleri, kuruluşunuzun verilerini korumanıza yardımcı olabilir. Örneğin, ayrıca toorequiring kimlik bilgileri, bir ilke Microsoft Intune, kuruluşunuzun hassas Hizmetleri erişebilir, bir mobil cihaz yönetim sisteminde kayıtlı yalnızca cihazların olabilir.

## <a name="prerequisites"></a>Ön koşullar
Azure AD koşullu erişim özelliğidir [Azure Active Directory Premium](http://www.microsoft.com/identity). Koşullu erişim ilkelerinin uygulandığı olan bir uygulama erişen her kullanıcı bir Azure AD Premium lisansına sahip olmalıdır. Lisans gereksinimleri hakkında daha fazla bilgiyi [lisanssız kullanıcı raporu](https://aka.ms/utc5ix).

## <a name="how-is-conditional-access-control-enforced"></a>Koşullu erişim denetimi nasıl uygulanır?
Yerinde koşullu erişim denetimi ile Azure AD, bir uygulama için kullanıcı tooaccess ayarladığınız hello belirli koşullarını denetler. Erişim gereksinimlerinin karşılandığını sonra hello kullanıcı kimlik doğrulaması ve hello uygulamasına erişebilir.  

![Koşullu erişim genel bakış](./media/active-directory-conditional-access/conditionalaccess-overview.png)

## <a name="conditions"></a>Koşullar
Bir koşullu erişim ilkesine dahil koşullar şunlardır:

* **Grup üyelikleri**. Bir grup içinde üyelik dayalı bir kullanıcının erişimi denetler.
* **Konum**. Başlangıç konumu hello kullanıcı tootrigger çok faktörlü kimlik doğrulaması kullanmak ve bir kullanıcı güvenilir bir ağ üzerinde olmadığında blok denetimleri kullanın.
* **Cihaz platformu**. İOS, Android, Windows Mobile veya Windows gibi Hello cihaz platformu ilkesi uygulamak için bir koşul olarak kullanın.
* **Aygıt etkin**. Cihaz durumu, etkin veya devre dışı, cihaz İlkesi değerlendirmesi sırasında doğrulanır. Merhaba dizininde kaybolan veya çalınan bir cihazın devre dışı bırakırsanız, artık ilke gereksinimlerini karşılayabilen.
* **Oturum açma ve kullanıcı riski**. Kullanabileceğiniz [Azure AD Identity Protection](active-directory-identityprotection.md) koşullu erişim risk ilkeleri için. Koşullu erişim risk ilkeleri risk olaylarına ve olağan dışı oturum açma etkinlikleri göre kuruluşun gelişmiş koruma sağlamak yardımcı olur.

## <a name="controls"></a>Denetimler
Bir koşullu erişim ilkesi tooenforce kullanabileceğiniz denetimleri şunlardır:

* **Çok faktörlü kimlik doğrulaması**. Çok faktörlü kimlik doğrulaması aracılığıyla güçlü kimlik doğrulamasını isteyebilirsiniz. Azure multi-Factor Authentication veya Active Directory Federasyon Hizmetleri (AD FS) ile birlikte bir şirket içi çok faktörlü kimlik doğrulama sağlayıcısı kullanarak çok faktörlü kimlik doğrulaması kullanabilirsiniz. Çok faktörlü kimlik doğrulamasını kullanarak erişim toohello geçerli bir kullanıcı kimlik bilgilerini elde etmiştir yetkisiz bir kullanıcı tarafından erişilen kaynaklar korunmasına yardımcı olur.
* **Blok**. Kullanıcı konumu tooblock kullanıcı erişimi gibi koşullar uygulayabilirsiniz. Örneğin, bir kullanıcı güvenilir bir ağ üzerinde olmadığında erişimi engelleyebilir.
* **Uyumlu cihazların**. Merhaba cihaz düzeyinde koşullu erişim ilkeleri ayarlayabilirsiniz. Yalnızca etki alanına katılmış olan bilgisayarları veya bir mobil cihaz Yönetimi uygulamasında kaydedilen Mobil cihazların kuruluşunuzdaki kaynaklara erişebilmesi için bir ilke ayarlayabilir. Örneğin, Intune toocheck cihaz uyumluluğu kullanın ve hello kullanıcı tooaccess uygulama çalıştığında tooAzure AD zorlama için rapor. Toouse Intune tooprotect uygulamaları ve verileri nasıl görürüm hakkında ayrıntılı yönergeler için [uygulamaları ve Microsoft Intune ile verileri koruma](https://docs.microsoft.com/intune/deploy-use/protect-apps-and-data-with-microsoft-intune). Intune tooenforce veri koruması kaybolan veya çalınan cihazlar için de kullanabilirsiniz. Daha fazla bilgi için bkz: [Microsoft Intune kullanarak tam veya seçmeli Temizleme ile verilerinizin korunmasına yardımcı olma](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).

## <a name="applications"></a>Uygulamalar
Merhaba uygulama düzeyinde bir koşullu erişim ilkesi zorunlu kılabilir. Uygulamaları ve Hizmetleri için erişim düzeylerini hello Bulut veya şirket içi ayarlayın. Merhaba uygulanan doğrudan toohello Web sitesi ya da hizmet ilkesidir. Hello İlkesi toohello tarayıcı erişimi ve hello hizmete erişim tooapplications için uygulanır.

## <a name="device-based-conditional-access"></a>Cihaz temelli koşullu erişim
Azure AD ile kayıtlı ve hangi belirli koşullara uyan cihazlardan erişim tooapplications kısıtlayabilirsiniz. Cihaz temelli koşullu erişim kuruluşun kaynakları tooaccess hello kaynaklardan denemesi kullanıcıların korur:

* Bilinmeyen veya yönetilmeyen cihazlar.
* Kuruluşunuz hello güvenlik ilkeleri uymayan cihazları ayarlayın.

Bu gereksinimlerine göre ilkeleri ayarlayabilirsiniz:

* **Etki alanına katılmış aygıtlar**. Şirket içi Active Directory etki alanına katılmış tooan olan ve Azure AD ile de kayıtlı bir ilke toorestrict erişim toodevices ayarlayın. Bu ilke tooWindows Masaüstü ve dizüstü bilgisayarlar ile Kurumsal tabletlerde uygulanır.
  Hakkında daha fazla bilgi için Azure AD ile etki alanına katılmış aygıtlar otomatik kaydı yukarı tooset bkz [etki alanına katılmış Windows cihazlarının Azure Active Directory ile otomatik kayıt ayarlama](active-directory-conditional-access-automatic-device-registration-setup.md).
* **Uyumlu cihazların**. İşaretlenen bir ilke toorestrict erişim toodevices ayarlamak **uyumlu** hello yönetim sistemi dizininde. Bu ilke, yalnızca bir aygıtta dosya şifreleme zorlama gibi güvenlik ilkeleri uyan cihazlara erişim verilir sağlar. Bu cihazları aşağıdaki hello İlkesi toorestrict erişimden kullanabilirsiniz:
  
  * **Windows etki alanına katılmış cihazları**. Tarafından System Center Configuration karma yapılandırmasında dağıtılmış Manager'da (Merhaba geçerli dal) yönetilen.
  * **Windows 10 Mobile iş veya kişisel cihazlara**. Desteklenen üçüncü taraf mobil cihaz yönetim sistemi veya Intune tarafından yönetiliyor.
  * **iOS ve Android cihazları**. Intune tarafından yönetiliyor.

Bir aygıt tabanlı tarafından korunan uygulamalar erişen kullanıcılar, bu ilkenin gereksinimlerini karşılayan bir aygıttan Merhaba uygulaması sertifika yetkilisi ilkesi erişmeniz gerekir. Erişim denendiğinde reddedildi bir cihazda ilke gereksinimlerini karşılamıyor.

Tooconfigure aygıt tabanlı bir, sertifika yetkilisi ilkesini Azure AD'de nasıl görürüm hakkında bilgi için [ayarlamak için Azure Active Directory bağlı uygulamalar cihaz temelli koşullu erişim ilkesi](active-directory-conditional-access-policy-connected-applications.md).

## <a name="resources"></a>Kaynaklar
Kaynak kategorileri ve makaleleri toolearn, kuruluşunuz için koşullu erişimi ayarlama hakkında daha fazla aşağıdaki hello bakın.

### <a name="multi-factor-authentication-and-location-policies"></a>Çok faktörlü kimlik doğrulama ve konum ilkeleri
* [Grup, konumu ve çok faktörlü kimlik doğrulama ilkeleri tabanlı koşullu erişim tooAzure AD bağlı uygulamalar ile çalışmaya başlama](active-directory-conditional-access-azuread-connected-apps.md)
* [Uygulamalar ve desteklenen tarayıcılar](active-directory-conditional-access-supported-apps.md)

### <a name="device-based-conditional-access"></a>Cihaz temelli koşullu erişim
* [Cihaz temelli koşullu erişim ilkesi erişim denetimi tooAzure Active Directory bağlı uygulamaları ayarlayın](active-directory-conditional-access-policy-connected-applications.md)
* [Windows otomatik kayıt Azure Active Directory ile etki alanına katılmış cihazları ayarlama](active-directory-conditional-access-automatic-device-registration-setup.md)
* [Azure Active Directory'ye erişim sorunları giderme](active-directory-conditional-access-device-remediation.md)
* [Microsoft Intune kullanarak kaybolan veya çalınan cihazlardaki verileri korumaya yardımcı olma](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune)

### <a name="protect-resources-based-on-sign-in-risk"></a>Oturum açma riski üzerinde temel kaynaklarını koruma
* [Azure AD kimlik koruması](active-directory-identityprotection.md)

### <a name="next-steps"></a>Sonraki adımlar
* [Koşullu erişim ile ilgili SSS](active-directory-conditional-faqs.md)
* [Teknik başvuru](active-directory-conditional-access-technical-reference.md)

