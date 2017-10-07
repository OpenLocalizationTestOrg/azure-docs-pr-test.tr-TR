---
title: "aaaGet başlatılan Azure Active Directory'de lisans | Microsoft Docs"
description: "Azure Active works lisans dizinini nasıl tooget en iyi uygulamalar ile çalışmaya nasıl"
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
ms.openlocfilehash: 268dab806b8b959790341d630a0355c6a43871d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
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

Office 365, Microsoft Intune ve Azure AD oldukları gibi pek çok Microsoft Çevrimiçi hizmetler gibi çoğu Azure AD Ücretli sürümleri kullanıcı başına yetkilendirmeler teslim edilir. Bu durumlarda, hello hizmeti satın alma bir veya daha fazla abonelik tarafından temsil edilen ve her abonelik prepurchased bazı lisanslar kiracınızdaki içerir. Kullanıcı başına yetkilendirmeler tarafından sağlanır:

* Bir lisans atama. 
* Merhaba kullanıcı ve hello ürün arasında bir bağlantı oluşturuluyor.
* Merhaba hizmet bileşenleri hello kullanıcı için etkinleştiriliyor.
* Merhaba birini kullanma lisansları ön ödemeli.

[Azure AD Premium şimdi deneyin.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

Azure AD hizmet özellikleri geniş kapsamlı bir genel bakış için bkz: [Azure AD nedir?](active-directory-whatis.md). Daha fazla bilgi için bizim [hizmet düzeyi sözleşmeleri sayfa](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/).

> [!NOTE]
> Azure Kullandıkça Öde abonelikleri Azure kaynaklarını oluşturulmasını sağlamak ve ardından bunları tooyour ödeme yöntemi eşleyebilirsiniz. Merhaba abonelikle ilişkili hiçbir lisans sayıları vardır. Bir kullanıcı izni toooperate Azure kaynaklarına toohello aboneliği eşleştirilmiş vermek, hello abonelikle ilişkilendirilmiş ve abonelik kaynakları yönetebilir.

## <a name="how-does-azure-active-directory-licensing-work"></a>Azure Active Directory lisanslama nasıl çalışır?

Lisans tabanlı Azure AD, Azure AD hizmeti kiracınız abonelikte etkinleştirerek iş Hizmetleri. Hello abonelik etkinleştirildikten sonra hello hizmet özellikleri Azure AD yöneticiler tarafından yönetilir ve lisanslı kullanıcılar tarafından kullanılır.

### <a name="manage-subscription-information"></a>Abonelik bilgilerini yönetin

Enterprise Mobility + güvenlik, Azure AD Premium veya Azure AD temel, Kiracı satın ne zaman geçerlilik süresinin dahil olmak üzere hello abonelikle güncelleştirilir ve lisansları ön ödemeli. Hello atanan veya kullanılabilir lisans sayısı gibi abonelik bilgilerinizi hello Azure portalı kullanılabilir: altında **Azure Active Directory**açın hello **lisansları** Merhaba döşeme özel dizin. Merhaba **lisansları** dikey olduğunu da hello en iyi yeri toomanage lisans atamalarınızı.

Bir veya daha fazla hizmet planları, Azure AD gibi her abonelik oluşan çok faktörlü kimlik doğrulaması, Intune, Exchange Online veya SharePoint Online.  Azure AD lisans yönetimini yapan *değil* hizmet planı düzeyi yönetim gerektirir. Bu gelişmiş yapılandırma modu toomanage erişim tooincluded Services'de kullandığından office 365 farklıdır. Azure AD Kullanımdaki yapılandırma tooenable özellikleri kullanır ve tek tek izinleri yönetin.

> [!IMPORTANT]
> Azure AD Premium, Azure AD temel ve Enterprise Mobility + güvenlik abonelikleri yalıtılmış tootheir sağlanan dizin/Kiracı var. Abonelikler, dizinleri veya diğer dizinlerde kullanılan tooentitle kullanıcılar arasında bölünemez. Dizinler arasındaki bir abonelik mümkündür taşıma ancak gerektiriyorsa bir destek bileti göndermeyi veya satın alma işlemleri doğrudan iptal ve repurchase için.
>
> Zaman Azure AD veya Enterprise Mobility + Security Toplu Lisanslama bir abonelik satın ve hello sözleşmesi diğer Microsoft Online Hizmetleri (örneğin, Office 365) içerdiğinde, etkinleştirme otomatik olarak gerçekleşir. 

### <a name="assign-licenses"></a>Lisans atama

Bir aboneliği elde tüm yetenekleri Ücretli tooconfigure ihtiyacınız olsa da, özellikleri toousers Ücretli Azure AD için hala lisansları dağıtmanız gerekir. Özellik Ücretli bir Azure AD ile yönetilen erişim tooor olmalıdır herhangi bir kullanıcı bir lisans atanması gerekir. Lisans atama, kullanıcı ve Azure AD Premium, Basic veya Enterprise Mobility + Security gibi bir satın alınan hizmet arasındaki bir eşlemedir.


Dizininizdeki hangi kullanıcıların bir lisansı olması yönetme tarafından gerçekleştirilebilir: 

* Merhaba toogroups lisansları atama [Azure portal](active-directory-licensing-whatis-azure-portal.md).
* Atama toousers hello portal, PowerShell veya API aracılığıyla doğrudan lisansları. 

Lisansları tooa Grup atarken tüm Grup üyeleri lisansı atanır. Kullanıcıların eklediyseniz veya hello grubundan kaldırılmış hello uygun lisans atanmış veya kaldırılmış. Grup ataması tüm Grup Yönetimi kullanılabilir tooyou kullanabilir ve grup tabanlı atama tooapplications ile tutarlıdır.

Kullanabileceğiniz [grup tabanlı lisans atamasını](active-directory-licensing-whatis-azure-portal.md) tooset hello aşağıdaki gibi kurallar:
* Dizininizdeki tüm kullanıcılara otomatik olarak bir lisans alın
* Merhaba uygun iş unvanı herkesle bir lisans alır
* Merhaba karar tooother yöneticileri hello kuruluşunuzdaki devredebilirsiniz (kullanarak [Self Servis grup](active-directory-accessmanagement-self-service-group-management.md))

Lisans atama toogroups hakkında ayrıntılı bilgi için Gelişmiş senaryoları ve Office 365 senaryoları, lisanslama dahil olmak üzere bkz [Ata lisansları Azure Active Directory'de Grup üyeliğiyle toousers](active-directory-licensing-group-assignment-azure-portal.md).

## <a name="get-started-with-azure-ad-licensing"></a>Başlama Azure AD lisansı

Azure AD ile çalışmaya başlama kolaydır. Dizininiz için imzalama bir parçası olarak her zaman oluşturabileceğiniz bir [Azure ücretsiz deneme](https://azure.microsoft.com/offers/ms-azr-0044p/).

Merhaba aşağıdaki en iyi yöntemleri Kiracı tüketen diğer Microsoft Hizmetleri ile hedeflerinize hello hizmeti için hizalanır sağlamaya yardımcı olabilir:

- Zaten hello kuruluş Microsoft hizmetlerinden birini kullanıyorsanız, Azure AD kiracısı zaten sahip. Merhaba hizmetleri sağlama dahil olmak üzere çekirdek kimlik yönetimi ve karma çoklu oturum açma (SSO), kullanılabilir böylece aynı diğer hizmetler için Kiracı yararlı toouse hello olur. Çoklu oturum açma ile kullanıcılarınız hello zengin özelliklerini hello Hizmetleri yararlanır. Bu nedenle, toobuy bir Ücretli Azure AD hizmeti, iş gücü için karar verirseniz, aynı yeniden Kiracı hello kullanmanızı öneririz.

- Planlıyorsanız, yeni bir kiracı hello Azure portalını kullanmanızı öneririz:
  - Azure AD (örneğin, iş ortakları veya müşterilerin) kullanıcılar farklı bir kümesini kullanın.
  - Azure AD hizmetlerinde üretim hizmetinizden yalıtım değerlendirin.
  - Bir korumalı alan ortamıdır hizmetleriniz için ayarlayın.

  Merhaba yeni dizin hesabınızla genel yönetici izinlerine sahip bir dış kullanıcı olarak oluşturulur. Toohello bu hesapla Azure Portalı'nda oturum açtığınızda, bu Kiracı görebilir ve tüm yönetim görevlerini erişebilirsiniz.

> [!NOTE]
> Azure AD "Microsoft hesabı ya da başka bir kiracı bir Azure AD kimlik aracılığıyla oluşturulan kullanıcı hesaplarında Azure AD kiracısı olan konuk kullanıcılar," destekler. Merhaba Office 365 Yönetim Portalı, bu kullanıcılar şu anda desteklemiyor. Diğer Azure AD kiracılarıyla konuk kullanıcıların göz ardı edilir ancak Konuk kullanıcılar Microsoft hesaplarıyla mümkün tooaccess hello Office 365 Yönetim Portalı hiç olup olmadığı. Merhaba ikinci durumda, yalnızca kullanıcının yerel hesabı hello Azure AD hello veya hello kullanıcı ilk olarak oluşturulduğu, Office 365 Kiracı erişilebilir değil.

### <a name="select-one-or-more-license-trials"></a>Bir veya daha fazla lisans denemeler seçin

Etkinleştirme için Azure AD Premium veya Enterprise Mobility + güvenlik deneme aboneliği altında **Azure Active Directory** &gt; **Hızlı Başlangıç**.

![Bir lisans deneme sürümü'nü seçin](media/active-directory-licensing-get-started-azure-portal/select-a-license-trial.png)

Merhaba deneme lisansı kullanılabilir **lisansları** dikey.

### <a name="assign-licenses-toousers-and-groups"></a>Lisansları toousers ve grupları atama

Merhaba abonelik etkinleştirildikten sonra lisans tooyourself atamanız gerekir. Ardından tüm hello özellikleri görüyorsunuz hello tarayıcı tooensure yenileyin. Merhaba sonraki toopaid Azure AD özelliklerine erişmek isteyen tooassign lisansları toohello kullanıcılar adımdır. Bölümünde açıklandığı gibi [lisansları atamak](#assign-licenses), kolay yollarından tooassign lisansı olabilir tooidentify hello Grup hello temsil eden hedef kitle istenen ve hello lisans tooit atayın. Bu şekilde, eklenen veya kendi ömrü hello grubundan kaldırılmış kullanıcıların atanan veya hello lisanstan sırasıyla kaldırıldı.

> [!NOTE]
> Bazı Microsoft Hizmetleri tüm konumlarda kullanılabilir değil. Bir lisans tooa kullanıcı atanabilmesi için önce hello yönetici hello belirtmelidir **kullanım konumu** hello kullanıcı özelliği. Bu özelliği altında ayarlayabilirsiniz **kullanıcı** &gt; **profil** &gt; **ayarları** hello Azure Portalı'nda. Grup lisans atamasını kullanırken, kullanım konumu belirtilmezse herhangi bir kullanıcı hello dizininin hello konumu devralır.

tooassign lisansı altında **Azure Active Directory** &gt; **lisansları** &gt; **tüm ürünleri**, bir veya daha fazla ürünleri seçin ve ardından seçin **Atamak** hello komut çubuğunda.

![Bir lisans tooassign seçin](media/active-directory-licensing-get-started-azure-portal/select-license-to-assign.png)

Merhaba kullanabilirsiniz **kullanıcılar ve gruplar** birden çok kullanıcı veya grupları ve toodisable hizmet planları hello üründe dikey toochoose. Merhaba arama kutusunu üzerinde üst toosearch için kullanıcı ve grup adları kullanın.

![Bir kullanıcı veya grup için lisans atamasını seçin](media/active-directory-licensing-get-started-azure-portal/select-user-for-license-assignment.png)

Bir lisans tooa grubu atarken tüm kullanıcılar hello grubundaki kullanıcılar hello sayısı bağlı olarak hello lisans devralırlar önce biraz zaman alabilir. Merhaba hello işleme durumunu denetleyebilirsiniz **grup** hello altında dikey **lisansları** döşeme.

![Lisans atama durumu](media/active-directory-licensing-get-started-azure-portal/license-assignment-status.png)

Atama hataları sırasında Azure AD lisans atamasını gerçekleşebileceğini, ancak Azure AD yönetirken görece olarak daha ender ve Enterprise Mobility + güvenlik ürünleri. Olası atama hataları sınırlıdır:
- Atama çakışma: ne zaman bir kullanıcı daha önce atanma hello geçerli lisans ile uyumsuz bir lisans. Bu durumda, hello yeni lisans atama hello geçerli kaldırılması gerekir.
- Kullanılabilir lisans aşıldı: atanan gruplarındaki kullanıcılar hello sayısı hello kullanılabilir lisans aşarsa, bir kullanıcının atama durumu hatası tooassign toomissing lisansları son yansıtır.

#### <a name="azure-ad-b2b-collaboration-licensing"></a>Azure AD B2B işbirliği lisanslama

B2B işbirliği, Azure AD Kiracı tooprovide erişim tooAzure AD hizmetlerine tooinvite Konuk kullanıcılar sağlar ve Azure kaynaklarını kullanılabilir yapın.  

B2B kullanıcıları davet ve bunları Azure AD'de tooan uygulama atama için ücretsizdir. Konuk başına too10 uygulamaları yukarı kullanıcı ve 3 temel raporları da B2B işbirliği kullanıcılar için boş. Konuk kullanıcı hello ortağın Azure AD kiracısında atanmış uygun lisans varsa, bunlar sizin içinde de lisansına sahip olması.

Gerekli değildir, ancak tooprovide erişim toopaid Azure AD özellikler istiyorsanız, bu B2B Konuk kullanıcılar lisansına sahip olması gerekir ile Azure AD lisansları uygun. Lisans Ücretli bir Azure AD ile bir davet Kiracı davet tooan ek beş Konuk kullanıcılar B2B işbirliği kullanıcı hakları atamak toohello Kiracı. Senaryolar ve bilgi için bkz: [Kılavuzu lisans B2B işbirliği](active-directory-b2b-licensing.md).

### <a name="view-assigned-licenses"></a>Görünüm atanan lisansları

Atanan ve kullanılabilir lisans Özet görünümünü altında görüntülenen **Azure Active Directory** &gt; **lisansları** &gt; **tüm ürünleri**.

![Özet görünümü lisans](media/active-directory-licensing-get-started-azure-portal/view-license-summary.png)

Atanan kullanıcıların ve grupların ayrıntılı bir liste, belirli bir ürün seçildiğinde kullanılabilir. Merhaba **lisanslı kullanıcı** listesi şu anda bir lisans ve olup hello lisans doğrudan toohello kullanıcı veya gruptan devralınan varsa atandı kullanan tüm kullanıcıları gösterir.

![Lisans ayrıntıları görüntüle](media/active-directory-licensing-get-started-azure-portal/view-license-detail.png)

Benzer şekilde, hello **lisans grupları** liste toowhich lisansları atanmış tüm grupları gösterir. Bir kullanıcı veya grup tooopen hello seçin **lisansları** tüm lisanslar gösteren dikey atanan toothat nesnesi.

### <a name="remove-a-license"></a>Bir lisans Kaldır

tooremove bir lisans toohello kullanıcı veya grup gidin ve açmak hello **lisansları** döşeme. Merhaba lisans seçin ve tıklayın **kaldırmak**.

![Bir lisans Kaldır](media/active-directory-licensing-get-started-azure-portal/remove-license.png)

Bir gruptan hello kullanıcı tarafından devralınmış lisansları doğrudan kaldırılamaz. Bunun yerine, hello kullanıcı, bunlar hello lisans devralan hello grubundan kaldırın.

### <a name="extend-trials"></a>Denemeler genişletme

Deneme müşteriler uzantıları mevcut Self Servis hello Office 365 Portalı aracılığıyla kaydolma olarak. Bir müşteri yönetici toohello Office portalı gidebilirsiniz (erişim bağımlı hello Office portalı izinlerini) ve hello Azure AD Premium deneme sürümü'nü seçin. Tıklatmak hello **genişletmek deneme** bağlantısı hello uzantısı işlemi başlatır. Bir kredi kartı gereklidir, ancak değil doludur.

![Bir deneme hello Azure portal genişletme](media/active-directory-licensing-get-started-azure-portal/extend-trial-beginning.png)

## <a name="next-steps"></a>Sonraki adımlar

Merhaba makalesini okuyun hakkında daha fazla bilgi toolearn Gelişmiş senaryoları grupları aracılığıyla lisans yönetimi için [atama lisansları tooa grup](active-directory-licensing-group-assignment-azure-portal.md).

Hakkında bilgi İşte tooconfigure ve diğer Azure AD özellikleri Ücretli kullanın:

* [Self Servis parola sıfırlama](active-directory-manage-passwords.md)
* [Self Servis Grup Yönetimi](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect health](active-directory-aadconnect-health.md)
* [Azure çok faktörlü kimlik doğrulaması](../multi-factor-authentication/multi-factor-authentication.md)
* [Doğrudan lisansları satın almanızdan Azure AD Premium](http://aka.ms/buyaadp)
