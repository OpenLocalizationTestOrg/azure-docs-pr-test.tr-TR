---
title: "Azure Service Fabric terminolojisi öğrenin | Microsoft Docs"
description: "Service Fabric terminolojisi bakış. Önemli terminolojiyi kavramlar ve belgelere geri kalanı kullanılan terimler açıklanmaktadır."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: chackdan;subramar
ms.assetid: 3a970679-e19e-43b3-9be8-71773f307c57
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/02/2017
ms.author: ryanwi
ms.openlocfilehash: 42e5e651d5a3c08e829b48bb47e14458a5c65900
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-terminology-overview"></a>Service Fabric terminolojisi genel bakış
Service Fabric paketi, dağıtmak ve ölçeklenebilir ve güvenilir mikro kolaylaştıran bir dağıtılmış sistemler platformudur. Bu konuda belgelerde kullanılan terimler anlamak için Service Fabric tarafından kullanılan terminolojiyi ayrıntılarını verir.

Bu bölümde listelenen kavramları aşağıdaki Microsoft Virtual Academy videoları ele alınmıştır: <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">temel kavramları</a>, <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965">tasarım zamanı kavramları</a>, ve <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">çalışma zamanı kavramları</a>.

## <a name="infrastructure-concepts"></a>Altyapı kavramları
**Küme**: içine, mikro dağıtılır ve yönetilen sanal veya fiziksel makineler ağa bağlı bir dizi.  Kümeleri makineler binlerce ölçeklendirebilirsiniz.

**Düğüm**: makine ya da bir kümenin parçasıysa VM bir düğüm olarak adlandırılır. Her düğüme bir düğüm adı (dize) atanır. Düğümleri yerleşim özellikleri gibi özelliklere sahiptir. Her makine ya da VM bir otomatik başlatılan Windows hizmet sahip `FabricHost.exe`, önyükleme sırasında çalışmaya başlar ve ardından iki yürütülebilir dosyalar başlatır: `Fabric.exe` ve `FabricGateway.exe`. Bu iki yürütülebilir dosyalar düğümü olun. Senaryoları test etmek için bir tek makine ya da VM birden çok düğümde birden çok örneğini çalıştırarak barındırabilir `Fabric.exe` ve `FabricGateway.exe`.

## <a name="application-concepts"></a>Uygulama kavramları
**Uygulama türü**: hizmet türlerinin bir koleksiyona atanan ad/sürüm. İçinde tanımlanan bir `ApplicationManifest.xml` dosyasının, ardından Service Fabric kümenin görüntü deposuna kopyalanır bir uygulama paketi dizini katıştırılmış. Bu uygulama türü küme içindeki bir adlandırılmış uygulama sonra oluşturabilirsiniz.

Okuma [uygulama modeli](service-fabric-application-model.md) daha fazla bilgi için makalenin.

**Uygulama paketi**: uygulama tür içeren bir disk dizini `ApplicationManifest.xml` dosya. Uygulama türü yapar her hizmet türünün hizmet paketleri başvurur. Uygulama paketi dizindeki dosyaların Service Fabric kümenin görüntü deposuna kopyalanır. Örneğin, e-posta uygulama türü için bir uygulama paketi sırası hizmet paketi, ön uç hizmet paketi ve veritabanı hizmet paketi başvurular içerebilir.

**Uygulama adlı**: bir uygulama paketi görüntü deposuna kopyalandıktan sonra küme içindeki uygulama örneğini uygulama paketin uygulama türü (kendi ad/sürüm kullanarak) belirterek oluşturun. Her uygulama türü örneği benzer bir URI ad atanır: `"fabric:/MyNamedApp"`. Bir küme içinde tek bir uygulama türünden birden çok adlandırılmış uygulamaları oluşturabilirsiniz. Ayrıca, farklı uygulama türlerinden adlandırılmış uygulamaları oluşturabilirsiniz. Her adlandırılmış bağımsız olarak yönetilen ve sürümü tutulan uygulamasıdır.      

