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
# <a name="use-devops-environments-effectively-for-your-web-apps"></a><span data-ttu-id="881a0-103">DevOps ortamları etkili bir şekilde web uygulamaları için kullanın</span><span class="sxs-lookup"><span data-stu-id="881a0-103">Use DevOps environments effectively for your web apps</span></span>
<span data-ttu-id="881a0-104">Bu makale size nasıl gösterir tooset ayarlama ve birden çok sürümü, uygulamanızın, geliştirme, hazırlama, kalite güvence (QA) ve üretim gibi çeşitli ortamlarda olduğunda web uygulama dağıtımlarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="881a0-104">This article shows you how tooset up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="881a0-105">Her bir sürümü, uygulamanızın bir geliştirme ortamı hello belirli amacı, dağıtım işleminiz için kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="881a0-105">Each version of your application can be considered as a development environment for hello specific purpose of your deployment process.</span></span> <span data-ttu-id="881a0-106">Örneğin, hello değişiklikleri tooproduction sokmadan önce geliştiriciler hello QA ortamı tootest hello hello uygulama kalitesini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="881a0-106">For example, developers can use hello QA environment tootest hello quality of hello application before they push hello changes tooproduction.</span></span>
<span data-ttu-id="881a0-107">Birden çok geliştirme ortamı bir sınama tootrack kod gerektiğinden kaynakların (hesaplama, web uygulaması, veritabanı, önbellek, vb.) yönetmek ve kod ortamlar genelinde dağıtmak olabilir.</span><span class="sxs-lookup"><span data-stu-id="881a0-107">Multiple development environments can be a challenge because you need tootrack code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span></span>

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a><span data-ttu-id="881a0-108">Bir üretim dışı ortamını (aşaması, geliştirme, QA) ayarlama</span><span class="sxs-lookup"><span data-stu-id="881a0-108">Set up a non-production environment (stage, dev, QA)</span></span>
<span data-ttu-id="881a0-109">Bir üretim web uygulaması çalışır durumda sonra hello sonraki toocreate bir üretim ortamı dışındaki bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="881a0-109">After a production web app is up and running, hello next step is toocreate a non-production environment.</span></span> <span data-ttu-id="881a0-110">toouse dağıtım yuvaları, hello standart veya Premium Azure uygulama hizmeti planı modunda çalışır durumda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="881a0-110">toouse deployment slots, make sure that you are running in hello Standard or Premium Azure App Service plan mode.</span></span> <span data-ttu-id="881a0-111">Dağıtım yuvaları, kendi ana bilgisayar adları olan canlı web uygulamalardır.</span><span class="sxs-lookup"><span data-stu-id="881a0-111">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="881a0-112">Web uygulaması içerik ve yapılandırma öğeleri hello üretim yuvası da dahil olmak üzere iki dağıtım yuvası arasında değişiklik yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="881a0-112">Web app content and configuration elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="881a0-113">Uygulama tooa dağıtım yuvası dağıttığınızda, aşağıdaki faydaları hello alın:</span><span class="sxs-lookup"><span data-stu-id="881a0-113">When you deploy your application tooa deployment slot, you get hello following benefits:</span></span>

