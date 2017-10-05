---
title: "Azure’da ASP.NET web uygulaması oluşturma | Microsoft Docs"
description: "Varsayılan ASP.NET web uygulamasını dağıtarak Azure App Service'te web uygulamalarını çalıştırma hakkında bilgi edinin."
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
ms.openlocfilehash: 0f0035f6fef03ddcbb500b78f3445ced5b749808
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a><span data-ttu-id="3e915-103">Azure’da ASP.NET web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="3e915-103">Create an ASP.NET web app in Azure</span></span>

<span data-ttu-id="3e915-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="3e915-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="3e915-105">Bu hızlı başlangıçta, Azure Web Apps’e ilk ASP.NET web uygulamanızı dağıtma işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3e915-105">This quickstart shows how to deploy your first ASP.NET web app to Azure Web Apps.</span></span> <span data-ttu-id="3e915-106">İşlemi tamamladığınızda bir App Service planı ve dağıtılmış web uygulaması ile Azure web uygulamasından oluşan kaynak grubunuz olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3e915-106">When you're finished, you'll have a resource group that consists of an App Service plan and an Azure web app with a deployed web application.</span></span>

<span data-ttu-id="3e915-107">Bu hızlı başlangıcı uygulamada görmek için videoyu izleyin ve sonra adımları kendiniz uygulayarak Azure’da ilk .NET uygulamanızı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="3e915-107">Watch the video to see this quickstart in action and then follow the steps yourself to publish your first .NET app on Azure.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a><span data-ttu-id="3e915-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3e915-108">Prerequisites</span></span>

<span data-ttu-id="3e915-109">Bu öğreticiyi tamamlamak için:</span><span class="sxs-lookup"><span data-stu-id="3e915-109">To complete this tutorial:</span></span>

