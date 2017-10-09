---
title: "API uygulamaları ve App Service'te ASP.NET ile çalışmaya aaaGet | Microsoft Docs"
description: "Nasıl toocreate, dağıtmayı ve Azure App Service'te bir ASP.NET API uygulamasını Visual Studio 2015 kullanarak kullanmayı öğrenin."
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
ms.openlocfilehash: d3e90f1585907d183b0435c6cafc5585bc1e29ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a><span data-ttu-id="5ab5b-103">Azure App Service’de API Apps, ASP.NET ve Swagger kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="5ab5b-103">Get started with API Apps, ASP.NET, and Swagger in Azure App Service</span></span>
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="5ab5b-104">Merhaba ilk bir dizi budur nasıl toouse özelliklerini Azure uygulama hizmetine Göster öğreticileri geliştirmek ve RESTful API'lerini barındırmak için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-104">This is hello first in a series of tutorials that show how toouse features of Azure App Service that are helpful for developing and hosting RESTful APIs.</span></span>  <span data-ttu-id="5ab5b-105">Bu öğretici, Swagger biçiminde API meta veri desteğini ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-105">This tutorial covers support for API metadata in Swagger format.</span></span>

<span data-ttu-id="5ab5b-106">Şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="5ab5b-106">You'll learn:</span></span>

* <span data-ttu-id="5ab5b-107">Nasıl toocreate dağıtıp [API uygulamaları](app-service-api-apps-why-best-platform.md) Visual Studio 2015 yerleşik araçlarını kullanarak Azure App Service'te.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-107">How toocreate and deploy [API apps](app-service-api-apps-why-best-platform.md) in Azure App Service by using tools built into Visual Studio 2015.</span></span>
* <span data-ttu-id="5ab5b-108">Hello kullanarak tooautomate API bulma Swashbuckle NuGet paketini nasıl toodynamically Swagger API'si meta verilerini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-108">How tooautomate API discovery by using hello Swashbuckle NuGet package toodynamically generate Swagger API metadata.</span></span>
* <span data-ttu-id="5ab5b-109">Nasıl toouse Swagger API'si meta verileri tooautomatically bir API uygulaması için istemci kodu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-109">How toouse Swagger API metadata tooautomatically generate client code for an API app.</span></span>

## <a name="sample-application-overview"></a><span data-ttu-id="5ab5b-110">Örnek uygulamaya genel bakış</span><span class="sxs-lookup"><span data-stu-id="5ab5b-110">Sample application overview</span></span>
<span data-ttu-id="5ab5b-111">Bu öğreticide, bir basit bir yapılacaklar listesi örnek uygulaması ile çalışırsınız.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-111">In this tutorial, you work with a simple to-do list sample application.</span></span> <span data-ttu-id="5ab5b-112">Merhaba uygulaması tek sayfalı uygulama (SPA) ön uç, ASP.NET Web API'si Orta katmanına ve ASP.NET Web API'si veri katmanına sahip.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-112">hello application has a single-page application (SPA) front end, an ASP.NET Web API middle tier, and an ASP.NET Web API data tier.</span></span>

