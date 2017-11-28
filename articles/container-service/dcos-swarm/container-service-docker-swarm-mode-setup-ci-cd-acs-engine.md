---
title: "Azure kapsayıcı hizmeti altyapısı ve Swarm modu ile aaaCI/CD | Microsoft Docs"
description: "Docker Swarm modu, bir Azure kapsayıcı kayıt defteri ve Visual Studio Team Services toodeliver sürekli olarak bir çok kapsayıcı .NET Core uygulaması ile Azure kapsayıcı hizmeti altyapısını kullanma"
services: container-service
documentationcenter: " "
author: diegomrtnzg
manager: esterdnb
tags: acs, azure-container-service, acs-engine
keywords: "Mikro docker, kapsayıcıları, hizmetleri, Swarm, Azure, Visual Studio Team Services, DevOps, ACS altyapısı"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 040522c452f7ea0ce3c92f2fe57b1c141b97e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a><span data-ttu-id="b87aa-104">Tam CI/CD ardışık düzen toodeploy ACS altyapısı ve Docker Swarm Visual Studio Team Services kullanarak modu ile Azure kapsayıcı hizmeti üzerinde çok kapsayıcı uygulama</span><span class="sxs-lookup"><span data-stu-id="b87aa-104">Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with ACS Engine and Docker Swarm Mode using Visual Studio Team Services</span></span>

<span data-ttu-id="b87aa-105">*Bu makalede dayanır [tam CI/CD kanal toodeploy Visual Studio Team Services kullanarak Docker Swarm ile Azure kapsayıcı hizmeti üzerinde çok kapsayıcı uygulama](container-service-docker-swarm-setup-ci-cd.md) belgeleri*</span><span class="sxs-lookup"><span data-stu-id="b87aa-105">*This article is based on [Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentation*</span></span>

<span data-ttu-id="b87aa-106">Günümüzde, aşağıdakilerden birini hello en büyük zorluklardan hello bulut için modern uygulamalar geliştirme mümkün toodeliver yüklenirken bu uygulamalara sürekli olarak.</span><span class="sxs-lookup"><span data-stu-id="b87aa-106">Nowadays, One of hello biggest challenges when developing modern applications for hello cloud is being able toodeliver these applications continuously.</span></span> <span data-ttu-id="b87aa-107">Bu makalede, tooimplement tam sürekli tümleştirme ve dağıtım (CI/CD) kullanarak nasıl kanal öğrenin:</span><span class="sxs-lookup"><span data-stu-id="b87aa-107">In this article, you learn how tooimplement a full continuous integration and deployment (CI/CD) pipeline using:</span></span> 
* <span data-ttu-id="b87aa-108">Azure kapsayıcı hizmeti altyapısı Docker Swarm modu</span><span class="sxs-lookup"><span data-stu-id="b87aa-108">Azure Container Service Engine with Docker Swarm Mode</span></span>
* <span data-ttu-id="b87aa-109">Azure Container Kayıt Defteri</span><span class="sxs-lookup"><span data-stu-id="b87aa-109">Azure Container Registry</span></span>
* <span data-ttu-id="b87aa-110">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="b87aa-110">Visual Studio Team Services</span></span>

<span data-ttu-id="b87aa-111">Bu makalede, kullanılabilen basit bir uygulama dayalı [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), ASP.NET Core ile geliştirilen.</span><span class="sxs-lookup"><span data-stu-id="b87aa-111">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), developed with ASP.NET Core.</span></span> <span data-ttu-id="b87aa-112">Merhaba uygulaması dört farklı hizmetlerini oluşur: üç API'ları ve bir web ön uç web:</span><span class="sxs-lookup"><span data-stu-id="b87aa-112">hello application is composed of four different services: three web APIs and one web front end:</span></span>

