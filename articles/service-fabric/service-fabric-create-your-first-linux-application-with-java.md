---
title: "Linux üzerinde Azure Service Fabric reliable actors Java uygulaması oluşturma | Microsoft Docs"
description: "Beş dakika içinde Java Service Fabric reliable actors uygulaması oluşturmayı ve dağıtmayı öğrenin."
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
ms.openlocfilehash: baf948587ede31fe3d5b4f6f0981269b4cfe4d3d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a><span data-ttu-id="e6c9d-103">Linux üzerinde ilk Java Service Fabric Reliable Actors uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6c9d-103">Create your first Java Service Fabric Reliable Actors application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e6c9d-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="e6c9d-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="e6c9d-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="e6c9d-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="e6c9d-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="e6c9d-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="e6c9d-107">Bu hızlı başlangıç, bir Linux geliştirme ortamında ilk Azure Service Fabric Java uygulamanızı yalnızca birkaç dakikada oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-107">This quick-start helps you create your first Azure Service Fabric Java application in a Linux development environment in just a few minutes.</span></span>  <span data-ttu-id="e6c9d-108">İşlemi tamamladığınızda, yerel geliştirme kümesinde çalışan basit bir Java tek hizmet uygulamanız olacak.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-108">When you are finished, you'll have a simple Java single-service application running on the local development cluster.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="e6c9d-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e6c9d-109">Prerequisites</span></span>
<span data-ttu-id="e6c9d-110">Başlamadan önce Service Fabric SDK’sı ile Service Fabric CLI aracını yükleyin ve [Linux geliştirme ortamınızda](service-fabric-get-started-linux.md) bir geliştirme kümesi kurun.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-110">Before you get started, install the Service Fabric SDK, the Service Fabric CLI, and setup a development cluster in your [Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="e6c9d-111">Mac OS X kullanıyorsanız, [Vagrant kullanarak bir sanal makinede Linux geliştirme ortamı ayarlayabilirsiniz](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="e6c9d-111">If you are using Mac OS X, you can [set up a Linux development environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="e6c9d-112">[Service Fabric CLI](service-fabric-cli.md)’yı de yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-112">You will also want to install the [Service Fabric CLI](service-fabric-cli.md).</span></span>

### <a name="install-and-set-up-the-generators-for-java"></a><span data-ttu-id="e6c9d-113">Java için oluşturucuları yükleme ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="e6c9d-113">Install and set up the generators for Java</span></span>
<span data-ttu-id="e6c9d-114">Service Fabric, Yeoman şablon oluşturucu kullanarak terminalden Service Fabric Java uygulaması oluşturmanıza yardımcı olacak yapı iskelesi araçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric Java application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="e6c9d-115">Lütfen makinenizde çalışan bir Java için Service Fabric yeoman şablon oluşturucu olduğundan emin olmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-115">Please follow the steps below to ensure you have the Service Fabric yeoman template generator for Java working on your machine.</span></span>
1. <span data-ttu-id="e6c9d-116">Makinenize nodejs ve NPM yükleme</span><span class="sxs-lookup"><span data-stu-id="e6c9d-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="e6c9d-117">NPM’den makinenize [Yeoman](http://yeoman.io/) şablon oluşturucuyu yükleme</span><span class="sxs-lookup"><span data-stu-id="e6c9d-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="e6c9d-118">NPM’den Service Fabric Yeo Java uygulama oluşturucuyu yükleme</span><span class="sxs-lookup"><span data-stu-id="e6c9d-118">Install the Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-the-application"></a><span data-ttu-id="e6c9d-119">Uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6c9d-119">Create the application</span></span>
<span data-ttu-id="e6c9d-120">Service Fabric uygulaması bir veya birden çok hizmet içerir ve bu hizmetlerin her biri, uygulamanın işlevselliğini sunma konusunda belirli bir role sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-120">A Service Fabric application contains one or more services, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="e6c9d-121">Son bölümde yüklediğiniz oluşturucu, ilk hizmetinizi oluşturmayı ve daha sonra hizmet eklemeyi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-121">The generator you installed in the last section, makes it easy to create your first service and to add more later.</span></span>  <span data-ttu-id="e6c9d-122">Service Fabric Java uygulamalarını Eclipse’e yönelik bir eklentiyi kullanarak da oluşturabilir, derleyebilir ve dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-122">You can also create, build, and deploy Service Fabric Java applications using a plugin for Eclipse.</span></span> <span data-ttu-id="e6c9d-123">Bkz. [Eclipse kullanarak ilk Java uygulamanızı oluşturma ve dağıtma](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="e6c9d-123">See [Create and deploy your first Java application using Eclipse](service-fabric-get-started-eclipse.md).</span></span> <span data-ttu-id="e6c9d-124">Bu hızlı başlangıç için bir sayaç değerini alan ve depolayan tek bir hizmete sahip bir uygulama oluşturmak üzere Yeoman’ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-124">For this quick start, use Yeoman to create an application with a single service that stores and gets a counter value.</span></span>

