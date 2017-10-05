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
# <a name="use-devops-environments-effectively-for-your-web-apps"></a><span data-ttu-id="61a3f-103">DevOps ortamları etkili bir şekilde web uygulamaları için kullanın</span><span class="sxs-lookup"><span data-stu-id="61a3f-103">Use DevOps environments effectively for your web apps</span></span>
<span data-ttu-id="61a3f-104">Bu makalede ayarlama ve birden çok sürümü, uygulamanızın, geliştirme, hazırlama, kalite güvence (QA) ve üretim gibi çeşitli ortamlarda olduğunda web uygulama dağıtımlarını yönetin gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-104">This article shows you how to set up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="61a3f-105">Her bir sürümü, uygulamanızın bir geliştirme ortamı, dağıtım işlemi belirli amaç için kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-105">Each version of your application can be considered as a development environment for the specific purpose of your deployment process.</span></span> <span data-ttu-id="61a3f-106">Örneğin, geliştiriciler, QA ortamı bunlar değişiklikleri üretime sokmadan önce uygulama kalitesini test etmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61a3f-106">For example, developers can use the QA environment to test the quality of the application before they push the changes to production.</span></span>
<span data-ttu-id="61a3f-107">Kod izlemek, kaynakların (hesaplama, web uygulaması, veritabanı, önbellek, vb.) yönetmek ve kod ortamlar genelinde dağıtmak gerektiğinden birden çok geliştirme ortamlarını zor olabilir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-107">Multiple development environments can be a challenge because you need to track code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span></span>

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a><span data-ttu-id="61a3f-108">Bir üretim dışı ortamını (aşaması, geliştirme, QA) ayarlama</span><span class="sxs-lookup"><span data-stu-id="61a3f-108">Set up a non-production environment (stage, dev, QA)</span></span>
<span data-ttu-id="61a3f-109">Bir üretim web uygulaması çalışır durumda sonra sonraki adım bir üretim ortamı dışındaki oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="61a3f-109">After a production web app is up and running, the next step is to create a non-production environment.</span></span> <span data-ttu-id="61a3f-110">Dağıtım yuvası kullanmak için standart veya Premium Azure uygulama hizmeti planı modunda çalışır durumda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="61a3f-110">To use deployment slots, make sure that you are running in the Standard or Premium Azure App Service plan mode.</span></span> <span data-ttu-id="61a3f-111">Dağıtım yuvaları, kendi ana bilgisayar adları olan canlı web uygulamalardır.</span><span class="sxs-lookup"><span data-stu-id="61a3f-111">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="61a3f-112">Web uygulaması içerik ve yapılandırma öğeleri üretim yuvası da dahil olmak üzere iki dağıtım yuvası arasında değişiklik yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-112">Web app content and configuration elements can be swapped between two deployment slots, including the production slot.</span></span> <span data-ttu-id="61a3f-113">Bir dağıtım yuvası uygulamanıza dağıttığınızda, aşağıdaki faydaları alın:</span><span class="sxs-lookup"><span data-stu-id="61a3f-113">When you deploy your application to a deployment slot, you get the following benefits:</span></span>

