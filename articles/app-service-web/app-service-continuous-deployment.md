---
title: "Azure uygulama hizmeti için sürekli dağıtım | Microsoft Docs"
description: "Azure Uygulama Hizmeti’ne sürekli dağıtımı etkinleştirme hakkında bilgi edinin."
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
ms.openlocfilehash: 7d978e623aaff25a9400090bd3ac18ed560d2ebf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="continuous-deployment-to-azure-app-service"></a><span data-ttu-id="1b71a-103">Azure Uygulama Hizmeti’ne Sürekli Dağıtım</span><span class="sxs-lookup"><span data-stu-id="1b71a-103">Continuous Deployment to Azure App Service</span></span>
<span data-ttu-id="1b71a-104">Bu öğreticide [Azure Uygulama Hizmeti] uygulamanız için sürekli dağıtım iş akışını yapılandırma işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="1b71a-104">This tutorial shows you how to configure a continuous deployment workflow for your [Azure App Service] app.</span></span> <span data-ttu-id="1b71a-105">BitBucket, GitHub, uygulama hizmeti tümleşme ve [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) projenizden en son güncelleştirmeleri Azure burada çekmesi sürekli dağıtım iş akışı yayımlanan Bu hizmetlerden biri için etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="1b71a-105">App Service integration with BitBucket, GitHub, and [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) enables a continuous deployment workflow where Azure pulls in the most recent updates from your project published to one of these services.</span></span> <span data-ttu-id="1b71a-106">Sürekli dağıtım, birden fazla ve sık gerçekleşen katkıların tümleştirildiği projeler için mükemmel bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="1b71a-106">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span>

