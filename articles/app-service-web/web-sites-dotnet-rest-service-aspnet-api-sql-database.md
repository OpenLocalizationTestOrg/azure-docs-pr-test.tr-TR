---
title: ASP.NET ve SQL DB ile azure'da bir REST API aaaCreate | Microsoft Docs
description: "Öğretici, nasıl toodeploy kullanan bir uygulama hello ASP.NET Web API tooan Azure web uygulaması Visual Studio kullanarak öğretilmektedir."
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
writer: Rick-Anderson
manager: erikre
editor: 
ms.assetid: f4916fc0-ea08-41f7-846b-73e41bc88149
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: riande
ms.openlocfilehash: 1ef45dd1582bfda367e53c39f863164422ad678b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a><span data-ttu-id="02aec-103">Azure App Service'te ASP.NET Web API ve SQL veritabanı kullanan bir REST hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="02aec-103">Create a REST service using ASP.NET Web API and SQL Database in Azure App Service</span></span>
<span data-ttu-id="02aec-104">Bu öğretici nasıl toodeploy bir ASP.NET web uygulaması tooan gösterir [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) hello Web'de Yayımla Sihirbazında Visual Studio 2013 veya Visual Studio 2013 Community Edition kullanarak.</span><span class="sxs-lookup"><span data-stu-id="02aec-104">This tutorial shows how toodeploy an ASP.NET web app tooan [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by using hello Publish Web wizard in Visual Studio 2013 or Visual Studio 2013 Community Edition.</span></span> 

<span data-ttu-id="02aec-105">Ücretsiz bir Azure hesabı açın ve Visual Studio 2013 zaten yoksa, hello SDK otomatik olarak Visual Studio 2013 Web Express için yükler.</span><span class="sxs-lookup"><span data-stu-id="02aec-105">You can open an Azure account for free, and if you don't already have Visual Studio 2013, hello SDK automatically installs Visual Studio 2013 for Web Express.</span></span> <span data-ttu-id="02aec-106">Bu nedenle Azure tamamen için ücretsiz geliştirmeye başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02aec-106">So you can start developing for Azure entirely for free.</span></span>

<span data-ttu-id="02aec-107">Bu öğretici Azure kullanımına ilişkin deneyim sahibi olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="02aec-107">This tutorial assumes that you have no prior experience using Azure.</span></span> <span data-ttu-id="02aec-108">Bu öğreticiyi tamamladığınızda, bir basit bir web uygulamasını kurup ve hello bulutta çalışan sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="02aec-108">On completing this tutorial, you'll have a simple web app up and running in hello cloud.</span></span>

<span data-ttu-id="02aec-109">Şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="02aec-109">You'll learn:</span></span>

* <span data-ttu-id="02aec-110">Nasıl tooenable makinenize yükleyerek Azure geliştirme için Azure SDK'sı hello.</span><span class="sxs-lookup"><span data-stu-id="02aec-110">How tooenable your machine for Azure development by installing hello Azure SDK.</span></span>
* <span data-ttu-id="02aec-111">Nasıl toocreate bir Visual Studio ASP.NET MVC 5 proje ve tooan Azure uygulaması yayımlama.</span><span class="sxs-lookup"><span data-stu-id="02aec-111">How toocreate a Visual Studio ASP.NET MVC 5 project and publish it tooan Azure app.</span></span>
* <span data-ttu-id="02aec-112">ASP.NET Web API tooenable toouse hello nasıl Restful API'sini çağırır.</span><span class="sxs-lookup"><span data-stu-id="02aec-112">How toouse hello ASP.NET Web API tooenable Restful API calls.</span></span>
* <span data-ttu-id="02aec-113">Nasıl toouse bir SQL Azure toostore verileri veritabanı.</span><span class="sxs-lookup"><span data-stu-id="02aec-113">How toouse a SQL database toostore data in Azure.</span></span>
* <span data-ttu-id="02aec-114">Nasıl toopublish uygulama tooAzure güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="02aec-114">How toopublish application updates tooAzure.</span></span>

<span data-ttu-id="02aec-115">ASP.NET MVC 5'te yerleşik bir basit kişi listesi web uygulaması oluşturacağınız ve veritabanı erişimi için ADO.NET Entity Framework kullanan hello.</span><span class="sxs-lookup"><span data-stu-id="02aec-115">You'll build a simple contact list web application that is built on ASP.NET MVC 5 and uses hello ADO.NET Entity Framework for database access.</span></span> <span data-ttu-id="02aec-116">Aşağıdaki çizimde gösterildiği hello hello uygulama tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="02aec-116">hello following illustration shows hello completed application:</span></span>

