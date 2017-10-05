---
title: "Azure işlevleri için sürekli dağıtım | Microsoft Docs"
description: "Azure işlevleri yayımlamak için sürekli dağıtım özellikleri Azure App Service'in kullanın."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: 3756f1a039730bfd99b0375ce9bfeaf27178f2e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="07541-103">Azure İşlevleri için sürekli dağıtım</span><span class="sxs-lookup"><span data-stu-id="07541-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="07541-104">Azure işlevleri uygulama hizmeti sürekli tümleştirme kullanarak işlevi uygulamanızı dağıtmak kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="07541-104">Azure Functions makes it easy to deploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="07541-105">İşlevler, BitBucket, Dropbox, GitHub ve Visual Studio Team Services (VSTS) ile tümleşir.</span><span class="sxs-lookup"><span data-stu-id="07541-105">Functions integrates with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS).</span></span> <span data-ttu-id="07541-106">Bu, Azure'a bu tümleşik hizmetler tetikleyici dağıtımı birini kullanarak yapılan burada işlev kodu güncelleştirmeleri bir iş akışı sağlar.</span><span class="sxs-lookup"><span data-stu-id="07541-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment to Azure.</span></span> <span data-ttu-id="07541-107">Azure işlevleri yeniyseniz, başlayın [Azure işlevlerine genel bakış](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="07541-107">If you are new to Azure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="07541-108">Sürekli dağıtım, birden fazla ve sık gerçekleşen katkıların tümleştirildiği projeler için mükemmel bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="07541-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="07541-109">Ayrıca, kaynak denetimi işlevleri kodunuzu tutmanıza sağlar.</span><span class="sxs-lookup"><span data-stu-id="07541-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="07541-110">Aşağıdaki dağıtım kaynakları şu anda desteklenir:</span><span class="sxs-lookup"><span data-stu-id="07541-110">The following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="07541-111">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="07541-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="07541-112">Açılan kutu</span><span class="sxs-lookup"><span data-stu-id="07541-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="07541-113">Dış depo (Git veya Mercurial)</span><span class="sxs-lookup"><span data-stu-id="07541-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="07541-114">Yerel Git deposu</span><span class="sxs-lookup"><span data-stu-id="07541-114">Git local repository</span></span>](../app-service-web/app-service-deploy-local-git.md)
* [<span data-ttu-id="07541-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="07541-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="07541-116">OneDrive</span><span class="sxs-lookup"><span data-stu-id="07541-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="07541-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="07541-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="07541-118">Dağıtımları bir işlev başına uygulama temelinde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="07541-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="07541-119">Sürekli dağıtım etkinleştirildikten sonra portal işlev kodu erişim kümesine *salt okunur*.</span><span class="sxs-lookup"><span data-stu-id="07541-119">After continuous deployment is enabled, access to function code in the portal is set to *read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="07541-120">Sürekli dağıtım gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="07541-120">Continuous deployment requirements</span></span>

<span data-ttu-id="07541-121">Yapılandırılan dağıtım kaynağınız ve işlevleri kodunuz, sürekli dağıtım ayarlayın. önce dağıtım kaynağı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="07541-121">You must have your deployment source configured and your functions code in the deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="07541-122">Verilen işlevin uygulama dağıtımı her işlevi dizin adı işlevin adı olduğu bir adlandırılmış alt dizininde bulunur.</span><span class="sxs-lookup"><span data-stu-id="07541-122">In a given function app deployment, each function lives in a named subdirectory, where the directory name is the name of the function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="07541-123">Sürekli dağıtım ayarlama</span><span class="sxs-lookup"><span data-stu-id="07541-123">Set up continuous deployment</span></span>
<span data-ttu-id="07541-124">Varolan bir işlev uygulaması için sürekli dağıtım yapılandırmak için bu yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="07541-124">Use this procedure to configure continuous deployment for an existing function app.</span></span> <span data-ttu-id="07541-125">GitHub depo ile tümleştirme adımları gösterir, ancak Visual Studio Team Services veya diğer Dağıtım Hizmetleri için benzer adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="07541-125">These steps demonstrate integration with a GitHub repository, but similar steps apply for Visual Studio Team Services or other deployment services.</span></span>

1. <span data-ttu-id="07541-126">İşlev uygulamanızda [Azure portal](https://portal.azure.com), tıklatın **Platform özellikleri** ve **dağıtım seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="07541-126">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Sürekli dağıtım ayarlayın](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="07541-128">Ardından **dağıtımları** dikey penceresinde **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="07541-128">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![Sürekli dağıtım ayarlayın](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="07541-130">İçinde **dağıtım kaynağı** dikey penceresinde tıklatın **Kaynak Seç**, seçtiğiniz dağıtım kaynağınız bilgileri doldurun ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="07541-130">In the **Deployment source** blade, click **Choose source**, then fill in the information for your chosen deployment source and click **OK**.</span></span>
   
    ![Dağıtım kaynağı seçin](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="07541-132">Sürekli dağıtım yapılandırıldıktan sonra tüm dosya değişiklikleri dağıtım kaynağınızda işlev uygulaması kopyalanır ve bir sitenin tam dağıtım tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="07541-132">After continuous deployment is configured, all file changes in your deployment source are copied to the function app and a full site deployment is triggered.</span></span> <span data-ttu-id="07541-133">Kaynak dosyalar güncelleştirildiğinde site yeniden dağıtıldı.</span><span class="sxs-lookup"><span data-stu-id="07541-133">The site is redeployed when files in the source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="07541-134">Dağıtım seçenekleri</span><span class="sxs-lookup"><span data-stu-id="07541-134">Deployment options</span></span>

<span data-ttu-id="07541-135">Bazı tipik dağıtım senaryoları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="07541-135">The following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="07541-136">Hazırlama dağıtımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="07541-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="07541-137">Var olan işlevler için sürekli dağıtım taşıma</span><span class="sxs-lookup"><span data-stu-id="07541-137">Move existing functions to continuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="07541-138">Hazırlama dağıtımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="07541-138">Create a staging deployment</span></span>

<span data-ttu-id="07541-139">İşlev uygulamalar henüz dağıtım yuvaları desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="07541-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="07541-140">Ancak, yine de, sürekli tümleştirme kullanarak ayrı hazırlama ve üretim dağıtımları yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07541-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="07541-141">Yapılandırma ve hazırlama dağıtımı ile çalışmak için işlemi genellikle şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="07541-141">The process to configure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="07541-142">İki işlev uygulamalarının aboneliğiniz, üretim kodu için bir tane ve hazırlama için bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="07541-142">Create two function apps in your subscription, one for the production code and one for staging.</span></span> 

2. <span data-ttu-id="07541-143">Zaten yoksa, bir dağıtım kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="07541-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="07541-144">Bu örnekte [GitHub].</span><span class="sxs-lookup"><span data-stu-id="07541-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="07541-145">Üretim işlevi uygulamanız için yukarıdaki adımları tamamlayın **sürekli dağıtım ayarlayın** ve GitHub deponuz ana dala dağıtım şube ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="07541-145">For your production function app, complete the preceding steps in **Set up continuous deployment** and set the deployment branch to the master branch of your GitHub repository.</span></span>
   
    ![Dağıtım şube seçin](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="07541-147">Hazırlama işlev uygulaması için bu adımı yineleyin, ancak hazırlama dal, bunun yerine, GitHub depo seçin.</span><span class="sxs-lookup"><span data-stu-id="07541-147">Repeat this step for the staging function app, but choose the staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="07541-148">Dağıtım kaynağı dallanma desteklemiyorsa, farklı bir klasör kullanın.</span><span class="sxs-lookup"><span data-stu-id="07541-148">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="07541-149">Hazırlama şube veya klasör kodunuzda güncelleştirmeleri yapmak ve sonra bu değişiklikleri hazırlama dağıtımda yansıtılır doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="07541-149">Make updates to your code in the staging branch or folder, then verify that those changes are reflected in the staging deployment.</span></span>

6. <span data-ttu-id="07541-150">Test sonra birleştirme ana dala hazırlama daldan değiştirir.</span><span class="sxs-lookup"><span data-stu-id="07541-150">After testing, merge changes from the staging branch into the master branch.</span></span> <span data-ttu-id="07541-151">Bu birleştirme üretim işlev uygulaması için dağıtım tetikler.</span><span class="sxs-lookup"><span data-stu-id="07541-151">This merge triggers deployment to the production function app.</span></span> <span data-ttu-id="07541-152">Dağıtım kaynağı dalları desteklemiyorsa, üretim klasöründeki dosyaları hazırlama klasördeki dosyaların üzerine yazın.</span><span class="sxs-lookup"><span data-stu-id="07541-152">If your deployment source doesn't support branches, overwrite the files in the production folder with the files from the staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-to-continuous-deployment"></a><span data-ttu-id="07541-153">Var olan işlevler için sürekli dağıtım taşıma</span><span class="sxs-lookup"><span data-stu-id="07541-153">Move existing functions to continuous deployment</span></span>
<span data-ttu-id="07541-154">Ne zaman oluşturulur ve Portalı'nda saklanır, FTP kullanarak, varolan işlevi kod dosyaları karşıdan yüklemeniz veya yerel Git deposu, önce yukarıda açıklandığı gibi sürekli dağıtım ayarlayabilirsiniz var olan işlevler sahip.</span><span class="sxs-lookup"><span data-stu-id="07541-154">When you have existing functions that you have created and maintained in the portal, you need to download your existing function code files using FTP or the local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="07541-155">Uygulama hizmeti ayarlarında işlevi uygulamanız için bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07541-155">You can do this in the App Service settings for your function app.</span></span> <span data-ttu-id="07541-156">Dosyalarınızı İndirildikten sonra seçilen sürekli dağıtım kaynağınız karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07541-156">After your files are downloaded, you can upload them to your chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="07541-157">Sürekli Tümleştirme yapılandırdıktan sonra artık kaynak dosyalarınız işlevleri portalındaki düzenlemeniz mümkün olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="07541-157">After you configure continuous integration, you will no longer be able to edit your source files in the Functions portal.</span></span>

- [<span data-ttu-id="07541-158">Nasıl yapılır: dağıtım kimlik bilgilerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="07541-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="07541-159">Nasıl yapılır: FTP kullanarak dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="07541-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="07541-160">Nasıl yapılır: yerel Git deposu kullanarak dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="07541-160">How to: Download files using the local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="07541-161">Nasıl yapılır: dağıtım kimlik bilgilerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="07541-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="07541-162">FTP veya yerel Git deposu ile işlevi uygulamanızdan dosyalarını indirmeden önce siteye erişmek için kimlik bilgilerinizi yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="07541-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials to access the site.</span></span> <span data-ttu-id="07541-163">Kimlik bilgileri işlevi uygulama düzeyinde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="07541-163">Credentials are set at the Function app level.</span></span> <span data-ttu-id="07541-164">Azure portalında dağıtım kimlik bilgilerini ayarlamak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="07541-164">Use the following steps to set deployment credentials in the Azure portal:</span></span>

1. <span data-ttu-id="07541-165">İşlev uygulamanızda [Azure portal](https://portal.azure.com), tıklatın **Platform özellikleri** ve **dağıtım kimlik bilgileri**.</span><span class="sxs-lookup"><span data-stu-id="07541-165">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![Yerel dağıtım kimlik bilgilerini ayarlama](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="07541-167">Bir kullanıcı adı ve parolasını yazın ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="07541-167">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="07541-168">Bu kimlik bilgileri şimdi işlevi uygulamanızı FTP ya da yerleşik Git deposuna erişmek için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07541-168">You can now use these credentials to access your function app from FTP or the built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="07541-169">Nasıl yapılır: FTP kullanarak dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="07541-169">How to: Download files using FTP</span></span>

1. <span data-ttu-id="07541-170">İşlev uygulamanızda [Azure portal](https://portal.azure.com), tıklatın **Platform özellikleri** ve **özellikleri**, değerlerini kopyalayın **FTP/dağıtım kullanıcı**, **FTP konak adı**, ve **FTPS konak adı**.</span><span class="sxs-lookup"><span data-stu-id="07541-170">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="07541-171">**FTP/dağıtım kullanıcısı** FTP sunucusu için uygun bağlamı sağlamak için uygulama adı dahil olmak üzere Portalı'nda görüntülenen girilmelidir.</span><span class="sxs-lookup"><span data-stu-id="07541-171">**FTP/Deployment User** must be entered as displayed in the portal, including the app name, to provide proper context for the FTP server.</span></span>
   
    ![Dağıtım bilgileri alma](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="07541-173">Bağlantı bilgileri, bir FTP istemcisinden kullanın, uygulamanızın bağlanmak ve işlevlerinizi kaynak dosyalarını indirmek için toplanan.</span><span class="sxs-lookup"><span data-stu-id="07541-173">From your FTP client, use the connection information you gathered to connect to your app and download the source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="07541-174">Nasıl yapılır: yerel bir Git deposu kullanarak dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="07541-174">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="07541-175">İşlev uygulamanızda [Azure portal](https://portal.azure.com), tıklatın **Platform özellikleri** ve **dağıtım seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="07541-175">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Sürekli dağıtım ayarlayın](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="07541-177">Ardından **dağıtımları** dikey penceresinde **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="07541-177">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![Sürekli dağıtım ayarlayın](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="07541-179">İçinde **dağıtım kaynağı** dikey penceresinde tıklatın **yerel Git deposu** ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="07541-179">In the **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="07541-180">İçinde **Platform özellikleri**, tıklatın **özellikleri** ve Git URL'si değerini not edin.</span><span class="sxs-lookup"><span data-stu-id="07541-180">In **Platform features**, click **Properties** and note the value of Git URL.</span></span> 
   
    ![Sürekli dağıtım ayarlayın](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="07541-182">Uygulamanızı yerel makinenizde Git algılayan bir komut istemi veya sık kullanılan Git aracını kullanarak depoyu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="07541-182">Clone the repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="07541-183">Git kopya komut şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="07541-183">The Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="07541-184">Dosyaları aşağıdaki örnekteki gibi yerel bilgisayarınızda kopyaya işlevi uygulamanızdan getirin:</span><span class="sxs-lookup"><span data-stu-id="07541-184">Fetch files from your function app to the clone on your local computer, as in the following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="07541-185">İstenirse, sağlamanız, [dağıtım kimlik bilgileri yapılandırılmış](#credentials).</span><span class="sxs-lookup"><span data-stu-id="07541-185">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

<span data-ttu-id="07541-186">[GitHub]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="07541-186">[GitHub]: https://github.com/</span></span>
