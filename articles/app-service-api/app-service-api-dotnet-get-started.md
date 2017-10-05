---
title: "App Service’te API Apps’i ve ASP.NET’i kullanmaya başlama | Microsoft Belgeleri"
description: "Azure App Service’de bir ASP.NET API uygulamasını Visual Studio 2015’i kullanarak oluşturmayı, dağıtmayı ve kullanmayı öğrenin."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: ddc028b2-cde0-4567-a6ee-32cb264a830a
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: alkarche
ms.openlocfilehash: e8fbffde29efcdbb2f67362474061e9f6ee0d59d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a><span data-ttu-id="ef4e4-103">Azure App Service’de API Apps, ASP.NET ve Swagger kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ef4e4-103">Get started with API Apps, ASP.NET, and Swagger in Azure App Service</span></span>
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="ef4e4-104">Bu, RESTful API’lerini geliştirme ve barındırma için yardımcı olara Azure App Service özelliklerini kullanmayı gösteren öğretici serisinde ilktir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-104">This is the first in a series of tutorials that show how to use features of Azure App Service that are helpful for developing and hosting RESTful APIs.</span></span>  <span data-ttu-id="ef4e4-105">Bu öğretici, Swagger biçiminde API meta veri desteğini ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-105">This tutorial covers support for API metadata in Swagger format.</span></span>

<span data-ttu-id="ef4e4-106">Şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="ef4e4-106">You'll learn:</span></span>

* <span data-ttu-id="ef4e4-107">Azure App Service’de Visual Studio 2015 yerleşik araçlarını kullanarak [API Uygulamaları](app-service-api-apps-why-best-platform.md) oluşturma ve dağıtma.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-107">How to create and deploy [API apps](app-service-api-apps-why-best-platform.md) in Azure App Service by using tools built into Visual Studio 2015.</span></span>
* <span data-ttu-id="ef4e4-108">Dinamik olarak Swagger API’si meta verileri oluşturmak için Swashbuckle NuGet paketini kullanmak üzere API keşfetmeyi otomatik hale getirmeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-108">How to automate API discovery by using the Swashbuckle NuGet package to dynamically generate Swagger API metadata.</span></span>
* <span data-ttu-id="ef4e4-109">Bir API uygulaması için otomatik olarak istemci kodu oluşturmak üzere Swagger API’si meta verilerini otomatik olarak kullanma.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-109">How to use Swagger API metadata to automatically generate client code for an API app.</span></span>

## <a name="sample-application-overview"></a><span data-ttu-id="ef4e4-110">Örnek uygulamaya genel bakış</span><span class="sxs-lookup"><span data-stu-id="ef4e4-110">Sample application overview</span></span>
<span data-ttu-id="ef4e4-111">Bu öğreticide, bir basit bir yapılacaklar listesi örnek uygulaması ile çalışırsınız.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-111">In this tutorial, you work with a simple to-do list sample application.</span></span> <span data-ttu-id="ef4e4-112">Uygulama, tek sayfalı uygulama (SPA) ön ucuna, ASP.NET Web API’si orta katmanına ve ASP.NET Web API’si veri katmanına sahip.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-112">The application has a single-page application (SPA) front end, an ASP.NET Web API middle tier, and an ASP.NET Web API data tier.</span></span>