**Hizmet türü**: bir hizmetin kod paketler, veri paketleri ve yapılandırma paketleri atanan ad/sürüm. İçinde tanımlanan bir `ServiceManifest.xml` dosyasının, bir hizmet paketi dizini ve hizmet paketi dizininde katıştırılmış sonra bir uygulama paketin tarafından başvurulan `ApplicationManifest.xml` dosya. Küme içinde adlandırılmış bir uygulama oluşturduktan sonra adlandırılmış bir hizmet uygulaması tür hizmet türlerinden birini oluşturabilirsiniz. Hizmet türünün `ServiceManifest.xml` dosya hizmeti tanımlar.

Okuma [uygulama modeli](service-fabric-application-model.md) daha fazla bilgi için makalenin.

İki tür hizmet vardır:

* **Stateless:** hizmetin kalıcı durumunu Azure Storage, Azure SQL Database veya Azure Cosmos DB gibi bir harici depolama hizmetindeki depolandığında durumsuz bir hizmet kullanın. Hizmet kalıcı depolama hiç varsa, durum bilgisi olmayan bir hizmet kullanın. Burada değerler hizmete geçirilir, bir hesaplama bu değerleri kullanılarak gerçekleştirilir ve bir sonuç döndürdü Örneğin, bir hesap makinesi hizmeti.
* **Durum bilgisi olan:** Hizmetinizin durumunu kendi güvenilir koleksiyonları veya Reliable Actors modellerini programlama aracılığıyla yönetmek için Service Fabric istediğinizde, durum bilgisi olan bir hizmet kullanın. İstediğiniz kaç bölümleri (için ölçeklenebilirlik) üzerinden durumunuza yayılan belirttiğinizde adlandırılmış bir hizmet oluşturuluyor. Ayrıca, durumunuza düğümleri (için güvenilirlik) üzerinden çoğaltmak için kaç kez belirtin. Tek bir birincil çoğaltma ve birden fazla ikincil çoğaltmaları her adlandırılmış hizmetin vardır. Birincil çoğaltmayı yazarak adlandırılmış Hizmetinizin durumunu değiştirin. Service Fabric, bu durum, durumu eşitlenmiş şekilde kalmasının tüm ikincil çoğaltmalar için sonra çoğaltır. Birincil çoğaltma işlemi başarısız olur ve var olan bir ikincil çoğaltma birincil çoğaltmaya yükseltir Service Fabric otomatik olarak algılar. Service Fabric daha sonra yeni bir ikincil çoğaltma oluşturur.  

**Hizmet paketi**: hizmet türünün içeren bir disk dizini `ServiceManifest.xml` dosya. Bu dosya kodu, statik verileri ve yapılandırma paketleri hizmet türünün başvurur. Hizmet paketi dizindeki dosyaların uygulama tür tarafından başvurulan `ApplicationManifest.xml` dosya. Örneğin, bir hizmet paketi, kod, statik verileri ve veritabanı hizmeti oluşturan yapılandırma paketleri başvurabileceğiniz.

**Adlı hizmetin**: adlandırılmış bir uygulama oluşturduktan sonra küme içindeki hizmet türlerinden birini örneği (kendi ad/sürüm kullanarak) hizmet türü belirterek oluşturabilirsiniz. Her hizmet türü örneği, adlandırılmış uygulamanın URI altında kapsamlı bir URI ad atanır. "Hizmet"uygulama adlı bir MyNamedApp"içinde adlı bir Veritabanım" oluşturursanız, örneğin, URI gibi görünüyor: `"fabric:/MyNamedApp/MyDatabase"`. Adlandırılmış bir uygulama içinde birden fazla adlandırılmış hizmetler oluşturabilirsiniz. Adlandırılmış her hizmetin kendi bölüm düzeni olabilir ve örnek/çoğaltma sayar.

**Paket kod**: hizmet türünün yürütülebilir dosyaları (genellikle EXE/DLL dosyaları) içeren bir disk dizini. Kod paketi dizindeki dosyaların hizmet türünün tarafından başvurulan `ServiceManifest.xml` dosya. Adlandırılmış bir hizmet oluşturulduğunda, kod paketi düğüme veya adlandırılmış hizmetini çalıştırmak için seçili düğümlere kopyalanır. Ardından kod çalışmaya başlar. Kod Paketi yürütülebilir dosyalar iki tür vardır:

