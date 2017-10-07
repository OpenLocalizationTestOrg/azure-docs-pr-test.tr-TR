---
title: "aaaIntroduction tooAzure Linux üzerinde Web uygulaması | Microsoft Docs"
description: "Linux üzerinde Azure Web uygulaması hakkında bilgi edinin."
keywords: Azure uygulama hizmeti, linux, oss
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 43b9865ade251909a77429eb3e18fe0bcaac3bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-web-app-on-linux"></a><span data-ttu-id="b2a2b-104">Giriş tooAzure Linux üzerinde Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="b2a2b-104">Introduction tooAzure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="b2a2b-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b2a2b-105">Overview</span></span>
<span data-ttu-id="b2a2b-106">Müşterilerin Web uygulaması için desteklenen uygulama yığınları Linux toohost web uygulamalarını Linux üzerinde yerel olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2a2b-106">Customers can use Web App on Linux toohost web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="b2a2b-107">Merhaba aşağıdaki bölümde şu anda desteklenen hello uygulama yığınları listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="b2a2b-107">hello following section lists hello application stacks that are currently supported.</span></span> 

## <a name="features"></a><span data-ttu-id="b2a2b-108">Özellikler</span><span class="sxs-lookup"><span data-stu-id="b2a2b-108">Features</span></span>
<span data-ttu-id="b2a2b-109">Web uygulaması Linux üzerinde şu anda uygulama yığınları aşağıdaki hello destekler:</span><span class="sxs-lookup"><span data-stu-id="b2a2b-109">Web App on Linux currently supports hello following application stacks:</span></span>

* <span data-ttu-id="b2a2b-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="b2a2b-110">Node.js</span></span>
    * <span data-ttu-id="b2a2b-111">4.4</span><span class="sxs-lookup"><span data-stu-id="b2a2b-111">4.4</span></span>
    * <span data-ttu-id="b2a2b-112">4.5</span><span class="sxs-lookup"><span data-stu-id="b2a2b-112">4.5</span></span>
    * <span data-ttu-id="b2a2b-113">6.2</span><span class="sxs-lookup"><span data-stu-id="b2a2b-113">6.2</span></span>
    * <span data-ttu-id="b2a2b-114">6.6</span><span class="sxs-lookup"><span data-stu-id="b2a2b-114">6.6</span></span>
    * <span data-ttu-id="b2a2b-115">6.9</span><span class="sxs-lookup"><span data-stu-id="b2a2b-115">6.9</span></span>
    * <span data-ttu-id="b2a2b-116">6.10</span><span class="sxs-lookup"><span data-stu-id="b2a2b-116">6.10</span></span>
    * <span data-ttu-id="b2a2b-117">6.11</span><span class="sxs-lookup"><span data-stu-id="b2a2b-117">6.11</span></span>
    * <span data-ttu-id="b2a2b-118">8.0</span><span class="sxs-lookup"><span data-stu-id="b2a2b-118">8.0</span></span>
    * <span data-ttu-id="b2a2b-119">8.1</span><span class="sxs-lookup"><span data-stu-id="b2a2b-119">8.1</span></span>
* <span data-ttu-id="b2a2b-120">PHP</span><span class="sxs-lookup"><span data-stu-id="b2a2b-120">PHP</span></span>
    * <span data-ttu-id="b2a2b-121">5.6</span><span class="sxs-lookup"><span data-stu-id="b2a2b-121">5.6</span></span>
    * <span data-ttu-id="b2a2b-122">7.0</span><span class="sxs-lookup"><span data-stu-id="b2a2b-122">7.0</span></span>
* <span data-ttu-id="b2a2b-123">.NET core</span><span class="sxs-lookup"><span data-stu-id="b2a2b-123">.Net Core</span></span>
    * <span data-ttu-id="b2a2b-124">1.0</span><span class="sxs-lookup"><span data-stu-id="b2a2b-124">1.0</span></span>
    * <span data-ttu-id="b2a2b-125">1.1</span><span class="sxs-lookup"><span data-stu-id="b2a2b-125">1.1</span></span>
* <span data-ttu-id="b2a2b-126">Ruby</span><span class="sxs-lookup"><span data-stu-id="b2a2b-126">Ruby</span></span>
    * <span data-ttu-id="b2a2b-127">2.3</span><span class="sxs-lookup"><span data-stu-id="b2a2b-127">2.3</span></span>

<span data-ttu-id="b2a2b-128">Müşterilerin kendi uygulamalarında kullanarak dağıtabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b2a2b-128">Customers can deploy their applications by using:</span></span>

* <span data-ttu-id="b2a2b-129">FTP</span><span class="sxs-lookup"><span data-stu-id="b2a2b-129">FTP</span></span>
* <span data-ttu-id="b2a2b-130">Yerel Git</span><span class="sxs-lookup"><span data-stu-id="b2a2b-130">Local Git</span></span>
* <span data-ttu-id="b2a2b-131">GitHub</span><span class="sxs-lookup"><span data-stu-id="b2a2b-131">GitHub</span></span>
* <span data-ttu-id="b2a2b-132">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="b2a2b-132">Bitbucket</span></span>

