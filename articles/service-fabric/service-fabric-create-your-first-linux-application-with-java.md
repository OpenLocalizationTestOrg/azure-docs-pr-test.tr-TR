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
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a><span data-ttu-id="9babd-103">Linux üzerinde ilk Java Service Fabric Reliable Actors uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9babd-103">Create your first Java Service Fabric Reliable Actors application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9babd-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="9babd-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="9babd-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="9babd-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="9babd-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="9babd-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="9babd-107">Bu hızlı başlangıç, bir Linux geliştirme ortamında ilk Azure Service Fabric Java uygulamanızı yalnızca birkaç dakikada oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9babd-107">This quick-start helps you create your first Azure Service Fabric Java application in a Linux development environment in just a few minutes.</span></span>  <span data-ttu-id="9babd-108">İşiniz bittiğinde, hello yerel geliştirme küme üzerinde çalışan basit bir Java tek hizmet uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9babd-108">When you are finished, you'll have a simple Java single-service application running on hello local development cluster.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="9babd-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9babd-109">Prerequisites</span></span>
<span data-ttu-id="9babd-110">Başlamadan önce hello Service Fabric SDK yüklemek, Service Fabric CLI hello ve geliştirme Küme kurulumu, [Linux geliştirme ortamı](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9babd-110">Before you get started, install hello Service Fabric SDK, hello Service Fabric CLI, and setup a development cluster in your [Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="9babd-111">Mac OS X kullanıyorsanız, [Vagrant kullanarak bir sanal makinede Linux geliştirme ortamı ayarlayabilirsiniz](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="9babd-111">If you are using Mac OS X, you can [set up a Linux development environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="9babd-112">Ayrıca tooinstall hello isteyeceksiniz [Service Fabric CLI](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9babd-112">You will also want tooinstall hello [Service Fabric CLI](service-fabric-cli.md).</span></span>

### <a name="install-and-set-up-hello-generators-for-java"></a><span data-ttu-id="9babd-113">Yükleme ve Java için hello oluşturucuları ayarlama</span><span class="sxs-lookup"><span data-stu-id="9babd-113">Install and set up hello generators for Java</span></span>
<span data-ttu-id="9babd-114">Service Fabric, Yeoman şablon oluşturucu kullanarak terminalden Service Fabric Java uygulaması oluşturmanıza yardımcı olacak yapı iskelesi araçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="9babd-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric Java application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="9babd-115">Lütfen makine üzerinde çalışan Java için hello Service Fabric yeoman şablonu oluşturucuyu sahip tooensure hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="9babd-115">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for Java working on your machine.</span></span>
1. <span data-ttu-id="9babd-116">Makinenize nodejs ve NPM yükleme</span><span class="sxs-lookup"><span data-stu-id="9babd-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="9babd-117">NPM’den makinenize [Yeoman](http://yeoman.io/) şablon oluşturucuyu yükleme</span><span class="sxs-lookup"><span data-stu-id="9babd-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="9babd-118">Merhaba Service Fabric Yeo Java uygulama üreteci NPM yükleme</span><span class="sxs-lookup"><span data-stu-id="9babd-118">Install hello Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a><span data-ttu-id="9babd-119">Merhaba uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="9babd-119">Create hello application</span></span>
<span data-ttu-id="9babd-120">Service Fabric uygulaması her hello uygulamanın işlevselliğini aktarma konusunda belirli bir rol ile bir veya daha fazla hizmet içeriyor.</span><span class="sxs-lookup"><span data-stu-id="9babd-120">A Service Fabric application contains one or more services, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="9babd-121">Merhaba son bölümünde yüklü hello Oluşturucu kolay toocreate kılar ilk hizmet ve daha sonra tooadd.</span><span class="sxs-lookup"><span data-stu-id="9babd-121">hello generator you installed in hello last section, makes it easy toocreate your first service and tooadd more later.</span></span>  <span data-ttu-id="9babd-122">Service Fabric Java uygulamalarını Eclipse’e yönelik bir eklentiyi kullanarak da oluşturabilir, derleyebilir ve dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9babd-122">You can also create, build, and deploy Service Fabric Java applications using a plugin for Eclipse.</span></span> <span data-ttu-id="9babd-123">Bkz. [Eclipse kullanarak ilk Java uygulamanızı oluşturma ve dağıtma](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="9babd-123">See [Create and deploy your first Java application using Eclipse](service-fabric-get-started-eclipse.md).</span></span> <span data-ttu-id="9babd-124">Bu Hızlı Başlangıç için depolar ve bir sayaç değeri alan tek bir hizmetle Yeoman toocreate bir uygulama kullanın.</span><span class="sxs-lookup"><span data-stu-id="9babd-124">For this quick start, use Yeoman toocreate an application with a single service that stores and gets a counter value.</span></span>

1. <span data-ttu-id="9babd-125">Bir terminal penceresinde ``yo azuresfjava`` yazın.</span><span class="sxs-lookup"><span data-stu-id="9babd-125">In a terminal, type ``yo azuresfjava``.</span></span>
2. <span data-ttu-id="9babd-126">Uygulamanızı adlandırın.</span><span class="sxs-lookup"><span data-stu-id="9babd-126">Name your application.</span></span>
3. <span data-ttu-id="9babd-127">İlk hizmetiniz Hello türünü seçin ve adlandırın.</span><span class="sxs-lookup"><span data-stu-id="9babd-127">Choose hello type of your first service and name it.</span></span> <span data-ttu-id="9babd-128">Bu öğretici için bir Reliable Actor Hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="9babd-128">For this tutorial, choose a Reliable Actor Service.</span></span> <span data-ttu-id="9babd-129">Diğer türlerdeki Hizmetleri, hello hakkında daha fazla bilgi için bkz [Service Fabric programlama modeline genel bakış](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="9babd-129">For more information about hello other types of services, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
   <span data-ttu-id="9babd-130">![Java için Service Fabric Yeoman oluşturucusu][sf-yeoman]</span><span class="sxs-lookup"><span data-stu-id="9babd-130">![Service Fabric Yeoman generator for Java][sf-yeoman]</span></span>

## <a name="build-hello-application"></a><span data-ttu-id="9babd-131">Merhaba uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="9babd-131">Build hello application</span></span>
<span data-ttu-id="9babd-132">Merhaba Service Fabric Yeoman şablonları içerir bir yapı komut dosyası için [Gradle](https://gradle.org/), hangi toobuild hello hello terminal uygulamasından kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9babd-132">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span>
<span data-ttu-id="9babd-133">Service Fabric Java bağımlılıkları Maven’dan alınır.</span><span class="sxs-lookup"><span data-stu-id="9babd-133">Service Fabric Java dependencies get fetched from Maven.</span></span> <span data-ttu-id="9babd-134">toobuild ve iş hello Service Fabric Java uygulamaları, JDK varsa ve Gradle yüklü tooensure gerekir.</span><span class="sxs-lookup"><span data-stu-id="9babd-134">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK and Gradle installed.</span></span> <span data-ttu-id="9babd-135">Henüz yüklü değilse, hello çalıştırabilirsiniz aşağıdaki tooinstall JDK(openjdk-8-jdk) ve Gradle -</span><span class="sxs-lookup"><span data-stu-id="9babd-135">If not yet installed, you can run hello following tooinstall JDK(openjdk-8-jdk) and Gradle -</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

<span data-ttu-id="9babd-136">Merhaba aşağıdaki çalıştırma toobuild ve paket hello uygulaması:</span><span class="sxs-lookup"><span data-stu-id="9babd-136">toobuild and package hello application, run hello following:</span></span>

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-hello-application"></a><span data-ttu-id="9babd-137">Merhaba uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="9babd-137">Deploy hello application</span></span>
<span data-ttu-id="9babd-138">Merhaba uygulama oluşturulduktan sonra toohello yerel küme dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9babd-138">Once hello application is built, you can deploy it toohello local cluster.</span></span>

1. <span data-ttu-id="9babd-139">Toohello yerel Service Fabric kümesi bağlayın.</span><span class="sxs-lookup"><span data-stu-id="9babd-139">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="9babd-140">Merhaba şablonu toocopy Merhaba uygulaması toohello kümenin görüntü deposu paketini, hello uygulama türünü kaydetme ve hello uygulama örneğini oluşturmak sağlanan hello yükleme betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9babd-140">Run hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="9babd-141">Dağıtma yerleşik hello aynı başka bir Service Fabric uygulama hello uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="9babd-141">Deploying hello built application is hello same as any other Service Fabric application.</span></span> <span data-ttu-id="9babd-142">Merhaba belgelerine bakın [bir Service Fabric uygulaması hello Service Fabric CLI ile yönetme](service-fabric-application-lifecycle-sfctl.md) ayrıntılı yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="9babd-142">See hello documentation on [managing a Service Fabric application with hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="9babd-143">Parametreleri toothese komutları hello oluşturulan bildirimleri hello uygulama paketi içinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="9babd-143">Parameters toothese commands can be found in hello generated manifests inside hello application package.</span></span>

<span data-ttu-id="9babd-144">Merhaba uygulama dağıtıldıktan sonra bir tarayıcı açın ve gidin [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) adresindeki [http://localhost: 19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="9babd-144">Once hello application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span>
<span data-ttu-id="9babd-145">Ardından, hello genişletin **uygulamaları** düğümü ve olduğunu şimdi uygulama türü için bir giriş ve hello bu türünün ilk örneği için başka bir not.</span><span class="sxs-lookup"><span data-stu-id="9babd-145">Then, expand hello **Applications** node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

## <a name="start-hello-test-client-and-perform-a-failover"></a><span data-ttu-id="9babd-146">Merhaba test istemcisi başlatın ve bir yük devretme gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="9babd-146">Start hello test client and perform a failover</span></span>
<span data-ttu-id="9babd-147">Aktör bunu kendi başına hiçbir şey, başka bir hizmet veya istemci toosend gereksinim duydukları bunları iletileri.</span><span class="sxs-lookup"><span data-stu-id="9babd-147">Actors do not do anything on their own, they require another service or client toosend them messages.</span></span> <span data-ttu-id="9babd-148">Merhaba aktör şablon toointeract hello aktör hizmeti ile kullanabileceğiniz bir basit bir sınama betiği içerir.</span><span class="sxs-lookup"><span data-stu-id="9babd-148">hello actor template includes a simple test script that you can use toointeract with hello actor service.</span></span>

1. <span data-ttu-id="9babd-149">Merhaba izleme yardımcı programı toosee hello çıkış hello aktör hizmeti kullanan hello komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9babd-149">Run hello script using hello watch utility toosee hello output of hello actor service.</span></span>  <span data-ttu-id="9babd-150">Merhaba test komut dosyasını çağıran hello `setCountAsync()` hello aktör tooincrement bir sayaç yöntemini çağıran hello `getCountAsync()` yöntemi hello aktör tooget hello yeni sayaç değeri ve toohello konsol değeri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9babd-150">hello test script calls hello `setCountAsync()` method on hello actor tooincrement a counter, calls hello `getCountAsync()` method on hello actor tooget hello new counter value, and displays that value toohello console.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. <span data-ttu-id="9babd-151">Service Fabric Explorer'da hello düğümü barındırma hello için birincil kopya hello aktör hizmeti bulun.</span><span class="sxs-lookup"><span data-stu-id="9babd-151">In Service Fabric Explorer, locate hello node hosting hello primary replica for hello actor service.</span></span> <span data-ttu-id="9babd-152">Merhaba ekran görüntüsünde, onu 3 düğümdür.</span><span class="sxs-lookup"><span data-stu-id="9babd-152">In hello screenshot below, it is node 3.</span></span> <span data-ttu-id="9babd-153">Merhaba birincil hizmet çoğaltma tanıtıcıları okuma ve yazma işlemleri.</span><span class="sxs-lookup"><span data-stu-id="9babd-153">hello primary service replica handles read and write operations.</span></span>  <span data-ttu-id="9babd-154">Hizmet durumu değişiklikleri sonra toohello ikincil çoğaltmalar, 0 ve 1. aşağıda gösterilen hello ekran düğümlerde çalışan çıkışı çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="9babd-154">Changes in service state are then replicated out toohello secondary replicas, running on nodes 0 and 1 in hello screen shot below.</span></span>

    ![Service Fabric Explorer'da bulma hello birincil çoğaltma][sfx-primary]

3. <span data-ttu-id="9babd-156">İçinde **düğümleri**, hello önceki adımda bulunan sonra seçin hello düğümünü tıklatın **devre dışı bırak (yeniden)** hello Eylemler menüsünden.</span><span class="sxs-lookup"><span data-stu-id="9babd-156">In **Nodes**, click hello node you found in hello previous step, then select **Deactivate (restart)** from hello Actions menu.</span></span> <span data-ttu-id="9babd-157">Bu eylemin hello birincil hizmet çoğaltması çalıştıran hello düğümü yeniden başlatır ve hello ikincil çoğaltmaların başka bir düğüm üzerinde çalışan bir yük devretme tooone zorlar.</span><span class="sxs-lookup"><span data-stu-id="9babd-157">This action restarts hello node running hello primary service replica and forces a failover tooone of hello secondary replicas running on another node.</span></span>  <span data-ttu-id="9babd-158">Bu ikincil çoğaltma yükseltilen tooprimary olduğundan, başka bir ikincil çoğaltma farklı bir düğümde oluşturulur ve tootake okuma/yazma işlemleri hello birincil çoğaltma başlar.</span><span class="sxs-lookup"><span data-stu-id="9babd-158">That secondary replica is promoted tooprimary, another secondary replica is created on a different node, and hello primary replica begins tootake read/write operations.</span></span> <span data-ttu-id="9babd-159">Merhaba düğümü yeniden başlatılırken hello çıktısını hello test istemcisi ve hello sayaç tooincrement hello yük devretme rağmen devam Not izleyin.</span><span class="sxs-lookup"><span data-stu-id="9babd-159">As hello node restarts, watch hello output from hello test client and note that hello counter continues tooincrement despite hello failover.</span></span>

## <a name="remove-hello-application"></a><span data-ttu-id="9babd-160">Merhaba uygulamayı kaldırma</span><span class="sxs-lookup"><span data-stu-id="9babd-160">Remove hello application</span></span>
<span data-ttu-id="9babd-161">Merhaba şablon toodelete hello uygulama örneği içinde sağlanan hello kaldırma komut dosyası kullanmak, hello uygulama paketi kaydı ve hello uygulama paketi hello kümenin görüntü deposundan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="9babd-161">Use hello uninstall script provided in hello template toodelete hello application instance, unregister hello application package, and remove hello application package from hello cluster's image store.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="9babd-162">Service Fabric Explorer'da hello uygulama ve uygulama türü artık hello göründüğünü görmek **uygulamaları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="9babd-162">In Service Fabric explorer you see that hello application and application type no longer appear in hello **Applications** node.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="9babd-163">Maven'da Service Fabric Java kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="9babd-163">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="9babd-164">Maven’da barındırılan Service Fabric Java kitaplıkları.</span><span class="sxs-lookup"><span data-stu-id="9babd-164">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="9babd-165">Hello hello bağımlılıklar ekleyebilirsiniz ``pom.xml`` veya ``build.gradle`` projeleri toouse Service Fabric Java kitaplıklarından birini **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="9babd-165">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="9babd-166">Aktörler</span><span class="sxs-lookup"><span data-stu-id="9babd-166">Actors</span></span>

<span data-ttu-id="9babd-167">Uygulamanız için Service Fabric Güvenilir Aktör desteği.</span><span class="sxs-lookup"><span data-stu-id="9babd-167">Service Fabric Reliable Actor support for your application.</span></span>

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

### <a name="services"></a><span data-ttu-id="9babd-168">Hizmetler</span><span class="sxs-lookup"><span data-stu-id="9babd-168">Services</span></span>

<span data-ttu-id="9babd-169">Uygulamanız için Service Fabric Durum Bilgisi Olmayan Hizmet desteği.</span><span class="sxs-lookup"><span data-stu-id="9babd-169">Service Fabric Stateless Service support for your application.</span></span>

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

### <a name="others"></a><span data-ttu-id="9babd-170">Diğer</span><span class="sxs-lookup"><span data-stu-id="9babd-170">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="9babd-171">Aktarım</span><span class="sxs-lookup"><span data-stu-id="9babd-171">Transport</span></span>

<span data-ttu-id="9babd-172">Service Fabric Java uygulaması için Aktarım katmanı desteği.</span><span class="sxs-lookup"><span data-stu-id="9babd-172">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="9babd-173">İhtiyacınız olmayan tooexplicitly, bu bağımlılık tooyour güvenilir aktör ya da hizmet uygulamaları hello aktarım katmanında program sürece ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9babd-173">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

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

#### <a name="fabric-support"></a><span data-ttu-id="9babd-174">Fabric desteği</span><span class="sxs-lookup"><span data-stu-id="9babd-174">Fabric support</span></span>

<span data-ttu-id="9babd-175">Sistem düzeyinde toonative Service Fabric çalışma zamanı ettiği Service Fabric desteği.</span><span class="sxs-lookup"><span data-stu-id="9babd-175">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="9babd-176">İhtiyacınız olmayan tooexplicitly eklemek bu bağımlılık tooyour güvenilir aktör veya hizmet uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="9babd-176">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="9babd-177">Bu otomatik olarak Maven alınan, eklediğiniz zaman yukarıdaki başka bir bağımlılık hello.</span><span class="sxs-lookup"><span data-stu-id="9babd-177">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

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

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a><span data-ttu-id="9babd-178">Maven ile kullanılan eski Service Fabric Java uygulamaları toobe geçirme</span><span class="sxs-lookup"><span data-stu-id="9babd-178">Migrating old Service Fabric Java applications toobe used with Maven</span></span>
<span data-ttu-id="9babd-179">Service Fabric Java kitaplıkları yakın zamanda Service Fabric Java SDK tooMaven depodan taşınmış.</span><span class="sxs-lookup"><span data-stu-id="9babd-179">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK tooMaven repository.</span></span> <span data-ttu-id="9babd-180">Yeoman veya Eclipse, kullanarak Oluştur hello yeni uygulamalar üretir (Maven ile mümkün toowork olacaktır) en son güncelleştirilen projeleri, ancak varolan Service Fabric durum bilgisiz veya hello hizmet kullanmakta olduğunuz aktör Java uygulamalarını güncelleştirebilirsiniz Doku Java SDK'sı daha önce toouse hello Service Fabric Java Maven bağımlılıklardan.</span><span class="sxs-lookup"><span data-stu-id="9babd-180">While hello new applications you generate using Yeoman or Eclipse, will generate latest updated projects (which will be able toowork with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using hello Service Fabric Java SDK earlier, toouse hello Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="9babd-181">Lütfen belirtilen hello adımları [burada](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure eski uygulamanızı Maven ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="9babd-181">Please follow hello steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure your older application works with Maven.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9babd-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9babd-182">Next steps</span></span>

* [<span data-ttu-id="9babd-183">Linux’ta Eclipse kullanarak ilk Service Fabric Java uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9babd-183">Create your first Service Fabric Java application on Linux using Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="9babd-184">Reliable Actors hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="9babd-184">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="9babd-185">Merhaba Service Fabric CLI kullanarak Service Fabric kümeleri ile etkileşim</span><span class="sxs-lookup"><span data-stu-id="9babd-185">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="9babd-186">[Service Fabric destek seçenekleri](service-fabric-support.md) hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="9babd-186">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="9babd-187">Service Fabric CLI ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="9babd-187">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
