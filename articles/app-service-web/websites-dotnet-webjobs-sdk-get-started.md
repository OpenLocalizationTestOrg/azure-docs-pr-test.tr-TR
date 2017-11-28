---
title: Azure App Service'te bir .NET WebJob aaaCreate | Microsoft Docs
description: "ASP.NET MVC ve Azure kullanarak çok katmanlı bir uygulama oluşturun. Azure App Service'in web uygulamasında ön uç çalıştırmalarında hello ve arka uç çalıştığı bir Web işi hello. Merhaba uygulama Entity Framework, SQL Database ve Azure depolama kuyrukları ve blobları kullanır."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/14/2017
ms.author: glenga
ms.openlocfilehash: d92fc4b81cc0d58f8e900f257e747af56d32b911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a><span data-ttu-id="f18a7-105">Azure Uygulama Hizmeti’nde .NET WebJob oluşturma</span><span class="sxs-lookup"><span data-stu-id="f18a7-105">Create a .NET WebJob in Azure App Service</span></span>
<span data-ttu-id="f18a7-106">Bu öğretici nasıl toowrite hello kullanan basit bir çok katmanlı ASP.NET MVC 5 uygulaması için kod gösterir [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="f18a7-106">This tutorial shows how toowrite code for a simple multi-tier ASP.NET MVC 5 application that uses hello [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="f18a7-107">Merhaba hello amacı [WebJobs SDK](websites-webjobs-resources.md) toosimplify hello kodu yazma için bir Web işi gerçekleştirebilirsiniz, görüntü işleme, sıra işleme, RSS toplama, dosya bakımı gibi genel görevleri ve e-postaları gönderme.</span><span class="sxs-lookup"><span data-stu-id="f18a7-107">hello purpose of hello [WebJobs SDK](websites-webjobs-resources.md) is toosimplify hello code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="f18a7-108">Merhaba Web işleri SDK'si, Azure Storage ve Service Bus ile çalışmak için görev zamanlama ve hataları işleme ve diğer birçok yaygın senaryolar için yerleşik özelliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-108">hello WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="f18a7-109">Ayrıca, sahip toobe Genişletilebilir tasarlanmış ve var olan bir [uzantıları için açık kaynak deposu](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span><span class="sxs-lookup"><span data-stu-id="f18a7-109">In addition, it's designed toobe extensible, and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="f18a7-110">Merhaba örnek uygulama bir reklam Bülteni panosudur.</span><span class="sxs-lookup"><span data-stu-id="f18a7-110">hello sample application is an advertising bulletin board.</span></span> <span data-ttu-id="f18a7-111">Kullanıcılar yansımaları reklamları için karşıya yükleyebilir ve bir arka uç işlem hello görüntüleri toothumbnails dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="f18a7-111">Users can upload images for ads, and a backend process converts hello images toothumbnails.</span></span> <span data-ttu-id="f18a7-112">Merhaba ad listesi sayfası hello küçük resimleri gösterir ve hello ad Ayrıntılar sayfası hello tam boyutlu görüntüyü gösterir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-112">hello ad list page shows hello thumbnails, and hello ad details page shows hello full-size image.</span></span> <span data-ttu-id="f18a7-113">Bir ekran görüntüsü aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f18a7-113">Here's a screenshot:</span></span>

![Reklam listesi](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

<span data-ttu-id="f18a7-115">Bu örnek uygulama ile çalışır [Azure kuyrukları](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) ve [Azure BLOB'ları](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="f18a7-115">This sample application works with [Azure queues](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) and [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span></span> <span data-ttu-id="f18a7-116">Merhaba öğretici nasıl toodeploy hello uygulama çok gösterir[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) ve [Azure SQL veritabanı](http://msdn.microsoft.com/library/azure/ee336279).</span><span class="sxs-lookup"><span data-stu-id="f18a7-116">hello tutorial shows how toodeploy hello application too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span></span>

## <span data-ttu-id="f18a7-117"><a id="prerequisites"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="f18a7-117"><a id="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="f18a7-118">Merhaba Öğreticisi, bildiğinizi varsayar nasıl toowork ile [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) Visual Studio projelerinde.</span><span class="sxs-lookup"><span data-stu-id="f18a7-118">hello tutorial assumes that you know how toowork with [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projects in Visual Studio.</span></span>

<span data-ttu-id="f18a7-119">Merhaba öğretici ilk olarak Visual Studio 2013 için yazılmıştır, ancak Visual Studio'nun daha yeni sürümlerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-119">hello tutorial was originally written for Visual Studio 2013, but can be used with later versions of Visual Studio.</span></span> <span data-ttu-id="f18a7-120">Visual Studio 2015 veya 2017 kullanıyorsanız, hello uygulamayı yerel olarak çalıştırmadan önce hello değiştirmelisiniz Not `Data Source` hello Web.config ve App.config dosyalarından hello SQL Server yerel veritabanı bağlantı dizesinde parçası `Data Source=(localdb)\v11.0` çok`Data Source=(LocalDb)\MSSQLLocalDB`.</span><span class="sxs-lookup"><span data-stu-id="f18a7-120">If you are using Visual Studio 2015 or 2017, make note that before you run hello application locally, you must change hello `Data Source` part of hello SQL Server LocalDB connection string in hello Web.config and App.config files from `Data Source=(localdb)\v11.0` too`Data Source=(LocalDb)\MSSQLLocalDB`.</span></span>

> [!NOTE]
> <span data-ttu-id="f18a7-121"><a name="note"></a>Bu öğretici bir Azure hesabı toocomplete olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="f18a7-121"><a name="note"></a>You must have an Azure account toocomplete this tutorial:</span></span>
>
> * <span data-ttu-id="f18a7-122">Yapabilecekleriniz [ücretsiz bir Azure hesabı açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): Ücretli Azure hizmetlerini tootry çıkışı kullanabilirsiniz, ve hatta kullanıldıktan sonra hello hesabı sürdürebilir ve Web siteleri gibi ücretsiz Azure hizmetlerinden faydalanabilirsiniz krediler alırsınız.</span><span class="sxs-lookup"><span data-stu-id="f18a7-122">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): You get credits that you can use tootry out paid Azure services, and even after they're used up, you can keep hello account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="f18a7-123">Açıkça ayarlarınızı değiştirip ücret toobe isteyin sürece kredi kartınız asla ücretlendirilir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-123">Your credit card will never be charged, unless you explicitly change your settings and ask toobe charged.</span></span>
> * <span data-ttu-id="f18a7-124">Yapabilecekleriniz [Visual Studio aboneleri için aylık Azure kredi etkinleştirme](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): aboneliğinizi Ücretli Azure hizmetlerinizi kullanabildiğiniz her ay kredi verir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-124">You can [activate Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): Your subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="f18a7-125">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f18a7-125">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f18a7-126">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f18a7-126">No credit cards required; no commitments.</span></span>
>
>

## <span data-ttu-id="f18a7-127"><a id="learn"></a>Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="f18a7-127"><a id="learn"></a>What you'll learn</span></span>
<span data-ttu-id="f18a7-128">Merhaba öğretici nasıl toodo hello aşağıdaki görevleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="f18a7-128">hello tutorial shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="f18a7-129">(Yalnızca Visual Studio 2013 ve 2015 kullanıcılar için) hello Azure SDK'sı yükleyerek makinenizi Azure geliştirme için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f18a7-129">Enable your machine for Azure development by installing hello Azure SDK (only for Visual Studio 2013 and 2015 users).</span></span>
* <span data-ttu-id="f18a7-130">Merhaba ilişkili web projesi dağıttığınızda, bir Azure Web işi otomatik olarak dağıtan bir konsol uygulama projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f18a7-130">Create a Console Application project that automatically deploys as an Azure WebJob when you deploy hello associated web project.</span></span>
* <span data-ttu-id="f18a7-131">Web işleri SDK'si arka uç hello geliştirme bilgisayarındaki yerel olarak test edin.</span><span class="sxs-lookup"><span data-stu-id="f18a7-131">Test a WebJobs SDK backend locally on hello development computer.</span></span>
* <span data-ttu-id="f18a7-132">App Service'te bir Web işleri arka uç tooa web uygulaması ile uygulama yayımlama.</span><span class="sxs-lookup"><span data-stu-id="f18a7-132">Publish an application with a WebJobs backend tooa web app in App Service.</span></span>
* <span data-ttu-id="f18a7-133">Dosyaları karşıya yükleme ve hello Azure Blob hizmeti depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f18a7-133">Upload files and store them in hello Azure Blob service.</span></span>
* <span data-ttu-id="f18a7-134">Hello Azure WebJobs SDK toowork Azure Storage kuyruklarını ve BLOB'ları kullanın.</span><span class="sxs-lookup"><span data-stu-id="f18a7-134">Use hello Azure WebJobs SDK toowork with Azure Storage queues and blobs.</span></span>

## <span data-ttu-id="f18a7-135"><a id="contosoads"></a>Uygulama mimarisi</span><span class="sxs-lookup"><span data-stu-id="f18a7-135"><a id="contosoads"></a>Application architecture</span></span>
<span data-ttu-id="f18a7-136">Merhaba örnek uygulamanın kullandığı hello [kuyruk merkezli çalışma deseni](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff yük hello CPU yoğunluklu iş küçük resimleri tooa arka uç işlem oluşturma.</span><span class="sxs-lookup"><span data-stu-id="f18a7-136">hello sample application uses hello [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff-load hello CPU-intensive work of creating thumbnails tooa backend process.</span></span>

<span data-ttu-id="f18a7-137">Merhaba uygulama ads Entity Framework Code First toocreate hello tabloları ve erişim hello verilerini kullanarak bir SQL veritabanında depolar.</span><span class="sxs-lookup"><span data-stu-id="f18a7-137">hello app stores ads in a SQL database, using Entity Framework Code First toocreate hello tables and access hello data.</span></span> <span data-ttu-id="f18a7-138">Her ad için hello veritabanı iki URL depolar: hello tam boyutlu görüntüyü, diğeri hello küçük resim için için.</span><span class="sxs-lookup"><span data-stu-id="f18a7-138">For each ad, hello database stores two URLs: one for hello full-size image and one for hello thumbnail.</span></span>

![Reklam tablosu](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

<span data-ttu-id="f18a7-140">Ne zaman bir kullanıcı karşıya yükleyen bir görüntü, hello web uygulaması hello görüntüde depolayan bir [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), ve hello veritabanı toohello blob'u işaret eden bir URL ile Merhaba ad bilgilerini depolar.</span><span class="sxs-lookup"><span data-stu-id="f18a7-140">When a user uploads an image, hello web app stores hello image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores hello ad information in hello database with a URL that points toohello blob.</span></span> <span data-ttu-id="f18a7-141">AT hello aynı zaman, ileti tooan Azure kuyruk yazar.</span><span class="sxs-lookup"><span data-stu-id="f18a7-141">At hello same time, it writes a message tooan Azure queue.</span></span> <span data-ttu-id="f18a7-142">Bir Azure Web işi çalışan bir arka uç işleminde hello Web işleri SDK'si hello sıra yeni iletiler için yoklar.</span><span class="sxs-lookup"><span data-stu-id="f18a7-142">In a backend process running as an Azure WebJob, hello WebJobs SDK polls hello queue for new messages.</span></span> <span data-ttu-id="f18a7-143">Yeni bir ileti görüntülendiğinde, görüntü için bir küçük resim hello Web işi oluşturur ve küçük resim URL'si veritabanı alanını bu reklam güncelleştirmeleri hello.</span><span class="sxs-lookup"><span data-stu-id="f18a7-143">When a new message appears, hello WebJob creates a thumbnail for that image and updates hello thumbnail URL database field for that ad.</span></span> <span data-ttu-id="f18a7-144">Merhaba uygulaması hello bölümlerini nasıl etkileşim kurduğu gösterilmektedir bir diyagram şöyledir:</span><span class="sxs-lookup"><span data-stu-id="f18a7-144">Here's a diagram that shows how hello parts of hello application interact:</span></span>

![Contoso Ads mimarisi](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
<span data-ttu-id="f18a7-146">Merhaba öğretici yönergeleri uygulayın tooAzure SDK .NET 2.7.1 veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="f18a7-146">hello tutorial instructions apply tooAzure SDK for .NET 2.7.1 or later.</span></span>

## <span data-ttu-id="f18a7-147"><a id="storage"></a>Bir Azure depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f18a7-147"><a id="storage"></a>Create an Azure Storage account</span></span>
<span data-ttu-id="f18a7-148">Bir Azure depolama hesabı, kuyruk ve blob verilerini hello bulutta depolamak için kaynaklar sağlar.</span><span class="sxs-lookup"><span data-stu-id="f18a7-148">An Azure storage account provides resources for storing queue and blob data in hello cloud.</span></span> <span data-ttu-id="f18a7-149">Merhaba Pano için Web işleri SDK'si toostore günlük verilerini hello tarafından da kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f18a7-149">It's also used by hello WebJobs SDK toostore logging data for hello dashboard.</span></span>

<span data-ttu-id="f18a7-150">Gerçek dünya uygulamada genellikle uygulama verilerine karşı günlük verileri için ayrı hesaplar ve test verilerine karşı üretim verileri için ayrı hesaplar oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="f18a7-150">In a real-world application, you typically create separate accounts for application data versus logging data and separate accounts for test data versus production data.</span></span> <span data-ttu-id="f18a7-151">Bu öğreticide yalnızca tek bir hesap kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="f18a7-151">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="f18a7-152">Açık hello **Sunucu Gezgini** Visual Studio'daki.</span><span class="sxs-lookup"><span data-stu-id="f18a7-152">Open hello **Server Explorer** window in Visual Studio.</span></span>
2. <span data-ttu-id="f18a7-153">Sağ hello **Azure** düğümünü ve ardından **tooMicrosoft Azure aboneliğine Bağlan...** .</span><span class="sxs-lookup"><span data-stu-id="f18a7-153">Right-click hello **Azure** node, and then click **Connect tooMicrosoft Azure Subscription...**.</span></span>
   
   ![TooAzure Bağlan](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. <span data-ttu-id="f18a7-155">Azure kimlik bilgilerinizi kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f18a7-155">Sign in using your Azure credentials.</span></span>
4. <span data-ttu-id="f18a7-156">Sağ **depolama** altında Azure düğümü hello ve ardından **depolama hesabı oluştur**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-156">Right-click **Storage** under hello Azure node, and then click **Create Storage Account**.</span></span>
   
   ![Depolama hesabı oluşturma](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. <span data-ttu-id="f18a7-158">Merhaba, **depolama hesabı oluştur** iletişim kutusunda, hello depolama hesabı için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="f18a7-158">In hello **Create Storage Account** dialog, enter a name for hello storage account.</span></span>

    <span data-ttu-id="f18a7-159">Merhaba adı olmalı benzersiz olmalıdır (başka bir Azure depolama hesabı hello olabilir aynı adı).</span><span class="sxs-lookup"><span data-stu-id="f18a7-159">hello name must be must be unique (no other Azure storage account can have hello same name).</span></span> <span data-ttu-id="f18a7-160">Girdiğiniz hello adı zaten kullanımda olduğundan, bir fırsat toochange alırsınız.</span><span class="sxs-lookup"><span data-stu-id="f18a7-160">If hello name you enter is already in use, you'll get a chance toochange it.</span></span>

    <span data-ttu-id="f18a7-161">Depolama hesabınız olacak URL tooaccess hello *{ad}*. core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="f18a7-161">hello URL tooaccess your storage account will be *{name}*.core.windows.net.</span></span>
6. <span data-ttu-id="f18a7-162">Set hello **bölge veya benzeşim grubunda** aşağı açılan liste toohello bölgeye en yakın tooyou.</span><span class="sxs-lookup"><span data-stu-id="f18a7-162">Set hello **Region or Affinity Group** drop-down list toohello region closest tooyou.</span></span>

    <span data-ttu-id="f18a7-163">Bu ayar, hangi Azure veri merkezi depolama hesabınız barındıracak belirtir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-163">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="f18a7-164">Bu öğretici için tercih ettiğiniz bir dikkat çekici fark yapmaz.</span><span class="sxs-lookup"><span data-stu-id="f18a7-164">For this tutorial, your choice won't make a noticeable difference.</span></span> <span data-ttu-id="f18a7-165">Ancak, bir üretim web uygulaması için web sunucunuz, depolama hesabı toobe hello içinde istediğiniz aynı bölge toominimize gecikme süresi ve veri çıkış ücretleri.</span><span class="sxs-lookup"><span data-stu-id="f18a7-165">However, for a production web app, you want your web server and your storage account toobe in hello same region toominimize latency and data egress charges.</span></span> <span data-ttu-id="f18a7-166">(daha sonra oluşturacağınız) hello web uygulamasını sipariş toominimize gecikme hello web uygulamasına erişme olabildiğince toohello tarayıcılar kapatmak gibi veri merkezi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-166">hello web app (which you'll create later) datacenter should be as close as possible toohello browsers accessing hello web app in order toominimize latency.</span></span>
7. <span data-ttu-id="f18a7-167">Set hello **çoğaltma** aşağı açılan listesinde çok**yerel olarak yedekli**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-167">Set hello **Replication** drop-down list too**Locally redundant**.</span></span>

    <span data-ttu-id="f18a7-168">Bir depolama hesabı için coğrafi çoğaltma etkinleştirildiğinde, depolanan hello içerik çoğaltılmış tooa ikincil veri merkezine tooenable yük devretme toothat hello birincil konumda büyük bir felaket durumunda konumdur.</span><span class="sxs-lookup"><span data-stu-id="f18a7-168">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover toothat location in case of a major disaster in hello primary location.</span></span> <span data-ttu-id="f18a7-169">Coğrafi çoğaltma ek ücretlere neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-169">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="f18a7-170">Test ve geliştirme hesaplarında genellikle coğrafi çoğaltma için toopay istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="f18a7-170">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="f18a7-171">Daha fazla bilgi için bkz. [Depolama hesabı oluşturma, yönetme veya silme](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="f18a7-171">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
8. <span data-ttu-id="f18a7-172">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f18a7-172">Click **Create**.</span></span>

    ![Yeni depolama hesabı](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <span data-ttu-id="f18a7-174"><a id="download"></a>Merhaba uygulama indirin</span><span class="sxs-lookup"><span data-stu-id="f18a7-174"><a id="download"></a>Download hello application</span></span>
1. <span data-ttu-id="f18a7-175">İndirip hello sıkıştırmasını [tamamlanan çözümü](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span><span class="sxs-lookup"><span data-stu-id="f18a7-175">Download and unzip hello [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span></span>
2. <span data-ttu-id="f18a7-176">Visual Studio’yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f18a7-176">Start Visual Studio.</span></span>
3. <span data-ttu-id="f18a7-177">Merhaba gelen **dosya** menüsünü seçin **Aç > Proje/çözüm**hello çözümü indirdiğiniz toowhere gidin ve ardından hello çözüm dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="f18a7-177">From hello **File** menu choose **Open > Project/Solution**, navigate toowhere you downloaded hello solution, and then open hello solution file.</span></span>
4. <span data-ttu-id="f18a7-178">CTRL + SHIFT + B toobuild hello çözüm tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="f18a7-178">Press CTRL+SHIFT+B toobuild hello solution.</span></span>

    <span data-ttu-id="f18a7-179">Varsayılan olarak, Visual Studio hello dahil edilmeyen hello NuGet paket içeriği otomatik olarak yükler *.zip* dosyası.</span><span class="sxs-lookup"><span data-stu-id="f18a7-179">By default, Visual Studio automatically restores hello NuGet package content, which was not included in hello *.zip* file.</span></span> <span data-ttu-id="f18a7-180">Merhaba paketler geri yüklenmezse varsa bunları el ile giderek toohello tarafından yükleyin **çözüm için NuGet paketlerini Yönet** iletişim ve hello tıklayarak **geri** düğmesine sağ hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="f18a7-180">If hello packages don't restore, install them manually by going toohello **Manage NuGet Packages for Solution** dialog and clicking hello **Restore** button at hello top right.</span></span>
5. <span data-ttu-id="f18a7-181">İçinde **Çözüm Gezgini**, olduğundan emin olun **ContosoAdsWeb** hello başlangıç projesi olarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-181">In **Solution Explorer**, make sure that **ContosoAdsWeb** is selected as hello startup project.</span></span>

## <span data-ttu-id="f18a7-182"><a id="configurestorage"></a>Depolama hesabınızı Hello uygulama toouse yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f18a7-182"><a id="configurestorage"></a>Configure hello application toouse your storage account</span></span>
1. <span data-ttu-id="f18a7-183">Açık Merhaba uygulaması *Web.config* hello ContosoAdsWeb projesinde dosya.</span><span class="sxs-lookup"><span data-stu-id="f18a7-183">Open hello application *Web.config* file in hello ContosoAdsWeb project.</span></span>

    <span data-ttu-id="f18a7-184">Merhaba dosyası bir SQL bağlantı dizesi ve BLOB'lar ve kuyruklarla çalışmaya yönelik bir Azure depolama bağlantı dizesi içerir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-184">hello file contains a SQL connection string and an Azure storage connection string for working with blobs and queues.</span></span>

    <span data-ttu-id="f18a7-185">Merhaba SQL bağlantı dizesi işaret tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) veritabanı.</span><span class="sxs-lookup"><span data-stu-id="f18a7-185">hello SQL connection string points tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span></span>

    <span data-ttu-id="f18a7-186">Merhaba depolama bağlantı dizesi yer tutucuları Merhaba, depolama hesabı adı ve erişim anahtarı için olan bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-186">hello storage connection string is an example that has placeholders for hello storage account name and access key.</span></span> <span data-ttu-id="f18a7-187">Bu hello adını ve anahtarını depolama hesabınızın sahip bir bağlantı dizesi ile değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f18a7-187">You'll replace this with a connection string that has hello name and key of your storage account.</span></span>  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    <span data-ttu-id="f18a7-188">Merhaba depolama bağlantı dizesi, Web işleri SDK'sini kullanan hello adı hello olduğundan AzureWebJobsStorage varsayılan olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="f18a7-188">hello storage connection string is named AzureWebJobsStorage because that's hello name hello WebJobs SDK uses by default.</span></span> <span data-ttu-id="f18a7-189">Merhaba hello Azure ortamı tooset yalnızca bir bağlantı dizesi değerine sahip biçimde aynı adı buraya kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f18a7-189">hello same name is used here so you have tooset only one connection string value in hello Azure environment.</span></span>
2. <span data-ttu-id="f18a7-190">İçinde **Sunucu Gezgini**, depolama hesabınız hello altında sağ **depolama** düğümünü ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-190">In **Server Explorer**, right-click your storage account under hello **Storage** node, and then click **Properties**.</span></span>

    ![Depolama hesabı Özellikler'i tıklatın](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. <span data-ttu-id="f18a7-192">Merhaba, **özellikleri** penceresinde, tıklatın **depolama hesabı anahtarlarını**ve hello üç nokta'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f18a7-192">In hello **Properties** window, click **Storage Account Keys**, and then click hello ellipsis.</span></span>

    ![Depolama hesabı anahtarları](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. <span data-ttu-id="f18a7-194">Kopya hello **bağlantı dizesi**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-194">Copy hello **Connection String**.</span></span>

    ![Depolama hesabı anahtarları iletişim](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. <span data-ttu-id="f18a7-196">Merhaba Hello depolama bağlantı dizesini değiştirin *Web.config* dosyasını kopyaladığınız hello bağlantı dizesine sahip.</span><span class="sxs-lookup"><span data-stu-id="f18a7-196">Replace hello storage connection string in hello *Web.config* file with hello connection string you just copied.</span></span> <span data-ttu-id="f18a7-197">Her şeyi hello tırnak işaretleri içindeki ancak yapıştırmadan önce hello tırnak işaretleri dahil değil seçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="f18a7-197">Make sure you select everything inside hello quotation marks but not including hello quotation marks before pasting.</span></span>
6. <span data-ttu-id="f18a7-198">Açık hello *App.config* hello ContosoAdsWebJob proje dosyasında.</span><span class="sxs-lookup"><span data-stu-id="f18a7-198">Open hello *App.config* file in hello ContosoAdsWebJob project.</span></span>

    <span data-ttu-id="f18a7-199">Bu dosya iki depolama bağlantı dizeleri, bir uygulama verileri için ve günlüğe kaydetme için bir sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-199">This file has two storage connection strings, one for application data and one for logging.</span></span> <span data-ttu-id="f18a7-200">Uygulama verilerini ve günlüğe kaydetme için ayrı bir depolama hesaplarını kullanabilirsiniz ve kullanabileceğiniz [birden çok depolama hesapları için verileri](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="f18a7-200">You can use separate storage accounts for application data and logging, and you can use [multiple storage accounts for data](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span> <span data-ttu-id="f18a7-201">Bu öğreticide, tek bir depolama hesabına kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="f18a7-201">For this tutorial, you'll use a single storage account.</span></span> <span data-ttu-id="f18a7-202">Merhaba depolama hesabı anahtarlarını yer tutucular Hello bağlantı dizelerine sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="f18a7-202">hello connection strings have placeholders for hello storage account keys.</span></span>

    ```
    <configuration>
        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/>
    </connectionStrings>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    </configuration>

    ```

    <span data-ttu-id="f18a7-203">Varsayılan olarak, Web işleri SDK'si hello için bağlantı dizelerini AzureWebJobsStorage ve AzureWebJobsDashboard adlı arar.</span><span class="sxs-lookup"><span data-stu-id="f18a7-203">By default, hello WebJobs SDK looks for connection strings named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="f18a7-204">Alternatif olarak, şunları yapabilirsiniz [ancak istediğiniz ve açıkça toohello içinde geçirmek hello bağlantı dizesi depolamak `JobHost` nesne](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span><span class="sxs-lookup"><span data-stu-id="f18a7-204">As an alternative, you can [store hello connection string however you want and pass it in explicitly toohello `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span></span>
7. <span data-ttu-id="f18a7-205">Her iki storage bağlantı dizelerini daha önce kopyaladığınız hello bağlantı dizesi ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f18a7-205">Replace both storage connection strings with hello connection string you copied earlier.</span></span>
8. <span data-ttu-id="f18a7-206">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f18a7-206">Save your changes.</span></span>

## <span data-ttu-id="f18a7-207"><a id="run"></a>Merhaba uygulama yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="f18a7-207"><a id="run"></a>Run hello application locally</span></span>
1. <span data-ttu-id="f18a7-208">Merhaba uygulamasının toostart hello web ön uç CTRL + F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="f18a7-208">toostart hello web frontend of hello application, press CTRL+F5.</span></span>

    <span data-ttu-id="f18a7-209">Merhaba varsayılan tarayıcı toohello giriş sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="f18a7-209">hello default browser opens toohello home page.</span></span> <span data-ttu-id="f18a7-210">(Merhaba web projesi çalıştırır, yaptığınız çünkü hello başlangıç projesi.)</span><span class="sxs-lookup"><span data-stu-id="f18a7-210">(hello web project runs because you've made it hello startup project.)</span></span>

    ![Contoso Ads giriş sayfası](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. <span data-ttu-id="f18a7-212">toostart hello WebJob arka hello uygulamasının sağ hello ContosoAdsWebJob projesinde **Çözüm Gezgini**ve ardından **hata ayıklama** > **başlangıç yeni örneği** .</span><span class="sxs-lookup"><span data-stu-id="f18a7-212">toostart hello WebJob backend of hello application, right-click hello ContosoAdsWebJob project in **Solution Explorer**, and then click **Debug** > **Start new instance**.</span></span>

    <span data-ttu-id="f18a7-213">Bir konsol uygulama penceresi açar ve hello WebJobs SDK JobHost nesne toorun başlatıldı belirten günlük iletilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f18a7-213">A console application window opens and displays logging messages indicating hello WebJobs SDK JobHost object has started toorun.</span></span>

    ![Bu hello arka uç gösteren konsol uygulama penceresi çalışıyor](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. <span data-ttu-id="f18a7-215">Tarayıcınızda, tıklatın **bir Ad oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-215">In your browser, click  **Create an Ad**.</span></span>
4. <span data-ttu-id="f18a7-216">Bazı test verilerini girin, bir görüntü tooupload seçin ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-216">Enter some test data, select an image tooupload, and then click **Create**.</span></span>

    ![Sayfa oluşturma](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    <span data-ttu-id="f18a7-218">Merhaba uygulama toohello dizin sayfasına gider, ancak işleme henüz tamamlanmadığından hello yeni ad için bir küçük resim göstermez.</span><span class="sxs-lookup"><span data-stu-id="f18a7-218">hello app goes toohello Index page, but it doesn't show a thumbnail for hello new ad because that processing hasn't happened yet.</span></span>

    <span data-ttu-id="f18a7-219">Bu sırada, kısa bekleme bir kuyruk iletisi alındı ve işlenmiş olan bir günlük iletisi hello konsol uygulaması penceresinde gösterir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-219">Meanwhile, after a short wait a logging message in hello console application window shows that a queue message was received and has been processed.</span></span>

    ![Bir kuyruk iletisi işlendiğini gösteren konsol uygulama penceresi](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. <span data-ttu-id="f18a7-221">İletileri günlüğe kaydetme hello konsol uygulaması penceresinde hello gördükten sonra hello dizin sayfası toosee hello küçük yenileyin.</span><span class="sxs-lookup"><span data-stu-id="f18a7-221">After you see hello logging messages in hello console application window, refresh hello Index page toosee hello thumbnail.</span></span>

    ![Dizin sayfası](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. <span data-ttu-id="f18a7-223">Tıklatın **ayrıntıları** ad toosee hello tam boyutlu görüntü için.</span><span class="sxs-lookup"><span data-stu-id="f18a7-223">Click **Details** for your ad toosee hello full-size image.</span></span>

    ![Ayrıntılar sayfası](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

<span data-ttu-id="f18a7-225">Merhaba uygulama'yı yerel bilgisayarınızda çalışır durumda ve bilgisayarınızın, ancak üzerinde bulunan veritabanı Kuyruklarla Çalışma ve içinde BLOB'bir SQL Server kullanarak hello bulut.</span><span class="sxs-lookup"><span data-stu-id="f18a7-225">You've been running hello application on your local computer, and it's using a SQL Server database located on your computer, but it's working with queues and blobs in hello cloud.</span></span> <span data-ttu-id="f18a7-226">Bölümden hello bulut veritabanı yanı sıra bulut BLOB'ları ve kuyrukları kullanma hello uygulaması hello bulutta çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="f18a7-226">In hello following section you'll run hello application in hello cloud, using a cloud database as well as cloud blobs and queues.</span></span>  

## <span data-ttu-id="f18a7-227"><a id="runincloud"></a>Merhaba uygulaması hello bulutta çalışan</span><span class="sxs-lookup"><span data-stu-id="f18a7-227"><a id="runincloud"></a>Run hello application in hello cloud</span></span>
<span data-ttu-id="f18a7-228">Siz gerçekleştirirsiniz adımları toorun hello hello bulut uygulamasında aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="f18a7-228">You'll do hello following steps toorun hello application in hello cloud:</span></span>

* <span data-ttu-id="f18a7-229">TooWeb uygulamaları dağıtın.</span><span class="sxs-lookup"><span data-stu-id="f18a7-229">Deploy tooWeb Apps.</span></span> <span data-ttu-id="f18a7-230">Visual Studio otomatik olarak yeni bir web uygulaması App Service ve bir SQL veritabanı örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f18a7-230">Visual Studio automatically creates a new web app in App Service and a SQL Database instance.</span></span>
* <span data-ttu-id="f18a7-231">Merhaba web uygulama toouse Azure SQL veritabanı ve depolama hesabı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f18a7-231">Configure hello web app toouse your Azure SQL database and storage account.</span></span>

<span data-ttu-id="f18a7-232">Merhaba bulutta çalıştırılırken bazı ads oluşturduktan sonra hello Web işleri SDK'si Pano toosee hello İzleme özelliklerini toooffer sahip zengin görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f18a7-232">After you've created some ads while running in hello cloud, you'll view hello WebJobs SDK dashboard toosee hello rich monitoring features it has toooffer.</span></span>

### <a name="deploy-tooweb-apps"></a><span data-ttu-id="f18a7-233">TooWeb uygulamaları dağıtma</span><span class="sxs-lookup"><span data-stu-id="f18a7-233">Deploy tooWeb Apps</span></span>

1. <span data-ttu-id="f18a7-234">Merhaba tarayıcı ve hello konsol uygulaması penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="f18a7-234">Close hello browser and hello console application window.</span></span>
2. <span data-ttu-id="f18a7-235">Merhaba Hello adımları [tooAzure SQL veritabanı ile yayımlama](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) bölümü.</span><span class="sxs-lookup"><span data-stu-id="f18a7-235">Follow hello steps in hello [Publish tooAzure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) section.</span></span>
3. <span data-ttu-id="f18a7-236">Merhaba dağıtma adımları tamamladıktan sonra bu makaledeki hello kalan görevlere devam edin.</span><span class="sxs-lookup"><span data-stu-id="f18a7-236">After you complete hello steps for deploying, continue with hello remaining tasks in this article.</span></span>

### <a name="configure-hello-web-app-toouse-your-azure-sql-database-and-storage-account"></a><span data-ttu-id="f18a7-237">Azure SQL veritabanı ve depolama hesabınızı Hello web uygulama toouse yapılandırın</span><span class="sxs-lookup"><span data-stu-id="f18a7-237">Configure hello web app toouse your Azure SQL database and storage account</span></span>
<span data-ttu-id="f18a7-238">En iyi güvenlik uygulaması çok olan[bağlantı dizeleri gibi hassas bilgileri kaynak kodu depoları içinde depolanan dosyaları içinde Geçirilmemesi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="f18a7-238">It's a security best practice too[avoid putting sensitive information such as connection strings in files that are stored in source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span> <span data-ttu-id="f18a7-239">Azure, bir şekilde toodo sağlar: ASP.NET yapılandırma API'leri hello uygulama Azure'da çalıştırıldığında bu değerleri otomatik olarak seçmesini ve hello Azure ortamı bağlantı dizesini ve diğer ayar değerlerini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f18a7-239">Azure provides a way toodo that: you can set connection string and other setting values in hello Azure environment, and ASP.NET configuration APIs automatically pick up these values when hello app runs in Azure.</span></span> <span data-ttu-id="f18a7-240">Bu değerleri kullanarak Azure'da ayarlayabilirsiniz **Sunucu Gezgini**, Azure portalı, Windows PowerShell hello veya hello platformlar arası komut satırı arabirimi.</span><span class="sxs-lookup"><span data-stu-id="f18a7-240">You can set these values in Azure by using **Server Explorer**, hello Azure Portal, Windows PowerShell, or hello cross-platform command-line interface.</span></span> <span data-ttu-id="f18a7-241">Daha fazla bilgi için bkz: [nasıl uygulama dizeleri ve bağlantı dizeleri çalışma](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="f18a7-241">For more information, see [How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span>

<span data-ttu-id="f18a7-242">Bu bölümde, kullandığınız **Sunucu Gezgini** azure'da tooset bağlantı dizesi değerleri.</span><span class="sxs-lookup"><span data-stu-id="f18a7-242">In this section, you use **Server Explorer** tooset connection string values in Azure.</span></span>

1. <span data-ttu-id="f18a7-243">İçinde **Sunucu Gezgini**, web uygulamanızı altında sağ **Azure > uygulama hizmeti > {kaynak grubunuz}**ve ardından **görünüm ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-243">In **Server Explorer**, right-click your web app under **Azure > App Service > {your resource group}**, and then click **View Settings**.</span></span>

    <span data-ttu-id="f18a7-244">Merhaba **Azure Web uygulaması** penceresi açılır hello üzerinde **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="f18a7-244">hello **Azure Web App** window opens on hello **Configuration** tab.</span></span>
2. <span data-ttu-id="f18a7-245">Değişiklik hello adını hello DefaultConnection bağlantı dizesi toohello seçtiğiniz hello hello SQL veritabanı yapılandırdığınızda [tooAzure SQL veritabanı ile yayımlama](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) makalesi.</span><span class="sxs-lookup"><span data-stu-id="f18a7-245">Change hello name of hello DefaultConnection connection string toohello name you chose when you configured hello SQL database in hello [Publish tooAzure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) article.</span></span>

    <span data-ttu-id="f18a7-246">Zaten hello sağ bağlantı dizesi değerine sahip şekilde ilişkilendirilmiş bir veritabanı ile Merhaba web uygulaması oluşturduğunuzda azure, bu bağlantı dizesi otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f18a7-246">Azure automatically created this connection string when you created hello web app with an associated database, so it already has hello right connection string value.</span></span> <span data-ttu-id="f18a7-247">Yalnızca, kodunuzu aramakta hello adı toowhat değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f18a7-247">You're changing just hello name toowhat your code is looking for.</span></span>
3. <span data-ttu-id="f18a7-248">AzureWebJobsStorage ve AzureWebJobsDashboard adlı iki yeni bağlantı dizeleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f18a7-248">Add two new connection strings, named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="f18a7-249">Merhaba veritabanı türü çok ayarlamak**özel**ve aynı değeri hello için daha önce kullanılan kümesi hello bağlantı dizesi değeri toohello *Web.config* ve *App.config* dosyaları.</span><span class="sxs-lookup"><span data-stu-id="f18a7-249">Set hello database type too**Custom**, and set hello connection string value toohello same value that you used earlier for hello *Web.config* and *App.config* files.</span></span> <span data-ttu-id="f18a7-250">(Merhaba tüm bağlantı dizesi, yalnızca hello erişim anahtarı içerir ve hello tırnak işaretleri dahil etmeyin emin olun.)</span><span class="sxs-lookup"><span data-stu-id="f18a7-250">(Be sure you include hello entire connection string, not just hello access key, and don't include hello quotation marks.)</span></span>

    <span data-ttu-id="f18a7-251">Bu bağlantı dizeleri hello Web işleri SDK'si ve uygulama verileri için bir günlük kaydı için bir tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f18a7-251">These connection strings are used by hello WebJobs SDK, one for application data and one for logging.</span></span> <span data-ttu-id="f18a7-252">Daha önce anlatıldığı gibi uygulama verileri için hello hello web ön uç kodu tarafından da kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f18a7-252">As you saw earlier, hello one for application data is also used by hello web front-end code.</span></span>
4. <span data-ttu-id="f18a7-253">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f18a7-253">Click **Save**.</span></span>

    ![Azure Portalı'nda bağlantı dizeleri](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. <span data-ttu-id="f18a7-255">İçinde **Sunucu Gezgini**hello web uygulaması sağ tıklayın ve ardından **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-255">In **Server Explorer**, right-click hello web app, and then click **Stop**.</span></span>
6. <span data-ttu-id="f18a7-256">Merhaba web uygulaması durdurulduktan sonra hello web uygulaması tekrar sağ tıklayın ve ardından **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-256">After hello web app stops, right-click hello web app again, and then click **Start**.</span></span>

   <span data-ttu-id="f18a7-257">Merhaba WebJob yayımladığınızda, ancak bir yapılandırma değişikliği yaptığınızda durdurur otomatik olarak başlar.</span><span class="sxs-lookup"><span data-stu-id="f18a7-257">hello WebJob automatically starts when you publish, but it stops when you make a configuration change.</span></span> <span data-ttu-id="f18a7-258">toorestart, hello web uygulaması yeniden başlatabilir veya hello hello Web işi yeniden [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="f18a7-258">toorestart it, you can either restart hello web app or restart hello WebJob in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="f18a7-259">Bu genellikle önerilen toorestart hello web yapılandırma değişikliğinden sonra uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="f18a7-259">It's generally recommended toorestart hello web app after a configuration change.</span></span>
7. <span data-ttu-id="f18a7-260">Adres çubuğunu hello web uygulaması URL'si sahip hello tarayıcı penceresini yenileyin.</span><span class="sxs-lookup"><span data-stu-id="f18a7-260">Refresh hello browser window that has hello web app URL in its address bar.</span></span>

    <span data-ttu-id="f18a7-261">Merhaba giriş sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-261">hello home page appears.</span></span>
8. <span data-ttu-id="f18a7-262">Ne zaman yaptığınız gibi bir ad oluşturun, [hello uygulama yerel olarak çalıştırılan](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span><span class="sxs-lookup"><span data-stu-id="f18a7-262">Create an ad, as you did when you [ran hello application locally](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span></span>

   <span data-ttu-id="f18a7-263">küçük resim ilk olmadan Hello dizin sayfası gösterilir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-263">hello Index page shows without a thumbnail at first.</span></span>
9. <span data-ttu-id="f18a7-264">Birkaç saniye sonra Hello sayfayı yenileyin ve hello küçük resmi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-264">Refresh hello page after a few seconds and hello thumbnail appears.</span></span>

   <span data-ttu-id="f18a7-265">Hello küçük resim görünmüyorsa, toowait veya bunu dakika hello WebJob toorestart için olabilir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-265">If hello thumbnail doesn't appear, you might have toowait a minute or so for hello WebJob toorestart.</span></span> <span data-ttu-id="f18a7-266">Biraz varsa sonra hala hello sayfasında, hello WebJob yenilediğinizde hello küçük resim otomatik olarak başlatılmamış olabilir görmüyorum.</span><span class="sxs-lookup"><span data-stu-id="f18a7-266">If after a while, you still don't see hello thumbnail when you refresh hello page, hello WebJob might not have started automatically.</span></span> <span data-ttu-id="f18a7-267">Bu durumda, toohello Git **uygulama hizmetleri** dikey penceresinde hello [Azure portal](https://portal.azure.com/), web uygulamanızı bulun ve ardından **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-267">In that case, go toohello **App Services** blade in hello [Azure portal](https://portal.azure.com/), locate your web app, and then click **Start**.</span></span>

### <a name="view-hello-webjobs-sdk-dashboard"></a><span data-ttu-id="f18a7-268">Görünüm hello Web işleri SDK'si Panosu</span><span class="sxs-lookup"><span data-stu-id="f18a7-268">View hello WebJobs SDK dashboard</span></span>
1. <span data-ttu-id="f18a7-269">Merhaba, [Azure portal](https://portal.azure.com/)seçin hello **App Services dikey**web uygulamanızı bulun ve seçin **WebJobs**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-269">In hello [Azure portal](https://portal.azure.com/), select hello **App Services blade**, locate your web app, and select **WebJobs**.</span></span>
3. <span data-ttu-id="f18a7-270">Select hello **günlükleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="f18a7-270">Select hello **Logs** tab.</span></span>

    ![Günlükleri sekmesi](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    <span data-ttu-id="f18a7-272">Yeni bir tarayıcı sekmesi toohello WebJobs SDK panosu açılır.</span><span class="sxs-lookup"><span data-stu-id="f18a7-272">A new browser tab opens toohello WebJobs SDK dashboard.</span></span> <span data-ttu-id="f18a7-273">Başlangıç Panosu WebJob çalışıyor ve işlevlerin bir listesini, kodunuzda Web işleri SDK'si tetiklenen bu hello gösterir. Bu hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-273">hello dashboard shows that hello WebJob is running and shows a list of functions in your code that hello WebJobs SDK triggered.</span></span>
4. <span data-ttu-id="f18a7-274">Merhaba işlevleri toosee yürütülmesinin ayrıntılarını birini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f18a7-274">Click one of hello functions toosee details about its execution.</span></span>

    ![Web işleri SDK'si Panosu](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![Web işleri SDK'si Panosu](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    <span data-ttu-id="f18a7-277">Merhaba **yeniden yürütme işlevi** bu sayfadaki düğme hello Web işleri SDK'si yeniden framework toocall hello işlevi neden, ve onu bir fırsat toochange hello geçirilen verileri toohello işlevi ilk verir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-277">hello **Replay Function** button on this page causes hello WebJobs SDK framework toocall hello function again, and it gives you a chance toochange hello data passed toohello function first.</span></span>

> [!NOTE]
> <span data-ttu-id="f18a7-278">Bitirdiğinizde hello web uygulaması, depolama hesabı ve SQL veritabanı örneğinde silme test, göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="f18a7-278">When you're finished testing, consider deleting hello web app, storage account, and your SQL Database instance.</span></span> <span data-ttu-id="f18a7-279">Merhaba web uygulaması ücretsiz, ancak hello SQL depolama hesabı ve veritabanı örneği ücretler tahakkuk eder (barındırabilir, en az toohello küçük boyutu nedeniyle).</span><span class="sxs-lookup"><span data-stu-id="f18a7-279">hello web app is free, but hello SQL storage account and database instance accrue charges (albeit, minimal due toohello small size).</span></span> <span data-ttu-id="f18a7-280">Ayrıca, başlangıç web uygulaması çalıştıran değiştirmeden bırakırsanız, URL'nizi bulan herkes oluşturun ve reklamları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="f18a7-280">Also, if you leave hello web app running, anyone who finds your URL can create and view ads.</span></span> 
>
>

### <a name="delete-your-web-app"></a><span data-ttu-id="f18a7-281">Web uygulamanızı Sil</span><span class="sxs-lookup"><span data-stu-id="f18a7-281">Delete your web app</span></span>
<span data-ttu-id="f18a7-282">Merhaba Portalı'nda toohello Git **uygulama hizmetleri** dikey penceresinde, bulun ve web uygulamanızı seçin ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-282">In hello portal, go toohello **App Services** blade, locate and select your web app, and then click **Delete**.</span></span> <span data-ttu-id="f18a7-283">Yalnızca istiyorsanız tootemporarily önlemek başkalarının hello web uygulaması erişmesini tıklatın **durdurmak** yerine.</span><span class="sxs-lookup"><span data-stu-id="f18a7-283">If you just want tootemporarily prevent others from accessing hello web app, click **Stop** instead.</span></span> <span data-ttu-id="f18a7-284">Bu durumda ücretler hello SQL veritabanı ve depolama hesabı için tooaccrue devam eder.</span><span class="sxs-lookup"><span data-stu-id="f18a7-284">In that case, charges will continue tooaccrue for hello SQL Database and Storage account.</span></span>

### <a name="delete-your-storage-account"></a><span data-ttu-id="f18a7-285">Depolama hesabınızı silme</span><span class="sxs-lookup"><span data-stu-id="f18a7-285">Delete your storage account</span></span>
<span data-ttu-id="f18a7-286">toodelete depolama hesabınızın bkz [bir depolama hesabını silmek](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="f18a7-286">toodelete your storage account, see [Delete a storage account](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span></span> 

### <a name="delete-your-database"></a><span data-ttu-id="f18a7-287">Veritabanınızı Sil</span><span class="sxs-lookup"><span data-stu-id="f18a7-287">Delete your database</span></span>
<span data-ttu-id="f18a7-288">toodelete SQL veritabanı, hello bkz [Azure SQL Database REST API'sini](https://docs.microsoft.com/rest/api/sql/) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="f18a7-288">toodelete your SQL database, see hello [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) documentation.</span></span>

## <span data-ttu-id="f18a7-289"><a id="create"></a>Merhaba uygulamayı sıfırdan oluşturma</span><span class="sxs-lookup"><span data-stu-id="f18a7-289"><a id="create"></a>Create hello application from scratch</span></span>
<span data-ttu-id="f18a7-290">Bu bölümde siz gerçekleştirirsiniz hello görevler:</span><span class="sxs-lookup"><span data-stu-id="f18a7-290">In this section you'll do hello following tasks:</span></span>

* <span data-ttu-id="f18a7-291">Visual Studio çözümü ile bir web projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f18a7-291">Create a Visual Studio solution with a web project.</span></span>
* <span data-ttu-id="f18a7-292">Merhaba veriler için bir sınıf kitaplığı projesi eklemek hello ön uç ve arka uç arasında paylaşılan erişim katmanı.</span><span class="sxs-lookup"><span data-stu-id="f18a7-292">Add a class library project for hello data access layer that is shared between hello front end and back end.</span></span>
* <span data-ttu-id="f18a7-293">Bir konsol uygulama projesi hello arka uç için etkin Web işleri dağıtımı ile ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f18a7-293">Add a Console Application project for hello backend, with WebJobs deployment enabled.</span></span>
* <span data-ttu-id="f18a7-294">NuGet paketleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f18a7-294">Add NuGet packages.</span></span>
* <span data-ttu-id="f18a7-295">Proje başvurularını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f18a7-295">Set project references.</span></span>
* <span data-ttu-id="f18a7-296">Merhaba önceki bölümde hello öğreticinin çalıştığınız indirilen hello uygulamasından uygulama kodu ve yapılandırma dosyalarını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="f18a7-296">Copy application code and configuration files from hello downloaded application that you worked with in hello previous section of hello tutorial.</span></span>
* <span data-ttu-id="f18a7-297">Azure BLOB'ları ve kuyrukları ile çalışan ve Web işleri SDK'si hello hello kod hello bölümleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="f18a7-297">Review hello parts of hello code that work with Azure blobs and queues and hello WebJobs SDK.</span></span>

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a><span data-ttu-id="f18a7-298">Bir web projesi ve sınıf kitaplığı proje bir Visual Studio çözümü oluşturun</span><span class="sxs-lookup"><span data-stu-id="f18a7-298">Create a Visual Studio solution with a web project and class library project</span></span>
1. <span data-ttu-id="f18a7-299">Visual Studio'da, **dosya** > **yeni** > **proje**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-299">In Visual Studio, choose **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="f18a7-300">Merhaba, **yeni proje** iletişim kutusunda, seçin **Visual C#** > **Web** > **ASP.NET Web uygulaması (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-300">In hello **New Project** dialog, choose **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>
3. <span data-ttu-id="f18a7-301">Merhaba projeyi ContosoAdsWeb olarak adlandırın, hello çözüm ContosoAdsWebJobsSDK adı (hello koyma hello çözüm adı tıklarsanız hello aynı klasöre yüklenen çözüm) ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-301">Name hello project ContosoAdsWeb, name hello solution ContosoAdsWebJobsSDK (change hello solution name if you're putting it in hello same folder as hello downloaded solution), and then click **OK**.</span></span>

    ![Yeni Proje](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. <span data-ttu-id="f18a7-303">Merhaba, **yeni ASP.NET Web uygulaması** iletişim kutusunda, hello MVC şablonunu seçin ve Seç **kimlik doğrulamayı Değiştir**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-303">In hello **New ASP.NET Web Application** dialog, choose hello MVC template, and select **Change Authentication**.</span></span>

    ![Kimlik Doğrulamayı Değiştirme](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. <span data-ttu-id="f18a7-305">Merhaba, **kimlik doğrulamayı Değiştir** iletişim kutusunda, seçin **doğrulaması yok**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-305">In hello **Change Authentication** dialog, choose **No Authentication**, and then click **OK**.</span></span>

    ![Kimlik Doğrulaması Yok](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. <span data-ttu-id="f18a7-307">Merhaba, **yeni ASP.NET Web uygulaması** iletişim kutusunda, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-307">In hello **New ASP.NET Web Application** dialog, click **OK**.</span></span>

    <span data-ttu-id="f18a7-308">Visual Studio hello çözüm ve hello web projesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f18a7-308">Visual Studio creates hello solution and hello web project.</span></span>
7. <span data-ttu-id="f18a7-309">İçinde **Çözüm Gezgini**hello çözümü (Merhaba proje değil) sağ tıklatın ve seçin **Ekle** > **yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-309">In **Solution Explorer**, right-click hello solution (not hello project), and choose **Add** > **New Project**.</span></span>
8. <span data-ttu-id="f18a7-310">Merhaba, **Yeni Proje Ekle** iletişim kutusunda, seçin **Visual C#** > **Windows Klasik Masaüstü** > **sınıf kitaplığı (.NET Framework)** şablonu.</span><span class="sxs-lookup"><span data-stu-id="f18a7-310">In hello **Add New Project** dialog, choose **Visual C#** > **Windows Classic Desktop** > **Class Library (.NET Framework)** template.</span></span>  
9. <span data-ttu-id="f18a7-311">Ad hello proje *ContosoAdsCommon*ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-311">Name hello project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="f18a7-312">Bu proje, hem ön uç hello hello Entity Framework bağlamına ve hello veri modeli içerir ve arka uç kullanır.</span><span class="sxs-lookup"><span data-stu-id="f18a7-312">This project will contain hello Entity Framework context and hello data model which both hello front end and back end will use.</span></span> <span data-ttu-id="f18a7-313">Alternatif olarak, hello EF ile ilgili sınıflar hello web projesinde tanımlayın ve proje hello Web işi projesi başvuru.</span><span class="sxs-lookup"><span data-stu-id="f18a7-313">As an alternative, you could define hello EF-related classes in hello web project and reference that project from hello WebJob project.</span></span> <span data-ttu-id="f18a7-314">Ancak, Web işi projeniz gerekli olmayan bir başvuru tooweb derlemeleri sonra olurdu.</span><span class="sxs-lookup"><span data-stu-id="f18a7-314">But, then your WebJob project would have a reference tooweb assemblies, which it doesn't need.</span></span>

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a><span data-ttu-id="f18a7-315">Web işleri dağıtımı etkin olan bir konsol uygulama projesi ekleyin</span><span class="sxs-lookup"><span data-stu-id="f18a7-315">Add a Console Application project that has WebJobs deployment enabled</span></span>
1. <span data-ttu-id="f18a7-316">Merhaba web projesi (değil hello çözüm ya da hello sınıf kitaplığı Proje) sağ tıklayın ve ardından **Ekle** > **yeni Azure Web işi projesi**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-316">Right-click hello web project (not hello solution or hello class library project), and then click **Add** > **New Azure WebJob Project**.</span></span>

    ![Yeni Azure Web işi projesinin menü seçimi](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. <span data-ttu-id="f18a7-318">Merhaba, **Azure Web işine Ekle** iletişim kutusunda, her iki hello ContosoAdsWebJob girin **proje adı** ve hello **Web işi adı**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-318">In hello **Add Azure WebJob** dialog, enter ContosoAdsWebJob as both hello **Project name** and hello **WebJob name**.</span></span> <span data-ttu-id="f18a7-319">Bırakın **WebJob çalıştırma modu** çok ayarlamak**sürekli olarak çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-319">Leave **WebJob run mode** set too**Run Continuously**.</span></span>
3. <span data-ttu-id="f18a7-320">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f18a7-320">Click **OK**.</span></span>

   <span data-ttu-id="f18a7-321">Visual Studio hello web projesi dağıttığınız her bir Web işi yapılandırılmış toodeploy olan bir konsol uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f18a7-321">Visual Studio creates a Console application that is configured toodeploy as a WebJob whenever you deploy hello web project.</span></span> <span data-ttu-id="f18a7-322">başlangıç projesi oluşturduktan sonra görevleri aşağıdaki hello gerçekleştirilen, toodo:</span><span class="sxs-lookup"><span data-stu-id="f18a7-322">toodo that, it performed hello following tasks after creating hello project:</span></span>

   * <span data-ttu-id="f18a7-323">Eklenen bir *webjob yayımlama settings.json* hello Web işi projesi özellikleri klasördeki dosya.</span><span class="sxs-lookup"><span data-stu-id="f18a7-323">Added a *webjob-publish-settings.json* file in hello WebJob project Properties folder.</span></span>
   * <span data-ttu-id="f18a7-324">Eklenen bir *webjobs list.json* hello web projesi özellikleri klasörü dosyasında.</span><span class="sxs-lookup"><span data-stu-id="f18a7-324">Added a *webjobs-list.json* file in hello web project Properties folder.</span></span>
   * <span data-ttu-id="f18a7-325">Merhaba Microsoft.Web.WebJobs.Publish NuGet paketi hello WebJob projesinde yüklü.</span><span class="sxs-lookup"><span data-stu-id="f18a7-325">Installed hello Microsoft.Web.WebJobs.Publish NuGet package in hello WebJob project.</span></span>

   <span data-ttu-id="f18a7-326">Bu değişiklikler hakkında daha fazla bilgi için bkz: [nasıl Visual Studio'yu kullanarak Web işleri toodeploy](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="f18a7-326">For more information about these changes, see [How toodeploy WebJobs by using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span>

### <a name="add-nuget-packages"></a><span data-ttu-id="f18a7-327">NuGet paketleri ekleme</span><span class="sxs-lookup"><span data-stu-id="f18a7-327">Add NuGet packages</span></span>
<span data-ttu-id="f18a7-328">bir Web işi projesi için Hello yeni proje şablonu hello WebJobs SDK NuGet paketini otomatik olarak yükler [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) ve bağımlılıklarını.</span><span class="sxs-lookup"><span data-stu-id="f18a7-328">hello new-project template for a WebJob project automatically installs hello WebJobs SDK NuGet package [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) and its dependencies.</span></span>

<span data-ttu-id="f18a7-329">Merhaba Web işi projesinin otomatik olarak yüklenen Web işleri SDK'si bağımlılık hello birini Azure Storage istemci kitaplığı (SCL) hello.</span><span class="sxs-lookup"><span data-stu-id="f18a7-329">One of hello WebJobs SDK dependencies that is installed automatically in hello WebJob project is hello Azure Storage Client Library (SCL).</span></span> <span data-ttu-id="f18a7-330">Ancak, tooadd gerekir, BLOB'ları ve kuyrukları ile toohello web projesi toowork.</span><span class="sxs-lookup"><span data-stu-id="f18a7-330">However, you need tooadd it toohello web project toowork with blobs and queues.</span></span>

1. <span data-ttu-id="f18a7-331">Açık hello **NuGet paketlerini Yönet** hello çözüm için iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="f18a7-331">Open hello **Manage NuGet Packages** dialog for hello solution.</span></span>
2. <span data-ttu-id="f18a7-332">Merhaba sol bölmesinde seçin **yüklü paketleri**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-332">In hello left pane, select **Installed packages**.</span></span>
3. <span data-ttu-id="f18a7-333">Hello bulur *Azure Storage* paketini ve ardından **Yönet**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-333">Find hello *Azure Storage* package, and then click **Manage**.</span></span>
4. <span data-ttu-id="f18a7-334">Merhaba, **projeleri seçin** kutusu, select hello **ContosoAdsWeb** onay kutusunu işaretleyin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-334">In hello **Select Projects** box, select hello **ContosoAdsWeb** check box, and then click **OK**.</span></span>

    <span data-ttu-id="f18a7-335">Üç projenin hello Entity Framework toowork SQL veritabanındaki verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="f18a7-335">All three projects use hello Entity Framework toowork with data in SQL Database.</span></span>
5. <span data-ttu-id="f18a7-336">Merhaba sol bölmesinde seçin **çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-336">In hello left pane, select **Online**.</span></span>
6. <span data-ttu-id="f18a7-337">Hello bulur *EntityFramework* NuGet paketini bulun ve üç projenin tamamına yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f18a7-337">Find hello *EntityFramework* NuGet package, and install it in all three projects.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="f18a7-338">Proje başvurularını ayarlama</span><span class="sxs-lookup"><span data-stu-id="f18a7-338">Set project references</span></span>
<span data-ttu-id="f18a7-339">Bu nedenle hem de bir başvuru toohello ContosoAdsCommon projesine gerekir hem web hem de Web işi projeleri hello SQL veritabanı ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="f18a7-339">Both web and WebJob projects work with hello SQL database, so both need a reference toohello ContosoAdsCommon project.</span></span>

1. <span data-ttu-id="f18a7-340">Merhaba ContosoAdsWeb projesinde bir başvuru toohello ContosoAdsCommon projesine ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f18a7-340">In hello ContosoAdsWeb project, set a reference toohello ContosoAdsCommon project.</span></span> <span data-ttu-id="f18a7-341">(Merhaba ContosoAdsWeb projesine sağ tıklayın ve ardından **Ekle** > **başvuru**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-341">(Right-click hello ContosoAdsWeb project, and then click **Add** > **Reference**.</span></span> 
2. <span data-ttu-id="f18a7-342">Merhaba, **başvuru Yöneticisi** iletişim kutusunda **projeleri** > **çözüm** > **ContosoAdsCommon**ve ardından **Tamam**.)</span><span class="sxs-lookup"><span data-stu-id="f18a7-342">In hello **Reference Manager** dialog box, select **Projects** > **Solution** > **ContosoAdsCommon**, and then click **OK**.)</span></span>
   
    <span data-ttu-id="f18a7-343">Merhaba Web işi projesinin başvuruları görüntülerle çalışma ve bağlantı dizeleri erişmek için gerekir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-343">hello WebJob project needs references for working with images and for accessing connection strings.</span></span>

4. <span data-ttu-id="f18a7-344">Merhaba ContosoAdsWebJob projesinde çok bir başvuru ayarlayın`System.Drawing` ve `System.Configuration`.</span><span class="sxs-lookup"><span data-stu-id="f18a7-344">In hello ContosoAdsWebJob project, set a reference too`System.Drawing` and `System.Configuration`.</span></span>

### <a name="add-code-and-configuration-files"></a><span data-ttu-id="f18a7-345">Kod ve yapılandırma dosyaları Ekle</span><span class="sxs-lookup"><span data-stu-id="f18a7-345">Add code and configuration files</span></span>
<span data-ttu-id="f18a7-346">Bu öğretici nasıl çok göstermez[MVC denetleyicileri ve yapı iskelesi kullanarak görünümleri oluşturma](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), nasıl çok[SQL Server veritabanları ile çalışan Entity Framework kod yazma](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), veya [hello temelleri zaman uyumsuz ASP.NET 4.5 programlama](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="f18a7-346">This tutorial does not show how too[create MVC controllers and views using scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), how too[write Entity Framework code that works with SQL Server databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), or [hello basics of asynchronous programming in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span> <span data-ttu-id="f18a7-347">Bu nedenle, tüm bu kalır toodo hello yeni çözüm hello indirilen çözümden kod ve yapılandırma dosyaları Kopyala ' dir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-347">So, all that remains toodo is copy code and configuration files from hello downloaded solution into hello new solution.</span></span> <span data-ttu-id="f18a7-348">Bunu sonra hello aşağıdaki bölümlerde Göster ve anahtar hello kod bölümlerini açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="f18a7-348">After you do that, hello following sections show and explain key parts of hello code.</span></span>

<span data-ttu-id="f18a7-349">tooadd dosyalar tooa proje veya bir klasörü, sağ hello proje veya klasöre tıklatın **Ekle** > **varolan öğeyi**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-349">tooadd files tooa project or a folder, right-click hello project or folder and click **Add** > **Existing Item**.</span></span> <span data-ttu-id="f18a7-350">Select hello dosyalarını tıklayın ve istediğiniz **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-350">Select hello files you want and click **Add**.</span></span> <span data-ttu-id="f18a7-351">Tooreplace var olan dosyaları isteyip istemediğinizi sorulursa tıklatın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="f18a7-351">If asked whether you want tooreplace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="f18a7-352">Merhaba ContosoAdsCommon projesinde hello silme *Class1.cs* dosya ve kendi yer hello hello indirilen projeden aşağıdaki dosyaları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f18a7-352">In hello ContosoAdsCommon project, delete hello *Class1.cs* file and add in its place hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="f18a7-353">*Ad.cs*</span><span class="sxs-lookup"><span data-stu-id="f18a7-353">*Ad.cs*</span></span>
   * <span data-ttu-id="f18a7-354">*ContosoAdscontext.cs*</span><span class="sxs-lookup"><span data-stu-id="f18a7-354">*ContosoAdscontext.cs*</span></span>
   * <span data-ttu-id="f18a7-355">*BlobInformation.cs*</span><span class="sxs-lookup"><span data-stu-id="f18a7-355">*BlobInformation.cs*</span></span>
2. <span data-ttu-id="f18a7-356">Merhaba ContosoAdsWeb projesinde hello hello indirilen projeden aşağıdaki dosyaları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f18a7-356">In hello ContosoAdsWeb project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="f18a7-357">*Web.config*</span><span class="sxs-lookup"><span data-stu-id="f18a7-357">*Web.config*</span></span>
   * <span data-ttu-id="f18a7-358">*Global.asax.cs*</span><span class="sxs-lookup"><span data-stu-id="f18a7-358">*Global.asax.cs*</span></span>  
   * <span data-ttu-id="f18a7-359">Merhaba, *denetleyicileri* klasörü: *AdController.cs*</span><span class="sxs-lookup"><span data-stu-id="f18a7-359">In hello *Controllers* folder: *AdController.cs*</span></span>
   * <span data-ttu-id="f18a7-360">Merhaba, *görünümler/paylaşılan* klasörü: *_Layout.cshtml* dosyası</span><span class="sxs-lookup"><span data-stu-id="f18a7-360">In hello *Views\Shared* folder: *_Layout.cshtml* file</span></span>
   * <span data-ttu-id="f18a7-361">Merhaba, *görünümler* klasörü: *Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="f18a7-361">In hello *Views\Home* folder: *Index.cshtml*</span></span>
   * <span data-ttu-id="f18a7-362">Merhaba, *görünümler/reklam* klasörü (öncelikle hello klasörü oluşturun): beş *.cshtml* dosyaları</span><span class="sxs-lookup"><span data-stu-id="f18a7-362">In hello *Views\Ad* folder (create hello folder first): five *.cshtml* files</span></span>
3. <span data-ttu-id="f18a7-363">Merhaba ContosoAdsWebJob projesinde hello hello indirilen projeden aşağıdaki dosyaları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f18a7-363">In hello ContosoAdsWebJob project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="f18a7-364">*App.config* (Merhaba dosya türü filtresi çok değiştirme**tüm dosyaları**)</span><span class="sxs-lookup"><span data-stu-id="f18a7-364">*App.config* (change hello file type filter too**All Files**)</span></span>
   * <span data-ttu-id="f18a7-365">*Program.cs*</span><span class="sxs-lookup"><span data-stu-id="f18a7-365">*Program.cs*</span></span>
   * <span data-ttu-id="f18a7-366">*Functions.cs*</span><span class="sxs-lookup"><span data-stu-id="f18a7-366">*Functions.cs*</span></span>

<span data-ttu-id="f18a7-367">Artık derleme, çalıştırmak ve hello öğreticide daha önce belirtildiği gibi hello uygulama dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f18a7-367">You can now build, run, and deploy hello application as instructed earlier in hello tutorial.</span></span> <span data-ttu-id="f18a7-368">Ancak, bunu yapmadan önce hello hala için dağıtılan hello ilk web uygulamasında çalışan Web işi durdurun.</span><span class="sxs-lookup"><span data-stu-id="f18a7-368">Before you do that, however, stop hello WebJob that is still running in hello first web app you deployed to.</span></span> <span data-ttu-id="f18a7-369">Aksi takdirde, bu Web işi yerel olarak oluşturulan sıra iletileri veya tüm kullanıyorsanız bu yana yeni bir web uygulamasında çalışan hello uygulama tarafından aynı hello depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="f18a7-369">Otherwise, that WebJob will process queue messages created locally or by hello app running in a new web app, since all are using hello same storage account.</span></span>

## <span data-ttu-id="f18a7-370"><a id="code"></a>Merhaba uygulama kodu gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="f18a7-370"><a id="code"></a>Review hello application code</span></span>
<span data-ttu-id="f18a7-371">Merhaba aşağıdaki bölümlerde açıklanmıştır hello kod tooworking hello WebJobs SDK ile ve Azure Storage BLOB'lar ve kuyruklarla ilgili.</span><span class="sxs-lookup"><span data-stu-id="f18a7-371">hello following sections explain hello code related tooworking with hello WebJobs SDK and Azure Storage blobs and queues.</span></span>

> [!NOTE]
> <span data-ttu-id="f18a7-372">Merhaba kodu belirli toohello için Web işleri SDK'si, toohello Git [Program.cs ve Functions.cs](#programcs) bölümler.</span><span class="sxs-lookup"><span data-stu-id="f18a7-372">For hello code specific toohello WebJobs SDK, go toohello [Program.cs and Functions.cs](#programcs) sections.</span></span>
>
>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="f18a7-373">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="f18a7-373">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="f18a7-374">Merhaba Ad.cs dosyası reklam kategorileri için bir numaralandırma ve reklam bilgileri için bir POCO varlık sınıfı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f18a7-374">hello Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="f18a7-375">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="f18a7-375">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="f18a7-376">Merhaba ContosoAdsContext sınıfı hello reklam sınıfının Entity Framework bir SQL veritabanında depolayan bir DbSet koleksiyonunda kullanıldığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-376">hello ContosoAdsContext class specifies that hello Ad class is used in a DbSet collection, which Entity Framework stores in a SQL database.</span></span>

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

<span data-ttu-id="f18a7-377">Merhaba sınıfın iki Oluşturucusu vardır.</span><span class="sxs-lookup"><span data-stu-id="f18a7-377">hello class has two constructors.</span></span> <span data-ttu-id="f18a7-378">Merhaba ilk hello web projesi tarafından kullanılan ve hello hello Web.config dosyasını veya hello Azure çalışma zamanı ortamı saklanan bir bağlantı dizesinin adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-378">hello first is used by hello web project, and specifies hello name of a connection string that is stored in hello Web.config file or hello Azure runtime environment.</span></span> <span data-ttu-id="f18a7-379">Merhaba ikinci oluşturucu hello gerçek bağlantı dizesine toopass sağlar.</span><span class="sxs-lookup"><span data-stu-id="f18a7-379">hello second constructor enables you toopass in hello actual connection string.</span></span> <span data-ttu-id="f18a7-380">Bir Web.config dosyası olmadığından, hello Web işi projesi tarafından gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-380">That is needed by hello WebJob project since it doesn't have a Web.config file.</span></span> <span data-ttu-id="f18a7-381">Daha önce gördüğünüzle burada Bu bağlantı dizesi depolanır ve daha sonra nasıl hello DbContext sınıfını başlattığında hello kodu hello bağlantı dizesini alır görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f18a7-381">You saw earlier where this connection string was stored, and you'll see later how hello code retrieves hello connection string when it instantiates hello DbContext class.</span></span>

### <a name="contosoadscommon---blobinformationcs"></a><span data-ttu-id="f18a7-382">ContosoAdsCommon - BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="f18a7-382">ContosoAdsCommon - BlobInformation.cs</span></span>
<span data-ttu-id="f18a7-383">Merhaba `BlobInformation` bir görüntü blob'u bir kuyruk iletisi içinde kullanılan toostore bilgilerini bir sınıftır.</span><span class="sxs-lookup"><span data-stu-id="f18a7-383">hello `BlobInformation` class is used toostore information about an image blob in a queue message.</span></span>

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="f18a7-384">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="f18a7-384">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="f18a7-385">Hello adlı kod `Application_Start` yöntemi oluşturur bir *görüntüleri* blob kapsayıcısı ve bir *görüntüleri* henüz yoksa sıra.</span><span class="sxs-lookup"><span data-stu-id="f18a7-385">Code that is called from hello `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="f18a7-386">Bu, yeni bir depolama hesabı kullanarak başlattığınızda hello blob kapsayıcısının ve kuyruğun otomatik olarak oluşturulan gerekli sağlar.</span><span class="sxs-lookup"><span data-stu-id="f18a7-386">This ensures that whenever you start using a new storage account, hello required blob container and queue are created automatically.</span></span>

<span data-ttu-id="f18a7-387">Merhaba kod alır erişim toohello depolama hesabı hello hello depolama bağlantı dizesini kullanarak *Web.config* dosya ya da Azure çalışma zamanı ortamı.</span><span class="sxs-lookup"><span data-stu-id="f18a7-387">hello code gets access toohello storage account by using hello storage connection string from hello *Web.config* file or Azure runtime environment.</span></span>

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

<span data-ttu-id="f18a7-388">Ardından, bir başvuru toohello alır *görüntüleri* blob kapsayıcısı, önceden var olmayan ve erişim izinlerini hello yeni kapsayıcı ayarlar hello kapsayıcı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f18a7-388">Then, it gets a reference toohello *images* blob container, creates hello container if it doesn't already exist, and sets access permissions on hello new container.</span></span> <span data-ttu-id="f18a7-389">Varsayılan olarak, yeni kapsayıcılar yalnızca depolama hesabı kimlik bilgileri tooaccess BLOB'ları olan istemcilerin izin verin.</span><span class="sxs-lookup"><span data-stu-id="f18a7-389">By default, new containers allow only clients with storage account credentials tooaccess blobs.</span></span> <span data-ttu-id="f18a7-390">Bu nokta toohello görüntü BLOB'larını URL'leri kullanarak görüntüleri gösterebilmek hello web uygulaması BLOB'lar toobe ortak hello.</span><span class="sxs-lookup"><span data-stu-id="f18a7-390">hello web app needs hello blobs toobe public so that it can display images using URLs that point toohello image blobs.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

<span data-ttu-id="f18a7-391">Benzer bir kod alır başvuru toohello *thumbnailrequest* sıraya almak ve yeni bir sıra oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f18a7-391">Similar code gets a reference toohello *thumbnailrequest* queue and creates a new queue.</span></span> <span data-ttu-id="f18a7-392">Bu durumda hiçbir izin değişikliği gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-392">In this case no permissions change is needed.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="f18a7-393">ContosoAdsWeb - _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="f18a7-393">ContosoAdsWeb - _Layout.cshtml</span></span>
<span data-ttu-id="f18a7-394">Merhaba *_Layout.cshtml* dosya hello üstbilgi ve altbilgi hello uygulama adını ayarlar ve bir "Reklamlar" menü girişi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f18a7-394">hello *_Layout.cshtml* file sets hello app name in hello header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="f18a7-395">ContosoAdsWeb - Görünümler\Giriş\Dizin.cshtml</span><span class="sxs-lookup"><span data-stu-id="f18a7-395">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="f18a7-396">Merhaba *Views\Home\Index.cshtml* dosya hello giriş sayfasında kategori bağlantılarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-396">hello *Views\Home\Index.cshtml* file displays category links on hello home page.</span></span> <span data-ttu-id="f18a7-397">Merhaba bağlantılar geçirmek hello hello tamsayı değeri `Category` enum bir sorgu dizesi değişkeni toohello reklam dizini sayfasına içindeki.</span><span class="sxs-lookup"><span data-stu-id="f18a7-397">hello links pass hello integer value of hello `Category` enum in a querystring variable toohello Ads Index page.</span></span>

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="f18a7-398">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="f18a7-398">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="f18a7-399">Merhaba, *AdController.cs* dosya, hello Oluşturucusu çağrıları hello `InitializeStorage` BLOB'lar ve kuyruklarla çalışmaya yönelik bir API sağlayan yöntemi toocreate Azure Storage istemci Kitaplığı nesneleri.</span><span class="sxs-lookup"><span data-stu-id="f18a7-399">In hello *AdController.cs* file, hello constructor calls hello `InitializeStorage` method toocreate Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="f18a7-400">Ardından, bir başvuru toohello hello kodu alır *görüntüleri* daha önce gördüğünüz gibi blob kapsayıcısı *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="f18a7-400">Then, hello code gets a reference toohello *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="f18a7-401">Yaparken, varsayılan ayarlar [yeniden deneme ilkesi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) bir web uygulaması için uygun.</span><span class="sxs-lookup"><span data-stu-id="f18a7-401">While doing that, it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="f18a7-402">Merhaba varsayılan üstel geri alma yeniden deneme ilkesi hello web uygulaması için geçici bir hata için tekrarlanan yeniden denemelerde bir dakikadan uzun süre askıya alabilir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-402">hello default exponential backoff retry policy could hang hello web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="f18a7-403">Burada belirtilen hello yeniden deneme ilkesi üç her denemeden sonra toothree çalıştığında saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="f18a7-403">hello retry policy specified here waits three seconds after each try for up toothree tries.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

<span data-ttu-id="f18a7-404">Benzer bir kod alır başvuru toohello *görüntüleri* sırası.</span><span class="sxs-lookup"><span data-stu-id="f18a7-404">Similar code gets a reference toohello *images* queue.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

<span data-ttu-id="f18a7-405">Merhaba denetleyici kodlarının birçoğu bir DbContext sınıfı kullanarak bir Entity Framework veri modeli ile çalışmak için tipiktir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-405">Most of hello controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="f18a7-406">Merhaba HttpPost bir istisnadır `Create` yöntemi, bir dosya yükler ve blob depolama alanına kaydeder.</span><span class="sxs-lookup"><span data-stu-id="f18a7-406">An exception is hello HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="f18a7-407">Merhaba model bağlayıcı sağlar bir [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) nesne toohello yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f18a7-407">hello model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object toohello method.</span></span>

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

<span data-ttu-id="f18a7-408">Merhaba kullanıcı dosya tooupload seçtiyseniz, hello kod hello dosyayı yükler, bir blob'a kaydeder ve hello Ad veritabanı kaydını toohello blob'u işaret eden bir URL ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-408">If hello user selected a file tooupload, hello code uploads hello file, saves it in a blob, and updates hello Ad database record with a URL that points toohello blob.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

<span data-ttu-id="f18a7-409">Merhaba, karşıya yükleme hello hello koddur `UploadAndSaveBlobAsync` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f18a7-409">hello code that does hello upload is in hello `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="f18a7-410">Merhaba blob, yüklemeleri ve kaydeder hello dosyası için bir GUID adı oluşturur ve bir başvuru toohello kaydedilmiş blob döndürür.</span><span class="sxs-lookup"><span data-stu-id="f18a7-410">It creates a GUID name for hello blob, uploads and saves hello file, and returns a reference toohello saved blob.</span></span>

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

<span data-ttu-id="f18a7-411">Merhaba HttpPost sonra `Create` yöntemi bir blob'u karşıya yüklemeleri ve güncelleştirmeleri Merhaba veritabanı, bir görüntü için dönüştürme tooa küçük resim hazır olduğunu bir sıraya ileti tooinform hello arka uç işlemi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f18a7-411">After hello HttpPost `Create` method uploads a blob and updates hello database, it creates a queue message tooinform hello back-end process that an image is ready for conversion tooa thumbnail.</span></span>

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

<span data-ttu-id="f18a7-412">Merhaba hello HttpPost kodunu `Edit` yöntemi olduğunu benzer, hello kullanıcı yeni bir görüntü dosyası seçerse, bu ad zaten mevcut BLOB silinmelidir dışında.</span><span class="sxs-lookup"><span data-stu-id="f18a7-412">hello code for hello HttpPost `Edit` method is similar, except that if hello user selects a new image file, any blobs that already exist for this ad must be deleted.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

<span data-ttu-id="f18a7-413">Bir ad sildiğinizde, BLOB'ları siler hello kod aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="f18a7-413">Here is hello code that deletes blobs when you delete an ad:</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="f18a7-414">ContosoAdsWeb - Views\Ad\Index.cshtml ve Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="f18a7-414">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="f18a7-415">Merhaba *Index.cshtml* dosyası küçük resimleri hello ile diğer ad verileri görüntüler:</span><span class="sxs-lookup"><span data-stu-id="f18a7-415">hello *Index.cshtml* file displays thumbnails with hello other ad data:</span></span>

        <img  src="@Html.Raw(item.ThumbnailURL)" />

<span data-ttu-id="f18a7-416">Merhaba *Details.cshtml* dosyası hello tam boyutlu görüntüyü gösterir:</span><span class="sxs-lookup"><span data-stu-id="f18a7-416">hello *Details.cshtml* file displays hello full-size image:</span></span>

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="f18a7-417">ContosoAdsWeb - Views\Ad\Create.cshtml ve Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="f18a7-417">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="f18a7-418">Merhaba *Create.cshtml* ve *Edit.cshtml* dosyaları belirtin etkinleştirir denetleyicisi tooget hello hello kodlama form `HttpPostedFileBase` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="f18a7-418">hello *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables hello controller tooget hello `HttpPostedFileBase` object.</span></span>

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

<span data-ttu-id="f18a7-419">Bir `<input>` öğesi, bir dosya seçme iletişim kutusu hello tarayıcı tooprovide söyler.</span><span class="sxs-lookup"><span data-stu-id="f18a7-419">An `<input>` element tells hello browser tooprovide a file selection dialog.</span></span>

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <span data-ttu-id="f18a7-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span><span class="sxs-lookup"><span data-stu-id="f18a7-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span></span>
<span data-ttu-id="f18a7-421">Ne zaman hello Web işi başladığında hello `Main` yöntem çağrılarını hello WebJobs SDK `JobHost.RunAndBlock` yöntemi toobegin yürütme hello geçerli iş parçacığında tetiklenen işlevlerin.</span><span class="sxs-lookup"><span data-stu-id="f18a7-421">When hello WebJob starts, hello `Main` method calls hello WebJobs SDK `JobHost.RunAndBlock` method toobegin execution of triggered functions on hello current thread.</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <span data-ttu-id="f18a7-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail yöntemi</span><span class="sxs-lookup"><span data-stu-id="f18a7-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail method</span></span>
<span data-ttu-id="f18a7-423">bir kuyruk iletisi alındığında hello Web işleri SDK'si bu yöntemi çağırır.</span><span class="sxs-lookup"><span data-stu-id="f18a7-423">hello WebJobs SDK calls this method when a queue message is received.</span></span> <span data-ttu-id="f18a7-424">Merhaba yöntemi, bir küçük resim oluşturur ve yerleştirmelerin hello küçük resim hello veritabanındaki URL.</span><span class="sxs-lookup"><span data-stu-id="f18a7-424">hello method creates a thumbnail and puts hello thumbnail URL in hello database.</span></span>

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within hello function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* <span data-ttu-id="f18a7-425">Merhaba `QueueTrigger` özniteliği hello thumbnailrequest sırada yeni bir ileti alındığında bu hello WebJobs SDK toocall bu yöntem yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-425">hello `QueueTrigger` attribute directs hello WebJobs SDK toocall this method when a new message is received on hello thumbnailrequest queue.</span></span>

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    <span data-ttu-id="f18a7-426">Merhaba `BlobInformation` hello kuyruk iletisi nesnedir hello otomatik olarak Serisi kaldırılan `blobInfo` parametresi.</span><span class="sxs-lookup"><span data-stu-id="f18a7-426">hello `BlobInformation` object in hello queue message is automatically deserialized into hello `blobInfo` parameter.</span></span> <span data-ttu-id="f18a7-427">Merhaba kuyruk iletisi Hello yöntemi tamamlandığında silinir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-427">When hello method completes, hello queue message is deleted.</span></span> <span data-ttu-id="f18a7-428">Merhaba yöntemi tamamlanmadan önce başarısız olursa, hello kuyruk iletisi silinmez; 10 dakikalık kiralama süresi dolduktan sonra hello yeniden toplanmış ve işlenen yayımlanan toobe iletisidir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-428">If hello method fails before completing, hello queue message is not deleted; after a 10-minute lease expires, hello message is released toobe picked up again and processed.</span></span> <span data-ttu-id="f18a7-429">Bir ileti her zaman bir özel durum neden olursa bu sırası süresiz olarak yinelenen olmaz.</span><span class="sxs-lookup"><span data-stu-id="f18a7-429">This sequence won't be repeated indefinitely if a message always causes an exception.</span></span> <span data-ttu-id="f18a7-430">5 başarısız tooprocess bir ileti denemesinden sonra hello adlı taşınan tooa sıra {queuename} iletisidir-zararlı.</span><span class="sxs-lookup"><span data-stu-id="f18a7-430">After 5 unsuccessful attempts tooprocess a message, hello message is moved tooa queue named {queuename}-poison.</span></span> <span data-ttu-id="f18a7-431">Merhaba en fazla deneme sayısı yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-431">hello maximum number of attempts is configurable.</span></span>
* <span data-ttu-id="f18a7-432">iki hello `Blob` öznitelikler ilişkili tooblobs olan nesneler sağlar: bir toohello mevcut görüntü blob'u ve hello yöntemi oluşturan bir tooa yeni küçük resim blob.</span><span class="sxs-lookup"><span data-stu-id="f18a7-432">hello two `Blob` attributes provide objects that are bound tooblobs: one toohello existing image blob and one tooa new thumbnail blob that hello method creates.</span></span>

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    <span data-ttu-id="f18a7-433">BLOB adları gelen hello özelliklerinden `BlobInformation` nesne hello kuyruk iletisi aldı (`BlobName` ve `BlobNameWithoutExtension`).</span><span class="sxs-lookup"><span data-stu-id="f18a7-433">Blob names come from properties of hello `BlobInformation` object received in hello queue message (`BlobName` and `BlobNameWithoutExtension`).</span></span> <span data-ttu-id="f18a7-434">tooget hello tam işlevselliğini hello depolama istemci kitaplığı, kullanabileceğiniz hello `CloudBlockBlob` sınıfı toowork BLOB'lar ile.</span><span class="sxs-lookup"><span data-stu-id="f18a7-434">tooget hello full functionality of hello Storage Client Library, you can use hello `CloudBlockBlob` class toowork with blobs.</span></span> <span data-ttu-id="f18a7-435">Toowork ile yazılmış tooreuse kodun isteyip istemediğinizi `Stream` nesneleri hello kullanabileceğiniz `Stream` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="f18a7-435">If you want tooreuse code that was written toowork with `Stream` objects, you can use hello `Stream` class.</span></span>

<span data-ttu-id="f18a7-436">Nasıl toowrite, işlevleri hakkında daha fazla bilgi için Web işleri SDK'si öznitelikleri kullanmak, kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="f18a7-436">For more information about how toowrite functions that use  WebJobs SDK attributes, see hello following resources:</span></span>

* [<span data-ttu-id="f18a7-437">Nasıl toouse Azure kuyruk depolama hello WebJobs SDK ile</span><span class="sxs-lookup"><span data-stu-id="f18a7-437">How toouse Azure queue storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [<span data-ttu-id="f18a7-438">Nasıl toouse Azure blob depolama hello WebJobs SDK ile</span><span class="sxs-lookup"><span data-stu-id="f18a7-438">How toouse Azure blob storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [<span data-ttu-id="f18a7-439">Nasıl toouse Azure tablo depolama hello WebJobs SDK ile</span><span class="sxs-lookup"><span data-stu-id="f18a7-439">How toouse Azure table storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [<span data-ttu-id="f18a7-440">Web işleri SDK'si toouse Azure Service Bus ile nasıl hello</span><span class="sxs-lookup"><span data-stu-id="f18a7-440">How toouse Azure Service Bus with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * <span data-ttu-id="f18a7-441">Web uygulamanız birden çok sanal makine çalışıyorsa, birden çok Web işleri eşzamanlı çalışan ve bazı senaryolarda bu hello aynı birden çok kez işlenen veri neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-441">If your web app runs on multiple VMs, multiple WebJobs will be running simultaneously, and in some scenarios this can result in hello same data getting processed multiple times.</span></span> <span data-ttu-id="f18a7-442">Merhaba yerleşik sırası, blob ve Service Bus Tetikleyicileri kullanırsanız, bir sorun değildir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-442">This is not a problem if you use hello built-in queue, blob, and Service Bus triggers.</span></span> <span data-ttu-id="f18a7-443">Merhaba SDK işlevlerinizi yalnızca bir kez her ileti veya blob işleneceğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="f18a7-443">hello SDK ensures that your functions will be processed only once for each message or blob.</span></span>
> * <span data-ttu-id="f18a7-444">Hakkında bilgi için tooimplement normal şekilde kapatılmasını bkz [kapama](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span><span class="sxs-lookup"><span data-stu-id="f18a7-444">For information about how tooimplement graceful shutdown, see [Graceful Shutdown](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span></span>
> * <span data-ttu-id="f18a7-445">Merhaba hello kodda `ConvertImageToThumbnailJPG` yöntemi (gösterilmez) hello sınıfları kullanır `System.Drawing` kolaylık olması için ad alanı.</span><span class="sxs-lookup"><span data-stu-id="f18a7-445">hello code in hello `ConvertImageToThumbnailJPG` method (not shown) uses classes in hello `System.Drawing` namespace for simplicity.</span></span> <span data-ttu-id="f18a7-446">Ancak, bu ad alanındaki hello sınıflar Windows Forms ile kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f18a7-446">However, hello classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="f18a7-447">Bir Windows veya ASP.NET hizmetinde kullanılması desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="f18a7-447">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="f18a7-448">Görüntü işleme seçenekleri hakkında daha fazla bilgi için bkz. [Dinamik Görüntü Oluşturma](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) ve [Görüntü Yeniden Boyutlandırmaya Ayrıntılı Bakış](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span><span class="sxs-lookup"><span data-stu-id="f18a7-448">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="f18a7-449">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f18a7-449">Next steps</span></span>
<span data-ttu-id="f18a7-450">Bu öğreticide, arka uç işleme için hello WebJobs SDK kullanan basit bir çok katmanlı uygulama gördünüz.</span><span class="sxs-lookup"><span data-stu-id="f18a7-450">In this tutorial, you've seen a simple multi-tier application that uses hello WebJobs SDK for backend processing.</span></span> <span data-ttu-id="f18a7-451">Bu bölümde, ASP.NET çok katmanlı uygulamaları ve Web işleri hakkında daha fazla bilgi edinmek için bazı öneriler sunar.</span><span class="sxs-lookup"><span data-stu-id="f18a7-451">This section offers some suggestions for learning more about ASP.NET multi-tier applications and WebJobs.</span></span>

### <a name="missing-features"></a><span data-ttu-id="f18a7-452">Eksik Özellikler</span><span class="sxs-lookup"><span data-stu-id="f18a7-452">Missing features</span></span>
<span data-ttu-id="f18a7-453">Merhaba uygulaması bir başlangıç öğreticisi için basit tutulmuştur.</span><span class="sxs-lookup"><span data-stu-id="f18a7-453">hello application has been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="f18a7-454">Gerçek dünya uygulamada uygulamak [bağımlılık ekleme](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) ve hello [depo ve iş birimi düzenleri](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), kullanın [günlüğe kaydetme için bir arabirimi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), kullanın[ EF Code First geçişleri](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage veri modeli değişikliklerini ve kullanmak [EF bağlantı dayanıklılığı](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage geçici ağ hataları.</span><span class="sxs-lookup"><span data-stu-id="f18a7-454">In a real-world application you would implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) and hello [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model changes, and use [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transient network errors.</span></span>

### <a name="scaling-webjobs"></a><span data-ttu-id="f18a7-455">Web işleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="f18a7-455">Scaling WebJobs</span></span>
<span data-ttu-id="f18a7-456">Web işleri hello bir web uygulaması bağlamında çalışır ve ayrı olarak ölçeklenebilir değildir.</span><span class="sxs-lookup"><span data-stu-id="f18a7-456">WebJobs run in hello context of a web app and are not scalable separately.</span></span> <span data-ttu-id="f18a7-457">Örneğin, bir standart web app örneği varsa, çalışan, arka plan işlemi yalnızca bir örneğine sahip ve bazı kullanılabilir tooserve web içeriği Aksi durumda olacak hello sunucu kaynaklarının (CPU, bellek, vb.) kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="f18a7-457">For example, if you have one Standard web app instance, you have only one instance of your background process running, and it is using some of hello server resources (CPU, memory, etc.) that otherwise would be available tooserve web content.</span></span>

<span data-ttu-id="f18a7-458">Trafik gün veya haftanın günü zamanına göre değişir ve hello arka uç, işleme gerekiyorsa toodo bekleyebilir, Web işleri toorun trafiği düşük zamanlarda zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f18a7-458">If traffic varies by time of day or day of week, and if hello backend processing you need toodo can wait, you could schedule your WebJobs toorun at low-traffic times.</span></span> <span data-ttu-id="f18a7-459">Hello yük hala Bu çözüm için çok yüksekse, hello arka uç adanmış bir ayrı bir web uygulamasında Web işi olarak bu amaçla çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f18a7-459">If hello load is still too high for that solution, you can run hello backend as a WebJob in a separate web app dedicated for that purpose.</span></span> <span data-ttu-id="f18a7-460">Arka uç web uygulamanızı sonra bağımsız olarak ve ön uç web uygulamanızdan ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f18a7-460">You can then scale your backend web app independently from your frontend web app.</span></span>

<span data-ttu-id="f18a7-461">Daha fazla bilgi için bkz: [ölçeklendirme WebJobs](websites-webjobs-resources.md#scale).</span><span class="sxs-lookup"><span data-stu-id="f18a7-461">For more information, see [Scaling WebJobs](websites-webjobs-resources.md#scale).</span></span>

### <a name="avoiding-web-app-timeout-shut-downs"></a><span data-ttu-id="f18a7-462">Web uygulaması zaman aşımı kapatma listeleri önleme</span><span class="sxs-lookup"><span data-stu-id="f18a7-462">Avoiding web app timeout shut-downs</span></span>
<span data-ttu-id="f18a7-463">toomake emin Webjob'larınızı her zaman çalışıyor ve web uygulamasının tüm örneklerini çalıştıran, tooenable hello sahip [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) özelliği.</span><span class="sxs-lookup"><span data-stu-id="f18a7-463">toomake sure your WebJobs are always running, and running on all instances of your web app, you have tooenable hello [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) feature.</span></span>

### <a name="using-hello-webjobs-sdk-outside-of-webjobs"></a><span data-ttu-id="f18a7-464">Merhaba WebJobs SDK Web işleri dışında kullanma</span><span class="sxs-lookup"><span data-stu-id="f18a7-464">Using hello WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="f18a7-465">Bir Web işi olarak azure'da hello WebJobs SDK kullanan bir program toorun sahip değil.</span><span class="sxs-lookup"><span data-stu-id="f18a7-465">A program that uses hello WebJobs SDK doesn't have toorun in Azure in a WebJob.</span></span> <span data-ttu-id="f18a7-466">Yerel olarak çalıştırabilir ve bulut hizmeti çalışan rolü veya bir Windows hizmeti gibi diğer ortamlarda da çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f18a7-466">It can run locally, and it can also run in other environments such as a Cloud Service worker role or a Windows service.</span></span> <span data-ttu-id="f18a7-467">Ancak, hello Web işleri SDK'si Pano yalnızca Azure web uygulaması erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f18a7-467">However, you can only access hello WebJobs SDK dashboard through an Azure web app.</span></span> <span data-ttu-id="f18a7-468">tooconnect hello web uygulama toohello depolama hesabı üzerinde hello hello AzureWebJobsDashboard bağlantı dizesi ayarlayarak kullanmakta olduğunuz sahip toouse hello Pano **yapılandırma** hello Klasik portal sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="f18a7-468">toouse hello dashboard you have tooconnect hello web app toohello storage account you're using by setting hello AzureWebJobsDashboard connection string on hello **Configure** tab of hello classic portal.</span></span> <span data-ttu-id="f18a7-469">Ardından, URL aşağıdaki hello kullanarak toohello Pano elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f18a7-469">Then, you can get toohello Dashboard by using hello following URL:</span></span>

<span data-ttu-id="f18a7-470">https://{webappname}.SCM.azurewebsites.NET/azurejobs/#/Functions</span><span class="sxs-lookup"><span data-stu-id="f18a7-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span></span>

<span data-ttu-id="f18a7-471">Daha fazla bilgi için bkz: [hello WebJobs SDK ile yerel geliştirme için bir Pano alma](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), ancak eski bir bağlantı dizesi adı gösterdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f18a7-471">For more information, see [Getting a dashboard for local development with hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that it shows an old connection string name.</span></span>

### <a name="more-webjobs-documentation"></a><span data-ttu-id="f18a7-472">Daha fazla Web işleri belgeleri</span><span class="sxs-lookup"><span data-stu-id="f18a7-472">More WebJobs documentation</span></span>
<span data-ttu-id="f18a7-473">Daha fazla bilgi için bkz: [Azure Web işleri belge kaynakları](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="f18a7-473">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span>
