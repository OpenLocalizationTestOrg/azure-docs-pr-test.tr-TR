---
title: "aaaHow toouse Linux Azure Web uygulaması için özel bir Docker görüntü | Microsoft Docs"
description: "Nasıl toouse özel Docker görüntü Linux Azure Web uygulaması için."
keywords: "Azure uygulama hizmeti, web uygulaması, linux, docker, kapsayıcı"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: b97bd4e6-dff0-4976-ac20-d5c109a559a8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 8853095d0e1067cfea4297bbd23b622fe4a0d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a><span data-ttu-id="d06f5-104">Linux üzerinde Azure Web uygulaması için özel bir Docker görüntü kullanma</span><span class="sxs-lookup"><span data-stu-id="d06f5-104">Using a custom Docker image for Azure Web App on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="d06f5-105">Uygulama hizmeti önceden tanımlanmış uygulama yığınları PHP 7.0 ve Node.js 4.5 gibi belirli sürümleri için destek ile Linux'ta sağlar.</span><span class="sxs-lookup"><span data-stu-id="d06f5-105">App Service provides pre-defined application stacks on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span></span> <span data-ttu-id="d06f5-106">Uygulama hizmeti Linux'ta kullanan Docker kapsayıcıları toohost bunlar önceden oluşturulmuş uygulama yığınları.</span><span class="sxs-lookup"><span data-stu-id="d06f5-106">App Service on Linux uses Docker containers toohost these pre-built application stacks.</span></span> <span data-ttu-id="d06f5-107">Bir özel Docker görüntü toodeploy Azure içinde tanımlı değil, web uygulaması tooan uygulama yığınını de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d06f5-107">You can also use a custom Docker image toodeploy your web app tooan application stack that is not already defined in Azure.</span></span> <span data-ttu-id="d06f5-108">Özel Docker görüntülerinizi ya da bir genel veya özel Docker deposu üzerinde barındırılabilir.</span><span class="sxs-lookup"><span data-stu-id="d06f5-108">Custom Docker images can be hosted on either a public or private Docker repository.</span></span>


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a><span data-ttu-id="d06f5-109">Nasıl yapılır: bir web uygulaması için özel bir Docker resmi ayarlama</span><span class="sxs-lookup"><span data-stu-id="d06f5-109">How to: set a custom Docker image for a web app</span></span>
<span data-ttu-id="d06f5-110">Merhaba özel Docker görüntü için hem de yeni ve mevcut webs uygulamalar ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d06f5-110">You can set hello custom Docker image for both new and existing webs apps.</span></span> <span data-ttu-id="d06f5-111">Oluşturduğunuzda, bir web uygulaması Linux'ta hello [Azure portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), tıklatın **yapılandırma kapsayıcısı** tooset özel Docker görüntü:</span><span class="sxs-lookup"><span data-stu-id="d06f5-111">When you create a web app on Linux in hello [Azure portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), click **Configure container** tooset a custom Docker image:</span></span>

