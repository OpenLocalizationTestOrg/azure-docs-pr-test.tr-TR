---
title: "CI/CD Azure kapsayıcı hizmeti ve Swarm ile | Microsoft Docs"
description: "Azure kapsayıcı hizmeti sürekli olarak çok kapsayıcı .NET Core uygulama göndermek için Docker Swarm, bir Azure kapsayıcı kayıt defteri ve Visual Studio Team Services ile kullanma"
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
ms.openlocfilehash: 99c27c37218a35d2a3416d6edd5e0a871cd5c011
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="full-cicd-pipeline-to-deploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a><span data-ttu-id="44dec-104">Visual Studio Team Services kullanarak Docker Swarm ile Azure kapsayıcı hizmeti üzerinde çok kapsayıcı uygulama dağıtmak için tam CI/CD ardışık düzen</span><span class="sxs-lookup"><span data-stu-id="44dec-104">Full CI/CD pipeline to deploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services</span></span>

<span data-ttu-id="44dec-105">Modern bulut uygulamaları geliştirirken en büyük zorluklardan biri, bu uygulamalara sürekli olarak teslim etmek mümkün yapılıyor.</span><span class="sxs-lookup"><span data-stu-id="44dec-105">One of the biggest challenges when developing modern applications for the cloud is being able to deliver these applications continuously.</span></span> <span data-ttu-id="44dec-106">Bu makalede, bir tam sürekli tümleştirme ve Docker Swarm, Azure kapsayıcı kayıt defteri ve Visual Studio Team Services yapı ile Azure kapsayıcı hizmeti kullanılarak (CI/CD) dağıtım ardışık düzen uygulamak ve yayın Yönetimi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="44dec-106">In this article, you learn how to implement a full continuous integration and deployment (CI/CD) pipeline using Azure Container Service with Docker Swarm, Azure Container Registry, and Visual Studio Team Services build and release management.</span></span>

<span data-ttu-id="44dec-107">Bu makalede, kullanılabilen basit bir uygulama dayalı [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), ASP.NET Core ile geliştirilen.</span><span class="sxs-lookup"><span data-stu-id="44dec-107">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), developed with ASP.NET Core.</span></span> <span data-ttu-id="44dec-108">Uygulama dört farklı hizmetlerinden oluşur: üç API'ları ve bir web ön uç web:</span><span class="sxs-lookup"><span data-stu-id="44dec-108">The application is composed of four different services: three web APIs and one web front end:</span></span>

