---
title: "Azure App Service'te bir ASP.NET MVC 5 aaaDeploy mobil web uygulaması"
description: "Nasıl toodeploy bir web uygulaması tooAzure App Service mobile kullanarak ASP.NET MVC 5 web uygulaması özellikleri öğretilmektedir öğretici."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 0752c802-8609-4956-a755-686116913645
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 01119c07246c0252fd357562774a2e90b3ef77d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a>Azure App Service'te bir ASP.NET MVC 5 mobil web uygulaması dağıtma
Bu öğretici nasıl toobuild bir ASP.NET MVC 5 web, mobil dostu uygulamasını temellerini hello ve tooAzure uygulama hizmeti dağıtma öğretir. Bu öğretici için gereksinim duyduğunuz [için Visual Studio Express 2013 Web] [ Visual Studio Express 2013] veya hello professional, zaten varsa, Visual Studio sürümü. Kullanabileceğiniz [Visual Studio 2015] ancak hello ekran görüntüleri farklı olacaktır ve hello ASP.NET 4.x şablonları kullanmanız gerekir.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a>Ne oluşturacağınız
Bu öğretici için sağlanan mobil özellikleri toohello basit konferans listeleme uygulama hello ekleyeceksiniz [başlangıç projesi][StarterProject]. Merhaba aşağıdaki ekran görüntüsü hello ASP.NET oturumları tamamlandı hello uygulamada, Internet Explorer 11 F12 geliştirici araçları hello tarayıcı öykünücüsünde görüldüğü gibi gösterir.

![][FixedSessionsByTag]

Internet Explorer 11 F12 hello geliştirici araçları ve hello kullanabilirsiniz [Fiddler aracı] [ Fiddler] toohelp uygulamanızın hatalarını ayıklama. 

## <a name="skills-youll-learn"></a>Bilgi edineceksiniz yetenekleri
Öğrenecekleriniz aşağıda verilmiştir:

* Nasıl toouse Visual Studio 2013 toopublish web uygulamanızı doğrudan Azure App Service'teki web uygulamasına tooa.
* Nasıl mobil cihazlarda görünen geliştirmek için hello CSS önyükleme framework hello ASP.NET MVC 5 şablonlarını kullanma
* Nasıl hello iPhone ve Android gibi tootarget belirli mobil tarayıcılar toocreate mobile özgü görünümler
* Nasıl toocreate esnek görünümler (aygıtlarda toodifferent tarayıcılar yanıt görünümler)

## <a name="set-up-hello-development-environment"></a>Merhaba geliştirme ortamını ayarlama
2.5.1 .NET için Azure SDK'sı hello yükleyerek geliştirme ortamınızı ayarlayın veya sonraki bir sürümü. 

1. .NET için Azure SDK tooinstall hello hello bağlantıyı tıklatın. Henüz yüklü Visual Studio 2013 yoksa, hello bağlantı tarafından yüklenir. Bu öğreticide Visual Studio 2013 gerektirir. [Visual Studio 2013 için Azure SDK][AzureSDKVs2013]
2. Merhaba Web Platformu yükleyicisi penceresinde **yüklemek** ve hello yükleme işlemine devam edin.

Bir mobil tarayıcı öykünücüsü de gerekir. Merhaba aşağıdakilerden herhangi birini çalışır:

* Tarayıcı öykünücüsünde [Internet Explorer 11 F12 Geliştirici Araçları] [ EmulatorIE11] (tüm mobil tarayıcı ekran görüntülerinde kullanılır). Windows Phone 8, Windows Phone 7 ve Apple iPad için kullanıcı aracısı dizesi hazır sahiptir.
* Tarayıcı öykünücüsünde [Google Chrome DevTools][EmulatorChrome]. Çok sayıda Android aygıtların yanı sıra Apple iPhone, Apple iPad ve Amazon Kindle yangın için hazır ayarları içerir. Ayrıca, dokunma olayları öykünür.
* [Opera Mobile öykünücüsü][EmulatorOpera]

C ile Visual Studio projeleri\# kaynak kodu bu konuda kullanılabilir tooaccompany şunlardır:

* [Başlangıç projesi indirme][StarterProject]
* [Proje indirme tamamlandı][CompletedProject]

