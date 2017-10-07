---
title: "(Azure App Service'te test beta) aaaFlighting dağıtımı"
description: "Uygulama veya beta tooflight yeni özellikler, güncelleştirmeleri bu uçtan uca öğretici test nasıl öğrenin. Ayrıca sürekli yayımlama, yuvaları, trafik yönlendirme ve Application Insights tümleştirme gibi uygulama hizmeti özellikleri araya getirir."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 17953c51-38f8-442d-bb0b-f69c1542f0e9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cephalin
ms.openlocfilehash: e83477b1fe46be09e5baa7bc2bd239b840b05cf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a><span data-ttu-id="85835-104">(Azure App Service'te test beta) flighting dağıtımı</span><span class="sxs-lookup"><span data-stu-id="85835-104">Flighting deployment (beta testing) in Azure App Service</span></span>
<span data-ttu-id="85835-105">Bu öğretici şunların nasıl yapıldığını gösterir toodo *flighting dağıtımları* tümleştirerek çeşitli özelliklerini hello [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) ve [Azure Application Insights](/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="85835-105">This tutorial shows you how toodo *flighting deployments* by integrating hello various capabilities of [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure Application Insights](/services/application-insights/).</span></span>

<span data-ttu-id="85835-106">*Flighting* bir yeni özellik veya sınırlı sayıda gerçek müşteri değişiklikle doğrulayan bir dağıtım işlemidir ve ana üretim senaryosunda test etmektir.</span><span class="sxs-lookup"><span data-stu-id="85835-106">*Flighting* is a deployment process that validates a new feature or change with a limited number of real customers, and is a major testing in production scenario.</span></span> <span data-ttu-id="85835-107">Akin toobeta olan sınama ve bazen "denetimli test uçuş" bilinir.</span><span class="sxs-lookup"><span data-stu-id="85835-107">It is akin toobeta testing and is sometimes known as "controlled test flight".</span></span> <span data-ttu-id="85835-108">Bir web varlığı çok büyük ölçekli işletmeler için erken doğrulama bunların bir uygulamada kendi uygulama güncelleştirmelerini almak üzere bu yaklaşımı kullanın [Çevik Geliştirme](https://en.wikipedia.org/wiki/Agile_software_development).</span><span class="sxs-lookup"><span data-stu-id="85835-108">Many large enterprises with a web presence use this approach to get early validation on their app updates in their practice of [agile development](https://en.wikipedia.org/wiki/Agile_software_development).</span></span> <span data-ttu-id="85835-109">Application Insights tooimplement hello aynı DevOps senaryo ve Azure uygulama hizmeti sürekli yayımlama ile üretimde toointegrate test sağlar.</span><span class="sxs-lookup"><span data-stu-id="85835-109">Azure App Service enables you toointegrate test in production with continous publishing and Application Insights tooimplement hello same DevOps scenario.</span></span> <span data-ttu-id="85835-110">Bu yaklaşımın avantajları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="85835-110">Benefits of this approach include:</span></span>

* <span data-ttu-id="85835-111">**Gerçek geri bildirim sağlamak *önce* güncelleştirmelerin yayımlanan tooproduction** -bırakmadan önce yayın hemen sonra geri bildirim sağlamasını daha iyi bir şey geribildirim sağlamasını yalnızca hello.</span><span class="sxs-lookup"><span data-stu-id="85835-111">**Gain real feedback *before* updates are released tooproduction** - hello only thing better than gaining feedback as soon as you release is gaining feedback before you release.</span></span> <span data-ttu-id="85835-112">Gerçek kullanıcı trafiği ve davranışları güncelleştirmeleriyle hello ürün yaşam döngüsünde işlemleriniz olabildiğince erken test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85835-112">You can test updates with real user traffic and behaviors as early as you desire in hello product life cycle.</span></span>
* <span data-ttu-id="85835-113">**Geliştirmek [sürekli teste dayalı geliştirme (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)**  - kullanıcı doğrulama ürün yaşam döngüsünde erken ve otomatik olarak gerçekleşir üretim aşamasındaki bir test sürekli tümleştirme ve Application Insights ile araçları ile tümleştirme.</span><span class="sxs-lookup"><span data-stu-id="85835-113">**Enhance [continuous test-driven development (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)** - By integrating test in production with continuous integration and instrumentation with Application Insights, user validation happens early and automatically in your product life cycle.</span></span> <span data-ttu-id="85835-114">Bu, el ile test yürütme zamanı yatırım azaltılmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="85835-114">This helps reduce time investments in manual test execution.</span></span>
* <span data-ttu-id="85835-115">**Test iş akışı en iyi duruma getirme** -sürekli izleme araçları ile üretim aşamasındaki bir test otomatik hale getirerek, potansiyel olarak tek bir işlem testlerinde çeşitli hello amaçları gibi gerçekleştirebilirsiniz [tümleştirme](https://en.wikipedia.org/wiki/Integration_testing), [regresyon](https://en.wikipedia.org/wiki/Regression_testing), [kullanılabilirlik](https://en.wikipedia.org/wiki/Usability_testing), erişilebilirlik, yerelleştirme, [performans](https://en.wikipedia.org/wiki/Software_performance_testing), [güvenlik](https://en.wikipedia.org/wiki/Security_testing), ve [ kabul](https://en.wikipedia.org/wiki/Acceptance_testing).</span><span class="sxs-lookup"><span data-stu-id="85835-115">**Optimize test workflow** - By automating test in production with continuous monitoring instrumentation, you can potentially accomplish hello goals of various kinds of tests in a single process, such as [integration](https://en.wikipedia.org/wiki/Integration_testing), [regression](https://en.wikipedia.org/wiki/Regression_testing), [usability](https://en.wikipedia.org/wiki/Usability_testing), accessibility, localization, [performance](https://en.wikipedia.org/wiki/Software_performance_testing), [security](https://en.wikipedia.org/wiki/Security_testing), and [acceptance](https://en.wikipedia.org/wiki/Acceptance_testing).</span></span>

<span data-ttu-id="85835-116">Flighting dağıtım neredeyse dinamik trafik yönlendirme değil.</span><span class="sxs-lookup"><span data-stu-id="85835-116">A flighting deployment is not just about routing live traffic.</span></span> <span data-ttu-id="85835-117">Böyle bir dağıtımda toogain Insight mümkün olan en kısa sürede olması gerekmediğini beklenmeyen bir hata, bir performans düşüşü, kullanıcı deneyimi sorunları istiyor.</span><span class="sxs-lookup"><span data-stu-id="85835-117">In such a deployment you want toogain insight as quickly as possible, whether it be an unexpected bug, performance degradation, user experience issues.</span></span> <span data-ttu-id="85835-118">Gerçek müşterilerle çalışıyorsanız unutmayın.</span><span class="sxs-lookup"><span data-stu-id="85835-118">Remember, you are dealing with real customers.</span></span> <span data-ttu-id="85835-119">Bunu toodo, sağ, içinde toomake bilinçli bir karar sonraki adımınız için sipariş tüm hello veri flighting, dağıtım toogather ayarladığınızdan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="85835-119">So toodo it right, you must make sure that you have set up your flighting deployment toogather all hello data you need in order toomake an informed decision for your next step.</span></span> <span data-ttu-id="85835-120">Bu öğreticide gösterilmiştir nasıl toocollect verilerin Application Insights, ancak New Relic veya kullanabilirler senaryonuza uygun diğer teknolojiler.</span><span class="sxs-lookup"><span data-stu-id="85835-120">This tutorial shows you how toocollect data with Application Insights, but you can use New Relic or other technologies that suits your scenario.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="85835-121">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="85835-121">What you will do</span></span>
<span data-ttu-id="85835-122">Bu öğreticide şunları öğreneceksiniz nasıl toobring senaryoları birlikte tootest uygulama hizmeti uygulamanızı üretim hello:</span><span class="sxs-lookup"><span data-stu-id="85835-122">In this tutorial, you will learn how toobring hello following scenarios together tootest your App Service app in production:</span></span>

* <span data-ttu-id="85835-123">[Üretim trafiği yönlendirmek](app-service-web-test-in-production-get-start.md) tooyour beta uygulama</span><span class="sxs-lookup"><span data-stu-id="85835-123">[Route production traffic](app-service-web-test-in-production-get-start.md) tooyour beta app</span></span>
* <span data-ttu-id="85835-124">[Uygulamanızı izleme](../application-insights/app-insights-web-track-usage.md) tooobtain yararlı ölçümler</span><span class="sxs-lookup"><span data-stu-id="85835-124">[Instrument your app](../application-insights/app-insights-web-track-usage.md) tooobtain useful metrics</span></span>
* <span data-ttu-id="85835-125">Sürekli olarak beta uygulamanızı dağıtma ve dinamik uygulama ölçümleri izleme</span><span class="sxs-lookup"><span data-stu-id="85835-125">Continuously deploy your beta app and track live app metrics</span></span>
* <span data-ttu-id="85835-126">Merhaba üretim uygulama ve kod nasıl değiştiğini hello beta uygulama toosee arasında karşılaştırma ölçümleri tooresults Çevir</span><span class="sxs-lookup"><span data-stu-id="85835-126">Compare metrics between hello production app and hello beta app toosee how code changes translate tooresults</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="85835-127">İhtiyacınız olacak</span><span class="sxs-lookup"><span data-stu-id="85835-127">What you will need</span></span>
* <span data-ttu-id="85835-128">Bir Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="85835-128">An Azure account</span></span>
* <span data-ttu-id="85835-129">A [GitHub](https://github.com/) hesabı</span><span class="sxs-lookup"><span data-stu-id="85835-129">A [GitHub](https://github.com/) account</span></span>
* <span data-ttu-id="85835-130">Visual Studio 2015 - hello yükleyebilir [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="85835-130">Visual Studio 2015 - you can download hello [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).</span></span>
* <span data-ttu-id="85835-131">Git Kabuğu (yüklenmiş [Windows için GitHub](https://windows.github.com/))-Bu, toorun hello hem hello Git ve PowerShell komutları sağlar aynı oturum</span><span class="sxs-lookup"><span data-stu-id="85835-131">Git Shell (installed with [GitHub for Windows](https://windows.github.com/)) - this enables you toorun both hello Git and PowerShell commands in hello same session</span></span>
* <span data-ttu-id="85835-132">En son [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) BITS</span><span class="sxs-lookup"><span data-stu-id="85835-132">Latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) bits</span></span>
* <span data-ttu-id="85835-133">Merhaba aşağıdaki temel anlama:</span><span class="sxs-lookup"><span data-stu-id="85835-133">Basic understanding of hello following:</span></span>
  * <span data-ttu-id="85835-134">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) şablon dağıtımı (bkz [beklendiği azure'da karmaşık bir uygulama dağıtmak](app-service-deploy-complex-application-predictably.md))</span><span class="sxs-lookup"><span data-stu-id="85835-134">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) template deployment (see [Deploy a complex application predictably in Azure](app-service-deploy-complex-application-predictably.md))</span></span>
  * [<span data-ttu-id="85835-135">Git</span><span class="sxs-lookup"><span data-stu-id="85835-135">Git</span></span>](http://git-scm.com/documentation)
  * [<span data-ttu-id="85835-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="85835-136">PowerShell</span></span>](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> <span data-ttu-id="85835-137">Bu öğretici bir Azure hesabı toocomplete gerekir:</span><span class="sxs-lookup"><span data-stu-id="85835-137">You need an Azure account toocomplete this tutorial:</span></span>
>
> * <span data-ttu-id="85835-138">Yapabilecekleriniz [ücretsiz bir Azure hesabı açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/) -krediler alırsınız Ücretli Azure hizmetlerini tootry çıkışı kullanabilirsiniz ve hatta kullanıldıktan sonra hello hesabı tutabilir ve ücretsiz Web uygulamaları gibi Azure hizmetlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85835-138">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use tootry out paid Azure services, and even after they're used up you can keep hello account and use free Azure services, such as Web Apps.</span></span>
> * <span data-ttu-id="85835-139">Yapabilecekleriniz [Visual Studio abone Avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -bilgisayarınızı Visual Studio abonelik size kredi verir Ücretli Azure hizmetlerinizi kullanabildiğiniz her ay.</span><span class="sxs-lookup"><span data-stu-id="85835-139">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="85835-140">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85835-140">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="85835-141">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="85835-141">No credit cards required; no commitments.</span></span>
>
>

## <a name="set-up-your-production-web-app"></a><span data-ttu-id="85835-142">Üretim web uygulamanızı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="85835-142">Set up your production web app</span></span>
> [!NOTE]
> <span data-ttu-id="85835-143">Bu öğreticide kullanılan hello betik GitHub havuzunuzdan sürekli yayımlama otomatik olarak yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="85835-143">hello script used in this tutorial will automatically configure continuous publishing from your GitHub repository.</span></span> <span data-ttu-id="85835-144">Bu gerektirir GitHub kimlik bilgilerinizi zaten Azure'da depolanır, aksi takdirde komut dosyasıyla hello dağıtım tooconfigure kaynak denetim ayarları hello web uygulamaları için çalışırken başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="85835-144">This requires that your GitHub credentials are already stored in Azure, otherwise hello scripted deployment will fail when attempting tooconfigure source control settings for hello web apps.</span></span>
>
> <span data-ttu-id="85835-145">toostore, GitHub kimlik bilgileri, Azure'da hello bir web uygulaması oluşturma [Azure Portal](https://portal.azure.com/) ve [GitHub dağıtımını yapılandırma](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="85835-145">toostore your GitHub credentials in Azure, create a web app in hello [Azure Portal](https://portal.azure.com/) and [configure GitHub deployment](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="85835-146">Toodo yalnızca bu kez gerekir.</span><span class="sxs-lookup"><span data-stu-id="85835-146">You only need toodo this once.</span></span>
>
>

<span data-ttu-id="85835-147">Tipik bir DevOps senaryo azure'da çalışan bir uygulamanız varsa ve sürekli yayımı üzerinden toomake değişiklikleri tooit istiyor.</span><span class="sxs-lookup"><span data-stu-id="85835-147">In a typical DevOps scenario, you have an application that’s running live in Azure, and you want toomake changes tooit through continuous publishing.</span></span> <span data-ttu-id="85835-148">Bu senaryoda, tooproduction geliştirilen ve sınanmış bir şablon dağıtır.</span><span class="sxs-lookup"><span data-stu-id="85835-148">In this scenario, you will deploy tooproduction a template that you have developed and tested.</span></span>

1. <span data-ttu-id="85835-149">Merhaba, kendi çatalı oluşturma [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) deposu.</span><span class="sxs-lookup"><span data-stu-id="85835-149">Create your own fork of hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repository.</span></span> <span data-ttu-id="85835-150">Çatalı oluşturma hakkında daha fazla bilgi için bkz: [bir depoyu Çatallaştırma](https://help.github.com/articles/fork-a-repo/).</span><span class="sxs-lookup"><span data-stu-id="85835-150">For information on creating your fork, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/).</span></span> <span data-ttu-id="85835-151">Çatalı oluşturulduktan sonra tarayıcınızı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85835-151">Once your fork is created, you can see it in your browser.</span></span>

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. <span data-ttu-id="85835-152">Git kabuk oturumu açın.</span><span class="sxs-lookup"><span data-stu-id="85835-152">Open a Git Shell session.</span></span> <span data-ttu-id="85835-153">Git Kabuk henüz yoksa, yükleme [Windows için GitHub](https://windows.github.com/) şimdi.</span><span class="sxs-lookup"><span data-stu-id="85835-153">If you don't have Git Shell yet, install [GitHub for Windows](https://windows.github.com/) now.</span></span>
3. <span data-ttu-id="85835-154">Merhaba aşağıdaki komutu çalıştırarak, çatalı yerel bir kopyasını oluşturun:</span><span class="sxs-lookup"><span data-stu-id="85835-154">Create a local clone of your fork by executing hello following command:</span></span>

     <span data-ttu-id="85835-155">Git kopya https://github.com/<your_fork>/ToDoApp.git</span><span class="sxs-lookup"><span data-stu-id="85835-155">git clone https://github.com/<your_fork>/ToDoApp.git</span></span>
4. <span data-ttu-id="85835-156">Yerel kopya sahip olduğunda, çok gidin*&lt;repository_root >*\ARMTemplates ve çalışma hello deploy.ps1 aşağıdaki komut dosyası gösterildiği gibi benzersiz bir son eke sahip:</span><span class="sxs-lookup"><span data-stu-id="85835-156">Once you have your local clone, navigate too*&lt;repository_root>*\ARMTemplates, and run hello deploy.ps1 script with a unique suffix, as shown below:</span></span>

     <span data-ttu-id="85835-157">.\deploy.ps1 – RepoUrl https://github.com/<your_fork>/todoapp.git - ResourceGroupSuffix < your_suffix ></span><span class="sxs-lookup"><span data-stu-id="85835-157">.\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git -ResourceGroupSuffix <your_suffix></span></span>
5. <span data-ttu-id="85835-158">İstendiğinde, istenen hello kullanıcı adı ve veritabanı erişimi için parola yazın.</span><span class="sxs-lookup"><span data-stu-id="85835-158">When prompted, type in hello desired username and password for database access.</span></span> <span data-ttu-id="85835-159">Veritabanınızı toospecify gerekir çünkü kimlik bilgilerini Hatırla onları yeniden zaman güncelleştirme hello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="85835-159">Remember your database credentials because you will need toospecify them again when updating hello resource group.</span></span>

   <span data-ttu-id="85835-160">Çeşitli Azure kaynaklarını ilerlemesini sağlama hello görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="85835-160">You should see hello provisioning progress of various Azure resources.</span></span> <span data-ttu-id="85835-161">Dağıtım tamamlandığında hello betik hello tarayıcıda hello uygulamasını başlatın ve kolay bip sesi verin.</span><span class="sxs-lookup"><span data-stu-id="85835-161">When deployment completes, hello script will launch hello application in hello browser and give you a friendly beep.</span></span>
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. <span data-ttu-id="85835-162">Geri Git Kabuk oturumunuzda çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="85835-162">Back in your Git Shell session, run:</span></span>

     <span data-ttu-id="85835-163">. \swap – adı ToDoApp < your_suffix ></span><span class="sxs-lookup"><span data-stu-id="85835-163">.\swap –Name ToDoApp<your_suffix></span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. <span data-ttu-id="85835-164">Merhaba betik tamamlandığında toobrowse toohello frontend'ın adresi geri dönün (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) üretimde çalışan toosee Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="85835-164">When hello script finishes, go back toobrowse toohello frontend’s address (http://ToDoApp*&lt;your_suffix>*.azurewebsites.net/) toosee hello application running in production.</span></span>
8. <span data-ttu-id="85835-165">Merhaba günlüğüne [Azure Portal](https://portal.azure.com/) ve ne oluşturulan bir göz atalım.</span><span class="sxs-lookup"><span data-stu-id="85835-165">Log into hello [Azure Portal](https://portal.azure.com/) and take a look at what’s created.</span></span>

   <span data-ttu-id="85835-166">Merhaba mümkün toosee iki web uygulamalarında olmalıdır aynı kaynak grubu, hello biriyle `Api` hello adı soneki.</span><span class="sxs-lookup"><span data-stu-id="85835-166">You should be able toosee two web apps in hello same resource group, one with hello `Api` suffix in hello name.</span></span> <span data-ttu-id="85835-167">Merhaba kaynak grubu görünümü bakarsanız, hello SQL veritabanı ve sunucu, hello uygulama hizmeti planı ve hello web uygulamaları için hazırlama yuvası hello görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="85835-167">If you look at hello resource group view, you will also see hello SQL Database and server, hello App Service plan, and hello staging slots for hello web apps.</span></span> <span data-ttu-id="85835-168">Üzerinden Hello farklı kaynaklara göz atın ve bunlarla karşılaştırmak  *&lt;repository_root >*yapılandırmaya hello şablonunda \ARMTemplates\ProdAndStage.json toosee.</span><span class="sxs-lookup"><span data-stu-id="85835-168">Browse through hello different resources and compare them with *&lt;repository_root>*\ARMTemplates\ProdAndStage.json toosee how they are configured in hello template.</span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

<span data-ttu-id="85835-169">Merhaba üretim uygulamasını ayarladınız.</span><span class="sxs-lookup"><span data-stu-id="85835-169">You have set up hello production app.</span></span>  <span data-ttu-id="85835-170">Şimdi, şimdi hello uygulaması için kullanılabilirlik zayıftır geri bildirim alma düşünün.</span><span class="sxs-lookup"><span data-stu-id="85835-170">Now, let's imagine that you receive feedback that usability is poor for hello app.</span></span> <span data-ttu-id="85835-171">Bu nedenle tooinvestigate karar verin.</span><span class="sxs-lookup"><span data-stu-id="85835-171">So you decide tooinvestigate.</span></span> <span data-ttu-id="85835-172">Uygulama toogive tooinstrument oluşturacağız, geri bildirim.</span><span class="sxs-lookup"><span data-stu-id="85835-172">You're going tooinstrument your app toogive you feedback.</span></span>

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a><span data-ttu-id="85835-173">Araştırın: izleme izleme ölçümünün istemci uygulamanızı</span><span class="sxs-lookup"><span data-stu-id="85835-173">Investigate: Instrument your client app for monitoring/metrics</span></span>
1. <span data-ttu-id="85835-174">Açık  *&lt;repository_root >*\src\MultiChannelToDo.sln Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="85835-174">Open *&lt;repository_root>*\src\MultiChannelToDo.sln in Visual Studio.</span></span>
2. <span data-ttu-id="85835-175">Çözüm sağ tıklayarak tüm Nuget paketlerini geri yüklemek > **çözüm için NuGet paketlerini Yönet** > **geri**.</span><span class="sxs-lookup"><span data-stu-id="85835-175">Restore all Nuget packages by right-clicking solution > **Manage NuGet Packages for Solution** > **Restore**.</span></span>
3. <span data-ttu-id="85835-176">Sağ **MultiChannelToDo.Web** > **Application Insights Telemetrisi Ekle** > **ayarlarını yapılandır** > kaynak grubu Değiştir tooToDoApp*&lt;your_suffix >* > **Application Insights Ekle tooProject**.</span><span class="sxs-lookup"><span data-stu-id="85835-176">Right-click **MultiChannelToDo.Web** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group tooToDoApp*&lt;your_suffix>* > **Add Application Insights tooProject**.</span></span>
4. <span data-ttu-id="85835-177">Hello Azure Portal, hello hello dikey penceresini açmak **MultiChannelToDo.Web** uygulama Insight kaynak.</span><span class="sxs-lookup"><span data-stu-id="85835-177">In hello Azure Portal, open hello blade for hello **MultiChannelToDo.Web** Application Insight resource.</span></span> <span data-ttu-id="85835-178">Merhaba sonra **uygulama sistem** kısım, tıklatın **nasıl toocollect tarayıcı sayfası veri yükleme öğrenin** > kodu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="85835-178">Then in hello **Application health** part, click **Learn how toocollect browser page load data** > copy code.</span></span>
5. <span data-ttu-id="85835-179">Merhaba kopyalanan JS araçları kodu çok eklemek*&lt;repository_root >*hello kapatmadan önce yalnızca \src\MultiChannelToDo.Web\app\Index.cshtml `<heading>` etiketi.</span><span class="sxs-lookup"><span data-stu-id="85835-179">Add hello copied JS instrumentation code too*&lt;repository_root>*\src\MultiChannelToDo.Web\app\Index.cshtml, just before hello closing `<heading>` tag.</span></span> <span data-ttu-id="85835-180">Uygulama Insight kaynağınız hello benzersiz izleme anahtarını içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="85835-180">It should contain hello unique instrumentation key of your Application Insight resource.</span></span>

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. <span data-ttu-id="85835-181">Özel olaylar, gövde kod toohello altına aşağıdaki hello ekleyerek fare tıklamaları için tooApplication Insights gönder:</span><span class="sxs-lookup"><span data-stu-id="85835-181">Send custom events tooApplication Insights for mouse clicks by adding hello following code toohello bottom of body:</span></span>

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   <span data-ttu-id="85835-182">Bir kullanıcı herhangi bir yere hello web uygulamasında, her zaman bu JavaScript kod parçacığı Öngörüler özel olay tooApplication gönderir.</span><span class="sxs-lookup"><span data-stu-id="85835-182">This JavaScript snippet sends a custom event tooApplication Insights every time a user clicks anywhere in hello web app.</span></span>
7. <span data-ttu-id="85835-183">Git Kabuğu'nda yürütme ve değişiklikleri tooyour çatalı Github'da gönderme.</span><span class="sxs-lookup"><span data-stu-id="85835-183">In Git Shell, commit and push your changes tooyour fork in GitHub.</span></span> <span data-ttu-id="85835-184">Daha sonra istemcileri toorefresh tarayıcı için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="85835-184">Then, wait for clients toorefresh browser.</span></span>

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. <span data-ttu-id="85835-185">Dağıtılan hello uygulama değişiklikleri tooproduction değiştirme:</span><span class="sxs-lookup"><span data-stu-id="85835-185">Swap hello deployed app changes tooproduction:</span></span>

     <span data-ttu-id="85835-186">. \swap – adı ToDoApp < your_suffix ></span><span class="sxs-lookup"><span data-stu-id="85835-186">.\swap –Name ToDoApp<your_suffix></span></span>
9. <span data-ttu-id="85835-187">Yapılandırdığınız toohello Application Insights kaynağı göz atın.</span><span class="sxs-lookup"><span data-stu-id="85835-187">Browse toohello Application Insights resource that you configured.</span></span> <span data-ttu-id="85835-188">Özel olaylar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="85835-188">Click Custom events.</span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   <span data-ttu-id="85835-189">Özel olaylar için ölçümleri görmüyorsanız, birkaç dakika bekleyin ve tıklayın **yenileme**.</span><span class="sxs-lookup"><span data-stu-id="85835-189">If you don't see metrics for custom events, wait a few minutes and click **Refresh**.</span></span>

<span data-ttu-id="85835-190">Bir grafik gördüğünüz varsayalım ister altında:</span><span class="sxs-lookup"><span data-stu-id="85835-190">Suppose you see a chart like below:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

<span data-ttu-id="85835-191">Ve olay kılavuz altındaki hello:</span><span class="sxs-lookup"><span data-stu-id="85835-191">And hello event grid below it:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

<span data-ttu-id="85835-192">Tooyour ToDoApp uygulama koduna göre hello **düğmesini** olay karşılık gelen toohello Gönder düğmesi ve hello **giriş** olay toohello textbox karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="85835-192">According tooyour ToDoApp application code, hello **BUTTON** event corresponds toohello submit button, and hello **INPUT** event corresponds toohello textbox.</span></span> <span data-ttu-id="85835-193">Şu ana kadar şeyler anlamlıdır.</span><span class="sxs-lookup"><span data-stu-id="85835-193">So far, things make sense.</span></span> <span data-ttu-id="85835-194">Ancak, iyi miktarını tıklar ve çok az tıklama hello yapılacak işler öğelerinde gibi görünür (Merhaba **LI** olayları).</span><span class="sxs-lookup"><span data-stu-id="85835-194">However, it looks like there's a good amount of clicks and very few clicks on hello to-do items (hello **LI** events).</span></span>

<span data-ttu-id="85835-195">Bazı kullanıcılar, varsayımınızın hello hangi kısmına UI tıklanabilir ve hello liste öğelerini ve simgelerine geldiğinde hello imleç için metin seçimi stilde çünkü kafası bu formda, size temel.</span><span class="sxs-lookup"><span data-stu-id="85835-195">Based on this, you form your hypothesis that some users are confused which part of hello UI is clickable and it is because hello cursor is styled for text selection when it hovers on hello list items and their icons.</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

<span data-ttu-id="85835-196">Bu contrived bir örnek olabilir.</span><span class="sxs-lookup"><span data-stu-id="85835-196">This might be a contrived example.</span></span> <span data-ttu-id="85835-197">Bununla birlikte, devam eden toomake geliştirme tooyour uygulama olduğunuz ve flighting bir dağıtım tooget kullanılabilirlik geri bildirim Canlı müşterilerden gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="85835-197">Nevertheless, you're going toomake an improvement tooyour app, and then perform a flighting deployment tooget usability feedback from live customers.</span></span>

### <a name="instrument-your-server-app-for-monitoringmetrics"></a><span data-ttu-id="85835-198">Sunucu uygulamanız için izleme ölçümleri izleme</span><span class="sxs-lookup"><span data-stu-id="85835-198">Instrument your server app for monitoring/metrics</span></span>
<span data-ttu-id="85835-199">Bu öğreticide gösterilen hello senaryo yalnızca hello istemci uygulaması ile ilgilenir bu yana bir tanjantını budur.</span><span class="sxs-lookup"><span data-stu-id="85835-199">This is a tangent since hello scenario demonstrated in this tutorial only deals with hello client app.</span></span> <span data-ttu-id="85835-200">Ancak, bütünlük açısından hello sunucu tarafı uygulama ayarlama.</span><span class="sxs-lookup"><span data-stu-id="85835-200">However, for completeness you will set up hello server-side app.</span></span>

1. <span data-ttu-id="85835-201">Sağ **MultiChannelToDo** > **Application Insights Telemetrisi Ekle** > **ayarlarını yapılandır** > kaynak grubu Değiştir tooToDoApp*&lt;your_suffix >* > **Application Insights Ekle tooProject**.</span><span class="sxs-lookup"><span data-stu-id="85835-201">Right-click **MultiChannelToDo** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group tooToDoApp*&lt;your_suffix>* > **Add Application Insights tooProject**.</span></span>
2. <span data-ttu-id="85835-202">Git Kabuğu'nda yürütme ve değişiklikleri tooyour çatalı Github'da gönderme.</span><span class="sxs-lookup"><span data-stu-id="85835-202">In Git Shell, commit and push your changes tooyour fork in GitHub.</span></span> <span data-ttu-id="85835-203">Daha sonra istemcileri toorefresh tarayıcı için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="85835-203">Then, wait for clients toorefresh browser.</span></span>

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. <span data-ttu-id="85835-204">Dağıtılan hello uygulama değişiklikleri tooproduction değiştirme:</span><span class="sxs-lookup"><span data-stu-id="85835-204">Swap hello deployed app changes tooproduction:</span></span>

     <span data-ttu-id="85835-205">. \swap – adı ToDoApp < your_suffix ></span><span class="sxs-lookup"><span data-stu-id="85835-205">.\swap –Name ToDoApp<your_suffix></span></span>

<span data-ttu-id="85835-206">İşte bu kadar!</span><span class="sxs-lookup"><span data-stu-id="85835-206">That's it!</span></span>

## <a name="investigate-add-slot-specific-tags-tooyour-client-app-metrics"></a><span data-ttu-id="85835-207">Araştır: yuvası özgü etiketler tooyour istemci uygulaması ölçüm Ekle</span><span class="sxs-lookup"><span data-stu-id="85835-207">Investigate: Add slot-specific tags tooyour client app metrics</span></span>
<span data-ttu-id="85835-208">Bu bölümde, hello farklı dağıtım yuvası toosend yuva özel telemetri toohello yapılandıracak aynı Application Insights kaynağı.</span><span class="sxs-lookup"><span data-stu-id="85835-208">In this section, you will configure hello different deployment slots toosend slot-specific telemetry toohello same Application Insights resource.</span></span> <span data-ttu-id="85835-209">Bu şekilde telemetri karşılaştırabilirsiniz farklı yuvaları (dağıtım ortamlarda) tooeasily gelen trafiği arasında veri uygulama değişikliklerinizi hello etkisini bakın.</span><span class="sxs-lookup"><span data-stu-id="85835-209">This way, you can compare telemetry data between traffic from different slots (deployment environments) tooeasily see hello effect of your app changes.</span></span> <span data-ttu-id="85835-210">AT hello aynı zaman, hello kalan kısmından, toomonitor üretim uygulamanız gerektiğinde devam edebilmeniz için şekilde hello üretim trafiği ayırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85835-210">At hello same time, you can separate hello production traffic from hello rest so you can continue toomonitor your production app as needed.</span></span>

<span data-ttu-id="85835-211">İstemci davranışı verisi toplama olduğundan, şunları yapacaksınız [telemetri Başlatıcı tooyour JavaScript kodu eklemek](../application-insights/app-insights-api-filtering-sampling.md) Index.cshtml içinde.</span><span class="sxs-lookup"><span data-stu-id="85835-211">Since you're gathering data on client behavior, you will [add a telemetry initializer tooyour JavaScript code](../application-insights/app-insights-api-filtering-sampling.md) in index.cshtml.</span></span> <span data-ttu-id="85835-212">Tootest sunucu tarafı performans isterseniz, örneğin, bunu da benzer şekilde, sunucu kodunuzda yapabilirsiniz (bkz [özel olayları ve ölçümleri için Application Insights API'si](../application-insights/app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="85835-212">If you want tootest server-side performance, for example, you can also do similarly in your server code (see [Application Insights API for custom events and metrics](../application-insights/app-insights-api-custom-events-metrics.md).</span></span>

1. <span data-ttu-id="85835-213">İlk olarak, hello kod bewteen hello iki ekleyin `//` toohello eklenen açıklamalar aşağıda hello JavaScript bloğu içinde `<heading>` önceki etiketi.</span><span class="sxs-lookup"><span data-stu-id="85835-213">First, add hello code bewteen hello two `//` comments below in hello JavaScript block that you added toohello `<heading>` tag earlier.</span></span>

        window.appInsights = appInsights;

        // Begin new code
        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["Environment"] = "@System.Configuration.ConfigurationManager.AppSettings["environment"]";
            });
        });
        // End new code

        appInsights.trackPageView();

    <span data-ttu-id="85835-214">Bu Başlatıcı kod hello neden `appInsights` nesne tooadd hello adlı bir özel özellik `Environment` tooevery parçası telemetri gönderir.</span><span class="sxs-lookup"><span data-stu-id="85835-214">This initializer code causes hello `appInsights` object tooadd hello a custom property called `Environment` tooevery piece of telemetry it sends.</span></span>
2. <span data-ttu-id="85835-215">Ardından, bu özel özellik olarak ekleme bir [yuva ayarı](web-sites-staged-publishing.md#AboutConfiguration) azure'da web uygulamanız için.</span><span class="sxs-lookup"><span data-stu-id="85835-215">Next, add this custom property as a [slot setting](web-sites-staged-publishing.md#AboutConfiguration) for your web app in Azure.</span></span> <span data-ttu-id="85835-216">toodo Git Kabuk oturumunuzda komutları aşağıdaki Bu, çalışma hello.</span><span class="sxs-lookup"><span data-stu-id="85835-216">toodo this, run hello following commands in your Git Shell session.</span></span>

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    <span data-ttu-id="85835-217">Projenizdeki Hello Web.config zaten hello tanımlar `environment` uygulama ayarı.</span><span class="sxs-lookup"><span data-stu-id="85835-217">hello Web.config in your project already defines hello `environment` app setting.</span></span> <span data-ttu-id="85835-218">Merhaba uygulama yerel olarak test ettiğinizde bu ayar, ölçümlerinizi ile Etiketlenecek `VS Debugger`.</span><span class="sxs-lookup"><span data-stu-id="85835-218">With this setting, when you test hello app locally, your metrics will be tagged with `VS Debugger`.</span></span> <span data-ttu-id="85835-219">Ancak, değişiklikleri tooAzure bastığınızda, Azure bulabilir ve hello `environment` hello web uygulamanızın yapılandırmasında bunun yerine ayarı uygulama ve ölçümlerinizi etiketli ile `Production`.</span><span class="sxs-lookup"><span data-stu-id="85835-219">However, when you push your changes tooAzure, Azure will find and use hello `environment` app setting in hello web app's configuration instead, and your metrics will be tagged with `Production`.</span></span>
3. <span data-ttu-id="85835-220">Yürütme ve kod değişiklikleri tooyour çatalı Github'da gönderin ve kullanıcıların toouse hello yeni uygulamanız için (gerek toorefresh hello tarayıcısı) bekleyin.</span><span class="sxs-lookup"><span data-stu-id="85835-220">Commit and push your code changes tooyour fork on GitHub, and then wait for your users toouse hello new app (need toorefresh hello browser).</span></span> <span data-ttu-id="85835-221">Application Insights'da yaklaşık 15 dakika hello yeni özellik tooshow işgal `MultiChannelToDo.Web` kaynak.</span><span class="sxs-lookup"><span data-stu-id="85835-221">It takes about 15 minutes for hello new property tooshow up in your Application Insights `MultiChannelToDo.Web` resource.</span></span>

        git add -A :/
        git commit -m "add environment property tooAI events for client app"
        git push origin master
4. <span data-ttu-id="85835-222">Şimdi, toohello Git **özel olayları** dikey penceresinde tekrar ve filtre üzerinde ölçümleri hello `Environment=Production`.</span><span class="sxs-lookup"><span data-stu-id="85835-222">Now, go toohello **Custom events** blade again and filter hello metrics on `Environment=Production`.</span></span> <span data-ttu-id="85835-223">Artık bu filtre ile tüm hello yeni özel olaylar hello üretim yuvası mümkün toosee olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="85835-223">You should now be able toosee all hello new custom events in hello production slot with this filter.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. <span data-ttu-id="85835-224">Merhaba tıklatın **Sık Kullanılanlar** düğmesini toosave hello Geçerli ölçüm Gezgini ayarları toosomething ister **özel olayları: üretim**.</span><span class="sxs-lookup"><span data-stu-id="85835-224">Click hello **Favorites** button toosave hello current Metrics Explorer settings toosomething like **Custom events: Production**.</span></span> <span data-ttu-id="85835-225">Kolayca bu görünümü ve bir dağıtım yuvası görünüm arasında daha sonra geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85835-225">You can easily switch between this view and a deployment slot view later.</span></span>

   > [!TIP]
   > <span data-ttu-id="85835-226">Daha güçlü analytics için göz önünde bulundurun [Application Insights kaynağınıza Power BI ile tümleştirme](../application-insights/app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="85835-226">For even more powerful analytics, consider [integrating your Application Insights resource with Power BI](../application-insights/app-insights-export-power-bi.md).</span></span>
   >
   >

### <a name="add-slot-specific-tags-tooyour-server-app-metrics"></a><span data-ttu-id="85835-227">Yuva özgü etiketler tooyour sunucu uygulama ölçüm Ekle</span><span class="sxs-lookup"><span data-stu-id="85835-227">Add slot-specific tags tooyour server app metrics</span></span>
<span data-ttu-id="85835-228">Yeniden, bütünlük açısından hello sunucu tarafı uygulama ayarlama.</span><span class="sxs-lookup"><span data-stu-id="85835-228">Again, for completeness you will set up hello server-side app.</span></span> <span data-ttu-id="85835-229">JavaScript'te izlenmiş hello istemci uygulaması, yuva özgü etiketler hello sunucu uygulaması için izlenmiş .NET koduyla.</span><span class="sxs-lookup"><span data-stu-id="85835-229">Unlike hello client app which is instrumented in JavaScript, slot-specific tags for hello server app is instrumented with .NET code.</span></span>

1. <span data-ttu-id="85835-230">Açık  *&lt;repository_root >*\src\MultiChannelToDo\Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="85835-230">Open *&lt;repository_root>*\src\MultiChannelToDo\Global.asax.cs.</span></span> <span data-ttu-id="85835-231">Yalnızca ad alanı kuşak kapatma hello önce aşağıda Hello kod bloğunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="85835-231">Add hello code block below, just before hello closing namespace curly brace.</span></span>

        namespace MultiChannelToDo
        {
                ...

                // Begin new code
            public class ConfigInitializer
            : ITelemetryInitializer
            {
                void ITelemetryInitializer.Initialize(ITelemetry telemetry)
                {
                    telemetry.Context.Properties["Environment"] = System.Configuration.ConfigurationManager.AppSettings["environment"];
                }
            }
                // End new code
        }
2. <span data-ttu-id="85835-232">Merhaba ekleyerek hello ad çözümleme hataları düzeltin `using` toohello başına aşağıdaki deyimleri hello dosyasının:</span><span class="sxs-lookup"><span data-stu-id="85835-232">Correct hello name resolution errors by adding hello `using` statements below toohello beginning of hello file:</span></span>

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. <span data-ttu-id="85835-233">Merhaba toohello başlangıcını aşağıda Hello kodu ekleyin `Application_Start()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="85835-233">Add hello code below toohello beginning of hello `Application_Start()` method:</span></span>

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. <span data-ttu-id="85835-234">Yürütme ve kod değişiklikleri tooyour çatalı Github'da gönderin ve kullanıcıların toouse hello yeni uygulamanız için (gerek toorefresh hello tarayıcısı) bekleyin.</span><span class="sxs-lookup"><span data-stu-id="85835-234">Commit and push your code changes tooyour fork on GitHub, and then wait for your users toouse hello new app (need toorefresh hello browser).</span></span> <span data-ttu-id="85835-235">Application Insights'da yaklaşık 15 dakika hello yeni özellik tooshow işgal `MultiChannelToDo` kaynak.</span><span class="sxs-lookup"><span data-stu-id="85835-235">It takes about 15 minutes for hello new property tooshow up in your Application Insights `MultiChannelToDo` resource.</span></span>

        git add -A :/
        git commit -m "add environment property tooAI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a><span data-ttu-id="85835-236">Güncelleştirmesi: Beta dal ayarlama</span><span class="sxs-lookup"><span data-stu-id="85835-236">Update: Set up your beta branch</span></span>
1. <span data-ttu-id="85835-237">Açık  *&lt;repository_root >*\ARMTemplates\ProdAndStagetest.json ve bulma hello `appsettings` kaynakları (arama `"name": "appsettings"`).</span><span class="sxs-lookup"><span data-stu-id="85835-237">Open *&lt;repository_root>*\ARMTemplates\ProdAndStagetest.json and find hello `appsettings` resources (search for `"name": "appsettings"`).</span></span> <span data-ttu-id="85835-238">Biri, her yuva için bir tane 4 vardır.</span><span class="sxs-lookup"><span data-stu-id="85835-238">There are 4 of them, one for each slot.</span></span>
2. <span data-ttu-id="85835-239">Her `appsettings` kaynak eklemek bir `"environment": "[parameters('slotName')]"` uygulama ayarı toohello hello sonuna `properties` dizi.</span><span class="sxs-lookup"><span data-stu-id="85835-239">For each `appsettings` resource, add an  `"environment": "[parameters('slotName')]"` app setting toohello end of hello `properties` array.</span></span> <span data-ttu-id="85835-240">Virgül ile tooend hello önceki satıra unutmayın.</span><span class="sxs-lookup"><span data-stu-id="85835-240">Don't forget tooend hello previous line with a comma.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    <span data-ttu-id="85835-241">Merhaba eklemiş olduğunuz `environment` uygulama tooall hello yuvaları hello şablonunda ayarlama.</span><span class="sxs-lookup"><span data-stu-id="85835-241">You have just added hello `environment` app setting tooall hello slots in hello template.</span></span>
3. <span data-ttu-id="85835-242">Buna Merhaba aynı dosya, hello bulur `slotconfignames` kaynakları (arama `"name": "slotconfignames"`).</span><span class="sxs-lookup"><span data-stu-id="85835-242">In hello same file, find hello `slotconfignames` resources (search for `"name": "slotconfignames"`).</span></span> <span data-ttu-id="85835-243">Her uygulama için bir tane bunların, 2 vardır.</span><span class="sxs-lookup"><span data-stu-id="85835-243">There are 2 of them, one for each app.</span></span>
4. <span data-ttu-id="85835-244">Her `slotconfignames` kaynak eklemek `"environment"` hello toohello sonuna `appSettingNames` dizi.</span><span class="sxs-lookup"><span data-stu-id="85835-244">For each `slotconfignames` resource, add `"environment"` toohello end of hello `appSettingNames` array.</span></span> <span data-ttu-id="85835-245">Virgül ile tooend hello önceki satıra unutmayın.</span><span class="sxs-lookup"><span data-stu-id="85835-245">Don't forget tooend hello previous line with a comma.</span></span>

    <span data-ttu-id="85835-246">Merhaba yaptığınız `environment` uygulama ayarı çubuğu tooits ilgili dağıtım yuvası hem uygulamalar için.</span><span class="sxs-lookup"><span data-stu-id="85835-246">You have just made hello `environment` app setting stick tooits respective deployment slot for both apps.</span></span>  
5. <span data-ttu-id="85835-247">Çalışma hello aşağıdaki Git Kabuk oturumunuzda hello ile aynı komutları önce kullandığınız kaynak grubu soneki.</span><span class="sxs-lookup"><span data-stu-id="85835-247">In your Git Shell session, run hello following commands with hello same resource group suffix that you used before.</span></span>

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. <span data-ttu-id="85835-248">İstendiğinde, belirtin öncekiyle aynı SQL veritabanı kimlik bilgileri hello.</span><span class="sxs-lookup"><span data-stu-id="85835-248">When prompted, specify hello same SQL database credentials as before.</span></span> <span data-ttu-id="85835-249">Ardından, ne zaman sorulan tooupdate hello kaynak grubu, türü `Y`, ardından `ENTER`.</span><span class="sxs-lookup"><span data-stu-id="85835-249">Then, when asked tooupdate hello resource group, type `Y`, then `ENTER`.</span></span>

    <span data-ttu-id="85835-250">Merhaba betik tamamlandıktan, hello özgün kaynak grubundaki tüm kaynaklarınızı korunur, ancak "beta" adlı yeni bir yuva içinde hello ile aynı oluşturulduktan sonra hello'den itibaren oluşturulduğu hello "Hazırlama" yuvası yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="85835-250">Once hello script finishes, all your resources in hello original resource group are retained, but a new slot named "beta" is created in it with hello same configuration as hello "Staging" slot that was created in hello beginning.</span></span>

   > [!NOTE]
   > <span data-ttu-id="85835-251">Bu yöntem farklı dağıtım ortamları oluşturma hello yönteminden farklıdır [Azure App Service ile Çevik Yazılım Geliştirme](app-service-agile-software-development.md).</span><span class="sxs-lookup"><span data-stu-id="85835-251">This method of creating different deployment environments is different from hello method in [Agile software development with Azure App Service](app-service-agile-software-development.md).</span></span> <span data-ttu-id="85835-252">Burada, beklenmediğini dağıtım ortamları kaynak gruplarıyla oluşturduğunuz dağıtım yuvası ile dağıtım ortamlar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="85835-252">Here, you create deployment environments with deployment slots, where as there you create deployment environments with resource groups.</span></span> <span data-ttu-id="85835-253">Dağıtım ortamları kaynak gruplarıyla yönetme tookeep hello üretim ortamı off-limits toodevelopers sağlar, ancak yuvası ile kolayca yapabilirsiniz üretim test kolay toodo değil.</span><span class="sxs-lookup"><span data-stu-id="85835-253">Managing deployment environments with resource groups enables you tookeep hello production environment off-limits toodevelopers, but it's not easy toodo testing in production, which you can do easily with slots.</span></span>
   >
   >

<span data-ttu-id="85835-254">İsterseniz, ayrıca bir alfa uygulamayı çalıştırarak oluşturabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="85835-254">If you wish, you can also create an alpha app by running</span></span>

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

<span data-ttu-id="85835-255">Bu öğretici için yalnızca beta uygulamanızı kullanmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="85835-255">For this tutorial, you will just keep using your beta app.</span></span>

## <a name="update-push-your-updates-toohello-beta-app"></a><span data-ttu-id="85835-256">Güncelleştirme: güncelleştirmeleri toohello beta uygulamanıza anında iletme</span><span class="sxs-lookup"><span data-stu-id="85835-256">Update: Push your updates toohello beta app</span></span>
<span data-ttu-id="85835-257">Tooimprove istediğiniz tooyour uygulama yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="85835-257">Back tooyour app that you want tooimprove.</span></span>

1. <span data-ttu-id="85835-258">Şimdi, beta dalında olduğunuzdan emin olun</span><span class="sxs-lookup"><span data-stu-id="85835-258">Make sure you're now in your beta branch</span></span>

        git checkout beta
2. <span data-ttu-id="85835-259">İçinde  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, Bul hello `<li>` etiketi ve hello eklemek `style="cursor:pointer"` , aşağıda gösterildiği gibi özniteliği.</span><span class="sxs-lookup"><span data-stu-id="85835-259">In *&lt;repository_root>*\src\MultiChannelToDo.Web\app\Index.cshtml, find hello `<li>` tag and add hello `style="cursor:pointer"` attribute, as shown below.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. <span data-ttu-id="85835-260">yürütme ve anında iletme tooAzure.</span><span class="sxs-lookup"><span data-stu-id="85835-260">commit and push tooAzure.</span></span>
4. <span data-ttu-id="85835-261">Merhaba değişiklik şimdi hello beta yuvada toohttp://todoapp giderek yansıtılır doğrulayın*&lt;your_suffix >*-beta.azurewebsites.net/.</span><span class="sxs-lookup"><span data-stu-id="85835-261">Verify that hello change is now reflected in hello beta slot by navigating toohttp://todoapp*&lt;your_suffix>*-beta.azurewebsites.net/.</span></span> <span data-ttu-id="85835-262">Değiştirme henüz, tarayıcı tooget hello yeni javascript kodu Yenile hello görmüyorsanız.</span><span class="sxs-lookup"><span data-stu-id="85835-262">If you don't see hello change yet, refresh your browser tooget hello new javascript code.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

<span data-ttu-id="85835-263">Merhaba beta yuvasında çalıştıran değişikliğinizin sahip olduğunuza göre hazır tooperform flighting dağıtım olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="85835-263">Now that you have your change running in hello beta slot, you are ready tooperform a flighting deployment.</span></span>

## <a name="validate-route-traffic-toohello-beta-app"></a><span data-ttu-id="85835-264">Doğrulama: Rota trafiği toohello beta uygulama</span><span class="sxs-lookup"><span data-stu-id="85835-264">Validate: Route traffic toohello beta app</span></span>
<span data-ttu-id="85835-265">Bu bölümde, trafik toohello beta uygulama yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="85835-265">In this section, you will route traffic toohello beta app.</span></span> <span data-ttu-id="85835-266">For sake of daha anlaşılır olması, tanıtım tooroute hello kullanıcı trafiği tooit önemli bir kısmını oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="85835-266">For sake of clarity of demonstration, you're going tooroute a significant portion of hello user traffic tooit.</span></span> <span data-ttu-id="85835-267">Gerçekte, tooroute belirli durumunuza bağlıdır istediğiniz trafik miktarı hello.</span><span class="sxs-lookup"><span data-stu-id="85835-267">In reality, hello amount of traffic you want tooroute will depend on your specific situation.</span></span> <span data-ttu-id="85835-268">Örneğin, siteniz microsoft.com hello ölçekte ise, toplam trafiğinizi sipariş toogain yararlı verilerdeki yüzde biri'den az gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="85835-268">For example, if your site is at hello scale of microsoft.com, then you may need less than one percent of your total traffic in order toogain useful data.</span></span>

1. <span data-ttu-id="85835-269">Git Kabuk oturumunuzda komutları tooroute aşağıdaki hello hello üretim trafiği toohello beta yuvası yarısı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="85835-269">In your Git Shell session, run hello following commands tooroute half of hello production traffic toohello beta slot:</span></span>

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   <span data-ttu-id="85835-270">Merhaba `ReroutePercentage=50` özelliği, % 50'hello üretim trafik yönlendirilmiş toohello beta uygulamanızın URL'sine olacağını belirtir (Merhaba tarafından belirtilen `ActionHostName` özelliği).</span><span class="sxs-lookup"><span data-stu-id="85835-270">hello `ReroutePercentage=50` property specifies that 50% of hello production traffic will be routed toohello beta app's URL (specified by hello `ActionHostName` property).</span></span>
2. <span data-ttu-id="85835-271">Şimdi toohttp://ToDoApp gidin*&lt;your_suffix >*. azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="85835-271">Now navigate toohttp://ToDoApp*&lt;your_suffix>*.azurewebsites.net.</span></span> <span data-ttu-id="85835-272">% 50'hello trafik artık yeniden yönlendirilen toohello beta yuvası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="85835-272">50% of hello traffic should now be redirected toohello beta slot.</span></span>
3. <span data-ttu-id="85835-273">Application Insights kaynağınıza hello ölçümleri ortamı tarafından filtre "beta" =.</span><span class="sxs-lookup"><span data-stu-id="85835-273">In your Application Insights resource, filter hello metrics by environment="beta".</span></span>

   > [!NOTE]
   > <span data-ttu-id="85835-274">Bu filtre uygulanmış bir görünüm başka bir sık kullanılan olarak kaydederseniz, hello ölçüm Gezgini görünümler üretim ve beta görünümler arasında kolayca çevirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85835-274">If you save this filtered view as another favorite, then you can easily flip hello metric explorer views between production and beta views.</span></span>
   >
   >

<span data-ttu-id="85835-275">Application Insights'ta benzeri toohello aşağıdakilere bakın varsayın:</span><span class="sxs-lookup"><span data-stu-id="85835-275">Suppose in Application Insights you see something similar toohello following:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

<span data-ttu-id="85835-276">Yalnızca bu hello pek çok daha fazla tıklar olduğunu gösteriyor `<li>` etiketleri yok gibi görünüyor, ancak toobe dalgalanma tıklama `<li>` etiketler.</span><span class="sxs-lookup"><span data-stu-id="85835-276">Not only is this showing that there are many more clicks on hello `<li>` tags, but there seems toobe a surge of clicks on `<li>` tags.</span></span> <span data-ttu-id="85835-277">Ardından kişiler hello yeni bulunmuş tamamlanabilmesi `<li>` etiketleri tıklanabilir ve tüm daha önce tamamlandı görevlerini hello uygulamasında artık temizleme.</span><span class="sxs-lookup"><span data-stu-id="85835-277">You can then conclude that people have discovered hello new `<li>` tags are clickable and are now clearing all their previously-completed tasks in hello app.</span></span>

<span data-ttu-id="85835-278">Flighting dağıtımınızı Hello verilerini temel alarak yeni UI üretime hazır olduğuna karar verin.</span><span class="sxs-lookup"><span data-stu-id="85835-278">Based on hello data of your flighting deployment, you decide that your new UI is ready for production.</span></span>

## <a name="go-live-move-your-new-code-into-production"></a><span data-ttu-id="85835-279">Canlı gidin: yeni kodunuzu üretim ortamına taşıyın</span><span class="sxs-lookup"><span data-stu-id="85835-279">Go live: Move your new code into production</span></span>
<span data-ttu-id="85835-280">Güncelleştirme tooproduction şimdi hazır toomove demektir.</span><span class="sxs-lookup"><span data-stu-id="85835-280">You're now ready toomove your update tooproduction.</span></span> <span data-ttu-id="85835-281">Artık güncelleştirmenizi zaten doğrulandı biliyorsunuz harika nedir olan *önce* tooproduction gönderilir.</span><span class="sxs-lookup"><span data-stu-id="85835-281">What's great is that now you know that your update has already been validated *before* it is pushed tooproduction.</span></span> <span data-ttu-id="85835-282">Artık bunu güvenle dağıtabilir.</span><span class="sxs-lookup"><span data-stu-id="85835-282">So now you can confidently deploy it.</span></span> <span data-ttu-id="85835-283">Bir güncelleştirme toohello AngularJS istemci uygulama tarafından olduğundan, yalnızca hello istemci-tarafı kodu doğrulandı.</span><span class="sxs-lookup"><span data-stu-id="85835-283">Since you made an update toohello AngularJS client app, you only validated hello client-side code.</span></span> <span data-ttu-id="85835-284">Toomake değişiklikleri toohello arka uç Web API uygulaması olsaydı, değişikliklerinizi benzer şekilde ve kolayca doğrulamak.</span><span class="sxs-lookup"><span data-stu-id="85835-284">If you were toomake changes toohello back-end Web API app, you could validate your changes similarly and easily.</span></span>

1. <span data-ttu-id="85835-285">Git Kabuğu'nda hello trafik yönlendirme kuralı hello aşağıdaki komutu çalıştırarak kaldırın:</span><span class="sxs-lookup"><span data-stu-id="85835-285">In Git Shell, remove hello traffic routing rule by running hello following command:</span></span>

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. <span data-ttu-id="85835-286">Merhaba Git komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="85835-286">Run hello Git commands:</span></span>

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. <span data-ttu-id="85835-287">Yeni hello için bir kaç dakika hazırlık yuvasındaki dağıtılan toobe toohello kod sonra http://ToDoApp başlatma için beklemesi*&lt;your_suffix >*-yeni güncelleştirme hello staging.azurewebsites.net tooverify warmed hello hazırlama Yuva.</span><span class="sxs-lookup"><span data-stu-id="85835-287">Wait for a few minutes for hello new code toobe deployed toohello staging slot, then launch http://ToDoApp*&lt;your_suffix>*-staging.azurewebsites.net tooverify that hello new update is warmed up in hello staging slot.</span></span> <span data-ttu-id="85835-288">Çatalı ait ana dala olduğundan bu hello bağlı toohello hazırlama unutmayın, uygulamanızın yuvası.</span><span class="sxs-lookup"><span data-stu-id="85835-288">Remember that hello your fork's master branch is linked toohello staging slot of your app.</span></span>
4. <span data-ttu-id="85835-289">Şimdi, üretime hazırlık yuvasındaki hello değiştirme</span><span class="sxs-lookup"><span data-stu-id="85835-289">Now, swap hello staging slot into production</span></span>

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a><span data-ttu-id="85835-290">Özet</span><span class="sxs-lookup"><span data-stu-id="85835-290">Summary</span></span>
<span data-ttu-id="85835-291">Azure uygulama hizmeti küçük toomedium-ölçekli işletmeler tootest müşterilerle uygulamalarını üretimde bir şey büyük kuruluşlarda bir geleneksel yapılan kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="85835-291">Azure App Service makes it easy for small- toomedium-sized businesses tootest their customer-facing apps in production, something that has been traditionally done in big enterprises.</span></span> <span data-ttu-id="85835-292">Neyse ki bu öğretici verdiği hello ihtiyacınız toobring birlikte App Service ve Application Insights toomake olası flighting dağıtım ve hatta diğer test üretimde senaryoları DevOps dünyada bilgi.</span><span class="sxs-lookup"><span data-stu-id="85835-292">Hopefully, this tutorial has given you hello knowledge you need toobring together App Service and Application Insights toomake possible flighting deployment, and even other test-in-production scenarios, in your DevOps world.</span></span>

## <a name="more-resources"></a><span data-ttu-id="85835-293">Diğer kaynaklar</span><span class="sxs-lookup"><span data-stu-id="85835-293">More resources</span></span>
* [<span data-ttu-id="85835-294">Azure App Service ile Çevik Yazılım Geliştirme</span><span class="sxs-lookup"><span data-stu-id="85835-294">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)
* [<span data-ttu-id="85835-295">Hazırlık ortamları için Azure App Service'te web uygulamalarını ayarlama</span><span class="sxs-lookup"><span data-stu-id="85835-295">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)
* [<span data-ttu-id="85835-296">Azure'nın beklendiği karmaşık bir uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="85835-296">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="85835-297">Azure Resource Manager şablonları yazma</span><span class="sxs-lookup"><span data-stu-id="85835-297">Authoring Azure Resource Manager Templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="85835-298">JSONLint - hello JSON Doğrulayıcı</span><span class="sxs-lookup"><span data-stu-id="85835-298">JSONLint - hello JSON Validator</span></span>](http://jsonlint.com/)
* [<span data-ttu-id="85835-299">Git dallanma – temel dallandırma ve birleştirme</span><span class="sxs-lookup"><span data-stu-id="85835-299">Git Branching – Basic Branching and Merging</span></span>](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [<span data-ttu-id="85835-300">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="85835-300">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="85835-301">Proje Kudu Wiki</span><span class="sxs-lookup"><span data-stu-id="85835-301">Project Kudu Wiki</span></span>](https://github.com/projectkudu/kudu/wiki)
