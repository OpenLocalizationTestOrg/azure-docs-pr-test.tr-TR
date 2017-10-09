---
title: "aaaIntroduction tooAzure güvenlik | Microsoft Docs"
description: "Azure güvenlik, hizmetlerinin ve nasıl çalıştığı hakkında bilgi edinin."
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
ms.date: 05/03/2017
ms.author: TomSh
ms.openlocfilehash: 2d42057e9586a0b6ce16a1582db3b3af842297af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security"></a>Giriş tooAzure güvenlik
## <a name="overview"></a>Genel Bakış
Güvenlik hello bulutta iş ve nasıl önemli Azure güvenliği hakkında doğru ve güncel bilgi bulma olduğunu olduğunu biliyoruz. Merhaba en iyi uygulamalar ve hizmetler için nedenleri toouse Azure, çeşitli güvenlik araçları ve yetenekleri tootake avantajlarından biri. Bu araçları ve yetenekleri, olası toocreate güvenli çözümleri hello güvenli Azure platformu yardımcı olur. Microsoft Azure gizlilik, bütünlük ve müşteri verilerini, kullanılabilirliğini de saydam sorumluluk etkinleştirirken sağlar.

Merhaba Müşteri'nin ve Microsoft operations perspektiften, bu teknik incelemede "Güvenlik giriş tooAzure" Microsoft Azure içinde uygulanan güvenlik denetimleri hello koleksiyonunu daha iyi anlamak toohelp tooprovide yazılmış bir Microsoft Azure ile kullanılabilir hello güvenlik kapsamlı bakın.

### <a name="azure-platform"></a>Azure platformu
Azure işletim sistemleri, programlama dilleri, çerçeveleri, Araçlar, veritabanları ve aygıtları geniş çapta destekleyen bir genel bulut hizmeti platformudur. Docker Tümleştirmesi ile Linux kapsayıcıları çalıştırabilirsiniz; JavaScript, Python, .NET, PHP, Java ve Node.js ile uygulamalar oluşturma; Yapı geri-iOS, Android ve Windows cihazları sona erer.

Azure genel bulut Hizmetleri, geliştiriciler ve BT uzmanları, aynı teknolojileri milyonlarca zaten kullanır ve güven hello destekler. Derleme ya da BT varlıklarına geçirmek hello Hizmetleri ve hello denetimleri ile veri ve uygulamaları, bir kuruluşun yeteneklerini tooprotect üzerinde bağlı bir genel bulut hizmeti sağlayıcısı, bulut tabanlı toomanage hello güvenliğini sağlarlar varlıklar.

Azure'nın altyapısını aynı anda milyonlarca müşteri barındırmak için tesis tooapplications gelen tasarlanmıştır ve güvenlik gereksinimlerine bağlı işletmeler karşılayabilecek güvenilir bir temel sağlar.

Ayrıca, Azure, çok çeşitli yapılandırılabilir güvenlik seçenekleri ve hello özelliği toocontrol sağlar bunları böylece güvenlik toomeet hello benzersiz gereksinimleri, kuruluşunuzun dağıtımlarının özelleştirebilirsiniz. Bu belge, nasıl Azure güvenliği anlamanıza yardımcı olur. özellikler, bu gereksinimleri karşılamak yardımcı.

> [!Note]
> Bu belgenin birincil odağı Hello müşterilerle denetimlere toocustomize kullanın ve uygulamalar ve hizmetler için güvenliği artırmaya var.
>
> Bazı genel bir bakış sağlar, ancak Azure platformu kendisini nasıl Microsoft hello güvenliğini sağlama hakkında ayrıntılı bilgi için hello sağlanan bilgileri görmek [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/default.aspx).

### <a name="abstract"></a>Özet
Başlangıçta, genel bulut geçişler maliyet tasarrufu ve çeviklik tooinnovate tarafından yönlendirilen. Güvenlik süre ve hatta bir Göster stopper, genel bulut geçiş için başlıca sorunlardan olarak kabul edildi. Ancak, genel bulutun güvenlik sorunu tooone buluta geçiş hello sürücülerini önemli çözümlemeye geçmiş. Bu arkasında Hello stratejinin hello üstün özelliği büyük ortak bulut hizmet sağlayıcılarının tooprotect uygulamaları ve bulut tabanlı varlıklar hello verilerini ' dir.

Azure'nın altyapı hello tesis tooapplications aynı anda milyonlarca müşteri barındırmak için gelen tasarlanmıştır ve güvenlik gereksinimlerine bağlı işletmeler karşılayabilecek güvenilir bir temel sağlar. Ayrıca, Azure, çok çeşitli yapılandırılabilir güvenlik seçenekleri ve hello özelliği toocontrol sağlar bunları güvenlik toomeet hello benzersiz gereksinimlerini dağıtımları toomeet özelleştirebilirsiniz böylece BT denetim ilkeleri ve tooexternal uyması düzenlemeleri.

Bu yazı, Microsoft'un yaklaşımı toosecurity hello Microsoft Azure bulut platformu içinde özetlenmektedir:
* Microsoft toosecure hello Azure altyapı, müşteri verileri ve uygulamalar tarafından uygulanan güvenlik özellikleri.
* Azure Hizmetleri ve güvenlik özellikleri kullanılabilir tooyou toomanage hello hello hizmetlerin ve verilerinizi Azure aboneliklerinin içindeki güvenlik.

## <a name="summary-azure-security-capabilities"></a>Özet Azure güvenlik özellikleri
Merhaba tablo aşağıdaki Microsoft toosecure hello Azure altyapı, müşteri verileri ve güvenli uygulamalar tarafından uygulanan hello güvenlik özelliklerinin kısa bir açıklama sağlayın.
### <a name="security-features-implemented-toosecure-hello-azure-platform"></a>Güvenlik özellikleri uygulanan tooSecure hello Azure platformu:
Aşağıdaki listelenen hello Azure platformu güvenli bir şekilde yönetilir bu hello tooprovide hello güvence gözden geçirebilirsiniz yetenekleri özellikleridir. Bağlantılar için daha fazla Microsoft Müşteri güven soruları dört alanlarda nasıl ele üzerinde ayrıntıya sağlandı: Güvenli Platform, gizlilik ve denetimler, uyumluluk ve saydamlığı.


