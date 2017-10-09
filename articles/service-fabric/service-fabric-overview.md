---
title: Azure Service Fabric aaaOverview | Microsoft Docs
description: "Service Fabric, birçok mikro tooprovide ölçek ve esneklik uygulamaları burada oluşur genel bakış. Service Fabric bir dağıtılmış sistemler platform toobuild ölçeklenebilir, güvenilir kullanılan ve kolayca yönetilen hello bulut uygulamalarının ' dir."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: masnider
ms.assetid: bbcc652a-a790-4bc4-926b-e8cd966587c0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: mfussell
ms.openlocfilehash: 427fcedf97e6b2aae42d240c63e9f85daed8d962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-service-fabric"></a>Azure Service Fabric genel bakış
Azure Service Fabric kolay toopackage kolaylaştıran bir dağıtılmış sistemler platformudur, dağıtın ve ölçeklenebilir ve güvenilir mikro ve kapsayıcıları yönetin. Service Fabric da geliştirmeye ve bulut yerel uygulamaları yönetme hello önemli sorunları giderir. Geliştiriciler ve yöneticiler, karmaşık altyapı sorunlarını çözmeye çalışmak yerine görev açısından kritik, zorlu iş yüklerini uygulamaya odaklanabilir. Service Fabric, bu iş yüklerinin ölçeklenebilir, güvenilir ve yönetilebilir olmasını sağlar. Service Fabric oluşturmak ve yönetmek bu kurumsal sınıf, Katman 1, kapsayıcılarında çalışan bulut ölçekli uygulamalar için yeni nesil platform hello temsil eder.

Bu kısa video Service Fabric ve mikro hizmetler sunar:<center><a target="_blank" href="https://aka.ms/servicefabricvideo">  
<img src="./media/service-fabric-overview/OverviewVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="applications-composed-of-microservices"></a>Uygulamalar mikro oluşur 
Service Fabric yüksek yoğunluklu makinelerin paylaşılan havuzu üzerinde çalışır, hangi tooas bir küme adlandırılır, mikro oluşan ölçeklenebilir ve güvenilir uygulamaları yönetmek ve toobuild sağlar. Dağıtılmış, çalışan kapsayıcılar ölçeklenebilir, durum bilgisiz ve durum bilgisi olan mikro Gelişmiş ve basit çalışma zamanı toobuild sağlar. Ayrıca kapsamlı uygulama yönetim özellikleri tooprovision sağlar, dağıtmak, izlemek, yükseltme/düzeltme eki ve dağıtılan uygulamaları kapsayıcılı Hizmetleri dahil olmak üzere silin.

Azure SQL veritabanı dahil olmak üzere birçok Microsoft hizmetlerinin Bugün, Service Fabric çalıştırır, Azure Hizmetleri Azure Cosmos DB, Cortana, Microsoft Power BI, Microsoft Intune, Azure Event Hubs, Azure IOT Hub, Dynamics 365, Skype Kurumsal ve birçok çekirdek.

Service Fabric gerektiği gibi küçük, başlatmak ve yüzlerce veya binlerce makinelerin ile toomassive ölçek büyütme uyarlanmış toocreate bulut yerel hizmetleridir.

Bugünün Internet ölçekli hizmetler mikro oluşturulur. Protokol ağ geçitleri mikro örnekleri arasında kullanıcı profilleri, alışveriş, işleme, Envanter sıraları, sepetleri ve önbelleğe alır. Service Fabric her mikro hizmet (veya kapsayıcı) durum bilgisiz ya da durum bilgisi olan benzersiz bir ad veren mikro bir platformdur.

Service Fabric Bu mikro oluşan kapsamlı çalışma zamanı ve yaşam döngüsü yönetimi özellikleri tooapplications sağlar. Mikro dağıtılan ve hello Service Fabric kümesi arasında etkinleştirilen kapsayıcılar içinde barındırır. Sanal makineler toocontainers bir taşımak büyüklük sipariş artışı yoğunluğu içinde mümkün kılar. Benzer şekilde, bu kapsayıcılardaki kapsayıcıları toomicroservices'den taşıdığınızda, başka bir büyüklük yoğunluğu içinde mümkün olur. Örneğin, Azure SQL veritabanı için tek bir küme on binlerce kapsayıcıları barındıran yüz binlerce veritabanları toplam çalışan makineler yüzlerce oluşur. Her bir Service Fabric durum bilgisi olan mikro hizmet veritabanıdır. 