## <a name="bkmk_DeployStarterProject"></a>Merhaba başlangıç projesi tooan Azure web uygulaması dağıtma
1. Merhaba konferans listeleme uygulamayı karşıdan [başlangıç projesi][StarterProject].
2. Ardından Windows Gezgini'nde, indirilen hello ZIP dosyasını sağ tıklatın ve seçin *özellikleri*.
3. Merhaba, **özellikleri** iletişim kutusunda, hello seçin **Engellemeyi Kaldır** düğmesi. (Engellemelerini kaldırma toouse çalıştığınızda oluşan bir güvenlik uyarısı engelleyen bir *.zip* hello Web'den indirdiğiniz dosya.)
4. Merhaba ZIP dosyasını sağ tıklatın ve seçin **tümünü Ayıkla** hello dosya sıkıştırmasını açmak için. 
5. Visual Studio'da hello açın *C#\Mvc5Mobile.sln* dosya.
6. Çözüm Gezgini'nde, hello projesine sağ tıklayın ve **Yayımla**.
   
   ![][DeployClickPublish]
7. Web'de yayımlama tıklatın **Microsoft Azure App Service**.
   
   ![][DeployClickWebSites]
8. Azure'da oturum zaten yapmadıysanız, tıklatın **Hesap Ekle**.
   
   ![][DeploySignIn]
9. Merhaba istemleri toolog Azure hesabınızda izleyin.
10. Merhaba App Service iletişim şimdi oturum gibi göstermelidir. **Yeni**’ye tıklayın.
    
    ![][DeployNewWebsite]  
11. Merhaba, **Web uygulaması adı** alanında, benzersiz uygulama adı ön ekini belirtin. Tam web uygulaması adı olacaktır  *&lt;öneki >*. azurewebsites.net. Ayrıca, seçin veya yeni bir kaynak grubu adı belirtin **kaynak grubu**. Ardından **yeni** toocreate yeni bir uygulama hizmeti planı.
    
    ![][DeploySiteSettings]
12. Merhaba yeni uygulama hizmeti planı yapılandırmak ve tıklatın **Tamam**. 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. Geri hello App Service Oluştur iletişim kutusunda tıklatın **oluşturma**.
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. Hello Azure kaynaklarını oluşturulduktan sonra hello Web Yayımla iletişim yeni uygulamanızı hello ayarları ile doldurulur. **Yayımla**’ta tıklayın.
    
    ![][DeployPublishSite]
    
    Visual Studio yayımlama hello başlangıç projesi toohello Azure web uygulaması tamamlandığında toodisplay hello canlı web uygulaması hello Masaüstü tarayıcı penceresinde açar.
15. Mobil tarayıcı öykünücüsü'ı başlatın, Merhaba konferans uygulaması hello URL'sini kopyalayın (*<prefix>*. azurewebsites.net) hello öykünücüsü içine sağ üst düğmesini tıklatın ve seçin **etiketegöreGözat**. Merhaba varsayılan tarayıcı olarak Internet Explorer 11 kullanıyorsanız, tootype yeterlidir `F12`, ardından `Ctrl+8`, hello tarayıcı profilini çok değiştirmek**Windows Phone**. Aşağıdaki görüntü hello gösterir *AllTags* dikey modunda görüntüle (seçme gelen **etikete göre Gözat**).
    
    ![][AllTags]

> [!TIP]
> MVC 5 uygulamanızı Visual Studio'dan ayıklayabilirsiniz olsa da, web uygulaması tooAzure yayımlayabilirsiniz yeniden tooverify hello canlı web uygulamasından doğrudan mobil, tarayıcı veya tarayıcı öykünücüsü.
> 
> 

Merhaba görünen bir mobil cihazda çok okunabilir durumdadır. Merhaba görsel efektler hello önyükleme CSS çerçevesi tarafından uygulanan bazıları da zaten görebilirsiniz.
Merhaba tıklatın **ASP.NET** bağlantı.

![][SessionsByTagASP.NET]

Merhaba ASP.NET etiket görünümünü önyükleme sizin için otomatik olarak yapar yakınlaştırma donatılmıştır toohello ekrandır. Ancak, bu görünüm toobetter seri hello mobil tarayıcı artırabilir. Örneğin, hello **tarih** okumak sütun zordur. Daha sonra hello öğreticide hello değiştireceğiz *AllTags* toomake görüntülemek, mobil dostu.

## <a name="bkmk_bootstrap"></a>Önyükleme CSS Framework
Yeni hello MVC 5 yerleşik önyükleme destek şablonudur. Nasıl hello farklı görünümleri, uygulamanızda hemen artırır zaten gördünüz. Örneğin, Hello tarayıcı genişliği daha küçük olduğunda hello gezinti çubuğu hello üstünde otomatik olarak daraltılabilir. Hello Masaüstü tarayıcının hello tarayıcı penceresini yeniden boyutlandırmayı deneyin ve hello gezinti çubuğu kendi görünüm nasıl değiştiğini görebilirsiniz. Önyükleme yerleşik hello yanıt veren web tasarımı budur.

Merhaba Web uygulaması önyükleme görünür nasıl toosee açmak *uygulama\_Başlat\\BundleConfig.cs* ve açıklamayı içeren hello satırları *bootstrap.js* ve *bootstrap.css*. Merhaba aşağıdaki kod hello hello son iki bilgilerinin gösterir `RegisterBundles` yöntemi hello değişiklikten sonra:

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

Tuşuna `Ctrl+F5` toorun Merhaba uygulaması.

Bu hello daraltılabilir gezinti çubuğu sunulmuştur yalnızca normal sırasız bir listesini inceleyin. Tıklatın **etikete göre Gözat** yeniden, ardından **ASP.NET**.
Merhaba mobil öykünücü görünümünde, artık yakınlaştırma donatılmıştır toohello ekran değildir ve sipariş toosee hello sağ tarafında Merhaba tablonun yana kaydırma gerekir göre görebilirsiniz.

![][SessionsByTagASP.NETNoBootstrap]

Yaptığınız değişiklikleri geri almak ve mobil dostu görünen hello yenileme hello mobil tarayıcı tooverify geri yüklendi.

Önyükleme belirli tooASP.NET MVC 5 değildir ve herhangi bir web uygulamasında bu özelliklerden yararlanabilirsiniz. Ancak, MVC 5 Web uygulaması önyükleme varsayılan olarak yararlanabilir böylece artık ASP.NET MVC 5 proje şablonuna kuruludur.

Önyükleme hakkında daha fazla bilgi için toothe Git [önyükleme] [ BootstrapSite] site.

Merhaba sonraki bölümde göreceğiniz nasıl tooprovide mobil tarayıcı özel görünümler.

## <a name="bkmk_overrideviews"></a>Merhaba görünümleri, düzenleri ve kısmi görünümler geçersiz kıl
Genel olarak, tek bir mobil tarayıcı için veya belirli bir tarayıcı için mobil tarayıcılar için (düzenler ve kısmi görünümler dahil) herhangi bir görünüm geçersiz kılabilirsiniz. mobile özgü tooprovide görüntülemek için bir görünüm dosyasını kopyalayın ve ekleme *. Mobil* toohello dosya adı. Örneğin, bir mobil toocreate *dizin* görünümü kopyalayabilir *görünümleri\\giriş\\Index.cshtml* için *görünümleri\\giriş\\ Index.Mobile.cshtml*.

Bu bölümde, bir mobil özgü Düzen dosyası oluşturacaksınız.

toostart, kopya *görünümleri\\paylaşılan\\\_Layout.cshtml* için *görünümleri\\paylaşılan\\\_Layout.Mobile.cshtml* . Açık  *\_Layout.Mobile.cshtml* hello başlığını değiştirip **MVC5 uygulama** çok**MVC5 uygulama (mobil)**.

Her `Html.ActionLink` çağırmak için hello gezinti çubuğu, "her bağlantısını gözatma türü" kaldırmak *ActionLink*. Merhaba aşağıdaki kod gösterir tamamlandı hello `<ul class="nav navbar-nav">` hello mobil düzeni dosyasının etiketi.

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

Kopya hello *görünümleri\\giriş\\AllTags.cshtml* dosya *görünümleri\\giriş\\AllTags.Mobile.cshtml*. Merhaba yeni dosyasını açın ve değişiklik `<h2>` "Etiketleri" öğesinden çok "etiketler (M)":

    <h2>Tags (M)</h2>

Bir masaüstü tarayıcısı kullanarak ve mobil tarayıcı öykünücüsü kullanarak toohello etiketleri sayfasına göz atın. Merhaba mobil tarayıcı öykünücüsü iki değişiklik yaptığınız hello gösterir (Merhaba başlığını  *\_Layout.Mobile.cshtml* ve hello başlığını *AllTags.Mobile.cshtml*).

![][AllTagsMobile_LayoutMobile]

Buna karşılık, hello Masaüstü görüntü değişmediğini (başlıkları ile  *\_Layout.cshtml* ve *AllTags.cshtml*).

![][AllTagsMobile_LayoutMobileDesktop]

## <a name="bkmk_browserviews"></a>Tarayıcı özel görünümlerini oluşturma
Ayrıca toomobile ve Masaüstü özgü görünümler, tek bir tarayıcı için görünümler oluşturabilirsiniz. Örneğin, özellikle hello iPhone veya hello Android tarayıcı görünümler oluşturabilirsiniz. Bu bölümde, hello iPhone tarayıcı ve hello iPhone sürümü için bir düzen oluşturacaksınız *AllTags* görünümü.

Açık hello *Global.asax* dosyasını ve kod toohello altına aşağıdaki hello eklemek `Application_Start` yöntemi.

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

Bu kod, "her gelen istek karşı eşleşen iPhone" adlı yeni bir görüntü modu tanımlar. Merhaba gelen istek (diğer bir deyişle, hello kullanıcı aracısı hello dizesi "iPhone" içeriyorsa), tanımlanmış bir koşulu eşleşirse, ASP.NET MVC için görünümleri adında "iPhone" soneki içeren arar.

> [!NOTE]
> Mobil tarayıcı özgü ekleme görüntülediğinizde modları, gibi iPhone ve Android için olması emin tooset hello ilk bağımsız değişkeni çok`0` (Merhaba listenin hello Ekle) toomake bu hello tarayıcıya özgü modu hello mobil şablonu göre önceliklidir emin (*. Mobile.cshtml). Merhaba mobil şablonu hello hello listesinin başında yerine ise, bu, hedeflenen görüntü modu seçilir (ilk eşleşme WINS hello ve eşleşen tüm mobil tarayıcılar hello mobil şablonu). 
> 
> 

Merhaba kodda sağ `DefaultDisplayMode`, seçin **gidermek**ve ardından `using System.Web.WebPages;`. Bu başvuru toothe ekler `System.Web.WebPages` yerdir ad alanı `DisplayModeProvider` ve `DefaultDisplayMode` türleri tanımlanmıştır.

![][ResolveDefaultDisplayMode]

Alternatif olarak, aşağıdaki satırı toothe hello yalnızca el ile ekleyebileceğiniz `using` hello dosyasının bölümü.

    using System.Web.WebPages;

Merhaba değişiklikleri kaydedin. Kopya *görünümleri\\paylaşılan\\\_Layout.Mobile.cshtml* dosya *görünümleri\\paylaşılan\\\_Layout.iPhone.cshtml*. Merhaba yeni dosyasını açın ve hello başlığını değiştirme `MVC5 Application (Mobile)` için `MVC5 Application (iPhone)`.

Kopya hello *görünümleri\\giriş\\AllTags.Mobile.cshtml* dosya *görünümleri\\giriş\\AllTags.iPhone.cshtml*. Merhaba Hello yeni dosyasında değişiklik `<h2>` öğesi öğesinden "etiketler (M)" çok "etiketler (iPhone)".

Merhaba uygulamayı çalıştırın. Bir mobil tarayıcı öykünücüsü çalıştırmak, kendi kullanıcı aracısı çok ayarlandığından emin olun "iPhone" ve toohello Gözat *AllTags* görünümü. Internet Explorer 11 F12 geliştirici araçları hello öykünücüsü kullanıyorsanız, öykünme toohello aşağıdakileri yapılandırın:

* Tarayıcı profili = **Windows Phone**
* Kullanıcı aracısı dizesi = **özel**
* Özel bir dize = **Apple-iPhone5C1/1001.525**

Merhaba aşağıdaki ekran gösterilir hello *AllTags* Internet Explorer 11 F12 geliştirici araçları hello özel kullanıcı aracısı dizesi ile öykünücüde işlenmiş Görünüm (Bu, bir iPhone 5 C kullanıcı aracısı dizesi).

![][AllTagsIPhone_LayoutIPhone]

Merhaba mobil tarayıcıda hello seçin **konuşmacılar** bağlantı. Mobil bir görünüm olduğundan (*AllSpeakers.Mobile.cshtml*), hello varsayılan konuşmacılar görüntülemek (*AllSpeakers.cshtml*) hello mobil düzeni görünümü kullanılarak oluşturulması ( *\_ Layout.Mobile.cshtml*). Merhaba başlık aşağıda gösterildiği gibi **MVC5 uygulama (mobil)** tanımlanan  *\_Layout.Mobile.cshtml*.

![][AllSpeakers_LayoutMobile]

Ayarlayarak genel işleme mobil düzeni içinde varsayılan (mobil olmayan) görünümünden devre dışı bırakabilirsiniz `RequireConsistentDisplayMode` için `true` hello içinde *görünümleri\\\_ViewStart.cshtml* dosyası şuna benzer:

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

Zaman `RequireConsistentDisplayMode` çok ayarlanır`true`, hello mobil Düzen (*\_Layout.Mobile.cshtml*) yalnızca mobil görünümleri için kullanılır (yani görünüm dosyası hello biçiminde olduğunda  ***Görünümadı** . Mobile.cshtml*). Tooset isteyebilirsiniz `RequireConsistentDisplayMode` çok`true` mobil düzeninizi iyi mobil olmayan görünümlerle işe yaramazsa. Merhaba ekran görüntüsü aşağıda gösterilmiştir nasıl hello *konuşmacılar* sayfasını işler `RequireConsistentDisplayMode` çok ayarlanır`true` (olmadan hello dizesindeki "(mobil)" Merhaba hello üstünde gezinti çubuğu).

![][AllSpeakers_LayoutMobileOverridden]

Ayarlayarak belirli bir görünümde tutarlı görüntü modu devre dışı bırakabilirsiniz `RequireConsistentDisplayMode` çok`false` hello görünüm dosyasında. Merhaba aşağıdaki biçimlendirmede *görünümleri\\giriş\\AllSpeakers.cshtml* dosya kümeleri `RequireConsistentDisplayMode` çok`false`:

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

Bu bölümde gördük nasıl toocreate mobil düzenleri ve görünümler ve iPhone toocreate düzenleri ve görünümler gibi belirli cihazlar için nasıl hello.
Ancak, tek bir stil Masaüstü, telefon ve tablet tarayıcılar toocreate tutarlı bir görünüm arasında uygulanabilir anlamına gelir esnek düzeni hello ana avantajı hello önyükleme CSS framework'ün olmasıdır. Merhaba sonraki bölümde nasıl tooleverage Bootstrap toocreate mobil dostu görürsünüz görünümleri.

## <a name="bkmk_Improvespeakerslist"></a>Merhaba konuşmacılar listesi geliştirmek
Yalnızca anlatıldığı gibi hello *konuşmacılar* görünümdür okunabilir ancak hello bağlantılar küçük olduğunda ve bir mobil cihazda zor tootap. Bu bölümde, hello yapacağız *AllSpeakers* büyük, dokunun kolay bağlantıları görüntüler ve arama kutusu tooquickly içeren görünümü mobil dostu konuşmacılar bulur.

Merhaba önyükleme kullanabilirsiniz [bağlantılı listesi grubu] [ linked list group] hello artırmak için stil *konuşmacılar* görünümü. İçinde *görünümleri\\giriş\\AllSpeakers.cshtml*, hello hello Razor dosyasının içeriğini aşağıdaki hello kod ile değiştirin.

     @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, "SessionsBySpeaker", new { speaker }, new { @class = "list-group-item" })
        }
    </div>

