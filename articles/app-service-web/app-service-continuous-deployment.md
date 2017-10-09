---
title: "aaaContinuous dağıtım tooAzure App Service | Microsoft Docs"
description: "Bilgi nasıl tooenable sürekli dağıtım tooAzure uygulama hizmeti."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 62a22cbda354fd5b0a1b9729c8c375408e75049f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-tooazure-app-service"></a><span data-ttu-id="b9ba6-103">Sürekli dağıtım tooAzure uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="b9ba6-103">Continuous Deployment tooAzure App Service</span></span>
<span data-ttu-id="b9ba6-104">Bu öğretici şunların nasıl yapıldığını gösterir tooconfigure sürekli dağıtımı iş akışı için [Azure App Service] uygulama.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-104">This tutorial shows you how tooconfigure a continuous deployment workflow for your [Azure App Service] app.</span></span> <span data-ttu-id="b9ba6-105">BitBucket, GitHub, uygulama hizmeti tümleşme ve [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) bir sürekli etkinleştirir hello en son güncelleştirmeleri projenizden Azure burada çekmesi dağıtımı iş akışı yayımlanan bu hizmetlerin tooone.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-105">App Service integration with BitBucket, GitHub, and [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) enables a continuous deployment workflow where Azure pulls in hello most recent updates from your project published tooone of these services.</span></span> <span data-ttu-id="b9ba6-106">Sürekli dağıtım, birden fazla ve sık gerçekleşen katkıların tümleştirildiği projeler için mükemmel bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-106">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span>

