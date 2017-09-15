## <a name="create-the-webapi-project"></a><span data-ttu-id="9bd4e-101">WebAPI Projesi Oluşturma</span><span class="sxs-lookup"><span data-stu-id="9bd4e-101">Create the WebAPI Project</span></span>
<span data-ttu-id="9bd4e-102">Aşağıdaki bölümlerde yeni bir ASP.NET WebAPI arka ucu oluşturulur ve bu işlemi üç temel amacı vardır:</span><span class="sxs-lookup"><span data-stu-id="9bd4e-102">A new ASP.NET WebAPI backend will be created in the sections that follow and it will have three main purposes:</span></span>

1. <span data-ttu-id="9bd4e-103">**İstemcilerin Kimliğini Doğrulama**: İstemci isteklerinin kimliğini doğrulamak ve kullanıcıyı istekle ilişkilendirmek üzere daha sonra bir ileti işleyicisi eklenir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-103">**Authenticating Clients**: A message handler will be added later to authenticate client requests and associate the user with the request.</span></span>
2. <span data-ttu-id="9bd4e-104">**İstemci Bildirimi Kayıtları**: Daha sonra, bir istemci cihazının bildirimleri alması için yeni kayıtları işlemek üzere bir denetleyici ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-104">**Client Notification Registrations**: Later, you will add a controller to handle new registrations for a client device to receive notifications.</span></span> <span data-ttu-id="9bd4e-105">Kimliği doğrulanmış kullanıcı adı, kayda bir [etiket](https://msdn.microsoft.com/library/azure/dn530749.aspx) olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-105">The authenticated user name will automatically be added to the registration as a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span></span>
3. <span data-ttu-id="9bd4e-106">**İstemcilere Bildirimleri Gönderme**: Daha sonra, kullanıcının etiketle ilişkili cihazlara ve istemcilere güvenli bir iletmeyi tetiklemesi için yeni bir yol sağlamak üzere bir denetleyici de ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-106">**Sending Notifications to Clients**: Later, you will also add a controller to provide a way for a user to trigger a secure push to devices and clients associated with the tag.</span></span> 

<span data-ttu-id="9bd4e-107">Aşağıdaki adımlar yeni ASP.NET WebAPI arka ucunun nasıl oluşturulacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="9bd4e-107">The following steps show how to create the new ASP.NET WebAPI backend:</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9bd4e-108">Visual Studio 2015 veya önceki bir sürümü kullanıyorsanız, bu öğreticiye başlamadan önce lütfen NuGet Paket Yöneticisi’nin en son sürümünü yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-108">If you are using Visual Studio 2015 or earlier, before starting this tutorial, please ensure that you have installed the latest version of the NuGet Package Manager.</span></span> <span data-ttu-id="9bd4e-109">Denetlemek için Visual Studio’yu başlatın.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-109">To check, start Visual Studio.</span></span> <span data-ttu-id="9bd4e-110">**Araçlar** menüsünde **Uzantılar ve Güncelleştirmeler**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-110">From the **Tools** menu, click **Extensions and Updates**.</span></span> <span data-ttu-id="9bd4e-111">Visual Studio sürümünüz için **NuGet Paket Yöneticisi** araması yapın ve en son sürümü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-111">Search for **NuGet Package Manager** for your version of Visual Studio, and make sure you have the latest version.</span></span> <span data-ttu-id="9bd4e-112">En son sürümü kullanmıyorsanız, NuGet Paket Yöneticisi'ni yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-112">If not, please uninstall, then reinstall the NuGet Package Manager.</span></span>
> 
> ![][B4]
> 
> [!NOTE]
> <span data-ttu-id="9bd4e-113">Web sitesi dağıtımı için Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/)’sını yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-113">Make sure you have installed the Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) for website deployment.</span></span>
> 
> 

1. <span data-ttu-id="9bd4e-114">Visual Studio veya Visual Studio Express’i başlatın.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-114">Start Visual Studio or Visual Studio Express.</span></span> <span data-ttu-id="9bd4e-115">**Sunucu Gezgini**’ne tıklayıp Azure hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-115">Click **Server Explorer** and sign in to your Azure account.</span></span> <span data-ttu-id="9bd4e-116">Visual Studio, hesabınızda web sitesi kaynakları oluşturmak için oturum açmanızı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-116">Visual Studio will need you signed in to create the web site resources on your account.</span></span>
2. <span data-ttu-id="9bd4e-117">Visual Studio’da sırasıyla **Dosya**, **Yeni** ve **Proje**’ye tıklayın, **Şablonlar**’ı ve **Visual C#**’yi genişletip **Web** ve **ASP.NET Web Uygulaması**’na tıklayın, **AppBackend** adını yazın ve ardından **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-117">In Visual Studio, click **File**, then click **New**, then **Project**, expand **Templates**, **Visual C#**, then click **Web** and **ASP.NET Web Application**, type the name **AppBackend**, and then click **OK**.</span></span> 
   
    ![][B1]
