---
title: "Azure Service Fabric güvenilir aktörler Java uygulaması Linux'ta aaaCreate | Microsoft Docs"
description: "Bilgi nasıl toocreate beş dakika içinde Java Service Fabric bir güvenilir aktörler uygulama ve dağıtın."
services: service-fabric
documentationcenter: java
author: rwike77
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: ryanwi
ms.openlocfilehash: 11496b767811c89969c65d1682d843448eb6a922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a>Linux üzerinde ilk Java Service Fabric Reliable Actors uygulamanızı oluşturma
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

Bu hızlı başlangıç, bir Linux geliştirme ortamında ilk Azure Service Fabric Java uygulamanızı yalnızca birkaç dakikada oluşturmanıza yardımcı olur.  İşiniz bittiğinde, hello yerel geliştirme küme üzerinde çalışan basit bir Java tek hizmet uygulaması gerekir.  

## <a name="prerequisites"></a>Ön koşullar
Başlamadan önce hello Service Fabric SDK yüklemek, Service Fabric CLI hello ve geliştirme Küme kurulumu, [Linux geliştirme ortamı](service-fabric-get-started-linux.md). Mac OS X kullanıyorsanız, [Vagrant kullanarak bir sanal makinede Linux geliştirme ortamı ayarlayabilirsiniz](service-fabric-get-started-mac.md).

Ayrıca tooinstall hello isteyeceksiniz [Service Fabric CLI](service-fabric-cli.md).

