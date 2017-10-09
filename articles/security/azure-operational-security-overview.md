---
title: "aaaAzure işletimsel güvenlik genel bakış | Microsoft Docs"
description: "Bu makalede hello Azure işletimsel güvenlik genel bir bakış sağlar."
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
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: b91c7889660b32e4933c305007692bd6e1ded05f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-overview"></a>Azure operational güvenliğine genel bakış
Azure işlem güvenliği verilerini, uygulamaları ve diğer Microsoft Azure varlıkları korumak için toohello Hizmetleri, denetimleri ve özellikler kullanılabilir toousers ifade eder. [Azure işlem güvenliği](https://docs.microsoft.com/azure/security/azure-operational-security) hello bilgi içeren bir çerçeve hello Microsoft Security Development Lifecycle (SDL), Microsoft Security hello dahil olmak üzere benzersiz tooMicrosoft yetenekleri çeşitli elde edilen Response Center program ve hello siber güvenlik tehdit derin tanıma.

Bu Azure işletimsel güvenlik genel bakış makalesi alanları aşağıdaki hello üzerinde odaklanır:

- Azure Operations Management Suite
-   Azure Güvenlik Merkezi
-   Azure İzleyici
-   Azure Ağ İzleyicisi
-   Azure depolama çözümlemeleri
-   Azure Active directory

## <a name="azure-operations-management-suite"></a>Azure Operations Management Suite
BT işlemleri veri merkezi altyapı, uygulamaları ve verileri hello kararlılık ve bu sistemlerin güvenlik dahil olmak üzere, yönetmekle sorumlu. Ancak, karmaşık BT ortamları arasında genellikle artırma güvenlik bilgileri elde kuruluşlar toocobble birlikte verileri birden çok güvenlik ve yönetim sistemi gerektirir.

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) , yönetmek ve şirket içi korumak ve bulut altyapısı yardımcı olan Microsoft'un bulut tabanlı BT yönetimi çözümüdür.

OMS bulut tabanlı BT Yönetim BT Otomasyon, güvenlik ve uyumluluk, günlük analizi ve yedekleme ve kurtarma gibi birçok olanakları sunan çözümüdür. Bu nedenle, kusursuz yardımcı toomanage olduğundan ve BT altyapınızın korumak — şirket içinde ve hello bulut.

OMS Hello çekirdek işlevselliğini Azure üzerinde çalışan hizmetleri kümesi tarafından sağlanır. Her hizmet belirli yönetim işlevi sağlar ve Hizmetleri tooachieve farklı yönetim senaryoları birleştirebilirsiniz. İçerir:

-   Log Analytics
-   Otomasyon
-   Backup
-   Site Recovery

### <a name="log-analytics"></a>Log Analytics
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics), yönetilen kaynaklardan toplanan verileri merkezi bir depoda birleştirerek OMS için izleme hizmetleri sağlar. Bu veriler, olayları, performans verileri veya hello API sağlanan özel verileri içerebilir. Toplandığında, hello veri uyarı, analiz ve dışarı aktarma için kullanılabilir. Mevcut şirket içi ortamınız ile Azure hizmetlerinden verileri birleştirebilirsiniz şekilde bu yöntem, çeşitli kaynaklardan tooconsolidate verileri sağlar. Aynı zamanda açıkça hello hello veri koleksiyonunu tüm eylemleri kullanılabilir tooall veri türlerini; böylece bu veriler üzerinde gerçekleştirilecek hello eylemden ayırır.

