---
title: "aaaAzure App Service, sanal makineleri, Service Fabric ve Cloud Services karşılaştırması | Microsoft Docs"
description: "Bilgi nasıl toochoose Azure App Service, sanal makineleri, Service Fabric ve bulut barındırma hizmetleri arasında web uygulamaları."
services: app-service\web, virtual-machines, cloud-services
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 7d346a23-532a-42a9-98a8-23b7286d32a8
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 07/07/2016
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 7577332ed049df66178c7b2cd5c440a7f93a7865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-virtual-machines-service-fabric-and-cloud-services-comparison"></a>Azure App Service, sanal makineler, Service Fabric ve Cloud Services karşılaştırması
## <a name="overview"></a>Genel Bakış
Azure toohost web siteleri çeşitli yöntemler sunar: [Azure App Service][Azure App Service], [sanal makineleri][Virtual Machines], [Service Fabric ] [ Service Fabric], ve [bulut hizmetlerini][Cloud Services]. Bu makalede hello seçenekleri anlamanıza ve hello web uygulamanız için doğru seçim yapmanıza yardımcı olur.

Azure uygulama hizmeti hello iyi çoğu web uygulamaları için seçimdir. Dağıtım ve yönetim hello platformu ile tümleştirilir, sitelerini hızlı bir şekilde toohandle yüksek trafik yükleri ölçeklenebilir ve hello yerleşik Yük Dengeleme ve trafik Yöneticisi yüksek kullanılabilirlik sağlar. Var olan siteler tooAzure uygulama hizmeti taşıyabilirsiniz kolayca bir [çevrimiçi geçiş aracı](https://www.migratetoazure.net/)hello Web uygulama Galerisi açık kaynak uygulama kullanın veya hello framework ve tercih ettiğiniz araçları kullanarak yeni bir site oluşturun. Merhaba [WebJobs] [ WebJobs] özellik kolay tooadd arka plan iş işleme tooyour App Service web uygulaması sağlar.

Service Fabric iyi bir yöntemdir yeni bir uygulama oluşturma ya da mevcut bir uygulamayı yeniden yazma toouse mikro hizmet mimarisi. Paylaşılan bir havuzunda makineleri çalıştırmak, uygulamaları küçük başlayın ve yüzlerce veya binlerce gerektiğinde makinelerin ile toomassive ölçeği büyütün. Durum bilgisi olan hizmetler kolay tooconsistently kolaylaştırır ve uygulama durumunu güvenilir bir şekilde depolamak ve Service Fabric otomatik olarak hizmet bölümlendirme, ölçeklendirme ve kullanılabilirlik tarafından yönetilir.  Service Fabric Webapı açık Web arabirimi ile .NET (OWIN) ve ASP.NET Core için de destekler.  Karşılaştırılan tooApp hizmeti, Service Fabric ayrıca daha fazla denetime ya da doğrudan erişim, hello temel altyapı sağlar. Sunucu başlangıç görevleri yapılandırmak veya sunucularınızı uzaktan kullanabilirsiniz. Bulut Hizmetleri benzer tooService denetim kullanım kolaylığı karşı derecesini yapıda olan ancak bu artık eski bir hizmet olduğundan ve yeni geliştirme projeleri için Service Fabric önerilir.

Uygulama hizmeti veya Service Fabric önemli değişiklikler toorun gerektiren var olan bir uygulamanız varsa, toohello bulut geçiş sırası toosimplify sanal makineleri seçebilir. Ancak, doğru şekilde yapılandırmak, güvenli hale getirme ve Vm'leri koruma çok daha fazla süresi gerektirir ve BT uzmanlık tooAzure uygulama hizmeti ve Service Fabric karşılaştırılan. Azure sanal makineleri düşünüyorsanız, hesap hello devam eden bakım gereken çaba toopatch emin olmak güncelleştirin ve VM ortamınızı yönetmek. Azure sanal makinelerin App Service ve Service Fabric Platform olarak-hizmet (Paas) durumdayken-olarak-hizmet altyapı (Iaas) şeklindedir. 

## <a name="features"></a>Özellik karşılaştırması
Uygulama hizmeti hello özelliklerini aşağıdaki tablonun hello karşılaştırır, bulut Hizmetleri, sanal makineler ve Service Fabric toohelp hello en iyi seçim yapın. Her seçenek için başlangıç SLA hakkında güncel bilgiler için bkz: [Azure hizmet düzeyi sözleşmeleri](https://azure.microsoft.com/support/legal/sla/).

| Özellik | Uygulama Hizmeti (web uygulamaları) | Bulut Hizmetleri (web rolleri) | Virtual Machines | Service Fabric | Notlar |
| --- | --- | --- | --- | --- | --- |
| Neredeyse anında dağıtım |X | | |X |Bir uygulama veya bir uygulama güncelleştirme tooa bulut hizmeti dağıtma veya bir VM oluşturma en az birkaç dakika sürer; bir uygulama tooa web uygulaması dağıtma birkaç saniye sürer. |
| Dağıtın olmayan toolarger makineler ölçeklendirin |X | | |X | |
| Web sunucusu örneğine içerik ve tooredeploy sahip değilsiniz veya kendi ölçeklendirmenize göre yeniden yapılandırmanız anlamına gelir yapılandırma paylaşır. |X | | |X | |
| Birden çok dağıtım ortamı (üretim ve hazırlama) |X |X | |X |Service Fabric toohave verir uygulamalarınıza veya toodeploy, uygulama yan yana farklı sürümleri için birden çok ortamı. |
| Otomatik işletim sistemi güncelleştirme yönetimi |X |X | | |Gelecekteki bir Service Fabric yayın için otomatik işletim sistemi güncelleştirmelerini planlanmaktadır. |
| Sorunsuz platform değiştirme (32 bit ve 64 bit arasında kolayca geçiş) |X |X | | | |
| GIT, FTP ile kod dağıtma |X | |X | | |
| Web dağıtımı ile kod dağıtma |X | |X | |Bulut Hizmetleri hello toodeploy güncelleştirmeleri tooindividual rol örnekleri Web dağıtımı kullanımını destekler. Ancak, bir rolün ilk dağıtımınızı kullanamazsınız ve bir güncelleştirme için Web dağıtımı kullanırsanız toodeploy ayrı olarak sahip bir rol tooeach örneği. Birden çok sipariş tooqualify üretim ortamları için bulut hizmeti SLA hello için gereklidir. |
| WebMatrix desteği |X | |X | | |
| Hizmet veri yolu, depolama, SQL veritabanı gibi erişim tooservices |X |X |X |X | |
| Ana bilgisayar web veya web hizmetleri katmanı çok katmanlı mimarisi |X |X |X |X | |
| Çok katmanlı mimarisinin konak orta katman |X |X |X |X |App Service web apps kolayca bir REST API'si Orta katmanı barındırmak ve hello [WebJobs](http://go.microsoft.com/fwlink/?linkid=390226) özelliği, arka plan işleme işleri barındırabilir. Ayrılmış Web sitesinde bir tooachieve bağımsız ölçeklenebilirlik hello katmanı için Web işleri çalıştırabilirsiniz. Merhaba Önizleme [API uygulamaları](../app-service-api/app-service-api-apps-why-best-platform.md) özelliği REST Hizmetleri barındırmak için daha da fazla özellikleri sağlar. |
| Tümleşik Hizmet olarak MySQL desteği |X |X |X | |Bulut Hizmetleri hizmet olarak MySQL Cleardb'nin teklifleri aracılığıyla ancak hello Azure Portal iş akışının parçası olarak değil tümleştirebilirsiniz. |
| ASP.NET, klasik ASP, Node.js, PHP, Python desteği |X |X |X |X |Service Fabric kullanarak bir web ön uç hello oluşturulmasını destekler [ASP.NET 5](../service-fabric/service-fabric-add-a-web-frontend.md) veya herhangi bir türde uygulamayı (Node.js, Java, vb.) olarak dağıtabileceğiniz bir [Konuk yürütülebilir](../service-fabric/service-fabric-deploy-existing-app.md). |
| Toomultiple örnekleri dağıtın olmadan ölçeğini genişletme |X |X |X |X |Sanal makineler toomultiple örnekleri ölçeklendirme yapabilir, ancak bunlar üzerinde çalışan hello Hizmetleri toohandle bu genişleme yazılmış olmalıdır. Merhaba makineler arasında bir yük dengeleyici tooroute isteklerini tooconfigure sahip ve bir benzeşim grubu tooprevent toomaintenance veya donanım hataları nedeniyle tüm örnekleri aynı anda yeniden oluşturun. |
| SSL desteği |X |X |X |X |App Service web uygulamaları için özel etki alanı adları için SSL yalnızca temel ve Standart modu için desteklenir. Web uygulamaları ile SSL kullanma hakkında daha fazla bilgi için bkz: [bir Azure Web sitesi için bir SSL sertifikası yapılandırma](app-service-web-tutorial-custom-ssl.md). |
| Visual Studio tümleştirmesi |X |X |X |X | |
| Uzaktan hata ayıklama |X |X |X | | |
| Kod TFS ile Dağıt |X |X |X |X | |
| Ağ yalıtımı ile [Azure sanal ağ](/azure/virtual-network/) |X |X |X |X |Ayrıca bkz. [Azure Web siteleri sanal ağ tümleştirme](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/) |
| Desteği [Azure trafik Yöneticisi](/azure/traffic-manager/) |X |X |X |X | |
| Tümleşik uç nokta izleme |X |X |X | | |
| Uzak Masaüstü erişimi tooservers | |X |X |X | |
| Tüm özel MSI yükleme | |X |X |X |Service Fabric sağlar, herhangi bir yürütülebilir dosya olarak toohost bir [Konuk yürütülebilir](../service-fabric/service-fabric-deploy-existing-app.md) veya hello Vm'leri üzerinde herhangi bir uygulama yükleyebilirsiniz. |
| Özelliği toodefine ve yürütme başlangıç görevleri | |X |X |X | |
| TooETW olayları dinleme | |X |X |X | |

## <a name="scenarios"></a>Senaryolar ve öneriler
Toowhich Azure web barındırma seçeneği her biri için en uygun olabileceği bazı ortak uygulama senaryolar öneriler verilmiştir.

* [Bir web ön uç arka plan işlemeye ve veritabanı arka uç toorun iş uygulamaları ile şirket içi varlıklarını tümleşik ihtiyacım.](#onprem)
* [Well ve teklifleri genel ölçekler my Kurumsal Web sitesi ulaşmak güvenilir şekilde toohost ihtiyacım.](#corp)
* [Windows Server 2003'te çalışan bir IIS6 uygulama var.](#iis6)
* [Küçük işletme sahibi ben ve uygun maliyetli şekilde toohost Sitem ihtiyacım ancak Gelecekteki büyümeyi unutmayın.](#smallbusiness)
* [Bir web veya grafik Tasarımcı ben ve toodesign istediğiniz ve my müşteriler için web siteleri oluşturmak.](#designer)
* [Bir web ön uç toohello bulut ile çok katmanlı Uygulamam geçirme.](#multitier)
* [Yüksek oranda özelleştirilmiş Windows Uygulamam bağlıdır ya da Linux ortamları ve istediğiniz toomove onu toohello bulut.](#custom)
* [Açık kaynak yazılımının Sitem kullanır ve toohost istediğiniz Azure içinde.](#oss)
* [Tooconnect toohello Kurumsal ağda gereken bir iş kolu satır uygulama var.](#lob)
* [Toohost mobil istemciler için bir REST API veya web hizmeti istiyorum.](#mobile)

### <a id="onprem"></a>Bir web ön uç arka plan işlemeye ve veritabanı arka uç toorun iş uygulamaları ile şirket içi varlıklarını tümleşik ihtiyacım.
Azure uygulama hizmeti, karmaşık iş uygulamaları için mükemmel bir çözümdür. Sağlar ölçeği otomatik olarak bir yük dengeli platformda, Active Directory ile güvenli kılınan ve tooyour şirket içi kaynaklara bağlanmak uygulamaları geliştirin. Bu uygulamaları bir dünya çapındaki portal ve API kolay hale getirir ve nasıl müşteriler bunları app Insight araçlarıyla kullandığını içine toogain hakkında bilgi sağlar. Merhaba [Webjobs] [ Webjobs] özelliği arka plan işlemlerini çalıştırmak olanak tanır ve görevleri karma bağlantı ve sanal ağ özellikleri, web katmanının bir parçası olarak kolay tooconnect geri tooon içi kaynaklar kolaylaştırır. Azure uygulama hizmeti web uygulamaları için üç 9 ait SLA sağlar ve sağlar:

* Uygulamalarınızın güvenilir bir şekilde kendini onarma, otomatik düzeltme eki uygulama bulut platformu üzerinde çalıştırın.
* Veri merkezlerinin küresel bir ağda otomatik olarak ölçeklendirin.
* Yedekleme ve olağanüstü durum kurtarma için geri yükleme.
* ISO, SOC2 ve PCI uyumlu olmalıdır.
* Active Directory ile tümleştirin

### <a id="corp"></a>Well ve teklifleri genel ölçekler my Kurumsal Web sitesi ulaşmak güvenilir şekilde toohost ihtiyacım.
Azure uygulama hizmeti, şirket Web siteleri barındırmak için harika bir çözümdür. Web uygulamaları tooscale hızlı bir şekilde etkinleştirir ve kolayca toomeet talep veri merkezlerinin küresel bir ağda. Yerel reach, hata toleransı ve akıllı trafik yönetimi sunar. Dünya çapındaki yönetim araçları sağlayan tüm bir platformda, hızlı ve kolay bir şekilde toogain fikirler site durumu ve site trafik sağlayarak. Azure uygulama hizmeti web uygulamaları için üç 9 ait SLA sağlar ve sağlar:

* Sitelerinizi güvenilir bir şekilde kendini onarma, otomatik düzeltme eki uygulama bulut platformu üzerinde çalıştırın.
* Veri merkezlerinin küresel bir ağda otomatik olarak ölçeklendirin.
* Yedekleme ve olağanüstü durum kurtarma için geri yükleme.
* Günlüklerini yönetmek ve tümleşik araçlarıyla trafiği.
* ISO, SOC2 ve PCI uyumlu olmalıdır.
* Active Directory ile tümleştirin

### <a id="iis6"></a>Windows Server 2003'te çalışan bir IIS6 uygulama var.
Azure uygulama hizmeti kolay tooavoid kılar hello altyapı maliyetlerini geçirme eski IIS6 uygulamalarla ilişkili. Microsoft oluşturdu [kolay toouse geçiş araçları ve ayrıntılı geçiş yönergeleri](https://www.movemetowebsites.net/) toocheck uyumluluk etkinleştirmek ve yapılan toobe gereken değişiklikleri tanımlar. Visual Studio, TFS ve ortak CMS araçları ile tümleştirme toohello bulut doğrudan kolay toodeploy IIS6 uygulamaları kolaylaştırır. Uygulama dağıtıldıktan sonra hello Azure Portal tooscale toomanage maliyetleri aşağı ve yukarı toomeet talep gerekli olarak sağlayan güçlü yönetim araçları sağlar. Merhaba geçiş aracı ile şunları yapabilirsiniz:

* Hızla ve kolayca eski Windows Server 2003 web uygulama toohello bulut geçirin.
* Tooleave ekli, SQL veritabanı şirket içi toocreate karma uygulama kabul et.
* Otomatik olarak SQL veritabanınız eski uygulamanızı birlikte taşınır.

### <a id="smallbusiness"></a>Küçük işletme sahibi ben ve uygun maliyetli şekilde toohost Sitem ihtiyacım ancak Gelecekteki büyümeyi unutmayın.
Ücretsiz kullanmaya başlamak ve bunları gerektiğinde daha fazla özellikleri eklemek için azure uygulama hizmeti bu senaryo için harika bir çözümdür. Her ücretsiz bir web uygulamasını Azure tarafından sağlanan bir etki alanı ile birlikte gelir (*your_company*. azurewebsites.net), ve hello platform içerir tümleşik dağıtım ve yönetim araçları ve bunun yanı sıra kolay tooget olun bir uygulama Galerisi başlatıldı. Diğer birçok Hizmetleri ve artan kullanıcı talep hello site tooevolve izin ölçeklendirme seçenekleri vardır. Azure App Service ile şunları yapabilirsiniz:

* Merhaba ücretsiz katmanı ile başlayın ve gerektikçe sonra ölçeği.
* WordPress gibi popüler web uygulamalarını ayarlama hello uygulama Galerisi tooquickly kullanın.
* Ek Azure Hizmetleri ve özellikleri tooyour uygulama gerektiği gibi ekleyin.
* Web uygulamanızı HTTPS ile güvenli hale getirin.

### <a id="designer"></a>Bir web veya grafik Tasarımcı ben ve toodesign istediğiniz ve my müşteriler için Web siteleri oluşturun
Azure uygulama hizmeti çeşitli çerçeveler ve araçları ile kolayca tümleşir web geliştiricileri ve tasarımcıları, Git ve FTP için dağıtım desteği içerir ve araçları ve Visual Studio ve SQL veritabanı gibi hizmetleri ile sıkı tümleştirme sağlar. App Service ile yapabilecekleriniz:

* İçin komut satırı araçlarını kullanmayı [otomatik görevleri][scripting].
* Popüler dillerde gibi çalışmak [.Net][dotnet], [PHP][PHP], [Node.js][nodejs], ve [Python][Python].
* Toovery yüksek kapasite ölçekleme için üç farklı ölçeklendirme düzeylerini seçin.
* Gibi diğer Azure hizmetleriyle tümleştirme [SQL veritabanı][sqldatabase], [Service Bus] [ servicebus] ve [depolama] [ Storage], veya ortak hello sunduğu [Azure depolama][azurestore], MySQL ve MongoDB gibi.
* Visual Studio, Git, WebMatrix, WebDeploy, TFS ve FTP gibi araçları ile tümleştirin.

### <a id="multitier"></a>Çok katmanlı Uygulamam bir web ön uç toohello bulut ile geçirmek
Tooa veritabanına bağlanan bir web sunucusu gibi çok katmanlı bir uygulama çalıştırıyorsanız, Azure App Service, Azure SQL veritabanı ile sıkı tümleştirme sunan iyi bir seçenektir. Ve arka uç işlemlerini çalıştırmak için hello WebJobs özelliğini kullanabilirsiniz.

Service Fabric birini veya daha fazla daha ihtiyacınız varsa, bu katmanların hello özelliği tooremote sunucunuz içine gibi hello sunucu ortamı üzerinden denetlemesine veya sunucu başlangıç görevleri yapılandırın.

Toouse istiyorsanız, sanal makineleri bir veya daha fazla, katmanları için kendi makine görüntüsü seçin veya sunucu yazılımı veya Service Fabric yapılandıramazsınız Hizmetleri çalıştırın.

### <a id="custom"></a>Yüksek oranda özelleştirilmiş Windows Uygulamam bağlıdır ya da Linux ortamları ve istediğiniz toomove onu toohello bulut.
Uygulamanızı karmaşık yükleme veya yazılım ve hello işletim sisteminin yapılandırmasını gerektiriyorsa, sanal makineleri büyük olasılıkla hello en iyi çözüm. Sanal makineler ile şunları yapabilirsiniz:

* Bir işletim sistemi, Windows veya Linux gibi Hello sanal makineye Galerisi toostart kullanın ve sonra uygulamanızın gereksinimleri için özelleştirin.
* Oluşturun ve mevcut şirket içi sunucu toorun azure'da bir sanal makinede özel bir görüntüsünü yükleyin.

### <a id="oss"></a>Açık kaynak yazılımının Sitem kullanır ve toohost istediğiniz Azure içinde
Varsa, açık kaynak framework uygulama hizmeti hello dilleri desteklenir ve uygulama tarafından gerek duyulan çerçeveleri sizin için otomatik olarak yapılandırılır. Uygulama hizmeti sağlar:

* Birçok popüler açık kaynak dilleri, gibi kullandığınız [.NET][dotnet], [PHP][PHP], [Node.js][nodejs], ve [Python][Python].
* WordPress, Drupal, Umbraco, DNN ve diğer birçok üçüncü taraf web uygulamalarını ayarlayın.
* Var olan bir uygulama geçirmek veya hello uygulama Galerisi öğesinden yeni bir tane oluşturun.

Uygulama hizmeti, açık kaynak framework desteklenmiyorsa, hello birinde diğer Azure web sitesi barındırma seçenekleri çalıştırabilirsiniz. Sanal makineler ile yükleme ve hello yazılım Windows olabilen hello makine görüntüsüne, yapılandırma veya Linux tabanlı.

### <a id="lob"></a>Tooconnect toohello Kurumsal ağda gereken bir iş kolu satır uygulama yüklü
Toocreate iş kolu satır uygulama isterseniz, sitenizi doğrudan erişim tooservices veya veri hello şirket ağındaki gerektirebilir. Bu uygulama hizmeti, Service Fabric ve hello kullanarak sanal makineleri mümkündür [Azure Virtual Network service](/azure/virtual-network/). Uygulama hizmeti hello kullanabilirsiniz [VNET tümleştirme özelliği](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/), şirket ağınıza değilmiş gibi Azure uygulamalarını toorun sağlar.

### <a id="mobile"></a>Toohost mobil istemciler için bir REST API veya web hizmeti istiyorum
HTTP tabanlı web hizmetlerinde toosupport çok çeşitli istemciler, mobil istemciler dahil olmak üzere etkinleştirin. ASP.NET Web API gibi çerçeveleri isteğe bağlı olarak Visual Studio toomake ile daha kolay toocreate bütünleşir ve REST hizmetlerini kullanma.  Bu Hizmetleri web uç noktasından sunulur, böylece olası toouse herhangi Azure toosupport barındırma tekniği bu senaryo web. Ancak, REST API'leri barındırmak için harika bir seçim uygulama hizmetidir. App Service ile yapabilecekleriniz:

* Hızlı Oluştur bir [mobil uygulama](../app-service-mobile/app-service-mobile-value-prop.md) veya [API uygulaması](../app-service-api/app-service-api-apps-why-best-platform.md) toohost hello HTTP web hizmeti Azure'nın genel olarak dağıtılmış veri merkezlerinde birinde.
* Varolan hizmetlerini geçirme veya yenilerini oluşturun.
* Tek bir örnekle kullanılabilirlik SLA elde etmek veya ayrılmış toomultiple makineler ölçeklendirin.
* Kullanım hello mobil istemciler dahil olmak üzere site tooprovide REST API'leri tooany HTTP istemcilerinin, yayımladı.

> [!NOTE]
> Bir hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git<a href="https://trywebsites.azurewebsites.net/">https://trywebsites.azurewebsites.net</a>, burada hemen bir kısa süreli başlangıç uygulaması Azure App Service'te ücretsiz oluşturabilirsiniz. Kredi kartı gerekli, hiçbir taahhüt.
> 
> 

## <a id="nextsteps"></a>Sonraki adımlar
Merhaba üç web barındırma seçenekleri hakkında daha fazla bilgi için bkz: [Tanıtımı Azure](../fundamentals-introduction-to-azure.md).

Seçilen hello seçenekleri, uygulamanız için kullanmaya tooget kaynakları aşağıdaki hello bakın:

* [Azure App Service](/azure/app-service/)
* [Azure Cloud Services](/azure/cloud-services/)
* [Azure sanal makineler](/azure/virtual-machines/)
* [Service Fabric](/azure/service-fabric/)

<!-- URL List -->

[Azure App Service]: /azure/app-service/
[Cloud Services]: /azure/cloud-services/
[Virtual Machines]: /azure/virtual-machines/
[Service Fabric]: /azure/service-fabric/
[ClearDB]: http://www.cleardb.com/
[WebJobs]: http://go.microsoft.com/fwlink/?linkid=390226&clcid=0x409
[Configuring an SSL certificate for an Azure Website]: app-service-web-tutorial-custom-ssl.md
[azurestore]: https://azuremarketplace.microsoft.com/en-us/marketplace/apps
[scripting]: https://azure.microsoft.com/documentation/scripts/?services=web-sites
[dotnet]: https://azure.microsoft.com/develop/net/
[nodejs]: https://azure.microsoft.com/develop/nodejs/
[PHP]: https://azure.microsoft.com/develop/php/
[Python]: https://azure.microsoft.com/develop/python/
[servicebus]: /azure/service-bus/
[sqldatabase]: /azure/sql-database/
[Storage]: /azure/storage/

<!-- IMG List -->

[ChoicesDiagram]: ./media/choose-web-site-cloud-service-vm/Websites_CloudServices_VMs_3.png
