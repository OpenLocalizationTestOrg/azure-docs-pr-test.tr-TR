---
title: "Ayrıca, Azure Automation ile Başlarken | Microsoft Docs"
description: "Bu makalede, Azure Marketi'nden sunumu hazırlık tooonboard hello hello tasarım ve uygulama ayrıntıları gözden geçirerek Azure Otomasyon hizmetine genel bir bakış sağlar."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 434e8ea28c55ff9bda1d2e46a7a6b8378a3baa0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation"></a>Azure Otomasyonu’nu Kullanmaya Başlama

Bu başlangıç kılavuzuna temel kavramları ilgili toohello Azure Otomasyonu dağıtımını tanıtır. Azure'da yeni tooAutomation olan veya System Center Orchestrator gibi Otomasyon iş akışı yazılım deneyimiyle varsa, bu kılavuz anlamanıza yardımcı olur nasıl tooprepare ve yerleşik Otomasyon.  Daha sonra runbook'ları işlemi Otomasyon gerekliliklerini desteklemek geliştirme toobegin hazır. 


## <a name="automation-architecture-overview"></a>Otomasyon mimarisine genel bakış

![Azure Automation’a genel bakış](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Azure Otomasyonu, ölçeklenebilir ve güvenilir bir çok kiracılı sağlayan bir hizmet (SaaS) uygulaması bir yazılım olduğu ortam tooautomate işler runbook'larla ve yapılandırma değişiklikleri tooWindows ve istenen durum yapılandırması kullanarak Linux sistemlerini yönetme (DSC) Azure, bulut Hizmetleri ya da şirket içi. Otomasyon hesabınızda bulunan runbook, varlık ve Farklı Çalıştır hesapları gibi varlıklar, aboneliğinizdeki ve diğer aboneliklerdeki başka Otomasyon hesaplarından yalıtılır.  

Azure'da çalıştırdığınız runbook'lar, Azure hizmet olarak platform (PaaS) sanal makinelerinde barındırılan Otomasyon korumalı alanı üzerinde yürütülür.  Otomasyon korumalı alanları, runbook yürütme işleminin tüm yönleri için (modüller, depolama, bellek, ağ iletişimi, iş akışları vb.) kiracı yalıtımı sağlar. Bu rolü hello hizmeti tarafından yönetiliyor ve Azure veya Azure Automation hesabınız, toocontrol için erişilebilir değil.         

tooautomate hello dağıtım ve yönetim yerel veri merkeziniz ya da bir Otomasyon hesabı oluşturduktan sonra diğer bulut hizmetlerine kaynakların bir veya daha fazla makineler toorun hello belirleyebilirler [karma Runbook çalışanı (HRW)](automation-hybrid-runbook-worker.md) rol.  Her HRW hello Microsoft Yönetim Aracısı bağlantısı tooa günlük analizi çalışma alanı ve bir Otomasyon hesabı gerektirir.  Günlük analizi kullanılan toobootstrap hello yükleme korumak hello Microsoft Yönetim aracısı ve hello HRW hello işlevselliğini izleyin.  runbook'ları teslimini hello ve bunları Azure Automation tarafından gerçekleştirilen yönerge toorun hello.

Birden çok HRW tooprovide yüksek kullanılabilirlik için runbook'ları dağıtmak, Yük Dengeleme runbook işleri ve belirli iş yükleri veya ortamlar için bazı durumlarda bunları ayrılması.  Merhaba Microsoft İzleme Aracısı hello HRW üzerinde TCP bağlantı noktası 443 hello Otomasyon hizmeti ile iletişim başlatır ve gelen güvenlik duvarı gereksinimi yoktur.  Bir HRW hello ortamında çalışan runbook varsa ve istediğiniz diğer makineler veya hizmetler bu ortam içinde karşı hello runbook tooperform yönetim görevleri, olabilir sonra hello diğer bağlantı noktası olarak runbook erişimi olmalıdır.  BT güvenlik ilkeleri, ağ tooconnect toohello Internet bilgisayarları izin vermiyorsa hello makalesini inceleyin [OMS ağ geçidi](../log-analytics/log-analytics-oms-gateway.md), hangi hello HRW toocollect için bir proxy olarak görev yapar iş durumu ve yapılandırma bilgilerini alma Otomasyon hesabınızı.

Merhaba bilgisayardaki yerel sistem hesabı hello hello bağlamında çalıştırın HRW üzerinde çalışan Runbook'lar, hangi hello güvenlik bağlamı hello yerel Windows makinesinde yönetici eylemleri gerçekleştirirken önerilir. Merhaba runbook toorun görevleri hello yerel makine dışında kaynaklara karşı istiyorsanız hello hello runbook'tan erişmek ve tooauthenticate hello dış kaynak ile kullanmak Otomasyon hesabı toodefine güvenli kimlik bilgisi varlıkları gerekebilir. Kullanabileceğiniz [kimlik bilgisi](automation-credentials.md), [sertifika](automation-certificates.md), ve [bağlantı](automation-connections.md) runbook'unuzda bunları doğrulanabilir şekilde toospecify kimlik bilgilerine izin ver cmdlet'leri ile varlıklar.

DSC yapılandırmaları Azure Otomasyonu'nda depolanan doğrudan uygulanan tooAzure sanal makineler olabilir. Diğer fiziksel ve sanal makine yapılandırmaları hello Azure Otomasyonu DSC istek sunucusundan isteyebilir.  Sistemlerinizin şirket içi fiziksel veya sanal Windows ve Linux yapılandırmaları yönetmek için tüm altyapı toosupport hello Otomasyonu DSC istek sunucusuyla, yalnızca giden Internet erişimden Automation DSC tarafından yönetilen her sistem toobe toodeploy gerekmez , TCP bağlantı noktası 443 toohello OMS hizmeti iletişim.   

## <a name="prerequisites"></a>Ön koşullar

### <a name="automation-dsc"></a>Automation DSC
Azure Otomasyonu DSC kullanılan toomanage çeşitli makineler olabilir:

* Windows veya Linux çalıştıran Azure sanal makineleri (klasik)
* Windows veya Linux çalıştıran Azure sanal makineleri
* Windows veya Linux çalıştıran Amazon Web Services (AWS) sanal makineleri
* Şirket içinde veya Azure ya da AWS dışındaki bir bulutta bulunan fiziksel/sanal Windows bilgisayarları
* Şirket içinde veya Azure ya da AWS dışındaki bir bulutta bulunan fiziksel/sanal Linux bilgisayarları

WMF 5 en son sürümünü Hello hello PowerShell DSC Aracısı Windows toobe mümkün toocommunicate Azure otomasyonu için yüklenmelidir. Merhaba en son sürümünü Hello [Linux için PowerShell DSC Aracısı](https://www.microsoft.com/en-us/download/details.aspx?id=49150) Linux toobe mümkün toocommunicate Azure otomasyonu için yüklü olmalıdır.

### <a name="hybrid-runbook-worker"></a>Karma Runbook Çalışanı  
Bir bilgisayar toorun karma runbook işleri atandığında, bu bilgisayar hello şunlara sahip olmanız gerekir:

* Windows Server 2012 veya üzeri
* Windows PowerShell 4.0 veya üzeri.  Daha fazla güvenilirlik için hello bilgisayarda Windows PowerShell 5.0 yüklemenizi öneririz. Hello hello yeni sürümü indirebilirsiniz [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=50395)
* En az iki çekirdek
* En az 4 GB RAM

### <a name="permissions-required-toocreate-automation-account"></a>Toocreate Otomasyon hesabı gereken izinler
Bu konuda toocomplete gereken izinler ve toocreate veya güncelleştirme Automation hesabı, belirli ayrıcalıkları aşağıdaki hello sahip olmalıdır.   
 
* Sipariş toocreate bir Otomasyon hesabı'da, AD kullanıcı hesabınızın toobe eklenen tooa izinleri eşdeğer toohello sahip rolünü rolüyle Microsoft.Automation kaynaklar için makalesinde ana hatlarıyla gereken [Azure automation'da rol tabanlı erişim denetimi ](automation-role-based-access-control.md).  
* Merhaba uygulama kayıtlar ayarı ayarlarsanız çok**Evet**, Azure AD kiracınızda yönetici olmayan kullanıcılar [AD uygulamaları kaydetmek](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions).  Merhaba uygulama kayıtlar ayarı ayarlarsanız çok**Hayır**, hello kullanıcının bu eylemi gerçekleştirmeden Azure AD genel yönetici olması gerekir. 

Toohello genel yönetici/co-administrator rolüne hello abonelik eklenmeden önce hello aboneliğinin Active Directory örneğine üyesi değilseniz, tooActive dizinine konuk olarak eklenir. Bu durumda, bir "sahip olmadığınız izinleri toocreate..." alırsınız. Merhaba üzerinde uyarı **Automation hesabı Ekle** dikey. Toohello genel yönetici/co-administrator rolüne ilk hello aboneliğinin Active Directory örneğinden kaldırılabilir ve yeniden, toomake eklendi eklenen kullanıcılar bunları Active Directory'de tam bir kullanıcı. tooverify bu durumdan hello **Azure Active Directory** hello Azure portal, select bölmesinde **kullanıcılar ve gruplar**seçin **tüm kullanıcılar** ve hello seçtikten sonra belirli bir kullanıcı, select **profil**. Merhaba hello değerini **kullanıcı türü** hello kullanıcı profili altındaki özniteliğini eşit değil **Konuk**.

## <a name="authentication-planning"></a>Kimlik doğrulaması planlama
Azure Otomasyonu, Azure, şirket içi ve diğer bulut sağlayıcılarıyla kaynaklara karşı tooautomate görevleri sağlar.  Bir runbook tooperform için gerekli işlemleri, onu hello kaynaklarına erişim izinleri toosecurely hello abonelikte gereken hello en düşük haklara sahip olması gerekir.  

### <a name="what-is-an-automation-account"></a>Otomasyon Hesabı nedir? 
Azure Otomasyonu'nda hello Azure cmdlet'lerini kullanan kaynaklara karşı gerçekleştirdiğiniz tüm hello otomasyon görevleri tooAzure kullanarak Azure Active Directory kuruluş kimlik bilgileri tabanlı kimlik doğrulaması.  Automation hesabı Azure kaynaklarına toohello portal tooconfigure içinde toosign kullanın ve hello hesabından ayrıdır.  Otomasyon kaynaklar dahil olan bir hesap hello şunlardır:

* **Sertifikalar** - Runbook’tan veya DSC yapılandırmasından kimlik doğrulaması için kullanılan bir sertifika içerir. Bunları siz de ekleyebilirsiniz.
* **Bağlantıları** -kimlik doğrulama ve yapılandırma gerekli bilgileri tooconnect tooan dış hizmet veya uygulama bir runbook veya DSC yapılandırması içerir.
* **Kimlik bilgileri** -bir kullanıcı adı ve parola gerekli gibi güvenlik kimlik bilgileri içeren bir PSCredential nesnesi tooauthenticate bir runbook veya DSC yapılandırması.
* **Tümleştirme modülleri** -olan runbook'ları ve DSC yapılandırmalarınızda içinden cmdlet'leri bir Azure Otomasyonu hesabı toomake kullanımı ile birlikte gelen PowerShell modülleri.
* **Zamanlamalar** - Bir runbook’u yineleme sıklıkları dahil belirtilen zamanda başlatan veya durduran zamanlamaları içerir.
* **Değişkenler** -Runbook veya DSC yapılandırmasından kullanılabilen değerleri içerir.
* **DSC yapılandırmaları** -açıklar PowerShell komut dosyaları nasıl tooconfigure bir işletim sistemi özelliği ayarlama veya bir uygulamanın bir Windows veya Linux bilgisayara yükleyin.  
* **Runbook’lar** - Windows PowerShell’i temel alarak Azure Otomasyonu’nda bazı otomatik işlemleri gerçekleştiren görevler gruplarıdır.    

Merhaba her Automation hesabı için Automation kaynakları tek bir Azure bölgesiyle ilişkilendirilir, ancak Automation hesapları tüm hello kaynakları yönetebilir. Veri ve kaynaklarınız toobe yalıtılmış tooa belirli bölge gerektiren ilkeleri varsa, farklı bölgelerde Automation hesapları oluşturun.

> [!NOTE]
> Automation hesapları ve içerdikleri hello kaynakları hello Azure portalında oluşturulur, hello Klasik Azure portalında erişilemez. Bu hesapları veya kaynaklarını Windows PowerShell ile toomanage istiyorsanız hello Azure Resource Manager modüllerini kullanmanız gerekir.
> 

Hello Azure portalında bir Otomasyon hesabı oluşturduğunuzda, otomatik olarak iki kimlik doğrulama varlık oluşturun:

* Bir Farklı Çalıştır hesabı. Bu hesap, Azure Active Directory'de (Azure AD) bir hizmet sorumlusu ve bir sertifika oluşturur. Ayrıca, runbook'lar kullanılarak Resource Manager kaynaklarını yöneten hello katkıda bulunan rol tabanlı erişim denetimi (RBAC) atar.
* Klasik Farklı Çalıştır hesabı. Bu hesap, runbook'ları kullanarak kullanılan toomanage Klasik kaynakları olan bir yönetim sertifikası karşıya yükleme.

Rol tabanlı erişim denetimi ile Azure Resource Manager toogrant Eylemler tooan Azure AD kullanıcı hesabı ve farklı çalıştır hesabı izin kullanılabilir ve bu hizmet sorumlusunun kimliğini.  Okuma [Azure automation'da rol tabanlı erişim denetimi](automation-role-based-access-control.md) daha fazla bilgi için toohelp Automation izinlerinin yönetilmesi için modelinizin geliştirin.  

#### <a name="authentication-methods"></a>Kimlik doğrulama yöntemleri
Merhaba aşağıdaki tabloda Azure Automation'ın desteklediği her ortam için hello farklı kimlik doğrulama yöntemlerini özetler.

| Yöntem | Ortam 
| --- | --- | 
| Azure Farklı Çalıştır ve Klasik Farklı Çalıştır hesabı |Azure Resource Manager ve Azure klasik dağıtımı |  
| Azure AD Kullanıcı hesabı |Azure Resource Manager ve Azure klasik dağıtımı |  
| Windows kimlik doğrulaması |Yerel veri merkezinde veya hello karma Runbook çalışanı kullanarak diğer bulut sağlayıcısı |  
| AWS kimlik bilgileri |Amazon Web Hizmetleri |  

Merhaba altında **nasıl to\Authentication ve güvenlik** bölümünde, tooconfigure kimlik doğrulaması bu ortamlarda, varolan bir ya da genel bakış ve uygulama adımlarını sağlayarak makaleleri destekleme veya yeni hesabı Bu ortam için atayın.  Hello Azure farklı çalıştır ve klasik farklı çalıştır hesabı için konu hello [güncelleştirme Automation farklı çalıştır hesabı](automation-create-runas-account.md) nasıl tooupdate hello portal veya PowerShell başarısız olduysa kullanarak var olan Otomasyon hesabınızı hello farklı çalıştır hesapları açıklar ilk olarak bir farklı çalıştır veya Klasik farklı çalıştır hesabıyla yapılandırılmış. Toocreate bir farklı çalıştır ve klasik farklı çalıştır hesabı kuruluş sertifika yetkilisi (CA) tarafından verilen bir sertifika ile isterseniz, nasıl toocreate hello hesaplarını kullanarak bu makale toolearn gözden geçirin. Bu yapılandırma.     
 
## <a name="network-planning"></a>Ağ planlama
Hello karma Runbook çalışanı tooconnect tooand kayıt Microsoft Operations Management Suite (OMS), erişim toohello bağlantı noktası numarası olmalıdır ve hello URL'leri aşağıda açıklanmıştır.  Ayrıca toohello budur [bağlantı noktalarını ve URL'ler için gerekli hello Microsoft İzleme Aracısı](../log-analytics/log-analytics-windows-agents.md#network) tooconnect tooOMS. Merhaba Aracısı ile Merhaba OMS hizmeti arasındaki iletişimi için bir proxy sunucu kullanıyorsanız hello uygun kaynaklara erişilebilir tooensure gerekir. Bir güvenlik duvarı toorestrict erişim toohello Internet kullanırsanız, güvenlik duvarı toopermit erişiminizi tooconfigure gerekir.

Liste hello bağlantı noktası ve otomasyon ile Merhaba karma Runbook çalışanı toocommunicate için gerekli olan URL'ler altındaki Hello bilgi.

* Bağlantı noktası: Giden İnternet erişimi için yalnızca TCP 443 gereklidir
* Genel URL: *.azure-automation.net

Belirli bir bölge için tanımlanmış bir Otomasyon hesabınız var ve bu Bölgesel veri merkezi ile toorestrict iletişim istiyorsanız hello aşağıdaki tabloda hello DNS kaydı her bölge için sağlar.

| **Bölge** | **DNS Kaydı** |
| --- | --- |
| Orta Güney ABD |scus-jobruntimedata-prod-su1.azure-automation.net |
| Doğu ABD 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| Batı Orta ABD | wcus-jobruntimedata-prod-su1.azure-automation.net |
| Batı Avrupa |we-jobruntimedata-prod-su1.azure-automation.net |
| Kuzey Avrupa |ne-jobruntimedata-prod-su1.azure-automation.net |
| Orta Kanada |cc-jobruntimedata-prod-su1.azure-automation.net |
| Güneydoğu Asya |sea-jobruntimedata-prod-su1.azure-automation.net |
| Orta Hindistan |cid-jobruntimedata-prod-su1.azure-automation.net |
| Japonya Doğu |jpe-jobruntimedata-prod-su1.azure-automation.net |
| Avustralya Güneydoğu |ase-jobruntimedata-prod-su1.azure-automation.net |
| Birleşik Krallık Güney | uks-jobruntimedata-prod-su1.azure-automation.net |
| ABD Devleti Virginia | usge-jobruntimedata-prod-su1.azure-automation.us |

Adları yerine IP adresleri listesi, indirin ve hello gözden [Azure veri merkezi IP adresi](https://www.microsoft.com/download/details.aspx?id=41653) hello Microsoft Download Center xml dosyasından. 

> [!NOTE]
> Bu dosya hello Microsoft Azure veri merkezleri kullanılan (işlem, SQL ve depolama aralıkları dahil) başlangıç IP adresi aralıklarını içerir. Güncelleştirilen bir dosya şu anda dağıtılan hello aralıkları ve tüm yaklaşan değişiklikleri toohello IP aralıkları yansıtır haftalık nakledilir. Merhaba dosyasında görünen yeni aralıkları için en az bir hafta hello veri merkezlerinde kullanılmayacak. Lütfen yükleme hello yeni xml dosyası her hafta ve sitenizde hello gerekli değişiklikleri yapın toocorrectly Azure üzerinde çalışan hizmetleri tanımlayın. Hızlı rota kullanıcıların bu dosyayı tooupdate hello BGP reklamı'hello Azure alan her ayın ilk haftasında kullanılan unutmayın. 
> 

## <a name="creating-an-automation-account"></a>Otomasyon hesabı oluşturma

Bir Otomasyon hesabı hello Azure portalında oluşturabileceğiniz farklı yolu vardır.  Aşağıdaki tablonun hello her tür dağıtım deneyimi ve arasındaki farkları tanıtır.  

|Yöntem | Açıklama |
|-------|-------------|
| Otomasyon & hello Market denetiminden Seç | Bir Otomasyon hesabı ve OMS çalışma alanı oluşturur bir sunum tooone bağlı başka bir programda hello aynı kaynak grubu ve bölge.  OMS ile tümleştirme de günlük analizi toomonitor kullanmanın avantajı hello içerir ve runbook iş durumu ve iş akışları zamanla çözümlemek ve Gelişmiş Özellikler tooescalate kullanma veya sorunlarını araştırmak. Merhaba ayrıca sunumu varsayılan olarak etkinleştirilen hello değişiklik izleme ve güncelleştirme yönetimi çözümleri, dağıtır. |
| Otomasyon Market hello seçin | Bağlantılı tooan OMS çalışma değildir ve hello otomasyon ve denetim teklifi kullanılabilir tüm çözümlerinden içermeyen bir yeni veya var olan kaynak grubunda bir Otomasyon hesabı oluşturur. Bu tooAutomation tanıtan bir temel yapılandırma ve toowrite runbook'ları, DSC yapılandırmalarını ve kullanım hello hizmet özelliklerini nasıl hello öğrenmenize yardımcı olabilir. |
| Seçili Yönetim çözümleri | Bir çözüm – seçerseniz  **[güncelleştirme yönetimi](../operations-management-suite/oms-solution-update-management.md)**,  **[dışı saatlerde sırasında sanal makineleri Başlat/Durdur](automation-solution-vm-management.md)**, veya  **[ Değişiklik izleme](../log-analytics/log-analytics-change-tracking.md)**  tooselect var olan otomasyon ve OMS çalışma sor veya aboneliğinizde dağıtılan hello çözüm toobe için gerekli olarak her ikisi de seçeneği toocreate hello sunar. |

Bu konuda bir Otomasyon hesabı ve OMS çalışma ekleme hello otomasyon ve denetim teklifi tarafından oluşturmada size yol gösterir.  tek başına bir Otomasyon hesabı sınama ya da toopreview hello hizmeti için aşağıdaki makaleye bakın gözden geçirme hello toocreate [tek başına Automation hesabı oluşturma](automation-create-standalone-account.md).  

### <a name="create-automation-account-integrated-with-oms"></a>OMS ile tümleştirilmiş Otomasyon hesabı oluşturma
Merhaba Market hello hello otomasyon ve denetim teklifi seçerek Otomasyon olduğu yöntemi tooonboard önerilir.  Bu, hem bir Otomasyon hesabı oluşturur ve hello teklifi ile kullanılabilen hello seçeneği tooinstall hello yönetim çözümleri dahil olmak üzere bir OMS çalışma ile Merhaba tümleştirme oluşturur.  

1. Toohello Azure portal hello abonelik Yöneticileri rolünün üyesi ve hello aboneliğinin ortak yöneticisi olan bir hesapla oturum açın.

2. **Yeni**’ye tıklayın.<br><br> ![Azure portalında Yeni seçeneğini belirleyin](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  

3. Arama **Otomasyon** ve ardından hello seçin arama sonuçları **otomasyon ve Denetim***.<br><br> ![Market’te Otomasyon ve Denetim araması yapıp seçin](media/automation-offering-get-started/automation-portal-martketplace-select-automationandcontrol.png).<br>   

4. Merhaba teklifi Hello açıklamasını okuduktan sonra tıklatın **oluşturma**.  

5. Merhaba üzerinde **otomasyon ve Denetim** dikey penceresinde, select **OMS çalışma**.  Merhaba üzerinde **OMS çalışma alanları** dikey penceresinde, Automation hesabı hello aynı Azure aboneliği olan bir OMS çalışma bağlı toohello seçin veya bir OMS çalışma alanı oluşturun.  Bir OMS çalışma yoksa seçin **yeni çalışma alanı oluştur** ve hello **OMS çalışma** dikey penceresinde hello aşağıdakileri gerçekleştirin: 
   - Merhaba yeni bir ad belirtin **OMS çalışma**.
   - Seçin bir **abonelik** hello varsayılan seçili uygun değilse toolink tooby hello aşağı açılan listeden seçerek..
   - **Kaynak Grubu** için bir kaynak grubu oluşturabilir veya mevcut bir kaynak grubunu seçebilirsiniz.  
   - Bir **Konum** seçin.  Şu anda hello yalnızca kullanılabilir konumlarının **Avustralya Güneydoğu**, **Doğu ABD**, **Güneydoğu Asya**, **Batı Orta ABD**ve  **Batı Avrupa**.
   - Bir **Fiyatlandırma katmanı** seçin.  Merhaba çözüm iki katmanlarda sunulur: boşaltın ve her düğüm (OMS) katmanı.  Merhaba ücretsiz katmanı hello günlük tutma süresi ve runbook iş çalışma zamanı dakika toplanan veri miktarına bir sınırı vardır.  Merhaba başına düğüm (OMS) katmanı bir sınır hello günlük toplanan veri miktarına sahip değil.  
   - **Otomasyonu Hesabı**’nı seçin.  Yeni bir OMS çalışma alanı oluşturuyorsanız, gerekli tooalso Azure abonelik, kaynak grubu ve bölge gibi daha önce belirtilen hello yeni OMS çalışma alanı ile ilişkili olan bir Otomasyon hesabı oluşturun.  Seçebileceğiniz **Automation hesabı oluşturma** ve hello **Otomasyon hesabı** dikey penceresinde hello şunları sağlar: 
  - Merhaba, **adı** alanında, hello hello Automation hesabı adını girin.

    Seçili hello OMS çalışma alanı temelli tüm diğer seçenekler otomatik olarak doldurulur ve bu seçenekleri değiştirilemez.  Bir Azure farklı çalıştır hesabı hello varsayılan kimlik doğrulama hello teklifi için yöntemidir.  Tıkladığınızda **Tamam**hello yapılandırma seçenekleri doğrulanır ve hello Otomasyon hesabı oluşturulur.  Altında ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde. 

    Aksi takdirde, mevcut bir Otomasyon Farklı Çalıştır hesabını seçebilirsiniz.  Seçtiğiniz hello hesabı zaten bağlı tooanother OMS çalışma olamaz, aksi takdirde bir bildirim iletisi hello dikey pencerede sunulur.  Zaten bağlıysa, tooselect farklı bir Automation farklı çalıştır hesabı gerekiyor veya bir tane oluşturun.

    Gerekli hello bilgileri tamamladıktan sonra tıklatın **oluşturma**.  Merhaba bilgi doğrulanır ve hello Otomasyon hesabı ve farklı çalıştır hesapları oluşturulur.  Toohello döndürülen **OMS çalışma** dikey penceresinde otomatik olarak.  

6. Merhaba üzerinde hello gerekli bilgileri girdikten sonra **OMS çalışma** dikey penceresinde tıklatın **oluşturma**.  Merhaba bilgi doğrulanır ve hello çalışma alanı oluşturulur, ancak altında ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde.  Toohello döndürülen **Çözüm Ekle** dikey.  

7. Merhaba üzerinde **otomasyon ve Denetim** dikey penceresinde, istediğiniz tooinstall hello önerilen önceden seçilmiş çözümleri onaylayın. Herhangi bir seçimi kaldırırsanız, daha sonra tek tek yükleyebilirsiniz.  

8. Tıklatın **oluşturma** tooproceed ekleme otomasyon ve bir OMS çalışma. Tüm ayarlar doğrulanır ve aboneliğinizde sunumu toodeploy hello çalışır.  Bu işlem birkaç sürebilir saniye toocomplete ve altında ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde. 

Hello teklifi edildi olduktan sonra yönetim çözümleri, etkin runbook'ları, hello çalışmak oluşturmaya başlamak, dağıtımı bir [karma Runbook çalışanı](automation-hybrid-runbook-worker.md) rol veya ile çalışmaya başlamak [günlük analizi](https://docs.microsoft.com/azure/log-analytics) toocollect verileri Bulut veya şirket içi ortamınızdaki kaynakların tarafından üretildi.   

## <a name="next-steps"></a>Sonraki adımlar
* [Azure Otomasyonu Farklı Çalıştır hesabı kimlik doğrulama testi](automation-verify-runas-authentication.md) bölümünü gözden geçirerek, yeni Otomasyon hesabınızın Azure kaynaklarıyla kimlik doğrulaması yapıp yapamadığını onaylayabilirsiniz.
* tooget başlatılan runbook'larınızı oluşturma ile ilk hello gözden [Automation runbook türleri](automation-runbook-types.md) yazma başlamadan önce ilgili dikkat edilecek noktalar ve desteklenir.


