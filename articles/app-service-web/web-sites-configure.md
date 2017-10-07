---
title: "Azure App Service'te web uygulamalarını aaaConfigure"
description: "Nasıl tooconfigure bir web uygulamasını Azure uygulama hizmetleri"
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 8697ab6f21cfeb470e11f0d82c68692d43142fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a><span data-ttu-id="e6978-103">Azure Uygulama Hizmeti’nde Web uygulamalarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e6978-103">Configure web apps in Azure App Service</span></span>
<span data-ttu-id="e6978-104">Bu konuda, bir web uygulamasını kullanarak tooconfigure nasıl hello açıklanmaktadır [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="e6978-104">This topic explains how tooconfigure a web app using hello [Azure Portal].</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a><span data-ttu-id="e6978-105">Uygulama ayarları</span><span class="sxs-lookup"><span data-stu-id="e6978-105">Application settings</span></span>
1. <span data-ttu-id="e6978-106">Merhaba, [Azure Portal]açın hello dikey penceresinde hello web uygulaması için.</span><span class="sxs-lookup"><span data-stu-id="e6978-106">In hello [Azure Portal], open hello blade for hello web app.</span></span>
2. <span data-ttu-id="e6978-107">Tıklatın **tüm ayarları**.</span><span class="sxs-lookup"><span data-stu-id="e6978-107">Click **All Settings**.</span></span>
3. <span data-ttu-id="e6978-108">Tıklatın **uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="e6978-108">Click **Application Settings**.</span></span>

![Uygulama ayarları][configure01]

<span data-ttu-id="e6978-110">Merhaba **uygulama ayarları** dikey birkaç kategoriler altında gruplanmış ayarlara sahip.</span><span class="sxs-lookup"><span data-stu-id="e6978-110">hello **Application settings** blade has settings grouped under several categories.</span></span>

### <a name="general-settings"></a><span data-ttu-id="e6978-111">Genel ayarları</span><span class="sxs-lookup"><span data-stu-id="e6978-111">General settings</span></span>
<span data-ttu-id="e6978-112">**Framework sürümlerini**.</span><span class="sxs-lookup"><span data-stu-id="e6978-112">**Framework versions**.</span></span> <span data-ttu-id="e6978-113">Uygulamanız herhangi bu çerçeveleri kullanıyorsa bu seçenekleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="e6978-113">Set these options if your app uses any these frameworks:</span></span> 

* <span data-ttu-id="e6978-114">**.NET framework**: kümesi hello .NET framework sürümü.</span><span class="sxs-lookup"><span data-stu-id="e6978-114">**.NET Framework**: Set hello .NET framework version.</span></span> 
* <span data-ttu-id="e6978-115">**PHP**: kümesi hello PHP sürümünü veya **OFF** toodisable PHP.</span><span class="sxs-lookup"><span data-stu-id="e6978-115">**PHP**: Set hello PHP version, or **OFF** toodisable PHP.</span></span> 
* <span data-ttu-id="e6978-116">**Java**: Select hello Java sürümü veya **OFF** toodisable Java.</span><span class="sxs-lookup"><span data-stu-id="e6978-116">**Java**: Select hello Java version or **OFF** toodisable Java.</span></span> <span data-ttu-id="e6978-117">Kullanım hello **Web kapsayıcısına** seçeneği toochoose Tomcat ve Jetty sürümleri arasında.</span><span class="sxs-lookup"><span data-stu-id="e6978-117">Use hello **Web Container** option toochoose between Tomcat and Jetty versions.</span></span>
* <span data-ttu-id="e6978-118">**Python**: Select hello Python sürümü veya **OFF** toodisable Python.</span><span class="sxs-lookup"><span data-stu-id="e6978-118">**Python**: Select hello Python version, or **OFF** toodisable Python.</span></span>

<span data-ttu-id="e6978-119">Teknik nedenlerle hello .NET, PHP ve Python seçenekleri uygulamanız için Java'yı etkinleştirme devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="e6978-119">For technical reasons, enabling Java for your app disables hello .NET, PHP, and Python options.</span></span>

<span data-ttu-id="e6978-120"><a name="platform"></a>
**Platform**.</span><span class="sxs-lookup"><span data-stu-id="e6978-120"><a name="platform"></a>
**Platform**.</span></span> <span data-ttu-id="e6978-121">Web uygulamanızı 32 bit veya 64-bit bir ortamda çalışır olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="e6978-121">Selects whether your web app runs in a 32-bit or 64-bit environment.</span></span> <span data-ttu-id="e6978-122">Merhaba 64-bit ortamı temel veya standart modu gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e6978-122">hello 64-bit environment requires Basic or Standard mode.</span></span> <span data-ttu-id="e6978-123">Ücretsiz ve paylaşılan modları her zaman bir 32 bit ortamda çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="e6978-123">Free and Shared modes always run in a 32-bit environment.</span></span>

<span data-ttu-id="e6978-124">**Web yuvaları**.</span><span class="sxs-lookup"><span data-stu-id="e6978-124">**Web Sockets**.</span></span> <span data-ttu-id="e6978-125">Ayarlama **ON** tooenable hello WebSocket Protokolü; Örneğin, web uygulamanızı kullanıyorsa [ASP.NET SignalR] veya [Socket.IO].</span><span class="sxs-lookup"><span data-stu-id="e6978-125">Set **ON** tooenable hello WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io].</span></span>

