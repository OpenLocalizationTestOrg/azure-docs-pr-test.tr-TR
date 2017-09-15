
1. <span data-ttu-id="e26a0-101">Ayrıcalıkları yükseltmek için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="e26a0-101">To escalate privileges, type:</span></span>
   
        sudo -s
   
    <span data-ttu-id="e26a0-102">Parolanızı girin.</span><span class="sxs-lookup"><span data-stu-id="e26a0-102">Enter your password.</span></span>
2. <span data-ttu-id="e26a0-103">MySQL Community Server edition'ı yüklemek için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="e26a0-103">To install MySQL Community Server edition, type:</span></span>
   
        zypper install mysql-community-server
   
    <span data-ttu-id="e26a0-104">MySQL indirilir ve yüklenir bekleyin.</span><span class="sxs-lookup"><span data-stu-id="e26a0-104">Wait while MySQL downloads and installs.</span></span>
3. <span data-ttu-id="e26a0-105">Sistem önyüklendiğinde başlatmak için MySQL ayarlamak için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="e26a0-105">To set MySQL to start when the system boots, type:</span></span>
   
        insserv mysql
4. <span data-ttu-id="e26a0-106">MySQL arka plan programı (mysqld), bu komutla el ile başlatın:</span><span class="sxs-lookup"><span data-stu-id="e26a0-106">Start the MySQL daemon (mysqld) manually with this command:</span></span>
   
        rcmysql start
   
    <span data-ttu-id="e26a0-107">MySQL arka plan programı durumunu denetlemek için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="e26a0-107">To check the status of the MySQL daemon, type:</span></span>
   
        rcmysql status
   
    <span data-ttu-id="e26a0-108">MySQL arka plan programı durdurmak için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="e26a0-108">To stop the MySQL daemon, type:</span></span>
   
        rcmysql stop
   
   > [!IMPORTANT]
   > <span data-ttu-id="e26a0-109">Yükleme sonrasında, MySQL kök parola varsayılan olarak boştur.</span><span class="sxs-lookup"><span data-stu-id="e26a0-109">After installation, the MySQL root password is empty by default.</span></span> <span data-ttu-id="e26a0-110">Çalıştırmanızı öneririz **mysql\_güvenli\_yükleme**, güvenli MySQL yardımcı olan bir komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="e26a0-110">We recommended that you run **mysql\_secure\_installation**, a script that helps secure MySQL.</span></span> <span data-ttu-id="e26a0-111">Komut dosyası MySQL kök parolasını değiştirmek, anonim kullanıcı hesaplarını kaldırın, uzak kök oturum açmalar devre dışı bırakmak, test veritabanlarını kaldırmanız ve ayrıcalıkları tablo yeniden ister.</span><span class="sxs-lookup"><span data-stu-id="e26a0-111">The script prompts you to change the MySQL root password, remove anonymous user accounts, disable remote root logins, remove test databases, and reload the privileges table.</span></span> <span data-ttu-id="e26a0-112">Bu seçeneklerin Tümüne Evet yanıtlayın ve kök parola değiştirme önerilir.</span><span class="sxs-lookup"><span data-stu-id="e26a0-112">We recommended that you answer yes to all of these options and change the root password.</span></span>
   > 
   > 
5. <span data-ttu-id="e26a0-113">MySQL yükleme betiği komut dosyasını çalıştırmak için bunu yazın:</span><span class="sxs-lookup"><span data-stu-id="e26a0-113">Type this to run the script MySQL installation script:</span></span>
   
        mysql_secure_installation
6. <span data-ttu-id="e26a0-114">MySQL için oturum açın:</span><span class="sxs-lookup"><span data-stu-id="e26a0-114">Log in to MySQL:</span></span>
   
        mysql -u root -p
   
    <span data-ttu-id="e26a0-115">(Önceki adımda değiştirdiğiniz) MySQL kök parola girin ve bir istemiyle, sunulur veritabanıyla etkileşim için SQL deyimleri burada verebilir.</span><span class="sxs-lookup"><span data-stu-id="e26a0-115">Enter the MySQL root password (which you changed in the previous step) and you'll be presented with a prompt where you can issue SQL statements to interact with the database.</span></span>