Merhaba `class="list-group"` hello özniteliğinde `<div>` etiket uygular önyükleme listesi stil ve hello `class="input-group-item"` özniteliği önyükleme liste öğesi stil tooeach bağlantısını uygular.

Merhaba mobil tarayıcıyı yenileyin. Bu görünüm görülüyor Hello güncelleştirildi:

![][AllSpeakersFixed]

Merhaba önyükleme [bağlantılı listesi grubu] [ linked list group] stil kadar daha iyi bir kullanıcı deneyimi olan hello tüm kutusunu tıklanabilir, her bağlantı için yapar. Toothe Masaüstü görünümüne geçin ve hello tutarlı bir görünüm gözlemleyin.

![][AllSpeakersFixedDesktop]

Merhaba mobil tarayıcı görünümü geliştirilmiştir rağmen hello uzun konuşmacılar listesi gidin zordur. Önyükleme bir arama filtresi işlevselliği out-of--box sağlamaz, ancak birkaç kod satırıyla, ekleyebilirsiniz. İlk arama kutusu toohello görünümü ekleme sonra hello hello filtre işlevi için JavaScript kodu kanca. İçinde *görünümleri\\giriş\\AllSpeakers.cshtml*, ekleme bir \<form\> etiketi hello hemen sonra \<h2\> , aşağıda gösterildiği gibi etiketi:

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <form class="input-group">
        <span class="input-group-addon"><span class="glyphicon glyphicon-search"></span></span>
        <input type="text" class="form-control" placeholder="Search speaker">
    </form>
    <br />
    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class = "list-group-item" })
        }
    </div>