<span data-ttu-id="e6978-126"><a name="alwayson"></a>
**Always On**.</span><span class="sxs-lookup"><span data-stu-id="e6978-126"><a name="alwayson"></a>
**Always On**.</span></span> <span data-ttu-id="e6978-127">Varsayılan olarak, belirli bir süre için boşta olmaları durumunda web uygulamaları kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="e6978-127">By default, web apps are unloaded if they are idle for some period of time.</span></span> <span data-ttu-id="e6978-128">Bu hello sistem kaynakların tasarrufu sağlar.</span><span class="sxs-lookup"><span data-stu-id="e6978-128">This lets hello system conserve resources.</span></span> <span data-ttu-id="e6978-129">Temel veya standart modunda etkinleştirebilirsiniz **her zaman açık** tookeep hello uygulama yüklenen tüm hello zaman.</span><span class="sxs-lookup"><span data-stu-id="e6978-129">In Basic or Standard mode, you can enable **Always On** tookeep hello app loaded all hello time.</span></span> <span data-ttu-id="e6978-130">Sürekli Webjob'lar uygulamanızın çalıştırdığı veya çalıştığı Web işleri tetiklenen CRON ifade kullanılarak, etkinleştirmeniz gerekir **her zaman açık**, veya hello web işleri güvenilir bir şekilde çalıştıramıyor.</span><span class="sxs-lookup"><span data-stu-id="e6978-130">If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or hello web jobs may not run reliably.</span></span>

<span data-ttu-id="e6978-131">**Yönetilen ardışık düzen sürüm**.</span><span class="sxs-lookup"><span data-stu-id="e6978-131">**Managed Pipeline Version**.</span></span> <span data-ttu-id="e6978-132">Ayarlar hello IIS [ardışık düzen modu].</span><span class="sxs-lookup"><span data-stu-id="e6978-132">Sets hello IIS [pipeline mode].</span></span> <span data-ttu-id="e6978-133">Bırakın IIS daha eski bir sürümü gerektiren eski bir uygulama yoksa bu tooIntegrated (Merhaba varsayılan) ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e6978-133">Leave this set tooIntegrated (hello default) unless you have a legacy app that requires an older version of IIS.</span></span>

<span data-ttu-id="e6978-134">**Otomatik Takas**.</span><span class="sxs-lookup"><span data-stu-id="e6978-134">**Auto Swap**.</span></span> <span data-ttu-id="e6978-135">Otomatik Takas için bir dağıtım yuvası etkinleştirirseniz, bir güncelleştirme toothat yuvaya bastığınızda uygulama hizmeti otomatik olarak başlangıç web uygulaması üretime değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e6978-135">If you enable Auto Swap for a deployment slot, App Service will automatically swap hello web app into production when you push an update toothat slot.</span></span> <span data-ttu-id="e6978-136">Daha fazla bilgi için bkz: [toostaging yuvaları için Azure App Service'te web uygulamalarını dağıtma](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="e6978-136">For more information, see [Deploy toostaging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span>

