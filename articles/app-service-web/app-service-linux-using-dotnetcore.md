---
title: "Linux üzerinde Web uygulamasında .NET Core kullanın | Microsoft Docs"
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
ms.openlocfilehash: 9226dfb90e52ac2cae2cfc4af7c0705a93f56b44
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a><span data-ttu-id="5f1ea-104">.NET Core Linux Azure web uygulaması kullanın</span><span class="sxs-lookup"><span data-stu-id="5f1ea-104">Use .NET Core in an Azure web app on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="5f1ea-105">[Web uygulaması](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) düzeyde ölçeklenebilir, otomatik olarak düzeltme eki uygulama web barındırma hizmeti Linux işletim sistemini kullanarak Linux'ta sağlar.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-105">[Web App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) on Linux provides a highly scalable, self-patching web hosting service using the Linux operating system.</span></span> <span data-ttu-id="5f1ea-106">Bu öğretici nasıl oluşturulacağını gösteren adım adım yönergeler içeren bir [.NET Core](https://docs.microsoft.com/aspnet/core/) Linux Azure web uygulaması üzerinde uygulama.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-106">This tutorial contains step-by-step instructions showing how to create a [.NET Core](https://docs.microsoft.com/aspnet/core/) app on Azure web app on Linux.</span></span> 

![Linux üzerinde Web Uygulaması][10]

<span data-ttu-id="5f1ea-108">Mac, Windows veya Linux makinesi kullanarak aşağıdaki adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f1ea-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5f1ea-109">Prerequisites</span></span> ##

<span data-ttu-id="5f1ea-110">Bu öğreticiyi tamamlamak için:</span><span class="sxs-lookup"><span data-stu-id="5f1ea-110">To complete this tutorial:</span></span> 

