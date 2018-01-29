---
title: "Azure'da Service Fabric'e genel bakış | Microsoft Docs"
description: "Ölçek ve dayanıklılık sağlamak için uygulamaların birçok mikro hizmetten oluşturulduğu Service Fabric'e genel bakış. Service Fabric, bulut için ölçeklenebilir, güvenilir ve kolayca yönetilebilir uygulamalar derlemek amacıyla kullanılan dağıtılmış bir sistemler platformudur."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: masnider
ms.assetid: bbcc652a-a790-4bc4-926b-e8cd966587c0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: overview
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/20/2017
ms.author: msfussell
ms.custom: mvc
ms.openlocfilehash: 4aca25f74d3e22911ab5059a8cdec45f189dc8cf
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/08/2017
---
# <a name="overview-of-azure-service-fabric"></a>Azure Service Fabric'e genel bakış
Azure Service Fabric; ölçeklenebilir ve güvenilir mikro hizmetleri ve kapsayıcıları paketlemeyi, dağıtmayı ve yönetmeyi kolaylaştırmayı sağlayan bir dağıtılmış sistemler platformudur. Service Fabric ayrıca bulut yerel uygulamalarını geliştirme ve yönetme sürecinde karşılaşılan başlıca sorunların giderilmesini de sağlar. Geliştiriciler ve yöneticiler, karmaşık altyapı sorunlarını çözmeye çalışmak yerine görev açısından kritik, zorlu iş yüklerini uygulamaya odaklanabilir. Service Fabric, bu iş yüklerinin ölçeklenebilir, güvenilir ve yönetilebilir olmasını sağlar. Service Fabric, kapsayıcılarda çalıştırılan 1. katman bulut ölçeğindeki bu kurumsal sınıf uygulamaları oluşturmak ve yönetmek için tasarlanan yeni nesil bir platformdur.

Bu kısa videoda Service Fabric ve mikro hizmetler tanıtılır: <center><a target="_blank" href="https://aka.ms/servicefabricvideo">  
<img src="./media/service-fabric-overview/OverviewVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="applications-composed-of-microservices"></a>Mikro hizmetlerden oluşturulmuş uygulamalar 
Service Fabric, makinenin küme olarak adlandırılan bir paylaşılan havuzunda yüksek yoğunlukta çalışan mikro hizmetlerden oluşturulmuş, ölçeklendirilebilir ve güvenilir uygulamalar oluşturmanıza ve bunları yönetmenize olanak tanır. Dağıtılmış, ölçeklendirilebilir, durum bilgisi olmayan, durum bilgisi olan ve kapsayıcılarda çalıştırılan mikro hizmetler oluşturmak için gelişmiş, basit bir çalışma zamanı sağlar. Ayrıca, kapsayıcılı hizmetler de dahil olmak üzere dağıtılan uygulamaları sağlamak, dağıtmak, izlemek, yükseltmek/yama uygulamak ve silmek için kapsamlı uygulama yönetim özellikleri de sağlar.

Service Fabric bugün Azure SQL Veritabanı, Azure Cosmos DB, Cortana, Microsoft Power BI, Microsoft Intune, Azure Event Hubs, Azure IoT Hub, Dynamics 365, Skype Kurumsal ve birçok temel Azure hizmeti gibi çok sayıda Microsoft hizmetini güçlendirir.

Service Fabric, gerektiği kadar küçükten başlatılabilecek ve yüzlerce veya binlerce makineyle muazzam bir ölçeğe kadar büyütülebilecek bulut yerel hizmetleri oluşturmaya uyarlanmıştır.

Günümüzde İnternet ölçeğindeki hizmetler mikro hizmetlerden oluşturulur. Mikro hizmetlere örnek olarak protokol ağ geçitleri, kullanıcı profilleri, alışveriş sepetleri, envanter işleme, kuyruklar ve önbellekler verilebilir. Service Fabric, durum bilgisi olan veya olmayan her mikro hizmete (veya kapsayıcıya) benzersiz bir ad veren bir mikro hizmetler platformudur.

Service Fabric, bu mikro hizmetlerden oluşturulmuş uygulamalara kapsamlı çalışma zamanı ve yaşam döngüsü yönetim özellikleri sağlar. Mikro hizmetleri, Service Fabric kümesi genelinde dağıtılan ve etkinleştirilen kapsayıcıların içinde barındırır. Sanal makinelerden taşıyıcılara geçiş, büyüklük sırasına göre yoğunluk artışını mümkün kılar. Benzer biçimde, kapsayıcılardan bu kapsayıcıların içindeki mikro hizmetlere geçtiğinizde de yoğunlukta başka bir büyüklük sırası mümkün olur. Örneğin, Azure SQL Veritabanı'nın tek bir kümesi, toplamda yüz binlerce veritabanını barındıran on binlerce kapsayıcının çalıştırıldığı yüzlerce makineden oluşur. Her veritabanı bir durum bilgisi olan bir Service Fabric mikro hizmetidir. 

