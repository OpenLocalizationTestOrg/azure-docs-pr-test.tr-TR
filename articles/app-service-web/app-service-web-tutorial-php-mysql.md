---
title: "aaaBuild azure'da PHP ve MySQL bir web uygulaması | Microsoft Docs"
description: "Bilgi nasıl Azure'da çalışan bir PHP uygulaması ile bağlantı tooa MySQL veritabanı Azure'da tooget."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 14feb4f3-5095-496e-9a40-690e1414bd73
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 07/21/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3c050b30e2e2c80d011bed989cd5f8cecac35d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a>Azure'da PHP ve MySQL bir web uygulaması oluşturma

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar. Bu öğretici nasıl toocreate bir PHP web uygulaması Azure ve tooa MySQL veritabanına bağlanmak gösterir. İşiniz bittiğinde, gerekir bir [Laravel](https://laravel.com/) Azure App Service Web Apps üzerinde çalışan uygulama.

![Azure uygulama Hizmeti'nde çalışan PHP uygulaması](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * Azure üzerinde MySQL veritabanı oluşturma
> * PHP uygulama tooMySQL Bağlan
> * Merhaba uygulama tooAzure dağıtma
> * Merhaba veri modeli güncelleştirmek ve hello uygulama yeniden dağıtın
> * Azure Stream tanılama günlükleri
> * Merhaba uygulamada hello Azure portalı Yönet

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğretici:

* [Git'i yükleyin](https://git-scm.com/)
* [PHP 5.6.4 yükleme veya üstü](http://php.net/downloads.php)
* [Oluşturucu yükleyin](https://getcomposer.org/doc/00-intro.md)
* PHP uzantıları Laravel gereksinimlerini aşağıdaki hello etkinleştirin: OpenSSL, PDO MySQL, Mbstring, belirteç Oluşturucu, XML
* [Yükleyin ve MySQL başlatın](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a>Yerel MySQL hazırlama

Bu adımda, bir veritabanı yerel MySQL sunucunuzu Bu öğreticide, kullanımınız için oluşturun.

### <a name="connect-toolocal-mysql-server"></a>Toolocal MySQL server Bağlan

Bir terminal penceresi tooyour yerel MySQL sunucusuna bağlanın. Bu bir terminal penceresi toorun Bu öğreticide tüm hello komutlarını kullanabilirsiniz.

```bash
mysql -u root -p
```

İçin bir parola istenirse Merhaba hello parolayı girin `root` hesabı. Kök hesap parolanızı hatırlamıyorsanız bkz [MySQL: nasıl tooReset hello kök parola](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).

Komutunuzu başarıyla çalışırsa, MySQL sunucunuzu çalışıyor. Aksi takdirde, yerel MySQL sunucunuz tarafından aşağıdaki hello başlatıldığından emin olun [MySQL yükleme sonrası adımları](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).

### <a name="create-a-database-locally"></a>Yerel bir veritabanı oluşturun

Merhaba, `mysql` isteminde, bir veritabanı oluşturun.

```sql 
CREATE DATABASE sampledb;
```

Sunucu bağlantısı yazarak çıkmak `quit`.

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a>Yerel olarak bir PHP uygulaması oluşturma
Bu adımda, Laravel örnek bir uygulama almak, veritabanı bağlantısını yapılandırın ve yerel olarak çalıştırın. 

### <a name="clone-hello-sample"></a>Kopya hello örnek

Merhaba terminal penceresinde `cd` tooa çalışma dizini.

Çalışma hello aşağıdaki tooclone hello örnek depo komutu.

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

`cd`tooyour kopyalanan dizin.
Gerekli hello paketlerini yükleyin.

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a>MySQL bağlantısını yapılandırın

Merhaba depo kök dizininde adlı bir dosya oluşturun *.env*. Değişkenleri hello aşağıdaki kopyalama hello *.env* dosya. Hello yerine  _&lt;root_password >_ yer tutucusunu hello MySQL kök kullanıcının parolası ile.

```
APP_ENV=local
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=sampledb
DB_USERNAME=root
DB_PASSWORD=<root_password>
```

Laravel hello nasıl kullandığı hakkında bilgi için _.env_ dosya için bkz: [Laravel ortamı Yapılandırması](https://laravel.com/docs/5.4/configuration#environment-configuration).

### <a name="run-hello-sample-locally"></a>Merhaba örnek yerel olarak çalıştırma

Çalıştırma [Laravel veritabanı geçişler](https://laravel.com/docs/5.4/migrations) toocreate hello tabloları hello uygulama gereksinimleri. hangi tablolar oluşturulur hello geçişlerde, arama hello toosee _veritabanı/geçişler_ hello Git deposu dizin.

```bash
php artisan migrate
```

Yeni bir Laravel uygulama anahtarı oluşturur.

```bash
php artisan key:generate
```

Merhaba uygulamayı çalıştırın.

```bash
php artisan serve
```

Çok gidin`http://localhost:8000` bir tarayıcıda. Bazı görevleri hello sayfasında ekleyin.

![PHP tooMySQL başarıyla bağlanır.](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

PHP, toostop yazın `Ctrl + C` hello terminal içinde.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a>MySQL oluşturma

Bu adımda oluşturduğunuz MySQL veritabanında [Azure veritabanı için MySQL (Önizleme)](/azure/mysql). Daha sonra hello PHP uygulama tooconnect toothis veritabanını yapılandırın.

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a>MySQL sunucusu oluşturun

Bir sunucu Azure veritabanı'nda MySQL (Önizleme) ile Merhaba oluşturmak [az mysql sunucusu oluşturun](/cli/azure/mysql/server#create) komutu.

Hello hello gördüğünüz MySQL server adınızı alternatif komutu, aşağıdaki  _&lt;mysql_server_name >_ yer tutucu (geçerli karakterler `a-z`, `0-9`, ve `-`). Bu ad hello MySQL sunucunun ana bilgisayar adı bir parçasıdır (`<mysql_server_name>.database.windows.net`), toobe genel olarak benzersiz olmalıdır.

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

Merhaba MySQL server oluşturulduğunda hello Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir:

```json
{
  "administratorLogin": "adminuser",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<mysql_server_name>.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>",
  "location": "northeurope",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  ...
}
```

### <a name="configure-server-firewall"></a>Sunucu Güvenlik Duvarı'nı yapılandırma

Bağlantılar için MySQL server tooallow istemcinizi hello kullanarak bir güvenlik duvarı kuralı oluşturun [az mysql server güvenlik duvarı kuralı oluşturmak](/cli/azure/mysql/server/firewall-rule#create) komutu.

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> Azure veritabanı için MySQL (Önizleme) şu anda bağlantıları yalnızca tooAzure Hizmetleri sınırlamak değil. Dinamik olarak atanmış IP adresleri azure'da gibi daha iyi tooenable olan tüm IP adresleri. Merhaba, önizlemede hizmetidir. Veritabanınızın güvenliğini sağlamak için daha iyi yöntemleri aşağıda verilmiştir.
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a>Yerel olarak tooproduction MySQL server Bağlan

Merhaba terminal penceresinde, azure'da toohello MySQL sunucusuna bağlanın. Daha önce için belirttiğiniz başlangıç değeri kullanın  _&lt;mysql_server_name >_.

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

Kullanmak için bir parola istendiğinde, _tr0ngPa $$ w0rd!_, hello veritabanı oluşturduğunuzda belirttiğiniz.

### <a name="create-a-production-database"></a>Bir üretim veritabanı oluşturma

Merhaba, `mysql` isteminde, bir veritabanı oluşturun.

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a>İzinleri olan bir kullanıcı oluşturun

Adlı bir veritabanı kullanıcısı oluşturmalıdır _phpappuser_ ve hello tüm ayrıcalıkları vermek `sampledb` veritabanı.

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

Exit hello sunucu bağlantısı yazarak `quit`.

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a>Uygulama tooAzure MySQL Bağlan

Bu adımda, Azure veritabanı'nda MySQL (Önizleme) için oluşturulan hello PHP uygulama toohello MySQL veritabanını bağlayın.

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a>Merhaba veritabanı bağlantısını yapılandır

Merhaba depo kök dizininde oluşturma bir _. env.production_ değişkenleri içine aşağıdaki dosya ve kopyalama hello. Merhaba yer tutucu Değiştir  _&lt;mysql_server_name >_.

```
APP_ENV=production
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=<mysql_server_name>.database.windows.net
DB_DATABASE=sampledb
DB_USERNAME=phpappuser@<mysql_server_name>
DB_PASSWORD=MySQLAzure2017
MYSQL_SSL=true
```

Merhaba değişiklikleri kaydedin.

> [!TIP]
> MySQL bağlantı bilgilerinizi, bu dosya zaten hello Git deposundan dışarıda toosecure (bkz _.gitignore_ hello depo kök). Daha sonra uygulama hizmeti tooconnect tooyour tooconfigure ortam değişkenleri Azure veritabanı'nda MySQL (Önizleme) nasıl veritabanı öğrenin. Ortam değişkenleri ile Merhaba gerekmeyen *.env* uygulama hizmeti dosyasında.
>

### <a name="configure-ssl-certificate"></a>SSL sertifikası yapılandırma

Varsayılan olarak, Azure veritabanı için MySQL istemcilerden gelen SSL bağlantıları zorlar. tooconnect tooyour MySQL veritabanında Azure kullanmalıdır bir _.pem_ SSL sertifikası.

Açık _config/database.php_ ve hello ekleyin _sslmode_ ve _seçenekleri_ parametreler çok`connections.mysql`hello kod aşağıdaki gösterildiği gibi.

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

toolearn nasıl toogenerate bu _certificate.pem_, bkz: [yapılandırma SSL bağlantısı'nda uygulama toosecurely bağlanmak tooAzure veritabanı için MySQL](../mysql/howto-configure-ssl.md).

> [!TIP]
> Merhaba yolu _/ssl/certificate.pem_ işaret tooan varolan _certificate.pem_ hello Git deposu dosyasında. Bu dosya, bu öğreticide kolaylık sağlaması açısından sunulmuştur. En iyi yöntem yürüttükten değil, _.pem_ kaynak denetimine sertifikalar. 
>

### <a name="test-hello-application-locally"></a>Merhaba uygulamayı yerel olarak test etme

Laravel veritabanı geçişler ile Çalıştır _. env.production_ (Önizleme) MySQL için ortam dosya toocreate hello MySQL veritabanınızı Azure veritabanında tablolarda hello gibi. Unutmayın _. env.production_ Azure'da hello bağlantı bilgileri tooyour MySQL veritabanı vardır.

```bash
php artisan migrate --env=production --force
```

_. env.production_ geçerli uygulama anahtarı henüz yok. Merhaba terminal daha yeni bir tane oluşturun.

```bash
php artisan key:generate --env=production --force
```

Merhaba örnek uygulaması ile Çalıştır _. env.production_ hello ortam dosyası olarak.

```bash
php artisan serve --env=production
```

Çok gidin`http://localhost:8000`. Hello sayfa hatasız yüklerse hello PHP uygulaması Azure toohello MySQL veritabanına bağlanıyor.

Bazı görevleri hello sayfasında ekleyin.

![PHP tooAzure veritabanı için MySQL (Önizleme) başarıyla bağlanır.](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

PHP, toostop yazın `Ctrl + C` hello terminal içinde.

### <a name="commit-your-changes"></a>Değişikliklerinizi uygulamak

Git komutları toocommit aşağıdaki hello değişikliklerinizi çalıştırın:

```bash
git add .
git commit -m "database.php updates"
```

Uygulamanızı dağıtılan hazır toobe ' dir.

## <a name="deploy-tooazure"></a>TooAzure dağıtma

Bu adımda, hello MySQL bağlı PHP uygulama tooAzure uygulama hizmeti dağıtın.

### <a name="create-an-app-service-plan"></a>App Service planı oluşturma

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a>Web uygulaması oluşturma

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a>Set hello PHP sürümü

Uygulama hello kümesi hello PHP sürümünü gerektirir hello kullanarak [az webapp yapılandırma kümesi](/cli/azure/webapp/config#set) komutu.

Merhaba aşağıdaki komut hello PHP sürümü too_7.0_ ayarlar.

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a>Veritabanı ayarlarını yapılandırma

Daha önce işaret edildiği gibi App Service'te ortam değişkenlerini kullanma tooyour Azure MySQL veritabanı bağlanabilir.

Ortam değişkenleri olarak ayarladığınız App Service'te _uygulama ayarları_ hello kullanarak [az webapp config appsettings kümesi](/cli/azure/webapp/config/appsettings#set) komutu.

Merhaba aşağıdaki komutu hello uygulama ayarlarını yapılandırır `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, ve `DB_PASSWORD`. Merhaba yer tutucuları değiştirmek  _&lt;uygulamaadı >_ ve  _&lt;mysql_server_name >_.

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

Merhaba PHP kullanabilirsiniz [getenv](http://www.php.net/manual/function.getenv.php) yöntemi tooaccess hello ayarları. Merhaba Laravel kodu kullanan bir [env](https://laravel.com/docs/5.4/helpers#method-env) sarmalayıcı hello PHP üzerinden `getenv`. Örneğin, hello MySQL yapılandırmasında _config/database.php_ hello kod aşağıdaki gibi görünür:

```php
'mysql' => [
    'driver'    => 'mysql',
    'host'      => env('DB_HOST', 'localhost'),
    'database'  => env('DB_DATABASE', 'forge'),
    'username'  => env('DB_USERNAME', 'forge'),
    'password'  => env('DB_PASSWORD', ''),
    ...
],
```

### <a name="configure-laravel-environment-variables"></a>Laravel ortam değişkenlerini yapılandırın

Laravel App Service'te bir uygulama anahtarı gerekir. Uygulama ayarları ile yapılandırabilirsiniz.

Kullanım `php artisan` toogenerate too_.env_ kaydetmeden yeni bir uygulama anahtarı.

```bash
php artisan key:generate --show
```

Merhaba uygulama anahtarı hello App Service web uygulaması hello kullanarak ayarlamak [az webapp config appsettings kümesi](/cli/azure/webapp/config/appsettings#set) komutu. Merhaba yer tutucuları değiştirmek  _&lt;uygulamaadı >_ ve  _&lt;outputofphpartisankey: Oluştur >_.

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

`APP_DEBUG="true"`Merhaba web uygulaması dağıtıldığında Laravel tooreturn hata ayıklama bilgilerini hatayla karşılaştığında söyler. Bir üretim uygulaması çalışırken çok ayarlamak`false`, daha güvenli olduğu.

### <a name="set-hello-virtual-application-path"></a>Merhaba sanal uygulama yolu ayarla

Merhaba sanal uygulama yolu hello web uygulaması için ayarlayın. Bu adım gereklidir çünkü hello [Laravel uygulama yaşam döngüsü](https://laravel.com/docs/5.4/lifecycle) hello başlar _ortak_ hello uygulamanızın kök dizininde yerine dizin. Diğer PHP çerçeveleri, yaşam döngüsünü başlatma hello kök dizininde hello sanal uygulama yolu el ile yapılandırma olmadan çalışabilir.

Hello kullanarak hello sanal uygulama yolu ayarla [az kaynak güncelleştirme](/cli/azure/resource#update) komutu. Hello yerine  _&lt;uygulamaadı >_ yer tutucu.

```azurecli-interactive
az resource update \
    --name web \
    --resource-group myResourceGroup \
    --namespace Microsoft.Web \
    --resource-type config \
    --parent sites/<app_name> \
    --set properties.virtualApplications[0].physicalPath="site\wwwroot\public" \
    --api-version 2015-06-01
```

Varsayılan olarak, Azure App Service hello kök sanal uygulama yolu işaret (_/_) toohello kök dizini hello dağıtılan uygulama dosyaları (_sites\wwwroot_).

### <a name="configure-a-deployment-user"></a>Dağıtım kullanıcısı yapılandırma

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a>Yerel Git dağıtımını yapılandırma

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a>Anında iletme tooAzure Git

Bir Azure uzak tooyour yerel Git deposu ekleyin.

```bash
git remote add azure <paste_copied_url_here>
```

Toohello Azure uzak toodeploy Merhaba PHP uygulaması iletin. Merhaba dağıtım kullanıcının hello oluşturmanın bir parçası daha önce sağlanan hello parola istenir.

```bash
git push azure master
```

Dağıtım sırasında Azure App Service, ilerleme durumunu Git ile iletişim kurar.

```bash
Counting objects: 3, done.
Delta compression using up too8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 291 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'a5e076db9c'.
remote: Running custom deployment command...
remote: Running deployment command...
...
< Output has been truncated for readability >
```

> [!NOTE]
> Merhaba dağıtım işlemi yükleyeceğini karşılaşabilirsiniz [Oluşturucu](https://getcomposer.org/) hello sonunda paketler. Uygulama hizmeti bu otomasyonlara varsayılan dağıtımı sırasında çalışmaz, bu örnek depo üç nedenle ek kendi kök dizin tooenable, dosyalarını:
>
> - `.deployment`-Uygulama hizmeti toorun bu dosya söyler `bash deploy.sh` hello özel dağıtım komut dosyası olarak.
> - `deploy.sh`-hello özel dağıtım komut dosyası. Merhaba dosya gözden geçirirseniz, çalıştığını görürsünüz `php composer.phar install` sonra `npm install`.
> - `composer.phar`-hello Oluşturucu Paket Yöneticisi.
>
> Bu yaklaşım tooadd herhangi adım tooyour Git tabanlı dağıtım tooApp hizmetini kullanabilirsiniz. Daha fazla bilgi için bkz: [özel dağıtım betiği](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).
>

### <a name="browse-toohello-azure-web-app"></a>Toohello Azure web uygulaması Gözat

Çok Gözat`http://<app_name>.azurewebsites.net` ve birkaç görevleri toohello listesine ekleyin.

![Azure uygulama Hizmeti'nde çalışan PHP uygulaması](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

Tebrikler, Azure App Service'te bir veri güdümlü PHP uygulaması çalıştırıyorsanız.

## <a name="update-model-locally-and-redeploy"></a>Modeli yerel olarak güncelleştirin ve yeniden dağıtın

Bu adımda, bir basit değişiklik toohello yaptığınız `task` veri modeli ve webapp hello ve hello güncelleştirme tooAzure yayımlayın.

Merhaba görevler senaryo için bir görev tamamlandı olarak işaretleyebilirsiniz şekilde hello uygulama değiştirin.

### <a name="add-a-column"></a>Bir sütun ekleyin

Hello terminal, hello Git deposu toohello köküne gidin.

Hello için yeni bir veritabanı geçiş oluşturmayı `tasks` tablosu:

```bash
php artisan make:migration add_complete_column --table=tasks
```

Bu komut oluşturulan hello geçiş dosyasının adı hello gösterir. Bu dosyada Bul _veritabanı/geçişler_ ve açın.

Hello yerine `up` koddan hello yöntemiyle:

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

Merhaba önceki kod bir boolean sütun hello ekler `tasks` adlı bir tablo `complete`.

Hello yerine `down` hello geri alma eylemi için kod aşağıdaki hello yöntemiyle:

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

Hello terminal, Laravel veritabanı geçişler toomake hello değişikliği hello yerel veritabanında çalıştırın.

```bash
php artisan migrate
```

Merhaba üzerinde temel [Laravel adlandırma kuralı](https://laravel.com/docs/5.4/eloquent#defining-models), hello modeli `Task` (bkz _app/Task.php_) toohello eşlemeleri `tasks` varsayılan olarak tablo.

### <a name="update-application-logic"></a>Uygulama mantığını güncelleştir

Açık hello *routes/web.php* dosya. Merhaba uygulaması kendi yollar ve iş mantığı buraya tanımlar.

Merhaba dosya Hello sonunda koddan hello ile bir rota ekleyin:

```php
/**
 * Toggle Task completeness
 */
Route::post('/task/{id}', function ($id) {
    error_log('INFO: post /task/'.$id);
    $task = Task::findOrFail($id);

    $task->complete = !$task->complete;
    $task->save();

    return redirect('/');
});
```

Merhaba önceki kod basit güncelleştirme toohello veri modeli hello değerini değiştirerek yapar `complete`.

### <a name="update-hello-view"></a>Merhaba görünümünü güncelleştirme

Açık hello *resources/views/tasks.blade.php* dosya. Hello bulur `<tr>` açma etiketi ve ile değiştirin:

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

Merhaba görev tam olup olmamasına bağlı olarak kod değişiklikleri hello satır rengi önceki hello.

Merhaba sonraki satırda, kod aşağıdaki hello vardır:

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

Merhaba tüm satırı koddan hello ile değiştirin:

```html
<td>
    <form action="{{ url('task/'.$task->id) }}" method="POST">
        {{ csrf_field() }}

        <button type="submit" class="btn btn-xs">
            <i class="fa {{$task->complete ? 'fa-check-square-o' : 'fa-square-o'}}"></i>
        </button>
        {{ $task->name }}
    </form>
</td>
```

Merhaba önceki kod daha önce tanımlanan hello rota başvuran hello Gönder düğmesi ekler.

### <a name="test-hello-changes-locally"></a>Yerel olarak test hello değişiklikleri

Merhaba Git deposu, Hello kök dizinindeki hello geliştirme sunucusu çalıştırın.

```bash
php artisan serve
```

toosee hello görev durumu değişikliği, çok gidin`http://localhost:8000` ve select hello onay kutusu.

![Eklenen onay kutusunu tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

PHP, toostop yazın `Ctrl + C` hello terminal içinde.

### <a name="publish-changes-tooazure"></a>Değişiklikleri tooAzure yayımlama

Hello terminal, Laravel veritabanı geçişler hello üretim bağlantı dizesi toomake hello değişikliği hello Azure veritabanı ile çalıştırın.

```bash
php artisan migrate --env=production --force
```

Git tüm hello değişiklikleri kaydetmek ve hello kod değişiklikleri tooAzure anında iletme.

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

Bir kez hello `git push` tamamlamak ise toohello Azure web uygulaması ve test hello yeni işlevsellik gidin.

![Model ve veritabanı değişikliklerini tooAzure yayımlanan](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

Herhangi bir görevi eklediyseniz bunlar hello veritabanında tutulur. Güncelleştirmeleri toohello veri şeması bırakın mevcut verileri kalır.

## <a name="stream-diagnostic-logs"></a>Akış tanılama günlükleri

Merhaba PHP uygulaması Azure App Service'te çalışırken hello konsol günlükleri yöneltilen tooyour terminal elde edebilirsiniz. Bu şekilde hello aynı tanılama iletileri alabilirsiniz uygulama hatalarını hata ayıklama toohelp.

Akış, kullanım hello toostart günlük [az webapp günlük tail](/cli/azure/webapp/log#tail) komutu.

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

Günlük akış başladıktan sonra bazı web trafiği hello tarayıcı tooget hello Azure web uygulamasında yenileyin. Konsol günlükleri yöneltilen toohello terminal şimdi görebilirsiniz. Konsol günlükleri hemen görmüyorsanız, 30 saniye içinde yeniden kontrol edin.

istediğiniz zaman, akış toostop günlük türü `Ctrl` + `C`.

> [!TIP]
> Bir PHP uygulaması hello standart kullanabilir [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello konsol. Merhaba örnek uygulama bu yaklaşımı kullanır _app/Http/routes.php_.
>
> Bir web çerçevesidir olarak [Laravel kullanan Monolog](https://laravel.com/docs/5.4/errors) hello oturum açma sağlayıcısı olarak. toosee tooget Monolog toooutput toohello konsol iletileri nasıl bkz [PHP: nasıl toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).
>
>

## <a name="manage-hello-azure-web-app"></a>Hello Azure web uygulaması yönetme

Toohello Git [Azure portal](https://portal.azure.com) oluşturduğunuz toomanage hello web uygulaması.

Merhaba sol menüden **uygulama hizmetleri**ve ardından, Azure web uygulamanızın hello adına tıklayın.

![Portal Gezinti tooAzure web uygulaması](./media/app-service-web-tutorial-php-mysql/access-portal.png)

Web uygulamanızın Genel Bakış sayfasını görürsünüz. Burada, Durdur, Başlat, yeniden başlatma, Gözat ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz.

Merhaba soldaki menüden, uygulamanızı yapılandırmak için sayfaları sağlar.

![Azure portalında App Service sayfası](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:

> [!div class="checklist"]
> * Azure üzerinde MySQL veritabanı oluşturma
> * PHP uygulama tooMySQL Bağlan
> * Merhaba uygulama tooAzure dağıtma
> * Merhaba veri modeli güncelleştirmek ve hello uygulama yeniden dağıtın
> * Azure Stream tanılama günlükleri
> * Merhaba uygulamada hello Azure portalı Yönet

İlerlemek toohello sonraki öğretici toolearn nasıl toomap özel DNS ad tooa web uygulaması.

> [!div class="nextstepaction"]
> [Harita bir var olan özel DNS adı tooAzure Web uygulamaları](app-service-web-tutorial-custom-domain.md)
