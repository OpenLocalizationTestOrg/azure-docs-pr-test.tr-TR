---
title: "aaaCreate Service Fabric için bir .NET uygulaması | Microsoft Docs"
description: "Nasıl toocreate ön uç bir ASP.NET Core ve güvenilir bir uygulamayla durum bilgisi olan arka uç hizmeti ve hello uygulama tooa kümesi dağıtma öğrenin."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: bab331b9f8616c50a2794b6c048aace15579c8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a><span data-ttu-id="e40bc-103">Bir ASP.NET çekirdek Web API ön uç hizmeti ve durum bilgisi olan bir arka uç hizmeti ile bir uygulama oluşturun ve dağıtın</span><span class="sxs-lookup"><span data-stu-id="e40bc-103">Create and deploy an application with an ASP.NET Core Web API front-end service and a stateful back-end service</span></span>
<span data-ttu-id="e40bc-104">Bu öğretici bir dizi birini bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="e40bc-104">This tutorial is part one of a series.</span></span>  <span data-ttu-id="e40bc-105">Verilerinizin nasıl toocreate bir Azure Service Fabric uygulaması bir ASP.NET çekirdek Web API ön ile bitmelidir ve bir durum bilgisi olan arka uç hizmetine toostore öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e40bc-105">You will learn how toocreate an Azure Service Fabric application with an ASP.NET Core Web API front end and a stateful back-end service toostore your data.</span></span> <span data-ttu-id="e40bc-106">İşlemi tamamladığınızda, oylama bir durum bilgisi olan bir arka uç hizmetinde hello kümedeki Oylama sonuçlarını kaydettiği ön uç bir ASP.NET Core web uygulamasıyla sahip.</span><span class="sxs-lookup"><span data-stu-id="e40bc-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in hello cluster.</span></span> <span data-ttu-id="e40bc-107">Toomanually istemiyorsanız, uygulama oylama hello oluşturma, şunları yapabilirsiniz [hello kaynak kodunu indirebilir](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) Merhaba uygulama tamamlandı ve İleri çok atlayabilirsiniz[örnek uygulama oylama hello yol](#walkthrough_anchor).</span><span class="sxs-lookup"><span data-stu-id="e40bc-107">If you don't want toomanually create hello voting application, you can [download hello source code](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) for hello completed application and skip ahead too[Walk through hello voting sample application](#walkthrough_anchor).</span></span>

![Uygulama diyagramı](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="e40bc-109">Bölümünde hello serisi birini öğrenin nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="e40bc-109">In part one of hello series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e40bc-110">Durum bilgisi olan güvenilir bir hizmet olarak bir ASP.NET çekirdek Web API hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="e40bc-110">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="e40bc-111">Durum bilgisiz web hizmeti olarak bir ASP.NET çekirdek Web uygulaması hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="e40bc-111">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="e40bc-112">Merhaba durum bilgisi olan hizmeti ile Merhaba ters proxy toocommunicate kullanın</span><span class="sxs-lookup"><span data-stu-id="e40bc-112">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="e40bc-113">Bu öğretici serisinde öğrenin nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="e40bc-113">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="e40bc-114">Bir .NET Service Fabric uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e40bc-114">Build a .NET Service Fabric application</span></span>
> * [<span data-ttu-id="e40bc-115">Merhaba uygulama tooa uzak kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="e40bc-115">Deploy hello application tooa remote cluster</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [<span data-ttu-id="e40bc-116">CI/CD Visual Studio Team Services kullanarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e40bc-116">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="e40bc-117">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e40bc-117">Prerequisites</span></span>
<span data-ttu-id="e40bc-118">Bu öğreticiye başlamadan önce:</span><span class="sxs-lookup"><span data-stu-id="e40bc-118">Before you begin this tutorial:</span></span>
- <span data-ttu-id="e40bc-119">Bir Azure aboneliğiniz yoksa, oluşturma bir [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="e40bc-119">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="e40bc-120">[Visual Studio 2017 yükleme](https://www.visualstudio.com/) hello yükleyip **Azure geliştirme** ve **ASP.NET ve web geliştirme** iş yükleri.</span><span class="sxs-lookup"><span data-stu-id="e40bc-120">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="e40bc-121">Merhaba Service Fabric SDK yükleme</span><span class="sxs-lookup"><span data-stu-id="e40bc-121">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a><span data-ttu-id="e40bc-122">Bir ASP.NET Web API hizmeti güvenilir bir hizmet olarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="e40bc-122">Create an ASP.NET Web API service as a reliable service</span></span>
<span data-ttu-id="e40bc-123">İlk olarak hello web ön ucu ASP.NET Core kullanarak uygulama oylama hello olarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e40bc-123">First, create hello web front-end of hello voting application using ASP.NET Core.</span></span> <span data-ttu-id="e40bc-124">ASP.NET Core toocreate modern web kullanıcı arabirimini kullanın ve API web bir basit, platformlar arası web geliştirme altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="e40bc-124">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> <span data-ttu-id="e40bc-125">ASP.NET Core Service Fabric ile nasıl tümleşik çalıştığını'nın tam bir anlayış tooget öneririz hello okuma [Service Fabric Reliable Services ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="e40bc-125">tooget a complete understanding of how ASP.NET Core integrates with Service Fabric, we strongly recommend reading through hello [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) article.</span></span> <span data-ttu-id="e40bc-126">Şu an için hızlı şekilde kullanmaya Bu öğretici tooget izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e40bc-126">For now, you can follow this tutorial tooget started quickly.</span></span> <span data-ttu-id="e40bc-127">ASP.NET Çekirdeği hakkında daha fazla toolearn hello bkz [ASP.NET Core belgeleri](https://docs.microsoft.com/aspnet/core/).</span><span class="sxs-lookup"><span data-stu-id="e40bc-127">toolearn more about ASP.NET Core, see hello [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core/).</span></span>

> [!NOTE]
> <span data-ttu-id="e40bc-128">Bu öğretici hello üzerinde temel [ASP.NET Core araçları için Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span><span class="sxs-lookup"><span data-stu-id="e40bc-128">This tutorial is based on hello [ASP.NET Core tools for Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span></span> <span data-ttu-id="e40bc-129">Merhaba .NET Core araçları Visual Studio 2015 için artık güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="e40bc-129">hello .NET Core tools for Visual Studio 2015 are no longer being updated.</span></span>

1. <span data-ttu-id="e40bc-130">Visual Studio'yu **yönetici** olarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="e40bc-130">Launch Visual Studio as an **administrator**.</span></span>

2. <span data-ttu-id="e40bc-131">Bir proje oluşturun **dosya**->**yeni**->**proje**</span><span class="sxs-lookup"><span data-stu-id="e40bc-131">Create a project with **File**->**New**->**Project**</span></span>

3. <span data-ttu-id="e40bc-132">Merhaba, **yeni proje** iletişim kutusunda, seçin **bulut > Service Fabric uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="e40bc-132">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

4. <span data-ttu-id="e40bc-133">Ad Merhaba uygulaması **oylama** ve basın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e40bc-133">Name hello application **Voting** and press **OK**.</span></span>

   ![Visual Studio'da yeni proje iletişim kutusu](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. <span data-ttu-id="e40bc-135">Merhaba üzerinde **yeni yapı hizmeti** sayfasında, **durum bilgisiz ASP.NET Core**ve hizmetinizin adını **VotingWeb**.</span><span class="sxs-lookup"><span data-stu-id="e40bc-135">On hello **New Service Fabric Service** page, choose **Stateless ASP.NET Core**, and name your service **VotingWeb**.</span></span>
   
   ![ASP.NET web hizmeti hello yeni hizmet iletişim kutusunda seçme](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. <span data-ttu-id="e40bc-137">Merhaba sonraki sayfaya ASP.NET Core birtakım proje şablonları sağlar.</span><span class="sxs-lookup"><span data-stu-id="e40bc-137">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="e40bc-138">Bu öğretici için seçin **Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="e40bc-138">For this tutorial, choose **Web Application**.</span></span> 
   
   ![ASP.NET proje türü seçin](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   <span data-ttu-id="e40bc-140">Visual Studio, uygulama ve hizmet projesi oluşturur ve bunları Çözüm Gezgini'nde görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e40bc-140">Visual Studio creates an application and a service project and displays them in Solution Explorer.</span></span>

   ![ASP.NET core Web API hizmeti içeren uygulama oluşturulduktan sonra Çözüm Gezgini]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a><span data-ttu-id="e40bc-142">AngularJS toohello VotingWeb Hizmet Ekle</span><span class="sxs-lookup"><span data-stu-id="e40bc-142">Add AngularJS toohello VotingWeb service</span></span>
<span data-ttu-id="e40bc-143">Ekleme [AngularJS](http://angularjs.org/) hello yerleşik kullanarak tooyour hizmet [Bower Destek](/aspnet/core/client-side/bower).</span><span class="sxs-lookup"><span data-stu-id="e40bc-143">Add [AngularJS](http://angularjs.org/) tooyour service using hello built-in [Bower support](/aspnet/core/client-side/bower).</span></span> <span data-ttu-id="e40bc-144">Açık *bower.json* ve Açısal ve önyükleme Açısal girişlerini ekleyin, sonra yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e40bc-144">Open *bower.json* and add entries for angular and angular-bootstrap, then save your changes.</span></span>

```json
{
  "name": "asp.net",
  "private": true,
  "dependencies": {
    "bootstrap": "3.3.7",
    "jquery": "2.2.0",
    "jquery-validation": "1.14.0",
    "jquery-validation-unobtrusive": "3.2.6",
    "angular": "v1.6.5",
    "angular-bootstrap": "v1.1.0"
  }
}
```
<span data-ttu-id="e40bc-145">Merhaba kaydetme sırasında *bower.json* dosya, Angular projenizin içinde yüklü *wwwroot/lib* klasör.</span><span class="sxs-lookup"><span data-stu-id="e40bc-145">Upon saving hello *bower.json* file, Angular is installed in your project's *wwwroot/lib* folder.</span></span> <span data-ttu-id="e40bc-146">Ayrıca, hello içinde listelenen *bağımlılıkları/Bower* klasör.</span><span class="sxs-lookup"><span data-stu-id="e40bc-146">Additionally, it is listed within hello *Dependencies/Bower* folder.</span></span>

### <a name="update-hello-sitejs-file"></a><span data-ttu-id="e40bc-147">Merhaba site.js dosyasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="e40bc-147">Update hello site.js file</span></span>
<span data-ttu-id="e40bc-148">Açık hello *wwwroot/js/site.js* dosya.</span><span class="sxs-lookup"><span data-stu-id="e40bc-148">Open hello *wwwroot/js/site.js* file.</span></span>  <span data-ttu-id="e40bc-149">İçeriği hello hello giriş görünümleri tarafından kullanılan JavaScript ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="e40bc-149">Replace its contents with hello JavaScript used by hello Home views:</span></span>

```javascript
var app = angular.module('VotingApp', ['ui.bootstrap']);
app.run(function () { });

app.controller('VotingAppController', ['$rootScope', '$scope', '$http', '$timeout', function ($rootScope, $scope, $http, $timeout) {

    $scope.refresh = function () {
        $http.get('api/Votes?c=' + new Date().getTime())
            .then(function (data, status) {
                $scope.votes = data;
            }, function (data, status) {
                $scope.votes = undefined;
            });
    };

    $scope.remove = function (item) {
        $http.delete('api/Votes/' + item)
            .then(function (data, status) {
                $scope.refresh();
            })
    };

    $scope.add = function (item) {
        var fd = new FormData();
        fd.append('item', item);
        $http.put('api/Votes/' + item, fd, {
            transformRequest: angular.identity,
            headers: { 'Content-Type': undefined }
        })
            .then(function (data, status) {
                $scope.refresh();
                $scope.item = undefined;
            })
    };
}]);
```

### <a name="update-hello-indexcshtml-file"></a><span data-ttu-id="e40bc-150">Merhaba Index.cshtml dosyasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="e40bc-150">Update hello Index.cshtml file</span></span>
<span data-ttu-id="e40bc-151">Açık hello *Views/Home/Index.cshtml* dosya, hello görünüm belirli toohello giriş denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="e40bc-151">Open hello *Views/Home/Index.cshtml* file, hello view specific toohello Home controller.</span></span>  <span data-ttu-id="e40bc-152">İçeriğinin hello şununla değiştirin ve değişikliklerinizi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e40bc-152">Replace its contents with hello following, then save your changes.</span></span>

```html
@{
    ViewData["Title"] = "Service Fabric Voting Sample";
}

<div ng-controller="VotingAppController" ng-init="refresh()">
    <div class="container-fluid">
        <div class="row">
            <div class="col-xs-8 col-xs-offset-2 text-center">
                <h2>Service Fabric Voting Sample</h2>
            </div>
        </div>

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <form class="col-xs-12 center-block">
                    <div class="col-xs-6 form-group">
                        <input id="txtAdd" type="text" class="form-control" placeholder="Add voting option" ng-model="item" />
                    </div>
                    <button id="btnAdd" class="btn btn-default" ng-click="add(item)">
                        <span class="glyphicon glyphicon-plus" aria-hidden="true"></span>
                        Add
                    </button>
                </form>
            </div>
        </div>

        <hr />

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <div class="row">
                    <div class="col-xs-4">
                        Click toovote
                    </div>
                </div>
                <div class="row top-buffer" ng-repeat="vote in votes.data">
                    <div class="col-xs-8">
                        <button class="btn btn-success text-left btn-block" ng-click="add(vote.key)">
                            <span class="pull-left">
                                {{vote.key}}
                            </span>
                            <span class="badge pull-right">
                                {{vote.value}} Votes
                            </span>
                        </button>
                    </div>
                    <div class="col-xs-4">
                        <button class="btn btn-danger pull-right btn-block" ng-click="remove(vote.key)">
                            <span class="glyphicon glyphicon-remove" aria-hidden="true"></span>
                            Remove
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
```

### <a name="update-hello-layoutcshtml-file"></a><span data-ttu-id="e40bc-153">Merhaba _Layout.cshtml dosyasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="e40bc-153">Update hello _Layout.cshtml file</span></span>
<span data-ttu-id="e40bc-154">Açık hello *Views/Shared/_Layout.cshtml* dosya, hello ASP.NET uygulaması için hello varsayılan düzeni.</span><span class="sxs-lookup"><span data-stu-id="e40bc-154">Open hello *Views/Shared/_Layout.cshtml* file, hello default layout for hello ASP.NET app.</span></span>  <span data-ttu-id="e40bc-155">İçeriğinin hello şununla değiştirin ve değişikliklerinizi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e40bc-155">Replace its contents with hello following, then save your changes.</span></span>

```html
<!DOCTYPE html>
<html ng-app="VotingApp" xmlns:ng="http://angularjs.org">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"]</title>

    <link href="~/lib/bootstrap/dist/css/bootstrap.min.css" rel="stylesheet" />
    <link href="~/css/site.css" rel="stylesheet" />

</head>
<body>
    <div class="container body-content">
        @RenderBody()
    </div>

    <script src="~/lib/jquery/dist/jquery.js"></script>
    <script src="~/lib/bootstrap/dist/js/bootstrap.js"></script>
    <script src="~/lib/angular/angular.js"></script>
    <script src="~/lib/angular-bootstrap/ui-bootstrap-tpls.js"></script>
    <script src="~/js/site.js"></script>

    @RenderSection("Scripts", required: false)
</body>
</html>
```

### <a name="update-hello-votingwebcs-file"></a><span data-ttu-id="e40bc-156">Merhaba VotingWeb.cs dosyasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="e40bc-156">Update hello VotingWeb.cs file</span></span>
<span data-ttu-id="e40bc-157">Açık hello *VotingWeb.cs* hello ASP.NET Core WebHost hello WebListener web sunucusu kullanarak hello durum bilgisiz hizmeti içinde oluşturur dosya.</span><span class="sxs-lookup"><span data-stu-id="e40bc-157">Open hello *VotingWeb.cs* file, which creates hello ASP.NET Core WebHost inside hello stateless service using hello WebListener web server.</span></span>  <span data-ttu-id="e40bc-158">Merhaba eklemek `using System.Net.Http;` yönerge toohello dosyasının üst kısmında hello.</span><span class="sxs-lookup"><span data-stu-id="e40bc-158">Add hello `using System.Net.Http;` directive toohello top of hello file.</span></span>  <span data-ttu-id="e40bc-159">Hello yerine `CreateServiceInstanceListeners()` işlev hello aşağıdakilerle sonra yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e40bc-159">Replace hello `CreateServiceInstanceListeners()` function with hello following, then save your changes.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
            {
                ServiceEventSource.Current.ServiceMessage(serviceContext, $"Starting WebListener on {url}");

                return new WebHostBuilder().UseWebListener()
                            .ConfigureServices(
                                services => services
                                    .AddSingleton<StatelessServiceContext>(serviceContext)
                                    .AddSingleton<HttpClient>())
                            .UseContentRoot(Directory.GetCurrentDirectory())
                            .UseStartup<Startup>()
                            .UseApplicationInsights()
                            .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                            .UseUrls(url)
                            .Build();
            }))
    };
}
```

### <a name="add-hello-votescontrollercs-file"></a><span data-ttu-id="e40bc-160">Merhaba VotesController.cs dosyası ekleme</span><span class="sxs-lookup"><span data-stu-id="e40bc-160">Add hello VotesController.cs file</span></span>
<span data-ttu-id="e40bc-161">Oylama Eylemler tanımlayan bir denetleyici ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e40bc-161">Add a controller which defines voting actions.</span></span> <span data-ttu-id="e40bc-162">Hello üzerinde sağ **denetleyicileri** klasörünü seçip **Ekle -> Yeni öğe sınıfı ->**.</span><span class="sxs-lookup"><span data-stu-id="e40bc-162">Right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span>  <span data-ttu-id="e40bc-163">Merhaba dosya "VotesController.cs" olarak adlandırın ve tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e40bc-163">Name hello file "VotesController.cs" and click **Add**.</span></span>  <span data-ttu-id="e40bc-164">Merhaba dosya içeriklerini hello şununla değiştirin ve değişikliklerinizi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e40bc-164">Replace hello file contents with hello following, then save your changes.</span></span>  <span data-ttu-id="e40bc-165">Daha sonra [güncelleştirme hello VotesController.cs dosyası](#updatevotecontroller_anchor), bu dosyası değiştirilmiş tooread ve hello arka uç hizmetinden oylama veri yazma.</span><span class="sxs-lookup"><span data-stu-id="e40bc-165">Later, in [Update hello VotesController.cs file](#updatevotecontroller_anchor), this file will be modified tooread and write voting data from hello back-end service.</span></span>  <span data-ttu-id="e40bc-166">Şu an için statik bir dize veri toohello görünümü hello denetleyicisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="e40bc-166">For now, hello controller returns static string data toohello view.</span></span>

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using System.Collections.Generic;
using Newtonsoft.Json;
using System.Text;
using System.Net.Http;
using System.Net.Http.Headers;

namespace VotingWeb.Controllers
{
    [Produces("application/json")]
    [Route("api/Votes")]
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            List<KeyValuePair<string, int>> votes= new List<KeyValuePair<string, int>>();
            votes.Add(new KeyValuePair<string, int>("Pizza", 3));
            votes.Add(new KeyValuePair<string, int>("Ice cream", 4));

            return Json(votes);
        }
     }
}
```



### <a name="deploy-and-run-hello-application-locally"></a><span data-ttu-id="e40bc-167">Dağıtma ve hello uygulama yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e40bc-167">Deploy and run hello application locally</span></span>
<span data-ttu-id="e40bc-168">Şimdi devam edin ve hello uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e40bc-168">You can now go ahead and run hello application.</span></span> <span data-ttu-id="e40bc-169">Visual Studio'da basın `F5` hata ayıklama için toodeploy Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="e40bc-169">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span> <span data-ttu-id="e40bc-170">`F5`Visual Studio olarak daha önce açılmazsa başarısız **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="e40bc-170">`F5` fails if you didn't previously open Visual Studio as **administrator**.</span></span>

> [!NOTE]
> <span data-ttu-id="e40bc-171">Merhaba ilk kez çalıştırma ve yerel olarak hello uygulamayı Visual Studio dağıtmak hata ayıklama için yerel bir küme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e40bc-171">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span>  <span data-ttu-id="e40bc-172">Küme oluşturma biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="e40bc-172">Cluster creation may take some time.</span></span> <span data-ttu-id="e40bc-173">Merhaba küme oluşturma durumunu hello Visual Studio çıktı penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e40bc-173">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="e40bc-174">Bu noktada, web uygulamanızı aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="e40bc-174">At this point, your web app should look like this:</span></span>

![ASP.NET Core ön uç](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

<span data-ttu-id="e40bc-176">Merhaba uygulamada hata ayıklama toostop tooVisual Studio ve tuşuna dönmek **Shift + F5**.</span><span class="sxs-lookup"><span data-stu-id="e40bc-176">toostop debugging hello application, go back tooVisual Studio and press **Shift+F5**.</span></span>

## <a name="add-a-stateful-back-end-service-tooyour-application"></a><span data-ttu-id="e40bc-177">Bir durum bilgisi olan arka uç hizmeti tooyour uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="e40bc-177">Add a stateful back-end service tooyour application</span></span>
<span data-ttu-id="e40bc-178">Biz uygulamamız içinde çalışan bir ASP.NET Web API hizmeti sahip olduğunuza göre edelim ve bir durum bilgisi olan güvenilir hizmet toostore bizim uygulamada bazı verileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e40bc-178">Now that we have an ASP.NET Web API service running in our application, let's go ahead and add a stateful reliable service toostore some data in our application.</span></span>

<span data-ttu-id="e40bc-179">Service Fabric tooconsistently sağlar ve güvenilir koleksiyonları kullanarak hizmetinizin içinde veri hak güvenilir bir şekilde saklayın.</span><span class="sxs-lookup"><span data-stu-id="e40bc-179">Service Fabric allows you tooconsistently and reliably store your data right inside your service by using reliable collections.</span></span> <span data-ttu-id="e40bc-180">C# koleksiyonları kullanan bilinen tooanyone olan yüksek oranda kullanılabilir ve güvenilir koleksiyon sınıfları kümesi güvenilir koleksiyonlarıdır.</span><span class="sxs-lookup"><span data-stu-id="e40bc-180">Reliable collections are a set of highly available and reliable collection classes that are familiar tooanyone who has used C# collections.</span></span>

<span data-ttu-id="e40bc-181">Bu öğreticide, güvenilir bir koleksiyonda bir sayaç değeri depolayan bir hizmet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e40bc-181">In this tutorial, you create a service which stores a counter value in a reliable collection.</span></span>

1. <span data-ttu-id="e40bc-182">Çözüm Gezgini'nde sağ **Hizmetleri** içinde hello uygulama projesi ve seçin **Ekle > Yeni yapı hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="e40bc-182">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Yeni bir hizmet tooan varolan uygulama ekleme](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. <span data-ttu-id="e40bc-184">Merhaba, **yeni Service Fabric hizmeti** iletişim kutusunda, seçin **durum bilgisi olan ASP.NET Core**ve ad hello hizmeti **VotingData** ve basın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e40bc-184">In hello **New Service Fabric Service** dialog, choose **Stateful ASP.NET Core**, and name hello service **VotingData** and press **OK**.</span></span>

    ![Visual Studio'da yeni hizmet iletişim kutusu](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    <span data-ttu-id="e40bc-186">Hizmet projeniz oluşturulduktan sonra uygulamanızda iki hizmetler sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e40bc-186">Once your service project is created, you have two services in your application.</span></span> <span data-ttu-id="e40bc-187">Uygulamanızı toobuild devam ederken, daha fazla hizmet hello ekleyebilirsiniz aynı şekilde.</span><span class="sxs-lookup"><span data-stu-id="e40bc-187">As you continue toobuild your application, you can add more services in hello same way.</span></span> <span data-ttu-id="e40bc-188">Her bağımsız olarak sürümlü hem de yükseltilmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="e40bc-188">Each can be independently versioned and upgraded.</span></span>

3. <span data-ttu-id="e40bc-189">Merhaba sonraki sayfaya ASP.NET Core birtakım proje şablonları sağlar.</span><span class="sxs-lookup"><span data-stu-id="e40bc-189">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="e40bc-190">Bu öğretici için seçin **Web API**.</span><span class="sxs-lookup"><span data-stu-id="e40bc-190">For this tutorial, choose **Web API**.</span></span>

    ![ASP.NET proje türü seçin](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    <span data-ttu-id="e40bc-192">Visual Studio hizmet projesi oluşturur ve bunları Çözüm Gezgini'nde görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e40bc-192">Visual Studio creates a service project and displays them in Solution Explorer.</span></span>

    ![Çözüm Gezgini](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a><span data-ttu-id="e40bc-194">Merhaba VoteDataController.cs dosyası ekleme</span><span class="sxs-lookup"><span data-stu-id="e40bc-194">Add hello VoteDataController.cs file</span></span>

<span data-ttu-id="e40bc-195">Merhaba, **VotingData** Merhaba projeyi sağ tıklatın **denetleyicileri** klasörünü seçip **Ekle -> Yeni öğe sınıfı ->**.</span><span class="sxs-lookup"><span data-stu-id="e40bc-195">In hello **VotingData** project right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span> <span data-ttu-id="e40bc-196">Merhaba dosya "VoteDataController.cs" olarak adlandırın ve tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e40bc-196">Name hello file "VoteDataController.cs" and click **Add**.</span></span> <span data-ttu-id="e40bc-197">Merhaba dosya içeriklerini hello şununla değiştirin ve değişikliklerinizi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e40bc-197">Replace hello file contents with hello following, then save your changes.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.ServiceFabric.Data;
using System.Threading;
using Microsoft.ServiceFabric.Data.Collections;

namespace VotingData.Controllers
{
    [Route("api/[controller]")]
    public class VoteDataController : Controller
    {
        private readonly IReliableStateManager stateManager;

        public VoteDataController(IReliableStateManager stateManager)
        {
            this.stateManager = stateManager;
        }

        // GET api/VoteData
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            var ct = new CancellationToken();

            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                var list = await votesDictionary.CreateEnumerableAsync(tx);

                var enumerator = list.GetAsyncEnumerator();

                var result = new List<KeyValuePair<string, int>>();

                while (await enumerator.MoveNextAsync(ct))
                {
                    result.Add(enumerator.Current);
                }

                return Json(result);
            }
        }

        // PUT api/VoteData/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                await votesDictionary.AddOrUpdateAsync(tx, name, 1, (key, oldvalue) => oldvalue + 1);
                await tx.CommitAsync();
            }

            return new OkResult();
        }

        // DELETE api/VoteData/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                if (await votesDictionary.ContainsKeyAsync(tx, name))
                {
                    await votesDictionary.TryRemoveAsync(tx, name);
                    await tx.CommitAsync();
                    return new OkResult();
                }
                else
                {
                    return new NotFoundResult();
                }
            }
        }
    }
}
```


## <a name="connect-hello-services"></a><span data-ttu-id="e40bc-198">Merhaba Hizmetleri'ne Bağlama</span><span class="sxs-lookup"><span data-stu-id="e40bc-198">Connect hello services</span></span>
<span data-ttu-id="e40bc-199">Bu sonraki adımda, biz hello iki Hizmetleri bağlanmak ve uygulama alma ve hello arka uç hizmetinden bilgi oylama ayarlama ön uç Web hello olun.</span><span class="sxs-lookup"><span data-stu-id="e40bc-199">In this next step, we will connect hello two services and make hello front-end Web application get and set voting information from hello back-end service.</span></span>

<span data-ttu-id="e40bc-200">Service Fabric reliable services ile nasıl iletişim kuracağını tam esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="e40bc-200">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="e40bc-201">Tek bir uygulama içinde TCP üzerinden erişilebilir Hizmetleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="e40bc-201">Within a single application, you might have services that are accessible via TCP.</span></span> <span data-ttu-id="e40bc-202">Bir HTTP REST API erişilebilir diğer hizmetler ve hala diğer hizmetleri web yuvalarını erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="e40bc-202">Other services that might be accessible via an HTTP REST API and still other services could be accessible via web sockets.</span></span> <span data-ttu-id="e40bc-203">Merhaba seçenekleri ve hello bileşim ilgili arka plan için bkz: [hizmetleriyle iletişim kurmasını](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="e40bc-203">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

<span data-ttu-id="e40bc-204">Bu öğreticide, kullanıyoruz [ASP.NET çekirdek Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="e40bc-204">In this tutorial, we are using [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a><span data-ttu-id="e40bc-205">Merhaba VotesController.cs dosyasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="e40bc-205">Update hello VotesController.cs file</span></span>
<span data-ttu-id="e40bc-206">Merhaba, **VotingWeb** proje, açık hello *Controllers/VotesController.cs* dosya.</span><span class="sxs-lookup"><span data-stu-id="e40bc-206">In hello **VotingWeb** project, open hello *Controllers/VotesController.cs* file.</span></span>  <span data-ttu-id="e40bc-207">Hello yerine `VotesController` sınıf tanımı hello aşağıdaki içerikle sonra yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e40bc-207">Replace hello `VotesController` class definition contents with hello following, then save your changes.</span></span>

```csharp
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;
        string serviceProxyUrl = "http://localhost:19081/Voting/VotingData/api/VoteData";
        string partitionKind = "Int64Range";
        string partitionKey = "0";

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            IEnumerable<KeyValuePair<string, int>> votes;

            HttpResponseMessage response = await this.httpClient.GetAsync($"{serviceProxyUrl}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            votes = JsonConvert.DeserializeObject<List<KeyValuePair<string, int>>>(await response.Content.ReadAsStringAsync());

            return Json(votes);
        }

        // PUT: api/Votes/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            string payload = $"{{ 'name' : '{name}' }}";
            StringContent putContent = new StringContent(payload, Encoding.UTF8, "application/json");
            putContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");

            string proxyUrl = $"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}";

            HttpResponseMessage response = await this.httpClient.PutAsync(proxyUrl, putContent);

            return new ContentResult()
            {
                StatusCode = (int)response.StatusCode,
                Content = await response.Content.ReadAsStringAsync()
            };
        }

        // DELETE: api/Votes/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            HttpResponseMessage response = await this.httpClient.DeleteAsync($"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            return new OkResult();

        }
    }
```
<a id="walkthrough" name="walkthrough_anchor"></a>

## <a name="walk-through-hello-voting-sample-application"></a><span data-ttu-id="e40bc-208">Örnek uygulama oylama hello yol</span><span class="sxs-lookup"><span data-stu-id="e40bc-208">Walk through hello voting sample application</span></span>
<span data-ttu-id="e40bc-209">Uygulama oylama hello iki hizmetinden oluşur:</span><span class="sxs-lookup"><span data-stu-id="e40bc-209">hello voting application consists of two services:</span></span>
- <span data-ttu-id="e40bc-210">Web ön uç hizmeti (VotingWeb) - bir ASP.NET Core web hello web sayfası hizmet ön uç hizmeti ve düzenlemenizi sağlayan web API'leri toocommunicate hello arka uç hizmeti ile.</span><span class="sxs-lookup"><span data-stu-id="e40bc-210">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves hello web page and exposes web APIs toocommunicate with hello backend service.</span></span>
- <span data-ttu-id="e40bc-211">Arka uç hizmetine (VotingData)-disk üzerinde bir API toostore hello oy sonuçları güvenilir sözlükte çıkarır kalıcı bir ASP.NET Core web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="e40bc-211">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API toostore hello vote results in a reliable dictionary persisted on disk.</span></span>

![Uygulama diyagramı](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="e40bc-213">Olaylar, aşağıdaki hello uygulama hello oy oluşur:</span><span class="sxs-lookup"><span data-stu-id="e40bc-213">When you vote in hello application hello following events occur:</span></span>
1. <span data-ttu-id="e40bc-214">JavaScript hello oy isteği toohello web API hello web ön uç hizmetinde bir HTTP PUT İsteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="e40bc-214">A JavaScript sends hello vote request toohello web API in hello web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="e40bc-215">Merhaba web ön uç hizmeti proxy toolocate kullanır ve bir HTTP PUT İsteği toohello arka uç hizmeti iletin.</span><span class="sxs-lookup"><span data-stu-id="e40bc-215">hello web front-end service uses a proxy toolocate and forward an HTTP PUT request toohello back-end service.</span></span>

3. <span data-ttu-id="e40bc-216">Merhaba arka uç hizmeti hello gelen isteği alır ve depolar hello hello kümede çoğaltılmış toomultiple düğüm alır ve diskte kalıcı bir güvenilir bir sözlük sonucunda güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="e40bc-216">hello back-end service takes hello incoming request, and stores hello updated result in a reliable dictionary, which gets replicated toomultiple nodes within hello cluster and persisted on disk.</span></span> <span data-ttu-id="e40bc-217">Hiçbir veritabanı gerektiği şekilde tüm hello uygulamanın veri hello kümesinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="e40bc-217">All hello application's data is stored in hello cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="e40bc-218">Visual Studio'da hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="e40bc-218">Debug in Visual Studio</span></span>
<span data-ttu-id="e40bc-219">Visual Studio uygulamasında hata ayıklama sırasında yerel bir Service Fabric geliştirme küme kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="e40bc-219">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="e40bc-220">Hata ayıklama deneyimini tooyour senaryonuz hello seçeneği tooadjust var.</span><span class="sxs-lookup"><span data-stu-id="e40bc-220">You have hello option tooadjust your debugging experience tooyour scenario.</span></span> <span data-ttu-id="e40bc-221">Bu uygulamada, veri arka uç hizmetimizi güvenilir sözlüğünü kullanarak depolarız.</span><span class="sxs-lookup"><span data-stu-id="e40bc-221">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="e40bc-222">Merhaba hata ayıklayıcıyı durdurduğunuzda visual Studio hello uygulama varsayılan başına kaldırır.</span><span class="sxs-lookup"><span data-stu-id="e40bc-222">Visual Studio removes hello application per default when you stop hello debugger.</span></span> <span data-ttu-id="e40bc-223">Merhaba arka ucun neden hello veri Hello uygulamasını kaldırma hizmet tooalso kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="e40bc-223">Removing hello application causes hello data in hello back-end service tooalso be removed.</span></span> <span data-ttu-id="e40bc-224">hata ayıklama oturumları arasında toopersist hello veri hello değiştirebilirsiniz **uygulama hata ayıklama modu** hello bir özellik olarak **oylama** Visual Studio projesi.</span><span class="sxs-lookup"><span data-stu-id="e40bc-224">toopersist hello data between debugging sessions, you can change hello **Application Debug Mode** as a property on hello **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="e40bc-225">toolook nedir hello kod, aşağıdaki adımları tam hello olur:</span><span class="sxs-lookup"><span data-stu-id="e40bc-225">toolook at what happens in hello code, complete hello following steps:</span></span>
1. <span data-ttu-id="e40bc-226">Açık hello **VotesController.cs** dosya ve hello web API'nin bir kesme noktası belirleyerek **Put** yöntemi (satır 47) - hello Visual Studio'da Çözüm Gezgini'nde hello dosyasında arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e40bc-226">Open hello **VotesController.cs** file and set a breakpoint in hello web API's **Put** method (line 47) - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="e40bc-227">Açık hello **VoteDataController.cs** dosya ve bu web API'nin bir kesme noktası belirleyerek **Put** yöntemi (satır 50).</span><span class="sxs-lookup"><span data-stu-id="e40bc-227">Open hello **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="e40bc-228">Toohello tarayıcı geri dönün ve oylama seçeneği tıklatın veya yeni bir oylama seçeneği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e40bc-228">Go back toohello browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="e40bc-229">Merhaba hello web ön uç 's API denetleyicisi içinde ilk kesme noktası isabet.</span><span class="sxs-lookup"><span data-stu-id="e40bc-229">You hit hello first breakpoint in hello web front-end's api controller.</span></span>
    
    1. <span data-ttu-id="e40bc-230">Burada hello JavaScript hello tarayıcıda hello ön uç hizmetinde bir istek toohello web API denetleyicisi gönderir budur.</span><span class="sxs-lookup"><span data-stu-id="e40bc-230">This is where hello JavaScript in hello browser sends a request toohello web API controller in hello front-end service.</span></span>
    
    ![Oy ön uç Hizmet Ekle](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. <span data-ttu-id="e40bc-232">Biz arka uç hizmetimizi hello URL toohello ReverseProxy ilk oluşturmak **(1)**.</span><span class="sxs-lookup"><span data-stu-id="e40bc-232">First we construct hello URL toohello ReverseProxy for our back-end service **(1)**.</span></span>
    3. <span data-ttu-id="e40bc-233">Biz hello HTTP PUT İsteği toohello ReverseProxy Gönder sonra **(2)**.</span><span class="sxs-lookup"><span data-stu-id="e40bc-233">Then we send hello HTTP PUT Request toohello ReverseProxy **(2)**.</span></span>
    4. <span data-ttu-id="e40bc-234">Son olarak hello hello yanıt hello arka uç hizmetine toohello istemciden döndürürüz **(3)**.</span><span class="sxs-lookup"><span data-stu-id="e40bc-234">Finally hello we return hello response from hello back-end service toohello client **(3)**.</span></span>

4. <span data-ttu-id="e40bc-235">Tuşuna **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="e40bc-235">Press **F5** toocontinue</span></span>
    1. <span data-ttu-id="e40bc-236">Artık hello arka uç hizmetinde hello kesme noktası bulunur.</span><span class="sxs-lookup"><span data-stu-id="e40bc-236">You are now at hello break point in hello back-end service.</span></span>
    
    ![Oy arka uç hizmeti ekleme](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. <span data-ttu-id="e40bc-238">Hello yönteminin ilk satırında hello **(1)** hello kullanıyoruz `StateManager` tooget veya adlı güvenilir bir sözlük ekleme `counts`.</span><span class="sxs-lookup"><span data-stu-id="e40bc-238">In hello first line in hello method **(1)** we are using hello `StateManager` tooget or add a reliable dictionary called `counts`.</span></span>
    3. <span data-ttu-id="e40bc-239">Kullanarak bu işlem, güvenilir bir sözlükteki değerlerle tüm etkileşimleri gerektiren deyimi **(2)** bu işlem oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e40bc-239">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    4. <span data-ttu-id="e40bc-240">Merhaba işlemde sonra hello hello seçeneğine oy verdiğiniz için hello ilgili anahtarın değerini güncelleştiriyoruz ve yürütme işlemi hello **(3)**.</span><span class="sxs-lookup"><span data-stu-id="e40bc-240">In hello transaction, we then update hello value of hello relevant key for hello voting option and commits hello operation **(3)**.</span></span> <span data-ttu-id="e40bc-241">Merhaba yürüttükten sonra yöntemi döndürür, veri hello sözlükte güncelleştirilir ve hello kümedeki tooother düğümler çoğaltılan hello.</span><span class="sxs-lookup"><span data-stu-id="e40bc-241">Once hello commit method returns, hello data is updated in hello dictionary and replicated tooother nodes in hello cluster.</span></span> <span data-ttu-id="e40bc-242">Merhaba veriler artık güvenli bir şekilde hello kümesinde depolanır ve hello arka uç hizmetine kullanılabilir hello veri yaşamaya tooother düğümler başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="e40bc-242">hello data is now safely stored in hello cluster, and hello back-end service can fail over tooother nodes, still having hello data available.</span></span>
5. <span data-ttu-id="e40bc-243">Tuşuna **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="e40bc-243">Press **F5** toocontinue</span></span>

<span data-ttu-id="e40bc-244">hata ayıklama oturumunun, basın toostop hello **Shift + F5**.</span><span class="sxs-lookup"><span data-stu-id="e40bc-244">toostop hello debugging session, press **Shift+F5**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e40bc-245">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e40bc-245">Next steps</span></span>
<span data-ttu-id="e40bc-246">Merhaba öğreticinin bu bölümünde, öğrenilen nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="e40bc-246">In this part of hello tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e40bc-247">Durum bilgisi olan güvenilir bir hizmet olarak bir ASP.NET çekirdek Web API hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="e40bc-247">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="e40bc-248">Durum bilgisiz web hizmeti olarak bir ASP.NET çekirdek Web uygulaması hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="e40bc-248">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="e40bc-249">Merhaba durum bilgisi olan hizmeti ile Merhaba ters proxy toocommunicate kullanın</span><span class="sxs-lookup"><span data-stu-id="e40bc-249">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="e40bc-250">Gelişmiş toohello sonraki öğretici:</span><span class="sxs-lookup"><span data-stu-id="e40bc-250">Advance toohello next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e40bc-251">Merhaba uygulama tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="e40bc-251">Deploy hello application tooAzure</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