| [Güvenli Platform](https://www.microsoft.com/en-us/trustcenter/Security/default.aspx)  | [Gizlilik ve denetimleri](https://www.microsoft.com/en-us/trustcenter/Privacy/default.aspx)  |[Uyumluluk](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx)   | [Saydamlık](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx) |
| :-- | :-- | :-- | :-- |
| [Güvenlik geliştirme döngüsü](https://www.microsoft.com/en-us/sdl/), dahili denetimler | [Verilerinizi hello zaman yönetme](https://www.microsoft.com/en-us/trustcenter/Privacy/You-own-your-data) | [Güven Merkezi](https://www.microsoft.com/en-us/trustcenter/default.aspx) |[Microsoft Azure hizmetlerinde müşteri verilerini nasıl korur](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx) |
| [Zorunlu güvenlik Eğitimi, arka plan denetimleri](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiwsOCpganRAhWqxVQKHUdiDsMQFghAMAE&url=https%3A%2F%2Fdownloads.cloudsecurityalliance.org%2Fstar%2Fself-assessment%2FStandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx&usg=AFQjCNEYvBky4zNeDQPN6YJGPFRZA7eeZg&sig2=2kkw1lOCP_kzLzgE9RS2Tg&bvm=bv.142059868,d.amc) |  [Veri konumu denetleme](https://www.microsoft.com/en-us/trustcenter/Privacy/Where-your-data-is-located) |  [Ortak Denetimler Hub](https://www.microsoft.com/en-us/trustcenter/Common-Controls-Hub) |[Microsoft Azure Hizmetleri veri konumda yönetmek hakkında](http://azuredatacentermap.azurewebsites.net/)|
| [Sızma testi](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiwsOCpganRAhWqxVQKHUdiDsMQFghAMAE&url=https%3A%2F%2Fdownloads.cloudsecurityalliance.org%2Fstar%2Fself-assessment%2FStandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx&usg=AFQjCNEYvBky4zNeDQPN6YJGPFRZA7eeZg&sig2=2kkw1lOCP_kzLzgE9RS2Tg&bvm=bv.142059868,d.amc), [izinsiz giriş algılama DDoS](https://www.microsoft.com/en-us/trustcenter/Security/ThreatManagemen), [denetimleri & günlüğe kaydetme](https://www.microsoft.com/en-us/trustcenter/Security/AuditingAndLogging) | [Sizin koşullarınızda veri erişimi sağlar](https://www.microsoft.com/en-us/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms) |  [Merhaba bulut Hizmetleri son Tespitlerini denetim listesi](https://www.microsoft.com/en-us/trustcenter/Compliance/Due-Diligence-Checklist) |[Microsoft, verilerinizi hangi koşullarınızda erişebilecek mi](https://www.microsoft.com/en-us/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms)|
| [Resim datacentre durumu](https://www.microsoft.com/en-us/cloud-platform/global-datacenters), fiziksel güvenlik [güvenli ağ](https://docs.microsoft.com/en-us/azure/security/security-network-overview) | [Yanıt veren toolaw zorlama](https://www.microsoft.com/en-us/trustcenter/Privacy/Responding-to-govt-agency-requests-for-customer-data) |  [Hizmet, konum ve endüstri göre uyumluluk](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx) |[Microsoft Azure hizmetlerinde müşteri verilerini nasıl korur](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx)|
|  [Güvenlik olay yanıtı](http://aka.ms/SecurityResponsepaper), [paylaşılan sorumluluk](http://aka.ms/sharedresponsibility) |[Sıkı gizlilik standartları](https://www.microsoft.com/en-us/TrustCenter/Privacy/We-set-and-adhere-to-stringent-standards) |  | [Sertifika saydamlık hub'ı, Azure Hizmetleri için inceleyin](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx)|



### <a name="security-features-offered-by-azure-toosecure-data-and-application"></a>Güvenlik özellikleri Azure tooSecure veri tarafından sunulan ve uygulama
Merhaba bulut hizmeti modeline bağlı olarak, kimin Merhaba uygulaması veya hizmeti hello güvenliğini yönetilmesinden sorumludur değişken sorumluluğunu yoktur. Size bu Sorumluluklar yerleşik özellikler sayesinde ve aracılığıyla toplantı iş ortağı Azure aboneliğinize dağıtılabilir çözümleri hello Azure platformu tooassist bulunan özellikleri vardır.

Merhaba yerleşik özellikleri altı (6) işlevsel düzenlenir: işlem, uygulamalar, depolama, ağ, hesaplama ve kimlik. Merhaba özellikleri ve yetenekleri hello Azure platformu bu altı (6) alanlarda bulunan ek ayrıntı Özet bilgiler sağlanır.

## <a name="operations"></a>İşlemler
Bu bölüm, güvenlik işlemlerinde temel özellikleri ile ilgili ek bilgiler ve bu özellikler hakkındaki özet bilgileri sağlar.

### <a name="operations-management-suite-security-and-audit-dashboard"></a>Operations Management Suite güvenlik ve Denetim Panosu
Merhaba [OMS güvenlik ve denetim çözümü](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) kuruluşunuzun kapsamlı bir görünüme sağlar BT güvenlik tutumunu ile [yerleşik arama sorguları](https://blogs.technet.microsoft.com/msoms/2016/01/21/easy-microsoft-operations-management-suite-search-queries/) dikkat etmeniz gereken önemli sorunlar için. Merhaba [güvenlik ve Denetim](https://technet.microsoft.com/library/mt484091.aspx) Pano olan her şeyi hello giriş ekranı ilgili OMS toosecurity. Merhaba bilgisayarlarınızı güvenlik durumunu üst düzey bir anlayış sağlar. Son 24 saat, 7 gün hello tüm olayları veya diğer özel zaman çerçevesi ayrıca hello özelliği tooview içerir.

Ayrıca, OMS güvenlik ve uyumluluk çok yapılandırabilirsiniz[otomatik olarak belirli eylemleri gerçekleştirme](https://blogs.technet.microsoft.com/robdavies/2016/04/20/simple-look-at-oms-alert-remediation-with-runbooks-part-1/) zaman belirli bir olay algılandı.

### <a name="azure-resource-manager"></a>Azure Resource Manager
[Azure Resource Manager ](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model) hello kaynaklarla bir grup olarak çözümünüzdeki toowork sağlar. Dağıtma, güncelleştirme veya tek ve eşgüdümlü bir işlemle, çözümünüz için tüm hello kaynakları silin. Kullandığınız bir [Azure Resource Manager şablonu](https://blogs.technet.microsoft.com/canitpro/2015/06/29/devops-basics-infrastructure-as-code-arm-templates/) için dağıtım ve bu şablon test, hazırlama ve üretim gibi farklı ortamları için çalışabilir. Resource Manager Güvenlik denetimi sağlar ve özellikleri toohelp etiketleme, kaynaklarınızın dağıtımdan sonra yönetin.

Azure Resource Manager şablonu tabanlı dağıtımlar çözümlerinin standart güvenlik ayarlarını denetleme ve Azure üzerinde dağıtılan hello güvenlik artırılmasına yardımcı tümleşik standartlaştırılmış şablon tabanlı dağıtımlar. Bu dağıtımlar sırasında gerçekleşmesi güvenlik yapılandırma hataları hello riskini azaltır.

### <a name="application-insights"></a>Application Insights
[Application Insights](https://docs.microsoft.com/azure/application-insights/) web geliştiricileri için genişletilebilir bir uygulama performansı Yönetimi (APM) hizmetidir. Application Insights ile canlı web uygulamalarınızı izleyin ve performans anormalliklerini otomatik olarak algıla. Sorunları ve hangi kullanıcıların gerçekte uygulamalarınızı ile yerine toounderstand tanılamak güçlü analytics araçları toohelp içerir. Uygulamanız, test sırasında hem yayımlanan veya dağıtılmış sonra çalıştığı tüm hello saat izler.

Application Insights grafikler ve gösteren tablolar oluşturur, örneğin, çoğu kullanıcı alma günün ne zaman esnek hello uygulaması nasıl ve iyi bir dış tarafından sunulan hizmetler nasıl bağlıdır.

Kilitlenmeler, hatalar veya performans sorunları varsa, ayrıntı toodiagnose hello neden hello telemetri verilerini aracılığıyla arama yapabilirsiniz. Ve hello hizmeti hello kullanılabilirlik ve performans, uygulamanızın herhangi bir değişiklik varsa e-posta gönderir. Merhaba gizlilik, bütünlük ve kullanılabilirlik güvenlik Üçlü hello kullanılabilirlik ile yardımcı olması uygulama Insight böylece değerli güvenlik aracı haline gelir.

### <a name="azure-monitor"></a>Azure İzleyici
[Azure İzleyici](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) görselleştirme, sorgu, yönlendirme, uyarı, otomatik ölçeklendirme ve Otomasyon verileri hem Azure altyapısı hello sunar ([etkinlik günlüğü](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)) ve tek tek her Azure kaynak ([ Tanılama günlüklerini](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)). Azure İzleyici tooalert kullanabilirsiniz, güvenlikle ilgili olayları, Azure günlükleri oluşturulur.

### <a name="log-analytics"></a>Log Analytics
[Günlük analizi](https://azure.microsoft.com/documentation/services/log-analytics/) parçası [Operations Management Suite](https://www.microsoft.com/cloud-platform/operations-management-suite) – BT yönetim çözümünü şirket içi ve üçüncü taraf bulut tabanlı altyapı (AWS gibi) ek olarak tooAzure kaynaklar sağlar. Verileri Azure İzleyicisi'nden yönlendirilir doğrudan tooLog ölçümleri ve günlükleri görebilmeniz için tüm ortamınız tek bir yerde Analytics.

Günlük analizi Hello aracı tooquickly arama ile ilgili girdileri esnek sorgu yaklaşımı büyük miktarlarda aracılığıyla sağlar adli de yararlı bir araç ve diğer güvenlik analizi olabilir. Ayrıca, şirket içi [güvenlik duvarı ve proxy günlüklerini Azure'a dışarı ve günlük analizi kullanarak analiz için kullanılabilir.](https://docs.microsoft.com/azure/log-analytics/log-analytics-proxy-firewall)

### <a name="azure-advisor"></a>Azure Advisor
[Azure Danışmanı](https://docs.microsoft.com/azure/advisor/) toooptimize yardımcı olan bir kişiselleştirilmiş bulut Danışman Azure dağıtımlarınızı olduğu. Kaynak yapılandırmanızı ve kullanım telemetrinizi çözümler. Ardından bir çözüm önerir toohelp artırmak hello [performans](https://docs.microsoft.com/azure/advisor/advisor-performance-recommendations), [güvenlik](https://docs.microsoft.com/azure/advisor/advisor-security-recommendations), ve [yüksek kullanılabilirlik](https://docs.microsoft.com/azure/advisor/advisor-high-availability-recommendations) olanaklarını çok arama sırasında kaynaklarınızın[genel Azure azaltmak harcamanız](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations). Azure Danışmanı güvenlik önerileri, geliştirme, genel güvenlik duruşunu Azure'da dağıtmak çözümleri için önemli hangi yollarını sağlar. Bu öneriler tarafından gerçekleştirilen güvenlik analizi gelen çizilir [Azure Güvenlik Merkezi.](https://docs.microsoft.com/azure/security-center/security-center-intro)

### <a name="azure-security-center"></a>Azure Güvenlik Merkezi
[Azure Güvenlik Merkezi](https://docs.microsoft.com/azure/security-center/security-center-intro) hello Azure kaynaklarınızın güvenlik engellemek, algılamak, artırılmış görünürlük aracılığı ile toothreats yanıt ve üzerinden denetlemesine yardımcı olur. Aboneliklerinizde, tümleşik güvenlik izleme ve ilke yönetimi sağlar; normal koşullarda gözden kaçabilecek tehditleri algılamaya yardımcı olur ve güvenlik çözümlerinin geniş ekosistemiyle çalışır.

Ayrıca, Azure Güvenlik Merkezi güvenlik işlemleri ile tek bir panoya sağlayarak bu yüzeyleri uyarıları ve sonra hemen işlem yapılması öneriler yardımcı olur. Genellikle, tek bir tıklatmayla hello Azure Güvenlik Merkezi Konsolu içinden sorunları düzeltebilir.
## <a name="applications"></a>Uygulamalar
Merhaba bölüm uygulama güvenlik ve Özet bilgilerini bu özellikleri hakkında temel özellikleri ile ilgili ek bilgiler sağlar.

### <a name="web-application-vulnerability-scanning"></a>Web uygulaması güvenlik açığı taraması
Merhaba en kolay yolu tooget birini kullanmaya güvenlik açıkları için testi ile [App Service uygulaması](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is) toouse hello olan [Tinfoil Security ile tümleştirme](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) tooperform tek tıklatmayla güvenlik açığı üzerinde tarama Uygulamanızı. Kolay anlaşılır bir raporda hello test sonuçlarını görüntülemek ve bilgi nasıl toofix her bir güvenlik açığı hakkında adım adım yönergeler.

### <a name="penetration-testing"></a>Sızma Testi
Tooperform tercih ederseniz, kendi sızma testleri veya başka bir tarayıcı paketi ya da sağlayıcı toouse istediğiniz, hello izlemelisiniz [onay işlemini test Azure sızma](https://security-forms.azure.com/penetration-testing/terms) ve önceki onay tooperform istenen hello sızma edinme test eder.

### <a name="web-application-firewall"></a>Web uygulaması güvenlik duvarı
Web uygulaması Güvenlik Duvarı (WAF) içinde hello [Azure uygulama ağ geçidi](https://azure.microsoft.com/services/application-gateway/) SQL ekleme gibi ortak web tabanlı saldırıları, siteler arası komut dosyası saldırıları ve oturumu ele geçirme web uygulamalarını korumaya yardımcı olur. Bunu hello tarafından tanımlanan tehditlere karşı koruma ile önceden yapılandırılmış olarak gelir [açık Web uygulaması güvenlik proje (OWASP) hello olarak ilk 10 Ortak Güvenlik Açıkları](https://msdn.microsoft.com/library/).

### <a name="authentication-and-authorization-in-azure-app-service"></a>Azure Uygulama Hizmeti’nde kimlik doğrulaması ve yetkilendirme
[App Service kimlik doğrulama / yetkilendirme](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) , uygulama toosign kullanıcılar için bir yol sağlar ve böylece hello uygulama arka uçta toochange koduna sahip değilseniz bir özelliktir. Bir kolay bir yolu tooprotect, uygulama ve iş ile kullanıcı başına veri sağlar.

### <a name="layered-security-architecture"></a>Katmanlı güvenlik mimarisi
Bu yana [App Service ortamları](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-intro) içine dağıtılan bir yalıtılmış çalışma zamanı ortamı sağlamak bir [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview), geliştiriciler, her uygulama katmanı için ağ erişim düzeyleri farklı sağlayan bir katmanlı güvenlik mimarisi oluşturabilirsiniz. Ortak desire toohide API'si arka uçları genel Internet erişimine karşı olduğu ve yalnızca Yukarı Akış web uygulamaları tarafından adlı API'leri toobe sağlar. [Ağ güvenlik grubu (Nsg'ler)](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/) App Service ortamları toorestrict genel erişim tooAPI uygulamaları içeren Azure sanal ağ alt ağları üzerinde kullanılabilir.

### <a name="web-server-diagnostics-and-application-diagnostics"></a>Web sunucusu tanılama ve uygulama tanılama
App Service web apps hello web sunucusu ve hello web uygulamasının içinden bilgileri günlüğe kaydetme için tanılama işlevsellik sağlar. Bu mantıksal olarak ayrılmış [web sunucusu tanılama](https://docs.microsoft.com/azure/app-service-web/web-sites-enable-diagnostic-log) ve [uygulama tanılama](https://technet.microsoft.com/library/hh530058(v=sc.12).aspx). Web sunucusu iki önemli gelişmeler tanılama ve sorun giderme siteleri ve uygulamaları içerir.

Merhaba ilk yeni uygulama havuzları, çalışan işlem, site, uygulama etki alanları ve çalışan istekleri gerçek zamanlı durum bilgilerini özelliğidir. Merhaba ikinci yeni avantajları hello hello tam istek ve yanıt işlemi boyunca bir isteğin izlenmesi ayrıntılı izleme olayları.

Bu izleme olaylarını tooenable hello koleksiyonu, IIS 7 yapılandırılmış tooautomatically yakalama tam izleme günlükleri, geçen süre veya hata yanıtı kodlarına dayalı herhangi belirli bir istek için XML biçiminde olabilir.

#### <a name="web-server-diagnostics"></a>Web sunucu tanıları
Etkinleştirmek veya tür günlüğe aşağıdaki hello devre dışı bırakabilirsiniz:

-   Hata günlüğü - ayrıntılı ayrıntılı hata bilgileri (durum kodu 400 veya daha büyük) hatası olduğunu gösteren HTTP durum kodları için. Bu neden hello sunucu hello hata kodunu döndürdü belirlemenize yardımcı olabilecek bilgiler içerebilir.

-   Başarısız istek izleme - ayrıntılı izleme hello IIS kullanılan bileşenler tooprocess hello isteği ve her bileşenin geçen hello süre dahil olmak üzere, başarısız istekler hakkında bilgi. Döndürülen belirli bir HTTP hata toobe neden olan ayırmak veya tooincrease site performansını çalışıyorsunuz, bu yararlı olabilir.

-   Web sunucu günlüğü - hello W3C Genişletilmiş günlük dosyası biçimini kullanarak HTTP işlemler hakkında bilgi. Bu, işlenen istek hello sayısı gibi genel site ölçümleri veya belirli bir IP adresinden kaç isteklerdir belirlerken yararlıdır.

#### <a name="application-diagnostics"></a>Uygulama tanılama
[Uygulama tanılama](https://docs.microsoft.com/azure/app-service-web/web-sites-enable-diagnostic-log) bir web uygulaması tarafından üretilen toocapture bilgileri sağlar. ASP.NET uygulamaları hello kullanabileceğiniz [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) sınıfı toolog bilgi toohello uygulama tanılama günlük. Uygulama Tanılama, başlıca iki türde olay vardır ve bu tooapplication performans ile ilgili olanlar tooapplication arızaları ve hataları ile ilgili. Merhaba arızaları ve hataları ayrılabilir bağlantı, güvenlik ve arıza sorunları daha. Hata, genellikle ilgili tooa hello uygulama kodu sorun sorunlardır.

Uygulama tanılamada, bu şekilde gruplandırılmış olayları görebilirsiniz:

-   Tümü (tüm olayları görüntüler)
-   Uygulama hataları (özel durumları görüntüler)
-   Performans (performans olaylarını görüntüler)

## <a name="storage"></a>Depolama
Merhaba bölümünde Azure depolama güvenlik ve Özet bilgilerini bu özellikleri hakkında temel özellikleri ile ilgili ek bilgiler sağlar.

### <a name="role-based-access-control-rbac"></a>Rol Tabanlı Erişim Denetimi (RBAC)
Rol tabanlı erişim denetimi (RBAC) ile depolama hesabınızın güvenliğini sağlayabilirsiniz. Erişimi kısıtlama tabanlı hello üzerinde [tooknow gerek](https://en.wikipedia.org/wiki/Need_to_know) ve [en az ayrıcalık](https://en.wikipedia.org/wiki/Principle_of_least_privilege) güvenlik ilkeleri kesinlik temelli tooenforce güvenlik ilkeleri veri erişimi için istediğiniz kuruluşlar için. Bu erişim haklarını hello uygun RBAC rolü toogroups ve belirli bir kapsamda uygulamaları atayarak verilir. Kullanabileceğiniz [yerleşik RBAC rolleri](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles), depolama hesabı katkıda bulunanlar gibi tooassign toousers ayrıcalıkları. Erişim toohello depolama anahtarları hello kullanarak bir depolama hesabı için [Azure Resource Manager](https://docs.microsoft.com/azure/storage/storage-security-guide) modeli rol tabanlı erişim denetimi (RBAC) denetlenebilir.

### <a name="shared-access-signature"></a>Paylaşılan erişim imzası
A [paylaşılan erişim imzası (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) depolama hesabınızda atanmış erişim tooresources sağlar. Merhaba SAS anlamına gelir, bir istemci belirli bir süre için ve belirtilen bir izin kümesi ile depolama hesabınızdaki izinleri tooobjects sınırlı verebilirsiniz. Hesap erişim tuşlarınızı tooshare gerek kalmadan bu sınırlı izinleri verebilirsiniz.

### <a name="encryption-in-transit"></a>Aktarımdaki şifreleme
Şifreleme Aktarımdaki ağlar üzerinden iletilirken veri koruma, bir mekanizmadır. Azure Storage ile verileri kullanarak güvenliğini sağlayabilirsiniz:
-   [Aktarım düzeyinde şifreleme](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-in-transit), içine veya dışına Azure Storage veri aktarırken HTTPS gibi.

-   [Şifreleme wire](https://docs.microsoft.com/azure/storage/storage-security-guide#using-encryption-during-transit-with-azure-file-shares), gibi [SMB 3.0 şifrelemesi](https://docs.microsoft.com/azure/storage/storage-security-guide) için [Azure dosya paylaşımları](https://docs.microsoft.com/azure/storage/storage-dotnet-how-to-use-files).

-   İstemci tarafı şifreleme, depolama alanına transfer önce tooencrypt hello veri ve depolama alanı biterse aktarıldıktan sonra toodecrypt hello verileri.

### <a name="encryption-at-rest"></a>Bekleme sırasında şifreleme
Çoğu kuruluş için bekleyen verileri şifreleme veri gizliliği, uyumluluk ve veri egemenliği doğru zorunlu bir adımdır. "Bekleyen" olan verilerin şifrelenmesini sağlayan üç Azure depolama güvenlik özellikleri şunlardır:

-   [Depolama hizmeti şifrelemesi](https://docs.microsoft.com/azure/storage/storage-service-encryption) toorequest hello depolama hizmeti otomatik olarak veri tooAzure depolama yazılırken şifrelemenizi sağlar.

-   [İstemci tarafı şifreleme](https://docs.microsoft.com/azure/storage/storage-client-side-encryption) bekleyen şifreleme hello özelliği de sağlar.

-   [Azure Disk şifrelemesi](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) tooencrypt hello işletim sistemi ve bir Iaas sanal makine tarafından kullanılan veri disklerle sağlar.

### <a name="storage-analytics"></a>Depolama Analizi
[Azure Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) günlüğe kaydetme işlemlerini gerçekleştiren ve ölçümler veriler için bir depolama hesabı sağlar. Bu veri tootrace istekleri kullanır, kullanım eğilimleri çözümlemek ve depolama hesabınızla sorunlarını tanılamak. Storage Analytics başarılı ve başarısız istekleri tooa depolama birimi hizmeti hakkındaki ayrıntılı bilgileri kaydeder. Bu bilgiler kullanılan toomonitor istekleri ayrı ayrı ve depolama hizmeti toodiagnose sorunları olabilir. İstekleri en iyi çaba ilkesine göre günlüğe kaydedilir. Kimliği doğrulanmış istekler türleri aşağıdaki hello kaydedilir:
-   Başarılı istek sayısı.

-   İstek zaman aşımı, azaltma, ağ, yetkilendirme ve başka hatalar da dahil olmak üzere, başarısız oldu.

-   Başarılı ve başarısız istekleri dahil olmak üzere paylaşılan erişim imzası (SAS), kullanarak istek sayısı.

-   İstekleri tooanalytics verileri.

### <a name="enabling-browser-based-clients-using-cors"></a>Tarayıcı tabanlı istemcileri CORS kullanarak etkinleştirme
[Çıkış noktaları arası kaynak paylaşımı (CORS)](https://docs.microsoft.com/rest/api/storageservices/fileservices/cross-origin-resource-sharing--cors--support-for-the-azure-storage-services) etki alanları toogive birbirine sağlayan bir mekanizmadır birbirlerinin kaynaklarına erişim izni. Merhaba kullanıcı aracısı hello JavaScript kodu belirli bir etki alanından yüklü başka bir etki alanında bulunan tooaccess kaynakları izin fazladan üstbilgiler tooensure gönderir. Hello ikinci etki alanı sonra izin verme veya tooits kaynakları hello özgün etki alanı erişimi engelleme ek üst bilgilerle yanıt verir.

Merhaba hizmetinin hello CORS kurallarını ayarladıktan sonra elinizde toohello kuralları göre izin verilip verilmeyeceğini hello hizmet karşı farklı bir etki alanından yapılan düzgün bir şekilde kimliği doğrulanmış bir isteği değerlendirilen toodetermine böylece şimdi destek CORS azure depolama hizmetleri Belirtilen.
## <a name="networking"></a>Ağ
Merhaba bölüm Azure ağ güvenliği ve Özet bilgilerini bu özellikleri hakkında temel özellikleri ile ilgili ek bilgiler sağlar.

### <a name="network-layer-controls"></a>Ağ katmanı denetimleri
Ağ erişim denetimi, belirli aygıtları veya alt ağ bağlantısı tooand sınırlama hello işlemidir ve ağ güvenliği çekirdek temsil hello. sanal makineler ve hizmetler erişilebilir tooonly kullanıcılardır ve aygıtları toowhich erişilebilir istediğiniz emin toomake Hello ağ erişim denetimi belirtilir.

#### <a name="network-security-groups"></a>Ağ Güvenlik Grupları
A [ağ güvenlik grubu (NSG)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) temel bir durum bilgisi olan paket güvenlik duvarı ve filtreleme etkinleştirir temelinde, toocontrol erişimi olan bir [5-tanımlama grubu](https://www.techopedia.com/definition/28190/5-tuple). Nsg'ler erişim denetimleri kimlik doğrulamalı veya uygulama katmanı denetleme sağlamaz. Kullanılabilmesi için bir Azure sanal ağ içindeki alt ağlara ve bir Azure sanal ağ ve hello Internet arasında trafiği arasında taşıma toocontrol trafiği.

#### <a name="route-control-and-forced-tunneling"></a>Rota denetimi ve zorlamalı tünel
Merhaba özelliği toocontrol yönlendirme, Azure sanal ağlar üzerindeki bir kritik ağ güvenliği ve erişim denetimi özelliği davranıştır. Örneğin, Azure sanal ağınızda gelen tüm trafiği tooand bu sanal güvenlik gereç yoluyla gider emin toomake istiyorsanız, toobe mümkün toocontrol ve gerekir yönlendirme davranışını özelleştirebilirsiniz. Azure'da kullanıcı tanımlı rotaları yapılandırarak bunu yapabilirsiniz.

[Kullanıcı tanımlı yollar](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) toocustomize izin içine ve dışına tek tek sanal makineleri veya alt ağlar tooinsure taşıma trafiği gelen ve giden yollar hello en güvenli yolu mümkün. [Zorlanan tünel](https://www.petri.com/azure-forced-tunneling) olan hizmetlerinizi olmayan tooensure kullanabileceğiniz bir mekanizma hello Internet üzerinde bir bağlantı toodevices tooinitiate izin.

Bu mümkün tooaccept gelen bağlantıları olan ve ardından yanıt farklıdır toothem. Gelen toothese web sunucuları ve hello web sunucuları Internet kaynaklanan trafiğe izin şekilde yanıt verebilir ve ön uç web sunucuları Internet konakları toorespond toorequests gerekir.

Zorlamalı tünel yaygın olarak kullanılan tooforce giden trafiği toohello Internet toogo şirket içi güvenlik proxy ve güvenlik duvarları üzerinden olur.

#### <a name="virtual-network-security-appliances"></a>Sanal ağ güvenlik uygulamaları
Ağ güvenlik grupları, kullanıcı tanımlı yollar ve zorlamalı tünel hello hello ağ ve Aktarım katmanı güvenlik düzeyini sunarken [OSI modeli](https://en.wikipedia.org/wiki/OSI_model), en yüksek düzeylerde tooenable güvenlik istediğinizde zamanlar olabilir Merhaba yığını. Bu gelişmiş ağ güvenlik özellikleri Azure iş ortağı ağ güvenlik Gereci çözümünü kullanarak erişebilirsiniz. Merhaba ziyaret ederek en güncel Azure iş ortağı ağ güvenlik çözümlerini hello bulabilirsiniz [Azure Marketi](https://azure.microsoft.com/marketplace/) ve "güvenlik" ve "ağ güvenliği" için arama

### <a name="azure-virtual-network"></a>Azure Sanal Ağ

Bir Azure sanal ağı (VNet), kendi ağ hello bulutta gösterimidir. Hello Azure ağ ayrılmış doku tooyour abonelik mantıksal yalıtımının olur. Başlangıç IP adresi blokları, DNS ayarları, güvenlik ilkeleri ve bu ağ içindeki yol tablolarını tam olarak denetleyebilirsiniz. Sanal ağınızı alt ağlara ayırabilir ve Azure Iaas sanal makineleri (VM'ler) koyun ve/veya [bulut hizmetlerini (PaaS rolü örnekleri)](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me) Azure sanal ağlar üzerindeki.

Ayrıca, hello birini kullanarak hello sanal ağ tooyour şirket ağına bağlanabilir [bağlantı seçenekleri](https://docs.microsoft.com/azure/vpn-gateway/) Azure içinde kullanılabilir. Esas olarak, Azure sunduğu Kurumsal ölçek hello yararı IP adres blokları üzerinde tam denetim, ağ tooAzure genişletebilirsiniz.

Azure ağı çeşitli güvenli uzaktan erişim senaryoları destekler. Bunlardan bazıları şunlardır:

-   [Ayrı iş istasyonları tooan Azure Virtual Network Bağlan](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps)

-   [VPN ile şirket içi ağ tooan Azure Virtual Network Bağlan](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

-   [Ayrılmış bir WAN bağlantısı ile şirket içi ağ tooan Azure Virtual Network Bağlan](https://docs.microsoft.com/azure/expressroute/expressroute-introduction)

-   [Diğer Azure sanal ağlar tooeach Bağlan](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vnet-vnet-rm-ps)

### <a name="vpn-gateway"></a>VPN Gateway
Azure sanal ağınızda ve şirket içi sitenizi arasındaki ağ trafiğini toosend, Azure sanal ağınız için bir VPN ağ geçidi oluşturmanız gerekir. A [VPN ağ geçidi](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) şifrelenmiş trafik ortak bir bağlantı üzerinden gönderir sanal ağ geçidi türüdür. Hello Azure ağ yapısı üzerinden Azure sanal ağlar arasında VPN ağ geçitleri toosend trafiği de kullanabilirsiniz.

### <a name="express-route"></a>Express Route
Microsoft Azure [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) bağlantı sağlayıcı tarafından kolaylaştırılan adanmış özel bağlantı üzerinden şirket içi ağlarınızı Microsoft bulut hello genişletmenizi sağlayan adanmış bir WAN bağlantısı.

![Express Route](./media/azure-security/azure-security-fig1.png)

ExpressRoute ile Microsoft Azure, Office 365 ve CRM Online gibi bağlantıları tooMicrosoft bulut Hizmetleri kurabilirsiniz. Ortak yerleşim tesisinde bağlantı sağlayıcısı üzerinden herhangi bir ağdan herhangi bir ağa (IP VP), noktadan noktaya Ethernet ağı veya sanal çapraz bağlantısından bağlantı olabilir. 

ExpressRoute bağlantıları değil Git genel Internet hello ve bu nedenle VPN tabanlı çözümler daha güvenli kabul edilebilir. Bu ExpressRoute bağlantıları toooffer daha fazla güvenilirlik, yüksek hız, düşük gecikme ve normal bağlantıları daha yüksek güvenlik hello Internet sağlar.


### <a name="application-gateway"></a>Application Gateway
Microsoft [Azure uygulama ağ geçidi](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) sağlayan bir [uygulama teslim denetleyici (ADC)](https://en.wikipedia.org/wiki/Application_delivery_controller) çeşitli katman 7 Yük Dengeleme, uygulamanız için sunumu bir hizmet olarak.

![Application Gateway](./media/azure-security/azure-security-fig2.png)

Bu CPU yoğunluklu SSL sonlandırma toohello uygulama ağ geçidi (olarak da bilinen "SSL boşaltma" veya "SSL köprülemesi") boşaltarak toooptimize web grubu verimlilik sağlar. Tek bir uygulama ağ geçidi arkasında birden çok Web sitesini hepsini dağıtım gelen trafiği, tanımlama bilgisi tabanlı oturum benzeşimi, URL yolu tabanlı Yönlendirme ve hello özelliği toohost dahil olmak üzere diğer katman 7 Yönlendirme yetenekleri de sağlar. Azure Application Gateway, bir katman 7 yük dengeleyicidir.

Merhaba Bulut veya şirket içinde olmalarından bağımsız yük devretme, HTTP isteklerini, farklı sunucular arasında performans amaçlı yönlendirme sağlar.

Uygulamanın sağladığı HTTP dahil olmak üzere pek çok uygulama teslim denetleyici (ADC) özelliklerini Yük Dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi [Güvenli Yuva Katmanı (SSL)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-powershell) boşaltma, özel sistem durumu araştırmalarının, çoklu site desteği ve diğer birçok.

### <a name="web-application-firewall"></a>Web Uygulaması Güvenlik Duvarı
Web uygulaması güvenlik duvarı özelliğidir [Azure uygulama ağ geçidi](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) standart uygulama teslim denetimi (ADC) işlevleri için uygulama ağ geçidini kullanan tooweb uygulamaları koruma sağlar. Web uygulaması Güvenlik Duvarı bu hello OWASP üst 10 ortak web güvenlik açıkları çoğunu karşı koruma tarafından yapar.

![Web Uygulaması Güvenlik Duvarı](./media/azure-security/azure-security-fig1.png)

-   SQL ekleme koruması

-   Komut ekleme, HTTP isteği kaçakçılığı, HTTP yanıtı bölme ve uzak dosya ekleme saldırıcı gibi Yaygın Web Saldırıları Koruması

-   HTTP protokolü ihlallerine karşı koruma

-   Eksik konak kullanıcısı-aracısı ve kabul üst bilgileri gibi HTTP protokolü anormalliklerine karşı koruma

-   Robotlar, gezginler ve tarayıcıları önleme

-   Ortak uygulama yapılandırma hataları (diğer bir deyişle, Apache, IIS, vb.) algılanması


Bir merkezi web uygulaması güvenlik duvarı tooprotect web saldırılarına karşı güvenlik yönetimi daha kolay hale getirir ve yetkisiz hello tehditlere karşı daha iyi bir güvence toohello uygulama verir. WAF Çözüm Merkezi bir konumda her tek tek web uygulamalarının güvenliğini sağlama karşı bilinen bir güvenlik açığı düzeltme eki uygulama tarafından tooa güvenlik tehdidi daha hızlı ayrıca tepki. Varolan bir uygulama ağ geçitleri olabilir tooan uygulama ağ geçidi web uygulaması güvenlik duvarı ile kolayca dönüştürülür.
### <a name="traffic-manager"></a>Traffic Manager
Microsoft [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) toocontrol hello dağıtım kullanıcı trafiğinin farklı veri merkezlerinde hizmet uç noktaları sağlar. Hizmet uç noktaları traffic Manager tarafından desteklenen Azure VM'ler, Web uygulamaları ve bulut hizmetleri içerir. Traffic Manager’ı harici, Azure dışı uç noktalar için de kullanabilirsiniz. Trafik Yöneticisi kullanan etki alanı adı sistemi (DNS) toodirect istemci istekleri göre en uygun toohello uç nokta hello bir [trafik yönlendirme yöntemini](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) ve hello uç noktaları hello sistem durumu.

Trafik Yöneticisi sağlayan bir dizi trafik yönlendirme yöntemleri toosuit farklı, uygulama gereksinimlerinde uç nokta durumu [izleme](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring)ve otomatik yük devretme. Trafik, tüm bir Azure bölgesi hello başarısızlığını dahil esnek toofailure yöneticisidir.
### <a name="azure-load-balancer"></a>Azure Load Balancer
[Azure yük dengeleyici](https://docs.microsoft.com/azure/load-balancer/load-balancer-overview) tooyour uygulamaları yüksek kullanılabilirlik ve ağ performansı sunar. Gelen trafiği yükü dengelenmiş bir kümede tanımlanmış Hizmetleri sağlıklı örnekleri arasında dağıtır bir katman 4 (TCP, UDP) yük dengeleyici olur. Azure yük dengeleyici için yapılandırılabilir:

-   Gelen Internet trafiği toovirtual makinelerin yük dengelemesini. Bu yapılandırma olarak bilinir [Internet'e yönelik Yük Dengeleme](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview).

-   Yük Dengeleme trafiği sanal ağ içindeki sanal makineler arasında bulut Hizmetleri içindeki sanal makineler arasında veya şirket içi bilgisayarlar ve bir şirket içi sanal ağdaki sanal makineler arasında. Bu yapılandırma olarak bilinir [iç Yük Dengeleme](https://docs.microsoft.com/azure/load-balancer/load-balancer-internal-overview). 

- Dış trafiğin tooa belirli bir sanal makine ilet

### <a name="internal-dns"></a>İç DNS
DNS sunucularının bir VNet hello Yönetim Portalı veya hello ağ yapılandırma dosyasında kullanılan hello listesini yönetebilirsiniz. Müşteri için her bir Vnet'teki too12 DNS sunucularını ekleyebilirsiniz. DNS sunucuları belirtirken, müşterinin ortamı için hello doğru sırayla Müşteri'nin DNS sunucularını listelemek önemli tooverify var. DNS sunucu listelerini hepsini çalışmaz. Bunlar belirtildikleri hello sırada kullanılır. Hello ilk DNS sunucusunda hello listesi ulaşıldı mümkün toobe ise, hello istemci hello DNS sunucusu değil veya düzgün çalışmıyor bağımsız olarak, DNS sunucusunu kullanır. toochange hello müşterinin sanal ağ için DNS sunucusu sırası hello DNS sunucuları hello listesinden kaldırmak ve bunları geri hello sırada o müşteri eklemek istiyor. DNS hello kullanılabilirlik hello "CIA" güvenlik Üçlü yönünü destekler.

### <a name="azure-dns"></a>Azure DNS
Merhaba [etki alanı adı sistemi](https://technet.microsoft.com/library/bb629410.aspx), veya DNS, çevirmek için sorumlu (veya çözme) bir Web sitesi veya hizmet name tooits IP adresi. [Azure DNS](https://docs.microsoft.com/azure/dns/dns-overview) DNS etki alanı, Microsoft Azure altyapı kullanılarak ad çözümlemesi sağlamak için bir barındırma hizmetidir. Azure etki alanlarınızı barındırarak DNS sunucunuzun yönetebilirsiniz kullanarak kayıtları, diğer Azure hizmetleriyle aynı kimlik bilgileri, API'leri, Araçlar ve faturalama hello. DNS hello kullanılabilirlik hello "CIA" güvenlik Üçlü yönünü destekler.
### <a name="log-analytics-nsgs"></a>Günlük analizi Nsg'ler
Tanılama günlük kategorileri için Nsg'ler aşağıdaki hello etkinleştirebilirsiniz:
-   Olay: için hangi NSG uygulanan tooVMs ve örnek rolleriniz MAC adresine dayalı kurallardır girdiler içeriyor. Bu kurallar Hello durumunun her 60 saniyede toplanır.

-   Kuralları sayaç: her NSG kural uygulanan toodeny kaç defa için girdiler içeriyor veya trafiğe izin verecek.

### <a name="azure-security-center"></a>Azure Güvenlik Merkezi
Güvenlik Merkezi, engellemenize, algılamanıza ve toothreats yanıt yardımcı olur ve, artırılmış görünürlük ve denetim olanağı, Azure kaynaklarınızın güvenlik hello sağlar. Azure aboneliklerinize arasında tümleşik güvenlik izleme ve ilke yönetimi sağlar, kaçabilecek tehditleri ve güvenlik çözümlerinin geniş ekosistemiyle çalışır algılamaya yardımcı olur. Ağ önerileri Merkezi güvenlik duvarları, ağ güvenlik grupları, yapılandırma gelen trafiği kuralları ve daha fazla etrafında.

Kullanılabilir ağ önerileri aşağıdaki gibidir:

-   [Yeni nesil güvenlik duvarı ekleme](https://docs.microsoft.com/azure/security-center/security-center-add-next-generation-firewall) güvenlik korumaları bir Microsoft iş ortağı tooincrease İleri nesil Güvenlik Duvarı (NGFW) eklemek önerir

-   [Rota yalnızca trafiği NGFW aracılığıyla](https://docs.microsoft.com/azure/security-center/security-center-add-next-generation-firewall#route-traffic-through-ngfw-only) yapılandırdığınız önerir gelen trafiği tooyour, NGFW aracılığıyla VM zorla güvenlik grubu (NSG) kuralları ağ.

-   [Ağ güvenlik grupları alt ağları veya sanal makinelerde etkinleştir](https://docs.microsoft.com/azure/security-center/security-center-enable-network-security-groups) Nsg'ler alt ağları veya VM'ler etkinleştirmenizi önerir.

-   [Uç nokta Internet'e aracılığıyla erişimi kısıtlamak](https://docs.microsoft.com/azure/security-center/security-center-restrict-access-through-internet-facing-endpoints) için Nsg'ler gelen trafik kurallarını yapılandırmak önerir.


## <a name="compute"></a>İşlem

Merhaba bölüm bu alan ve Özet bilgilerini bu özellikleri hakkında temel özellikleri ile ilgili ek bilgiler sağlar.

### <a name="antimalware--antivirus"></a>Kötü amaçlı yazılımdan koruma & virüsten koruma
Azure Iaas ile sanal makinelerinizi kötü amaçlı dosyalar, reklam ve diğer tehditlere kötü amaçlı yazılımdan koruma yazılımı Microsoft, Symantec, eğilim mikro, McAfee ve Kaspersky tooprotect gibi güvenlik satıcılardan kullanabilirsiniz. [Microsoft Antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware) Azure Cloud Services ve sanal makineler için belirlemek ve virüsler, casus yazılım ve diğer kötü amaçlı yazılımları kaldırmak yardımcı olan bir koruma özelliğidir. Microsoft Antimalware bilinen kötü amaçlı veya istenmeyen yazılım girişimleri tooinstall kendisini veya Azure sistemlerinize çalıştırdığınızda yapılandırılabilir uyarılar sağlar. Microsoft Antimalware ayrıca Azure Güvenlik Merkezi kullanılarak dağıtılabilir

### <a name="hardware-security-module"></a>Donanım güvenlik modülü
Merhaba anahtarlar kendilerini korunan sürece şifreleme ve kimlik doğrulama güvenliği değil. Bunları depolayarak hello yönetim ve güvenlik kritik parolaları ve anahtarlar basitleştirebilirsiniz [Azure anahtar kasası](https://docs.microsoft.com/azure/key-vault/key-vault-whatis). Anahtar kasası hello seçeneği toostore anahtarlarınızı donanım güvenlik modülleri (HSM'ler) sertifikalı tooFIPS 140-2 Düzey 2 standartları de sağlar. SQL Server şifreleme anahtarları için yedekleme veya [saydam veri şifreleme](https://msdn.microsoft.com/library/bb934049.aspx) herhangi bir anahtar veya gizli, uygulamalardan ile anahtar kasasına tüm depolanabilir. İzinler ve erişim toothese korunan öğeleri üzerinden yönetilir [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).

### <a name="virtual-machine-backup"></a>Sanal makine yedekleme
[Azure yedekleme](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) sıfır sermaye yatırımı ve en az uygulama verilerinizi koruyan bir çözüm işletim maliyetlerini. Uygulama hataları, veri bozulmasına neden ve İnsan hatalara uygulamalarınıza toosecurity sorunları neden olabilecek hataları neden olabilir. Azure Backup ile Windows ve Linux çalıştıran sanal makinelerinizi korunur.

### <a name="azure-site-recovery"></a>Azure Site Recovery
Kuruluşunuzun önemli bir kısmını [iş sürekliliği/olağanüstü durum kurtarma (BCDR)](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) stratejisi açık nasıl tookeep kurumsal iş yüklerini ve uygulamaları kurma ve Planlı çalışan ve planlanmayan kesintiler meydana çıkışı. [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) yardımcı olur, çoğaltma, yük devretme ve kurtarma iş yükleri ve uygulamalar, birincil konumunuzun çökmesi durumunda ikincil konum kullanılabilir; böylece düzenlemek.

### <a name="sql-vm-tde"></a>SQL VM TDE'NİN
[Saydam veri şifreleme (TDE)](https://docs.microsoft.com/azure/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-ps-sql-keyvault) ve sütun düzeyinde şifreleme (Temizle) SQL server şifreleme özellikleri. Bu şifreleme biçimi müşteriler toomanage ve depolama şifreleme için kullandığınız şifreleme anahtarları hello gerektirir.

Hello Azure anahtar kasası (AKV) hizmeti tasarlanmış tooimprove hello güvenliği ve yönetimi için güvenli ve yüksek oranda kullanılabilir bir konumda Bu anahtarları ' dir. Merhaba SQL Server Bağlayıcısı Bu anahtarları Azure anahtar Kasası'ndan SQL Server toouse sağlar.

Şirket içi makineler ile SQL Server çalışıyorsa, şirket içi SQL Server makinenizden tooaccess Azure anahtar kasası izleyebileceğiniz adımlar vardır. Ancak Azure vm'lerinde SQL Server için hello Azure anahtar kasası tümleştirmeyi özelliğini kullanarak zaman kazanabilirsiniz. Bu özellik ile birkaç Azure PowerShell cmdlet'leri tooenable otomatikleştirebilirsiniz yapılandırması için bir SQL VM tooaccess gerekli anahtar kasanızı hello.

### <a name="vm-disk-encryption"></a>VM Disk şifrelemesi
[Azure Disk şifrelemesi](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) yardımcı olan yeni bir özellik, Windows ve Linux Iaas sanal makine diskleriniz şifrelemek değil. Merhaba endüstri standart BitLocker özelliği, Windows ve Linux tooprovide birim şifreleme hello işletim sistemi için hello DM-Crypt özelliği ve hello veri diskleri geçerlidir. Merhaba çözüm denetlemek ve hello disk şifreleme anahtarları ve gizli anahtar kasası aboneliğinizi yönetmek Azure anahtar kasası toohelp tümleşiktir. Merhaba çözüm ayrıca hello sanal makine disklerdeki tüm veriler Azure depolama alanınızı bekleyen şifrelenmesini sağlar.

### <a name="virtual-networking"></a>Sanal ağ
Sanal makinelerin ağ bağlantısı gerekir. toosupport bu gereksinim, Azure gerektirir bağlı sanal makineleri toobe tooan Azure sanal ağı. Bir Azure sanal ağı hello Azure fiziksel ağ yapısında en üstünde oluşturulmuş mantıksal bir yapıdır. Her mantıksal [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) tüm diğer Azure sanal ağlardan yalıtılır. Bu yalıtım dağıtımlarınızı ağ trafiğini değil erişilebilir tooother Microsoft Azure müşterilerin olduğunu güvence altına yardımcı olur.

### <a name="patch-updates"></a>Düzeltme eki güncelleştirir
Düzeltme eki güncelleştirmeleri hello temel bulma ve olası sorunları düzeltmek için sunar ve hello yazılım güncelleştirme yönetimi işlemi, yazılım güncelleştirmeleri, kuruluşunuzda dağıtmalısınız hello sayısını azaltarak hem özelliği toomonitor artırarak basitleştirin Uyumluluk.

### <a name="security-policy-management-and-reporting"></a>Güvenlik İlkesi Yönetimi ve Raporlama
[Azure Güvenlik Merkezi](https://docs.microsoft.com/azure/security-center/security-center-intro) engellemenize, algılamanıza ve toothreats yanıt yardımcı olur ve artan, görünürlük ve denetim üzerinden, Azure kaynaklarınızın hello güvenlik sağlar. Azure aboneliklerinize arasında tümleşik güvenlik izleme ve ilke yönetimi sağlar, kaçabilecek tehditleri ve güvenlik çözümlerinin geniş ekosistemiyle çalışır algılamaya yardımcı olur.

### <a name="azure-security-center"></a>Azure Güvenlik Merkezi
Güvenlik Merkezi engellemek, algılamanıza ve Artırılmış görünürlük aracılığıyla toothreats hello Azure kaynaklarınızın güvenliğini denetlemenize yanıtlamanıza yardımcı olur. Aboneliklerinizde, tümleşik güvenlik izleme ve ilke yönetimi sağlar; normal koşullarda gözden kaçabilecek tehditleri algılamaya yardımcı olur ve güvenlik çözümlerinin geniş ekosistemiyle çalışır.

## <a name="identify-and-access-management"></a>Tanımlama ve yönetim erişme

Sistemleri, uygulamaları ve verileri güvenli hale getirme kimlik tabanlı erişim denetimlerini ile başlar. Microsoft iş ürünleri ve Hizmetleri yerleşik hello kimlik ve erişim yönetimi özellikleri, kullanılabilir toolegitimate kullanıcıların ne zaman ve yerde yaparken, kurumsal ve kişisel bilgilerinizi yetkisiz erişime karşı korunmasına yardımcı olur Bunu ihtiyaç duyar.

### <a name="secure-identity"></a>Güvenli kimlik
Microsoft, ürün ve Hizmetleri toomanage kimlik ve erişim arasında birden çok güvenlik uygulamaları ve teknolojileri kullanır.
-   [Çok faktörlü kimlik doğrulaması](https://azure.microsoft.com/services/multi-factor-authentication/) erişim, şirket içi ve hello bulutta kullanıcılar toouse birden çok yöntem gerektirir. Basit bir oturum açma işlemini kullanıcılarla destekleme sırasında güçlü kimlik doğrulaması kolay doğrulama seçeneklerini aralıklı sağlar.

-   [Microsoft Authenticator](https://aka.ms/authenticator) Microsoft Azure Active Directory ve Microsoft hesapları ile çalışır ve wearables ve parmak izi tabanlı onayları desteği içeren kullanıcı dostu bir çok faktörlü kimlik doğrulaması deneyimi sağlar.

-   [Parola ilkesi zorlama](https://azure.microsoft.com/documentation/articles/active-directory-passwords-policy/) artar düzenli döndürme, zorunlu, uzunluğu ve karmaşıklık gereksinimleri koyarak geleneksel parolaların güvenliğini hello ve hesap kilitleme başarısız kimlik doğrulamasından sonra çalışır.

-   [Belirteç tabanlı kimlik doğrulaması](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/) Active Directory Federasyon Hizmetleri (AD FS) aracılığıyla kimlik doğrulaması veya üçüncü taraf güvenli belirteç sistemlerde sağlar.

-   [Rol tabanlı erişim denetimi (RBAC)](https://azure.microsoft.com/documentation/articles/role-based-access-built-in-roles/) etkinleştirir hello kullanıcının dayalı toogrant erişim atanan rol, kolay toogive kullanıcılar yalnızca hello erişim miktarını yapmadan tooperform, iş görevlerini ihtiyaç duydukları. Kuruluşunuzun iş modeli ve risk toleransınıza RBAC özelleştirebilirsiniz.

-   [Tümleşik Kimlik Yönetimi (karma kimlik)](https://azure.microsoft.com/documentation/articles/active-directory-hybrid-identity-design-considerations-overview/) tooall kaynakları tek bir kullanıcı kimliği kimlik doğrulaması ve yetkilendirme oluşturma iç veri merkezleri ile bulut platformlarda, kullanıcıların erişim toomaintain denetim sağlar.

### <a name="secure-apps-and-data"></a>Güvenli uygulamalar ve veriler
[Azure Active Directory](https://azure.microsoft.com/services/active-directory/), kapsamlı bir kimlik ve erişim yönetimi bulut çözüm, güvenli erişim toodata sitesindeki uygulamaların ve hello bulut yardımcı olur ve kullanıcılar ve gruplar hello yönetimini basitleştirir. Kimlik Yönetimi, güvenlik ve uygulamaya erişim yönetimi, Gelişmiş çekirdek dizin hizmetlerini birleştirir ve geliştiricilerin toobuild ilke tabanlı kimlik uygulamalarını yönetime kolaylaştırır. tooenhance, Azure Active Directory hello Azure Active Directory temel, Premium P1 ve Premium P2 sürümleri kullanılarak Ücretli özellikleri ekleyebilirsiniz.

| Ücretsiz / ortak özellikler     | Temel özellikler    |Premium P1 özellikleri |Premium P2 özellikleri | Azure Active Directory katılım – Windows 10 yalnızca ilgili özellikleri|
| :------------- | :------------- |:------------- |:------------- |:------------- |
|   [Dizin nesnelerini](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#directory-objects), [kullanıcı/Grup Yönetimi (ekleme/güncelleştirme/silme) / kullanıcı tabanlı sağlama, cihaz kaydı](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#usergroup-management-addupdatedelete-user-based-provisioning-device-registration), [çoklu oturum açma (SSO)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#single-sign-on-sso), [Self Servis Bulut kullanıcıları için parola değişikliği](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-change-for-cloud-users), [Bağlan (şirket içi dizinleri tooAzure Active Directory genişletir eşitleme altyapısı)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#connect-sync-engine-that-extends-on-premises-directories-to-azure-active-directory), [güvenlik / kullanım raporları](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#securityusage-reports)       |     [Grup tabanlı erişim yönetimi / sağlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#group-based-access-managementprovisioning), [bulut kullanıcıları için Self Servis parola sıfırlama](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-reset-for-cloud-users), [şirket markası (oturum açma sayfaları/erişim paneli özelleştirme)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#company-branding-logon-pagesaccess-panel-customization), [uygulama proxy'si](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#application-proxy), [% SLA 99,9](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#sla-999) |  [Self Servis grup ve uygulama yönetimi/Self-Servis uygulama eklemeleri/dinamik gruplar](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-group), [Self Servis parola sıfırlama/Değiştir/Unlock ile şirket içi sonradan yazma](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-resetchangeunlock-with-on-premises-write-back), [(Bulut ve şirket içi (MFA sunucusu)) çok faktörlü kimlik doğrulaması](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#multi-factor-authentication-cloud-and-on-premises-mfa-server), [MIM CAL + MIM sunucusu](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#mim-cal-mim-server), [Cloud App Discovery](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#cloud-app-discovery), [Connect Health](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#connect-health), [grup hesapları için otomatik parola geçişi](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#automatic-password-rollover-for-group-accounts)|     [Kimlik koruması](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-identityprotection), [Privileged Identity Management](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-privileged-identity-management-configure)|    [Azure AD, yönetici Bitlocker kurtarma için Microsoft Passport bir aygıt tooAzure AD, Masaüstü SSO katılma](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#join-a-device-to-azure-ad-desktop-sso-microsoft-passport-for-azure-ad-administrator-bitlocker-recovery), [MDM otomatik kayıt, Self Servis Bitlocker kurtarma, Azure yoluyla ek yerel Yöneticiler tooWindows 10 cihazlar AD birleştirme](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#mdm-auto-enrollment)|


- [Cloud App Discovery](https://docs.microsoft.com/azure/active-directory/active-directory-cloudappdiscovery-whatis) kuruluşunuzdaki hello çalışanlar tarafından kullanılan tooidentify bulut uygulamalarını sağlar Azure Active Directory premium özelliğidir.

- [Azure Active Directory kimlik koruması](https://azure.microsoft.com/documentation/articles/active-directory-identityprotection/) Azure Active Directory anomali algılama yeteneklerini tooprovide birleştirilmiş görünüme risk olaylarına ve etkileyebilecek olası güvenlik açıklarını kullanan bir güvenlik hizmeti, Kuruluşunuzun kimlik.

- [Azure Active Directory etki alanı Hizmetleri](https://azure.microsoft.com/services/active-directory-ds/) hello gerek olmadan toodeploy etki alanı denetleyicileri toojoin Azure VM'ler tooa etki alanı sağlar. Kullanıcılar toothese VM'ler Kurumsal Active Directory kimlik bilgilerini kullanarak oturum açın ve kaynaklara sorunsuz bir şekilde erişebilir.

- [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) ölçeklendirmek kimlikleri milyonlarca toohundreds ve mobil arasında tümleştirme tüketiciye yönelik uygulamalar için yüksek oranda kullanılabilir, genel kimlik yönetim hizmeti ve web platformlar. Müşterilerinize uygulamalarınızı var olan sosyal medya hesaplarını kullanmak özelleştirilebilir deneyimler aracılığıyla tooall kaydolabilirsiniz veya yeni tek başına kimlik bilgileri oluşturabilirsiniz.

- [Azure Active Directory B2B işbirliği](https://aka.ms/aad-b2b-collaboration) etkinleştirerek, şirketler arası ilişkilerinizi destekler güvenli iş ortağı tümleştirme çözüm ortakları tooaccess şirket uygulamaları ve verileri seçmeli olarak kendi kendi kendine yönetilen kullanarak olduğu kimlikler.

- [Azure Active Directory katılım](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-overview/) tooextend bulut özellikleri tooWindows 10 cihazlar için merkezi yönetim sağlar. Kullanıcıların tooconnect toohello şirket veya kuruluş bulut Azure Active Directory üzerinden mümkün hale getirir ve erişim tooapps ve kaynakları basitleştirir.

- [Azure Active Directory Uygulama proxy'si](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/) şirket içinde barındırılan web uygulamalarını SSO ve güvenli uzaktan erişim sağlar.

## <a name="next-steps"></a>Sonraki Adımlar
- [Microsoft Azure Security ile çalışmaya başlama](https://docs.microsoft.com/azure/security/azure-security-getting-started)

Azure hizmetlerini ve özellikleri toohelp kullanabilirsiniz, hizmetleri ve Azure içindeki verilerinizi güvenli

- [Azure Güvenlik Merkezi](https://azure.microsoft.com/services/security-center/)

Engellemenize, algılamanıza ve Azure kaynaklarınızın hello güvenlik üzerinde daha fazla görünürlük ve Denetim ile toothreats yanıt

- [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](https://docs.microsoft.com/azure/security-center/security-center-monitoring)

Azure Güvenlik Merkezi toomonitor uyumluluk ilkeleriyle izleme kapasiteleri hello.