<span data-ttu-id="1b71a-107">El ile Azure Portal tarafından listelenmeyen bir bulut deposu sürekli dağıtımını yapılandırmak nasıl öğrenmek için (gibi [GitLab](https://gitlab.com/)), bkz: [el ile adımları kullanarak sürekli dağıtım ayarı](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span><span class="sxs-lookup"><span data-stu-id="1b71a-107">To find out how to configure continuous deployment manually from a cloud repository not listed by the Azure Portal (such as [GitLab](https://gitlab.com/)), see [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span></span>

## <span data-ttu-id="1b71a-108"><a name="overview"></a>Sürekli dağıtımı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="1b71a-108"><a name="overview"></a>Enable continuous deployment</span></span>
<span data-ttu-id="1b71a-109">Sürekli dağıtımı etkinleştirmek için,</span><span class="sxs-lookup"><span data-stu-id="1b71a-109">To enable continuous deployment,</span></span>

1. <span data-ttu-id="1b71a-110">Uygulamanızın içeriğini sürekli dağıtım için kullanılacak depoda yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="1b71a-110">Publish your app content to the repository that will be used for continuous deployment.</span></span>  
    <span data-ttu-id="1b71a-111">Projenizi bu hizmetlerde yayımlama hakkında daha fazla bilgi için bkz. [Depo oluşturma (GitHub)], [Depo oluşturma (BitBucket)] ve [VSTS kullanmaya başlama].</span><span class="sxs-lookup"><span data-stu-id="1b71a-111">For more information on publishing your project to these services, see [Create a repo (GitHub)], [Create a repo (BitBucket)], and [Get started with VSTS].</span></span>
2. <span data-ttu-id="1b71a-112">Uygulamanızın [Azure Portal] menü dikey penceresinde **UYGULAMA DAĞITIMI > Dağıtım seçenekleri**’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1b71a-112">In your app's menu blade in the [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="1b71a-113">**Kaynak Seç**’e tıklayın, ardından dağıtım kaynağını seçin.</span><span class="sxs-lookup"><span data-stu-id="1b71a-113">Click **Choose Source**, then select the deployment source.</span></span>  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > <span data-ttu-id="1b71a-114">Uygulama Hizmeti dağıtımına yönelik bir VSTS hesabı yapılandırmak için lütfen bu [öğreticiye](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App) bakın.</span><span class="sxs-lookup"><span data-stu-id="1b71a-114">To configure a VSTS account for App Service deployment please see this [tutorial](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span></span>
   > 
   > 
3. <span data-ttu-id="1b71a-115">Yetkilendirme iş akışını tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="1b71a-115">Complete the authorization workflow.</span></span>
4. <span data-ttu-id="1b71a-116">**Dağıtım kaynağı** dikey penceresinde dağıtımın yapılacağı projeyi ve dalı seçin.</span><span class="sxs-lookup"><span data-stu-id="1b71a-116">In the **Deployment source** blade, choose the project and branch to deploy from.</span></span> <span data-ttu-id="1b71a-117">İşiniz bittiğinde, **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1b71a-117">When you're done, click **OK**.</span></span>
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > <span data-ttu-id="1b71a-118">GitHub veya BitBucket ile sürekli dağıtımı etkinleştirirken hem genel hem de özel projeler gösterilir.</span><span class="sxs-lookup"><span data-stu-id="1b71a-118">When enabling continuous deployment with GitHub or BitBucket, both public and private projects will be displayed.</span></span>
   > 
   > 
   
    <span data-ttu-id="1b71a-119">Uygulama Hizmeti seçili depo ile bir ilişki oluşturur, belirtilen daldan dosyaları seçer ve deponuzun bir kopyasını Uygulama Hizmeti uygulamasında tutar.</span><span class="sxs-lookup"><span data-stu-id="1b71a-119">App Service creates an association with the selected repository, pulls in the files from the specified branch, and maintains a clone of your repository for your App Service app.</span></span> <span data-ttu-id="1b71a-120">Azure portalında VSTS sürekli dağıtımını yapılandırdığınızda tümleştirme, her `git push` ile derleme ve dağıtım görevini otomatik hale getiren Uygulama Hizmeti [Kudu dağıtım altyapısını](https://github.com/projectkudu/kudu/wiki) kullanır.</span><span class="sxs-lookup"><span data-stu-id="1b71a-120">When you configure VSTS continuous deployment from the Azure portal, the integration uses the App Service [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki), which already automates build and deployment tasks with every `git push`.</span></span> <span data-ttu-id="1b71a-121">VSTS’de sürekli dağıtımı ayrıca ayarlamanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="1b71a-121">You do not need to separately set up continuous deployment in VSTS.</span></span> <span data-ttu-id="1b71a-122">Bu işlem tamamlandıktan sonra **Dağıtım seçenekleri** uygulama dikey penceresinde dağıtımın başarılı olduğunu belirten bir etkin dağıtım gösterilir.</span><span class="sxs-lookup"><span data-stu-id="1b71a-122">After this process completes, the **Deployment options** app blade will show an active deployment that indicates deployment has succeeded.</span></span>
5. <span data-ttu-id="1b71a-123">Uygulamanın başarıyla dağıtıldığını doğrulamak için Azure portalındaki uygulama dikey penceresinin üstünde bulunan **URL**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1b71a-123">To verify the app is successfully deployed, click the **URL** at the top of the app's blade in the Azure portal.</span></span>
6. <span data-ttu-id="1b71a-124">Sürekli dağıtımın seçtiğiniz depodan gerçekleştiğini doğrulamak için depoya bir değişiklik gönderin.</span><span class="sxs-lookup"><span data-stu-id="1b71a-124">To verify that continuous deployment is occurring from the repository of your choice, push a change to the repository.</span></span> <span data-ttu-id="1b71a-125">Depoya gönderilen değişiklik tamamlandıktan kısa süre sonra uygulamanız değişiklikleri yansıtacak şekilde güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1b71a-125">Your app should update to reflect the changes shortly after the push to the repository completes.</span></span> <span data-ttu-id="1b71a-126">Uygulamanızın **Dağıtım seçenekleri** dikey penceresinde güncelleştirmenin alındığını doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b71a-126">You can verify that it has pulled in the update in the **Deployment options** blade of your app.</span></span>

## <span data-ttu-id="1b71a-127"><a name="VSsolution"></a>Visual Studio çözümünün sürekli dağıtımı</span><span class="sxs-lookup"><span data-stu-id="1b71a-127"><a name="VSsolution"></a>Continuous deployment of a Visual Studio solution</span></span>
<span data-ttu-id="1b71a-128">Azure Uygulama Hizmeti’ne bir Visual Studio çözümünün gönderilmesi, basit bir index.html dosyası göndermek kadar kolaydır.</span><span class="sxs-lookup"><span data-stu-id="1b71a-128">Pushing a Visual Studio solution to Azure App Service is just as easy as pushing a simple index.html file.</span></span> <span data-ttu-id="1b71a-129">Uygulama Hizmeti dağıtım işlemi, NuGet bağımlılıklarını geri yükleme ve uygulama ikili dosyalarını oluşturma dahil tüm ayrıntıları kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="1b71a-129">The App Service deployment process streamlines all the details, including restoring NuGet dependencies and building the application binaries.</span></span> <span data-ttu-id="1b71a-130">Kodu yalnızca Git deponuzda tutmayı ve Uygulama Hizmeti dağıtımının geri kalan işlemlerini yapmasına izin vermeyi içeren kaynak denetimi en iyi uygulamalarını izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b71a-130">You can follow the source control best practices of maintaining code only in your Git repository, and let App Service deployment take care of the rest.</span></span>

<span data-ttu-id="1b71a-131">Çözümünüzü ve deponuzu aşağıdaki gibi yapılandırmanız şartıyla, Visual Studio çözümünüzü Uygulama Hizmeti’ne gönderme adımları [önceki bölümde](#overview) verilen adımlarla aynıdır:</span><span class="sxs-lookup"><span data-stu-id="1b71a-131">The steps for pushing your Visual Studio solution to App Service are the same as in the [previous section](#overview), provided that you configure your solution and repository as follows:</span></span>

* <span data-ttu-id="1b71a-132">Aşağıdaki görüntüye benzer bir `.gitignore` dosyası oluşturmak veya deponuzda bu [.gitignore örneğine](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore) benzer içeriğe sahip bir `.gitignore` dosyasını el ile eklemek için Visual Studio kaynak denetimi seçeneğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1b71a-132">Use the Visual Studio source control option to generate a `.gitignore` file such as the image below or manually add a `.gitignore` file in your repository root with content similar to this [.gitignore sample](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* <span data-ttu-id="1b71a-133">Çözümün tamamına ait dizin ağacını, .sln dosyası depo kökünde olacak şekilde deponuza ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1b71a-133">Add the entire solution's directory tree to your repository, with the .sln file in the repository root.</span></span>

<span data-ttu-id="1b71a-134">Deponuzu anlatılan şekilde ayarlayıp Azure’da uygulamanızı çevrimiçi Git depolarından birinden sürekli yayımlama için yapılandırdıktan sonra, Visual Studio’da ASP.NET uygulamanızı yerel olarak geliştirebilir ve değişikliklerinizi çevrimiçi Git deponuza göndererek kodunuzu sürekli olarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b71a-134">Once you have set up your repository as described, and configured your app in Azure for continuous publishing from one of the online Git repositories, you can develop your ASP.NET application locally in Visual Studio and continuously deploy your code simply by pushing your changes to your online Git repository.</span></span>

## <span data-ttu-id="1b71a-135"><a name="disableCD"></a>Sürekli dağıtımı devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="1b71a-135"><a name="disableCD"></a>Disable continuous deployment</span></span>
<span data-ttu-id="1b71a-136">Sürekli dağıtımı devre dışı bırakmak için,</span><span class="sxs-lookup"><span data-stu-id="1b71a-136">To disable continuous deployment,</span></span>

1. <span data-ttu-id="1b71a-137">Uygulamanızın [Azure Portal] menü dikey penceresinde **UYGULAMA DAĞITIMI > Dağıtım seçenekleri**’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1b71a-137">In your app's menu blade in the [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="1b71a-138">Ardından **Dağıtım seçenekleri** dikey penceresinde **Bağlantıyı Kes**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1b71a-138">Then click **Disconnect** in the **Deployment options** blade.</span></span>
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. <span data-ttu-id="1b71a-139">Onay iletisine **Evet** cevabını verdikten sonra başka bir kaynaktan yayımlamayı ayarlamak isterseniz uygulamanın dikey penceresine geri dönüp **UYGULAMA DAĞITIMI > Dağıtım seçenekleri**’ne tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b71a-139">After answering **Yes** to the confirmation message, you can return to your app's blade and click **APP DEPLOYMENT > Deployment options** if you would like to set up publishing from another source.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1b71a-140">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="1b71a-140">Additional Resources</span></span>
* [<span data-ttu-id="1b71a-141">Sürekli dağıtımla ilgili yaygın sorunları araştırma</span><span class="sxs-lookup"><span data-stu-id="1b71a-141">How to investigate common issues with continuous deployment</span></span>](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* <span data-ttu-id="1b71a-142">[Azure için PowerShell'i kullanma]</span><span class="sxs-lookup"><span data-stu-id="1b71a-142">[How to use PowerShell for Azure]</span></span>
* <span data-ttu-id="1b71a-143">[Mac ve Linux için Azure Komut Satırı Araçlarını kullanma]</span><span class="sxs-lookup"><span data-stu-id="1b71a-143">[How to use the Azure Command-Line Tools for Mac and Linux]</span></span>
* <span data-ttu-id="1b71a-144">[Git belgeleri]</span><span class="sxs-lookup"><span data-stu-id="1b71a-144">[Git documentation]</span></span>
* [<span data-ttu-id="1b71a-145">Kudu Projesi</span><span class="sxs-lookup"><span data-stu-id="1b71a-145">Project Kudu</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="1b71a-146">Otomatik olarak ASP.NET 4 uygulama dağıtmak için bir CI/CD ardışık düzen oluşturmak için Azure kullanın</span><span class="sxs-lookup"><span data-stu-id="1b71a-146">Use Azure to automatically generate a CI/CD pipeline to deploy an ASP.NET 4 app</span></span>](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> <span data-ttu-id="1b71a-147">Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="1b71a-147">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="1b71a-148">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="1b71a-148">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="1b71a-149">[Azure Uygulama Hizmeti]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/</span><span class="sxs-lookup"><span data-stu-id="1b71a-149">[Azure App Service]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/</span></span>
<span data-ttu-id="1b71a-150">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="1b71a-150">[Azure portal]: https://portal.azure.com</span></span>
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
<span data-ttu-id="1b71a-151">[Azure için PowerShell'i kullanma]: /powershell/azureps-cmdlets-docs</span><span class="sxs-lookup"><span data-stu-id="1b71a-151">[How to use PowerShell for Azure]: /powershell/azureps-cmdlets-docs</span></span>
<span data-ttu-id="1b71a-152">[Mac ve Linux için Azure Komut Satırı Araçlarını kullanma]:../cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="1b71a-152">[How to use the Azure Command-Line Tools for Mac and Linux]:../cli-install-nodejs.md</span></span>
<span data-ttu-id="1b71a-153">[Git Belgeleri]: http://git-scm.com/documentation</span><span class="sxs-lookup"><span data-stu-id="1b71a-153">[Git Documentation]: http://git-scm.com/documentation</span></span>

<span data-ttu-id="1b71a-154">[Depo oluşturma (GitHub)]: https://help.github.com/articles/create-a-repo</span><span class="sxs-lookup"><span data-stu-id="1b71a-154">[Create a repo (GitHub)]: https://help.github.com/articles/create-a-repo</span></span>
<span data-ttu-id="1b71a-155">[Depo oluşturma (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo</span><span class="sxs-lookup"><span data-stu-id="1b71a-155">[Create a repo (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo</span></span>
<span data-ttu-id="1b71a-156">[VSTS kullanmaya başlama]: https://www.visualstudio.com/docs/vsts-tfs-overview</span><span class="sxs-lookup"><span data-stu-id="1b71a-156">[Get started with VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview</span></span>
