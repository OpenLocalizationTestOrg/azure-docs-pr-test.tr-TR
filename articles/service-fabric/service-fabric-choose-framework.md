---
title: "aaaService doku programlama modeline genel bakış | Microsoft Docs"
description: "Service Fabric hizmetleri oluşturmak için iki çerçeveleri sunar: Merhaba aktör çerçevesi ve hello Hizmetleri çerçevesi. Bunlar ayrı dengelemeler Basitlik ve denetim sağlar."
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: vturecek
ms.assetid: 974b2614-014e-4587-a947-28fcef28b382
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: vturecek
ms.openlocfilehash: b48af2a7b41935bdf0e4594c765f363e520c254e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-programming-model-overview"></a>Service Fabric programlama modeline genel bakış
Service Fabric birden çok yol toowrite sunar ve hizmetlerinizi yönetin. Hizmetleri toouse hello Service Fabric API'leri tootake tam anlamıyla hello platformun özellikleri ve uygulama çerçeveleri seçebilirsiniz. Hizmetleri herhangi bir dil veya basit bir Service Fabric kümesi üzerinde barındırılan bir kapsayıcıda çalışan kodu yazılmış derlenmiş bir yürütülebilir program da olabilir.

## <a name="guest-executables"></a>Konuk yürütülebilir dosyalar
A [Konuk yürütülebilir](service-fabric-deploy-existing-app.md) mevcut ise, uygulamanızdaki bir hizmet farklı çalıştır (herhangi bir dilde yazılmış) rasgele çalıştırılabilir. Konuk yürütülebilir dosyalar hello Service Fabric SDK'sı API'lerini doğrudan çağırmayın. Ancak bunlar hala özellikleri hello platformundan yararlanır, hizmet bulunabilirliği, özel durumu ve yük REST API'ları Service Fabric tarafından kullanıma sunulan çağırarak raporlama gibi sunar. Aynı zamanda tam uygulama yaşam döngüsü destek sahiptirler.

Konuk yürütülebilir dosyaları ile ilk dağıtmaya başlamak [Konuk yürütülebilir uygulama](service-fabric-deploy-existing-app.md).

## <a name="containers"></a>Kapsayıcılar
Varsayılan olarak, Service Fabric dağıtır ve Hizmetleri işlemler olarak etkinleştirir. Service Fabric da Hizmetleri'nde dağıtım [kapsayıcıları](service-fabric-containers-overview.md). Service Fabric, Windows Server 2016 Linux kapsayıcıları ve Windows kapsayıcıları dağıtımını destekler. Kapsayıcı görüntüleri tüm kapsayıcı depodan çekebilir ve toohello makine dağıtılabilir. Service Fabric durum bilgisiz veya durum bilgisi olan güvenilir hizmetler Konuk exectuables mevcut uygulamaları dağıtabilir veya kapsayıcıları ve Reliable Actors işlemleri Hizmetleri'nde karıştırabilirsiniz ve aynı uygulama kapsayıcılarında Hizmetleri'nde hello.

[Windows veya Linux hizmetlerinizi containerizing hakkında daha fazla bilgi edinin](service-fabric-deploy-container.md)

## <a name="reliable-services"></a>Reliable Services
Güvenilir hizmetler hello Service Fabric platformu ile tümleştirme ve hello tam platform özellik kümesinden yararlanabilirsiniz Hizmetleri yazmak için bir çerçevedir hafif. Güvenilir hizmetler en az bir hello Service Fabric çalışma zamanı toomanage hello kullanım ömrü boyunca hizmetlerinizi izin ve hello çalışma zamanı, hizmetleri toointeract izin veren API kümesi sağlar. Hello uygulama çerçevesi en az, tam vermiş tasarım ve uygulama seçeneklerin üzerinde denetlemek ve herhangi diğer uygulama çerçevesi, ASP.NET Core gibi kullanılan toohost olabilir.

Güvenilir hizmetler hello hizmeti her örneği eşit oluşturulur ve durumu Azure DB veya Azure Table Storage gibi harici bir çözümde kalıcı web sunucuları gibi durum bilgisiz, benzer toomost hizmet platformları olabilir.

Güvenilir hizmetler, durum doğrudan hello hizmetinde kendisini güvenilir koleksiyonları kullanarak burada kalıcı durum bilgisi olan, özel tooService doku, da olabilir. Durumu yüksek oranda çoğaltma yoluyla kullanılabilir hale ve, otomatik olarak Service Fabric tarafından yönetilen tüm bölümleme aracılığıyla dağıtılır.

[Reliable Services hakkında daha fazla bilgi](service-fabric-reliable-services-introduction.md) veya başlayın [ilk güvenilir hizmetiniz yazma](service-fabric-reliable-services-quick-start.md).

## <a name="reliable-actors"></a>Reliable Actors
Güvenilir hizmetler en üstünde oluşturulan hello güvenilir aktör hello aktör tasarım deseni temel alınarak hello sanal aktör deseni uygulayan bir uygulama çerçevesi çerçevedir. Merhaba güvenilir aktör çerçevesi yürütme aktörler olarak adlandırılan tek iş parçacıklı işlem ve durumunun bağımsız bir birim kullanır. Merhaba güvenilir aktör framework aktörler ve önceden ayarlanmış durumu kalıcılığını ve genişleme yapılandırmaları için yerleşik iletişim sağlar.

Reliable Actors kendisini Reliable Services üzerinde bir uygulama altyapısıdır olduğu gibi hello Service Fabric platformundan ve avantajları kümesinden hello tam hello platformu tarafından sunulan özelliklerden tam olarak tümleşiktir.

[Reliable Actors hakkında daha fazla bilgi](service-fabric-reliable-actors-introduction.md) veya başlayın [ilk güvenilir aktör hizmetiniz yazma](service-fabric-reliable-actors-get-started.md)

## <a name="aspnet-core"></a>ASP.NET Çekirdeği
Service Fabric tümleşir [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) için Web ve API hizmetleri oluşturmaya uygulamanızın veya bir parçası olarak dahil edilebilir. 

[ASP.NET Core kullanarak bir ön uç hizmet oluşturma](service-fabric-add-a-web-frontend.md)

## <a name="next-steps"></a>Sonraki adımlar
[Service Fabric ve kapsayıcıları genel bakış](service-fabric-containers-overview.md)

[Güvenilir Hizmetleri'ne Genel Bakış](service-fabric-reliable-services-introduction.md)

[Güvenilir Hizmetleri'ne Genel Bakış](service-fabric-reliable-actors-introduction.md)

[Service Fabric ve ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)




