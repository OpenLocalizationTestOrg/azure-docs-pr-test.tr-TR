<span data-ttu-id="2bad2-101">Yüklemek ve Windows Server çalıştıran bir sanal makinede MongoDB çalıştırmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="2bad2-101">Follow these steps to install and run MongoDB on a virtual machine running Windows Server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2bad2-102">Kimlik doğrulaması ve IP adresi bağlama gibi MongoDB güvenlik özellikleri varsayılan olarak etkin değildir.</span><span class="sxs-lookup"><span data-stu-id="2bad2-102">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="2bad2-103">Güvenlik özellikleri, MongoDB üretim ortamına dağıtmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="2bad2-103">Security features should be enabled before deploying MongoDB to a production environment.</span></span>  <span data-ttu-id="2bad2-104">Daha fazla bilgi için bkz: [güvenlik ve kimlik doğrulama](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="2bad2-104">For more information, see [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>
>
>

1. <span data-ttu-id="2bad2-105">Uzak Masaüstü kullanarak sanal makineye bağlandıktan sonra Internet Explorer'dan açmak **Başlat** sanal makine menüsünde.</span><span class="sxs-lookup"><span data-stu-id="2bad2-105">After you've connected to the virtual machine using Remote Desktop, open Internet Explorer from the **Start** menu on the virtual machine.</span></span>
2. <span data-ttu-id="2bad2-106">Seçin **Araçları** sağ üst köşesinde düğmesini.</span><span class="sxs-lookup"><span data-stu-id="2bad2-106">Select the **Tools** button in the upper right corner.</span></span>  <span data-ttu-id="2bad2-107">İçinde **Internet Seçenekleri**seçin **güvenlik** sekmesini tıklatın ve ardından **Güvenilen siteler** simgesi ve son olarak tıklayın **siteleri** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2bad2-107">In **Internet Options**, select the **Security** tab, and then select the **Trusted Sites** icon, and finally click the **Sites** button.</span></span> <span data-ttu-id="2bad2-108">Ekleme *https://\*. mongodb.org* Güvenilen siteler listesine.</span><span class="sxs-lookup"><span data-stu-id="2bad2-108">Add *https://\*.mongodb.org* to the list of trusted sites.</span></span>
3. <span data-ttu-id="2bad2-109">Git [yüklemeleri - MongoDB](https://www.mongodb.com/download-center#community).</span><span class="sxs-lookup"><span data-stu-id="2bad2-109">Go to [Downloads - MongoDB](https://www.mongodb.com/download-center#community).</span></span>
4. <span data-ttu-id="2bad2-110">Bul **geçerli durağan sürümü** , **Community Server**, en son seçin **64-bit** Windows sütununda sürümü.</span><span class="sxs-lookup"><span data-stu-id="2bad2-110">Find the **Current Stable Release** of **Community Server**, select the latest **64-bit** version in the Windows column.</span></span> <span data-ttu-id="2bad2-111">Karşıdan yükle ve MSI yükleyicisi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2bad2-111">Download, then run the MSI installer.</span></span>
5. <span data-ttu-id="2bad2-112">MongoDB genellikle C:\Program Files\MongoDB yüklenir.</span><span class="sxs-lookup"><span data-stu-id="2bad2-112">MongoDB is typically installed in C:\Program Files\MongoDB.</span></span> <span data-ttu-id="2bad2-113">Ortam değişkenleri için masaüstünde arayın ve PATH değişkenine MongoDB ikili dosyalarının yolunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2bad2-113">Search for Environment Variables on the desktop and add the MongoDB binaries path to the PATH variable.</span></span> <span data-ttu-id="2bad2-114">Örneğin, C:\Program Files\MongoDB\Server\3.4\bin ikili dosyaları makinenizde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2bad2-114">For example, you might find the binaries at C:\Program Files\MongoDB\Server\3.4\bin on your machine.</span></span>
6. <span data-ttu-id="2bad2-115">MongoDB veri ve günlük dizinleri veri disketi (sürücü gibi **F:**), önceki adımlarda oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="2bad2-115">Create MongoDB data and log directories in the data disk (such as drive **F:**) you created in the preceding steps.</span></span> <span data-ttu-id="2bad2-116">Gelen **Başlat**seçin **komut istemi** bir komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="2bad2-116">From **Start**, select **Command Prompt** to open a command prompt window.</span></span>  <span data-ttu-id="2bad2-117">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="2bad2-117">Type:</span></span>

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. <span data-ttu-id="2bad2-118">Veritabanı çalıştırmak için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2bad2-118">To run the database, run:</span></span>

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    <span data-ttu-id="2bad2-119">Tüm günlük iletilerini yönlendirilir *F:\MongoLogs\mongolog.log* dosya mongod.exe sunucu başlar ve günlük dosyalarını preallocates gibi.</span><span class="sxs-lookup"><span data-stu-id="2bad2-119">All log messages are directed to the *F:\MongoLogs\mongolog.log* file as mongod.exe server starts and preallocates journal files.</span></span> <span data-ttu-id="2bad2-120">Günlük dosyaları erişinceye ve bağlantıları dinlemeyi başlatmak MongoDB için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="2bad2-120">It may take several minutes for MongoDB to preallocate the journal files and start listening for connections.</span></span> <span data-ttu-id="2bad2-121">MongoDB örneğinizin çalışırken komut istemini bu görevde odaklanmış kalır.</span><span class="sxs-lookup"><span data-stu-id="2bad2-121">The command prompt stays focused on this task while your MongoDB instance is running.</span></span>
8. <span data-ttu-id="2bad2-122">MongoDB Yönetim Kabuğu'nu başlatmak için başka bir komut penceresinde açın **Başlat** ve aşağıdaki komutları yazın:</span><span class="sxs-lookup"><span data-stu-id="2bad2-122">To start the MongoDB administrative shell, open another command window from **Start** and type the following commands:</span></span>

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    <span data-ttu-id="2bad2-123">Veritabanı Ekle tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2bad2-123">The database is created by the insert.</span></span>
9. <span data-ttu-id="2bad2-124">Alternatif olarak, bir hizmet olarak mongod.exe yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2bad2-124">Alternatively, you can install mongod.exe as a service:</span></span>

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    <span data-ttu-id="2bad2-125">Bir hizmeti yüklendi "Mongo VT" açıklaması ile MongoDB adlı.</span><span class="sxs-lookup"><span data-stu-id="2bad2-125">A service is installed named MongoDB with a description of "Mongo DB".</span></span> <span data-ttu-id="2bad2-126">`--logpath` Seçeneği, çalışan hizmetin çıktı görüntülemek için bir komut penceresi sahip olmadığından bir günlük dosyası belirtmek için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2bad2-126">The `--logpath` option must be used to specify a log file, since the running service does not have a command window to display output.</span></span>  <span data-ttu-id="2bad2-127">`--logappend` Seçeneği, hizmet yeniden varolan günlük dosyasına eklenecek çıkışına neden belirtir.</span><span class="sxs-lookup"><span data-stu-id="2bad2-127">The `--logappend` option specifies that a restart of the service causes output to append to the existing log file.</span></span>  <span data-ttu-id="2bad2-128">`--dbpath` Seçeneği veri dizininin konumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="2bad2-128">The `--dbpath` option specifies the location of the data directory.</span></span> <span data-ttu-id="2bad2-129">Daha fazla hizmeti ile ilgili komut satırı seçenekleri için bkz [hizmeti ile ilgili komut satırı seçenekleri][MongoWindowsSvcOptions].</span><span class="sxs-lookup"><span data-stu-id="2bad2-129">For more service-related command-line options, see [Service-related command-line options][MongoWindowsSvcOptions].</span></span>

    <span data-ttu-id="2bad2-130">Hizmeti başlatmak için şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2bad2-130">To start the service, run this command:</span></span>

        C:\> net start MongoDB
10. <span data-ttu-id="2bad2-131">MongoDB yüklü ve çalışan, MongoDB için uzaktan bağlanabilmesi için bir bağlantı noktası Windows Güvenlik Duvarı'nı açmak ihtiyacınız olduğunu.</span><span class="sxs-lookup"><span data-stu-id="2bad2-131">Now that MongoDB is installed and running, you need to open a port in Windows Firewall so you can remotely connect to MongoDB.</span></span>  <span data-ttu-id="2bad2-132">Gelen **Başlat** menüsünde, select **Yönetimsel Araçlar** ve ardından **Gelişmiş Güvenlik Özellikli Windows Güvenlik Duvarı**.</span><span class="sxs-lookup"><span data-stu-id="2bad2-132">From the **Start** menu, select **Administrative Tools** and then **Windows Firewall with Advanced Security**.</span></span>
11. <span data-ttu-id="2bad2-133">bir) sol bölmede seçin **gelen kuralları**.</span><span class="sxs-lookup"><span data-stu-id="2bad2-133">a) In the left pane, select **Inbound Rules**.</span></span>  <span data-ttu-id="2bad2-134">İçinde **Eylemler** sağdaki seçin bölmesinde **yeni kural...** .</span><span class="sxs-lookup"><span data-stu-id="2bad2-134">In the **Actions** pane on the right, select **New Rule...**.</span></span>

    ![Windows Güvenlik Duvarı][Image1]

    <span data-ttu-id="2bad2-136">b) içinde **yeni gelen kuralı Sihirbazı**seçin **bağlantı noktası** ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2bad2-136">b) In the **New Inbound Rule Wizard**, select **Port** and then click **Next**.</span></span>

    ![Windows Güvenlik Duvarı][Image2]

    <span data-ttu-id="2bad2-138">c) select **TCP** ve ardından **belirli yerel bağlantı noktaları**.</span><span class="sxs-lookup"><span data-stu-id="2bad2-138">c) Select **TCP** and then **Specific local ports**.</span></span>  <span data-ttu-id="2bad2-139">' I tıklatın ve "27017" (MongoDB dinlediği varsayılan bağlantı noktası) bir bağlantı noktası belirtin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2bad2-139">Specify a port of "27017" (the default port MongoDB listens on) and click **Next**.</span></span>

    ![Windows Güvenlik Duvarı][Image3]

    <span data-ttu-id="2bad2-141">d) select **bağlantıya izin** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2bad2-141">d) Select **Allow the connection** and click **Next**.</span></span>

    ![Windows Güvenlik Duvarı][Image4]

    <span data-ttu-id="2bad2-143">e) tıklatın **sonraki** yeniden.</span><span class="sxs-lookup"><span data-stu-id="2bad2-143">e) Click **Next** again.</span></span>

    ![Windows Güvenlik Duvarı][Image5]

    <span data-ttu-id="2bad2-145">f) "MongoPort" gibi kural için bir ad belirtin ve tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="2bad2-145">f) Specify a name for the rule, such as "MongoPort", and click **Finish**.</span></span>

    ![Windows Güvenlik Duvarı][Image6]

