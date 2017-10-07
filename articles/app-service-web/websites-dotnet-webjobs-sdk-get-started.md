---
title: Azure App Service'te bir .NET WebJob aaaCreate | Microsoft Docs
description: "ASP.NET MVC ve Azure kullanarak çok katmanlı bir uygulama oluşturun. Azure App Service'in web uygulamasında ön uç çalıştırmalarında hello ve arka uç çalıştığı bir Web işi hello. Merhaba uygulama Entity Framework, SQL Database ve Azure depolama kuyrukları ve blobları kullanır."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/14/2017
ms.author: glenga
ms.openlocfilehash: d92fc4b81cc0d58f8e900f257e747af56d32b911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a>Azure Uygulama Hizmeti’nde .NET WebJob oluşturma
Bu öğretici nasıl toowrite hello kullanan basit bir çok katmanlı ASP.NET MVC 5 uygulaması için kod gösterir [WebJobs SDK](websites-dotnet-webjobs-sdk.md).

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Merhaba hello amacı [WebJobs SDK](websites-webjobs-resources.md) toosimplify hello kodu yazma için bir Web işi gerçekleştirebilirsiniz, görüntü işleme, sıra işleme, RSS toplama, dosya bakımı gibi genel görevleri ve e-postaları gönderme. Merhaba Web işleri SDK'si, Azure Storage ve Service Bus ile çalışmak için görev zamanlama ve hataları işleme ve diğer birçok yaygın senaryolar için yerleşik özelliğine sahiptir. Ayrıca, sahip toobe Genişletilebilir tasarlanmış ve var olan bir [uzantıları için açık kaynak deposu](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

Merhaba örnek uygulama bir reklam Bülteni panosudur. Kullanıcılar yansımaları reklamları için karşıya yükleyebilir ve bir arka uç işlem hello görüntüleri toothumbnails dönüştürür. Merhaba ad listesi sayfası hello küçük resimleri gösterir ve hello ad Ayrıntılar sayfası hello tam boyutlu görüntüyü gösterir. Bir ekran görüntüsü aşağıda verilmiştir:

![Reklam listesi](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

Bu örnek uygulama ile çalışır [Azure kuyrukları](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) ve [Azure BLOB'ları](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage). Merhaba öğretici nasıl toodeploy hello uygulama çok gösterir[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) ve [Azure SQL veritabanı](http://msdn.microsoft.com/library/azure/ee336279).

## <a id="prerequisites"></a>Önkoşullar
Merhaba Öğreticisi, bildiğinizi varsayar nasıl toowork ile [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) Visual Studio projelerinde.

Merhaba öğretici ilk olarak Visual Studio 2013 için yazılmıştır, ancak Visual Studio'nun daha yeni sürümlerinde kullanılabilir. Visual Studio 2015 veya 2017 kullanıyorsanız, hello uygulamayı yerel olarak çalıştırmadan önce hello değiştirmelisiniz Not `Data Source` hello Web.config ve App.config dosyalarından hello SQL Server yerel veritabanı bağlantı dizesinde parçası `Data Source=(localdb)\v11.0` çok`Data Source=(LocalDb)\MSSQLLocalDB`.

> [!NOTE]
> <a name="note"></a>Bu öğretici bir Azure hesabı toocomplete olması gerekir:
>
> * Yapabilecekleriniz [ücretsiz bir Azure hesabı açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): Ücretli Azure hizmetlerini tootry çıkışı kullanabilirsiniz, ve hatta kullanıldıktan sonra hello hesabı sürdürebilir ve Web siteleri gibi ücretsiz Azure hizmetlerinden faydalanabilirsiniz krediler alırsınız. Açıkça ayarlarınızı değiştirip ücret toobe isteyin sürece kredi kartınız asla ücretlendirilir.
> * Yapabilecekleriniz [Visual Studio aboneleri için aylık Azure kredi etkinleştirme](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): aboneliğinizi Ücretli Azure hizmetlerinizi kullanabildiğiniz her ay kredi verir.
>
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
>
>

## <a id="learn"></a>Öğrenecekleriniz
Merhaba öğretici nasıl toodo hello aşağıdaki görevleri gösterir:

* (Yalnızca Visual Studio 2013 ve 2015 kullanıcılar için) hello Azure SDK'sı yükleyerek makinenizi Azure geliştirme için etkinleştirin.
* Merhaba ilişkili web projesi dağıttığınızda, bir Azure Web işi otomatik olarak dağıtan bir konsol uygulama projesi oluşturun.
* Web işleri SDK'si arka uç hello geliştirme bilgisayarındaki yerel olarak test edin.
* App Service'te bir Web işleri arka uç tooa web uygulaması ile uygulama yayımlama.
* Dosyaları karşıya yükleme ve hello Azure Blob hizmeti depolayabilirsiniz.
* Hello Azure WebJobs SDK toowork Azure Storage kuyruklarını ve BLOB'ları kullanın.

## <a id="contosoads"></a>Uygulama mimarisi
Merhaba örnek uygulamanın kullandığı hello [kuyruk merkezli çalışma deseni](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff yük hello CPU yoğunluklu iş küçük resimleri tooa arka uç işlem oluşturma.

Merhaba uygulama ads Entity Framework Code First toocreate hello tabloları ve erişim hello verilerini kullanarak bir SQL veritabanında depolar. Her ad için hello veritabanı iki URL depolar: hello tam boyutlu görüntüyü, diğeri hello küçük resim için için.

![Reklam tablosu](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

Ne zaman bir kullanıcı karşıya yükleyen bir görüntü, hello web uygulaması hello görüntüde depolayan bir [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), ve hello veritabanı toohello blob'u işaret eden bir URL ile Merhaba ad bilgilerini depolar. AT hello aynı zaman, ileti tooan Azure kuyruk yazar. Bir Azure Web işi çalışan bir arka uç işleminde hello Web işleri SDK'si hello sıra yeni iletiler için yoklar. Yeni bir ileti görüntülendiğinde, görüntü için bir küçük resim hello Web işi oluşturur ve küçük resim URL'si veritabanı alanını bu reklam güncelleştirmeleri hello. Merhaba uygulaması hello bölümlerini nasıl etkileşim kurduğu gösterilmektedir bir diyagram şöyledir:

![Contoso Ads mimarisi](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
Merhaba öğretici yönergeleri uygulayın tooAzure SDK .NET 2.7.1 veya üzeri.

## <a id="storage"></a>Bir Azure depolama hesabı oluşturma
Bir Azure depolama hesabı, kuyruk ve blob verilerini hello bulutta depolamak için kaynaklar sağlar. Merhaba Pano için Web işleri SDK'si toostore günlük verilerini hello tarafından da kullanılır.

Gerçek dünya uygulamada genellikle uygulama verilerine karşı günlük verileri için ayrı hesaplar ve test verilerine karşı üretim verileri için ayrı hesaplar oluşturursunuz. Bu öğreticide yalnızca tek bir hesap kullanacaksınız.

1. Açık hello **Sunucu Gezgini** Visual Studio'daki.
2. Sağ hello **Azure** düğümünü ve ardından **tooMicrosoft Azure aboneliğine Bağlan...** .
   
   ![TooAzure Bağlan](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. Azure kimlik bilgilerinizi kullanarak oturum açın.
4. Sağ **depolama** altında Azure düğümü hello ve ardından **depolama hesabı oluştur**.
   
   ![Depolama hesabı oluşturma](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. Merhaba, **depolama hesabı oluştur** iletişim kutusunda, hello depolama hesabı için bir ad girin.

    Merhaba adı olmalı benzersiz olmalıdır (başka bir Azure depolama hesabı hello olabilir aynı adı). Girdiğiniz hello adı zaten kullanımda olduğundan, bir fırsat toochange alırsınız.

    Depolama hesabınız olacak URL tooaccess hello *{ad}*. core.windows.net.
6. Set hello **bölge veya benzeşim grubunda** aşağı açılan liste toohello bölgeye en yakın tooyou.

    Bu ayar, hangi Azure veri merkezi depolama hesabınız barındıracak belirtir. Bu öğretici için tercih ettiğiniz bir dikkat çekici fark yapmaz. Ancak, bir üretim web uygulaması için web sunucunuz, depolama hesabı toobe hello içinde istediğiniz aynı bölge toominimize gecikme süresi ve veri çıkış ücretleri. (daha sonra oluşturacağınız) hello web uygulamasını sipariş toominimize gecikme hello web uygulamasına erişme olabildiğince toohello tarayıcılar kapatmak gibi veri merkezi olması gerekir.
7. Set hello **çoğaltma** aşağı açılan listesinde çok**yerel olarak yedekli**.

    Bir depolama hesabı için coğrafi çoğaltma etkinleştirildiğinde, depolanan hello içerik çoğaltılmış tooa ikincil veri merkezine tooenable yük devretme toothat hello birincil konumda büyük bir felaket durumunda konumdur. Coğrafi çoğaltma ek ücretlere neden olabilir. Test ve geliştirme hesaplarında genellikle coğrafi çoğaltma için toopay istemezsiniz. Daha fazla bilgi için bkz. [Depolama hesabı oluşturma, yönetme veya silme](../storage/common/storage-create-storage-account.md).
8. **Oluştur**'a tıklayın.

    ![Yeni depolama hesabı](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <a id="download"></a>Merhaba uygulama indirin
1. İndirip hello sıkıştırmasını [tamamlanan çözümü](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).
2. Visual Studio’yu çalıştırın.
3. Merhaba gelen **dosya** menüsünü seçin **Aç > Proje/çözüm**hello çözümü indirdiğiniz toowhere gidin ve ardından hello çözüm dosyasını açın.
4. CTRL + SHIFT + B toobuild hello çözüm tuşuna basın.

    Varsayılan olarak, Visual Studio hello dahil edilmeyen hello NuGet paket içeriği otomatik olarak yükler *.zip* dosyası. Merhaba paketler geri yüklenmezse varsa bunları el ile giderek toohello tarafından yükleyin **çözüm için NuGet paketlerini Yönet** iletişim ve hello tıklayarak **geri** düğmesine sağ hello üstünde.
5. İçinde **Çözüm Gezgini**, olduğundan emin olun **ContosoAdsWeb** hello başlangıç projesi olarak seçilir.

## <a id="configurestorage"></a>Depolama hesabınızı Hello uygulama toouse yapılandırma
1. Açık Merhaba uygulaması *Web.config* hello ContosoAdsWeb projesinde dosya.

    Merhaba dosyası bir SQL bağlantı dizesi ve BLOB'lar ve kuyruklarla çalışmaya yönelik bir Azure depolama bağlantı dizesi içerir.

    Merhaba SQL bağlantı dizesi işaret tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) veritabanı.

    Merhaba depolama bağlantı dizesi yer tutucuları Merhaba, depolama hesabı adı ve erişim anahtarı için olan bir örnektir. Bu hello adını ve anahtarını depolama hesabınızın sahip bir bağlantı dizesi ile değiştirirsiniz.  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    Merhaba depolama bağlantı dizesi, Web işleri SDK'sini kullanan hello adı hello olduğundan AzureWebJobsStorage varsayılan olarak adlandırılır. Merhaba hello Azure ortamı tooset yalnızca bir bağlantı dizesi değerine sahip biçimde aynı adı buraya kullanılır.
2. İçinde **Sunucu Gezgini**, depolama hesabınız hello altında sağ **depolama** düğümünü ve ardından **özellikleri**.

    ![Depolama hesabı Özellikler'i tıklatın](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. Merhaba, **özellikleri** penceresinde, tıklatın **depolama hesabı anahtarlarını**ve hello üç nokta'ı tıklatın.

    ![Depolama hesabı anahtarları](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. Kopya hello **bağlantı dizesi**.

    ![Depolama hesabı anahtarları iletişim](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. Merhaba Hello depolama bağlantı dizesini değiştirin *Web.config* dosyasını kopyaladığınız hello bağlantı dizesine sahip. Her şeyi hello tırnak işaretleri içindeki ancak yapıştırmadan önce hello tırnak işaretleri dahil değil seçtiğinizden emin olun.
6. Açık hello *App.config* hello ContosoAdsWebJob proje dosyasında.

    Bu dosya iki depolama bağlantı dizeleri, bir uygulama verileri için ve günlüğe kaydetme için bir sahiptir. Uygulama verilerini ve günlüğe kaydetme için ayrı bir depolama hesaplarını kullanabilirsiniz ve kullanabileceğiniz [birden çok depolama hesapları için verileri](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs). Bu öğreticide, tek bir depolama hesabına kullanacaksınız. Merhaba depolama hesabı anahtarlarını yer tutucular Hello bağlantı dizelerine sahipsiniz.

    ```
    <configuration>
        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/>
    </connectionStrings>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    </configuration>

    ```

    Varsayılan olarak, Web işleri SDK'si hello için bağlantı dizelerini AzureWebJobsStorage ve AzureWebJobsDashboard adlı arar. Alternatif olarak, şunları yapabilirsiniz [ancak istediğiniz ve açıkça toohello içinde geçirmek hello bağlantı dizesi depolamak `JobHost` nesne](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).
7. Her iki storage bağlantı dizelerini daha önce kopyaladığınız hello bağlantı dizesi ile değiştirin.
8. Yaptığınız değişiklikleri kaydedin.

## <a id="run"></a>Merhaba uygulama yerel olarak çalıştırma
1. Merhaba uygulamasının toostart hello web ön uç CTRL + F5 tuşuna basın.

    Merhaba varsayılan tarayıcı toohello giriş sayfası açılır. (Merhaba web projesi çalıştırır, yaptığınız çünkü hello başlangıç projesi.)

    ![Contoso Ads giriş sayfası](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. toostart hello WebJob arka hello uygulamasının sağ hello ContosoAdsWebJob projesinde **Çözüm Gezgini**ve ardından **hata ayıklama** > **başlangıç yeni örneği** .

    Bir konsol uygulama penceresi açar ve hello WebJobs SDK JobHost nesne toorun başlatıldı belirten günlük iletilerini görüntüler.

    ![Bu hello arka uç gösteren konsol uygulama penceresi çalışıyor](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. Tarayıcınızda, tıklatın **bir Ad oluşturmak**.
4. Bazı test verilerini girin, bir görüntü tooupload seçin ve ardından **oluşturma**.

    ![Sayfa oluşturma](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    Merhaba uygulama toohello dizin sayfasına gider, ancak işleme henüz tamamlanmadığından hello yeni ad için bir küçük resim göstermez.

    Bu sırada, kısa bekleme bir kuyruk iletisi alındı ve işlenmiş olan bir günlük iletisi hello konsol uygulaması penceresinde gösterir.

    ![Bir kuyruk iletisi işlendiğini gösteren konsol uygulama penceresi](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. İletileri günlüğe kaydetme hello konsol uygulaması penceresinde hello gördükten sonra hello dizin sayfası toosee hello küçük yenileyin.

    ![Dizin sayfası](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. Tıklatın **ayrıntıları** ad toosee hello tam boyutlu görüntü için.

    ![Ayrıntılar sayfası](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

Merhaba uygulama'yı yerel bilgisayarınızda çalışır durumda ve bilgisayarınızın, ancak üzerinde bulunan veritabanı Kuyruklarla Çalışma ve içinde BLOB'bir SQL Server kullanarak hello bulut. Bölümden hello bulut veritabanı yanı sıra bulut BLOB'ları ve kuyrukları kullanma hello uygulaması hello bulutta çalıştıracaksınız.  

## <a id="runincloud"></a>Merhaba uygulaması hello bulutta çalışan
Siz gerçekleştirirsiniz adımları toorun hello hello bulut uygulamasında aşağıdaki hello:

* TooWeb uygulamaları dağıtın. Visual Studio otomatik olarak yeni bir web uygulaması App Service ve bir SQL veritabanı örneği oluşturur.
* Merhaba web uygulama toouse Azure SQL veritabanı ve depolama hesabı yapılandırın.

Merhaba bulutta çalıştırılırken bazı ads oluşturduktan sonra hello Web işleri SDK'si Pano toosee hello İzleme özelliklerini toooffer sahip zengin görürsünüz.

### <a name="deploy-tooweb-apps"></a>TooWeb uygulamaları dağıtma

1. Merhaba tarayıcı ve hello konsol uygulaması penceresini kapatın.
2. Merhaba Hello adımları [tooAzure SQL veritabanı ile yayımlama](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) bölümü.
3. Merhaba dağıtma adımları tamamladıktan sonra bu makaledeki hello kalan görevlere devam edin.

### <a name="configure-hello-web-app-toouse-your-azure-sql-database-and-storage-account"></a>Azure SQL veritabanı ve depolama hesabınızı Hello web uygulama toouse yapılandırın
En iyi güvenlik uygulaması çok olan[bağlantı dizeleri gibi hassas bilgileri kaynak kodu depoları içinde depolanan dosyaları içinde Geçirilmemesi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets). Azure, bir şekilde toodo sağlar: ASP.NET yapılandırma API'leri hello uygulama Azure'da çalıştırıldığında bu değerleri otomatik olarak seçmesini ve hello Azure ortamı bağlantı dizesini ve diğer ayar değerlerini ayarlayabilirsiniz. Bu değerleri kullanarak Azure'da ayarlayabilirsiniz **Sunucu Gezgini**, Azure portalı, Windows PowerShell hello veya hello platformlar arası komut satırı arabirimi. Daha fazla bilgi için bkz: [nasıl uygulama dizeleri ve bağlantı dizeleri çalışma](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).

Bu bölümde, kullandığınız **Sunucu Gezgini** azure'da tooset bağlantı dizesi değerleri.

1. İçinde **Sunucu Gezgini**, web uygulamanızı altında sağ **Azure > uygulama hizmeti > {kaynak grubunuz}**ve ardından **görünüm ayarlarını**.

    Merhaba **Azure Web uygulaması** penceresi açılır hello üzerinde **yapılandırma** sekmesi.
2. Değişiklik hello adını hello DefaultConnection bağlantı dizesi toohello seçtiğiniz hello hello SQL veritabanı yapılandırdığınızda [tooAzure SQL veritabanı ile yayımlama](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) makalesi.

    Zaten hello sağ bağlantı dizesi değerine sahip şekilde ilişkilendirilmiş bir veritabanı ile Merhaba web uygulaması oluşturduğunuzda azure, bu bağlantı dizesi otomatik olarak oluşturulur. Yalnızca, kodunuzu aramakta hello adı toowhat değiştirirsiniz.
3. AzureWebJobsStorage ve AzureWebJobsDashboard adlı iki yeni bağlantı dizeleri ekleyin. Merhaba veritabanı türü çok ayarlamak**özel**ve aynı değeri hello için daha önce kullanılan kümesi hello bağlantı dizesi değeri toohello *Web.config* ve *App.config* dosyaları. (Merhaba tüm bağlantı dizesi, yalnızca hello erişim anahtarı içerir ve hello tırnak işaretleri dahil etmeyin emin olun.)

    Bu bağlantı dizeleri hello Web işleri SDK'si ve uygulama verileri için bir günlük kaydı için bir tarafından kullanılır. Daha önce anlatıldığı gibi uygulama verileri için hello hello web ön uç kodu tarafından da kullanılır.
4. **Kaydet** düğmesine tıklayın.

    ![Azure Portalı'nda bağlantı dizeleri](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. İçinde **Sunucu Gezgini**hello web uygulaması sağ tıklayın ve ardından **durdurmak**.
6. Merhaba web uygulaması durdurulduktan sonra hello web uygulaması tekrar sağ tıklayın ve ardından **Başlat**.

   Merhaba WebJob yayımladığınızda, ancak bir yapılandırma değişikliği yaptığınızda durdurur otomatik olarak başlar. toorestart, hello web uygulaması yeniden başlatabilir veya hello hello Web işi yeniden [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715). Bu genellikle önerilen toorestart hello web yapılandırma değişikliğinden sonra uygulamasıdır.
7. Adres çubuğunu hello web uygulaması URL'si sahip hello tarayıcı penceresini yenileyin.

    Merhaba giriş sayfası görüntülenir.
8. Ne zaman yaptığınız gibi bir ad oluşturun, [hello uygulama yerel olarak çalıştırılan](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).

   küçük resim ilk olmadan Hello dizin sayfası gösterilir.
9. Birkaç saniye sonra Hello sayfayı yenileyin ve hello küçük resmi görüntülenir.

   Hello küçük resim görünmüyorsa, toowait veya bunu dakika hello WebJob toorestart için olabilir. Biraz varsa sonra hala hello sayfasında, hello WebJob yenilediğinizde hello küçük resim otomatik olarak başlatılmamış olabilir görmüyorum. Bu durumda, toohello Git **uygulama hizmetleri** dikey penceresinde hello [Azure portal](https://portal.azure.com/), web uygulamanızı bulun ve ardından **Başlat**.

### <a name="view-hello-webjobs-sdk-dashboard"></a>Görünüm hello Web işleri SDK'si Panosu
1. Merhaba, [Azure portal](https://portal.azure.com/)seçin hello **App Services dikey**web uygulamanızı bulun ve seçin **WebJobs**.
3. Select hello **günlükleri** sekmesi.

    ![Günlükleri sekmesi](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    Yeni bir tarayıcı sekmesi toohello WebJobs SDK panosu açılır. Başlangıç Panosu WebJob çalışıyor ve işlevlerin bir listesini, kodunuzda Web işleri SDK'si tetiklenen bu hello gösterir. Bu hello gösterir.
4. Merhaba işlevleri toosee yürütülmesinin ayrıntılarını birini tıklatın.

    ![Web işleri SDK'si Panosu](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![Web işleri SDK'si Panosu](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    Merhaba **yeniden yürütme işlevi** bu sayfadaki düğme hello Web işleri SDK'si yeniden framework toocall hello işlevi neden, ve onu bir fırsat toochange hello geçirilen verileri toohello işlevi ilk verir.

> [!NOTE]
> Bitirdiğinizde hello web uygulaması, depolama hesabı ve SQL veritabanı örneğinde silme test, göz önünde bulundurun. Merhaba web uygulaması ücretsiz, ancak hello SQL depolama hesabı ve veritabanı örneği ücretler tahakkuk eder (barındırabilir, en az toohello küçük boyutu nedeniyle). Ayrıca, başlangıç web uygulaması çalıştıran değiştirmeden bırakırsanız, URL'nizi bulan herkes oluşturun ve reklamları görüntüleyin. 
>
>

### <a name="delete-your-web-app"></a>Web uygulamanızı Sil
Merhaba Portalı'nda toohello Git **uygulama hizmetleri** dikey penceresinde, bulun ve web uygulamanızı seçin ve ardından **silmek**. Yalnızca istiyorsanız tootemporarily önlemek başkalarının hello web uygulaması erişmesini tıklatın **durdurmak** yerine. Bu durumda ücretler hello SQL veritabanı ve depolama hesabı için tooaccrue devam eder.

### <a name="delete-your-storage-account"></a>Depolama hesabınızı silme
toodelete depolama hesabınızın bkz [bir depolama hesabını silmek](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account). 

### <a name="delete-your-database"></a>Veritabanınızı Sil
toodelete SQL veritabanı, hello bkz [Azure SQL Database REST API'sini](https://docs.microsoft.com/rest/api/sql/) belgeleri.

## <a id="create"></a>Merhaba uygulamayı sıfırdan oluşturma
Bu bölümde siz gerçekleştirirsiniz hello görevler:

* Visual Studio çözümü ile bir web projesi oluşturun.
* Merhaba veriler için bir sınıf kitaplığı projesi eklemek hello ön uç ve arka uç arasında paylaşılan erişim katmanı.
* Bir konsol uygulama projesi hello arka uç için etkin Web işleri dağıtımı ile ekleyin.
* NuGet paketleri ekleyin.
* Proje başvurularını ayarlayın.
* Merhaba önceki bölümde hello öğreticinin çalıştığınız indirilen hello uygulamasından uygulama kodu ve yapılandırma dosyalarını kopyalayın.
* Azure BLOB'ları ve kuyrukları ile çalışan ve Web işleri SDK'si hello hello kod hello bölümleri gözden geçirin.

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a>Bir web projesi ve sınıf kitaplığı proje bir Visual Studio çözümü oluşturun
1. Visual Studio'da, **dosya** > **yeni** > **proje**.
2. Merhaba, **yeni proje** iletişim kutusunda, seçin **Visual C#** > **Web** > **ASP.NET Web uygulaması (.NET Framework)**.
3. Merhaba projeyi ContosoAdsWeb olarak adlandırın, hello çözüm ContosoAdsWebJobsSDK adı (hello koyma hello çözüm adı tıklarsanız hello aynı klasöre yüklenen çözüm) ve ardından **Tamam**.

    ![Yeni Proje](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. Merhaba, **yeni ASP.NET Web uygulaması** iletişim kutusunda, hello MVC şablonunu seçin ve Seç **kimlik doğrulamayı Değiştir**.

    ![Kimlik Doğrulamayı Değiştirme](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. Merhaba, **kimlik doğrulamayı Değiştir** iletişim kutusunda, seçin **doğrulaması yok**ve ardından **Tamam**.

    ![Kimlik Doğrulaması Yok](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. Merhaba, **yeni ASP.NET Web uygulaması** iletişim kutusunda, tıklatın **Tamam**.

    Visual Studio hello çözüm ve hello web projesi oluşturur.
7. İçinde **Çözüm Gezgini**hello çözümü (Merhaba proje değil) sağ tıklatın ve seçin **Ekle** > **yeni proje**.
8. Merhaba, **Yeni Proje Ekle** iletişim kutusunda, seçin **Visual C#** > **Windows Klasik Masaüstü** > **sınıf kitaplığı (.NET Framework)** şablonu.  
9. Ad hello proje *ContosoAdsCommon*ve ardından **Tamam**.

    Bu proje, hem ön uç hello hello Entity Framework bağlamına ve hello veri modeli içerir ve arka uç kullanır. Alternatif olarak, hello EF ile ilgili sınıflar hello web projesinde tanımlayın ve proje hello Web işi projesi başvuru. Ancak, Web işi projeniz gerekli olmayan bir başvuru tooweb derlemeleri sonra olurdu.

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a>Web işleri dağıtımı etkin olan bir konsol uygulama projesi ekleyin
1. Merhaba web projesi (değil hello çözüm ya da hello sınıf kitaplığı Proje) sağ tıklayın ve ardından **Ekle** > **yeni Azure Web işi projesi**.

    ![Yeni Azure Web işi projesinin menü seçimi](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. Merhaba, **Azure Web işine Ekle** iletişim kutusunda, her iki hello ContosoAdsWebJob girin **proje adı** ve hello **Web işi adı**. Bırakın **WebJob çalıştırma modu** çok ayarlamak**sürekli olarak çalıştır**.
3. **Tamam** düğmesine tıklayın.

   Visual Studio hello web projesi dağıttığınız her bir Web işi yapılandırılmış toodeploy olan bir konsol uygulaması oluşturur. başlangıç projesi oluşturduktan sonra görevleri aşağıdaki hello gerçekleştirilen, toodo:

   * Eklenen bir *webjob yayımlama settings.json* hello Web işi projesi özellikleri klasördeki dosya.
   * Eklenen bir *webjobs list.json* hello web projesi özellikleri klasörü dosyasında.
   * Merhaba Microsoft.Web.WebJobs.Publish NuGet paketi hello WebJob projesinde yüklü.

   Bu değişiklikler hakkında daha fazla bilgi için bkz: [nasıl Visual Studio'yu kullanarak Web işleri toodeploy](websites-dotnet-deploy-webjobs.md).

### <a name="add-nuget-packages"></a>NuGet paketleri ekleme
bir Web işi projesi için Hello yeni proje şablonu hello WebJobs SDK NuGet paketini otomatik olarak yükler [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) ve bağımlılıklarını.

Merhaba Web işi projesinin otomatik olarak yüklenen Web işleri SDK'si bağımlılık hello birini Azure Storage istemci kitaplığı (SCL) hello. Ancak, tooadd gerekir, BLOB'ları ve kuyrukları ile toohello web projesi toowork.

1. Açık hello **NuGet paketlerini Yönet** hello çözüm için iletişim kutusu.
2. Merhaba sol bölmesinde seçin **yüklü paketleri**.
3. Hello bulur *Azure Storage* paketini ve ardından **Yönet**.
4. Merhaba, **projeleri seçin** kutusu, select hello **ContosoAdsWeb** onay kutusunu işaretleyin ve ardından **Tamam**.

    Üç projenin hello Entity Framework toowork SQL veritabanındaki verileri kullanın.
5. Merhaba sol bölmesinde seçin **çevrimiçi**.
6. Hello bulur *EntityFramework* NuGet paketini bulun ve üç projenin tamamına yükleyin.

### <a name="set-project-references"></a>Proje başvurularını ayarlama
Bu nedenle hem de bir başvuru toohello ContosoAdsCommon projesine gerekir hem web hem de Web işi projeleri hello SQL veritabanı ile çalışır.

1. Merhaba ContosoAdsWeb projesinde bir başvuru toohello ContosoAdsCommon projesine ayarlayın. (Merhaba ContosoAdsWeb projesine sağ tıklayın ve ardından **Ekle** > **başvuru**. 
2. Merhaba, **başvuru Yöneticisi** iletişim kutusunda **projeleri** > **çözüm** > **ContosoAdsCommon**ve ardından **Tamam**.)
   
    Merhaba Web işi projesinin başvuruları görüntülerle çalışma ve bağlantı dizeleri erişmek için gerekir.

4. Merhaba ContosoAdsWebJob projesinde çok bir başvuru ayarlayın`System.Drawing` ve `System.Configuration`.

### <a name="add-code-and-configuration-files"></a>Kod ve yapılandırma dosyaları Ekle
Bu öğretici nasıl çok göstermez[MVC denetleyicileri ve yapı iskelesi kullanarak görünümleri oluşturma](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), nasıl çok[SQL Server veritabanları ile çalışan Entity Framework kod yazma](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), veya [hello temelleri zaman uyumsuz ASP.NET 4.5 programlama](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async). Bu nedenle, tüm bu kalır toodo hello yeni çözüm hello indirilen çözümden kod ve yapılandırma dosyaları Kopyala ' dir. Bunu sonra hello aşağıdaki bölümlerde Göster ve anahtar hello kod bölümlerini açıklamaktadır.

tooadd dosyalar tooa proje veya bir klasörü, sağ hello proje veya klasöre tıklatın **Ekle** > **varolan öğeyi**. Select hello dosyalarını tıklayın ve istediğiniz **Ekle**. Tooreplace var olan dosyaları isteyip istemediğinizi sorulursa tıklatın **Evet**.

1. Merhaba ContosoAdsCommon projesinde hello silme *Class1.cs* dosya ve kendi yer hello hello indirilen projeden aşağıdaki dosyaları ekleyin.

   * *Ad.cs*
   * *ContosoAdscontext.cs*
   * *BlobInformation.cs*
2. Merhaba ContosoAdsWeb projesinde hello hello indirilen projeden aşağıdaki dosyaları ekleyin.

   * *Web.config*
   * *Global.asax.cs*  
   * Merhaba, *denetleyicileri* klasörü: *AdController.cs*
   * Merhaba, *görünümler/paylaşılan* klasörü: *_Layout.cshtml* dosyası
   * Merhaba, *görünümler* klasörü: *Index.cshtml*
   * Merhaba, *görünümler/reklam* klasörü (öncelikle hello klasörü oluşturun): beş *.cshtml* dosyaları
3. Merhaba ContosoAdsWebJob projesinde hello hello indirilen projeden aşağıdaki dosyaları ekleyin.

   * *App.config* (Merhaba dosya türü filtresi çok değiştirme**tüm dosyaları**)
   * *Program.cs*
   * *Functions.cs*

Artık derleme, çalıştırmak ve hello öğreticide daha önce belirtildiği gibi hello uygulama dağıtabilirsiniz. Ancak, bunu yapmadan önce hello hala için dağıtılan hello ilk web uygulamasında çalışan Web işi durdurun. Aksi takdirde, bu Web işi yerel olarak oluşturulan sıra iletileri veya tüm kullanıyorsanız bu yana yeni bir web uygulamasında çalışan hello uygulama tarafından aynı hello depolama hesabı.

## <a id="code"></a>Merhaba uygulama kodu gözden geçirme
Merhaba aşağıdaki bölümlerde açıklanmıştır hello kod tooworking hello WebJobs SDK ile ve Azure Storage BLOB'lar ve kuyruklarla ilgili.

> [!NOTE]
> Merhaba kodu belirli toohello için Web işleri SDK'si, toohello Git [Program.cs ve Functions.cs](#programcs) bölümler.
>
>

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
Merhaba Ad.cs dosyası reklam kategorileri için bir numaralandırma ve reklam bilgileri için bir POCO varlık sınıfı tanımlar.

        public enum Category
        {
            Cars,
            [Display(Name="Real Estate")]
            RealEstate,
            [Display(Name = "Free Stuff")]
            FreeStuff
        }

        public class Ad
        {
            public int AdId { get; set; }

            [StringLength(100)]
            public string Title { get; set; }

            public int Price { get; set; }

            [StringLength(1000)]
            [DataType(DataType.MultilineText)]
            public string Description { get; set; }

            [StringLength(1000)]
            [DisplayName("Full-size Image")]
            public string ImageURL { get; set; }

            [StringLength(1000)]
            [DisplayName("Thumbnail")]
            public string ThumbnailURL { get; set; }

            [DataType(DataType.Date)]
            [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
            public DateTime PostedDate { get; set; }

            public Category? Category { get; set; }
            [StringLength(12)]
            public string Phone { get; set; }
        }

### <a name="contosoadscommon---contosoadscontextcs"></a>ContosoAdsCommon - ContosoAdsContext.cs
Merhaba ContosoAdsContext sınıfı hello reklam sınıfının Entity Framework bir SQL veritabanında depolayan bir DbSet koleksiyonunda kullanıldığını belirtir.

        public class ContosoAdsContext : DbContext
        {
            public ContosoAdsContext() : base("name=ContosoAdsContext")
            {
            }
            public ContosoAdsContext(string connString)
                : base(connString)
            {
            }
            public System.Data.Entity.DbSet<Ad> Ads { get; set; }
        }

Merhaba sınıfın iki Oluşturucusu vardır. Merhaba ilk hello web projesi tarafından kullanılan ve hello hello Web.config dosyasını veya hello Azure çalışma zamanı ortamı saklanan bir bağlantı dizesinin adını belirtir. Merhaba ikinci oluşturucu hello gerçek bağlantı dizesine toopass sağlar. Bir Web.config dosyası olmadığından, hello Web işi projesi tarafından gereklidir. Daha önce gördüğünüzle burada Bu bağlantı dizesi depolanır ve daha sonra nasıl hello DbContext sınıfını başlattığında hello kodu hello bağlantı dizesini alır görürsünüz.

### <a name="contosoadscommon---blobinformationcs"></a>ContosoAdsCommon - BlobInformation.cs
Merhaba `BlobInformation` bir görüntü blob'u bir kuyruk iletisi içinde kullanılan toostore bilgilerini bir sınıftır.

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb - Global.asax.cs
Hello adlı kod `Application_Start` yöntemi oluşturur bir *görüntüleri* blob kapsayıcısı ve bir *görüntüleri* henüz yoksa sıra. Bu, yeni bir depolama hesabı kullanarak başlattığınızda hello blob kapsayıcısının ve kuyruğun otomatik olarak oluşturulan gerekli sağlar.

Merhaba kod alır erişim toohello depolama hesabı hello hello depolama bağlantı dizesini kullanarak *Web.config* dosya ya da Azure çalışma zamanı ortamı.

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

Ardından, bir başvuru toohello alır *görüntüleri* blob kapsayıcısı, önceden var olmayan ve erişim izinlerini hello yeni kapsayıcı ayarlar hello kapsayıcı oluşturur. Varsayılan olarak, yeni kapsayıcılar yalnızca depolama hesabı kimlik bilgileri tooaccess BLOB'ları olan istemcilerin izin verin. Bu nokta toohello görüntü BLOB'larını URL'leri kullanarak görüntüleri gösterebilmek hello web uygulaması BLOB'lar toobe ortak hello.

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

Benzer bir kod alır başvuru toohello *thumbnailrequest* sıraya almak ve yeni bir sıra oluşturur. Bu durumda hiçbir izin değişikliği gerekli değildir.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb - _Layout.cshtml
Merhaba *_Layout.cshtml* dosya hello üstbilgi ve altbilgi hello uygulama adını ayarlar ve bir "Reklamlar" menü girişi oluşturur.

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Görünümler\Giriş\Dizin.cshtml
Merhaba *Views\Home\Index.cshtml* dosya hello giriş sayfasında kategori bağlantılarını gösterir. Merhaba bağlantılar geçirmek hello hello tamsayı değeri `Category` enum bir sorgu dizesi değişkeni toohello reklam dizini sayfasına içindeki.

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
Merhaba, *AdController.cs* dosya, hello Oluşturucusu çağrıları hello `InitializeStorage` BLOB'lar ve kuyruklarla çalışmaya yönelik bir API sağlayan yöntemi toocreate Azure Storage istemci Kitaplığı nesneleri.

Ardından, bir başvuru toohello hello kodu alır *görüntüleri* daha önce gördüğünüz gibi blob kapsayıcısı *Global.asax.cs*. Yaparken, varsayılan ayarlar [yeniden deneme ilkesi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) bir web uygulaması için uygun. Merhaba varsayılan üstel geri alma yeniden deneme ilkesi hello web uygulaması için geçici bir hata için tekrarlanan yeniden denemelerde bir dakikadan uzun süre askıya alabilir. Burada belirtilen hello yeniden deneme ilkesi üç her denemeden sonra toothree çalıştığında saniye bekler.

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

Benzer bir kod alır başvuru toohello *görüntüleri* sırası.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

Merhaba denetleyici kodlarının birçoğu bir DbContext sınıfı kullanarak bir Entity Framework veri modeli ile çalışmak için tipiktir. Merhaba HttpPost bir istisnadır `Create` yöntemi, bir dosya yükler ve blob depolama alanına kaydeder. Merhaba model bağlayıcı sağlar bir [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) nesne toohello yöntemi.

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

Merhaba kullanıcı dosya tooupload seçtiyseniz, hello kod hello dosyayı yükler, bir blob'a kaydeder ve hello Ad veritabanı kaydını toohello blob'u işaret eden bir URL ile güncelleştirir.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

Merhaba, karşıya yükleme hello hello koddur `UploadAndSaveBlobAsync` yöntemi. Merhaba blob, yüklemeleri ve kaydeder hello dosyası için bir GUID adı oluşturur ve bir başvuru toohello kaydedilmiş blob döndürür.

        private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
        {
            string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
            CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
            using (var fileStream = imageFile.InputStream)
            {
                await imageBlob.UploadFromStreamAsync(fileStream);
            }
            return imageBlob;
        }

Merhaba HttpPost sonra `Create` yöntemi bir blob'u karşıya yüklemeleri ve güncelleştirmeleri Merhaba veritabanı, bir görüntü için dönüştürme tooa küçük resim hazır olduğunu bir sıraya ileti tooinform hello arka uç işlemi oluşturur.

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

Merhaba hello HttpPost kodunu `Edit` yöntemi olduğunu benzer, hello kullanıcı yeni bir görüntü dosyası seçerse, bu ad zaten mevcut BLOB silinmelidir dışında.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

Bir ad sildiğinizde, BLOB'ları siler hello kod aşağıdadır:

        private async Task DeleteAdBlobsAsync(Ad ad)
        {
            if (!string.IsNullOrWhiteSpace(ad.ImageURL))
            {
                Uri blobUri = new Uri(ad.ImageURL);
                await DeleteAdBlobAsync(blobUri);
            }
            if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
            {
                Uri blobUri = new Uri(ad.ThumbnailURL);
                await DeleteAdBlobAsync(blobUri);
            }
        }
        private static async Task DeleteAdBlobAsync(Uri blobUri)
        {
            string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
            CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
            await blobToDelete.DeleteAsync();
        }

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a>ContosoAdsWeb - Views\Ad\Index.cshtml ve Details.cshtml
Merhaba *Index.cshtml* dosyası küçük resimleri hello ile diğer ad verileri görüntüler:

        <img  src="@Html.Raw(item.ThumbnailURL)" />

Merhaba *Details.cshtml* dosyası hello tam boyutlu görüntüyü gösterir:

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml ve Edit.cshtml
Merhaba *Create.cshtml* ve *Edit.cshtml* dosyaları belirtin etkinleştirir denetleyicisi tooget hello hello kodlama form `HttpPostedFileBase` nesnesi.

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

Bir `<input>` öğesi, bir dosya seçme iletişim kutusu hello tarayıcı tooprovide söyler.

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <a id="programcs"></a>ContosoAdsWebJob - Program.cs
Ne zaman hello Web işi başladığında hello `Main` yöntem çağrılarını hello WebJobs SDK `JobHost.RunAndBlock` yöntemi toobegin yürütme hello geçerli iş parçacığında tetiklenen işlevlerin.

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail yöntemi
bir kuyruk iletisi alındığında hello Web işleri SDK'si bu yöntemi çağırır. Merhaba yöntemi, bir küçük resim oluşturur ve yerleştirmelerin hello küçük resim hello veritabanındaki URL.

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within hello function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* Merhaba `QueueTrigger` özniteliği hello thumbnailrequest sırada yeni bir ileti alındığında bu hello WebJobs SDK toocall bu yöntem yönlendirir.

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    Merhaba `BlobInformation` hello kuyruk iletisi nesnedir hello otomatik olarak Serisi kaldırılan `blobInfo` parametresi. Merhaba kuyruk iletisi Hello yöntemi tamamlandığında silinir. Merhaba yöntemi tamamlanmadan önce başarısız olursa, hello kuyruk iletisi silinmez; 10 dakikalık kiralama süresi dolduktan sonra hello yeniden toplanmış ve işlenen yayımlanan toobe iletisidir. Bir ileti her zaman bir özel durum neden olursa bu sırası süresiz olarak yinelenen olmaz. 5 başarısız tooprocess bir ileti denemesinden sonra hello adlı taşınan tooa sıra {queuename} iletisidir-zararlı. Merhaba en fazla deneme sayısı yapılandırılabilir.
* iki hello `Blob` öznitelikler ilişkili tooblobs olan nesneler sağlar: bir toohello mevcut görüntü blob'u ve hello yöntemi oluşturan bir tooa yeni küçük resim blob.

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    BLOB adları gelen hello özelliklerinden `BlobInformation` nesne hello kuyruk iletisi aldı (`BlobName` ve `BlobNameWithoutExtension`). tooget hello tam işlevselliğini hello depolama istemci kitaplığı, kullanabileceğiniz hello `CloudBlockBlob` sınıfı toowork BLOB'lar ile. Toowork ile yazılmış tooreuse kodun isteyip istemediğinizi `Stream` nesneleri hello kullanabileceğiniz `Stream` sınıfı.

Nasıl toowrite, işlevleri hakkında daha fazla bilgi için Web işleri SDK'si öznitelikleri kullanmak, kaynakları aşağıdaki hello bakın:

* [Nasıl toouse Azure kuyruk depolama hello WebJobs SDK ile](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [Nasıl toouse Azure blob depolama hello WebJobs SDK ile](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [Nasıl toouse Azure tablo depolama hello WebJobs SDK ile](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [Web işleri SDK'si toouse Azure Service Bus ile nasıl hello](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * Web uygulamanız birden çok sanal makine çalışıyorsa, birden çok Web işleri eşzamanlı çalışan ve bazı senaryolarda bu hello aynı birden çok kez işlenen veri neden olabilir. Merhaba yerleşik sırası, blob ve Service Bus Tetikleyicileri kullanırsanız, bir sorun değildir. Merhaba SDK işlevlerinizi yalnızca bir kez her ileti veya blob işleneceğini sağlar.
> * Hakkında bilgi için tooimplement normal şekilde kapatılmasını bkz [kapama](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).
> * Merhaba hello kodda `ConvertImageToThumbnailJPG` yöntemi (gösterilmez) hello sınıfları kullanır `System.Drawing` kolaylık olması için ad alanı. Ancak, bu ad alanındaki hello sınıflar Windows Forms ile kullanılmak üzere tasarlanmıştır. Bir Windows veya ASP.NET hizmetinde kullanılması desteklenmez. Görüntü işleme seçenekleri hakkında daha fazla bilgi için bkz. [Dinamik Görüntü Oluşturma](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) ve [Görüntü Yeniden Boyutlandırmaya Ayrıntılı Bakış](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).
>
>

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, arka uç işleme için hello WebJobs SDK kullanan basit bir çok katmanlı uygulama gördünüz. Bu bölümde, ASP.NET çok katmanlı uygulamaları ve Web işleri hakkında daha fazla bilgi edinmek için bazı öneriler sunar.

### <a name="missing-features"></a>Eksik Özellikler
Merhaba uygulaması bir başlangıç öğreticisi için basit tutulmuştur. Gerçek dünya uygulamada uygulamak [bağımlılık ekleme](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) ve hello [depo ve iş birimi düzenleri](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), kullanın [günlüğe kaydetme için bir arabirimi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), kullanın[ EF Code First geçişleri](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage veri modeli değişikliklerini ve kullanmak [EF bağlantı dayanıklılığı](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage geçici ağ hataları.

### <a name="scaling-webjobs"></a>Web işleri ölçeklendirme
Web işleri hello bir web uygulaması bağlamında çalışır ve ayrı olarak ölçeklenebilir değildir. Örneğin, bir standart web app örneği varsa, çalışan, arka plan işlemi yalnızca bir örneğine sahip ve bazı kullanılabilir tooserve web içeriği Aksi durumda olacak hello sunucu kaynaklarının (CPU, bellek, vb.) kullanıyor.

Trafik gün veya haftanın günü zamanına göre değişir ve hello arka uç, işleme gerekiyorsa toodo bekleyebilir, Web işleri toorun trafiği düşük zamanlarda zamanlayabilirsiniz. Hello yük hala Bu çözüm için çok yüksekse, hello arka uç adanmış bir ayrı bir web uygulamasında Web işi olarak bu amaçla çalıştırabilirsiniz. Arka uç web uygulamanızı sonra bağımsız olarak ve ön uç web uygulamanızdan ölçeklendirebilirsiniz.

Daha fazla bilgi için bkz: [ölçeklendirme WebJobs](websites-webjobs-resources.md#scale).

### <a name="avoiding-web-app-timeout-shut-downs"></a>Web uygulaması zaman aşımı kapatma listeleri önleme
toomake emin Webjob'larınızı her zaman çalışıyor ve web uygulamasının tüm örneklerini çalıştıran, tooenable hello sahip [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) özelliği.

### <a name="using-hello-webjobs-sdk-outside-of-webjobs"></a>Merhaba WebJobs SDK Web işleri dışında kullanma
Bir Web işi olarak azure'da hello WebJobs SDK kullanan bir program toorun sahip değil. Yerel olarak çalıştırabilir ve bulut hizmeti çalışan rolü veya bir Windows hizmeti gibi diğer ortamlarda da çalıştırabilirsiniz. Ancak, hello Web işleri SDK'si Pano yalnızca Azure web uygulaması erişebilirsiniz. tooconnect hello web uygulama toohello depolama hesabı üzerinde hello hello AzureWebJobsDashboard bağlantı dizesi ayarlayarak kullanmakta olduğunuz sahip toouse hello Pano **yapılandırma** hello Klasik portal sekmesinde. Ardından, URL aşağıdaki hello kullanarak toohello Pano elde edebilirsiniz:

https://{webappname}.SCM.azurewebsites.NET/azurejobs/#/Functions

Daha fazla bilgi için bkz: [hello WebJobs SDK ile yerel geliştirme için bir Pano alma](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), ancak eski bir bağlantı dizesi adı gösterdiğine dikkat edin.

### <a name="more-webjobs-documentation"></a>Daha fazla Web işleri belgeleri
Daha fazla bilgi için bkz: [Azure Web işleri belge kaynakları](http://go.microsoft.com/fwlink/?LinkId=390226).
