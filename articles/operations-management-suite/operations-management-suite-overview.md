---
title: "aaaOperations Yönetim Paketi (OMS) genel bakış | Microsoft Docs"
description: "Microsoft Operations Management Suite (OMS), şirket içi ve bulut altyapınızı yönetmenize ve korumanıza yardımcı olan, Microsoft'un bulut tabanlı BT yönetim çözümüdür.  Bu makalede OMS hello değeri, hello farklı Hizmetleri ve OMS dahil teklifleri tanımlar ve bağlantılar sağlar tootheir ayrıntılı içerik."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: bwren
ms.openlocfilehash: ec3fe6d82aec46d1f715a4338f126e79e04a9147
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-operations-management-suite-oms"></a>Operations Management Suite (OMS) nedir?
Bu makalede bir giriş tooOperations Yönetim Paketi (OMS) dahil olmak üzere sağladığı hello iş değeri, içerdiği hello Hizmetleri ve yönetim çözümleri ve birlikte farklı paketleme hello teklifleri kısa bir genel bakış sağlar ve çözümleri.  Bağlantılar dahil toohello ayrıntılı dağıtma ve her bir hizmet ve çözüm kullanarak belgeleri.

## <a name="from-on-premises-toohello-cloud"></a>Şirket içi toohello buluttan
Microsoft, uzun bir süredir kurumsal ortamların yönetilmesine yönelik ürünler sağlıyor.  Birden fazla ürün 2007'de yönetim ürünlerinin System Center paketine hello birleştirilmiş.  Bu yazılım dağıtımı ve envanter, proaktif sistemleri ve uygulamaların, izleme runbook'lar tooautomate el ile işlemler içeren Orchestrator sağlayan bir Operations Manager gibi özellikler sağlayan bir Configuration Manager dahil ve Data Protection Manager yedekleme ve kurtarma, kritik verilerin.

Toohello bulut taşıyarak daha fazla bilgi işlem kaynakları ile System Center ürünleri Operations Manager ve Azure kaynaklarında yönetme Orchestrator gibi daha fazla bulut özellikleri kazanılan.  Ne var ki bunlar hâlâ özünde şirket içi çözümler olarak tasarlanıyordu ve şirket içi yönetim ortamında dağıtılıp bakımlarının yapılabilmesi için ciddi bir yatırım gerekiyordu.  toocompletely gelecekteki destek ve yararlanın hello bulut uygulamaları, yeni bir yaklaşım toomanagement gerekli.

## <a name="introducing-operations-management-suite"></a>Operations Management Suite’e Giriş
Operations Management Suite (OMS olarak da bilinir) hello başından hello bulutta tasarlanmış Yönetim Hizmetleri koleksiyonudur.  Şirket içinde dağıtılması ve yönetilmesi gereken kaynakların aksine, OMS bileşenleri tamamen Azure'da barındırılır.  Çok az yapılandırma gerektirir ve yalnızca birkaç dakikada kullanmaya başlayabilirsiniz.  

- **En az maliyet ve dağıtım karmaşıklığı.**  Tüm hello bileşenleri ve OMS verileri Azure'da depolandığından yukarı olabilir ve hello karmaşıklık ve yatırım olmadan kısa bir süre içinde çalışan bileşenleri şirket.
- **Ölçek toocloud düzeyleri.**  Gerekmeyen işlem kaynaklarını ödeme hakkında tooworry yoksa veya bu yana hello depolama alanının tükenmesinden hakkında bulut neleri gerçekte kullanın ve ihtiyaç duyduğunuz tooany yük taşımalarına ölçeklenir için yalnızca toopay sağlar.  Başlatılan birkaç kaynakları tooget yöneterek başlatın ve tooyour tüm ortamını ölçeklendirin.
- **Merhaba en son özelliklerden yararlanabilir.**  OMS hizmetlerine sürekli yeni özellikler eklenir ve mevcut özellikler güncelleştirilir.  Sürekli erişim toohello en son özellikleri herhangi bir gereksinimi toodeploy güncelleştirme olmadan var.
- **Tümleşik hizmetler.**  Merhaba OMS hizmetlerinin her biri sunarken önemli değeri, kendi, bunlar toosolve karmaşık yönetim senaryoları birlikte çalışabilir.  Örneğin, Azure Automation runbook bir Azure Site Recovery ile yük devretme işlemi sürücü ve bilgi tooLog Analytics toogenerate bir uyarı oturum açın.
- **Küresel bilgi.**  OMS yönetim çözümlerine sürekli erişim toohello en son bilgilere sahip.  Merhaba güvenlik ve denetim çözümü, örneğin, hello en son tehditler Merhaba Dünya algılanan kullanarak bir tehdit analizi gerçekleştirebilir.
- **Her yerden erişim.**  Yönetim ortamınıza bir tarayıcı kullanabileceğiniz her yerden erişin.  Smartphone için hazır erişim tooyour izleme verilerini Hello OMS uygulama yükleyin.

