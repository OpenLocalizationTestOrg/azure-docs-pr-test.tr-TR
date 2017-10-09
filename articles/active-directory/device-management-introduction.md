---
title: "Azure Active Directory'de aaaIntroduction toodevice Yönetimi | Microsoft Docs"
description: "Nasıl aygıt yönetimi, ortamınızdaki kaynakları erişen hello aygıtları üzerinde tooget denetim yardımcı olabileceğini öğrenin."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: e2fc0a3e8d00dc69cf01db9074e34427e396cfcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodevice-management-in-azure-active-directory"></a>Azure Active Directory'de giriş toodevice Yönetimi

Bir mobil ilk olarak, bulut ilk dünyada tek oturum açma toodevices, uygulama ve hizmetlere her yerden Azure Active Directory (Azure AD) sağlar. Kendi cihazını getir (KCG), aygıtlar - Hello artışı ile BT uzmanları iki rakip hedefle karşılaştığı:

- Merhaba son kullanıcıların toobe üretken yerde ve zamanda güç kazandırma
- Herhangi bir zamanda Hello şirket varlıklarını koruma

Aygıtlar, kullanıcılarınızın tooyour Kurumsal varlıklar erişim sağlama. tooprotect şirket varlıklarınızı bir BT yöneticisi olarak, bu aygıtlar üzerinde toohave denetimine istiyor. Bu, güvenlik ve uyumluluğa yönelik standartlarınızı karşılamak aygıtlardan kullanıcılarınızın kaynaklarınızı eriştiğiniz emin toomake sağlar. 

Cihaz yönetimi, ayrıca hello temeli [cihaz temelli koşullu erişim](active-directory-conditional-access-policy-connected-applications.md). Cihaz temelli koşullu erişim ile ortamınızdaki tooresources yalnızca ile mümkündür erişim cihazlar güvenilen emin olabilirsiniz.   

Bu konuda, Azure Active Directory içindeki aygıt yönetimi nasıl çalıştığı açıklanmaktadır.

## <a name="getting-devices-under-hello-control-of-azure-ad"></a>Azure ad hello denetimindeki aygıtları alma

Azure ad hello denetimindeki bir aygıtı tooget, iki seçeneğiniz vardır:

- Kaydetme 
- Birleştirme

**Kaydetme** aygıt tooAzure AD, toomanage bir cihazın kimliğini sağlar. Bir cihaz kaydedildiğinde Azure AD cihaz kaydı hello kullanılan tooauthenticate hello aygıt bir kullanıcı oturum açtığında tooAzure olduğunda AD olan kimliğe sahip cihazı sağlar. Merhaba kimlik tooenable kullanın veya bir aygıtı devre dışı.

Microsoft Intune gibi bir mobil cihaz birleştirildiğinde çözüm ile birlikte kullanıldığında, Azure AD'de hello cihaz öznitelikleri hello cihaz hakkındaki ek bilgilerle güncelleştirilir. Bu, cihazları toomeet erişimden zorunlu toocreate koşullu erişim kuralları, güvenlik ve uyumluluğa yönelik standartlarınızı sağlar. Microsoft Intune kaydolan cihazlar hakkında daha fazla bilgi için Yönetim için ıntune'a kaydetme aygıtları bakın.

**Birleştirme** uzantısı tooregistering bir aygıtı aygıttır. Bunun anlamı tüm hello avantajları bir cihaz kaydetme ve ayrıca toothis sağlar, ayrıca hello yerel bir cihazın durumunu değiştirir. Merhaba yerel durumunu değiştirme kişisel hesabı yerine bir kuruluş iş veya Okul hesabını kullanarak kullanıcılar toosign bileşenini tooa Cihazınızı sağlar.

## <a name="azure-ad-registered-devices"></a>Azure AD kayıtlı cihazları   

Hello Azure AD kayıtlı cihazlar ile desteklediğiniz Merhaba tooprovide hedefidir **kendi cihazını getir (KCG)** senaryo. Bu senaryoda, bir kullanıcı kişisel bir cihazı kullanarak, kuruluşunuzun Azure Active Directory denetlenen kaynaklarına erişebilir.  

![Azure AD kayıtlı cihazları](./media/device-management-introduction/03.png)

Merhaba erişim hello aygıtta girilen bir iş veya Okul hesabı temel alır.  
Örneğin, Windows 10 iş veya Okul hesabı tooa kişisel bilgisayar, tablet veya telefon kullanıcıları tooadd sağlar.  
Ne zaman bir kullanıcı eklenmiş bir iş veya Okul hesabı, hello aygıt Azure AD ile kayıtlı ve isteğe bağlı olarak, kuruluşunuz yapılandırılmış hello mobil cihaz Yönetimi (MDM) sisteminde kayıtlı. Kuruluşunuzdaki kullanıcılar bir iş ekleyebilir veya hesap tooa kişisel cihaz rahat Okul:

- Bir iş uygulaması ilk kez hello için erişirken
- Hello kullanarak el ile **ayarları** Windows 10 hello durumda menüsü 

Azure AD kayıtlı cihazlara Windows 10, iOS, Android ve macOS için yapılandırabilirsiniz.

## <a name="azure-ad-joined-devices"></a>Azure AD alanına katılmış aygıtlar

Azure AD alanına katılmış aygıtlar Hello amacı toosimplify şöyledir:

- Windows dağıtımları iş ait cihazlar 
- Erişim tooorganizational uygulamaları ve herhangi bir Windows aygıtı kaynaklardan

![Azure AD kayıtlı cihazları](./media/device-management-introduction/02.png)