Bu hello fark `<form>` ve `<input>` etiketlere hem de hello uygulanan önyükleme stilleri toothem sahip. Merhaba `<span>` öğesi ekler bir önyükleme [glyphicon] [ glyphicon] toothe arama kutusu.

Merhaba, *betikleri* klasörü, adlandırılan bir JavaScript dosyası ekleme *filter.js*. Merhaba dosyasını açın ve kod içine aşağıdaki hello yapıştırın:

    $(function () {

        // reset hello search form when hello page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up hello events toohello <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with hello typed text and hide others
            for (var i = 0; i < items.length; i++) {
                var val = items[i].text.toLowerCase();
                val = val.substring(0, searchtxt.length);
                if (val == searchtxt) {
                    $(items[i]).show();
                }
                else {
                    $(items[i]).hide();
                }
            }
        });
    });

Ayrıca, kayıtlı paketlerin tooinclude filter.js gerekir. Açık *uygulama\_Başlat\\BundleConfig.cs* ve hello ilk paketleri değiştirin. İlk değiştirme `bundles.Add` deyimi (hello için **jquery** paket) tooinclude *betikleri\\filter.js*aşağıdaki gibi:

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

Merhaba **jquery** paket hello varsayılan olarak zaten işlenmiş  *\_düzeni* görünümü. Daha sonra hello kullanabilir aynı JavaScript kodu tooapply filtre işlevselliği tooother liste görünümleri.

