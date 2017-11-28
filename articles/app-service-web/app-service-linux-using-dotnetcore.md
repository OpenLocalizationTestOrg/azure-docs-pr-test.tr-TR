---
title: ".NET Core Linux üzerinde Web uygulamasında aaaUse | Microsoft Docs"
description: ".NET Core Linux üzerinde Web uygulaması kullanın."
keywords: "Azure uygulama hizmeti, web uygulaması, dotnet, çekirdek, linux, oss"
services: app-service
documentationCenter: 
authors: michimune, rachelappel
manager: erikre
editor: 
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: aelnably;wesmc;mikono;rachelap
ms.openlocfilehash: 9b7fb7185dff2c99ed88e7937d455177504937b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a><span data-ttu-id="fe59a-104">.NET Core Linux Azure web uygulaması kullanın</span><span class="sxs-lookup"><span data-stu-id="fe59a-104">Use .NET Core in an Azure web app on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="fe59a-105">[Web uygulaması](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) Linux'ta hello Linux işletim sistemi kullanan bir düzeyde ölçeklenebilir, otomatik olarak düzeltme eki uygulama web barındırma hizmeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="fe59a-105">[Web App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) on Linux provides a highly scalable, self-patching web hosting service using hello Linux operating system.</span></span> <span data-ttu-id="fe59a-106">Bu öğretici gösteren adım adım yönergeler içerir nasıl toocreate bir [.NET Core](https://docs.microsoft.com/aspnet/core/) Linux Azure web uygulaması üzerinde uygulama.</span><span class="sxs-lookup"><span data-stu-id="fe59a-106">This tutorial contains step-by-step instructions showing how toocreate a [.NET Core](https://docs.microsoft.com/aspnet/core/) app on Azure web app on Linux.</span></span> 

![Linux üzerinde Web Uygulaması][10]

<span data-ttu-id="fe59a-108">Mac, Windows veya Linux makine kullanarak aşağıda hello adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe59a-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe59a-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fe59a-109">Prerequisites</span></span> ##

<span data-ttu-id="fe59a-110">toocomplete Bu öğretici:</span><span class="sxs-lookup"><span data-stu-id="fe59a-110">toocomplete this tutorial:</span></span> 

