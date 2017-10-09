---
title: aaaCI/Jenkins tooAzure Team Services ile sanal makineleri CD'den | Microsoft Docs
description: "Sürekli Tümleştirme (CI) ve Visual Studio Team Services (VSTS) veya Microsoft Team Foundation Server (TFS) yayın yönetimini Jenkins tooAzure VM'lerin kullanarak bir Node.js uygulaması sürekli dağıtımını (CD) ayarlama"
author: ahomer
manager: douge
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/15/2017
ms.author: ahomer
ms.custom: mvc
ms.openlocfilehash: 400ae34cbdf45da65351811c0ff6ff5d61ef862c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-toolinux-vms-using-jenkins-and-team-services"></a><span data-ttu-id="f21f9-103">Uygulama tooLinux sanal makineleri dağıtmak Jenkins ve Team Services kullanma</span><span class="sxs-lookup"><span data-stu-id="f21f9-103">Deploy your app tooLinux VMs using Jenkins and Team Services</span></span>

<span data-ttu-id="f21f9-104">Sürekli Tümleştirme (CI) ve sürekli dağıtımı (CD) olarak derleme, sürüm ve kullanabilirsiniz, kodunuzu dağıtmak bir ardışık düzen olur.</span><span class="sxs-lookup"><span data-stu-id="f21f9-104">Continuous integration (CI) and continuous deployment (CD) is a pipeline by which you can build, release, and deploy your code.</span></span> <span data-ttu-id="f21f9-105">Team Services için dağıtım tooAzure CI/CD Otomasyon Araçları'nın tam, tam özellikli bir kümesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="f21f9-105">Team Services provides a complete, fully featured set of CI/CD automation tools for deployment tooAzure.</span></span> <span data-ttu-id="f21f9-106">Jenkins CI/CD Otomasyon de sağlayan bir Popüler 3. taraf CI/CD sunucu tabanlı araçtır.</span><span class="sxs-lookup"><span data-stu-id="f21f9-106">Jenkins is a popular 3rd-party CI/CD server-based tool that also provides CI/CD automation.</span></span> <span data-ttu-id="f21f9-107">Her iki birlikte toocustomize kullanabilirsiniz, bulut uygulaması veya hizmeti nasıl teslim.</span><span class="sxs-lookup"><span data-stu-id="f21f9-107">You can use both together toocustomize how you deliver your cloud app or service.</span></span>

<span data-ttu-id="f21f9-108">Bu öğreticide kullandığınız Jenkins toobuild bir **Node.js web uygulamasına**ve Visual Studio Team Services toodeploy, tooa [dağıtım grubu](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) Linux sanal makineleri içeren.</span><span class="sxs-lookup"><span data-stu-id="f21f9-108">In this tutorial, you use Jenkins toobuild a **Node.js web app**, and Visual Studio Team Services toodeploy it tooa [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) containing Linux virtual machines.</span></span>

<span data-ttu-id="f21f9-109">Yapacaklarınız:</span><span class="sxs-lookup"><span data-stu-id="f21f9-109">You will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f21f9-110">Jenkins uygulamanızda derleme</span><span class="sxs-lookup"><span data-stu-id="f21f9-110">Build your app in Jenkins</span></span>
> * <span data-ttu-id="f21f9-111">Jenkins Team Services tümleştirme için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f21f9-111">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="f21f9-112">Azure sanal makineler hello için bir dağıtım grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="f21f9-112">Create a deployment group for hello Azure virtual machines</span></span>
> * <span data-ttu-id="f21f9-113">Merhaba VM'ler yapılandırır ve hello uygulamayı dağıtır bir yayın tanımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="f21f9-113">Create a release definition that configures hello VMs and deploys hello app</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f21f9-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="f21f9-114">Before you begin</span></span>

* <span data-ttu-id="f21f9-115">Erişim tooa Jenkins hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f21f9-115">You need access tooa Jenkins account.</span></span> <span data-ttu-id="f21f9-116">Jenkins server henüz oluşturmadıysanız, bkz: [Jenkins belgelerine](https://jenkins.io/doc/).</span><span class="sxs-lookup"><span data-stu-id="f21f9-116">If you have not yet created a Jenkins server, see [Jenkins Documentation](https://jenkins.io/doc/).</span></span> 

