---
title: CI/CD'den Jenkins Team Services ile Azure vm'lerinin | Microsoft Docs
description: "Sürekli Tümleştirme (CI) ve Visual Studio Team Services (VSTS) ya da Microsoft Team Foundation Server (TFS) yayın Yönetimi'nden Azure Vm'lerine Jenkins kullanarak bir Node.js uygulaması sürekli dağıtımını (CD) ayarlama"
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
ms.openlocfilehash: a40e26a8681df31fad664e4d1df4c1513311900d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-app-to-linux-vms-using-jenkins-and-team-services"></a><span data-ttu-id="70fd4-103">Jenkins ve Team Services kullanarak Linux VM'ler için uygulamanızı dağıtma</span><span class="sxs-lookup"><span data-stu-id="70fd4-103">Deploy your app to Linux VMs using Jenkins and Team Services</span></span>

<span data-ttu-id="70fd4-104">Sürekli Tümleştirme (CI) ve sürekli dağıtımı (CD) olarak derleme, sürüm ve kullanabilirsiniz, kodunuzu dağıtmak bir ardışık düzen olur.</span><span class="sxs-lookup"><span data-stu-id="70fd4-104">Continuous integration (CI) and continuous deployment (CD) is a pipeline by which you can build, release, and deploy your code.</span></span> <span data-ttu-id="70fd4-105">Team Services dağıtımı için CI/CD Otomasyon Araçları'nın tam, tam özellikli bir dizi Azure'a sağlar.</span><span class="sxs-lookup"><span data-stu-id="70fd4-105">Team Services provides a complete, fully featured set of CI/CD automation tools for deployment to Azure.</span></span> <span data-ttu-id="70fd4-106">Jenkins CI/CD Otomasyon de sağlayan bir Popüler 3. taraf CI/CD sunucu tabanlı araçtır.</span><span class="sxs-lookup"><span data-stu-id="70fd4-106">Jenkins is a popular 3rd-party CI/CD server-based tool that also provides CI/CD automation.</span></span> <span data-ttu-id="70fd4-107">Her ikisi de birlikte bulut uygulaması veya hizmeti teslim nasıl özelleştirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70fd4-107">You can use both together to customize how you deliver your cloud app or service.</span></span>

<span data-ttu-id="70fd4-108">Bu öğreticide, Jenkins oluşturmak için kullandığınız bir **Node.js web uygulamasına**ve Visual Studio Team Services aygıtını dağıtılacağı bir [dağıtım grubu](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) Linux sanal makineleri içeren.</span><span class="sxs-lookup"><span data-stu-id="70fd4-108">In this tutorial, you use Jenkins to build a **Node.js web app**, and Visual Studio Team Services to deploy it to a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) containing Linux virtual machines.</span></span>

<span data-ttu-id="70fd4-109">Yapacaklarınız:</span><span class="sxs-lookup"><span data-stu-id="70fd4-109">You will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="70fd4-110">Jenkins uygulamanızda derleme</span><span class="sxs-lookup"><span data-stu-id="70fd4-110">Build your app in Jenkins</span></span>
> * <span data-ttu-id="70fd4-111">Jenkins Team Services tümleştirme için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="70fd4-111">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="70fd4-112">Azure sanal makineler için bir dağıtım grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="70fd4-112">Create a deployment group for the Azure virtual machines</span></span>
> * <span data-ttu-id="70fd4-113">Sanal makineleri yapılandırır ve uygulamayı dağıtır bir yayın tanımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="70fd4-113">Create a release definition that configures the VMs and deploys the app</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="70fd4-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="70fd4-114">Before you begin</span></span>