![API Apps örnek uygulama diyagramı](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

<span data-ttu-id="5ab5b-114">Merhaba ekran görüntüsü işte [AngularJS](https://angularjs.org/) ön uç.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-114">Here's a screen shot of hello [AngularJS](https://angularjs.org/) front end.</span></span>

![API Apps örnek uygulama toodo listesi](./media/app-service-api-dotnet-get-started/todospa.png)

<span data-ttu-id="5ab5b-116">Merhaba Visual Studio çözümü üç projeyi içerir:</span><span class="sxs-lookup"><span data-stu-id="5ab5b-116">hello Visual Studio solution includes three projects:</span></span>

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* <span data-ttu-id="5ab5b-117">**ToDoListAngular** -hello ön uç: hello Orta katmanı çağıran bir AngularJS SPA.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-117">**ToDoListAngular** - hello front end: an AngularJS SPA that calls hello middle tier.</span></span>
* <span data-ttu-id="5ab5b-118">**Todolistapı** -hello orta katman: yapılacak işler öğelerinde CRUD işlemleri tooperform hello veri katmanını çağıran bir ASP.NET Web API projesi.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-118">**ToDoListAPI** - hello middle tier: an ASP.NET Web API project that calls hello data tier tooperform CRUD operations on to-do items.</span></span>
* <span data-ttu-id="5ab5b-119">**Todolistdataapı** -hello veri katman: yapılacak işler öğelerinde CRUD işlemleri gerçekleştiren bir ASP.NET Web API projesi.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-119">**ToDoListDataAPI** - hello data tier:  an ASP.NET Web API project that performs CRUD operations on to-do items.</span></span>

<span data-ttu-id="5ab5b-120">Merhaba üç katmanlı yapı, API Apps kullanarak uygulayabileceğiniz ve burada yalnızca gösterim amacıyla kullanılan birçok mimarisi biridir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-120">hello three-tier architecture is one of many architectures that you can implement by using API Apps and is used here only for demonstration purposes.</span></span> <span data-ttu-id="5ab5b-121">Her katmandaki Hello kod olası toodemonstrate API Apps özelliklerini kadar basit hale getirir; Örneğin, hello veri katmanı Kalıcılık mekanizması olarak veritabanı yerine sunucu belleği kullanır.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-121">hello code in each tier is as simple as possible toodemonstrate API Apps features; for example, hello data tier uses server memory rather than a database as its persistence mechanism.</span></span>

<span data-ttu-id="5ab5b-122">Bu öğreticiyi tamamladığınızda, hello iki Web API projelerini ve App Service API uygulamalarında hello bulutta çalışan sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-122">On completing this tutorial, you'll have hello two Web API projects up and running in hello cloud in App Service API apps.</span></span>

<span data-ttu-id="5ab5b-123">Merhaba serideki sonraki öğretici Hello hello SPA ön uç toohello bulut dağıtır.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-123">hello next tutorial in hello series deploys hello SPA front end toohello cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ab5b-124">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5ab5b-124">Prerequisites</span></span>
* <span data-ttu-id="5ab5b-125">ASP.NET Web API - öğretici yönergeleri hello varsayın nasıl temel bilgiye sahip ASP.NET ile toowork [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-125">ASP.NET Web API - hello tutorial instructions assume you have a basic knowledge of how toowork with ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.</span></span>
* <span data-ttu-id="5ab5b-126">Azure hesabı - [Ücretsiz bir Azure hesabı açabilir](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) veya [Visual Studio abonelik avantajlarını etkinleştirebilirsiniz](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="5ab5b-126">Azure account - You can [Open an Azure account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
  
    <span data-ttu-id="5ab5b-127">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="5ab5b-127">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="5ab5b-128">Burada, Uygulama Hizmetleri’nde hemen bir kısa süreli başlangıç uygulaması oluşturabilirsiniz; **kredi kartı gerekmez** ve hiçbir taahhüt yoktur.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-128">There, you can immediately create a short-lived starter app in App Service — **no credit card required**, and no commitments.</span></span>
* <span data-ttu-id="5ab5b-129">Visual Studio 2015'hello ile [.NET için Azure SDK](https://azure.microsoft.com/downloads/archive-net-downloads/) -, zaten yoksa hello SDK Visual Studio 2015 otomatik olarak yükler..</span><span class="sxs-lookup"><span data-stu-id="5ab5b-129">Visual Studio 2015 with hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) - hello SDK installs Visual Studio 2015 automatically if you don't already have it.</span></span>
  
  * <span data-ttu-id="5ab5b-130">Visual Studio’da Yardım -> Microsoft Visual Studio Hakkında’ya tıklayın ve "Azure App Service Tools v2.9.1" veya sonraki bir sürümün yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-130">In Visual Studio, click Help -> About Microsoft Visual Studio and ensure that you have "Azure App Service Tools v2.9.1" or higher installed.</span></span>
    
    ![Azure App Tools sürümü](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > <span data-ttu-id="5ab5b-132">Merhaba SDK bağımlılıkları kaç makinenizde zaten bağlı olarak, yükleme hello SDK tooa yarım saat veya daha fazla birkaç dakikadan uzun bir zaman ele geçirebilir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-132">Depending on how many of hello SDK dependencies you already have on your machine, installing hello SDK could take a long time, from several minutes tooa half hour or more.</span></span>
    > 
    > 

## <a name="download-hello-sample-application"></a><span data-ttu-id="5ab5b-133">Merhaba örnek uygulamayı indirin</span><span class="sxs-lookup"><span data-stu-id="5ab5b-133">Download hello sample application</span></span>
1. <span data-ttu-id="5ab5b-134">Merhaba karşıdan [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) deposu.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-134">Download hello [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repository.</span></span>
   
    <span data-ttu-id="5ab5b-135">Merhaba tıklayabilirsiniz **ZIP'i indir** yerel makinenizde düğmesini veya kopya hello deposu.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-135">You can click hello **Download ZIP** button or clone hello repository on your local machine.</span></span>
2. <span data-ttu-id="5ab5b-136">Visual Studio 2015 veya 2013 Hello ToDoList çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-136">Open hello ToDoList solution in Visual Studio 2015 or 2013.</span></span>
   
   1. <span data-ttu-id="5ab5b-137">Her çözüm tootrust gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-137">You will need tootrust each solution.</span></span>
         <span data-ttu-id="5ab5b-138">![Güvenlik Uyarısı](./media/app-service-api-dotnet-get-started/securitywarning.png)</span><span class="sxs-lookup"><span data-stu-id="5ab5b-138">![Security Warning](./media/app-service-api-dotnet-get-started/securitywarning.png)</span></span>
3. <span data-ttu-id="5ab5b-139">Merhaba çözüm (CTRL + SHIFT + B) toorestore hello NuGet paketleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-139">Build hello solution (CTRL + SHIFT + B)  toorestore hello NuGet packages.</span></span>
   
    <span data-ttu-id="5ab5b-140">Dağıtmadan önce toosee hello uygulama işleminde isterseniz, yerel olarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-140">If you want toosee hello application in operation before you deploy it, you can run it locally.</span></span> <span data-ttu-id="5ab5b-141">Todolistdataapı başlangıç projesi ve çalışma hello çözümü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-141">Make sure that ToDoListDataAPI is your startup project and run hello solution.</span></span> <span data-ttu-id="5ab5b-142">Tarayıcınızda toosee HTTP 403 hata beklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-142">You should expect toosee a HTTP 403 error in your browser.</span></span>

## <a name="use-swagger-api-metadata-and-ui"></a><span data-ttu-id="5ab5b-143">Swagger API meta verileri ve kullanıcı arabirimi kullanma</span><span class="sxs-lookup"><span data-stu-id="5ab5b-143">Use Swagger API metadata and UI</span></span>
<span data-ttu-id="5ab5b-144">[Swagger](http://swagger.io/) 2.0 API meta verileri desteği Azure App Service’de yerleşiktir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-144">Support for [Swagger](http://swagger.io/) 2.0 API metadata is built into Azure App Service.</span></span> <span data-ttu-id="5ab5b-145">Her API uygulama meta verileri hello API için Swagger JSON biçiminde döndüren bir URL uç noktası belirtebilir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-145">Each API app can specify a URL endpoint that returns metadata for hello API in Swagger JSON format.</span></span> <span data-ttu-id="5ab5b-146">Merhaba Bu uç noktadan döndürülen meta veri olabilir toogenerate istemci kodu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-146">hello metadata returned from that endpoint can be used toogenerate client code.</span></span>

<span data-ttu-id="5ab5b-147">Bir ASP.NET Web API projesi dinamik olarak Swagger meta verileri hello kullanarak oluşturabilirsiniz [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-147">An ASP.NET Web API project can dynamically generate Swagger metadata by using hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package.</span></span> <span data-ttu-id="5ab5b-148">Merhaba Swashbuckle NuGet paketi indirdiğiniz hello Todolistdataapı ve Todolistapı projelerinde zaten yüklüdür.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-148">hello Swashbuckle NuGet package is already installed in hello ToDoListDataAPI and ToDoListAPI projects that you downloaded.</span></span>

<span data-ttu-id="5ab5b-149">Merhaba öğreticinin bu bölümünde, oluşturulan hello Swagger 2.0 meta verileri oluşturmayı inceler ve ardından hello Swagger meta verileri temel alan UI test çıkışı deneyin.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-149">In this section of hello tutorial, you look at hello generated Swagger 2.0 metadata, and then you try out a test UI that is based on hello Swagger metadata.</span></span>

1. <span data-ttu-id="5ab5b-150">Merhaba Todolistdataapı projesini ayarlayın (**değil** hello Todolistapı projesi) hello başlangıç projesi olarak.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-150">Set hello ToDoListDataAPI project (**not** hello ToDoListAPI project) as hello startup project.</span></span>
   
    ![ToDoDataAPI ayarını Başlangıç Projesi olarak belirleyin](./media/app-service-api-dotnet-get-started/startupproject.png)
2. <span data-ttu-id="5ab5b-152">F5 tuşuna basın veya tıklatın **hata ayıklama > hata ayıklamayı Başlat** toorun Merhaba projeyi hata ayıklama modunda.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-152">Press F5 or click **Debug > Start Debugging** toorun hello project in debug mode.</span></span>
   
    <span data-ttu-id="5ab5b-153">Merhaba tarayıcı açar ve hello HTTP 403 hata sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-153">hello browser opens and shows hello HTTP 403 error page.</span></span>
3. <span data-ttu-id="5ab5b-154">Tarayıcınızın adres çubuğuna, ekleme `swagger/docs/v1` toohello sonuna hello satır ve Return tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-154">In your browser address bar, add `swagger/docs/v1` toohello end of hello line, and then press Return.</span></span> <span data-ttu-id="5ab5b-155">(URL hello `http://localhost:45914/swagger/docs/v1`.)</span><span class="sxs-lookup"><span data-stu-id="5ab5b-155">(hello URL is `http://localhost:45914/swagger/docs/v1`.)</span></span>
   
    <span data-ttu-id="5ab5b-156">Bu API hello için Swashbuckle tooreturn Swagger 2.0 JSON meta verileri tarafından kullanılan hello varsayılan URL'dir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-156">This is hello default URL used by Swashbuckle tooreturn Swagger 2.0 JSON metadata for hello API.</span></span>
   
    <span data-ttu-id="5ab5b-157">Merhaba tarayıcı Internet Explorer kullanıyorsanız, toodownload ister bir *v1.json* dosya.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-157">If you're using Internet Explorer, hello browser prompts you toodownload a *v1.json* file.</span></span>
   
    ![IE’de JSON meta veriler indirme](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    <span data-ttu-id="5ab5b-159">Chrome, Firefox veya Microsoft Edge kullanıyorsanız, hello tarayıcı hello tarayıcı penceresinde hello JSON görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-159">If you're using Chrome, Firefox, or Edge, hello browser displays hello JSON in hello browser window.</span></span> <span data-ttu-id="5ab5b-160">Farklı tarayıcılar JSON dosyasını farklı şekilde işler ve tarayıcı pencereniz tam olarak hello örnekteki gibi görünmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-160">Different browsers handle JSON differently, and your browser window may not look exactly like hello example.</span></span>
   
    ![Chrome’da JSON meta verileri](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    <span data-ttu-id="5ab5b-162">Merhaba aşağıdaki örnek hello ilk bölümü hello hello API, Swagger meta verilerini gösterir hello için hello tanımıyla yöntemi alın.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-162">hello following sample shows hello first section of hello Swagger metadata for hello API, with hello definition for hello Get method.</span></span> <span data-ttu-id="5ab5b-163">Bu meta veriler, hangi sürücü hello Swagger hello aşağıdaki adımları kullanın ve hello öğretici tooautomatically daha sonraki bir bölüme kullanın UI istemci kodu oluştur ' dir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-163">This metadata is what drives hello Swagger UI that you use in hello following steps, and you use it in a later section of hello tutorial tooautomatically generate client code.</span></span>
   
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
4. <span data-ttu-id="5ab5b-164">Merhaba tarayıcınızı kapatın ve Visual Studio hata ayıklamayı durdurun.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-164">Close hello browser and stop Visual Studio debugging.</span></span>
5. <span data-ttu-id="5ab5b-165">Merhaba Todolistdataapı proje **Çözüm Gezgini**açın hello *App_Start\SwaggerConfig.cs* dosya ve sonra aşağı tooline 174 ve koddan hello açıklamadan çıkarın kaydırma.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-165">In hello ToDoListDataAPI project in **Solution Explorer**, open hello *App_Start\SwaggerConfig.cs* file, then scroll down tooline 174 and uncomment hello following code.</span></span>
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    <span data-ttu-id="5ab5b-166">Merhaba *SwaggerConfig.cs* dosya projede hello Swashbuckle paketini yüklediğinizde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-166">hello *SwaggerConfig.cs* file is created when you install hello Swashbuckle package in a project.</span></span> <span data-ttu-id="5ab5b-167">Merhaba dosya yolları tooconfigure Swashbuckle sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-167">hello file provides a number of ways tooconfigure Swashbuckle.</span></span>
   
    <span data-ttu-id="5ab5b-168">Swagger aşağıdaki hello kullanan kullanıcı Arabirimi adımları etkinleştirir hello kaldırdığını hello kodu.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-168">hello code you've uncommented enables hello Swagger UI that you use in hello following steps.</span></span> <span data-ttu-id="5ab5b-169">Hello API uygulaması proje şablonunu kullanarak bir Web API projesi oluşturduğunuzda, bu kod çıkışı varsayılan olarak bir güvenlik önlemi olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-169">When you create a Web API project by using hello API app project template, this code is commented out by default as a security measure.</span></span>
6. <span data-ttu-id="5ab5b-170">Merhaba projeyi tekrar çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-170">Run hello project again.</span></span>
7. <span data-ttu-id="5ab5b-171">Tarayıcınızın adres çubuğuna, ekleme `swagger` toohello sonuna hello satır ve Return tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-171">In your browser address bar, add `swagger` toohello end of hello line, and then press Return.</span></span> <span data-ttu-id="5ab5b-172">(URL hello `http://localhost:45914/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="5ab5b-172">(hello URL is `http://localhost:45914/swagger`.)</span></span>
8. <span data-ttu-id="5ab5b-173">Merhaba Swagger kullanıcı Arabirimi sayfası görüntülendiğinde **ToDoList** toosee hello yöntemler kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-173">When hello Swagger UI page appears, click **ToDoList** toosee hello methods available.</span></span>
   
    ![Swagger kullanıcı arabirimi kullanılabilir yöntemleri](./media/app-service-api-dotnet-get-started/methods.png)
9. <span data-ttu-id="5ab5b-175">Merhaba ilk tıklatın **almak** hello listesinde düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-175">Click hello first **Get** button in hello list.</span></span>
10. <span data-ttu-id="5ab5b-176">Merhaba, **parametreleri** bölümünde, hello hello değeri olarak bir yıldız işareti girin `owner` parametre ve ardından **deneyin**.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-176">In hello **Parameters** section, enter an asterisk as hello value of hello `owner` parameter, and then click **Try it out**.</span></span>
    
    <span data-ttu-id="5ab5b-177">Sonraki öğreticilerde kimlik doğrulama eklediğinizde, orta katman hello hello gerçek kullanıcı kimliği toohello veri katmanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-177">When you add authentication in later tutorials, hello middle tier will provide hello actual user ID toohello data tier.</span></span> <span data-ttu-id="5ab5b-178">Hello uygulama kimlik doğrulama etkin olmadan çalışırken şu an için tüm görevler kendi sahibinin kimliği yıldız işareti olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-178">For now, all tasks will have asterisk as their owner ID while hello application runs without authentication enabled.</span></span>
    
    ![Swagger kullanıcı arabirimini deneyin](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    <span data-ttu-id="5ab5b-180">Merhaba Swagger kullanıcı arabirimini hello ToDoList alma yöntemini çağırır ve hello yanıt kodunu ve JSON sonuçlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-180">hello Swagger UI calls hello ToDoList Get method and displays hello response code and JSON results.</span></span>
    
    ![Swagger kullanıcı arabirimini deneyin sonuçları](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. <span data-ttu-id="5ab5b-182">Tıklatın **Post**ve ardından hello kutusunda altında **Model şeması**.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-182">Click **Post**, and then click hello box under **Model Schema**.</span></span>
    
    <span data-ttu-id="5ab5b-183">Merhaba hello Post yöntemi için parametre değeri belirtebileceğiniz hello model şeması prefills hello giriş kutusunu tıklatarak.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-183">Clicking hello model schema prefills hello input box where you can specify hello parameter value for hello Post method.</span></span> <span data-ttu-id="5ab5b-184">(Internet Explorer'da bu işe yaramazsa, farklı bir tarayıcı kullanın veya hello parametre değeri hello sonraki adımda el ile girebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="5ab5b-184">(If this doesn't work in Internet Explorer, use a different browser or enter hello parameter value manually in hello next step.)</span></span>  
    
    ![Swagger kullanıcı arabirimini deneyin Gönder](./media/app-service-api-dotnet-get-started/post.png)
12. <span data-ttu-id="5ab5b-186">Değişiklik hello JSON hello `todo` giriş parametresi aşağıdaki örneğine hello gibi görünüyor. böylece kutusunda ya da kendi açıklama metninizle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="5ab5b-186">Change hello JSON in hello `todo` parameter input box so that it looks like hello following example, or substitute your own description text:</span></span>
    
        {
          "ID": 2,
          "Description": "buy hello dog a toy",
          "Owner": "*"
        }
13. <span data-ttu-id="5ab5b-187">**Deneyin**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-187">Click **Try it out**.</span></span>
    
    <span data-ttu-id="5ab5b-188">Merhaba ToDoList API başarı belirten bir HTTP 204 yanıtı döndürür.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-188">hello ToDoList API returns an HTTP 204 response code that indicates success.</span></span>
14. <span data-ttu-id="5ab5b-189">Merhaba ilk tıklatın **almak** düğmesini tıklatın ve ardından hello sayfanın bu bölümünde hello tıklatın **deneyin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-189">Click hello first **Get** button, and then in that section of hello page click hello **Try it out** button.</span></span>
    
    <span data-ttu-id="5ab5b-190">Merhaba Get yöntemi yanıtı şimdi hello yeni toodo öğesi içerir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-190">hello Get method response now includes hello new toodo item.</span></span>
15. <span data-ttu-id="5ab5b-191">İsteğe bağlı: hello Put, Delete, ayrıca deneyin ve kimliği yöntemlerle alın.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-191">Optional: Try also hello Put, Delete, and Get by ID methods.</span></span>
16. <span data-ttu-id="5ab5b-192">Merhaba tarayıcınızı kapatın ve Visual Studio hata ayıklamayı durdurun.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-192">Close hello browser and stop Visual Studio debugging.</span></span>

<span data-ttu-id="5ab5b-193">Swashbuckle her ASP.NET Web API projesi ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-193">Swashbuckle works with any ASP.NET Web API project.</span></span> <span data-ttu-id="5ab5b-194">Tooadd Swagger meta veri oluşturma tooan mevcut proje istiyorsanız, yalnızca hello Swashbuckle paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-194">If you want tooadd Swagger metadata generation tooan existing project, just install hello Swashbuckle package.</span></span>

> [!NOTE]
> <span data-ttu-id="5ab5b-195">Swagger meta verileri her API işlemi için benzersiz bir kimlik içerir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-195">Swagger metadata includes a unique ID for each API operation.</span></span> <span data-ttu-id="5ab5b-196">Varsayılan olarak, Swashbuckle Web API denetleyicisi yöntemleriniz için yinelenen Swagger işlemi kimlikleri oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-196">By default, Swashbuckle may generate duplicate Swagger operation IDs for your Web API controller methods.</span></span> <span data-ttu-id="5ab5b-197">Bu durum, denetleyiciniz `Get()` ve `Get(id)` gibi, HTTP yöntemleriyle aşırı yüklü olduğunda gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-197">This happens if your controller has overloaded HTTP methods, such as `Get()` and `Get(id)`.</span></span> <span data-ttu-id="5ab5b-198">Nasıl toohandle aşırı yüklemeler hakkında daha fazla bilgi için bkz: [özelleştirme Swashbuckle tarafından oluşturulan API tanımlarını](app-service-api-dotnet-swashbuckle-customize.md).</span><span class="sxs-lookup"><span data-stu-id="5ab5b-198">For information about how toohandle overloads, see [Customize Swashbuckle-generated API definitions](app-service-api-dotnet-swashbuckle-customize.md).</span></span> <span data-ttu-id="5ab5b-199">Visual Studio'da hello Azure API uygulaması şablonu kullanarak bir Web API projesi oluşturursanız, benzersiz işlem kimlikleri oluşturan kod otomatik olarak toohello eklenen *SwaggerConfig.cs* dosya.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-199">If you create a Web API project in Visual Studio by using hello Azure API App template, code that generates unique operation IDs is automatically added toohello *SwaggerConfig.cs* file.</span></span>  
> 
> 

## <span data-ttu-id="5ab5b-200"><a id="createapiapp"></a>Azure'da API uygulaması oluşturma ve kod tooit dağıtma</span><span class="sxs-lookup"><span data-stu-id="5ab5b-200"><a id="createapiapp"></a> Create an API app in Azure and deploy code tooit</span></span>
<span data-ttu-id="5ab5b-201">Bu bölümde, Visual Studio hello tümleştirilmiştir Azure araçlarını kullanırsınız **Web'i Yayımla** Sihirbazı toocreate yeni bir API uygulamasına.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-201">In this section, you use Azure tools that are integrated into hello Visual Studio **Publish Web** wizard toocreate a new API app in Azure.</span></span> <span data-ttu-id="5ab5b-202">Ardından hello Todolistdataapı projesi toohello yeni API uygulamasına dağıtmak ve hello Swagger kullanıcı arabirimini çalıştırarak hello API çağrısı.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-202">Then you deploy hello ToDoListDataAPI project toohello new API app and call hello API by running hello Swagger UI.</span></span>

1. <span data-ttu-id="5ab5b-203">İçinde **Çözüm Gezgini**hello Todolistdataapı projesine sağ tıklayın ve ardından **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-203">In **Solution Explorer**, right-click hello ToDoListDataAPI project, and then click **Publish**.</span></span>
   
    ![Visual Studio’ya Yayımla'ya tıklama](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. <span data-ttu-id="5ab5b-205">Merhaba, **profil** hello adımında **Web'i Yayımla** Sihirbazı'nı tıklatın **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-205">In hello **Profile** step of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
   
   ![Web’de Yayımla sihirbazında Azure App Service’e tıklama](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. <span data-ttu-id="5ab5b-207">Zaten yapmadıysanız tooyour Azure hesabı oturum veya süresi dolduysa, kimlik bilgilerinizi yenileyin.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-207">Sign in tooyour Azure account if you have not already done so, or refresh your credentials if they're expired.</span></span>
4. <span data-ttu-id="5ab5b-208">Buna hello App Service iletişim kutusunda, hello Azure'ı seçin **abonelik** toouse istediğiniz ve ardından **yeni**.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-208">In hello App Service dialog box, choose hello Azure **Subscription** you want toouse, and then click **New**.</span></span>
   
    ![App Service iletişim kutusunda Yeni’ye tıklama](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    <span data-ttu-id="5ab5b-210">Merhaba **barındırma** hello sekmesinde **App Service Oluştur** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-210">hello **Hosting** tab of hello **Create App Service** dialog box appears.</span></span>
   
    <span data-ttu-id="5ab5b-211">Swashbuckle yüklü olan bir Web API projesi dağıttığınız için Visual Studio bir API uygulaması toocreate istediğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-211">Because you're deploying a Web API project that has Swashbuckle installed, Visual Studio assumes that you want toocreate an API App.</span></span> <span data-ttu-id="5ab5b-212">Bu hello tarafından belirtilir **API uygulaması adı** başlık ve tarafından bu hello olgu hello **türünü değiştir** aşağı açılan liste çok ayarlamak**API uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-212">This is indicated by hello **API App Name** title and by hello fact that hello **Change Type** drop-down list is set too**API App**.</span></span>
   
    ![App Service iletişim kutusunda Uygulama türü](./media/app-service-api-dotnet-get-started/apptype.png)
5. <span data-ttu-id="5ab5b-214">Girin bir **API uygulaması adı** hello benzersiz *azurewebsites.net* etki alanı.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-214">Enter an **API App Name** that is unique in hello *azurewebsites.net* domain.</span></span> <span data-ttu-id="5ab5b-215">Visual Studio'nun önerdiği hello varsayılan adı kabul edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-215">You can accept hello default name that Visual Studio proposes.</span></span>
   
    <span data-ttu-id="5ab5b-216">Başka birinin önceden kullandığı bir adı girerseniz, kırmızı bir ünlem işareti toohello sağ bakın.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-216">If you enter a name that someone else has already used, you see a red exclamation mark toohello right.</span></span>
   
    <span data-ttu-id="5ab5b-217">Merhaba hello API uygulamasının URL'si olacaktır `{API app name}.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-217">hello URL of hello API app will be `{API app name}.azurewebsites.net`.</span></span>
6. <span data-ttu-id="5ab5b-218">Merhaba, **kaynak grubu** açılır menüsünde tıklatın **yeni**ve ardından isterseniz "isterseniz ToDoListGroup" ya da başka bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-218">In hello **Resource Group** drop-down, click **New**, and then enter "ToDoListGroup" or another name if you prefer.</span></span>
   
    <span data-ttu-id="5ab5b-219">Kaynak grubu API uygulamaları, veritabanları, sanal makineler ve benzerleri gibi Azure kaynakları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-219">A resource group is a collection of Azure resources such as API apps, databases, VMs, and so forth.</span></span>    <span data-ttu-id="5ab5b-220">Kolay toodelete tüm hello öğretici için oluşturduğunuz Azure kaynaklarını hello tek bir adımda kolaylaştırır Bu öğretici için en iyi toocreate yeni bir kaynak grubu demektir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-220">For this tutorial, it's best toocreate a new resource group because that makes it easy toodelete in one step all hello Azure resources that you create for hello tutorial.</span></span>
   
    <span data-ttu-id="5ab5b-221">Bu kutu mevcut [kaynak grubunu](../azure-resource-manager/resource-group-overview.md) seçmenize ya da aboneliklerinizdeki kaynak grubunda olanlardan farklı bir ad yazarak yeni bir tane oluşturmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-221">This box lets you select an existing [resource group](../azure-resource-manager/resource-group-overview.md) or create a new one by typing in a name that is different from any existing resource group in your subscription.</span></span>
7. <span data-ttu-id="5ab5b-222">Merhaba tıklatın **yeni** düğmesine bir sonraki toohello **App Service planı** açılır.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-222">Click hello **New** button next toohello **App Service Plan** drop-down.</span></span>
   
    <span data-ttu-id="5ab5b-223">Merhaba gösteren ekran görüntüsü için örnek değerleri **API uygulaması adı**, **abonelik**, ve **kaynak grubu** --değerlerinizi farklı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-223">hello screen shot shows sample values for **API App Name**, **Subscription**, and **Resource Group** -- your values will be different.</span></span>
   
    ![App Service iletişim kutusu oluşturma](./media/app-service-api-dotnet-get-started/createas.png)
   
    <span data-ttu-id="5ab5b-225">Aşağıdaki adımları hello hello yeni kaynak grubu için bir uygulama hizmeti planı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-225">In hello following steps you create an App Service plan for hello new resource group.</span></span> <span data-ttu-id="5ab5b-226">Bir uygulama hizmeti planı, API uygulamanızın üzerinde çalışacağı hello işlem kaynaklarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-226">An App Service plan specifies hello compute resources that your API app runs on.</span></span> <span data-ttu-id="5ab5b-227">Örneğin, hello ücretsiz katmanı seçerseniz API uygulamanız paylaşılan Vm'lerinde bazı Ücretli katmanlarda ayrılmış sanal makine çalışırken çalışır.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-227">For example, if you choose hello free tier, your API app runs on shared VMs, while for some paid tiers it runs on dedicated VMs.</span></span> <span data-ttu-id="5ab5b-228">App Service planları hakkında bilgi için bkz. [App Service planlarına genel bakış](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ab5b-228">For information about App Service plans, see [App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
8. <span data-ttu-id="5ab5b-229">Merhaba, **App Service planı Yapılandır** iletişim kutusunda, tercih ederseniz, "ToDoListPlan" ya da başka bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-229">In hello **Configure App Service Plan** dialog, enter "ToDoListPlan" or another name if you prefer.</span></span>
9. <span data-ttu-id="5ab5b-230">Merhaba, **konumu** aşağı açılan listesinde, en yakın tooyou hello konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-230">In hello **Location** drop-down list, choose hello location that is closest tooyou.</span></span>
   
    <span data-ttu-id="5ab5b-231">Bu ayar, uygulamanızın hangi Azure veri merkezinde çalıştırılacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-231">This setting specifies which Azure datacenter your app will run in.</span></span> <span data-ttu-id="5ab5b-232">Bir konum kapatmak tooyou toominimize seçin [gecikme](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span><span class="sxs-lookup"><span data-stu-id="5ab5b-232">Choose a location close tooyou toominimize [latency](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span></span>
10. <span data-ttu-id="5ab5b-233">Merhaba, **boyutu** açılır menüsünde tıklatın **serbest**.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-233">In hello **Size** drop-down, click **Free**.</span></span>
    
    <span data-ttu-id="5ab5b-234">Bu öğretici için hello ücretsiz fiyatlandırma katmanı yeterli ölçüde performans sunacaktır.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-234">For this tutorial, hello free pricing tier will provide sufficient performance.</span></span>
11. <span data-ttu-id="5ab5b-235">Merhaba, **App Service planı Yapılandır** iletişim kutusunda, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-235">In hello **Configure App Service Plan** dialog, click **OK**.</span></span>
    
    ![App Service Planı Yapılandır iletişim kutusunda Tamam’a tıklama](./media/app-service-api-dotnet-get-started/configasp.png)
12. <span data-ttu-id="5ab5b-237">Merhaba, **App Service Oluştur** iletişim kutusu, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-237">In hello **Create App Service** dialog box, click **Create**.</span></span>
    
    ![App Service Oluştur iletişim kutusunda Oluştur’a tıklama](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    <span data-ttu-id="5ab5b-239">Visual Studio hello API uygulaması ve tüm gerekli hello ayarlarını hello API uygulaması için sahip bir yayımlama profili oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-239">Visual Studio creates hello API app and a publish profile that has all of hello required settings for hello API app.</span></span> <span data-ttu-id="5ab5b-240">Merhaba açar sonra **Web'i Yayımla** kullanacağınız Sihirbazı toodeploy hello projesi.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-240">Then it opens hello **Publish Web** wizard, which you'll use toodeploy hello project.</span></span>
    
    <span data-ttu-id="5ab5b-241">Merhaba **Web'i Yayımla** Sihirbazı açılır hello üzerinde **bağlantı** sekmesidir (aşağıda gösterilen).</span><span class="sxs-lookup"><span data-stu-id="5ab5b-241">hello **Publish Web** wizard opens on hello **Connection** tab (shown below).</span></span>
    
    <span data-ttu-id="5ab5b-242">Merhaba üzerinde **bağlantı** hello sekmesinde, **Server** ve **Site adı** ayarları noktası tooyour API uygulaması.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-242">On hello **Connection** tab, hello **Server** and **Site name** settings point tooyour API app.</span></span> <span data-ttu-id="5ab5b-243">Merhaba **kullanıcı adı** ve **parola** Azure'un sizin için oluşturduğu dağıtım kimlik bilgileridir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-243">hello **User name** and **Password** are deployment credentials that Azure creates for you.</span></span> <span data-ttu-id="5ab5b-244">Dağıtımdan sonra Visual Studio tarayıcı toohello açılır **hedef URL** (Merhaba tek amacıdır olan **hedef URL**).</span><span class="sxs-lookup"><span data-stu-id="5ab5b-244">After deployment, Visual Studio opens a browser toohello **Destination URL** (that's hello only purpose for **Destination URL**).</span></span>  
13. <span data-ttu-id="5ab5b-245">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-245">Click **Next**.</span></span>
    
    ![Web'i Yayımla sihirbazının Bağlantı sekmesinde İleri'ye tıklama](./media/app-service-api-dotnet-get-started/connnext.png)
    
    <span data-ttu-id="5ab5b-247">Merhaba sonraki sekme kullanılabilir hello **ayarları** sekmesidir (aşağıda gösterilen).</span><span class="sxs-lookup"><span data-stu-id="5ab5b-247">hello next tab is hello **Settings** tab (shown below).</span></span> <span data-ttu-id="5ab5b-248">Burada bir hata ayıklama derlemesi için hello derleme yapılandırma sekmesini toodeploy değiştirebilirsiniz [uzaktan hata ayıklama](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span><span class="sxs-lookup"><span data-stu-id="5ab5b-248">Here you can change hello build configuration tab toodeploy a debug build for [remote debugging](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span></span> <span data-ttu-id="5ab5b-249">Merhaba ayrıca sekmede birkaç farklı **dosya yayımlama seçeneği**:</span><span class="sxs-lookup"><span data-stu-id="5ab5b-249">hello tab also offers several **File Publish Options**:</span></span>
    
    * <span data-ttu-id="5ab5b-250">Hedefteki ek dosyaları kaldır</span><span class="sxs-lookup"><span data-stu-id="5ab5b-250">Remove additional files at destination</span></span>
    * <span data-ttu-id="5ab5b-251">Yayımlama sırasında ön derleme yap</span><span class="sxs-lookup"><span data-stu-id="5ab5b-251">Precompile during publishing</span></span>
    * <span data-ttu-id="5ab5b-252">Merhaba App_Data klasöründeki dosyaları dışarıda bırak</span><span class="sxs-lookup"><span data-stu-id="5ab5b-252">Exclude files from hello App_Data folder</span></span>
    
    <span data-ttu-id="5ab5b-253">Bu öğreticide bunlardan biri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-253">For this tutorial you don't need any of these.</span></span> <span data-ttu-id="5ab5b-254">Bunların ne yaptıklarına ilişkin ayrıntılı açıklamalar için bkz. [Nasıl yapılır: Visual Studio’da Tek Tıklamayla Yayımlamayı Kullanarak Web Projesi Dağıtma](https://msdn.microsoft.com/library/dd465337.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ab5b-254">For detailed explanations of what they do, see [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span></span>
14. <span data-ttu-id="5ab5b-255">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-255">Click **Next**.</span></span>
    
    ![Web’i Yayımla sihirbazının Ayarlar sekmesi İleri’ye tıklama](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    <span data-ttu-id="5ab5b-257">Sonraki hello olduğu **Önizleme** hangi dosyaların proje toohello API uygulamanızdan kopyalanan toobe giderek bir fırsat toosee sağlayan sekmesidir (aşağıda gösterilen),.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-257">Next is hello **Preview** tab (shown below), which gives you an opportunity toosee what files are going toobe copied from your project toohello API app.</span></span> <span data-ttu-id="5ab5b-258">Tooearlier zaten dağıtılmış bir proje tooan API uygulaması dağıtıyorsanız, yalnızca değiştirilen dosyalar kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-258">When you're deploying a project tooan API app that you already deployed tooearlier, only changed files are copied.</span></span> <span data-ttu-id="5ab5b-259">Toosee kopyalanacak dosyaların bir listesini istiyorsanız hello tıklatabilirsiniz **önizlemeyi Başlat** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-259">If you want toosee a list of what will be copied, you can click hello **Start Preview** button.</span></span>
15. <span data-ttu-id="5ab5b-260">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-260">Click **Publish**.</span></span>
    
    ![Web’i Yayımla sihirbazının Önizleme sekmesinde Yayımla’ya tıklama](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    <span data-ttu-id="5ab5b-262">Visual Studio hello Todolistdataapı projesi toohello yeni API uygulamasına dağıtır.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-262">Visual Studio deploys hello ToDoListDataAPI project toohello new API app.</span></span> <span data-ttu-id="5ab5b-263">Merhaba **çıkış** penceresi başarılı dağıtımı günlüğe kaydeder ve bir tarayıcı açılır pencere toohello URL hello API uygulamasının "başarıyla oluşturuldu" sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-263">hello **Output** window logs successful deployment, and a "successfully created" page appears in a browser window opened toohello URL of hello API app.</span></span>
    
    ![Çıktı penceresi başarılı dağıtım](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Yeni API uygulaması başarıyla oluşturuldu sayfası](./media/app-service-api-dotnet-get-started/appcreated.png)
16. <span data-ttu-id="5ab5b-266">Merhaba tarayıcının adres çubuğunda "swagger" toohello URL'sini ekleyin ve ardından Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-266">Add "swagger" toohello URL in hello browser's address bar, and then press Enter.</span></span> <span data-ttu-id="5ab5b-267">(URL hello `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="5ab5b-267">(hello URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
    
    <span data-ttu-id="5ab5b-268">Merhaba tarayıcı aynı Swagger daha önce gördüğünüzle kullanıcı arabirimini, ancak şimdi hello bulutta çalışan hello görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-268">hello browser displays hello same Swagger UI that you saw earlier, but now it's running in hello cloud.</span></span> <span data-ttu-id="5ab5b-269">GET yöntemi hello ve geri toohello varsayılan 2 yapılacak işler öğelerine döndüğünüzü görün deneyin.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-269">Try out hello Get method, and you see that you're back toohello default 2 to-do items.</span></span> <span data-ttu-id="5ab5b-270">daha önce yaptığınız hello değişiklikler hello yerel makine bellekte kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-270">hello changes you made earlier were saved in memory in hello local machine.</span></span>
17. <span data-ttu-id="5ab5b-271">Açık hello [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5ab5b-271">Open hello [Azure portal](https://portal.azure.com/).</span></span>
    
    <span data-ttu-id="5ab5b-272">Hello Azure portal, API uygulamaları gibi Azure kaynakları yöneten için bir web arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-272">hello Azure portal is a web interface for managing Azure resources such as API apps.</span></span>
18. <span data-ttu-id="5ab5b-273">**Diğer Hizmetler > Uygulama Hizmetleri**’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-273">Click **More Services > App Services**.</span></span>
    
    ![Uygulama Hizmetleri’ne Gözatma](./media/app-service-api-dotnet-get-started/browseas.png)
19. <span data-ttu-id="5ab5b-275">Merhaba, **uygulama hizmetleri** dikey penceresinde, bulma ve yeni API uygulamanızı'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-275">In hello **App Services** blade, find and click your new API app.</span></span> <span data-ttu-id="5ab5b-276">(Toohello sağ açın windows hello Azure portal, olarak adlandırılan *dikey*.)</span><span class="sxs-lookup"><span data-stu-id="5ab5b-276">(In hello Azure portal, windows that open toohello right are called *blades*.)</span></span>
    
    ![Uygulama Hizmetleri dikey penceresi](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    <span data-ttu-id="5ab5b-278">İki dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-278">Two blades open.</span></span> <span data-ttu-id="5ab5b-279">Bir dikey pencerede hello API uygulamasına genel bir bakış ve bir görüntüleyip değiştirmek ayarları uzun bir listesi varsa.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-279">One blade has an overview of hello API app, and one has a long list of settings that you can view and change.</span></span>
20. <span data-ttu-id="5ab5b-280">Merhaba, **ayarları** dikey penceresinde, Bul hello **API** 'ye tıklayın **API tanımı**.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-280">In hello **Settings** blade, find hello **API** section and click **API Definition**.</span></span>
    
    ![Ayarlar dikey penceresinde API Tanımı](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    <span data-ttu-id="5ab5b-282">Merhaba **API tanımı** dikey penceresi JSON biçiminde Swagger 2.0 meta verileri döndürür hello URL'yi belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-282">hello **API Definition** blade lets you specify hello URL that returns Swagger 2.0 metadata in JSON format.</span></span> <span data-ttu-id="5ab5b-283">Visual Studio hello API uygulaması oluşturduğunda, hello API uygulaması, daha önce gördüğünüz Swashbuckle tarafından oluşturulan meta verileri temel için hello API tanımı URL toohello varsayılan değeri ayarlar URL'si artı `/swagger/docs/v1`.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-283">When Visual Studio creates hello API app, it sets hello API definition URL toohello default value for Swashbuckle-generated metadata that you saw earlier, which is hello API app's base URL plus `/swagger/docs/v1`.</span></span>
    
    ![API tanımı URL'si](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    <span data-ttu-id="5ab5b-285">Bunun için bir API uygulaması toogenerate istemci kodu seçtiğinizde, Visual Studio hello meta verileri bu URL'den alır.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-285">When you select an API app toogenerate client code for it, Visual Studio retrieves hello metadata from this URL.</span></span>

## <span data-ttu-id="5ab5b-286"><a id="codegen"></a>Merhaba veri katmanı için istemci kodu oluştur</span><span class="sxs-lookup"><span data-stu-id="5ab5b-286"><a id="codegen"></a> Generate client code for hello data tier</span></span>
<span data-ttu-id="5ab5b-287">Azure API uygulamaları Swagger tümleştirme hello avantajları otomatik kod oluşturma biridir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-287">One of hello advantages of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="5ab5b-288">Oluşturulan istemci sınıfları API uygulamasını çağıran bir daha kolay toowrite kod kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-288">Generated client classes make it easier toowrite code that calls an API app.</span></span>

<span data-ttu-id="5ab5b-289">Merhaba Todolistapı projesinin oluşturulan hello istemci kodu zaten sahip, ancak aşağıdaki adımları hello silin ve nasıl toodo hello kod oluşturma toosee yeniden.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-289">hello ToDoListAPI project already has hello generated client code, but in hello following steps you'll delete it and regenerate it toosee how toodo hello code generation.</span></span>

1. <span data-ttu-id="5ab5b-290">Visual Studio'da **Çözüm Gezgini**, hello Todolistapı projesi, hello silme *Todolistdataapı* klasör.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-290">In Visual Studio **Solution Explorer**, in hello ToDoListAPI project, delete hello *ToDoListDataAPI* folder.</span></span> <span data-ttu-id="5ab5b-291">**Dikkat: Merhaba Todolistdataapı projesini yalnızca hello klasörünü silin.**</span><span class="sxs-lookup"><span data-stu-id="5ab5b-291">**Caution: Delete only hello folder, not hello ToDoListDataAPI project.**</span></span>
   
    ![Oluşturulan istemci kodunu silme](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    <span data-ttu-id="5ab5b-293">Bu klasör, toogo hakkında olduğunuz hello kod oluşturma işlemi kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-293">This folder was created by using hello code generation process that you're about toogo through.</span></span>
2. <span data-ttu-id="5ab5b-294">Merhaba Todolistapı projesine sağ tıklayın ve ardından **Ekle > REST API istemcisi**.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-294">Right-click hello ToDoListAPI project, and then click **Add > REST API Client**.</span></span>
   
    ![Visual Studio'da REST API istemcisi ekleme](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. <span data-ttu-id="5ab5b-296">Merhaba, **REST API istemcisi Ekle** iletişim kutusu, tıklatın **Swagger URL'si**ve ardından **Azure varlığını Seç**.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-296">In hello **Add REST API Client** dialog box, click **Swagger URL**, and then click **Select Azure Asset**.</span></span>
   
    ![Azure Varlığını Seç](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. <span data-ttu-id="5ab5b-298">Merhaba, **uygulama hizmeti** iletişim kutusunda, Bu öğretici için kullanmakta olduğunuz hello kaynak grubunu genişletin ve API uygulamanızı seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-298">In hello **App Service** dialog box, expand hello resource group you're using for this tutorial and select your API app, and then click **OK**.</span></span>
   
    ![Kod oluşturma için API uygulaması seçme](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    <span data-ttu-id="5ab5b-300">Toohello döndüğünüzde dikkat **REST API istemcisi Ekle** iletişim kutusunda, hello metin kutusuna doldurulmuş hello API tanımı oturum hello Portalı'nda daha önce gördüğünüz URL değeri.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-300">Notice that when you return toohello **Add REST API Client** dialog, hello text box has been filled in with hello API definition URL value that you saw earlier in hello portal.</span></span>
   
    ![API Tanımı URL'si](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > <span data-ttu-id="5ab5b-302">Kod oluşturma için bir alternatif yol tooget meta verileri hello Gözat iletişim kutusunu kullanmak yerine doğrudan tooenter hello URL'dir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-302">An alternative way tooget metadata for code generation is tooenter hello URL directly instead of going through hello browse dialog.</span></span> <span data-ttu-id="5ab5b-303">Veya tooAzure dağıtmadan önce toogenerate istemci kodu istiyorsanız hello Web API projesini yerel olarak çalıştırmak, hello dosyayı Kaydet hello Swagger JSON dosyasını sağlayan toohello URL gidin ve hello kullanabilirsiniz **mevcut bir Swagger meta veri dosyasıseçin**seçeneği.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-303">Or if you want toogenerate client code before deploying tooAzure, you could run hello Web API project locally, go toohello URL that provides hello Swagger JSON file, save hello file, and use hello **Select an existing Swagger metadata file** option.</span></span>
   > 
   > 
5. <span data-ttu-id="5ab5b-304">Merhaba, **REST API istemcisi Ekle** iletişim kutusu, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-304">In hello **Add REST API Client** dialog box, click **OK**.</span></span>
   
    <span data-ttu-id="5ab5b-305">Visual Studio hello API uygulamasının adını alan bir klasör oluşturur ve istemci sınıfları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-305">Visual Studio creates a folder named after hello API app and generates client classes.</span></span>
   
    ![Oluşturulan istemci için kod dosyaları](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. <span data-ttu-id="5ab5b-307">Merhaba Todolistapı projesinde, açık *Controllers\ToDoListController.cs* toosee hello kodu 40 satırında oluşturulan hello istemcisini kullanarak hello API'sini çağırır.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-307">In hello ToDoListAPI project, open *Controllers\ToDoListController.cs* toosee hello code at line 40  that calls hello API by using hello generated client.</span></span>
   
    <span data-ttu-id="5ab5b-308">Get yöntemi çağrıları hello ve aşağıdaki kod parçacığında hello hello kod hello istemci nesnesini nasıl başlatır gösterir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-308">hello following snippet shows how hello code instantiates hello client object and calls hello Get method.</span></span>
   
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
   
    <span data-ttu-id="5ab5b-309">Merhaba Oluşturucu parametresini alır hello uç nokta URL'si hello `toDoListDataAPIURL` uygulama ayarı.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-309">hello constructor parameter gets hello endpoint URL from  hello `toDoListDataAPIURL` app setting.</span></span> <span data-ttu-id="5ab5b-310">Merhaba Web.config dosyasında bu, yerel IIS Express URL'sini hello API proje hello uygulama yerel olarak çalıştırabilmeniz için kümesi toohello değerdir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-310">In hello Web.config file, that value is set toohello local IIS Express URL of hello API project so that you can run hello application locally.</span></span> <span data-ttu-id="5ab5b-311">Merhaba Oluşturucu parametresini atlarsanız, hello varsayılan uç hello koddan oluşturulan hello URL'dir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-311">If you omit hello constructor parameter, hello default endpoint is hello URL that you generated hello code from.</span></span>
7. <span data-ttu-id="5ab5b-312">İstemci sınıfınız, API uygulaması adınıza göre farklı bir ad ile oluşturulur; Merhaba kodda değişiklik *Controllers\ToDoListController.cs* hello türü adı ne projenizde oluşturulan böylece eşleşir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-312">Your client class will be generated with a different name based on your API app name; change hello code in *Controllers\ToDoListController.cs* so that hello type name matches what was generated in your project.</span></span> <span data-ttu-id="5ab5b-313">Örneğin, API Uygulamanıza ToDoListDataAPI071316 adını verdiyseniz kodu değiştirin:</span><span class="sxs-lookup"><span data-stu-id="5ab5b-313">For example, if you named your API App ToDoListDataAPI071316, you would change this code:</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

<span data-ttu-id="5ab5b-314">toothis:</span><span class="sxs-lookup"><span data-stu-id="5ab5b-314">toothis:</span></span>

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-toohost-hello-middle-tier"></a><span data-ttu-id="5ab5b-315">Bir API uygulaması toohost hello orta katman oluşturma</span><span class="sxs-lookup"><span data-stu-id="5ab5b-315">Create an API app toohost hello middle tier</span></span>
<span data-ttu-id="5ab5b-316">Daha önce [hello veri katmanı API uygulaması oluşturdunuz ve kodu tooit dağıtılan](#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="5ab5b-316">Earlier you [created hello data tier API app and deployed code tooit](#createapiapp).</span></span>  <span data-ttu-id="5ab5b-317">Merhaba izleyin artık hello orta katman API uygulaması için aynı yordamı.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-317">Now you follow hello same procedure for hello middle tier API app.</span></span>

1. <span data-ttu-id="5ab5b-318">İçinde **Çözüm Gezgini**, sağ hello orta katman Todolistapı projesine (değil hello veri katmanı Todolistdataapı) ve ardından **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-318">In **Solution Explorer**, right-click hello middle tier ToDoListAPI  project (not hello data tier ToDoListDataAPI), and then click **Publish**.</span></span>
   
    ![Visual Studio’ya Yayımla'ya tıklama](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. <span data-ttu-id="5ab5b-320">Merhaba, **profil** hello sekmesinde **Web'i Yayımla** Sihirbazı'nı tıklatın **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-320">In hello **Profile** tab of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="5ab5b-321">Merhaba, **uygulama hizmeti** iletişim kutusu, tıklatın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-321">In hello **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="5ab5b-322">Merhaba, **barındırma** hello sekmesinde **App Service Oluştur** iletişim kutusunda, hello varsayılanı kabul **API uygulaması adı** hello benzersiz bir ad girin veya  *azurewebsites.NET* etki alanı.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-322">In hello **Hosting** tab of hello **Create App Service** dialog box, accept hello default **API App Name** or enter a name that is unique in hello *azurewebsites.net* domain.</span></span>
5. <span data-ttu-id="5ab5b-323">Hello Azure'ı seçin **abonelik** , kullanmakta olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-323">Choose hello Azure **Subscription** you have been using.</span></span>
6. <span data-ttu-id="5ab5b-324">Merhaba, **kaynak grubu** açılan listesinde, hello seçin daha önce oluşturduğunuz aynı kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-324">In hello **Resource Group** drop-down, choose hello same resource group you created earlier.</span></span>
7. <span data-ttu-id="5ab5b-325">Merhaba, **uygulama hizmeti planı** açılan listesinde, hello seçin önceden oluşturduğunuz planı.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-325">In hello **App Service Plan** drop-down, choose hello same plan you created earlier.</span></span> <span data-ttu-id="5ab5b-326">Bu varsayılan toothat değer kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-326">It will default toothat value.</span></span>
8. <span data-ttu-id="5ab5b-327">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-327">Click **Create**.</span></span>
   
    <span data-ttu-id="5ab5b-328">Visual Studio hello API uygulamasını oluşturur, bunun için bir yayımlama profili oluşturur ve görüntüler hello **bağlantı** hello adımında **Web'i Yayımla** Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-328">Visual Studio creates hello API app, creates a publish profile for it, and displays hello **Connection** step of hello **Publish Web** wizard.</span></span>
9. <span data-ttu-id="5ab5b-329">Merhaba, **bağlantı** hello adımında **Web'i Yayımla** Sihirbazı'nı tıklatın **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-329">In hello **Connection** step of hello **Publish Web** wizard, click **Publish**.</span></span>
   
   <span data-ttu-id="5ab5b-330">Visual Studio hello Todolistapı projesi toohello yeni API uygulamasına dağıtır ve tarayıcı toohello hello API uygulaması URL'sini açar.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-330">Visual Studio deploys hello ToDoListAPI project toohello new API app and opens a browser toohello URL of hello API app.</span></span> <span data-ttu-id="5ab5b-331">Merhaba "başarıyla oluşturuldu" sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-331">hello "successfully created" page appears.</span></span>

## <a name="configure-hello-middle-tier-toocall-hello-data-tier"></a><span data-ttu-id="5ab5b-332">Merhaba orta katman toocall hello veri katmanını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5ab5b-332">Configure hello middle tier toocall hello data tier</span></span>
<span data-ttu-id="5ab5b-333">Merhaba orta katman API uygulamasını çağırdıysanız, hala hello Web.config dosyasındaki hello localhost URL'sini kullanarak toocall hello veri katmanı isteriz.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-333">If you called hello middle tier API app now, it would try toocall hello data tier using hello localhost URL that is still in hello Web.config file.</span></span> <span data-ttu-id="5ab5b-334">Bu bölümde hello orta katman API uygulamasındaki bir ortam ayarına hello veri katmanı API uygulaması URL'sini girin.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-334">In this section you enter hello data tier API app URL into an environment setting in hello middle tier API app.</span></span> <span data-ttu-id="5ab5b-335">Merhaba hello orta katman API uygulamasındaki kod hello veri katmanı URL ayarını aldığında hello ortamı ayarı ne hello Web.config dosyasında geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-335">When hello code in hello middle tier API app retrieves hello data tier URL setting, hello environment setting will override what's in hello Web.config file.</span></span>

1. <span data-ttu-id="5ab5b-336">Toohello Git [Azure portal](https://portal.azure.com/)ve ardından toohello gidin **API uygulaması** toohost hello Todolistapı (orta katman) proje oluşturulan hello API uygulaması dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-336">Go toohello [Azure portal](https://portal.azure.com/), and then navigate toohello **API App** blade for hello API app that you created toohost hello TodoListAPI (middle tier) project.</span></span>
2. <span data-ttu-id="5ab5b-337">İçinde API uygulamasının hello **ayarları** dikey penceresinde tıklatın **uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-337">In hello API App's **Settings** blade, click **Application settings**.</span></span>
3. <span data-ttu-id="5ab5b-338">İçinde API uygulamasının hello **uygulama ayarları** dikey penceresinde, toohello aşağı **uygulama ayarları** bölümünde ve hello aşağıdakileri ekleyin anahtar ve değer.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-338">In hello API App's **Application Settings** blade, scroll down toohello **App settings** section and add hello following key and value.</span></span> <span data-ttu-id="5ab5b-339">Merhaba değer hello ilk API Bu öğreticide yayımlanan uygulama hello URL'si olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-339">hello value will be hello URL of hello first API App you published in this tutorial.</span></span>
   
   | <span data-ttu-id="5ab5b-340">**Anahtar**</span><span class="sxs-lookup"><span data-stu-id="5ab5b-340">**Key**</span></span> | <span data-ttu-id="5ab5b-341">toDoListDataAPIURL</span><span class="sxs-lookup"><span data-stu-id="5ab5b-341">toDoListDataAPIURL</span></span> |
   | --- | --- |
   | <span data-ttu-id="5ab5b-342">**Değer**</span><span class="sxs-lookup"><span data-stu-id="5ab5b-342">**Value**</span></span> |<span data-ttu-id="5ab5b-343">https://{your data tier API app name}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="5ab5b-343">https://{your data tier API app name}.azurewebsites.net</span></span> |
   | <span data-ttu-id="5ab5b-344">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="5ab5b-344">**Example**</span></span> |<span data-ttu-id="5ab5b-345">https://todolistdataapi.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="5ab5b-345">https://todolistdataapi.azurewebsites.net</span></span> |
4. <span data-ttu-id="5ab5b-346">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-346">Click **Save**.</span></span>
   
    ![Uygulama Ayarları için Kaydet’e tıklama](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    <span data-ttu-id="5ab5b-348">Merhaba kod Azure içinde çalıştığında, bu değer şimdi hello Web.config dosyasındaki hello localhost URL'sini geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-348">When hello code runs in Azure, this value will now override hello localhost URL that is in hello Web.config file.</span></span>

## <a name="test"></a><span data-ttu-id="5ab5b-349">Test etme</span><span class="sxs-lookup"><span data-stu-id="5ab5b-349">Test</span></span>
1. <span data-ttu-id="5ab5b-350">Bir tarayıcı penceresinde hello yeni orta katman Todolistapı için oluşturduğunuz API uygulaması URL'sini toohello göz atın.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-350">In a browser window, browse toohello URL of hello new middle tier API app that you just created for ToDoListAPI.</span></span> <span data-ttu-id="5ab5b-351">Merhaba API uygulamasının ana dikey hello portalında hello URL'de tıklayarak buradan ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-351">You can get there by clicking hello URL in hello API app's main blade in hello portal.</span></span>
2. <span data-ttu-id="5ab5b-352">Merhaba tarayıcının adres çubuğunda "swagger" toohello URL'sini ekleyin ve ardından Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-352">Add "swagger" toohello URL in hello browser's address bar, and then press Enter.</span></span> <span data-ttu-id="5ab5b-353">(URL hello `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="5ab5b-353">(hello URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
   
    <span data-ttu-id="5ab5b-354">Merhaba tarayıcı görüntüler hello aynı Swagger Todolistdataapı için daha önce ancak şimdi gördüğünüzle kullanıcı arabirimini `owner` hello orta katman API uygulaması sizin için bu değeri toohello veri katmanı API uygulamasına gönderdiği için hello alma işlemi için gerekli bir alan değil.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-354">hello browser displays hello same Swagger UI that you saw earlier for ToDoListDataAPI, but now `owner` is not a required field for hello Get operation, because hello middle tier API app is sending that value toohello data tier API app for you.</span></span> <span data-ttu-id="5ab5b-355">(Kimlik doğrulaması öğreticilerini hello hello orta katman hello için gerçek kullanıcı kimliklerini gönderir `owner` parametresi; şimdi onu bir yıldız işareti kodlamak için.)</span><span class="sxs-lookup"><span data-stu-id="5ab5b-355">(When you do hello authentication tutorials, hello middle tier will send actual user IDs for hello `owner` parameter; for now it is hard-coding an asterisk.)</span></span>
3. <span data-ttu-id="5ab5b-356">GET yöntemi hello ve hello orta katman API uygulaması hello diğer yöntemleri toovalidate başarıyla hello veri katmanı API uygulamasını çağıran deneyin.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-356">Try out hello Get method and hello other methods toovalidate that hello middle tier API app is successfully calling hello data tier API app.</span></span>
   
    ![Swagger kullanıcı arabirimi Alma yöntemi](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a><span data-ttu-id="5ab5b-358">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="5ab5b-358">Troubleshooting</span></span>
<span data-ttu-id="5ab5b-359">Bu öğreticiyi izlerken bir sorunla karşılaşırsanız, bazı sorun giderme fikirlerini burada bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-359">In case you run into a problem as you go through this tutorial here are some troubleshooting ideas:</span></span>

* <span data-ttu-id="5ab5b-360">Merhaba hello en son sürümünü kullandığınızdan emin olun [.NET için Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="5ab5b-360">Make sure that you're using hello latest version of hello [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="5ab5b-361">Merhaba proje adı benzerdir (Todolistapı, Todolistdataapı) ikisidir.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-361">Two of hello project names are similar (ToDoListAPI, ToDoListDataAPI).</span></span> <span data-ttu-id="5ab5b-362">Öğeleri bir projeyle çalışırken hello yönergelerde açıklandığı gibi görünmüyorsa, hello doğru projeyi açtığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-362">If things don't look as described in hello instructions when you are working with a project, make sure you have opened hello correct project.</span></span>
* <span data-ttu-id="5ab5b-363">Kurumsal bir ağda bulunuyorsanız ve bir güvenlik duvarı üzerinden toodeploy tooAzure uygulama hizmeti çalışıyorsanız, bağlantı noktası 443 ve 8172 Web dağıtımı için açık olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-363">If you're on a corporate network and are trying toodeploy tooAzure App Service through a firewall, make sure that ports 443 and 8172 are open for Web Deploy.</span></span> <span data-ttu-id="5ab5b-364">Bu bağlantı noktalarını açamıyorsanız, diğer dağıtım yöntemlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-364">If you can't open those ports, you can use other deployment methods.</span></span>  <span data-ttu-id="5ab5b-365">Bkz: [, uygulama tooAzure uygulama hizmeti dağıtmak](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="5ab5b-365">See [Deploy your app tooAzure App Service](../app-service-web/web-sites-deploy.md).</span></span>
* <span data-ttu-id="5ab5b-366">Yanlışlıkla hello yanlış projeyi tooan API uygulama dağıtır ve daha sonra hello doğru bir tooit dağıtma "rota adları benzersiz olmalıdır" hataları--bu hataları alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-366">"Route names must be unique" errors -- you could get these if you accidentally deploy hello wrong project tooan API app and then later deploy hello correct one tooit.</span></span> <span data-ttu-id="5ab5b-367">toocorrect Bu, yeniden dağıtın hello doğru projeyi toohello API uygulaması ve hello **ayarları** hello sekmesinde **Web'i Yayımla** Sihirbazı'nı seçin **hedeftekiekdosyalarıKaldır**.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-367">toocorrect this, redeploy hello correct project toohello API app, and on hello **Settings** tab of hello **Publish Web** wizard select **Remove additional files at destination**.</span></span>

<span data-ttu-id="5ab5b-368">Azure App Service'de ASP.NET API uygulamanızı çalıştırdıktan sonra sorun giderme sürecini kolaylaştıracak Visual Studio özellikleri hakkında daha fazla toolearn isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-368">After you have your ASP.NET API app running in Azure App Service, you may want toolearn more about Visual Studio features that simplify troubleshooting.</span></span> <span data-ttu-id="5ab5b-369">Günlüğe kaydetme, uzaktan hata ayıklama ve çok daha fazlası hakkında bilgi edinmek için bkz. [Visual Studio’da Azure App Service uygulamalarının sorunlarını giderme](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="5ab5b-369">For information about logging, remote debugging, and more, see  [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ab5b-370">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5ab5b-370">Next steps</span></span>
<span data-ttu-id="5ab5b-371">Nasıl toodeploy mevcut Web API projeleri tooAPI apps, API uygulamaları için istemci kodu oluşturmak ve .NET istemcilerinden API uygulamalarını kullanmayı gördünüz.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-371">You've seen how toodeploy existing Web API projects tooAPI apps, generate client code for API apps, and consume API apps from .NET clients.</span></span> <span data-ttu-id="5ab5b-372">Bu serideki sonraki öğretici Hello gösterir nasıl çok[JavaScript istemcilerinden CORS tooconsume API uygulamalarını kullanmak](app-service-api-cors-consume-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="5ab5b-372">hello next tutorial in this series shows how too[use CORS tooconsume API apps from JavaScript clients](app-service-api-cors-consume-javascript.md).</span></span>

<span data-ttu-id="5ab5b-373">İstemci kodu oluşturma hakkında daha fazla bilgi için bkz: Merhaba [Azure/AutoRest](https://github.com/azure/autorest) Github.com'u havuzda. Oluşturulan hello istemcisini kullanarak sorunlarıyla ilgili Yardım için açık bir [hello AutoRest deposunda sorunu](https://github.com/azure/autorest/issues).</span><span class="sxs-lookup"><span data-stu-id="5ab5b-373">For more information about client code generation, see hello [Azure/AutoRest](https://github.com/azure/autorest) repository on GitHub.com. For help with problems using hello generated client, open an [issue in hello AutoRest repository](https://github.com/azure/autorest/issues).</span></span>

<span data-ttu-id="5ab5b-374">Toocreate yeni API uygulaması projeleri sıfırdan istiyorsanız hello kullanın **Azure API uygulaması** şablonu.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-374">If you want toocreate new API app projects from scratch, use hello **Azure API App** template.</span></span>

![Visual Studio’da API Uygulaması şablonu](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

<span data-ttu-id="5ab5b-376">Merhaba **Azure API uygulaması** proje şablonudur eşdeğer toochoosing hello **boş** ASP.NET 4.5.2 şablonu hello onay kutusunu tooadd Web API desteği tıklayarak ve hello Swashbuckle NuGet paketi yükleniyor.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-376">hello **Azure API App** project template is equivalent toochoosing hello **Empty** ASP.NET 4.5.2 template, clicking hello check box tooadd Web API support, and installing hello Swashbuckle NuGet package.</span></span> <span data-ttu-id="5ab5b-377">Ayrıca, bazı Swashbuckle yapılandırma tasarlanmış kod tooprevent hello oluşturulmasını yinelenen Swagger işlem kimlikleri hello şablon ekler.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-377">In addition, hello template adds some Swashbuckle configuration code designed tooprevent hello creation of duplicate Swagger operation IDs.</span></span> <span data-ttu-id="5ab5b-378">Bir API uygulaması projesi oluşturduktan sonra tooan API uygulaması hello dağıtabilirsiniz Bu öğreticide gördüğünüz şekilde.</span><span class="sxs-lookup"><span data-stu-id="5ab5b-378">Once you've created an API App project, you can deploy it tooan API app hello same way you saw in this tutorial.</span></span>

