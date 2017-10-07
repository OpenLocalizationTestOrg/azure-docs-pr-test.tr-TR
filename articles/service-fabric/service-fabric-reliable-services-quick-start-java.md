---
title: "aaaCreate, ilk güvenilir Azure mikro hizmet Java | Microsoft Docs"
description: "Giriş toocreating durum bilgisiz ve durum bilgisi olan hizmetler ile Microsoft Azure Service Fabric uygulaması."
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 577d96591797bbfe6be5c1094426b5f1435cca0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a>Reliable Services özelliğini kullanmaya başlayın
> [!div class="op_single_selector"]
> * [Windows üzerinde C#](service-fabric-reliable-services-quick-start.md)
> * [Linux üzerinde Java](service-fabric-reliable-services-quick-start-java.md)
>
>

Bu makalede, Azure Service Fabric Reliable Services hello temelleri açıklanır ve oluşturma ve Java'da yazılmış basit bir güvenilir hizmet uygulaması dağıtma size yol gösterir. Bu Microsoft Virtual Academy video de nasıl gösterir toocreate durum bilgisiz güvenilir hizmet:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965">  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a>Yükleme ve Kurulum
Başlamadan önce makinenizde ayarlanan hello Service Fabric geliştirme ortamı sahip olduğunuzdan emin olun.
Tooset ihtiyacınız varsa bunun Git çok[Mac Başlarken](service-fabric-get-started-mac.md) veya [Linux'ta Başlarken](service-fabric-get-started-linux.md).

## <a name="basic-concepts"></a>Temel kavramlar
Reliable Services ile size yalnızca çalışmaya tooget birkaç temel kavramları toounderstand gerekir:

* **Hizmet türü**: hizmet uygulamanızın budur. Genişleten yazma hello sınıf tarafından tanımlanan `StatelessService` ve diğer kod veya bağımlılıkları, bir ad ve sürüm numarası ile birlikte kullanılır.
* **Hizmet örneği adlı**: toorun sınıf türü nesne örneklerini oluşturmak gibi hizmetiniz, adlandırılmış örnekleri, hizmet türüne ilişkin çok oluşturmak. Hizmeti aslında, yazma, bir hizmet sınıfında nesne örneklemesi örnekleridir.
* **Hizmet ana bilgisayarı**: gerek toorun bir ana bilgisayar içinde oluşturduğunuz hizmet örnekleri adlı hello. Merhaba hizmet ana bilgisayarı hizmet örneklerini çalıştırdığı yalnızca bir işlemdir.
* **Hizmet kayıt**: kayıt getirir her şeyi birlikte. Merhaba hizmet türü kaydedilmelidir Service Fabric hello ile bir hizmeti çalışma zamanı ana bilgisayar tooallow Service Fabric toocreate örnekleri toorun.  

## <a name="create-a-stateless-service"></a>Durum bilgisi olmayan bir hizmet oluşturma
Service Fabric uygulaması oluşturmaya başlayın. Merhaba Linux için Service Fabric SDK içeren bir Yeoman durum bilgisiz hizmeti ile bir Service Fabric uygulaması için oluşturucu tooprovide hello askılamayı. Merhaba çalıştırarak Yeoman komutu:

```bash
$ yo azuresfjava
```

Merhaba yönergeleri toocreate izleyin bir **güvenilir durum bilgisiz hizmet**. Bu öğretici için ad Merhaba uygulaması "HelloWorldApplication" Merhaba "HelloWorld" service ve. Merhaba sonuç içerir hello için dizinler `HelloWorldApplication` ve `HelloWorld`.

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-hello-service"></a>Merhaba hizmet ekleme
Açık **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**. Bu sınıf hello hizmet türünü tanımlar ve herhangi bir kod çalıştırabilirsiniz. Merhaba hizmeti API'si kodunuz için iki giriş noktaları sağlar:

* Adlı bir uçlu giriş noktası yöntemi `runAsync()`, burada uzun süre çalışan işlem iş yükleri de dahil olmak üzere tüm iş yükleri yürütme başlayabilirsiniz.

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* Seçim içinde iletişim yığını burada takın iletişimi giriş noktası. Kullanıcılar ve diğer hizmetler isteklerini almak başlayabileceğiniz budur.

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

Bu öğreticide, biz hello üzerinde odaklanmak `runAsync()` giriş noktası yöntemi. Hemen kodunuzu çalıştırmaya başlayabileceğiniz budur.

### <a name="runasync"></a>RunAsync
bir hizmet örneği yerleştirilen ve hazır tooexecute olduğunda hello platform bu yöntemi çağırır. Merhaba hizmet örneği açıldığında durumsuz bir hizmet için basitçe anlamına gelir. Hizmet örneğinizi kapalı toobe gerektiğinde bir iptal belirteci toocoordinate sağlanır. Service Fabric bu hizmet örneği Aç/Kapat döngüsünü hello hizmetinin birçok kez hello ömrü boyunca bir bütün olarak ortaya çıkabilir. Bu da dahil olmak üzere çeşitli nedenlerden kaynaklanabilir:

* Merhaba sistem, hizmet örneği için kaynak Dengeleme taşır.
* Kodunuzdaki hataları oluşur.
* Merhaba uygulama veya sistem yükseltilir.
* Merhaba temel alınan donanım kesinti karşılaşır.

Bu düzenlemesi Service Fabric tookeep tarafından yönetilen hizmetinizi yüksek oranda kullanılabilir ve düzgün şekilde dengeli.

`runAsync()`zaman uyumlu olarak bloğu değil. Uygulamanıza runAsync CompletableFuture tooallow hello çalışma zamanı toocontinue döndürmelidir. İş yükünüzün tooimplement içinde yapılmalıdır uzun süre çalışan bir görev gerekiyorsa CompletableFuture hello.

#### <a name="cancellation"></a>İptal etme
İş yükünüzün iptaline iptal belirteci sağlanan hello tarafından düzenlenmiş işbirlikçi çaba ' dir. Merhaba sistem bekler, görev tooend için (başarılı bir şekilde tamamlandığında, iptal veya hataya göre) taşır önce. Herhangi bir iş ve çıkış önemli toohonor hello iptal belirteci, bitiş olduğu `runAsync()` hello sistem iptal istediğinde mümkün olan en kısa sürede. Merhaba aşağıdaki örnekte gösterilmiştir nasıl toohandle iptal olay:

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace hello following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a>Hizmet kayıt
Hizmet türlerini hello Service Fabric çalışma zamanı ile kayıtlı olması gerekir. Merhaba hizmet türü hello tanımlanan `ServiceManifest.xml` ve uygulayan hizmet sınıfınızı `StatelessService`. Hizmet kayıt hello işlem ana giriş noktası gerçekleştirilir. Bu örnekte, ana giriş noktası işlem hello `HelloWorldServiceHost.java`:

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-hello-application"></a>Merhaba uygulamayı çalıştırın

Merhaba Yeoman yapı iskelesi, gradle betik toobuild hello uygulama ve bash betikleri toodeploy ve Kaldır uygulamayı içerir. toorun hello uygulama ilk yapı hello gradle ile:

```bash
$ gradle
```

Bu, Service Fabric CLI kullanarak dağıtılan bir Service Fabric uygulama paketi oluşturur.

### <a name="deploy-with-service-fabric-cli"></a>Service Fabric CLI ile dağıtma

Merhaba install.sh betik hello gerekli Service Fabric CLI komutları toodeploy hello uygulama paketi içerir. İnstall.sh betik toodeploy hello uygulamayı çalıştırın.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>Sonraki adımlar

* [Service Fabric CLI ile çalışmaya başlama](service-fabric-cli.md)
