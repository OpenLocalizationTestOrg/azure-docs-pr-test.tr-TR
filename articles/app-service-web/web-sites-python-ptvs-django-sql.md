---
title: "Visual Studio için Python Araçları 2.2 ile Azure’da Django ve SQL Veritabanı"
description: "SQL veritabanı örneğinde veri depolayan bir Django web uygulaması oluşturmak için Visual Studio için Python araçlarını kullanmayı öğrenin ve Azure App Service Web Apps için dağıtın."
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
ms.openlocfilehash: 65b59dee2b7bddca77d31c692dab713c68d67e24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="75b3e-103">Visual Studio için Python Araçları 2.2 ile Azure’da Django ve SQL Veritabanı</span><span class="sxs-lookup"><span data-stu-id="75b3e-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="75b3e-104">Bu öğreticide, kullanacağız [Visual Studio için Python Araçları] yoklamalar web uygulaması PTVS örnek şablonlarından birini kullanarak basit bir oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="75b3e-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="75b3e-105">Bu öğretici olarak da kullanılabilir bir [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span><span class="sxs-lookup"><span data-stu-id="75b3e-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="75b3e-106">Biz Azure üzerinde barındırılan bir SQL veritabanı kullanmayı, bir SQL veritabanını kullanmak için web uygulamasını yapılandırma ve web uygulaması'na yayımlamak nasıl öğreneceksiniz [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="75b3e-106">We'll learn how to use a SQL database hosted on Azure, how to configure the web app to use a SQL database, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="75b3e-107">Bkz: [Python Geliştirici Merkezi] Bottle kullanarak PTVS ile Azure App Service Web Apps geliştirmeyi kapsayan diğer makaleler için Flask ve Django web altyapılarını Azure Table Storage, MySQL ve SQL Database hizmetleriyle.</span><span class="sxs-lookup"><span data-stu-id="75b3e-107">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="75b3e-108">Bu makale App Service’e odaklanmakla birlikte, [Azure Cloud Services]’i geliştirirken adımlar benzerdir.</span><span class="sxs-lookup"><span data-stu-id="75b3e-108">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75b3e-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="75b3e-109">Prerequisites</span></span>
* <span data-ttu-id="75b3e-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="75b3e-110">Visual Studio 2015</span></span>
* <span data-ttu-id="75b3e-111">[Python 2.7 32 bit]</span><span class="sxs-lookup"><span data-stu-id="75b3e-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="75b3e-112">[Visual Studio için Python Araçları 2.2]</span><span class="sxs-lookup"><span data-stu-id="75b3e-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="75b3e-113">[Visual Studio Örnekleri VSIX için Python Tools 2.2]</span><span class="sxs-lookup"><span data-stu-id="75b3e-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="75b3e-114">[VS 2015 için Azure SDK Araçları]</span><span class="sxs-lookup"><span data-stu-id="75b3e-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="75b3e-115">Django 1.9 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="75b3e-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="75b3e-116">Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="75b3e-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="75b3e-117">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="75b3e-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-the-project"></a><span data-ttu-id="75b3e-118">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="75b3e-118">Create the Project</span></span>
<span data-ttu-id="75b3e-119">Bu bölümde, örnek şablonu kullanarak bir Visual Studio projesi oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="75b3e-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="75b3e-120">Biz sanal ortam oluşturacak ve gerekli paketleri yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="75b3e-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="75b3e-121">Sqlite kullanarak yerel bir veritabanı oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="75b3e-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="75b3e-122">Ardından web uygulamasını yerel olarak çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="75b3e-122">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="75b3e-123">Visual Studio'da, **Dosya**, **Yeni Proje**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="75b3e-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="75b3e-124">[Visual Studio Örnekleri VSIX için Python Tools 2.2] proje şablonlarını **Python**, **Örnekler** altında bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75b3e-124">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="75b3e-125">**Yoklamalar Django Web Projesi**’ni seçin ve projeyi oluşturmak için Tamam’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="75b3e-125">Select **Polls Django Web Project** and click OK to create the project.</span></span>

     ![Yeni Proje İletişim Kutusu](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="75b3e-127">Dış paketleri yüklemeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="75b3e-127">You will be prompted to install external packages.</span></span> <span data-ttu-id="75b3e-128">**Sanal bir ortama yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="75b3e-128">Select **Install into a virtual environment**.</span></span>

     ![Dış Paketler İletişim Kutusu](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="75b3e-130">Temel yorumlayıcı olarak **Python 2.7**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="75b3e-130">Select **Python 2.7** as the base interpreter.</span></span>

     ![Sanal Ortama Ekle İletişim Kutusu](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="75b3e-132">**Çözüm Gezgini**’nde, proje düğümüne sağ tıklayın ve **Python**’u ve ardından **Django Geçişi**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="75b3e-132">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="75b3e-133">Ardından **Django Yetkili Kullanıcısı Oluşturma**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="75b3e-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="75b3e-134">Bu, Django yönetim konsolunu açar ve proje klasöründe bir sqlite veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="75b3e-134">This will open a Django Management Console and create a sqlite database in the project folder.</span></span> <span data-ttu-id="75b3e-135">Bir kullanıcı oluşturmak için istemleri takip edin.</span><span class="sxs-lookup"><span data-stu-id="75b3e-135">Follow the prompts to create a user.</span></span>
7. <span data-ttu-id="75b3e-136">Uygulama tuşlarına basarak çalıştığını onaylayın <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="75b3e-136">Confirm that the application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="75b3e-137">Üst kısımdaki gezinti çubuğunda **Oturum Aç**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="75b3e-137">Click **Log in** from the navigation bar at the top.</span></span>

     ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="75b3e-139">Veritabanını eşitlediğinizde, oluşturduğunuz kullanıcı için kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="75b3e-139">Enter the credentials for the user you created when you synchronized the database.</span></span>

     ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="75b3e-141">**Örnek Yoklamalar Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="75b3e-141">Click **Create Sample Polls**.</span></span>

      ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="75b3e-143">Bir yoklamaya tıklayın ve oy verin.</span><span class="sxs-lookup"><span data-stu-id="75b3e-143">Click on a poll and vote.</span></span>

      ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="75b3e-145">SQL Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="75b3e-145">Create a SQL Database</span></span>
<span data-ttu-id="75b3e-146">Veritabanı için Azure SQL veritabanını oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="75b3e-146">For the database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="75b3e-147">Aşağıdaki adımları izleyerek bir veritabanı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75b3e-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="75b3e-148">İçine oturum [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="75b3e-148">Log into the [Azure Portal].</span></span>
2. <span data-ttu-id="75b3e-149">Gezinti bölmesinin en altında tıklatın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="75b3e-149">At the bottom of the navigation pane, click **NEW**.</span></span> <span data-ttu-id="75b3e-150">, tıklatın **veri + depolama** > **SQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="75b3e-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="75b3e-151">Yeni bir kaynak grubu oluşturarak yeni SQL veritabanı yapılandırın ve uygun bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="75b3e-151">Configure the new SQL Database by creating a new resource group and select the appropriate location for it.</span></span>
4. <span data-ttu-id="75b3e-152">SQL veritabanı oluşturulduktan sonra tıklatın **Visual Studio'da Aç** veri tabanı dikey.</span><span class="sxs-lookup"><span data-stu-id="75b3e-152">Once the SQL Database is created, click **Open in Visual Studio** in the database blade.</span></span>
5. <span data-ttu-id="75b3e-153">Tıklatın **güvenlik duvarınızı yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="75b3e-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="75b3e-154">İçinde **güvenlik duvarı ayarlarını** dikey penceresinde sahip bir güvenlik duvarı kuralı ekleme **başlangıç IP** ve **bitiş IP** geliştirme makinenizde ortak IP adresi olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="75b3e-154">In the **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set to the public IP address of your development machine.</span></span> <span data-ttu-id="75b3e-155">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="75b3e-155">Click **Save**.</span></span>

   <span data-ttu-id="75b3e-156">Bu işlem, geliştirme makinenizden veritabanı sunucusuna bağlantılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="75b3e-156">This will allow connections to the database server from your development machine.</span></span>
7. <span data-ttu-id="75b3e-157">Geri veritabanı dikey penceresinde tıklayın **özellikleri**, ardından **veritabanı bağlantı dizelerini Göster**.</span><span class="sxs-lookup"><span data-stu-id="75b3e-157">Back in the database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="75b3e-158">Değeri koymak için Kopyala düğmesini kullanın **ADO.NET** panoya.</span><span class="sxs-lookup"><span data-stu-id="75b3e-158">Use the copy button to put the value of **ADO.NET** on the clipboard.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="75b3e-159">Projeyi Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="75b3e-159">Configure the Project</span></span>
<span data-ttu-id="75b3e-160">Bu bölümde, yeni oluşturduğumuz SQL veritabanını kullanmak için web uygulamamızı yapılandıracağız.</span><span class="sxs-lookup"><span data-stu-id="75b3e-160">In this section, we'll configure our web app to use the SQL database we just created.</span></span> <span data-ttu-id="75b3e-161">Biz de SQL veritabanlarını Django ile birlikte kullanmak için gerekli ek Python paketlerini de yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="75b3e-161">We'll also install additional Python packages required to use SQL databases with Django.</span></span> <span data-ttu-id="75b3e-162">Ardından web uygulamasını yerel olarak çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="75b3e-162">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="75b3e-163">Visual Studio'da, *ProjectName* klasöründe **settings.py** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="75b3e-163">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span></span> <span data-ttu-id="75b3e-164">Geçici olarak bağlantı dizesini düzenleyiciye yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="75b3e-164">Temporarily paste the connection string in the editor.</span></span> <span data-ttu-id="75b3e-165">Bağlantı dizesi bu biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="75b3e-165">The connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="75b3e-166">Tanımını Düzenle `DATABASES` yukarıdaki değerleri kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="75b3e-166">Edit the definition of `DATABASES` to use the values above.</span></span>

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

1. <span data-ttu-id="75b3e-167">Çözüm Gezgini'nde, **Python Ortamları** altında, sanal ortama sağ tıklayın ve **Python Paketini Yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="75b3e-167">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="75b3e-168">**pip** kullanarak `pyodbc` paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="75b3e-168">Install the package `pyodbc` using **pip**.</span></span>

     ![Python paketi Yükle iletişim kutusu](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="75b3e-170">**pip** kullanarak `django-pyodbc-azure` paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="75b3e-170">Install the package `django-pyodbc-azure` using **pip**.</span></span>

     ![Python paketi Yükle iletişim kutusu](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="75b3e-172">**Çözüm Gezgini**’nde, proje düğümüne sağ tıklayın ve **Python**’u ve ardından **Django Geçişi**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="75b3e-172">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="75b3e-173">Ardından **Django Yetkili Kullanıcısı Oluşturma**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="75b3e-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="75b3e-174">Bu önceki bölümde oluşturduğumuz SQL veritabanı için tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="75b3e-174">This will create the tables for the SQL database we created in the previous section.</span></span> <span data-ttu-id="75b3e-175">Kullanıcının ilk bölümünde oluşturulan sqlite veritabanındaki kullanıcıyla eşleşmesi gerekmeyen bir kullanıcı oluşturmak için istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="75b3e-175">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section.</span></span>
5. <span data-ttu-id="75b3e-176">Uygulamayı `F5` ile çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="75b3e-176">Run the application with `F5`.</span></span> <span data-ttu-id="75b3e-177">İle oluşturulan yoklamalar **örnek yoklamalar Oluştur** ve oy vermeyle gönderilen veriler SQL veritabanında seri hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="75b3e-177">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the SQL database.</span></span>

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="75b3e-178">Web uygulamasını Azure App Service’te yayımlama</span><span class="sxs-lookup"><span data-stu-id="75b3e-178">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="75b3e-179">Azure .NET SDK'sı Azure App Service Web Apps için web web uygulamanızı dağıtmak için kolay bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="75b3e-179">The Azure .NET SDK provides an easy way to deploy your web web app to Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="75b3e-180">**Çözüm Gezgini**’nde, proje düğümüne sağ tıklayın ve **Yayımla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="75b3e-180">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>

     ![Web Yayımlama İletişim Kutusu](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="75b3e-182">**Microsoft Azure Web Apps** ’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="75b3e-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="75b3e-183">Yeni bir web uygulaması oluşturmak için **Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="75b3e-183">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="75b3e-184">Aşağıdaki alanları doldurun ve **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="75b3e-184">Fill in the following fields and click **Create**.</span></span>

   * <span data-ttu-id="75b3e-185">**Web Uygulaması adı**</span><span class="sxs-lookup"><span data-stu-id="75b3e-185">**Web App name**</span></span>
   * <span data-ttu-id="75b3e-186">**App Service planı**</span><span class="sxs-lookup"><span data-stu-id="75b3e-186">**App Service plan**</span></span>
   * <span data-ttu-id="75b3e-187">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="75b3e-187">**Resource group**</span></span>
   * <span data-ttu-id="75b3e-188">**Bölge**</span><span class="sxs-lookup"><span data-stu-id="75b3e-188">**Region**</span></span>
   * <span data-ttu-id="75b3e-189">**Veritabanı sunucusu**nu **Veritabanı yok** olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="75b3e-189">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="75b3e-190">Diğer tüm varsayılanları kabul edin ve **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="75b3e-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="75b3e-191">Web tarayıcınız yayımlanan web uygulamasına otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="75b3e-191">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="75b3e-192">Web uygulaması kullanarak, beklendiği gibi çalıştığını görmelisiniz **SQL** Azure üzerinde barındırılan veritabanı.</span><span class="sxs-lookup"><span data-stu-id="75b3e-192">You should see the web app working as expected, using the **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="75b3e-193">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="75b3e-193">Congratulations!</span></span>

     ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="75b3e-195">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="75b3e-195">Next steps</span></span>
<span data-ttu-id="75b3e-196">Visual Studio, Django ve SQL veritabanı için Python araçları hakkında daha fazla bilgi için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="75b3e-196">Follow these links to learn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="75b3e-197">[Visual Studio için Python Araçları Belgeleri]</span><span class="sxs-lookup"><span data-stu-id="75b3e-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="75b3e-198">[Web Projeleri]</span><span class="sxs-lookup"><span data-stu-id="75b3e-198">[Web Projects]</span></span>
  * <span data-ttu-id="75b3e-199">[Bulut Hizmeti Projeleri]</span><span class="sxs-lookup"><span data-stu-id="75b3e-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="75b3e-200">[Microsoft Azure’da Uzaktan Hata Ayıklama]</span><span class="sxs-lookup"><span data-stu-id="75b3e-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="75b3e-201">[Django Belgeleri]</span><span class="sxs-lookup"><span data-stu-id="75b3e-201">[Django Documentation]</span></span>
* <span data-ttu-id="75b3e-202">[SQL Veritabanı]</span><span class="sxs-lookup"><span data-stu-id="75b3e-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="75b3e-203">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="75b3e-203">What's changed</span></span>
* <span data-ttu-id="75b3e-204">Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="75b3e-204">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="75b3e-205">[Python Geliştirici Merkezi]: /develop/python/</span><span class="sxs-lookup"><span data-stu-id="75b3e-205">[Python Developer Center]: /develop/python/</span></span>
<span data-ttu-id="75b3e-206">[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md</span><span class="sxs-lookup"><span data-stu-id="75b3e-206">[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md</span></span>

<!--External Link references-->
<span data-ttu-id="75b3e-207">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="75b3e-207">[Azure Portal]: https://portal.azure.com</span></span>
<span data-ttu-id="75b3e-208">[Visual Studio için Python Araçları]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="75b3e-208">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="75b3e-209">[Visual Studio için Python Araçları 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="75b3e-209">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="75b3e-210">[Visual Studio Örnekleri VSIX için Python Tools 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="75b3e-210">[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="75b3e-211">[VS 2015 için Azure SDK Araçları]: http://go.microsoft.com/fwlink/?LinkId=518003</span><span class="sxs-lookup"><span data-stu-id="75b3e-211">[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003</span></span>
<span data-ttu-id="75b3e-212">[Python 2.7 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517190</span><span class="sxs-lookup"><span data-stu-id="75b3e-212">[Python 2.7 32-bit]: http://go.microsoft.com/fwlink/?LinkId=517190</span></span>
<span data-ttu-id="75b3e-213">[Visual Studio için Python Araçları Belgeleri]: http://aka.ms/ptvsdocs</span><span class="sxs-lookup"><span data-stu-id="75b3e-213">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs</span></span>
<span data-ttu-id="75b3e-214">[Microsoft Azure’da Uzaktan Hata Ayıklama]: http://go.microsoft.com/fwlink/?LinkId=624026</span><span class="sxs-lookup"><span data-stu-id="75b3e-214">[Remote Debugging on Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026</span></span>
<span data-ttu-id="75b3e-215">[Web Projeleri]: http://go.microsoft.com/fwlink/?LinkId=624027</span><span class="sxs-lookup"><span data-stu-id="75b3e-215">[Web Projects]: http://go.microsoft.com/fwlink/?LinkId=624027</span></span>
<span data-ttu-id="75b3e-216">[Bulut Hizmeti Projeleri]: http://go.microsoft.com/fwlink/?LinkId=624028</span><span class="sxs-lookup"><span data-stu-id="75b3e-216">[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028</span></span>
<span data-ttu-id="75b3e-217">[Django Belgeleri]: https://www.djangoproject.com/</span><span class="sxs-lookup"><span data-stu-id="75b3e-217">[Django Documentation]: https://www.djangoproject.com/</span></span>
<span data-ttu-id="75b3e-218">[SQL Veritabanı]: /documentation/services/sql-database/</span><span class="sxs-lookup"><span data-stu-id="75b3e-218">[SQL Database]: /documentation/services/sql-database/</span></span>
