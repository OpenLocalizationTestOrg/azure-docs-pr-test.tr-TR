---
title: "(Azure App Service'te test beta) flighting dağıtımı"
description: "Yeni özellikler, uygulamanızda uçuş veya beta bu uçtan uca öğretici, güncelleştirmeleri test öğrenin. Ayrıca sürekli yayımlama, yuvaları, trafik yönlendirme ve Application Insights tümleştirme gibi uygulama hizmeti özellikleri araya getirir."
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
ms.openlocfilehash: 83e3247310461ac148fff3c4ade3aa7216478537
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a><span data-ttu-id="cdebc-104">(Azure App Service'te test beta) flighting dağıtımı</span><span class="sxs-lookup"><span data-stu-id="cdebc-104">Flighting deployment (beta testing) in Azure App Service</span></span>
<span data-ttu-id="cdebc-105">Bu öğretici nasıl yapılacağını gösterir *flighting dağıtımları* çeşitli özelliklerini tümleştirme tarafından [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) ve [Azure Application Insights](/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="cdebc-105">This tutorial shows you how to do *flighting deployments* by integrating the various capabilities of [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure Application Insights](/services/application-insights/).</span></span>

<span data-ttu-id="cdebc-106">*Flighting* bir yeni özellik veya sınırlı sayıda gerçek müşteri değişiklikle doğrulayan bir dağıtım işlemidir ve ana üretim senaryosunda test etmektir.</span><span class="sxs-lookup"><span data-stu-id="cdebc-106">*Flighting* is a deployment process that validates a new feature or change with a limited number of real customers, and is a major testing in production scenario.</span></span> <span data-ttu-id="cdebc-107">Bu beta test benzer ve bazen "denetimli test uçuş" bilinir.</span><span class="sxs-lookup"><span data-stu-id="cdebc-107">It is akin to beta testing and is sometimes known as "controlled test flight".</span></span> <span data-ttu-id="cdebc-108">Bir web varlığı çok büyük ölçekli işletmeler için erken doğrulama bunların bir uygulamada kendi uygulama güncelleştirmelerini almak üzere bu yaklaşımı kullanın [Çevik Geliştirme](https://en.wikipedia.org/wiki/Agile_software_development).</span><span class="sxs-lookup"><span data-stu-id="cdebc-108">Many large enterprises with a web presence use this approach to get early validation on their app updates in their practice of [agile development](https://en.wikipedia.org/wiki/Agile_software_development).</span></span> <span data-ttu-id="cdebc-109">Azure uygulama hizmeti, üretim aşamasındaki bir test sürekli yayımlama ve aynı DevOps senaryosunu uygulamak için Application Insights ile tümleştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="cdebc-109">Azure App Service enables you to integrate test in production with continous publishing and Application Insights to implement the same DevOps scenario.</span></span> <span data-ttu-id="cdebc-110">Bu yaklaşımın avantajları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="cdebc-110">Benefits of this approach include:</span></span>

* <span data-ttu-id="cdebc-111">**Gerçek geri bildirim sağlamak *önce* güncelleştirmeleri üretime serbest** -bırakmadan önce yayın hemen sonra geri bildirim sağlamasını daha iyi tek şey geri bildirim alma.</span><span class="sxs-lookup"><span data-stu-id="cdebc-111">**Gain real feedback *before* updates are released to production** - The only thing better than gaining feedback as soon as you release is gaining feedback before you release.</span></span> <span data-ttu-id="cdebc-112">Gerçek kullanıcı trafiği ve davranışları güncelleştirmeleriyle ürün yaşam döngüsünde işlemleriniz olabildiğince erken test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdebc-112">You can test updates with real user traffic and behaviors as early as you desire in the product life cycle.</span></span>
* <span data-ttu-id="cdebc-113">**Geliştirmek [sürekli teste dayalı geliştirme (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)**  - kullanıcı doğrulama ürün yaşam döngüsünde erken ve otomatik olarak gerçekleşir üretim aşamasındaki bir test sürekli tümleştirme ve Application Insights ile araçları ile tümleştirme.</span><span class="sxs-lookup"><span data-stu-id="cdebc-113">**Enhance [continuous test-driven development (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)** - By integrating test in production with continuous integration and instrumentation with Application Insights, user validation happens early and automatically in your product life cycle.</span></span> <span data-ttu-id="cdebc-114">Bu, el ile test yürütme zamanı yatırım azaltılmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="cdebc-114">This helps reduce time investments in manual test execution.</span></span>
* <span data-ttu-id="cdebc-115">**Test iş akışı en iyi duruma getirme** -sürekli izleme araçları ile üretim aşamasındaki bir test otomatik hale getirerek, potansiyel olarak çeşitli tek bir işlem içinde Test amaçları gibi gerçekleştirebilirsiniz [tümleştirme](https://en.wikipedia.org/wiki/Integration_testing), [regresyon](https://en.wikipedia.org/wiki/Regression_testing), [kullanılabilirlik](https://en.wikipedia.org/wiki/Usability_testing), erişilebilirlik, yerelleştirme, [performans](https://en.wikipedia.org/wiki/Software_performance_testing), [güvenlik](https://en.wikipedia.org/wiki/Security_testing), ve [kabul](https://en.wikipedia.org/wiki/Acceptance_testing).</span><span class="sxs-lookup"><span data-stu-id="cdebc-115">**Optimize test workflow** - By automating test in production with continuous monitoring instrumentation, you can potentially accomplish the goals of various kinds of tests in a single process, such as [integration](https://en.wikipedia.org/wiki/Integration_testing), [regression](https://en.wikipedia.org/wiki/Regression_testing), [usability](https://en.wikipedia.org/wiki/Usability_testing), accessibility, localization, [performance](https://en.wikipedia.org/wiki/Software_performance_testing), [security](https://en.wikipedia.org/wiki/Security_testing), and [acceptance](https://en.wikipedia.org/wiki/Acceptance_testing).</span></span>

<span data-ttu-id="cdebc-116">Flighting dağıtım neredeyse dinamik trafik yönlendirme değil.</span><span class="sxs-lookup"><span data-stu-id="cdebc-116">A flighting deployment is not just about routing live traffic.</span></span> <span data-ttu-id="cdebc-117">Mümkün olan en kısa sürede iyi kavramak için istediğiniz böyle bir dağıtımda, olması beklenmeyen bir hata, bir performans düşüşü, kullanıcı deneyimi sorunları.</span><span class="sxs-lookup"><span data-stu-id="cdebc-117">In such a deployment you want to gain insight as quickly as possible, whether it be an unexpected bug, performance degradation, user experience issues.</span></span> <span data-ttu-id="cdebc-118">Gerçek müşterilerle çalışıyorsanız unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cdebc-118">Remember, you are dealing with real customers.</span></span> <span data-ttu-id="cdebc-119">Bu nedenle yapmak için sağ, sonraki adımınız için bilinçli bir karar yapmak için gereken tüm verileri toplamak için flighting dağıtımınızın ayarladığınızdan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cdebc-119">So to do it right, you must make sure that you have set up your flighting deployment to gather all the data you need in order to make an informed decision for your next step.</span></span> <span data-ttu-id="cdebc-120">Bu öğretici, Application Insights ile verileri toplamak nasıl gösterir, ancak New Relic veya senaryonuza uygun diğer teknolojileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdebc-120">This tutorial shows you how to collect data with Application Insights, but you can use New Relic or other technologies that suits your scenario.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="cdebc-121">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="cdebc-121">What you will do</span></span>
<span data-ttu-id="cdebc-122">Bu öğreticide, birlikte üretimde uygulama hizmeti uygulamanızı test etmek için aşağıdaki senaryoları Getir öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="cdebc-122">In this tutorial, you will learn how to bring the following scenarios together to test your App Service app in production:</span></span>

* <span data-ttu-id="cdebc-123">[Üretim trafiği yönlendirmek](app-service-web-test-in-production-get-start.md) beta uygulamanıza</span><span class="sxs-lookup"><span data-stu-id="cdebc-123">[Route production traffic](app-service-web-test-in-production-get-start.md) to your beta app</span></span>
* <span data-ttu-id="cdebc-124">[Uygulamanızı izleme](../application-insights/app-insights-web-track-usage.md) yararlı ölçümler edinme</span><span class="sxs-lookup"><span data-stu-id="cdebc-124">[Instrument your app](../application-insights/app-insights-web-track-usage.md) to obtain useful metrics</span></span>
* <span data-ttu-id="cdebc-125">Sürekli olarak beta uygulamanızı dağıtma ve dinamik uygulama ölçümleri izleme</span><span class="sxs-lookup"><span data-stu-id="cdebc-125">Continuously deploy your beta app and track live app metrics</span></span>
* <span data-ttu-id="cdebc-126">Ölçümleri üretim uygulamasına nasıl kod değişiklikleri sonuçları Çevir görmek için beta uygulama arasında karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="cdebc-126">Compare metrics between the production app and the beta app to see how code changes translate to results</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="cdebc-127">İhtiyacınız olacak</span><span class="sxs-lookup"><span data-stu-id="cdebc-127">What you will need</span></span>
* <span data-ttu-id="cdebc-128">Bir Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="cdebc-128">An Azure account</span></span>
* <span data-ttu-id="cdebc-129">A [GitHub](https://github.com/) hesabı</span><span class="sxs-lookup"><span data-stu-id="cdebc-129">A [GitHub](https://github.com/) account</span></span>
* <span data-ttu-id="cdebc-130">Visual Studio 2015 - yükleyebilir [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="cdebc-130">Visual Studio 2015 - you can download the [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).</span></span>
* <span data-ttu-id="cdebc-131">Git Kabuğu (yüklenmiş [Windows için GitHub](https://windows.github.com/))-Bu, aynı oturumunda Git ve PowerShell komutlarını çalıştırmanıza olanak sağlar</span><span class="sxs-lookup"><span data-stu-id="cdebc-131">Git Shell (installed with [GitHub for Windows](https://windows.github.com/)) - this enables you to run both the Git and PowerShell commands in the same session</span></span>
* <span data-ttu-id="cdebc-132">En son [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) BITS</span><span class="sxs-lookup"><span data-stu-id="cdebc-132">Latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) bits</span></span>
* <span data-ttu-id="cdebc-133">Aşağıdaki temel bilgilere:</span><span class="sxs-lookup"><span data-stu-id="cdebc-133">Basic understanding of the following:</span></span>
  * <span data-ttu-id="cdebc-134">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) şablon dağıtımı (bkz [beklendiği azure'da karmaşık bir uygulama dağıtmak](app-service-deploy-complex-application-predictably.md))</span><span class="sxs-lookup"><span data-stu-id="cdebc-134">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) template deployment (see [Deploy a complex application predictably in Azure](app-service-deploy-complex-application-predictably.md))</span></span>
  * [<span data-ttu-id="cdebc-135">Git</span><span class="sxs-lookup"><span data-stu-id="cdebc-135">Git</span></span>](http://git-scm.com/documentation)
  * [<span data-ttu-id="cdebc-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cdebc-136">PowerShell</span></span>](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> <span data-ttu-id="cdebc-137">Bu öğreticiyi tamamlamak için bir Azure hesabınızın olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="cdebc-137">You need an Azure account to complete this tutorial:</span></span>
>
> * <span data-ttu-id="cdebc-138">Yapabilecekleriniz [ücretsiz bir Azure hesabı açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/) -krediler alırsınız, ücretli Azure hizmetlerini denemek için kullanabileceğiniz ve bunlar bitmiş bile hesabı sürdürebilir ve ücretsiz Web uygulamaları gibi Azure hizmetlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdebc-138">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Web Apps.</span></span>
> * <span data-ttu-id="cdebc-139">Yapabilecekleriniz [Visual Studio abone Avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -bilgisayarınızı Visual Studio abonelik size kredi verir Ücretli Azure hizmetlerinizi kullanabildiğiniz her ay.</span><span class="sxs-lookup"><span data-stu-id="cdebc-139">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="cdebc-140">Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="cdebc-140">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="cdebc-141">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="cdebc-141">No credit cards required; no commitments.</span></span>
>
>

## <a name="set-up-your-production-web-app"></a><span data-ttu-id="cdebc-142">Üretim web uygulamanızı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="cdebc-142">Set up your production web app</span></span>
> [!NOTE]
> <span data-ttu-id="cdebc-143">Bu öğreticide kullanılan komut dosyası, GitHub havuzunuzdan sürekli yayımlama otomatik olarak yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="cdebc-143">The script used in this tutorial will automatically configure continuous publishing from your GitHub repository.</span></span> <span data-ttu-id="cdebc-144">Bu gerektirir GitHub kimlik bilgilerinizi zaten Azure'da depolanır, aksi takdirde komut dosyalı dağıtım web uygulamaları için kaynak denetim ayarları yapılandırmak çalışırken başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="cdebc-144">This requires that your GitHub credentials are already stored in Azure, otherwise the scripted deployment will fail when attempting to configure source control settings for the web apps.</span></span>
>
> <span data-ttu-id="cdebc-145">Azure'da GitHub kimlik bilgilerinizi depolamak için bir web uygulaması oluşturmak [Azure Portal](https://portal.azure.com/) ve [GitHub dağıtımını yapılandırma](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="cdebc-145">To store your GitHub credentials in Azure, create a web app in the [Azure Portal](https://portal.azure.com/) and [configure GitHub deployment](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="cdebc-146">Yalnızca bu kez yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cdebc-146">You only need to do this once.</span></span>
>
>

<span data-ttu-id="cdebc-147">Tipik bir DevOps senaryo azure'da çalışan bir uygulamanız varsa ve kullanarak sürekli yayımlama değişiklik istiyor.</span><span class="sxs-lookup"><span data-stu-id="cdebc-147">In a typical DevOps scenario, you have an application that’s running live in Azure, and you want to make changes to it through continuous publishing.</span></span> <span data-ttu-id="cdebc-148">Bu senaryoda üretime geliştirilen ve sınanmış bir şablon dağıtır.</span><span class="sxs-lookup"><span data-stu-id="cdebc-148">In this scenario, you will deploy to production a template that you have developed and tested.</span></span>

1. <span data-ttu-id="cdebc-149">Kendi çatalı oluşturma [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) deposu.</span><span class="sxs-lookup"><span data-stu-id="cdebc-149">Create your own fork of the [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repository.</span></span> <span data-ttu-id="cdebc-150">Çatalı oluşturma hakkında daha fazla bilgi için bkz: [bir depoyu Çatallaştırma](https://help.github.com/articles/fork-a-repo/).</span><span class="sxs-lookup"><span data-stu-id="cdebc-150">For information on creating your fork, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/).</span></span> <span data-ttu-id="cdebc-151">Çatalı oluşturulduktan sonra tarayıcınızı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdebc-151">Once your fork is created, you can see it in your browser.</span></span>

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. <span data-ttu-id="cdebc-152">Git kabuk oturumu açın.</span><span class="sxs-lookup"><span data-stu-id="cdebc-152">Open a Git Shell session.</span></span> <span data-ttu-id="cdebc-153">Git Kabuk henüz yoksa, yükleme [Windows için GitHub](https://windows.github.com/) şimdi.</span><span class="sxs-lookup"><span data-stu-id="cdebc-153">If you don't have Git Shell yet, install [GitHub for Windows](https://windows.github.com/) now.</span></span>
3. <span data-ttu-id="cdebc-154">Aşağıdaki komutu çalıştırarak, çatalı yerel bir kopyasını oluşturun:</span><span class="sxs-lookup"><span data-stu-id="cdebc-154">Create a local clone of your fork by executing the following command:</span></span>

     <span data-ttu-id="cdebc-155">Git kopya https://github.com/<your_fork>/ToDoApp.git</span><span class="sxs-lookup"><span data-stu-id="cdebc-155">git clone https://github.com/<your_fork>/ToDoApp.git</span></span>
4. <span data-ttu-id="cdebc-156">Yerel kopya oluşturduktan sonra gidin  *&lt;repository_root >*\ARMTemplates ve deploy.ps1 komut dosyası benzersiz bir sonek ile aşağıda gösterildiği gibi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="cdebc-156">Once you have your local clone, navigate to *&lt;repository_root>*\ARMTemplates, and run the deploy.ps1 script with a unique suffix, as shown below:</span></span>

     <span data-ttu-id="cdebc-157">.\deploy.ps1 – RepoUrl https://github.com/<your_fork>/todoapp.git - ResourceGroupSuffix < your_suffix ></span><span class="sxs-lookup"><span data-stu-id="cdebc-157">.\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git -ResourceGroupSuffix <your_suffix></span></span>
5. <span data-ttu-id="cdebc-158">İstendiğinde, istenilen kullanıcı adı ve veritabanı erişimi için parolayı yazın.</span><span class="sxs-lookup"><span data-stu-id="cdebc-158">When prompted, type in the desired username and password for database access.</span></span> <span data-ttu-id="cdebc-159">Bunları kaynak grubu güncelleştirilirken yeniden belirtmeniz gerekir çünkü veritabanı kimlik bilgilerinizi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cdebc-159">Remember your database credentials because you will need to specify them again when updating the resource group.</span></span>

   <span data-ttu-id="cdebc-160">Çeşitli Azure kaynaklarını hazırlama sürecini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cdebc-160">You should see the provisioning progress of various Azure resources.</span></span> <span data-ttu-id="cdebc-161">Dağıtım tamamlandığında, komut dosyası uygulamayı tarayıcıda başlatmak ve kolay bip sesi verin.</span><span class="sxs-lookup"><span data-stu-id="cdebc-161">When deployment completes, the script will launch the application in the browser and give you a friendly beep.</span></span>
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. <span data-ttu-id="cdebc-162">Geri Git Kabuk oturumunuzda çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="cdebc-162">Back in your Git Shell session, run:</span></span>

     <span data-ttu-id="cdebc-163">. \swap – adı ToDoApp < your_suffix ></span><span class="sxs-lookup"><span data-stu-id="cdebc-163">.\swap –Name ToDoApp<your_suffix></span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. <span data-ttu-id="cdebc-164">Komut tamamlandığında, ön uç'ın adresine göz atın dönün (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) üretimde çalışan uygulama görmek için.</span><span class="sxs-lookup"><span data-stu-id="cdebc-164">When the script finishes, go back to browse to the frontend’s address (http://ToDoApp*&lt;your_suffix>*.azurewebsites.net/) to see the application running in production.</span></span>
8. <span data-ttu-id="cdebc-165">İçine oturum [Azure Portal](https://portal.azure.com/) ve ne oluşturulan bir göz atalım.</span><span class="sxs-lookup"><span data-stu-id="cdebc-165">Log into the [Azure Portal](https://portal.azure.com/) and take a look at what’s created.</span></span>

   <span data-ttu-id="cdebc-166">Aynı kaynak grubunda biriyle iki web uygulamaları görmeye olmalıdır `Api` adı soneki.</span><span class="sxs-lookup"><span data-stu-id="cdebc-166">You should be able to see two web apps in the same resource group, one with the `Api` suffix in the name.</span></span> <span data-ttu-id="cdebc-167">Kaynak grubu görünümü bakarsanız, SQL veritabanı ve sunucu, uygulama hizmeti planı ve web uygulamaları için hazırlama yuvası görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="cdebc-167">If you look at the resource group view, you will also see the SQL Database and server, the App Service plan, and the staging slots for the web apps.</span></span> <span data-ttu-id="cdebc-168">Farklı kaynaklara göz atın ve bunlarla karşılaştırmak  *&lt;repository_root >*\ARMTemplates\ProdAndStage.json şablonda nasıl yapılandırıldıklarına bakın.</span><span class="sxs-lookup"><span data-stu-id="cdebc-168">Browse through the different resources and compare them with *&lt;repository_root>*\ARMTemplates\ProdAndStage.json to see how they are configured in the template.</span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

<span data-ttu-id="cdebc-169">Üretim uygulamasını ayarladınız.</span><span class="sxs-lookup"><span data-stu-id="cdebc-169">You have set up the production app.</span></span>  <span data-ttu-id="cdebc-170">Şimdi, şimdi uygulama için kullanılabilirlik zayıftır geri bildirim alma düşünün.</span><span class="sxs-lookup"><span data-stu-id="cdebc-170">Now, let's imagine that you receive feedback that usability is poor for the app.</span></span> <span data-ttu-id="cdebc-171">Bu nedenle, araştırmak karar verin.</span><span class="sxs-lookup"><span data-stu-id="cdebc-171">So you decide to investigate.</span></span> <span data-ttu-id="cdebc-172">Geribildirim vermek için uygulamayı izlemek oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="cdebc-172">You're going to instrument your app to give you feedback.</span></span>

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a><span data-ttu-id="cdebc-173">Araştırın: izleme izleme ölçümünün istemci uygulamanızı</span><span class="sxs-lookup"><span data-stu-id="cdebc-173">Investigate: Instrument your client app for monitoring/metrics</span></span>
1. <span data-ttu-id="cdebc-174">Açık  *&lt;repository_root >*\src\MultiChannelToDo.sln Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cdebc-174">Open *&lt;repository_root>*\src\MultiChannelToDo.sln in Visual Studio.</span></span>
2. <span data-ttu-id="cdebc-175">Çözüm sağ tıklayarak tüm Nuget paketlerini geri yüklemek > **çözüm için NuGet paketlerini Yönet** > **geri**.</span><span class="sxs-lookup"><span data-stu-id="cdebc-175">Restore all Nuget packages by right-clicking solution > **Manage NuGet Packages for Solution** > **Restore**.</span></span>
3. <span data-ttu-id="cdebc-176">Sağ **MultiChannelToDo.Web** > **Application Insights Telemetrisi Ekle** > **ayarlarını yapılandır** > ToDoApp değişiklik kaynak grubuna*&lt;your_suffix >* > **projeye Application Insights Ekle**.</span><span class="sxs-lookup"><span data-stu-id="cdebc-176">Right-click **MultiChannelToDo.Web** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group to ToDoApp*&lt;your_suffix>* > **Add Application Insights to Project**.</span></span>
4. <span data-ttu-id="cdebc-177">Azure Portalı'nda dikey penceresini açmak **MultiChannelToDo.Web** uygulama Insight kaynak.</span><span class="sxs-lookup"><span data-stu-id="cdebc-177">In the Azure Portal, open the blade for the **MultiChannelToDo.Web** Application Insight resource.</span></span> <span data-ttu-id="cdebc-178">Ardından **uygulama sistem** kısım, tıklatın **tarayıcı sayfa yükü veri toplamak öğrenin** > kodu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="cdebc-178">Then in the **Application health** part, click **Learn how to collect browser page load data** > copy code.</span></span>
5. <span data-ttu-id="cdebc-179">Kopyalanan JS araçları koda ekleyin  *&lt;repository_root >*kapatmadan önce yalnızca \src\MultiChannelToDo.Web\app\Index.cshtml `<heading>` etiketi.</span><span class="sxs-lookup"><span data-stu-id="cdebc-179">Add the copied JS instrumentation code to *&lt;repository_root>*\src\MultiChannelToDo.Web\app\Index.cshtml, just before the closing `<heading>` tag.</span></span> <span data-ttu-id="cdebc-180">Uygulama Insight kaynağınız benzersiz izleme anahtarını içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="cdebc-180">It should contain the unique instrumentation key of your Application Insight resource.</span></span>

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. <span data-ttu-id="cdebc-181">Özel olaylar için Application Insights için fare tıklatma gövde altına aşağıdaki kodu ekleyerek gönder:</span><span class="sxs-lookup"><span data-stu-id="cdebc-181">Send custom events to Application Insights for mouse clicks by adding the following code to the bottom of body:</span></span>

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   <span data-ttu-id="cdebc-182">Bir kullanıcı web uygulamasında her yerden, her zaman bu JavaScript kod parçacığı özel bir olay Application Insights'a gönderir.</span><span class="sxs-lookup"><span data-stu-id="cdebc-182">This JavaScript snippet sends a custom event to Application Insights every time a user clicks anywhere in the web app.</span></span>
7. <span data-ttu-id="cdebc-183">Git Kabuğu'nda yürütme ve değişikliklerinizi github, çatalı iletin.</span><span class="sxs-lookup"><span data-stu-id="cdebc-183">In Git Shell, commit and push your changes to your fork in GitHub.</span></span> <span data-ttu-id="cdebc-184">Daha sonra istemcilerin tarayıcıyı yenilemek için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="cdebc-184">Then, wait for clients to refresh browser.</span></span>

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. <span data-ttu-id="cdebc-185">Üretim dağıtılmış bir uygulamayı değişiklikleri değiştirme:</span><span class="sxs-lookup"><span data-stu-id="cdebc-185">Swap the deployed app changes to production:</span></span>

     <span data-ttu-id="cdebc-186">. \swap – adı ToDoApp < your_suffix ></span><span class="sxs-lookup"><span data-stu-id="cdebc-186">.\swap –Name ToDoApp<your_suffix></span></span>
9. <span data-ttu-id="cdebc-187">Yapılandırdığınız Application Insights kaynağı göz atın.</span><span class="sxs-lookup"><span data-stu-id="cdebc-187">Browse to the Application Insights resource that you configured.</span></span> <span data-ttu-id="cdebc-188">Özel olaylar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="cdebc-188">Click Custom events.</span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   <span data-ttu-id="cdebc-189">Özel olaylar için ölçümleri görmüyorsanız, birkaç dakika bekleyin ve tıklayın **yenileme**.</span><span class="sxs-lookup"><span data-stu-id="cdebc-189">If you don't see metrics for custom events, wait a few minutes and click **Refresh**.</span></span>

<span data-ttu-id="cdebc-190">Bir grafik gördüğünüz varsayalım ister altında:</span><span class="sxs-lookup"><span data-stu-id="cdebc-190">Suppose you see a chart like below:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

<span data-ttu-id="cdebc-191">Ve altındaki olay kılavuz:</span><span class="sxs-lookup"><span data-stu-id="cdebc-191">And the event grid below it:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

<span data-ttu-id="cdebc-192">ToDoApp uygulama kodunuz göre **düğmesini** olay gönderme düğmesi için karşılık gelen ve **giriş** olay metin kutusuna karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="cdebc-192">According to your ToDoApp application code, the **BUTTON** event corresponds to the submit button, and the **INPUT** event corresponds to the textbox.</span></span> <span data-ttu-id="cdebc-193">Şu ana kadar şeyler anlamlıdır.</span><span class="sxs-lookup"><span data-stu-id="cdebc-193">So far, things make sense.</span></span> <span data-ttu-id="cdebc-194">Ancak, iyi miktarını tıklar ve çok az tıklama yapılacak işler öğelerinde gibi görünür ( **LI** olayları).</span><span class="sxs-lookup"><span data-stu-id="cdebc-194">However, it looks like there's a good amount of clicks and very few clicks on the to-do items (the **LI** events).</span></span>

<span data-ttu-id="cdebc-195">Bu bilgisayarda, form tabanlı bazı kullanıcılar, varsayımınızın kullanıcı arabiriminin hangi bölümünün tıklanabilir kafası ve liste öğeleri ve simgelerine geldiğinde imleci için metin seçimi stilde olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="cdebc-195">Based on this, you form your hypothesis that some users are confused which part of the UI is clickable and it is because the cursor is styled for text selection when it hovers on the list items and their icons.</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

<span data-ttu-id="cdebc-196">Bu contrived bir örnek olabilir.</span><span class="sxs-lookup"><span data-stu-id="cdebc-196">This might be a contrived example.</span></span> <span data-ttu-id="cdebc-197">Bununla birlikte, uygulamanız için bir geliştirme yapmak ve canlı müşterilerden kullanılabilirlik geri bildirim almak için flighting bir dağıtım gerçekleştirin oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="cdebc-197">Nevertheless, you're going to make an improvement to your app, and then perform a flighting deployment to get usability feedback from live customers.</span></span>

### <a name="instrument-your-server-app-for-monitoringmetrics"></a><span data-ttu-id="cdebc-198">Sunucu uygulamanız için izleme ölçümleri izleme</span><span class="sxs-lookup"><span data-stu-id="cdebc-198">Instrument your server app for monitoring/metrics</span></span>
<span data-ttu-id="cdebc-199">Bu öğreticide gösterilen senaryo yalnızca istemci uygulaması ile ilgilenir bu yana bir tanjantını budur.</span><span class="sxs-lookup"><span data-stu-id="cdebc-199">This is a tangent since the scenario demonstrated in this tutorial only deals with the client app.</span></span> <span data-ttu-id="cdebc-200">Ancak, bütünlük açısından sunucu tarafı uygulama ayarlama.</span><span class="sxs-lookup"><span data-stu-id="cdebc-200">However, for completeness you will set up the server-side app.</span></span>

1. <span data-ttu-id="cdebc-201">Sağ **MultiChannelToDo** > **Application Insights Telemetrisi Ekle** > **ayarlarını yapılandır** > ToDoApp değişiklik kaynak grubuna*&lt;your_suffix >* > **projeye Application Insights Ekle**.</span><span class="sxs-lookup"><span data-stu-id="cdebc-201">Right-click **MultiChannelToDo** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group to ToDoApp*&lt;your_suffix>* > **Add Application Insights to Project**.</span></span>
2. <span data-ttu-id="cdebc-202">Git Kabuğu'nda yürütme ve değişikliklerinizi github, çatalı iletin.</span><span class="sxs-lookup"><span data-stu-id="cdebc-202">In Git Shell, commit and push your changes to your fork in GitHub.</span></span> <span data-ttu-id="cdebc-203">Daha sonra istemcilerin tarayıcıyı yenilemek için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="cdebc-203">Then, wait for clients to refresh browser.</span></span>

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. <span data-ttu-id="cdebc-204">Üretim dağıtılmış bir uygulamayı değişiklikleri değiştirme:</span><span class="sxs-lookup"><span data-stu-id="cdebc-204">Swap the deployed app changes to production:</span></span>

     <span data-ttu-id="cdebc-205">. \swap – adı ToDoApp < your_suffix ></span><span class="sxs-lookup"><span data-stu-id="cdebc-205">.\swap –Name ToDoApp<your_suffix></span></span>

<span data-ttu-id="cdebc-206">İşte bu kadar!</span><span class="sxs-lookup"><span data-stu-id="cdebc-206">That's it!</span></span>

## <a name="investigate-add-slot-specific-tags-to-your-client-app-metrics"></a><span data-ttu-id="cdebc-207">Araştırmak: istemci uygulama ölçümlerinizi yuva özel etiketler ekleyin</span><span class="sxs-lookup"><span data-stu-id="cdebc-207">Investigate: Add slot-specific tags to your client app metrics</span></span>
<span data-ttu-id="cdebc-208">Bu bölümde, yuva özel telemetri aynı Application Insights kaynağa göndermek için farklı dağıtım yuvası yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="cdebc-208">In this section, you will configure the different deployment slots to send slot-specific telemetry to the same Application Insights resource.</span></span> <span data-ttu-id="cdebc-209">Bu şekilde kolayca uygulama değişikliklerinizi etkisini görmek için farklı yuvaları (dağıtım ortamlarda) gelen trafiği arasında telemetri verileri karşılaştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdebc-209">This way, you can compare telemetry data between traffic from different slots (deployment environments) to easily see the effect of your app changes.</span></span> <span data-ttu-id="cdebc-210">Aynı anda gerektiğinde üretim uygulamanızı izlemek devam edebilmek için kalan kısmından üretim trafiği ayırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdebc-210">At the same time, you can separate the production traffic from the rest so you can continue to monitor your production app as needed.</span></span>

<span data-ttu-id="cdebc-211">İstemci davranışı verisi toplama olduğundan, şunları yapacaksınız [JavaScript kodunuzu bir telemetri başlatıcı ekleyin](../application-insights/app-insights-api-filtering-sampling.md) Index.cshtml içinde.</span><span class="sxs-lookup"><span data-stu-id="cdebc-211">Since you're gathering data on client behavior, you will [add a telemetry initializer to your JavaScript code](../application-insights/app-insights-api-filtering-sampling.md) in index.cshtml.</span></span> <span data-ttu-id="cdebc-212">Sunucu tarafı performansını test etmek isterseniz, örneğin, bunu da benzer şekilde, sunucu kodunuzda yapabilirsiniz (bkz [özel olayları ve ölçümleri için Application Insights API'si](../application-insights/app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="cdebc-212">If you want to test server-side performance, for example, you can also do similarly in your server code (see [Application Insights API for custom events and metrics](../application-insights/app-insights-api-custom-events-metrics.md).</span></span>

1. <span data-ttu-id="cdebc-213">İlk olarak, iki kod bewteen ekleyin `//` JavaScript aşağıda açıklamaları engellemek, eklenen `<heading>` daha önce etiketi.</span><span class="sxs-lookup"><span data-stu-id="cdebc-213">First, add the code bewteen the two `//` comments below in the JavaScript block that you added to the `<heading>` tag earlier.</span></span>

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

    <span data-ttu-id="cdebc-214">Bu Başlatıcı kod neden `appInsights` eklenecek nesne bir özel özellik adında `Environment` her parçasına telemetri gönderir.</span><span class="sxs-lookup"><span data-stu-id="cdebc-214">This initializer code causes the `appInsights` object to add the a custom property called `Environment` to every piece of telemetry it sends.</span></span>
2. <span data-ttu-id="cdebc-215">Ardından, bu özel özellik olarak ekleme bir [yuva ayarı](web-sites-staged-publishing.md#AboutConfiguration) azure'da web uygulamanız için.</span><span class="sxs-lookup"><span data-stu-id="cdebc-215">Next, add this custom property as a [slot setting](web-sites-staged-publishing.md#AboutConfiguration) for your web app in Azure.</span></span> <span data-ttu-id="cdebc-216">Bunu yapmak için Git Kabuk oturumunda aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cdebc-216">To do this, run the following commands in your Git Shell session.</span></span>

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    <span data-ttu-id="cdebc-217">Projenizdeki Web.config zaten tanımlar `environment` uygulama ayarı.</span><span class="sxs-lookup"><span data-stu-id="cdebc-217">The Web.config in your project already defines the `environment` app setting.</span></span> <span data-ttu-id="cdebc-218">Uygulamayı yerel olarak test ettiğinizde bu ayar, ölçümlerinizi ile Etiketlenecek `VS Debugger`.</span><span class="sxs-lookup"><span data-stu-id="cdebc-218">With this setting, when you test the app locally, your metrics will be tagged with `VS Debugger`.</span></span> <span data-ttu-id="cdebc-219">Değişikliklerinizi Azure'a gönderin, ancak Azure Bul kullanın ve `environment` web uygulamanızın yapılandırmasında bunun yerine ayarı uygulama ve ölçümlerinizi etiketli ile `Production`.</span><span class="sxs-lookup"><span data-stu-id="cdebc-219">However, when you push your changes to Azure, Azure will find and use the `environment` app setting in the web app's configuration instead, and your metrics will be tagged with `Production`.</span></span>
3. <span data-ttu-id="cdebc-220">Yürütme ve kod değişikliklerinizi GitHub üzerinde sayfanızı çatala gönderin ve yeni uygulamayı (tarayıcıyı yenilemek için gereklidir) kullanmak, kullanıcılarınız için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="cdebc-220">Commit and push your code changes to your fork on GitHub, and then wait for your users to use the new app (need to refresh the browser).</span></span> <span data-ttu-id="cdebc-221">Application Insights'ta gösterilmesini yeni özellik için yaklaşık 15 dakika sürer `MultiChannelToDo.Web` kaynak.</span><span class="sxs-lookup"><span data-stu-id="cdebc-221">It takes about 15 minutes for the new property to show up in your Application Insights `MultiChannelToDo.Web` resource.</span></span>

        git add -A :/
        git commit -m "add environment property to AI events for client app"
        git push origin master
4. <span data-ttu-id="cdebc-222">Şimdi, Git **özel olayları** dikey penceresini yeniden ve ölçümleri filtre `Environment=Production`.</span><span class="sxs-lookup"><span data-stu-id="cdebc-222">Now, go to the **Custom events** blade again and filter the metrics on `Environment=Production`.</span></span> <span data-ttu-id="cdebc-223">Şimdi bu filtre ile tüm yeni özel olayları üretim yuvasına görüyor olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="cdebc-223">You should now be able to see all the new custom events in the production slot with this filter.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. <span data-ttu-id="cdebc-224">Tıklatın **Sık Kullanılanlar** gibi bir geçerli ölçüm Gezgini ayarları kaydetmek için düğmesini **özel olayları: üretim**.</span><span class="sxs-lookup"><span data-stu-id="cdebc-224">Click the **Favorites** button to save the current Metrics Explorer settings to something like **Custom events: Production**.</span></span> <span data-ttu-id="cdebc-225">Kolayca bu görünümü ve bir dağıtım yuvası görünüm arasında daha sonra geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdebc-225">You can easily switch between this view and a deployment slot view later.</span></span>

   > [!TIP]
   > <span data-ttu-id="cdebc-226">Daha güçlü analytics için göz önünde bulundurun [Application Insights kaynağınıza Power BI ile tümleştirme](../application-insights/app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="cdebc-226">For even more powerful analytics, consider [integrating your Application Insights resource with Power BI](../application-insights/app-insights-export-power-bi.md).</span></span>
   >
   >

### <a name="add-slot-specific-tags-to-your-server-app-metrics"></a><span data-ttu-id="cdebc-227">Sunucu uygulaması ölçümlerinizi yuva özel etiketler ekleyin</span><span class="sxs-lookup"><span data-stu-id="cdebc-227">Add slot-specific tags to your server app metrics</span></span>
<span data-ttu-id="cdebc-228">Yeniden, bütünlük açısından sunucu tarafı uygulama ayarlama.</span><span class="sxs-lookup"><span data-stu-id="cdebc-228">Again, for completeness you will set up the server-side app.</span></span> <span data-ttu-id="cdebc-229">JavaScript'te izlenmiş olan istemci uygulaması yuvası özgü etiketler sunucu uygulaması için izlenmiş .NET koduyla.</span><span class="sxs-lookup"><span data-stu-id="cdebc-229">Unlike the client app which is instrumented in JavaScript, slot-specific tags for the server app is instrumented with .NET code.</span></span>

1. <span data-ttu-id="cdebc-230">Açık  *&lt;repository_root >*\src\MultiChannelToDo\Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="cdebc-230">Open *&lt;repository_root>*\src\MultiChannelToDo\Global.asax.cs.</span></span> <span data-ttu-id="cdebc-231">Aşağıdaki kod bloğu yalnızca kapatmadan önce eklemek ad alanı kaşlı ayraç.</span><span class="sxs-lookup"><span data-stu-id="cdebc-231">Add the code block below, just before the closing namespace curly brace.</span></span>

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
2. <span data-ttu-id="cdebc-232">Ekleyerek ad çözümleme hataları düzeltin `using` aşağıda dosyasının deyimleri başına:</span><span class="sxs-lookup"><span data-stu-id="cdebc-232">Correct the name resolution errors by adding the `using` statements below to the beginning of the file:</span></span>

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. <span data-ttu-id="cdebc-233">Aşağıdaki kodu ekleyin `Application_Start()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="cdebc-233">Add the code below to the beginning of the `Application_Start()` method:</span></span>

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. <span data-ttu-id="cdebc-234">Yürütme ve kod değişikliklerinizi GitHub üzerinde sayfanızı çatala gönderin ve yeni uygulamayı (tarayıcıyı yenilemek için gereklidir) kullanmak, kullanıcılarınız için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="cdebc-234">Commit and push your code changes to your fork on GitHub, and then wait for your users to use the new app (need to refresh the browser).</span></span> <span data-ttu-id="cdebc-235">Application Insights'ta gösterilmesini yeni özellik için yaklaşık 15 dakika sürer `MultiChannelToDo` kaynak.</span><span class="sxs-lookup"><span data-stu-id="cdebc-235">It takes about 15 minutes for the new property to show up in your Application Insights `MultiChannelToDo` resource.</span></span>

        git add -A :/
        git commit -m "add environment property to AI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a><span data-ttu-id="cdebc-236">Güncelleştirmesi: Beta dal ayarlama</span><span class="sxs-lookup"><span data-stu-id="cdebc-236">Update: Set up your beta branch</span></span>
1. <span data-ttu-id="cdebc-237">Açık  *&lt;repository_root >*\ARMTemplates\ProdAndStagetest.json ve bulma `appsettings` kaynakları (arama `"name": "appsettings"`).</span><span class="sxs-lookup"><span data-stu-id="cdebc-237">Open *&lt;repository_root>*\ARMTemplates\ProdAndStagetest.json and find the `appsettings` resources (search for `"name": "appsettings"`).</span></span> <span data-ttu-id="cdebc-238">Biri, her yuva için bir tane 4 vardır.</span><span class="sxs-lookup"><span data-stu-id="cdebc-238">There are 4 of them, one for each slot.</span></span>
2. <span data-ttu-id="cdebc-239">Her `appsettings` kaynak eklemek bir `"environment": "[parameters('slotName')]"` uygulama ayarı sonuna `properties` dizi.</span><span class="sxs-lookup"><span data-stu-id="cdebc-239">For each `appsettings` resource, add an  `"environment": "[parameters('slotName')]"` app setting to the end of the `properties` array.</span></span> <span data-ttu-id="cdebc-240">Virgül ile önceki satırın sonuna unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cdebc-240">Don't forget to end the previous line with a comma.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    <span data-ttu-id="cdebc-241">Eklemiş olduğunuz `environment` şablondaki tüm yuvalarına uygulama ayarı.</span><span class="sxs-lookup"><span data-stu-id="cdebc-241">You have just added the `environment` app setting to all the slots in the template.</span></span>
3. <span data-ttu-id="cdebc-242">Aynı dosyada Bul `slotconfignames` kaynakları (arama `"name": "slotconfignames"`).</span><span class="sxs-lookup"><span data-stu-id="cdebc-242">In the same file, find the `slotconfignames` resources (search for `"name": "slotconfignames"`).</span></span> <span data-ttu-id="cdebc-243">Her uygulama için bir tane bunların, 2 vardır.</span><span class="sxs-lookup"><span data-stu-id="cdebc-243">There are 2 of them, one for each app.</span></span>
4. <span data-ttu-id="cdebc-244">Her `slotconfignames` kaynak eklemek `"environment"` sonuna `appSettingNames` dizi.</span><span class="sxs-lookup"><span data-stu-id="cdebc-244">For each `slotconfignames` resource, add `"environment"` to the end of the `appSettingNames` array.</span></span> <span data-ttu-id="cdebc-245">Virgül ile önceki satırın sonuna unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cdebc-245">Don't forget to end the previous line with a comma.</span></span>

    <span data-ttu-id="cdebc-246">Yapmış olduğunuz `environment` uygulama çubuğu hem uygulamalar için kendi ilgili dağıtım yuvası için ayarlama.</span><span class="sxs-lookup"><span data-stu-id="cdebc-246">You have just made the `environment` app setting stick to its respective deployment slot for both apps.</span></span>  
5. <span data-ttu-id="cdebc-247">Git Kabuk oturumunuzda önce kullandığınız aynı kaynak grubu soneki aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cdebc-247">In your Git Shell session, run the following commands with the same resource group suffix that you used before.</span></span>

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. <span data-ttu-id="cdebc-248">İstendiğinde, aynı SQL veritabanı kimlik bilgileri olarak önce belirtin.</span><span class="sxs-lookup"><span data-stu-id="cdebc-248">When prompted, specify the same SQL database credentials as before.</span></span> <span data-ttu-id="cdebc-249">Sonra kaynak grubunu güncelleştirmek için sorulduğunda yazın `Y`, ardından `ENTER`.</span><span class="sxs-lookup"><span data-stu-id="cdebc-249">Then, when asked to update the resource group, type `Y`, then `ENTER`.</span></span>

    <span data-ttu-id="cdebc-250">Komut dosyası tamamlandıktan, özgün kaynak grubundaki tüm kaynaklarınızı korunur, ancak yeni bir yuva "beta" adlı bir kez içinde ' den itibaren oluşturuldu "Hazırlama" yuvası aynı yapılandırmaya sahip oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cdebc-250">Once the script finishes, all your resources in the original resource group are retained, but a new slot named "beta" is created in it with the same configuration as the "Staging" slot that was created in the beginning.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cdebc-251">Bu yöntem farklı dağıtım ortamları oluşturma yönteminden farklıdır [Azure App Service ile Çevik Yazılım Geliştirme](app-service-agile-software-development.md).</span><span class="sxs-lookup"><span data-stu-id="cdebc-251">This method of creating different deployment environments is different from the method in [Agile software development with Azure App Service](app-service-agile-software-development.md).</span></span> <span data-ttu-id="cdebc-252">Burada, beklenmediğini dağıtım ortamları kaynak gruplarıyla oluşturduğunuz dağıtım yuvası ile dağıtım ortamlar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cdebc-252">Here, you create deployment environments with deployment slots, where as there you create deployment environments with resource groups.</span></span> <span data-ttu-id="cdebc-253">Dağıtım ortamları kaynak grupları ile yönetme, üretim ortamı için geliştiricilere off-limits olmanızı sağlar, ancak yuvası ile kolayca yapabilirsiniz üretim testi yapmak kolay değildir.</span><span class="sxs-lookup"><span data-stu-id="cdebc-253">Managing deployment environments with resource groups enables you to keep the production environment off-limits to developers, but it's not easy to do testing in production, which you can do easily with slots.</span></span>
   >
   >

<span data-ttu-id="cdebc-254">İsterseniz, ayrıca bir alfa uygulamayı çalıştırarak oluşturabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cdebc-254">If you wish, you can also create an alpha app by running</span></span>

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

<span data-ttu-id="cdebc-255">Bu öğretici için yalnızca beta uygulamanızı kullanmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="cdebc-255">For this tutorial, you will just keep using your beta app.</span></span>

## <a name="update-push-your-updates-to-the-beta-app"></a><span data-ttu-id="cdebc-256">Güncelleştirme: güncelleştirmelerinizi beta uygulamasına anında iletme</span><span class="sxs-lookup"><span data-stu-id="cdebc-256">Update: Push your updates to the beta app</span></span>
<span data-ttu-id="cdebc-257">İyileştirmek istediğiniz geri uygulamanıza.</span><span class="sxs-lookup"><span data-stu-id="cdebc-257">Back to your app that you want to improve.</span></span>

1. <span data-ttu-id="cdebc-258">Şimdi, beta dalında olduğunuzdan emin olun</span><span class="sxs-lookup"><span data-stu-id="cdebc-258">Make sure you're now in your beta branch</span></span>

        git checkout beta
2. <span data-ttu-id="cdebc-259">İçinde  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, bulma `<li>` etiketi ve ekleme `style="cursor:pointer"` , aşağıda gösterildiği gibi özniteliği.</span><span class="sxs-lookup"><span data-stu-id="cdebc-259">In *&lt;repository_root>*\src\MultiChannelToDo.Web\app\Index.cshtml, find the `<li>` tag and add the `style="cursor:pointer"` attribute, as shown below.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. <span data-ttu-id="cdebc-260">yürütme ve azure'a gönderin.</span><span class="sxs-lookup"><span data-stu-id="cdebc-260">commit and push to Azure.</span></span>
4. <span data-ttu-id="cdebc-261">Bu değişiklik şimdi beta yuvasında için http://todoapp giderek yansıtılır doğrulayın*&lt;your_suffix >*-beta.azurewebsites.net/.</span><span class="sxs-lookup"><span data-stu-id="cdebc-261">Verify that the change is now reflected in the beta slot by navigating to http://todoapp*&lt;your_suffix>*-beta.azurewebsites.net/.</span></span> <span data-ttu-id="cdebc-262">Değişiklik henüz görmüyorsanız, yeni javascript kodu almak için tarayıcınızı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="cdebc-262">If you don't see the change yet, refresh your browser to get the new javascript code.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

<span data-ttu-id="cdebc-263">Beta yuvasında çalıştıran değişikliğinizin sahip olduğunuza göre flighting dağıtım gerçekleştirmek hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="cdebc-263">Now that you have your change running in the beta slot, you are ready to perform a flighting deployment.</span></span>

## <a name="validate-route-traffic-to-the-beta-app"></a><span data-ttu-id="cdebc-264">Doğrulama: Beta uygulamasına yolu trafiğini</span><span class="sxs-lookup"><span data-stu-id="cdebc-264">Validate: Route traffic to the beta app</span></span>
<span data-ttu-id="cdebc-265">Bu bölümde, beta uygulamaya trafiğini yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="cdebc-265">In this section, you will route traffic to the beta app.</span></span> <span data-ttu-id="cdebc-266">For sake of daha anlaşılır olması, tanıtım kullanıcı trafiğinin önemli bir kısmını yönlendirmekte paylaşacağız.</span><span class="sxs-lookup"><span data-stu-id="cdebc-266">For sake of clarity of demonstration, you're going to route a significant portion of the user traffic to it.</span></span> <span data-ttu-id="cdebc-267">Gerçekte, yönlendirmek istediğiniz trafik miktarı belirli durumunuza bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="cdebc-267">In reality, the amount of traffic you want to route will depend on your specific situation.</span></span> <span data-ttu-id="cdebc-268">Sitenizi microsoft.com ölçekte ise, örneğin, daha sonra toplam trafiğin yüzde biri'den az yararlı veri sağlamak için gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="cdebc-268">For example, if your site is at the scale of microsoft.com, then you may need less than one percent of your total traffic in order to gain useful data.</span></span>

1. <span data-ttu-id="cdebc-269">Git Kabuk oturumunuzda, beta yuvaya yarısı üretim trafiği yönlendirmek için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="cdebc-269">In your Git Shell session, run the following commands to route half of the production traffic to the beta slot:</span></span>

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   <span data-ttu-id="cdebc-270">`ReroutePercentage=50` Özelliği, üretim trafiği % 50'si beta uygulamanızın URL'sine yönlendirilir belirtir (tarafından belirtilen `ActionHostName` özelliği).</span><span class="sxs-lookup"><span data-stu-id="cdebc-270">The `ReroutePercentage=50` property specifies that 50% of the production traffic will be routed to the beta app's URL (specified by the `ActionHostName` property).</span></span>
2. <span data-ttu-id="cdebc-271">Şimdi http://ToDoApp için gidin*&lt;your_suffix >*. azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="cdebc-271">Now navigate to http://ToDoApp*&lt;your_suffix>*.azurewebsites.net.</span></span> <span data-ttu-id="cdebc-272">% 50'trafiğin şimdi beta yuvaya yönlendirilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cdebc-272">50% of the traffic should now be redirected to the beta slot.</span></span>
3. <span data-ttu-id="cdebc-273">Application Insights kaynağınıza ölçümleri ortamı tarafından filtre "beta" =.</span><span class="sxs-lookup"><span data-stu-id="cdebc-273">In your Application Insights resource, filter the metrics by environment="beta".</span></span>

   > [!NOTE]
   > <span data-ttu-id="cdebc-274">Bu filtre uygulanmış bir görünüm başka bir sık kullanılan olarak kaydederseniz ölçüm Gezgini Görünüm üretim ve beta görünümler arasında kolayca çevirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdebc-274">If you save this filtered view as another favorite, then you can easily flip the metric explorer views between production and beta views.</span></span>
   >
   >

<span data-ttu-id="cdebc-275">Application Insights'ta, aşağıdakine benzer bir şey görürsünüz varsayın:</span><span class="sxs-lookup"><span data-stu-id="cdebc-275">Suppose in Application Insights you see something similar to the following:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

<span data-ttu-id="cdebc-276">Yalnızca bu olduğunu üzerinde çok daha fazla tıklama gösteriyor `<li>` etiketleri olduğu anlaşılıyor ancak üzerinde ani artışı işleme tıklama olmasını `<li>` etiketler.</span><span class="sxs-lookup"><span data-stu-id="cdebc-276">Not only is this showing that there are many more clicks on the `<li>` tags, but there seems to be a surge of clicks on `<li>` tags.</span></span> <span data-ttu-id="cdebc-277">Ardından kişiler yeni bulunmuş tamamlanabilmesi `<li>` etiketleri tıklanabilir ve tüm daha önce tamamlandı görevlerini uygulamasında artık temizleme.</span><span class="sxs-lookup"><span data-stu-id="cdebc-277">You can then conclude that people have discovered the new `<li>` tags are clickable and are now clearing all their previously-completed tasks in the app.</span></span>

<span data-ttu-id="cdebc-278">Flighting dağıtımınızı verilerini temel alarak yeni UI üretime hazır olduğuna karar verin.</span><span class="sxs-lookup"><span data-stu-id="cdebc-278">Based on the data of your flighting deployment, you decide that your new UI is ready for production.</span></span>

## <a name="go-live-move-your-new-code-into-production"></a><span data-ttu-id="cdebc-279">Canlı gidin: yeni kodunuzu üretim ortamına taşıyın</span><span class="sxs-lookup"><span data-stu-id="cdebc-279">Go live: Move your new code into production</span></span>
<span data-ttu-id="cdebc-280">Artık güncelleştirmenizi üretime taşımak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="cdebc-280">You're now ready to move your update to production.</span></span> <span data-ttu-id="cdebc-281">Artık güncelleştirmenizi zaten doğrulandı biliyorsunuz harika nedir olan *önce* üretime gönderilir.</span><span class="sxs-lookup"><span data-stu-id="cdebc-281">What's great is that now you know that your update has already been validated *before* it is pushed to production.</span></span> <span data-ttu-id="cdebc-282">Artık bunu güvenle dağıtabilir.</span><span class="sxs-lookup"><span data-stu-id="cdebc-282">So now you can confidently deploy it.</span></span> <span data-ttu-id="cdebc-283">AngularJS istemci uygulamaları için bir güncelleştirme yapılan olduğundan, yalnızca istemci tarafında kodu doğrulandı.</span><span class="sxs-lookup"><span data-stu-id="cdebc-283">Since you made an update to the AngularJS client app, you only validated the client-side code.</span></span> <span data-ttu-id="cdebc-284">Arka uç Web API uygulamasına değişiklik yapmak için olsaydı, değişikliklerinizi benzer şekilde ve kolayca doğrulamak.</span><span class="sxs-lookup"><span data-stu-id="cdebc-284">If you were to make changes to the back-end Web API app, you could validate your changes similarly and easily.</span></span>

1. <span data-ttu-id="cdebc-285">Git Kabuğu'nda, aşağıdaki komutu çalıştırarak trafik yönlendirme kuralı kaldırın:</span><span class="sxs-lookup"><span data-stu-id="cdebc-285">In Git Shell, remove the traffic routing rule by running the following command:</span></span>

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. <span data-ttu-id="cdebc-286">Git komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="cdebc-286">Run the Git commands:</span></span>

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. <span data-ttu-id="cdebc-287">Hazırlama yuvasını dağıtılacak yeni kodu için bir kaç dakika bekleyin, sonra http://ToDoApp başlatma*&lt;your_suffix >*-staging.azurewebsites.net yeni güncelleştirme hazırlama yuvası warmed olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="cdebc-287">Wait for a few minutes for the new code to be deployed to the staging slot, then launch http://ToDoApp*&lt;your_suffix>*-staging.azurewebsites.net to verify that the new update is warmed up in the staging slot.</span></span> <span data-ttu-id="cdebc-288">Unutmayın, uygulamanızın hazırlama yuvasını çatalı ait ana dala bağlı.</span><span class="sxs-lookup"><span data-stu-id="cdebc-288">Remember that the your fork's master branch is linked to the staging slot of your app.</span></span>
4. <span data-ttu-id="cdebc-289">Şimdi, üretime hazırlama yuvası takas</span><span class="sxs-lookup"><span data-stu-id="cdebc-289">Now, swap the staging slot into production</span></span>

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a><span data-ttu-id="cdebc-290">Özet</span><span class="sxs-lookup"><span data-stu-id="cdebc-290">Summary</span></span>
<span data-ttu-id="cdebc-291">Azure uygulama hizmeti bir şey üretimde müşterilerle uygulamalarını test etmek küçük - için orta ölçekli işletmeler için geleneksel olarak yapılan büyük kuruluşlarda kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="cdebc-291">Azure App Service makes it easy for small- to medium-sized businesses to test their customer-facing apps in production, something that has been traditionally done in big enterprises.</span></span> <span data-ttu-id="cdebc-292">Neyse ki bu öğretici, App Service ve Application Insights olası flighting dağıtım ve hatta diğer test üretimde senaryoları DevOps dünyada yapmak için bir araya getirme gerek bilgi verdiği.</span><span class="sxs-lookup"><span data-stu-id="cdebc-292">Hopefully, this tutorial has given you the knowledge you need to bring together App Service and Application Insights to make possible flighting deployment, and even other test-in-production scenarios, in your DevOps world.</span></span>

## <a name="more-resources"></a><span data-ttu-id="cdebc-293">Diğer kaynaklar</span><span class="sxs-lookup"><span data-stu-id="cdebc-293">More resources</span></span>
* [<span data-ttu-id="cdebc-294">Azure App Service ile Çevik Yazılım Geliştirme</span><span class="sxs-lookup"><span data-stu-id="cdebc-294">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)
* [<span data-ttu-id="cdebc-295">Hazırlık ortamları için Azure App Service'te web uygulamalarını ayarlama</span><span class="sxs-lookup"><span data-stu-id="cdebc-295">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)
* [<span data-ttu-id="cdebc-296">Azure'nın beklendiği karmaşık bir uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="cdebc-296">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="cdebc-297">Azure Resource Manager şablonları yazma</span><span class="sxs-lookup"><span data-stu-id="cdebc-297">Authoring Azure Resource Manager Templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="cdebc-298">JSONLint - JSON Doğrulayıcı</span><span class="sxs-lookup"><span data-stu-id="cdebc-298">JSONLint - The JSON Validator</span></span>](http://jsonlint.com/)
* [<span data-ttu-id="cdebc-299">Git dallanma – temel dallandırma ve birleştirme</span><span class="sxs-lookup"><span data-stu-id="cdebc-299">Git Branching – Basic Branching and Merging</span></span>](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [<span data-ttu-id="cdebc-300">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cdebc-300">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="cdebc-301">Proje Kudu Wiki</span><span class="sxs-lookup"><span data-stu-id="cdebc-301">Project Kudu Wiki</span></span>](https://github.com/projectkudu/kudu/wiki)
