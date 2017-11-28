---
title: "Azure Cloud Services ve ASP.NET kullanmaya başlama | Microsoft Belgeleri"
description: "ASP.NET MVC ve Azure kullanarak çok katmanlı bir uygulama oluşturma hakkında bilgi edinin. Uygulama, web rolü ve çalışan rolü ile birlikte bir bulut hizmetinde çalışır. Entity Framework, SQL Database ve Azure Storage kuyruklarını ve blob’larını kullanır."
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
ms.openlocfilehash: d2c197db73477d06d86d1c4faa8c4a2f58c7b391
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a><span data-ttu-id="3fd58-105">Azure Cloud Services ve ASP.NET kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="3fd58-105">Get started with Azure Cloud Services and ASP.NET</span></span>

## <a name="overview"></a><span data-ttu-id="3fd58-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3fd58-106">Overview</span></span>
<span data-ttu-id="3fd58-107">Bu öğreticide ASP.NET MVC ön ucuyla çok katmanlı bir .NET uygulaması oluşturma ve bir [Azure bulut hizmetine](cloud-services-choose-me.md) dağıtma işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-107">This tutorial shows how to create a multi-tier .NET application with an ASP.NET MVC front-end, and deploy it to an [Azure cloud service](cloud-services-choose-me.md).</span></span> <span data-ttu-id="3fd58-108">Uygulama [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), [Azure Blob hizmeti](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage) ve [Azure Queue hizmeti](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) kullanır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-108">The application uses [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), the [Azure Blob service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and the [Azure Queue service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span></span> <span data-ttu-id="3fd58-109">MSDN Kod Galerisi’nden [Visual Studio projesini](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fd58-109">You can [download the Visual Studio project](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) from the MSDN Code Gallery.</span></span>

<span data-ttu-id="3fd58-110">Öğreticide, uygulamayı yerel olarak oluşturup çalıştırma, Azure’a dağıtma ve bulutta çalıştırmanın yanı sıra sıfırdan oluşturma işlemleri de gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-110">The tutorial shows you how to build and run the application locally, how to deploy it to Azure and run in the cloud, and how to build it from scratch.</span></span> <span data-ttu-id="3fd58-111">Tercih ederseniz sıfırdan oluşturmaya başlayabilir ve ardından test ve dağıtım adımlarını gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fd58-111">You can start by building from scratch and then do the test and deploy steps afterward if you prefer.</span></span>

## <a name="contoso-ads-application"></a><span data-ttu-id="3fd58-112">Contoso Ads uygulaması</span><span class="sxs-lookup"><span data-stu-id="3fd58-112">Contoso Ads application</span></span>
<span data-ttu-id="3fd58-113">Uygulama bir reklam bülteni panosudur.</span><span class="sxs-lookup"><span data-stu-id="3fd58-113">The application is an advertising bulletin board.</span></span> <span data-ttu-id="3fd58-114">Kullanıcılar metin girerek ve görüntüyü karşıya yükleyerek bir reklam oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3fd58-114">Users create an ad by entering text and uploading an image.</span></span> <span data-ttu-id="3fd58-115">Küçük resim görüntüleriyle birlikte bir reklam listesi görebilir ve ayrıntılarını görmek üzere bir reklam seçtiklerinde tam boyutlu görüntüyü görebilirler.</span><span class="sxs-lookup"><span data-stu-id="3fd58-115">They can see a list of ads with thumbnail images, and they can see the full-size image when they select an ad to see the details.</span></span>

![Reklam listesi](./media/cloud-services-dotnet-get-started/list.png)

<span data-ttu-id="3fd58-117">Uygulama bir arka uç işleminde küçük resim oluşturmaya yönelik CPU yoğunluklu iş yükünü azaltmak üzere [kuyruk merkezli çalışma deseni](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) kullanır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-117">The application uses the [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) to off-load the CPU-intensive work of creating thumbnails to a back-end process.</span></span>

## <a name="alternative-architecture-websites-and-webjobs"></a><span data-ttu-id="3fd58-118">Alternatif mimari: Websites ve WebJobs</span><span class="sxs-lookup"><span data-stu-id="3fd58-118">Alternative architecture: Websites and WebJobs</span></span>
<span data-ttu-id="3fd58-119">Bu öğreticide bir Azure bulut hizmetinde hem ön ucun hem de arka ucun nasıl çalıştırılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-119">This tutorial shows how to run both front-end and back-end in an Azure cloud service.</span></span> <span data-ttu-id="3fd58-120">Alternatif yöntem bir [Azure web sitesinde](/services/web-sites/) ön uç çalıştırılması ve arka uç için [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) özelliğinin (şu anda önizlemede) kullanılmasıdır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-120">An alternative is to run the front-end in an [Azure website](/services/web-sites/) and use the [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) feature (currently in preview) for the back-end.</span></span> <span data-ttu-id="3fd58-121">WebJobs kullanan bir öğretici için bkz. [Azure WebJobs SDK ile Çalışmaya Başlama](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3fd58-121">For a tutorial that uses WebJobs, see [Get Started with the Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span></span> <span data-ttu-id="3fd58-122">Senaryonuza en uygun hizmetlerin nasıl seçileceği hakkında bilgi için bkz. [Azure Web Siteleri, Cloud Services ve sanal makineler karşılaştırması](../app-service-web/choose-web-site-cloud-service-vm.md).</span><span class="sxs-lookup"><span data-stu-id="3fd58-122">For information about how to choose the services that best fit your scenario, see [Azure Websites, Cloud Services, and virtual machines comparison](../app-service-web/choose-web-site-cloud-service-vm.md).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="3fd58-123">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="3fd58-123">What you'll learn</span></span>
* <span data-ttu-id="3fd58-124">Azure SDK’sını yükleyerek Azure dağıtımı için makinenizi etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="3fd58-124">How to enable your machine for Azure development by installing the Azure SDK.</span></span>
* <span data-ttu-id="3fd58-125">Bir ASP.NET MVC web rolü ve çalışan rolü ile Visual Studio bulut hizmeti projesi oluşturma.</span><span class="sxs-lookup"><span data-stu-id="3fd58-125">How to create a Visual Studio cloud service project with an ASP.NET MVC web role and a worker role.</span></span>
* <span data-ttu-id="3fd58-126">Azure Storage öykünücüsü kullanarak bulut hizmeti projesini yerel olarak test etme.</span><span class="sxs-lookup"><span data-stu-id="3fd58-126">How to test the cloud service project locally, using the Azure storage emulator.</span></span>
* <span data-ttu-id="3fd58-127">Bulut projesini bir Azure bulut hizmetinde yayımlama ve Azure Storage hesabını kullanarak test etme.</span><span class="sxs-lookup"><span data-stu-id="3fd58-127">How to publish the cloud project to an Azure cloud service and test using an Azure storage account.</span></span>
* <span data-ttu-id="3fd58-128">Dosyaları karşıya yükleme ve Azure Blob hizmetine depolama.</span><span class="sxs-lookup"><span data-stu-id="3fd58-128">How to upload files and store them in the Azure Blob service.</span></span>
* <span data-ttu-id="3fd58-129">Katmanlar arasında iletişim için Azure Queue hizmetini kullanma.</span><span class="sxs-lookup"><span data-stu-id="3fd58-129">How to use the Azure Queue service for communication between tiers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fd58-130">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3fd58-130">Prerequisites</span></span>
<span data-ttu-id="3fd58-131">Öğretici *web rolü* ve *çalışan rolü* terminolojisi gibi [Azure bulut hizmetleri hakkında temel kavramları](cloud-services-choose-me.md) anladığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="3fd58-131">The tutorial assumes that you understand [basic concepts about Azure cloud services](cloud-services-choose-me.md) such as *web role* and *worker role* terminology.</span></span>  <span data-ttu-id="3fd58-132">Ayrıca Visual Studio’da [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) veya [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projeleri ile nasıl çalışılacağını bildiğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="3fd58-132">It also assumes that you know how to work with [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) or [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projects in Visual Studio.</span></span> <span data-ttu-id="3fd58-133">Örnek uygulama MVC kullanır, ancak öğreticinin büyük bölümü Web Forms için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-133">The sample application uses MVC, but most of the tutorial also applies to Web Forms.</span></span>

<span data-ttu-id="3fd58-134">Uygulamayı bir Azure aboneliği olmadan yerel olarak çalıştırabilirsiniz, ancak uygulamayı buluta dağıtmak için bir abonelik gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-134">You can run the app locally without an Azure subscription, but you'll need one to deploy the application to the cloud.</span></span> <span data-ttu-id="3fd58-135">Bir hesabınız yoksa, [MSDN abone avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) veya [ücretsiz deneme için kaydolabilirsiniz.](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668)</span><span class="sxs-lookup"><span data-stu-id="3fd58-135">If you don't have an account, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span></span>

<span data-ttu-id="3fd58-136">Öğretici yönergeleri aşağıdaki ürünlerden biri ile çalışır:</span><span class="sxs-lookup"><span data-stu-id="3fd58-136">The tutorial instructions work with either of the following products:</span></span>

* <span data-ttu-id="3fd58-137">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3fd58-137">Visual Studio 2013</span></span>
* <span data-ttu-id="3fd58-138">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="3fd58-138">Visual Studio 2015</span></span>
* <span data-ttu-id="3fd58-139">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="3fd58-139">Visual Studio 2017</span></span>

<span data-ttu-id="3fd58-140">Bunlardan birine sahip değilseniz Azure SDK'yı yüklediğinizde Visual Studio otomatik olarak yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-140">If you don't have one of these, Visual Studio may be installed automatically when you install the Azure SDK.</span></span>

## <a name="application-architecture"></a><span data-ttu-id="3fd58-141">Uygulama mimarisi</span><span class="sxs-lookup"><span data-stu-id="3fd58-141">Application architecture</span></span>
<span data-ttu-id="3fd58-142">Uygulama, tablolar oluşturmak ve verilere erişmek için Entity Framework Code First kullanarak reklamları bir SQL veritabanına depolar.</span><span class="sxs-lookup"><span data-stu-id="3fd58-142">The app stores ads in a SQL database, using Entity Framework Code First to create the tables and access the data.</span></span> <span data-ttu-id="3fd58-143">Her reklam için veritabanı, biri tam boyutlu görüntü ve diğeri küçük resim olmak üzere iki URL depolar.</span><span class="sxs-lookup"><span data-stu-id="3fd58-143">For each ad, the database stores two URLs, one for the full-size image and one for the thumbnail.</span></span>

![Reklam tablosu](./media/cloud-services-dotnet-get-started/adtable.png)

<span data-ttu-id="3fd58-145">Bir kullanıcı görüntü yüklediğinde bir web rolünde çalışan ön uç görüntüyü bir [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)’a depolar ve reklam bilgilerini blob’u işaret eden bir URL ile birlikte veritabanına depolar.</span><span class="sxs-lookup"><span data-stu-id="3fd58-145">When a user uploads an image, the front-end running in a web role stores the image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores the ad information in the database with a URL that points to the blob.</span></span> <span data-ttu-id="3fd58-146">Aynı zamanda bir Azure kuyruğuna ileti yazar.</span><span class="sxs-lookup"><span data-stu-id="3fd58-146">At the same time, it writes a message to an Azure queue.</span></span> <span data-ttu-id="3fd58-147">Bir çalışan rolünde çalışan arka uç işlemi, kuyruğu yeni iletiler için düzenli olarak yoklar.</span><span class="sxs-lookup"><span data-stu-id="3fd58-147">A back-end process running in a worker role periodically polls the queue for new messages.</span></span> <span data-ttu-id="3fd58-148">Yeni bir ileti görüntülendiğinde çalışan rolü bu görüntü için bir küçük resim oluşturur ve küçük resim URL'si veritabanı alanını bu reklam için güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-148">When a new message appears, the worker role creates a thumbnail for that image and updates the thumbnail URL database field for that ad.</span></span> <span data-ttu-id="3fd58-149">Aşağıdaki diyagramda uygulama bölümlerinin nasıl etkileşim kurduğu gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-149">The following diagram shows how the parts of the application interact.</span></span>

![Contoso Ads mimarisi](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-the-completed-solution"></a><span data-ttu-id="3fd58-151">Tamamlanan çözümü indirme ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="3fd58-151">Download and run the completed solution</span></span>
1. <span data-ttu-id="3fd58-152">[Tamamlanan çözümü](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) indirip sıkıştırmasını açın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-152">Download and unzip the [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span></span>
2. <span data-ttu-id="3fd58-153">Visual Studio’yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-153">Start Visual Studio.</span></span>
3. <span data-ttu-id="3fd58-154">**Dosya** menüsünden **Proje Aç**’ı seçin, çözümü indirdiğiniz yere gidin ve ardından çözüm dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-154">From the **File** menu choose **Open Project**, navigate to where you downloaded the solution, and then open the solution file.</span></span>
4. <span data-ttu-id="3fd58-155">Çözümü derlemek için CTRL+SHIFT+B'ye basın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-155">Press CTRL+SHIFT+B to build the solution.</span></span>

    <span data-ttu-id="3fd58-156">Varsayılan olarak Visual Studio, *.zip* dosyasına dahil edilmeyen NuGet paketini otomatik olarak geri yükler.</span><span class="sxs-lookup"><span data-stu-id="3fd58-156">By default, Visual Studio automatically restores the NuGet package content, which was not included in the *.zip* file.</span></span> <span data-ttu-id="3fd58-157">Paketler geri yüklenmezse **Çözüm için NuGet Paketlerini Yönet** iletişim kutusuna gidip sağ üst köşedeki **Geri Yükle** düğmesine tıklayarak el ile yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-157">If the packages don't restore, install them manually by going to the **Manage NuGet Packages for Solution** dialog box and clicking the **Restore** button at the top right.</span></span>
5. <span data-ttu-id="3fd58-158">**Çözüm Gezgini**’nde başlangıç projesi olarak **ContosoAdsCloudService** öğesinin seçildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="3fd58-158">In **Solution Explorer**, make sure that **ContosoAdsCloudService** is selected as the startup project.</span></span>
6. <span data-ttu-id="3fd58-159">Visual Studio 2015 veya sonraki bir sürümü kullanıyorsanız ContosoAdsWeb projesinin uygulama *Web.config* dosyasında SQL Server bağlantı dizesini ve ContosoAdsCloudService projesinin *ServiceConfiguration.Local.cscfg* dosyasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-159">If you're using Visual Studio 2015 or higher, change the SQL Server connection string in the application *Web.config* file of the ContosoAdsWeb project and in the *ServiceConfiguration.Local.cscfg* file of the ContosoAdsCloudService project.</span></span> <span data-ttu-id="3fd58-160">Her iki örnekte de "(localdb)\v11.0" seçeneğini "(localdb)\MSSQLLocalDB" olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-160">In each case, change "(localdb)\v11.0" to "(localdb)\MSSQLLocalDB".</span></span>
7. <span data-ttu-id="3fd58-161">Uygulamayı çalıştırmak için CTRL+F5'e basın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-161">Press CTRL+F5 to run the application.</span></span>

    <span data-ttu-id="3fd58-162">Bir bulut hizmeti projesini yerel olarak çalıştırdığınızda Visual Studio, Azure *işlem öykünücüsü* ve Azure *depolama öykünücüsünü* otomatik olarak çağırır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-162">When you run a cloud service project locally, Visual Studio automatically invokes the Azure *compute emulator* and Azure *storage emulator*.</span></span> <span data-ttu-id="3fd58-163">İşlem öykünücüsü, web rolü ve çalışan rolü ortamlarını benzetmek için bilgisayarınızın kaynaklarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-163">The compute emulator uses your computer's resources to simulate the web role and worker role environments.</span></span> <span data-ttu-id="3fd58-164">Depolama öykünücüsü Azure bulut depolamayı benzetmek için bir [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) veritabanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-164">The storage emulator uses a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database to simulate Azure cloud storage.</span></span>

    <span data-ttu-id="3fd58-165">Bir bulut hizmeti projesini ilk kez çalıştırdığınızda öykünücülerin başlatılması yaklaşık bir dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="3fd58-165">The first time you run a cloud service project, it takes a minute or so for the emulators to start up.</span></span> <span data-ttu-id="3fd58-166">Öykünücü başlatma tamamlandığında varsayılan tarayıcıda uygulama giriş sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-166">When emulator startup is finished, the default browser opens to the application home page.</span></span>

    ![Contoso Ads mimarisi](./media/cloud-services-dotnet-get-started/home.png)
8. <span data-ttu-id="3fd58-168">**Reklam Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-168">Click  **Create an Ad**.</span></span>
9. <span data-ttu-id="3fd58-169">Bazı test verilerini girin ve karşıya yüklenecek bir *.jpg* görüntüsü seçip **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-169">Enter some test data and select a *.jpg* image to upload, and then click **Create**.</span></span>

    ![Sayfa oluşturma](./media/cloud-services-dotnet-get-started/create.png)

    <span data-ttu-id="3fd58-171">Uygulama Dizin sayfasına gider, ancak işleme henüz tamamlanmadığından yeni reklam için bir küçük resim göstermez.</span><span class="sxs-lookup"><span data-stu-id="3fd58-171">The app goes to the Index page, but it doesn't show a thumbnail for the new ad because that processing hasn't happened yet.</span></span>
10. <span data-ttu-id="3fd58-172">Biraz bekleyin ve ardından küçük resmi görmek için Dizin sayfasını yenileyin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-172">Wait a moment and then refresh the Index page to see the thumbnail.</span></span>

     ![Dizin sayfası](./media/cloud-services-dotnet-get-started/list.png)
11. <span data-ttu-id="3fd58-174">Tam boyutlu görüntüyü görmek için reklamınıza ilişkin **Ayrıntılar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-174">Click **Details** for your ad to see the full-size image.</span></span>

     ![Ayrıntılar sayfası](./media/cloud-services-dotnet-get-started/details.png)

<span data-ttu-id="3fd58-176">Uygulamayı herhangi bir bulut bağlantısı olmadan tamamen yerel bilgisayarınızda çalıştırıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="3fd58-176">You've been running the application entirely on your local computer, with no connection to the cloud.</span></span> <span data-ttu-id="3fd58-177">Depolama öykünücüsü kuyruk ve blob verilerini bir SQL Server Express LocalDB veritabanına, uygulama ise reklam verilerini başka bir LocalDB veritabanına depolar.</span><span class="sxs-lookup"><span data-stu-id="3fd58-177">The storage emulator stores the queue and blob data in a SQL Server Express LocalDB database, and the application stores the ad data in another LocalDB database.</span></span> <span data-ttu-id="3fd58-178">Entity Framework Code First, web uygulaması ilk kez erişmeye çalıştığında reklam veritabanını otomatik olarak oluşturmuştur.</span><span class="sxs-lookup"><span data-stu-id="3fd58-178">Entity Framework Code First automatically created the ad database the first time the web app tried to access it.</span></span>

<span data-ttu-id="3fd58-179">Aşağıdaki bölümde çözümü bulutta çalışan kuyruklar, blob’lar ve uygulama veritabanı için Azure bulut kaynakları kullanacak şekilde yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="3fd58-179">In the following section you'll configure the solution to use Azure cloud resources for queues, blobs, and the application database when it runs in the cloud.</span></span> <span data-ttu-id="3fd58-180">Yerel olarak çalıştırmaya devam ederken bulut depolama alanını ve veritabanı kaynaklarını da kullanmak istiyorsanız bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fd58-180">If you wanted to continue to run locally but use cloud storage and database resources, you could do that.</span></span> <span data-ttu-id="3fd58-181">Bunun için yalnızca bağlantı dizesi ayarlarını yapmanız gerekir. Bu ayarları nasıl yapacağınızı ileride öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="3fd58-181">It's just a matter of setting connection strings, which you'll see how to do.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="3fd58-182">Uygulamayı Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="3fd58-182">Deploy the application to Azure</span></span>
<span data-ttu-id="3fd58-183">Uygulamayı bulutta çalıştırmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3fd58-183">You'll do the following steps to run the application in the cloud:</span></span>

* <span data-ttu-id="3fd58-184">Bir Azure bulut hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3fd58-184">Create an Azure cloud service.</span></span>
* <span data-ttu-id="3fd58-185">Bir Azure SQL veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3fd58-185">Create an Azure SQL database.</span></span>
* <span data-ttu-id="3fd58-186">Bir Azure Storage hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3fd58-186">Create an Azure storage account.</span></span>
* <span data-ttu-id="3fd58-187">Çözümünüzü Azure’da çalıştığında Azure SQL veritabanınızı kullanacak şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-187">Configure the solution to use your Azure SQL database when it runs in Azure.</span></span>
* <span data-ttu-id="3fd58-188">Çözümünüzü Azure’da çalıştığında Azure Storage hesabınızı kullanacak şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-188">Configure the solution to use your Azure storage account when it runs in Azure.</span></span>
* <span data-ttu-id="3fd58-189">Projeyi Azure bulut hizmetinize dağıtın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-189">Deploy the project to your Azure cloud service.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="3fd58-190">Bir Azure bulut hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="3fd58-190">Create an Azure cloud service</span></span>
<span data-ttu-id="3fd58-191">Azure bulut hizmeti, uygulamanın çalıştırılacağı ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-191">An Azure cloud service is the environment the application will run in.</span></span>

1. <span data-ttu-id="3fd58-192">Tarayıcınızda [Azure portalı](https://portal.azure.com)’nı açın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-192">In your browser, open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3fd58-193">**Yeni > Hesapla > Bulut Hizmeti**’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-193">Click **New > Compute > Cloud Service**.</span></span>

3. <span data-ttu-id="3fd58-194">DNS adı giriş kutusuna bulut hizmeti için bir URL ön eki girin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-194">In the DNS name input box, enter a URL prefix for the cloud service.</span></span>

    <span data-ttu-id="3fd58-195">Bu URL benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-195">This URL has to be unique.</span></span>  <span data-ttu-id="3fd58-196">Seçtiğiniz ön ek zaten kullanılıyorsa bir hata iletisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="3fd58-196">You'll get an error message if the prefix you choose is already in use.</span></span>
4. <span data-ttu-id="3fd58-197">Hizmet için yeni bir Kaynak grubu belirtin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-197">Specify a new Resource group for the  service.</span></span> <span data-ttu-id="3fd58-198">**Yeni oluştur**’a tıklayın ve Kaynak grubu giriş kutusuna CS_contososadsRG gibi bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-198">Click **Create new** and then type a name in the Resource group input box, such as CS_contososadsRG.</span></span>

5. <span data-ttu-id="3fd58-199">Uygulamayı dağıtmak istediğiniz bölgeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-199">Choose the region where you want to deploy the application.</span></span>

    <span data-ttu-id="3fd58-200">Bu alan, bulut hizmetinizin hangi veri merkezinde barındırılacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-200">This field specifies which datacenter your cloud service will be hosted in.</span></span> <span data-ttu-id="3fd58-201">Bir üretim uygulaması için müşterilerinize en yakın bölgeyi seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-201">For a production application, you'd choose the region closest to your customers.</span></span> <span data-ttu-id="3fd58-202">Bu öğretici için size en yakın bölgeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-202">For this tutorial, choose the region closest to you.</span></span>
5. <span data-ttu-id="3fd58-203">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-203">Click **Create**.</span></span>

    <span data-ttu-id="3fd58-204">Aşağıdaki görüntüde bulut hizmeti CSvccontosoads.cloudapp.net URL’si ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3fd58-204">In the following image, a cloud service is created with the URL CSvccontosoads.cloudapp.net.</span></span>

    ![Yeni Bulut Hizmeti](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a><span data-ttu-id="3fd58-206">Bir Azure SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3fd58-206">Create an Azure SQL database</span></span>
<span data-ttu-id="3fd58-207">Uygulama bulutta çalıştırıldığında bulut tabanlı bir veritabanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-207">When the app runs in the cloud, it will use a cloud-based database.</span></span>

1. <span data-ttu-id="3fd58-208">[Azure portalı](https://portal.azure.com)’nda **Yeni > Veritabanları > SQL Veritabanı**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-208">In the [Azure portal](https://portal.azure.com), click **New > Databases > SQL Database**.</span></span>
2. <span data-ttu-id="3fd58-209">**Veritabanı Adı** kutusuna *contosoads* yazın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-209">In the **Database Name** box, enter *contosoads*.</span></span>
3. <span data-ttu-id="3fd58-210">**Kaynak grubu**’nda **Var olanı kullan**’a tıklayın ve bulut hizmeti için kullanılan kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-210">In the **Resource group**, click **Use existing** and select the resource group used for the cloud service.</span></span>
4. <span data-ttu-id="3fd58-211">Aşağıdaki görüntüde, **Sunucu - Gerekli ayarları yapılandır**’a ve **Yeni sunucu oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-211">In the following image, click **Server - Configure required settings** and **Create a new server**.</span></span>

    ![Veritabanı sunucusu için tünel](./media/cloud-services-dotnet-get-started/newdb.png)

    <span data-ttu-id="3fd58-213">Alternatif olarak, aboneliğiniz zaten bir sunucuya sahipse aşağı açılan listeden bu sunucuyu seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fd58-213">Alternatively, if your subscription already has a server, you can select that server from the drop-down list.</span></span>
5. <span data-ttu-id="3fd58-214">**Sunucu adı** kutusuna *csvccontosodbserver*’ı girin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-214">In the **Server name** box, enter *csvccontosodbserver*.</span></span>

6. <span data-ttu-id="3fd58-215">Bir yönetici için **Kullanıcı Adı** ve **Parola** girin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-215">Enter an administrator **Login Name** and **Password**.</span></span>

    <span data-ttu-id="3fd58-216">**Yeni sunucu oluştur**’u seçtiyseniz buraya mevcut bir adı ve parolayı girmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fd58-216">If you selected **Create a new server**, you aren't entering an existing name and password here.</span></span> <span data-ttu-id="3fd58-217">Daha sonra veritabanına eriştiğinizde kullanmak için şu anda tanımladığınız bir adı ve parolayı girersiniz.</span><span class="sxs-lookup"><span data-stu-id="3fd58-217">You're entering a new name and password that you're defining now to use later when you access the database.</span></span> <span data-ttu-id="3fd58-218">Daha önce oluşturduğunuz bir sunucuyu seçtiyseniz önceden oluşturduğunuz yönetici kullanıcı hesabı için parola istenir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-218">If you selected a server that you created previously, you'll be prompted for the password to the administrative user account you already created.</span></span>
7. <span data-ttu-id="3fd58-219">Bulut hizmeti için seçtiğiniz aynı **Konum**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-219">Choose the same **Location** that you chose for the cloud service.</span></span>

    <span data-ttu-id="3fd58-220">Bulut hizmeti ve veritabanı farklı veri merkezlerinde (farklı bölgelerde) olduğunda gecikme artar ve veri merkezinin dışındaki bant genişliği için sizden ücret alınır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-220">When the cloud service and database are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside the data center.</span></span> <span data-ttu-id="3fd58-221">Bir veri merkezi içinde bant genişliği ücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-221">Bandwidth within a data center is free.</span></span>
8. <span data-ttu-id="3fd58-222">**Azure hizmetlerinin sunucuya erişmesine izin ver** seçeneğini işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-222">Check **Allow azure services to access server**.</span></span>
9. <span data-ttu-id="3fd58-223">Yeni sunucu için **Seçin**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-223">Click **Select** for the new server.</span></span>

    ![Yeni SQL Veritabanı sunucusu](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. <span data-ttu-id="3fd58-225">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-225">Click **Create**.</span></span>

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="3fd58-226">Azure Storage hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3fd58-226">Create an Azure storage account</span></span>
<span data-ttu-id="3fd58-227">Azure Storage hesabı kuyruk ve blob verilerini buluta depolamaya yönelik kaynaklar sağlar.</span><span class="sxs-lookup"><span data-stu-id="3fd58-227">An Azure storage account provides resources for storing queue and blob data in the cloud.</span></span>

<span data-ttu-id="3fd58-228">Gerçek bir uygulamada genellikle uygulama verilerine karşı günlük verileri için ve test verilerine karşı üretim verileri için ayrı hesaplar oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="3fd58-228">In a real-world application, you would typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span></span> <span data-ttu-id="3fd58-229">Bu öğreticide yalnızca tek bir hesap kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="3fd58-229">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="3fd58-230">[Azure portalı](https://portal.azure.com)’nda **Yeni > Depolama > Depolama hesabı - blob, dosya, tablo, kuyruk**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-230">In the [Azure portal](https://portal.azure.com), click **New > Storage > Storage account - blob, file, table, queue**.</span></span>
2. <span data-ttu-id="3fd58-231">**Ad** kutusuna bir URL ön eki girin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-231">In the **Name** box, enter a URL prefix.</span></span>

    <span data-ttu-id="3fd58-232">Bu ön ek ile birlikte kutunun altında gördüğünüz metin, depolama hesabınızın benzersiz URL’si olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-232">This prefix plus the text you see under the box will be the unique URL to your storage account.</span></span> <span data-ttu-id="3fd58-233">Girdiğiniz ön ek başka bir kişi tarafından zaten kullanılıyorsa farklı bir ön ek seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-233">If the prefix you enter has already been used by someone else, you'll have to choose a different prefix.</span></span>
3. <span data-ttu-id="3fd58-234">**Dağıtım modeli**’ni *Klasik* olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-234">Set the **Deployment model** to *Classic*.</span></span>

4. <span data-ttu-id="3fd58-235">**Çoğaltma** açılır listesini **Yerel olarak yedekli depolama** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-235">Set the **Replication** drop-down list to **Locally redundant storage**.</span></span>

    <span data-ttu-id="3fd58-236">Bir depolama hesabı için coğrafi çoğaltma etkinleştirildiğinde, birincil konumda önemli bir olağanüstü durum oluşursa yük devretmeyi etkinleştirmek için depolanan içerik ikincil bir veri merkezine çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-236">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover if a major disaster occurs in the primary location.</span></span> <span data-ttu-id="3fd58-237">Coğrafi çoğaltma ek ücretlere neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-237">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="3fd58-238">Test ve geliştirme hesaplarında genellikle coğrafi çoğaltma için ödeme yapmak istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fd58-238">For test and development accounts, you generally don't want to pay for geo-replication.</span></span> <span data-ttu-id="3fd58-239">Daha fazla bilgi için bkz. [Depolama hesabı oluşturma, yönetme veya silme](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="3fd58-239">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>

5. <span data-ttu-id="3fd58-240">**Kaynak grubu**’nda **Var olanı kullan**’a tıklayın ve bulut hizmeti için kullanılan kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-240">In the **Resource group**, click **Use existing** and select the resource group used for the cloud service.</span></span>
6. <span data-ttu-id="3fd58-241">**Konum** açılır listesini bulut hizmeti için seçtiğiniz aynı bölgeye ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-241">Set the **Location** drop-down list to the same region you chose for the cloud service.</span></span>

    <span data-ttu-id="3fd58-242">Bulut hizmeti ve depolama hesabı farklı veri merkezlerinde (farklı bölgelerde) olduğunda gecikme artar ve veri merkezinin dışındaki bant genişliği için sizden ücret alınır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-242">When the cloud service and storage account are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside the data center.</span></span> <span data-ttu-id="3fd58-243">Bir veri merkezi içinde bant genişliği ücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-243">Bandwidth within a data center is free.</span></span>

    <span data-ttu-id="3fd58-244">Azure benzeşim grupları bir veri merkezinde bulunan kaynaklar arasındaki uzaklığı en aza indirmeye yönelik bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="3fd58-244">Azure affinity groups provide a mechanism to minimize the distance between resources in a data center, which can reduce latency.</span></span> <span data-ttu-id="3fd58-245">Bu öğretici benzeşim gruplarını kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="3fd58-245">This tutorial does not use affinity groups.</span></span> <span data-ttu-id="3fd58-246">Daha fazla bilgi için bkz. [Azure’da Benzeşim Grubu Oluşturma](http://msdn.microsoft.com/library/jj156209.aspx).</span><span class="sxs-lookup"><span data-stu-id="3fd58-246">For more information, see [How to Create an Affinity Group in Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span></span>
7. <span data-ttu-id="3fd58-247">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-247">Click **Create**.</span></span>

    ![Yeni depolama hesabı](./media/cloud-services-dotnet-get-started/newstorage.png)

    <span data-ttu-id="3fd58-249">Görüntüde `csvccontosoads.core.windows.net` URL’si ile bir depolama hesabı oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="3fd58-249">In the image, a storage account is created with the URL `csvccontosoads.core.windows.net`.</span></span>

### <a name="configure-the-solution-to-use-your-azure-sql-database-when-it-runs-in-azure"></a><span data-ttu-id="3fd58-250">Çözümünüzü Azure’da çalıştığında Azure SQL veritabanınızı kullanacak şekilde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3fd58-250">Configure the solution to use your Azure SQL database when it runs in Azure</span></span>
<span data-ttu-id="3fd58-251">Web projesi ve çalışan rolü projelerinin her biri kendi veritabanı bağlantı dizesine sahiptir ve uygulama Azure'da çalıştırıldığında her birinin Azure SQL veritabanına işaret etmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-251">The web project and the worker role project each has its own database connection string, and each needs to point to the Azure SQL database when the app runs in Azure.</span></span>

<span data-ttu-id="3fd58-252">Web rolü için bir [Web.config dönüşümü](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) ve çalışan rolü için bir bulut hizmet ortamı ayarı kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="3fd58-252">You'll use a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) for the web role and a cloud service environment setting for the worker role.</span></span>

> [!NOTE]
> <span data-ttu-id="3fd58-253">Bu ve sonraki bölümde, kimlik bilgilerini proje dosyalarında depolarsınız.</span><span class="sxs-lookup"><span data-stu-id="3fd58-253">In this section and the next section, you store credentials in project files.</span></span> <span data-ttu-id="3fd58-254">[Hassas verileri ortak kaynak kodu depolarına kaydetmeyin](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="3fd58-254">[Don't store sensitive data in public source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span>
>
>

1. <span data-ttu-id="3fd58-255">ContosoAdsWeb projesinde uygulama *Web.config* dosyasının *Web.Release.config* dönüşüm dosyasını açın, bir `<connectionStrings>` öğesi içeren açıklama bloğunu silin ve aşağıdaki kodu yerine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-255">In the ContosoAdsWeb project, open the *Web.Release.config* transform file for the application *Web.config* file, delete the comment block that contains a `<connectionStrings>` element, and paste the following code in its place.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    <span data-ttu-id="3fd58-256">Dosyayı düzenlemek için açık bırakın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-256">Leave the file open for editing.</span></span>
2. <span data-ttu-id="3fd58-257">[Azure portalı](https://portal.azure.com)’nda sol bölmedeki **SQL Veritabanları**’na, bu öğretici için oluşturduğunuz veritabanına ve ardından **Bağlantı dizelerini göster**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-257">In the [Azure portal](https://portal.azure.com), click **SQL Databases** in the left pane, click the database you created for this tutorial, and then click **Show connection strings**.</span></span>

    ![Bağlantı dizelerini göster](./media/cloud-services-dotnet-get-started/showcs.png)

    <span data-ttu-id="3fd58-259">Portal, parola için bir yer tutucu ile birlikte bağlantı dizelerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-259">The portal displays connection strings, with a placeholder for the password.</span></span>

    ![Bağlantı dizeleri](./media/cloud-services-dotnet-get-started/connstrings.png)
3. <span data-ttu-id="3fd58-261">*Web.Release.config* dönüşüm dosyasında `{connectionstring}` öğesini silin ve yerine Azure portalındaki ADO.NET bağlantı dizesini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-261">In the *Web.Release.config* transform file, delete `{connectionstring}` and paste in its place the ADO.NET connection string from the Azure portal.</span></span>
4. <span data-ttu-id="3fd58-262">*Web.Release.config* dönüşüm dosyasının içine yapıştırdığınız bağlantı dizesinde `{your_password_here}` öğesini yeni SQL veritabanı için oluşturduğunuz parola ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-262">In the connection string that you pasted into the *Web.Release.config* transform file, replace `{your_password_here}` with the password you created for the new SQL database.</span></span>
5. <span data-ttu-id="3fd58-263">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-263">Save the file.</span></span>  
6. <span data-ttu-id="3fd58-264">Bağlantı dizesini (çevresindeki soru işaretleri olmadan) çalışan rolünü yapılandırmaya yönelik aşağıdaki adımlarda kullanılmak üzere seçip kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-264">Select and copy the connection string (without the surrounding quotation marks) for use in the following steps for configuring the worker role project.</span></span>
7. <span data-ttu-id="3fd58-265">**Çözüm Gezgini**’nde bulut hizmeti projesindeki **Roller** altında **ContosoAdsWorker**’a ve ardından **Özellikler**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-265">In **Solution Explorer**, under **Roles** in the cloud service project, right-click **ContosoAdsWorker** and then click **Properties**.</span></span>

    ![Rol özellikleri](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. <span data-ttu-id="3fd58-267">**Ayarlar** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-267">Click the **Settings** tab.</span></span>
9. <span data-ttu-id="3fd58-268">**Hizmet Yapılandırması**’nı **Bulut** olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-268">Change **Service Configuration** to **Cloud**.</span></span>
10. <span data-ttu-id="3fd58-269">`ContosoAdsDbConnectionString` ayarı için **Değer** alanını seçin ve ardından öğreticinin önceki bölümünde kopyaladığınız bağlantı dizesini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-269">Select the **Value** field for the `ContosoAdsDbConnectionString` setting, and then paste the connection string that you copied from the previous section of the tutorial.</span></span>

     ![Çalışan rolü için veritabanı bağlantı dizesi](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. <span data-ttu-id="3fd58-271">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-271">Save your changes.</span></span>  

### <a name="configure-the-solution-to-use-your-azure-storage-account-when-it-runs-in-azure"></a><span data-ttu-id="3fd58-272">Çözümünüzü Azure’da çalıştığında Azure Storage hesabınızı kullanacak şekilde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3fd58-272">Configure the solution to use your Azure storage account when it runs in Azure</span></span>
<span data-ttu-id="3fd58-273">Hem web rolü projesinin hem de çalışan rolü projesinin Azure Storage hesabı bağlantı dizeleri, bulut hizmeti projesindeki ortam ayarlarına depolanır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-273">Azure storage account connection strings for both the web role project and the worker role project are stored in environment settings in the cloud service project.</span></span> <span data-ttu-id="3fd58-274">Her proje için uygulama yerel olarak çalıştığında ve bulutta çalıştığında kullanılacak ayrı ayarlar vardır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-274">For each project, there is a separate set of settings to be used when the application runs locally and when it runs in the cloud.</span></span> <span data-ttu-id="3fd58-275">Hem web hem de çalışan rolü projeleri için bulut ortamı ayarlarını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-275">You'll update the cloud environment settings for both web and worker role projects.</span></span>

1. <span data-ttu-id="3fd58-276">**Çözüm Gezgini**’nde **ContosoAdsCloudService** projesindeki **Roller** altında **ContosoAdsWeb**’e sağ tıklayın ve ardından **Özellikler**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-276">In **Solution Explorer**, right-click **ContosoAdsWeb** under **Roles** in the **ContosoAdsCloudService** project, and then click **Properties**.</span></span>

    ![Rol özellikleri](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. <span data-ttu-id="3fd58-278">**Ayarlar** sekmesine tıklayın. **Hizmet Yapılandırma** açılır kutusunda **Bulut**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-278">Click the **Settings** tab. In the **Service Configuration** drop-down box, choose **Cloud**.</span></span>

    ![Bulut yapılandırması](./media/cloud-services-dotnet-get-started/sccloud.png)
3. <span data-ttu-id="3fd58-280">**StorageConnectionString** girdisini seçtiğinizde satırın sağ uç kısmında bir üç nokta (**...**) göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="3fd58-280">Select the **StorageConnectionString** entry, and you'll see an ellipsis (**...**) button at the right end of the line.</span></span> <span data-ttu-id="3fd58-281">**Depolama Hesabı Bağlantı Dizesi Oluştur** iletişim kutusunu açmak için üç nokta düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-281">Click the ellipsis button to open the **Create Storage Account Connection String** dialog box.</span></span>

    ![Bağlantı Dizesi Oluştur kutusunu açma](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. <span data-ttu-id="3fd58-283">**Depolama Bağlantı Dizesi Oluştur** iletişim kutusunda **Aboneliğiniz**’e tıklayın, daha önce oluşturduğunuz depolama hesabını seçin ve ardından **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-283">In the **Create Storage Connection String** dialog box, click **Your subscription**, choose the storage account that you created earlier, and then click **OK**.</span></span> <span data-ttu-id="3fd58-284">Henüz oturum açmadıysanız Azure hesabı kimlik bilgileriniz istenir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-284">If you're not already logged in, you'll be prompted for your Azure account credentials.</span></span>

    ![Depolama Bağlantı Dizesi oluşturma](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. <span data-ttu-id="3fd58-286">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-286">Save your changes.</span></span>
6. <span data-ttu-id="3fd58-287">`Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` bağlantı dizesini ayarlamak için `StorageConnectionString` bağlantı dizesi için kullandığınız yordamın aynısını izleyin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-287">Follow the same procedure that you used for the `StorageConnectionString` connection string to set the `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` connection string.</span></span>

    <span data-ttu-id="3fd58-288">Bu bağlantı dizesi günlüğe kaydetme için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-288">This connection string is used for logging.</span></span>
7. <span data-ttu-id="3fd58-289">**ContosoAdsWeb** rolü için **ContosoAdsWorker** rolünün her iki bağlantı dizesini ayarlamak üzere kullandığınız yordamın aynısını izleyin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-289">Follow the same procedure that you used for the **ContosoAdsWeb** role to set both connection strings for the **ContosoAdsWorker** role.</span></span> <span data-ttu-id="3fd58-290">**Hizmet Yapılandırması**’nı **Bulut** olarak ayarlamayı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-290">Don't forget to set **Service Configuration** to **Cloud**.</span></span>

<span data-ttu-id="3fd58-291">Visual Studio kullanıcı arabirimini kullanılarak yapılandırdığınız rol ortamı ayarları ContosoAdsCloudService projesinde aşağıdaki dosyalara depolanır:</span><span class="sxs-lookup"><span data-stu-id="3fd58-291">The role environment settings that you have configured using the Visual Studio UI are stored in the following files in the ContosoAdsCloudService project:</span></span>

* <span data-ttu-id="3fd58-292">*ServiceDefinition.csdef* - Ayar adlarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3fd58-292">*ServiceDefinition.csdef* - Defines the setting names.</span></span>
* <span data-ttu-id="3fd58-293">*ServiceConfiguration.Cloud.cscfg* - Uygulamanın yerel olarak çalıştığı durumlar için değerler sağlar.</span><span class="sxs-lookup"><span data-stu-id="3fd58-293">*ServiceConfiguration.Cloud.cscfg* - Provides values for when the app runs in the cloud.</span></span>
* <span data-ttu-id="3fd58-294">*ServiceConfiguration.Local.cscfg* - Uygulamanın yerel olarak çalıştığı durumlar için değerler sağlar.</span><span class="sxs-lookup"><span data-stu-id="3fd58-294">*ServiceConfiguration.Local.cscfg* - Provides values for when the app runs locally.</span></span>

<span data-ttu-id="3fd58-295">Örneğin, ServiceDefinition.csdef aşağıdaki tanımları içerir:</span><span class="sxs-lookup"><span data-stu-id="3fd58-295">For example, the ServiceDefinition.csdef includes the following definitions:</span></span>

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

<span data-ttu-id="3fd58-296">*ServiceConfiguration.Cloud.cscfg* dosyası ise Visual Studio’da bu ayarlar için girdiğiniz değerleri içerir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-296">And the *ServiceConfiguration.Cloud.cscfg* file includes the values you entered for those settings in Visual Studio.</span></span>

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

<span data-ttu-id="3fd58-297">`<Instances>` ayarı Azure’un çalışan rolü kodunu çalıştıracağı sanal makine sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-297">The `<Instances>` setting specifies the number of virtual machines that Azure will run the worker role code on.</span></span> <span data-ttu-id="3fd58-298">[Sonraki adımlar](#next-steps) bölümünde bir bulut hizmetinin ölçeğini artırma hakkında daha fazla bilgi içeren bağlantılar bulunur.</span><span class="sxs-lookup"><span data-stu-id="3fd58-298">The [Next steps](#next-steps) section includes links to more information about scaling out a cloud service,</span></span>

### <a name="deploy-the-project-to-azure"></a><span data-ttu-id="3fd58-299">Projeyi Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="3fd58-299">Deploy the project to Azure</span></span>
1. <span data-ttu-id="3fd58-300">**Çözüm Gezgini**’nde **ContosoAdsCloudService** bulut projesine sağ tıklayın ve ardından **Yayımla** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-300">In **Solution Explorer**, right-click the **ContosoAdsCloudService** cloud project and then select **Publish**.</span></span>

   ![Yayımla menüsü](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. <span data-ttu-id="3fd58-302">**Azure Uygulaması Yayımlama** sihirbazının **Oturum aç** adımında **Sonraki** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-302">In the **Sign in** step of the **Publish Azure Application** wizard, click **Next**.</span></span>

    ![Oturum açma adımı](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. <span data-ttu-id="3fd58-304">Sihirbazın **Ayarlar** adımında **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-304">In the **Settings** step of the wizard, click **Next**.</span></span>

    ![Ayarlar adımı](./media/cloud-services-dotnet-get-started/pubsettings.png)

    <span data-ttu-id="3fd58-306">**Gelişmiş** sekmesindeki varsayılan ayarlar bu öğretici için uygundur.</span><span class="sxs-lookup"><span data-stu-id="3fd58-306">The default settings in the **Advanced** tab are fine for this tutorial.</span></span> <span data-ttu-id="3fd58-307">Gelişmiş sekmesi hakkında bilgi için bkz. [Azure Uygulaması Yayımlama Sihirbazı](http://msdn.microsoft.com/library/hh535756.aspx).</span><span class="sxs-lookup"><span data-stu-id="3fd58-307">For information about the advanced tab, see [Publish Azure Application Wizard](http://msdn.microsoft.com/library/hh535756.aspx).</span></span>
4. <span data-ttu-id="3fd58-308">**Özet** adımında **Yayımla** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-308">In the **Summary** step, click **Publish**.</span></span>

    ![Özet adımı](./media/cloud-services-dotnet-get-started/pubsummary.png)

   <span data-ttu-id="3fd58-310">Visual Studio’da **Azure Etkinlik Günlüğü** penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-310">The **Azure Activity Log** window opens in Visual Studio.</span></span>
5. <span data-ttu-id="3fd58-311">Dağıtım ayrıntılarını genişletmek için sağ ok simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-311">Click the right arrow icon to expand the deployment details.</span></span>

    <span data-ttu-id="3fd58-312">Dağıtımın tamamlanması 5 dakika veya daha fazla sürebilir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-312">The deployment can take up to 5 minutes or more to complete.</span></span>

    ![Azure Etkinlik Günlüğü penceresi](./media/cloud-services-dotnet-get-started/waal.png)
6. <span data-ttu-id="3fd58-314">Dağıtım durumu tamamlandığında uygulamayı başlatmak için **Web uygulaması URL'si** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-314">When the deployment status is complete, click the **Web app URL** to start the application.</span></span>
7. <span data-ttu-id="3fd58-315">Uygulamayı yerel olarak çalıştırdığınızda yaptığınız gibi reklam oluşturarak, görüntüleyerek ve bazılarını düzenleyerek uygulamayı test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fd58-315">You can now test the app by creating, viewing, and editing some ads, as you did when you ran the application locally.</span></span>

> [!NOTE]
> <span data-ttu-id="3fd58-316">Testi tamamladığınızda bulut hizmetini silin veya durdurun.</span><span class="sxs-lookup"><span data-stu-id="3fd58-316">When you're finished testing, delete or stop the cloud service.</span></span> <span data-ttu-id="3fd58-317">Bulut hizmeti kullanmıyorsanız bile onun için sanal makine kaynakları ayrılmış olduğundan ücretler tahakkuk eder.</span><span class="sxs-lookup"><span data-stu-id="3fd58-317">Even if you're not using the cloud service, it's accruing charges because virtual machine resources are reserved for it.</span></span> <span data-ttu-id="3fd58-318">Ayrıca çalışır durumda bırakırsanız, URL’nizi bulan herhangi bir kişi reklam oluşturabilir ve görüntüleyebilir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-318">And if you leave it running, anyone who finds your URL can create and view ads.</span></span> <span data-ttu-id="3fd58-319">[Azure portalı](https://portal.azure.com)’nda bulut hizmetinizin **Genel Bakış** sekmesine gidin ve ardından sayfanın üstündeki **Sil** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-319">In the [Azure portal](https://portal.azure.com), go to the **Overview** tab for your cloud service, and then click the **Delete** button at the top of the page.</span></span> <span data-ttu-id="3fd58-320">Başkalarının siteye erişmesini yalnızca geçici olarak engellemek istiyorsanız bunun yerine **Durdur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-320">If you just want to temporarily prevent others from accessing the site, click **Stop** instead.</span></span> <span data-ttu-id="3fd58-321">Bu durumda ücretler tahakkuk etmeye devam eder.</span><span class="sxs-lookup"><span data-stu-id="3fd58-321">In that case, charges will continue to accrue.</span></span> <span data-ttu-id="3fd58-322">Artık ihtiyacınız kalmadığında SQL veritabanını ve depolama hesabını silmek için benzer bir yordamı izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fd58-322">You can follow a similar procedure to delete the SQL database and storage account when you no longer need them.</span></span>
>
>

## <a name="create-the-application-from-scratch"></a><span data-ttu-id="3fd58-323">Uygulamayı sıfırdan oluşturma</span><span class="sxs-lookup"><span data-stu-id="3fd58-323">Create the application from scratch</span></span>
<span data-ttu-id="3fd58-324">[Tamamlanmış uygulamayı](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) daha önce yüklemediyseniz şimdi yapın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-324">If you haven't already downloaded [the completed application](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), do that now.</span></span> <span data-ttu-id="3fd58-325">İndirilen projedeki dosyaları yeni projeye kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-325">You'll copy files from the downloaded project into the new project.</span></span>

<span data-ttu-id="3fd58-326">Contoso Ads uygulamasının oluşturulması aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="3fd58-326">Creating the Contoso Ads application involves the following steps:</span></span>

* <span data-ttu-id="3fd58-327">Bir bulut hizmeti Visual Studio çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3fd58-327">Create a cloud service Visual Studio solution.</span></span>
* <span data-ttu-id="3fd58-328">NuGet paketlerini güncelleştirin ve ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-328">Update and add NuGet packages.</span></span>
* <span data-ttu-id="3fd58-329">Proje başvurularını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-329">Set project references.</span></span>
* <span data-ttu-id="3fd58-330">Bağlantı dizelerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-330">Configure connection strings.</span></span>
* <span data-ttu-id="3fd58-331">Kod dosyaları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-331">Add code files.</span></span>

<span data-ttu-id="3fd58-332">Çözüm oluşturulduktan sonra bulut hizmeti projelerinde ve Azure blob'ları ile kuyruklarda benzersiz olan kodu gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-332">After the solution is created, you'll review the code that is unique to cloud service projects and Azure blobs and queues.</span></span>

### <a name="create-a-cloud-service-visual-studio-solution"></a><span data-ttu-id="3fd58-333">Bir bulut hizmeti Visual Studio çözümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="3fd58-333">Create a cloud service Visual Studio solution</span></span>
1. <span data-ttu-id="3fd58-334">Visual Studio'da **Dosya** menüsünden **Yeni Proje**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-334">In Visual Studio, choose **New Project** from the **File** menu.</span></span>
2. <span data-ttu-id="3fd58-335">**Yeni Proje** iletişim kutusunun sol bölmesinde **Visual C#** öğesini genişletin ve **Bulut** şablonlarını, ardından **Azure Cloud Service** şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-335">In the left pane of the **New Project** dialog box, expand **Visual C#** and choose **Cloud** templates, and then choose the **Azure Cloud Service** template.</span></span>
3. <span data-ttu-id="3fd58-336">Projeyi ve çözümü ContosoAdsCloudService olarak adlandırın ve ardından **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-336">Name the project and solution ContosoAdsCloudService, and then click **OK**.</span></span>

    ![Yeni Proje](./media/cloud-services-dotnet-get-started/newproject.png)
4. <span data-ttu-id="3fd58-338">**Yeni Azure Bulut Hizmeti** iletişim kutusunda bir web rolü ve bir çalışan rolü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-338">In the **New Azure Cloud Service** dialog box, add a web role and a worker role.</span></span> <span data-ttu-id="3fd58-339">Web rolünü ContosoAdsWeb olarak ve çalışan rolünü ContosoAdsWorker olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-339">Name the web role ContosoAdsWeb, and name the worker role ContosoAdsWorker.</span></span> <span data-ttu-id="3fd58-340">(Rollerin varsayılan adlarını değiştirmek için sağ bölmedeki kurşun kalem simgesini kullanın.)</span><span class="sxs-lookup"><span data-stu-id="3fd58-340">(Use the pencil icon in the right-hand pane to change the default names of the roles.)</span></span>

    ![Yeni Bulut Hizmeti Projesi](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. <span data-ttu-id="3fd58-342">Web rolü için **Yeni ASP.NET Projesi** iletişim kutusunu gördüğünüzde MVC şablonunu seçin ve ardından **Kimlik Doğrulamayı Değiştir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-342">When you see the **New ASP.NET Project** dialog box for the web role, choose the MVC template, and then click **Change Authentication**.</span></span>

    ![Kimlik Doğrulamayı Değiştirme](./media/cloud-services-dotnet-get-started/chgauth.png)
6. <span data-ttu-id="3fd58-344">**Kimlik Doğrulamayı Değiştir** iletişim kutusunda **Kimlik Doğrulaması Yok**’u seçin ve ardından **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-344">In the **Change Authentication** dialog box, choose **No Authentication**, and then click **OK**.</span></span>

    ![Kimlik Doğrulaması Yok](./media/cloud-services-dotnet-get-started/noauth.png)
7. <span data-ttu-id="3fd58-346">**Yeni ASP.NET Projesi** iletişim kutusunda **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-346">In the **New ASP.NET Project** dialog, click **OK**.</span></span>
8. <span data-ttu-id="3fd58-347">**Çözüm Gezgini**’nde çözüme (projelerden birine değil) sağ tıklayın ve **Ekle - Yeni Proje**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-347">In **Solution Explorer**, right-click the solution (not one of the projects), and choose **Add - New Project**.</span></span>
9. <span data-ttu-id="3fd58-348">**Yeni Proje Ekle** iletişim kutusunda sol bölmedeki **Visual C#** altında bulunan **Windows**’u seçin ve ardından **Sınıf Kitaplığı** şablonuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-348">In the **Add New Project** dialog box, choose **Windows** under **Visual C#** in the left pane, and then click the **Class Library** template.</span></span>  
10. <span data-ttu-id="3fd58-349">Projeyi *ContosoAdsCommon* olarak adlandırın ve ardından **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-349">Name the project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="3fd58-350">Entity Framework bağlamına ve hem web hem de çalışan rolü projelerindeki veri modeline başvurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-350">You need to reference the Entity Framework context and the data model from both web and worker role projects.</span></span> <span data-ttu-id="3fd58-351">Alternatif olarak, web rolü projesinde EF ile ilgili sınıfları tanımlayabilir ve çalışan rolü projesinde bu projeye başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fd58-351">As an alternative, you could define the EF-related classes in the web role project and reference that project from the worker role project.</span></span> <span data-ttu-id="3fd58-352">Ancak, alternatif yaklaşımda çalışan rolü projeniz gerekli olmayan web bütünleştirme kodlarına başvuruda bulunur.</span><span class="sxs-lookup"><span data-stu-id="3fd58-352">But in the alternative approach, your worker role project would have a reference to web assemblies that it doesn't need.</span></span>

### <a name="update-and-add-nuget-packages"></a><span data-ttu-id="3fd58-353">NuGet paketlerini güncelleştirme ve ekleme</span><span class="sxs-lookup"><span data-stu-id="3fd58-353">Update and add NuGet packages</span></span>
1. <span data-ttu-id="3fd58-354">Çözüm için **NuGet Paketlerini Yönet** iletişim kutusunu açın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-354">Open the **Manage NuGet Packages** dialog box for the solution.</span></span>
2. <span data-ttu-id="3fd58-355">Pencerenin en üstündeki **Güncelleştirmeler**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-355">At the top of the window, select **Updates**.</span></span>
3. <span data-ttu-id="3fd58-356">*WindowsAzure.Storage* paketini arayın ve listede varsa onu ve içinde güncelleştirileceği web ve çalışan projelerini seçin, ardından **Güncelleştir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-356">Look for the *WindowsAzure.Storage* package, and if it's in the list, select it and select the web and worker projects to update it in, and then click **Update**.</span></span>

    <span data-ttu-id="3fd58-357">Depolama istemcisi kitaplığı Visual Studio proje şablonlarından daha sık güncelleştirildiği için yeni oluşturulan bir projedeki sürümün güncelleştirilmesi gerektiğini sık sık görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3fd58-357">The storage client library is updated more frequently than Visual Studio project templates, so you'll often find that the version in a newly-created project needs to be updated.</span></span>
4. <span data-ttu-id="3fd58-358">Pencerenin en üstünde **Gözat**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-358">At the top of the window, select **Browse**.</span></span>
5. <span data-ttu-id="3fd58-359">*EntityFramework* NuGet paketini bulun ve üç projenin tamamına yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-359">Find the *EntityFramework* NuGet package, and install it in all three projects.</span></span>
6. <span data-ttu-id="3fd58-360">*Microsoft.WindowsAzure.ConfigurationManager* NuGet paketini bulun ve çalışan rolü projesine yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-360">Find the *Microsoft.WindowsAzure.ConfigurationManager* NuGet package, and install it in the worker role project.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="3fd58-361">Proje başvurularını ayarlama</span><span class="sxs-lookup"><span data-stu-id="3fd58-361">Set project references</span></span>
1. <span data-ttu-id="3fd58-362">ContosoAdsWeb projesinde ContosoAdsCommon projesine bir başvuru ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-362">In the ContosoAdsWeb project, set a reference to the ContosoAdsCommon project.</span></span> <span data-ttu-id="3fd58-363">ContosoAdsWeb projesine sağ tıklayın ve ardından **Başvurular** - **Başvuru Ekle** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-363">Right-click the ContosoAdsWeb project, and then click **References** - **Add References**.</span></span> <span data-ttu-id="3fd58-364">**Başvuru Yöneticisi** iletişim kutusunda sol bölmedeki **Çözüm – Projeler** öğesini seçin, **ContosoAdsCommon**’ı seçin ve ardından **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-364">In the **Reference Manager** dialog box, select **Solution – Projects** in the left pane, select **ContosoAdsCommon**, and then click **OK**.</span></span>
2. <span data-ttu-id="3fd58-365">ContosoAdsWorker projesinde ContosoAdsCommon projesine bir başvuru ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-365">In the ContosoAdsWorker project, set a reference to the ContosAdsCommon project.</span></span>

    <span data-ttu-id="3fd58-366">ContosoAdsCommon hem ön uç ve arka uç tarafından kullanılacak olan Entity Framework veri modeli ve bağlam sınıfını içerir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-366">ContosoAdsCommon will contain the Entity Framework data model and context class, which will be used by both the front-end and back-end.</span></span>
3. <span data-ttu-id="3fd58-367">ContosoAdsWorker projesinde bir `System.Drawing` başvurusu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-367">In the ContosoAdsWorker project, set a reference to `System.Drawing`.</span></span>

    <span data-ttu-id="3fd58-368">Bu bütünleştirilmiş kod, görüntüleri küçük resimlere dönüştürmek için arka uç tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-368">This assembly is used by the back-end to convert images to thumbnails.</span></span>

### <a name="configure-connection-strings"></a><span data-ttu-id="3fd58-369">Bağlantı dizelerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3fd58-369">Configure connection strings</span></span>
<span data-ttu-id="3fd58-370">Bu bölümde, yerel olarak test etmek amacıyla Azure Storage ve SQL bağlantı dizelerini yapılandırırsınız.</span><span class="sxs-lookup"><span data-stu-id="3fd58-370">In this section, you configure Azure Storage and SQL connection strings for testing locally.</span></span> <span data-ttu-id="3fd58-371">Öğreticinin önceki bölümlerinde verilen dağıtım yönergeleri, uygulamanın bulutta çalıştığı durumlar için bağlantı dizelerinin nasıl ayarlandığını açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-371">The deployment instructions earlier in the tutorial explain how to set up the connection strings for when the app runs in the cloud.</span></span>

1. <span data-ttu-id="3fd58-372">ContosoAdsWeb projesinde uygulamanın Web.config dosyasını açın ve aşağıdaki `connectionStrings` öğesini `configSections` öğesinden sonra ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-372">In the ContosoAdsWeb project, open the application Web.config file, and insert the following `connectionStrings` element after the `configSections` element.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="3fd58-373">Visual Studio 2015 ve sonraki bir sürümü kullanıyorsanız "v11.0" ifadesini "MSSQLLocalDB" ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-373">If you're using Visual Studio 2015 or higher, replace "v11.0" with "MSSQLLocalDB".</span></span>
2. <span data-ttu-id="3fd58-374">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-374">Save your changes.</span></span>
3. <span data-ttu-id="3fd58-375">ContosoAdsCloudService projesinde **Roller** altındaki ContosoAdsWeb öğesine sağ tıklayın ve ardından **Özellikler**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-375">In the ContosoAdsCloudService project, right-click ContosoAdsWeb under **Roles**, and then click **Properties**.</span></span>

    ![Rol özellikleri](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. <span data-ttu-id="3fd58-377">**ContosAdsWeb [Rolü]** özellikleri penceresinde **Ayarlar** sekmesine ve ardından **Ayar Ekle** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-377">In the **ContosAdsWeb [Role]** properties window, click the **Settings** tab, and then click **Add Setting**.</span></span>

    <span data-ttu-id="3fd58-378">**Hizmet Yapılandırma** ayarını **Tüm Yapılandırmalar** olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-378">Leave **Service Configuration** set to **All Configurations**.</span></span>
5. <span data-ttu-id="3fd58-379">*StorageConnectionString* adlı bir ayar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-379">Add a setting named *StorageConnectionString*.</span></span> <span data-ttu-id="3fd58-380">**Tür** değerini *ConnectionString* olarak, **Değer** seçeneğini *UseDevelopmentStorage=true* olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-380">Set **Type** to *ConnectionString*, and set **Value** to *UseDevelopmentStorage=true*.</span></span>

    ![Yeni bağlantı dizesi](./media/cloud-services-dotnet-get-started/scall.png)
6. <span data-ttu-id="3fd58-382">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-382">Save your changes.</span></span>
7. <span data-ttu-id="3fd58-383">ContosoAdsWorker rol özelliklerine bir depolama bağlantı dizesi eklemek için aynı yordamı izleyin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-383">Follow the same procedure to add a storage connection string in the ContosoAdsWorker role properties.</span></span>
8. <span data-ttu-id="3fd58-384">Hala **ContosoAdsWorker [Rolü]** özellikler penceresindeyken başka bir bağlantı dizesi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3fd58-384">Still in the **ContosoAdsWorker [Role]** properties window, add another connection string:</span></span>

   * <span data-ttu-id="3fd58-385">Ad: ContosoAdsDbConnectionString</span><span class="sxs-lookup"><span data-stu-id="3fd58-385">Name: ContosoAdsDbConnectionString</span></span>
   * <span data-ttu-id="3fd58-386">Türü: Dize</span><span class="sxs-lookup"><span data-stu-id="3fd58-386">Type: String</span></span>
   * <span data-ttu-id="3fd58-387">Değer: Web rolü projesi kullandığınız bağlantı dizesinin aynısını yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-387">Value: Paste the same connection string you used for the web role project.</span></span> <span data-ttu-id="3fd58-388">(Aşağıdaki örnek Visual Studio 2013 içindir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-388">(The following example is for Visual Studio 2013.</span></span> <span data-ttu-id="3fd58-389">Bu örneği kopyalarsanız ve Visual Studio 2015 veya sonraki bir sürümü kullanıyorsanız Veri Kaynağını değiştirmeyi unutmayın.)</span><span class="sxs-lookup"><span data-stu-id="3fd58-389">Don't forget to change the Data Source if you copy this example and you're using Visual Studio 2015 or higher.)</span></span>

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a><span data-ttu-id="3fd58-390">Kod dosyaları ekleme</span><span class="sxs-lookup"><span data-stu-id="3fd58-390">Add code files</span></span>
<span data-ttu-id="3fd58-391">Bu bölümde, indirilen çözümden yeni çözüme kod dosyaları kopyalarsınız.</span><span class="sxs-lookup"><span data-stu-id="3fd58-391">In this section, you copy code files from the downloaded solution into the new solution.</span></span> <span data-ttu-id="3fd58-392">Aşağıdaki bölümlerde bu kodun temel kısımları gösterilmiş ve açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-392">The following sections will show and explain key parts of this code.</span></span>

<span data-ttu-id="3fd58-393">Bir proje veya klasöre dosya eklemek için proje veya klasöre sağ tıklayıp **Ekle** - **Mevcut Öğe** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-393">To add files to a project or a folder, right-click the project or folder and click **Add** - **Existing Item**.</span></span> <span data-ttu-id="3fd58-394">İstediğiniz dosyaları seçin ve ardından **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-394">Select the files you want and then click **Add**.</span></span> <span data-ttu-id="3fd58-395">Mevcut dosyaları değiştirmek isteyip istemediğiniz sorulursa **Evet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-395">If asked whether you want to replace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="3fd58-396">ContosoAdsCommon projesinde *Class1.cs* dosyasını silin ve indirilen projedeki *Ad.cs* ve *ContosoAdscontext.cs* dosyalarını onun yerine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-396">In the ContosoAdsCommon project, delete the *Class1.cs* file and add in its place the *Ad.cs* and *ContosoAdscontext.cs* files from the downloaded project.</span></span>
2. <span data-ttu-id="3fd58-397">ContosoAdsWeb projesinde indirilen projeden aşağıdaki dosyaları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-397">In the ContosoAdsWeb project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="3fd58-398">*Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="3fd58-398">*Global.asax.cs*.</span></span>  
   * <span data-ttu-id="3fd58-399">*Görünümler/Paylaşılan* klasöründe: *\_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="3fd58-399">In the *Views\Shared* folder: *\_Layout.cshtml*.</span></span>
   * <span data-ttu-id="3fd58-400">*Görünümler/Giriş* klasöründe: *Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="3fd58-400">In the *Views\Home* folder: *Index.cshtml*.</span></span>
   * <span data-ttu-id="3fd58-401">*Denetleyiciler* klasöründe: *AdController.cs*.</span><span class="sxs-lookup"><span data-stu-id="3fd58-401">In the *Controllers* folder: *AdController.cs*.</span></span>
   * <span data-ttu-id="3fd58-402">*Görünümler/Reklam* klasöründe (öncelikle klasörü oluşturun): beş *.cshtml* dosyası.</span><span class="sxs-lookup"><span data-stu-id="3fd58-402">In the *Views\Ad* folder (create the folder first): five *.cshtml* files.</span></span>
3. <span data-ttu-id="3fd58-403">ContosoAdsWorker projesinde indirilen projeden *WorkerRole.cs* ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-403">In the ContosoAdsWorker project, add *WorkerRole.cs* from the downloaded project.</span></span>

<span data-ttu-id="3fd58-404">Uygulamayı artık öğreticinin önceki bölümlerinde anlatılan şekilde derleyip çalıştırabilirsiniz; uygulama yerel veritabanı ve depolama öykünücüsü kaynaklarını kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-404">You can now build and run the application as instructed earlier in the tutorial, and the app will use local database and storage emulator resources.</span></span>

<span data-ttu-id="3fd58-405">Aşağıdaki bölümlerde Azure ortamı, blob'ları ve kuyrukları ile çalışmayla ilgili kod açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-405">The following sections explain the code related to working with the Azure environment, blobs, and queues.</span></span> <span data-ttu-id="3fd58-406">Bu öğretici, iskele kurma kullanarak MVC denetleyicilerinin ve görünümlerin nasıl oluşturulacağını, SQL Server veritabanları ile çalışan Entity Framework kodunun nasıl yazılacağını veya ASP.NET 4.5 içinde zaman uyumsuz programlamanın temel bilgilerini açıklamaz.</span><span class="sxs-lookup"><span data-stu-id="3fd58-406">This tutorial does not explain how to create MVC controllers and views using scaffolding, how to write Entity Framework code that works with SQL Server databases, or the basics of asynchronous programming in ASP.NET 4.5.</span></span> <span data-ttu-id="3fd58-407">Bu konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="3fd58-407">For information about these topics, see the following resources:</span></span>

* [<span data-ttu-id="3fd58-408">MVC 5 kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="3fd58-408">Get started with MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="3fd58-409">EF 6 ve MVC 5 kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="3fd58-409">Get started with EF 6 and MVC 5</span></span>](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* <span data-ttu-id="3fd58-410">[.NET 4.5’te zaman uyumsuz programlamaya giriş](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="3fd58-410">[Introduction to asynchronous programming in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="3fd58-411">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="3fd58-411">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="3fd58-412">Ad.cs dosyası reklam kategorileri için bir numaralandırma ve reklam bilgileri için bir POCO varlık sınıfı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3fd58-412">The Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="3fd58-413">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="3fd58-413">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="3fd58-414">ContosoAdsContext sınıfı Reklam sınıfının Entity Framework tarafından bir SQL veritabanına depolanacak olan Db koleksiyonunda kullanıldığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-414">The ContosoAdsContext class specifies that the Ad class is used in a DbSet collection, which Entity Framework will store in a SQL database.</span></span>

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

<span data-ttu-id="3fd58-415">Sınıfın iki oluşturucusu vardır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-415">The class has two constructors.</span></span> <span data-ttu-id="3fd58-416">Birincisi web projesi tarafından kullanılır ve Web.config dosyasına depolanan bir bağlantı dizesinin adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-416">The first of them is used by the web project, and specifies the name of a connection string that is stored in the Web.config file.</span></span> <span data-ttu-id="3fd58-417">İkinci oluşturucu, Web.config dosyasına sahip olmadığı için çalışan rolü projesi tarafından kullanılan gerçek bağlantı dizesini geçirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="3fd58-417">The second constructor enables you to pass in the actual connection string used by the worker role project, since it doesn't have a Web.config file.</span></span> <span data-ttu-id="3fd58-418">Bu bağlantı dizesinin nereye depolandığını daha önce gördünüz ve kodun DbContext sınıfını başlattığında bağlantı dizesini nasıl aldığını daha sonra göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="3fd58-418">You saw earlier where this connection string was stored, and you'll see later how the code retrieves the connection string when it instantiates the DbContext class.</span></span>

### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="3fd58-419">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="3fd58-419">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="3fd58-420">`Application_Start` yönteminden çağrılan kod, henüz yoksa bir *görüntüler* blob kapsayıcısı ve bir *görüntüler* kuyruğu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3fd58-420">Code that is called from the `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="3fd58-421">Bunun yapılması yeni bir depolama hesabını başlattığınız veya depolama öykünücüsünü yeni bir bilgisayarda kullanmaya başladığınız her durumda gerekli blob kapsayıcısının ve kuyruğun otomatik olarak oluşturulmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="3fd58-421">This ensures that whenever you start using a new storage account, or start using the storage emulator on a new computer, the required blob container and queue will be created automatically.</span></span>

<span data-ttu-id="3fd58-422">Kod *.cscfg* dosyasından depolama bağlantı dizesini kullanarak depolama hesabına erişim elde eder.</span><span class="sxs-lookup"><span data-stu-id="3fd58-422">The code gets access to the storage account by using the storage connection string from the *.cscfg* file.</span></span>

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

<span data-ttu-id="3fd58-423">Ardından *görüntüler* blob kapsayıcısına bir başvuru edinir, henüz yoksa kapsayıcıyı oluşturur ve yeni kapsayıcıda erişim izinlerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3fd58-423">Then it gets a reference to the *images* blob container, creates the container if it doesn't already exist, and sets access permissions on the new container.</span></span> <span data-ttu-id="3fd58-424">Varsayılan olarak, yeni kapsayıcılar yalnızca depolama hesabı kimlik bilgilerine sahip istemcilerin blob’lara erişmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-424">By default, new containers only allow clients with storage account credentials to access blobs.</span></span> <span data-ttu-id="3fd58-425">Web sitesi, görüntü blob’larını işaret eden URL’leri kullanarak görüntüleri gösterebilmek için blob’ların herkese açık olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-425">The website needs the blobs to be public so that it can display images using URLs that point to the image blobs.</span></span>

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

<span data-ttu-id="3fd58-426">Benzer bir kod, *görüntüler* kuyruğuna başvuru edinir ve yeni bir kuyruk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3fd58-426">Similar code gets a reference to the *images* queue and creates a new queue.</span></span> <span data-ttu-id="3fd58-427">Bu durumda hiçbir izin değişikliğine gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="3fd58-427">In this case, no permissions change is needed.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="3fd58-428">ContosoAdsWeb - \_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="3fd58-428">ContosoAdsWeb - \_Layout.cshtml</span></span>
<span data-ttu-id="3fd58-429">*_Layout.cshtml* dosyası üst bilgi ve alt bilgide uygulama adını ayarlar ve bir "Reklamlar" menü girişi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3fd58-429">The *_Layout.cshtml* file sets the app name in the header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="3fd58-430">ContosoAdsWeb - Görünümler\Giriş\Dizin.cshtml</span><span class="sxs-lookup"><span data-stu-id="3fd58-430">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="3fd58-431">*Görünümler\Giriş\Dizin.cshtml* dosyası, giriş sayfasında kategori bağlantılarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-431">The *Views\Home\Index.cshtml* file displays category links on the home page.</span></span> <span data-ttu-id="3fd58-432">Bağlantılar `Category` numaralandırmasının bir sorgu dizesi değişkeni içindeki tamsayı değerini Reklam Dizini sayfasına geçirir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-432">The links pass the integer value of the `Category` enum in a querystring variable to the Ads Index page.</span></span>

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="3fd58-433">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="3fd58-433">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="3fd58-434">Oluşturucu, *AdController.cs* dosyasında blob’larla ve kuyruklarla çalışmaya yönelik bir API sağlayan Azure Storage İstemci Kitaplığı nesneleri oluşturmak için `InitializeStorage` yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-434">In the *AdController.cs* file, the constructor calls the `InitializeStorage` method to create Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="3fd58-435">Ardından kod daha önce gördüğünüz gibi *görüntüler* blob kapsayıcısı için *Global.asax.cs* içinde bir başvuru edinir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-435">Then the code gets a reference to the *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="3fd58-436">Bunu yaparken bir web uygulaması için uygun bir varsayılan [yeniden deneme ilkesi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3fd58-436">While doing that it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="3fd58-437">Varsayılan üstel geri alma yeniden deneme ilkesi, web uygulamasını geçici bir hata için tekrarlanan yeniden denemelerde bir dakikadan uzun süre askıya alabilir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-437">The default exponential backoff retry policy could hang the web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="3fd58-438">Burada belirtilen yeniden deneme ilkesi üç denemeye kadar her denemeden sonra en fazla üç saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="3fd58-438">The retry policy specified here waits three seconds after each try for up to three tries.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

<span data-ttu-id="3fd58-439">Benzer bir kod, *görüntüler* kuyruğuna başvuru edinir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-439">Similar code gets a reference to the *images* queue.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

<span data-ttu-id="3fd58-440">Denetleyici kodlarının birçoğu bir DbContext sınıfı kullanarak Entity Framework veri modeli ile çalışmak için tipiktir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-440">Most of the controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="3fd58-441">Dosyayı karşıya yükleyen ve blob depolama alanına kaydeden HttpPost `Create` yöntemi bunun bir istisnasıdır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-441">An exception is the HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="3fd58-442">Model bağlayıcı, yönteme bir [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) nesnesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="3fd58-442">The model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object to the method.</span></span>

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

<span data-ttu-id="3fd58-443">Kullanıcı karşıya yüklemek için bir dosya seçtiyse kod bu dosyayı karşıya yükler, bir blob'a kaydeder ve Ad veritabanı kaydını blob’a işaret eden bir URL ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-443">If the user selected a file to upload, the code uploads the file, saves it in a blob, and updates the Ad database record with a URL that points to the blob.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

<span data-ttu-id="3fd58-444">Karşıya yüklemeyi yapan kod `UploadAndSaveBlobAsync` yöntemindedir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-444">The code that does the upload is in the `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="3fd58-445">Blob için bir GUID adı oluşturur, dosyayı karşıya yükler ve kaydeder ve kaydedilmiş blob için bir başvuru döndürür.</span><span class="sxs-lookup"><span data-stu-id="3fd58-445">It creates a GUID name for the blob, uploads and saves the file, and returns a reference to the saved blob.</span></span>

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

<span data-ttu-id="3fd58-446">HttpPost `Create` yöntemi bir blob’u karşıya yükleyip veritabanını güncelleştirdikten sonra bir görüntünün küçük resme dönüştürme için hazır olduğunu ilgili arka uç işlemine bildirmek üzere bir kuyruk iletisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3fd58-446">After the HttpPost `Create` method uploads a blob and updates the database, it creates a queue message to inform that back-end process that an image is ready for conversion to a thumbnail.</span></span>

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

<span data-ttu-id="3fd58-447">Kullanıcının yeni bir görüntü dosyası seçtiği durumlarda zaten mevcut blob’ların silinmesinin gerekli olması dışında HttpPost `Edit` yönteminin kodu aynıdır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-447">The code for the HttpPost `Edit` method is similar except that if the user selects a new image file any blobs that already exist must be deleted.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

<span data-ttu-id="3fd58-448">Sonraki örnekte bir reklamı sildiğinizde blob'ları silen kod gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-448">The next example shows the code that deletes blobs when you delete an ad.</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="3fd58-449">ContosoAdsWeb - Views\Ad\Index.cshtml ve Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="3fd58-449">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="3fd58-450">*Index.cshtml* dosyası küçük resimleri diğer reklam verileriyle birlikte gösterir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-450">The *Index.cshtml* file displays thumbnails with the other ad data.</span></span>

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

<span data-ttu-id="3fd58-451">*Details.cshtml* dosyası tam boyutlu görüntüyü gösterir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-451">The *Details.cshtml* file displays the full-size image.</span></span>

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="3fd58-452">ContosoAdsWeb - Views\Ad\Create.cshtml ve Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="3fd58-452">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="3fd58-453">*Create.cshtml* ve *Edit.cshtml* dosyaları denetleyicinin `HttpPostedFileBase` nesnesi almasını sağlayan form kodlamasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-453">The *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables the controller to get the `HttpPostedFileBase` object.</span></span>

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

<span data-ttu-id="3fd58-454">Bir `<input>` öğesi tarayıcıya bir dosya seçme iletişim kutusu açmasını söyler.</span><span class="sxs-lookup"><span data-stu-id="3fd58-454">An `<input>` element tells the browser to provide a file selection dialog.</span></span>

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a><span data-ttu-id="3fd58-455">ContosoAdsWorker - WorkerRole.cs - OnStart yöntemi</span><span class="sxs-lookup"><span data-stu-id="3fd58-455">ContosoAdsWorker - WorkerRole.cs - OnStart method</span></span>
<span data-ttu-id="3fd58-456">Azure çalışan rolü ortamı, çalışan rolü başlatılırken `WorkerRole` sınıfındaki `OnStart` yöntemini, `OnStart` yöntemi tamamlandığında ise `Run` yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-456">The Azure worker role environment calls the `OnStart` method in the `WorkerRole` class when the worker role is getting started, and it calls the `Run` method when the `OnStart` method finishes.</span></span>

<span data-ttu-id="3fd58-457">`OnStart` yöntemi *.cscfg* dosyasından veritabanı bağlantı dizesini alır ve Entity Framework DbContext sınıfına geçirir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-457">The `OnStart` method gets the database connection string from the *.cscfg* file and passes it to the Entity Framework DbContext class.</span></span> <span data-ttu-id="3fd58-458">Varsayılan olarak SQLClient sağlayıcısı kullanılır, bu nedenle sağlayıcının belirtilmesi gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-458">The SQLClient provider is used by default, so the provider does not have to be specified.</span></span>

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

<span data-ttu-id="3fd58-459">Bundan sonra yöntem, depolama hesabı için bir başvuru alır ve yoksa blob kapsayıcısı ve kuyruk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3fd58-459">After that, the method gets a reference to the storage account and creates the blob container and queue if they don't exist.</span></span> <span data-ttu-id="3fd58-460">Bunun kodu, web rolü `Application_Start` yönteminde daha önce gördüğünüzle aynıdır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-460">The code for that is similar to what you already saw in the web role `Application_Start` method.</span></span>

### <a name="contosoadsworker---workerrolecs---run-method"></a><span data-ttu-id="3fd58-461">ContosoAdsWorker - WorkerRole.cs - Run yöntemi</span><span class="sxs-lookup"><span data-stu-id="3fd58-461">ContosoAdsWorker - WorkerRole.cs - Run method</span></span>
<span data-ttu-id="3fd58-462">`OnStart` yöntemi başlatma işini tamamladığında `Run` yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-462">The `Run` method is called when the `OnStart` method finishes its initialization work.</span></span> <span data-ttu-id="3fd58-463">Yöntem yeni bir kuyruk iletisi bekleyen ve ulaşan iletileri işleyen sonsuz bir döngü yürütür.</span><span class="sxs-lookup"><span data-stu-id="3fd58-463">The method executes an infinite loop that watches for new queue messages and processes them when they arrive.</span></span>

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

<span data-ttu-id="3fd58-464">Döngünün her yinelemesinden sonra herhangi bir kuyruk iletisi bulunmazsa program bir saniye için uyku moduna geçer.</span><span class="sxs-lookup"><span data-stu-id="3fd58-464">After each iteration of the loop, if no queue message was found, the program sleeps for a second.</span></span> <span data-ttu-id="3fd58-465">Bunun yapılması çalışan rolünün aşırı CPU süresi ve depolama işlem maliyetleri doğurmasını engeller.</span><span class="sxs-lookup"><span data-stu-id="3fd58-465">This prevents the worker role from incurring excessive CPU time and storage transaction costs.</span></span> <span data-ttu-id="3fd58-466">Microsoft Müşteri Danışma Ekibi bunu dahil etmeyi unutan, üretime dağıtan ve tatile giden bir geliştiricinin hikayesini anlatır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-466">The Microsoft Customer Advisory Team tells a story about a  developer who forgot to include this, deployed to production, and left for vacation.</span></span> <span data-ttu-id="3fd58-467">Geri döndüğünde gözetim maliyeti tatilin maliyetini aşmıştı.</span><span class="sxs-lookup"><span data-stu-id="3fd58-467">When he got back, his oversight cost more than the vacation.</span></span>

<span data-ttu-id="3fd58-468">Bazı durumlarda bir kuyruk iletisinin içeriği işlemede hataya neden olur.</span><span class="sxs-lookup"><span data-stu-id="3fd58-468">Sometimes the content of a queue message causes an error in processing.</span></span> <span data-ttu-id="3fd58-469">Buna *zehir iletisi* adı verilir ve bir hatayı günlüğe kaydedip döngüyü yeniden başlatırsanız bu iletiyi sonu gelmez bir şekilde işlemeye çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fd58-469">This is called a *poison message*, and if you just logged an error and restarted the loop, you could endlessly try to process that message.</span></span>  <span data-ttu-id="3fd58-470">Bu nedenle, yakalama bloğu uygulamanın geçerli iletiyi işlemeyi kaç kez denediğini denetleyen bir if deyimi içerir ve 5’ten fazla kez denediyse ileti kuyruktan silinir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-470">Therefore the catch block includes an if statement that checks to see how many times the app has tried to process the current message, and if it has been more than 5 times, the message is deleted from the queue.</span></span>

<span data-ttu-id="3fd58-471">Bir kuyruk iletisi bulunduğunda `ProcessQueueMessage` çağrılır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-471">`ProcessQueueMessage` is called when a queue message is found.</span></span>

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

<span data-ttu-id="3fd58-472">Bu kod, görüntü URL’sini almak için veritabanını okur, görüntüyü bir küçük resme dönüştürür, küçük resmi bir blob’a kaydeder, veritabanını küçük resim blob URL’si ile güncelleştirir ve kuyruk iletisini siler.</span><span class="sxs-lookup"><span data-stu-id="3fd58-472">This code reads the database to get the image URL, converts the image to a thumbnail, saves the thumbnail in a blob, updates the database with the thumbnail blob URL, and deletes the queue message.</span></span>

> [!NOTE]
> <span data-ttu-id="3fd58-473">`ConvertImageToThumbnailJPG` yöntemindeki kod kolaylık için System.Drawing ad alanındaki sınıfları kullanır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-473">The code in the `ConvertImageToThumbnailJPG` method uses classes in the System.Drawing namespace for simplicity.</span></span> <span data-ttu-id="3fd58-474">Ancak, bu ad alanındaki sınıflar Windows Forms ile kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-474">However, the classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="3fd58-475">Bir Windows veya ASP.NET hizmetinde kullanılması desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="3fd58-475">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="3fd58-476">Görüntü işleme seçenekleri hakkında daha fazla bilgi için bkz. [Dinamik Görüntü Oluşturma](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) ve [Görüntü Yeniden Boyutlandırmaya Ayrıntılı Bakış](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span><span class="sxs-lookup"><span data-stu-id="3fd58-476">For more information about image-processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="troubleshooting"></a><span data-ttu-id="3fd58-477">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="3fd58-477">Troubleshooting</span></span>
<span data-ttu-id="3fd58-478">Bu öğreticideki yönergeleri izlerken bir sorun oluşması durumunda bazı yaygın hatalar ve çözümleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-478">In case something doesn't work while you're following the instructions in this tutorial, here are some common errors and how to resolve them.</span></span>

### <a name="serviceruntimeroleenvironmentexception"></a><span data-ttu-id="3fd58-479">ServiceRuntime.RoleEnvironmentException</span><span class="sxs-lookup"><span data-stu-id="3fd58-479">ServiceRuntime.RoleEnvironmentException</span></span>
<span data-ttu-id="3fd58-480">Uygulamayı Azure’da çalıştırdığınızda ya da Azure işlem öykünücüsü kullanarak yerel olarak çalıştırdığınızda Azure tarafından `RoleEnvironment` nesnesi sağlanır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-480">The `RoleEnvironment` object is provided by Azure when you run an application in Azure or when you run locally using the Azure compute emulator.</span></span>  <span data-ttu-id="3fd58-481">Yerel olarak çalıştırırken bu hatayı alırsanız ContosoAdsCloudService projesini başlangıç projesi olarak ayarladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3fd58-481">If you get this error when you're running locally, make sure that you have set the ContosoAdsCloudService project as the startup project.</span></span> <span data-ttu-id="3fd58-482">Bunun yapılması projeyi Azure işlem öykünücüsü kullanarak çalışacak şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3fd58-482">This sets up the project to run using the Azure compute emulator.</span></span>

<span data-ttu-id="3fd58-483">Uygulamanın Azure RoleEnvironment’ı kullanmasının bir nedeni *.cscfg* dosyalarına depolanmış bağlantı dizelerinin alınmasıdır; dolayısıyla bu özel durumun başka bir nedeni de eksik bir bağlantı dizesidir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-483">One of the things the application uses the Azure RoleEnvironment for is to get the connection string values that are stored in the *.cscfg* files, so another cause of this exception is a missing connection string.</span></span> <span data-ttu-id="3fd58-484">ContosoAdsWeb projesinde hem Bulut hem de Yerel yapılandırmaları için StorageConnectionString ayarını oluşturduğunuzdan ve ContosoAdsWorker projesinde her iki yapılandırma için iki bağlantı dizesini de oluşturduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3fd58-484">Make sure that you created the StorageConnectionString setting for both Cloud and Local configurations in the ContosoAdsWeb project, and that you created both connection strings for both configurations in the ContosoAdsWorker project.</span></span> <span data-ttu-id="3fd58-485">StorageConnectionString için çözümün tamamında **Tümünü Bul** araması yaparsanız 6 dosyada 9 kez görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-485">If you do a **Find All** search for StorageConnectionString in the entire solution, you should see it 9 times in 6 files.</span></span>

### <a name="cannot-override-to-port-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a><span data-ttu-id="3fd58-486">xxx bağlantı noktası için geçersiz kılınamıyor.</span><span class="sxs-lookup"><span data-stu-id="3fd58-486">Cannot override to port xxx.</span></span> <span data-ttu-id="3fd58-487">Yeni bağlantı noktası http protokolü için izin verilen en düşük 8080 değerinin altında</span><span class="sxs-lookup"><span data-stu-id="3fd58-487">New port below minimum allowed value 8080 for protocol http</span></span>
<span data-ttu-id="3fd58-488">Web projesi tarafından kullanılan bağlantı noktası numarasını değiştirmeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-488">Try changing the port number used by the web project.</span></span> <span data-ttu-id="3fd58-489">ContosoAdsWeb projesine sağ tıklayın ve ardından **Özellikler** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-489">Right-click the ContosoAdsWeb project, and then click **Properties**.</span></span> <span data-ttu-id="3fd58-490">**Web** sekmesine tıklayın ve ardından **Proje Url’si** ayarında bağlantı noktası numarasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3fd58-490">Click the **Web** tab, and then change the port number in the **Project Url** setting.</span></span>

<span data-ttu-id="3fd58-491">Sorunu çözebilecek başka bir alternatif için sonraki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-491">For another alternative that might resolve the problem, see the following  section.</span></span>

### <a name="other-errors-when-running-locally"></a><span data-ttu-id="3fd58-492">Yerel olarak çalışırken oluşan diğer hatalar</span><span class="sxs-lookup"><span data-stu-id="3fd58-492">Other errors when running locally</span></span>
<span data-ttu-id="3fd58-493">Varsayılan olarak yeni bulut hizmeti projeleri, Azure ortamının benzetimini yapmak için Azure işlem öykünücüsü kullanır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-493">By default new cloud service projects use the Azure compute emulator express to simulate the Azure environment.</span></span> <span data-ttu-id="3fd58-494">Bu, tam işlem öykünücüsünün hafif sürümüdür ve hızlı sürümün çalışmadığı bazı koşullarda tam öykünücü çalışır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-494">This is a lightweight version of the full compute emulator, and under some conditions the full emulator will work when the express version does not.</span></span>  

<span data-ttu-id="3fd58-495">Projeyi tam öykünücü kullanacak şekilde değiştirmek için ContosoAdsCloudService projesine sağ tıklayın ve ardından **Özellikler**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-495">To change the project to use the full emulator, right-click the ContosoAdsCloudService project, and then click **Properties**.</span></span> <span data-ttu-id="3fd58-496">**Özellikler** penceresinde **Web** sekmesine ve ardından **Tam Öykünücü Kullan** radyo düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fd58-496">In the **Properties** window click the **Web** tab, and then click the **Use Full Emulator** radio button.</span></span>

<span data-ttu-id="3fd58-497">Uygulamayı tam öykünücü ile çalıştırmak için Visual Studio’yu yönetici ayrıcalıklarıyla açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-497">In order to run the application with the full emulator, you have to open Visual Studio with administrator privileges.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fd58-498">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3fd58-498">Next steps</span></span>
<span data-ttu-id="3fd58-499">Contoso Ads uygulaması bir başlangıç öğreticisi için kasıtlı olarak basit tutulmuştur.</span><span class="sxs-lookup"><span data-stu-id="3fd58-499">The Contoso Ads application has intentionally been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="3fd58-500">Örneğin, [bağımlılık ekleme](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) veya [depo ve iş birimi düzenleri](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo) uygulamaz, [günlüğe kaydetme arabirimi yoktur](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), veri modeli değişikliklerini yönetmek için [EF Code First Geçişleri](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) veya geçici ağ hatalarını yönetmek için [EF Bağlantı Dayanıklılığı](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) kullanmaz, vb.</span><span class="sxs-lookup"><span data-stu-id="3fd58-500">For example, it doesn't implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) or the [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), it doesn't [use an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), it doesn't use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) to manage data model changes or [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) to manage transient network errors, and so forth.</span></span>

<span data-ttu-id="3fd58-501">Daha gerçek kodlama uygulamalarını gösteren bazı bulut hizmeti örnek uygulamaları en az karmaşık olandan en karmaşığa doğru aşağıda listelenmiştir:</span><span class="sxs-lookup"><span data-stu-id="3fd58-501">Here are some cloud service sample applications that demonstrate more real-world coding practices, listed from less complex to more complex:</span></span>

* <span data-ttu-id="3fd58-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span><span class="sxs-lookup"><span data-stu-id="3fd58-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span></span> <span data-ttu-id="3fd58-503">Contoso Ads uygulamasıyla kavram olarak benzerdir, ancak daha fazla özellik ve daha gerçek kodlama uygulamaları kullanır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-503">Similar in concept to Contoso Ads but implements more features and more real-world coding practices.</span></span>
* <span data-ttu-id="3fd58-504">[Tablolar, Kuyruklar ve Blob’lar ile Azure Cloud Service Çok Katmanlı Uygulaması](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span><span class="sxs-lookup"><span data-stu-id="3fd58-504">[Azure Cloud Service Multi-Tier Application with Tables, Queues, and Blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span></span> <span data-ttu-id="3fd58-505">Azure Storage tablolarının yanı sıra blob’ları ve kuyrukları tanıtır.</span><span class="sxs-lookup"><span data-stu-id="3fd58-505">Introduces Azure Storage tables as well as blobs and queues.</span></span> <span data-ttu-id="3fd58-506">.NET için daha eski bir Azure SDK sürümünü temel alır ve geçerli sürümle çalışmak için bazı değişiklikler gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-506">Based on an older version of the Azure SDK for .NET, will require some modifications to work with the current version.</span></span>
* <span data-ttu-id="3fd58-507">[Microsoft Azure’da Bulut Hizmeti Temel Bilgileri](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span><span class="sxs-lookup"><span data-stu-id="3fd58-507">[Cloud Service Fundamentals in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span></span> <span data-ttu-id="3fd58-508">Microsoft Patterns and Practices grubu tarafından oluşturulan çok çeşitli en iyi yöntemleri gösteren kapsamlı bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="3fd58-508">A comprehensive sample demonstrating a wide range of best practices, produced by the Microsoft Patterns and Practices group.</span></span>

<span data-ttu-id="3fd58-509">Bulut için geliştirme hakkında genel bilgi için bkz. [Azure ile Gerçek Bulut Uygulamaları Derleme](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span><span class="sxs-lookup"><span data-stu-id="3fd58-509">For general information about developing for the cloud, see [Building Real-World Cloud Apps with Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span></span>

<span data-ttu-id="3fd58-510">Azure Storage’da en iyi yöntemler ve yaklaşımlar hakkında bir tanıtım için bkz. [Microsoft Azure Storage – Yenilikler, En İyi Yöntemler ve Yaklaşımlar](http://channel9.msdn.com/Events/Build/2014/3-628).</span><span class="sxs-lookup"><span data-stu-id="3fd58-510">For a video introduction to Azure Storage best practices and patterns, see [Microsoft Azure Storage – What's New, Best Practices and Patterns](http://channel9.msdn.com/Events/Build/2014/3-628).</span></span>

<span data-ttu-id="3fd58-511">Daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="3fd58-511">For more information, see the following resources:</span></span>

* [<span data-ttu-id="3fd58-512">Azure Cloud Services Bölüm 1: Giriş</span><span class="sxs-lookup"><span data-stu-id="3fd58-512">Azure Cloud Services Part 1: Introduction</span></span>](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [<span data-ttu-id="3fd58-513">Cloud Services nasıl yönetilir?</span><span class="sxs-lookup"><span data-stu-id="3fd58-513">How to manage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="3fd58-514">Azure Depolama</span><span class="sxs-lookup"><span data-stu-id="3fd58-514">Azure Storage</span></span>](/documentation/services/storage/)
* [<span data-ttu-id="3fd58-515">Bulut hizmeti sağlayıcısı seçme</span><span class="sxs-lookup"><span data-stu-id="3fd58-515">How to choose a cloud service provider</span></span>](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