<span data-ttu-id="b2a2b-133">Uygulama ölçeklendirme için:</span><span class="sxs-lookup"><span data-stu-id="b2a2b-133">For application scaling:</span></span>

* <span data-ttu-id="b2a2b-134">Müşterilerin web uygulamaları yukarı ve aşağı App Service planlarına hello katmanını değiştirerek ölçeği</span><span class="sxs-lookup"><span data-stu-id="b2a2b-134">Customers can scale web apps up and down by changing hello tier of their App Service plan</span></span>
* <span data-ttu-id="b2a2b-135">Müşterilerin uygulamalarının ölçekleme ve birden çok uygulama örneğini hello sınırlar içinde kendi SKU çalıştırın</span><span class="sxs-lookup"><span data-stu-id="b2a2b-135">Customers can scale out applications and run multiple app instances within hello confines of their SKU</span></span>

<span data-ttu-id="b2a2b-136">Kudu için bazı hello temel işlevlerini:</span><span class="sxs-lookup"><span data-stu-id="b2a2b-136">For Kudu, some of hello basic functionality:</span></span>

* <span data-ttu-id="b2a2b-137">Ortamlar</span><span class="sxs-lookup"><span data-stu-id="b2a2b-137">Environments</span></span>
* <span data-ttu-id="b2a2b-138">Dağıtımlar</span><span class="sxs-lookup"><span data-stu-id="b2a2b-138">Deployments</span></span>
* <span data-ttu-id="b2a2b-139">Temel konsol</span><span class="sxs-lookup"><span data-stu-id="b2a2b-139">Basic console</span></span>
* <span data-ttu-id="b2a2b-140">SSH</span><span class="sxs-lookup"><span data-stu-id="b2a2b-140">SSH</span></span>

<span data-ttu-id="b2a2b-141">Devops için:</span><span class="sxs-lookup"><span data-stu-id="b2a2b-141">For devops:</span></span>

* <span data-ttu-id="b2a2b-142">Hazırlık ortamları</span><span class="sxs-lookup"><span data-stu-id="b2a2b-142">Staging environments</span></span>
* <span data-ttu-id="b2a2b-143">ACR ve DockerHub CI/CD</span><span class="sxs-lookup"><span data-stu-id="b2a2b-143">ACR and DockerHub CI/CD</span></span>

## <a name="limitations"></a><span data-ttu-id="b2a2b-144">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="b2a2b-144">Limitations</span></span>
<span data-ttu-id="b2a2b-145">Hello Azure portal Linux üzerinde Web uygulaması için şu anda iş yalnızca özelliklerini gösterir ve hello rest gizler.</span><span class="sxs-lookup"><span data-stu-id="b2a2b-145">hello Azure portal shows only features that currently work for Web App on Linux and hides hello rest.</span></span> <span data-ttu-id="b2a2b-146">Daha fazla özellik etkinleştirme gibi hello portalda görünür olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b2a2b-146">As we enable more features, they will be visible on hello portal.</span></span>

<span data-ttu-id="b2a2b-147">Sanal ağ tümleştirmesinin, Azure Active Directory/üçüncü taraf kimlik doğrulama veya Kudu site uzantıları gibi bazı özellikler henüz kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="b2a2b-147">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span></span> <span data-ttu-id="b2a2b-148">Bu özellikler kullanılabilir olduktan sonra bizim belgelerini ve blogu hello değişiklikler hakkında güncelleştireceğiz.</span><span class="sxs-lookup"><span data-stu-id="b2a2b-148">Once these features are available, we will update our documentation and blog about hello changes.</span></span>

<span data-ttu-id="b2a2b-149">Bu genel önizlemesi şu anda yalnızca bölgeleri aşağıdaki hello kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="b2a2b-149">This public preview is currently only available in hello following regions:</span></span>

* <span data-ttu-id="b2a2b-150">Batı ABD</span><span class="sxs-lookup"><span data-stu-id="b2a2b-150">West US</span></span>
* <span data-ttu-id="b2a2b-151">Doğu ABD</span><span class="sxs-lookup"><span data-stu-id="b2a2b-151">East US</span></span>
* <span data-ttu-id="b2a2b-152">Batı Avrupa</span><span class="sxs-lookup"><span data-stu-id="b2a2b-152">West Europe</span></span>
* <span data-ttu-id="b2a2b-153">Kuzey Avrupa</span><span class="sxs-lookup"><span data-stu-id="b2a2b-153">North Europe</span></span>
* <span data-ttu-id="b2a2b-154">Orta Güney ABD</span><span class="sxs-lookup"><span data-stu-id="b2a2b-154">South Central US</span></span>
* <span data-ttu-id="b2a2b-155">Orta Kuzey ABD</span><span class="sxs-lookup"><span data-stu-id="b2a2b-155">North Central US</span></span>
* <span data-ttu-id="b2a2b-156">Güneydoğu Asya</span><span class="sxs-lookup"><span data-stu-id="b2a2b-156">Southeast Asia</span></span>
* <span data-ttu-id="b2a2b-157">Doğu Asya</span><span class="sxs-lookup"><span data-stu-id="b2a2b-157">East Asia</span></span>
* <span data-ttu-id="b2a2b-158">Avustralya Doğu</span><span class="sxs-lookup"><span data-stu-id="b2a2b-158">Australia East</span></span>
* <span data-ttu-id="b2a2b-159">Japonya Doğu</span><span class="sxs-lookup"><span data-stu-id="b2a2b-159">Japan East</span></span>
* <span data-ttu-id="b2a2b-160">Güney Brezilya</span><span class="sxs-lookup"><span data-stu-id="b2a2b-160">Brazil South</span></span>
* <span data-ttu-id="b2a2b-161">Güney Hindistan</span><span class="sxs-lookup"><span data-stu-id="b2a2b-161">South India</span></span>

