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
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a>Azure App Service'te ASP.NET Web API ve SQL veritabanı kullanan bir REST hizmeti oluşturma
Bu öğretici nasıl toodeploy bir ASP.NET web uygulaması tooan gösterir [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) hello Web'de Yayımla Sihirbazında Visual Studio 2013 veya Visual Studio 2013 Community Edition kullanarak. 

Ücretsiz bir Azure hesabı açın ve Visual Studio 2013 zaten yoksa, hello SDK otomatik olarak Visual Studio 2013 Web Express için yükler. Bu nedenle Azure tamamen için ücretsiz geliştirmeye başlayabilirsiniz.

Bu öğretici Azure kullanımına ilişkin deneyim sahibi olduğunuzu varsayar. Bu öğreticiyi tamamladığınızda, bir basit bir web uygulamasını kurup ve hello bulutta çalışan sahip olacaksınız.

Şunları öğreneceksiniz:

* Nasıl tooenable makinenize yükleyerek Azure geliştirme için Azure SDK'sı hello.
* Nasıl toocreate bir Visual Studio ASP.NET MVC 5 proje ve tooan Azure uygulaması yayımlama.
* ASP.NET Web API tooenable toouse hello nasıl Restful API'sini çağırır.
* Nasıl toouse bir SQL Azure toostore verileri veritabanı.
* Nasıl toopublish uygulama tooAzure güncelleştirir.

ASP.NET MVC 5'te yerleşik bir basit kişi listesi web uygulaması oluşturacağınız ve veritabanı erişimi için ADO.NET Entity Framework kullanan hello. Aşağıdaki çizimde gösterildiği hello hello uygulama tamamlandı:

![web sitesinin ekran görüntüsü][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a>Başlangıç projesi oluşturma
1. Visual Studio 2013'ü başlatın.
2. Merhaba gelen **dosya** menüsünü tıklatın **yeni proje**.
3. Merhaba, **yeni proje** iletişim kutusunda, genişletin **Visual C#** seçip **Web** ve ardından **ASP.NET Web uygulaması**. Ad Merhaba uygulaması **ContactManager** tıklatıp **Tamam**.
   
    ![Yeni Proje iletişim kutusu](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. Merhaba, **yeni ASP.NET projesi** iletişim kutusu, select hello **MVC** şablonu, onay **Web API** ve ardından **kimlik doğrulamayı Değiştir**.
5. Merhaba, **kimlik doğrulamayı Değiştir** iletişim kutusu, tıklatın **doğrulaması yok**ve ardından **Tamam**.
   
    ![Kimlik Doğrulaması Yok](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    Oluşturmakta olduğunuz Merhaba örnek uygulaması, kullanıcıların toolog gerektiren özellikleri olmayacaktır. Hakkında bilgi için bkz: Merhaba tooimplement kimlik doğrulama ve yetkilendirme özellikleri [sonraki adımlar](#nextsteps) Bu öğreticinin hello sonunda bölüm. 
6. Merhaba, **yeni ASP.NET projesi** iletişim kutusu, yapma emin hello **hello bulut ana** denetlenir ve tıklayın **Tamam**.

Daha önce tooAzure içinde oturum değil, istendiğinde toosign olacaktır.

1. Merhaba Yapılandırma Sihirbazı'nı temel benzersiz bir ad önermek *ContactManager* (Merhaba resimde bakın). Yakın bir bölge seçin. Kullanabileceğiniz [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello en düşük gecikme süresi veri merkezi. 
2. Bir veritabanı sunucusu önce oluşturmadıysanız, seçin **oluştur yeni sunucu**, bir veritabanı kullanıcı adı ve parola girin.
   
    ![Azure Web sitesi yapılandırma](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

Bir veritabanı sunucusu varsa, o toocreate yeni bir veritabanı kullanın. Veritabanı sunucularıdır değerli bir kaynak ve genellikle toocreate hello birden fazla veritabanı istediğiniz test ve geliştirme yerine bir veritabanı sunucusu her bir veritabanı oluşturmak için aynı sunucu. Web sitesi ve veritabanı hello olduğundan emin olun aynı bölgede.

![Azure Web sitesi yapılandırma](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a>Merhaba sayfa üstbilgi ve altbilgi ayarlayın
1. İçinde **Çözüm Gezgini**, hello genişletin *görünümler/paylaşılan* klasörü ve açık hello *_Layout.cshtml* dosya.
   
    ![Çözüm Gezgini'nde _Layout.cshtml][newapp004]
2. Merhaba Hello içeriğini değiştirin *Views\Shared_Layout.cshtml* koddan hello dosyasıyla:

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

Merhaba biçimlendirme değişiklikleri hello uygulama adı "ASP.NET Uygulamam" yukarıda çok "Contact Manager" ve kaldırır hello bağlantılar çok**giriş**, **hakkında** ve **kişi**.

### <a name="run-hello-application-locally"></a>Merhaba uygulama yerel olarak çalıştırma
1. CTRL + F5 toorun Merhaba uygulaması tuşuna basın.
   Merhaba varsayılan tarayıcıda Hello uygulama giriş sayfası görüntülenir.
    ![tooDo listesi giriş sayfası](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)

Tüm toodo şimdi toocreate hello uygulama tooAzure dağıtacaksınız için gereken budur. Daha sonra veritabanı işlevselliği eklersiniz.

## <a name="deploy-hello-application-tooazure"></a>Merhaba uygulama tooAzure dağıtma
1. Visual Studio'da'nde hello projeye sağ **Çözüm Gezgini** seçip **Yayımla** hello bağlam menüsünden.
   
    ![Proje bağlam menüsünde Yayımla][PublishVSSolution]
   
    Merhaba **Web'i Yayımla** Sihirbazı açılır.
2. **Yayımla**’ta tıklayın.

![Ayarlar sekmesi](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

Visual Studio hello hello dosyaları toohello Azure sunucusuna kopyalama işlemi başlar. Merhaba **çıkış** penceresinde hangi dağıtım eylemlerinin gerçekleştirilen gösterir ve hello dağıtım başarılı şekilde tamamlandığını bildirir.

1. Merhaba varsayılan tarayıcı otomatik olarak dağıtılan hello site toohello URL'sini açar.
   
   oluşturduğunuz Merhaba uygulaması hello bulutta şu anda çalışıyor.
   
   ![Azure'da çalışan tooDo listesi giriş sayfası][rxz2]

## <a name="add-a-database-toohello-application"></a>Bir veritabanı toohello uygulama ekleme
Ardından, hello MVC uygulama tooadd hello özelliği toodisplay güncelleştirme kişileri güncelleştir ve hello veri bir veritabanında depolar. Merhaba uygulaması hello Entity Framework toocreate hello veritabanı ve tooread kullanın ve hello veritabanındaki verileri güncelleştirin.

### <a name="add-data-model-classes-for-hello-contacts"></a>Merhaba kişiler için veri modeli sınıfları ekleme
Kodda bir basit veri modeli oluşturarak başlayın.

1. İçinde **Çözüm Gezgini**, hello modeller klasörü sağ tıklatın, **Ekle**ve ardından **sınıfı**.
   
    ![Modeller klasörü bağlam menüsünde sınıfı ekleme][adddb001]
2. Merhaba, **Yeni Öğe Ekle** iletişim kutusu, ad hello yeni sınıf dosyası *Contact.cs*ve ardından **Ekle**.
   
    ![Yeni Öğe Ekle iletişim kutusu][adddb002]
3. Merhaba Contacts.cs dosyasının Merhaba içeriğine koddan hello ile değiştirin.
   
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

Merhaba **başvurun** sınıfı, her kişi yanı sıra, birincil anahtar, hello veritabanı tarafından gereken ilgili kişi kimliği için depolayacak hello verileri tanımlar. Hello veri modelleri hakkında daha fazla bilgi edinebilirsiniz [sonraki adımlar](#nextsteps) Bu öğreticinin hello sonunda bölüm.

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a>Uygulama kullanıcıların toowork hello kişilerle etkinleştirmek Web sayfaları oluşturma
Merhaba ASP.NET MVC hello yapı iskelesi özelliği otomatik olarak gerçekleştirir kodu oluşturabilir oluşturma, okuma, güncelleştirme ve silme (CRUD) eylemleri.

## <a name="add-a-controller-and-a-view-for-hello-data"></a>Bir denetleyici ve hello veriler için bir görünüm ekleyin
1. İçinde **Çözüm Gezgini**, hello denetleyicileri klasörünü genişletin.
2. Merhaba projeyi **(Ctrl + Shift + B)**. (Yapı iskelesi mekanizması kullanmadan önce hello proje oluşturmalısınız.) 
3. Merhaba denetleyicileri klasörü sağ tıklatın ve **Ekle**ve ardından **denetleyicisi**.
   
    ![Denetleyici denetleyicileri klasör bağlam menüsü ekleme][addcode001]
4. Merhaba, **İskele Ekle** iletişim kutusunda **görünümleri ile MVC Entity Framework kullanarak denetleyicisi** tıklatıp **Ekle**.
   
   ![Denetleyici ekleme](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. Merhaba Denetleyici adı çok ayarlamak**HomeController**. Seçin **kişi** model sınıfı olarak. Merhaba tıklatın **yeni veri bağlamı** düğmesine tıklayın ve hello varsayılan "ContactManager.Models.ContactManagerContext" Merhaba kabul **yeni veri bağlam türü**. **Ekle**'ye tıklayın.

    Bir iletişim kutusu ister: "Merhaba ada sahip bir dosya HomeController zaten çıkar. Tooreplace istiyorsunuz onu? ". **Evet**'e tıklayın. Merhaba giriş hello yeni proje ile oluşturulan denetleyici üzerine. Merhaba yeni giriş denetleyicisi bizim kişi listesi için kullanacağız.

    Visual Studio oluşturur denetleyicisi yöntemleri ve CRUD veritabanı işlemleri için görünümleri **kişi** nesneleri.

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a>Geçişleri etkinleştirecek, hello veritabanı oluşturma, örnek veriler ve veri Başlatıcısı ekleme
Merhaba sonraki görevdir tooenable hello [Code First Migrations](http://curah.microsoft.com/55220) sipariş toocreate hello veritabanını özelliğinde dayalı oluşturduğunuz hello veri modeli üzerinde.

1. Merhaba, **Araçları** menüsünde, select **kitaplık Paket Yöneticisi** ve ardından **Paket Yöneticisi Konsolu**.
   
    ![Paket Yöneticisi konsolu Araçları menüsünde][addcode008]
2. Merhaba, **Paket Yöneticisi Konsolu** penceresinde hello aşağıdaki komutu girin:
   
        enable-migrations 
   
    Merhaba **enable-migrations** komut oluşturur bir *geçişler* klasöre ve bu klasörde koyar bir *Configuration.cs* dosya tooconfigure geçişler düzenleyebilirsiniz. 
3. Merhaba, **Paket Yöneticisi Konsolu** penceresinde hello aşağıdaki komutu girin:
   
        add-migration Initial
   
    Merhaba **add-migration ilk** komutu adlı bir sınıf oluşturur  **&lt;date_stamp&gt;ilk** hello veritabanı oluşturur. İlk parametre hello ( *ilk* ) rasgele ve kullanılan toocreate hello hello dosyasının adıdır. Merhaba yeni sınıf dosyalarında görebilirsiniz **Çözüm Gezgini**.
   
    Merhaba, **ilk** hello sınıfı **yukarı** yöntemi oluşturur hello kişiler tablosunu ve hello **aşağı** yöntemi (tooreturn toohello önceki durumuna istediğinizde kullanılır) bırakır.
4. Açık hello *Migrations\Configuration.cs* dosya. 
5. Ad alanları aşağıdaki hello ekleyin. 
   
         using ContactManager.Models;
6. Hello yerine *çekirdek* koddan hello yöntemiyle:
   
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
   
    Bu kodu yukarıdaki hello kişi bilgilerini hello veritabanıyla başlatacak. Hello veritabanı dengeli dağıtımı ile ilgili daha fazla bilgi için bkz: [hata ayıklama Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).
7. Merhaba, **Paket Yöneticisi Konsolu** hello komutu girin:
   
        update-database
   
    ![Paket Yöneticisi Konsolu komutları][addcode009]
   
    Merhaba **update-database** çalıştırır hello hello veritabanı oluşturan ilk geçiş. Varsayılan olarak, hello veritabanı bir SQL Server Express LocalDB veritabanı olarak oluşturulur.
8. CTRL + F5 toorun Merhaba uygulaması tuşuna basın. 

Merhaba uygulaması hello çekirdek veri gösterir ve düzenleme, Ayrıntılar ve delete bağlantılar sağlar.

![Verilerinin MVC görünümü][rxz3]

## <a name="edit-hello-view"></a>Merhaba Görünümü Düzenle
1. Açık hello *Views\Home\Index.cshtml* dosya. Merhaba sonraki adımda, biz oluşturulan hello biçimlendirme kullanan kodu ile değiştirir [jQuery](http://jquery.com/) ve [Knockout.js](http://knockoutjs.com/). Web API kullanarak bu yeni kodu hello kişilerinizin listesini alır ve JSON ve bağlamalar hello kişi veri toohello UI knockout.js kullanarak. Daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#nextsteps) Bu öğreticinin hello sonunda bölüm. 
2. Merhaba hello dosyasının içeriğini koddan hello ile değiştirin.
   
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
3. Merhaba içerik klasörünü sağ tıklatın ve **Ekle**ve ardından **yeni öğe...** .
   
    ![İçerik klasörünü bağlam menüsünde Stil sayfası ekleme][addcode005]
4. Merhaba, **Yeni Öğe Ekle** iletişim kutusunda, girin **stili** hello üst sağ arama kutusuna ve ardından **stil sayfası**.
    ![Yeni Öğe Ekle iletişim kutusu][rxStyle]
5. Ad hello dosyası *Contacts.css* tıklatıp **Ekle**. Merhaba hello dosyasının içeriğini koddan hello ile değiştirin.
   
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
   
    Merhaba düzeni, renkler ve hello Kişi Yöneticisi uygulamada kullanılan stiller bu stil sayfası kullanacağız.
6. Açık hello *App_Start\BundleConfig.cs* dosya.
7. Aşağıdaki kod tooregister hello hello eklemek [Boşaltılan](http://knockoutjs.com/index.html "KO") eklentisi.
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    Merhaba ekran şablonları işleyen Boşaltılan toosimplify dinamik JavaScript kodu kullanarak bu örnek.
8. Merhaba içeriği/css girişi tooregister hello değiştirme *contacts.css* stil sayfası. Merhaba satırı aşağıdaki gibi değiştirin:
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   Hedef:
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. Hello Paket Yöneticisi konsolu, komut tooinstall Boşaltılan aşağıdaki hello çalıştırın.
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a>Merhaba Web API Restful arabirimi için bir denetleyici ekleyin
1. İçinde **Çözüm Gezgini**, denetleyicileri sağ tıklatın ve **Ekle** ve ardından **denetleyicisi...** 
2. Merhaba, **İskele Ekle** iletişim kutusunda, girin **Web API 2 denetleyici Entity Framework kullanarak Eylemler ile** ve ardından **Ekle**.
   
    ![API denetleyicisi ekleme](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. Merhaba, **denetleyici Ekle** iletişim kutusunda, "ContactsController", denetleyici adı girin. "Kişiyi (ContactManager.Models)" Merhaba seçin **Model sınıfı**.  Merhaba hello için varsayılan değer tutmak **veri bağlamı sınıfı**. 
4. **Ekle**'ye tıklayın.

### <a name="run-hello-application-locally"></a>Merhaba uygulama yerel olarak çalıştırma
1. CTRL + F5 toorun Merhaba uygulaması tuşuna basın.
   
    ![Dizin sayfası][intro001]
2. Bir kişi girin ve tıklayın **Ekle**. Merhaba uygulama toohello giriş sayfasını döndürür ve girdiğiniz hello kişi görüntüler.
   
    ![Yapılacaklar listesi öğeleri içeren dizin sayfası][addwebapi004]
3. Merhaba tarayıcıda append **/api/contacts** toohello URL.
   
    Merhaba elde edilen URL http://localhost:1234/api/contacts sayfasında benzeyecektir. Merhaba RESTful web API'si eklediğiniz depolanan hello kişiler döndürür. Firefox ve Chrome hello verileri XML biçiminde görüntüler.
   
    ![Yapılacaklar listesi öğeleri içeren dizin sayfası][rxFFchrome]

    IE tooopen isteyebilir veya hello kişiler kaydedin.

    ![Web API Kaydet iletişim kutusu][addwebapi006]


    Not Defteri veya bir tarayıcı kişiler döndürülen hello açabilirsiniz.

    Bu çıktı, mobil web sayfası veya uygulama gibi başka bir uygulama tarafından kullanılabilecek.

    ![Web API Kaydet iletişim kutusu][addwebapi007]

    **Güvenlik Uyarısı**: Bu noktada, güvenli olmayan ve güvenlik açığı tooCSRF saldırı uygulamasıdır. Daha sonra hello öğreticide Biz bu güvenlik açığından kaldırır. Daha fazla bilgi için bkz: [önleme siteler arası istek sahteciliği (CSRF) saldırılarını][prevent-csrf-attacks].
## <a name="add-xsrf-protection"></a>XSRF koruma Ekle
Siteler arası istek sahtekarlığı (XSRF veya CSRF olarak da bilinir) kötü amaçlı bir Web sitesi istemci tarayıcısına ve bu tarayıcı tarafından güvenilen bir Web sitesi arasındaki hello etkileşim yapabildiği etkileyebilir web barındırılan uygulamalara yönelik bir saldırı ' dir. Web tarayıcıları kimlik doğrulama belirteçleri her isteği tooa Web sitesi ile otomatik olarak gönderecektir çünkü bu saldırıların olası yapılır. Merhaba klasik ASP gibi bir kimlik doğrulama tanımlama bilgisini bir örneğidir. NET'in form kimlik doğrulaması bileti. Ancak, tüm kalıcı kimlik doğrulama mekanizması (örneğin, Windows kimlik doğrulaması, temel ve benzeri) kullanan Web siteleri tarafından bu saldırıların hedeflenebilir.

Bir kimlik avı saldırıdan XSRF saldırının farklıdır. Kimlik avı saldırıları hello kurban müdahalesini gerektirir. Bir kimlik avı saldırısı kötü amaçlı bir Web sitesi hello hedef Web sitesi benzetimini yapacak ve hello kurban hassas bilgileri toohello saldırgan sağlama içine sizi kandırmalarına. Bir XSRF saldırısında, genellikle bir etkileşim yoktur hello kurban gerekli. Bunun yerine, hello saldırgan tüm ilgili tanımlama bilgilerini toohello hedef Web sitesi otomatik olarak göndermeye hello tarayıcıya bağlı olan.

Daha fazla bilgi için bkz: Merhaba [açık Web uygulaması güvenlik projesi](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).

1. İçinde **Çözüm Gezgini**, sağ **ContactManager** proje ve tıklatın **Ekle** ve ardından **sınıfı**.
2. Ad hello dosyası *ValidateHttpAntiForgeryTokenAttribute.cs* ve hello aşağıdaki kodu ekleyin:
   
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
3. Merhaba aşağıdakileri ekleyin *kullanarak* deyimi toohello sözleşmeler denetleyicisi erişim toohello alacak şekilde **[ValidateHttpAntiForgeryToken]** özniteliği.
   
        using ContactManager.Filters;
4. Merhaba eklemek **[ValidateHttpAntiForgeryToken]** toohello Post yöntemleri hello özniteliği **ContactsController** tooprotect, XSRF tehditlere karşı. Toohello "PutContact", "PostContact" ekleyecek ve **DeleteContact** eylem yöntemleri.
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. Güncelleştirme hello *betikleri* hello bölümünü *Views\Home\Index.cshtml* tooinclude kod tooget hello XSRF belirteçleri dosya.
   
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

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a>Yayımlama Hello uygulama güncelleştirme tooAzure ve SQL veritabanı
toopublish hello uygulama, daha önce uyguladığınız hello yordamı yineleyin.

1. İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve seçin **Yayımla**.
   
    ![Yayımlama][rxP]
2. Merhaba tıklatın **ayarları** sekmesi.
3. Altında **ContactsManagerContext(ContactsManagerContext)**, hello tıklatın **v** simgesi toochange *uzak bağlantı dizesi* toohello bağlantı dizesi hello başvurun Veritabanı. Tıklatın **ContactDB**.
   
    ![Ayarlar](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. Merhaba kutuyu **yürütme önce kod uygulamalı geçişler (uygulama başlatılırken çalışır)**.
5. Tıklatın **sonraki** ve ardından **Önizleme**. Visual Studio eklenen veya güncelleştirilen hello dosyaların bir listesini görüntüler.
6. **Yayımla**’ta tıklayın.
   Merhaba dağıtım tamamlandıktan sonra hello tarayıcı Merhaba uygulaması toohello giriş sayfasını açar.
   
    ![Hiçbir kişilerle dizin sayfası][intro001]
   
    dağıtılan hello Hello Visual Studio yayımlama işlemi otomatik olarak yapılandırılan hello bağlantı dizesi *Web.config* toopoint toohello SQL veritabanı dosyası. Ayrıca, hello ilk zaman Merhaba uygulaması hello veritabanına dağıtımdan sonra erişir Code First Migrations tooautomatically yükseltme hello veritabanı toohello en son sürümü yapılandırılır.
   
    Bu yapılandırma sonucunda Code First hello veritabanı hello hello kod çalıştırarak oluşturulan **ilk** daha önce oluşturduğunuz sınıfı. Dağıtımdan sonra bu hello ilk zaman hello çalıştığınız uygulama tooaccess hello veritabanı yaptınız.
7. Yerel olarak hello uygulama veritabanı dağıtımı başarılı oldu tooverify çalıştırdığınızda yaptığınız gibi bir kişi girin.

Girdiğiniz hello öğenin kaydedilir ve hello Kişi Yöneticisi sayfada görünen gördüğünüzde hello veritabanında depolandı bilirsiniz.

![Kişilerle dizin sayfası][addwebapi004]

Merhaba uygulaması artık hello bulutta SQL veritabanı toostore kullanarak verileri çalışıyor. Azure'da hello uygulamayı test ettikten sonra silin. Merhaba uygulamanın genel ve mekanizması toolimit erişimi yok.

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="next-steps"></a>Sonraki Adımlar
Başka bir şekilde toostore bir Azure uygulamasında toouse ilişkisel olmayan verileri depolama BLOB'ları ve tabloları hello biçiminde sağlayan Azure depolama verilerdir. bağlantılar aşağıdaki hello Web API, ASP.NET MVC ve Windows Azure üzerinde daha fazla bilgi sağlar.

* [MVC kullanarak Entity Framework ile çalışmaya başlama][EFCodeFirstMVCTutorial]
* [Giriş tooASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [İlk ASP.NET Web API](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [WAWS hata ayıklama](web-sites-dotnet-troubleshoot-visual-studio.md)

Bu öğretici ve hello örnek uygulaması tarafından yazıldı [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) zel Dykstra ve Hakan Dorrans yardımla (Twitter [ @blowdart ](https://twitter.com/blowdart)). 

Lütfen geri bildirim neleri beğendiğinizi veya yalnızca hello öğretici kendisi hakkında aynı zamanda bu gösteren hello ürünlerle ilgili, geliştirilmiş toosee ister misiniz bırakın. Geri bildiriminiz geliştirmeleri belirlememize yardımcı olur. Yapılandırma ve dağıtma hello üyelik veritabanının daha fazla Otomasyon hello işlemi için ne kadar ilgi var olduğunu bulma özellikle ilginizi duyuyoruz. 

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

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

