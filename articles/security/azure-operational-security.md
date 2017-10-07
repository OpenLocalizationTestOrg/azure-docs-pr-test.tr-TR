---
title: "işletimsel güvenlik aaaAzure | Microsoft Docs"
description: "Microsoft Operations Management Suite (OMS), hizmetlerinin ve nasıl çalıştığı hakkında bilgi edinin."
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
ms.openlocfilehash: 85e0c74314ed97a53d395b209e348b779a5d14c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security"></a>Azure işlem güvenliği
## <a name="introduction"></a>Giriş

### <a name="overview"></a>Genel Bakış
Güvenlik hello bulutta iş ve nasıl önemli Azure güvenliği hakkında doğru ve güncel bilgi bulma olduğunu olduğunu biliyoruz. Merhaba en iyi uygulamalar ve hizmetler için nedenleri toouse Azure hello çeşitli güvenlik araçları ve yetenekler tootake avantajlarından biri. Bu araçları ve yetenekleri, olası toocreate güvenli çözümleri hello güvenli Azure platformu yardımcı olur. Windows Azure gizlilik, bütünlük ve müşteri verilerini, kullanılabilirliğini, ayrıca saydam sorumluluk etkinleştirirken sağlamanız gerekir.

toohelp müşteriler, Microsoft Azure içinde her iki hello müşterinin uygulanan güvenlik denetimleri hello dizisi daha iyi anlamak ve Microsoft işlemsel bakış açılarını, "Azure işletimsel güvenlik", bu teknik incelemede sağlayan yazılmış bir Merhaba işletimsel güvenlik Windows Azure ile kullanılabilir kapsamlı bakın.

### <a name="azure-platform"></a>Azure platformu
Azure işletim sistemleri, programlama dilleri, çerçeveleri, Araçlar, veritabanları ve aygıtları geniş çapta destekleyen bir genel bulut hizmeti platformudur. Docker Tümleştirmesi ile Linux kapsayıcıları çalıştırabilirsiniz; JavaScript, Python, .NET, PHP, Java ve Node.js ile uygulamalar oluşturma; Yapı geri-iOS, Android ve Windows cihazları sona erer. Azure bulut hizmeti, geliştiriciler ve BT uzmanları, aynı teknolojileri milyonlarca zaten kullanır ve güven hello destekler.

Derleme ya da BT varlıklarına geçirmek hello Hizmetleri ve hello denetimleri ile veri ve uygulamaları, bir kuruluşun yeteneklerini tooprotect üzerinde bağlı bir genel bulut hizmeti sağlayıcısı, bulut tabanlı toomanage hello güvenliğini sağlarlar varlıklar.

Azure'un altyapısından aynı anda milyonlarca müşteri barındırmak için hello tesis tooapplications gelen tasarlanmıştır ve güvenlik gereksinimlerine bağlı işletmeler karşılayabilecek güvenilir bir temel sağlar. Ayrıca, Azure, çok çeşitli yapılandırılabilir güvenlik seçenekleri ve hello özelliği toocontrol sağlar bunları böylece güvenlik toomeet hello benzersiz gereksinimleri, kuruluşunuzun dağıtımlarının özelleştirebilirsiniz. Bu belge, nasıl Azure güvenliği anlamanıza yardımcı özellikler, bu gereksinimleri karşılamak yardımcı.

### <a name="abstract"></a>Özet
Azure işlem güvenliği verilerini, uygulamaları ve diğer Microsoft Azure varlıkları korumak için toohello Hizmetleri, denetimleri ve özellikler kullanılabilir toousers ifade eder. Azure işlem güvenliği benzersiz tooMicrosoft hello Microsoft Security Development Lifecycle (SDL), Microsoft Security Response Center hello dahil olmak üzere, çeşitli özelliklerini elde edilen hello bilgi içeren bir çerçevesi üzerine inşa edilmiştir Program ve hello siber güvenlik tehdit derin tanıma.

