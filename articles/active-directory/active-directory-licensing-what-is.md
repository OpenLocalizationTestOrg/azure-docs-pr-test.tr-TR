---
title: "Lisans Klasik Azure portalındaki Azure Active Directory Kullanıcıları | Microsoft Docs"
description: "Microsoft Azure Active Directory lisans açıklaması, nasıl çalıştığını, nasıl başlayacağınızı ve Office 365, Microsoft Intune ve Azure Active Directory Premium ve Basic sürümleri de dahil olmak üzere en iyi uygulamalar"
services: active-directory
keywords: Azure AD lisanslama
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d769e8c6-7581-43f5-a3b4-de4b1dca2344
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;H1Hack27Feb2017
ms.openlocfilehash: 9da5bb6987a9eb3398abe0d6066f1945620df9a4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-microsoft-azure-active-directory-licensing-in-the-azure-classic-portal"></a>Azure Klasik Portalı'nda ne Microsoft Azure Active Directory lisanslaması nedir?

> [!div class="op_single_selector"]
> * [Azure portal yönergeler alın](active-directory-licensing-get-started-azure-portal.md)
> * [Azure Klasik portalı bilgileri](active-directory-licensing-what-is.md)
>
>

Azure Active Directory (Azure AD), Microsoft Identity Service (Idaas) çözümü ve platform. Azure AD, Office 365, Dynamics, Microsoft Intune ve Azure gibi herhangi bir Microsoft hizmeti ile kullanılabilir olan Azure AD serbest arasında değişen teknik ve işlevsel sürümleri çeşitli sunulur (Azure AD oluşturmaz tüm tüketim ücretlerinden bu modda), Azure AD Ücretli bir Azure çok faktörlü kimlik doğrulama (MFA) yanı sıra, Enterprise Mobility Suite (EMS), Azure AD Premium ve Basic gibi sürümleri. Office 365, Microsoft Intune ve Azure AD oldukları gibi pek çok Microsoft Çevrimiçi hizmetler gibi çoğu Azure AD Ücretli sürümleri kullanıcı başına yetkilendirmeler teslim edilir. Bu durumda, hizmeti satın alma bir veya daha fazla abonelik ile temsil edilir ve her abonelik kiracınızdaki lisans satın alma öncesi sayısını içerir. Kullanıcı başına yetkilendirmeler kullanıcı ve kullanıcı için hizmet bileşenleri etkinleştirme ve ön ödemeli lisanstan tüketen ürün arasında bir bağlantı oluşturuluyor, lisans atama yoluyla sağlanır.

