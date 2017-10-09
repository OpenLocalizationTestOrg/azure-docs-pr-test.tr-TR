
1. <span data-ttu-id="227a6-101">tooescalate ayrıcalıklar, türü:</span><span class="sxs-lookup"><span data-stu-id="227a6-101">tooescalate privileges, type:</span></span>
   
        sudo -s
   
    <span data-ttu-id="227a6-102">Parolanızı girin.</span><span class="sxs-lookup"><span data-stu-id="227a6-102">Enter your password.</span></span>
2. <span data-ttu-id="227a6-103">MySQL Community Server edition tooinstall yazın:</span><span class="sxs-lookup"><span data-stu-id="227a6-103">tooinstall MySQL Community Server edition, type:</span></span>
   
        zypper install mysql-community-server
   
    <span data-ttu-id="227a6-104">MySQL indirilir ve yüklenir bekleyin.</span><span class="sxs-lookup"><span data-stu-id="227a6-104">Wait while MySQL downloads and installs.</span></span>
3. <span data-ttu-id="227a6-105">Merhaba sistem önyüklendiğinde tooset MySQL toostart, türü:</span><span class="sxs-lookup"><span data-stu-id="227a6-105">tooset MySQL toostart when hello system boots, type:</span></span>
   
        insserv mysql
4. <span data-ttu-id="227a6-106">Merhaba MySQL arka plan programı (mysqld), bu komutla el ile başlatın:</span><span class="sxs-lookup"><span data-stu-id="227a6-106">Start hello MySQL daemon (mysqld) manually with this command:</span></span>
   
        rcmysql start
   
    <span data-ttu-id="227a6-107">Merhaba MySQL arka plan programı, türü toocheck hello durumu:</span><span class="sxs-lookup"><span data-stu-id="227a6-107">toocheck hello status of hello MySQL daemon, type:</span></span>
   
        rcmysql status
   
    <span data-ttu-id="227a6-108">toostop hello MySQL arka plan programı, yazın:</span><span class="sxs-lookup"><span data-stu-id="227a6-108">toostop hello MySQL daemon, type:</span></span>
   
        rcmysql stop
   
   > [!IMPORTANT]
   > <span data-ttu-id="227a6-109">Yükleme sonrasında, hello MySQL kök parola varsayılan olarak boştur.</span><span class="sxs-lookup"><span data-stu-id="227a6-109">After installation, hello MySQL root password is empty by default.</span></span> <span data-ttu-id="227a6-110">Çalıştırmanızı öneririz **mysql\_güvenli\_yükleme**, güvenli MySQL yardımcı olan bir komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="227a6-110">We recommended that you run **mysql\_secure\_installation**, a script that helps secure MySQL.</span></span> <span data-ttu-id="227a6-111">Hello betik toochange hello MySQL kök parola ister, anonim kullanıcı hesaplarını kaldırın, uzak kök oturum açmalar devre dışı bırakmak, test veritabanları kaldırın ve hello ayrıcalıkları tablo yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="227a6-111">hello script prompts you toochange hello MySQL root password, remove anonymous user accounts, disable remote root logins, remove test databases, and reload hello privileges table.</span></span> <span data-ttu-id="227a6-112">Bu seçeneklerin Evet tooall yanıtlayın ve hello kök parolasını değiştirme önerilir.</span><span class="sxs-lookup"><span data-stu-id="227a6-112">We recommended that you answer yes tooall of these options and change hello root password.</span></span>
   > 
   > 
5. <span data-ttu-id="227a6-113">Bu toorun hello betiği MySQL yükleme komut dosyası yazın:</span><span class="sxs-lookup"><span data-stu-id="227a6-113">Type this toorun hello script MySQL installation script:</span></span>
   
        mysql_secure_installation
6. <span data-ttu-id="227a6-114">İçinde tooMySQL oturum:</span><span class="sxs-lookup"><span data-stu-id="227a6-114">Log in tooMySQL:</span></span>
   
        mysql -u root -p
   
    <span data-ttu-id="227a6-115">(Hangi hello önceki adımda değiştirdiğiniz) hello MySQL kök parola girin ve bir istemiyle, sunulur burada hello veritabanıyla SQL deyimleri toointeract verebilir.</span><span class="sxs-lookup"><span data-stu-id="227a6-115">Enter hello MySQL root password (which you changed in hello previous step) and you'll be presented with a prompt where you can issue SQL statements toointeract with hello database.</span></span>