- <span data-ttu-id="61a3f-114">Uygulamayı, üretim yuvası takas önce hazırlık dağıtım yuvasındaki web uygulamasında değişiklikler doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61a3f-114">You can validate changes to a web app in a staging deployment slot before you swap the app with the production slot.</span></span>
- <span data-ttu-id="61a3f-115">Bir web uygulaması yuvası için ilk dağıtma ve üretim ortamına takas yuvası tüm örneklerini üretime takas önce warmed.</span><span class="sxs-lookup"><span data-stu-id="61a3f-115">When you deploy a web app to a slot first and swap it into production, all instances of the slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="61a3f-116">Bu işlem, web uygulamanızı dağıtırken kapalı kalma süresini ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="61a3f-116">This process eliminates downtime when you deploy your web app.</span></span> <span data-ttu-id="61a3f-117">Trafik yeniden yönlendirmesi sorunsuzdur ve değiştirme işlemleri nedeniyle hiçbir istek bırakılır.</span><span class="sxs-lookup"><span data-stu-id="61a3f-117">The traffic redirection is seamless, and no requests are dropped due to swap operations.</span></span> <span data-ttu-id="61a3f-118">Bu iş akışının tamamı otomatikleştirmek için yapılandırma [otomatik takas](web-sites-staged-publishing.md#configure-auto-swap) zaman öncesi takas doğrulama gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-118">To automate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span></span>
- <span data-ttu-id="61a3f-119">Değiştirme işleminden sonra önceden hazırlanmış web uygulaması şimdi sahip yuvası önceki üretim web uygulamasına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-119">After a swap, the slot that has the previously staged web app now has the previous production web app.</span></span> <span data-ttu-id="61a3f-120">Beklendiği gibi üretim yuvasına değişiklikleri varsa, "bilinen son iyi" web almak için uygulama geri hemen aynı değiştirme işlemini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61a3f-120">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good" web app back.</span></span>

<span data-ttu-id="61a3f-121">Hazırlık dağıtım yuvasındaki ayarlamak için bkz: [hazırlık Azure App Service'deki web uygulamaları için ortamları ayarlama](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="61a3f-121">To set up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="61a3f-122">Her ortam kaynakları kendi kümesini içermelidir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-122">Every environment should include its own set of resources.</span></span> <span data-ttu-id="61a3f-123">Web uygulamanız bir veritabanı kullanıyorsa, örneğin, daha sonra hem üretim hem de web uygulamaları hazırlama farklı veritabanları kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span></span> <span data-ttu-id="61a3f-124">Veritabanı, depolama veya hazırlama geliştirme ortamınızı ayarlamak için önbellek gibi hazırlama geliştirme ortamı kaynakları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="61a3f-124">Add staging development environment resources such as database, storage, or cache to set your staging development environment.</span></span>

## <a name="examples-of-using-multiple-development-environments"></a><span data-ttu-id="61a3f-125">Birden çok geliştirme ortamı kullanma örnekleri</span><span class="sxs-lookup"><span data-stu-id="61a3f-125">Examples of using multiple development environments</span></span>
<span data-ttu-id="61a3f-126">Herhangi bir projenin kaynak kodu yönetimi en az iki ortamlarla izlemelidir: geliştirme ve üretim.</span><span class="sxs-lookup"><span data-stu-id="61a3f-126">Any project should follow source code management with at least two environments: development and production.</span></span> <span data-ttu-id="61a3f-127">İçerik yönetim sistemleri (CMSs), uygulama çerçeveleri, vb. kullanırsanız uygulamanın bu senaryo özelleştirme olmadan desteklemeyebilir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-127">If you use content management systems (CMSs), application frameworks, etc., the application might not support this scenario without customization.</span></span> <span data-ttu-id="61a3f-128">Bu planlıyorsanız, aşağıdaki bölümlerde açıklanan popüler uygulamayı bazıları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-128">This eventuality is true for some of the popular frameworks that are discussed in the following sections.</span></span> <span data-ttu-id="61a3f-129">CMS/çerçeveleri ile gibi çalışırken soruları birçok aklınıza getirir:</span><span class="sxs-lookup"><span data-stu-id="61a3f-129">Lots of questions come to mind when you work with CMS/frameworks, such as:</span></span>

- <span data-ttu-id="61a3f-130">Nasıl, içeriği farklı ortamlara başlama?</span><span class="sxs-lookup"><span data-stu-id="61a3f-130">How do you break the content out into different environments?</span></span>
- <span data-ttu-id="61a3f-131">Hangi dosyaların framework sürüm güncelleştirmelerini etkilemeden değiştirebilir miyim?</span><span class="sxs-lookup"><span data-stu-id="61a3f-131">What files can you change without affecting framework version updates?</span></span>
- <span data-ttu-id="61a3f-132">Ortam başına yapılandırmaları nasıl yönettiğiniz?</span><span class="sxs-lookup"><span data-stu-id="61a3f-132">How do you manage configurations per environment?</span></span>
- <span data-ttu-id="61a3f-133">Modüller, eklenti ve çekirdek framework sürüm güncelleştirmelerini nasıl yönettiğiniz?</span><span class="sxs-lookup"><span data-stu-id="61a3f-133">How do you manage version updates for modules, plugins, and the core framework?</span></span>

<span data-ttu-id="61a3f-134">Projeniz için birden çok ortamları ayarlamak için birçok yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="61a3f-134">There are many ways to set up multiple environments for your project.</span></span> <span data-ttu-id="61a3f-135">Aşağıdaki örnekler, ilgili her uygulama için bir yöntemi gösterir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-135">The following examples show one method for each respective application.</span></span>

### <a name="wordpress"></a><span data-ttu-id="61a3f-136">WordPress</span><span class="sxs-lookup"><span data-stu-id="61a3f-136">WordPress</span></span>
<span data-ttu-id="61a3f-137">Bu bölümde, WordPress için yuvaları kullanarak bir dağıtım iş akışını Ayarla öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="61a3f-137">In this section, you will learn how to set up a deployment workflow by using slots for WordPress.</span></span> <span data-ttu-id="61a3f-138">WordPress, çoğu CMS çözümleri gibi özelleştirme olmadan birden fazla geliştirme ortamları desteklemez.</span><span class="sxs-lookup"><span data-stu-id="61a3f-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span></span> <span data-ttu-id="61a3f-139">Azure App Service Web Apps özelliğidir kodunuzu dışında yapılandırma ayarlarını depolamak kolaylaştıran birkaç özelliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-139">The Web Apps feature of Azure App Service has a few features that make it easy to store configuration settings outside your code.</span></span>

1. <span data-ttu-id="61a3f-140">Hazırlama yuvası oluşturmadan önce birden çok ortamlarını desteklemek için uygulama kodunuz ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="61a3f-140">Before you create a staging slot, set up your application code to support multiple environments.</span></span> <span data-ttu-id="61a3f-141">WordPress içinde birden çok ortamlarını desteklemek için düzenlemeniz gerekir `wp-config.php` yerel geliştirme üzerinde web uygulaması ve dosyasının başında aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="61a3f-141">To support multiple environments in WordPress, you need to edit `wp-config.php` on your local development web app and add the following code at the beginning of the file.</span></span> <span data-ttu-id="61a3f-142">Bu işlem, seçili ortamına bağlı doğru yapılandırmayı almak uygulamanızı olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="61a3f-142">This process will enable your application to pick the correct configuration based on the selected environment.</span></span>

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

2. <span data-ttu-id="61a3f-143">Adlı web uygulama kökü altındaki bir klasör oluşturun `config`ve ekleme `wp-config.azure.php` ve `wp-config.local.php` Azure ortamı ve yerel ortamı sırasıyla temsil dosyaları.</span><span class="sxs-lookup"><span data-stu-id="61a3f-143">Create a folder under web app root called `config`, and add the `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span></span>

3. <span data-ttu-id="61a3f-144">Aşağıda, kopyalama `wp-config.local.php`:</span><span class="sxs-lookup"><span data-stu-id="61a3f-144">Copy the following in `wp-config.local.php`:</span></span>

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

    <span data-ttu-id="61a3f-145">Önceki kodda gösterildiği şekilde anahtarları izinsiz giriş gelen web uygulamanızı önlemek için yardımcı olabilecek güvenlik ayarı, bu nedenle benzersiz değerleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="61a3f-145">Setting the security keys as illustrated in the previous code can help to prevent your web app from being hacked, so use unique values.</span></span> <span data-ttu-id="61a3f-146">Dizesi oluşturmak ihtiyacınız varsa güvenlik anahtarları belirtilen kodda yapabileceğiniz [otomatik Oluşturucu gidin](https://api.wordpress.org/secret-key/1.1/salt) yeni anahtar/değer çiftleri oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="61a3f-146">If you need to generate the string for security keys mentioned in the code, you can [go to the automatic generator](https://api.wordpress.org/secret-key/1.1/salt) to create new key/value pairs.</span></span>

4. <span data-ttu-id="61a3f-147">Aşağıdaki kodu kopyalayın `wp-config.azure.php`:</span><span class="sxs-lookup"><span data-stu-id="61a3f-147">Copy the following code in `wp-config.azure.php`:</span></span>

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

#### <a name="use-relative-paths"></a><span data-ttu-id="61a3f-148">Göreli yollar kullanın</span><span class="sxs-lookup"><span data-stu-id="61a3f-148">Use relative paths</span></span>
<span data-ttu-id="61a3f-149">WordPress uygulamasında yapılandırmak için bir son göreli yollar şeydir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-149">One last thing to configure in the WordPress app is relative paths.</span></span> <span data-ttu-id="61a3f-150">WordPress URL bilgileri veritabanında depolar.</span><span class="sxs-lookup"><span data-stu-id="61a3f-150">WordPress stores URL information in the database.</span></span> <span data-ttu-id="61a3f-151">Bu depolama bir ortamdan taşıma içeriği başka bir daha zor hale getirir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-151">This storage makes moving content from one environment to another more difficult.</span></span> <span data-ttu-id="61a3f-152">Veritabanı yerel yerine aşama veya üretim ortamları için aşamasına geçmeden her zaman güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-152">You need to update the database every time you move from local to stage or stage to production environments.</span></span> <span data-ttu-id="61a3f-153">Bir ortamdan diğerine dağıttığınız her zaman bir veritabanı dağıtımı ile neden sorunları riskini azaltmak için kullanmak [göreli kök bağlantılar eklentisi](https://wordpress.org/plugins/root-relative-urls/), hangi WordPress yönetici Panoyu kullanarak yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61a3f-153">To reduce the risk of issues that can be caused with deploying a database every time you deploy from one environment to another, use the [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using the WordPress administrator dashboard.</span></span>

<span data-ttu-id="61a3f-154">Aşağıdaki girdileri eklemek, `wp-config.php` önce dosya `That's all, stop editing!` Açıklama:</span><span class="sxs-lookup"><span data-stu-id="61a3f-154">Add the following entries to your `wp-config.php` file before the `That's all, stop editing!` comment:</span></span>

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

<span data-ttu-id="61a3f-155">Eklentisi aracılığıyla etkinleştirme `Plugins` WordPress yönetici Pano menüde.</span><span class="sxs-lookup"><span data-stu-id="61a3f-155">Activate the plugin through the `Plugins` menu in WordPress administrator dashboard.</span></span> <span data-ttu-id="61a3f-156">WordPress uygulaması için sabit bağlantı ayarlarınızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="61a3f-156">Save your permalink settings for WordPress app.</span></span>

#### <a name="the-final-wp-configphp-file"></a><span data-ttu-id="61a3f-157">En son `wp-config.php` dosyası</span><span class="sxs-lookup"><span data-stu-id="61a3f-157">The final `wp-config.php` file</span></span>
<span data-ttu-id="61a3f-158">WordPress çekirdek güncelleştirmeleri değil etkiler, `wp-config.php`, `wp-config.azure.php`, ve `wp-config.local.php` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="61a3f-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span></span> <span data-ttu-id="61a3f-159">Son sürümü işte `wp-config.php` dosyası:</span><span class="sxs-lookup"><span data-stu-id="61a3f-159">Here's a final version of the `wp-config.php` file:</span></span>

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

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="61a3f-160">Hazırlama ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="61a3f-160">Set up a staging environment</span></span>
1. <span data-ttu-id="61a3f-161">Azure aboneliğiniz üzerinde çalışan bir WordPress web uygulaması zaten varsa, oturum [Azure portal](http://portal.azure.com)ve WordPress web uygulamanıza gidin.</span><span class="sxs-lookup"><span data-stu-id="61a3f-161">If you already have a WordPress web app running on your Azure subscription, sign in to the [Azure portal](http://portal.azure.com), and then go to your WordPress web app.</span></span> <span data-ttu-id="61a3f-162">WordPress web uygulaması yoksa, bir Azure Marketi'nden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61a3f-162">If you don't have a WordPress web app, you can create one from the Azure Marketplace.</span></span> <span data-ttu-id="61a3f-163">Daha fazla bilgi için bkz: [Azure App Service'te bir WordPress web uygulaması oluşturma](web-sites-php-web-site-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="61a3f-163">To learn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span></span>
<span data-ttu-id="61a3f-164">Tıklatın **ayarları** > **dağıtım yuvası** > **Ekle** adlı bir dağıtım yuvası oluşturmak için *aşama* .</span><span class="sxs-lookup"><span data-stu-id="61a3f-164">Click **Settings** > **Deployment slots** > **Add** to create a deployment slot with the name *stage*.</span></span> <span data-ttu-id="61a3f-165">Bir dağıtım yuvası daha önce oluşturduğunuz birincil web uygulaması olarak aynı kaynakları paylaşan başka bir web uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="61a3f-165">A deployment slot is another web application that shares the same resources as the primary web app that you created previously.</span></span>

    ![Aşama dağıtım yuvası oluşturma](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. <span data-ttu-id="61a3f-167">Başka bir MySQL veritabanı deyin Ekle `wordpress-stage-db`, kaynak grubunuz için `wordpressapp-group`.</span><span class="sxs-lookup"><span data-stu-id="61a3f-167">Add another MySQL database, say `wordpress-stage-db`, to your resource group, `wordpressapp-group`.</span></span>

    ![MySQL veritabanı kaynak grubuna Ekle](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. <span data-ttu-id="61a3f-169">Yeni veritabanına işaret etmek, aşama dağıtım yuvası için bağlantı dizelerini güncelleştirmek `wordpress-stage-db`.</span><span class="sxs-lookup"><span data-stu-id="61a3f-169">Update the connection strings for your stage deployment slot to point to the new database, `wordpress-stage-db`.</span></span> <span data-ttu-id="61a3f-170">Üretim web uygulamanız `wordpressprodapp`ve web uygulaması hazırlama `wordpressprodapp-stage`, farklı veritabanlarına işaret etmelidir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point to different databases.</span></span>

#### <a name="configure-environment-specific-app-settings"></a><span data-ttu-id="61a3f-171">Ortama özgü uygulaması ayarlarını yapılandır</span><span class="sxs-lookup"><span data-stu-id="61a3f-171">Configure environment-specific app settings</span></span>
<span data-ttu-id="61a3f-172">Geliştiriciler saklayabilir anahtar/değer çiftlerinin dize Azure'da adlı yapılandırma bilgilerini bir parçası olarak **uygulama ayarları**, bir web uygulaması ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="61a3f-172">Developers can store key/value string pairs in Azure as part of the configuration information, called **App Settings**, that's associated with a web app.</span></span> <span data-ttu-id="61a3f-173">Çalışma zamanında web uygulamaları otomatik olarak bu değerleri almak ve bunları web uygulamanızda çalışan kod kullanılabilir yapın.</span><span class="sxs-lookup"><span data-stu-id="61a3f-173">At runtime, web apps automatically retrieve these values and make them available to code that's running in your web app.</span></span> <span data-ttu-id="61a3f-174">Güvenlik açısından bakıldığında, olduğundan iyi tarafı avantajı parolalar dahil veritabanı bağlantı dizeleri gibi hassas bilgileri hiçbir zaman görünmesini bir dosyada düz metin olarak gibi `wp-config.php`.</span><span class="sxs-lookup"><span data-stu-id="61a3f-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span></span>

<span data-ttu-id="61a3f-175">Aşağıdaki paragrafta açıklanan, bu işlem, dosya değişiklikleri ve WordPress uygulaması için veritabanı değişikliklerini içerdiği için yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="61a3f-175">This process, which is explained in the following paragraphs, is useful because it includes both file changes and database changes for the WordPress app:</span></span>

* <span data-ttu-id="61a3f-176">WordPress sürüm yükseltme</span><span class="sxs-lookup"><span data-stu-id="61a3f-176">WordPress version upgrade</span></span>
* <span data-ttu-id="61a3f-177">Yeni Ekle veya Düzenle veya eklentileri yükseltme</span><span class="sxs-lookup"><span data-stu-id="61a3f-177">Add new or edit or upgrade plugins</span></span>
* <span data-ttu-id="61a3f-178">Yeni Ekle veya Düzenle veya Temalar yükseltme</span><span class="sxs-lookup"><span data-stu-id="61a3f-178">Add new or edit or upgrade themes</span></span>

<span data-ttu-id="61a3f-179">Uygulama ayarlarını yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="61a3f-179">Configure app settings for:</span></span>

* <span data-ttu-id="61a3f-180">Veritabanı bilgileri</span><span class="sxs-lookup"><span data-stu-id="61a3f-180">Database information</span></span>
* <span data-ttu-id="61a3f-181">Kapatma açık/kapalı WordPress günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="61a3f-181">Turning on/off WordPress logging</span></span>
* <span data-ttu-id="61a3f-182">WordPress güvenlik ayarları</span><span class="sxs-lookup"><span data-stu-id="61a3f-182">WordPress security settings</span></span>

![Wordpress web uygulaması için uygulama ayarları](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

<span data-ttu-id="61a3f-184">Aşağıdaki uygulama ayarları için üretim web app ve hazırlama yuvası eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="61a3f-184">Make sure that you add the following app settings for your production web app and stage slot.</span></span> <span data-ttu-id="61a3f-185">Web uygulaması hazırlama ve üretim web uygulaması farklı veritabanları kullandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="61a3f-185">Note that the production web app and staging web app use different databases.</span></span>

1. <span data-ttu-id="61a3f-186">Clear **yuva ayarı** WP_ENV dışında tüm ayarlar parametreleri için onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="61a3f-186">Clear the **Slot Setting** checkbox for all the settings parameters except WP_ENV.</span></span> <span data-ttu-id="61a3f-187">Bu işlem, web uygulaması, dosya içeriğini ve veritabanı için yapılandırma değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="61a3f-187">This process will swap the configuration for your web app, file content, and database.</span></span> <span data-ttu-id="61a3f-188">Varsa **yuva ayarı** denetlenir, web uygulamanızın uygulama ayarlarının ve bağlantı dizesi yapılandırma *değil* ortamlar genelinde yapılırken taşıma bir **takas** işlemi.</span><span class="sxs-lookup"><span data-stu-id="61a3f-188">If **Slot Setting** is checked, the web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span></span> <span data-ttu-id="61a3f-189">Var olan veritabanı değişiklikleri üretim web uygulamanız bölün değil.</span><span class="sxs-lookup"><span data-stu-id="61a3f-189">Any database changes that are present will not break your production web app.</span></span>

2. <span data-ttu-id="61a3f-190">Yerel geliştirme ortamı web uygulaması aşama web uygulaması ve veritabanı WebMatrix veya tercih ettiğiniz, FTP, Git veya PhpMyAdmin gibi araçları kullanarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="61a3f-190">Deploy the local development environment web app to the stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span></span>

    ![WordPress web uygulaması için Web matris Yayımla iletişim kutusu](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. <span data-ttu-id="61a3f-192">Gözat ve hazırlama web uygulamanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="61a3f-192">Browse and test your staging web app.</span></span> <span data-ttu-id="61a3f-193">Web uygulamasının tema güncelleştirilmesi olduğu bir senaryo göz önünde bulundurularak, hazırlama web uygulaması aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-193">Considering a scenario where the theme of the web app is to be updated, here is the staging web app.</span></span>

    ![Web uygulaması yuvaları takas önce hazırlama Gözat](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. <span data-ttu-id="61a3f-195">Tüm görünüyorsa iyi, tıklatın **takas** içeriğinizi üretim ortamına taşımak için hazırlama web uygulamanızı düğmesinde.</span><span class="sxs-lookup"><span data-stu-id="61a3f-195">If all looks good, click the **Swap** button on your staging web app to move your content to the production environment.</span></span> <span data-ttu-id="61a3f-196">Bu durumda, web uygulaması ve veritabanı sırasında ortamlar üzerinde takas her **takas** işlemi.</span><span class="sxs-lookup"><span data-stu-id="61a3f-196">In this case, you swap the web app and the database across environments during every **Swap** operation.</span></span>

    ![Önizleme değişiklikleri için WordPress değiştirme](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > <span data-ttu-id="61a3f-198">Senaryonuz yalnızca dosyaları (veritabanı güncelleştirmeleri) anında gerekiyorsa, ardından denetleyin **yuva ayarı** tüm veritabanı ile ilgili için *uygulama ayarları* ve *bağlantı dizeleri ayarları* içinde **Web uygulaması ayarları** dikey penceresinde bunun önce Azure portalındaki **takas**.</span><span class="sxs-lookup"><span data-stu-id="61a3f-198">If your scenario needs to only push files (no database updates), then check **Slot Setting** for all the database-related *app settings* and *connection strings settings* in the **Web App Settings** blade within the Azure portal before doing the **Swap**.</span></span> <span data-ttu-id="61a3f-199">Bunu yaptığınızda bu durumda, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER ve varsayılan bağlantı dizesi ayarlarının Önizleme değişiklikleri gösterilmesi gerekir olmayan bir **takas**.</span><span class="sxs-lookup"><span data-stu-id="61a3f-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span></span> <span data-ttu-id="61a3f-200">Tamamlandığında, şu anda **takas** işlemi, yalnızca güncelleştirme dosyaları WordPress web uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-200">At this time, when you complete the **Swap** operation, the WordPress web app will have the updates files only.</span></span>
    >
    >

    <span data-ttu-id="61a3f-201">Bunu yaptığınızda önce bir **takas**, üretim WordPress web uygulaması aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="61a3f-201">Before doing a **Swap**, here is the production WordPress web app.</span></span>
    <span data-ttu-id="61a3f-202">![Üretim web uygulaması yuvaları takas önce](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span><span class="sxs-lookup"><span data-stu-id="61a3f-202">![Production web app before swapping slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span></span>

    <span data-ttu-id="61a3f-203">Sonra **takas** işlemi, temayı üretim web uygulamanız güncelleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-203">After the **Swap** operation, the theme has been updated on your production web app.</span></span>

    ![Üretim web uygulaması yuvaları takas sonra](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. <span data-ttu-id="61a3f-205">Geri alma gerektiğinde, üretim web gidebilirsiniz **uygulama ayarları**, tıklatıp **takas** web uygulaması ve üretim veritabanına hazırlama yuvası takas düğmesi.</span><span class="sxs-lookup"><span data-stu-id="61a3f-205">When you need to roll back, you can go to the production web **App Settings**, and click the **Swap** button to swap the web app and database from production to staging slot.</span></span> <span data-ttu-id="61a3f-206">Veritabanı değişiklikleri birlikte olup olmadığını unutmayın bir **takas** işlemi, daha sonra hazırlama web uygulamanızın dağıttığınız sonraki sefer hazırlama web uygulamanız için geçerli veritabanı için veritabanı değişikliklerini dağıtmak vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-206">Remember that if database changes are included with a **Swap** operation, then the next time you deploy to your staging web app, you need to deploy the database changes to the current database for your staging web app.</span></span> <span data-ttu-id="61a3f-207">Geçerli veritabanı, önceki üretim veya aşama veritabanının olabilir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-207">The current database might be the previous production database or the stage database.</span></span>

#### <a name="summary"></a><span data-ttu-id="61a3f-208">Özet</span><span class="sxs-lookup"><span data-stu-id="61a3f-208">Summary</span></span>
<span data-ttu-id="61a3f-209">Aşağıda, bir veritabanı sahip herhangi bir uygulama için genelleştirilmiş bir işlemdir:</span><span class="sxs-lookup"><span data-stu-id="61a3f-209">Following is a generalized process for any application that has a database:</span></span>

1. <span data-ttu-id="61a3f-210">Uygulamayı yerel ortamınıza yükleyin.</span><span class="sxs-lookup"><span data-stu-id="61a3f-210">Install the application on your local environment.</span></span>
2. <span data-ttu-id="61a3f-211">Ortama özgü yapılandırmaları (yerel ve Azure Web Apps) içerir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-211">Include environment-specific configurations (local and Azure Web Apps).</span></span>
3. <span data-ttu-id="61a3f-212">Web uygulamaları için hazırlama ve üretim ortamları ayarlama.</span><span class="sxs-lookup"><span data-stu-id="61a3f-212">Set up your staging and production environments for Web Apps.</span></span>
4. <span data-ttu-id="61a3f-213">Zaten Azure üzerinde çalışan bir üretim uygulamanız varsa, üretim içeriğinize (dosyalar/kodu ve veritabanı) yerel ve hazırlama ortamları eşitleyin.</span><span class="sxs-lookup"><span data-stu-id="61a3f-213">If you have a production application already running on Azure, sync your production content (files/code and database) to local and staging environments.</span></span>
5. <span data-ttu-id="61a3f-214">Uygulamanızı yerel ortamınızda geliştirin.</span><span class="sxs-lookup"><span data-stu-id="61a3f-214">Develop your application on your local environment.</span></span>
6. <span data-ttu-id="61a3f-215">Üretim web uygulamanız Bakım veya kilitli modu altında yerleştirin ve üretim veritabanını içerik hazırlama ve geliştirme ortamlarını eşitleyin.</span><span class="sxs-lookup"><span data-stu-id="61a3f-215">Place your production web app under maintenance or locked mode, and sync database content from production to staging and dev environments.</span></span>
7. <span data-ttu-id="61a3f-216">Test ve hazırlık ortamı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="61a3f-216">Deploy to the staging environment and test.</span></span>
8. <span data-ttu-id="61a3f-217">Üretim ortamınıza dağıtın.</span><span class="sxs-lookup"><span data-stu-id="61a3f-217">Deploy to production environment.</span></span>
9. <span data-ttu-id="61a3f-218">4 ile 6 arasındaki adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="61a3f-218">Repeat steps 4 through 6.</span></span>

### <a name="umbraco"></a><span data-ttu-id="61a3f-219">Umbraco</span><span class="sxs-lookup"><span data-stu-id="61a3f-219">Umbraco</span></span>
<span data-ttu-id="61a3f-220">Bu bölümde, nasıl özel bir modülü birden çok DevOps ortamlar genelinde dağıtmak için kullandığı Umbraco CMS öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="61a3f-220">In this section, you will learn how the Umbraco CMS uses a custom module to deploy across multiple DevOps environments.</span></span> <span data-ttu-id="61a3f-221">Bu örnek, birden çok geliştirme ortamı yönetmek için farklı bir yaklaşım sağlar.</span><span class="sxs-lookup"><span data-stu-id="61a3f-221">This example provides a different approach to managing multiple development environments.</span></span>

<span data-ttu-id="61a3f-222">[Umbraco CMS](http://umbraco.com/) birçok geliştiriciler tarafından kullanılan bir popüler .NET CMS çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="61a3f-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span></span> <span data-ttu-id="61a3f-223">Sağladığı [Courier2](http://umbraco.com/products/more-add-ons/courier-2) geliştirme üretim ortamları için hazırlama dağıtmak için modülü.</span><span class="sxs-lookup"><span data-stu-id="61a3f-223">It provides the [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module to deploy from development to staging to production environments.</span></span> <span data-ttu-id="61a3f-224">WebMatrix veya Visual Studio'yu kullanarak kolayca bir Umbraco CMS web uygulaması için bir yerel geliştirme ortamı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61a3f-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span></span>

- [<span data-ttu-id="61a3f-225">Visual Studio ile bir Umbraco web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="61a3f-225">Create an Umbraco web app with Visual Studio</span></span>](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [<span data-ttu-id="61a3f-226">WebMatrix ile bir Umbraco web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="61a3f-226">Create an Umbraco web app with WebMatrix</span></span>](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

<span data-ttu-id="61a3f-227">Her zaman kaldırmayı unutmayın `install` , uygulamanızın altında bir klasör ve hiçbir zaman aşama veya üretim web uygulamaları için karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="61a3f-227">Always remember to remove the `install` folder under your application, and never upload it to stage or production web apps.</span></span> <span data-ttu-id="61a3f-228">Bu öğretici, WebMatrix kullanır.</span><span class="sxs-lookup"><span data-stu-id="61a3f-228">This tutorial uses WebMatrix.</span></span>

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="61a3f-229">Hazırlama ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="61a3f-229">Set up a staging environment</span></span>
1. <span data-ttu-id="61a3f-230">Bir dağıtım yuvası Umbraco CMS web uygulaması zaten varsa ve çalıştırma Umbraco CMS web uygulaması için daha önce belirtildiği gibi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="61a3f-230">Create a deployment slot as mentioned previously for the Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span></span> <span data-ttu-id="61a3f-231">Bunu yapmazsanız, marketten bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61a3f-231">If you do not, you can create one from the Marketplace.</span></span>
2. <span data-ttu-id="61a3f-232">Yeni işaret edecek şekilde, aşama dağıtım yuvası için bağlantı dizesini güncellemeniz **umbraco aşama db** veritabanı.</span><span class="sxs-lookup"><span data-stu-id="61a3f-232">Update the connection string for your stage deployment slot to point to the new **umbraco-stage-db** database.</span></span> <span data-ttu-id="61a3f-233">Üretim web uygulaması (umbraositecms-1) ve hazırlama web uygulaması (umbracositecms-1-aşama) *gerekir* farklı veritabanlarına gelin.</span><span class="sxs-lookup"><span data-stu-id="61a3f-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point to different databases.</span></span>

    ![Yeni hazırlama veritabanı ile web uygulaması hazırlama için kullanılan bağlantı dizesi güncelleştir](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. <span data-ttu-id="61a3f-235">Tıklatın **alma yayımlama ayarları** dağıtım yuvası için **aşama**.</span><span class="sxs-lookup"><span data-stu-id="61a3f-235">Click **Get Publish settings** for the deployment slot **stage**.</span></span> <span data-ttu-id="61a3f-236">Bu işlem, yerel geliştirme web uygulamasından uygulamanızı Azure web uygulamasına yayımlamak için Visual Studio veya WebMatrix gerektiren tüm bilgilerini depolayan bir yayımlama ayarları dosyası indirir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-236">This process will download a publish settings file that stores all the information that Visual Studio or WebMatrix requires to publish your application from the local development web app to the Azure web app.</span></span>

    ![Get ayarı hazırlama web uygulaması yayımlama](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. <span data-ttu-id="61a3f-238">Yerel geliştirme web uygulamanızı WebMatrix veya Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="61a3f-238">Open your local development web app in WebMatrix or Visual Studio.</span></span> <span data-ttu-id="61a3f-239">Bu öğretici, WebMatrix kullanır.</span><span class="sxs-lookup"><span data-stu-id="61a3f-239">This tutorial uses WebMatrix.</span></span> <span data-ttu-id="61a3f-240">İlk olarak, hazırlama web uygulamanız için yayımlama ayarları dosyasını içeri aktarmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-240">First, you need to import the publish settings file for your staging web app.</span></span>

    ![Web Matrix kullanarak Umbraco yayımlama ayarlarını içeri aktarma](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. <span data-ttu-id="61a3f-242">İletişim kutusunda değişiklikleri gözden geçirin ve yerel web uygulamanızı Azure web uygulamasına dağıtma *umbracositecms 1 aşama*.</span><span class="sxs-lookup"><span data-stu-id="61a3f-242">Review changes in the dialog box, and deploy your local web app to your Azure web app, *umbracositecms-1-stage*.</span></span> <span data-ttu-id="61a3f-243">Dosyaları doğrudan hazırlama web uygulamanıza dağıttığınızda, dosyalarında atlayacak `~/app_data/TEMP/` aşama web uygulaması ilk çalıştırıldığında bu dosyalar yeniden oluşturulacak olmadığından klasör başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="61a3f-243">When you deploy files directly to your staging web app, you will omit files in the `~/app_data/TEMP/` folder because these files will be regenerated when the stage web app is first started.</span></span> <span data-ttu-id="61a3f-244">Ayrıca atlayın `~/app_data/umbraco.config` de yeniden oluşturulacak dosya.</span><span class="sxs-lookup"><span data-stu-id="61a3f-244">You should also omit the `~/app_data/umbraco.config` file, which will also be regenerated.</span></span>

    ![Web Matristeki Yayımla değişiklikleri gözden geçirin](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. <span data-ttu-id="61a3f-246">Hazırlama web uygulaması başarıyla Umbraco yerel web uygulaması yayımladıktan sonra hazırlama web uygulamanıza göz atın ve sorunları kural için birkaç testleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="61a3f-246">After you successfully publish the Umbraco local web app to the staging web app, browse to your staging web app, and run a few tests to rule out any issues.</span></span>

#### <a name="set-up-the-courier2-deployment-module"></a><span data-ttu-id="61a3f-247">Courier2 dağıtım modülünü kurun</span><span class="sxs-lookup"><span data-stu-id="61a3f-247">Set up the Courier2 deployment module</span></span>
<span data-ttu-id="61a3f-248">İle [Courier2](http://umbraco.com/products/more-add-ons/courier-2) modül yalnızca sağ anında içeriği, stil sayfaları ve geliştirme modülleri hazırlama bir web uygulamasından bir üretim web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="61a3f-248">With the [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click to push content, style sheets, and development modules from a staging web app to a production web app.</span></span> <span data-ttu-id="61a3f-249">Bu işlem bir güncelleştirme dağıttığınızda üretim web uygulamanız çiğnemekten riskini azaltır.</span><span class="sxs-lookup"><span data-stu-id="61a3f-249">This process reduces the risk of breaking your production web app when you deploy an update.</span></span>
<span data-ttu-id="61a3f-250">Courier2 için için bir lisans satın `*.azurewebsites.net` etki alanı ve özel etki alanınızı (örneğin http://abc.com).</span><span class="sxs-lookup"><span data-stu-id="61a3f-250">Purchase a license for Courier2 for the `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span></span> <span data-ttu-id="61a3f-251">Lisans satın aldıktan sonra indirilen lisans yerleştirin (. Lisans Sözleşmesi dosyası) içinde `bin` klasör.</span><span class="sxs-lookup"><span data-stu-id="61a3f-251">After you purchase the license, place the downloaded license (.LIC file) in the `bin` folder.</span></span>

![Bin klasörü altındaki açılan lisans dosyası](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. <span data-ttu-id="61a3f-253">[Courier2 paketini indirin](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span><span class="sxs-lookup"><span data-stu-id="61a3f-253">[Download the Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span></span> <span data-ttu-id="61a3f-254">Aşama web uygulamanıza, deyin http://umbracocms-site-stage.azurewebsites.net/umbraco, oturum açma tıklatın **Geliştirici** menüsüne ve ardından **paketleri** > **yükleme yerel Paket**.</span><span class="sxs-lookup"><span data-stu-id="61a3f-254">Sign in to your stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click the **Developer** menu, and then click **Packages** > **Install local package**.</span></span>

    ![Umbraco paketi yükleyicisi](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. <span data-ttu-id="61a3f-256">Courier2 paketi yükleyici kullanarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="61a3f-256">Upload the Courier2 package by using the installer.</span></span>

    ![Paketi courier modülü için yükleme](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. <span data-ttu-id="61a3f-258">Paketi yapılandırmak için courier.config dosyasını güncelleştirmeniz gerekir **Config** klasör, web uygulamanızın.</span><span class="sxs-lookup"><span data-stu-id="61a3f-258">To configure the package, you need to update the courier.config file under the **Config** folder of your web app.</span></span>

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

4. <span data-ttu-id="61a3f-259">Altında `<repositories>`, üretim site URL'si ve kullanıcı bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="61a3f-259">Under `<repositories>`, enter the production site URL and user information.</span></span>
    <span data-ttu-id="61a3f-260">Varsayılan Umbraco üyelik sağlayıcısı kullanıyorsanız, yönetim kullanıcı kimliği eklemek &lt;kullanıcı&gt; bölümü.</span><span class="sxs-lookup"><span data-stu-id="61a3f-260">If you are using the default Umbraco membership provider, then add the ID for the Administration user in the &lt;user&gt; section.</span></span>
    <span data-ttu-id="61a3f-261">Özel bir Umbraco üyelik sağlayıcısı kullanıyorsanız `<login>`,`<password>` üretim siteye bağlamak için Courier2 modülünde.</span><span class="sxs-lookup"><span data-stu-id="61a3f-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in the Courier2 module to connect to the production site.</span></span>
    <span data-ttu-id="61a3f-262">Daha fazla ayrıntı için [Courier2 modülü belgelerini gözden](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span><span class="sxs-lookup"><span data-stu-id="61a3f-262">For more details, [review the documentation for the Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span></span>

5. <span data-ttu-id="61a3f-263">Benzer şekilde, üretim sitenizde Courier2 modülünü yüklemek ve aşağıda gösterildiği gibi ilgili courier.config dosya aşama web uygulamasında işaret edecek şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="61a3f-263">Similarly, install the Courier2 module on your production site, and configure it to point to the stage web app in its respective courier.config file as shown here.</span></span>

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

6. <span data-ttu-id="61a3f-264">Tıklatın **Courier2** sekmesinde Umbraco CMS web uygulama panosunda ve ardından **konumları**.</span><span class="sxs-lookup"><span data-stu-id="61a3f-264">Click the **Courier2** tab in the Umbraco CMS web app dashboard, and then click **Locations**.</span></span> <span data-ttu-id="61a3f-265">Depo adını bölümünde belirtildiği gibi görmeniz gerekir `courier.config`.</span><span class="sxs-lookup"><span data-stu-id="61a3f-265">You should see the repository name as mentioned in `courier.config`.</span></span> <span data-ttu-id="61a3f-266">Üretim ve hazırlama web uygulamaları üzerinde bu işlemi yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61a3f-266">Do this process on both your production and staging web apps.</span></span>

    ![Görünüm hedef web uygulama havuzu](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. <span data-ttu-id="61a3f-268">Hazırlama sitesinden içerik üretim siteye dağıtmak için Git **içerik**ve varolan bir sayfayı seçebilir veya yeni bir sayfa oluşturun.</span><span class="sxs-lookup"><span data-stu-id="61a3f-268">To deploy content from the staging site to the production site, go to **Content**, and select an existing page or create a new page.</span></span> <span data-ttu-id="61a3f-269">Varolan bir sayfayı sayfanın başlığı olduğu my web uygulamasından seçecektir **başlarken – yeni**ve ardından **kaydetmek ve yayımlamak**.</span><span class="sxs-lookup"><span data-stu-id="61a3f-269">I will select an existing page from my web app where the title of the page is **Getting Started – new**, and then click **Save and Publish**.</span></span>

    ![Sayfasının başlığını değiştirme ve yayımlama](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. <span data-ttu-id="61a3f-271">Tüm seçenekleri görüntülemek için değiştirilmiş sayfanın sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="61a3f-271">Right-click the modified page to view all the options.</span></span> <span data-ttu-id="61a3f-272">Tıklatın **Courier** açmak için **dağıtım** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="61a3f-272">Click **Courier** to open the **Deployment** dialog box.</span></span> <span data-ttu-id="61a3f-273">Tıklatın **dağıtma** dağıtımını başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="61a3f-273">Click **Deploy** to initiate deployment.</span></span>

    ![Courier modülü dağıtım iletişim](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. <span data-ttu-id="61a3f-275">Değişiklikleri gözden geçirin ve ardından **devam**.</span><span class="sxs-lookup"><span data-stu-id="61a3f-275">Review the changes, and then click **Continue**.</span></span>

    ![Courier modülü dağıtım iletişim değişiklikleri gözden geçir](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    <span data-ttu-id="61a3f-277">Dağıtım günlüğü dağıtım başarılı olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-277">The deployment log shows if the deployment was successful.</span></span>

     ![Courier modülden dağıtım günlüklerini görüntüle](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. <span data-ttu-id="61a3f-279">Değişiklikler yansıtılır görmek için üretim web uygulamanız göz atın.</span><span class="sxs-lookup"><span data-stu-id="61a3f-279">Browse your production web app to see if the changes are reflected.</span></span>

     ![Üretim web uygulamasına göz atın](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

<span data-ttu-id="61a3f-281">Courier kullanma hakkında daha fazla bilgi için belgelerini gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="61a3f-281">To learn more about how to use Courier, review the documentation.</span></span>

#### <a name="how-to-upgrade-the-umbraco-cms-version"></a><span data-ttu-id="61a3f-282">Umbraco CMS sürüm yükseltme</span><span class="sxs-lookup"><span data-stu-id="61a3f-282">How to upgrade the Umbraco CMS version</span></span>
<span data-ttu-id="61a3f-283">Courier olacak başka bir Umbraco CMS sürümünden yükseltme Yardımı.</span><span class="sxs-lookup"><span data-stu-id="61a3f-283">Courier will not help you upgrade from one version of Umbraco CMS to another.</span></span> <span data-ttu-id="61a3f-284">Umbraco CMS sürümüne yükselttiğinizde, özel modüller veya iş ortakları ve Umbraco çekirdek kitaplıkları modüllerden uyumsuzluklar için işaretlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and the Umbraco Core libraries.</span></span> <span data-ttu-id="61a3f-285">En iyi uygulamalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="61a3f-285">Here are best practices:</span></span>

* <span data-ttu-id="61a3f-286">Yükseltmeden önce her zaman, web uygulaması ve veritabanı yedekleme.</span><span class="sxs-lookup"><span data-stu-id="61a3f-286">Always back up your web app and database before you upgrade.</span></span> <span data-ttu-id="61a3f-287">Azure Web uygulamaları üzerinde Yedekleme özelliğini kullanarak, Web siteleri için Otomatik yedekler ayarlayın ve geri yükleme özelliğini kullanarak gerekirse sitenize geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="61a3f-287">On web apps in Azure, you can set up automatic backups for your websites by using the backup feature and restore your site if needed by using the restore feature.</span></span> <span data-ttu-id="61a3f-288">Daha fazla ayrıntı için bkz: [web uygulamanızı nasıl](web-sites-backup.md) ve [web uygulamanızı geri yükleme](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="61a3f-288">For more details, see [How to back up your web app](web-sites-backup.md) and [How to restore your web app](web-sites-restore.md).</span></span>
* <span data-ttu-id="61a3f-289">İş ortakları paketlerinden yükseltme yapıyorsanız sürümü ile uyumlu olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="61a3f-289">Check if packages from partners are compatible with the version you're upgrading to.</span></span> <span data-ttu-id="61a3f-290">Paketin üzerinde sayfa yükleme, Umbraco CMS sürümüyle proje uyumluluğu gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="61a3f-290">On the package's download page, review the project compatibility with Umbraco CMS version.</span></span>

<span data-ttu-id="61a3f-291">Web uygulamanızı yerel olarak yükseltme hakkında daha fazla ayrıntı için [genel yükseltme yönergelere bakın](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span><span class="sxs-lookup"><span data-stu-id="61a3f-291">For more details about how to upgrade your web app locally, [see the general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span></span>

<span data-ttu-id="61a3f-292">Yerel geliştirme sitenizi yükselttikten sonra değişiklikleri hazırlama web uygulamasını yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="61a3f-292">After your local development site is upgraded, publish the changes to the staging web app.</span></span> <span data-ttu-id="61a3f-293">Uygulamanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="61a3f-293">Test your application.</span></span> <span data-ttu-id="61a3f-294">Tüm görünüyorsa iyi kullanmak **takas** hazırlama sitenizi üretim web uygulamasına değiştirme düğmesi.</span><span class="sxs-lookup"><span data-stu-id="61a3f-294">If all looks good, use the **Swap** button to swap your staging site to the production web app.</span></span> <span data-ttu-id="61a3f-295">Kullandığınızda **takas** işlemi, web uygulamanızın yapılandırmasında etkilenecek değişiklikleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61a3f-295">When you use the **Swap** operation, you can view the changes that will be affected in your web app's configuration.</span></span> <span data-ttu-id="61a3f-296">Bu **takas** işlemi ile web uygulamaları ve veritabanları değiştirir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-296">This **Swap** operation swaps the web apps and databases.</span></span> <span data-ttu-id="61a3f-297">Sonra **takas**, üretim web uygulaması umbraco aşama db veritabanına işaret edecek ve hazırlama web uygulaması umbraco üretim db veritabanına işaret.</span><span class="sxs-lookup"><span data-stu-id="61a3f-297">After the **Swap**, the production web app will point to the umbraco-stage-db database, and the staging web app will point to umbraco-prod-db database.</span></span>

![Umbraco CMS dağıtmak için Önizleme değiştirme](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

<span data-ttu-id="61a3f-299">Web uygulaması ve veritabanı takas avantajları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="61a3f-299">Here are advantages of swapping both the web app and the database:</span></span>

* <span data-ttu-id="61a3f-300">Başka bir web uygulamanızın önceki sürüme geri alabilirsiniz **takas** herhangi bir uygulama sorun varsa.</span><span class="sxs-lookup"><span data-stu-id="61a3f-300">You can roll back to the previous version of your web app with another **Swap** if there are any application issues.</span></span>
* <span data-ttu-id="61a3f-301">Yükseltme için dosyaları ve üretim web uygulaması hazırlama web uygulamasından veritabanları ve veritabanı dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-301">For an upgrade, you need to deploy files and databases from the staging web app to the production web app and database.</span></span> <span data-ttu-id="61a3f-302">Dosyaları ve veritabanları dağıttığınızda pek çok yanlış gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61a3f-302">Many things can go wrong when you deploy files and databases.</span></span> <span data-ttu-id="61a3f-303">Kullanarak **takas** özelliği yuvaları biz kapalı kalma süresi yükseltme sırasında ve değişiklikleri dağıtırken oluşabilecek hatalar riskini azaltmak.</span><span class="sxs-lookup"><span data-stu-id="61a3f-303">By using the **Swap** feature of slots, we can reduce downtime during an upgrade and reduce the risk of failures that can occur when you deploy changes.</span></span>
* <span data-ttu-id="61a3f-304">Yapabileceğiniz **A / B testi** kullanarak [üretimde test](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) özelliği.</span><span class="sxs-lookup"><span data-stu-id="61a3f-304">You can do **A/B testing** by using the [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span></span>

<span data-ttu-id="61a3f-305">Bu örnek özel modüller ortamlar genelinde dağıtımını yönetmek için Umbraco Courier modülüne benzer burada yapı platform esnekliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="61a3f-305">This example shows you the flexibility of the platform where you can build custom modules similar to Umbraco Courier module to manage deployment across environments.</span></span>

## <a name="references"></a><span data-ttu-id="61a3f-306">Başvurular</span><span class="sxs-lookup"><span data-stu-id="61a3f-306">References</span></span>
[<span data-ttu-id="61a3f-307">Azure App Service ile Çevik Yazılım Geliştirme</span><span class="sxs-lookup"><span data-stu-id="61a3f-307">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)

[<span data-ttu-id="61a3f-308">Hazırlık ortamları için Azure App Service'te web uygulamalarını ayarlama</span><span class="sxs-lookup"><span data-stu-id="61a3f-308">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)

[<span data-ttu-id="61a3f-309">Üretim dışı dağıtım yuvaları Web erişimi engellemek nasıl</span><span class="sxs-lookup"><span data-stu-id="61a3f-309">How to block web access to non-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
