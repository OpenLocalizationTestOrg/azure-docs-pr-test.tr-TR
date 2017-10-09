---
title: "Service Fabric ve kapsayıcıları aaaOverview | Microsoft Docs"
description: "Service Fabric ve hello genel bir bakış kapsayıcıları toodeploy mikro hizmet uygulamaları kullanın. Bu makalede nasıl kapsayıcıları kullanılabilir ve Service Fabric kullanılabilir özellikleri hello genel bir bakış sağlar."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: c98b3fcb-c992-4dd9-b67d-2598a9bf8aab
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: fce94c4b476351c90f23f706aab8bc17319cce22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-and-containers"></a>Service Fabric ve kapsayıcıları
> [!NOTE]
> Linux için Önizleme'de bu özellik kullanılabilir.  Windows 10 tooa Service Fabric kümesi desteklenmiyor kapsayıcıları dağıtma henüz (yakında). 
>   

## <a name="introduction"></a>Giriş
Azure Service fabric bir [orchestrator](service-fabric-cluster-resource-manager-introduction.md) makine bir küme içinde kullanım ve yüksek ölçüde ölçeklendirmeyi iyileştirme yıllık ile Microsoft Hizmetleri. Hizmetleri, hello kullanarak birçok yönden geliştirilebilir [Service Fabric modellerini programlama](service-fabric-choose-framework.md) toodeploying [Konuk yürütülebilir dosyalar](service-fabric-deploy-existing-app.md). Varsayılan olarak, Service Fabric dağıtır ve bu hizmetleri işlemler olarak etkinleştirir. İşlemler hello hızlı etkinleştirme ve bir kümedeki hello kaynaklar yüksek yoğunluk kullanımını sağlar. Service Fabric kapsayıcı görüntüleri Hizmetleri'nde de dağıtabilirsiniz. Önemlisi, işlemleri Hizmetleri'nde ve Merhaba kapsayıcılara Hizmetleri'nde karıştırabilirsiniz aynı uygulama. 

## <a name="containers-and-service-fabric-roadmap"></a>Kapsayıcılar ve Service Fabric yol haritası
Gelecek sürümlerde birçok gelişme Service Fabric kapsayıcı düzenlemesini aşağıda verilmiştir. Geliştirmeleri, Gelişmiş bir uygulama, güvenlik özellikleri, Gelişmiş tanılama içindeki sanal ağlar için destek ile ağ ve araç desteği için özellikler içerir. Service Fabric, var olan kodda (örneğin, IIS MVC uygulamaları) paketlenmiş kapsayıcıları hello Service Fabric programlama modelleri kullanılarak geliştirilen hizmetleriyle karıştıran toocreate uygulamaları sağlar.  Tek bir kümede gibi çeşitli uygulamaları çalıştırabilir. 

## <a name="what-are-containers"></a>Kapsayıcıları nelerdir?
Kapsayıcıları kapsüllenmiş, bir işletim sistemi sağlar sanallaştırma aynı çekirdek tootake avantajlarından yalıtılmış örneklerde çalıştıracağınız ayrı ayrı dağıtılabilir bileşenleri hello. Bu nedenle, her uygulama ve çalışma zamanı, bağımlılıklar ve sistem başlatılamadığından bir kapsayıcı içinde tam, özel erişim toohello yalıtılmış kapsayıcının kendi görünümünü işletim sistemi yapıları ile çalıştırın. Taşınabilirlik yanı sıra, bu güvenlik ve kaynak ayırma derecesini hello ana avantajı, aksi takdirde Hizmetleri işlemlerde çalışan Service Fabric ile kapsayıcıları kullanma ' dir.

Merhaba temel işletim sistemi uygulamalardan sanallaştıran sanallaştırma teknolojisi kapsayıcılardır. Kapsayıcıları derecelerde yalıtım ile uygulamaları toorun için sabit bir ortam sağlar. Kapsayıcıları doğrudan hello çekirdek üstünde çalıştırın ve hello dosya sistemi yalıtılmış bir görünümünü ve diğer kaynaklara sahip. Karşılaştırılan toovirtual makineler kapsayıcıları avantajları aşağıdaki hello sahiptir:

* **Küçük**: kapsayıcıları bir tek bir depolama alanı ve katman sürümleri ve güncelleştirmeleri tooincrease verimliliği kullanın.
* **Hızlı**: kapsayıcıları sahip değilseniz tooboot tüm işletim sistemi, bunlar çok daha hızlı, genellikle saniye cinsinden başlatabilmeniz.
* **Taşınabilirlik**: kapsayıcılı uygulama görüntüsü şirket içinde sanal makinelerde ya da doğrudan fiziksel makinelerde hello bulutta taşınmasını toorun olabilir.
* **Kaynak İdaresi**: bir kapsayıcı, konakta tüketebileceği fiziksel kaynakları hello sınırlayabilirsiniz.

## <a name="container-types"></a>Kapsayıcı türleri
Service Fabric hem Linux hem de Windows kapsayıcıları destekler ve ayrıca hello ikinci Hyper-V yalıtım modunu destekler. 

### <a name="docker-containers-on-linux"></a>Linux üzerinde docker kapsayıcıları
Docker üst düzey API'leri toocreate sağlar ve Linux çekirdek kapsayıcıları üstünde kapsayıcıları yönetin. Docker hub'a merkezi bir depoya toostore olduğu ve kapsayıcı görüntülerini alın.
Bir öğretici için bkz: [Docker kapsayıcısı tooService doku dağıtmak](service-fabric-get-started-containers-linux.md).

### <a name="windows-server-containers"></a>Windows Server kapsayıcıları
Windows Server 2016 sağlanan yalıtım hello düzeyinde farklı kapsayıcılar iki farklı türde sağlar. Windows Server kapsayıcıları ve Docker kapsayıcıları hem de ad alanı ve dosya sistemi yalıtım ancak paylaşımı hello çekirdeği bunlar çalıştıran hello ana bilgisayarla olduğundan benzerdir. Linux üzerinde bu yalıtım tarafından geleneksel olarak sağlanmış `cgroups` ve `namespaces`, ve Windows Server kapsayıcıları benzer şekilde davranır.

Her kapsayıcı hello işletim sisteminin çekirdek hello ana bilgisayar veya diğer kapsayıcılar ile paylaşmaz çünkü Windows Hyper-V kapsayıcıları fazla yalıtım ve güvenlik sağlar. Bu daha yüksek düzeyde güvenlik yalıtım ile Hyper-V kapsayıcıları saldırgan, çok müşterili senaryolarında hedefler.
Bir öğretici için bkz: [Windows kapsayıcı tooService doku dağıtmak](service-fabric-get-started-containers.md).

Merhaba aşağıdaki şekilde hello sanallaştırmasının ve yalıtım düzeyi hello işletim sisteminde kullanılabilir farklı türleri gösterilmiştir.
![Service Fabric platformundan][Image1]

## <a name="scenarios-for-using-containers"></a>Kapsayıcıları kullanma senaryoları
Burada bir kapsayıcı iyi bir seçimdir tipik örnekler şunlardır:

* **IIS kaldırın ve shift**: Varolan varsa [ASP.NET MVC](https://www.asp.net/mvc) toocontinue toouse istediğiniz uygulamalar yerine bir kapsayıcıda bunları put tooASP.NET çekirdek geçirme. Bu ASP.NET MVC uygulamaları Internet Information Services (IIS) bağlıdır. Bu uygulamalardan kapsayıcı görüntülerle IIS görüntü precreated hello paketini ve bunları Service Fabric ile dağıtabilirsiniz. Bkz: [kapsayıcı Windows Server görüntülerinde](https://msdn.microsoft.com/virtualization/windowscontainers/quick_start/quick_start_images) hakkında bilgi için toocreate IIS görüntüler.
* **Karışık kapsayıcıları ve Service Fabric mikro**: uygulamanızın bir parçası için var olan bir kapsayıcı görüntüsünü kullanın. Örneğin, hello kullanabilirsiniz [NGINX kapsayıcısı](https://hub.docker.com/_/nginx/) hello web ön ucu hello için durum bilgisi olan hizmetler ve uygulama için daha yoğun arka uç hesaplama.
* **"Gürültülü komşu" Hizmetleri etkisini azaltmak**: kapsayıcıları toorestrict hello kaynakların bir konakta bir hizmetin kullandığı hello kaynak İdaresi özelliğini kullanabilirsiniz. Hizmetleri birçok kaynaklarını tüketebilir ve (örneğin, uzun süre çalışan, sorgu benzeri işlemi) diğer hello performansını etkiler, bu hizmetleri kaynak İdaresi kapsayıcılarına yerleştirmeyi düşünün.

## <a name="service-fabric-support-for-containers"></a>Kapsayıcıları için Service Fabric desteği
Service Fabric şu anda Hyper-V yalıtım modunu desteğinin yanı sıra Windows Server 2016, Linux ve Windows Server kapsayıcılarında Docker kapsayıcıları dağıtımını destekler. 

Merhaba Service Fabric içinde [uygulama modeli](service-fabric-application-model.md), hangi birden çok çoğaltmaları hizmete bir uygulama konağı bir kapsayıcıyı temsil eder. Service Fabric, herhangi bir kapsayıcıdaki çalıştırabilir ve hello senaryodur benzer toohello [Konuk yürütülebilir senaryo](service-fabric-deploy-existing-app.md), bir kapsayıcı içinde var olan bir uygulama paketi burada. Merhaba ortak kullanım örneği kapsayıcıları için bu senaryodur ve herhangi bir dil veya çerçevelerini kullanarak, ancak hello yerleşik Service Fabric programlama modelleri kullanmayan yazılmış bir uygulama çalıştıran örnekler.

Ayrıca, Service Fabric hizmetleri de kapsayıcılar içinde çalıştırabilirsiniz. Şu anda, gelecek sürümlerde gelişmiş toobe ancak kapsayıcılar içinde çalışan Service Fabric Hizmetleri için destek sınırlıdır.

* **Kapsayıcılar içinde güvenilir durum bilgisi olmayan hizmetler**: hello güvenilir programlama modelleri yalnızca Linux üzerinde desteklenen hizmetlerini kullanarak güvenilir ve durum bilgisi olmayan hizmetler. Windows kapsayıcılarında güvenilir ve durum bilgisi olmayan hizmetler için destek için gelecekteki bir sürüm planlanmaktadır.
* **Durum bilgisi olan hizmetler kapsayıcılar içinde**: hello Reliable Actors veya Reliable Services programlama modeli bu hizmetleri kullanın. Destek kapsayıcılarında durum bilgisi olan Hizmetleri çalıştıran gelecekte eklenir bırakın.

Service Fabric sahip birkaç yardımcı kapsayıcı yeteneklerini oluşturmak, kapsayıcılı mikro uygulamalarının oluşur. Service Fabric yetenekleri kapsayıcılı Hizmetleri için aşağıdaki hello sunar:

* Kapsayıcı görüntü dağıtımının ve etkinleştirmesinin.
* Kaynak İdaresi.
* Depo kimlik doğrulaması.
* Kapsayıcı bağlantı noktası toohost bağlantı noktası eşlemesi.
* Kapsayıcıya bulma ve iletişim.
* Özelliği tooconfigure ve ortam değişkenlerini ayarlama.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, öğrenilen kapsayıcıları hakkında bir kapsayıcı orchestrator Service Fabric olduğunu ve bu Service Fabric kapsayıcıları destekleyen özellikler sahip. Sonraki adım olarak, her bir hello özellikleri tooshow örnekler, nasıl ele alacağız toouse bunları.

[Bir Windows kapsayıcı tooService Windows Server 2016 doku dağıtma](service-fabric-get-started-containers.md)

[Docker kapsayıcısı tooService doku Linux'ta dağıtma](service-fabric-get-started-containers-linux.md)

[Image1]: media/service-fabric-containers/Service-Fabric-Types-of-Isolation.png