Merhaba mobil tarayıcıyı yenileyin ve Git toohello *AllSpeakers* görünümü. Arama kutusuna "sc" yazın. Merhaba konuşmacılar listesi şimdi tooyour arama dizesi göre filtrelenmelidir.

![][AllSpeakersFixedSearchBySC]

## <a name="bkmk_improvetags"></a>Merhaba Etiketler listesi geliştirmek
Hello gibi *konuşmacılar* hello görünümü *etiketleri* görünümdür okunabilir ancak hello bağlantılardır mobil aygıttaki zor ve küçük tootap. Merhaba düzeltebilirsiniz *etiketleri* görünüm hello aynı şekilde hello düzeltme *konuşmacılar* daha önce ancak hello aşağıda açıklanan hello kod değişiklikleri kullanırsanız, görüntülemek `Html.ActionLink` yöntemi sözdiziminde  *Görünümler\\giriş\\AllTags.cshtml*:

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

Merhaba Masaüstü tarayıcısı görünümler gibi yenilenir:

![][AllTagsFixedDesktop]

Ve mobil tarayıcı görünümler gibi hello yenilenir: 

![][AllTagsFixed]

> [!NOTE]
> Bu hello özgün liste biçimlendirmesini fark ederseniz yine de var. mobil tarayıcı hello ve ne oldu tooyour iyi önyükleme stil merak ediyor; Bu, önceki eylem toocreate mobil belirli görünüm bir yapı Ancak, hello önyükleme CSS framework toocreate yanıt veren web tasarımı kullanıyorsanız, head gidin ve bu mobile özgü görünümler ve hello mobile özgü Düzen görünümleri kaldırın. Bunu yaptıktan sonra hello yenilendi mobil tarayıcı hello önyükleme stil gösterir.
> 
> 

