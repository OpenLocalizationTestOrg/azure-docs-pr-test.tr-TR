---
title: "Azure App Service'te bir .NET WebJob oluşturma | Microsoft Docs"
description: "ASP.NET MVC ve Azure kullanarak çok katmanlı bir uygulama oluşturun. Bir web uygulamasını Azure App Service ve arka uç çalıştırır ön uç Web işi çalıştırır. Uygulama Entity Framework, SQL Database ve Azure depolama kuyrukları ve blobları kullanır."
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
ms.openlocfilehash: a20b13058caecff75af14957468f20e63a3325c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a><span data-ttu-id="571c7-105">Azure Uygulama Hizmeti’nde .NET WebJob oluşturma</span><span class="sxs-lookup"><span data-stu-id="571c7-105">Create a .NET WebJob in Azure App Service</span></span>
<span data-ttu-id="571c7-106">Bu öğretici kullanan basit bir çok katmanlı ASP.NET MVC 5 uygulama kodunun nasıl yazılacağını gösterir [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="571c7-106">This tutorial shows how to write code for a simple multi-tier ASP.NET MVC 5 application that uses the [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="571c7-107">Amacı [WebJobs SDK](websites-webjobs-resources.md) bir Web işi gerçekleştirebilirsiniz, görüntü işleme, sıra işleme, RSS toplama, dosya bakımı gibi ortak görevler için yazdığınız kodları kolaylaştırmaktır ve e-postaları gönderme.</span><span class="sxs-lookup"><span data-stu-id="571c7-107">The purpose of the [WebJobs SDK](websites-webjobs-resources.md) is to simplify the code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="571c7-108">Web işleri SDK'si, Azure Storage ve Service Bus ile çalışmak için görev zamanlama ve hataları işleme ve diğer birçok yaygın senaryolar için yerleşik özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="571c7-108">The WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="571c7-109">Ayrıca, Genişletilebilir olmak için tasarlanmıştır ve var. bir [uzantıları için açık kaynak deposu](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span><span class="sxs-lookup"><span data-stu-id="571c7-109">In addition, it's designed to be extensible, and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="571c7-110">Örnek uygulama bir reklam Bülteni panosudur.</span><span class="sxs-lookup"><span data-stu-id="571c7-110">The sample application is an advertising bulletin board.</span></span> <span data-ttu-id="571c7-111">Kullanıcılar yansımaları reklamları için karşıya yükleyebilir ve bir arka uç işlem görüntüleri küçük resimlere dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="571c7-111">Users can upload images for ads, and a backend process converts the images to thumbnails.</span></span> <span data-ttu-id="571c7-112">Ad listesi sayfası küçük resimleri gösterir ve ad Ayrıntılar sayfası tam boyutlu görüntüyü gösterir.</span><span class="sxs-lookup"><span data-stu-id="571c7-112">The ad list page shows the thumbnails, and the ad details page shows the full-size image.</span></span> <span data-ttu-id="571c7-113">Bir ekran görüntüsü aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="571c7-113">Here's a screenshot:</span></span>

![Reklam listesi](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

<span data-ttu-id="571c7-115">Bu örnek uygulama ile çalışır [Azure kuyrukları](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) ve [Azure BLOB'ları](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="571c7-115">This sample application works with [Azure queues](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) and [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span></span> <span data-ttu-id="571c7-116">Öğretici, uygulamayı dağıtmak gösterilmiştir [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) ve [Azure SQL veritabanı](http://msdn.microsoft.com/library/azure/ee336279).</span><span class="sxs-lookup"><span data-stu-id="571c7-116">The tutorial shows how to deploy the application to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span></span>

## <span data-ttu-id="571c7-117"><a id="prerequisites"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="571c7-117"><a id="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="571c7-118">Öğretici ile nasıl çalışılacağını bildiğinizi varsayar [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) Visual Studio projelerinde.</span><span class="sxs-lookup"><span data-stu-id="571c7-118">The tutorial assumes that you know how to work with [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projects in Visual Studio.</span></span>

<span data-ttu-id="571c7-119">Öğreticinin ilk olarak Visual Studio 2013 için yazılmıştır, ancak Visual Studio'nun daha yeni sürümlerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="571c7-119">The tutorial was originally written for Visual Studio 2013, but can be used with later versions of Visual Studio.</span></span> <span data-ttu-id="571c7-120">Visual Studio 2015 veya 2017 kullanıyorsanız, önce uygulamayı yerel olarak çalıştırın, değiştirmelisiniz Not `Data Source` Web.config ve App.config dosyaları SQL Server yerel veritabanı bağlantı dizesinde parçası `Data Source=(localdb)\v11.0` için `Data Source=(LocalDb)\MSSQLLocalDB`.</span><span class="sxs-lookup"><span data-stu-id="571c7-120">If you are using Visual Studio 2015 or 2017, make note that before you run the application locally, you must change the `Data Source` part of the SQL Server LocalDB connection string in the Web.config and App.config files from `Data Source=(localdb)\v11.0` to `Data Source=(LocalDb)\MSSQLLocalDB`.</span></span>

> [!NOTE]
> <span data-ttu-id="571c7-121"><a name="note"></a>Bu öğreticiyi tamamlamak için bir Azure hesabınızın olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="571c7-121"><a name="note"></a>You must have an Azure account to complete this tutorial:</span></span>
>
> * <span data-ttu-id="571c7-122">Yapabilecekleriniz [ücretsiz bir Azure hesabı açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): Ücretli Azure hizmetlerini denemek için kullanabileceğiniz, ve hatta kullanıldıktan sonra hesabı sürdürebilir ve Web siteleri gibi ücretsiz Azure hizmetlerine krediler alırsınız.</span><span class="sxs-lookup"><span data-stu-id="571c7-122">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): You get credits that you can use to try out paid Azure services, and even after they're used up, you can keep the account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="571c7-123">Açıkça ayarlarınızı değiştirip ücretlendirme istemediğiniz sürece kredi kartınız asla ücretlendirilmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="571c7-123">Your credit card will never be charged, unless you explicitly change your settings and ask to be charged.</span></span>
> * <span data-ttu-id="571c7-124">Yapabilecekleriniz [Visual Studio aboneleri için aylık Azure kredi etkinleştirme](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): aboneliğinizi Ücretli Azure hizmetlerinizi kullanabildiğiniz her ay kredi verir.</span><span class="sxs-lookup"><span data-stu-id="571c7-124">You can [activate Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): Your subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="571c7-125">Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="571c7-125">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="571c7-126">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="571c7-126">No credit cards required; no commitments.</span></span>
>
>

## <span data-ttu-id="571c7-127"><a id="learn"></a>Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="571c7-127"><a id="learn"></a>What you'll learn</span></span>
<span data-ttu-id="571c7-128">Öğretici aşağıdaki görevlerin nasıl yapılacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="571c7-128">The tutorial shows how to do the following tasks:</span></span>

* <span data-ttu-id="571c7-129">Makinenizi Azure geliştirme için Azure SDK'sını (yalnızca Visual Studio 2013 ve 2015 kullanıcılar için) yükleyerek etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="571c7-129">Enable your machine for Azure development by installing the Azure SDK (only for Visual Studio 2013 and 2015 users).</span></span>
* <span data-ttu-id="571c7-130">İlişkili web projesi dağıttığınızda, bir Azure Web işi otomatik olarak dağıtan bir konsol uygulama projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="571c7-130">Create a Console Application project that automatically deploys as an Azure WebJob when you deploy the associated web project.</span></span>
* <span data-ttu-id="571c7-131">Web işleri SDK'si arka uç geliştirme bilgisayarındaki yerel olarak test edin.</span><span class="sxs-lookup"><span data-stu-id="571c7-131">Test a WebJobs SDK backend locally on the development computer.</span></span>
* <span data-ttu-id="571c7-132">App Service'teki bir web uygulaması için Web işleri arka ucu ile bir uygulama yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="571c7-132">Publish an application with a WebJobs backend to a web app in App Service.</span></span>
* <span data-ttu-id="571c7-133">Dosyaları karşıya yükleme ve Azure Blob hizmetine depolama.</span><span class="sxs-lookup"><span data-stu-id="571c7-133">Upload files and store them in the Azure Blob service.</span></span>
* <span data-ttu-id="571c7-134">Azure Storage kuyruklarını ve BLOB'ları ile çalışmak için Azure WebJobs SDK'sını kullanın.</span><span class="sxs-lookup"><span data-stu-id="571c7-134">Use the Azure WebJobs SDK to work with Azure Storage queues and blobs.</span></span>

## <span data-ttu-id="571c7-135"><a id="contosoads"></a>Uygulama mimarisi</span><span class="sxs-lookup"><span data-stu-id="571c7-135"><a id="contosoads"></a>Application architecture</span></span>
<span data-ttu-id="571c7-136">Örnek uygulama kullanır [kuyruk merkezli çalışma deseni](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) bir arka uç işleme küçük resimler oluşturma CPU yoğunluklu iş yükünü azaltmak için.</span><span class="sxs-lookup"><span data-stu-id="571c7-136">The sample application uses the [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) to off-load the CPU-intensive work of creating thumbnails to a backend process.</span></span>

<span data-ttu-id="571c7-137">Uygulama, tablolar oluşturmak ve verilere erişmek için Entity Framework Code First kullanarak reklamları bir SQL veritabanına depolar.</span><span class="sxs-lookup"><span data-stu-id="571c7-137">The app stores ads in a SQL database, using Entity Framework Code First to create the tables and access the data.</span></span> <span data-ttu-id="571c7-138">Her reklam için veritabanı iki URL depolar: biri tam boyutlu görüntü ve diğeri küçük resim.</span><span class="sxs-lookup"><span data-stu-id="571c7-138">For each ad, the database stores two URLs: one for the full-size image and one for the thumbnail.</span></span>

![Reklam tablosu](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

<span data-ttu-id="571c7-140">Bir kullanıcı görüntü yüklediğinde, web uygulaması görüntüde depolayan bir [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), ve reklam bilgilerini blob'u işaret eden bir URL veritabanıyla depolar.</span><span class="sxs-lookup"><span data-stu-id="571c7-140">When a user uploads an image, the web app stores the image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores the ad information in the database with a URL that points to the blob.</span></span> <span data-ttu-id="571c7-141">Aynı zamanda bir Azure kuyruğuna ileti yazar.</span><span class="sxs-lookup"><span data-stu-id="571c7-141">At the same time, it writes a message to an Azure queue.</span></span> <span data-ttu-id="571c7-142">Bir Azure Web işi çalışan bir arka uç işleminde sıra yeni iletiler için Web işleri SDK'si yoklar.</span><span class="sxs-lookup"><span data-stu-id="571c7-142">In a backend process running as an Azure WebJob, the WebJobs SDK polls the queue for new messages.</span></span> <span data-ttu-id="571c7-143">Yeni bir ileti görüntülendiğinde, Web işi, görüntü için bir küçük resim oluşturur ve küçük resim URL'si veritabanı alanını bu reklam için güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="571c7-143">When a new message appears, the WebJob creates a thumbnail for that image and updates the thumbnail URL database field for that ad.</span></span> <span data-ttu-id="571c7-144">Uygulama bölümlerinin nasıl etkileşim gösteren diyagram şöyledir:</span><span class="sxs-lookup"><span data-stu-id="571c7-144">Here's a diagram that shows how the parts of the application interact:</span></span>

![Contoso Ads mimarisi](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
<span data-ttu-id="571c7-146">Öğretici yönergeleri 2.7.1 .NET için Azure SDK'SININ uygulamak veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="571c7-146">The tutorial instructions apply to Azure SDK for .NET 2.7.1 or later.</span></span>

## <span data-ttu-id="571c7-147"><a id="storage"></a>Bir Azure depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="571c7-147"><a id="storage"></a>Create an Azure Storage account</span></span>
<span data-ttu-id="571c7-148">Azure Storage hesabı kuyruk ve blob verilerini buluta depolamaya yönelik kaynaklar sağlar.</span><span class="sxs-lookup"><span data-stu-id="571c7-148">An Azure storage account provides resources for storing queue and blob data in the cloud.</span></span> <span data-ttu-id="571c7-149">Pano günlük verilerini depolamak için bu WebJobs SDK'sı tarafından da kullanılır.</span><span class="sxs-lookup"><span data-stu-id="571c7-149">It's also used by the WebJobs SDK to store logging data for the dashboard.</span></span>

<span data-ttu-id="571c7-150">Gerçek dünya uygulamada genellikle uygulama verilerine karşı günlük verileri için ayrı hesaplar ve test verilerine karşı üretim verileri için ayrı hesaplar oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="571c7-150">In a real-world application, you typically create separate accounts for application data versus logging data and separate accounts for test data versus production data.</span></span> <span data-ttu-id="571c7-151">Bu öğreticide yalnızca tek bir hesap kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="571c7-151">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="571c7-152">Açık **Sunucu Gezgini** Visual Studio'daki.</span><span class="sxs-lookup"><span data-stu-id="571c7-152">Open the **Server Explorer** window in Visual Studio.</span></span>
2. <span data-ttu-id="571c7-153">Sağ **Azure** düğümünü ve ardından **Microsoft Azure aboneliğine Bağlan...** .</span><span class="sxs-lookup"><span data-stu-id="571c7-153">Right-click the **Azure** node, and then click **Connect to Microsoft Azure Subscription...**.</span></span>
   
   ![Azure'a Bağlanma](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. <span data-ttu-id="571c7-155">Azure kimlik bilgilerinizi kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="571c7-155">Sign in using your Azure credentials.</span></span>
4. <span data-ttu-id="571c7-156">Sağ **depolama** Azure düğümünü ve ardından altında **depolama hesabı oluştur**.</span><span class="sxs-lookup"><span data-stu-id="571c7-156">Right-click **Storage** under the Azure node, and then click **Create Storage Account**.</span></span>
   
   ![Depolama hesabı oluşturma](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. <span data-ttu-id="571c7-158">İçinde **depolama hesabı oluştur** iletişim kutusunda, depolama hesabı için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="571c7-158">In the **Create Storage Account** dialog, enter a name for the storage account.</span></span>

    <span data-ttu-id="571c7-159">Adı olmalı benzersiz olmalıdır (başka bir Azure depolama hesabı aynı ada sahip olabilir).</span><span class="sxs-lookup"><span data-stu-id="571c7-159">The name must be must be unique (no other Azure storage account can have the same name).</span></span> <span data-ttu-id="571c7-160">Girdiğiniz ad zaten kullanımda değiştirmek için bir fırsat alırsınız.</span><span class="sxs-lookup"><span data-stu-id="571c7-160">If the name you enter is already in use, you'll get a chance to change it.</span></span>

    <span data-ttu-id="571c7-161">Depolama hesabınıza erişmek için URL *{ad}*. core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="571c7-161">The URL to access your storage account will be *{name}*.core.windows.net.</span></span>
6. <span data-ttu-id="571c7-162">Ayarlama **bölge veya benzeşim grubunda** size en yakın bölgeyi aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="571c7-162">Set the **Region or Affinity Group** drop-down list to the region closest to you.</span></span>

    <span data-ttu-id="571c7-163">Bu ayar, hangi Azure veri merkezi depolama hesabınız barındıracak belirtir.</span><span class="sxs-lookup"><span data-stu-id="571c7-163">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="571c7-164">Bu öğretici için tercih ettiğiniz bir dikkat çekici fark yapmaz.</span><span class="sxs-lookup"><span data-stu-id="571c7-164">For this tutorial, your choice won't make a noticeable difference.</span></span> <span data-ttu-id="571c7-165">Ancak, bir üretim web uygulaması için web sunucunuz ve gecikme süresi ve veri çıkış ücretleri en aza indirmek için aynı bölgede olması için depolama hesabınız istiyor.</span><span class="sxs-lookup"><span data-stu-id="571c7-165">However, for a production web app, you want your web server and your storage account to be in the same region to minimize latency and data egress charges.</span></span> <span data-ttu-id="571c7-166">(Daha sonra oluşturacağınız) web uygulamasını datacenter gecikme süresi en aza indirmek için web uygulamasına erişme tarayıcılar mümkün olduğunca yakın.</span><span class="sxs-lookup"><span data-stu-id="571c7-166">The web app (which you'll create later) datacenter should be as close as possible to the browsers accessing the web app in order to minimize latency.</span></span>
7. <span data-ttu-id="571c7-167">**Çoğaltma** açılır listesini **Yerel olarak yedekli** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="571c7-167">Set the **Replication** drop-down list to **Locally redundant**.</span></span>

    <span data-ttu-id="571c7-168">Bir depolama hesabı için coğrafi çoğaltma etkinleştirildiğinde, birincil konumda önemli bir olağanüstü durum oluşması halinde ikincil bir veri merkezine yük devretme için depolanan içerik bu konuma çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="571c7-168">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover to that location in case of a major disaster in the primary location.</span></span> <span data-ttu-id="571c7-169">Coğrafi çoğaltma ek ücretlere neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="571c7-169">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="571c7-170">Test ve geliştirme hesaplarında genellikle coğrafi çoğaltma için ödeme yapmak istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="571c7-170">For test and development accounts, you generally don't want to pay for geo-replication.</span></span> <span data-ttu-id="571c7-171">Daha fazla bilgi için bkz. [Depolama hesabı oluşturma, yönetme veya silme](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="571c7-171">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
8. <span data-ttu-id="571c7-172">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="571c7-172">Click **Create**.</span></span>

    ![Yeni depolama hesabı](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <span data-ttu-id="571c7-174"><a id="download"></a>Uygulamayı Yükle</span><span class="sxs-lookup"><span data-stu-id="571c7-174"><a id="download"></a>Download the application</span></span>
1. <span data-ttu-id="571c7-175">[Tamamlanan çözümü](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb) indirip sıkıştırmasını açın.</span><span class="sxs-lookup"><span data-stu-id="571c7-175">Download and unzip the [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span></span>
2. <span data-ttu-id="571c7-176">Visual Studio’yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="571c7-176">Start Visual Studio.</span></span>
3. <span data-ttu-id="571c7-177">Gelen **dosya** menüsünü seçin **Aç > Proje/çözüm**, çözümü indirdiğiniz yere gidin ve ardından çözüm dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="571c7-177">From the **File** menu choose **Open > Project/Solution**, navigate to where you downloaded the solution, and then open the solution file.</span></span>
4. <span data-ttu-id="571c7-178">Çözümü derlemek için CTRL+SHIFT+B'ye basın.</span><span class="sxs-lookup"><span data-stu-id="571c7-178">Press CTRL+SHIFT+B to build the solution.</span></span>

    <span data-ttu-id="571c7-179">Varsayılan olarak Visual Studio, *.zip* dosyasına dahil edilmeyen NuGet paketini otomatik olarak geri yükler.</span><span class="sxs-lookup"><span data-stu-id="571c7-179">By default, Visual Studio automatically restores the NuGet package content, which was not included in the *.zip* file.</span></span> <span data-ttu-id="571c7-180">Paketler geri yüklenmezse varsa bunları el ile giderek yükleyin **çözüm için NuGet paketlerini Yönet** iletişim ve tıklayarak **geri** sağ üst köşedeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="571c7-180">If the packages don't restore, install them manually by going to the **Manage NuGet Packages for Solution** dialog and clicking the **Restore** button at the top right.</span></span>
5. <span data-ttu-id="571c7-181">İçinde **Çözüm Gezgini**, olduğundan emin olun **ContosoAdsWeb** başlangıç projesi olarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="571c7-181">In **Solution Explorer**, make sure that **ContosoAdsWeb** is selected as the startup project.</span></span>

## <span data-ttu-id="571c7-182"><a id="configurestorage"></a>Depolama hesabınızı kullanmak için uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="571c7-182"><a id="configurestorage"></a>Configure the application to use your storage account</span></span>
1. <span data-ttu-id="571c7-183">Uygulamayı açmak *Web.config* ContosoAdsWeb projesinde dosya.</span><span class="sxs-lookup"><span data-stu-id="571c7-183">Open the application *Web.config* file in the ContosoAdsWeb project.</span></span>

    <span data-ttu-id="571c7-184">Dosya, bir SQL bağlantı dizesi ve BLOB'lar ve kuyruklarla çalışmaya yönelik bir Azure depolama bağlantı dizesi içerir.</span><span class="sxs-lookup"><span data-stu-id="571c7-184">The file contains a SQL connection string and an Azure storage connection string for working with blobs and queues.</span></span>

    <span data-ttu-id="571c7-185">SQL bağlantı dizesi işaret bir [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) veritabanı.</span><span class="sxs-lookup"><span data-stu-id="571c7-185">The SQL connection string points to a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span></span>

    <span data-ttu-id="571c7-186">Depolama bağlantı dizesi yer tutucuları depolama hesabı adı ve erişim anahtarı için olan bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="571c7-186">The storage connection string is an example that has placeholders for the storage account name and access key.</span></span> <span data-ttu-id="571c7-187">Bu ad ve anahtar depolama hesabınızın sahip bir bağlantı dizesi ile değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="571c7-187">You'll replace this with a connection string that has the name and key of your storage account.</span></span>  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    <span data-ttu-id="571c7-188">Depolama bağlantı dizesi, Web işleri SDK'si kullandığı adı olduğundan AzureWebJobsStorage varsayılan olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="571c7-188">The storage connection string is named AzureWebJobsStorage because that's the name the WebJobs SDK uses by default.</span></span> <span data-ttu-id="571c7-189">Azure ortamında yalnızca bir bağlantı dizesi değerine ayarlamanız gerekir böylece aynı adı burada kullanılır.</span><span class="sxs-lookup"><span data-stu-id="571c7-189">The same name is used here so you have to set only one connection string value in the Azure environment.</span></span>
2. <span data-ttu-id="571c7-190">İçinde **Sunucu Gezgini**, depolama hesabınızın altında sağ **depolama** düğümünü ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="571c7-190">In **Server Explorer**, right-click your storage account under the **Storage** node, and then click **Properties**.</span></span>

    ![Depolama hesabı Özellikler'i tıklatın](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. <span data-ttu-id="571c7-192">İçinde **özellikleri** penceresinde, tıklatın **depolama hesabı anahtarlarını**ve üç nokta'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="571c7-192">In the **Properties** window, click **Storage Account Keys**, and then click the ellipsis.</span></span>

    ![Depolama hesabı anahtarları](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. <span data-ttu-id="571c7-194">Kopya **bağlantı dizesi**.</span><span class="sxs-lookup"><span data-stu-id="571c7-194">Copy the **Connection String**.</span></span>

    ![Depolama hesabı anahtarları iletişim](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. <span data-ttu-id="571c7-196">Depolama bağlantı dizesini değiştirin *Web.config* kopyaladığınız bağlantı dizesini içeren dosya.</span><span class="sxs-lookup"><span data-stu-id="571c7-196">Replace the storage connection string in the *Web.config* file with the connection string you just copied.</span></span> <span data-ttu-id="571c7-197">Her şeyi tırnak işaretleri içindeki ancak yapıştırmadan önce tırnak işaretleri dahil değil seçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="571c7-197">Make sure you select everything inside the quotation marks but not including the quotation marks before pasting.</span></span>
6. <span data-ttu-id="571c7-198">Açık *App.config* ContosoAdsWebJob proje dosyasında.</span><span class="sxs-lookup"><span data-stu-id="571c7-198">Open the *App.config* file in the ContosoAdsWebJob project.</span></span>

    <span data-ttu-id="571c7-199">Bu dosya iki depolama bağlantı dizeleri, bir uygulama verileri için ve günlüğe kaydetme için bir sahiptir.</span><span class="sxs-lookup"><span data-stu-id="571c7-199">This file has two storage connection strings, one for application data and one for logging.</span></span> <span data-ttu-id="571c7-200">Uygulama verilerini ve günlüğe kaydetme için ayrı bir depolama hesaplarını kullanabilirsiniz ve kullanabileceğiniz [birden çok depolama hesapları için verileri](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="571c7-200">You can use separate storage accounts for application data and logging, and you can use [multiple storage accounts for data](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span> <span data-ttu-id="571c7-201">Bu öğreticide, tek bir depolama hesabına kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="571c7-201">For this tutorial, you'll use a single storage account.</span></span> <span data-ttu-id="571c7-202">Depolama hesabı anahtarlarını yer tutucular bağlantı dizelerine sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="571c7-202">The connection strings have placeholders for the storage account keys.</span></span>

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

    <span data-ttu-id="571c7-203">Varsayılan olarak, Web işleri SDK'si için bağlantı dizelerini AzureWebJobsStorage ve AzureWebJobsDashboard adlı arar.</span><span class="sxs-lookup"><span data-stu-id="571c7-203">By default, the WebJobs SDK looks for connection strings named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="571c7-204">Alternatif olarak, şunları yapabilirsiniz [deposu bağlantı dizesi ancak istediğiniz ve içinde açıkça geçirmek `JobHost` nesne](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span><span class="sxs-lookup"><span data-stu-id="571c7-204">As an alternative, you can [store the connection string however you want and pass it in explicitly to the `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span></span>
7. <span data-ttu-id="571c7-205">Her iki storage bağlantı dizelerini daha önce kopyaladığınız bağlantı dizesi ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="571c7-205">Replace both storage connection strings with the connection string you copied earlier.</span></span>
8. <span data-ttu-id="571c7-206">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="571c7-206">Save your changes.</span></span>

## <span data-ttu-id="571c7-207"><a id="run"></a>Uygulamayı yerel olarak çalıştırın</span><span class="sxs-lookup"><span data-stu-id="571c7-207"><a id="run"></a>Run the application locally</span></span>
1. <span data-ttu-id="571c7-208">Web ön uç uygulamasının başlatmak için CTRL + F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="571c7-208">To start the web frontend of the application, press CTRL+F5.</span></span>

    <span data-ttu-id="571c7-209">Varsayılan tarayıcı giriş sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="571c7-209">The default browser opens to the home page.</span></span> <span data-ttu-id="571c7-210">(Web projesini başlangıç projesi yapmış olduğunuz için çalışır.)</span><span class="sxs-lookup"><span data-stu-id="571c7-210">(The web project runs because you've made it the startup project.)</span></span>

    ![Contoso Ads giriş sayfası](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. <span data-ttu-id="571c7-212">Web işi arka uç uygulamasının başlatmak için ContosoAdsWebJob projeye sağ **Çözüm Gezgini**ve ardından **hata ayıklama** > **başlangıç yeni örnek**.</span><span class="sxs-lookup"><span data-stu-id="571c7-212">To start the WebJob backend of the application, right-click the ContosoAdsWebJob project in **Solution Explorer**, and then click **Debug** > **Start new instance**.</span></span>

    <span data-ttu-id="571c7-213">Bir konsol uygulama penceresi açar ve WebJobs SDK JobHost nesne çalışmaya başladı belirten günlük iletilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="571c7-213">A console application window opens and displays logging messages indicating the WebJobs SDK JobHost object has started to run.</span></span>

    ![Arka uç çalıştığını gösteren konsol uygulama penceresi](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. <span data-ttu-id="571c7-215">Tarayıcınızda, tıklatın **bir Ad oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="571c7-215">In your browser, click  **Create an Ad**.</span></span>
4. <span data-ttu-id="571c7-216">Bazı test verilerini girin, karşıya yükleyin ve ardından bir görüntü seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="571c7-216">Enter some test data, select an image to upload, and then click **Create**.</span></span>

    ![Sayfa oluşturma](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    <span data-ttu-id="571c7-218">Uygulama Dizin sayfasına gider, ancak işleme henüz tamamlanmadığından yeni reklam için bir küçük resim göstermez.</span><span class="sxs-lookup"><span data-stu-id="571c7-218">The app goes to the Index page, but it doesn't show a thumbnail for the new ad because that processing hasn't happened yet.</span></span>

    <span data-ttu-id="571c7-219">Bu sırada, kısa bir bekleme bir kuyruk iletisi alındı ve işlenmiş olan bir günlük iletisi konsol uygulaması penceresinde gösterir.</span><span class="sxs-lookup"><span data-stu-id="571c7-219">Meanwhile, after a short wait a logging message in the console application window shows that a queue message was received and has been processed.</span></span>

    ![Bir kuyruk iletisi işlendiğini gösteren konsol uygulama penceresi](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. <span data-ttu-id="571c7-221">Konsol uygulaması penceresinde günlük iletilerini gördükten sonra küçük resmi görmek için dizin sayfasını yenileyin.</span><span class="sxs-lookup"><span data-stu-id="571c7-221">After you see the logging messages in the console application window, refresh the Index page to see the thumbnail.</span></span>

    ![Dizin sayfası](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. <span data-ttu-id="571c7-223">Tam boyutlu görüntüyü görmek için reklamınıza ilişkin **Ayrıntılar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="571c7-223">Click **Details** for your ad to see the full-size image.</span></span>

    ![Ayrıntılar sayfası](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

<span data-ttu-id="571c7-225">Uygulama'yı yerel bilgisayarınızda çalışır durumda ve bir SQL veritabanı bilgisayarınızı, ancak üzerinde bulunan Kuyruklarla Çalışma ve içinde BLOB'ların sunucusu kullanarak bulut.</span><span class="sxs-lookup"><span data-stu-id="571c7-225">You've been running the application on your local computer, and it's using a SQL Server database located on your computer, but it's working with queues and blobs in the cloud.</span></span> <span data-ttu-id="571c7-226">Aşağıdaki bölümde bulut veritabanı yanı sıra bulut BLOB'ları ve kuyrukları kullanma uygulaması bulutta çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="571c7-226">In the following section you'll run the application in the cloud, using a cloud database as well as cloud blobs and queues.</span></span>  

## <span data-ttu-id="571c7-227"><a id="runincloud"></a>Uygulamayı bulutta çalıştırın</span><span class="sxs-lookup"><span data-stu-id="571c7-227"><a id="runincloud"></a>Run the application in the cloud</span></span>
<span data-ttu-id="571c7-228">Uygulamayı bulutta çalıştırmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="571c7-228">You'll do the following steps to run the application in the cloud:</span></span>

* <span data-ttu-id="571c7-229">Web uygulamaları dağıtın.</span><span class="sxs-lookup"><span data-stu-id="571c7-229">Deploy to Web Apps.</span></span> <span data-ttu-id="571c7-230">Visual Studio otomatik olarak yeni bir web uygulaması App Service ve bir SQL veritabanı örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="571c7-230">Visual Studio automatically creates a new web app in App Service and a SQL Database instance.</span></span>
* <span data-ttu-id="571c7-231">Web uygulaması, Azure SQL veritabanı ve depolama hesabınızı kullanacak şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="571c7-231">Configure the web app to use your Azure SQL database and storage account.</span></span>

<span data-ttu-id="571c7-232">Bulutta çalıştırılırken bazı ads oluşturduktan sonra izleme özelliklerini sunmak için sahip zengin görmek için Web işleri SDK'si Panoyu görebilmek.</span><span class="sxs-lookup"><span data-stu-id="571c7-232">After you've created some ads while running in the cloud, you'll view the WebJobs SDK dashboard to see the rich monitoring features it has to offer.</span></span>

### <a name="deploy-to-web-apps"></a><span data-ttu-id="571c7-233">Web uygulamaları dağıtma</span><span class="sxs-lookup"><span data-stu-id="571c7-233">Deploy to Web Apps</span></span>

1. <span data-ttu-id="571c7-234">Tarayıcı ve konsol uygulaması penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="571c7-234">Close the browser and the console application window.</span></span>
2. <span data-ttu-id="571c7-235">Adımları [Azure SQL veritabanı ile Yayımla](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) bölümü.</span><span class="sxs-lookup"><span data-stu-id="571c7-235">Follow the steps in the [Publish to Azure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) section.</span></span>
3. <span data-ttu-id="571c7-236">Dağıtma adımları tamamladıktan sonra bu makaledeki kalan görevlere devam edin.</span><span class="sxs-lookup"><span data-stu-id="571c7-236">After you complete the steps for deploying, continue with the remaining tasks in this article.</span></span>

### <a name="configure-the-web-app-to-use-your-azure-sql-database-and-storage-account"></a><span data-ttu-id="571c7-237">Azure SQL veritabanı ve depolama hesabınızı kullanmak için web uygulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="571c7-237">Configure the web app to use your Azure SQL database and storage account</span></span>
<span data-ttu-id="571c7-238">Bir güvenlik en iyi uygulama olan [bağlantı dizeleri gibi hassas bilgileri kaynak kodu depoları içinde depolanan dosyaları içinde Geçirilmemesi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="571c7-238">It's a security best practice to [avoid putting sensitive information such as connection strings in files that are stored in source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span> <span data-ttu-id="571c7-239">Azure Bunu yapmak için bir yöntem sunar: ASP.NET yapılandırma API'leri uygulama Azure'da çalıştırıldığında bu değerleri otomatik olarak seçmesini ve Azure ortamında bağlantı dizesini ve diğer ayar değerlerini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="571c7-239">Azure provides a way to do that: you can set connection string and other setting values in the Azure environment, and ASP.NET configuration APIs automatically pick up these values when the app runs in Azure.</span></span> <span data-ttu-id="571c7-240">Bu değerleri kullanarak Azure'da ayarlayabilirsiniz **Sunucu Gezgini**, Azure portalı, Windows PowerShell veya platformlar arası komut satırı arabirimi.</span><span class="sxs-lookup"><span data-stu-id="571c7-240">You can set these values in Azure by using **Server Explorer**, the Azure Portal, Windows PowerShell, or the cross-platform command-line interface.</span></span> <span data-ttu-id="571c7-241">Daha fazla bilgi için bkz: [nasıl uygulama dizeleri ve bağlantı dizeleri çalışma](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="571c7-241">For more information, see [How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span>

<span data-ttu-id="571c7-242">Bu bölümde, kullandığınız **Sunucu Gezgini** bağlantı ile Azure dize değerlerini ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="571c7-242">In this section, you use **Server Explorer** to set connection string values in Azure.</span></span>

1. <span data-ttu-id="571c7-243">İçinde **Sunucu Gezgini**, web uygulamanızı altında sağ **Azure > uygulama hizmeti > {kaynak grubunuz}**ve ardından **görünüm ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="571c7-243">In **Server Explorer**, right-click your web app under **Azure > App Service > {your resource group}**, and then click **View Settings**.</span></span>

    <span data-ttu-id="571c7-244">**Azure Web uygulaması** penceresi açılır **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="571c7-244">The **Azure Web App** window opens on the **Configuration** tab.</span></span>
2. <span data-ttu-id="571c7-245">Seçtiğiniz SQL veritabanında yapılandırdığınızda adına DefaultConnection bağlantı dizesinin adını değiştirmek [Azure SQL veritabanı ile Yayımla](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) makalesi.</span><span class="sxs-lookup"><span data-stu-id="571c7-245">Change the name of the DefaultConnection connection string to the name you chose when you configured the SQL database in the [Publish to Azure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) article.</span></span>

    <span data-ttu-id="571c7-246">Doğru bağlantı dizesi değeri zaten şekilde ilişkilendirilmiş bir veritabanı ile web uygulaması oluşturduğunuzda azure, bu bağlantı dizesi otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="571c7-246">Azure automatically created this connection string when you created the web app with an associated database, so it already has the right connection string value.</span></span> <span data-ttu-id="571c7-247">Kodunuzu görmek için yalnızca adını değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="571c7-247">You're changing just the name to what your code is looking for.</span></span>
3. <span data-ttu-id="571c7-248">AzureWebJobsStorage ve AzureWebJobsDashboard adlı iki yeni bağlantı dizeleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="571c7-248">Add two new connection strings, named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="571c7-249">Veritabanı türü kümesine **özel**ve bağlantı dizesi değerini daha önce kullandığınız aynı değere ayarlayın *Web.config* ve *App.config* dosyaları.</span><span class="sxs-lookup"><span data-stu-id="571c7-249">Set the database type to **Custom**, and set the connection string value to the same value that you used earlier for the *Web.config* and *App.config* files.</span></span> <span data-ttu-id="571c7-250">(Tüm bağlantı dizesi, yalnızca erişim anahtarı içerir ve tırnak işaretleri dahil etmeyin emin olun.)</span><span class="sxs-lookup"><span data-stu-id="571c7-250">(Be sure you include the entire connection string, not just the access key, and don't include the quotation marks.)</span></span>

    <span data-ttu-id="571c7-251">Bu bağlantı dizeleri WebJobs SDK tarafından kullanılan uygulama verileri, diğeri için günlük için.</span><span class="sxs-lookup"><span data-stu-id="571c7-251">These connection strings are used by the WebJobs SDK, one for application data and one for logging.</span></span> <span data-ttu-id="571c7-252">Daha önce gördüğünüz gibi bir uygulama verileri için de web ön uç kodu tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="571c7-252">As you saw earlier, the one for application data is also used by the web front-end code.</span></span>
4. <span data-ttu-id="571c7-253">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="571c7-253">Click **Save**.</span></span>

    ![Azure Portalı'nda bağlantı dizeleri](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. <span data-ttu-id="571c7-255">İçinde **Sunucu Gezgini**, web uygulaması sağ tıklayın ve ardından **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="571c7-255">In **Server Explorer**, right-click the web app, and then click **Stop**.</span></span>
6. <span data-ttu-id="571c7-256">Web uygulaması durdurulduktan sonra web uygulaması tekrar sağ tıklayın ve ardından **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="571c7-256">After the web app stops, right-click the web app again, and then click **Start**.</span></span>

   <span data-ttu-id="571c7-257">Web işi yayımladığınızda, ancak bir yapılandırma değişikliği yaptığınızda durdurur otomatik olarak başlar.</span><span class="sxs-lookup"><span data-stu-id="571c7-257">The WebJob automatically starts when you publish, but it stops when you make a configuration change.</span></span> <span data-ttu-id="571c7-258">Yeniden başlatmak için web uygulaması yeniden veya WebJob içinde yeniden [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="571c7-258">To restart it, you can either restart the web app or restart the WebJob in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="571c7-259">Bu genellikle bir yapılandırma değişikliğinden sonra web uygulaması yeniden önerilir.</span><span class="sxs-lookup"><span data-stu-id="571c7-259">It's generally recommended to restart the web app after a configuration change.</span></span>
7. <span data-ttu-id="571c7-260">Web uygulaması URL'si kendi adres çubuğunda sahip tarayıcı penceresini yenileyin.</span><span class="sxs-lookup"><span data-stu-id="571c7-260">Refresh the browser window that has the web app URL in its address bar.</span></span>

    <span data-ttu-id="571c7-261">Giriş sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="571c7-261">The home page appears.</span></span>
8. <span data-ttu-id="571c7-262">Ne zaman yaptığınız gibi bir ad oluşturun, [uygulama yerel olarak çalıştırılan](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span><span class="sxs-lookup"><span data-stu-id="571c7-262">Create an ad, as you did when you [ran the application locally](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span></span>

   <span data-ttu-id="571c7-263">Küçük resim ilk olmadan dizin sayfası gösterilir.</span><span class="sxs-lookup"><span data-stu-id="571c7-263">The Index page shows without a thumbnail at first.</span></span>
9. <span data-ttu-id="571c7-264">Birkaç saniye sonra sayfayı yenileyin ve küçük resim görünür.</span><span class="sxs-lookup"><span data-stu-id="571c7-264">Refresh the page after a few seconds and the thumbnail appears.</span></span>

   <span data-ttu-id="571c7-265">Küçük resim görünmüyorsa, veya bunu yeniden başlatmak Web işi için bir dakika beklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="571c7-265">If the thumbnail doesn't appear, you might have to wait a minute or so for the WebJob to restart.</span></span> <span data-ttu-id="571c7-266">Sayfa yenilediğinizde bir süre sonra hala küçük resim görmüyorsanız, Web işi otomatik olarak başlatılmamış olabilir.</span><span class="sxs-lookup"><span data-stu-id="571c7-266">If after a while, you still don't see the thumbnail when you refresh the page, the WebJob might not have started automatically.</span></span> <span data-ttu-id="571c7-267">Bu durumda, Git **uygulama hizmetleri** dikey penceresinde [Azure portal](https://portal.azure.com/), web uygulamanızı bulun ve ardından **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="571c7-267">In that case, go to the **App Services** blade in the [Azure portal](https://portal.azure.com/), locate your web app, and then click **Start**.</span></span>

### <a name="view-the-webjobs-sdk-dashboard"></a><span data-ttu-id="571c7-268">Web işleri SDK'si Pano görünümü</span><span class="sxs-lookup"><span data-stu-id="571c7-268">View the WebJobs SDK dashboard</span></span>
1. <span data-ttu-id="571c7-269">İçinde [Azure portal](https://portal.azure.com/)seçin **App Services dikey**web uygulamanızı bulun ve seçin **WebJobs**.</span><span class="sxs-lookup"><span data-stu-id="571c7-269">In the [Azure portal](https://portal.azure.com/), select the **App Services blade**, locate your web app, and select **WebJobs**.</span></span>
3. <span data-ttu-id="571c7-270">Seçin **günlükleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="571c7-270">Select the **Logs** tab.</span></span>

    ![Günlükleri sekmesi](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    <span data-ttu-id="571c7-272">Web işleri SDK'si Pano için yeni bir tarayıcı sekmesi açar.</span><span class="sxs-lookup"><span data-stu-id="571c7-272">A new browser tab opens to the WebJobs SDK dashboard.</span></span> <span data-ttu-id="571c7-273">WebJob çalışıyor ve işlevlerin bir listesini kodunuzda WebJobs SDK tetiklenen gösterir Panosu gösterir.</span><span class="sxs-lookup"><span data-stu-id="571c7-273">The dashboard shows that the WebJob is running and shows a list of functions in your code that the WebJobs SDK triggered.</span></span>
4. <span data-ttu-id="571c7-274">Yürütülmesinin ayrıntılarını görmek için işlevleri birini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="571c7-274">Click one of the functions to see details about its execution.</span></span>

    ![Web işleri SDK'si Panosu](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![Web işleri SDK'si Panosu](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    <span data-ttu-id="571c7-277">**Yeniden yürütme işlevi** düğmesi, bu sayfada işlevi yeniden çağırın Web işleri SDK'si framework neden olur ve ilk işlevine geçirilen verileri değiştirme olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="571c7-277">The **Replay Function** button on this page causes the WebJobs SDK framework to call the function again, and it gives you a chance to change the data passed to the function first.</span></span>

> [!NOTE]
> <span data-ttu-id="571c7-278">Bitirdiğinizde test, web uygulaması, depolama hesabı ve SQL veritabanı örneğinde silme düşünün.</span><span class="sxs-lookup"><span data-stu-id="571c7-278">When you're finished testing, consider deleting the web app, storage account, and your SQL Database instance.</span></span> <span data-ttu-id="571c7-279">Web uygulaması ücretsizdir, ancak SQL depolama hesabı ve veritabanı örneği ücretler tahakkuk (barındırabilir, küçük boyutu en az).</span><span class="sxs-lookup"><span data-stu-id="571c7-279">The web app is free, but the SQL storage account and database instance accrue charges (albeit, minimal due to the small size).</span></span> <span data-ttu-id="571c7-280">Ayrıca, çalışan web uygulaması değiştirmeden bırakırsanız, URL'nizi bulan herkes oluşturun ve reklamları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="571c7-280">Also, if you leave the web app running, anyone who finds your URL can create and view ads.</span></span> 
>
>

### <a name="delete-your-web-app"></a><span data-ttu-id="571c7-281">Web uygulamanızı Sil</span><span class="sxs-lookup"><span data-stu-id="571c7-281">Delete your web app</span></span>
<span data-ttu-id="571c7-282">Portalda, Git **uygulama hizmetleri** dikey penceresinde, bulun ve web uygulamanızı seçin ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="571c7-282">In the portal, go to the **App Services** blade, locate and select your web app, and then click **Delete**.</span></span> <span data-ttu-id="571c7-283">Yalnızca istiyorsanız geçici olarak başkalarının web uygulaması erişmesini önlemek için tıklatın **durdurmak** yerine.</span><span class="sxs-lookup"><span data-stu-id="571c7-283">If you just want to temporarily prevent others from accessing the web app, click **Stop** instead.</span></span> <span data-ttu-id="571c7-284">Bu durumda ücretler SQL veritabanı ve depolama hesabı için tahakkuk etmeye devam eder.</span><span class="sxs-lookup"><span data-stu-id="571c7-284">In that case, charges will continue to accrue for the SQL Database and Storage account.</span></span>

### <a name="delete-your-storage-account"></a><span data-ttu-id="571c7-285">Depolama hesabınızı silme</span><span class="sxs-lookup"><span data-stu-id="571c7-285">Delete your storage account</span></span>
<span data-ttu-id="571c7-286">Depolama hesabınızı silmek için bkz: [bir depolama hesabını silmek](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="571c7-286">To delete your storage account, see [Delete a storage account](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span></span> 

### <a name="delete-your-database"></a><span data-ttu-id="571c7-287">Veritabanınızı Sil</span><span class="sxs-lookup"><span data-stu-id="571c7-287">Delete your database</span></span>
<span data-ttu-id="571c7-288">SQL veritabanınız silmek için bkz: [Azure SQL Database REST API'sini](https://docs.microsoft.com/rest/api/sql/) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="571c7-288">To delete your SQL database, see the [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) documentation.</span></span>

## <span data-ttu-id="571c7-289"><a id="create"></a>Uygulamayı sıfırdan oluşturma</span><span class="sxs-lookup"><span data-stu-id="571c7-289"><a id="create"></a>Create the application from scratch</span></span>
<span data-ttu-id="571c7-290">Bu bölümde aşağıdaki görevleri gerçekleştirmeniz:</span><span class="sxs-lookup"><span data-stu-id="571c7-290">In this section you'll do the following tasks:</span></span>

* <span data-ttu-id="571c7-291">Visual Studio çözümü ile bir web projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="571c7-291">Create a Visual Studio solution with a web project.</span></span>
* <span data-ttu-id="571c7-292">Veriler için bir sınıf kitaplığı proje ekleyin ön uç ve arka uç arasında paylaşılan erişim katmanı.</span><span class="sxs-lookup"><span data-stu-id="571c7-292">Add a class library project for the data access layer that is shared between the front end and back end.</span></span>
* <span data-ttu-id="571c7-293">Arka uç için bir konsol uygulama projesi etkin Web işleri dağıtımı ile ekleyin.</span><span class="sxs-lookup"><span data-stu-id="571c7-293">Add a Console Application project for the backend, with WebJobs deployment enabled.</span></span>
* <span data-ttu-id="571c7-294">NuGet paketleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="571c7-294">Add NuGet packages.</span></span>
* <span data-ttu-id="571c7-295">Proje başvurularını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="571c7-295">Set project references.</span></span>
* <span data-ttu-id="571c7-296">Öğreticinin önceki bölümde çalıştığınız indirilen uygulama uygulama kodu ve yapılandırma dosyalarını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="571c7-296">Copy application code and configuration files from the downloaded application that you worked with in the previous section of the tutorial.</span></span>
* <span data-ttu-id="571c7-297">Azure BLOB'ları ve kuyrukları ve WebJobs SDK ile çalışan kod bölümlerini gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="571c7-297">Review the parts of the code that work with Azure blobs and queues and the WebJobs SDK.</span></span>

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a><span data-ttu-id="571c7-298">Bir web projesi ve sınıf kitaplığı proje bir Visual Studio çözümü oluşturun</span><span class="sxs-lookup"><span data-stu-id="571c7-298">Create a Visual Studio solution with a web project and class library project</span></span>
1. <span data-ttu-id="571c7-299">Visual Studio'da, **dosya** > **yeni** > **proje**.</span><span class="sxs-lookup"><span data-stu-id="571c7-299">In Visual Studio, choose **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="571c7-300">İçinde **yeni proje** iletişim kutusunda, seçin **Visual C#** > **Web** > **ASP.NET Web uygulaması (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="571c7-300">In the **New Project** dialog, choose **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>
3. <span data-ttu-id="571c7-301">Projeyi ContosoAdsWeb, ad ContosoAdsWebJobsSDK (çözüm adı, onu indirilen çözümü ile aynı klasörde yerleştiriyorsanız değiştirin) çözümü olarak adlandırın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="571c7-301">Name the project ContosoAdsWeb, name the solution ContosoAdsWebJobsSDK (change the solution name if you're putting it in the same folder as the downloaded solution), and then click **OK**.</span></span>

    ![Yeni Proje](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. <span data-ttu-id="571c7-303">İçinde **yeni ASP.NET Web uygulaması** iletişim kutusunda, MVC şablonunu seçin ve Seç **kimlik doğrulamayı Değiştir**.</span><span class="sxs-lookup"><span data-stu-id="571c7-303">In the **New ASP.NET Web Application** dialog, choose the MVC template, and select **Change Authentication**.</span></span>

    ![Kimlik Doğrulamayı Değiştirme](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. <span data-ttu-id="571c7-305">İçinde **kimlik doğrulamayı Değiştir** iletişim kutusunda, seçin **doğrulaması yok**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="571c7-305">In the **Change Authentication** dialog, choose **No Authentication**, and then click **OK**.</span></span>

    ![Kimlik Doğrulaması Yok](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. <span data-ttu-id="571c7-307">İçinde **yeni ASP.NET Web uygulaması** iletişim kutusunda, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="571c7-307">In the **New ASP.NET Web Application** dialog, click **OK**.</span></span>

    <span data-ttu-id="571c7-308">Visual Studio çözümü ve web projesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="571c7-308">Visual Studio creates the solution and the web project.</span></span>
7. <span data-ttu-id="571c7-309">İçinde **Çözüm Gezgini**, çözüme (projeye değil) sağ tıklayın ve seçin **Ekle** > **yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="571c7-309">In **Solution Explorer**, right-click the solution (not the project), and choose **Add** > **New Project**.</span></span>
8. <span data-ttu-id="571c7-310">İçinde **Yeni Proje Ekle** iletişim kutusunda, seçin **Visual C#** > **Windows Klasik Masaüstü** > **sınıf kitaplığı (.NET Framework)**  şablonu.</span><span class="sxs-lookup"><span data-stu-id="571c7-310">In the **Add New Project** dialog, choose **Visual C#** > **Windows Classic Desktop** > **Class Library (.NET Framework)** template.</span></span>  
9. <span data-ttu-id="571c7-311">Projeyi *ContosoAdsCommon* olarak adlandırın ve ardından **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="571c7-311">Name the project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="571c7-312">Bu projenin Entity Framework bağlamına ve ön uç ve arka uç kullanacağı veri modeli içerir.</span><span class="sxs-lookup"><span data-stu-id="571c7-312">This project will contain the Entity Framework context and the data model which both the front end and back end will use.</span></span> <span data-ttu-id="571c7-313">Alternatif olarak, web projesinde EF ile ilgili sınıflar tanımlayın ve Web işi projeden proje başvurusu.</span><span class="sxs-lookup"><span data-stu-id="571c7-313">As an alternative, you could define the EF-related classes in the web project and reference that project from the WebJob project.</span></span> <span data-ttu-id="571c7-314">Ancak, ardından Web işi projeniz gerekli olmayan web derlemelerine başvuru olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="571c7-314">But, then your WebJob project would have a reference to web assemblies, which it doesn't need.</span></span>

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a><span data-ttu-id="571c7-315">Web işleri dağıtımı etkin olan bir konsol uygulama projesi ekleyin</span><span class="sxs-lookup"><span data-stu-id="571c7-315">Add a Console Application project that has WebJobs deployment enabled</span></span>
1. <span data-ttu-id="571c7-316">Web projesi (çözüm veya sınıf kitaplığı proje değil) sağ tıklayın ve ardından **Ekle** > **yeni Azure Web işi projesi**.</span><span class="sxs-lookup"><span data-stu-id="571c7-316">Right-click the web project (not the solution or the class library project), and then click **Add** > **New Azure WebJob Project**.</span></span>

    ![Yeni Azure Web işi projesinin menü seçimi](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. <span data-ttu-id="571c7-318">İçinde **Azure Web işine Ekle** iletişim kutusunda, ContosoAdsWebJob her ikisini birden girin **proje adı** ve **Web işi adı**.</span><span class="sxs-lookup"><span data-stu-id="571c7-318">In the **Add Azure WebJob** dialog, enter ContosoAdsWebJob as both the **Project name** and the **WebJob name**.</span></span> <span data-ttu-id="571c7-319">Bırakın **WebJob çalıştırma modu** kümesine **sürekli olarak çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="571c7-319">Leave **WebJob run mode** set to **Run Continuously**.</span></span>
3. <span data-ttu-id="571c7-320">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="571c7-320">Click **OK**.</span></span>

   <span data-ttu-id="571c7-321">Visual Studio web projesini dağıtma her bir Web işi dağıtmak için yapılandırılmış bir konsol uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="571c7-321">Visual Studio creates a Console application that is configured to deploy as a WebJob whenever you deploy the web project.</span></span> <span data-ttu-id="571c7-322">Bunu yapmak için aşağıdaki görevleri projesi oluşturduktan sonra gerçekleştirilen:</span><span class="sxs-lookup"><span data-stu-id="571c7-322">To do that, it performed the following tasks after creating the project:</span></span>

   * <span data-ttu-id="571c7-323">Eklenen bir *webjob yayımlama settings.json* Web işi projesi özellikleri klasördeki dosya.</span><span class="sxs-lookup"><span data-stu-id="571c7-323">Added a *webjob-publish-settings.json* file in the WebJob project Properties folder.</span></span>
   * <span data-ttu-id="571c7-324">Eklenen bir *webjobs list.json* web projesi özellikleri klasörü dosyasında.</span><span class="sxs-lookup"><span data-stu-id="571c7-324">Added a *webjobs-list.json* file in the web project Properties folder.</span></span>
   * <span data-ttu-id="571c7-325">Web işi projesinin Microsoft.Web.WebJobs.Publish NuGet paketi yüklü.</span><span class="sxs-lookup"><span data-stu-id="571c7-325">Installed the Microsoft.Web.WebJobs.Publish NuGet package in the WebJob project.</span></span>

   <span data-ttu-id="571c7-326">Bu değişiklikler hakkında daha fazla bilgi için bkz: [Visual Studio kullanarak Web işleri dağıtma](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="571c7-326">For more information about these changes, see [How to deploy WebJobs by using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span>

### <a name="add-nuget-packages"></a><span data-ttu-id="571c7-327">NuGet paketleri ekleme</span><span class="sxs-lookup"><span data-stu-id="571c7-327">Add NuGet packages</span></span>
<span data-ttu-id="571c7-328">Bir Web işi projesi için yeni proje şablonu WebJobs SDK NuGet paketini otomatik olarak yükler [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) ve bağımlılıklarını.</span><span class="sxs-lookup"><span data-stu-id="571c7-328">The new-project template for a WebJob project automatically installs the WebJobs SDK NuGet package [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) and its dependencies.</span></span>

<span data-ttu-id="571c7-329">Web işi projesinin otomatik olarak yüklenen Web işleri SDK'si bağımlılıkları Azure Storage istemci kitaplığı (SCL) biridir.</span><span class="sxs-lookup"><span data-stu-id="571c7-329">One of the WebJobs SDK dependencies that is installed automatically in the WebJob project is the Azure Storage Client Library (SCL).</span></span> <span data-ttu-id="571c7-330">Ancak, BLOB'lar ve kuyruklarla çalışmaya web projesine ekleme gerekir.</span><span class="sxs-lookup"><span data-stu-id="571c7-330">However, you need to add it to the web project to work with blobs and queues.</span></span>

1. <span data-ttu-id="571c7-331">Açık **NuGet paketlerini Yönet** çözümü için iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="571c7-331">Open the **Manage NuGet Packages** dialog for the solution.</span></span>
2. <span data-ttu-id="571c7-332">Sol bölmede seçin **yüklü paketleri**.</span><span class="sxs-lookup"><span data-stu-id="571c7-332">In the left pane, select **Installed packages**.</span></span>
3. <span data-ttu-id="571c7-333">Bul *Azure Storage* paketini ve ardından **Yönet**.</span><span class="sxs-lookup"><span data-stu-id="571c7-333">Find the *Azure Storage* package, and then click **Manage**.</span></span>
4. <span data-ttu-id="571c7-334">İçinde **projeleri seçin** kutusunda, seçin **ContosoAdsWeb** onay kutusunu işaretleyin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="571c7-334">In the **Select Projects** box, select the **ContosoAdsWeb** check box, and then click **OK**.</span></span>

    <span data-ttu-id="571c7-335">Üç projenin Entity Framework SQL veritabanındaki verilerle çalışmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="571c7-335">All three projects use the Entity Framework to work with data in SQL Database.</span></span>
5. <span data-ttu-id="571c7-336">Sol bölmede seçin **çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="571c7-336">In the left pane, select **Online**.</span></span>
6. <span data-ttu-id="571c7-337">*EntityFramework* NuGet paketini bulun ve üç projenin tamamına yükleyin.</span><span class="sxs-lookup"><span data-stu-id="571c7-337">Find the *EntityFramework* NuGet package, and install it in all three projects.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="571c7-338">Proje başvurularını ayarlama</span><span class="sxs-lookup"><span data-stu-id="571c7-338">Set project references</span></span>
<span data-ttu-id="571c7-339">Her ikisi de ContosoAdsCommon projesine bir başvuru gerekir böylece hem web hem de Web işi projeleri SQL veritabanı ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="571c7-339">Both web and WebJob projects work with the SQL database, so both need a reference to the ContosoAdsCommon project.</span></span>

1. <span data-ttu-id="571c7-340">ContosoAdsWeb projesinde ContosoAdsCommon projesine bir başvuru ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="571c7-340">In the ContosoAdsWeb project, set a reference to the ContosoAdsCommon project.</span></span> <span data-ttu-id="571c7-341">(ContosoAdsWeb projesine sağ tıklayın ve ardından **Ekle** > **başvuru**.</span><span class="sxs-lookup"><span data-stu-id="571c7-341">(Right-click the ContosoAdsWeb project, and then click **Add** > **Reference**.</span></span> 
2. <span data-ttu-id="571c7-342">İçinde **başvuru Yöneticisi** iletişim kutusunda **projeleri** > **çözüm** > **ContosoAdsCommon**, ve ardından **Tamam**.)</span><span class="sxs-lookup"><span data-stu-id="571c7-342">In the **Reference Manager** dialog box, select **Projects** > **Solution** > **ContosoAdsCommon**, and then click **OK**.)</span></span>
   
    <span data-ttu-id="571c7-343">Web işi projesinin başvuruları görüntülerle çalışma ve bağlantı dizeleri erişmek için gerekir.</span><span class="sxs-lookup"><span data-stu-id="571c7-343">The WebJob project needs references for working with images and for accessing connection strings.</span></span>

4. <span data-ttu-id="571c7-344">Bir başvuru ContosoAdsWebJob projesinde kümesine `System.Drawing` ve `System.Configuration`.</span><span class="sxs-lookup"><span data-stu-id="571c7-344">In the ContosoAdsWebJob project, set a reference to `System.Drawing` and `System.Configuration`.</span></span>

### <a name="add-code-and-configuration-files"></a><span data-ttu-id="571c7-345">Kod ve yapılandırma dosyaları Ekle</span><span class="sxs-lookup"><span data-stu-id="571c7-345">Add code and configuration files</span></span>
<span data-ttu-id="571c7-346">Bu öğretici gösterme nasıl [MVC denetleyicileri ve yapı iskelesi kullanarak görünümleri oluşturma](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), nasıl için [SQL Server veritabanları ile çalışan Entity Framework kod yazma](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), veya [temelleri zaman uyumsuz ASP.NET 4.5 programlama](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="571c7-346">This tutorial does not show how to [create MVC controllers and views using scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), how to [write Entity Framework code that works with SQL Server databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), or [the basics of asynchronous programming in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span> <span data-ttu-id="571c7-347">Bu nedenle, tüm bu yapmak için kalan tek şey indirilen çözümden yeni çözüme kod ve yapılandırma dosyaları kopyala.</span><span class="sxs-lookup"><span data-stu-id="571c7-347">So, all that remains to do is copy code and configuration files from the downloaded solution into the new solution.</span></span> <span data-ttu-id="571c7-348">Bunu sonra aşağıdaki bölümlerde Göster ve kodun temel kısımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="571c7-348">After you do that, the following sections show and explain key parts of the code.</span></span>

<span data-ttu-id="571c7-349">Bir proje veya klasöre dosya eklemek için proje veya klasöre sağ tıklayıp **Ekle** > **Mevcut Öğe** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="571c7-349">To add files to a project or a folder, right-click the project or folder and click **Add** > **Existing Item**.</span></span> <span data-ttu-id="571c7-350">İstediğiniz dosyaları seçin **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="571c7-350">Select the files you want and click **Add**.</span></span> <span data-ttu-id="571c7-351">Mevcut dosyaları değiştirmek isteyip istemediğiniz sorulursa **Evet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="571c7-351">If asked whether you want to replace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="571c7-352">ContosoAdsCommon projesinde silme *Class1.cs* dosya ve onun yerine, indirilen projeden aşağıdaki dosyaları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="571c7-352">In the ContosoAdsCommon project, delete the *Class1.cs* file and add in its place the following files from the downloaded project.</span></span>

   * <span data-ttu-id="571c7-353">*Ad.cs*</span><span class="sxs-lookup"><span data-stu-id="571c7-353">*Ad.cs*</span></span>
   * <span data-ttu-id="571c7-354">*ContosoAdscontext.cs*</span><span class="sxs-lookup"><span data-stu-id="571c7-354">*ContosoAdscontext.cs*</span></span>
   * <span data-ttu-id="571c7-355">*BlobInformation.cs*</span><span class="sxs-lookup"><span data-stu-id="571c7-355">*BlobInformation.cs*</span></span>
2. <span data-ttu-id="571c7-356">ContosoAdsWeb projesinde indirilen projeden aşağıdaki dosyaları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="571c7-356">In the ContosoAdsWeb project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="571c7-357">*Web.config*</span><span class="sxs-lookup"><span data-stu-id="571c7-357">*Web.config*</span></span>
   * <span data-ttu-id="571c7-358">*Global.asax.cs*</span><span class="sxs-lookup"><span data-stu-id="571c7-358">*Global.asax.cs*</span></span>  
   * <span data-ttu-id="571c7-359">İçinde *denetleyicileri* klasörü: *AdController.cs*</span><span class="sxs-lookup"><span data-stu-id="571c7-359">In the *Controllers* folder: *AdController.cs*</span></span>
   * <span data-ttu-id="571c7-360">İçinde *görünümler/paylaşılan* klasörü: *_Layout.cshtml* dosyası</span><span class="sxs-lookup"><span data-stu-id="571c7-360">In the *Views\Shared* folder: *_Layout.cshtml* file</span></span>
   * <span data-ttu-id="571c7-361">İçinde *görünümler* klasörü: *Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="571c7-361">In the *Views\Home* folder: *Index.cshtml*</span></span>
   * <span data-ttu-id="571c7-362">İçinde *görünümler/reklam* klasörü (öncelikle klasörü oluşturun): beş *.cshtml* dosyaları</span><span class="sxs-lookup"><span data-stu-id="571c7-362">In the *Views\Ad* folder (create the folder first): five *.cshtml* files</span></span>
3. <span data-ttu-id="571c7-363">ContosoAdsWebJob projesinde indirilen projeden aşağıdaki dosyaları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="571c7-363">In the ContosoAdsWebJob project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="571c7-364">*App.config* (dosya türü filtresi için değiştirme **tüm dosyaları**)</span><span class="sxs-lookup"><span data-stu-id="571c7-364">*App.config* (change the file type filter to **All Files**)</span></span>
   * <span data-ttu-id="571c7-365">*Program.cs*</span><span class="sxs-lookup"><span data-stu-id="571c7-365">*Program.cs*</span></span>
   * <span data-ttu-id="571c7-366">*Functions.cs*</span><span class="sxs-lookup"><span data-stu-id="571c7-366">*Functions.cs*</span></span>

<span data-ttu-id="571c7-367">Şimdi oluşturmak, çalıştırmak ve öğreticide daha önce belirtildiği gibi uygulamayı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="571c7-367">You can now build, run, and deploy the application as instructed earlier in the tutorial.</span></span> <span data-ttu-id="571c7-368">Ancak, bunu yapmadan önce hala için dağıtılan ilk web uygulamasında çalışan Web işini durdurma.</span><span class="sxs-lookup"><span data-stu-id="571c7-368">Before you do that, however, stop the WebJob that is still running in the first web app you deployed to.</span></span> <span data-ttu-id="571c7-369">Aksi takdirde, bu Web işi sıra iletileri yerel olarak veya tümü aynı depolama hesabı kullanıyorsanız bu yana yeni bir web uygulamasında çalışan uygulama tarafından oluşturulan işler.</span><span class="sxs-lookup"><span data-stu-id="571c7-369">Otherwise, that WebJob will process queue messages created locally or by the app running in a new web app, since all are using the same storage account.</span></span>

## <span data-ttu-id="571c7-370"><a id="code"></a>Uygulama kodu gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="571c7-370"><a id="code"></a>Review the application code</span></span>
<span data-ttu-id="571c7-371">Aşağıdaki bölümlerde Web işleri SDK'si ve Azure Storage blobları ve kuyrukları ile çalışmayla ilgili kod açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="571c7-371">The following sections explain the code related to working with the WebJobs SDK and Azure Storage blobs and queues.</span></span>

> [!NOTE]
> <span data-ttu-id="571c7-372">Web işleri SDK'si belirli kodunu Git [Program.cs ve Functions.cs](#programcs) bölümler.</span><span class="sxs-lookup"><span data-stu-id="571c7-372">For the code specific to the WebJobs SDK, go to the [Program.cs and Functions.cs](#programcs) sections.</span></span>
>
>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="571c7-373">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="571c7-373">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="571c7-374">Ad.cs dosyası reklam kategorileri için bir numaralandırma ve reklam bilgileri için bir POCO varlık sınıfı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="571c7-374">The Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="571c7-375">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="571c7-375">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="571c7-376">ContosoAdsContext sınıfı reklam sınıfının Entity Framework bir SQL veritabanında depolayan bir DbSet koleksiyonunda kullanıldığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="571c7-376">The ContosoAdsContext class specifies that the Ad class is used in a DbSet collection, which Entity Framework stores in a SQL database.</span></span>

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

<span data-ttu-id="571c7-377">Sınıfın iki oluşturucusu vardır.</span><span class="sxs-lookup"><span data-stu-id="571c7-377">The class has two constructors.</span></span> <span data-ttu-id="571c7-378">Birincisi web projesi tarafından kullanılır ve Web.config dosyasını veya Azure çalışma zamanı ortamı saklanan bir bağlantı dizesinin adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="571c7-378">The first is used by the web project, and specifies the name of a connection string that is stored in the Web.config file or the Azure runtime environment.</span></span> <span data-ttu-id="571c7-379">İkinci oluşturucu, gerçek bağlantı dizesine geçmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="571c7-379">The second constructor enables you to pass in the actual connection string.</span></span> <span data-ttu-id="571c7-380">Bir Web.config dosyası olmadığından, Web işi projesi tarafından gereklidir.</span><span class="sxs-lookup"><span data-stu-id="571c7-380">That is needed by the WebJob project since it doesn't have a Web.config file.</span></span> <span data-ttu-id="571c7-381">Bu bağlantı dizesinin nereye depolandığını daha önce gördünüz ve kodun DbContext sınıfını başlattığında bağlantı dizesini nasıl aldığını daha sonra göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="571c7-381">You saw earlier where this connection string was stored, and you'll see later how the code retrieves the connection string when it instantiates the DbContext class.</span></span>

### <a name="contosoadscommon---blobinformationcs"></a><span data-ttu-id="571c7-382">ContosoAdsCommon - BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="571c7-382">ContosoAdsCommon - BlobInformation.cs</span></span>
<span data-ttu-id="571c7-383">`BlobInformation` Sınıfı, bir kuyruk iletisi bir görüntü blob'u hakkında bilgi depolamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="571c7-383">The `BlobInformation` class is used to store information about an image blob in a queue message.</span></span>

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


### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="571c7-384">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="571c7-384">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="571c7-385">`Application_Start` yönteminden çağrılan kod, henüz yoksa bir *görüntüler* blob kapsayıcısı ve bir *görüntüler* kuyruğu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="571c7-385">Code that is called from the `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="571c7-386">Bu, yeni bir depolama hesabı kullanarak başlattığınızda, gerekli blob kapsayıcısının ve kuyruğun otomatik olarak oluşturulmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="571c7-386">This ensures that whenever you start using a new storage account, the required blob container and queue are created automatically.</span></span>

<span data-ttu-id="571c7-387">Depolama bağlantı dizesini kullanarak depolama hesabına erişim izni kodu alır *Web.config* dosya ya da Azure çalışma zamanı ortamı.</span><span class="sxs-lookup"><span data-stu-id="571c7-387">The code gets access to the storage account by using the storage connection string from the *Web.config* file or Azure runtime environment.</span></span>

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

<span data-ttu-id="571c7-388">Ardından, bir başvuru edinir *görüntüleri* blob kapsayıcısı, önceden var olmayan ve erişim izinlerini ve yeni kapsayıcıda ayarlar kapsayıcı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="571c7-388">Then, it gets a reference to the *images* blob container, creates the container if it doesn't already exist, and sets access permissions on the new container.</span></span> <span data-ttu-id="571c7-389">Varsayılan olarak, istemcilerin blob'lara erişmesine yalnızca depolama hesabı kimlik bilgileri ile yeni kapsayıcılar izin verin.</span><span class="sxs-lookup"><span data-stu-id="571c7-389">By default, new containers allow only clients with storage account credentials to access blobs.</span></span> <span data-ttu-id="571c7-390">Web uygulaması BLOB'ları, görüntü BLOB'larını işaret eden URL'leri kullanarak görüntüleri gösterebilmek ortak olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="571c7-390">The web app needs the blobs to be public so that it can display images using URLs that point to the image blobs.</span></span>

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

<span data-ttu-id="571c7-391">Benzer bir kod başvuru edinir *thumbnailrequest* sıraya almak ve yeni bir sıra oluşturur.</span><span class="sxs-lookup"><span data-stu-id="571c7-391">Similar code gets a reference to the *thumbnailrequest* queue and creates a new queue.</span></span> <span data-ttu-id="571c7-392">Bu durumda hiçbir izin değişikliği gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="571c7-392">In this case no permissions change is needed.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="571c7-393">ContosoAdsWeb - _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="571c7-393">ContosoAdsWeb - _Layout.cshtml</span></span>
<span data-ttu-id="571c7-394">*_Layout.cshtml* dosyası üst bilgi ve alt bilgide uygulama adını ayarlar ve bir "Reklamlar" menü girişi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="571c7-394">The *_Layout.cshtml* file sets the app name in the header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="571c7-395">ContosoAdsWeb - Görünümler\Giriş\Dizin.cshtml</span><span class="sxs-lookup"><span data-stu-id="571c7-395">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="571c7-396">*Görünümler\Giriş\Dizin.cshtml* dosyası, giriş sayfasında kategori bağlantılarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="571c7-396">The *Views\Home\Index.cshtml* file displays category links on the home page.</span></span> <span data-ttu-id="571c7-397">Bağlantılar `Category` numaralandırmasının bir sorgu dizesi değişkeni içindeki tamsayı değerini Reklam Dizini sayfasına geçirir.</span><span class="sxs-lookup"><span data-stu-id="571c7-397">The links pass the integer value of the `Category` enum in a querystring variable to the Ads Index page.</span></span>

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="571c7-398">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="571c7-398">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="571c7-399">Oluşturucu, *AdController.cs* dosyasında blob’larla ve kuyruklarla çalışmaya yönelik bir API sağlayan Azure Storage İstemci Kitaplığı nesneleri oluşturmak için `InitializeStorage` yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="571c7-399">In the *AdController.cs* file, the constructor calls the `InitializeStorage` method to create Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="571c7-400">Ardından, kodu bir başvuru alır *görüntüleri* daha önce gördüğünüz gibi blob kapsayıcısı *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="571c7-400">Then, the code gets a reference to the *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="571c7-401">Yaparken, varsayılan ayarlar [yeniden deneme ilkesi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) bir web uygulaması için uygun.</span><span class="sxs-lookup"><span data-stu-id="571c7-401">While doing that, it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="571c7-402">Varsayılan üstel geri alma yeniden deneme ilkesi, web uygulamasını geçici bir hata için tekrarlanan yeniden denemelerde bir dakikadan uzun süre askıya alabilir.</span><span class="sxs-lookup"><span data-stu-id="571c7-402">The default exponential backoff retry policy could hang the web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="571c7-403">Burada belirtilen yeniden deneme ilkesi üç denemeye kadar her denemeden sonra en fazla üç saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="571c7-403">The retry policy specified here waits three seconds after each try for up to three tries.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

<span data-ttu-id="571c7-404">Benzer bir kod, *görüntüler* kuyruğuna başvuru edinir.</span><span class="sxs-lookup"><span data-stu-id="571c7-404">Similar code gets a reference to the *images* queue.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

<span data-ttu-id="571c7-405">Denetleyici kodlarının birçoğu bir DbContext sınıfı kullanarak Entity Framework veri modeli ile çalışmak için tipiktir.</span><span class="sxs-lookup"><span data-stu-id="571c7-405">Most of the controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="571c7-406">Dosyayı karşıya yükleyen ve blob depolama alanına kaydeden HttpPost `Create` yöntemi bunun bir istisnasıdır.</span><span class="sxs-lookup"><span data-stu-id="571c7-406">An exception is the HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="571c7-407">Model bağlayıcı, yönteme bir [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) nesnesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="571c7-407">The model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object to the method.</span></span>

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

<span data-ttu-id="571c7-408">Kullanıcı karşıya yüklemek için bir dosya seçtiyse kod bu dosyayı karşıya yükler, bir blob'a kaydeder ve Ad veritabanı kaydını blob’a işaret eden bir URL ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="571c7-408">If the user selected a file to upload, the code uploads the file, saves it in a blob, and updates the Ad database record with a URL that points to the blob.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

<span data-ttu-id="571c7-409">Karşıya yüklemeyi yapan kod `UploadAndSaveBlobAsync` yöntemindedir.</span><span class="sxs-lookup"><span data-stu-id="571c7-409">The code that does the upload is in the `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="571c7-410">Blob için bir GUID adı oluşturur, dosyayı karşıya yükler ve kaydeder ve kaydedilmiş blob için bir başvuru döndürür.</span><span class="sxs-lookup"><span data-stu-id="571c7-410">It creates a GUID name for the blob, uploads and saves the file, and returns a reference to the saved blob.</span></span>

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

<span data-ttu-id="571c7-411">HttpPost sonra `Create` yöntemi bir blob'u karşıya yükleyip veritabanını güncelleştirir, görüntüyü bir küçük resim dönüştürme için hazır olduğunu arka uç işlemine bildirmek üzere bir kuyruk iletisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="571c7-411">After the HttpPost `Create` method uploads a blob and updates the database, it creates a queue message to inform the back-end process that an image is ready for conversion to a thumbnail.</span></span>

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

<span data-ttu-id="571c7-412">HttpPost kodunu `Edit` yöntemi olduğunu benzer, kullanıcı yeni bir görüntü dosyası belirlerse, bu ad zaten mevcut BLOB silinmelidir dışında.</span><span class="sxs-lookup"><span data-stu-id="571c7-412">The code for the HttpPost `Edit` method is similar, except that if the user selects a new image file, any blobs that already exist for this ad must be deleted.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

<span data-ttu-id="571c7-413">Bir ad sildiğinizde, BLOB'ları silen kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="571c7-413">Here is the code that deletes blobs when you delete an ad:</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="571c7-414">ContosoAdsWeb - Views\Ad\Index.cshtml ve Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="571c7-414">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="571c7-415">*Index.cshtml* dosyası küçük resimleri diğer reklam verileriyle birlikte gösterir:</span><span class="sxs-lookup"><span data-stu-id="571c7-415">The *Index.cshtml* file displays thumbnails with the other ad data:</span></span>

        <img  src="@Html.Raw(item.ThumbnailURL)" />

<span data-ttu-id="571c7-416">*Details.cshtml* dosyası tam boyutlu görüntüyü gösterir:</span><span class="sxs-lookup"><span data-stu-id="571c7-416">The *Details.cshtml* file displays the full-size image:</span></span>

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="571c7-417">ContosoAdsWeb - Views\Ad\Create.cshtml ve Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="571c7-417">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="571c7-418">*Create.cshtml* ve *Edit.cshtml* dosyaları denetleyicinin `HttpPostedFileBase` nesnesi almasını sağlayan form kodlamasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="571c7-418">The *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables the controller to get the `HttpPostedFileBase` object.</span></span>

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

<span data-ttu-id="571c7-419">Bir `<input>` öğesi tarayıcıya bir dosya seçme iletişim kutusu açmasını söyler.</span><span class="sxs-lookup"><span data-stu-id="571c7-419">An `<input>` element tells the browser to provide a file selection dialog.</span></span>

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <span data-ttu-id="571c7-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span><span class="sxs-lookup"><span data-stu-id="571c7-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span></span>
<span data-ttu-id="571c7-421">Web işi başladığında, `Main` yöntemini çağırır WebJobs SDK `JobHost.RunAndBlock` yürütülmesi başlamaya yöntemi tetiklenen geçerli iş parçacığının işlevleri.</span><span class="sxs-lookup"><span data-stu-id="571c7-421">When the WebJob starts, the `Main` method calls the WebJobs SDK `JobHost.RunAndBlock` method to begin execution of triggered functions on the current thread.</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <span data-ttu-id="571c7-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail yöntemi</span><span class="sxs-lookup"><span data-stu-id="571c7-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail method</span></span>
<span data-ttu-id="571c7-423">Bir kuyruk iletisi alındığında WebJobs SDK bu yöntemi çağırır.</span><span class="sxs-lookup"><span data-stu-id="571c7-423">The WebJobs SDK calls this method when a queue message is received.</span></span> <span data-ttu-id="571c7-424">Yöntem bir küçük resim oluşturur ve küçük resim koyar veritabanındaki URL.</span><span class="sxs-lookup"><span data-stu-id="571c7-424">The method creates a thumbnail and puts the thumbnail URL in the database.</span></span>

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
            // be instantiated and disposed within the function.
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

* <span data-ttu-id="571c7-425">`QueueTrigger` Özniteliği thumbnailrequest sıranın üzerinde yeni bir ileti alındığında bu yöntemi çağırmak için Web işleri SDK'si yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="571c7-425">The `QueueTrigger` attribute directs the WebJobs SDK to call this method when a new message is received on the thumbnailrequest queue.</span></span>

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    <span data-ttu-id="571c7-426">`BlobInformation` Kuyruk iletisini nesnedir içine otomatik olarak Serisi kaldırılan `blobInfo` parametresi.</span><span class="sxs-lookup"><span data-stu-id="571c7-426">The `BlobInformation` object in the queue message is automatically deserialized into the `blobInfo` parameter.</span></span> <span data-ttu-id="571c7-427">Kuyruk iletisini yöntemi tamamlandığında silinir.</span><span class="sxs-lookup"><span data-stu-id="571c7-427">When the method completes, the queue message is deleted.</span></span> <span data-ttu-id="571c7-428">Yöntem tamamlanmadan önce başarısız olursa, kuyruk iletisini silinmez; 10 dakikalık kiralama süresi dolduktan sonra yeniden çekilmesi için yayımlanan ve işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="571c7-428">If the method fails before completing, the queue message is not deleted; after a 10-minute lease expires, the message is released to be picked up again and processed.</span></span> <span data-ttu-id="571c7-429">Bir ileti her zaman bir özel durum neden olursa bu sırası süresiz olarak yinelenen olmaz.</span><span class="sxs-lookup"><span data-stu-id="571c7-429">This sequence won't be repeated indefinitely if a message always causes an exception.</span></span> <span data-ttu-id="571c7-430">Bir iletiyi işlemek 5 başarısız denemeden sonra {queuename} adlı bir sıraya ileti taşınır-zararlı.</span><span class="sxs-lookup"><span data-stu-id="571c7-430">After 5 unsuccessful attempts to process a message, the message is moved to a queue named {queuename}-poison.</span></span> <span data-ttu-id="571c7-431">En fazla denemesi sayısı yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="571c7-431">The maximum number of attempts is configurable.</span></span>
* <span data-ttu-id="571c7-432">İki `Blob` öznitelikler BLOB'lar için bağlı olan nesneleri sağlar: biri mevcut görüntü blob'u, yöntem oluşturur Yeni bir küçük resim blob birine.</span><span class="sxs-lookup"><span data-stu-id="571c7-432">The two `Blob` attributes provide objects that are bound to blobs: one to the existing image blob and one to a new thumbnail blob that the method creates.</span></span>

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    <span data-ttu-id="571c7-433">BLOB adları gelen özelliklerinden `BlobInformation` kuyruk iletisini alınan nesne (`BlobName` ve `BlobNameWithoutExtension`).</span><span class="sxs-lookup"><span data-stu-id="571c7-433">Blob names come from properties of the `BlobInformation` object received in the queue message (`BlobName` and `BlobNameWithoutExtension`).</span></span> <span data-ttu-id="571c7-434">Depolama istemcisi kitaplığı tam işlevselliğini almak için kullanabileceğiniz `CloudBlockBlob` BLOB'lar ile çalışmak için sınıf.</span><span class="sxs-lookup"><span data-stu-id="571c7-434">To get the full functionality of the Storage Client Library, you can use the `CloudBlockBlob` class to work with blobs.</span></span> <span data-ttu-id="571c7-435">Çalışmak için yazılmış kodun yeniden isteyip istemediğinizi `Stream` nesneleri kullanabileceğiniz `Stream` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="571c7-435">If you want to reuse code that was written to work with `Stream` objects, you can use the `Stream` class.</span></span>

<span data-ttu-id="571c7-436">Web işleri SDK'si öznitelikleri kullanan işlevler yazma hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="571c7-436">For more information about how to write functions that use  WebJobs SDK attributes, see the following resources:</span></span>

* [<span data-ttu-id="571c7-437">Web İşleri SDK’sı ile Azure kuyruk depolama kullanımı</span><span class="sxs-lookup"><span data-stu-id="571c7-437">How to use Azure queue storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [<span data-ttu-id="571c7-438">Web İşleri SDK’sı ile Azure blob depolama kullanımı</span><span class="sxs-lookup"><span data-stu-id="571c7-438">How to use Azure blob storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [<span data-ttu-id="571c7-439">Web İşleri SDK’sı ile Azure tablo depolama kullanımı</span><span class="sxs-lookup"><span data-stu-id="571c7-439">How to use Azure table storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [<span data-ttu-id="571c7-440">Web İşleri SDK’sı ile Azure Service Bus kullanımı</span><span class="sxs-lookup"><span data-stu-id="571c7-440">How to use Azure Service Bus with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * <span data-ttu-id="571c7-441">Web uygulamanız birden çok sanal makine çalışıyorsa, birden çok Web işleri eşzamanlı çalışan ve bazı senaryolarda bu birden çok kez işlenen aynı veri kaybına neden.</span><span class="sxs-lookup"><span data-stu-id="571c7-441">If your web app runs on multiple VMs, multiple WebJobs will be running simultaneously, and in some scenarios this can result in the same data getting processed multiple times.</span></span> <span data-ttu-id="571c7-442">Yerleşik sırası, blob ve Service Bus Tetikleyicileri kullanırsanız, bir sorun değildir.</span><span class="sxs-lookup"><span data-stu-id="571c7-442">This is not a problem if you use the built-in queue, blob, and Service Bus triggers.</span></span> <span data-ttu-id="571c7-443">SDK işlevlerinizi yalnızca bir kez her ileti veya blob işleneceğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="571c7-443">The SDK ensures that your functions will be processed only once for each message or blob.</span></span>
> * <span data-ttu-id="571c7-444">Normal şekilde kapatılmasını uygulama hakkında daha fazla bilgi için bkz: [kapama](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span><span class="sxs-lookup"><span data-stu-id="571c7-444">For information about how to implement graceful shutdown, see [Graceful Shutdown](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span></span>
> * <span data-ttu-id="571c7-445">Kodda `ConvertImageToThumbnailJPG` (gösterilmez) yöntemini kullanır sınıflarda `System.Drawing` kolaylık olması için ad alanı.</span><span class="sxs-lookup"><span data-stu-id="571c7-445">The code in the `ConvertImageToThumbnailJPG` method (not shown) uses classes in the `System.Drawing` namespace for simplicity.</span></span> <span data-ttu-id="571c7-446">Ancak, bu ad alanındaki sınıflar Windows Forms ile kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="571c7-446">However, the classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="571c7-447">Bir Windows veya ASP.NET hizmetinde kullanılması desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="571c7-447">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="571c7-448">Görüntü işleme seçenekleri hakkında daha fazla bilgi için bkz. [Dinamik Görüntü Oluşturma](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) ve [Görüntü Yeniden Boyutlandırmaya Ayrıntılı Bakış](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span><span class="sxs-lookup"><span data-stu-id="571c7-448">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="571c7-449">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="571c7-449">Next steps</span></span>
<span data-ttu-id="571c7-450">Bu öğreticide, arka uç işleme için Web işleri SDK'si kullanan basit bir çok katmanlı uygulama gördünüz.</span><span class="sxs-lookup"><span data-stu-id="571c7-450">In this tutorial, you've seen a simple multi-tier application that uses the WebJobs SDK for backend processing.</span></span> <span data-ttu-id="571c7-451">Bu bölümde, ASP.NET çok katmanlı uygulamaları ve Web işleri hakkında daha fazla bilgi edinmek için bazı öneriler sunar.</span><span class="sxs-lookup"><span data-stu-id="571c7-451">This section offers some suggestions for learning more about ASP.NET multi-tier applications and WebJobs.</span></span>

### <a name="missing-features"></a><span data-ttu-id="571c7-452">Eksik Özellikler</span><span class="sxs-lookup"><span data-stu-id="571c7-452">Missing features</span></span>
<span data-ttu-id="571c7-453">Uygulama bir başlangıç öğreticisi için basit tutulmuştur.</span><span class="sxs-lookup"><span data-stu-id="571c7-453">The application has been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="571c7-454">Gerçek dünya uygulamada uygulamak [bağımlılık ekleme](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) ve [depo ve iş birimi düzenleri](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), kullanın [günlüğe kaydetme için bir arabirimi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), kullanmak[EF Code First geçişleri](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) veri modeli değişikliklerini yönetmek ve kullanmak için [EF bağlantı dayanıklılığı](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) geçici ağ hatalarını yönetmek için.</span><span class="sxs-lookup"><span data-stu-id="571c7-454">In a real-world application you would implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) and the [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) to manage data model changes, and use [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) to manage transient network errors.</span></span>

### <a name="scaling-webjobs"></a><span data-ttu-id="571c7-455">Web işleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="571c7-455">Scaling WebJobs</span></span>
<span data-ttu-id="571c7-456">Web işleri bir web uygulaması bağlamında çalışır ve ayrı olarak ölçeklenebilir değildir.</span><span class="sxs-lookup"><span data-stu-id="571c7-456">WebJobs run in the context of a web app and are not scalable separately.</span></span> <span data-ttu-id="571c7-457">Örneğin, bir standart web app örneği varsa, çalışan, arka plan işlemi yalnızca bir örneğine sahip ve bazı Aksi durumda web içerik sunmak kullanılabilir olacak sunucu kaynaklarının (CPU, bellek, vb.) kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="571c7-457">For example, if you have one Standard web app instance, you have only one instance of your background process running, and it is using some of the server resources (CPU, memory, etc.) that otherwise would be available to serve web content.</span></span>

<span data-ttu-id="571c7-458">Trafik gün veya haftanın günü zamanına göre değişir ve arka uç işleme bekleyebilirsiniz ihtiyacınız varsa, Webjob'larınızı trafiği düşük zamanlarda çalışmak üzere zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="571c7-458">If traffic varies by time of day or day of week, and if the backend processing you need to do can wait, you could schedule your WebJobs to run at low-traffic times.</span></span> <span data-ttu-id="571c7-459">Yük hala Bu çözüm için çok yüksekse, arka uç adanmış bir ayrı bir web uygulamasında Web işi olarak bu amaçla çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="571c7-459">If the load is still too high for that solution, you can run the backend as a WebJob in a separate web app dedicated for that purpose.</span></span> <span data-ttu-id="571c7-460">Arka uç web uygulamanızı sonra bağımsız olarak ve ön uç web uygulamanızdan ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="571c7-460">You can then scale your backend web app independently from your frontend web app.</span></span>

<span data-ttu-id="571c7-461">Daha fazla bilgi için bkz: [ölçeklendirme WebJobs](websites-webjobs-resources.md#scale).</span><span class="sxs-lookup"><span data-stu-id="571c7-461">For more information, see [Scaling WebJobs](websites-webjobs-resources.md#scale).</span></span>

### <a name="avoiding-web-app-timeout-shut-downs"></a><span data-ttu-id="571c7-462">Web uygulaması zaman aşımı kapatma listeleri önleme</span><span class="sxs-lookup"><span data-stu-id="571c7-462">Avoiding web app timeout shut-downs</span></span>
<span data-ttu-id="571c7-463">Webjob'larınızı her zaman çalıştırıyorsanız ve etkinleştirmek zorunda web uygulamanız tüm örneklerini çalıştıran, emin olmak için [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) özelliği.</span><span class="sxs-lookup"><span data-stu-id="571c7-463">To make sure your WebJobs are always running, and running on all instances of your web app, you have to enable the [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) feature.</span></span>

### <a name="using-the-webjobs-sdk-outside-of-webjobs"></a><span data-ttu-id="571c7-464">Web işleri dışında WebJobs SDK'sını kullanarak</span><span class="sxs-lookup"><span data-stu-id="571c7-464">Using the WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="571c7-465">WebJobs SDK kullanan bir program, bir Web işi olarak azure'da çalıştırmak sahip değil.</span><span class="sxs-lookup"><span data-stu-id="571c7-465">A program that uses the WebJobs SDK doesn't have to run in Azure in a WebJob.</span></span> <span data-ttu-id="571c7-466">Yerel olarak çalıştırabilir ve bulut hizmeti çalışan rolü veya bir Windows hizmeti gibi diğer ortamlarda da çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="571c7-466">It can run locally, and it can also run in other environments such as a Cloud Service worker role or a Windows service.</span></span> <span data-ttu-id="571c7-467">Ancak, Web işleri SDK'si Panosu yalnızca Azure web uygulaması erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="571c7-467">However, you can only access the WebJobs SDK dashboard through an Azure web app.</span></span> <span data-ttu-id="571c7-468">Web uygulaması üzerinde AzureWebJobsDashboard bağlantı dizesi ayarlayarak kullandığınız depolama hesabı bağlanmak zorunda panoyu kullanmak için **yapılandırma** sekmesini Klasik portalı.</span><span class="sxs-lookup"><span data-stu-id="571c7-468">To use the dashboard you have to connect the web app to the storage account you're using by setting the AzureWebJobsDashboard connection string on the **Configure** tab of the classic portal.</span></span> <span data-ttu-id="571c7-469">Ardından, aşağıdaki URL'yi kullanarak panoya elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="571c7-469">Then, you can get to the Dashboard by using the following URL:</span></span>

<span data-ttu-id="571c7-470">https://{webappname}.SCM.azurewebsites.NET/azurejobs/#/Functions</span><span class="sxs-lookup"><span data-stu-id="571c7-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span></span>

<span data-ttu-id="571c7-471">Daha fazla bilgi için bkz: [WebJobs SDK ile yerel geliştirme için bir Pano alma](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), ancak eski bir bağlantı dizesi adı gösterdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="571c7-471">For more information, see [Getting a dashboard for local development with the WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that it shows an old connection string name.</span></span>

### <a name="more-webjobs-documentation"></a><span data-ttu-id="571c7-472">Daha fazla Web işleri belgeleri</span><span class="sxs-lookup"><span data-stu-id="571c7-472">More WebJobs documentation</span></span>
<span data-ttu-id="571c7-473">Daha fazla bilgi için bkz: [Azure Web işleri belge kaynakları](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="571c7-473">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span>