7. <span data-ttu-id="227a6-116">hello Hello aşağıdakini çalıştırın toocreate yeni bir MySQL kullanıcı **mysql >** istemi:</span><span class="sxs-lookup"><span data-stu-id="227a6-116">toocreate a new MySQL user, run hello following at hello **mysql>** prompt:</span></span>
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="227a6-117">Not, hello noktalı virgül (;) hello hello sonunda satırları hello komutları bitiş için önemli.</span><span class="sxs-lookup"><span data-stu-id="227a6-117">Note, hello semi-colons (;) at hello end of hello lines are crucial for ending hello commands.</span></span>
8. <span data-ttu-id="227a6-118">toocreate bir veritabanı ve grant hello `mysqluser` üzerindeki komutları aşağıdaki sorunu hello kullanıcının izinleri:</span><span class="sxs-lookup"><span data-stu-id="227a6-118">toocreate a database and grant hello `mysqluser` user permissions on it, issue hello following commands:</span></span>
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="227a6-119">Veritabanı kullanıcı adları ve parolalar toohello veritabanına bağlanma komut dosyaları tarafından yalnızca kullanıldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="227a6-119">Note that database user names and passwords are only used by scripts connecting toohello database.</span></span>  <span data-ttu-id="227a6-120">Veritabanı kullanıcı hesabı adları mutlaka hello sistem gerçek kullanıcı hesaplarında temsil etmiyor.</span><span class="sxs-lookup"><span data-stu-id="227a6-120">Database user account names do not necessarily represent actual user accounts on hello system.</span></span>
9. <span data-ttu-id="227a6-121">başka bir bilgisayardan türü toolog içinde:</span><span class="sxs-lookup"><span data-stu-id="227a6-121">toolog in from another computer, type:</span></span>
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    <span data-ttu-id="227a6-122">Burada `ip-address` içinden, bağlanan tooMySQL hello bilgisayar hello IP adresidir.</span><span class="sxs-lookup"><span data-stu-id="227a6-122">where `ip-address` is hello IP address of hello computer from which you will connect tooMySQL.</span></span>
10. <span data-ttu-id="227a6-123">MySQL veritabanı yönetim yardımcı programı, tooexit hello yazın:</span><span class="sxs-lookup"><span data-stu-id="227a6-123">tooexit hello MySQL database administration utility, type:</span></span>
    
        quit

## <a name="add-an-endpoint"></a><span data-ttu-id="227a6-124">Bir uç nokta ekleme</span><span class="sxs-lookup"><span data-stu-id="227a6-124">Add an endpoint</span></span>
1. <span data-ttu-id="227a6-125">MySQL yüklendikten sonra tooconfigure bir uç nokta tooaccess MySQL uzaktan gerekir.</span><span class="sxs-lookup"><span data-stu-id="227a6-125">After MySQL is installed, you'll need tooconfigure an endpoint tooaccess MySQL remotely.</span></span> <span data-ttu-id="227a6-126">İçinde toohello oturum [Klasik Azure portalı][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="227a6-126">Log in toohello [Azure  classic portal][AzurePortal].</span></span> <span data-ttu-id="227a6-127">Tıklatın **sanal makineleri**, yeni bir sanal makine hello adına tıklayın ve ardından **uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="227a6-127">Click **Virtual Machines**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>
2. <span data-ttu-id="227a6-128">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="227a6-128">Click **Add** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="227a6-129">Protokolüyle "MySQL" adlı bir uç nokta ekleyin **TCP**, ve **ortak** ve **özel** bağlantı noktaları kümesi çok "3306".</span><span class="sxs-lookup"><span data-stu-id="227a6-129">Add an endpoint named "MySQL" with protocol **TCP**, and **Public** and **Private** ports set too"3306".</span></span>
4. <span data-ttu-id="227a6-130">tooremotely bilgisayarınızdan türü toohello sanal makineye bağlanın:</span><span class="sxs-lookup"><span data-stu-id="227a6-130">tooremotely connect toohello virtual machine from your computer, type:</span></span>
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    <span data-ttu-id="227a6-131">Örneğin, bu öğreticide oluşturduğumuz hello sanal makine kullanarak, bu komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="227a6-131">For example, using hello virual machine we created in this tutorial, type this command:</span></span>
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
