
1. <span data-ttu-id="1b846-101">Merhaba tıklatın **uygulama hizmetleri** düğmesi, Mobile Apps arka ucunuz seçin, **Hızlı Başlangıç**ve ardından, istemci Platformu (iOS, Android, Xamarin, Cordova) seçin.</span><span class="sxs-lookup"><span data-stu-id="1b846-101">Click hello **App Services** button, select your Mobile Apps back end, select **Quickstart**, and then select your client platform (iOS, Android, Xamarin, Cordova).</span></span>

    ![Mobile Apps Hızlı Başlangıcın vurgulandığı Azure Portal][quickstart]

2. <span data-ttu-id="1b846-103">Bir veritabanı bağlantısı yapılandırılmamışsa, hello aşağıdakileri yaparak oluşturun:</span><span class="sxs-lookup"><span data-stu-id="1b846-103">If a database connection is not configured, create one by doing hello following:</span></span>

    ![Azure portalı ile mobil uygulamaları bağlamak toodatabase][connect]

    <span data-ttu-id="1b846-105">a.</span><span class="sxs-lookup"><span data-stu-id="1b846-105">a.</span></span> <span data-ttu-id="1b846-106">Yeni bir SQL veritabanı ve sunucusu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1b846-106">Create a new SQL database and server.</span></span>

    ![Mobile Apps ile Azure Portal, yeni veritabanı ve sunucu oluşturma][server]

    <span data-ttu-id="1b846-108">b.</span><span class="sxs-lookup"><span data-stu-id="1b846-108">b.</span></span> <span data-ttu-id="1b846-109">Merhaba veri bağlantısı başarıyla oluşturulana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="1b846-109">Wait until hello data connection is successfully created.</span></span>

    ![Veri bağlantısının başarıyla oluşturulduğunu gösteren Azure Portal bildirimi][notification]

    <span data-ttu-id="1b846-111">c.</span><span class="sxs-lookup"><span data-stu-id="1b846-111">c.</span></span> <span data-ttu-id="1b846-112">Veri bağlantısının başarılı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b846-112">Data connection must be successful.</span></span>

    ![Azure Portal bildirimi, "Bir veri bağlantınız zaten var"][already-connection]

3. <span data-ttu-id="1b846-114">**2. Tablo API'si oluştur**'un altında **Arka uç dili** olarak Node.js seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="1b846-114">Under **2. Create a table API**, select Node.js for **Backend language**.</span></span> 
 
4. <span data-ttu-id="1b846-115">Merhaba bildirimi kabul edin ve ardından **Todoıtem tablosu oluştur**.</span><span class="sxs-lookup"><span data-stu-id="1b846-115">Accept hello acknowledgment, and then select **Create TodoItem table**.</span></span>  
    <span data-ttu-id="1b846-116">Böylece veritabanınızda yeni bir yapılacaklar tablosu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1b846-116">This action creates a new to-do item table in your database.</span></span> 

    >[!IMPORTANT]
    > <span data-ttu-id="1b846-117">Var olan bir arka uç tooNode.js geçiş tüm içeriğinin üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="1b846-117">Switching an existing back end tooNode.js overwrites all contents.</span></span> <span data-ttu-id="1b846-118">Bunun yerine, bir .NET arka uç bkz toocreate [hello .NET arka uç sunucusu SDK ile Mobile Apps için iş][instructions].</span><span class="sxs-lookup"><span data-stu-id="1b846-118">toocreate a .NET back end instead, see [Work with hello .NET back-end server SDK for Mobile Apps][instructions].</span></span>

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
