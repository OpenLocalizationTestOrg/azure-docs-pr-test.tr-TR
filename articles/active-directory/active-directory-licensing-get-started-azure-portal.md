---
title: "Azure Active Directory'de lisanslama ile çalışmaya başlama | Microsoft Docs"
description: "Azure Active Directory lisanslaması işleyişi, en iyi yöntemlerle nereden başlayacaksınız"
services: active-directory
keywords: Azure AD lisanslama
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 6fa7cbbc452861870136482aa320d268e78fe3d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="license-yourself-and-your-users-in-azure-active-directory"></a>Kendinizin ve kullanıcılarınızın Azure Active Directory'de lisans

> [!div class="op_single_selector"]
> * [Azure portal yönergeleri](active-directory-licensing-get-started-azure-portal.md)
> * [Azure Klasik portalı bilgilerini al](active-directory-licensing-what-is.md)
>
>

Azure Active Directory (Azure AD) service (Idaas) çözümü ve Microsoft platform olarak bir kimlik değil. Azure AD farklı hizmet sürümlerinde sunulur:

* Azure Active Directory ile Office 365, Dynamics, Microsoft Intune veya Azure gibi herhangi bir Microsoft hizmeti kullanılabilir olan boş. Azure AD, bu modda tüm tüketim ücretlerinden oluşturmaz.

* Azure AD sürümleri, gibi Ücretli:
  - Enterprise Mobility + Security 
  - Azure AD Premium (P1 ve P2)
  - Azure AD Basic
  - Azure Multi-Factor Authentication

Office 365, Microsoft Intune ve Azure AD oldukları gibi pek çok Microsoft Çevrimiçi hizmetler gibi çoğu Azure AD Ücretli sürümleri kullanıcı başına yetkilendirmeler teslim edilir. Bu durumlarda, hizmeti satın alma bir veya daha fazla abonelik tarafından temsil edilen ve her abonelik prepurchased bazı lisanslar kiracınızdaki içerir. Kullanıcı başına yetkilendirmeler tarafından sağlanır:

* Bir lisans atama. 
* Kullanıcı ve ürün arasında bir bağlantı oluşturuluyor.
* Kullanıcı için hizmet bileşenleri etkinleştiriliyor.
* Ön ödemeli lisanstan kullanma.

