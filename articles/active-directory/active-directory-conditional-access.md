---
title: "Klasik Azure portalındaki koşullu erişim | Microsoft Docs"
description: "Koşullu erişim denetimi için belirli koşullar uygulamalara erişim için kimlik doğrulaması yapılırken denetlemek için Klasik Azure portalında kullanın."
services: active-directory
keywords: "uygulamaları, Azure AD ile koşullu erişim, koşullu erişim ilkeleri, şirket kaynaklarına güvenli erişim için koşullu erişim"
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
ms.openlocfilehash: d96eeb07c4bf3944be82d9c54aea93d52b54a37a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="conditional-access-in-the-azure-classic-portal"></a>Klasik Azure portalındaki koşullu erişim

Bu konu, Klasik Azure portalındaki koşullu erişim hakkındadır. En son Azure Active Directory'de koşullu erişim hakkında bilgi için [Azure Active Directory'de koşullu erişim](active-directory-conditional-access-azure-portal.md).


Azure Active Directory (Azure AD) koşullu erişim denetimi özelliklerinden bulutta ve şirket içi güvenli kaynaklara yardımcı olmak için basit yollar sunar. Çok faktörlü kimlik doğrulama riskini karşı korunmasına yardımcı olabilirsiniz gibi koşullu erişim ilkeleri çalınması ve phished kimlik bilgileri. Diğer koşullu erişim ilkeleri, kuruluşunuzun verilerini korumanıza yardımcı olabilir. Örneğin, kimlik bilgileri gerektiren yanı sıra Microsoft Intune, kuruluşunuzun hassas Hizmetleri erişebilir, bir mobil cihaz yönetim sisteminde kayıtlı yalnızca cihazların bir ilke olabilir.

