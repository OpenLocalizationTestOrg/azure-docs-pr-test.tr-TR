---
title: aaaLearn Azure Service Fabric terminolojisi | Microsoft Docs
description: "Service Fabric terminolojisi bakış. Önemli terminolojiyi kavramlar ve hello belgelerin hello kalan kullanılan terimler açıklanmaktadır."
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
ms.openlocfilehash: 4781fc0527b8a58e534183249bc2759aded2730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-terminology-overview"></a>Service Fabric terminolojisi genel bakış
Service Fabric kolay toopackage kolaylaştıran bir dağıtılmış sistemler platformudur, dağıtın ve ölçeklenebilir ve güvenilir mikro yönetin. Service Fabric toounderstand hello koşulları hello belgelerde kullanılan tarafından bu konuda ayrıntıları hello terminolojisi.

Merhaba Bu bölümde listelenen kavramları de Microsoft Virtual Academy videoları izleyerek hello ele alınmıştır: <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">temel kavramları</a>, <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965">tasarım zamanı kavramları</a>, ve <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">çalışma zamanı kavramları</a>.

## <a name="infrastructure-concepts"></a>Altyapı kavramları
**Küme**: içine, mikro dağıtılır ve yönetilen sanal veya fiziksel makineler ağa bağlı bir dizi.  Kümeleri toothousands makinelerin ölçeklendirebilirsiniz.

**Düğüm**: makine ya da bir kümenin parçasıysa VM bir düğüm olarak adlandırılır. Her düğüme bir düğüm adı (dize) atanır. Düğümleri yerleşim özellikleri gibi özelliklere sahiptir. Her makine ya da VM bir otomatik başlatılan Windows hizmet sahip `FabricHost.exe`, önyükleme sırasında çalışmaya başlar ve ardından iki yürütülebilir dosyalar başlatır: `Fabric.exe` ve `FabricGateway.exe`. Bu iki yürütülebilir dosyalar hello düğümü olun. Senaryoları test etmek için bir tek makine ya da VM birden çok düğümde birden çok örneğini çalıştırarak barındırabilir `Fabric.exe` ve `FabricGateway.exe`.

## <a name="application-concepts"></a>Uygulama kavramları
**Uygulama türü**: Merhaba atanan ad/sürüm tooa hizmet türleri koleksiyonu. İçinde tanımlanan bir `ApplicationManifest.xml` dosya, bir uygulama paketi dizininde katıştırılmış, hangi sonra toohello Service Fabric kümenin görüntü deposu kopyalanır. Bu uygulama türü hello küme içindeki bir adlandırılmış uygulama sonra oluşturabilirsiniz.

Okuma hello [uygulama modeli](service-fabric-application-model.md) daha fazla bilgi için makalenin.

**Uygulama paketi**: hello uygulama türü içeren bir disk dizini `ApplicationManifest.xml` dosya. Başvuruları hello uygulama türü yapar her hizmet türü için hizmet paketleri hello. Merhaba hello uygulama paketi dizinindeki kopyalanan tooService doku kümenin görüntü deposu dosyalarıdır. Örneğin, e-posta uygulama türü için bir uygulama paketi başvuruları tooa sıra hizmet paketi, ön uç hizmet paketi ve veritabanı hizmet paketi içerebilir.

**Uygulama adlı**: kopyalanan toohello Image store bir uygulama paketidir sonra hello uygulama paketin uygulama türü (kendi ad/sürüm kullanarak) belirterek hello uygulamasının hello küme içindeki bir örneğini oluşturabilirsiniz. Her uygulama türü örneği benzer bir URI ad atanır: `"fabric:/MyNamedApp"`. Bir küme içinde tek bir uygulama türünden birden çok adlandırılmış uygulamaları oluşturabilirsiniz. Ayrıca, farklı uygulama türlerinden adlandırılmış uygulamaları oluşturabilirsiniz. Her adlandırılmış bağımsız olarak yönetilen ve sürümü tutulan uygulamasıdır.      