<span data-ttu-id="b9ba6-107">nasıl tooconfigure sürekli dağıtım depodan tarafından listelenmeyen el ile bir bulut hello Azure Portal çıkışı toofind (gibi [GitLab](https://gitlab.com/)), bkz: [el ile adımları kullanarak sürekli dağıtım ayarı](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span><span class="sxs-lookup"><span data-stu-id="b9ba6-107">toofind out how tooconfigure continuous deployment manually from a cloud repository not listed by hello Azure Portal (such as [GitLab](https://gitlab.com/)), see [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span></span>

## <span data-ttu-id="b9ba6-108"><a name="overview"></a>Sürekli dağıtımı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="b9ba6-108"><a name="overview"></a>Enable continuous deployment</span></span>
<span data-ttu-id="b9ba6-109">tooenable sürekli dağıtım</span><span class="sxs-lookup"><span data-stu-id="b9ba6-109">tooenable continuous deployment,</span></span>

1. <span data-ttu-id="b9ba6-110">Sürekli dağıtım için kullanılacak olan uygulama içerik toohello deponuza yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-110">Publish your app content toohello repository that will be used for continuous deployment.</span></span>  
    <span data-ttu-id="b9ba6-111">Proje toothese hizmetlerinizi yayımlama ile ilgili daha fazla bilgi için bkz: [deposu (GitHub) oluşturma], [deposu (BitBucket) oluşturma], ve [VSTS ile çalışmaya başlama].</span><span class="sxs-lookup"><span data-stu-id="b9ba6-111">For more information on publishing your project toothese services, see [Create a repo (GitHub)], [Create a repo (BitBucket)], and [Get started with VSTS].</span></span>
2. <span data-ttu-id="b9ba6-112">Uygulamanızın menü dikey penceresinde hello içinde [Azure portal], tıklatın **uygulama dağıtımı > Dağıtım Seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-112">In your app's menu blade in hello [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="b9ba6-113">Tıklatın **Kaynağı Seç**seçeneğini belirleyip hello dağıtım kaynağı.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-113">Click **Choose Source**, then select hello deployment source.</span></span>  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > <span data-ttu-id="b9ba6-114">tooconfigure VSTS hesap uygulama hizmeti dağıtımı için lütfen bkz. Bu [Öğreticisi](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span><span class="sxs-lookup"><span data-stu-id="b9ba6-114">tooconfigure a VSTS account for App Service deployment please see this [tutorial](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span></span>
   > 
   > 
3. <span data-ttu-id="b9ba6-115">Merhaba yetkilendirme iş akışı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-115">Complete hello authorization workflow.</span></span>
4. <span data-ttu-id="b9ba6-116">Merhaba, **dağıtım kaynağı** dikey penceresinde hello projesini seçin ve dal gelen toodeploy.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-116">In hello **Deployment source** blade, choose hello project and branch toodeploy from.</span></span> <span data-ttu-id="b9ba6-117">İşiniz bittiğinde, **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-117">When you're done, click **OK**.</span></span>
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > <span data-ttu-id="b9ba6-118">GitHub veya BitBucket ile sürekli dağıtımı etkinleştirirken hem genel hem de özel projeler gösterilir.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-118">When enabling continuous deployment with GitHub or BitBucket, both public and private projects will be displayed.</span></span>
   > 
   > 
   
    <span data-ttu-id="b9ba6-119">Uygulama hizmeti hello seçili deposu ile ilişkilendirir, hello belirtilen şube hello dosyalarından çeker ve deponuz App Service uygulamanız için bir kopyasını tutar.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-119">App Service creates an association with hello selected repository, pulls in hello files from hello specified branch, and maintains a clone of your repository for your App Service app.</span></span> <span data-ttu-id="b9ba6-120">VSTS hello Azure portalı sürekli dağıtımı yapılandırdığınızda hello tümleştirme hello uygulama hizmeti kullanan [Kudu dağıtım altyapısı](https://github.com/projectkudu/kudu/wiki), hangi zaten ile derleme ve dağıtım görevleri otomatikleştiren her `git push`.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-120">When you configure VSTS continuous deployment from hello Azure portal, hello integration uses hello App Service [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki), which already automates build and deployment tasks with every `git push`.</span></span> <span data-ttu-id="b9ba6-121">Tooseparately gerekmez VSTS sürekli dağıtım ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-121">You do not need tooseparately set up continuous deployment in VSTS.</span></span> <span data-ttu-id="b9ba6-122">Bu işlem, hello tamamlandıktan sonra **dağıtım seçenekleri** uygulaması dikey dağıtım belirten etkin dağıtımı başarılı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-122">After this process completes, hello **Deployment options** app blade will show an active deployment that indicates deployment has succeeded.</span></span>
5. <span data-ttu-id="b9ba6-123">tooverify hello uygulama başarıyla dağıtıldığından, hello tıklatın **URL** hello uygulamanızın dikey penceresinde hello Azure portal hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-123">tooverify hello app is successfully deployed, click hello **URL** at hello top of hello app's blade in hello Azure portal.</span></span>
6. <span data-ttu-id="b9ba6-124">sürekli dağıtım tercih ettiğiniz hello depodan oluştuğunu tooverify bir değişiklik toohello deposu iletin.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-124">tooverify that continuous deployment is occurring from hello repository of your choice, push a change toohello repository.</span></span> <span data-ttu-id="b9ba6-125">Kısa süre içinde hello itme toohello depo tamamlandıktan sonra uygulamanızı tooreflect hello değişiklikleri güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-125">Your app should update tooreflect hello changes shortly after hello push toohello repository completes.</span></span> <span data-ttu-id="b9ba6-126">Merhaba hello güncelleştirmedeki çekilen doğrulayabilirsiniz **dağıtım seçenekleri** dikey penceresinde uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-126">You can verify that it has pulled in hello update in hello **Deployment options** blade of your app.</span></span>

## <span data-ttu-id="b9ba6-127"><a name="VSsolution"></a>Visual Studio çözümünün sürekli dağıtımı</span><span class="sxs-lookup"><span data-stu-id="b9ba6-127"><a name="VSsolution"></a>Continuous deployment of a Visual Studio solution</span></span>
<span data-ttu-id="b9ba6-128">Visual Studio çözümü tooAzure uygulama hizmeti Ftp'den basit index.html dosya itme olarak oldukça kolaydır.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-128">Pushing a Visual Studio solution tooAzure App Service is just as easy as pushing a simple index.html file.</span></span> <span data-ttu-id="b9ba6-129">Merhaba uygulama hizmeti dağıtım işlemi NuGet bağımlılıkları geri yükleme ve hello uygulama ikili dosyaları oluşturma dahil olmak üzere tüm hello ayrıntıları kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-129">hello App Service deployment process streamlines all hello details, including restoring NuGet dependencies and building hello application binaries.</span></span> <span data-ttu-id="b9ba6-130">Git deponuz yalnızca kodda sürdürme hello kaynak denetimi en iyi uygulamaları izleyin ve uygulama hizmeti dağıtım ilgilenebilmek hello geri kalanı sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-130">You can follow hello source control best practices of maintaining code only in your Git repository, and let App Service deployment take care of hello rest.</span></span>

<span data-ttu-id="b9ba6-131">Merhaba, Visual Studio çözümü tooApp hizmet gönderilmesi için adımları aynı olduğu gibi hello hello [önceki bölümde](#overview), çözümünüz ve depo gibi yapılandırmanız koşuluyla:</span><span class="sxs-lookup"><span data-stu-id="b9ba6-131">hello steps for pushing your Visual Studio solution tooApp Service are hello same as in hello [previous section](#overview), provided that you configure your solution and repository as follows:</span></span>

* <span data-ttu-id="b9ba6-132">Merhaba Visual Studio kaynak denetim seçeneği toogenerate kullanmak bir `.gitignore` dosya aşağıdaki hello görüntü gibi veya el ile eklemeniz bir `.gitignore` içerik benzer toothis ile depo kök dosyasında [.gitignore örnek](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="b9ba6-132">Use hello Visual Studio source control option toogenerate a `.gitignore` file such as hello image below or manually add a `.gitignore` file in your repository root with content similar toothis [.gitignore sample](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* <span data-ttu-id="b9ba6-133">Merhaba tüm çözümün dizin ağacında tooyour depo hello depo kök hello .sln dosyasını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-133">Add hello entire solution's directory tree tooyour repository, with hello .sln file in hello repository root.</span></span>

<span data-ttu-id="b9ba6-134">Deponuz açıklandığı ayarlayın ve uygulamanızı sürekli yayımlama hello çevrimiçi Git depoları birinden Azure içinde yapılandırılmış sonra ASP.NET uygulamanızı yerel olarak Visual Studio'da geliştirme ve sürekli olarak kodunuzu yalnızca göre dağıtma değişiklikleri tooyour çevrimiçi Git deponuzu Ftp'den.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-134">Once you have set up your repository as described, and configured your app in Azure for continuous publishing from one of hello online Git repositories, you can develop your ASP.NET application locally in Visual Studio and continuously deploy your code simply by pushing your changes tooyour online Git repository.</span></span>

## <span data-ttu-id="b9ba6-135"><a name="disableCD"></a>Sürekli dağıtımı devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="b9ba6-135"><a name="disableCD"></a>Disable continuous deployment</span></span>
<span data-ttu-id="b9ba6-136">toodisable sürekli dağıtım</span><span class="sxs-lookup"><span data-stu-id="b9ba6-136">toodisable continuous deployment,</span></span>

1. <span data-ttu-id="b9ba6-137">Uygulamanızın menü dikey penceresinde hello içinde [Azure portal], tıklatın **uygulama dağıtımı > Dağıtım Seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-137">In your app's menu blade in hello [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="b9ba6-138">Ardından **Bağlantıyı Kes** hello içinde **dağıtım seçenekleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-138">Then click **Disconnect** in hello **Deployment options** blade.</span></span>
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. <span data-ttu-id="b9ba6-139">Yanıtlama sonra **Evet** toohello onay iletisi tooyour uygulamanızın dikey dönün ve tıklatın **uygulama dağıtımı > Dağıtım Seçenekleri** tooset başka bir kaynaktan yayımlamayı istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-139">After answering **Yes** toohello confirmation message, you can return tooyour app's blade and click **APP DEPLOYMENT > Deployment options** if you would like tooset up publishing from another source.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b9ba6-140">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b9ba6-140">Additional Resources</span></span>
* [<span data-ttu-id="b9ba6-141">İle sürekli dağıtımın nasıl tooinvestigate ortak sorunları</span><span class="sxs-lookup"><span data-stu-id="b9ba6-141">How tooinvestigate common issues with continuous deployment</span></span>](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* <span data-ttu-id="b9ba6-142">[Nasıl toouse Azure PowerShell]</span><span class="sxs-lookup"><span data-stu-id="b9ba6-142">[How toouse PowerShell for Azure]</span></span>
* <span data-ttu-id="b9ba6-143">[Nasıl toouse hello Azure komut satırı araçları Mac ve Linux için]</span><span class="sxs-lookup"><span data-stu-id="b9ba6-143">[How toouse hello Azure Command-Line Tools for Mac and Linux]</span></span>
* <span data-ttu-id="b9ba6-144">[Git belgeleri]</span><span class="sxs-lookup"><span data-stu-id="b9ba6-144">[Git documentation]</span></span>
* [<span data-ttu-id="b9ba6-145">Kudu Projesi</span><span class="sxs-lookup"><span data-stu-id="b9ba6-145">Project Kudu</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="b9ba6-146">Azure kullanmak tooautomatically bir CI/CD ardışık düzen toodeploy ASP.NET 4 uygulaması oluştur</span><span class="sxs-lookup"><span data-stu-id="b9ba6-146">Use Azure tooautomatically generate a CI/CD pipeline toodeploy an ASP.NET 4 app</span></span>](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> <span data-ttu-id="b9ba6-147">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-147">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b9ba6-148">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b9ba6-148">No credit cards required; no commitments.</span></span>
> 
> 

[Azure App Service]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[Azure portal]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Nasıl toouse Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Nasıl toouse hello Azure komut satırı araçları Mac ve Linux için]:../cli-install-nodejs.md
[Git Belgeleri]: http://git-scm.com/documentation

[deposu (GitHub) oluşturma]: https://help.github.com/articles/create-a-repo
[deposu (BitBucket) oluşturma]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[VSTS ile çalışmaya başlama]: https://www.visualstudio.com/docs/vsts-tfs-overview