### <a name="debugging"></a><span data-ttu-id="e6978-137">Hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="e6978-137">Debugging</span></span>
<span data-ttu-id="e6978-138">**Uzaktan hata ayıklama**.</span><span class="sxs-lookup"><span data-stu-id="e6978-138">**Remote Debugging**.</span></span> <span data-ttu-id="e6978-139">Uzaktan hata ayıklamayı etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="e6978-139">Enables remote debugging.</span></span> <span data-ttu-id="e6978-140">Tooyour web doğrudan uygulama etkinleştirildiğinde, Visual Studio tooconnect hello uzaktan hata ayıklayıcı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6978-140">When enabled, you can use hello remote debugger in Visual Studio tooconnect directly tooyour web app.</span></span> <span data-ttu-id="e6978-141">Uzaktan hata ayıklama 48 saat boyunca etkin kalır.</span><span class="sxs-lookup"><span data-stu-id="e6978-141">Remote debugging will remain enabled for 48 hours.</span></span> 

### <a name="app-settings"></a><span data-ttu-id="e6978-142">Uygulama ayarları</span><span class="sxs-lookup"><span data-stu-id="e6978-142">App settings</span></span>
<span data-ttu-id="e6978-143">Bu bölümde, web ad/değer çiftleri içeren uygulama başlangıç yükler.</span><span class="sxs-lookup"><span data-stu-id="e6978-143">This section contains name/value pairs that you web app will load on start up.</span></span> 

* <span data-ttu-id="e6978-144">.NET yapılandırmanızı eklenen .NET uygulamaları için bu ayarları `AppSettings` çalışma zamanında mevcut ayarları geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="e6978-144">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span></span> 
* <span data-ttu-id="e6978-145">PHP, Python, Java ve düğüm uygulamalar, bu ayarlar çalışma zamanında ortam değişkenleri olarak erişebilir.</span><span class="sxs-lookup"><span data-stu-id="e6978-145">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span></span> <span data-ttu-id="e6978-146">Her uygulama ayarı için iki ortam değişkenin oluşturulur; bir hello uygulama ayarı girişi ve APPSETTING_ önekine sahip başka bir tarafından belirtilen hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="e6978-146">For each app setting, two environment variables are created; one with hello name specified by hello app setting entry, and another with a prefix of APPSETTING_.</span></span> <span data-ttu-id="e6978-147">Her ikisi de hello içeren aynı değeri.</span><span class="sxs-lookup"><span data-stu-id="e6978-147">Both contain hello same value.</span></span>

### <a name="connection-strings"></a><span data-ttu-id="e6978-148">Bağlantı dizeleri</span><span class="sxs-lookup"><span data-stu-id="e6978-148">Connection strings</span></span>
<span data-ttu-id="e6978-149">Bağlantılı kaynaklar için bağlantı dizelerini.</span><span class="sxs-lookup"><span data-stu-id="e6978-149">Connection strings for linked resources.</span></span> 

<span data-ttu-id="e6978-150">.NET uygulamaları için bu bağlantı dizeleri .NET yapılandırmanızı eklenmiş `connectionStrings` burada hello anahtar eşittir girişlerin ayarlar çalışma zamanında hello bağlantılı veritabanı adı.</span><span class="sxs-lookup"><span data-stu-id="e6978-150">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where hello key equals hello linked database name.</span></span> 

<span data-ttu-id="e6978-151">PHP, Python, Java ve düğüm uygulamalar için bu ayarları hello bağlantı türüyle önekli zamanında ortam değişkenleri olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e6978-151">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with hello connection type.</span></span> <span data-ttu-id="e6978-152">Merhaba ortam değişkeni önekleri aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="e6978-152">hello environment variable prefixes are as follows:</span></span> 

* <span data-ttu-id="e6978-153">SQL sunucusu:`SQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="e6978-153">SQL Server: `SQLCONNSTR_`</span></span>
* <span data-ttu-id="e6978-154">MySQL:`MYSQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="e6978-154">MySQL: `MYSQLCONNSTR_`</span></span>
* <span data-ttu-id="e6978-155">SQL veritabanı:`SQLAZURECONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="e6978-155">SQL Database: `SQLAZURECONNSTR_`</span></span>
* <span data-ttu-id="e6978-156">Özel:`CUSTOMCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="e6978-156">Custom: `CUSTOMCONNSTR_`</span></span>

