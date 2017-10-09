---
title: "aaaLearn Azure Service Fabric hakkında daha fazla bilgi | Microsoft Docs"
description: "Merhaba temel kavramlar ve Azure Service Fabric ana alanları hakkında bilgi edinin. Service Fabric genişletilmiş bir bakış sağlar ve nasıl toocreate mikro."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/14/2017
ms.author: ryanwi
ms.openlocfilehash: 7fe8de777755be11635912613bb5b970e3fe3ea3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="so-you-want-toolearn-about-service-fabric"></a>Service Fabric hakkında toolearn istediğiniz şekilde?
Azure Service Fabric kolay toopackage kolaylaştıran bir dağıtılmış sistemler platformudur, dağıtın ve ölçeklenebilir ve güvenilir mikro yönetin.  Ancak, büyük bir yüzey alanı Service Fabric sahiptir ve çok toolearn yok.  Bu makale, Service Fabric özeti sağlar ve modeller, uygulama yaşam döngüsü, test, kümeler ve sistem durumu izleme programlama hello temel kavramlarını açıklar. Okuma hello [genel bakış](service-fabric-overview.md) ve [mikro nelerdir?](service-fabric-overview-microservices.md) giriş ve Service Fabric kullanılan toocreate mikro nasıl olabilir. Bu makalede, kapsamlı bir içerik listesi içermiyor, ancak toooverview ve Service Fabric her alan için Başlarken makaleleri bağlantı. 

## <a name="core-concepts"></a>Temel kavramlar
[Service Fabric terminolojisi](service-fabric-technical-overview.md), [uygulama modeli](service-fabric-application-model.md), ve [desteklenen programlama modelleri](service-fabric-choose-framework.md) daha fazla kavramları ve açıklamalar sağlar, ancak hello temel kavramları şunlardır.

<table><tr><th>Temel kavramlar</th><th>Tasarım zamanı</th><th>Çalışma zamanı</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="./media/service-fabric-content-roadmap/CoreConceptsVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965"><img src="./media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">
<img src="./media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td></tr>
</table>

### <a name="design-time-application-type-service-type-application-package-and-manifest-service-package-and-manifest"></a>Tasarım zamanı: uygulama türü, hizmet türü, uygulama paketi ve bildirim, hizmet paketi ve bildirimi
Merhaba ad/sürüm tooa hizmet türleri koleksiyonunu atanmış bir uygulama türüdür. Bu tanımlanan bir *ApplicationManifest.xml* bir uygulama paketi dizininde ekli dosya. Merhaba uygulama paketi sonra kopyalanır toohello Service Fabric kümenin görüntü deposu. Merhaba küme içinde çalışan uygulama türünden bir adlandırılmış uygulama daha sonra oluşturabilirsiniz. 

Merhaba ad/sürüm tooa hizmetin kod paketler, veri paketleri ve yapılandırma paketleri atanmış bir hizmet türüdür. Bu, bir hizmet paketi dizinde katıştırılmış bir ServiceManifest.xml dosyasında tanımlanır. Merhaba hizmet paket dizinini sonra bir uygulama paketin tarafından başvuruda bulunulan *ApplicationManifest.xml* dosya. Merhaba küme içinde adlandırılmış bir uygulama oluşturduktan sonra adlandırılmış bir hizmet hello birinden uygulama türünün hizmet türleri oluşturabilirsiniz. Bir hizmet türü tarafından açıklanan kendi *ServiceManifest.xml* dosya. Çalışma zamanında yüklenir, yürütülebilir kod hizmeti yapılandırma ayarlarını ve hello hizmeti tarafından tüketilen statik verileri Hello hizmet türü oluşur.

![Service Fabric uygulama türleri ve hizmet türleri][cluster-imagestore-apptypes]

Merhaba uygulama paketi hello uygulama türü içeren bir disk dizindir *ApplicationManifest.xml* hello hizmet paketleri hello uygulama türü yapar her hizmet türü için başvuran dosya. Örneğin, e-posta uygulama türü için bir uygulama paketi başvuruları tooa sıra hizmet paketi, ön uç hizmet paketi ve veritabanı hizmet paketi içerebilir. Merhaba hello uygulama paketi dizinindeki kopyalanan toohello Service Fabric kümenin görüntü deposu dosyalarıdır. 

Bir hizmet paketi hello hizmet türü içeren bir disk dizindir *ServiceManifest.xml* hello kodu, statik verileri ve yapılandırma paketleri hello hizmet türünün başvuran dosya. Merhaba hizmet paketi dizinindeki Hello dosyaları hello uygulama türünün tarafından başvurulan *ApplicationManifest.xml* dosya. Örneğin, bir hizmet paketi toohello kodu, statik verileri ve veritabanı hizmeti oluşturan yapılandırma paketleri başvurabileceğiniz.