**Hizmet türü**: hello ad/sürüm atanan tooa hizmetin kod paketler, veri paketleri ve yapılandırma paketleri. İçinde tanımlanan bir `ServiceManifest.xml` dosya, bir hizmet paketi dizini ve hello hizmet paket dizinini katıştırılmış sonra bir uygulama paketin tarafından başvurulan `ApplicationManifest.xml` dosya. Merhaba küme içinde adlandırılmış bir uygulama oluşturduktan sonra adlandırılmış bir hizmet hello birinden uygulama türünün hizmet türleri oluşturabilirsiniz. Merhaba hizmet türünün `ServiceManifest.xml` dosya hello hizmeti tanımlar.

Okuma hello [uygulama modeli](service-fabric-application-model.md) daha fazla bilgi için makalenin.

İki tür hizmet vardır:

* **Stateless:** hello hizmetin kalıcı durumunu Azure Storage, Azure SQL Database veya Azure Cosmos DB gibi bir harici depolama hizmetindeki depolandığında durumsuz bir hizmet kullanın. Merhaba hizmet kalıcı depolama hiç varsa durum bilgisi olmayan bir hizmet kullanın. Burada değerler toohello hizmet geçirilir, bir hesaplama bu değerleri kullanılarak gerçekleştirilir ve bir sonuç döndürdü Örneğin, bir hesap makinesi hizmeti.
* **Durum bilgisi olan:** kendi güvenilir koleksiyonları veya Reliable Actors modellerini programlama aracılığıyla Hizmetinizin durumunu Service Fabric toomanage istediğinizde, durum bilgisi olan bir hizmet kullanın. İstediğiniz toospread durumunuza üzerinden (ölçeklenebilirlik) ne zaman kaç bölümleri belirtin adlandırılmış bir hizmet oluşturuluyor. Ayrıca tooreplicate kaç kez belirtin (için güvenilirlik) düğümleri arasında durumu. Tek bir birincil çoğaltma ve birden fazla ikincil çoğaltmaları her adlandırılmış hizmetin vardır. Toohello birincil çoğaltmayı yazarak adlandırılmış Hizmetinizin durumunu değiştirin. Service Fabric sonra durumunuza eşitlenmiş şekilde kalmasının bu durumu tooall hello ikincil çoğaltmaları çoğaltır. Birincil çoğaltma işlemi başarısız olur ve var olan bir ikincil çoğaltma tooa birincil çoğaltma yükseltir Service Fabric otomatik olarak algılar. Service Fabric daha sonra yeni bir ikincil çoğaltma oluşturur.  

**Hizmet paketi**: hello hizmet türü içeren bir disk dizini `ServiceManifest.xml` dosya. Bu dosya hello kodu, statik verileri ve yapılandırma paketleri hello hizmet türünün başvurur. Merhaba hizmet paketi dizinindeki Hello dosyaları hello uygulama türünün tarafından başvurulan `ApplicationManifest.xml` dosya. Örneğin, bir hizmet paketi toohello kodu, statik verileri ve veritabanı hizmeti oluşturan yapılandırma paketleri başvurabileceğiniz.

**Adlı hizmetin**: adlandırılmış bir uygulama oluşturduktan sonra hello küme içindeki hizmet türlerinden birini örneği hello hizmet türü (kendi ad/sürüm kullanarak) belirterek oluşturabilirsiniz. Her hizmet türü örneği, adlandırılmış uygulamanın URI altında kapsamlı bir URI ad atanır. "Hizmet"uygulama adlı bir MyNamedApp"içinde adlı bir Veritabanım" oluşturursanız, örneğin, hello URI gibi görünüyor: `"fabric:/MyNamedApp/MyDatabase"`. Adlandırılmış bir uygulama içinde birden fazla adlandırılmış hizmetler oluşturabilirsiniz. Adlandırılmış her hizmetin kendi bölüm düzeni olabilir ve örnek/çoğaltma sayar.

**Paket kod**: hello hizmet türünün yürütülebilir dosyaları (genellikle EXE/DLL dosyaları) içeren bir disk dizini. Merhaba kod paketi dizini Hello dosyalarında hello hizmet türünün tarafından başvurulan `ServiceManifest.xml` dosya. Adlandırılmış bir hizmet oluşturulduğunda hello kod kopyalanan toohello düğüm veya düğümler seçili toorun hello adlı hizmetin paketidir. Ardından hello kod çalışmaya başlar. Kod Paketi yürütülebilir dosyalar iki tür vardır:

