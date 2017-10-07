---
title: "yerel bir Docker kapsayıcısı aaaDebugging uygulamalarında | Microsoft Docs"
description: "Nasıl toomodify yerel Docker kapsayıcısı içinde çalışan bir uygulama hello kapsayıcı düzenleme ve yenileme aracılığıyla yenileyin ve hata ayıklama kesme noktaları ayarlayın öğrenin"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/22/2016
ms.author: mlearned
ms.openlocfilehash: ff64e62fbb93901a29b5496bd5e17d2c4ea5ca99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a><span data-ttu-id="2de53-103">Yerel Docker kapsayıcısındaki uygulamalar için hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="2de53-103">Debugging apps in a local Docker container</span></span>
## <a name="overview"></a><span data-ttu-id="2de53-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2de53-104">Overview</span></span>
<span data-ttu-id="2de53-105">Docker için Visual Studio Araçları Hello bir tutarlı bir yol toodevelop sağlar ve uygulamanızda yerel olarak Linux Docker kapsayıcısı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="2de53-105">hello Visual Studio Tools for Docker provides a consistent way toodevelop in and validate your application locally in a Linux Docker container.</span></span>
<span data-ttu-id="2de53-106">Bir kod değişikliği yaptığınızda toorestart hello kapsayıcısı yok.</span><span class="sxs-lookup"><span data-stu-id="2de53-106">You don't have toorestart hello container each time you make a code change.</span></span>
<span data-ttu-id="2de53-107">Bu makalede nasıl toouse hello "Düzenle ve Yenile" özelliği toostart yerel bir Docker kapsayıcısı ASP.NET çekirdek Web uygulamasında gerekli değişiklikleri yapın ve ardından bu değişiklikleri hello tarayıcı toosee yenileyin gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="2de53-107">This article illustrates how toouse hello "Edit and Refresh" feature toostart an ASP.NET Core Web app in a local Docker container, make any necessary changes, and then refresh hello browser toosee those changes.</span></span>
<span data-ttu-id="2de53-108">Bu makalede ayrıca nasıl gösterilmektedir hata ayıklama için tooset kesme noktaları.</span><span class="sxs-lookup"><span data-stu-id="2de53-108">This article also shows you how tooset breakpoints for debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="2de53-109">Windows kapsayıcı desteği gelecekteki bir sürümde geliyor</span><span class="sxs-lookup"><span data-stu-id="2de53-109">Windows Container support will be coming in a future release</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="2de53-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2de53-110">Prerequisites</span></span>
<span data-ttu-id="2de53-111">Araçlar aşağıdaki hello yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2de53-111">hello following tools must be installed.</span></span>

