---
title: "aaaDjango ve Visual Studio için Python araçları 2.2 ile azure'da SQL veritabanı"
description: "Nasıl toouse hello Python araçları Visual Studio toocreate için bir SQL veritabanı örneğinde veri depolayan bir Django web uygulaması öğrenin ve tooAzure App Service Web Apps dağıtın."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="72337-103">Visual Studio için Python Araçları 2.2 ile Azure’da Django ve SQL Veritabanı</span><span class="sxs-lookup"><span data-stu-id="72337-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="72337-104">Bu öğreticide, kullanacağız [Visual Studio için Python Araçları] toocreate basit bir web uygulamasına hello PTVS örnek şablonlarından birini kullanarak yoklar.</span><span class="sxs-lookup"><span data-stu-id="72337-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="72337-105">Bu öğretici olarak da kullanılabilir bir [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span><span class="sxs-lookup"><span data-stu-id="72337-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="72337-106">Biz nasıl toouse bir SQL veritabanı Azure üzerinde barındırılan, nasıl tooconfigure hello web uygulama toouse bir SQL veritabanı ve nasıl toopublish hello web uygulaması çok öğreneceksiniz[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="72337-106">We'll learn how toouse a SQL database hosted on Azure, how tooconfigure hello web app toouse a SQL database, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="72337-107">Merhaba bkz [Python Geliştirici Merkezi] Bottle kullanarak PTVS ile Azure App Service Web Apps geliştirmeyi kapsayan diğer makaleler için Flask ve Django web altyapılarını Azure Table Storage, MySQL ve SQL Database hizmetleriyle.</span><span class="sxs-lookup"><span data-stu-id="72337-107">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="72337-108">Bu makale App Service'e odaklanmakla birlikte hello adımlar geliştirirken benzer [Azure Cloud Services].</span><span class="sxs-lookup"><span data-stu-id="72337-108">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72337-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="72337-109">Prerequisites</span></span>
* <span data-ttu-id="72337-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="72337-110">Visual Studio 2015</span></span>
* <span data-ttu-id="72337-111">[Python 2.7 32 bit]</span><span class="sxs-lookup"><span data-stu-id="72337-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="72337-112">[Visual Studio için Python Araçları 2.2]</span><span class="sxs-lookup"><span data-stu-id="72337-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="72337-113">[Visual Studio Örnekleri VSIX için Python araçları 2.2]</span><span class="sxs-lookup"><span data-stu-id="72337-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="72337-114">[VS 2015 için Azure SDK Araçları]</span><span class="sxs-lookup"><span data-stu-id="72337-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="72337-115">Django 1.9 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="72337-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="72337-116">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72337-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="72337-117">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="72337-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-hello-project"></a><span data-ttu-id="72337-118">Başlangıç projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="72337-118">Create hello Project</span></span>
<span data-ttu-id="72337-119">Bu bölümde, örnek şablonu kullanarak bir Visual Studio projesi oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="72337-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="72337-120">Biz sanal ortam oluşturacak ve gerekli paketleri yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="72337-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="72337-121">Sqlite kullanarak yerel bir veritabanı oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="72337-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="72337-122">Ardından hello web uygulamasını yerel olarak çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="72337-122">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="72337-123">Visual Studio'da, **Dosya**, **Yeni Proje**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="72337-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="72337-124">Proje şablonlarını hello hello [Visual Studio Örnekleri VSIX için Python araçları 2.2] altında kullanılabilir **Python**, **örnekleri**.</span><span class="sxs-lookup"><span data-stu-id="72337-124">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="72337-125">Seçin **yoklamalar Django Web projesi** ve Tamam toocreate hello proje'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="72337-125">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>

     ![Yeni Proje İletişim Kutusu](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="72337-127">İstendiğinde tooinstall dış paketler olacaktır.</span><span class="sxs-lookup"><span data-stu-id="72337-127">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="72337-128">**Sanal bir ortama yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="72337-128">Select **Install into a virtual environment**.</span></span>

     ![Dış Paketler İletişim Kutusu](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="72337-130">Seçin **Python 2.7** hello temel yorumlayıcı olarak.</span><span class="sxs-lookup"><span data-stu-id="72337-130">Select **Python 2.7** as hello base interpreter.</span></span>

     ![Sanal Ortama Ekle İletişim Kutusu](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="72337-132">İçinde **Çözüm Gezgini**, hello proje düğümüne sağ tıklayın ve seçin **Python**ve ardından **Django geçirmek**.</span><span class="sxs-lookup"><span data-stu-id="72337-132">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="72337-133">Ardından **Django Yetkili Kullanıcısı Oluşturma**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="72337-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="72337-134">Bu, Django yönetim konsolunu açın ve hello proje klasöründe bir sqlite veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="72337-134">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="72337-135">Merhaba istemleri toocreate kullanıcı izleyin.</span><span class="sxs-lookup"><span data-stu-id="72337-135">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="72337-136">Merhaba uygulaması tuşlarına basarak çalıştığını onaylayın <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="72337-136">Confirm that hello application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="72337-137">Tıklatın **oturum** hello gezinti çubuğunda hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="72337-137">Click **Log in** from hello navigation bar at hello top.</span></span>

     ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="72337-139">Hello veritabanını eşitlediğinizde, oluşturduğunuz hello kullanıcı için Hello kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="72337-139">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>

     ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="72337-141">**Örnek Yoklamalar Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="72337-141">Click **Create Sample Polls**.</span></span>

      ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="72337-143">Bir yoklamaya tıklayın ve oy verin.</span><span class="sxs-lookup"><span data-stu-id="72337-143">Click on a poll and vote.</span></span>

      ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="72337-145">SQL Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="72337-145">Create a SQL Database</span></span>
<span data-ttu-id="72337-146">Merhaba veritabanı için bir Azure SQL veritabanı oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="72337-146">For hello database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="72337-147">Aşağıdaki adımları izleyerek bir veritabanı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72337-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="72337-148">Merhaba günlüğüne [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="72337-148">Log into hello [Azure Portal].</span></span>
2. <span data-ttu-id="72337-149">Merhaba Gezinti bölmesinin Hello altında tıklatın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="72337-149">At hello bottom of hello navigation pane, click **NEW**.</span></span> <span data-ttu-id="72337-150">, tıklatın **veri + depolama** > **SQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="72337-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="72337-151">Yapılandırma yeni bir kaynak grubu oluşturarak yeni SQL veritabanı hello ve hello uygun bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="72337-151">Configure hello new SQL Database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="72337-152">Merhaba SQL veritabanı oluşturulduktan sonra tıklatın **Visual Studio'da Aç** hello veritabanı dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="72337-152">Once hello SQL Database is created, click **Open in Visual Studio** in hello database blade.</span></span>
5. <span data-ttu-id="72337-153">Tıklatın **güvenlik duvarınızı yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="72337-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="72337-154">Merhaba, **güvenlik duvarı ayarlarını** dikey penceresinde ile güvenlik duvarı kuralı ekleyin **başlangıç IP** ve **bitiş IP** geliştirme makinenizde toohello genel IP adresi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="72337-154">In hello **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set toohello public IP address of your development machine.</span></span> <span data-ttu-id="72337-155">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="72337-155">Click **Save**.</span></span>

   <span data-ttu-id="72337-156">Bu bağlantıları toohello veritabanı geliştirme makinenizde sunucusundan olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="72337-156">This will allow connections toohello database server from your development machine.</span></span>
7. <span data-ttu-id="72337-157">Geri hello veritabanı dikey penceresinde tıklayın **özellikleri**, ardından **veritabanı bağlantı dizelerini Göster**.</span><span class="sxs-lookup"><span data-stu-id="72337-157">Back in hello database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="72337-158">Merhaba Kopyala düğmesine tooput hello değerini kullanın **ADO.NET** hello Panosu'nda.</span><span class="sxs-lookup"><span data-stu-id="72337-158">Use hello copy button tooput hello value of **ADO.NET** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="72337-159">Merhaba projeyi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="72337-159">Configure hello Project</span></span>
<span data-ttu-id="72337-160">Bu bölümde, yeni oluşturduğumuz bizim web uygulama toouse hello SQL veritabanı yapılandıracağız.</span><span class="sxs-lookup"><span data-stu-id="72337-160">In this section, we'll configure our web app toouse hello SQL database we just created.</span></span> <span data-ttu-id="72337-161">Ek Python paketlerini gerekli toouse SQL veritabanlarını da Django ile yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="72337-161">We'll also install additional Python packages required toouse SQL databases with Django.</span></span> <span data-ttu-id="72337-162">Ardından hello web uygulamasını yerel olarak çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="72337-162">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="72337-163">Visual Studio'da açın **ProjectName**, hello gelen *ProjectName* klasör.</span><span class="sxs-lookup"><span data-stu-id="72337-163">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="72337-164">Geçici olarak hello Düzenleyicisi'nde hello bağlantı dizesini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="72337-164">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="72337-165">Merhaba bağlantı dizesi bu biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="72337-165">hello connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="72337-166">Merhaba tanımını Düzenle `DATABASES` toouse hello değerleri yukarıdaki.</span><span class="sxs-lookup"><span data-stu-id="72337-166">Edit hello definition of `DATABASES` toouse hello values above.</span></span>

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. <span data-ttu-id="72337-167">Çözüm Gezgini'nde, altında **Python ortamları**, hello sanal ortamda sağ tıklayıp **Python paketini Yükle**.</span><span class="sxs-lookup"><span data-stu-id="72337-167">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="72337-168">Merhaba paketini Yükle `pyodbc` kullanarak **PIP**.</span><span class="sxs-lookup"><span data-stu-id="72337-168">Install hello package `pyodbc` using **pip**.</span></span>

     ![Python paketi Yükle iletişim kutusu](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="72337-170">Merhaba paketini Yükle `django-pyodbc-azure` kullanarak **PIP**.</span><span class="sxs-lookup"><span data-stu-id="72337-170">Install hello package `django-pyodbc-azure` using **pip**.</span></span>

     ![Python paketi Yükle iletişim kutusu](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="72337-172">İçinde **Çözüm Gezgini**, hello proje düğümüne sağ tıklayın ve seçin **Python**ve ardından **Django geçirmek**.</span><span class="sxs-lookup"><span data-stu-id="72337-172">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="72337-173">Ardından **Django Yetkili Kullanıcısı Oluşturma**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="72337-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="72337-174">Bu hello önceki bölümde oluşturduğumuz hello SQL veritabanı için hello tabloları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="72337-174">This will create hello tables for hello SQL database we created in hello previous section.</span></span> <span data-ttu-id="72337-175">Merhaba istemleri toocreate toomatch hello kullanıcının hello ilk bölümünde oluşturulan hello sqlite veritabanındaki yoksa bir kullanıcı izleyin.</span><span class="sxs-lookup"><span data-stu-id="72337-175">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section.</span></span>
5. <span data-ttu-id="72337-176">Merhaba uygulamayla çalıştırmak `F5`.</span><span class="sxs-lookup"><span data-stu-id="72337-176">Run hello application with `F5`.</span></span> <span data-ttu-id="72337-177">İle oluşturulan yoklamalar **örnek yoklamalar Oluştur** ve oy vermeyle gönderilen hello veri hello SQL veritabanında seri.</span><span class="sxs-lookup"><span data-stu-id="72337-177">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello SQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="72337-178">Yayımlama Hello web uygulama tooAzure uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="72337-178">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="72337-179">Hello Azure .NET SDK'sı, web web uygulama tooAzure App Service Web Apps kolay bir yolu toodeploy sağlar.</span><span class="sxs-lookup"><span data-stu-id="72337-179">hello Azure .NET SDK provides an easy way toodeploy your web web app tooAzure App Service Web Apps.</span></span>

1. <span data-ttu-id="72337-180">İçinde **Çözüm Gezgini**, hello proje düğümüne sağ tıklayın ve seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="72337-180">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>

     ![Web Yayımlama İletişim Kutusu](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="72337-182">**Microsoft Azure Web Apps** ’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="72337-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="72337-183">Tıklayın **yeni** toocreate yeni bir web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="72337-183">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="72337-184">Hello aşağıdaki alanları doldurun ve **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="72337-184">Fill in hello following fields and click **Create**.</span></span>

   * <span data-ttu-id="72337-185">**Web Uygulaması adı**</span><span class="sxs-lookup"><span data-stu-id="72337-185">**Web App name**</span></span>
   * <span data-ttu-id="72337-186">**App Service planı**</span><span class="sxs-lookup"><span data-stu-id="72337-186">**App Service plan**</span></span>
   * <span data-ttu-id="72337-187">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="72337-187">**Resource group**</span></span>
   * <span data-ttu-id="72337-188">**Bölge**</span><span class="sxs-lookup"><span data-stu-id="72337-188">**Region**</span></span>
   * <span data-ttu-id="72337-189">Bırakın **veritabanı sunucusu** çok ayarlamak**veritabanı yok**</span><span class="sxs-lookup"><span data-stu-id="72337-189">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="72337-190">Diğer tüm varsayılanları kabul edin ve **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="72337-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="72337-191">Web tarayıcınız toohello yayımlanan web uygulamasına otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="72337-191">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="72337-192">Hello kullanarak, beklendiği gibi hello web uygulama çalışma görmelisiniz **SQL** Azure üzerinde barındırılan veritabanı.</span><span class="sxs-lookup"><span data-stu-id="72337-192">You should see hello web app working as expected, using hello **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="72337-193">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="72337-193">Congratulations!</span></span>

     ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="72337-195">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="72337-195">Next steps</span></span>
<span data-ttu-id="72337-196">Visual Studio, Django ve SQL veritabanı için Python araçları hakkında daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="72337-196">Follow these links toolearn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="72337-197">[Visual Studio için Python Araçları Belgeleri]</span><span class="sxs-lookup"><span data-stu-id="72337-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="72337-198">[Web Projeleri]</span><span class="sxs-lookup"><span data-stu-id="72337-198">[Web Projects]</span></span>
  * <span data-ttu-id="72337-199">[Bulut Hizmeti Projeleri]</span><span class="sxs-lookup"><span data-stu-id="72337-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="72337-200">[Microsoft Azure’da Uzaktan Hata Ayıklama]</span><span class="sxs-lookup"><span data-stu-id="72337-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="72337-201">[Django Belgeleri]</span><span class="sxs-lookup"><span data-stu-id="72337-201">[Django Documentation]</span></span>
* <span data-ttu-id="72337-202">[SQL Veritabanı]</span><span class="sxs-lookup"><span data-stu-id="72337-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="72337-203">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="72337-203">What's changed</span></span>
* <span data-ttu-id="72337-204">Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="72337-204">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Python Geliştirici Merkezi]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Visual Studio için Python Araçları]: http://aka.ms/ptvs
[Visual Studio için Python Araçları 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio Örnekleri VSIX için Python araçları 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025
[VS 2015 için Azure SDK Araçları]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517190
[Visual Studio için Python Araçları Belgeleri]: http://aka.ms/ptvsdocs
[Microsoft Azure’da Uzaktan Hata Ayıklama]: http://go.microsoft.com/fwlink/?LinkId=624026
[Web Projeleri]: http://go.microsoft.com/fwlink/?LinkId=624027
[Bulut Hizmeti Projeleri]: http://go.microsoft.com/fwlink/?LinkId=624028
[Django Belgeleri]: https://www.djangoproject.com/
[SQL Veritabanı]: /documentation/services/sql-database/
