---
title: "Azure App Service'te bir .NET WebJob oluşturma | Microsoft Docs"
description: "ASP.NET MVC ve Azure kullanarak çok katmanlı bir uygulama oluşturun. Bir web uygulamasını Azure App Service ve arka uç çalıştırır ön uç Web işi çalıştırır. Uygulama Entity Framework, SQL Database ve Azure depolama kuyrukları ve blobları kullanır."
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
ms.openlocfilehash: a20b13058caecff75af14957468f20e63a3325c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a>Azure Uygulama Hizmeti’nde .NET WebJob oluşturma
Bu öğretici kullanan basit bir çok katmanlı ASP.NET MVC 5 uygulama kodunun nasıl yazılacağını gösterir [WebJobs SDK](websites-dotnet-webjobs-sdk.md).

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Amacı [WebJobs SDK](websites-webjobs-resources.md) bir Web işi gerçekleştirebilirsiniz, görüntü işleme, sıra işleme, RSS toplama, dosya bakımı gibi ortak görevler için yazdığınız kodları kolaylaştırmaktır ve e-postaları gönderme. Web işleri SDK'si, Azure Storage ve Service Bus ile çalışmak için görev zamanlama ve hataları işleme ve diğer birçok yaygın senaryolar için yerleşik özellikler vardır. Ayrıca, Genişletilebilir olmak için tasarlanmıştır ve var. bir [uzantıları için açık kaynak deposu](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

Örnek uygulama bir reklam Bülteni panosudur. Kullanıcılar yansımaları reklamları için karşıya yükleyebilir ve bir arka uç işlem görüntüleri küçük resimlere dönüştürür. Ad listesi sayfası küçük resimleri gösterir ve ad Ayrıntılar sayfası tam boyutlu görüntüyü gösterir. Bir ekran görüntüsü aşağıda verilmiştir:

