---
title: "Azure Service Fabric bir kapsayıcıda .NET uygulaması dağıtma | Microsoft Docs"
description: "Docker kapsayıcısı içinde Visual Studio'da .NET uygulaması paketlemek öğretir. Bu yeni \"kapsayıcı\" uygulaması, ardından bir Service Fabric kümesi dağıtılır."
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
ms.openlocfilehash: 484db494e7975df950543d19bf841a4df7cdd139
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-to-azure-service-fabric"></a><span data-ttu-id="18178-104">Azure Service Fabric Windows kapsayıcısında .NET uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="18178-104">Deploy a .NET application in a Windows container to Azure Service Fabric</span></span>

<span data-ttu-id="18178-105">Bu öğretici, Azure üzerinde bir Windows kapsayıcıda mevcut bir ASP.NET uygulamasını dağıtma gösterir.</span><span class="sxs-lookup"><span data-stu-id="18178-105">This tutorial shows you how to deploy an existing ASP.NET application in a Windows container on Azure.</span></span>

<span data-ttu-id="18178-106">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="18178-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="18178-107">Visual Studio'da bir Docker projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="18178-107">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="18178-108">Varolan bir uygulama containerize</span><span class="sxs-lookup"><span data-stu-id="18178-108">Containerize an existing application</span></span>
> * <span data-ttu-id="18178-109">Visual Studio ve VSTS sürekli tümleştirme Kurulumu</span><span class="sxs-lookup"><span data-stu-id="18178-109">Setup continuous integration with Visual Studio and VSTS</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18178-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="18178-110">Prerequisites</span></span>

