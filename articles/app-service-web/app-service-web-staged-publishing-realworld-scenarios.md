---
title: "Web uygulamanız için etkili bir şekilde kullanan DevOps ortamlar | Microsoft Docs"
description: "Dağıtım yuvaları ayarlamak ve uygulamanız için birden çok geliştirme ortamı yönetmek için nasıl kullanılacağını öğrenin"
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
ms.openlocfilehash: 25248411659f6c7b2e386e310428c365c44ea2e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-devops-environments-effectively-for-your-web-apps"></a>DevOps ortamları etkili bir şekilde web uygulamaları için kullanın
Bu makalede ayarlama ve birden çok sürümü, uygulamanızın, geliştirme, hazırlama, kalite güvence (QA) ve üretim gibi çeşitli ortamlarda olduğunda web uygulama dağıtımlarını yönetin gösterilmektedir. Her bir sürümü, uygulamanızın bir geliştirme ortamı, dağıtım işlemi belirli amaç için kabul edilebilir. Örneğin, geliştiriciler, QA ortamı bunlar değişiklikleri üretime sokmadan önce uygulama kalitesini test etmek için kullanabilirsiniz.
Kod izlemek, kaynakların (hesaplama, web uygulaması, veritabanı, önbellek, vb.) yönetmek ve kod ortamlar genelinde dağıtmak gerektiğinden birden çok geliştirme ortamlarını zor olabilir.

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a>Bir üretim dışı ortamını (aşaması, geliştirme, QA) ayarlama
Bir üretim web uygulaması çalışır durumda sonra sonraki adım bir üretim ortamı dışındaki oluşturmaktır. Dağıtım yuvası kullanmak için standart veya Premium Azure uygulama hizmeti planı modunda çalışır durumda olduğundan emin olun. Dağıtım yuvaları, kendi ana bilgisayar adları olan canlı web uygulamalardır. Web uygulaması içerik ve yapılandırma öğeleri üretim yuvası da dahil olmak üzere iki dağıtım yuvası arasında değişiklik yapılabilir. Bir dağıtım yuvası uygulamanıza dağıttığınızda, aşağıdaki faydaları alın:

- Uygulamayı, üretim yuvası takas önce hazırlık dağıtım yuvasındaki web uygulamasında değişiklikler doğrulayabilirsiniz.
- Bir web uygulaması yuvası için ilk dağıtma ve üretim ortamına takas yuvası tüm örneklerini üretime takas önce warmed. Bu işlem, web uygulamanızı dağıtırken kapalı kalma süresini ortadan kaldırır. Trafik yeniden yönlendirmesi sorunsuzdur ve değiştirme işlemleri nedeniyle hiçbir istek bırakılır. Bu iş akışının tamamı otomatikleştirmek için yapılandırma [otomatik takas](web-sites-staged-publishing.md#configure-auto-swap) zaman öncesi takas doğrulama gerekli değildir.
- Değiştirme işleminden sonra önceden hazırlanmış web uygulaması şimdi sahip yuvası önceki üretim web uygulamasına sahiptir. Beklendiği gibi üretim yuvasına değişiklikleri varsa, "bilinen son iyi" web almak için uygulama geri hemen aynı değiştirme işlemini gerçekleştirebilirsiniz.

Hazırlık dağıtım yuvasındaki ayarlamak için bkz: [hazırlık Azure App Service'deki web uygulamaları için ortamları ayarlama](web-sites-staged-publishing.md). Her ortam kaynakları kendi kümesini içermelidir. Web uygulamanız bir veritabanı kullanıyorsa, örneğin, daha sonra hem üretim hem de web uygulamaları hazırlama farklı veritabanları kullanmanız gerekir. Veritabanı, depolama veya hazırlama geliştirme ortamınızı ayarlamak için önbellek gibi hazırlama geliştirme ortamı kaynakları ekleyin.

## <a name="examples-of-using-multiple-development-environments"></a>Birden çok geliştirme ortamı kullanma örnekleri
Herhangi bir projenin kaynak kodu yönetimi en az iki ortamlarla izlemelidir: geliştirme ve üretim. İçerik yönetim sistemleri (CMSs), uygulama çerçeveleri, vb. kullanırsanız uygulamanın bu senaryo özelleştirme olmadan desteklemeyebilir. Bu planlıyorsanız, aşağıdaki bölümlerde açıklanan popüler uygulamayı bazıları için geçerlidir. CMS/çerçeveleri ile gibi çalışırken soruları birçok aklınıza getirir:

- Nasıl, içeriği farklı ortamlara başlama?
- Hangi dosyaların framework sürüm güncelleştirmelerini etkilemeden değiştirebilir miyim?
- Ortam başına yapılandırmaları nasıl yönettiğiniz?
- Modüller, eklenti ve çekirdek framework sürüm güncelleştirmelerini nasıl yönettiğiniz?

Projeniz için birden çok ortamları ayarlamak için birçok yolu vardır. Aşağıdaki örnekler, ilgili her uygulama için bir yöntemi gösterir.

### <a name="wordpress"></a>WordPress
Bu bölümde, WordPress için yuvaları kullanarak bir dağıtım iş akışını Ayarla öğreneceksiniz. WordPress, çoğu CMS çözümleri gibi özelleştirme olmadan birden fazla geliştirme ortamları desteklemez. Azure App Service Web Apps özelliğidir kodunuzu dışında yapılandırma ayarlarını depolamak kolaylaştıran birkaç özelliklere sahiptir.

1. Hazırlama yuvası oluşturmadan önce birden çok ortamlarını desteklemek için uygulama kodunuz ayarlayın. WordPress içinde birden çok ortamlarını desteklemek için düzenlemeniz gerekir `wp-config.php` yerel geliştirme üzerinde web uygulaması ve dosyasının başında aşağıdaki kodu ekleyin. Bu işlem, seçili ortamına bağlı doğru yapılandırmayı almak uygulamanızı olanak sağlar.

    ```
    // Support multiple environments
    // set the config file based on current environment
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
    // include the config file if it exists, otherwise WP is going to fail
    require_once $path. $config_file;
    ```

2. Adlı web uygulama kökü altındaki bir klasör oluşturun `config`ve ekleme `wp-config.azure.php` ve `wp-config.local.php` Azure ortamı ve yerel ortamı sırasıyla temsil dosyaları.

3. Aşağıda, kopyalama `wp-config.local.php`:

    ```
    <?php
    // MySQL settings
    /** The name of the database for WordPress */

    define('DB_NAME', 'yourdatabasename');

    /** MySQL database username */
    define('DB_USER', 'yourdbuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'yourpassword');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    /**
     * For developers: WordPress debugging mode.
     * * Change this to true to enable the display of notices during development.
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

    Önceki kodda gösterildiği şekilde anahtarları izinsiz giriş gelen web uygulamanızı önlemek için yardımcı olabilecek güvenlik ayarı, bu nedenle benzersiz değerleri kullanın. Dizesi oluşturmak ihtiyacınız varsa güvenlik anahtarları belirtilen kodda yapabileceğiniz [otomatik Oluşturucu gidin](https://api.wordpress.org/secret-key/1.1/salt) yeni anahtar/değer çiftleri oluşturmak için.

4. Aşağıdaki kodu kopyalayın `wp-config.azure.php`:

    ```    
    <?php
    // MySQL settings
    /** The name of the database for WordPress */

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
    * Change this to true to enable the display of notices during development.
    * It is strongly recommended that plugin and theme developers use WP_DEBUG
    * in their development environments.
    * Turn on debug logging to investigate issues without displaying to end user. For WP_DEBUG_LOG to
    * do anything, WP_DEBUG must be enabled (true). WP_DEBUG_DISPLAY should be used in conjunction
    * with WP_DEBUG_LOG so that errors are not displayed on the page */

    */
    define('WP_DEBUG', getenv('WP_DEBUG'));
    define('WP_DEBUG_LOG', getenv('TURN_ON_DEBUG_LOG'));
    define('WP_DEBUG_DISPLAY',false);

    //Security key settings
    /** If you need to generate the string for security keys mentioned above, you can go the automatic generator to create new keys/values: https://api.wordpress.org/secret-key/1.1/salt **/
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
WordPress uygulamasında yapılandırmak için bir son göreli yollar şeydir. WordPress URL bilgileri veritabanında depolar. Bu depolama bir ortamdan taşıma içeriği başka bir daha zor hale getirir. Veritabanı yerel yerine aşama veya üretim ortamları için aşamasına geçmeden her zaman güncelleştirmeniz gerekir. Bir ortamdan diğerine dağıttığınız her zaman bir veritabanı dağıtımı ile neden sorunları riskini azaltmak için kullanmak [göreli kök bağlantılar eklentisi](https://wordpress.org/plugins/root-relative-urls/), hangi WordPress yönetici Panoyu kullanarak yükleyebilirsiniz.

Aşağıdaki girdileri eklemek, `wp-config.php` önce dosya `That's all, stop editing!` Açıklama:

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

Eklentisi aracılığıyla etkinleştirme `Plugins` WordPress yönetici Pano menüde. WordPress uygulaması için sabit bağlantı ayarlarınızı kaydedin.

#### <a name="the-final-wp-configphp-file"></a>En son `wp-config.php` dosyası
WordPress çekirdek güncelleştirmeleri değil etkiler, `wp-config.php`, `wp-config.azure.php`, ve `wp-config.local.php` dosyaları. Son sürümü işte `wp-config.php` dosyası:

```
<?php
/**
 * The base configurations of the WordPress.
 *
 * This file has the following configurations: MySQL settings, Table Prefix,
 * Secret Keys, and ABSPATH. You can find more information by visiting
 *
 * Codex page. You can get the MySQL settings from your web host.
 *
 * This file is used by the wp-config.php creation script during the
 * installation. You don't have to use the web web app, you can just copy this file
 * to "wp-config.php" and fill in the values.
 *
 * @package WordPress
 */

// Support multiple environments
// set the config file based on current environment
if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) { // local development
  $config_file = 'config/wp-config.local.php';
}
elseif ((strpos(getenv('WP_ENV'),'stage') !== false) ||(strpos(getenv('WP_ENV'),'prod' )!== false )){
  $config_file = 'config/wp-config.azure.php';
}


$path = dirname(__FILE__). '/';
if (file_exists($path. $config_file)) {
  // include the config file if it exists, otherwise WP is going to fail
  require_once $path. $config_file;
}

/** Database Charset to use in creating database tables. */
define('DB_CHARSET', 'utf8');

/** The Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/* That's all, stop editing! Happy blogging. */

define('WP_HOME', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_CONTENT_URL', '/wp-content');
define('DOMAIN_CURRENT_SITE', $_SERVER['HTTP_HOST']);

/** Absolute path to the WordPress directory. */
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__). '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH. 'wp-settings.php');
```

#### <a name="set-up-a-staging-environment"></a>Hazırlama ortamını ayarlama
1. Azure aboneliğiniz üzerinde çalışan bir WordPress web uygulaması zaten varsa, oturum [Azure portal](http://portal.azure.com)ve WordPress web uygulamanıza gidin. WordPress web uygulaması yoksa, bir Azure Marketi'nden oluşturabilirsiniz. Daha fazla bilgi için bkz: [Azure App Service'te bir WordPress web uygulaması oluşturma](web-sites-php-web-site-gallery.md).
Tıklatın **ayarları** > **dağıtım yuvası** > **Ekle** adlı bir dağıtım yuvası oluşturmak için *aşama* . Bir dağıtım yuvası daha önce oluşturduğunuz birincil web uygulaması olarak aynı kaynakları paylaşan başka bir web uygulamasıdır.

    ![Aşama dağıtım yuvası oluşturma](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. Başka bir MySQL veritabanı deyin Ekle `wordpress-stage-db`, kaynak grubunuz için `wordpressapp-group`.

    ![MySQL veritabanı kaynak grubuna Ekle](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. Yeni veritabanına işaret etmek, aşama dağıtım yuvası için bağlantı dizelerini güncelleştirmek `wordpress-stage-db`. Üretim web uygulamanız `wordpressprodapp`ve web uygulaması hazırlama `wordpressprodapp-stage`, farklı veritabanlarına işaret etmelidir.

#### <a name="configure-environment-specific-app-settings"></a>Ortama özgü uygulaması ayarlarını yapılandır
Geliştiriciler saklayabilir anahtar/değer çiftlerinin dize Azure'da adlı yapılandırma bilgilerini bir parçası olarak **uygulama ayarları**, bir web uygulaması ile ilişkili. Çalışma zamanında web uygulamaları otomatik olarak bu değerleri almak ve bunları web uygulamanızda çalışan kod kullanılabilir yapın. Güvenlik açısından bakıldığında, olduğundan iyi tarafı avantajı parolalar dahil veritabanı bağlantı dizeleri gibi hassas bilgileri hiçbir zaman görünmesini bir dosyada düz metin olarak gibi `wp-config.php`.

Aşağıdaki paragrafta açıklanan, bu işlem, dosya değişiklikleri ve WordPress uygulaması için veritabanı değişikliklerini içerdiği için yararlıdır:

* WordPress sürüm yükseltme
* Yeni Ekle veya Düzenle veya eklentileri yükseltme
* Yeni Ekle veya Düzenle veya Temalar yükseltme

Uygulama ayarlarını yapılandırın:

* Veritabanı bilgileri
* Kapatma açık/kapalı WordPress günlüğe kaydetme
* WordPress güvenlik ayarları

![Wordpress web uygulaması için uygulama ayarları](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

Aşağıdaki uygulama ayarları için üretim web app ve hazırlama yuvası eklediğinizden emin olun. Web uygulaması hazırlama ve üretim web uygulaması farklı veritabanları kullandığını unutmayın.

1. Clear **yuva ayarı** WP_ENV dışında tüm ayarlar parametreleri için onay kutusu. Bu işlem, web uygulaması, dosya içeriğini ve veritabanı için yapılandırma değiştireceksiniz. Varsa **yuva ayarı** denetlenir, web uygulamanızın uygulama ayarlarının ve bağlantı dizesi yapılandırma *değil* ortamlar genelinde yapılırken taşıma bir **takas** işlemi. Var olan veritabanı değişiklikleri üretim web uygulamanız bölün değil.

2. Yerel geliştirme ortamı web uygulaması aşama web uygulaması ve veritabanı WebMatrix veya tercih ettiğiniz, FTP, Git veya PhpMyAdmin gibi araçları kullanarak dağıtın.

    ![WordPress web uygulaması için Web matris Yayımla iletişim kutusu](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. Gözat ve hazırlama web uygulamanızı test edin. Web uygulamasının tema güncelleştirilmesi olduğu bir senaryo göz önünde bulundurularak, hazırlama web uygulaması aşağıda verilmiştir.

    ![Web uygulaması yuvaları takas önce hazırlama Gözat](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. Tüm görünüyorsa iyi, tıklatın **takas** içeriğinizi üretim ortamına taşımak için hazırlama web uygulamanızı düğmesinde. Bu durumda, web uygulaması ve veritabanı sırasında ortamlar üzerinde takas her **takas** işlemi.

    ![Önizleme değişiklikleri için WordPress değiştirme](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > Senaryonuz yalnızca dosyaları (veritabanı güncelleştirmeleri) anında gerekiyorsa, ardından denetleyin **yuva ayarı** tüm veritabanı ile ilgili için *uygulama ayarları* ve *bağlantı dizeleri ayarları* içinde **Web uygulaması ayarları** dikey penceresinde bunun önce Azure portalındaki **takas**. Bunu yaptığınızda bu durumda, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER ve varsayılan bağlantı dizesi ayarlarının Önizleme değişiklikleri gösterilmesi gerekir olmayan bir **takas**. Tamamlandığında, şu anda **takas** işlemi, yalnızca güncelleştirme dosyaları WordPress web uygulaması gerekir.
    >
    >

    Bunu yaptığınızda önce bir **takas**, üretim WordPress web uygulaması aşağıdadır.
    ![Üretim web uygulaması yuvaları takas önce](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)

    Sonra **takas** işlemi, temayı üretim web uygulamanız güncelleştirilmiştir.

    ![Üretim web uygulaması yuvaları takas sonra](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. Geri alma gerektiğinde, üretim web gidebilirsiniz **uygulama ayarları**, tıklatıp **takas** web uygulaması ve üretim veritabanına hazırlama yuvası takas düğmesi. Veritabanı değişiklikleri birlikte olup olmadığını unutmayın bir **takas** işlemi, daha sonra hazırlama web uygulamanızın dağıttığınız sonraki sefer hazırlama web uygulamanız için geçerli veritabanı için veritabanı değişikliklerini dağıtmak vermeniz gerekir. Geçerli veritabanı, önceki üretim veya aşama veritabanının olabilir.

#### <a name="summary"></a>Özet
Aşağıda, bir veritabanı sahip herhangi bir uygulama için genelleştirilmiş bir işlemdir:

1. Uygulamayı yerel ortamınıza yükleyin.
2. Ortama özgü yapılandırmaları (yerel ve Azure Web Apps) içerir.
3. Web uygulamaları için hazırlama ve üretim ortamları ayarlama.
4. Zaten Azure üzerinde çalışan bir üretim uygulamanız varsa, üretim içeriğinize (dosyalar/kodu ve veritabanı) yerel ve hazırlama ortamları eşitleyin.
5. Uygulamanızı yerel ortamınızda geliştirin.
6. Üretim web uygulamanız Bakım veya kilitli modu altında yerleştirin ve üretim veritabanını içerik hazırlama ve geliştirme ortamlarını eşitleyin.
7. Test ve hazırlık ortamı dağıtın.
8. Üretim ortamınıza dağıtın.
9. 4 ile 6 arasındaki adımları yineleyin.

### <a name="umbraco"></a>Umbraco
Bu bölümde, nasıl özel bir modülü birden çok DevOps ortamlar genelinde dağıtmak için kullandığı Umbraco CMS öğreneceksiniz. Bu örnek, birden çok geliştirme ortamı yönetmek için farklı bir yaklaşım sağlar.

[Umbraco CMS](http://umbraco.com/) birçok geliştiriciler tarafından kullanılan bir popüler .NET CMS çözümüdür. Sağladığı [Courier2](http://umbraco.com/products/more-add-ons/courier-2) geliştirme üretim ortamları için hazırlama dağıtmak için modülü. WebMatrix veya Visual Studio'yu kullanarak kolayca bir Umbraco CMS web uygulaması için bir yerel geliştirme ortamı oluşturabilirsiniz.

- [Visual Studio ile bir Umbraco web uygulaması oluşturma](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [WebMatrix ile bir Umbraco web uygulaması oluşturma](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

Her zaman kaldırmayı unutmayın `install` , uygulamanızın altında bir klasör ve hiçbir zaman aşama veya üretim web uygulamaları için karşıya yükleme. Bu öğretici, WebMatrix kullanır.

#### <a name="set-up-a-staging-environment"></a>Hazırlama ortamını ayarlama
1. Bir dağıtım yuvası Umbraco CMS web uygulaması zaten varsa ve çalıştırma Umbraco CMS web uygulaması için daha önce belirtildiği gibi oluşturun. Bunu yapmazsanız, marketten bir tane oluşturabilirsiniz.
2. Yeni işaret edecek şekilde, aşama dağıtım yuvası için bağlantı dizesini güncellemeniz **umbraco aşama db** veritabanı. Üretim web uygulaması (umbraositecms-1) ve hazırlama web uygulaması (umbracositecms-1-aşama) *gerekir* farklı veritabanlarına gelin.

    ![Yeni hazırlama veritabanı ile web uygulaması hazırlama için kullanılan bağlantı dizesi güncelleştir](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. Tıklatın **alma yayımlama ayarları** dağıtım yuvası için **aşama**. Bu işlem, yerel geliştirme web uygulamasından uygulamanızı Azure web uygulamasına yayımlamak için Visual Studio veya WebMatrix gerektiren tüm bilgilerini depolayan bir yayımlama ayarları dosyası indirir.

    ![Get ayarı hazırlama web uygulaması yayımlama](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. Yerel geliştirme web uygulamanızı WebMatrix veya Visual Studio'da açın. Bu öğretici, WebMatrix kullanır. İlk olarak, hazırlama web uygulamanız için yayımlama ayarları dosyasını içeri aktarmanız gerekir.

    ![Web Matrix kullanarak Umbraco yayımlama ayarlarını içeri aktarma](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. İletişim kutusunda değişiklikleri gözden geçirin ve yerel web uygulamanızı Azure web uygulamasına dağıtma *umbracositecms 1 aşama*. Dosyaları doğrudan hazırlama web uygulamanıza dağıttığınızda, dosyalarında atlayacak `~/app_data/TEMP/` aşama web uygulaması ilk çalıştırıldığında bu dosyalar yeniden oluşturulacak olmadığından klasör başlatıldı. Ayrıca atlayın `~/app_data/umbraco.config` de yeniden oluşturulacak dosya.

    ![Web Matristeki Yayımla değişiklikleri gözden geçirin](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. Hazırlama web uygulaması başarıyla Umbraco yerel web uygulaması yayımladıktan sonra hazırlama web uygulamanıza göz atın ve sorunları kural için birkaç testleri çalıştırın.

#### <a name="set-up-the-courier2-deployment-module"></a>Courier2 dağıtım modülünü kurun
İle [Courier2](http://umbraco.com/products/more-add-ons/courier-2) modül yalnızca sağ anında içeriği, stil sayfaları ve geliştirme modülleri hazırlama bir web uygulamasından bir üretim web uygulaması. Bu işlem bir güncelleştirme dağıttığınızda üretim web uygulamanız çiğnemekten riskini azaltır.
Courier2 için için bir lisans satın `*.azurewebsites.net` etki alanı ve özel etki alanınızı (örneğin http://abc.com). Lisans satın aldıktan sonra indirilen lisans yerleştirin (. Lisans Sözleşmesi dosyası) içinde `bin` klasör.

![Bin klasörü altındaki açılan lisans dosyası](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. [Courier2 paketini indirin](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/). Aşama web uygulamanıza, deyin http://umbracocms-site-stage.azurewebsites.net/umbraco, oturum açma tıklatın **Geliştirici** menüsüne ve ardından **paketleri** > **yükleme yerel Paket**.

    ![Umbraco paketi yükleyicisi](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. Courier2 paketi yükleyici kullanarak yükleyin.

    ![Paketi courier modülü için yükleme](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. Paketi yapılandırmak için courier.config dosyasını güncelleştirmeniz gerekir **Config** klasör, web uygulamanızın.

    ```xml
    <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how to connect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set the passwordEncoding to clear: -->
        <repository name="production web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1.azurewebsites.net</url>
          <user>0</user>
          <!--<login>user@email.com</login> -->
          <!-- <password>user_password</password>-->
          <!-- <passwordEncoding>Clear</passwordEncoding>-->
          </repository>
     </repositories>
     ```

4. Altında `<repositories>`, üretim site URL'si ve kullanıcı bilgilerini girin.
    Varsayılan Umbraco üyelik sağlayıcısı kullanıyorsanız, yönetim kullanıcı kimliği eklemek &lt;kullanıcı&gt; bölümü.
    Özel bir Umbraco üyelik sağlayıcısı kullanıyorsanız `<login>`,`<password>` üretim siteye bağlamak için Courier2 modülünde.
    Daha fazla ayrıntı için [Courier2 modülü belgelerini gözden](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).

5. Benzer şekilde, üretim sitenizde Courier2 modülünü yüklemek ve aşağıda gösterildiği gibi ilgili courier.config dosya aşama web uygulamasında işaret edecek şekilde yapılandırın.

    ```xml
     <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how to connect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set the passwordEncoding to clear: -->
        <repository name="Stage web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1-stage.azurewebsites.net</url>
          <user>0</user>
          </repository>
     </repositories>
    ```

6. Tıklatın **Courier2** sekmesinde Umbraco CMS web uygulama panosunda ve ardından **konumları**. Depo adını bölümünde belirtildiği gibi görmeniz gerekir `courier.config`. Üretim ve hazırlama web uygulamaları üzerinde bu işlemi yapabilirsiniz.

    ![Görünüm hedef web uygulama havuzu](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. Hazırlama sitesinden içerik üretim siteye dağıtmak için Git **içerik**ve varolan bir sayfayı seçebilir veya yeni bir sayfa oluşturun. Varolan bir sayfayı sayfanın başlığı olduğu my web uygulamasından seçecektir **başlarken – yeni**ve ardından **kaydetmek ve yayımlamak**.

    ![Sayfasının başlığını değiştirme ve yayımlama](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. Tüm seçenekleri görüntülemek için değiştirilmiş sayfanın sağ tıklayın. Tıklatın **Courier** açmak için **dağıtım** iletişim kutusu. Tıklatın **dağıtma** dağıtımını başlatmak için.

    ![Courier modülü dağıtım iletişim](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. Değişiklikleri gözden geçirin ve ardından **devam**.

    ![Courier modülü dağıtım iletişim değişiklikleri gözden geçir](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    Dağıtım günlüğü dağıtım başarılı olup olmadığını gösterir.

     ![Courier modülden dağıtım günlüklerini görüntüle](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. Değişiklikler yansıtılır görmek için üretim web uygulamanız göz atın.

     ![Üretim web uygulamasına göz atın](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

Courier kullanma hakkında daha fazla bilgi için belgelerini gözden geçirin.

#### <a name="how-to-upgrade-the-umbraco-cms-version"></a>Umbraco CMS sürüm yükseltme
Courier olacak başka bir Umbraco CMS sürümünden yükseltme Yardımı. Umbraco CMS sürümüne yükselttiğinizde, özel modüller veya iş ortakları ve Umbraco çekirdek kitaplıkları modüllerden uyumsuzluklar için işaretlemeniz gerekir. En iyi uygulamalar şunlardır:

* Yükseltmeden önce her zaman, web uygulaması ve veritabanı yedekleme. Azure Web uygulamaları üzerinde Yedekleme özelliğini kullanarak, Web siteleri için Otomatik yedekler ayarlayın ve geri yükleme özelliğini kullanarak gerekirse sitenize geri yükleyin. Daha fazla ayrıntı için bkz: [web uygulamanızı nasıl](web-sites-backup.md) ve [web uygulamanızı geri yükleme](web-sites-restore.md).
* İş ortakları paketlerinden yükseltme yapıyorsanız sürümü ile uyumlu olup olmadığını denetleyin. Paketin üzerinde sayfa yükleme, Umbraco CMS sürümüyle proje uyumluluğu gözden geçirin.

Web uygulamanızı yerel olarak yükseltme hakkında daha fazla ayrıntı için [genel yükseltme yönergelere bakın](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).

Yerel geliştirme sitenizi yükselttikten sonra değişiklikleri hazırlama web uygulamasını yayımlayın. Uygulamanızı test edin. Tüm görünüyorsa iyi kullanmak **takas** hazırlama sitenizi üretim web uygulamasına değiştirme düğmesi. Kullandığınızda **takas** işlemi, web uygulamanızın yapılandırmasında etkilenecek değişiklikleri görüntüleyebilirsiniz. Bu **takas** işlemi ile web uygulamaları ve veritabanları değiştirir. Sonra **takas**, üretim web uygulaması umbraco aşama db veritabanına işaret edecek ve hazırlama web uygulaması umbraco üretim db veritabanına işaret.

![Umbraco CMS dağıtmak için Önizleme değiştirme](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

Web uygulaması ve veritabanı takas avantajları şunlardır:

* Başka bir web uygulamanızın önceki sürüme geri alabilirsiniz **takas** herhangi bir uygulama sorun varsa.
* Yükseltme için dosyaları ve üretim web uygulaması hazırlama web uygulamasından veritabanları ve veritabanı dağıtmanız gerekir. Dosyaları ve veritabanları dağıttığınızda pek çok yanlış gidebilirsiniz. Kullanarak **takas** özelliği yuvaları biz kapalı kalma süresi yükseltme sırasında ve değişiklikleri dağıtırken oluşabilecek hatalar riskini azaltmak.
* Yapabileceğiniz **A / B testi** kullanarak [üretimde test](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) özelliği.

Bu örnek özel modüller ortamlar genelinde dağıtımını yönetmek için Umbraco Courier modülüne benzer burada yapı platform esnekliğini gösterir.

## <a name="references"></a>Başvurular
[Azure App Service ile Çevik Yazılım Geliştirme](app-service-agile-software-development.md)

[Hazırlık ortamları için Azure App Service'te web uygulamalarını ayarlama](web-sites-staged-publishing.md)

[Üretim dışı dağıtım yuvaları Web erişimi engellemek nasıl](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