3. <span data-ttu-id="9bd4e-118">**Yeni ASP.NET Projesi** iletişim kutusunda **Web API**’sine ve ardından **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-118">In the **New ASP.NET Project** dialog, click **Web API**, then click **OK**.</span></span>
   
    ![][B2]
4. <span data-ttu-id="9bd4e-119">**Microsoft Azure Web Uygulaması** iletişim kutusunda bir aboneliği ve daha önce oluşturduğunuz **App Service planını** seçin.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-119">In the **Configure Microsoft Azure Web App** dialog, choose a subscription, and an **App Service plan** you have already created.</span></span> <span data-ttu-id="9bd4e-120">Ayrıca **Yeni bir app service planı oluştur**’u seçip iletişim kutusundan bir plan oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-120">You can also choose **Create a new app service plan** and create one from the dialog.</span></span> <span data-ttu-id="9bd4e-121">Bu öğretici için bir veritabanı gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-121">You do not need a database for this tutorial.</span></span> <span data-ttu-id="9bd4e-122">App service planınızı seçtikten sonra projeyi oluşturmak için **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-122">Once you have selected your app service plan, click **OK** to create the project.</span></span>
   
    ![][B5]

## <a name="authenticating-clients-to-the-webapi-backend"></a><span data-ttu-id="9bd4e-123">WebAPI Arka Ucunda İstemcilerin Kimliğini Doğrulama</span><span class="sxs-lookup"><span data-stu-id="9bd4e-123">Authenticating Clients to the WebAPI Backend</span></span>
<span data-ttu-id="9bd4e-124">Bu bölümde, yeni arka uç için **AuthenticationTestHandler** adlı yeni bir ileti işleyicisi oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-124">In this section, you will create a new message handler class named **AuthenticationTestHandler** for the new backend.</span></span> <span data-ttu-id="9bd4e-125">Bu sınıf [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx)’dan türetilip bir ileti işleyicisi olarak eklenir, böylece arka uca gelen istekleri işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-125">This class is derived from [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) and added as a message handler so it can process all requests coming into the backend.</span></span> 