1. <span data-ttu-id="18178-111">Yükleme [Docker Windows CE](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) kapsayıcıları üzerinde Windows 10 çalıştırabilmeniz için.</span><span class="sxs-lookup"><span data-stu-id="18178-111">Install [Docker CE for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) so that you can run containers on Windows 10.</span></span>
2. <span data-ttu-id="18178-112">İle öğrenmeniz [Windows 10 kapsayıcıları quickstart][link-container-quickstart].</span><span class="sxs-lookup"><span data-stu-id="18178-112">Familiarize yourself with the [Windows 10 Containers quickstart][link-container-quickstart].</span></span>
3. <span data-ttu-id="18178-113">Karşıdan [Fabrikam Fiber CallCenter] [ link-fabrikam-github] örnek uygulama.</span><span class="sxs-lookup"><span data-stu-id="18178-113">Download the [Fabrikam Fiber CallCenter][link-fabrikam-github] sample application.</span></span>
4. <span data-ttu-id="18178-114">Yükleme [Azure PowerShell][link-azure-powershell-install]</span><span class="sxs-lookup"><span data-stu-id="18178-114">Install [Azure PowerShell][link-azure-powershell-install]</span></span>
5. <span data-ttu-id="18178-115">Yükleme [Visual Studio 2017 için sürekli teslim araçları uzantısı][link-visualstudio-cd-extension]</span><span class="sxs-lookup"><span data-stu-id="18178-115">Install the [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension]</span></span>
6. <span data-ttu-id="18178-116">Oluşturma bir [Azure aboneliği] [ link-azure-subscription] ve [Visual Studio Team Services hesabı][link-vsts-account].</span><span class="sxs-lookup"><span data-stu-id="18178-116">Create an [Azure subscription][link-azure-subscription] and a [Visual Studio Team Services account][link-vsts-account].</span></span> 
7. [<span data-ttu-id="18178-117">Azure üzerinde bir küme oluşturun</span><span class="sxs-lookup"><span data-stu-id="18178-117">Create a cluster on Azure</span></span>](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-the-application"></a><span data-ttu-id="18178-118">Uygulama containerize</span><span class="sxs-lookup"><span data-stu-id="18178-118">Containerize the application</span></span>

<span data-ttu-id="18178-119">Sahip olduğunuza göre bir [Service Fabric kümesi Azure'da çalışan](service-fabric-tutorial-create-cluster-azure-ps.md) oluşturup kapsayıcılı uygulama dağıtmak hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="18178-119">Now that you have a [Service Fabric cluster is running in Azure](service-fabric-tutorial-create-cluster-azure-ps.md) you are ready to create and deploy a containerized application.</span></span> <span data-ttu-id="18178-120">Uygulamamız bir kapsayıcıda çalışan başlatmak için eklemek ihtiyacımız **Docker Destek** Visual Studio'da projeye.</span><span class="sxs-lookup"><span data-stu-id="18178-120">To start running our application in a container, we need to add **Docker Support** to the project in Visual Studio.</span></span> <span data-ttu-id="18178-121">Eklediğinizde **Docker Destek** uygulamaya iki şey olur.</span><span class="sxs-lookup"><span data-stu-id="18178-121">When you add **Docker support** to the application, two things happen.</span></span> <span data-ttu-id="18178-122">İlk olarak, bir _Dockerfile_ projeye eklenir.</span><span class="sxs-lookup"><span data-stu-id="18178-122">First, a _Dockerfile_ is added to the project.</span></span> <span data-ttu-id="18178-123">Bu yeni dosya nasıl kapsayıcı görüntünün oluşturulması açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="18178-123">This new file describes how the container image is to be built.</span></span> <span data-ttu-id="18178-124">Ardından ikinci, yeni bir _docker compose'u_ proje çözüme eklenir.</span><span class="sxs-lookup"><span data-stu-id="18178-124">Then second, a new _docker-compose_ project is added to the solution.</span></span> <span data-ttu-id="18178-125">Yeni Proje birkaç içeren dosyaları docker compose'u.</span><span class="sxs-lookup"><span data-stu-id="18178-125">The new project contains a few docker-compose files.</span></span> <span data-ttu-id="18178-126">Docker compose'u dosyaları kapsayıcı nasıl yürütüleceğini tanımlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="18178-126">Docker-compose files can be used to describe how the container is run.</span></span>

<span data-ttu-id="18178-127">İle çalışma hakkında daha fazla bilgi [Visual Studio kapsayıcı Araçları][link-visualstudio-container-tools].</span><span class="sxs-lookup"><span data-stu-id="18178-127">More info on working with [Visual Studio Container Tools][link-visualstudio-container-tools].</span></span>

>[!NOTE]
><span data-ttu-id="18178-128">Windows kapsayıcı görüntülerini bilgisayarınızda çalıştırdığınız ilk kez ise, Docker CE kapsayıcılarınızı temel görüntülerde aşağı çekmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="18178-128">If it is the first time you are running Windows container images on your computer, Docker CE must pull down the base images for your containers.</span></span> <span data-ttu-id="18178-129">Bu öğreticide kullanılan görüntüleri 14 GB bağımsızdır.</span><span class="sxs-lookup"><span data-stu-id="18178-129">The images used in this tutorial are 14 GB.</span></span> <span data-ttu-id="18178-130">Bir tane temel görüntüleri çıkarmak için terminal aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="18178-130">Go ahead and run the following terminal command to pull the base images:</span></span>
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a><span data-ttu-id="18178-131">Docker desteği ekleme</span><span class="sxs-lookup"><span data-stu-id="18178-131">Add Docker support</span></span>

<span data-ttu-id="18178-132">Açık [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] dosyasını Visual Studio'da.</span><span class="sxs-lookup"><span data-stu-id="18178-132">Open the [FabrikamFiber.CallCenter.sln][link-fabrikam-github] file in Visual Studio.</span></span>

<span data-ttu-id="18178-133">Sağ **FabrikamFiber.Web** Proje > **Ekle** > **Docker Destek**.</span><span class="sxs-lookup"><span data-stu-id="18178-133">Right-click the **FabrikamFiber.Web** project > **Add** > **Docker Support**.</span></span>

### <a name="add-support-for-sql"></a><span data-ttu-id="18178-134">SQL desteği ekleme</span><span class="sxs-lookup"><span data-stu-id="18178-134">Add support for SQL</span></span>

<span data-ttu-id="18178-135">Bu uygulama, bir SQL server uygulamayı çalıştırmak için gerekli olacak şekilde SQL veri sağlayıcısı olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="18178-135">This application uses SQL as the data provider, so a SQL server is required to run the application.</span></span> <span data-ttu-id="18178-136">Bizim docker compose.override.yml dosyasındaki bir SQL Server kapsayıcı yansıma başvuru.</span><span class="sxs-lookup"><span data-stu-id="18178-136">Reference a SQL Server container image in our docker-compose.override.yml file.</span></span>

<span data-ttu-id="18178-137">Visual Studio'da açın **Çözüm Gezgini**, bulma **docker compose'u**ve dosyayı açmak **docker compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="18178-137">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open the file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="18178-138">Gidin `services:` düğümü, adlandırılmış bir düğüm eklemek `db:` kapsayıcısı için SQL Server giriş tanımlar.</span><span class="sxs-lookup"><span data-stu-id="18178-138">Navigate to the `services:` node, add a node named `db:` that defines the SQL Server entry for the container.</span></span>

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
><span data-ttu-id="18178-139">Ana bilgisayardan erişilebilir olduğu müddetçe, yerel hata ayıklama için tercih ettiğiniz herhangi bir SQL sunucusu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18178-139">You can use any SQL Server you prefer for local debugging, as long as it is reachable from your host.</span></span> <span data-ttu-id="18178-140">Ancak, **localdb** desteklemediği `container -> host` iletişim.</span><span class="sxs-lookup"><span data-stu-id="18178-140">However, **localdb** does not support `container -> host` communication.</span></span>

>[!WARNING]
><span data-ttu-id="18178-141">SQL Server çalıştıran bir kapsayıcıda kalıcı veri desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="18178-141">Running SQL Server in a container does not support persisting data.</span></span> <span data-ttu-id="18178-142">Kapsayıcı sona erdiğinde, verileriniz silinir.</span><span class="sxs-lookup"><span data-stu-id="18178-142">When the container stops, your data is erased.</span></span> <span data-ttu-id="18178-143">Bu yapılandırma, üretim için kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="18178-143">Do not use this configuration for production.</span></span>

<span data-ttu-id="18178-144">Gidin `fabrikamfiber.web:` düğümü ve adlı bir alt düğüm eklemek `depends_on:`.</span><span class="sxs-lookup"><span data-stu-id="18178-144">Navigate to the `fabrikamfiber.web:` node and add a child node named `depends_on:`.</span></span> <span data-ttu-id="18178-145">Bu sağlar `db` hizmetini (SQL Server kapsayıcısı) web uygulamamız önce (fabrikamfiber.web) başlatır.</span><span class="sxs-lookup"><span data-stu-id="18178-145">This ensures that the `db` service (the SQL Server container) starts before our web application (fabrikamfiber.web).</span></span>

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-the-web-config"></a><span data-ttu-id="18178-146">Güncelleştirme web yapılandırma</span><span class="sxs-lookup"><span data-stu-id="18178-146">Update the web config</span></span>

<span data-ttu-id="18178-147">Geri **FabrikamFiber.Web** proje, bağlantı dizesinde güncelleştirme **web.config** kapsayıcısında SQL sunucusunu işaret edecek şekilde dosya.</span><span class="sxs-lookup"><span data-stu-id="18178-147">Back in the **FabrikamFiber.Web** project, update the connection string in the **web.config** file, to point to the SQL Server in the container.</span></span>

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
><span data-ttu-id="18178-148">Farklı bir kullanmak istiyorsanız, bir yayın oluştururken, SQL Server web uygulamanızın veya derleme, başka bir bağlantı dizesi web.release.config dosyanıza ekleyin.</span><span class="sxs-lookup"><span data-stu-id="18178-148">If you want to use a different SQL Server when building a release build of your web application, add another connection string to your web.release.config file.</span></span>

### <a name="test-your-container"></a><span data-ttu-id="18178-149">Test, kapsayıcısı</span><span class="sxs-lookup"><span data-stu-id="18178-149">Test your container</span></span>

<span data-ttu-id="18178-150">Tuşuna **F5** çalıştırıp, kapsayıcı uygulamada hata ayıklama için.</span><span class="sxs-lookup"><span data-stu-id="18178-150">Press **F5** to run and debug the application in your container.</span></span>

<span data-ttu-id="18178-151">Edge iç NAT ağdaki (genellikle 172.x.x.x) kapsayıcı IP adresini kullanarak uygulamanızın tanımlanmış başlatma sayfasını açar.</span><span class="sxs-lookup"><span data-stu-id="18178-151">Edge opens your application's defined launch page using the IP address of the container on the internal NAT network (typically 172.x.x.x).</span></span> <span data-ttu-id="18178-152">Visual Studio 2017 kullanarak kapsayıcıları uygulamalarında hata ayıklama hakkında daha fazla bilgi için bkz: [bu makalede][link-debug-container].</span><span class="sxs-lookup"><span data-stu-id="18178-152">To learn more about debugging applications in containers using Visual Studio 2017, see [this article][link-debug-container].</span></span>

![bir kapsayıcıda fabrikam örneği][image-web-preview]

<span data-ttu-id="18178-154">Kapsayıcı şimdi oluşturulur ve bir Service Fabric uygulaması paketlenmiş hazırdır.</span><span class="sxs-lookup"><span data-stu-id="18178-154">The container is now ready to be built and packaged in a Service Fabric application.</span></span> <span data-ttu-id="18178-155">Makinenizde yerleşik kapsayıcı görüntü olduktan sonra kapsayıcı kayıt defterine itme ve çalıştırmak için herhangi bir ana aşağıya doğru çekme.</span><span class="sxs-lookup"><span data-stu-id="18178-155">Once you have the container image built on your machine, you can push it to any container registry and pull it down to any host to run.</span></span>

## <a name="get-the-application-ready-for-the-cloud"></a><span data-ttu-id="18178-156">Uygulamayı bulut için hazırlanma</span><span class="sxs-lookup"><span data-stu-id="18178-156">Get the application ready for the cloud</span></span>

<span data-ttu-id="18178-157">Uygulama Azure Service Fabric içinde çalıştırmak için hazır hale getirmek için iki adımı tamamlamak ihtiyacımız var:</span><span class="sxs-lookup"><span data-stu-id="18178-157">To get the application ready for running in Service Fabric in Azure, we need to complete two steps:</span></span>

1. <span data-ttu-id="18178-158">Burada web uygulamamız Service Fabric kümesindeki ulaşabilmesi istiyoruz bağlantı noktasını kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="18178-158">Expose the port where we want to be able to reach our web application in the Service Fabric cluster.</span></span>
2. <span data-ttu-id="18178-159">Bir üretim hazır SQL veritabanı uygulamamız için sağlayın.</span><span class="sxs-lookup"><span data-stu-id="18178-159">Provide a production ready SQL database for our application.</span></span>

### <a name="expose-the-port-for-the-app"></a><span data-ttu-id="18178-160">Uygulama için bağlantı noktası kullanıma sunma</span><span class="sxs-lookup"><span data-stu-id="18178-160">Expose the port for the app</span></span>
<span data-ttu-id="18178-161">Yapılandırılmış, Service Fabric kümesi olan bağlantı noktası *80* açık Azure yük dengeleyici varsayılan olarak, kümeye gelen trafiği dengeler.</span><span class="sxs-lookup"><span data-stu-id="18178-161">The Service Fabric cluster we have configured, has port *80* open by default in the Azure Load Balancer, that balances incoming traffic to the cluster.</span></span> <span data-ttu-id="18178-162">Biz bu bağlantı noktasında bizim kapsayıcı bizim docker-compose.yml dosyası getirebilir.</span><span class="sxs-lookup"><span data-stu-id="18178-162">We can expose our container on this port via our docker-compose.yml file.</span></span>

<span data-ttu-id="18178-163">Visual Studio'da açın **Çözüm Gezgini**, bulma **docker compose'u**ve dosyayı açmak **docker compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="18178-163">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open the file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="18178-164">Değiştirme `fabrikamfiber.web:` düğümü adlı bir alt düğüm eklemek `ports:`.</span><span class="sxs-lookup"><span data-stu-id="18178-164">Modify the `fabrikamfiber.web:` node, add a child node named `ports:`.</span></span>

<span data-ttu-id="18178-165">Bir dize girişi ekleme `- "80:80"`.</span><span class="sxs-lookup"><span data-stu-id="18178-165">Add a string entry `- "80:80"`.</span></span>

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

### <a name="use-a-production-sql-database"></a><span data-ttu-id="18178-166">Bir üretim SQL veritabanını kullan</span><span class="sxs-lookup"><span data-stu-id="18178-166">Use a production SQL database</span></span>
<span data-ttu-id="18178-167">Üretimde çalıştırırken, verilerimizi ihtiyacımız bizim veritabanında kalıcı.</span><span class="sxs-lookup"><span data-stu-id="18178-167">When running in production, we need our data persisted in our database.</span></span> <span data-ttu-id="18178-168">Şu anda bir kapsayıcıda kalıcı veri güvence altına almak için bir yolu yoktur, bu nedenle bir kapsayıcıda SQL Server'daki üretim verileri depolanamıyor.</span><span class="sxs-lookup"><span data-stu-id="18178-168">There is currently no way to guarantee persistent data in a container, therefore you cannot store production data in SQL Server in a container.</span></span>

<span data-ttu-id="18178-169">Bir Azure SQL veritabanı kullanan öneririz.</span><span class="sxs-lookup"><span data-stu-id="18178-169">We recommend you utilize an Azure SQL Database.</span></span> <span data-ttu-id="18178-170">Ayarlama ve yönetilen bir SQL Server Azure'da çalışması için ziyaret edin [Azure SQL veritabanı hızlı başlangıç ipuçları] [ link-azure-sql] makalesi.</span><span class="sxs-lookup"><span data-stu-id="18178-170">To set up and run a managed SQL Server in Azure, visit the [Azure SQL Database Quickstarts][link-azure-sql] article.</span></span>

>[!NOTE]
><span data-ttu-id="18178-171">SQL server için bağlantı dizelerini değiştirmeyi unutmayın **web.release.config** dosyasını **FabrikamFiber.Web** projesi.</span><span class="sxs-lookup"><span data-stu-id="18178-171">Remember to change the connection strings to the SQL server in the **web.release.config** file in the **FabrikamFiber.Web** project.</span></span>
>
><span data-ttu-id="18178-172">SQL veritabanı erişilebilir olduğundan, bu uygulama düzgün biçimde başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="18178-172">This application fails gracefully if no SQL database is reachable.</span></span> <span data-ttu-id="18178-173">Devam edin ve SQL server ile uygulama dağıtmak seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18178-173">You can choose to go ahead and deploy the application with no SQL server.</span></span>

## <a name="deploy-with-visual-studio-team-services"></a><span data-ttu-id="18178-174">Visual Studio Team Services ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="18178-174">Deploy with Visual Studio Team Services</span></span>

<span data-ttu-id="18178-175">Visual Studio Team Services kullanarak dağıtımı ayarlamak için yüklemeniz gerekir [sürekli teslim araçları uzantısı için Visual Studio 2017][link-visualstudio-cd-extension].</span><span class="sxs-lookup"><span data-stu-id="18178-175">To set up deployment using Visual Studio Team Services, you need to install the [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension].</span></span> <span data-ttu-id="18178-176">Bu uzantıyı Visual Studio Team Services yapılandırarak Azure'a dağıtma ve, Service Fabric kümesi dağıtılmış uygulamanızı alma daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="18178-176">This extension makes it easy to deploy to Azure by configuring Visual Studio Team Services and get your app deployed to your Service Fabric cluster.</span></span>

<span data-ttu-id="18178-177">Başlamak için kaynak denetiminde kodunuzun barındırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="18178-177">To get started, your code must be hosted in source control.</span></span> <span data-ttu-id="18178-178">Bu bölümde rest varsayar **git** kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="18178-178">The rest of this section assumes **git** is being used.</span></span>

### <a name="set-up-a-vsts-repo"></a><span data-ttu-id="18178-179">VSTS depodaki ayarlayın</span><span class="sxs-lookup"><span data-stu-id="18178-179">Set up a VSTS repo</span></span>
<span data-ttu-id="18178-180">Visual Studio sağ alt köşesinde tıklatın **eklemek için kaynak denetimi** > **Git** (veya hangi seçeneği tercih).</span><span class="sxs-lookup"><span data-stu-id="18178-180">At the bottom-right corner of Visual Studio, click **Add to Source Control** > **Git** (or whichever option you prefer).</span></span>

![Kaynak denetimi düğmesine basın][image-source-control]

<span data-ttu-id="18178-182">İçinde _Takım Gezgini_ bölmesi, basın **yayımlama Git deposuna**.</span><span class="sxs-lookup"><span data-stu-id="18178-182">In the _Team Explorer_ pane, press **Publish Git Repo**.</span></span>

<span data-ttu-id="18178-183">VSTS havuz adı ve tuşuna seçin **depo**.</span><span class="sxs-lookup"><span data-stu-id="18178-183">Select your VSTS repository name and press **Repository**.</span></span>

![Depodaki VSTS yayımlama][image-publish-repo]

<span data-ttu-id="18178-185">Kodunuzu VSTS kaynak deposu ile eşitlenir, sürekli tümleştirme ve kesintisiz teslim yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18178-185">Now that your code is synchronized with a VSTS source repository, you can configure continuous integration and continuous delivery.</span></span>

### <a name="setup-continuous-delivery"></a><span data-ttu-id="18178-186">Kurulum kesintisiz teslim</span><span class="sxs-lookup"><span data-stu-id="18178-186">Setup continuous delivery</span></span>

<span data-ttu-id="18178-187">İçinde _Çözüm Gezgini_, sağ **çözüm** > **yapılandırma kesintisiz teslim**.</span><span class="sxs-lookup"><span data-stu-id="18178-187">In _Solution Explorer_, right-click the **solution** > **Configure Continuous Delivery**.</span></span>

<span data-ttu-id="18178-188">Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="18178-188">Select the Azure Subscription.</span></span>

<span data-ttu-id="18178-189">Ayarlama **ana bilgisayar türü** için **Service Fabric kümesi**.</span><span class="sxs-lookup"><span data-stu-id="18178-189">Set **Host Type** to **Service Fabric Cluster**.</span></span>

<span data-ttu-id="18178-190">Ayarlama **hedef ana bilgisayarın** önceki bölümde oluşturduğunuz service fabric kümesi için.</span><span class="sxs-lookup"><span data-stu-id="18178-190">Set **Target Host** to the service fabric cluster you created in the previous section.</span></span>

<span data-ttu-id="18178-191">Seçin bir **kapsayıcı kayıt defteri** , kapsayıcıya yayımlamak için.</span><span class="sxs-lookup"><span data-stu-id="18178-191">Choose a **Container Registry** to publish your container to.</span></span>

>[!TIP]
><span data-ttu-id="18178-192">Kullanım **Düzenle** kapsayıcı kayıt oluşturmak üzere düğmesi.</span><span class="sxs-lookup"><span data-stu-id="18178-192">Use the **Edit** button to create a container registry.</span></span>

<span data-ttu-id="18178-193">**Tamam**'a basın.</span><span class="sxs-lookup"><span data-stu-id="18178-193">Press **OK**.</span></span>

![Kurulum service fabric sürekli tümleştirme][image-setup-ci]
   
   <span data-ttu-id="18178-195">Yapılandırma tamamlandıktan sonra kapsayıcı için Service Fabric dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="18178-195">Once the configuration is completed, your container is deployed to Service Fabric.</span></span> <span data-ttu-id="18178-196">Her değiştiğinde, anında iletme depoya yeni bir yapı güncelleştirir ve yayın yürütülür.</span><span class="sxs-lookup"><span data-stu-id="18178-196">Whenever you push updates to the repository a new build and release is executed.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="18178-197">Kapsayıcı görüntüleri alma yaklaşık 15 dakika oluşturma.</span><span class="sxs-lookup"><span data-stu-id="18178-197">Building the container images take approximately 15 minutes.</span></span>
   ><span data-ttu-id="18178-198">Service Fabric kümesi ilk dağıtımda yüklenmek üzere temel Windows Server Core kapsayıcı görüntüleri neden olur.</span><span class="sxs-lookup"><span data-stu-id="18178-198">The first deployment to the Service Fabric cluster causes the base Windows Server Core container images to be downloaded.</span></span> <span data-ttu-id="18178-199">Yüklemeyi tamamlamak için ek 5-10 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="18178-199">The download takes additional 5-10 minutes to complete.</span></span>

<span data-ttu-id="18178-200">Kümenizin URL'yi kullanarak Fabrikam çağrı merkezi uygulaması'na göz: Örneğin, *http://mycluster.westeurope.cloudapp.azure.com*</span><span class="sxs-lookup"><span data-stu-id="18178-200">Browse to the Fabrikam Call Center application using the url of your cluster: for example, *http://mycluster.westeurope.cloudapp.azure.com*</span></span>

<span data-ttu-id="18178-201">Kapsayıcılı ve Fabrikam çağrı merkezi çözümü dağıtılmış göre açabilirsiniz [Azure portal] [ link-azure-portal] ve Service Fabric içinde çalışan uygulama bakın.</span><span class="sxs-lookup"><span data-stu-id="18178-201">Now that you have containerized and deployed the Fabrikam Call Center solution, you can open the [Azure portal][link-azure-portal] and see the application running in Service Fabric.</span></span> <span data-ttu-id="18178-202">Uygulama denemek için bir web tarayıcısı açın ve Service Fabric kümesi URL'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="18178-202">To try the application, open a web browser and go to the URL of your Service Fabric cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18178-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="18178-203">Next steps</span></span>

<span data-ttu-id="18178-204">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="18178-204">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="18178-205">Visual Studio'da bir Docker projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="18178-205">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="18178-206">Varolan bir uygulama containerize</span><span class="sxs-lookup"><span data-stu-id="18178-206">Containerize an existing application</span></span>
> * <span data-ttu-id="18178-207">Visual Studio ve VSTS sürekli tümleştirme Kurulumu</span><span class="sxs-lookup"><span data-stu-id="18178-207">Setup continuous integration with Visual Studio and VSTS</span></span>

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance to the next tutorial to learn how to bind a custom SSL certificate to it.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate to Azure Web Apps](app-service-web-tutorial-custom-ssl.md)

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
