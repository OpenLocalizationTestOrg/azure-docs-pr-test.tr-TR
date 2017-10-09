---
title: "aaaCreate bir ASP.NET web uygulamasına | Microsoft Docs"
description: "Nasıl hello varsayılan ASP.NET dağıtarak toorun web uygulamaları Azure App Service'te web uygulaması hakkında bilgi edinin."
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: eec916b3c32b6c8b68083177938c5c822a9782b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a><span data-ttu-id="73760-103">Azure’da ASP.NET web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="73760-103">Create an ASP.NET web app in Azure</span></span>

<span data-ttu-id="73760-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="73760-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="73760-105">Bu hızlı başlangıç gösterir nasıl toodeploy ilk ASP.NET web uygulaması tooAzure Web uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="73760-105">This quickstart shows how toodeploy your first ASP.NET web app tooAzure Web Apps.</span></span> <span data-ttu-id="73760-106">İşlemi tamamladığınızda bir App Service planı ve dağıtılmış web uygulaması ile Azure web uygulamasından oluşan kaynak grubunuz olacaktır.</span><span class="sxs-lookup"><span data-stu-id="73760-106">When you're finished, you'll have a resource group that consists of an App Service plan and an Azure web app with a deployed web application.</span></span>

<span data-ttu-id="73760-107">Bu hızlı başlangıç eylem Hello video toosee izleyin ve ardından izleyin hello adımları kendiniz toopublish ilk .NET uygulamanızı Azure üzerinde.</span><span class="sxs-lookup"><span data-stu-id="73760-107">Watch hello video toosee this quickstart in action and then follow hello steps yourself toopublish your first .NET app on Azure.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a><span data-ttu-id="73760-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="73760-108">Prerequisites</span></span>

<span data-ttu-id="73760-109">toocomplete Bu öğretici:</span><span class="sxs-lookup"><span data-stu-id="73760-109">toocomplete this tutorial:</span></span>

