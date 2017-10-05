---
title: "Azure Uygulama Hizmeti’nde karma bağlantıları kullanarak şirket içi kaynaklara erişme"
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
ms.openlocfilehash: fbd22e6e285c5ddaef2a473671d4a06a97384b4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a>Azure Uygulama Hizmeti’nde karma bağlantıları kullanarak şirket içi kaynaklara erişme
Azure App Service uygulama SQL Server, MySQL, HTTP Web API'leri ve birçok özel Web hizmeti gibi statik TCP bağlantı kullanan şirket içi kaynaklara bağlanabilir. Bu makale App Service ve bir şirket içi SQL Server veritabanı arasında bir karma bağlantı oluşturulacağını gösterir.

> [!NOTE]
> Web uygulamalarının karma bağlantılar özelliği yalnızca bölümüdür [Azure Portal](https://portal.azure.com). BizTalk Services'da bir bağlantı oluşturmak için bkz: [karma bağlantılar](http://go.microsoft.com/fwlink/p/?LinkID=397274). 
> 
> Bu içerik, Azure App Service'de Mobile Apps için de geçerlidir. 
> 
> 

## <a name="prerequisites"></a>Ön koşullar
* Azure aboneliği. Ücretsiz bir abonelik için bkz: [Azure ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/). 
  
    Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin. Kredi kartı ve taahhüt gerekmez.
* Bir şirket içi SQL Server veya SQL Server Express veritabanı ile karma bağlantı kullanmak için TCP/IP'yi statik bağlantı noktasına etkinleştirilmesi gerekir. Statik bağlantı noktası 1433 kullandığından, varsayılan bir örnek SQL Server üzerinde kullanılması önerilir. Yükleme ve karma bağlantılar ile kullanmak için SQL Server Express yapılandırma hakkında daha fazla bilgi için bkz: [karma bağlantılar kullanarak bir Azure web sitesinden bir şirket içi SQL Server'a Bağlan](http://go.microsoft.com/fwlink/?LinkID=397979).
* Bilgisayar üzerinde bu makalenin sonraki bölümlerinde açıklanan şirket içi karma Bağlantı Yöneticisi aracısı yükleyin:
  
  * Azure için bağlantı noktası 5671 üzerinden bağlanabilmesi gerekir
  * Ulaşabilmesi olmalıdır *ana bilgisayar adı*:*BağlantıNoktasıNumarası* , şirket içi kaynak. 

> [!NOTE]
> Bu makaledeki adımları, şirket içi karma Bağlantı Aracısı'nı barındıracak bilgisayarı tarayıcıdan kullandığınızı varsayar.
> 
> 

## <a name="create-a-web-app-in-the-azure-portal"></a>Azure Portalı'nda bir web uygulaması oluşturma
> [!NOTE]
> Bu öğretici için kullanmak istediğiniz Azure Portalı'nda bir web uygulaması veya mobil uygulama arka ucu zaten oluşturmuş durumdaysanız, atlayabilirsiniz [karma bağlantı ve bir BizTalk hizmeti oluşturma](#CreateHC) ve buradan başlayın.
> 
> 

1. Sol üst köşesindeki [Azure Portal](https://portal.azure.com), tıklatın **yeni** > **Web + mobil** > **Web uygulaması**.
   
    ![Yeni web uygulaması][NewWebsite]
2. Üzerinde **Web uygulaması** dikey penceresinde, bir URL sağlayın ve tıklatın **oluşturma**. 
   
    ![Web sitesi adı][WebsiteCreationBlade]
3. Birkaç dakika sonra web uygulaması oluşturuldu ve kendi web uygulaması dikey penceresi görünür. Dikey sitenizi yönetmenize olanak sağlayan bir dikey olarak kaydırılabilir Pano ' dir.
   
    ![Çalışan Web sitesi][WebSiteRunningBlade]
4. Site Canlı doğrulamak için tıklayabilirsiniz **Gözat** varsayılan sayfasını görüntülemek için simge.
   
    ![Web uygulamanızı görmek için Gözat'ı tıklatın][Browse]
   
    ![Varsayılan web uygulama sayfası][DefaultWebSitePage]

Ardından, karma bir bağlantı ve web uygulaması BizTalk hizmeti oluşturur.

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a>Karma bağlantı ve bir BizTalk hizmeti oluşturma
1. Web uygulaması dikey penceresinde tıklayın **tüm ayarları** > **ağ** > **karma bağlantı uç noktalarınızı yapılandırın**.
   
    ![Karma bağlantılar][CreateHCHCIcon]
2. Karma bağlantılar dikey penceresinde **Ekle**.
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. **Karma bağlantı ekleyin** dikey pencere açılır.  Bu ilk karma bağlantınız olduğundan **yeni karma bağlantı** seçeneği seçilmiş ve **karma bağlantı oluşturmak** sizin için dikey pencere açılır.
   
    ![Karma bağlantı oluşturma][TwinCreateHCBlades]
   
    Üzerinde **oluşturma karma bağlantı dikey**:
   
   * İçin **adı**, bağlantı için bir ad sağlayın.
   * İçin **ana bilgisayar adı**, kaynağınızın barındıran şirket içi bilgisayarın adını girin.
   * İçin **bağlantı noktası**, şirket içi kaynağa (1433 SQL Server varsayılan bir örnek için) kullandığı bağlantı noktası numarası girin.
   * Tıklatın **Biz konuşması hizmeti**
4. **BizTalk hizmeti oluşturma** dikey pencere açılır. BizTalk hizmeti için bir ad girin ve ardından **Tamam**.
   
    ![BizTalk hizmeti oluşturma][CreateHCCreateBTS]
   
    **BizTalk hizmeti oluşturma** dikey penceresi kapanır ve döndürülürsünüz **karma bağlantı oluşturmak** dikey.
5. Create karma bağlantı dikey penceresinde **Tamam**. 
   
    ![Tamam'ı tıklatın][CreateBTScomplete]
6. İşlem tamamlandığında, Portal bildirimleri alanında bağlantı başarıyla oluşturuldu bildirir.
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in the dogfood portal. I switch to the classic portal
    (full portal) and created the BizTalk service but it doesn't seem to let you connnect them - When you finish the
    Create hybrid conn step, you get the following error
    Failed to create hybrid connection RelecIoudHC. The 
    resource type could not be found in the namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    The error indicates it couldn't find the type, not the instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. Web uygulamanızın dikey penceresinde, **karma bağlantılar** simgesi artık gösterir 1 karma bağlantı oluşturuldu.
   
    ![Oluşturulan bir karma bağlantı][CreateHCOneConnectionCreated]

Bu noktada, bulut karma bağlantı altyapı önemli bir kısmını tamamladınız. Ardından, karşılık gelen bir şirket içi parça oluşturur.

<a name="InstallHCM"></a>

## <a name="install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a>Bağlantıyı tamamlamak için şirket içi karma Bağlantı Yöneticisi'ni yükleyin
1. Web uygulamanızın dikey penceresinde **tüm ayarları** > **ağ** > **karma bağlantı uç noktalarınızı yapılandırın**. 
   
    ![Karma bağlantıları simgesi][HCIcon]
2. Üzerinde **karma bağlantılar** dikey penceresinde **durum** sütun için en son eklenen uç nokta gösterir **bağlı**. Yapılandırmak için bağlantıyı tıklatın.
   
    ![Bağlı değil][NotConnected]
   
    Karma bağlantı dikey pencere açılır.
   
    ![NotConnectedBlade][NotConnectedBlade]
3. Dikey penceresinde **dinleyicisi Kur**.
   
    ![Dinleyici Kur'a tıklayın][ClickListenerSetup]
4. **Karma bağlantı özelliklerini** dikey pencere açılır. Altında **şirket içi karma Bağlantı Yöneticisi**, seçin **yüklemek için burayı tıklatın**.
   
    ![Yüklemek için burayı tıklatın][ClickToInstallHCM]
5. Uygulamayı çalıştırmak Güvenlik Uyarısı iletişim kutusunda seçin **çalıştırmak** devam etmek için.
   
    ![Devam etmek için Çalıştır'ı seçin][ApplicationRunWarning]
6. İçinde **kullanıcı hesabı denetimi** iletişim kutusunda, seçin **Evet**.
   
   ![Evet'i seçin][UAC]
7. Karma Bağlantı Yöneticisi'ni indirilen ve yüklenmiş. 
   
    ![Yükleme][HCMInstalling]
8. Yükleme tamamlandığında tıklayın **Kapat**.
   
    ![Kapat'ı tıklatın][HCMInstallComplete]
   
    Üzerinde **karma bağlantılar** dikey penceresinde **durum** sütun şimdi gösterir **bağlı**. 
   
    ![Bağlı durumu][HCStatusConnected]

Karma bağlantı altyapı tamamlandığına göre bunu kullanan bir karma uygulama oluşturabilirsiniz. 

> [!NOTE]
> Aşağıdaki bölümlerde, Mobile Apps .NET arka uç projesi ile karma bağlantı kullanmayı gösterir.
> 
> 

## <a name="configure-the-mobile-app-net-backend-project-to-connect-to-the-sql-server-database"></a>SQL Server veritabanına bağlanmak için mobil uygulama .NET arka uç projesini yapılandırma
App Service'de Mobile Apps .NET arka uç projesi yalnızca ASP.NET web uygulamasını bir ek Mobile Apps yüklenmiş ve başlatılmış SDK'sı ' dir. Web uygulamanızı Mobile Apps arka ucu olarak kullanmak için şunları yapmalısınız [karşıdan yüklemek ve mobil uygulamaları .NET arka ucu SDK başlatma](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).  

Mobil uygulamalar için ayrıca şirket içi veritabanına bir bağlantı dizesi tanımlayın ve bu bağlantıyı kullanmak için arka uç değiştirmek gerekir. 

1. Visual Studio'da Çözüm Gezgini'nde, mobil uygulama .NET arka ucu için Web.config dosyasını açın, bulun **connectionStrings** bölümünde, yeni bir SqlClient giriş şirket içi SQL Server veritabanına işaret eden aşağıdaki gibi ekleyin:
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    Değiştirilecek unutmayın `<**secure_password**>` için oluşturduğunuz parola ile bu dizesinde *HybridConnectionLogin*.
2. Tıklatın **kaydetmek** Web.config dosyasını kaydetmek için Visual Studio'da.
   
   > [!NOTE]
   > Bu bağlantı ayarı, yerel bilgisayarda çalışırken kullanılır. Azure üzerinde çalışırken, bu ayarı geçersiz kılınmadı Portalı'nda tanımlanan bağlantı ayarlayarak.
   > 
   > 
3. Genişletme **modelleri** klasörü ve açık ile biten veri modeli dosyası *Context.cs*.
4. Değiştirme **DbContext** değeri geçirmek için örnek oluşturucusu `OnPremisesDBConnection` bankasına **DbContext** oluşturucusu, aşağıdaki kod parçacığını benzer:
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    Hizmeti artık yeni SQL Server veritabanına bağlantı kullanır.

## <a name="update-the-mobile-app-backend-to-use-the-on-premises-connection-string"></a>Şirket içi bağlantı dizesi kullanmak için mobil uygulama arka ucu güncelleştir
Ardından, böylece Azure'dan kullanılabilmesi için bu yeni bağlantı dizesi için bir uygulama ayarı eklemeniz gerekir.  

1. Geri [Azure portal](https://portal.azure.com) mobil uygulamanızın web app arka uç kodu içini tıklatın **tüm ayarları**, ardından **uygulama ayarları**.
2. İçinde **Web uygulaması ayarları** dikey penceresinde, aşağı kaydırın **bağlantı dizeleri** ve yeni bir ekleme **SQL Server** adlı bağlantı dizesi `OnPremisesDBConnection` gibi bir değerle `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.
   
    Değiştir `<**secure_password**>` şirket içi veritabanınız için güvenli parola ile.
   
    ![Şirket içi veritabanı için bağlantı dizesi](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. Tuşuna **kaydetmek** karma kaydetmek için bağlantı ve bağlantı, yeni oluşturduğunuz dize.

Bu noktada sunucu projesi yeniden yayımlamanız ve mevcut Mobile Apps istemcileriniz ile yeni bağlantıyı sınayın. Veri okuma ve karma bağlantıyı kullanarak şirket içi veritabanına yazılır.

<a name="NextSteps"></a>

## <a name="next-steps"></a>Sonraki Adımlar
* Karma bağlantı kullanan bir ASP.NET web uygulaması oluşturma hakkında daha fazla bilgi için bkz: [karma bağlantılar kullanarak bir Azure web sitesinden bir şirket içi SQL Server'a Bağlan](http://go.microsoft.com/fwlink/?LinkID=397979). 

### <a name="additional-resources"></a>Ek Kaynaklar
[Karma Bağlantılara genel bakış](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Karma bağlantılar (Channel 9 video) Josh geçiş sunar](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[Karma bağlantılar web sitesi](https://azure.microsoft.com/services/biztalk-services/)

[BizTalk Services: Pano, İzleyici, Ölçek, yapılandırma ve karma bağlantı sekmeleri](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[Gerçek dünya karma bir buluta sorunsuz uygulama taşıma (Channel 9 video) ile oluşturma](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[Azure Mobile Services karma bağlantılar (Channel 9 video) kullanarak bir şirket içi SQL Server'a bağlanma](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

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