![API Apps örnek uygulama diyagramı](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

<span data-ttu-id="ef4e4-114">Burada [AngularJS](https://angularjs.org/) ön ucu ekran görüntüsü yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-114">Here's a screen shot of the [AngularJS](https://angularjs.org/) front end.</span></span>

![API Apps örnek uygulama yapılacaklar listesi](./media/app-service-api-dotnet-get-started/todospa.png)

<span data-ttu-id="ef4e4-116">Visual Studio çözümü üç projeyi içerir:</span><span class="sxs-lookup"><span data-stu-id="ef4e4-116">The Visual Studio solution includes three projects:</span></span>

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* <span data-ttu-id="ef4e4-117">**ToDoListAngular** -Ön uç: Orta katmanı çağıran bir AngularJS SPA’sı.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-117">**ToDoListAngular** - The front end: an AngularJS SPA that calls the middle tier.</span></span>
* <span data-ttu-id="ef4e4-118">**ToDoListAPI** -Orta katman: Yapılacak işler öğelerinde CRUD işlemleri gerçekleştirmek üzere veri katmanını çağıran bir ASP.NET Web API projesi.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-118">**ToDoListAPI** - The middle tier: an ASP.NET Web API project that calls the data tier to perform CRUD operations on to-do items.</span></span>
* <span data-ttu-id="ef4e4-119">**ToDoListDataAPI** -Orta katman: Yapılacak işler öğelerinde CRUD işlemleri gerçekleştiren bir ASP.NET Web API projesi.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-119">**ToDoListDataAPI** - The data tier:  an ASP.NET Web API project that performs CRUD operations on to-do items.</span></span>

<span data-ttu-id="ef4e4-120">Üç katmanlı yapı, API Apps kullanarak uygulayabileceğiniz birçok yapıdan biridir ve burada yalnızca gösterim amacıyla kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-120">The three-tier architecture is one of many architectures that you can implement by using API Apps and is used here only for demonstration purposes.</span></span> <span data-ttu-id="ef4e4-121">Her katmandaki kod API Apps özelliklerini göstermek üzere mümkün olduğu kadar basittir: örneğin, veri katmanı kalıcılık mekanizması olarak veritabanı yerine sunucu belleği kullanır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-121">The code in each tier is as simple as possible to demonstrate API Apps features; for example, the data tier uses server memory rather than a database as its persistence mechanism.</span></span>

<span data-ttu-id="ef4e4-122">Bu öğreticiyi tamamladığınızda, App Service API uygulamalarında bulutta çalışmaya hazır iki adet Web API projesine sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-122">On completing this tutorial, you'll have the two Web API projects up and running in the cloud in App Service API apps.</span></span>

<span data-ttu-id="ef4e4-123">Serideki sonraki öğretici SPA ön ucunu buluta dağıtır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-123">The next tutorial in the series deploys the SPA front end to the cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef4e4-124">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ef4e4-124">Prerequisites</span></span>
* <span data-ttu-id="ef4e4-125">ASP.NET Web API - Öğretici yönergeleri, Visual Studio’da ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) ile çalışmaya ilişkin temel bilgiye sahip olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-125">ASP.NET Web API - The tutorial instructions assume you have a basic knowledge of how to work with ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.</span></span>
* <span data-ttu-id="ef4e4-126">Azure hesabı - [Ücretsiz bir Azure hesabı açabilir](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) veya [Visual Studio abonelik avantajlarını etkinleştirebilirsiniz](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="ef4e4-126">Azure account - You can [Open an Azure account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
  
    <span data-ttu-id="ef4e4-127">Bir Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak istiyorsanız [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/)’e gidin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-127">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="ef4e4-128">Burada, Uygulama Hizmetleri’nde hemen bir kısa süreli başlangıç uygulaması oluşturabilirsiniz; **kredi kartı gerekmez** ve hiçbir taahhüt yoktur.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-128">There, you can immediately create a short-lived starter app in App Service — **no credit card required**, and no commitments.</span></span>
* <span data-ttu-id="ef4e4-129">[.NET için Azure SDK](https://azure.microsoft.com/downloads/archive-net-downloads/) ile Visual Studio 2015 - Halihazırda yoksa SDK, Visual Studio 2015’i otomatik olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-129">Visual Studio 2015 with the [Azure SDK for .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) - The SDK installs Visual Studio 2015 automatically if you don't already have it.</span></span>
  
  * <span data-ttu-id="ef4e4-130">Visual Studio’da Yardım -> Microsoft Visual Studio Hakkında’ya tıklayın ve "Azure App Service Tools v2.9.1" veya sonraki bir sürümün yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-130">In Visual Studio, click Help -> About Microsoft Visual Studio and ensure that you have "Azure App Service Tools v2.9.1" or higher installed.</span></span>
    
    ![Azure App Tools sürümü](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > <span data-ttu-id="ef4e4-132">Makinenizde zaten bulunan SDK bağımlılığı sayısına bağlı olarak, SDK’nin yüklenmesi birkaç dakikadan yarım saate uzanacak şekilde biraz uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-132">Depending on how many of the SDK dependencies you already have on your machine, installing the SDK could take a long time, from several minutes to a half hour or more.</span></span>
    > 
    > 

## <a name="download-the-sample-application"></a><span data-ttu-id="ef4e4-133">Örnek uygulamayı indirin:</span><span class="sxs-lookup"><span data-stu-id="ef4e4-133">Download the sample application</span></span>
1. <span data-ttu-id="ef4e4-134">[Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) deposunu indirin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-134">Download the [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repository.</span></span>
   
    <span data-ttu-id="ef4e4-135">**ZIP’i İndir** düğmesine tıklayabilir ya da depoyu yerel makinenize kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-135">You can click the **Download ZIP** button or clone the repository on your local machine.</span></span>
2. <span data-ttu-id="ef4e4-136">Visual Studio 2015 ya da 2013’te ToDoList çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-136">Open the ToDoList solution in Visual Studio 2015 or 2013.</span></span>
   
   1. <span data-ttu-id="ef4e4-137">Her çözüme güvenmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-137">You will need to trust each solution.</span></span>
         <span data-ttu-id="ef4e4-138">![Güvenlik Uyarısı](./media/app-service-api-dotnet-get-started/securitywarning.png)</span><span class="sxs-lookup"><span data-stu-id="ef4e4-138">![Security Warning](./media/app-service-api-dotnet-get-started/securitywarning.png)</span></span>
3. <span data-ttu-id="ef4e4-139">NuGet paketlerini geri yüklemek için çözümü oluşturun (CTRL + SHIFT + B).</span><span class="sxs-lookup"><span data-stu-id="ef4e4-139">Build the solution (CTRL + SHIFT + B)  to restore the NuGet packages.</span></span>
   
    <span data-ttu-id="ef4e4-140">Dağıtmadan önce uygulamanın çalışmasını görmek istiyorsanız, yerel olarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-140">If you want to see the application in operation before you deploy it, you can run it locally.</span></span> <span data-ttu-id="ef4e4-141">ToDoListDataAPI öğesinin başlangıç projeniz olduğundan emin olun ve çözümü çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-141">Make sure that ToDoListDataAPI is your startup project and run the solution.</span></span> <span data-ttu-id="ef4e4-142">Tarayıcınızda bir HTTP 403 hatası görmeyi beklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-142">You should expect to see a HTTP 403 error in your browser.</span></span>

## <a name="use-swagger-api-metadata-and-ui"></a><span data-ttu-id="ef4e4-143">Swagger API meta verileri ve kullanıcı arabirimi kullanma</span><span class="sxs-lookup"><span data-stu-id="ef4e4-143">Use Swagger API metadata and UI</span></span>
<span data-ttu-id="ef4e4-144">[Swagger](http://swagger.io/) 2.0 API meta verileri desteği Azure App Service’de yerleşiktir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-144">Support for [Swagger](http://swagger.io/) 2.0 API metadata is built into Azure App Service.</span></span> <span data-ttu-id="ef4e4-145">Her API, API meta verilerini Swagger JSON biçiminde döndüren bir URL uç noktası belirtebilir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-145">Each API app can specify a URL endpoint that returns metadata for the API in Swagger JSON format.</span></span> <span data-ttu-id="ef4e4-146">Bu uç noktadan döndürülen meta veriler istemci kodu oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-146">The metadata returned from that endpoint can be used to generate client code.</span></span>

<span data-ttu-id="ef4e4-147">Bir ASP.NET Web API projesi [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet paketi kullanarak dinamik olarak Swagger meta verileri oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-147">An ASP.NET Web API project can dynamically generate Swagger metadata by using the [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package.</span></span> <span data-ttu-id="ef4e4-148">Swashbuckle NuGet paketi indirdiğiniz ToDoListDataAPI ve ToDoListAPI projelerinde zaten yüklüdür.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-148">The Swashbuckle NuGet package is already installed in the ToDoListDataAPI and ToDoListAPI projects that you downloaded.</span></span>

<span data-ttu-id="ef4e4-149">Öğreticinin bu bölümünde, Swagger 2.0 Swagger meta verileri oluşturmayı inceler ve ardından Swagger meta verilerini temel alan bir kullanıcı arabirimini denersiniz.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-149">In this section of the tutorial, you look at the generated Swagger 2.0 metadata, and then you try out a test UI that is based on the Swagger metadata.</span></span>

1. <span data-ttu-id="ef4e4-150">Başlangıç projesi olarak ToDoListDataAPI projesi (ToDoListAPI projesi **değil**) ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-150">Set the ToDoListDataAPI project (**not** the ToDoListAPI project) as the startup project.</span></span>
   
    ![ToDoDataAPI ayarını Başlangıç Projesi olarak belirleyin](./media/app-service-api-dotnet-get-started/startupproject.png)
2. <span data-ttu-id="ef4e4-152">Projeyi hata ayıklama modunda çalıştırmak için ,F5 tuşuna basın veya **Hata Ayıklama > Hata Ayıklamayı Başlat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-152">Press F5 or click **Debug > Start Debugging** to run the project in debug mode.</span></span>
   
    <span data-ttu-id="ef4e4-153">Tarayıcı açılır ve HTTP 403 hata sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-153">The browser opens and shows the HTTP 403 error page.</span></span>
3. <span data-ttu-id="ef4e4-154">Tarayıcınızın adres çubuğuna, satırın sonuna `swagger/docs/v1` ekleyin ve Return tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-154">In your browser address bar, add `swagger/docs/v1` to the end of the line, and then press Return.</span></span> <span data-ttu-id="ef4e4-155">(URL `http://localhost:45914/swagger/docs/v1` şeklindedir.)</span><span class="sxs-lookup"><span data-stu-id="ef4e4-155">(The URL is `http://localhost:45914/swagger/docs/v1`.)</span></span>
   
    <span data-ttu-id="ef4e4-156">Bu API için Swagger 2.0 JSON meta verileri döndürmek üzere Swashbuckle tarafından kullanılan varsayılan URL'dir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-156">This is the default URL used by Swashbuckle to return Swagger 2.0 JSON metadata for the API.</span></span>
   
    <span data-ttu-id="ef4e4-157">Internet Explorer kullanıyorsanız, tarayıcı bir *v1.json* dosyası yüklemenizi ister.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-157">If you're using Internet Explorer, the browser prompts you to download a *v1.json* file.</span></span>
   
    ![IE’de JSON meta veriler indirme](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    <span data-ttu-id="ef4e4-159">Chrome, Firefox veya Microsoft Edge kullanıyorsanız, tarayıcıyı JSON dosyasını tarayıcı penceresinde görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-159">If you're using Chrome, Firefox, or Edge, the browser displays the JSON in the browser window.</span></span> <span data-ttu-id="ef4e4-160">Farklı tarayıcılar JSON dosyasını farklı şekilde işler ve tarayıcı pencereniz tam olarak örnekteki gibi görünmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-160">Different browsers handle JSON differently, and your browser window may not look exactly like the example.</span></span>
   
    ![Chrome’da JSON meta verileri](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    <span data-ttu-id="ef4e4-162">Aşağıdaki örnek, Get yöntemi tanımıyla, API için Swagger meta verilerinin ilk bölümü gösterir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-162">The following sample shows the first section of the Swagger metadata for the API, with the definition for the Get method.</span></span> <span data-ttu-id="ef4e4-163">Bu meta veriler aşağıdaki adımlarda kullandığınız Swagger kullanıcı arabirimini yönlendirir ve bunu öğreticinin sonraki bölümünde otomatik olarak istemci kodu oluşturmak üzere kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-163">This metadata is what drives the Swagger UI that you use in the following steps, and you use it in a later section of the tutorial to automatically generate client code.</span></span>
   
        {
          "swagger": "2.0",
          "info": {
            "version": "v1",
            "title": "ToDoListDataAPI"
          },
          "host": "localhost:45914",
          "schemes": [ "http" ],
          "paths": {
            "/api/ToDoList": {
              "get": {
                "tags": [ "ToDoList" ],
                "operationId": "ToDoList_GetByOwner",
                "consumes": [ ],
                "produces": [ "application/json", "text/json", "application/xml", "text/xml" ],
                "parameters": [
                  {
                    "name": "owner",
                    "in": "query",
                    "required": true,
                    "type": "string"
                  }
                ],
                "responses": {
                  "200": {
                    "description": "OK",
                    "schema": {
                      "type": "array",
                      "items": { "$ref": "#/definitions/ToDoItem" }
                    }
                  }
                },
                "deprecated": false
              },
4. <span data-ttu-id="ef4e4-164">Tarayıcıyı kapatın ve Visual Studio hata ayıklamayı durdurun.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-164">Close the browser and stop Visual Studio debugging.</span></span>
5. <span data-ttu-id="ef4e4-165">**Çözüm Gezgini**’ndeki ToDoListDataAPI projesinde *App_Start\SwaggerConfig.cs* dosyasını açın ve ardından satır 174’e inerek aşağıdaki kodun açıklamasını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-165">In the ToDoListDataAPI project in **Solution Explorer**, open the *App_Start\SwaggerConfig.cs* file, then scroll down to line 174 and uncomment the following code.</span></span>
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    <span data-ttu-id="ef4e4-166">Projede Swashbuckle paketini yüklediğinizde *SwaggerConfig.cs* dosyası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-166">The *SwaggerConfig.cs* file is created when you install the Swashbuckle package in a project.</span></span> <span data-ttu-id="ef4e4-167">Dosya Swashbuckle yapılandırmak için çeşitli yöntemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-167">The file provides a number of ways to configure Swashbuckle.</span></span>
   
    <span data-ttu-id="ef4e4-168">Açıklamasını kaldırdığını kod aşağıdaki adımlarda kullandığınız Swagger kullanıcı arabirimini etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-168">The code you've uncommented enables the Swagger UI that you use in the following steps.</span></span> <span data-ttu-id="ef4e4-169">API uygulaması proje şablonunu kullanarak bir Web API projesi oluşturduğunuzda, bu kod varsayılan bir güvenlik önlemi olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-169">When you create a Web API project by using the API app project template, this code is commented out by default as a security measure.</span></span>
6. <span data-ttu-id="ef4e4-170">Projeyi tekrar çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-170">Run the project again.</span></span>
7. <span data-ttu-id="ef4e4-171">Tarayıcınızın adres çubuğuna, satırın sonuna `swagger` ekleyin ve Return tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-171">In your browser address bar, add `swagger` to the end of the line, and then press Return.</span></span> <span data-ttu-id="ef4e4-172">(URL `http://localhost:45914/swagger` şeklindedir.)</span><span class="sxs-lookup"><span data-stu-id="ef4e4-172">(The URL is `http://localhost:45914/swagger`.)</span></span>
8. <span data-ttu-id="ef4e4-173">Swagger kullanıcı arabirimi sayfası görüntülendiğinde, kullanılabilecek yöntemleri görmek için**ToDoList**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-173">When the Swagger UI page appears, click **ToDoList** to see the methods available.</span></span>
   
    ![Swagger kullanıcı arabirimi kullanılabilir yöntemleri](./media/app-service-api-dotnet-get-started/methods.png)
9. <span data-ttu-id="ef4e4-175">Listede ilk **Al** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-175">Click the first **Get** button in the list.</span></span>
10. <span data-ttu-id="ef4e4-176">**Parametreler** bölümünde, `owner` parametresi değerini bir yıldız işareti olarak girin ve ardından **Deneyin**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-176">In the **Parameters** section, enter an asterisk as the value of the `owner` parameter, and then click **Try it out**.</span></span>
    
    <span data-ttu-id="ef4e4-177">Sonraki öğreticilerde kimlik doğrulama eklediğinizde, orta katman veri katmanına asıl kullanıcı kimliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-177">When you add authentication in later tutorials, the middle tier will provide the actual user ID to the data tier.</span></span> <span data-ttu-id="ef4e4-178">Şimdilik, tüm görevler kendi kimlikleri olarak yıldız işaretine sahip olurken uygulama kimlik doğrulama etkin olmadan çalışır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-178">For now, all tasks will have asterisk as their owner ID while the application runs without authentication enabled.</span></span>
    
    ![Swagger kullanıcı arabirimini deneyin](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    <span data-ttu-id="ef4e4-180">Swagger kullanıcı arabirimi ToDoList Alma yöntemini çağırır ve yanıt kodunu ve JSON sonuçlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-180">The Swagger UI calls the ToDoList Get method and displays the response code and JSON results.</span></span>
    
    ![Swagger kullanıcı arabirimini deneyin sonuçları](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. <span data-ttu-id="ef4e4-182">**Gönder**’e tıklayın ve ardından **Model Şeması** altındaki kutuya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-182">Click **Post**, and then click the box under **Model Schema**.</span></span>
    
    <span data-ttu-id="ef4e4-183">Model şemasına tıklamak, Gönderme yöntemi için parametre değerini belirtebileceğiniz giriş kutusunu doldurur.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-183">Clicking the model schema prefills the input box where you can specify the parameter value for the Post method.</span></span> <span data-ttu-id="ef4e4-184">(Internet Explorer'da bu işe yaramazsa, farklı bir tarayıcı kullanın veya sonraki adımda parametre değerini el ile girin.)</span><span class="sxs-lookup"><span data-stu-id="ef4e4-184">(If this doesn't work in Internet Explorer, use a different browser or enter the parameter value manually in the next step.)</span></span>  
    
    ![Swagger kullanıcı arabirimini deneyin Gönder](./media/app-service-api-dotnet-get-started/post.png)
12. <span data-ttu-id="ef4e4-186">`todo` parametresi giriş kutusunda JSON’ı aşağıdaki örnekte görünecek şekilde değiştirin ya da kendi açıklama metninizle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ef4e4-186">Change the JSON in the `todo` parameter input box so that it looks like the following example, or substitute your own description text:</span></span>
    
        {
          "ID": 2,
          "Description": "buy the dog a toy",
          "Owner": "*"
        }
13. <span data-ttu-id="ef4e4-187">**Deneyin**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-187">Click **Try it out**.</span></span>
    
    <span data-ttu-id="ef4e4-188">ToDoList API’sı başarı belirten bir HTTP 204 yanıtı döndürür.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-188">The ToDoList API returns an HTTP 204 response code that indicates success.</span></span>
14. <span data-ttu-id="ef4e4-189">İlk **Al** düğmesine tıklayın ve ardından sayfanın bu bölümünde **Deneyin** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-189">Click the first **Get** button, and then in that section of the page click the **Try it out** button.</span></span>
    
    <span data-ttu-id="ef4e4-190">Get yöntemi yanıtı şimdi yeni yapılacak iş öğesini içerir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-190">The Get method response now includes the new to do item.</span></span>
15. <span data-ttu-id="ef4e4-191">İsteğe bağlı: Ayrıca kimlik yöntemlerine göre Koy, Sil ve Al seçeneklerini deneyin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-191">Optional: Try also the Put, Delete, and Get by ID methods.</span></span>
16. <span data-ttu-id="ef4e4-192">Tarayıcıyı kapatın ve Visual Studio hata ayıklamayı durdurun.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-192">Close the browser and stop Visual Studio debugging.</span></span>

<span data-ttu-id="ef4e4-193">Swashbuckle her ASP.NET Web API projesi ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-193">Swashbuckle works with any ASP.NET Web API project.</span></span> <span data-ttu-id="ef4e4-194">Mevcut bir projeye Swagger meta verileri oluşturma olanağı eklemek istiyorsanız, yalnızca Swashbuckle paketini yüklemeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-194">If you want to add Swagger metadata generation to an existing project, just install the Swashbuckle package.</span></span>

> [!NOTE]
> <span data-ttu-id="ef4e4-195">Swagger meta verileri her API işlemi için benzersiz bir kimlik içerir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-195">Swagger metadata includes a unique ID for each API operation.</span></span> <span data-ttu-id="ef4e4-196">Varsayılan olarak, Swashbuckle Web API denetleyicisi yöntemleriniz için yinelenen Swagger işlemi kimlikleri oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-196">By default, Swashbuckle may generate duplicate Swagger operation IDs for your Web API controller methods.</span></span> <span data-ttu-id="ef4e4-197">Bu durum, denetleyiciniz `Get()` ve `Get(id)` gibi, HTTP yöntemleriyle aşırı yüklü olduğunda gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-197">This happens if your controller has overloaded HTTP methods, such as `Get()` and `Get(id)`.</span></span> <span data-ttu-id="ef4e4-198">Aşırı yükleri işleme hakkında daha fazla bilgi için bkz. [Swashbuckle tarafından oluşturulan API tanımlarını özelleştirme](app-service-api-dotnet-swashbuckle-customize.md).</span><span class="sxs-lookup"><span data-stu-id="ef4e4-198">For information about how to handle overloads, see [Customize Swashbuckle-generated API definitions](app-service-api-dotnet-swashbuckle-customize.md).</span></span> <span data-ttu-id="ef4e4-199">Visual Studio'da Azure API Uygulaması şablonu kullanarak bir Web API projesi oluşturursanız, benzersiz işlem kimlikleri oluşturan kod otomatik olarak *SwaggerConfig.cs* dosyasına eklenir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-199">If you create a Web API project in Visual Studio by using the Azure API App template, code that generates unique operation IDs is automatically added to the *SwaggerConfig.cs* file.</span></span>  
> 
> 

## <span data-ttu-id="ef4e4-200"><a id="createapiapp"></a> Azure’da API uygulaması oluşturma ve buna kod dağıtma</span><span class="sxs-lookup"><span data-stu-id="ef4e4-200"><a id="createapiapp"></a> Create an API app in Azure and deploy code to it</span></span>
<span data-ttu-id="ef4e4-201">Bu bölümde, Azure’da yeni bir API uygulaması oluşturmak için Visual Studio **Web’i Yayımla** sihirbazına tümleştirilen Azure araçlarını kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-201">In this section, you use Azure tools that are integrated into the Visual Studio **Publish Web** wizard to create a new API app in Azure.</span></span> <span data-ttu-id="ef4e4-202">Ardından, yeni API uygulamasına ToDoListDataAPI projesini dağıtır ve Swagger kullanıcı arabirimini çalıştırarak API’yi çağırırsınız.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-202">Then you deploy the ToDoListDataAPI project to the new API app and call the API by running the Swagger UI.</span></span>

1. <span data-ttu-id="ef4e4-203">**Çözüm Gezgini**’nde ToDoListDataAPI projesine sağ tıklayın ve ardından **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-203">In **Solution Explorer**, right-click the ToDoListDataAPI project, and then click **Publish**.</span></span>
   
    ![Visual Studio’ya Yayımla'ya tıklama](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. <span data-ttu-id="ef4e4-205">**Web’de Yayımla** sihirbazının **Profil** adımında, **Microsoft Azure App Service**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-205">In the **Profile** step of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
   
   ![Web’de Yayımla sihirbazında Azure App Service’e tıklama](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. <span data-ttu-id="ef4e4-207">Henüz yapmadıysanız, Azure hesabınızda oturum açın veya süresi dolduysa, kimlik bilgilerinizi yenileyin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-207">Sign in to your Azure account if you have not already done so, or refresh your credentials if they're expired.</span></span>
4. <span data-ttu-id="ef4e4-208">App Service iletişim kutusunda, kullanmak istediğiniz Azure **Aboneliğini** seçin ve ardından **Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-208">In the App Service dialog box, choose the Azure **Subscription** you want to use, and then click **New**.</span></span>
   
    ![App Service iletişim kutusunda Yeni’ye tıklama](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    <span data-ttu-id="ef4e4-210">**App Service oluşturma** iletişim kutusunun **Barındırma** sekmesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-210">The **Hosting** tab of the **Create App Service** dialog box appears.</span></span>
   
    <span data-ttu-id="ef4e4-211">Swashbuckle yüklü olan bir Web API projesi dağıttığınız için, Visual Studio bir API uygulaması oluşturmak istediğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-211">Because you're deploying a Web API project that has Swashbuckle installed, Visual Studio assumes that you want to create an API App.</span></span> <span data-ttu-id="ef4e4-212">Bu **API Uygulaması Adı** başlığı ve **Türü Değiştir** açılır listesinin **API Uygulaması** olarak ayarlanmasıyla belirtilir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-212">This is indicated by the **API App Name** title and by the fact that the **Change Type** drop-down list is set to **API App**.</span></span>
   
    ![App Service iletişim kutusunda Uygulama türü](./media/app-service-api-dotnet-get-started/apptype.png)
5. <span data-ttu-id="ef4e4-214">*azurewebsites.net* etki alanında benzersiz bir **API Uygulaması Adı** girin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-214">Enter an **API App Name** that is unique in the *azurewebsites.net* domain.</span></span> <span data-ttu-id="ef4e4-215">Visual Studio’nun önerdiği varsayılan adı kabul edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-215">You can accept the default name that Visual Studio proposes.</span></span>
   
    <span data-ttu-id="ef4e4-216">Başka birinin önceden kullandığı bir adı girerseniz, sağda kırmızı bir ünlem işareti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-216">If you enter a name that someone else has already used, you see a red exclamation mark to the right.</span></span>
   
    <span data-ttu-id="ef4e4-217">API uygulamasının URL’si `{API app name}.azurewebsites.net` olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-217">The URL of the API app will be `{API app name}.azurewebsites.net`.</span></span>
6. <span data-ttu-id="ef4e4-218">**Kaynak Grubu** açılır menüsünde, **Yeni**’ye tıklayın ve ardından isterseniz "ToDoListGroup" ya da başka bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-218">In the **Resource Group** drop-down, click **New**, and then enter "ToDoListGroup" or another name if you prefer.</span></span>
   
    <span data-ttu-id="ef4e4-219">Kaynak grubu API uygulamaları, veritabanları, sanal makineler ve benzerleri gibi Azure kaynakları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-219">A resource group is a collection of Azure resources such as API apps, databases, VMs, and so forth.</span></span>    <span data-ttu-id="ef4e4-220">Bu öğreticide, en iyi uygulama yeni bir kaynak grubu oluşturulmasıdır; böylece, öğretici için oluşturduğunuz Azure kaynaklarını tek bir adımda kolayca silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-220">For this tutorial, it's best to create a new resource group because that makes it easy to delete in one step all the Azure resources that you create for the tutorial.</span></span>
   
    <span data-ttu-id="ef4e4-221">Bu kutu mevcut [kaynak grubunu](../azure-resource-manager/resource-group-overview.md) seçmenize ya da aboneliklerinizdeki kaynak grubunda olanlardan farklı bir ad yazarak yeni bir tane oluşturmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-221">This box lets you select an existing [resource group](../azure-resource-manager/resource-group-overview.md) or create a new one by typing in a name that is different from any existing resource group in your subscription.</span></span>
7. <span data-ttu-id="ef4e4-222">**App Service Planı** açılır menüsünün yanındaki **Yeni** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-222">Click the **New** button next to the **App Service Plan** drop-down.</span></span>
   
    <span data-ttu-id="ef4e4-223">Ekran görüntüsü **API Uygulaması Adı**, **Abonelik** ve **Kaynak Grubu** için örnek değerleri gösterir - sizin değerlerinizi farklı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-223">The screen shot shows sample values for **API App Name**, **Subscription**, and **Resource Group** -- your values will be different.</span></span>
   
    ![App Service Oluştur iletişim kutusu](./media/app-service-api-dotnet-get-started/createas.png)
   
    <span data-ttu-id="ef4e4-225">Aşağıdaki adımlarda, yeni kaynak grubu için bir App Service planı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-225">In the following steps you create an App Service plan for the new resource group.</span></span> <span data-ttu-id="ef4e4-226">App Service planı, API uygulamanızın üzerinde çalışacağı işlem kaynaklarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-226">An App Service plan specifies the compute resources that your API app runs on.</span></span> <span data-ttu-id="ef4e4-227">Örneğin, ücretsiz katmanı seçerseniz API uygulamanız paylaşılan sanal makineler üzerinde çalışır, bazı ücretli katmanlarda ise ayrılmış sanal makineler üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-227">For example, if you choose the free tier, your API app runs on shared VMs, while for some paid tiers it runs on dedicated VMs.</span></span> <span data-ttu-id="ef4e4-228">App Service planları hakkında bilgi için bkz. [App Service planlarına genel bakış](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ef4e4-228">For information about App Service plans, see [App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
8. <span data-ttu-id="ef4e4-229">**App Service Planı Yapılandır** iletişim kutusunda, "ToDoListPlan" ifadesini veya tercih ettiğiniz başka bir adı girin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-229">In the **Configure App Service Plan** dialog, enter "ToDoListPlan" or another name if you prefer.</span></span>
9. <span data-ttu-id="ef4e4-230">**Konum** açılır listesinde, size en yakın konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-230">In the **Location** drop-down list, choose the location that is closest to you.</span></span>
   
    <span data-ttu-id="ef4e4-231">Bu ayar, uygulamanızın hangi Azure veri merkezinde çalıştırılacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-231">This setting specifies which Azure datacenter your app will run in.</span></span> <span data-ttu-id="ef4e4-232">[Gecikmeyi](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090) en aza indirmek için yakın bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-232">Choose a location close to you to minimize [latency](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span></span>
10. <span data-ttu-id="ef4e4-233">**Boyut** açılır menüsünde **Ücretsiz**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-233">In the **Size** drop-down, click **Free**.</span></span>
    
    <span data-ttu-id="ef4e4-234">Bu öğretici için ücretsiz fiyatlandırma katmanı yeterli ölçüde performans sunacaktır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-234">For this tutorial, the free pricing tier will provide sufficient performance.</span></span>
11. <span data-ttu-id="ef4e4-235">**App Service Planı Yapılandır** iletişim kutusunda **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-235">In the **Configure App Service Plan** dialog, click **OK**.</span></span>
    
    ![App Service Planı Yapılandır iletişim kutusunda Tamam’a tıklama](./media/app-service-api-dotnet-get-started/configasp.png)
12. <span data-ttu-id="ef4e4-237">**App Service Oluştur** iletişim kutusunda **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-237">In the **Create App Service** dialog box, click **Create**.</span></span>
    
    ![App Service Oluştur iletişim kutusunda Oluştur’a tıklama](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    <span data-ttu-id="ef4e4-239">Visual Studio API uygulamasını ve API uygulaması için gereken tüm ayarları içeren bir yayımlama profili oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-239">Visual Studio creates the API app and a publish profile that has all of the required settings for the API app.</span></span> <span data-ttu-id="ef4e4-240">Sonra, projeyi dağıtmak için kullanacağınız **Web’i Yayımla** sihirbazını açar.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-240">Then it opens the **Publish Web** wizard, which you'll use to deploy the project.</span></span>
    
    <span data-ttu-id="ef4e4-241">**Web’i Yayımla** sihirbazı **Bağlantı** sekmesinde (aşağıda gösterilen) açılır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-241">The **Publish Web** wizard opens on the **Connection** tab (shown below).</span></span>
    
    <span data-ttu-id="ef4e4-242">**Bağlantı** sekmesinde **Sunucu** ve **Site adı** ayarları API uygulamanızı işaret eder.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-242">On the **Connection** tab, the **Server** and **Site name** settings point to your API app.</span></span> <span data-ttu-id="ef4e4-243">**Kullanıcı adı** ve **Parola** Azure’un sizin için oluşturduğu dağıtım kimlik bilgileridir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-243">The **User name** and **Password** are deployment credentials that Azure creates for you.</span></span> <span data-ttu-id="ef4e4-244">Dağıtımdan sonra, Visual Studio **Hedef URL’si**nde (bu **Hedef URL**’sinin tek amacıdır) bir tarayıcı açar.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-244">After deployment, Visual Studio opens a browser to the **Destination URL** (that's the only purpose for **Destination URL**).</span></span>  
13. <span data-ttu-id="ef4e4-245">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-245">Click **Next**.</span></span>
    
    ![Web'i Yayımla sihirbazının Bağlantı sekmesinde İleri'ye tıklama](./media/app-service-api-dotnet-get-started/connnext.png)
    
    <span data-ttu-id="ef4e4-247">Sonraki sekme **Ayarlar** sekmesidir (aşağıda gösterilen).</span><span class="sxs-lookup"><span data-stu-id="ef4e4-247">The next tab is the **Settings** tab (shown below).</span></span> <span data-ttu-id="ef4e4-248">Burada, [uzaktan hata ayıklama](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug) için hata ayıklama derlemesi dağıtmak üzere derleme yapılandırma sekmesini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-248">Here you can change the build configuration tab to deploy a debug build for [remote debugging](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span></span> <span data-ttu-id="ef4e4-249">Ayrıca, bu sekmede birkaç farklı **Dosya Yayımlama Seçeneği** bulunur:</span><span class="sxs-lookup"><span data-stu-id="ef4e4-249">The tab also offers several **File Publish Options**:</span></span>
    
    * <span data-ttu-id="ef4e4-250">Hedefteki ek dosyaları kaldır</span><span class="sxs-lookup"><span data-stu-id="ef4e4-250">Remove additional files at destination</span></span>
    * <span data-ttu-id="ef4e4-251">Yayımlama sırasında ön derleme yap</span><span class="sxs-lookup"><span data-stu-id="ef4e4-251">Precompile during publishing</span></span>
    * <span data-ttu-id="ef4e4-252">App_Data klasöründeki dosyaları dışarıda bırak</span><span class="sxs-lookup"><span data-stu-id="ef4e4-252">Exclude files from the App_Data folder</span></span>
    
    <span data-ttu-id="ef4e4-253">Bu öğreticide bunlardan biri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-253">For this tutorial you don't need any of these.</span></span> <span data-ttu-id="ef4e4-254">Bunların ne yaptıklarına ilişkin ayrıntılı açıklamalar için bkz. [Nasıl yapılır: Visual Studio’da Tek Tıklamayla Yayımlamayı Kullanarak Web Projesi Dağıtma](https://msdn.microsoft.com/library/dd465337.aspx).</span><span class="sxs-lookup"><span data-stu-id="ef4e4-254">For detailed explanations of what they do, see [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span></span>
14. <span data-ttu-id="ef4e4-255">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-255">Click **Next**.</span></span>
    
    ![Web’i Yayımla sihirbazının Ayarlar sekmesi İleri’ye tıklama](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    <span data-ttu-id="ef4e4-257">Burada, İleri seçeneği hangi dosyaların projenizden API uygulamasına kopyalanacağını görme fırsatı veren **Önizleme** sekmesidir (aşağıda gösterilen).</span><span class="sxs-lookup"><span data-stu-id="ef4e4-257">Next is the **Preview** tab (shown below), which gives you an opportunity to see what files are going to be copied from your project to the API app.</span></span> <span data-ttu-id="ef4e4-258">Daha önce dağıttığınız bir API uygulamasına bir proje dağıtıyorsanız, yalnızca değiştirilen dosyalar kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-258">When you're deploying a project to an API app that you already deployed to earlier, only changed files are copied.</span></span> <span data-ttu-id="ef4e4-259">Kopyalanacak dosyaların bir listesi görmek isterseniz, **Önizlemeyi Başlat** düğmesine tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-259">If you want to see a list of what will be copied, you can click the **Start Preview** button.</span></span>
15. <span data-ttu-id="ef4e4-260">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-260">Click **Publish**.</span></span>
    
    ![Web’i Yayımla sihirbazının Önizleme sekmesinde Yayımla’ya tıklama](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    <span data-ttu-id="ef4e4-262">Visual Studio ToDoListDataAPI projesini yeni API uygulamasına dağıtır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-262">Visual Studio deploys the ToDoListDataAPI project to the new API app.</span></span> <span data-ttu-id="ef4e4-263">**Çıktı** penceresi başarılı dağıtımı günlüğe kaydeder ve API uygulamasının URL’sinde açılan bir tarayıcı penceresinde “başarıyla oluşturuldu” sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-263">The **Output** window logs successful deployment, and a "successfully created" page appears in a browser window opened to the URL of the API app.</span></span>
    
    ![Çıktı penceresi başarılı dağıtım](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Yeni API uygulaması başarıyla oluşturuldu sayfası](./media/app-service-api-dotnet-get-started/appcreated.png)
16. <span data-ttu-id="ef4e4-266">Tarayıcının adres çubuğundaki URL’ye "swagger" ifadesini ekleyin ve ardından Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-266">Add "swagger" to the URL in the browser's address bar, and then press Enter.</span></span> <span data-ttu-id="ef4e4-267">(URL `http://{apiappname}.azurewebsites.net/swagger` şeklindedir.)</span><span class="sxs-lookup"><span data-stu-id="ef4e4-267">(The URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
    
    <span data-ttu-id="ef4e4-268">Tarayıcı daha önce gördüğünüzle aynı Swagger kullanıcı arabirimini görüntüler, ancak artık bulutta çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-268">The browser displays the same Swagger UI that you saw earlier, but now it's running in the cloud.</span></span> <span data-ttu-id="ef4e4-269">Alma yöntemini deneyin ve yeniden varsayılan 2 yapılacak işler öğelerine döndüğünüzü görün.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-269">Try out the Get method, and you see that you're back to the default 2 to-do items.</span></span> <span data-ttu-id="ef4e4-270">Daha önce yaptığınız değişiklikler yerel makinede bulunan belleğe kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-270">The changes you made earlier were saved in memory in the local machine.</span></span>
17. <span data-ttu-id="ef4e4-271">[Azure portalı](https://portal.azure.com/) açın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-271">Open the [Azure portal](https://portal.azure.com/).</span></span>
    
    <span data-ttu-id="ef4e4-272">Azure portal, API uygulamaları gibi Azure kaynaklarını yönetmek için bir web arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-272">The Azure portal is a web interface for managing Azure resources such as API apps.</span></span>
18. <span data-ttu-id="ef4e4-273">**Diğer Hizmetler > Uygulama Hizmetleri**’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-273">Click **More Services > App Services**.</span></span>
    
    ![Uygulama Hizmetleri’ne Gözatma](./media/app-service-api-dotnet-get-started/browseas.png)
19. <span data-ttu-id="ef4e4-275">**App Service** dikey penceresinde,yeni API uygulamanızı bulun ve tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-275">In the **App Services** blade, find and click your new API app.</span></span> <span data-ttu-id="ef4e4-276">(Azure portalda, sağda açılan pencerelere *dikey pencere* adı verilir.)</span><span class="sxs-lookup"><span data-stu-id="ef4e4-276">(In the Azure portal, windows that open to the right are called *blades*.)</span></span>
    
    ![Uygulama Hizmetleri dikey penceresi](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    <span data-ttu-id="ef4e4-278">İki dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-278">Two blades open.</span></span> <span data-ttu-id="ef4e4-279">Bir dikey pencerede API uygulamasına genel bakış, diğerinde görüntüleyebileceğiniz ve değiştirebileceğini ayarlayın uzun bir listesi yer alır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-279">One blade has an overview of the API app, and one has a long list of settings that you can view and change.</span></span>
20. <span data-ttu-id="ef4e4-280">**Ayarlar** dikey penceresinde, **API** bölümünü bulun ve **API Tanımı**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-280">In the **Settings** blade, find the **API** section and click **API Definition**.</span></span>
    
    ![Ayarlar dikey penceresinde API Tanımı](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    <span data-ttu-id="ef4e4-282">**API tanımı** dikey penceresi JSON biçiminde Swagger 2.0 meta verilerine döndüren URL’yi belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-282">The **API Definition** blade lets you specify the URL that returns Swagger 2.0 metadata in JSON format.</span></span> <span data-ttu-id="ef4e4-283">Visual Studio API uygulaması oluşturduğunda, API uygulamasının temel URL’si artı `/swagger/docs/v1` olan, daha önce gördüğünüz Swashbuckle tarafından oluşturulan meta verilerinin varsayılan değerine API tanımı URL’sini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-283">When Visual Studio creates the API app, it sets the API definition URL to the default value for Swashbuckle-generated metadata that you saw earlier, which is the API app's base URL plus `/swagger/docs/v1`.</span></span>
    
    ![API tanımı URL'si](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    <span data-ttu-id="ef4e4-285">Kendisi için istemci kodu oluşturmak üzere API uygulamasını seçtiğinizde, Visual Studio meta verileri bu URL’den alır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-285">When you select an API app to generate client code for it, Visual Studio retrieves the metadata from this URL.</span></span>

## <span data-ttu-id="ef4e4-286"><a id="codegen"></a> Veri katmanı için istemci kodu oluşturma</span><span class="sxs-lookup"><span data-stu-id="ef4e4-286"><a id="codegen"></a> Generate client code for the data tier</span></span>
<span data-ttu-id="ef4e4-287">Swagger’ı Azure API uygulamalarına tümleştirmenin avantajlarından biri otomatik kod oluşturmadır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-287">One of the advantages of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="ef4e4-288">Oluşturulan istemci sınıfları API uygulamasını çağıran bir kod yazmayı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-288">Generated client classes make it easier to write code that calls an API app.</span></span>

<span data-ttu-id="ef4e4-289">ToDoListAPI projesinin oluşturulan istemci kodu zaten vardır, ancak aşağıdaki adımlarda bunu silecek ve kod oluşturmanın nasıl yapıldığını görmek için yeniden oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-289">The ToDoListAPI project already has the generated client code, but in the following steps you'll delete it and regenerate it to see how to do the code generation.</span></span>

1. <span data-ttu-id="ef4e4-290">Visual Studio **Çözüm Gezgini**’nde, ToDoListAPI projesinde *ToDoListDataAPI* klasörünü silin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-290">In Visual Studio **Solution Explorer**, in the ToDoListAPI project, delete the *ToDoListDataAPI* folder.</span></span> <span data-ttu-id="ef4e4-291">**Dikkat: ToDoListDataAPI projesini değil, yalnızca klasörü silin.**</span><span class="sxs-lookup"><span data-stu-id="ef4e4-291">**Caution: Delete only the folder, not the ToDoListDataAPI project.**</span></span>
   
    ![Oluşturulan istemci kodunu silme](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    <span data-ttu-id="ef4e4-293">Bu klasör, üzerinden geçmek üzere olduğunuz kod oluşturma işlemi kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-293">This folder was created by using the code generation process that you're about to go through.</span></span>
2. <span data-ttu-id="ef4e4-294">ToDoListAPI projesine sağ tıklayın ve ardından **Ekle > REST API İstemci**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-294">Right-click the ToDoListAPI project, and then click **Add > REST API Client**.</span></span>
   
    ![Visual Studio'da REST API istemcisi ekleme](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. <span data-ttu-id="ef4e4-296">**REST API İstemci Ekle** iletişim kutusunda, **Swagger URL’si**’ne tıklayın ve ardından **Azure Varlığını Seç**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-296">In the **Add REST API Client** dialog box, click **Swagger URL**, and then click **Select Azure Asset**.</span></span>
   
    ![Azure Varlığını Seç](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. <span data-ttu-id="ef4e4-298">**App Service** iletişim kutusunda, bu öğretici için kullandığınız kaynak grubunu genişletin ve API uygulamanızı seçin ve ardından **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-298">In the **App Service** dialog box, expand the resource group you're using for this tutorial and select your API app, and then click **OK**.</span></span>
   
    ![Kod oluşturma için API uygulaması seçme](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    <span data-ttu-id="ef4e4-300">**REST API İstemcisi Ekle** iletişim kutusuna döndüğünüzde, metin kutusunun portalda daha önce gördüğünüz API tanımı URL değeriyle doldurulduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-300">Notice that when you return to the **Add REST API Client** dialog, the text box has been filled in with the API definition URL value that you saw earlier in the portal.</span></span>
   
    ![API Tanımı URL'si](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > <span data-ttu-id="ef4e4-302">Kod oluşturma için meta verileri almanın alternatif bir yolu, gözat iletişim kutusunu kullanmak yerine doğrudan URL'yi girmektir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-302">An alternative way to get metadata for code generation is to enter the URL directly instead of going through the browse dialog.</span></span> <span data-ttu-id="ef4e4-303">Veya Azure’a dağıtmadan önce istemci kodunu oluşturmak istiyorsanız, Web API projesini yerel olarak çalıştırabilir, Swagger JSON dosyasını sağlayan URL’ye gidebilir, dosyayı kaydedebilir ve **Mevcut bir Swagger meta veri dosyasını seç** seçeneğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-303">Or if you want to generate client code before deploying to Azure, you could run the Web API project locally, go to the URL that provides the Swagger JSON file, save the file, and use the **Select an existing Swagger metadata file** option.</span></span>
   > 
   > 
5. <span data-ttu-id="ef4e4-304">**REST API İstemcisi Ekle** iletişim kutusunda, **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-304">In the **Add REST API Client** dialog box, click **OK**.</span></span>
   
    <span data-ttu-id="ef4e4-305">Visual Studio API uygulamasının adını alan bir klasör oluşturur ve istemci sınıfları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-305">Visual Studio creates a folder named after the API app and generates client classes.</span></span>
   
    ![Oluşturulan istemci için kod dosyaları](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. <span data-ttu-id="ef4e4-307">ToDoListAPI projesinde, oluşturulan istemciyi kullanarak satır 40’ta API’yi çağıran kodu görmek için *Controllers\ToDoListController.cs*’yi açın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-307">In the ToDoListAPI project, open *Controllers\ToDoListController.cs* to see the code at line 40  that calls the API by using the generated client.</span></span>
   
    <span data-ttu-id="ef4e4-308">Aşağıdaki kod parçası, kodun istemci nesnesini nasıl başlattığını Alma yöntemini nasıl çağırdığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-308">The following snippet shows how the code instantiates the client object and calls the Get method.</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));
            return client;
        }
   
        public async Task<IEnumerable<ToDoItem>> Get()
        {
            using (var client = NewDataAPIClient())
            {
                var results = await client.ToDoList.GetByOwnerAsync(owner);
                return results.Select(m => new ToDoItem
                {
                    Description = m.Description,
                    ID = (int)m.ID,
                    Owner = m.Owner
                });
            }
        }
   
    <span data-ttu-id="ef4e4-309">Oluşturucu parametresi uç nokta URL’sini `toDoListDataAPIURL` uygulama ayarından alır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-309">The constructor parameter gets the endpoint URL from  the `toDoListDataAPIURL` app setting.</span></span> <span data-ttu-id="ef4e4-310">Uygulamayı yerel olarak çalıştırabilmeniz için, Web.config dosyasında, değer API projesinin yerel IIS Express URL’sine ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-310">In the Web.config file, that value is set to the local IIS Express URL of the API project so that you can run the application locally.</span></span> <span data-ttu-id="ef4e4-311">Oluşturucu parametresini atlarsanız, varsayılan uç nokta koddan oluşturulan URL'dir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-311">If you omit the constructor parameter, the default endpoint is the URL that you generated the code from.</span></span>
7. <span data-ttu-id="ef4e4-312">İstemci sınıfınız, API uygulaması adınıza göre farklı bir adla oluşturulacaktır; projenizde oluşturulanla tür adının eşleşmesi için, *Controllers\ToDoListController.cs*’deki kodda değişiklik yapın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-312">Your client class will be generated with a different name based on your API app name; change the code in *Controllers\ToDoListController.cs* so that the type name matches what was generated in your project.</span></span> <span data-ttu-id="ef4e4-313">Örneğin, API Uygulamanıza ToDoListDataAPI071316 adını verdiyseniz kodu değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ef4e4-313">For example, if you named your API App ToDoListDataAPI071316, you would change this code:</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

<span data-ttu-id="ef4e4-314">şu şekilde:</span><span class="sxs-lookup"><span data-stu-id="ef4e4-314">to this:</span></span>

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-to-host-the-middle-tier"></a><span data-ttu-id="ef4e4-315">Orta katmanı barındırmak için API uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ef4e4-315">Create an API app to host the middle tier</span></span>
<span data-ttu-id="ef4e4-316">Daha önce [veri katmanı API uygulaması oluşturdunuz ve kodu buna dağıttınız](#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="ef4e4-316">Earlier you [created the data tier API app and deployed code to it](#createapiapp).</span></span>  <span data-ttu-id="ef4e4-317">Şimdi orta katman API uygulaması için aynı yordamı izleyin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-317">Now you follow the same procedure for the middle tier API app.</span></span>

1. <span data-ttu-id="ef4e4-318">**Çözüm Gezgini**’nde, orta katman ToDoListAPI projesine (veri katmanı ToDoListDataAPI değil) sağ tıklayın ve ardından **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-318">In **Solution Explorer**, right-click the middle tier ToDoListAPI  project (not the data tier ToDoListDataAPI), and then click **Publish**.</span></span>
   
    ![Visual Studio’ya Yayımla'ya tıklama](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. <span data-ttu-id="ef4e4-320">**Web’de Yayımla** sihirbazının **Profil** sekmesinde, **Microsoft Azure App Service**’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-320">In the **Profile** tab of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="ef4e4-321">**App Service** iletişim kutusunda **Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-321">In the **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="ef4e4-322">**App Service Oluştur** iletişim kutusunun **Barındırma** sekmesinde, varsayılan **API Uygulaması Adı**’nı kabul edin ya da *azurewebsites.net* etki alanında benzersiz bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-322">In the **Hosting** tab of the **Create App Service** dialog box, accept the default **API App Name** or enter a name that is unique in the *azurewebsites.net* domain.</span></span>
5. <span data-ttu-id="ef4e4-323">Çalışmakta olduğunuz Azure **Aboneliğini** seçin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-323">Choose the Azure **Subscription** you have been using.</span></span>
6. <span data-ttu-id="ef4e4-324">**Kaynak Grubu** açılır listesinde, önceden oluşturduğunuz kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-324">In the **Resource Group** drop-down, choose the same resource group you created earlier.</span></span>
7. <span data-ttu-id="ef4e4-325">**App Service Planı** açılır listesinde, önceden oluşturduğunuz planı seçin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-325">In the **App Service Plan** drop-down, choose the same plan you created earlier.</span></span> <span data-ttu-id="ef4e4-326">Bu, bu değeri varsayılan olarak alır.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-326">It will default to that value.</span></span>
8. <span data-ttu-id="ef4e4-327">**Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-327">Click **Create**.</span></span>
   
    <span data-ttu-id="ef4e4-328">Visual Studio API uygulamasını oluşturur, bunun için bir yayımlama profili oluşturur ve **Web’i Yayımla** sihirbazının **Bağlantı** adımını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-328">Visual Studio creates the API app, creates a publish profile for it, and displays the **Connection** step of the **Publish Web** wizard.</span></span>
9. <span data-ttu-id="ef4e4-329">**Web’i Yayımla** sihirbazının **Bağlantı** adımında, **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-329">In the **Connection** step of the **Publish Web** wizard, click **Publish**.</span></span>
   
   <span data-ttu-id="ef4e4-330">Visual Studio, ToDoListAPI projesini yeni API uygulamasına dağıtır ve API uygulaması URL'sini bir tarayıcı penceresinde açar.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-330">Visual Studio deploys the ToDoListAPI project to the new API app and opens a browser to the URL of the API app.</span></span> <span data-ttu-id="ef4e4-331">"Başarıyla oluşturuldu" sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-331">The "successfully created" page appears.</span></span>

## <a name="configure-the-middle-tier-to-call-the-data-tier"></a><span data-ttu-id="ef4e4-332">Veri katmanını çağırmak için orta katmanı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ef4e4-332">Configure the middle tier to call the data tier</span></span>
<span data-ttu-id="ef4e4-333">Orta katman API uygulamasını çağırdıysanız, hala Web.config dosyasında bulunan localhost URL’sini kullanarak veri katmanını çağırmaya çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-333">If you called the middle tier API app now, it would try to call the data tier using the localhost URL that is still in the Web.config file.</span></span> <span data-ttu-id="ef4e4-334">Bu bölümde, veri katmanı API uygulaması URL’sini orta katman API uygulamasındaki bir ortam ayarına girersiniz.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-334">In this section you enter the data tier API app URL into an environment setting in the middle tier API app.</span></span> <span data-ttu-id="ef4e4-335">Orta katman API uygulamasındaki kod veri katmanı URL ayarını aldığında, ortam ayarı Web.config dosyasındakini geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-335">When the code in the middle tier API app retrieves the data tier URL setting, the environment setting will override what's in the Web.config file.</span></span>

1. <span data-ttu-id="ef4e4-336">[Azure portalına](https://portal.azure.com/) gidin ve ardından TodoListAPI (orta katman) projesini barındırmak için oluşturduğunuz **API uygulaması** dikey penceresine gidin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-336">Go to the [Azure portal](https://portal.azure.com/), and then navigate to the **API App** blade for the API app that you created to host the TodoListAPI (middle tier) project.</span></span>
2. <span data-ttu-id="ef4e4-337">API uygulamasının **Ayarlar** dikey penceresinde, **Uygulama ayarları**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-337">In the API App's **Settings** blade, click **Application settings**.</span></span>
3. <span data-ttu-id="ef4e4-338">API uygulamasının **Uygulama Ayarları** dikey penceresinde, **Uygulama Ayarları** bölümüne aşağı kaydırın ve aşağıdaki anahtarı ve değeri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-338">In the API App's **Application Settings** blade, scroll down to the **App settings** section and add the following key and value.</span></span> <span data-ttu-id="ef4e4-339">Bu değer bu öğreticide yayımladığınız birinci API Uygulamasının URL’sidir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-339">The value will be the URL of the first API App you published in this tutorial.</span></span>
   
   | <span data-ttu-id="ef4e4-340">**Anahtar**</span><span class="sxs-lookup"><span data-stu-id="ef4e4-340">**Key**</span></span> | <span data-ttu-id="ef4e4-341">toDoListDataAPIURL</span><span class="sxs-lookup"><span data-stu-id="ef4e4-341">toDoListDataAPIURL</span></span> |
   | --- | --- |
   | <span data-ttu-id="ef4e4-342">**Değer**</span><span class="sxs-lookup"><span data-stu-id="ef4e4-342">**Value**</span></span> |<span data-ttu-id="ef4e4-343">https://{your data tier API app name}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="ef4e4-343">https://{your data tier API app name}.azurewebsites.net</span></span> |
   | <span data-ttu-id="ef4e4-344">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="ef4e4-344">**Example**</span></span> |<span data-ttu-id="ef4e4-345">https://todolistdataapi.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="ef4e4-345">https://todolistdataapi.azurewebsites.net</span></span> |
4. <span data-ttu-id="ef4e4-346">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-346">Click **Save**.</span></span>
   
    ![Uygulama Ayarları için Kaydet’e tıklama](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    <span data-ttu-id="ef4e4-348">Kod Azure içinde çalıştığında, bu değer Web.config dosyasındaki localhost URL’sini geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-348">When the code runs in Azure, this value will now override the localhost URL that is in the Web.config file.</span></span>

## <a name="test"></a><span data-ttu-id="ef4e4-349">Test etme</span><span class="sxs-lookup"><span data-stu-id="ef4e4-349">Test</span></span>
1. <span data-ttu-id="ef4e4-350">Bir tarayıcı penceresinde, ToDoListAPI için oluşturduğunuz yeni orta katman API uygulamasının URL'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-350">In a browser window, browse to the URL of the new middle tier API app that you just created for ToDoListAPI.</span></span> <span data-ttu-id="ef4e4-351">Buraya portalda API uygulamasının ana dikey penceresindeki URL’ye tıklayarak gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-351">You can get there by clicking the URL in the API app's main blade in the portal.</span></span>
2. <span data-ttu-id="ef4e4-352">Tarayıcının adres çubuğundaki URL’ye "swagger" ifadesini ekleyin ve ardından Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-352">Add "swagger" to the URL in the browser's address bar, and then press Enter.</span></span> <span data-ttu-id="ef4e4-353">(URL `http://{apiappname}.azurewebsites.net/swagger` şeklindedir.)</span><span class="sxs-lookup"><span data-stu-id="ef4e4-353">(The URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
   
    <span data-ttu-id="ef4e4-354">Tarayıcı ToDoListDataAPI için daha önce gördüğünüzle aynı Swagger kullanıcı arabirimini görüntüler, ancak orta kamanı API uygulaması sizin için bu değeri veri katmanı API uygulamasına gönderdiği için Alma işlemi için `owner` şimdi gerekli bir alan değildir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-354">The browser displays the same Swagger UI that you saw earlier for ToDoListDataAPI, but now `owner` is not a required field for the Get operation, because the middle tier API app is sending that value to the data tier API app for you.</span></span> <span data-ttu-id="ef4e4-355">(Kimlik doğrulaması öğreticilerini gerçekleştirdiğinizde, orta katman `owner` parametresi için gerçek kullanıcı kimliklerini gönderir; şimdilik bu kodlanmış bir yıldız işaretidir.)</span><span class="sxs-lookup"><span data-stu-id="ef4e4-355">(When you do the authentication tutorials, the middle tier will send actual user IDs for the `owner` parameter; for now it is hard-coding an asterisk.)</span></span>
3. <span data-ttu-id="ef4e4-356">Orta katman API uygulamasının veri katmanı API uygulamasını başarılı şekilde çağırdığını doğrulamak için Alma yöntemini ve diğer yöntemleri deneyin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-356">Try out the Get method and the other methods to validate that the middle tier API app is successfully calling the data tier API app.</span></span>
   
    ![Swagger kullanıcı arabirimi Alma yöntemi](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a><span data-ttu-id="ef4e4-358">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="ef4e4-358">Troubleshooting</span></span>
<span data-ttu-id="ef4e4-359">Bu öğreticiyi izlerken bir sorunla karşılaşırsanız, bazı sorun giderme fikirlerini burada bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-359">In case you run into a problem as you go through this tutorial here are some troubleshooting ideas:</span></span>

* <span data-ttu-id="ef4e4-360">[.NET için Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003)’nin en yeni sürümünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-360">Make sure that you're using the latest version of the [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="ef4e4-361">İki proje adı benzerdir (ToDoListAPI, ToDoListDataAPI).</span><span class="sxs-lookup"><span data-stu-id="ef4e4-361">Two of the project names are similar (ToDoListAPI, ToDoListDataAPI).</span></span> <span data-ttu-id="ef4e4-362">Projeyle çalışırken bir şeylerinde yönergelerde açıklandığı gibi görünmüyorsa, doğru projeyi açtığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-362">If things don't look as described in the instructions when you are working with a project, make sure you have opened the correct project.</span></span>
* <span data-ttu-id="ef4e4-363">Kurumsal bir ağda bulunuyorsanız ve Azure App Service’e bir güvenlik duvarı aracılığıyla dağıtmaya çalışıyorsanız, 443 ve 8172 numaralı bağlantı noktalarının Web Dağıtımı için açık olduklarından emin olun.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-363">If you're on a corporate network and are trying to deploy to Azure App Service through a firewall, make sure that ports 443 and 8172 are open for Web Deploy.</span></span> <span data-ttu-id="ef4e4-364">Bu bağlantı noktalarını açamıyorsanız, diğer dağıtım yöntemlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-364">If you can't open those ports, you can use other deployment methods.</span></span>  <span data-ttu-id="ef4e4-365">Bkz. [Uygulamanızı Azure App Service’e dağıtma](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ef4e4-365">See [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md).</span></span>
* <span data-ttu-id="ef4e4-366">“Rota adları benzersiz olmalıdır” hataları - Yanlışlıkla bir API uygulamasına yanlış projeyi dağıttığınızda ve sonrasında doğru projeyi dağıtırsınız bu hataları alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-366">"Route names must be unique" errors -- you could get these if you accidentally deploy the wrong project to an API app and then later deploy the correct one to it.</span></span> <span data-ttu-id="ef4e4-367">Bu sorunu gidermek için, API uygulamasına doğru projeyi yeniden dağıtın ve **Web’i Yayımla** sihirbazının **Ayarlar** sekmesinde **Hedefteki ek dosyaları kaldır**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-367">To correct this, redeploy the correct project to the API app, and on the **Settings** tab of the **Publish Web** wizard select **Remove additional files at destination**.</span></span>

<span data-ttu-id="ef4e4-368">Azure App Service’de ASP.NET API uygulamanızı çalıştırdıktan sonra, sorun giderme sürecini kolaylaştıracak Visual Studio özellikleri hakkında daha fazla bilgi edinmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-368">After you have your ASP.NET API app running in Azure App Service, you may want to learn more about Visual Studio features that simplify troubleshooting.</span></span> <span data-ttu-id="ef4e4-369">Günlüğe kaydetme, uzaktan hata ayıklama ve çok daha fazlası hakkında bilgi edinmek için bkz. [Visual Studio’da Azure App Service uygulamalarının sorunlarını giderme](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="ef4e4-369">For information about logging, remote debugging, and more, see  [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef4e4-370">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ef4e4-370">Next steps</span></span>
<span data-ttu-id="ef4e4-371">Mevcut Web API projelerini API uygulamalarına dağıtmayı, API uygulamaları için istemci kodu oluşturmayı ve .NET istemcilerinden alınan API uygulamalarını kullanmayı gördünüz.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-371">You've seen how to deploy existing Web API projects to API apps, generate client code for API apps, and consume API apps from .NET clients.</span></span> <span data-ttu-id="ef4e4-372">Bu serideki sonraki öğretici, [JavaScript istemcilerden alınan API uygulamalarını kullanmak için CORS kullanma](app-service-api-cors-consume-javascript.md)yı gösterir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-372">The next tutorial in this series shows how to [use CORS to consume API apps from JavaScript clients](app-service-api-cors-consume-javascript.md).</span></span>

<span data-ttu-id="ef4e4-373">İstemci kodu oluşturma hakkında daha fazla bilgi için, GitHub.com’da [Azure/AutoRest](https://github.com/azure/autorest) deposuna bakın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-373">For more information about client code generation, see the [Azure/AutoRest](https://github.com/azure/autorest) repository on GitHub.com.</span></span> <span data-ttu-id="ef4e4-374">Oluşturulan istemciyi kullanma ile ilgili sorunlarda yardım için, [AutoRest deposunda bir sorun açın](https://github.com/azure/autorest/issues).</span><span class="sxs-lookup"><span data-stu-id="ef4e4-374">For help with problems using the generated client, open an [issue in the AutoRest repository](https://github.com/azure/autorest/issues).</span></span>

<span data-ttu-id="ef4e4-375">Sıfırdan yeni API uygulaması projeleri oluşturmak istiyorsanız, **Azure API Uygulaması** şablonu kullanın.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-375">If you want to create new API app projects from scratch, use the **Azure API App** template.</span></span>

![Visual Studio’da API Uygulaması şablonu](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

<span data-ttu-id="ef4e4-377">**Azure API Uygulaması** proje şablonu, **Boş** ASP.NET 4.5.2 şablonu seçmeye, Web API desteği eklemek için onay kutusuna tıklamaya ve Swashbuckle NuGet paketi yüklemeye eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-377">The **Azure API App** project template is equivalent to choosing the **Empty** ASP.NET 4.5.2 template, clicking the check box to add Web API support, and installing the Swashbuckle NuGet package.</span></span> <span data-ttu-id="ef4e4-378">Ayrıca, şablon yinelenen Swagger işlem kimlikleri oluşturulmasını önlemek için tasarlanmış bazı Swashbuckle yapılandırma kodları ekler.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-378">In addition, the template adds some Swashbuckle configuration code designed to prevent the creation of duplicate Swagger operation IDs.</span></span> <span data-ttu-id="ef4e4-379">Bir API uygulaması projesi oluşturduktan sonra, bu öğreticide gördüğünüz şekilde bunu bir API uygulamasına dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef4e4-379">Once you've created an API App project, you can deploy it to an API app the same way you saw in this tutorial.</span></span>