<span data-ttu-id="e6978-157">Örneğin, bir MySql bağlantı dizesi olarak adlandırılmışsa `connectionstring1`, hello ortam değişkeni erişilebilecek `MYSQLCONNSTR_connectionString1`.</span><span class="sxs-lookup"><span data-stu-id="e6978-157">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through hello environment variable `MYSQLCONNSTR_connectionString1`.</span></span>

### <a name="default-documents"></a><span data-ttu-id="e6978-158">Varsayılan belgeler</span><span class="sxs-lookup"><span data-stu-id="e6978-158">Default documents</span></span>
<span data-ttu-id="e6978-159">Hello varsayılan belge hello web hello kök URL'de bir Web sitesi için görüntülenen sayfadır.</span><span class="sxs-lookup"><span data-stu-id="e6978-159">hello default document is hello web page that is displayed at hello root URL for a website.</span></span>  <span data-ttu-id="e6978-160">Merhaba ilk eşleşen dosya hello listesinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e6978-160">hello first matching file in hello list is used.</span></span> 

<span data-ttu-id="e6978-161">Web uygulamaları rota URL'sine bağlı yerine, bu nedenle bir varsayılan belge statik içerik vardır; bu durumda hizmet olan modülleri kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="e6978-161">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span></span>    

### <a name="handler-mappings"></a><span data-ttu-id="e6978-162">İşleyici eşlemeleri</span><span class="sxs-lookup"><span data-stu-id="e6978-162">Handler mappings</span></span>
<span data-ttu-id="e6978-163">Bu alan tooadd özel komut dosyası işlemciler toohandle istekleri için belirli dosya uzantılarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6978-163">Use this area tooadd custom script processors toohandle requests for specific file extensions.</span></span> 

* <span data-ttu-id="e6978-164">**Uzantı**.</span><span class="sxs-lookup"><span data-stu-id="e6978-164">**Extension**.</span></span> <span data-ttu-id="e6978-165">Merhaba dosya uzantısı toobe *.php veya handler.fcgi gibi işlenir.</span><span class="sxs-lookup"><span data-stu-id="e6978-165">hello file extension toobe handled, such as *.php or handler.fcgi.</span></span> 
* <span data-ttu-id="e6978-166">**Betik işleyici yolu**.</span><span class="sxs-lookup"><span data-stu-id="e6978-166">**Script Processor Path**.</span></span> <span data-ttu-id="e6978-167">Merhaba hello betik işlemcisi mutlak yolu.</span><span class="sxs-lookup"><span data-stu-id="e6978-167">hello absolute path of hello script processor.</span></span> <span data-ttu-id="e6978-168">Merhaba dosya uzantısı ile eşleşen istekleri toofiles hello betik işleyici tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="e6978-168">Requests toofiles that match hello file extension will be processed by hello script processor.</span></span> <span data-ttu-id="e6978-169">Merhaba yolu kullan `D:\home\site\wwwroot` toorefer tooyour uygulamanızın kök dizini.</span><span class="sxs-lookup"><span data-stu-id="e6978-169">Use hello path `D:\home\site\wwwroot` toorefer tooyour app's root directory.</span></span>
* <span data-ttu-id="e6978-170">**Ek bağımsız değişkenler**.</span><span class="sxs-lookup"><span data-stu-id="e6978-170">**Additional Arguments**.</span></span> <span data-ttu-id="e6978-171">Merhaba betik işleyici için isteğe bağlı komut satırı bağımsız değişkenleri</span><span class="sxs-lookup"><span data-stu-id="e6978-171">Optional command-line arguments for hello script processor</span></span> 

### <a name="virtual-applications-and-directories"></a><span data-ttu-id="e6978-172">Sanal uygulamalar ve dizinler</span><span class="sxs-lookup"><span data-stu-id="e6978-172">Virtual applications and directories</span></span>
<span data-ttu-id="e6978-173">tooconfigure sanal uygulamalar ve dizinler, her sanal dizini ve karşılık gelen fiziksel yolu göreli toohello Web sitesi kökü belirtin.</span><span class="sxs-lookup"><span data-stu-id="e6978-173">tooconfigure virtual applications and directories, specify each virtual directory and its corresponding physical path relative toohello website root.</span></span> <span data-ttu-id="e6978-174">İsteğe bağlı olarak, hello seçebilirsiniz **uygulama** onay kutusunu toomark bir uygulama olarak bir sanal dizin.</span><span class="sxs-lookup"><span data-stu-id="e6978-174">Optionally, you can select hello **Application** checkbox toomark a virtual directory as an application.</span></span>