![Reklam listesi](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

Bu örnek uygulama ile çalışır [Azure kuyrukları](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) ve [Azure BLOB'ları](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage). Öğretici, uygulamayı dağıtmak gösterilmiştir [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) ve [Azure SQL veritabanı](http://msdn.microsoft.com/library/azure/ee336279).

## <a id="prerequisites"></a>Önkoşullar
Öğretici ile nasıl çalışılacağını bildiğinizi varsayar [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) Visual Studio projelerinde.

Öğreticinin ilk olarak Visual Studio 2013 için yazılmıştır, ancak Visual Studio'nun daha yeni sürümlerinde kullanılabilir. Visual Studio 2015 veya 2017 kullanıyorsanız, önce uygulamayı yerel olarak çalıştırın, değiştirmelisiniz Not `Data Source` Web.config ve App.config dosyaları SQL Server yerel veritabanı bağlantı dizesinde parçası `Data Source=(localdb)\v11.0` için `Data Source=(LocalDb)\MSSQLLocalDB`.

> [!NOTE]
> <a name="note"></a>Bu öğreticiyi tamamlamak için bir Azure hesabınızın olması gerekir:
>
> * Yapabilecekleriniz [ücretsiz bir Azure hesabı açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): Ücretli Azure hizmetlerini denemek için kullanabileceğiniz, ve hatta kullanıldıktan sonra hesabı sürdürebilir ve Web siteleri gibi ücretsiz Azure hizmetlerine krediler alırsınız. Açıkça ayarlarınızı değiştirip ücretlendirme istemediğiniz sürece kredi kartınız asla ücretlendirilmeyecektir.
> * Yapabilecekleriniz [Visual Studio aboneleri için aylık Azure kredi etkinleştirme](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): aboneliğinizi Ücretli Azure hizmetlerinizi kullanabildiğiniz her ay kredi verir.
>
> Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin. Kredi kartı ve taahhüt gerekmez.
>
>

## <a id="learn"></a>Öğrenecekleriniz
Öğretici aşağıdaki görevlerin nasıl yapılacağını gösterir:

* Makinenizi Azure geliştirme için Azure SDK'sını (yalnızca Visual Studio 2013 ve 2015 kullanıcılar için) yükleyerek etkinleştirin.
* İlişkili web projesi dağıttığınızda, bir Azure Web işi otomatik olarak dağıtan bir konsol uygulama projesi oluşturun.
* Web işleri SDK'si arka uç geliştirme bilgisayarındaki yerel olarak test edin.
* App Service'teki bir web uygulaması için Web işleri arka ucu ile bir uygulama yayımlayın.
* Dosyaları karşıya yükleme ve Azure Blob hizmetine depolama.
* Azure Storage kuyruklarını ve BLOB'ları ile çalışmak için Azure WebJobs SDK'sını kullanın.

## <a id="contosoads"></a>Uygulama mimarisi
Örnek uygulama kullanır [kuyruk merkezli çalışma deseni](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) bir arka uç işleme küçük resimler oluşturma CPU yoğunluklu iş yükünü azaltmak için.

Uygulama, tablolar oluşturmak ve verilere erişmek için Entity Framework Code First kullanarak reklamları bir SQL veritabanına depolar. Her reklam için veritabanı iki URL depolar: biri tam boyutlu görüntü ve diğeri küçük resim.

![Reklam tablosu](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

Bir kullanıcı görüntü yüklediğinde, web uygulaması görüntüde depolayan bir [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), ve reklam bilgilerini blob'u işaret eden bir URL veritabanıyla depolar. Aynı zamanda bir Azure kuyruğuna ileti yazar. Bir Azure Web işi çalışan bir arka uç işleminde sıra yeni iletiler için Web işleri SDK'si yoklar. Yeni bir ileti görüntülendiğinde, Web işi, görüntü için bir küçük resim oluşturur ve küçük resim URL'si veritabanı alanını bu reklam için güncelleştirir. Uygulama bölümlerinin nasıl etkileşim gösteren diyagram şöyledir:

![Contoso Ads mimarisi](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
Öğretici yönergeleri 2.7.1 .NET için Azure SDK'SININ uygulamak veya sonraki bir sürümü.

## <a id="storage"></a>Bir Azure depolama hesabı oluşturma
Azure Storage hesabı kuyruk ve blob verilerini buluta depolamaya yönelik kaynaklar sağlar. Pano günlük verilerini depolamak için bu WebJobs SDK'sı tarafından da kullanılır.

Gerçek dünya uygulamada genellikle uygulama verilerine karşı günlük verileri için ayrı hesaplar ve test verilerine karşı üretim verileri için ayrı hesaplar oluşturursunuz. Bu öğreticide yalnızca tek bir hesap kullanacaksınız.

1. Açık **Sunucu Gezgini** Visual Studio'daki.
2. Sağ **Azure** düğümünü ve ardından **Microsoft Azure aboneliğine Bağlan...** .
   
   ![Azure'a Bağlanma](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. Azure kimlik bilgilerinizi kullanarak oturum açın.
4. Sağ **depolama** Azure düğümünü ve ardından altında **depolama hesabı oluştur**.
   
   ![Depolama hesabı oluşturma](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. İçinde **depolama hesabı oluştur** iletişim kutusunda, depolama hesabı için bir ad girin.

    Adı olmalı benzersiz olmalıdır (başka bir Azure depolama hesabı aynı ada sahip olabilir). Girdiğiniz ad zaten kullanımda değiştirmek için bir fırsat alırsınız.

    Depolama hesabınıza erişmek için URL *{ad}*. core.windows.net.
6. Ayarlama **bölge veya benzeşim grubunda** size en yakın bölgeyi aşağı açılan liste.

    Bu ayar, hangi Azure veri merkezi depolama hesabınız barındıracak belirtir. Bu öğretici için tercih ettiğiniz bir dikkat çekici fark yapmaz. Ancak, bir üretim web uygulaması için web sunucunuz ve gecikme süresi ve veri çıkış ücretleri en aza indirmek için aynı bölgede olması için depolama hesabınız istiyor. (Daha sonra oluşturacağınız) web uygulamasını datacenter gecikme süresi en aza indirmek için web uygulamasına erişme tarayıcılar mümkün olduğunca yakın.
7. **Çoğaltma** açılır listesini **Yerel olarak yedekli** olarak ayarlayın.

    Bir depolama hesabı için coğrafi çoğaltma etkinleştirildiğinde, birincil konumda önemli bir olağanüstü durum oluşması halinde ikincil bir veri merkezine yük devretme için depolanan içerik bu konuma çoğaltılır. Coğrafi çoğaltma ek ücretlere neden olabilir. Test ve geliştirme hesaplarında genellikle coğrafi çoğaltma için ödeme yapmak istemezsiniz. Daha fazla bilgi için bkz. [Depolama hesabı oluşturma, yönetme veya silme](../storage/common/storage-create-storage-account.md).
8. **Oluştur**'a tıklayın.

    ![Yeni depolama hesabı](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <a id="download"></a>Uygulamayı Yükle
1. [Tamamlanan çözümü](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb) indirip sıkıştırmasını açın.
2. Visual Studio’yu çalıştırın.
3. Gelen **dosya** menüsünü seçin **Aç > Proje/çözüm**, çözümü indirdiğiniz yere gidin ve ardından çözüm dosyasını açın.
4. Çözümü derlemek için CTRL+SHIFT+B'ye basın.

    Varsayılan olarak Visual Studio, *.zip* dosyasına dahil edilmeyen NuGet paketini otomatik olarak geri yükler. Paketler geri yüklenmezse varsa bunları el ile giderek yükleyin **çözüm için NuGet paketlerini Yönet** iletişim ve tıklayarak **geri** sağ üst köşedeki düğmesi.
5. İçinde **Çözüm Gezgini**, olduğundan emin olun **ContosoAdsWeb** başlangıç projesi olarak seçilir.

## <a id="configurestorage"></a>Depolama hesabınızı kullanmak için uygulamayı yapılandırma
1. Uygulamayı açmak *Web.config* ContosoAdsWeb projesinde dosya.

    Dosya, bir SQL bağlantı dizesi ve BLOB'lar ve kuyruklarla çalışmaya yönelik bir Azure depolama bağlantı dizesi içerir.

    SQL bağlantı dizesi işaret bir [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) veritabanı.

    Depolama bağlantı dizesi yer tutucuları depolama hesabı adı ve erişim anahtarı için olan bir örnektir. Bu ad ve anahtar depolama hesabınızın sahip bir bağlantı dizesi ile değiştirirsiniz.  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    Depolama bağlantı dizesi, Web işleri SDK'si kullandığı adı olduğundan AzureWebJobsStorage varsayılan olarak adlandırılır. Azure ortamında yalnızca bir bağlantı dizesi değerine ayarlamanız gerekir böylece aynı adı burada kullanılır.
2. İçinde **Sunucu Gezgini**, depolama hesabınızın altında sağ **depolama** düğümünü ve ardından **özellikleri**.

    ![Depolama hesabı Özellikler'i tıklatın](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. İçinde **özellikleri** penceresinde, tıklatın **depolama hesabı anahtarlarını**ve üç nokta'ı tıklatın.

    ![Depolama hesabı anahtarları](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. Kopya **bağlantı dizesi**.

    ![Depolama hesabı anahtarları iletişim](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. Depolama bağlantı dizesini değiştirin *Web.config* kopyaladığınız bağlantı dizesini içeren dosya. Her şeyi tırnak işaretleri içindeki ancak yapıştırmadan önce tırnak işaretleri dahil değil seçtiğinizden emin olun.
6. Açık *App.config* ContosoAdsWebJob proje dosyasında.

    Bu dosya iki depolama bağlantı dizeleri, bir uygulama verileri için ve günlüğe kaydetme için bir sahiptir. Uygulama verilerini ve günlüğe kaydetme için ayrı bir depolama hesaplarını kullanabilirsiniz ve kullanabileceğiniz [birden çok depolama hesapları için verileri](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs). Bu öğreticide, tek bir depolama hesabına kullanacaksınız. Depolama hesabı anahtarlarını yer tutucular bağlantı dizelerine sahipsiniz.

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

    Varsayılan olarak, Web işleri SDK'si için bağlantı dizelerini AzureWebJobsStorage ve AzureWebJobsDashboard adlı arar. Alternatif olarak, şunları yapabilirsiniz [deposu bağlantı dizesi ancak istediğiniz ve içinde açıkça geçirmek `JobHost` nesne](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).
7. Her iki storage bağlantı dizelerini daha önce kopyaladığınız bağlantı dizesi ile değiştirin.
8. Yaptığınız değişiklikleri kaydedin.

## <a id="run"></a>Uygulamayı yerel olarak çalıştırın
1. Web ön uç uygulamasının başlatmak için CTRL + F5 tuşuna basın.

    Varsayılan tarayıcı giriş sayfası açılır. (Web projesini başlangıç projesi yapmış olduğunuz için çalışır.)

    ![Contoso Ads giriş sayfası](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. Web işi arka uç uygulamasının başlatmak için ContosoAdsWebJob projeye sağ **Çözüm Gezgini**ve ardından **hata ayıklama** > **başlangıç yeni örnek**.

    Bir konsol uygulama penceresi açar ve WebJobs SDK JobHost nesne çalışmaya başladı belirten günlük iletilerini görüntüler.

    ![Arka uç çalıştığını gösteren konsol uygulama penceresi](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. Tarayıcınızda, tıklatın **bir Ad oluşturmak**.
4. Bazı test verilerini girin, karşıya yükleyin ve ardından bir görüntü seçin **oluşturma**.

    ![Sayfa oluşturma](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    Uygulama Dizin sayfasına gider, ancak işleme henüz tamamlanmadığından yeni reklam için bir küçük resim göstermez.

    Bu sırada, kısa bir bekleme bir kuyruk iletisi alındı ve işlenmiş olan bir günlük iletisi konsol uygulaması penceresinde gösterir.

    ![Bir kuyruk iletisi işlendiğini gösteren konsol uygulama penceresi](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. Konsol uygulaması penceresinde günlük iletilerini gördükten sonra küçük resmi görmek için dizin sayfasını yenileyin.

    ![Dizin sayfası](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. Tam boyutlu görüntüyü görmek için reklamınıza ilişkin **Ayrıntılar**’a tıklayın.

    ![Ayrıntılar sayfası](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

Uygulama'yı yerel bilgisayarınızda çalışır durumda ve bir SQL veritabanı bilgisayarınızı, ancak üzerinde bulunan Kuyruklarla Çalışma ve içinde BLOB'ların sunucusu kullanarak bulut. Aşağıdaki bölümde bulut veritabanı yanı sıra bulut BLOB'ları ve kuyrukları kullanma uygulaması bulutta çalıştıracaksınız.  

## <a id="runincloud"></a>Uygulamayı bulutta çalıştırın
Uygulamayı bulutta çalıştırmak için aşağıdaki adımları gerçekleştirin:

* Web uygulamaları dağıtın. Visual Studio otomatik olarak yeni bir web uygulaması App Service ve bir SQL veritabanı örneği oluşturur.
* Web uygulaması, Azure SQL veritabanı ve depolama hesabınızı kullanacak şekilde yapılandırın.

Bulutta çalıştırılırken bazı ads oluşturduktan sonra izleme özelliklerini sunmak için sahip zengin görmek için Web işleri SDK'si Panoyu görebilmek.

### <a name="deploy-to-web-apps"></a>Web uygulamaları dağıtma

1. Tarayıcı ve konsol uygulaması penceresini kapatın.
2. Adımları [Azure SQL veritabanı ile Yayımla](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) bölümü.
3. Dağıtma adımları tamamladıktan sonra bu makaledeki kalan görevlere devam edin.

### <a name="configure-the-web-app-to-use-your-azure-sql-database-and-storage-account"></a>Azure SQL veritabanı ve depolama hesabınızı kullanmak için web uygulamasını yapılandırma
Bir güvenlik en iyi uygulama olan [bağlantı dizeleri gibi hassas bilgileri kaynak kodu depoları içinde depolanan dosyaları içinde Geçirilmemesi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets). Azure Bunu yapmak için bir yöntem sunar: ASP.NET yapılandırma API'leri uygulama Azure'da çalıştırıldığında bu değerleri otomatik olarak seçmesini ve Azure ortamında bağlantı dizesini ve diğer ayar değerlerini ayarlayabilirsiniz. Bu değerleri kullanarak Azure'da ayarlayabilirsiniz **Sunucu Gezgini**, Azure portalı, Windows PowerShell veya platformlar arası komut satırı arabirimi. Daha fazla bilgi için bkz: [nasıl uygulama dizeleri ve bağlantı dizeleri çalışma](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).

Bu bölümde, kullandığınız **Sunucu Gezgini** bağlantı ile Azure dize değerlerini ayarlamak için.

1. İçinde **Sunucu Gezgini**, web uygulamanızı altında sağ **Azure > uygulama hizmeti > {kaynak grubunuz}**ve ardından **görünüm ayarlarını**.

    **Azure Web uygulaması** penceresi açılır **yapılandırma** sekmesi.
2. Seçtiğiniz SQL veritabanında yapılandırdığınızda adına DefaultConnection bağlantı dizesinin adını değiştirmek [Azure SQL veritabanı ile Yayımla](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) makalesi.

    Doğru bağlantı dizesi değeri zaten şekilde ilişkilendirilmiş bir veritabanı ile web uygulaması oluşturduğunuzda azure, bu bağlantı dizesi otomatik olarak oluşturulur. Kodunuzu görmek için yalnızca adını değiştirirsiniz.
3. AzureWebJobsStorage ve AzureWebJobsDashboard adlı iki yeni bağlantı dizeleri ekleyin. Veritabanı türü kümesine **özel**ve bağlantı dizesi değerini daha önce kullandığınız aynı değere ayarlayın *Web.config* ve *App.config* dosyaları. (Tüm bağlantı dizesi, yalnızca erişim anahtarı içerir ve tırnak işaretleri dahil etmeyin emin olun.)

    Bu bağlantı dizeleri WebJobs SDK tarafından kullanılan uygulama verileri, diğeri için günlük için. Daha önce gördüğünüz gibi bir uygulama verileri için de web ön uç kodu tarafından kullanılır.
4. **Kaydet** düğmesine tıklayın.

    ![Azure Portalı'nda bağlantı dizeleri](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. İçinde **Sunucu Gezgini**, web uygulaması sağ tıklayın ve ardından **durdurmak**.
6. Web uygulaması durdurulduktan sonra web uygulaması tekrar sağ tıklayın ve ardından **Başlat**.

   Web işi yayımladığınızda, ancak bir yapılandırma değişikliği yaptığınızda durdurur otomatik olarak başlar. Yeniden başlatmak için web uygulaması yeniden veya WebJob içinde yeniden [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715). Bu genellikle bir yapılandırma değişikliğinden sonra web uygulaması yeniden önerilir.
7. Web uygulaması URL'si kendi adres çubuğunda sahip tarayıcı penceresini yenileyin.

    Giriş sayfası görüntülenir.
8. Ne zaman yaptığınız gibi bir ad oluşturun, [uygulama yerel olarak çalıştırılan](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).

   Küçük resim ilk olmadan dizin sayfası gösterilir.
9. Birkaç saniye sonra sayfayı yenileyin ve küçük resim görünür.

   Küçük resim görünmüyorsa, veya bunu yeniden başlatmak Web işi için bir dakika beklemeniz gerekebilir. Sayfa yenilediğinizde bir süre sonra hala küçük resim görmüyorsanız, Web işi otomatik olarak başlatılmamış olabilir. Bu durumda, Git **uygulama hizmetleri** dikey penceresinde [Azure portal](https://portal.azure.com/), web uygulamanızı bulun ve ardından **Başlat**.

### <a name="view-the-webjobs-sdk-dashboard"></a>Web işleri SDK'si Pano görünümü
1. İçinde [Azure portal](https://portal.azure.com/)seçin **App Services dikey**web uygulamanızı bulun ve seçin **WebJobs**.
3. Seçin **günlükleri** sekmesi.

    ![Günlükleri sekmesi](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    Web işleri SDK'si Pano için yeni bir tarayıcı sekmesi açar. WebJob çalışıyor ve işlevlerin bir listesini kodunuzda WebJobs SDK tetiklenen gösterir Panosu gösterir.
4. Yürütülmesinin ayrıntılarını görmek için işlevleri birini tıklatın.

    ![Web işleri SDK'si Panosu](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![Web işleri SDK'si Panosu](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    **Yeniden yürütme işlevi** düğmesi, bu sayfada işlevi yeniden çağırın Web işleri SDK'si framework neden olur ve ilk işlevine geçirilen verileri değiştirme olanağı sağlar.

> [!NOTE]
> Bitirdiğinizde test, web uygulaması, depolama hesabı ve SQL veritabanı örneğinde silme düşünün. Web uygulaması ücretsizdir, ancak SQL depolama hesabı ve veritabanı örneği ücretler tahakkuk (barındırabilir, küçük boyutu en az). Ayrıca, çalışan web uygulaması değiştirmeden bırakırsanız, URL'nizi bulan herkes oluşturun ve reklamları görüntüleyin. 
>
>

### <a name="delete-your-web-app"></a>Web uygulamanızı Sil
Portalda, Git **uygulama hizmetleri** dikey penceresinde, bulun ve web uygulamanızı seçin ve ardından **silmek**. Yalnızca istiyorsanız geçici olarak başkalarının web uygulaması erişmesini önlemek için tıklatın **durdurmak** yerine. Bu durumda ücretler SQL veritabanı ve depolama hesabı için tahakkuk etmeye devam eder.

### <a name="delete-your-storage-account"></a>Depolama hesabınızı silme
Depolama hesabınızı silmek için bkz: [bir depolama hesabını silmek](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account). 

### <a name="delete-your-database"></a>Veritabanınızı Sil
SQL veritabanınız silmek için bkz: [Azure SQL Database REST API'sini](https://docs.microsoft.com/rest/api/sql/) belgeleri.

## <a id="create"></a>Uygulamayı sıfırdan oluşturma
Bu bölümde aşağıdaki görevleri gerçekleştirmeniz:

* Visual Studio çözümü ile bir web projesi oluşturun.
* Veriler için bir sınıf kitaplığı proje ekleyin ön uç ve arka uç arasında paylaşılan erişim katmanı.
* Arka uç için bir konsol uygulama projesi etkin Web işleri dağıtımı ile ekleyin.
* NuGet paketleri ekleyin.
* Proje başvurularını ayarlayın.
* Öğreticinin önceki bölümde çalıştığınız indirilen uygulama uygulama kodu ve yapılandırma dosyalarını kopyalayın.
* Azure BLOB'ları ve kuyrukları ve WebJobs SDK ile çalışan kod bölümlerini gözden geçirin.

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a>Bir web projesi ve sınıf kitaplığı proje bir Visual Studio çözümü oluşturun
1. Visual Studio'da, **dosya** > **yeni** > **proje**.
2. İçinde **yeni proje** iletişim kutusunda, seçin **Visual C#** > **Web** > **ASP.NET Web uygulaması (.NET Framework)**.
3. Projeyi ContosoAdsWeb, ad ContosoAdsWebJobsSDK (çözüm adı, onu indirilen çözümü ile aynı klasörde yerleştiriyorsanız değiştirin) çözümü olarak adlandırın ve ardından **Tamam**.

    ![Yeni Proje](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. İçinde **yeni ASP.NET Web uygulaması** iletişim kutusunda, MVC şablonunu seçin ve Seç **kimlik doğrulamayı Değiştir**.

    ![Kimlik Doğrulamayı Değiştirme](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. İçinde **kimlik doğrulamayı Değiştir** iletişim kutusunda, seçin **doğrulaması yok**ve ardından **Tamam**.

    ![Kimlik Doğrulaması Yok](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. İçinde **yeni ASP.NET Web uygulaması** iletişim kutusunda, tıklatın **Tamam**.

    Visual Studio çözümü ve web projesi oluşturur.
7. İçinde **Çözüm Gezgini**, çözüme (projeye değil) sağ tıklayın ve seçin **Ekle** > **yeni proje**.
8. İçinde **Yeni Proje Ekle** iletişim kutusunda, seçin **Visual C#** > **Windows Klasik Masaüstü** > **sınıf kitaplığı (.NET Framework)**  şablonu.  
9. Projeyi *ContosoAdsCommon* olarak adlandırın ve ardından **Tamam**’a tıklayın.

    Bu projenin Entity Framework bağlamına ve ön uç ve arka uç kullanacağı veri modeli içerir. Alternatif olarak, web projesinde EF ile ilgili sınıflar tanımlayın ve Web işi projeden proje başvurusu. Ancak, ardından Web işi projeniz gerekli olmayan web derlemelerine başvuru olması gerekir.

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a>Web işleri dağıtımı etkin olan bir konsol uygulama projesi ekleyin
1. Web projesi (çözüm veya sınıf kitaplığı proje değil) sağ tıklayın ve ardından **Ekle** > **yeni Azure Web işi projesi**.

    ![Yeni Azure Web işi projesinin menü seçimi](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. İçinde **Azure Web işine Ekle** iletişim kutusunda, ContosoAdsWebJob her ikisini birden girin **proje adı** ve **Web işi adı**. Bırakın **WebJob çalıştırma modu** kümesine **sürekli olarak çalıştır**.
3. **Tamam** düğmesine tıklayın.

   Visual Studio web projesini dağıtma her bir Web işi dağıtmak için yapılandırılmış bir konsol uygulaması oluşturur. Bunu yapmak için aşağıdaki görevleri projesi oluşturduktan sonra gerçekleştirilen:

   * Eklenen bir *webjob yayımlama settings.json* Web işi projesi özellikleri klasördeki dosya.
   * Eklenen bir *webjobs list.json* web projesi özellikleri klasörü dosyasında.
   * Web işi projesinin Microsoft.Web.WebJobs.Publish NuGet paketi yüklü.

   Bu değişiklikler hakkında daha fazla bilgi için bkz: [Visual Studio kullanarak Web işleri dağıtma](websites-dotnet-deploy-webjobs.md).

### <a name="add-nuget-packages"></a>NuGet paketleri ekleme
Bir Web işi projesi için yeni proje şablonu WebJobs SDK NuGet paketini otomatik olarak yükler [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) ve bağımlılıklarını.

Web işi projesinin otomatik olarak yüklenen Web işleri SDK'si bağımlılıkları Azure Storage istemci kitaplığı (SCL) biridir. Ancak, BLOB'lar ve kuyruklarla çalışmaya web projesine ekleme gerekir.

1. Açık **NuGet paketlerini Yönet** çözümü için iletişim kutusu.
2. Sol bölmede seçin **yüklü paketleri**.
3. Bul *Azure Storage* paketini ve ardından **Yönet**.
4. İçinde **projeleri seçin** kutusunda, seçin **ContosoAdsWeb** onay kutusunu işaretleyin ve ardından **Tamam**.

    Üç projenin Entity Framework SQL veritabanındaki verilerle çalışmak için kullanın.
5. Sol bölmede seçin **çevrimiçi**.
6. *EntityFramework* NuGet paketini bulun ve üç projenin tamamına yükleyin.

### <a name="set-project-references"></a>Proje başvurularını ayarlama
Her ikisi de ContosoAdsCommon projesine bir başvuru gerekir böylece hem web hem de Web işi projeleri SQL veritabanı ile çalışır.

1. ContosoAdsWeb projesinde ContosoAdsCommon projesine bir başvuru ayarlayın. (ContosoAdsWeb projesine sağ tıklayın ve ardından **Ekle** > **başvuru**. 
2. İçinde **başvuru Yöneticisi** iletişim kutusunda **projeleri** > **çözüm** > **ContosoAdsCommon**, ve ardından **Tamam**.)
   
    Web işi projesinin başvuruları görüntülerle çalışma ve bağlantı dizeleri erişmek için gerekir.

4. Bir başvuru ContosoAdsWebJob projesinde kümesine `System.Drawing` ve `System.Configuration`.

### <a name="add-code-and-configuration-files"></a>Kod ve yapılandırma dosyaları Ekle
Bu öğretici gösterme nasıl [MVC denetleyicileri ve yapı iskelesi kullanarak görünümleri oluşturma](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), nasıl için [SQL Server veritabanları ile çalışan Entity Framework kod yazma](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), veya [temelleri zaman uyumsuz ASP.NET 4.5 programlama](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async). Bu nedenle, tüm bu yapmak için kalan tek şey indirilen çözümden yeni çözüme kod ve yapılandırma dosyaları kopyala. Bunu sonra aşağıdaki bölümlerde Göster ve kodun temel kısımları açıklanmaktadır.

Bir proje veya klasöre dosya eklemek için proje veya klasöre sağ tıklayıp **Ekle** > **Mevcut Öğe** seçeneğine tıklayın. İstediğiniz dosyaları seçin **Ekle**. Mevcut dosyaları değiştirmek isteyip istemediğiniz sorulursa **Evet**’e tıklayın.

1. ContosoAdsCommon projesinde silme *Class1.cs* dosya ve onun yerine, indirilen projeden aşağıdaki dosyaları ekleyin.

   * *Ad.cs*
   * *ContosoAdscontext.cs*
   * *BlobInformation.cs*
2. ContosoAdsWeb projesinde indirilen projeden aşağıdaki dosyaları ekleyin.

   * *Web.config*
   * *Global.asax.cs*  
   * İçinde *denetleyicileri* klasörü: *AdController.cs*
   * İçinde *görünümler/paylaşılan* klasörü: *_Layout.cshtml* dosyası
   * İçinde *görünümler* klasörü: *Index.cshtml*
   * İçinde *görünümler/reklam* klasörü (öncelikle klasörü oluşturun): beş *.cshtml* dosyaları
3. ContosoAdsWebJob projesinde indirilen projeden aşağıdaki dosyaları ekleyin.

   * *App.config* (dosya türü filtresi için değiştirme **tüm dosyaları**)
   * *Program.cs*
   * *Functions.cs*

Şimdi oluşturmak, çalıştırmak ve öğreticide daha önce belirtildiği gibi uygulamayı dağıtın. Ancak, bunu yapmadan önce hala için dağıtılan ilk web uygulamasında çalışan Web işini durdurma. Aksi takdirde, bu Web işi sıra iletileri yerel olarak veya tümü aynı depolama hesabı kullanıyorsanız bu yana yeni bir web uygulamasında çalışan uygulama tarafından oluşturulan işler.

## <a id="code"></a>Uygulama kodu gözden geçirme
Aşağıdaki bölümlerde Web işleri SDK'si ve Azure Storage blobları ve kuyrukları ile çalışmayla ilgili kod açıklanmaktadır.

> [!NOTE]
> Web işleri SDK'si belirli kodunu Git [Program.cs ve Functions.cs](#programcs) bölümler.
>
>

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
Ad.cs dosyası reklam kategorileri için bir numaralandırma ve reklam bilgileri için bir POCO varlık sınıfı tanımlar.

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
ContosoAdsContext sınıfı reklam sınıfının Entity Framework bir SQL veritabanında depolayan bir DbSet koleksiyonunda kullanıldığını belirtir.

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

Sınıfın iki oluşturucusu vardır. Birincisi web projesi tarafından kullanılır ve Web.config dosyasını veya Azure çalışma zamanı ortamı saklanan bir bağlantı dizesinin adını belirtir. İkinci oluşturucu, gerçek bağlantı dizesine geçmenizi sağlar. Bir Web.config dosyası olmadığından, Web işi projesi tarafından gereklidir. Bu bağlantı dizesinin nereye depolandığını daha önce gördünüz ve kodun DbContext sınıfını başlattığında bağlantı dizesini nasıl aldığını daha sonra göreceksiniz.

### <a name="contosoadscommon---blobinformationcs"></a>ContosoAdsCommon - BlobInformation.cs
`BlobInformation` Sınıfı, bir kuyruk iletisi bir görüntü blob'u hakkında bilgi depolamak için kullanılır.

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
`Application_Start` yönteminden çağrılan kod, henüz yoksa bir *görüntüler* blob kapsayıcısı ve bir *görüntüler* kuyruğu oluşturur. Bu, yeni bir depolama hesabı kullanarak başlattığınızda, gerekli blob kapsayıcısının ve kuyruğun otomatik olarak oluşturulmasını sağlar.

Depolama bağlantı dizesini kullanarak depolama hesabına erişim izni kodu alır *Web.config* dosya ya da Azure çalışma zamanı ortamı.

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

Ardından, bir başvuru edinir *görüntüleri* blob kapsayıcısı, önceden var olmayan ve erişim izinlerini ve yeni kapsayıcıda ayarlar kapsayıcı oluşturur. Varsayılan olarak, istemcilerin blob'lara erişmesine yalnızca depolama hesabı kimlik bilgileri ile yeni kapsayıcılar izin verin. Web uygulaması BLOB'ları, görüntü BLOB'larını işaret eden URL'leri kullanarak görüntüleri gösterebilmek ortak olması gerekir.

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

Benzer bir kod başvuru edinir *thumbnailrequest* sıraya almak ve yeni bir sıra oluşturur. Bu durumda hiçbir izin değişikliği gerekli değildir.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb - _Layout.cshtml
*_Layout.cshtml* dosyası üst bilgi ve alt bilgide uygulama adını ayarlar ve bir "Reklamlar" menü girişi oluşturur.

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Görünümler\Giriş\Dizin.cshtml
*Görünümler\Giriş\Dizin.cshtml* dosyası, giriş sayfasında kategori bağlantılarını gösterir. Bağlantılar `Category` numaralandırmasının bir sorgu dizesi değişkeni içindeki tamsayı değerini Reklam Dizini sayfasına geçirir.

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
Oluşturucu, *AdController.cs* dosyasında blob’larla ve kuyruklarla çalışmaya yönelik bir API sağlayan Azure Storage İstemci Kitaplığı nesneleri oluşturmak için `InitializeStorage` yöntemini çağırır.

Ardından, kodu bir başvuru alır *görüntüleri* daha önce gördüğünüz gibi blob kapsayıcısı *Global.asax.cs*. Yaparken, varsayılan ayarlar [yeniden deneme ilkesi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) bir web uygulaması için uygun. Varsayılan üstel geri alma yeniden deneme ilkesi, web uygulamasını geçici bir hata için tekrarlanan yeniden denemelerde bir dakikadan uzun süre askıya alabilir. Burada belirtilen yeniden deneme ilkesi üç denemeye kadar her denemeden sonra en fazla üç saniye bekler.

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

Benzer bir kod, *görüntüler* kuyruğuna başvuru edinir.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

Denetleyici kodlarının birçoğu bir DbContext sınıfı kullanarak Entity Framework veri modeli ile çalışmak için tipiktir. Dosyayı karşıya yükleyen ve blob depolama alanına kaydeden HttpPost `Create` yöntemi bunun bir istisnasıdır. Model bağlayıcı, yönteme bir [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) nesnesi sağlar.

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

Kullanıcı karşıya yüklemek için bir dosya seçtiyse kod bu dosyayı karşıya yükler, bir blob'a kaydeder ve Ad veritabanı kaydını blob’a işaret eden bir URL ile güncelleştirir.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

Karşıya yüklemeyi yapan kod `UploadAndSaveBlobAsync` yöntemindedir. Blob için bir GUID adı oluşturur, dosyayı karşıya yükler ve kaydeder ve kaydedilmiş blob için bir başvuru döndürür.

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

HttpPost sonra `Create` yöntemi bir blob'u karşıya yükleyip veritabanını güncelleştirir, görüntüyü bir küçük resim dönüştürme için hazır olduğunu arka uç işlemine bildirmek üzere bir kuyruk iletisi oluşturur.

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

HttpPost kodunu `Edit` yöntemi olduğunu benzer, kullanıcı yeni bir görüntü dosyası belirlerse, bu ad zaten mevcut BLOB silinmelidir dışında.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

Bir ad sildiğinizde, BLOB'ları silen kod aşağıdaki gibidir:

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
*Index.cshtml* dosyası küçük resimleri diğer reklam verileriyle birlikte gösterir:

        <img  src="@Html.Raw(item.ThumbnailURL)" />

*Details.cshtml* dosyası tam boyutlu görüntüyü gösterir:

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml ve Edit.cshtml
*Create.cshtml* ve *Edit.cshtml* dosyaları denetleyicinin `HttpPostedFileBase` nesnesi almasını sağlayan form kodlamasını belirtir.

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

Bir `<input>` öğesi tarayıcıya bir dosya seçme iletişim kutusu açmasını söyler.

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <a id="programcs"></a>ContosoAdsWebJob - Program.cs
Web işi başladığında, `Main` yöntemini çağırır WebJobs SDK `JobHost.RunAndBlock` yürütülmesi başlamaya yöntemi tetiklenen geçerli iş parçacığının işlevleri.

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail yöntemi
Bir kuyruk iletisi alındığında WebJobs SDK bu yöntemi çağırır. Yöntem bir küçük resim oluşturur ve küçük resim koyar veritabanındaki URL.

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
            // be instantiated and disposed within the function.
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

* `QueueTrigger` Özniteliği thumbnailrequest sıranın üzerinde yeni bir ileti alındığında bu yöntemi çağırmak için Web işleri SDK'si yönlendirir.

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    `BlobInformation` Kuyruk iletisini nesnedir içine otomatik olarak Serisi kaldırılan `blobInfo` parametresi. Kuyruk iletisini yöntemi tamamlandığında silinir. Yöntem tamamlanmadan önce başarısız olursa, kuyruk iletisini silinmez; 10 dakikalık kiralama süresi dolduktan sonra yeniden çekilmesi için yayımlanan ve işlenebilir. Bir ileti her zaman bir özel durum neden olursa bu sırası süresiz olarak yinelenen olmaz. Bir iletiyi işlemek 5 başarısız denemeden sonra {queuename} adlı bir sıraya ileti taşınır-zararlı. En fazla denemesi sayısı yapılandırılabilir.
* İki `Blob` öznitelikler BLOB'lar için bağlı olan nesneleri sağlar: biri mevcut görüntü blob'u, yöntem oluşturur Yeni bir küçük resim blob birine.

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    BLOB adları gelen özelliklerinden `BlobInformation` kuyruk iletisini alınan nesne (`BlobName` ve `BlobNameWithoutExtension`). Depolama istemcisi kitaplığı tam işlevselliğini almak için kullanabileceğiniz `CloudBlockBlob` BLOB'lar ile çalışmak için sınıf. Çalışmak için yazılmış kodun yeniden isteyip istemediğinizi `Stream` nesneleri kullanabileceğiniz `Stream` sınıfı.

Web işleri SDK'si öznitelikleri kullanan işlevler yazma hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

* [Web İşleri SDK’sı ile Azure kuyruk depolama kullanımı](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [Web İşleri SDK’sı ile Azure blob depolama kullanımı](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [Web İşleri SDK’sı ile Azure tablo depolama kullanımı](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [Web İşleri SDK’sı ile Azure Service Bus kullanımı](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * Web uygulamanız birden çok sanal makine çalışıyorsa, birden çok Web işleri eşzamanlı çalışan ve bazı senaryolarda bu birden çok kez işlenen aynı veri kaybına neden. Yerleşik sırası, blob ve Service Bus Tetikleyicileri kullanırsanız, bir sorun değildir. SDK işlevlerinizi yalnızca bir kez her ileti veya blob işleneceğini sağlar.
> * Normal şekilde kapatılmasını uygulama hakkında daha fazla bilgi için bkz: [kapama](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).
> * Kodda `ConvertImageToThumbnailJPG` (gösterilmez) yöntemini kullanır sınıflarda `System.Drawing` kolaylık olması için ad alanı. Ancak, bu ad alanındaki sınıflar Windows Forms ile kullanılmak üzere tasarlanmıştır. Bir Windows veya ASP.NET hizmetinde kullanılması desteklenmez. Görüntü işleme seçenekleri hakkında daha fazla bilgi için bkz. [Dinamik Görüntü Oluşturma](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) ve [Görüntü Yeniden Boyutlandırmaya Ayrıntılı Bakış](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).
>
>

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, arka uç işleme için Web işleri SDK'si kullanan basit bir çok katmanlı uygulama gördünüz. Bu bölümde, ASP.NET çok katmanlı uygulamaları ve Web işleri hakkında daha fazla bilgi edinmek için bazı öneriler sunar.

### <a name="missing-features"></a>Eksik Özellikler
Uygulama bir başlangıç öğreticisi için basit tutulmuştur. Gerçek dünya uygulamada uygulamak [bağımlılık ekleme](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) ve [depo ve iş birimi düzenleri](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), kullanın [günlüğe kaydetme için bir arabirimi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), kullanmak[EF Code First geçişleri](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) veri modeli değişikliklerini yönetmek ve kullanmak için [EF bağlantı dayanıklılığı](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) geçici ağ hatalarını yönetmek için.

### <a name="scaling-webjobs"></a>Web işleri ölçeklendirme
Web işleri bir web uygulaması bağlamında çalışır ve ayrı olarak ölçeklenebilir değildir. Örneğin, bir standart web app örneği varsa, çalışan, arka plan işlemi yalnızca bir örneğine sahip ve bazı Aksi durumda web içerik sunmak kullanılabilir olacak sunucu kaynaklarının (CPU, bellek, vb.) kullanıyor.

Trafik gün veya haftanın günü zamanına göre değişir ve arka uç işleme bekleyebilirsiniz ihtiyacınız varsa, Webjob'larınızı trafiği düşük zamanlarda çalışmak üzere zamanlayabilirsiniz. Yük hala Bu çözüm için çok yüksekse, arka uç adanmış bir ayrı bir web uygulamasında Web işi olarak bu amaçla çalıştırabilirsiniz. Arka uç web uygulamanızı sonra bağımsız olarak ve ön uç web uygulamanızdan ölçeklendirebilirsiniz.

Daha fazla bilgi için bkz: [ölçeklendirme WebJobs](websites-webjobs-resources.md#scale).

### <a name="avoiding-web-app-timeout-shut-downs"></a>Web uygulaması zaman aşımı kapatma listeleri önleme
Webjob'larınızı her zaman çalıştırıyorsanız ve etkinleştirmek zorunda web uygulamanız tüm örneklerini çalıştıran, emin olmak için [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) özelliği.

### <a name="using-the-webjobs-sdk-outside-of-webjobs"></a>Web işleri dışında WebJobs SDK'sını kullanarak
WebJobs SDK kullanan bir program, bir Web işi olarak azure'da çalıştırmak sahip değil. Yerel olarak çalıştırabilir ve bulut hizmeti çalışan rolü veya bir Windows hizmeti gibi diğer ortamlarda da çalıştırabilirsiniz. Ancak, Web işleri SDK'si Panosu yalnızca Azure web uygulaması erişebilirsiniz. Web uygulaması üzerinde AzureWebJobsDashboard bağlantı dizesi ayarlayarak kullandığınız depolama hesabı bağlanmak zorunda panoyu kullanmak için **yapılandırma** sekmesini Klasik portalı. Ardından, aşağıdaki URL'yi kullanarak panoya elde edebilirsiniz:

https://{webappname}.SCM.azurewebsites.NET/azurejobs/#/Functions

Daha fazla bilgi için bkz: [WebJobs SDK ile yerel geliştirme için bir Pano alma](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), ancak eski bir bağlantı dizesi adı gösterdiğine dikkat edin.

### <a name="more-webjobs-documentation"></a>Daha fazla Web işleri belgeleri
Daha fazla bilgi için bkz: [Azure Web işleri belge kaynakları](http://go.microsoft.com/fwlink/?LinkId=390226).
