---
title: "aaaCreate ilk Azure mikro uygulamanıza C# kullanarak Linux | Microsoft Docs"
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
ms.openlocfilehash: 68d685e130be338ebcdb2f1af24b66d1e14f580a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a><span data-ttu-id="2a6bd-103">İlk Azure Service Fabric uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2a6bd-103">Create your first Azure Service Fabric application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2a6bd-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="2a6bd-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="2a6bd-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="2a6bd-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="2a6bd-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="2a6bd-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="2a6bd-107">Service Fabric, Linux üzerinde hem .NET Core hem de Java dillerinde hizmet oluşturmaya yönelik SDK’lar sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span></span> <span data-ttu-id="2a6bd-108">Bu öğreticide, nasıl tümleştirildiği incelenmektedir toocreate Linux ve yapı C# (.NET Core) kullanarak bir hizmet için bir uygulama.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-108">In this tutorial, we look at how toocreate an application for Linux and build a service using C# (.NET Core).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a6bd-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2a6bd-109">Prerequisites</span></span>
<span data-ttu-id="2a6bd-110">Başlamadan önce [Linux geliştirme ortamınızı ayarladığınızdan](service-fabric-get-started-linux.md) emin olun.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-110">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="2a6bd-111">Mac OS X kullanıyorsanız, [Vagrant kullanarak bir sanal makinede Linux one-box ortamı ayarlayabilirsiniz](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="2a6bd-111">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="2a6bd-112">Ayrıca tooinstall hello isteyeceksiniz [Service Fabric CLI](service-fabric-cli.md)</span><span class="sxs-lookup"><span data-stu-id="2a6bd-112">You will also want tooinstall hello [Service Fabric CLI](service-fabric-cli.md)</span></span>

