---
title: "Karma bağlantılar kullanarak Azure App Service web uygulamasından şirket içi SQL Server'a bağlanma"
description: "Microsoft Azure üzerinde bir web uygulaması oluşturma ve bir şirket içi SQL Server veritabanına bağlan"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 2b4e0539-1a0b-4aa1-8a69-b4b053c3b2e5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: cephalin
ms.openlocfilehash: 12456ef3e2aecfa7a03cca97de2ff6ffd9602357
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a>Karma bağlantılar kullanarak Azure App Service web uygulamasından şirket içi SQL Server'a bağlanma
Karma bağlantılar bağlanabilir [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web uygulamaları için statik bir TCP bağlantı noktası kullanan şirket içi kaynakları. Desteklenen kaynaklar Microsoft SQL Server, MySQL, HTTP Web API'leri, uygulama hizmeti ve birçok özel Web hizmeti içerir.

Bu öğreticide, bir App Service web uygulamasının nasıl oluşturulacağını öğreneceksiniz [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), web uygulamasının yeni karma bağlantı özelliğini kullanarak, yerel şirket içi SQL Server veritabanına bağlanmak, karma bağlantıyı kullan ve App Service web uygulaması uygulamayı dağıtmak basit bir ASP.NET uygulaması oluşturun. Azure tamamlanan web uygulamasında kullanıcı kimlik bilgilerini şirket içi bir üyelik veritabanında depolar. Öğretici, Azure veya ASP.NET kullanma konusunda deneyim varsayar.

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin. Kredi kartı ve taahhüt gerekmez.
> 
> Web uygulamalarının karma bağlantılar özelliği yalnızca bölümüdür [Azure Portal](https://portal.azure.com). BizTalk Services'da bir bağlantı oluşturmak için bkz: [karma bağlantılar](http://go.microsoft.com/fwlink/p/?LinkID=397274).  
> 
> 

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiyi tamamlamak için aşağıdaki ürünler gerekir. Azure için tamamen ücretsiz geliştirme başlatabilmeniz tüm boş sürümlerinde kullanılabilir.

* **Azure aboneliği** - ücretsiz bir abonelik için bkz: [Azure ücretsiz deneme sürümü](/pricing/free-trial/).
* **Visual Studio 2013** - Visual Studio 2013 ücretsiz bir deneme sürümünü karşıdan yüklemek için bkz: [Visual Studio indirmeleri](http://www.visualstudio.com/downloads/download-visual-studio-vs). Bu, devam etmeden önce yükleyin.
* **Microsoft .NET Framework 3.5 Service Pack 1** -işletim sisteminiz Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 veya Windows Server 2008 R2 ise, bu Denetim Masası'nda etkinleştirebilirsiniz > Programlar ve Özellikler > kapatma Windows özelliklerini aç veya kapat. Aksi takdirde, buradan indirebilirsiniz [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).
* **SQL Server 2014 Express araçları ile** -Microsoft SQL Server Express, ücretsiz indirme [Microsoft Web Platformu veritabanı sayfası](http://www.microsoft.com/web/platform/database.aspx). Seçin **Express** (yerel veritabanı değil) sürümü. **Araçlarıyla Express** sürüm, bu öğreticide kullanacağı SQL Server Management Studio içerir.
* **SQL Server Management Studio Express** - yukarıda belirtilen araçları indirme ile SQL Server 2014 Express ile dahil, ancak ayrı olarak yüklemeniz gerekiyorsa, indirin ve şuradan yükleyin [SQL Server Express indirme sayfası](http://www.microsoft.com/web/platform/database.aspx).

Öğretici, Visual Studio 2013 yüklediyseniz ve yüklenmemiş veya .NET Framework 3.5 etkin bir Azure aboneliğine sahip olduğunuzu varsayar. Öğretici Azure karma bağlantılar özelliği (varsayılan bir örnek ile statik bir TCP bağlantı noktası) ile iyi çalışır bir yapılandırmasında SQL Server 2014 Express yükleme gösterir. Öğretici başlamadan önce SQL Server 2014 Express araçları ile SQL Server yüklü yoksa, yukarıda belirtilen konumdan indirin.

### <a name="notes"></a>Notlar
Bir şirket içi SQL Server veya SQL Server Express veritabanı ile karma bağlantı kullanmak için TCP/IP'yi statik bağlantı noktasına etkinleştirilmesi gerekir. Adlandırılmış örneklerin yapılamaz SQL Server'da varsayılan örnekleri statik bağlantı noktası 1433 kullanın.

Şirket içi karma Bağlantı Yöneticisi Aracı yüklediğiniz bilgisayar:

* Azure giden bağlantısı üzerinden olması gerekir:

| Bağlantı noktası | Neden |
| --- | --- |
| 80 |**Gerekli** sertifika doğrulama ve isteğe bağlı olarak veri bağlantısı için HTTP bağlantı noktası. |
| 443 |**İsteğe bağlı** veri bağlantısı için. TCP bağlantı noktası 80, 443 giden bağlantı kullanılamıyorsa, kullanılır. |
| 5671 ve 9352 |**Önerilen** ancak veri bağlantısı için isteğe bağlı. Bu mod genellikle daha yüksek verimlilik verir unutmayın. Bu bağlantı noktalarına giden bağlantı kullanılamıyorsa, TCP bağlantı noktası 443 kullanılır. |

* Ulaşabilmesi olmalıdır *ana bilgisayar adı*:*BağlantıNoktasıNumarası* , şirket içi kaynak.

Bu makaledeki adımları, şirket içi karma Bağlantı Aracısı'nı barındıracak bilgisayarı tarayıcıdan kullandığınızı varsayar.

Bir yapılandırma ve yukarıda açıklanan koşullara uyan bir ortamda yüklü SQL Server zaten varsa, İleri atlayabilirsiniz ve başlayın [şirket içi SQL Server veritabanı oluşturma](#CreateSQLDB).

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a>A. SQL Server Express'i yüklemek, TCP/IP'yi etkinleştirin ve şirket içi SQL Server veritabanı oluşturma
Bu bölümde SQL Server Express'i yüklemek, TCP/IP'yi etkinleştirin ve böylece, web uygulamanızın Azure Portal ile çalışacak bir veritabanı oluşturmak nasıl gösterir.

### <a name="install-sql-server-express"></a>SQL Server Express'i Yükleme
1. SQL Server Express'i yüklemek için **SQLEXPRWT_x64_ENU.exe** veya **SQLEXPR_x86_ENU.exe** indirdiğiniz dosya. SQL Server Yükleme Merkezi'ni Sihirbazı görünür.
   
    ![SQL Server yükleme][SQLServerInstall]
2. Seçin **yeni SQL Server tek başına yükleme veya mevcut bir yüklemeye özellikler ekleme**. İçin elde edene kadar varsayılan seçenekleri ve ayarları, kabul etme yönergeleri izleyerek **örnek Yapılandırması** sayfası.
3. Üzerinde **örnek Yapılandırması** sayfasında, **varsayılan örnek**.
   
    ![Varsayılan bir örnek seçin][ChooseDefaultInstance]
   
    Varsayılan olarak, SQL Server'ın varsayılan örneğinin statik bağlantı noktası 1433, SQL Server istemcilerinden gelen istekleri ne karma bağlantılar özellik gerektirir olduğu dinler. Karma bağlantılar tarafından desteklenmeyen dinamik bağlantı noktaları ve UDP, adlandırılmış örnekleri kullanın.
4. Varsayılanları kabul **sunucu yapılandırması** sayfası.
5. Üzerinde **veritabanı altyapısı Yapılandırması** sayfasında **kimlik doğrulama modu**, seçin **karma mod (SQL Server kimlik doğrulaması ve Windows kimlik doğrulaması)**ve bir parola belirtin.
   
    ![Karma mod seçin][ChooseMixedMode]
   
    Bu öğreticide, SQL Server kimlik doğrulamasını kullanır. Daha sonra ihtiyacınız olacak çünkü sağlarsanız, parolayı anımsa emin olun.
6. Yüklemeyi tamamlamak için Sihirbazı'nı kullanılmadıkları adım.

### <a name="enable-tcpip"></a>TCP/IP'yi etkinleştirin
TCP/IP'yi etkinleştirmek için SQL Server Express yüklendiğinde, yüklü olduğu SQL Server Configuration Manager kullanır. Adımları [SQL Server TCP/IP ağ protokolünü etkinleştirin](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) devam etmeden önce.

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a>Şirket içi SQL Server veritabanı oluşturma
Visual Studio web uygulamanızı Azure tarafından erişilebilir bir üyelik veritabanı gerektirir. Bu bir SQL Server veya SQL Server Express veritabanı (varsayılan olarak MVC şablonu kullanan LocalDB veritabanı değil), gerektirir üyelik veritabanının sonraki oluşturmanız.

1. SQL Server Management Studio'da yalnızca yüklü olan SQL Server bağlayın. (Varsa **sunucuya Bağlan** iletişim otomatik olarak görünmez, gitmek **Object Explorer** sol bölmede **Bağlan**ve ardından **veritabanı altyapısı**.) ![Sunucuya Bağlan][SSMSConnectToServer]
   
    İçin **sunucu türü**, seçin **veritabanı altyapısı**. İçin **sunucu adı**, kullanabileceğiniz **localhost** veya kullanmakta olduğunuz bilgisayarın adı. Seçin **SQL Server kimlik doğrulaması**ve ardından sa kullanıcı adını ve daha önce oluşturduğunuz parola ile oturum açın.
2. SQL Server Management Studio'yu kullanarak yeni bir veritabanı oluşturmak için sağ **veritabanları** , Nesne Gezgini ve ardından **yeni veritabanı**.
   
    ![Yeni veritabanı oluştur][SSMScreateNewDB]
3. İçinde **yeni veritabanı** iletişim kutusunda, MembershipDB veritabanı adını girin ve ardından **Tamam**.
   
    ![Veritabanı adı girin][SSMSprovideDBname]
   
    Veritabanına bu noktada değişiklik yok olduğunu unutmayın. Çalıştırdığınızda, web uygulamanız tarafından üyelik bilgilerini daha sonra otomatik olarak eklenir.
4. Nesne Gezgini'nde, genişletirseniz, **veritabanları**, üyelik veritabanının oluşturulduğunu görürsünüz.
   
    ![Oluşturulan MembershipDB][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-the-azure-portal"></a>B. Azure Portalı'nda bir web uygulaması oluşturma
> [!NOTE]
> Bu öğretici için kullanmak istediğiniz Azure Portalı'nda bir web uygulaması zaten oluşturduysanız, atlayabilirsiniz [karma bağlantı ve bir BizTalk hizmeti oluşturma](#CreateHC) ve buradan devam edin.
> 
> 

1. İçinde [Azure Portal](https://portal.azure.com), tıklatın **yeni** > **Web + mobil** > **Web uygulaması**.
   
    ![Yeni düğmesi][New]
2. Web Uygulamanızı yapılandırmak ve ardından **oluşturma**.
   
    ![Web sitesi adı][WebsiteCreationBlade]
3. Birkaç dakika sonra web uygulaması oluşturuldu ve kendi web uygulaması dikey penceresi görünür. Dikey web uygulamanızı yönetmenizi sağlayan bir dikey olarak kaydırılabilir Pano ' dir.
   
    ![Çalışan Web sitesi][WebSiteRunningBlade]
   
    Web uygulaması Canlı doğrulamak için tıklayabilirsiniz **Gözat** varsayılan sayfasını görüntülemek için simge.

Ardından, karma bir bağlantı ve web uygulaması BizTalk hizmeti oluşturur.

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a>C. Karma bağlantı ve bir BizTalk hizmeti oluşturma
1. Geri Portalı'nda Ayarlar'a gidip tıklayın **ağ** > **karma bağlantı uç noktalarınızı yapılandırın**.
   
    ![Karma bağlantılar][CreateHCHCIcon]
2. Karma bağlantılar dikey penceresinde **Ekle** > **yeni karma bağlantı**.
3. Üzerinde **karma bağlantı oluşturmak** dikey penceresinde:
   
   * İçin **adı**, bağlantı için bir ad sağlayın.
   * İçin **ana bilgisayar adı**, SQL Server ana bilgisayarınız bilgisayar adını girin.
   * İçin **bağlantı noktası**, 1433 (varsayılan bağlantı noktası için SQL Server) girin.
   * Tıklatın **BizTalk hizmeti** > **yeni BizTalk hizmeti** ve BizTalk hizmeti için bir ad girin.
     
     ![Karma bağlantı oluşturma][TwinCreateHCBlades]
4. Tıklatın **Tamam** iki kez.
   
    İşlem tamamlandığında **bildirimleri** alanı yeşil flash **başarı** ve **karma bağlantı** dikey durumundaki yeni karma bağlantıyı gösterir **bağlı**.
   
    ![Oluşturulan bir karma bağlantı][CreateHCOneConnectionCreated]

Bu noktada, bulut karma bağlantı altyapı önemli bir kısmını tamamladınız. Ardından, karşılık gelen bir şirket içi parça oluşturur.

<a name="InstallHCM"></a>

## <a name="d-install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a>D. Bağlantıyı tamamlamak için şirket içi karma Bağlantı Yöneticisi'ni yükleyin
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

Karma bağlantı altyapı tamamlandığına göre bunu kullanan bir web uygulaması oluşturacaksınız.

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-the-database-connection-string-and-run-the-project-locally"></a>E. Temel bir ASP.NET web projesi oluşturun, veritabanı bağlantı dizesini düzenlemek ve projeyi yerel olarak çalıştırın
### <a name="create-a-basic-aspnet-project"></a>Temel bir ASP.NET projesi oluşturma
1. Visual Studio'da üzerinde **dosya** menüsünde yeni bir proje oluşturun:
   
    ![Yeni Visual Studio projesi][HCVSNewProject]
2. İçinde **şablonları** bölümünü **yeni proje** iletişim kutusunda **Web** ve **ASP.NET Web uygulaması**ve ardından **Tamam**.
   
    ![ASP.NET Web uygulaması seçin][HCVSChooseASPNET]
3. İçinde **yeni ASP.NET projesi** iletişim kutusunda, seçin **MVC**ve ardından **Tamam**.
   
    ![MVC seçin][HCVSChooseMVC]
4. Proje oluşturduğunuzda uygulama Benioku sayfası görüntülenir. Web projesinin henüz çalıştırmayın.
   
    ![Benioku sayfası][HCVSReadmePage]

### <a name="edit-the-database-connection-string-for-the-application"></a>Uygulama için veritabanı bağlantı dizesini Düzenle
Bu adımda, uygulamanızın yerel SQL Server Express veritabanınızın nerede bulacağını bildirir bağlantı dizesini düzenleyin. Uygulama yapılandırma bilgilerini içeren uygulamanın Web.config dosyasında bağlantı dizesidir.

> [!NOTE]
> Uygulamanızı SQL Server Express ve olanı değil, Visual Studio'nun varsayılan yerel veritabanı oluşturulan veritabanı kullandığından emin olmak için projenizi çalıştırmadan önce bu adımı tamamlamak önemlidir.
> 
> 

1. Çözüm Gezgini'nde, Web.config dosyasını çift tıklatın.
   
    ![Web.config][HCVSChooseWebConfig]
2. Düzen **connectionStrings** bölümü aşağıdaki söz dizimini aşağıdaki örnekte, yerel makinenizde SQL Server veritabanına işaret etmek için:
   
    ![Bağlantı dizesi][HCVSConnectionString]
   
    Bağlantı dizesi oluştururken aşağıdakileri unutmayın:
   
   * Varsayılan örneği (örneğin, Sunucunuz\\sqlexpress) yerine adlandırılmış bir örneğine bağlanıyorsanız, SQL Server statik bağlantı noktalarını kullanacak şekilde yapılandırmanız gerekir. Statik bağlantı noktalarını yapılandırma hakkında daha fazla bilgi için bkz: [SQL Server'ın belirli bir bağlantı noktasında dinleyecek şekilde yapılandırma konusunda](http://support.microsoft.com/kb/823938). Varsayılan olarak, adlandırılmış örnekleri UDP ve karma bağlantılar tarafından desteklenmeyen dinamik bağlantı noktaları kullanır.
   * Önerilen bağlantı noktasını belirtin (varsayılan olarak örnekte gösterildiği gibi 1433) bağlantı dizesi, emin olabilir yerel SQL Server'ınızdaki sahip etkin TCP ve doğru bağlantı noktası kullanıyordur.
   * SQL Server kimlik doğrulaması bağlanmak için kullanılacak bağlantı dizenizi kullanıcı kimliği ve parola belirterek unutmayın.
3. Tıklatın **kaydetmek** Web.config dosyasını kaydetmek için Visual Studio'da.

### <a name="run-the-project-locally-and-register-a-new-user"></a>Projeyi yerel olarak çalıştırın ve yeni bir kullanıcı kaydı
1. Artık, yeni web projeniz yerel olarak hata ayıklama altında Gözat düğmesine tıklayarak çalıştırın. Bu örnek, Internet Explorer kullanır.
   
    ![Projeyi çalıştırın][HCVSRunProject]
2. Sağ üst tarafındaki varsayılan web sayfası üzerinde seçin **kaydetmek** yeni bir hesap kaydetmek için:
   
    ![Yeni bir hesap Kaydet][HCVSRegisterLocally]
3. Bir kullanıcı adı ve parola girin:
   
    ![Kullanıcı adı ve parola girin][HCVSCreateNewAccount]
   
    Bu otomatik olarak bir veritabanı uygulamanız için üyelik bilgilerini tutan yerel SQL Server üzerinde oluşturur. Tablolardan birini (**dbo. AspNetUsers**) ayrı tutma web uygulama kullanıcı kimlik bilgilerini girdiğiniz ayarlara benzer. Öğreticide daha sonra bu tabloyu görürsünüz.
4. Varsayılan web sayfasının tarayıcı penceresini kapatın. Bu, Visual Studio uygulamasında durdurur.

Şimdi uygulamayı Azure'a yayımlama ve test için sonraki adıma hazır olursunuz.

<a name="PubNTest"></a>

## <a name="f-publish-the-web-application-to-azure-and-test-it"></a>F Azure web uygulamasına yayımlamak ve test
Artık uygulamanızı App Service web uygulaması yayımlama ve web uygulamanızı yerel makinenizde veritabanına bağlanmak için daha önce yapılandırılmış karma bağlantı'nın nasıl kullanıldığını görmek için test.

### <a name="publish-the-web-application"></a>Web uygulaması yayımlama
1. Yayımlama profilinizi Azure Portalı'nda App Service web uygulaması için yükleyebilirsiniz. Web uygulamanız için dikey penceresinde **Get yayımlama profili**ve ardından dosyayı bilgisayarınıza kaydedin.
   
    ![Yayım profili indirin][PortalDownloadPublishProfile]
   
    Ardından, Visual Studio web uygulamanıza bu dosyayı içeri aktaracak.
2. Visual Studio'daki Çözüm Gezgini'nde proje adına sağ tıklayın ve seçin **Yayımla**.
   
    ![Select yayımlama][HCVSRightClickProjectSelectPublish]
3. İçinde **Web'i Yayımla** iletişim, **profil** sekmesinde, seçin **alma**.
   
    ![İçeri Aktarma][HCVSPublishWebDialogImport]
4. İndirilen yayımlama profiline göz atın, onu seçin ve ardından **Tamam**.
   
    ![Profiline göz atın][HCVSBrowseToImportPubProfile]
5. Yayımlama bilgilerinizi içe aktarılır ve görüntüler **bağlantı** iletişim kutusunun sekmesi.
   
    ![Yayınla'yı tıklatın][HCVSClickPublish]
   
    **Yayımla**’ta tıklayın.
   
    Yayımlama tamamlandığında tarayıcınızı başlatın ve şimdi bunu Azure bulutunda dinamik olması dışında şimdi bilinen ASP.NET uygulamanızın--Göster!

Ardından, uygulamada karma bağlantısını görmek için canlı web uygulamanızı kullanır.

### <a name="test-the-completed-web-application-on-azure"></a>Azure üzerinde tamamlanan web uygulamasını test
1. Üst kısmında, web sayfasının sağ Azure üzerinde seçin **oturum**.
   
    ![Test oturum açma][HCTestLogIn]
2. App Service web uygulaması, web uygulamanızın üyelik veritabanının yerel makinenizde şimdi bağlı. Bunu doğrulamak için daha önce girdiğiniz yerel veritabanında aynı kimlik bilgileriyle oturum açın.
   
    ![Merhaba Karşılama][HCTestHelloContoso]
3. Daha fazla yeni karma bağlantınızı sınamak için Azure web uygulamanızın dışına oturum ve başka bir kullanıcı olarak kaydedin. Yeni bir kullanıcı adı ve parolasını girin ve ardından **kaydetmek**.
   
    ![Test başka bir kullanıcı kaydetme][HCTestRegisterRelecloud]
4. Yeni kullanıcının kimlik bilgilerini yerel veritabanınızda karma bağlantınız üzerinden depolanmıştı doğrulamak için yerel bilgisayarınızda SQL Management Studio'yu açın. Nesne Gezgini'nde genişletin **MembershipDB** veritabanı ve ardından **tabloları**. Sağ **dbo. AspNetUsers** üyelik tablosunda ve seçin **ilk 1000 satırı Seç** sonuçları görüntülemek için.
   
    ![Sonuçları görüntüleme][HCTestSSMSTree]
5. Yerel üyelik tablonuz şimdi her iki hesap - yerel olarak oluşturulan ve Azure bulutta oluşturulan bir gösterir. Bulutta oluşturulan bir Azure'nın karma bağlantı özelliği aracılığıyla şirket içi veritabanına kaydedildi.
   
    ![Şirket içi veritabanında kayıtlı kullanıcılar][HCTestShowMemberDb]

Artık oluşturduğunuz ve bir web uygulaması Azure bulutta ve şirket içi SQL Server veritabanı arasında bir karma bağlantı kullanan bir ASP.NET web uygulaması dağıtılmış. Tebrikler!

## <a name="see-also"></a>Ayrıca Bkz.
[Karma Bağlantılara genel bakış](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Karma bağlantılar (Channel 9 video) Josh geçiş sunar](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[Karma Bağlantılara genel bakış](/services/biztalk-services/)

[BizTalk Services: Pano, İzleyici, Ölçek, yapılandırma ve karma bağlantı sekmeleri](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[Gerçek dünya karma bir buluta sorunsuz uygulama taşıma (Channel 9 video) ile oluşturma](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[Azure App Service içinde karma bağlantılar kullanarak şirket kaynaklarına erişmek](web-sites-hybrid-connection-get-started.md)

[ASP.NET Kimliği'ne genel bakış](http://www.asp.net/identity)

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- IMAGES -->
[SQLServerInstall]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A01SQLServerInstall.png
[ChooseDefaultInstance]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A02ChooseDefaultInstance.png
[ChooseMixedMode]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A03ChooseMixedMode.png
[SSMSConnectToServer]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A04SSMSConnectToServer.png
[SSMScreateNewDB]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A05SSMScreateNewDBlh.png
[SSMSprovideDBname]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A06SSMSprovideDBname.png
[SSMSMembershipDBCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A07SSMSMembershipDBCreated.png
[New]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D10HCStatusConnected.png
[HCVSNewProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E01HCVSNewProject.png
[HCVSChooseASPNET]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E02HCVSChooseASPNET.png
[HCVSChooseMVC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E03HCVSChooseMVC.png
[HCVSReadmePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E04HCVSReadmePage.png
[HCVSChooseWebConfig]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E05HCVSChooseWebConfig.png
[HCVSConnectionString]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSConnectionString.png
[HCVSRunProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSRunProject.png
[HCVSRegisterLocally]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E07HCVSRegisterLocally.png
[HCVSCreateNewAccount]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E08HCVSCreateNewAccount.png
[PortalDownloadPublishProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F01PortalDownloadPublishProfile.png
[HCVSPublishProfileInDownloadsFolder]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F02HCVSPublishProfileInDownloadsFolder.png
[HCVSRightClickProjectSelectPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F03HCVSRightClickProjectSelectPublish.png
[HCVSPublishWebDialogImport]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F04HCVSPublishWebDialogImport.png
[HCVSBrowseToImportPubProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F05HCVSBrowseToImportPubProfile.png
[HCVSClickPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F06HCVSClickPublish.png
[HCTestLogIn]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F07HCTestLogIn.png
[HCTestHelloContoso]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F08HCTestHelloContoso.png
[HCTestRegisterRelecloud]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F09HCTestRegisterRelecloud.png
[HCTestSSMSTree]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F10HCTestSSMSTree.png
[HCTestShowMemberDb]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F11HCTestShowMemberDb.png