Merhaba mikro yaklaşımı hakkında daha fazla bilgi için okuma [mikro yaklaşım toobuilding uygulamalar neden?](service-fabric-overview-microservices.md)

## <a name="container-deployment-and-orchestration"></a>Kapsayıcı dağıtım ve düzenleme
Service Fabric olan Microsoft'un [kapsayıcı orchestrator](service-fabric-cluster-resource-manager-introduction.md) mikro makine bir kümede dağıtma. Mikro hello kullanarak birçok yolla geliştirilebilir [Service Fabric modellerini programlama](service-fabric-choose-framework.md), [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md), toodeploying [tercih ettiğiniz herhangi bir kod](service-fabric-deploy-existing-app.md). Önemlisi, hem işlemlerde Hizmetleri ve Merhaba kapsayıcılara Hizmetleri'nde karıştırabilirsiniz aynı uygulama. Yalnızca çok istiyorsanız[dağıtmak ve kapsayıcıları yönetmek](service-fabric-containers-overview.md), Service Fabric kapsayıcı orchestrator olarak mükemmel bir seçim değil.

## <a name="any-os-any-cloud"></a>Herhangi bir işletim sistemi, herhangi bir bulut
Service Fabric her yerde çalışır. Azure dahil olmak üzere birçok ortamda veya şirket içinde Windows Server veya Linux için Service Fabric kümeleri oluşturabilirsiniz. Hatta diğer ortak bulutlarda kümeleri oluşturabilirsiniz. Ayrıca, hello geliştirme ortamında hello SDK yer alan **aynı** toohello üretim ortamında, söz konusu hiçbir Öykünücüler. Diğer bir deyişle, ne yerel geliştirme kümenizde çalışan diğer ortamlarda toohello kümelerini dağıtır.

![Service Fabric platformundan][Image1]

Şirket içi oluşturma hakkında daha fazla bilgi kümeleri için okuma [Windows Server veya Linux üzerinde bir küme oluşturma](service-fabric-deploy-anywhere.md) veya küme oluşturma Azure [hello Azure portal aracılığıyla](service-fabric-cluster-creation-via-portal.md).

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Durum bilgisiz ve durum bilgisi olan mikro Service Fabric için
Service Fabric mikro veya kapsayıcıları oluşması toobuild uygulamaları etkinleştirir. Durum bilgisiz mikro (örneğin, protokol ağ geçitleri ve web proxy) dışında bir istek ve yanıt hello hizmetinden değişebilir bir duruma bulundurmayan. Azure bulut Hizmetleri çalışan rolleri, bir durum bilgisi olmayan hizmetin bir örnektir. Durum bilgisi olan mikro (örneğin, kullanıcı hesapları, veritabanları, aygıtlar, Alışveriş sepetleri ve Kuyruklar) değişebilir, yetkili durumu hello istek ve yanıt ötesinde korur. Bugünün Internet ölçekli uygulamalar durum bilgisiz ve durum bilgisi olan mikro birleşiminden oluşur. 

Service Fabric ile anahtar differentation hello ile ya da durum bilgisi olan hizmetler oluşturma, güçlü odaklanmasına olan [yerleşik programlama modelleri ](service-fabric-choose-framework.md) veya kapsayıcılı durum bilgisi olan hizmetler ile. Merhaba [uygulama senaryoları](service-fabric-application-scenarios.md) durum bilgisi olan hizmetler kullanıldığı hello senaryolar açıklanmaktadır.


## <a name="application-lifecycle-management"></a>Uygulama yaşam döngüsü yönetimi
Service Fabric hello tam uygulama yaşam döngüsü ve CI/CD kapsayıcıları dahil olmak üzere bulut uygulamaları için destek sağlar. Bu yaşam döngüsünün geliştirme aşamasından dağıtım, günlük yönetim ve Bakım tooeventual yetkisini içerir.

Service Fabric uygulama yaşam döngüsü yönetimi özellikleri uygulama yöneticileri ve BT işleçleri toouse basit ve düşük dokunma iş akışları tooprovision etkinleştirmek, dağıtma, düzeltme eki ve uygulamaları izleyin. Bu yerleşik iş akışları BT işleçleri tookeep uygulamaların sürekli olarak kullanılabilir hello yükünü büyük ölçüde azaltabilir.

