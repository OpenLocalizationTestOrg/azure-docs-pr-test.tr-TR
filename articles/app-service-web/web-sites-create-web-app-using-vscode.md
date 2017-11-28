---
title: "Visual Studio Code ASP.NET Core web uygulamasında aaaCreate"
description: "Bu öğretici nasıl toocreate ASP.NET Core web uygulamasını Visual Studio Code kullanarak gösterilmektedir."
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a><span data-ttu-id="e09d8-103">Visual Studio kodda bir ASP.NET Core web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e09d8-103">Create an ASP.NET Core web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="e09d8-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e09d8-104">Overview</span></span>
<span data-ttu-id="e09d8-105">Bu öğreticide, bir ASP.NET Core toocreate nasıl web uygulamasını kullanarak gösterilir [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) ve çok dağıtma[Azure App Service](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="e09d8-105">This tutorial shows you how toocreate an ASP.NET Core web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it too[Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="e09d8-106">Bu makalede tooweb uygulamaları başvuruyor ancak tooAPI uygulamaları ve mobil uygulamalara da uygulanır.</span><span class="sxs-lookup"><span data-stu-id="e09d8-106">Although this article refers tooweb apps, it also applies tooAPI apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="e09d8-107">ASP.NET çekirdeği ASP.NET önemli yeniden tasarlanması olur.</span><span class="sxs-lookup"><span data-stu-id="e09d8-107">ASP.NET Core is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="e09d8-108">ASP.NET Core .NET kullanarak modern bulut tabanlı web uygulamaları oluşturmak için yeni bir açık kaynaklı ve çapraz platform framework kümesidir.</span><span class="sxs-lookup"><span data-stu-id="e09d8-108">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="e09d8-109">Daha fazla bilgi için bkz: [giriş tooASP.NET çekirdek](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span><span class="sxs-lookup"><span data-stu-id="e09d8-109">For more information, see [Introduction tooASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="e09d8-110">Azure App Service web apps hakkında daha fazla bilgi için bkz: [Web Apps'e genel bakış](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e09d8-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="e09d8-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e09d8-111">Prerequisites</span></span>
* <span data-ttu-id="e09d8-112">Yükleme [VS Code](http://code.visualstudio.com/Docs/setup).</span><span class="sxs-lookup"><span data-stu-id="e09d8-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="e09d8-113">Git - yüklemek bu konumları birinden yükleyebilirsiniz: [Chocolatey](https://chocolatey.org/packages/git) veya [git scm.com](http://git-scm.com/downloads). Yeni tooGit varsa, seçin [git scm.com](http://git-scm.com/downloads) ve hello seçeneğini çok**kullanım Git hello Windows komut istemi gelen**.</span><span class="sxs-lookup"><span data-stu-id="e09d8-113">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads). If you are new tooGit, choose [git-scm.com](http://git-scm.com/downloads) and select hello option too**Use Git from hello Windows Command Prompt**.</span></span> <span data-ttu-id="e09d8-114">Git yükledikten sonra (bir yürütme VS koddan gerçekleştirirken) daha sonra hello öğreticide gerektiği şekilde de tooset hello Git kullanıcı adı ve e-posta ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="e09d8-114">Once you install Git, you'll also need tooset hello Git user name and email as it's required later in hello tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-core"></a><span data-ttu-id="e09d8-115">ASP.NET Core yükleyin</span><span class="sxs-lookup"><span data-stu-id="e09d8-115">Install ASP.NET Core</span></span>
<span data-ttu-id="e09d8-116">ASP.NET çekirdeği modern Bulut ve OS X, Linux ve Windows çalıştıran web uygulamaları oluşturmak için yalın bir .NET yığını olur.</span><span class="sxs-lookup"><span data-stu-id="e09d8-116">ASP.NET Core is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="e09d8-117">Bu tooprovide plan hello gelen ya da dağıtılmış toohello Bulut veya şirket içi uygulamalar için en iyi duruma getirilmiş geliştirme framework oluşturulmadı.</span><span class="sxs-lookup"><span data-stu-id="e09d8-117">It has been built from hello ground up tooprovide an optimized development framework for apps that are either deployed toohello cloud or run on-premises.</span></span> <span data-ttu-id="e09d8-118">Çözümlerinizi oluşturulurken esneklik korumak için en az ek yük, modüler bileşenlerden oluşur.</span><span class="sxs-lookup"><span data-stu-id="e09d8-118">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="e09d8-119">Bu öğretici sürümleriyle hello son geliştirme ASP.NET Core uygulamaları oluşturmaya başladı tasarlanmış tooget ' dir.</span><span class="sxs-lookup"><span data-stu-id="e09d8-119">This tutorial is designed tooget you started building applications with hello latest development versions of ASP.NET Core.</span></span> <span data-ttu-id="e09d8-120">yönergeleri izleyerek hello belirli tooWindows ' dir.</span><span class="sxs-lookup"><span data-stu-id="e09d8-120">hello following instructions are specific tooWindows.</span></span> <span data-ttu-id="e09d8-121">OS X, Linux ve Windows yükleme yönergeleri için bkz: [ASP.NET Core ile çalışmaya başlama](https://docs.microsoft.com/aspnet/core/getting-started).</span><span class="sxs-lookup"><span data-stu-id="e09d8-121">For installation instructions on OS X, Linux, and Windows, see [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span></span> 


> [!NOTE]
> <span data-ttu-id="e09d8-122">Daha ayrıntılı OS X, Linux ve Windows için yükleme yönergeleri için bkz: [yükleme ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span><span class="sxs-lookup"><span data-stu-id="e09d8-122">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-hello-web-app"></a><span data-ttu-id="e09d8-123">Merhaba web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e09d8-123">Create hello web app</span></span>
<span data-ttu-id="e09d8-124">Bu bölümde, nasıl tooscaffold yeni bir uygulama ASP.NET web uygulaması hello .NET CLI aracını kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="e09d8-124">This section shows you how tooscaffold a new app ASP.NET web app using hello .NET CLI tool.</span></span> 

1. <span data-ttu-id="e09d8-125">Merhaba komut istemi toocreate hello proje klasörünü ve iskele hello uygulama Hello aşağıdaki girin.</span><span class="sxs-lookup"><span data-stu-id="e09d8-125">Enter hello following at hello command prompt toocreate hello project folder and scaffold hello app.</span></span>
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![DotNet CLI - ASP.NET Core Oluşturucusu](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. <span data-ttu-id="e09d8-127">toorestore gerekli NuGet paketlerini Merhaba, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e09d8-127">toorestore hello necessary NuGet packages, run hello following command:</span></span>
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a><span data-ttu-id="e09d8-128">Merhaba web uygulamasını yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e09d8-128">Run hello web app locally</span></span>
<span data-ttu-id="e09d8-129">Merhaba web uygulaması oluşturuldu ve hello uygulama için tüm hello NuGet paketlerini alınan göre hello web uygulamasını yerel olarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e09d8-129">Now that you have created hello web app and retrieved all hello NuGet packages for hello app, you can run hello web app locally.</span></span>

1. <span data-ttu-id="e09d8-130">Merhaba uygulamayı çalıştırın (Merhaba `dotnet run` komutu, hello uygulama oluşturacaksınız, eski olduğunda):</span><span class="sxs-lookup"><span data-stu-id="e09d8-130">Run hello app  (hello `dotnet run` command will build hello app when it's out of date):</span></span>
    ```terminal
    dotnet run
    ```
2. <span data-ttu-id="e09d8-131">Bir tarayıcı açın ve URL'yi aşağıdaki toohello gidin.</span><span class="sxs-lookup"><span data-stu-id="e09d8-131">Open a browser and navigate toohello following URL.</span></span>
   
    <span data-ttu-id="e09d8-132">**http://localhost: 5000**</span><span class="sxs-lookup"><span data-stu-id="e09d8-132">**http://localhost:5000**</span></span>
   
    <span data-ttu-id="e09d8-133">Merhaba web uygulaması Hello varsayılan sayfasını aşağıdaki gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="e09d8-133">hello default page of hello web app will appear as follows.</span></span>
   
    ![Bir tarayıcıda yerel web uygulaması](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="e09d8-135">Tarayıcınızı kapatın.</span><span class="sxs-lookup"><span data-stu-id="e09d8-135">Close your browser.</span></span> <span data-ttu-id="e09d8-136">Merhaba, **komut penceresi**, basın **Ctrl + C** hello uygulama ve Kapat hello aşağı tooshut **komut penceresi**.</span><span class="sxs-lookup"><span data-stu-id="e09d8-136">In hello **Command Window**, press **Ctrl+C** tooshut down hello application and close hello **Command Window**.</span></span> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="e09d8-137">Hello Azure portalı bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e09d8-137">Create a web app in hello Azure Portal</span></span>
<span data-ttu-id="e09d8-138">Hello aşağıdaki adımlar, bir web uygulaması hello Azure Portal oluşturmada size yol gösterecektir.</span><span class="sxs-lookup"><span data-stu-id="e09d8-138">hello following steps will guide you through creating a web app in hello Azure Portal.</span></span>

1. <span data-ttu-id="e09d8-139">İçinde toohello oturum [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e09d8-139">Log in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e09d8-140">Tıklatın **yeni** hello adresindeki hello Portal ' sol üst.</span><span class="sxs-lookup"><span data-stu-id="e09d8-140">Click **NEW** at hello top left of hello Portal.</span></span>
3. <span data-ttu-id="e09d8-141">Tıklatın **Web uygulamaları > Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="e09d8-141">Click **Web Apps > Web App**.</span></span>
   
    ![Azure yeni web uygulaması](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="e09d8-143">İçin bir değer girin **adı**, gibi **SampleWebAppDemo**.</span><span class="sxs-lookup"><span data-stu-id="e09d8-143">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="e09d8-144">Toobe bu adı benzersiz olmalıdır ve tooenter hello adı çalıştığınızda hello portal, zorunlu kılacak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e09d8-144">Note that this name needs toobe unique, and hello portal will enforce that when you attempt tooenter hello name.</span></span> <span data-ttu-id="e09d8-145">Enter farklı bir değer seçerseniz, bu nedenle, değer toosubstitute her oluşumu için ihtiyacınız vardır **SampleWebAppDemo** Bu öğreticide gördüğünüz.</span><span class="sxs-lookup"><span data-stu-id="e09d8-145">Therefore, if you select a enter a different value, you'll need toosubstitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="e09d8-146">Var olan seçin **App Service planı** veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e09d8-146">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="e09d8-147">Yeni bir plan oluşturursanız, fiyatlandırma katmanı, konum ve diğer seçenekleri hello seçin.</span><span class="sxs-lookup"><span data-stu-id="e09d8-147">If you create a new plan, select hello pricing tier, location, and other options.</span></span> <span data-ttu-id="e09d8-148">Merhaba makale App Service planları hakkında daha fazla bilgi için bkz [Azure App Service planlarına ayrıntılı genel bakış](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e09d8-148">For more information on App Service plans, see hello article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Yeni Azure web uygulaması dikey](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="e09d8-150">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e09d8-150">Click **Create**.</span></span>
   
    ![Web uygulaması dikey](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a><span data-ttu-id="e09d8-152">Merhaba yeni web uygulaması için Git yayımlamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="e09d8-152">Enable Git publishing for hello new web app</span></span>
<span data-ttu-id="e09d8-153">Git Azure App Service web uygulamanızı toodeploy kullanabileceğiniz bir dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="e09d8-153">Git is a distributed version control system that you can use toodeploy your Azure App Service web app.</span></span> <span data-ttu-id="e09d8-154">Web uygulamanızda yerel bir Git deposu için yazma hello kod depolayacak ve tooa uzak depoya ileterek kod tooAzure dağıtacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e09d8-154">You'll store hello code you write for your web app in a local Git repository, and you'll deploy your code tooAzure by pushing tooa remote repository.</span></span>   

1. <span data-ttu-id="e09d8-155">Merhaba günlüğüne [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e09d8-155">Log into hello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e09d8-156">**Gözat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e09d8-156">Click **Browse**.</span></span>
3. <span data-ttu-id="e09d8-157">Tıklatın **Web Apps** tooview hello web uygulamaları Azure aboneliğinizle ilişkili listesi.</span><span class="sxs-lookup"><span data-stu-id="e09d8-157">Click **Web Apps** tooview a list of hello web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="e09d8-158">Bu öğreticide oluşturduğunuz hello web uygulaması seçin.</span><span class="sxs-lookup"><span data-stu-id="e09d8-158">Select hello web app you created in this tutorial.</span></span>
5. <span data-ttu-id="e09d8-159">Merhaba web uygulaması dikey penceresinde tıklatın **ayarları** > **sürekli dağıtım**.</span><span class="sxs-lookup"><span data-stu-id="e09d8-159">In hello web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![Azure web uygulaması konağı](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="e09d8-161">Tıklatın **Kaynak Seç > yerel Git deposu**.</span><span class="sxs-lookup"><span data-stu-id="e09d8-161">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="e09d8-162">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e09d8-162">Click **OK**.</span></span>
   
    ![Azure yerel Git depo](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="e09d8-164">Daha önce bir web uygulaması veya diğer App Service uygulama yayımlamak için dağıtım kimlik bilgileri ayarlamadıysanız, bunları şimdi kurun:</span><span class="sxs-lookup"><span data-stu-id="e09d8-164">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="e09d8-165">Tıklatın **ayarları** > **dağıtım kimlik bilgileri**.</span><span class="sxs-lookup"><span data-stu-id="e09d8-165">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="e09d8-166">Merhaba **dağıtım kimlik bilgilerini ayarla** dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e09d8-166">hello **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="e09d8-167">Bir kullanıcı adı ve parola oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e09d8-167">Create a user name and password.</span></span>  <span data-ttu-id="e09d8-168">Git ayarlarken daha sonra bu parola gerekir.</span><span class="sxs-lookup"><span data-stu-id="e09d8-168">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="e09d8-169">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e09d8-169">Click **Save**.</span></span>
9. <span data-ttu-id="e09d8-170">Web uygulamanızın dikey penceresinde tıklayın **ayarlar > Özellikler**.</span><span class="sxs-lookup"><span data-stu-id="e09d8-170">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="e09d8-171">Merhaba, altında gösterilen toois dağıtacaksınız hello uzak Git deposu URL'sini **GIT URL'si**.</span><span class="sxs-lookup"><span data-stu-id="e09d8-171">hello URL of hello remote Git repository that you'll deploy toois shown under **GIT URL**.</span></span>
10. <span data-ttu-id="e09d8-172">Kopya hello **GIT URL'si** hello öğreticide daha sonra kullanmak için değer.</span><span class="sxs-lookup"><span data-stu-id="e09d8-172">Copy hello **GIT URL** value for later use in hello tutorial.</span></span>
    
    ![Azure Git URL'si](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a><span data-ttu-id="e09d8-174">Web uygulaması tooAzure uygulama hizmeti yayımlama</span><span class="sxs-lookup"><span data-stu-id="e09d8-174">Publish your web app tooAzure App Service</span></span>
<span data-ttu-id="e09d8-175">Bu bölümde, yerel bir Git deposu oluşturursunuz ve bu depo tooAzure toodeploy web uygulama tooAzure gönderme.</span><span class="sxs-lookup"><span data-stu-id="e09d8-175">In this section, you will create a local Git repository and push from that repository tooAzure toodeploy your web app tooAzure.</span></span>

1. <span data-ttu-id="e09d8-176">VS Code'da hello seçin **Git** hello sol gezinti çubuğunda seçeneği.</span><span class="sxs-lookup"><span data-stu-id="e09d8-176">In VS Code, select hello **Git** option in hello left navigation bar.</span></span>
   
    ![VS code'da Git simgesi](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="e09d8-178">Seçin **Initialize git deposu** toomake emin çalışma alanınız olduğundan git kaynak denetimi altında.</span><span class="sxs-lookup"><span data-stu-id="e09d8-178">Select **Initialize git repository** toomake sure your workspace is under git source control.</span></span> 
   
    ![Git başlatma](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="e09d8-180">Merhaba komut penceresi açın ve dizinleri toohello dizini, web uygulamanızın değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e09d8-180">Open hello Command Window and change directories toohello directory of your web app.</span></span> <span data-ttu-id="e09d8-181">Ardından, komutu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="e09d8-181">Then, enter hello following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="e09d8-182">Bu komut, burada CRLF sonları ve LF sonları oynayan metin ilgili bir sorunu önler.</span><span class="sxs-lookup"><span data-stu-id="e09d8-182">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="e09d8-183">VS code'da kaydetme iletisi ekleyin ve hello tıklatın **tamamlama tüm** onay simgesi.</span><span class="sxs-lookup"><span data-stu-id="e09d8-183">In VS Code, add a commit message and click hello **Commit All** check icon.</span></span>
   
    ![Git Tümünü Yürüt](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="e09d8-185">Git işleme tamamlandıktan sonra hello Git penceresinde altında listelenen dosyası yok görürsünüz **değişiklikleri**.</span><span class="sxs-lookup"><span data-stu-id="e09d8-185">After Git has completed processing, you'll see that there are no files listed in hello Git window under **Changes**.</span></span> 
   
    ![Git hiçbir değişiklik](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="e09d8-187">Geri toohello komut burada hello komut istemi toohello dizin işaret web uygulamanızı bulunduğu penceresi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e09d8-187">Change back toohello Command Window where hello command prompt points toohello directory where your web app is located.</span></span>
7. <span data-ttu-id="e09d8-188">Merhaba Git daha önce kopyaladığınız URL'yi (".git" alanında biten) kullanarak güncelleştirmeleri tooyour web uygulaması gönderilmesi için uzak bir başvuru oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e09d8-188">Create a remote reference for pushing updates tooyour web app by using hello Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="e09d8-189">Git toosave kimlik bilgilerinizi VS koddan oluşturulan otomatik olarak eklenen tooyour itme komutları yerel olarak olacak şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e09d8-189">Configure Git toosave your credentials locally so that they will be automatically appended tooyour push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="e09d8-190">Değişiklikleri tooAzure komutu aşağıdaki hello girerek iletin.</span><span class="sxs-lookup"><span data-stu-id="e09d8-190">Push your changes tooAzure by entering hello following command.</span></span> <span data-ttu-id="e09d8-191">Bu ilk anında tooAzure sonra tüm hello itme VS koddan komutları mümkün toodo olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e09d8-191">After this initial push tooAzure, you will be able toodo all hello push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="e09d8-192">Azure'da daha önce oluşturduğunuz hello parola istenir.</span><span class="sxs-lookup"><span data-stu-id="e09d8-192">You are prompted for hello password you created earlier in Azure.</span></span> <span data-ttu-id="e09d8-193">**Not: Parolanızı görünür olmaz.**</span><span class="sxs-lookup"><span data-stu-id="e09d8-193">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="e09d8-194">Merhaba komutu yukarıda Hello çıktısını dağıtım başarılı olduğunu belirten bir ileti ile sona erer.</span><span class="sxs-lookup"><span data-stu-id="e09d8-194">hello output from hello above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="e09d8-195">Değişiklikleri tooyour uygulama yaparsanız, doğrudan kodda VS hello seçerek hello yerleşik Git işlevini kullanarak yayımlayabilirsiniz **Commit tüm** seçeneğinin ardından hello tarafından **anında** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="e09d8-195">If you make changes tooyour app, you can republish directly in VS Code using hello built-in Git functionality by selecting hello **Commit All** option followed by hello **Push** option.</span></span> <span data-ttu-id="e09d8-196">Hello bulacaksınız **anında** seçeneği hello açılır menü sonraki toohello kullanılabilir **yürütme tüm** ve **yenileme** düğmeler.</span><span class="sxs-lookup"><span data-stu-id="e09d8-196">You will find hello **Push** option available in hello drop-down menu next toohello **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="e09d8-197">Bir proje üzerinde toocollaborate gerekiyorsa, tooAzure Ftp'den Between tooGitHub Ftp'den düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="e09d8-197">If you need toocollaborate on a project, you should consider pushing tooGitHub in between pushing tooAzure.</span></span>

## <a name="run-hello-app-in-azure"></a><span data-ttu-id="e09d8-198">Azure'da Hello uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e09d8-198">Run hello app in Azure</span></span>
<span data-ttu-id="e09d8-199">Şimdi web uygulamanızı dağıttıysanız, Azure'da barındırılan sırada hello uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e09d8-199">Now that you have deployed your web app, let's run hello app while hosted in Azure.</span></span> 

<span data-ttu-id="e09d8-200">Bu iki yolla yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="e09d8-200">This can be done in two ways:</span></span>

* <span data-ttu-id="e09d8-201">Bir tarayıcı açın ve aşağıdaki gibi web uygulamanızın hello adını girin.</span><span class="sxs-lookup"><span data-stu-id="e09d8-201">Open a browser and enter hello name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="e09d8-202">Buna hello Azure Portal, web uygulamanız için başlangıç web uygulaması dikey bulun ve tıklatın **Gözat** tooview uygulamanızı</span><span class="sxs-lookup"><span data-stu-id="e09d8-202">In hello Azure Portal, locate hello web app blade for your web app, and click **Browse** tooview your app</span></span> 
* <span data-ttu-id="e09d8-203">varsayılan tarayıcınızda.</span><span class="sxs-lookup"><span data-stu-id="e09d8-203">in your default browser.</span></span>

![Azure web uygulaması](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="e09d8-205">Özet</span><span class="sxs-lookup"><span data-stu-id="e09d8-205">Summary</span></span>
<span data-ttu-id="e09d8-206">Bu öğreticide, nasıl öğrenilen toocreate VS code'da bir web uygulaması ve tooAzure dağıtın.</span><span class="sxs-lookup"><span data-stu-id="e09d8-206">In this tutorial, you learned how toocreate a web app in VS Code and deploy it tooAzure.</span></span> <span data-ttu-id="e09d8-207">VS Code hakkında daha fazla bilgi için hello makalesine bakın [neden Visual Studio Code?](https://code.visualstudio.com/Docs/)</span><span class="sxs-lookup"><span data-stu-id="e09d8-207">For more information about VS Code, see hello article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="e09d8-208">App Service web apps hakkında daha fazla bilgi için bkz: [Web Apps'e genel bakış](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e09d8-208">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 

