---
title: "aaaDeploy kapsayıcı tooAzure Service Fabric, bir .NET uygulamasında | Microsoft Docs"
description: "Nasıl öğretilmektedir toopackage Docker kapsayıcısı içinde Visual Studio'da .NET uygulaması. Bu yeni \"kapsayıcı\" uygulama sonra dağıtılan tooa Service Fabric kümesi."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: mikhegn
ms.openlocfilehash: 094b0e71d76b2e56ffb9b23638dd8154b3aff5fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a><span data-ttu-id="83354-104">Bir Windows kapsayıcı tooAzure Service Fabric bir .NET uygulamasında dağıtma</span><span class="sxs-lookup"><span data-stu-id="83354-104">Deploy a .NET application in a Windows container tooAzure Service Fabric</span></span>

<span data-ttu-id="83354-105">Bu öğretici şunların nasıl yapıldığını gösterir toodeploy Azure üzerinde bir Windows kapsayıcıda mevcut bir ASP.NET uygulamasını.</span><span class="sxs-lookup"><span data-stu-id="83354-105">This tutorial shows you how toodeploy an existing ASP.NET application in a Windows container on Azure.</span></span>

<span data-ttu-id="83354-106">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="83354-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="83354-107">Visual Studio'da bir Docker projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="83354-107">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="83354-108">Varolan bir uygulama containerize</span><span class="sxs-lookup"><span data-stu-id="83354-108">Containerize an existing application</span></span>
> * <span data-ttu-id="83354-109">Visual Studio ve VSTS sürekli tümleştirme Kurulumu</span><span class="sxs-lookup"><span data-stu-id="83354-109">Setup continuous integration with Visual Studio and VSTS</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83354-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="83354-110">Prerequisites</span></span>