* <span data-ttu-id="70fd4-115">Jenkins hesabınıza erişmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="70fd4-115">You need access to a Jenkins account.</span></span> <span data-ttu-id="70fd4-116">Jenkins server henüz oluşturmadıysanız, bkz: [Jenkins belgelerine](https://jenkins.io/doc/).</span><span class="sxs-lookup"><span data-stu-id="70fd4-116">If you have not yet created a Jenkins server, see [Jenkins Documentation](https://jenkins.io/doc/).</span></span> 

* <span data-ttu-id="70fd4-117">Team Services hesabınızda oturum açın (`https://{youraccount}.visualstudio.com`).</span><span class="sxs-lookup"><span data-stu-id="70fd4-117">Sign in to your Team Services account (`https://{youraccount}.visualstudio.com`).</span></span> 
  <span data-ttu-id="70fd4-118">Alabileceğiniz bir [serbest Team Services hesabı](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span><span class="sxs-lookup"><span data-stu-id="70fd4-118">You can get a [free Team Services account](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span></span>

  > [!NOTE]
  > <span data-ttu-id="70fd4-119">Daha fazla bilgi için bkz: [Team Services Bağlan](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span><span class="sxs-lookup"><span data-stu-id="70fd4-119">For more information, see [Connect to Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span></span>

* <span data-ttu-id="70fd4-120">Zaten yoksa, kişisel erişim belirteci (PAT), Team Services hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="70fd4-120">Create a personal access token (PAT) in your Team Services account if you don't already have one.</span></span> <span data-ttu-id="70fd4-121">Jenkins Team Services hesabınıza erişmek için bu bilgileri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="70fd4-121">Jenkins requires this information to access your Team Services account.</span></span>
  <span data-ttu-id="70fd4-122">Okuma [nasıl oluşturabilirim kişisel erişim belirteci Team Services ve TFS için](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) biri oluşturma hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="70fd4-122">Read [How do I create a personal access token for Team Services and TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) to learn how to generate one.</span></span>

## <a name="get-the-sample-app"></a><span data-ttu-id="70fd4-123">Örnek uygulamayı Al</span><span class="sxs-lookup"><span data-stu-id="70fd4-123">Get the sample app</span></span>

<span data-ttu-id="70fd4-124">Bir uygulamayı dağıtmak için bir Git deposu içinde depolanan gerekir.</span><span class="sxs-lookup"><span data-stu-id="70fd4-124">You need an app to deploy stored in a Git repository.</span></span>
<span data-ttu-id="70fd4-125">Bu öğretici için kullandığınız olan öneririz [Github'dan Bu örnek uygulama](https://github.com/azooinmyluggage/fabrikam-node).</span><span class="sxs-lookup"><span data-stu-id="70fd4-125">For this tutorial, we recommend you use [this sample app available from GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span></span>

1. <span data-ttu-id="70fd4-126">Bu uygulamanın çatalı oluşturun ve bu öğreticinin daha sonraki adımlarda kullanılmak konumu (URL) not edin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-126">Create a fork of this app and take note of the location (URL) for use in later steps of this tutorial.</span></span>

1. <span data-ttu-id="70fd4-127">Çatalı olun **ortak** GitHub için daha sonra bağlanmayı basitleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="70fd4-127">Make the fork **public** to simplify connecting to GitHub later.</span></span>

> [!NOTE]
> <span data-ttu-id="70fd4-128">Daha fazla bilgi için bkz: [bir depoyu Çatallaştırma](https://help.github.com/articles/fork-a-repo/) ve [özel bir depo ortak yapma](https://help.github.com/articles/making-a-private-repository-public/).</span><span class="sxs-lookup"><span data-stu-id="70fd4-128">For more information, see [Fork a repo](https://help.github.com/articles/fork-a-repo/) and [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/).</span></span>

> [!NOTE]
> <span data-ttu-id="70fd4-129">Uygulama kullanılarak oluşturulan [Yeoman](http://yeoman.io/learning/index.html); kullandığı **Express**, **bower**, ve **grunt**; ve bazı sahip **npm** paketler bağımlılık olarak.</span><span class="sxs-lookup"><span data-stu-id="70fd4-129">The app was built using [Yeoman](http://yeoman.io/learning/index.html); it uses **Express**, **bower**, and **grunt**; and it has some **npm** packages as dependencies.</span></span>
> <span data-ttu-id="70fd4-130">Örnek uygulama kümesini içeren [Azure Resource Manager şablonları](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) dağıtımı için sanal makineleri Azure üzerinde dinamik olarak oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="70fd4-130">The sample app contains a set of [Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) that are used to dynamically create the virtual machines for deployment on Azure.</span></span> <span data-ttu-id="70fd4-131">Bu şablonlar görevleri tarafından kullanılan [Team Services sürüm tanımı](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span><span class="sxs-lookup"><span data-stu-id="70fd4-131">These templates are used by tasks in the [Team Services release definition](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span></span>
> <span data-ttu-id="70fd4-132">Ana şablon bir ağ güvenlik grubu, bir sanal makine ve sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="70fd4-132">The main template creates a network security group, a virtual machine, and a virtual network.</span></span> <span data-ttu-id="70fd4-133">Bir ortak IP adresini atar ve gelen bağlantı noktası 80'i açar.</span><span class="sxs-lookup"><span data-stu-id="70fd4-133">It assigns a public IP address and opens inbound port 80.</span></span> <span data-ttu-id="70fd4-134">Ayrıca, dağıtım almak için makine seçmek için dağıtım grubu tarafından kullanılan bir etiket ekler.</span><span class="sxs-lookup"><span data-stu-id="70fd4-134">It also adds a tag that is used by the deployment group to select the machines to receive the deployment.</span></span>
>
> <span data-ttu-id="70fd4-135">Örnek, Nginx ayarlar ve uygulamayı dağıtır bir betik de içerir.</span><span class="sxs-lookup"><span data-stu-id="70fd4-135">The sample also contains a script that sets up Nginx and deploys the app.</span></span> <span data-ttu-id="70fd4-136">Her sanal makineler üzerinde yürütülür.</span><span class="sxs-lookup"><span data-stu-id="70fd4-136">It is executed on each of the virtual machines.</span></span> <span data-ttu-id="70fd4-137">Özellikle, betik düğümünde, Nginx ve PM2 yükler; Nginx ve PM2 yapılandırır; ardından düğümü uygulaması başlatır.</span><span class="sxs-lookup"><span data-stu-id="70fd4-137">Specifically, the script installs Node, Nginx, and PM2; configures Nginx and PM2; then starts the Node app.</span></span>

## <a name="configure-jenkins-plugins"></a><span data-ttu-id="70fd4-138">Jenkins eklentileri yapılandırın</span><span class="sxs-lookup"><span data-stu-id="70fd4-138">Configure Jenkins plugins</span></span>

<span data-ttu-id="70fd4-139">İlk olarak, iki Jenkins eklentileri için yapılandırmanız gerekir **NodeJS** ve **Team Services ile tümleştirme**.</span><span class="sxs-lookup"><span data-stu-id="70fd4-139">First, you must configure two Jenkins plugins for **NodeJS** and **Integration with Team Services**.</span></span>

1. <span data-ttu-id="70fd4-140">Jenkins hesabınızı açın ve seçin **yönetmek Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="70fd4-140">Open your Jenkins account and choose **Manage Jenkins**.</span></span>

1. <span data-ttu-id="70fd4-141">İçinde **yönetmek Jenkins** sayfasında, **eklentileri yönetme**.</span><span class="sxs-lookup"><span data-stu-id="70fd4-141">In the **Manage Jenkins** page, choose **Manage Plugins**.</span></span>

1. <span data-ttu-id="70fd4-142">Listenin bulmak için filtre **NodeJS** eklentisi ve yeniden başlatma gerekmeden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-142">Filter the list to locate the **NodeJS** plugin and install it without restart.</span></span>

   ![Jenkins için NodeJS eklenti ekleme](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. <span data-ttu-id="70fd4-144">Listenin bulmak için filtre **Team Foundation Server** eklentisini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-144">Filter the list to find the **Team Foundation Server** plugin and install it.</span></span> <span data-ttu-id="70fd4-145">(Bu eklenti çalışır Team Services ve Team Foundation Server için.) Jenkins yeniden başlatılması gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="70fd4-145">(This plug-in works for both Team Services and Team Foundation Server.) Restarting Jenkins is not necessary.</span></span>

## <a name="configure-jenkins-build-for-nodejs"></a><span data-ttu-id="70fd4-146">Node.js için Jenkins yapı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="70fd4-146">Configure Jenkins build for Node.js</span></span>

<span data-ttu-id="70fd4-147">Jenkins, yeni bir derleme projesi oluşturun ve aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="70fd4-147">In Jenkins, create a new build project and configure it as follows:</span></span>

1. <span data-ttu-id="70fd4-148">İçinde **genel** sekmesinde, yapı projeniz için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-148">In the **General** tab, enter a name for your build project.</span></span>

1. <span data-ttu-id="70fd4-149">İçinde **kaynak kodu Yönetimi** sekmesine **Git** ve depo ve uygulama kodu içeren dalı ayrıntılarını girin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-149">In the **Source Code Management** tab, select **Git** and enter the details of the repository and the branch containing your app code.</span></span>

   ![Bir depo, derleme ekleyin](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > <span data-ttu-id="70fd4-151">Deponuzda ortak değilse seçin **Ekle** ve buna bağlanmak için kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="70fd4-151">If your repository is not public, choose **Add** and provide credentials to connect to it.</span></span>

1. <span data-ttu-id="70fd4-152">İçinde **yapı tetikleyicileri** sekmesine **yoklama SCM** ve zamanlama girin `H/03 * * * *` değişiklikleri için Git deposu üç dakikada yoklamak için.</span><span class="sxs-lookup"><span data-stu-id="70fd4-152">In the **Build Triggers** tab, select **Poll SCM** and enter the schedule `H/03 * * * *` to poll the Git repository for changes every three minutes.</span></span> 

1. <span data-ttu-id="70fd4-153">İçinde **yapı ortamı** sekmesine **sağlayan düğüm &amp; npm bin / klasör yolu** ve girin `NodeJS` düğümü JS yükleme değeri.</span><span class="sxs-lookup"><span data-stu-id="70fd4-153">In the **Build Environment** tab, select **Provide Node &amp; npm bin/ folder PATH** and enter `NodeJS` for the Node JS Installation value.</span></span> <span data-ttu-id="70fd4-154">Bırakın **npmrc dosya** "sistem varsayılan kullanır." olarak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="70fd4-154">Leave **npmrc file** set to "use system default."</span></span>

1. <span data-ttu-id="70fd4-155">İçinde **yapı** sekmesinde, aşağıdaki komutu girin `npm install` tüm bağımlılıkları güncelleştirilir emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="70fd4-155">In the **Build** tab, enter the command `npm install` to ensure all dependencies are updated.</span></span>

## <a name="configure-jenkins-for-team-services-integration"></a><span data-ttu-id="70fd4-156">Jenkins Team Services tümleştirme için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="70fd4-156">Configure Jenkins for Team Services integration</span></span>

1. <span data-ttu-id="70fd4-157">İçinde **oluşturma sonrası eylemleri** sekmesinde için **arşivlemek için dosyaları**, girin `**/*` tüm dosyaları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="70fd4-157">In the **Post-build Actions** tab, for **Files to archive**, enter `**/*` to include all files.</span></span>

1. <span data-ttu-id="70fd4-158">İçin **tetiklemek TFS/Team Services sürümde**, hesabınızı tam URL'sini girin (gibi `https://your-account-name.visualstudio.com`), proje adı, (daha sonra oluşturulan) sürüm tanımı ve hesabınıza bağlanmak için kimlik bilgileri için bir ad.</span><span class="sxs-lookup"><span data-stu-id="70fd4-158">For **Trigger release in TFS/Team Services**, enter the full URL of your account (such as `https://your-account-name.visualstudio.com`), the project name, a name for the release definition (created later), and the credentials to connect to your account.</span></span>
   <span data-ttu-id="70fd4-159">Kullanıcı adınızı ve daha önce oluşturduğunuz PAT gerekir.</span><span class="sxs-lookup"><span data-stu-id="70fd4-159">You need your user name and the PAT you created earlier.</span></span> 

   ![Jenkins oluşturma sonrası eylemleri yapılandırma](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. <span data-ttu-id="70fd4-161">Derleme projesi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-161">Save the build project.</span></span>

## <a name="create-a-jenkins-service-endpoint"></a><span data-ttu-id="70fd4-162">Jenkins hizmet uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="70fd4-162">Create a Jenkins service endpoint</span></span>

<span data-ttu-id="70fd4-163">Hizmet uç noktası Team Services'ı için Jenkins bağlanmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="70fd4-163">A service endpoint allows Team Services to connect to Jenkins.</span></span>

1. <span data-ttu-id="70fd4-164">Açık **Hizmetleri** Team Services, açık sayfasında **yeni hizmet uç noktası** listesinde ve seçin **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="70fd4-164">Open the **Services** page in Team Services, open the **New Service Endpoint** list, and choose **Jenkins**.</span></span>

   ![Jenkins uç nokta ekleyin](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. <span data-ttu-id="70fd4-166">Bu bağlantıya başvurmak için kullanacağınız bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-166">Enter a name you will use to refer to this connection.</span></span>

1. <span data-ttu-id="70fd4-167">Jenkins sunucunuza ve onay URL'sini girin **kabul güvenilmeyen SSL sertifikalarını** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="70fd4-167">Enter the URL of your Jenkins server, and tick the **Accept untrusted SSL certificates** option.</span></span>

1. <span data-ttu-id="70fd4-168">Jenkins hesabınız için kullanıcı adını ve parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-168">Enter the user name and password for your Jenkins account.</span></span>

1. <span data-ttu-id="70fd4-169">Seçin **bağlantısını doğrulama** bilgilerin doğru olup olmadığını denetlemek için.</span><span class="sxs-lookup"><span data-stu-id="70fd4-169">Choose **Verify connection** to check that the information is correct.</span></span>

1. <span data-ttu-id="70fd4-170">Seçin **Tamam** hizmet uç noktası oluşturulamadı.</span><span class="sxs-lookup"><span data-stu-id="70fd4-170">Choose **OK** to create the service endpoint.</span></span>

## <a name="create-a-deployment-group"></a><span data-ttu-id="70fd4-171">Bir dağıtım grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="70fd4-171">Create a deployment group</span></span>

<span data-ttu-id="70fd4-172">Gereksinim duyduğunuz bir [dağıtım grubu](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) sanal makineleri içeren için.</span><span class="sxs-lookup"><span data-stu-id="70fd4-172">You need a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) to  contain the virtual machines.</span></span>

1. <span data-ttu-id="70fd4-173">Açık **sürümleri** sekmesinde **yapı &amp; sürüm** hub'ı açın **dağıtım grupları** sekmesini tıklatın ve seçin **+ yeni**.</span><span class="sxs-lookup"><span data-stu-id="70fd4-173">Open the **Releases** tab of the **Build &amp; Release** hub, then open the **Deployment groups** tab, and choose **+ New**.</span></span>

1. <span data-ttu-id="70fd4-174">Dağıtım grubu ve isteğe bağlı bir açıklama için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-174">Enter a name for the deployment group, and an optional description.</span></span>
   <span data-ttu-id="70fd4-175">Ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="70fd4-175">Then choose **Create**.</span></span>

<span data-ttu-id="70fd4-176">Azure kaynak grubu dağıtımı görev oluşturur ve Azure Resource Manager şablonu kullanarak çalıştığında VM'ler kaydeder.</span><span class="sxs-lookup"><span data-stu-id="70fd4-176">The Azure Resource Group Deployment task creates and registers the VMs when it runs using the Azure Resource Manager template.</span></span>
<span data-ttu-id="70fd4-177">Oluşturun ve sanal makineleri kendiniz kaydetmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="70fd4-177">You don't need to create and register the virtual machines yourself.</span></span>

## <a name="create-a-release-definition"></a><span data-ttu-id="70fd4-178">Bir yayın tanımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="70fd4-178">Create a release definition</span></span>

<span data-ttu-id="70fd4-179">Bir yayın tanımı işlem Team Services uygulamasını dağıtmak için yürütecek belirtir.</span><span class="sxs-lookup"><span data-stu-id="70fd4-179">A release definition specifies the process Team Services will execute to deploy the app.</span></span>
<span data-ttu-id="70fd4-180">Team Services içinde sürüm tanımı oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="70fd4-180">To create the release definition in Team Services:</span></span>

1. <span data-ttu-id="70fd4-181">Açmak **sürümleri** sekmesinde **yapı &amp; yayın** hub'ı Aç  **+**  aşağı açılan listesinde, sürüm tanımlarını ve seçin **oluşturma yayın tanımı**.</span><span class="sxs-lookup"><span data-stu-id="70fd4-181">Open the **Releases** tab of the **Build &amp; Release** hub, open the **+** drop-down in the list of release definitions, and choose the **Create release definition**.</span></span> 

1. <span data-ttu-id="70fd4-182">Seçin **boş** şablonu ve **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="70fd4-182">Select the **Empty** template and choose **Next**.</span></span>

1. <span data-ttu-id="70fd4-183">İçinde **yapıları** bölümünde, tıklayın **bir yapı bağlantı** ve **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="70fd4-183">In the **Artifacts** section, click on **Link an Artifact** and choose **Jenkins**.</span></span> <span data-ttu-id="70fd4-184">Jenkins hizmet uç noktası bağlantınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-184">Select your Jenkins service endpoint connection.</span></span> <span data-ttu-id="70fd4-185">Ardından Jenkins kaynak iş seçip **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="70fd4-185">Then select the Jenkins source job and choose **Create**.</span></span> 

1. <span data-ttu-id="70fd4-186">Yeni sürüm tanımı, seçin **+ görev ekleme** ve ekleme bir **Azure kaynak grubu dağıtımı** varsayılan ortamına görev.</span><span class="sxs-lookup"><span data-stu-id="70fd4-186">In the new release definition, choose **+ Add tasks** and add an **Azure Resource Group Deployment** task to the default environment.</span></span>

1. <span data-ttu-id="70fd4-187">Açılan ok seçin **+ Ekle görevleri** bağlantı ve bir dağıtım grubu aşaması tanımına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-187">Choose the drop down arrow next to the **+ Add tasks** link and add a deployment group phase to the definition.</span></span>

   ![Bir dağıtım grubu aşaması ekleme](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. <span data-ttu-id="70fd4-189">Görev Kataloğu'nda açmak **yardımcı programı** bölüm ve bir örnek ekler **Kabuk betiği** görev.</span><span class="sxs-lookup"><span data-stu-id="70fd4-189">In the Task catalog, open the **Utility** section and add an instance of the **Shell Script** task.</span></span>

1. <span data-ttu-id="70fd4-190">Azure kaynak grubu dağıtımı görevde kullanılan parametreleri şablonu Vm'lere bağlanmak için kullanılan yönetici parolasını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="70fd4-190">The parameters template used in the Azure Resource Group Deployment task sets the admin password used to connect to the VMs.</span></span>
   <span data-ttu-id="70fd4-191">Değişkenle bu parola **$(adminpassword)**:</span><span class="sxs-lookup"><span data-stu-id="70fd4-191">You provide this password with the variable **$(adminpassword)**:</span></span>
   
   - <span data-ttu-id="70fd4-192">Açık **değişkenleri** sekmesini hem de **değişkenleri** bölümünde, bir ad girin `adminpassword`.</span><span class="sxs-lookup"><span data-stu-id="70fd4-192">Open the **Variables** tab and, in the **Variables** section, enter the name `adminpassword`.</span></span>

   - <span data-ttu-id="70fd4-193">Yönetici parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-193">Enter the administrator password.</span></span>

   - <span data-ttu-id="70fd4-194">Parolayla korumak için değer textbox yanındaki "asma kilit" simgesini seçin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-194">Choose the "padlock" icon next to the value textbox to protect the password.</span></span> 

## <a name="configure-the-azure-resource-group-deployment-task"></a><span data-ttu-id="70fd4-195">Azure kaynak grubu dağıtımı görevi yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="70fd4-195">Configure the Azure Resource Group Deployment task</span></span>

<span data-ttu-id="70fd4-196">**Azure kaynak grubu dağıtımı** görev, bir dağıtım grubu oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="70fd4-196">The **Azure Resource Group Deployment** task is used to create the deployment group.</span></span> <span data-ttu-id="70fd4-197">Aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="70fd4-197">Configure it as follows:</span></span>

* <span data-ttu-id="70fd4-198">**Azure aboneliği:** altındaki listeden bir bağlantı seçin **kullanılabilir Azure hizmet bağlantıları**.</span><span class="sxs-lookup"><span data-stu-id="70fd4-198">**Azure Subscription:** Select a connection from the list under **Available Azure Service Connections**.</span></span> 
  <span data-ttu-id="70fd4-199">Hiçbir bağlantı görünüyorsa seçin **Yönet**seçin **yeni hizmet uç noktası** sonra **Azure Resource Manager**ve yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-199">If no connections appear, choose **Manage**, select **New Service Endpoint** then **Azure Resource Manager**, and follow the prompts.</span></span>
  <span data-ttu-id="70fd4-200">İade yayın tanımınızı, yenileme **AzureRM abonelik** listesinde ve oluşturduğunuz bağlantıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-200">Return to your release definition, refresh the **AzureRM Subscription** list, and select the connection you created.</span></span>

* <span data-ttu-id="70fd4-201">**Kaynak grubu**: daha önce oluşturduğunuz kaynak grubunun adını girin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-201">**Resource group**: Enter a name of the resource group you created earlier.</span></span>

* <span data-ttu-id="70fd4-202">**Konum**: dağıtım için bir bölge seçin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-202">**Location**: Select a region for the deployment.</span></span>

  ![Yeni bir kaynak grubu oluşturma](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* <span data-ttu-id="70fd4-204">**Şablon konumu**:`URL of the file`</span><span class="sxs-lookup"><span data-stu-id="70fd4-204">**Template location**: `URL of the file`</span></span>

* <span data-ttu-id="70fd4-205">**Şablon bağlantısı**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span><span class="sxs-lookup"><span data-stu-id="70fd4-205">**Template link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span></span>

* <span data-ttu-id="70fd4-206">**Şablon parametreleri bağlantısı**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span><span class="sxs-lookup"><span data-stu-id="70fd4-206">**Template parameters link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span></span>

* <span data-ttu-id="70fd4-207">**Şablon parametreleri geçersiz kılma**: geçersiz kılma listesini değerleri, örneğin: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span><span class="sxs-lookup"><span data-stu-id="70fd4-207">**Override template parameters**: A list of the override values, for example: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span></span><br /><span data-ttu-id="70fd4-208">{Yer tutucular} kendi özel değerlerinizi yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-208">Insert your own specific values for the {placeholders}.</span></span> 

* <span data-ttu-id="70fd4-209">**Önkoşullar etkinleştirme**:`Configure with Deployment Group agent`</span><span class="sxs-lookup"><span data-stu-id="70fd4-209">**Enable prerequisites**: `Configure with Deployment Group agent`</span></span>

* <span data-ttu-id="70fd4-210">**TFS/VSTS endpoint**: seçin **Ekle** ve "Yeni Team Foundation Server/Team Services Bağlantısı Ekle" iletişim kutusunda seçin **belirteç tabanlı kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="70fd4-210">**TFS/VSTS endpoint**: Choose **Add** and, in the "Add new Team Foundation Server/Team Services Connection" dialog, select **Token Based Authentication**.</span></span> <span data-ttu-id="70fd4-211">Bağlantının adını ve takım projenizin URL'sini girin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-211">Enter a name of the connection and the URL of your team project.</span></span> <span data-ttu-id="70fd4-212">Ardından oluşturmak ve girin bir [kişisel erişim belirteci (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) takım projenize bağlantı kimliğini doğrulamak için.</span><span class="sxs-lookup"><span data-stu-id="70fd4-212">Then generate and enter a [Personal Access Token (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) to authenticate the connection to your team project.</span></span>

  ![Kişisel oluşturma erişim belirteci](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* <span data-ttu-id="70fd4-214">**Takım projesi**: geçerli projenizi seçin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-214">**Team project**: Select your current project.</span></span>

* <span data-ttu-id="70fd4-215">**Dağıtım grubu**: siz için kullanılan aynı dağıtım grubu adı girin **kaynak grubu** parametresi.</span><span class="sxs-lookup"><span data-stu-id="70fd4-215">**Deployment Group**: Enter the same deployment group name as you used for the **Resource group** parameter.</span></span>

<span data-ttu-id="70fd4-216">Azure kaynak grubu dağıtımı görev için varsayılan ayarları oluşturmak veya bir kaynak güncelleştirmek için ve bunu artımlı olarak yapmak için ' dir.</span><span class="sxs-lookup"><span data-stu-id="70fd4-216">The default settings for the Azure Resource Group Deployment task are to create or update a resource, and to do so incrementally.</span></span> <span data-ttu-id="70fd4-217">Görev ilk kez çalıştırır ve daha sonra yalnızca güncelleştirmenizi VM'ler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="70fd4-217">The task creates the VMs the first time it runs, and subsequently just update them.</span></span>

## <a name="configure-the-shell-script-task"></a><span data-ttu-id="70fd4-218">Kabuk betiği görevi yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="70fd4-218">Configure the Shell Script task</span></span>

<span data-ttu-id="70fd4-219">**Kabuk betiği** görev Node.js yüklemek ve uygulamayı başlatmak için her sunucuda çalıştırmak bir komut dosyası için yapılandırma sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="70fd4-219">The **Shell Script** task is used to provide the configuration for a script to run on each server to install Node.js and start the app.</span></span> <span data-ttu-id="70fd4-220">Aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="70fd4-220">Configure it as follows:</span></span>

* <span data-ttu-id="70fd4-221">**Komut dosyası yolu**:`$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span><span class="sxs-lookup"><span data-stu-id="70fd4-221">**Script Path**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span></span>

* <span data-ttu-id="70fd4-222">**Çalışma belirtin dizin**:`Checked`</span><span class="sxs-lookup"><span data-stu-id="70fd4-222">**Specify Working Directory**: `Checked`</span></span>

* <span data-ttu-id="70fd4-223">**Çalışma dizini**:`$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span><span class="sxs-lookup"><span data-stu-id="70fd4-223">**Working Directory**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span></span>
   
## <a name="rename-and-save-the-release-definition"></a><span data-ttu-id="70fd4-224">Yeniden adlandırın ve yayın tanımını kaydet</span><span class="sxs-lookup"><span data-stu-id="70fd4-224">Rename and save the release definition</span></span>

1. <span data-ttu-id="70fd4-225">İçinde belirtilen adı yayın tanımına adını düzenleyin **oluşturma sonrası eylemleri** Jenkins derlemede sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="70fd4-225">Edit the name of the release definition to the name you specified in the **Post-build Actions** tab of the build in Jenkins.</span></span> <span data-ttu-id="70fd4-226">Jenkins kaynak yapıları güncelleştirildiğinde yeni sürüm tetikleme edebilmek için bu ad gerektirir.</span><span class="sxs-lookup"><span data-stu-id="70fd4-226">Jenkins requires this name to be able to trigger a new release when the source artifacts are updated.</span></span>

1. <span data-ttu-id="70fd4-227">İsteğe bağlı olarak, adına tıklayarak ortam adını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-227">Optionally, change the name of the environment by clicking on the name.</span></span> 

1. <span data-ttu-id="70fd4-228">Seçin **kaydetmek**ve seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="70fd4-228">Choose **Save**, and choose **OK**.</span></span>

## <a name="start-a-manual-deployment"></a><span data-ttu-id="70fd4-229">El ile dağıtımı Başlat</span><span class="sxs-lookup"><span data-stu-id="70fd4-229">Start a manual deployment</span></span>

1. <span data-ttu-id="70fd4-230">Seçin **+ yayın** seçip **sürüm oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="70fd4-230">Choose **+ Release** and select **Create Release**.</span></span>

1. <span data-ttu-id="70fd4-231">Tamamlanan yapı vurgulanan aşağı açılan listeden seçip **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="70fd4-231">Select the build you completed in the highlighted drop-down list and choose **Create**.</span></span>

1. <span data-ttu-id="70fd4-232">Yayın bağı açılan iletide'i seçin.</span><span class="sxs-lookup"><span data-stu-id="70fd4-232">Choose the release link in the popup message.</span></span> <span data-ttu-id="70fd4-233">Örneğin: "yayın **sürüm 1** oluşturuldu."</span><span class="sxs-lookup"><span data-stu-id="70fd4-233">For example: "Release **Release-1** has been created."</span></span>

1. <span data-ttu-id="70fd4-234">Açık **günlükleri** yayın konsol çıktısı izlemek için sekmesi.</span><span class="sxs-lookup"><span data-stu-id="70fd4-234">Open the **Logs** tab to watch the release console output.</span></span>

1. <span data-ttu-id="70fd4-235">Tarayıcınızda, dağıtım grubuna eklenen sunucuların birini URL'sini açın.</span><span class="sxs-lookup"><span data-stu-id="70fd4-235">In your browser, open the URL of one of the servers you added to your deployment group.</span></span> <span data-ttu-id="70fd4-236">Örneğin, girin`http://{your-server-ip-address}`</span><span class="sxs-lookup"><span data-stu-id="70fd4-236">For example, enter `http://{your-server-ip-address}`</span></span>

## <a name="start-a-cicd-deployment"></a><span data-ttu-id="70fd4-237">CI/CD dağıtım Başlat</span><span class="sxs-lookup"><span data-stu-id="70fd4-237">Start a CI/CD deployment</span></span>

1. <span data-ttu-id="70fd4-238">Yayın tanımı'nda onay kutusunu temizleyin **etkin** onay kutusu **denetim seçeneklerini** Azure kaynak grubu dağıtımı görev için ayarları bölümü.</span><span class="sxs-lookup"><span data-stu-id="70fd4-238">In the release definition, uncheck the **Enabled** checkbox in the **Control Options** section of the settings for the Azure Resource Group Deployment task.</span></span>
   <span data-ttu-id="70fd4-239">Varolan bir dağıtım grubu için gelecekteki dağıtımlar için bu görevi yeniden yürütme gerekmez.</span><span class="sxs-lookup"><span data-stu-id="70fd4-239">For future deployments to the existing deployment group, you do not need to re-execute this task.</span></span>

1. <span data-ttu-id="70fd4-240">Kaynak Git deposuna gidin ve içeriğini değiştirmeye **h1** dosyasında başlık [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span><span class="sxs-lookup"><span data-stu-id="70fd4-240">Go to the source Git repository and modify the contents of the **h1** heading in the file [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span></span>

1. <span data-ttu-id="70fd4-241">Değişikliğiniz uygulayın.</span><span class="sxs-lookup"><span data-stu-id="70fd4-241">Commit your change.</span></span>

1. <span data-ttu-id="70fd4-242">Birkaç dakika sonra oluşturulan yeni bir sürüm görürsünüz **sürümleri** Team Services veya TFS sayfası.</span><span class="sxs-lookup"><span data-stu-id="70fd4-242">After a few minutes, you will see a new release created in the **Releases** page of Team Services or TFS.</span></span> <span data-ttu-id="70fd4-243">Yayın gerçekleşmesini dağıtım görmek için açın.</span><span class="sxs-lookup"><span data-stu-id="70fd4-243">Open the release to see the deployment taking place.</span></span> <span data-ttu-id="70fd4-244">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="70fd4-244">Congratulations!</span></span>

## <a name="next-steps"></a><span data-ttu-id="70fd4-245">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="70fd4-245">Next Steps</span></span>

<span data-ttu-id="70fd4-246">Bu öğreticide, Azure Jenkins derleme ve sürüm için Team Services kullanarak bir uygulama dağıtımını otomatik.</span><span class="sxs-lookup"><span data-stu-id="70fd4-246">In this tutorial, you automated the deployment of an app to Azure using Jenkins build and Team Services for release.</span></span> <span data-ttu-id="70fd4-247">Size nasıl öğrenilen için:</span><span class="sxs-lookup"><span data-stu-id="70fd4-247">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="70fd4-248">Jenkins uygulamanızda derleme</span><span class="sxs-lookup"><span data-stu-id="70fd4-248">Build your app in Jenkins</span></span>
> * <span data-ttu-id="70fd4-249">Jenkins Team Services tümleştirme için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="70fd4-249">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="70fd4-250">Azure sanal makineler için bir dağıtım grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="70fd4-250">Create a deployment group for the Azure virtual machines</span></span>
> * <span data-ttu-id="70fd4-251">Sanal makineleri yapılandırır ve uygulamayı dağıtır bir yayın tanımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="70fd4-251">Create a release definition that configures the VMs and deploys the app</span></span>

<span data-ttu-id="70fd4-252">Bir AMPUL dağıtma hakkında daha fazla bilgi için sonraki öğretici İlerlet (Linux, Apache, MySQL ve PHP) yığını.</span><span class="sxs-lookup"><span data-stu-id="70fd4-252">Advance to the next tutorial to learn more about how to deploy a LAMP (Linux, Apache, MySQL, and PHP) stack.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="70fd4-253">LAMP yığını dağıtma</span><span class="sxs-lookup"><span data-stu-id="70fd4-253">Deploy LAMP stack</span></span>](tutorial-lamp-stack.md)