![MyShop örnek uygulama](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

<span data-ttu-id="44dec-110">Amacı, bu uygulama, Visual Studio Team Services kullanarak bir Docker Swarm kümesinde, sürekli olarak teslim etmek sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="44dec-110">The objective is to deliver this application continuously in a Docker Swarm cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="44dec-111">Aşağıdaki şekilde bu kesintisiz teslim ardışık düzen ayrıntıları:</span><span class="sxs-lookup"><span data-stu-id="44dec-111">The following figure details this continuous delivery pipeline:</span></span>

![MyShop örnek uygulama](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

<span data-ttu-id="44dec-113">Kısa bir açıklama adımları şöyledir:</span><span class="sxs-lookup"><span data-stu-id="44dec-113">Here is a brief explanation of the steps:</span></span>

1. <span data-ttu-id="44dec-114">Kod değişiklikleri kaynak kodu depoya taahhüt (burada, GitHub)</span><span class="sxs-lookup"><span data-stu-id="44dec-114">Code changes are committed to the source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="44dec-115">Visual Studio Team Services derlemede GitHub tetikler</span><span class="sxs-lookup"><span data-stu-id="44dec-115">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="44dec-116">Visual Studio Team Services kaynakları en son sürümünü alır ve uygulamayı oluşturan tüm görüntü oluşturur</span><span class="sxs-lookup"><span data-stu-id="44dec-116">Visual Studio Team Services gets the latest version of the sources and builds all the images that compose the application</span></span> 
4. <span data-ttu-id="44dec-117">Visual Studio Team Services her görüntü Azure kapsayıcı kayıt defteri hizmeti kullanılarak oluşturulan bir Docker kayıt defterine iter.</span><span class="sxs-lookup"><span data-stu-id="44dec-117">Visual Studio Team Services pushes each image to a Docker registry created using the Azure Container Registry service</span></span> 
5. <span data-ttu-id="44dec-118">Yeni bir sürüm Visual Studio Team Services tetikler</span><span class="sxs-lookup"><span data-stu-id="44dec-118">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="44dec-119">Azure kapsayıcı hizmeti küme ana düğümünde SSH kullanarak bazı komutları yayın çalıştırır</span><span class="sxs-lookup"><span data-stu-id="44dec-119">The release runs some commands using SSH on the Azure container service cluster master node</span></span> 
7. <span data-ttu-id="44dec-120">Docker Swarm kümesinde görüntüleri en son sürümünü çeker</span><span class="sxs-lookup"><span data-stu-id="44dec-120">Docker Swarm on the cluster pulls the latest version of the images</span></span> 
8. <span data-ttu-id="44dec-121">Uygulamanın yeni sürümü Docker Compose kullanılarak dağıtılır</span><span class="sxs-lookup"><span data-stu-id="44dec-121">The new version of the application is deployed using Docker Compose</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="44dec-122">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="44dec-122">Prerequisites</span></span>

<span data-ttu-id="44dec-123">Bu öğreticiye başlamadan önce aşağıdaki görevleri tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="44dec-123">Before starting this tutorial, you need to complete the following tasks:</span></span>

- [<span data-ttu-id="44dec-124">Azure Container Service'te Swarm kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="44dec-124">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)
- [<span data-ttu-id="44dec-125">Azure Container Service'teki Swarm kümesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="44dec-125">Connect with the Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="44dec-126">Azure kapsayıcı kayıt defteri oluşturma</span><span class="sxs-lookup"><span data-stu-id="44dec-126">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="44dec-127">Oluşturulan Visual Studio Team Services hesabı ve ekip projesinde olması</span><span class="sxs-lookup"><span data-stu-id="44dec-127">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="44dec-128">GitHub hesabınızda GitHub depoyu çatallaştırmanız</span><span class="sxs-lookup"><span data-stu-id="44dec-128">Fork the GitHub repository to your GitHub account</span></span>](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="44dec-129">Ayrıca bir Ubuntu (14.04 veya 16.04) makinede yüklü Docker ile gerekir.</span><span class="sxs-lookup"><span data-stu-id="44dec-129">You also need an Ubuntu (14.04 or 16.04) machine with Docker installed.</span></span> <span data-ttu-id="44dec-130">Bu makinede Visual Studio Team Services tarafından derleme ve sürüm işlemleri sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="44dec-130">This machine is used by Visual Studio Team Services during the build and release processes.</span></span> <span data-ttu-id="44dec-131">Bu makine oluşturmanın yollarından biri, görüntünün bulunan kullanmaktır [Azure Marketi](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span><span class="sxs-lookup"><span data-stu-id="44dec-131">One way to create this machine is to use the image available in the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span></span> 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="44dec-132">1. adım: Visual Studio Team Services hesabınızın yapılandırma</span><span class="sxs-lookup"><span data-stu-id="44dec-132">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="44dec-133">Bu bölümde, Visual Studio Team Services hesabınızın yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="44dec-133">In this section, you configure your Visual Studio Team Services account.</span></span>

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a><span data-ttu-id="44dec-134">Visual Studio Team Services Linux derleme Aracısı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="44dec-134">Configure a Visual Studio Team Services Linux build agent</span></span>

<span data-ttu-id="44dec-135">Docker görüntüleri oluşturmak ve bu görüntüleri Visual Studio Team Services derleme Azure kapsayıcı kayıt defterine itme için Linux Aracısı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="44dec-135">To create Docker images and push these images into an Azure container registry from a Visual Studio Team Services build, you need to register a Linux agent.</span></span> <span data-ttu-id="44dec-136">Bu yükleme seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="44dec-136">You have these installation options:</span></span>

* [<span data-ttu-id="44dec-137">Linux üzerinde bir aracıyla Dağıt</span><span class="sxs-lookup"><span data-stu-id="44dec-137">Deploy an agent on Linux</span></span>](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [<span data-ttu-id="44dec-138">VSTS Aracısı'nı çalıştırmak için Docker kullanın</span><span class="sxs-lookup"><span data-stu-id="44dec-138">Use Docker to run the VSTS agent</span></span>](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-the-docker-integration-vsts-extension"></a><span data-ttu-id="44dec-139">Docker tümleştirmesi VSTS uzantısını yükleyin</span><span class="sxs-lookup"><span data-stu-id="44dec-139">Install the Docker Integration VSTS extension</span></span>

<span data-ttu-id="44dec-140">Microsoft, yapı Docker ile çalışmaya ve işlemler yayın VSTS uzantısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="44dec-140">Microsoft provides a VSTS extension to work with Docker in build and release processes.</span></span> <span data-ttu-id="44dec-141">Bu uzantı kullanılabilir [VSTS Market](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span><span class="sxs-lookup"><span data-stu-id="44dec-141">This extension is available in the [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span></span> <span data-ttu-id="44dec-142">Tıklatın **yükleme** bu uzantı VSTS hesabınızı eklemek için:</span><span class="sxs-lookup"><span data-stu-id="44dec-142">Click **Install** to add this extension to your VSTS account:</span></span>

![Docker tümleştirmesi yükleyin](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

<span data-ttu-id="44dec-144">VSTS hesabınıza kimlik bilgilerinizi kullanarak bağlanın istenir.</span><span class="sxs-lookup"><span data-stu-id="44dec-144">You are asked to connect to your VSTS account using your credentials.</span></span> 

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="44dec-145">Visual Studio Team Services ve GitHub Bağlan</span><span class="sxs-lookup"><span data-stu-id="44dec-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="44dec-146">VSTS projeniz, GitHub hesabınızda arasında bir bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="44dec-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="44dec-147">Visual Studio Team Services projenizi tıklatın **ayarları** simgesini seçin ve araç **Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="44dec-147">In your Visual Studio Team Services project, click the **Settings** icon in the toolbar, and select **Services**.</span></span>

    ![Visual Studio Team Services - dış bağlantı](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. <span data-ttu-id="44dec-149">Sol bölmede, tıklatın **yeni hizmet uç noktası** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="44dec-149">On the left, click **New Service Endpoint** > **GitHub**.</span></span>

    ![Visual Studio Team Services - GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. <span data-ttu-id="44dec-151">GitHub hesabınızla çalışmaya VSTS yetkilendirmek için tıklatın **Authorize** ve açılır pencere yordamı izleyin.</span><span class="sxs-lookup"><span data-stu-id="44dec-151">To authorize VSTS to work with your GitHub account, click **Authorize** and follow the procedure in the window that opens.</span></span>

    ![Visual Studio Team Services - GitHub yetkilendirmek](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-to-your-azure-container-registry-and-azure-container-service-cluster"></a><span data-ttu-id="44dec-153">VSTS, Azure kapsayıcı kayıt defteri ve Azure kapsayıcı hizmeti kümesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="44dec-153">Connect VSTS to your Azure container registry and Azure Container Service cluster</span></span>

<span data-ttu-id="44dec-154">CI/CD ardışık düzenine alma önce son Azure'da kapsayıcı kaydınız ve Docker Swarm kümesi dış bağlantıları yapılandırmak için adımlardır.</span><span class="sxs-lookup"><span data-stu-id="44dec-154">The last steps before getting into the CI/CD pipeline are to configure external connections to your container registry and your Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="44dec-155">İçinde **Hizmetleri** Visual Studio Team Services projenizin ayarları ekleme Hizmeti uç noktası türü **Docker kayıt defteri**.</span><span class="sxs-lookup"><span data-stu-id="44dec-155">In the **Services** settings of your Visual Studio Team Services project, add a service endpoint of type **Docker Registry**.</span></span> 

2. <span data-ttu-id="44dec-156">Açılır açılan penceresinde, URL ve Azure kapsayıcı kaydınız kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="44dec-156">In the popup that opens, enter the URL and the credentials of your Azure container registry.</span></span>

    ![Visual Studio Team Services - Docker kayıt defteri](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. <span data-ttu-id="44dec-158">Docker Swarm kümesi için bir uç nokta türü ekleme **SSH**.</span><span class="sxs-lookup"><span data-stu-id="44dec-158">For the Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="44dec-159">Ardından Swarm kümenizin SSH bağlantı bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="44dec-159">Then enter the SSH connection information of your Swarm cluster.</span></span>

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

<span data-ttu-id="44dec-161">Tüm yapılandırma şimdi yapılır.</span><span class="sxs-lookup"><span data-stu-id="44dec-161">All the configuration is done now.</span></span> <span data-ttu-id="44dec-162">Sonraki adımda oluşturan ve Docker Swarm kümesi uygulamaya dağıtır CI/CD ardışık düzen oluşturun.</span><span class="sxs-lookup"><span data-stu-id="44dec-162">In the next steps, you create the CI/CD pipeline that builds and deploys the application to the Docker Swarm cluster.</span></span> 

## <a name="step-2-create-the-build-definition"></a><span data-ttu-id="44dec-163">2. adım: derleme tanımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="44dec-163">Step 2: Create the build definition</span></span>

<span data-ttu-id="44dec-164">Bu adımda, bir yapı definitionfor VSTS projenizi ayarlayın ve yapı iş akışı için kapsayıcı görüntülerinizi tanımlayın</span><span class="sxs-lookup"><span data-stu-id="44dec-164">In this step, you set up a build definitionfor your VSTS project and define the build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="44dec-165">Başlangıç tanım Kurulumu</span><span class="sxs-lookup"><span data-stu-id="44dec-165">Initial definition setup</span></span>

1. <span data-ttu-id="44dec-166">Yapı tanımı oluşturmak için Visual Studio Team Services projenize bağlanmak ve **yapı & yayın**.</span><span class="sxs-lookup"><span data-stu-id="44dec-166">To create a build definition, connect to your Visual Studio Team Services project and click **Build & Release**.</span></span> 

2. <span data-ttu-id="44dec-167">İçinde **yapı tanımları** 'yi tıklatın **+ yeni**.</span><span class="sxs-lookup"><span data-stu-id="44dec-167">In the **Build definitions** section, click **+ New**.</span></span> <span data-ttu-id="44dec-168">Seçin **boş** şablonu.</span><span class="sxs-lookup"><span data-stu-id="44dec-168">Select the **Empty** template.</span></span>

    ![Visual Studio Team Services - yeni yapı tanımı](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. <span data-ttu-id="44dec-170">GitHub depo ile kaynak denetimi yeni bir yapı yapılandırma **sürekli tümleştirme**ve Linux Aracısı kayıtlı olduğu Aracısı kuyruğu seçin.</span><span class="sxs-lookup"><span data-stu-id="44dec-170">Configure the new build with a GitHub repository source, check **Continuous integration**, and select the agent queue where you registered your Linux agent.</span></span> <span data-ttu-id="44dec-171">Tıklatın **oluşturma** derleme tanımı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="44dec-171">Click **Create** to create the build definition.</span></span>

    ![Visual Studio Team Services - derleme tanımı oluştur](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. <span data-ttu-id="44dec-173">Üzerinde **yapı tanımlarını** sayfasında, ilk açmak **depo** sekmesinde ve önkoşullar oluşturulan MyShop proje çatalı kullanmak için yapıyı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="44dec-173">On the **Build Definitions** page, first open the **Repository** tab and configure the build to use the fork of the MyShop project that you created in the prerequisites.</span></span> <span data-ttu-id="44dec-174">Seçtiğinizden emin olun *acs belgeleri* olarak **varsayılan dalı**.</span><span class="sxs-lookup"><span data-stu-id="44dec-174">Make sure that you select *acs-docs* as the **Default branch**.</span></span>

    ![Visual Studio Team Services - derleme deposu yapılandırma](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. <span data-ttu-id="44dec-176">Üzerinde **Tetikleyicileri** sekmesinde, her yürütme tetiklenmesi için yapıyı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="44dec-176">On the **Triggers** tab, configure the build to be triggered after each commit.</span></span> <span data-ttu-id="44dec-177">Seçin **sürekli tümleştirme** ve **toplu değişiklikleri**.</span><span class="sxs-lookup"><span data-stu-id="44dec-177">Select **Continuous integration** and **Batch changes**.</span></span>

    ![Visual Studio Team Services - derleme tetikleyici yapılandırması](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-the-build-workflow"></a><span data-ttu-id="44dec-179">Yapı iş akışı tanımlayın</span><span class="sxs-lookup"><span data-stu-id="44dec-179">Define the build workflow</span></span>
<span data-ttu-id="44dec-180">Sonraki adımlar yapı iş akışı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="44dec-180">The next steps define the build workflow.</span></span> <span data-ttu-id="44dec-181">Beş kapsayıcı görüntülerini oluşturmak için *MyShop* uygulama.</span><span class="sxs-lookup"><span data-stu-id="44dec-181">There are five container images to build for the *MyShop* application.</span></span> <span data-ttu-id="44dec-182">Her görüntü proje klasörleri'nde bulunan Dockerfile kullanılarak oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="44dec-182">Each image is built using the Dockerfile located in the project folders:</span></span>

* <span data-ttu-id="44dec-183">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="44dec-183">ProductsApi</span></span>
* <span data-ttu-id="44dec-184">Ara sunucu</span><span class="sxs-lookup"><span data-stu-id="44dec-184">Proxy</span></span>
* <span data-ttu-id="44dec-185">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="44dec-185">RatingsApi</span></span>
* <span data-ttu-id="44dec-186">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="44dec-186">RecommandationsApi</span></span>
* <span data-ttu-id="44dec-187">ShopFront</span><span class="sxs-lookup"><span data-stu-id="44dec-187">ShopFront</span></span>

<span data-ttu-id="44dec-188">Her görüntü, görüntü oluşturmak için diğeri Azure kapsayıcı kayıt defterinde Görüntü göndermeyi için iki Docker adımı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="44dec-188">You need to add two Docker steps for each image, one to build the image, and one to push the image in the Azure container registry.</span></span> 

1. <span data-ttu-id="44dec-189">Yapı iş akışında bir adım eklemek için tıklatın **+ Ekle derleme adımı** seçip **Docker**.</span><span class="sxs-lookup"><span data-stu-id="44dec-189">To add a step in the build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services - eklemek derleme adımları](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. <span data-ttu-id="44dec-191">Her görüntü için kullandığı bir adım yapılandırma `docker build` komutu.</span><span class="sxs-lookup"><span data-stu-id="44dec-191">For each image, configure one step that uses the `docker build` command.</span></span>

    ![Visual Studio Team Services - Docker derleme](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    <span data-ttu-id="44dec-193">Derleme işlemi için Azure kapsayıcı kayıt defteri seçin **görüntü yapı** eylem ve her görüntü tanımlar Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="44dec-193">For the build operation, select your Azure container registry, the **Build an image** action, and the Dockerfile that defines each image.</span></span> <span data-ttu-id="44dec-194">Ayarlama **yapı bağlam** Dockerfile kök dizini ve tanımlayın **görüntü adı**.</span><span class="sxs-lookup"><span data-stu-id="44dec-194">Set the **Build context** as the Dockerfile root directory, and define the **Image Name**.</span></span> 
    
    <span data-ttu-id="44dec-195">Önceki ekranda gösterildiği gibi görüntü adı Azure kapsayıcı kaydınız URI ile başlatın.</span><span class="sxs-lookup"><span data-stu-id="44dec-195">As shown on the preceding screen, start the image name with the URI of your Azure container registry.</span></span> <span data-ttu-id="44dec-196">(Ayrıca bir yapı değişkeni Bu örnekte derleme tanımlayıcı gibi görüntü etiketi Parametreleştirme için kullanabileceğiniz.)</span><span class="sxs-lookup"><span data-stu-id="44dec-196">(You can also use a build variable to parameterize the tag of the image, such as the build identifier in this example.)</span></span>

3. <span data-ttu-id="44dec-197">Her görüntü için kullanır ikinci bir adım yapılandırma `docker push` komutu.</span><span class="sxs-lookup"><span data-stu-id="44dec-197">For each image, configure a second step that uses the `docker push` command.</span></span>

    ![Visual Studio Team Services - Docker gönderme](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    <span data-ttu-id="44dec-199">Gönderme işlemi için Azure kapsayıcı kayıt defteri seçin **görüntü anında** eylemi ve girin **görüntü adı** önceki adımda oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="44dec-199">For the push operation, select your Azure container registry, the **Push an image** action, and enter the **Image Name** that is built in the previous step.</span></span>

4. <span data-ttu-id="44dec-200">Derleme ve anında iletme adımları her beş görüntüleri için yapılandırdıktan sonra iki daha fazla adım yapı iş akışında ekleyin.</span><span class="sxs-lookup"><span data-stu-id="44dec-200">After you configure the build and push steps for each of the five images, add two more steps in the build workflow.</span></span>

    <span data-ttu-id="44dec-201">a.</span><span class="sxs-lookup"><span data-stu-id="44dec-201">a.</span></span> <span data-ttu-id="44dec-202">Değiştirmek için bir bash komut dosyası kullanan bir komut satırı görevi *BuildNumber* docker-compose.yml dosyası geçerli yineleme derleme kimliği Ayrıntılar için aşağıdaki ekran görüntüsüne bakın.</span><span class="sxs-lookup"><span data-stu-id="44dec-202">A command-line task that uses a bash script to replace the *BuildNumber* occurrence in the docker-compose.yml file with the current build Id. See the following screen for details.</span></span>

    ![Visual Studio Team Services - güncelleştirme oluşturma dosya](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    <span data-ttu-id="44dec-204">b.</span><span class="sxs-lookup"><span data-stu-id="44dec-204">b.</span></span> <span data-ttu-id="44dec-205">Bu sürümde kullanılabilir, böylece güncelleştirilmiş Oluştur dosya derleme yapısı olarak bırakır bir görev.</span><span class="sxs-lookup"><span data-stu-id="44dec-205">A task that drops the updated Compose file as a build artifact so it can be used in the release.</span></span> <span data-ttu-id="44dec-206">Ayrıntılar için aşağıdaki ekran görüntüsüne bakın.</span><span class="sxs-lookup"><span data-stu-id="44dec-206">See the following screen for details.</span></span>

    ![Visual Studio Team Services - Oluştur yayımlama dosyası](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. <span data-ttu-id="44dec-208">Tıklatın **kaydetmek** ve yapı tanımının adı.</span><span class="sxs-lookup"><span data-stu-id="44dec-208">Click **Save** and name your build definition.</span></span>

## <a name="step-3-create-the-release-definition"></a><span data-ttu-id="44dec-209">3. adım: sürüm tanımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="44dec-209">Step 3: Create the release definition</span></span>

<span data-ttu-id="44dec-210">Visual Studio Team Services olanak tanır [sürümleri arasında ortamlarını](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="44dec-210">Visual Studio Team Services allows you to [manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="44dec-211">Kesintisiz bir şekilde uygulamanız farklı ortamınızı (örneğin, geliştirme, test, ön üretim ve üretim) üzerinde dağıtıldığından emin olmak sürekli dağıtım etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44dec-211">You can enable continuous deployment to make sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="44dec-212">Azure kapsayıcı hizmeti Docker Swarm kümesi temsil eden yeni bir ortam oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44dec-212">You can create a new environment that represents your Azure Container Service Docker Swarm cluster.</span></span>

![Visual Studio Team Services - ACS sürüme](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="44dec-214">Kurulum ilk sürüm</span><span class="sxs-lookup"><span data-stu-id="44dec-214">Initial release setup</span></span>

1. <span data-ttu-id="44dec-215">Bir yayın tanımı oluşturmak için tıklatın **sürümleri** > **+ sürüm**</span><span class="sxs-lookup"><span data-stu-id="44dec-215">To create a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="44dec-216">Yapı kaynağını yapılandırmak için tıklatın **yapıları** > **bir yapı kaynak bağlantı**.</span><span class="sxs-lookup"><span data-stu-id="44dec-216">To configure the artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="44dec-217">Burada, bu yeni sürüm tanımı önceki adımda tanımlanan yapı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="44dec-217">Here, link this new release definition to the build that you defined in the previous step.</span></span> <span data-ttu-id="44dec-218">Bunu yaparak, docker-compose.yml dosyası yayın işlemde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="44dec-218">By doing this, the docker-compose.yml file is available in the release process.</span></span>

    ![Visual Studio Team Services - sürüm yapıları](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. <span data-ttu-id="44dec-220">Yayın tetikleyici yapılandırmak için tıklatın **Tetikleyicileri** seçip **sürekli dağıtım**.</span><span class="sxs-lookup"><span data-stu-id="44dec-220">To configure the release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="44dec-221">Tetikleyici aynı yapı kaynağında ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="44dec-221">Set the trigger on the same artifact source.</span></span> <span data-ttu-id="44dec-222">Bu ayar, yapı başarıyla tamamlanır tamamlanmaz yeni bir sürüm başlayacağını sağlar.</span><span class="sxs-lookup"><span data-stu-id="44dec-222">This setting ensures that a new release starts as soon as the build completes successfully.</span></span>

    ![Visual Studio Team Services - sürüm Tetikleyicileri](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-the-release-workflow"></a><span data-ttu-id="44dec-224">Yayın iş akışı tanımlama</span><span class="sxs-lookup"><span data-stu-id="44dec-224">Define the release workflow</span></span>

<span data-ttu-id="44dec-225">Yayın iş akışı eklediğiniz iki görevlerin oluşur.</span><span class="sxs-lookup"><span data-stu-id="44dec-225">The release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="44dec-226">Güvenli bir şekilde Oluştur dosyasına kopyalamak için bir görevi yapılandırmaya bir *dağıtmak* daha önce yapılandırdığınız SSH bağlantısını kullanarak Docker Swarm ana düğümde, klasör.</span><span class="sxs-lookup"><span data-stu-id="44dec-226">Configure a task to securely copy the compose file to a *deploy* folder on the Docker Swarm master node, using the SSH connection you configured previously.</span></span> <span data-ttu-id="44dec-227">Ayrıntılar için aşağıdaki ekran görüntüsüne bakın.</span><span class="sxs-lookup"><span data-stu-id="44dec-227">See the following screen for details.</span></span>

    ![Visual Studio Team Services - sürüm SCP](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. <span data-ttu-id="44dec-229">Çalıştırılacak bash komutu yürütmek için ikinci bir görevi yapılandırmaya `docker` ve `docker-compose` ana düğümde komutları.</span><span class="sxs-lookup"><span data-stu-id="44dec-229">Configure a second task to execute a bash command to run `docker` and `docker-compose` commands on the master node.</span></span> <span data-ttu-id="44dec-230">Ayrıntılar için aşağıdaki ekran görüntüsüne bakın.</span><span class="sxs-lookup"><span data-stu-id="44dec-230">See the following screen for details.</span></span>

    ![Visual Studio Team Services - sürüm Bash](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    <span data-ttu-id="44dec-232">Komutu, Docker CLI ve Docker Compose CLI aşağıdaki görevleri gerçekleştirmek için ana kullanımda yürütülebilir:</span><span class="sxs-lookup"><span data-stu-id="44dec-232">The command executed on the master use the Docker CLI and the Docker-Compose CLI to do the following tasks:</span></span>

    - <span data-ttu-id="44dec-233">Azure kapsayıcı kayıt defterine oturum açma (tanımlanan üç yapı variab'les kullanan **değişkenleri** sekmesinde)</span><span class="sxs-lookup"><span data-stu-id="44dec-233">Login to the Azure container registry (it uses three build variab\`les that are defined in the **Variables** tab)</span></span>
    - <span data-ttu-id="44dec-234">Tanımlamak **DOCKER_HOST** Swarm uç noktalarına ile çalışmak için değişken (: 2375)</span><span class="sxs-lookup"><span data-stu-id="44dec-234">Define the **DOCKER_HOST** variable to work with the Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="44dec-235">Gidin *dağıtmak* önceki güvenli kopyalama görevi tarafından oluşturulan ve docker-compose.yml dosyası içeren klasör</span><span class="sxs-lookup"><span data-stu-id="44dec-235">Navigate to the *deploy* folder that was created by the preceding secure copy task and that contains the docker-compose.yml file</span></span> 
    - <span data-ttu-id="44dec-236">Yürütme `docker-compose` yeni görüntüleri pull komutlarını hizmetleri durdurun, olan hizmetleri kaldırın ve kapsayıcıları oluşturma.</span><span class="sxs-lookup"><span data-stu-id="44dec-236">Execute `docker-compose` commands that pull the new images, stop the services, remove the services, and create the containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="44dec-237">Önceki ekranda gösterildiği gibi bırakın **STDERR üzerinde başarısız** onay kutusu işaretli.</span><span class="sxs-lookup"><span data-stu-id="44dec-237">As shown on the preceding screen, leave the **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="44dec-238">Bunun nedeni bir önemli ayarı, `docker-compose` durdurma veya standart hata çıktı siliniyor kapsayıcılardır gibi birkaç tanılama iletilerini yazdırır.</span><span class="sxs-lookup"><span data-stu-id="44dec-238">This is an important setting, because `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on the standard error output.</span></span> <span data-ttu-id="44dec-239">Onay kutusunu işaretlerseniz, tüm aşsa bile iyi Visual Studio Team Services hataları yayın sırasında oluştuğunu bildiriyor.</span><span class="sxs-lookup"><span data-stu-id="44dec-239">If you check the checkbox, Visual Studio Team Services reports that errors occurred during the release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="44dec-240">Bu yeni sürüm tanımını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="44dec-240">Save this new release definition.</span></span>


>[!NOTE]
><span data-ttu-id="44dec-241">Biz eski hizmetleri durdurma ve yeni bir çalışan olduğundan bu dağıtım miktar kapalı kalma süresi içerir.</span><span class="sxs-lookup"><span data-stu-id="44dec-241">This deployment includes some downtime because we are stopping the old services and running the new one.</span></span> <span data-ttu-id="44dec-242">Mavi yeşil dağıtım yaparak bu durumu önlemek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="44dec-242">It is possible to avoid this by doing a blue-green deployment.</span></span>
>

## <a name="step-4-test-the-cicd-pipeline"></a><span data-ttu-id="44dec-243">4. Adım.</span><span class="sxs-lookup"><span data-stu-id="44dec-243">Step 4.</span></span> <span data-ttu-id="44dec-244">CI/CD ardışık düzen test</span><span class="sxs-lookup"><span data-stu-id="44dec-244">Test the CI/CD pipeline</span></span>

<span data-ttu-id="44dec-245">Yapılandırma ile yapılır, bu yeni CI/CD ardışık düzen test zamanı geldi.</span><span class="sxs-lookup"><span data-stu-id="44dec-245">Now that you are done with the configuration, it's time to test this new CI/CD pipeline.</span></span> <span data-ttu-id="44dec-246">Test etmek için kolay kaynak kodunu güncelleştirin ve GitHub deponuz içine değişiklikleri yoludur.</span><span class="sxs-lookup"><span data-stu-id="44dec-246">The easiest way to test it is to update the source code and commit the changes into your GitHub repository.</span></span> <span data-ttu-id="44dec-247">Birkaç saniye kod itme sonra Visual Studio Team Services içinde çalışan yeni bir derleme görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="44dec-247">A few seconds after you push the code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="44dec-248">Başarıyla tamamlandığında, yeni bir sürüm tetiklenir ve Azure kapsayıcı hizmeti kümesi uygulamanın yeni sürümünü dağıtır.</span><span class="sxs-lookup"><span data-stu-id="44dec-248">Once completed successfully, a new release will be triggered and will deploy the new version of the application on the Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44dec-249">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="44dec-249">Next Steps</span></span>

* <span data-ttu-id="44dec-250">CI/CD Visual Studio Team Services ile ilgili daha fazla bilgi için bkz: [VSTS derleme genel bakış](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="44dec-250">For more information about CI/CD with Visual Studio Team Services, see the [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