1. <span data-ttu-id="9bd4e-126">Çözüm Gezgini'nde **AppBackend** projesine sağ tıklayın, **Ekle**'ye ve ardından **Sınıf**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-126">In Solution Explorer, right-click the **AppBackend** project, click **Add**, then click **Class**.</span></span> <span data-ttu-id="9bd4e-127">Yeni **AuthenticationTestHandler.cs** sınıfını adlandırıp **Ekle**’ye tıklayarak sınıfı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-127">Name the new class **AuthenticationTestHandler.cs**, and click **Add** to generate the class.</span></span> <span data-ttu-id="9bd4e-128">Bu sınıf, kolaylık için *Temel Kimlik Doğrulaması* kullanan kullanıcıların kimliğini doğrulamak amacıyla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-128">This class will be used to authenticate users using *Basic Authentication* for simplicity.</span></span> <span data-ttu-id="9bd4e-129">Uygulamanız herhangi bir kimlik doğrulama şemasını kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-129">Note that your app can use any authentication scheme.</span></span>
2. <span data-ttu-id="9bd4e-130">AuthenticationTestHandler.cs sınıfına aşağıdaki `using` deyimlerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9bd4e-130">In AuthenticationTestHandler.cs, add the following `using` statements:</span></span>
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. <span data-ttu-id="9bd4e-131">AuthenticationTestHandler.cs sınıfında `AuthenticationTestHandler` sınıf tanımını aşağıdaki kod ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-131">In AuthenticationTestHandler.cs, replacing the `AuthenticationTestHandler` class definition with the following code.</span></span> 
   
    <span data-ttu-id="9bd4e-132">Bu işleyici aşağıdaki üç koşulun tümü geçerli olduğunda bu isteği yetkilendirir:</span><span class="sxs-lookup"><span data-stu-id="9bd4e-132">This handler will authorize the request when the following three conditions are all true:</span></span>
   
   * <span data-ttu-id="9bd4e-133">İstek bir *Yetkilendirme* üst bilgisi içerir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-133">The request included an *Authorization* header.</span></span> 
   * <span data-ttu-id="9bd4e-134">İstek *temel* kimlik doğrulaması kullanır.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-134">The request uses *basic* authentication.</span></span> 
   * <span data-ttu-id="9bd4e-135">Kullanıcı adı dizesi ve parola dizesi aynı dizelerdir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-135">The user name string and the password string are the same string.</span></span>
     
     <span data-ttu-id="9bd4e-136">Aksi takdirde istek reddedilir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-136">Otherwise, the request will be rejected.</span></span> <span data-ttu-id="9bd4e-137">Bu geçerli bir kimlik doğrulama ve yetkilendirme yaklaşımı değildir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-137">This is not a true authentication and authorization approach.</span></span> <span data-ttu-id="9bd4e-138">Yalnızca bu öğreticiye yönelik çok basit bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-138">It is just a very simple example for this tutorial.</span></span>
     
     <span data-ttu-id="9bd4e-139">İstek iletisi `AuthenticationTestHandler` tarafından yetkilendirilir ve kimlik doğrulaması yapılırsa, temel kimlik doğrulaması kullanıcısı [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx) üzerindeki geçerli isteğe eklenir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-139">If the request message is authenticated and authorized by the `AuthenticationTestHandler`, then the basic authentication user will be attached to the current request on the [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span></span> <span data-ttu-id="9bd4e-140">HttpContext içindeki kullanıcı bilgileri, bildirim kaydı isteğine bir [etiket](https://msdn.microsoft.com/library/azure/dn530749.aspx) eklemek amacıyla daha sonra başka bir denetleyici (RegisterController) tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-140">User information in the HttpContext will be used by another controller (RegisterController) later to add a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) to the notification registration request.</span></span>
     
       <span data-ttu-id="9bd4e-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span><span class="sxs-lookup"><span data-stu-id="9bd4e-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span></span>
     
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
                       // Attach the new principal object to the current HttpContext object
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
       <span data-ttu-id="9bd4e-142">}</span><span class="sxs-lookup"><span data-stu-id="9bd4e-142">}</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="9bd4e-143">**Güvenlik Notu**: `AuthenticationTestHandler` sınıfı gerçek kimlik doğrulaması sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-143">**Security Note**: The `AuthenticationTestHandler` class does not provide true authentication.</span></span> <span data-ttu-id="9bd4e-144">Yalnızca temel kimlik doğrulamasını taklit etmek için kullanılır ve güvenli değildir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-144">It is used only to mimic basic authentication and is not secure.</span></span> <span data-ttu-id="9bd4e-145">Üretim uygulamalarınızda ve hizmetlerinizde güvenli bir kimlik doğrulama mekanizması uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-145">You must implement a secure authentication mechanism in your production applications and services.</span></span>                
     > 
     > 
4. <span data-ttu-id="9bd4e-146">İleti işleyicisini kaydetmek için **App_Start/WebApiConfig.cs** sınıfındaki `Register` yönteminin sonuna aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9bd4e-146">Add the following code at the end of the `Register` method in the **App_Start/WebApiConfig.cs** class to register the message handler:</span></span>
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. <span data-ttu-id="9bd4e-147">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-147">Save your changes.</span></span>

## <a name="registering-for-notifications-using-the-webapi-backend"></a><span data-ttu-id="9bd4e-148">WebAPI Arka Ucunu Kullanarak Bildirimlere Kaydolma</span><span class="sxs-lookup"><span data-stu-id="9bd4e-148">Registering for Notifications using the WebAPI Backend</span></span>
<span data-ttu-id="9bd4e-149">Bu bölümde, bildirim hub’ları için istemci kitaplığını kullanarak WebAPI arka ucuna bir kullanıcı ve cihazı bildirimlere kaydetme isteklerini işlemek üzere yeni bir denetleyici ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-149">In this section, we will add a new controller to the WebAPI backend to handle requests to register a user and device for notifications using the client library for notification hubs.</span></span> <span data-ttu-id="9bd4e-150">Denetleyici, kimliği doğrulanmış ve `AuthenticationTestHandler` tarafından HttpContext’e eklenmiş kullanıcı için bir kullanıcı etiketi ekler.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-150">The controller will add a user tag for the user that was authenticated and attached to the HttpContext by the `AuthenticationTestHandler`.</span></span> <span data-ttu-id="9bd4e-151">Etiket `"username:<actual username>"` dize biçiminde olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-151">The tag will have the string format, `"username:<actual username>"`.</span></span>

