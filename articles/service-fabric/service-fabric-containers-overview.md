---
title: "Service Fabric ve kapsayıcıları genel bakış | Microsoft Docs"
description: "Service Fabric ve kapsayıcıları kullanımını mikro hizmet uygulamalarını dağıtmak için genel bakış. Bu makalede nasıl kapsayıcıları kullanılabilir bir genel bakış ve Service Fabric içinde kullanılabilen özellikleri sağlar."
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
ms.openlocfilehash: f770b6181a99d24ea6a6e945d505da914e1b6128
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="service-fabric-and-containers"></a>Service Fabric ve kapsayıcıları
> [!NOTE]
> Linux için Önizleme'de bu özellik kullanılabilir.  Windows 10 kümesinde desteklenmeyen bir Service Fabric kapsayıcıları dağıtma henüz (yakında). 
>   

## <a name="introduction"></a>Giriş
Azure Service fabric bir [orchestrator](service-fabric-cluster-resource-manager-introduction.md) makine bir küme içinde kullanım ve yüksek ölçüde ölçeklendirmeyi iyileştirme yıllık ile Microsoft Hizmetleri. Hizmetleri kullanmanın birçok yönden geliştirilebilir [Service Fabric modellerini programlama](service-fabric-choose-framework.md) dağıtma [Konuk yürütülebilir dosyalar](service-fabric-deploy-existing-app.md). Varsayılan olarak, Service Fabric dağıtır ve bu hizmetleri işlemler olarak etkinleştirir. İşlemler hızlı etkinleştirme ve küme kaynaklarının yüksek yoğunluk kullanım sağlar. Service Fabric kapsayıcı görüntüleri Hizmetleri'nde de dağıtabilirsiniz. Önemlisi işlemlerde Hizmetleri ve Hizmetleri aynı uygulamada kapsayıcılardaki karıştırabilirsiniz. 

## <a name="containers-and-service-fabric-roadmap"></a>Kapsayıcılar ve Service Fabric yol haritası
Gelecek sürümlerde birçok gelişme Service Fabric kapsayıcı düzenlemesini aşağıda verilmiştir. Geliştirmeleri, Gelişmiş bir uygulama, güvenlik özellikleri, Gelişmiş tanılama içindeki sanal ağlar için destek ile ağ ve araç desteği için özellikler içerir. Service Fabric, var olan kodda (örneğin, IIS MVC uygulamaları) modellerini programlama Service Fabric kullanılarak geliştirilen hizmetleriyle paketlenmiş kapsayıcıları karıştırma uygulamalar oluşturmanıza olanak sağlar.  Tek bir kümede gibi çeşitli uygulamaları çalıştırabilir. 

## <a name="what-are-containers"></a>Kapsayıcıları nelerdir?
Bir işletim sistemi sağlar sanallaştırma yararlanmak için aynı çekirdek yalıtılmış örneklerinde Çalıştır kapsüllenmiş, ayrı ayrı dağıtılabilir bileşenleri kapsayıcılardır. Bu nedenle, her uygulama ve çalışma zamanı, bağımlılıklar ve sistem başlatılamadığından içinde bir kapsayıcı, tam, özel erişim ile işletim sistemi yapıları yalıtılmış kapsayıcının kendi görünümüne'e çalıştırın. Taşınabilirlik yanı sıra, bu güvenlik ve kaynak ayırma derecesini kapsayıcıları, aksi takdirde Hizmetleri işlemlerde çalışan Service Fabric ile kullanmak için ana avantajdır.

Uygulamaları temel işletim sisteminden sanallaştıran sanallaştırma teknolojisi kapsayıcılardır. Kapsayıcıları derecelerde yalıtım ile çalışacak uygulamaları için sabit bir ortam sağlar. Kapsayıcıları doğrudan üstünde çekirdek çalıştırın ve dosya sistemi ve diğer kaynakları yalıtılmış bir görünüm. Sanal makineler ile karşılaştırıldığında, kapsayıcıları aşağıdaki avantajlara sahip olursunuz:

* **Küçük**: verimliliği artırmak için kapsayıcılar kullanma tek bir depolama alanı ve katman sürümleri ve güncelleştirmeler.
* **Hızlı**: kapsayıcıları, bunlar çok daha hızlı, genellikle saniye cinsinden başlatabilmeniz tüm bir işletim sistemi önyükleme zorunda değilsiniz.
* **Taşınabilirlik**: kapsayıcılı uygulama görüntüsü şirket içinde sanal makinelerde ya da doğrudan fiziksel makinelerde bulutta çalıştırmak için bağlantı noktası kurulmuş.
* **Kaynak İdaresi**: bir kapsayıcı, konakta tüketebileceği fiziksel kaynakları sınırlayabilirsiniz.

## <a name="container-types"></a>Kapsayıcı türleri
Service Fabric kapsayıcıları hem Linux hem de Windows ve aynı zamanda Hyper-V yalıtım modunu ikinci üzerinde destekler. 

### <a name="docker-containers-on-linux"></a>Linux üzerinde docker kapsayıcıları
Docker oluşturmak ve Linux çekirdek kapsayıcıları üstünde kapsayıcıları yönetmek için üst düzey API'ler sağlar. Docker hub'a depolamak ve kapsayıcı görüntüleri almak için merkezi bir depodur.
Bir öğretici için bkz: [Docker kapsayıcısı dağıtmak için Service Fabric](service-fabric-get-started-containers-linux.md).

### <a name="windows-server-containers"></a>Windows Server kapsayıcıları
Windows Server 2016 sağlanan yalıtım düzeyi farklı kapsayıcılar iki farklı türde sağlar. Her ikisi de ad alanı ve dosya sistemi ayırma varsa, ancak bunlar çalıştıran ana çekirdek paylaşmak için Windows Server kapsayıcıları ve Docker kapsayıcıları benzerdir. Linux üzerinde bu yalıtım tarafından geleneksel olarak sağlanmış `cgroups` ve `namespaces`, ve Windows Server kapsayıcıları benzer şekilde davranır.

Her kapsayıcı diğer kapsayıcılar veya ana bilgisayar işletim sistemi çekirdeği paylaşmaz çünkü Windows Hyper-V kapsayıcıları fazla yalıtım ve güvenlik sağlar. Bu daha yüksek düzeyde güvenlik yalıtım ile Hyper-V kapsayıcıları saldırgan, çok müşterili senaryolarında hedefler.
Bir öğretici için bkz: [bir Windows kapsayıcıyı dağıtmak için Service Fabric](service-fabric-get-started-containers.md).

Aşağıdaki şekilde sanallaştırmasının ve yalıtım düzeyi işletim sisteminde kullanılabilir farklı uygulama türleri gösterilmektedir.
![Service Fabric platformundan][Image1]

## <a name="scenarios-for-using-containers"></a>Kapsayıcıları kullanma senaryoları
Burada bir kapsayıcı iyi bir seçimdir tipik örnekler şunlardır:

* **IIS kaldırın ve shift**: Varolan varsa [ASP.NET MVC](https://www.asp.net/mvc) kullanmaya devam etmek istediğiniz uygulamaları geçirmek yerine bir kapsayıcıda bunları put ASP.NET Core onları. Bu ASP.NET MVC uygulamaları Internet Information Services (IIS) bağlıdır. Bu kapsayıcı görüntüleri uygulamalarla precreated IIS görüntüden paketini ve bunları Service Fabric ile dağıtabilirsiniz. Bkz: [kapsayıcı Windows Server görüntülerinde](https://msdn.microsoft.com/virtualization/windowscontainers/quick_start/quick_start_images) IIS görüntüleri oluşturma hakkında bilgi için.
* **Karışık kapsayıcıları ve Service Fabric mikro**: uygulamanızın bir parçası için var olan bir kapsayıcı görüntüsünü kullanın. Örneğin, kullanabilirsiniz [NGINX kapsayıcısı](https://hub.docker.com/_/nginx/) uygulama ve durum bilgisi olan hizmetler daha yoğun arka uç hesaplama için web ön ucu için.
* **"Gürültülü komşu" Hizmetleri etkisini azaltmak**: bir konakta bir hizmetin kullandığı kaynakları kısıtlamak için kapsayıcıları kaynak İdaresi özelliğini kullanabilirsiniz. Hizmetleri birçok kaynaklarını tüketebilir ve diğer performans (örneğin, uzun süre çalışan, sorgu benzeri işlemi) etkiler, bu hizmetleri kaynak İdaresi kapsayıcılarına yerleştirmeyi düşünün.

## <a name="service-fabric-support-for-containers"></a>Kapsayıcıları için Service Fabric desteği
Service Fabric şu anda Hyper-V yalıtım modunu desteğinin yanı sıra Windows Server 2016, Linux ve Windows Server kapsayıcılarında Docker kapsayıcıları dağıtımını destekler. 

Service Fabric içinde [uygulama modeli](service-fabric-application-model.md), hangi birden çok çoğaltmaları hizmete bir uygulama konağı bir kapsayıcıyı temsil eder. Service Fabric, herhangi bir kapsayıcıdaki çalıştırabilir ve senaryosu benzer [Konuk yürütülebilir senaryo](service-fabric-deploy-existing-app.md), bir kapsayıcı içinde var olan bir uygulama paketi burada. Genel kullanım örneği kapsayıcıları için bu senaryodur ve herhangi bir dil veya çerçevelerini kullanarak, ancak yerleşik Service Fabric programlama modelleri kullanmayan yazılmış bir uygulama çalıştıran örnekler.

Ayrıca, Service Fabric hizmetleri de kapsayıcılar içinde çalıştırabilirsiniz. Şu anda, gelecek sürümlerde gelişmiş üzere ancak kapsayıcılar içinde çalışan Service Fabric Hizmetleri için destek sınırlıdır.

* **Kapsayıcılar içinde güvenilir durum bilgisi olmayan hizmetler**: güvenilir programlama modelleri yalnızca Linux üzerinde desteklenen hizmetlerini kullanarak güvenilir ve durum bilgisi olmayan hizmetler. Windows kapsayıcılarında güvenilir ve durum bilgisi olmayan hizmetler için destek için gelecekteki bir sürüm planlanmaktadır.
* **Durum bilgisi olan hizmetler kapsayıcılar içinde**: Reliable Actors veya Reliable Services programlama modeli bu hizmetleri kullanın. Destek kapsayıcılarında durum bilgisi olan Hizmetleri çalıştıran gelecekte eklenir bırakın.

Service Fabric sahip birkaç yardımcı kapsayıcı yeteneklerini oluşturmak, kapsayıcılı mikro uygulamalarının oluşur. Service Fabric kapsayıcılı Hizmetleri için aşağıdaki özellikleri sunar:

* Kapsayıcı görüntü dağıtımının ve etkinleştirmesinin.
* Kaynak İdaresi.
* Depo kimlik doğrulaması.
* Ana bilgisayar bağlantı noktası eşlemesi noktasına kapsayıcı.
* Kapsayıcıya bulma ve iletişim.
* Yapılandırma ve ortam değişkenlerini ayarlama kabiliyeti.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, öğrenilen kapsayıcıları hakkında bir kapsayıcı orchestrator Service Fabric olduğunu ve bu Service Fabric kapsayıcıları destekleyen özellikler sahip. Sonraki adım olarak, bunların nasıl kullanılacağını göstermek için özelliklerin her biri üzerinde örnekler alacağız.

[Windows Server 2016 Service Fabric Windows kapsayıcı dağıtma](service-fabric-get-started-containers.md)

[Service Fabric Linux'ta Docker kapsayıcısı dağıtma](service-fabric-get-started-containers-linux.md)

[Image1]: media/service-fabric-containers/Service-Fabric-Types-of-Isolation.png
