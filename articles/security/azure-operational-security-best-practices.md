---
title: "aaaAzure işletimsel güvenlik en iyi uygulamalar | Microsoft Docs"
description: "Bu makale Azure işletimsel güvenlik için en iyi yöntemler kümesi sağlar."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: b3b17ef20fb3545b1c268ac0d7ce692e07c8da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-best-practices"></a>Azure işletimsel güvenlik en iyi uygulamalar
Azure işlem güvenliği verilerini, uygulamaları ve diğer Microsoft Azure varlıkları korumak için toohello Hizmetleri, denetimleri ve özellikler kullanılabilir toousers ifade eder. Azure işlem güvenliği benzersiz tooMicrosoft hello Microsoft Security Development Lifecycle (SDL), Microsoft Security Response Center hello dahil olmak üzere, çeşitli özelliklerini elde edilen hello bilgi içeren bir çerçevesi üzerine inşa edilmiştir Program ve hello siber güvenlik tehdit derin tanıma.

Bu makalede, en iyi güvenlik uygulamaları, Azure veritabanı koleksiyonunu tartışın. Bu en iyi uygulamaları ile Azure veritabanı güvenlik bizim deneyimlerden türetilen ve müşterilerin hello deneyimleri bulunun.

En iyi her uygulama için biz açıklamaktadır:
-   Hangi hello en iyi uygulamadır
-   Neden bu en iyi uygulama tooenable istiyor
-   Tooenable hello en iyi yöntem başarısız olursa ne hello sonucu olabilir
- Tooenable hello en iyi yöntem nasıl öğrenin

Bu makalenin yazıldığı hello zamanında oldukları gibi bu Azure işletimsel güvenlik en iyi yöntemler makalesi anlaşma fikir ve Azure platformu özellikleri ve özellik kümeleri dayanır. Bu makalede olacaktır ve görüşlerini ve teknolojileri değiştirmek zaman içinde bu değişiklikleri düzenli olarak tooreflect üzerinde güncelleştirildi.

Bu makalede ele alınan azure işlem en iyi yöntemler şunlardır:

-   İzleme, yönetme ve bulut altyapısını koruma
-   Kimlik ve çoklu oturum açma (SSO) uygulama
-   Kullanım Eğilimleri çözümlemek ve tanılama sorunlarını izleyebilirsiniz istekleri
-   Hizmetleri Merkezi bir izleme çözümü ile izleme
-   Engellemenize, algılamanıza ve toothreats yanıt
-   Uçtan uca senaryo tabanlı ağ izleme
-   Güvenli dağıtım başarısı kanıtlanmış DevOps araçlarını kullanma

## <a name="monitor-manage-and-protect-cloud-infrastructure"></a>İzleme, yönetme ve bulut altyapısını koruma
BT işlemleri veri merkezi altyapı, uygulamaları ve verileri hello kararlılık ve bu sistemlerin güvenlik dahil olmak üzere, yönetmekle sorumlu. Ancak, karmaşık BT ortamları arasında genellikle artırma güvenlik bilgileri elde kuruluşlar toocobble birlikte verileri birden çok güvenlik ve yönetim sistemi gerektirir.

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) , yönetmek ve şirket içi korumak ve bulut altyapısı yardımcı olan Microsoft'un bulut tabanlı BT yönetimi çözümüdür.

[OMS güvenlik ve denetim çözümü](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources) BT tooactively izlemenize yardımcı olabilecek tüm kaynakları etkinleştirir, güvenlik olaylarına hello etkisini en aza indirmek. OMS güvenlik ve denetim kaynakları izlemek için kullanılan güvenlik etki alanları sahiptir.

