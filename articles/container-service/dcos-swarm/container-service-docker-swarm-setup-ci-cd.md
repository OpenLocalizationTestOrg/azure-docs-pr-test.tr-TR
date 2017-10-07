---
title: "Azure kapsayıcı hizmeti ve Swarm ile aaaCI/CD | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Docker Swarm, bir Azure kapsayıcı kayıt defteri ve Visual Studio Team Services toodeliver sürekli olarak bir çok kapsayıcı .NET Core uygulaması ile kullanma"
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: "Docker, kapsayıcıları, mikro-services, Azure, Visual Studio Team Services, DevOps Swarm"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 35348800aa620469fb62ab3e5a02b33834359446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a><span data-ttu-id="5c003-104">Tam CI/CD ardışık düzen toodeploy Visual Studio Team Services kullanarak Docker Swarm ile Azure kapsayıcı hizmeti üzerinde çok kapsayıcı uygulama</span><span class="sxs-lookup"><span data-stu-id="5c003-104">Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services</span></span>

<span data-ttu-id="5c003-105">Aşağıdakilerden birini hello en büyük zorluklardan hello bulut için modern uygulamalar geliştirme mümkün toodeliver yüklenirken bu uygulamalara sürekli olarak.</span><span class="sxs-lookup"><span data-stu-id="5c003-105">One of hello biggest challenges when developing modern applications for hello cloud is being able toodeliver these applications continuously.</span></span> <span data-ttu-id="5c003-106">Bu makalede, tooimplement tam sürekli tümleştirme ve Docker Swarm, Azure kapsayıcı kayıt defteri ve Visual Studio Team Services ile Azure kapsayıcı hizmeti kullanarak dağıtım (CI/CD) ardışık nasıl oluşturulacağına öğrenin ve yayın yönetimi.</span><span class="sxs-lookup"><span data-stu-id="5c003-106">In this article, you learn how tooimplement a full continuous integration and deployment (CI/CD) pipeline using Azure Container Service with Docker Swarm, Azure Container Registry, and Visual Studio Team Services build and release management.</span></span>

<span data-ttu-id="5c003-107">Bu makalede, kullanılabilen basit bir uygulama dayalı [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), ASP.NET Core ile geliştirilen.</span><span class="sxs-lookup"><span data-stu-id="5c003-107">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), developed with ASP.NET Core.</span></span> <span data-ttu-id="5c003-108">Merhaba uygulaması dört farklı hizmetlerini oluşur: üç API'ları ve bir web ön uç web:</span><span class="sxs-lookup"><span data-stu-id="5c003-108">hello application is composed of four different services: three web APIs and one web front end:</span></span>