### <a name="is-it-just-for-hello-cloud"></a>Yalnızca hello bulut için mi?
Yalnızca OMS hizmetlerini çalıştırmak için hello bulut bunlar etkili bir şekilde şirket içi ortamınız yönetemez anlamına gelmez.  Bir aracı üzerinde herhangi bir Windows put veya Linux bilgisayarı veri merkezinizi ve bunu diğer verilerle birlikte burada çözümlenebilir Analytics Bulut veya şirket içi Hizmetleri'nden toplanan verileri tooLog gönderir.  Şirket içi kaynakları için yedekleme ve yüksek kullanılabilirlik için Azure Backup ve Azure Site Recovery tooleverage hello bulut kullanın.  
Runbook'ları hello bulutta şirket içi kaynaklarınıza genellikle erişemiyor, ancak bir veya daha fazla bilgisayara bir aracı yükleyebilirsiniz çok barındıracak runbook'ları veri merkezinizdeki.  Bir runbook'u başlattığınızda, yalnızca toorun hello bulutta veya yerel bir çalışan üzerinde istediğinizi belirtin.

## <a name="hybrid-management-with-system-center"></a>System Center ile karma yönetim
System Center olan bir yüklemesini varsa, bu bileşenlerin her iki şirket içi için OMS Hizmetleri tooprovide karma bir çözüm tümleştirmek ve her ürünün hello göreli uzmanlık alanları yararlanarak ortamları bulut.  Var olan Operations Manager yönetim grubu tooLog Analytics yönetilen tooanalyze aracılarınızı hello bulutta bağlayın.  Var olan yedekleme işleminize Data Protection Manager toobackup ile veri toohello bulut kullanın.  


## <a name="oms-services"></a>OMS hizmetleri
OMS Hello çekirdek işlevselliğini Azure üzerinde çalışan hizmetleri kümesi tarafından sağlanır.  Her hizmet belirli yönetim işlevi sağlar ve Hizmetleri tooachieve farklı yönetim senaryoları birleştirebilirsiniz.

|| Hizmet | Açıklama |
|:--|:--|:--|
| ![Log Analytics](media/operations-management-suite-overview/icon-log-analytics.png) | Log Analytics | İzleme ve hello kullanılabilirlik ve fiziksel gibi farklı kaynaklarına ve sanal makineleri performansını analiz edin. |
| ![Azure Otomasyonu](media/operations-management-suite-overview/icon-automation.png) | Automation | El ile gerçekleştirilen işlemleri otomatikleştirin; fiziksel ve sanal makinelere yapılandırma uygulayın. |
| ![Azure Backup](media/operations-management-suite-overview/icon-backup.png) | Backup | Kritik verileri yedekleyin ve geri yükleyin. |
| ![Azure Site Recovery](media/operations-management-suite-overview/icon-site-recovery.png) | Site Recovery | Kritik uygulamalar için yüksek kullanılabilirlik sağlayın. |

### <a name="log-analytics"></a>Log Analytics
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics), yönetilen kaynaklardan toplanan verileri merkezi bir depoda birleştirerek OMS için izleme hizmetleri sağlar.  Bu veriler, olayları, performans verileri veya hello API sağlanan özel verileri içerebilir. Toplandığında, hello veri uyarı, analiz ve dışarı aktarma için kullanılabilir.  Mevcut şirket içi ortamınız ile Azure hizmetlerinden verileri birleştirebilirsiniz şekilde bu yöntem, çeşitli kaynaklardan tooconsolidate verileri sağlar.  Aynı zamanda açıkça hello hello veri koleksiyonunu tüm eylemleri kullanılabilir tooall veri türlerini; böylece bu veriler üzerinde gerçekleştirilecek hello eylemden ayırır.  