* <span data-ttu-id="73760-110">Yükleme [Visual Studio 2017](https://www.visualstudio.com/downloads/) iş yükleri aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="73760-110">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello following workloads:</span></span>
    - <span data-ttu-id="73760-111">**ASP.NET ve web geliştirme**</span><span class="sxs-lookup"><span data-stu-id="73760-111">**ASP.NET and web development**</span></span>
    - <span data-ttu-id="73760-112">**Azure geliştirme**</span><span class="sxs-lookup"><span data-stu-id="73760-112">**Azure development**</span></span>

    ![ASP.NET ve web geliştirme ile Azure geliştirme (Web ve Bulut altında)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="73760-114">ASP.NET web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="73760-114">Create an ASP.NET web app</span></span>

<span data-ttu-id="73760-115">Visual Studio'da **Dosya > Yeni > Proje**’yi seçerek bir proje oluşturun.</span><span class="sxs-lookup"><span data-stu-id="73760-115">In Visual Studio, create a project by selecting **File > New > Project**.</span></span> 

<span data-ttu-id="73760-116">Merhaba, **yeni proje** iletişim kutusunda **Visual C# > Web > ASP.NET Web uygulaması (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="73760-116">In hello **New Project** dialog, select **Visual C# > Web > ASP.NET Web Application (.NET Framework)**.</span></span>

<span data-ttu-id="73760-117">Ad Merhaba uygulaması _myFirstAzureWebApp_ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="73760-117">Name hello application _myFirstAzureWebApp_, and then select **OK**.</span></span>
   
![Yeni Proje iletişim kutusu](./media/app-service-web-get-started-dotnet/new-project.png)

<span data-ttu-id="73760-119">ASP.NET web uygulaması tooAzure herhangi bir türde dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73760-119">You can deploy any type of ASP.NET web app tooAzure.</span></span> <span data-ttu-id="73760-120">Bu Hızlı Başlangıç için hello seçin **MVC** şablonu ve kimlik doğrulama çok ayarlandığından emin olun**doğrulaması yok**.</span><span class="sxs-lookup"><span data-stu-id="73760-120">For this quickstart, select hello **MVC** template, and make sure authentication is set too**No Authentication**.</span></span>
      
<span data-ttu-id="73760-121">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="73760-121">Select **OK**.</span></span>

![Yeni ASP.NET Projesi iletişim kutusu](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

<span data-ttu-id="73760-123">Başlangıç menüsünden seçin **hata ayıklama > hata ayıklama olmadan Başlat** toorun hello web uygulamasını yerel olarak.</span><span class="sxs-lookup"><span data-stu-id="73760-123">From hello menu, select **Debug > Start without Debugging** toorun hello web app locally.</span></span>

![Uygulamayı yerel olarak çalıştırma](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-tooazure"></a><span data-ttu-id="73760-125">TooAzure yayımlama</span><span class="sxs-lookup"><span data-stu-id="73760-125">Publish tooAzure</span></span>

<span data-ttu-id="73760-126">Merhaba, **Çözüm Gezgini**, sağ hello **myFirstAzureWebApp** proje ve seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="73760-126">In hello **Solution Explorer**, right-click hello **myFirstAzureWebApp** project and select **Publish**.</span></span>

![Çözüm Gezgini'nden yayımlama](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

<span data-ttu-id="73760-128">**Microsoft Azure App Service**’in seçili olduğundan emin olup **Yayımla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="73760-128">Make sure that **Microsoft Azure App Service** is selected and select **Publish**.</span></span>

![Projeye genel bakış sayfasından yayımlama](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

<span data-ttu-id="73760-130">Merhaba açılır **App Service Oluştur** iletişim kutusu, Azure'da tüm hello gerekli Azure kaynaklarını toorun hello ASP.NET web uygulaması oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="73760-130">This opens hello **Create App Service** dialog, which helps you create all hello necessary Azure resources toorun hello ASP.NET web app in Azure.</span></span>

## <a name="sign-in-tooazure"></a><span data-ttu-id="73760-131">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="73760-131">Sign in tooAzure</span></span>

<span data-ttu-id="73760-132">Merhaba, **App Service Oluştur** iletişim kutusunda **Hesap Ekle**ve tooyour Azure aboneliği oturum açın.</span><span class="sxs-lookup"><span data-stu-id="73760-132">In hello **Create App Service** dialog, select **Add an account**, and sign in tooyour Azure subscription.</span></span> <span data-ttu-id="73760-133">Zaten oturum açtınız, hello içeren select hello hesabı hello açılır abonelikten istenen.</span><span class="sxs-lookup"><span data-stu-id="73760-133">If you're already signed in, select hello account containing hello desired subscription from hello dropdown.</span></span>

> [!NOTE]
> <span data-ttu-id="73760-134">Zaten oturum açtıysanız **Oluştur** öğesini henüz seçmeyin.</span><span class="sxs-lookup"><span data-stu-id="73760-134">If you're already signed in, don't select **Create** yet.</span></span>
>
>
   
![İçinde tooAzure oturum](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a><span data-ttu-id="73760-136">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="73760-136">Create a resource group</span></span>

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

<span data-ttu-id="73760-137">Sonraki çok**kaynak grubu**seçin **yeni**.</span><span class="sxs-lookup"><span data-stu-id="73760-137">Next too**Resource Group**, select **New**.</span></span>

<span data-ttu-id="73760-138">Ad hello kaynak grubu **myResourceGroup** seçip **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="73760-138">Name hello resource group **myResourceGroup** and select **OK**.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="73760-139">App Service planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="73760-139">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="73760-140">Sonraki çok**App Service planı**seçin **yeni**.</span><span class="sxs-lookup"><span data-stu-id="73760-140">Next too**App Service Plan**, select **New**.</span></span> 

<span data-ttu-id="73760-141">Merhaba, **App Service planı Yapılandır** iletişim kutusunda, hello ekran aşağıdaki hello tablosundaki hello ayarları kullanın.</span><span class="sxs-lookup"><span data-stu-id="73760-141">In hello **Configure App Service Plan** dialog, use hello settings in hello table following hello screenshot.</span></span>

![App Service planı oluşturma](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| <span data-ttu-id="73760-143">Ayar</span><span class="sxs-lookup"><span data-stu-id="73760-143">Setting</span></span> | <span data-ttu-id="73760-144">Önerilen Değer</span><span class="sxs-lookup"><span data-stu-id="73760-144">Suggested Value</span></span> | <span data-ttu-id="73760-145">Açıklama</span><span class="sxs-lookup"><span data-stu-id="73760-145">Description</span></span> |
|-|-|-|
|<span data-ttu-id="73760-146">App Service Planı</span><span class="sxs-lookup"><span data-stu-id="73760-146">App Service Plan</span></span>| <span data-ttu-id="73760-147">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="73760-147">myAppServicePlan</span></span> | <span data-ttu-id="73760-148">Merhaba uygulama hizmeti plan adı.</span><span class="sxs-lookup"><span data-stu-id="73760-148">Name of hello App Service plan.</span></span> |
| <span data-ttu-id="73760-149">Konum</span><span class="sxs-lookup"><span data-stu-id="73760-149">Location</span></span> | <span data-ttu-id="73760-150">Batı Avrupa</span><span class="sxs-lookup"><span data-stu-id="73760-150">West Europe</span></span> | <span data-ttu-id="73760-151">Merhaba veri merkezi başlangıç web uygulaması barındırıldığı.</span><span class="sxs-lookup"><span data-stu-id="73760-151">hello datacenter where hello web app is hosted.</span></span> |
| <span data-ttu-id="73760-152">Boyut</span><span class="sxs-lookup"><span data-stu-id="73760-152">Size</span></span> | <span data-ttu-id="73760-153">Ücretsiz</span><span class="sxs-lookup"><span data-stu-id="73760-153">Free</span></span> | <span data-ttu-id="73760-154">[Fiyatlandırma katmanı](https://azure.microsoft.com/pricing/details/app-service/), barındırma özelliklerini belirler.</span><span class="sxs-lookup"><span data-stu-id="73760-154">[Pricing tier](https://azure.microsoft.com/pricing/details/app-service/) determines hosting features.</span></span> |

<span data-ttu-id="73760-155">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="73760-155">Select **OK**.</span></span>

## <a name="create-and-publish-hello-web-app"></a><span data-ttu-id="73760-156">Oluşturma ve yayımlama hello web uygulaması</span><span class="sxs-lookup"><span data-stu-id="73760-156">Create and publish hello web app</span></span>

<span data-ttu-id="73760-157">İçinde **Web uygulaması adı**, benzersiz uygulama adını yazın (geçerli karakterler `a-z`, `0-9`, ve `-`), veya hello otomatik olarak oluşturulan benzersiz adı kabul edin.</span><span class="sxs-lookup"><span data-stu-id="73760-157">In **Web App Name**, type a unique app name (valid characters are `a-z`, `0-9`, and `-`), or accept hello automatically generated unique name.</span></span> <span data-ttu-id="73760-158">Merhaba web uygulaması Hello URL'sidir `http://<app_name>.azurewebsites.net`, burada `<app_name>` web uygulaması adı.</span><span class="sxs-lookup"><span data-stu-id="73760-158">hello URL of hello web app is `http://<app_name>.azurewebsites.net`, where `<app_name>` is your web app name.</span></span>

<span data-ttu-id="73760-159">Seçin **oluşturma** toostart hello Azure kaynakları oluşturma.</span><span class="sxs-lookup"><span data-stu-id="73760-159">Select **Create** toostart creating hello Azure resources.</span></span>

![Web uygulaması adını yapılandırma](./media/app-service-web-get-started-dotnet/web-app-name.png)

<span data-ttu-id="73760-161">Merhaba Sihirbaz tamamlandıktan sonra hello ASP.NET web uygulaması tooAzure yayımlar ve ardından başlatır hello varsayılan tarayıcıda uygulama hello.</span><span class="sxs-lookup"><span data-stu-id="73760-161">Once hello wizard completes, it publishes hello ASP.NET web app tooAzure, and then launches hello app in hello default browser.</span></span>

![Azure’da yayımlanmış ASP.NET web uygulaması](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

<span data-ttu-id="73760-163">Hello belirtilen hello web uygulaması adı [oluşturma ve yayımlama adım](#create-and-publish-the-web-app) URL öneki hello biçiminde hello olarak kullanılan `http://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="73760-163">hello web app name specified in hello [create and publish step](#create-and-publish-the-web-app) is used as hello URL prefix in hello format `http://<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="73760-164">Tebrikler, ASP.NET web uygulamanız Azure App Service’te çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="73760-164">Congratulations, your ASP.NET web app is running live in Azure App Service.</span></span>

## <a name="update-hello-app-and-redeploy"></a><span data-ttu-id="73760-165">Güncelleştirme hello uygulama ve yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="73760-165">Update hello app and redeploy</span></span>

<span data-ttu-id="73760-166">Merhaba gelen **Çözüm Gezgini**, açık _Views\Home\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="73760-166">From hello **Solution Explorer**, open _Views\Home\Index.cshtml_.</span></span>

<span data-ttu-id="73760-167">Hello bulur `<div class="jumbotron">` HTML etiketi hello yukarıya yakın ve koddan hello ile Merhaba tüm öğeyi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="73760-167">Find hello `<div class="jumbotron">` HTML tag near hello top, and replace hello entire element with hello following code:</span></span>

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how toodeploy a .NET app tooAzure App Service.</p>
</div>
```

<span data-ttu-id="73760-168">tooredeploy tooAzure, sağ hello **myFirstAzureWebApp** proje **Çözüm Gezgini** seçip **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="73760-168">tooredeploy tooAzure, right-click hello **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span></span>

<span data-ttu-id="73760-169">Merhaba, yayımlama sayfası, seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="73760-169">In hello publish page, select **Publish**.</span></span>

<span data-ttu-id="73760-170">Yayımlama tamamlandığında Visual Studio Başlangıç web uygulaması bir tarayıcı toohello URL başlatır.</span><span class="sxs-lookup"><span data-stu-id="73760-170">When publishing completes, Visual Studio launches a browser toohello URL of hello web app.</span></span>

![Azure’da güncelleştirilmiş ASP.NET web uygulaması](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-hello-azure-web-app"></a><span data-ttu-id="73760-172">Hello Azure web uygulaması yönetme</span><span class="sxs-lookup"><span data-stu-id="73760-172">Manage hello Azure web app</span></span>

<span data-ttu-id="73760-173">Toohello Git <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="73760-173">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app.</span></span>

<span data-ttu-id="73760-174">Merhaba sol menüden seçin **uygulama hizmetleri**ve ardından, Azure web uygulamanızın hello adı seçin.</span><span class="sxs-lookup"><span data-stu-id="73760-174">From hello left menu, select **App Services**, and then select hello name of your Azure web app.</span></span>

![Portal Gezinti tooAzure web uygulaması](./media/app-service-web-get-started-dotnet/access-portal.png)

<span data-ttu-id="73760-176">Web uygulamanızın Genel Bakış sayfasını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="73760-176">You see your web app's Overview page.</span></span> <span data-ttu-id="73760-177">Buradan göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73760-177">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Azure portalında App Service dikey penceresi](./media/app-service-web-get-started-dotnet/web-app-blade.png)

<span data-ttu-id="73760-179">Merhaba soldaki menüden, uygulamanızı yapılandırmak için farklı sayfaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="73760-179">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="73760-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="73760-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="73760-181">SQL Veritabanı ile ASP.NET</span><span class="sxs-lookup"><span data-stu-id="73760-181">ASP.NET with SQL Database</span></span>](app-service-web-tutorial-dotnet-sqldatabase.md)