* **Konuk yürütülebilir dosyalar**: Farklı Çalıştır yürütülebilir dosyalar-hello ana bilgisayar işletim sistemindeki (Windows veya Linux). Diğer bir deyişle, bu yürütülebilir dosyalar Service Fabric çalışma zamanı dosyaları bağlantı tooor başvurusu yapmak ve modelleri programlama herhangi Service Fabric kullanmayın. Bu yürütülebilir Hizmeti uç noktası bulma için adlandırma gibi bazı Service Fabric özellikleri hello oluşturulamıyor toouse dosyalar. Konuk yürütülebilir dosyalar yük ölçümleri belirli tooeach hizmet örneği raporlayamazsınız.
* **Hizmet ana yürütülebilir dosyalar**: hizmet tooService doku çalışma zamanı dosyalarını bağlayarak modellerini programlama Service Fabric özelliklerini etkinleştirme Fabric kullanan yürütülebilir. Örneğin, bir adlandırılmış hizmet örneği uç noktaları Service Fabric'ın adlandırma hizmeti ile kaydedebilir ve yük ölçümleri de bildirebilirsiniz.      

**Veri paketi**: hello hizmet türünün statik ve salt okunur veri dosyaları (genellikle fotoğraf, ses ve video dosyaları) içeren bir disk dizini. Merhaba veri paket dizinini Hello dosyalarında hello hizmet türünün tarafından başvurulan `ServiceManifest.xml` dosya. Adlandırılmış bir hizmet oluşturulduğunda hello veri kopyalanan toohello düğüm veya düğümler seçili toorun hello adlı hizmetin paketidir.  Hello kod çalışmaya başlar ve şimdi hello veri dosyalara erişebilir.

**Yapılandırma paketi**: hello hizmet türünün statik içeren bir disk dizin salt okunur yapılandırma dosyaları (genellikle metin dosyaları). Merhaba yapılandırma paket dizini Hello dosyalarında hello hizmet türünün tarafından başvurulan `ServiceManifest.xml` dosya. Adlandırılmış bir hizmet oluşturulduğunda hello dosyaları hello yapılandırma paketi kopyalanan toohello biri ya daha fazla düğüm seçili toorun hello adlı hizmetin. Ardından hello kod çalışmaya başlar ve artık hello yapılandırma dosyalarını erişebilir.

**Kapsayıcıları**: varsayılan olarak, Service Fabric dağıtır ve Hizmetleri işlemler olarak etkinleştirir. Service Fabric kapsayıcı görüntüleri Hizmetleri'nde de dağıtabilirsiniz. Merhaba temel işletim sistemi uygulamalardan sanallaştıran sanallaştırma teknolojisi kapsayıcılardır. Bir uygulama ve çalışma zamanı, bağımlılıklar ve sistem başlatılamadığından bir kapsayıcı içinde tam, özel erişim toohello yalıtılmış kapsayıcının kendi görünümünü işletim sistemi yapıları ile çalıştırın. Service Fabric, Linux ve Windows Server kapsayıcılarında Docker kapsayıcıları destekler.  Daha fazla bilgi için okuma [Service Fabric ve kapsayıcıları](service-fabric-containers-overview.md).

**Bölüm düzeni**: adlandırılmış hizmet oluşturulurken bir bölüm düzeni belirtin. Büyük miktarlarda durumu hizmetleriyle hello veri hello durumu hello kümenin düğümleri arasında yayar bölümleri arasında bölün. Bu adlandırılmış hizmetinizin durumu tooscale sağlar. Durum bilgisi olan adlandırılmış Hizmetleri çoğaltmaları olsa da bir bölüm içinde durum bilgisiz adlandırılmış Hizmetleri örneğe sahip. Genellikle, hiçbir iç durumu sahip olduğu durum bilgisiz adlandırılmış hizmetleri her zaman sadece bir bölümü olmalıdır. Merhaba bölüm örnekleri için kullanılabilirlik sağlar; bir örnek başarısız olursa, diğer örnekleri toooperate normal şekilde devam ve ardından Service Fabric yeni bir örneğini oluşturur. Durum bilgisi olan hizmetler adlı durumlarına çoğaltmaları içinde korumak ve her bölüm kendi çoğaltma eşitlenmiş olarak tutulduğunu tüm hello durumuyla kümesi vardır. Bir çoğaltma işlemi başarısız olursa, Service Fabric hello mevcut çoğaltmaların yeni bir kopya oluşturur.