1. <span data-ttu-id="83354-111">Yükleme [Docker Windows CE](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) kapsayıcıları üzerinde Windows 10 çalıştırabilmeniz için.</span><span class="sxs-lookup"><span data-stu-id="83354-111">Install [Docker CE for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) so that you can run containers on Windows 10.</span></span>
2. <span data-ttu-id="83354-112">Merhaba ile öğrenmeniz [Windows 10 kapsayıcıları quickstart][link-container-quickstart].</span><span class="sxs-lookup"><span data-stu-id="83354-112">Familiarize yourself with hello [Windows 10 Containers quickstart][link-container-quickstart].</span></span>
3. <span data-ttu-id="83354-113">Merhaba karşıdan [Fabrikam Fiber CallCenter] [ link-fabrikam-github] örnek uygulama.</span><span class="sxs-lookup"><span data-stu-id="83354-113">Download hello [Fabrikam Fiber CallCenter][link-fabrikam-github] sample application.</span></span>
4. <span data-ttu-id="83354-114">Yükleme [Azure PowerShell][link-azure-powershell-install]</span><span class="sxs-lookup"><span data-stu-id="83354-114">Install [Azure PowerShell][link-azure-powershell-install]</span></span>
5. <span data-ttu-id="83354-115">Merhaba yüklemek [Visual Studio 2017 için sürekli teslim araçları uzantısı][link-visualstudio-cd-extension]</span><span class="sxs-lookup"><span data-stu-id="83354-115">Install hello [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension]</span></span>
6. <span data-ttu-id="83354-116">Oluşturma bir [Azure aboneliği] [ link-azure-subscription] ve [Visual Studio Team Services hesabı][link-vsts-account].</span><span class="sxs-lookup"><span data-stu-id="83354-116">Create an [Azure subscription][link-azure-subscription] and a [Visual Studio Team Services account][link-vsts-account].</span></span> 
7. [<span data-ttu-id="83354-117">Azure üzerinde bir küme oluşturun</span><span class="sxs-lookup"><span data-stu-id="83354-117">Create a cluster on Azure</span></span>](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-hello-application"></a><span data-ttu-id="83354-118">Merhaba uygulaması containerize</span><span class="sxs-lookup"><span data-stu-id="83354-118">Containerize hello application</span></span>

<span data-ttu-id="83354-119">Sahip olduğunuza göre bir [Service Fabric kümesi Azure'da çalışan](service-fabric-tutorial-create-cluster-azure-ps.md) hazır toocreate olan ve kapsayıcılı uygulamayı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="83354-119">Now that you have a [Service Fabric cluster is running in Azure](service-fabric-tutorial-create-cluster-azure-ps.md) you are ready toocreate and deploy a containerized application.</span></span> <span data-ttu-id="83354-120">uygulamamız bir kapsayıcıda çalışan toostart tooadd ihtiyacımız **Docker Destek** Visual Studio'da toohello projesi.</span><span class="sxs-lookup"><span data-stu-id="83354-120">toostart running our application in a container, we need tooadd **Docker Support** toohello project in Visual Studio.</span></span> <span data-ttu-id="83354-121">Eklediğinizde **Docker Destek** iki şey toohello uygulama olur.</span><span class="sxs-lookup"><span data-stu-id="83354-121">When you add **Docker support** toohello application, two things happen.</span></span> <span data-ttu-id="83354-122">İlk olarak, bir _Dockerfile_ toohello projesi eklenir.</span><span class="sxs-lookup"><span data-stu-id="83354-122">First, a _Dockerfile_ is added toohello project.</span></span> <span data-ttu-id="83354-123">Bu yeni dosya nasıl hello kapsayıcı görüntü yerleşik toobe açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="83354-123">This new file describes how hello container image is toobe built.</span></span> <span data-ttu-id="83354-124">Ardından ikinci, yeni bir _docker compose'u_ proje toohello çözüm eklenir.</span><span class="sxs-lookup"><span data-stu-id="83354-124">Then second, a new _docker-compose_ project is added toohello solution.</span></span> <span data-ttu-id="83354-125">Merhaba yeni proje içeren birkaç dosyaları docker compose'u.</span><span class="sxs-lookup"><span data-stu-id="83354-125">hello new project contains a few docker-compose files.</span></span> <span data-ttu-id="83354-126">Docker compose'u dosyaları hello kapsayıcı nasıl yürütüleceğini kullanılan toodescribe olabilir.</span><span class="sxs-lookup"><span data-stu-id="83354-126">Docker-compose files can be used toodescribe how hello container is run.</span></span>

<span data-ttu-id="83354-127">İle çalışma hakkında daha fazla bilgi [Visual Studio kapsayıcı Araçları][link-visualstudio-container-tools].</span><span class="sxs-lookup"><span data-stu-id="83354-127">More info on working with [Visual Studio Container Tools][link-visualstudio-container-tools].</span></span>

>[!NOTE]
><span data-ttu-id="83354-128">Bu hello Windows kapsayıcı görüntülerini bilgisayarınızda çalıştırdığınız ilk kez kullanıyorsanız, Docker CE hello temel görüntüler, kapsayıcıları için aşağı çekmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="83354-128">If it is hello first time you are running Windows container images on your computer, Docker CE must pull down hello base images for your containers.</span></span> <span data-ttu-id="83354-129">Bu öğreticide kullanılan hello görüntüleri 14 GB bağımsızdır.</span><span class="sxs-lookup"><span data-stu-id="83354-129">hello images used in this tutorial are 14 GB.</span></span> <span data-ttu-id="83354-130">Bir tane terminal komutu toopull hello taban görüntüleri aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="83354-130">Go ahead and run hello following terminal command toopull hello base images:</span></span>
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a><span data-ttu-id="83354-131">Docker desteği ekleme</span><span class="sxs-lookup"><span data-stu-id="83354-131">Add Docker support</span></span>

<span data-ttu-id="83354-132">Açık hello [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] dosyasını Visual Studio'da.</span><span class="sxs-lookup"><span data-stu-id="83354-132">Open hello [FabrikamFiber.CallCenter.sln][link-fabrikam-github] file in Visual Studio.</span></span>

<span data-ttu-id="83354-133">Sağ hello **FabrikamFiber.Web** Proje > **Ekle** > **Docker Destek**.</span><span class="sxs-lookup"><span data-stu-id="83354-133">Right-click hello **FabrikamFiber.Web** project > **Add** > **Docker Support**.</span></span>

### <a name="add-support-for-sql"></a><span data-ttu-id="83354-134">SQL desteği ekleme</span><span class="sxs-lookup"><span data-stu-id="83354-134">Add support for SQL</span></span>

<span data-ttu-id="83354-135">Bir SQL server gerekli toorun Merhaba uygulaması olacak şekilde bu uygulama SQL hello veri sağlayıcısı olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="83354-135">This application uses SQL as hello data provider, so a SQL server is required toorun hello application.</span></span> <span data-ttu-id="83354-136">Bizim docker compose.override.yml dosyasındaki bir SQL Server kapsayıcı yansıma başvuru.</span><span class="sxs-lookup"><span data-stu-id="83354-136">Reference a SQL Server container image in our docker-compose.override.yml file.</span></span>

<span data-ttu-id="83354-137">Visual Studio'da açın **Çözüm Gezgini**, bulma **docker compose'u**ve açık hello dosya **docker compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="83354-137">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open hello file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="83354-138">Toohello gidin `services:` düğümü, adlandırılmış bir düğüm eklemek `db:` hello SQL Server girişi hello kapsayıcısı için tanımlar.</span><span class="sxs-lookup"><span data-stu-id="83354-138">Navigate toohello `services:` node, add a node named `db:` that defines hello SQL Server entry for hello container.</span></span>

```yml
  db:
    image: microsoft/mssql-server-windows-developer
    environment:
      sa_password: "Password1"
      ACCEPT_EULA: "Y"
    ports:
      - "1433"
    healthcheck:
      test: [ "CMD", "sqlcmd", "-U", "sa", "-P", "Password1", "-Q", "select 1" ]
      interval: 1s
      retries: 20
```

>[!NOTE]
><span data-ttu-id="83354-139">Ana bilgisayardan erişilebilir olduğu müddetçe, yerel hata ayıklama için tercih ettiğiniz herhangi bir SQL sunucusu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83354-139">You can use any SQL Server you prefer for local debugging, as long as it is reachable from your host.</span></span> <span data-ttu-id="83354-140">Ancak, **localdb** desteklemediği `container -> host` iletişim.</span><span class="sxs-lookup"><span data-stu-id="83354-140">However, **localdb** does not support `container -> host` communication.</span></span>

>[!WARNING]
><span data-ttu-id="83354-141">SQL Server çalıştıran bir kapsayıcıda kalıcı veri desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="83354-141">Running SQL Server in a container does not support persisting data.</span></span> <span data-ttu-id="83354-142">Merhaba kapsayıcı sona erdiğinde, verileriniz silinir.</span><span class="sxs-lookup"><span data-stu-id="83354-142">When hello container stops, your data is erased.</span></span> <span data-ttu-id="83354-143">Bu yapılandırma, üretim için kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="83354-143">Do not use this configuration for production.</span></span>

<span data-ttu-id="83354-144">Toohello gidin `fabrikamfiber.web:` düğümü ve adlı bir alt düğüm eklemek `depends_on:`.</span><span class="sxs-lookup"><span data-stu-id="83354-144">Navigate toohello `fabrikamfiber.web:` node and add a child node named `depends_on:`.</span></span> <span data-ttu-id="83354-145">Bu, hello sağlar `db` hizmetini (Merhaba SQL Server kapsayıcısı) web uygulamamız önce (fabrikamfiber.web) başlatır.</span><span class="sxs-lookup"><span data-stu-id="83354-145">This ensures that hello `db` service (hello SQL Server container) starts before our web application (fabrikamfiber.web).</span></span>

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a><span data-ttu-id="83354-146">Merhaba web yapılandırma güncelleştir</span><span class="sxs-lookup"><span data-stu-id="83354-146">Update hello web config</span></span>

<span data-ttu-id="83354-147">Merhaba edilene **FabrikamFiber.Web** proje, güncelleştirme hello bağlantı dizesine hello **web.config** dosya, SQL Server hello kapsayıcısında toopoint toohello.</span><span class="sxs-lookup"><span data-stu-id="83354-147">Back in hello **FabrikamFiber.Web** project, update hello connection string in hello **web.config** file, toopoint toohello SQL Server in hello container.</span></span>

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
><span data-ttu-id="83354-148">Bir yayın oluştururken farklı SQL Server web uygulamanızın veya yapı toouse istiyorsanız, başka bir bağlantı dizesi tooyour web.release.config dosyası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="83354-148">If you want toouse a different SQL Server when building a release build of your web application, add another connection string tooyour web.release.config file.</span></span>

### <a name="test-your-container"></a><span data-ttu-id="83354-149">Test, kapsayıcısı</span><span class="sxs-lookup"><span data-stu-id="83354-149">Test your container</span></span>

<span data-ttu-id="83354-150">Tuşuna **F5** , kapsayıcı toorun ve hata ayıklama hello uygulamada.</span><span class="sxs-lookup"><span data-stu-id="83354-150">Press **F5** toorun and debug hello application in your container.</span></span>

<span data-ttu-id="83354-151">Kenar başlangıç IP adresi hello kapsayıcısının hello iç NAT ağda (genellikle 172.x.x.x) kullanan uygulamanızın tanımlanmış başlatma sayfasını açar.</span><span class="sxs-lookup"><span data-stu-id="83354-151">Edge opens your application's defined launch page using hello IP address of hello container on hello internal NAT network (typically 172.x.x.x).</span></span> <span data-ttu-id="83354-152">Visual Studio 2017 kullanarak kapsayıcıları uygulamalarında hata ayıklama hakkında daha fazla toolearn bkz [bu makalede][link-debug-container].</span><span class="sxs-lookup"><span data-stu-id="83354-152">toolearn more about debugging applications in containers using Visual Studio 2017, see [this article][link-debug-container].</span></span>

![bir kapsayıcıda fabrikam örneği][image-web-preview]

<span data-ttu-id="83354-154">Merhaba kapsayıcı oluşturulur ve bir Service Fabric uygulaması paketlenmiş hazır toobe sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="83354-154">hello container is now ready toobe built and packaged in a Service Fabric application.</span></span> <span data-ttu-id="83354-155">Makinenizde yerleşik hello kapsayıcı görüntüsünü oluşturduktan sonra tooany kapsayıcı kayıt defteri itme ve tooany konak toorun çekmek.</span><span class="sxs-lookup"><span data-stu-id="83354-155">Once you have hello container image built on your machine, you can push it tooany container registry and pull it down tooany host toorun.</span></span>

## <a name="get-hello-application-ready-for-hello-cloud"></a><span data-ttu-id="83354-156">Merhaba uygulaması hello bulut için hazırlanma</span><span class="sxs-lookup"><span data-stu-id="83354-156">Get hello application ready for hello cloud</span></span>

<span data-ttu-id="83354-157">tooget Merhaba uygulaması Azure Service Fabric içinde çalıştırmak için hazır, toocomplete iki adım gerekir:</span><span class="sxs-lookup"><span data-stu-id="83354-157">tooget hello application ready for running in Service Fabric in Azure, we need toocomplete two steps:</span></span>

1. <span data-ttu-id="83354-158">Başlangıç bağlantı noktası toobe mümkün tooreach web uygulamamız hello Service Fabric kümesindeki burada istiyoruz kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="83354-158">Expose hello port where we want toobe able tooreach our web application in hello Service Fabric cluster.</span></span>
2. <span data-ttu-id="83354-159">Bir üretim hazır SQL veritabanı uygulamamız için sağlayın.</span><span class="sxs-lookup"><span data-stu-id="83354-159">Provide a production ready SQL database for our application.</span></span>

### <a name="expose-hello-port-for-hello-app"></a><span data-ttu-id="83354-160">Merhaba uygulama için başlangıç bağlantı noktası kullanıma sunma</span><span class="sxs-lookup"><span data-stu-id="83354-160">Expose hello port for hello app</span></span>
<span data-ttu-id="83354-161">Merhaba Service Fabric kümesi yapılandırılmış, bağlantı noktası olan *80* açık varsayılan olarak hello Azure yük dengeleyici, gelen trafiği toohello küme dengeler.</span><span class="sxs-lookup"><span data-stu-id="83354-161">hello Service Fabric cluster we have configured, has port *80* open by default in hello Azure Load Balancer, that balances incoming traffic toohello cluster.</span></span> <span data-ttu-id="83354-162">Biz bu bağlantı noktasında bizim kapsayıcı bizim docker-compose.yml dosyası getirebilir.</span><span class="sxs-lookup"><span data-stu-id="83354-162">We can expose our container on this port via our docker-compose.yml file.</span></span>

<span data-ttu-id="83354-163">Visual Studio'da açın **Çözüm Gezgini**, bulma **docker compose'u**ve açık hello dosya **docker compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="83354-163">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open hello file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="83354-164">Merhaba değiştirme `fabrikamfiber.web:` düğümü adlı bir alt düğüm eklemek `ports:`.</span><span class="sxs-lookup"><span data-stu-id="83354-164">Modify hello `fabrikamfiber.web:` node, add a child node named `ports:`.</span></span>

<span data-ttu-id="83354-165">Bir dize girişi ekleme `- "80:80"`.</span><span class="sxs-lookup"><span data-stu-id="83354-165">Add a string entry `- "80:80"`.</span></span>

```yml
  version: '3'

  services:
    fabrikamfiber.web:
      image: fabrikamfiber.web
      build:
        context: .\FabrikamFiber.Web
        dockerfile: Dockerfile
      ports:
        - "80:80"
```

### <a name="use-a-production-sql-database"></a><span data-ttu-id="83354-166">Bir üretim SQL veritabanını kullan</span><span class="sxs-lookup"><span data-stu-id="83354-166">Use a production SQL database</span></span>
<span data-ttu-id="83354-167">Üretimde çalıştırırken, verilerimizi ihtiyacımız bizim veritabanında kalıcı.</span><span class="sxs-lookup"><span data-stu-id="83354-167">When running in production, we need our data persisted in our database.</span></span> <span data-ttu-id="83354-168">Bir kapsayıcıda şu anda yolu tooguarantee kalıcı veri yok, bu nedenle bir kapsayıcıda SQL Server'daki üretim verileri depolanamıyor.</span><span class="sxs-lookup"><span data-stu-id="83354-168">There is currently no way tooguarantee persistent data in a container, therefore you cannot store production data in SQL Server in a container.</span></span>

<span data-ttu-id="83354-169">Bir Azure SQL veritabanı kullanan öneririz.</span><span class="sxs-lookup"><span data-stu-id="83354-169">We recommend you utilize an Azure SQL Database.</span></span> <span data-ttu-id="83354-170">tooset ayarlama ve çalıştırma Azure, yönetilen bir SQL Server'da ziyaret hello [Azure SQL veritabanı hızlı başlangıç ipuçları] [ link-azure-sql] makalesi.</span><span class="sxs-lookup"><span data-stu-id="83354-170">tooset up and run a managed SQL Server in Azure, visit hello [Azure SQL Database Quickstarts][link-azure-sql] article.</span></span>

>[!NOTE]
><span data-ttu-id="83354-171">Toochange hello bağlantı dizeleri toohello SQL Server'da hello unutmayın **web.release.config** hello dosyasında **FabrikamFiber.Web** projesi.</span><span class="sxs-lookup"><span data-stu-id="83354-171">Remember toochange hello connection strings toohello SQL server in hello **web.release.config** file in hello **FabrikamFiber.Web** project.</span></span>
>
><span data-ttu-id="83354-172">SQL veritabanı erişilebilir olduğundan, bu uygulama düzgün biçimde başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="83354-172">This application fails gracefully if no SQL database is reachable.</span></span> <span data-ttu-id="83354-173">Şimdi toogo seçin ve SQL server ile Merhaba uygulaması dağıtın.</span><span class="sxs-lookup"><span data-stu-id="83354-173">You can choose toogo ahead and deploy hello application with no SQL server.</span></span>

## <a name="deploy-with-visual-studio-team-services"></a><span data-ttu-id="83354-174">Visual Studio Team Services ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="83354-174">Deploy with Visual Studio Team Services</span></span>

<span data-ttu-id="83354-175">tooset Visual Studio Team Services kullanarak dağıtım, gereksinim duyduğunuz tooinstall hello [sürekli teslim araçları uzantısı için Visual Studio 2017][link-visualstudio-cd-extension].</span><span class="sxs-lookup"><span data-stu-id="83354-175">tooset up deployment using Visual Studio Team Services, you need tooinstall hello [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension].</span></span> <span data-ttu-id="83354-176">Bu uzantıyı Visual Studio Team Services yapılandırarak kolay toodeploy tooAzure kolaylaştırır ve dağıtılmış uygulama tooyour Service Fabric kümesi alın.</span><span class="sxs-lookup"><span data-stu-id="83354-176">This extension makes it easy toodeploy tooAzure by configuring Visual Studio Team Services and get your app deployed tooyour Service Fabric cluster.</span></span>

<span data-ttu-id="83354-177">başlatıldı, tooget kaynak denetiminde kodunuzun barındırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="83354-177">tooget started, your code must be hosted in source control.</span></span> <span data-ttu-id="83354-178">Bu bölümde Hello kalan varsayar **git** kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="83354-178">hello rest of this section assumes **git** is being used.</span></span>

### <a name="set-up-a-vsts-repo"></a><span data-ttu-id="83354-179">VSTS depodaki ayarlayın</span><span class="sxs-lookup"><span data-stu-id="83354-179">Set up a VSTS repo</span></span>
<span data-ttu-id="83354-180">Merhaba sağ alt köşesinde Visual Studio, tıklatın **tooSource denetim eklemek** > **Git** (veya hangi seçeneği tercih).</span><span class="sxs-lookup"><span data-stu-id="83354-180">At hello bottom-right corner of Visual Studio, click **Add tooSource Control** > **Git** (or whichever option you prefer).</span></span>

![Merhaba kaynak denetimi düğmesine basın][image-source-control]

<span data-ttu-id="83354-182">Merhaba, _Takım Gezgini_ bölmesi, basın **yayımlama Git deposuna**.</span><span class="sxs-lookup"><span data-stu-id="83354-182">In hello _Team Explorer_ pane, press **Publish Git Repo**.</span></span>

<span data-ttu-id="83354-183">VSTS havuz adı ve tuşuna seçin **depo**.</span><span class="sxs-lookup"><span data-stu-id="83354-183">Select your VSTS repository name and press **Repository**.</span></span>

![Depodaki tooVSTS yayımlama][image-publish-repo]

<span data-ttu-id="83354-185">Kodunuzu VSTS kaynak deposu ile eşitlenir, sürekli tümleştirme ve kesintisiz teslim yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83354-185">Now that your code is synchronized with a VSTS source repository, you can configure continuous integration and continuous delivery.</span></span>

### <a name="setup-continuous-delivery"></a><span data-ttu-id="83354-186">Kurulum kesintisiz teslim</span><span class="sxs-lookup"><span data-stu-id="83354-186">Setup continuous delivery</span></span>

<span data-ttu-id="83354-187">İçinde _Çözüm Gezgini_, sağ hello **çözüm** > **yapılandırma kesintisiz teslim**.</span><span class="sxs-lookup"><span data-stu-id="83354-187">In _Solution Explorer_, right-click hello **solution** > **Configure Continuous Delivery**.</span></span>

<span data-ttu-id="83354-188">Hello Azure aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="83354-188">Select hello Azure Subscription.</span></span>

<span data-ttu-id="83354-189">Ayarlama **ana bilgisayar türü** çok**Service Fabric kümesi**.</span><span class="sxs-lookup"><span data-stu-id="83354-189">Set **Host Type** too**Service Fabric Cluster**.</span></span>

<span data-ttu-id="83354-190">Ayarlama **hedef ana bilgisayarın** hello önceki bölümde oluşturduğunuz toohello service fabric kümesi.</span><span class="sxs-lookup"><span data-stu-id="83354-190">Set **Target Host** toohello service fabric cluster you created in hello previous section.</span></span>

<span data-ttu-id="83354-191">Seçin bir **kapsayıcı kayıt defteri** toopublish, kapsayıcıya.</span><span class="sxs-lookup"><span data-stu-id="83354-191">Choose a **Container Registry** toopublish your container to.</span></span>

>[!TIP]
><span data-ttu-id="83354-192">Kullanım hello **Düzenle** düğmesini toocreate bir kapsayıcı kayıt defteri.</span><span class="sxs-lookup"><span data-stu-id="83354-192">Use hello **Edit** button toocreate a container registry.</span></span>

<span data-ttu-id="83354-193">**Tamam**'a basın.</span><span class="sxs-lookup"><span data-stu-id="83354-193">Press **OK**.</span></span>

![Kurulum service fabric sürekli tümleştirme][image-setup-ci]
   
   <span data-ttu-id="83354-195">Merhaba Yapılandırma tamamlandıktan sonra dağıtılan tooService doku kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="83354-195">Once hello configuration is completed, your container is deployed tooService Fabric.</span></span> <span data-ttu-id="83354-196">Güncelleştirmeleri toohello depo itme her bir yeni derleme ve sürüm gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="83354-196">Whenever you push updates toohello repository a new build and release is executed.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="83354-197">Yapı hello kapsayıcı görüntüleri yaklaşık 15 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="83354-197">Building hello container images take approximately 15 minutes.</span></span>
   ><span data-ttu-id="83354-198">Merhaba ilk dağıtım toohello Service Fabric kümesi hello temel Windows Server Core kapsayıcı görüntüleri toobe indirilen neden olur.</span><span class="sxs-lookup"><span data-stu-id="83354-198">hello first deployment toohello Service Fabric cluster causes hello base Windows Server Core container images toobe downloaded.</span></span> <span data-ttu-id="83354-199">Merhaba indirme ek 5-10 dakika toocomplete alır.</span><span class="sxs-lookup"><span data-stu-id="83354-199">hello download takes additional 5-10 minutes toocomplete.</span></span>

<span data-ttu-id="83354-200">Kümenizin Hello URL'yi kullanarak toohello Fabrikam çağrı merkezi uygulama göz atın: Örneğin, *http://mycluster.westeurope.cloudapp.azure.com*</span><span class="sxs-lookup"><span data-stu-id="83354-200">Browse toohello Fabrikam Call Center application using hello url of your cluster: for example, *http://mycluster.westeurope.cloudapp.azure.com*</span></span>

<span data-ttu-id="83354-201">Kapsayıcılı ve hello Fabrikam çağrı merkezi çözümü dağıtılmış göre hello açabilirsiniz [Azure portal] [ link-azure-portal] ve Service Fabric çalışan hello uygulama bakın.</span><span class="sxs-lookup"><span data-stu-id="83354-201">Now that you have containerized and deployed hello Fabrikam Call Center solution, you can open hello [Azure portal][link-azure-portal] and see hello application running in Service Fabric.</span></span> <span data-ttu-id="83354-202">tootry Merhaba uygulaması, bir web tarayıcısı açın ve Service Fabric kümesi toohello URL'sini gidin.</span><span class="sxs-lookup"><span data-stu-id="83354-202">tootry hello application, open a web browser and go toohello URL of your Service Fabric cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83354-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="83354-203">Next steps</span></span>

<span data-ttu-id="83354-204">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="83354-204">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="83354-205">Visual Studio'da bir Docker projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="83354-205">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="83354-206">Varolan bir uygulama containerize</span><span class="sxs-lookup"><span data-stu-id="83354-206">Containerize an existing application</span></span>
> * <span data-ttu-id="83354-207">Visual Studio ve VSTS sürekli tümleştirme Kurulumu</span><span class="sxs-lookup"><span data-stu-id="83354-207">Setup continuous integration with Visual Studio and VSTS</span></span>

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooit.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate tooAzure Web Apps](app-service-web-tutorial-custom-ssl.md)

## Next steps

- [Container Tooling in Visual Studio][link-visualstudio-container-tools]
- [Get started with containers in Service Fabric][link-servicefabric-containers]
- [Creating Service Fabric applications][link-servicefabric-createapp]
-->

[link-debug-container]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-fabrikam-github]: https://aka.ms/fabrikamcontainer
[link-container-quickstart]: /virtualization/windowscontainers/quick-start/quick-start-windows-10
[link-visualstudio-container-tools]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-azure-powershell-install]: /powershell/azure/install-azurerm-ps
[link-servicefabric-create-secure-clusters]: service-fabric-cluster-creation-via-arm.md
[link-visualstudio-cd-extension]: https://aka.ms/cd4vs
[link-servicefabric-containers]: service-fabric-get-started-containers.md
[link-servicefabric-createapp]: service-fabric-create-your-first-application-in-visual-studio.md
[link-azure-portal]: https://portal.azure.com
[link-sf-clustertemplate]: https://aka.ms/securepreviewonelineclustertemplate
[link-azure-pricing-calculator]: https://azure.microsoft.com/en-us/pricing/calculator/
[link-azure-subscription]: https://azure.microsoft.com/en-us/free/
[link-vsts-account]: https://www.visualstudio.com/team-services/pricing/
[link-azure-sql]: /azure/sql-database/

[image-web-preview]: media/service-fabric-host-app-in-a-container/fabrikam-web-sample.png
[image-source-control]: media/service-fabric-host-app-in-a-container/add-to-source-control.png
[image-publish-repo]: media/service-fabric-host-app-in-a-container/publish-repo.png
[image-setup-ci]: media/service-fabric-host-app-in-a-container/configure-continuous-integration.png
