---
title: "Azure işlevleri için aaaContinuous dağıtımı | Microsoft Docs"
description: "Azure uygulama hizmeti toopublish, sürekli dağıtım özellikleri, Azure işlevlerini kullanın."
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
ms.openlocfilehash: 28c44f737dad3feab3cf54f7dd42b6a978d0617e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="70b23-103">Azure İşlevleri için sürekli dağıtım</span><span class="sxs-lookup"><span data-stu-id="70b23-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="70b23-104">Azure işlevleri kılar kolay toodeploy uygulama hizmeti sürekli tümleştirme kullanarak işlevi uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="70b23-104">Azure Functions makes it easy toodeploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="70b23-105">İşlevler, BitBucket, Dropbox, GitHub ve Visual Studio Team Services (VSTS) ile tümleşir.</span><span class="sxs-lookup"><span data-stu-id="70b23-105">Functions integrates with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS).</span></span> <span data-ttu-id="70b23-106">Bu Tümleşik Hizmetler tetikleyici dağıtım tooAzure birini kullanarak yapılan burada işlev kodu güncelleştirmeleri bir iş akışı sağlar.</span><span class="sxs-lookup"><span data-stu-id="70b23-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment tooAzure.</span></span> <span data-ttu-id="70b23-107">Yeni tooAzure işlevleri varsa, başlayın [Azure işlevlerine genel bakış](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="70b23-107">If you are new tooAzure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="70b23-108">Sürekli dağıtım, birden fazla ve sık gerçekleşen katkıların tümleştirildiği projeler için mükemmel bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="70b23-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="70b23-109">Ayrıca, kaynak denetimi işlevleri kodunuzu tutmanıza sağlar.</span><span class="sxs-lookup"><span data-stu-id="70b23-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="70b23-110">Aşağıdaki dağıtım kaynaklar hello şu anda desteklenir:</span><span class="sxs-lookup"><span data-stu-id="70b23-110">hello following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="70b23-111">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="70b23-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="70b23-112">Açılan kutu</span><span class="sxs-lookup"><span data-stu-id="70b23-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="70b23-113">Dış depo (Git veya Mercurial)</span><span class="sxs-lookup"><span data-stu-id="70b23-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="70b23-114">Yerel Git deposu</span><span class="sxs-lookup"><span data-stu-id="70b23-114">Git local repository</span></span>](../app-service-web/app-service-deploy-local-git.md)
* [<span data-ttu-id="70b23-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="70b23-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="70b23-116">OneDrive</span><span class="sxs-lookup"><span data-stu-id="70b23-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="70b23-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="70b23-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="70b23-118">Dağıtımları bir işlev başına uygulama temelinde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="70b23-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="70b23-119">Sürekli dağıtım etkinleştirildikten sonra erişim toofunction kod hello portalında çok kümesi*salt okunur*.</span><span class="sxs-lookup"><span data-stu-id="70b23-119">After continuous deployment is enabled, access toofunction code in hello portal is set too*read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="70b23-120">Sürekli dağıtım gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="70b23-120">Continuous deployment requirements</span></span>

<span data-ttu-id="70b23-121">Yapılandırılan dağıtım kaynağınız ve işlevleri kodunuz hello dağıtım kaynağı, sürekli dağıtım ayarlayın. önce olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="70b23-121">You must have your deployment source configured and your functions code in hello deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="70b23-122">Verilen işlevin uygulama dağıtımı her işlevi hello dizin adı hello işlevinin hello adı olduğu bir adlandırılmış alt dizininde bulunur.</span><span class="sxs-lookup"><span data-stu-id="70b23-122">In a given function app deployment, each function lives in a named subdirectory, where hello directory name is hello name of hello function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="70b23-123">Sürekli dağıtım ayarlama</span><span class="sxs-lookup"><span data-stu-id="70b23-123">Set up continuous deployment</span></span>
<span data-ttu-id="70b23-124">Bu yordam tooconfigure sürekli dağıtımı için var olan bir işlev uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="70b23-124">Use this procedure tooconfigure continuous deployment for an existing function app.</span></span> <span data-ttu-id="70b23-125">GitHub depo ile tümleştirme adımları gösterir, ancak Visual Studio Team Services veya diğer Dağıtım Hizmetleri için benzer adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="70b23-125">These steps demonstrate integration with a GitHub repository, but similar steps apply for Visual Studio Team Services or other deployment services.</span></span>

1. <span data-ttu-id="70b23-126">Merhaba işlevi uygulamanızda [Azure portal](https://portal.azure.com), tıklatın **Platform özellikleri** ve **dağıtım seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="70b23-126">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Sürekli dağıtım ayarlayın](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="70b23-128">Merhaba sonra **dağıtımları** dikey penceresinde **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="70b23-128">Then in hello **Deployments** blade click **Setup**.</span></span>
 
    ![Sürekli dağıtım ayarlayın](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="70b23-130">Merhaba, **dağıtım kaynağı** dikey penceresinde tıklatın **Kaynak Seç**, seçtiğiniz dağıtım kaynağınız hello bilgileri doldurun ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="70b23-130">In hello **Deployment source** blade, click **Choose source**, then fill in hello information for your chosen deployment source and click **OK**.</span></span>
   
    ![Dağıtım kaynağı seçin](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="70b23-132">Sürekli dağıtım yapılandırıldıktan sonra tüm dosya değişiklikler dağıtım kaynağınızda kopyalanan toohello işlev uygulaması ve bir sitenin tam dağıtım tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="70b23-132">After continuous deployment is configured, all file changes in your deployment source are copied toohello function app and a full site deployment is triggered.</span></span> <span data-ttu-id="70b23-133">Merhaba kaynak dosyalarında güncelleştirildiğinde hello site yeniden dağıtıldı.</span><span class="sxs-lookup"><span data-stu-id="70b23-133">hello site is redeployed when files in hello source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="70b23-134">Dağıtım seçenekleri</span><span class="sxs-lookup"><span data-stu-id="70b23-134">Deployment options</span></span>

<span data-ttu-id="70b23-135">Merhaba, bazı tipik dağıtım senaryoları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="70b23-135">hello following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="70b23-136">Hazırlama dağıtımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="70b23-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="70b23-137">Var olan işlevler toocontinuous dağıtımını taşıma</span><span class="sxs-lookup"><span data-stu-id="70b23-137">Move existing functions toocontinuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="70b23-138">Hazırlama dağıtımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="70b23-138">Create a staging deployment</span></span>

<span data-ttu-id="70b23-139">İşlev uygulamalar henüz dağıtım yuvaları desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="70b23-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="70b23-140">Ancak, yine de, sürekli tümleştirme kullanarak ayrı hazırlama ve üretim dağıtımları yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70b23-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="70b23-141">işlem tooconfigure hello ve iş hazırlama dağıtımıyla genellikle şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="70b23-141">hello process tooconfigure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="70b23-142">Aboneliğiniz, hello üretim kodu için diğeri için hazırlama iki işlevi uygulamalar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="70b23-142">Create two function apps in your subscription, one for hello production code and one for staging.</span></span> 

2. <span data-ttu-id="70b23-143">Zaten yoksa, bir dağıtım kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="70b23-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="70b23-144">Bu örnekte [GitHub].</span><span class="sxs-lookup"><span data-stu-id="70b23-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="70b23-145">Üretim işlevi uygulamanız için tam hello önceki bölümlerinde bulunan adımları **sürekli dağıtım ayarlayın** ve kümesi hello dağıtım şube toohello ana, GitHub deponun dalı.</span><span class="sxs-lookup"><span data-stu-id="70b23-145">For your production function app, complete hello preceding steps in **Set up continuous deployment** and set hello deployment branch toohello master branch of your GitHub repository.</span></span>
   
    ![Dağıtım şube seçin](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="70b23-147">İşlev uygulaması hazırlama hello için bu adımı yineleyin, ancak dal, bunun yerine, GitHub deposuna hazırlama hello seçin.</span><span class="sxs-lookup"><span data-stu-id="70b23-147">Repeat this step for hello staging function app, but choose hello staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="70b23-148">Dağıtım kaynağı dallanma desteklemiyorsa, farklı bir klasör kullanın.</span><span class="sxs-lookup"><span data-stu-id="70b23-148">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="70b23-149">Güncelleştirmeleri tooyour Kodu'nu şube veya klasörün hazırlama hello sonra bu değişiklikleri dağıtım hazırlama hello yansıtılır doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="70b23-149">Make updates tooyour code in hello staging branch or folder, then verify that those changes are reflected in hello staging deployment.</span></span>

6. <span data-ttu-id="70b23-150">Test sonra birleştirme hello ana dala hello hazırlama daldan değiştirir.</span><span class="sxs-lookup"><span data-stu-id="70b23-150">After testing, merge changes from hello staging branch into hello master branch.</span></span> <span data-ttu-id="70b23-151">Bu birleştirme dağıtım toohello üretim işlev uygulaması tetikler.</span><span class="sxs-lookup"><span data-stu-id="70b23-151">This merge triggers deployment toohello production function app.</span></span> <span data-ttu-id="70b23-152">Dağıtım kaynağı dalları desteklemiyorsa, hello üretim klasöründeki hello dosyaları klasörü hazırlama hello hello dosyalarından üzerine yazın.</span><span class="sxs-lookup"><span data-stu-id="70b23-152">If your deployment source doesn't support branches, overwrite hello files in hello production folder with hello files from hello staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-toocontinuous-deployment"></a><span data-ttu-id="70b23-153">Var olan işlevler toocontinuous dağıtımını taşıma</span><span class="sxs-lookup"><span data-stu-id="70b23-153">Move existing functions toocontinuous deployment</span></span>
<span data-ttu-id="70b23-154">Oluşturulmuş ve korunan hello Portalı'nda toodownload ihtiyacınız var olan işlevler varsa, yukarıda açıklandığı gibi sürekli dağıtım ayarlamadan önce FTP veya hello yerel Git deposu kullanarak kod dosyaları işlev varolan.</span><span class="sxs-lookup"><span data-stu-id="70b23-154">When you have existing functions that you have created and maintained in hello portal, you need toodownload your existing function code files using FTP or hello local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="70b23-155">Hello App Service ayarlarını işlevi uygulamanız için bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70b23-155">You can do this in hello App Service settings for your function app.</span></span> <span data-ttu-id="70b23-156">Dosyalarınızı İndirildikten sonra seçilen tooyour sürekli dağıtım kaynağı karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70b23-156">After your files are downloaded, you can upload them tooyour chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="70b23-157">Sürekli Tümleştirme yapılandırdıktan sonra artık hello işlevleri Portalı'nda, kaynak dosyaları mümkün tooedit olacaktır.</span><span class="sxs-lookup"><span data-stu-id="70b23-157">After you configure continuous integration, you will no longer be able tooedit your source files in hello Functions portal.</span></span>

- [<span data-ttu-id="70b23-158">Nasıl yapılır: dağıtım kimlik bilgilerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="70b23-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="70b23-159">Nasıl yapılır: FTP kullanarak dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="70b23-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="70b23-160">Nasıl yapılır: hello yerel Git deposu kullanarak dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="70b23-160">How to: Download files using hello local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="70b23-161">Nasıl yapılır: dağıtım kimlik bilgilerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="70b23-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="70b23-162">FTP veya yerel Git deposu ile işlevi uygulamanızdan dosyalarını indirmeden önce kimlik bilgilerini tooaccess hello sitenizi yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="70b23-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials tooaccess hello site.</span></span> <span data-ttu-id="70b23-163">Kimlik bilgileri hello işlevi uygulama düzeyinde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="70b23-163">Credentials are set at hello Function app level.</span></span> <span data-ttu-id="70b23-164">Hello Azure portal adımları tooset dağıtım kimlik bilgilerini aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="70b23-164">Use hello following steps tooset deployment credentials in hello Azure portal:</span></span>

1. <span data-ttu-id="70b23-165">Merhaba işlevi uygulamanızda [Azure portal](https://portal.azure.com), tıklatın **Platform özellikleri** ve **dağıtım kimlik bilgileri**.</span><span class="sxs-lookup"><span data-stu-id="70b23-165">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![Yerel dağıtım kimlik bilgilerini ayarlama](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="70b23-167">Bir kullanıcı adı ve parolasını yazın ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="70b23-167">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="70b23-168">Bu gibi durumlarda, bu kimlik bilgileri tooaccess şimdi işlevi uygulamanızdan FTP veya hello yerleşik Git deposu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70b23-168">You can now use these credentials tooaccess your function app from FTP or hello built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="70b23-169">Nasıl yapılır: FTP kullanarak dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="70b23-169">How to: Download files using FTP</span></span>

1. <span data-ttu-id="70b23-170">Merhaba işlevi uygulamanızda [Azure portal](https://portal.azure.com), tıklatın **Platform özellikleri** ve **özellikleri**, hello değerlerini kopyalayın **FTP/dağıtım kullanıcı**, **FTP ana bilgisayar adı**, ve **FTPS konak adı**.</span><span class="sxs-lookup"><span data-stu-id="70b23-170">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="70b23-171">**FTP/dağıtım kullanıcısı** hello uygulama adı, tooprovide uygun bağlamı hello FTP sunucusu için de dahil olmak üzere hello portalında görüntülenen girilmelidir.</span><span class="sxs-lookup"><span data-stu-id="70b23-171">**FTP/Deployment User** must be entered as displayed in hello portal, including hello app name, tooprovide proper context for hello FTP server.</span></span>
   
    ![Dağıtım bilgileri alma](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="70b23-173">FTP istemcisinden, tooconnect tooyour uygulama topladığınız hello bağlantı bilgilerini kullanın ve işlevlerinizi hello kaynak dosyalarını indirin.</span><span class="sxs-lookup"><span data-stu-id="70b23-173">From your FTP client, use hello connection information you gathered tooconnect tooyour app and download hello source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="70b23-174">Nasıl yapılır: yerel bir Git deposu kullanarak dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="70b23-174">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="70b23-175">Merhaba işlevi uygulamanızda [Azure portal](https://portal.azure.com), tıklatın **Platform özellikleri** ve **dağıtım seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="70b23-175">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Sürekli dağıtım ayarlayın](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="70b23-177">Merhaba sonra **dağıtımları** dikey penceresinde **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="70b23-177">Then in hello **Deployments** blade click **Setup**.</span></span>
 
    ![Sürekli dağıtım ayarlayın](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="70b23-179">Merhaba, **dağıtım kaynağı** dikey penceresinde tıklatın **yerel Git deposu** ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="70b23-179">In hello **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="70b23-180">İçinde **Platform özellikleri**, tıklatın **özellikleri** ve Git URL'si hello değerini not edin.</span><span class="sxs-lookup"><span data-stu-id="70b23-180">In **Platform features**, click **Properties** and note hello value of Git URL.</span></span> 
   
    ![Sürekli dağıtım ayarlayın](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="70b23-182">Git algılayan bir komut istemi veya sık kullanılan Git aracı kullanarak yerel makinenizde Hello depoyu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="70b23-182">Clone hello repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="70b23-183">Merhaba Git kopya komut şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="70b23-183">hello Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="70b23-184">Dosyaları aşağıdaki örneğine hello olduğu gibi yerel bilgisayarınızda, işlev uygulaması toohello kopya getirin:</span><span class="sxs-lookup"><span data-stu-id="70b23-184">Fetch files from your function app toohello clone on your local computer, as in hello following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="70b23-185">İstenirse, sağlamanız, [dağıtım kimlik bilgileri yapılandırılmış](#credentials).</span><span class="sxs-lookup"><span data-stu-id="70b23-185">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

[GitHub]: https://github.com/
