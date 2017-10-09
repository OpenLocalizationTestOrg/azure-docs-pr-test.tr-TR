---
title: "Bulut Hizmetleri ve Service Fabric arasında aaaDifferences | Microsoft Docs"
description: "Geçiş için kavramsal genel bulut Hizmetleri tooService doku uygulamalardan."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 0b87b1d3-88ad-4658-a465-9f05a3376dee
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: bbc5ef4fe0fe1b0da55454cb6b766925030198fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-hello-differences-between-cloud-services-and-service-fabric-before-migrating-applications"></a>Geçirmeden önce hello farklarını bulut Hizmetleri ve Service Fabric öğrenin uygulamalar.
Microsoft Azure Service Fabric hello nesil bulut uygulama düzeyde ölçeklenebilir, yüksek oranda güvenilir dağıtılmış uygulamalar için platformudur. Paketleme, dağıtma, yükseltme ve dağıtılmış bulut uygulamalarını yönetmek için birçok yeni özellik sunar. 

Bulut Hizmetleri tooService doku tanıtım Kılavuzu toomigrating uygulamalardan budur. Öncelikle mimari odaklanır ve bulut Hizmetleri ve Service Fabric arasındaki farklar tasarlayın.

## <a name="applications-and-infrastructure"></a>Uygulamalar ve altyapı
Bulut Hizmetleri ve Service Fabric arasındaki temel fark hello VM'ler, iş yüklerini ve uygulamaları arasındaki ilişkidir. Buraya bir iş yükü, belirli bir görevi tooperform yazmak veya bir hizmet sağlamak hello kodu olarak tanımlanır.

* **Bulut Hizmetleri ' dir. vm'lerle uygulamaları dağıtma hakkında** Merhaba kodları sıkı şekilde bağlı tooa VM, Web veya çalışan rolü gibi örneğidir. Bulut Hizmetleri iş yükünü toodeploy toodeploy bir ya da çalışma hello iş yükü daha fazla VM örnekleri. Uygulamalar ve sanal makineleri hiçbir ayrımı yoktur ve bu nedenle yoktur uygulamanın resmi tanımı yok. Bir uygulama, ardından bir bulut Hizmetleri dağıtımı içindeki Web veya çalışan rolü örnekleri bir dizi veya tam bir bulut Hizmetleri dağıtımını olarak düşünülebilir. Bu örnekte, bir uygulama rolü örnekleri bir küme olarak gösterilir.

![Bulut Hizmetleri uygulamalar ve topolojisi][1]

* **Service Fabric dağıtma uygulamaları tooexisting Vm'leri veya Windows veya Linux'ta Service Fabric çalışan makineler hakkındadır.** Yazdığınız hello uygulamanın dağıtılan toomultiple ortamları olabilir hello Service Fabric uygulaması platformu tarafından hemen soyutlanır altyapı, temel alınan hello tamamen ayrılmış hizmetleridir. Service Fabric iş yükünü bir "hizmet" adı verilir ve bir veya daha fazla hizmet hello Service Fabric uygulaması platformu üzerinde çalışan resmi olarak tanımlanan bir uygulama içinde gruplandırılır. Birden çok uygulama dağıtılan tooa tek Service Fabric kümesi olabilir.

![Service Fabric uygulamaları ve topolojisi][2]

Bulut Hizmetleri ile bağlı iş yüklerini Azure yönetilen sanal makineleri dağıtmak için bir sistem iken Service Fabric kendisi Windows veya Linux çalıştıran bir uygulama platformu katmanıdır.
Merhaba Service Fabric uygulama modeli, çok sayıda avantaj vardır:

* Hızlı Dağıtım zamanları. VM örnekleri oluşturmak zaman alabilir. Service Fabric içinde tooform barındıran bir küme hello sonra Service Fabric uygulaması platformu VM'ler yalnızca dağıtılır. Bu noktadan itibaren uygulama paketleri dağıtılan toohello küme çok hızlı bir şekilde olabilir.
* Yüksek yoğunlukta barındırma. Bulut Hizmetleri'nde bir iş yükü çalışan rolü VM barındırır. Service Fabric içinde uygulamalar çok sayıda uygulamaları tooa az sayıda daha büyük dağıtımlar için genel maliyeti düşürebilirsiniz VM'ler dağıtabileceğiniz anlamına gelir, çalıştırmasına hello VM'ler ayrıdır.
* Azure veya şirket içi olup hello Service Fabric platform herhangi bir yerden çalıştırabilirsiniz Windows Server veya Linux makineye sahiptir. Uygulamanızın üzerinde farklı ortamlarda çalıştırabilmeniz için hello platformu hello altyapının bir soyutlama katmanı sağlar. 
* Dağıtılmış uygulama yönetimi. Service Fabric yalnızca ana dağıtılmış uygulamalar, ancak da yardımcı olur yaşam döngüleri VM barındırma hello bağımsız olarak yönetmek veya yaşam döngüsü makine, bir platformdur.

## <a name="application-architecture"></a>Uygulama mimarisi
Merhaba mimarisi bir bulut Hizmetleri uygulaması genellikle Service Bus, Azure Table ve Blob Storage, SQL, Redis ve diğerleri gibi çok sayıda dış Hizmet bağımlılıklarını içerir toomanage hello durum ve verileri bir uygulama ve Web arasındaki iletişim ve bulut Hizmetleri dağıtımında çalışan rolleri. Tam bir bulut Hizmetleri uygulamanın örnek şuna benzeyebilir:  

![Bulut Hizmetleri mimarisi][9]

