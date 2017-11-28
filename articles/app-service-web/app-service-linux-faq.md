---
title: "aaaAzure App Service Web uygulamasında Linux SSS | Microsoft Docs"
description: "Azure App Service Web uygulaması Linux SSS."
keywords: "Azure uygulama hizmeti, web uygulaması, SSS, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: c7798d9144d936eecdc0e191fc870b0ee0b220c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a><span data-ttu-id="3c84d-104">Azure App Service Web uygulaması Linux SSS</span><span class="sxs-lookup"><span data-stu-id="3c84d-104">Azure App Service Web App on Linux FAQ</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="3c84d-105">Özellik ekleme ve geliştirmeler tooour platform yapmadan Linux üzerinde Web uygulaması Hello sürümüyle çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="3c84d-105">With hello release of Web App on Linux, we're working on adding features and making improvements tooour platform.</span></span> <span data-ttu-id="3c84d-106">Bazı sık sorulan aşağıda verilmiştir müşterilerimizin bize hello son isteyen sorular (SSS) ay.</span><span class="sxs-lookup"><span data-stu-id="3c84d-106">Here are some frequently asked questions (FAQ) that our customers have been asking us over hello last months.</span></span>
<span data-ttu-id="3c84d-107">Varsa, yorum hello makale üzerinde sorularınız ve biz bunu mümkün olan en kısa sürede yanıt.</span><span class="sxs-lookup"><span data-stu-id="3c84d-107">If you have a question, comment on hello article and we'll answer it as soon as possible.</span></span>

## <a name="built-in-images"></a><span data-ttu-id="3c84d-108">Yerleşik görüntüleri</span><span class="sxs-lookup"><span data-stu-id="3c84d-108">Built-in images</span></span>

<span data-ttu-id="3c84d-109">**S:** platform hello toofork hello yerleşik Docker kapsayıcıları sağlar istiyorum.</span><span class="sxs-lookup"><span data-stu-id="3c84d-109">**Q:** I want toofork hello built-in Docker containers that hello platform provides.</span></span> <span data-ttu-id="3c84d-110">Bu dosyaları nereden bulabilirim?</span><span class="sxs-lookup"><span data-stu-id="3c84d-110">Where can I find those files?</span></span>