1. <span data-ttu-id="9bd4e-152">Çözüm Gezgini'nde, **AppBackend** projesine sağ tıklayın ve ardından **NuGet Paketlerini Yönet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-152">In Solution Explorer, right-click the **AppBackend** project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="9bd4e-153">Sol taraftaki **Çevrimiçi** öğesine tıklayıp, **Ara** kutusunda **Microsoft.Azure.NotificationHubs** araması yapın.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-153">On the left-hand side, click **Online**, and search for **Microsoft.Azure.NotificationHubs** in the **Search** box.</span></span>
3. <span data-ttu-id="9bd4e-154">Sonuç listesinde **Microsoft Azure Notification Hubs**’a ve ardından **Yükle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-154">In the results list, click **Microsoft Azure Notification Hubs**, and then click **Install**.</span></span> <span data-ttu-id="9bd4e-155">Yüklemeyi tamamlayın ve sonra NuGet paket yöneticisi penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-155">Complete the installation, then close the NuGet package manager window.</span></span>
   
    <span data-ttu-id="9bd4e-156">Bu, <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet paketini</a> kullanarak Azure Notification Hubs SDK'sına bir başvuru ekler.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-156">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="9bd4e-157">Bildirimleri göndermek için bildirim hub'ı kullanarak bağlantıyı temsil eden yeni bir sınıf dosyası oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-157">We will now create a new class file that represents the connection with notification hub used to send notifications.</span></span> <span data-ttu-id="9bd4e-158">Çözüm Gezgini'nde **Modeller** klasörüne sağ tıklayın, **Ekle**'ye ve ardından **Sınıf**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-158">In the Solution Explorer, right-click the **Models** folder, click **Add**, then click **Class**.</span></span> <span data-ttu-id="9bd4e-159">Yeni sınıfı **Notifications.cs** olarak adlandırın, ardından **Ekle**’ye tıklayarak sınıfı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-159">Name the new class **Notifications.cs**, then click **Add** to generate the class.</span></span> 
   
    ![][B6]
