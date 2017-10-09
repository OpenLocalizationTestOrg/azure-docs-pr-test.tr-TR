---
title: "aaaFlask ve Visual Studio için Python araçları 2.2 ile azure'da Azure tablo depolaması"
description: "Nasıl toouse hello Python araçları için Visual Studio toocreate verileri Azure tablo depolama alanında depolar Flask web uygulaması öğrenin ve tooAzure App Service Web Apps dağıtın."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: d8e70a29-aca1-4010-95f5-cfe769e3be06
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1a09d4cc78078a00492ba4fe7e2075df96fb0380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="flask-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="b7d9d-103">Flask ve Visual Studio için Python araçları 2.2 ile azure'da Azure tablo depolaması</span><span class="sxs-lookup"><span data-stu-id="b7d9d-103">Flask and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="b7d9d-104">Bu öğreticide, kullanacağız [Visual Studio için Python Araçları] toocreate basit bir web uygulamasına hello PTVS örnek şablonlarından birini kullanarak yoklar.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="b7d9d-105">Bu öğretici olarak da kullanılabilir bir [video](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span><span class="sxs-lookup"><span data-stu-id="b7d9d-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span></span>

<span data-ttu-id="b7d9d-106">depoları (bellek içi, Azure Table Storage, MongoDB) farklı türleri arasında kolayca geçebilirsiniz şekilde hello yoklamalar web uygulaması, havuz için bir Özet tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-106">hello polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="b7d9d-107">Biz nasıl toocreate bir Azure depolama hesabı, tooconfigure hello nasıl web uygulama toouse Azure tablo depolaması ve nasıl öğreneceksiniz toopublish hello web uygulaması çok[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="b7d9d-107">We'll learn how toocreate an Azure Storage account, how tooconfigure hello web app toouse Azure Table Storage, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="b7d9d-108">Merhaba bkz [Python Geliştirici Merkezi] Bottle kullanarak PTVS ile Azure App Service Web Apps geliştirmeyi kapsayan diğer makaleler için Flask ve Django web altyapılarını MongoDB, Azure Table Storage, MySQL ve SQL Database hizmetleriyle.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="b7d9d-109">Bu makale App Service'e odaklanmakla birlikte hello adımlar geliştirirken benzer [Azure Cloud Services].</span><span class="sxs-lookup"><span data-stu-id="b7d9d-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7d9d-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b7d9d-110">Prerequisites</span></span>
* <span data-ttu-id="b7d9d-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="b7d9d-111">Visual Studio 2015</span></span>
* <span data-ttu-id="b7d9d-112">[Visual Studio için Python Araçları 2.2]</span><span class="sxs-lookup"><span data-stu-id="b7d9d-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="b7d9d-113">[Visual Studio Örnekleri VSIX için Python araçları 2.2]</span><span class="sxs-lookup"><span data-stu-id="b7d9d-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="b7d9d-114">[VS 2015 için Azure SDK Araçları]</span><span class="sxs-lookup"><span data-stu-id="b7d9d-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="b7d9d-115">[Python 2.7 32 bit] veya [Python 3.4 32 bit]</span><span class="sxs-lookup"><span data-stu-id="b7d9d-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="b7d9d-116">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b7d9d-117">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="b7d9d-118">Başlangıç projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b7d9d-118">Create hello Project</span></span>
<span data-ttu-id="b7d9d-119">Bu bölümde, örnek şablonu kullanarak bir Visual Studio projesi oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="b7d9d-120">Biz sanal ortam oluşturacak ve gerekli paketleri yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="b7d9d-121">Ardından biz hello uygulaması hello varsayılan bellek içi depoya kullanarak yerel olarak çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-121">Then we'll run hello application locally using hello default in-memory repository.</span></span>