OMS hakkında daha fazla bilgi için hello makaleyi okuyun [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

engellemenize, algılamanıza ve toothreats, yanıt toohelp [Operations Management Suite (OMS) güvenlik ve denetim çözümü](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) içeren veri kaynaklarınızı ilgili işler ve toplar:

-   Güvenlik olay günlüğü
-   Windows için Olay İzleme (ETW) olayları
-   AppLocker denetim olayları
-   Windows Güvenlik Duvarı günlüğü
-   Gelişmiş Threat Analytics olayları
-   Temel değerlendirmesinin sonuçları
-   Kötü amaçlı yazılımdan koruma değerlendirmesinin sonuçları
-   Güncelleştirme/düzeltme eki değerlendirmesinin sonuçları
-   Merhaba aracısında açıkça etkin Syslog akışlar


## <a name="manage-identity-and-implement-single-sign-on"></a>Kimlik ve çoklu oturum açmayı uygulamak
[Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) Microsoft'un çok kiracılı bulut tabanlı dizin ve Kimlik Yönetimi Hizmeti.

[Azure AD](https://azure.microsoft.com/services/active-directory/) da tam dizisi içerir [Kimlik Yönetimi](https://docs.microsoft.com/azure/security/security-identity-management-overview) yetenekleri de dahil olmak üzere [çok faktörlü kimlik doğrulaması](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication), cihaz kaydı, Self Servis parola yönetimi Self Servis Grup Yönetimi, ayrıcalıklı hesap yönetimi, rol tabanlı erişim denetimi, uygulama kullanımını izleme, zengin denetim ve güvenlik izleme ve uyarma.

özellikleri aşağıdaki hello bulut tabanlı uygulamaların güvenliğini sağlamak, BT işlemlerini kolaylaştırır, maliyetleri kesebilir ve kurumsal uyumluluk hedefleri karşılandığından emin olun yardımcı:

-   Merhaba bulut için kimlik ve erişim yönetimi
-   Kullanıcı erişim tooany bulut uygulamasının basitleştirin
-   Hassas verileri ve uygulamaları koruyun
-   Çalışanlarınıza self-servis olanağı sağlayın
-   Azure Active Directory ile tümleştirin

### <a name="identity-and-access-management-for-hello-cloud"></a>Merhaba bulut için kimlik ve erişim yönetimi
Azure Active Directory (Azure AD) şu kapsamlı bir [kimlik ve erişim yönetimi bulut çözümü](https://www.microsoft.com/cloud-platform/identity-management), sağlayan, bir dizi sağlam yetenekleri toomanage kullanıcılar ve gruplar. Güvenli erişim tooon içi ve bulut uygulamalarında hizmet (SaaS) uygulamaları olarak Office 365 ve kadar Microsoft dışı yazılımlar gibi Microsoft web hizmetlerini de dahil olmak üzere, yardımcı olur.
tooenable kimlik koruması Azure AD'de daha nasıl görürüm toolearn [etkinleştirme Azure Active Directory kimlik koruması](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection-enable).

### <a name="simplify-user-access-tooany-cloud-app"></a>Kullanıcı erişim tooany bulut uygulamasının basitleştirin
[Çoklu oturum açmayı etkinleştir](https://docs.microsoft.com/azure/active-directory/active-directory-sso-integrate-saas-apps) toosimplify kullanıcı erişimi toothousands Windows, Mac, Android ve iOS cihazlarından bulut uygulamalarının. Kullanıcıların kişiselleştirilmiş web tabanlı erişim paneli veya şirket kimlik bilgilerini kullanarak mobil uygulama uygulamalardan başlatabilirsiniz. Ve şirket içi web uygulamaları tooprovide yüksek güvenlikli uzaktan erişim ve çoklu oturum açma yayımlama Hello Azure AD uygulama proxy'si modülü toogo SaaS uygulamaları ötesinde kullanın.

### <a name="protect-sensitive-data-and-applications"></a>Hassas verileri ve uygulamaları koruyun
Etkinleştirme [Azure çok faktörlü kimlik doğrulaması](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) tooprevent yetkisiz erişim tooon içi ve bulut uygulamaları ek bir kimlik doğrulama düzeyi sağlayarak. Tutarsız erişim düzenlerini belirleyen güvenli izleme, uyarılar ve makine öğrenme tabanlı güvenlik raporları ile işinizi koruyun ve olası tehditleri azaltın.

### <a name="enable-self-service-for-your-employees"></a>Çalışanlarınıza self-servis olanağı sağlayın
Parolaları sıfırlama ve grup oluşturma ve yönetme gibi önemli görevleri tooyour çalışanlar, temsilci. [Self Servis parola değişikliğini etkinleştir](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-update-your-own-password)sıfırlayın ve Self Servis Grup Yönetimi Azure AD ile.

### <a name="integrate-with-azure-active-directory"></a>Azure Active Directory ile tümleştirin
Genişletme [Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-to-integrate) ve diğer dizinleri tooAzure AD tooenable çoklu oturum açma tüm bulut tabanlı uygulamalar için şirket içi. Kullanıcı öznitelikleri her türlü şirket içi dizinleri otomatik olarak eşitlenen tooyour bulut dizininden olabilir.

Azure Active Directory Tümleştirmesi hakkında daha fazla toolearn ve nasıl tooenable, hello makalesini okuyun [şirket içi dizinlerinizi Azure Active Directory ile tümleştirme](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

## <a name="trace-requests-analyze-usage-trends-and-diagnose-issues"></a>Kullanım Eğilimleri çözümlemek ve tanılama sorunlarını izleyebilirsiniz istekleri
[Azure Storage Analytics](https://docs.microsoft.com/azure/storage/storage-analytics) günlüğe kaydetme işlemlerini gerçekleştiren ve ölçümler veriler için bir depolama hesabı sağlar. Bu veri tootrace istekleri kullanır, kullanım eğilimleri çözümlemek ve depolama hesabınızla sorunlarını tanılamak.

Storage Analytics ölçümleri, yeni depolama hesapları için varsayılan olarak etkinleştirilir. Günlük kaydını etkinleştirmek ve ölçümleri ve hello Azure portalında oturum yapılandırın; Ayrıntılar için bkz [hello Azure portalında bir depolama hesabını izleme](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account). Storage Analytics hello REST API aracılığıyla programlı olarak veya hello istemci kitaplığı da etkinleştirebilirsiniz. Merhaba hizmet özelliklerini ayarlama işlemi tooenable Storage Analytics her hizmet için ayrı ayrı kullanın.

Kapsamlı bir kılavuz depolama çözümlemeleri ve diğer araçları tooidentify kullanma hakkında bilgi için tanılama ve Azure Storage ile ilgili sorunları giderme bkz [izleme, tanılama ve Microsoft Azure Storage sorun giderme](https://docs.microsoft.com/azure/storage/storage-monitoring-diagnosing-troubleshooting).

Azure Active Directory Tümleştirmesi hakkında daha fazla toolearn okuyup nasıl tooenable, hello makale [etkinleştirme ve yapılandırma depolama çözümlemeleri](https://docs.microsoft.com/rest/api/storageservices/Enabling-and-Configuring-Storage-Analytics?redirectedfrom=MSDN).

## <a name="monitoring-services"></a>İzleme Hizmetleri
Bulut uygulamalarını birçok taşıma bölümleriyle karmaşıktır. İzleme, uygulamanızı kurma kalır veri tooensure ve sistem durumu iyi çalışan sağlar. Olası sorunlar kapalı veya olanları sorun giderme, toostave yardımcı olur. Ayrıca, uygulamanız hakkında izleme verileri toogain ayrıntılı Öngörüler kullanabilirsiniz. Bu bilgi tooimprove uygulama performansı veya bakım yardımcı veya aksi halde el ile müdahale gerektiren Eylemler otomatik hale getirme.

### <a name="monitor-azure-resources"></a>Azure kaynaklarını izleme
[Azure İzleyici](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started) Azure kaynakları izlemek için tek bir kaynağı sağlayan hello platform hizmetidir. Azure izleme ile görselleştirme, sorgulama yapabilir, yol, arşiv ve hello ölçümleri ve Azure kaynaklarında'ten gelen günlükleri üzerinde işlem gerçekleştirin. Merhaba İzleyici portal dikey penceresinde, kullanarak bu verilerle çalışma [İzleyici PowerShell cmdlet'leri](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-powershell-samples), [platformlar arası CLI](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-cli-samples), veya [Azure İzleyici REST API'lerini](https://msdn.microsoft.com/library/dn931943.aspx).

### <a name="enable-autoscale-with-azure-monitor"></a>Otomatik ölçeklendirme ile Azure izleyicisini etkinleştirmek
Etkinleştirme [Azure İzleyici otomatik ölçeklendirme](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-autoscale-get-started) yalnızca toovirtual makine ölçekleme kümeleri (VMSS), bulut Hizmetleri, uygulama hizmeti planları ve app service ortamları için geçerlidir.

### <a name="manage-roles-permissions-and-security"></a>Rolleri yönetme izinleri ve güvenlik
Birçok ekip toostrictly gerek [erişim toomonitoring düzenleyen](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-roles-permissions-security) veriler ve ayarlar. Örneğin, özel olarak (destek mühendisleri, devops mühendisleri) izleme üzerinde çalışan takım üyeleri varsa veya bir yönetilen hizmet sağlayıcısı kullanıyorsanız, bunların özelliği toocreate kısıtlama sırasında izleme verilerini tooonly erişmesine toogrant isteyebilirsiniz değiştirebilir veya kaynakları silin.

Bu, nasıl tooquickly azure'da yerleşik izleme RBAC rolü tooa kullanıcı uygulamak veya kendi özel rol sınırlı izleme izinleri gereken kullanıcılar için yapı gösterir. Ardından Azure İzleyici ilgili kaynaklarınız için güvenlik konuları açıklanır ve erişim toohello verileri sınırlayabilirsiniz nasıl içerirler.

## <a name="prevent-detect-and-respond-toothreats"></a>Engellemenize, algılamanıza ve toothreats yanıt
Güvenlik Merkezi tehdit algılaması Azure kaynaklarını, hello ağ ve bağlı iş ortağı çözümlerinden güvenlik bilgileri otomatik olarak toplayarak çalışır. Bu, genellikle birden fazla kaynaktan tooidentify tehditleri bilgileri ilişkilendirerek, bu bilgileri analizleri yaparken. Güvenlik uyarıları nasıl tooremediate hello tehdit ilişkin öneriler birlikte Güvenlik Merkezi'nde önceliklendirilir.

-   [Güvenlik ilkesini yapılandırma](https://docs.microsoft.com/azure/security-center/security-center-policies) Azure aboneliğiniz için.
-   Kullanım hello [Güvenlik Merkezi'nde öneriler](https://docs.microsoft.com/azure/security-center/security-center-recommendations) Azure kaynaklarınızı korumak toohelp.
-   Gözden geçirin ve geçerli yönetmek [güvenlik uyarıları](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).

[Azure Güvenlik Merkezi](https://docs.microsoft.com/azure/security-center/security-center-intro) hello Azure kaynaklarınızın güvenlik engellemek, algılamak, artırılmış görünürlük aracılığı ile toothreats yanıt ve üzerinden denetlemesine yardımcı olur. Aboneliklerinizde, tümleşik güvenlik izleme ve ilke yönetimi sağlar; normal koşullarda gözden kaçabilecek tehditleri algılamaya yardımcı olur ve güvenlik çözümlerinin geniş ekosistemiyle çalışır.

Güvenlik Merkezi, kullanımı kolay ve etkili tehdit tooAzure içinde yerleşik olan önleme, saptama ve yanıt özellikleri sağlar. Temel işlevler şunlardır:

-   Bulut güvenlik durumu anlama
-   Bulut güvenliğinin denetimini elinize alın
-   Tümleşik bulut güvenliği çözümlerini kolayca dağıtın
-   Tehditleri algılayın ve hızlı yanıt verin

### <a name="understand-cloud-security-state"></a>Bulut güvenlik durumu anlama
Azure Güvenlik Merkezi'ni kullanın tooget tüm Azure kaynaklarınızı hello güvenlik durumunun merkezi bir görünüm. Bir bakışta hello uygun güvenlik denetimleri yerinde olduğundan ve doğru yapılandırılmış ve dikkat gerektiren tüm kaynaklar hızlı bir şekilde tanımlamak doğrulayın.

### <a name="take-control-of-cloud-security"></a>Bulut güvenliğinin denetimini elinize alın
Tanımlamak [güvenlik ilkeleri](https://docs.microsoft.com/azure/security-center/security-center-policies) tooyour şirket göre Azure aboneliklerinize bulut güvenlik ihtiyaçlarını, uygulamaların toohello türü veya hello veri duyarlılığını her abonelik için özel olarak hazırlanmış kullanıcının. İlke temelli önerileri tooguide kaynak sahiplerine hello süreci gerekli denetimleri uygulama kullanmak — hello konusunda güvenilir bilgiler bulut güvenlik dışında alın.

### <a name="easily-deploy-integrated-cloud-security-solutions"></a>Tümleşik bulut güvenliği çözümlerini kolayca dağıtın
[Güvenlik çözümlerle](https://docs.microsoft.com/azure/security-center/security-center-partner-integration) Microsoft ve onun ortakları, endüstri lideri güvenlik duvarları ve kötü amaçlı yazılımdan koruma dahil olmak üzere. Kullanım hızlandırıldı sağlama toodeploy güvenlik çözümleri — bile ağ değişiklikleri sizin için yapılandırılır. İş ortaklarının çözümlerinden alınan güvenlik olaylarınız, analiz ve uyarı amacıyla otomatik olarak toplanır.

### <a name="detect-threats-and-respond-fast"></a>Tehditleri algılayın ve hızlı yanıt verin
Tümleşik ve analiz odaklı bir yaklaşımla mevcut ve gelişmekte olan bulut tehditlerinin önüne geçin. Microsoft Genel birleştirerek [tehdit Intelligence](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities) ve uzmanlık Öngörüler ile bulut güvenlikle ilgili olayları, Azure dağıtımlar arasında Güvenlik Merkezi, gerçek tehditleri erken algılamak ve hatalı pozitif sonuçları azaltmak yardımcı olur. Bulut güvenlik uyarıları hello saldırı kampanya ilgili olaylar ve etkilenen kaynakları da dahil olmak üzere, fikir vermek ve tooremediate sorunları ve hızlı bir şekilde kurtarmak yöntemler önerir.

## <a name="end-to-end-scenario-based-network-monitoring"></a>Uçtan uca senaryo tabanlı ağ izleme
Müşterilerin bir uçtan uca ağ Azure VNet, ExpressRoute, uygulama ağ geçidi, yük Dengeleyiciler ve daha fazlasını gibi çeşitli tek tek ağ kaynaklarına oluşturma ve yönetme tarafından oluşturun. İzleme her hello ağ kaynaklarına kullanılabilir.

[Ağ İzleyicisi](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) koşullar içinde için ve azure'dan ağ senaryo düzeydeki tanılama ve toomonitor sağlayan bölgesel bir hizmettir. Ağ Tanılama ve görselleştirme Ağ İzleyicisi ile kullanılabilen araçlar anlamak, tanılama ve Öngörüler tooyour Azure ağında geçirmesine yardımcı olur.

### <a name="automate-remote-network-monitoring-with-packet-capture"></a>Paket yakalama ile uzaktan ağ izlemeyi otomatikleştirin
Tooyour Sanal Ağ İzleyicisi'ni kullanarak makineleri (VM'ler) oturum olmadan ağ sorunlarını tanılamak ve izleyin. Tetikleyici [paket yakalama](https://docs.microsoft.com/azure/network-watcher/network-watcher-alert-triggered-packet-capture) göre uyarıları ayarlama ve erişimi tooreal zamanı performans bilgileri hello paket düzeyinde geçirmesine. Bir sorunla karşılaştığınızda, daha iyi tanılama için ayrıntılı olarak inceleme yapabilirsiniz.

### <a name="gain-insight-into-your-network-traffic-using-flow-logs"></a>Akış günlüklerini kullanarak ağ trafiğiniz hakkında ayrıntılı bilgi edinin
Ağ trafiği düzeni kullanarak, daha derin bir anlayış oluşturmak [ağ güvenlik grubu akış günlükleri](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview). Akış günlükleri tarafından sağlanan bilgiler, Denetim ve ağ güvenlik profili izleme uyumluluk için veri toplayacak yardımcı olur.

### <a name="diagnose-vpn-connectivity-issues"></a>VPN bağlantısıyla ilgili sorunları tanılayın
Ağ İzleyicisi sağlar, hello özelliği çok[VPN ağ geçidi ve ağ bağlantıları, en sık karşılaşılan sorunları tanılamak](https://docs.microsoft.com/azure/network-watcher/network-watcher-diagnose-on-premises-connectivity). Yalnızca tooidentify hello sorunu aynı zamanda toouse izin vererek hello oluşturulan toohelp daha fazla araştırmak günlükleri ayrıntılı.

toolearn nasıl hakkında daha fazla tooconfigure Ağ İzleyicisi'ni ve nasıl tooenable, hello makalesini okuyun [Ağ İzleyicisi'ni yapılandırma](https://docs.microsoft.com/azure/network-watcher/network-watcher-create).

## <a name="secure-deployment-using-proven-devops-tools"></a>Güvenli dağıtım başarısı kanıtlanmış DevOps araçlarını kullanma
Bunlar, hello listesi, Azure DevOps yöntemler kuruluşlar ve ekipleri ve verimli hale getirir Microsoft Cloud alanındaki bazılarıdır.

-   **Kod (IaC) olarak altyapı:** kod olarak altyapı teknikleri kümesidir ve BT uzmanlarının yardımcı yöntemler hello gün tooday yapı ve modüler altyapısının yönetim ilişkili hello yük kaldırın. BT uzmanları toobuild sağlar ve modern sunucu ortamlarında nasıl geliştiricilerine oluşturmak ve uygulama kodu korumak gibi bir yol sağlamak. Azure için sahip olduğumuz [Azure Resource Manager]( https://azure.microsoft.com/documentation/articles/resource-group-authoring-templates/) bildirim temelli bir şablon kullanarak uygulamalarınızı tooprovision izin verir. Tek bir şablonda birden çok hizmeti bağımlılıklarıyla birlikte dağıtabilirsiniz. Merhaba kullandığınız aynı şablon toorepeatedly hello uygulama yaşam döngüsünün her aşaması sırasında uygulamanızı dağıtın.
-   **Sürekli tümleştirme ve dağıtım:** Visual Studio Online takım projeleriniz çok yapılandırabilirsiniz[otomatik olarak oluşturma ve dağıtma](https://www.visualstudio.com/docs/build/overview) tooAzure web uygulamaları veya Bulut hizmetlerini. VSO kodu her iade sonra yapı tooAzure yaptıktan sonra hello ikili dosyaları otomatik olarak dağıtır. Merhaba paket oluşturma işlemi burada açıklanan eşdeğer toohello paket komut Visual Studio'da, ve hello yayımlama eşdeğer toohello Yayımla komutunu Visual Studio'da adımlardır.
-   **Yayın Yönetimi:** Visual Studio [yayın Yönetimi](https://msdn.microsoft.com/library/vs/alm/release/overview) çok aşamalı dağıtımı otomatikleştirme ve hello yönetme işlemi yayın için harika bir çözümdür. Yönetilen sürekli dağıtım ardışık düzen toorelease hızlı, kolay ve genellikle oluşturun. Sürüm yönetimi ile biz çok bizim yayın süreci otomatik hale getirebilirsiniz ve biz onay iş akışları önceden. Şirket içi ve toohello dağıtmak bulut, genişletme ve gerektiği gibi özelleştirin.
-   **Uygulama performansı izleme:** sorunları algılamak, sorunları çözmek ve uygulamanızı sürekli geliştirin. Canlı uygulamanızdaki sorunları hemen tanılayın. Kullanıcılarınızın bununla neler yaptığını anlayın. Yapılandırma JS kod ve webconfig girişi ekleme kolay konudur ve tüm hello ayrıntılarla hello portalında dakika içinde sonuçlarını görebilirsiniz. [App ınsights](https://azure.microsoft.com/documentation/articles/app-insights-start-monitoring-app-health-usage/) kuruluşlar sorunları & düzeltme daha hızlı algılanması için yardımcı olur.
-   **Test & otomatik ölçeklendirme yük:** bizim uygulama tooimprove dağıtım kalite ve toomake uygulamamıza olduğundan her zaman yukarı veya kullanılabilir toocater toohello iş gereksinimlerini emin biz performans sorunlarını bulabilirsiniz. Uygulamanızı bir sonraki başlatma veya pazarlama kampanyanızı için trafiği işleyebilir emin olun. Bulut tabanlı çalıştırma başlatın [yük testleri](https://www.visualstudio.com/docs/test/performance-testing/getting-started/getting-started-with-performance-testing) Visual Studio Online ile neredeyse hiçbir zaman.

## <a name="next-steps"></a>Sonraki adımlar
- Daha fazla bilgi edinmek [Azure işletimsel güvenlik](https://docs.microsoft.com/azure/security/azure-operational-security).
- Daha fazla tooLearn [Operations Management Suite | Güvenlik ve Uyumluluk](https://www.microsoft.com/cloud-platform/security-and-compliance).
- [Operations Management Suite güvenlik ve denetim çözümü ile çalışmaya başlama](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started).