<span data-ttu-id="b2a2b-162">Web uygulamaları Linux'ta hello ayrılmış uygulama hizmeti planlarında yalnızca desteklenir ve ücretsiz veya paylaşılan bir katmanı yok.</span><span class="sxs-lookup"><span data-stu-id="b2a2b-162">Web Apps on Linux is only supported in hello Dedicated app service plans and does not have a Free or Shared tier.</span></span> <span data-ttu-id="b2a2b-163">Ayrıca, Linux olmayan uygulama hizmeti planında Linux web uygulaması oluşturamıyor normal ve Linux web uygulamaları için uygulama hizmeti planları karşılıklı olarak birbirini dışlar.</span><span class="sxs-lookup"><span data-stu-id="b2a2b-163">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span></span>

<span data-ttu-id="b2a2b-164">Web uygulamaları Linux üzerinde oluşturulan, Linux olmayan web uygulamaları hello içermeyen bir kaynak grubunda aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="b2a2b-164">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in hello same region.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b2a2b-165">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="b2a2b-165">Troubleshooting</span></span> ##

<span data-ttu-id="b2a2b-166">Uygulamanızı toostart başarısız veya uygulamanızdan toocheck hello günlük istediğiniz, Docker hello LogFiles dizinde oturum hello denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b2a2b-166">When your application fails toostart or you want toocheck hello logging from your app, check hello Docker logs in hello LogFiles directory.</span></span> <span data-ttu-id="b2a2b-167">SCM siteniz veya FTP aracılığıyla bu dizine erişebilir.</span><span class="sxs-lookup"><span data-stu-id="b2a2b-167">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="b2a2b-168">toolog hello `stdout` ve `stderr` tooenable gerekir, kapsayıcıdan **Docker kapsayıcısı günlük** altında **tanılama günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="b2a2b-168">toolog hello `stdout` and `stderr` from your container, you need tooenable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Günlüğü etkinleştirme][2]

![Kudu tooview Docker günlüklerini kullanma][1]

<span data-ttu-id="b2a2b-171">Merhaba SCM sitesinden erişebilirsiniz **Gelişmiş Araçlar** hello içinde **geliştirme araçları** menüsü.</span><span class="sxs-lookup"><span data-stu-id="b2a2b-171">You can access hello SCM site from **Advanced Tools** in hello **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2a2b-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b2a2b-172">Next steps</span></span>
<span data-ttu-id="b2a2b-173">Uygulama hizmeti Linux'ta kullanmaya bağlantılar tooget aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="b2a2b-173">See hello following links tooget started with App Service on Linux.</span></span> <span data-ttu-id="b2a2b-174">Hakkında sorular ve sorunları nakledebilirsiniz [forumumuzda](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="b2a2b-174">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="b2a2b-175">Linux üzerinde Azure Web uygulaması için nasıl toouse özel Docker görüntü</span><span class="sxs-lookup"><span data-stu-id="b2a2b-175">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="b2a2b-176">Linux üzerinde Azure Web uygulamasında Node.js için PM2 Yapılandırması'nı kullanarak</span><span class="sxs-lookup"><span data-stu-id="b2a2b-176">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="b2a2b-177">.NET Core Linux Azure App Service Web uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="b2a2b-177">Using .NET Core in Azure App Service Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="b2a2b-178">Azure App Service Web uygulaması Linux'ta Ruby kullanma</span><span class="sxs-lookup"><span data-stu-id="b2a2b-178">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="b2a2b-179">Azure App Service Web uygulaması Linux SSS</span><span class="sxs-lookup"><span data-stu-id="b2a2b-179">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="b2a2b-180">Linux üzerinde Azure Web uygulaması için SSH desteği</span><span class="sxs-lookup"><span data-stu-id="b2a2b-180">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="b2a2b-181">Hazırlık Azure App Service ortamları ayarlama</span><span class="sxs-lookup"><span data-stu-id="b2a2b-181">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="b2a2b-182">Docker hub'a sürekli dağıtım Linux Azure Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="b2a2b-182">Docker Hub Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png