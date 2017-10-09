## <a name="create-hello-webapi-project"></a><span data-ttu-id="213ad-101">Merhaba Webapı projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="213ad-101">Create hello WebAPI Project</span></span>
<span data-ttu-id="213ad-102">Yeni bir ASP.NET Webapı arka izleyin hello bölümlerde oluşturulur ve üç ana amacı vardır:</span><span class="sxs-lookup"><span data-stu-id="213ad-102">A new ASP.NET WebAPI backend will be created in hello sections that follow and it will have three main purposes:</span></span>

1. <span data-ttu-id="213ad-103">**Kimlik doğrulaması yapan istemcilerin**: ileti işleyicisi sonraki tooauthenticate istemci istekleri ve hello isteği ile ilişkilendirme hello kullanıcı eklenir.</span><span class="sxs-lookup"><span data-stu-id="213ad-103">**Authenticating Clients**: A message handler will be added later tooauthenticate client requests and associate hello user with hello request.</span></span>
2. <span data-ttu-id="213ad-104">**İstemci bildirim kayıtları**: denetleyicisi toohandle yeni kayıtlar için bir istemci cihaz tooreceive bildirimleri daha sonra ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="213ad-104">**Client Notification Registrations**: Later, you will add a controller toohandle new registrations for a client device tooreceive notifications.</span></span> <span data-ttu-id="213ad-105">Merhaba kimliği doğrulanmış kullanıcı adı otomatik olarak toohello kayıt olarak eklenecek bir [etiketi](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span><span class="sxs-lookup"><span data-stu-id="213ad-105">hello authenticated user name will automatically be added toohello registration as a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span></span>
3. <span data-ttu-id="213ad-106">**Bildirimleri tooClients gönderme**: daha sonra siz de denetleyicisi tooprovide kullanıcı tootrigger güvenli itme toodevices yolu ve istemciler hello etiketiyle ilişkili ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="213ad-106">**Sending Notifications tooClients**: Later, you will also add a controller tooprovide a way for a user tootrigger a secure push toodevices and clients associated with hello tag.</span></span> 

<span data-ttu-id="213ad-107">Aşağıdaki adımları hello nasıl toocreate hello yeni ASP.NET Webapı arka uç göster:</span><span class="sxs-lookup"><span data-stu-id="213ad-107">hello following steps show how toocreate hello new ASP.NET WebAPI backend:</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="213ad-108">Visual Studio 2015 kullanıyorsanız veya önceki sürümleri, bu öğreticiye başlamadan önce lütfen hello hello NuGet Paket Yöneticisi en son sürümünü yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="213ad-108">If you are using Visual Studio 2015 or earlier, before starting this tutorial, please ensure that you have installed hello latest version of hello NuGet Package Manager.</span></span> <span data-ttu-id="213ad-109">toocheck, Visual Studio Başlangıç.</span><span class="sxs-lookup"><span data-stu-id="213ad-109">toocheck, start Visual Studio.</span></span> <span data-ttu-id="213ad-110">Merhaba gelen **Araçları** menüsünde tıklatın **Uzantılar ve güncelleştirmeler**.</span><span class="sxs-lookup"><span data-stu-id="213ad-110">From hello **Tools** menu, click **Extensions and Updates**.</span></span> <span data-ttu-id="213ad-111">Arama **NuGet Paket Yöneticisi** hello en son sürümü yüklü sürümü için Visual Studio ve emin olun.</span><span class="sxs-lookup"><span data-stu-id="213ad-111">Search for **NuGet Package Manager** for your version of Visual Studio, and make sure you have hello latest version.</span></span> <span data-ttu-id="213ad-112">Aksi takdirde, kaldırın, ardından hello NuGet Paket Yöneticisi'ni yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="213ad-112">If not, please uninstall, then reinstall hello NuGet Package Manager.</span></span>
> 
> ![][B4]
> 
> [!NOTE]
> <span data-ttu-id="213ad-113">Visual Studio hello yüklediğinizden emin olun [Azure SDK'sı](https://azure.microsoft.com/downloads/) Web dağıtımı için.</span><span class="sxs-lookup"><span data-stu-id="213ad-113">Make sure you have installed hello Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) for website deployment.</span></span>
> 
> 

1. <span data-ttu-id="213ad-114">Visual Studio veya Visual Studio Express’i başlatın.</span><span class="sxs-lookup"><span data-stu-id="213ad-114">Start Visual Studio or Visual Studio Express.</span></span> <span data-ttu-id="213ad-115">Tıklatın **Sunucu Gezgini** ve tooyour Azure hesabı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="213ad-115">Click **Server Explorer** and sign in tooyour Azure account.</span></span> <span data-ttu-id="213ad-116">Visual Studio toocreate hello web sitesi kaynakları hesabınızda imzalı ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="213ad-116">Visual Studio will need you signed in toocreate hello web site resources on your account.</span></span>
2. <span data-ttu-id="213ad-117">Visual Studio'da sırasıyla **dosya**, ardından **yeni**, ardından **proje**, genişletin **şablonları**, **Visual C#**, ardından **Web** ve **ASP.NET Web uygulaması**, tür hello adı **AppBackend**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="213ad-117">In Visual Studio, click **File**, then click **New**, then **Project**, expand **Templates**, **Visual C#**, then click **Web** and **ASP.NET Web Application**, type hello name **AppBackend**, and then click **OK**.</span></span> 
   
    ![][B1]
3. <span data-ttu-id="213ad-118">Merhaba, **yeni ASP.NET projesi** iletişim kutusunda, tıklatın **Web API**, ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="213ad-118">In hello **New ASP.NET Project** dialog, click **Web API**, then click **OK**.</span></span>
   
    ![][B2]
4. <span data-ttu-id="213ad-119">Merhaba, **yapılandırma Microsoft Azure Web uygulaması** iletişim kutusunda, bir abonelik seçin ve bir **uygulama hizmeti planı** zaten oluşturmuş.</span><span class="sxs-lookup"><span data-stu-id="213ad-119">In hello **Configure Microsoft Azure Web App** dialog, choose a subscription, and an **App Service plan** you have already created.</span></span> <span data-ttu-id="213ad-120">Ayrıca seçebilirsiniz **yeni bir uygulama hizmeti planı oluştur** hello iletişim kutusundan oluşturun.</span><span class="sxs-lookup"><span data-stu-id="213ad-120">You can also choose **Create a new app service plan** and create one from hello dialog.</span></span> <span data-ttu-id="213ad-121">Bu öğretici için bir veritabanı gerekmez.</span><span class="sxs-lookup"><span data-stu-id="213ad-121">You do not need a database for this tutorial.</span></span> <span data-ttu-id="213ad-122">Uygulama hizmet planınız seçtikten sonra tıklatın **Tamam** toocreate hello projesi.</span><span class="sxs-lookup"><span data-stu-id="213ad-122">Once you have selected your app service plan, click **OK** toocreate hello project.</span></span>
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a><span data-ttu-id="213ad-123">İstemcileri toohello Webapı arka uç kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="213ad-123">Authenticating Clients toohello WebAPI Backend</span></span>
<span data-ttu-id="213ad-124">Bu bölümde, adlı yeni bir ileti işleyicisi sınıfı oluşturacak **AuthenticationTestHandler** hello yeni arka uç için.</span><span class="sxs-lookup"><span data-stu-id="213ad-124">In this section, you will create a new message handler class named **AuthenticationTestHandler** for hello new backend.</span></span> <span data-ttu-id="213ad-125">Bu sınıfın türetildiği [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) ve hello arka uç gelen tüm istekleri işleyebilmek için ileti işleyicisi eklenir.</span><span class="sxs-lookup"><span data-stu-id="213ad-125">This class is derived from [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) and added as a message handler so it can process all requests coming into hello backend.</span></span> 

1. <span data-ttu-id="213ad-126">Çözüm Gezgini'nde hello sağ **AppBackend** proje, tıklatın **Ekle**, ardından **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="213ad-126">In Solution Explorer, right-click hello **AppBackend** project, click **Add**, then click **Class**.</span></span> <span data-ttu-id="213ad-127">Ad hello yeni sınıf **AuthenticationTestHandler.cs**, tıklatıp **Ekle** toogenerate hello sınıfı.</span><span class="sxs-lookup"><span data-stu-id="213ad-127">Name hello new class **AuthenticationTestHandler.cs**, and click **Add** toogenerate hello class.</span></span> <span data-ttu-id="213ad-128">Bu sınıfı kullanarak kullanılan tooauthenticate kullanıcıların olacaktır *temel kimlik doğrulaması* basitleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="213ad-128">This class will be used tooauthenticate users using *Basic Authentication* for simplicity.</span></span> <span data-ttu-id="213ad-129">Uygulamanız herhangi bir kimlik doğrulama şemasını kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="213ad-129">Note that your app can use any authentication scheme.</span></span>
2. <span data-ttu-id="213ad-130">AuthenticationTestHandler.cs içinde hello aşağıdakileri ekleyin `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="213ad-130">In AuthenticationTestHandler.cs, add hello following `using` statements:</span></span>
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. <span data-ttu-id="213ad-131">Merhaba değiştirme AuthenticationTestHandler.cs içinde `AuthenticationTestHandler` sınıf tanımının koddan hello ile.</span><span class="sxs-lookup"><span data-stu-id="213ad-131">In AuthenticationTestHandler.cs, replacing hello `AuthenticationTestHandler` class definition with hello following code.</span></span> 
   
    <span data-ttu-id="213ad-132">Aşağıdaki üç koşul hello tümü doğru olduğunda bu işleyici hello isteği yetkilendirin.</span><span class="sxs-lookup"><span data-stu-id="213ad-132">This handler will authorize hello request when hello following three conditions are all true:</span></span>
   
   * <span data-ttu-id="213ad-133">Merhaba isteği dahil bir *yetkilendirme* üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="213ad-133">hello request included an *Authorization* header.</span></span> 
   * <span data-ttu-id="213ad-134">Merhaba isteği kullanır *temel* kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="213ad-134">hello request uses *basic* authentication.</span></span> 
   * <span data-ttu-id="213ad-135">Merhaba kullanıcı adı dizesi ve hello parola dizesi olan hello aynı dize.</span><span class="sxs-lookup"><span data-stu-id="213ad-135">hello user name string and hello password string are hello same string.</span></span>
     
     <span data-ttu-id="213ad-136">Aksi takdirde hello isteği reddedilir.</span><span class="sxs-lookup"><span data-stu-id="213ad-136">Otherwise, hello request will be rejected.</span></span> <span data-ttu-id="213ad-137">Bu geçerli bir kimlik doğrulama ve yetkilendirme yaklaşımı değildir.</span><span class="sxs-lookup"><span data-stu-id="213ad-137">This is not a true authentication and authorization approach.</span></span> <span data-ttu-id="213ad-138">Yalnızca bu öğreticiye yönelik çok basit bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="213ad-138">It is just a very simple example for this tutorial.</span></span>
     
     <span data-ttu-id="213ad-139">Merhaba istek iletisi kimliği doğrulanmış ve hello tarafından yetkili varsa `AuthenticationTestHandler`, sonra hello temel kimlik doğrulaması kullanıcı hello geçerli istekte ekli toohello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span><span class="sxs-lookup"><span data-stu-id="213ad-139">If hello request message is authenticated and authorized by hello `AuthenticationTestHandler`, then hello basic authentication user will be attached toohello current request on hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span></span> <span data-ttu-id="213ad-140">Kullanıcı bilgilerini hello HttpContext başka bir denetleyici (RegisterController) tarafından kullanılacak sonraki tooadd bir [etiketi](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello bildirimi kayıt isteği.</span><span class="sxs-lookup"><span data-stu-id="213ad-140">User information in hello HttpContext will be used by another controller (RegisterController) later tooadd a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello notification registration request.</span></span>
     
       <span data-ttu-id="213ad-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span><span class="sxs-lookup"><span data-stu-id="213ad-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span></span>
     
               if (authorizationHeader != null && authorizationHeader
                   .StartsWith("Basic ", StringComparison.InvariantCultureIgnoreCase))
               {
                   string authorizationUserAndPwdBase64 =
                       authorizationHeader.Substring("Basic ".Length);
                   string authorizationUserAndPwd = Encoding.Default
                       .GetString(Convert.FromBase64String(authorizationUserAndPwdBase64));
                   string user = authorizationUserAndPwd.Split(':')[0];
                   string password = authorizationUserAndPwd.Split(':')[1];
     
                   if (verifyUserAndPwd(user, password))
                   {
                       // Attach hello new principal object toohello current HttpContext object
                       HttpContext.Current.User =
                           new GenericPrincipal(new GenericIdentity(user), new string[0]);
                       System.Threading.Thread.CurrentPrincipal =
                           System.Web.HttpContext.Current.User;
                   }
                   else return Unauthorized();
               }
               else return Unauthorized();
     
               return base.SendAsync(request, cancellationToken);
           }
     
           private bool verifyUserAndPwd(string user, string password)
           {
               // This is not a real authentication scheme.
               return user == password;
           }
     
           private Task<HttpResponseMessage> Unauthorized()
           {
               var response = new HttpResponseMessage(HttpStatusCode.Forbidden);
               var tsc = new TaskCompletionSource<HttpResponseMessage>();
               tsc.SetResult(response);
               return tsc.Task;
           }
       <span data-ttu-id="213ad-142">}</span><span class="sxs-lookup"><span data-stu-id="213ad-142">}</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="213ad-143">**Güvenlik Notu**: Merhaba `AuthenticationTestHandler` sınıfı doğru kimlik doğrulaması sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="213ad-143">**Security Note**: hello `AuthenticationTestHandler` class does not provide true authentication.</span></span> <span data-ttu-id="213ad-144">Kullanılan yalnızca toomimic temel kimlik doğrulaması ve güvenli değildir.</span><span class="sxs-lookup"><span data-stu-id="213ad-144">It is used only toomimic basic authentication and is not secure.</span></span> <span data-ttu-id="213ad-145">Üretim uygulamalarınızda ve hizmetlerinizde güvenli bir kimlik doğrulama mekanizması uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="213ad-145">You must implement a secure authentication mechanism in your production applications and services.</span></span>                
     > 
     > 
4. <span data-ttu-id="213ad-146">Merhaba hello sonunda koddan hello eklemek `Register` hello yönteminde **App_Start/WebApiConfig.cs** tooregister hello ileti işleyicisi sınıfı:</span><span class="sxs-lookup"><span data-stu-id="213ad-146">Add hello following code at hello end of hello `Register` method in hello **App_Start/WebApiConfig.cs** class tooregister hello message handler:</span></span>
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. <span data-ttu-id="213ad-147">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="213ad-147">Save your changes.</span></span>

## <a name="registering-for-notifications-using-hello-webapi-backend"></a><span data-ttu-id="213ad-148">Merhaba Webapı arka uç kullanarak bildirimleri için kaydediliyor</span><span class="sxs-lookup"><span data-stu-id="213ad-148">Registering for Notifications using hello WebAPI Backend</span></span>
<span data-ttu-id="213ad-149">Bu bölümde, yeni bir denetleyici toohello Webapı arka uç toohandle tooregister bir kullanıcı ve cihaz bildirimlerinin bildirim hub'ları için hello istemci kitaplığı kullanılarak istekleri ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="213ad-149">In this section, we will add a new controller toohello WebAPI backend toohandle requests tooregister a user and device for notifications using hello client library for notification hubs.</span></span> <span data-ttu-id="213ad-150">Merhaba denetleyicisi doğrulandı ve toohello HttpContext hello tarafından eklenen hello kullanıcı için bir kullanıcı etiketi eklemek `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="213ad-150">hello controller will add a user tag for hello user that was authenticated and attached toohello HttpContext by hello `AuthenticationTestHandler`.</span></span> <span data-ttu-id="213ad-151">Merhaba etiketi hello dize biçiminde olacaktır `"username:<actual username>"`.</span><span class="sxs-lookup"><span data-stu-id="213ad-151">hello tag will have hello string format, `"username:<actual username>"`.</span></span>

1. <span data-ttu-id="213ad-152">Çözüm Gezgini'nde hello sağ **AppBackend** proje ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="213ad-152">In Solution Explorer, right-click hello **AppBackend** project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="213ad-153">Merhaba sol taraftaki tıklatın **çevrimiçi**, arayın ve **Microsoft.Azure.NotificationHubs** hello içinde **arama** kutusu.</span><span class="sxs-lookup"><span data-stu-id="213ad-153">On hello left-hand side, click **Online**, and search for **Microsoft.Azure.NotificationHubs** in hello **Search** box.</span></span>
3. <span data-ttu-id="213ad-154">Merhaba sonuçlar listesinde tıklayın **Microsoft Azure bildirim hub'ları**ve ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="213ad-154">In hello results list, click **Microsoft Azure Notification Hubs**, and then click **Install**.</span></span> <span data-ttu-id="213ad-155">Merhaba yüklemeyi tamamlamak ve sonra hello NuGet Paket Yöneticisi penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="213ad-155">Complete hello installation, then close hello NuGet package manager window.</span></span>
   
    <span data-ttu-id="213ad-156">Bu başvuru toohello Azure Notification Hubs SDK'sı ekler hello kullanarak <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet paketini</a>.</span><span class="sxs-lookup"><span data-stu-id="213ad-156">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="213ad-157">Bildirim hub'ı kullanılan toosend bildirimleri ile Merhaba bağlantısını temsil eden yeni bir sınıf dosyası artık oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="213ad-157">We will now create a new class file that represents hello connection with notification hub used toosend notifications.</span></span> <span data-ttu-id="213ad-158">Hello Hello Çözüm Gezgini, sağ tıklatın **modelleri** klasörü, tıklatın **Ekle**, ardından **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="213ad-158">In hello Solution Explorer, right-click hello **Models** folder, click **Add**, then click **Class**.</span></span> <span data-ttu-id="213ad-159">Ad hello yeni sınıf **Notifications.cs**, ardından **Ekle** toogenerate hello sınıfı.</span><span class="sxs-lookup"><span data-stu-id="213ad-159">Name hello new class **Notifications.cs**, then click **Add** toogenerate hello class.</span></span> 
   
    ![][B6]
5. <span data-ttu-id="213ad-160">Notifications.cs içinde hello aşağıdakileri ekleyin `using` deyimi hello dosyanın üst kısmındaki hello:</span><span class="sxs-lookup"><span data-stu-id="213ad-160">In Notifications.cs, add hello following `using` statement at hello top of hello file:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
6. <span data-ttu-id="213ad-161">Hello yerine `Notifications` sınıf hello aşağıdaki tanımıyla ve hello bağlantı dizesi (tam erişim) bildirim hub'ınız için emin tooreplace hello iki yer tutucularını yapıp hello hub adını (adresinde [Klasik Azure portalı ](http://manage.windowsazure.com)):</span><span class="sxs-lookup"><span data-stu-id="213ad-161">Replace hello `Notifications` class definition with hello following and make sure tooreplace hello two placeholders with hello connection string (with full access) for your notification hub, and hello hub name (available at [Azure Classic Portal](http://manage.windowsazure.com)):</span></span>
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. <span data-ttu-id="213ad-162">Bundan sonra **RegisterController** adlı yeni bir denetleyici oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="213ad-162">Next we will create a new controller named **RegisterController**.</span></span> <span data-ttu-id="213ad-163">Hello Çözüm Gezgini'nde sağ **denetleyicileri** klasörü, ardından **Ekle**, ardından **denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="213ad-163">In Solution Explorer, right-click hello **Controllers** folder, then click **Add**, then click **Controller**.</span></span> <span data-ttu-id="213ad-164">Merhaba tıklatın **Web API 2 denetleyicisi--boş** öğesini ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="213ad-164">Click hello **Web API 2 Controller -- Empty** item, and then click **Add**.</span></span> <span data-ttu-id="213ad-165">Ad hello yeni sınıf **RegisterController**ve ardından **Ekle** yeniden toogenerate hello denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="213ad-165">Name hello new class **RegisterController**, and then click **Add** again toogenerate hello controller.</span></span>
   
    ![][B7]
   
    ![][B8]
8. <span data-ttu-id="213ad-166">RegisterController.cs içinde hello aşağıdakileri ekleyin `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="213ad-166">In RegisterController.cs, add hello following `using` statements:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. <span data-ttu-id="213ad-167">Merhaba içindeki kodu aşağıdaki hello eklemek `RegisterController` sınıf tanımının.</span><span class="sxs-lookup"><span data-stu-id="213ad-167">Add hello following code inside hello `RegisterController` class definition.</span></span> <span data-ttu-id="213ad-168">Bu kodda unutmayın, biz bu hello kullanıcı için bir kullanıcı etiket toohello HttpContext bağlı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="213ad-168">Note that in this code, we add a user tag for hello user this is attached toohello HttpContext.</span></span> <span data-ttu-id="213ad-169">Merhaba kullanıcı doğrulandı ve toohello HttpContext eklediğimiz, hello İleti Filtresi tarafından bağlı `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="213ad-169">hello user was authenticated and attached toohello HttpContext by hello message filter we added, `AuthenticationTestHandler`.</span></span> <span data-ttu-id="213ad-170">Kullanıcı hello isteğe bağlı denetimleri tooverify haklarına sahip de ekleyebilirsiniz tooregister hello için istenen etiketler.</span><span class="sxs-lookup"><span data-stu-id="213ad-170">You can also add optional checks tooverify that hello user has rights tooregister for hello requested tags.</span></span>
   
        private NotificationHubClient hub;
   
        public RegisterController()
        {
            hub = Notifications.Instance.Hub;
        }
   
        public class DeviceRegistration
        {
            public string Platform { get; set; }
            public string Handle { get; set; }
            public string[] Tags { get; set; }
        }
   
        // POST api/register
        // This creates a registration id
        public async Task<string> Post(string handle = null)
        {
            string newRegistrationId = null;
   
            // make sure there are no existing registrations for this push handle (used for iOS and Android)
            if (handle != null)
            {
                var registrations = await hub.GetRegistrationsByChannelAsync(handle, 100);
   
                foreach (RegistrationDescription registration in registrations)
                {
                    if (newRegistrationId == null)
                    {
                        newRegistrationId = registration.RegistrationId;
                    }
                    else
                    {
                        await hub.DeleteRegistrationAsync(registration);
                    }
                }
            }
   
            if (newRegistrationId == null) 
                newRegistrationId = await hub.CreateRegistrationIdAsync();
   
            return newRegistrationId;
        }
   
        // PUT api/register/5
        // This creates or updates a registration (with provided channelURI) at hello specified id
        public async Task<HttpResponseMessage> Put(string id, DeviceRegistration deviceUpdate)
        {
            RegistrationDescription registration = null;
            switch (deviceUpdate.Platform)
            {
                case "mpns":
                    registration = new MpnsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "wns":
                    registration = new WindowsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "apns":
                    registration = new AppleRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "gcm":
                    registration = new GcmRegistrationDescription(deviceUpdate.Handle);
                    break;
                default:
                    throw new HttpResponseException(HttpStatusCode.BadRequest);
            }
   
            registration.RegistrationId = id;
            var username = HttpContext.Current.User.Identity.Name;
   
            // add check if user is allowed tooadd these tags
            registration.Tags = new HashSet<string>(deviceUpdate.Tags);
            registration.Tags.Add("username:" + username);
   
            try
            {
                await hub.CreateOrUpdateRegistrationAsync(registration);
            }
            catch (MessagingException e)
            {
                ReturnGoneIfHubResponseIsGone(e);
            }
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        // DELETE api/register/5
        public async Task<HttpResponseMessage> Delete(string id)
        {
            await hub.DeleteRegistrationAsync(id);
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        private static void ReturnGoneIfHubResponseIsGone(MessagingException e)
        {
            var webex = e.InnerException as WebException;
            if (webex.Status == WebExceptionStatus.ProtocolError)
            {
                var response = (HttpWebResponse)webex.Response;
                if (response.StatusCode == HttpStatusCode.Gone)
                    throw new HttpRequestException(HttpStatusCode.Gone.ToString());
            }
        }
10. <span data-ttu-id="213ad-171">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="213ad-171">Save your changes.</span></span>

## <a name="sending-notifications-from-hello-webapi-backend"></a><span data-ttu-id="213ad-172">Merhaba Webapı arka uç gönderen bildirimleri</span><span class="sxs-lookup"><span data-stu-id="213ad-172">Sending Notifications from hello WebAPI Backend</span></span>
<span data-ttu-id="213ad-173">Bu bölümde istemci cihazları toosend hello ASP.NET Webapı arka uç Azure bildirim hub'ları Hizmet Yönetimi Kitaplığı kullanarak hello kullanıcı adı etiketi dayalı bir bildirim için bir yol sunan yeni bir denetleyici ekleyin.</span><span class="sxs-lookup"><span data-stu-id="213ad-173">In this section you add a new controller that exposes a way for client devices toosend a notification based on hello username tag using Azure Notification Hubs Service Management Library in hello ASP.NET WebAPI backend.</span></span>

1. <span data-ttu-id="213ad-174">**NotificationsController** adlı başka bir yeni denetleyici oluşturun.</span><span class="sxs-lookup"><span data-stu-id="213ad-174">Create another new controller named **NotificationsController**.</span></span> <span data-ttu-id="213ad-175">Merhaba oluşturmak hello oluşturduğunuz aynı şekilde **RegisterController** hello önceki bölümdeki.</span><span class="sxs-lookup"><span data-stu-id="213ad-175">Create it hello same way you created hello **RegisterController** in hello previous section.</span></span>
2. <span data-ttu-id="213ad-176">NotificationsController.cs içinde hello aşağıdakileri ekleyin `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="213ad-176">In NotificationsController.cs, add hello following `using` statements:</span></span>
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. <span data-ttu-id="213ad-177">Yöntem toohello aşağıdaki hello eklemek **NotificationsController** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="213ad-177">Add hello following method toohello **NotificationsController** class.</span></span>
   
    <span data-ttu-id="213ad-178">Bu kod Gönder hello Platform bildirim hizmeti (PNS) üzerinde göre bir bildirim türü `pns` parametresi.</span><span class="sxs-lookup"><span data-stu-id="213ad-178">This code send a notification type based on hello Platform Notification Service (PNS) `pns` parameter.</span></span> <span data-ttu-id="213ad-179">Merhaba değerini `to_tag` kullanılan tooset hello olan *kullanıcıadı* hello ileti etiketi.</span><span class="sxs-lookup"><span data-stu-id="213ad-179">hello value of `to_tag` is used tooset hello *username* tag on hello message.</span></span> <span data-ttu-id="213ad-180">Bu etiket, etkin bir bildirim hub'ı kaydının kullanıcı etiketi ile eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="213ad-180">This tag must match a username tag of an active notification hub registration.</span></span> <span data-ttu-id="213ad-181">Merhaba bildirim iletisi hello hello POST isteği gövdesinden çekilen ve hello hedef PNS biçimlendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="213ad-181">hello notification message is pulled from hello body of hello POST request and formatted for hello target PNS.</span></span> 
   
    <span data-ttu-id="213ad-182">Merhaba, desteklenen aygıtların tooreceive bildirimleri kullanmayı Platform bildirim hizmeti (PNS) bağlı olarak farklı bildirimleri farklı biçimlerini kullanarak desteklenir.</span><span class="sxs-lookup"><span data-stu-id="213ad-182">Depending on hello Platform Notification Service (PNS) that your supported devices use tooreceive notifications, different notifications are supported using different formats.</span></span> <span data-ttu-id="213ad-183">Örneğin, Windows cihazlarında başka bir PNS tarafından doğrudan desteklenmeyen bir [WNS ile bildirim](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="213ad-183">For example on Windows devices, you could use a [toast notification with WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) that isn't directly supported by another PNS.</span></span> <span data-ttu-id="213ad-184">Arka PNS cihazların Merhaba için desteklenen bir bildirim içine tooformat hello bildirim gerekir böylece toosupport planlayın.</span><span class="sxs-lookup"><span data-stu-id="213ad-184">So your backend would need tooformat hello notification into a supported notification for hello PNS of devices you plan toosupport.</span></span> <span data-ttu-id="213ad-185">Ardından üzerinde hello hello uygun gönderme API kullanan [NotificationHubClient sınıfı](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span><span class="sxs-lookup"><span data-stu-id="213ad-185">Then use hello appropriate send API on hello [NotificationHubClient class](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span></span>
   
        public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag)
        {
            var user = HttpContext.Current.User.Identity.Name;
            string[] userTag = new string[2];
            userTag[0] = "username:" + to_tag;
            userTag[1] = "from:" + user;
   
            Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;
            HttpStatusCode ret = HttpStatusCode.InternalServerError;
   
            switch (pns.ToLower())
            {
                case "wns":
                    // Windows 8.1 / Windows Phone 8.1
                    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" + 
                                "From " + user + ": " + message + "</text></binding></visual></toast>";
                    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
                    break;
                case "apns":
                    // iOS
                    var alert = "{\"aps\":{\"alert\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(alert, userTag);
                    break;
                case "gcm":
                    // Android
                    var notif = "{ \"data\" : {\"message\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendGcmNativeNotificationAsync(notif, userTag);
                    break;
            }
   
            if (outcome != null)
            {
                if (!((outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Abandoned) ||
                    (outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Unknown)))
                {
                    ret = HttpStatusCode.OK;
                }
            }
   
            return Request.CreateResponse(ret);
        }
4. <span data-ttu-id="213ad-186">Tuşuna **F5** toorun hello uygulama ve tooensure hello çalışmanızın doğruluğunu kadarki.</span><span class="sxs-lookup"><span data-stu-id="213ad-186">Press **F5** toorun hello application and tooensure hello accuracy of your work so far.</span></span> <span data-ttu-id="213ad-187">Hello uygulama, bir web tarayıcısı başlatmak ve hello ASP.NET giriş sayfasını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="213ad-187">hello app should launch a web browser and display hello ASP.NET home page.</span></span> 

## <a name="publish-hello-new-webapi-backend"></a><span data-ttu-id="213ad-188">Yayımlama hello yeni Webapı arka uç</span><span class="sxs-lookup"><span data-stu-id="213ad-188">Publish hello new WebAPI Backend</span></span>
1. <span data-ttu-id="213ad-189">Biz sipariş toomake bu uygulama tooan Azure Web sitesi dağıtacağınız şimdi onu tüm cihazlardan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="213ad-189">Now we will deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="213ad-190">Merhaba üzerinde sağ **AppBackend** proje ve seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="213ad-190">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="213ad-191">Yayımlama hedefi olarak **Microsoft Azure Uygulama Hizmeti**’ni seçip **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="213ad-191">Select **Microsoft Azure App Service** as your publish target and click **Publish**.</span></span> <span data-ttu-id="213ad-192">Bu, Azure'da tüm hello gerekli Azure kaynaklarını toorun hello ASP.NET web uygulaması oluşturmanıza yardımcı olacak hello App Service Oluştur iletişim kutusunu açar.</span><span class="sxs-lookup"><span data-stu-id="213ad-192">This opens hello Create App Service dialog, which helps you create all hello necessary Azure resources toorun hello ASP.NET web app in Azure.</span></span>

    ![][B15]
3. <span data-ttu-id="213ad-193">Merhaba, **App Service Oluştur** iletişim kutusunda, Azure hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="213ad-193">In hello **Create App Service** dialog, select your Azure account.</span></span> <span data-ttu-id="213ad-194">**Tür Değiştir**’e tıklayıp **Web Uygulaması**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="213ad-194">Click **Change Type** and select **Web App**.</span></span> <span data-ttu-id="213ad-195">Merhaba tutmak **Web uygulaması adı** seçin ve verilen hello **abonelik**, **kaynak grubu**, ve **App Service planı**.</span><span class="sxs-lookup"><span data-stu-id="213ad-195">Keep hello **Web App Name** given and select hello **Subscription**, **Resource Group**, and **App Service Plan**.</span></span>  <span data-ttu-id="213ad-196">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="213ad-196">Click **Create**.</span></span>

4. <span data-ttu-id="213ad-197">Merhaba Not **Site URL'si** hello özelliğinde **Özet** bölümü.</span><span class="sxs-lookup"><span data-stu-id="213ad-197">Make a note of hello **Site URL** property in hello **Summary** section.</span></span> <span data-ttu-id="213ad-198">Toothis URL'si olarak başvuruda bulunacak, *arka uç nokta* Bu öğreticide daha sonra.</span><span class="sxs-lookup"><span data-stu-id="213ad-198">We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="213ad-199">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="213ad-199">Click **Publish**.</span></span>

5. <span data-ttu-id="213ad-200">Merhaba Sihirbaz tamamlandıktan sonra hello ASP.NET web uygulaması tooAzure yayımlar ve ardından başlatır hello varsayılan tarayıcıda uygulama hello.</span><span class="sxs-lookup"><span data-stu-id="213ad-200">Once hello wizard completes, it publishes hello ASP.NET web app tooAzure, and then launches hello app in hello default browser.</span></span>  <span data-ttu-id="213ad-201">Uygulamanız Azure Uygulama Hizmetileri’nde görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="213ad-201">Your application will be viewable in Azure App Services.</span></span>

<span data-ttu-id="213ad-202">Merhaba URL hello biçimi http://<app_name>.azurewebsites.net ile daha önce belirtilen başlangıç web uygulaması adı kullanır.</span><span class="sxs-lookup"><span data-stu-id="213ad-202">hello URL uses hello web app name that you specified earlier, with hello format http://<app_name>.azurewebsites.net.</span></span>

[B1]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push1.png
[B2]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push2.png
[B3]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push3.png
[B4]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push4.png
[B5]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push5.png
[B6]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push6.png
[B7]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push7.png
[B8]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push8.png
[B14]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push14.png
[B15]: ./media/notification-hubs-aspnet-backend-notifyusers/publish-to-app-service.png
[B16]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users16.PNG
[B18]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users18.PNG