### <a name="install-and-set-up-hello-generators-for-java"></a>Yükleme ve Java için hello oluşturucuları ayarlama
Service Fabric, Yeoman şablon oluşturucu kullanarak terminalden Service Fabric Java uygulaması oluşturmanıza yardımcı olacak yapı iskelesi araçları sağlar. Lütfen makine üzerinde çalışan Java için hello Service Fabric yeoman şablonu oluşturucuyu sahip tooensure hello adımları izleyin.
1. Makinenize nodejs ve NPM yükleme

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. NPM’den makinenize [Yeoman](http://yeoman.io/) şablon oluşturucuyu yükleme

  ```bash
  sudo npm install -g yo
  ```
3. Merhaba Service Fabric Yeo Java uygulama üreteci NPM yükleme

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a>Merhaba uygulaması oluşturma
Service Fabric uygulaması her hello uygulamanın işlevselliğini aktarma konusunda belirli bir rol ile bir veya daha fazla hizmet içeriyor. Merhaba son bölümünde yüklü hello Oluşturucu kolay toocreate kılar ilk hizmet ve daha sonra tooadd.  Service Fabric Java uygulamalarını Eclipse’e yönelik bir eklentiyi kullanarak da oluşturabilir, derleyebilir ve dağıtabilirsiniz. Bkz. [Eclipse kullanarak ilk Java uygulamanızı oluşturma ve dağıtma](service-fabric-get-started-eclipse.md). Bu Hızlı Başlangıç için depolar ve bir sayaç değeri alan tek bir hizmetle Yeoman toocreate bir uygulama kullanın.

1. Bir terminal penceresinde ``yo azuresfjava`` yazın.
2. Uygulamanızı adlandırın.
3. İlk hizmetiniz Hello türünü seçin ve adlandırın. Bu öğretici için bir Reliable Actor Hizmeti seçin. Diğer türlerdeki Hizmetleri, hello hakkında daha fazla bilgi için bkz [Service Fabric programlama modeline genel bakış](service-fabric-choose-framework.md).
   ![Java için Service Fabric Yeoman oluşturucusu][sf-yeoman]

## <a name="build-hello-application"></a>Merhaba uygulaması oluşturma
Merhaba Service Fabric Yeoman şablonları içerir bir yapı komut dosyası için [Gradle](https://gradle.org/), hangi toobuild hello hello terminal uygulamasından kullanabilirsiniz.
Service Fabric Java bağımlılıkları Maven’dan alınır. toobuild ve iş hello Service Fabric Java uygulamaları, JDK varsa ve Gradle yüklü tooensure gerekir. Henüz yüklü değilse, hello çalıştırabilirsiniz aşağıdaki tooinstall JDK(openjdk-8-jdk) ve Gradle -

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

Merhaba aşağıdaki çalıştırma toobuild ve paket hello uygulaması:

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-hello-application"></a>Merhaba uygulaması dağıtma
Merhaba uygulama oluşturulduktan sonra toohello yerel küme dağıtabilirsiniz.

1. Toohello yerel Service Fabric kümesi bağlayın.

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. Merhaba şablonu toocopy Merhaba uygulaması toohello kümenin görüntü deposu paketini, hello uygulama türünü kaydetme ve hello uygulama örneğini oluşturmak sağlanan hello yükleme betiğini çalıştırın.

    ```bash
    ./install.sh
    ```

Dağıtma yerleşik hello aynı başka bir Service Fabric uygulama hello uygulamasıdır. Merhaba belgelerine bakın [bir Service Fabric uygulaması hello Service Fabric CLI ile yönetme](service-fabric-application-lifecycle-sfctl.md) ayrıntılı yönergeler için.

Parametreleri toothese komutları hello oluşturulan bildirimleri hello uygulama paketi içinde bulunabilir.

Merhaba uygulama dağıtıldıktan sonra bir tarayıcı açın ve gidin [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) adresindeki [http://localhost: 19080/Explorer](http://localhost:19080/Explorer).
Ardından, hello genişletin **uygulamaları** düğümü ve olduğunu şimdi uygulama türü için bir giriş ve hello bu türünün ilk örneği için başka bir not.

## <a name="start-hello-test-client-and-perform-a-failover"></a>Merhaba test istemcisi başlatın ve bir yük devretme gerçekleştirin.
Aktör bunu kendi başına hiçbir şey, başka bir hizmet veya istemci toosend gereksinim duydukları bunları iletileri. Merhaba aktör şablon toointeract hello aktör hizmeti ile kullanabileceğiniz bir basit bir sınama betiği içerir.

1. Merhaba izleme yardımcı programı toosee hello çıkış hello aktör hizmeti kullanan hello komut dosyasını çalıştırın.  Merhaba test komut dosyasını çağıran hello `setCountAsync()` hello aktör tooincrement bir sayaç yöntemini çağıran hello `getCountAsync()` yöntemi hello aktör tooget hello yeni sayaç değeri ve toohello konsol değeri görüntüler.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. Service Fabric Explorer'da hello düğümü barındırma hello için birincil kopya hello aktör hizmeti bulun. Merhaba ekran görüntüsünde, onu 3 düğümdür. Merhaba birincil hizmet çoğaltma tanıtıcıları okuma ve yazma işlemleri.  Hizmet durumu değişiklikleri sonra toohello ikincil çoğaltmalar, 0 ve 1. aşağıda gösterilen hello ekran düğümlerde çalışan çıkışı çoğaltılır.

    ![Service Fabric Explorer'da bulma hello birincil çoğaltma][sfx-primary]

3. İçinde **düğümleri**, hello önceki adımda bulunan sonra seçin hello düğümünü tıklatın **devre dışı bırak (yeniden)** hello Eylemler menüsünden. Bu eylemin hello birincil hizmet çoğaltması çalıştıran hello düğümü yeniden başlatır ve hello ikincil çoğaltmaların başka bir düğüm üzerinde çalışan bir yük devretme tooone zorlar.  Bu ikincil çoğaltma yükseltilen tooprimary olduğundan, başka bir ikincil çoğaltma farklı bir düğümde oluşturulur ve tootake okuma/yazma işlemleri hello birincil çoğaltma başlar. Merhaba düğümü yeniden başlatılırken hello çıktısını hello test istemcisi ve hello sayaç tooincrement hello yük devretme rağmen devam Not izleyin.

## <a name="remove-hello-application"></a>Merhaba uygulamayı kaldırma
Merhaba şablon toodelete hello uygulama örneği içinde sağlanan hello kaldırma komut dosyası kullanmak, hello uygulama paketi kaydı ve hello uygulama paketi hello kümenin görüntü deposundan kaldırın.

```bash
./uninstall.sh
```

Service Fabric Explorer'da hello uygulama ve uygulama türü artık hello göründüğünü görmek **uygulamaları** düğümü.

## <a name="service-fabric-java-libraries-on-maven"></a>Maven'da Service Fabric Java kitaplıkları
Maven’da barındırılan Service Fabric Java kitaplıkları. Hello hello bağımlılıklar ekleyebilirsiniz ``pom.xml`` veya ``build.gradle`` projeleri toouse Service Fabric Java kitaplıklarından birini **mavenCentral**.

### <a name="actors"></a>Aktörler

Uygulamanız için Service Fabric Güvenilir Aktör desteği.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a>Hizmetler

Uygulamanız için Service Fabric Durum Bilgisi Olmayan Hizmet desteği.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a>Diğer
#### <a name="transport"></a>Aktarım

Service Fabric Java uygulaması için Aktarım katmanı desteği. İhtiyacınız olmayan tooexplicitly, bu bağımlılık tooyour güvenilir aktör ya da hizmet uygulamaları hello aktarım katmanında program sürece ekleyin.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a>Fabric desteği

Sistem düzeyinde toonative Service Fabric çalışma zamanı ettiği Service Fabric desteği. İhtiyacınız olmayan tooexplicitly eklemek bu bağımlılık tooyour güvenilir aktör veya hizmet uygulamaları. Bu otomatik olarak Maven alınan, eklediğiniz zaman yukarıdaki başka bir bağımlılık hello.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a>Maven ile kullanılan eski Service Fabric Java uygulamaları toobe geçirme
Service Fabric Java kitaplıkları yakın zamanda Service Fabric Java SDK tooMaven depodan taşınmış. Yeoman veya Eclipse, kullanarak Oluştur hello yeni uygulamalar üretir (Maven ile mümkün toowork olacaktır) en son güncelleştirilen projeleri, ancak varolan Service Fabric durum bilgisiz veya hello hizmet kullanmakta olduğunuz aktör Java uygulamalarını güncelleştirebilirsiniz Doku Java SDK'sı daha önce toouse hello Service Fabric Java Maven bağımlılıklardan. Lütfen belirtilen hello adımları [burada](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure eski uygulamanızı Maven ile çalışır.

## <a name="next-steps"></a>Sonraki adımlar

* [Linux’ta Eclipse kullanarak ilk Service Fabric Java uygulamanızı oluşturma](service-fabric-get-started-eclipse.md)
* [Reliable Actors hakkında daha fazla bilgi edinin](service-fabric-reliable-actors-introduction.md)
* [Merhaba Service Fabric CLI kullanarak Service Fabric kümeleri ile etkileşim](service-fabric-cli.md)
* [Service Fabric destek seçenekleri](service-fabric-support.md) hakkında bilgi edinin
* [Service Fabric CLI ile çalışmaya başlama](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
