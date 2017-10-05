---
title: "Bottle ve Visual Studio için Python araçları 2.2 ile azure'da Azure tablo depolaması"
description: "Verileri Azure tablo depolama alanında depolar Bottle uygulaması oluşturmak için Visual Studio için Python araçlarını kullanmayı öğrenin ve Azure App Service Web Apps için web uygulaması dağıtma."
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
ms.openlocfilehash: fb25f03607ac6e9af46b47f54e830e0283dd1b0a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="ef74f-103">Bottle ve Visual Studio için Python araçları 2.2 ile azure'da Azure tablo depolaması</span><span class="sxs-lookup"><span data-stu-id="ef74f-103">Bottle and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="ef74f-104">Bu öğreticide, kullanacağız [Visual Studio için Python Araçları] yoklamalar web uygulaması PTVS örnek şablonlarından birini kullanarak basit bir oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="ef74f-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="ef74f-105">Bu öğretici olarak da kullanılabilir bir [video](https://www.youtube.com/watch?v=GJXDGaEPy94).</span><span class="sxs-lookup"><span data-stu-id="ef74f-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=GJXDGaEPy94).</span></span>

<span data-ttu-id="ef74f-106">Depoları (bellek içi, Azure Table Storage, MongoDB) farklı türleri arasında kolayca geçebilirsiniz şekilde yoklamalar web uygulaması, havuz için bir Özet tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ef74f-106">The polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="ef74f-107">Size bir Azure depolama hesabının nasıl oluşturulacağını, Azure Table Storage kullanmak için web uygulamasını yapılandırma ve web uygulaması'na yayımlamak nasıl öğreneceksiniz [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="ef74f-107">We'll learn how to create an Azure Storage account, how to configure the web app to use Azure Table Storage, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="ef74f-108">Bkz: [Python Geliştirici Merkezi] Bottle kullanarak PTVS ile Azure App Service Web Apps geliştirmeyi kapsayan diğer makaleler için Flask ve Django web altyapılarını MongoDB, Azure Table Storage, MySQL ve SQL Database hizmetleriyle.</span><span class="sxs-lookup"><span data-stu-id="ef74f-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="ef74f-109">Bu makale App Service’e odaklanmakla birlikte, [Azure Cloud Services]’i geliştirirken adımlar benzerdir.</span><span class="sxs-lookup"><span data-stu-id="ef74f-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef74f-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ef74f-110">Prerequisites</span></span>
* <span data-ttu-id="ef74f-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="ef74f-111">Visual Studio 2015</span></span>
* <span data-ttu-id="ef74f-112">[Visual Studio için Python Araçları 2.2]</span><span class="sxs-lookup"><span data-stu-id="ef74f-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="ef74f-113">[Visual Studio Örnekleri VSIX için Python Tools 2.2]</span><span class="sxs-lookup"><span data-stu-id="ef74f-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="ef74f-114">[VS 2015 için Azure SDK Araçları]</span><span class="sxs-lookup"><span data-stu-id="ef74f-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="ef74f-115">[Python 2.7 32 bit] veya [Python 3.4 32 bit]</span><span class="sxs-lookup"><span data-stu-id="ef74f-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="ef74f-116">Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="ef74f-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ef74f-117">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ef74f-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-the-project"></a><span data-ttu-id="ef74f-118">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="ef74f-118">Create the Project</span></span>
<span data-ttu-id="ef74f-119">Bu bölümde, örnek şablonu kullanarak bir Visual Studio projesi oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="ef74f-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="ef74f-120">Biz sanal ortam oluşturacak ve gerekli paketleri yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="ef74f-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="ef74f-121">Ardından biz varsayılan bellek içi depoya kullanarak yerel olarak uygulaması çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="ef74f-121">Then we'll run the application locally using the default in-memory repository.</span></span>

