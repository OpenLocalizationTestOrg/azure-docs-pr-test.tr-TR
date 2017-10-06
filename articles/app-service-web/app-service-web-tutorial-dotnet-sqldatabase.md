---
title: "Azure SQL veritabanı ile ASP.NET uygulamasında aaaBuild | Microsoft Docs"
description: "Bilgi nasıl tooget bir ASP.NET bağlantı tooa SQL veritabanı ile Azure üzerinde çalışan uygulama."
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
ms.openlocfilehash: d21c2bc404bfe038608c17e5a94d96847153002c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="20891-103">Azure SQL veritabanı ile bir ASP.NET uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="20891-103">Build an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="20891-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="20891-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="20891-105">Bu öğretici nasıl toodeploy veri güdümlü bir ASP.NET web uygulamasına ve çok bağlanacağını gösterir[Azure SQL veritabanı](../sql-database/sql-database-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="20891-105">This tutorial shows you how toodeploy a data-driven ASP.NET web app in Azure and connect it too[Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span></span> <span data-ttu-id="20891-106">İşiniz bittiğinde, çalışır durumda bir ASP.NET uygulamanız [Azure App Service](../app-service/app-service-value-prop-what-is.md) ve tooSQL veritabanına bağlı.</span><span class="sxs-lookup"><span data-stu-id="20891-106">When you're finished, you have a ASP.NET app running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected tooSQL Database.</span></span>

![Azure web uygulamasında yayımlanan ASP.NET uygulaması](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="20891-108">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="20891-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="20891-109">Azure SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="20891-109">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="20891-110">Bir ASP.NET uygulaması tooSQL veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="20891-110">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="20891-111">Merhaba uygulama tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="20891-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="20891-112">Merhaba veri modeli güncelleştirmek ve hello uygulama yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="20891-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="20891-113">Azure tooyour terminal akış günlükleri</span><span class="sxs-lookup"><span data-stu-id="20891-113">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="20891-114">Merhaba uygulamada hello Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="20891-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20891-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="20891-115">Prerequisites</span></span>

<span data-ttu-id="20891-116">toocomplete Bu öğretici:</span><span class="sxs-lookup"><span data-stu-id="20891-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="20891-117">Yükleme [Visual Studio 2017](https://www.visualstudio.com/downloads/) iş yükleri aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="20891-117">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello following workloads:</span></span>
  - <span data-ttu-id="20891-118">**ASP.NET ve web geliştirme**</span><span class="sxs-lookup"><span data-stu-id="20891-118">**ASP.NET and web development**</span></span>
  - <span data-ttu-id="20891-119">**Azure geliştirme**</span><span class="sxs-lookup"><span data-stu-id="20891-119">**Azure development**</span></span>

  ![ASP.NET ve web geliştirme ile Azure geliştirme (Web ve Bulut altında)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="20891-121">Merhaba örnek indirme</span><span class="sxs-lookup"><span data-stu-id="20891-121">Download hello sample</span></span>

<span data-ttu-id="20891-122">[Merhaba örnek projesini indirin](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="20891-122">[Download hello sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>

<span data-ttu-id="20891-123">Extract (sıkıştırmasını açın) hello *dotnet-sqldb-öğretici-master.zip* dosya.</span><span class="sxs-lookup"><span data-stu-id="20891-123">Extract (unzip) hello  *dotnet-sqldb-tutorial-master.zip* file.</span></span>

<span data-ttu-id="20891-124">Merhaba örnek projesini içeren temel bir [ASP.NET MVC](https://www.asp.net/mvc) CRUD (Oluştur-okunur-güncelleştirme-Sil) uygulamasını kullanarak [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="20891-124">hello sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-hello-app"></a><span data-ttu-id="20891-125">Merhaba uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="20891-125">Run hello app</span></span>

<span data-ttu-id="20891-126">Açık hello *dotnet-sqldb-öğretici-ana/DotNetAppSqlDb.sln* dosyasını Visual Studio'da.</span><span class="sxs-lookup"><span data-stu-id="20891-126">Open hello *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span></span> 

<span data-ttu-id="20891-127">Tür `Ctrl+F5` hata ayıklama olmadan toorun hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="20891-127">Type `Ctrl+F5` toorun hello app without debugging.</span></span> <span data-ttu-id="20891-128">Merhaba uygulama varsayılan tarayıcınızda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="20891-128">hello app is displayed in your default browser.</span></span> <span data-ttu-id="20891-129">Select hello **Yeni Oluştur** bağlayın ve birkaç oluşturun *Yapılacaklar* öğeleri.</span><span class="sxs-lookup"><span data-stu-id="20891-129">Select hello **Create New** link and create a couple *to-do* items.</span></span> 

![Yeni ASP.NET Projesi iletişim kutusu](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="20891-131">Test hello **Düzenle**, **ayrıntıları**, ve **silmek** bağlantılar.</span><span class="sxs-lookup"><span data-stu-id="20891-131">Test hello **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="20891-132">Merhaba uygulama bir veritabanı bağlamını tooconnect hello veritabanıyla kullanır.</span><span class="sxs-lookup"><span data-stu-id="20891-132">hello app uses a database context tooconnect with hello database.</span></span> <span data-ttu-id="20891-133">Bu örnekte, hello veritabanı bağlamını adlı bir bağlantı dizesi kullanır `MyDbConnection`.</span><span class="sxs-lookup"><span data-stu-id="20891-133">In this sample, hello database context uses a connection string named `MyDbConnection`.</span></span> <span data-ttu-id="20891-134">Merhaba bağlantı dizesi hello ayarlanmış *Web.config* dosya ve başvurulan hello *Models/MyDatabaseContext.cs* dosya.</span><span class="sxs-lookup"><span data-stu-id="20891-134">hello connection string is set in hello *Web.config* file and referenced in hello *Models/MyDatabaseContext.cs* file.</span></span> <span data-ttu-id="20891-135">Merhaba bağlantı dizesi adı daha sonra hello öğretici tooconnect hello Azure web uygulaması tooan Azure SQL veritabanı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="20891-135">hello connection string name is used later in hello tutorial tooconnect hello Azure web app tooan Azure SQL Database.</span></span> 

## <a name="publish-tooazure-with-sql-database"></a><span data-ttu-id="20891-136">SQL veritabanı ile tooAzure yayımlama</span><span class="sxs-lookup"><span data-stu-id="20891-136">Publish tooAzure with SQL Database</span></span>

<span data-ttu-id="20891-137">Merhaba, **Çözüm Gezgini**, sağ tıklatın, **DotNetAppSqlDb** proje ve seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="20891-137">In hello **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![Çözüm Gezgini'nden yayımlama](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="20891-139">**Microsoft Azure App Service**’in seçili olduğundan emin olup **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="20891-139">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![Projeye genel bakış sayfasından yayımlama](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="20891-141">Yayımlama hello açılır **App Service Oluştur** iletişim kutusunda, oluşturduğunuz tüm yardımcı olan hello Azure kaynaklarını azure'da ASP.NET web uygulamanız toorun gerekir.</span><span class="sxs-lookup"><span data-stu-id="20891-141">Publishing opens hello **Create App Service** dialog, which helps you create all hello Azure resources you need toorun your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="20891-142">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="20891-142">Sign in tooAzure</span></span>

<span data-ttu-id="20891-143">Merhaba, **App Service Oluştur** iletişim kutusunda, tıklatın **Hesap Ekle**ve tooyour Azure aboneliği oturum açın.</span><span class="sxs-lookup"><span data-stu-id="20891-143">In hello **Create App Service** dialog, click **Add an account**, and then sign in tooyour Azure subscription.</span></span> <span data-ttu-id="20891-144">Bir Microsoft hesabında zaten oturum açtıysanız hesabın Azure aboneliğinizi barındırdığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="20891-144">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="20891-145">Microsoft hesabı oturum açmış Hello Azure aboneliğiniz yoksa, tooadd hello doğru hesabını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="20891-145">If hello signed-in Microsoft account doesn't have your Azure subscription, click it tooadd hello correct account.</span></span>
   
![İçinde tooAzure oturum](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

<span data-ttu-id="20891-147">Oturum açıldıktan sonra tüm Azure web uygulamanız bu iletişim için gereken kaynakları hello hazır toocreate demektir.</span><span class="sxs-lookup"><span data-stu-id="20891-147">Once signed in, you're ready toocreate all hello resources you need for your Azure web app in this dialog.</span></span>

### <a name="configure-hello-web-app-name"></a><span data-ttu-id="20891-148">Merhaba web uygulaması adını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="20891-148">Configure hello web app name</span></span>

<span data-ttu-id="20891-149">Oluşturulan başlangıç web uygulaması adı tutun veya tooanother benzersiz adını değiştirin (geçerli karakterler `a-z`, `0-9`, ve `-`).</span><span class="sxs-lookup"><span data-stu-id="20891-149">You can keep hello generated web app name, or change it tooanother unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="20891-150">Merhaba web uygulaması adı, uygulamanız için hello varsayılan URL bir parçası olarak kullanılır (`<app_name>.azurewebsites.net`, burada `<app_name>` web uygulaması adınız).</span><span class="sxs-lookup"><span data-stu-id="20891-150">hello web app name is used as part of hello default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span></span> <span data-ttu-id="20891-151">Merhaba web uygulaması adı toobe benzersiz azure'da tüm uygulamalarında gerekir.</span><span class="sxs-lookup"><span data-stu-id="20891-151">hello web app name needs toobe unique across all apps in Azure.</span></span> 

![App service Oluştur iletişim kutusu](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a><span data-ttu-id="20891-153">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="20891-153">Create a resource group</span></span>

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="20891-154">Sonraki çok**kaynak grubu**, tıklatın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="20891-154">Next too**Resource Group**, click **New**.</span></span>

![Sonraki tooResource grubu, yeni tıklayın.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

<span data-ttu-id="20891-156">Ad hello kaynak grubu **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="20891-156">Name hello resource group **myResourceGroup**.</span></span>

> [!NOTE]
> <span data-ttu-id="20891-157">' A tıklamayın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="20891-157">Do not click **Create**.</span></span> <span data-ttu-id="20891-158">Önce bir SQL veritabanını sonraki adımda tooset gerekir.</span><span class="sxs-lookup"><span data-stu-id="20891-158">You first need tooset up a SQL Database in a later step.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="20891-159">App Service planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="20891-159">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="20891-160">Sonraki çok**App Service planı**, tıklatın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="20891-160">Next too**App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="20891-161">Merhaba, **uygulama hizmeti planı yapılandırmak** iletişim kutusunda, ayarları aşağıdaki hello ile Merhaba yeni uygulama hizmeti planını yapılandır:</span><span class="sxs-lookup"><span data-stu-id="20891-161">In hello **Configure App Service Plan** dialog, configure hello new App Service plan with hello following settings:</span></span>

![App Service planı oluşturma](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| <span data-ttu-id="20891-163">Ayar</span><span class="sxs-lookup"><span data-stu-id="20891-163">Setting</span></span>  | <span data-ttu-id="20891-164">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="20891-164">Suggested value</span></span> | <span data-ttu-id="20891-165">Daha fazla bilgi için</span><span class="sxs-lookup"><span data-stu-id="20891-165">For more information</span></span> |
| ----------------- | ------------ | ----|
|<span data-ttu-id="20891-166">**Uygulama hizmeti planı**</span><span class="sxs-lookup"><span data-stu-id="20891-166">**App Service Plan**</span></span>| <span data-ttu-id="20891-167">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="20891-167">myAppServicePlan</span></span> | [<span data-ttu-id="20891-168">App Service planları</span><span class="sxs-lookup"><span data-stu-id="20891-168">App Service plans</span></span>](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|<span data-ttu-id="20891-169">**Konum**</span><span class="sxs-lookup"><span data-stu-id="20891-169">**Location**</span></span>| <span data-ttu-id="20891-170">Batı Avrupa</span><span class="sxs-lookup"><span data-stu-id="20891-170">West Europe</span></span> | [<span data-ttu-id="20891-171">Azure bölgeleri</span><span class="sxs-lookup"><span data-stu-id="20891-171">Azure regions</span></span>](https://azure.microsoft.com/regions/) |
|<span data-ttu-id="20891-172">**Boyut**</span><span class="sxs-lookup"><span data-stu-id="20891-172">**Size**</span></span>| <span data-ttu-id="20891-173">Ücretsiz</span><span class="sxs-lookup"><span data-stu-id="20891-173">Free</span></span> | [<span data-ttu-id="20891-174">Fiyatlandırma katmanları</span><span class="sxs-lookup"><span data-stu-id="20891-174">Pricing tiers</span></span>](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="20891-175">SQL Server örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="20891-175">Create a SQL Server instance</span></span>

<span data-ttu-id="20891-176">Bir veritabanı oluşturmadan önce gereken bir [Azure SQL Database mantıksal sunucusu](../sql-database/sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="20891-176">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span></span> <span data-ttu-id="20891-177">Mantıksal sunucu, grup olarak yönetilen bir veritabanı grubu içerir.</span><span class="sxs-lookup"><span data-stu-id="20891-177">A logical server contains a group of databases managed as a group.</span></span>

<span data-ttu-id="20891-178">Seçin **diğer Azure hizmetlerini keşfedin**.</span><span class="sxs-lookup"><span data-stu-id="20891-178">Select **Explore additional Azure services**.</span></span>

![Web uygulaması adını yapılandırma](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

<span data-ttu-id="20891-180">Merhaba, **Hizmetleri** sekmesini ve ardından hello  **+**  simgesi sonraki çok**SQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="20891-180">In hello **Services** tab, click hello **+** icon next too**SQL Database**.</span></span> 

![Merhaba Hizmetleri, sekmesini Merhaba + simgesi sonraki tooSQL veritabanı.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

<span data-ttu-id="20891-182">Merhaba, **SQL veritabanını yapılandırma** iletişim kutusunda, tıklatın **yeni** sonraki çok**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="20891-182">In hello **Configure SQL Database** dialog, click **New** next too**SQL Server**.</span></span> 

<span data-ttu-id="20891-183">Benzersiz sunucu adı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="20891-183">A unique server name is generated.</span></span> <span data-ttu-id="20891-184">Bu ad hello varsayılan URL bir parçası olarak mantıksal sunucunuz için kullanılan `<server_name>.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="20891-184">This name is used as part of hello default URL for your logical server, `<server_name>.database.windows.net`.</span></span> <span data-ttu-id="20891-185">Bunu Azure tüm mantıksal sunucu örnekleri arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="20891-185">It must be unique across all logical server instances in Azure.</span></span> <span data-ttu-id="20891-186">Merhaba sunucu adını değiştirmek, ancak bu öğretici için oluşturulan hello değeri tutun.</span><span class="sxs-lookup"><span data-stu-id="20891-186">You can change hello server name, but for this tutorial, keep hello generated value.</span></span>

<span data-ttu-id="20891-187">Bir yönetici kullanıcı adı ve parolayı ekleyin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="20891-187">Add an administrator username and password, and then select **OK**.</span></span> <span data-ttu-id="20891-188">Parola karmaşıklık gereksinimleri için bkz: [parola ilkesi](/sql/relational-databases/security/password-policy).</span><span class="sxs-lookup"><span data-stu-id="20891-188">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span></span>

<span data-ttu-id="20891-189">Bu kullanıcı adı ve parola unutmayın.</span><span class="sxs-lookup"><span data-stu-id="20891-189">Remember this username and password.</span></span> <span data-ttu-id="20891-190">Toomanage hello mantıksal sunucusuna gerek daha sonra örneği.</span><span class="sxs-lookup"><span data-stu-id="20891-190">You need them toomanage hello logical server instance later.</span></span>

![SQL Server örneği oluşturma](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a><span data-ttu-id="20891-192">SQL Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="20891-192">Create a SQL Database</span></span>

<span data-ttu-id="20891-193">Merhaba, **SQL veritabanını yapılandırma** iletişim:</span><span class="sxs-lookup"><span data-stu-id="20891-193">In hello **Configure SQL Database** dialog:</span></span> 

* <span data-ttu-id="20891-194">Merhaba varsayılan olarak oluşturulan tutmak **veritabanı adı**.</span><span class="sxs-lookup"><span data-stu-id="20891-194">Keep hello default generated **Database Name**.</span></span>
* <span data-ttu-id="20891-195">İçinde **bağlantı dizesi adı**, türü *MyDbConnection*.</span><span class="sxs-lookup"><span data-stu-id="20891-195">In **Connection String Name**, type *MyDbConnection*.</span></span> <span data-ttu-id="20891-196">Bu ad başvuru hello bağlantı dizesi eşleşmelidir *Models/MyDatabaseContext.cs*.</span><span class="sxs-lookup"><span data-stu-id="20891-196">This name must match hello connection string that is referenced in *Models/MyDatabaseContext.cs*.</span></span>
* <span data-ttu-id="20891-197">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="20891-197">Select **OK**.</span></span>

![SQL veritabanını Yapılandır](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

<span data-ttu-id="20891-199">Merhaba **App Service Oluştur** iletişim oluşturduğunuz hello kaynakları gösterir.</span><span class="sxs-lookup"><span data-stu-id="20891-199">hello **Create App Service** dialog shows hello resources you've created.</span></span> <span data-ttu-id="20891-200">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="20891-200">Click **Create**.</span></span> 

![oluşturduğunuz hello kaynakları](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

<span data-ttu-id="20891-202">Hello Azure kaynakları oluşturma Hello Sihirbazı tamamlandıktan sonra ASP.NET uygulama tooAzure yayımlar.</span><span class="sxs-lookup"><span data-stu-id="20891-202">Once hello wizard finishes creating hello Azure resources, it  publishes your ASP.NET app tooAzure.</span></span> <span data-ttu-id="20891-203">Varsayılan tarayıcı hello URL dağıtılan toohello uygulamayla başlatılır.</span><span class="sxs-lookup"><span data-stu-id="20891-203">Your default browser is launched with hello URL toohello deployed app.</span></span> 

<span data-ttu-id="20891-204">Birkaç Yapılacaklar öğelerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="20891-204">Add a few to-do items.</span></span>

![Azure web uygulamasında yayımlanan ASP.NET uygulaması](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="20891-206">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="20891-206">Congratulations!</span></span> <span data-ttu-id="20891-207">Veri tabanlı ASP.NET uygulamanızı Azure App Service'te çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="20891-207">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="access-hello-sql-database-locally"></a><span data-ttu-id="20891-208">Yerel olarak erişim hello SQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="20891-208">Access hello SQL Database locally</span></span>

<span data-ttu-id="20891-209">Visual Studio keşfedin ve yönetmenize olanak sağlar, yeni SQL veritabanınızı kolayca hello **SQL Server Nesne Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="20891-209">Visual Studio lets you explore and manage your new SQL Database easily in hello **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="20891-210">Bir veritabanı bağlantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="20891-210">Create a database connection</span></span>

<span data-ttu-id="20891-211">Merhaba gelen **Görünüm** menüsünde, select **SQL Server Nesne Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="20891-211">From hello **View** menu, select **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="20891-212">Merhaba üst kısmındaki **SQL Server Nesne Gezgini**, hello tıklatın **SQL Server Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="20891-212">At hello top of **SQL Server Object Explorer**, click hello **Add SQL Server** button.</span></span>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="20891-213">Merhaba veritabanı bağlantısını yapılandır</span><span class="sxs-lookup"><span data-stu-id="20891-213">Configure hello database connection</span></span>

<span data-ttu-id="20891-214">Merhaba, **Bağlan** iletişim kutusunda, hello genişletin **Azure** düğümü.</span><span class="sxs-lookup"><span data-stu-id="20891-214">In hello **Connect** dialog, expand hello **Azure** node.</span></span> <span data-ttu-id="20891-215">Tüm SQL veritabanı örnekleri Azure burada listelenir.</span><span class="sxs-lookup"><span data-stu-id="20891-215">All your SQL Database instances in Azure are listed here.</span></span>

<span data-ttu-id="20891-216">Select hello `DotNetAppSqlDb` SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="20891-216">Select hello `DotNetAppSqlDb` SQL Database.</span></span> <span data-ttu-id="20891-217">daha önce oluşturduğunuz hello bağlantı hello altındaki otomatik olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="20891-217">hello connection you created earlier is automatically filled at hello bottom.</span></span>

<span data-ttu-id="20891-218">Daha önce oluşturduğunuz hello veritabanı yönetici parolasını yazıp tıklatın **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="20891-218">Type hello database administrator password you created earlier and click **Connect**.</span></span>

![Visual Studio'dan veritabanı bağlantısını yapılandır](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="20891-220">İstemci bağlantısı bilgisayarınızdan izin ver</span><span class="sxs-lookup"><span data-stu-id="20891-220">Allow client connection from your computer</span></span>

<span data-ttu-id="20891-221">Merhaba **yeni bir güvenlik duvarı kuralı oluşturmak** iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="20891-221">hello **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="20891-222">Varsayılan olarak, SQL veritabanı örneğinde bağlantılar Azure web uygulamanızın gibi Azure hizmetlerinden yalnızca izin verir.</span><span class="sxs-lookup"><span data-stu-id="20891-222">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="20891-223">tooconnect tooyour veritabanı, hello SQL veritabanı örneğinde bir güvenlik duvarı kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="20891-223">tooconnect tooyour database, create a firewall rule in hello SQL Database instance.</span></span> <span data-ttu-id="20891-224">Merhaba güvenlik duvarı kuralı hello genel IP adresi, yerel bilgisayarınızın sağlar.</span><span class="sxs-lookup"><span data-stu-id="20891-224">hello firewall rule allows hello public IP address of your local computer.</span></span>

<span data-ttu-id="20891-225">Merhaba iletişim zaten bilgisayarınızın ortak IP adresi ile doldurulur.</span><span class="sxs-lookup"><span data-stu-id="20891-225">hello dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="20891-226">Olduğundan emin olun **my istemci IP'si Ekle** seçilir ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="20891-226">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![SQL veritabanı örneği için güvenlik duvarını ayarlama](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="20891-228">Visual Studio, SQL veritabanı örneğinizin hello güvenlik duvarı ayarı oluşturma tamamlandığında, bağlantınızı görünür **SQL Server Nesne Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="20891-228">Once Visual Studio finishes creating hello firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="20891-229">Burada, gerçekleştirebileceğiniz hello en yaygın veritabanı gibi işlemleri çalıştırma sorguları, görünümler ve saklı yordamları ve daha fazla oluşturun.</span><span class="sxs-lookup"><span data-stu-id="20891-229">Here, you can perform hello most common database operations, such as run queries, create views and stored procedures, and more.</span></span> 

<span data-ttu-id="20891-230">Merhaba üzerinde sağ `Todoes` tablo ve seçin **görünüm verilerini**.</span><span class="sxs-lookup"><span data-stu-id="20891-230">Right-click on hello `Todoes` table and select **View Data**.</span></span> 

![SQL veritabanı nesneleri keşfedin](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a><span data-ttu-id="20891-232">Code First geçişleri uygulamayı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="20891-232">Update app with Code First Migrations</span></span>

<span data-ttu-id="20891-233">Veritabanı ve web uygulamanızı Azure'da hello tanıdık araçlar Visual Studio tooupdate de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20891-233">You can use hello familiar tools in Visual Studio tooupdate your database and web app in Azure.</span></span> <span data-ttu-id="20891-234">Bu adımda, Entity Framework toomake bir değişiklik tooyour veritabanı şeması Code First geçişleri kullanın ve tooAzure yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="20891-234">In this step, you use Code First Migrations in Entity Framework toomake a change tooyour database schema and publish it tooAzure.</span></span>

<span data-ttu-id="20891-235">Entity Framework Code First Migrations kullanma hakkında daha fazla bilgi için bkz: [Entity Framework 6 kod MVC 5 kullanarak ilk ile çalışmaya başlama](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="20891-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="20891-236">Veri modelinizi güncelleştir</span><span class="sxs-lookup"><span data-stu-id="20891-236">Update your data model</span></span>

<span data-ttu-id="20891-237">Açık _Models\Todo.cs_ hello Kod düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="20891-237">Open _Models\Todo.cs_ in hello code editor.</span></span> <span data-ttu-id="20891-238">Özellik toohello aşağıdaki hello eklemek `ToDo` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="20891-238">Add hello following property toohello `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="20891-239">Code First Migrations yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="20891-239">Run Code First Migrations locally</span></span>

<span data-ttu-id="20891-240">Birkaç komutları toomake güncelleştirmeleri tooyour yerel veritabanı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="20891-240">Run a few commands toomake updates tooyour local database.</span></span> 

<span data-ttu-id="20891-241">Merhaba gelen **Araçları** menüsünde tıklatın **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="20891-241">From hello **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="20891-242">Hello Paket Yöneticisi konsolu penceresinde, Code First geçişleri etkinleştir:</span><span class="sxs-lookup"><span data-stu-id="20891-242">In hello Package Manager Console window, enable Code First Migrations:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="20891-243">Bir geçiş ekleyin:</span><span class="sxs-lookup"><span data-stu-id="20891-243">Add a migration:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="20891-244">Merhaba yerel veritabanı güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="20891-244">Update hello local database:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="20891-245">Tür `Ctrl+F5` toorun hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="20891-245">Type `Ctrl+F5` toorun hello app.</span></span> <span data-ttu-id="20891-246">Test Merhaba, ayrıntıları düzenlemek ve bağlantıları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="20891-246">Test hello edit, details, and create links.</span></span>

<span data-ttu-id="20891-247">Merhaba uygulaması hatasız yüklerse, Code First Migrations başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="20891-247">If hello application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="20891-248">Ancak, uygulama mantığınızın bu yeni özellik henüz kullanmadığından, sayfa hala görünüyor aynı hello.</span><span class="sxs-lookup"><span data-stu-id="20891-248">However, your page still looks hello same because your application logic is not using this new property yet.</span></span> 

### <a name="use-hello-new-property"></a><span data-ttu-id="20891-249">Merhaba yeni özelliğini kullanın</span><span class="sxs-lookup"><span data-stu-id="20891-249">Use hello new property</span></span>

<span data-ttu-id="20891-250">Kod toouse hello bazı değişiklikler yapmak `Done` özelliği.</span><span class="sxs-lookup"><span data-stu-id="20891-250">Make some changes in your code toouse hello `Done` property.</span></span> <span data-ttu-id="20891-251">Bu öğreticide kolaylık sağlamak için yalnızca toochange hello oluşturacağız `Index` ve `Create` toosee hello özellik eylemi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="20891-251">For simplicity in this tutorial, you're only going toochange hello `Index` and `Create` views toosee hello property in action.</span></span>

<span data-ttu-id="20891-252">Açık _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="20891-252">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="20891-253">Hello bulur `Create()` yöntemi ekleyin `Done` hello özelliklerinde toohello listesi `Bind` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="20891-253">Find hello `Create()` method and add `Done` toohello list of properties in hello `Bind` attribute.</span></span> <span data-ttu-id="20891-254">İşiniz bittiğinde, `Create()` yöntemi imza hello kod aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="20891-254">When you're done, your `Create()` method signature looks like hello following code:</span></span>

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="20891-255">Açık _Views\Todos\Create.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="20891-255">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="20891-256">Hello Razor kodunun, görmelisiniz bir `<div class="form-group">` kullanan öğesi `model.Description`ve ardından başka bir `<div class="form-group">` kullanan öğesi `model.CreatedDate`.</span><span class="sxs-lookup"><span data-stu-id="20891-256">In hello Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span></span> <span data-ttu-id="20891-257">Bu iki öğenin hemen ardından, eklemek başka `<div class="form-group">` kullanan öğesi `model.Done`:</span><span class="sxs-lookup"><span data-stu-id="20891-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span></span>

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

<span data-ttu-id="20891-258">Açık _Views\Todos\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="20891-258">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="20891-259">Merhaba boş Ara `<th></th>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="20891-259">Search for hello empty `<th></th>` element.</span></span> <span data-ttu-id="20891-260">Bu öğe yalnızca Razor kod aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="20891-260">Just above this element, add hello following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="20891-261">Hello bulur `<td>` hello içeren öğeyi `Html.ActionLink()` yardımcı yöntemler.</span><span class="sxs-lookup"><span data-stu-id="20891-261">Find hello `<td>` element that contains hello `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="20891-262">Bu öğe yalnızca Razor kod aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="20891-262">Just above this element, add hello following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="20891-263">Tüm yapmanız gereken hello toosee hello değişiklikleri olan `Index` ve `Create` görünümleri.</span><span class="sxs-lookup"><span data-stu-id="20891-263">That's all you need toosee hello changes in hello `Index` and `Create` views.</span></span> 

<span data-ttu-id="20891-264">Tür `Ctrl+F5` toorun hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="20891-264">Type `Ctrl+F5` toorun hello app.</span></span>

<span data-ttu-id="20891-265">Şimdi Yapılacaklar öğesi ekleyin ve denetleme **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="20891-265">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="20891-266">Ardından, giriş sayfanız tamamlanmış bir öğe olarak gösterilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="20891-266">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="20891-267">Bu hello unutmayın `Edit` görünümü hello Göster değil `Done` alan hello değişmedi çünkü `Edit` görünümü.</span><span class="sxs-lookup"><span data-stu-id="20891-267">Remember that hello `Edit` view doesn't show hello `Done` field, because you didn't change hello `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="20891-268">Azure'da Code First geçişleri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="20891-268">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="20891-269">Kodunuzu değiştirmek works veritabanı geçiş dahil olmak üzere, göre tooyour Azure web uygulaması yayımlama ve SQL veritabanınızı Code First Migrations ile çok güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="20891-269">Now that your code change works, including database migration, you publish it tooyour Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="20891-270">Tıpkı, projenize sağ tıklayın ve önce seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="20891-270">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="20891-271">Tıklatın **ayarları** tooopen hello Yayımla Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="20891-271">Click **Settings** tooopen hello publish wizard.</span></span>

![Açık yayımlama ayarları](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="20891-273">Başlangıç Sihirbazı'nda tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="20891-273">In hello wizard, click **Next**.</span></span>

<span data-ttu-id="20891-274">SQL veritabanınız olarak doldurulur için hello bağlantı dizesini doğrulayın **MyDatabaseContext (MyDbConnection)**.</span><span class="sxs-lookup"><span data-stu-id="20891-274">Make sure that hello connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="20891-275">Tooselect hello gerekebilir **myToDoAppDb** veritabanından hello açılır.</span><span class="sxs-lookup"><span data-stu-id="20891-275">You may need tooselect hello **myToDoAppDb** database from hello dropdown.</span></span> 

<span data-ttu-id="20891-276">Seçin **yürütme önce kod uygulamalı geçişler (uygulama başlatılırken çalışır)**, ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="20891-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![Azure web uygulamasında Code First geçişleri etkinleştir](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="20891-278">Yaptığınız değişiklikleri yayımlama</span><span class="sxs-lookup"><span data-stu-id="20891-278">Publish your changes</span></span>

<span data-ttu-id="20891-279">Azure web uygulamanızda Code First Migrations etkinleştirildi, kod değişikliklerinizin yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="20891-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span></span>

<span data-ttu-id="20891-280">Merhaba, yayımlama sayfası, tıklatın **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="20891-280">In hello publish page, click **Publish**.</span></span>

<span data-ttu-id="20891-281">Yapılacaklar öğelerini yeniden eklemeyi deneyin ve seçin **Bitti**, ve bunlar sayfanız tamamlanmış bir öğe olarak içinde gösterilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="20891-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![Kod ilk geçişten sonra Azure web uygulaması](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="20891-283">Tüm mevcut Yapılacaklar öğelerini hala görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="20891-283">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="20891-284">ASP.NET uygulamanızı yayımladığınızda, SQL veritabanında var olan veri kaybı olmadığından.</span><span class="sxs-lookup"><span data-stu-id="20891-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="20891-285">Ayrıca, Code First Migrations hello veri şeması yalnızca değiştirir ve varolan verilerinizi dokunmaz.</span><span class="sxs-lookup"><span data-stu-id="20891-285">Also, Code First Migrations only changes hello data schema and leaves your existing data intact.</span></span>


## <a name="stream-application-logs"></a><span data-ttu-id="20891-286">Akış uygulama günlükleri</span><span class="sxs-lookup"><span data-stu-id="20891-286">Stream application logs</span></span>

<span data-ttu-id="20891-287">İzleme iletileri doğrudan, Azure web uygulaması tooVisual Studio akışını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20891-287">You can stream tracing messages directly from your Azure web app tooVisual Studio.</span></span>

<span data-ttu-id="20891-288">Açık _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="20891-288">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="20891-289">Her eylem ile başlayan bir `Trace.WriteLine()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="20891-289">Each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="20891-290">Bu kodu tooshow eklenir, nasıl tooyour Azure web uygulaması tooadd izleme iletileri.</span><span class="sxs-lookup"><span data-stu-id="20891-290">This code is added tooshow you how tooadd trace messages tooyour Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="20891-291">Açık Sunucu Gezgini</span><span class="sxs-lookup"><span data-stu-id="20891-291">Open Server Explorer</span></span>

<span data-ttu-id="20891-292">Merhaba gelen **Görünüm** menüsünde, select **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="20891-292">From hello **View** menu, select **Server Explorer**.</span></span> <span data-ttu-id="20891-293">Azure web uygulamanız için günlük kaydını yapılandırmak **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="20891-293">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

### <a name="enable-log-streaming"></a><span data-ttu-id="20891-294">Günlük akışı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="20891-294">Enable log streaming</span></span>

<span data-ttu-id="20891-295">İçinde **Sunucu Gezgini**, genişletin **Azure** > **uygulama hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="20891-295">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="20891-296">Merhaba genişletin **myResourceGroup** kaynak grubu, oluşturduğunuz ilk hello Azure web uygulaması oluşturduğunuzda.</span><span class="sxs-lookup"><span data-stu-id="20891-296">Expand hello **myResourceGroup** resource group, you created when you first created hello Azure web app.</span></span>

<span data-ttu-id="20891-297">Azure web uygulamanızın sağ tıklatıp **akış günlüklerini görüntüle**.</span><span class="sxs-lookup"><span data-stu-id="20891-297">Right-click your Azure web app and select **View Streaming Logs**.</span></span>

![Günlük akışı etkinleştir](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="20891-299">Merhaba günlükleri şimdi hello akışı **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="20891-299">hello logs are now streamed into hello **Output** window.</span></span> 

![Çıktı penceresinde akış günlük](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="20891-301">Ancak, hello izleme iletilerini henüz görmüyorsanız.</span><span class="sxs-lookup"><span data-stu-id="20891-301">However, you don't see any of hello trace messages yet.</span></span> <span data-ttu-id="20891-302">Bu ilk seçtiğinizde, çünkü **akış günlüklerini görüntüle**, Azure web uygulamanızın ayarlar hello izleme düzeyi çok`Error`, hangi yalnızca günlükleri hata olayları (Merhaba ile `Trace.TraceError()` yöntemi).</span><span class="sxs-lookup"><span data-stu-id="20891-302">That's because when you first select **View Streaming Logs**, your Azure web app sets hello trace level too`Error`, which only logs error events (with hello `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="20891-303">Değişiklik izleme düzeyi</span><span class="sxs-lookup"><span data-stu-id="20891-303">Change trace levels</span></span>

<span data-ttu-id="20891-304">toochange hello izleme düzeyleri toooutput gidin diğer izleme iletilerini geri çok**Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="20891-304">toochange hello trace levels toooutput other trace messages, go back too**Server Explorer**.</span></span>

<span data-ttu-id="20891-305">Azure web uygulamanızı yeniden sağ tıklatıp **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="20891-305">Right-click your Azure web app again and select **Settings**.</span></span>

<span data-ttu-id="20891-306">Merhaba, **uygulama günlüğü (dosya sistemi)** açılan listesinde, select **ayrıntılı**.</span><span class="sxs-lookup"><span data-stu-id="20891-306">In hello **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="20891-307">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="20891-307">Click **Save**.</span></span>

![Değişiklik izleme düzeyi tooVerbose](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="20891-309">Ne tür iletileri her düzeyi için görüntülenen farklı izleme düzeyleri toosee ile deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20891-309">You can experiment with different trace levels toosee what types of messages are displayed for each level.</span></span> <span data-ttu-id="20891-310">Örneğin, hello **bilgi** düzeyi tarafından oluşturulan tüm günlükleri içeren `Trace.TraceInformation()`, `Trace.TraceWarning()`, ve `Trace.TraceError()`, ancak tarafından oluşturulan günlükleri `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="20891-310">For example, hello **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="20891-311">Tarayıcınızda, azure'da hello Yapılacaklar listesi uygulaması geçici tıklatmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="20891-311">In your browser, try clicking around hello to-do list application in Azure.</span></span> <span data-ttu-id="20891-312">Merhaba izleme iletilerini şimdi toohello akışı **çıkış** Visual Studio'daki.</span><span class="sxs-lookup"><span data-stu-id="20891-312">hello trace messages are now streamed toohello **Output** window in Visual Studio.</span></span>

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a><span data-ttu-id="20891-313">Akış Günlüğü Durdur</span><span class="sxs-lookup"><span data-stu-id="20891-313">Stop log streaming</span></span>

<span data-ttu-id="20891-314">toostop günlük akış hizmeti Merhaba, hello tıklatın **izlemeyi durdurmak** hello düğmesini **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="20891-314">toostop hello log-streaming service, click hello **Stop monitoring** button in hello **Output** window.</span></span>

![Akış Günlüğü Durdur](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="20891-316">Azure web uygulamanızı yönetme</span><span class="sxs-lookup"><span data-stu-id="20891-316">Manage your Azure web app</span></span>

<span data-ttu-id="20891-317">Toohello Git [Azure portal](https://portal.azure.com) oluşturduğunuz toosee hello web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="20891-317">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span> 



<span data-ttu-id="20891-318">Merhaba sol menüden **uygulama hizmeti**, Azure web uygulamanızın hello adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="20891-318">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![Portal Gezinti tooAzure web uygulaması](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="20891-320">Web uygulamanızın sayfasında indiniz.</span><span class="sxs-lookup"><span data-stu-id="20891-320">You have landed in your web app's page.</span></span> 

<span data-ttu-id="20891-321">Varsayılan olarak, hello portal hello gösterir **genel bakış** sayfası.</span><span class="sxs-lookup"><span data-stu-id="20891-321">By default, hello portal shows hello **Overview** page.</span></span> <span data-ttu-id="20891-322">Bu sayfa, uygulamanızın nasıl çalıştığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="20891-322">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="20891-323">Buradan ayrıca göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20891-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="20891-324">Merhaba sekmeler hello sayfasının sol tarafında hello açabilirsiniz hello farklı yapılandırma sayfaları gösterir.</span><span class="sxs-lookup"><span data-stu-id="20891-324">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span> 

![Azure portalında App Service sayfası](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="20891-326">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="20891-326">Next steps</span></span>

<span data-ttu-id="20891-327">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="20891-327">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="20891-328">Azure SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="20891-328">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="20891-329">Bir ASP.NET uygulaması tooSQL veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="20891-329">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="20891-330">Merhaba uygulama tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="20891-330">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="20891-331">Merhaba veri modeli güncelleştirmek ve hello uygulama yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="20891-331">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="20891-332">Azure tooyour terminal akış günlükleri</span><span class="sxs-lookup"><span data-stu-id="20891-332">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="20891-333">Merhaba uygulamada hello Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="20891-333">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="20891-334">İlerlemek toohello sonraki öğretici toolearn nasıl toomap özel DNS ad toohello web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="20891-334">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="20891-335">Harita bir var olan özel DNS adı tooAzure Web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="20891-335">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