Okuma hello [bölüm Service Fabric güvenilir hizmetler](service-fabric-concepts-partitioning.md) daha fazla bilgi için makalenin.

## <a name="system-services"></a>Sistem Hizmetleri
Service Fabric hello platform özelliklerini sağlayan her kümede oluşturulan sistem hizmetleri vardır.

**Adlandırma Hizmeti**: her Service Fabric kümesi, hizmet adlarını tooa konumu hello kümedeki çözümlenen bir adlandırma hizmeti vardır. Merhaba hizmeti adları ve özellikleri, benzer tooan yönettiğiniz Internet hello kümesi için etki alanı adı hizmeti (DNS). İstemcileri güvenli bir şekilde hello adlandırma hizmeti tooresolve kullanarak hello kümedeki herhangi bir düğümün sahip bir hizmet adı ve konumu iletişim kurar.  Örneğin son toofailures, kaynak Dengeleme veya hello hello kümesini yeniden boyutlandırma hello kümedeki uygulamaları taşıyın. Hizmetler ve hello geçerli ağ konumu çözümlemek istemcileri geliştirebilirsiniz. İstemcileri hello gerçek Makine IP adresi ve bağlantı noktası şu anda çalıştığı edinin.

Okuma [Hizmetleri ile iletişim kurun](service-fabric-connect-and-communicate-with-services.md) hello hizmet ve istemci iletişimi hello Naming service ile iş API'ler hakkında daha fazla bilgi için.

**Görüntü Deposu hizmetini**: her Service Fabric kümesi dağıtılan, sürümlü uygulama paketleri tutulduğu bir görüntü Deposu hizmetini sahiptir. Bir uygulama paketi toohello Image Store kopyalayın ve ardından o uygulama paketi içinde yer alan hello uygulama türünü kaydetme. Hello uygulama türü sağlandıktan sonra ondan adlandırılmış uygulama oluşturabilirsiniz. Tüm adlandırılmış uygulamaları sildikten sonra hello görüntü depolama hizmeti uygulaması türünden kaydını kaldırabilirsiniz.

Okuma [hello ImageStoreConnectionString ayarı anlamak](service-fabric-image-store-connection-string.md) hello Image Store hizmeti hakkında daha fazla bilgi.

Okuma hello [bir uygulamayı dağıtmak](service-fabric-deploy-remove-applications.md) uygulamaları toohello görüntü Deposu hizmetini dağıtma hakkında daha fazla bilgi için makalenin.

## <a name="built-in-programming-models"></a>Yerleşik programlama modelleri
.NET Framework programlama modelleri, toobuild Service Fabric Hizmetleri kullanabilirsiniz:

**Güvenilir hizmetler**: bir API toobuild durum bilgisiz ve durum bilgisi olan hizmetler. Durum bilgisi olan hizmet depolamak durumlarına güvenilir koleksiyonlarda (bir sözlük veya bir kuyruk gibi). Ayrıca Web API ve Windows Communication Foundation (WCF) gibi çeşitli iletişim yığınlardaki tooplug alın.

**Güvenilir aktörler**: hello sanal aktör programlama modeli aracılığıyla bir API toobuild durum bilgisiz ve durum bilgisi olan nesneleri. Çok sayıda hesaplama/durumunun bağımsız bir birim varsa, bu model yararlı olabilir. Bu model Aç tabanlı bir iş parçacığı modelini kullandığından, tüm giden istekleri tamamlayıncaya kadar tek bir aktör diğer gelen istekleri işleyemiyor olduğundan, tooother aktörler veya hizmetleri çağıran en iyi tooavoid kodu bulunur.

Okuma hello [hizmetiniz için bir programlama modeli seçin](service-fabric-choose-framework.md) daha fazla bilgi için makalenin.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Sonraki adımlar
toolearn Service Fabric hakkında daha fazla bilgi:

* [Service Fabric genel bakış](service-fabric-overview.md)
* [Neden bir mikro toobuilding uygulamaları yaklaşımını?](service-fabric-overview-microservices.md)
* [Uygulama senaryoları](service-fabric-application-scenarios.md)

