<span data-ttu-id="b13c7-101">Bu adımları tooinstall izleyin ve MongoDB Windows Server çalıştıran bir sanal makinede çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b13c7-101">Follow these steps tooinstall and run MongoDB on a virtual machine running Windows Server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b13c7-102">Kimlik doğrulaması ve IP adresi bağlama gibi MongoDB güvenlik özellikleri varsayılan olarak etkin değildir.</span><span class="sxs-lookup"><span data-stu-id="b13c7-102">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="b13c7-103">Güvenlik özellikleri, MongoDB tooa üretim ortamına dağıtmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="b13c7-103">Security features should be enabled before deploying MongoDB tooa production environment.</span></span>  <span data-ttu-id="b13c7-104">Daha fazla bilgi için bkz: [güvenlik ve kimlik doğrulama](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="b13c7-104">For more information, see [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>
>
>

1. <span data-ttu-id="b13c7-105">Uzak Masaüstü kullanarak toohello sanal makineye bağlandıktan sonra Internet Explorer hello açın **Başlat** hello sanal makine menüsünde.</span><span class="sxs-lookup"><span data-stu-id="b13c7-105">After you've connected toohello virtual machine using Remote Desktop, open Internet Explorer from hello **Start** menu on hello virtual machine.</span></span>
2. <span data-ttu-id="b13c7-106">Select hello **Araçları** hello sağ üst köşesindeki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="b13c7-106">Select hello **Tools** button in hello upper right corner.</span></span>  <span data-ttu-id="b13c7-107">İçinde **Internet Seçenekleri**seçin hello **güvenlik** sekmesini tıklatın ve ardından hello seçin **Güvenilen siteler** simgesi ve son olarak hello tıklayın **siteleri** düğme.</span><span class="sxs-lookup"><span data-stu-id="b13c7-107">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon, and finally click hello **Sites** button.</span></span> <span data-ttu-id="b13c7-108">Ekleme *https://\*. mongodb.org* Güvenilen siteler toohello listesi.</span><span class="sxs-lookup"><span data-stu-id="b13c7-108">Add *https://\*.mongodb.org* toohello list of trusted sites.</span></span>
3. <span data-ttu-id="b13c7-109">Çok Git[yüklemeleri - MongoDB](https://www.mongodb.com/download-center#community).</span><span class="sxs-lookup"><span data-stu-id="b13c7-109">Go too[Downloads - MongoDB](https://www.mongodb.com/download-center#community).</span></span>
4. <span data-ttu-id="b13c7-110">Hello bulur **geçerli durağan sürümü** , **Community Server**seçin hello son **64-bit** hello Windows sütununda sürümü.</span><span class="sxs-lookup"><span data-stu-id="b13c7-110">Find hello **Current Stable Release** of **Community Server**, select hello latest **64-bit** version in hello Windows column.</span></span> <span data-ttu-id="b13c7-111">Karşıdan yükle ve hello MSI yükleyicisi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b13c7-111">Download, then run hello MSI installer.</span></span>
5. <span data-ttu-id="b13c7-112">MongoDB genellikle C:\Program Files\MongoDB yüklenir.</span><span class="sxs-lookup"><span data-stu-id="b13c7-112">MongoDB is typically installed in C:\Program Files\MongoDB.</span></span> <span data-ttu-id="b13c7-113">İçin ortam değişkenleri hello masaüstünde arayın ve hello MongoDB ikili dosyalarının yolu toohello PATH değişkeni ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b13c7-113">Search for Environment Variables on hello desktop and add hello MongoDB binaries path toohello PATH variable.</span></span> <span data-ttu-id="b13c7-114">Örneğin, C:\Program Files\MongoDB\Server\3.4\bin hello ikili dosyaları makinenizde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b13c7-114">For example, you might find hello binaries at C:\Program Files\MongoDB\Server\3.4\bin on your machine.</span></span>
6. <span data-ttu-id="b13c7-115">MongoDB veri ve günlük dizinleri hello veri diski oluşturma (sürücü gibi **F:**) adımları önceki hello oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="b13c7-115">Create MongoDB data and log directories in hello data disk (such as drive **F:**) you created in hello preceding steps.</span></span> <span data-ttu-id="b13c7-116">Gelen **Başlat**seçin **komut istemi** tooopen bir komut istemi penceresi.</span><span class="sxs-lookup"><span data-stu-id="b13c7-116">From **Start**, select **Command Prompt** tooopen a command prompt window.</span></span>  <span data-ttu-id="b13c7-117">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="b13c7-117">Type:</span></span>

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. <span data-ttu-id="b13c7-118">toorun hello veritabanı, çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b13c7-118">toorun hello database, run:</span></span>

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    <span data-ttu-id="b13c7-119">Tüm günlük iletilerini yönlendirilmiş toohello olan *F:\MongoLogs\mongolog.log* dosya mongod.exe sunucu başlar ve günlük dosyalarını preallocates gibi.</span><span class="sxs-lookup"><span data-stu-id="b13c7-119">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as mongod.exe server starts and preallocates journal files.</span></span> <span data-ttu-id="b13c7-120">Merhaba günlük dosyaları MongoDB toopreallocate için birkaç dakika sürer ve bağlantıları dinlemeyi Başlat.</span><span class="sxs-lookup"><span data-stu-id="b13c7-120">It may take several minutes for MongoDB toopreallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="b13c7-121">MongoDB örneğinizin çalışırken hello komut istemi bu görevde odaklanmış kalır.</span><span class="sxs-lookup"><span data-stu-id="b13c7-121">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span>
8. <span data-ttu-id="b13c7-122">toostart hello MongoDB yönetim kabuğunu açın başka bir komut penceresinde **Başlat** ve türü hello aşağıdaki komutlar:</span><span class="sxs-lookup"><span data-stu-id="b13c7-122">toostart hello MongoDB administrative shell, open another command window from **Start** and type hello following commands:</span></span>

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

    <span data-ttu-id="b13c7-123">Merhaba veritabanı hello Ekle tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b13c7-123">hello database is created by hello insert.</span></span>
9. <span data-ttu-id="b13c7-124">Alternatif olarak, bir hizmet olarak mongod.exe yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b13c7-124">Alternatively, you can install mongod.exe as a service:</span></span>

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    <span data-ttu-id="b13c7-125">Bir hizmeti yüklendi "Mongo VT" açıklaması ile MongoDB adlı.</span><span class="sxs-lookup"><span data-stu-id="b13c7-125">A service is installed named MongoDB with a description of "Mongo DB".</span></span> <span data-ttu-id="b13c7-126">Merhaba `--logpath` seçeneği kullanılan toospecify bir günlük dosyası olması gerekir, bu yana hello hizmetini çalıştıran bir komut penceresinde toodisplay çıktısı yok.</span><span class="sxs-lookup"><span data-stu-id="b13c7-126">hello `--logpath` option must be used toospecify a log file, since hello running service does not have a command window toodisplay output.</span></span>  <span data-ttu-id="b13c7-127">Merhaba `--logappend` seçeneği belirtir hello hizmetinin yeniden başlatma çıkış tooappend toohello mevcut günlük dosyası neden olur.</span><span class="sxs-lookup"><span data-stu-id="b13c7-127">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>  <span data-ttu-id="b13c7-128">Merhaba `--dbpath` seçeneği hello hello veri dizininin konumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="b13c7-128">hello `--dbpath` option specifies hello location of hello data directory.</span></span> <span data-ttu-id="b13c7-129">Daha fazla hizmeti ile ilgili komut satırı seçenekleri için bkz [hizmeti ile ilgili komut satırı seçenekleri][MongoWindowsSvcOptions].</span><span class="sxs-lookup"><span data-stu-id="b13c7-129">For more service-related command-line options, see [Service-related command-line options][MongoWindowsSvcOptions].</span></span>

    <span data-ttu-id="b13c7-130">toostart hello hizmeti, şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b13c7-130">toostart hello service, run this command:</span></span>

        C:\> net start MongoDB
10. <span data-ttu-id="b13c7-131">Böylece MongoDB yüklü ve çalışan, tooopen bir bağlantı noktası Windows Güvenlik Duvarı'nda gereksinim tooMongoDB uzaktan bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b13c7-131">Now that MongoDB is installed and running, you need tooopen a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span>  <span data-ttu-id="b13c7-132">Merhaba gelen **Başlat** menüsünde, select **Yönetimsel Araçlar** ve ardından **Gelişmiş Güvenlik Özellikli Windows Güvenlik Duvarı**.</span><span class="sxs-lookup"><span data-stu-id="b13c7-132">From hello **Start** menu, select **Administrative Tools** and then **Windows Firewall with Advanced Security**.</span></span>
11. <span data-ttu-id="b13c7-133">bir) Merhaba sol bölmesinde seçin **gelen kuralları**.</span><span class="sxs-lookup"><span data-stu-id="b13c7-133">a) In hello left pane, select **Inbound Rules**.</span></span>  <span data-ttu-id="b13c7-134">Merhaba, **Eylemler** bölmesinde sağ hello select **yeni kural...** .</span><span class="sxs-lookup"><span data-stu-id="b13c7-134">In hello **Actions** pane on hello right, select **New Rule...**.</span></span>

    ![Windows Güvenlik Duvarı][Image1]

    <span data-ttu-id="b13c7-136">b) içinde hello **yeni gelen kuralı Sihirbazı**seçin **bağlantı noktası** ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="b13c7-136">b) In hello **New Inbound Rule Wizard**, select **Port** and then click **Next**.</span></span>

    ![Windows Güvenlik Duvarı][Image2]

    <span data-ttu-id="b13c7-138">c) select **TCP** ve ardından **belirli yerel bağlantı noktaları**.</span><span class="sxs-lookup"><span data-stu-id="b13c7-138">c) Select **TCP** and then **Specific local ports**.</span></span>  <span data-ttu-id="b13c7-139">' I tıklatın ve "27017" (MongoDB dinlediği hello varsayılan bağlantı noktası) bir bağlantı noktası belirtin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="b13c7-139">Specify a port of "27017" (hello default port MongoDB listens on) and click **Next**.</span></span>

    ![Windows Güvenlik Duvarı][Image3]

    <span data-ttu-id="b13c7-141">d) select **hello bağlantıya izin verme** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="b13c7-141">d) Select **Allow hello connection** and click **Next**.</span></span>

    ![Windows Güvenlik Duvarı][Image4]

    <span data-ttu-id="b13c7-143">e) tıklatın **sonraki** yeniden.</span><span class="sxs-lookup"><span data-stu-id="b13c7-143">e) Click **Next** again.</span></span>

    ![Windows Güvenlik Duvarı][Image5]

    <span data-ttu-id="b13c7-145">f) "MongoPort" gibi hello kuralı için bir ad belirtin ve tıklayın **son**.</span><span class="sxs-lookup"><span data-stu-id="b13c7-145">f) Specify a name for hello rule, such as "MongoPort", and click **Finish**.</span></span>

    ![Windows Güvenlik Duvarı][Image6]

