---
title: "aaaBottle ve Visual Studio için Python araçları 2.2 ile azure'da Azure tablo depolaması"
description: "Merhaba web uygulama tooAzure App Service Web Apps dağıtmak ve nasıl toouse hello Python araçları için Visual Studio toocreate verileri Azure tablo depolama alanında depolar Bottle uygulama öğrenin."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: f075124b-db79-4e51-b394-09187dd6c634
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 25b9eb002b8748483d5b9458b7b5860a958b4bb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="401c1-103">Bottle ve Visual Studio için Python araçları 2.2 ile azure'da Azure tablo depolaması</span><span class="sxs-lookup"><span data-stu-id="401c1-103">Bottle and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="401c1-104">Bu öğreticide, kullanacağız [Visual Studio için Python Araçları] toocreate basit bir web uygulamasına hello PTVS örnek şablonlarından birini kullanarak yoklar.</span><span class="sxs-lookup"><span data-stu-id="401c1-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="401c1-105">Bu öğretici olarak da kullanılabilir bir [video](https://www.youtube.com/watch?v=GJXDGaEPy94).</span><span class="sxs-lookup"><span data-stu-id="401c1-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=GJXDGaEPy94).</span></span>

<span data-ttu-id="401c1-106">depoları (bellek içi, Azure Table Storage, MongoDB) farklı türleri arasında kolayca geçebilirsiniz şekilde hello yoklamalar web uygulaması, havuz için bir Özet tanımlar.</span><span class="sxs-lookup"><span data-stu-id="401c1-106">hello polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="401c1-107">Biz nasıl toocreate bir Azure depolama hesabı, tooconfigure hello nasıl web uygulama toouse Azure tablo depolaması ve nasıl öğreneceksiniz toopublish hello web uygulaması çok[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="401c1-107">We'll learn how toocreate an Azure Storage account, how tooconfigure hello web app toouse Azure Table Storage, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="401c1-108">Merhaba bkz [Python Geliştirici Merkezi] Bottle kullanarak PTVS ile Azure App Service Web Apps geliştirmeyi kapsayan diğer makaleler için Flask ve Django web altyapılarını MongoDB, Azure Table Storage, MySQL ve SQL Database hizmetleriyle.</span><span class="sxs-lookup"><span data-stu-id="401c1-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="401c1-109">Bu makale App Service'e odaklanmakla birlikte hello adımlar geliştirirken benzer [Azure Cloud Services].</span><span class="sxs-lookup"><span data-stu-id="401c1-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="401c1-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="401c1-110">Prerequisites</span></span>
* <span data-ttu-id="401c1-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="401c1-111">Visual Studio 2015</span></span>
* <span data-ttu-id="401c1-112">[Visual Studio için Python Araçları 2.2]</span><span class="sxs-lookup"><span data-stu-id="401c1-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="401c1-113">[Visual Studio Örnekleri VSIX için Python araçları 2.2]</span><span class="sxs-lookup"><span data-stu-id="401c1-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="401c1-114">[VS 2015 için Azure SDK Araçları]</span><span class="sxs-lookup"><span data-stu-id="401c1-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="401c1-115">[Python 2.7 32 bit] veya [Python 3.4 32 bit]</span><span class="sxs-lookup"><span data-stu-id="401c1-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="401c1-116">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="401c1-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="401c1-117">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="401c1-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="401c1-118">Başlangıç projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="401c1-118">Create hello Project</span></span>
<span data-ttu-id="401c1-119">Bu bölümde, örnek şablonu kullanarak bir Visual Studio projesi oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="401c1-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="401c1-120">Biz sanal ortam oluşturacak ve gerekli paketleri yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="401c1-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="401c1-121">Ardından biz hello uygulaması hello varsayılan bellek içi depoya kullanarak yerel olarak çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="401c1-121">Then we'll run hello application locally using hello default in-memory repository.</span></span>

1. <span data-ttu-id="401c1-122">Visual Studio'da, **Dosya**, **Yeni Proje**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="401c1-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="401c1-123">Proje şablonlarını hello hello [Visual Studio Örnekleri VSIX için Python araçları 2.2] altında kullanılabilir **Python**, **örnekleri**.</span><span class="sxs-lookup"><span data-stu-id="401c1-123">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="401c1-124">Seçin **yoklamalar Bottle Web projesi** ve Tamam toocreate hello proje'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="401c1-124">Select **Polls Bottle Web Project** and click OK toocreate hello project.</span></span>
   
     ![Yeni Proje İletişim Kutusu](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. <span data-ttu-id="401c1-126">İstendiğinde tooinstall dış paketler olacaktır.</span><span class="sxs-lookup"><span data-stu-id="401c1-126">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="401c1-127">**Sanal bir ortama yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="401c1-127">Select **Install into a virtual environment**.</span></span>
   
     ![Dış Paketler İletişim Kutusu](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. <span data-ttu-id="401c1-129">Seçin **Python 2.7** veya **Python 3.4** hello temel yorumlayıcı olarak.</span><span class="sxs-lookup"><span data-stu-id="401c1-129">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
     ![Sanal Ortama Ekle İletişim Kutusu](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="401c1-131">Merhaba uygulaması tuşlarına basarak çalıştığını onaylayın `F5`.</span><span class="sxs-lookup"><span data-stu-id="401c1-131">Confirm that hello application works by pressing `F5`.</span></span> <span data-ttu-id="401c1-132">Varsayılan olarak, herhangi bir yapılandırma gerektirmeyen bir bellek içi depoya hello uygulama kullanır.</span><span class="sxs-lookup"><span data-stu-id="401c1-132">By default, hello application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="401c1-133">Tüm veriler kaybolur hello web sunucusu durdurulduğunda.</span><span class="sxs-lookup"><span data-stu-id="401c1-133">All data is lost when hello web server is stopped.</span></span>
6. <span data-ttu-id="401c1-134">Tıklatın **örnek yoklamalar Oluştur**, ardından bir yoklamaya tıklayın ve oy verin.</span><span class="sxs-lookup"><span data-stu-id="401c1-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Web Tarayıcısı](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="401c1-136">Bir Azure depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="401c1-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="401c1-137">toouse depolama işlemleri, bir Azure depolama hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="401c1-137">toouse storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="401c1-138">Aşağıdaki adımları izleyerek bir depolama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="401c1-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="401c1-139">Merhaba günlüğüne [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="401c1-139">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="401c1-140">Merhaba tıklatın **yeni** hello üst simgesine sol hello Portal ', ardından **veri + depolama** > **depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="401c1-140">Click hello **New** icon on hello top left of hello Portal, then click **Data + Storage** > **Storage Account**.</span></span>  <span data-ttu-id="401c1-141">Merhaba tıklatın **oluşturma** düğmesine tıklayın, ardından hello depolama hesabı benzersiz bir ad verin ve yeni bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) onun için.</span><span class="sxs-lookup"><span data-stu-id="401c1-141">Click hello **Create** button, then give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Hızlı oluştur](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="401c1-143">Merhaba depolama hesabı oluşturduğunuzda hello **bildirimleri** düğmesi yeşil flash **başarı** ve hello depolama hesabının dikey penceresi açık toohello yeni kaynak ait tooshow grubunu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="401c1-143">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="401c1-144">Merhaba tıklatın **erişim anahtarları** hello depolama hesabı dikey penceresinde parçası.</span><span class="sxs-lookup"><span data-stu-id="401c1-144">Click hello **Access keys** part in hello storage account's blade.</span></span> <span data-ttu-id="401c1-145">Merhaba hesap adı ve key1 not edin.</span><span class="sxs-lookup"><span data-stu-id="401c1-145">Take note of hello account name and key1.</span></span>
   
      ![Anahtarlar](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="401c1-147">Biz bu bilgileri tooconfigure hello sonraki bölümde projenizde gerekir.</span><span class="sxs-lookup"><span data-stu-id="401c1-147">We will need this information tooconfigure your project in hello next section.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="401c1-148">Merhaba projeyi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="401c1-148">Configure hello Project</span></span>
<span data-ttu-id="401c1-149">Bu bölümde, yeni oluşturduğumuz bizim uygulama toouse hello depolama hesabı yapılandıracağız.</span><span class="sxs-lookup"><span data-stu-id="401c1-149">In this section, we'll configure our application toouse hello storage account we just created.</span></span> <span data-ttu-id="401c1-150">Ardından hello uygulama yerel olarak çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="401c1-150">Then we'll run hello application locally.</span></span>

1. <span data-ttu-id="401c1-151">Visual Studio'da, Çözüm Gezgini'nde, proje düğümüne sağ tıklayın ve seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="401c1-151">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="401c1-152">Tıklatın hello üzerinde **hata ayıklama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="401c1-152">Click on hello **Debug** tab.</span></span>
   
     ![Proje hata ayıklama ayarları](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="401c1-154">Merhaba değerlerini hello uygulamada gerekli ortam değişkenleri **Debug sunucu komutunu**, **ortam**.</span><span class="sxs-lookup"><span data-stu-id="401c1-154">Set hello values of environment variables required by hello application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="401c1-155">Bu hello ortam değişkenleri ayarlar olduğunda, **hata ayıklamayı Başlat**.</span><span class="sxs-lookup"><span data-stu-id="401c1-155">This will set hello environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="401c1-156">İsterseniz hello değişkenleri toobe ne zaman ayarlayın, **hata ayıklama olmadan Başlat**, aynı değerleri kümesi hello **sunucu komutu Çalıştır** de.</span><span class="sxs-lookup"><span data-stu-id="401c1-156">If you want hello variables toobe set when you **Start Without Debugging**, set hello same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="401c1-157">Alternatif olarak, Windows Denetim Masası hello kullanarak ortam değişkenlerini tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="401c1-157">Alternatively, you can define environment variables using hello Windows Control Panel.</span></span> <span data-ttu-id="401c1-158">Kaynak kodunda kimlik bilgilerini depolama tooavoid istediğiniz / proje dosyası, daha iyi bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="401c1-158">This is a better option if you want tooavoid storing credentials in source code / project file.</span></span> <span data-ttu-id="401c1-159">Merhaba yeni ortam değerleri toobe kullanılabilir toohello uygulaması için Visual Studio toorestart gerektiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="401c1-159">Note that you will need toorestart Visual Studio for hello new environment values toobe available toohello application.</span></span>
3. <span data-ttu-id="401c1-160">hello Azure Table Storage deposu uygulayan hello kodudur içinde **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="401c1-160">hello code that implements hello Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="401c1-161">Merhaba bkz [belgelerine] hakkında daha fazla bilgi için toouse Python tablo hizmetinden.</span><span class="sxs-lookup"><span data-stu-id="401c1-161">See hello [documentation] for more information on how toouse Table Service from Python.</span></span>
4. <span data-ttu-id="401c1-162">Merhaba uygulamayla çalıştırmak `F5`.</span><span class="sxs-lookup"><span data-stu-id="401c1-162">Run hello application with `F5`.</span></span> <span data-ttu-id="401c1-163">İle oluşturulan yoklamalar **örnek yoklamalar Oluştur** ve oy vermeyle gönderilen hello veri Azure tablo Depolama'da seri.</span><span class="sxs-lookup"><span data-stu-id="401c1-163">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="401c1-164">Merhaba Python 2.7 sanal ortamı Visual Studio'da bir özel durum sonu neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="401c1-164">hello Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="401c1-165">Tuşuna `F5` toocontinue hello web projesi yükleniyor.</span><span class="sxs-lookup"><span data-stu-id="401c1-165">Press `F5` toocontinue loading hello web project.</span></span>
   > 
   > 
5. <span data-ttu-id="401c1-166">Toohello Gözat **hakkında** uygulama hello sayfa tooverify hello kullanarak **Azure Table Storage** deposu.</span><span class="sxs-lookup"><span data-stu-id="401c1-166">Browse toohello **About** page tooverify that hello application is using hello **Azure Table Storage** repository.</span></span>
   
     ![Web Tarayıcısı](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a><span data-ttu-id="401c1-168">Hello Azure Table Storage keşfedin</span><span class="sxs-lookup"><span data-stu-id="401c1-168">Explore hello Azure Table Storage</span></span>
<span data-ttu-id="401c1-169">Bu kolay tooview ve Visual Studio Cloud Explorer kullanarak depolama tabloları düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="401c1-169">It's easy tooview and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="401c1-170">Bu bölümde Sunucu Gezgini tooview hello hello yoklamalar uygulama tabloların içeriğini kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="401c1-170">In this section we'll use Server Explorer tooview hello contents of hello polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="401c1-171">Bu, kullanılabilir olan yüklü Microsoft Azure Araçları toobe gerektirir hello bir parçası olarak [.NET için Azure SDK].</span><span class="sxs-lookup"><span data-stu-id="401c1-171">This requires Microsoft Azure Tools toobe installed, which are available as part of hello [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="401c1-172">Açık **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="401c1-172">Open **Cloud Explorer**.</span></span> <span data-ttu-id="401c1-173">Genişletme **depolama hesapları**, depolama hesabınızın sonra **tabloları**.</span><span class="sxs-lookup"><span data-stu-id="401c1-173">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Bulut Gezgini](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="401c1-175">Merhaba üzerinde çift **yoklamalar** veya **seçenekleri** tablo tooview hello Ekle/Kaldır/Düzenle varlıklar yanı sıra, bir belge penceresinde hello tablosunun içeriğini.</span><span class="sxs-lookup"><span data-stu-id="401c1-175">Double-click on hello **polls** or **choices** table tooview hello contents of hello table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![Tablo sorgusu sonuçları](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="401c1-177">Yayımlama Hello web uygulama tooAzure uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="401c1-177">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="401c1-178">Hello Azure .NET SDK'sını kolay bir yolu toodeploy web uygulama tooAzure uygulama hizmeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="401c1-178">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="401c1-179">İçinde **Çözüm Gezgini**, hello proje düğümüne sağ tıklayın ve seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="401c1-179">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
     ![Web Yayımlama İletişim Kutusu](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="401c1-181">**Microsoft Azure Web Apps** ’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="401c1-181">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="401c1-182">Tıklayın **yeni** toocreate yeni bir web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="401c1-182">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="401c1-183">Hello aşağıdaki alanları doldurun ve **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="401c1-183">Fill in hello following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="401c1-184">**Web Uygulaması adı**</span><span class="sxs-lookup"><span data-stu-id="401c1-184">**Web App name**</span></span>
   * <span data-ttu-id="401c1-185">**App Service planı**</span><span class="sxs-lookup"><span data-stu-id="401c1-185">**App Service plan**</span></span>
   * <span data-ttu-id="401c1-186">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="401c1-186">**Resource group**</span></span>
   * <span data-ttu-id="401c1-187">**Bölge**</span><span class="sxs-lookup"><span data-stu-id="401c1-187">**Region**</span></span>
   * <span data-ttu-id="401c1-188">Bırakın **veritabanı sunucusu** çok ayarlamak**veritabanı yok**</span><span class="sxs-lookup"><span data-stu-id="401c1-188">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="401c1-189">Diğer tüm varsayılanları kabul edin ve **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="401c1-189">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="401c1-190">Web tarayıcınız toohello yayımlanan web uygulamasına otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="401c1-190">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="401c1-191">Sayfa hakkında toohello göz atarsanız, hello kullandığını görürsünüz **bellek içi** deposu, değil hello **Azure Table Storage** deposu.</span><span class="sxs-lookup"><span data-stu-id="401c1-191">If you browse toohello about page, you'll see that it uses hello **In-Memory** repository, not hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="401c1-192">Merhaba ortam değişkenleri hello Azure App Service'te Web Apps örneğinde ayarlanmamış belirtilen hello varsayılan değerleri kullanan çünkü **ProjectName**.</span><span class="sxs-lookup"><span data-stu-id="401c1-192">That's because hello environment variables are not set on hello Web Apps instance in Azure App Service, so it uses hello default values specified in **settings.py**.</span></span>

## <a name="configure-hello-web-apps-instance"></a><span data-ttu-id="401c1-193">Merhaba Web uygulamaları örnek yapılandırma</span><span class="sxs-lookup"><span data-stu-id="401c1-193">Configure hello Web Apps instance</span></span>
<span data-ttu-id="401c1-194">Bu bölümde, hello Web Apps örneği için ortam değişkenleri yapılandıracağız.</span><span class="sxs-lookup"><span data-stu-id="401c1-194">In this section, we'll configure environment variables for hello Web Apps instance.</span></span>

1. <span data-ttu-id="401c1-195">İçinde [Azure Portal], tıklayarak hello web uygulamanızın dikey penceresini açmak **Gözat** > **uygulama hizmetleri** >, web uygulaması adı.</span><span class="sxs-lookup"><span data-stu-id="401c1-195">In [Azure Portal], open hello web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="401c1-196">Web uygulamanızın dikey penceresinde tıklayın **tüm ayarları**, ardından **uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="401c1-196">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="401c1-197">Toohello aşağı **uygulama ayarları** bölümünde ve hello değerlerini ayarlayabilirsiniz **deposu\_adı**, **depolama\_adı** ve  **Depolama\_anahtar** hello açıklandığı gibi **yapılandırma hello proje** yukarıdaki bölümde.</span><span class="sxs-lookup"><span data-stu-id="401c1-197">Scroll down toohello **App settings** section and set hello values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in hello **Configure hello project** section above.</span></span>
   
     ![Uygulama ayarları](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="401c1-199">**Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="401c1-199">Click on **Save**.</span></span> <span data-ttu-id="401c1-200">Merhaba değişiklikleri uygulandı hello bildirimleri aldığınız sonra tıklayın **Gözat** hello Web uygulama ana dikey penceresinden.</span><span class="sxs-lookup"><span data-stu-id="401c1-200">After you've received hello notifications that hello changes were applied, click on **Browse** from hello Web app main blade.</span></span>
5. <span data-ttu-id="401c1-201">Hello kullanarak, beklendiği gibi hello web uygulama çalışma görmelisiniz **Azure Table Storage** deposu.</span><span class="sxs-lookup"><span data-stu-id="401c1-201">You should see hello web app working as expected, using hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="401c1-202">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="401c1-202">Congratulations!</span></span>
   
     ![Web Tarayıcısı](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="401c1-204">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="401c1-204">Next steps</span></span>
<span data-ttu-id="401c1-205">Visual Studio, Bottle ve Azure tablo depolaması için Python araçları hakkında daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="401c1-205">Follow these links toolearn more about Python Tools for Visual Studio, Bottle and Azure Table Storage.</span></span>

* <span data-ttu-id="401c1-206">[Visual Studio için Python Araçları Belgeleri]</span><span class="sxs-lookup"><span data-stu-id="401c1-206">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="401c1-207">[Web Projeleri]</span><span class="sxs-lookup"><span data-stu-id="401c1-207">[Web Projects]</span></span>
  * <span data-ttu-id="401c1-208">[Bulut Hizmeti Projeleri]</span><span class="sxs-lookup"><span data-stu-id="401c1-208">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="401c1-209">[Microsoft Azure’da Uzaktan Hata Ayıklama]</span><span class="sxs-lookup"><span data-stu-id="401c1-209">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="401c1-210">[Bottle belgeleri]</span><span class="sxs-lookup"><span data-stu-id="401c1-210">[Bottle Documentation]</span></span>
* <span data-ttu-id="401c1-211">[Azure Depolama]</span><span class="sxs-lookup"><span data-stu-id="401c1-211">[Azure Storage]</span></span>
* <span data-ttu-id="401c1-212">[Python için Azure SDK]</span><span class="sxs-lookup"><span data-stu-id="401c1-212">[Azure SDK for Python]</span></span>
* <span data-ttu-id="401c1-213">[Nasıl tooUse hello Python tablo Depolama hizmetinden]</span><span class="sxs-lookup"><span data-stu-id="401c1-213">[How tooUse hello Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="401c1-214">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="401c1-214">What's changed</span></span>
* <span data-ttu-id="401c1-215">Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="401c1-215">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Python Geliştirici Merkezi]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md
[belgelerine]:../cosmos-db/table-storage-how-to-use-python.md
[Nasıl tooUse hello Python tablo Depolama hizmetinden]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[.NET için Azure SDK]: http://azure.microsoft.com/downloads/
[Visual Studio için Python Araçları]: http://aka.ms/ptvs
[Visual Studio için Python Araçları 2.2]: http://go.microsoft.com/fwlink/?LinkId=624025
[Visual Studio Örnekleri VSIX için Python araçları 2.2]: http://go.microsoft.com/fwlink/?LinkId=624025
[VS 2015 için Azure SDK Araçları]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517191
[Visual Studio için Python Araçları Belgeleri]: http://aka.ms/ptvsdocs
[Bottle belgeleri]: http://bottlepy.org/docs/dev/index.html
[Microsoft Azure’da Uzaktan Hata Ayıklama]: http://go.microsoft.com/fwlink/?LinkId=624026
[Web Projeleri]: http://go.microsoft.com/fwlink/?LinkId=624027
[Bulut Hizmeti Projeleri]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure Depolama]: http://azure.microsoft.com/documentation/services/storage/
[Python için Azure SDK]: https://github.com/Azure/azure-sdk-for-python