* [<span data-ttu-id="2de53-112">Visual Studio en son sürümü</span><span class="sxs-lookup"><span data-stu-id="2de53-112">Latest version of Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="2de53-113">Microsoft ASP.NET Core 1.0 SDK'sı</span><span class="sxs-lookup"><span data-stu-id="2de53-113">Microsoft ASP.NET Core 1.0 SDK</span></span>](https://go.microsoft.com/fwlink/?LinkID=809122)

<span data-ttu-id="2de53-114">yerel olarak toorun Docker kapsayıcıları için yerel docker istemci gerekir.</span><span class="sxs-lookup"><span data-stu-id="2de53-114">toorun Docker containers locally, you'll need a local docker client.</span></span>
<span data-ttu-id="2de53-115">Hello kullanabilirsiniz [Docker araç](https://www.docker.com/products/docker-toolbox), Hyper-V toobe devre dışı gerektiren veya kullanabilirsiniz [Docker için Windows](https://www.docker.com/get-docker), Hyper-V kullanır ve Windows 10 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2de53-115">You can use hello [Docker Toolbox](https://www.docker.com/products/docker-toolbox), which requires Hyper-V toobe disabled, or you can use [Docker for Windows](https://www.docker.com/get-docker), which uses Hyper-V, and requires Windows 10.</span></span>

<span data-ttu-id="2de53-116">Docker araç kullanıyorsanız, çok gerekir[hello Docker istemcisini yapılandırma](vs-azure-tools-docker-setup.md)</span><span class="sxs-lookup"><span data-stu-id="2de53-116">If using Docker Toolbox, you'll need too[configure hello Docker client](vs-azure-tools-docker-setup.md)</span></span>

## <a name="1-create-a-web-app"></a><span data-ttu-id="2de53-117">1. Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="2de53-117">1. Create a web app</span></span>
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="2de53-118">2. Docker desteği ekleme</span><span class="sxs-lookup"><span data-stu-id="2de53-118">2. Add Docker support</span></span>
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a><span data-ttu-id="2de53-119">3. Kod ve yenileme Düzenle</span><span class="sxs-lookup"><span data-stu-id="2de53-119">3. Edit your code and refresh</span></span>
<span data-ttu-id="2de53-120">tooquickly yinelemek değişiklikleri, uygulamanızı bir kapsayıcıdaki başlatın ve IIS Express ile olduğu gibi bunları görüntüleme toomake değişiklikler devam.</span><span class="sxs-lookup"><span data-stu-id="2de53-120">tooquickly iterate changes, you can start your application within a container, and continue toomake changes, viewing them as you would with IIS Express.</span></span>

1. <span data-ttu-id="2de53-121">Merhaba çözüm yapılandırma çok ayarlamak`Debug` ve tuşuna basın  **&lt;CTRL + F5 >** toobuild, docker görüntü ve yerel olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2de53-121">Set hello Solution Configuration too`Debug` and press **&lt;CTRL + F5>** toobuild your docker image and run it locally.</span></span>

    <span data-ttu-id="2de53-122">Merhaba kapsayıcı görüntü oluşturulduğundan ve Docker kapsayıcısı içinde çalışan sonra Visual Studio varsayılan tarayıcınızda hello Web uygulaması başlatın.</span><span class="sxs-lookup"><span data-stu-id="2de53-122">Once hello container image has been built and is running in a Docker container, Visual Studio will launch hello Web app in your default browser.</span></span>
    <span data-ttu-id="2de53-123">Merhaba Microsoft Edge tarayıcı kullanıyorsanız veya aksi halde hatalar varsa, bkz: [sorun giderme](vs-azure-tools-docker-troubleshooting-docker-errors.md) bölümü.</span><span class="sxs-lookup"><span data-stu-id="2de53-123">If you are using hello Microsoft Edge browser or otherwise have errors, see [Troubleshooting](vs-azure-tools-docker-troubleshooting-docker-errors.md) section.</span></span>
2. <span data-ttu-id="2de53-124">Toohello toomake değişikliklerimizi burada yapacağız olduğundan sayfa hakkında gidin.</span><span class="sxs-lookup"><span data-stu-id="2de53-124">Go toohello About page, which is where we're going toomake our changes.</span></span>
3. <span data-ttu-id="2de53-125">TooVisual Studio dönün ve açık `Views\Home\About.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="2de53-125">Return tooVisual Studio and open `Views\Home\About.cshtml`.</span></span>
4. <span data-ttu-id="2de53-126">HTML içerik toohello hello dosyasının sonuna aşağıdaki hello ekleyin ve hello değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2de53-126">Add hello following HTML content toohello end of hello file and save hello changes.</span></span>

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. <span data-ttu-id="2de53-127">Hello çıktı penceresinde hello .NET derleme tamamlandığında ve bu satırları görmek görüntüleme, geri tooyour tarayıcı geçin ve sayfa hakkında hello yenileyin.</span><span class="sxs-lookup"><span data-stu-id="2de53-127">Viewing hello output window, when hello .NET build is completed and you see these lines, switch back tooyour browser and refresh hello About page.</span></span>

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C tooshut down
   ```
6. <span data-ttu-id="2de53-128">Yaptığınız değişiklikleri uygulandı!</span><span class="sxs-lookup"><span data-stu-id="2de53-128">Your changes have been applied!</span></span>

## <a name="4-debug-with-breakpoints"></a><span data-ttu-id="2de53-129">4. Kesme noktaları ile hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="2de53-129">4. Debug with breakpoints</span></span>
<span data-ttu-id="2de53-130">Genellikle, değişiklikleri daha ayrıntılı denetleme, Visual Studio'nun özellikleri hata ayıklama hello yararlanarak gerekir.</span><span class="sxs-lookup"><span data-stu-id="2de53-130">Often, changes will need further inspection, leveraging hello debugging features of Visual Studio.</span></span>

1. <span data-ttu-id="2de53-131">Dönüş tooVisual Studio ve Aç`Controllers\HomeController.cs`</span><span class="sxs-lookup"><span data-stu-id="2de53-131">Return tooVisual Studio and open `Controllers\HomeController.cs`</span></span>
2. <span data-ttu-id="2de53-132">Merhaba About() yöntemi Merhaba içeriğine hello şununla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="2de53-132">Replace hello contents of hello About() method with hello following:</span></span>

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. <span data-ttu-id="2de53-133">Kesme noktası toohello Merhaba sol kümesi `string message`... satır.</span><span class="sxs-lookup"><span data-stu-id="2de53-133">Set a breakpoint toohello left of hello `string message`... line.</span></span>
4. <span data-ttu-id="2de53-134">İsabet  **&lt;F5 >** toostart hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="2de53-134">Hit **&lt;F5>** toostart debugging.</span></span>
5. <span data-ttu-id="2de53-135">Sayfa toohit hakkında toohello isabetini gidin.</span><span class="sxs-lookup"><span data-stu-id="2de53-135">Navigate toohello About page toohit your breakpoint.</span></span>
6. <span data-ttu-id="2de53-136">TooVisual Studio tooview hello kesme geçin ve ileti hello değerini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="2de53-136">Switch tooVisual Studio tooview hello breakpoint, and inspect hello value of message.</span></span>

   ![][2]

## <a name="summary"></a><span data-ttu-id="2de53-137">Özet</span><span class="sxs-lookup"><span data-stu-id="2de53-137">Summary</span></span>
<span data-ttu-id="2de53-138">İle [Docker için Visual Studio 2015 Araçları](https://aka.ms/DockerToolsForVS), yerel olarak Docker kapsayıcısı içinde geliştirmenin hello üretim daha iyi çalışma hello verimliliği elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2de53-138">With [Visual Studio 2015 Tools for Docker](https://aka.ms/DockerToolsForVS), you can get hello productivity of working locally, with hello production realism of developing within a Docker container.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2de53-139">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="2de53-139">Troubleshooting</span></span>
[<span data-ttu-id="2de53-140">Visual Studio Docker geliştirme sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="2de53-140">Troubleshooting Visual Studio Docker Development</span></span>](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a><span data-ttu-id="2de53-141">Visual Studio, Windows ve Azure ile Docker hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="2de53-141">More about Docker with Visual Studio, Windows, and Azure</span></span>
* <span data-ttu-id="2de53-142">[Visual Studio için docker Araçları](http://aka.ms/dockertoolsforvs) -.NET Core kodunuzda bir kapsayıcı geliştirme</span><span class="sxs-lookup"><span data-stu-id="2de53-142">[Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) - Developing your .NET Core code in a container</span></span>
* <span data-ttu-id="2de53-143">[Visual Studio Team Services için docker Araçları](http://aka.ms/dockertoolsforvsts) - yapı ve docker kapsayıcıları dağıtın</span><span class="sxs-lookup"><span data-stu-id="2de53-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) - Build and Deploy docker containers</span></span>
* <span data-ttu-id="2de53-144">[Visual Studio Code için docker Araçları](http://aka.ms/dockertoolsforvscode) -daha fazla e2e senaryo gelen docker dosyalarını düzenlemek için dil Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="2de53-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) - Language services for editing docker files, with more e2e scenarios coming</span></span>
* <span data-ttu-id="2de53-145">[Windows kapsayıcı bilgileri](http://aka.ms/containers)-Windows Server ve Nano Server bilgileri</span><span class="sxs-lookup"><span data-stu-id="2de53-145">[Windows Container Information](http://aka.ms/containers)- Windows Server and Nano Server information</span></span>
* <span data-ttu-id="2de53-146">[Azure kapsayıcı hizmeti](https://azure.microsoft.com/services/container-service/) - [Azure kapsayıcı hizmeti içerik](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="2de53-146">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service Content](http://aka.ms/AzureContainerService)</span></span>
* <span data-ttu-id="2de53-147">Docker ile çalışmaya ilişkin daha fazla örnek için bkz: [Docker ile çalışma](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) hello gelen [tanıtımında](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="2de53-147">For more examples of working with Docker, see [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) from hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span> <span data-ttu-id="2de53-148">Merhaba tanıtımında demo öğesinden daha fazla quickstarts için bkz: [Azure geliştirici araçları hızlı başlangıç ipuçları](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="2de53-148">For more quickstarts from hello HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>

## <a name="various-docker-tools"></a><span data-ttu-id="2de53-149">Çeşitli Docker araçları</span><span class="sxs-lookup"><span data-stu-id="2de53-149">Various Docker tools</span></span>
[<span data-ttu-id="2de53-150">Bazı harika docker Araçlar (Steve Lasker'ın blogu)</span><span class="sxs-lookup"><span data-stu-id="2de53-150">Some great docker tools (Steve Lasker's blog)</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a><span data-ttu-id="2de53-151">İyi makaleler</span><span class="sxs-lookup"><span data-stu-id="2de53-151">Good articles</span></span>
[<span data-ttu-id="2de53-152">Giriş tooMicroservices NGINX gelen</span><span class="sxs-lookup"><span data-stu-id="2de53-152">Introduction tooMicroservices from NGINX</span></span>](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a><span data-ttu-id="2de53-153">Sunular</span><span class="sxs-lookup"><span data-stu-id="2de53-153">Presentations</span></span>
* [<span data-ttu-id="2de53-154">Steve Lasker: VS Las Vegas 2016 - Docker e2e Canlı</span><span class="sxs-lookup"><span data-stu-id="2de53-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e</span></span>](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [<span data-ttu-id="2de53-155">Yapı 2016 - Burada, adresindeki Demo @ giriş tooASP.NET çekirdek</span><span class="sxs-lookup"><span data-stu-id="2de53-155">Introduction tooASP.NET Core @ build 2016 - Where You At Demo</span></span>](https://channel9.msdn.com/Events/Build/2016/B810)
* [<span data-ttu-id="2de53-156">Kapsayıcılardaki Channel 9 .NET uygulamaları geliştirme</span><span class="sxs-lookup"><span data-stu-id="2de53-156">Developing .NET apps in containers, Channel 9</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