Uygulamaların çoğu durum bilgisiz ve durum bilgisi olan mikro, kapsayıcıları ve birlikte dağıtılan diğer yürütülebilir bir birleşiminden oluşur. Merhaba uygulamaları güçlü türleri sağlayarak, Service Fabric birden fazla uygulama örneğinin hello dağıtımını sağlar. Her örnek yönetilen ve bağımsız olarak yükseltme. Önemlisi, Service Fabric kapsayıcıları veya tüm yürütülebilir dosyaları dağıtmak ve bu güvenilir hale getirebilirsiniz. Örneğin, Service Fabric .NET, ASP.NET Core, node.js, Windows kapsayıcıları, Linux kapsayıcıları, Java sanal makineler, komut dosyaları, Angular veya gerçek anlamda her şeyi uygulamanızı yapan dağıtabilirsiniz.

Service Fabric tümleşik CI/CD araçlarıyla gibi [Visual Studio Team Services](https://www.visualstudio.com/team-services/), [Jenkins](https://jenkins.io/index.html), ve [Octopus dağıtmak](https://octopus.com/) ve herhangi diğer popüler CI/CD aracı ile kullanılabilir.

Uygulama yaşam döngüsü yönetimi hakkında daha fazla bilgi için okuma [uygulama yaşam döngüsü](service-fabric-application-lifecycle.md). Hakkında daha fazla bilgi için toodeploy herhangi bir kod bkz [Konuk yürütülebilir dağıtmak](service-fabric-deploy-existing-app.md).

## <a name="key-capabilities"></a>Temel işlevler
Service Fabric kullanarak şunları yapabilirsiniz:

* Windows veya Linux sıfır kod değişikliklerle çalıştırmak tooAzure veya tooon içi veri merkezleri dağıtın. Bir kez yazma ve herhangi bir yere tooany Service Fabric kümesi dağıtma.
* Merhaba Service Fabric programlama modelleri, kapsayıcı ya da herhangi bir kod kullanarak oluşan ölçeklenebilir mikro uygulamaları geliştirin.
* Yüksek oranda güvenilir durum bilgisiz ve durum bilgisi olan mikro geliştirin. Durum bilgisi olan mikro kullanarak uygulamanızın Hello tasarım basitleştirin. 
* Merhaba yeni Reliable Actors programlama modeli toocreate bulut nesnelerini self yer alan kodu ve durum kullanın.
* Dağıtma ve Windows kapsayıcıları ve Linux kapsayıcıları dahil kapsayıcıları düzenlemek. Service Fabric veri kullanan, durum bilgisi kapsayıcı orchestrator ' dir.
* Saniye cinsinden yüksek yoğunluklu yüzlerce veya binlerce uygulamalar veya makine başına kapsayıcılar olan uygulamalar dağıtın.
* Aynı uygulama yan yana ve her uygulama bağımsız olarak yükseltme hello farklı sürümlerini dağıtın.
* Merhaba yaşam döngüsü uygulamalarınızın çiğnemekten ve bölünemez yükseltmeleri dahil olmak üzere herhangi bir kapalı kalma süresi olmadan yönetin.
* Ölçeği genişletme veya ölçeklendirmek kümedeki düğümler hello sayısı. Düğümleri ölçeklendirirken uygulamalarınızı otomatik olarak ölçeklendirin.
* İzleme ve uygulamalarınızı hello durumunu tanılama ve otomatik onarım gerçekleştirmek için ilkeler ayarlama.
* Uygulamaları Hello dağıtılması hello kümede düzenlemek hello kaynak dengeleyicisi izleyin. Service Fabric hatalarından kurtarır ve hello dağıtım kullanılabilir kaynaklara bağlı iş yükünün en iyi duruma getirir.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi için:
  * [Neden bir mikro toobuilding uygulamaları yaklaşımını?](service-fabric-overview-microservices.md)
  * [Terminolojisi genel bakış](service-fabric-technical-overview.md)
* Hizmet dokunuz ayarı [geliştirme ortamı](service-fabric-get-started.md)  
* [Service Fabric destek seçenekleri](service-fabric-support.md) hakkında bilgi edinin

[Image1]: media/service-fabric-overview/Service-Fabric-Overview.png
