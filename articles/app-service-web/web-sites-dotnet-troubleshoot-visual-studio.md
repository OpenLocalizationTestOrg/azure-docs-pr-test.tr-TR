---
title: "Visual Studio kullanarak Azure App Service web uygulamasında aaaTroubleshoot"
description: "Nasıl tootroubleshoot uzaktan hata ayıklama kullanarak Azure web uygulaması, izleme ve günlüğe kaydetme tooVisual Studio 2013 oluşturulan araçları hakkında bilgi edinin."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: 
ms.assetid: def8e481-7803-4371-aa55-64025d116c97
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: 8e3a8a58293f2ebcdc131fbf2534f8ff99b26730
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-web-app-in-azure-app-service-using-visual-studio"></a>Visual Studio kullanarak Azure App Service web uygulamasında sorun giderme
## <a name="overview"></a>Genel Bakış
Bu öğretici nasıl yardımcı toouse Visual Studio Araçları, bir web uygulamasında hata ayıklama gösterir [uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714), çalıştırarak [hata ayıklama modu](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) uzaktan veya uygulama ve web sunucu günlükleri görüntüleme.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

Şunları öğreneceksiniz:

* Azure web uygulaması yönetim işlevleri, Visual Studio'da kullanılabilir.
* Nasıl toouse Visual Studio uzaktan görüntülemek toomake hızlı değişiklikler, bir uzak web uygulamasında.
* Nasıl bir proje sırasında uzaktan hata ayıklama modu toorun hem bir web uygulaması için hem de bir Web işi için Azure üzerinde çalışıyor.
* Bunları nasıl toocreate uygulama izleme günlükleri ve hello uygulama çalışırken görüntülemek oluşturuyor.
* Nasıl tooview web sunucu günlükleri de dahil olmak üzere, ayrıntılı hata iletilerini ve başarısız istek izleme.
* Nasıl toosend tanılama tooan Azure depolama hesabı günlüğe kaydeder ve bunları görüntüleyin.

