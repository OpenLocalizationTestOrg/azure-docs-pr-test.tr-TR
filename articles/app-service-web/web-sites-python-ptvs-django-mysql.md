---
title: "aaaDjango ve Visual Studio için Python araçları 2.2 ile azure'da MySQL"
description: "Nasıl toouse hello Python araçları Visual Studio toocreate için bir MySQL veritabanı örneğinde veri depolayan bir Django web uygulaması öğrenin ve tooAzure App Service Web Apps dağıtın."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: c60a50b5-8b5e-4818-a442-16362273dabb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1597c391d20c8e8ef629b4e4d05c9eb64c83bffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="50991-103">Visual Studio için Python Araçları 2.2 ile Azure’da Django ve MySQL</span><span class="sxs-lookup"><span data-stu-id="50991-103">Django and MySQL on Azure with Python Tools 2.2 for Visual Studio</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="50991-104">Bu öğreticide kullanacaksınız [Visual Studio için Python Araçları](https://www.visualstudio.com/vs/python) toocreate basit bir web uygulamasına hello PTVS örnek şablonlarından birini kullanarak yoklar.</span><span class="sxs-lookup"><span data-stu-id="50991-104">In this tutorial, you'll use [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="50991-105">Nasıl toouse MySQL hizmeti Azure üzerinde barındırılan, nasıl tooconfigure hello web uygulama toouse MySQL ve nasıl toopublish hello web uygulaması çok öğreneceksiniz[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="50991-105">You'll learn how toouse a MySQL service hosted on Azure, how tooconfigure hello web app toouse MySQL, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

> [!NOTE]
> <span data-ttu-id="50991-106">Bu öğreticide yer alan hello bilgi de video aşağıdaki hello bulunmaktadır:</span><span class="sxs-lookup"><span data-stu-id="50991-106">hello information contained in this tutorial is also available in hello following video:</span></span>
> 
> <span data-ttu-id="50991-107">[PTVS 2.1: MySQL ile Django uygulaması][video]</span><span class="sxs-lookup"><span data-stu-id="50991-107">[PTVS 2.1: Django app with MySQL][video]</span></span>
> 
> 

<span data-ttu-id="50991-108">Merhaba bkz [Python Geliştirici Merkezi] Bottle kullanarak PTVS ile Azure App Service Web Apps geliştirmeyi kapsayan diğer makaleler için Flask ve Django web altyapılarını Azure Table Storage, MySQL ve SQL Database hizmetleriyle.</span><span class="sxs-lookup"><span data-stu-id="50991-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL, and SQL Database services.</span></span> <span data-ttu-id="50991-109">Bu makale App Service'e odaklanmakla birlikte hello adımlar geliştirirken benzer [Azure Cloud Services].</span><span class="sxs-lookup"><span data-stu-id="50991-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50991-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="50991-110">Prerequisites</span></span>
* <span data-ttu-id="50991-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="50991-111">Visual Studio 2015</span></span>
* <span data-ttu-id="50991-112">[Python 2.7 32 bit] veya [Python 3.4 32 bit]</span><span class="sxs-lookup"><span data-stu-id="50991-112">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>
* <span data-ttu-id="50991-113">[Visual Studio için Python Araçları 2.2]</span><span class="sxs-lookup"><span data-stu-id="50991-113">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="50991-114">[Visual Studio Örnekleri VSIX için Python araçları 2.2]</span><span class="sxs-lookup"><span data-stu-id="50991-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="50991-115">[VS 2015 için Azure SDK Araçları]</span><span class="sxs-lookup"><span data-stu-id="50991-115">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="50991-116">Django 1.9 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="50991-116">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of hello hello previous include. -->

> [!NOTE]
> <span data-ttu-id="50991-117">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50991-117">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="50991-118">Kredi kartı ve taahhüt gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="50991-118">No credit card is required, and no commitments are necessary.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="50991-119">Başlangıç projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="50991-119">Create hello Project</span></span>
<span data-ttu-id="50991-120">Bu bölümde, örnek şablonu kullanarak bir Visual Studio projesi oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="50991-120">In this section, you'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="50991-121">Bir sanal ortam oluşturacak ve gerekli paketleri yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="50991-121">You'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="50991-122">Sqlite kullanarak yerel bir veritabanı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="50991-122">You'll create a local database using sqlite.</span></span> <span data-ttu-id="50991-123">Ardından hello uygulamayı yerel olarak çalışacaksınız.</span><span class="sxs-lookup"><span data-stu-id="50991-123">Then you'll run hello application locally.</span></span>

1. <span data-ttu-id="50991-124">Visual Studio'da, **Dosya**, **Yeni Proje**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="50991-124">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="50991-125">Proje şablonlarını hello hello [Visual Studio Örnekleri VSIX için Python araçları 2.2] altında kullanılabilir **Python**, **örnekleri**.</span><span class="sxs-lookup"><span data-stu-id="50991-125">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="50991-126">Seçin **yoklamalar Django Web projesi** ve Tamam toocreate hello proje'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="50991-126">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>
   
    ![Yeni Proje İletişim Kutusu](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. <span data-ttu-id="50991-128">İstendiğinde tooinstall dış paketler olacaktır.</span><span class="sxs-lookup"><span data-stu-id="50991-128">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="50991-129">**Sanal bir ortama yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="50991-129">Select **Install into a virtual environment**.</span></span>
   
    ![Dış Paketler İletişim Kutusu](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="50991-131">Seçin **Python 2.7** veya **Python 3.4** hello temel yorumlayıcı olarak.</span><span class="sxs-lookup"><span data-stu-id="50991-131">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
    ![Sanal Ortama Ekle İletişim Kutusu](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="50991-133">İçinde **Çözüm Gezgini**, hello proje düğümüne sağ tıklayın ve seçin **Python**ve ardından **Django geçirmek**.</span><span class="sxs-lookup"><span data-stu-id="50991-133">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="50991-134">Ardından **Django Yetkili Kullanıcısı Oluşturma**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="50991-134">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="50991-135">Bu, Django yönetim konsolunu açın ve hello proje klasöründe bir sqlite veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="50991-135">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="50991-136">Merhaba istemleri toocreate kullanıcı izleyin.</span><span class="sxs-lookup"><span data-stu-id="50991-136">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="50991-137">Merhaba uygulaması tuşlarına basarak çalıştığını onaylayın `F5`.</span><span class="sxs-lookup"><span data-stu-id="50991-137">Confirm that hello application works by pressing `F5`.</span></span>
8. <span data-ttu-id="50991-138">Tıklatın **oturum** hello gezinti çubuğunda hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="50991-138">Click **Log in** from hello navigation bar at hello top.</span></span>
   
    ![Django Gezinti Çubuğu](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="50991-140">Hello veritabanını eşitlediğinizde, oluşturduğunuz hello kullanıcı için Hello kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="50991-140">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>
   
    ![Oturum Açma Formu](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="50991-142">**Örnek Yoklamalar Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="50991-142">Click **Create Sample Polls**.</span></span>
    
     ![Örnek Yoklamalar Oluştur](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="50991-144">Bir yoklamaya tıklayın ve oy verin.</span><span class="sxs-lookup"><span data-stu-id="50991-144">Click on a poll and vote.</span></span>
    
     ![Örnek Yoklamalarda Oy Verme](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a><span data-ttu-id="50991-146">MySQL Veritabanı Oluşturma</span><span class="sxs-lookup"><span data-stu-id="50991-146">Create a MySQL Database</span></span>
<span data-ttu-id="50991-147">Merhaba veritabanı için Azure'da ClearDB MySQL barındırılan veritabanı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="50991-147">For hello database, you'll create a ClearDB MySQL hosted database on Azure.</span></span>

<span data-ttu-id="50991-148">Alternatif olarak, Azure'da çalışan kendi sanal makinenizi oluşturabilir ve ardından MySQL’i kendiniz yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50991-148">As an alternative, you can create your own Virtual Machine running in Azure, then install and administer MySQL yourself.</span></span>

<span data-ttu-id="50991-149">Aşağıdaki adımları izleyerek, boş bir plan ile bir veritabanı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50991-149">You can create a database with a free plan by following these steps.</span></span>

1. <span data-ttu-id="50991-150">İçinde toohello oturum [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="50991-150">Log in toohello [Azure Portal].</span></span>
2. <span data-ttu-id="50991-151">Merhaba hello Gezinti bölmesinin üst kısmında tıklatın **yeni**, ardından **veri + depolama**ve ardından **MySQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="50991-151">At hello Top of hello navigation pane, click **NEW**, then click **Data + Storage**, and then click **MySQL Database**.</span></span>
3. <span data-ttu-id="50991-152">Yeni bir kaynak grubu oluşturarak yeni MySQL veritabanı Hello yapılandırın ve hello uygun bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="50991-152">Configure hello new MySQL database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="50991-153">Merhaba MySQL veritabanı oluşturulduktan sonra tıklatın **özellikleri** hello veritabanı dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="50991-153">Once hello MySQL database is created, click **Properties** in hello database blade.</span></span>
5. <span data-ttu-id="50991-154">Merhaba Kopyala düğmesine tooput hello değerini kullanın **bağlantı DİZESİ** hello Panosu'nda.</span><span class="sxs-lookup"><span data-stu-id="50991-154">Use hello copy button tooput hello value of **CONNECTION STRING** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="50991-155">Merhaba projeyi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="50991-155">Configure hello Project</span></span>
<span data-ttu-id="50991-156">Bu bölümde, az önce oluşturduğunuz web uygulaması toouse hello MySQL Veritabanımıza yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="50991-156">In this section, you'll configure our web app toouse hello MySQL database you just created.</span></span> <span data-ttu-id="50991-157">Ek Python paketlerini gerekli toouse MySQL veritabanlarını Django ile de yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="50991-157">You'll also install additional Python packages required toouse MySQL databases with Django.</span></span> <span data-ttu-id="50991-158">Ardından hello web uygulamasını yerel olarak çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="50991-158">Then you'll run hello web app locally.</span></span>

1. <span data-ttu-id="50991-159">Visual Studio'da açın **ProjectName**, hello gelen *ProjectName* klasör.</span><span class="sxs-lookup"><span data-stu-id="50991-159">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="50991-160">Geçici olarak hello Düzenleyicisi'nde hello bağlantı dizesini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="50991-160">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="50991-161">Merhaba bağlantı dizesi bu biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="50991-161">hello connection string is in this format:</span></span>
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    <span data-ttu-id="50991-162">Değişiklik hello varsayılan veritabanı **altyapısı** toouse MySQL ve kümesi hello değerlerini **adı**, **kullanıcı**, **parola** ve  **Ana bilgisayar** hello gelen **CONNECTIONSTRING**.</span><span class="sxs-lookup"><span data-stu-id="50991-162">Change hello default database **ENGINE** toouse MySQL, and set hello values for **NAME**, **USER**, **PASSWORD** and **HOST** from hello **CONNECTIONSTRING**.</span></span>
   
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': '<Database>',
                'USER': '<User Id>',
                'PASSWORD': '<Password>',
                'HOST': '<Data Source>',
                'PORT': '',
            }
        }
2. <span data-ttu-id="50991-163">Çözüm Gezgini'nde, altında **Python ortamları**, hello sanal ortamda sağ tıklayıp **Python paketini Yükle**.</span><span class="sxs-lookup"><span data-stu-id="50991-163">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
3. <span data-ttu-id="50991-164">Merhaba paketini Yükle `mysqlclient` kullanarak **PIP**.</span><span class="sxs-lookup"><span data-stu-id="50991-164">Install hello package `mysqlclient` using **pip**.</span></span>
   
    ![Paketi Yükle İletişim Kutusu](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. <span data-ttu-id="50991-166">İçinde **Çözüm Gezgini**, hello proje düğümüne sağ tıklayın ve seçin **Python**ve ardından **Django geçirmek**.</span><span class="sxs-lookup"><span data-stu-id="50991-166">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="50991-167">Ardından **Django Yetkili Kullanıcısı Oluşturma**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="50991-167">Then select **Django Create Superuser**.</span></span>
   
    <span data-ttu-id="50991-168">Bu hello tablolar için hello önceki bölümde oluşturduğunuz hello MySQL veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="50991-168">This will create hello tables for hello MySQL database you created in hello previous section.</span></span> <span data-ttu-id="50991-169">Merhaba istemleri toocreate toomatch hello kullanıcının bu makalenin hello ilk bölümünde oluşturulan hello sqlite veritabanındaki yoksa bir kullanıcı izleyin.</span><span class="sxs-lookup"><span data-stu-id="50991-169">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section of this article.</span></span>
5. <span data-ttu-id="50991-170">Merhaba uygulamayla çalıştırmak `F5`.</span><span class="sxs-lookup"><span data-stu-id="50991-170">Run hello application with `F5`.</span></span> <span data-ttu-id="50991-171">İle oluşturulan yoklamalar **örnek yoklamalar Oluştur** ve oy vermeyle gönderilen hello veri hello MySQL veritabanında seri.</span><span class="sxs-lookup"><span data-stu-id="50991-171">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello MySQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="50991-172">Yayımlama Hello web uygulama tooAzure uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="50991-172">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="50991-173">Hello Azure .NET SDK'sını kolay bir yolu toodeploy web uygulama tooAzure uygulama hizmeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="50991-173">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="50991-174">İçinde **Çözüm Gezgini**, hello proje düğümüne sağ tıklayın ve seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="50991-174">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
    ![Web Yayımlama İletişim Kutusu](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="50991-176">**Microsoft Azure Uygulama Hizmeti**’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="50991-176">Click on **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="50991-177">Tıklayın **yeni** toocreate yeni bir web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="50991-177">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="50991-178">Hello aşağıdaki alanları doldurun ve **oluşturma**:</span><span class="sxs-lookup"><span data-stu-id="50991-178">Fill in hello following fields and click **Create**:</span></span>
   
   * <span data-ttu-id="50991-179">**Web Uygulaması adı**</span><span class="sxs-lookup"><span data-stu-id="50991-179">**Web App name**</span></span>
   * <span data-ttu-id="50991-180">**App Service planı**</span><span class="sxs-lookup"><span data-stu-id="50991-180">**App Service plan**</span></span>
   * <span data-ttu-id="50991-181">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="50991-181">**Resource group**</span></span>
   * <span data-ttu-id="50991-182">**Bölge**</span><span class="sxs-lookup"><span data-stu-id="50991-182">**Region**</span></span>
   * <span data-ttu-id="50991-183">Bırakın **veritabanı sunucusu** çok ayarlamak**veritabanı yok**</span><span class="sxs-lookup"><span data-stu-id="50991-183">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="50991-184">Diğer tüm varsayılanları kabul edin ve **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="50991-184">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="50991-185">Web tarayıcınız toohello yayımlanan web uygulamasına otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="50991-185">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="50991-186">Hello kullanarak, beklendiği gibi hello web uygulama çalışma görmelisiniz **MySQL** Azure üzerinde barındırılan veritabanı.</span><span class="sxs-lookup"><span data-stu-id="50991-186">You should see hello web app working as expected, using hello **MySQL** database hosted on Azure.</span></span>
   
    ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    <span data-ttu-id="50991-188">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="50991-188">Congratulations!</span></span> <span data-ttu-id="50991-189">MySQL tabanlı web uygulama tooAzure başarıyla yayımladınız.</span><span class="sxs-lookup"><span data-stu-id="50991-189">You have successfully published your MySQL-based web app tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50991-190">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="50991-190">Next steps</span></span>
<span data-ttu-id="50991-191">Visual Studio, Django ve MySQL için Python araçları hakkında daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="50991-191">Follow these links toolearn more about Python Tools for Visual Studio, Django and MySQL.</span></span>

* <span data-ttu-id="50991-192">[Visual Studio için Python Araçları Belgeleri]</span><span class="sxs-lookup"><span data-stu-id="50991-192">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="50991-193">[Web Projeleri]</span><span class="sxs-lookup"><span data-stu-id="50991-193">[Web Projects]</span></span>
  * <span data-ttu-id="50991-194">[Bulut Hizmeti Projeleri]</span><span class="sxs-lookup"><span data-stu-id="50991-194">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="50991-195">[Microsoft Azure’da Uzaktan Hata Ayıklama]</span><span class="sxs-lookup"><span data-stu-id="50991-195">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="50991-196">[Django Belgeleri]</span><span class="sxs-lookup"><span data-stu-id="50991-196">[Django Documentation]</span></span>
* <span data-ttu-id="50991-197">[MySQL]</span><span class="sxs-lookup"><span data-stu-id="50991-197">[MySQL]</span></span>

<span data-ttu-id="50991-198">Daha fazla bilgi için bkz: Merhaba [Python Geliştirici Merkezi](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="50991-198">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

<!--Link references-->

[Python Geliştirici Merkezi]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Azure Portal]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Visual Studio için Python Araçları 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio Örnekleri VSIX için Python araçları 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025
[VS 2015 için Azure SDK Araçları]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517191
[Visual Studio için Python Araçları Belgeleri]: http://aka.ms/ptvsdocs
[Microsoft Azure’da Uzaktan Hata Ayıklama]: http://go.microsoft.com/fwlink/?LinkId=624026
[Web Projeleri]: http://go.microsoft.com/fwlink/?LinkId=624027
[Bulut Hizmeti Projeleri]: http://go.microsoft.com/fwlink/?LinkId=624028
[Django Belgeleri]: https://www.djangoproject.com/
[MySQL]: http://www.mysql.com/
[video]: http://youtu.be/oKCApIrS0Lo