- <span data-ttu-id="881a0-114">Merhaba uygulama hello üretim yuvasıyla takas önce değişiklikleri hazırlık dağıtım yuvasındaki web uygulamasında tooa doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="881a0-114">You can validate changes tooa web app in a staging deployment slot before you swap hello app with hello production slot.</span></span>
- <span data-ttu-id="881a0-115">Bir web uygulaması tooa yuvası ilk Dağıt ve üretime takas hello yuvası tüm örneklerini üretime takas önce warmed.</span><span class="sxs-lookup"><span data-stu-id="881a0-115">When you deploy a web app tooa slot first and swap it into production, all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="881a0-116">Bu işlem, web uygulamanızı dağıtırken kapalı kalma süresini ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="881a0-116">This process eliminates downtime when you deploy your web app.</span></span> <span data-ttu-id="881a0-117">Merhaba trafik yeniden yönlendirmesi sorunsuzdur ve hiçbir istek tooswap işlemleri bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="881a0-117">hello traffic redirection is seamless, and no requests are dropped due tooswap operations.</span></span> <span data-ttu-id="881a0-118">tooautomate tüm bu iş akışını yapılandırmak [otomatik takas](web-sites-staged-publishing.md#configure-auto-swap) zaman öncesi takas doğrulama gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="881a0-118">tooautomate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span></span>
- <span data-ttu-id="881a0-119">Değiştirme işleminden sonra önceden hazırlanmış hello web uygulaması şimdi sahip hello yuvası hello önceki üretim web uygulamasına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="881a0-119">After a swap, hello slot that has hello previously staged web app now has hello previous production web app.</span></span> <span data-ttu-id="881a0-120">Beklendiği gibi hello üretim yuvasına hello değişiklikleri varsa, hello gerçekleştirebilirsiniz aynı, "bilinen iyi en son" hemen tooget takas web app arka.</span><span class="sxs-lookup"><span data-stu-id="881a0-120">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good" web app back.</span></span>

<span data-ttu-id="881a0-121">Hazırlık dağıtım yuvasındaki yukarı tooset bkz [hazırlık Azure App Service'deki web uygulamaları için ortamları ayarlama](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="881a0-121">tooset up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="881a0-122">Her ortam kaynakları kendi kümesini içermelidir.</span><span class="sxs-lookup"><span data-stu-id="881a0-122">Every environment should include its own set of resources.</span></span> <span data-ttu-id="881a0-123">Web uygulamanız bir veritabanı kullanıyorsa, örneğin, daha sonra hem üretim hem de web uygulamaları hazırlama farklı veritabanları kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="881a0-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span></span> <span data-ttu-id="881a0-124">Veritabanı, depolama veya önbellek tooset gibi hazırlama geliştirme ortamı kaynakları hazırlama geliştirme ortamınızı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="881a0-124">Add staging development environment resources such as database, storage, or cache tooset your staging development environment.</span></span>

## <a name="examples-of-using-multiple-development-environments"></a><span data-ttu-id="881a0-125">Birden çok geliştirme ortamı kullanma örnekleri</span><span class="sxs-lookup"><span data-stu-id="881a0-125">Examples of using multiple development environments</span></span>
<span data-ttu-id="881a0-126">Herhangi bir projenin kaynak kodu yönetimi en az iki ortamlarla izlemelidir: geliştirme ve üretim.</span><span class="sxs-lookup"><span data-stu-id="881a0-126">Any project should follow source code management with at least two environments: development and production.</span></span> <span data-ttu-id="881a0-127">İçerik yönetim sistemleri (CMSs), uygulama çerçeveleri, vb. kullanırsanız Merhaba uygulaması özelleştirme olmadan bu senaryo desteklemeyebilir.</span><span class="sxs-lookup"><span data-stu-id="881a0-127">If you use content management systems (CMSs), application frameworks, etc., hello application might not support this scenario without customization.</span></span> <span data-ttu-id="881a0-128">Bu planlıyorsanız, bazı hello aşağıdaki bölümlerde açıklanan hello popüler uygulamayı için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="881a0-128">This eventuality is true for some of hello popular frameworks that are discussed in hello following sections.</span></span> <span data-ttu-id="881a0-129">CMS/çerçeveleri ile gibi çalışırken çok soruların toomind getirir:</span><span class="sxs-lookup"><span data-stu-id="881a0-129">Lots of questions come toomind when you work with CMS/frameworks, such as:</span></span>

- <span data-ttu-id="881a0-130">Nasıl, hello içerik farklı ortamlara başlama?</span><span class="sxs-lookup"><span data-stu-id="881a0-130">How do you break hello content out into different environments?</span></span>
- <span data-ttu-id="881a0-131">Hangi dosyaların framework sürüm güncelleştirmelerini etkilemeden değiştirebilir miyim?</span><span class="sxs-lookup"><span data-stu-id="881a0-131">What files can you change without affecting framework version updates?</span></span>
- <span data-ttu-id="881a0-132">Ortam başına yapılandırmaları nasıl yönettiğiniz?</span><span class="sxs-lookup"><span data-stu-id="881a0-132">How do you manage configurations per environment?</span></span>
- <span data-ttu-id="881a0-133">Modüller, eklenti ve hello çekirdek framework sürüm güncelleştirmelerini nasıl yönettiğiniz?</span><span class="sxs-lookup"><span data-stu-id="881a0-133">How do you manage version updates for modules, plugins, and hello core framework?</span></span>

<span data-ttu-id="881a0-134">Projeniz için birden çok ortamları ayarlama birçok yolu tooset vardır.</span><span class="sxs-lookup"><span data-stu-id="881a0-134">There are many ways tooset up multiple environments for your project.</span></span> <span data-ttu-id="881a0-135">Merhaba Aşağıdaki örnekler ilgili her uygulama için bir yöntemi gösterir.</span><span class="sxs-lookup"><span data-stu-id="881a0-135">hello following examples show one method for each respective application.</span></span>

### <a name="wordpress"></a><span data-ttu-id="881a0-136">WordPress</span><span class="sxs-lookup"><span data-stu-id="881a0-136">WordPress</span></span>
<span data-ttu-id="881a0-137">Bu bölümde, nasıl tooset kullanarak bir dağıtım iş akışı için WordPress yuvası öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="881a0-137">In this section, you will learn how tooset up a deployment workflow by using slots for WordPress.</span></span> <span data-ttu-id="881a0-138">WordPress, çoğu CMS çözümleri gibi özelleştirme olmadan birden fazla geliştirme ortamları desteklemez.</span><span class="sxs-lookup"><span data-stu-id="881a0-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span></span> <span data-ttu-id="881a0-139">Azure App Service Web Apps özelliğini Hello kodunuzu dışında kolay toostore yapılandırma ayarları yapmanız birkaç özelliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="881a0-139">hello Web Apps feature of Azure App Service has a few features that make it easy toostore configuration settings outside your code.</span></span>

1. <span data-ttu-id="881a0-140">Hazırlama yuvası oluşturmadan önce uygulama kodu toosupport birden çok ortamı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="881a0-140">Before you create a staging slot, set up your application code toosupport multiple environments.</span></span> <span data-ttu-id="881a0-141">toosupport birden çok ortamları WordPress içinde tooedit gerek `wp-config.php` yerel geliştirme üzerinde web uygulaması ve kod hello dosya hello başında aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="881a0-141">toosupport multiple environments in WordPress, you need tooedit `wp-config.php` on your local development web app and add hello following code at hello beginning of hello file.</span></span> <span data-ttu-id="881a0-142">Bu işlem hello Seçili ortamı tabanlı uygulama toopick hello doğru yapılandırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="881a0-142">This process will enable your application toopick hello correct configuration based on hello selected environment.</span></span>

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

2. <span data-ttu-id="881a0-143">Adlı web uygulama kökü altındaki bir klasör oluşturun `config`ve hello ekleyin `wp-config.azure.php` ve `wp-config.local.php` Azure ortamı ve yerel ortamı sırasıyla temsil dosyaları.</span><span class="sxs-lookup"><span data-stu-id="881a0-143">Create a folder under web app root called `config`, and add hello `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span></span>

3. <span data-ttu-id="881a0-144">Merhaba aşağıdakileri kopyalayın `wp-config.local.php`:</span><span class="sxs-lookup"><span data-stu-id="881a0-144">Copy hello following in `wp-config.local.php`:</span></span>

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

    <span data-ttu-id="881a0-145">Merhaba önceki kodda gösterildiği gibi Hello güvenlik anahtarları ayarlama izinsiz giriş gelen web uygulamanızı tooprevent Yardım, benzersiz değerleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="881a0-145">Setting hello security keys as illustrated in hello previous code can help tooprevent your web app from being hacked, so use unique values.</span></span> <span data-ttu-id="881a0-146">Merhaba kodda belirtilen güvenlik anahtarlarını toogenerate hello dize ihtiyacınız yoksa, şunları yapabilirsiniz [gidin toohello otomatik Oluşturucu](https://api.wordpress.org/secret-key/1.1/salt) toocreate yeni anahtar/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="881a0-146">If you need toogenerate hello string for security keys mentioned in hello code, you can [go toohello automatic generator](https://api.wordpress.org/secret-key/1.1/salt) toocreate new key/value pairs.</span></span>

4. <span data-ttu-id="881a0-147">Kopya hello aşağıdaki kod `wp-config.azure.php`:</span><span class="sxs-lookup"><span data-stu-id="881a0-147">Copy hello following code in `wp-config.azure.php`:</span></span>

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

#### <a name="use-relative-paths"></a><span data-ttu-id="881a0-148">Göreli yollar kullanın</span><span class="sxs-lookup"><span data-stu-id="881a0-148">Use relative paths</span></span>
<span data-ttu-id="881a0-149">Son bir şey tooconfigure hello WordPress uygulamasında göreli yollar ' dir.</span><span class="sxs-lookup"><span data-stu-id="881a0-149">One last thing tooconfigure in hello WordPress app is relative paths.</span></span> <span data-ttu-id="881a0-150">WordPress URL bilgileri hello veritabanında depolar.</span><span class="sxs-lookup"><span data-stu-id="881a0-150">WordPress stores URL information in hello database.</span></span> <span data-ttu-id="881a0-151">Bu depolama bir ortam tooanother taşıma içerikten daha zor hale getirir.</span><span class="sxs-lookup"><span data-stu-id="881a0-151">This storage makes moving content from one environment tooanother more difficult.</span></span> <span data-ttu-id="881a0-152">Yerel toostage veya aşama tooproduction ortamları taşımak her zaman tooupdate hello veritabanınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="881a0-152">You need tooupdate hello database every time you move from local toostage or stage tooproduction environments.</span></span> <span data-ttu-id="881a0-153">tooreduce hello kullan hello bir ortam tooanother dağıtmak her zaman bir veritabanı dağıtımı ile neden sorunları riskini [göreli kök bağlantılar eklentisi](https://wordpress.org/plugins/root-relative-urls/), hangi hello WordPress Yöneticisi'ni kullanarak yükleyebilirsiniz Pano.</span><span class="sxs-lookup"><span data-stu-id="881a0-153">tooreduce hello risk of issues that can be caused with deploying a database every time you deploy from one environment tooanother, use hello [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using hello WordPress administrator dashboard.</span></span>

<span data-ttu-id="881a0-154">Girişleri tooyour aşağıdaki hello eklemek `wp-config.php` hello önce dosyayı `That's all, stop editing!` Açıklama:</span><span class="sxs-lookup"><span data-stu-id="881a0-154">Add hello following entries tooyour `wp-config.php` file before hello `That's all, stop editing!` comment:</span></span>

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

<span data-ttu-id="881a0-155">Merhaba eklentisi hello aracılığıyla etkinleştirme `Plugins` WordPress yönetici Pano menüde.</span><span class="sxs-lookup"><span data-stu-id="881a0-155">Activate hello plugin through hello `Plugins` menu in WordPress administrator dashboard.</span></span> <span data-ttu-id="881a0-156">WordPress uygulaması için sabit bağlantı ayarlarınızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="881a0-156">Save your permalink settings for WordPress app.</span></span>

#### <a name="hello-final-wp-configphp-file"></a><span data-ttu-id="881a0-157">Merhaba son `wp-config.php` dosyası</span><span class="sxs-lookup"><span data-stu-id="881a0-157">hello final `wp-config.php` file</span></span>
<span data-ttu-id="881a0-158">WordPress çekirdek güncelleştirmeleri değil etkiler, `wp-config.php`, `wp-config.azure.php`, ve `wp-config.local.php` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="881a0-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span></span> <span data-ttu-id="881a0-159">Merhaba son sürümünü işte `wp-config.php` dosyası:</span><span class="sxs-lookup"><span data-stu-id="881a0-159">Here's a final version of hello `wp-config.php` file:</span></span>

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

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="881a0-160">Hazırlama ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="881a0-160">Set up a staging environment</span></span>
1. <span data-ttu-id="881a0-161">Azure aboneliğiniz üzerinde çalışan bir WordPress web uygulaması zaten varsa toohello oturum [Azure portal](http://portal.azure.com), ve ardından tooyour WordPress web uygulamasına gidin.</span><span class="sxs-lookup"><span data-stu-id="881a0-161">If you already have a WordPress web app running on your Azure subscription, sign in toohello [Azure portal](http://portal.azure.com), and then go tooyour WordPress web app.</span></span> <span data-ttu-id="881a0-162">WordPress web uygulaması yoksa, hello Azure Marketi birinden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="881a0-162">If you don't have a WordPress web app, you can create one from hello Azure Marketplace.</span></span> <span data-ttu-id="881a0-163">toolearn daha, fazla [Azure App Service'te bir WordPress web uygulaması oluşturma](web-sites-php-web-site-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="881a0-163">toolearn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span></span>
<span data-ttu-id="881a0-164">Tıklatın **ayarları** > **dağıtım yuvası** > **Ekle** toocreate hello ada sahip bir dağıtım yuvası *aşama*.</span><span class="sxs-lookup"><span data-stu-id="881a0-164">Click **Settings** > **Deployment slots** > **Add** toocreate a deployment slot with hello name *stage*.</span></span> <span data-ttu-id="881a0-165">Bir dağıtım yuvası, daha önce oluşturduğunuz hello birincil web uygulaması olarak aynı kaynakları paylaşımları hello başka bir web uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="881a0-165">A deployment slot is another web application that shares hello same resources as hello primary web app that you created previously.</span></span>

    ![Aşama dağıtım yuvası oluşturma](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. <span data-ttu-id="881a0-167">Başka bir MySQL veritabanı deyin Ekle `wordpress-stage-db`, tooyour kaynak grubu, `wordpressapp-group`.</span><span class="sxs-lookup"><span data-stu-id="881a0-167">Add another MySQL database, say `wordpress-stage-db`, tooyour resource group, `wordpressapp-group`.</span></span>

    ![MySQL veritabanı tooresource grubu Ekle](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. <span data-ttu-id="881a0-169">Merhaba, aşama dağıtım yuvası toopoint toohello yeni bir veritabanı için bağlantı dizelerini güncelleştirmek `wordpress-stage-db`.</span><span class="sxs-lookup"><span data-stu-id="881a0-169">Update hello connection strings for your stage deployment slot toopoint toohello new database, `wordpress-stage-db`.</span></span> <span data-ttu-id="881a0-170">Üretim web uygulamanız `wordpressprodapp`ve web uygulaması hazırlama `wordpressprodapp-stage`, gereken noktası toodifferent veritabanları.</span><span class="sxs-lookup"><span data-stu-id="881a0-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point toodifferent databases.</span></span>

#### <a name="configure-environment-specific-app-settings"></a><span data-ttu-id="881a0-171">Ortama özgü uygulaması ayarlarını yapılandır</span><span class="sxs-lookup"><span data-stu-id="881a0-171">Configure environment-specific app settings</span></span>
<span data-ttu-id="881a0-172">Geliştiriciler saklayabilir anahtar/değer çiftlerinin dize Azure'da hello yapılandırma bilgileri, adlı bir parçası olarak **uygulama ayarları**, bir web uygulaması ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="881a0-172">Developers can store key/value string pairs in Azure as part of hello configuration information, called **App Settings**, that's associated with a web app.</span></span> <span data-ttu-id="881a0-173">Çalışma zamanında web uygulamaları otomatik olarak bu değerleri almak ve bunları web uygulamanızda çalışan kullanılabilir toocode getirin.</span><span class="sxs-lookup"><span data-stu-id="881a0-173">At runtime, web apps automatically retrieve these values and make them available toocode that's running in your web app.</span></span> <span data-ttu-id="881a0-174">Güvenlik açısından bakıldığında, olduğundan iyi tarafı avantajı parolalar dahil veritabanı bağlantı dizeleri gibi hassas bilgileri hiçbir zaman görünmesini bir dosyada düz metin olarak gibi `wp-config.php`.</span><span class="sxs-lookup"><span data-stu-id="881a0-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span></span>

<span data-ttu-id="881a0-175">Paragrafları aşağıdaki hello anlatılmıştır, bu işlem, dosya değişiklikleri ve hello WordPress uygulaması için veritabanı değişikliklerini içerdiği için yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="881a0-175">This process, which is explained in hello following paragraphs, is useful because it includes both file changes and database changes for hello WordPress app:</span></span>

* <span data-ttu-id="881a0-176">WordPress sürüm yükseltme</span><span class="sxs-lookup"><span data-stu-id="881a0-176">WordPress version upgrade</span></span>
* <span data-ttu-id="881a0-177">Yeni Ekle veya Düzenle veya eklentileri yükseltme</span><span class="sxs-lookup"><span data-stu-id="881a0-177">Add new or edit or upgrade plugins</span></span>
* <span data-ttu-id="881a0-178">Yeni Ekle veya Düzenle veya Temalar yükseltme</span><span class="sxs-lookup"><span data-stu-id="881a0-178">Add new or edit or upgrade themes</span></span>

<span data-ttu-id="881a0-179">Uygulama ayarlarını yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="881a0-179">Configure app settings for:</span></span>

* <span data-ttu-id="881a0-180">Veritabanı bilgileri</span><span class="sxs-lookup"><span data-stu-id="881a0-180">Database information</span></span>
* <span data-ttu-id="881a0-181">Kapatma açık/kapalı WordPress günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="881a0-181">Turning on/off WordPress logging</span></span>
* <span data-ttu-id="881a0-182">WordPress güvenlik ayarları</span><span class="sxs-lookup"><span data-stu-id="881a0-182">WordPress security settings</span></span>

![Wordpress web uygulaması için uygulama ayarları](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

<span data-ttu-id="881a0-184">Uygulama ayarları üretim web app ve hazırlama yuvası için aşağıdaki hello eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="881a0-184">Make sure that you add hello following app settings for your production web app and stage slot.</span></span> <span data-ttu-id="881a0-185">Merhaba üretim web uygulaması ve hazırlama web uygulaması farklı veritabanları kullandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="881a0-185">Note that hello production web app and staging web app use different databases.</span></span>

1. <span data-ttu-id="881a0-186">Clear hello **yuva ayarı** WP_ENV dışındaki tüm hello ayarları parametrelerden onay kutusunu.</span><span class="sxs-lookup"><span data-stu-id="881a0-186">Clear hello **Slot Setting** checkbox for all hello settings parameters except WP_ENV.</span></span> <span data-ttu-id="881a0-187">Bu işlem, web uygulaması, dosya içeriğini ve veritabanını hello yapılandırma değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="881a0-187">This process will swap hello configuration for your web app, file content, and database.</span></span> <span data-ttu-id="881a0-188">Varsa **yuva ayarı** olan işaretli hello web uygulamanızın uygulama ayarlarının ve bağlantı dizesini yapılandırma olacak *değil* ortamlar genelinde yapılırken taşıma bir **takas** işlemi.</span><span class="sxs-lookup"><span data-stu-id="881a0-188">If **Slot Setting** is checked, hello web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span></span> <span data-ttu-id="881a0-189">Var olan veritabanı değişiklikleri üretim web uygulamanız bölün değil.</span><span class="sxs-lookup"><span data-stu-id="881a0-189">Any database changes that are present will not break your production web app.</span></span>

2. <span data-ttu-id="881a0-190">Merhaba yerel geliştirme ortamı web uygulama toohello aşama web uygulaması ve veritabanı WebMatrix veya tercih ettiğiniz, FTP, Git veya PhpMyAdmin gibi araçları kullanarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="881a0-190">Deploy hello local development environment web app toohello stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span></span>

    ![WordPress web uygulaması için Web matris Yayımla iletişim kutusu](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. <span data-ttu-id="881a0-192">Gözat ve hazırlama web uygulamanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="881a0-192">Browse and test your staging web app.</span></span> <span data-ttu-id="881a0-193">Merhaba teması hello web uygulaması, güncelleştirilmiş toobe bulunduğu bir senaryoyu göz önünde bulundurularak, web uygulaması hazırlama hello aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="881a0-193">Considering a scenario where hello theme of hello web app is toobe updated, here is hello staging web app.</span></span>

    ![Web uygulaması yuvaları takas önce hazırlama Gözat](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. <span data-ttu-id="881a0-195">Tüm görünüyorsa iyi, hello tıklatın **takas** üzerinde hazırlama web uygulama toomove içerik toohello üretim ortamınıza düğmesi.</span><span class="sxs-lookup"><span data-stu-id="881a0-195">If all looks good, click hello **Swap** button on your staging web app toomove your content toohello production environment.</span></span> <span data-ttu-id="881a0-196">Bu durumda, hello web app ve hello veritabanı sırasında ortamlar üzerinde takas her **takas** işlemi.</span><span class="sxs-lookup"><span data-stu-id="881a0-196">In this case, you swap hello web app and hello database across environments during every **Swap** operation.</span></span>

    ![Önizleme değişiklikleri için WordPress değiştirme](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > <span data-ttu-id="881a0-198">Senaryonuz tooonly zorlama dosyaların (veritabanı güncelleştirmeleri) gerekiyorsa, ardından denetleyin **yuva ayarı** tüm hello veritabanıyla ilgili için *uygulama ayarları* ve *bağlantı dizeleri ayarları*hello içinde **Web uygulaması ayarları** dikey penceresinde hello hello yapmadan önce Azure portalı içinde **takas**.</span><span class="sxs-lookup"><span data-stu-id="881a0-198">If your scenario needs tooonly push files (no database updates), then check **Slot Setting** for all hello database-related *app settings* and *connection strings settings* in hello **Web App Settings** blade within hello Azure portal before doing hello **Swap**.</span></span> <span data-ttu-id="881a0-199">Bunu yaptığınızda bu durumda, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER ve varsayılan bağlantı dizesi ayarlarının Önizleme değişiklikleri gösterilmesi gerekir olmayan bir **takas**.</span><span class="sxs-lookup"><span data-stu-id="881a0-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span></span> <span data-ttu-id="881a0-200">Şu anda hello tamamlandığında **takas** işlemi, WordPress web uygulaması Hello ifadesini sahip hello yalnızca dosyalar güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="881a0-200">At this time, when you complete hello **Swap** operation, hello WordPress web app will have hello updates files only.</span></span>
    >
    >

    <span data-ttu-id="881a0-201">Bunu yaptığınızda önce bir **takas**, hello üretim WordPress web uygulaması aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="881a0-201">Before doing a **Swap**, here is hello production WordPress web app.</span></span>
    <span data-ttu-id="881a0-202">![Üretim web uygulaması yuvaları takas önce](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span><span class="sxs-lookup"><span data-stu-id="881a0-202">![Production web app before swapping slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span></span>

    <span data-ttu-id="881a0-203">Merhaba sonra **takas** işlemi, hello tema üretim web uygulamanız güncelleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="881a0-203">After hello **Swap** operation, hello theme has been updated on your production web app.</span></span>

    ![Üretim web uygulaması yuvaları takas sonra](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. <span data-ttu-id="881a0-205">Geri tooroll gerektiğinde toohello üretim web gidebilirsiniz **uygulama ayarları**, hello tıklatıp **takas** düğmesini tooswap hello web app ve üretim toostaging yuvası veritabanından.</span><span class="sxs-lookup"><span data-stu-id="881a0-205">When you need tooroll back, you can go toohello production web **App Settings**, and click hello **Swap** button tooswap hello web app and database from production toostaging slot.</span></span> <span data-ttu-id="881a0-206">Veritabanı değişiklikleri birlikte olup olmadığını unutmayın bir **takas** işlemi sonra hello web uygulaması hazırlama tooyour dağıttığınız sonraki sefer hazırlama web uygulamanız için toodeploy hello veritabanı değişiklikleri toohello geçerli veritabanınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="881a0-206">Remember that if database changes are included with a **Swap** operation, then hello next time you deploy tooyour staging web app, you need toodeploy hello database changes toohello current database for your staging web app.</span></span> <span data-ttu-id="881a0-207">Merhaba geçerli veritabanı hello önceki üretim veritabanını veya hello aşama veritabanını olabilir.</span><span class="sxs-lookup"><span data-stu-id="881a0-207">hello current database might be hello previous production database or hello stage database.</span></span>

#### <a name="summary"></a><span data-ttu-id="881a0-208">Özet</span><span class="sxs-lookup"><span data-stu-id="881a0-208">Summary</span></span>
<span data-ttu-id="881a0-209">Aşağıda, bir veritabanı sahip herhangi bir uygulama için genelleştirilmiş bir işlemdir:</span><span class="sxs-lookup"><span data-stu-id="881a0-209">Following is a generalized process for any application that has a database:</span></span>

1. <span data-ttu-id="881a0-210">Merhaba uygulaması yerel ortamınıza yükleyin.</span><span class="sxs-lookup"><span data-stu-id="881a0-210">Install hello application on your local environment.</span></span>
2. <span data-ttu-id="881a0-211">Ortama özgü yapılandırmaları (yerel ve Azure Web Apps) içerir.</span><span class="sxs-lookup"><span data-stu-id="881a0-211">Include environment-specific configurations (local and Azure Web Apps).</span></span>
3. <span data-ttu-id="881a0-212">Web uygulamaları için hazırlama ve üretim ortamları ayarlama.</span><span class="sxs-lookup"><span data-stu-id="881a0-212">Set up your staging and production environments for Web Apps.</span></span>
4. <span data-ttu-id="881a0-213">Zaten Azure üzerinde çalışan bir üretim uygulamanız varsa, üretim içerik (dosyalar/kod ve veritabanı) toolocal ve hazırlama ortamları eşitleyin.</span><span class="sxs-lookup"><span data-stu-id="881a0-213">If you have a production application already running on Azure, sync your production content (files/code and database) toolocal and staging environments.</span></span>
5. <span data-ttu-id="881a0-214">Uygulamanızı yerel ortamınızda geliştirin.</span><span class="sxs-lookup"><span data-stu-id="881a0-214">Develop your application on your local environment.</span></span>
6. <span data-ttu-id="881a0-215">Üretim web uygulamanız Bakım veya kilitli modu altında yerleştirin ve üretim toostaging ve geliştirme ortamlarını veritabanı içerikten eşitleyin.</span><span class="sxs-lookup"><span data-stu-id="881a0-215">Place your production web app under maintenance or locked mode, and sync database content from production toostaging and dev environments.</span></span>
7. <span data-ttu-id="881a0-216">Hazırlama ortamı ve test toohello dağıtın.</span><span class="sxs-lookup"><span data-stu-id="881a0-216">Deploy toohello staging environment and test.</span></span>
8. <span data-ttu-id="881a0-217">Tooproduction ortamı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="881a0-217">Deploy tooproduction environment.</span></span>
9. <span data-ttu-id="881a0-218">4 ile 6 arasındaki adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="881a0-218">Repeat steps 4 through 6.</span></span>

### <a name="umbraco"></a><span data-ttu-id="881a0-219">Umbraco</span><span class="sxs-lookup"><span data-stu-id="881a0-219">Umbraco</span></span>
<span data-ttu-id="881a0-220">Bu bölümde, hello Umbraco CMS özel modülü toodeploy birden çok DevOps ortamlar genelinde nasıl kullandığını öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="881a0-220">In this section, you will learn how hello Umbraco CMS uses a custom module toodeploy across multiple DevOps environments.</span></span> <span data-ttu-id="881a0-221">Bu örnekte, farklı bir yaklaşım toomanaging birden çok geliştirme ortamı sağlar.</span><span class="sxs-lookup"><span data-stu-id="881a0-221">This example provides a different approach toomanaging multiple development environments.</span></span>

<span data-ttu-id="881a0-222">[Umbraco CMS](http://umbraco.com/) birçok geliştiriciler tarafından kullanılan bir popüler .NET CMS çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="881a0-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span></span> <span data-ttu-id="881a0-223">Merhaba sağlar [Courier2](http://umbraco.com/products/more-add-ons/courier-2) geliştirme toostaging tooproduction ortamlarından modülü toodeploy.</span><span class="sxs-lookup"><span data-stu-id="881a0-223">It provides hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module toodeploy from development toostaging tooproduction environments.</span></span> <span data-ttu-id="881a0-224">WebMatrix veya Visual Studio'yu kullanarak kolayca bir Umbraco CMS web uygulaması için bir yerel geliştirme ortamı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="881a0-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span></span>

- [<span data-ttu-id="881a0-225">Visual Studio ile bir Umbraco web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="881a0-225">Create an Umbraco web app with Visual Studio</span></span>](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [<span data-ttu-id="881a0-226">WebMatrix ile bir Umbraco web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="881a0-226">Create an Umbraco web app with WebMatrix</span></span>](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

<span data-ttu-id="881a0-227">Her zaman tooremove hello unutmayın `install` , uygulamanızın altında bir klasör ve hiçbir zaman toostage veya üretim web uygulamaları karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="881a0-227">Always remember tooremove hello `install` folder under your application, and never upload it toostage or production web apps.</span></span> <span data-ttu-id="881a0-228">Bu öğretici, WebMatrix kullanır.</span><span class="sxs-lookup"><span data-stu-id="881a0-228">This tutorial uses WebMatrix.</span></span>

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="881a0-229">Hazırlama ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="881a0-229">Set up a staging environment</span></span>
1. <span data-ttu-id="881a0-230">Bir dağıtım yuvası Merhaba Umbraco CMS web uygulaması zaten varsa ve çalıştırma Umbraco CMS web uygulaması, daha önce belirtildiği gibi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="881a0-230">Create a deployment slot as mentioned previously for hello Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span></span> <span data-ttu-id="881a0-231">Bunu yapmazsanız, hello Market birinden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="881a0-231">If you do not, you can create one from hello Marketplace.</span></span>
2. <span data-ttu-id="881a0-232">Merhaba bağlantı dizesi, aşama dağıtım yuvası toopoint toohello yeni güncelleştirme **umbraco aşama db** veritabanı.</span><span class="sxs-lookup"><span data-stu-id="881a0-232">Update hello connection string for your stage deployment slot toopoint toohello new **umbraco-stage-db** database.</span></span> <span data-ttu-id="881a0-233">Üretim web uygulaması (umbraositecms-1) ve hazırlama web uygulaması (umbracositecms-1-aşama) *gerekir* noktası toodifferent veritabanları.</span><span class="sxs-lookup"><span data-stu-id="881a0-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point toodifferent databases.</span></span>

    ![Yeni hazırlama veritabanı ile web uygulaması hazırlama için kullanılan bağlantı dizesi güncelleştir](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. <span data-ttu-id="881a0-235">Tıklatın **alma yayımlama ayarları** hello dağıtım yuvası için **aşama**.</span><span class="sxs-lookup"><span data-stu-id="881a0-235">Click **Get Publish settings** for hello deployment slot **stage**.</span></span> <span data-ttu-id="881a0-236">Bu işlem, Visual Studio veya WebMatrix toopublish uygulamanızın hello yerel geliştirme web uygulama toohello Azure web uygulamasından gerektirdiği tüm hello bilgileri depolayan bir yayımlama ayarları dosyası indirir.</span><span class="sxs-lookup"><span data-stu-id="881a0-236">This process will download a publish settings file that stores all hello information that Visual Studio or WebMatrix requires toopublish your application from hello local development web app toohello Azure web app.</span></span>

    ![Get yayımlama hello web uygulaması hazırlama ayarı](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. <span data-ttu-id="881a0-238">Yerel geliştirme web uygulamanızı WebMatrix veya Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="881a0-238">Open your local development web app in WebMatrix or Visual Studio.</span></span> <span data-ttu-id="881a0-239">Bu öğretici, WebMatrix kullanır.</span><span class="sxs-lookup"><span data-stu-id="881a0-239">This tutorial uses WebMatrix.</span></span> <span data-ttu-id="881a0-240">Öncelikle, tooimport hello gerekir yayımlama ayarları dosyası hazırlama web uygulamanız için.</span><span class="sxs-lookup"><span data-stu-id="881a0-240">First, you need tooimport hello publish settings file for your staging web app.</span></span>

    ![Web Matrix kullanarak Umbraco yayımlama ayarlarını içeri aktarma](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. <span data-ttu-id="881a0-242">Merhaba iletişim kutusunda değişiklikleri gözden geçirin ve, yerel web uygulaması tooyour Azure web uygulaması dağıtma *umbracositecms 1 aşama*.</span><span class="sxs-lookup"><span data-stu-id="881a0-242">Review changes in hello dialog box, and deploy your local web app tooyour Azure web app, *umbracositecms-1-stage*.</span></span> <span data-ttu-id="881a0-243">Tooyour hazırlama web doğrudan uygulama dosyaları dağıttığınızda, hello dosyalarında atlayacak `~/app_data/TEMP/` hello aşama web uygulaması ilk çalıştırıldığında bu dosyalar yeniden oluşturulacak olmadığından klasör başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="881a0-243">When you deploy files directly tooyour staging web app, you will omit files in hello `~/app_data/TEMP/` folder because these files will be regenerated when hello stage web app is first started.</span></span> <span data-ttu-id="881a0-244">Merhaba atlayın `~/app_data/umbraco.config` de yeniden oluşturulacak dosya.</span><span class="sxs-lookup"><span data-stu-id="881a0-244">You should also omit hello `~/app_data/umbraco.config` file, which will also be regenerated.</span></span>

    ![Web Matristeki Yayımla değişiklikleri gözden geçirin](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. <span data-ttu-id="881a0-246">Merhaba Umbraco yerel web uygulama toohello hazırlama web uygulaması başarıyla yayımladıktan sonra tooyour hazırlama web uygulaması göz atın ve sorunları çıkışı birkaç testleri toorule çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="881a0-246">After you successfully publish hello Umbraco local web app toohello staging web app, browse tooyour staging web app, and run a few tests toorule out any issues.</span></span>

#### <a name="set-up-hello-courier2-deployment-module"></a><span data-ttu-id="881a0-247">Merhaba Courier2 dağıtım modülünü kurun</span><span class="sxs-lookup"><span data-stu-id="881a0-247">Set up hello Courier2 deployment module</span></span>
<span data-ttu-id="881a0-248">Merhaba ile [Courier2](http://umbraco.com/products/more-add-ons/courier-2) modülü, yalnızca toopush içerik, stil sayfaları ve bir hazırlama web uygulama tooa üretim web uygulaması geliştirme modüllerden tıklayabilir.</span><span class="sxs-lookup"><span data-stu-id="881a0-248">With hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click toopush content, style sheets, and development modules from a staging web app tooa production web app.</span></span> <span data-ttu-id="881a0-249">Bu işlem bir güncelleştirme dağıttığınızda üretim web uygulamanız çiğnemekten hello riskini azaltır.</span><span class="sxs-lookup"><span data-stu-id="881a0-249">This process reduces hello risk of breaking your production web app when you deploy an update.</span></span>
<span data-ttu-id="881a0-250">Merhaba Courier2 için bir lisans satın `*.azurewebsites.net` etki alanı ve özel etki alanınızı (örneğin http://abc.com).</span><span class="sxs-lookup"><span data-stu-id="881a0-250">Purchase a license for Courier2 for hello `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span></span> <span data-ttu-id="881a0-251">Merhaba lisans satın aldıktan sonra lisans yer hello indirilen (. Lisans Sözleşmesi dosyası) hello içinde `bin` klasör.</span><span class="sxs-lookup"><span data-stu-id="881a0-251">After you purchase hello license, place hello downloaded license (.LIC file) in hello `bin` folder.</span></span>

![Bin klasörü altındaki açılan lisans dosyası](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. <span data-ttu-id="881a0-253">[Merhaba Courier2 paketini indirin](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span><span class="sxs-lookup"><span data-stu-id="881a0-253">[Download hello Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span></span> <span data-ttu-id="881a0-254">Tooyour aşama web uygulamasında, deyin http://umbracocms-site-stage.azurewebsites.net/umbraco işaretini tıklatın hello **Geliştirici** menüsüne ve ardından **paketleri** > **yükleyin Yerel Paket**.</span><span class="sxs-lookup"><span data-stu-id="881a0-254">Sign in tooyour stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click hello **Developer** menu, and then click **Packages** > **Install local package**.</span></span>

    ![Umbraco paketi yükleyicisi](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. <span data-ttu-id="881a0-256">Merhaba Courier2 paket hello yükleyicisini kullanarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="881a0-256">Upload hello Courier2 package by using hello installer.</span></span>

    ![Paketi courier modülü için yükleme](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. <span data-ttu-id="881a0-258">tooconfigure hello paket tooupdate hello courier.config dosya hello altında ihtiyacınız **Config** klasör, web uygulamanızın.</span><span class="sxs-lookup"><span data-stu-id="881a0-258">tooconfigure hello package, you need tooupdate hello courier.config file under hello **Config** folder of your web app.</span></span>

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

4. <span data-ttu-id="881a0-259">Altında `<repositories>`, Merhaba, üretim site URL'si ve kullanıcı bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="881a0-259">Under `<repositories>`, enter hello production site URL and user information.</span></span>
    <span data-ttu-id="881a0-260">Merhaba varsayılan Umbraco üyelik sağlayıcısı kullanıyorsanız, hello yönetim kullanıcının hello kimliği hello ekleyin &lt;kullanıcı&gt; bölümü.</span><span class="sxs-lookup"><span data-stu-id="881a0-260">If you are using hello default Umbraco membership provider, then add hello ID for hello Administration user in hello &lt;user&gt; section.</span></span>
    <span data-ttu-id="881a0-261">Özel bir Umbraco üyelik sağlayıcısı kullanıyorsanız `<login>`,`<password>` hello Courier2 modülü tooconnect toohello üretim sitedeki.</span><span class="sxs-lookup"><span data-stu-id="881a0-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in hello Courier2 module tooconnect toohello production site.</span></span>
    <span data-ttu-id="881a0-262">Daha fazla ayrıntı için [hello Courier2 modülü için hello belgelerini gözden geçirin](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span><span class="sxs-lookup"><span data-stu-id="881a0-262">For more details, [review hello documentation for hello Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span></span>

5. <span data-ttu-id="881a0-263">Benzer şekilde, üretim sitenizde hello Courier2 modülünü yüklemek ve aşağıda gösterildiği gibi ilgili courier.config dosyasında toopoint toohello aşama web uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="881a0-263">Similarly, install hello Courier2 module on your production site, and configure it toopoint toohello stage web app in its respective courier.config file as shown here.</span></span>

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

6. <span data-ttu-id="881a0-264">Merhaba tıklatın **Courier2** sekmesinde hello Umbraco CMS web uygulaması Pano ve ardından **konumları**.</span><span class="sxs-lookup"><span data-stu-id="881a0-264">Click hello **Courier2** tab in hello Umbraco CMS web app dashboard, and then click **Locations**.</span></span> <span data-ttu-id="881a0-265">Bölümünde belirtildiği gibi hello depo adını görmeniz gerekir `courier.config`.</span><span class="sxs-lookup"><span data-stu-id="881a0-265">You should see hello repository name as mentioned in `courier.config`.</span></span> <span data-ttu-id="881a0-266">Üretim ve hazırlama web uygulamaları üzerinde bu işlemi yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="881a0-266">Do this process on both your production and staging web apps.</span></span>

    ![Görünüm hedef web uygulama havuzu](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. <span data-ttu-id="881a0-268">toohello üretim siteler, hazırlama hello toodeploy içerikten Git çok**içerik**ve varolan bir sayfayı seçebilir veya yeni bir sayfa oluşturun.</span><span class="sxs-lookup"><span data-stu-id="881a0-268">toodeploy content from hello staging site toohello production site, go too**Content**, and select an existing page or create a new page.</span></span> <span data-ttu-id="881a0-269">Varolan bir sayfayı hello sayfasının hello başlığını olduğu my web uygulamasından seçecektir **başlarken – yeni**ve ardından **kaydetmek ve yayımlamak**.</span><span class="sxs-lookup"><span data-stu-id="881a0-269">I will select an existing page from my web app where hello title of hello page is **Getting Started – new**, and then click **Save and Publish**.</span></span>

    ![Sayfasının başlığını değiştirme ve yayımlama](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. <span data-ttu-id="881a0-271">Sağ hello tüm hello Seçenekleri sayfası tooview değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="881a0-271">Right-click hello modified page tooview all hello options.</span></span> <span data-ttu-id="881a0-272">Tıklatın **Courier** tooopen hello **dağıtım** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="881a0-272">Click **Courier** tooopen hello **Deployment** dialog box.</span></span> <span data-ttu-id="881a0-273">Tıklatın **dağıtma** tooinitiate dağıtım.</span><span class="sxs-lookup"><span data-stu-id="881a0-273">Click **Deploy** tooinitiate deployment.</span></span>

    ![Courier modülü dağıtım iletişim](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. <span data-ttu-id="881a0-275">Merhaba değişiklikleri gözden geçirin ve ardından **devam**.</span><span class="sxs-lookup"><span data-stu-id="881a0-275">Review hello changes, and then click **Continue**.</span></span>

    ![Courier modülü dağıtım iletişim değişiklikleri gözden geçir](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    <span data-ttu-id="881a0-277">Merhaba dağıtım günlüğü hello dağıtım başarılı olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="881a0-277">hello deployment log shows if hello deployment was successful.</span></span>

     ![Courier modülden dağıtım günlüklerini görüntüle](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. <span data-ttu-id="881a0-279">Merhaba değişiklikler yansıtılır varsa, üretim web uygulama toosee göz atın.</span><span class="sxs-lookup"><span data-stu-id="881a0-279">Browse your production web app toosee if hello changes are reflected.</span></span>

     ![Üretim web uygulamasına göz atın](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

<span data-ttu-id="881a0-281">toolearn nasıl toouse Courier, gözden geçirme hello belgeleri hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="881a0-281">toolearn more about how toouse Courier, review hello documentation.</span></span>

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a><span data-ttu-id="881a0-282">Nasıl tooupgrade hello Umbraco CMS sürümü</span><span class="sxs-lookup"><span data-stu-id="881a0-282">How tooupgrade hello Umbraco CMS version</span></span>
<span data-ttu-id="881a0-283">Courier Umbraco CMS tooanother bir sürümünden yükseltme Yardımı.</span><span class="sxs-lookup"><span data-stu-id="881a0-283">Courier will not help you upgrade from one version of Umbraco CMS tooanother.</span></span> <span data-ttu-id="881a0-284">Bir Umbraco CMS sürümüne yükselttiğinizde, özel modüller veya iş ortakları modüllerden uyumsuzluklar denetleyin ve Umbraco çekirdek kitaplıkları hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="881a0-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and hello Umbraco Core libraries.</span></span> <span data-ttu-id="881a0-285">En iyi uygulamalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="881a0-285">Here are best practices:</span></span>

* <span data-ttu-id="881a0-286">Yükseltmeden önce her zaman, web uygulaması ve veritabanı yedekleme.</span><span class="sxs-lookup"><span data-stu-id="881a0-286">Always back up your web app and database before you upgrade.</span></span> <span data-ttu-id="881a0-287">Azure Web uygulamaları üzerinde hello yedekleme özelliğini kullanarak, Web siteleri için Otomatik yedekler ayarlamak ve hello geri yükleme özelliğini kullanarak gerekirse sitenize geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="881a0-287">On web apps in Azure, you can set up automatic backups for your websites by using hello backup feature and restore your site if needed by using hello restore feature.</span></span> <span data-ttu-id="881a0-288">Daha fazla ayrıntı için bkz: [nasıl web uygulamanızı yedekleme tooback](web-sites-backup.md) ve [nasıl toorestore web uygulamanızı](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="881a0-288">For more details, see [How tooback up your web app](web-sites-backup.md) and [How toorestore your web app](web-sites-restore.md).</span></span>
* <span data-ttu-id="881a0-289">İş ortakları paketlerinden yükseltme yapıyorsanız hello sürümüyle uyumlu olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="881a0-289">Check if packages from partners are compatible with hello version you're upgrading to.</span></span> <span data-ttu-id="881a0-290">Merhaba paketin üzerinde sayfa yükleme, Umbraco CMS sürümüyle hello proje uyumluluğu gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="881a0-290">On hello package's download page, review hello project compatibility with Umbraco CMS version.</span></span>

<span data-ttu-id="881a0-291">Nasıl hakkında daha fazla ayrıntı için tooupgrade web uygulamanızı yerel olarak [hello genel yükseltme yönergelere bakın](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span><span class="sxs-lookup"><span data-stu-id="881a0-291">For more details about how tooupgrade your web app locally, [see hello general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span></span>

<span data-ttu-id="881a0-292">Yerel geliştirme sitenizi yükselttikten sonra web uygulaması hazırlama hello değişiklikleri toohello yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="881a0-292">After your local development site is upgraded, publish hello changes toohello staging web app.</span></span> <span data-ttu-id="881a0-293">Uygulamanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="881a0-293">Test your application.</span></span> <span data-ttu-id="881a0-294">Tüm görünüyorsa iyi, hello kullanın **takas** tooswap hazırlama sitesi toohello üretim web uygulamanız düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="881a0-294">If all looks good, use hello **Swap** button tooswap your staging site toohello production web app.</span></span> <span data-ttu-id="881a0-295">Merhaba kullandığınızda **takas** işlemi, web uygulamanızın yapılandırmasında etkilenecek hello değişiklikleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="881a0-295">When you use hello **Swap** operation, you can view hello changes that will be affected in your web app's configuration.</span></span> <span data-ttu-id="881a0-296">Bu **takas** işlemi hello web uygulamaları ve veritabanları ile değiştirir.</span><span class="sxs-lookup"><span data-stu-id="881a0-296">This **Swap** operation swaps hello web apps and databases.</span></span> <span data-ttu-id="881a0-297">Merhaba sonra **takas**hello üretim web uygulaması olacak noktası toohello umbraco aşama db veritabanı ve hazırlama web uygulaması olacak noktası tooumbraco üretim db veritabanı hello.</span><span class="sxs-lookup"><span data-stu-id="881a0-297">After hello **Swap**, hello production web app will point toohello umbraco-stage-db database, and hello staging web app will point tooumbraco-prod-db database.</span></span>

![Umbraco CMS dağıtmak için Önizleme değiştirme](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

<span data-ttu-id="881a0-299">Merhaba web app ve hello veritabanı takas avantajları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="881a0-299">Here are advantages of swapping both hello web app and hello database:</span></span>

* <span data-ttu-id="881a0-300">Web uygulamanızı başka ile toohello önceki sürümünü geri alabilirsiniz **takas** herhangi bir uygulama sorun varsa.</span><span class="sxs-lookup"><span data-stu-id="881a0-300">You can roll back toohello previous version of your web app with another **Swap** if there are any application issues.</span></span>
* <span data-ttu-id="881a0-301">Yükseltme için toodeploy dosyaları ve web uygulama toohello üretim web uygulaması hazırlama hello veritabanlarından ve veritabanını gerekir.</span><span class="sxs-lookup"><span data-stu-id="881a0-301">For an upgrade, you need toodeploy files and databases from hello staging web app toohello production web app and database.</span></span> <span data-ttu-id="881a0-302">Dosyaları ve veritabanları dağıttığınızda pek çok yanlış gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="881a0-302">Many things can go wrong when you deploy files and databases.</span></span> <span data-ttu-id="881a0-303">Hello kullanarak **takas** özelliği yuvaları biz yükseltme sırasında kapalı kalma süresini kısaltabilir ve değişiklikleri dağıtırken oluşabilecek hatalar hello riskini azaltır.</span><span class="sxs-lookup"><span data-stu-id="881a0-303">By using hello **Swap** feature of slots, we can reduce downtime during an upgrade and reduce hello risk of failures that can occur when you deploy changes.</span></span>
* <span data-ttu-id="881a0-304">Yapabileceğiniz **A / B testi** hello kullanarak [üretimde test](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) özelliği.</span><span class="sxs-lookup"><span data-stu-id="881a0-304">You can do **A/B testing** by using hello [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span></span>

<span data-ttu-id="881a0-305">Burada özel modüller benzer tooUmbraco Courier modülü toomanage dağıtımı ortamlar genelinde oluşturabileceğiniz hello platform esnekliğini hello Bu örnek gösterir.</span><span class="sxs-lookup"><span data-stu-id="881a0-305">This example shows you hello flexibility of hello platform where you can build custom modules similar tooUmbraco Courier module toomanage deployment across environments.</span></span>

## <a name="references"></a><span data-ttu-id="881a0-306">Başvurular</span><span class="sxs-lookup"><span data-stu-id="881a0-306">References</span></span>
[<span data-ttu-id="881a0-307">Azure App Service ile Çevik Yazılım Geliştirme</span><span class="sxs-lookup"><span data-stu-id="881a0-307">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)

[<span data-ttu-id="881a0-308">Hazırlık ortamları için Azure App Service'te web uygulamalarını ayarlama</span><span class="sxs-lookup"><span data-stu-id="881a0-308">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)

[<span data-ttu-id="881a0-309">Nasıl tooblock web erişim toonon üretim dağıtım yuvaları</span><span class="sxs-lookup"><span data-stu-id="881a0-309">How tooblock web access toonon-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