### <a name="automation"></a>Otomasyon
Microsoft [Azure Otomasyonu](https://docs.microsoft.com/azure/automation/automation-intro) bir bulut ve Kurumsal ortamda sık gerçekleştirilen hello el ile uzun süreli, hatasız ve sık tekrarlanan görevleri kullanıcılar tooautomate için bir yol sağlar. Kaydeder zaman hello normal yönetim görevlerinin güvenilirliğini artırır ve hatta bunları toobe otomatik olarak zamanlar düzenli aralıklarla gerçekleştirilen. Runbook’ları kullanarak işlemleri otomatik hale getirebilir ya da İstenen Durum Yapılandırması’nı kullanarak yapılandırmayı otomatik hale getirebilirsiniz.

### <a name="backup"></a>Backup
[Azure yedekleme](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) tooback kullanır (veya koruma) hello Azure tabanlı bir hizmettir ve verilerinizi hello Microsoft bulut geri yükleyin. Azure Backup, var olan şirket içi veya şirket dışı yedekleme çözümünüzün yerine, güvenilir, güvenli ve maliyet açısından rekabetçi bir bulut tabanlı çözüm sunar. Azure yedekleme sunar indirin ve hello uygun bilgisayarda dağıtan birden çok bileşen sunucusu veya hello bulutta. Hello bileşeni ya da dağıttığınız aracısına bağlıdır, istediğiniz üzerinde tooprotect. Tüm Azure Backup bileşenleri (koruduğunuz verileri şirket içi olsun veya hello bulutta) veri Azure kurtarma Hizmetleri kasasına tooa yukarı kullanılan tooback olabilir. Merhaba bkz [Azure Backup bileşenleri tablo](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup#which-azure-backup-components-should-i-use).

### <a name="site-recovery"></a>Site kurtarma
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) çoğaltma, şirket içi sanal ve fiziksel makineler tooAzure veya tooa ikincil site düzenleyerek iş sürekliliği sağlar. Birincil site kullanılamıyorsa, böylece kullanıcılar çalışma tutun ve geri sistemleri tooworking sipariş döndüğünüzde başarısız toohello ikincil konum başarısız. Akıllı ve etkili tehdit algılama.

## <a name="azure-active-directory"></a>Azure Active Directory
[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-enable-sso-scenario) Microsoft'un kapsamlı kimlik Service (Idaas) çözümü olarak:

-   Bulut hizmeti olarak IAM sağlar
-   Merkezi erişim yönetimi, çoklu oturum açma (SSO) ve raporlama sağlar
-   Destekleyen tümleşik erişim yönetimi için [uygulamaları binlerce](https://azure.microsoft.com/marketplace/active-directory/) hello uygulama galerisinde Salesforce, Google Apps, kutusunu, Concur ve benzeri.

Azure AD de içeren tam dizisi [kimlik yönetimi özelliklerini](https://docs.microsoft.com/azure/security/security-identity-management-overview#security-monitoring-alerts-and-machine-learning-based-reports) dahil olmak üzere [çok faktörlü kimlik doğrulaması](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication), [aygıt kaydı]( https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-overview), [ Self Servis parola yönetimi](https://azure.microsoft.com/resources/videos/self-service-password-reset-azure-ad/), [Self Servis Grup Yönetimi](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-update-your-own-password), [ayrıcalıklı hesap yönetimi](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure), [rol tabanlı erişim denetimi](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is), [uygulama kullanımını izleme](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health), [zengin denetim](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), ve [izleme ve uyarma güvenlik](https://docs.microsoft.com/azure/operations-management-suite/oms-security-responding-alerts).

Azure Active Directory ile iş ortakları için yayımlama tüm uygulamaları ve müşterilerin (iş veya tüketici) sahip hello aynı kimlik ve erişim yönetimi özellikleri. Bu, toosignificantly işletim maliyetlerini azaltmak olanak tanır.

## <a name="azure-security-center"></a>Azure Güvenlik Merkezi
[Azure Güvenlik Merkezi](https://docs.microsoft.com/azure/security-center/security-center-get-started) hello Azure kaynaklarınızın güvenlik engellemek, algılamak, artırılmış görünürlük aracılığı ile toothreats yanıt ve üzerinden denetlemesine yardımcı olur. Aboneliklerinizde tümleşik güvenlik izleme ve ilke yönetimi sağlar, normal koşullarda gözden kaçabilecek tehditleri algılamaya yardımcı olur ve güvenlik çözümlerinin geniş ekosistemiyle çalışır.

[Güvenlik Merkezi](https://docs.microsoft.com/azure/security-center/security-center-linux-virtual-machine) , koruma azure'da sanal makine verilerinin sanal makinenizin güvenlik ayarlarını görünürlük sağlayarak ve tehditleri için izleme yardımcı olur. Güvenlik Merkezi, sanal makinelerinizi şu açılardan izleyebilir:

-   Yapılandırma kuralları önerilen hello ile işletim sistemi (OS) güvenlik ayarları
-   Sistem güvenliği ve eksik olan kritik güncelleştirmeler
-   Uç nokta koruması önerileri
-   Disk şifreleme doğrulaması
-   Ağ tabanlı saldırılara

Azure Güvenlik Merkezi kullanan [rol tabanlı erişim denetimi (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure), sağlayan [yerleşik roller](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) atanabilen toousers, grupları ve Azure Hizmetleri.

Güvenlik Merkezi kaynakları tooidentify güvenlik sorunları ve güvenlik açıkları hello yapılandırmasını değerlendirir. Güvenlik Merkezi'nde, yalnızca bilgi sahibi, katkıda bulunan veya okuyucu bir kaynağa ait hello abonelik veya kaynak grubu için hello rolüne atandığında ilgili tooa kaynak.

>[!Note]
>Bkz: [izinleri Azure Güvenlik Merkezi'nde](https://docs.microsoft.com/azure/security-center/security-center-permissions) toolearn rolleri ve Güvenlik Merkezi'nde izin verilen eylemleri hakkında daha fazla.

Güvenlik Merkezi, Microsoft Monitoring Agent hello kullanır – aynı aracı hello Operations Management Suite ve günlük analizi hizmeti tarafından kullanılan hello budur. Bu Aracıdan toplanan verileri herhangi bir varolan günlük analizi içinde depolanan [çalışma](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access) hesabı hello coğrafi konuma hello VM, alma, Azure aboneliğinizin veya yeni bir çalışma alanları ile ilişkili.

## <a name="azure-monitor"></a>Azure İzleyici
Performans sorunlarını bulut uygulamanızda iş etkileyebilir. Birden çok birbirine bağlı bileşenleri ve sık sürümleri ile degradations herhangi bir zamanda oluşabilir. Ve kullanıcılarınızın bir uygulama geliştiriyorsanız, genellikle testinde bulamadı sorunları keşfedin. Bu hemen bilmeniz ve hello sorunlarını tanılamak ve araçları olması gerekir.

[Azure İzleyici](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor) Azure üzerinde çalışan hizmetleri izlemek için temel araçtır. Altyapı düzeyinde veri hizmeti ve ortam çevreleyen hello hello işleme hakkında sağlar. Uygulamalarınızda tüm Azure yönetiyorsanız, yukarı veya aşağı kaynakları tooscale, ardından Azure İzleyicisi, ne kullandığınız sunar olup olmadığını karar toostart.

Ayrıca, uygulamanız hakkında izleme verileri toogain ayrıntılı Öngörüler kullanabilirsiniz. Bu bilgi tooimprove uygulama performansı veya bakım yardımcı veya aksi halde el ile müdahale gerektiren Eylemler otomatik hale getirme. Aşağıdakileri içerir:

-   Azure etkinlik günlüğü
-   Azure tanılama günlükleri
-   Ölçümler
-   Azure Tanılama

### <a name="azure-activity-log"></a>Azure etkinlik günlüğü
Aboneliğinizi kaynaklarında gerçekleştirilen hello işlemleri hakkında bilgi sağlayan bir günlüktür. Merhaba [etkinlik günlüğü](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) aboneliklerinizi denetim düzlemi olaylarını raporları olduğundan daha önce "Denetim günlüklerini" veya "İşlem günlükleri," olarak biliniyordu.

### <a name="azure-diagnostic-logs"></a>Azure tanılama günlükleri
[Azure tanılama günlüklerini](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) bir kaynak tarafından gösterilen ve bu kaynağın hello işlemi hakkında zengin, sık veriler sağlar. Bu günlükler Merhaba içeriğine kaynak türüne göre değişir.

Örneğin, Windows olayı sistem günlükleri tanılama günlüğünün VM'ler ve blob, tablo için bir kategori, ve sıra günlükleri tanılama günlüklerini kategorileri depolama hesapları için.

Tanılama günlüklerini farklı hello [etkinlik günlüğü (önceki adıyla denetim günlüğü veya işlem günlüğü olarak bilinir)](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs). Merhaba etkinlik günlüğü aboneliğinizde kaynaklara gerçekleştirilen hello işlemleri hakkında bilgi sağlar. Tanılama günlükleri işlemleri kaynağınız kendisini gerçekleştirilen bir anlayış sağlar.

### <a name="metrics"></a>Ölçümler
Azure İzleyicisi tooconsume telemetri toogain görünürlük hello performans ve iş yüklerinizi Azure üzerinde durumunu sağlar. Merhaba en önemli Azure telemetri verilerini (performans sayaçlarını olarak da bilinir) hello ölçümleri çoğu Azure kaynaklar tarafından gösterilen türüdür. Azure İzleyici birkaç yolu tooconfigure sağlar ve bunlar tüketen [ölçümleri](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) izleme ve sorun giderme için.

### <a name="azure-diagnostics"></a>Azure Tanılama
Bunu hello dağıtılan bir uygulama tanılama verilerini hello koleksiyonunu sağlayan Azure içinde bir özelliktir. Çeşitli farklı kaynaklardan hello tanılama uzantısını kullanabilirsiniz. Şu anda desteklenen [Azure bulut hizmeti Web ve çalışan rolleri](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service), [Azure sanal makineleri](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service) Microsoft Windows çalıştıran ve [Service Fabric](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics).


## <a name="network-watcher"></a>Ağ İzleyicisi
Müşterilerin bir uçtan uca ağ Azure VNet, ExpressRoute, uygulama ağ geçidi, yük Dengeleyiciler ve daha fazlasını gibi çeşitli tek tek ağ kaynaklarına oluşturma ve yönetme tarafından oluşturun. İzleme her hello ağ kaynaklarına kullanılabilir.

Merhaba uç tooend ağ karmaşık yapılandırmalar ve senaryo tabanlı ağ izlemekte gereken karmaşık senaryolar oluşturma kaynakları arasındaki etkileşimler sahip olabilir.

[Ağ İzleyicisi](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) izleme ve Tanılama, Azure ağı basitleştirir. Tanılama ve görselleştirme araçları bulunan bir Azure sanal makinesinde, tootake uzaktan paket yakalar Ağ İzleyicisi'ni etkinleştir akış günlükleri kullanarak, ağ trafiğini alın ve VPN ağ geçidi ve bağlantıları tanılama.

Ağ İzleyicisi'ni şu anda özellikleri aşağıdaki hello sahiptir:

- [Topoloji](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) -bir ağ seviye görünümü gösteren hello çeşitli bağlantılar ve ağ kaynakları bir kaynak grubunda arasındaki ilişkilendirmeleri sağlar.
-   [Değişken paket yakalama](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) -bir sanal makine ve paket verilerini yakalar. Gelişmiş seçenekleri ve mümkün tooset anda gibi ince ayar denetimleri filtreleme ve boyut sınırlamaları yönlülük sağlayın. Merhaba paket verileri blob Mağazası'nda veya .cap biçiminde hello yerel diskte depolanabilir.
-   [IP akışları doğrulayın](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) -paket izin verilen veya reddedilen denetimleri temel akış bilgi 5-tanımlama grubu paket parametrelerine (hedef IP, kaynak IP, hedef bağlantı noktası, kaynak bağlantı noktası ve protokol). Başlangıç paketi bir güvenlik grubu tarafından engellenirse hello kuralı ve hello Paket reddedildi Grup döndürülür.
-   [Sonraki atlama](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) -hello toodiagnose herhangi yanlış yapılandırılmış kullanıcı tanımlı yollar etkinleştirme Azure ağ yapısında yönlendirilen paketler için sonraki atlama hello belirler.
-   [Güvenlik grubu görünümü](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) -bir VM üzerinde uygulanan hello etkili ve uygulanan güvenlik kuralları alır.
-   [NSG akış günlük](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) -akış günlükleri ağ güvenlik grupları için izin verilen veya hello Grup hello güvenlik kuralları tarafından reddedilen toocapture günlükleri ilgili tootraffic sağlar. Merhaba akışı bir 5-tanımlama grubu bilgileriyle – kaynak IP, hedef IP, kaynak bağlantı noktası, hedef bağlantı noktası ve protokol tanımlanır.
-   [Sanal ağ geçidi ve bağlantı sorunlarını giderme](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) -hello özelliği tootroubleshoot sağlayan sanal ağ geçitleri ve ağ bağlantıları.
-   [Ağ abonelik sınırları](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) -sınırları karşı tooview ağ kaynağı kullanımı sağlar.
-   [Tanılama günlük yapılandırma](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) – bölmeden tooenable sağlar veya bir kaynak grubunda ağ kaynakları için tanılama günlükleri devre dışı bırakın.

Daha fazla nasıl tooconfigure Ağ İzleyicisi bakın, toolearn [Ağ İzleyicisi'ni yapılandırma](https://docs.microsoft.com/azure/network-watcher/network-watcher-create).

## <a name="developer-operations-devops"></a>Geliştirici işlemleri (DevOps)
Önceki tooDevOps uygulama geliştirme ekipleri yazılım programı için iş gereksinimlerini toplama ve kod yazma sorumlu yoktu. Sonra ayrı bir QA takım hello program bir yalıtılmış geliştirme ortamında, gereksinimlerin karşılanıp karşılanmadığı ve işlemleri toodeploy kodunu sürümleri hello sınar. Merhaba dağıtım ekipleri daha fazla ağ ve veritabanı gibi siloed gruplar halinde parçalanmış. Bir yazılım programının "oluşur hello duvar" her zaman tooan bağımsız takım performans sorunlarını ekler.

[DevOps](https://www.visualstudio.com/learn/what-is-devops/) etkinleştirir, takımlar toodeliver daha hızlı ve ucuz daha güvenli, daha yüksek kaliteli çözümler. Müşteriler, yazılım ve hizmetlerini kullanırken dinamik ve güvenilir bir deneyim bekler.  Takımlar yazılım güncelleştirmelerini, hızlı bir şekilde yinelemek gerekir hello güncelleştirmeleri hello etkisini ölçüyor ve yeni geliştirme yineleme tooaddress sorunları hızla yanıt veya daha fazla değer sağlayın.  Microsoft Azure gibi bulut platformlarıyla geleneksel performans sorunlarını kaldırıldı ve altyapı commoditize Yardım. Yazılım, temel fark yatan unsur ve işletme sonuçlarını faktörünü hello gibi her iş reigns. Hiçbir kuruluş, geliştirici ve BT çalışan olabilir veya hello DevOps taşıma kaçınmalısınız.

Olgun DevOps uygulayıcıları hello yöntemler aşağıdaki çeşitli benimser. Bu yöntemler [kişileri içeren](https://www.visualstudio.com/learn/what-is-devops-culture/) tooform stratejileri hello iş senaryolarını temel alarak.  Araç otomatikleştirmek yardımcı çeşitli yöntemler hello:

-   [Çevik planlama ve proje yönetimi](https://www.visualstudio.com/learn/what-is-agile/) teknikleri kullanılan tooplan olan ve yalıtmak iş sprint içine, ekip kapasitesi yönetmek ve Yardım hızla toochanging iş ihtiyaçlarınıza uyum ekipler.
-   [Sürüm denetimi, genellikle Git ile](https://www.visualstudio.com/learn/what-is-git/), herhangi bir yere hello world tooshare kaynağında bulunan takımlar etkinleştirir ve yazılım geliştirme araçları tooautomate hello yayın ardışık düzeni ile tümleştirin.
-   [Sürekli Tümleştirme](https://www.visualstudio.com/learn/what-is-continuous-integration/) sürücüleri hello sürekli birleştirme ve toofinding kusurları erken müşteri adayları kodu test etme.  Birleştirme sorunlar ve hızlı geri bildirim geliştirme ekipleri için mücadele küçülttüğü iyi bir şekilde daha az zaman diğer avantajlar şunlardır.
-   [Kesintisiz teslim](https://www.visualstudio.com/learn/what-is-continuous-delivery/) yazılım çözümlerini tooproduction ve test ortamları hızlı bir şekilde hataları düzeltin ve iş tooever değiştirme yanıt yardımcı gereksinimleri.
-   [İzleme](https://www.visualstudio.com/learn/what-is-monitoring/) çalışan uygulamalar üretim ortamları için uygulama durumu da dahil olmak üzere müşteri kullanım Yardım kuruluşlar form olarak bir varsayım yanı sıra ve hızlı bir şekilde doğrulamak veya stratejileri disprove.  Zengin veri yakalanan ve çeşitli günlük biçimlerde depolanır.
-   [Kod (IaC) olarak altyapı](https://www.visualstudio.com/learn/what-is-infrastructure-as-code/) hello otomasyon ve doğrulama oluşturma ve güvenli, kararlı uygulama platformları barındırma teslim ile ağlar ve sanal makineleri toohelp erdirme sağlayan bir uygulama.
-   [Mikro](https://www.visualstudio.com/learn/what-are-microservices/) çevrelerini tooisolate iş kullanımı durumlarını küçük yeniden kullanılabilir hizmetlerine bir mimaridir.  Bu mimari, ölçeklenebilirlik ve verimlilik sağlar.

## <a name="next-steps"></a>Sonraki adımlar
OMS güvenlik ve denetim çözümü hakkında daha fazla toolearn makaleler hello bakın:

- [Operations Management Suite | Güvenlik ve Uyumluluk](https://www.microsoft.com/cloud-platform/security-and-compliance).
- [İzleme ve yanıt tooSecurity uyarıları Operations Management Suite güvenlik ve denetim çözümü](https://docs.microsoft.com/en-us/azure/operations-management-suite/oms-security-responding-alerts).
- [Operations Management Suite güvenlik ve denetim çözümü kaynakları izleme](https://docs.microsoft.com/en-us/azure/operations-management-suite/oms-security-monitoring-resources).
