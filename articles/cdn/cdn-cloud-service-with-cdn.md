---
title: bir Azure bulut hizmeti Azure CDN ile aaaIntegrate | Microsoft Docs
description: "Nasıl bir tümleşik Azure CDN uç noktasından içerik sunan toodeploy bir bulut hizmeti öğrenin"
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="intro"></a>Bir bulut hizmeti Azure CDN ile tümleştirme
Bir bulut hizmeti, tüm içeriği hello bulut hizmetinin konumundan hizmet veren Azure CDN ile tümleştirilebilir. Bu yaklaşım, avantajları hello sağlar:

* Kolayca dağıtın ve görüntüleri, komut dosyalarını ve stil sayfalarını bulut hizmetinizin proje dizinlerde güncelleştir
* Bulut hizmetinizde jQuery veya önyükleme sürümleri gibi hello NuGet paketlerini kolayca yükseltme
* Web uygulamanızı yönetmek, CDN sunulan tüm hello aynı içerik ve Visual Studio arabirimi
* Web uygulamanız ve CDN sunulan içeriğiniz için birleşik dağıtım iş akışı
* ASP.NET paketleme ve küçültme Azure CDN ile tümleştirme

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu öğreticide şunları öğreneceksiniz nasıl yapılır:

* [Azure CDN uç bulut hizmetiniz ile bütünleşir ve statik içerik Web sayfalarınıza Azure CDN hizmet](#deploy)
* [Bulut hizmetinizde statik içeriği için önbellek ayarlarını yapılandırın](#caching)
* [Denetleyici eylemleri Azure CDN aracılığıyla içerikten hizmet](#controller)
* [Hizmet vermemesini gruplanır ve Visual Studio deneyimi hello ayıklamasını korurken Azure CDN içeriğinden küçültülmüş](#bundling)
* [Azure CDN çevrimdışı olduğunda geri dönüş komut dosyaları ve CSS yapılandırın.](#fallback)

## <a name="what-you-will-build"></a>Yapı
Merhaba varsayılan ASP.NET MVC şablonu kullanarak bir bulut hizmeti Web rolü dağıtacağınızı, görüntü, denetleyici eylem sonuçlarını ve hello varsayılan JavaScript ve CSS dosyaları gibi tümleşik bir Azure CDN kod tooserve içerik ekleme ve ayrıca kod tooconfigure hello yazma Bu hello CDN hello olayda hizmet paketleri için geri dönüş mekanizması çevrimdışıdır.

## <a name="what-you-will-need"></a>İhtiyacınız olacak
Bu öğretici önkoşulları aşağıdaki hello sahiptir:

* Etkin bir [Microsoft Azure hesabı](/account/)
* Visual Studio 2015 ile birlikte [Azure SDK'sı](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)

> [!NOTE]
> Bu öğretici bir Azure hesabı toocomplete gerekir:
> 
> * Yapabilecekleriniz [ücretsiz bir Azure hesabı açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/) -krediler alırsınız tootry çıkışı Ücretli Azure hizmetlerini kullanabilirsiniz ve hatta kullanıldıktan sonra en fazla hello hesabı tutabilir ve ücretsiz Web siteleri gibi Azure hizmetlerini kullanabilirsiniz.
> * Yapabilecekleriniz [MSDN abone Avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -MSDN aboneliğiniz size kredi verir Ücretli Azure hizmetlerinizi kullanabildiğiniz her ay.
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a>Bir bulut hizmeti dağıtma
Bu bölümde, hello varsayılan Visual Studio 2015 tooa bulut hizmeti Web rolünde ASP.NET MVC uygulama şablonu dağıtmak ve yeni bir CDN uç noktası ile tümleştirin. Aşağıdaki Hello yönergeleri izleyin:

1. Visual Studio 2015'te, çok giderek hello menü çubuğundan yeni bir Azure bulut hizmeti oluşturma**Dosya > Yeni > Proje > bulut > Azure bulut hizmeti**. Bir ad verin ve tıklatın **Tamam**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. Seçin **ASP.NET Web rolü** hello tıklatıp  **>**  düğmesi. Tamam'a tıklayın.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. Seçin **MVC** tıklatıp **Tamam**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. Şimdi, bu Web rolü tooan Azure bulut hizmeti yayımlayın. Merhaba bulut hizmeti projesine sağ tıklatın ve **Yayımla**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. Henüz Microsoft Azure'da oturum değil, hello tıklatın **Hesap Ekle...**  tıklayın ve açılan hello **Hesap Ekle** menü öğesi.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. Merhaba oturum açma, hello Azure hesabınıza tooactivate kullanılan Microsoft hesabı ile oturum açma sayfası.
7. Oturum açtınız sonra tıklayın **sonraki**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. Bir bulut hizmeti veya depolama hesabı oluşturmadıysanız varsayılarak, Visual Studio hem de oluşturmanıza yardımcı olur. Merhaba, **bulut hizmeti oluşturun ve hesabı** iletişim kutusu, türü hello istenen hizmet adı ve istediğiniz bölgeyi seçin hello. Sonra, **Oluştur**’a tıklayın.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. Merhaba yayımlama Ayarları sayfası, hello yapılandırmasını doğrulayın ve tıklayın **Yayımla**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > Bulut Hizmetleri için Hello yayımlama işlemi çok uzun sürüyor. Merhaba Web dağıtımını etkinleştirin tüm rolleri seçeneği için Web rolleri hızlı (ancak geçici) güncelleştirmeleri tooyour sağlayarak bulut hizmetiniz çok daha hızlı hata ayıklama yapabilirsiniz. Bu seçenek hakkında daha fazla bilgi için bkz: [yayımlama hello Azure araçlarını kullanarak bir bulut hizmeti](http://msdn.microsoft.com/library/ff683672.aspx).
   > 
   > 
   
    Ne zaman hello **Microsoft Azure etkinlik günlüğü** yayımlama durumu gösterir **tamamlandı**, bulut hizmeti ile tümleşik bir CDN uç noktası oluşturur.
   
   > [!WARNING]
   > Yayımladıktan sonra dağıtılan hello bulut hizmeti hata ekranı görüntüler, dağıttığınız hello bulut hizmeti tarafından kullanıldığından, büyük olasılıkla varsa, bir [konuk .NET 4.5.2 içermez OS](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).  Bu sorundan getirebilirler [.NET 4.5.2 bir başlangıç görevi olarak dağıtma](../cloud-services/cloud-services-dotnet-install-dotnet.md).
   > 
   > 

## <a name="create-a-new-cdn-profile"></a>Yeni bir CDN profili oluşturma
CDN profili, CDN uç noktaları koleksiyonudur.  Her bir profil, bir veya daha fazla CDN uç noktası içerir.  Birden çok profilleri tooorganize toouse isteyebilir CDN uç noktalarınızı internet etki alanı, web uygulaması veya başka bir ölçüt.

> [!TIP]
> Bu öğretici için toouse istediğiniz bir CDN profili varsa, çok devam[yeni bir CDN uç noktası oluşturma](#create-a-new-cdn-endpoint).
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>Yeni bir CDN uç noktası oluşturma
**toocreate depolama hesabınız için yeni bir CDN uç noktası**

1. Merhaba, [Azure Yönetim Portalı](https://portal.azure.com), tooyour CDN profili gidin.  Bu toohello Pano hello önceki adımda sabitlemiş olabilirsiniz.  Bunu tıklayarak bulabilirsiniz değil, varsa **Gözat**, ardından **CDN profili**, ve hello profili tıklatarak tooadd uç noktanızı planladığınız.
   
    Merhaba CDN profili dikey penceresi görünür.
   
    ![CDN profili][cdn-profile-settings]
2. Merhaba tıklatın **uç nokta Ekle** düğmesi.
   
    ![Uç nokta ekle düğmesi][cdn-new-endpoint-button]
   
    Merhaba **bir uç nokta ekleyin** dikey penceresi görünür.
   
    ![Uç nokta ekleme dikey penceresi][cdn-add-endpoint]
3. Bu CDN uç noktası için bir **Ad** girin.  Bu ad kullanılan tooaccess hello etki alanındaki önbelleğe alınmış kaynaklarınıza olacaktır `<EndpointName>.azureedge.net`.
4. Merhaba, **kaynak türü** açılan listesinde, select *bulut hizmeti*.  
5. Merhaba, **kaynak ana bilgisayar adı** açılan listesinde, bulut hizmetinizi seçin.
6. Merhaba Varsayılanları bırakabilir **kaynak yolu**, **kaynak ana bilgisayar üstbilgisi**, ve **Protokolü/kaynak bağlantı noktası**.  En az bir protokol (HTTP veya HTTPS) belirtmeniz gerekir.
7. Merhaba tıklatın **Ekle** düğmesini toocreate hello yeni uç noktası.
8. Merhaba uç nokta oluşturulduktan sonra hello profil için uç noktalar listesinde görünür. Merhaba URL toouse tooaccess hello kaynak etki alanının yanı sıra, içeriği önbelleğe Hello liste görünümü gösterir.
   
    ![CDN uç noktası][cdn-endpoint-success]
   
   > [!NOTE]
   > Merhaba uç nokta hemen kullanılabilir olmaz.  Merhaba kayıt toopropagate hello CDN ağ üzerinden too90 dakika yukarı alabilir. Merhaba içerik CDN hello kullanılabilir hale gelene kadar hemen toouse hello CDN etki alanı adı deneyen kullanıcılar durum kodu 404 alabilirsiniz.
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a>Test hello CDN uç noktası
Durum yayımlama hello olduğunda **tamamlandı**, bir tarayıcı penceresi açın ve çok gidin**http://<cdnName>*.azureedge.net/Content/bootstrap.css**. My Kurulum, bu URL'yi şöyledir:

    http://camservice.azureedge.net/Content/bootstrap.css

Kaynak URL hello CDN uç noktada aşağıdaki toohello karşılık geldiği:

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

Ne zaman gezinmenizi çok**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**, tarayıcınıza bağlı olarak, istendiğinde toodownload veya açık hello bootstrap.css olacaktır, yayımlanan Web uygulamanızdan geldi.

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

Genel olarak erişilebilir bir URL'de benzer şekilde erişebilirsiniz  **http://*&lt;serviceName >*doğrudan CDN uç noktanız gelen.cloudapp.net/**. Örneğin:

* Merhaba/Script yolundan .js dosya
* Merhaba/Content içerik dosyanın yolu
* Herhangi bir denetleyici/eylem
* CDN uç noktanız, sorgu dizeleri içeren herhangi bir URL'ye adresindeki Hello sorgu dizesi etkinleştirilirse

Aslında, yapılandırma yukarıda hello ile hello tüm bulut hizmetinden barındırabilir  **http://*&lt;cdnName >*.azureedge.net/**. Çok giderseniz,**http://camservice.azureedge.net/ ** alıyorum hello eylem sonucu giriş/dizinden.

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

Bu, ancak bu her zaman iyi bir fikir tooserve tüm bulut hizmeti Azure CDN aracılığıyla olduğunu anlamına gelmez. 

CDN statik teslim iyileştirme önbelleğe toobe amaçlanmamıştır veya hello CDN hello varlık yeni bir sürümü hello kaynak sunucudan çok sık çekme gerekir bu yana çok sık güncelleştirilen dinamik varlıklarını teslimat mutlaka hızlandırmak değil. Bu senaryo için etkinleştirmeniz [dinamik Site hızlandırma](cdn-dynamic-site-acceleration.md) çeşitli teknikleri toospeed alınabilir olmayan dinamik varlıklar teslimini kullanan CDN uç noktanız iyileştirmeyi (DSA). 

Dinamik ve statik içeriği karışımını içeren bir siteniz varsa, tooserve CDN statik içerik (örneğin, genel web teslim) statik iyileştirme türüyle ve tooserve dinamik içerik hello kaynak sunucudan doğrudan ya da bir CDN aracılığıyla seçebilirsiniz bir olay temelinde açık DSA iyileştirme uç noktası. toothat son nasıl hello CDN uç noktasından tooaccess ayrı içerik dosyaları zaten gördünüz. I nasıl tooserve belirli denetleyici eylemi belirli bir CDN uç noktası aracılığıyla hizmet denetleyici eylemleri aracılığıyla Azure CDN içeriğini gösterir.

Merhaba, Azure CDN gelen tooserve bulut hizmetinizde olay temelinde içerik toodetermine alternatiftir. toothat son nasıl hello CDN uç noktasından tooaccess ayrı içerik dosyaları zaten gördünüz. I size nasıl tooserve belirli denetleyici eylemi üzerinden hello CDN uç gösterir [hizmet denetleyici eylemleri Azure CDN aracılığıyla içerikten](#controller).

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a>Bulut hizmetinizde statik dosyalar için önbellek seçeneklerini yapılandırın
Bulut hizmetinizde Azure CDN tümleştirme ile nasıl hello CDN uç önbelleğe statik içerik toobe istediğinizi belirtebilirsiniz. toodo Bu, açık *Web.config* (örneğin WebRole1), Web rolünden proje ve ekleme bir `<staticContent>` öğesi çok`<system.webServer>`. Merhaba XML aşağıdaki hello önbellek tooexpire 3 gün içinde yapılandırır.  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

Bunu yaptıktan sonra bulut hizmetindeki tüm statik dosyaları aynı CDN önbelleğiniz kural hello gözlemleyin. Önbellek ayarları konusunda daha ayrıntılı denetim için ekleme bir *Web.config* bir klasöre dosya ve ayarlarınızı var. ekleyin. Örneğin, bir *Web.config* toohello dosya *\Content* klasörü ve Değiştir XML aşağıdaki hello ile içerik hello:

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

Bu ayarı tüm statik dosyaları hello neden *\Content* 15 gün boyunca önbelleğe alınan klasörü toobe.

Hakkında daha fazla bilgi için tooconfigure hello `<clientCache>` öğesi, bkz: [istemci önbelleği &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).

İçinde [hizmet denetleyici eylemleri Azure CDN aracılığıyla içerikten](#controller), ı de hello CDN önbellek denetleyici eylem sonuçlarını için önbellek ayarlarını nasıl yapılandıracağınızı gösterilir.

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a>Denetleyici eylemleri Azure CDN aracılığıyla içerikten hizmet
Bulut hizmeti Web rolü Azure CDN ile tümleştirmek denetleyici eylemleri hello Azure CDN aracılığıyla görece kolay tooserve içerikten olur. Bulut hizmet veren dışında doğrudan Azure (yukarıda gösterilen), CDN hizmet [Maarten Balliauw](https://twitter.com/maartenballiauw) nasıl gösterir toodo eğlenceli bir kendisiyle MemeGenerator denetleyicisi [hello Azure CDN ile Merhaba Web'de gecikmesini azaltır ](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN). I yalnızca onu buraya yeniden.

Bulut hizmetinizde Küçük yaştaki ALi Norris görüntüyü temel alarak toogenerate memes istediğinizi düşünelim (tarafından fotoğraf [Alan ışık](http://www.flickr.com/photos/alan-light/218493788/)) şöyle:

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

Basit bir sahip `Index` hello müşterilerin toospecify hello derecelerinin hello görüntüde sağlayan eylem toohello eylem sonrası sonra hello meme sonra oluşturur. ALi Norris olduğundan, bu sayfa toobecome müthiş bir başarı popüler genel beklediğiniz. Bu, yarı dinamik içerik Azure CDN ile hizmet veren, iyi bir örnektir.

Bu denetleyici eylemi toosetup yukarıdaki Hello adımları izleyin:

1. Merhaba, *\Controllers* klasör adında yeni bir .cs dosyası oluşturmak *MemeGeneratorController.cs* ve Değiştir hello hello ile içerik aşağıdaki kodu. CDN adıyla emin tooreplace hello vurgulanan bölümü olabilir.  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. Merhaba varsayılan olarak sağ `Index()` eylem ve select **Görünüm Ekle**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. Aşağıdaki Hello ayarlarını kabul edin ve tıklatın **Ekle**.
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. Açık hello yeni *Views\MemeGenerator\Index.cshtml* ve basit HTML hello derecelerinin göndermek için aşağıdaki hello hello içerik değiştirin:
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. Merhaba bulut hizmeti yeniden yayımlamanız ve çok gidin**http://*&lt;serviceName >*tarayıcınızda.cloudapp.net/MemeGenerator/Index**.

Ne zaman gönderdiğiniz hello form değerleri çok`/MemeGenerator/Index`, hello `Index_Post` eylem yöntemine döndürür bağlantı toohello `Show` eylem yöntemi, hello ilgili giriş tanımlayıcısı. Merhaba bağlantısını tıklattığınızda koddan hello ulaşmak:  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

Ardından, yerel hata ayıklayıcısı ekli, yerel bir yeniden yönlendirme ile Merhaba normal hata ayıklama deneyimini alırsınız. Merhaba bulut Hizmeti çalışıyorsa, için yönlendirir:

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

CDN uç noktanız kaynak URL'de aşağıdaki toohello karşılık geldiği:

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


Merhaba sonra kullanabileceğiniz `OutputCacheAttribute` hello öznitelikte `Generate` nasıl hello eylem sonucu, önbelleğe, Azure CDN dokunmaz yöntemi toospecify. Aşağıdaki Hello kodu Önbellek süre sonu 1 saatlik (3.600 saniye) belirtin.

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

Benzer şekilde, size herhangi bir denetleyici eylem içerikten yukarı bulut hizmetiniz istenen hello önbelleğe alma seçeneği ile Azure CDN aracılığıyla hizmet verebilir.

Merhaba sonraki bölümde, ı size nasıl tooserve hello toplanmış ve komut dosyaları ve CSS Azure CDN aracılığıyla küçültülmüş gösterir.

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a>ASP.NET paketleme ve küçültme Azure CDN ile tümleştirme
Komut dosyaları ve CSS stil sayfaları, seyrek değiştirin ve hello Azure CDN önbellek prime adaylar. Hizmet hello Azure CDN ile tüm Web rolü olan hello en kolay yolu toointegrate paketleme ve küçültme Azure CDN ile. Toodo bu isteyebilirsiniz, ancak, t, nasıl toodo hello korurken, ASP.NET paketleme ve küçültme, develper deneyimi gibi istenen gösterecektir:

* Harika hata ayıklama modu deneyimi
* Basitleştirilmiş Dağıtım
* Komut dosyası/CSS sürüm yükseltme için hemen güncelleştirmeleri tooclients
* CDN uç noktanız başarısız olduğunda bir geri dönüş mekanizması
* Kod değişikliği simge durumuna küçült

Merhaba, **WebRole1** oluşturduğunuz proje [Azure CDN uç Azure Web sitesi ile bütünleşir ve Azure CDN Web sayfalarınıza statik içerik sunmanızı](#deploy), açık *App_Start\ BundleConfig.cs* ve hello bakalım `bundles.Add()` yöntem çağrıları.

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

ilk hello `bundles.Add()` deyimi hello sanal dizininde betik paket ekler `~/bundles/jquery`. Ardından, açın *görünümler/paylaşılan\_Layout.cshtml* toosee hello paket etiketi nasıl işlenir. Razor kod satırı aşağıdaki mümkün toofind hello olmalıdır:

    @Scripts.Render("~/bundles/jquery")

Bu Razor kod hello Azure Web rolünde çalıştırdığınızda kılacak bir `<script>` etiketi hello için paket benzer toohello aşağıdaki komut dosyası:

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

Ancak, çalıştırıldığında Visual Studio'da yazarak `F5`, her komut dosyası hello paketteki tek tek kılacak (Merhaba yukarıdaki, yalnızca bir komut dosyası hello pakette bir durumdur):

    <script src="/Scripts/jquery-1.10.2.js"></script>

Eşzamanlı istemci bağlantıları (paketleme) azaltma ve dosya geliştirme performans (küçültme) üretimde karşıdan yüklerken bu, geliştirme ortamınızı toodebug hello JavaScript kodu sağlar. Azure CDN Tümleştirmesi ile bir önemli özellik toopreserve olur. Ayrıca, işlenen hello paket zaten bir otomatik olarak oluşturulan sürüm dizesi içerdiğinden işlevselliği şekilde hello jQuery sürümünüz, NuGet aracılığıyla güncelleştirdiğinizde tooreplicate istediğiniz hello istemci tarafında güncelleştirilebilir hemen olası.

ASP.NET toointegration paketleme ve küçültme CDN uç noktanız ile Merhaba adımları izleyin.

1. Geri *App_Start\BundleConfig.cs*, hello değiştirme `bundles.Add()` yöntemleri toouse farklı bir [paket Oluşturucusu](http://msdn.microsoft.com/library/jj646464.aspx), bir CDN adresini belirtir. toodo Bu, Değiştir hello `RegisterBundles` koddan hello yöntemi tanımıyla:  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    Emin tooreplace olması `<yourCDNName>` Azure CDN hello adı.
   
    Düz metin olarak ayarladığınız `bundles.UseCdn = true` ve dikkatli bir şekilde hazırlanmış bir CDN URL'sine tooeach paket eklenir. Örneğin, hello ilk oluşturucuda hello kod:
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    olan hello aynıdır:
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    Bu oluşturucu ASP.NET paketleme ve küçültme hata ayıklaması sırasında toorender ayrı komut dosyaları yerel olarak bildirir ancak kullanım hello CDN adresi tooaccess hello betik söz konusu belirtilmedi. Ancak, bu dikkatle hazırlanmış CDN URL ile iki önemli özelliklere dikkat edin:
   
   * Bu CDN URL'sine Hello kaynağı `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, aslında hello sanal dizin hello betik paketin bulut hizmetinizde olduğu.
   * CDN Oluşturucusu kullandığından hello hello paket için CDN komut dosyası etiketinin artık otomatik olarak oluşturulan hello sürüm dizesi URL çizilir hello içinde içerir. Merhaba betik paket bir önbellek, Azure CDN kaçırılması değiştirilmiş tooforce her kullanılışında benzersiz sürüm dizesi el ile oluşturmanız gerekir. AT hello aynı zaman, bu benzersiz sürüm dizesi devam etmelidir hello dağıtım toomaximize İsabetli Önbellek okuma sayısının Azure CDN adresindeki hello ömrü boyunca sabit hello paket dağıtıldıktan sonra.
   * Sorgu dizesi v merhaba < W.X.Y.Z > çeken gelen = *Properties\AssemblyInfo.cs* Web rolü projenizdeki. TooAzure her yayımladığınızda hello derleme sürümü artırma içeren bir dağıtım iş akışı olabilir. Veya yalnızca değiştirebileceğiniz *Properties\AssemblyInfo.cs* , oluşturduğunuz her zaman, proje tooautomatically artırma hello sürüm dizesi hello joker karakter kullanarak ' *'. Örneğin:
     
        [derleme: AssemblyVersion("1.0.0.*")]
     
     Merhaba ömrü dağıtımı için benzersiz bir dize oluşturma diğer strateji toostreamline burada çalışır.
2. Merhaba bulut hizmeti ve erişim hello giriş sayfasına yeniden yayımlayın.
3. Görünüm hello hello sayfasının HTML kodunu. Mümkün toosee hello CDN, değişiklikleri tooyour bulut hizmeti yeniden yayımlamanız her zaman bir benzersiz sürüm dizesi ile işlenen URL olmalıdır. Örneğin:  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. Visual Studio'da yazarak hello bulut hizmeti Visual Studio'da hata ayıklama `F5`.,
5. Görünüm hello hello sayfasının HTML kodunu. Böylece Visual Studio'da deneyimi tutarlı bir hata ayıklama sahip tek tek işlenen her komut dosyası hala görürsünüz.  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a>CDN URL'ler için geri dönüş mekanizması
Azure CDN uç noktanız için herhangi bir nedenle başarısız olduğunda, Web sayfası toobe hello JavaScript veya önyükleme yüklenmesi için geri dönüş seçeneği olarak, kaynak Web sunucunuzun yeterli tooaccess akıllı istiyor. Web sitenizi tooCDN kullanılamazlık ancak komut dosyalarını ve stil sayfalarını tarafından sağlanan çok daha ağır toolose önemli sayfa işlevselliği nedeniyle yeterince önemli toolose görüntülerinde olur.

Merhaba [paket](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) sınıfı adlı bir özellik içerir [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) , CDN hatası tooconfigure hello geri dönüş mekanizması sağlar. toouse bu özellik, aşağıdaki hello adımları izleyin:

1. Web rolü projesinde açmak *App_Start\BundleConfig.cs*, CDN URL'sine her eklediğiniz [paket Oluşturucusu](http://msdn.microsoft.com/library/jj646464.aspx)ve vurgulanmış hello aşağıdaki tooadd geri dönüş mekanizması toohello değiştirir Varsayılan paket:  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    Zaman `CdnFallbackExpression` olan hello paket başarıyla yüklendi olup olmadığını null, komut dosyası hello HTML tootest eklenmiş ve aksi durumda, doğrudan hello kaynak Web sunucusundan hello paket erişim. Bu özellik hello ilgili CDN paket düzgün şekilde yüklenmesini olup olmadığını sınar toobe kümesi tooa JavaScript ifadesi olması gerekiyor. Merhaba ifade gerekli tootest according toohello içerik her paket farklıdır. Merhaba varsayılan paketleri için yukarıdaki:
   
   * `window.jquery`JQuery-{version} .js tanımlanır
   * `$.validator`JQuery.Validate.js tanımlanır
   * `window.Modernizr`modernizer gibi-{version} .js tanımlanır
   * `$.fn.modal`Bootstrap.js tanımlanır
     
     I CdnFallbackExpression Merhaba ayarlamamış olduğunu fark etmiş olabilirsiniz `~/Cointent/css` paket. Şu anda bu olmadığından bir [System.Web.Optimization hatada](https://aspnetoptimization.codeplex.com/workitem/104) , yerleştirir bir `<script>` hello yerine geri dönüş CSS beklenen hello için etiket `<link>` etiketi.
     
     Yoktur, ancak iyi bir [stili paket geri dönüş](https://github.com/EmberConsultingGroup/StyleBundleFallback) tarafından sunulan [Ember danışmanlık grup](https://github.com/EmberConsultingGroup).
2. CSS için toouse hello geçici çözüm, Web rolü projenizin içinde yeni bir .cs dosyası oluşturma *App_Start* adlı bir klasör *StyleBundleExtensions.cs*ve ile Merhaba içeriğine Değiştir [gelen kod GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).
3. İçinde *App_Start\StyleFundleExtensions.cs*, başlangıç ad alanı tooyour Web rolün yeniden adlandırın (örneğin **WebRole1**).
4. Çok dön`App_Start\BundleConfig.cs` ve hello son değiştirme `bundles.Add` vurgulanmış kodu aşağıdaki hello deyimiyle:  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    Bu yeni genişletme yöntemi hello kullanan aynı fikir tooinject komut hello HTML toocheck hello DOM hello için içinde eşleşen sınıf adı, kural adı ve hello CSS paket ve toofind hello eşleşme başarısız olursa döner geri toohello kaynağı Web sunucusu tanımlanmış kural değer.
5. Yeniden Hello bulut hizmeti ve erişim hello giriş sayfası yayımlayın.
6. Görünüm hello hello sayfasının HTML kodunu. Eklenen komut dosyaları benzer toohello aşağıdaki bulmanız gerekir:    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    Merhaba CSS paket için eklenen komut hello gelen hello yalıtılarak işlemi hala içerdiğine dikkat edin `CdnFallbackExpression` hello satır özelliğinde:

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    Ancak hello ilk kısmı hello itibaren || ifade her zaman true (doğrudan yukarıdaki hello satırdaki) döndürür ve hello document.write() işlevi asla çalışmaz.

## <a name="more-information"></a>Daha Fazla Bilgi
* [Hello Azure içerik teslim ağı (CDN) genel bakış](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [Azure CDN'yi kullanma](cdn-create-new-endpoint.md)
* [ASP.NET paketleme ve küçültme](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
