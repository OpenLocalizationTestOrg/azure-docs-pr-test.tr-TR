---
title: "Azure SQL veritabanı ile bir ASP.NET uygulaması oluşturma | Microsoft Docs"
description: "Bir SQL veritabanına bağlantı ile Azure içinde çalışan bir ASP.NET uygulaması alma hakkında bilgi."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/09/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: c22b8ef4866fe2f1ae32c7cb9158fc7866788b26
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="6e1cf-103">Azure SQL veritabanı ile bir ASP.NET uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e1cf-103">Build an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="6e1cf-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="6e1cf-105">Bu öğreticide, bir veri tabanlı ASP.NET web uygulamasını Azure dağıtmak ve buna bağlanmak nasıl gösterilir [Azure SQL veritabanı](../sql-database/sql-database-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6e1cf-105">This tutorial shows you how to deploy a data-driven ASP.NET web app in Azure and connect it to [Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span></span> <span data-ttu-id="6e1cf-106">İşiniz bittiğinde, çalışır durumda bir ASP.NET uygulamanız [Azure App Service](../app-service/app-service-value-prop-what-is.md) ve SQL veritabanına bağlı.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-106">When you're finished, you have a ASP.NET app running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected to SQL Database.</span></span>

![Azure web uygulamasında yayımlanan ASP.NET uygulaması](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="6e1cf-108">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="6e1cf-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6e1cf-109">Azure SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e1cf-109">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="6e1cf-110">Bir ASP.NET uygulaması SQL veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="6e1cf-110">Connect an ASP.NET app to SQL Database</span></span>
> * <span data-ttu-id="6e1cf-111">Uygulamayı Azure'a dağıtma</span><span class="sxs-lookup"><span data-stu-id="6e1cf-111">Deploy the app to Azure</span></span>
> * <span data-ttu-id="6e1cf-112">Veri modeli güncelleştirme ve uygulamayı yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="6e1cf-112">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="6e1cf-113">Azure akış günlükleri, terminal</span><span class="sxs-lookup"><span data-stu-id="6e1cf-113">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="6e1cf-114">Azure portalında uygulama yönetme</span><span class="sxs-lookup"><span data-stu-id="6e1cf-114">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e1cf-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6e1cf-115">Prerequisites</span></span>

<span data-ttu-id="6e1cf-116">Bu öğreticiyi tamamlamak için:</span><span class="sxs-lookup"><span data-stu-id="6e1cf-116">To complete this tutorial:</span></span>

* <span data-ttu-id="6e1cf-117">[Visual Studio 2017](https://www.visualstudio.com/downloads/)’yi aşağıdaki iş yükleri ile yükleyin:</span><span class="sxs-lookup"><span data-stu-id="6e1cf-117">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span></span>
  - <span data-ttu-id="6e1cf-118">**ASP.NET ve web geliştirme**</span><span class="sxs-lookup"><span data-stu-id="6e1cf-118">**ASP.NET and web development**</span></span>
  - <span data-ttu-id="6e1cf-119">**Azure geliştirme**</span><span class="sxs-lookup"><span data-stu-id="6e1cf-119">**Azure development**</span></span>

  ![ASP.NET ve web geliştirme ile Azure geliştirme (Web ve Bulut altında)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample"></a><span data-ttu-id="6e1cf-121">Örneği indirme</span><span class="sxs-lookup"><span data-stu-id="6e1cf-121">Download the sample</span></span>

<span data-ttu-id="6e1cf-122">[Örnek Proje indirme](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="6e1cf-122">[Download the sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>

<span data-ttu-id="6e1cf-123">Extract (sıkıştırmasını açın) *dotnet-sqldb-öğretici-master.zip* dosya.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-123">Extract (unzip) the  *dotnet-sqldb-tutorial-master.zip* file.</span></span>

<span data-ttu-id="6e1cf-124">Temel bir örnek proje içeren [ASP.NET MVC](https://www.asp.net/mvc) CRUD (Oluştur-okunur-güncelleştirme-Sil) uygulamasını kullanarak [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="6e1cf-124">The sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-the-app"></a><span data-ttu-id="6e1cf-125">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="6e1cf-125">Run the app</span></span>

<span data-ttu-id="6e1cf-126">Açık *dotnet-sqldb-öğretici-ana/DotNetAppSqlDb.sln* dosyasını Visual Studio'da.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-126">Open the *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span></span> 

<span data-ttu-id="6e1cf-127">Tür `Ctrl+F5` hata ayıklama olmadan uygulamayı çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-127">Type `Ctrl+F5` to run the app without debugging.</span></span> <span data-ttu-id="6e1cf-128">Uygulamanın varsayılan tarayıcınızda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-128">The app is displayed in your default browser.</span></span> <span data-ttu-id="6e1cf-129">Seçin **Yeni Oluştur** bağlayın ve birkaç oluşturun *Yapılacaklar* öğeleri.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-129">Select the **Create New** link and create a couple *to-do* items.</span></span> 

![Yeni ASP.NET Projesi iletişim kutusu](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="6e1cf-131">Test **Düzenle**, **ayrıntıları**, ve **silmek** bağlantılar.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-131">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="6e1cf-132">Uygulama, veritabanı ile bağlantı için bir veritabanı bağlamını kullanır.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-132">The app uses a database context to connect with the database.</span></span> <span data-ttu-id="6e1cf-133">Bu örnekte, veritabanı bağlamı adlı bir bağlantı dizesi kullanır `MyDbConnection`.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-133">In this sample, the database context uses a connection string named `MyDbConnection`.</span></span> <span data-ttu-id="6e1cf-134">Bağlantı dizesi kümesinde *Web.config* dosya ve başvurulan *Models/MyDatabaseContext.cs* dosya.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-134">The connection string is set in the *Web.config* file and referenced in the *Models/MyDatabaseContext.cs* file.</span></span> <span data-ttu-id="6e1cf-135">Bağlantı dizesi adı daha sonra öğreticide, Azure web uygulaması bir Azure SQL veritabanına bağlanmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-135">The connection string name is used later in the tutorial to connect the Azure web app to an Azure SQL Database.</span></span> 

## <a name="publish-to-azure-with-sql-database"></a><span data-ttu-id="6e1cf-136">Azure SQL veritabanı ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="6e1cf-136">Publish to Azure with SQL Database</span></span>

<span data-ttu-id="6e1cf-137">İçinde **Çözüm Gezgini**, sağ tıklatın, **DotNetAppSqlDb** proje ve seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-137">In the **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![Çözüm Gezgini'nden yayımlama](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="6e1cf-139">**Microsoft Azure App Service**’in seçili olduğundan emin olup **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-139">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![Projeye genel bakış sayfasından yayımlama](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="6e1cf-141">Açılır yayımlama **App Service Oluştur** iletişim kutusu, Azure'da ASP.NET web uygulamanızı çalıştırmak için gereken tüm Azure kaynaklarına oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-141">Publishing opens the **Create App Service** dialog, which helps you create all the Azure resources you need to run your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="6e1cf-142">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="6e1cf-142">Sign in to Azure</span></span>

<span data-ttu-id="6e1cf-143">**App Service Oluştur** iletişim kutusunda **Hesap ekle**’ye tıklayın ve ardından Azure aboneliğinizde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-143">In the **Create App Service** dialog, click **Add an account**, and then sign in to your Azure subscription.</span></span> <span data-ttu-id="6e1cf-144">Bir Microsoft hesabında zaten oturum açtıysanız hesabın Azure aboneliğinizi barındırdığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-144">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="6e1cf-145">Oturum açtığınız Microsoft hesabında Azure aboneliğiniz yoksa, doğru hesabı eklemek için tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-145">If the signed-in Microsoft account doesn't have your Azure subscription, click it to add the correct account.</span></span>
   
![Azure'da oturum açma](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

<span data-ttu-id="6e1cf-147">Oturum açtıktan sonra bu iletişim kutusunda Azure web uygulamanız için gereken tüm kaynakları oluşturmaya hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-147">Once signed in, you're ready to create all the resources you need for your Azure web app in this dialog.</span></span>

### <a name="configure-the-web-app-name"></a><span data-ttu-id="6e1cf-148">Web uygulaması adını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6e1cf-148">Configure the web app name</span></span>

<span data-ttu-id="6e1cf-149">Oluşturulan web uygulaması adı tutun veya için başka bir benzersiz adını değiştirin (geçerli karakterler `a-z`, `0-9`, ve `-`).</span><span class="sxs-lookup"><span data-stu-id="6e1cf-149">You can keep the generated web app name, or change it to another unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="6e1cf-150">Web uygulaması adı varsayılan URL bir parçası olarak uygulamanız için kullanılır (`<app_name>.azurewebsites.net`, burada `<app_name>` web uygulaması adınız).</span><span class="sxs-lookup"><span data-stu-id="6e1cf-150">The web app name is used as part of the default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span></span> <span data-ttu-id="6e1cf-151">Web uygulaması adı Azure tüm uygulamalar arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-151">The web app name needs to be unique across all apps in Azure.</span></span> 

![App service Oluştur iletişim kutusu](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a><span data-ttu-id="6e1cf-153">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e1cf-153">Create a resource group</span></span>

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="6e1cf-154">**Kaynak Grubu**’nun yanındaki **Yeni** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-154">Next to **Resource Group**, click **New**.</span></span>

![Kaynak grubu yanında, yeni'yi tıklatın.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

<span data-ttu-id="6e1cf-156">Kaynak grubu adı **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-156">Name the resource group **myResourceGroup**.</span></span>

> [!NOTE]
> <span data-ttu-id="6e1cf-157">' A tıklamayın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-157">Do not click **Create**.</span></span> <span data-ttu-id="6e1cf-158">Önce bir SQL veritabanı sonraki adımda ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-158">You first need to set up a SQL Database in a later step.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="6e1cf-159">App Service planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e1cf-159">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="6e1cf-160">**App Service Planı**’nın yanındaki **Yeni** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-160">Next to **App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="6e1cf-161">**App Service Planını Yapılandır** iletişim kutusunda yeni App Service planını aşağıdaki ayarlarla yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="6e1cf-161">In the **Configure App Service Plan** dialog, configure the new App Service plan with the following settings:</span></span>

![App Service planı oluşturma](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| <span data-ttu-id="6e1cf-163">Ayar</span><span class="sxs-lookup"><span data-stu-id="6e1cf-163">Setting</span></span>  | <span data-ttu-id="6e1cf-164">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="6e1cf-164">Suggested value</span></span> | <span data-ttu-id="6e1cf-165">Daha fazla bilgi için</span><span class="sxs-lookup"><span data-stu-id="6e1cf-165">For more information</span></span> |
| ----------------- | ------------ | ----|
|<span data-ttu-id="6e1cf-166">**Uygulama hizmeti planı**</span><span class="sxs-lookup"><span data-stu-id="6e1cf-166">**App Service Plan**</span></span>| <span data-ttu-id="6e1cf-167">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="6e1cf-167">myAppServicePlan</span></span> | [<span data-ttu-id="6e1cf-168">App Service planları</span><span class="sxs-lookup"><span data-stu-id="6e1cf-168">App Service plans</span></span>](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|<span data-ttu-id="6e1cf-169">**Konum**</span><span class="sxs-lookup"><span data-stu-id="6e1cf-169">**Location**</span></span>| <span data-ttu-id="6e1cf-170">Batı Avrupa</span><span class="sxs-lookup"><span data-stu-id="6e1cf-170">West Europe</span></span> | [<span data-ttu-id="6e1cf-171">Azure bölgeleri</span><span class="sxs-lookup"><span data-stu-id="6e1cf-171">Azure regions</span></span>](https://azure.microsoft.com/regions/) |
|<span data-ttu-id="6e1cf-172">**Boyut**</span><span class="sxs-lookup"><span data-stu-id="6e1cf-172">**Size**</span></span>| <span data-ttu-id="6e1cf-173">Ücretsiz</span><span class="sxs-lookup"><span data-stu-id="6e1cf-173">Free</span></span> | [<span data-ttu-id="6e1cf-174">Fiyatlandırma katmanları</span><span class="sxs-lookup"><span data-stu-id="6e1cf-174">Pricing tiers</span></span>](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="6e1cf-175">SQL Server örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e1cf-175">Create a SQL Server instance</span></span>

<span data-ttu-id="6e1cf-176">Bir veritabanı oluşturmadan önce gereken bir [Azure SQL Database mantıksal sunucusu](../sql-database/sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="6e1cf-176">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span></span> <span data-ttu-id="6e1cf-177">Mantıksal sunucu, grup olarak yönetilen bir veritabanı grubu içerir.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-177">A logical server contains a group of databases managed as a group.</span></span>

<span data-ttu-id="6e1cf-178">Seçin **diğer Azure hizmetlerini keşfedin**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-178">Select **Explore additional Azure services**.</span></span>

![Web uygulaması adını yapılandırma](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

<span data-ttu-id="6e1cf-180">İçinde **Hizmetleri** sekmesini tıklatın,  **+**  yanındaki simge **SQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-180">In the **Services** tab, click the **+** icon next to **SQL Database**.</span></span> 

![Hizmetler sekmesini tıklatın + SQL veritabanı yanındaki simge.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

<span data-ttu-id="6e1cf-182">İçinde **SQL veritabanını yapılandırma** iletişim kutusunda, tıklatın **yeni** yanına **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-182">In the **Configure SQL Database** dialog, click **New** next to **SQL Server**.</span></span> 

<span data-ttu-id="6e1cf-183">Benzersiz sunucu adı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-183">A unique server name is generated.</span></span> <span data-ttu-id="6e1cf-184">Bu ad mantıksal sunucunuz için varsayılan URL bir parçası olarak kullanılır `<server_name>.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-184">This name is used as part of the default URL for your logical server, `<server_name>.database.windows.net`.</span></span> <span data-ttu-id="6e1cf-185">Bunu Azure tüm mantıksal sunucu örnekleri arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-185">It must be unique across all logical server instances in Azure.</span></span> <span data-ttu-id="6e1cf-186">Sunucu adını değiştirmek, ancak bu öğreticide, üretilen değer tutun.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-186">You can change the server name, but for this tutorial, keep the generated value.</span></span>

<span data-ttu-id="6e1cf-187">Bir yönetici kullanıcı adı ve parolayı ekleyin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-187">Add an administrator username and password, and then select **OK**.</span></span> <span data-ttu-id="6e1cf-188">Parola karmaşıklık gereksinimleri için bkz: [parola ilkesi](/sql/relational-databases/security/password-policy).</span><span class="sxs-lookup"><span data-stu-id="6e1cf-188">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span></span>

<span data-ttu-id="6e1cf-189">Bu kullanıcı adı ve parola unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-189">Remember this username and password.</span></span> <span data-ttu-id="6e1cf-190">Mantıksal sunucu örneğini daha sonra yönetmek için gereksinim duyarsınız.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-190">You need them to manage the logical server instance later.</span></span>

![SQL Server örneği oluşturma](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a><span data-ttu-id="6e1cf-192">SQL Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e1cf-192">Create a SQL Database</span></span>

<span data-ttu-id="6e1cf-193">İçinde **SQL veritabanını yapılandırma** iletişim:</span><span class="sxs-lookup"><span data-stu-id="6e1cf-193">In the **Configure SQL Database** dialog:</span></span> 

* <span data-ttu-id="6e1cf-194">Varsayılan olarak oluşturulan tutmak **veritabanı adı**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-194">Keep the default generated **Database Name**.</span></span>
* <span data-ttu-id="6e1cf-195">İçinde **bağlantı dizesi adı**, türü *MyDbConnection*.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-195">In **Connection String Name**, type *MyDbConnection*.</span></span> <span data-ttu-id="6e1cf-196">Bu ad başvuru bağlantı dizesi eşleşmelidir *Models/MyDatabaseContext.cs*.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-196">This name must match the connection string that is referenced in *Models/MyDatabaseContext.cs*.</span></span>
* <span data-ttu-id="6e1cf-197">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-197">Select **OK**.</span></span>

![SQL veritabanını Yapılandır](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

<span data-ttu-id="6e1cf-199">**App Service Oluştur** iletişim oluşturduğunuz kaynakları gösterir.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-199">The **Create App Service** dialog shows the resources you've created.</span></span> <span data-ttu-id="6e1cf-200">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-200">Click **Create**.</span></span> 

![oluşturduğunuz kaynakları](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

<span data-ttu-id="6e1cf-202">Azure kaynaklarını Oluşturma Sihirbazı'nı tamamladıktan sonra ASP.NET uygulamanızı Azure'da yayımlar.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-202">Once the wizard finishes creating the Azure resources, it  publishes your ASP.NET app to Azure.</span></span> <span data-ttu-id="6e1cf-203">Dağıtılan uygulama URL'si ile varsayılan tarayıcı başlatılır.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-203">Your default browser is launched with the URL to the deployed app.</span></span> 

<span data-ttu-id="6e1cf-204">Birkaç Yapılacaklar öğelerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-204">Add a few to-do items.</span></span>

![Azure web uygulamasında yayımlanan ASP.NET uygulaması](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="6e1cf-206">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="6e1cf-206">Congratulations!</span></span> <span data-ttu-id="6e1cf-207">Veri tabanlı ASP.NET uygulamanızı Azure App Service'te çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-207">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="access-the-sql-database-locally"></a><span data-ttu-id="6e1cf-208">Yerel olarak SQL veritabanına erişim</span><span class="sxs-lookup"><span data-stu-id="6e1cf-208">Access the SQL Database locally</span></span>

<span data-ttu-id="6e1cf-209">Visual Studio keşfedin ve yeni SQL veritabanınızı kolayca içinde yönetmenize olanak tanır **SQL Server Nesne Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-209">Visual Studio lets you explore and manage your new SQL Database easily in the **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="6e1cf-210">Bir veritabanı bağlantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e1cf-210">Create a database connection</span></span>

<span data-ttu-id="6e1cf-211">Gelen **Görünüm** menüsünde, select **SQL Server Nesne Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-211">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="6e1cf-212">Üstündeki **SQL Server Nesne Gezgini**, tıklatın **SQL Server Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-212">At the top of **SQL Server Object Explorer**, click the **Add SQL Server** button.</span></span>

### <a name="configure-the-database-connection"></a><span data-ttu-id="6e1cf-213">Veritabanı bağlantısını yapılandır</span><span class="sxs-lookup"><span data-stu-id="6e1cf-213">Configure the database connection</span></span>

<span data-ttu-id="6e1cf-214">İçinde **Bağlan** iletişim kutusunda, genişletin **Azure** düğümü.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-214">In the **Connect** dialog, expand the **Azure** node.</span></span> <span data-ttu-id="6e1cf-215">Tüm SQL veritabanı örnekleri Azure burada listelenir.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-215">All your SQL Database instances in Azure are listed here.</span></span>

<span data-ttu-id="6e1cf-216">Seçin `DotNetAppSqlDb` SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-216">Select the `DotNetAppSqlDb` SQL Database.</span></span> <span data-ttu-id="6e1cf-217">Daha önce oluşturduğunuz bağlantı altındaki otomatik olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-217">The connection you created earlier is automatically filled at the bottom.</span></span>

<span data-ttu-id="6e1cf-218">Daha önce oluşturduğunuz veritabanı yönetici parolasını yazın ve'ı tıklatın **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-218">Type the database administrator password you created earlier and click **Connect**.</span></span>

![Visual Studio'dan veritabanı bağlantısını yapılandır](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="6e1cf-220">İstemci bağlantısı bilgisayarınızdan izin ver</span><span class="sxs-lookup"><span data-stu-id="6e1cf-220">Allow client connection from your computer</span></span>

<span data-ttu-id="6e1cf-221">**Yeni bir güvenlik duvarı kuralı oluşturmak** iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-221">The **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="6e1cf-222">Varsayılan olarak, SQL veritabanı örneğinde bağlantılar Azure web uygulamanızın gibi Azure hizmetlerinden yalnızca izin verir.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-222">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="6e1cf-223">Veritabanınıza bağlanmak için SQL veritabanı örneğinde bir güvenlik duvarı kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-223">To connect to your database, create a firewall rule in the SQL Database instance.</span></span> <span data-ttu-id="6e1cf-224">Güvenlik duvarı kuralını yerel bilgisayarınızın genel IP adresi sağlar.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-224">The firewall rule allows the public IP address of your local computer.</span></span>

<span data-ttu-id="6e1cf-225">İletişim kutusu zaten bilgisayarınızın ortak IP adresi ile doldurulur.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-225">The dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="6e1cf-226">Olduğundan emin olun **my istemci IP'si Ekle** seçilir ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-226">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![SQL veritabanı örneği için güvenlik duvarını ayarlama](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="6e1cf-228">Visual Studio, SQL veritabanı örneği için güvenlik duvarı ayarı oluşturma tamamlandığında, bağlantınızı görünür **SQL Server Nesne Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-228">Once Visual Studio finishes creating the firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="6e1cf-229">Burada, en sık karşılaşılan gerçekleştirebilirsiniz çalışma sorguları gibi veritabanı işlemlerini oluşturma görünümleri ve saklı yordamları ve daha fazla.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-229">Here, you can perform the most common database operations, such as run queries, create views and stored procedures, and more.</span></span> 

<span data-ttu-id="6e1cf-230">Sağ `Todoes` tablo ve seçin **görünüm verilerini**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-230">Right-click on the `Todoes` table and select **View Data**.</span></span> 

![SQL veritabanı nesneleri keşfedin](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a><span data-ttu-id="6e1cf-232">Code First geçişleri uygulamayı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="6e1cf-232">Update app with Code First Migrations</span></span>

<span data-ttu-id="6e1cf-233">Veritabanı ve web uygulamanızda Azure güncelleştirmek için Visual Studio'da alıştığınız araçları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-233">You can use the familiar tools in Visual Studio to update your database and web app in Azure.</span></span> <span data-ttu-id="6e1cf-234">Bu adımda, Code First Migrations Entity Framework veritabanı şemanızı değişiklik ve Azure'da yayımlamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-234">In this step, you use Code First Migrations in Entity Framework to make a change to your database schema and publish it to Azure.</span></span>

<span data-ttu-id="6e1cf-235">Entity Framework Code First Migrations kullanma hakkında daha fazla bilgi için bkz: [Entity Framework 6 kod MVC 5 kullanarak ilk ile çalışmaya başlama](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="6e1cf-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="6e1cf-236">Veri modelinizi güncelleştir</span><span class="sxs-lookup"><span data-stu-id="6e1cf-236">Update your data model</span></span>

<span data-ttu-id="6e1cf-237">Açık _Models\Todo.cs_ Kod düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-237">Open _Models\Todo.cs_ in the code editor.</span></span> <span data-ttu-id="6e1cf-238">Aşağıdaki özellik ekleme `ToDo` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="6e1cf-238">Add the following property to the `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="6e1cf-239">Code First Migrations yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="6e1cf-239">Run Code First Migrations locally</span></span>

<span data-ttu-id="6e1cf-240">Yerel veritabanınızı güncelleştirme yapmak için birkaç komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-240">Run a few commands to make updates to your local database.</span></span> 

<span data-ttu-id="6e1cf-241">Gelen **Araçları** menüsünde tıklatın **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-241">From the **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="6e1cf-242">Paket Yöneticisi konsolu penceresinde Code First geçişleri etkinleştir:</span><span class="sxs-lookup"><span data-stu-id="6e1cf-242">In the Package Manager Console window, enable Code First Migrations:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="6e1cf-243">Bir geçiş ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6e1cf-243">Add a migration:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="6e1cf-244">Yerel veritabanı güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="6e1cf-244">Update the local database:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="6e1cf-245">Tür `Ctrl+F5` uygulamayı çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-245">Type `Ctrl+F5` to run the app.</span></span> <span data-ttu-id="6e1cf-246">Düzenleme, Ayrıntılar, test ve bağlantıları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-246">Test the edit, details, and create links.</span></span>

<span data-ttu-id="6e1cf-247">Uygulama hatasız yüklerse, Code First Migrations başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-247">If the application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="6e1cf-248">Uygulama mantığınızın bu yeni özellik henüz kullanmadığından ancak sayfanızı hala aynı görünür.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-248">However, your page still looks the same because your application logic is not using this new property yet.</span></span> 

### <a name="use-the-new-property"></a><span data-ttu-id="6e1cf-249">Yeni özelliğini kullanın</span><span class="sxs-lookup"><span data-stu-id="6e1cf-249">Use the new property</span></span>

<span data-ttu-id="6e1cf-250">Kodunuzu kullanmak için bazı değişiklikler yapmak `Done` özelliği.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-250">Make some changes in your code to use the `Done` property.</span></span> <span data-ttu-id="6e1cf-251">Bu öğreticide kolaylık olması için yalnızca değiştirme oluşturacağız `Index` ve `Create` görünümleri eylem özelliğine bakın.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-251">For simplicity in this tutorial, you're only going to change the `Index` and `Create` views to see the property in action.</span></span>

<span data-ttu-id="6e1cf-252">Açık _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-252">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="6e1cf-253">Bul `Create()` yöntemi ekleyin `Done` özelliklerinde listesine `Bind` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-253">Find the `Create()` method and add `Done` to the list of properties in the `Bind` attribute.</span></span> <span data-ttu-id="6e1cf-254">İşiniz bittiğinde, `Create()` yöntemi imza aşağıdaki kod gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="6e1cf-254">When you're done, your `Create()` method signature looks like the following code:</span></span>

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="6e1cf-255">Açık _Views\Todos\Create.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-255">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="6e1cf-256">Razor kodunda görmelisiniz bir `<div class="form-group">` kullanan öğesi `model.Description`ve ardından başka bir `<div class="form-group">` kullanan öğesi `model.CreatedDate`.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-256">In the Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span></span> <span data-ttu-id="6e1cf-257">Bu iki öğenin hemen ardından, eklemek başka `<div class="form-group">` kullanan öğesi `model.Done`:</span><span class="sxs-lookup"><span data-stu-id="6e1cf-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span></span>

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

<span data-ttu-id="6e1cf-258">Açık _Views\Todos\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-258">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="6e1cf-259">Boş bir Ara `<th></th>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-259">Search for the empty `<th></th>` element.</span></span> <span data-ttu-id="6e1cf-260">Bu öğe yalnızca aşağıdaki Razor kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6e1cf-260">Just above this element, add the following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="6e1cf-261">Bul `<td>` içeren öğeyi `Html.ActionLink()` yardımcı yöntemler.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-261">Find the `<td>` element that contains the `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="6e1cf-262">Bu öğe yalnızca aşağıdaki Razor kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6e1cf-262">Just above this element, add the following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="6e1cf-263">Tüm değişiklikleri görmek için ihtiyacınız olan `Index` ve `Create` görünümleri.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-263">That's all you need to see the changes in the `Index` and `Create` views.</span></span> 

<span data-ttu-id="6e1cf-264">Tür `Ctrl+F5` uygulamayı çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-264">Type `Ctrl+F5` to run the app.</span></span>

<span data-ttu-id="6e1cf-265">Şimdi Yapılacaklar öğesi ekleyin ve denetleme **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-265">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="6e1cf-266">Ardından, giriş sayfanız tamamlanmış bir öğe olarak gösterilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-266">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="6e1cf-267">Unutmayın `Edit` değil görünümü göster `Done` alan, değişmedi çünkü `Edit` görünümü.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-267">Remember that the `Edit` view doesn't show the `Done` field, because you didn't change the `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="6e1cf-268">Azure'da Code First geçişleri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="6e1cf-268">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="6e1cf-269">Kodunuzu değiştirmek artık göre works veritabanı geçiş dahil olmak üzere, Azure web uygulamanızı yayınlama ve SQL veritabanınızı Code First Migrations ile çok güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-269">Now that your code change works, including database migration, you publish it to your Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="6e1cf-270">Tıpkı, projenize sağ tıklayın ve önce seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-270">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="6e1cf-271">Tıklatın **ayarları** yayımlama sihirbazını açın.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-271">Click **Settings** to open the publish wizard.</span></span>

![Açık yayımlama ayarları](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="6e1cf-273">Sihirbazı'nda tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-273">In the wizard, click **Next**.</span></span>

<span data-ttu-id="6e1cf-274">SQL veritabanı bağlantı dizesi içinde doldurulur emin olun **MyDatabaseContext (MyDbConnection)**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-274">Make sure that the connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="6e1cf-275">Seçmek için gerek duyabileceğiniz **myToDoAppDb** veritabanından açılır.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-275">You may need to select the **myToDoAppDb** database from the dropdown.</span></span> 

<span data-ttu-id="6e1cf-276">Seçin **yürütme önce kod uygulamalı geçişler (uygulama başlatılırken çalışır)**, ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![Azure web uygulamasında Code First geçişleri etkinleştir](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="6e1cf-278">Yaptığınız değişiklikleri yayımlama</span><span class="sxs-lookup"><span data-stu-id="6e1cf-278">Publish your changes</span></span>

<span data-ttu-id="6e1cf-279">Azure web uygulamanızda Code First Migrations etkinleştirildi, kod değişikliklerinizin yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span></span>

<span data-ttu-id="6e1cf-280">Yayımlama sayfasında **Yayımla**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-280">In the publish page, click **Publish**.</span></span>

<span data-ttu-id="6e1cf-281">Yapılacaklar öğelerini yeniden eklemeyi deneyin ve seçin **Bitti**, ve bunlar sayfanız tamamlanmış bir öğe olarak içinde gösterilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![Kod ilk geçişten sonra Azure web uygulaması](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="6e1cf-283">Tüm mevcut Yapılacaklar öğelerini hala görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-283">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="6e1cf-284">ASP.NET uygulamanızı yayımladığınızda, SQL veritabanında var olan veri kaybı olmadığından.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="6e1cf-285">Ayrıca, Code First Migrations yalnızca veri şemasını değiştirir ve varolan verilerinizi dokunmaz.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-285">Also, Code First Migrations only changes the data schema and leaves your existing data intact.</span></span>


## <a name="stream-application-logs"></a><span data-ttu-id="6e1cf-286">Akış uygulama günlükleri</span><span class="sxs-lookup"><span data-stu-id="6e1cf-286">Stream application logs</span></span>

<span data-ttu-id="6e1cf-287">İzleme iletileri doğrudan Azure web uygulamasından Visual Studio'ya akışını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-287">You can stream tracing messages directly from your Azure web app to Visual Studio.</span></span>

<span data-ttu-id="6e1cf-288">Açık _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-288">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="6e1cf-289">Her eylem ile başlayan bir `Trace.WriteLine()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-289">Each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="6e1cf-290">Bu kod, Azure web uygulamanızın izleme iletileri ekleme göstermek için eklenir.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-290">This code is added to show you how to add trace messages to your Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="6e1cf-291">Açık Sunucu Gezgini</span><span class="sxs-lookup"><span data-stu-id="6e1cf-291">Open Server Explorer</span></span>

<span data-ttu-id="6e1cf-292">Gelen **Görünüm** menüsünde, select **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-292">From the **View** menu, select **Server Explorer**.</span></span> <span data-ttu-id="6e1cf-293">Azure web uygulamanız için günlük kaydını yapılandırmak **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-293">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

### <a name="enable-log-streaming"></a><span data-ttu-id="6e1cf-294">Günlük akışı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="6e1cf-294">Enable log streaming</span></span>

<span data-ttu-id="6e1cf-295">İçinde **Sunucu Gezgini**, genişletin **Azure** > **uygulama hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-295">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="6e1cf-296">Genişletme **myResourceGroup** kaynak grubu, oluşturduğunuz ilk Azure web uygulaması oluşturduğunuzda.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-296">Expand the **myResourceGroup** resource group, you created when you first created the Azure web app.</span></span>

<span data-ttu-id="6e1cf-297">Azure web uygulamanızın sağ tıklatıp **akış günlüklerini görüntüle**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-297">Right-click your Azure web app and select **View Streaming Logs**.</span></span>

![Günlük akışı etkinleştir](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="6e1cf-299">Günlükleri şimdi içine akışı **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-299">The logs are now streamed into the **Output** window.</span></span> 

![Çıktı penceresinde akış günlük](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="6e1cf-301">Bununla birlikte, izleme iletilerini henüz görmüyorsanız.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-301">However, you don't see any of the trace messages yet.</span></span> <span data-ttu-id="6e1cf-302">Bu ilk seçtiğinizde, çünkü **akış günlüklerini görüntüle**, Azure web uygulamanızı izleme düzeyini ayarlar `Error`, hangi yalnızca günlükleri hata olayları (ile `Trace.TraceError()` yöntemi).</span><span class="sxs-lookup"><span data-stu-id="6e1cf-302">That's because when you first select **View Streaming Logs**, your Azure web app sets the trace level to `Error`, which only logs error events (with the `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="6e1cf-303">Değişiklik izleme düzeyi</span><span class="sxs-lookup"><span data-stu-id="6e1cf-303">Change trace levels</span></span>

<span data-ttu-id="6e1cf-304">Diğer izleme iletilerini çıktısını almak için izleme düzeyi değiştirmek için geri dönüp **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-304">To change the trace levels to output other trace messages, go back to **Server Explorer**.</span></span>

<span data-ttu-id="6e1cf-305">Azure web uygulamanızı yeniden sağ tıklatıp **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-305">Right-click your Azure web app again and select **Settings**.</span></span>

<span data-ttu-id="6e1cf-306">İçinde **uygulama günlüğü (dosya sistemi)** açılan listesinde, select **ayrıntılı**.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-306">In the **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="6e1cf-307">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-307">Click **Save**.</span></span>

![Verbose için değişiklik izleme düzeyi](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="6e1cf-309">Ne tür iletileri her düzeyi için görüntülenen görmek için farklı izleme düzeyleri ile deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-309">You can experiment with different trace levels to see what types of messages are displayed for each level.</span></span> <span data-ttu-id="6e1cf-310">Örneğin, **bilgi** düzeyi tarafından oluşturulan tüm günlükleri içeren `Trace.TraceInformation()`, `Trace.TraceWarning()`, ve `Trace.TraceError()`, ancak tarafından oluşturulan günlükleri `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-310">For example, the **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="6e1cf-311">Tarayıcınızda, yapılacaklar listesi uygulaması Azure geçici tıklatmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-311">In your browser, try clicking around the to-do list application in Azure.</span></span> <span data-ttu-id="6e1cf-312">İzleme iletileri şimdi akışı **çıkış** Visual Studio'daki.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-312">The trace messages are now streamed to the **Output** window in Visual Studio.</span></span>

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a><span data-ttu-id="6e1cf-313">Akış Günlüğü Durdur</span><span class="sxs-lookup"><span data-stu-id="6e1cf-313">Stop log streaming</span></span>

<span data-ttu-id="6e1cf-314">Günlük akış hizmetini durdurmak için tıklatın **izlemeyi durdurmak** düğmesini **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-314">To stop the log-streaming service, click the **Stop monitoring** button in the **Output** window.</span></span>

![Akış Günlüğü Durdur](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="6e1cf-316">Azure web uygulamanızı yönetme</span><span class="sxs-lookup"><span data-stu-id="6e1cf-316">Manage your Azure web app</span></span>

<span data-ttu-id="6e1cf-317">Git [Azure portal](https://portal.azure.com) oluşturduğunuz web uygulaması görmek için.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-317">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span> 



<span data-ttu-id="6e1cf-318">Sol menüden **App Service**’e ve ardından Azure web uygulamanızın adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-318">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![Portaldan Azure web uygulamasına gitme](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="6e1cf-320">Web uygulamanızın sayfasında indiniz.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-320">You have landed in your web app's page.</span></span> 

<span data-ttu-id="6e1cf-321">Varsayılan olarak, portal gösterir **genel bakış** sayfası.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-321">By default, the portal shows the **Overview** page.</span></span> <span data-ttu-id="6e1cf-322">Bu sayfa, uygulamanızın nasıl çalıştığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-322">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="6e1cf-323">Buradan ayrıca göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="6e1cf-324">Sayfanın sol tarafında sekmeleri açabilir farklı yapılandırma sayfalarında gösterilir.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-324">The tabs on the left side of the page show the different configuration pages you can open.</span></span> 

![Azure portalında App Service sayfası](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="6e1cf-326">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6e1cf-326">Next steps</span></span>

<span data-ttu-id="6e1cf-327">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="6e1cf-327">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6e1cf-328">Azure SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e1cf-328">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="6e1cf-329">Bir ASP.NET uygulaması SQL veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="6e1cf-329">Connect an ASP.NET app to SQL Database</span></span>
> * <span data-ttu-id="6e1cf-330">Uygulamayı Azure'a dağıtma</span><span class="sxs-lookup"><span data-stu-id="6e1cf-330">Deploy the app to Azure</span></span>
> * <span data-ttu-id="6e1cf-331">Veri modeli güncelleştirme ve uygulamayı yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="6e1cf-331">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="6e1cf-332">Azure akış günlükleri, terminal</span><span class="sxs-lookup"><span data-stu-id="6e1cf-332">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="6e1cf-333">Azure portalında uygulama yönetme</span><span class="sxs-lookup"><span data-stu-id="6e1cf-333">Manage the app in the Azure portal</span></span>

<span data-ttu-id="6e1cf-334">Web uygulaması için özel bir DNS adı eşleme öğrenmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="6e1cf-334">Advance to the next tutorial to learn how to map a custom DNS name to the web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6e1cf-335">Mevcut bir özel DNS adını Azure Web Apps ile eşleme</span><span class="sxs-lookup"><span data-stu-id="6e1cf-335">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
