---
title: "Java, ilk aktör tabanlı Azure mikro hizmet oluşturma | Microsoft Docs"
description: "Bu öğretici oluşturma, hata ayıklama ve Service Fabric Reliable Actors kullanarak basit bir aktör tabanlı hizmet dağıtma adımları açıklanmaktadır."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 288f1ed1016f50031065e66444d2562427194dc7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-reliable-actors"></a>Reliable Actors ile çalışmaya başlama
> [!div class="op_single_selector"]
> * [Windows üzerinde C#](service-fabric-reliable-actors-get-started.md)
> * [Linux üzerinde Java](service-fabric-reliable-actors-get-started-java.md)
> 
> 

Bu makalede, Azure Service Fabric Reliable Actors temelleri açıklanır ve oluşturma ve Java basit bir güvenilir aktör uygulama dağıtma size yol gösterir.

## <a name="installation-and-setup"></a>Yükleme ve Kurulum
Başlamadan önce makinenizde ayarlanan Service Fabric geliştirme ortamı sahip olduğunuzdan emin olun.
Bunu ayarlamak gerekiyorsa, Git [Mac Başlarken](service-fabric-get-started-mac.md) veya [Linux'ta Başlarken](service-fabric-get-started-linux.md).

## <a name="basic-concepts"></a>Temel kavramlar
Reliable Actors ile çalışmaya başlamak için yalnızca birkaç temel kavramları anlamanız gerekir:

* **Aktör hizmeti**. Güvenilir aktörler Service Fabric altyapısında dağıtılabilir Reliable Services paketlenir. Aktör örnekleri adlı hizmet örneği içinde etkinleştirilir.
* **Aktör kayıt**. Olarak Reliable Services ile güvenilir aktör hizmeti Service Fabric çalışma zamanı ile kayıtlı olması gerekir. Ayrıca, aktör türü aktör çalışma zamanı ile kayıtlı olması gerekir.
* **Aktör arabirimi**. Aktör arabirimi bir aktör, türü kesin belirlenmiş bir ortak arabirimi tanımlamak için kullanılır. Güvenilir aktör modeli terminolojisinde aktör arabirimi aktör anlayabileceği iletileri ve işlem türlerini tanımlar. Aktör arabirimi "(uyumsuz) aktör göndermek için" diğer aktörler ve istemci uygulamalar tarafından kullanılır. Güvenilir aktörler birden çok arabirimi uygulayabilirsiniz.
* **ActorProxy sınıfı**. ActorProxy sınıfı aktör arabirimi aracılığıyla kullanıma sunulan yöntemleri çağırmak için istemci uygulamaları tarafından kullanılır. ActorProxy sınıfı iki önemli işlevleri sağlar:
  
  * Ad çözümlemesi: küme (Bul onu barındırıldığı küme düğümünün) aktör bulabilir.
  * Hata işleme: yöntem çağrılarına yeniden deneyin ve yeniden aktör konumu, örneğin, kümedeki başka bir düğüme yeniden konumlandırılmasını aktör gerektiren bir hatadan sonra çözümleyin.

Aktör arabirimlerine ilgilidir aşağıdaki kurallar tümleştirilmediği şunlardır:

* Aktör arabirim yöntemleri aşırı yüklenemez.
* Aktör arabirimi yöntemlerini çıkışı olmamalıdır, ref veya isteğe bağlı parametreler.
* Genel arabirimler desteklenmez.

## <a name="create-an-actor-service"></a>Aktör hizmeti oluşturma
Yeni bir Service Fabric uygulaması oluşturmaya başlayın. Linux için Service Fabric SDK'sı bir Yeoman içeren bir durum bilgisiz Service Service Fabric uygulaması için askılamayı sağlamak için oluşturucu. Aşağıdaki Yeoman çalıştırarak komutu:

```bash
$ yo azuresfjava
```

Oluşturmak için yönergeleri izleyin bir **güvenilir aktör hizmeti**. Bu öğretici için "HelloWorldActorApplication" uygulama adı ve aktör "HelloWorldActor." Aşağıdaki yapı iskelesi oluşturulacak:

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a>Güvenilir aktörler temel yapı taşları
Daha önce açıklanan temel kavramları güvenilir aktör hizmetinin temel yapı taşlarının çevir.

### <a name="actor-interface"></a>Aktör arabirimi
Aktör arabirimi tanımını içerir. Bu arabirim aktör uygulama ve böylece genellikle aktör uygulamasından ayrı bir yerde tanımlamak için mantıklı ve birden çok diğer hizmetlerin veya istemci uygulamaları tarafından paylaşılan aktör çağırma istemcileri tarafından paylaşılan aktör sözleşme tanımlar.

`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a>Aktör hizmeti
Bu, aktör uygulama ve aktör kayıt kodunu içerir. Aktör sınıfı aktör arabirimini uygular. Burada, aktör çalıştığını budur.

`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a>Aktör kayıt
Aktör hizmeti Service Fabric çalışma zamanında bir hizmet türü ile kayıtlı olması gerekir. Aktör hizmetinin aktör örneklerinizi çalışması sırayla aktör türünüz aktör hizmeti ile kaydedilmelidir. `ActorRuntime` Kayıt yöntemi, bu iş aktörleri gerçekleştirir.

`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a>Test İstemcisi
Bu basit bir sınama istemci uygulaması olan aktör hizmetinizi test etmek için Service Fabric uygulamadan ayrı olarak çalıştırabilirsiniz. Bir örnek, burada ActorProxy etkinleştirmek ve aktör örnekleri ile iletişim kurmak için kullanılabilir. Hizmetiniz ile dağıtılan.

### <a name="the-application"></a>Uygulama
Son olarak, uygulama aktör hizmeti ve gelecekte birlikte dağıtım için eklemiş olabileceğiniz diğer hizmetler paketler. İçerdiği *ApplicationManifest.xml* ve aktör hizmet paketi için yer tutucu.

## <a name="run-the-application"></a>Uygulamayı çalıştırma

Yeoman yapı iskelesi uygulama oluşturup dağıtın ve uygulamayı kaldırmak için komut dosyaları bash bir gradle komut dosyası içerir. Uygulamayı dağıtmak için ilk uygulama gradle ile oluşturun:

```bash
$ gradle
```

Bu Service Fabric CLI araçlarını kullanarak dağıtılan bir Service Fabric uygulama paketi oluşturur.

### <a name="deploy-service-fabric-cli"></a>Service Fabric CLI dağıtma

İnstall.sh betik uygulama paketi dağıtmak için gerekli Service Fabric CLI (sfctl) komutlarını içerir.
Uygulamayı dağıtmak için install.sh komut dosyasını çalıştırın.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>Sonraki adımlar

* [Service Fabric CLI ile çalışmaya başlama](service-fabric-cli.md)