Visual Studio Ultimate varsa de kullanabilirsiniz [IntelliTrace](http://msdn.microsoft.com/library/vstudio/dd264915.aspx) hata ayıklama için. Bu öğreticide IntelliTrace kapsamında değildir.

## <a name="prerequisites"></a>Önkoşullar
Bu öğretici hello geliştirme ortamı, web projesi ve bölümünde ayarladığınız Azure web uygulaması ile çalışır [Azure ve ASP.NET kullanmaya başlama][GetStarted]. Merhaba WebJobs bölümleri için oluşturduğunuz Merhaba uygulaması gerekir [hello Azure WebJobs SDK ile çalışmaya başlama][GetStartedWJ].

Bu öğreticide gösterilen örnek bir C# MVC web uygulaması için olan, ancak sorun giderme yordamları hello hello kod olan hello Visual Basic ve Web Forms uygulamaları için aynı.

Visual Studio 2015 veya 2013 kullanıyorsanız Hello öğretici varsayar. Visual Studio 2013 kullanıyorsanız, hello WebJobs özellikleri gerektirir [güncelleştirme 4](http://go.microsoft.com/fwlink/?LinkID=510314) veya sonraki bir sürümü.

Merhaba akış günlükleri, .NET Framework 4 veya sonrasını hedefleyen uygulamalar için çalışır özelliği.

## <a name="sitemanagement"></a>Web Uygulama Yapılandırması ve Yönetimi
Visual Studio sağlar erişim tooa alt hello web uygulama yönetimi işlevleri ve yapılandırma ayarlarını hello kullanılabilir [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715). Bu bölümde kullanarak kullanılabilenleri görürsünüz **Sunucu Gezgini**. toosee hello en son Azure tümleştirme özellikleri denemek **Cloud Explorer** de. Her iki windows hello açabilirsiniz **Görünüm** menüsü.

1. Visual Studio'da tooAzure zaten imzalanmadığını hello tıklatın **tooAzure bağlanmak** düğmesini **Sunucu Gezgini**.

    Tooinstall etkinleştirir tooyour hesabınıza erişmeniz bir yönetim sertifikası alternatiftir. Tooinstall bir sertifika seçerseniz, hello sağ **Azure** düğümünde **Sunucu Gezgini**ve ardından **yönetin ve filtre abonelikleri** hello bağlam menüsünde. Merhaba, **Azure Aboneliklerini Yönet** iletişim kutusunda, hello **sertifikaları** sekmesini ve ardından **alma**. Merhaba yönergeleri toodownload izleyin ve abonelik dosyasını içeri (olarak da adlandırılan bir *.publishsettings* dosyası) Azure hesabınız için.

   > [!NOTE]
   > Abonelik dosya indirme, kaynak kodu dizinlerinizi (örneğin, klasöründe hello yüklemeleri) dışında tooa klasörüne kaydedin ve hello içeri aktarma tamamlandıktan sonra silin. Erişim toohello abonelik dosyası kazanır kötü niyetli bir kullanıcı düzenleme, oluşturma ve Azure hizmetlerinizi silin.
   >
   >

    Visual Studio'dan tooAzure kaynaklarına bağlanma hakkında daha fazla bilgi için bkz: [hesaplarını yönetme, abonelikleri ve yönetici rollerini](http://go.microsoft.com/fwlink/?LinkId=324796#BKMK_AccountVCert).
2. İçinde **Sunucu Gezgini**, genişletin **Azure** ve genişletin **uygulama hizmeti**.
3. Oluşturduğunuz hello web uygulamasını içeren hello kaynak grubunu genişletin [Azure ve ASP.NET ile çalışmaya başlama][GetStarted]ve ardından hello web uygulaması düğümünü sağ tıklatın ve'ı tıklatın **ayarlarınıgörüntüle**.

    ![Sunucu Gezgininde görünümü ayarları](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewsettings.png)

    Merhaba **Azure Web uygulaması** sekmesi görüntülenir ve vardır, Visual Studio'da bulunan web uygulaması yönetim ve yapılandırma görevlerini hello görebilirsiniz.

    ![Azure Web uygulaması penceresi](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configtab.png)

    Bu öğreticide, hello günlüğe kaydetme ve izleme aşağı açılan listeler kullanıyor olmanız. Uzaktan hata ayıklama kullanacağınız ancak farklı bir yöntem tooenable kullanacağınız onu.

    Bu penceresinde hello uygulama ayarlarının ve bağlantı dizelerinin kutuları hakkında daha fazla bilgi için bkz: [Azure Web Apps: nasıl uygulama dizeleri ve bağlantı dizeleri çalışma](http://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).

    Tooperform Bu pencerede yapılamaz bir web uygulaması yönetim görevi istiyorsanız, **Yönetim Portalı'nda Aç** tooopen bir tarayıcı penceresi toohello Azure portalı.

## <a name="remoteview"></a>Server Explorer'da erişim web uygulama dosyaları
Genellikle hello ile bir web projesi dağıtma `customErrors` hello Web.config dosyası kümesinin çok bayrak`On` veya `RemoteOnly`, yanlış giden anlamına yararlı hata iletisi bir şey olduğunda elde etmezsiniz. İçin birçok hata aldığınız tek şey olanları aşağıdaki hello biri gibi bir sayfa.

**'/' Uygulamasında sunucu hatası:**

![Faydasız hata sayfası](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror.png)

**Bir hata oluştu:**

![Faydasız hata sayfası](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror1.png)

**Merhaba Web sitesi hello sayfa görüntülenemiyor**

![Faydasız hata sayfası](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror2.png)

Sık hello en kolay yolu toofind hello hello hata tooenable nedenidir ekran görüntüleri önceki hello ilk hello ayrıntılı hata iletileri açıklanmaktadır nasıl toodo. Web.config dosyası hello değişikliği dağıtılan gerektirir. Merhaba düzenleyebilirsiniz *Web.config* dosya hello proje ve yeniden dağıtın hello proje veya oluşturma bir [Web.config dönüştürmesi](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) ve hata ayıklama derlemesi dağıtmak, ancak daha hızlı bir yolu yoktur: içinde **çözümü Explorer** doğrudan görüntüleyin ve hello kullanarak dosyaları hello Uzak web uygulamasında düzenleyin *uzak görünümü* özelliği.

1. İçinde **Sunucu Gezgini**, genişletin **Azure**, genişletin **uygulama hizmeti**, web uygulamanızı bulunan hello kaynak grubunu genişletin ve ardından web uygulamanız için hello düğümünü genişletin.

    Erişim toohello web uygulamanızın içerik dosyalarını ve günlük dosyalarını size düğümleri bakın.
2. Merhaba genişletin **dosyaları** düğümü hello çift tıklayın ve *Web.config* dosya.

    ![Web.config dosyasını açın](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfig.png)

    Visual Studio hello Uzak web uygulamasından hello Web.config dosyasını açar ve hello başlık çubuğunda [uzak] sonraki toohello dosya adını gösterir.
3. Satır toohello aşağıdaki hello eklemek `system.web` öğe:

    `<customErrors mode="Off"></customErrors>`

    ![Web.config Düzenle](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfigedit.png)
4. Merhaba faydasız hata iletisi gösteren hello tarayıcıyı yenileyin ve şimdi, aşağıdaki örneğine hello gibi bir ayrıntılı hata iletisi alırsınız:

    ![Ayrıntılı hata iletisi](./media/web-sites-dotnet-troubleshoot-visual-studio/detailederror.png)

    (gösterilen hello hata kırmızı ile çok gösterilen hello satırı ekleyerek oluşturulduğu*Views\Home\Index.cshtml*.)

Düzenleme hello Web.config dosyasında daha kolay sorun giderme hangi hello özelliği, Azure web uygulamanızın tooread ve düzenleme dosyalarda olun senaryoları yalnızca bir örnektir.

## <a name="remotedebug"></a>Uzaktan hata ayıklama web uygulamaları
Hello ayrıntılı hata iletisi yeterli bilgi sağlamaz ve yerel olarak hello hata yeniden oluşturulamaz, başka bir şekilde tootroubleshoot uzaktan hata ayıklama modunda toorun olur. Kesme noktalarını ayarlayın, bellek doğrudan işlemek, kod üzerinden adım ve bile hello kod yolu değiştirin.

Uzaktan hata ayıklama Visual Studio Express sürümlerinde çalışmaz.

Bu bölümde nasıl hello kullanarak uzaktan toodebug projesinin gösterir oluşturmak [Azure ve ASP.NET ile çalışmaya başlama][GetStarted].

1. Oluşturduğunuz açık hello web projesi [Azure ve ASP.NET ile çalışmaya başlama][GetStarted].
2. Açık *Controllers\HomeController.cs*.
3. Merhaba silme `About()` yöntemi ve INSERT hello aşağıdaki kodu yerine.

        public ActionResult About()
        {
            string currentTime = DateTime.Now.ToLongTimeString();
            ViewBag.Message = "hello current time is " + currentTime;
            return View();
        }
4. [Bir kesme noktası belirleyerek](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) hello üzerinde `ViewBag.Message` satır.
5. İçinde **Çözüm Gezgini**, hello projesine sağ tıklayın ve **Yayımla**.
6. Merhaba, **profil** aşağı açılan listesinden, select hello aynı profil, kullanılan [Azure ve ASP.NET ile çalışmaya başlama][GetStarted].
7. Merhaba tıklatın **ayarları** sekmesini tıklatın ve değiştirme **yapılandırma** çok**hata ayıklama**ve ardından **Yayımla**.

    ![Hata ayıklama modunda yayımlama](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-publishdebug.png)
8. Dağıtımdan sonra biter ve tarayıcınız toohello Kapat hello tarayıcı, web uygulamanızın Azure URL'sini açar.
9. İçinde **Sunucu Gezgini**, web uygulamanızı sağ tıklayın ve ardından **Attach hata ayıklayıcı**.

    ![Hata ayıklayıcıyı Ekle](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-attachdebugger.png)

    Merhaba tarayıcı otomatik olarak Azure'da çalışan tooyour giriş sayfası açılır. 20 saniye toowait sahip olabilir veya bu nedenle while hello server hata ayıklama için Azure kurar. Bu gecikme, yalnızca ilk kez bir web uygulamasında hata ayıklama modunda çalıştırılması hello gerçekleşir. Sonraki kez var. hata ayıklamayı yeniden başlattığınızda sonraki 48 saat içinde hello bir gecikme olmayacaktır.

    **Not:** hello hata ayıklayıcı başlangıç herhangi bir sorun varsa, toodo deneyin kullanarak **Cloud Explorer** yerine **Sunucu Gezgini**.
10. Tıklatın **hakkında** hello menüsünde.

     Visual Studio hello kesme noktasına durdurur ve hello kod Azure içinde değil, yerel bilgisayarınızda çalışıyor.
11. Merhaba getirin `currentTime` değişken toosee hello saat değeri.

     ![Hata ayıklama modunda Azure'da çalışan görünümü değişkeni](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugviewinwa.png)

     gördüğünüz hello yerel bilgisayarınıza daha farklı bir saat diliminde olabilir hello Azure sunucu saati saattir.
12. Hello için yeni bir değer girin `currentTime` değişken "Şimdi Azure'da çalışan" gibi.
13. Çalışan toocontinue F5 tuşuna basın.

     Azure'da çalışan sayfa hakkında Hello hello currentTime değişkenine girdiğiniz hello yeni değeri görüntüler.

     ![Yeni değerle sayfası hakkında](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugchangeinwa.png)

## <a name="remotedebugwj"></a>Uzaktan hata ayıklama Web işleri
Bu bölümde nasıl Merhaba projeyi ve web uygulamasını kullanarak uzaktan toodebug oluşturduğunuz gösterir [hello Azure WebJobs SDK ile çalışmaya başlama](websites-dotnet-webjobs-sdk.md).

Bu bölümde gösterilen hello özellikleri yalnızca Visual Studio 2013'te, Update 4 veya daha sonra kullanılabilir.

Uzaktan hata ayıklama yalnızca sürekli Webjob'lar ile çalışır. Zamanlanmış ve isteğe bağlı Webjob'lar, hata ayıklama desteklemez.

1. Oluşturduğunuz açık hello web projesi [hello Azure WebJobs SDK ile çalışmaya başlama][GetStartedWJ].
2. Merhaba ContosoAdsWebJob projeyi açın *Functions.cs*.
3. [Bir kesme noktası belirleyerek](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) hello ilk hello deyiminde üzerinde `GnerateThumbnail` yöntemi.

    ![Kesme noktası ayarlama](./media/web-sites-dotnet-troubleshoot-visual-studio/wjbreakpoint.png)
4. İçinde **Çözüm Gezgini**, hello web projesi (Merhaba Web işi projesi değil) sağ tıklayın ve **Yayımla**.
5. Merhaba, **profil** aşağı açılan listesinden, select hello aynı profil, kullanılan [hello Azure WebJobs SDK ile çalışmaya başlama](websites-dotnet-webjobs-sdk.md).
6. Merhaba tıklatın **ayarları** sekmesini tıklatın ve değiştirme **yapılandırma** çok**hata ayıklama**ve ardından **Yayımla**.

    Visual Studio hello web ve Web işi projeleri dağıtır ve toohello web uygulamanızı Azure URL'sini tarayıcınızın açılır.
7. İçinde **Sunucu Gezgini** genişletin **Azure > uygulama hizmeti > kaynak grubunuz > web uygulamanızı > WebJobs > sürekli**ve ardından sağ **ContosoAdsWebJob**.
8. Tıklatın **hata ayıklayıcısını**.

    ![Hata ayıklayıcıyı Ekle](./media/web-sites-dotnet-troubleshoot-visual-studio/wjattach.png)

    Merhaba tarayıcı otomatik olarak Azure'da çalışan tooyour giriş sayfası açılır. 20 saniye toowait sahip olabilir veya bu nedenle while hello server hata ayıklama için Azure kurar. Bu gecikme, yalnızca ilk kez bir web uygulamasında hata ayıklama modunda çalıştırılması hello gerçekleşir. 48 saat içinde yaparsanız hello bir gecikme vardır hello hata ayıklayıcıyı Ekle sonraki sefer olmayacaktır.
9. Açılan toohello Contoso Ads giriş sayfası olan hello web tarayıcısında, yeni bir ad oluşturun.

    Bir ad oluşturma WebJob hello tarafından toplanmış ve işlenen oluşturulmuş bir kuyruk iletisi toobe neden olur. Merhaba WebJobs SDK hello işlevi tooprocess hello kuyruk iletisi çağırdığında hello kod isabetini karşılaşır.
10. Merhaba hata ayıklayıcı kesme noktasında böldüğünde inceleyin ve hello program hello bulut çalışırken değişken değerlerini değiştirin. Hello aşağıdaki çizimde hello hata ayıklayıcı toohello GenerateThumbnail yöntemi geçildi hello blobInfo nesne hello içeriğini gösterir.

     ![hata ayıklayıcı blobInfo nesnesinde](./media/web-sites-dotnet-troubleshoot-visual-studio/blobinfo.png)
11. Çalışan toocontinue F5 tuşuna basın.

     Merhaba GenerateThumbnail yöntemi hello küçük resim oluşturmayı tamamlar.
12. Merhaba tarayıcıda yenileme hello dizin sayfası ve hello küçük resim bakın.
13. Visual Studio'da toostop hata ayıklama SHIFT + F5 tuşuna basın.
14. İçinde **Sunucu Gezgini**, hello ContosoAdsWebJob düğümünü sağ tıklatın ve **görünüm Pano**.
15. Azure kimlik bilgilerinizle oturum ve hello Web işi adı toogo toohello sayfası için WebJob'ı tıklatın.

     ![ContosoAdsWebJob'ı tıklatın](./media/web-sites-dotnet-troubleshoot-visual-studio/clickcaw.png)

     Merhaba Pano bu hello son yürütülen GenerateThumbnail işlev gösterir.

     (Merhaba sonraki tıklattığınızda **görünüm Pano**toosign içinde yoktur ve hello tarayıcı gider doğrudan, WebJob için toohello sayfası.)
16. Merhaba işlevi adı toosee hello işlevi yürütme ayrıntılarını'ı tıklatın.

     ![İşlev ayrıntıları](./media/web-sites-dotnet-troubleshoot-visual-studio/funcdetails.png)

İşlevinizi [günlükleri yazdı](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs), tıklatın **ToggleOutput** toosee bunları.

## <a name="notes-about-remote-debugging"></a>Uzaktan hata ayıklama hakkında notlar
* Hata ayıklama modunda üretimde çalışan önerilmez. Üretim web uygulamanız toomultiple sunucu örnekleri ölçeklenmez, hata ayıklama hello web sunucusunun yanıt verme tooother istekleri engeller. Bunu yaparsanız rastgele bir örneği ve alacaksınız toohello hata ayıklayıcı taktığınızda birden çok web sunucusu örneğine sahip hiçbir şekilde tooensure sonraki bu tarayıcı istekleri toothat örneği gider. Ayrıca, genellikle bir hata ayıklama yapı tooproduction dağıtmazsınız ve derleyici iyileştirmelerini sürüm yapıları için olanlar imkansız tooshow satır kaynak kodunuzda kolaylaştırır. Üretim ilgili sorunları gidermek için en iyi uygulama kaynaktır izleme ve web sunucu günlükleri.
* Kesme noktaları uzak uzun durur kaçının hata ayıklama. Azure, yanıt vermeyen bir işlem olarak birkaç dakikadan uzun süre için durduruldu ve öyle kapanır bir işlem değerlendirir.
* Hatalarını ayıkladığınız sırada hello sunucu veri tooVisual bant genişliği ücretleri etkileyebilecek Studio gönderiyor. Bant genişliği oranları hakkında daha fazla bilgi için bkz: [Azure fiyatlandırma](https://azure.microsoft.com/pricing/calculator/).
* Bu hello emin olun `debug` hello özniteliği `compilation` hello öğesinde *Web.config* dosya tootrue ayarlanır. Hata ayıklama yapı yapılandırması yayımladığınızda tootrue varsayılan olarak ayarlanır.

        <system.web>
          <compilation debug="true" targetFramework="4.5" />
          <httpRuntime targetFramework="4.5" />
        </system.web>
* Bu hello hata ayıklayıcı toodebug istediğiniz koda adım olmaz bulursanız, toochange hello sadece kendi kodumu ayarı olabilir.  Daha fazla bilgi için bkz: [sürüm tooJust kendi kodumu kısıtlamak](http://msdn.microsoft.com/library/vstudio/y740d9d3.aspx#BKMK_Restrict_stepping_to_Just_My_Code).
* Süreölçer hello sunucuda hello uzaktan hata ayıklama özelliği etkinleştirdiğinizde ve 48 saat sonra hello özelliği otomatik olarak kapatılır başlatır. Bu 48 saat sınır güvenlik ve performans nedenleriyle yapılır. İstediğiniz şekilde geri sayıda saatlerinin hello özelliğini kolayca kapatabilirsiniz. Değil etkin olarak ayıklarken devre dışı bırakarak öneririz.
* Merhaba hata ayıklayıcı tooany işlem, yalnızca hello web uygulaması işlem'in (w3wp.exe) el ile ekleyebilirsiniz. Toouse Visual Studio modunda nasıl hata ayıklama hakkında daha fazla bilgi için bkz: [Visual Studio'da hata ayıklamayı](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx).

## <a name="logsoverview"></a>Tanılama günlükleri'ne genel bakış
Bir Azure web uygulamasında çalışan bir ASP.NET uygulaması tür günlüğe aşağıdaki hello oluşturabilirsiniz:

* **Uygulama izleme günlükleri**<br/>
  Merhaba uygulama Bu günlükler hello yöntemlerini çağırarak oluşturur [System.Diagnostics.Trace](http://msdn.microsoft.com/library/system.diagnostics.trace.aspx) sınıfı.
* **Web sunucu günlükleri**<br/>
  Merhaba web sunucusu her HTTP isteği toohello web uygulaması için bir günlük girişi oluşturur.
* **Ayrıntılı hata iletisi günlükleri**<br/>
  Merhaba web sunucusu başarısız HTTP isteklerini (Bu durum kodu 400 veya daha büyük sonuç) için bazı ek bilgiler içeren bir HTML sayfası oluşturur.
* **İstek izleme günlüklerini başarısız oldu**<br/>
  Hello web sunucusu, başarısız olan HTTP istekleri için ayrıntılı izleme bilgilerini içeren bir XML dosyası oluşturur. Merhaba web sunucusu, aynı zamanda bir XSL dosyasını tooformat hello XML bir tarayıcıda sağlar.

Azure verir şekilde etkiler web uygulaması performans günlüğü özelliğini tooenable hello veya her günlük türü gerektiği gibi devre dışı bırakın. Uygulama günlükleri için yalnızca belirli bir önem düzeyi yukarıda günlükleri yazılması belirtebilirsiniz. Yeni bir web uygulaması varsayılan olarak tüm günlük oluştururken devre dışı bırakılır.

Günlükleri dilini toofiles bir *LogFiles* hello dosya sistemi, web uygulaması ve FTP aracılığıyla erişilebilir olan klasöründe. Ayrıca Web sunucusu ve uygulama günlükleri tooan Azure depolama hesabı yazılabilir. Büyük bir birim hello dosya sisteminde mümkün olandan bir depolama hesabındaki günlükler tutabilirsiniz. Merhaba dosya sistemi kullandığınızda sınırlı tooa en fazla 100 megabaytlık günlükleri demektir. (Yalnızca kısa vadeli bekletme için dosya sistemi günlükleri içindir. "Hello sınıra ulaşıldıktan sonra azure yenilerini için eski günlük dosyaları toomake yeri siler.)  

## <a name="apptracelogs"></a>Oluşturma ve uygulama izleme günlüklerini görüntüle
Bu bölümde siz gerçekleştirirsiniz hello görevler:

* Oluşturduğunuz izleme deyimleri toohello web projesi eklemek [Azure ve ASP.NET kullanmaya başlama][GetStarted].
* Merhaba projeyi yerel olarak çalıştırdığınızda hello günlüklerine bakın.
* Azure'da çalışan hello uygulama tarafından üretilen gibi hello günlüklerine bakın.

Toocreate uygulaması Web işleri içinde nasıl günlüğe yazacağını hakkında daha fazla bilgi için bkz: [Azure kuyruk depolama kullanma toowork hello nasıl WebJobs SDK - toowrite nasıl günlüğe yazacağını](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs). Merhaba günlükleri görüntüleme ve Azure'da nasıl depolandıkları denetlemek için aşağıdaki yönergeleri de WebJobs tarafından oluşturulan tooapplication günlükleri geçerlidir.

### <a name="add-tracing-statements-toohello-application"></a>İzleme deyimleri toohello uygulama ekleme
1. Açık *Controllers\HomeController.cs*ve hello yerine `Index`, `About`, ve `Contact` aşağıdaki hello yöntemleriyle kod sipariş tooadd `Trace` deyimleri ve `using` deyimi için `System.Diagnostics`:

        public ActionResult Index()
        {
            Trace.WriteLine("Entering Index method");
            ViewBag.Message = "Modify this template toojump-start your ASP.NET MVC application.";
            Trace.TraceInformation("Displaying hello Index page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Index method");
            return View();
        }

        public ActionResult About()
        {
            Trace.WriteLine("Entering About method");
            ViewBag.Message = "Your app description page.";
            Trace.TraceWarning("Transient error on hello About page at " + DateTime.Now.ToShortTimeString());
            Trace.WriteLine("Leaving About method");
            return View();
        }

        public ActionResult Contact()
        {
            Trace.WriteLine("Entering Contact method");
            ViewBag.Message = "Your contact page.";
            Trace.TraceError("Fatal error on hello Contact page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Contact method");
            return View();
        }        
2. Ekleme bir `using System.Diagnostics;` deyimi toohello dosyasının üst kısmında hello.

### <a name="view-hello-tracing-output-locally"></a>Yerel olarak çıkış görünüm hello izleme
1. F5 toorun hello uygulama hata ayıklama modunda tuşuna basın.

    Merhaba varsayılan İzleme dinleyicisi Yazar tüm izleme çıktısı toohello **çıkış** yanı sıra diğer hata ayıklama çıktı penceresi. Merhaba aşağıdaki çizimde hello çıktısını hello toohello eklenen izleme deyimleri gösterir `Index` yöntemi.

    ![Hata ayıklama penceresinde izleme](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugtracing.png)

    Aşağıdaki adımları hello hata ayıklama modunda derleme olmadan bir web sayfasında nasıl tooview izleme çıktısını gösterir.
2. Merhaba uygulamanın Web.config dosyasını (Merhaba proje klasöründe bulunan hello) açın ve eklemek bir `<system.diagnostics>` hello dosya yalnızca hello kapatılmadan önce hello ucundaki öğe `</configuration>` öğe:

          <system.diagnostics>
            <trace>
              <listeners>
                <add name="WebPageTraceListener"
                    type="System.Web.WebPageTraceListener,
                    System.Web,
                    Version=4.0.0.0,
                    Culture=neutral,
                    PublicKeyToken=b03f5f7f11d50a3a" />
              </listeners>
            </trace>
          </system.diagnostics>

    Merhaba `WebPageTraceListener` görüntülemenizi sağlar, çok göz atarak çıkış izleme`/trace.axd`.
3. Ekleme bir <a href="http://msdn.microsoft.com/library/vstudio/6915t83k(v=vs.100).aspx">trace ögesi</a> altında `<system.web>` hello Web.config dosyasında aşağıdaki örneğine hello gibi:

        <trace enabled="true" writeToDiagnosticsTrace="true" mostRecent="true" pageOutput="false" />
4. CTRL + F5 toorun Merhaba uygulaması tuşuna basın.
5. Merhaba adres çubuğuna hello tarayıcı penceresinin eklemek *trace.axd* toohello URL ve (Merhaba URL benzer toohttp://localhost:53370/trace.axd olacaktır) Enter tuşuna basın.
6. Merhaba üzerinde **uygulama izleme** sayfasında, **ayrıntıları görüntüle** hello ilk satırda (değil BrowserLink satır hello).

    ![Trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd1.png)

    Merhaba **istek ayrıntıları** sayfası görüntülenirse ve hello **izleme bilgilerini** toohello eklenen hello izleme deyimleri hello çıktısını gördüğünüz bölüm `Index` yöntemi.

    ![Trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd2.png)

    Varsayılan olarak, `trace.axd` yalnızca yerel olarak kullanılabilir. Toomake istediyseniz, Uzak web uygulamasından kullanılabilir ekleyebilirsiniz `localOnly="false"` toohello `trace` hello öğesinde *Web.config* hello aşağıdaki örnekte gösterildiği gibi dosya:

        <trace enabled="true" writeToDiagnosticsTrace="true" localOnly="false" mostRecent="true" pageOutput="false" />

    Ancak, etkinleştirme `trace.axd` bir üretim web uygulaması güvenlik nedenleriyle genellikle önerilmez ve bölümler aşağıdaki hello izleme günlüklerini bir Azure web uygulamasında daha kolay bir şekilde tooread görürsünüz.

### <a name="view-hello-tracing-output-in-azure"></a>Azure'da Hello izleme çıktısını görüntüleyin
1. İçinde **Çözüm Gezgini**, hello web projesi sağ tıklatın ve **Yayımla**.
2. Merhaba, **Web'i Yayımla** iletişim kutusu, tıklatın **Yayımla**.

    Visual Studio güncelleştirmenizi yayımlar sonra bir tarayıcı penceresi tooyour giriş sayfasını açar (kaydetmedi temizleyin varsayılarak **hedef URL** hello üzerinde **bağlantı** sekmesi).
3. İçinde **Sunucu Gezgini**, web uygulamanızı sağ tıklatıp **akış günlüklerini görüntüle**.

    ![Bağlam menüsünde akış günlüklerini görüntüle](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewlogsmenu.png)

    Merhaba **çıkış** günlük akış bağlı toohello olan penceresi şunu gösterir hizmet ve günlük toodisplay gider her dakika bir bildirim satırı ekler.

    ![Bağlam menüsünde akış günlüklerini görüntüle](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-nologsyet.png)
4. Uygulama giriş sayfanız gösteren hello tarayıcı penceresinde **kişi**.

    Toohello eklediğiniz hello hata düzeyi izlemesinden çıktı birkaç saniye hello içinde `Contact` yöntemi görünür hello **çıkış** penceresi.

    ![Çıktı penceresinde hata izleme](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-errortrace.png)

    İzleme hizmeti hello günlük etkinleştirdiğinizde, hello varsayılan ayar olduğu için visual Studio hata düzeyi izlemeleri yalnızca göstermez. Yeni bir Azure web uygulaması oluşturduğunuzda, daha önce hello Ayarları sayfası açıldığında, gördüğünüz gibi tüm günlük varsayılan olarak devre dışıdır:

    ![Oturum kapatma uygulama](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-apploggingoff.png)

    Ancak, seçtiğinizde **akış günlüklerini görüntüle**, Visual Studio otomatik olarak değiştirildi **uygulama Logging(File System)** çok**hata**, hata düzeyi günlükleri anlamına gelir Rapor. Tüm izleme günlüklerini toosee sipariş, bu çok ayarı değiştirebilirsiniz**ayrıntılı**. Hata düşük bir önem düzeyi seçtiğinizde, daha yüksek önem düzeyleri için tüm günlükleri de raporlanır. Ayrıntılı seçtiğinizde, bu nedenle, aynı zamanda bilgi, uyarı ve Hata günlüklerini görürsünüz.  

1. İçinde **Sunucu Gezgini**hello web uygulaması sağ tıklayın ve ardından **görünüm ayarlarını** daha önce yaptığınız gibi.
2. Değişiklik **uygulama günlüğü (dosya sistemi)** çok**ayrıntılı**ve ardından **kaydetmek**.

    ![İzleme düzeyi tooVerbose ayarlama](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-applogverbose.png)
3. Şimdi gösteren tarayıcı penceresinde hello, **kişi** sayfasında, **giriş**, ardından **hakkında**ve ardından **kişi**.

    Birkaç saniye içinde hello **çıkış** penceresi tüm izleme çıktısını gösterir.

    ![Ayrıntılı izleme çıktısı](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-verbosetraces.png)

    Bu bölümde etkin ve Azure web uygulaması ayarları kullanarak günlük kaydını devre dışı. Ayrıca, etkinleştirme ve izleme dinleyicileri hello Web.config dosyasını değiştirerek devre dışı. Merhaba web uygulama yapılandırması aracılığıyla günlüğünü etkinleştirme, yapmaz sırada ancak hello Web.config dosyasında değişiklik hello uygulama etki alanı toorecycle neden olur. Merhaba sorun uzun süre tooreproduce sürüyor veya aralıklı, hello uygulama etki alanı geri dönüştürme "Düzelt" ve yeniden işlem yapılana kadar toowait zorla. Hata bilgilerini hemen yakalama başlatabilmeniz Azure tanılama etkinleştirme, bunu yapmaz.

### <a name="output-window-features"></a>Çıktı penceresi özellikleri
Hello **Azure günlükleri** hello sekmesinde **çıkış** penceresinde birkaç düğmeler ve metin kutusu vardır:

![Düğmeleri günlükleri sekmesi](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-icons.png)

Bu işlevler aşağıdaki hello gerçekleştirin:

* Clear hello **çıkış** penceresi.
* Etkinleştirmek veya sözcük kaydırmayı devre dışı.
* Başlat veya günlüklerini İzlemeyi Durdur.
* Belirtmek toomonitor günlüğe kaydeder.
* Günlükleri indirin.
* Bir arama dizesi veya normal bir ifade göre günlükleri filtreleyin.
* Kapat hello **çıkış** penceresi.

Bir arama dizesi veya normal ifade girerseniz, Visual Studio hello istemci günlük bilgileri filtreler. Merhaba günlükleri hello görüntülendikten sonra hello ölçütleri girebilirsiniz anlamına **çıkış** penceresindeki değiştirebilirsiniz filtreleme ölçütlerini tooregenerate hello günlükleri gerek kalmadan.

## <a name="webserverlogs"></a>Web sunucusu günlüklerini görüntüle
Web sunucu günlükleri hello web uygulaması için tüm HTTP etkinliğini kaydeder. Sipariş toosee içinde hello bunları **çıkış** bunları hello için web uygulaması ve Visual Studio toomonitor istediğiniz söyleyin tooenable sahip pencere bunları.

1. Merhaba, **Azure Web uygulaması yapılandırmasında** gelen açtığınız sekmesini **Sunucu Gezgini**, Web Server günlüğü çok değiştirme**üzerinde**ve ardından **kaydetmek**.

    ![Web sunucusu günlüğü etkinleştirme](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-webserverloggingon.png)
2. Hello içinde **çıkış** penceresinde hello tıklatın **hangi Azure günlükleri toomonitor belirtin** düğmesi.

    ![Hangi Azure günlükleri toomonitor belirtin](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-specifylogs.png)
3. Merhaba, **Azure günlük seçenekleri** iletişim kutusunda **Web sunucu günlükleri**ve ardından **Tamam**.

    ![İzleyici web sunucu günlükleri](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorwslogson.png)
4. Merhaba web uygulaması gösteren hello tarayıcı penceresinde **giriş**, ardından **hakkında**ve ardından **kişi**.

    Merhaba uygulama günlüklerini genellikle hello web sunucu günlükleri tarafından izlenen önce görünür. Toowait olabilir biraz hello tooappear günlüğe kaydeder.

    ![Çıktı penceresinde Web sunucu günlükleri](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-wslogs.png)

Visual Studio kullanarak ilk web sunucu günlükleri etkinleştirdiğinizde varsayılan olarak, Azure hello günlükleri toohello dosya sistemi yazar. Alternatif olarak, hello Azure kullanabilirsiniz sunucu günlükleri web portalı toospecify yazılmış bir depolama hesabında tooa blob kapsayıcısı.

Depolama hesap ayarlarınızı tooan Azure depolama hesabı günlüğü hello portal tooenable web sunucusu kullanıyorsanız ve yeniden etkinleştirmeniz Visual Studio'da oturum Visual Studio'da günlüğe kaydetme devre dışı bırakmak geri yüklenir.

## <a name="detailederrorlogs"></a>Ayrıntılı hata iletisi günlükleri görüntüle
Ayrıntılı hata günlükleri hata yanıt kodları (400 veya üstü) neden HTTP istekleriyle ilgili bazı ek bilgiler sağlar. Sipariş toosee içinde hello bunları **çıkış** penceresinde hello için web uygulaması ve Visual Studio toomonitor istediğiniz söyleyin tooenable sahip bunları.

1. Merhaba, **Azure Web uygulaması yapılandırmasında** gelen açtığınız sekmesini **Sunucu Gezgini**, değiştirme **ayrıntılı hata iletileri** çok**üzerinde**, ve ardından **kaydetmek**.

    ![Ayrıntılı hata iletilerini etkinleştir](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailedlogson.png)
2. Hello içinde **çıkış** penceresinde hello tıklatın **hangi Azure günlükleri toomonitor belirtin** düğmesi.
3. Merhaba, **Azure günlük seçenekleri** iletişim kutusu, tıklatın **tüm günlükleri**ve ardından **Tamam**.

    ![Tüm günlükler izleme](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorall.png)
4. Bir ek karakter toohello URL toocause 404 hatası Hello adres çubuğuna hello tarayıcı penceresinin ekleyin (örneğin, `http://localhost:53370/Home/Contactx`), ve Enter tuşuna basın.

    Birkaç saniye sonra hello ayrıntılı hata günlüğü hello Visual Studio görünüyor **çıkış** penceresi.

    ![Çıktı penceresinde ayrıntılı hata günlüğü](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorlog.png)

    Control + bir tarayıcıda biçimlendirilmiş hello bağlantı toosee hello günlük Çıkış'ı tıklatın:

    ![Tarayıcı penceresinde ayrıntılı hata günlüğü](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorloginbrowser.png)

## <a name="downloadlogs"></a>Dosya sistem günlüklerini indirin
Hello izleyebilirsiniz herhangi bir günlük **çıkış** penceresi de indirilebilir olarak bir *.zip* dosyası.

1. Merhaba, **çıkış** penceresinde tıklatın **akış günlükleri indirmek**.

    ![Düğmeleri günlükleri sekmesi](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadicon.png)

    Dosya Gezgini'ni açar tooyour *indirmeleri* hello klasörüyle indirilen seçili dosyası.

    ![İndirilen Dosya](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadedfile.png)
2. Merhaba ayıklamak *.zip* dosya ve klasör yapısı aşağıdaki hello bakın:

    ![İndirilen Dosya](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilefolders.png)

   * Uygulama izleme günlükleri olan *.txt* hello dosyalarında *LogFiles\Application* klasör.
   * Web sunucu günlükleri olan *.log* hello dosyalarında *LogFiles\http\RawLogs* klasör. Bir aracı gibi kullanabilir [günlük ayrıştırıcısı](http://www.microsoft.com/download/details.aspx?displaylang=en&id=24659) tooview ve bu dosyaları değiştirebilirler.
   * Ayrıntılı hata iletisi günlüklerin içinde *.html* hello dosyalarında *LogFiles\DetailedErrors* klasör.

     (Merhaba *dağıtımları* klasördür kaynak denetim yayımlamayı; tarafından oluşturulan dosyalar için herhangi bir şey ilgili tooVisual Studio yayımlama sahip değil. Merhaba *Git* hizmet akış izlemeleri ilgili toosource denetim yayımlama ve hello günlük dosyası için bir klasördür.)  

## <a name="storagelogs"></a>Depolama günlüklerini görüntüle
Uygulama izleme günlükleri tooan Azure depolama hesabı da gönderilebilir ve Visual Studio'da görüntüleyebilirsiniz. Depolama hesabı oluşturma, depolama günlüklerine hello Klasik Portalı'nda etkinleştirmek ve hello görüntülemek, toodo **günlükleri** hello sekmesinde **Azure Web uygulaması** penceresi.

Günlükleri tooany veya tümünü üç hedefleri gönderebilirsiniz:

* Merhaba dosya sistemi.
* Depolama hesabı tabloları.
* Depolama hesabı BLOB'ları.

Her hedef için farklı önem düzeyi belirtebilirsiniz.

İsteğe bağlı olarak tablolar kolay tooview ayrıntıları günlüklerinin çevrimiçi yapın ve akış destekledikleri; tablolardaki günlüklerini sorgular ve bunlar oluşturuldukça yeni günlüklerine bakın. BLOB'ları kolaylaştırır kolay toodownload günlükleri dosyaları ve tooanalyze Hdınsight bildiği için Hdınsight, kullanarak bunları nasıl toowork blob storage ile. Daha fazla bilgi için bkz: **Hadoop ve MapReduce** içinde [veri depolama seçenekleri (yapı gerçek bulut uygulamaları Azure ile)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options).

Şu anda dosya sistemi günlükleri kümesi tooverbose düzeyi yok; Merhaba aşağıdaki adımlar, bilgi düzeyi günlükleri toogo toostorage hesap tabloları ayarı aracılığıyla yol. Bilgi düzeyi anlamına gelmektedir çağrılarak oluşturulan tüm günlükleri `Trace.TraceInformation`, `Trace.TraceWarning`, ve `Trace.TraceError` , çağıran oluşturulan günlükleri ancak görüntülenir `Trace.WriteLine`.

Depolama hesapları, depolama ve kalıcı daha uzun bekletme günlükleri için daha fazla toohello dosya sistemi ile karşılaştırıldığında sunar. Gönderen uygulama günlükleri toostorage izleme başka bir avantajı, dosya sistem günlüklerini alma her günlüğü ile bazı ek bilgiler almak ' dir.

1. Sağ **depolama** altında Azure düğümü hello ve ardından **depolama hesabı oluştur**.

![Depolama hesabı oluşturma](./media/web-sites-dotnet-troubleshoot-visual-studio/createstor.png)

1. Merhaba, **depolama hesabı oluştur** iletişim kutusunda, hello depolama hesabı için bir ad girin.

    Merhaba adı olmalı benzersiz olmalıdır (başka bir Azure depolama hesabı hello olabilir aynı adı). Girdiğiniz hello adı zaten kullanımda olduğunda bir fırsat toochange alırsınız.

    Depolama hesabınız olacak URL tooaccess hello *{ad}*. core.windows.net.
2. Set hello **bölge veya benzeşim grubunda** aşağı açılan liste toohello bölgeye en yakın tooyou.

    Bu ayar, hangi Azure veri merkezi depolama hesabınız barındıracak belirtir. Bu öğretici için tercih ettiğiniz bir dikkat çekici fark yapmaz, ancak bir üretim web uygulaması için web sunucunuz, depolama hesabı toobe hello içinde istediğiniz aynı bölge toominimize gecikme süresi ve veri çıkış ücretleri. (daha sonra oluşturacağınız) hello web uygulamasını bir bölgede web uygulamanızı sipariş toominimize gecikme erişme olası toohello tarayıcı olarak kapatmak çalıştırmanız gerekir.
3. Set hello **çoğaltma** aşağı açılan listesinde çok**yerel olarak yedekli**.
   
    Bir depolama hesabı için coğrafi çoğaltma etkinleştirildiğinde, depolanan hello içerik çoğaltılmış tooa ikincil veri merkezine tooenable yük devretme toothat hello birincil konumda büyük bir felaket durumunda konumdur. Coğrafi çoğaltma ek ücretlere neden olabilir. Test ve geliştirme hesaplarında genellikle coğrafi çoğaltma için toopay istemezsiniz. Daha fazla bilgi için bkz. [Depolama hesabı oluşturma, yönetme veya silme](../storage/common/storage-create-storage-account.md).
4. **Oluştur**'a tıklayın.

    ![Yeni depolama hesabı](./media/web-sites-dotnet-troubleshoot-visual-studio/newstorage.png)    
5. Hello Visual Studio içinde **Azure Web uygulaması** penceresinde hello tıklatın **günlükleri** sekmesini ve ardından **günlüğü yapılandırma Yönetim Portalı'nda**.

    <!-- todo:screenshot of new portal if hello VS page link goes toonew portal -->
    ![Günlük tutmayı yapılandırma](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configlogging.png)

    Merhaba açılır **yapılandırma** hello Klasik portal web uygulamanız için bir sekmede.
6. Merhaba Klasik portalın içinde **yapılandırma** sekmesinde toohello uygulama Tanılama bölümüne kaydırın ve ardından değiştirmek **uygulama günlüğü (Table Storage)** çok**üzerinde**.
7. Değişiklik **günlük düzeyi** çok**bilgi**.
8. Tıklatın **tablo depolama yönetin**.

    ![TableStorage Yönet'e tıklayın](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-stgsettingsmgmtportal.png)

    Merhaba, **uygulama tanılama için Tablo depolama yönetmek** kutusunda seçebileceğiniz depolama hesabınızın birden fazla varsa. Yeni bir tablo oluşturmak veya mevcut bir kullanın.

    ![Tablo depolama yönetin](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-choosestorageacct.png)
9. Merhaba, **uygulama tanılama için Tablo depolama yönetmek** kutusunu hello onay işareti tooclose hello kutusunu tıklatın.
10. Merhaba Klasik portalın içinde **yapılandırma** sekmesini tıklatın, **kaydetmek**.
11. Merhaba uygulama web uygulaması görüntüleyen hello tarayıcı penceresinde **giriş**, ardından **hakkında**ve ardından **kişi**.

     Bu web sayfaları göz atarak üretilen hello günlük bilgilerini toohello depolama hesabına yazılır.
12. Merhaba, **günlükleri** hello sekmesinde **Azure Web uygulaması** Visual Studio penceresinde tıklatın **yenileme** altında **tanılama özeti**.

     ![Yenile'yi tıklatın](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-refreshstorage.png)

     Merhaba **tanılama özeti** bölümünde son 15 dakika günlükleri hello için varsayılan olarak gösterilir. Daha fazla günlükleri hello dönem toosee değiştirebilirsiniz.

     ("Tablosu bulunamadı" hata iletisi alırsanız, etkin sonra izleme hello toohello sayfaları taranan doğrulayın **uygulama günlüğü (Depolama)** ve tıklattığınız sonra **kaydetmek**.)

     ![Depolama günlükleri](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-storagelogs.png)

     Bu konuda gördüğünüz bildirimi bkz **işlem kimliği** ve **iş parçacığı kimliği** hello dosya sistemi günlükleri alma her oturum için. Ek alanlar hello Azure depolama tablosu doğrudan görüntüleyerek görebilirsiniz.
13. Tıklatın **tüm uygulama günlüklerini görüntüle**.

     Merhaba izleme günlüğü tablosu hello Azure depolama tablo Görüntüleyicisi'nde görüntülenir.

     ("Dizi bir öğe içermiyor" bir hata alırsanız, açmak **Sunucu Gezgini**, depolama hesabınızın hello altında hello düğümünü **Azure** düğümünü ve ardından sağ **tabloları**tıklatıp **yenileme**.)

     ![Tablo görünümünde depolama günlükleri](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracelogtableview.png)

     Bu görünüm, diğer bir görünümlerde görmüyorum ek alanlar gösterir. Bu görünüm, da toofilter günlükleri bir sorgu oluşturmak için özel sorgu oluşturucu kullanıcı arabirimini kullanarak sağlar. Daha fazla bilgi için bkz. tablo kaynaklarla çalışmak - varlıklarda filtreleme [Sunucu Gezgini ile depolama kaynaklarını gözatma](http://msdn.microsoft.com/library/ff683677.aspx).
14. tek bir satır hello ayrıntılarını adresindeki toolook hello satırlardan birinin çift tıklayın.

     ![Sunucu Gezgininde izleme tablosu](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracetablerow.png)

## <a name="failedrequestlogs"></a>Başarısız istek izleme günlüklerini görüntüle
Başarısız istek izleme günlüklerini toounderstand hello ayrıntılarını, IIS URL yeniden yazma işlemi veya kimlik doğrulama sorunları gibi senaryolarda bir HTTP isteğinin nasıl işlediğinin gerektiğinde faydalıdır.

Azure web apps kullanım hello aynı başarısız istek IIS 7.0 ile kullanılabilir ve sonraki izleme işlevselliği. Erişim toohello hangi hatalarını yapılandırma IIS ayarlarını kaydedilir, ancak yok. Başarısız istek izleme etkinleştirdiğinizde, tüm hataları yakalanır.

Visual Studio kullanarak başarısız istek izleme etkinleştirebilirsiniz, ancak Visual Studio'da görüntüleyemezsiniz. Bu günlükler XML dosyalarıdır. yalnızca günlük hizmeti akış hello düz metin modunda okunabilir sayılan dosyaları izler: *.txt*, *.html*, ve *.log* dosyaları.

Yerel olarak bir FTP aracı toodownload kullandıktan sonra veya FTP aracılığıyla doğrudan tarayıcıda başarısız istek izleme günlüklerini görüntüleyebilirsiniz bunları tooyour yerel bilgisayar. Bu bölümde, bir tarayıcıda doğrudan görüntülediğiniz.

1. Merhaba, **yapılandırma** hello sekmesinde **Azure Web uygulaması** den açılan pencere **Sunucu Gezgini**, değiştirme **başarısız istek izleme özellikli**çok**üzerinde**ve ardından **kaydetmek**.

    ![Başarısız istek izlemeyi etkinleştir](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequeston.png)
2. Merhaba adres çubuğundaki hello web uygulaması gösteren hello tarayıcı penceresinin bir ek karakter toohello URL'sini ekleyin ve Enter toocause 404 hatası'ı tıklatın.

    Bu oluşturulan bir başarısız istek izleme günlük toobe neden olur ve hello aşağıdaki adımlar nasıl tooview ya da indirme hello günlük gösterir.
3. Visual Studio'da, hello **yapılandırma** hello sekmesinde **Azure Web uygulaması** penceresinde tıklatın **Yönetim Portalı'nda Aç**.
4. Merhaba, [Azure Portal](https://portal.azure.com) **ayarları** web uygulamanız için dikey tıklayın **dağıtım kimlik bilgileri**ve ardından yeni bir kullanıcı adı ve parolayı girin.

    ![Yeni FTP kullanıcı adı ve parola](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-enterftpcredentials.png)

    ** Oturum açtığınızda hello web uygulaması adı öneki tooit ile toouse hello tam kullanıcı adına sahip. Örneğin, "myId" bir kullanıcı adı girin ve "Örneğin" ifadesini hello site ise, "myexample\myid" oturum açın.
5. Yeni bir tarayıcı penceresinde altında gösterilen toohello URL Git **FTP ana bilgisayar adı** veya **FTPS konak adı** hello içinde **Web uygulaması** dikey web uygulamanız için.
6. Daha önce (dahil hello web uygulaması adı öneki hello kullanıcı adı için) oluşturulan hello FTP kimlik bilgilerini kullanarak oturum açın.

    Merhaba tarayıcı hello web uygulaması hello kök klasörünü gösterir.
7. Açık hello *LogFiles* klasör.

    ![LogFiles klasörünü açın](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilesfolder.png)
8. W3SVC artı bir sayısal değer adlı hello klasörünü açın.

    ![W3SVC klasörünü açın](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfolder.png)

    Merhaba klasör XML dosyaları için başarısız istek izleme etkin sonra günlüğe kaydedilmiş hataları ve bir tarayıcı tooformat hello XML kullanabileceğiniz bir XSL dosyasını içerir.

    ![W3SVC klasörü](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfoldercontents.png)
9. Merhaba XML dosyası toosee izleme bilgi almak için başarısız istek hello için tıklatın.

    Merhaba aşağıda bir örnek hata için hello izleme bilgilerinin bir parçası gösterilmiştir.

    ![Başarısız istek izleme tarayıcıda](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequestinbrowser.png)

## <a name="nextsteps"></a>Sonraki Adımlar
Nasıl Visual Studio kolay tooview kolaylaştırır gördüğünüz Azure web uygulaması tarafından oluşturulan günlükleri. Merhaba aşağıdaki bölümlerde bağlantılar toomore kaynakları ilgili konularda verilmiştir:

* Azure web uygulaması sorunlarını giderme
* Visual Studio'da hata ayıklama
* Uzaktan hata ayıklama ile Azure
* ASP.NET uygulamalarında izleme
* Analiz etme web sunucu günlükleri
* Başarısız istek izleme günlüklerini analiz etme
* Hata ayıklama bulut Hizmetleri

### <a name="azure-web-app-troubleshooting"></a>Azure web uygulaması sorunlarını giderme
Azure App Service'deki web uygulamaları sorunlarını giderme hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [Nasıl toomonitor web uygulamaları](/manage/services/web-sites/how-to-monitor-websites/)
* [Bellek sızıntıları Visual Studio 2013 ile Azure Web uygulamalarında araştırma](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/20/investigating-memory-leaks-in-azure-web-sites-with-visual-studio-2013.aspx). Microsoft ALM blog gönderisi yönetilen bellek sorunları çözümlemek için Visual Studio özellikleri hakkında.
* [Azure web apps çevrimiçi araçları hakkında bilmeniz](https://azure.microsoft.com/blog/2014/03/28/windows-azure-websites-online-tools-you-should-know-about-2/). Blog gönderisi Amit Apple tarafından.

Belirli bir sorun giderme sorusu ile daha fazla yardım için bir iş parçacığı forumları aşağıdaki hello birini başlatabilirsiniz:

* [Azure Forumu hello ASP.NET sitesinde hello](http://forums.asp.net/1247.aspx/1?Azure+and+ASP+NET).
* [MSDN'deki Azure Forumu hello](http://social.msdn.microsoft.com/Forums/windowsazure/).
* [StackOverflow.com](http://www.stackoverflow.com).

### <a name="debugging-in-visual-studio"></a>Visual Studio'da hata ayıklama
Merhaba toouse Visual Studio modunda nasıl hata ayıklama hakkında daha fazla bilgi için bkz: [Visual Studio'da hata ayıklamayı](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx) MSDN konusuna ve [Visual Studio 2010 ile hata ayıklama ipuçları](http://weblogs.asp.net/scottgu/archive/2010/08/18/debugging-tips-with-visual-studio-2010.aspx).

### <a name="remote-debugging-in-azure"></a>Uzaktan hata ayıklama ile Azure
Azure web uygulamaları ve Web işleri için uzaktan hata ayıklama hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [Giriş tooRemote hata ayıklama Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/).
* [Giriş tooRemote uzaktan hata ayıklama içinde Azure App Service Web Apps hata ayıklama bölüm 2-](https://azure.microsoft.com/blog/2014/05/07/introduction-to-remote-debugging-azure-web-sites-part-2-inside-remote-debugging/)
* [Giriş tooRemote Azure App Service Web Apps bölümü 3 - çok örnekli ortamı ve GIT hata ayıklama](https://azure.microsoft.com/blog/2014/05/08/introduction-to-remote-debugging-on-azure-web-sites-part-3-multi-instance-environment-and-git/)
* [Web işleri hata ayıklama (video)](https://www.youtube.com/watch?v=ncQm9q5ZFZs&list=UU_SjTh-ZltPmTYzAybypB-g&index=1)

Bir Azure Web API'si veya Mobile Services arka uç, web uygulamanızın kullanır ve bakın, toodebug ihtiyacınız varsa [Visual Studio .NET arka ucu hata ayıklama](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx).

### <a name="tracing-in-aspnet-applications"></a>ASP.NET uygulamalarında izleme
Merhaba Internet üzerinde kullanılabilir izleme hiçbir kapsamlı ve güncel tanıtımları tooASP.NET vardır. Merhaba en iyi yapabileceğiniz olduğu ile çalışmaya başlama MVC kaydetmedi henüz mevcut ve yeni Web günlüğü ile desteklemek için Web Forms belirli sorunları odaklanan yazıları için yazılmış eski giriş malzemeleri. Bazı iyi yer toostart kaynakları aşağıdaki hello şunlardır:

* [İzleme ve Telemetri (Azure ile gerçek bulut uygulamaları derleme)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry).<br>
  E-kitap bölüm Azure bulut uygulamalarında izleme için öneriler.
* [ASP.NET izleme](http://msdn.microsoft.com/library/ms972204.aspx)<br/>
  Eski ancak yine de iyi bir kaynak için bir temel giriş toohello konu.
* [İzleme dinleyicileri](http://msdn.microsoft.com/library/4y5y10s7.aspx)<br/>
  İzleme dinleyicileri hakkında bilgi hello belirttiğinizden değil ancak [WebPageTraceListener](http://msdn.microsoft.com/library/system.web.webpagetracelistener.aspx).
* [İzlenecek yol: ASP.NET izleme System.Diagnostics izleme ile tümleştirme](http://msdn.microsoft.com/library/b0ectfxd.aspx)<br/>
  Bu çok eski olduğundan, ancak bazı ek bilgiler içeren bu hello giriş makalesi kapsamaz.
* [ASP.NET MVC Razor görünümleri izleme](http://blogs.msdn.com/b/webdev/archive/2013/07/16/tracing-in-asp-net-mvc-razor-views.aspx)<br/>
  Razor görünümlerinde izlemenin yanı sıra nasıl toocreate hata filtre sırası toolog MVC uygulamasındaki tüm işlenmeyen özel durumlar hello post de açıklanmaktadır. Nasıl toolog tüm işlenmemiş hakkında bilgi için bir Web Forms uygulamasında özel durumları görmek hello Global.asax örnekte [hata işleyicileri için tam bir örnek](http://msdn.microsoft.com/library/bb397417.aspx) konusuna bakın. MVC veya Web Forms belirli özel durumları toolog istiyor ancak hello varsayılan framework etkili kendileri için işleme izin yaparsanız catch ve aşağıdaki örneğine hello olduğu gibi yeniden oluşturma:

        try
        {
           // Your code that might cause an exception toobe thrown.
        }
        catch (Exception ex)
        {
            Trace.TraceError("Exception: " + ex.ToString());
            throw;
        }
* [Tanılama izleme oturum açmasını hello Azure komut satırı (artı Glimpse'in!) akış](http://www.hanselman.com/blog/StreamingDiagnosticsTraceLoggingFromTheAzureCommandLinePlusGlimpse.aspx)<br/>
  Nasıl toouse hello komut satırı toodo Bu öğretici gösterir nasıl toodo Visual Studio. [Glimpse'in](http://www.hanselman.com/blog/IfYoureNotUsingGlimpseWithASPNETForDebuggingAndProfilingYoureMissingOut.aspx) ASP.NET uygulamalarında hata ayıklama için bir araçtır.
* [Web uygulamaları günlüğe kaydetme ve tanılama - David Ebbo ile kullanarak](/documentation/videos/azure-web-site-logging-and-diagnostics/) ve [- David Ebbo ile Web uygulamaları günlüklerinden akış](/documentation/videos/log-streaming-with-azure-web-sites/)<br>
  Videolar Scott Hanselman ve David Ebbo.

Hata günlüğü için alternatif bir toowriting kendi izleme kodu toouse açık kaynaklı günlüğe kaydetme gibi çerçevedir [ELMAH](http://nuget.org/packages/elmah/). Daha fazla bilgi için bkz: [Scott Hanselman'ın blog yazılarını hakkında ELMAH](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx).

Ayrıca, toouse ASP.NET yoksa veya Azure'dan tooget akış istiyorsanız System.Diagnostics izleme günlükleri unutmayın. Merhaba günlük hizmeti akış Azure web uygulaması herhangi akışı sağlanacak *.txt*, *.html*, veya *.log* hello bulduğu dosya *LogFiles* klasör. Bu nedenle, toohello dosya sistemi hello web uygulamasının Yazar kendi günlük sistem oluşturabilir ve dosyanızı otomatik olarak akışı ve indirilen. Tüm toodo sahip olan dosyaları hello oluşturur yazma uygulama kodu *d:\home\logfiles* klasör.

### <a name="analyzing-web-server-logs"></a>Analiz etme web sunucu günlükleri
Web sunucusu günlüklerini çözümleme hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [LogParser](http://www.microsoft.com/download/details.aspx?id=24659)<br/>
  Web sunucusu günlüklerini verilerini görüntülemek için bir aracı (*.log* dosyaları).
* [IIS performans sorunları veya uygulama LogParser kullanarak hataları giderme](http://www.iis.net/learn/troubleshoot/performance-issues/troubleshooting-iis-performance-issues-or-application-errors-using-logparser)<br/>
  Tooanalyze web sunucusu kullanabileceğiniz bir giriş toohello günlük ayrıştırıcısı aracı günlüğe kaydeder.
* [LogParser kullanarak Robert McMurray'tarafından blog yazılarını](http://blogs.msdn.com/b/robert_mcmurray/archive/tags/logparser/)<br/>
* [Merhaba IIS 7.0, IIS 7.5 ve IIS 8.0 HTTP durum kodu](http://support.microsoft.com/kb/943891)

### <a name="analyzing-failed-request-tracing-logs"></a>Başarısız istek izleme günlüklerini analiz etme
Merhaba Microsoft TechNet Web sitesi içeren bir [kullanarak başarısız istek izleme](http://www.iis.net/learn/troubleshoot/using-failed-request-tracing) anlamak için yararlı olabilecek bölüm nasıl toouse Bu günlükler. Ancak, bu belge çoğunlukla başarısız istek izleme Azure Web uygulamalarında yapamayacağı IIS Yöneticisi'nde yapılandırma üzerinde durulmaktadır.

[GetStarted]: app-service-web-get-started-dotnet.md
[GetStartedWJ]: websites-dotnet-webjobs-sdk.md