* <span data-ttu-id="f21f9-117">Tooyour Team Services hesabı oturum (`https://{youraccount}.visualstudio.com`).</span><span class="sxs-lookup"><span data-stu-id="f21f9-117">Sign in tooyour Team Services account (`https://{youraccount}.visualstudio.com`).</span></span> 
  <span data-ttu-id="f21f9-118">Alabileceğiniz bir [serbest Team Services hesabı](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span><span class="sxs-lookup"><span data-stu-id="f21f9-118">You can get a [free Team Services account](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span></span>

  > [!NOTE]
  > <span data-ttu-id="f21f9-119">Daha fazla bilgi için bkz: [tooTeam Hizmetleri'ne Bağlama](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span><span class="sxs-lookup"><span data-stu-id="f21f9-119">For more information, see [Connect tooTeam Services](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span></span>

* <span data-ttu-id="f21f9-120">Zaten yoksa, kişisel erişim belirteci (PAT), Team Services hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f21f9-120">Create a personal access token (PAT) in your Team Services account if you don't already have one.</span></span> <span data-ttu-id="f21f9-121">Jenkins bu bilgileri tooaccess Team Services hesabınızın gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f21f9-121">Jenkins requires this information tooaccess your Team Services account.</span></span>
  <span data-ttu-id="f21f9-122">Okuma [nasıl oluşturabilirim kişisel erişim belirteci Team Services ve TFS için](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn nasıl toogenerate biri.</span><span class="sxs-lookup"><span data-stu-id="f21f9-122">Read [How do I create a personal access token for Team Services and TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn how toogenerate one.</span></span>

## <a name="get-hello-sample-app"></a><span data-ttu-id="f21f9-123">Merhaba örnek uygulamayı Al</span><span class="sxs-lookup"><span data-stu-id="f21f9-123">Get hello sample app</span></span>

<span data-ttu-id="f21f9-124">Git deposunda saklanan bir uygulama toodeploy gerekir.</span><span class="sxs-lookup"><span data-stu-id="f21f9-124">You need an app toodeploy stored in a Git repository.</span></span>
<span data-ttu-id="f21f9-125">Bu öğretici için kullandığınız olan öneririz [Github'dan Bu örnek uygulama](https://github.com/azooinmyluggage/fabrikam-node).</span><span class="sxs-lookup"><span data-stu-id="f21f9-125">For this tutorial, we recommend you use [this sample app available from GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span></span>

1. <span data-ttu-id="f21f9-126">Bu uygulamanın çatalı oluşturun ve bu öğreticinin daha sonraki adımlarda kullanılmak hello konumu (URL) not edin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-126">Create a fork of this app and take note of hello location (URL) for use in later steps of this tutorial.</span></span>

1. <span data-ttu-id="f21f9-127">Merhaba çatalı olun **ortak** tooGitHub daha sonra bağlanmayı toosimplify.</span><span class="sxs-lookup"><span data-stu-id="f21f9-127">Make hello fork **public** toosimplify connecting tooGitHub later.</span></span>

> [!NOTE]
> <span data-ttu-id="f21f9-128">Daha fazla bilgi için bkz: [bir depoyu Çatallaştırma](https://help.github.com/articles/fork-a-repo/) ve [özel bir depo ortak yapma](https://help.github.com/articles/making-a-private-repository-public/).</span><span class="sxs-lookup"><span data-stu-id="f21f9-128">For more information, see [Fork a repo](https://help.github.com/articles/fork-a-repo/) and [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/).</span></span>

> [!NOTE]
> <span data-ttu-id="f21f9-129">Merhaba uygulama kullanarak yapılmış [Yeoman](http://yeoman.io/learning/index.html); kullandığı **Express**, **bower**, ve **grunt**; ve bazı sahip **npm**paketler bağımlılık olarak.</span><span class="sxs-lookup"><span data-stu-id="f21f9-129">hello app was built using [Yeoman](http://yeoman.io/learning/index.html); it uses **Express**, **bower**, and **grunt**; and it has some **npm** packages as dependencies.</span></span>
> <span data-ttu-id="f21f9-130">Merhaba örnek uygulamayı içeren bir dizi [Azure Resource Manager şablonları](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) olan kullanılan toodynamically oluşturduğunuz hello sanal makine dağıtımı için Azure üzerinde.</span><span class="sxs-lookup"><span data-stu-id="f21f9-130">hello sample app contains a set of [Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) that are used toodynamically create hello virtual machines for deployment on Azure.</span></span> <span data-ttu-id="f21f9-131">Bu şablonlar hello görevleri tarafından kullanılan [Team Services sürüm tanımı](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span><span class="sxs-lookup"><span data-stu-id="f21f9-131">These templates are used by tasks in hello [Team Services release definition](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span></span>
> <span data-ttu-id="f21f9-132">Merhaba ana şablon bir ağ güvenlik grubu, bir sanal makine ve sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f21f9-132">hello main template creates a network security group, a virtual machine, and a virtual network.</span></span> <span data-ttu-id="f21f9-133">Bir ortak IP adresini atar ve gelen bağlantı noktası 80'i açar.</span><span class="sxs-lookup"><span data-stu-id="f21f9-133">It assigns a public IP address and opens inbound port 80.</span></span> <span data-ttu-id="f21f9-134">Ayrıca, hello dağıtım grubu çok select hello makineler tooreceive hello dağıtım tarafından kullanılan bir etiket ekler.</span><span class="sxs-lookup"><span data-stu-id="f21f9-134">It also adds a tag that is used by hello deployment group too select hello machines tooreceive hello deployment.</span></span>
>
> <span data-ttu-id="f21f9-135">Merhaba örnek, Nginx ayarlar ve hello uygulamayı dağıtır bir betik de içerir.</span><span class="sxs-lookup"><span data-stu-id="f21f9-135">hello sample also contains a script that sets up Nginx and deploys hello app.</span></span> <span data-ttu-id="f21f9-136">Her hello sanal makineler üzerinde yürütülür.</span><span class="sxs-lookup"><span data-stu-id="f21f9-136">It is executed on each of hello virtual machines.</span></span> <span data-ttu-id="f21f9-137">Özellikle, hello betik düğümünde, Nginx ve PM2 yükler; Nginx ve PM2 yapılandırır; ardından hello düğüm uygulama başlatır.</span><span class="sxs-lookup"><span data-stu-id="f21f9-137">Specifically, hello script installs Node, Nginx, and PM2; configures Nginx and PM2; then starts hello Node app.</span></span>

## <a name="configure-jenkins-plugins"></a><span data-ttu-id="f21f9-138">Jenkins eklentileri yapılandırın</span><span class="sxs-lookup"><span data-stu-id="f21f9-138">Configure Jenkins plugins</span></span>

<span data-ttu-id="f21f9-139">İlk olarak, iki Jenkins eklentileri için yapılandırmanız gerekir **NodeJS** ve **Team Services ile tümleştirme**.</span><span class="sxs-lookup"><span data-stu-id="f21f9-139">First, you must configure two Jenkins plugins for **NodeJS** and **Integration with Team Services**.</span></span>

1. <span data-ttu-id="f21f9-140">Jenkins hesabınızı açın ve seçin **yönetmek Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="f21f9-140">Open your Jenkins account and choose **Manage Jenkins**.</span></span>

1. <span data-ttu-id="f21f9-141">Merhaba, **yönetmek Jenkins** sayfasında, **eklentileri yönetme**.</span><span class="sxs-lookup"><span data-stu-id="f21f9-141">In hello **Manage Jenkins** page, choose **Manage Plugins**.</span></span>

1. <span data-ttu-id="f21f9-142">Filtre hello listesi toolocate hello **NodeJS** eklentisi ve yeniden başlatma gerekmeden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-142">Filter hello list toolocate hello **NodeJS** plugin and install it without restart.</span></span>

   ![Merhaba NodeJS eklentisi tooJenkins ekleme](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. <span data-ttu-id="f21f9-144">Filtre hello listesi toofind hello **Team Foundation Server** eklentisini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-144">Filter hello list toofind hello **Team Foundation Server** plugin and install it.</span></span> <span data-ttu-id="f21f9-145">(Bu eklenti çalışır Team Services ve Team Foundation Server için.) Jenkins yeniden başlatılması gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="f21f9-145">(This plug-in works for both Team Services and Team Foundation Server.) Restarting Jenkins is not necessary.</span></span>

## <a name="configure-jenkins-build-for-nodejs"></a><span data-ttu-id="f21f9-146">Node.js için Jenkins yapı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f21f9-146">Configure Jenkins build for Node.js</span></span>

<span data-ttu-id="f21f9-147">Jenkins, yeni bir derleme projesi oluşturun ve aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="f21f9-147">In Jenkins, create a new build project and configure it as follows:</span></span>

1. <span data-ttu-id="f21f9-148">Merhaba, **genel** sekmesinde, yapı projeniz için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-148">In hello **General** tab, enter a name for your build project.</span></span>

1. <span data-ttu-id="f21f9-149">Merhaba, **kaynak kodu Yönetimi** sekmesine **Git** ve hello deposu ve uygulama kodunuzu içeren hello şube hello ayrıntılarını girin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-149">In hello **Source Code Management** tab, select **Git** and enter hello details of hello repository and hello branch containing your app code.</span></span>

   ![Depodaki tooyour derleme ekleyin](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > <span data-ttu-id="f21f9-151">Deponuzda ortak değilse seçin **Ekle** ve kimlik bilgilerini tooconnect tooit sağlayın.</span><span class="sxs-lookup"><span data-stu-id="f21f9-151">If your repository is not public, choose **Add** and provide credentials tooconnect tooit.</span></span>

1. <span data-ttu-id="f21f9-152">Merhaba, **yapı tetikleyicileri** sekmesine **yoklama SCM** ve hello zamanlama girin `H/03 * * * *` toopoll hello Git deposu değişiklikleri üç dakikada.</span><span class="sxs-lookup"><span data-stu-id="f21f9-152">In hello **Build Triggers** tab, select **Poll SCM** and enter hello schedule `H/03 * * * *` toopoll hello Git repository for changes every three minutes.</span></span> 

1. <span data-ttu-id="f21f9-153">Merhaba, **yapı ortamı** sekmesine **sağlayan düğüm &amp; npm bin / klasör yolu** ve girin `NodeJS` hello düğümü JS yükleme değeri için.</span><span class="sxs-lookup"><span data-stu-id="f21f9-153">In hello **Build Environment** tab, select **Provide Node &amp; npm bin/ folder PATH** and enter `NodeJS` for hello Node JS Installation value.</span></span> <span data-ttu-id="f21f9-154">Bırakın **npmrc dosya** "sistem varsayılan kullanır." olarak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="f21f9-154">Leave **npmrc file** set to "use system default."</span></span>

1. <span data-ttu-id="f21f9-155">Merhaba, **yapı** sekmesinde, hello komutu girin `npm install` tooensure tüm bağımlılıkları güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="f21f9-155">In hello **Build** tab, enter hello command `npm install` tooensure all dependencies are updated.</span></span>

## <a name="configure-jenkins-for-team-services-integration"></a><span data-ttu-id="f21f9-156">Jenkins Team Services tümleştirme için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f21f9-156">Configure Jenkins for Team Services integration</span></span>

1. <span data-ttu-id="f21f9-157">Merhaba, **oluşturma sonrası eylemleri** sekmesinde için **dosyaları tooarchive**, girin `**/*` tooinclude tüm dosyalar.</span><span class="sxs-lookup"><span data-stu-id="f21f9-157">In hello **Post-build Actions** tab, for **Files tooarchive**, enter `**/*` tooinclude all files.</span></span>

1. <span data-ttu-id="f21f9-158">İçin **tetiklemek TFS/Team Services sürümde**, hesabınızın hello tam URL'sini girin (gibi `https://your-account-name.visualstudio.com`), hello proje adı (daha sonra oluşturulan) hello yayın tanımı için bir ad ve kimlik bilgilerini tooconnect tooyour hesabı hello.</span><span class="sxs-lookup"><span data-stu-id="f21f9-158">For **Trigger release in TFS/Team Services**, enter hello full URL of your account (such as `https://your-account-name.visualstudio.com`), hello project name, a name for hello release definition (created later), and hello credentials tooconnect tooyour account.</span></span>
   <span data-ttu-id="f21f9-159">Kullanıcı adınızı ve hello daha önce oluşturduğunuz PAT gerekir.</span><span class="sxs-lookup"><span data-stu-id="f21f9-159">You need your user name and hello PAT you created earlier.</span></span> 

   ![Jenkins oluşturma sonrası eylemleri yapılandırma](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. <span data-ttu-id="f21f9-161">Merhaba yapı projeyi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-161">Save hello build project.</span></span>

## <a name="create-a-jenkins-service-endpoint"></a><span data-ttu-id="f21f9-162">Jenkins hizmet uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="f21f9-162">Create a Jenkins service endpoint</span></span>

<span data-ttu-id="f21f9-163">Hizmet uç noktası Team Services tooconnect tooJenkins sağlar.</span><span class="sxs-lookup"><span data-stu-id="f21f9-163">A service endpoint allows Team Services tooconnect tooJenkins.</span></span>

1. <span data-ttu-id="f21f9-164">Açık hello **Hizmetleri** Team Services, açık hello sayfasında **yeni hizmet uç noktası** listesinde ve seçin **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="f21f9-164">Open hello **Services** page in Team Services, open hello **New Service Endpoint** list, and choose **Jenkins**.</span></span>

   ![Jenkins uç nokta ekleyin](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. <span data-ttu-id="f21f9-166">Toorefer toothis bağlantısının kullanacağı bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-166">Enter a name you will use toorefer toothis connection.</span></span>

1. <span data-ttu-id="f21f9-167">Merhaba Jenkins sunucunuzun URL'sini girin ve değer hello **kabul güvenilmeyen SSL sertifikalarını** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="f21f9-167">Enter hello URL of your Jenkins server, and tick hello **Accept untrusted SSL certificates** option.</span></span>

1. <span data-ttu-id="f21f9-168">Jenkins hesabınızın Hello kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-168">Enter hello user name and password for your Jenkins account.</span></span>

1. <span data-ttu-id="f21f9-169">Seçin **bağlantısını doğrulama** bilgi hello toocheck doğru.</span><span class="sxs-lookup"><span data-stu-id="f21f9-169">Choose **Verify connection** toocheck that hello information is correct.</span></span>

1. <span data-ttu-id="f21f9-170">Seçin **Tamam** toocreate hello Hizmeti uç noktası.</span><span class="sxs-lookup"><span data-stu-id="f21f9-170">Choose **OK** toocreate hello service endpoint.</span></span>

## <a name="create-a-deployment-group"></a><span data-ttu-id="f21f9-171">Bir dağıtım grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="f21f9-171">Create a deployment group</span></span>

<span data-ttu-id="f21f9-172">Gereksinim duyduğunuz bir [dağıtım grubu](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) çok hello sanal makineler içeriyor.</span><span class="sxs-lookup"><span data-stu-id="f21f9-172">You need a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) too contain hello virtual machines.</span></span>

1. <span data-ttu-id="f21f9-173">Açık hello **sürümleri** hello sekmesinde **yapı &amp; sürüm** hub sonra açık hello **dağıtım grupları** sekmesini tıklatın ve seçin **+ yeni**.</span><span class="sxs-lookup"><span data-stu-id="f21f9-173">Open hello **Releases** tab of hello **Build &amp; Release** hub, then open hello **Deployment groups** tab, and choose **+ New**.</span></span>

1. <span data-ttu-id="f21f9-174">Merhaba dağıtım grubu ve isteğe bağlı bir açıklama için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-174">Enter a name for hello deployment group, and an optional description.</span></span>
   <span data-ttu-id="f21f9-175">Ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="f21f9-175">Then choose **Create**.</span></span>

<span data-ttu-id="f21f9-176">Hello Azure kaynak grubu dağıtımı görev oluşturur ve hello Azure Resource Manager şablonu kullanarak çalıştığında hello VM'ler kaydeder.</span><span class="sxs-lookup"><span data-stu-id="f21f9-176">hello Azure Resource Group Deployment task creates and registers hello VMs when it runs using hello Azure Resource Manager template.</span></span>
<span data-ttu-id="f21f9-177">Toocreate gerek yoktur ve hello sanal makineleri kendiniz kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-177">You don't need toocreate and register hello virtual machines yourself.</span></span>

## <a name="create-a-release-definition"></a><span data-ttu-id="f21f9-178">Bir yayın tanımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="f21f9-178">Create a release definition</span></span>

<span data-ttu-id="f21f9-179">Bir yayın tanımı hello işlem Team Services toodeploy hello uygulama yürütecek belirtir.</span><span class="sxs-lookup"><span data-stu-id="f21f9-179">A release definition specifies hello process Team Services will execute toodeploy hello app.</span></span>
<span data-ttu-id="f21f9-180">Team Services toocreate hello yayın tanımı:</span><span class="sxs-lookup"><span data-stu-id="f21f9-180">toocreate hello release definition in Team Services:</span></span>

1. <span data-ttu-id="f21f9-181">Açık hello **sürümleri** hello sekmesinde **yapı &amp; yayın** hub, açık hello  **+**  açılan hello sürüm tanımlarını listesinde ve seçin Merhaba **oluşturma yayın tanımı**.</span><span class="sxs-lookup"><span data-stu-id="f21f9-181">Open hello **Releases** tab of hello **Build &amp; Release** hub, open hello **+** drop-down in hello list of release definitions, and choose hello **Create release definition**.</span></span> 

1. <span data-ttu-id="f21f9-182">Select hello **boş** şablonu ve **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="f21f9-182">Select hello **Empty** template and choose **Next**.</span></span>

1. <span data-ttu-id="f21f9-183">Merhaba, **yapıları** bölümünde, tıklayın **bir yapı bağlantı** ve seçin **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="f21f9-183">In hello **Artifacts** section, click on **Link an Artifact** and choose **Jenkins**.</span></span> <span data-ttu-id="f21f9-184">Jenkins hizmet uç noktası bağlantınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-184">Select your Jenkins service endpoint connection.</span></span> <span data-ttu-id="f21f9-185">Ardından hello Jenkins kaynak iş seçip **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="f21f9-185">Then select hello Jenkins source job and choose **Create**.</span></span> 

1. <span data-ttu-id="f21f9-186">Merhaba yeni yayın tanımı, seçin **+ görev ekleme** ve ekleme bir **Azure kaynak grubu dağıtımı** görev toohello varsayılan ortamı.</span><span class="sxs-lookup"><span data-stu-id="f21f9-186">In hello new release definition, choose **+ Add tasks** and add an **Azure Resource Group Deployment** task toohello default environment.</span></span>

1. <span data-ttu-id="f21f9-187">Merhaba açılan ok sonraki toohello seçin **+ Ekle görevleri** bağlantı ve bir dağıtım grubu aşaması toohello tanımını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-187">Choose hello drop down arrow next toohello **+ Add tasks** link and add a deployment group phase toohello definition.</span></span>

   ![Bir dağıtım grubu aşaması ekleme](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. <span data-ttu-id="f21f9-189">Merhaba Hello görev Kataloğu'nda açmak **yardımcı programı** bölümünde ve hello bir örnek ekler **Kabuk betiği** görev.</span><span class="sxs-lookup"><span data-stu-id="f21f9-189">In hello Task catalog, open hello **Utility** section and add an instance of hello **Shell Script** task.</span></span>

1. <span data-ttu-id="f21f9-190">Hello Azure kaynak grubu dağıtımı görevde kullanılan hello parametreleri şablonu hello yönetici kullanılan parola tooconnect toohello VM'ler ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f21f9-190">hello parameters template used in hello Azure Resource Group Deployment task sets hello admin password used tooconnect toohello VMs.</span></span>
   <span data-ttu-id="f21f9-191">Merhaba değişkenle bu parola **$(adminpassword)**:</span><span class="sxs-lookup"><span data-stu-id="f21f9-191">You provide this password with hello variable **$(adminpassword)**:</span></span>
   
   - <span data-ttu-id="f21f9-192">Açık hello **değişkenleri** sekmesi ve hello **değişkenleri** bölümünde, hello adı girin `adminpassword`.</span><span class="sxs-lookup"><span data-stu-id="f21f9-192">Open hello **Variables** tab and, in hello **Variables** section, enter hello name `adminpassword`.</span></span>

   - <span data-ttu-id="f21f9-193">Merhaba yönetici parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-193">Enter hello administrator password.</span></span>

   - <span data-ttu-id="f21f9-194">Merhaba "asma" simgesini sonraki toohello değeri metin kutusu tooprotect hello parola seçin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-194">Choose hello "padlock" icon next toohello value textbox tooprotect hello password.</span></span> 

## <a name="configure-hello-azure-resource-group-deployment-task"></a><span data-ttu-id="f21f9-195">Hello Azure kaynak grubu dağıtımı görev yapılandırın</span><span class="sxs-lookup"><span data-stu-id="f21f9-195">Configure hello Azure Resource Group Deployment task</span></span>

<span data-ttu-id="f21f9-196">Merhaba **Azure kaynak grubu dağıtımı** kullanılan toocreate hello dağıtım grubu bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="f21f9-196">hello **Azure Resource Group Deployment** task is used toocreate hello deployment group.</span></span> <span data-ttu-id="f21f9-197">Aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="f21f9-197">Configure it as follows:</span></span>

* <span data-ttu-id="f21f9-198">**Azure aboneliği:** altında hello listesinden bir bağlantı seçin **kullanılabilir Azure hizmet bağlantıları**.</span><span class="sxs-lookup"><span data-stu-id="f21f9-198">**Azure Subscription:** Select a connection from hello list under **Available Azure Service Connections**.</span></span> 
  <span data-ttu-id="f21f9-199">Hiçbir bağlantı görünüyorsa seçin **Yönet**seçin **yeni hizmet uç noktası** sonra **Azure Resource Manager**ve hello istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-199">If no connections appear, choose **Manage**, select **New Service Endpoint** then **Azure Resource Manager**, and follow hello prompts.</span></span>
  <span data-ttu-id="f21f9-200">Dönüş tooyour yayın tanımı, yenileme hello **AzureRM abonelik** listesini ve oluşturduğunuz select hello bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="f21f9-200">Return tooyour release definition, refresh hello **AzureRM Subscription** list, and select hello connection you created.</span></span>

* <span data-ttu-id="f21f9-201">**Kaynak grubu**: daha önce oluşturduğunuz hello kaynak grubunun adını girin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-201">**Resource group**: Enter a name of hello resource group you created earlier.</span></span>

* <span data-ttu-id="f21f9-202">**Konum**: hello dağıtımı için bir bölge seçin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-202">**Location**: Select a region for hello deployment.</span></span>

  ![Yeni bir kaynak grubu oluşturma](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* <span data-ttu-id="f21f9-204">**Şablon konumu**:`URL of hello file`</span><span class="sxs-lookup"><span data-stu-id="f21f9-204">**Template location**: `URL of hello file`</span></span>

* <span data-ttu-id="f21f9-205">**Şablon bağlantısı**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span><span class="sxs-lookup"><span data-stu-id="f21f9-205">**Template link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span></span>

* <span data-ttu-id="f21f9-206">**Şablon parametreleri bağlantısı**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span><span class="sxs-lookup"><span data-stu-id="f21f9-206">**Template parameters link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span></span>

* <span data-ttu-id="f21f9-207">**Şablon parametreleri geçersiz kılma**: hello listesini geçersiz kılma değerleri, örneğin: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span><span class="sxs-lookup"><span data-stu-id="f21f9-207">**Override template parameters**: A list of hello override values, for example: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span></span><br /><span data-ttu-id="f21f9-208">Merhaba {yer tutucuları} için belirli kendi değerlerinizi yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-208">Insert your own specific values for hello {placeholders}.</span></span> 

* <span data-ttu-id="f21f9-209">**Önkoşullar etkinleştirme**:`Configure with Deployment Group agent`</span><span class="sxs-lookup"><span data-stu-id="f21f9-209">**Enable prerequisites**: `Configure with Deployment Group agent`</span></span>

* <span data-ttu-id="f21f9-210">**TFS/VSTS endpoint**: seçin **Ekle** ve "Yeni Team Foundation Server/Team Services Bağlantısı Ekle" Merhaba iletişim kutusunda seçin **belirteç tabanlı kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="f21f9-210">**TFS/VSTS endpoint**: Choose **Add** and, in hello "Add new Team Foundation Server/Team Services Connection" dialog, select **Token Based Authentication**.</span></span> <span data-ttu-id="f21f9-211">Merhaba bağlantının adını ve takım projenizin hello URL'sini girin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-211">Enter a name of hello connection and hello URL of your team project.</span></span> <span data-ttu-id="f21f9-212">Ardından oluşturmak ve girin bir [kişisel erişim belirteci (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) tooauthenticate hello bağlantı tooyour takım projesi.</span><span class="sxs-lookup"><span data-stu-id="f21f9-212">Then generate and enter a [Personal Access Token (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) tooauthenticate hello connection tooyour team project.</span></span>

  ![Kişisel oluşturma erişim belirteci](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* <span data-ttu-id="f21f9-214">**Takım projesi**: geçerli projenizi seçin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-214">**Team project**: Select your current project.</span></span>

* <span data-ttu-id="f21f9-215">**Dağıtım grubu**: girin hello için kullanılan aynı dağıtım grubu adını hello **kaynak grubu** parametresi.</span><span class="sxs-lookup"><span data-stu-id="f21f9-215">**Deployment Group**: Enter hello same deployment group name as you used for hello **Resource group** parameter.</span></span>

<span data-ttu-id="f21f9-216">hello Azure kaynak grubu dağıtımı görev için Hello varsayılan ayarları toocreate olan veya bir kaynak ve toodo kadar artımlı bir şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-216">hello default settings for hello Azure Resource Group Deployment task are toocreate or update a resource, and toodo so incrementally.</span></span> <span data-ttu-id="f21f9-217">Merhaba görev hello VM'ler hello ilk kez çalıştırır ve daha sonra yalnızca güncelleştirmenizi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f21f9-217">hello task creates hello VMs hello first time it runs, and subsequently just update them.</span></span>

## <a name="configure-hello-shell-script-task"></a><span data-ttu-id="f21f9-218">Merhaba Kabuk betiği görev yapılandırın</span><span class="sxs-lookup"><span data-stu-id="f21f9-218">Configure hello Shell Script task</span></span>

<span data-ttu-id="f21f9-219">Merhaba **Kabuk betiği** kullanılan tooprovide hello yapılandırması için bir komut dosyası toorun her sunucu tooinstall Node.js ve başlangıç hello uygulamada bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="f21f9-219">hello **Shell Script** task is used tooprovide hello configuration for a script toorun on each server tooinstall Node.js and start hello app.</span></span> <span data-ttu-id="f21f9-220">Aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="f21f9-220">Configure it as follows:</span></span>

* <span data-ttu-id="f21f9-221">**Komut dosyası yolu**:`$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span><span class="sxs-lookup"><span data-stu-id="f21f9-221">**Script Path**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span></span>

* <span data-ttu-id="f21f9-222">**Çalışma belirtin dizin**:`Checked`</span><span class="sxs-lookup"><span data-stu-id="f21f9-222">**Specify Working Directory**: `Checked`</span></span>

* <span data-ttu-id="f21f9-223">**Çalışma dizini**:`$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span><span class="sxs-lookup"><span data-stu-id="f21f9-223">**Working Directory**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span></span>
   
## <a name="rename-and-save-hello-release-definition"></a><span data-ttu-id="f21f9-224">Yeniden adlandırın ve hello yayın tanımını kaydet</span><span class="sxs-lookup"><span data-stu-id="f21f9-224">Rename and save hello release definition</span></span>

1. <span data-ttu-id="f21f9-225">Merhaba adını, belirtilen hello yayın tanımı toohello Düzenle **oluşturma sonrası eylemleri** Jenkins hello derlemede sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="f21f9-225">Edit hello name of hello release definition toohello name you specified in the **Post-build Actions** tab of hello build in Jenkins.</span></span> <span data-ttu-id="f21f9-226">Merhaba kaynak yapıları güncelleştirildiğinde Jenkins bu adı toobe mümkün tootrigger yeni bir sürüm gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f21f9-226">Jenkins requires this name toobe able tootrigger a new release when hello source artifacts are updated.</span></span>

1. <span data-ttu-id="f21f9-227">İsteğe bağlı olarak, hello adına tıklayarak hello ortamı hello adını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-227">Optionally, change hello name of hello environment by clicking on hello name.</span></span> 

1. <span data-ttu-id="f21f9-228">Seçin **kaydetmek**ve seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="f21f9-228">Choose **Save**, and choose **OK**.</span></span>

## <a name="start-a-manual-deployment"></a><span data-ttu-id="f21f9-229">El ile dağıtımı Başlat</span><span class="sxs-lookup"><span data-stu-id="f21f9-229">Start a manual deployment</span></span>

1. <span data-ttu-id="f21f9-230">Seçin **+ yayın** seçip **sürüm oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="f21f9-230">Choose **+ Release** and select **Create Release**.</span></span>

1. <span data-ttu-id="f21f9-231">Merhaba yapı, tamamlandı hello vurgulanan aşağı açılan listeden seçip **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="f21f9-231">Select hello build you completed in hello highlighted drop-down list and choose **Create**.</span></span>

1. <span data-ttu-id="f21f9-232">Merhaba sürüm bağlantı hello açılan iletide seçin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-232">Choose hello release link in hello popup message.</span></span> <span data-ttu-id="f21f9-233">Örneğin: "yayın **sürüm 1** oluşturuldu."</span><span class="sxs-lookup"><span data-stu-id="f21f9-233">For example: "Release **Release-1** has been created."</span></span>

1. <span data-ttu-id="f21f9-234">Açık hello **günlükleri** sekmesinde toowatch hello yayın konsol çıkışı.</span><span class="sxs-lookup"><span data-stu-id="f21f9-234">Open hello **Logs** tab toowatch hello release console output.</span></span>

1. <span data-ttu-id="f21f9-235">Tarayıcınızda, hello URL'yi açın hello sunucuların birini tooyour dağıtım grubuna eklendi.</span><span class="sxs-lookup"><span data-stu-id="f21f9-235">In your browser, open hello URL of one of hello servers you added tooyour deployment group.</span></span> <span data-ttu-id="f21f9-236">Örneğin, girin`http://{your-server-ip-address}`</span><span class="sxs-lookup"><span data-stu-id="f21f9-236">For example, enter `http://{your-server-ip-address}`</span></span>

## <a name="start-a-cicd-deployment"></a><span data-ttu-id="f21f9-237">CI/CD dağıtım Başlat</span><span class="sxs-lookup"><span data-stu-id="f21f9-237">Start a CI/CD deployment</span></span>

1. <span data-ttu-id="f21f9-238">Hello tanımı sürüm, hello seçeneğinin işaretini kaldırın **etkin** hello onay kutusu **denetim seçeneklerini** hello Azure kaynak grubu dağıtımı görev için hello ayarları bölümü.</span><span class="sxs-lookup"><span data-stu-id="f21f9-238">In hello release definition, uncheck hello **Enabled** checkbox in hello **Control Options** section of hello settings for hello Azure Resource Group Deployment task.</span></span>
   <span data-ttu-id="f21f9-239">Gelecekteki dağıtımlar toohello için var olan dağıtım grubu, toore gerekmez-bu görevi yürütün.</span><span class="sxs-lookup"><span data-stu-id="f21f9-239">For future deployments toohello existing deployment group, you do not need toore-execute this task.</span></span>

1. <span data-ttu-id="f21f9-240">Toohello kaynak Git deposu dönüp hello Merhaba içeriğine değiştirmek **h1** hello dosyasında başlık [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span><span class="sxs-lookup"><span data-stu-id="f21f9-240">Go toohello source Git repository and modify hello contents of hello **h1** heading in hello file [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span></span>

1. <span data-ttu-id="f21f9-241">Değişikliğiniz uygulayın.</span><span class="sxs-lookup"><span data-stu-id="f21f9-241">Commit your change.</span></span>

1. <span data-ttu-id="f21f9-242">Birkaç dakika sonra hello oluşturulan yeni bir sürüm görürsünüz **sürümleri** Team Services veya TFS sayfası.</span><span class="sxs-lookup"><span data-stu-id="f21f9-242">After a few minutes, you will see a new release created in hello **Releases** page of Team Services or TFS.</span></span> <span data-ttu-id="f21f9-243">Merhaba yayın toosee hello dağıtım gerçekleşmesini açın.</span><span class="sxs-lookup"><span data-stu-id="f21f9-243">Open hello release toosee hello deployment taking place.</span></span> <span data-ttu-id="f21f9-244">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="f21f9-244">Congratulations!</span></span>

## <a name="next-steps"></a><span data-ttu-id="f21f9-245">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="f21f9-245">Next Steps</span></span>

<span data-ttu-id="f21f9-246">Bu öğreticide, Jenkins derleme ve sürüm için Team Services kullanarak bir uygulama tooAzure hello dağıtımını otomatik.</span><span class="sxs-lookup"><span data-stu-id="f21f9-246">In this tutorial, you automated hello deployment of an app tooAzure using Jenkins build and Team Services for release.</span></span> <span data-ttu-id="f21f9-247">Şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="f21f9-247">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f21f9-248">Jenkins uygulamanızda derleme</span><span class="sxs-lookup"><span data-stu-id="f21f9-248">Build your app in Jenkins</span></span>
> * <span data-ttu-id="f21f9-249">Jenkins Team Services tümleştirme için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f21f9-249">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="f21f9-250">Azure sanal makineler hello için bir dağıtım grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="f21f9-250">Create a deployment group for hello Azure virtual machines</span></span>
> * <span data-ttu-id="f21f9-251">Merhaba VM'ler yapılandırır ve hello uygulamayı dağıtır bir yayın tanımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="f21f9-251">Create a release definition that configures hello VMs and deploys hello app</span></span>

<span data-ttu-id="f21f9-252">Toohello sonraki öğretici toolearn nasıl toodeploy AMPUL (Linux, Apache, MySQL ve PHP) yığın hakkında daha fazla ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="f21f9-252">Advance toohello next tutorial toolearn more about how toodeploy a LAMP (Linux, Apache, MySQL, and PHP) stack.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f21f9-253">LAMP yığını dağıtma</span><span class="sxs-lookup"><span data-stu-id="f21f9-253">Deploy LAMP stack</span></span>](tutorial-lamp-stack.md)