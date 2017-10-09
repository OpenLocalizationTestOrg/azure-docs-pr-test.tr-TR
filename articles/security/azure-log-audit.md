---
title: "günlüğe kaydetme ve denetim aaaAzure | Microsoft Docs"
description: "Nasıl günlük veri toogain ayrıntılı Öngörüler uygulamanız hakkında kullanabileceğiniz hakkında bilgi edinin."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: d0e817b071962ad9bef6250267092b5f9282bc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-logging-and-auditing"></a>Azure günlüğe kaydetme ve denetleme
## <a name="introduction"></a>Giriş
### <a name="overview"></a>Genel Bakış
anlama ve kullanma tooassist geçerli ve gelecekteki Azure müşterilerin çeşitli güvenlikle ilgili özellikleri bulunan hello ve hello Azure platformu çevreleyen, Microsoft teknik incelemeler, güvenlik genel bakışlar, en iyi yöntemler, bir dizi geliştirmiştir ve denetim listeleri. Merhaba konuları avantajlarına ve derinliği bakımından aralığı ve düzenli aralıklarla güncelleştirilir. Bu belge, soyut bölümden hello özetlendiği gibi serisi bir parçası değil.
### <a name="azure-platform"></a>Azure platformu
Azure işletim sistemlerinin programlama dilleri, çerçeveleri, Araçlar, veritabanları ve cihazları, en geniş seçim hello destekleyen açık ve esnek bir bulut hizmeti platformudur.

Örneğin, şunları yapabilirsiniz:
-   Linux kapsayıcıları Docker Tümleştirmesi ile çalıştırın.

-   JavaScript, Python, .NET, PHP, Java ve Node.js ile uygulamalar oluşturma

-   Yapı geri-iOS, Android ve Windows cihazları sona erer.

Azure genel bulut Hizmetleri, geliştiriciler ve BT uzmanları, aynı teknolojileri milyonlarca zaten kullanır ve güven hello destekler.

Oluşturmanıza veya BT varlıklar, bir bulut sağlayıcısına geçiş yapma, uygulamalarınızı, bir kuruluşun yeteneklerini tooprotect üzerinde bağlı ve hizmetler ve hello denetimleri ile veri hello toomanage hello güvenlik bulut tabanlı varlıklarınızın sağlarlar.

Azure'nın altyapı hello tesis tooapplications aynı anda milyonlarca müşteri barındırmak için gelen tasarlanmıştır ve güvenlik gereksinimlerine bağlı işletmeler karşılayabilecek güvenilir bir temel sağlar. Ayrıca, Azure, çok çeşitli yapılandırılabilir güvenlik seçenekleri ve hello özelliği toocontrol sağlar bunları böylece güvenlik toomeet hello benzersiz gereksinimlerini dağıtımlarınızı özelleştirebilirsiniz. Bu belge yardımcı olur, bu gereksinimleri karşılayan.

### <a name="abstract"></a>Özet
Denetim ve güvenlikle ilgili olaylar ve ilgili uyarıları günlük kaydını etkili verileri koruma stratejisi, önemli bileşenleridir. Güvenlik günlüklerini ve raporları kuşkulu etkinlikleri ve iç saldırıların yanı sıra hello ağ denenen veya başarılı dış sızma gösterebilir desenlerini algılayabilir Yardım elektronik bir kayıtla sağlar. Adli analiz gerçekleştirmek, Denetim toomonitor kullanıcı etkinliği, belge Mevzuat uyumluluğu kullanın. Güvenlik olayları oluştuğunda uyarılar anında bildirim sağlar.

Microsoft Azure Hizmetleri ve ürünleriyle yapılandırılabilir güvenlik denetimi ile sağlamak ve güvenlik ilkeleri ve mekanizmaları çözebileceğiniz boşlukları tanımlar ve bu boşluklar toohelp Adres seçenekleri toohelp günlüğü ihlallerini engelleyebilirsiniz. Bazı Microsoft hizmetleri sunar (ve bazı durumlarda, tüm), aşağıdaki seçenekleri şu hello: izleme, günlüğe kaydetme ve analiz sistemleri tooprovide sürekli görünürlüğü; Merkezi zamanında uyarıları; ve raporları toohelp hello büyük miktarda bilgi cihazları ve Hizmetleri tarafından oluşturulan yönetin.

Microsoft Azure günlük verilerini dışa aktarılan tooSecurity çözümleme için olay ve Olay yönetimi (SIEM) sistemleri olabilir ve üçüncü taraf denetim çözümler ile entegre olur.

Bu teknik oluşturma, toplama ve güvenlik günlüklerini Azure üzerinde barındırılan hizmetlerden analiz için bir giriş sağlar ve Azure dağıtımlarınızı güvenlik Öngörüler elde yardımcı olabilir. Bu teknik incelemede Hello kapsamını sınırlı tooapplications olan ve yerleşik ve azure'da dağıtılan Hizmetleri.

> [!Note]
> Burada yer alan bazı öneriler artan veri, ağ ya da işlem kaynağı kullanımına neden ve lisans ya da abonelik maliyetlerinizi artırabilir.

## <a name="types-of-logs-in-azure"></a>Azure günlükleri türleri
Bulut uygulamalarını birçok taşıma bölümleriyle karmaşıktır. Günlükleri, uygulamanızı kurma kalır veri tooensure ve iyi durumda çalışan sağlar. Olası sorunlar kapalı veya olanları sorun giderme, toostave yardımcı olur. Ayrıca, uygulamanız hakkında günlük veri toogain ayrıntılı Öngörüler kullanabilirsiniz. Bu bilgi tooimprove uygulama performansı veya bakım yardımcı veya aksi halde el ile müdahale gerektiren Eylemler otomatik hale getirme.

Azure Azure her hizmet için ayrıntılı günlük kaydını üretir. Bu günlükler, bu ana türleri tarafından kategorilere ayrılır:
-   **Denetim/Yönetim günlüklerini** Azure Kaynak Yöneticisi oluşturma, güncelleştirme ve silme işlemleri hello görünürlük sağlar. [Azure etkinlik günlükleri](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) günlük bu tür bir örneğidir.

-   **Veri günlüklerini düzlemine** bir Azure kaynağı hello kullanımını bir parçası olarak oluşturulan hello olaylara görünürlük sağlar. Bu günlük türü örnekler Windows olayı sistem, güvenlik, hello ve uygulama günlüklerini bir sanal makine ve hello [tanılama günlükleri](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) Azure İzleyicisi aracılığıyla yapılandırılmış


