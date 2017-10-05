---
title: "Linux üzerinde C# kullanarak ilk Azure mikro hizmetlerinizi oluşturma | Microsoft Docs"
description: "C# kullanarak Service Fabric uygulaması oluşturma ve dağıtma"
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/21/2017
ms.author: subramar
ms.openlocfilehash: adcafaa5522fcddc0a01eb1dc8deba04ebfc38f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a><span data-ttu-id="21afd-103">İlk Azure Service Fabric uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="21afd-103">Create your first Azure Service Fabric application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="21afd-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="21afd-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="21afd-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="21afd-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="21afd-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="21afd-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="21afd-107">Service Fabric, Linux üzerinde hem .NET Core hem de Java dillerinde hizmet oluşturmaya yönelik SDK’lar sağlar.</span><span class="sxs-lookup"><span data-stu-id="21afd-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span></span> <span data-ttu-id="21afd-108">Bu öğreticide, C# (.NET Core) kullanarak Linux için bir uygulama ve hizmet oluşturmayı öğreneceğiz.</span><span class="sxs-lookup"><span data-stu-id="21afd-108">In this tutorial, we look at how to create an application for Linux and build a service using C# (.NET Core).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21afd-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="21afd-109">Prerequisites</span></span>
<span data-ttu-id="21afd-110">Başlamadan önce [Linux geliştirme ortamınızı ayarladığınızdan](service-fabric-get-started-linux.md) emin olun.</span><span class="sxs-lookup"><span data-stu-id="21afd-110">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="21afd-111">Mac OS X kullanıyorsanız, [Vagrant kullanarak bir sanal makinede Linux one-box ortamı ayarlayabilirsiniz](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="21afd-111">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="21afd-112">[Service Fabric CLI](service-fabric-cli.md)’yı de yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="21afd-112">You will also want to install the [Service Fabric CLI](service-fabric-cli.md)</span></span>

### <a name="install-and-set-up-the-generators-for-csharp"></a><span data-ttu-id="21afd-113">CSharp için oluşturucuları yükleme ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="21afd-113">Install and set up the generators for CSharp</span></span>
<span data-ttu-id="21afd-114">Service Fabric, Yeoman şablon oluşturucu kullanarak terminalden Service Fabric CSharp uygulaması oluşturmanıza yardımcı olacak yapı iskelesi araçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="21afd-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric CSharp application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="21afd-115">Lütfen makinenizde çalışan bir CSharp için Service Fabric yeoman şablon oluşturucu olduğundan emin olmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="21afd-115">Please follow the steps below to ensure you have the Service Fabric yeoman template generator for CSharp working on your machine.</span></span>
1. <span data-ttu-id="21afd-116">Makinenize nodejs ve NPM yükleme</span><span class="sxs-lookup"><span data-stu-id="21afd-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="21afd-117">NPM’den makinenize [Yeoman](http://yeoman.io/) şablon oluşturucuyu yükleme</span><span class="sxs-lookup"><span data-stu-id="21afd-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="21afd-118">NPM’den Service Fabric Yeo Java uygulama oluşturucuyu yükleme</span><span class="sxs-lookup"><span data-stu-id="21afd-118">Install the Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-the-application"></a><span data-ttu-id="21afd-119">Uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="21afd-119">Create the application</span></span>
<span data-ttu-id="21afd-120">Service Fabric uygulaması bir veya birden çok hizmet içerebilir. Bu hizmetlerin her biri uygulamanın işlevselliğini aktarma konusunda belirli bir role sahiptir.</span><span class="sxs-lookup"><span data-stu-id="21afd-120">A Service Fabric application can contain one or more services, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="21afd-121">Son adımda yüklediğiniz CSharp için Service Fabric [Yeoman](http://yeoman.io/) oluşturucu, ilk hizmetinizi oluşturmanızı ve daha sonra yeni hizmetler eklemenizi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="21afd-121">The Service Fabric [Yeoman](http://yeoman.io/) generator for CSharp, which you installed in last step, makes it easy to create your first service and to add more later.</span></span> <span data-ttu-id="21afd-122">Tek bir hizmetle uygulama oluşturmak için Yeoman’ı kullanalım.</span><span class="sxs-lookup"><span data-stu-id="21afd-122">Let's use Yeoman to create an application with a single service.</span></span>

1. <span data-ttu-id="21afd-123">Bir terminalde iskele oluşturmaya başlamak için aşağıdaki komutu yazın:`yo azuresfcsharp`</span><span class="sxs-lookup"><span data-stu-id="21afd-123">In a terminal, type the following command to start building the scaffolding: `yo azuresfcsharp`</span></span>
2. <span data-ttu-id="21afd-124">Uygulamanızı adlandırın.</span><span class="sxs-lookup"><span data-stu-id="21afd-124">Name your application.</span></span>
3. <span data-ttu-id="21afd-125">Birinci hizmetinizin türünü seçin ve adlandırın.</span><span class="sxs-lookup"><span data-stu-id="21afd-125">Choose the type of your first service and name it.</span></span> <span data-ttu-id="21afd-126">Bu öğreticinin amaçları doğrultusunda, Reliable Actor Hizmetini seçiyoruz.</span><span class="sxs-lookup"><span data-stu-id="21afd-126">For the purposes of this tutorial, we choose a Reliable Actor Service.</span></span>

   ![C# için Service Fabric Yeoman oluşturucusu][sf-yeoman]

> [!NOTE]
> <span data-ttu-id="21afd-128">Seçenekler hakkında daha fazla bilgi için bkz. [Service Fabric programlama modeline genel bakış](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="21afd-128">For more information about the options, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
>
>

## <a name="build-the-application"></a><span data-ttu-id="21afd-129">Uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="21afd-129">Build the application</span></span>
<span data-ttu-id="21afd-130">Service Fabric Yeoman şablonları, uygulamayı terminalden oluşturmak (uygulama klasörüne gittikten sonra) için kullanabileceğiniz bir yapı betiği içerir.</span><span class="sxs-lookup"><span data-stu-id="21afd-130">The Service Fabric Yeoman templates include a build script that you can use to build the app from the terminal (after navigating to the application folder).</span></span>

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-the-application"></a><span data-ttu-id="21afd-131">Uygulamayı dağıtma</span><span class="sxs-lookup"><span data-stu-id="21afd-131">Deploy the application</span></span>

<span data-ttu-id="21afd-132">Uygulama oluşturulduktan sonra uygulamayı yerel kümeye dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21afd-132">Once the application is built, you can deploy it to the local cluster.</span></span>

1. <span data-ttu-id="21afd-133">Yerel Service Fabric kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="21afd-133">Connect to the local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="21afd-134">Uygulama paketini kümenin görüntü deposuna kopyalamak, uygulama türünü kaydetmek ve uygulamanın bir örneğini oluşturmak için şablonda verilen yükleme betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="21afd-134">Run the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="21afd-135">Oluşturulan uygulamayı dağıtma işlemi, diğer tüm Service Fabric uygulamalarında olduğu gibidir.</span><span class="sxs-lookup"><span data-stu-id="21afd-135">Deploying the built application is the same as any other Service Fabric application.</span></span> <span data-ttu-id="21afd-136">Ayrıntılı yönergeler için [Service Fabric uygulamasını Service Fabric CLI ile yönetme](service-fabric-application-lifecycle-sfctl.md) ile ilgili belgelere bakın.</span><span class="sxs-lookup"><span data-stu-id="21afd-136">See the documentation on [managing a Service Fabric application with the Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="21afd-137">Bu komutların parametreleri, uygulama paketi içinde oluşturulmuş bildirimlerde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="21afd-137">Parameters to these commands can be found in the generated manifests inside the application package.</span></span>

<span data-ttu-id="21afd-138">Uygulama dağıtıldığında bir tarayıcı açın ve [http://localhost:19080/Explorer](http://localhost:19080/Explorer) konumundaki [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)'a gidin.</span><span class="sxs-lookup"><span data-stu-id="21afd-138">Once the application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="21afd-139">Ardından, **Uygulamalar** düğümünü genişletin ve geçerli olarak uygulamanızın türü için bir giriş ve bu türün ilk örneği için başka bir giriş olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="21afd-139">Then, expand the **Applications** node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>

## <a name="start-the-test-client-and-perform-a-failover"></a><span data-ttu-id="21afd-140">Test istemcisini başlatma ve yük devre gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="21afd-140">Start the test client and perform a failover</span></span>
<span data-ttu-id="21afd-141">Actor projeleri kendi başına bir işlem yapamaz.</span><span class="sxs-lookup"><span data-stu-id="21afd-141">Actor projects do not do anything on their own.</span></span> <span data-ttu-id="21afd-142">Bunlar başka bir hizmet veya istemcinin kendilerine iletiler göndermesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="21afd-142">They require another service or client to send them messages.</span></span> <span data-ttu-id="21afd-143">Actor şablonu, actor hizmetiyle etkileşim kurmak üzere kullanabileceğiniz basit bir test betiği içerir.</span><span class="sxs-lookup"><span data-stu-id="21afd-143">The actor template includes a simple test script that you can use to interact with the actor service.</span></span>

1. <span data-ttu-id="21afd-144">Actor hizmetinin çıktısını görmek için izleme yardımcı programını kullanarak betiği çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="21afd-144">Run the script using the watch utility to see the output of the actor service.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. <span data-ttu-id="21afd-145">Service Fabric Explorer’da actor hizmetinin birincil çoğaltmasını barındıran düğümü bulun.</span><span class="sxs-lookup"><span data-stu-id="21afd-145">In Service Fabric Explorer, locate node hosting the primary replica for the actor service.</span></span> <span data-ttu-id="21afd-146">Aşağıdaki ekran görüntüsünde düğüm 3’tür.</span><span class="sxs-lookup"><span data-stu-id="21afd-146">In the screenshot below, it is node 3.</span></span>

    ![Service Fabric Explorer’da birincil çoğaltmayı bulma][sfx-primary]
3. <span data-ttu-id="21afd-148">Önceki adımda bulduğunuz düğüme tıklayın, ardından Eylemler menüsünden **Devre dışı bırak (yeniden başlat)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="21afd-148">Click the node you found in the previous step, then select **Deactivate (restart)** from the Actions menu.</span></span> <span data-ttu-id="21afd-149">Bu eylem, yerel kümenizdeki bir düğümü yeniden başlatır. Böylece başka bir düğümde çalışan ikincil bir çoğaltmaya yük devretmesi için zorlanır.</span><span class="sxs-lookup"><span data-stu-id="21afd-149">This action restarts one node in your local cluster forcing a failover to a secondary replica running on another node.</span></span> <span data-ttu-id="21afd-150">Bu eylemi gerçekleştirirken, test istemcisinden gelen çıkışa dikkat edin ve sayacın yük devretmeye rağmen artmaya devam ettiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="21afd-150">As you perform this action, pay attention to the output from the test client and note that the counter continues to increment despite the failover.</span></span>

## <a name="adding-more-services-to-an-existing-application"></a><span data-ttu-id="21afd-151">Mevcut bir uygulamaya daha fazla hizmet ekleme</span><span class="sxs-lookup"><span data-stu-id="21afd-151">Adding more services to an existing application</span></span>

<span data-ttu-id="21afd-152">`yo` kullanılarak oluşturulmuş bir uygulamaya başka bir hizmet eklemek için aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="21afd-152">To add another service to an application already created using `yo`, perform the following steps:</span></span>
1. <span data-ttu-id="21afd-153">Dizini mevcut uygulamanın kök dizinine değiştirin.</span><span class="sxs-lookup"><span data-stu-id="21afd-153">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="21afd-154">Örneğin Yeoman tarafından oluşturulan uygulama `MyApplication` ise `cd ~/YeomanSamples/MyApplication` olacaktır.</span><span class="sxs-lookup"><span data-stu-id="21afd-154">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="21afd-155">`yo azuresfcsharp:AddService` öğesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="21afd-155">Run `yo azuresfcsharp:AddService`</span></span>

## <a name="migrating-from-projectjson-to-csproj"></a><span data-ttu-id="21afd-156">project.json biçiminden .csproj biçimine geçiş</span><span class="sxs-lookup"><span data-stu-id="21afd-156">Migrating from project.json to .csproj</span></span>
1. <span data-ttu-id="21afd-157">Proje kök dizininde "dotnet migrate" komutunun çalıştırılmasıyla tüm project.json dosyaları csproj biçimine geçirilir.</span><span class="sxs-lookup"><span data-stu-id="21afd-157">Running 'dotnet migrate' in project root directory will migrate all the project.json to csproj format.</span></span>
2. <span data-ttu-id="21afd-158">Proje dosyalarındaki proje başvurularını uygun şekilde csproj dosyalarına güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="21afd-158">Update the project references accordingly to csproj files in project files.</span></span>
3. <span data-ttu-id="21afd-159">build.sh'deki proje dosya adlarını csproj dosyalarına güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="21afd-159">Update the project file names to csproj files in build.sh.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21afd-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="21afd-160">Next steps</span></span>

* [<span data-ttu-id="21afd-161">Reliable Actors hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="21afd-161">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="21afd-162">Service Fabric CLI’sını kullanarak Service Fabric kümeleriyle etkileşim kurma</span><span class="sxs-lookup"><span data-stu-id="21afd-162">Interacting with Service Fabric clusters using the Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="21afd-163">[Service Fabric destek seçenekleri](service-fabric-support.md) hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="21afd-163">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="21afd-164">Service Fabric CLI ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="21afd-164">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
