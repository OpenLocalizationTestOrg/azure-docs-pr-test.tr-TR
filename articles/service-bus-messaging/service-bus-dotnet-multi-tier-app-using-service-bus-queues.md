---
title: "Azure Service Bus kullanan aaa.NET çok katmanlı uygulaması | Microsoft Docs"
description: "Yardımcı olan bir .NET Öğreticisi Service Bus kuyrukları toocommunicate katmanları arasında kullanan azure'da çok katmanlı bir uygulama geliştirin."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 485910ff1d3b8b0a709ee14ede32e57cf873829a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a>Azure Service Bus kuyruklarını kullanan çok katmanlı .NET uygulaması
## <a name="introduction"></a>Giriş
Microsoft Azure, Visual Studio kullanarak kolaydır ve hello .NET için Azure SDK'sı boş için geliştirme. Bu öğreticide, yerel ortamınızda çalışan birden çok Azure kaynağı kullanan bir uygulama hello adımları toocreate açıklanmaktadır.

Merhaba şunları öğreneceksiniz:

* Nasıl tooenable tek bir Azure geliştirme bilgisayarınıza indirin ve yükleyin.
* Nasıl toouse Visual Studio toodevelop Azure için.
* Nasıl toocreate web ve çalışan rollerini kullanarak azure'da çok katmanlı bir uygulama.
* Service Bus kuyruklarını kullanan toocommunicate arasında katmanlarını nasıl.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

Bu öğreticide oluşturun ve bir Azure bulut hizmetinde hello çok katmanlı uygulamayı çalıştırın. Merhaba ön uç bir ASP.NET MVC web rolü ve hello arka uç Service Bus kuyruğu kullanan bir alt-rolü. Oluşturabileceğiniz hello hello ön uç ile dağıtılan tooan Azure Web sitesi bulut hizmeti yerine bir web projesi, aynı çok katmanlı uygulama. Out hello de deneyebilirsiniz [şirket içi/bulut karma .NET uygulama](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) Öğreticisi.

Merhaba aşağıdaki ekran görüntüsünde tamamlanan hello uygulamayı gösterir.

![][0]

## <a name="scenario-overview-inter-role-communication"></a>Senaryoya genel bakış: roller arası iletişim
toosubmit, hello web rolünde çalışan hello ön uç kullanıcı Arabirimi bileşeninin işlemek için bir sıra hello çalışan rolünde çalışmakta hello orta katman mantığı ile etkileşim kurmalıdır. Bu örnek hello hello katmanlar arasında iletişim için Service Bus Mesajlaşma kullanır.

Hizmet veri yolu kullanarak hello web ve orta katman arasında ileti iki bileşeni birbirinden ayırır. Buna karşılık toodirect (diğer bir deyişle, TCP veya HTTP) Mesajlaşma hello web katmanı bağlanamama toohello orta katman doğrudan; Bunun yerine, iş, birimleri iletileri gibi hizmet güvenilir bir şekilde hello orta katman hazır tooconsume kadar kurtarılmasını ve işlenecekleri Bus hizmetine gönderir.

Hizmet veri yolu sağlayan iki toosupport aracılı Mesajlaşma: sıraları ve konuları. Kuyruklar, her ileti toohello sıra tek bir alıcı tarafından tüketilen gönderilir. Konuları kullanılabilir tooa abonelik hello konuya kaydedilen her yayımlanan ileti yapıldığı hello Yayınla/Abone ol düzenini destekler. Her abonelik mantıksal olarak kendi ileti kuyruğunu korur. Abonelikleri hello filtreyle eşleşen gönderilen ileti hello abonelik sıra toothose için hello kümesini sınırlayan filtre kuralları ile de yapılandırılabilir. Merhaba aşağıdaki örnekte Service Bus kuyrukları kullanılır.

![][1]

Bu iletişim mekanizması, doğrudan mesajlaşma ile karşılaştırıldığında birçok avantaj sunar:

* **Zamana bağlı ayırma.** Merhaba zaman uyumsuz Mesajlaşma düzeni sayesinde üreticilerin ve tüketicilerin hello çevrimiçi olması gerekmez aynı anda. Merhaba kullanıcı tarafı almaya hazır olana kadar hizmet veri yolu iletileri güvenilir bir şekilde depolar. Bu, ya da gönüllü, örneğin, Bakım veya tooa bileşen çökmesinden dolayı sistemin tamamını etkilemeden bağlantısı kesilmiş hello dağıtılmış uygulama toobe hello bileşenlerinin sağlar. Ayrıca, uygulama hello hello günün belirli zamanlarında yalnızca çevrimiçi toocome gerekebilir.
* **Yük dengeleme.** Her iş birimi için gerekli hello işleme süresi genellikle sabit durumdayken birçok uygulamada, sistem yükü zaman içinde değişir. Aracılığıyla ileti üreticileri ve tüketicileri bir kuyruk, uygulama (Merhaba çalışan) yalnızca gereksinimlerini toobe tüketen bu hello yoğun yük yerine tooaccommodate ortalama yük sağlanması anlamına gelir. Merhaba hello sıra derinliği büyüdükçe ve hello gelen Yük hacmi değiştikçe sözleşme. Bu doğrudan hello altyapı gerekli tooservice hello uygulama yük miktarı bakımından paradan tasarruf eder.
* **Yük dengeleme.** Yük arttıkça daha fazla çalışan işlemi hello sıradan tooread eklenebilir. Her ileti tek hello çalışan işlemleri tarafından işlenir. Ayrıca, çalışan makinelerin işleme gücünü bakımından farklılık gösterse bile iletileri kendi maksimum hızında çeker gibi hello çalışan makinelerin optimum kullanımına bu çekme tabanlı yük dengeleme sağlar. Bu desen genellikle hello adlandırılır *rakip tüketici* düzeni.
  
  ![][2]

Aşağıdaki bölümlerde hello bu mimariyi uygulayan hello kod ele alınır.

## <a name="set-up-hello-development-environment"></a>Merhaba geliştirme ortamını ayarlama
Azure uygulamalarını geliştirmeye başlamadan önce hello araçları edinin ve geliştirme ortamınızı ayarlayın.

