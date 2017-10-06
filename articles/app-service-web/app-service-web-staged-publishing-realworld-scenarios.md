---
title: "web uygulamanız için etkili bir şekilde aaaUse DevOps ortamları | Microsoft Docs"
description: "Nasıl yukarı tooset toouse dağıtım yuvalarını öğrenin ve uygulamanız için birden çok geliştirme ortamlarını yönetebilir"
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 16a594dc-61f5-4984-b5ca-9d5abc39fb1e
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 61a552e735a4ad9769b661d7c988744074ba2962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-devops-environments-effectively-for-your-web-apps"></a>DevOps ortamları etkili bir şekilde web uygulamaları için kullanın
Bu makale size nasıl gösterir tooset ayarlama ve birden çok sürümü, uygulamanızın, geliştirme, hazırlama, kalite güvence (QA) ve üretim gibi çeşitli ortamlarda olduğunda web uygulama dağıtımlarını yönetin. Her bir sürümü, uygulamanızın bir geliştirme ortamı hello belirli amacı, dağıtım işleminiz için kabul edilebilir. Örneğin, hello değişiklikleri tooproduction sokmadan önce geliştiriciler hello QA ortamı tootest hello hello uygulama kalitesini kullanabilir.
Birden çok geliştirme ortamı bir sınama tootrack kod gerektiğinden kaynakların (hesaplama, web uygulaması, veritabanı, önbellek, vb.) yönetmek ve kod ortamlar genelinde dağıtmak olabilir.

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a>Bir üretim dışı ortamını (aşaması, geliştirme, QA) ayarlama
Bir üretim web uygulaması çalışır durumda sonra hello sonraki toocreate bir üretim ortamı dışındaki bir adımdır. toouse dağıtım yuvaları, hello standart veya Premium Azure uygulama hizmeti planı modunda çalışır durumda olduğundan emin olun. Dağıtım yuvaları, kendi ana bilgisayar adları olan canlı web uygulamalardır. Web uygulaması içerik ve yapılandırma öğeleri hello üretim yuvası da dahil olmak üzere iki dağıtım yuvası arasında değişiklik yapılabilir. Uygulama tooa dağıtım yuvası dağıttığınızda, aşağıdaki faydaları hello alın:

- Merhaba uygulama hello üretim yuvasıyla takas önce değişiklikleri hazırlık dağıtım yuvasındaki web uygulamasında tooa doğrulayabilirsiniz.
- Bir web uygulaması tooa yuvası ilk Dağıt ve üretime takas hello yuvası tüm örneklerini üretime takas önce warmed. Bu işlem, web uygulamanızı dağıtırken kapalı kalma süresini ortadan kaldırır. Merhaba trafik yeniden yönlendirmesi sorunsuzdur ve hiçbir istek tooswap işlemleri bırakıldı. tooautomate tüm bu iş akışını yapılandırmak [otomatik takas](web-sites-staged-publishing.md#configure-auto-swap) zaman öncesi takas doğrulama gerekli değildir.
- Değiştirme işleminden sonra önceden hazırlanmış hello web uygulaması şimdi sahip hello yuvası hello önceki üretim web uygulamasına sahiptir. Beklendiği gibi hello üretim yuvasına hello değişiklikleri varsa, hello gerçekleştirebilirsiniz aynı, "bilinen iyi en son" hemen tooget takas web app arka.

Hazırlık dağıtım yuvasındaki yukarı tooset bkz [hazırlık Azure App Service'deki web uygulamaları için ortamları ayarlama](web-sites-staged-publishing.md). Her ortam kaynakları kendi kümesini içermelidir. Web uygulamanız bir veritabanı kullanıyorsa, örneğin, daha sonra hem üretim hem de web uygulamaları hazırlama farklı veritabanları kullanmanız gerekir. Veritabanı, depolama veya önbellek tooset gibi hazırlama geliştirme ortamı kaynakları hazırlama geliştirme ortamınızı ekleyin.

## <a name="examples-of-using-multiple-development-environments"></a>Birden çok geliştirme ortamı kullanma örnekleri
Herhangi bir projenin kaynak kodu yönetimi en az iki ortamlarla izlemelidir: geliştirme ve üretim. İçerik yönetim sistemleri (CMSs), uygulama çerçeveleri, vb. kullanırsanız Merhaba uygulaması özelleştirme olmadan bu senaryo desteklemeyebilir. Bu planlıyorsanız, bazı hello aşağıdaki bölümlerde açıklanan hello popüler uygulamayı için geçerlidir. CMS/çerçeveleri ile gibi çalışırken çok soruların toomind getirir:

- Nasıl, hello içerik farklı ortamlara başlama?
- Hangi dosyaların framework sürüm güncelleştirmelerini etkilemeden değiştirebilir miyim?
- Ortam başına yapılandırmaları nasıl yönettiğiniz?
- Modüller, eklenti ve hello çekirdek framework sürüm güncelleştirmelerini nasıl yönettiğiniz?

Projeniz için birden çok ortamları ayarlama birçok yolu tooset vardır. Merhaba Aşağıdaki örnekler ilgili her uygulama için bir yöntemi gösterir.

### <a name="wordpress"></a>WordPress
Bu bölümde, nasıl tooset kullanarak bir dağıtım iş akışı için WordPress yuvası öğreneceksiniz. WordPress, çoğu CMS çözümleri gibi özelleştirme olmadan birden fazla geliştirme ortamları desteklemez. Azure App Service Web Apps özelliğini Hello kodunuzu dışında kolay toostore yapılandırma ayarları yapmanız birkaç özelliklere sahiptir.

1. Hazırlama yuvası oluşturmadan önce uygulama kodu toosupport birden çok ortamı ayarlayın. toosupport birden çok ortamları WordPress içinde tooedit gerek `wp-config.php` yerel geliştirme üzerinde web uygulaması ve kod hello dosya hello başında aşağıdaki hello ekleyin. Bu işlem hello Seçili ortamı tabanlı uygulama toopick hello doğru yapılandırmanıza olanak sağlar.

    ```
    // Support multiple environments
    // set hello config file based on current environment
    if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) {
    // local development
     $config_file = 'config/wp-config.local.php';
    }
    elseif ((strpos(getenv('WP_ENV'),'stage') !== false) || (strpos(getenv('WP_ENV'),'prod' )!== false ))
    //single file for all azure development environments
     $config_file = 'config/wp-config.azure.php';
    }
    $path = dirname(__FILE__). '/';
    if (file_exists($path. $config_file)) {
    // include hello config file if it exists, otherwise WP is going toofail
    require_once $path. $config_file;
    ```

2. Adlı web uygulama kökü altındaki bir klasör oluşturun `config`ve hello ekleyin `wp-config.azure.php` ve `wp-config.local.php` Azure ortamı ve yerel ortamı sırasıyla temsil dosyaları.

3. Merhaba aşağıdakileri kopyalayın `wp-config.local.php`:

    ```
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

    define('DB_NAME', 'yourdatabasename');

    /** MySQL database username */
    define('DB_USER', 'yourdbuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'yourpassword');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    /**
     * For developers: WordPress debugging mode.
     * * Change this tootrue tooenable hello display of notices during development.
     * It is strongly recommended that plugin and theme developers use WP_DEBUG
     * in their development environments.
     */
    define('WP_DEBUG', true);

    //Security key settings
    define('AUTH_KEY', 'put your unique phrase here');
    define('SECURE_AUTH_KEY','put your unique phrase here');
    define('LOGGED_IN_KEY','put your unique phrase here');
    define('NONCE_KEY', 'put your unique phrase here');
    define('AUTH_SALT', 'put your unique phrase here');
    define('SECURE_AUTH_SALT', 'put your unique phrase here');
    define('LOGGED_IN_SALT', 'put your unique phrase here');
    define('NONCE_SALT', 'put your unique phrase here');

    /**
     * WordPress Database Table prefix.
     *
     * You can have multiple installations in one database if you give each a unique
     * prefix. Only numbers, letters, and underscores please!
     */
    $table_prefix = 'wp_';
    ```

    Merhaba önceki kodda gösterildiği gibi Hello güvenlik anahtarları ayarlama izinsiz giriş gelen web uygulamanızı tooprevent Yardım, benzersiz değerleri kullanın. Merhaba kodda belirtilen güvenlik anahtarlarını toogenerate hello dize ihtiyacınız yoksa, şunları yapabilirsiniz [gidin toohello otomatik Oluşturucu](https://api.wordpress.org/secret-key/1.1/salt) toocreate yeni anahtar/değer çiftleri.

4. Kopya hello aşağıdaki kod `wp-config.azure.php`:

    ```    
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

    define('DB_NAME', getenv('DB_NAME'));

    /** MySQL database username */
    define('DB_USER', getenv('DB_USER'));

    /** MySQL database password */
    define('DB_PASSWORD', getenv('DB_PASSWORD'));

    /** MySQL hostname */
    define('DB_HOST', getenv('DB_HOST'));

    /**
    * For developers: WordPress debugging mode.
    *
    * Change this tootrue tooenable hello display of notices during development.
    * It is strongly recommended that plugin and theme developers use WP_DEBUG
    * in their development environments.
    * Turn on debug logging tooinvestigate issues without displaying tooend user. For WP_DEBUG_LOG to
    * do anything, WP_DEBUG must be enabled (true). WP_DEBUG_DISPLAY should be used in conjunction
    * with WP_DEBUG_LOG so that errors are not displayed on hello page */

    */
    define('WP_DEBUG', getenv('WP_DEBUG'));
    define('WP_DEBUG_LOG', getenv('TURN_ON_DEBUG_LOG'));
    define('WP_DEBUG_DISPLAY',false);

    //Security key settings
    /** If you need toogenerate hello string for security keys mentioned above, you can go hello automatic generator toocreate new keys/values: https://api.wordpress.org/secret-key/1.1/salt **/
    define('AUTH_KEY',getenv('DB_AUTH_KEY'));
    define('SECURE_AUTH_KEY', getenv('DB_SECURE_AUTH_KEY'));
    define('LOGGED_IN_KEY', getenv('DB_LOGGED_IN_KEY'));
    define('NONCE_KEY', getenv('DB_NONCE_KEY'));
    define('AUTH_SALT', getenv('DB_AUTH_SALT'));
    define('SECURE_AUTH_SALT', getenv('DB_SECURE_AUTH_SALT'));
    define('LOGGED_IN_SALT',  getenv('DB_LOGGED_IN_SALT'));
    define('NONCE_SALT',  getenv('DB_NONCE_SALT'));

    /**
    * WordPress Database Table prefix.
    *
    * You can have multiple installations in one database if you give each a unique
    * prefix. Only numbers, letters, and underscores please!
    */
    $table_prefix = getenv('DB_PREFIX');
    ```

#### <a name="use-relative-paths"></a>Göreli yollar kullanın
Son bir şey tooconfigure hello WordPress uygulamasında göreli yollar ' dir. WordPress URL bilgileri hello veritabanında depolar. Bu depolama bir ortam tooanother taşıma içerikten daha zor hale getirir. Yerel toostage veya aşama tooproduction ortamları taşımak her zaman tooupdate hello veritabanınızın olması gerekir. tooreduce hello kullan hello bir ortam tooanother dağıtmak her zaman bir veritabanı dağıtımı ile neden sorunları riskini [göreli kök bağlantılar eklentisi](https://wordpress.org/plugins/root-relative-urls/), hangi hello WordPress Yöneticisi'ni kullanarak yükleyebilirsiniz Pano.

Girişleri tooyour aşağıdaki hello eklemek `wp-config.php` hello önce dosyayı `That's all, stop editing!` Açıklama:

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

Merhaba eklentisi hello aracılığıyla etkinleştirme `Plugins` WordPress yönetici Pano menüde. WordPress uygulaması için sabit bağlantı ayarlarınızı kaydedin.

#### <a name="hello-final-wp-configphp-file"></a>Merhaba son `wp-config.php` dosyası
WordPress çekirdek güncelleştirmeleri değil etkiler, `wp-config.php`, `wp-config.azure.php`, ve `wp-config.local.php` dosyaları. Merhaba son sürümünü işte `wp-config.php` dosyası:

```
<?php
/**
 * hello base configurations of hello WordPress.
 *
 * This file has hello following configurations: MySQL settings, Table Prefix,
 * Secret Keys, and ABSPATH. You can find more information by visiting
 *
 * Codex page. You can get hello MySQL settings from your web host.
 *
 * This file is used by hello wp-config.php creation script during the
 * installation. You don't have toouse hello web web app, you can just copy this file
 * too"wp-config.php" and fill in hello values.
 *
 * @package WordPress
 */

// Support multiple environments
// set hello config file based on current environment
if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) { // local development
  $config_file = 'config/wp-config.local.php';
}
elseif ((strpos(getenv('WP_ENV'),'stage') !== false) ||(strpos(getenv('WP_ENV'),'prod' )!== false )){
  $config_file = 'config/wp-config.azure.php';
}


$path = dirname(__FILE__). '/';
if (file_exists($path. $config_file)) {
  // include hello config file if it exists, otherwise WP is going toofail
  require_once $path. $config_file;
}

/** Database Charset toouse in creating database tables. */
define('DB_CHARSET', 'utf8');

/** hello Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/* That's all, stop editing! Happy blogging. */

define('WP_HOME', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_CONTENT_URL', '/wp-content');
define('DOMAIN_CURRENT_SITE', $_SERVER['HTTP_HOST']);

/** Absolute path toohello WordPress directory. */
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__). '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH. 'wp-settings.php');
```

#### <a name="set-up-a-staging-environment"></a>Hazırlama ortamını ayarlama
1. Azure aboneliğiniz üzerinde çalışan bir WordPress web uygulaması zaten varsa toohello oturum [Azure portal](http://portal.azure.com), ve ardından tooyour WordPress web uygulamasına gidin. WordPress web uygulaması yoksa, hello Azure Marketi birinden oluşturabilirsiniz. toolearn daha, fazla [Azure App Service'te bir WordPress web uygulaması oluşturma](web-sites-php-web-site-gallery.md).
Tıklatın **ayarları** > **dağıtım yuvası** > **Ekle** toocreate hello ada sahip bir dağıtım yuvası *aşama*. Bir dağıtım yuvası, daha önce oluşturduğunuz hello birincil web uygulaması olarak aynı kaynakları paylaşımları hello başka bir web uygulamasıdır.

    ![Aşama dağıtım yuvası oluşturma](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. Başka bir MySQL veritabanı deyin Ekle `wordpress-stage-db`, tooyour kaynak grubu, `wordpressapp-group`.

    ![MySQL veritabanı tooresource grubu Ekle](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. Merhaba, aşama dağıtım yuvası toopoint toohello yeni bir veritabanı için bağlantı dizelerini güncelleştirmek `wordpress-stage-db`. Üretim web uygulamanız `wordpressprodapp`ve web uygulaması hazırlama `wordpressprodapp-stage`, gereken noktası toodifferent veritabanları.

#### <a name="configure-environment-specific-app-settings"></a>Ortama özgü uygulaması ayarlarını yapılandır
Geliştiriciler saklayabilir anahtar/değer çiftlerinin dize Azure'da hello yapılandırma bilgileri, adlı bir parçası olarak **uygulama ayarları**, bir web uygulaması ile ilişkili. Çalışma zamanında web uygulamaları otomatik olarak bu değerleri almak ve bunları web uygulamanızda çalışan kullanılabilir toocode getirin. Güvenlik açısından bakıldığında, olduğundan iyi tarafı avantajı parolalar dahil veritabanı bağlantı dizeleri gibi hassas bilgileri hiçbir zaman görünmesini bir dosyada düz metin olarak gibi `wp-config.php`.

Paragrafları aşağıdaki hello anlatılmıştır, bu işlem, dosya değişiklikleri ve hello WordPress uygulaması için veritabanı değişikliklerini içerdiği için yararlıdır:

* WordPress sürüm yükseltme
* Yeni Ekle veya Düzenle veya eklentileri yükseltme
* Yeni Ekle veya Düzenle veya Temalar yükseltme

Uygulama ayarlarını yapılandırın:

* Veritabanı bilgileri
* Kapatma açık/kapalı WordPress günlüğe kaydetme
* WordPress güvenlik ayarları

![Wordpress web uygulaması için uygulama ayarları](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

Uygulama ayarları üretim web app ve hazırlama yuvası için aşağıdaki hello eklediğinizden emin olun. Merhaba üretim web uygulaması ve hazırlama web uygulaması farklı veritabanları kullandığını unutmayın.

1. Clear hello **yuva ayarı** WP_ENV dışındaki tüm hello ayarları parametrelerden onay kutusunu. Bu işlem, web uygulaması, dosya içeriğini ve veritabanını hello yapılandırma değiştireceksiniz. Varsa **yuva ayarı** olan işaretli hello web uygulamanızın uygulama ayarlarının ve bağlantı dizesini yapılandırma olacak *değil* ortamlar genelinde yapılırken taşıma bir **takas** işlemi. Var olan veritabanı değişiklikleri üretim web uygulamanız bölün değil.

2. Merhaba yerel geliştirme ortamı web uygulama toohello aşama web uygulaması ve veritabanı WebMatrix veya tercih ettiğiniz, FTP, Git veya PhpMyAdmin gibi araçları kullanarak dağıtın.

    ![WordPress web uygulaması için Web matris Yayımla iletişim kutusu](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. Gözat ve hazırlama web uygulamanızı test edin. Merhaba teması hello web uygulaması, güncelleştirilmiş toobe bulunduğu bir senaryoyu göz önünde bulundurularak, web uygulaması hazırlama hello aşağıda verilmiştir.

    ![Web uygulaması yuvaları takas önce hazırlama Gözat](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. Tüm görünüyorsa iyi, hello tıklatın **takas** üzerinde hazırlama web uygulama toomove içerik toohello üretim ortamınıza düğmesi. Bu durumda, hello web app ve hello veritabanı sırasında ortamlar üzerinde takas her **takas** işlemi.

    ![Önizleme değişiklikleri için WordPress değiştirme](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > Senaryonuz tooonly zorlama dosyaların (veritabanı güncelleştirmeleri) gerekiyorsa, ardından denetleyin **yuva ayarı** tüm hello veritabanıyla ilgili için *uygulama ayarları* ve *bağlantı dizeleri ayarları*hello içinde **Web uygulaması ayarları** dikey penceresinde hello hello yapmadan önce Azure portalı içinde **takas**. Bunu yaptığınızda bu durumda, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER ve varsayılan bağlantı dizesi ayarlarının Önizleme değişiklikleri gösterilmesi gerekir olmayan bir **takas**. Şu anda hello tamamlandığında **takas** işlemi, WordPress web uygulaması Hello ifadesini sahip hello yalnızca dosyalar güncelleştirir.
    >
    >

    Bunu yaptığınızda önce bir **takas**, hello üretim WordPress web uygulaması aşağıdadır.
    ![Üretim web uygulaması yuvaları takas önce](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)

    Merhaba sonra **takas** işlemi, hello tema üretim web uygulamanız güncelleştirilmiştir.

    ![Üretim web uygulaması yuvaları takas sonra](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. Geri tooroll gerektiğinde toohello üretim web gidebilirsiniz **uygulama ayarları**, hello tıklatıp **takas** düğmesini tooswap hello web app ve üretim toostaging yuvası veritabanından. Veritabanı değişiklikleri birlikte olup olmadığını unutmayın bir **takas** işlemi sonra hello web uygulaması hazırlama tooyour dağıttığınız sonraki sefer hazırlama web uygulamanız için toodeploy hello veritabanı değişiklikleri toohello geçerli veritabanınızın olması gerekir. Merhaba geçerli veritabanı hello önceki üretim veritabanını veya hello aşama veritabanını olabilir.

#### <a name="summary"></a>Özet
Aşağıda, bir veritabanı sahip herhangi bir uygulama için genelleştirilmiş bir işlemdir:

1. Merhaba uygulaması yerel ortamınıza yükleyin.
2. Ortama özgü yapılandırmaları (yerel ve Azure Web Apps) içerir.
3. Web uygulamaları için hazırlama ve üretim ortamları ayarlama.
4. Zaten Azure üzerinde çalışan bir üretim uygulamanız varsa, üretim içerik (dosyalar/kod ve veritabanı) toolocal ve hazırlama ortamları eşitleyin.
5. Uygulamanızı yerel ortamınızda geliştirin.
6. Üretim web uygulamanız Bakım veya kilitli modu altında yerleştirin ve üretim toostaging ve geliştirme ortamlarını veritabanı içerikten eşitleyin.
7. Hazırlama ortamı ve test toohello dağıtın.
8. Tooproduction ortamı dağıtın.
9. 4 ile 6 arasındaki adımları yineleyin.

### <a name="umbraco"></a>Umbraco
Bu bölümde, hello Umbraco CMS özel modülü toodeploy birden çok DevOps ortamlar genelinde nasıl kullandığını öğreneceksiniz. Bu örnekte, farklı bir yaklaşım toomanaging birden çok geliştirme ortamı sağlar.

[Umbraco CMS](http://umbraco.com/) birçok geliştiriciler tarafından kullanılan bir popüler .NET CMS çözümüdür. Merhaba sağlar [Courier2](http://umbraco.com/products/more-add-ons/courier-2) geliştirme toostaging tooproduction ortamlarından modülü toodeploy. WebMatrix veya Visual Studio'yu kullanarak kolayca bir Umbraco CMS web uygulaması için bir yerel geliştirme ortamı oluşturabilirsiniz.

- [Visual Studio ile bir Umbraco web uygulaması oluşturma](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [WebMatrix ile bir Umbraco web uygulaması oluşturma](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

Her zaman tooremove hello unutmayın `install` , uygulamanızın altında bir klasör ve hiçbir zaman toostage veya üretim web uygulamaları karşıya yükleme. Bu öğretici, WebMatrix kullanır.

#### <a name="set-up-a-staging-environment"></a>Hazırlama ortamını ayarlama
1. Bir dağıtım yuvası Merhaba Umbraco CMS web uygulaması zaten varsa ve çalıştırma Umbraco CMS web uygulaması, daha önce belirtildiği gibi oluşturun. Bunu yapmazsanız, hello Market birinden oluşturabilirsiniz.
2. Merhaba bağlantı dizesi, aşama dağıtım yuvası toopoint toohello yeni güncelleştirme **umbraco aşama db** veritabanı. Üretim web uygulaması (umbraositecms-1) ve hazırlama web uygulaması (umbracositecms-1-aşama) *gerekir* noktası toodifferent veritabanları.

    ![Yeni hazırlama veritabanı ile web uygulaması hazırlama için kullanılan bağlantı dizesi güncelleştir](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. Tıklatın **alma yayımlama ayarları** hello dağıtım yuvası için **aşama**. Bu işlem, Visual Studio veya WebMatrix toopublish uygulamanızın hello yerel geliştirme web uygulama toohello Azure web uygulamasından gerektirdiği tüm hello bilgileri depolayan bir yayımlama ayarları dosyası indirir.

    ![Get yayımlama hello web uygulaması hazırlama ayarı](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. Yerel geliştirme web uygulamanızı WebMatrix veya Visual Studio'da açın. Bu öğretici, WebMatrix kullanır. Öncelikle, tooimport hello gerekir yayımlama ayarları dosyası hazırlama web uygulamanız için.

    ![Web Matrix kullanarak Umbraco yayımlama ayarlarını içeri aktarma](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. Merhaba iletişim kutusunda değişiklikleri gözden geçirin ve, yerel web uygulaması tooyour Azure web uygulaması dağıtma *umbracositecms 1 aşama*. Tooyour hazırlama web doğrudan uygulama dosyaları dağıttığınızda, hello dosyalarında atlayacak `~/app_data/TEMP/` hello aşama web uygulaması ilk çalıştırıldığında bu dosyalar yeniden oluşturulacak olmadığından klasör başlatıldı. Merhaba atlayın `~/app_data/umbraco.config` de yeniden oluşturulacak dosya.

    ![Web Matristeki Yayımla değişiklikleri gözden geçirin](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. Merhaba Umbraco yerel web uygulama toohello hazırlama web uygulaması başarıyla yayımladıktan sonra tooyour hazırlama web uygulaması göz atın ve sorunları çıkışı birkaç testleri toorule çalıştırın.

#### <a name="set-up-hello-courier2-deployment-module"></a>Merhaba Courier2 dağıtım modülünü kurun
Merhaba ile [Courier2](http://umbraco.com/products/more-add-ons/courier-2) modülü, yalnızca toopush içerik, stil sayfaları ve bir hazırlama web uygulama tooa üretim web uygulaması geliştirme modüllerden tıklayabilir. Bu işlem bir güncelleştirme dağıttığınızda üretim web uygulamanız çiğnemekten hello riskini azaltır.
Merhaba Courier2 için bir lisans satın `*.azurewebsites.net` etki alanı ve özel etki alanınızı (örneğin http://abc.com). Merhaba lisans satın aldıktan sonra lisans yer hello indirilen (. Lisans Sözleşmesi dosyası) hello içinde `bin` klasör.

![Bin klasörü altındaki açılan lisans dosyası](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. [Merhaba Courier2 paketini indirin](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/). Tooyour aşama web uygulamasında, deyin http://umbracocms-site-stage.azurewebsites.net/umbraco işaretini tıklatın hello **Geliştirici** menüsüne ve ardından **paketleri** > **yükleyin Yerel Paket**.

    ![Umbraco paketi yükleyicisi](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. Merhaba Courier2 paket hello yükleyicisini kullanarak yükleyin.

    ![Paketi courier modülü için yükleme](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. tooconfigure hello paket tooupdate hello courier.config dosya hello altında ihtiyacınız **Config** klasör, web uygulamanızın.

    ```xml
    <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="production web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1.azurewebsites.net</url>
          <user>0</user>
          <!--<login>user@email.com</login> -->
          <!-- <password>user_password</password>-->
          <!-- <passwordEncoding>Clear</passwordEncoding>-->
          </repository>
     </repositories>
     ```

4. Altında `<repositories>`, Merhaba, üretim site URL'si ve kullanıcı bilgilerini girin.
    Merhaba varsayılan Umbraco üyelik sağlayıcısı kullanıyorsanız, hello yönetim kullanıcının hello kimliği hello ekleyin &lt;kullanıcı&gt; bölümü.
    Özel bir Umbraco üyelik sağlayıcısı kullanıyorsanız `<login>`,`<password>` hello Courier2 modülü tooconnect toohello üretim sitedeki.
    Daha fazla ayrıntı için [hello Courier2 modülü için hello belgelerini gözden geçirin](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).

5. Benzer şekilde, üretim sitenizde hello Courier2 modülünü yüklemek ve aşağıda gösterildiği gibi ilgili courier.config dosyasında toopoint toohello aşama web uygulaması yapılandırın.

    ```xml
     <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="Stage web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1-stage.azurewebsites.net</url>
          <user>0</user>
          </repository>
     </repositories>
    ```

6. Merhaba tıklatın **Courier2** sekmesinde hello Umbraco CMS web uygulaması Pano ve ardından **konumları**. Bölümünde belirtildiği gibi hello depo adını görmeniz gerekir `courier.config`. Üretim ve hazırlama web uygulamaları üzerinde bu işlemi yapabilirsiniz.

    ![Görünüm hedef web uygulama havuzu](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. toohello üretim siteler, hazırlama hello toodeploy içerikten Git çok**içerik**ve varolan bir sayfayı seçebilir veya yeni bir sayfa oluşturun. Varolan bir sayfayı hello sayfasının hello başlığını olduğu my web uygulamasından seçecektir **başlarken – yeni**ve ardından **kaydetmek ve yayımlamak**.

    ![Sayfasının başlığını değiştirme ve yayımlama](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. Sağ hello tüm hello Seçenekleri sayfası tooview değiştirdi. Tıklatın **Courier** tooopen hello **dağıtım** iletişim kutusu. Tıklatın **dağıtma** tooinitiate dağıtım.

    ![Courier modülü dağıtım iletişim](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. Merhaba değişiklikleri gözden geçirin ve ardından **devam**.

    ![Courier modülü dağıtım iletişim değişiklikleri gözden geçir](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    Merhaba dağıtım günlüğü hello dağıtım başarılı olup olmadığını gösterir.

     ![Courier modülden dağıtım günlüklerini görüntüle](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. Merhaba değişiklikler yansıtılır varsa, üretim web uygulama toosee göz atın.

     ![Üretim web uygulamasına göz atın](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

toolearn nasıl toouse Courier, gözden geçirme hello belgeleri hakkında daha fazla bilgi.

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a>Nasıl tooupgrade hello Umbraco CMS sürümü
Courier Umbraco CMS tooanother bir sürümünden yükseltme Yardımı. Bir Umbraco CMS sürümüne yükselttiğinizde, özel modüller veya iş ortakları modüllerden uyumsuzluklar denetleyin ve Umbraco çekirdek kitaplıkları hello gerekir. En iyi uygulamalar şunlardır:

* Yükseltmeden önce her zaman, web uygulaması ve veritabanı yedekleme. Azure Web uygulamaları üzerinde hello yedekleme özelliğini kullanarak, Web siteleri için Otomatik yedekler ayarlamak ve hello geri yükleme özelliğini kullanarak gerekirse sitenize geri yükleyin. Daha fazla ayrıntı için bkz: [nasıl web uygulamanızı yedekleme tooback](web-sites-backup.md) ve [nasıl toorestore web uygulamanızı](web-sites-restore.md).
* İş ortakları paketlerinden yükseltme yapıyorsanız hello sürümüyle uyumlu olup olmadığını denetleyin. Merhaba paketin üzerinde sayfa yükleme, Umbraco CMS sürümüyle hello proje uyumluluğu gözden geçirin.

Nasıl hakkında daha fazla ayrıntı için tooupgrade web uygulamanızı yerel olarak [hello genel yükseltme yönergelere bakın](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).

Yerel geliştirme sitenizi yükselttikten sonra web uygulaması hazırlama hello değişiklikleri toohello yayımlayın. Uygulamanızı test edin. Tüm görünüyorsa iyi, hello kullanın **takas** tooswap hazırlama sitesi toohello üretim web uygulamanız düğmesine tıklayın. Merhaba kullandığınızda **takas** işlemi, web uygulamanızın yapılandırmasında etkilenecek hello değişiklikleri görüntüleyebilirsiniz. Bu **takas** işlemi hello web uygulamaları ve veritabanları ile değiştirir. Merhaba sonra **takas**hello üretim web uygulaması olacak noktası toohello umbraco aşama db veritabanı ve hazırlama web uygulaması olacak noktası tooumbraco üretim db veritabanı hello.

![Umbraco CMS dağıtmak için Önizleme değiştirme](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

Merhaba web app ve hello veritabanı takas avantajları şunlardır:

* Web uygulamanızı başka ile toohello önceki sürümünü geri alabilirsiniz **takas** herhangi bir uygulama sorun varsa.
* Yükseltme için toodeploy dosyaları ve web uygulama toohello üretim web uygulaması hazırlama hello veritabanlarından ve veritabanını gerekir. Dosyaları ve veritabanları dağıttığınızda pek çok yanlış gidebilirsiniz. Hello kullanarak **takas** özelliği yuvaları biz yükseltme sırasında kapalı kalma süresini kısaltabilir ve değişiklikleri dağıtırken oluşabilecek hatalar hello riskini azaltır.
* Yapabileceğiniz **A / B testi** hello kullanarak [üretimde test](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) özelliği.

Burada özel modüller benzer tooUmbraco Courier modülü toomanage dağıtımı ortamlar genelinde oluşturabileceğiniz hello platform esnekliğini hello Bu örnek gösterir.

## <a name="references"></a>Başvurular
[Azure App Service ile Çevik Yazılım Geliştirme](app-service-agile-software-development.md)

[Hazırlık ortamları için Azure App Service'te web uygulamalarını ayarlama](web-sites-staged-publishing.md)

[Nasıl tooblock web erişim toonon üretim dağıtım yuvaları](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
