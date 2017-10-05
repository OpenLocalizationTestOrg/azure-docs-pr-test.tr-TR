---
title: "Yerel bir Docker kapsayıcısı uygulamalarında hata ayıklama | Microsoft Docs"
description: "Yerel bir Docker kapsayıcısı içinde çalışan bir uygulamayı değiştirmek öğrenin, düzenleme ve yenileme aracılığıyla kapsayıcı yenileyin ve hata ayıklama kesme noktaları ayarlayın"
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
ms.openlocfilehash: fcd58736d8915a61683a416fb9bf3892ba7b7bd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a><span data-ttu-id="988f9-103">Yerel Docker kapsayıcısındaki uygulamalar için hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="988f9-103">Debugging apps in a local Docker container</span></span>
## <a name="overview"></a><span data-ttu-id="988f9-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="988f9-104">Overview</span></span>
<span data-ttu-id="988f9-105">Docker için Visual Studio Araçları, geliştirmek ve uygulamanızda yerel olarak Linux Docker kapsayıcısı doğrulamak için tutarlı bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="988f9-105">The Visual Studio Tools for Docker provides a consistent way to develop in and validate your application locally in a Linux Docker container.</span></span>
<span data-ttu-id="988f9-106">Kapsayıcı bir kod değişikliği yaptığınız her zaman yeniden başlatmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="988f9-106">You don't have to restart the container each time you make a code change.</span></span>
<span data-ttu-id="988f9-107">Bu makalede "Düzenle ve Yenile" özelliği bir yerel Docker kapsayıcısı bir ASP.NET çekirdek Web uygulaması başlatın, gerekli değişiklikleri yapın ve bu değişiklikleri görmek için tarayıcıyı yenilemek için nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="988f9-107">This article illustrates how to use the "Edit and Refresh" feature to start an ASP.NET Core Web app in a local Docker container, make any necessary changes, and then refresh the browser to see those changes.</span></span>
<span data-ttu-id="988f9-108">Bu makalede ayrıca hata ayıklama kesme noktalarını ayarlama gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="988f9-108">This article also shows you how to set breakpoints for debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="988f9-109">Windows kapsayıcı desteği gelecekteki bir sürümde geliyor</span><span class="sxs-lookup"><span data-stu-id="988f9-109">Windows Container support will be coming in a future release</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="988f9-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="988f9-110">Prerequisites</span></span>
<span data-ttu-id="988f9-111">Aşağıdaki araçları yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="988f9-111">The following tools must be installed.</span></span>