## <a name="bkmk_improvedates"></a>Merhaba tarihleri listesi geliştirmek
Merhaba artırabilir *tarihleri* hello geliştirilmiş gibi görüntülemek *konuşmacılar* ve *etiketleri* daha önce ancak aşağıdaki hello açıklanan hello kod değişiklikleri kullanırsanızgörünümleri`Html.ActionLink` yöntemi sözdiziminde *görünümleri\\giriş\\AllDates.cshtml*:

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

Böyle bir yenilenen mobil tarayıcı görünümü alırsınız:

![][AllDatesFixed]

Daha fazla hello artırabilir *tarihleri* tarihe göre hello tarih-saat değerlerini düzenleme görünümü. Bu önyükleme hello ile yapılabilir [paneller] [ panels] stil oluşturma. Merhaba Hello içeriğini değiştirin *görünümleri\\giriş\\AllDates.cshtml* aşağıdaki kod ile dosya:

    @model IEnumerable<DateTime>

    @{
        ViewBag.Title = "All Dates";
    }

    <h2>Dates</h2>

    @foreach (var dategroup in Model.GroupBy(x=>x.Date))
    {
        <div class="panel panel-primary">
            <div class="panel-heading">
                @dategroup.Key.ToString("ddd, MMM dd")
            </div>
            <div class="panel-body list-group">
                @foreach (var date in dategroup)
                {
                    @Html.ActionLink(date.ToString("h:mm tt"), 
                                     "SessionsByDate", 
                                     new { date }, 
                                     new { @class = "list-group-item" })
                }
            </div>
        </div>
    }

Bu kod ayrı bir oluşturur `<div class="panel panel-primary">` her farklı tarih hello listesi ve kullandığı hello için etiket [bağlantılı listesi grubu] [ linked list group] ilgili için bağlantılar olarak önce. Bu kod çalıştığında gibi görünüyor hangi hello mobil tarayıcı şöyledir:

![][AllDatesFixed2]

Anahtar toohello Masaüstü tarayıcısı. Yeniden hello tutarlı bir görünüm unutmayın.

![][AllDatesFixed2Desktop]

## <a name="bkmk_improvesessionstable"></a>Merhaba SessionsTable görünüm geliştirmek
Bu bölümde, hello yapacağız *SessionsTable* daha fazla mobil dostu görüntüleyin. Daha kapsamlı hello önceki değişiklikler değişikliktir.

Merhaba mobil tarayıcıda hello dokunun **etiketi** düğmesine ve ardından girin `asp` arama kutusuna.

![][AllTagsFixedSearchByASP]

Merhaba dokunun **ASP.NET** bağlantı.

![][SessionsTableTagASP.NET]

Gördüğünüz gibi hello görüntü şu anda tasarlanmış toobe hello Masaüstü tarayıcıda görüntülenen olan bir tablo olarak biçimlendirilir. Ancak, bir mobil tarayıcı üzerinde biraz zor tooread olur. toofix Bu, açık *görünümleri\\giriş\\SessionsTable.cshtml* ve ardından dosya Merhaba içeriğine koddan hello ile değiştirin:

    @model IEnumerable<Mvc5Mobile.Models.Session>

    <h2>@ViewBag.Title</h2>

    <div class="container">
        <div class="row">
            @foreach (var session in Model)
            {
                <div class="col-md-4">
                    <div class="list-group">
                        @Html.ActionLink(session.Title, 
                                         "SessionByCode", 
                                         new { session.Code }, 
                                         new { @class="list-group-item active" })
                        <div class="list-group-item">
                            <div class="list-group-item-text">
                                @Html.Partial("_SpeakersLinks", session)
                            </div>
                            <div class="list-group-item-info">
                                @session.DateText
                            </div>
                            <div class="list-group-item-info small hidden-xs">
                                @Html.Partial("_TagsLinks", session)
                            </div>
                        </div>
                    </div>
                </div>
            }
        </div>
    </div>