1. <span data-ttu-id="b7d9d-122">Visual Studio'da, **Dosya**, **Yeni Proje**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="b7d9d-123">Proje şablonlarını hello hello [Visual Studio Örnekleri VSIX için Python araçları 2.2] altında kullanılabilir **Python**, **örnekleri**.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-123">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="b7d9d-124">Seçin **yoklamalar Flask Web projesi** ve Tamam toocreate hello proje'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-124">Select **Polls Flask Web Project** and click OK toocreate hello project.</span></span>
   
     ![Yeni Proje İletişim Kutusu](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskNewProject.png)
3. <span data-ttu-id="b7d9d-126">İstendiğinde tooinstall dış paketler olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-126">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="b7d9d-127">**Sanal bir ortama yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-127">Select **Install into a virtual environment**.</span></span>
   
     ![Dış Paketler İletişim Kutusu](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskExternalPackages.png)
4. <span data-ttu-id="b7d9d-129">Seçin **Python 2.7** veya **Python 3.4** hello temel yorumlayıcı olarak.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-129">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
     ![Sanal Ortama Ekle İletişim Kutusu](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="b7d9d-131">Merhaba uygulaması tuşlarına basarak çalıştığını onaylayın `F5`.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-131">Confirm that hello application works by pressing `F5`.</span></span> <span data-ttu-id="b7d9d-132">Varsayılan olarak, herhangi bir yapılandırma gerektirmeyen bir bellek içi depoya hello uygulama kullanır.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-132">By default, hello application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="b7d9d-133">Tüm veriler kaybolur hello web sunucusu durdurulduğunda.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-133">All data is lost when hello web server is stopped.</span></span>
6. <span data-ttu-id="b7d9d-134">Tıklatın **örnek yoklamalar Oluştur**, ardından bir yoklamaya tıklayın ve oy verin.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Web Tarayıcısı](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="b7d9d-136">Bir Azure depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b7d9d-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="b7d9d-137">toouse depolama işlemleri, bir Azure depolama hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-137">toouse storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="b7d9d-138">Aşağıdaki adımları izleyerek bir depolama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="b7d9d-139">Merhaba günlüğüne [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b7d9d-139">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b7d9d-140">Merhaba tıklatın **yeni** hello üst simgesine sol hello Portal ', ardından **veri + depolama** > **depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-140">Click hello **New** icon on hello top left of hello Portal, then click **Data + Storage** > **Storage Account**.</span></span> <span data-ttu-id="b7d9d-141">Tıklayın **oluşturma**, ardından hello depolama hesabı benzersiz bir ad verin ve yeni bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) onun için.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-141">Click on **Create**, then give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Hızlı oluştur](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="b7d9d-143">Merhaba depolama hesabı oluşturduğunuzda hello **bildirimleri** düğmesi yeşil flash **başarı** ve hello depolama hesabının dikey penceresi açık toohello yeni kaynak ait tooshow grubunu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-143">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="b7d9d-144">Merhaba tıklatın **erişim tuşları** hello depolama hesabı dikey penceresinde parçası.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-144">Click hello **Access Keys** part in hello storage account's blade.</span></span> <span data-ttu-id="b7d9d-145">Merhaba hesap adı ve hello key1 not edin.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-145">Take note of hello account name and hello key1.</span></span>
   
      ![Anahtarlar](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="b7d9d-147">Biz bu bilgileri tooconfigure hello sonraki bölümde projenizde gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-147">We will need this information tooconfigure your project in hello next section.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="b7d9d-148">Merhaba projeyi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b7d9d-148">Configure hello Project</span></span>
<span data-ttu-id="b7d9d-149">Bu bölümde, yeni oluşturduğumuz bizim uygulama toouse hello depolama hesabı yapılandıracağız.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-149">In this section, we'll configure our application toouse hello storage account we just created.</span></span> <span data-ttu-id="b7d9d-150">Azure Portal tooobtain bağlantı ayarlarını nasıl hello göreceğiz.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-150">We'll see how tooobtain connection settings from hello Azure Portal.</span></span> <span data-ttu-id="b7d9d-151">Ardından hello uygulama yerel olarak çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-151">Then we'll run hello application locally.</span></span>

1. <span data-ttu-id="b7d9d-152">Visual Studio'da, Çözüm Gezgini'nde, proje düğümüne sağ tıklayın ve seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-152">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="b7d9d-153">Tıklatın hello üzerinde **hata ayıklama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-153">Click on hello **Debug** tab.</span></span>
   
     ![Proje hata ayıklama ayarları](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="b7d9d-155">Merhaba değerlerini hello uygulamada gerekli ortam değişkenleri **Debug sunucu komutunu**, **ortam**.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-155">Set hello values of environment variables required by hello application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="b7d9d-156">Bu hello ortam değişkenleri ayarlar olduğunda, **hata ayıklamayı Başlat**.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-156">This will set hello environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="b7d9d-157">İsterseniz hello değişkenleri toobe ne zaman ayarlayın, **hata ayıklama olmadan Başlat**, aynı değerleri kümesi hello **sunucu komutu Çalıştır** de.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-157">If you want hello variables toobe set when you **Start Without Debugging**, set hello same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="b7d9d-158">Alternatif olarak, Windows Denetim Masası hello kullanarak ortam değişkenlerini tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-158">Alternatively, you can define environment variables using hello Windows Control Panel.</span></span> <span data-ttu-id="b7d9d-159">Kaynak kodunda kimlik bilgilerini depolama tooavoid istediğiniz / proje dosyası, daha iyi bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-159">This is a better option if you want tooavoid storing credentials in source code / project file.</span></span> <span data-ttu-id="b7d9d-160">Merhaba yeni ortam değerleri toobe kullanılabilir toohello uygulaması için Visual Studio toorestart gerektiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-160">Note that you will need toorestart Visual Studio for hello new environment values toobe available toohello application.</span></span>
3. <span data-ttu-id="b7d9d-161">hello Azure Table Storage deposu uygulayan hello kodudur içinde **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-161">hello code that implements hello Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="b7d9d-162">Merhaba bkz [belgelerine] hakkında daha fazla bilgi için toouse Python tablo hizmetinden.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-162">See hello [documentation] for more information on how toouse Table Service from Python.</span></span>
4. <span data-ttu-id="b7d9d-163">Merhaba uygulamayla çalıştırmak `F5`.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-163">Run hello application with `F5`.</span></span> <span data-ttu-id="b7d9d-164">İle oluşturulan yoklamalar **örnek yoklamalar Oluştur** ve oy vermeyle gönderilen hello veri Azure tablo Depolama'da seri.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-164">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b7d9d-165">Merhaba Python 2.7 sanal ortamı Visual Studio'da bir özel durum sonu neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-165">hello Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="b7d9d-166">Tuşuna `F5` toocontinue hello web projesi yükleniyor.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-166">Press `F5` toocontinue loading hello web project.</span></span>
   > 
   > 
5. <span data-ttu-id="b7d9d-167">Toohello Gözat **hakkında** uygulama hello sayfa tooverify hello kullanarak **Azure Table Storage** deposu.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-167">Browse toohello **About** page tooverify that hello application is using hello **Azure Table Storage** repository.</span></span>
   
     ![Web Tarayıcısı](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a><span data-ttu-id="b7d9d-169">Hello Azure Table Storage keşfedin</span><span class="sxs-lookup"><span data-stu-id="b7d9d-169">Explore hello Azure Table Storage</span></span>
<span data-ttu-id="b7d9d-170">Bu kolay tooview ve Visual Studio Cloud Explorer kullanarak depolama tabloları düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-170">It's easy tooview and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="b7d9d-171">Bu bölümde Sunucu Gezgini tooview hello hello yoklamalar uygulama tabloların içeriğini kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-171">In this section we'll use Server Explorer tooview hello contents of hello polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="b7d9d-172">Bu, kullanılabilir olan yüklü Microsoft Azure Araçları toobe gerektirir hello bir parçası olarak [.NET için Azure SDK].</span><span class="sxs-lookup"><span data-stu-id="b7d9d-172">This requires Microsoft Azure Tools toobe installed, which are available as part of hello [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="b7d9d-173">Açık **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-173">Open **Cloud Explorer**.</span></span> <span data-ttu-id="b7d9d-174">Genişletme **depolama hesapları**, depolama hesabınızın sonra **tabloları**.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-174">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Bulut Gezgini](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="b7d9d-176">Merhaba üzerinde çift **yoklamalar** veya **seçenekleri** tablo tooview hello Ekle/Kaldır/Düzenle varlıklar yanı sıra, bir belge penceresinde hello tablosunun içeriğini.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-176">Double-click on hello **polls** or **choices** table tooview hello contents of hello table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![Tablo sorgusu sonuçları](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="b7d9d-178">Yayımlama Hello web uygulama tooAzure uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="b7d9d-178">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="b7d9d-179">Hello Azure .NET SDK'sını kolay bir yolu toodeploy web uygulama tooAzure uygulama hizmeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-179">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="b7d9d-180">İçinde **Çözüm Gezgini**, hello proje düğümüne sağ tıklayın ve seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-180">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
     ![Web Yayımlama İletişim Kutusu](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="b7d9d-182">**Microsoft Azure Web Apps** ’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="b7d9d-183">Tıklayın **yeni** toocreate yeni bir web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-183">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="b7d9d-184">Hello aşağıdaki alanları doldurun ve **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-184">Fill in hello following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="b7d9d-185">**Web Uygulaması adı**</span><span class="sxs-lookup"><span data-stu-id="b7d9d-185">**Web App name**</span></span>
   * <span data-ttu-id="b7d9d-186">**App Service planı**</span><span class="sxs-lookup"><span data-stu-id="b7d9d-186">**App Service plan**</span></span>
   * <span data-ttu-id="b7d9d-187">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="b7d9d-187">**Resource group**</span></span>
   * <span data-ttu-id="b7d9d-188">**Bölge**</span><span class="sxs-lookup"><span data-stu-id="b7d9d-188">**Region**</span></span>
   * <span data-ttu-id="b7d9d-189">Bırakın **veritabanı sunucusu** çok ayarlamak**veritabanı yok**</span><span class="sxs-lookup"><span data-stu-id="b7d9d-189">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="b7d9d-190">Diğer tüm varsayılanları kabul edin ve **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="b7d9d-191">Web tarayıcınız toohello yayımlanan web uygulamasına otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-191">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="b7d9d-192">Sayfa hakkında toohello göz atarsanız, hello kullandığını görürsünüz **bellek içi** deposu, değil hello **Azure Table Storage** deposu.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-192">If you browse toohello about page, you'll see that it uses hello **In-Memory** repository, not hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="b7d9d-193">Merhaba ortam değişkenleri hello Azure App Service'te Web Apps örneğinde ayarlanmamış belirtilen hello varsayılan değerleri kullanan çünkü **ProjectName**.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-193">That's because hello environment variables are not set on hello Web Apps instance in Azure App Service, so it uses hello default values specified in **settings.py**.</span></span>

## <a name="configure-hello-web-apps-instance"></a><span data-ttu-id="b7d9d-194">Merhaba Web uygulamaları örnek yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b7d9d-194">Configure hello Web Apps instance</span></span>
<span data-ttu-id="b7d9d-195">Bu bölümde, hello Web Apps örneği için ortam değişkenleri yapılandıracağız.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-195">In this section, we'll configure environment variables for hello Web Apps instance.</span></span>

1. <span data-ttu-id="b7d9d-196">İçinde [Azure Portal](https://portal.azure.com), tıklayarak hello web uygulamanızın dikey penceresini açmak **Gözat** > **uygulama hizmetleri** >, web uygulaması adı.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-196">In [Azure Portal](https://portal.azure.com), open hello web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="b7d9d-197">Web uygulamanızın dikey penceresinde tıklayın **tüm ayarları**, ardından **uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-197">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="b7d9d-198">Toohello aşağı **uygulama ayarları** bölümünde ve hello değerlerini ayarlayabilirsiniz **deposu\_adı**, **depolama\_adı** ve  **Depolama\_anahtar** hello açıklandığı gibi **yapılandırma hello proje** yukarıdaki bölümde.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-198">Scroll down toohello **App settings** section and set hello values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in hello **Configure hello project** section above.</span></span>
   
     ![Uygulama ayarları](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="b7d9d-200">**Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-200">Click on **Save**.</span></span> <span data-ttu-id="b7d9d-201">Merhaba değişiklikleri uygulandı hello bildirimleri aldığınız sonra tıklayın **Gözat** hello Web uygulama ana dikey penceresinden.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-201">After you've received hello notifications that hello changes were applied, click on **Browse** from hello Web app main blade.</span></span>
5. <span data-ttu-id="b7d9d-202">Hello kullanarak, beklendiği gibi hello web uygulama çalışma görmelisiniz **Azure Table Storage** deposu.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-202">You should see hello web app working as expected, using hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="b7d9d-203">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="b7d9d-203">Congratulations!</span></span>
   
     ![Web Tarayıcısı](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="b7d9d-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b7d9d-205">Next steps</span></span>
<span data-ttu-id="b7d9d-206">Visual Studio, Flask ve Azure tablo depolaması için Python araçları hakkında daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="b7d9d-206">Follow these links toolearn more about Python Tools for Visual Studio, Flask and Azure Table Storage.</span></span>

* <span data-ttu-id="b7d9d-207">[Visual Studio için Python Araçları Belgeleri]</span><span class="sxs-lookup"><span data-stu-id="b7d9d-207">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="b7d9d-208">[Web Projeleri]</span><span class="sxs-lookup"><span data-stu-id="b7d9d-208">[Web Projects]</span></span>
  * <span data-ttu-id="b7d9d-209">[Bulut Hizmeti Projeleri]</span><span class="sxs-lookup"><span data-stu-id="b7d9d-209">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="b7d9d-210">[Microsoft Azure’da Uzaktan Hata Ayıklama]</span><span class="sxs-lookup"><span data-stu-id="b7d9d-210">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="b7d9d-211">[Flask belgeleri]</span><span class="sxs-lookup"><span data-stu-id="b7d9d-211">[Flask Documentation]</span></span>
* <span data-ttu-id="b7d9d-212">[Azure Depolama]</span><span class="sxs-lookup"><span data-stu-id="b7d9d-212">[Azure Storage]</span></span>
* <span data-ttu-id="b7d9d-213">[Python için Azure SDK]</span><span class="sxs-lookup"><span data-stu-id="b7d9d-213">[Azure SDK for Python]</span></span>
* <span data-ttu-id="b7d9d-214">[Nasıl tooUse hello Python tablo Depolama hizmetinden]</span><span class="sxs-lookup"><span data-stu-id="b7d9d-214">[How tooUse hello Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="b7d9d-215">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="b7d9d-215">What's changed</span></span>
* <span data-ttu-id="b7d9d-216">Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="b7d9d-216">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Python Geliştirici Merkezi]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md
[belgelerine]:../cosmos-db/table-storage-how-to-use-python.md
[Nasıl tooUse hello Python tablo Depolama hizmetinden]:../cosmos-db/table-storage-how-to-use-python.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[.NET için Azure SDK]: http://azure.microsoft.com/downloads/
[Visual Studio için Python Araçları]: http://aka.ms/ptvs
[Visual Studio için Python Araçları 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio Örnekleri VSIX için Python araçları 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025
[VS 2015 için Azure SDK Araçları]: http://go.microsoft.com/fwlink/?linkid=518003
[Python 2.7 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517191
[Visual Studio için Python Araçları Belgeleri]: http://aka.ms/ptvsdocs
[Flask belgeleri]: http://flask.pocoo.org/
[Microsoft Azure’da Uzaktan Hata Ayıklama]: http://go.microsoft.com/fwlink/?LinkId=624026
[Web Projeleri]: http://go.microsoft.com/fwlink/?LinkId=624027
[Bulut Hizmeti Projeleri]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure Depolama]: http://azure.microsoft.com/documentation/services/storage/
[Python için Azure SDK]: https://github.com/Azure/azure-sdk-for-python
