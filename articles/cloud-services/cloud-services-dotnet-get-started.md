---
title: "aaaGet başlatılan Azure Cloud Services ve ASP.NET ile | Microsoft Docs"
description: "Bilgi nasıl toocreate ASP.NET MVC ve Azure kullanarak çok katmanlı bir uygulama. web rolü ve çalışan rolü ile birlikte bir bulut hizmetinde Hello uygulama çalışır. Entity Framework, SQL Database ve Azure Storage kuyruklarını ve blob’larını kullanır."
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: adegeo
ms.openlocfilehash: 86271c29b79fad3f01f8ea0e88fd00c7aefc970c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a><span data-ttu-id="e0f3e-105">Azure Cloud Services ve ASP.NET kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e0f3e-105">Get started with Azure Cloud Services and ASP.NET</span></span>

## <a name="overview"></a><span data-ttu-id="e0f3e-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e0f3e-106">Overview</span></span>
<span data-ttu-id="e0f3e-107">Bu öğreticide gösterilmiştir nasıl toocreate ön uç, ASP.NET MVC ile çok katmanlı .NET uygulaması ve tooan dağıtma [Azure bulut hizmeti](cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="e0f3e-107">This tutorial shows how toocreate a multi-tier .NET application with an ASP.NET MVC front-end, and deploy it tooan [Azure cloud service](cloud-services-choose-me.md).</span></span> <span data-ttu-id="e0f3e-108">Merhaba uygulamanız tarafından kullanılan [Azure SQL veritabanı](http://msdn.microsoft.com/library/azure/ee336279), hello [Azure Blob hizmeti](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)ve hello [Azure Queue hizmeti](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span><span class="sxs-lookup"><span data-stu-id="e0f3e-108">hello application uses [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), hello [Azure Blob service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and hello [Azure Queue service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span></span> <span data-ttu-id="e0f3e-109">Yapabilecekleriniz [hello Visual Studio projesi indirme](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) hello MSDN kod Galerisi'nden gelen.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-109">You can [download hello Visual Studio project](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) from hello MSDN Code Gallery.</span></span>

<span data-ttu-id="e0f3e-110">Merhaba öğretici gösterir, nasıl yerel olarak toobuild ve Çalıştır Merhaba uygulaması nasıl toodeploy, tooAzure ve içinde çalışma hello Bulut ve nasıl toobuild, sıfırdan.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-110">hello tutorial shows you how toobuild and run hello application locally, how toodeploy it tooAzure and run in hello cloud, and how toobuild it from scratch.</span></span> <span data-ttu-id="e0f3e-111">Sıfırdan oluşturmaya başlatın ve sonra test hello ve dağıtım adımlarını gerçekleştirebilirsiniz olarak tercih ederseniz otomatik.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-111">You can start by building from scratch and then do hello test and deploy steps afterward if you prefer.</span></span>

## <a name="contoso-ads-application"></a><span data-ttu-id="e0f3e-112">Contoso Ads uygulaması</span><span class="sxs-lookup"><span data-stu-id="e0f3e-112">Contoso Ads application</span></span>
<span data-ttu-id="e0f3e-113">Merhaba uygulama bir reklam Bülteni panosudur.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-113">hello application is an advertising bulletin board.</span></span> <span data-ttu-id="e0f3e-114">Kullanıcılar metin girerek ve görüntüyü karşıya yükleyerek bir reklam oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-114">Users create an ad by entering text and uploading an image.</span></span> <span data-ttu-id="e0f3e-115">Küçük resim görüntüleriyle birlikte bir reklam listesi görebilir ve bir ad toosee hello ayrıntıları seçtiğinizde hello tam boyutlu görüntüyü görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-115">They can see a list of ads with thumbnail images, and they can see hello full-size image when they select an ad toosee hello details.</span></span>

![Reklam listesi](./media/cloud-services-dotnet-get-started/list.png)

<span data-ttu-id="e0f3e-117">Merhaba uygulamanın kullandığı hello [kuyruk merkezli çalışma deseni](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff yük hello CPU yoğunluklu iş tooa arka uç işleminde küçük resim oluşturma.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-117">hello application uses hello [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff-load hello CPU-intensive work of creating thumbnails tooa back-end process.</span></span>

## <a name="alternative-architecture-websites-and-webjobs"></a><span data-ttu-id="e0f3e-118">Alternatif mimari: Websites ve WebJobs</span><span class="sxs-lookup"><span data-stu-id="e0f3e-118">Alternative architecture: Websites and WebJobs</span></span>
<span data-ttu-id="e0f3e-119">Bu öğretici nasıl toorun ön uç ve arka uç Azure içinde bulut gösterir hizmet.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-119">This tutorial shows how toorun both front-end and back-end in an Azure cloud service.</span></span> <span data-ttu-id="e0f3e-120">Ön uç içindeki toorun hello alternatiftir bir [Azure Web sitesi](/services/web-sites/) ve hello kullanın [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) hello arka uç (şu anda önizlemede) özelliği.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-120">An alternative is toorun hello front-end in an [Azure website](/services/web-sites/) and use hello [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) feature (currently in preview) for hello back-end.</span></span> <span data-ttu-id="e0f3e-121">WebJobs kullanan bir öğretici için bkz [hello Azure WebJobs SDK ile çalışmaya başlama](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e0f3e-121">For a tutorial that uses WebJobs, see [Get Started with hello Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span></span> <span data-ttu-id="e0f3e-122">Senaryonuz nasıl toochoose hello en iyi hizmetler hakkında bilgi sığması için bkz: [Azure Websites, Cloud Services ve sanal makineleri karşılaştırma](../app-service-web/choose-web-site-cloud-service-vm.md).</span><span class="sxs-lookup"><span data-stu-id="e0f3e-122">For information about how toochoose hello services that best fit your scenario, see [Azure Websites, Cloud Services, and virtual machines comparison](../app-service-web/choose-web-site-cloud-service-vm.md).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="e0f3e-123">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="e0f3e-123">What you'll learn</span></span>
* <span data-ttu-id="e0f3e-124">Nasıl tooenable makinenize yükleyerek Azure geliştirme için Azure SDK'sı hello.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-124">How tooenable your machine for Azure development by installing hello Azure SDK.</span></span>
* <span data-ttu-id="e0f3e-125">Nasıl toocreate Visual Studio bulut hizmeti projesine bir ASP.NET MVC web rolü ve çalışan rolü ile.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-125">How toocreate a Visual Studio cloud service project with an ASP.NET MVC web role and a worker role.</span></span>
* <span data-ttu-id="e0f3e-126">Nasıl tootest hello Azure storage öykünücüsü kullanarak bulut hizmeti projesini yerel olarak hello.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-126">How tootest hello cloud service project locally, using hello Azure storage emulator.</span></span>
* <span data-ttu-id="e0f3e-127">Nasıl toopublish hello bulut proje tooan Azure bulut hizmeti ve bir Azure depolama hesabı kullanarak test edin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-127">How toopublish hello cloud project tooan Azure cloud service and test using an Azure storage account.</span></span>
* <span data-ttu-id="e0f3e-128">Nasıl tooupload dosyaları ve hello Azure Blob hizmetine depolama.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-128">How tooupload files and store them in hello Azure Blob service.</span></span>
* <span data-ttu-id="e0f3e-129">Nasıl toouse katmanlar arasında iletişim için Azure Queue hizmetini hello.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-129">How toouse hello Azure Queue service for communication between tiers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0f3e-130">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e0f3e-130">Prerequisites</span></span>
<span data-ttu-id="e0f3e-131">Merhaba Öğreticisi, anladığınızı varsayar [Azure hakkında temel kavramları bulut hizmetlerini](cloud-services-choose-me.md) gibi *web rolü* ve *çalışan rolü* terminolojisi.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-131">hello tutorial assumes that you understand [basic concepts about Azure cloud services](cloud-services-choose-me.md) such as *web role* and *worker role* terminology.</span></span>  <span data-ttu-id="e0f3e-132">Ayrıca, bildiğinizi varsayar nasıl toowork ile [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) veya [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) Visual Studio projelerinde.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-132">It also assumes that you know how toowork with [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) or [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projects in Visual Studio.</span></span> <span data-ttu-id="e0f3e-133">Merhaba örnek uygulama MVC kullanır ancak çoğu hello öğreticinin tooWeb Forms de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-133">hello sample application uses MVC, but most of hello tutorial also applies tooWeb Forms.</span></span>

<span data-ttu-id="e0f3e-134">Merhaba uygulamayı bir Azure aboneliği olmadan yerel olarak çalıştırabilirsiniz, ancak bir toodeploy hello uygulama toohello bulut gerekir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-134">You can run hello app locally without an Azure subscription, but you'll need one toodeploy hello application toohello cloud.</span></span> <span data-ttu-id="e0f3e-135">Bir hesabınız yoksa, [MSDN abone avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) veya [ücretsiz deneme için kaydolabilirsiniz.](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668)</span><span class="sxs-lookup"><span data-stu-id="e0f3e-135">If you don't have an account, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span></span>

<span data-ttu-id="e0f3e-136">Merhaba öğretici yönergeleri aşağıdaki ürünler hello birini kullanarak çalışır:</span><span class="sxs-lookup"><span data-stu-id="e0f3e-136">hello tutorial instructions work with either of hello following products:</span></span>

* <span data-ttu-id="e0f3e-137">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="e0f3e-137">Visual Studio 2013</span></span>
* <span data-ttu-id="e0f3e-138">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="e0f3e-138">Visual Studio 2015</span></span>
* <span data-ttu-id="e0f3e-139">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="e0f3e-139">Visual Studio 2017</span></span>

<span data-ttu-id="e0f3e-140">Bunlardan birine sahip değilseniz, hello Azure SDK'yı yüklediğinizde Visual Studio otomatik olarak yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-140">If you don't have one of these, Visual Studio may be installed automatically when you install hello Azure SDK.</span></span>

## <a name="application-architecture"></a><span data-ttu-id="e0f3e-141">Uygulama mimarisi</span><span class="sxs-lookup"><span data-stu-id="e0f3e-141">Application architecture</span></span>
<span data-ttu-id="e0f3e-142">Merhaba uygulama ads Entity Framework Code First toocreate hello tabloları ve erişim hello verilerini kullanarak bir SQL veritabanında depolar.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-142">hello app stores ads in a SQL database, using Entity Framework Code First toocreate hello tables and access hello data.</span></span> <span data-ttu-id="e0f3e-143">Her ad için hello veritabanı depoları iki URL'ler, biri tam boyutlu görüntü ve diğeri hello küçük resim hello.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-143">For each ad, hello database stores two URLs, one for hello full-size image and one for hello thumbnail.</span></span>

![Reklam tablosu](./media/cloud-services-dotnet-get-started/adtable.png)

<span data-ttu-id="e0f3e-145">Bir kullanıcı görüntü yüklediğinde hello ön uç web rolünde çalışan hello görüntüde depolayan bir [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), ve hello veritabanı toohello blob'u işaret eden bir URL ile Merhaba ad bilgilerini depolar.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-145">When a user uploads an image, hello front-end running in a web role stores hello image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores hello ad information in hello database with a URL that points toohello blob.</span></span> <span data-ttu-id="e0f3e-146">AT hello aynı zaman, ileti tooan Azure kuyruk yazar.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-146">At hello same time, it writes a message tooan Azure queue.</span></span> <span data-ttu-id="e0f3e-147">Bir çalışan rolü düzenli aralıklarla çalışan bir arka uç işlemi hello sıra yeni iletiler için yoklar.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-147">A back-end process running in a worker role periodically polls hello queue for new messages.</span></span> <span data-ttu-id="e0f3e-148">Yeni bir ileti görüntülendiğinde, hello çalışan rolü bu görüntü için bir küçük resim oluşturur ve küçük resim URL'si veritabanı alanını bu reklam güncelleştirmeleri hello.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-148">When a new message appears, hello worker role creates a thumbnail for that image and updates hello thumbnail URL database field for that ad.</span></span> <span data-ttu-id="e0f3e-149">Merhaba Aşağıdaki diyagramda nasıl hello uygulamanın hello bölümlerini etkileşim kurduğu gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-149">hello following diagram shows how hello parts of hello application interact.</span></span>

![Contoso Ads mimarisi](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-hello-completed-solution"></a><span data-ttu-id="e0f3e-151">İndirme ve çalıştırma hello çözüm tamamlandı</span><span class="sxs-lookup"><span data-stu-id="e0f3e-151">Download and run hello completed solution</span></span>
1. <span data-ttu-id="e0f3e-152">İndirip hello sıkıştırmasını [tamamlanan çözümü](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span><span class="sxs-lookup"><span data-stu-id="e0f3e-152">Download and unzip hello [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span></span>
2. <span data-ttu-id="e0f3e-153">Visual Studio’yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-153">Start Visual Studio.</span></span>
3. <span data-ttu-id="e0f3e-154">Merhaba gelen **dosya** menüsünü seçin **Proje Aç**hello çözümü indirdiğiniz toowhere gidin ve ardından hello çözüm dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-154">From hello **File** menu choose **Open Project**, navigate toowhere you downloaded hello solution, and then open hello solution file.</span></span>
4. <span data-ttu-id="e0f3e-155">CTRL + SHIFT + B toobuild hello çözüm tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-155">Press CTRL+SHIFT+B toobuild hello solution.</span></span>

    <span data-ttu-id="e0f3e-156">Varsayılan olarak, Visual Studio hello dahil edilmeyen hello NuGet paket içeriği otomatik olarak yükler *.zip* dosyası.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-156">By default, Visual Studio automatically restores hello NuGet package content, which was not included in hello *.zip* file.</span></span> <span data-ttu-id="e0f3e-157">Merhaba paketler geri yüklenmezse varsa bunları el ile giderek toohello tarafından yükleyin **çözüm için NuGet paketlerini Yönet** iletişim kutusu ve hello tıklayarak **geri** düğmesine sağ hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-157">If hello packages don't restore, install them manually by going toohello **Manage NuGet Packages for Solution** dialog box and clicking hello **Restore** button at hello top right.</span></span>
5. <span data-ttu-id="e0f3e-158">İçinde **Çözüm Gezgini**, olduğundan emin olun **ContosoAdsCloudService** hello başlangıç projesi olarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-158">In **Solution Explorer**, make sure that **ContosoAdsCloudService** is selected as hello startup project.</span></span>
6. <span data-ttu-id="e0f3e-159">Sonraki hello uygulamada hello SQL Server bağlantı dizesini değiştirin veya Visual Studio 2015 kullanıyorsanız *Web.config* hello ContosoAdsWeb projesinin ve hello dosyasının *ServiceConfiguration.Local.cscfg* hello ContosoAdsCloudService projesinin dosya.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-159">If you're using Visual Studio 2015 or higher, change hello SQL Server connection string in hello application *Web.config* file of hello ContosoAdsWeb project and in hello *ServiceConfiguration.Local.cscfg* file of hello ContosoAdsCloudService project.</span></span> <span data-ttu-id="e0f3e-160">Her durumda, "(localdb) \v11.0" çok değiştirme "(localdb) \MSSQLLocalDB".</span><span class="sxs-lookup"><span data-stu-id="e0f3e-160">In each case, change "(localdb)\v11.0" too"(localdb)\MSSQLLocalDB".</span></span>
7. <span data-ttu-id="e0f3e-161">CTRL + F5 toorun Merhaba uygulaması tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-161">Press CTRL+F5 toorun hello application.</span></span>

    <span data-ttu-id="e0f3e-162">Bir bulut hizmeti projesini yerel olarak çalıştırdığınızda, Visual Studio hello Azure otomatik olarak çağırır. *işlem öykünücüsü* ve Azure *depolama öykünücüsü*.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-162">When you run a cloud service project locally, Visual Studio automatically invokes hello Azure *compute emulator* and Azure *storage emulator*.</span></span> <span data-ttu-id="e0f3e-163">bilgisayarınızın kaynaklarını toosimulate hello web rolü ve çalışan rolü ortamlarını Hello işlem öykünücüsü kullanır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-163">hello compute emulator uses your computer's resources toosimulate hello web role and worker role environments.</span></span> <span data-ttu-id="e0f3e-164">Merhaba depolama öykünücüsü kullanan bir [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) veritabanı toosimulate Azure bulut depolama.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-164">hello storage emulator uses a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database toosimulate Azure cloud storage.</span></span>

    <span data-ttu-id="e0f3e-165">Merhaba bir bulut hizmeti projesini ilk çalıştırdığınızda veya bunu dakika hello Öykünücüler toostart geçen.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-165">hello first time you run a cloud service project, it takes a minute or so for hello emulators toostart up.</span></span> <span data-ttu-id="e0f3e-166">Öykünücü başlatma tamamlandığında hello varsayılan tarayıcı toohello uygulama giriş sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-166">When emulator startup is finished, hello default browser opens toohello application home page.</span></span>

    ![Contoso Ads mimarisi](./media/cloud-services-dotnet-get-started/home.png)
8. <span data-ttu-id="e0f3e-168">**Reklam Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-168">Click  **Create an Ad**.</span></span>
9. <span data-ttu-id="e0f3e-169">Bazı test verilerini girin ve bir *.jpg* görüntü tooupload ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-169">Enter some test data and select a *.jpg* image tooupload, and then click **Create**.</span></span>

    ![Sayfa oluşturma](./media/cloud-services-dotnet-get-started/create.png)

    <span data-ttu-id="e0f3e-171">Merhaba uygulama toohello dizin sayfasına gider, ancak işleme henüz tamamlanmadığından hello yeni ad için bir küçük resim göstermez.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-171">hello app goes toohello Index page, but it doesn't show a thumbnail for hello new ad because that processing hasn't happened yet.</span></span>
10. <span data-ttu-id="e0f3e-172">Biraz bekleyin ve ardından hello dizin sayfası toosee hello küçük yenileyin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-172">Wait a moment and then refresh hello Index page toosee hello thumbnail.</span></span>

     ![Dizin sayfası](./media/cloud-services-dotnet-get-started/list.png)
11. <span data-ttu-id="e0f3e-174">Tıklatın **ayrıntıları** ad toosee hello tam boyutlu görüntü için.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-174">Click **Details** for your ad toosee hello full-size image.</span></span>

     ![Ayrıntılar sayfası](./media/cloud-services-dotnet-get-started/details.png)

<span data-ttu-id="e0f3e-176">Merhaba uygulaması tamamen, yerel bilgisayarınızda, bağlantı toohello bulutsuz çalışır durumda.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-176">You've been running hello application entirely on your local computer, with no connection toohello cloud.</span></span> <span data-ttu-id="e0f3e-177">Merhaba depolama öykünücüsü hello sıra depolar ve blob verilerini bir SQL Server Express LocalDB veritabanına ve Merhaba uygulaması hello ad verileri başka bir LocalDB veritabanına depolar.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-177">hello storage emulator stores hello queue and blob data in a SQL Server Express LocalDB database, and hello application stores hello ad data in another LocalDB database.</span></span> <span data-ttu-id="e0f3e-178">Entity Framework Code First otomatik olarak oluşturulan hello ad veritabanı hello hello web uygulaması tooaccess çalıştı ilk kez.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-178">Entity Framework Code First automatically created hello ad database hello first time hello web app tried tooaccess it.</span></span>

<span data-ttu-id="e0f3e-179">Bölümden hello hello bulutta çalışan kuyruklar, BLOB'lar ve hello uygulama veritabanı için hello çözüm toouse Azure bulut kaynakları yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-179">In hello following section you'll configure hello solution toouse Azure cloud resources for queues, blobs, and hello application database when it runs in hello cloud.</span></span> <span data-ttu-id="e0f3e-180">Yerel olarak toocontinue toorun istedi, ancak bulut depolama ve veritabanı kaynaklarını kullanan, yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-180">If you wanted toocontinue toorun locally but use cloud storage and database resources, you could do that.</span></span> <span data-ttu-id="e0f3e-181">Bunu göreceğiniz bağlantı dizelerini ayarlama yalnızca bir konudur nasıl toodo.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-181">It's just a matter of setting connection strings, which you'll see how toodo.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="e0f3e-182">Merhaba uygulama tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="e0f3e-182">Deploy hello application tooAzure</span></span>
<span data-ttu-id="e0f3e-183">Siz gerçekleştirirsiniz adımları toorun hello hello bulut uygulamasında aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="e0f3e-183">You'll do hello following steps toorun hello application in hello cloud:</span></span>

* <span data-ttu-id="e0f3e-184">Bir Azure bulut hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-184">Create an Azure cloud service.</span></span>
* <span data-ttu-id="e0f3e-185">Bir Azure SQL veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-185">Create an Azure SQL database.</span></span>
* <span data-ttu-id="e0f3e-186">Bir Azure Storage hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-186">Create an Azure storage account.</span></span>
* <span data-ttu-id="e0f3e-187">Azure'da çalıştığında Azure SQL veritabanınızı hello çözüm toouse yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-187">Configure hello solution toouse your Azure SQL database when it runs in Azure.</span></span>
* <span data-ttu-id="e0f3e-188">Azure'da çalıştığında Azure storage hesabınızı hello çözüm toouse yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-188">Configure hello solution toouse your Azure storage account when it runs in Azure.</span></span>
* <span data-ttu-id="e0f3e-189">Merhaba proje tooyour Azure bulut hizmeti dağıtın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-189">Deploy hello project tooyour Azure cloud service.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="e0f3e-190">Bir Azure bulut hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="e0f3e-190">Create an Azure cloud service</span></span>
<span data-ttu-id="e0f3e-191">Merhaba ortamı hello uygulamanın çalıştırılacağı bir Azure bulut hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-191">An Azure cloud service is hello environment hello application will run in.</span></span>

1. <span data-ttu-id="e0f3e-192">Merhaba, tarayıcınızı açmak [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e0f3e-192">In your browser, open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e0f3e-193">**Yeni > Hesapla > Bulut Hizmeti**’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-193">Click **New > Compute > Cloud Service**.</span></span>

3. <span data-ttu-id="e0f3e-194">Merhaba DNS adı giriş kutusuna hello bulut hizmeti için bir URL ön eki girin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-194">In hello DNS name input box, enter a URL prefix for hello cloud service.</span></span>

    <span data-ttu-id="e0f3e-195">Bu URL benzersiz toobe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-195">This URL has toobe unique.</span></span>  <span data-ttu-id="e0f3e-196">Seçtiğiniz hello öneki zaten kullanılıyorsa bir hata iletisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-196">You'll get an error message if hello prefix you choose is already in use.</span></span>
4. <span data-ttu-id="e0f3e-197">Merhaba hizmet için yeni bir kaynak grubu belirtin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-197">Specify a new Resource group for hello  service.</span></span> <span data-ttu-id="e0f3e-198">Tıklatın **Yeni Oluştur** ve hello kaynak grubu giriş kutusunda CS_contososadsRG gibi bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-198">Click **Create new** and then type a name in hello Resource group input box, such as CS_contososadsRG.</span></span>

5. <span data-ttu-id="e0f3e-199">Merhaba bölge toodeploy Merhaba uygulaması istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-199">Choose hello region where you want toodeploy hello application.</span></span>

    <span data-ttu-id="e0f3e-200">Bu alan, bulut hizmetinizin hangi veri merkezinde barındırılacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-200">This field specifies which datacenter your cloud service will be hosted in.</span></span> <span data-ttu-id="e0f3e-201">Bir üretim uygulaması için hello bölgeye en yakın tooyour müşteriler seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-201">For a production application, you'd choose hello region closest tooyour customers.</span></span> <span data-ttu-id="e0f3e-202">Bu öğretici için hello bölgeye en yakın tooyou seçin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-202">For this tutorial, choose hello region closest tooyou.</span></span>
5. <span data-ttu-id="e0f3e-203">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-203">Click **Create**.</span></span>

    <span data-ttu-id="e0f3e-204">Görüntü aşağıdaki hello, bir bulut hizmeti ile Merhaba URL CSvccontosoads.cloudapp.net oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-204">In hello following image, a cloud service is created with hello URL CSvccontosoads.cloudapp.net.</span></span>

    ![Yeni Bulut Hizmeti](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a><span data-ttu-id="e0f3e-206">Bir Azure SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e0f3e-206">Create an Azure SQL database</span></span>
<span data-ttu-id="e0f3e-207">Merhaba uygulama hello bulutta çalıştırıldığında bulut tabanlı bir veritabanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-207">When hello app runs in hello cloud, it will use a cloud-based database.</span></span>

1. <span data-ttu-id="e0f3e-208">Merhaba, [Azure portal](https://portal.azure.com), tıklatın **yeni > veritabanları > SQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-208">In hello [Azure portal](https://portal.azure.com), click **New > Databases > SQL Database**.</span></span>
2. <span data-ttu-id="e0f3e-209">Merhaba, **veritabanı adı** kutusuna *contosoads*.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-209">In hello **Database Name** box, enter *contosoads*.</span></span>
3. <span data-ttu-id="e0f3e-210">Merhaba, **kaynak grubu**, tıklatın **var olanı kullan** ve hello bulut hizmeti için kullanılan select hello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-210">In hello **Resource group**, click **Use existing** and select hello resource group used for hello cloud service.</span></span>
4. <span data-ttu-id="e0f3e-211">Görüntü, aşağıdaki Hello tıklatın **Server - gerekli ayarları Yapılandır** ve **yeni bir sunucu oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-211">In hello following image, click **Server - Configure required settings** and **Create a new server**.</span></span>

    ![Tünel toodatabase sunucusu](./media/cloud-services-dotnet-get-started/newdb.png)

    <span data-ttu-id="e0f3e-213">Alternatif olarak, aboneliğiniz zaten bir sunucu varsa, bu sunucu hello aşağı açılan listeden seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-213">Alternatively, if your subscription already has a server, you can select that server from hello drop-down list.</span></span>
5. <span data-ttu-id="e0f3e-214">Merhaba, **sunucu adı** kutusuna *csvccontosodbserver*.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-214">In hello **Server name** box, enter *csvccontosodbserver*.</span></span>

6. <span data-ttu-id="e0f3e-215">Bir yönetici için **Kullanıcı Adı** ve **Parola** girin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-215">Enter an administrator **Login Name** and **Password**.</span></span>

    <span data-ttu-id="e0f3e-216">**Yeni sunucu oluştur**’u seçtiyseniz buraya mevcut bir adı ve parolayı girmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-216">If you selected **Create a new server**, you aren't entering an existing name and password here.</span></span> <span data-ttu-id="e0f3e-217">Yeni bir ad ve parola hello veritabanına eriştiğinizde şimdi toouse daha sonra tanımladığınız girersiniz.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-217">You're entering a new name and password that you're defining now toouse later when you access hello database.</span></span> <span data-ttu-id="e0f3e-218">Daha önce oluşturduğunuz bir sunucuyu seçtiyseniz önceden oluşturduğunuz hello parola toohello yönetici kullanıcı hesabı için istenir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-218">If you selected a server that you created previously, you'll be prompted for hello password toohello administrative user account you already created.</span></span>
7. <span data-ttu-id="e0f3e-219">Seçin aynı hello **konumu** hello bulut hizmeti için seçtiğiniz.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-219">Choose hello same **Location** that you chose for hello cloud service.</span></span>

    <span data-ttu-id="e0f3e-220">Merhaba bulut hizmeti ve veritabanı olduğunda farklı veri merkezlerinde (farklı bölgelerde) gecikme artar ve, hello veri merkezinin dışındaki bant genişliği için sizden ücret alınır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-220">When hello cloud service and database are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside hello data center.</span></span> <span data-ttu-id="e0f3e-221">Bir veri merkezi içinde bant genişliği ücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-221">Bandwidth within a data center is free.</span></span>
8. <span data-ttu-id="e0f3e-222">Denetleme **izin azure Hizmetleri tooaccess sunucusu**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-222">Check **Allow azure services tooaccess server**.</span></span>
9. <span data-ttu-id="e0f3e-223">Tıklatın **seçin** hello yeni sunucu için.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-223">Click **Select** for hello new server.</span></span>

    ![Yeni SQL Veritabanı sunucusu](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. <span data-ttu-id="e0f3e-225">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-225">Click **Create**.</span></span>

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="e0f3e-226">Azure Storage hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e0f3e-226">Create an Azure storage account</span></span>
<span data-ttu-id="e0f3e-227">Bir Azure depolama hesabı, kuyruk ve blob verilerini hello bulutta depolamak için kaynaklar sağlar.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-227">An Azure storage account provides resources for storing queue and blob data in hello cloud.</span></span>

<span data-ttu-id="e0f3e-228">Gerçek bir uygulamada genellikle uygulama verilerine karşı günlük verileri için ve test verilerine karşı üretim verileri için ayrı hesaplar oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-228">In a real-world application, you would typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span></span> <span data-ttu-id="e0f3e-229">Bu öğreticide yalnızca tek bir hesap kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-229">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="e0f3e-230">Merhaba, [Azure portal](https://portal.azure.com), tıklatın **yeni > depolama > depolama hesabı - blob, dosya, tablo, kuyruk**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-230">In hello [Azure portal](https://portal.azure.com), click **New > Storage > Storage account - blob, file, table, queue**.</span></span>
2. <span data-ttu-id="e0f3e-231">Merhaba, **adı** kutusunda, bir URL ön eki girin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-231">In hello **Name** box, enter a URL prefix.</span></span>

    <span data-ttu-id="e0f3e-232">Merhaba kutunun altında gördüğünüz bu öneki ve hello metin hello benzersiz URL tooyour depolama hesabı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-232">This prefix plus hello text you see under hello box will be hello unique URL tooyour storage account.</span></span> <span data-ttu-id="e0f3e-233">Girdiğiniz hello öneki zaten başka bir kullanıcı tarafından kullanılıyorsa, farklı bir önek toochoose sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-233">If hello prefix you enter has already been used by someone else, you'll have toochoose a different prefix.</span></span>
3. <span data-ttu-id="e0f3e-234">Set hello **dağıtım modeli** çok*Klasik*.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-234">Set hello **Deployment model** too*Classic*.</span></span>

4. <span data-ttu-id="e0f3e-235">Set hello **çoğaltma** aşağı açılan listesinde çok**yerel olarak yedekli depolama**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-235">Set hello **Replication** drop-down list too**Locally redundant storage**.</span></span>

    <span data-ttu-id="e0f3e-236">Bir depolama hesabı için coğrafi çoğaltma etkinleştirildiğinde, hello birincil konumda önemli bir olağanüstü durum oluşursa, depolanan hello çoğaltılmış tooa ikincil veri merkezine tooenable yük devretme içeriktir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-236">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover if a major disaster occurs in hello primary location.</span></span> <span data-ttu-id="e0f3e-237">Coğrafi çoğaltma ek ücretlere neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-237">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="e0f3e-238">Test ve geliştirme hesaplarında genellikle coğrafi çoğaltma için toopay istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-238">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="e0f3e-239">Daha fazla bilgi için bkz. [Depolama hesabı oluşturma, yönetme veya silme](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e0f3e-239">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>

5. <span data-ttu-id="e0f3e-240">Merhaba, **kaynak grubu**, tıklatın **var olanı kullan** ve hello bulut hizmeti için kullanılan select hello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-240">In hello **Resource group**, click **Use existing** and select hello resource group used for hello cloud service.</span></span>
6. <span data-ttu-id="e0f3e-241">Set hello **konumu** aşağı açılan liste toohello hello bulut hizmeti için seçtiğiniz aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-241">Set hello **Location** drop-down list toohello same region you chose for hello cloud service.</span></span>

    <span data-ttu-id="e0f3e-242">Merhaba bulut hizmeti ve depolama hesabı farklı veri merkezlerinde olduğunda (farklı bölgelerde) gecikme artar ve, hello veri merkezinin dışındaki bant genişliği için sizden ücret alınır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-242">When hello cloud service and storage account are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside hello data center.</span></span> <span data-ttu-id="e0f3e-243">Bir veri merkezi içinde bant genişliği ücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-243">Bandwidth within a data center is free.</span></span>

    <span data-ttu-id="e0f3e-244">Azure benzeşim grupları mekanizmasını toominimize hello uzaklığı gecikme süresini azaltmak bir veri merkezindeki kaynaklarına arasında sağlar.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-244">Azure affinity groups provide a mechanism toominimize hello distance between resources in a data center, which can reduce latency.</span></span> <span data-ttu-id="e0f3e-245">Bu öğretici benzeşim gruplarını kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-245">This tutorial does not use affinity groups.</span></span> <span data-ttu-id="e0f3e-246">Daha fazla bilgi için bkz: [nasıl tooCreate benzeşim grubunda Azure'da](http://msdn.microsoft.com/library/jj156209.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0f3e-246">For more information, see [How tooCreate an Affinity Group in Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span></span>
7. <span data-ttu-id="e0f3e-247">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-247">Click **Create**.</span></span>

    ![Yeni depolama hesabı](./media/cloud-services-dotnet-get-started/newstorage.png)

    <span data-ttu-id="e0f3e-249">Merhaba görüntüde hello URL ile bir depolama hesabı oluşturulur `csvccontosoads.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-249">In hello image, a storage account is created with hello URL `csvccontosoads.core.windows.net`.</span></span>

### <a name="configure-hello-solution-toouse-your-azure-sql-database-when-it-runs-in-azure"></a><span data-ttu-id="e0f3e-250">Azure'da çalıştığında Azure SQL veritabanınızı hello çözüm toouse yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e0f3e-250">Configure hello solution toouse your Azure SQL database when it runs in Azure</span></span>
<span data-ttu-id="e0f3e-251">Web projesi hello hello çalışan rolü projesi her kendi veritabanı bağlantı dizesi içeriyor ve hello uygulama Azure'da çalıştırıldığında her toopoint toohello Azure SQL veritabanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-251">hello web project and hello worker role project each has its own database connection string, and each needs toopoint toohello Azure SQL database when hello app runs in Azure.</span></span>

<span data-ttu-id="e0f3e-252">Kullanacağınız bir [Web.config dönüştürmesi](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) hello web rolü ve bir bulut hizmet ortamı ayarı hello çalışan rolü için.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-252">You'll use a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) for hello web role and a cloud service environment setting for hello worker role.</span></span>

> [!NOTE]
> <span data-ttu-id="e0f3e-253">Bu bölüm ve hello sonraki bölümde kimlik bilgilerini proje dosyalarına depolar.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-253">In this section and hello next section, you store credentials in project files.</span></span> <span data-ttu-id="e0f3e-254">[Hassas verileri ortak kaynak kodu depolarına kaydetmeyin](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="e0f3e-254">[Don't store sensitive data in public source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span>
>
>

1. <span data-ttu-id="e0f3e-255">Merhaba ContosoAdsWeb projesinde hello açmak *Web.Release.config* Merhaba uygulaması dönüşüm dosyasını *Web.config* dosya, içeren hello açıklama bloğunu silin bir `<connectionStrings>` öğesi ve Yapıştır onun yerine koddan hello.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-255">In hello ContosoAdsWeb project, open hello *Web.Release.config* transform file for hello application *Web.config* file, delete hello comment block that contains a `<connectionStrings>` element, and paste hello following code in its place.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    <span data-ttu-id="e0f3e-256">Merhaba dosyasını düzenlemek için açık bırakın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-256">Leave hello file open for editing.</span></span>
2. <span data-ttu-id="e0f3e-257">Merhaba, [Azure portal](https://portal.azure.com), tıklatın **SQL veritabanları** hello sol bölmesinde, Bu öğretici için oluşturduğunuz hello veritabanı'nı tıklatın ve ardından **bağlantı dizelerini Göster**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-257">In hello [Azure portal](https://portal.azure.com), click **SQL Databases** in hello left pane, click hello database you created for this tutorial, and then click **Show connection strings**.</span></span>

    ![Bağlantı dizelerini göster](./media/cloud-services-dotnet-get-started/showcs.png)

    <span data-ttu-id="e0f3e-259">Merhaba portal hello parola için bir yer tutucu bağlantı dizeleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-259">hello portal displays connection strings, with a placeholder for hello password.</span></span>

    ![Bağlantı dizeleri](./media/cloud-services-dotnet-get-started/connstrings.png)
3. <span data-ttu-id="e0f3e-261">Merhaba, *Web.Release.config* dönüşüm dosyasında, silme `{connectionstring}` ve onun yerine hello hello Azure portalındaki ADO.NET bağlantı dizesini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-261">In hello *Web.Release.config* transform file, delete `{connectionstring}` and paste in its place hello ADO.NET connection string from hello Azure portal.</span></span>
4. <span data-ttu-id="e0f3e-262">Merhaba yapıştırdığınız bağlantı dizesinde hello *Web.Release.config* dönüşüm dosyasında, yerine `{your_password_here}` hello yeni SQL veritabanı için oluşturduğunuz hello parola ile.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-262">In hello connection string that you pasted into hello *Web.Release.config* transform file, replace `{your_password_here}` with hello password you created for hello new SQL database.</span></span>
5. <span data-ttu-id="e0f3e-263">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-263">Save hello file.</span></span>  
6. <span data-ttu-id="e0f3e-264">Seçin ve aşağıdaki hello çalışan rolü projesi yapılandırma adımları hello kullanmak için (tırnak işaretleri çevreleyen hello) hello bağlantı dizesini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-264">Select and copy hello connection string (without hello surrounding quotation marks) for use in hello following steps for configuring hello worker role project.</span></span>
7. <span data-ttu-id="e0f3e-265">İçinde **Çözüm Gezgini**altında **rolleri** hello bulut hizmeti projesini sağ **ContosoAdsWorker** ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-265">In **Solution Explorer**, under **Roles** in hello cloud service project, right-click **ContosoAdsWorker** and then click **Properties**.</span></span>

    ![Rol özellikleri](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. <span data-ttu-id="e0f3e-267">Merhaba tıklatın **ayarları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-267">Click hello **Settings** tab.</span></span>
9. <span data-ttu-id="e0f3e-268">Değişiklik **hizmet yapılandırmasını** çok**bulut**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-268">Change **Service Configuration** too**Cloud**.</span></span>
10. <span data-ttu-id="e0f3e-269">Select hello **değeri** hello alanındaki `ContosoAdsDbConnectionString` ayarlama ve hello önceki bölümden hello öğreticinin kopyaladığınız hello bağlantı dizesini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-269">Select hello **Value** field for hello `ContosoAdsDbConnectionString` setting, and then paste hello connection string that you copied from hello previous section of hello tutorial.</span></span>

     ![Çalışan rolü için veritabanı bağlantı dizesi](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. <span data-ttu-id="e0f3e-271">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-271">Save your changes.</span></span>  

### <a name="configure-hello-solution-toouse-your-azure-storage-account-when-it-runs-in-azure"></a><span data-ttu-id="e0f3e-272">Azure içinde çalıştığında Azure storage hesabınızı hello çözüm toouse yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e0f3e-272">Configure hello solution toouse your Azure storage account when it runs in Azure</span></span>
<span data-ttu-id="e0f3e-273">Azure depolama hesabı bağlantı dizeleri hello web rolü projesinin hem hello çalışan rolü projesi hello bulut hizmeti projesindeki ortam ayarlarına depolanır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-273">Azure storage account connection strings for both hello web role project and hello worker role project are stored in environment settings in hello cloud service project.</span></span> <span data-ttu-id="e0f3e-274">Her proje için hello bulutta çalıştığında ve hello uygulama yerel olarak çalıştığında kullanılan ayarları toobe ayrı bir dizi yoktur.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-274">For each project, there is a separate set of settings toobe used when hello application runs locally and when it runs in hello cloud.</span></span> <span data-ttu-id="e0f3e-275">Web ve çalışan rolü projeleri için hello bulut ortamı ayarlarını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-275">You'll update hello cloud environment settings for both web and worker role projects.</span></span>

1. <span data-ttu-id="e0f3e-276">İçinde **Çözüm Gezgini**, sağ **ContosoAdsWeb** altında **rolleri** hello içinde **ContosoAdsCloudService** proje ve ardından **Özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-276">In **Solution Explorer**, right-click **ContosoAdsWeb** under **Roles** in hello **ContosoAdsCloudService** project, and then click **Properties**.</span></span>

    ![Rol özellikleri](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. <span data-ttu-id="e0f3e-278">Merhaba tıklatın **ayarları** sekmesi. Merhaba, **hizmet yapılandırmasını** açılır kutusunda, seçin **bulut**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-278">Click hello **Settings** tab. In hello **Service Configuration** drop-down box, choose **Cloud**.</span></span>

    ![Bulut yapılandırması](./media/cloud-services-dotnet-get-started/sccloud.png)
3. <span data-ttu-id="e0f3e-280">Select hello **StorageConnectionString** girişi ve üç nokta göreceksiniz (**...** ) düğmesini hello sağ ucunda hello satır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-280">Select hello **StorageConnectionString** entry, and you'll see an ellipsis (**...**) button at hello right end of hello line.</span></span> <span data-ttu-id="e0f3e-281">Merhaba üç nokta düğmesini tooopen hello tıklatın **depolama hesabı bağlantı dizesi oluştur** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-281">Click hello ellipsis button tooopen hello **Create Storage Account Connection String** dialog box.</span></span>

    ![Bağlantı Dizesi Oluştur kutusunu açma](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. <span data-ttu-id="e0f3e-283">Merhaba, **depolama bağlantı dizesi oluştur** iletişim kutusu, tıklatın **aboneliğinizi**, daha önce oluşturduğunuz hello depolama hesabını seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-283">In hello **Create Storage Connection String** dialog box, click **Your subscription**, choose hello storage account that you created earlier, and then click **OK**.</span></span> <span data-ttu-id="e0f3e-284">Henüz oturum açmadıysanız Azure hesabı kimlik bilgileriniz istenir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-284">If you're not already logged in, you'll be prompted for your Azure account credentials.</span></span>

    ![Depolama Bağlantı Dizesi oluşturma](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. <span data-ttu-id="e0f3e-286">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-286">Save your changes.</span></span>
6. <span data-ttu-id="e0f3e-287">İzleme hello aynı hello için kullandığınız yordam `StorageConnectionString` bağlantı dizesi tooset hello `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-287">Follow hello same procedure that you used for hello `StorageConnectionString` connection string tooset hello `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` connection string.</span></span>

    <span data-ttu-id="e0f3e-288">Bu bağlantı dizesi günlüğe kaydetme için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-288">This connection string is used for logging.</span></span>
7. <span data-ttu-id="e0f3e-289">İzleme hello aynı hello için kullandığınız yordam **ContosoAdsWeb** rol tooset Merhaba için iki bağlantı dizesini **ContosoAdsWorker** rol.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-289">Follow hello same procedure that you used for hello **ContosoAdsWeb** role tooset both connection strings for hello **ContosoAdsWorker** role.</span></span> <span data-ttu-id="e0f3e-290">Tooset unutmayın **hizmet yapılandırmasını** çok**bulut**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-290">Don't forget tooset **Service Configuration** too**Cloud**.</span></span>

<span data-ttu-id="e0f3e-291">hello hello Visual Studio kullanıcı arabirimini kullanılarak yapılandırdığınız rol ortamı ayarları aşağıdaki dosyaları hello ContosoAdsCloudService projesinde hello depolanır:</span><span class="sxs-lookup"><span data-stu-id="e0f3e-291">hello role environment settings that you have configured using hello Visual Studio UI are stored in hello following files in hello ContosoAdsCloudService project:</span></span>

* <span data-ttu-id="e0f3e-292">*ServiceDefinition.csdef* -hello ayar adlarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-292">*ServiceDefinition.csdef* - Defines hello setting names.</span></span>
* <span data-ttu-id="e0f3e-293">*ServiceConfiguration.Cloud.cscfg* -hello uygulama hello bulutta çalıştığında için değerler sağlar.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-293">*ServiceConfiguration.Cloud.cscfg* - Provides values for when hello app runs in hello cloud.</span></span>
* <span data-ttu-id="e0f3e-294">*ServiceConfiguration.Local.cscfg* -hello uygulama yerel olarak çalıştığında için değerler sağlar.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-294">*ServiceConfiguration.Local.cscfg* - Provides values for when hello app runs locally.</span></span>

<span data-ttu-id="e0f3e-295">Örneğin, hello ServiceDefinition.csdef aşağıdaki tanımları hello içerir:</span><span class="sxs-lookup"><span data-stu-id="e0f3e-295">For example, hello ServiceDefinition.csdef includes hello following definitions:</span></span>

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

<span data-ttu-id="e0f3e-296">Ve hello *ServiceConfiguration.Cloud.cscfg* dosyası, Visual Studio'da bu ayarlar için girdiğiniz hello değerleri içerir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-296">And hello *ServiceConfiguration.Cloud.cscfg* file includes hello values you entered for those settings in Visual Studio.</span></span>

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

<span data-ttu-id="e0f3e-297">Merhaba `<Instances>` ayar Azure hello çalışan rolü kodunu çalıştıracağı sanal makine hello sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-297">hello `<Instances>` setting specifies hello number of virtual machines that Azure will run hello worker role code on.</span></span> <span data-ttu-id="e0f3e-298">Merhaba [sonraki adımlar](#next-steps) bölümünde bir bulut hizmetinin ölçeklendirme hakkında bağlantılar toomore bilgileri içerir</span><span class="sxs-lookup"><span data-stu-id="e0f3e-298">hello [Next steps](#next-steps) section includes links toomore information about scaling out a cloud service,</span></span>

### <a name="deploy-hello-project-tooazure"></a><span data-ttu-id="e0f3e-299">Merhaba proje tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="e0f3e-299">Deploy hello project tooAzure</span></span>
1. <span data-ttu-id="e0f3e-300">İçinde **Çözüm Gezgini**, sağ hello **ContosoAdsCloudService** bulut projesine ve ardından **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-300">In **Solution Explorer**, right-click hello **ContosoAdsCloudService** cloud project and then select **Publish**.</span></span>

   ![Yayımla menüsü](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. <span data-ttu-id="e0f3e-302">Merhaba, **oturum** hello adımında **Azure uygulamasını Yayımla** Sihirbazı'nı tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-302">In hello **Sign in** step of hello **Publish Azure Application** wizard, click **Next**.</span></span>

    ![Oturum açma adımı](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. <span data-ttu-id="e0f3e-304">Merhaba, **ayarları** adım hello Sihirbazı'nın tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-304">In hello **Settings** step of hello wizard, click **Next**.</span></span>

    ![Ayarlar adımı](./media/cloud-services-dotnet-get-started/pubsettings.png)

    <span data-ttu-id="e0f3e-306">Merhaba hello varsayılan ayarlarında **Gelişmiş** sekmesinde Bu öğretici için uygundur.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-306">hello default settings in hello **Advanced** tab are fine for this tutorial.</span></span> <span data-ttu-id="e0f3e-307">Merhaba Gelişmiş sekmesi hakkında daha fazla bilgi için bkz: [Azure uygulaması Yayımlama Sihirbazı](http://msdn.microsoft.com/library/hh535756.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0f3e-307">For information about hello advanced tab, see [Publish Azure Application Wizard](http://msdn.microsoft.com/library/hh535756.aspx).</span></span>
4. <span data-ttu-id="e0f3e-308">Merhaba, **Özet** adımını, **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-308">In hello **Summary** step, click **Publish**.</span></span>

    ![Özet adımı](./media/cloud-services-dotnet-get-started/pubsummary.png)

   <span data-ttu-id="e0f3e-310">Merhaba **Azure etkinlik günlüğü** Visual Studio'da penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-310">hello **Azure Activity Log** window opens in Visual Studio.</span></span>
5. <span data-ttu-id="e0f3e-311">Merhaba sağ ok simgesine tooexpand hello dağıtım Ayrıntılar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-311">Click hello right arrow icon tooexpand hello deployment details.</span></span>

    <span data-ttu-id="e0f3e-312">Merhaba dağıtım too5 dakika veya daha fazla toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-312">hello deployment can take up too5 minutes or more toocomplete.</span></span>

    ![Azure Etkinlik Günlüğü penceresi](./media/cloud-services-dotnet-get-started/waal.png)
6. <span data-ttu-id="e0f3e-314">Merhaba dağıtım durumu tamamlandığında hello tıklatın **Web uygulaması URL'si** toostart Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-314">When hello deployment status is complete, click hello **Web app URL** toostart hello application.</span></span>
7. <span data-ttu-id="e0f3e-315">Merhaba uygulamayı yerel olarak çalıştırdığınızda yaptığınız gibi hello uygulama oluşturma, görüntüleme ve bazı ads düzenleme artık test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-315">You can now test hello app by creating, viewing, and editing some ads, as you did when you ran hello application locally.</span></span>

> [!NOTE]
> <span data-ttu-id="e0f3e-316">Ne zaman sınama, silmek veya Dur hello bulut hizmeti bitti.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-316">When you're finished testing, delete or stop hello cloud service.</span></span> <span data-ttu-id="e0f3e-317">Merhaba bulut hizmeti kullanmıyorsanız bile, sanal makine kaynakları için ayrılmış olduğundan ücretler tahakkuk eder.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-317">Even if you're not using hello cloud service, it's accruing charges because virtual machine resources are reserved for it.</span></span> <span data-ttu-id="e0f3e-318">Ayrıca çalışır durumda bırakırsanız, URL’nizi bulan herhangi bir kişi reklam oluşturabilir ve görüntüleyebilir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-318">And if you leave it running, anyone who finds your URL can create and view ads.</span></span> <span data-ttu-id="e0f3e-319">Merhaba, [Azure portal](https://portal.azure.com), Git toohello **genel bakış** bulut hizmetiniz için sekmesini ve sonra hello **silmek** hello sayfanın üst kısmındaki hello düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-319">In hello [Azure portal](https://portal.azure.com), go toohello **Overview** tab for your cloud service, and then click hello **Delete** button at hello top of hello page.</span></span> <span data-ttu-id="e0f3e-320">Yalnızca istiyorsanız tootemporarily önlemek başkalarının hello siteye erişmesini, tıklatın **durdurmak** yerine.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-320">If you just want tootemporarily prevent others from accessing hello site, click **Stop** instead.</span></span> <span data-ttu-id="e0f3e-321">Bu durumda ücretler tooaccrue devam eder.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-321">In that case, charges will continue tooaccrue.</span></span> <span data-ttu-id="e0f3e-322">Artık gereksinim duyduğunuzda, benzer bir yordamı toodelete hello SQL veritabanı ve depolama hesabı izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-322">You can follow a similar procedure toodelete hello SQL database and storage account when you no longer need them.</span></span>
>
>

## <a name="create-hello-application-from-scratch"></a><span data-ttu-id="e0f3e-323">Merhaba uygulamayı sıfırdan oluşturma</span><span class="sxs-lookup"><span data-stu-id="e0f3e-323">Create hello application from scratch</span></span>
<span data-ttu-id="e0f3e-324">Zaten indirmediyseniz [tamamlandı Merhaba uygulaması](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), bunu şimdi yapın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-324">If you haven't already downloaded [hello completed application](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), do that now.</span></span> <span data-ttu-id="e0f3e-325">Dosyaları hello indirilen projeden hello yeni projeye kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-325">You'll copy files from hello downloaded project into hello new project.</span></span>

<span data-ttu-id="e0f3e-326">Merhaba Contoso Ads uygulamasının oluşturulması hello aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="e0f3e-326">Creating hello Contoso Ads application involves hello following steps:</span></span>

* <span data-ttu-id="e0f3e-327">Bir bulut hizmeti Visual Studio çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-327">Create a cloud service Visual Studio solution.</span></span>
* <span data-ttu-id="e0f3e-328">NuGet paketlerini güncelleştirin ve ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-328">Update and add NuGet packages.</span></span>
* <span data-ttu-id="e0f3e-329">Proje başvurularını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-329">Set project references.</span></span>
* <span data-ttu-id="e0f3e-330">Bağlantı dizelerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-330">Configure connection strings.</span></span>
* <span data-ttu-id="e0f3e-331">Kod dosyaları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-331">Add code files.</span></span>

<span data-ttu-id="e0f3e-332">Merhaba çözüm oluşturulduktan sonra benzersiz toocloud hizmeti projeleri ve Azure BLOB'ları ve kuyrukları hello kodu gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-332">After hello solution is created, you'll review hello code that is unique toocloud service projects and Azure blobs and queues.</span></span>

### <a name="create-a-cloud-service-visual-studio-solution"></a><span data-ttu-id="e0f3e-333">Bir bulut hizmeti Visual Studio çözümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="e0f3e-333">Create a cloud service Visual Studio solution</span></span>
1. <span data-ttu-id="e0f3e-334">Visual Studio'da, **yeni proje** hello gelen **dosya** menüsü.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-334">In Visual Studio, choose **New Project** from hello **File** menu.</span></span>
2. <span data-ttu-id="e0f3e-335">Hello sol bölmesinde hello **yeni proje** iletişim kutusunda, genişletin **Visual C#** ve seçin **bulut** şablonları ve ardından hello **Azure bulut hizmeti** şablonu.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-335">In hello left pane of hello **New Project** dialog box, expand **Visual C#** and choose **Cloud** templates, and then choose hello **Azure Cloud Service** template.</span></span>
3. <span data-ttu-id="e0f3e-336">Merhaba projeyi ve çözümü ContosoAdsCloudService olarak adlandırın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-336">Name hello project and solution ContosoAdsCloudService, and then click **OK**.</span></span>

    ![Yeni Proje](./media/cloud-services-dotnet-get-started/newproject.png)
4. <span data-ttu-id="e0f3e-338">Merhaba, **yeni Azure bulut hizmeti** iletişim kutusunda, web rolü ve çalışan rolü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-338">In hello **New Azure Cloud Service** dialog box, add a web role and a worker role.</span></span> <span data-ttu-id="e0f3e-339">Merhaba web rolünü ContosoAdsWeb ve hello çalışan rolünü ContosoAdsWorker olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-339">Name hello web role ContosoAdsWeb, and name hello worker role ContosoAdsWorker.</span></span> <span data-ttu-id="e0f3e-340">(Merhaba kalem simgesine hello sağ bölmedeki toochange hello varsayılan adlarında hello rollerin kullanın.)</span><span class="sxs-lookup"><span data-stu-id="e0f3e-340">(Use hello pencil icon in hello right-hand pane toochange hello default names of hello roles.)</span></span>

    ![Yeni Bulut Hizmeti Projesi](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. <span data-ttu-id="e0f3e-342">Merhaba gördüğünüzde **yeni ASP.NET projesi** hello web rolü için iletişim kutusu hello MVC şablonunu seçin ve ardından **kimlik doğrulamayı Değiştir**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-342">When you see hello **New ASP.NET Project** dialog box for hello web role, choose hello MVC template, and then click **Change Authentication**.</span></span>

    ![Kimlik Doğrulamayı Değiştirme](./media/cloud-services-dotnet-get-started/chgauth.png)
6. <span data-ttu-id="e0f3e-344">Merhaba, **kimlik doğrulamayı Değiştir** iletişim kutusunda, seçin **doğrulaması yok**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-344">In hello **Change Authentication** dialog box, choose **No Authentication**, and then click **OK**.</span></span>

    ![Kimlik Doğrulaması Yok](./media/cloud-services-dotnet-get-started/noauth.png)
7. <span data-ttu-id="e0f3e-346">Merhaba, **yeni ASP.NET projesi** iletişim kutusunda, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-346">In hello **New ASP.NET Project** dialog, click **OK**.</span></span>
8. <span data-ttu-id="e0f3e-347">İçinde **Çözüm Gezgini**hello çözümü (değil hello projelerden biri) sağ tıklatın ve seçin **Ekle - yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-347">In **Solution Explorer**, right-click hello solution (not one of hello projects), and choose **Add - New Project**.</span></span>
9. <span data-ttu-id="e0f3e-348">Merhaba, **Yeni Proje Ekle** iletişim kutusunda, seçin **Windows** altında **Visual C#** hello sol bölmesinde ve hello ardından **sınıf kitaplığı** Şablon.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-348">In hello **Add New Project** dialog box, choose **Windows** under **Visual C#** in hello left pane, and then click hello **Class Library** template.</span></span>  
10. <span data-ttu-id="e0f3e-349">Ad hello proje *ContosoAdsCommon*ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-349">Name hello project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="e0f3e-350">Tooreference hello Entity Framework bağlamını ve hello veri modeli web ve çalışan rolü projelerindeki gerekir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-350">You need tooreference hello Entity Framework context and hello data model from both web and worker role projects.</span></span> <span data-ttu-id="e0f3e-351">Alternatif olarak, hello web rolü projesinde EF ile ilgili sınıflar hello tanımlayın ve hello çalışan rolü projesinde bu projeye başvuruda.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-351">As an alternative, you could define hello EF-related classes in hello web role project and reference that project from hello worker role project.</span></span> <span data-ttu-id="e0f3e-352">Ancak hello alternatif yaklaşımda çalışan rolü projeniz gerekli olmayan bir başvuru tooweb derlemeleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-352">But in hello alternative approach, your worker role project would have a reference tooweb assemblies that it doesn't need.</span></span>

### <a name="update-and-add-nuget-packages"></a><span data-ttu-id="e0f3e-353">NuGet paketlerini güncelleştirme ve ekleme</span><span class="sxs-lookup"><span data-stu-id="e0f3e-353">Update and add NuGet packages</span></span>
1. <span data-ttu-id="e0f3e-354">Açık hello **NuGet paketlerini Yönet** hello çözüm için iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-354">Open hello **Manage NuGet Packages** dialog box for hello solution.</span></span>
2. <span data-ttu-id="e0f3e-355">Merhaba penceresinin Hello üstünde seçin **güncelleştirmeleri**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-355">At hello top of hello window, select **Updates**.</span></span>
3. <span data-ttu-id="e0f3e-356">Merhaba Ara *WindowsAzure.Storage* paketini ve hello listesinde olması durumunda onu seçip hello web ve çalışan projelerini tooupdate içinde ve ardından **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-356">Look for hello *WindowsAzure.Storage* package, and if it's in hello list, select it and select hello web and worker projects tooupdate it in, and then click **Update**.</span></span>

    <span data-ttu-id="e0f3e-357">Merhaba sürümünün güncelleştirilmiş yeni oluşturulan proje gereksinimlerini toobe içinde sık sık görürsünüz hello depolama istemcisi Kitaplığı Visual Studio proje şablonlarından daha sık güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-357">hello storage client library is updated more frequently than Visual Studio project templates, so you'll often find that hello version in a newly-created project needs toobe updated.</span></span>
4. <span data-ttu-id="e0f3e-358">Merhaba penceresinin Hello üstünde seçin **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-358">At hello top of hello window, select **Browse**.</span></span>
5. <span data-ttu-id="e0f3e-359">Hello bulur *EntityFramework* NuGet paketini bulun ve üç projenin tamamına yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-359">Find hello *EntityFramework* NuGet package, and install it in all three projects.</span></span>
6. <span data-ttu-id="e0f3e-360">Hello bulur *Microsoft.WindowsAzure.ConfigurationManager* NuGet paketini ve hello çalışan rolü projesine yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-360">Find hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet package, and install it in hello worker role project.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="e0f3e-361">Proje başvurularını ayarlama</span><span class="sxs-lookup"><span data-stu-id="e0f3e-361">Set project references</span></span>
1. <span data-ttu-id="e0f3e-362">Merhaba ContosoAdsWeb projesinde bir başvuru toohello ContosoAdsCommon projesine ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-362">In hello ContosoAdsWeb project, set a reference toohello ContosoAdsCommon project.</span></span> <span data-ttu-id="e0f3e-363">Merhaba ContosoAdsWeb projesine sağ tıklayın ve ardından **başvuruları** - **Başvuru Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-363">Right-click hello ContosoAdsWeb project, and then click **References** - **Add References**.</span></span> <span data-ttu-id="e0f3e-364">Merhaba, **başvuru Yöneticisi** iletişim kutusunda **çözüm – projeler** hello sol bölmesinde seçin **ContosoAdsCommon**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-364">In hello **Reference Manager** dialog box, select **Solution – Projects** in hello left pane, select **ContosoAdsCommon**, and then click **OK**.</span></span>
2. <span data-ttu-id="e0f3e-365">Merhaba ContosoAdsWorker projesinde bir başvuru toohello Contosoadscommon projesine ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-365">In hello ContosoAdsWorker project, set a reference toohello ContosAdsCommon project.</span></span>

    <span data-ttu-id="e0f3e-366">ContosoAdsCommon hem hello ön uç ve arka uç tarafından kullanılacak olan hello Entity Framework veri modeli ve bağlam sınıfını içerir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-366">ContosoAdsCommon will contain hello Entity Framework data model and context class, which will be used by both hello front-end and back-end.</span></span>
3. <span data-ttu-id="e0f3e-367">Merhaba ContosoAdsWorker projesinde bir başvuru çok ayarlayın`System.Drawing`.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-367">In hello ContosoAdsWorker project, set a reference too`System.Drawing`.</span></span>

    <span data-ttu-id="e0f3e-368">Bu derleme hello arka uç tooconvert görüntüleri toothumbnails tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-368">This assembly is used by hello back-end tooconvert images toothumbnails.</span></span>

### <a name="configure-connection-strings"></a><span data-ttu-id="e0f3e-369">Bağlantı dizelerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e0f3e-369">Configure connection strings</span></span>
<span data-ttu-id="e0f3e-370">Bu bölümde, yerel olarak test etmek amacıyla Azure Storage ve SQL bağlantı dizelerini yapılandırırsınız.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-370">In this section, you configure Azure Storage and SQL connection strings for testing locally.</span></span> <span data-ttu-id="e0f3e-371">Başlangıç Öğreticisi dağıtım yönergeleri Hello hello uygulama hello bulutta çalıştığında nasıl tooset hello bağlantı kurmak için dizeleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-371">hello deployment instructions earlier in hello tutorial explain how tooset up hello connection strings for when hello app runs in hello cloud.</span></span>

1. <span data-ttu-id="e0f3e-372">Merhaba ContosoAdsWeb projesine, açık hello uygulamanın Web.config dosyasını ve INSERT hello aşağıdaki `connectionStrings` öğeden sonra hello `configSections` öğesi.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-372">In hello ContosoAdsWeb project, open hello application Web.config file, and insert hello following `connectionStrings` element after hello `configSections` element.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="e0f3e-373">Visual Studio 2015 ve sonraki bir sürümü kullanıyorsanız "v11.0" ifadesini "MSSQLLocalDB" ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-373">If you're using Visual Studio 2015 or higher, replace "v11.0" with "MSSQLLocalDB".</span></span>
2. <span data-ttu-id="e0f3e-374">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-374">Save your changes.</span></span>
3. <span data-ttu-id="e0f3e-375">Merhaba ContosoAdsCloudService projesinde altındaki ContosoAdsWeb sağ **rolleri**ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-375">In hello ContosoAdsCloudService project, right-click ContosoAdsWeb under **Roles**, and then click **Properties**.</span></span>

    ![Rol özellikleri](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. <span data-ttu-id="e0f3e-377">Merhaba, **ContosAdsWeb [rolü]** Özellikleri penceresinde hello tıklatın **ayarları** sekmesini ve ardından **ayar Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-377">In hello **ContosAdsWeb [Role]** properties window, click hello **Settings** tab, and then click **Add Setting**.</span></span>

    <span data-ttu-id="e0f3e-378">Bırakın **hizmet yapılandırmasını** çok ayarlamak**tüm yapılandırmaları**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-378">Leave **Service Configuration** set too**All Configurations**.</span></span>
5. <span data-ttu-id="e0f3e-379">*StorageConnectionString* adlı bir ayar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-379">Add a setting named *StorageConnectionString*.</span></span> <span data-ttu-id="e0f3e-380">Ayarlama **türü** çok*ConnectionString*ve **değeri** çok*UseDevelopmentStorage = true*.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-380">Set **Type** too*ConnectionString*, and set **Value** too*UseDevelopmentStorage=true*.</span></span>

    ![Yeni bağlantı dizesi](./media/cloud-services-dotnet-get-started/scall.png)
6. <span data-ttu-id="e0f3e-382">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-382">Save your changes.</span></span>
7. <span data-ttu-id="e0f3e-383">Merhaba ContosoAdsWorker rol özelliklerine bir depolama bağlantı dizesi aynı yordamı tooadd hello izleyin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-383">Follow hello same procedure tooadd a storage connection string in hello ContosoAdsWorker role properties.</span></span>
8. <span data-ttu-id="e0f3e-384">Merhaba yine de **ContosoAdsWorker [rolü]** Özellikleri penceresinde, başka bir bağlantı dizesi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e0f3e-384">Still in hello **ContosoAdsWorker [Role]** properties window, add another connection string:</span></span>

   * <span data-ttu-id="e0f3e-385">Ad: ContosoAdsDbConnectionString</span><span class="sxs-lookup"><span data-stu-id="e0f3e-385">Name: ContosoAdsDbConnectionString</span></span>
   * <span data-ttu-id="e0f3e-386">Türü: Dize</span><span class="sxs-lookup"><span data-stu-id="e0f3e-386">Type: String</span></span>
   * <span data-ttu-id="e0f3e-387">Değer: Yapıştır hello aynı hello web rolü projesi için kullanılan bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-387">Value: Paste hello same connection string you used for hello web role project.</span></span> <span data-ttu-id="e0f3e-388">(aşağıdaki örneğine hello için Visual Studio 2013 içindir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-388">(hello following example is for Visual Studio 2013.</span></span> <span data-ttu-id="e0f3e-389">Veri kaynağı toochange hello Bu örneği kopyalarsanız ve Visual Studio 2015 veya üzeri kullanıyorsanız unutmayın.)</span><span class="sxs-lookup"><span data-stu-id="e0f3e-389">Don't forget toochange hello Data Source if you copy this example and you're using Visual Studio 2015 or higher.)</span></span>

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a><span data-ttu-id="e0f3e-390">Kod dosyaları ekleme</span><span class="sxs-lookup"><span data-stu-id="e0f3e-390">Add code files</span></span>
<span data-ttu-id="e0f3e-391">Bu bölümde, kod dosyaları hello yeni çözüme hello indirilen çözümden kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-391">In this section, you copy code files from hello downloaded solution into hello new solution.</span></span> <span data-ttu-id="e0f3e-392">Merhaba aşağıdaki bölümlerde gösterilmiş ve bu kodun temel kısımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-392">hello following sections will show and explain key parts of this code.</span></span>

<span data-ttu-id="e0f3e-393">tooadd dosyalar tooa proje veya bir klasörü, sağ hello proje veya klasöre tıklatın **Ekle** - **varolan öğeyi**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-393">tooadd files tooa project or a folder, right-click hello project or folder and click **Add** - **Existing Item**.</span></span> <span data-ttu-id="e0f3e-394">İstediğiniz ve ardından hello dosyaları seçin **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-394">Select hello files you want and then click **Add**.</span></span> <span data-ttu-id="e0f3e-395">Tooreplace var olan dosyaları isteyip istemediğinizi sorulursa tıklatın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-395">If asked whether you want tooreplace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="e0f3e-396">Merhaba ContosoAdsCommon projesinde hello silmek *Class1.cs* dosya ve onun yerine hello ekleyin *Ad.cs* ve *ContosoAdscontext.cs* hello dosyalarından proje indirilir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-396">In hello ContosoAdsCommon project, delete hello *Class1.cs* file and add in its place hello *Ad.cs* and *ContosoAdscontext.cs* files from hello downloaded project.</span></span>
2. <span data-ttu-id="e0f3e-397">Merhaba ContosoAdsWeb projesinde hello hello indirilen projeden aşağıdaki dosyaları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-397">In hello ContosoAdsWeb project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="e0f3e-398">*Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-398">*Global.asax.cs*.</span></span>  
   * <span data-ttu-id="e0f3e-399">Merhaba, *görünümler/paylaşılan* klasörü:  *\_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-399">In hello *Views\Shared* folder: *\_Layout.cshtml*.</span></span>
   * <span data-ttu-id="e0f3e-400">Merhaba, *görünümler* klasörü: *Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-400">In hello *Views\Home* folder: *Index.cshtml*.</span></span>
   * <span data-ttu-id="e0f3e-401">Merhaba, *denetleyicileri* klasörü: *AdController.cs*.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-401">In hello *Controllers* folder: *AdController.cs*.</span></span>
   * <span data-ttu-id="e0f3e-402">Merhaba, *görünümler/reklam* klasörü (öncelikle hello klasörü oluşturun): beş *.cshtml* dosyaları.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-402">In hello *Views\Ad* folder (create hello folder first): five *.cshtml* files.</span></span>
3. <span data-ttu-id="e0f3e-403">Merhaba ContosoAdsWorker projesinde ekleyin *WorkerRole.cs* proje hello indirilir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-403">In hello ContosoAdsWorker project, add *WorkerRole.cs* from hello downloaded project.</span></span>

<span data-ttu-id="e0f3e-404">Artık derleme ve hello öğreticide daha önce belirtildiği gibi hello uygulamayı çalıştırın ve hello uygulama yerel veritabanı ve depolama öykünücüsü kaynaklarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-404">You can now build and run hello application as instructed earlier in hello tutorial, and hello app will use local database and storage emulator resources.</span></span>

<span data-ttu-id="e0f3e-405">Merhaba aşağıdaki bölümlerde açıklanmıştır hello kodu ile ilgili tooworking hello Azure ortamı, BLOB'ları ve kuyrukları.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-405">hello following sections explain hello code related tooworking with hello Azure environment, blobs, and queues.</span></span> <span data-ttu-id="e0f3e-406">Bu öğretici değil açıklayan nasıl toocreate MVC denetleyicileri yapı iskelesi kullanarak görünümleri nasıl toowrite Entity Framework kod çalışır SQL Server veritabanları veya ASP.NET 4.5 içinde zaman uyumsuz programlama temelleri hello.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-406">This tutorial does not explain how toocreate MVC controllers and views using scaffolding, how toowrite Entity Framework code that works with SQL Server databases, or hello basics of asynchronous programming in ASP.NET 4.5.</span></span> <span data-ttu-id="e0f3e-407">Bu konular hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="e0f3e-407">For information about these topics, see hello following resources:</span></span>

* [<span data-ttu-id="e0f3e-408">MVC 5 kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e0f3e-408">Get started with MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="e0f3e-409">EF 6 ve MVC 5 kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e0f3e-409">Get started with EF 6 and MVC 5</span></span>](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* <span data-ttu-id="e0f3e-410">[Giriş tooasynchronous .NET 4.5 programlamada](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="e0f3e-410">[Introduction tooasynchronous programming in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="e0f3e-411">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="e0f3e-411">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="e0f3e-412">Merhaba Ad.cs dosyası reklam kategorileri için bir numaralandırma ve reklam bilgileri için bir POCO varlık sınıfı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-412">hello Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

```csharp
public enum Category
{
    Cars,
    [Display(Name="Real Estate")]
    RealEstate,
    [Display(Name = "Free Stuff")]
    FreeStuff
}

public class Ad
{
    public int AdId { get; set; }

    [StringLength(100)]
    public string Title { get; set; }

    public int Price { get; set; }

    [StringLength(1000)]
    [DataType(DataType.MultilineText)]
    public string Description { get; set; }

    [StringLength(1000)]
    [DisplayName("Full-size Image")]
    public string ImageURL { get; set; }

    [StringLength(1000)]
    [DisplayName("Thumbnail")]
    public string ThumbnailURL { get; set; }

    [DataType(DataType.Date)]
    [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
    public DateTime PostedDate { get; set; }

    public Category? Category { get; set; }
    [StringLength(12)]
    public string Phone { get; set; }
}
```

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="e0f3e-413">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="e0f3e-413">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="e0f3e-414">Merhaba ContosoAdsContext sınıfı hello reklam sınıfının Entity Framework bir SQL veritabanına depolanacak bir DbSet koleksiyonunda kullanıldığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-414">hello ContosoAdsContext class specifies that hello Ad class is used in a DbSet collection, which Entity Framework will store in a SQL database.</span></span>

```csharp
public class ContosoAdsContext : DbContext
{
    public ContosoAdsContext() : base("name=ContosoAdsContext")
    {
    }
    public ContosoAdsContext(string connString)
        : base(connString)
    {
    }
    public System.Data.Entity.DbSet<Ad> Ads { get; set; }
}
```

<span data-ttu-id="e0f3e-415">Merhaba sınıfın iki Oluşturucusu vardır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-415">hello class has two constructors.</span></span> <span data-ttu-id="e0f3e-416">ilk hello bunları hello web projesi tarafından kullanılır ve hello hello Web.config dosyasında saklanan bir bağlantı dizesinin adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-416">hello first of them is used by hello web project, and specifies hello name of a connection string that is stored in hello Web.config file.</span></span> <span data-ttu-id="e0f3e-417">Merhaba ikinci oluşturucu bir Web.config dosyası olmadığından hello çalışan rolü projesi tarafından kullanılan hello gerçek bağlantı dizesine toopass sağlar.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-417">hello second constructor enables you toopass in hello actual connection string used by hello worker role project, since it doesn't have a Web.config file.</span></span> <span data-ttu-id="e0f3e-418">Daha önce gördüğünüzle burada Bu bağlantı dizesi depolanır ve daha sonra nasıl hello DbContext sınıfını başlattığında hello kodu hello bağlantı dizesini alır görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-418">You saw earlier where this connection string was stored, and you'll see later how hello code retrieves hello connection string when it instantiates hello DbContext class.</span></span>

### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="e0f3e-419">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="e0f3e-419">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="e0f3e-420">Hello adlı kod `Application_Start` yöntemi oluşturur bir *görüntüleri* blob kapsayıcısı ve bir *görüntüleri* henüz yoksa sıra.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-420">Code that is called from hello `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="e0f3e-421">Bu, yeni bir depolama hesabı kullanmaya başlamak ya da hello depolama öykünücüsünü yeni bir bilgisayarda kullanmaya başladığınız her hello gerekli blob kapsayıcısının ve kuyruğun otomatik olarak oluşturulmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-421">This ensures that whenever you start using a new storage account, or start using hello storage emulator on a new computer, hello required blob container and queue will be created automatically.</span></span>

<span data-ttu-id="e0f3e-422">Merhaba kod alır erişim toohello depolama hesabı hello hello depolama bağlantı dizesini kullanarak *.cscfg* dosya.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-422">hello code gets access toohello storage account by using hello storage connection string from hello *.cscfg* file.</span></span>

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

<span data-ttu-id="e0f3e-423">Bir başvuru toohello alır sonra *görüntüleri* blob kapsayıcısı, önceden var olmayan ve erişim izinlerini hello yeni kapsayıcı ayarlar hello kapsayıcı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-423">Then it gets a reference toohello *images* blob container, creates hello container if it doesn't already exist, and sets access permissions on hello new container.</span></span> <span data-ttu-id="e0f3e-424">Varsayılan olarak, yeni kapsayıcılar yalnızca depolama hesabı istemcileriyle kimlik bilgilerini tooaccess BLOB'lar izin verir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-424">By default, new containers only allow clients with storage account credentials tooaccess blobs.</span></span> <span data-ttu-id="e0f3e-425">Bu nokta toohello görüntü BLOB'larını URL'leri kullanarak görüntüleri gösterebilmek hello Web sitesi BLOB'lar toobe ortak hello.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-425">hello website needs hello blobs toobe public so that it can display images using URLs that point toohello image blobs.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

<span data-ttu-id="e0f3e-426">Benzer bir kod alır başvuru toohello *görüntüleri* sıraya almak ve yeni bir sıra oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-426">Similar code gets a reference toohello *images* queue and creates a new queue.</span></span> <span data-ttu-id="e0f3e-427">Bu durumda hiçbir izin değişikliğine gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-427">In this case, no permissions change is needed.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="e0f3e-428">ContosoAdsWeb - \_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="e0f3e-428">ContosoAdsWeb - \_Layout.cshtml</span></span>
<span data-ttu-id="e0f3e-429">Merhaba *_Layout.cshtml* dosya hello üstbilgi ve altbilgi hello uygulama adını ayarlar ve bir "Reklamlar" menü girişi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-429">hello *_Layout.cshtml* file sets hello app name in hello header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="e0f3e-430">ContosoAdsWeb - Görünümler\Giriş\Dizin.cshtml</span><span class="sxs-lookup"><span data-stu-id="e0f3e-430">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="e0f3e-431">Merhaba *Views\Home\Index.cshtml* dosya hello giriş sayfasında kategori bağlantılarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-431">hello *Views\Home\Index.cshtml* file displays category links on hello home page.</span></span> <span data-ttu-id="e0f3e-432">Merhaba bağlantılar geçirmek hello hello tamsayı değeri `Category` enum bir sorgu dizesi değişkeni toohello reklam dizini sayfasına içindeki.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-432">hello links pass hello integer value of hello `Category` enum in a querystring variable toohello Ads Index page.</span></span>

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="e0f3e-433">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="e0f3e-433">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="e0f3e-434">Merhaba, *AdController.cs* dosya, hello Oluşturucusu çağrıları hello `InitializeStorage` BLOB'lar ve kuyruklarla çalışmaya yönelik bir API sağlayan yöntemi toocreate Azure Storage istemci Kitaplığı nesneleri.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-434">In hello *AdController.cs* file, hello constructor calls hello `InitializeStorage` method toocreate Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="e0f3e-435">Bir başvuru toohello Hello kodu alır sonra *görüntüleri* daha önce gördüğünüz gibi blob kapsayıcısı *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-435">Then hello code gets a reference toohello *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="e0f3e-436">Bunu yaparken bir web uygulaması için uygun bir varsayılan [yeniden deneme ilkesi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-436">While doing that it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="e0f3e-437">Merhaba varsayılan üstel geri alma yeniden deneme ilkesi hello web uygulaması için geçici bir hata için tekrarlanan yeniden denemelerde bir dakikadan uzun süre askıya alabilir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-437">hello default exponential backoff retry policy could hang hello web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="e0f3e-438">Burada belirtilen hello yeniden deneme ilkesi üç her denemeden sonra toothree çalıştığında saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-438">hello retry policy specified here waits three seconds after each try for up toothree tries.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

<span data-ttu-id="e0f3e-439">Benzer bir kod alır başvuru toohello *görüntüleri* sırası.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-439">Similar code gets a reference toohello *images* queue.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

<span data-ttu-id="e0f3e-440">Merhaba denetleyici kodlarının birçoğu bir DbContext sınıfı kullanarak bir Entity Framework veri modeli ile çalışmak için tipiktir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-440">Most of hello controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="e0f3e-441">Merhaba HttpPost bir istisnadır `Create` yöntemi, bir dosya yükler ve blob depolama alanına kaydeder.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-441">An exception is hello HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="e0f3e-442">Merhaba model bağlayıcı sağlar bir [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) nesne toohello yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-442">hello model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object toohello method.</span></span>

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

<span data-ttu-id="e0f3e-443">Merhaba kullanıcı dosya tooupload seçtiyseniz, hello kod hello dosyayı yükler, bir blob'a kaydeder ve hello Ad veritabanı kaydını toohello blob'u işaret eden bir URL ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-443">If hello user selected a file tooupload, hello code uploads hello file, saves it in a blob, and updates hello Ad database record with a URL that points toohello blob.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

<span data-ttu-id="e0f3e-444">Merhaba, karşıya yükleme hello hello koddur `UploadAndSaveBlobAsync` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-444">hello code that does hello upload is in hello `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="e0f3e-445">Merhaba blob, yüklemeleri ve kaydeder hello dosyası için bir GUID adı oluşturur ve bir başvuru toohello kaydedilmiş blob döndürür.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-445">It creates a GUID name for hello blob, uploads and saves hello file, and returns a reference toohello saved blob.</span></span>

```csharp
private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
{
    string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
    CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
    using (var fileStream = imageFile.InputStream)
    {
        await imageBlob.UploadFromStreamAsync(fileStream);
    }
    return imageBlob;
}
```

<span data-ttu-id="e0f3e-446">Merhaba HttpPost sonra `Create` yöntemi bir blob'u karşıya yüklemeleri ve güncelleştirmeleri Merhaba veritabanı, bir kuyruk iletisi tooinform görüntü için dönüştürme tooa küçük resim hazır olduğunu, arka uç işlemi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-446">After hello HttpPost `Create` method uploads a blob and updates hello database, it creates a queue message tooinform that back-end process that an image is ready for conversion tooa thumbnail.</span></span>

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

<span data-ttu-id="e0f3e-447">Merhaba hello HttpPost kodunu `Edit` yöntemi, hello kullanıcı yeni bir görüntü dosyası seçtiği durumlarda zaten mevcut BLOB silinmelidir dışında benzer.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-447">hello code for hello HttpPost `Edit` method is similar except that if hello user selects a new image file any blobs that already exist must be deleted.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

<span data-ttu-id="e0f3e-448">Merhaba sonraki örnek bir ad sildiğinizde, BLOB'ları siler hello kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-448">hello next example shows hello code that deletes blobs when you delete an ad.</span></span>

```csharp
private async Task DeleteAdBlobsAsync(Ad ad)
{
    if (!string.IsNullOrWhiteSpace(ad.ImageURL))
    {
        Uri blobUri = new Uri(ad.ImageURL);
        await DeleteAdBlobAsync(blobUri);
    }
    if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
    {
        Uri blobUri = new Uri(ad.ThumbnailURL);
        await DeleteAdBlobAsync(blobUri);
    }
}
private static async Task DeleteAdBlobAsync(Uri blobUri)
{
    string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
    CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
    await blobToDelete.DeleteAsync();
}
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="e0f3e-449">ContosoAdsWeb - Views\Ad\Index.cshtml ve Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="e0f3e-449">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="e0f3e-450">Merhaba *Index.cshtml* dosyası küçük resimleri hello ile diğer ad verileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-450">hello *Index.cshtml* file displays thumbnails with hello other ad data.</span></span>

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

<span data-ttu-id="e0f3e-451">Merhaba *Details.cshtml* dosyası hello tam boyutlu görüntüyü gösterir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-451">hello *Details.cshtml* file displays hello full-size image.</span></span>

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="e0f3e-452">ContosoAdsWeb - Views\Ad\Create.cshtml ve Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="e0f3e-452">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="e0f3e-453">Merhaba *Create.cshtml* ve *Edit.cshtml* dosyaları belirtin etkinleştirir denetleyicisi tooget hello hello kodlama form `HttpPostedFileBase` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-453">hello *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables hello controller tooget hello `HttpPostedFileBase` object.</span></span>

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

<span data-ttu-id="e0f3e-454">Bir `<input>` öğesi, bir dosya seçme iletişim kutusu hello tarayıcı tooprovide söyler.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-454">An `<input>` element tells hello browser tooprovide a file selection dialog.</span></span>

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a><span data-ttu-id="e0f3e-455">ContosoAdsWorker - WorkerRole.cs - OnStart yöntemi</span><span class="sxs-lookup"><span data-stu-id="e0f3e-455">ContosoAdsWorker - WorkerRole.cs - OnStart method</span></span>
<span data-ttu-id="e0f3e-456">Hello Azure çalışan rolü ortamı çağırır hello `OnStart` hello yönteminde `WorkerRole` sınıf hello çalışan rolü Başlarken ve hello çağırır `Run` yöntemi hello zaman `OnStart` yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-456">hello Azure worker role environment calls hello `OnStart` method in hello `WorkerRole` class when hello worker role is getting started, and it calls hello `Run` method when hello `OnStart` method finishes.</span></span>

<span data-ttu-id="e0f3e-457">Merhaba `OnStart` yöntemi alır hello veritabanı bağlantı dizesi hello *.cscfg* dosya ve toohello Entity Framework DbContext sınıfına geçirir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-457">hello `OnStart` method gets hello database connection string from hello *.cscfg* file and passes it toohello Entity Framework DbContext class.</span></span> <span data-ttu-id="e0f3e-458">Merhaba sağlayıcı belirtilen toobe içermiyor biçimde hello SQLClient sağlayıcısı varsayılan olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-458">hello SQLClient provider is used by default, so hello provider does not have toobe specified.</span></span>

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

<span data-ttu-id="e0f3e-459">Bundan sonra hello yöntemi bir başvuru toohello depolama hesabı alır ve yoksa hello blob kapsayıcısı ve kuyruk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-459">After that, hello method gets a reference toohello storage account and creates hello blob container and queue if they don't exist.</span></span> <span data-ttu-id="e0f3e-460">Merhaba, kodudur zaten gördüğünüz hello web rolünde benzer toowhat `Application_Start` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-460">hello code for that is similar toowhat you already saw in hello web role `Application_Start` method.</span></span>

### <a name="contosoadsworker---workerrolecs---run-method"></a><span data-ttu-id="e0f3e-461">ContosoAdsWorker - WorkerRole.cs - Run yöntemi</span><span class="sxs-lookup"><span data-stu-id="e0f3e-461">ContosoAdsWorker - WorkerRole.cs - Run method</span></span>
<span data-ttu-id="e0f3e-462">Merhaba `Run` yöntemi çağrılır hello `OnStart` yöntemi başlatma işini tamamladığında.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-462">hello `Run` method is called when hello `OnStart` method finishes its initialization work.</span></span> <span data-ttu-id="e0f3e-463">Merhaba yöntemi yeni bir kuyruk iletisi izleyen ve bunlar ulaşan iletileri işleyen sonsuz bir döngü yürütür.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-463">hello method executes an infinite loop that watches for new queue messages and processes them when they arrive.</span></span>

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

<span data-ttu-id="e0f3e-464">Hello döngü her yinelemeden sonra herhangi bir kuyruk iletisi bulunmazsa için ikinci bir hello program uyku moduna geçer.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-464">After each iteration of hello loop, if no queue message was found, hello program sleeps for a second.</span></span> <span data-ttu-id="e0f3e-465">Bu, hello çalışan rolü aşırı CPU süresi ve depolama işlem maliyetleri doğurmasını engeller.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-465">This prevents hello worker role from incurring excessive CPU time and storage transaction costs.</span></span> <span data-ttu-id="e0f3e-466">Merhaba Microsoft Müşteri danışma ekibi tooproduction dağıtılan ve tatile ekleyip hikayeyi kimin tooinclude bunu unuttunuz bir geliştiricinin hikayesini anlatır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-466">hello Microsoft Customer Advisory Team tells a story about a  developer who forgot tooinclude this, deployed tooproduction, and left for vacation.</span></span> <span data-ttu-id="e0f3e-467">Kendisine geri alındı, birden çok hello tatil döndüğünde gözetim maliyeti.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-467">When he got back, his oversight cost more than hello vacation.</span></span>

<span data-ttu-id="e0f3e-468">Bazen bir kuyruk iletisi Merhaba içeriğine işlenirken bir hata neden olur.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-468">Sometimes hello content of a queue message causes an error in processing.</span></span> <span data-ttu-id="e0f3e-469">Bu adlı bir *zehir iletisi*, ve yalnızca bir hatayı günlüğe kaydedip hello döngüyü yeniden, bu iletiyi tooprocess sonsuz çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-469">This is called a *poison message*, and if you just logged an error and restarted hello loop, you could endlessly try tooprocess that message.</span></span>  <span data-ttu-id="e0f3e-470">Bu nedenle bir if hello catch bloğu içerir toosee denetler deyimi hello uygulama tooprocess çalıştı kaç kez hello geçerli iletiyi ve 5 defadan fazla olması durumunda, selamlama iletisine hello sıradan silinir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-470">Therefore hello catch block includes an if statement that checks toosee how many times hello app has tried tooprocess hello current message, and if it has been more than 5 times, hello message is deleted from hello queue.</span></span>

<span data-ttu-id="e0f3e-471">Bir kuyruk iletisi bulunduğunda `ProcessQueueMessage` çağrılır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-471">`ProcessQueueMessage` is called when a queue message is found.</span></span>

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

<span data-ttu-id="e0f3e-472">Bu kod hello veritabanı tooget hello resim URL'si okur, hello görüntü tooa küçük dönüştürür, hello küçük resmi bir blob'a kaydeder, hello veritabanı hello küçük resim blob URL'si ile güncelleştirir ve hello kuyruk iletisini siler.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-472">This code reads hello database tooget hello image URL, converts hello image tooa thumbnail, saves hello thumbnail in a blob, updates hello database with hello thumbnail blob URL, and deletes hello queue message.</span></span>

> [!NOTE]
> <span data-ttu-id="e0f3e-473">Merhaba hello kodda `ConvertImageToThumbnailJPG` yöntemi kolaylık sağlaması açısından hello System.Drawing ad alanındaki sınıfları kullanır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-473">hello code in hello `ConvertImageToThumbnailJPG` method uses classes in hello System.Drawing namespace for simplicity.</span></span> <span data-ttu-id="e0f3e-474">Ancak, bu ad alanındaki hello sınıflar Windows Forms ile kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-474">However, hello classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="e0f3e-475">Bir Windows veya ASP.NET hizmetinde kullanılması desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-475">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="e0f3e-476">Görüntü işleme seçenekleri hakkında daha fazla bilgi için bkz. [Dinamik Görüntü Oluşturma](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) ve [Görüntü Yeniden Boyutlandırmaya Ayrıntılı Bakış](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span><span class="sxs-lookup"><span data-stu-id="e0f3e-476">For more information about image-processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="troubleshooting"></a><span data-ttu-id="e0f3e-477">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="e0f3e-477">Troubleshooting</span></span>
<span data-ttu-id="e0f3e-478">Bu öğreticide hello yönergeleri izleyerek sırasında sorun oluşması durumunda bazı yaygın hatalar şunlardır ve nasıl tooresolve bunları.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-478">In case something doesn't work while you're following hello instructions in this tutorial, here are some common errors and how tooresolve them.</span></span>

### <a name="serviceruntimeroleenvironmentexception"></a><span data-ttu-id="e0f3e-479">ServiceRuntime.RoleEnvironmentException</span><span class="sxs-lookup"><span data-stu-id="e0f3e-479">ServiceRuntime.RoleEnvironmentException</span></span>
<span data-ttu-id="e0f3e-480">Merhaba `RoleEnvironment` nesnesi, bir uygulamayı Azure'da çalıştırdığınızda ya da hello Azure işlem öykünücüsü kullanarak yerel olarak çalıştırdığınızda Azure tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-480">hello `RoleEnvironment` object is provided by Azure when you run an application in Azure or when you run locally using hello Azure compute emulator.</span></span>  <span data-ttu-id="e0f3e-481">Yerel olarak çalıştırırken bu hatayı alırsanız, hello ContosoAdsCloudService projesinde hello başlangıç projesi olarak ayarladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-481">If you get this error when you're running locally, make sure that you have set hello ContosoAdsCloudService project as hello startup project.</span></span> <span data-ttu-id="e0f3e-482">Hello Azure işlem öykünücüsü kullanarak hello proje toorun ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-482">This sets up hello project toorun using hello Azure compute emulator.</span></span>

<span data-ttu-id="e0f3e-483">Merhaba uygulamanız tarafından kullanılan Azure RoleEnvironment hello hello şeyler biri hello depolanan tooget hello bağlantı dizesi değerleri *.cscfg* dosyaları, bu özel durumun başka bir nedeni eksik bir bağlantı dizesi gelir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-483">One of hello things hello application uses hello Azure RoleEnvironment for is tooget hello connection string values that are stored in hello *.cscfg* files, so another cause of this exception is a missing connection string.</span></span> <span data-ttu-id="e0f3e-484">Merhaba ContosoAdsWeb projesinde hem bulut için hello StorageConnectionString ayarını hem de yerel yapılandırmaları oluşturulur ve hello ContosoAdsWorker projesinde her iki yapılandırma için iki bağlantı dizesini oluşturulan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-484">Make sure that you created hello StorageConnectionString setting for both Cloud and Local configurations in hello ContosoAdsWeb project, and that you created both connection strings for both configurations in hello ContosoAdsWorker project.</span></span> <span data-ttu-id="e0f3e-485">Bunu yaparsanız bir **Tümünü Bul** arama StorageConnectionString için çözümün tamamında Merhaba, onu 9 kez 6 dosyada görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-485">If you do a **Find All** search for StorageConnectionString in hello entire solution, you should see it 9 times in 6 files.</span></span>

### <a name="cannot-override-tooport-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a><span data-ttu-id="e0f3e-486">Tooport xxx geçersiz kılamaz.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-486">Cannot override tooport xxx.</span></span> <span data-ttu-id="e0f3e-487">Yeni bağlantı noktası http protokolü için izin verilen en düşük 8080 değerinin altında</span><span class="sxs-lookup"><span data-stu-id="e0f3e-487">New port below minimum allowed value 8080 for protocol http</span></span>
<span data-ttu-id="e0f3e-488">Merhaba web projesi tarafından kullanılan başlangıç bağlantı noktası numarasını değiştirmeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-488">Try changing hello port number used by hello web project.</span></span> <span data-ttu-id="e0f3e-489">Merhaba ContosoAdsWeb projesine sağ tıklayın ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-489">Right-click hello ContosoAdsWeb project, and then click **Properties**.</span></span> <span data-ttu-id="e0f3e-490">Merhaba tıklatın **Web** sekmesini ve ardından hello hello bağlantı noktası numarasını değiştirin **proje URL'sini** ayarı.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-490">Click hello **Web** tab, and then change hello port number in hello **Project Url** setting.</span></span>

<span data-ttu-id="e0f3e-491">Merhaba sorunu çözebilecek başka bir alternatif için bölümden hello bakın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-491">For another alternative that might resolve hello problem, see hello following  section.</span></span>

### <a name="other-errors-when-running-locally"></a><span data-ttu-id="e0f3e-492">Yerel olarak çalışırken oluşan diğer hatalar</span><span class="sxs-lookup"><span data-stu-id="e0f3e-492">Other errors when running locally</span></span>
<span data-ttu-id="e0f3e-493">Varsayılan olarak yeni bulut hizmeti projeleri hello Azure işlem öykünücüsü express toosimulate hello Azure ortamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-493">By default new cloud service projects use hello Azure compute emulator express toosimulate hello Azure environment.</span></span> <span data-ttu-id="e0f3e-494">Bu bir hello tam işlem öykünücüsünün hafif sürümüdür ve hello hızlı sürümün çalışmadığı bazı koşullar hello altında tam öykünücü çalışır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-494">This is a lightweight version of hello full compute emulator, and under some conditions hello full emulator will work when hello express version does not.</span></span>  

<span data-ttu-id="e0f3e-495">toochange proje toouse hello tam öykünücü Merhaba, hello ContosoAdsCloudService projesine sağ tıklayın ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-495">toochange hello project toouse hello full emulator, right-click hello ContosoAdsCloudService project, and then click **Properties**.</span></span> <span data-ttu-id="e0f3e-496">Merhaba, **özellikleri** penceresinde hello tıklatın **Web** sekmesini ve sonra hello **tam öykünücü kullan** radyo düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-496">In hello **Properties** window click hello **Web** tab, and then click hello **Use Full Emulator** radio button.</span></span>

<span data-ttu-id="e0f3e-497">Sipariş toorun hello uygulamada hello tam öykünücü ile yönetici ayrıcalıklarıyla Visual Studio tooopen sahip.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-497">In order toorun hello application with hello full emulator, you have tooopen Visual Studio with administrator privileges.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0f3e-498">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e0f3e-498">Next steps</span></span>
<span data-ttu-id="e0f3e-499">Contoso Ads uygulaması Hello kasıtlı olarak bir başlangıç öğreticisi için basit tutulmuştur.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-499">hello Contoso Ads application has intentionally been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="e0f3e-500">Örneğin, uygulamaz [bağımlılık ekleme](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) veya hello [depo ve iş birimi düzenleri](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), yoktur [bir arabirim için günlük kaydını kullanmak](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), kullanmaz[ EF Code First geçişleri](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage veri modeli değişikliklerini veya [EF bağlantı dayanıklılığı](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage geçici ağ hataları ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-500">For example, it doesn't implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) or hello [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), it doesn't [use an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), it doesn't use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model changes or [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transient network errors, and so forth.</span></span>

<span data-ttu-id="e0f3e-501">En az karmaşık toomore karmaşık listelenen daha fazla gerçek kodlama uygulamalarını gösteren bazı bulut hizmeti örnek uygulamaları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e0f3e-501">Here are some cloud service sample applications that demonstrate more real-world coding practices, listed from less complex toomore complex:</span></span>

* <span data-ttu-id="e0f3e-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span><span class="sxs-lookup"><span data-stu-id="e0f3e-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span></span> <span data-ttu-id="e0f3e-503">Kavram benzer tooContoso Ads ancak daha fazla özellik ve daha fazla gerçek kodlama uygulamalarını uygular.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-503">Similar in concept tooContoso Ads but implements more features and more real-world coding practices.</span></span>
* <span data-ttu-id="e0f3e-504">[Tablolar, Kuyruklar ve Blob’lar ile Azure Cloud Service Çok Katmanlı Uygulaması](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span><span class="sxs-lookup"><span data-stu-id="e0f3e-504">[Azure Cloud Service Multi-Tier Application with Tables, Queues, and Blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span></span> <span data-ttu-id="e0f3e-505">Azure Storage tablolarının yanı sıra blob’ları ve kuyrukları tanıtır.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-505">Introduces Azure Storage tables as well as blobs and queues.</span></span> <span data-ttu-id="e0f3e-506">.NET için Azure SDK'sı hello daha eski bir sürümü bağlı olarak, bazı değişiklikler toowork hello geçerli sürümle gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-506">Based on an older version of hello Azure SDK for .NET, will require some modifications toowork with hello current version.</span></span>
* <span data-ttu-id="e0f3e-507">[Microsoft Azure’da Bulut Hizmeti Temel Bilgileri](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span><span class="sxs-lookup"><span data-stu-id="e0f3e-507">[Cloud Service Fundamentals in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span></span> <span data-ttu-id="e0f3e-508">Çok çeşitli hello Microsoft Patterns and Practices grubu tarafından oluşturulan en iyi yöntemleri gösteren kapsamlı bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="e0f3e-508">A comprehensive sample demonstrating a wide range of best practices, produced by hello Microsoft Patterns and Practices group.</span></span>

<span data-ttu-id="e0f3e-509">Merhaba bulut için geliştirme hakkında genel bilgi için bkz: [yapı Azure ile gerçek bulut uygulamaları](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span><span class="sxs-lookup"><span data-stu-id="e0f3e-509">For general information about developing for hello cloud, see [Building Real-World Cloud Apps with Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span></span>

<span data-ttu-id="e0f3e-510">Video girişi tooAzure depolama için en iyi yöntemler ve desenler için bkz: [Microsoft Azure Storage – yeni, en iyi yöntemler ve yaklaşımlar nedir](http://channel9.msdn.com/Events/Build/2014/3-628).</span><span class="sxs-lookup"><span data-stu-id="e0f3e-510">For a video introduction tooAzure Storage best practices and patterns, see [Microsoft Azure Storage – What's New, Best Practices and Patterns](http://channel9.msdn.com/Events/Build/2014/3-628).</span></span>

<span data-ttu-id="e0f3e-511">Daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="e0f3e-511">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="e0f3e-512">Azure Cloud Services Bölüm 1: Giriş</span><span class="sxs-lookup"><span data-stu-id="e0f3e-512">Azure Cloud Services Part 1: Introduction</span></span>](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [<span data-ttu-id="e0f3e-513">Toomanage Cloud Services nasıl</span><span class="sxs-lookup"><span data-stu-id="e0f3e-513">How toomanage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="e0f3e-514">Azure Depolama</span><span class="sxs-lookup"><span data-stu-id="e0f3e-514">Azure Storage</span></span>](/documentation/services/storage/)
* [<span data-ttu-id="e0f3e-515">Nasıl toochoose bir bulut hizmet sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="e0f3e-515">How toochoose a cloud service provider</span></span>](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
