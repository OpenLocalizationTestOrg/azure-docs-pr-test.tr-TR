## <a name="install-wordpress"></a>WordPress yükleme

Yığın tootry istiyorsanız, örnek bir uygulama yükleyin. Örnek olarak, aşağıdaki adımları hello yüklemek hello açık kaynak [WordPress](https://wordpress.org/) platform toocreate Web siteleri ve Web günlükleri. Diğer iş yükleri tootry dahil [Drupal](http://www.drupal.org) ve [Moodle](https://moodle.org/). 

Kavram kanıtı için bu WordPress kurulur. Daha fazla bilgi ve üretim yüklemesine yönelik ayarlar için bkz: hello [WordPress belgelerine](https://codex.wordpress.org/Main_Page). 



### <a name="install-hello-wordpress-package"></a>Merhaba WordPress paketini yükle

Merhaba aşağıdaki komutu çalıştırın:

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a>WordPress’i yapılandırma

WordPress toouse MySQL ve PHP yapılandırın. Bir metin düzenleyiciyi komutu tooopen aşağıdaki hello çalıştırın ve hello dosyası oluşturma `/etc/wordpress/config-localhost.php`:

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
Aşağıdaki satırları toohello dosyasına, veritabanı parolasını değiştirme kopyalama hello *yourPassword* (diğer değerleri değiştirmeden bırakın). Ardından hello dosyayı kaydedin.

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

Bir çalışma dizini içinde bir metin dosyası oluşturun `wordpress.sql` tooconfigure hello WordPress veritabanı: 

```bash
sudo sensible-editor wordpress.sql
```

Aşağıdaki komutlar, veritabanı parolasını değiştirme hello eklemek *yourPassword* (diğer değerleri değiştirmeden bırakın). Ardından hello dosyayı kaydedin.

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


Komut toocreate hello veritabanı aşağıdaki hello çalıştırın:

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

Merhaba komut tamamlandıktan sonra hello dosya silme `wordpress.sql`.

Merhaba WordPress yükleme toohello web sunucusu belge kökü Taşı:

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

Şimdi hello WordPress Kurulumu tamamlamak ve hello platformda yayımlayın. Bir tarayıcı açın ve çok`http://yourPublicIPAddress/wordpress`. VM Hello genel IP adresini değiştirin. Benzer toothis görüntü görünmelidir.

![WordPress yükleme sayfası](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)