5. <span data-ttu-id="9bd4e-160">Notifications.cs sınıfında aşağıdaki `using` deyimini dosyanın üst kısmına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9bd4e-160">In Notifications.cs, add the following `using` statement at the top of the file:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
6. <span data-ttu-id="9bd4e-161">`Notifications` sınıf tanımını aşağıdakiyle değiştirin ve iki yer tutucuyu bildirim hub’ınızın bağlantı dizesi ile (tam erişimli) değiştirdiğinizden emin olun ([Klasik Azure Portalında bulunabilir](http://manage.windowsazure.com)):</span><span class="sxs-lookup"><span data-stu-id="9bd4e-161">Replace the `Notifications` class definition with the following and make sure to replace the two placeholders with the connection string (with full access) for your notification hub, and the hub name (available at [Azure Classic Portal](http://manage.windowsazure.com)):</span></span>
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. <span data-ttu-id="9bd4e-162">Bundan sonra **RegisterController** adlı yeni bir denetleyici oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-162">Next we will create a new controller named **RegisterController**.</span></span> <span data-ttu-id="9bd4e-163">Çözüm Gezgini'nde **Denetleyiciler** klasörüne sağ tıklayın, **Ekle**'ye ve ardından **Denetleyici**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-163">In Solution Explorer, right-click the **Controllers** folder, then click **Add**, then click **Controller**.</span></span> <span data-ttu-id="9bd4e-164">**Web API 2 Denetleyicisi -- Boş** öğesine ve ardından **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-164">Click the **Web API 2 Controller -- Empty** item, and then click **Add**.</span></span> <span data-ttu-id="9bd4e-165">Yeni sınıfı **RegisterController** olarak adlandırın ve ardından **Ekle**’ye tekrar tıklayarak denetleyiciyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-165">Name the new class **RegisterController**, and then click **Add** again to generate the controller.</span></span>
   
    ![][B7]
   
    ![][B8]
8. <span data-ttu-id="9bd4e-166">RegisterController.cs sınıfına aşağıdaki `using` deyimlerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9bd4e-166">In RegisterController.cs, add the following `using` statements:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. <span data-ttu-id="9bd4e-167">Aşağıdaki kodu `RegisterController` sınıf tanımına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-167">Add the following code inside the `RegisterController` class definition.</span></span> <span data-ttu-id="9bd4e-168">Bu kodda, kodun HttpContext’e eklendiği kullanıcı için bir kullanıcı etiketi ekleriz.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-168">Note that in this code, we add a user tag for the user this is attached to the HttpContext.</span></span> <span data-ttu-id="9bd4e-169">Kullanıcının kimliği doğrulanmış ve eklediğimiz `AuthenticationTestHandler` mesaj filtresi ile HttpContext’e eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-169">The user was authenticated and attached to the HttpContext by the message filter we added, `AuthenticationTestHandler`.</span></span> <span data-ttu-id="9bd4e-170">Ayrıca, kullanıcının istenen etiketlere kaydolma haklarının olduğunu doğrulamak için isteğe bağlı denetimler ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-170">You can also add optional checks to verify that the user has rights to register for the requested tags.</span></span>
   
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
        // This creates or updates a registration (with provided channelURI) at the specified id
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
   
            // add check if user is allowed to add these tags
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
10. <span data-ttu-id="9bd4e-171">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-171">Save your changes.</span></span>

## <a name="sending-notifications-from-the-webapi-backend"></a><span data-ttu-id="9bd4e-172">WebAPI Arka Ucundan Bildirim Gönderme</span><span class="sxs-lookup"><span data-stu-id="9bd4e-172">Sending Notifications from the WebAPI Backend</span></span>
<span data-ttu-id="9bd4e-173">Bu bölümde, istemci cihazlarının, ASP.NET WebAPI arka ucundaki Azure Notification Hubs Hizmet Yönetimi Kitaplığı’nı kullanarak kullanıcı adı etiketini temel alan bir bildirim göndermesini sağlayan yeni bir denetleyici ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-173">In this section you add a new controller that exposes a way for client devices to send a notification based on the username tag using Azure Notification Hubs Service Management Library in the ASP.NET WebAPI backend.</span></span>

1. <span data-ttu-id="9bd4e-174">**NotificationsController** adlı başka bir yeni denetleyici oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-174">Create another new controller named **NotificationsController**.</span></span> <span data-ttu-id="9bd4e-175">Bu denetleyici de önceki bölümde oluşturduğunuz **RegisterController** ile aynı şekilde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-175">Create it the same way you created the **RegisterController** in the previous section.</span></span>
2. <span data-ttu-id="9bd4e-176">NotificationsController.cs sınıfına aşağıdaki `using` deyimlerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9bd4e-176">In NotificationsController.cs, add the following `using` statements:</span></span>
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. <span data-ttu-id="9bd4e-177">Aşağıdaki yöntemi **NotificationsController** sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-177">Add the following method to the **NotificationsController** class.</span></span>
   
    <span data-ttu-id="9bd4e-178">Bu kod, Platform Bildirim Sistemi (PNS) `pns` parametresini temel alan bir bildirim türü gönderir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-178">This code send a notification type based on the Platform Notification Service (PNS) `pns` parameter.</span></span> <span data-ttu-id="9bd4e-179">`to_tag` değeri, iletideki *kullanıcı adı* etiketini ayarlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-179">The value of `to_tag` is used to set the *username* tag on the message.</span></span> <span data-ttu-id="9bd4e-180">Bu etiket, etkin bir bildirim hub'ı kaydının kullanıcı etiketi ile eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-180">This tag must match a username tag of an active notification hub registration.</span></span> <span data-ttu-id="9bd4e-181">Bildirim iletisi, POST isteğinin gövdesinden çekilir ve hedef PNS biçimlendirilir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-181">The notification message is pulled from the body of the POST request and formatted for the target PNS.</span></span> 
   
    <span data-ttu-id="9bd4e-182">Desteklenen cihazlarınızın bildirimleri almak için kullandığı Platform Bildirim Hizmeti’ne (PNS) bağlı olarak, farklı biçimleri kullanan farklı bildirimler desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-182">Depending on the Platform Notification Service (PNS) that your supported devices use to receive notifications, different notifications are supported using different formats.</span></span> <span data-ttu-id="9bd4e-183">Örneğin, Windows cihazlarında başka bir PNS tarafından doğrudan desteklenmeyen bir [WNS ile bildirim](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-183">For example on Windows devices, you could use a [toast notification with WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) that isn't directly supported by another PNS.</span></span> <span data-ttu-id="9bd4e-184">Bu nedenle arka ucunuzun, desteklemeyi planladığınız cihazların PNS’si için bildirimi desteklenen bir bildirim biçimine dönüştürmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-184">So your backend would need to format the notification into a supported notification for the PNS of devices you plan to support.</span></span> <span data-ttu-id="9bd4e-185">Bundan sonra [NotificationHubClient sınıfında](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx) uygun gönderme API’sini kullanın</span><span class="sxs-lookup"><span data-stu-id="9bd4e-185">Then use the appropriate send API on the [NotificationHubClient class](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span></span>
   
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
4. <span data-ttu-id="9bd4e-186">Uygulamayı çalıştırmak için **F5** tuşuna basın ve o ana kadar gerçekleştirdiğiniz işin doğruluğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-186">Press **F5** to run the application and to ensure the accuracy of your work so far.</span></span> <span data-ttu-id="9bd4e-187">Uygulama bir web tarayıcısı başlatmalı ve ASP.NET giriş sayfasını göstermelidir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-187">The app should launch a web browser and display the ASP.NET home page.</span></span> 

## <a name="publish-the-new-webapi-backend"></a><span data-ttu-id="9bd4e-188">Yeni WebAPI Arka Ucunu yayımlama</span><span class="sxs-lookup"><span data-stu-id="9bd4e-188">Publish the new WebAPI Backend</span></span>
1. <span data-ttu-id="9bd4e-189">Şimdi bu uygulamayı tüm cihazlardan erişilebilir olması için bir Azure Web Sitesinde yayımlayacağız.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-189">Now we will deploy this app to an Azure Website in order to make it accessible from all devices.</span></span> <span data-ttu-id="9bd4e-190">**AppBackend** projesine sağ tıklayıp **Yayımla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-190">Right-click on the **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="9bd4e-191">Yayımlama hedefi olarak **Microsoft Azure Uygulama Hizmeti**’ni seçip **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-191">Select **Microsoft Azure App Service** as your publish target and click **Publish**.</span></span> <span data-ttu-id="9bd4e-192">Bu işlem, ASP.NET web uygulamasını Azure’da çalıştırmak için gereken tüm Azure kaynaklarını oluşturmanıza yardımcı olan App Service Oluştur iletişim kutusunu açar.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-192">This opens the Create App Service dialog, which helps you create all the necessary Azure resources to run the ASP.NET web app in Azure.</span></span>

    ![][B15]
3. <span data-ttu-id="9bd4e-193">**App Service Oluştur** iletişim kutusunda Azure hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-193">In the **Create App Service** dialog, select your Azure account.</span></span> <span data-ttu-id="9bd4e-194">**Tür Değiştir**’e tıklayıp **Web Uygulaması**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-194">Click **Change Type** and select **Web App**.</span></span> <span data-ttu-id="9bd4e-195">Mevcut **Web Uygulaması Adı**’nı değiştirmeyin ve **Abonelik**, **Kaynak Grubu** ve **App Service Planı**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-195">Keep the **Web App Name** given and select the **Subscription**, **Resource Group**, and **App Service Plan**.</span></span>  <span data-ttu-id="9bd4e-196">**Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-196">Click **Create**.</span></span>

4. <span data-ttu-id="9bd4e-197">**Özet** bölümündeki **Site URL** özelliğini not edin.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-197">Make a note of the **Site URL** property in the **Summary** section.</span></span> <span data-ttu-id="9bd4e-198">Bu URL'ye bu öğreticinin sonraki bölümlerinde *arka uca ait uç nokta* olarak başvuracağız.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-198">We will refer to this URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="9bd4e-199">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-199">Click **Publish**.</span></span>

5. <span data-ttu-id="9bd4e-200">Sihirbaz tamamlandıktan sonra ASP.NET web uygulamasını Azure’da yayımlar ve ardından uygulamayı varsayılan tarayıcıda başlatır.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-200">Once the wizard completes, it publishes the ASP.NET web app to Azure, and then launches the app in the default browser.</span></span>  <span data-ttu-id="9bd4e-201">Uygulamanız Azure Uygulama Hizmetileri’nde görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-201">Your application will be viewable in Azure App Services.</span></span>

<span data-ttu-id="9bd4e-202">URL daha önce belirttiğiniz web uygulaması adını http://<uygulama_adı>.azurewebsites.net biçimiyle kullanır.</span><span class="sxs-lookup"><span data-stu-id="9bd4e-202">The URL uses the web app name that you specified earlier, with the format http://<app_name>.azurewebsites.net.</span></span>

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