Mikro hizmetler yaklaşımı hakkında daha fazla bilgi edinmek için [Uygulamaları oluşturmak için neden mikro hizmetler yaklaşımı öneriliyor?](service-fabric-overview-microservices.md)

## <a name="container-deployment-and-orchestration"></a>Kapsayıcı dağıtımı ve düzenlemesi
Service Fabric, Microsoft'un bir makine kümesine mikro hizmetleri dağıtan [kapsayıcı düzenleyicisidir](service-fabric-cluster-resource-manager-introduction.md). Mikro hizmetler, [Service Fabric programlama modelleri](service-fabric-choose-framework.md), [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) kullanmaktan [tercih ettiğiniz herhangi bir kodun](service-fabric-deploy-existing-app.md) dağıtılmasına kadar birçok yolla geliştirilebilir. Önemli olan, işlemlerdeki hizmetlerle kapsayıcılardaki hizmetleri aynı uygulama içinde karma kullanabilmenizdir. Yalnızca [kapsayıcıları dağıtma ve yönetmek](service-fabric-containers-overview.md) istiyorsanız, Service Fabric kapsayıcı düzenleyicisi olarak mükemmel bir seçenektir.

## <a name="any-os-any-cloud"></a>Tüm işletim sistemleri, tüm bulutlar
Service Fabric her yerde çalıştırılır. Service Fabric için birçok ortamda, örneğin Azure'da, şirket içinde, Windows Server'da veya Linux'ta kümeler oluşturabilirsiniz. Hatta diğer genel bulutlarda bile kümeler oluşturabilirsiniz. Buna ek olarak, SDK'daki geliştirme ortamı üretim ortamıyla **özdeştir**; öykünücüler yoktur. Diğer bir deyişle, yerel geliştirme kümenizde çalıştırılan, diğer ortamlardaki kümelere dağıtılır.

![Service Fabric platformu][Image1]

Windows geliştirmesi için, Service Fabric .NET SDK'sı Visual Studio ve Powershell ile tümleştirilmiştir. Bkz. [Windows üzerinde geliştirme ortamınızı hazırlama](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started.md). Linux geliştirmesi için, Service Fabric Java SDK'sı Eclipse ile tümleştirilmiştir ve Java, .NET Core ve kapsayıcı uygulamaları için şablonların oluşturulmasında Yeoman kullanılır. Bkz. [Linux üzerinde geliştirme ortamınızı hazırlama](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started.md)