### <a name="run-time-clusters-and-nodes-named-applications-named-services-partitions-and-replicas"></a>Çalışma zamanı: kümeleri ve uygulamalar, hizmetler, bölümler ve çoğaltmalar adlı adlı düğümler
[Service Fabric kümesi](service-fabric-deploy-anywhere.md), mikro hizmetlerin dağıtılıp yönetildiği, ağa bağlı bir sanal veya fiziksel makine kümesidir. Kümeleri toothousands makinelerin ölçeklendirebilirsiniz.

Bir makine ya da bir kümenin parçasıysa VM düğüm denir. Her düğüme bir düğüm adı (dize) atanır. Düğümleri yerleşim özellikleri gibi özelliklere sahiptir. Her makine ya da VM bir otomatik başlatılan Windows hizmet sahip `FabricHost.exe`, önyükleme sırasında çalışmaya başlar ve ardından iki yürütülebilir dosyalar başlatır: `Fabric.exe` ve `FabricGateway.exe`. Bu iki yürütülebilir dosyalar hello düğümü olun. Geliştirme veya test senaryoları için birden çok örneğini çalıştırarak birden çok düğümde tek makine ya da VM barındırabilir `Fabric.exe` ve `FabricGateway.exe`.

Belirli bir işlevi veya işlevleri gerçekleştiren bir hizmetler koleksiyonunu içeren adlandırılmış bir adlandırılmış uygulamasıdır. Bir hizmet (bunu başlatmak ve diğer hizmetler bağımsız olarak çalışır) tam ve tek başına bir işlev gerçekleştirir ve kod, yapılandırma ve verileri oluşur. Bir uygulama paketi kopyalanan toohello Image store sonra hello uygulama paketin uygulama türü (kendi ad/sürüm kullanarak) belirterek hello uygulamasının hello küme içindeki bir örneğini oluşturun. Her uygulama türü örneğe benzer bir URI ad atanmış *fabric: / MyNamedApp*. Bir küme içinde tek bir uygulama türünden birden çok adlandırılmış uygulamaları oluşturabilirsiniz. Ayrıca, farklı uygulama türlerinden adlandırılmış uygulamaları oluşturabilirsiniz. Her adlandırılmış bağımsız olarak yönetilen ve sürümü tutulan uygulamasıdır.

Adlandırılmış bir uygulama oluşturduktan sonra hello hizmet türü (kendi ad/sürüm kullanarak) belirterek hello küme içinde kendi hizmet türleri (adlandırılmış bir hizmeti) bir örneğini oluşturabilirsiniz. Her hizmet türü örneği, adlandırılmış uygulamanın URI altında kapsamlı bir URI ad atanır. "Hizmet"uygulama adlı bir MyNamedApp"içinde adlı bir Veritabanım" oluşturursanız, örneğin, hello URI gibi görünüyor: *fabric: / MyNamedApp/Veritabanım*. Adlandırılmış bir uygulama içinde bir veya daha fazla adlandırılmış hizmetler oluşturabilirsiniz. Adlandırılmış her hizmetin kendi bölüm düzeni olabilir ve örnek/çoğaltma sayar. 

İki tür hizmet vardır: durum bilgisiz ve durum bilgisi. Durum bilgisi olmayan hizmetler kalıcı durum bir dış depolama hizmeti Azure Storage, Azure SQL Database veya Azure Cosmos DB gibi depolayabilirsiniz. Merhaba hizmet kalıcı depolama hiç varsa durum bilgisi olmayan bir hizmet kullanın. Bir durum bilgisi olan hizmet kendi güvenilir koleksiyonları veya Reliable Actors modellerini programlama aracılığıyla Hizmetinizin durumunu Service Fabric toomanage kullanır. 

Adlandırılmış hizmet oluşturulurken bir bölüm düzeni belirtin. Büyük miktarlarda durumu hizmetleriyle hello veri bölümler bölün. Her bölüm, bir kısmı hello tam hello kümenin düğümlere yayılır hello hizmetinin durumunu sorumludur. Durum bilgisi olan adlandırılmış Hizmetleri çoğaltmaları olsa da bir bölüm içinde durum bilgisiz adlandırılmış Hizmetleri örneğe sahip. Genellikle, hiçbir iç durumu sahip olduğu durum bilgisiz adlandırılmış hizmetleri her zaman sadece bir bölümü olmalıdır. Durum bilgisi olan hizmetler adlı korumak durumlarına çoğaltmaları ve her bir bölümü içinde kendi çoğaltma kümesi vardır. Okuma ve yazma işlemleri (Merhaba birincil olarak adlandırılır) bir yinelemede gerçekleştirilir. Yazma işlemleri gelen değişiklikler toostate toomultiple (etkin ikincil kopya olarak adlandırılır) diğer çoğaltmaları çoğaltılan. 