### <a name="install-and-set-up-hello-generators-for-csharp"></a><span data-ttu-id="2a6bd-113">Yükleme ve hello oluşturucuları için CSharp ayarlayın</span><span class="sxs-lookup"><span data-stu-id="2a6bd-113">Install and set up hello generators for CSharp</span></span>
<span data-ttu-id="2a6bd-114">Service Fabric, Yeoman şablon oluşturucu kullanarak terminalden Service Fabric CSharp uygulaması oluşturmanıza yardımcı olacak yapı iskelesi araçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric CSharp application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="2a6bd-115">Lütfen makinenizde çalışma CSharp hello Service Fabric yeoman şablonu üreteci olan tooensure hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-115">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for CSharp working on your machine.</span></span>
1. <span data-ttu-id="2a6bd-116">Makinenize nodejs ve NPM yükleme</span><span class="sxs-lookup"><span data-stu-id="2a6bd-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="2a6bd-117">NPM’den makinenize [Yeoman](http://yeoman.io/) şablon oluşturucuyu yükleme</span><span class="sxs-lookup"><span data-stu-id="2a6bd-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="2a6bd-118">Merhaba Service Fabric Yeo Java uygulama üreteci NPM yükleme</span><span class="sxs-lookup"><span data-stu-id="2a6bd-118">Install hello Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a><span data-ttu-id="2a6bd-119">Merhaba uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="2a6bd-119">Create hello application</span></span>
<span data-ttu-id="2a6bd-120">Service Fabric uygulaması bir veya daha fazla hizmetlerin her hello uygulamanın işlevselliğini aktarma konusunda belirli bir rol içerebilir.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-120">A Service Fabric application can contain one or more services, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="2a6bd-121">Merhaba Service Fabric [Yeoman](http://yeoman.io/) son adımda yüklediğiniz, CSharp için oluşturucuyu kolay toocreate kılar ilk hizmet ve daha sonra tooadd.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-121">hello Service Fabric [Yeoman](http://yeoman.io/) generator for CSharp, which you installed in last step, makes it easy toocreate your first service and tooadd more later.</span></span> <span data-ttu-id="2a6bd-122">Yeoman toocreate uygulamanın tek bir hizmetle kullanalım.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-122">Let's use Yeoman toocreate an application with a single service.</span></span>

1. <span data-ttu-id="2a6bd-123">Bir terminale hello iskele oluşturma komut toostart aşağıdaki hello yazın:`yo azuresfcsharp`</span><span class="sxs-lookup"><span data-stu-id="2a6bd-123">In a terminal, type hello following command toostart building hello scaffolding: `yo azuresfcsharp`</span></span>
2. <span data-ttu-id="2a6bd-124">Uygulamanızı adlandırın.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-124">Name your application.</span></span>
3. <span data-ttu-id="2a6bd-125">İlk hizmetiniz Hello türünü seçin ve adlandırın.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-125">Choose hello type of your first service and name it.</span></span> <span data-ttu-id="2a6bd-126">Bu öğreticinin Hello amaçları doğrultusunda, güvenilir bir aktör hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-126">For hello purposes of this tutorial, we choose a Reliable Actor Service.</span></span>

   ![C# için Service Fabric Yeoman oluşturucusu][sf-yeoman]

> [!NOTE]
> <span data-ttu-id="2a6bd-128">Başlangıç seçenekleri hakkında daha fazla bilgi için bkz: [Service Fabric programlama modeline genel bakış](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="2a6bd-128">For more information about hello options, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
>
>

## <a name="build-hello-application"></a><span data-ttu-id="2a6bd-129">Merhaba uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="2a6bd-129">Build hello application</span></span>
<span data-ttu-id="2a6bd-130">Merhaba Service Fabric Yeoman şablonları toobuild hello hello terminal uygulamadan (toohello uygulama klasörü gezinme sonra) kullanabileceğiniz bir yapı betiği içerir.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-130">hello Service Fabric Yeoman templates include a build script that you can use toobuild hello app from hello terminal (after navigating toohello application folder).</span></span>

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-hello-application"></a><span data-ttu-id="2a6bd-131">Merhaba uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="2a6bd-131">Deploy hello application</span></span>

<span data-ttu-id="2a6bd-132">Merhaba uygulama oluşturulduktan sonra toohello yerel küme dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-132">Once hello application is built, you can deploy it toohello local cluster.</span></span>

1. <span data-ttu-id="2a6bd-133">Toohello yerel Service Fabric kümesi bağlayın.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-133">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="2a6bd-134">Merhaba şablonu toocopy Merhaba uygulaması toohello kümenin görüntü deposu paketini, hello uygulama türünü kaydetme ve hello uygulama örneğini oluşturmak sağlanan hello yükleme betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-134">Run hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="2a6bd-135">Dağıtma yerleşik hello aynı başka bir Service Fabric uygulama hello uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-135">Deploying hello built application is hello same as any other Service Fabric application.</span></span> <span data-ttu-id="2a6bd-136">Merhaba belgelerine bakın [bir Service Fabric uygulaması hello Service Fabric CLI ile yönetme](service-fabric-application-lifecycle-sfctl.md) ayrıntılı yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-136">See hello documentation on [managing a Service Fabric application with hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="2a6bd-137">Parametreleri toothese komutları hello oluşturulan bildirimleri hello uygulama paketi içinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-137">Parameters toothese commands can be found in hello generated manifests inside hello application package.</span></span>

<span data-ttu-id="2a6bd-138">Merhaba uygulama dağıtıldıktan sonra bir tarayıcı açın ve gidin [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) adresindeki [http://localhost: 19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="2a6bd-138">Once hello application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="2a6bd-139">Ardından, hello genişletin **uygulamaları** düğümü ve olduğunu şimdi uygulama türü için bir giriş ve hello bu türünün ilk örneği için başka bir not.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-139">Then, expand hello **Applications** node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

## <a name="start-hello-test-client-and-perform-a-failover"></a><span data-ttu-id="2a6bd-140">Merhaba test istemcisi başlatın ve bir yük devretme gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-140">Start hello test client and perform a failover</span></span>
<span data-ttu-id="2a6bd-141">Actor projeleri kendi başına bir işlem yapamaz.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-141">Actor projects do not do anything on their own.</span></span> <span data-ttu-id="2a6bd-142">Başka bir hizmet veya istemci toosend gereksinim duydukları bunları iletileri.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-142">They require another service or client toosend them messages.</span></span> <span data-ttu-id="2a6bd-143">Merhaba aktör şablon toointeract hello aktör hizmeti ile kullanabileceğiniz bir basit bir sınama betiği içerir.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-143">hello actor template includes a simple test script that you can use toointeract with hello actor service.</span></span>

1. <span data-ttu-id="2a6bd-144">Merhaba izleme yardımcı programı toosee hello çıkış hello aktör hizmeti kullanan hello komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-144">Run hello script using hello watch utility toosee hello output of hello actor service.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. <span data-ttu-id="2a6bd-145">Service Fabric Explorer'da hello birincil çoğaltma hello aktör hizmeti için barındırma düğümü bulun.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-145">In Service Fabric Explorer, locate node hosting hello primary replica for hello actor service.</span></span> <span data-ttu-id="2a6bd-146">Merhaba ekran görüntüsünde, onu 3 düğümdür.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-146">In hello screenshot below, it is node 3.</span></span>

    ![Service Fabric Explorer'da bulma hello birincil çoğaltma][sfx-primary]
3. <span data-ttu-id="2a6bd-148">Merhaba önceki adımda bulunan sonra seçin hello düğümünü tıklatın **devre dışı bırak (yeniden)** hello Eylemler menüsünden.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-148">Click hello node you found in hello previous step, then select **Deactivate (restart)** from hello Actions menu.</span></span> <span data-ttu-id="2a6bd-149">Bu eylem, yerel kümedeki başka bir düğüm üzerinde çalışan bir yük devretme tooa ikincil bir çoğaltma zorlama bir düğümü yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-149">This action restarts one node in your local cluster forcing a failover tooa secondary replica running on another node.</span></span> <span data-ttu-id="2a6bd-150">Bu eylemi gerçekleştirme gibi dikkat toohello çıktı hello test istemcisi ve hello sayaç tooincrement hello yük devretme rağmen devam Not ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-150">As you perform this action, pay attention toohello output from hello test client and note that hello counter continues tooincrement despite hello failover.</span></span>

## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="2a6bd-151">Daha fazla Hizmetleri tooan varolan uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="2a6bd-151">Adding more services tooan existing application</span></span>

<span data-ttu-id="2a6bd-152">tooadd başka bir hizmet tooan uygulaması zaten kullanılarak oluşturulan `yo`, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2a6bd-152">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span>
1. <span data-ttu-id="2a6bd-153">Merhaba var olan uygulamanın toohello kök dizini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-153">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="2a6bd-154">Örneğin, `cd ~/YeomanSamples/MyApplication`, `MyApplication` Yeoman tarafından oluşturulan hello uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-154">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="2a6bd-155">`yo azuresfcsharp:AddService` öğesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="2a6bd-155">Run `yo azuresfcsharp:AddService`</span></span>

## <a name="migrating-from-projectjson-toocsproj"></a><span data-ttu-id="2a6bd-156">Project.JSON too.csproj ' geçiş</span><span class="sxs-lookup"><span data-stu-id="2a6bd-156">Migrating from project.json too.csproj</span></span>
1. <span data-ttu-id="2a6bd-157">'Dotnet geçirmek' proje kök dizininde çalıştıran tüm hello project.json toocsproj biçimi geçirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-157">Running 'dotnet migrate' in project root directory will migrate all hello project.json toocsproj format.</span></span>
2. <span data-ttu-id="2a6bd-158">Güncelleştirme hello proje uygun şekilde proje dosyalarını toocsproj dosyalarında başvurur.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-158">Update hello project references accordingly toocsproj files in project files.</span></span>
3. <span data-ttu-id="2a6bd-159">Merhaba proje dosyası adları toocsproj dosyalarında build.sh güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="2a6bd-159">Update hello project file names toocsproj files in build.sh.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a6bd-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2a6bd-160">Next steps</span></span>

* [<span data-ttu-id="2a6bd-161">Reliable Actors hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="2a6bd-161">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="2a6bd-162">Merhaba Service Fabric CLI kullanarak Service Fabric kümeleri ile etkileşim kurma</span><span class="sxs-lookup"><span data-stu-id="2a6bd-162">Interacting with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="2a6bd-163">[Service Fabric destek seçenekleri](service-fabric-support.md) hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="2a6bd-163">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="2a6bd-164">Service Fabric CLI ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="2a6bd-164">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