Bu teknik incelemede hello Microsoft Azure bulut platformu ve Hizmetleri aşağıdaki kapsar içinde Microsoft'un yaklaşımı tooAzure işletimsel güvenlik özetlenmektedir:
1.  [Azure Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

2.  [Azure Güvenlik Merkezi](https://docs.microsoft.com/azure/security-center/security-center-intro)

3.  [Azure İzleyici](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

4.  [Azure Ağ İzleyicisi](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)

5.  [Azure depolama çözümlemeleri](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)

6.  [Azure Active directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)


## <a name="microsoft-operations-management-suite"></a>Microsoft Operations Management Suite

Microsoft Operations Management Suite (OMS) hello hello karma bulut BT yönetimi çözümü ' dir. Tek başına kullanıldığında veya var olan System Center dağıtımınızı OMS verir tooextend hello en fazla esneklik ve bulut tabanlı yönetim altyapınızın denetim.

![Microsoft Operations Management Suite](./media/azure-operational-security/azure-operational-security-fig1.png)

OMS ile şirket içi, Azure, AWS, Windows Server, Linux, VMware ve OpenStack, rekabet çözümleri daha düşük bir maliyetle de dahil olmak üzere tüm bulut örnek yönetebilirsiniz. Merhaba bulut ilk dünya için yerleşik, OMS toomeet yeni iş sınar ve yeni iş yükleri, uygulamaları ve bulut ortamlarını uyum hello en hızlı ve en ekonomik yoludur, kuruluşunuzdaki yeni bir yaklaşım toomanaging sunar.

### <a name="oms-services"></a>OMS hizmetleri

OMS Hello çekirdek işlevselliğini Azure üzerinde çalışan hizmetleri kümesi tarafından sağlanır. Her hizmet belirli yönetim işlevi sağlar ve Hizmetleri tooachieve farklı yönetim senaryoları birleştirebilirsiniz.

| Hizmet  | Açıklama|
| :------------- | :-------------|
| Log Analytics | İzleme ve hello kullanılabilirlik ve fiziksel gibi farklı kaynaklarına ve sanal makineleri performansını analiz edin. |
|Otomasyon | El ile gerçekleştirilen işlemleri otomatikleştirin; fiziksel ve sanal makinelere yapılandırma uygulayın. |
| Backup | Yedekleme ve geri yükleme kritik verileri. |
| Site Recovery | Kritik uygulamalar için yüksek kullanılabilirlik sağlayın. |

### <a name="log-analytics"></a>Log Analytics

[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics), yönetilen kaynaklardan toplanan verileri merkezi bir depoda birleştirerek OMS için izleme hizmetleri sağlar. Bu veriler, olayları, performans verileri veya hello API sağlanan özel verileri içerebilir. Toplandığında, hello veri uyarı, analiz ve dışarı aktarma için kullanılabilir.


Bu yöntem, çeşitli kaynaklardan tooconsolidate veri tanır, birleştirebilirsiniz şekilde varolan ile Azure hizmetlerinizi verilerden ortamı şirket. Aynı zamanda açıkça hello hello veri koleksiyonunu tüm eylemleri kullanılabilir tooall veri türlerini; böylece bu veriler üzerinde gerçekleştirilecek hello eylemden ayırır.


![Log Analytics](./media/azure-operational-security/azure-operational-security-fig2.png)

Merhaba günlük analizi hizmeti yöntemler aşağıdaki hello kullanarak bulut tabanlı verilerinizi güvenli bir şekilde yönetir:
-   veriler arasında ayrım yapma
-   veri saklama
-   Fiziksel güvenlik
-   Olay yönetimi
-   Uyumluluk
-   güvenlik standartları sertifikaları

### <a name="azure-backup"></a>Azure Backup

[Azure yedekleme](http://azure.microsoft.com/documentation/services/backup) veri yedekleme ve Hizmetleri geri yükleme ve ürün ve hizmetlerini hello OMS paketinin bir parçası olan sağlar.
Uygulama verilerinizi korur ve herhangi bir sermaye yatırımı olmadan en düşük işletim giderleriyle yıllar boyunca saklar. Bu verileri fiziksel ve sanal Windows sunucularından ayrıca SQL Server ve SharePoint gibi tooapplication iş yüklerinin yedekleyebilirsiniz. Tarafından da kullanılabilir [System Center Data Protection Manager (DPM)](https://en.wikipedia.org/wiki/System_Center_Data_Protection_Manager) tooreplicate veri tooAzure artıklık ve uzun vadeli depolama için korumalı.


Azure Backup'ta korunan veriler belirli bir coğrafi bölgede yer alan bir yedekleme kasasında depolanır. Merhaba veri çoğaltıldığında içinde hello aynı bölgede ve, kasa hello türüne bağlı olarak, ayrıca çoğaltılmış tooanother bölge daha fazla esneklik için olabilir.

### <a name="management-solutions"></a>Yönetim Çözümleri
[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) , yönetmek ve şirket içi korumak ve bulut altyapısı yardımcı olan Microsoft'un bulut tabanlı BT yönetimi çözümüdür.


[Yönetim çözümleri](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solutions) bir veya daha fazla OMS hizmetlerini kullanarak belirli bir yönetim senaryoları uygulayacak logics paketlenmiş kümeleridir. Farklı çözümler, Microsoft'un ve iş ortakları OMS tooyour Azure aboneliği tooincrease hello yatırımınızı değerini kolayca ekleyebilirsiniz kullanılabilir. Bir iş ortağı, kendi çözümleri toosupport uygulamaları ve hizmetleri oluşturmak ve bunları hello Azure Marketi veya hızlı başlangıç şablonlarından aracılığıyla toousers sağlayın.


![Yönetim Çözümleri](./media/azure-operational-security/azure-operational-security-fig4.png)

Merhaba birden çok Hizmetleri tooprovide ek işlevleri kullanan bir çözüm iyi bir örneği olan [güncelleştirme yönetimi çözümü](https://docs.microsoft.com/azure/operations-management-suite/oms-solution-update-management). Bu çözüm hello kullanır [günlük analizi](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) Aracısı Windows ve Linux toocollect hakkında bilgi için gerekli güncelleştirmeleri her aracı. Burada içeren dahil bir Pano çözümleyebilirsiniz bu verileri toohello günlük analizi depo yazar.

Runbook'ları bir dağıtım oluşturduğunuzda [Azure Otomasyonu](https://docs.microsoft.com/azure/automation/automation-intro) kullanılan tooinstall gereken güncelleştirmeler. Tüm işlem hello portalında yönetmek ve hello temel ayrıntıları hakkında tooworry olması gerekmez.

## <a name="azure-security-center"></a>Azure Güvenlik Merkezi

Azure Güvenlik Merkezi, Azure kaynaklarınızı korumanıza yardımcı olur. Aboneliklerinizde tümleşik güvenlik izleme ve ilke yönetimi, Azure sağlar. Merhaba Hizmeti'nde misiniz toodefine ilkeleri yalnızca, Azure aboneliklerinize karşı aynı zamanda karşı [kaynak grupları](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups), daha ayrıntılı olabilir.

### <a name="security-policies-and-recommendations"></a>Güvenlik ilkeleri ve öneriler

Bir güvenlik ilkesi hello belirtilen abonelik veya kaynak grubu içindeki kaynaklar için önerilen denetimleri hello kümesini tanımlar.

Güvenlik Merkezi'nde tooyour şirketinizin güvenlik gereksinimleri ve uygulamaların hello türü veya hello verilerin duyarlılığına göre ilkeleri tanımlarsınız.

![Güvenlik ilkeleri ve öneriler](./media/azure-operational-security/azure-operational-security-fig5.png)


Merhaba abonelik düzeyinde otomatik olarak etkinleştirilen ilkeler hello sağ tarafındaki hello diyagramda gösterildiği gibi hello abonelik içindeki tooall kaynak gruplarına yayılması:


### <a name="data-collection"></a>Veri toplama

Güvenlik Merkezi, sanal makineleri (VM'ler) tooassess güvenlik durumlarına toplar, güvenlik önerileri sağlamak ve toothreats sizi uyarır. Tüm vm'lerde aboneliğinizde ilk erişiminizi Güvenlik Merkezi, veri koleksiyonu etkin olmadığında. Veri toplama önerilir, ancak siz hello Güvenlik Merkezi İlkesi'nde veri toplamayı devre dışı bırakarak iptal edilebilir.

### <a name="data-sources"></a>Veri kaynakları

- Azure Güvenlik Merkezi güvenlik durumuna kaynakları tooprovide görünürlük aşağıdaki hello verilerini analiz eder, güvenlik açıklarını belirleme ve bunları azaltmanın yollarını önerilir ve etkin tehditleri algılayabilir:

-   Azure Hizmetleri: hello Azure hizmetlerinin yapılandırmasına ilişkin ilgili hizmetin kaynak sağlayıcısıyla iletişim kurarak dağıtmış olan bilgileri kullanır.

- Ağ Trafiği: Microsoft’un altyapısından kaynak/hedef IP/bağlantı noktası, paket boyutu ve ağ protokolü gibi örneği alınmış ağ trafiği meta verilerini kullanır.

-   İş Ortağı Çözümleri: Güvenlik duvarları ve kötü amaçlı yazılımdan koruma çözümleri gibi tümleşik iş ortağı çözümlerinden güvenlik uyarılarını kullanır.

-   Sanal Makineleriniz: Sanal makinelerinizdeki yapılandırma bilgilerini ve Windows olay ve denetim günlükleri, IIS günlükleri, syslog iletileri ve kilitlenme dökümü dosyaları gibi güvenlik olaylarına ilişkin bilgileri kullanır.

### <a name="data-protection"></a>Veri koruma

toohelp müşteriler engellemenize, algılamanıza ve toothreats yanıt, Azure Güvenlik Merkezi toplar ve yapılandırma bilgileri, meta verileri, olay günlükleri, kilitlenme döküm dosyaları ve daha da dahil olmak üzere, güvenlikle ilgili verileri işler. Microsoft aynılarını toostrict uyumluluk ve güvenlik yönergelerine — toooperating hizmet kodlama gelen.

-   **Veriler arasında ayrım yapma**: veri hello hizmet boyunca her bir bileşende baz mantıksal olarak ayrı tutulur. Tüm veriler kuruluşa göre etiketlenir. Bu etiketleme hello veri yaşam döngüsü boyunca devam ederse ve her hello hizmet katmanında uygulanır.

-   **Veri erişimi**: tooprovide güvenlik önerileri ve olası güvenlik tehditlerini araştırmak, Microsoft personeli erişim toplanan bilgileri veya kilitlenme döküm dosyaları da dahil olmak üzere Azure Hizmetleri tarafından analiz işlem oluşturma olayları, VM disk Anlık görüntüler ve yapıları kasıtsız olarak müşteri verilerini veya sanal makinelerinizi kişisel verileri içerebilir. Biz toohello uyması [Microsoft çevrimiçi hizmet koşulları ve gizlilik bildirimini](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31), Microsoft olmayan hangi durum müşteri verilerini kullanır veya reklam ya da benzeri ticari amaçlarla için bu bilgileri türetilir.

-   **Veri kullanımı**: Microsoft desenleri kullanır ve tehdit bilgileri birden çok görülen kiracılar tooenhance bizim önleme ve algılama yeteneklerini; biz açıklanan hello gizlilik taahhütlerine uygun olarak bunu bizim [gizlilik Deyimi](https://www.microsoft.com/privacystatement/OnlineServices/Default.aspx).

### <a name="data-location"></a>Veri konumu

Azure Güvenlik Merkezi, kilitlenme döküm dosyalarının kısa ömürlü kopyalarını toplar ve açıktan yararlanma girişimlerinin ve başarılı uzlaşmaların kanıtı olarak analiz eder. Azure Güvenlik Merkezi gerçekleştirir bu analizi içinde aynı coğrafi çalışma hello gibi hello ve analiz tamamlandığında kısa ömürlü kopyaları siler hello. Makine yapıları merkezi olarak içinde depolanan VM hello gibi aynı bölgede hello.

-   **Depolama hesaplarınızı**: sanal makineleri çalıştırdığı her bölge için bir depolama hesabı belirtilir. Hangi hello veriler toplanır hello sanal makine ile aynı bölgeye, toostore verilerde hello bu sağlar.

-   **Azure Güvenlik Merkezi deposunda**: iş ortağı uyarıları, öneriler ve sistem durumu da dahil olmak üzere güvenlik uyarıları hakkında bilgi merkezi olarak, şu anda hello Amerika Birleşik Devletleri'nde depolanır. Bu bilgiler, ilgili yapılandırma bilgilerini içerebilir ve güvenlik olaylarını sanal makinelerden gerekli tooprovide, ile Merhaba Güvenlik Uyarısı, öneri veya güvenlik sistem durumu toplanır.


## <a name="azure-monitor"></a>Azure İzleyici

Merhaba [OMS güvenlik](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources) ve BT tooactively izlemenize yardımcı olabilecek tüm kaynakları denetim çözümü sağlar, güvenlik olaylarına hello etkisini en aza indirmenize. OMS güvenlik ve denetim kaynakları izlemek için kullanılan güvenlik etki alanları sahiptir. hızlı erişim toooptions Hello güvenlik etki alanı sağlar, güvenliği hello izleme için şu etki alanlarına daha ayrıntılı olarak ele alınmıştır:

-   kötü amaçlı yazılım değerlendirmesi
-   Güncelleştirme değerlendirmesi
-   Kimlik ve erişim.

Azure İzleyicisi işaretçileri tooinformation kaynakları belirli türlerdeki sağlar. Görselleştirme, sorgu, yönlendirme, uyarı, otomatik ölçeklendirme ve Otomasyon verilerden hem hello Azure altyapısı (Etkinlik günlüğü) ve tek tek her Azure kaynak (tanılama günlükleri) sunar.

![Azure İzleyici](./media/azure-operational-security/azure-operational-security-fig6.png)


Bulut uygulamalarını birçok taşıma bölümleriyle karmaşıktır. İzleme, uygulamanızı kurma kalır veri tooensure ve sistem durumu iyi çalışan sağlar. Olası sorunlar kapalı veya olanları sorun giderme, toostave yardımcı olur.

Ayrıca, uygulamanız hakkında izleme verileri toogain ayrıntılı Öngörüler kullanabilirsiniz. Bu bilgi tooimprove uygulama performansı veya bakım yardımcı veya aksi halde el ile müdahale gerektiren Eylemler otomatik hale getirme.

### <a name="azure-activity-log"></a>Azure etkinlik günlüğü


Aboneliğinizi kaynaklarında gerçekleştirilen hello işlemleri hakkında bilgi sağlayan bir günlüktür. Denetim düzlemi olayları aboneliklerinizi için raporları beri hello etkinlik günlüğü daha önce "Denetim günlüklerini" veya "İşlem günlükleri," olarak bilinir.

![Azure etkinlik günlüğü](./media/azure-operational-security/azure-operational-security-fig7.png)

Merhaba etkinlik günlüğü kullanarak hello belirleyebilirsiniz ' ne, kimin, ne zaman ve ' herhangi yazma işlemleri (PUT, POST, DELETE) aboneliğinizde hello kaynaklar üzerinde gerçekleştirilecek için. Merhaba hello işleminin durumunu ve ilgili diğer özellikleri de anlayabilirsiniz. Merhaba etkinlik günlüğü okuma (GET) işlemleri veya hello Klasik modeli kullanan kaynakları işlemlerinde içermez.

### <a name="azure-diagnostic-logs"></a>Azure tanılama günlükleri

Bu günlükler bir kaynak tarafından gösterilen ve bu kaynağın hello işlemi hakkında zengin, sık veriler sağlar. Bu günlükler Merhaba içeriğine kaynak türüne göre değişir.

Örneğin, Windows olayı sistem günlükleri tanılama günlüğünün VM'ler ve blob, tablo için bir kategori, ve sıra günlükleri tanılama günlüklerini kategorileri depolama hesapları için.

Tanılama günlüklerini farklı hello [etkinlik günlüğü (önceki adıyla denetim günlüğü veya işlem günlüğü olarak bilinir)](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs). Merhaba etkinlik günlüğü aboneliğinizde kaynaklara gerçekleştirilen hello işlemleri hakkında bilgi sağlar. Tanılama günlükleri işlemleri kaynağınız kendisini gerçekleştirilen bir anlayış sağlar.

### <a name="metrics"></a>Ölçümler

Azure İzleyicisi tooconsume telemetri toogain görünürlük hello performans ve iş yüklerinizi Azure üzerinde durumunu sağlar. Merhaba en önemli Azure telemetri verilerini (performans sayaçlarını olarak da bilinir) hello ölçümleri çoğu Azure kaynaklar tarafından gösterilen türüdür. Azure İzleyici birkaç yolu tooconfigure sağlar ve bunlar tüketen [ölçümleri](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) izleme ve sorun giderme için. Ölçümleri telemetri değerli bir kaynaktır ve görevleri aşağıdaki toodo hello etkinleştirin:

-   **İzleme hello performans** kendi ölçümleri portal grafik Çizdirmek ve o grafik tooa panoya sabitleme kaynağın (örneğin, bir VM, Web sitesi ya da mantıksal uygulama).

-   **Bir sorun bildirim alma** belirli bir eşiği ölçüm kestiği zaman etkileri kaynağınız performansını hello.

-   **Otomatik eylemler yapılandırma**, bir kaynak ölçekleme veya belirli bir eşiği ölçüm kestiği olduğunda bir runbook tetikleme otomatik gibi.

-   **Gelişmiş analizler gerçekleştirmek** veya kaynağınız performans ya da kullanım eğilimlerini üzerinde raporlama.

-   **Arşiv** hello uyumluluk veya denetim amacıyla bir kaynak performans veya sistem durumu geçmişini.

### <a name="azure-diagnostics"></a>Azure Tanılama

Bunu hello dağıtılan bir uygulama tanılama verilerini hello koleksiyonunu sağlayan Azure içinde bir özelliktir. Çeşitli farklı kaynaklardan hello tanılama uzantısını kullanabilirsiniz. Şu anda desteklenen [Azure bulut hizmeti Web ve çalışan rolleri](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service), [Azure sanal makineleri](https://docs.microsoft.com/azure/virtual-machines/windows/overview) Microsoft Windows çalıştıran ve [Service Fabric](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics). Diğer Azure hizmetleriyle kendi ayrı tanılama vardır.

## <a name="azure-network-watcher"></a>Azure Ağ İzleyicisi

Ağınızda güvenlik denetimi, ağ güvenlik açıklarını algılama ve BT güvenliği ve Mevzuat idare modeli ile uyumluluğu sağlamak için önemlidir. Güvenlik grubu görünümü ile yapılandırılmış hello ağ güvenlik grubu ve güvenlik kuralları alabilir ve etkili güvenlik kuralları hello. Uygulanacak kurallar Hello listesiyle, açık olan ve ağ güvenlik açığı değerlendirmek hello bağlantı noktaları belirleyebilirsiniz.

[Ağ İzleyicisi](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) bir ağ düzeyinde içinde için ve azure'dan koşullar tanılamak ve toomonitor sağlayan bölgesel bir hizmettir. Ağ Tanılama ve görselleştirme Ağ İzleyicisi ile kullanılabilen araçlar anlamak, tanılama ve Öngörüler tooyour Azure ağında geçirmesine yardımcı olur. Bu hizmet içeren paket yakalama, sonraki atlama IP akış, güvenlik grubu görünümü, NSG akış günlükleri doğrulayın. Senaryo düzeyi izleme Karşıtlık tooindividual ağ kaynak izleme ağ kaynaklarına bir uçtan tooend görünümünü sağlar.

![Azure Ağ İzleyicisi](./media/azure-operational-security/azure-operational-security-fig8.png)

Ağ İzleyicisi'ni şu anda özellikleri aşağıdaki hello sahiptir:

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview">Denetim günlükleri</a>**-ağların hello yapılandırmasının bir parçası gerçekleştirilen işlemleri günlüğe kaydedilir. Bu günlükler hello Azure portal görüntülenebilir veya Power BI gibi Microsoft araçları veya üçüncü taraf araçlarını kullanarak alınamıyor. Denetim günlüklerini hello portal, PowerShell'i, CLI ve Rest API kullanılabilir. Denetim günlükleri hakkında daha fazla bilgi için denetim işlemleri Resource Manager ile bakın. Denetim günlükleri, tüm ağ kaynaklarına yapılan işlemleri için kullanılabilir.


-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview">IP akış doğrular </a>**  -paket izin verilen veya reddedilen denetimleri temel akış bilgi 5-tanımlama grubu paket parametrelerine (hedef IP, kaynak IP, hedef bağlantı noktası, kaynak bağlantı noktası ve protokol). Başlangıç paketi bir ağ güvenlik grubu tarafından engellenirse hello kuralı ve hello Paket reddedildi ağ güvenlik grubu döndürülür.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview">Sonraki atlama</a>**  -hello toodiagnose herhangi yanlış yapılandırılmış kullanıcı tanımlı yollar etkinleştirme Azure ağ yapısında yönlendirilen paketler için sonraki atlama hello belirler.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview">Güvenlik grubu görünümü</a>**  -bir VM üzerinde uygulanan hello etkili ve uygulanan güvenlik kuralları alır.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview">NSG akış günlük</a>**  -akış günlükleri ağ güvenlik grupları için izin verilen veya hello Grup hello güvenlik kuralları tarafından reddedilen toocapture günlükleri ilgili tootraffic sağlar. Merhaba akışı bir 5-tanımlama grubu bilgileriyle – kaynak IP, hedef IP, kaynak bağlantı noktası, hedef bağlantı noktası ve protokol tanımlanır.

## <a name="azure-storage-analytics"></a>Azure Depolama Analizi

[Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) istekleri tooa depolama hizmeti hakkında toplu işlem istatistiklerini ve kapasite verilerini dahil ölçümleri depolayabilirsiniz. İşlemler her iki hello API işlemi düzeyinde ve hello depolama hizmeti düzeyinde bildirilir ve kapasite hello depolama hizmet düzeyinde bildirilir. Ölçüm verilerini kullanılan tooanalyze depolama hizmeti kullanım olması, hello depolama hizmeti ve tooimprove hello bir hizmeti kullanan uygulamaların performansını karşı yapılan istekleri ile sorunları tanılayın.

[Azure Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) günlüğe kaydetme işlemlerini gerçekleştiren ve ölçümler veriler için bir depolama hesabı sağlar. Bu veri tootrace istekleri kullanır, kullanım eğilimleri çözümlemek ve depolama hesabınızla sorunlarını tanılamak. Storage Analytics günlük Merhaba kullanılabilir [Blob, kuyruk ve tablo hizmetlerine](https://docs.microsoft.com/azure/storage/storage-introduction). Storage Analytics başarılı ve başarısız istekleri tooa depolama birimi hizmeti hakkındaki ayrıntılı bilgileri kaydeder.

Bu bilgiler kullanılan toomonitor istekleri ayrı ayrı ve depolama hizmeti toodiagnose sorunları olabilir. İstekleri en iyi çaba ilkesine göre günlüğe kaydedilir. Merhaba Hizmeti uç noktası karşı yapılan istekleri varsa günlük girişleri oluşturulur. Bir depolama hesabı Blob uç ancak kendi tablo veya kuyruğu uç noktaları etkinlik varsa ilgili örnek yalnızca günlükleri için toohello Blob hizmeti oluşturulur.

Storage Analytics toouse etkinleştirmeniz gerekir, tek tek her hizmet için toomonitor istediğiniz. Hello etkinleştirmek [Azure portal](https://portal.azure.com/); Ayrıntılar için bkz: [hello Azure portalında bir depolama hesabını izleme](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account). Storage Analytics hello REST API aracılığıyla programlı olarak veya hello istemci kitaplığı da etkinleştirebilirsiniz. Merhaba hizmet özelliklerini ayarlama işlemi tooenable Storage Analytics her hizmet için ayrı ayrı kullanın.

Merhaba toplanan veriler (günlük için) iyi bilinen bir blob ve hello Blob hizmeti ve tablo hizmeti API'leri kullanılarak erişilebilecek (için ölçümleri), iyi bilinen tablolara depolanır.

Storage Analytics bir 20-TB hello depolama hesabınız için toplam sınırı hello bağımsızdır depolanan veri miktarına sahiptir. Tüm günlükler depolanmış [blok blobları](https://docs.microsoft.com/azure/storage/storage-analytics) $logs adlı bir kapsayıcıda, otomatik olarak oluşturulan depolama çözümlemeleri için bir depolama hesabı etkin olduğunda.

Storage Analytics tarafından gerçekleştirilen eylemler şu hello Faturalanabilir şunlardır:

-   Günlük için istekleri toocreate BLOB'ları
-   Ölçümler için istekleri toocreate tablo varlıklar.

> [!Note]
> Faturalama ve veri bekletme ilkeleri hakkında daha fazla bilgi için bkz: [depolama çözümlemeleri ve faturalama](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-and-billing).
> En iyi performans için yüksek oranda kullanılan disk toolimit hello sayısı toohello sanal makine tooavoid olası azaltma bağlı istiyorsunuz. Tüm diskleri yüksek oranda hello sırasında kullanılan değil, aynı anda hello depolama hesabı, daha büyük bir sayı disk destekleyebilir.

> [!Note]
> Depolama hesabı sınırları hakkında daha fazla bilgi için bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](https://docs.microsoft.com/azure/storage/storage-scalability-targets).


Kimliği doğrulanmış ve anonim istek türlerini aşağıdaki hello günlüğe kaydedilir.

| Kimlik doğrulaması  | Anonim|
| :------------- | :-------------|
| Başarılı istekler | Başarılı istekler |
|İstek zaman aşımı, azaltma, ağ, yetkilendirme ve başka hatalar da dahil olmak üzere, başarısız oldu | Başarılı ve başarısız istekleri dahil olmak üzere paylaşılan erişim imzası (SAS), kullanarak istekleri |
| Başarılı ve başarısız istekleri dahil olmak üzere paylaşılan erişim imzası (SAS), kullanarak istekleri |İstemci ve sunucu zaman aşımı hataları |
|   İstekleri tooanalytics veri |    304 (değişiklik) hata koduyla başarısız olan GET istekleri |
| Storage Analytics kendisini günlük oluşturma veya silme gibi tarafından yapılan istekleri günlüğe kaydedilmez. Oturum hello verilerin tam bir liste hello belgelenen [depolama Analytics günlüğe yazılan işlemler ve durum iletileri](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) ve [depolama Analytics günlük biçimi](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format) Konular. | Diğer tüm başarısız anonim istekler günlüğe kaydedilmez. Oturum hello verilerin tam bir liste hello belgelenen [depolama Analytics günlüğe yazılan işlemler ve durum iletileri](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) ve [depolama Analytics günlük biçimi](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format). |
## <a name="azure-active-directory"></a>Azure Active Directory

Azure AD kimlik yönetimi özelliklerini çok faktörlü kimlik doğrulaması, cihaz kaydı, Self Servis parola yönetimi, Self Servis Grup Yönetimi, ayrıcalıklı hesap yönetimi, rol tabanlı erişim dahil olmak üzere, tam bir paketi de içerir. Denetim, uygulama kullanımını izleme, zengin denetim ve güvenlik izleme ve uyarı.

-   Azure AD çok faktörlü kimlik doğrulama ve koşullu erişim ile uygulama güvenliği artırır.

-   Uygulama kullanımını izlemek ve işletmenizi raporlama ve izleme güvenliğiyle Gelişmiş tehditlere karşı koruyun.

Azure Active Directory (Azure AD), dizininize yönelik güvenlik, etkinlik ve denetim raporlarını içerir. [Hello Azure Active Directory denetim raporu](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) , müşterilerin kendi Azure Active Directory'de oluştu tooidentify ayrıcalıklı Eylemler yardımcı olur. Ayrıcalıklı Eylemler dahil ayrıcalık değişiklikler (örneğin, rolü oluşturma veya parola sıfırlama) ilkesi yapılandırmaları (örneğin, parola ilkelerinin) veya değişiklikleri toodirectory yapılandırması (örneğin, değişiklikleri toodomain Federasyon ayarları) değiştirme.

Merhaba raporları hello denetim kaydı hello olay adı, hello eylemin hello değişiklik ve hello tarih ve saat (UTC içinde) etkilenen hello hedef kaynak gerçekleştiren hello aktör sağlar. Müşterilerdir mümkün tooretrieve hello hello aracılığıyla kendi Azure Active Directory için denetim olayları listesini [Azure portal](https://portal.azure.com/)açıklandığı gibi [denetim günlüklerini görüntülemek](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal). Dahil hello raporları listesi aşağıdadır:

| Güvenlik raporları  | Etkinlik raporları| Denetim raporları |
| :------------- | :-------------| :-------------|
|Bilinmeyen kaynaklardan gerçekleştirilen oturum açma işlemleri | Uygulama kullanımı: özet | Dizin denetimi raporu |
|Birden çok hatadan sonra gerçekleştirilen oturum açma işlemleri | Uygulama kullanımı: ayrıntılı |   |
|Birden çok coğrafyadan gerçekleştirilen oturum açma işlemleri | Uygulama panosu |  |
|Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum açma işlemleri |Hesap hazırlama hataları |  |
|Düzensiz oturum açma etkinliği |Bireysel kullanıcı cihazları |  |
|Muhtemelen virüs bulaşmış cihazlardan gerçekleştirilen oturum açma işlemleri |Bireysel kullanıcı Etkinliği |   |
|Anormal oturum açma etkinliği gösteren kullanıcılar |Grup etkinlik raporu |   |
| |Parola Sıfırlama Kayıt Etkinlik Raporu |   |
| |Parola sıfırlama etkinliği |   | |



Bu raporların Hello veriler SIEM sistemlerinden, Denetim ve iş zekası araçları gibi yararlı tooyour uygulamalar olabilir. Hello Azure AD raporlama [API'leri](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started) bir dizi REST tabanlı API'ler aracılığıyla programlı erişim toohello veriler sağlar. Bu API'leri çeşitli programlama dilleri ve Araçlar menüsünden çağırabilirsiniz.

Hello Azure AD Denetim Raporu olayları 180 gün boyunca saklanır.

> [!Note]
> Raporlarda bekletme hakkında daha fazla bilgi için bkz: [Azure Active Directory rapor bekletme ilkeleri](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention).

Müşteriler depolanırken ilgilenen kendi [olaylarını denetleme](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-audit-events) daha uzun bekletme dönemleri hello raporlama API'si kullanılan tooregularly çekme denetim olayları ayrı veri deposuna olabilir.

## <a name="summary"></a>Özet

Bu makale özetleri gizliliğinizi korumaya ve yazılım ve yardımcı hizmetleri sunarken, verilerinizi güvenli hale getirme Merhaba, kuruluşunuzun BT altyapısı yönetin. Microsoft, kendi veri tooothers güvenilen bu güven sıkı güvenlik gerektiren tanır. Microsoft aynılarını toostrict uyumluluk ve güvenlik yönergelerine — toooperating hizmet kodlama gelen. Güvenli hale getirme ve verileri koruma Microsoft'taki önceliğe sahiptir.

Bu makalede açıklanır

-   Nasıl veri toplanan, işlenen ve hello Operations Management Suite (OMS) güvenli.

-   Birden çok veri kaynağında olayları hızla çözümleyin. Güvenlik risklerini belirlemeniz ve hello kapsamını ve güvenliği ihlal toomitigate hello zarar Tehditler ve saldırıların etkisini anlayın.

-   Giden kötü amaçlı IP trafiğini ve kötü amaçlı tehdit türlerini görselleştirerek saldırı desenlerini tanımlayın. Merhaba güvenlik tutumunu platformdan bağımsız olarak tüm ortamınızın anlayın.

-   Güvenlik ve uyumluluk denetimi için gerekli tüm hello günlüğü ve olay verilerini yakalama. Eğik çizgi hello zaman ve kaynak bir güvenlik denetim tamamlandı, aranabilir ve dışarı aktarılabilir günlüğü ve olay veri kümesi ile toosupply gerekli.

<ul>
<li>Güvenlikle ilgili olayları, Denetim ve tookeep bir kapatma göz varlıklarınızı ihlali analiz Topla:</li>
<ul>
<li>Güvenlik yaklaşımı</li>
<li>Önemli sorun</li>
<li>Özetleri tehditleri</li>
</ul>
</ul>

## <a name="next-steps"></a>Sonraki Adımlar

- [Tasarım ve işlem güvenliği](https://www.microsoft.com/trustcenter/security/designopsecurity)

Microsoft hizmetlerinin tasarlayan ve yazılım göz toohelp güvenlik ile bulut altyapısı esnek ve saldırılara karşı korunuyor olduğundan emin olun.

- [Operations Management Suite | Güvenlik ve uyumluluk](https://www.microsoft.com/cloud-platform/security-and-compliance)

Microsoft güvenlik veri ve analiz tooperform daha akıllı ve etkili kullanmak tehdit algılama.

- [Azure Güvenlik Merkezi planlama ve işlemler](https://docs.microsoft.com/azure/security-center/security-center-planning-and-operations-guide) adımları ve Güvenlik Merkezi kullanımınızı tabanlı kuruluşunuzun güvenlik gereksinimlerine ve bulut Yönetimi modeline toooptimize izleyebileceğiniz bir dizi.