![Linux üzerinde yeni bir web uygulaması için özel Docker görüntü][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a><span data-ttu-id="d06f5-113">Nasıl yapılır: özel Docker görüntü Docker hub'dan kullanın</span><span class="sxs-lookup"><span data-stu-id="d06f5-113">How to: use a custom Docker image from Docker Hub</span></span> ##
<span data-ttu-id="d06f5-114">toouse Docker hub'dan özel Docker görüntü:</span><span class="sxs-lookup"><span data-stu-id="d06f5-114">toouse a custom Docker image from Docker Hub:</span></span>

1. <span data-ttu-id="d06f5-115">Merhaba, [Azure portal](https://portal.azure.com), web uygulamanızı Linux üzerinde sonra bulun **ayarları** tıklatın **Docker kapsayıcısı**.</span><span class="sxs-lookup"><span data-stu-id="d06f5-115">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="d06f5-116">Seçin **Docker hub'a** hello olarak **görüntü kaynağı**, ya da ardından **ortak** veya **özel** ve türü hello **görüntü ve İsteğe bağlı etiket adı**, gibi `node:4.5`.</span><span class="sxs-lookup"><span data-stu-id="d06f5-116">Select **Docker Hub** as hello **Image source**, then click either **Public** or **Private** and type hello **Image and optional tag name**, such as `node:4.5`.</span></span> <span data-ttu-id="d06f5-117">Merhaba **başlangıç komutu** kümesi hello Docker yansıma dosyasında tanımlanmış üzerinde otomatik olarak temel alır, ancak kendi komutları ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d06f5-117">hello **Startup command** is set automatically based on what is defined in hello Docker image file, but you can set your own commands.</span></span>  

    ![Yapılandırma Docker hub'a genel depo resmi][2]

    <span data-ttu-id="d06f5-119">Görüntünüzü özel depodan olduğunda tooenter hello Docker hub'a kimlik olarak da gerekir (**oturum açma kullanıcı** ve **parola**) hello özel Docker hub'a depo.</span><span class="sxs-lookup"><span data-stu-id="d06f5-119">When your image is from a private repository, you also need tooenter hello Docker Hub credentials as (**Login username** and **Password**) for hello private Docker Hub repository.</span></span>

    ![Yapılandırma Docker hub'a özel depo resmi][3]

3. <span data-ttu-id="d06f5-121">Merhaba kapsayıcı yapılandırdıktan sonra tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d06f5-121">After you have configured hello container, click **Save**.</span></span>

## <a name="how-toouse-a-docker-image-from-a-private-image-registry"></a><span data-ttu-id="d06f5-122">Nasıl toouse bir Docker görüntü özel görüntü kayıt defterinden</span><span class="sxs-lookup"><span data-stu-id="d06f5-122">How toouse a Docker image from a private image registry</span></span> ##
<span data-ttu-id="d06f5-123">özel görüntü kayıt defterinden özel Docker görüntü toouse:</span><span class="sxs-lookup"><span data-stu-id="d06f5-123">toouse a custom Docker image from a private image registry:</span></span>

1. <span data-ttu-id="d06f5-124">Merhaba, [Azure portal](https://portal.azure.com), web uygulamanızı Linux üzerinde sonra bulun **ayarları** tıklatın **Docker kapsayıcısı**.</span><span class="sxs-lookup"><span data-stu-id="d06f5-124">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="d06f5-125">Tıklatın **özel kayıt defteri** hello olarak **görüntü kaynağı**.</span><span class="sxs-lookup"><span data-stu-id="d06f5-125">Click **Private registry** as hello **Image source**.</span></span> <span data-ttu-id="d06f5-126">Merhaba girin **görüntü ve isteğe bağlı etiket adı**, **sunucu URL'si** hello kimlik bilgileri ile birlikte hello özel kayıt için (**oturum açma kullanıcı** ve **parola** ).</span><span class="sxs-lookup"><span data-stu-id="d06f5-126">Enter hello **Image and optional tag name**, **Server URL** for hello private registry, along with hello credentials (**Login username** and **Password**).</span></span> <span data-ttu-id="d06f5-127">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d06f5-127">Click **Save**.</span></span>

    ![Yapılandırma özel kayıt defteri Docker resmi][4]


## <a name="how-to-set-hello-port-used-by-your-docker-image"></a><span data-ttu-id="d06f5-129">Nasıl yapılır: ayarlama, Docker görüntü tarafından kullanılan başlangıç bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="d06f5-129">How to: set hello port used by your Docker image</span></span> ##

<span data-ttu-id="d06f5-130">Web uygulamanız için özel bir Docker görüntü kullandığınızda hello kullanabilirsiniz `WEBSITES_PORT` oluşturulan toohello kapsayıcı eklenen, Dockerfile ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="d06f5-130">When you use a custom Docker image for your web app, you can use hello `WEBSITES_PORT` environment variable in your Dockerfile, which gets added toohello generated container.</span></span> <span data-ttu-id="d06f5-131">Söyleniş bir uygulama için bir docker dosyası örneği aşağıdaki hello göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="d06f5-131">Consider hello following example of a docker file for a Ruby application:</span></span>

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

<span data-ttu-id="d06f5-132">Merhaba komutu son satırında, bu hello WEBSITES_PORT ortam değişkeni çalışma zamanında geçirilen görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d06f5-132">On last line of hello command, you can see that hello WEBSITES_PORT environment variable is passed at runtime.</span></span> <span data-ttu-id="d06f5-133">Büyük/küçük harf komutlarda önemli unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d06f5-133">Remember that casing matters in commands.</span></span>

<span data-ttu-id="d06f5-134">Daha önce hello platform tarafından kullanılan `PORT` uygulama ayarı biz toodeprecate hello kullan ayarını bu uygulamayı planlama ve toousing taşıma `WEBSITES_PORT` özel olarak.</span><span class="sxs-lookup"><span data-stu-id="d06f5-134">Previously hello platform was using `PORT` app setting, we are planning toodeprecate hello use this app setting and move toousing `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="d06f5-135">Başka bir kullanıcı tarafından oluşturulmuş var olan bir Docker görüntüsünü kullandığınızda, toospecify bağlantı noktası 80 dışında bir bağlantı noktası hello uygulama için gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d06f5-135">When you use an existing Docker image built by someone else, you may need toospecify a port other than port 80 for hello application.</span></span> <span data-ttu-id="d06f5-136">tooconfigure Merhaba bağlantı noktası, adlandırılmış ayarlama uygulama ekleme `WEBSITES_PORT` aşağıda gösterildiği gibi hello değere sahip:</span><span class="sxs-lookup"><span data-stu-id="d06f5-136">tooconfigure hello port, add an application setting named `WEBSITES_PORT` with hello value as shown below:</span></span>

![Özel Docker görüntü için bağlantı noktası uygulama ayarını yapılandırın][6]

## <a name="how-to-set-hello-startup-time-for-your-docker-image"></a><span data-ttu-id="d06f5-138">Nasıl yapılır: hello başlangıç saati, Docker görüntüsü için ayarlayın</span><span class="sxs-lookup"><span data-stu-id="d06f5-138">How to: set hello startup time for your Docker image</span></span> ##

<span data-ttu-id="d06f5-139">Varsayılan olarak, kapsayıcı 230 saniye önce başlamazsa hello platform, kapsayıcı yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="d06f5-139">By default, if your container does not start before 230 seconds, hello platform will restart your container.</span></span> <span data-ttu-id="d06f5-140">Özel Docker görüntünüzü 230 saniyeden fazla başlarsa, hello kullanabilirsiniz `WEBSITES_CONTAINER_START_TIME_LIMIT` ayarını, uygulama için bu ayarın hello değerini saniye cinsinden, bu yeniden başlatmadan önce çalışan, kapsayıcı hello platform Koru izin verir.</span><span class="sxs-lookup"><span data-stu-id="d06f5-140">If your custom Docker image starts in more than 230 seconds, you can use hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting, hello value for this setting is in seconds, this will allow hello platform keep your container running before restarting it.</span></span> <span data-ttu-id="d06f5-141">Merhaba varsayılan değer 230 saniyedir ve hello en büyük değer 600 saniye izin verilir.</span><span class="sxs-lookup"><span data-stu-id="d06f5-141">hello default value is 230 seconds, and hello max allowed value is 600 seconds.</span></span>

## <a name="how-to-unmount-hello-platform-provided-storage"></a><span data-ttu-id="d06f5-142">Nasıl yapılır: hello sağlanan platformu depolama çıkarın</span><span class="sxs-lookup"><span data-stu-id="d06f5-142">How to: unmount hello platform provided storage</span></span> ##

<span data-ttu-id="d06f5-143">Varsayılan olarak, kalıcı depolama paylaşımı toohello hello platform bağlar `\home\` dizin.</span><span class="sxs-lookup"><span data-stu-id="d06f5-143">By default, hello platform will mount a persistent storage share toohello `\home\` directory.</span></span> <span data-ttu-id="d06f5-144">Kapsayıcı görüntünüzü kalıcı bir paylaşımı gerekli değildir, bu depolama ayarı hello tarafından takma devre dışı bırakabilirsiniz `WEBSITES_ENABLE_APP_SERVICE_STORAGE` uygulama çok ayarı`false`.</span><span class="sxs-lookup"><span data-stu-id="d06f5-144">If your container image does not need a persistent share, you can disable mounting that storage by setting hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting too`false`.</span></span> <span data-ttu-id="d06f5-145">Hala hello scm sitesinden erişim toothat depolama alanına sahip ve tüm Docker günlükleri (etkinse) hello platformu tarafından oluşturulan toohello günlük dosyaları yazılır.</span><span class="sxs-lookup"><span data-stu-id="d06f5-145">You will still have access toothat storage from hello scm site, and all Docker logs (if enabled) will be written toohello log files generated by hello platform.</span></span>

## <a name="how-to-switch-back-toousing-a-built-in-image"></a><span data-ttu-id="d06f5-146">Nasıl yapılır: geri dönün toousing yerleşik bir görüntü</span><span class="sxs-lookup"><span data-stu-id="d06f5-146">How to: Switch back toousing a built-in image</span></span> ##

<span data-ttu-id="d06f5-147">özel görüntü toousing yerleşik bir görüntü kullanarak tooswitch:</span><span class="sxs-lookup"><span data-stu-id="d06f5-147">tooswitch from using a custom image toousing a built-in image:</span></span>

1. <span data-ttu-id="d06f5-148">Merhaba, [Azure portal](https://portal.azure.com), web uygulamanızı Linux üzerinde sonra bulun **ayarları** tıklatın **uygulama hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="d06f5-148">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **App Service**.</span></span>

2. <span data-ttu-id="d06f5-149">Seçin, **çalışma zamanı yığın** toouse hello yerleşik görüntüsü, ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d06f5-149">Select your **Runtime Stack** toouse for hello built-in image, then click **Save**.</span></span> 

![Yerleşik Docker görüntüsü yapılandırma][5]


## <a name="troubleshooting"></a><span data-ttu-id="d06f5-151">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="d06f5-151">Troubleshooting</span></span> ##

<span data-ttu-id="d06f5-152">Toostart özel Docker görüntünüzü ile uygulamanızı başarısız olduğunda, hello hello LogFiles dizininde Docker günlüklerini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="d06f5-152">When your application fails toostart with your custom Docker image, check hello Docker logs in hello LogFiles directory.</span></span> <span data-ttu-id="d06f5-153">SCM siteniz veya FTP aracılığıyla bu dizine erişebilir.</span><span class="sxs-lookup"><span data-stu-id="d06f5-153">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="d06f5-154">toolog hello `stdout` ve `stderr` tooenable gerekir, kapsayıcıdan **Docker kapsayıcısı günlük** altında **tanılama günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="d06f5-154">toolog hello `stdout` and `stderr` from your container, you need tooenable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Günlüğü etkinleştirme][8]

![Kudu tooview Docker günlüklerini kullanma][7]

<span data-ttu-id="d06f5-157">Merhaba SCM sitesinden erişebilirsiniz **Gelişmiş Araçlar** hello içinde **geliştirme araçları** menüsü.</span><span class="sxs-lookup"><span data-stu-id="d06f5-157">You can access hello SCM site from **Advanced Tools** in hello **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d06f5-158">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="d06f5-158">Next Steps</span></span> ##

<span data-ttu-id="d06f5-159">Linux üzerinde Web uygulaması ile çalışmaya bağlantılar tooget aşağıdaki hello izleyin.</span><span class="sxs-lookup"><span data-stu-id="d06f5-159">Follow hello following links tooget started with Web App on Linux.</span></span>   

* [<span data-ttu-id="d06f5-160">Giriş tooAzure Linux üzerinde Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="d06f5-160">Introduction tooAzure Web App on Linux</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="d06f5-161">Linux üzerinde Azure Web uygulamasında Node.js için PM2 Yapılandırması'nı kullanarak</span><span class="sxs-lookup"><span data-stu-id="d06f5-161">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](./app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="d06f5-162">Azure App Service Web uygulaması Linux SSS</span><span class="sxs-lookup"><span data-stu-id="d06f5-162">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<span data-ttu-id="d06f5-163">POST sorular ve sorunları üzerinde [forumumuzda](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="d06f5-163">Post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