[Azure AD Premium şimdi deneyin.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

Azure AD hizmet özellikleri geniş kapsamlı bir genel bakış için bkz: [Azure AD nedir?](active-directory-whatis.md). Daha fazla bilgi için bizim [hizmet düzeyi sözleşmeleri sayfa](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/).

> [!NOTE]
> Azure Kullandıkça Öde abonelikleri Azure kaynaklarını oluşturulmasını sağlamak ve ardından bunları ödeme yönteminizi eşleyin. Abonelikle ilişkili hiçbir lisans sayıları vardır. Abonelik eşlenen Azure kaynaklarını üzerinde çalışacağı bir kullanıcı izni vermek, abonelikle ilişkili ve abonelik kaynakları yönetebilir.

## <a name="how-does-azure-active-directory-licensing-work"></a>Azure Active Directory lisanslama nasıl çalışır?

Lisans tabanlı Azure AD, Azure AD hizmeti kiracınız abonelikte etkinleştirerek iş Hizmetleri. Abonelik etkinleştirildikten sonra hizmet özellikleri Azure AD yöneticileri tarafından yönetilir ve lisanslı kullanıcılar tarafından kullanılır.

### <a name="manage-subscription-information"></a>Abonelik bilgilerini yönetin

Enterprise Mobility + güvenlik, Azure AD Premium veya Azure AD temel satın aldığınızda, Kiracı, geçerlilik süresi ve ön ödemeli lisansları dahil olmak üzere abonelikle güncelleştirilir. Atanan veya kullanılabilir lisans sayısı gibi abonelik bilgilerinizi Azure portalı üzerinden kullanılabilir: altında **Azure Active Directory**açın **lisansları** özel döşeme Dizin. **Lisansları** dikey olan lisans anlaşmalarını yönetme için en iyi yerdir.

Bir veya daha fazla hizmet planları, Azure AD gibi her abonelik oluşan çok faktörlü kimlik doğrulaması, Intune, Exchange Online veya SharePoint Online.  Azure AD lisans yönetimini yapan *değil* hizmet planı düzeyi yönetim gerektirir. Office 365 dahil hizmetlere erişimi yönetmek üzere bu Gelişmiş Yapılandırma modu kullandığından farklıdır. Azure AD özelliklerini etkinleştirebilmek ve tek tek izinleri yönetmek için Kullanımdaki yapılandırmasına bağlıdır.

> [!IMPORTANT]
> Azure AD Premium, Azure AD temel ve Enterprise Mobility + güvenlik abonelikleri sağlanan kendi dizin/Kiracı sınırlandırılmıştır. Abonelikleri dizinler arasında bölme veya diğer dizinlerdeki kullanıcıları entitle için kullanılır. Dizinler arasındaki bir abonelik mümkündür taşıma ancak gerektiriyorsa bir destek bileti göndermeyi veya satın alma işlemleri doğrudan iptal ve repurchase için.
>
> Zaman Azure AD veya Enterprise Mobility + Security Toplu Lisanslama bir abonelik satın ve anlaşmayı diğer Microsoft Online Hizmetleri (örneğin, Office 365) içerdiğinde, etkinleştirme otomatik olarak gerçekleşir. 

### <a name="assign-licenses"></a>Lisans atama

Bir aboneliği elde Ücretli özellikleri yapılandırmak için gereken her şeyi olsa da, kullanıcıların özellikleri Ücretli Azure AD için hala lisansları dağıtmanız gerekir. Özellik erişimi olması gereken veya Azure AD ile yönetilen Ücretli herhangi bir kullanıcı bir lisans atanması gerekir. Lisans atama, kullanıcı ve Azure AD Premium, Basic veya Enterprise Mobility + Security gibi bir satın alınan hizmet arasındaki bir eşlemedir.


Dizininizdeki hangi kullanıcıların bir lisansı olması yönetme tarafından gerçekleştirilebilir: 

* Lisans gruplarına atama [Azure portal](active-directory-licensing-whatis-azure-portal.md).
* Doğrudan portal, PowerShell veya API aracılığıyla kullanıcılara lisanslar atama. 

Bir gruba lisans atama, tüm Grup üyeleri lisansı atanır. Kullanıcılar eklendiğinde veya gruptan kaldırıldığında, uygun lisans atanmış veya kaldırılmış. Grup ataması kullanabileceğiniz herhangi bir Grup Yönetim kullanabilir ve uygulamalara grup tabanlı atama ile tutarlıdır.

Kullanabileceğiniz [grup tabanlı lisans atamasını](active-directory-licensing-whatis-azure-portal.md) aşağıdaki gibi kurallar ayarlamak için:
* Dizininizdeki tüm kullanıcılara otomatik olarak bir lisans alın
* Uygun iş unvanı herkesle bir lisans alır
* Kuruluştaki diğer yöneticiler kararını devredebilirsiniz (kullanarak [Self Servis grup](active-directory-accessmanagement-self-service-group-management.md))

Gelişmiş senaryolar ve Office 365 senaryoları, lisans gruplarına lisans atama hakkında ayrıntılı bilgi için dahil olmak üzere bkz [Azure Active Directory'de Grup üyeliğiyle kullanıcılara lisanslar atama](active-directory-licensing-group-assignment-azure-portal.md).

## <a name="get-started-with-azure-ad-licensing"></a>Başlama Azure AD lisansı

Azure AD ile çalışmaya başlama kolaydır. Dizininiz için imzalama bir parçası olarak her zaman oluşturabileceğiniz bir [Azure ücretsiz deneme](https://azure.microsoft.com/offers/ms-azr-0044p/).

Aşağıdaki en iyi yöntemler, Kiracı tüketen diğer Microsoft Hizmetleri ile hedeflerinize hizmet hizalanır sağlamaya yardımcı olabilir:

- Zaten bir Microsoft Kuruluş hizmetlerini kullanıyorsanız, Azure AD kiracısı zaten sahip. Sağlama dahil olmak üzere çekirdek kimlik yönetimi ve karma çoklu oturum açma (SSO), kullanılabilir hizmetler arasında böylece diğer hizmetler için aynı Kiracı kullanmak yararlıdır. Çoklu oturum açma ile kullanıcılarınız Hizmetleri zengin özelliklerini yarar sağlar. Bu nedenle, hizmeti, iş gücü için ücretli bir Azure AD satın karar verirseniz, aynı kiracıyı yeniden kullanmanızı öneririz.

- Dağıtmayı planlıyorsanız, Azure portalında yeni bir kiracı kullanmanızı öneririz:
  - Azure AD (örneğin, iş ortakları veya müşterilerin) kullanıcılar farklı bir kümesini kullanın.
  - Azure AD hizmetlerinde üretim hizmetinizden yalıtım değerlendirin.
  - Bir korumalı alan ortamıdır hizmetleriniz için ayarlayın.

  Yeni dizin hesabınızla genel yönetici izinlerine sahip bir dış kullanıcı olarak oluşturulur. Azure portalına bu hesapla oturum açtığınızda, bu Kiracı görebilir ve tüm yönetim görevlerini erişebilirsiniz.

> [!NOTE]
> Azure AD "Microsoft hesabı ya da başka bir kiracı bir Azure AD kimlik aracılığıyla oluşturulan kullanıcı hesaplarında Azure AD kiracısı olan konuk kullanıcılar," destekler. Office 365 Yönetim Portalı'nı bu kullanıcılar şu anda desteklemiyor. Konuk kullanıcılar Microsoft hesabı olan diğer Azure AD kiracılarıyla konuk kullanıcıların göz ardı edilir sırada Office 365 Yönetim Portalı'nı hiç erişmek mümkün değildir. İkinci durumda, yalnızca kullanıcının yerel hesabı, Azure AD'de veya Office 365 Kiracı Kullanıcı ilk olarak oluşturulduğu, erişilebilir.

### <a name="select-one-or-more-license-trials"></a>Bir veya daha fazla lisans denemeler seçin

Etkinleştirme için Azure AD Premium veya Enterprise Mobility + güvenlik deneme aboneliği altında **Azure Active Directory** &gt; **Hızlı Başlangıç**.

![Bir lisans deneme sürümü'nü seçin](media/active-directory-licensing-get-started-azure-portal/select-a-license-trial.png)

Deneme lisansı bulunur **lisansları** dikey.

### <a name="assign-licenses-to-users-and-groups"></a>Kullanıcılar ve gruplar için lisans atama

Abonelik etkinleştirildikten sonra kendiniz için bir lisans atamanız gerekir. Ardından tüm özellikleri görmesini sağlamak için tarayıcıyı yenileyin. Azure AD özelliklerini erişmek isteyen kullanıcıların lisans atamak için ücretli sonraki adımdır. Bölümünde açıklandığı gibi [lisansları atamak](#assign-licenses), bir lisans atamak için kolay yoludur istenen hedef kitle temsil eden tanımlayın ve lisans atamak için. Bu şekilde, kullanıcılar eklendiğinde veya gruptan kendi ömrü kaldırıldığında atanan veya lisansı, sırasıyla kaldırıldı.

> [!NOTE]
> Bazı Microsoft Hizmetleri tüm konumlarda kullanılabilir değil. Yönetici bir kullanıcıya bir lisans atanabilmesi için önce belirtmelidir **kullanım konumu** kullanıcı için özellik. Bu özelliği altında ayarlayabilirsiniz **kullanıcı** &gt; **profil** &gt; **ayarları** Azure portalında. Grup lisans atamasını kullanırken, kullanım konumu belirtilmezse herhangi bir kullanıcı dizininin konumunu devralır.

Altında bir lisans atamak için **Azure Active Directory** &gt; **lisansları** &gt; **tüm ürünleri**, bir veya daha fazla ürünleri seçin ve ardından seçin **Ata** komut çubuğunda.

![Bir lisans atamak için seçin](media/active-directory-licensing-get-started-azure-portal/select-license-to-assign.png)

Kullanabileceğiniz **kullanıcılar ve gruplar** dikey birden çok kullanıcı veya grup seçin ya da hizmet planları üründeki devre dışı bırakmak için. Arama kutusuna üstte kullanıcı ve grup adları aramak için kullanın.

![Bir kullanıcı veya grup için lisans atamasını seçin](media/active-directory-licensing-get-started-azure-portal/select-user-for-license-assignment.png)

Bir gruba bir lisans atama, tüm kullanıcılar grubunda kullanıcıların sayısına bağlı olarak lisans devralırlar önce biraz zaman alabilir. İşleme durumunu denetleyebilirsiniz **grup** dikey altında **lisansları** döşeme.

![Lisans atama durumu](media/active-directory-licensing-get-started-azure-portal/license-assignment-status.png)

Atama hataları sırasında Azure AD lisans atamasını gerçekleşebileceğini, ancak Azure AD yönetirken görece olarak daha ender ve Enterprise Mobility + güvenlik ürünleri. Olası atama hataları sınırlıdır:
- Atama çakışma: ne zaman bir kullanıcı daha önce atanma geçerli lisansı ile uyumsuz bir lisans. Bu durumda, yeni lisans atama geçerli kaldırılması gerekir.
- Kullanılabilir lisans aşıldı: atanan gruplarındaki kullanıcılar kullanılabilir lisans sayısını aştığında, bir hata nedeniyle eksik lisansları atamak için bir kullanıcının atama durumu yansıtır.

#### <a name="azure-ad-b2b-collaboration-licensing"></a>Azure AD B2B işbirliği lisanslama

B2B işbirliği Azure AD hizmetlerinde erişim sağlamak için Azure AD kiracınıza içine Konuk kullanıcıları davet sağlar ve Azure kaynaklarını kullanılabilir yapın.  

B2B kullanıcıları davet ve bunları Azure AD'de bir uygulamaya atamak için ücretsizdir. En fazla 10 Konuk kullanıcı ve 3 temel rapor başına uygulamalardır ayrıca B2B işbirliği kullanıcılar için boş. Konuk kullanıcı ortağının Azure AD kiracısında atanmış uygun lisans varsa, bunlar sizin içinde de lisansına sahip olması.

Gerekli değildir, ancak Azure AD özelliklerini Ücretli erişim sağlamak istiyorsanız, bu B2B Konuk kullanıcılar lisansına sahip olması gerekir ile Azure AD lisansları uygun. Davet bir kiracı ile lisans Ücretli bir Azure AD B2B işbirliği Kiracı için davet ek bir beş Konuk kullanıcılar kullanıcı hakları atayabilirsiniz. Senaryolar ve bilgi için bkz: [Kılavuzu lisans B2B işbirliği](active-directory-b2b-licensing.md).

### <a name="view-assigned-licenses"></a>Görünüm atanan lisansları

Atanan ve kullanılabilir lisans Özet görünümünü altında görüntülenen **Azure Active Directory** &gt; **lisansları** &gt; **tüm ürünleri**.

![Özet görünümü lisans](media/active-directory-licensing-get-started-azure-portal/view-license-summary.png)

Atanan kullanıcıların ve grupların ayrıntılı bir liste, belirli bir ürün seçildiğinde kullanılabilir. **Lisanslı kullanıcı** listesi şu anda bir lisans ve lisans doğrudan kullanıcıya atanmış olup olmadığını veya bir gruptan devralınan varsa kullanan tüm kullanıcıları gösterir.

![Lisans ayrıntıları görüntüle](media/active-directory-licensing-get-started-azure-portal/view-license-detail.png)

Benzer şekilde, **lisans grupları** liste olduğu lisansları atanan tüm grupları gösterir. Bir kullanıcı veya açmak için grup seçin **lisansları** bu nesne için atanmış tüm lisanslar gösteren dikey.

### <a name="remove-a-license"></a>Bir lisans Kaldır

Bir lisans kaldırmak için kullanıcı veya gruba gidin ve açmak **lisansları** döşeme. Lisans seçin ve tıklayın **kaldırmak**.

![Bir lisans Kaldır](media/active-directory-licensing-get-started-azure-portal/remove-license.png)

Bir gruptan bir kullanıcı tarafından devralınmış lisansları doğrudan kaldırılamaz. Bunun yerine, kullanıcı, bunlar lisans devralan grubundan kaldırın.

### <a name="extend-trials"></a>Denemeler genişletme

Deneme müşteriler uzantıları mevcut Office 365 Portalı aracılığıyla kaydolma Self Servisi olarak. Bir müşteri yönetici Office portalı gidebilirsiniz (erişim bağımlı Office portalı izinlerini) ve Azure AD Premium deneme sürümü'nü seçin. Tıklatarak **genişletmek deneme** bağlantı uzantısı işlemi başlatır. Bir kredi kartı gereklidir, ancak değil doludur.

![Azure portalında bir deneme genişletme](media/active-directory-licensing-get-started-azure-portal/extend-trial-beginning.png)

## <a name="next-steps"></a>Sonraki adımlar

Gelişmiş senaryolar için grupları üzerinden lisans yönetimi hakkında daha fazla bilgi için makaleyi okuyun [bir gruba lisans atama](active-directory-licensing-group-assignment-azure-portal.md).

Aşağıda, yapılandırma ve diğer Azure AD Ücretli özelliklerini kullanma hakkında bilgi verilmiştir:

* [Self Servis parola sıfırlama](active-directory-manage-passwords.md)
* [Self Servis Grup Yönetimi](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect health](active-directory-aadconnect-health.md)
* [Azure çok faktörlü kimlik doğrulaması](../multi-factor-authentication/multi-factor-authentication.md)
* [Doğrudan lisansları satın almanızdan Azure AD Premium](http://aka.ms/buyaadp)