* **Konuk yürütülebilir dosyalar**: Farklı Çalıştır yürütülebilir dosyalar-ana bilgisayar işletim sistemindeki (Windows veya Linux). Diğer bir deyişle, bu yürütülebilir dosyalar değil bağlamak veya herhangi bir Service Fabric çalışma zamanı dosya başvuru ve bu nedenle yapmak modellerini programlama herhangi Service Fabric kullanmayın. Bu yürütülebilir dosyaları Adlandırma Hizmeti uç noktası bulma gibi bazı Service Fabric özelliklerini kullanma sorunu yaşıyor. Konuk yürütülebilir dosyaları her bir hizmet örneğine yük ölçümleri belirli raporlayamazsınız.
* **Hizmet ana yürütülebilir dosyalar**: Service Service Fabric çalışma zamanı dosyaları bağlayarak modellerini programlama Service Fabric özelliklerini etkinleştirme Fabric kullanan yürütülebilir. Örneğin, bir adlandırılmış hizmet örneği uç noktaları Service Fabric'ın adlandırma hizmeti ile kaydedebilir ve yük ölçümleri de bildirebilirsiniz.      

**Veri paketi**: hizmet türünün statik ve salt okunur veri dosyaları (genellikle fotoğraf, ses ve video dosyaları) içeren bir disk dizini. Veri paketi dizindeki dosyaların hizmet türünün tarafından başvurulan `ServiceManifest.xml` dosya. Adlandırılmış bir hizmet oluşturulduğunda, veri paketi düğüme veya adlandırılmış hizmetini çalıştırmak için seçili düğümlere kopyalanır.  Kod çalışmaya başlar ve artık veri dosyalarına erişebilir.

**Yapılandırma paketi**: hizmet türünün statik ve salt okunur yapılandırma dosyaları (genellikle metin) içeren bir disk dizini. Yapılandırma paketi dizindeki dosyaların hizmet türünün tarafından başvurulan `ServiceManifest.xml` dosya. Adlandırılmış bir hizmet oluşturulduğunda, yapılandırma paketteki dosyaların adlandırılmış hizmetini çalıştırmak üzere seçilen bir veya daha fazla düğümleri kopyalanır. Ardından kod çalışmaya başlar ve yapılandırma dosyalarını şimdi erişebilir.

**Kapsayıcıları**: varsayılan olarak, Service Fabric dağıtır ve Hizmetleri işlemler olarak etkinleştirir. Service Fabric kapsayıcı görüntüleri Hizmetleri'nde de dağıtabilirsiniz. Uygulamaları temel işletim sisteminden sanallaştıran sanallaştırma teknolojisi kapsayıcılardır. Bir uygulama ve çalışma zamanı, bağımlılıklar ve sistem başlatılamadığından kapsayıcısı içindeki işletim sistemi yapıları yalıtılmış kapsayıcının kendi görünümüne tam, özel erişim ile çalıştırın. Service Fabric, Linux ve Windows Server kapsayıcılarında Docker kapsayıcıları destekler.  Daha fazla bilgi için okuma [Service Fabric ve kapsayıcıları](service-fabric-containers-overview.md).

**Bölüm düzeni**: adlandırılmış hizmet oluşturulurken bir bölüm düzeni belirtin. Büyük miktarlarda durumu hizmetleriyle durumu küme düğümleri arasında yayar bölümleri arasında verileri bölün. Bu ölçeklendirmek adlandırılmış Hizmetinizin durumunu sağlar. Durum bilgisi olan adlandırılmış Hizmetleri çoğaltmaları olsa da bir bölüm içinde durum bilgisiz adlandırılmış Hizmetleri örneğe sahip. Genellikle, hiçbir iç durumu sahip olduğu durum bilgisiz adlandırılmış hizmetleri her zaman sadece bir bölümü olmalıdır. Bölüm örnekleri için kullanılabilirlik sağlar; bir örnek başarısız olursa, diğer örnekleri normal şekilde çalışmaya devam eder ve ardından Service Fabric yeni bir örneğini oluşturur. Durum bilgisi olan hizmetler adlı korumak eşitlenmiş olarak tutulduğunu tüm durumu ile kendi çoğaltma çoğaltmaları ve her bölüm içinde durumlarına sahiptir. Bir çoğaltma işlemi başarısız olursa, Service Fabric mevcut çoğaltmaların yeni bir kopya oluşturur.