![web sitesinin ekran görüntüsü][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a><span data-ttu-id="02aec-118">Başlangıç projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="02aec-118">Create hello project</span></span>
1. <span data-ttu-id="02aec-119">Visual Studio 2013'ü başlatın.</span><span class="sxs-lookup"><span data-stu-id="02aec-119">Start Visual Studio 2013.</span></span>
2. <span data-ttu-id="02aec-120">Merhaba gelen **dosya** menüsünü tıklatın **yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="02aec-120">From hello **File** menu click **New Project**.</span></span>
3. <span data-ttu-id="02aec-121">Merhaba, **yeni proje** iletişim kutusunda, genişletin **Visual C#** seçip **Web** ve ardından **ASP.NET Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="02aec-121">In hello **New Project** dialog box, expand **Visual C#** and select **Web**  and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="02aec-122">Ad Merhaba uygulaması **ContactManager** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="02aec-122">Name hello application **ContactManager** and click **OK**.</span></span>
   
    ![Yeni Proje iletişim kutusu](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. <span data-ttu-id="02aec-124">Merhaba, **yeni ASP.NET projesi** iletişim kutusu, select hello **MVC** şablonu, onay **Web API** ve ardından **kimlik doğrulamayı Değiştir**.</span><span class="sxs-lookup"><span data-stu-id="02aec-124">In hello **New ASP.NET Project** dialog box, select hello **MVC** template, check **Web API** and then click **Change Authentication**.</span></span>
5. <span data-ttu-id="02aec-125">Merhaba, **kimlik doğrulamayı Değiştir** iletişim kutusu, tıklatın **doğrulaması yok**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="02aec-125">In hello **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span>
   
    ![Kimlik Doğrulaması Yok](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    <span data-ttu-id="02aec-127">Oluşturmakta olduğunuz Merhaba örnek uygulaması, kullanıcıların toolog gerektiren özellikleri olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="02aec-127">hello sample application you're creating won't have features that require users toolog in.</span></span> <span data-ttu-id="02aec-128">Hakkında bilgi için bkz: Merhaba tooimplement kimlik doğrulama ve yetkilendirme özellikleri [sonraki adımlar](#nextsteps) Bu öğreticinin hello sonunda bölüm.</span><span class="sxs-lookup"><span data-stu-id="02aec-128">For information about how tooimplement authentication and authorization features, see hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span> 
6. <span data-ttu-id="02aec-129">Merhaba, **yeni ASP.NET projesi** iletişim kutusu, yapma emin hello **hello bulut ana** denetlenir ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="02aec-129">In hello **New ASP.NET Project** dialog box, make sure hello **Host in hello Cloud** is checked and click **OK**.</span></span>

<span data-ttu-id="02aec-130">Daha önce tooAzure içinde oturum değil, istendiğinde toosign olacaktır.</span><span class="sxs-lookup"><span data-stu-id="02aec-130">If you have not previously signed in tooAzure, you will be prompted toosign in.</span></span>

1. <span data-ttu-id="02aec-131">Merhaba Yapılandırma Sihirbazı'nı temel benzersiz bir ad önermek *ContactManager* (Merhaba resimde bakın).</span><span class="sxs-lookup"><span data-stu-id="02aec-131">hello configuration wizard will suggest a unique name based on *ContactManager* (see hello image below).</span></span> <span data-ttu-id="02aec-132">Yakın bir bölge seçin.</span><span class="sxs-lookup"><span data-stu-id="02aec-132">Select a region near you.</span></span> <span data-ttu-id="02aec-133">Kullanabileceğiniz [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello en düşük gecikme süresi veri merkezi.</span><span class="sxs-lookup"><span data-stu-id="02aec-133">You can use [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello lowest latency data center.</span></span> 
2. <span data-ttu-id="02aec-134">Bir veritabanı sunucusu önce oluşturmadıysanız, seçin **oluştur yeni sunucu**, bir veritabanı kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="02aec-134">If you haven't created a database server before, select **Create new server**, enter a database user name and password.</span></span>
   
    ![Azure Web sitesi yapılandırma](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

<span data-ttu-id="02aec-136">Bir veritabanı sunucusu varsa, o toocreate yeni bir veritabanı kullanın.</span><span class="sxs-lookup"><span data-stu-id="02aec-136">If you have a database server, use that toocreate a new database.</span></span> <span data-ttu-id="02aec-137">Veritabanı sunucularıdır değerli bir kaynak ve genellikle toocreate hello birden fazla veritabanı istediğiniz test ve geliştirme yerine bir veritabanı sunucusu her bir veritabanı oluşturmak için aynı sunucu.</span><span class="sxs-lookup"><span data-stu-id="02aec-137">Database servers are a precious resource, and you generally want toocreate multiple databases on hello same server for testing and development rather than creating a database server per database.</span></span> <span data-ttu-id="02aec-138">Web sitesi ve veritabanı hello olduğundan emin olun aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="02aec-138">Make sure your web site and database are in hello same region.</span></span>

![Azure Web sitesi yapılandırma](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a><span data-ttu-id="02aec-140">Merhaba sayfa üstbilgi ve altbilgi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="02aec-140">Set hello page header and footer</span></span>
1. <span data-ttu-id="02aec-141">İçinde **Çözüm Gezgini**, hello genişletin *görünümler/paylaşılan* klasörü ve açık hello *_Layout.cshtml* dosya.</span><span class="sxs-lookup"><span data-stu-id="02aec-141">In **Solution Explorer**, expand hello *Views\Shared* folder and open hello *_Layout.cshtml* file.</span></span>
   
    ![Çözüm Gezgini'nde _Layout.cshtml][newapp004]
2. <span data-ttu-id="02aec-143">Merhaba Hello içeriğini değiştirin *Views\Shared_Layout.cshtml* koddan hello dosyasıyla:</span><span class="sxs-lookup"><span data-stu-id="02aec-143">Replace hello contents of hello *Views\Shared_Layout.cshtml* file with hello following code:</span></span>

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="utf-8" />
            <title>@ViewBag.Title - Contact Manager</title>
            <link href="~/favicon.ico" rel="shortcut icon" type="image/x-icon" />
            <meta name="viewport" content="width=device-width" />
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
        </head>
        <body>
            <header>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p class="site-title">@Html.ActionLink("Contact Manager", "Index", "Home")</p>
                    </div>
                </div>
            </header>
            <div id="body">
                @RenderSection("featured", required: false)
                <section class="content-wrapper main-content clear-fix">
                    @RenderBody()
                </section>
            </div>
            <footer>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p>&copy; @DateTime.Now.Year - Contact Manager</p>
                    </div>
                </div>
            </footer>
            @Scripts.Render("~/bundles/jquery")
            @RenderSection("scripts", required: false)
        </body>
        </html>

<span data-ttu-id="02aec-144">Merhaba biçimlendirme değişiklikleri hello uygulama adı "ASP.NET Uygulamam" yukarıda çok "Contact Manager" ve kaldırır hello bağlantılar çok**giriş**, **hakkında** ve **kişi**.</span><span class="sxs-lookup"><span data-stu-id="02aec-144">hello markup above changes hello app name from "My ASP.NET App" too"Contact Manager", and it removes hello links too**Home**, **About** and **Contact**.</span></span>

### <a name="run-hello-application-locally"></a><span data-ttu-id="02aec-145">Merhaba uygulama yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="02aec-145">Run hello application locally</span></span>
1. <span data-ttu-id="02aec-146">CTRL + F5 toorun Merhaba uygulaması tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="02aec-146">Press CTRL+F5 toorun hello application.</span></span>
   <span data-ttu-id="02aec-147">Merhaba varsayılan tarayıcıda Hello uygulama giriş sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="02aec-147">hello application home page appears in hello default browser.</span></span>
    <span data-ttu-id="02aec-148">![tooDo listesi giriş sayfası](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span><span class="sxs-lookup"><span data-stu-id="02aec-148">![tooDo List home page](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span></span>

<span data-ttu-id="02aec-149">Tüm toodo şimdi toocreate hello uygulama tooAzure dağıtacaksınız için gereken budur.</span><span class="sxs-lookup"><span data-stu-id="02aec-149">This is all you need toodo for now toocreate hello application that you'll deploy tooAzure.</span></span> <span data-ttu-id="02aec-150">Daha sonra veritabanı işlevselliği eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="02aec-150">Later you'll add database functionality.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="02aec-151">Merhaba uygulama tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="02aec-151">Deploy hello application tooAzure</span></span>
1. <span data-ttu-id="02aec-152">Visual Studio'da'nde hello projeye sağ **Çözüm Gezgini** seçip **Yayımla** hello bağlam menüsünden.</span><span class="sxs-lookup"><span data-stu-id="02aec-152">In Visual Studio, right-click hello project in **Solution Explorer** and select **Publish** from hello context menu.</span></span>
   
    ![Proje bağlam menüsünde Yayımla][PublishVSSolution]
   
    <span data-ttu-id="02aec-154">Merhaba **Web'i Yayımla** Sihirbazı açılır.</span><span class="sxs-lookup"><span data-stu-id="02aec-154">hello **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="02aec-155">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="02aec-155">Click **Publish**.</span></span>

![Ayarlar sekmesi](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

<span data-ttu-id="02aec-157">Visual Studio hello hello dosyaları toohello Azure sunucusuna kopyalama işlemi başlar.</span><span class="sxs-lookup"><span data-stu-id="02aec-157">Visual Studio begins hello process of copying hello files toohello Azure server.</span></span> <span data-ttu-id="02aec-158">Merhaba **çıkış** penceresinde hangi dağıtım eylemlerinin gerçekleştirilen gösterir ve hello dağıtım başarılı şekilde tamamlandığını bildirir.</span><span class="sxs-lookup"><span data-stu-id="02aec-158">hello **Output** window shows what deployment actions were taken and reports successful completion of hello deployment.</span></span>

1. <span data-ttu-id="02aec-159">Merhaba varsayılan tarayıcı otomatik olarak dağıtılan hello site toohello URL'sini açar.</span><span class="sxs-lookup"><span data-stu-id="02aec-159">hello default browser automatically opens toohello URL of hello deployed site.</span></span>
   
   <span data-ttu-id="02aec-160">oluşturduğunuz Merhaba uygulaması hello bulutta şu anda çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="02aec-160">hello application you created is now running in hello cloud.</span></span>
   
   ![Azure'da çalışan tooDo listesi giriş sayfası][rxz2]

## <a name="add-a-database-toohello-application"></a><span data-ttu-id="02aec-162">Bir veritabanı toohello uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="02aec-162">Add a database toohello application</span></span>
<span data-ttu-id="02aec-163">Ardından, hello MVC uygulama tooadd hello özelliği toodisplay güncelleştirme kişileri güncelleştir ve hello veri bir veritabanında depolar.</span><span class="sxs-lookup"><span data-stu-id="02aec-163">Next, you'll update hello MVC application tooadd hello ability toodisplay and update contacts and store hello data in a database.</span></span> <span data-ttu-id="02aec-164">Merhaba uygulaması hello Entity Framework toocreate hello veritabanı ve tooread kullanın ve hello veritabanındaki verileri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="02aec-164">hello application will use hello Entity Framework toocreate hello database and tooread and update data in hello database.</span></span>

### <a name="add-data-model-classes-for-hello-contacts"></a><span data-ttu-id="02aec-165">Merhaba kişiler için veri modeli sınıfları ekleme</span><span class="sxs-lookup"><span data-stu-id="02aec-165">Add data model classes for hello contacts</span></span>
<span data-ttu-id="02aec-166">Kodda bir basit veri modeli oluşturarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="02aec-166">You begin by creating a simple data model in code.</span></span>

1. <span data-ttu-id="02aec-167">İçinde **Çözüm Gezgini**, hello modeller klasörü sağ tıklatın, **Ekle**ve ardından **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="02aec-167">In **Solution Explorer**, right-click hello Models folder, click **Add**, and then **Class**.</span></span>
   
    ![Modeller klasörü bağlam menüsünde sınıfı ekleme][adddb001]
2. <span data-ttu-id="02aec-169">Merhaba, **Yeni Öğe Ekle** iletişim kutusu, ad hello yeni sınıf dosyası *Contact.cs*ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="02aec-169">In hello **Add New Item** dialog box, name hello new class file *Contact.cs*, and then click **Add**.</span></span>
   
    ![Yeni Öğe Ekle iletişim kutusu][adddb002]
3. <span data-ttu-id="02aec-171">Merhaba Contacts.cs dosyasının Merhaba içeriğine koddan hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="02aec-171">Replace hello contents of hello Contacts.cs file with hello following code.</span></span>
   
        using System.Globalization;
        namespace ContactManager.Models
        {
            public class Contact
               {
                public int ContactId { get; set; }
                public string Name { get; set; }
                public string Address { get; set; }
                public string City { get; set; }
                public string State { get; set; }
                public string Zip { get; set; }
                public string Email { get; set; }
                public string Twitter { get; set; }
                public string Self
                {
                    get { return string.Format(CultureInfo.CurrentCulture,
                         "api/contacts/{0}", this.ContactId); }
                    set { }
                }
            }
        }

<span data-ttu-id="02aec-172">Merhaba **başvurun** sınıfı, her kişi yanı sıra, birincil anahtar, hello veritabanı tarafından gereken ilgili kişi kimliği için depolayacak hello verileri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="02aec-172">hello **Contact** class defines hello data that you will store for each contact, plus a primary key, ContactID, that is needed by hello database.</span></span> <span data-ttu-id="02aec-173">Hello veri modelleri hakkında daha fazla bilgi edinebilirsiniz [sonraki adımlar](#nextsteps) Bu öğreticinin hello sonunda bölüm.</span><span class="sxs-lookup"><span data-stu-id="02aec-173">You can get more information about data models in hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span>

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a><span data-ttu-id="02aec-174">Uygulama kullanıcıların toowork hello kişilerle etkinleştirmek Web sayfaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="02aec-174">Create web pages that enable app users toowork with hello contacts</span></span>
<span data-ttu-id="02aec-175">Merhaba ASP.NET MVC hello yapı iskelesi özelliği otomatik olarak gerçekleştirir kodu oluşturabilir oluşturma, okuma, güncelleştirme ve silme (CRUD) eylemleri.</span><span class="sxs-lookup"><span data-stu-id="02aec-175">hello ASP.NET MVC hello scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span></span>

## <a name="add-a-controller-and-a-view-for-hello-data"></a><span data-ttu-id="02aec-176">Bir denetleyici ve hello veriler için bir görünüm ekleyin</span><span class="sxs-lookup"><span data-stu-id="02aec-176">Add a Controller and a view for hello data</span></span>
1. <span data-ttu-id="02aec-177">İçinde **Çözüm Gezgini**, hello denetleyicileri klasörünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="02aec-177">In **Solution Explorer**, expand hello Controllers folder.</span></span>
2. <span data-ttu-id="02aec-178">Merhaba projeyi **(Ctrl + Shift + B)**.</span><span class="sxs-lookup"><span data-stu-id="02aec-178">Build hello project **(Ctrl+Shift+B)**.</span></span> <span data-ttu-id="02aec-179">(Yapı iskelesi mekanizması kullanmadan önce hello proje oluşturmalısınız.)</span><span class="sxs-lookup"><span data-stu-id="02aec-179">(You must build hello project before using scaffolding mechanism.)</span></span> 
3. <span data-ttu-id="02aec-180">Merhaba denetleyicileri klasörü sağ tıklatın ve **Ekle**ve ardından **denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="02aec-180">Right-click hello Controllers folder and click **Add**, and then click **Controller**.</span></span>
   
    ![Denetleyici denetleyicileri klasör bağlam menüsü ekleme][addcode001]
4. <span data-ttu-id="02aec-182">Merhaba, **İskele Ekle** iletişim kutusunda **görünümleri ile MVC Entity Framework kullanarak denetleyicisi** tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="02aec-182">In hello **Add Scaffold** dialog box, select **MVC Controller with views, using Entity Framework** and click **Add**.</span></span>
   
   ![Denetleyici ekleme](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. <span data-ttu-id="02aec-184">Merhaba Denetleyici adı çok ayarlamak**HomeController**.</span><span class="sxs-lookup"><span data-stu-id="02aec-184">Set hello controller name too**HomeController**.</span></span> <span data-ttu-id="02aec-185">Seçin **kişi** model sınıfı olarak.</span><span class="sxs-lookup"><span data-stu-id="02aec-185">Select **Contact** as your model class.</span></span> <span data-ttu-id="02aec-186">Merhaba tıklatın **yeni veri bağlamı** düğmesine tıklayın ve hello varsayılan "ContactManager.Models.ContactManagerContext" Merhaba kabul **yeni veri bağlam türü**.</span><span class="sxs-lookup"><span data-stu-id="02aec-186">Click hello **New data context** button and accept hello default "ContactManager.Models.ContactManagerContext" for hello **New data context type**.</span></span> <span data-ttu-id="02aec-187">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="02aec-187">Click **Add**.</span></span>

    <span data-ttu-id="02aec-188">Bir iletişim kutusu ister: "Merhaba ada sahip bir dosya HomeController zaten çıkar.</span><span class="sxs-lookup"><span data-stu-id="02aec-188">A dialog box will prompt you: "A file with hello name HomeController already exits.</span></span> <span data-ttu-id="02aec-189">Tooreplace istiyorsunuz onu? ".</span><span class="sxs-lookup"><span data-stu-id="02aec-189">Do you want tooreplace it?".</span></span> <span data-ttu-id="02aec-190">**Evet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="02aec-190">Click **Yes**.</span></span> <span data-ttu-id="02aec-191">Merhaba giriş hello yeni proje ile oluşturulan denetleyici üzerine.</span><span class="sxs-lookup"><span data-stu-id="02aec-191">We are overwriting hello Home Controller that was created with hello new project.</span></span> <span data-ttu-id="02aec-192">Merhaba yeni giriş denetleyicisi bizim kişi listesi için kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="02aec-192">We will use hello new Home Controller for our contact list.</span></span>

    <span data-ttu-id="02aec-193">Visual Studio oluşturur denetleyicisi yöntemleri ve CRUD veritabanı işlemleri için görünümleri **kişi** nesneleri.</span><span class="sxs-lookup"><span data-stu-id="02aec-193">Visual Studio creates controller methods and views for CRUD database operations for **Contact** objects.</span></span>

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a><span data-ttu-id="02aec-194">Geçişleri etkinleştirecek, hello veritabanı oluşturma, örnek veriler ve veri Başlatıcısı ekleme</span><span class="sxs-lookup"><span data-stu-id="02aec-194">Enable Migrations, create hello database, add sample data and a data initializer</span></span>
<span data-ttu-id="02aec-195">Merhaba sonraki görevdir tooenable hello [Code First Migrations](http://curah.microsoft.com/55220) sipariş toocreate hello veritabanını özelliğinde dayalı oluşturduğunuz hello veri modeli üzerinde.</span><span class="sxs-lookup"><span data-stu-id="02aec-195">hello next task is tooenable hello [Code First Migrations](http://curah.microsoft.com/55220) feature in order toocreate hello database based on hello data model you created.</span></span>

1. <span data-ttu-id="02aec-196">Merhaba, **Araçları** menüsünde, select **kitaplık Paket Yöneticisi** ve ardından **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="02aec-196">In hello **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>
   
    ![Paket Yöneticisi konsolu Araçları menüsünde][addcode008]
2. <span data-ttu-id="02aec-198">Merhaba, **Paket Yöneticisi Konsolu** penceresinde hello aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="02aec-198">In hello **Package Manager Console** window, enter hello following command:</span></span>
   
        enable-migrations 
   
    <span data-ttu-id="02aec-199">Merhaba **enable-migrations** komut oluşturur bir *geçişler* klasöre ve bu klasörde koyar bir *Configuration.cs* dosya tooconfigure geçişler düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02aec-199">hello **enable-migrations** command creates a *Migrations* folder and it puts in that folder a *Configuration.cs* file that you can edit tooconfigure Migrations.</span></span> 
3. <span data-ttu-id="02aec-200">Merhaba, **Paket Yöneticisi Konsolu** penceresinde hello aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="02aec-200">In hello **Package Manager Console** window, enter hello following command:</span></span>
   
        add-migration Initial
   
    <span data-ttu-id="02aec-201">Merhaba **add-migration ilk** komutu adlı bir sınıf oluşturur  **&lt;date_stamp&gt;ilk** hello veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="02aec-201">hello **add-migration Initial** command generates a class named **&lt;date_stamp&gt;Initial** that creates hello database.</span></span> <span data-ttu-id="02aec-202">İlk parametre hello ( *ilk* ) rasgele ve kullanılan toocreate hello hello dosyasının adıdır.</span><span class="sxs-lookup"><span data-stu-id="02aec-202">hello first parameter ( *Initial* ) is arbitrary and used toocreate hello name of hello file.</span></span> <span data-ttu-id="02aec-203">Merhaba yeni sınıf dosyalarında görebilirsiniz **Çözüm Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="02aec-203">You can see hello new class files in **Solution Explorer**.</span></span>
   
    <span data-ttu-id="02aec-204">Merhaba, **ilk** hello sınıfı **yukarı** yöntemi oluşturur hello kişiler tablosunu ve hello **aşağı** yöntemi (tooreturn toohello önceki durumuna istediğinizde kullanılır) bırakır.</span><span class="sxs-lookup"><span data-stu-id="02aec-204">In hello **Initial** class, hello **Up** method creates hello Contacts table, and hello **Down** method (used when you want tooreturn toohello previous state) drops it.</span></span>
4. <span data-ttu-id="02aec-205">Açık hello *Migrations\Configuration.cs* dosya.</span><span class="sxs-lookup"><span data-stu-id="02aec-205">Open hello *Migrations\Configuration.cs* file.</span></span> 
5. <span data-ttu-id="02aec-206">Ad alanları aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="02aec-206">Add hello following namespaces.</span></span> 
   
         using ContactManager.Models;
6. <span data-ttu-id="02aec-207">Hello yerine *çekirdek* koddan hello yöntemiyle:</span><span class="sxs-lookup"><span data-stu-id="02aec-207">Replace hello *Seed* method with hello following code:</span></span>
   
        protected override void Seed(ContactManager.Models.ContactManagerContext context)
        {
            context.Contacts.AddOrUpdate(p => p.Name,
               new Contact
               {
                   Name = "Debra Garcia",
                   Address = "1234 Main St",
                   City = "Redmond",
                   State = "WA",
                   Zip = "10999",
                   Email = "debra@example.com",
                   Twitter = "debra_example"
               },
                new Contact
                {
                    Name = "Thorsten Weinrich",
                    Address = "5678 1st Ave W",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "thorsten@example.com",
                    Twitter = "thorsten_example"
                },
                new Contact
                {
                    Name = "Yuhong Li",
                    Address = "9012 State st",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "yuhong@example.com",
                    Twitter = "yuhong_example"
                },
                new Contact
                {
                    Name = "Jon Orton",
                    Address = "3456 Maple St",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "jon@example.com",
                    Twitter = "jon_example"
                },
                new Contact
                {
                    Name = "Diliana Alexieva-Bosseva",
                    Address = "7890 2nd Ave E",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "diliana@example.com",
                    Twitter = "diliana_example"
                }
                );
        }
   
    <span data-ttu-id="02aec-208">Bu kodu yukarıdaki hello kişi bilgilerini hello veritabanıyla başlatacak.</span><span class="sxs-lookup"><span data-stu-id="02aec-208">This code above will initialize hello database with hello contact information.</span></span> <span data-ttu-id="02aec-209">Hello veritabanı dengeli dağıtımı ile ilgili daha fazla bilgi için bkz: [hata ayıklama Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span><span class="sxs-lookup"><span data-stu-id="02aec-209">For more information on seeding hello database, see [Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span></span>
7. <span data-ttu-id="02aec-210">Merhaba, **Paket Yöneticisi Konsolu** hello komutu girin:</span><span class="sxs-lookup"><span data-stu-id="02aec-210">In hello **Package Manager Console** enter hello command:</span></span>
   
        update-database
   
    ![Paket Yöneticisi Konsolu komutları][addcode009]
   
    <span data-ttu-id="02aec-212">Merhaba **update-database** çalıştırır hello hello veritabanı oluşturan ilk geçiş.</span><span class="sxs-lookup"><span data-stu-id="02aec-212">hello **update-database** runs hello first migration which creates hello database.</span></span> <span data-ttu-id="02aec-213">Varsayılan olarak, hello veritabanı bir SQL Server Express LocalDB veritabanı olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="02aec-213">By default, hello database is created as a SQL Server Express LocalDB database.</span></span>
8. <span data-ttu-id="02aec-214">CTRL + F5 toorun Merhaba uygulaması tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="02aec-214">Press CTRL+F5 toorun hello application.</span></span> 

<span data-ttu-id="02aec-215">Merhaba uygulaması hello çekirdek veri gösterir ve düzenleme, Ayrıntılar ve delete bağlantılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="02aec-215">hello application shows hello seed data and provides edit, details and delete links.</span></span>

![Verilerinin MVC görünümü][rxz3]

## <a name="edit-hello-view"></a><span data-ttu-id="02aec-217">Merhaba Görünümü Düzenle</span><span class="sxs-lookup"><span data-stu-id="02aec-217">Edit hello View</span></span>
1. <span data-ttu-id="02aec-218">Açık hello *Views\Home\Index.cshtml* dosya.</span><span class="sxs-lookup"><span data-stu-id="02aec-218">Open hello *Views\Home\Index.cshtml* file.</span></span> <span data-ttu-id="02aec-219">Merhaba sonraki adımda, biz oluşturulan hello biçimlendirme kullanan kodu ile değiştirir [jQuery](http://jquery.com/) ve [Knockout.js](http://knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="02aec-219">In hello next step, we will replace hello generated markup with code that uses [jQuery](http://jquery.com/) and [Knockout.js](http://knockoutjs.com/).</span></span> <span data-ttu-id="02aec-220">Web API kullanarak bu yeni kodu hello kişilerinizin listesini alır ve JSON ve bağlamalar hello kişi veri toohello UI knockout.js kullanarak.</span><span class="sxs-lookup"><span data-stu-id="02aec-220">This new code retrieves hello list of contacts from using web API and JSON and then binds hello contact data toohello UI using knockout.js.</span></span> <span data-ttu-id="02aec-221">Daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#nextsteps) Bu öğreticinin hello sonunda bölüm.</span><span class="sxs-lookup"><span data-stu-id="02aec-221">For more information, see hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span> 
2. <span data-ttu-id="02aec-222">Merhaba hello dosyasının içeriğini koddan hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="02aec-222">Replace hello contents of hello file with hello following code.</span></span>
   
        @model IEnumerable<ContactManager.Models.Contact>
        @{
            ViewBag.Title = "Home";
        }
        @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                function ContactsViewModel() {
                    var self = this;
                    self.contacts = ko.observableArray([]);
                    self.addContact = function () {
                        $.post("api/contacts",
                            $("#addContact").serialize(),
                            function (value) {
                                self.contacts.push(value);
                            },
                            "json");
                    }
                    self.removeContact = function (contact) {
                        $.ajax({
                            type: "DELETE",
                            url: contact.Self,
                            success: function () {
                                self.contacts.remove(contact);
                            }
                        });
                    }
   
                    $.getJSON("api/contacts", function (data) {
                        self.contacts(data);
                    });
                }
                ko.applyBindings(new ContactsViewModel());    
        </script>
        }
        <ul id="contacts" data-bind="foreach: contacts">
            <li class="ui-widget-content ui-corner-all">
                <h1 data-bind="text: Name" class="ui-widget-header"></h1>
                <div><span data-bind="text: $data.Address || 'Address?'"></span></div>
                <div>
                    <span data-bind="text: $data.City || 'City?'"></span>,
                    <span data-bind="text: $data.State || 'State?'"></span>
                    <span data-bind="text: $data.Zip || 'Zip?'"></span>
                </div>
                <div data-bind="if: $data.Email"><a data-bind="attr: { href: 'mailto:' + Email }, text: Email"></a></div>
                <div data-bind="ifnot: $data.Email"><span>Email?</span></div>
                <div data-bind="if: $data.Twitter"><a data-bind="attr: { href: 'http://twitter.com/' + Twitter }, text: '@@' + Twitter"></a></div>
                <div data-bind="ifnot: $data.Twitter"><span>Twitter?</span></div>
                <p><a data-bind="attr: { href: Self }, click: $root.removeContact" class="removeContact ui-state-default ui-corner-all">Remove</a></p>
            </li>
        </ul>
        <form id="addContact" data-bind="submit: addContact">
            <fieldset>
                <legend>Add New Contact</legend>
                <ol>
                    <li>
                        <label for="Name">Name</label>
                        <input type="text" name="Name" />
                    </li>
                    <li>
                        <label for="Address">Address</label>
                        <input type="text" name="Address" >
                    </li>
                    <li>
                        <label for="City">City</label>
                        <input type="text" name="City" />
                    </li>
                    <li>
                        <label for="State">State</label>
                        <input type="text" name="State" />
                    </li>
                    <li>
                        <label for="Zip">Zip</label>
                        <input type="text" name="Zip" />
                    </li>
                    <li>
                        <label for="Email">E-mail</label>
                        <input type="text" name="Email" />
                    </li>
                    <li>
                        <label for="Twitter">Twitter</label>
                        <input type="text" name="Twitter" />
                    </li>
                </ol>
                <input type="submit" value="Add" />
            </fieldset>
        </form>
3. <span data-ttu-id="02aec-223">Merhaba içerik klasörünü sağ tıklatın ve **Ekle**ve ardından **yeni öğe...** .</span><span class="sxs-lookup"><span data-stu-id="02aec-223">Right-click hello Content folder and click **Add**, and then click **New Item...**.</span></span>
   
    ![İçerik klasörünü bağlam menüsünde Stil sayfası ekleme][addcode005]
4. <span data-ttu-id="02aec-225">Merhaba, **Yeni Öğe Ekle** iletişim kutusunda, girin **stili** hello üst sağ arama kutusuna ve ardından **stil sayfası**.</span><span class="sxs-lookup"><span data-stu-id="02aec-225">In hello **Add New Item** dialog box, enter **Style** in hello upper right search box and then select **Style Sheet**.</span></span>
    <span data-ttu-id="02aec-226">![Yeni Öğe Ekle iletişim kutusu][rxStyle]</span><span class="sxs-lookup"><span data-stu-id="02aec-226">![Add New Item dialog box][rxStyle]</span></span>
5. <span data-ttu-id="02aec-227">Ad hello dosyası *Contacts.css* tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="02aec-227">Name hello file *Contacts.css* and click **Add**.</span></span> <span data-ttu-id="02aec-228">Merhaba hello dosyasının içeriğini koddan hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="02aec-228">Replace hello contents of hello file with hello following code.</span></span>
   
        .column {
            float: left;
            width: 50%;
            padding: 0;
            margin: 5px 0;
        }
        form ol {
            list-style-type: none;
            padding: 0;
            margin: 0;
        }
        form li {
            padding: 1px;
            margin: 3px;
        }
        form input[type="text"] {
            width: 100%;
        }
        #addContact {
            width: 300px;
            float: left;
            width:30%;
        }
        #contacts {
            list-style-type: none;
            margin: 0;
            padding: 0;
            float:left;
            width: 70%;
        }
        #contacts li {
            margin: 3px 3px 3px 0;
            padding: 1px;
            float: left;
            width: 300px;
            text-align: center;
            background-image: none;
            background-color: #F5F5F5;
        }
        #contacts li h1
        {
            padding: 0;
            margin: 0;
            background-image: none;
            background-color: Orange;
            color: White;
            font-family: Trebuchet MS, Tahoma, Verdana, Arial, sans-serif;
        }
        .removeContact, .viewImage
        {
            padding: 3px;
            text-decoration: none;
        }
   
    <span data-ttu-id="02aec-229">Merhaba düzeni, renkler ve hello Kişi Yöneticisi uygulamada kullanılan stiller bu stil sayfası kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="02aec-229">We will use this style sheet for hello layout, colors and styles used in hello contact manager app.</span></span>
6. <span data-ttu-id="02aec-230">Açık hello *App_Start\BundleConfig.cs* dosya.</span><span class="sxs-lookup"><span data-stu-id="02aec-230">Open hello *App_Start\BundleConfig.cs* file.</span></span>
7. <span data-ttu-id="02aec-231">Aşağıdaki kod tooregister hello hello eklemek [Boşaltılan](http://knockoutjs.com/index.html "KO") eklentisi.</span><span class="sxs-lookup"><span data-stu-id="02aec-231">Add hello following code tooregister hello [Knockout](http://knockoutjs.com/index.html "KO") plugin.</span></span>
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    <span data-ttu-id="02aec-232">Merhaba ekran şablonları işleyen Boşaltılan toosimplify dinamik JavaScript kodu kullanarak bu örnek.</span><span class="sxs-lookup"><span data-stu-id="02aec-232">This sample using knockout toosimplify dynamic JavaScript code that handles hello screen templates.</span></span>
8. <span data-ttu-id="02aec-233">Merhaba içeriği/css girişi tooregister hello değiştirme *contacts.css* stil sayfası.</span><span class="sxs-lookup"><span data-stu-id="02aec-233">Modify hello contents/css entry tooregister hello *contacts.css* style sheet.</span></span> <span data-ttu-id="02aec-234">Merhaba satırı aşağıdaki gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="02aec-234">Change hello following line:</span></span>
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   <span data-ttu-id="02aec-235">Hedef:</span><span class="sxs-lookup"><span data-stu-id="02aec-235">To:</span></span>
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. <span data-ttu-id="02aec-236">Hello Paket Yöneticisi konsolu, komut tooinstall Boşaltılan aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="02aec-236">In hello Package Manager Console, run hello following command tooinstall Knockout.</span></span>
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a><span data-ttu-id="02aec-237">Merhaba Web API Restful arabirimi için bir denetleyici ekleyin</span><span class="sxs-lookup"><span data-stu-id="02aec-237">Add a controller for hello Web API Restful interface</span></span>
1. <span data-ttu-id="02aec-238">İçinde **Çözüm Gezgini**, denetleyicileri sağ tıklatın ve **Ekle** ve ardından **denetleyicisi...**</span><span class="sxs-lookup"><span data-stu-id="02aec-238">In **Solution Explorer**, right-click Controllers and click **Add** and then **Controller....**</span></span> 
2. <span data-ttu-id="02aec-239">Merhaba, **İskele Ekle** iletişim kutusunda, girin **Web API 2 denetleyici Entity Framework kullanarak Eylemler ile** ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="02aec-239">In hello **Add Scaffold** dialog box, enter **Web API 2 Controller with actions, using Entity Framework** and then click **Add**.</span></span>
   
    ![API denetleyicisi ekleme](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. <span data-ttu-id="02aec-241">Merhaba, **denetleyici Ekle** iletişim kutusunda, "ContactsController", denetleyici adı girin.</span><span class="sxs-lookup"><span data-stu-id="02aec-241">In hello **Add Controller** dialog box, enter "ContactsController" as your controller name.</span></span> <span data-ttu-id="02aec-242">"Kişiyi (ContactManager.Models)" Merhaba seçin **Model sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="02aec-242">Select "Contact (ContactManager.Models)" for hello **Model class**.</span></span>  <span data-ttu-id="02aec-243">Merhaba hello için varsayılan değer tutmak **veri bağlamı sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="02aec-243">Keep hello default value for hello **Data context class**.</span></span> 
4. <span data-ttu-id="02aec-244">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="02aec-244">Click **Add**.</span></span>

### <a name="run-hello-application-locally"></a><span data-ttu-id="02aec-245">Merhaba uygulama yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="02aec-245">Run hello application locally</span></span>
1. <span data-ttu-id="02aec-246">CTRL + F5 toorun Merhaba uygulaması tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="02aec-246">Press CTRL+F5 toorun hello application.</span></span>
   
    ![Dizin sayfası][intro001]
2. <span data-ttu-id="02aec-248">Bir kişi girin ve tıklayın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="02aec-248">Enter a contact and click **Add**.</span></span> <span data-ttu-id="02aec-249">Merhaba uygulama toohello giriş sayfasını döndürür ve girdiğiniz hello kişi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="02aec-249">hello app returns toohello home page and displays hello contact you entered.</span></span>
   
    ![Yapılacaklar listesi öğeleri içeren dizin sayfası][addwebapi004]
3. <span data-ttu-id="02aec-251">Merhaba tarayıcıda append **/api/contacts** toohello URL.</span><span class="sxs-lookup"><span data-stu-id="02aec-251">In hello browser, append **/api/contacts** toohello URL.</span></span>
   
    <span data-ttu-id="02aec-252">Merhaba elde edilen URL http://localhost:1234/api/contacts sayfasında benzeyecektir.</span><span class="sxs-lookup"><span data-stu-id="02aec-252">hello resulting URL will resemble http://localhost:1234/api/contacts.</span></span> <span data-ttu-id="02aec-253">Merhaba RESTful web API'si eklediğiniz depolanan hello kişiler döndürür.</span><span class="sxs-lookup"><span data-stu-id="02aec-253">hello RESTful web API you added returns hello stored contacts.</span></span> <span data-ttu-id="02aec-254">Firefox ve Chrome hello verileri XML biçiminde görüntüler.</span><span class="sxs-lookup"><span data-stu-id="02aec-254">Firefox and Chrome will display hello data in XML format.</span></span>
   
    ![Yapılacaklar listesi öğeleri içeren dizin sayfası][rxFFchrome]

    <span data-ttu-id="02aec-256">IE tooopen isteyebilir veya hello kişiler kaydedin.</span><span class="sxs-lookup"><span data-stu-id="02aec-256">IE will prompt you tooopen or save hello contacts.</span></span>

    ![Web API Kaydet iletişim kutusu][addwebapi006]


    <span data-ttu-id="02aec-258">Not Defteri veya bir tarayıcı kişiler döndürülen hello açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02aec-258">You can open hello returned contacts in notepad or a browser.</span></span>

    <span data-ttu-id="02aec-259">Bu çıktı, mobil web sayfası veya uygulama gibi başka bir uygulama tarafından kullanılabilecek.</span><span class="sxs-lookup"><span data-stu-id="02aec-259">This output can be consumed by another application such as mobile web page or application.</span></span>

    ![Web API Kaydet iletişim kutusu][addwebapi007]

    <span data-ttu-id="02aec-261">**Güvenlik Uyarısı**: Bu noktada, güvenli olmayan ve güvenlik açığı tooCSRF saldırı uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="02aec-261">**Security Warning**: At this point, your application is insecure and vulnerable tooCSRF attack.</span></span> <span data-ttu-id="02aec-262">Daha sonra hello öğreticide Biz bu güvenlik açığından kaldırır.</span><span class="sxs-lookup"><span data-stu-id="02aec-262">Later in hello tutorial we will remove this vulnerability.</span></span> <span data-ttu-id="02aec-263">Daha fazla bilgi için bkz: [önleme siteler arası istek sahteciliği (CSRF) saldırılarını][prevent-csrf-attacks].</span><span class="sxs-lookup"><span data-stu-id="02aec-263">For more information see [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks].</span></span>
## <a name="add-xsrf-protection"></a><span data-ttu-id="02aec-264">XSRF koruma Ekle</span><span class="sxs-lookup"><span data-stu-id="02aec-264">Add XSRF Protection</span></span>
<span data-ttu-id="02aec-265">Siteler arası istek sahtekarlığı (XSRF veya CSRF olarak da bilinir) kötü amaçlı bir Web sitesi istemci tarayıcısına ve bu tarayıcı tarafından güvenilen bir Web sitesi arasındaki hello etkileşim yapabildiği etkileyebilir web barındırılan uygulamalara yönelik bir saldırı ' dir.</span><span class="sxs-lookup"><span data-stu-id="02aec-265">Cross-site request forgery (also known as XSRF or CSRF) is an attack against web-hosted applications whereby a malicious website can influence hello interaction between a client browser and a website trusted by that browser.</span></span> <span data-ttu-id="02aec-266">Web tarayıcıları kimlik doğrulama belirteçleri her isteği tooa Web sitesi ile otomatik olarak gönderecektir çünkü bu saldırıların olası yapılır.</span><span class="sxs-lookup"><span data-stu-id="02aec-266">These attacks are made possible because web browsers will send authentication tokens automatically with every request tooa website.</span></span> <span data-ttu-id="02aec-267">Merhaba klasik ASP gibi bir kimlik doğrulama tanımlama bilgisini bir örneğidir. NET'in form kimlik doğrulaması bileti.</span><span class="sxs-lookup"><span data-stu-id="02aec-267">hello canonical example is an authentication cookie, such as ASP.NET's Forms Authentication ticket.</span></span> <span data-ttu-id="02aec-268">Ancak, tüm kalıcı kimlik doğrulama mekanizması (örneğin, Windows kimlik doğrulaması, temel ve benzeri) kullanan Web siteleri tarafından bu saldırıların hedeflenebilir.</span><span class="sxs-lookup"><span data-stu-id="02aec-268">However, websites which use any persistent authentication mechanism (such as Windows Authentication, Basic, and so forth) can be targeted by these attacks.</span></span>

<span data-ttu-id="02aec-269">Bir kimlik avı saldırıdan XSRF saldırının farklıdır.</span><span class="sxs-lookup"><span data-stu-id="02aec-269">An XSRF attack is distinct from a phishing attack.</span></span> <span data-ttu-id="02aec-270">Kimlik avı saldırıları hello kurban müdahalesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="02aec-270">Phishing attacks require interaction from hello victim.</span></span> <span data-ttu-id="02aec-271">Bir kimlik avı saldırısı kötü amaçlı bir Web sitesi hello hedef Web sitesi benzetimini yapacak ve hello kurban hassas bilgileri toohello saldırgan sağlama içine sizi kandırmalarına.</span><span class="sxs-lookup"><span data-stu-id="02aec-271">In a phishing attack, a malicious website will mimic hello target website, and hello victim is fooled into providing sensitive information toohello attacker.</span></span> <span data-ttu-id="02aec-272">Bir XSRF saldırısında, genellikle bir etkileşim yoktur hello kurban gerekli.</span><span class="sxs-lookup"><span data-stu-id="02aec-272">In an XSRF attack, there is often no interaction necessary from hello victim.</span></span> <span data-ttu-id="02aec-273">Bunun yerine, hello saldırgan tüm ilgili tanımlama bilgilerini toohello hedef Web sitesi otomatik olarak göndermeye hello tarayıcıya bağlı olan.</span><span class="sxs-lookup"><span data-stu-id="02aec-273">Rather, hello attacker is relying on hello browser automatically sending all relevant cookies toohello destination website.</span></span>

<span data-ttu-id="02aec-274">Daha fazla bilgi için bkz: Merhaba [açık Web uygulaması güvenlik projesi](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span><span class="sxs-lookup"><span data-stu-id="02aec-274">For more information, see hello [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span></span>

1. <span data-ttu-id="02aec-275">İçinde **Çözüm Gezgini**, sağ **ContactManager** proje ve tıklatın **Ekle** ve ardından **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="02aec-275">In **Solution Explorer**, right **ContactManager** project and click **Add** and then click **Class**.</span></span>
2. <span data-ttu-id="02aec-276">Ad hello dosyası *ValidateHttpAntiForgeryTokenAttribute.cs* ve hello aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="02aec-276">Name hello file *ValidateHttpAntiForgeryTokenAttribute.cs* and add hello following code:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Helpers;
        using System.Web.Http.Controllers;
        using System.Web.Http.Filters;
        using System.Web.Mvc;
        namespace ContactManager.Filters
        {
            public class ValidateHttpAntiForgeryTokenAttribute : AuthorizationFilterAttribute
            {
                public override void OnAuthorization(HttpActionContext actionContext)
                {
                    HttpRequestMessage request = actionContext.ControllerContext.Request;
                    try
                    {
                        if (IsAjaxRequest(request))
                        {
                            ValidateRequestHeader(request);
                        }
                        else
                        {
                            AntiForgery.Validate();
                        }
                    }
                    catch (HttpAntiForgeryException e)
                    {
                        actionContext.Response = request.CreateErrorResponse(HttpStatusCode.Forbidden, e);
                    }
                }
                private bool IsAjaxRequest(HttpRequestMessage request)
                {
                    IEnumerable<string> xRequestedWithHeaders;
                    if (request.Headers.TryGetValues("X-Requested-With", out xRequestedWithHeaders))
                    {
                        string headerValue = xRequestedWithHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(headerValue))
                        {
                            return String.Equals(headerValue, "XMLHttpRequest", StringComparison.OrdinalIgnoreCase);
                        }
                    }
                    return false;
                }
                private void ValidateRequestHeader(HttpRequestMessage request)
                {
                    string cookieToken = String.Empty;
                    string formToken = String.Empty;
                    IEnumerable<string> tokenHeaders;
                    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
                    {
                        string tokenValue = tokenHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(tokenValue))
                        {
                            string[] tokens = tokenValue.Split(':');
                            if (tokens.Length == 2)
                            {
                                cookieToken = tokens[0].Trim();
                                formToken = tokens[1].Trim();
                            }
                        }
                    }
                    AntiForgery.Validate(cookieToken, formToken);
                }
            }
        }
3. <span data-ttu-id="02aec-277">Merhaba aşağıdakileri ekleyin *kullanarak* deyimi toohello sözleşmeler denetleyicisi erişim toohello alacak şekilde **[ValidateHttpAntiForgeryToken]** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="02aec-277">Add hello following *using* statement toohello contracts controller so you have access toohello **[ValidateHttpAntiForgeryToken]** attribute.</span></span>
   
        using ContactManager.Filters;
4. <span data-ttu-id="02aec-278">Merhaba eklemek **[ValidateHttpAntiForgeryToken]** toohello Post yöntemleri hello özniteliği **ContactsController** tooprotect, XSRF tehditlere karşı.</span><span class="sxs-lookup"><span data-stu-id="02aec-278">Add hello **[ValidateHttpAntiForgeryToken]** attribute toohello Post methods of hello **ContactsController** tooprotect it from XSRF threats.</span></span> <span data-ttu-id="02aec-279">Toohello "PutContact", "PostContact" ekleyecek ve **DeleteContact** eylem yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="02aec-279">You will add it toohello "PutContact",  "PostContact" and **DeleteContact** action methods.</span></span>
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. <span data-ttu-id="02aec-280">Güncelleştirme hello *betikleri* hello bölümünü *Views\Home\Index.cshtml* tooinclude kod tooget hello XSRF belirteçleri dosya.</span><span class="sxs-lookup"><span data-stu-id="02aec-280">Update hello *Scripts* section of hello *Views\Home\Index.cshtml* file tooinclude code tooget hello XSRF tokens.</span></span>
   
         @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                @functions{
                   public string TokenHeaderValue()
                   {
                      string cookieToken, formToken;
                      AntiForgery.GetTokens(null, out cookieToken, out formToken);
                      return cookieToken + ":" + formToken;                
                   }
                }
   
               function ContactsViewModel() {
                  var self = this;
                  self.contacts = ko.observableArray([]);
                  self.addContact = function () {
   
                     $.ajax({
                        type: "post",
                        url: "api/contacts",
                        data: $("#addContact").serialize(),
                        dataType: "json",
                        success: function (value) {
                           self.contacts.push(value);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
                     });
   
                  }
                  self.removeContact = function (contact) {
                     $.ajax({
                        type: "DELETE",
                        url: contact.Self,
                        success: function () {
                           self.contacts.remove(contact);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
   
                     });
                  }
   
                  $.getJSON("api/contacts", function (data) {
                     self.contacts(data);
                  });
               }
               ko.applyBindings(new ContactsViewModel());
            </script>
         }

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a><span data-ttu-id="02aec-281">Yayımlama Hello uygulama güncelleştirme tooAzure ve SQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="02aec-281">Publish hello application update tooAzure and SQL Database</span></span>
<span data-ttu-id="02aec-282">toopublish hello uygulama, daha önce uyguladığınız hello yordamı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="02aec-282">toopublish hello application, you repeat hello procedure you followed earlier.</span></span>

1. <span data-ttu-id="02aec-283">İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="02aec-283">In **Solution Explorer**, right click hello project and select **Publish**.</span></span>
   
    ![Yayımlama][rxP]
2. <span data-ttu-id="02aec-285">Merhaba tıklatın **ayarları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="02aec-285">Click hello **Settings** tab.</span></span>
3. <span data-ttu-id="02aec-286">Altında **ContactsManagerContext(ContactsManagerContext)**, hello tıklatın **v** simgesi toochange *uzak bağlantı dizesi* toohello bağlantı dizesi hello başvurun Veritabanı.</span><span class="sxs-lookup"><span data-stu-id="02aec-286">Under **ContactsManagerContext(ContactsManagerContext)**, click hello **v** icon toochange *Remote connection string* toohello connection string for hello contact database.</span></span> <span data-ttu-id="02aec-287">Tıklatın **ContactDB**.</span><span class="sxs-lookup"><span data-stu-id="02aec-287">Click **ContactDB**.</span></span>
   
    ![Ayarlar](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. <span data-ttu-id="02aec-289">Merhaba kutuyu **yürütme önce kod uygulamalı geçişler (uygulama başlatılırken çalışır)**.</span><span class="sxs-lookup"><span data-stu-id="02aec-289">Check hello box for **Execute Code First Migrations (runs on application start)**.</span></span>
5. <span data-ttu-id="02aec-290">Tıklatın **sonraki** ve ardından **Önizleme**.</span><span class="sxs-lookup"><span data-stu-id="02aec-290">Click **Next** and then click **Preview**.</span></span> <span data-ttu-id="02aec-291">Visual Studio eklenen veya güncelleştirilen hello dosyaların bir listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="02aec-291">Visual Studio displays a list of hello files that will be added or updated.</span></span>
6. <span data-ttu-id="02aec-292">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="02aec-292">Click **Publish**.</span></span>
   <span data-ttu-id="02aec-293">Merhaba dağıtım tamamlandıktan sonra hello tarayıcı Merhaba uygulaması toohello giriş sayfasını açar.</span><span class="sxs-lookup"><span data-stu-id="02aec-293">After hello deployment completes, hello browser opens toohello home page of hello application.</span></span>
   
    ![Hiçbir kişilerle dizin sayfası][intro001]
   
    <span data-ttu-id="02aec-295">dağıtılan hello Hello Visual Studio yayımlama işlemi otomatik olarak yapılandırılan hello bağlantı dizesi *Web.config* toopoint toohello SQL veritabanı dosyası.</span><span class="sxs-lookup"><span data-stu-id="02aec-295">hello Visual Studio publish process automatically configured hello connection string in hello deployed *Web.config* file toopoint toohello SQL database.</span></span> <span data-ttu-id="02aec-296">Ayrıca, hello ilk zaman Merhaba uygulaması hello veritabanına dağıtımdan sonra erişir Code First Migrations tooautomatically yükseltme hello veritabanı toohello en son sürümü yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="02aec-296">It also configured Code First Migrations tooautomatically upgrade hello database toohello latest version hello first time hello application accesses hello database after deployment.</span></span>
   
    <span data-ttu-id="02aec-297">Bu yapılandırma sonucunda Code First hello veritabanı hello hello kod çalıştırarak oluşturulan **ilk** daha önce oluşturduğunuz sınıfı.</span><span class="sxs-lookup"><span data-stu-id="02aec-297">As a result of this configuration, Code First created hello database by running hello code in hello **Initial** class that you created earlier.</span></span> <span data-ttu-id="02aec-298">Dağıtımdan sonra bu hello ilk zaman hello çalıştığınız uygulama tooaccess hello veritabanı yaptınız.</span><span class="sxs-lookup"><span data-stu-id="02aec-298">It did this hello first time hello application tried tooaccess hello database after deployment.</span></span>
7. <span data-ttu-id="02aec-299">Yerel olarak hello uygulama veritabanı dağıtımı başarılı oldu tooverify çalıştırdığınızda yaptığınız gibi bir kişi girin.</span><span class="sxs-lookup"><span data-stu-id="02aec-299">Enter a contact as you did when you ran hello app locally, tooverify that database deployment succeeded.</span></span>

<span data-ttu-id="02aec-300">Girdiğiniz hello öğenin kaydedilir ve hello Kişi Yöneticisi sayfada görünen gördüğünüzde hello veritabanında depolandı bilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02aec-300">When you see that hello item you enter is saved and appears on hello contact manager page, you know that it has been stored in hello database.</span></span>

![Kişilerle dizin sayfası][addwebapi004]

<span data-ttu-id="02aec-302">Merhaba uygulaması artık hello bulutta SQL veritabanı toostore kullanarak verileri çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="02aec-302">hello application is now running in hello cloud, using SQL Database toostore its data.</span></span> <span data-ttu-id="02aec-303">Azure'da hello uygulamayı test ettikten sonra silin.</span><span class="sxs-lookup"><span data-stu-id="02aec-303">After you finish testing hello application in Azure, delete it.</span></span> <span data-ttu-id="02aec-304">Merhaba uygulamanın genel ve mekanizması toolimit erişimi yok.</span><span class="sxs-lookup"><span data-stu-id="02aec-304">hello application is public and doesn't have a mechanism toolimit access.</span></span>

> [!NOTE]
> <span data-ttu-id="02aec-305">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02aec-305">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="02aec-306">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="02aec-306">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="02aec-307">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="02aec-307">Next Steps</span></span>
<span data-ttu-id="02aec-308">Başka bir şekilde toostore bir Azure uygulamasında toouse ilişkisel olmayan verileri depolama BLOB'ları ve tabloları hello biçiminde sağlayan Azure depolama verilerdir.</span><span class="sxs-lookup"><span data-stu-id="02aec-308">Another way toostore data in an Azure application is toouse Azure storage, which provide non-relational data storage in hello form of blobs and tables.</span></span> <span data-ttu-id="02aec-309">bağlantılar aşağıdaki hello Web API, ASP.NET MVC ve Windows Azure üzerinde daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="02aec-309">hello following links provide more information on Web API, ASP.NET MVC and Window Azure.</span></span>

* <span data-ttu-id="02aec-310">[MVC kullanarak Entity Framework ile çalışmaya başlama][EFCodeFirstMVCTutorial]</span><span class="sxs-lookup"><span data-stu-id="02aec-310">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial]</span></span>
* [<span data-ttu-id="02aec-311">Giriş tooASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="02aec-311">Intro tooASP.NET MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="02aec-312">İlk ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="02aec-312">Your First ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [<span data-ttu-id="02aec-313">WAWS hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="02aec-313">Debugging WAWS</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)

<span data-ttu-id="02aec-314">Bu öğretici ve hello örnek uygulaması tarafından yazıldı [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) zel Dykstra ve Hakan Dorrans yardımla (Twitter [ @blowdart ](https://twitter.com/blowdart)).</span><span class="sxs-lookup"><span data-stu-id="02aec-314">This tutorial and hello sample application was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span></span> 

<span data-ttu-id="02aec-315">Lütfen geri bildirim neleri beğendiğinizi veya yalnızca hello öğretici kendisi hakkında aynı zamanda bu gösteren hello ürünlerle ilgili, geliştirilmiş toosee ister misiniz bırakın.</span><span class="sxs-lookup"><span data-stu-id="02aec-315">Please leave feedback on what you liked or what you would like toosee improved, not only about hello tutorial itself but also about hello products that it demonstrates.</span></span> <span data-ttu-id="02aec-316">Geri bildiriminiz geliştirmeleri belirlememize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="02aec-316">Your feedback will help us prioritize improvements.</span></span> <span data-ttu-id="02aec-317">Yapılandırma ve dağıtma hello üyelik veritabanının daha fazla Otomasyon hello işlemi için ne kadar ilgi var olduğunu bulma özellikle ilginizi duyuyoruz.</span><span class="sxs-lookup"><span data-stu-id="02aec-317">We are especially interested in finding out how much interest there is in more automation for hello process of configuring and deploying hello membership database.</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="02aec-318">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="02aec-318">What's changed</span></span>
* <span data-ttu-id="02aec-319">Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="02aec-319">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles toohello Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update hello Membership Database]:#ppd2
[setupdbenv]: #bkmk_setupdevenv
[setupwindowsazureenv]: #bkmk_setupwindowsazure
[createapplication]: #bkmk_createmvc4app
[deployapp1]: #bkmk_deploytowindowsazure1
[adddb]: #bkmk_addadatabase
[addcontroller]: #bkmk_addcontroller
[addwebapi]: #bkmk_addwebapi
[deploy2]: #bkmk_deploydatabaseupdate

<!-- links -->
[EFCodeFirstMVCTutorial]: http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
[dbcontext-link]: http://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx


<!-- images-->
[rxE]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxE.png
[rxP]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxP.png
[rx22]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/
[rxb2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxb2.png
[rxz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz.png
[rxzz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxzz.png
[rxz2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz2.png
[rxz3]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz3.png
[rxStyle]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxStyle.png
[rxz4]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz4.png
[rxz44]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz44.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxPrevDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPrevDB.png
[rxOverwrite]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxOverwrite.png
[rxPWS]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPWS.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxAddApiController]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxAddApiController.png
[rxFFchrome]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxFFchrome.png
[intro001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobil-intro-finished-web-app.png
[rxCreateWSwithDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxCreateWSwithDB.png
[setup007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-setup-azure-site-004.png
[setup009]: ../Media/dntutmobile-setup-azure-site-006.png
[newapp002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-002.png
[newapp004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-004.png
[firsdeploy007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-005.png
[firsdeploy009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-007.png
[adddb001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-001.png
[adddb002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-002.png
[addcode001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-context-menu.png
[addcode002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-controller-dialog.png
[addcode004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-index-context.png
[addcode005]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-contents-context-menu.png
[addcode007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-bundleconfig-context.png
[addcode008]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-menu.png
[addcode009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-console.png
[addwebapi004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-added-contact.png
[addwebapi006]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-save-returned-contacts.png
[addwebapi007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-contacts-in-notepad.png
[Add XSRF Protection]: #xsrf
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[Add XSRF Protection]: #xsrf
[ImportPublishSettings]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishSettings.png
[ImportPublishProfile]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishProfile.png
[PublishVSSolution]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/PublishVSSolution.png
[ValidateConnection]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ValidateConnection.png
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[prevent-csrf-attacks]: http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-(csrf)-attacks

