---
title: "aaaCreate, ilk aktör tabanlı Azure mikro hizmet Java | Microsoft Docs"
description: "Bu öğretici oluşturma, hata ayıklama ve Service Fabric Reliable Actors kullanarak basit bir aktör tabanlı hizmet dağıtma hello adımlarda size yol gösterir."
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
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a>Reliable Actors ile çalışmaya başlama
> [!div class="op_single_selector"]
> * [Windows üzerinde C#](service-fabric-reliable-actors-get-started.md)
> * [Linux üzerinde Java](service-fabric-reliable-actors-get-started-java.md)
> 
> 

Bu makalede, Azure Service Fabric Reliable Actors hello temelleri açıklanır ve oluşturma ve Java basit bir güvenilir aktör uygulama dağıtma size yol gösterir.

## <a name="installation-and-setup"></a>Yükleme ve Kurulum
Başlamadan önce makinenizde ayarlanan hello Service Fabric geliştirme ortamı sahip olduğunuzdan emin olun.
Tooset ihtiyacınız varsa bunun Git çok[Mac Başlarken](service-fabric-get-started-mac.md) veya [Linux'ta Başlarken](service-fabric-get-started-linux.md).

## <a name="basic-concepts"></a>Temel kavramlar
Reliable Actors ile yalnızca, başlatılan tooget birkaç temel kavramları toounderstand gerekir:

* **Aktör hizmeti**. Güvenilir aktörler hello Service Fabric altyapısında dağıtılabilir Reliable Services paketlenir. Aktör örnekleri adlı hizmet örneği içinde etkinleştirilir.
* **Aktör kayıt**. Olarak Reliable Services ile güvenilir aktör hizmeti ile Merhaba Service Fabric çalışma zamanı kayıtlı toobe gerekir. Ayrıca, hello aktör türü hello aktör çalışma zamanı ile kayıtlı toobe gerekir.
* **Aktör arabirimi**. Merhaba aktör kullanılan toodefine bir aktör kesin türü belirtilmiş bir ortak arabiriminin bir arabirimdir. Hello güvenilir aktör modeli terminolojisi, aktör Merhaba ileti türlerini anlamak ve işleyebilirsiniz hello hello aktör arabirimi tanımlar. Merhaba aktör arabirimi diğer aktörler tarafından kullanılır ve istemci uygulamaları çok "(uyumsuz) iletileri toohello aktör Gönder". Güvenilir aktörler birden çok arabirimi uygulayabilirsiniz.
* **ActorProxy sınıfı**. Merhaba ActorProxy sınıfı istemci uygulamaları tooinvoke tarafından kullanılan hello hello aktör arabirimi aracılığıyla kullanıma sunulan yöntemleri. Merhaba ActorProxy sınıfı iki önemli işlevleri sağlar:
  
  * Ad çözümlemesi: mümkün toolocate hello aktör (bunu barındırıldığı hello kümesinin Bul hello düğümü) hello kümedeki olduğu.
  * Hata işleme: Bu yöntem çağrılarına yeniden deneyin ve sonra hello aktör konumu yeniden çözümlemek, örneğin, hello aktör toobe gerektiren bir hata hello kümedeki tooanother düğümde yeniden konumlandırılmasını.

tooactor arabirimleri ilgilidir kuralları aşağıdaki hello tümleştirilmediği şunlardır:

* Aktör arabirim yöntemleri aşırı yüklenemez.
* Aktör arabirimi yöntemlerini çıkışı olmamalıdır, ref veya isteğe bağlı parametreler.
* Genel arabirimler desteklenmez.

## <a name="create-an-actor-service"></a>Aktör hizmeti oluşturma
Yeni bir Service Fabric uygulaması oluşturmaya başlayın. Merhaba Linux için Service Fabric SDK içeren bir Yeoman durum bilgisiz hizmeti ile bir Service Fabric uygulaması için oluşturucu tooprovide hello askılamayı. Merhaba çalıştırarak Yeoman komutu:

```bash
$ yo azuresfjava
```

Merhaba yönergeleri toocreate izleyin bir **güvenilir aktör hizmeti**. Bu öğretici için ad hello uygulama "HelloWorldActorApplication" ve hello aktör "HelloWorldActor." Yapı iskelesi aşağıdaki hello oluşturulacak:

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
daha önce açıklanan hello temel kavramları hello temel yapı taşlarını bir güvenilir aktör hizmeti çevir.

### <a name="actor-interface"></a>Aktör arabirimi
Bu hello aktör hello arabirimi tanımını içerir. Bu arabirim hello aktör uygulama ve genellikle bu olan bir yerde hello aktör uygulamasından ayırın ve birden çok diğer tarafından paylaşılan algılama toodefine kolaylaştırır şekilde hello aktör çağırma hello istemcileri tarafından paylaşılan hello aktör sözleşme tanımlar Hizmet veya istemci uygulamaları.

`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a>Aktör hizmeti
Bu, aktör uygulama ve aktör kayıt kodunu içerir. Merhaba Aktör sınıfı hello aktör arabirimini uygular. Burada, aktör çalıştığını budur.

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
Merhaba aktör hizmeti hello Service Fabric çalışma zamanında bir hizmet türü ile kayıtlı olması gerekir. Merhaba, aktör örneklerinizi aktör hizmeti toorun sipariş, aktör türünüz hello aktör hizmeti ile da kayıtlı olması gerekir. Merhaba `ActorRuntime` kayıt yöntemi, bu iş aktörleri gerçekleştirir.

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
Bu basit bir sınama istemci uygulaması olan aktör hizmetinizi hello Service Fabric uygulaması tootest ayrı olarak çalıştırabilirsiniz. Bir örnek burada hello ActorProxy kullanılan tooactivate olması ve aktör örnekleriyle iletişim. Hizmetiniz ile dağıtılan.

### <a name="hello-application"></a>Merhaba uygulaması
Son olarak, hello uygulama paketleri aktör hizmeti ve hello birlikte dağıtım için gelecekte ekleme olasılığınız diğer hizmetler hello. Merhaba içerdiği *ApplicationManifest.xml* ve hello aktör hizmet paketi için yer tutucu.

## <a name="run-hello-application"></a>Merhaba uygulamayı çalıştırın

Merhaba Yeoman yapı iskelesi, gradle betik toobuild hello uygulama ve bash betikleri toodeploy ve Kaldır uygulamayı içerir. toodeploy hello uygulama ilk yapı hello gradle ile:

```bash
$ gradle
```

Bu Service Fabric CLI araçlarını kullanarak dağıtılan bir Service Fabric uygulama paketi oluşturur.

### <a name="deploy-service-fabric-cli"></a>Service Fabric CLI dağıtma

Merhaba install.sh betik hello gerekli Service Fabric CLI (sfctl) komutları toodeploy hello uygulama paketi içerir.
Merhaba install.sh betik toodeploy hello uygulamayı çalıştırın.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>Sonraki adımlar

* [Service Fabric CLI ile çalışmaya başlama](service-fabric-cli.md)