![Log Analytics’e genel bakış](media/operations-management-suite-overview/overview-log-analytics.png)

#### <a name="collecting-data"></a>Verileri toplama
Çeşitli günlük analizi tooanalyze hello havuzunda Veri Al şekillerde vardır.

- **Windows veya Linux bilgisayarları ve sanal makineler.**  Merhaba Microsoft izleme aracısı yüklemek [Windows](../log-analytics/log-analytics-windows-agents.md) ve [Linux](../log-analytics/log-analytics-linux-agents.md) bilgisayarlar ya da toocollect verileri istediğiniz sanal makineleri.  Merhaba aracısı olayları ve performans verileri toocollect tanımlar günlük analizi yapılandırmasından otomatik olarak indirir.  Kolayca, hello Aracısı hello Azure portal kullanarak Azure'da çalışan sanal makinelere yükleyebilirsiniz.  Varolan bir Operations Manager ortamınız varsa, hello yönetim grubu tooLog Analytics bağlanın ve tüm mevcut aracılardan veri toplama otomatik olarak başlat.
- **Azure hizmetleri.**  Günlük analizi toplar telemetrisinden [Azure tanılama ve Azure Monitoring](../log-analytics/log-analytics-azure-storage.md) hello havuzunda böylece Azure kaynaklarını izleyebilirsiniz.
- **Veri Toplayıcı API’si**  Log Analytics, [tüm istemcilerden toplanan verilerin doldurulması için bir REST API](../log-analytics/log-analytics-data-collector-api.md) içerir.  Bu, üçüncü taraf uygulamalardan toocollect veri izin verir veya özel yönetim senaryolarını uygulayan.  Bir ortak yöntemi toouse bir Azure Otomasyonu toocollect veri runbook'ta ve hello veri toplayıcı API toowrite kullanın, toohello deposu.

#### <a name="reporting-and-analyzing-data"></a>Raporlama ve veri analizi
Günlük analizi hello deposunda bulunan güçlü sorgu dili tooextract verileri içerir.  Tüm kaynaklardan toplanan veriler kayıt olarak depolandığından, birden çok kaynaktan gelen verileri tek bir sorguda analiz edebilirsiniz.
  
Ayrıca tooad anlık analiz, günlük analizi birden çok yol tooreport sağlar ve bir sorgu verileri analiz edin.

- **Görünümler ve panolar.**  [Görünümler](../log-analytics/log-analytics-view-designer.md) ve [panolar](../log-analytics/log-analytics-dashboards.md) hello hello Portalı'nda bir sorgunun sonuçlarını görselleştirin.  Yönetim çözümleri genellikle hello çözümden hello verileri çözümlemek görünümleri içerir.  Ayrıca, kendi özel görünümlerinizi tooanalyze veri oluşturabilir ve özel portalınızın kullanıma hazır olun.
- **Dışarı aktarın.**  Böylece günlük analizi dışında çözümleyebilirsiniz hello seçeneği tooexport hello herhangi bir sorgu sonuçlarını sahip.  Normal verme çok bile zamanlama[Power BI](../log-analytics/log-analytics-powerbi.md) önemli Görselleştirme ve analiz özellikleri sağlar.
- **Günlük Arama API’si.**  Log Analytics, [tüm istemcilerden veri toplanması için bir REST API](../log-analytics/log-analytics-log-search-api.md) içerir.  Bu hello deposunda toplanan verilerle tooprogrammatically iş izin verir veya başka bir izleme aracından erişim.

#### <a name="alerting"></a>Uyarı
Log Analytics bir sorun algıladığında sizi [proaktif olarak uyarabilir](../log-analytics/log-analytics-alerts.md) veya düzeltici bir eylem uygulayabilir.  Log Analytics’teki diğer tüm analizler gibi bu işlem de bir günlük aramasıyla gerçekleştirilir.  Bu arama düzenli bir zamanlamaya göre çalışır ve hello sonuçları belirli ölçütlere uyan varsa bir uyarı oluşturulur.

![Log Analytics uyarıları](media/operations-management-suite-overview/overview-alerts.png)