1. .NET için SDK hello Hello Azure SDK'sını yüklemek [indirmeler sayfası](https://azure.microsoft.com/downloads/).
2. Merhaba, **.NET** sütun hello sürümünü [Visual Studio](http://www.visualstudio.com) kullanmakta olduğunuz. Bu öğretici kullanımda Visual Studio 2015 Hello adımlar, ancak bunlar da Visual Studio 2017 ile çalışır.
3. Toorun istenir veya hello yükleyici kaydettiğinizde tıklatın **çalıştırmak**.
4. Merhaba, **Web Platformu yükleyicisi**,'ı tıklatın **yüklemek** ve hello yükleme işlemine devam edin.
5. Merhaba yüklemesi tamamlandıktan sonra her şeyi olacaktır gerekli toostart toodevelop hello uygulama. Merhaba SDK, Visual Studio'da Azure uygulamalarını kolayca geliştirmenize olanak sağlayan araçları içerir.

## <a name="create-a-namespace"></a>Ad alanı oluşturma
Merhaba sonraki adıma toocreate bir hizmet ad alanıdır ve bir paylaşılan erişim imzası (SAS) anahtarı edinin. Ad alanı, Service Bus tarafından kullanıma sunulan her uygulama için bir uygulama sınırı sağlar. Bir ad alanı oluşturulduğunda hello sistem tarafından bir SAS anahtarı oluşturulur. ad alanı ve SAS anahtarı birleşimi Hello Service Bus tooauthenticate erişim tooan uygulamanız için hello kimlik bilgileri sağlar.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a>Web rolü oluşturma
Bu bölümde, uygulamanızın ön uç hello oluşturun. İlk olarak, uygulamanızın görüntülediği hello sayfaları oluşturun.
Bundan sonra öğeleri tooa Service Bus kuyruğuna gönderir ve hello kuyruk hakkındaki durum bilgilerini görüntüleyen kodu ekleyin.

### <a name="create-hello-project"></a>Başlangıç projesi oluşturma
1. Yönetici ayrıcalıklarını kullanarak Visual Studio'yu başlatın: sağ hello **Visual Studio** program simgesine ve ardından **yönetici olarak çalıştır**. Merhaba, bu makalenin sonraki bölümlerinde ele alınan Azure işlem öykünücüsü, Visual Studio'nun yönetici ayrıcalıklarıyla başlatılmasını gerektirir.
   
   Visual Studio'da, hello **dosya** menüsünde tıklatın **yeni**ve ardından **proje**.
2. **Yüklü Şablonlar**'da **Visual C#** kısmında **Bulut** seçeneğine ve ardından **Azure Bulut Hizmeti**'ne tıklayın. Ad hello proje **MultiTierApp**. Daha sonra, **Tamam**'a tıklayın.
   
   ![][9]
3. **.NET Framework 4.5** rollerinden **ASP.NET Web Rolü**'ne çift tıklayın.
   
   ![][10]
4. Üzerine gelerek **WebRole1** altında **Azure bulut hizmeti çözümü**hello kalem simgesine tıklayın ve hello web rolü çok yeniden adlandırma**FrontendWebRole**. Daha sonra, **Tamam**'a tıklayın. ("Frontend" öğesini "FrontEnd" olarak değil de küçük 'e' ile yazdığınızdan emin olun.)
   
   ![][11]
5. Merhaba gelen **yeni ASP.NET projesi** iletişim kutusunda hello **bir şablon seçin** tıklatın **MVC**.
   
   ![][12]
6. Merhaba yine de **yeni ASP.NET projesi** iletişim kutusunda, hello **kimlik doğrulamayı Değiştir** düğmesi. Merhaba, **kimlik doğrulamayı Değiştir** iletişim kutusu, tıklatın **doğrulaması yok**ve ardından **Tamam**. Bu öğreticide kullanıcının oturum açmasını gerektirmeyen bir uygulamayı dağıtıyorsunuz.
   
    ![][16]
7. Merhaba edilene **yeni ASP.NET projesi** iletişim kutusu, tıklatın **Tamam** toocreate hello projesi.
8. İçinde **Çözüm Gezgini**, hello içinde **FrontendWebRole** projesinde **başvuruları**, ardından **NuGet paketlerini Yönet**.
9. Merhaba tıklatın **Gözat** sekmesini ve ardından arama `Microsoft Azure Service Bus`. Select hello **WindowsAzure.ServiceBus** paketini, tıklatın **yükleme**ve hello kullanım koşullarını kabul edin.
   
   ![][13]
   
   Bu hello gerekli istemci derlemelerine başvuru oluşturulduğunu ve bazı yeni kod dosyaları eklendiğini unutmayın.
10. **Çözüm Gezgini**'nde, **Modeller**'e sağ tıklayın ve ardından **Ekle** ile **Sınıf** seçeneklerine tıklayın. Merhaba, **adı** kutusu, tür hello adı **OnlineOrder.cs**. Daha sonra **Ekle**'ye tıklayın.

### <a name="write-hello-code-for-your-web-role"></a>Merhaba web rolünüz için kod yazma
Bu bölümde, uygulamanızın görüntülediği çeşitli sayfalar hello oluşturun.

1. Merhaba OnlineOrder.cs dosyasında Visual Studio, var olan ad alanı tanımını koddan hello ile değiştirin:
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. **Çözüm Gezgini**'nde **Controllers\HomeController.cs** öğesine çift tıklayın. Merhaba aşağıdakileri ekleyin **kullanarak** deyimleri hello hello üstündeki dosya, yeni oluşturduğunuz, Service Bus hizmetinin yanı sıra modelin tooinclude hello ad alanları.
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. Ayrıca hello HomeController.cs dosyasında Visual Studio, var olan ad alanı tanımını koddan hello ile değiştirin. Bu kod öğeleri toohello sırasının hello gönderimi işlenmesine yönelik yöntemler içerir.
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect tooSubmit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for hello submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from hello submission
           // form.
           [HttpPost]
           // Attribute toohelp prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting tooqueue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. Merhaba gelen **yapı** menüsünde tıklatın **yapı çözümü** tootest hello çalışmanızın o ana kadarki doğruluğunu.
5. Şimdi, hello hello görünümünü oluşturmak `Submit()` daha önce oluşturduğunuz yöntemi. İçinde Hello sağ `Submit()` yöntemi (Merhaba aşırı yüklemesini `Submit()` parametre almayan) ve ardından **Görünüm Ekle**.
   
   ![][14]
6. Merhaba görünümü oluşturmak için bir iletişim kutusu görüntülenir. Merhaba, **şablonu** listesinde, seçin **oluşturma**. Merhaba, **Model sınıfı** hello tıklatın **OnlineOrder** sınıfı.
   
   ![][15]
7. **Ekle**'ye tıklayın.
8. Şimdi, uygulamanızın görüntülenen hello adını değiştirin. İçinde **Çözüm Gezgini**, çift **görünümler/paylaşılan\\_Layout.cshtml** tooopen dosya hello Visual Studio düzenleyicisinde içinde.
9. **My ASP.NET Application** uygulamasının tüm örneklerini **LITWARE's Products** olarak değiştirin.
10. Merhaba kaldırmak **giriş**, **hakkında**, ve **kişi** bağlantılar. Merhaba vurgulanmış kodu silme:
    
    ![][28]
11. Son olarak, hello gönderme sayfası tooinclude hello sırası hakkında bazı bilgiler değiştirin. İçinde **Çözüm Gezgini**, çift **Views\Home\Submit.cshtml** tooopen dosya hello Visual Studio düzenleyicisinde içinde. Satır sonlarında aşağıdaki hello eklemek `<h2>Submit</h2>`. Şimdilik, hello `ViewBag.MessageCount` boş. Bu alanı daha sonra dolduracaksınız.
    
    ```html
    <p>Current number of orders in queue waiting toobe processed: @ViewBag.MessageCount</p>
    ```
12. Şu anda kullanıcı arabiriminizi uyguladınız. Basabilirsiniz **F5** toorun uygulamanız ve istediğiniz gibi göründüğünü doğrulayın.
    
    ![][17]

### <a name="write-hello-code-for-submitting-items-tooa-service-bus-queue"></a>Öğeleri tooa Service Bus kuyruğuna göndermek için hello kod yazma
Şimdi, öğeleri tooa sıraya göndermek için kodu ekleyin. İlk olarak, Service Bus kuyruğunuzun bağlantı bilgilerini içeren bir sınıf oluşturun. Ardından, bağlantınızı Global.aspx.cs üzerinden başlatın. Son olarak, daha önce HomeController.cs tooactually gönderme öğeleri tooa Service Bus sırada oluşturduğunuz hello gönderme kodunu güncelleştirin.

1. İçinde **Çözüm Gezgini**, sağ **FrontendWebRole** (sağ hello proje, hello rolü değil). **Ekle** seçeneğine ve ardından **Sınıf**'a tıklayın.
2. Ad hello sınıfı **QueueConnector.cs**. Tıklatın **Ekle** toocreate hello sınıfı.
3. Şimdi, hello bağlantı bilgilerini yalıtan ve hello bağlantı tooa Service Bus kuyruğuna başlatan kodu ekleyin. QueueConnector.cs tüm içeriğini Hello koddan hello ile değiştirin ve için değerleri girin `your Service Bus namespace` (ad alanı adınız) ve `yourKey`, hello olduğu **birincil anahtar** hello Azure ' daha önce edindiğiniz Portal.
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from hello portal.
           public const string Namespace = "your Service Bus namespace";
   
           // hello name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create hello namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http toobe friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create hello namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create hello queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client toohello queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. Şimdi **Başlat** yönteminizin çağrıldığından emin olun. **Çözüm Gezgini**'nde **Global.asax\Global.asax.cs** öğesine çift tıklayın.
5. Aşağıdaki kod hello hello sonunda hello eklemek **Application_Start** yöntemi.
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. Son olarak, öğeleri toohello sıraya göndermek için daha önce oluşturduğunuz hello web kodunu güncelleştirin. **Çözüm Gezgini**'nde **Controllers\HomeController.cs** öğesine çift tıklayın.
7. Güncelleştirme hello `Submit()` yöntemini (parametre almayan hello aşırı yük) aşağıdaki gibi tooget selamlama iletisine saymak hello sırası.
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you tooperform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get hello queue, and obtain hello message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. Güncelleştirme hello `Submit(OnlineOrder order)` yöntemi (bir parametre alan hello aşırı yük) aşağıdaki gibi toosubmit sipariş bilgilerini toohello sırası.
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from hello order.
           var message = new BrokeredMessage(order);
   
           // Submit hello order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. Şimdi hello uygulamayı tekrar çalıştırabilirsiniz. Bir sipariş göndermek her zaman hello ileti sayısı da artar.
   
   ![][18]

## <a name="create-hello-worker-role"></a>Merhaba çalışan rolü oluşturma
Şimdi hello sipariş gönderimlerini işleyen hello çalışan rolü oluşturun. Bu örnek hello kullanır **Service Bus kuyruğu içeren çalışan rolü** Visual Studio Proje şablonu. Merhaba gerekli kimlik bilgileri zaten hello portaldan almıştınız.

1. Visual Studio tooyour Azure hesabı bağladığınızdan emin olun.
2. Visual Studio'da içinde **Çözüm Gezgini** sağ **rolleri** hello altında bir klasör **MultiTierApp** projesi.
3. **Ekle**'ye ve ardından **Yeni Çalışan Rolü Projesi**'ne tıklayın. Merhaba **yeni rol projesi Ekle** iletişim kutusu görüntülenir.
   
   ![][26]
4. Merhaba, **yeni rol projesi Ekle** iletişim kutusu, tıklatın **Service Bus kuyruğu içeren çalışan rolü**.
   
   ![][23]
5. Merhaba, **adı** kutusu, ad hello proje **OrderProcessingRole**. Daha sonra **Ekle**'ye tıklayın.
6. Merhaba "Service Bus ad alanı oluşturma" bölümünde toohello Pano 9. adımında elde ettiğiniz hello bağlantı dizesini kopyalayın.
7. İçinde **Çözüm Gezgini**, sağ hello **OrderProcessingRole** 5. adımda oluşturduğunuz (, sağ emin olun **OrderProcessingRole** altında**Rolleri**, ve sınıf hello değil). Daha sonra **Özellikler**'e tıklayın.
8. Merhaba üzerinde **ayarları** hello sekmesinde **özellikleri** iletişim kutusunda hello içinde **değeri** kutusunun **Microsoft.ServiceBus.ConnectionString**ve 6. adımda kopyaladığınız hello uç nokta değerini yapıştırın.
   
   ![][25]
9. Oluşturma bir **OnlineOrder** hello sıradan işlemek gibi toorepresent hello siparişleri sınıfı. Önceden oluşturduğunuz bir sınıfı yeniden kullanabilirsiniz. İçinde **Çözüm Gezgini**, sağ hello **OrderProcessingRole** sınıfı (sağ hello sınıf simgesi, hello rolü değil). **Ekle**'ye ve **Var Olan Öğe**'ye tıklayın.
10. Toohello alt klasör için Gözat **FrontendWebRole\Models**, çift tıklayın ve ardından **OnlineOrder.cs** tooadd, toothis projesi.
11. İçinde **WorkerRole.cs**, hello hello değerini değiştirme **QueueName** değişkeni `"ProcessingQueue"` çok`"OrdersQueue"` hello kod aşağıdaki gösterildiği gibi.
    
    ```csharp
    // hello name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. Merhaba aşağıdakileri ekleyin hello'hello WorkerRole.cs dosyasının üst kısmında deyimiyle.
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. Merhaba, `Run()` işlevinde hello `OnMessage()` çağrısı, hello hello içeriğini değiştirin `try` yan tümcesiyle birlikte koddan hello.
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View hello message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. Merhaba uygulaması tamamladınız. Çözüm Gezgini'nde hello MultiTierApp projesine sağ tıklayarak hello tam uygulama sınayabilirsiniz seçme **başlangıç projesi olarak ayarla**ve F5 tuşuna basın. Merhaba çalışan rolü öğeleri hello sırasından işler ve bunları tamamlanmış olarak işaretler olduğundan ileti sayısında artış olmayacağını unutmayın. Hello Azure işlem öykünücüsü kullanıcı Arabiriminde görüntüleyerek çalışan rolünüzün izleme çıktısını hello görebilirsiniz. Merhaba bildirim alanı görev çubuğunuzdaki hello öykünücü simgesine sağ tıklayıp seçerek bunu yapabilirsiniz **Göster işlem öykünücüsü kullanıcı Arabiriminde**.
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a>Sonraki adımlar
Service Bus hakkında daha fazla toolearn kaynakları aşağıdaki hello bakın:  

* [Azure Service Bus belgeleri][sbdocs]  
* [Service Bus hizmet sayfası][sbacom]  
* [Nasıl tooUse hizmet veri yolu kuyrukları][sbacomqhowto]  

çok katmanlı senaryoları hakkında daha fazla toolearn bakın:  

* [Depolama Tabloları, Kuyruklar ve Blob'ların Kullanıldığı .NET Çok Katmanlı Uygulaması][mutitierstorage]  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36