Azure ad hello denetiminde çalışma şirkete ait cihazları almak için kullanıcılarınızın bir Self Servis deneyimi sağlayarak bu hedefleri gerçekleştirilebilir.  
**Azure AD birleştirme** bulut ilk / salt bulut olan kuruluşlar için tasarlanmıştır. Bir şirket içi Windows Server Active Directory altyapısına sahip olmayan küçük ve orta ölçekli işletmeler genellikle şunlardır. 

Azure AD alanına katılmış aygıtlar uygulama ile Merhaba aşağıdaki avantajları sağlar:

- **Çoklu oturum açma (SSO)** tooyour Azure yönetilen SaaS uygulamaları ve Hizmetleri. Kullanıcılarınızın, iş kaynaklarına erişirken ek kimlik doğrulama istekleri görmüyorum. Merhaba SSO işlevlerini bağlı toohello etki alanı ağında kullanılabilir değil olduğunda bile.

- **Kurumsal uyumlu gezici** alanına katılmış aygıtlar arasındaki kullanıcı ayarlarının. Kullanıcılar, cihazlar arasında bir Microsoft hesabı (örneğin, Hotmail) toosee ayarları tooconnect ihtiyacınız yoktur.

- **İş için erişim tooWindows mağazası** AD hesabı kullanarak. Kullanıcılarınızın hello kuruluş tarafından önceden seçilmiş uygulamalarının stoğunu arasından seçim yapabilirsiniz.

- **Windows Hello** toowork kaynaklarına güvenli ve kolay erişim için destek.

- **Erişim kısıtlama** uyumluluk ilkesine uygun aygıtlardan tooapps.

Azure AD birleştirme öncelikle bir şirket içi Windows Server Active Directory altyapısına sahip olmayan kuruluşlar için tasarlanmıştır ancak kesinlikle yapabilecekleriniz senaryolarda de burada:

- Tabletler ve telefonlardan denetimindeki gibi mobil cihazları tooget ihtiyacınız varsa, örneğin, bir şirket içi etki alanına katılma kullanamazsınız.

- Kullanıcılarınızın öncelikle tooaccess Office 365 veya Azure AD ile tümleşik diğer SaaS uygulamaları gerekir.

- Active Directory yerine Azure AD'de toomanage bir kullanıcı grubuna istiyor. Bu, örneğin, tooseasonal çalışanları, Yükleniciler veya Öğrenciler uygulayabilirsiniz.

- Tooprovide katılma yetenekleri tooworkers sınırlı şirket içi altyapı ile uzak şube ofislerinde istiyor.

Windows 10 cihazlar için Azure AD alanına katılmış cihazları yapılandırabilirsiniz.


## <a name="hybrid-azure-ad-joined-devices"></a>Karma Azure AD alanına katılmış aygıtlar

Birden fazla bir süredir birçok kuruluş hello etki alanına katılma tootheir şirket içi Active Directory tooenable kullanmıştır:

- BT departmanları toomanage iş şirkete ait cihazları merkezi bir konumdan.

- Kullanıcıların toosign tootheir aygıtları kendi Active Directory ile iş veya Okul hesapları. 

Genellikle, bir şirket içi ayak izini kuruluşlarla kullanan görüntüleme yöntemleri tooprovision aygıtları ve sık kullandıkları **System Center Configuration Manager (SCCM)** veya **Grup İlkesi (GP)** toomanage bunları.

Şirket içi ortamınız varsa, AD alanını ve ayrıca Azure Active Directory tarafından sağlanan hello özelliklerden avantajı istiyorsanız, karma Azure AD alanına katılmış aygıtlar uygulayabilirsiniz. Bunlar, her ikisi de aygıtlardır, birleştirilmiş tooyour şirket içi Active Directory ve Azure Active Directory'yi.

![Azure AD kayıtlı cihazları](./media/device-management-introduction/01.png)


Varsa Azure AD karma alanına katılmış aygıtlar kullanmanız gerekir:

- NTLM kullanan Win32 uygulamaları dağıtılan toothese aygıtlar sahip / Kerberos.

- GP veya SCCM gerektiren / DCM toomanage aygıtlar.

- Çalışanlarınız için toocontinue toouse görüntüleme çözümleri tooconfigure cihazların istediğiniz.

Karma Azure yapılandırabilirsiniz AD alanına katılmış cihazlar Windows 10 ve Windows 8 ve Windows 7 gibi alt düzey cihazlar.

## <a name="summary"></a>Özet

Azure AD'de cihaz yönetimi ile şunları yapabilirsiniz: 

- Azure AD hello denetiminde aygıtlarını getiren hello işlemini basitleştirmek

- Kullanıcılarınıza kolay toouse erişim tooyour kuruluşun bulut tabanlı kaynaklar ile sağlama

Bir Flash bir kural olarak kullanmanız gerekir:

- Kişisel cihazlar için Azure AD kayıtlı cihazları

- Azure AD alanına katılmış aygıtlar tooan katılmış olmayan cihazlarda şirket içi AD 

- Karma Azure AD alanına katılmış aygıtlar tooan katılmış olan cihazlarda şirket içi AD     




## <a name="next-steps"></a>Sonraki adımlar

- tooget nasıl toomanage aygıtı hello Azure portal, bkz: genel bakış [hello Azure portalını kullanarak cihazları yönetme](device-management-azure-portal.md)

- cihaz temelli koşullu erişim hakkında daha fazla toolearn bkz [Azure Active Directory cihaz temelli koşullu erişim ilkelerini yapılandırma](active-directory-conditional-access-policy-connected-applications.md).

- bkz: toosetup karma Azure AD alanına katılmış aygıtlar [nasıl tooconfigure karma Azure Active Directory'ye katılmış cihazlarda](device-management-hybrid-azuread-joined-devices-setup.md).