Merhaba kod 3 işlemi yapar:

* kullandığı hello önyükleme [özel bağlantılı listesi grubu] [ custom linked list group] bu bilgileri (sınıflar gibi kullanarak bir mobil tarayıcı üzerinde okunabilir olmasını sağlamak tooformat oturum bilgilerini dikey olarak hello. Liste-Grup-öğesi-metin)
* Merhaba geçerlidir [kılavuz sistem] [ grid system] toothe düzeni, bu nedenle bu hello oturum öğelerini akış yatay tarayıcıda hello Masaüstü ve dikey olarak hello mobil tarayıcıda (Merhaba sütun md 4 sınıfı kullanarak)
* kullandığı hello [esnek yardımcı programları] [ responsive utilities] (Merhaba gizli xs sınıfı kullanarak) hello mobil tarayıcıda görüntülendiğinde hello oturum etiketlerini gizlemek için

Ayrıca bir başlık bağlantı toogo toohello ilgili oturumu dokunabilirsiniz. Aşağıdaki Hello görüntü hello kod değişiklikleri yansıtır.

![][FixedSessionsByTag]

otomatik olarak uygulanan hello önyükleme kılavuz sistem hello mobil tarayıcı oturumlarında dikey düzenler. Ayrıca, hello etiketleri gösterilmez dikkat edin. Anahtar toohello Masaüstü tarayıcısı.

![][SessionsTableFixedTagASP.NETDesktop]

Merhaba Masaüstü tarayıcıda hello etiketleri şimdi görüntülenen dikkat edin. Ayrıca, uyguladığınız hello önyükleme kılavuz sistem hello oturum öğeleri iki sütunlardaki düzenler görebilirsiniz. Tarayıcı büyütmek, hello düzenleme toothree sütunları değiştiğini görürsünüz.

## <a name="bkmk_improvesessionbycode"></a>Merhaba SessionByCode görünüm geliştirmek
Son olarak, hello düzeltme *SessionByCode* toomake görüntülemek, mobil dostu.

Merhaba mobil tarayıcıda hello dokunun **etiketi** düğmesine ve ardından girin `asp` arama kutusuna.

![][AllTagsFixedSearchByASP]

Merhaba dokunun **ASP.NET** bağlantı. Merhaba ASP.NET etiketi oturumlar görüntülenir.

![][FixedSessionsByTag]

Merhaba seçin **ASP.NET ve AngularJS ile tek sayfa uygulaması oluşturma** bağlantı.

![][SessionByCode3-644]

Merhaba varsayılan masaüstü görünümünde sorun yoktur, ancak bazı önyükleme GUI bileşenlerini kullanarak hello görünüm kolayca artırabilirsiniz.

Açık *görünümleri\\giriş\\SessionByCode.cshtml* ve hello içeriği biçimlendirme aşağıdaki hello ile değiştirin:

    @model Mvc5Mobile.Models.Session

    @{
        ViewBag.Title = "Session details";
    }
    <h3>@Model.Title (@Model.Code)</h3>
    <p>
        <strong>@Model.DateText</strong> in <strong>@Model.Room</strong>
    </p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Speakers
        </div>
        @foreach (var speaker in Model.Speakers)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class="panel-body" })
        }
    </div>

    <p>@Model.Abstract</p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Tags
        </div>
        @foreach (var tag in Model.Tags)
        {
            @Html.ActionLink(tag, 
                             "SessionsByTag", 
                             new { tag }, 
                             new { @class = "panel-body" })
        }
    </div>

Merhaba yeni markup tooimprove hello mobil görüntüle stil oluşturma önyükleme paneller kullanır. 

Merhaba mobil tarayıcıyı yenileyin. Merhaba aşağıdaki görüntüde yaptığınız hello kod değişiklikleri yansıtır:

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a>Kaydırma ve gözden geçirin
Bu öğretici, nasıl göstermiştir toouse ASP.NET MVC 5 toodevelop mobil dostu Web uygulamaları. Bunlar:

* Bir ASP.NET MVC 5 uygulama tooan App Service web uygulaması dağıtma
* MVC 5 uygulamanızda önyükleme toocreate yanıt veren web düzenini kullanın
* Düzen, görünümleri ve kısmi görünümler, hem genel hem de tek bir görünümü için geçersiz kılma
* Denetim düzenini ve kısmi geçersiz kılma zorlama kullanarak `RequireConsistentDisplayMode` özelliği
* Merhaba iPhone tarayıcısı gibi belirli tarayıcılar hedef görünümlerini oluşturma
* Razor kodunda önyükleme Stil Uygula