## <a name="enabling-diagnostic-logs"></a><span data-ttu-id="e6978-175">Tanılama günlüklerini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="e6978-175">Enabling diagnostic logs</span></span>
<span data-ttu-id="e6978-176">tooenable tanılama günlükleri:</span><span class="sxs-lookup"><span data-stu-id="e6978-176">tooenable diagnostic logs:</span></span>

1. <span data-ttu-id="e6978-177">Web uygulamanız için Hello dikey penceresinde tıklayın **tüm ayarları**.</span><span class="sxs-lookup"><span data-stu-id="e6978-177">In hello blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="e6978-178">Tıklatın **tanılama günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="e6978-178">Click **Diagnostic logs**.</span></span> 

<span data-ttu-id="e6978-179">Bir web uygulamasından tanılama günlüklerini yazma seçenekleri, günlük kaydı destekler:</span><span class="sxs-lookup"><span data-stu-id="e6978-179">Options for writing diagnostic logs from a web application that supports logging:</span></span> 

* <span data-ttu-id="e6978-180">**Uygulama günlüğü**.</span><span class="sxs-lookup"><span data-stu-id="e6978-180">**Application Logging**.</span></span> <span data-ttu-id="e6978-181">Uygulama günlüklerini toohello dosya sistemi yazar.</span><span class="sxs-lookup"><span data-stu-id="e6978-181">Writes application logs toohello file system.</span></span> <span data-ttu-id="e6978-182">Lasts 12 saatlik bir dönem için günlüğe kaydetme.</span><span class="sxs-lookup"><span data-stu-id="e6978-182">Logging lasts for a period of 12 hours.</span></span> 

<span data-ttu-id="e6978-183">**Düzey**.</span><span class="sxs-lookup"><span data-stu-id="e6978-183">**Level**.</span></span> <span data-ttu-id="e6978-184">Uygulama günlüğü etkinleştirildiğinde, bu seçenek kayıtlı (hata, uyarı, bilgi veya ayrıntılı) olacak bilgileri hello miktarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e6978-184">When application logging is enabled, this option specifies hello amount of information that will be recorded (Error, Warning, Information, or Verbose).</span></span>

<span data-ttu-id="e6978-185">**Web sunucusu günlüğü**.</span><span class="sxs-lookup"><span data-stu-id="e6978-185">**Web server logging**.</span></span> <span data-ttu-id="e6978-186">Günlükleri hello W3C Genişletilmiş günlük dosyası biçiminde kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="e6978-186">Logs are saved in hello W3C extended log file format.</span></span> 

<span data-ttu-id="e6978-187">**Ayrıntılı hata iletileri**.</span><span class="sxs-lookup"><span data-stu-id="e6978-187">**Detailed error messages**.</span></span> <span data-ttu-id="e6978-188">.Htm dosyaları kaydeder ayrıntılı hata iletileri.</span><span class="sxs-lookup"><span data-stu-id="e6978-188">Saves detailed error messages .htm files.</span></span> <span data-ttu-id="e6978-189">Merhaba dosyaları /LogFiles/DetailedErrors altında kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="e6978-189">hello files are saved under /LogFiles/DetailedErrors.</span></span> 

<span data-ttu-id="e6978-190">**Başarısız istek izleme**.</span><span class="sxs-lookup"><span data-stu-id="e6978-190">**Failed request tracing**.</span></span> <span data-ttu-id="e6978-191">Günlükleri istekleri tooXML dosyaları başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="e6978-191">Logs failed requests tooXML files.</span></span> <span data-ttu-id="e6978-192">Merhaba dosyalar/LogFiles/altında W3SVC kaydedilir*xxx*, burada xxx benzersiz bir tanımlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="e6978-192">hello files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span></span> <span data-ttu-id="e6978-193">Bu klasör bir XSL dosyası ve bir veya daha fazla XML dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="e6978-193">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="e6978-194">Biçimlendirme ve hello XML dosyaları Merhaba içeriğine filtreleme için işlevsellik sağlar olduğundan emin toodownload hello XSL dosyasını olun.</span><span class="sxs-lookup"><span data-stu-id="e6978-194">Make sure toodownload hello XSL file, because it provides functionality for formatting and filtering hello contents of hello XML files.</span></span>