Ayrıca toocreating hello günlük analizi deposundaki bir uyarı kaydı, aşağıdaki eylemler hello uyarıları alabilir.

- **E-posta gönderme.**  Bir e-posta Gönder tooproactively algılanan bir sorun bildirin.
- **Runbook.**  Log Analytics’teki bir uyarı, Azure Otomasyonu’ndaki bir runbook’u başlatabilir.  Bu, genellikle tooattempt toocorrect hello Algılanan Sorun gerçekleştirilir.  Merhaba runbook başlatılabilir hello hello bulutta Azure veya başka bir bulut ya da bir sorunu durumunun bir fiziksel veya sanal makinede bir sorun için yerel bir aracı üzerinde başlatılamadı.
- **Web kancası.**  Bir uyarı, bir Web kancası başlatın ve hello hello günlük Arama sonuçlarından veri iletmek.  Bu alternatif bir uyarı sistem gibi dış hizmetler ile entegrasyon sağlar veya bir dış web sitesi için düzeltme eylemi tootake deneyebilir.

### <a name="azure-automation"></a>Azure Otomasyonu
[Azure Otomasyonu](http://azure.microsoft.com/documentation/services/automation) işlem Otomasyonu ve yapılandırma yönetimi tooOMS sağlar.  El ile süreçlerini otomatikleştirir ve fiziksel ve sanal bilgisayarlar için tooenforce yapılandırmaları yardımcı olur.  

#### <a name="process-automation"></a>Süreç Otomasyonu
Azure Otomasyonu, PowerShell betiğini ya da PowerShell iş akışını temel alan [runbook](../automation/automation-runbook-types.md)'ları kullanarak el ile gerçekleştirilen işlemleri otomatikleştirir.  Ayrıca, runbook'ları gibi birden çok runbook'ları ve kimlik bilgilerini ve runbook kimlik doğrulaması için gerekli olabilecek şifrelenmiş toostore bilgi olanak tanıyan bağlantıları arasında paylaşılan değişkenleri destekleyen varlıkları içerir.
Runbook'ları hello için işlem Otomasyonu hello grubundaki diğer hizmetleri sunar.  Her hello itibaren diğer hizmetler erişilebilir PowerShell ile ya da bir REST API'si aracılığıyla Azure yedekleme ile bir yedekleme başlatmak veya günlük analizi yönetim verileri toplamak olarak bu tür işlevler runbook'ları tooperform oluşturabilirsiniz.

##### <a name="accessing-resources"></a>Kaynaklara erişme
Runbook’lar PowerShell’i temel aldığından, PowerShell cmdlet’leriyle erişilebilen tüm kaynakları yönetebilir.  Olduğunda, [bir modülü](../automation/automation-integration-modules.md) isteğe bağlı olarak Otomasyon hesabınızda o hesabı kullanılabilir tooall runbook'larda olur. 
 
Runbook'lar hello bulutta çalıştırdığınızda, bunlar hello buluttan erişilebilen herhangi bir kaynağa erişebilir.  Bu kaynaklara örnek olarak Azure aboneliğinizdeki kaynaklar, Amazon Web Services (AWS) gibi başka bir buluttaki kaynaklar ya da bir REST API aracılığıyla erişilebilen bir hizmet verilebilir.  Runbook'ları hello bulutta altında herhangi bir kimlik bilgisi çalıştırma, ancak kimlik bilgileri, bağlantıları ve sertifikaları tooauthenticate tooresources eriştiklerinde gibi Otomasyon varlıkları yararlanabilirsiniz.

Veri merkezinizdeki kaynaklarına büyük olasılıkla hello bulutta çalışan bir runbook'tan erişilemez.  Bir veya daha fazla yükleyebilirsiniz [karma Runbook çalışanları](../automation/automation-hybrid-runbook-worker.md) verilerinizi ancak toolocal kaynaklarına erişim gerektiren toorun runbook'ları Merkezi.  Bir runbook'u başlattığınızda bu hello bulutta ya da belirli bir çalışan üzerinde çalıştırılması gerekip gerekmediğini belirtin.

![Azure Otomasyonu runbook’ları](media/operations-management-suite-overview/overview-runbooks.png)

##### <a name="starting-a-runbook"></a>Runbook başlatma
Runbook’lar, çeşitli yönetim senaryolarına dahil edilebilmeleri için [farklı metotlarla başlatılabilir](../automation/automation-starting-a-runbook.md).  

- **Azure Portal.**  Diğer Azure hizmetleriyle gibi Azure Otomasyonu hello Azure Portalı ' yönetilebilir.  Ayrıca toostarting runbook'ları, bunları içeri aktarabilir veya kendi yazar.
- **Zamanlananlar.**  Runbook'ları toostart düzenli aralıklarla zamanlayabilirsiniz.  Bu, tooautomatically yineleme normal yönetim işlemi veya veri toplama tooLog analizi sağlar.
- **PowerShell ve API.**  Azure Otomasyonu REST API hello veya runbook'ları ve PowerShell cmdlet'ini parametre bilgileri gerekli geçişi başlatabilirsiniz.  
- **Web kancası.**  Bir Web kancası veren herhangi bir runbook için oluşturulabilir toobe dış uygulamaları veya web siteleri başlatıldı.
- **Log Analytics Uyarısı.**  Günlük analizi bir uyarıda hello uyarı tarafından tanımlanan bir runbook tooattempt toocorrect hello sorunun otomatik olarak başlatabilirsiniz.

#### <a name="configuration-management"></a>Yapılandırma Yönetimi
[PowerShell istenen durum yapılandırması (DSC)](../automation/automation-dsc-overview.md) toodeploy sağlar ve hello yapılandırma fiziksel ve sanal makineleri zorunlu Windows PowerShell'in bir yönetim platformudur.  Azure Otomasyonu DSC yapılandırmaları yönetir ve çekme sunucu hello bulutta aracıları tooretrieve gerekli yapılandırmaları erişebilmesini sağlar.

![Azure Automation DSC](media/operations-management-suite-overview/overview-dsc.png)

### <a name="azure-backup-and-azure-site-recovery"></a>Azure Backup ve Azure Site Recovery
Azure Backup ve Azure Site Recovery toobusiness devamlılığı ve olağanüstü durum kurtarma katkıda.  Her uygulama kesintiler meydana ve sistemler tekrar çevrimiçi olduğunda toonormal işlemleri iade ettiğinde kullanılabilir kalmasını tooensure yardımcı olan özellikler vardır.  Her iki hizmet katkıda bulunan toohello kurtarma noktası hedefi (RPO'lar) ve kuruluşunuz için tanımlanan kurtarma zamanı hedeflerine (Rto'lar). Merhaba kabul edilebilir sınırı içinde veri kullanılamaz kesinti sırasında RPO tanımlar ve hello RTO sınırlar hello kabul edilebilir süreyi, bir hizmet veya uygulama kesinti sırasında kullanılamaz.

#### <a name="azure-backup"></a>Azure Backup
[Azure Backup](http://azure.microsoft.com/documentation/services/backup), OMS için veri yedekleme ve geri yükleme hizmetleri sağlar.  Uygulama verilerinizi korur ve herhangi bir sermaye yatırımı olmadan en düşük işletim giderleriyle yıllar boyunca saklar.  Veri toplama tooapplication iş yükleri SQL Server ve SharePoint gibi fiziksel ve sanal Windows Server yedekleme yapabilir.  Bu aynı zamanda System Center Data Protection Manager (DPM) korumalı tooreplicate veri tooAzure tarafından artıklık ve uzun vadeli depolama için kullanılabilir.

Azure Backup'ta korunan veriler belirli bir coğrafi bölgede yer alan bir yedekleme kasasında depolanır. Merhaba veri çoğaltıldığında içinde hello aynı bölgede ve, kasa hello türüne bağlı olarak, ayrıca çoğaltılmış tooanother bölge daha fazla esneklik için olabilir.

Azure Backup için üç temel senaryo söz konusudur.

- **Azure Backup aracısının yüklediği Windows makinesi.** Yedekleme dosyaları ve klasörleri herhangi bir Windows server ya da istemci doğrudan tooyour Azure yedekleme kasası.<br><br>![Azure Backup aracısının yüklediği Windows makinesi](media/operations-management-suite-overview/overview-backup-01.png)
- **System Center Data Protection Manager (DPM) veya Microsoft Azure Backup Sunucusu.** Azure yedekleme kasası tooyour çoğaltmak ve DPM veya Microsoft Azure yedekleme sunucusu toobackup dosya ve klasörleri SQL ve SharePoint toolocal depolama gibi ek tooapplication iş yüklerinin yararlanın. Hyper-V veya VMware’de Windows ve Linux sanal makinelerini destekler.<br><br>![System Center Data Protection Manager (DPM) veya Microsoft Azure Backup Sunucusu](media/operations-management-suite-overview/overview-backup-02.png)
- **Azure Sanal Makine Uzantıları.** Yedekleme Windows veya Linux sanal içinde Azure tooyour Azure yedekleme kasası makineleri.<br><br>![Azure Sanal Makine Uzantıları](media/operations-management-suite-overview/overview-backup-03.png)



#### <a name="azure-site-recovery"></a>Azure Site Recovery
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) çoğaltma, şirket içi sanal ve fiziksel makineler tooAzure veya tooa ikincil site düzenleyerek iş sürekliliği sağlar. Birincil site kullanılamıyorsa, böylece kullanıcılar çalışma tutun ve geri sistemleri tooworking sipariş döndüğünüzde başarısız toohello ikincil konum başarısız. 

Azure Site Recovery, sunucular ve uygulamalar için yüksek kullanılabilirlik sağlar.  Bu tooyour iş devamlılığı ve olağanüstü durum kurtarma (BCDR) stratejinize çoğaltma, yük devretme ve kurtarma şirket içi Hyper-V sanal makineleri, VMware sanal makineleri ve fiziksel Windows/Linux sunucuları düzenleyerek katkıda bulunur. Makineler tooa ikincil veri merkezine çoğaltma veya tooAzure çoğaltarak, veri merkezinizdeki genişletin. Site Recovery aynı zamanda iş yükleri için basit bir yük devretme ve kurtarma işlevi sunar. SQL Server AlwaysOn gibi olağanüstü durum kurtarma mekanizmaları ile tümleştirilir ve birden çok makinede katmanlı halde bulunan iş yüklerine yönelik kolay bir yük devretme işlemi için kurtarma planları sağlar.

Azure Site Recovery için üç temel çoğaltma senaryosu söz konusudur.

- **Hyper-V sanal makinelerini çoğaltma.**  VMM bulutlarındaki Hyper-V sanal makineleri yönetiliyorsa tooa ikincil veri merkezi veya tooAzure depolama çoğaltabilirsiniz. Çoğaltma tooAzure güvenli bir internet bağlantısıdır. Çoğaltma tooa ikincil veri merkezine hello LAN ' dir.  Hyper-V sanal makineleri VMM tarafından yönetilmeyen, yalnızca tooAzure depolama çoğaltabilirsiniz. Çoğaltma tooAzure güvenli bir internet bağlantısıdır.<br><br>![Hyper-V sanal makinelerini çoğaltma](media/operations-management-suite-overview/overview-siterecovery-hyperv.png)
- **VMware sanal makinelerini çoğaltma.**  VMware veya tooAzure depolama çalıştıran VMware sanal makineleri tooa ikincil veri merkezine çoğaltabilirsiniz. Çoğaltma tooAzure bir siteden siteye VPN veya Azure ExpressRoute veya güvenli bir Internet bağlantısı üzerinden oluşabilir. Çoğaltma tooa ikincil veri merkezine hello Inmage Scout veri kanalı gerçekleşir.<br><br>![VMware sanal makinelerini çoğaltma](media/operations-management-suite-overview/overview-siterecovery-vmware.png)
- **Fiziksel Windows ve Linux sunucularını çoğaltma.**  Fiziksel sunucuları tooa ikincil veri merkezi ya da tooAzure depolama çoğaltabilirsiniz. Çoğaltma tooAzure bir siteden siteye VPN veya Azure ExpressRoute veya güvenli bir Internet bağlantısı üzerinden oluşabilir. Çoğaltma tooa ikincil veri merkezine hello Inmage Scout veri kanalı gerçekleşir. Azure Site Recovery için bazı istatistiklerini görüntüler OMS çözümünü olsa da, herhangi bir işlem hello Azure portalını kullanmanız gerekir.<br><br>![Fiziksel Windows ve Linux sunucularını çoğaltma](media/operations-management-suite-overview/overview-siterecovery-physical.png)


Site Recovery, belirli bir coğrafi Azure bölgesinde yer alan kasalardaki meta verileri depolar. Hiçbir çoğaltılan veriler Site Recovery hizmeti hello tarafından depolanır.

## <a name="management-solutions"></a>Yönetim Çözümleri
[Yönetim Çözümleri](operations-management-suite-solutions.md), bir veya daha fazla OMS hizmetinden yararlanarak belirli bir yönetim senaryosunu uygulayan önceden paketlenmiş mantık kümeleridir.  Farklı çözümler, Microsoft'un ve iş ortakları OMS tooyour Azure aboneliği tooincrease hello yatırımınızı değerini kolayca ekleyebilirsiniz kullanılabilir.  Bir iş ortağı olarak kendi çözümleri toosupport uygulamaları ve hizmetleri oluşturmak ve bunları hello Azure Marketi ya da Quickstart şablon aracılığıyla toousers sağlayın.

Merhaba birden çok Hizmetleri tooprovide ek işlevleri kullanan bir çözüm iyi bir örneği olan [güncelleştirme yönetimi çözümü](oms-solution-update-management.md).  Bu çözüm, Windows ve Linux toocollect hakkında bilgi için gerekli güncelleştirmeleri her bir aracının hello günlük analizi aracı kullanır.  Burada içeren dahil bir Pano çözümleyebilirsiniz bu verileri toohello günlük analizi depo yazar.  Bir dağıtım oluşturduğunuzda, Azure Otomasyonu'nda runbook'lar gerekli kullanılan tooinstall güncelleştirmelerdir.  Tüm işlem hello portalında yönetmek ve hello temel ayrıntıları hakkında tooworry olması gerekmez.

![Çözüm](media/operations-management-suite-overview/overview-solution.png)

Çözümlerinin çoğu, bir veya daha fazla hello aşağıdaki işlevleri gerçekleştirebilir.

- Ek bilgi toplama.  Log Analytics, istemcilerden ve hizmetlerden olaylar ve performans verileri dahil çeşitli veriler toplar.  Bir yönetim çözümü, çoğunlukla Azure Otomasyonu runbook’larını kullanarak diğer veri kaynakları tarafından sağlanmayan ek bilgiler toplayabilir.
- Toplanan bilgilerin ek analizini gerçekleştirme.  Yönetim çözümleri, verilerin analizi edilmesini ve görselleştirilmesini sağlayan panolar ve görünümler içerir.  Merhaba toodrill izin Bu bağlantı geri toopredefined günlük aramalar veri ayrıntılı.  Bunlar ayrıca örneğin bir tehdit belirtmek desenler için güvenlik olaylarının genelinde arama hello depoya zaten toplanan veriler üzerinde analiz gerçekleştirebilir.
- İşlev ekleme.  Microsoft tarafından sağlanan bazı çözümleri hello Çekirdek Hizmetleri tooprovide ek işlevsellik hello yeteneklerini oluşturabilir.  Hizmet eşlemesi örneğin kendi konsol toodiscover sağlar ve sunucu ve gerçek zamanlı işlem bağımlılıkları eşler.
Çözümleri düzenli olarak tooOMS Microsoft tarafından eklenen ve toocontinuously izin vererek ortakları yatırımınızı hello değerini artırın.  Göz atın ve Microsoft solutions hello çözümleri katalog üzerinden hello OMS portalında yükleyin veya göz atın ve hem Microsoft hem de iş ortağı çözümleri hello Azure Market üzerinden hello Azure Portal yükleyin.  

![Çözüm Galerisi](media/operations-management-suite-overview/solution-gallery.png)


## <a name="next-steps"></a>Sonraki adımlar
* [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) hakkında bilgi edinme.
* [Azure Otomasyonu](../automation/automation-intro.md) hakkında bilgi edinme.
* [Azure Backup](http://azure.microsoft.com/documentation/services/backup) hakkında bilgi edinme.
* [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) hakkında bilgi edinme.
* Merhaba Bul [kullanılabilir çözümleri](../log-analytics/log-analytics-add-solutions.md) hello farklı OMS teklifleri içinde. 