Merhaba Aşağıdaki diyagramda hello uygulamalar ve hizmet örnekleri, bölümler ve çoğaltmalar arasındaki ilişkiyi gösterir.

![Bölümler ve çoğaltmalar bir hizmet kapsamındaki][cluster-application-instances]

### <a name="partitioning-scaling-and-availability"></a>Bölümlendirme, ölçeklendirme ve kullanılabilirlik
[Bölümleme](service-fabric-concepts-partitioning.md) benzersiz tooService doku değil. Veri bölümlendirme veya parçalama bölümleme iyi bilinen biçimi değil. Durum bilgisi olan hizmetleri durumu büyük miktarlarda ile Merhaba veri bölümler bölün. Her bölüm hello tam hello hizmetinin durumunu bir kısmı için sorumludur. 

Her bölüm kopyalarını Hello adlandırılmış hizmetinizin durumu çok sağlayan hello kümenin düğümleri arasında yayılır[ölçek](service-fabric-concepts-scalability.md). Merhaba veri büyüme gereksinimlerine göre bölümleri büyümesine ve Service Fabric bölümleri düğümleri toomake verimli kullanımı, donanım kaynaklarına arasında yeniden dengeler. Yeni düğümler toohello kümesi eklerseniz, Service Fabric düğümleri artan hello sayısı hello çoğaltmalarını yeniden dengelemeniz. Genel uygulama performansını artıran ve erişim toomemory için çekişmeyi azaltır. Merhaba kümedeki Hello düğümler verimli bir şekilde kullanılmayan, hello hello kümedeki düğüm sayısını azaltabilirsiniz. Service Fabric yeniden hello çoğaltmalarını düğümleri toomake daha iyi kullanımı hello donanım her düğümde azaltılabilir hello sayısı arasında yeniden dengeler.

Durum bilgisi olan adlandırılmış Hizmetleri çoğaltmaları olsa da bir bölüm içinde durum bilgisiz adlandırılmış Hizmetleri örneğe sahip. Genellikle, hiçbir iç durumu sahip olduğu durum bilgisiz adlandırılmış hizmetleri her zaman sadece bir bölümü olmalıdır. Merhaba bölüm örnekleri sağlamak için [kullanılabilirlik](service-fabric-availability-services.md). Bir örnek başarısız olursa, diğer örnekleri toooperate normal şekilde devam edin ve ardından Service Fabric yeni bir örneğini oluşturur. Durum bilgisi olan hizmetler adlı korumak durumlarına çoğaltmaları ve her bir bölümü içinde kendi çoğaltma kümesi vardır. Okuma ve yazma işlemleri (Merhaba birincil olarak adlandırılır) bir yinelemede gerçekleştirilir. Yazma işlemleri gelen değişiklikler toostate toomultiple (etkin ikincil kopya olarak adlandırılır) diğer çoğaltmaları çoğaltılan. Bir çoğaltma işlemi başarısız olursa, Service Fabric hello mevcut çoğaltmaların yeni bir kopya oluşturur.

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Durum bilgisiz ve durum bilgisi olan mikro Service Fabric için
Service Fabric mikro veya kapsayıcıları oluşması toobuild uygulamaları etkinleştirir. Durum bilgisiz mikro (örneğin, protokol ağ geçitleri ve web proxy) dışında bir istek ve yanıt hello hizmetinden değişebilir bir duruma bulundurmayan. Azure bulut Hizmetleri çalışan rolleri, bir durum bilgisi olmayan hizmetin bir örnektir. Durum bilgisi olan mikro (örneğin, kullanıcı hesapları, veritabanları, aygıtlar, Alışveriş sepetleri ve Kuyruklar) değişebilir, yetkili durumu hello istek ve yanıt ötesinde korur. Bugünün Internet ölçekli uygulamalar durum bilgisiz ve durum bilgisi olan mikro birleşiminden oluşur. 

Service Fabric ile anahtar differentation hello ile ya da durum bilgisi olan hizmetler oluşturma, güçlü odaklanmasına olan [modellerini programlama yerleşik ](service-fabric-choose-framework.md) veya kapsayıcılı durum bilgisi olan hizmetler ile. Merhaba [uygulama senaryoları](service-fabric-application-scenarios.md) durum bilgisi olan hizmetler kullanıldığı hello senaryolar açıklanmaktadır.

Durum bilgisiz olanları birlikte durum bilgisi olan mikro neden var mı? Merhaba iki nedenler şunlardır:

* Yüksek verimlilik, düşük tutma kodla hataya dayanıklı çevrimiçi işlem işleme (OLTP) Hizmetleri ve kapatın verileri aynı makine hello Gecikmeli, oluşturabilirsiniz. Bazı, etkileşimli veriş, arama, nesnelerin interneti (IOT) sistemleri, ticaret sistemleri, kredi kartı işleme ve sahtekarlık algılama sistemleri ve kişisel kayıt yönetimi örnektir.
* Uygulama tasarımı basitleştirebilirsiniz. Durum bilgisi olan mikro ek sıraları hello gereksinimini kaldırın ve geleneksel olan önbellekleri tooaddress hello kullanılabilirlik ve gecikme süresi gereksinimlerine tamamen durum bilgisiz uygulama gerekli. Durum bilgisi olan doğal olarak yüksek kullanılabilirlik ve bir bütün olarak uygulamanızdaki taşıma bölümleri toomanage hello sayısını azaltan düşük-gecikme, hizmetleridir.

## <a name="supported-programming-models"></a>Desteklenen programlama modelleri
Service Fabric birden çok yol toowrite sunar ve hizmetlerinizi yönetin. Hizmetleri hello Service Fabric API'leri tootake tam anlamıyla hello platformun özellikleri ve uygulama çerçeveleri kullanabilirsiniz. Hizmetleri de herhangi dilinde yazılmıştır ve Service Fabric kümesi üzerinde barındırılan herhangi derlenmiş bir yürütülebilir program olabilir. Daha fazla bilgi için bkz: [desteklenen programlama modelleri](service-fabric-choose-framework.md).

### <a name="containers"></a>Kapsayıcılar
Varsayılan olarak, Service Fabric dağıtır ve Hizmetleri işlemler olarak etkinleştirir. Service Fabric da Hizmetleri'nde dağıtım [kapsayıcıları](service-fabric-containers-overview.md). Önemlisi, işlemleri Hizmetleri'nde ve Merhaba kapsayıcılara Hizmetleri'nde karıştırabilirsiniz aynı uygulama. Service Fabric Windows Server 2016 Linux kapsayıcıları Windows kapsayıcıları dağıtımını destekler. Var olan uygulamalar, durum bilgisi olmayan hizmetler veya durum bilgisi olan hizmetleri kapsayıcılarında dağıtabilirsiniz. 

### <a name="reliable-services"></a>Reliable Services
[Güvenilir hizmetler](service-fabric-reliable-services-introduction.md) hello Service Fabric platformu ile tümleştirme ve yararlı hello tam platform özellikleri kümesinden hizmetler yazmak için basit bir çerçevedir. Güvenilir hizmetler, durum bilgisiz (benzer toomost hizmet platformlar, web sunucuları veya çalışan rolleri Azure Cloud Services gibi), olabilir burada durumu kalıcıdır Azure DB veya Azure Table Storage gibi harici bir çözüm içinde. Güvenilir hizmetler, durum doğrudan hello hizmetinde kendisini güvenilir koleksiyonları kullanarak burada kalıcı durum bilgisi olan, da olabilir. Durum yapıldığında [yüksek oranda kullanılabilir](service-fabric-availability-services.md) çoğaltmayla ve aracılığıyla dağıtılmış [bölümleme](service-fabric-concepts-partitioning.md), tüm yönetilen Service Fabric tarafından otomatik olarak.

### <a name="reliable-actors"></a>Reliable Actors
Güvenilir hizmetler en üstünde oluşturulan hello [güvenilir aktör](service-fabric-reliable-actors-introduction.md) çerçevedir hello aktör tasarım deseni temel alınarak hello sanal aktör deseni uygulayan bir uygulama çerçevesi. Merhaba güvenilir aktör çerçevesi yürütme aktörler olarak adlandırılan tek iş parçacıklı işlem ve durumunun bağımsız bir birim kullanır. Merhaba güvenilir bir çerçeve sağlar aktör iletişimi aktörler ve önceden ayarlanmış durumu kalıcılığını ve genişleme yapılandırmaları için yerleşik.

### <a name="aspnet-core"></a>ASP.NET Çekirdeği
Service Fabric tümleşir [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) olarak web ve API uygulamaları oluşturmak için birinci sınıf bir programlama modeli

### <a name="guest-executables"></a>Konuk yürütülebilir dosyalar
A [Konuk yürütülebilir](service-fabric-deploy-existing-app.md) olduğu diğer hizmetlerin yanı sıra bir Service Fabric kümesi üzerinde barındırılan (herhangi bir dilde yazılmış) var olan, rasgele çalıştırılabilir. Konuk yürütülebilir dosyaları doğrudan hizmet doku API'leri ile tümleştirmeye değil. Ancak özelliklerinden'bunlar hala yararlanır özel durumu gibi platform teklifleri hello raporlama yük ve REST API'ları çağırarak bulunabilirliği hizmet. Aynı zamanda tam uygulama yaşam döngüsü destek sahiptirler. 

