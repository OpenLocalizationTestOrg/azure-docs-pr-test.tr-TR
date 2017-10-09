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
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a>Bir ASP.NET çekirdek Web API ön uç hizmeti ve durum bilgisi olan bir arka uç hizmeti ile bir uygulama oluşturun ve dağıtın
Bu öğretici bir dizi birini bir parçasıdır.  Verilerinizin nasıl toocreate bir Azure Service Fabric uygulaması bir ASP.NET çekirdek Web API ön ile bitmelidir ve bir durum bilgisi olan arka uç hizmetine toostore öğreneceksiniz. İşlemi tamamladığınızda, oylama bir durum bilgisi olan bir arka uç hizmetinde hello kümedeki Oylama sonuçlarını kaydettiği ön uç bir ASP.NET Core web uygulamasıyla sahip. Toomanually istemiyorsanız, uygulama oylama hello oluşturma, şunları yapabilirsiniz [hello kaynak kodunu indirebilir](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) Merhaba uygulama tamamlandı ve İleri çok atlayabilirsiniz[örnek uygulama oylama hello yol](#walkthrough_anchor).

![Uygulama diyagramı](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

Bölümünde hello serisi birini öğrenin nasıl yapılır:

> [!div class="checklist"]
> * Durum bilgisi olan güvenilir bir hizmet olarak bir ASP.NET çekirdek Web API hizmeti oluşturma
> * Durum bilgisiz web hizmeti olarak bir ASP.NET çekirdek Web uygulaması hizmeti oluşturma
> * Merhaba durum bilgisi olan hizmeti ile Merhaba ters proxy toocommunicate kullanın

Bu öğretici serisinde öğrenin nasıl yapılır:
> [!div class="checklist"]
> * Bir .NET Service Fabric uygulaması oluşturma
> * [Merhaba uygulama tooa uzak kümesi dağıtma](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [CI/CD Visual Studio Team Services kullanarak yapılandırma](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce:
- Bir Azure aboneliğiniz yoksa, oluşturma bir [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [Visual Studio 2017 yükleme](https://www.visualstudio.com/) hello yükleyip **Azure geliştirme** ve **ASP.NET ve web geliştirme** iş yükleri.
- [Merhaba Service Fabric SDK yükleme](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a>Bir ASP.NET Web API hizmeti güvenilir bir hizmet olarak oluşturma
İlk olarak hello web ön ucu ASP.NET Core kullanarak uygulama oylama hello olarak oluşturun. ASP.NET Core toocreate modern web kullanıcı arabirimini kullanın ve API web bir basit, platformlar arası web geliştirme altyapısıdır. ASP.NET Core Service Fabric ile nasıl tümleşik çalıştığını'nın tam bir anlayış tooget öneririz hello okuma [Service Fabric Reliable Services ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) makalesi. Şu an için hızlı şekilde kullanmaya Bu öğretici tooget izleyebilirsiniz. ASP.NET Çekirdeği hakkında daha fazla toolearn hello bkz [ASP.NET Core belgeleri](https://docs.microsoft.com/aspnet/core/).

> [!NOTE]
> Bu öğretici hello üzerinde temel [ASP.NET Core araçları için Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc). Merhaba .NET Core araçları Visual Studio 2015 için artık güncelleştiriliyor.

1. Visual Studio'yu **yönetici** olarak başlatın.

2. Bir proje oluşturun **dosya**->**yeni**->**proje**

3. Merhaba, **yeni proje** iletişim kutusunda, seçin **bulut > Service Fabric uygulaması**.

4. Ad Merhaba uygulaması **oylama** ve basın **Tamam**.

   ![Visual Studio'da yeni proje iletişim kutusu](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. Merhaba üzerinde **yeni yapı hizmeti** sayfasında, **durum bilgisiz ASP.NET Core**ve hizmetinizin adını **VotingWeb**.
   
   ![ASP.NET web hizmeti hello yeni hizmet iletişim kutusunda seçme](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. Merhaba sonraki sayfaya ASP.NET Core birtakım proje şablonları sağlar. Bu öğretici için seçin **Web uygulaması**. 
   
   ![ASP.NET proje türü seçin](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   Visual Studio, uygulama ve hizmet projesi oluşturur ve bunları Çözüm Gezgini'nde görüntüler.

   ![ASP.NET core Web API hizmeti içeren uygulama oluşturulduktan sonra Çözüm Gezgini]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a>AngularJS toohello VotingWeb Hizmet Ekle
Ekleme [AngularJS](http://angularjs.org/) hello yerleşik kullanarak tooyour hizmet [Bower Destek](/aspnet/core/client-side/bower). Açık *bower.json* ve Açısal ve önyükleme Açısal girişlerini ekleyin, sonra yaptığınız değişiklikleri kaydedin.

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
Merhaba kaydetme sırasında *bower.json* dosya, Angular projenizin içinde yüklü *wwwroot/lib* klasör. Ayrıca, hello içinde listelenen *bağımlılıkları/Bower* klasör.

### <a name="update-hello-sitejs-file"></a>Merhaba site.js dosyasını güncelleştirme
Açık hello *wwwroot/js/site.js* dosya.  İçeriği hello hello giriş görünümleri tarafından kullanılan JavaScript ile değiştirin:

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

### <a name="update-hello-indexcshtml-file"></a>Merhaba Index.cshtml dosyasını güncelleştirme
Açık hello *Views/Home/Index.cshtml* dosya, hello görünüm belirli toohello giriş denetleyicisi.  İçeriğinin hello şununla değiştirin ve değişikliklerinizi kaydedin.

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

### <a name="update-hello-layoutcshtml-file"></a>Merhaba _Layout.cshtml dosyasını güncelleştirme
Açık hello *Views/Shared/_Layout.cshtml* dosya, hello ASP.NET uygulaması için hello varsayılan düzeni.  İçeriğinin hello şununla değiştirin ve değişikliklerinizi kaydedin.

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

### <a name="update-hello-votingwebcs-file"></a>Merhaba VotingWeb.cs dosyasını güncelleştirme
Açık hello *VotingWeb.cs* hello ASP.NET Core WebHost hello WebListener web sunucusu kullanarak hello durum bilgisiz hizmeti içinde oluşturur dosya.  Merhaba eklemek `using System.Net.Http;` yönerge toohello dosyasının üst kısmında hello.  Hello yerine `CreateServiceInstanceListeners()` işlev hello aşağıdakilerle sonra yaptığınız değişiklikleri kaydedin.

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

### <a name="add-hello-votescontrollercs-file"></a>Merhaba VotesController.cs dosyası ekleme
Oylama Eylemler tanımlayan bir denetleyici ekleyin. Hello üzerinde sağ **denetleyicileri** klasörünü seçip **Ekle -> Yeni öğe sınıfı ->**.  Merhaba dosya "VotesController.cs" olarak adlandırın ve tıklatın **Ekle**.  Merhaba dosya içeriklerini hello şununla değiştirin ve değişikliklerinizi kaydedin.  Daha sonra [güncelleştirme hello VotesController.cs dosyası](#updatevotecontroller_anchor), bu dosyası değiştirilmiş tooread ve hello arka uç hizmetinden oylama veri yazma.  Şu an için statik bir dize veri toohello görünümü hello denetleyicisi döndürür.

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



### <a name="deploy-and-run-hello-application-locally"></a>Dağıtma ve hello uygulama yerel olarak çalıştırma
Şimdi devam edin ve hello uygulamayı çalıştırın. Visual Studio'da basın `F5` hata ayıklama için toodeploy Merhaba uygulaması. `F5`Visual Studio olarak daha önce açılmazsa başarısız **yönetici**.

> [!NOTE]
> Merhaba ilk kez çalıştırma ve yerel olarak hello uygulamayı Visual Studio dağıtmak hata ayıklama için yerel bir küme oluşturur.  Küme oluşturma biraz zaman alabilir. Merhaba küme oluşturma durumunu hello Visual Studio çıktı penceresinde görüntülenir.

Bu noktada, web uygulamanızı aşağıdaki gibi görünmelidir:

![ASP.NET Core ön uç](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

Merhaba uygulamada hata ayıklama toostop tooVisual Studio ve tuşuna dönmek **Shift + F5**.

## <a name="add-a-stateful-back-end-service-tooyour-application"></a>Bir durum bilgisi olan arka uç hizmeti tooyour uygulaması ekleyin
Biz uygulamamız içinde çalışan bir ASP.NET Web API hizmeti sahip olduğunuza göre edelim ve bir durum bilgisi olan güvenilir hizmet toostore bizim uygulamada bazı verileri ekleyin.

Service Fabric tooconsistently sağlar ve güvenilir koleksiyonları kullanarak hizmetinizin içinde veri hak güvenilir bir şekilde saklayın. C# koleksiyonları kullanan bilinen tooanyone olan yüksek oranda kullanılabilir ve güvenilir koleksiyon sınıfları kümesi güvenilir koleksiyonlarıdır.

Bu öğreticide, güvenilir bir koleksiyonda bir sayaç değeri depolayan bir hizmet oluşturun.

1. Çözüm Gezgini'nde sağ **Hizmetleri** içinde hello uygulama projesi ve seçin **Ekle > Yeni yapı hizmeti**.
   
    ![Yeni bir hizmet tooan varolan uygulama ekleme](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. Merhaba, **yeni Service Fabric hizmeti** iletişim kutusunda, seçin **durum bilgisi olan ASP.NET Core**ve ad hello hizmeti **VotingData** ve basın **Tamam**.

    ![Visual Studio'da yeni hizmet iletişim kutusu](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    Hizmet projeniz oluşturulduktan sonra uygulamanızda iki hizmetler sahiptir. Uygulamanızı toobuild devam ederken, daha fazla hizmet hello ekleyebilirsiniz aynı şekilde. Her bağımsız olarak sürümlü hem de yükseltilmiş olabilir.

3. Merhaba sonraki sayfaya ASP.NET Core birtakım proje şablonları sağlar. Bu öğretici için seçin **Web API**.

    ![ASP.NET proje türü seçin](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    Visual Studio hizmet projesi oluşturur ve bunları Çözüm Gezgini'nde görüntüler.

    ![Çözüm Gezgini](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a>Merhaba VoteDataController.cs dosyası ekleme

Merhaba, **VotingData** Merhaba projeyi sağ tıklatın **denetleyicileri** klasörünü seçip **Ekle -> Yeni öğe sınıfı ->**. Merhaba dosya "VoteDataController.cs" olarak adlandırın ve tıklatın **Ekle**. Merhaba dosya içeriklerini hello şununla değiştirin ve değişikliklerinizi kaydedin.

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


## <a name="connect-hello-services"></a>Merhaba Hizmetleri'ne Bağlama
Bu sonraki adımda, biz hello iki Hizmetleri bağlanmak ve uygulama alma ve hello arka uç hizmetinden bilgi oylama ayarlama ön uç Web hello olun.

Service Fabric reliable services ile nasıl iletişim kuracağını tam esneklik sağlar. Tek bir uygulama içinde TCP üzerinden erişilebilir Hizmetleri olabilir. Bir HTTP REST API erişilebilir diğer hizmetler ve hala diğer hizmetleri web yuvalarını erişilebilir. Merhaba seçenekleri ve hello bileşim ilgili arka plan için bkz: [hizmetleriyle iletişim kurmasını](service-fabric-connect-and-communicate-with-services.md).

Bu öğreticide, kullanıyoruz [ASP.NET çekirdek Web API](service-fabric-reliable-services-communication-aspnetcore.md).

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a>Merhaba VotesController.cs dosyasını güncelleştirme
Merhaba, **VotingWeb** proje, açık hello *Controllers/VotesController.cs* dosya.  Hello yerine `VotesController` sınıf tanımı hello aşağıdaki içerikle sonra yaptığınız değişiklikleri kaydedin.

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

## <a name="walk-through-hello-voting-sample-application"></a>Örnek uygulama oylama hello yol
Uygulama oylama hello iki hizmetinden oluşur:
- Web ön uç hizmeti (VotingWeb) - bir ASP.NET Core web hello web sayfası hizmet ön uç hizmeti ve düzenlemenizi sağlayan web API'leri toocommunicate hello arka uç hizmeti ile.
- Arka uç hizmetine (VotingData)-disk üzerinde bir API toostore hello oy sonuçları güvenilir sözlükte çıkarır kalıcı bir ASP.NET Core web hizmeti.

![Uygulama diyagramı](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

Olaylar, aşağıdaki hello uygulama hello oy oluşur:
1. JavaScript hello oy isteği toohello web API hello web ön uç hizmetinde bir HTTP PUT İsteği gönderir.

2. Merhaba web ön uç hizmeti proxy toolocate kullanır ve bir HTTP PUT İsteği toohello arka uç hizmeti iletin.

3. Merhaba arka uç hizmeti hello gelen isteği alır ve depolar hello hello kümede çoğaltılmış toomultiple düğüm alır ve diskte kalıcı bir güvenilir bir sözlük sonucunda güncelleştirilir. Hiçbir veritabanı gerektiği şekilde tüm hello uygulamanın veri hello kümesinde depolanır.

## <a name="debug-in-visual-studio"></a>Visual Studio'da hata ayıklama
Visual Studio uygulamasında hata ayıklama sırasında yerel bir Service Fabric geliştirme küme kullanıyor. Hata ayıklama deneyimini tooyour senaryonuz hello seçeneği tooadjust var. Bu uygulamada, veri arka uç hizmetimizi güvenilir sözlüğünü kullanarak depolarız. Merhaba hata ayıklayıcıyı durdurduğunuzda visual Studio hello uygulama varsayılan başına kaldırır. Merhaba arka ucun neden hello veri Hello uygulamasını kaldırma hizmet tooalso kaldırılır. hata ayıklama oturumları arasında toopersist hello veri hello değiştirebilirsiniz **uygulama hata ayıklama modu** hello bir özellik olarak **oylama** Visual Studio projesi.

toolook nedir hello kod, aşağıdaki adımları tam hello olur:
1. Açık hello **VotesController.cs** dosya ve hello web API'nin bir kesme noktası belirleyerek **Put** yöntemi (satır 47) - hello Visual Studio'da Çözüm Gezgini'nde hello dosyasında arayabilirsiniz.

2. Açık hello **VoteDataController.cs** dosya ve bu web API'nin bir kesme noktası belirleyerek **Put** yöntemi (satır 50).

3. Toohello tarayıcı geri dönün ve oylama seçeneği tıklatın veya yeni bir oylama seçeneği ekleyin. Merhaba hello web ön uç 's API denetleyicisi içinde ilk kesme noktası isabet.
    
    1. Burada hello JavaScript hello tarayıcıda hello ön uç hizmetinde bir istek toohello web API denetleyicisi gönderir budur.
    
    ![Oy ön uç Hizmet Ekle](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. Biz arka uç hizmetimizi hello URL toohello ReverseProxy ilk oluşturmak **(1)**.
    3. Biz hello HTTP PUT İsteği toohello ReverseProxy Gönder sonra **(2)**.
    4. Son olarak hello hello yanıt hello arka uç hizmetine toohello istemciden döndürürüz **(3)**.

4. Tuşuna **F5** toocontinue
    1. Artık hello arka uç hizmetinde hello kesme noktası bulunur.
    
    ![Oy arka uç hizmeti ekleme](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. Hello yönteminin ilk satırında hello **(1)** hello kullanıyoruz `StateManager` tooget veya adlı güvenilir bir sözlük ekleme `counts`.
    3. Kullanarak bu işlem, güvenilir bir sözlükteki değerlerle tüm etkileşimleri gerektiren deyimi **(2)** bu işlem oluşturur.
    4. Merhaba işlemde sonra hello hello seçeneğine oy verdiğiniz için hello ilgili anahtarın değerini güncelleştiriyoruz ve yürütme işlemi hello **(3)**. Merhaba yürüttükten sonra yöntemi döndürür, veri hello sözlükte güncelleştirilir ve hello kümedeki tooother düğümler çoğaltılan hello. Merhaba veriler artık güvenli bir şekilde hello kümesinde depolanır ve hello arka uç hizmetine kullanılabilir hello veri yaşamaya tooother düğümler başarısız olabilir.
5. Tuşuna **F5** toocontinue

hata ayıklama oturumunun, basın toostop hello **Shift + F5**.


## <a name="next-steps"></a>Sonraki adımlar
Merhaba öğreticinin bu bölümünde, öğrenilen nasıl yapılır:

> [!div class="checklist"]
> * Durum bilgisi olan güvenilir bir hizmet olarak bir ASP.NET çekirdek Web API hizmeti oluşturma
> * Durum bilgisiz web hizmeti olarak bir ASP.NET çekirdek Web uygulaması hizmeti oluşturma
> * Merhaba durum bilgisi olan hizmeti ile Merhaba ters proxy toocommunicate kullanın

Gelişmiş toohello sonraki öğretici:
> [!div class="nextstepaction"]
> [Merhaba uygulama tooAzure dağıtma](service-fabric-tutorial-deploy-app-to-party-cluster.md)
