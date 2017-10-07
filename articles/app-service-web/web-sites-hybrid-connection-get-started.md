---
title: "Azure App Service içinde karma bağlantılar kullanarak aaaAccess şirket içi kaynakları"
description: "Azure App Service'in web uygulamasında ve statik bir TCP bağlantı noktası kullanan şirket içi kaynağı arasında bağlantı oluşturma"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: a46ed26b-df8e-4fc3-8e05-2d002a6ee508
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: cephalin
ms.openlocfilehash: de7c57b94f4bd6250a93757817178e8455daae4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a>Azure Uygulama Hizmeti’nde karma bağlantıları kullanarak şirket içi kaynaklara erişme
SQL Server, MySQL, HTTP Web API'leri ve birçok özel Web hizmeti gibi statik TCP bağlantı kullanan bir Azure uygulama hizmeti uygulaması tooany şirket içi kaynaklara bağlanabilir. Bu makale size nasıl gösterir toocreate uygulama hizmeti ile bir şirket içi SQL Server veritabanı arasında karma bir bağlantı.

> [!NOTE]
> Hello Web Apps bölümü hello karma bağlantılar özelliği yalnızca hello kullanılabilir [Azure Portal](https://portal.azure.com). toocreate BizTalk Services bağlantısında bkz [karma bağlantılar](http://go.microsoft.com/fwlink/p/?LinkID=397274). 
> 
> Bu içerik, Azure uygulama hizmetinde tooMobile uygulamalar da geçerlidir. 
> 
> 

## <a name="prerequisites"></a>Ön koşullar
* Azure aboneliği. Ücretsiz bir abonelik için bkz: [Azure ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/). 
  
    Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
* toouse bir şirket içi SQL Server veya SQL Server Express veritabanı ile karma bağlantı, TCP/IP'yi statik bağlantı noktası üzerinde etkin toobe gerekir. Statik bağlantı noktası 1433 kullandığından, varsayılan bir örnek SQL Server üzerinde kullanılması önerilir. Yükleme ve karma bağlantılar ile kullanmak için SQL Server Express yapılandırma hakkında daha fazla bilgi için bkz: [Bağlan tooan şirket içi SQL Server bir Azure web karma bağlantılar kullanarak sitesinden](http://go.microsoft.com/fwlink/?LinkID=397979).
* Merhaba bilgisayar üzerinde bu makalenin sonraki bölümlerinde açıklanan hello şirket içi karma Bağlantı Yöneticisi aracısı yükleyin:
  
  * Mümkün tooconnect tooAzure 5671 bağlantı noktası üzerinden olmalıdır
  * Mümkün tooreach hello olmalıdır *ana bilgisayar adı*:*BağlantıNoktasıNumarası* , şirket içi kaynak. 

> [!NOTE]
> Bu makaledeki adımları Hello hello tarayıcı hello şirket içi karma bağlantı aracısını barındıracak bir hello bilgisayardan kullandığınızı varsayar.
> 
> 

## <a name="create-a-web-app-in-hello-azure-portal"></a>Hello Azure portalı bir web uygulaması oluşturma
> [!NOTE]
> Merhaba toouse Bu öğretici için istediğiniz Azure Portal, web uygulaması veya mobil uygulama arka ucu önceden oluşturduğunuz, şimdi çok atlayabilirsiniz[karma bağlantı ve bir BizTalk hizmeti oluşturma](#CreateHC) ve buradan başlayın.
> 
> 

1. Merhaba sol üst köşedeki Merhaba, [Azure Portal](https://portal.azure.com), tıklatın **yeni** > **Web + mobil** > **Web uygulaması**.
   
    ![Yeni web uygulaması][NewWebsite]
2. Merhaba üzerinde **Web uygulaması** dikey penceresinde, bir URL sağlayın ve tıklatın **oluşturma**. 
   
    ![Web sitesi adı][WebsiteCreationBlade]
3. Birkaç dakika sonra hello web uygulaması oluşturuldu ve kendi web uygulaması dikey penceresi görünür. Merhaba dikey sitenizi yönetmenize olanak sağlayan bir dikey olarak kaydırılabilir Pano ' dir.
   
    ![Çalışan Web sitesi][WebSiteRunningBlade]
4. tooverify hello site canlı, hello tıklayabilirsiniz **Gözat** simgesi toodisplay hello varsayılan sayfası.
   
    ![Web uygulamanızı Gözat toosee'ı tıklatın][Browse]
   
    ![Varsayılan web uygulama sayfası][DefaultWebSitePage]

Ardından, karma bir bağlantı ve BizTalk hizmeti hello web uygulaması için oluşturur.

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a>Karma bağlantı ve bir BizTalk hizmeti oluşturma
1. Web uygulaması dikey penceresinde tıklayın **tüm ayarları** > **ağ** > **karma bağlantı uç noktalarınızı yapılandırın**.
   
    ![Karma bağlantılar][CreateHCHCIcon]
2. Merhaba karma bağlantıları dikey penceresinde **Ekle**.
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. Merhaba **karma bağlantı ekleyin** dikey pencere açılır.  İlk karma bağlantınız olduğundan hello **yeni karma bağlantı** seçeneği önceden seçilmiştir ve hello **karma bağlantı oluşturmak** sizin için dikey pencere açılır.
   
    ![Karma bağlantı oluşturma][TwinCreateHCBlades]
   
    Merhaba üzerinde **oluşturma karma bağlantı dikey**:
   
   * İçin **adı**, hello bağlantı için bir ad sağlayın.
   * İçin **ana bilgisayar adı**, hello kaynağınız barındıran hello şirket içi bilgisayarın adını girin.
   * İçin **bağlantı noktası**, şirket içi kaynağa (1433 SQL Server varsayılan bir örnek için) kullandığı hello bağlantı noktası numarası girin.
   * Tıklatın **Biz konuşması hizmeti**
4. Merhaba **BizTalk hizmeti oluşturma** dikey pencere açılır. Merhaba BizTalk hizmeti için bir ad girin ve ardından **Tamam**.
   
    ![BizTalk hizmeti oluşturma][CreateHCCreateBTS]
   
    Merhaba **BizTalk hizmeti oluşturma** dikey penceresi kapanır ve toohello döndürülen **karma bağlantı oluşturmak** dikey.
5. Merhaba oluşturma karma bağlantı dikey penceresinde **Tamam**. 
   
    ![Tamam'ı tıklatın][CreateBTScomplete]
6. Merhaba işlemi tamamlandıktan sonra hello Portal bildirimleri alanında hello hello bağlantı başarıyla oluşturuldu bildirir.
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in hello dogfood portal. I switch toohello classic portal
    (full portal) and created hello BizTalk service but it doesn't seem toolet you connnect them - When you finish the
    Create hybrid conn step, you get hello following error
    Failed toocreate hybrid connection RelecIoudHC. hello 
    resource type could not be found in hello namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    hello error indicates it couldn't find hello type, not hello instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. Merhaba web uygulamanızın dikey penceresinde hello **karma bağlantılar** simgesi artık gösterir 1 karma bağlantı oluşturuldu.
   
    ![Oluşturulan bir karma bağlantı][CreateHCOneConnectionCreated]

Bu noktada, hello bulut karma bağlantı altyapı önemli bir kısmını tamamladınız. Ardından, karşılık gelen bir şirket içi parça oluşturur.

<a name="InstallHCM"></a>

## <a name="install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a>Merhaba şirket içi karma Bağlantı Yöneticisi toocomplete hello Bağlantısı'nı yükleme
1. Merhaba web uygulamanızın dikey penceresinde **tüm ayarları** > **ağ** > **karma bağlantı uç noktalarınızı yapılandırın**. 
   
    ![Karma bağlantıları simgesi][HCIcon]
2. Merhaba üzerinde **karma bağlantılar** dikey penceresinde, hello **durum** sütun hello için en son eklenen uç nokta gösterir **bağlı**. Merhaba bağlantı tooconfigure'ı tıklatın.
   
    ![Bağlı değil][NotConnected]
   
    Merhaba karma bağlantı dikey pencere açılır.
   
    ![NotConnectedBlade][NotConnectedBlade]
3. Merhaba dikey penceresinde **dinleyicisi Kur**.
   
    ![Dinleyici Kur'a tıklayın][ClickListenerSetup]
4. Merhaba **karma bağlantı özelliklerini** dikey pencere açılır. Altında **şirket içi karma Bağlantı Yöneticisi**, seçin **tooinstall burayı**.
   
    ![Tooinstall burayı tıklatın][ClickToInstallHCM]
5. Merhaba uygulamayı çalıştırmak Güvenlik Uyarısı iletişim kutusunda seçin **çalıştırmak** toocontinue.
   
    ![Çalışma toocontinue seçin][ApplicationRunWarning]
6. Merhaba, **kullanıcı hesabı denetimi** iletişim kutusunda, seçin **Evet**.
   
   ![Evet'i seçin][UAC]
7. Merhaba karma Bağlantı Yöneticisi'ni indirilen ve yüklenmiş. 
   
    ![Yükleme][HCMInstalling]
8. Merhaba yükleme tamamlandığında tıklayın **Kapat**.
   
    ![Kapat'ı tıklatın][HCMInstallComplete]
   
    Merhaba üzerinde **karma bağlantılar** dikey penceresinde, hello **durum** sütun şimdi gösterir **bağlı**. 
   
    ![Bağlı durumu][HCStatusConnected]

Bu hello karma bağlantı altyapı tamamlandı şimdi onu kullanan bir karma uygulama oluşturabilirsiniz. 

> [!NOTE]
> Merhaba aşağıdaki bölümler şunları nasıl yapacağınızı toouse Mobile Apps .NET arka uç projesi ile karma bağlantı.
> 
> 

## <a name="configure-hello-mobile-app-net-backend-project-tooconnect-toohello-sql-server-database"></a>Merhaba mobil uygulama .NET arka uç projesi tooconnect toohello SQL Server veritabanını Yapılandır
App Service'de Mobile Apps .NET arka uç projesi yalnızca ASP.NET web uygulamasını bir ek Mobile Apps yüklenmiş ve başlatılmış SDK'sı ' dir. toouse web uygulamanızı Mobile Apps arka uç olarak gerekir [indirin ve hello Mobile Apps .NET arka ucu SDK başlatma](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).  

Mobil uygulamalar için ayrıca hello şirket içi veritabanı için bir bağlantı dizesi toodefine gerekir ve hello arka uç toouse bu bağlantıyı değiştirmek. 

1. Visual Studio'da Aç hello Web.config dosyasında, mobil uygulama .NET arka ucu için Çözüm Gezgini'nde hello bulun **connectionStrings** bölümünde, yeni bir SqlClient giriş hangi noktaları toohello şirket içi SQL hello aşağıdaki gibi ekleyin: Veritabanı sunucusu:
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    Tooreplace unutmayın `<**secure_password**>` için oluşturduğunuz hello parola ile bu dizesinde *HybridConnectionLogin*.
2. Tıklatın **kaydetmek** Visual Studio toosave hello Web.config dosyasında.
   
   > [!NOTE]
   > Bu bağlantı ayarı hello yerel bilgisayarda çalışırken kullanılır. Azure üzerinde çalışırken, bu ayarı geçersiz kılınmadı hello Portalı'nda tanımlanan hello bağlantı ayarlayarak.
   > 
   > 
3. Merhaba genişletin **modelleri** klasörü ve biten açık hello veri modeli dosyası *Context.cs*.
4. Merhaba değiştirme **DbContext** örnek oluşturucusu toopass hello değeri `OnPremisesDBConnection` toohello temel **DbContext** oluşturucusu, aşağıdaki kod parçacığında benzer toohello:
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    Merhaba hizmeti şimdi hello yeni bağlantı toohello SQL Server veritabanı kullanır.

## <a name="update-hello-mobile-app-backend-toouse-hello-on-premises-connection-string"></a>Merhaba mobil uygulama arka uç toouse hello şirket içi bağlantı dizesi güncelleştir
Ardından, böylece Azure'dan kullanılabilir tooadd bir uygulama ayarı için bu yeni bağlantı dizesi gerekir.  

1. Merhaba edilene [Azure portal](https://portal.azure.com) mobil uygulamanızın hello web app arka uç kodu içini tıklatın **tüm ayarları**, ardından **uygulama ayarları**.
2. Merhaba, **Web uygulaması ayarları** dikey penceresinde çok ilerleyin**bağlantı dizeleri** ve yeni bir ekleyin **SQL Server** adlı bağlantı dizesi `OnPremisesDBConnection` gibibirdeğeresahip`Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.
   
    Değiştir `<**secure_password**>` şirket içi veritabanınız için hello güvenli parola ile.
   
    ![Şirket içi veritabanı için bağlantı dizesi](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. Tuşuna **kaydetmek** toosave hello karma bağlantı ve bağlantı dizesi, yeni oluşturduğunuz.

Bu noktada hello sunucu projesi yeniden yayımlamanız ve mevcut Mobile Apps istemcileriniz ile Merhaba yeni bağlantı sınayın. Veri okuma ve hello karma bağlantıyı kullanarak toohello şirket içi veritabanına yazılır.

<a name="NextSteps"></a>

## <a name="next-steps"></a>Sonraki Adımlar
* Karma bağlantı kullanan bir ASP.NET web uygulaması oluşturma hakkında daha fazla bilgi için bkz: [Bağlan tooan şirket içi SQL Server bir Azure web karma bağlantılar kullanarak sitesinden](http://go.microsoft.com/fwlink/?LinkID=397979). 

### <a name="additional-resources"></a>Ek Kaynaklar
[Karma Bağlantılara genel bakış](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Karma bağlantılar (Channel 9 video) Josh geçiş sunar](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[Karma bağlantılar web sitesi](https://azure.microsoft.com/services/biztalk-services/)

[BizTalk Services: Pano, İzleyici, Ölçek, yapılandırma ve karma bağlantı sekmeleri](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[Gerçek dünya karma bir buluta sorunsuz uygulama taşıma (Channel 9 video) ile oluşturma](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[Connect tooan şirket içi karma bağlantılar (Channel 9 video) kullanarak Azure Mobile Services SQL Server'dan](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[New]:./media/web-sites-hybrid-connection-get-started/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-get-started/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-get-started/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-get-started/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-get-started/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-get-started/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-get-started/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-get-started/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-get-started/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-get-started/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-get-started/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-get-started/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-get-started/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-get-started/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-get-started/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-get-started/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-get-started/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-get-started/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-get-started/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-get-started/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-get-started/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-get-started/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-get-started/D10HCStatusConnected.png