<span data-ttu-id="3c84d-111">**Y:** tüm Docker dosyaları bulabilirsiniz [GitHub](https://github.com/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="3c84d-111">**A:** You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span></span> <span data-ttu-id="3c84d-112">Tüm Docker kapsayıcıları bulabilirsiniz [Docker hub'a](https://hub.docker.com/u/appsvc/).</span><span class="sxs-lookup"><span data-stu-id="3c84d-112">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span></span>

<span data-ttu-id="3c84d-113">**S:** hello çalışma zamanı yığını yapılandırdığınızda hello beklenen değerler hello başlatma dosyası bölümü için nelerdir?</span><span class="sxs-lookup"><span data-stu-id="3c84d-113">**Q:** What are hello expected values for hello Startup File section when I configure hello runtime stack?</span></span>

<span data-ttu-id="3c84d-114">**Y:** için Node.Js, belirttiğiniz hello PM2 yapılandırma dosyası veya komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="3c84d-114">**A:** For Node.Js, you specify hello PM2 configuration file or your script file.</span></span> <span data-ttu-id="3c84d-115">.NET Core için derlenmiş DLL adınızı belirtin.</span><span class="sxs-lookup"><span data-stu-id="3c84d-115">For .NET Core, specify your compiled DLL name.</span></span> <span data-ttu-id="3c84d-116">Ruby için hello Söyleniş betik belirtebilirsiniz, uygulamanızı tooinitialize istiyor.</span><span class="sxs-lookup"><span data-stu-id="3c84d-116">For Ruby, you can specify hello Ruby script that you want tooinitialize your app with.</span></span>

## <a name="management"></a><span data-ttu-id="3c84d-117">Yönetim</span><span class="sxs-lookup"><span data-stu-id="3c84d-117">Management</span></span>

<span data-ttu-id="3c84d-118">**S:** hello yeniden düğmesine hello Azure portal bastığınızda ne olur?</span><span class="sxs-lookup"><span data-stu-id="3c84d-118">**Q:** What happens when I press hello restart button in hello Azure portal?</span></span>

<span data-ttu-id="3c84d-119">**Y:** bu olduğu hello Docker yeniden karşılığıdır.</span><span class="sxs-lookup"><span data-stu-id="3c84d-119">**A:** This is hello equivalent of Docker restart.</span></span>

<span data-ttu-id="3c84d-120">**S:** güvenli Kabuk (SSH) tooconnect toohello uygulama kapsayıcı sanal makine (VM) kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="3c84d-120">**Q:** Can I use Secure Shell (SSH) tooconnect toohello app container virtual machine (VM)?</span></span>

<span data-ttu-id="3c84d-121">**Y:** Evet, hello SCM sitesi aracılığıyla daha fazla bilgi için onay hello aşağıdaki makalesi yapabileceğiniz [Linux üzerinde Web uygulaması için SSH desteği](./app-service-linux-ssh-support.md)</span><span class="sxs-lookup"><span data-stu-id="3c84d-121">**A:** Yes, you can do that through hello SCM site, check hello following article for more information [SSH support for Web App on Linux](./app-service-linux-ssh-support.md)</span></span>

<span data-ttu-id="3c84d-122">**S:** toocreate Linux uygulama hizmeti düzlemi SDK veya bir ARM şablonu aracılığıyla istediğiniz, nasıl ı elde edebileceğiniz bu?</span><span class="sxs-lookup"><span data-stu-id="3c84d-122">**Q:** I want toocreate a Linux App Service plane through SDK or an ARM template, how can I achieve this?</span></span>

<span data-ttu-id="3c84d-123">**Y:** tooset hello gereksinim `reserved` hello uygulama alanının hizmet çok`true`.</span><span class="sxs-lookup"><span data-stu-id="3c84d-123">**A:** You need tooset hello `reserved` field of hello app service too`true`.</span></span>

## <a name="continuous-integrationdeployment"></a><span data-ttu-id="3c84d-124">Sürekli Tümleştirme/dağıtım</span><span class="sxs-lookup"><span data-stu-id="3c84d-124">Continuous integration/deployment</span></span>

<span data-ttu-id="3c84d-125">**S:** Docker hub'a hello görüntüde güncelleştirilmiş sonra web Uygulamam hala eski Docker kapsayıcısı görüntüyü kullanır.</span><span class="sxs-lookup"><span data-stu-id="3c84d-125">**Q:** My web app still uses an old Docker container image after I've updated hello image on Docker Hub.</span></span> <span data-ttu-id="3c84d-126">Sürekli Tümleştirme/özel kapsayıcılar dağıtımını destekliyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="3c84d-126">Do you support continuous integration/deployment of custom containers?</span></span>

<span data-ttu-id="3c84d-127">**Y:** aşağıdaki makaleye bakın onay hello tarafından Azure kapsayıcı kayıt defteri veya DockerHub görüntü için sürekli tümleştirme/dağıtım tooset [Linux Azure Web uygulaması ile sürekli dağıtımın](./app-service-linux-ci-cd.md).</span><span class="sxs-lookup"><span data-stu-id="3c84d-127">**A:** tooset up continuous integration/deployment for Azure Container Registry or DockerHub images by check hello following article [Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md).</span></span> <span data-ttu-id="3c84d-128">Özel kayıt defterleri için durdurma ve ardından web uygulamanızı başlatma hello kapsayıcı yenileyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3c84d-128">For private registries, you can refresh hello container by stopping and then starting your web app.</span></span> <span data-ttu-id="3c84d-129">Değiştirme veya tooforce, kapsayıcı yenileme ayarlama sahte bir uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3c84d-129">Or you can change or add a dummy application setting tooforce a refresh of your container.</span></span>

<span data-ttu-id="3c84d-130">**S:** hazırlama ortamlarını desteklemek musunuz?</span><span class="sxs-lookup"><span data-stu-id="3c84d-130">**Q:** Do you support staging environments?</span></span>

<span data-ttu-id="3c84d-131">**Y:** Evet.</span><span class="sxs-lookup"><span data-stu-id="3c84d-131">**A:** Yes.</span></span>

<span data-ttu-id="3c84d-132">**S:** kullanabilirim **web dağıtımı** toodeploy web Uygulamam?</span><span class="sxs-lookup"><span data-stu-id="3c84d-132">**Q:** Can I use **web deploy** toodeploy my web app?</span></span>

<span data-ttu-id="3c84d-133">**Y:** tooset denilen bir uygulamaya Evet, ihtiyacınız `WEBSITE_WEBDEPLOY_USE_SCM` çok`false`.</span><span class="sxs-lookup"><span data-stu-id="3c84d-133">**A:** Yes, you need tooset an app setting called `WEBSITE_WEBDEPLOY_USE_SCM` too`false`.</span></span>

## <a name="language-support"></a><span data-ttu-id="3c84d-134">Dil desteği</span><span class="sxs-lookup"><span data-stu-id="3c84d-134">Language support</span></span>

<span data-ttu-id="3c84d-135">**S:** derlenmemiş .NET Core uygulamaları desteği musunuz?</span><span class="sxs-lookup"><span data-stu-id="3c84d-135">**Q:** Do you support uncompiled .NET Core apps?</span></span>

<span data-ttu-id="3c84d-136">**Y:** Evet.</span><span class="sxs-lookup"><span data-stu-id="3c84d-136">**A:** Yes.</span></span>

<span data-ttu-id="3c84d-137">**S:** PHP uygulamaları için bir bağımlılık Yöneticisi olarak Oluşturucu desteklemez?</span><span class="sxs-lookup"><span data-stu-id="3c84d-137">**Q:** Do you support Composer as a dependency manager for PHP apps?</span></span>

<span data-ttu-id="3c84d-138">**Y:** Evet.</span><span class="sxs-lookup"><span data-stu-id="3c84d-138">**A:** Yes.</span></span> <span data-ttu-id="3c84d-139">Git dağıtımı sırasında bir PHP uygulaması (teşekkürler toohello dosyasının varlığı, yönetimin bir composer.json) dağıtma ve sizin için bir oluşturucu yükleme tetikleyecek Kudu tanımalıdır.</span><span class="sxs-lookup"><span data-stu-id="3c84d-139">During a Git deployment, Kudu should detect that you are deploying a PHP application (thanks toohello presence of a composer.json file) and will trigger a composer install for you.</span></span>

## <a name="custom-containers"></a><span data-ttu-id="3c84d-140">Özel kapsayıcılar</span><span class="sxs-lookup"><span data-stu-id="3c84d-140">Custom containers</span></span>

<span data-ttu-id="3c84d-141">**S:** kendi özel kapsayıcı kullanıyorum.</span><span class="sxs-lookup"><span data-stu-id="3c84d-141">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="3c84d-142">Uygulamam hello bulunduğu `\home\` dizin, ancak bulamıyor dosyalarımı ı hello kullanarak hello içerik göz attığınızda [SCM site](https://github.com/projectkudu/kudu) veya bir FTP istemcisi.</span><span class="sxs-lookup"><span data-stu-id="3c84d-142">My app resides in hello `\home\` directory, but I can't find my files when I browse hello content by using hello [SCM site](https://github.com/projectkudu/kudu) or an FTP client.</span></span> <span data-ttu-id="3c84d-143">Dosyalarımı nerede?</span><span class="sxs-lookup"><span data-stu-id="3c84d-143">Where are my files?</span></span>

<span data-ttu-id="3c84d-144">**Y:** biz bir SMB paylaşım toohello bağlama `\home\` dizin.</span><span class="sxs-lookup"><span data-stu-id="3c84d-144">**A:** We mount an SMB share toohello `\home\` directory.</span></span> <span data-ttu-id="3c84d-145">Bu, var olan herhangi bir içerik geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="3c84d-145">This will override any content that's there.</span></span>

<span data-ttu-id="3c84d-146">**S:** kendi özel kapsayıcı kullanıyorum.</span><span class="sxs-lookup"><span data-stu-id="3c84d-146">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="3c84d-147">Merhaba platform toomount bir SMB paylaşım toohello istemiyorum `\home\`.</span><span class="sxs-lookup"><span data-stu-id="3c84d-147">I don't want hello platform toomount an SMB share toohello `\home\`.</span></span>

<span data-ttu-id="3c84d-148">**Y:** bunu ayarı hello tarafından yapabilirsiniz `WEBSITES_ENABLE_APP_SERVICE_STORAGE` uygulama çok ayarı`false`.</span><span class="sxs-lookup"><span data-stu-id="3c84d-148">**A:** You can do that by setting hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting too`false`.</span></span>

<span data-ttu-id="3c84d-149">**S:** uzun süre toostart My özel kapsayıcı alır ve hello platform yeniden hello kapsayıcı kendisinden önce tamamlanır başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="3c84d-149">**Q:** My custom container takes a long time toostart, and hello platform restart hello container before it finishes starting up.</span></span>

<span data-ttu-id="3c84d-150">**Y:** hello platform, kapsayıcı yeniden başlatmadan önce bekleyeceği hello süre yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3c84d-150">**A:** You can configure hello time hello platform will wait before restarting your container.</span></span> <span data-ttu-id="3c84d-151">Bu ayarı hello tarafından yapılabilir `WEBSITES_CONTAINER_START_TIME_LIMIT` uygulama ayarı toohello saniye cinsinden değeri gerekli.</span><span class="sxs-lookup"><span data-stu-id="3c84d-151">This can be done by setting hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting toohello desired value in seconds.</span></span> <span data-ttu-id="3c84d-152">Merhaba varsayılan 230 saniyedir ve hello en fazla 600 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="3c84d-152">hello default is 230 seconds, and hello max is 600 seconds.</span></span>

<span data-ttu-id="3c84d-153">**S:** özel kayıt defteri sunucu URL'si için hello biçimi nedir?</span><span class="sxs-lookup"><span data-stu-id="3c84d-153">**Q:** What is hello format for private registry server url?</span></span>

<span data-ttu-id="3c84d-154">**Y:** tooprovide hello tam kayıt defteri URL'si de dahil olmak üzere ihtiyacınız `http://` veya `https://`.</span><span class="sxs-lookup"><span data-stu-id="3c84d-154">**A:** You need tooprovide hello full registry url including `http://` or `https://`.</span></span>

<span data-ttu-id="3c84d-155">**S:** özel kayıt defteri seçeneğinde hello görüntü adı için hello biçimi nedir?</span><span class="sxs-lookup"><span data-stu-id="3c84d-155">**Q:** What is hello format for hello image name in private registry option?</span></span>

<span data-ttu-id="3c84d-156">**Y:** hello özel kayıt defteri (ör. url dahil olmak üzere tooadd hello tam görüntü adı gerekiyor</span><span class="sxs-lookup"><span data-stu-id="3c84d-156">**A:** You need tooadd hello full image name including hello private registry url (eg.</span></span> <span data-ttu-id="3c84d-157">myacr.azurecr.io/dotnet:Latest)</span><span class="sxs-lookup"><span data-stu-id="3c84d-157">myacr.azurecr.io/dotnet:latest)</span></span>

<span data-ttu-id="3c84d-158">**S:** tooexpose birden fazla bağlantı noktası my özel kapsayıcı görüntüde istiyorum.</span><span class="sxs-lookup"><span data-stu-id="3c84d-158">**Q:** I want tooexpose more than one port on my custom container image.</span></span> <span data-ttu-id="3c84d-159">Bu mümkün mü?</span><span class="sxs-lookup"><span data-stu-id="3c84d-159">Is that possible?</span></span>

<span data-ttu-id="3c84d-160">**Y:** , şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="3c84d-160">**A:** Currently, that isn't supported.</span></span>

<span data-ttu-id="3c84d-161">**S:** kendi depolama kullanıma sunabilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="3c84d-161">**Q:** Can I bring my own storage?</span></span>

<span data-ttu-id="3c84d-162">**Y:** , şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="3c84d-162">**A:** Currently that isn't supported.</span></span>

<span data-ttu-id="3c84d-163">**S:** hello SCM sitesinden my özel kapsayıcının dosya sistemi veya çalışan işlemler öğesine göz atamıyor.</span><span class="sxs-lookup"><span data-stu-id="3c84d-163">**Q:** I can't browse my custom container's file system or running processes from hello SCM site.</span></span> <span data-ttu-id="3c84d-164">Bunun nedeni nedir?</span><span class="sxs-lookup"><span data-stu-id="3c84d-164">Why is that?</span></span>

<span data-ttu-id="3c84d-165">**Y:** hello SCM site ayrı bir kapsayıcıda çalışır.</span><span class="sxs-lookup"><span data-stu-id="3c84d-165">**A:** hello SCM site runs in a separate container.</span></span> <span data-ttu-id="3c84d-166">Merhaba dosya sistemi denetlenemiyor veya çalışan işlemler hello uygulama kapsayıcısının.</span><span class="sxs-lookup"><span data-stu-id="3c84d-166">You can't check hello file system or running processes of hello app container.</span></span>

<span data-ttu-id="3c84d-167">**S:** tooa bağlantı noktası 80 numaralı bağlantı noktası dışındaki My özel kapsayıcı dinler.</span><span class="sxs-lookup"><span data-stu-id="3c84d-167">**Q:** My custom container listens tooa port other than port 80.</span></span> <span data-ttu-id="3c84d-168">Uygulama tooroute hello istekleri toothat Noktam nasıl yapılandırabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="3c84d-168">How can I configure my app tooroute hello requests toothat port?</span></span>

<span data-ttu-id="3c84d-169">**Y:** otomatik bağlantı noktası algılama sahibiz, denilen bir uygulama da belirtebilirsiniz **WEBSITES_PORT**ve beklenen hello bağlantı noktası numarası hello değeri verin.</span><span class="sxs-lookup"><span data-stu-id="3c84d-169">**A:** We have auto port detection, also you can specify an application setting called **WEBSITES_PORT**, and give it hello value of hello expected port number.</span></span> <span data-ttu-id="3c84d-170">Daha önce hello platform tarafından kullanılan `PORT` uygulama ayarı biz toodeprecate hello kullan ayarını bu uygulamayı planlama ve toousing taşıma `WEBSITES_PORT` özel olarak.</span><span class="sxs-lookup"><span data-stu-id="3c84d-170">Previously hello platform was using `PORT` app setting, we are planning toodeprecate hello use this app setting and move toousing `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="3c84d-171">**S:** tooimplement HTTPS my özel kapsayıcısında zorunda.</span><span class="sxs-lookup"><span data-stu-id="3c84d-171">**Q:** Do I need tooimplement HTTPS in my custom container.</span></span>

<span data-ttu-id="3c84d-172">**Y:** Hayır, paylaşılan hello ön uçlar HTTPS sonlandırmanın hello platform işler.</span><span class="sxs-lookup"><span data-stu-id="3c84d-172">**A:** No, hello platform handles HTTPS termination at hello shared frontends.</span></span>

## <a name="pricing-and-sla"></a><span data-ttu-id="3c84d-173">Fiyatlandırma ve SLA</span><span class="sxs-lookup"><span data-stu-id="3c84d-173">Pricing and SLA</span></span>

<span data-ttu-id="3c84d-174">**S:** ne olduğunu hello fiyatlandırma hello genel Önizleme kullanırken?</span><span class="sxs-lookup"><span data-stu-id="3c84d-174">**Q:** What's hello pricing while you're using hello public preview?</span></span>

<span data-ttu-id="3c84d-175">**Y:** hello normal Azure uygulama hizmeti fiyatlandırması ile uygulamanızın çalıştırdığı saat yarım hello sayısını ücretlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3c84d-175">**A:** You are charged half hello number of hours that your app runs, with hello normal Azure App Service pricing.</span></span> <span data-ttu-id="3c84d-176">Bu, normal Azure uygulama hizmeti fiyatlandırması üzerinde bir yüzde 50 indirim almak anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3c84d-176">This means that you get a 50 percent discount on normal Azure App Service pricing.</span></span>

## <a name="other"></a><span data-ttu-id="3c84d-177">Diğer</span><span class="sxs-lookup"><span data-stu-id="3c84d-177">Other</span></span>

<span data-ttu-id="3c84d-178">**S:** hello desteklenen karakter uygulama ayarları adları nelerdir?</span><span class="sxs-lookup"><span data-stu-id="3c84d-178">**Q:** What are hello supported characters in application settings names?</span></span>

<span data-ttu-id="3c84d-179">**Y:** yalnızca, A-Z, a-z, 0-9 kullanın ve alt çizgi uygulama ayarları için hello.</span><span class="sxs-lookup"><span data-stu-id="3c84d-179">**A:** You can only use A-Z, a-z, 0-9, and hello underscore for application settings.</span></span>

<span data-ttu-id="3c84d-180">**S:** burada ı isteyebileceği yeni özellikler?</span><span class="sxs-lookup"><span data-stu-id="3c84d-180">**Q:** Where can I request new features?</span></span>

<span data-ttu-id="3c84d-181">**Y:** ilişkin düşünceniz hello adresindeki gönderebilirsiniz [Web Apps geri bildirim Forumunda](https://aka.ms/webapps-uservoice).</span><span class="sxs-lookup"><span data-stu-id="3c84d-181">**A:** You can submit your idea at hello [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span></span> <span data-ttu-id="3c84d-182">"[Linux]" toohello başlığı, fikir ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3c84d-182">Add "[Linux]" toohello title of your idea.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c84d-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3c84d-183">Next steps</span></span>
* [<span data-ttu-id="3c84d-184">Linux üzerinde Azure Web uygulaması nedir?</span><span class="sxs-lookup"><span data-stu-id="3c84d-184">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="3c84d-185">Linux üzerinde Azure Web uygulaması için SSH desteği</span><span class="sxs-lookup"><span data-stu-id="3c84d-185">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="3c84d-186">Hazırlık Azure App Service ortamları ayarlama</span><span class="sxs-lookup"><span data-stu-id="3c84d-186">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="3c84d-187">Linux üzerinde Azure Web uygulaması ile sürekli dağıtımı</span><span class="sxs-lookup"><span data-stu-id="3c84d-187">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