## <a name="prerequisites"></a>Ön koşullar
Azure AD koşullu erişim özelliğidir [Azure Active Directory Premium](http://www.microsoft.com/identity). Koşullu erişim ilkelerinin uygulandığı olan bir uygulama erişen her kullanıcı bir Azure AD Premium lisansına sahip olmalıdır. Lisans gereksinimleri hakkında daha fazla bilgiyi [lisanssız kullanıcı raporu](https://aka.ms/utc5ix).

## <a name="how-is-conditional-access-control-enforced"></a>Koşullu erişim denetimi nasıl uygulanır?
Yerinde koşullu erişim denetimi ile Azure AD denetler belirli koşullar için bir kullanıcı bir uygulamaya erişmek ayarlayın. Erişim gereksinimlerinin karşılandığını sonra kullanıcı kimlik doğrulaması ve uygulamaya erişebilir.  

![Koşullu erişim genel bakış](./media/active-directory-conditional-access/conditionalaccess-overview.png)

## <a name="conditions"></a>Koşullar
Bir koşullu erişim ilkesine dahil koşullar şunlardır:

* **Grup üyelikleri**. Bir grup içinde üyelik dayalı bir kullanıcının erişimi denetler.
* **Konum**. Tetikleyici çok faktörlü kimlik doğrulaması için kullanıcı konumunu kullanın ve bir kullanıcı güvenilir bir ağ üzerinde olmadığında blok denetimleri kullanın.
* **Cihaz platformu**. İOS, Android, Windows Mobile veya Windows gibi cihaz platformu ilkesi uygulamak için bir koşul olarak kullanın.
* **Aygıt etkin**. Cihaz durumu, etkin veya devre dışı, cihaz İlkesi değerlendirmesi sırasında doğrulanır. Dizinde kaybolan veya çalınan bir cihazın devre dışı bırakırsanız, artık ilke gereksinimlerini karşılayabilen.
* **Oturum açma ve kullanıcı riski**. Kullanabileceğiniz [Azure AD Identity Protection](active-directory-identityprotection.md) koşullu erişim risk ilkeleri için. Koşullu erişim risk ilkeleri risk olaylarına ve olağan dışı oturum açma etkinlikleri göre kuruluşun gelişmiş koruma sağlamak yardımcı olur.

## <a name="controls"></a>Denetimler
Koşullu erişim ilkesini uygulamak için kullanabileceğiniz denetimleri şunlardır:

* **Çok faktörlü kimlik doğrulaması**. Çok faktörlü kimlik doğrulaması aracılığıyla güçlü kimlik doğrulamasını isteyebilirsiniz. Azure multi-Factor Authentication veya Active Directory Federasyon Hizmetleri (AD FS) ile birlikte bir şirket içi çok faktörlü kimlik doğrulama sağlayıcısı kullanarak çok faktörlü kimlik doğrulaması kullanabilirsiniz. Çok faktörlü kimlik doğrulaması kullanarak geçerli bir kullanıcı kimlik bilgilerini erişim elde etmiştir yetkisiz bir kullanıcı tarafından erişilen kaynaklar korunmasına yardımcı olur.
* **Blok**. Kullanıcı erişimini engellemek için kullanıcı konumu gibi koşullar uygulayabilirsiniz. Örneğin, bir kullanıcı güvenilir bir ağ üzerinde olmadığında erişimi engelleyebilir.
* **Uyumlu cihazların**. Koşullu erişim ilkeleri cihaz düzeyinde ayarlayabilirsiniz. Yalnızca etki alanına katılmış olan bilgisayarları veya bir mobil cihaz Yönetimi uygulamasında kaydedilen Mobil cihazların kuruluşunuzdaki kaynaklara erişebilmesi için bir ilke ayarlayabilir. Örneğin, cihaz uyumluluğunu denetlemek için Intune kullanın ve kullanıcı bir uygulamaya erişmeye çalıştığında sonra onu Azure AD zorlama için rapor. Intune uygulamaları ve verileri korumak için nasıl kullanılacağı hakkında ayrıntılı yönergeler için bkz: [uygulamaları ve Microsoft Intune ile verileri koruma](https://docs.microsoft.com/intune/deploy-use/protect-apps-and-data-with-microsoft-intune). Intune, kaybolan veya çalınan cihazlar için veri koruması uygulamak için de kullanabilirsiniz. Daha fazla bilgi için bkz: [Microsoft Intune kullanarak tam veya seçmeli Temizleme ile verilerinizin korunmasına yardımcı olma](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).

## <a name="applications"></a>Uygulamalar
Uygulama düzeyinde bir koşullu erişim ilkesi zorunlu kılabilir. Uygulamaları ve Hizmetleri için erişim düzeylerini Bulut veya şirket içi ayarlayın. İlke Web sitesi veya hizmet için uygulanır. Tarayıcı ve hizmete erişim uygulamalar için erişim ilkesi uygulanır.

## <a name="device-based-conditional-access"></a>Cihaz temelli koşullu erişim
Azure AD ile kayıtlı ve hangi belirli koşullara uyan cihazlardan uygulamalara erişimi kısıtlayabilirsiniz. Cihaz temelli koşullu erişim kuruluşun kaynakları kaynaklardan erişmeye çalışan kullanıcılardan korur:

* Bilinmeyen veya yönetilmeyen cihazlar.
* Kuruluşunuzun güvenlik ilkelerini uymayan cihazları ayarlayın.

Bu gereksinimlerine göre ilkeleri ayarlayabilirsiniz:

* **Etki alanına katılmış aygıtlar**. Bir şirket içi Active Directory etki alanına katılmış ve ayrıca Azure AD ile kayıtlı cihazlar için erişimi kısıtlamak için bir ilke ayarlayın. Bu ilke, Windows Masaüstü ve dizüstü bilgisayarlar ile Kurumsal tabletlerde geçerlidir.
  Azure AD ile etki alanına katılmış aygıtların otomatik kayıt ayarlama hakkında daha fazla bilgi için bkz: [etki alanına katılmış Windows cihazlarının Azure Active Directory ile otomatik kayıt ayarlama](active-directory-conditional-access-automatic-device-registration-setup.md).
* **Uyumlu cihazların**. İşaretli cihazlar için erişimi kısıtlamak için bir ilke ayarlayın **uyumlu** yönetim sistemi dizininde. Bu ilke, yalnızca bir aygıtta dosya şifreleme zorlama gibi güvenlik ilkeleri uyan cihazlara erişim verilir sağlar. Bu ilke aşağıdaki aygıtlardan erişimi kısıtlamak için kullanabilirsiniz:
  
  * **Windows etki alanına katılmış cihazları**. Tarafından System Center Configuration karma yapılandırmasında dağıtılmış Manager'da (geçerli dal) yönetilen.
  * **Windows 10 Mobile iş veya kişisel cihazlara**. Desteklenen üçüncü taraf mobil cihaz yönetim sistemi veya Intune tarafından yönetiliyor.
  * **iOS ve Android cihazları**. Intune tarafından yönetiliyor.

Bir aygıt tabanlı tarafından korunan uygulamalar erişen kullanıcılar, bu ilkenin gereksinimlerini karşılayan bir aygıttan uygulama sertifika yetkilisi ilkesi erişmeniz gerekir. Erişim denendiğinde reddedildi bir cihazda ilke gereksinimlerini karşılamıyor.

Azure AD'de bir aygıt tabanlı sertifika yetkilisi ilkesini yapılandırma hakkında daha fazla bilgi için bkz: [ayarlamak için Azure Active Directory bağlı uygulamalar cihaz temelli koşullu erişim ilkesi](active-directory-conditional-access-policy-connected-applications.md).

## <a name="resources"></a>Kaynaklar
Aşağıdaki kaynak kategorileri ve makaleler, kuruluşunuz için koşullu erişimi ayarlama hakkında daha fazla bilgi edinmek için bkz.

### <a name="multi-factor-authentication-and-location-policies"></a>Çok faktörlü kimlik doğrulama ve konum ilkeleri
* [Grup, konumu ve çok faktörlü kimlik doğrulama ilkeleri tabanlı Azure AD bağlı uygulamalar için koşullu erişim ile çalışmaya başlama](active-directory-conditional-access-azuread-connected-apps.md)
* [Uygulamalar ve desteklenen tarayıcılar](active-directory-conditional-access-supported-apps.md)

### <a name="device-based-conditional-access"></a>Cihaz temelli koşullu erişim
* [Azure Active Directory bağlı uygulamalar için erişim denetimi için cihaz temelli koşullu erişim ilkesini ayarlama](active-directory-conditional-access-policy-connected-applications.md)
* [Windows otomatik kayıt Azure Active Directory ile etki alanına katılmış cihazları ayarlama](active-directory-conditional-access-automatic-device-registration-setup.md)
* [Azure Active Directory'ye erişim sorunları giderme](active-directory-conditional-access-device-remediation.md)
* [Microsoft Intune kullanarak kaybolan veya çalınan cihazlardaki verileri korumaya yardımcı olma](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune)

### <a name="protect-resources-based-on-sign-in-risk"></a>Oturum açma riski üzerinde temel kaynaklarını koruma
* [Azure AD kimlik koruması](active-directory-identityprotection.md)

### <a name="next-steps"></a>Sonraki adımlar
* [Koşullu erişim ile ilgili SSS](active-directory-conditional-faqs.md)
* [Teknik başvuru](active-directory-conditional-access-technical-reference.md)

