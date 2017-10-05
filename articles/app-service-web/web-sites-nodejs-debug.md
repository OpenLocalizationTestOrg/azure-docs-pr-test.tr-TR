---
title: "Azure App Service’teki bir Node.js web uygulamasına hata ayıklama"
description: "Azure App Service'te Node.js web uygulamasına hata ayıklama öğrenin."
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
ms.openlocfilehash: 5e302a4c58a171d40e43a22c34c724e868019ec8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-debug-a-nodejs-web-app-in-azure-app-service"></a><span data-ttu-id="b1889-103">Azure App Service’teki bir Node.js web uygulamasına hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="b1889-103">How to debug a Node.js web app in Azure App Service</span></span>
<span data-ttu-id="b1889-104">Azure içinde barındırılan Node.js uygulamalarını hata ayıklamaya yardımcı olması için yerleşik tanılama sağlar [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="b1889-104">Azure provides built-in diagnostics to assist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="b1889-105">Bu makalede, stdout ve stderr günlük kaydını etkinleştirmek için tarayıcıda hata bilgilerini görüntülemek nasıl ve indirmek ve günlük dosyalarını görüntülemek nasıl öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="b1889-105">In this article, you will learn how to enable logging of stdout and stderr, display error information in the browser, and how to download and view log files.</span></span>

<span data-ttu-id="b1889-106">Azure üzerinde barındırılan Node.js uygulamaları için tanılama tarafından sağlanan [IISNode].</span><span class="sxs-lookup"><span data-stu-id="b1889-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span></span> <span data-ttu-id="b1889-107">Tanılama bilgilerini toplamak için en yaygın ayarları bu makalede ele olsa da, onu tam bir başvuru IISNode ile çalışmak için sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="b1889-107">While this article discusses the most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span></span> <span data-ttu-id="b1889-108">IISNode ile çalışma hakkında daha fazla bilgi için bkz: [IISNode Benioku] github'da.</span><span class="sxs-lookup"><span data-stu-id="b1889-108">For more information on working with IISNode, see the [IISNode Readme] on GitHub.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="b1889-109">Günlü kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="b1889-109">Enable logging</span></span>
<span data-ttu-id="b1889-110">Varsayılan olarak, bir App Service web uygulaması yalnızca Git kullanarak bir web uygulaması dağıttığınızda gibi dağıtımları hakkında tanılama bilgilerini yakalar.</span><span class="sxs-lookup"><span data-stu-id="b1889-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span></span> <span data-ttu-id="b1889-111">Başvurulan modül yüklenirken bir hata gibi dağıtım sırasında sorun yaşıyorsanız bu bilgiler yararlıdır **package.json**, veya bir özel dağıtım komut dosyası kullanıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="b1889-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span></span>

<span data-ttu-id="b1889-112">Stdout ve stderr akışları günlüğe yazılmasını etkinleştirmek için oluşturmalısınız bir **IISNode.yml** dosya, Node.js uygulamanızın kök dizininde ve aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b1889-112">To enable the logging of stdout and stderr streams, you must create an **IISNode.yml** file at the root of your Node.js application and add the following:</span></span>

    loggingEnabled: true

<span data-ttu-id="b1889-113">Bu, Node.js uygulamanızdan stdout ve stderr günlük kaydını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="b1889-113">This enables the logging of stderr and stdout from your Node.js application.</span></span>

<span data-ttu-id="b1889-114">**IISNode.yml** dosya de kullanılabilir denetlemek için bir hata oluştuğunda kolay hataları veya Geliştirici hataları tarayıcıya döndürülür olup olmadığını.</span><span class="sxs-lookup"><span data-stu-id="b1889-114">The **IISNode.yml** file can also be used to control whether friendly errors or developer errors are returned to the browser when a failure occurs.</span></span> <span data-ttu-id="b1889-115">Geliştirici hataları etkinleştirmek için aşağıdaki satırı ekleyin **IISNode.yml** dosyası:</span><span class="sxs-lookup"><span data-stu-id="b1889-115">To enable developer errors, add the following line to the **IISNode.yml** file:</span></span>

    devErrorsEnabled: true

<span data-ttu-id="b1889-116">Bu seçenek etkinleştirildiğinde, IISNode son 64 K stderr kolay hatası yerine "İç sunucu hatası oluştu"gibi gönderilen bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="b1889-116">Once this option is enabled, IISNode will return the last 64K of information sent to stderr instead of a friendly error such as "an internal server error occurred".</span></span>

> [!NOTE]
> <span data-ttu-id="b1889-117">DevErrorsEnabled geliştirme sırasında sorunları tanılamada yararlı olsa da, bir üretim ortamında etkinleştirme son kullanıcılara gönderilen geliştirme hataları neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="b1889-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent to end users.</span></span>
> 
> 

<span data-ttu-id="b1889-118">Varsa **IISNode.yml** dosya, uygulama içinde zaten yoktu, güncelleştirilmiş uygulama yayımlandıktan sonra web uygulamanızı yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1889-118">If the **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing the updated application.</span></span> <span data-ttu-id="b1889-119">Var olan ayarları değiştiriyorsanız **IISNode.yml** daha önce yayımlanan dosyası, yeniden başlatma gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b1889-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span></span>

> [!NOTE]
> <span data-ttu-id="b1889-120">Web uygulamanızı Azure komut satırı araçlarını veya Azure PowerShell cmdlet'leri, varsayılan kullanarak oluşturduysanız **IISNode.yml** dosyası otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b1889-120">If your web app was created using the Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span></span>
> 
> 

<span data-ttu-id="b1889-121">Web uygulaması yeniden için web uygulaması seçin [Azure Portal](https://portal.azure.com)ve ardından **yeniden** düğmesi:</span><span class="sxs-lookup"><span data-stu-id="b1889-121">To restart the web app, select the web app in the [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span></span>

![düğme yeniden başlatın][restart-button]

<span data-ttu-id="b1889-123">Azure komut satırı araçları geliştirme ortamınızda yüklü değilse, web uygulaması yeniden başlatmak için aşağıdaki komutu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b1889-123">If the Azure Command-Line Tools are installed in your development environment, you can use the following command to restart the web app:</span></span>

    azure site restart [sitename]

> [!NOTE]
> <span data-ttu-id="b1889-124">En sık IISNode.yml yapılandırma seçenekleri tanılama bilgileri yakalamak için kullanılan loggingEnabled ve devErrorsEnabled olmakla birlikte, IISNode.yml çeşitli barındırma ortamınız için seçenekleri yapılandırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b1889-124">While loggingEnabled and devErrorsEnabled are the most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used to configure a variety of options for your hosting environment.</span></span> <span data-ttu-id="b1889-125">Yapılandırma seçeneklerinin tam bir listesi için bkz: [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) dosya.</span><span class="sxs-lookup"><span data-stu-id="b1889-125">For a full list of the configuration options, see the [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span></span>
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a><span data-ttu-id="b1889-126">Günlükleri erişme</span><span class="sxs-lookup"><span data-stu-id="b1889-126">Accessing logs</span></span>
<span data-ttu-id="b1889-127">Tanılama günlüklerini üç yolla erişilebilir; Dosya Aktarım Protokolü (Zip arşivini indirme FTP), kullanarak veya bir dinamik güncelleştirilen akış günlük (kuyruk olarak da bilinir).</span><span class="sxs-lookup"><span data-stu-id="b1889-127">Diagnostic logs can be accessed in three ways; Using the File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of the log (also known as a tail).</span></span> <span data-ttu-id="b1889-128">Günlük dosyalarının Zip arşivini indirilirken veya bir canlı akışı görüntüleme Azure komut satırı araçları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b1889-128">Downloading the Zip archive of the log files or viewing the live stream require the Azure Command-Line Tools.</span></span> <span data-ttu-id="b1889-129">Bunlar, aşağıdaki komutu kullanarak yüklenebilir:</span><span class="sxs-lookup"><span data-stu-id="b1889-129">These can be installed by using the following command:</span></span>

    npm install azure-cli -g

<span data-ttu-id="b1889-130">Yüklendikten sonra Araçlar 'azure' komutunu kullanarak erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="b1889-130">Once installed, the tools can be accessed using the 'azure' command.</span></span> <span data-ttu-id="b1889-131">Komut satırı araçlarını, ilk Azure aboneliğinizi kullanmak üzere yapılandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b1889-131">The command-line tools must first be configured to use your Azure subscription.</span></span> <span data-ttu-id="b1889-132">Bu görevi gerçekleştirmek hakkında daha fazla bilgi için bkz: **nasıl yükleneceği ve yayımlama ayarlarını içeri aktar** bölümünü [Azure komut satırı araçlarını kullanın nasıl](../xplat-cli-connect.md) makale.</span><span class="sxs-lookup"><span data-stu-id="b1889-132">For information on how to accomplish this task, see the **How to download and import publish settings** section of the [How to Use The Azure Command-Line Tools](../xplat-cli-connect.md) article.</span></span>

### <a name="ftp"></a><span data-ttu-id="b1889-133">FTP</span><span class="sxs-lookup"><span data-stu-id="b1889-133">FTP</span></span>
<span data-ttu-id="b1889-134">FTP aracılığıyla tanılama bilgilerine erişmek için ziyaret [Azure Portal](https://portal.azure.com)web uygulamanızı seçin ve ardından **PANO**.</span><span class="sxs-lookup"><span data-stu-id="b1889-134">To access the diagnostic information through FTP, visit the [Azure Portal](https://portal.azure.com), select your web app, and then select the **DASHBOARD**.</span></span> <span data-ttu-id="b1889-135">İçinde **hızlı bağlantılar** bölümünde **FTP tanılama GÜNLÜKLERİ** ve **FTPS tanılama GÜNLÜKLERİ** bağlantılar FTP protokolünü kullanarak günlükleri erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="b1889-135">In the **quick links** section, the **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access to the logs using the FTP protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="b1889-136">Daha önce kullanıcı adı ve parola FTP veya dağıtım için yapılandırmadıysanız, nden yapabilirsiniz **Hızlı Başlangıç** seçerek Yönetim sayfasında **dağıtım kimlik bilgilerini ayarlayın**.</span><span class="sxs-lookup"><span data-stu-id="b1889-136">If you have not previously configured user name and password for FTP or deployment, you can do so from the **Quickstart** management page by selecting **Set up deployment credentials**.</span></span>
> 
> 

<span data-ttu-id="b1889-137">FTP panosunda döndürülen URL içindir **LogFiles** aşağıdaki alt dizinler içerecek dizini:</span><span class="sxs-lookup"><span data-stu-id="b1889-137">The FTP URL returned in the dashboard is for the **LogFiles** directory, which will contain the following sub-directories:</span></span>

* <span data-ttu-id="b1889-138">[Dağıtım yöntemi](web-sites-deploy.md) -Git gibi dağıtım yöntemi kullanırsanız, aynı ada sahip bir dizin oluşturulur ve dağıtımları için ilgili bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="b1889-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span></span>
* <span data-ttu-id="b1889-139">nodejs - (loggingEnabled true olduğunda.), uygulamanızın tüm örneklerden yakalanan Stdout ve stderr bilgileri</span><span class="sxs-lookup"><span data-stu-id="b1889-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="zip-archive"></a><span data-ttu-id="b1889-140">Zip arşivini</span><span class="sxs-lookup"><span data-stu-id="b1889-140">Zip archive</span></span>
<span data-ttu-id="b1889-141">Tanılama günlüklerinin Zip arşivini indirmek için Azure komut satırı araçları aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="b1889-141">To download a Zip archive of the diagnostic logs, use the following command from the Azure Command-Line Tools:</span></span>

    azure site log download [sitename]

<span data-ttu-id="b1889-142">Bu yükleyecek bir **diagnostics.zip** geçerli dizin.</span><span class="sxs-lookup"><span data-stu-id="b1889-142">This will download a **diagnostics.zip** in the current directory.</span></span> <span data-ttu-id="b1889-143">Bu Arşiv aşağıdaki dizin yapısını içerir:</span><span class="sxs-lookup"><span data-stu-id="b1889-143">This archive contains the following directory structure:</span></span>

* <span data-ttu-id="b1889-144">dağıtımları - uygulamanızın dağıtımları hakkında bilgi günlüğü</span><span class="sxs-lookup"><span data-stu-id="b1889-144">deployments - A log of information about deployments of your application</span></span>
* <span data-ttu-id="b1889-145">LogFiles</span><span class="sxs-lookup"><span data-stu-id="b1889-145">LogFiles</span></span>
  
  * <span data-ttu-id="b1889-146">[Dağıtım yöntemi](web-sites-deploy.md) -Git gibi dağıtım yöntemi kullanırsanız, aynı ada sahip bir dizin oluşturulur ve dağıtımları için ilgili bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="b1889-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span></span>
  * <span data-ttu-id="b1889-147">nodejs - (loggingEnabled true olduğunda.), uygulamanızın tüm örneklerden yakalanan Stdout ve stderr bilgileri</span><span class="sxs-lookup"><span data-stu-id="b1889-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="live-stream-tail"></a><span data-ttu-id="b1889-148">Canlı akış (kuyruk)</span><span class="sxs-lookup"><span data-stu-id="b1889-148">Live stream (tail)</span></span>
<span data-ttu-id="b1889-149">Canlı akış tanılama günlük bilgileri görüntülemek için Azure komut satırı araçları aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="b1889-149">To view a live stream of diagnostic log information, use the following command from the Azure Command-Line Tools:</span></span>

    azure site log tail [sitename]

<span data-ttu-id="b1889-150">Bu sunucu üzerinde meydana gelirken, güncelleştirilmiş günlük olaylarının bir akış döndürür.</span><span class="sxs-lookup"><span data-stu-id="b1889-150">This will return a stream of log events that are updated as they occur on the server.</span></span> <span data-ttu-id="b1889-151">(LoggingEnabled true olduğunda.) Bu akış stdout ve stderr bilgi yanı sıra dağıtım bilgilerini döndürür</span><span class="sxs-lookup"><span data-stu-id="b1889-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="b1889-152">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="b1889-152">Next Steps</span></span>
<span data-ttu-id="b1889-153">Bu makalede etkinleştirmek ve Azure tanılama bilgilerine öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="b1889-153">In this article you learned how to enable and access diagnostics information for Azure.</span></span> <span data-ttu-id="b1889-154">Bu bilgiler ile uygulamanızı oluşan anlama sorunları kullanışlı olsa da, kullanmakta olduğunuz veya App Service Web Apps tarafından kullanılan Node.js sürümünü dağıtım ortamınızda kullanılan olandan farklı bir modülü bir soruna işaret edebilir.</span><span class="sxs-lookup"><span data-stu-id="b1889-154">While this information is useful in understanding problems that occur with your application, it may point to a problem with a module you are using or that the version of Node.js used by App Service Web Apps is different than the one used in your deployment environment.</span></span>

<span data-ttu-id="b1889-155">Modüllerle çalışma Azure ile ilgili bilgi için [Azure uygulamalarıyla Node.js modüllerini kullanma](../nodejs-use-node-modules-azure-apps.md).</span><span class="sxs-lookup"><span data-stu-id="b1889-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span></span>

<span data-ttu-id="b1889-156">Uygulamanız için Node.js sürümünü belirtme hakkında daha fazla bilgi için bkz: [bir Azure uygulamasında Node.js sürümünü belirtme].</span><span class="sxs-lookup"><span data-stu-id="b1889-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span></span>

<span data-ttu-id="b1889-157">Daha fazla bilgi için Ayrıca bkz. [Node.js Geliştirici Merkezi](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="b1889-157">For more information, see also the [Node.js Developer Center](/develop/nodejs/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="b1889-158">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="b1889-158">What's changed</span></span>
* <span data-ttu-id="b1889-159">Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="b1889-159">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="b1889-160">Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="b1889-160">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b1889-161">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b1889-161">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="b1889-162">[IISNode]: https://github.com/tjanczuk/iisnode</span><span class="sxs-lookup"><span data-stu-id="b1889-162">[IISNode]: https://github.com/tjanczuk/iisnode</span></span>
<span data-ttu-id="b1889-163">[IISNode Benioku]: https://github.com/tjanczuk/iisnode#readme</span><span class="sxs-lookup"><span data-stu-id="b1889-163">[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme</span></span>
[How to Use The Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
<span data-ttu-id="b1889-164">[bir Azure uygulamasında Node.js sürümünü belirtme]: ../nodejs-specify-node-version-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="b1889-164">[Specifying a Node.js version in an Azure application]: ../nodejs-specify-node-version-azure-apps.md</span></span>

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

