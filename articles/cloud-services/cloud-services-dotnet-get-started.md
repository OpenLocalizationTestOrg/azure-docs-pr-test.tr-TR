---
title: "aaaGet başlatılan Azure Cloud Services ve ASP.NET ile | Microsoft Docs"
description: "Bilgi nasıl toocreate ASP.NET MVC ve Azure kullanarak çok katmanlı bir uygulama. web rolü ve çalışan rolü ile birlikte bir bulut hizmetinde Hello uygulama çalışır. Entity Framework, SQL Database ve Azure Storage kuyruklarını ve blob’larını kullanır."
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: adegeo
ms.openlocfilehash: 86271c29b79fad3f01f8ea0e88fd00c7aefc970c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a>Azure Cloud Services ve ASP.NET kullanmaya başlama

## <a name="overview"></a>Genel Bakış
Bu öğreticide gösterilmiştir nasıl toocreate ön uç, ASP.NET MVC ile çok katmanlı .NET uygulaması ve tooan dağıtma [Azure bulut hizmeti](cloud-services-choose-me.md). Merhaba uygulamanız tarafından kullanılan [Azure SQL veritabanı](http://msdn.microsoft.com/library/azure/ee336279), hello [Azure Blob hizmeti](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)ve hello [Azure Queue hizmeti](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern). Yapabilecekleriniz [hello Visual Studio projesi indirme](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) hello MSDN kod Galerisi'nden gelen.

Merhaba öğretici gösterir, nasıl yerel olarak toobuild ve Çalıştır Merhaba uygulaması nasıl toodeploy, tooAzure ve içinde çalışma hello Bulut ve nasıl toobuild, sıfırdan. Sıfırdan oluşturmaya başlatın ve sonra test hello ve dağıtım adımlarını gerçekleştirebilirsiniz olarak tercih ederseniz otomatik.

## <a name="contoso-ads-application"></a>Contoso Ads uygulaması
Merhaba uygulama bir reklam Bülteni panosudur. Kullanıcılar metin girerek ve görüntüyü karşıya yükleyerek bir reklam oluşturur. Küçük resim görüntüleriyle birlikte bir reklam listesi görebilir ve bir ad toosee hello ayrıntıları seçtiğinizde hello tam boyutlu görüntüyü görebilirsiniz.

![Reklam listesi](./media/cloud-services-dotnet-get-started/list.png)

Merhaba uygulamanın kullandığı hello [kuyruk merkezli çalışma deseni](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff yük hello CPU yoğunluklu iş tooa arka uç işleminde küçük resim oluşturma.

## <a name="alternative-architecture-websites-and-webjobs"></a>Alternatif mimari: Websites ve WebJobs
Bu öğretici nasıl toorun ön uç ve arka uç Azure içinde bulut gösterir hizmet. Ön uç içindeki toorun hello alternatiftir bir [Azure Web sitesi](/services/web-sites/) ve hello kullanın [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) hello arka uç (şu anda önizlemede) özelliği. WebJobs kullanan bir öğretici için bkz [hello Azure WebJobs SDK ile çalışmaya başlama](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md). Senaryonuz nasıl toochoose hello en iyi hizmetler hakkında bilgi sığması için bkz: [Azure Websites, Cloud Services ve sanal makineleri karşılaştırma](../app-service-web/choose-web-site-cloud-service-vm.md).

## <a name="what-youll-learn"></a>Öğrenecekleriniz
* Nasıl tooenable makinenize yükleyerek Azure geliştirme için Azure SDK'sı hello.
* Nasıl toocreate Visual Studio bulut hizmeti projesine bir ASP.NET MVC web rolü ve çalışan rolü ile.
* Nasıl tootest hello Azure storage öykünücüsü kullanarak bulut hizmeti projesini yerel olarak hello.
* Nasıl toopublish hello bulut proje tooan Azure bulut hizmeti ve bir Azure depolama hesabı kullanarak test edin.
* Nasıl tooupload dosyaları ve hello Azure Blob hizmetine depolama.
* Nasıl toouse katmanlar arasında iletişim için Azure Queue hizmetini hello.

## <a name="prerequisites"></a>Ön koşullar
Merhaba Öğreticisi, anladığınızı varsayar [Azure hakkında temel kavramları bulut hizmetlerini](cloud-services-choose-me.md) gibi *web rolü* ve *çalışan rolü* terminolojisi.  Ayrıca, bildiğinizi varsayar nasıl toowork ile [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) veya [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) Visual Studio projelerinde. Merhaba örnek uygulama MVC kullanır ancak çoğu hello öğreticinin tooWeb Forms de geçerlidir.

Merhaba uygulamayı bir Azure aboneliği olmadan yerel olarak çalıştırabilirsiniz, ancak bir toodeploy hello uygulama toohello bulut gerekir. Bir hesabınız yoksa, [MSDN abone avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) veya [ücretsiz deneme için kaydolabilirsiniz.](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668)

Merhaba öğretici yönergeleri aşağıdaki ürünler hello birini kullanarak çalışır:

* Visual Studio 2013
* Visual Studio 2015
* Visual Studio 2017

Bunlardan birine sahip değilseniz, hello Azure SDK'yı yüklediğinizde Visual Studio otomatik olarak yüklenebilir.

## <a name="application-architecture"></a>Uygulama mimarisi
Merhaba uygulama ads Entity Framework Code First toocreate hello tabloları ve erişim hello verilerini kullanarak bir SQL veritabanında depolar. Her ad için hello veritabanı depoları iki URL'ler, biri tam boyutlu görüntü ve diğeri hello küçük resim hello.

![Reklam tablosu](./media/cloud-services-dotnet-get-started/adtable.png)

Bir kullanıcı görüntü yüklediğinde hello ön uç web rolünde çalışan hello görüntüde depolayan bir [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), ve hello veritabanı toohello blob'u işaret eden bir URL ile Merhaba ad bilgilerini depolar. AT hello aynı zaman, ileti tooan Azure kuyruk yazar. Bir çalışan rolü düzenli aralıklarla çalışan bir arka uç işlemi hello sıra yeni iletiler için yoklar. Yeni bir ileti görüntülendiğinde, hello çalışan rolü bu görüntü için bir küçük resim oluşturur ve küçük resim URL'si veritabanı alanını bu reklam güncelleştirmeleri hello. Merhaba Aşağıdaki diyagramda nasıl hello uygulamanın hello bölümlerini etkileşim kurduğu gösterilmektedir.

![Contoso Ads mimarisi](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-hello-completed-solution"></a>İndirme ve çalıştırma hello çözüm tamamlandı
1. İndirip hello sıkıştırmasını [tamamlanan çözümü](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).
2. Visual Studio’yu çalıştırın.
3. Merhaba gelen **dosya** menüsünü seçin **Proje Aç**hello çözümü indirdiğiniz toowhere gidin ve ardından hello çözüm dosyasını açın.
4. CTRL + SHIFT + B toobuild hello çözüm tuşuna basın.

    Varsayılan olarak, Visual Studio hello dahil edilmeyen hello NuGet paket içeriği otomatik olarak yükler *.zip* dosyası. Merhaba paketler geri yüklenmezse varsa bunları el ile giderek toohello tarafından yükleyin **çözüm için NuGet paketlerini Yönet** iletişim kutusu ve hello tıklayarak **geri** düğmesine sağ hello üstünde.
5. İçinde **Çözüm Gezgini**, olduğundan emin olun **ContosoAdsCloudService** hello başlangıç projesi olarak seçilir.
6. Sonraki hello uygulamada hello SQL Server bağlantı dizesini değiştirin veya Visual Studio 2015 kullanıyorsanız *Web.config* hello ContosoAdsWeb projesinin ve hello dosyasının *ServiceConfiguration.Local.cscfg* hello ContosoAdsCloudService projesinin dosya. Her durumda, "(localdb) \v11.0" çok değiştirme "(localdb) \MSSQLLocalDB".
7. CTRL + F5 toorun Merhaba uygulaması tuşuna basın.

    Bir bulut hizmeti projesini yerel olarak çalıştırdığınızda, Visual Studio hello Azure otomatik olarak çağırır. *işlem öykünücüsü* ve Azure *depolama öykünücüsü*. bilgisayarınızın kaynaklarını toosimulate hello web rolü ve çalışan rolü ortamlarını Hello işlem öykünücüsü kullanır. Merhaba depolama öykünücüsü kullanan bir [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) veritabanı toosimulate Azure bulut depolama.

    Merhaba bir bulut hizmeti projesini ilk çalıştırdığınızda veya bunu dakika hello Öykünücüler toostart geçen. Öykünücü başlatma tamamlandığında hello varsayılan tarayıcı toohello uygulama giriş sayfası açılır.

    ![Contoso Ads mimarisi](./media/cloud-services-dotnet-get-started/home.png)
8. **Reklam Oluştur**'a tıklayın.
9. Bazı test verilerini girin ve bir *.jpg* görüntü tooupload ve ardından **oluşturma**.

    ![Sayfa oluşturma](./media/cloud-services-dotnet-get-started/create.png)

    Merhaba uygulama toohello dizin sayfasına gider, ancak işleme henüz tamamlanmadığından hello yeni ad için bir küçük resim göstermez.
10. Biraz bekleyin ve ardından hello dizin sayfası toosee hello küçük yenileyin.

     ![Dizin sayfası](./media/cloud-services-dotnet-get-started/list.png)
11. Tıklatın **ayrıntıları** ad toosee hello tam boyutlu görüntü için.

     ![Ayrıntılar sayfası](./media/cloud-services-dotnet-get-started/details.png)

Merhaba uygulaması tamamen, yerel bilgisayarınızda, bağlantı toohello bulutsuz çalışır durumda. Merhaba depolama öykünücüsü hello sıra depolar ve blob verilerini bir SQL Server Express LocalDB veritabanına ve Merhaba uygulaması hello ad verileri başka bir LocalDB veritabanına depolar. Entity Framework Code First otomatik olarak oluşturulan hello ad veritabanı hello hello web uygulaması tooaccess çalıştı ilk kez.

Bölümden hello hello bulutta çalışan kuyruklar, BLOB'lar ve hello uygulama veritabanı için hello çözüm toouse Azure bulut kaynakları yapılandıracaksınız. Yerel olarak toocontinue toorun istedi, ancak bulut depolama ve veritabanı kaynaklarını kullanan, yapabilirsiniz. Bunu göreceğiniz bağlantı dizelerini ayarlama yalnızca bir konudur nasıl toodo.

## <a name="deploy-hello-application-tooazure"></a>Merhaba uygulama tooAzure dağıtma
Siz gerçekleştirirsiniz adımları toorun hello hello bulut uygulamasında aşağıdaki hello:

* Bir Azure bulut hizmeti oluşturun.
* Bir Azure SQL veritabanı oluşturun.
* Bir Azure Storage hesabı oluşturun.
* Azure'da çalıştığında Azure SQL veritabanınızı hello çözüm toouse yapılandırın.
* Azure'da çalıştığında Azure storage hesabınızı hello çözüm toouse yapılandırın.
* Merhaba proje tooyour Azure bulut hizmeti dağıtın.

### <a name="create-an-azure-cloud-service"></a>Bir Azure bulut hizmeti oluşturma
Merhaba ortamı hello uygulamanın çalıştırılacağı bir Azure bulut hizmetidir.

1. Merhaba, tarayıcınızı açmak [Azure portal](https://portal.azure.com).
2. **Yeni > Hesapla > Bulut Hizmeti**’ne tıklayın.

3. Merhaba DNS adı giriş kutusuna hello bulut hizmeti için bir URL ön eki girin.

    Bu URL benzersiz toobe sahiptir.  Seçtiğiniz hello öneki zaten kullanılıyorsa bir hata iletisi alırsınız.
4. Merhaba hizmet için yeni bir kaynak grubu belirtin. Tıklatın **Yeni Oluştur** ve hello kaynak grubu giriş kutusunda CS_contososadsRG gibi bir ad yazın.

5. Merhaba bölge toodeploy Merhaba uygulaması istediğiniz yeri seçin.

    Bu alan, bulut hizmetinizin hangi veri merkezinde barındırılacağını belirtir. Bir üretim uygulaması için hello bölgeye en yakın tooyour müşteriler seçmeniz gerekir. Bu öğretici için hello bölgeye en yakın tooyou seçin.
5. **Oluştur**'a tıklayın.

    Görüntü aşağıdaki hello, bir bulut hizmeti ile Merhaba URL CSvccontosoads.cloudapp.net oluşturulur.

    ![Yeni Bulut Hizmeti](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a>Bir Azure SQL veritabanı oluşturma
Merhaba uygulama hello bulutta çalıştırıldığında bulut tabanlı bir veritabanı kullanır.

1. Merhaba, [Azure portal](https://portal.azure.com), tıklatın **yeni > veritabanları > SQL veritabanı**.
2. Merhaba, **veritabanı adı** kutusuna *contosoads*.
3. Merhaba, **kaynak grubu**, tıklatın **var olanı kullan** ve hello bulut hizmeti için kullanılan select hello kaynak grubu.
4. Görüntü, aşağıdaki Hello tıklatın **Server - gerekli ayarları Yapılandır** ve **yeni bir sunucu oluşturmak**.

    ![Tünel toodatabase sunucusu](./media/cloud-services-dotnet-get-started/newdb.png)

    Alternatif olarak, aboneliğiniz zaten bir sunucu varsa, bu sunucu hello aşağı açılan listeden seçebilirsiniz.
5. Merhaba, **sunucu adı** kutusuna *csvccontosodbserver*.

6. Bir yönetici için **Kullanıcı Adı** ve **Parola** girin.

    **Yeni sunucu oluştur**’u seçtiyseniz buraya mevcut bir adı ve parolayı girmezsiniz. Yeni bir ad ve parola hello veritabanına eriştiğinizde şimdi toouse daha sonra tanımladığınız girersiniz. Daha önce oluşturduğunuz bir sunucuyu seçtiyseniz önceden oluşturduğunuz hello parola toohello yönetici kullanıcı hesabı için istenir.
7. Seçin aynı hello **konumu** hello bulut hizmeti için seçtiğiniz.

    Merhaba bulut hizmeti ve veritabanı olduğunda farklı veri merkezlerinde (farklı bölgelerde) gecikme artar ve, hello veri merkezinin dışındaki bant genişliği için sizden ücret alınır. Bir veri merkezi içinde bant genişliği ücretsizdir.
8. Denetleme **izin azure Hizmetleri tooaccess sunucusu**.
9. Tıklatın **seçin** hello yeni sunucu için.

    ![Yeni SQL Veritabanı sunucusu](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. **Oluştur**'a tıklayın.

### <a name="create-an-azure-storage-account"></a>Azure Storage hesabı oluşturma
Bir Azure depolama hesabı, kuyruk ve blob verilerini hello bulutta depolamak için kaynaklar sağlar.

Gerçek bir uygulamada genellikle uygulama verilerine karşı günlük verileri için ve test verilerine karşı üretim verileri için ayrı hesaplar oluşturursunuz. Bu öğreticide yalnızca tek bir hesap kullanacaksınız.

1. Merhaba, [Azure portal](https://portal.azure.com), tıklatın **yeni > depolama > depolama hesabı - blob, dosya, tablo, kuyruk**.
2. Merhaba, **adı** kutusunda, bir URL ön eki girin.

    Merhaba kutunun altında gördüğünüz bu öneki ve hello metin hello benzersiz URL tooyour depolama hesabı olacaktır. Girdiğiniz hello öneki zaten başka bir kullanıcı tarafından kullanılıyorsa, farklı bir önek toochoose sahip olacaksınız.
3. Set hello **dağıtım modeli** çok*Klasik*.

4. Set hello **çoğaltma** aşağı açılan listesinde çok**yerel olarak yedekli depolama**.

    Bir depolama hesabı için coğrafi çoğaltma etkinleştirildiğinde, hello birincil konumda önemli bir olağanüstü durum oluşursa, depolanan hello çoğaltılmış tooa ikincil veri merkezine tooenable yük devretme içeriktir. Coğrafi çoğaltma ek ücretlere neden olabilir. Test ve geliştirme hesaplarında genellikle coğrafi çoğaltma için toopay istemezsiniz. Daha fazla bilgi için bkz. [Depolama hesabı oluşturma, yönetme veya silme](../storage/common/storage-create-storage-account.md).

5. Merhaba, **kaynak grubu**, tıklatın **var olanı kullan** ve hello bulut hizmeti için kullanılan select hello kaynak grubu.
6. Set hello **konumu** aşağı açılan liste toohello hello bulut hizmeti için seçtiğiniz aynı bölgede.

    Merhaba bulut hizmeti ve depolama hesabı farklı veri merkezlerinde olduğunda (farklı bölgelerde) gecikme artar ve, hello veri merkezinin dışındaki bant genişliği için sizden ücret alınır. Bir veri merkezi içinde bant genişliği ücretsizdir.

    Azure benzeşim grupları mekanizmasını toominimize hello uzaklığı gecikme süresini azaltmak bir veri merkezindeki kaynaklarına arasında sağlar. Bu öğretici benzeşim gruplarını kullanmaz. Daha fazla bilgi için bkz: [nasıl tooCreate benzeşim grubunda Azure'da](http://msdn.microsoft.com/library/jj156209.aspx).
7. **Oluştur**'a tıklayın.

    ![Yeni depolama hesabı](./media/cloud-services-dotnet-get-started/newstorage.png)

    Merhaba görüntüde hello URL ile bir depolama hesabı oluşturulur `csvccontosoads.core.windows.net`.

### <a name="configure-hello-solution-toouse-your-azure-sql-database-when-it-runs-in-azure"></a>Azure'da çalıştığında Azure SQL veritabanınızı hello çözüm toouse yapılandırın
Web projesi hello hello çalışan rolü projesi her kendi veritabanı bağlantı dizesi içeriyor ve hello uygulama Azure'da çalıştırıldığında her toopoint toohello Azure SQL veritabanı gerekir.

Kullanacağınız bir [Web.config dönüştürmesi](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) hello web rolü ve bir bulut hizmet ortamı ayarı hello çalışan rolü için.

> [!NOTE]
> Bu bölüm ve hello sonraki bölümde kimlik bilgilerini proje dosyalarına depolar. [Hassas verileri ortak kaynak kodu depolarına kaydetmeyin](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).
>
>

1. Merhaba ContosoAdsWeb projesinde hello açmak *Web.Release.config* Merhaba uygulaması dönüşüm dosyasını *Web.config* dosya, içeren hello açıklama bloğunu silin bir `<connectionStrings>` öğesi ve Yapıştır onun yerine koddan hello.

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    Merhaba dosyasını düzenlemek için açık bırakın.
2. Merhaba, [Azure portal](https://portal.azure.com), tıklatın **SQL veritabanları** hello sol bölmesinde, Bu öğretici için oluşturduğunuz hello veritabanı'nı tıklatın ve ardından **bağlantı dizelerini Göster**.

    ![Bağlantı dizelerini göster](./media/cloud-services-dotnet-get-started/showcs.png)

    Merhaba portal hello parola için bir yer tutucu bağlantı dizeleri görüntüler.

    ![Bağlantı dizeleri](./media/cloud-services-dotnet-get-started/connstrings.png)
3. Merhaba, *Web.Release.config* dönüşüm dosyasında, silme `{connectionstring}` ve onun yerine hello hello Azure portalındaki ADO.NET bağlantı dizesini yapıştırın.
4. Merhaba yapıştırdığınız bağlantı dizesinde hello *Web.Release.config* dönüşüm dosyasında, yerine `{your_password_here}` hello yeni SQL veritabanı için oluşturduğunuz hello parola ile.
5. Merhaba dosyasını kaydedin.  
6. Seçin ve aşağıdaki hello çalışan rolü projesi yapılandırma adımları hello kullanmak için (tırnak işaretleri çevreleyen hello) hello bağlantı dizesini kopyalayın.
7. İçinde **Çözüm Gezgini**altında **rolleri** hello bulut hizmeti projesini sağ **ContosoAdsWorker** ve ardından **özellikleri**.

    ![Rol özellikleri](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. Merhaba tıklatın **ayarları** sekmesi.
9. Değişiklik **hizmet yapılandırmasını** çok**bulut**.
10. Select hello **değeri** hello alanındaki `ContosoAdsDbConnectionString` ayarlama ve hello önceki bölümden hello öğreticinin kopyaladığınız hello bağlantı dizesini yapıştırın.

     ![Çalışan rolü için veritabanı bağlantı dizesi](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. Yaptığınız değişiklikleri kaydedin.  

### <a name="configure-hello-solution-toouse-your-azure-storage-account-when-it-runs-in-azure"></a>Azure içinde çalıştığında Azure storage hesabınızı hello çözüm toouse yapılandırın
Azure depolama hesabı bağlantı dizeleri hello web rolü projesinin hem hello çalışan rolü projesi hello bulut hizmeti projesindeki ortam ayarlarına depolanır. Her proje için hello bulutta çalıştığında ve hello uygulama yerel olarak çalıştığında kullanılan ayarları toobe ayrı bir dizi yoktur. Web ve çalışan rolü projeleri için hello bulut ortamı ayarlarını güncelleştirin.

1. İçinde **Çözüm Gezgini**, sağ **ContosoAdsWeb** altında **rolleri** hello içinde **ContosoAdsCloudService** proje ve ardından **Özellikleri**.

    ![Rol özellikleri](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. Merhaba tıklatın **ayarları** sekmesi. Merhaba, **hizmet yapılandırmasını** açılır kutusunda, seçin **bulut**.

    ![Bulut yapılandırması](./media/cloud-services-dotnet-get-started/sccloud.png)
3. Select hello **StorageConnectionString** girişi ve üç nokta göreceksiniz (**...** ) düğmesini hello sağ ucunda hello satır. Merhaba üç nokta düğmesini tooopen hello tıklatın **depolama hesabı bağlantı dizesi oluştur** iletişim kutusu.

    ![Bağlantı Dizesi Oluştur kutusunu açma](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. Merhaba, **depolama bağlantı dizesi oluştur** iletişim kutusu, tıklatın **aboneliğinizi**, daha önce oluşturduğunuz hello depolama hesabını seçin ve ardından **Tamam**. Henüz oturum açmadıysanız Azure hesabı kimlik bilgileriniz istenir.

    ![Depolama Bağlantı Dizesi oluşturma](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. Yaptığınız değişiklikleri kaydedin.
6. İzleme hello aynı hello için kullandığınız yordam `StorageConnectionString` bağlantı dizesi tooset hello `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` bağlantı dizesi.

    Bu bağlantı dizesi günlüğe kaydetme için kullanılır.
7. İzleme hello aynı hello için kullandığınız yordam **ContosoAdsWeb** rol tooset Merhaba için iki bağlantı dizesini **ContosoAdsWorker** rol. Tooset unutmayın **hizmet yapılandırmasını** çok**bulut**.

hello hello Visual Studio kullanıcı arabirimini kullanılarak yapılandırdığınız rol ortamı ayarları aşağıdaki dosyaları hello ContosoAdsCloudService projesinde hello depolanır:

* *ServiceDefinition.csdef* -hello ayar adlarını tanımlar.
* *ServiceConfiguration.Cloud.cscfg* -hello uygulama hello bulutta çalıştığında için değerler sağlar.
* *ServiceConfiguration.Local.cscfg* -hello uygulama yerel olarak çalıştığında için değerler sağlar.

Örneğin, hello ServiceDefinition.csdef aşağıdaki tanımları hello içerir:

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

Ve hello *ServiceConfiguration.Cloud.cscfg* dosyası, Visual Studio'da bu ayarlar için girdiğiniz hello değerleri içerir.

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

Merhaba `<Instances>` ayar Azure hello çalışan rolü kodunu çalıştıracağı sanal makine hello sayısını belirtir. Merhaba [sonraki adımlar](#next-steps) bölümünde bir bulut hizmetinin ölçeklendirme hakkında bağlantılar toomore bilgileri içerir

### <a name="deploy-hello-project-tooazure"></a>Merhaba proje tooAzure dağıtma
1. İçinde **Çözüm Gezgini**, sağ hello **ContosoAdsCloudService** bulut projesine ve ardından **Yayımla**.

   ![Yayımla menüsü](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. Merhaba, **oturum** hello adımında **Azure uygulamasını Yayımla** Sihirbazı'nı tıklatın **sonraki**.

    ![Oturum açma adımı](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. Merhaba, **ayarları** adım hello Sihirbazı'nın tıklatın **sonraki**.

    ![Ayarlar adımı](./media/cloud-services-dotnet-get-started/pubsettings.png)

    Merhaba hello varsayılan ayarlarında **Gelişmiş** sekmesinde Bu öğretici için uygundur. Merhaba Gelişmiş sekmesi hakkında daha fazla bilgi için bkz: [Azure uygulaması Yayımlama Sihirbazı](http://msdn.microsoft.com/library/hh535756.aspx).
4. Merhaba, **Özet** adımını, **Yayımla**.

    ![Özet adımı](./media/cloud-services-dotnet-get-started/pubsummary.png)

   Merhaba **Azure etkinlik günlüğü** Visual Studio'da penceresi açılır.
5. Merhaba sağ ok simgesine tooexpand hello dağıtım Ayrıntılar'ı tıklatın.

    Merhaba dağıtım too5 dakika veya daha fazla toocomplete alabilir.

    ![Azure Etkinlik Günlüğü penceresi](./media/cloud-services-dotnet-get-started/waal.png)
6. Merhaba dağıtım durumu tamamlandığında hello tıklatın **Web uygulaması URL'si** toostart Merhaba uygulaması.
7. Merhaba uygulamayı yerel olarak çalıştırdığınızda yaptığınız gibi hello uygulama oluşturma, görüntüleme ve bazı ads düzenleme artık test edebilirsiniz.

> [!NOTE]
> Ne zaman sınama, silmek veya Dur hello bulut hizmeti bitti. Merhaba bulut hizmeti kullanmıyorsanız bile, sanal makine kaynakları için ayrılmış olduğundan ücretler tahakkuk eder. Ayrıca çalışır durumda bırakırsanız, URL’nizi bulan herhangi bir kişi reklam oluşturabilir ve görüntüleyebilir. Merhaba, [Azure portal](https://portal.azure.com), Git toohello **genel bakış** bulut hizmetiniz için sekmesini ve sonra hello **silmek** hello sayfanın üst kısmındaki hello düğmesi. Yalnızca istiyorsanız tootemporarily önlemek başkalarının hello siteye erişmesini, tıklatın **durdurmak** yerine. Bu durumda ücretler tooaccrue devam eder. Artık gereksinim duyduğunuzda, benzer bir yordamı toodelete hello SQL veritabanı ve depolama hesabı izleyebilirsiniz.
>
>

## <a name="create-hello-application-from-scratch"></a>Merhaba uygulamayı sıfırdan oluşturma
Zaten indirmediyseniz [tamamlandı Merhaba uygulaması](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), bunu şimdi yapın. Dosyaları hello indirilen projeden hello yeni projeye kopyalayın.

Merhaba Contoso Ads uygulamasının oluşturulması hello aşağıdaki adımları içerir:

* Bir bulut hizmeti Visual Studio çözümü oluşturun.
* NuGet paketlerini güncelleştirin ve ekleyin.
* Proje başvurularını ayarlayın.
* Bağlantı dizelerini yapılandırın.
* Kod dosyaları ekleyin.

Merhaba çözüm oluşturulduktan sonra benzersiz toocloud hizmeti projeleri ve Azure BLOB'ları ve kuyrukları hello kodu gözden geçirin.

### <a name="create-a-cloud-service-visual-studio-solution"></a>Bir bulut hizmeti Visual Studio çözümü oluşturma
1. Visual Studio'da, **yeni proje** hello gelen **dosya** menüsü.
2. Hello sol bölmesinde hello **yeni proje** iletişim kutusunda, genişletin **Visual C#** ve seçin **bulut** şablonları ve ardından hello **Azure bulut hizmeti** şablonu.
3. Merhaba projeyi ve çözümü ContosoAdsCloudService olarak adlandırın ve ardından **Tamam**.

    ![Yeni Proje](./media/cloud-services-dotnet-get-started/newproject.png)
4. Merhaba, **yeni Azure bulut hizmeti** iletişim kutusunda, web rolü ve çalışan rolü ekleyin. Merhaba web rolünü ContosoAdsWeb ve hello çalışan rolünü ContosoAdsWorker olarak adlandırın. (Merhaba kalem simgesine hello sağ bölmedeki toochange hello varsayılan adlarında hello rollerin kullanın.)

    ![Yeni Bulut Hizmeti Projesi](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. Merhaba gördüğünüzde **yeni ASP.NET projesi** hello web rolü için iletişim kutusu hello MVC şablonunu seçin ve ardından **kimlik doğrulamayı Değiştir**.

    ![Kimlik Doğrulamayı Değiştirme](./media/cloud-services-dotnet-get-started/chgauth.png)
6. Merhaba, **kimlik doğrulamayı Değiştir** iletişim kutusunda, seçin **doğrulaması yok**ve ardından **Tamam**.

    ![Kimlik Doğrulaması Yok](./media/cloud-services-dotnet-get-started/noauth.png)
7. Merhaba, **yeni ASP.NET projesi** iletişim kutusunda, tıklatın **Tamam**.
8. İçinde **Çözüm Gezgini**hello çözümü (değil hello projelerden biri) sağ tıklatın ve seçin **Ekle - yeni proje**.
9. Merhaba, **Yeni Proje Ekle** iletişim kutusunda, seçin **Windows** altında **Visual C#** hello sol bölmesinde ve hello ardından **sınıf kitaplığı** Şablon.  
10. Ad hello proje *ContosoAdsCommon*ve ardından **Tamam**.

    Tooreference hello Entity Framework bağlamını ve hello veri modeli web ve çalışan rolü projelerindeki gerekir. Alternatif olarak, hello web rolü projesinde EF ile ilgili sınıflar hello tanımlayın ve hello çalışan rolü projesinde bu projeye başvuruda. Ancak hello alternatif yaklaşımda çalışan rolü projeniz gerekli olmayan bir başvuru tooweb derlemeleri gerekir.

### <a name="update-and-add-nuget-packages"></a>NuGet paketlerini güncelleştirme ve ekleme
1. Açık hello **NuGet paketlerini Yönet** hello çözüm için iletişim kutusu.
2. Merhaba penceresinin Hello üstünde seçin **güncelleştirmeleri**.
3. Merhaba Ara *WindowsAzure.Storage* paketini ve hello listesinde olması durumunda onu seçip hello web ve çalışan projelerini tooupdate içinde ve ardından **güncelleştirme**.

    Merhaba sürümünün güncelleştirilmiş yeni oluşturulan proje gereksinimlerini toobe içinde sık sık görürsünüz hello depolama istemcisi Kitaplığı Visual Studio proje şablonlarından daha sık güncelleştirilir.
4. Merhaba penceresinin Hello üstünde seçin **Gözat**.
5. Hello bulur *EntityFramework* NuGet paketini bulun ve üç projenin tamamına yükleyin.
6. Hello bulur *Microsoft.WindowsAzure.ConfigurationManager* NuGet paketini ve hello çalışan rolü projesine yükleyin.

### <a name="set-project-references"></a>Proje başvurularını ayarlama
1. Merhaba ContosoAdsWeb projesinde bir başvuru toohello ContosoAdsCommon projesine ayarlayın. Merhaba ContosoAdsWeb projesine sağ tıklayın ve ardından **başvuruları** - **Başvuru Ekle**. Merhaba, **başvuru Yöneticisi** iletişim kutusunda **çözüm – projeler** hello sol bölmesinde seçin **ContosoAdsCommon**ve ardından **Tamam**.
2. Merhaba ContosoAdsWorker projesinde bir başvuru toohello Contosoadscommon projesine ayarlayın.

    ContosoAdsCommon hem hello ön uç ve arka uç tarafından kullanılacak olan hello Entity Framework veri modeli ve bağlam sınıfını içerir.
3. Merhaba ContosoAdsWorker projesinde bir başvuru çok ayarlayın`System.Drawing`.

    Bu derleme hello arka uç tooconvert görüntüleri toothumbnails tarafından kullanılır.

### <a name="configure-connection-strings"></a>Bağlantı dizelerini yapılandırma
Bu bölümde, yerel olarak test etmek amacıyla Azure Storage ve SQL bağlantı dizelerini yapılandırırsınız. Başlangıç Öğreticisi dağıtım yönergeleri Hello hello uygulama hello bulutta çalıştığında nasıl tooset hello bağlantı kurmak için dizeleri açıklanmaktadır.

1. Merhaba ContosoAdsWeb projesine, açık hello uygulamanın Web.config dosyasını ve INSERT hello aşağıdaki `connectionStrings` öğeden sonra hello `configSections` öğesi.

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    Visual Studio 2015 ve sonraki bir sürümü kullanıyorsanız "v11.0" ifadesini "MSSQLLocalDB" ile değiştirin.
2. Yaptığınız değişiklikleri kaydedin.
3. Merhaba ContosoAdsCloudService projesinde altındaki ContosoAdsWeb sağ **rolleri**ve ardından **özellikleri**.

    ![Rol özellikleri](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. Merhaba, **ContosAdsWeb [rolü]** Özellikleri penceresinde hello tıklatın **ayarları** sekmesini ve ardından **ayar Ekle**.

    Bırakın **hizmet yapılandırmasını** çok ayarlamak**tüm yapılandırmaları**.
5. *StorageConnectionString* adlı bir ayar ekleyin. Ayarlama **türü** çok*ConnectionString*ve **değeri** çok*UseDevelopmentStorage = true*.

    ![Yeni bağlantı dizesi](./media/cloud-services-dotnet-get-started/scall.png)
6. Yaptığınız değişiklikleri kaydedin.
7. Merhaba ContosoAdsWorker rol özelliklerine bir depolama bağlantı dizesi aynı yordamı tooadd hello izleyin.
8. Merhaba yine de **ContosoAdsWorker [rolü]** Özellikleri penceresinde, başka bir bağlantı dizesi ekleyin:

   * Ad: ContosoAdsDbConnectionString
   * Türü: Dize
   * Değer: Yapıştır hello aynı hello web rolü projesi için kullanılan bağlantı dizesi. (aşağıdaki örneğine hello için Visual Studio 2013 içindir. Veri kaynağı toochange hello Bu örneği kopyalarsanız ve Visual Studio 2015 veya üzeri kullanıyorsanız unutmayın.)

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a>Kod dosyaları ekleme
Bu bölümde, kod dosyaları hello yeni çözüme hello indirilen çözümden kopyalayın. Merhaba aşağıdaki bölümlerde gösterilmiş ve bu kodun temel kısımları açıklanmaktadır.

tooadd dosyalar tooa proje veya bir klasörü, sağ hello proje veya klasöre tıklatın **Ekle** - **varolan öğeyi**. İstediğiniz ve ardından hello dosyaları seçin **Ekle**. Tooreplace var olan dosyaları isteyip istemediğinizi sorulursa tıklatın **Evet**.

1. Merhaba ContosoAdsCommon projesinde hello silmek *Class1.cs* dosya ve onun yerine hello ekleyin *Ad.cs* ve *ContosoAdscontext.cs* hello dosyalarından proje indirilir.
2. Merhaba ContosoAdsWeb projesinde hello hello indirilen projeden aşağıdaki dosyaları ekleyin.

   * *Global.asax.cs*.  
   * Merhaba, *görünümler/paylaşılan* klasörü:  *\_Layout.cshtml*.
   * Merhaba, *görünümler* klasörü: *Index.cshtml*.
   * Merhaba, *denetleyicileri* klasörü: *AdController.cs*.
   * Merhaba, *görünümler/reklam* klasörü (öncelikle hello klasörü oluşturun): beş *.cshtml* dosyaları.
3. Merhaba ContosoAdsWorker projesinde ekleyin *WorkerRole.cs* proje hello indirilir.

Artık derleme ve hello öğreticide daha önce belirtildiği gibi hello uygulamayı çalıştırın ve hello uygulama yerel veritabanı ve depolama öykünücüsü kaynaklarını kullanır.

Merhaba aşağıdaki bölümlerde açıklanmıştır hello kodu ile ilgili tooworking hello Azure ortamı, BLOB'ları ve kuyrukları. Bu öğretici değil açıklayan nasıl toocreate MVC denetleyicileri yapı iskelesi kullanarak görünümleri nasıl toowrite Entity Framework kod çalışır SQL Server veritabanları veya ASP.NET 4.5 içinde zaman uyumsuz programlama temelleri hello. Bu konular hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [MVC 5 kullanmaya başlama](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [EF 6 ve MVC 5 kullanmaya başlama](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* [Giriş tooasynchronous .NET 4.5 programlamada](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
Merhaba Ad.cs dosyası reklam kategorileri için bir numaralandırma ve reklam bilgileri için bir POCO varlık sınıfı tanımlar.

```csharp
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
```

### <a name="contosoadscommon---contosoadscontextcs"></a>ContosoAdsCommon - ContosoAdsContext.cs
Merhaba ContosoAdsContext sınıfı hello reklam sınıfının Entity Framework bir SQL veritabanına depolanacak bir DbSet koleksiyonunda kullanıldığını belirtir.

```csharp
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
```

Merhaba sınıfın iki Oluşturucusu vardır. ilk hello bunları hello web projesi tarafından kullanılır ve hello hello Web.config dosyasında saklanan bir bağlantı dizesinin adını belirtir. Merhaba ikinci oluşturucu bir Web.config dosyası olmadığından hello çalışan rolü projesi tarafından kullanılan hello gerçek bağlantı dizesine toopass sağlar. Daha önce gördüğünüzle burada Bu bağlantı dizesi depolanır ve daha sonra nasıl hello DbContext sınıfını başlattığında hello kodu hello bağlantı dizesini alır görürsünüz.

### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb - Global.asax.cs
Hello adlı kod `Application_Start` yöntemi oluşturur bir *görüntüleri* blob kapsayıcısı ve bir *görüntüleri* henüz yoksa sıra. Bu, yeni bir depolama hesabı kullanmaya başlamak ya da hello depolama öykünücüsünü yeni bir bilgisayarda kullanmaya başladığınız her hello gerekli blob kapsayıcısının ve kuyruğun otomatik olarak oluşturulmasını sağlar.

Merhaba kod alır erişim toohello depolama hesabı hello hello depolama bağlantı dizesini kullanarak *.cscfg* dosya.

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

Bir başvuru toohello alır sonra *görüntüleri* blob kapsayıcısı, önceden var olmayan ve erişim izinlerini hello yeni kapsayıcı ayarlar hello kapsayıcı oluşturur. Varsayılan olarak, yeni kapsayıcılar yalnızca depolama hesabı istemcileriyle kimlik bilgilerini tooaccess BLOB'lar izin verir. Bu nokta toohello görüntü BLOB'larını URL'leri kullanarak görüntüleri gösterebilmek hello Web sitesi BLOB'lar toobe ortak hello.

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

Benzer bir kod alır başvuru toohello *görüntüleri* sıraya almak ve yeni bir sıra oluşturur. Bu durumda hiçbir izin değişikliğine gerek yoktur.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb - \_Layout.cshtml
Merhaba *_Layout.cshtml* dosya hello üstbilgi ve altbilgi hello uygulama adını ayarlar ve bir "Reklamlar" menü girişi oluşturur.

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Görünümler\Giriş\Dizin.cshtml
Merhaba *Views\Home\Index.cshtml* dosya hello giriş sayfasında kategori bağlantılarını gösterir. Merhaba bağlantılar geçirmek hello hello tamsayı değeri `Category` enum bir sorgu dizesi değişkeni toohello reklam dizini sayfasına içindeki.

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
Merhaba, *AdController.cs* dosya, hello Oluşturucusu çağrıları hello `InitializeStorage` BLOB'lar ve kuyruklarla çalışmaya yönelik bir API sağlayan yöntemi toocreate Azure Storage istemci Kitaplığı nesneleri.

Bir başvuru toohello Hello kodu alır sonra *görüntüleri* daha önce gördüğünüz gibi blob kapsayıcısı *Global.asax.cs*. Bunu yaparken bir web uygulaması için uygun bir varsayılan [yeniden deneme ilkesi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) ayarlar. Merhaba varsayılan üstel geri alma yeniden deneme ilkesi hello web uygulaması için geçici bir hata için tekrarlanan yeniden denemelerde bir dakikadan uzun süre askıya alabilir. Burada belirtilen hello yeniden deneme ilkesi üç her denemeden sonra toothree çalıştığında saniye bekler.

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

Benzer bir kod alır başvuru toohello *görüntüleri* sırası.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

Merhaba denetleyici kodlarının birçoğu bir DbContext sınıfı kullanarak bir Entity Framework veri modeli ile çalışmak için tipiktir. Merhaba HttpPost bir istisnadır `Create` yöntemi, bir dosya yükler ve blob depolama alanına kaydeder. Merhaba model bağlayıcı sağlar bir [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) nesne toohello yöntemi.

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

Merhaba kullanıcı dosya tooupload seçtiyseniz, hello kod hello dosyayı yükler, bir blob'a kaydeder ve hello Ad veritabanı kaydını toohello blob'u işaret eden bir URL ile güncelleştirir.

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

Merhaba, karşıya yükleme hello hello koddur `UploadAndSaveBlobAsync` yöntemi. Merhaba blob, yüklemeleri ve kaydeder hello dosyası için bir GUID adı oluşturur ve bir başvuru toohello kaydedilmiş blob döndürür.

```csharp
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
```

Merhaba HttpPost sonra `Create` yöntemi bir blob'u karşıya yüklemeleri ve güncelleştirmeleri Merhaba veritabanı, bir kuyruk iletisi tooinform görüntü için dönüştürme tooa küçük resim hazır olduğunu, arka uç işlemi oluşturur.

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

Merhaba hello HttpPost kodunu `Edit` yöntemi, hello kullanıcı yeni bir görüntü dosyası seçtiği durumlarda zaten mevcut BLOB silinmelidir dışında benzer.

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

Merhaba sonraki örnek bir ad sildiğinizde, BLOB'ları siler hello kodu gösterir.

```csharp
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
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a>ContosoAdsWeb - Views\Ad\Index.cshtml ve Details.cshtml
Merhaba *Index.cshtml* dosyası küçük resimleri hello ile diğer ad verileri görüntüler.

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

Merhaba *Details.cshtml* dosyası hello tam boyutlu görüntüyü gösterir.

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml ve Edit.cshtml
Merhaba *Create.cshtml* ve *Edit.cshtml* dosyaları belirtin etkinleştirir denetleyicisi tooget hello hello kodlama form `HttpPostedFileBase` nesnesi.

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

Bir `<input>` öğesi, bir dosya seçme iletişim kutusu hello tarayıcı tooprovide söyler.

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a>ContosoAdsWorker - WorkerRole.cs - OnStart yöntemi
Hello Azure çalışan rolü ortamı çağırır hello `OnStart` hello yönteminde `WorkerRole` sınıf hello çalışan rolü Başlarken ve hello çağırır `Run` yöntemi hello zaman `OnStart` yöntemini çağırır.

Merhaba `OnStart` yöntemi alır hello veritabanı bağlantı dizesi hello *.cscfg* dosya ve toohello Entity Framework DbContext sınıfına geçirir. Merhaba sağlayıcı belirtilen toobe içermiyor biçimde hello SQLClient sağlayıcısı varsayılan olarak kullanılır.

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

Bundan sonra hello yöntemi bir başvuru toohello depolama hesabı alır ve yoksa hello blob kapsayıcısı ve kuyruk oluşturur. Merhaba, kodudur zaten gördüğünüz hello web rolünde benzer toowhat `Application_Start` yöntemi.

### <a name="contosoadsworker---workerrolecs---run-method"></a>ContosoAdsWorker - WorkerRole.cs - Run yöntemi
Merhaba `Run` yöntemi çağrılır hello `OnStart` yöntemi başlatma işini tamamladığında. Merhaba yöntemi yeni bir kuyruk iletisi izleyen ve bunlar ulaşan iletileri işleyen sonsuz bir döngü yürütür.

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

Hello döngü her yinelemeden sonra herhangi bir kuyruk iletisi bulunmazsa için ikinci bir hello program uyku moduna geçer. Bu, hello çalışan rolü aşırı CPU süresi ve depolama işlem maliyetleri doğurmasını engeller. Merhaba Microsoft Müşteri danışma ekibi tooproduction dağıtılan ve tatile ekleyip hikayeyi kimin tooinclude bunu unuttunuz bir geliştiricinin hikayesini anlatır. Kendisine geri alındı, birden çok hello tatil döndüğünde gözetim maliyeti.

Bazen bir kuyruk iletisi Merhaba içeriğine işlenirken bir hata neden olur. Bu adlı bir *zehir iletisi*, ve yalnızca bir hatayı günlüğe kaydedip hello döngüyü yeniden, bu iletiyi tooprocess sonsuz çalışabilir.  Bu nedenle bir if hello catch bloğu içerir toosee denetler deyimi hello uygulama tooprocess çalıştı kaç kez hello geçerli iletiyi ve 5 defadan fazla olması durumunda, selamlama iletisine hello sıradan silinir.

Bir kuyruk iletisi bulunduğunda `ProcessQueueMessage` çağrılır.

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

Bu kod hello veritabanı tooget hello resim URL'si okur, hello görüntü tooa küçük dönüştürür, hello küçük resmi bir blob'a kaydeder, hello veritabanı hello küçük resim blob URL'si ile güncelleştirir ve hello kuyruk iletisini siler.

> [!NOTE]
> Merhaba hello kodda `ConvertImageToThumbnailJPG` yöntemi kolaylık sağlaması açısından hello System.Drawing ad alanındaki sınıfları kullanır. Ancak, bu ad alanındaki hello sınıflar Windows Forms ile kullanılmak üzere tasarlanmıştır. Bir Windows veya ASP.NET hizmetinde kullanılması desteklenmez. Görüntü işleme seçenekleri hakkında daha fazla bilgi için bkz. [Dinamik Görüntü Oluşturma](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) ve [Görüntü Yeniden Boyutlandırmaya Ayrıntılı Bakış](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).
>
>

## <a name="troubleshooting"></a>Sorun giderme
Bu öğreticide hello yönergeleri izleyerek sırasında sorun oluşması durumunda bazı yaygın hatalar şunlardır ve nasıl tooresolve bunları.

### <a name="serviceruntimeroleenvironmentexception"></a>ServiceRuntime.RoleEnvironmentException
Merhaba `RoleEnvironment` nesnesi, bir uygulamayı Azure'da çalıştırdığınızda ya da hello Azure işlem öykünücüsü kullanarak yerel olarak çalıştırdığınızda Azure tarafından sağlanır.  Yerel olarak çalıştırırken bu hatayı alırsanız, hello ContosoAdsCloudService projesinde hello başlangıç projesi olarak ayarladığınızdan emin olun. Hello Azure işlem öykünücüsü kullanarak hello proje toorun ayarlar.

Merhaba uygulamanız tarafından kullanılan Azure RoleEnvironment hello hello şeyler biri hello depolanan tooget hello bağlantı dizesi değerleri *.cscfg* dosyaları, bu özel durumun başka bir nedeni eksik bir bağlantı dizesi gelir. Merhaba ContosoAdsWeb projesinde hem bulut için hello StorageConnectionString ayarını hem de yerel yapılandırmaları oluşturulur ve hello ContosoAdsWorker projesinde her iki yapılandırma için iki bağlantı dizesini oluşturulan emin olun. Bunu yaparsanız bir **Tümünü Bul** arama StorageConnectionString için çözümün tamamında Merhaba, onu 9 kez 6 dosyada görmeniz gerekir.

### <a name="cannot-override-tooport-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a>Tooport xxx geçersiz kılamaz. Yeni bağlantı noktası http protokolü için izin verilen en düşük 8080 değerinin altında
Merhaba web projesi tarafından kullanılan başlangıç bağlantı noktası numarasını değiştirmeyi deneyin. Merhaba ContosoAdsWeb projesine sağ tıklayın ve ardından **özellikleri**. Merhaba tıklatın **Web** sekmesini ve ardından hello hello bağlantı noktası numarasını değiştirin **proje URL'sini** ayarı.

Merhaba sorunu çözebilecek başka bir alternatif için bölümden hello bakın.

### <a name="other-errors-when-running-locally"></a>Yerel olarak çalışırken oluşan diğer hatalar
Varsayılan olarak yeni bulut hizmeti projeleri hello Azure işlem öykünücüsü express toosimulate hello Azure ortamı kullanın. Bu bir hello tam işlem öykünücüsünün hafif sürümüdür ve hello hızlı sürümün çalışmadığı bazı koşullar hello altında tam öykünücü çalışır.  

toochange proje toouse hello tam öykünücü Merhaba, hello ContosoAdsCloudService projesine sağ tıklayın ve ardından **özellikleri**. Merhaba, **özellikleri** penceresinde hello tıklatın **Web** sekmesini ve sonra hello **tam öykünücü kullan** radyo düğmesi.

Sipariş toorun hello uygulamada hello tam öykünücü ile yönetici ayrıcalıklarıyla Visual Studio tooopen sahip.

## <a name="next-steps"></a>Sonraki adımlar
Contoso Ads uygulaması Hello kasıtlı olarak bir başlangıç öğreticisi için basit tutulmuştur. Örneğin, uygulamaz [bağımlılık ekleme](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) veya hello [depo ve iş birimi düzenleri](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), yoktur [bir arabirim için günlük kaydını kullanmak](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), kullanmaz[ EF Code First geçişleri](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage veri modeli değişikliklerini veya [EF bağlantı dayanıklılığı](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage geçici ağ hataları ve benzeri.

En az karmaşık toomore karmaşık listelenen daha fazla gerçek kodlama uygulamalarını gösteren bazı bulut hizmeti örnek uygulamaları şunlardır:

* [PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31). Kavram benzer tooContoso Ads ancak daha fazla özellik ve daha fazla gerçek kodlama uygulamalarını uygular.
* [Tablolar, Kuyruklar ve Blob’lar ile Azure Cloud Service Çok Katmanlı Uygulaması](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36). Azure Storage tablolarının yanı sıra blob’ları ve kuyrukları tanıtır. .NET için Azure SDK'sı hello daha eski bir sürümü bağlı olarak, bazı değişiklikler toowork hello geçerli sürümle gerektirir.
* [Microsoft Azure’da Bulut Hizmeti Temel Bilgileri](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Çok çeşitli hello Microsoft Patterns and Practices grubu tarafından oluşturulan en iyi yöntemleri gösteren kapsamlı bir örnektir.

Merhaba bulut için geliştirme hakkında genel bilgi için bkz: [yapı Azure ile gerçek bulut uygulamaları](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).

Video girişi tooAzure depolama için en iyi yöntemler ve desenler için bkz: [Microsoft Azure Storage – yeni, en iyi yöntemler ve yaklaşımlar nedir](http://channel9.msdn.com/Events/Build/2014/3-628).

Daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [Azure Cloud Services Bölüm 1: Giriş](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [Toomanage Cloud Services nasıl](cloud-services-how-to-manage.md)
* [Azure Depolama](/documentation/services/storage/)
* [Nasıl toochoose bir bulut hizmet sağlayıcısı](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