* <span data-ttu-id="fe59a-111">Merhaba yüklemek [.NET Core SDK](https://www.microsoft.com/net/download/core).</span><span class="sxs-lookup"><span data-stu-id="fe59a-111">Install hello [.NET Core SDK](https://www.microsoft.com/net/download/core).</span></span>
* <span data-ttu-id="fe59a-112">Yükleme [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="fe59a-112">Install [Git](https://git-scm.com/downloads).</span></span>

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a><span data-ttu-id="fe59a-113">Yerel bir .NET Core uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe59a-113">Create a local .NET Core application</span></span> ##

<span data-ttu-id="fe59a-114">Yeni bir terminal oturumu başlatın.</span><span class="sxs-lookup"><span data-stu-id="fe59a-114">Start a new terminal session.</span></span> <span data-ttu-id="fe59a-115">Adlı bir dizin oluşturun `hellodotnetcore`ve hello geçerli dizin tooit değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fe59a-115">Create a directory named `hellodotnetcore`, and change hello current directory tooit.</span></span> <span data-ttu-id="fe59a-116">Merhaba aşağıdakileri yazın:</span><span class="sxs-lookup"><span data-stu-id="fe59a-116">Then type hello following:</span></span> 

```
dotnet new web
``` 

  <span data-ttu-id="fe59a-117">Bu komut dosyaları üç oluşturur (*hellodotnetcore.csproj*, *Program.cs*, ve *haline*) ve bir boş klasör (*wwwroot /*) Merhaba geçerli dizinin altında.</span><span class="sxs-lookup"><span data-stu-id="fe59a-117">This command creates three files (*hellodotnetcore.csproj*, *Program.cs*, and *Startup.cs*) and one empty folder (*wwwroot/*) under hello current directory.</span></span> <span data-ttu-id="fe59a-118">Merhaba içeriğini `.csproj` dosya hello aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="fe59a-118">hello content of `.csproj` file should look like hello following:</span></span> 

```xml
  <!-- Empty lines are omitted. -->

  <Project Sdk="Microsoft.NET.Sdk.Web">
        <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
        <Folder Include="wwwroot\" />
        </ItemGroup>
        <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore" Version="1.1.2" />
        </ItemGroup>
  </Project>
```

<span data-ttu-id="fe59a-119">Bu uygulama bir web uygulaması olduğundan, ASP.NET Core paketi olan otomatik olarak bir başvuru tooan toohello eklenen *hellodotnetcore.csproj* dosya.</span><span class="sxs-lookup"><span data-stu-id="fe59a-119">Since this app is a web application, a reference tooan ASP.NET Core package was automatically added toohello *hellodotnetcore.csproj* file.</span></span> <span data-ttu-id="fe59a-120">Merhaba paketin Hello sürüm numarası framework seçilen toohello göre ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="fe59a-120">hello version number of hello package is set according toohello chosen framework.</span></span> <span data-ttu-id="fe59a-121">.NET Core 1.1 kullanılmakta olduğu için bu örnek ASP.NET Core sürüm 1.1.2 başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="fe59a-121">This example is referencing ASP.NET Core version 1.1.2 because .NET Core 1.1 is used.</span></span>

## <a name="build-and-test-hello-application-locally"></a><span data-ttu-id="fe59a-122">Derleme ve hello uygulama yerel olarak test</span><span class="sxs-lookup"><span data-stu-id="fe59a-122">Build and test hello application locally</span></span> ##

<span data-ttu-id="fe59a-123">Derleme ve .NET Core uygulamanızı hello ile çalıştırma `dotnet restore` hello tarafından izlenen komutu `dotnet run` aşağıda gösterildiği gibi komut:</span><span class="sxs-lookup"><span data-stu-id="fe59a-123">You can build and run your .NET Core app with hello `dotnet restore` command followed by hello `dotnet run` command, as shown here:</span></span>

```
dotnet restore
dotnet run
```


<span data-ttu-id="fe59a-124">Merhaba uygulaması başlatıldığında hello uygulama tooincoming isteklerini bir bağlantı noktasında dinleme belirten bir ileti görüntüler.</span><span class="sxs-lookup"><span data-stu-id="fe59a-124">When hello application starts, it displays a message indicating hello app is listening tooincoming requests at a port.</span></span> 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C tooshut down.
```

<span data-ttu-id="fe59a-125">Çok göz atarak test`http://localhost:5000/` tarayıcınızla.</span><span class="sxs-lookup"><span data-stu-id="fe59a-125">Test it by browsing too`http://localhost:5000/` with your browser.</span></span> <span data-ttu-id="fe59a-126">Her şeyi düzgün çalışır, "Hello World!" konusuna bakın</span><span class="sxs-lookup"><span data-stu-id="fe59a-126">If everything works fine, you see "Hello World!"</span></span> <span data-ttu-id="fe59a-127">Merhaba sonucu metin olarak.</span><span class="sxs-lookup"><span data-stu-id="fe59a-127">as hello result text.</span></span>

![Tarayıcı ile test][7]

## <a name="create-a-net-core-app-in-hello-azure-portal"></a><span data-ttu-id="fe59a-129">Hello Azure portalı bir .NET Core uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe59a-129">Create a .NET Core app in hello Azure Portal</span></span> ##

<span data-ttu-id="fe59a-130">İlk toocreate boş web uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe59a-130">First you need toocreate an empty web app.</span></span> <span data-ttu-id="fe59a-131">İçinde toohello oturum [Azure portal](https://portal.azure.com/) ve yeni bir [Linux üzerinde Web uygulaması](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="fe59a-131">Log in toohello [Azure portal](https://portal.azure.com/) and create a new [Web App on Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span></span>

![Bir web uygulaması oluşturma][1]

<span data-ttu-id="fe59a-133">Ne zaman hello **oluşturma** sayfası açılır, web uygulamanız hakkında ayrıntılar verilmektedir:</span><span class="sxs-lookup"><span data-stu-id="fe59a-133">When hello **Create** page opens, provide details about your web app:</span></span>

![Bir .NET çekirdeği çalışma zamanı yığını seçme][2]

<span data-ttu-id="fe59a-135">Kullanım hello aşağıdaki tablo Kılavuzu toofill hello çıkış olarak **oluşturma** sayfasında sonra seçin **Tamam** ve **oluşturma** toocreate hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="fe59a-135">Use hello following table as a guide toofill out hello **Create** page, then select **OK** and **Create** toocreate hello app.</span></span>

| <span data-ttu-id="fe59a-136">Ayar</span><span class="sxs-lookup"><span data-stu-id="fe59a-136">Setting</span></span>      | <span data-ttu-id="fe59a-137">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="fe59a-137">Suggested value</span></span>  | <span data-ttu-id="fe59a-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fe59a-138">Description</span></span>                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| <span data-ttu-id="fe59a-139">Uygulama adı</span><span class="sxs-lookup"><span data-stu-id="fe59a-139">App name</span></span> | <span data-ttu-id="fe59a-140">hellodotnetcore</span><span class="sxs-lookup"><span data-stu-id="fe59a-140">hellodotnetcore</span></span>  | <span data-ttu-id="fe59a-141">Merhaba, uygulamanızın adıdır.</span><span class="sxs-lookup"><span data-stu-id="fe59a-141">hello name of your app.</span></span> <span data-ttu-id="fe59a-142">Bu ad benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fe59a-142">This name must be unique.</span></span> |
| <span data-ttu-id="fe59a-143">Abonelik</span><span class="sxs-lookup"><span data-stu-id="fe59a-143">Subscription</span></span> | <span data-ttu-id="fe59a-144">Var olan bir abonelik seçin</span><span class="sxs-lookup"><span data-stu-id="fe59a-144">Choose an existing subscription</span></span> | <span data-ttu-id="fe59a-145">Hello Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="fe59a-145">hello Azure subscription.</span></span> |
| <span data-ttu-id="fe59a-146">Kaynak Grubu</span><span class="sxs-lookup"><span data-stu-id="fe59a-146">Resource Group</span></span> | <span data-ttu-id="fe59a-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fe59a-147">myResourceGroup</span></span> |  <span data-ttu-id="fe59a-148">Hello Azure kaynak grubu toocontain hello web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="fe59a-148">hello Azure resource group toocontain hello web app.</span></span> |
| <span data-ttu-id="fe59a-149">App Service Planı</span><span class="sxs-lookup"><span data-stu-id="fe59a-149">App Service Plan</span></span> | <span data-ttu-id="fe59a-150">Var olan uygulama hizmeti planı adı</span><span class="sxs-lookup"><span data-stu-id="fe59a-150">Existing App Service Plan name</span></span> |  <span data-ttu-id="fe59a-151">Uygulama hizmeti planı hello.</span><span class="sxs-lookup"><span data-stu-id="fe59a-151">hello App Service plan.</span></span>  |
| <span data-ttu-id="fe59a-152">Kapsayıcı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fe59a-152">Configure Container</span></span> | <span data-ttu-id="fe59a-153">.NET core 1.1</span><span class="sxs-lookup"><span data-stu-id="fe59a-153">.NET Core 1.1</span></span> | <span data-ttu-id="fe59a-154">Bu web uygulaması için kapsayıcı türü Hello: yerleşik, Docker veya özel kayıt defteri.</span><span class="sxs-lookup"><span data-stu-id="fe59a-154">hello type of container for this web app: Built-in, Docker, or Private registry.</span></span> |
| <span data-ttu-id="fe59a-155">Görüntü kaynağı</span><span class="sxs-lookup"><span data-stu-id="fe59a-155">Image source</span></span>  | <span data-ttu-id="fe59a-156">Yerleşik</span><span class="sxs-lookup"><span data-stu-id="fe59a-156">Built-in</span></span>  |  <span data-ttu-id="fe59a-157">Merhaba görüntü Hello kaynağı.</span><span class="sxs-lookup"><span data-stu-id="fe59a-157">hello source of hello image.</span></span> |
| <span data-ttu-id="fe59a-158">Çalışma zamanı yığını</span><span class="sxs-lookup"><span data-stu-id="fe59a-158">Runtime Stack</span></span>  | <span data-ttu-id="fe59a-159">.NET core 1.1</span><span class="sxs-lookup"><span data-stu-id="fe59a-159">.NET Core 1.1</span></span>  | <span data-ttu-id="fe59a-160">Merhaba çalışma zamanı yığını ve sürüm.</span><span class="sxs-lookup"><span data-stu-id="fe59a-160">hello runtime stack and version.</span></span>  |

## <a name="deploy-your-application-via-git"></a><span data-ttu-id="fe59a-161">Git aracılığıyla uygulamanızı dağıtma</span><span class="sxs-lookup"><span data-stu-id="fe59a-161">Deploy your application via Git</span></span> ##

<span data-ttu-id="fe59a-162">Git toodeploy hello .NET Core uygulama tooAzure App Service Web uygulaması Linux'ta kullanın.</span><span class="sxs-lookup"><span data-stu-id="fe59a-162">Use Git toodeploy hello .NET Core application tooAzure App Service Web App on Linux.</span></span>

<span data-ttu-id="fe59a-163">yapılandırılmış Git dağıtımı Hello yeni Azure web uygulaması zaten var.</span><span class="sxs-lookup"><span data-stu-id="fe59a-163">hello new Azure web app already has Git deployment configured.</span></span> <span data-ttu-id="fe59a-164">Web uygulaması adı ekledikten sonra URL aşağıdaki toohello giderek hello Git dağıtım URL'si bulacaksınız:</span><span class="sxs-lookup"><span data-stu-id="fe59a-164">You will find hello Git deployment URL by navigating toohello following URL after inserting your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

<span data-ttu-id="fe59a-165">Merhaba Git URL'si, web uygulaması adınıza göre form aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="fe59a-165">hello Git URL has hello following form based on your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

<span data-ttu-id="fe59a-166">Aşağıdaki komutları toodeploy hello yerel uygulama tooyour Azure web uygulaması hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fe59a-166">Run hello following commands toodeploy hello local application tooyour Azure web app:</span></span> 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="fe59a-167">Altındaki tüm dosyalar toopush gerekmeyen *bin /* veya *obj /* dizinleri uygulamanızı hello bulutta oluşturulduğundan zaman hello uygulamanın kaynak dosyaları tooAzure gönderilir.</span><span class="sxs-lookup"><span data-stu-id="fe59a-167">You don't need toopush any files under *bin/* or *obj/* directories because your application is built in hello cloud when hello application's source files are pushed tooAzure.</span></span> <span data-ttu-id="fe59a-168">Merhaba oluşturma işlemi tamamlandıktan sonra ikili dosyaları hello uygulamanın dizininde içine kopyalanır */home/site/wwwroot/*.</span><span class="sxs-lookup"><span data-stu-id="fe59a-168">After hello build process is complete, binary files are copied into hello application's directory at */home/site/wwwroot/*.</span></span>

<span data-ttu-id="fe59a-169">Merhaba uzak dağıtım işlemlerini Başarı Raporu onaylayın.</span><span class="sxs-lookup"><span data-stu-id="fe59a-169">Confirm that hello remote deployment operations report success.</span></span> <span data-ttu-id="fe59a-170">Gönderme işlemleri paket çözümleme itibaren sürebilir ve derleme hello bulutta çalışan işlemi olabilir.</span><span class="sxs-lookup"><span data-stu-id="fe59a-170">Push operations may take a while since package resolution and build process run in hello cloud.</span></span> <span data-ttu-id="fe59a-171">Olanları dosyaları kopyalandığını belirten dahil olmak üzere, birkaç durum iletilerini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="fe59a-171">You will see several status messages, including ones stating that files have been copied.</span></span> <span data-ttu-id="fe59a-172">Merhaba çıkış benzer toohello aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="fe59a-172">hello output should look similar toohello following:</span></span>

```bash
/* some output has been removed for brevity */
remote: Copying file: 'System.Net.Websockets.dll' 
remote: Copying file: 'System.Runtime.CompilerServices.Unsafe.dll' 
remote: Copying file: 'System.Runtime.Serialization.Primitives.dll' 
remote: Copying file: 'System.Text.Encodings.Web.dll' 
remote: Copying file: 'hellodotnetcore.deps.json' 
remote: Copying file: 'hellodotnetcore.dll' 
remote: Omitting next output lines...
remote: Finished successfully.
remote: Running post deployment commands...
remote: Deployment successful.
toohttps://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

<span data-ttu-id="fe59a-173">Merhaba dağıtım tamamlandıktan sonra web uygulamanız hello dağıtım tootake etkisi için yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="fe59a-173">Once hello deployment has completed, restart your web app for hello deployment tootake effect.</span></span> <span data-ttu-id="fe59a-174">toodo bunu toohello Azure portalına gidin ve toohello gidin **genel bakış** sayfası, web uygulamanızın.</span><span class="sxs-lookup"><span data-stu-id="fe59a-174">toodo this, go toohello Azure portal and navigate toohello **Overview** page of your web app.</span></span> <span data-ttu-id="fe59a-175">Select hello **yeniden** hello sayfasında düğmesini.</span><span class="sxs-lookup"><span data-stu-id="fe59a-175">Select hello **Restart** button in hello page.</span></span> <span data-ttu-id="fe59a-176">Açılan pencerede görüntülenir, seçin **Evet** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="fe59a-176">When a popup window shows up, select **Yes** tooconfirm.</span></span> <span data-ttu-id="fe59a-177">Ardından, aşağıda gösterildiği gibi web uygulamanızın göz atabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fe59a-177">You can then browse your web app, as shown here:</span></span>

![Uygulama tooAzure uygulama hizmeti Linux üzerinde dağıtılan .NET Core gözatma][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="fe59a-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fe59a-179">Next steps</span></span>
* [<span data-ttu-id="fe59a-180">Azure App Service Web uygulaması Linux SSS</span><span class="sxs-lookup"><span data-stu-id="fe59a-180">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