1. <span data-ttu-id="ef74f-122">Visual Studio'da, **Dosya**, **Yeni Proje**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="ef74f-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="ef74f-123">[Visual Studio Örnekleri VSIX için Python Tools 2.2] proje şablonlarını **Python**, **Örnekler** altında bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef74f-123">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="ef74f-124">Seçin **yoklamalar Bottle Web projesi** ve projeyi oluşturmak için Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ef74f-124">Select **Polls Bottle Web Project** and click OK to create the project.</span></span>
   
     ![Yeni Proje İletişim Kutusu](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. <span data-ttu-id="ef74f-126">Dış paketleri yüklemeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="ef74f-126">You will be prompted to install external packages.</span></span> <span data-ttu-id="ef74f-127">**Sanal bir ortama yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="ef74f-127">Select **Install into a virtual environment**.</span></span>
   
     ![Dış Paketler İletişim Kutusu](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. <span data-ttu-id="ef74f-129">Temel yorumlayıcı olarak **Python 2.7** veya **Python 3.4**’ü seçin.</span><span class="sxs-lookup"><span data-stu-id="ef74f-129">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span></span>
   
     ![Sanal Ortama Ekle İletişim Kutusu](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="ef74f-131">`F5` tuşuna basarak uygulamanın çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ef74f-131">Confirm that the application works by pressing `F5`.</span></span> <span data-ttu-id="ef74f-132">Varsayılan olarak, uygulama herhangi bir yapılandırma gerektirmeyen bir bellek içi depoya kullanır.</span><span class="sxs-lookup"><span data-stu-id="ef74f-132">By default, the application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="ef74f-133">Tüm veriler kaybolur web sunucusu durdurulduğunda.</span><span class="sxs-lookup"><span data-stu-id="ef74f-133">All data is lost when the web server is stopped.</span></span>
6. <span data-ttu-id="ef74f-134">Tıklatın **örnek yoklamalar Oluştur**, ardından bir yoklamaya tıklayın ve oy verin.</span><span class="sxs-lookup"><span data-stu-id="ef74f-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Web Tarayıcısı](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="ef74f-136">Bir Azure depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ef74f-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="ef74f-137">Depolama işlemlerini kullanmak için bir Azure depolama hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef74f-137">To use storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="ef74f-138">Aşağıdaki adımları izleyerek bir depolama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef74f-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="ef74f-139">İçine oturum [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ef74f-139">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ef74f-140">Tıklatın **yeni** üst simgesine portalın sol, ardından **veri + depolama** > **depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="ef74f-140">Click the **New** icon on the top left of the Portal, then click **Data + Storage** > **Storage Account**.</span></span>  <span data-ttu-id="ef74f-141">Tıklatın **oluşturma** düğmesine tıklayın, ardından depolama hesabı benzersiz bir ad verin ve yeni bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) onun için.</span><span class="sxs-lookup"><span data-stu-id="ef74f-141">Click the **Create** button, then give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Hızlı oluştur](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="ef74f-143">Depolama hesabı oluşturduğunuzda **bildirimleri** düğmesi yeşil flash **başarı** ve depolama hesabı dikey penceresinde, oluşturduğunuz yeni kaynak grubuna ait olduğunu göstermek için açık.</span><span class="sxs-lookup"><span data-stu-id="ef74f-143">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="ef74f-144">Tıklatın **erişim anahtarları** depolama hesabı dikey penceresinde parçası.</span><span class="sxs-lookup"><span data-stu-id="ef74f-144">Click the **Access keys** part in the storage account's blade.</span></span> <span data-ttu-id="ef74f-145">Hesap adı ve key1 not edin.</span><span class="sxs-lookup"><span data-stu-id="ef74f-145">Take note of the account name and key1.</span></span>
   
      ![Anahtarlar](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="ef74f-147">Sonraki bölümde projenizi yapılandırmak için bu bilgileri ihtiyacımız.</span><span class="sxs-lookup"><span data-stu-id="ef74f-147">We will need this information to configure your project in the next section.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="ef74f-148">Projeyi Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ef74f-148">Configure the Project</span></span>
<span data-ttu-id="ef74f-149">Bu bölümde, yeni oluşturduğumuz depolama hesabı kullanmak üzere uygulamamız yapılandıracağız.</span><span class="sxs-lookup"><span data-stu-id="ef74f-149">In this section, we'll configure our application to use the storage account we just created.</span></span> <span data-ttu-id="ef74f-150">Sonra uygulamayı yerel olarak çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="ef74f-150">Then we'll run the application locally.</span></span>

1. <span data-ttu-id="ef74f-151">Visual Studio'da, Çözüm Gezgini'nde, proje düğümüne sağ tıklayın ve seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="ef74f-151">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="ef74f-152">Tıklayın **hata ayıklama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ef74f-152">Click on the **Debug** tab.</span></span>
   
     ![Proje hata ayıklama ayarları](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="ef74f-154">Uygulama tarafından gerekli ortam değişkenlerinin değerlerini ayarlamak **Debug sunucu komutunu**, **ortam**.</span><span class="sxs-lookup"><span data-stu-id="ef74f-154">Set the values of environment variables required by the application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="ef74f-155">Bu ortam değişkenleri ayarlar olduğunda, **hata ayıklamayı Başlat**.</span><span class="sxs-lookup"><span data-stu-id="ef74f-155">This will set the environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="ef74f-156">Ne zaman ayarlanacak değişkenleri istiyorsanız, **hata ayıklama olmadan Başlat**, altında aynı değerlere ayarlamak **sunucu komutu Çalıştır** de.</span><span class="sxs-lookup"><span data-stu-id="ef74f-156">If you want the variables to be set when you **Start Without Debugging**, set the same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="ef74f-157">Alternatif olarak, Windows Denetim Masası'nı kullanarak ortam değişkenlerini tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef74f-157">Alternatively, you can define environment variables using the Windows Control Panel.</span></span> <span data-ttu-id="ef74f-158">Proje dosyası kaynak kodunda kimlik bilgilerini depolama önlemek istiyorsanız, daha iyi bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="ef74f-158">This is a better option if you want to avoid storing credentials in source code / project file.</span></span> <span data-ttu-id="ef74f-159">Uygulama için kullanılabilir olması için Visual Studio yeni ortam değerleri için yeniden başlatmanız gerekecektir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ef74f-159">Note that you will need to restart Visual Studio for the new environment values to be available to the application.</span></span>
3. <span data-ttu-id="ef74f-160">Azure Table Storage depo uygulayan kod **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="ef74f-160">The code that implements the Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="ef74f-161">Bkz: [belgelerine] Python tablo hizmetinden kullanma hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ef74f-161">See the [documentation] for more information on how to use Table Service from Python.</span></span>
4. <span data-ttu-id="ef74f-162">Uygulamayı `F5` ile çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ef74f-162">Run the application with `F5`.</span></span> <span data-ttu-id="ef74f-163">İle oluşturulan yoklamalar **örnek yoklamalar Oluştur** ve oy vermeyle gönderilen veriler Azure tablo Depolama'da seri hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="ef74f-163">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ef74f-164">Python 2.7 sanal ortamı Visual Studio'da bir özel durum sonu neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="ef74f-164">The Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="ef74f-165">Tuşuna `F5` web projesi yüklemeye devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="ef74f-165">Press `F5` to continue loading the web project.</span></span>
   > 
   > 
5. <span data-ttu-id="ef74f-166">Gözat **hakkında** uygulama kullandığını doğrulamak için sayfa **Azure Table Storage** deposu.</span><span class="sxs-lookup"><span data-stu-id="ef74f-166">Browse to the **About** page to verify that the application is using the **Azure Table Storage** repository.</span></span>
   
     ![Web Tarayıcısı](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-the-azure-table-storage"></a><span data-ttu-id="ef74f-168">Azure Table Storage keşfedin</span><span class="sxs-lookup"><span data-stu-id="ef74f-168">Explore the Azure Table Storage</span></span>
<span data-ttu-id="ef74f-169">Visual Studio Cloud Explorer kullanarak depolama tabloları görüntüleyip kolaydır.</span><span class="sxs-lookup"><span data-stu-id="ef74f-169">It's easy to view and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="ef74f-170">Bu bölümde yoklamalar uygulama tabloların içeriğini görüntülemek için Sunucu Gezgini kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="ef74f-170">In this section we'll use Server Explorer to view the contents of the polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="ef74f-171">Bu Microsoft Azure yüklenmek üzere olarak kullanılabilir olan araçları gerektirir parçası [.NET için Azure SDK].</span><span class="sxs-lookup"><span data-stu-id="ef74f-171">This requires Microsoft Azure Tools to be installed, which are available as part of the [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="ef74f-172">Açık **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="ef74f-172">Open **Cloud Explorer**.</span></span> <span data-ttu-id="ef74f-173">Genişletme **depolama hesapları**, depolama hesabınızın sonra **tabloları**.</span><span class="sxs-lookup"><span data-stu-id="ef74f-173">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Bulut Gezgini](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="ef74f-175">Çift **yoklamalar** veya **seçimler** bir belge penceresi, aynı zamanda Ekle/Kaldır/Düzenle varlıklar tablosunun içeriğini görüntülemek için tablo.</span><span class="sxs-lookup"><span data-stu-id="ef74f-175">Double-click on the **polls** or **choices** table to view the contents of the table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![Tablo sorgusu sonuçları](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="ef74f-177">Web uygulamasını Azure App Service’te yayımlama</span><span class="sxs-lookup"><span data-stu-id="ef74f-177">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="ef74f-178">Azure .NET SDK’sı web uygulamanızı Azure App Service’te dağıtmanız için kolay bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef74f-178">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span></span>

1. <span data-ttu-id="ef74f-179">**Çözüm Gezgini**’nde, proje düğümüne sağ tıklayın ve **Yayımla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="ef74f-179">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>
   
     ![Web Yayımlama İletişim Kutusu](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="ef74f-181">**Microsoft Azure Web Apps** ’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef74f-181">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="ef74f-182">Yeni bir web uygulaması oluşturmak için **Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef74f-182">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="ef74f-183">Aşağıdaki alanları doldurun ve **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="ef74f-183">Fill in the following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="ef74f-184">**Web Uygulaması adı**</span><span class="sxs-lookup"><span data-stu-id="ef74f-184">**Web App name**</span></span>
   * <span data-ttu-id="ef74f-185">**App Service planı**</span><span class="sxs-lookup"><span data-stu-id="ef74f-185">**App Service plan**</span></span>
   * <span data-ttu-id="ef74f-186">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="ef74f-186">**Resource group**</span></span>
   * <span data-ttu-id="ef74f-187">**Bölge**</span><span class="sxs-lookup"><span data-stu-id="ef74f-187">**Region**</span></span>
   * <span data-ttu-id="ef74f-188">**Veritabanı sunucusu**nu **Veritabanı yok** olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="ef74f-188">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="ef74f-189">Diğer tüm varsayılanları kabul edin ve **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef74f-189">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="ef74f-190">Web tarayıcınız yayımlanan web uygulamasına otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="ef74f-190">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="ef74f-191">Üzere göz atarsanız sayfası hakkında bunu kullandığını görürsünüz **bellek içi** deposunu değil **Azure Table Storage** deposu.</span><span class="sxs-lookup"><span data-stu-id="ef74f-191">If you browse to the about page, you'll see that it uses the **In-Memory** repository, not the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="ef74f-192">Ortam değişkenleri Azure App Service'te Web Apps örneğinde ayarlanmamış belirtilen varsayılan değerleri kullanan çünkü **ProjectName**.</span><span class="sxs-lookup"><span data-stu-id="ef74f-192">That's because the environment variables are not set on the Web Apps instance in Azure App Service, so it uses the default values specified in **settings.py**.</span></span>

## <a name="configure-the-web-apps-instance"></a><span data-ttu-id="ef74f-193">Web uygulamaları örnek yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ef74f-193">Configure the Web Apps instance</span></span>
<span data-ttu-id="ef74f-194">Bu bölümde, Web uygulamaları örneği için ortam değişkenleri yapılandıracağız.</span><span class="sxs-lookup"><span data-stu-id="ef74f-194">In this section, we'll configure environment variables for the Web Apps instance.</span></span>

1. <span data-ttu-id="ef74f-195">İçinde [Azure Portal], web uygulamanızın dikey tıklayarak açın **Gözat** > **uygulama hizmetleri** >, web uygulaması adı.</span><span class="sxs-lookup"><span data-stu-id="ef74f-195">In [Azure Portal], open the web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="ef74f-196">Web uygulamanızın dikey penceresinde tıklayın **tüm ayarları**, ardından **uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="ef74f-196">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="ef74f-197">Ekranı aşağı kaydırarak **uygulama ayarları** bölümünde ve değerlerini ayarlayın **deposu\_adı**, **depolama\_adı** ve **depolama \_Anahtar** açıklandığı gibi **projeyi yapılandırma** yukarıdaki bölümde.</span><span class="sxs-lookup"><span data-stu-id="ef74f-197">Scroll down to the **App settings** section and set the values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in the **Configure the project** section above.</span></span>
   
     ![Uygulama ayarları](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="ef74f-199">**Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef74f-199">Click on **Save**.</span></span> <span data-ttu-id="ef74f-200">Değişiklikleri uygulandı bildirimleri aldığınız sonra tıklayın **Gözat** Web uygulama ana dikey penceresinden.</span><span class="sxs-lookup"><span data-stu-id="ef74f-200">After you've received the notifications that the changes were applied, click on **Browse** from the Web app main blade.</span></span>
5. <span data-ttu-id="ef74f-201">Web uygulaması kullanarak, beklendiği gibi çalıştığını görmelisiniz **Azure Table Storage** deposu.</span><span class="sxs-lookup"><span data-stu-id="ef74f-201">You should see the web app working as expected, using the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="ef74f-202">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="ef74f-202">Congratulations!</span></span>
   
     ![Web Tarayıcısı](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="ef74f-204">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ef74f-204">Next steps</span></span>
<span data-ttu-id="ef74f-205">Visual Studio, Bottle ve Azure tablo depolaması için Python araçları hakkında daha fazla bilgi için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="ef74f-205">Follow these links to learn more about Python Tools for Visual Studio, Bottle and Azure Table Storage.</span></span>

* <span data-ttu-id="ef74f-206">[Visual Studio için Python Araçları Belgeleri]</span><span class="sxs-lookup"><span data-stu-id="ef74f-206">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="ef74f-207">[Web Projeleri]</span><span class="sxs-lookup"><span data-stu-id="ef74f-207">[Web Projects]</span></span>
  * <span data-ttu-id="ef74f-208">[Bulut Hizmeti Projeleri]</span><span class="sxs-lookup"><span data-stu-id="ef74f-208">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="ef74f-209">[Microsoft Azure’da Uzaktan Hata Ayıklama]</span><span class="sxs-lookup"><span data-stu-id="ef74f-209">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="ef74f-210">[Bottle belgeleri]</span><span class="sxs-lookup"><span data-stu-id="ef74f-210">[Bottle Documentation]</span></span>
* <span data-ttu-id="ef74f-211">[Azure Depolama]</span><span class="sxs-lookup"><span data-stu-id="ef74f-211">[Azure Storage]</span></span>
* <span data-ttu-id="ef74f-212">[Python için Azure SDK]</span><span class="sxs-lookup"><span data-stu-id="ef74f-212">[Azure SDK for Python]</span></span>
* <span data-ttu-id="ef74f-213">[Python'dan Table depolama hizmetini kullanma]</span><span class="sxs-lookup"><span data-stu-id="ef74f-213">[How to Use the Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="ef74f-214">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="ef74f-214">What's changed</span></span>
* <span data-ttu-id="ef74f-215">Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="ef74f-215">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Python Geliştirici Merkezi]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md
[belgelerine]:../cosmos-db/table-storage-how-to-use-python.md
[Python'dan Table depolama hizmetini kullanma]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[.NET için Azure SDK]: http://azure.microsoft.com/downloads/
[Visual Studio için Python Araçları]: http://aka.ms/ptvs
[Visual Studio için Python Araçları 2.2]: http://go.microsoft.com/fwlink/?LinkId=624025
[Visual Studio Örnekleri VSIX için Python Tools 2.2]: http://go.microsoft.com/fwlink/?LinkId=624025
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
