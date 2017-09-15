
1. <span data-ttu-id="0c053-101">Tıklatın **uygulama hizmetleri** düğmesi, Mobile Apps arka ucunuz seçin, **Hızlı Başlangıç**ve ardından, istemci Platformu (iOS, Android, Xamarin, Cordova) seçin.</span><span class="sxs-lookup"><span data-stu-id="0c053-101">Click the **App Services** button, select your Mobile Apps back end, select **Quickstart**, and then select your client platform (iOS, Android, Xamarin, Cordova).</span></span>

    ![Azure portal ile Mobile Apps vurgulanmış hızlı başlangıç][quickstart]

2. <span data-ttu-id="0c053-103">Bir veritabanı bağlantısı yapılandırılmamışsa, aşağıdakileri yaparak oluşturun:</span><span class="sxs-lookup"><span data-stu-id="0c053-103">If a database connection is not configured, create one by doing the following:</span></span>

    ![Azure portalına veritabanı Mobile Apps Connect ile][connect]

    <span data-ttu-id="0c053-105">a.</span><span class="sxs-lookup"><span data-stu-id="0c053-105">a.</span></span> <span data-ttu-id="0c053-106">Sunucu ve yeni SQL veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0c053-106">Create a new SQL database and server.</span></span>

    ![Mobile Apps ile Azure portalı, yeni veritabanı ve sunucu oluşturma][server]

    <span data-ttu-id="0c053-108">b.</span><span class="sxs-lookup"><span data-stu-id="0c053-108">b.</span></span> <span data-ttu-id="0c053-109">Veri bağlantısı başarıyla oluşturulana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="0c053-109">Wait until the data connection is successfully created.</span></span>

    ![Veri bağlantısı başarılı oluşturulma Azure portal bildirimi][notification]

    <span data-ttu-id="0c053-111">c.</span><span class="sxs-lookup"><span data-stu-id="0c053-111">c.</span></span> <span data-ttu-id="0c053-112">Veri bağlantısının başarılı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c053-112">Data connection must be successful.</span></span>

    !["Bir veri bağlantısı zaten" azure portal bildirimi][already-connection]

3. <span data-ttu-id="0c053-114">**2. Tablo API'si oluştur**'un altında **Arka uç dili** olarak Node.js seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="0c053-114">Under **2. Create a table API**, select Node.js for **Backend language**.</span></span> 
 
4. <span data-ttu-id="0c053-115">Bildirimi kabul edin ve ardından **Todoıtem tablosu oluştur**.</span><span class="sxs-lookup"><span data-stu-id="0c053-115">Accept the acknowledgment, and then select **Create TodoItem table**.</span></span>  
    <span data-ttu-id="0c053-116">Bu eylem, veritabanınızdaki yeni bir Yapılacaklar öğesi tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0c053-116">This action creates a new to-do item table in your database.</span></span> 

    >[!IMPORTANT]
    > <span data-ttu-id="0c053-117">Var olan bir arka uç node.js'ye geçirilmesinin tüm içeriğinin üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="0c053-117">Switching an existing back end to Node.js overwrites all contents.</span></span> <span data-ttu-id="0c053-118">Bunun yerine bir .NET arka ucu oluşturmak için bkz [mobil uygulamalar için .NET arka uç sunucusu SDK çalışma][instructions].</span><span class="sxs-lookup"><span data-stu-id="0c053-118">To create a .NET back end instead, see [Work with the .NET back-end server SDK for Mobile Apps][instructions].</span></span>

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