## <a name="see-also"></a>Ayrıca Bkz.
* [yanıt veren web tasarımı 9 temel ilkeleri](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* [Önyükleme][BootstrapSite]
* [Resmi önyükleme blogu][Official Bootstrap Blog]
* [Öğretici Cumhuriyeti gelen twitter Bootstrap Öğreticisi][Twitter Bootstrap Tutorial from Tutorial Republic]
* [Merhaba önyükleme Playground][hello Bootstrap Playground]
* [W3C öneri mobil Web uygulaması en iyi uygulamalar][W3C Recommendation Mobile Web Application Best Practices]
* [Medya sorgular için W3C adayı önerisi][W3C Candidate Recommendation for media queries]

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- Internal Links -->
[Deploy hello starter project tooan Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override hello Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve hello Speakers List]: #bkmk_Improvespeakerslist
[Improve hello Tags List]: #bkmk_improvetags
[Improve hello Dates List]: #bkmk_improvedates
[Improve hello SessionsTable View]: #bkmk_improvesessionstable
[Improve hello SessionByCode View]: #bkmk_improvesessionbycode

<!-- External Links -->
[Visual Studio Express 2013]: http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-web
[Visual Studio 2015]: https://www.visualstudio.com/downloads/download-visual-studio-vs
[AzureSDKVs2013]: http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409
[Fiddler]: http://www.fiddler2.com/fiddler2/
[EmulatorIE11]: http://msdn.microsoft.com/library/ie/dn255001.aspx
[EmulatorChrome]: https://developers.google.com/chrome-developer-tools/docs/mobile-emulation
[EmulatorOpera]: http://www.opera.com/developer/tools/mobile/
[StarterProject]: http://go.microsoft.com/fwlink/?LinkID=398780&clcid=0x409
[CompletedProject]: http://go.microsoft.com/fwlink/?LinkID=398781&clcid=0x409
[BootstrapSite]: http://getbootstrap.com/
[WebPIAzureSdk23NetVS13]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/WebPIAzureSdk23NetVS13.png
[linked list group]: http://getbootstrap.com/components/#list-group-linked
[glyphicon]: http://getbootstrap.com/components/#glyphicons
[panels]: http://getbootstrap.com/components/#panels
[custom linked list group]: http://getbootstrap.com/components/#list-group-custom-content
[grid system]: http://getbootstrap.com/css/#grid
[responsive utilities]: http://getbootstrap.com/css/#responsive-utilities
[Official Bootstrap Blog]: http://blog.getbootstrap.com/
[Twitter Bootstrap Tutorial from Tutorial Republic]: http://www.tutorialrepublic.com/twitter-bootstrap-tutorial/
[hello Bootstrap Playground]: http://www.bootply.com/
[W3C Recommendation Mobile Web Application Best Practices]: http://www.w3.org/TR/mwabp/
[W3C Candidate Recommendation for media queries]: http://www.w3.org/TR/css3-mediaqueries/

<!-- Images -->
[DeployClickPublish]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-1.png
[DeployClickWebSites]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-2.png
[DeploySignIn]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-3.png
[DeployUsername]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-4.png
[DeployPassword]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-5.png
[DeployNewWebsite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-6.png
[DeploySiteSettings]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7.png
[DeployPublishSite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-8.png
[MobileHomePage]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/mobile-home-page.png
[FixedSessionsByTag]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-Fixed.png
[AllTags]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags.png
[SessionsByTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET.png
[SessionsByTagASP.NETNoBootstrap]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-NoBootstrap.png
[AllTagsMobile_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile.png
[AllTagsMobile_LayoutMobileDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile-Desktop.png
[ResolveDefaultDisplayMode]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/Resolve-DefaultDisplayMode.png
[AllTagsIPhone_LayoutIPhone]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsIPhone-_LayoutIPhone.png
[AllSpeakers_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile.png
[AllSpeakers_LayoutMobileOverridden]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile-Overridden.png
[AllSpeakersFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed.png
[AllSpeakersFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-Desktop.png
[AllSpeakersFixedSearchBySC]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-SearchBySC.png
[AllTagsFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-Desktop.png 
[AllTagsFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed.png
[AllDatesFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed.png
[AllDatesFixed2]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2.png
[AllDatesFixed2Desktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2-Desktop.png
[AllTagsFixedSearchByASP]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-SearchByASP.png
[SessionsTableTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Tag-ASP.NET.png
[SessionsTableFixedTagASP.NETDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Fixed-Tag-ASP.NET-Desktop.png
[SessionByCode3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-3-644.png
[SessionByCodeFixed3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-Fixed-3-644.png