Kümeleri oluşturma hakkında daha fazla bilgi için, [Windows Server veya Linux'ta küme oluşturma](service-fabric-deploy-anywhere.md) konusunu veya Azure için [Azure Portal üzerinden küme oluşturma](service-fabric-cluster-creation-via-portal.md) konusunu okuyun.

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Service Fabric için durum bilgisi olan ve olmayan mikro hizmetler
Service Fabric, mikro hizmetlerden veya kapsayıcılardan oluşmuş uygulamalar hazırlamanıza olanak tanır. Durum bilgisi olmayan mikro hizmetler (protokol ağ geçitleri ve web ara sunucuları gibi), isteğin veya hizmetten gelen yanıtının dışında değişebilir bir durum bilgisi bulundurmaz. Azure Cloud Services çalışan rolleri, durum bilgisi olmayan hizmet örnekleridir. Durum bilgisi olan mikro hizmetler (kullanıcı hesapları, veritabanları, cihazlar, alışveriş sepetleri ve kuyruklar gibi), isteğin ve yanıtının ötesinde değişebilir, yetkili bir durum bilgisi bulundurur. Günümüzün İnternet ölçeğindeki uygulamaları, durum bilgisi olan ve olmayan mikro hizmetlerin bileşiminden oluşur. 

Service Fabric'in ayırt edici özelliği, [yerleşik programlama modelleriyle](service-fabric-choose-framework.md) veya kapsayıcılı durum bilgisi olan hizmetlerle, büyük ölçüde durum bilgisi olan hizmetler oluşturmaya odaklanmasıdır. [Uygulama senaryoları](service-fabric-application-scenarios.md), durum bilgisi olan hizmetlerin kullanıldığı senaryoları açıklar.


## <a name="application-lifecycle-management"></a>Uygulama yaşam döngüsü yönetimi
Service Fabric, kapsayıcılar da dahil olmak üzere bulut uygulamalarının tüm uygulama yaşam döngüsü ve CI/CD için destek sağlar. Bu yaşam döngüsü geliştirme, dağıtım, günlük yönetim ve bakımdan sonunda kullanımdan çıkarmaya kadar tüm aşamaları içerir.

Service Fabric uygulama yaşam döngüsü yönetim özellikleri, uygulama yöneticileriyle BT operatörlerinin basit, az müdahale gerektiren iş akışları kullanarak uygulamaları sağlamasına, dağıtmasına, yama uygulamasına ve izlemesine olanak tanır. Bu yerleşik iş akışları BT operatörlerinin uygulamaları sürekli kullanılabilir durumda tutma yüklerini büyük ölçüde azaltır.

Uygulamaların çoğu durum bilgisi olan ve olmayan mikro hizmetler, kapsayıcılar ve birlikte dağıtılan diğer yürütülebilir dosyaların bileşiminden oluşur. Service Fabric güçlü uygulama türleri sağlayarak, birden çok uygulama örneğinin dağıtılmasına olanak tanır. Her örnek bağımsız olarak yönetilir ve yükseltilir. Önemli olan, Service Fabric'in kapsayıcıları ve yürütülebilir dosyaları dağıtabilmesi ve bunların güvenilir olmasını sağlamasıdır. Örneğin Service Fabric .NET, ASP.NET Core, node.js, Windows kapsayıcıları, Linux kapsayıcıları, Java sanal makineleri, betikler, Angular veya sözcük anlamıyla uygulamanızı oluşturan her şeyi dağıtabilir.

[Visual Studio Team Services](https://www.visualstudio.com/team-services/), [Jenkins](https://jenkins.io/index.html) ve [Octopus Deploy](https://octopus.com/) gibi CI/CD araçlarıyla tümleştirilmiş olan Service Fabric, diğer herhangi bir popüler CI/CD aracıyla da kullanılabilir.

Uygulama yaşam döngüsü yönetimi hakkında daha fazla bilgi için, [Uygulama yaşam döngüsü](service-fabric-application-lifecycle.md) konusunu okuyun. Herhangi bir kodun dağıtımı hakkında daha fazla bilgi için, [konuk yürütülebilir dosyasını dağıtma](service-fabric-deploy-existing-app.md) konusuna bakın.

## <a name="key-capabilities"></a>Temel işlevler
Service Fabric kullanarak:

* Sıfır kod değişikliğiyle Azure'a ya da Windows veya Linux çalıştıran şirket içi veri merkezlerine dağıtım yapabilirsiniz. Bir kez yazıp herhangi bir Service Fabric kümesinde her yere dağıtabilirsiniz.
* Service Fabric programlama modellerini, kapsayıcıları veya herhangi bir kodu kullanarak mikro hizmetlerden oluşmuş ölçeklendirilebilir uygulamalar geliştirebilirsiniz.
* Durum bilgisi olan ve olmayan son derece güvenilir mikro hizmetler geliştirebilirsiniz. Durum bilgisi olan mikro hizmetler kullanarak uygulamanızın tasarımını basitleştirebilirsiniz. 
* Kendi içinde kodu ve durumu olan bulut nesneleri oluşturmak için yeni Reliable Actors programlama modelini kullanabilirsiniz.
* Windows kapsayıcılarını ve Linux kapsayıcılarını içeren kapsayıcılar dağıtabilir ve bunları düzenleyebilirsiniz. Service Fabric veri farkındalığına sahip, durum bilgisi olan bir kapsayıcı düzenleyicisidir.
* Uygulamaları, makine başına yüzlerce veya binlerce uygulama ya da kapsayıcıyla yüksek yoğunlukta, saniyeler içinde dağıtabilirsiniz.
* Aynı uygulamanın farklı sürümlerini yan yana dağıtabilir ve her uygulamayı bağımsız olarak yükseltebilirsiniz.
* Sistemi kapalı tutmaya gerek kalmadan, işi kesen ve kesmeyen yükseltmeler de dahil olmak üzere uygulamalarınızın yaşam döngüsünü yönetebilirsiniz.
* Kümedeki düğümlerin sayısını artırabilir veya azaltabilirsiniz. Siz düğümleri ölçeklendirirken, uygulamalarınız otomatik olarak ölçeklendirilir.
* Uygulamalarınızın durumunu izleyebilir ve tanılayabilir, otomatik onarımlar yapmak için ilkeler ayarlayabilirsiniz.
* Kaynak dengeleyicisinin küme genelinde uygulamaların yeniden dağıtımını nasıl düzenlediğini izleyebilirsiniz. Service Fabric hatalardan kurtarır ve kullanılabilir kaynaklar temelinde yük dağıtımını iyileştirir.

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi için:
  * [Uygulamaları oluşturmak için neden mikro hizmetler yaklaşımı öneriliyor?](service-fabric-overview-microservices.md)
  * [Terminolojiye genel bakış](service-fabric-technical-overview.md)
* [Windows dağıtım ortamınızı](service-fabric-get-started.md) ayarlama  
* [Linux dağıtım ortamınızı](service-fabric-get-started-linux.md) ayarlama
* [Service Fabric destek seçenekleri](service-fabric-support.md) hakkında bilgi edinin

[Image1]: media/service-fabric-overview/Service-Fabric-Overview.png
