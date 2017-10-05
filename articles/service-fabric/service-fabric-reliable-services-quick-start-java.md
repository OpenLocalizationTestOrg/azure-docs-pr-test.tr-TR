---
title: "Java'da ilk, güvenilir Azure mikro hizmet oluşturma | Microsoft Docs"
description: "Durum bilgisiz ve durum bilgisi olan Hizmetleri ile Microsoft Azure Service Fabric uygulaması oluşturma giriş."
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
ms.openlocfilehash: 1ebabe4844732412e04bab8c277f7ebbc4a5737c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-reliable-services"></a>Reliable Services özelliğini kullanmaya başlayın
> [!div class="op_single_selector"]
> * [Windows üzerinde C#](service-fabric-reliable-services-quick-start.md)
> * [Linux üzerinde Java](service-fabric-reliable-services-quick-start-java.md)
>
>

Bu makalede, Azure Service Fabric Reliable Services temelleri açıklanır ve oluşturma ve Java'da yazılmış basit bir güvenilir hizmet uygulaması dağıtma size yol gösterir. Bu Microsoft Virtual Academy video ayrıca durum bilgisiz güvenilir bir hizmetin nasıl oluşturulacağını gösterir:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965">  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a>Yükleme ve Kurulum
Başlamadan önce makinenizde ayarlanan Service Fabric geliştirme ortamı sahip olduğunuzdan emin olun.
Bunu ayarlamak gerekiyorsa, Git [Mac Başlarken](service-fabric-get-started-mac.md) veya [Linux'ta Başlarken](service-fabric-get-started-linux.md).

## <a name="basic-concepts"></a>Temel kavramlar
Reliable Services ile çalışmaya başlamak için yalnızca birkaç temel kavramları anlamanız gerekir:

* **Hizmet türü**: hizmet uygulamanızın budur. Genişleten yazma sınıf tarafından tanımlanan `StatelessService` ve diğer kod veya bağımlılıkları, bir ad ve sürüm numarası ile birlikte kullanılır.
* **Hizmet örneği adlı**: sınıf türü nesne örneklerini oluşturmak gibi hizmetinizi çalıştırmak için adlandırılmış örnekleri, hizmet türüne ilişkin çok oluşturmak. Hizmeti aslında, yazma, bir hizmet sınıfında nesne örneklemesi örnekleridir.
* **Hizmet ana bilgisayarı**: oluşturduğunuz adlandırılmış hizmet örneklerinin bir konak içinde çalıştırmanız gerekir. Hizmet ana bilgisayarı hizmet örneklerini çalıştırdığı yalnızca bir işlemdir.
* **Hizmet kayıt**: kayıt getirir her şeyi birlikte. Hizmet türü çalıştırmak için Service Fabric çalışma zamanı ile örnekleri oluşturmak Service Fabric izin vermek için bir hizmet ana bilgisayarı kayıtlı olması gerekir.  

## <a name="create-a-stateless-service"></a>Durum bilgisi olmayan bir hizmet oluşturma
Service Fabric uygulaması oluşturmaya başlayın. Linux için Service Fabric SDK'sı bir Yeoman içeren bir durum bilgisiz Service Service Fabric uygulaması için askılamayı sağlamak için oluşturucu. Aşağıdaki Yeoman çalıştırarak komutu:

```bash
$ yo azuresfjava
```

Oluşturmak için yönergeleri izleyin bir **güvenilir durum bilgisiz hizmet**. Bu öğretici için "HelloWorldApplication" uygulama adı ve "HelloWorld" hizmet. Dizinler için sonuç içerir `HelloWorldApplication` ve `HelloWorld`.

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

## <a name="implement-the-service"></a>Uygulama hizmeti
Açık **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**. Bu sınıf, hizmet türünü tanımlar ve herhangi bir kod çalıştırabilirsiniz. Hizmeti API'si kodunuz için iki giriş noktaları sağlar:

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

Bu öğreticide, biz odaklanmak `runAsync()` giriş noktası yöntemi. Hemen kodunuzu çalıştırmaya başlayabileceğiniz budur.

### <a name="runasync"></a>RunAsync
Bir hizmet örneği yerleştirilen ve çalıştırılmaya hazır olduğunda platform bu yöntemi çağırır. Hizmet örneği açıldığında durumsuz bir hizmet için basitçe anlamına gelir. Hizmet örneğinizi kapatılması gerektiğinde koordine etmek için bir iptal belirteci sağlanır. Service Fabric bu hizmet örneği Aç/Kapat döngüsünü birçok kez ömrü hizmeti bir bütün olarak ortaya çıkabilir. Bu da dahil olmak üzere çeşitli nedenlerden kaynaklanabilir:

* Sistem, hizmet örneği için kaynak Dengeleme taşır.
* Kodunuzdaki hataları oluşur.
* Uygulama veya sistem yükseltilir.
* Temel alınan donanım kesinti karşılaşır.

Bu düzenlemesi yönetilen hizmetinizi yüksek oranda kullanılabilir ve düzgün şekilde dengeli tutmak için Service Fabric tarafından.

`runAsync()`zaman uyumlu olarak bloğu değil. Uygulamanıza runAsync devam etmek çalışma zamanı izin vermek için bir CompletableFuture döndürmelidir. İş yükünüzün içinde CompletableFuture yapılmalıdır uzun süre çalışan bir görev uygulamak gerekip gerekmediğini.

#### <a name="cancellation"></a>İptal etme
İş yükünüzün iptaline tarafından sağlanan iptal belirteci bağımsızlıklar işbirlikçi çaba ' dir. Sistem göreviniz (başarılı bir şekilde tamamlandığında, iptal veya hataya göre) taşır önce sona erdirmek bekler. İptal belirteci dikkate için herhangi bir iş bitirip çıkmak önemlidir `runAsync()` sistem iptal istediğinde mümkün olan en kısa sürede. Aşağıdaki örnek, bir iptal olayını işlemek gösterilmiştir:

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace the following sample code with your own logic
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
Hizmet türlerini Service Fabric çalışma zamanı ile kayıtlı olması gerekir. Hizmet türü tanımlanan `ServiceManifest.xml` ve uygulayan hizmet sınıfınızı `StatelessService`. Hizmet kayıt işlemi ana giriş noktası gerçekleştirilir. Bu örnekte işlem ana giriş noktasıdır `HelloWorldServiceHost.java`:

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

## <a name="run-the-application"></a>Uygulamayı çalıştırma

Yeoman yapı iskelesi uygulama oluşturup dağıtın ve uygulamayı kaldırmak için komut dosyaları bash bir gradle komut dosyası içerir. Uygulamayı çalıştırmak için ilk uygulama gradle ile oluşturun:

```bash
$ gradle
```

Bu, Service Fabric CLI kullanarak dağıtılan bir Service Fabric uygulama paketi oluşturur.

### <a name="deploy-with-service-fabric-cli"></a>Service Fabric CLI ile dağıtma

Uygulama paketi dağıtmak için gerekli Service Fabric CLI komutları install.sh komut dosyası içerir. Uygulamayı dağıtmak için install.sh komut dosyasını çalıştırın.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>Sonraki adımlar

* [Service Fabric CLI ile çalışmaya başlama](service-fabric-cli.md)