* <span data-ttu-id="5f1ea-111">Yükleme [.NET Core SDK](https://www.microsoft.com/net/download/core).</span><span class="sxs-lookup"><span data-stu-id="5f1ea-111">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core).</span></span>
* <span data-ttu-id="5f1ea-112">Yükleme [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="5f1ea-112">Install [Git](https://git-scm.com/downloads).</span></span>

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a><span data-ttu-id="5f1ea-113">Yerel bir .NET Core uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f1ea-113">Create a local .NET Core application</span></span> ##

<span data-ttu-id="5f1ea-114">Yeni bir terminal oturumu başlatın.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-114">Start a new terminal session.</span></span> <span data-ttu-id="5f1ea-115">Adlı bir dizin oluşturun `hellodotnetcore`ve geçerli dizini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-115">Create a directory named `hellodotnetcore`, and change the current directory to it.</span></span> <span data-ttu-id="5f1ea-116">Ardından aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="5f1ea-116">Then type the following:</span></span> 

```
dotnet new web
``` 

  <span data-ttu-id="5f1ea-117">Bu komut dosyaları üç oluşturur (*hellodotnetcore.csproj*, *Program.cs*, ve *haline*) ve bir boş klasör (*wwwroot /*) Geçerli dizinin altında.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-117">This command creates three files (*hellodotnetcore.csproj*, *Program.cs*, and *Startup.cs*) and one empty folder (*wwwroot/*) under the current directory.</span></span> <span data-ttu-id="5f1ea-118">İçeriği `.csproj` dosya, aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="5f1ea-118">The content of `.csproj` file should look like the following:</span></span> 

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

<span data-ttu-id="5f1ea-119">Bu uygulama bir web uygulaması olduğundan, bir ASP.NET Core paketine başvuru otomatik olarak eklenen *hellodotnetcore.csproj* dosya.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-119">Since this app is a web application, a reference to an ASP.NET Core package was automatically added to the *hellodotnetcore.csproj* file.</span></span> <span data-ttu-id="5f1ea-120">Paketin sürüm numarası Seçilen framework göre ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-120">The version number of the package is set according to the chosen framework.</span></span> <span data-ttu-id="5f1ea-121">.NET Core 1.1 kullanılmakta olduğu için bu örnek ASP.NET Core sürüm 1.1.2 başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-121">This example is referencing ASP.NET Core version 1.1.2 because .NET Core 1.1 is used.</span></span>

## <a name="build-and-test-the-application-locally"></a><span data-ttu-id="5f1ea-122">Derleme ve uygulamayı yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="5f1ea-122">Build and test the application locally</span></span> ##

<span data-ttu-id="5f1ea-123">Derleme ve .NET Core uygulamanızı çalıştırma `dotnet restore` ve ardından komut `dotnet run` aşağıda gösterildiği gibi komut:</span><span class="sxs-lookup"><span data-stu-id="5f1ea-123">You can build and run your .NET Core app with the `dotnet restore` command followed by the `dotnet run` command, as shown here:</span></span>

```
dotnet restore
dotnet run
```


<span data-ttu-id="5f1ea-124">Uygulama başlatıldığında, uygulama bir bağlantı noktasında gelen istekleri dinlediği belirten bir ileti görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-124">When the application starts, it displays a message indicating the app is listening to incoming requests at a port.</span></span> 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

<span data-ttu-id="5f1ea-125">Göz atarak test `http://localhost:5000/` tarayıcınızla.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-125">Test it by browsing to `http://localhost:5000/` with your browser.</span></span> <span data-ttu-id="5f1ea-126">Her şeyi düzgün çalışır, "Hello World!" konusuna bakın</span><span class="sxs-lookup"><span data-stu-id="5f1ea-126">If everything works fine, you see "Hello World!"</span></span> <span data-ttu-id="5f1ea-127">Sonuç metin olarak.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-127">as the result text.</span></span>

![Tarayıcı ile test][7]

## <a name="create-a-net-core-app-in-the-azure-portal"></a><span data-ttu-id="5f1ea-129">Bir .NET oluşturma Azure portalında çekirdek uygulama</span><span class="sxs-lookup"><span data-stu-id="5f1ea-129">Create a .NET Core app in the Azure Portal</span></span> ##

<span data-ttu-id="5f1ea-130">Önce bir boş web uygulaması oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-130">First you need to create an empty web app.</span></span> <span data-ttu-id="5f1ea-131">Oturum [Azure portal](https://portal.azure.com/) ve yeni bir [Linux üzerinde Web uygulaması](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="5f1ea-131">Log in to the [Azure portal](https://portal.azure.com/) and create a new [Web App on Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span></span>

![Bir web uygulaması oluşturma][1]

<span data-ttu-id="5f1ea-133">Zaman **oluşturma** sayfası açılır, web uygulamanız hakkında ayrıntılar verilmektedir:</span><span class="sxs-lookup"><span data-stu-id="5f1ea-133">When the **Create** page opens, provide details about your web app:</span></span>

![Bir .NET çekirdeği çalışma zamanı yığını seçme][2]

<span data-ttu-id="5f1ea-135">Doldurmak için bir kılavuz olarak aşağıdaki tabloyu kullanın **oluşturma** sayfasında sonra seçin **Tamam** ve **oluşturma** uygulama oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-135">Use the following table as a guide to fill out the **Create** page, then select **OK** and **Create** to create the app.</span></span>

| <span data-ttu-id="5f1ea-136">Ayar</span><span class="sxs-lookup"><span data-stu-id="5f1ea-136">Setting</span></span>      | <span data-ttu-id="5f1ea-137">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="5f1ea-137">Suggested value</span></span>  | <span data-ttu-id="5f1ea-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5f1ea-138">Description</span></span>                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| <span data-ttu-id="5f1ea-139">Uygulama adı</span><span class="sxs-lookup"><span data-stu-id="5f1ea-139">App name</span></span> | <span data-ttu-id="5f1ea-140">hellodotnetcore</span><span class="sxs-lookup"><span data-stu-id="5f1ea-140">hellodotnetcore</span></span>  | <span data-ttu-id="5f1ea-141">Uygulamanızın adı.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-141">The name of your app.</span></span> <span data-ttu-id="5f1ea-142">Bu ad benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-142">This name must be unique.</span></span> |
| <span data-ttu-id="5f1ea-143">Abonelik</span><span class="sxs-lookup"><span data-stu-id="5f1ea-143">Subscription</span></span> | <span data-ttu-id="5f1ea-144">Var olan bir abonelik seçin</span><span class="sxs-lookup"><span data-stu-id="5f1ea-144">Choose an existing subscription</span></span> | <span data-ttu-id="5f1ea-145">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-145">The Azure subscription.</span></span> |
| <span data-ttu-id="5f1ea-146">Kaynak Grubu</span><span class="sxs-lookup"><span data-stu-id="5f1ea-146">Resource Group</span></span> | <span data-ttu-id="5f1ea-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5f1ea-147">myResourceGroup</span></span> |  <span data-ttu-id="5f1ea-148">Web uygulaması içeren Azure kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-148">The Azure resource group to contain the web app.</span></span> |
| <span data-ttu-id="5f1ea-149">App Service Planı</span><span class="sxs-lookup"><span data-stu-id="5f1ea-149">App Service Plan</span></span> | <span data-ttu-id="5f1ea-150">Var olan uygulama hizmeti planı adı</span><span class="sxs-lookup"><span data-stu-id="5f1ea-150">Existing App Service Plan name</span></span> |  <span data-ttu-id="5f1ea-151">Uygulama hizmeti planı.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-151">The App Service plan.</span></span>  |
| <span data-ttu-id="5f1ea-152">Kapsayıcı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5f1ea-152">Configure Container</span></span> | <span data-ttu-id="5f1ea-153">.NET core 1.1</span><span class="sxs-lookup"><span data-stu-id="5f1ea-153">.NET Core 1.1</span></span> | <span data-ttu-id="5f1ea-154">Bu web uygulaması için kapsayıcı türü: yerleşik, Docker veya özel kayıt defteri.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-154">The type of container for this web app: Built-in, Docker, or Private registry.</span></span> |
| <span data-ttu-id="5f1ea-155">Görüntü kaynağı</span><span class="sxs-lookup"><span data-stu-id="5f1ea-155">Image source</span></span>  | <span data-ttu-id="5f1ea-156">Yerleşik</span><span class="sxs-lookup"><span data-stu-id="5f1ea-156">Built-in</span></span>  |  <span data-ttu-id="5f1ea-157">Görüntünün kaynağı.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-157">The source of the image.</span></span> |
| <span data-ttu-id="5f1ea-158">Çalışma zamanı yığını</span><span class="sxs-lookup"><span data-stu-id="5f1ea-158">Runtime Stack</span></span>  | <span data-ttu-id="5f1ea-159">.NET core 1.1</span><span class="sxs-lookup"><span data-stu-id="5f1ea-159">.NET Core 1.1</span></span>  | <span data-ttu-id="5f1ea-160">Çalışma zamanı yığını ve sürüm.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-160">The runtime stack and version.</span></span>  |

## <a name="deploy-your-application-via-git"></a><span data-ttu-id="5f1ea-161">Git aracılığıyla uygulamanızı dağıtma</span><span class="sxs-lookup"><span data-stu-id="5f1ea-161">Deploy your application via Git</span></span> ##

<span data-ttu-id="5f1ea-162">Azure App Service Web uygulaması Linux'ta .NET Core uygulamayı dağıtmak için Git kullanın.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-162">Use Git to deploy the .NET Core application to Azure App Service Web App on Linux.</span></span>

<span data-ttu-id="5f1ea-163">Yeni Azure web uygulaması zaten yapılandırılmış Git dağıtımı içeriyor.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-163">The new Azure web app already has Git deployment configured.</span></span> <span data-ttu-id="5f1ea-164">Web uygulaması adı ekledikten sonra aşağıdaki URL'sine giderek Git dağıtım URL'si bulacaksınız:</span><span class="sxs-lookup"><span data-stu-id="5f1ea-164">You will find the Git deployment URL by navigating to the following URL after inserting your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

<span data-ttu-id="5f1ea-165">Git URL'si, web uygulaması adınıza göre aşağıdaki biçime sahiptir:</span><span class="sxs-lookup"><span data-stu-id="5f1ea-165">The Git URL has the following form based on your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

<span data-ttu-id="5f1ea-166">Azure web uygulamanızı yerel uygulamayı dağıtmak için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5f1ea-166">Run the following commands to deploy the local application to your Azure web app:</span></span> 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="5f1ea-167">Altındaki tüm dosyaları anında gerekmez *bin /* veya *obj /* dizinleri uygulamanın kaynak dosyaları için Azure basıldığında uygulamanızı bulutta oluşturulduğundan.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-167">You don't need to push any files under *bin/* or *obj/* directories because your application is built in the cloud when the application's source files are pushed to Azure.</span></span> <span data-ttu-id="5f1ea-168">Derleme işlemi tamamlandıktan sonra ikili dosyaları uygulamanın dizininde içine kopyalanır */home/site/wwwroot/*.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-168">After the build process is complete, binary files are copied into the application's directory at */home/site/wwwroot/*.</span></span>

<span data-ttu-id="5f1ea-169">Uzaktan dağıtım işlemlerini Başarı Raporu onaylayın.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-169">Confirm that the remote deployment operations report success.</span></span> <span data-ttu-id="5f1ea-170">Gönderme işlemleri paket çözümleme itibaren sürebilir ve derleme bulutta çalışan işlemi olabilir.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-170">Push operations may take a while since package resolution and build process run in the cloud.</span></span> <span data-ttu-id="5f1ea-171">Olanları dosyaları kopyalandığını belirten dahil olmak üzere, birkaç durum iletilerini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-171">You will see several status messages, including ones stating that files have been copied.</span></span> <span data-ttu-id="5f1ea-172">Çıktı aşağıdakine benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="5f1ea-172">The output should look similar to the following:</span></span>

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
To https://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

<span data-ttu-id="5f1ea-173">Dağıtım tamamlandıktan sonra web uygulamanızı etkili olması için dağıtım için yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-173">Once the deployment has completed, restart your web app for the deployment to take effect.</span></span> <span data-ttu-id="5f1ea-174">Bunu yapmak için Azure Portalı'na gidin ve gidin **genel bakış** sayfası, web uygulamanızın.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-174">To do this, go to the Azure portal and navigate to the **Overview** page of your web app.</span></span> <span data-ttu-id="5f1ea-175">Seçin **yeniden** sayfasının düğmesini.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-175">Select the **Restart** button in the page.</span></span> <span data-ttu-id="5f1ea-176">Açılan pencerede görüntülenir, seçin **Evet** onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="5f1ea-176">When a popup window shows up, select **Yes** to confirm.</span></span> <span data-ttu-id="5f1ea-177">Ardından, aşağıda gösterildiği gibi web uygulamanızın göz atabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5f1ea-177">You can then browse your web app, as shown here:</span></span>

![Azure App Service'e Linux üzerinde dağıtılan .NET Core uygulama gözatma][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="5f1ea-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5f1ea-179">Next steps</span></span>
* [<span data-ttu-id="5f1ea-180">Azure App Service Web uygulaması Linux SSS</span><span class="sxs-lookup"><span data-stu-id="5f1ea-180">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