Okuma [bölüm Service Fabric güvenilir hizmetler](service-fabric-concepts-partitioning.md) daha fazla bilgi için makalenin.

## <a name="system-services"></a>Sistem Hizmetleri
Service Fabric platform özelliklerini sağlayan her kümede oluşturulan sistem hizmetleri vardır.

**Adlandırma Hizmeti**: her Service Fabric kümesi, küme içindeki bir konuma hizmet adlarını çözümleyen bir adlandırma hizmeti sahiptir. Hizmet adları ve özellikleri, bir internet'e benzer yönettiğiniz etki alanı adı hizmeti (DNS) küme için. İstemciler, bir hizmet adı ve konumu çözümlemek için adlandırma hizmeti kullanmada kümedeki herhangi bir düğümün ile güvenli bir şekilde iletişim kurar.  Örneğin hataları, kaynak Dengeleme ya da nedeniyle kümesini yeniden boyutlandırma kümedeki uygulamaları taşıyın. Hizmetler ve geçerli ağ konumu çözümlemek istemcileri geliştirebilirsiniz. İstemciler gerçek Makine IP adresi ve bağlantı noktası şu anda çalıştığı edinin.

Okuma [Hizmetleri ile iletişim kurun](service-fabric-connect-and-communicate-with-services.md) hizmet ve istemci iletişimi adlandırma hizmeti ile çalışacak API'ler hakkında daha fazla bilgi için.

**Görüntü Deposu hizmetini**: her Service Fabric kümesi dağıtılan, sürümlü uygulama paketleri tutulduğu bir görüntü Deposu hizmetini sahiptir. Bir uygulama paketi görüntü deposuna kopyalama ve uygulama paket içinde bulunan uygulama türünün kaydedin. Uygulama türü sağlandıktan sonra adlandırılmış uygulama ondan oluşturun. Tüm adlandırılmış uygulamaları sildikten sonra Image Store hizmetinden uygulama türü kaydını kaldırabilirsiniz.

Okuma [ImageStoreConnectionString ayarı anlamak](service-fabric-image-store-connection-string.md) Image Store hizmeti hakkında daha fazla bilgi için.

Okuma [bir uygulamayı dağıtmak](service-fabric-deploy-remove-applications.md) görüntü Deposu hizmeti uygulamalarını dağıtma hakkında daha fazla bilgi için makalenin.

## <a name="built-in-programming-models"></a>Yerleşik programlama modelleri
Service Fabric hizmetleri oluşturmak için kullanılabilen .NET Framework programlama modeli vardır:

**Güvenilir hizmetler**: durum bilgisiz ve durum bilgisi olan hizmetler oluşturmak için bir API. Durum bilgisi olan hizmet depolamak durumlarına güvenilir koleksiyonlarda (bir sözlük veya bir kuyruk gibi). Web API ve Windows Communication Foundation (WCF) gibi çeşitli iletişim yığınları takın alın.

**Güvenilir aktörler**: sanal aktör programlama modeli aracılığıyla durum bilgisiz ve durum bilgisi olan nesneleri oluşturmak için bir API. Çok sayıda hesaplama/durumunun bağımsız bir birim varsa, bu model yararlı olabilir. Bu model Aç tabanlı bir iş parçacığı modelini kullandığından, tüm giden istekleri tamamlayıncaya kadar tek bir aktör diğer gelen istekleri işleyemiyor beri diğer aktörler veya hizmetleri çağıran kodu önlemek en iyisidir.

Okuma [hizmetiniz için bir programlama modeli seçin](service-fabric-choose-framework.md) daha fazla bilgi için makalenin.

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a>Sonraki adımlar
Service Fabric hakkında daha fazla bilgi için:

* [Service Fabric genel bakış](service-fabric-overview.md)
* [Neden bir mikro yaklaşımını uygulamaları oluşturmak için?](service-fabric-overview-microservices.md)
* [Uygulama senaryoları](service-fabric-application-scenarios.md)