![MyShop örnek uygulama](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

<span data-ttu-id="5c003-110">Merhaba hedefi toodeliver Visual Studio Team Services kullanarak sürekli bir Docker Swarm kümesinde, bu bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="5c003-110">hello objective is toodeliver this application continuously in a Docker Swarm cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="5c003-111">Merhaba aşağıdaki ayrıntıları bu kesintisiz teslim ardışık düzen şekil:</span><span class="sxs-lookup"><span data-stu-id="5c003-111">hello following figure details this continuous delivery pipeline:</span></span>

![MyShop örnek uygulama](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

<span data-ttu-id="5c003-113">Kısa bir açıklama başlangıç adımları şöyledir:</span><span class="sxs-lookup"><span data-stu-id="5c003-113">Here is a brief explanation of hello steps:</span></span>

1. <span data-ttu-id="5c003-114">Kod değişiklikleri olan taahhüt toohello kaynak kodu deposu (burada, GitHub)</span><span class="sxs-lookup"><span data-stu-id="5c003-114">Code changes are committed toohello source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="5c003-115">Visual Studio Team Services derlemede GitHub tetikler</span><span class="sxs-lookup"><span data-stu-id="5c003-115">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="5c003-116">Visual Studio Team Services hello en son sürümünü hello kaynakları alır ve Merhaba uygulaması oluşturan tüm hello görüntü oluşturur</span><span class="sxs-lookup"><span data-stu-id="5c003-116">Visual Studio Team Services gets hello latest version of hello sources and builds all hello images that compose hello application</span></span> 
4. <span data-ttu-id="5c003-117">Visual Studio Team Services hello Azure kapsayıcı kayıt defteri hizmeti kullanılarak oluşturulan her görüntü tooa Docker kayıt defteri iter</span><span class="sxs-lookup"><span data-stu-id="5c003-117">Visual Studio Team Services pushes each image tooa Docker registry created using hello Azure Container Registry service</span></span> 
5. <span data-ttu-id="5c003-118">Yeni bir sürüm Visual Studio Team Services tetikler</span><span class="sxs-lookup"><span data-stu-id="5c003-118">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="5c003-119">Merhaba yayın hello Azure kapsayıcı hizmeti küme ana düğümünde SSH kullanarak bazı komutları çalıştırır</span><span class="sxs-lookup"><span data-stu-id="5c003-119">hello release runs some commands using SSH on hello Azure container service cluster master node</span></span> 
7. <span data-ttu-id="5c003-120">Docker Swarm hello küme çeken hello en son sürümünü hello görüntüleri</span><span class="sxs-lookup"><span data-stu-id="5c003-120">Docker Swarm on hello cluster pulls hello latest version of hello images</span></span> 
8. <span data-ttu-id="5c003-121">Merhaba uygulamanın yeni sürümü Hello Docker Compose kullanılarak dağıtılır</span><span class="sxs-lookup"><span data-stu-id="5c003-121">hello new version of hello application is deployed using Docker Compose</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5c003-122">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5c003-122">Prerequisites</span></span>

<span data-ttu-id="5c003-123">Bu öğreticiye başlamadan önce görevleri aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5c003-123">Before starting this tutorial, you need toocomplete hello following tasks:</span></span>

- [<span data-ttu-id="5c003-124">Azure Container Service'te Swarm kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c003-124">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)
- [<span data-ttu-id="5c003-125">Azure kapsayıcı Hizmeti'nde hello Swarm kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="5c003-125">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="5c003-126">Azure kapsayıcı kayıt defteri oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c003-126">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="5c003-127">Oluşturulan Visual Studio Team Services hesabı ve ekip projesinde olması</span><span class="sxs-lookup"><span data-stu-id="5c003-127">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="5c003-128">Çatalı hello GitHub depo tooyour GitHub hesabı</span><span class="sxs-lookup"><span data-stu-id="5c003-128">Fork hello GitHub repository tooyour GitHub account</span></span>](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="5c003-129">Ayrıca bir Ubuntu (14.04 veya 16.04) makinede yüklü Docker ile gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c003-129">You also need an Ubuntu (14.04 or 16.04) machine with Docker installed.</span></span> <span data-ttu-id="5c003-130">Bu makine kullanılan hello sırasında Visual Studio Team Services tarafından derleme ve sürüm işlemler.</span><span class="sxs-lookup"><span data-stu-id="5c003-130">This machine is used by Visual Studio Team Services during hello build and release processes.</span></span> <span data-ttu-id="5c003-131">Tek yönlü toocreate bu makine toouse hello hello kullanılabilir görüntüdür [Azure Marketi](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span><span class="sxs-lookup"><span data-stu-id="5c003-131">One way toocreate this machine is toouse hello image available in hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span></span> 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="5c003-132">1. adım: Visual Studio Team Services hesabınızın yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5c003-132">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="5c003-133">Bu bölümde, Visual Studio Team Services hesabınızın yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5c003-133">In this section, you configure your Visual Studio Team Services account.</span></span>

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a><span data-ttu-id="5c003-134">Visual Studio Team Services Linux derleme Aracısı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5c003-134">Configure a Visual Studio Team Services Linux build agent</span></span>

<span data-ttu-id="5c003-135">toocreate Docker görüntüler ve bu bir Visual Studio Team Services Azure kapsayıcı defterinden görüntülere Yapı anında iletme, tooregister Linux Aracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c003-135">toocreate Docker images and push these images into an Azure container registry from a Visual Studio Team Services build, you need tooregister a Linux agent.</span></span> <span data-ttu-id="5c003-136">Bu yükleme seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="5c003-136">You have these installation options:</span></span>

* [<span data-ttu-id="5c003-137">Linux üzerinde bir aracıyla Dağıt</span><span class="sxs-lookup"><span data-stu-id="5c003-137">Deploy an agent on Linux</span></span>](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [<span data-ttu-id="5c003-138">Docker toorun hello VSTS aracı kullanın</span><span class="sxs-lookup"><span data-stu-id="5c003-138">Use Docker toorun hello VSTS agent</span></span>](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-hello-docker-integration-vsts-extension"></a><span data-ttu-id="5c003-139">Merhaba Docker tümleştirmesi VSTS uzantısını yükleyin</span><span class="sxs-lookup"><span data-stu-id="5c003-139">Install hello Docker Integration VSTS extension</span></span>

<span data-ttu-id="5c003-140">Microsoft, yapıda VSTS uzantısı toowork docker'la sağlar ve işlemler bırakın.</span><span class="sxs-lookup"><span data-stu-id="5c003-140">Microsoft provides a VSTS extension toowork with Docker in build and release processes.</span></span> <span data-ttu-id="5c003-141">Bu uzantı hello kullanılabilir [VSTS Market](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span><span class="sxs-lookup"><span data-stu-id="5c003-141">This extension is available in hello [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span></span> <span data-ttu-id="5c003-142">Tıklatın **yükleme** tooadd bu uzantı tooyour VSTS hesabı:</span><span class="sxs-lookup"><span data-stu-id="5c003-142">Click **Install** tooadd this extension tooyour VSTS account:</span></span>

![Merhaba Docker tümleştirmesi yükleyin](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

<span data-ttu-id="5c003-144">Kimlik bilgilerinizi kullanarak tooconnect tooyour VSTS hesap istenir.</span><span class="sxs-lookup"><span data-stu-id="5c003-144">You are asked tooconnect tooyour VSTS account using your credentials.</span></span> 

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="5c003-145">Visual Studio Team Services ve GitHub Bağlan</span><span class="sxs-lookup"><span data-stu-id="5c003-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="5c003-146">VSTS projeniz, GitHub hesabınızda arasında bir bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5c003-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="5c003-147">Visual Studio Team Services projenizde hello tıklatın **ayarları** simgesi hello araç ve seçin **Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="5c003-147">In your Visual Studio Team Services project, click hello **Settings** icon in hello toolbar, and select **Services**.</span></span>

    ![Visual Studio Team Services - dış bağlantı](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. <span data-ttu-id="5c003-149">Hello solda tıklatın **yeni hizmet uç noktası** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="5c003-149">On hello left, click **New Service Endpoint** > **GitHub**.</span></span>

    ![Visual Studio Team Services - GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. <span data-ttu-id="5c003-151">GitHub hesabınızla tooauthorize VSTS toowork tıklatın **Authorize** ve açılır hello penceresinde hello yordamı izleyin.</span><span class="sxs-lookup"><span data-stu-id="5c003-151">tooauthorize VSTS toowork with your GitHub account, click **Authorize** and follow hello procedure in hello window that opens.</span></span>

    ![Visual Studio Team Services - GitHub yetkilendirmek](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-tooyour-azure-container-registry-and-azure-container-service-cluster"></a><span data-ttu-id="5c003-153">VSTS tooyour Azure kapsayıcı kayıt defteri ve Azure kapsayıcı hizmeti kümesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="5c003-153">Connect VSTS tooyour Azure container registry and Azure Container Service cluster</span></span>

<span data-ttu-id="5c003-154">Merhaba CI/CD ardışık düzenine alma önce hello son tooconfigure dış bağlantıları tooyour kapsayıcı kayıt defteri ve Docker Swarm kümenizde Azure adımlardır.</span><span class="sxs-lookup"><span data-stu-id="5c003-154">hello last steps before getting into hello CI/CD pipeline are tooconfigure external connections tooyour container registry and your Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="5c003-155">Merhaba, **Hizmetleri** Visual Studio Team Services projenizin ayarları ekleme Hizmeti uç noktası türü **Docker kayıt defteri**.</span><span class="sxs-lookup"><span data-stu-id="5c003-155">In hello **Services** settings of your Visual Studio Team Services project, add a service endpoint of type **Docker Registry**.</span></span> 

2. <span data-ttu-id="5c003-156">Açılır hello açılan penceresinde hello URL ve Azure kapsayıcı kaydınız hello kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="5c003-156">In hello popup that opens, enter hello URL and hello credentials of your Azure container registry.</span></span>

    ![Visual Studio Team Services - Docker kayıt defteri](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. <span data-ttu-id="5c003-158">Merhaba Docker Swarm kümesi için bir uç nokta türü ekleme **SSH**.</span><span class="sxs-lookup"><span data-stu-id="5c003-158">For hello Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="5c003-159">Ardından Swarm kümenizin hello SSH bağlantı bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="5c003-159">Then enter hello SSH connection information of your Swarm cluster.</span></span>

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

<span data-ttu-id="5c003-161">Tüm hello yapılandırma şimdi yapılır.</span><span class="sxs-lookup"><span data-stu-id="5c003-161">All hello configuration is done now.</span></span> <span data-ttu-id="5c003-162">Merhaba sonraki adımlarda oluşturan ve hello uygulama toohello Docker Swarm kümesi dağıtır hello CI/CD ardışık düzen oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5c003-162">In hello next steps, you create hello CI/CD pipeline that builds and deploys hello application toohello Docker Swarm cluster.</span></span> 

## <a name="step-2-create-hello-build-definition"></a><span data-ttu-id="5c003-163">2. adım: hello derleme tanımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c003-163">Step 2: Create hello build definition</span></span>

<span data-ttu-id="5c003-164">Bu adımda, yapı definitionfor VSTS projenizi ayarlayın ve kapsayıcı görüntülerinizi hello yapı iş akışı tanımlayın</span><span class="sxs-lookup"><span data-stu-id="5c003-164">In this step, you set up a build definitionfor your VSTS project and define hello build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="5c003-165">Başlangıç tanım Kurulumu</span><span class="sxs-lookup"><span data-stu-id="5c003-165">Initial definition setup</span></span>

1. <span data-ttu-id="5c003-166">toocreate bir derleme tanımınız connect Visual Studio Team Services proje ve tıklatın tooyour **yapı & yayın**.</span><span class="sxs-lookup"><span data-stu-id="5c003-166">toocreate a build definition, connect tooyour Visual Studio Team Services project and click **Build & Release**.</span></span> 

2. <span data-ttu-id="5c003-167">Merhaba, **yapı tanımları** 'yi tıklatın **+ yeni**.</span><span class="sxs-lookup"><span data-stu-id="5c003-167">In hello **Build definitions** section, click **+ New**.</span></span> <span data-ttu-id="5c003-168">Select hello **boş** şablonu.</span><span class="sxs-lookup"><span data-stu-id="5c003-168">Select hello **Empty** template.</span></span>

    ![Visual Studio Team Services - yeni yapı tanımı](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. <span data-ttu-id="5c003-170">GitHub depo ile kaynak denetimi Hello yeni yapı yapılandırma **sürekli tümleştirme**ve Linux Aracısı kayıtlı olduğu select hello Aracısı sırası.</span><span class="sxs-lookup"><span data-stu-id="5c003-170">Configure hello new build with a GitHub repository source, check **Continuous integration**, and select hello agent queue where you registered your Linux agent.</span></span> <span data-ttu-id="5c003-171">Tıklatın **oluşturma** toocreate hello yapı tanımı.</span><span class="sxs-lookup"><span data-stu-id="5c003-171">Click **Create** toocreate hello build definition.</span></span>

    ![Visual Studio Team Services - derleme tanımı oluştur](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. <span data-ttu-id="5c003-173">Merhaba üzerinde **yapı tanımlarını** sayfasında, ilk hello'ni açın **depo** sekmesinde ve hello yapı toouse hello çatalı hello önkoşullarını oluşturulan hello MyShop projesinin yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5c003-173">On hello **Build Definitions** page, first open hello **Repository** tab and configure hello build toouse hello fork of hello MyShop project that you created in hello prerequisites.</span></span> <span data-ttu-id="5c003-174">Seçtiğinizden emin olun *acs belgeleri* hello olarak **varsayılan dalı**.</span><span class="sxs-lookup"><span data-stu-id="5c003-174">Make sure that you select *acs-docs* as hello **Default branch**.</span></span>

    ![Visual Studio Team Services - derleme deposu yapılandırma](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. <span data-ttu-id="5c003-176">Merhaba üzerinde **Tetikleyicileri** sekmesinde, her yürütme tetiklenen hello yapı toobe yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5c003-176">On hello **Triggers** tab, configure hello build toobe triggered after each commit.</span></span> <span data-ttu-id="5c003-177">Seçin **sürekli tümleştirme** ve **toplu değişiklikleri**.</span><span class="sxs-lookup"><span data-stu-id="5c003-177">Select **Continuous integration** and **Batch changes**.</span></span>

    ![Visual Studio Team Services - derleme tetikleyici yapılandırması](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-hello-build-workflow"></a><span data-ttu-id="5c003-179">Merhaba yapı iş akışı tanımlama</span><span class="sxs-lookup"><span data-stu-id="5c003-179">Define hello build workflow</span></span>
<span data-ttu-id="5c003-180">Merhaba sonraki adımlar hello yapı iş akışı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="5c003-180">hello next steps define hello build workflow.</span></span> <span data-ttu-id="5c003-181">Hello için beş kapsayıcı görüntüleri toobuild vardır *MyShop* uygulama.</span><span class="sxs-lookup"><span data-stu-id="5c003-181">There are five container images toobuild for hello *MyShop* application.</span></span> <span data-ttu-id="5c003-182">Her görüntü hello Dockerfile hello proje klasörlerde yer alan kullanılarak oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="5c003-182">Each image is built using hello Dockerfile located in hello project folders:</span></span>

* <span data-ttu-id="5c003-183">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="5c003-183">ProductsApi</span></span>
* <span data-ttu-id="5c003-184">Ara sunucu</span><span class="sxs-lookup"><span data-stu-id="5c003-184">Proxy</span></span>
* <span data-ttu-id="5c003-185">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="5c003-185">RatingsApi</span></span>
* <span data-ttu-id="5c003-186">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="5c003-186">RecommandationsApi</span></span>
* <span data-ttu-id="5c003-187">ShopFront</span><span class="sxs-lookup"><span data-stu-id="5c003-187">ShopFront</span></span>

<span data-ttu-id="5c003-188">Tooadd iki Docker adımları her görüntü için bir toobuild hello görüntüsü ve bir toopush hello görüntüsü hello Azure kapsayıcı kayıt defterinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c003-188">You need tooadd two Docker steps for each image, one toobuild hello image, and one toopush hello image in hello Azure container registry.</span></span> 

1. <span data-ttu-id="5c003-189">tooadd hello yapı iş akışı, bir adımda tıklatın **+ Ekle derleme adımı** seçip **Docker**.</span><span class="sxs-lookup"><span data-stu-id="5c003-189">tooadd a step in hello build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services - eklemek derleme adımları](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. <span data-ttu-id="5c003-191">Merhaba kullanan tek bir adımda yapılandırma her resmi için `docker build` komutu.</span><span class="sxs-lookup"><span data-stu-id="5c003-191">For each image, configure one step that uses hello `docker build` command.</span></span>

    ![Visual Studio Team Services - Docker derleme](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    <span data-ttu-id="5c003-193">Merhaba derleme işlemi, Azure kapsayıcı kaydınız hello seçin **görüntü yapı** eylem ve hello her görüntü tanımlar Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="5c003-193">For hello build operation, select your Azure container registry, hello **Build an image** action, and hello Dockerfile that defines each image.</span></span> <span data-ttu-id="5c003-194">Set hello **yapı bağlam** Dockerfile hello dizin kök ve hello tanımlamak **görüntü adı**.</span><span class="sxs-lookup"><span data-stu-id="5c003-194">Set hello **Build context** as hello Dockerfile root directory, and define hello **Image Name**.</span></span> 
    
    <span data-ttu-id="5c003-195">Ekran önceki hello üzerinde gösterildiği gibi Azure kapsayıcı kaydınız URI'sini hello ile Merhaba görüntü adı başlatın.</span><span class="sxs-lookup"><span data-stu-id="5c003-195">As shown on hello preceding screen, start hello image name with hello URI of your Azure container registry.</span></span> <span data-ttu-id="5c003-196">(Bu örnekte hello derleme tanımlayıcı gibi hello görüntüsünün yapı değişken tooparameterize hello etiketini de kullanabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="5c003-196">(You can also use a build variable tooparameterize hello tag of hello image, such as hello build identifier in this example.)</span></span>

3. <span data-ttu-id="5c003-197">Merhaba kullanır ikinci bir adım her görüntü için yapılandırma `docker push` komutu.</span><span class="sxs-lookup"><span data-stu-id="5c003-197">For each image, configure a second step that uses hello `docker push` command.</span></span>

    ![Visual Studio Team Services - Docker gönderme](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    <span data-ttu-id="5c003-199">Hello gönderme işlemi için Azure kapsayıcı kaydınız hello seçin **görüntü anında** eylemi ve hello girin **görüntü adı** hello önceki adımda oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="5c003-199">For hello push operation, select your Azure container registry, hello **Push an image** action, and enter hello **Image Name** that is built in hello previous step.</span></span>

4. <span data-ttu-id="5c003-200">Merhaba yapı yapılandırdıktan sonra ve her hello beş görüntüleri için adımları anında, hello daha fazla iki adımda iş akışı derleme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5c003-200">After you configure hello build and push steps for each of hello five images, add two more steps in hello build workflow.</span></span>

    <span data-ttu-id="5c003-201">a.</span><span class="sxs-lookup"><span data-stu-id="5c003-201">a.</span></span> <span data-ttu-id="5c003-202">Bir bash betik tooreplace hello kullanan bir komut satırı görevi *BuildNumber* hello docker-compose.yml dosyası hello geçerli ile olay kimliği oluşturma Ayrıntılar için ekran aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="5c003-202">A command-line task that uses a bash script tooreplace hello *BuildNumber* occurrence in hello docker-compose.yml file with hello current build Id. See hello following screen for details.</span></span>

    ![Visual Studio Team Services - güncelleştirme oluşturma dosya](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    <span data-ttu-id="5c003-204">b.</span><span class="sxs-lookup"><span data-stu-id="5c003-204">b.</span></span> <span data-ttu-id="5c003-205">Hello sürümde kullanılabilmesi için hello bırakır bir görev oluşturma dosyası derleme yapısı olarak güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="5c003-205">A task that drops hello updated Compose file as a build artifact so it can be used in hello release.</span></span> <span data-ttu-id="5c003-206">Ayrıntılar için ekran aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="5c003-206">See hello following screen for details.</span></span>

    ![Visual Studio Team Services - Oluştur yayımlama dosyası](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. <span data-ttu-id="5c003-208">Tıklatın **kaydetmek** ve yapı tanımının adı.</span><span class="sxs-lookup"><span data-stu-id="5c003-208">Click **Save** and name your build definition.</span></span>

## <a name="step-3-create-hello-release-definition"></a><span data-ttu-id="5c003-209">3. adım: hello yayın tanımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c003-209">Step 3: Create hello release definition</span></span>

<span data-ttu-id="5c003-210">Visual Studio Team Services verir çok[sürümleri arasında ortamlarını](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="5c003-210">Visual Studio Team Services allows you too[manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="5c003-211">Sürekli dağıtım toomake kesintisiz bir şekilde uygulamanız farklı ortamınızı (örneğin, geliştirme, test, ön üretim ve üretim) üzerinde dağıtıldığından emin etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c003-211">You can enable continuous deployment toomake sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="5c003-212">Azure kapsayıcı hizmeti Docker Swarm kümesi temsil eden yeni bir ortam oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c003-212">You can create a new environment that represents your Azure Container Service Docker Swarm cluster.</span></span>

![Visual Studio Team Services - sürüm tooACS](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="5c003-214">Kurulum ilk sürüm</span><span class="sxs-lookup"><span data-stu-id="5c003-214">Initial release setup</span></span>

1. <span data-ttu-id="5c003-215">toocreate bir yayın tanımı tıklatın **sürümleri** > **+ sürüm**</span><span class="sxs-lookup"><span data-stu-id="5c003-215">toocreate a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="5c003-216">tooconfigure hello yapı kaynak tıklatın **yapıları** > **bir yapı kaynak bağlantı**.</span><span class="sxs-lookup"><span data-stu-id="5c003-216">tooconfigure hello artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="5c003-217">Burada, hello önceki adımda tanımlanan bu yeni sürüm tanımı toohello derleme bağlayın.</span><span class="sxs-lookup"><span data-stu-id="5c003-217">Here, link this new release definition toohello build that you defined in hello previous step.</span></span> <span data-ttu-id="5c003-218">Bunu yaparak, hello docker-compose.yml dosyası hello yayın işlemde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5c003-218">By doing this, hello docker-compose.yml file is available in hello release process.</span></span>

    ![Visual Studio Team Services - sürüm yapıları](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. <span data-ttu-id="5c003-220">tooconfigure hello sürüm tetikleme tıklatın **Tetikleyicileri** seçip **sürekli dağıtım**.</span><span class="sxs-lookup"><span data-stu-id="5c003-220">tooconfigure hello release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="5c003-221">Merhaba kümesi hello tetikleyici aynı yapı kaynağı.</span><span class="sxs-lookup"><span data-stu-id="5c003-221">Set hello trigger on hello same artifact source.</span></span> <span data-ttu-id="5c003-222">Bu ayar hello yapı başarıyla tamamlanır tamamlanmaz yeni bir sürüm başlayacağını sağlar.</span><span class="sxs-lookup"><span data-stu-id="5c003-222">This setting ensures that a new release starts as soon as hello build completes successfully.</span></span>

    ![Visual Studio Team Services - sürüm Tetikleyicileri](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-hello-release-workflow"></a><span data-ttu-id="5c003-224">Merhaba yayın iş akışı tanımlama</span><span class="sxs-lookup"><span data-stu-id="5c003-224">Define hello release workflow</span></span>

<span data-ttu-id="5c003-225">Merhaba yayın iş akışı eklediğiniz iki görevlerin oluşur.</span><span class="sxs-lookup"><span data-stu-id="5c003-225">hello release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="5c003-226">Görev toosecurely kopyalama hello yapılandırma dosyası tooa oluşturan *dağıtmak* daha önce yapılandırdığınız hello SSH bağlantısını kullanarak hello Docker Swarm ana düğümde, klasör.</span><span class="sxs-lookup"><span data-stu-id="5c003-226">Configure a task toosecurely copy hello compose file tooa *deploy* folder on hello Docker Swarm master node, using hello SSH connection you configured previously.</span></span> <span data-ttu-id="5c003-227">Ayrıntılar için ekran aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="5c003-227">See hello following screen for details.</span></span>

    ![Visual Studio Team Services - sürüm SCP](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. <span data-ttu-id="5c003-229">İkinci bir görev tooexecute bash komutu toorun yapılandırma `docker` ve `docker-compose` hello ana düğümde komutları.</span><span class="sxs-lookup"><span data-stu-id="5c003-229">Configure a second task tooexecute a bash command toorun `docker` and `docker-compose` commands on hello master node.</span></span> <span data-ttu-id="5c003-230">Ayrıntılar için ekran aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="5c003-230">See hello following screen for details.</span></span>

    ![Visual Studio Team Services - sürüm Bash](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    <span data-ttu-id="5c003-232">Hello Yöneticisi kullanım hello Docker CLI ve görevleri aşağıdaki hello Docker Compose CLI toodo hello yürütülen hello komut:</span><span class="sxs-lookup"><span data-stu-id="5c003-232">hello command executed on hello master use hello Docker CLI and hello Docker-Compose CLI toodo hello following tasks:</span></span>

    - <span data-ttu-id="5c003-233">Oturum açma toohello Azure kapsayıcı kayıt defteri (hello tanımlanan üç yapı variab'les kullanan **değişkenleri** sekmesinde)</span><span class="sxs-lookup"><span data-stu-id="5c003-233">Login toohello Azure container registry (it uses three build variab\`les that are defined in hello **Variables** tab)</span></span>
    - <span data-ttu-id="5c003-234">Merhaba tanımlamak **DOCKER_HOST** hello Swarm uç noktası ile değişken toowork (: 2375)</span><span class="sxs-lookup"><span data-stu-id="5c003-234">Define hello **DOCKER_HOST** variable toowork with hello Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="5c003-235">Toohello gidin *dağıtmak* güvenli kopyalama görevi önceki hello tarafından oluşturulan ve hello docker-compose.yml dosyası içeren klasör</span><span class="sxs-lookup"><span data-stu-id="5c003-235">Navigate toohello *deploy* folder that was created by hello preceding secure copy task and that contains hello docker-compose.yml file</span></span> 
    - <span data-ttu-id="5c003-236">Yürütme `docker-compose` hello yeni görüntüleri pull komutlarını Durdur hello Hizmetleri, hello Hizmetleri kaldırın ve Merhaba kapsayıcılara oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5c003-236">Execute `docker-compose` commands that pull hello new images, stop hello services, remove hello services, and create hello containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="5c003-237">Ekran önceki hello üzerinde gösterildiği gibi hello bırakın **STDERR üzerinde başarısız** onay kutusu işaretli.</span><span class="sxs-lookup"><span data-stu-id="5c003-237">As shown on hello preceding screen, leave hello **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="5c003-238">Bunun nedeni bir önemli ayarı, `docker-compose` durdurma veya hello standart hata çıktısı üzerinde siliniyor kapsayıcılardır gibi birkaç tanılama iletilerini yazdırır.</span><span class="sxs-lookup"><span data-stu-id="5c003-238">This is an important setting, because `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on hello standard error output.</span></span> <span data-ttu-id="5c003-239">Merhaba onay kutusunu işaretlerseniz, tüm aşsa bile iyi Visual Studio Team Services hataları hello yayın sırasında oluştuğunu bildiriyor.</span><span class="sxs-lookup"><span data-stu-id="5c003-239">If you check hello checkbox, Visual Studio Team Services reports that errors occurred during hello release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="5c003-240">Bu yeni sürüm tanımını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5c003-240">Save this new release definition.</span></span>


>[!NOTE]
><span data-ttu-id="5c003-241">Bu dağıtım olduğundan biz hello eski hizmetleri durdurma ve hello çalıştıran yeni bir miktar kapalı kalma süresi içerir.</span><span class="sxs-lookup"><span data-stu-id="5c003-241">This deployment includes some downtime because we are stopping hello old services and running hello new one.</span></span> <span data-ttu-id="5c003-242">Bu olası tooavoid mavi yeşil dağıtım yaparak olan budur.</span><span class="sxs-lookup"><span data-stu-id="5c003-242">It is possible tooavoid this by doing a blue-green deployment.</span></span>
>

## <a name="step-4-test-hello-cicd-pipeline"></a><span data-ttu-id="5c003-243">4. Adım.</span><span class="sxs-lookup"><span data-stu-id="5c003-243">Step 4.</span></span> <span data-ttu-id="5c003-244">Test hello CI/CD ardışık düzen</span><span class="sxs-lookup"><span data-stu-id="5c003-244">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="5c003-245">Merhaba yapılandırma ile yapılır, bu yeni saat tootest olan CI/CD ardışık düzen.</span><span class="sxs-lookup"><span data-stu-id="5c003-245">Now that you are done with hello configuration, it's time tootest this new CI/CD pipeline.</span></span> <span data-ttu-id="5c003-246">Merhaba tooupdate hello kaynak kodu ve yürütme hello olduğu en kolay yolu tootest GitHub depoya değiştirir.</span><span class="sxs-lookup"><span data-stu-id="5c003-246">hello easiest way tootest it is tooupdate hello source code and commit hello changes into your GitHub repository.</span></span> <span data-ttu-id="5c003-247">Birkaç saniye hello kod itme sonra Visual Studio Team Services içinde çalışan yeni bir derleme görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5c003-247">A few seconds after you push hello code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="5c003-248">Başarıyla tamamlandığında, yeni bir sürüm tetiklenir ve hello hello Azure kapsayıcı hizmeti kümesinde hello uygulamasının yeni sürümünü dağıtır.</span><span class="sxs-lookup"><span data-stu-id="5c003-248">Once completed successfully, a new release will be triggered and will deploy hello new version of hello application on hello Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c003-249">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="5c003-249">Next Steps</span></span>

* <span data-ttu-id="5c003-250">Merhaba CI/CD Visual Studio Team Services ile ilgili daha fazla bilgi için bkz: [VSTS derleme genel bakış](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="5c003-250">For more information about CI/CD with Visual Studio Team Services, see hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