<span data-ttu-id="e6978-195">tooview hello günlük dosyaları, FTP kimlik bilgileri, şu şekilde oluşturmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e6978-195">tooview hello log files, you must create FTP credentials, as follows:</span></span>

1. <span data-ttu-id="e6978-196">Web uygulamanız için Hello dikey penceresinde tıklayın **tüm ayarları**.</span><span class="sxs-lookup"><span data-stu-id="e6978-196">In hello blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="e6978-197">Tıklatın **dağıtım kimlik bilgileri**.</span><span class="sxs-lookup"><span data-stu-id="e6978-197">Click **Deployment credentials**.</span></span>
3. <span data-ttu-id="e6978-198">Bir kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="e6978-198">Enter a user name and password.</span></span>
4. <span data-ttu-id="e6978-199">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e6978-199">Click **Save**.</span></span>

![Dağıtım kimlik bilgilerini ayarlama][configure03]

<span data-ttu-id="e6978-201">Merhaba tam FTP kullanıcı adı. "app\username" nerede *uygulama* web uygulamanızı hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="e6978-201">hello full FTP user name is “app\username” where *app* is hello name of your web app.</span></span> <span data-ttu-id="e6978-202">Merhaba kullanıcıadı hello web uygulaması dikey penceresinde altında listelenen **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="e6978-202">hello username is listed in hello web app blade, under **Essentials**.</span></span>  

![FTP dağıtımı kimlik bilgileri][configure02]

## <a name="other-configuration-tasks"></a><span data-ttu-id="e6978-204">Diğer yapılandırma görevleri</span><span class="sxs-lookup"><span data-stu-id="e6978-204">Other configuration tasks</span></span>
### <a name="ssl"></a><span data-ttu-id="e6978-205">SSL</span><span class="sxs-lookup"><span data-stu-id="e6978-205">SSL</span></span>
<span data-ttu-id="e6978-206">Temel veya standart modunda özel bir etki alanı için SSL sertifikalarını karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6978-206">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span></span> <span data-ttu-id="e6978-207">[Web uygulaması için HTTPS'yi etkinleştir] daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="e6978-207">For more information, see [Enable HTTPS for a web app].</span></span> 

<span data-ttu-id="e6978-208">Karşıya yüklenen sertifikalarınızı tooview tıklatın **tüm ayarları** > **özel etki alanları ve SSL**.</span><span class="sxs-lookup"><span data-stu-id="e6978-208">tooview your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="domain-names"></a><span data-ttu-id="e6978-209">Etki alanı adları</span><span class="sxs-lookup"><span data-stu-id="e6978-209">Domain names</span></span>
<span data-ttu-id="e6978-210">Web uygulamanız için özel etki alanı adlarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e6978-210">Add custom domain names for your web app.</span></span> <span data-ttu-id="e6978-211">Daha fazla bilgi için bkz: [yapılandırma Azure App Service'te bir web uygulaması için bir özel etki alanı adı].</span><span class="sxs-lookup"><span data-stu-id="e6978-211">For more information, see [Configure a custom domain name for a web app in Azure App Service].</span></span>