-   **İşlenen olayların** sizin adınıza çözümlenen olaylar/işlenen Uyarıları hakkında bilgi verin. Bu tür örnekleri [Azure Güvenlik Merkezi uyarılarını](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) nerede [Azure Güvenlik Merkezi](https://docs.microsoft.com/azure/security-center/security-center-intro) işlenir ve aboneliğinizi analiz ve kısa güvenlik uyarıları sağlar

Merhaba aşağıdaki liste en önemli Azure'da kullanılabilir günlük türünde tablo.

| Günlük kategorisi | Günlük türü | Kullanımları | Tümleştirme |
| ------------ | -------- | ------ | ----------- |
|[Etkinlik günlükleri](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)|Azure Resource Manager kaynaklarını denetim düzlemi olayları| Aboneliğinizi kaynaklarında gerçekleştirilen hello işlemleri hakkında bilgi sağlar.|   REST API & [Azure İzleyicisi](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)|
|[Azure tanılama günlükleri](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)|Sık kullanılan veri Abonelikteki Azure Resource Manager kaynakların hello işlemi hakkında| Operations kaynağınız kendisini gerçekleştirilen bir anlayış sağlayın| Azure İzleyici [akış](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)|
|[AAD raporlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-azure-portal)|Günlüklerini ve raporları|Kullanıcı oturum açma etkinliklerini & kullanıcı ve Grup Yönetimi hakkında sistem etkinlik bilgileri|[Grafik API'si](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-graph-api-quickstart)|
|[Sanal makine ve bulut Hizmetleri](https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)|Windows olay günlüğü & Linux Syslog|  Sistem verileri ve günlük verilerini hello sanal makinelerde yakalar ve bu verileri tercih ettiğiniz bir depolama hesabına aktarır.| Windows kullanarak [WAD](https://docs.microsoft.com/en-us/azure/azure-diagnostics) (Windows Azure Diagnostics depolama) ve Linux Azure İzleyicisi|
|[Depolama Analizi](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/storage-analytics)|Depolama günlüğe kaydetme ve ölçüm verileri için bir depolama hesabı sağlar|Insight sağlar trace istekleri, kullanım eğilimlerini çözümleme ve depolama hesabınız ile ilgili sorunları tanılamak.|  REST API veya hello [istemci kitaplığı](https://msdn.microsoft.com/en-us/library/azure/mt347887.aspx)|
|[NSG (ağ güvenlik grubu) akış günlükleri](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview)|JSON biçimi ve bir kural başına temelinde giden ve gelen akışları gösterir|Giriş ve çıkış IP trafiği bir ağ güvenlik grubu ile ilgili bilgileri görüntüleyin|[Ağ İzleyicisi](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)|
|[Uygulama Insight](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-overview)|Günlükleri, özel durumlar ve özel tanılama|  Uygulama performansı Yönetimi (APM) hizmeti birden çok platformdaki web geliştiricileri için.| REST API [Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-azure-and-power-bi/)|
|Veri işleme / Güvenlik Uyarısı| Azure Güvenlik Merkezi uyarı, OMS Uyarısı| Güvenlik bilgileri ve Uyarıları.|   REST API'leri, JSON|

### <a name="activity-log"></a>Etkinlik Günlüğü
Merhaba [Azure etkinlik günlüğü](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs), aboneliğinizde kaynaklara gerçekleştirilen hello işlemleri hakkında bilgi sağlar. Rapor beri hello etkinlik günlüğü daha önce "Denetim günlüklerini" veya "İşlem günlükleri," olarak biliniyordu [denetim düzlemi olayları](https://driftboatdave.com/2016/10/13/azure-auditing-options-for-your-custom-reporting-needs/) aboneliklerinizi için. Merhaba etkinlik günlüğü kullanarak hello belirleyebilirsiniz "ne, kim, ne zaman ve" herhangi bir yazma işlemleri (PUT, POST, DELETE) aboneliğinizde hello kaynaklar üzerinde gerçekleştirilecek için. Merhaba hello işleminin durumunu ve ilgili diğer özellikleri de anlayabilirsiniz. Merhaba etkinlik günlüğü okuma (GET) işlemleri içermez.

Burada PUT, POST, DELETE etkinlik günlüğü hello kaynakları içeren tooall hello yazma işlemlerini ifade eder. Örneğin, hello etkinlik günlükleri toofind sorun giderme sırasında bir hata veya toomonitor kullanabilirsiniz, kuruluşunuzdaki bir kullanıcı bir kaynak nasıl değişiklik.

![Etkinlik Günlüğü](./media/azure-log-audit/azure-log-audit-fig1.png)


Olaylar, etkinlik hello Azure portal kullanarak günlüğü alabilir [CLI](https://docs.microsoft.com/azure/storage/storage-azure-cli), PowerShell cmdlet'leri ve [Azure İzleyici REST API](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-rest-api-walkthrough). Etkinlik günlükleri 19 günlük veri saklama süresi vardır.

Tümleştirme senaryolarına
-   [Bir etkinlik günlüğü olay tetikler bir e-posta veya Web kancası uyarı oluşturabilir.](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-auditlog-to-webhook-email)

-   [Olay hub'ı tooan akış](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-stream-activity-logs-event-hubs) bir üçüncü taraf hizmeti veya Powerbı gibi özel analiz çözümü tarafından alımı için.

-   Hello kullanarak Powerbı içinde analiz [Power BI içerik paketi.](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/)

-   [Arşiv veya el ile İnceleme için depolama hesabı tooa kaydedin.](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-archive-activity-log) Günlük profilleri kullanarak hello bekletme süresi (gün) belirtebilirsiniz.

-   Sorgulamak ve hello Azure portalında görüntüleyin.

-   PowerShell Cmdlet, CLI veya REST API sorgu.

-   Merhaba etkinlik günlüğü günlük profilleriyle çok dışarı[Analytics oturum](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview).

Bir depolama hesabı kullanabilir veya [olay hub'ı ad](https://docs.microsoft.com/azure/event-hubs/event-hubs-resource-manager-namespace-event-hub-enable-archive) içinde değil tek bir verme günlük hello gibi aynı abonelik hello. Merhaba ayarı yapılandıran hello kullanıcının hello uygun olmalıdır [RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) erişim tooboth abonelikleri
### <a name="azure-diagnostic-logs"></a>Azure tanılama günlükleri
Azure tanılama günlüklerini hello işlemi bu kaynağın hakkında zengin, sık sık veri sağlayan bir kaynak tarafından gösterilen. Bu günlükler Merhaba içeriğine kaynak türüne göre değişir (örneğin, [Windows olayı sistem günlükleri](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)VM'ler için bir kategori tanılama günlüğünün olan ve [blob, tablo ve kuyruk günlükleri](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account) tanılama günlüklerinin kategoriler Depolama hesapları için) ve hello aboneliğinizde kaynaklara gerçekleştirilen hello işlemleri hakkında bilgi sağlayan etkinlik günlüğü farklıdır.

![Azure tanılama günlükleri](./media/azure-log-audit/azure-log-audit-fig2.png)

Azure tanılama günlükleri, birden çok olan yapılandırma seçenekleri, PowerShell, komut satırı arabirimi (CLI) ve REST API kullanarak Azure portalında sunar.

**Tümleştirme senaryolarına**
-   Tooa kaydetmek [depolama hesabı](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-archive-diagnostic-logs) denetim veya el ile İnceleme için. Merhaba tanılama ayarlarını kullanarak hello bekletme süresi (gün) belirtebilirsiniz.

-   [TooEvent hub akış](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs) bir üçüncü taraf hizmeti veya gibi özel analiz çözümü tarafından alımı için [Powerbı.](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

-   Bunları ile analiz [OMS günlük analizi.](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

**Tanılama günlüklerini ve kaynak türü başına desteklenen bir günlük kategorileri için şema Hizmetleri, desteklenen**


| Hizmet | Şema & belgeleri | Kaynak Türü | Kategori |
| ------- | ------------- | ------------- | -------- |
|Yük Dengeleyici| [Azure yük dengeleyici (Önizleme) için günlük analizi](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-monitor-log)|Microsoft.Network/loadBalancers|  LoadBalancerAlertEvent|
|||Microsoft.Network/loadBalancers| LoadBalancerProbeHealthStatus
|Ağ Güvenlik Grupları|[Ağ güvenlik grupları (NSG’ler) için Log Analytics](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-nsg-manage-log)|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupEvent|
|||Microsoft.Network/networksecuritygroups|NetworkSecurityGroupRuleCounter|
|Application Gatewayler|[Uygulama ağ geçidi için tanılama günlükleri](https://docs.microsoft.com/en-us/azure/application-gateway/application-gateway-diagnostics)|Microsoft.Network/applicationGateways|ApplicationGatewayAccessLog|
|||Microsoft.Network/applicationGateways|ApplicationGatewayPerformanceLog|
|||Microsoft.Network/applicationGateways|ApplicationGatewayFirewallLog|
|Anahtar Kasası|[Azure Anahtar Kasası Günlüğü](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-logging)|Microsoft.KeyVault/vaults|AuditEvent|
|Azure Search|[Etkinleştirme ve arama trafiği Analytics kullanma](https://docs.microsoft.com/en-us/azure/search/search-traffic-analytics)|Microsoft.Search/searchServices|OperationLogs|
|Data Lake Store|[Azure Data Lake Store için tanılama günlüklerine erişme](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-diagnostic-logs)|Microsoft.DataLakeStore/accounts|Denetim|
|Data Lake Analytics|[Azure Data Lake Analytics’te tanılama günlüklerine erişim](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-diagnostic-logs)|Microsoft.DataLakeAnalytics/accounts|Denetim|
|||Microsoft.DataLakeAnalytics/accounts|İstekler|
|||Microsoft.DataLakeStore/accounts|İstekler|
|Logic Apps|[Logic Apps B2B özel izleme şeması](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-track-integration-account-custom-tracking-schema)|Microsoft.Logic/workflows|İş akışı WorkflowRuntime|
|||Microsoft.Logic/integrationAccounts|IntegrationAccountTrackingEvents|
|Azure Batch|[Azure Batch Tanılama Günlüğü](https://docs.microsoft.com/en-us/azure/batch/batch-diagnostics)|Microsoft.Batch/batchAccounts|ServiceLog|
|Azure Otomasyonu|[Azure otomasyonu için günlük analizi](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics)|Microsoft.Automation/automationAccounts|JobLogs|
|||Microsoft.Automation/automationAccounts|JobStreams|
|Event Hubs|[Azure Event Hubs tanılama günlükleri](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-diagnostic-logs)|Microsoft.EventHub/namespaces|ArchiveLogs|
|||Microsoft.EventHub/namespaces|OperationalLogs|
|Akış Analizi|[İş tanılama günlükleri](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-job-diagnostic-logs)|Microsoft.StreamAnalytics/streamingjobs|Yürütme|
|||Microsoft.StreamAnalytics/streamingjobs|Yazma|
|Service Bus|[Azure Service Bus tanılama günlükleri](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-diagnostic-logs)|Microsoft.ServiceBus/namespaces|OperationalLogs|

### <a name="azure-active-directory-reporting"></a>Azure Active Directory raporlama
Azure Active Directory (Azure AD), dizininize yönelik güvenlik, etkinlik ve denetim raporlarını içerir. Merhaba [Azure Active Directory denetim raporu](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) , müşterilerin kendi Azure Active Directory'de oluştu tooidentify ayrıcalıklı Eylemler yardımcı olur. Ayrıcalıklı Eylemler dahil ayrıcalık değişiklikler (örneğin, rolü oluşturma veya parola sıfırlama) ilkesi yapılandırmaları (örneğin, parola ilkelerinin) veya değişiklikleri toodirectory yapılandırması (örneğin, değişiklikleri toodomain Federasyon ayarları) değiştirme.

Merhaba raporları hello denetim kaydı hello olay adı, hello eylemin hello değişiklik ve hello tarih ve saat (UTC içinde) etkilenen hello hedef kaynak gerçekleştiren hello aktör sağlar. Müşterilerdir mümkün tooretrieve hello hello aracılığıyla kendi Azure Active Directory için denetim olayları listesini [Azure portal](https://portal.azure.com/)açıklandığı gibi [denetim günlüklerini görüntülemek](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal). Dahil hello raporları listesi aşağıdadır:

| Güvenlik raporları | Etkinlik raporları | Denetim raporları |
| :--------------- | :--------------- | :------------ |
|Bilinmeyen kaynaklardan gerçekleştirilen oturum açma işlemleri| Uygulama kullanımı: özet| Dizin denetimi raporu|
|Birden çok hatadan sonra gerçekleştirilen oturum açma işlemleri|  Uygulama kullanımı: ayrıntılı||
|Birden çok coğrafyadan gerçekleştirilen oturum açma işlemleri|    Uygulama panosu||
|Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum açma işlemleri|   Hesap hazırlama hataları||
|Düzensiz oturum açma etkinliği|    Bireysel kullanıcı cihazları||
|Muhtemelen virüs bulaşmış cihazlardan gerçekleştirilen oturum açma işlemleri|   Bireysel kullanıcı Etkinliği||
|Anormal oturum açma etkinliği gösteren kullanıcılar| Grup etkinlik raporu||
||Parola Sıfırlama Kayıt Etkinlik Raporu||
||Parola sıfırlama etkinliği|||

Bu raporların Hello veriler SIEM sistemlerinden, Denetim ve iş zekası araçları gibi yararlı tooyour uygulamalar olabilir. bir dizi REST tabanlı API'ler aracılığıyla programlı erişim toohello veri API'leri sağlamak Hello Azure AD raporlama. Bu çağrı [API'leri](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started) çeşitli programlama dilleri ve araçları.

Hello Azure AD Denetim Raporu olayları 180 gün boyunca saklanır.

> [!Note]
> Raporlarda bekletme hakkında daha fazla bilgi için bkz: [Azure Active Directory rapor bekletme ilkeleri.](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention)

Müşteriler için daha uzun bekletme dönemleri bunların denetim olaylarını depolanırken ilgilenen, hello raporlama API'si olabilir tooregularly çekme kullanılan [olaylarını denetleme](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-audit-events) ayrı veri deposuna.

### <a name="virtual-machine-logs-using-azure-diagnostics"></a>Azure Tanılama'yı kullanarak sanal makine günlükleri
[Azure tanılama](https://docs.microsoft.com/azure/azure-diagnostics) dağıtılan bir uygulama tanılama verilerini hello koleksiyonunu sağlayan Azure içinde hello özelliğidir. Birkaç farklı kaynaklardan hello tanılama uzantısını kullanabilirsiniz. Şu anda desteklenen [Azure bulut hizmeti Web ve çalışan rolleri](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me),

![Azure Tanılama'yı kullanarak sanal makine günlükleri](./media/azure-log-audit/azure-log-audit-fig3.png)

[Azure sanal makineleri](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/) Microsoft Windows çalıştıran ve [Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview).

Azure tanılama kullanarak sanal makine etkinleştirebilirsiniz aşağıdaki:

-   Visual Studio kullanarak bkz [Visual Studio'yu kullanın tootrace Azure sanal makineler](https://docs.microsoft.com/azure/vs-azure-tools-debug-cloud-services-virtual-machines)

-   [Bir Azure sanal makine uzaktan üzerinde Azure tanılama ayarlama](https://docs.microsoft.com/azure/virtual-machines-dotnet-diagnostics)

-   [Azure sanal makinelerde tanılama yukarı PowerShell tooset kullanın](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-ps-extensions-diagnostics?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

-   [İzleme ve tanılama Azure Resource Manager şablonu kullanarak bir Windows sanal makine oluşturma](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-extensions-diagnostics-template?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="storage-analytics"></a>Depolama Analizi
[Azure Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) günlüğe kaydetme işlemlerini gerçekleştiren ve ölçümler veriler için bir depolama hesabı sağlar. Bu veri tootrace istekleri kullanır, kullanım eğilimleri çözümlemek ve depolama hesabınızla sorunlarını tanılamak. Storage Analytics günlük Merhaba kullanılabilir [Blob, kuyruk ve tablo hizmetlerine.](https://docs.microsoft.com/azure/storage/storage-introduction) Storage Analytics başarılı ve başarısız istekleri tooa depolama birimi hizmeti hakkındaki ayrıntılı bilgileri kaydeder.

Bu bilgiler kullanılan toomonitor istekleri ayrı ayrı ve depolama hizmeti toodiagnose sorunları olabilir. İstekleri en iyi çaba ilkesine göre günlüğe kaydedilir. Merhaba Hizmeti uç noktası karşı yapılan istekleri varsa günlük girişleri oluşturulur. Örneğin, bir depolama hesabı, Blob uç etkinlik vardır, ancak kendi tablo veya kuyruğu uç noktalarını, yalnızca ilgili günlüğe değil toohello Blob hizmeti oluşturulur.

Storage Analytics toouse etkinleştirmeniz gerekir, tek tek her hizmet için toomonitor istediğiniz. Hello etkinleştirmek [Azure portal](https://portal.azure.com/); Ayrıntılar için bkz: [hello Azure portalında bir depolama hesabını izleme.](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account) Storage Analytics hello REST API aracılığıyla programlı olarak veya hello istemci kitaplığı da etkinleştirebilirsiniz. Merhaba hizmet özelliklerini ayarlama işlemi tooenable Storage Analytics her hizmet için ayrı ayrı kullanın.

Merhaba toplanan veriler (günlük için) iyi bilinen bir blob ve hello Blob hizmeti ve tablo hizmeti API'leri kullanılarak erişilebilecek (için ölçümleri), iyi bilinen tablolara depolanır.

Storage Analytics bir 20-TB hello depolama hesabınız için toplam sınırı hello bağımsızdır depolanan veri miktarına sahiptir. Tüm günlükler depolanmış [blok blobları](https://docs.microsoft.com/azure/storage/storage-analytics) $logs adlı bir kapsayıcıda, otomatik olarak oluşturulan depolama çözümlemeleri için bir depolama hesabı etkin olduğunda.

> [!Note]
> Faturalama ve veri bekletme ilkeleri hakkında daha fazla bilgi için bkz: [Storage Analytics ve faturalama.](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-and-billing)
>
> [!Note]
> Depolama hesabı sınırları hakkında daha fazla bilgi için bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri.](https://docs.microsoft.com/azure/storage/storage-scalability-targets)

Kimliği doğrulanmış ve anonim istek türlerini aşağıdaki hello günlüğe kaydedilir.



| Kimlik doğrulaması  | Anonim|
| :------------- | :-------------|
| Başarılı istekler | Başarılı istekler |
|İstek zaman aşımı, azaltma, ağ, yetkilendirme ve başka hatalar da dahil olmak üzere, başarısız oldu | Başarılı ve başarısız istekleri dahil olmak üzere paylaşılan erişim imzası (SAS), kullanarak istekleri |
| Başarılı ve başarısız istekleri dahil olmak üzere paylaşılan erişim imzası (SAS), kullanarak istekleri |İstemci ve sunucu zaman aşımı hataları |
|   İstekleri tooanalytics veri |    304 (değişiklik) hata koduyla başarısız olan GET istekleri |
| Storage Analytics kendisini günlük oluşturma veya silme gibi tarafından yapılan istekleri günlüğe kaydedilmez. Oturum hello verilerin tam bir liste hello belgelenen [depolama Analytics günlüğe yazılan işlemler ve durum iletileri](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) ve [depolama Analytics günlük biçimi](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format) Konular. | Diğer tüm başarısız anonim istekler günlüğe kaydedilmez. Oturum hello verilerin tam bir liste hello belgelenen [depolama Analytics günlüğe yazılan işlemler ve durum iletileri](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) ve [depolama Analytics günlük biçimi](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format). |

### <a name="azure-networking-logs"></a>Azure ağ günlükleri
Günlüğe kaydetme ve Azure'da izleme ağ kapsamlı ve iki geniş kategorisi kapsar:

-   [Ağ İzleyicisi](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) -senaryo tabanlı ağ izleme Ağ İzleyicisi Merhaba özellikleriyle sağlanır. Bu hizmet içeren paket yakalama, sonraki atlama IP akış, güvenlik grubu görünümü, NSG akış günlükleri doğrulayın. Senaryo düzeyi izleme Karşıtlık tooindividual ağ kaynak izleme ağ kaynaklarına bir uçtan tooend görünümünü sağlar.

-   [Kaynak İzleme](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-resource-level-monitoring) -kaynak düzeyi izleme dört özellikleri, tanılama günlükleri, ölçümleri, sorun giderme ve kaynak durumu oluşur. Bu özelliklerin tümü hello ağ kaynak düzeyinde oluşturulur.

![Azure ağ günlükleri](./media/azure-log-audit/azure-log-audit-fig4.png)

Ağ İzleyicisi'ni ve koşullar bir ağ düzeyinde senaryo içinde gelen ve giden Azure Tanılama, toomonitor sağlayan bölgesel bir hizmettir. Ağ Tanılama ve görselleştirme Ağ İzleyicisi ile kullanılabilen araçlar anlamak, tanılama ve Öngörüler tooyour Azure ağında geçirmesine yardımcı olur.

**NSG akış günlük** -akış günlükleri ağ güvenlik grupları için izin verilen veya hello Grup hello güvenlik kuralları tarafından reddedilen toocapture günlükleri ilgili tootraffic sağlar. Bu akış günlükleri JSON biçiminde yazılmıştır ve giden Göster gelen akış kuralı başına temelinde hello NIC hello akış uygular, 5-tanımlama grubu ilgili bilgilere hello akış (kaynak/hedef IP, kaynak/hedef bağlantı noktası, Protokolü) ve hello varsa trafiğine izin veya engellendi.

### <a name="network-security-group-flow-logging"></a>Ağ güvenlik grubu akışı günlüğe kaydetme

[Ağ güvenlik grubu akış günlükleri](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) giriş ve çıkış IP trafiği bir ağ güvenlik grubu aracılığıyla tooview bilgilerini sağlayan Ağ İzleyicisi bir özelliğidir. Bu akış günlükleri JSON biçiminde yazılmıştır ve giden Göster gelen akış kuralı başına temelinde hello NIC hello akış uygular, 5-tanımlama grubu ilgili bilgilere hello akış (kaynak/hedef IP, kaynak/hedef bağlantı noktası, Protokolü) ve hello varsa trafiğine izin veya engellendi.

Hedef ağ güvenlik grupları akış günlükleri, ancak bunlar görüntülenmez aynı hello diğer günlükler hello. Akış günlükleri yalnızca bir depolama hesabında depolanır.

aynı hello diğer açtığında görülen bekletme ilkeleri uygulamak tooflow günlükleri. Günlükleri 1 gün too365 gün ayarlanabilir bir bekletme ilkesi vardır. Hello günlükleri sonsuza kadar bir bekletme ilkesi ayarlanmamışsa saklanır.

**Tanılama günlükleri**

Dönemsel ve spontaneous olayları ağ kaynakları tarafından oluşturulan ve gönderilen tooan olay hub'ı ya da günlük analizi depolama hesaplarında oturum. Bu günlükleri bir kaynak hello durumunu fikir sağlar. Bu günlükler Power BI ve günlük analizi gibi araçları görüntülenebilir. nasıl tooview tanılama günlükleri, ziyaret toolearn [günlük analizi.](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-networking-analytics)

![Tanılama günlükleri](./media/azure-log-audit/azure-log-audit-fig5.png)

Tanılama günlükleri için kullanılabilir [yük dengeleyici](https://docs.microsoft.com/azure/load-balancer/load-balancer-monitor-log), [ağ güvenlik grupları](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log), yollar ve [uygulama ağ geçidi.](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics)

Ağ İzleyicisi görünümü bir tanılama günlükleri sağlar. Bu görünüm, tanılama günlüğünün destekleyen tüm ağ kaynaklarını içerir. Bu görünümden etkinleştirin ve ağ kaynaklarını kolayca ve hızlı bir şekilde devre dışı bırakın.


Toplama toopreceding günlük yeteneği, Ağ İzleyicisi'ni şu anda özellikleri aşağıdaki hello sahiptir:
- [Topoloji](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) -bir ağ seviye görünümü gösteren hello çeşitli bağlantılar ve ağ kaynakları bir kaynak grubunda arasındaki ilişkilendirmeleri sağlar.

- [Değişken paket yakalama](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) -bir sanal makine ve paket verilerini yakalar. Gelişmiş filtreleme seçenekleri ve mümkün tooset olması gibi ince ayar denetimleri, zaman ve boyut sınırlamaları versatility.hello paket verileri blob Mağazası'nda veya .cap biçiminde hello yerel diskte depolanan sağlar.

-   [IP akış doğrular](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) -paket izin verilen veya reddedilen denetimleri temel akış bilgi 5-tanımlama grubu paket parametrelerine (hedef IP, kaynak IP, hedef bağlantı noktası, kaynak bağlantı noktası ve protokol). Başlangıç paketi bir güvenlik grubu tarafından engellenirse hello kuralı ve hello Paket reddedildi Grup döndürülür.

-   [Sonraki atlama](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) -hello toodiagnose herhangi yanlış yapılandırılmış kullanıcı tanımlı yollar etkinleştirme Azure ağ yapısında yönlendirilen paketler için sonraki atlama hello belirler.

-   [Güvenlik grubu görünümü](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) -bir VM üzerinde uygulanan hello etkili ve uygulanan güvenlik kuralları alır.

-   [Sanal ağ geçidi ve bağlantı sorunlarını giderme](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) -hello özelliği tootroubleshoot sağlayan sanal ağ geçitleri ve ağ bağlantıları.

-   [Ağ abonelik sınırları](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-subscription-limits) -sınırları karşı tooview ağ kaynağı kullanımı sağlar.

### <a name="application-insight"></a>Uygulama Insight

[Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) birden çok platformdaki web geliştiricileri için genişletilebilir bir uygulama performansı Yönetimi (APM) hizmetidir. Toomonitor kullanmak canlı web uygulamanızı. Bu performans anormalliklerini otomatik olarak algıla olur. Sorunları ve hangi kullanıcıların gerçekte uygulamanızla yerine toounderstand tanılamak güçlü analytics araçları toohelp içerir.

 Bunun tasarlandığından toohelp sürekli olarak artırmak performans ve kullanılabilirlik.

 Uygulamalar için çalışır platformları .NET, Node.js ve J2EE dahil olmak üzere çeşitli şirket içi barındırılan veya hello bulutta. DevOps işleminizi ile tümleşir ve bağlantı noktaları toovarious geliştirme araçları vardır.

![Uygulama Insight](./media/azure-log-audit/azure-log-audit-fig6.png)

Application Insights hello geliştirme ekibi, uygulamanızı nasıl çalıştığını ve nasıl kullanıldığını anlamak toohelp hedefler. Şunları izler:

-   **İstek oranları, yanıt süreleri ve hata oranları**: Hangi sayfaların günün hangi saatlerinde popüler olduğunu ve kullanıcılarınızın konumunu öğrenin. En iyi performansı hangi sayfaların gösterdiğini görün. Daha fazla istek olduğunda yanıt süreleriniz ve hata oranlarınız yükseliyorsa bir kaynak atama sorununuz olabilir.

-   **Bağımlılık oranları, yanıt süreleri ve hata oranları**: Dış hizmetlerin sizi yavaşlatıp yavaşlatmadığını öğrenin.

-   **Özel durumlar** - hello toplanan istatistikleri çözümlemek veya belirli örnekleri seçin ve hello yığın izleme ve ilgili istekleri ayrıntıya gidin. Hem sunucu hem de tarayıcı özel durumları raporlanır.

-   **Sayfa görüntüleme sayısı ve yükleme performansı**: Kullanıcılarınızın tarayıcıları tarafından gerçekleştirilir.

-   Web sayfalarından **AJAX çağrıları**: Oranlar, yanıt süreleri ve hata oranları.

-   **Kullanıcı ve oturum sayıları**.

-   Windows veya Linux sunucu makinelerinizden CPU, bellek ve ağ kullanımı gibi **performans sayaçları**.

-   Docker veya Azure’dan **konak tanılama**.

-   Uygulamanızdan **tanılama izleme günlükleri**: İzleme olayları ile istekler arasında bağıntı kurmanıza imkan tanır.

-   **Özel olayları ve ölçümleri** öğeleri satılan veya oyunları kazanılan gibi kendiniz hello istemci veya sunucu kodunda tootrack iş olaylarını yazma.

**Tümleştirme senaryolarına ve açıklama listesi:**

| Tümleştirme senaryolarına | Açıklama |
| --------------------- | :---------- |
|[Uygulama eşlemesi](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-app-map)|anahtar ölçümleri ve Uyarıları ile uygulamanızı Hello bileşenleri.||
|[Tanılama arama örneği için veri](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-diagnostic-search)| İstekler, özel durumlar, bağımlılık çağrıları, günlük izlemeleri ve sayfa görüntülemeleri gibi olaylarda arama yapın ve bunları filtreleyin.||
|[Toplanan veriler için ölçüm Gezgini](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-metrics-explorer)|İstek, hata ve özel durum oranları; yanıt süreleri, sayfa yükleme süreleri gibi toplu verileri keşfedin, filtreleyin ve bölümlere ayırın.||
|[Panolar](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-dashboards#dashboards)|Birden çok kaynaktan toplanan verileri birleştirin ve başkalarıyla paylaşın. Birden çok bileşen uygulamaları için ve hello takım odasında sürekli görüntülenmesi için harika.||
|[Canlı ölçümleri akış](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-live-stream)|Yeni bir yapı dağıttığınızda, bu her şeyin beklendiği gibi çalıştığından emin yakın gerçek zamanlı performans göstergeleri toomake izleyin.||
|[Analizler](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics)|Bu güçlü sorgulama dilini kullanarak uygulamanızın performansı ve kullanımıyla ilgili zor soruları yanıtlayın.||
|[Otomatik ve el ile uyarıları](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-alerts)|Otomatik uyarı olduğunda hello normal düzeni dışında bir şey tooyour uygulamanın normal desenleri telemetri ve tetikleyici uyarlayın. Belirli özel veya standart ölçüm düzeylerinde de uyarılar ayarlayabilirsiniz.||
|[Visual Studio](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-visual-studio)|Performans veri hello kod konusuna bakın. Toocode Yığın izlemeleri gidin.||
|[Power BI](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-power-bi)|Kullanım ölçümlerini diğer iş zekası verileriyle tümleştirin.||
|[REST API](https://dev.applicationinsights.io/)|Kod ölçümleri ve ham verileri üzerinden toorun sorgular yazarsınız.||
|[Sürekli dışarı aktarma](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-telemetry)|Bunu geldiğinde ham verileri toostorage toplu verme.||

### <a name="azure-security-center-alerts"></a>Azure Güvenlik Merkezi uyarıları
[Azure Güvenlik Merkezi](https://docs.microsoft.com/azure/security-center/security-center-intro) otomatik olarak toplar, çözümler ve Azure kaynakları, hello ağ ve güvenlik duvarı ve endpoint protection çözümleri gibi toodetect gerçek tehditleri bağlı iş ortağı çözümlerinden günlük verilerini tümleşir ve azaltır hatalı pozitif sonuç. Öncelikli güvenlik uyarıları listesi hello birlikte Güvenlik Merkezi'nde gösterilen tooquickly gereksinim duyduğunuz bilgileri araştırın hello sorun ve nasıl için öneriler tooremediate saldırının.

Güvenlik Merkezi tehdit algılaması Azure kaynaklarını, hello ağ ve bağlı iş ortağı çözümlerinden güvenlik bilgileri otomatik olarak toplayarak çalışır. Genellikle birden fazla kaynaktan tooidentify tehditleri bilgileri ilişkilendirerek, bu bilgileri çözümler. Güvenlik uyarıları nasıl tooremediate hello tehdit ilişkin öneriler birlikte Güvenlik Merkezi'nde önceliklendirilir.

![Azure Güvenlik Merkezi](./media/azure-log-audit/azure-log-audit-fig7.png)

Güvenlik Merkezi, imza tabanlı yaklaşımların ötesine geçen gelişmiş güvenlik analizleri kullanır. Büyük veri sıçramalar ve [makine öğrenme](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) teknolojilerdir uygulanan tooevaluate olayları elle yaklaşımlar kullanılarak ve hello tahmin etmeye imkansız tooidentify olacak tehditler hello tüm bulut yapısındaki – saldırıları evrimi. Bu güvenlik analizleri şunlardır:

-   **Tümleşik tehdit bilgileri:** görünüyor genel tehdit bilgileri Microsoft ürünleri ve Hizmetleri, uygulama tarafından bilinen kötü aktörleri hello için Microsoft dijital Suçlar birimi (DCU), hello Microsoft Güvenlik Yanıt Merkezi (MSRC) ve dış akışları.

-   **Davranış analizi:** bilinen desenleri toodiscover kötü amaçlı davranış uygulanır.

-   **Anomali algılama:** toobuild geçmiş taban çizgisi profil istatistiksel kullanır. Tooa olası saldırı vektörüne uygun olan yerleşik taban çizgilerinden sapmalar konusunda uyarır.


Birçok güvenlik işlemleri ve olay yanıtı takımlar başlangıç noktası önceliklendirmek ve güvenlik uyarıları İnceleme için hello olarak bir güvenlik bilgileri ve Olay yönetimi (SIEM) çözümünü kullanır. Azure günlük Tümleştirmesi ile müşteriler Güvenlik Merkezi uyarılarını ve sanal makine güvenlik olayları, kullanıcıların günlük analizi ya da yakın gerçek zamanlı SIEM çözümünden birlikte Azure tanılama ve Azure denetim günlükleri tarafından toplanan eşitleyebilirsiniz.


## <a name="log-analytics"></a>Log Analytics

Günlük analizi olan bir hizmet olarak [Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) toplamak ve bulut kaynakları tarafından oluşturulan verileri çözümlemek yardımcı olur ve şirket içi ortamları. Tümleşik arama özelliğini kullanarak gerçek zamanlı bilgiler verir ve özel panolar tooreadily tüm iş yükleri ve fiziksel konumlarından sunucular arasında milyonlarca kayıt çözümleyin.

![Log Analytics](./media/azure-log-audit/azure-log-audit-fig8.png)

Merhaba günlük analizi merkezi hello Azure bulut barındırılan hello OMS depo ' dir. Verileri hello depoya yapılandırma veri kaynakları ve ekleme çözümleri tooyour abonelik tarafından bağlı kaynaklardan toplanır. Veri kaynakları ve çözümleri her kendi özellikleri vardır, ancak hala birlikte sorguları toohello deposunda analiz farklı kayıt türleri oluşturur. Bu, farklı veri türleri ile aynı araçları ve yöntemleri toowork farklı bir kaynak tarafından toplanan toouse hello sağlar.

Bağlı kaynakları hello bilgisayarları ve günlük analizi tarafından toplanan verileri üreten diğer kaynakları ' dir. Bu, yüklü aracıları içerebilir [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) ve [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents) doğrudan bağlanan bilgisayarlar veya aracıları [bağlı bir System Center Operations Manager yönetim grubu.](https://docs.microsoft.com/azure/log-analytics/log-analytics-om-agents) Günlük analizi de verileri toplamak [Azure depolama.](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage)

[Veri kaynakları](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources) hello farklı bağlı her kaynaktan toplanan veri türleridir. Bu olaylar içerir ve [performans verileri](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-performance-counters) gelen [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events) ve Linux aracıları gibi ek toosources [IIS günlüklerini](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs), ve [özel metin günlükleri.](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-custom-logs) Toocollect istediğiniz ve otomatik olarak teslim tooeach bağlı kaynak hello yapılandırmadır her veri kaynağı yapılandırın.

Dört farklı yolu vardır [günlüklerini ve Azure Hizmetleri için ölçümleri toplama:](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage)
1.  Azure tanılama doğrudan tooLog Analytics (aşağıdaki tablonun hello tanılamada)

2.  Azure tanılama tooAzure depolama tooLog Analytics (depolama hello aşağıdaki tablonun içinde)

3.  Azure Hizmetleri (aşağıdaki tablonun hello bağlayıcılarını) bağlayıcıları

4.  Günlük analizi (boşlukları aşağıdaki tablonun hello ve için listelenmeyen Hizmetleri) içine toocollect ve gönderme verisi komutlar

| Hizmet | Kaynak Türü | Günlükler | Ölçümler | Çözüm |
| :------ | :------------ | :--- | :------ | :------- |
|Uygulama ağ geçitleri|  Microsoft.Network/<br>applicationGateways|  Tanılama|Tanılama|    [Azure uygulama](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-application-gateway-analytics-solution-in-log-analytics) [ağ geçidi analizi](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-application-gateway-analytics-solution-in-log-analytics)|
|Application ınsights||     Bağlayıcı|  Bağlayıcı|  [Application Insights](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/) [Bağlayıcısı (Önizleme)](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/)|
|Automation hesapları|   Microsoft.Automation/<br>AutomationAccounts|    Tanılama||       [Daha fazla bilgi](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics)|
|Toplu hesaplar|    Microsoft.Batch/<br>batchAccounts|  Tanılama|    Tanılama||
|Klasik bulut Hizmetleri||       Depolama||       [Daha fazla bilgi](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage-iis-table)|
|Bilişsel Hizmetler|    Microsoft.CognitiveServices/<br>accounts|       Tanılama|||
|Data Lake analizi|   Microsoft.DataLakeAnalytics/<br>accounts|   Tanılama|||
|Veri Gölü deposu|   Microsoft.DataLakeStore/<br>accounts|   Tanılama|||
|Olay Hub'ad alanı|   Microsoft.EventHub/<br>ad alanları|  Tanılama|    Tanılama||
|IOT hub'ları|  Microsoft.Devices/<br>IotHubs||     Tanılama||
|Anahtar Kasası| Microsoft.KeyVault/<br>kasaları|  Tanılama  || [KeyVault analizi](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-key-vault)|
|Yük Dengeleyici|    Microsoft.Network/<br>loadBalancers|    Tanılama|||
|Logic Apps|    Microsoft.Logic/<br>İş akışları|  Tanılama|    Tanılama||
||Microsoft.Logic/<br>integrationAccounts||||
|Ağ Güvenlik Grupları|   Microsoft.Network/<br>networksecuritygroups|Tanılama||   [Azure ağ güvenlik grubu analizi](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-network-security-group-analytics-solution-in-log-analytics)|
|Kurtarma kasaları|   Microsoft.RecoveryServices/<br>kasaları|||[Analytics (Önizleme) Azure kurtarma Hizmetleri](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
|Hizmet ara|   Microsoft.Search/<br>searchServices|    Tanılama|    Tanılama||
|Hizmet veri yolu ad alanı| Microsoft.ServiceBus/<br>ad alanları|    Tanılama|Tanılama|    [Hizmet veri yolu Analytics (Önizleme)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
|Service Fabric||       Depolama||    [Service Fabric Analytics (Önizleme)](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-service-fabric)|
|SQL (v12)| Microsoft.Sql/<br>sunucuları /<br>veritabanları||       Tanılama||
||Microsoft.Sql/<br>sunucuları /<br>elasticPools||||
|Depolama|||         Betik| [Azure depolama çözümlemeleri (Önizleme)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution)|
|Virtual Machines|  Microsoft.Compute/<br>virtualMachines|  Dahili numara|  Dahili numara||
||||Tanılama||
|Sanal makine ölçek kümeleri|   Microsoft.Compute/<br>virtualMachines    ||Tanılama||
||Microsoft.Compute/<br>virtualMachineScaleSets /<br>virtualMachines||||
|Web sunucu grupları|Microsoft.Web/<br>ServerFarm öğesine verilir||   Tanılama
|Web Siteleri| Microsoft.Web/<br>siteleri ||      Tanılama|    [Daha fazla bilgi](https://github.com/Azure/azure-quickstart-templates/tree/master/101-webappazure-oms-monitoring)|
||Microsoft.Web/<br>siteleri /<br>yuvaları|||||


## <a name="log-integration-with-on-premises-siem-systems"></a>Şirket içi SIEM sistemleriyle günlük tümleştirme
[Azure günlük tümleştirme](https://www.microsoft.com/download/details.aspx?id=53324) toointegrate ham Azure kaynaklarınızı tooyour şirket içi günlüklerinden etkinleştirir **güvenlik bilgileri ve Olay yönetimi (SIEM) sistemleri**.

![Günlük tümleştirme](./media/azure-log-audit/azure-log-audit-fig9.png)

Azure günlük tümleştirme Azure Tanılama'yı, Windows (WAD) sanal makinelerden, Azure etkinlik günlükleri, Azure Güvenlik Merkezi uyarılarını toplar ve Azure kaynak sağlayıcısı günlüğe kaydeder. Toplama, bağıntılı, çözümlemek ve güvenlik olayları için uyarı böylece bu tümleştirme tüm varlıklarınızı, şirket içi veya hello bulutta birleştirilmiş bir Pano sağlar.



Azure Güvenlik Merkezi uyarılarını, Azure tanılama günlüklerini ve Azure Active Directory denetim günlükleri, Azure günlük tümleştirme şu anda Azure etkinlik günlükleri, Azure aboneliğinizde Windows sanal makine Windows olay günlüğünden tümleştirilmesi destekler.

| Günlük türü | Günlük analizi JSON (Splunk, ArcSight, Qradar) destekleme |
| :------- | :-------------------------------------------------------- |
|AAD denetim günlükleri|    Evet|
|Etkinlik Günlükleri| Evet|
|ASC uyarıları |Evet|
|Tanılama günlükleri (kaynak günlükleri)|  Evet|
|VM günlükleri|   İletilen olaylar aracılığıyla ve JSON üzerinden değil Evet|


Merhaba aşağıdaki tabloda hello günlük kategori ve SIEM tümleştirme ayrıntı açıklanmaktadır.

[Azure günlük tümleştirme ile çalışmaya başlama](https://docs.microsoft.com/azure/security/security-azure-log-integration-get-started) - öğretici Azure günlük tümleştirme yükleme anlatılmaktadır ve Azure WAD depolama günlüklerinden tümleştirme, Azure etkinlik günlükleri, Azure Güvenlik Merkezi uyarılarını ve Azure Active Directory denetim günlükleri.

Tümleştirme senaryolarına

-   [Ortak yapılandırma adımları](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – bu blog gönderisine nasıl tooconfigure Azure oturum tümleştirme toowork Splunk, HP ArcSight ve IBM QRadar ile iş ortağı çözümlerini gösterir.

-   [Azure günlük sık sorulan sorular (SSS) tümleştirme](https://docs.microsoft.com/azure/security/security-azure-log-integration-faq) -bu SSS Azure günlük tümleştirmesi hakkında sorular yanıtlanmaktadır.

-   [Güvenlik Merkezi tümleştirme uyarıları Azure ile tümleştirme oturum](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration) – bu belgeyi nasıl toosync Güvenlik Merkezi, sanal makine güvenlik olayları, günlük analizi ile Azure tanılama ve Azure denetim günlükleri tarafından toplanan birlikte uyarıları gösterir veya SIEM çözümü.

## <a name="next-steps"></a>Sonraki Adımlar

- [Denetme ve günlüğe kaydetme](https://www.microsoft.com/trustcenter/security/auditingandlogging)

Görünürlüğü koruma ve hızlı bir şekilde tootimely güvenlik uyarıları yanıt veri koruma

- [Güvenlik günlüğü ve Azure içindeki denetim günlük toplama](https://azure.microsoft.com/resources/videos/security-logging-and-audit-log-collection/)

Doğru güvenlik tooenforce toomake Azure örneklerinizi toplama emin ihtiyacınız hangi ayarların hello ve denetim günlüklerini.

- [Bir site koleksiyonu denetim ayarlarını yapılandır](https://support.office.com/article/Configure-audit-settings-for-a-site-collection-A9920C97-38C0-44F2-8BCB-4CF1E2AE22D2?ui=&rs=&ad=US)

Bir site koleksiyonu yöneticisi olarak biri belirli bir kullanıcı tarafından gerçekleştirilen eylemlerin hello geçmişi alabilir ve belirli bir tarih aralığı içinde yapılan Eylemler hello geçmişini de alabilirsiniz. 

- [Arama hello denetim günlüğü hello Office 365 güvenlik ve Uyumluluk Merkezi](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=&rs=&ad=US)

Office 365 kuruluşunuza hello Office 365 güvenlik ve Uyumluluk Merkezi toosearch hello birleşik denetim günlüğü tooview kullanıcı ve yönetici etkinliğini kullanabilirsiniz.