* <span data-ttu-id="3e915-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/)’yi aşağıdaki iş yükleri ile yükleyin:</span><span class="sxs-lookup"><span data-stu-id="3e915-110">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span></span>
    - <span data-ttu-id="3e915-111">**ASP.NET ve web geliştirme**</span><span class="sxs-lookup"><span data-stu-id="3e915-111">**ASP.NET and web development**</span></span>
    - <span data-ttu-id="3e915-112">**Azure geliştirme**</span><span class="sxs-lookup"><span data-stu-id="3e915-112">**Azure development**</span></span>

    ![ASP.NET ve web geliştirme ile Azure geliştirme (Web ve Bulut altında)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="3e915-114">ASP.NET web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="3e915-114">Create an ASP.NET web app</span></span>

<span data-ttu-id="3e915-115">Visual Studio'da **Dosya > Yeni > Proje**’yi seçerek bir proje oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3e915-115">In Visual Studio, create a project by selecting **File > New > Project**.</span></span> 

<span data-ttu-id="3e915-116">**Yeni Proje** iletişim kutusunda **Visual C# > Web > ASP.NET Web Uygulaması (.NET Framework)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="3e915-116">In the **New Project** dialog, select **Visual C# > Web > ASP.NET Web Application (.NET Framework)**.</span></span>

<span data-ttu-id="3e915-117">Uygulamayı _myFirstAzureWebApp_ olarak adlandırın ve ardından **Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="3e915-117">Name the application _myFirstAzureWebApp_, and then select **OK**.</span></span>
   
![Yeni Proje iletişim kutusu](./media/app-service-web-get-started-dotnet/new-project.png)

<span data-ttu-id="3e915-119">Azure’a herhangi bir türde ASP.NET web uygulaması dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e915-119">You can deploy any type of ASP.NET web app to Azure.</span></span> <span data-ttu-id="3e915-120">Bu hızlı başlangıçta **MVC** şablonunu seçin ve kimlik doğrulamasının **Kimlik Doğrulaması Yok** olarak ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="3e915-120">For this quickstart, select the **MVC** template, and make sure authentication is set to **No Authentication**.</span></span>
      
<span data-ttu-id="3e915-121">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="3e915-121">Select **OK**.</span></span>

![Yeni ASP.NET Projesi iletişim kutusu](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

<span data-ttu-id="3e915-123">Menüden **Hata Ayıkla > Hata Ayıklamadan Başla**’yı seçerek web uygulamasını yerel olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3e915-123">From the menu, select **Debug > Start without Debugging** to run the web app locally.</span></span>

![Uygulamayı yerel olarak çalıştırma](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-to-azure"></a><span data-ttu-id="3e915-125">Azure’da Yayımlama</span><span class="sxs-lookup"><span data-stu-id="3e915-125">Publish to Azure</span></span>

<span data-ttu-id="3e915-126">**Çözüm Gezgini**’nde **myFirstAzureWebApp** projesine sağ tıklayıp **Yayımla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="3e915-126">In the **Solution Explorer**, right-click the **myFirstAzureWebApp** project and select **Publish**.</span></span>

![Çözüm Gezgini'nden yayımlama](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

<span data-ttu-id="3e915-128">**Microsoft Azure App Service**’in seçili olduğundan emin olup **Yayımla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="3e915-128">Make sure that **Microsoft Azure App Service** is selected and select **Publish**.</span></span>

![Projeye genel bakış sayfasından yayımlama](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

<span data-ttu-id="3e915-130">Bu işlem, ASP.NET web uygulamasını Azure’da çalıştırmak için gereken tüm Azure kaynaklarını oluşturmanıza yardımcı olan **App Service Oluştur** iletişim kutusunu açar.</span><span class="sxs-lookup"><span data-stu-id="3e915-130">This opens the **Create App Service** dialog, which helps you create all the necessary Azure resources to run the ASP.NET web app in Azure.</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="3e915-131">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="3e915-131">Sign in to Azure</span></span>

<span data-ttu-id="3e915-132">**App Service Oluştur** iletişim kutusunda **Hesap ekle**’yi seçin ve Azure aboneliğinizde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3e915-132">In the **Create App Service** dialog, select **Add an account**, and sign in to your Azure subscription.</span></span> <span data-ttu-id="3e915-133">Oturumunuz zaten açıksa, açılan menüden istediğiniz aboneliği içeren hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="3e915-133">If you're already signed in, select the account containing the desired subscription from the dropdown.</span></span>

> [!NOTE]
> <span data-ttu-id="3e915-134">Zaten oturum açtıysanız **Oluştur** öğesini henüz seçmeyin.</span><span class="sxs-lookup"><span data-stu-id="3e915-134">If you're already signed in, don't select **Create** yet.</span></span>
>
>
   
![Azure'da oturum açma](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a><span data-ttu-id="3e915-136">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="3e915-136">Create a resource group</span></span>

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

<span data-ttu-id="3e915-137">**Kaynak Grubu**’nun yanındaki **Yeni** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="3e915-137">Next to **Resource Group**, select **New**.</span></span>

<span data-ttu-id="3e915-138">Kaynak grubunuzu **myResourceGroup** olarak adlandırıp **Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="3e915-138">Name the resource group **myResourceGroup** and select **OK**.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="3e915-139">App Service planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3e915-139">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="3e915-140">**App Service Planı**’nın yanındaki **Yeni**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="3e915-140">Next to **App Service Plan**, select **New**.</span></span> 

<span data-ttu-id="3e915-141">**App Service Planını Yapılandır** iletişim kutusunda, ekran görüntüsünü izleyerek tablodaki ayarları kullanın.</span><span class="sxs-lookup"><span data-stu-id="3e915-141">In the **Configure App Service Plan** dialog, use the settings in the table following the screenshot.</span></span>

![App Service planı oluşturma](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| <span data-ttu-id="3e915-143">Ayar</span><span class="sxs-lookup"><span data-stu-id="3e915-143">Setting</span></span> | <span data-ttu-id="3e915-144">Önerilen Değer</span><span class="sxs-lookup"><span data-stu-id="3e915-144">Suggested Value</span></span> | <span data-ttu-id="3e915-145">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3e915-145">Description</span></span> |
|-|-|-|
|<span data-ttu-id="3e915-146">App Service Planı</span><span class="sxs-lookup"><span data-stu-id="3e915-146">App Service Plan</span></span>| <span data-ttu-id="3e915-147">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="3e915-147">myAppServicePlan</span></span> | <span data-ttu-id="3e915-148">App Service planının adı.</span><span class="sxs-lookup"><span data-stu-id="3e915-148">Name of the App Service plan.</span></span> |
| <span data-ttu-id="3e915-149">Konum</span><span class="sxs-lookup"><span data-stu-id="3e915-149">Location</span></span> | <span data-ttu-id="3e915-150">Batı Avrupa</span><span class="sxs-lookup"><span data-stu-id="3e915-150">West Europe</span></span> | <span data-ttu-id="3e915-151">Web uygulamasının barındırıldığı veri merkezi.</span><span class="sxs-lookup"><span data-stu-id="3e915-151">The datacenter where the web app is hosted.</span></span> |
| <span data-ttu-id="3e915-152">Boyut</span><span class="sxs-lookup"><span data-stu-id="3e915-152">Size</span></span> | <span data-ttu-id="3e915-153">Ücretsiz</span><span class="sxs-lookup"><span data-stu-id="3e915-153">Free</span></span> | <span data-ttu-id="3e915-154">[Fiyatlandırma katmanı](https://azure.microsoft.com/pricing/details/app-service/), barındırma özelliklerini belirler.</span><span class="sxs-lookup"><span data-stu-id="3e915-154">[Pricing tier](https://azure.microsoft.com/pricing/details/app-service/) determines hosting features.</span></span> |

<span data-ttu-id="3e915-155">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="3e915-155">Select **OK**.</span></span>

## <a name="create-and-publish-the-web-app"></a><span data-ttu-id="3e915-156">Web uygulaması oluşturma ve yayımlama</span><span class="sxs-lookup"><span data-stu-id="3e915-156">Create and publish the web app</span></span>

<span data-ttu-id="3e915-157">**Web Uygulaması Adı**’na benzersiz bir ad girin (geçerli karakterler `a-z`, `0-9` ve `-` karakterleridir) veya otomatik olarak oluşturulan adı kabul edin.</span><span class="sxs-lookup"><span data-stu-id="3e915-157">In **Web App Name**, type a unique app name (valid characters are `a-z`, `0-9`, and `-`), or accept the automatically generated unique name.</span></span> <span data-ttu-id="3e915-158">Web uygulamasının URL'si `http://<app_name>.azurewebsites.net` şeklindedir; burada `<app_name>`, web uygulamanızın adıdır.</span><span class="sxs-lookup"><span data-stu-id="3e915-158">The URL of the web app is `http://<app_name>.azurewebsites.net`, where `<app_name>` is your web app name.</span></span>

<span data-ttu-id="3e915-159">Azure kaynaklarını oluşturmaya başlamak için **Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="3e915-159">Select **Create** to start creating the Azure resources.</span></span>

![Web uygulaması adını yapılandırma](./media/app-service-web-get-started-dotnet/web-app-name.png)

<span data-ttu-id="3e915-161">Sihirbaz tamamlandıktan sonra ASP.NET web uygulamasını Azure’da yayımlar ve ardından uygulamayı varsayılan tarayıcıda başlatır.</span><span class="sxs-lookup"><span data-stu-id="3e915-161">Once the wizard completes, it publishes the ASP.NET web app to Azure, and then launches the app in the default browser.</span></span>

![Azure’da yayımlanmış ASP.NET web uygulaması](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

<span data-ttu-id="3e915-163">[Oluşturma ve yayımlama adımında](#create-and-publish-the-web-app) belirtilen web uygulaması adı `http://<app_name>.azurewebsites.net` biçiminde URL ön eki olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3e915-163">The web app name specified in the [create and publish step](#create-and-publish-the-web-app) is used as the URL prefix in the format `http://<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="3e915-164">Tebrikler, ASP.NET web uygulamanız Azure App Service’te çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="3e915-164">Congratulations, your ASP.NET web app is running live in Azure App Service.</span></span>

## <a name="update-the-app-and-redeploy"></a><span data-ttu-id="3e915-165">Uygulamayı güncelleştirme ve yeniden dağıtma</span><span class="sxs-lookup"><span data-stu-id="3e915-165">Update the app and redeploy</span></span>

<span data-ttu-id="3e915-166">**Çözüm Gezgini** menüsünden _Görünümler\Giriş\Index.cshtml_ dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="3e915-166">From the **Solution Explorer**, open _Views\Home\Index.cshtml_.</span></span>

<span data-ttu-id="3e915-167">Üst kısımda `<div class="jumbotron">` HTML etiketini bulun ve tüm öğeyi aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="3e915-167">Find the `<div class="jumbotron">` HTML tag near the top, and replace the entire element with the following code:</span></span>

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how to deploy a .NET app to Azure App Service.</p>
</div>
```

<span data-ttu-id="3e915-168">Azure’a yeniden dağıtmak için **Çözüm Gezgini**’nde **myFirstAzureWebApp** projesine sağ tıklayıp **Yayımla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="3e915-168">To redeploy to Azure, right-click the **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span></span>

<span data-ttu-id="3e915-169">Yayımlama sayfasında **Yayımla**'yı seçin.</span><span class="sxs-lookup"><span data-stu-id="3e915-169">In the publish page, select **Publish**.</span></span>

<span data-ttu-id="3e915-170">Yayımlama tamamlandığında Visual Studio, web uygulamasının URL’si ile bir tarayıcı başlatır.</span><span class="sxs-lookup"><span data-stu-id="3e915-170">When publishing completes, Visual Studio launches a browser to the URL of the web app.</span></span>

![Azure’da güncelleştirilmiş ASP.NET web uygulaması](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-the-azure-web-app"></a><span data-ttu-id="3e915-172">Azure web uygulamasını yönetme</span><span class="sxs-lookup"><span data-stu-id="3e915-172">Manage the Azure web app</span></span>

<span data-ttu-id="3e915-173">Web uygulamasını yönetmek için <a href="https://portal.azure.com" target="_blank">Azure portalına</a> gidin.</span><span class="sxs-lookup"><span data-stu-id="3e915-173">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app.</span></span>

<span data-ttu-id="3e915-174">Sol menüden **Uygulama Hizmetleri**'ni ve ardından Azure web uygulamanızın adını seçin.</span><span class="sxs-lookup"><span data-stu-id="3e915-174">From the left menu, select **App Services**, and then select the name of your Azure web app.</span></span>

![Portaldan Azure web uygulamasına gitme](./media/app-service-web-get-started-dotnet/access-portal.png)

<span data-ttu-id="3e915-176">Web uygulamanızın Genel Bakış sayfasını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3e915-176">You see your web app's Overview page.</span></span> <span data-ttu-id="3e915-177">Buradan göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e915-177">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Azure portalında App Service dikey penceresi](./media/app-service-web-get-started-dotnet/web-app-blade.png)

<span data-ttu-id="3e915-179">Soldaki menü, uygulamanızı yapılandırmak için farklı sayfalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="3e915-179">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="3e915-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3e915-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3e915-181">SQL Veritabanı ile ASP.NET</span><span class="sxs-lookup"><span data-stu-id="3e915-181">ASP.NET with SQL Database</span></span>](app-service-web-tutorial-dotnet-sqldatabase.md)