![MyShop örnek uygulama](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

<span data-ttu-id="b87aa-114">Merhaba hedefi toodeliver Visual Studio Team Services kullanarak sürekli bir Docker Swarm modu kümesinde, bu bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="b87aa-114">hello objective is toodeliver this application continuously in a Docker Swarm Mode cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="b87aa-115">Merhaba aşağıdaki ayrıntıları bu kesintisiz teslim ardışık düzen şekil:</span><span class="sxs-lookup"><span data-stu-id="b87aa-115">hello following figure details this continuous delivery pipeline:</span></span>

![MyShop örnek uygulama](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

<span data-ttu-id="b87aa-117">Kısa bir açıklama başlangıç adımları şöyledir:</span><span class="sxs-lookup"><span data-stu-id="b87aa-117">Here is a brief explanation of hello steps:</span></span>

1. <span data-ttu-id="b87aa-118">Kod değişiklikleri olan taahhüt toohello kaynak kodu deposu (burada, GitHub)</span><span class="sxs-lookup"><span data-stu-id="b87aa-118">Code changes are committed toohello source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="b87aa-119">Visual Studio Team Services derlemede GitHub tetikler</span><span class="sxs-lookup"><span data-stu-id="b87aa-119">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="b87aa-120">Visual Studio Team Services hello en son sürümünü hello kaynakları alır ve Merhaba uygulaması oluşturan tüm hello görüntü oluşturur</span><span class="sxs-lookup"><span data-stu-id="b87aa-120">Visual Studio Team Services gets hello latest version of hello sources and builds all hello images that compose hello application</span></span> 
4. <span data-ttu-id="b87aa-121">Visual Studio Team Services hello Azure kapsayıcı kayıt defteri hizmeti kullanılarak oluşturulan her görüntü tooa Docker kayıt defteri iter</span><span class="sxs-lookup"><span data-stu-id="b87aa-121">Visual Studio Team Services pushes each image tooa Docker registry created using hello Azure Container Registry service</span></span> 
5. <span data-ttu-id="b87aa-122">Yeni bir sürüm Visual Studio Team Services tetikler</span><span class="sxs-lookup"><span data-stu-id="b87aa-122">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="b87aa-123">Merhaba yayın hello Azure kapsayıcı hizmeti küme ana düğümünde SSH kullanarak bazı komutları çalıştırır</span><span class="sxs-lookup"><span data-stu-id="b87aa-123">hello release runs some commands using SSH on hello Azure container service cluster master node</span></span> 
7. <span data-ttu-id="b87aa-124">Docker Swarm modu hello kümede hello görüntüleri en son sürümünü hello çeker</span><span class="sxs-lookup"><span data-stu-id="b87aa-124">Docker Swarm Mode on hello cluster pulls hello latest version of hello images</span></span> 
8. <span data-ttu-id="b87aa-125">Merhaba uygulamanın yeni sürümü Hello Docker yığını kullanılarak dağıtılır</span><span class="sxs-lookup"><span data-stu-id="b87aa-125">hello new version of hello application is deployed using Docker Stack</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b87aa-126">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b87aa-126">Prerequisites</span></span>

<span data-ttu-id="b87aa-127">Bu öğreticiye başlamadan önce görevleri aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b87aa-127">Before starting this tutorial, you need toocomplete hello following tasks:</span></span>

- [<span data-ttu-id="b87aa-128">ACS altyapı ile Azure kapsayıcı Hizmeti'nde bir Swarm modu kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b87aa-128">Create a Swarm Mode cluster in Azure Container Service with ACS Engine</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [<span data-ttu-id="b87aa-129">Azure kapsayıcı Hizmeti'nde hello Swarm kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="b87aa-129">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="b87aa-130">Azure kapsayıcı kayıt defteri oluşturma</span><span class="sxs-lookup"><span data-stu-id="b87aa-130">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="b87aa-131">Oluşturulan Visual Studio Team Services hesabı ve ekip projesinde olması</span><span class="sxs-lookup"><span data-stu-id="b87aa-131">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="b87aa-132">Çatalı hello GitHub depo tooyour GitHub hesabı</span><span class="sxs-lookup"><span data-stu-id="b87aa-132">Fork hello GitHub repository tooyour GitHub account</span></span>](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> <span data-ttu-id="b87aa-133">Azure kapsayıcı Hizmeti'nde Hello Docker Swarm orchestrator eski tek başına Swarm kullanır.</span><span class="sxs-lookup"><span data-stu-id="b87aa-133">hello Docker Swarm orchestrator in Azure Container Service uses legacy standalone Swarm.</span></span> <span data-ttu-id="b87aa-134">Şu anda hello tümleşik [Swarm modu](https://docs.docker.com/engine/swarm/) (Docker 1.12 ve daha yüksek) desteklenen bir orchestrator Azure kapsayıcı Hizmeti'nde değil.</span><span class="sxs-lookup"><span data-stu-id="b87aa-134">Currently, hello integrated [Swarm mode](https://docs.docker.com/engine/swarm/) (in Docker 1.12 and higher) is not a supported orchestrator in Azure Container Service.</span></span> <span data-ttu-id="b87aa-135">Bu nedenle, kullanıyoruz [ACS altyapısı](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), topluluk katkıda [hızlı başlatma şablonunu](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), veya hello Docker çözümde [Azure Marketi](https://azuremarketplace.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b87aa-135">For this reason, we are using [ACS Engine](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), a community-contributed [quickstart template](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), or a Docker solution in hello [Azure Marketplace](https://azuremarketplace.microsoft.com).</span></span>
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="b87aa-136">1. adım: Visual Studio Team Services hesabınızın yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b87aa-136">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="b87aa-137">Bu bölümde, Visual Studio Team Services hesabınızın yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b87aa-137">In this section, you configure your Visual Studio Team Services account.</span></span> <span data-ttu-id="b87aa-138">Visual Studio Team Services projenizdeki tooconfigure VSTS Hizmetleri uç tıklatın hello **ayarları** simgesi hello araç ve seçin **Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="b87aa-138">tooconfigure VSTS Services Endpoints, in your Visual Studio Team Services project, click hello **Settings** icon in hello toolbar, and select **Services**.</span></span>

![Açık hizmet uç noktası](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a><span data-ttu-id="b87aa-140">Visual Studio Team Services ve Azure hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="b87aa-140">Connect Visual Studio Team Services and Azure account</span></span>

<span data-ttu-id="b87aa-141">VSTS projeniz ve Azure hesabınızda arasında bir bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b87aa-141">Set up a connection between your VSTS project and your Azure account.</span></span>

1. <span data-ttu-id="b87aa-142">Hello solda tıklatın **yeni hizmet uç noktası** > **Azure Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="b87aa-142">On hello left, click **New Service Endpoint** > **Azure Resource Manager**.</span></span>
2. <span data-ttu-id="b87aa-143">Azure hesabınızla tooauthorize VSTS toowork seçin, **abonelik** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="b87aa-143">tooauthorize VSTS toowork with your Azure account, select your **Subscription** and click **OK**.</span></span>

    ![Visual Studio Team Services - Azure yetkilendirmek](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="b87aa-145">Visual Studio Team Services ve GitHub Bağlan</span><span class="sxs-lookup"><span data-stu-id="b87aa-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="b87aa-146">VSTS projeniz, GitHub hesabınızda arasında bir bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b87aa-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="b87aa-147">Hello solda tıklatın **yeni hizmet uç noktası** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="b87aa-147">On hello left, click **New Service Endpoint** > **GitHub**.</span></span>
2. <span data-ttu-id="b87aa-148">GitHub hesabınızla tooauthorize VSTS toowork tıklatın **Authorize** ve açılır hello penceresinde hello yordamı izleyin.</span><span class="sxs-lookup"><span data-stu-id="b87aa-148">tooauthorize VSTS toowork with your GitHub account, click **Authorize** and follow hello procedure in hello window that opens.</span></span>

    ![Visual Studio Team Services - GitHub yetkilendirmek](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-tooyour-azure-container-service-cluster"></a><span data-ttu-id="b87aa-150">VSTS tooyour Azure kapsayıcı hizmeti kümesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="b87aa-150">Connect VSTS tooyour Azure Container Service cluster</span></span>

<span data-ttu-id="b87aa-151">Merhaba CI/CD ardışık düzenine alma önce hello son tooconfigure dış bağlantıları tooyour Docker Swarm kümesinde Azure adımlardır.</span><span class="sxs-lookup"><span data-stu-id="b87aa-151">hello last steps before getting into hello CI/CD pipeline are tooconfigure external connections tooyour Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="b87aa-152">Merhaba Docker Swarm kümesi için bir uç nokta türü ekleme **SSH**.</span><span class="sxs-lookup"><span data-stu-id="b87aa-152">For hello Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="b87aa-153">Ardından hello SSH bağlantı bilgilerini Swarm kümenizin (ana düğüm) girin.</span><span class="sxs-lookup"><span data-stu-id="b87aa-153">Then enter hello SSH connection information of your Swarm cluster (master node).</span></span>

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

<span data-ttu-id="b87aa-155">Tüm hello yapılandırma şimdi yapılır.</span><span class="sxs-lookup"><span data-stu-id="b87aa-155">All hello configuration is done now.</span></span> <span data-ttu-id="b87aa-156">Merhaba sonraki adımlarda oluşturan ve hello uygulama toohello Docker Swarm kümesi dağıtır hello CI/CD ardışık düzen oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b87aa-156">In hello next steps, you create hello CI/CD pipeline that builds and deploys hello application toohello Docker Swarm cluster.</span></span> 

## <a name="step-2-create-hello-build-definition"></a><span data-ttu-id="b87aa-157">2. adım: hello derleme tanımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b87aa-157">Step 2: Create hello build definition</span></span>

<span data-ttu-id="b87aa-158">Bu adımda, bir derleme tanımını VSTS projeniz için ayarlar ve kapsayıcı görüntülerinizi hello yapı iş akışı tanımlayın</span><span class="sxs-lookup"><span data-stu-id="b87aa-158">In this step, you set up a build definition for your VSTS project and define hello build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="b87aa-159">Başlangıç tanım Kurulumu</span><span class="sxs-lookup"><span data-stu-id="b87aa-159">Initial definition setup</span></span>

1. <span data-ttu-id="b87aa-160">toocreate bir derleme tanımınız connect Visual Studio Team Services proje ve tıklatın tooyour **yapı & yayın**.</span><span class="sxs-lookup"><span data-stu-id="b87aa-160">toocreate a build definition, connect tooyour Visual Studio Team Services project and click **Build & Release**.</span></span> <span data-ttu-id="b87aa-161">Merhaba, **yapı tanımları** 'yi tıklatın **+ yeni**.</span><span class="sxs-lookup"><span data-stu-id="b87aa-161">In hello **Build definitions** section, click **+ New**.</span></span> 

    ![Visual Studio Team Services - yeni yapı tanımı](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. <span data-ttu-id="b87aa-163">Select hello **boş işlem**.</span><span class="sxs-lookup"><span data-stu-id="b87aa-163">Select hello **Empty process**.</span></span>

    ![Visual Studio Team Services - yeni ve boş yapı tanımı](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. <span data-ttu-id="b87aa-165">Merhaba ardından **değişkenleri** sekmesinde ve iki yeni değişken oluşturma: **RegistryURL** ve **AgentURL**.</span><span class="sxs-lookup"><span data-stu-id="b87aa-165">Then, click hello **Variables** tab and create two new variables: **RegistryURL** and **AgentURL**.</span></span> <span data-ttu-id="b87aa-166">Kayıt defteri ve küme aracıları DNS Hello değerlerini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b87aa-166">Paste hello values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services - derleme değişkenleri yapılandırması](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. <span data-ttu-id="b87aa-168">Merhaba üzerinde **yapı tanımlarını** sayfası, açık hello **Tetikleyicileri** sekmesinde ve hello yapı toouse sürekli tümleştirme hello çatalı hello önkoşullarını oluşturulan hello MyShop projesinin yapılandırmak.</span><span class="sxs-lookup"><span data-stu-id="b87aa-168">On hello **Build Definitions** page, open hello **Triggers** tab and configure hello build toouse continuous integration with hello fork of hello MyShop project that you created in hello prerequisites.</span></span> <span data-ttu-id="b87aa-169">Ardından, seçin **toplu değişiklikleri**.</span><span class="sxs-lookup"><span data-stu-id="b87aa-169">Then, select **Batch changes**.</span></span> <span data-ttu-id="b87aa-170">Seçtiğinizden emin olun *docker linux* hello olarak **dal belirtimi**.</span><span class="sxs-lookup"><span data-stu-id="b87aa-170">Make sure that you select *docker-linux* as hello **Branch specification**.</span></span>

    ![Visual Studio Team Services - derleme deposu yapılandırma](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. <span data-ttu-id="b87aa-172">Son olarak, hello tıklatın **seçenekleri** sekmesinde ve hello varsayılan aracı sıra çok yapılandırma**barındırılan Linux Önizleme**.</span><span class="sxs-lookup"><span data-stu-id="b87aa-172">Finally, click hello **Options** tab and configure hello Default agent queue too**Hosted Linux Preview**.</span></span>

    ![Visual Studio Team Services - konak aracı yapılandırması](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-hello-build-workflow"></a><span data-ttu-id="b87aa-174">Merhaba yapı iş akışı tanımlama</span><span class="sxs-lookup"><span data-stu-id="b87aa-174">Define hello build workflow</span></span>
<span data-ttu-id="b87aa-175">Merhaba sonraki adımlar hello yapı iş akışı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="b87aa-175">hello next steps define hello build workflow.</span></span> <span data-ttu-id="b87aa-176">İlk olarak, tooconfigure hello kaynak hello kod gerekir.</span><span class="sxs-lookup"><span data-stu-id="b87aa-176">First, you need tooconfigure hello source of hello code.</span></span> <span data-ttu-id="b87aa-177">toodo, select **GitHub** ve **deposu** ve **şube** (docker-linux).</span><span class="sxs-lookup"><span data-stu-id="b87aa-177">toodo it, select **GitHub** and your **repository** and **branch** (docker-linux).</span></span>

![Visual Studio Team Services - yapılandırma kod kaynağı](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

<span data-ttu-id="b87aa-179">Hello için beş kapsayıcı görüntüleri toobuild vardır *MyShop* uygulama.</span><span class="sxs-lookup"><span data-stu-id="b87aa-179">There are five container images toobuild for hello *MyShop* application.</span></span> <span data-ttu-id="b87aa-180">Her görüntü hello Dockerfile hello proje klasörlerde yer alan kullanılarak oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="b87aa-180">Each image is built using hello Dockerfile located in hello project folders:</span></span>

* <span data-ttu-id="b87aa-181">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="b87aa-181">ProductsApi</span></span>
* <span data-ttu-id="b87aa-182">Ara sunucu</span><span class="sxs-lookup"><span data-stu-id="b87aa-182">Proxy</span></span>
* <span data-ttu-id="b87aa-183">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="b87aa-183">RatingsApi</span></span>
* <span data-ttu-id="b87aa-184">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="b87aa-184">RecommandationsApi</span></span>
* <span data-ttu-id="b87aa-185">ShopFront</span><span class="sxs-lookup"><span data-stu-id="b87aa-185">ShopFront</span></span>

<span data-ttu-id="b87aa-186">Her görüntü için iki Docker adımı, bir toobuild hello görüntüsü ve bir toopush hello görüntüsü hello Azure kapsayıcı kayıt defterinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="b87aa-186">You need two Docker steps for each image, one toobuild hello image, and one toopush hello image in hello Azure container registry.</span></span> 

1. <span data-ttu-id="b87aa-187">tooadd hello yapı iş akışı, bir adımda tıklatın **+ Ekle derleme adımı** seçip **Docker**.</span><span class="sxs-lookup"><span data-stu-id="b87aa-187">tooadd a step in hello build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services - eklemek derleme adımları](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. <span data-ttu-id="b87aa-189">Merhaba kullanan tek bir adımda yapılandırma her resmi için `docker build` komutu.</span><span class="sxs-lookup"><span data-stu-id="b87aa-189">For each image, configure one step that uses hello `docker build` command.</span></span>

    ![Visual Studio Team Services - Docker derleme](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    <span data-ttu-id="b87aa-191">Merhaba derleme işlemi, Azure kapsayıcı kaydınız hello seçin **görüntü yapı** eylem ve hello her görüntü tanımlar Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="b87aa-191">For hello build operation, select your Azure Container Registry, hello **Build an image** action, and hello Dockerfile that defines each image.</span></span> <span data-ttu-id="b87aa-192">Set hello **çalışma dizini** hello hello Dockerfile kök dizini olarak tanımlamak **görüntü adı**seçip **dahil en son etiket**.</span><span class="sxs-lookup"><span data-stu-id="b87aa-192">Set hello **Working Directory** as hello Dockerfile root directory, define hello **Image Name**, and select **Include Latest Tag**.</span></span>
    
    <span data-ttu-id="b87aa-193">Merhaba görüntü adı bu biçimde toobe vardır: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span><span class="sxs-lookup"><span data-stu-id="b87aa-193">hello Image Name has toobe in this format: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span></span> <span data-ttu-id="b87aa-194">Değiştir **[NAME]** hello görüntü adı ile:</span><span class="sxs-lookup"><span data-stu-id="b87aa-194">Replace **[NAME]** with hello image name:</span></span>
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. <span data-ttu-id="b87aa-195">Merhaba kullanır ikinci bir adım her görüntü için yapılandırma `docker push` komutu.</span><span class="sxs-lookup"><span data-stu-id="b87aa-195">For each image, configure a second step that uses hello `docker push` command.</span></span>

    ![Visual Studio Team Services - Docker gönderme](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    <span data-ttu-id="b87aa-197">Hello gönderme işlemi için Azure kapsayıcı kaydınız hello seçin **görüntü anında** eylem hello girin **görüntü adı** hello önceki adımı ve select yerleşik **dahil en son etiketi** .</span><span class="sxs-lookup"><span data-stu-id="b87aa-197">For hello push operation, select your Azure container registry, hello **Push an image** action, enter hello **Image Name** that is built in hello previous step and select **Include Latest Tag**.</span></span>

4. <span data-ttu-id="b87aa-198">Merhaba yapı yapılandırdıktan sonra ve her hello beş görüntüleri için adımları itme, hello daha fazla üç adımda iş akışı derleme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b87aa-198">After you configure hello build and push steps for each of hello five images, add three more steps in hello build workflow.</span></span>

   ![Visual Studio Team Services - komut satırı görev ekleme](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. <span data-ttu-id="b87aa-200">Bir bash betik tooreplace hello kullanan bir komut satırı görevi *RegistryURL* hello docker-compose.yml dosyası hello RegistryURL değişkeniyle geçişi.</span><span class="sxs-lookup"><span data-stu-id="b87aa-200">A command-line task that uses a bash script tooreplace hello *RegistryURL* occurrence in hello docker-compose.yml file with hello RegistryURL variable.</span></span> 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services - kayıt defteri URL dosyasıyla güncelleştirme oluştur](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. <span data-ttu-id="b87aa-202">Bir bash betik tooreplace hello kullanan bir komut satırı görevi *AgentURL* hello docker-compose.yml dosyası hello AgentURL değişkeniyle geçişi.</span><span class="sxs-lookup"><span data-stu-id="b87aa-202">A command-line task that uses a bash script tooreplace hello *AgentURL* occurrence in hello docker-compose.yml file with hello AgentURL variable.</span></span>
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. <span data-ttu-id="b87aa-203">Hello sürümde kullanılabilmesi için hello bırakır bir görev oluşturma dosyası derleme yapısı olarak güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="b87aa-203">A task that drops hello updated Compose file as a build artifact so it can be used in hello release.</span></span> <span data-ttu-id="b87aa-204">Ayrıntılar için ekran aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="b87aa-204">See hello following screen for details.</span></span>

         ![Visual Studio Team Services - yayımlama yapı](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services - Oluştur yayımlama dosyası](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. <span data-ttu-id="b87aa-207">Tıklatın **sıraya & Kaydet** tootest derleme tanımı.</span><span class="sxs-lookup"><span data-stu-id="b87aa-207">Click **Save & queue** tootest your build definition.</span></span>

   ![Visual Studio Team Services - Kaydet ve sırası](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services - yeni kuyruk](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. <span data-ttu-id="b87aa-210">Merhaba, **yapı** doğru bu ekranı toosee sahip:</span><span class="sxs-lookup"><span data-stu-id="b87aa-210">If hello **Build** is correct, you have toosee this screen:</span></span>

  ![Visual Studio Team Services - oluşturma başarılı oldu](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-hello-release-definition"></a><span data-ttu-id="b87aa-212">3. adım: hello yayın tanımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b87aa-212">Step 3: Create hello release definition</span></span>

<span data-ttu-id="b87aa-213">Visual Studio Team Services verir çok[sürümleri arasında ortamlarını](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="b87aa-213">Visual Studio Team Services allows you too[manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="b87aa-214">Sürekli dağıtım toomake kesintisiz bir şekilde uygulamanız farklı ortamınızı (örneğin, geliştirme, test, ön üretim ve üretim) üzerinde dağıtıldığından emin etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b87aa-214">You can enable continuous deployment toomake sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="b87aa-215">Azure kapsayıcı hizmeti Docker Swarm modu kümenizi temsil eden bir ortam oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b87aa-215">You can create an environment that represents your Azure Container Service Docker Swarm Mode cluster.</span></span>

![Visual Studio Team Services - sürüm tooACS](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="b87aa-217">Kurulum ilk sürüm</span><span class="sxs-lookup"><span data-stu-id="b87aa-217">Initial release setup</span></span>

1. <span data-ttu-id="b87aa-218">toocreate bir yayın tanımı tıklatın **sürümleri** > **+ sürüm**</span><span class="sxs-lookup"><span data-stu-id="b87aa-218">toocreate a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="b87aa-219">tooconfigure hello yapı kaynak tıklatın **yapıları** > **bir yapı kaynak bağlantı**.</span><span class="sxs-lookup"><span data-stu-id="b87aa-219">tooconfigure hello artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="b87aa-220">Burada, hello önceki adımda tanımlanan bu yeni sürüm tanımı toohello derleme bağlayın.</span><span class="sxs-lookup"><span data-stu-id="b87aa-220">Here, link this new release definition toohello build that you defined in hello previous step.</span></span> <span data-ttu-id="b87aa-221">Bundan sonra hello docker-compose.yml dosyası hello yayın işlemde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b87aa-221">After that, hello docker-compose.yml file is available in hello release process.</span></span>

    ![Visual Studio Team Services - sürüm yapıları](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. <span data-ttu-id="b87aa-223">tooconfigure hello sürüm tetikleme tıklatın **Tetikleyicileri** seçip **sürekli dağıtım**.</span><span class="sxs-lookup"><span data-stu-id="b87aa-223">tooconfigure hello release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="b87aa-224">Merhaba kümesi hello tetikleyici aynı yapı kaynağı.</span><span class="sxs-lookup"><span data-stu-id="b87aa-224">Set hello trigger on hello same artifact source.</span></span> <span data-ttu-id="b87aa-225">Bu ayar hello yapı başarıyla tamamlandığında, yeni bir sürüm başlayacağını sağlar.</span><span class="sxs-lookup"><span data-stu-id="b87aa-225">This setting ensures that a new release starts when hello build completes successfully.</span></span>

    ![Visual Studio Team Services - sürüm Tetikleyicileri](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. <span data-ttu-id="b87aa-227">tooconfigure hello sürüm, değişkenleri **değişkenleri** seçip **+ değişken** toocreate üç yeni değişkenlerle hello kayıt defteri başlangıç bilgileri: **docker.username**, **docker.password**, ve **docker.registry**.</span><span class="sxs-lookup"><span data-stu-id="b87aa-227">tooconfigure hello release variables, click **Variables** and select **+Variable** toocreate three new variables with hello info of hello registry: **docker.username**, **docker.password**, and **docker.registry**.</span></span> <span data-ttu-id="b87aa-228">Kayıt defteri ve küme aracıları DNS Hello değerlerini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b87aa-228">Paste hello values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services - derleme deposu yapılandırma](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > <span data-ttu-id="b87aa-230">Merhaba önceki ekranda gösterildiği gibi hello tıklayın **kilit** docker.password onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="b87aa-230">As shown on hello previous screen, click hello **Lock** checkbox in docker.password.</span></span> <span data-ttu-id="b87aa-231">Bu ayar, önemli toorestrict hello paroladır.</span><span class="sxs-lookup"><span data-stu-id="b87aa-231">This setting is important toorestrict hello password.</span></span>
    >

### <a name="define-hello-release-workflow"></a><span data-ttu-id="b87aa-232">Merhaba yayın iş akışı tanımlama</span><span class="sxs-lookup"><span data-stu-id="b87aa-232">Define hello release workflow</span></span>

<span data-ttu-id="b87aa-233">Merhaba yayın iş akışı eklediğiniz iki görevlerin oluşur.</span><span class="sxs-lookup"><span data-stu-id="b87aa-233">hello release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="b87aa-234">Görev toosecurely kopyalama hello yapılandırma dosyası tooa oluşturan *dağıtmak* daha önce yapılandırdığınız hello SSH bağlantısını kullanarak hello Docker Swarm ana düğümde, klasör.</span><span class="sxs-lookup"><span data-stu-id="b87aa-234">Configure a task toosecurely copy hello compose file tooa *deploy* folder on hello Docker Swarm master node, using hello SSH connection you configured previously.</span></span> <span data-ttu-id="b87aa-235">Ayrıntılar için ekran aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="b87aa-235">See hello following screen for details.</span></span>
    
    <span data-ttu-id="b87aa-236">Kaynak klasörü:```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span><span class="sxs-lookup"><span data-stu-id="b87aa-236">Source folder: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span></span>

    ![Visual Studio Team Services - sürüm SCP](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. <span data-ttu-id="b87aa-238">İkinci bir görev tooexecute bash komutu toorun yapılandırma `docker` ve `docker stack deploy` hello ana düğümde komutları.</span><span class="sxs-lookup"><span data-stu-id="b87aa-238">Configure a second task tooexecute a bash command toorun `docker` and `docker stack deploy` commands on hello master node.</span></span> <span data-ttu-id="b87aa-239">Ayrıntılar için ekran aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="b87aa-239">See hello following screen for details.</span></span>

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services - sürüm Bash](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    <span data-ttu-id="b87aa-241">Merhaba yöneticisinde yürütülen hello komut hello Docker CLI ve görevleri aşağıdaki hello Docker Compose CLI toodo hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="b87aa-241">hello command executed on hello master uses hello Docker CLI and hello Docker-Compose CLI toodo hello following tasks:</span></span>

    - <span data-ttu-id="b87aa-242">Toohello Azure kapsayıcı kayıt defterinde oturum (hello tanımlanan üç derleme değişkenleri kullanan **değişkenleri** sekmesinde)</span><span class="sxs-lookup"><span data-stu-id="b87aa-242">Log in toohello Azure container registry (it uses three build variables that are defined in hello **Variables** tab)</span></span>
    - <span data-ttu-id="b87aa-243">Merhaba tanımlamak **DOCKER_HOST** hello Swarm uç noktası ile değişken toowork (: 2375)</span><span class="sxs-lookup"><span data-stu-id="b87aa-243">Define hello **DOCKER_HOST** variable toowork with hello Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="b87aa-244">Toohello gidin *dağıtmak* güvenli kopyalama görevi önceki hello tarafından oluşturulan ve hello docker-compose.yml dosyası içeren klasör</span><span class="sxs-lookup"><span data-stu-id="b87aa-244">Navigate toohello *deploy* folder that was created by hello preceding secure copy task and that contains hello docker-compose.yml file</span></span> 
    - <span data-ttu-id="b87aa-245">Yürütme `docker stack deploy` hello yeni görüntüleri çekmek ve hello kapsayıcıları oluşturma komutları.</span><span class="sxs-lookup"><span data-stu-id="b87aa-245">Execute `docker stack deploy` commands that pull hello new images and create hello containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="b87aa-246">Merhaba önceki ekranda gösterildiği gibi hello bırakın **STDERR üzerinde başarısız** onay kutusu işaretli.</span><span class="sxs-lookup"><span data-stu-id="b87aa-246">As shown on hello previous screen, leave hello **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="b87aa-247">Bu ayar bize toocomplete hello yayın işlem nedeniyle çok sağlar`docker-compose` durdurma veya hello standart hata çıktısı üzerinde siliniyor kapsayıcılardır gibi birkaç tanılama iletilerini yazdırır.</span><span class="sxs-lookup"><span data-stu-id="b87aa-247">This setting allows us toocomplete hello release process due too`docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on hello standard error output.</span></span> <span data-ttu-id="b87aa-248">Merhaba onay kutusunu işaretlerseniz, tüm aşsa bile iyi Visual Studio Team Services hataları hello yayın sırasında oluştuğunu bildiriyor.</span><span class="sxs-lookup"><span data-stu-id="b87aa-248">If you check hello checkbox, Visual Studio Team Services reports that errors occurred during hello release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="b87aa-249">Bu yeni sürüm tanımını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b87aa-249">Save this new release definition.</span></span>

## <a name="step-4-test-hello-cicd-pipeline"></a><span data-ttu-id="b87aa-250">4. adım: hello CI/CD ardışık test etme</span><span class="sxs-lookup"><span data-stu-id="b87aa-250">Step 4: Test hello CI/CD pipeline</span></span>

<span data-ttu-id="b87aa-251">Merhaba yapılandırma ile yapılır, bu yeni saat tootest olan CI/CD ardışık düzen.</span><span class="sxs-lookup"><span data-stu-id="b87aa-251">Now that you are done with hello configuration, it's time tootest this new CI/CD pipeline.</span></span> <span data-ttu-id="b87aa-252">Merhaba tooupdate hello kaynak kodu ve yürütme hello olduğu en kolay yolu tootest GitHub depoya değiştirir.</span><span class="sxs-lookup"><span data-stu-id="b87aa-252">hello easiest way tootest it is tooupdate hello source code and commit hello changes into your GitHub repository.</span></span> <span data-ttu-id="b87aa-253">Birkaç saniye hello kod itme sonra Visual Studio Team Services içinde çalışan yeni bir derleme görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b87aa-253">A few seconds after you push hello code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="b87aa-254">Başarıyla tamamlandığında, yeni bir sürüm tetiklenir ve hello Azure kapsayıcı hizmeti kümesinde hello uygulamanın yeni sürümü hello dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="b87aa-254">Once completed successfully, a new release is triggered and deployed hello new version of hello application on hello Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b87aa-255">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b87aa-255">Next steps</span></span>

* <span data-ttu-id="b87aa-256">Merhaba CI/CD Visual Studio Team Services ile ilgili daha fazla bilgi için bkz: [VSTS derleme genel bakış](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="b87aa-256">For more information about CI/CD with Visual Studio Team Services, see hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
* <span data-ttu-id="b87aa-257">Merhaba ACS altyapısı hakkında daha fazla bilgi için bkz: [ACS altyapısı GitHub deposuna](https://github.com/Azure/acs-engine).</span><span class="sxs-lookup"><span data-stu-id="b87aa-257">For more information about ACS Engine, see hello [ACS Engine GitHub repo](https://github.com/Azure/acs-engine).</span></span>
* <span data-ttu-id="b87aa-258">Merhaba Docker Swarm modu hakkında daha fazla bilgi için bkz: [Docker Swarm moduna genel bakış](https://docs.docker.com/engine/swarm/).</span><span class="sxs-lookup"><span data-stu-id="b87aa-258">For more information about Docker Swarm mode, see hello [Docker Swarm mode overview](https://docs.docker.com/engine/swarm/).</span></span>