<span data-ttu-id="e6978-212">etki alanı adlarınızı tooview tıklatın **tüm ayarları** > **özel etki alanları ve SSL**.</span><span class="sxs-lookup"><span data-stu-id="e6978-212">tooview your domain names, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="deployments"></a><span data-ttu-id="e6978-213">Dağıtımlar</span><span class="sxs-lookup"><span data-stu-id="e6978-213">Deployments</span></span>
* <span data-ttu-id="e6978-214">Sürekli dağıtım ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e6978-214">Set up continuous deployment.</span></span> <span data-ttu-id="e6978-215">Bkz: [kullanarak Git toodeploy Azure App Service'te Web uygulamalarını](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e6978-215">See [Using Git toodeploy Web Apps in Azure App Service](web-sites-deploy.md).</span></span>
* <span data-ttu-id="e6978-216">Dağıtım yuvaları.</span><span class="sxs-lookup"><span data-stu-id="e6978-216">Deployment slots.</span></span> <span data-ttu-id="e6978-217">Bkz: [tooStaging ortamlar için Azure App Service'te Web uygulamalarını dağıtma].</span><span class="sxs-lookup"><span data-stu-id="e6978-217">See [Deploy tooStaging Environments for Web Apps in Azure App Service].</span></span>

<span data-ttu-id="e6978-218">tooview tıklatın, dağıtım yuvası **tüm ayarları** > **dağıtım yuvası**.</span><span class="sxs-lookup"><span data-stu-id="e6978-218">tooview your deployment slots, click **All Settings** > **Deployment slots**.</span></span>

### <a name="monitoring"></a><span data-ttu-id="e6978-219">İzleme</span><span class="sxs-lookup"><span data-stu-id="e6978-219">Monitoring</span></span>
<span data-ttu-id="e6978-220">Temel veya standart modunda hello kullanılabilirlik HTTP veya HTTPS uç noktaları, gelen toothree coğrafi olarak dağıtılan konumları test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6978-220">In Basic or Standard mode, you can  test hello availability of HTTP or HTTPS endpoints, from up toothree geo-distributed locations.</span></span> <span data-ttu-id="e6978-221">Merhaba HTTP yanıt kodu bir hata (4xx veya 5xx) ya da 30 saniyeden fazla hello yanıt alır, izleme testi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="e6978-221">A monitoring test fails if hello HTTP response code is an error (4xx or 5xx) or hello response takes more than 30 seconds.</span></span> <span data-ttu-id="e6978-222">Bir uç nokta hello izleme sınamalarını tümünden başarılı kullanılabilir sayılması hello belirtilen konumları.</span><span class="sxs-lookup"><span data-stu-id="e6978-222">An endpoint is considered available if hello monitoring tests succeed from all hello specified locations.</span></span> 

<span data-ttu-id="e6978-223">Daha fazla bilgi için bkz: [nasıl yapılır: izleme web uç noktası durumu].</span><span class="sxs-lookup"><span data-stu-id="e6978-223">For more information, see [How to: Monitor web endpoint status].</span></span>

> [!NOTE]
> <span data-ttu-id="e6978-224">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin], burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6978-224">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e6978-225">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="e6978-225">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e6978-226">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e6978-226">Next steps</span></span>
* <span data-ttu-id="e6978-227">[Azure App Service'te özel etki alanı adını yapılandırma]</span><span class="sxs-lookup"><span data-stu-id="e6978-227">[Configure a custom domain name in Azure App Service]</span></span>
* <span data-ttu-id="e6978-228">[Azure uygulama hizmetinde bir uygulama için HTTPS'yi etkinleştir]</span><span class="sxs-lookup"><span data-stu-id="e6978-228">[Enable HTTPS for an app in Azure App Service]</span></span>
* <span data-ttu-id="e6978-229">[Bir web uygulamasını Azure App Service'te ölçeklendirme]</span><span class="sxs-lookup"><span data-stu-id="e6978-229">[Scale a web app in Azure App Service]</span></span>
* <span data-ttu-id="e6978-230">[Azure App Service'deki Web uygulamaları için izleme temelleri]</span><span class="sxs-lookup"><span data-stu-id="e6978-230">[Monitoring basics for Web Apps in Azure App Service]</span></span>

<!-- URL List -->

[ASP.NET SignalR]: http://www.asp.net/signalr
[Azure Portal]: https://portal.azure.com/
[Azure App Service'te özel etki alanı adını yapılandırma]: ./app-service-web-tutorial-custom-domain.md
[tooStaging ortamlar için Azure App Service'te Web uygulamalarını dağıtma]: ./web-sites-staged-publishing.md
[Azure uygulama hizmetinde bir uygulama için HTTPS'yi etkinleştir]: ./app-service-web-tutorial-custom-ssl.md
[nasıl yapılır: izleme web uç noktası durumu]: http://go.microsoft.com/fwLink/?LinkID=279906
[Azure App Service'deki Web uygulamaları için izleme temelleri]: ./web-sites-monitor.md
[ardışık düzen modu]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[Bir web uygulamasını Azure App Service'te ölçeklendirme]: ./web-sites-scale.md
[Socket.IO]: ./web-sites-nodejs-chat-app-socketio.md
[App Service'i deneyin]: https://azure.microsoft.com/try/app-service/

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