1. <span data-ttu-id="e6c9d-125">Bir terminal penceresinde ``yo azuresfjava`` yazın.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-125">In a terminal, type ``yo azuresfjava``.</span></span>
2. <span data-ttu-id="e6c9d-126">Uygulamanızı adlandırın.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-126">Name your application.</span></span>
3. <span data-ttu-id="e6c9d-127">Birinci hizmetinizin türünü seçin ve adlandırın.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-127">Choose the type of your first service and name it.</span></span> <span data-ttu-id="e6c9d-128">Bu öğretici için bir Reliable Actor Hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-128">For this tutorial, choose a Reliable Actor Service.</span></span> <span data-ttu-id="e6c9d-129">Diğer hizmet türleri hakkında daha fazla bilgi edinmek için bkz. [Service Fabric programlama modeline genel bakış](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="e6c9d-129">For more information about the other types of services, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
   <span data-ttu-id="e6c9d-130">![Java için Service Fabric Yeoman oluşturucusu][sf-yeoman]</span><span class="sxs-lookup"><span data-stu-id="e6c9d-130">![Service Fabric Yeoman generator for Java][sf-yeoman]</span></span>

## <a name="build-the-application"></a><span data-ttu-id="e6c9d-131">Uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6c9d-131">Build the application</span></span>
<span data-ttu-id="e6c9d-132">Service Fabric Yeoman şablonları, uygulamayı terminalden oluşturmak için kullanabileceğiniz bir [Gradle](https://gradle.org/) derleme betiği içerir.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-132">The Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use to build the application from the terminal.</span></span>
<span data-ttu-id="e6c9d-133">Service Fabric Java bağımlılıkları Maven’dan alınır.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-133">Service Fabric Java dependencies get fetched from Maven.</span></span> <span data-ttu-id="e6c9d-134">Service Fabric Java uygulamalarını oluşturmak ve çalışmak için JDK ve Gradle’ın yüklü olduğundan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-134">To build and work on the Service Fabric Java applications, you need to ensure that you have JDK and Gradle installed.</span></span> <span data-ttu-id="e6c9d-135">Henüz yüklü değilse, JDK (openjdk-8-jdk) ve Gradle’ı yüklemek için aşağıdakini çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-135">If not yet installed, you can run the following to install JDK(openjdk-8-jdk) and Gradle -</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

<span data-ttu-id="e6c9d-136">Uygulamayı derlemek ve paketlemek için şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e6c9d-136">To build and package the application, run the following:</span></span>

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-the-application"></a><span data-ttu-id="e6c9d-137">Uygulamayı dağıtma</span><span class="sxs-lookup"><span data-stu-id="e6c9d-137">Deploy the application</span></span>
<span data-ttu-id="e6c9d-138">Uygulama oluşturulduktan sonra uygulamayı yerel kümeye dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-138">Once the application is built, you can deploy it to the local cluster.</span></span>

1. <span data-ttu-id="e6c9d-139">Yerel Service Fabric kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-139">Connect to the local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="e6c9d-140">Uygulama paketini kümenin görüntü deposuna kopyalamak, uygulama türünü kaydetmek ve uygulamanın bir örneğini oluşturmak için şablonda verilen yükleme betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-140">Run the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="e6c9d-141">Oluşturulan uygulamayı dağıtma işlemi, diğer tüm Service Fabric uygulamalarında olduğu gibidir.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-141">Deploying the built application is the same as any other Service Fabric application.</span></span> <span data-ttu-id="e6c9d-142">Ayrıntılı yönergeler için [Service Fabric uygulamasını Service Fabric CLI ile yönetme](service-fabric-application-lifecycle-sfctl.md) ile ilgili belgelere bakın.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-142">See the documentation on [managing a Service Fabric application with the Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="e6c9d-143">Bu komutların parametreleri, uygulama paketi içinde oluşturulmuş bildirimlerde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-143">Parameters to these commands can be found in the generated manifests inside the application package.</span></span>

<span data-ttu-id="e6c9d-144">Uygulama dağıtıldığında bir tarayıcı açın ve [http://localhost:19080/Explorer](http://localhost:19080/Explorer) konumundaki [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)'a gidin.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-144">Once the application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span>
<span data-ttu-id="e6c9d-145">Ardından, **Uygulamalar** düğümünü genişletin ve geçerli olarak uygulamanızın türü için bir giriş ve bu türün ilk örneği için başka bir giriş olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-145">Then, expand the **Applications** node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>

## <a name="start-the-test-client-and-perform-a-failover"></a><span data-ttu-id="e6c9d-146">Test istemcisini başlatma ve yük devre gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="e6c9d-146">Start the test client and perform a failover</span></span>
<span data-ttu-id="e6c9d-147">Aktörler kendi başına hiçbir şey yapmaz; başka bir hizmet veya istemcinin aktörlere ileti göndermesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-147">Actors do not do anything on their own, they require another service or client to send them messages.</span></span> <span data-ttu-id="e6c9d-148">Actor şablonu, actor hizmetiyle etkileşim kurmak üzere kullanabileceğiniz basit bir test betiği içerir.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-148">The actor template includes a simple test script that you can use to interact with the actor service.</span></span>

1. <span data-ttu-id="e6c9d-149">Actor hizmetinin çıktısını görmek için izleme yardımcı programını kullanarak betiği çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-149">Run the script using the watch utility to see the output of the actor service.</span></span>  <span data-ttu-id="e6c9d-150">Test betiği bir sayacın değerini yükseltmek için aktörde `setCountAsync()` yöntemine; yeni sayaç değerini edinmek içinse aktörde `getCountAsync()` yöntemine çağrı yapar ve bu değeri konsolda görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-150">The test script calls the `setCountAsync()` method on the actor to increment a counter, calls the `getCountAsync()` method on the actor to get the new counter value, and displays that value to the console.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. <span data-ttu-id="e6c9d-151">Service Fabric Explorer’da actor hizmetinin birincil çoğaltmasını barındıran düğümü bulun.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-151">In Service Fabric Explorer, locate the node hosting the primary replica for the actor service.</span></span> <span data-ttu-id="e6c9d-152">Aşağıdaki ekran görüntüsünde düğüm 3’tür.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-152">In the screenshot below, it is node 3.</span></span> <span data-ttu-id="e6c9d-153">Birincil hizmet çoğaltması okuma ve yazma işlemlerini işler.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-153">The primary service replica handles read and write operations.</span></span>  <span data-ttu-id="e6c9d-154">Daha sonra, hizmet durumundaki değişiklikler, aşağıdaki ekran görüntüsünde görülen 0 ve 1 düğümlerinde çalışan ikincil çoğaltmalara çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-154">Changes in service state are then replicated out to the secondary replicas, running on nodes 0 and 1 in the screen shot below.</span></span>

    ![Service Fabric Explorer’da birincil çoğaltmayı bulma][sfx-primary]

3. <span data-ttu-id="e6c9d-156">**Düğümler**’de, önceki adımda bulduğunuz düğüme tıklayın ve Eylemler menüsünden **Devre dışı bırak (yeniden başlat)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-156">In **Nodes**, click the node you found in the previous step, then select **Deactivate (restart)** from the Actions menu.</span></span> <span data-ttu-id="e6c9d-157">Bu eylem, birincil hizmet çoğaltmasını çalıştıran düğümü yeniden başlatır ve başka bir düğümde çalışan ikincil çoğaltmalardan birine yük devretmeyi zorlar.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-157">This action restarts the node running the primary service replica and forces a failover to one of the secondary replicas running on another node.</span></span>  <span data-ttu-id="e6c9d-158">Bu ikincil çoğaltma birincil konumuna yükseltilir, farklı bir düğümde başka bir ikincil çoğaltma oluşturulur ve birincil çoğaltma okuma/yazma işlemleri almaya başlar.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-158">That secondary replica is promoted to primary, another secondary replica is created on a different node, and the primary replica begins to take read/write operations.</span></span> <span data-ttu-id="e6c9d-159">Düğüm yeniden başlatılırken test istemcisinin çıktısına dikkat edin ve yük devretmeye rağmen sayacın artmaya devam ettiğini gözlemleyin.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-159">As the node restarts, watch the output from the test client and note that the counter continues to increment despite the failover.</span></span>

## <a name="remove-the-application"></a><span data-ttu-id="e6c9d-160">Uygulamayı kaldırma</span><span class="sxs-lookup"><span data-stu-id="e6c9d-160">Remove the application</span></span>
<span data-ttu-id="e6c9d-161">Uygulama örneğini silmek, uygulama paketinin kaydını silmek ve uygulama paketini kümenin görüntü deposundan kaldırmak için şablonda sağlanan kaldırma betiğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-161">Use the uninstall script provided in the template to delete the application instance, unregister the application package, and remove the application package from the cluster's image store.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="e6c9d-162">Service Fabric Explorer’da uygulamanın ve uygulama türünün artık **Uygulamalar** düğümünde olmadığını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-162">In Service Fabric explorer you see that the application and application type no longer appear in the **Applications** node.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="e6c9d-163">Maven'da Service Fabric Java kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="e6c9d-163">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="e6c9d-164">Maven’da barındırılan Service Fabric Java kitaplıkları.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-164">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="e6c9d-165">Projelerinizin **mavenCentral**’daki Service Fabric Java kitaplıklarını kullanması için ``pom.xml`` veya ``build.gradle`` altına bağımlılıklar ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-165">You can add the dependencies in the ``pom.xml`` or ``build.gradle`` of your projects to use Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="e6c9d-166">Aktörler</span><span class="sxs-lookup"><span data-stu-id="e6c9d-166">Actors</span></span>

<span data-ttu-id="e6c9d-167">Uygulamanız için Service Fabric Güvenilir Aktör desteği.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-167">Service Fabric Reliable Actor support for your application.</span></span>

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

### <a name="services"></a><span data-ttu-id="e6c9d-168">Hizmetler</span><span class="sxs-lookup"><span data-stu-id="e6c9d-168">Services</span></span>

<span data-ttu-id="e6c9d-169">Uygulamanız için Service Fabric Durum Bilgisi Olmayan Hizmet desteği.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-169">Service Fabric Stateless Service support for your application.</span></span>

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

### <a name="others"></a><span data-ttu-id="e6c9d-170">Diğer</span><span class="sxs-lookup"><span data-stu-id="e6c9d-170">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="e6c9d-171">Aktarım</span><span class="sxs-lookup"><span data-stu-id="e6c9d-171">Transport</span></span>

<span data-ttu-id="e6c9d-172">Service Fabric Java uygulaması için Aktarım katmanı desteği.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-172">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="e6c9d-173">Aktarım katmanında özellikle programlamadığınız sürece bu bağımlılığı Güvenilir Aktör veya Hizmet uygulamalarınız için özellikle eklemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-173">You do not need to explicitly add this dependency to your Reliable Actor or Service applications, unless you program at the transport layer.</span></span>

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

#### <a name="fabric-support"></a><span data-ttu-id="e6c9d-174">Fabric desteği</span><span class="sxs-lookup"><span data-stu-id="e6c9d-174">Fabric support</span></span>

<span data-ttu-id="e6c9d-175">Yerel Service Fabric çalışma zamanıyla iletişim kuran Service Fabric için sistem düzeyinde destek.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-175">System level support for Service Fabric, which talks to native Service Fabric runtime.</span></span> <span data-ttu-id="e6c9d-176">Bu bağımlılığı Güvenilir Aktör veya Hizmet uygulamalarınız için özellikle eklemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-176">You do not need to explicitly add this dependency to your Reliable Actor or Service applications.</span></span> <span data-ttu-id="e6c9d-177">Yukarıdaki diğer bağımlılıkları eklediğinizde bu otomatik olarak Maven’dan alınır.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-177">This gets fetched automatically from Maven, when you include the other dependencies above.</span></span>

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

## <a name="migrating-old-service-fabric-java-applications-to-be-used-with-maven"></a><span data-ttu-id="e6c9d-178">Eski Service Fabric Java uygulamalarını Maven ile kullanılmak üzere geçirme</span><span class="sxs-lookup"><span data-stu-id="e6c9d-178">Migrating old Service Fabric Java applications to be used with Maven</span></span>
<span data-ttu-id="e6c9d-179">Service Fabric Java kitaplıklarını yakın zamanda Service Fabric Java SDK’sından Maven deposuna taşıdık.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-179">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK to Maven repository.</span></span> <span data-ttu-id="e6c9d-180">Yeoman veya Eclipse kullanarak oluşturduğunuz yeni uygulamalar en son güncelleştirilen projeleri oluşturur (Maven ile çalışırlar), ancak daha önce Service Fabric Java SDK’sı kullanan mevcut Service Fabric durum bilgisi olmayan ya da aktör Java uygulamalarını Maven’ın Service Fabric Java bağımlılıklarını kullanacak şekilde güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-180">While the new applications you generate using Yeoman or Eclipse, will generate latest updated projects (which will be able to work with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using the Service Fabric Java SDK earlier, to use the Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="e6c9d-181">Eski uygulamanızın Maven ile çalıştığından emin olmak için lütfen [burada](service-fabric-migrate-old-javaapp-to-use-maven.md) belirtilen adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="e6c9d-181">Please follow the steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) to ensure your older application works with Maven.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6c9d-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e6c9d-182">Next steps</span></span>

* [<span data-ttu-id="e6c9d-183">Linux’ta Eclipse kullanarak ilk Service Fabric Java uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6c9d-183">Create your first Service Fabric Java application on Linux using Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="e6c9d-184">Reliable Actors hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="e6c9d-184">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="e6c9d-185">Service Fabric CLI’sını kullanarak Service Fabric kümeleriyle etkileşim kurma</span><span class="sxs-lookup"><span data-stu-id="e6c9d-185">Interact with Service Fabric clusters using the Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="e6c9d-186">[Service Fabric destek seçenekleri](service-fabric-support.md) hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="e6c9d-186">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="e6c9d-187">Service Fabric CLI ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e6c9d-187">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
