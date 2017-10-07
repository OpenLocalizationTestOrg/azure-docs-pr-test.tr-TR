---
title: "Merhaba Klasik Azure portalı aaaLicense Azure Active Directory Kullanıcılar | Microsoft Docs"
description: "Microsoft Azure Active Directory lisans açıklaması, nasıl çalıştığını, tooget nasıl başlatılacağını ve Office 365, Microsoft Intune ve Azure Active Directory Premium ve Basic sürümleri de dahil olmak üzere en iyi uygulamalar"
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
ms.openlocfilehash: 4d5f244cbee2ae37a30976f70b5d4f21c3516d90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-microsoft-azure-active-directory-licensing-in-hello-azure-classic-portal"></a>Ne hello Klasik Azure Portalı Microsoft Azure Active Directory lisanslaması nedir?

> [!div class="op_single_selector"]
> * [Azure portal yönergeler alın](active-directory-licensing-get-started-azure-portal.md)
> * [Azure Klasik portalı bilgileri](active-directory-licensing-what-is.md)
>
>

Azure Active Directory (Azure AD), Microsoft Identity Service (Idaas) çözümü ve platform. Azure AD, Office 365, Dynamics, Microsoft Intune ve Azure gibi herhangi bir Microsoft hizmeti ile kullanılabilir olan Azure AD serbest arasında değişen teknik ve işlevsel sürümleri çeşitli sunulur (Azure AD oluşturmaz tüm tüketim ücretlerinden bu modda), tooAzure AD Ücretli bir Azure çok faktörlü kimlik doğrulama (MFA) yanı sıra, Enterprise Mobility Suite (EMS), Azure AD Premium ve Basic gibi sürümleri. Office 365, Microsoft Intune ve Azure AD oldukları gibi pek çok Microsoft Çevrimiçi hizmetler gibi çoğu Azure AD Ücretli sürümleri kullanıcı başına yetkilendirmeler teslim edilir. Bu durumda, hello hizmeti satın alma bir veya daha fazla abonelik ile temsil edilir ve her abonelik kiracınızdaki lisans satın alma öncesi sayısını içerir. Kullanıcı başına yetkilendirmeler hello kullanıcı hem de hello Hizmeti bileşenlerinin hello kullanıcı etkinleştirme hello ürün arasında bir bağlantı oluşturuluyor, lisans atamasını aracılığıyla elde edilir ve lisansları ön ödemeli hello birini kullanma.

> [!IMPORTANT]
> Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı. Nasıl tooassign Yönetici rolü hello Azure AD Yönetim Merkezi için bkz: [kendinizin ve kullanıcılarınızın Azure AD içinde lisans](active-directory-licensing-get-started-azure-portal.md).