Service Fabric uygulamaları da toouse hello aynı dış hizmetler tam bir uygulama seçebilirsiniz. Bu örnek bulut Hizmetleri mimarisi kullanarak, hello en basit geçiş yolundan bulut Hizmetleri tooService doku tooreplace yalnızca hello bulut Hizmetleri hello tutma bir Service Fabric uygulaması ile dağıtımıdır genel mimarisi hello aynı. Merhaba Web ve çalışan rolleri taşınmasını tooService doku durum bilgisi olmayan hizmetler çok az kod değişiklikleri olabilir.

![Basit geçişten sonra Service Fabric mimarisi][10]

Bu aşamada hello sistem devam etmesi gerektiğini toowork hello aynı önceki gibi. Durum bilgisi olan uygunsa Hizmetleri gibi Service Fabric'ın durum bilgisi olan özellikleri, dış durumu depoları yararlanarak internalized. Bu eşdeğer işlevsellik tooyour uygulama hello dış hizmetler önce yaptığınız gibi sağlayan özel hizmetler yazma gerektirdiğinden daha basit bir Web ve çalışan rolleri tooService doku durum bilgisi olmayan hizmetler, geçiş daha karmaşıktır. Bunun yapılması hello avantajları şunlardır: 

* Dış bağımlılıkları kaldırma 
* Merhaba dağıtım, yönetim ve yükseltme modelleri birleştirin. 

Bu hizmetler internalizing bir örneği elde edilen mimarisi şöyle:

![Tam geçişten sonra Service Fabric mimarisi][11]

## <a name="communication-and-workflow"></a>İletişim ve iş akışı
Çoğu bulut hizmeti uygulamaları birden fazla katmanı oluşur. Benzer şekilde, Service Fabric uygulaması birden fazla hizmeti (genellikle birçok Hizmetleri) oluşur. İki ortak iletişim modelleri olan doğrudan iletişim ve dış dayanıklı bir depolama aracılığıyla.

### <a name="direct-communication"></a>Doğrudan iletişim
İle doğrudan iletişim, katmanları doğrudan her katmanı tarafından kullanıma sunulan bitiş noktası ile iletişim kurabilir. Bulut Hizmetleri, bu rastgele bir VM rol örneği ya da seçerek anlamına gelir veya hepsini toobalance yük ve bağlantı tooits uç noktası doğrudan gibi durum bilgisiz ortamlarda.

![Bulut Hizmetleri doğrudan iletişim][5]

 Doğrudan iletişim Service Fabric ortak bir iletişim modelidir. Service Fabric tooa hizmetine bağlanın ancak hello anahtar arasındaki Service Fabric ve Cloud Services bulut Hizmetleri'nde, tooa VM bağlanmak farktır. Bu, birkaç nedenlerle önemli bir fark oluşur:

* Service Fabric Hizmetleri'nde onlara konağı ilişkili toohello VM'ler olmayan; Hizmetleri hello kümede dolaşmak ve aslında, geçici beklenen toomove çeşitli nedenleri şunlardır: kaynak Dengeleme, yük devretme, uygulama ve altyapı yükseltmeleri ve yerleştirme ya da yük kısıtlamaları. Başka bir deyişle, bir hizmet örneğinin Adres dilediğiniz zaman değiştirebilirsiniz. 
* Service Fabric bir VM'de her benzersiz uç noktaları birden çok hizmet barındırabilir.

Service Fabric hello kullanılan tooresolve uç nokta adresleri hizmetlerinin olabilir adlandırma hizmeti adlı bir hizmet bulma mekanizma sağlar. 

![Service Fabric doğrudan iletişim][6]

### <a name="queues"></a>Kuyruklar
Bulut Hizmetleri gibi durum bilgisiz ortamlarda katmanları arasında ortak bir iletişim mekanizması toouse bir harici depolama kuyruğu toodurably olan bir katmanı tooanother iş görevleri depolamak. Yaygın bir senaryo, bir işleri tooan Azure kuyruk gönderir web katmanı veya hizmet burada çalışan rolü örnekleri dequeue ve hello işleri işlemek veri yolu değil.

![Bulut Hizmetleri sıra iletişimi][7]

Merhaba aynı iletişim modelini Service Fabric içinde kullanılabilir. Var olan bir bulut Hizmetleri uygulama tooService doku geçirirken bu yararlı olabilir. 

![Service Fabric doğrudan iletişim][8]

## <a name="next-steps"></a>Sonraki Adımlar
Merhaba doku yalnızca hello tutma bir Service Fabric uygulaması ile bulut Hizmetleri dağıtımı Merhaba, uygulamanızın genel mimarisi kabaca tooreplace olan bulut Hizmetleri tooService en basit geçiş yolundan hello aynı. aşağıdaki makaleye bakın hello toohelp dönüştürme bir Web veya çalışan rolü tooa Service Fabric durum bilgisiz hizmeti bir kılavuz sağlar.

* [Basit geçiş: bir Web veya çalışan rolü tooa Service Fabric durum bilgisiz hizmet Dönüştür](service-fabric-cloud-services-migration-worker-role-stateless-service.md)

<!--Image references-->
[1]: ./media/service-fabric-cloud-services-migration-differences/topology-cloud-services.png
[2]: ./media/service-fabric-cloud-services-migration-differences/topology-service-fabric.png
[5]: ./media/service-fabric-cloud-services-migration-differences/cloud-service-communication-direct.png
[6]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-communication-direct.png
[7]: ./media/service-fabric-cloud-services-migration-differences/cloud-service-communication-queues.png
[8]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-communication-queues.png
[9]: ./media/service-fabric-cloud-services-migration-differences/cloud-services-architecture.png
[10]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-architecture-simple.png
[11]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-architecture-full.png