* [<span data-ttu-id="988f9-112">Visual Studio en son sürümü</span><span class="sxs-lookup"><span data-stu-id="988f9-112">Latest version of Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="988f9-113">Microsoft ASP.NET Core 1.0 SDK'sı</span><span class="sxs-lookup"><span data-stu-id="988f9-113">Microsoft ASP.NET Core 1.0 SDK</span></span>](https://go.microsoft.com/fwlink/?LinkID=809122)

<span data-ttu-id="988f9-114">Yerel olarak Docker kapsayıcıları çalıştırmak için bir yerel docker istemci gerekir.</span><span class="sxs-lookup"><span data-stu-id="988f9-114">To run Docker containers locally, you'll need a local docker client.</span></span>
<span data-ttu-id="988f9-115">Kullanabilirsiniz [Docker araç](https://www.docker.com/products/docker-toolbox)devre dışı bırakılması Hyper-V gerektirir veya kullanabilirsiniz [Windows için Docker](https://www.docker.com/get-docker), Hyper-V kullanır ve Windows 10 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="988f9-115">You can use the [Docker Toolbox](https://www.docker.com/products/docker-toolbox), which requires Hyper-V to be disabled, or you can use [Docker for Windows](https://www.docker.com/get-docker), which uses Hyper-V, and requires Windows 10.</span></span>

<span data-ttu-id="988f9-116">Docker araç kullanıyorsanız, gerekecektir [Docker istemciyi Yapılandırma](vs-azure-tools-docker-setup.md)</span><span class="sxs-lookup"><span data-stu-id="988f9-116">If using Docker Toolbox, you'll need to [configure the Docker client](vs-azure-tools-docker-setup.md)</span></span>

## <a name="1-create-a-web-app"></a><span data-ttu-id="988f9-117">1. Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="988f9-117">1. Create a web app</span></span>
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="988f9-118">2. Docker desteği ekleme</span><span class="sxs-lookup"><span data-stu-id="988f9-118">2. Add Docker support</span></span>
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a><span data-ttu-id="988f9-119">3. Kod ve yenileme Düzenle</span><span class="sxs-lookup"><span data-stu-id="988f9-119">3. Edit your code and refresh</span></span>
<span data-ttu-id="988f9-120">Hızlı bir şekilde değişiklikleri yinelemek için bir kapsayıcı içindeki uygulamanızı başlatın ve değişiklik yapmak IIS Express ile olduğu gibi bunları görüntüleme devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="988f9-120">To quickly iterate changes, you can start your application within a container, and continue to make changes, viewing them as you would with IIS Express.</span></span>

1. <span data-ttu-id="988f9-121">Çözüm yapılandırma kümesi `Debug` ve basın  **&lt;CTRL + F5 >** docker görüntünüzü oluşturmak ve yerel olarak çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="988f9-121">Set the Solution Configuration to `Debug` and press **&lt;CTRL + F5>** to build your docker image and run it locally.</span></span>

    <span data-ttu-id="988f9-122">Kapsayıcı görüntü oluşturulduğundan ve Docker kapsayıcısı içinde çalışan sonra Visual Studio, varsayılan tarayıcıda Web uygulamasını başlatır.</span><span class="sxs-lookup"><span data-stu-id="988f9-122">Once the container image has been built and is running in a Docker container, Visual Studio will launch the Web app in your default browser.</span></span>
    <span data-ttu-id="988f9-123">Microsoft Edge tarayıcı kullanıyorsanız veya aksi halde hatalar varsa, bkz: [sorun giderme](vs-azure-tools-docker-troubleshooting-docker-errors.md) bölümü.</span><span class="sxs-lookup"><span data-stu-id="988f9-123">If you are using the Microsoft Edge browser or otherwise have errors, see [Troubleshooting](vs-azure-tools-docker-troubleshooting-docker-errors.md) section.</span></span>
2. <span data-ttu-id="988f9-124">Bizim değişiklik yapmak için burada yapacağız olan hakkında sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="988f9-124">Go to the About page, which is where we're going to make our changes.</span></span>
3. <span data-ttu-id="988f9-125">Visual Studio'ya dönmek ve açık `Views\Home\About.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="988f9-125">Return to Visual Studio and open `Views\Home\About.cshtml`.</span></span>
4. <span data-ttu-id="988f9-126">Aşağıdaki HTML içeriğini dosyanın sonuna ekleyin ve değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="988f9-126">Add the following HTML content to the end of the file and save the changes.</span></span>

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. <span data-ttu-id="988f9-127">.NET derleme tamamlandığında ve bu satırları görmek için çıkış penceresine görüntüleme, tarayıcınızın geri geçin ve hakkında sayfayı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="988f9-127">Viewing the output window, when the .NET build is completed and you see these lines, switch back to your browser and refresh the About page.</span></span>

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C to shut down
   ```
6. <span data-ttu-id="988f9-128">Yaptığınız değişiklikleri uygulandı!</span><span class="sxs-lookup"><span data-stu-id="988f9-128">Your changes have been applied!</span></span>

## <a name="4-debug-with-breakpoints"></a><span data-ttu-id="988f9-129">4. Kesme noktaları ile hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="988f9-129">4. Debug with breakpoints</span></span>
<span data-ttu-id="988f9-130">Genellikle, değişiklikleri daha ayrıntılı denetleme, Visual Studio hata ayıklama özelliklerini yararlanarak gerekir.</span><span class="sxs-lookup"><span data-stu-id="988f9-130">Often, changes will need further inspection, leveraging the debugging features of Visual Studio.</span></span>

1. <span data-ttu-id="988f9-131">Visual Studio'ya geri dönün ve açın`Controllers\HomeController.cs`</span><span class="sxs-lookup"><span data-stu-id="988f9-131">Return to Visual Studio and open `Controllers\HomeController.cs`</span></span>
2. <span data-ttu-id="988f9-132">About() yöntemi içeriğini aşağıdakiyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="988f9-132">Replace the contents of the About() method with the following:</span></span>

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. <span data-ttu-id="988f9-133">Sol tarafında bir kesme noktası belirleyerek `string message`... satır.</span><span class="sxs-lookup"><span data-stu-id="988f9-133">Set a breakpoint to the left of the `string message`... line.</span></span>
4. <span data-ttu-id="988f9-134">İsabet  **&lt;F5 >** hata ayıklama başlatılamıyor.</span><span class="sxs-lookup"><span data-stu-id="988f9-134">Hit **&lt;F5>** to start debugging.</span></span>
5. <span data-ttu-id="988f9-135">Kesme noktası isabet hakkında sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="988f9-135">Navigate to the About page to hit your breakpoint.</span></span>
6. <span data-ttu-id="988f9-136">Kesme noktası görüntülemek için Visual Studio geçin ve ileti değerini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="988f9-136">Switch to Visual Studio to view the breakpoint, and inspect the value of message.</span></span>

   ![][2]

## <a name="summary"></a><span data-ttu-id="988f9-137">Özet</span><span class="sxs-lookup"><span data-stu-id="988f9-137">Summary</span></span>
<span data-ttu-id="988f9-138">İle [Docker için Visual Studio 2015 Araçları](https://aka.ms/DockerToolsForVS), Docker kapsayıcısı içinde geliştirmenin üretim daha iyi ile yerel olarak çalışan verimliliği elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="988f9-138">With [Visual Studio 2015 Tools for Docker](https://aka.ms/DockerToolsForVS), you can get the productivity of working locally, with the production realism of developing within a Docker container.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="988f9-139">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="988f9-139">Troubleshooting</span></span>
[<span data-ttu-id="988f9-140">Visual Studio Docker geliştirme sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="988f9-140">Troubleshooting Visual Studio Docker Development</span></span>](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a><span data-ttu-id="988f9-141">Visual Studio, Windows ve Azure ile Docker hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="988f9-141">More about Docker with Visual Studio, Windows, and Azure</span></span>
* <span data-ttu-id="988f9-142">[Visual Studio için docker Araçları](http://aka.ms/dockertoolsforvs) -.NET Core kodunuzda bir kapsayıcı geliştirme</span><span class="sxs-lookup"><span data-stu-id="988f9-142">[Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) - Developing your .NET Core code in a container</span></span>
* <span data-ttu-id="988f9-143">[Visual Studio Team Services için docker Araçları](http://aka.ms/dockertoolsforvsts) - yapı ve docker kapsayıcıları dağıtın</span><span class="sxs-lookup"><span data-stu-id="988f9-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) - Build and Deploy docker containers</span></span>
* <span data-ttu-id="988f9-144">[Visual Studio Code için docker Araçları](http://aka.ms/dockertoolsforvscode) -daha fazla e2e senaryo gelen docker dosyalarını düzenlemek için dil Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="988f9-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) - Language services for editing docker files, with more e2e scenarios coming</span></span>
* <span data-ttu-id="988f9-145">[Windows kapsayıcı bilgileri](http://aka.ms/containers)-Windows Server ve Nano Server bilgileri</span><span class="sxs-lookup"><span data-stu-id="988f9-145">[Windows Container Information](http://aka.ms/containers)- Windows Server and Nano Server information</span></span>
* <span data-ttu-id="988f9-146">[Azure kapsayıcı hizmeti](https://azure.microsoft.com/services/container-service/) - [Azure kapsayıcı hizmeti içerik](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="988f9-146">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service Content](http://aka.ms/AzureContainerService)</span></span>
* <span data-ttu-id="988f9-147">Docker ile çalışmaya ilişkin daha fazla örnek için bkz: [Docker ile çalışma](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) gelen [tanıtımında](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="988f9-147">For more examples of working with Docker, see [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) from the [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span> <span data-ttu-id="988f9-148">HealthClinic.biz tanıtımından daha fazla hızlı başlangıç ipuçları için bkz. [Azure Geliştirici Araçları Hızlı Başlangıç İpuçları](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="988f9-148">For more quickstarts from the HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>

## <a name="various-docker-tools"></a><span data-ttu-id="988f9-149">Çeşitli Docker araçları</span><span class="sxs-lookup"><span data-stu-id="988f9-149">Various Docker tools</span></span>
[<span data-ttu-id="988f9-150">Bazı harika docker Araçlar (Steve Lasker'ın blogu)</span><span class="sxs-lookup"><span data-stu-id="988f9-150">Some great docker tools (Steve Lasker's blog)</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a><span data-ttu-id="988f9-151">İyi makaleler</span><span class="sxs-lookup"><span data-stu-id="988f9-151">Good articles</span></span>
[<span data-ttu-id="988f9-152">Mikro giriş NGINX gelen</span><span class="sxs-lookup"><span data-stu-id="988f9-152">Introduction to Microservices from NGINX</span></span>](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a><span data-ttu-id="988f9-153">Sunular</span><span class="sxs-lookup"><span data-stu-id="988f9-153">Presentations</span></span>
* [<span data-ttu-id="988f9-154">Steve Lasker: VS Las Vegas 2016 - Docker e2e Canlı</span><span class="sxs-lookup"><span data-stu-id="988f9-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e</span></span>](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [<span data-ttu-id="988f9-155">ASP.NET Core giriş yapı 2016 - Burada, adresindeki Demo @</span><span class="sxs-lookup"><span data-stu-id="988f9-155">Introduction to ASP.NET Core @ build 2016 - Where You At Demo</span></span>](https://channel9.msdn.com/Events/Build/2016/B810)
* [<span data-ttu-id="988f9-156">Kapsayıcılardaki Channel 9 .NET uygulamaları geliştirme</span><span class="sxs-lookup"><span data-stu-id="988f9-156">Developing .NET apps in containers, Channel 9</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
