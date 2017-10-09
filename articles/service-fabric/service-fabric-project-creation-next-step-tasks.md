---
title: "aaaService doku proje oluşturma sonraki adımlar | Microsoft Docs"
description: "Bu makale bağlantılar tooa kümesi çekirdeği geliştirme görevleri için Service Fabric içerir"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 45598bfabedf280fba8af449ef920f40b409a609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a>Service Fabric uygulaması ve sonraki adımlar
Azure Service Fabric uygulamanızı oluşturuldu. Bu makalede hello yapısıyla projenizi ve bazı olası sonraki adımlar açıklanmaktadır.

## <a name="your-application"></a>Uygulamanızı
Her yeni uygulama, bir uygulama projesi içerir. Bir veya iki ek projeleri, seçilen hizmet hello türüne bağlı olarak olabilir.

### <a name="hello-application-project"></a>Merhaba uygulama projesi
Merhaba uygulama projesi oluşur:

* Uygulamayı oluşturan başvurular toohello Hizmetleri kümesi.
* Üç toomaintain Tercihler--Tercihler ilgili tooa küme uç noktası ve olup tooperform yükseltme dağıtımları varsayılan olarak gibi farklı ortamlarda çalışmak için kullanabileceğiniz profilleri (1-düğümü yerel, 5-Node yerel ve bulut) yayımlayın.
* Üç uygulama parametreleri dosyalarını (aynı yukarıdaki) bir hizmet için bölümleri toocreate hello sayısı gibi toomaintain ortama özgü uygulama yapılandırmaları kullanabilirsiniz.
* Bir dağıtım komut dosyası toodeploy uygulamanızı hello komut satırından veya bir otomatik sürekli tümleştirme ve dağıtım ardışık parçası olarak kullanabilirsiniz.
* Merhaba uygulaması açıklar hello uygulama bildirimi. Merhaba bildirimi hello ApplicationPackageRoot klasörü altında bulabilirsiniz.

### <a name="stateless-service"></a>Durum bilgisiz hizmeti
Yeni bir durum bilgisiz hizmet eklediğinizde, Visual Studio gelen descended türünü içeren bir hizmet projesi tooyour çözümünü ekler `StatelessService`. Merhaba hizmeti bir sayaç yerel bir değişkende artırır.

### <a name="stateful-service"></a>Durum bilgisi olan hizmet
Yeni bir durum bilgisi olan hizmet eklediğinizde, Visual Studio gelen descended türünü içeren bir hizmet projesi tooyour çözümünü ekler `StatefulService`. Merhaba hizmet artırır bir sayaç kendi `RunAsync` yöntemi ve depoları hello sonucunda bir `ReliableDictionary`.

### <a name="actor-service"></a>Aktör hizmeti
Yeni bir güvenilir aktör eklediğinizde, Visual Studio iki projeler tooyour çözümü ekler: aktör projesinde hem de bir arabirim projesi.

Merhaba aktör proje ayarı için yöntemler sağlar ve bir sayacın başlangıç değerini alma güvenilir bir şekilde hello aktör'ın durum kalıcı. Merhaba arabirimi proje bir arabirim diğer hizmetler sağlar tooinvoke hello aktör kullanabilirsiniz.

### <a name="stateless-web-api"></a>Durum bilgisiz Web API'si
Merhaba durum bilgisiz Web API projesi sağlar temel bir web hizmeti uygulama tooexternal istemcileriniz tooopen kullanabilirsiniz. Nasıl hello proje yapılandırılmış hakkında daha fazla bilgi için bkz: [OWIN kendi kendine barındırma ile Service Fabric Web API Hizmetleri](service-fabric-reliable-services-communication-webapi.md).


### <a name="aspnet-core"></a>ASP.NET Çekirdeği
Merhaba Service Fabric SDK aynı kümesini tek başına ASP.NET Core projeleri için kullanılabilir olan ASP.NET Core şablonları, hello sağlar: boş [Web API][aspnet-webapi], ve [Web uygulaması][aspnet-webapp].

### <a name="guest-executables-and-guest-containers"></a>Konuk yürütülebilir dosyalar ve Konuk kapsayıcıları

Service Fabric 'Konuk' hello platformun programlama modeli ile yerleşik olmayan bir hizmettir. Bir konuk hello ikili dosyalar ya da paketleyebilirsiniz [hello uygulama paketindeki doğrudan](service-fabric-deploy-existing-app.md) veya [bir kapsayıcı görüntüsü aracılığıyla](service-fabric-deploy-container.md). Her iki durumda da, Visual Studio hello hello gerekli yapıları oluşturur **ApplicationPackageRoot** hello uygulama projesi klasörü. Visual Studio Hello kodu başka bir yerde zaten mevcut olduğundan yeni bir hizmet projesi oluşturmaz. Konuk projeleri hello Service Fabric uygulaması projesi toomanage isterseniz, bunları toohello ekleyebilirsiniz aynı Visual Studio çözümü.

## <a name="next-steps"></a>Sonraki adımlar
### <a name="create-an-azure-cluster"></a>Bir Azure kümesi oluşturma
Merhaba Service Fabric SDK, geliştirme ve test için yerel bir küme sağlar. Azure, kümede toocreate bkz [hello Azure portal ' bir Service Fabric kümesi ayarlama][create-cluster-in-portal].

### <a name="publish-your-application-tooazure"></a>Uygulama tooAzure yayımlama
Visual Studio tooan Azure küme uygulamadan doğrudan yayımlayabilirsiniz. toolearn nasıl bkz [uygulama tooAzure yayımlama][publish-app-to-azure].

### <a name="use-service-fabric-explorer-toovisualize-your-cluster"></a>Service Fabric Explorer toovisualize kümenizi kullanın
Service Fabric Explorer kolay bir yolu toovisualize dağıtılan uygulamalar ve fiziksel düzenini de dahil olmak üzere kümenizi sunar. toolearn daha, fazla [Service Fabric Explorer kullanarak kümenizi görselleştirme][visualize-with-sfx].

### <a name="version-and-upgrade-your-services"></a>Sürümü ve hizmetlerinizi yükseltme
Service Fabric bağımsız sürüm oluşturma ve uygulamada bağımsız Hizmetleri yükseltme sağlar. toolearn daha, fazla [sürüm oluşturma ve hizmetlerinizi yükseltme][app-upgrade-tutorial].

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a>Visual Studio Team Services ile sürekli tümleştirme yapılandırın
Service Fabric uygulamanız için bir sürekli tümleştirme işlemini ayarlayabilirsiniz nasıl toolearn bkz [sürekli tümleştirme ile Visual Studio Team Services yapılandırma][ci-with-vso].

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