7. <span data-ttu-id="e26a0-116">Yeni bir MySQL kullanıcı oluşturmak için aşağıdaki çalıştırın **mysql >** istemi:</span><span class="sxs-lookup"><span data-stu-id="e26a0-116">To create a new MySQL user, run the following at the **mysql>** prompt:</span></span>
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="e26a0-117">Not, noktalı virgül (;) satırları sonunda komutları bitiş için önemli olan.</span><span class="sxs-lookup"><span data-stu-id="e26a0-117">Note, the semi-colons (;) at the end of the lines are crucial for ending the commands.</span></span>
8. <span data-ttu-id="e26a0-118">Bir veritabanı oluşturmak ve vermek için `mysqluser` , kullanıcı izinlerini vermek aşağıdaki komutlar:</span><span class="sxs-lookup"><span data-stu-id="e26a0-118">To create a database and grant the `mysqluser` user permissions on it, issue the following commands:</span></span>
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* TO 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="e26a0-119">Veritabanı kullanıcı adları ve parolalar yalnızca veritabanına bağlanırken komut dosyaları tarafından kullanıldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e26a0-119">Note that database user names and passwords are only used by scripts connecting to the database.</span></span>  <span data-ttu-id="e26a0-120">Veritabanı kullanıcı hesabı adları mutlaka gerçek kullanıcı hesapları sistem üzerindeki temsil etmiyor.</span><span class="sxs-lookup"><span data-stu-id="e26a0-120">Database user account names do not necessarily represent actual user accounts on the system.</span></span>
9. <span data-ttu-id="e26a0-121">Başka bir bilgisayardan oturum açmak için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="e26a0-121">To log in from another computer, type:</span></span>
   
        GRANT ALL ON testdatabase.* TO 'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    <span data-ttu-id="e26a0-122">Burada `ip-address` içinden, bağlanan MySQL için bilgisayarın IP adresidir.</span><span class="sxs-lookup"><span data-stu-id="e26a0-122">where `ip-address` is the IP address of the computer from which you will connect to MySQL.</span></span>
10. <span data-ttu-id="e26a0-123">MySQL veritabanı yönetim yardımcı programı'ndan çıkmak için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="e26a0-123">To exit the MySQL database administration utility, type:</span></span>
    
        quit

## <a name="add-an-endpoint"></a><span data-ttu-id="e26a0-124">Bir uç nokta ekleme</span><span class="sxs-lookup"><span data-stu-id="e26a0-124">Add an endpoint</span></span>
1. <span data-ttu-id="e26a0-125">MySQL yüklendikten sonra MySQL uzaktan erişmek için bir uç nokta yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e26a0-125">After MySQL is installed, you'll need to configure an endpoint to access MySQL remotely.</span></span> <span data-ttu-id="e26a0-126">Oturum [Klasik Azure portalı][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="e26a0-126">Log in to the [Azure  classic portal][AzurePortal].</span></span> <span data-ttu-id="e26a0-127">Tıklatın **sanal makineleri**, yeni bir sanal makine adına tıklayın ve ardından **uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="e26a0-127">Click **Virtual Machines**, click the name of your new virtual machine, and then click **Endpoints**.</span></span>
2. <span data-ttu-id="e26a0-128">Tıklatın **Ekle** sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="e26a0-128">Click **Add** at the bottom of the page.</span></span>
3. <span data-ttu-id="e26a0-129">Protokolüyle "MySQL" adlı bir uç nokta ekleyin **TCP**, ve **ortak** ve **özel** bağlantı noktası "3306" ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e26a0-129">Add an endpoint named "MySQL" with protocol **TCP**, and **Public** and **Private** ports set to "3306".</span></span>
4. <span data-ttu-id="e26a0-130">Uzaktan bilgisayarınızdan sanal makineye bağlanmak için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="e26a0-130">To remotely connect to the virtual machine from your computer, type:</span></span>
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    <span data-ttu-id="e26a0-131">Örneğin, biz Bu öğreticide oluşturduğunuz sanal makine kullanarak, bu komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="e26a0-131">For example, using the virual machine we created in this tutorial, type this command:</span></span>
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