12. <span data-ttu-id="2bad2-147">Sanal makineyi oluşturduğunuzda MongoDB için bir uç nokta yapılandırmadıysanız, bunu şimdi yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2bad2-147">If you didn't configure an endpoint for MongoDB when you created the virtual machine, you can do it now.</span></span> <span data-ttu-id="2bad2-148">Güvenlik duvarı kuralı ve uç noktası için MongoDB uzaktan bağlanabilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2bad2-148">You need both the firewall rule and the endpoint to be able to connect to MongoDB remotely.</span></span>

  <span data-ttu-id="2bad2-149">Azure portalında tıklatın **sanal makineleri (Klasik)**, yeni bir sanal makine adına tıklayın ve ardından **uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="2bad2-149">In the Azure portal, click **Virtual Machines (classic)**, click the name of your new virtual machine, and then click **Endpoints**.</span></span>

    ![Uç Noktalar][Image7]

13. <span data-ttu-id="2bad2-151">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2bad2-151">Click **Add**.</span></span>

14. <span data-ttu-id="2bad2-152">Protokol "Mongo" adında bir uç nokta ekleyin **TCP**, her ikisi **ortak** ve **özel** bağlantı noktası "27017" ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2bad2-152">Add an endpoint with name "Mongo", protocol **TCP**, and both **Public** and **Private** ports set to "27017".</span></span> <span data-ttu-id="2bad2-153">Bu bağlantı noktası açmak, MongoDB uzaktan erişilmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="2bad2-153">Opening this port allows MongoDB to be accessed remotely.</span></span>

    ![Uç Noktalar][Image9]

> [!NOTE]
> <span data-ttu-id="2bad2-155">Bağlantı noktası 27017 MongoDB tarafından kullanılan varsayılan bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="2bad2-155">The port 27017 is the default port used by MongoDB.</span></span> <span data-ttu-id="2bad2-156">Bu varsayılan bağlantı noktası belirterek değiştirebileceğiniz `--port` mongod.exe sunucunun başlatırken parametresi.</span><span class="sxs-lookup"><span data-stu-id="2bad2-156">You can change this default port by specifying the `--port` parameter when starting the mongod.exe server.</span></span> <span data-ttu-id="2bad2-157">Güvenlik Duvarı'nda aynı bağlantı noktası numarası ve yukarıdaki yönergeleri "Mongo" uç verdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="2bad2-157">Make sure to give the same port number in the firewall and the "Mongo" endpoint in the preceding instructions.</span></span>
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png
