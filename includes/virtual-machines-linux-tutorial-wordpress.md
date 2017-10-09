## <a name="install-wordpress"></a><span data-ttu-id="e4e0c-101">WordPress yükleme</span><span class="sxs-lookup"><span data-stu-id="e4e0c-101">Install WordPress</span></span>

<span data-ttu-id="e4e0c-102">Yığın tootry istiyorsanız, örnek bir uygulama yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e4e0c-102">If you want tootry your stack, install a sample app.</span></span> <span data-ttu-id="e4e0c-103">Örnek olarak, aşağıdaki adımları hello yüklemek hello açık kaynak [WordPress](https://wordpress.org/) platform toocreate Web siteleri ve Web günlükleri.</span><span class="sxs-lookup"><span data-stu-id="e4e0c-103">As an example, hello following steps install hello open source [WordPress](https://wordpress.org/) platform toocreate websites and blogs.</span></span> <span data-ttu-id="e4e0c-104">Diğer iş yükleri tootry dahil [Drupal](http://www.drupal.org) ve [Moodle](https://moodle.org/).</span><span class="sxs-lookup"><span data-stu-id="e4e0c-104">Other workloads tootry include [Drupal](http://www.drupal.org) and [Moodle](https://moodle.org/).</span></span> 

<span data-ttu-id="e4e0c-105">Kavram kanıtı için bu WordPress kurulur.</span><span class="sxs-lookup"><span data-stu-id="e4e0c-105">This WordPress setup is for proof of concept.</span></span> <span data-ttu-id="e4e0c-106">Daha fazla bilgi ve üretim yüklemesine yönelik ayarlar için bkz: hello [WordPress belgelerine](https://codex.wordpress.org/Main_Page).</span><span class="sxs-lookup"><span data-stu-id="e4e0c-106">For more information and settings for production installation, see hello [WordPress documentation](https://codex.wordpress.org/Main_Page).</span></span> 



### <a name="install-hello-wordpress-package"></a><span data-ttu-id="e4e0c-107">Merhaba WordPress paketini yükle</span><span class="sxs-lookup"><span data-stu-id="e4e0c-107">Install hello WordPress package</span></span>

<span data-ttu-id="e4e0c-108">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e4e0c-108">Run hello following command:</span></span>

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a><span data-ttu-id="e4e0c-109">WordPress’i yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e4e0c-109">Configure WordPress</span></span>

<span data-ttu-id="e4e0c-110">WordPress toouse MySQL ve PHP yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e4e0c-110">Configure WordPress toouse MySQL and PHP.</span></span> <span data-ttu-id="e4e0c-111">Bir metin düzenleyiciyi komutu tooopen aşağıdaki hello çalıştırın ve hello dosyası oluşturma `/etc/wordpress/config-localhost.php`:</span><span class="sxs-lookup"><span data-stu-id="e4e0c-111">Run hello following command tooopen a text editor of your choice and create hello file `/etc/wordpress/config-localhost.php`:</span></span>

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
<span data-ttu-id="e4e0c-112">Aşağıdaki satırları toohello dosyasına, veritabanı parolasını değiştirme kopyalama hello *yourPassword* (diğer değerleri değiştirmeden bırakın).</span><span class="sxs-lookup"><span data-stu-id="e4e0c-112">Copy hello following lines toohello file, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="e4e0c-113">Ardından hello dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e4e0c-113">Then save hello file.</span></span>

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

<span data-ttu-id="e4e0c-114">Bir çalışma dizini içinde bir metin dosyası oluşturun `wordpress.sql` tooconfigure hello WordPress veritabanı:</span><span class="sxs-lookup"><span data-stu-id="e4e0c-114">In a working directory, create a text file `wordpress.sql` tooconfigure hello WordPress database:</span></span> 

```bash
sudo sensible-editor wordpress.sql
```

<span data-ttu-id="e4e0c-115">Aşağıdaki komutlar, veritabanı parolasını değiştirme hello eklemek *yourPassword* (diğer değerleri değiştirmeden bırakın).</span><span class="sxs-lookup"><span data-stu-id="e4e0c-115">Add hello following commands, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="e4e0c-116">Ardından hello dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e4e0c-116">Then save hello file.</span></span>

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


<span data-ttu-id="e4e0c-117">Komut toocreate hello veritabanı aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e4e0c-117">Run hello following command toocreate hello database:</span></span>

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

<span data-ttu-id="e4e0c-118">Merhaba komut tamamlandıktan sonra hello dosya silme `wordpress.sql`.</span><span class="sxs-lookup"><span data-stu-id="e4e0c-118">After hello command completes, delete hello file `wordpress.sql`.</span></span>

<span data-ttu-id="e4e0c-119">Merhaba WordPress yükleme toohello web sunucusu belge kökü Taşı:</span><span class="sxs-lookup"><span data-stu-id="e4e0c-119">Move hello WordPress installation toohello web server document root:</span></span>

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

<span data-ttu-id="e4e0c-120">Şimdi hello WordPress Kurulumu tamamlamak ve hello platformda yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="e4e0c-120">Now you can complete hello WordPress setup and publish on hello platform.</span></span> <span data-ttu-id="e4e0c-121">Bir tarayıcı açın ve çok`http://yourPublicIPAddress/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="e4e0c-121">Open a browser and go too`http://yourPublicIPAddress/wordpress`.</span></span> <span data-ttu-id="e4e0c-122">VM Hello genel IP adresini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e4e0c-122">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="e4e0c-123">Benzer toothis görüntü görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="e4e0c-123">It should look similar toothis image.</span></span>

![WordPress yükleme sayfası](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)