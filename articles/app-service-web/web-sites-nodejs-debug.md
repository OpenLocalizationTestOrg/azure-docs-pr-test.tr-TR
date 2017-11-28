---
title: "aaaHow toodebug Azure App Service'te bir Node.js web uygulaması"
description: "Nasıl toodebug bir Node.js web uygulamasını Azure App Service'te öğrenin."
tags: azure-portal
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: a48f906c-1a3e-43bc-ae84-7d2dde175b15
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 888ec5c3f92cfc3aeea4ea86005b9b6a0d1306ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-a-nodejs-web-app-in-azure-app-service"></a><span data-ttu-id="a5a4b-103">Nasıl toodebug bir Node.js web uygulamasını Azure App Service'te</span><span class="sxs-lookup"><span data-stu-id="a5a4b-103">How toodebug a Node.js web app in Azure App Service</span></span>
<span data-ttu-id="a5a4b-104">Azure içinde barındırılan Node.js uygulamalarında hata ayıklama ile yerleşik tanılama tooassist sağlar [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-104">Azure provides built-in diagnostics tooassist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="a5a4b-105">Bu makalede, öğreneceksiniz nasıl tooenable günlük stdout ve stderr, görünen hata bilgilerini hello tarayıcıda ve nasıl toodownload ve görünüm günlük dosyaları.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-105">In this article, you will learn how tooenable logging of stdout and stderr, display error information in hello browser, and how toodownload and view log files.</span></span>

<span data-ttu-id="a5a4b-106">Azure üzerinde barındırılan Node.js uygulamaları için tanılama tarafından sağlanan [IISNode].</span><span class="sxs-lookup"><span data-stu-id="a5a4b-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span></span> <span data-ttu-id="a5a4b-107">Tanılama bilgilerini toplamak için hello en yaygın ayarları bu makalede ele olsa da, onu tam bir başvuru IISNode ile çalışmak için sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-107">While this article discusses hello most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span></span> <span data-ttu-id="a5a4b-108">Merhaba IISNode ile çalışma hakkında daha fazla bilgi için bkz: [IISNode Benioku] github'da.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-108">For more information on working with IISNode, see hello [IISNode Readme] on GitHub.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="a5a4b-109">Günlü kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a5a4b-109">Enable logging</span></span>
<span data-ttu-id="a5a4b-110">Varsayılan olarak, bir App Service web uygulaması yalnızca Git kullanarak bir web uygulaması dağıttığınızda gibi dağıtımları hakkında tanılama bilgilerini yakalar.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span></span> <span data-ttu-id="a5a4b-111">Başvurulan modül yüklenirken bir hata gibi dağıtım sırasında sorun yaşıyorsanız bu bilgiler yararlıdır **package.json**, veya bir özel dağıtım komut dosyası kullanıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span></span>

<span data-ttu-id="a5a4b-112">tooenable hello stdout ve stderr akışları günlüğü, oluşturmanız gerekir bir **IISNode.yml** dosya hello Node.js uygulamanızı kökünde ve hello aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a5a4b-112">tooenable hello logging of stdout and stderr streams, you must create an **IISNode.yml** file at hello root of your Node.js application and add hello following:</span></span>

    loggingEnabled: true

<span data-ttu-id="a5a4b-113">Bu, Node.js uygulamanızdan stdout ve stderr hello günlük kaydını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-113">This enables hello logging of stderr and stdout from your Node.js application.</span></span>

<span data-ttu-id="a5a4b-114">Merhaba **IISNode.yml** bir hata oluştuğunda kolay hataları veya Geliştirici hataları toohello tarayıcı döndürülen olup olmadığını dosya kullanılan toocontrol de olabilir.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-114">hello **IISNode.yml** file can also be used toocontrol whether friendly errors or developer errors are returned toohello browser when a failure occurs.</span></span> <span data-ttu-id="a5a4b-115">tooenable Geliştirici hataları ekleme satırı toohello aşağıdaki hello **IISNode.yml** dosyası:</span><span class="sxs-lookup"><span data-stu-id="a5a4b-115">tooenable developer errors, add hello following line toohello **IISNode.yml** file:</span></span>

    devErrorsEnabled: true

<span data-ttu-id="a5a4b-116">Bu seçenek etkinleştirildiğinde, IISNode hello son 64 K "bir iç sunucu hatası oluştu"gibi kolay hatası yerine toostderr gönderilen bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-116">Once this option is enabled, IISNode will return hello last 64K of information sent toostderr instead of a friendly error such as "an internal server error occurred".</span></span>

> [!NOTE]
> <span data-ttu-id="a5a4b-117">DevErrorsEnabled geliştirme sırasında sorunları tanılamada yararlı olsa da, bir üretim ortamında etkinleştirme tooend kullanıcılara gönderilen geliştirme hatalarına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent tooend users.</span></span>
> 
> 

<span data-ttu-id="a5a4b-118">Merhaba, **IISNode.yml** dosya, uygulama içinde zaten yoktu, güncelleştirilmiş hello uygulama yayımlandıktan sonra web uygulamanızı yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-118">If hello **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing hello updated application.</span></span> <span data-ttu-id="a5a4b-119">Var olan ayarları değiştiriyorsanız **IISNode.yml** daha önce yayımlanan dosyası, yeniden başlatma gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span></span>

> [!NOTE]
> <span data-ttu-id="a5a4b-120">Web uygulamanızı hello Azure komut satırı araçlarını veya Azure PowerShell cmdlet'leri, varsayılan kullanarak oluşturduysanız **IISNode.yml** dosyası otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-120">If your web app was created using hello Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span></span>
> 
> 

<span data-ttu-id="a5a4b-121">toorestart hello web uygulaması, select hello web uygulamasında hello [Azure Portal](https://portal.azure.com)ve ardından **yeniden** düğmesi:</span><span class="sxs-lookup"><span data-stu-id="a5a4b-121">toorestart hello web app, select hello web app in hello [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span></span>

![düğme yeniden başlatın][restart-button]

<span data-ttu-id="a5a4b-123">Hello Azure komut satırı araçları geliştirme ortamınızda yüklü değilse, komutu toorestart hello web uygulama aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a5a4b-123">If hello Azure Command-Line Tools are installed in your development environment, you can use hello following command toorestart hello web app:</span></span>

    azure site restart [sitename]

> [!NOTE]
> <span data-ttu-id="a5a4b-124">LoggingEnabled ve devErrorsEnabled tanılama bilgileri yakalamak için en yaygın olarak kullanılan hello IISNode.yml yapılandırma seçenekleri olsa da, IISNode.yml kullanılan tooconfigure çeşitli seçenekleri barındırma ortamınıza olabilir.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-124">While loggingEnabled and devErrorsEnabled are hello most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used tooconfigure a variety of options for your hosting environment.</span></span> <span data-ttu-id="a5a4b-125">Merhaba hello yapılandırma seçeneklerinin tam bir listesi için bkz: [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) dosya.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-125">For a full list of hello configuration options, see hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span></span>
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a><span data-ttu-id="a5a4b-126">Günlükleri erişme</span><span class="sxs-lookup"><span data-stu-id="a5a4b-126">Accessing logs</span></span>
<span data-ttu-id="a5a4b-127">Tanılama günlüklerini üç yolla erişilebilir; Hello Dosya Aktarım Protokolü (Zip arşivini indirme FTP), kullanarak veya bir dinamik güncelleştirilen akış hello günlüğünün (kuyruk olarak da bilinir).</span><span class="sxs-lookup"><span data-stu-id="a5a4b-127">Diagnostic logs can be accessed in three ways; Using hello File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of hello log (also known as a tail).</span></span> <span data-ttu-id="a5a4b-128">Merhaba Zip arşivini hello günlük dosyalarının indirilirken veya hello canlı akış görüntüleme hello Azure komut satırı araçları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-128">Downloading hello Zip archive of hello log files or viewing hello live stream require hello Azure Command-Line Tools.</span></span> <span data-ttu-id="a5a4b-129">Bu komutu aşağıdaki hello kullanılarak yüklenebilir:</span><span class="sxs-lookup"><span data-stu-id="a5a4b-129">These can be installed by using hello following command:</span></span>

    npm install azure-cli -g

<span data-ttu-id="a5a4b-130">Bir kez yüklendikten sonra hello araçları hello 'azure' komutunu kullanarak erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-130">Once installed, hello tools can be accessed using hello 'azure' command.</span></span> <span data-ttu-id="a5a4b-131">komut satırı araçları hello ilk yapılandırılmış toouse, Azure aboneliğinizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-131">hello command-line tools must first be configured toouse your Azure subscription.</span></span> <span data-ttu-id="a5a4b-132">Merhaba nasıl tooaccomplish bu görev hakkında daha fazla bilgi için bkz **nasıl toodownload ve içeri aktarma yayımlama ayarları** hello bölümünü [nasıl tooUse hello Azure komut satırı araçları](../xplat-cli-connect.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-132">For information on how tooaccomplish this task, see hello **How toodownload and import publish settings** section of hello [How tooUse hello Azure Command-Line Tools](../xplat-cli-connect.md) article.</span></span>

### <a name="ftp"></a><span data-ttu-id="a5a4b-133">FTP</span><span class="sxs-lookup"><span data-stu-id="a5a4b-133">FTP</span></span>
<span data-ttu-id="a5a4b-134">FTP üzerinden tooaccess hello tanılama bilgilerini ziyaret hello [Azure Portal](https://portal.azure.com), web uygulamanızı seçin ve ardından hello seçin **PANO**.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-134">tooaccess hello diagnostic information through FTP, visit hello [Azure Portal](https://portal.azure.com), select your web app, and then select hello **DASHBOARD**.</span></span> <span data-ttu-id="a5a4b-135">Merhaba, **hızlı bağlantılar** hello bölümünde **FTP tanılama GÜNLÜKLERİ** ve **FTPS tanılama GÜNLÜKLERİ** hello FTP protokolünü kullanarak erişim toohello günlükleri bağlantılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-135">In hello **quick links** section, hello **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access toohello logs using hello FTP protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="a5a4b-136">Daha önce kullanıcı adı ve parola FTP veya dağıtım için yapılandırmadıysanız, hello bunu yapabilirsiniz **Hızlı Başlangıç** seçerek Yönetim sayfasında **dağıtım kimlik bilgilerini ayarlayın**.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-136">If you have not previously configured user name and password for FTP or deployment, you can do so from hello **Quickstart** management page by selecting **Set up deployment credentials**.</span></span>
> 
> 

<span data-ttu-id="a5a4b-137">Merhaba FTP hello panosunda döndürülen Merhaba URL'dir **LogFiles** alt dizinleri izleyen hello içerecek dizini:</span><span class="sxs-lookup"><span data-stu-id="a5a4b-137">hello FTP URL returned in hello dashboard is for hello **LogFiles** directory, which will contain hello following sub-directories:</span></span>

* <span data-ttu-id="a5a4b-138">[Dağıtım yöntemi](web-sites-deploy.md) -Git gibi dağıtım yöntemi kullanırsanız, bir dizin aynı adı oluşturulur ve bilgileri içerir hello toodeployments ilgili.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of hello same name will be created and will contain information related toodeployments.</span></span>
* <span data-ttu-id="a5a4b-139">nodejs - (loggingEnabled true olduğunda.), uygulamanızın tüm örneklerden yakalanan Stdout ve stderr bilgileri</span><span class="sxs-lookup"><span data-stu-id="a5a4b-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="zip-archive"></a><span data-ttu-id="a5a4b-140">Zip arşivini</span><span class="sxs-lookup"><span data-stu-id="a5a4b-140">Zip archive</span></span>
<span data-ttu-id="a5a4b-141">Zip arşivini hello Azure komut satırı araçları'ndan komutu aşağıdaki kullanım hello hello tanılama günlüklerinin toodownload:</span><span class="sxs-lookup"><span data-stu-id="a5a4b-141">toodownload a Zip archive of hello diagnostic logs, use hello following command from hello Azure Command-Line Tools:</span></span>

    azure site log download [sitename]

<span data-ttu-id="a5a4b-142">Bu yükleyecek bir **diagnostics.zip** hello geçerli dizinde.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-142">This will download a **diagnostics.zip** in hello current directory.</span></span> <span data-ttu-id="a5a4b-143">Bu Arşiv hello aşağıdaki dizin yapısını içerir:</span><span class="sxs-lookup"><span data-stu-id="a5a4b-143">This archive contains hello following directory structure:</span></span>

* <span data-ttu-id="a5a4b-144">dağıtımları - uygulamanızın dağıtımları hakkında bilgi günlüğü</span><span class="sxs-lookup"><span data-stu-id="a5a4b-144">deployments - A log of information about deployments of your application</span></span>
* <span data-ttu-id="a5a4b-145">LogFiles</span><span class="sxs-lookup"><span data-stu-id="a5a4b-145">LogFiles</span></span>
  
  * <span data-ttu-id="a5a4b-146">[Dağıtım yöntemi](web-sites-deploy.md) -Git gibi dağıtım yöntemi kullanırsanız, bir dizin aynı adı oluşturulur ve bilgileri içerir hello toodeployments ilgili.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of hello same name will be created and will contain information related toodeployments.</span></span>
  * <span data-ttu-id="a5a4b-147">nodejs - (loggingEnabled true olduğunda.), uygulamanızın tüm örneklerden yakalanan Stdout ve stderr bilgileri</span><span class="sxs-lookup"><span data-stu-id="a5a4b-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="live-stream-tail"></a><span data-ttu-id="a5a4b-148">Canlı akış (kuyruk)</span><span class="sxs-lookup"><span data-stu-id="a5a4b-148">Live stream (tail)</span></span>
<span data-ttu-id="a5a4b-149">tooview tanılama günlük bilgilerinin kullanımı hello hello Azure komut satırı araçları'ndan komutu aşağıdaki canlı akış:</span><span class="sxs-lookup"><span data-stu-id="a5a4b-149">tooview a live stream of diagnostic log information, use hello following command from hello Azure Command-Line Tools:</span></span>

    azure site log tail [sitename]

<span data-ttu-id="a5a4b-150">Bu hello sunucuda oluşurken, güncelleştirilmiş günlük olaylarının bir akış döndürür.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-150">This will return a stream of log events that are updated as they occur on hello server.</span></span> <span data-ttu-id="a5a4b-151">(LoggingEnabled true olduğunda.) Bu akış stdout ve stderr bilgi yanı sıra dağıtım bilgilerini döndürür</span><span class="sxs-lookup"><span data-stu-id="a5a4b-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="a5a4b-152">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="a5a4b-152">Next Steps</span></span>
<span data-ttu-id="a5a4b-153">Bu, nasıl öğrenilen makale Azure tooenable ve erişim tanılama bilgileri.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-153">In this article you learned how tooenable and access diagnostics information for Azure.</span></span> <span data-ttu-id="a5a4b-154">Bu bilgiler yararlı olsa da, kullanmakta olduğunuz bir modül veya App Service Web Apps tarafından kullanılan Node.js hello sürümünün tooa sorun gösterebilir uygulamanızla birlikte oluşan anlama sorunları hello Dağıtımınızda kullanılan farklı ortam.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-154">While this information is useful in understanding problems that occur with your application, it may point tooa problem with a module you are using or that hello version of Node.js used by App Service Web Apps is different than hello one used in your deployment environment.</span></span>

<span data-ttu-id="a5a4b-155">Modüllerle çalışma Azure ile ilgili bilgi için [Azure uygulamalarıyla Node.js modüllerini kullanma](../nodejs-use-node-modules-azure-apps.md).</span><span class="sxs-lookup"><span data-stu-id="a5a4b-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span></span>

<span data-ttu-id="a5a4b-156">Uygulamanız için Node.js sürümünü belirtme hakkında daha fazla bilgi için bkz: [bir Azure uygulamasında Node.js sürümünü belirtme].</span><span class="sxs-lookup"><span data-stu-id="a5a4b-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span></span>

<span data-ttu-id="a5a4b-157">Daha fazla bilgi için hello Ayrıca bkz. [Node.js Geliştirici Merkezi](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="a5a4b-157">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="a5a4b-158">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="a5a4b-158">What's changed</span></span>
* <span data-ttu-id="a5a4b-159">Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="a5a4b-159">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="a5a4b-160">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-160">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a5a4b-161">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a5a4b-161">No credit cards required; no commitments.</span></span>
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[IISNode Benioku]: https://github.com/tjanczuk/iisnode#readme
[How tooUse hello Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[bir Azure uygulamasında Node.js sürümünü belirtme]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