12. <span data-ttu-id="b13c7-147">Merhaba sanal makineyi oluşturduğunuzda MongoDB için bir uç nokta yapılandırmadıysanız, bunu şimdi yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b13c7-147">If you didn't configure an endpoint for MongoDB when you created hello virtual machine, you can do it now.</span></span> <span data-ttu-id="b13c7-148">Merhaba güvenlik duvarı kuralı ve hello uç nokta toobe mümkün tooconnect tooMongoDB uzaktan ihtiyacınız var.</span><span class="sxs-lookup"><span data-stu-id="b13c7-148">You need both hello firewall rule and hello endpoint toobe able tooconnect tooMongoDB remotely.</span></span>

  <span data-ttu-id="b13c7-149">Hello Azure portal'ı tıklatın **sanal makineleri (Klasik)**, yeni bir sanal makine hello adına tıklayın ve ardından **uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="b13c7-149">In hello Azure portal, click **Virtual Machines (classic)**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>

    ![Uç Noktalar][Image7]

13. <span data-ttu-id="b13c7-151">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b13c7-151">Click **Add**.</span></span>

14. <span data-ttu-id="b13c7-152">Protokol "Mongo" adında bir uç nokta ekleyin **TCP**, her ikisi **ortak** ve **özel** bağlantı noktaları kümesi "27017" çok.</span><span class="sxs-lookup"><span data-stu-id="b13c7-152">Add an endpoint with name "Mongo", protocol **TCP**, and both **Public** and **Private** ports set too"27017".</span></span> <span data-ttu-id="b13c7-153">Bu bağlantı noktası açmak, MongoDB toobe uzaktan erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="b13c7-153">Opening this port allows MongoDB toobe accessed remotely.</span></span>

    ![Uç Noktalar][Image9]

> [!NOTE]
> <span data-ttu-id="b13c7-155">başlangıç bağlantı noktası 27017 MongoDB tarafından kullanılan hello varsayılan bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="b13c7-155">hello port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="b13c7-156">Bu varsayılan bağlantı noktası hello belirterek değiştirebileceğiniz `--port` hello mongod.exe sunucu başlatırken parametresi.</span><span class="sxs-lookup"><span data-stu-id="b13c7-156">You can change this default port by specifying hello `--port` parameter when starting hello mongod.exe server.</span></span> <span data-ttu-id="b13c7-157">Merhaba Güvenlik Duvarı'nda aynı bağlantı noktası numarası hello ve yönergeleri önceki hello "Mongo" uç hello emin toogive olun.</span><span class="sxs-lookup"><span data-stu-id="b13c7-157">Make sure toogive hello same port number in hello firewall and hello "Mongo" endpoint in hello preceding instructions.</span></span>
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
