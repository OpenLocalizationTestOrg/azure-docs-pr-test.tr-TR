---
title: "Ürün Karşılaştırma izleme aaaMicrosoft | Microsoft Docs"
description: "Microsoft Operations Management Suite (OMS) Microsoft'un bulut yönetmek ve şirket içi korumak ve altyapı bulut yardımcı olan BT yönetim çözümü dayalıdır.  Bu makalede OMS dahil hello farklı hizmetleri tanımlar ve bağlantılar sağlar tootheir ayrıntılı içerik."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: a63ca0ad-61f8-425d-a48c-d87ba518c104
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/27/2016
ms.author: bwren
ms.openlocfilehash: 61144a298fe73c35181070d552c41b96fc445097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-monitoring-product-comparison"></a>Microsoft izleme ürün karşılaştırma
Bu makalede, kendi mimarisi, bunlar kaynakları nasıl izlemek ve hello veri analizi nasıl gerçekleştirdikleri hello mantığını bakımından System Center Operations Manager (SCOM) ve günlük analizi Operations Management Suite (OMS) arasında bir karşılaştırma sağlanmaktadır bunlar toplayın.  Toogive budur, kendi farklar ve göreli gücü temel bir anlayış.  

## <a name="basic-architecture"></a>Temel mimari
### <a name="system-center-operations-manager"></a>System Center Operations Manager
Tüm SCOM bileşenleri veri merkezinizde yüklenir.  [Aracıları yüklü](http://technet.microsoft.com/library/hh551142.aspx) Windows ve Linux makinelerde SCOM tarafından yönetilir.  Aracıları bağlanmak çok[yönetim sunucuları](https://technet.microsoft.com/library/hh301922.aspx) hello SCOM veritabanı ve veri ambarı ile iletişim kurar.  Aracıları etki alanı kimlik doğrulaması tooconnect toomanagement sunucularda kullanır.  Bu güvenilen bir etki alanının dışında sertifika kimlik doğrulaması gerçekleştirmek veya tooa bağlanmak [ağ geçidi sunucusu](https://technet.microsoft.com/library/hh212823.aspx).

SCOM iki SQL veritabanları, işlemsel veri için bir ve başka bir veri ambarı toosupport raporlama ve veri analizi gerektirir.  A [raporlama sunucusu](https://technet.microsoft.com/library/hh298611.aspx) SQL Reporting Services tooreport hello veri ambarından veri üzerinde çalışır. 

SCOM yönetim paketleri gibi ürünler için kullanarak bulut kaynaklarını izleyebilirsiniz [Azure](https://www.microsoft.com/download/details.aspx?id=38414), [Office 365](https://www.microsoft.com/download/details.aspx?id=43708), ve [AWS](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/AWSManagementPack.html).  Bu yönetim paketleri kullanın veya daha fazla yerel aracıları bulmak için proxy olarak kaynakları ve iş akışları toomeasure kendi performans ve kullanılabilirlik çalışan bulut.  Proxy aracıları ayrıca kullanılan çok[izleme ağ aygıtları](https://technet.microsoft.com/library/hh212935.aspx) ve diğer dış kaynaklara.

Merhaba işlemleri hello yönetim sunucularının tooone bağlanır ve hello yönetici tooview sağlar ve toplanan verileri çözümlemek ve hello SCOM ortamını yapılandırma bir Windows uygulaması konsoludur.  Web tabanlı bir konsol, herhangi bir IIS sunucusu üzerinde barındırılan ve tarayıcı üzerinden veri çözümleme sağlar.

![SCOM mimarisi](media/operations-management-suite-monitoring-product-comparison/scom-architecture.png)

### <a name="log-analytics"></a>Log Analytics
Dağıtma ve en düşük maliyeti ve yönetim çabası ile yönetmek için çoğu OMS hello Azure bulut bileşenleridir.  Günlük analizi tarafından toplanan tüm verileri hello OMS deposunda saklanır.

Günlük analizi veri üç kaynaktan birinde toplayabilirsiniz:

* Fiziksel ve sanal makineleri Windows hello çalıştıran ve [Microsoft İzleme Aracısı'nı (MMA)](https://technet.microsoft.com/library/mt484108.aspx) veya Linux ve hello [Linux için Operations Management Suite Aracısı](https://technet.microsoft.com/library/mt622052.aspx).  Bu makinelere şirket içi veya Azure veya başka sanal makineler olabilir bulut.
* Bir Azure depolama hesabıyla [Azure tanılama](../cloud-services/cloud-services-dotnet-diagnostics.md) Azure çalışan rolü, web rolü ya da sanal makine tarafından toplanan veriler.
* [Bağlantı tooa SCOM yönetim grubundan](https://technet.microsoft.com/library/mt484104.aspx).  Bu yapılandırmada, hello aracıları, burada sonra toohello OMS veri deposuna teslim hello veri toohello SCOM veritabanı teslim SCOM yönetim sunucularıyla iletişim kurar.
  Yöneticiler, toplanan verileri çözümlemek ve Azure üzerinde barındırılan ve herhangi bir tarayıcıdan erişilebilir hello OMS portalı ile günlük analizi yapılandırın.  Mobil uygulamaları tooaccess bu verileri hello standart platformlar için kullanılabilir.

![Günlük analizi mimarisi](media/operations-management-suite-monitoring-product-comparison/log-analytics-architecture.png)

### <a name="integrating-scom-and-log-analytics"></a>SCOM ve günlük analizi tümleştirme
SCOM için günlük analizi veri kaynağı olarak kullanıldığında, her iki ürün ortamında izleme karma hello özelliklerini yararlanabilirsiniz.  OMS tarafından yönetilen hello Operations Konsolu toobe aracılığıyla mevcut SCOM aracıları yapılandırabilirsiniz, ayrıca SCOM'den toocontinuing toorun yönetim paketleri.  
Bir bağlı SCOM yönetim grubundan veri tooLog dört yöntemden birini kullanarak Analytics teslim edilir:

* Olayları ve performans verilerini hello aracısı tarafından toplanan ve tooSCOM teslim.  SCOM yönetim sunucuları, ardından hello veri tooLog Analytics sunar.
* IIS günlükleri gibi bazı olaylar ve güvenlik olaylarını toobe hello Aracısı'ndan doğrudan tooLog Analytics teslim devam edin.
* Bazı çözümleri ek yazılım toohello Aracısı teslim veya yazılım yüklü toocollect ek veri olmasını gerektirir.  Bu veriler genellikle doğrudan tooLog Analytics gönderilir.
* Bazı çözümleri doğrudan hello Aracısı'ndan kaynaklanmayan SCOM yönetim sunucularından veri toplar.  Örneğin, hello [uyarı yönetimi çözümü](https://technet.microsoft.com/library/mt484092.aspx) oluşturulduktan sonra SCOM'den uyarılarını toplar.

## <a name="monitoring-logic"></a>İzleme mantığını
SCOM ve günlük analizi aracılardan toplanan benzer verilerle çalışır ancak nasıl tanımlamak ve veri toplama için kendi mantığını uygulamak ve nasıl bunlar bunlar toplamak hello verileri çözümlemek temel farklılıklar vardır.

### <a name="operations-manager"></a>Operations Manager
SCOM uygulanan için izleme mantığı [yönetim paketleri](https://technet.microsoft.com/library/hh457558.aspx) bileşenleri toomonitor, bu bileşenlerin hello durumunu ölçme keşfetmek ve veri tooanalyze toplamak için mantığı içerir.  İzleme verilerini bir olay veya performans sayacı toplama olarak kadar basit olabilir veya bir betikte uygulanan karmaşık mantık kullanabilirsiniz.  Tam izleme içeren yönetim paketleri çeşitli için kullanılabilir [Microsoft ve üçüncü taraf uygulamaları](http://go.microsoft.com/fwlink/?LinkId=82105) toplama toohardware ve ağ aygıtları.  Yapabilecekleriniz [kendi yönetim paketlerinizi Yazar](http://aka.ms/mpauthor) özel uygulamalar için.

Yönetim paketleri, her bir performans sayacı örnekleme, hello bir hizmetin durumunu denetleme veya betik çalıştırma gibi bazı farklı izleme işlevi yerine getiren birden çok iş akışı içerir.  Her bir iş akışı bağımsız olarak çalışır ve hangi veritabanı gibi tooand bir uyarı üretir olup olmadığını yazacak kendi sonuçları tanımlar. 

İş akışı çalıştırdıkları, hello sıklığı burada bunlar hata göz önünde bulundurun hello eşik gibi ayrıntılarını ve hello uyarının önem derecesini oluşturdukları hello geçersiz kılabilirsiniz.  Ayrıca, kendi iş akışları ekleyerek ek işlevsellik sağlayabilir.

![Geçersiz kılmaları](media/operations-management-suite-monitoring-product-comparison/scom-overrides.png)

Yönetim paketleri hello Operations Manager veritabanına yüklenir ve tooagents yönetim sunucuları tarafından otomatik olarak dağıtılır.  Her bir aracının otomatik olarak yönetim paketlerini karşıdan yüklemek ve iş akışları ilgili toohello uygulamaların yüklü olduğu yükleyin.  Merhaba aracısı tarafından toplanan veriler geri toohello yönetim sunucusu ekleme için hello SCOM veritabanı ve veri ambarına teslim edilir.  Hello Operations Konsolu tooview sağlar ve özel görünümler, panolar ve raporlar hello yönetim paketinde aracılığıyla bu verileri analiz edin.

yönetim paketlerinin Hello dağıtım diyagramı aşağıdaki hello gösterilmiştir.

![Yönetim Paketi akış](media/operations-management-suite-monitoring-product-comparison/scom-mpflow.png)

### <a name="log-analytics"></a>Log Analytics
#### <a name="event-and-performance-collection"></a>Olay ve performans toplama
Günlük analizi, Windows olay günlüğü, IIS günlüklerini ve Syslog gibi kaynakları kullanarak aracı sistemlerden olaylar ve performans sayaçlarını toplar.  Hangi veri hello günlük analizi portalından toplanır ve günlük sorguları tooanalyze hello toplanan verileri oluşturma ölçütü tanımlayabilirsiniz.  Standart ölçüt OMS çalışma alanınızı oluştururken ve belirli uygulamalar için ek veri tanımlayabilirsiniz tanımlanır. 

![Günlük analizi tanımlayan olay günlükleri](media/operations-management-suite-monitoring-product-comparison/log-analytics-definedata.png)

SCOM birçok genellikle veri belirli ölçütleri tanımlayın ayrıntılı iş akışları ve yanıt olarak gerçekleştirilmelidir hello eylem sahipken, günlük analizi veri toplama için daha fazla genel ölçüt içeriyor.  Günlük sorgular ve çözümleri analiz etme ve toplanan sonra hello bulut belirli veriler üzerinde çalışıyor. daha fazla hedeflenen ölçütlerini belirtin.

#### <a name="solutions"></a>Çözümler
Çözümleri, veri toplama ve analiz için ilave bir mantık sağlar.  Çözüm Galerisi hello çözümleri tooadd tooyour OMS abonelik seçebilirsiniz.

![Çözümleri Galerisi](media/operations-management-suite-monitoring-product-comparison/log-analytics-solutiongallery.png)

Olayları ve hello OMS deposunda toplanan performans sayaçlarının analizini sağlayan hello bulutta çözümleri öncelikle çalıştırın.  Bunlar, ayrıca günlük sorgularla veya hello OMS panosunda hello çözümü tarafından sağlanan ek kullanıcı arabirimi tarafından çözümlenebilir toplanan ek veri toobe tanımlayabilir. 

Örneğin, hello [değişiklik izleme çözümü](https://technet.microsoft.com/library/mt484099.aspx) yapılandırma aracı sistemlerinde dönüşür ve özetleyen birkaç grafik görünümlerle çözümlenebilir deposu değişiklikleri algılandı olayları toohello OMS Yazar algılar.  Özetlenen hello görünümünden günlük sorgulara bu görüntü hello ayrıntıya girebilirsiniz ayrıntılı hello çözümü tarafından toplanan veriler.

Hangi çözümü seçerken tooyour abonelik eklemek için şu anda hello özelliği toocreate kendi çözüm yok.  Merhaba olaylar ve performans sayaçları toocollect seçin ve kendi günlük sorguları temel alan özel görünümler oluşturun.

Günlük analizi için izleme mantığı hello diyagramı aşağıdaki hello özetlenir.

![Günlük analizi çözüm akışı](media/operations-management-suite-monitoring-product-comparison/log-analytics-solution-flow.png)

## <a name="health-monitoring"></a>Sistem Durumunu İzleme
### <a name="operations-manager"></a>Operations Manager
SCOM hello farklı bir uygulama bileşenlerinin model ve gerçek zamanlı bir sistem durumu için her sağlayın.  Bu, hataları ve zaman içerisinde performansı, toonot yalnızca görünüm algıladı, ancak ayrıca toovalidate hello gerçek bir uygulama veya sistem durumunu ve her bir bileşen herhangi bir zamanda sağlar.  Bir uygulama kullanılabilir dönemleri hello anladığı olduğundan, hello sistem durumu altyapısı scom'deki hizmet düzeyi sözleşmeleri (hangi çözümleme ve zaman içinde bir uygulamanın kullanılabilirliğini hello raporlama SLA) da destekler.

Örneğin, aşağıdaki hello görünüm hello gerçek zamanlı SQL veritabanı motoru tarafından SCOM izlenen durumunu gösterir.  Her bir hello veritabanı hello veritabanı motoru biri için Hello durumunu hello alta yarısı hello görünümü gösterilir.

![Durum görünümü](media/operations-management-suite-monitoring-product-comparison/scom-state-view.png)

Merhaba hello veritabanı motoru biri için sistem durumu Gezgini kullanılan toodetermine olan hello monitörlerle genel sistem durumu aşağıda verilmiştir.  Bu monitörlerin hello SQL Yönetim Paketi tanımlanır ve SCOM tarafından bulunan tüm SQL veritabanı motoru karşı çalıştırın.

![Sistem durumu Gezgini](media/operations-management-suite-monitoring-product-comparison/scom-health-explorer.png)

Birden çok sistem üzerinde bileşenleri birleşik toomeasure hello bir dağıtılmış uygulama durumunu olabilir.  Bu, birden çok Dağıtılmış Bileşen içeren iş kolu uygulamaları için özellikle yararlı olabilir.  Merhaba uygulaması için kullanılabilirlik içine, her bileşenin sistem durumu hello ölçer bir model, toplaması oluşturabilirsiniz.

Active Directory, dağıtılmış bileşenlerinden modeli tooanalyze sağlayan bir Yönetim Paketi örneğidir.  Merhaba örnek diyagramı gösterir hello durumunu aşağıda genel ortamında ve ormanlar, etki alanları ve etki alanı denetleyicileri arasında hello ilişki hello.  Bu bileşenlerin her birini bileşenleri içerir ve birden çok benzer toohello SQL örneği yukarıdaki izler.

![SCOM diyagram görünümü](media/operations-management-suite-monitoring-product-comparison/scom-diagram-view.png)

### <a name="log-analytics"></a>Log Analytics
OMS bir ortak altyapısı toomodel uygulamaları içermez ve gerçek zamanlı durumlarını ölçün.  Tek tek çözümlerinin hello değerlendirmek belirli hizmetleri genel durumunu toplanan verileri temel ve Özel mantık hello Aracısı tooperform üzerinde gerçek zamanlı analiz yükleyebilir.  Çözümleri erişim toohello OMS deposu ile Merhaba bulutta çalıştığından, genellikle genellikle yönetim paketleri tarafından gerçekleştirilen daha derin çözümleme sağlayabilir. 

Örneğin, hello [AD değerlendirmesi ve SQL değerlendirmesi çözümleri](https://technet.microsoft.com/library/mt484102.aspx) toplanan verileri çözümlemek ve farklı yönlerini hello ortam için bir derecelendirme sağlayın.  Tooimprove hello kullanılabilirliğini ve performansını hello ortamının yapılan iyileştirmeler için öneriler içerir.

![AD değerlendirme çözümü](media/operations-management-suite-monitoring-product-comparison/log-analytics-ad-assessment.png)

## <a name="data-analysis"></a>Veri analizi
SCOM ve günlük analizi farklı özellikler tooanalyze toplanan veriler sağlar.  SCOM görünümleri ve panoları hello Operations Konsolu biçimleri ve Tablo formunda hello veri ambarından veri sunmak için raporlar çeşitli son verileri çözümlemek için vardır.  Günlük analizi hello OMS deposundaki verileri çözümlemek için bir tam günlük sorgu dili ve arabirim sağlar.  SCOM için günlük analizi veri kaynağı olarak kullanıldığında, hello deposu hello günlük analiz araçları her iki sistemle kullanılan tooanalyze verilerden olabilir SCOM tarafından toplanan verileri içerir.

### <a name="operations-manager"></a>Operations Manager
#### <a name="views"></a>Görünümler
Merhaba Operations Konsolu görünümlerde, tooview farklı veri türleri farklı biçimlerde, olayları, uyarıları ve Durum verilerini ve performans verileri için çizgi grafikler için genellikle tablo SCOM tarafından toplanan izin verir.  Görünümler, en az çözümlemesi ya da hello veri birleştirilmesi ancak tooparticular ölçütleri göre toofilter izin. 

![Görünümler](media/operations-management-suite-monitoring-product-comparison/scom-views.png)

Yönetim paketleri genellikle Merhaba uygulaması ya da izlediği sistem destekleyen birden çok görünüm sağlar.  Bu hello yönetim paketinin bulduğu hello farklı nesneler için durum görünümleri içerir, algılanan sorunlar için görünümleri ve sayaçları için performans görünümleri uyarı.

Görünümler, özellikle, açık uyarılar ve hello sistem durumunu izlenen sistemleri ve nesneleri dahil olmak üzere hello ortamının hello geçerli durumu çözümlemek için uygundur.  Belirli bir uyarı sipariş toodiagnose destekleyen toodetailed olay veya performans verileri kök nedenini ayrıntıya girebilirsiniz. Benzer şekilde, geçerli sistem durumu hello performans ve farklı bir uygulama tooassess bileşenlerinin durumunu görüntüleyebilirsiniz.

#### <a name="dashboards"></a>Panolar
Daha özelleştirilebilir ve daha zengin Görselleştirmelerini içerebilir ancak görünümler gibi işlemler konsolunu öncelikle çalışabilirsiniz hello panolarında aynı veri hello.  Bir dizi standart panolar kullanılabilir kendi amaçlarınız doğrultusunda kolayca özelleştirebilirsiniz.  Bir PowerShell sorgudan döndürülen verileri görüntüleyen bir PowerShell pencere öğesini de kullanabilirsiniz.

![Pano](media/operations-management-suite-monitoring-product-comparison/scom-dashboard.png)

Geliştiriciler kendi yönetim paketlerine dahil hello özelliği tooadd özel bileşenler toodashboards sahip.  Bu, yüksek oranda özelleştirilmiş tooa hello panosunda hello SQL Yönetim Paketi aşağıda gösterildiği gibi belirli uygulama olabilir.  Bu panoyu özel sürümleri için de bir şablon olarak kullanılabilir.

![SQL Panosu](media/operations-management-suite-monitoring-product-comparison/scom-sql-dashboard.png)

#### <a name="reports"></a>Reports
Scom'deki raporları Tablo formunda hello veri ambarından veri çözümleyin.  Bunlar yazdırılabilir ve PDF, CSV ve Word gibi farklı dosya biçimlerinde otomatik teslim için zamanlanan.  Uzun vadeli eğilimlerini analiz için özellikle uygun şekilde raporları hello veri ambarından verilerle çalışır.

Yönetim paketleri genellikle özel raporlar için belirli bir uygulama sağlar.  Kendi uygulamalar için veya geçici analiz gerçekleştirmek için özelleştirebileceğiniz genel rapor kitaplığı seçebilirsiniz.

Merhaba Active Directory Yönetim Paketi tarafından toplanan verileri gösteren bir örnek performans raporu aşağıdadır.

![Rapor](media/operations-management-suite-monitoring-product-comparison/scom-report.png)

### <a name="log-analytics"></a>Log Analytics
Günlük analizi sahip bir [sorgu dili](https://technet.microsoft.com/library/mt484120.aspx) tooperform analiz hello gerek toocreate olmadan birden çok uygulama verilerinden arasında özel bir görünüm veya rapor kullanabileceğinizi.  OMS hello buluta uygulanan olduğundan, sorgular ve veri analizi performansını konu tooany donanım sınırlamaları değildir ve milyonlarca kayıt da dahil, sorguların kolayca çözümleyebilirsiniz. 

Günlük analizi sorgularında ayrıca hello diğer işlevselliğin temelidir.  Bir sorgu kaydetmek, sonuçları tooExcel dışarı aktarma veya sahip otomatik olarak düzenli aralıklarla çalıştırmak ve sonuçları belirli ölçütlere uyan varsa uyarı oluştur.  

![Günlük sorgu akışı](media/operations-management-suite-monitoring-product-comparison/log-analytics-query-flow.png)

Günlük analizi sorgu örneği aşağıdadır.  Bu örnekte "Merhaba adı kullanmaya" ile tüm olayları döndürülen ve olay tarafından gruplandırılmış kimliği  Merhaba kullanıcı yalnızca hello sorgu sağlar ve günlük analizi hello kullanıcı arabirimi tooperform hello çözümlemesi dinamik olarak oluşturur.  Merhaba listedeki herhangi bir öğeyi seçerek döndürecektir hello ayrıntılı olay verileri.

![Günlük sorgu](media/operations-management-suite-monitoring-product-comparison/log-analytics-query.png)

Ayrıca tooproviding geçici analiz, günlük analizi sorgularda gelecekte kullanmak ve aynı zamanda eklenen tooyour için kaydedilebilir [OMS Pano](http://technet.microsoft.com/library/mt484090.aspx) hello aşağıdaki örnekte gösterildiği gibi.

![OMS Panosu](media/operations-management-suite-monitoring-product-comparison/log-analytics-dashboard.png)

## <a name="next-steps"></a>Sonraki Adımlar
* Dağıtma [System Center Operations Manager (SCOM)](https://technet.microsoft.com/library/hh205987.aspx).
* Kaydolun [günlük analizi](https://azure.microsoft.com/documentation/services/log-analytics).  