## <a name="application-lifecycle"></a>Uygulama yaşam döngüsü
Diğer platformlar ile bir uygulama Service Fabric genellikle aşamaları aşağıdaki hello geçtikçe: tasarım, geliştirme, test, dağıtım, yükseltme, Bakım ve kaldırma. Service Fabric, bulut uygulamalarından geliştirme aşamasından dağıtım, günlük yönetim ve Bakım tooeventual yetkisini hello tam uygulama yaşam döngüsü için birinci sınıf destek sağlar. Merhaba hizmet modeli hello uygulama yaşam döngüsü, bağımsız olarak birçok farklı roller tooparticipate sağlar. [Service Fabric uygulama yaşam döngüsü](service-fabric-application-lifecycle.md) hello API'leri genel bir bakış ve hello hello Service Fabric uygulama yaşam döngüsü aşamaları boyunca hello farklı rolleri tarafından nasıl kullanıldıkları sağlar. 

Merhaba tüm uygulama yaşam döngüsü kullanılarak yönetilebilir [PowerShell cmdlet'leri](/powershell/module/ServiceFabric/), [C# API'leri](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient), [Java API](/java/api/system.fabric._application_management_client), ve [REST API'leri](/rest/api/servicefabric/). Gibi araçları kullanılarak sürekli tümleştirme/sürekli dağıtım ardışık düzen de ayarlayabilirsiniz [Visual Studio Team Services](service-fabric-set-up-continuous-integration.md) veya [Jenkins](service-fabric-cicd-your-linux-java-application-with-jenkins.md).

Merhaba aşağıdaki Microsoft Virtual Academy video açıklar nasıl toomanage, uygulama yaşam döngüsü:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=My3Ka56yC_6106218965">
<img src="./media/service-fabric-content-roadmap/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="test-applications-and-services"></a>Uygulama ve hizmetleri test etme
toocreate gerçekten bulut ölçekli Hizmetleri, uygulamaları ve Hizmetleri gerçek hataları dayanabilir kritik tooverify ise. Merhaba hata analizi hizmeti Service Fabric yerleşik Hizmetleri test etmek için tasarlanmıştır. Merhaba ile [hata analizi hizmeti](service-fabric-testability-overview.md), anlamlı hataları anlamına ve tam test senaryoları uygulamalarınızı karşı çalıştırmak. Bu hataları ve senaryoları uygulamanız ve doğrulama çok sayıda durumları ve hizmet yaşam süresi boyunca, tüm bir denetimli, güvenli ve tutarlı şekilde yaşar geçişleri hello.

[Eylemler](service-fabric-testability-actions.md) tek tek hataları kullanarak test etmek için bir hizmet hedefi. Bir hizmet Geliştirici yapı taşları toowrite karmaşık senaryolar olarak kullanabilirsiniz. Benzetimli hataları örnekleri şunlardır:

* Bir düğüm toosimulate olduğu bir makineye veya VM yeniden durumlarda herhangi bir sayıda yeniden başlatın.
* Bir çoğaltma, durum bilgisi olan hizmet toosimulate Yük Dengeleme, yük devretme veya uygulama yükseltme taşıyın.
* Çekirdek kayıp durum bilgisi olan hizmet toocreate yeterli "yedek" veya "ikincil" çoğaltmaları tooaccept yeni veri olmadığından burada yazma işlemleri devam edemiyor bir durum olarak çağırır.
* Durum bilgisi olan hizmet toocreate burada tüm bellek içi durumu tamamen silinmeden çıkışı bir durum veri kaybı çağırır.

[Senaryolar](service-fabric-testability-scenarios.md) karmaşık işlemleri bir veya daha fazla Eylemler oluşur. Hello hata analizi hizmeti, iki yerleşik tam senaryoları sağlar:

* [Chaos senaryo](service-fabric-controlled-chaos.md)-uzun süreler boyunca hello küme boyunca sürekli, araya eklemeli hataları (normal ve durunda) benzetimini yapar.
* [Yük devretme senaryosu](service-fabric-testability-scenarios.md#failover-test)-diğer hizmetler etkilenmemesini bırakarak belirli hizmet bölüm hedefler hello chaos testi senaryosu sürümü.

## <a name="clusters"></a>Kümeleri
[Service Fabric kümesi](service-fabric-deploy-anywhere.md), mikro hizmetlerin dağıtılıp yönetildiği, ağa bağlı bir sanal veya fiziksel makine kümesidir. Kümeleri toothousands makinelerin ölçeklendirebilirsiniz. Bir küme düğümü bir makine ya da bir kümenin parçasıysa VM adı verilir. Her düğüme bir düğüm adı (dize) atanır. Düğümleri yerleşim özellikleri gibi özelliklere sahiptir. Her makine ya da VM otomatik başlatılan hizmet sahip `FabricHost.exe`, önyükleme sırasında çalışmaya başlar ve ardından iki yürütülebilir dosyalar başlatır: Fabric.exe ve FabricGateway.exe. Bu iki yürütülebilir dosyalar hello düğümü olun. Senaryoları test etmek için bir tek makine ya da VM birden çok düğümde birden çok örneğini çalıştırarak barındırabilir `Fabric.exe` ve `FabricGateway.exe`.

Service Fabric kümeleri, Windows Server veya Linux çalıştıran sanal veya fiziksel makineler üzerinde oluşturulabilir. Mümkün toodeploy olan ve Service Fabric uygulamaları birbirine bağlı bir Windows Server veya Linux bilgisayarlar kümesi sahip olduğu herhangi bir ortamda çalıştırılabilir: şirket içi, Microsoft Azure veya herhangi bir bulut sağlayıcısı.

Merhaba aşağıdaki Microsoft Virtual Academy video Service Fabric kümeleri açıklanmaktadır:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="./media/service-fabric-content-roadmap/ClusterOverview.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="clusters-on-azure"></a>Azure’da kümeler
Service Fabric kümeleri Azure üzerinde çalışan işlemleri ve hello küme yönetimi daha kolay ve daha güvenilir yapar diğer Azure özellikleri ve Hizmetleri ile tümleştirme sağlar. Azure'daki diğer kaynakları gibi kümeleri model için bir Azure Resource Manager kaynak kümedir. Kaynak Yöneticisi'ni de tek bir birim olarak hello küme tarafından kullanılan tüm kaynakları kolay yönetim sağlar. Azure kümelerinde Azure tanılama ve günlük analizi ile tümleşiktir. Küme düğümü türleri [sanal makine ölçek kümeleri](/azure/virtual-machine-scale-sets/index), otomatik ölçeklendirmeyi işlevsellik oluşturulmuştur.

Bir küme Azure'da hello oluşturabilirsiniz [Azure portal](service-fabric-cluster-creation-via-portal.md), gelen bir [şablonu](service-fabric-cluster-creation-via-arm.md), veya [Visual Studio](service-fabric-cluster-creation-via-visual-studio.md).

Service Fabric Linux'ta Hello önizlemesini toobuild sağlar, dağıtın ve Linux üzerinde yüksek oranda kullanılabilir, ölçeklendirilebilir uygulamalar Windows üzerinde gibi yönetin. Merhaba Service Fabric çerçeveler (Reliable Services ve Reliable Actors) toplama tooC # (.NET Core) Linux üzerinde Java mevcuttur. Ayrıca, oluşturabilirsiniz [Konuk yürütülebilir Hizmetleri](service-fabric-deploy-existing-app.md) herhangi bir dil veya framework ile. Ayrıca, hello Önizleme yönetme Docker kapsayıcıları destekler. Docker kapsayıcıları Konuk yürütülebilir dosyalar veya hello Service Fabric çerçeveler kullanan yerel Service Fabric hizmetler çalıştırabilirsiniz. Daha fazla bilgi için okuma [Service Fabric Linux'ta](service-fabric-linux-overview.md).

Linux üzerindeki Service Fabric önizleme aşamasında olduğundan, Windows’ta desteklenip Linux’ta desteklenmeyen bazı özellikler mevcuttur. toolearn daha fazlasını okuyun [Service Fabric Linux ve Windows arasındaki farklar](service-fabric-linux-windows-differences.md).

### <a name="standalone-clusters"></a>Tek başına kümeler
Service Fabric bir yükleme paketi, toocreate tek başına Service Fabric kümeleri şirket içi veya herhangi bir bulut sağlayıcısına sağlar. Tek başına istediğiniz yere özgürlük toohost bir küme hello verin kümeleri. Verileriniz konu toocompliance veya yasal sınırlamalar bulunur veya veri yerel tookeep istiyorsanız kendi küme ve uygulamalarını barındırabilir. Bir barındırma ortamı tooanother uygulamaları oluşturma bilginiz taşıyan için Service Fabric uygulamaları herhangi bir değişiklik ile birden çok barındırma ortamlarında çalıştırabilirsiniz. 

[İlk Service Fabric tek başına kümenizi oluşturun](service-fabric-get-started-standalone-cluster.md)

Linux tek başına kümelerinin henüz desteklenmiyor.

### <a name="cluster-security"></a>Küme güvenliği
Kümeleri özellikle üretim iş yükleri üzerinde çalıştırılan olduğunda tooyour küme bağlanma güvenli tooprevent yetkisiz kullanıcıların olması gerekir. Olası toocreate güvenli olmayan bir küme olmasına rağmen Bunun yapılması yönetim uç noktaları varsa anonim kullanıcılar tooconnect tooit açığa toohello sağlayan ortak Internet. Olası toolater etkinleştir güvenlik güvenli olmayan bir kümede olmadığından: küme güvenlik, küme oluşturma sırasında etkindir.

Merhaba küme güvenlik senaryolar şunlardır:
* Düğümü düğümü güvenlik
* İstemcisi düğümü güvenlik
* Rol tabanlı erişim denetimi (RBAC)

Daha fazla bilgi için okuma [bir küme güvenli](service-fabric-cluster-security.md).

### <a name="scaling"></a>Ölçeklendirme
Yeni düğümler toohello kümesi eklerseniz, Service Fabric hello çoğaltmalarını ve örnekleri düğümleri artan hello sayısı arasında yeniden dengeler. Genel uygulama performansını artıran ve erişim toomemory için çekişmeyi azaltır. Merhaba kümedeki Hello düğümler verimli bir şekilde kullanılmayan, hello hello kümedeki düğüm sayısını azaltabilirsiniz. Service Fabric yeniden hello çoğaltmalarını yeniden dengeler ve her düğümde hello donanım düğümleri toomake azaltılabilir hello sayısı örneklerinde daha iyi kullanın. Azure kümelerinde ya da ölçeklendirebilirsiniz [el ile](service-fabric-cluster-scale-up-down.md) veya [program aracılığıyla](service-fabric-cluster-programmatic-scaling.md). Tek başına kümelerinin Genişletilmiş [el ile](service-fabric-cluster-windows-server-add-remove-nodes.md).

### <a name="cluster-upgrades"></a>Küme yükseltme
Merhaba Service Fabric çalışma zamanı yeni sürümleri düzenli aralıklarla yayınlanır. Çalışma zamanı ya da doku, yükseltmeler, kümenizde gerçekleştirin, böylelikle her zaman çalıştırdığınız bir [sürümünü desteklenen](service-fabric-support.md). Ayrıca toofabric yükseltir, sertifikalar veya uygulama bağlantı noktaları gibi küme yapılandırması da güncelleştirebilirsiniz.

Service Fabric kümesi sahip, ancak kısmen Microsoft tarafından yönetilen bir kaynaktır. Microsoft, işletim sistemi temelindeki ve fabric yükseltmelerinin kümenizde gerçekleştirme düzeltme eki uygulama hello sorumludur. Microsoft yeni bir sürümü yayımlandığında yükseltmeler, küme tooreceive otomatik dokunuz ayarlamayın veya tooselect istediğiniz desteklenen fabric sürümü seçin. Yapı ve yapılandırma yükseltmeleri hello Azure portalı üzerinden veya Kaynak Yöneticisi aracılığıyla ayarlanabilir. Daha fazla bilgi için okuma [Service Fabric kümesi yükseltme](service-fabric-cluster-upgrade.md). 

Tek başına küme bir kaynaktır, tamamen kendi. İşletim sistemi temelindeki ve fabric yükseltmelerinin başlatma düzeltme eki uygulama Merhaba sorumlu. Kümenizi çok bağlanabiliyorsa[https://www.microsoft.com/download](https://www.microsoft.com/download), küme tooautomatically karşıdan ayarlayabilir ve sağlama hello yeni Service Fabric çalışma zamanı paketi. Ardından hello yükseltme başlatmak. Kümenizi erişemiyorsanız [https://www.microsoft.com/download](https://www.microsoft.com/download), el ile bir Internet bağlantılı makineden hello yeni çalışma zamanı paketini indirin ve ardından hello yükseltme başlatın. Daha fazla bilgi için okuma [bir tek başına Service Fabric kümesi yükseltme](service-fabric-cluster-upgrade-windows-server.md).

## <a name="health-monitoring"></a>Sistem durumunu izleme
Service Fabric tanıtır bir [sistem durumu modeli](service-fabric-health-introduction.md) tasarlanmış tooflag sağlıksız küme ve uygulama koşullara belirli varlıkları (örneğin, küme düğümlerini ve hizmet çoğaltmaları). Merhaba sistem durumu modeli sistem durumu reporters (sistem bileşenleri ve watchdogs) kullanır. Merhaba kolay ve hızlı tanı ve onarım hedeftir. Hizmeti yazıcıları önceden sistem durumu hakkında toothink gerekir ve nasıl çok[sistem durumu raporlama tasarım](service-fabric-report-health.md#design-health-reporting). Özellikle, toohello kök kapatmak bayrağı sorunları yardımcı olur, sistem durumu etkileyebilir herhangi bir koşul, bildirilmelidir. Merhaba sistem durumu bilgileri, hata ayıklama ve hello hizmetin çalışır durumda bir kez araştırma ve çalışan ölçekli üretim zaman ve çaba kaydedebilirsiniz.

Merhaba Service Fabric reporters İzleyici faiz koşullarını tanımlanmış. Kendi yerel bir görünümü temel alarak bu koşullara bildirin. Merhaba [sistem durumu deposu](service-fabric-health-introduction.md#health-store) varlıklar genel sağlıklı olup tüm reporters toodetermine tarafından gönderilen sistem durumu verileri toplar. Merhaba, hedeflenen toobe zengin, esnek ve kolay toouse modelidir. Merhaba sistem durumu raporlarının Hello kalitesini hello küme hello sistem durumu görünümünü hello doğruluğunu belirler. Yanlış sağlıksız sorunları göstermek hatalı pozitif sonuç, yükseltme veya sistem durumu verileri kullanan diğer hizmetler olumsuz yönde etkileyebilir. Bu tür hizmetlerin onarım hizmetleri ve uyarı mekanizmaları gösterilebilir. Bu nedenle, bazı düşünce hello ilgi koşullarını yakalama gerekli tooprovide raporları olan en iyi olası yol.

Raporlama alanından yapılabilir:
* Merhaba, Service Fabric hizmeti çoğaltma veya örnek izlenen.
* İç watchdogs Service Fabric hizmeti (koşullar izler ve raporları sorunları Örneğin, bir Service Fabric durum bilgisiz hizmet) dağıtılmış. Merhaba watchdogs tüm düğümler üzerinde dağıtılabilir veya izlenen Benzetilen toohello hizmet olabilir.
* Merhaba Service Fabric düğümlerinde çalıştırın, ancak Service Fabric Hizmetleri olarak uygulanmamıştır iç watchdogs.
* Dış dış hello Service Fabric kümesi (örneğin, izleme hizmeti Gomez gibi) Bu araştırma hello kaynaktan watchdogs.

Merhaba kutudan çıktığında, Service Fabric bileşenleri hello kümedeki tüm varlıklar sistem durumu raporlamak. [Sistem durumu raporlarını](service-fabric-understand-and-troubleshoot-with-system-health-reports.md) küme ve uygulama işlevselliğini ve bayrağı sorunları sistem durumu aracılığıyla görünürlük sağlar. Uygulamalar ve hizmetler için sistem durumu raporlarını varlıkları uygulanır ve doğru şekilde hello hello Service Fabric çalışma zamanı perspektifinden davranmakta olduğunu doğrulayın. Merhaba raporları tüm sistem durumu izleme hello hizmetinin iş mantığını hello sağlamaz veya askıdaki işlemleri algılamak. tooadd sistem durumu bilgileri belirli tooyour hizmetin mantığı [özel durumu raporlama uygulamak](service-fabric-report-health.md) hizmetinizde.

Service Fabric birden çok yol çok sağlar[görüntülemek sistem durumu raporlarının](service-fabric-view-entities-aggregated-health.md) hello health store içinde toplanır:
* [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) veya diğer görsel araçlar.
* Sistem durumu sorgularının (aracılığıyla [PowerShell](/powershell/module/ServiceFabric/), hello [C# FabricClient API'leri](/api/system.fabric.fabricclient.healthclient) ve [Java FabricClient API'leri](/java/api/system.fabric._health_client), veya [REST API'leri](/rest/api/servicefabric)).
* Varlıklar listesi döndüren genel sorgular sistem durumu (aracılığıyla, PowerShell, hello API veya REST) hello özelliklerinden biri olarak vardır.

Merhaba, aşağıdaki Microsoft Virtual Academy video hello Service Fabric sistem durumu modeli ve nasıl kullanıldığı açıklanmaktadır:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tevZw56yC_1906218965">
<img src="./media/service-fabric-content-roadmap/HealthIntroVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="next-steps"></a>Sonraki adımlar
* Bilgi nasıl toocreate bir [Azure kümesinde](service-fabric-cluster-creation-via-portal.md) veya [Windows tek başına kümede](service-fabric-cluster-creation-for-windows-server.md).
* Hello kullanarak bir hizmet oluşturmayı deneyin [Reliable Services](service-fabric-reliable-services-quick-start.md) veya [Reliable Actors](service-fabric-reliable-actors-get-started.md) modellerini programlama.
* Nasıl çok öğrenin[bulut hizmetlerinden geçiş](service-fabric-cloud-services-migration-differences.md).
* Çok öğrenin[izlemek ve Hizmetleri tanılamak](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). 
* Çok öğrenin[uygulamaları ve Hizmetleri test](service-fabric-testability-overview.md).
* Çok öğrenin[yönetmek ve küme kaynaklarının düzenlemek](service-fabric-cluster-resource-manager-introduction.md).
* Merhaba Ara [Service Fabric örnekleri](http://aka.ms/servicefabricsamples).
* Hakkında bilgi edinin [Service Fabric destek seçenekleri](service-fabric-support.md).
* Okuma hello [blog ekip](https://blogs.msdn.microsoft.com/azureservicefabric/) makaleleri ve duyuruları için.


[cluster-application-instances]: media/service-fabric-content-roadmap/cluster-application-instances.png
[cluster-imagestore-apptypes]: ./media/service-fabric-content-roadmap/cluster-imagestore-apptypes.png