> [!IMPORTANT]
> Microsoft, Azure AD’yi bu makalede bahsedilen Klasik Azure Portalı yerine Azure portalındaki [Azure AD yönetim merkezini](https://aad.portal.azure.com) kullanarak yönetmenizi öneriyor. Azure AD Yönetim Merkezi'nden yönetici rolleri atamak için bkz: nasıl [kendinizin ve kullanıcılarınızın Azure AD içinde lisans](active-directory-licensing-get-started-azure-portal.md).

[Azure AD premium şimdi deneyin.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

> [!NOTE]
> Azure AD Yönetim Portalı, Azure Klasik Portalı'nın bir parçasıdır. Azure AD kullanarak tüm Azure satın alma işlemleri gerektirmez, ancak bu portalına erişim etkin bir Azure aboneliği gerektirir veya bir [Azure deneme aboneliği](https://azure.microsoft.com/pricing/free-trial/).
>
>

Azure AD hizmet özellikleri geniş kapsamlı bir genel bakış için bkz: [Azure AD nedir](active-directory-whatis.md).
[Azure AD hizmet düzeyleri hakkında daha fazla bilgi edinin](https://azure.microsoft.com/support/legal/sla/)

> [!NOTE]
> Azure Kullandıkça Öde abonelikleri farklıdır: Ayrıca dizininizde temsil ederken, bu abonelikleri Azure kaynaklarını oluşturulmasını sağlamak ve ödeme yönteminizi eşleştirebilirsiniz. Bu durumda abonelikle ilişkili hiçbir lisans sayıları vardır. Abonelik, abonelik kaynaklarını yönetmek için kullanıcıların erişimi olan kullanıcıların ilişkilendirmesini aboneliğine eşlenen Azure kaynaklarını üzerinde çalışmak için izin vererek elde edilir.
>
>

## <a name="how-does-azure-ad-licensing-work"></a>Azure AD lisanslama nasıl çalışır?
Lisans tabanlı Azure AD (yetkilendirme tabanlı), Azure AD directory/hizmet kiracınız abonelikte etkinleştirerek iş Hizmetleri. Abonelik etkinleştirildikten sonra hizmet özellikleri dizin/hizmet yöneticileri tarafından yönetilen ve lisanslı kullanıcılar tarafından kullanılır.

Satın alma veya Enterprise Mobility Suite, Azure AD Premium veya Azure AD temel etkinleştirme, dizininize abonelik geçerlilik süresi ve ön ödemeli lisansları dahil, güncelleştirilir. Abonelik bilgilerinizi durumunu, sonraki yaşam döngüsü olay ve atanan veya kullanılabilir lisans sayısını da dahil olmak üzere belirli dizin lisansları sekmesi altında Klasik Azure Portalı aracılığıyla kullanılabilir. Bu ayrıca lisans atamalarınızı yönetmek için en iyi yerdir.

Her abonelik bir veya daha fazla hizmet planları her hizmet türü dahil işlevsel düzeyini eşleme oluşur; Örneğin, Azure AD, Azure MFA, Microsoft Intune, Exchange Online veya SharePoint Online. Azure AD lisans yönetimi, hizmet planı düzeyi Yönetimi gerektirmez. Bu, eklenen hizmetlere erişimi yönetmek üzere bu Gelişmiş yapılandırma modunu kullanan bir Office 365 farklıdır. Hizmet yapılandırması özellikleri etkinleştirmek ve tek tek izinleri yönetmek için Azure AD güvenir.

Genel olarak, Azure AD abonelik bilgilerini belirli dizin lisansları sekmesi altında Azure Klasik portalı üzerinden yönetilir. Azure AD Premium, hariç olmak üzere Azure AD aboneliklerini Office Portalı'nda görünmüyor.

> [!IMPORTANT]
> Azure AD Premium ve Basic, Enterprise Mobility Suite abonelikleri yanı sıra, sağlanan kendi dizin/Kiracı sınırlandırılmıştır. Abonelikleri dizinler arasında bölme veya diğer dizinlerdeki kullanıcıları entitle için kullanılır. Bir abonelik dizinler arasında taşıma mümkündür, ancak bir destek bileti veya iptal etme ve yeniden satın alma doğrudan satın alma işlemleri söz konusu olduğunda gönderme gerektirir.
>
> Azure AD satın alırken veya Enterprise Mobility Suite aboneliği etkinleştirmesi Toplu Lisanslama üzerinden gerçekleşir otomatik olarak anlaşmayı örneğin Office 365 diğer Microsoft Online Hizmetleri zaman içerir.
>
>

Ücretli bir Azure AD özelliklerini span dizin derecesini. Örneklere şunlar dahildir:

* Yönetmekte olduğunuz belirli bir uygulamayı altında etkinleştirilmiş olan Grup tabanlı atama uygulamalar için.
* Gelişmiş ve Self Servis Grup Yönetimi Özellikleri Dizin yapılandırma bölümünde veya belirli grup içinde kullanılabilir.
* Raporlama sekmesindedir Premium güvenlik raporları
* Bulut uygulama bulma kimlik altında Azure portalında görünür.

### <a name="assigning-licenses"></a>Lisans atama
Bir aboneliği elde Ücretli özellikleri yapılandırmak için gereken her şeyi olmakla birlikte, Özellikler Ücretli Azure AD kullanarak sağ kişiler lisansları dağıtma gerektirir. Genel olarak, özellik erişimi olması gereken veya Azure AD ile yönetilen Ücretli herhangi bir kullanıcı bir lisans atanması gerekir. Lisans atama, kullanıcı ve Azure AD Premium, Basic veya Enterprise Mobility Suite gibi bir satın alınan hizmet arasındaki bir eşlemedir.

Dizininizdeki hangi kullanıcıların bir lisansı olması yönetme basit bir işlemdir. Azure AD Yönetim Portalı üzerinden atama kuralları oluşturmak için bir gruba atayarak veya portal, PowerShell veya API aracılığıyla doğrudan sağ bireylere lisans atama gerçekleştirilebilir. Lisansları bir gruba atarken, tüm Grup üyeleri lisansı atanır. Kullanıcılar eklenmiş veya gruptan kaldırılan atanacak veya uygun lisansları kaldırılamaz. Grup ataması kullanabileceğiniz herhangi bir Grup Yönetim kullanabilir ve uygulamalara grup tabanlı atama ile tutarlıdır. Bu yaklaşımı kullanarak, dizininizdeki tüm kullanıcılara otomatik olarak atanır, kurallar ayarlayabilir, uygun iş unvanı herkesle lisansına sahip olduğundan emin olun veya bile kararı kuruluştaki diğer yöneticileri temsilci.

Lisans grup tabanlı atama ile bir kullanım konumu eksik herhangi bir kullanıcı, atama sırasında dizin konumunu devralır. Bu konum yönetici tarafından herhangi bir zamanda değiştirilebilir. Otomatik atama hatası nedeniyle başarısız olduğu durumlarda, bu durumda kullanıcı bilgileri, lisans türü altında yansıtır.

## <a name="getting-started-with-azure-ad-licensing"></a>Azure AD lisansını kullanmaya başlayın
Azure AD ile çalışmaya başlama kolaydır; dizininizi ücretsiz Azure deneme için kaydolan bir parçası olarak her zaman oluşturabilirsiniz. [Kuruluş olarak kaydolma hakkında daha fazla bilgi](sign-up-organization.md). Aşağıdaki dizininize tüketen ya da kullanmak planlama diğer Microsoft Hizmetleri ve hizmet alma içinde hedeflerinize en iyi hizalanır emin olun yardımcı olabilir.

Birkaç en iyi uygulamalar şunlardır:

* Zaten Microsoft'un kuruluş hizmetlerinden herhangi birini kullanıyorsanız, Azure AD dizini zaten sahip. Bu durumda, böylece çekirdek Kimlik Yönetimi, sağlama ve karma SSO gibi hizmetleri kullanılabilir diğer hizmetler için aynı dizinde kullanmaya devam etmelidir. Kullanıcılarınız tek oturum açma deneyimine sahip olur ve daha zengin özelliklerini Hizmetleri yararlı olacaktır. Sonuç olarak, hizmeti, iş gücü için ücretli bir Azure AD satın karar verirseniz, bunu yapmak için aynı dizinde kullanmanızı öneririz.
* Farklı bir kullanıcı (iş ortakları, müşteriler vb.) veya Azure AD hizmetlerinde değerlendirmek istediğiniz ve üretim hizmetinizi yalıtım modunda yapmak istersiniz kümesi için Azure AD kullanmayı planlıyorsanız veya y sandbox ortamını kurmaya arıyorsanız hizmetlerimizi, ilk Azure Azure Klasik Portalı'nı kullanarak yeni bir dizin oluşturmanızı öneririz. [Yeni bir oluşturma hakkında daha fazla bilgi Klasik Azure portalındaki Azure AD dizini](active-directory-licensing-directory-independence.md). Yeni dizin hesabınızla genel yönetici izinlerine sahip bir dış kullanıcı olarak oluşturulur. Azure Klasik Portalı'nı bu hesapla oturum açın, bu dizin bakın ve tüm dizin yönetim görevleri erişebilir hale gelir. Diğer Microsoft Hizmetleri (olanlar Klasik Azure portalı üzerinden erişilemiyor) yönetmek için gerekli ayrıcalıklara sahip bir yerel hesap oluşturmanızı öneririz. [Azure AD'de kullanıcı hesapları oluşturma hakkında daha fazla bilgi](active-directory-create-users.md).

> [!NOTE]
> Azure AD "Microsoft hesabı (MSA) veya başka bir dizindeki bir Azure AD kimlik kullanılarak oluşturulan Azure ad örneğinde kullanıcı hesapları olan dış kullanıcılar," destekler. Biz meşgul durumdayken tüm Microsoft'un Kuruluş Hizmetleri, bu özellik şu anda bu genişletme hesapları bazı hizmetleri deneyimleri desteklenmez; Örneğin, Office 365 Yönetim Portalı'nı bu kullanıcılar şu anda desteklemiyor. Sonuç olarak, harici kullanıcılar Microsoft hesabı olan diğer Azure AD dizinlerinden dış kullanıcılar yoksayılacak sırada Office 365 Yönetim Portalı'nı hiç erişebilir olmaz. İkinci durumda, yalnızca kullanıcının yerel hesabı, Azure AD veya kullanıcı ilk olarak oluşturulduğu, Office 365 directory bu deneyimleriyle erişilebilir olacaktır.
>
>

Gösterildiği gibi Azure AD farklı Ücretli sürümlerini içerir. Bu sürümleri, satın alma kullanılabilirliklerini bazı küçük farklılıklar vardır:

| Ürün | EA/TOPLU LİSANS | Açık | CSP | MPN kullanım hakları | Doğrudan satın alma | Deneme |
| --- | --- | --- | --- | --- | --- | --- |
| Enterprise Mobility Suite |X |X |X |X | |X |
| Azure AD Premium |X |X |X | |X |X |
| Azure AD Basic |X |X |X |X |<br /> |<br /> |

### <a name="select-one-or-more-license-trials"></a>Bir veya daha fazla lisans denemeler seçin
 Her durumda, dizininizde lisansları sekmesinde istediğiniz belirli deneme seçerek Azure AD Premium veya Enterprise Mobility Suite deneme aboneliği etkinleştirebilirsiniz. Ya da deneme 100 lisanstan 30 günlük abonelikle içerir.

![Azure Active Directory deneme lisans planları](./media/active-directory-licensing-what-is/trial_plans.png)

![Enterprise Mobility Suite deneme lisans planları](./media/active-directory-licensing-what-is/EMS_trial_plan.png)

![Etkin deneme lisans planları](./media/active-directory-licensing-what-is/active_license_trials.png)

### <a name="assign-licenses"></a>Lisans atama
Abonelik etkinleştirildikten sonra lisans kendinize atamak ve tüm özellikleri görmesini sağlamak için tarayıcıyı yenileyin. Erişim ya da dahil edilmesi gereken kullanıcılara lisans atamak için Azure AD özelliklerini Ücretli sonraki adımdır. Biz "Atama lisansları" Yukarıdaki, bunu yapmak için en iyi yolu istediğiniz hedef kitle temsil eden tanımlayın ve lisansı atamak için aynıdır; Bu şekilde, kullanıcılar eklendiğinde veya gruptan kendi ömrü kaldırıldığında atanan veya kaldırılacak lisansı kaldırıldı.

Bir grup veya bireysel kullanıcılar için bir lisans atamak için tıklatıp atamak istediğiniz lisans planı seçin **atamak** komut çubuğunda.

![Etkin deneme lisans planları](./media/active-directory-licensing-what-is/assign_licenses.png)

Seçili plan için atama iletişim kutusunda, kullanıcıların ve bunlara ekleme seçebilirsiniz sonra **atamak** sağdaki sütun. Sayfa kullanıcı listesini ya da üst arayan kullanarak belirli kişiler cam arama kullanıcı kılavuzunun sağ. Grupları atamak için "Grupları" seçin **Göster** menüsünü seçin ve ardından onay düğmesine sağ tarafta görüntülenen atamaları yenilemek için.

![Lisans gruplarına atama](./media/active-directory-licensing-what-is/assign_licenses_to_groups.png)

Şimdi arayabilirsiniz veya sayfa aracılığıyla gruplarını ve bunları Ekle **atamak** aynı şekilde sütun. Bu, kullanıcıları ve grupları tek bir işlemle bir birleşimini atamak için kullanabilirsiniz. Atama işlemi tamamlamak için sayfanın sağ alt köşesindeki onay düğmesini tıklatın.

![Lisans atama ilerleme iletisi](./media/active-directory-licensing-what-is/license_assignment_progress_message.png)

Bir grup atandığında, üyelerine lisanslar 30 dakika içinde ancak genellikle 1-2 dakika içinde devralır.

Atama hataları Azure AD lisans atama sırasında meydana gelir, ancak görece olarak daha ender. Olası atama hataları sınırlıdır:

* Bir kullanıcı daha önce olduğu zaman atama çakışma - geçerli lisansı ile uyumsuz bir lisansı atanır. Bu durumda, yeni lisans atama öncekinin kaldırma gerektirir.
* İçin atanan gruplarındaki kullanıcılar kullanılabilir lisans sayısını zaman aşıldı kullanılabilir lisans - bir hata nedeniyle eksik lisansları atamak için kullanıcıların atama durumu yansıtır.

### <a name="view-assigned-licenses"></a>Görünüm atanan lisansları
Kullanılabilir, atanan ve sonraki abonelik yaşam döngüsü olay dahil olmak üzere atanan lisansları Özet görünümünü görüntülenir **lisansları** sekmesi.

![Atanan lisans sayısını görüntülemek](./media/active-directory-licensing-what-is/view_assigned_licenses.png)

Ayrıntılı bir liste atanan kullanıcıların ve grupların atama durumu ve yol (doğrudan veya bir veya daha fazla gruplarından devralınan) dahil olmak üzere bir lisans planına gezinirken kullanılabilir.

![İçin bir lisans planı atanan lisansları ayrıntı görünümünü](./media/active-directory-licensing-what-is/assigned_licenses_detail.png)

Lisanslar kaldırılıyor atama olarak oldukça kolaydır. Kullanıcının doğrudan atanmış veya atanmış bir grubu için lisans lisans türü seçerek kaldırabilirsiniz, seçme **kaldırmak**, kullanıcı veya grup Kaldır listesine ekleme ve eylem onaylama. Alternatif olarak, bir lisans türü açabilir, belirli kullanıcı veya grup seçin ve dokunun **kaldırmak** komut çubuğunda. Bir kullanıcının devralma bir gruptan bir lisans sona erdirmek için kullanıcıyı gruptan kaldırın.

### <a name="extending-trials"></a>Denemeler genişletme
Müşteriler için deneme uzantıları kullanılabilir olarak Self Servis Office 365 Portalı aracılığıyla. Bir müşteri yönetici gidebilirsiniz [Office portalı](https://portal.office.com/#Billing) (erişim bağımlı Office portalı izinlerini) ve Azure AD Premium deneme sürümünü seçin. Tıklatın **genişletmek deneme** bağlamak ve yönergeleri izleyin. Bir kredi kartı girmeniz gerekir, ancak değil ücretlendirilir.

![Office portalında lisans deneme genişletme](./media/active-directory-licensing-what-is/extend_license_trial.png)

Müşterilerin bir destek isteği göndererek deneme uzantısı da isteğinde bulunabilirsiniz. Bir müşteri yönetici Office 365 portalına gidebilirsiniz [destek sayfası](http://aka.ms/extendAADtrial) (erişim bağımlı Office destek sayfası izinlerini). Bu sayfada "Abonelikleri ve deneme" Özellikler altında seçin ve belirti altında "deneme soruları". Son olarak, koşullar hakkında bilgileri girin

![Bir destek isteği kullanarak bir lisans deneme genişletme](./media/active-directory-licensing-what-is/alternate_office_aad_trial_extension.png)

## <a name="next-steps"></a>Sonraki adımlar
Şimdi yapılandırmak ve bazı Azure AD Premium özellikleri kullanmak hazır olması.

* [Self Servis parola sıfırlama](active-directory-manage-passwords.md)
* [Self Servis Grup Yönetimi](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect sistem durumu](active-directory-aadconnect-health.md)
* [Grup ataması uygulamalar](active-directory-manage-groups.md)
* [Azure çok faktörlü kimlik doğrulaması](../multi-factor-authentication/multi-factor-authentication.md)
* [Doğrudan lisansları satın almanızdan Azure AD Premium](http://aka.ms/buyaadp)