[Azure AD premium şimdi deneyin.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

> [!NOTE]
> Azure AD yönetim portalında hello Klasik Azure portalı, bir parçasıdır. Azure AD kullanarak tüm Azure satın alma işlemleri gerektirmez, ancak bu portalına erişim etkin bir Azure aboneliği gerektirir veya bir [Azure deneme aboneliği](https://azure.microsoft.com/pricing/free-trial/).
>
>

Azure AD hizmet özellikleri geniş kapsamlı bir genel bakış için bkz: [Azure AD nedir](active-directory-whatis.md).
[Azure AD hizmet düzeyleri hakkında daha fazla bilgi edinin](https://azure.microsoft.com/support/legal/sla/)

> [!NOTE]
> Azure Kullandıkça Öde abonelikleri farklıdır: Ayrıca dizininizde temsil ederken, bu abonelikleri Azure kaynaklarını oluşturulmasını sağlamak ve tooyour ödeme yöntemini eşleştirebilirsiniz. Bu durumda hello abonelikle ilişkili hiçbir lisans sayıları vardır. Kullanıcıların ilişkilendirme hello aboneliğiyle hello kullanıcıların erişim toomanaging, abonelik kaynakları, izinleri toooperate eşlenen Azure kaynaklarını toohello abonelikte vererek elde edilir.
>
>

## <a name="how-does-azure-ad-licensing-work"></a>Azure AD lisanslama nasıl çalışır?
Lisans tabanlı Azure AD (yetkilendirme tabanlı), Azure AD directory/hizmet kiracınız abonelikte etkinleştirerek iş Hizmetleri. Merhaba abonelik etkinleştirildikten sonra hello hizmet özellikleri dizin/hizmet yöneticileri tarafından yönetilen ve lisanslı kullanıcılar tarafından kullanılır.

Ne zaman satın alma veya Enterprise Mobility Suite, Azure AD Premium veya Azure AD temel, dizininize etkinleştirme geçerlilik süresinin dahil olmak üzere hello abonelikle güncelleştirilir ve lisansları ön ödemeli. Abonelik bilgilerinizi durumunu, sonraki yaşam döngüsü olay ve hello atanmış veya kullanılabilir lisans sayısını da dahil olmak üzere hello hello belirli dizin için hello lisansları sekmesi altında Klasik Azure Portalı aracılığıyla kullanılabilir. Bu aynı zamanda, lisans anlaşmalarını toobest yer toomanage olan.

Bir veya daha fazla hizmet planları her abonelik oluşur, işlev düzeyi hello hizmet türüne ilişkin her eşleme hello dahil; Örneğin, Azure AD, Azure MFA, Microsoft Intune, Exchange Online veya SharePoint Online. Azure AD lisans yönetimi, hizmet planı düzeyi Yönetimi gerektirmez. Bu, bu Gelişmiş Yapılandırma modu toomanage erişim tooincluded hizmetlerini kullanan Office 365 farklıdır. Azure AD tooenable özellikleri, hizmet yapılandırmasını kullanır ve tek tek izinleri yönetin.

Genel olarak, abonelik bilgileri Azure AD'ye hello hello belirli dizin için hello lisansları sekmesi altında Klasik Azure portalı üzerinden yönetilir. Merhaba özel Azure AD Premium, Azure AD aboneliklerini hello Office Portalı'nda görünmüyor.

> [!IMPORTANT]
> Azure AD Premium ve Basic, Enterprise Mobility Suite abonelikleri yanı sıra, yalıtılmış tootheir sağlanan dizin/Kiracı şunlardır. Abonelikler, dizinleri veya diğer dizinlerde kullanılan tooentitle kullanıcılar arasında bölünemez. Bir abonelik dizinler arasında taşıma mümkündür, ancak bir destek bileti veya iptal etme ve yeniden satın alma doğrudan satınalma hello durumda gönderme gerektirir.
>
> Azure AD satın alırken veya Enterprise Mobility Suite aboneliği etkinleştirmesi Toplu Lisanslama üzerinden gerçekleşir otomatik olarak zaman diğer Microsoft Online Hizmetleri, örneğin Office 365 hello anlaşması içerir.
>
>

Azure AD özelliklerini hello dizin aralık hello derecesini Ücretli. Örneklere şunlar dahildir:

* Grup tabanlı atama tooapplications hello belirli uygulama yönettiğiniz altında etkinleştirilir.
* Gelişmiş ve Self Servis Grup Yönetimi özellikleri hello dizin yapılandırma bölümünde veya hello belirli bir grup içinde kullanılabilir.
* Merhaba raporlama sekmesindedir Premium güvenlik raporları
* Bulut uygulama bulma hello Azure portal kimlik altında görüntülenir.

### <a name="assigning-licenses"></a>Lisans atama
Bir aboneliği elde tüm yetenekleri Ücretli tooconfigure ihtiyacınız olsa da, özellikleri Ücretli Azure AD kullanarak lisansları toohello sağ kişiler dağıtma gerektirir. Genel olarak, özellik Ücretli bir Azure AD ile yönetilen erişim tooor olmalıdır herhangi bir kullanıcı bir lisans atanması gerekir. Lisans atama, kullanıcı ve Azure AD Premium, Basic veya Enterprise Mobility Suite gibi bir satın alınan hizmet arasındaki bir eşlemedir.

Dizininizdeki hangi kullanıcıların bir lisansı olması yönetme basit bir işlemdir. Atama kuralları hello Azure AD Yönetim Portalı üzerinden tooa Grup toocreate atayarak veya lisans toohello sağ kişiler portal, PowerShell veya API aracılığıyla doğrudan atama gerçekleştirilebilir. Lisansları tooa Grup atarken, tüm Grup üyeleri lisansı atanır. Kullanıcıların eklediyseniz veya hello grubundan kaldırılmış kullanıcılar atanmış veya kaldırılan hello uygun lisans. Grup ataması tüm Grup Yönetimi kullanılabilir tooyou kullanabilir ve grup tabanlı atama tooapplications ile tutarlıdır. Bu yaklaşımı kullanarak, dizininizdeki tüm kullanıcılara otomatik olarak atanır, kurallar ayarlayabilir, hello uygun iş unvanı herkesle lisansına sahip olduğundan emin olun veya bile hello karar tooother yöneticileri hello kuruluşunuzdaki temsilci.

Lisans grup tabanlı atama ile bir kullanım konumu eksik herhangi bir kullanıcı, atama sırasında hello dizin konumunu devralır. Bu konum, herhangi bir zamanda hello Yöneticisi tarafından değiştirilebilir. Burada hello otomatik ataması nedeniyle başarısız oldu durumlarda tooerror, hello kullanıcı bilgileri altında lisans türü bu durumu yansıtır.

## <a name="getting-started-with-azure-ad-licensing"></a>Azure AD lisansını kullanmaya başlayın
Azure AD ile çalışmaya başlama kolaydır; dizininizi tooa ücretsiz Azure deneme sürümü imzalama bir parçası olarak her zaman oluşturabilirsiniz. [Kuruluş olarak kaydolma hakkında daha fazla bilgi](sign-up-organization.md). Merhaba aşağıdaki dizininize tüketen ya da tooconsume ve hello hizmet alma içinde hedeflerinizi planlama diğer Microsoft Hizmetleri ile en iyi hizalanır emin olun yardımcı olabilir.

Birkaç en iyi uygulamalar şunlardır:

* Zaten Microsoft'un kuruluş hizmetlerinden herhangi birini kullanıyorsanız, Azure AD dizini zaten sahip. Bu durumda, devam etmelidir toouse hello diğer hizmetler için aynı dizinde böylece çekirdek Kimlik Yönetimi, sağlama ve karma SSO gibi hello Hizmetleri kullanılabilir. Kullanıcılarınız tek oturum açma deneyimine sahip olur ve daha zengin özelliklerini hello Hizmetleri yararlı olacaktır. Azure AD bir toobuy hizmeti, iş gücü için ücretli karar verirseniz, sonuç olarak, kullanmanızı öneririz aynı dizin toodo bu hello.
* Toouse farklı bir kullanıcı (iş ortakları, müşteriler vb.) kümesini için Azure AD planlıyorsanız veya tooevaluate Azure AD Hizmetleri istersiniz ve toodo istersiniz, üretim hizmetinizin yalıtım veya toosetup bir korumalı alan ortamıdır arıyorsanız hizmetlerinizin için yeni bir dizin hello Azure Azure Klasik portalı üzerinden ilk oluşturmanızı öneririz. [Yeni bir oluşturma hakkında daha fazla bilgi hello Klasik Azure portalında Azure AD dizininde](active-directory-licensing-directory-independence.md). Merhaba yeni dizin hesabınızla genel yönetici izinlerine sahip bir dış kullanıcı olarak oluşturulur. Toohello Azure klasik oturum açtığınızda bu hesapla portal, mümkün toosee bu dizin ve olması tüm dizin yönetim görevleri erişim. Diğer Microsoft Hizmetleri (olanlar hello Klasik Azure portalı erişilebilir değil) uygun ayrıcalıkları toomanage ile yerel bir hesap oluşturmanızı öneririz. [Azure AD'de kullanıcı hesapları oluşturma hakkında daha fazla bilgi](active-directory-create-users.md).

> [!NOTE]
> Azure AD "Microsoft hesabı (MSA) veya başka bir dizindeki bir Azure AD kimlik kullanılarak oluşturulan Azure ad örneğinde kullanıcı hesapları olan dış kullanıcılar," destekler. Biz meşgul durumdayken tüm Microsoft'un Kuruluş Hizmetleri, bu özellik şu anda bu genişletme hesapları hello Hizmetleri deneyimleri bazıları desteklenmez; Örneğin, hello Office 365 Yönetim Portalı, bu kullanıcılar şu anda desteklemiyor. Diğer Azure AD dizinlerinden dış kullanıcılar yoksayılacak sırada Sonuç olarak, Microsoft hesaplarıyla dış kullanıcılar mümkün tooaccess hello Office 365 Yönetim Portalı hiç olmaz. Merhaba ikinci durumda, yalnızca hello kullanıcının yerel hesabı, hello Azure AD veya Office 365 hello kullanıcı ilk olarak oluşturulduğu, dizin olacaktır bu deneyimler erişilebilir.
>
>

Gösterildiği gibi Azure AD farklı Ücretli sürümlerini içerir. Bu sürümleri, satın alma kullanılabilirliklerini bazı küçük farklılıklar vardır:

| Ürün | EA/TOPLU LİSANS | Açık | CSP | MPN kullanım hakları | Doğrudan satın alma | Deneme |
| --- | --- | --- | --- | --- | --- | --- |
| Enterprise Mobility Suite |X |X |X |X | |X |
| Azure AD Premium |X |X |X | |X |X |
| Azure AD Basic |X |X |X |X |<br /> |<br /> |

### <a name="select-one-or-more-license-trials"></a>Bir veya daha fazla lisans denemeler seçin
 Her durumda, dizininizde hello lisansları sekmesinde istediğiniz hello belirli deneme seçerek Azure AD Premium veya Enterprise Mobility Suite deneme aboneliği etkinleştirebilirsiniz. Ya da deneme 100 lisanstan 30 günlük abonelikle içerir.

![Azure Active Directory deneme lisans planları](./media/active-directory-licensing-what-is/trial_plans.png)

![Enterprise Mobility Suite deneme lisans planları](./media/active-directory-licensing-what-is/EMS_trial_plan.png)

![Etkin deneme lisans planları](./media/active-directory-licensing-what-is/active_license_trials.png)

### <a name="assign-licenses"></a>Lisans atama
Merhaba abonelik etkinleştirildikten sonra lisans tooyourself atayın ve tüm özelliklerinizi görüyorsunuz hello tarayıcı tooensure yenileyin. Merhaba sonraki tooassign lisansları adımdır tooaccess gerekir veya dahil edilmesini toohello kullanıcılar Ücretli Azure AD özellikleri. Biz yukarıda "Atama lisansları," Merhaba en iyi şekilde toodo bu belirtildiği gibi tooidentify hello Grup istenen hello İzleyici temsil eden ve toohello lisans atama; Bu şekilde, eklenen veya kendi ömrü hello grubundan kaldırılmış kullanıcıların hello lisanstan kaldırılan tooor atanır.

tooassign lisans tooa grubu veya bireysel kullanıcılar, select hello ve gibi tooassign tıklatın lisans planı **atamak** hello komut çubuğunda.

![Etkin deneme lisans planları](./media/active-directory-licensing-what-is/assign_licenses.png)

Merhaba seçili plan için Hello atama iletişim kutusunda, kullanıcıları ve toohello eklemeyi seçebilir sonra **atamak** hello sağ sütun. Sayfa hello kullanıcı listesi veya üzerinde hello hello arayan kullanarak belirli kişiler cam arama hello kullanıcı kılavuzunun sağ üst. tooassign grupları, seçin "Grupları" Merhaba **Göster** menüsünü ve sonra görüntülenen hello sağ toorefresh hello atamaları hello onay düğmesine tıklayın.

![Lisansları toogroups atama](./media/active-directory-licensing-what-is/assign_licenses_to_groups.png)

Şimdi arayabilirsiniz veya sayfa aracılığıyla gruplarını ve bunları toohello Ekle **atamak** hello sütununda aynı şekilde. Tek bir işlemde bu tooassign kullanıcıların ve grupların bileşimini kullanabilirsiniz. toocomplete Merhaba atama işlemi, hello hello hello sayfanın sağ alt köşesindeki onay düğmesini tıklatın.

![Lisans atama ilerleme iletisi](./media/active-directory-licensing-what-is/license_assignment_progress_message.png)

Bir grup atandığında, üyelerine hello lisansları 30 dakika içinde ancak genellikle 1-2 dakika içinde devralır.

Atama hataları Azure AD lisans atama sırasında meydana gelir, ancak görece olarak daha ender. Olası atama hataları sınırlıdır:

* Bir kullanıcı daha önce olduğu zaman atama çakışma - hello geçerli lisans ile uyumsuz bir lisansı atanır. Bu durumda, hello yeni lisans atama hello öncekinin kaldırma gerektirir.
* Merhaba atanan gruplarındaki kullanıcılar kullanılabilir lisans sayısını zaman aşıldı kullanılabilir lisans - hata tooassign toomissing lisansları son hello kullanıcıların atama durumu yansıtır.

### <a name="view-assigned-licenses"></a>Görünüm atanan lisansları
Kullanılabilir, atanan ve sonraki abonelik yaşam döngüsü olay dahil olmak üzere atanan lisansları Özet görünümünü hello üzerinde görüntülenen **lisansları** sekmesi.

![Görünüm hello atanan lisans sayısı](./media/active-directory-licensing-what-is/view_assigned_licenses.png)

Ayrıntılı bir liste atanan kullanıcıların ve grupların atama durumu ve yol (doğrudan veya bir veya daha fazla gruplarından devralınan) dahil olmak üzere bir lisans planına gezinirken kullanılabilir.

![İçin bir lisans planı atanan lisansları ayrıntı görünümünü](./media/active-directory-licensing-what-is/assigned_licenses_detail.png)

Lisanslar kaldırılıyor atama olarak oldukça kolaydır. Merhaba kullanıcı doğrudan atanmış veya atanmış bir grubu için hello lisans türünü seçerek hello lisans kaldırabilirsiniz, seçme **kaldırmak**hello kullanıcı veya grup toohello Kaldır listesi ekleme ve hello eylem onaylama. Alternatif olarak, lisans türü, select hello belirli bir kullanıcı veya grup açabilir ve dokunun **kaldırmak** hello komut çubuğunda. tooend bir gruptan bir lisans, bir kullanıcının devralma yalnızca hello kullanıcı hello grubundan kaldırın.

### <a name="extending-trials"></a>Denemeler genişletme
Müşteriler için deneme uzantıları kullanılabilir olarak Self Servis hello Office 365 Portalı aracılığıyla. Bir müşteri yönetici toohello gidebilirsiniz [Office portalı](https://portal.office.com/#Billing) (erişim bağımlı hello Office portalı izinlerini) ve Azure AD Premium deneme sürümünü seçin. Merhaba tıklatın **genişletmek deneme** bağlamak ve hello yönergeleri izleyin. Tooenter bir kredi kartı gerekir, ancak değil ücretlendirilir.

![Bir lisans deneme hello Office portalında genişletme](./media/active-directory-licensing-what-is/extend_license_trial.png)

Müşterilerin bir destek isteği göndererek deneme uzantısı da isteğinde bulunabilirsiniz. Bir müşteri yönetici toohello Office 365 portalı gidebilirsiniz [destek sayfası](http://aka.ms/extendAADtrial) (erişim bağımlı hello Office destek sayfası izinlerini). Bu sayfada "Abonelikleri ve deneme" Özellikler altında seçin ve belirti altında "deneme soruları". Son olarak, hello koşullar hakkında bilgileri girin

![Bir destek isteği kullanarak bir lisans deneme genişletme](./media/active-directory-licensing-what-is/alternate_office_aad_trial_extension.png)

## <a name="next-steps"></a>Sonraki adımlar
Şimdi hazır tooconfigure olması ve bazı Azure AD Premium özellikleri kullanır.

* [Self Servis parola sıfırlama](active-directory-manage-passwords.md)
* [Self Servis Grup Yönetimi](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect sistem durumu](active-directory-aadconnect-health.md)
* [Grup ataması tooapplications](active-directory-manage-groups.md)
* [Azure çok faktörlü kimlik doğrulaması](../multi-factor-authentication/multi-factor-authentication.md)
* [Doğrudan lisansları satın almanızdan Azure AD Premium](http://aka.ms/buyaadp)
