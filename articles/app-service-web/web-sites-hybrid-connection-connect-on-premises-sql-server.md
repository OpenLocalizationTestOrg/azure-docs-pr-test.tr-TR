---
title: "aaaConnect karma bağlantılar kullanarak Azure App Service web uygulamasından tooon içi SQL Server"
description: "Microsoft Azure üzerinde bir web uygulaması oluşturma ve tooan şirket içi SQL Server veritabanına bağlan"
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
ms.openlocfilehash: 2e8f8f7e0b9733cfb0433697615faba4358c6023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a>Karma bağlantılar kullanarak Azure App Service web uygulamasından tooon içi SQL Server'a bağlanma
Karma bağlantılar bağlanabilir [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) statik bir TCP bağlantı noktası kullanan Web uygulamaları tooon içi kaynakları. Desteklenen kaynaklar Microsoft SQL Server, MySQL, HTTP Web API'leri, uygulama hizmeti ve birçok özel Web hizmeti içerir.

Bu öğreticide, nasıl toocreate bir App Service web hello uygulamada öğreneceksiniz [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), hello yeni karma bağlantı özelliğini kullanarak hello web uygulama tooyour yerel şirket içi SQL Server veritabanına bağlanmak, basit bir ASP.NET oluşturma Merhaba karma bağlantıyı kullan ve hello uygulama toohello App Service web uygulaması dağıtma uygulama. Azure web uygulamasında tamamlandı hello kullanıcı kimlik bilgilerini şirket içi bir üyelik veritabanında depolar. Merhaba öğretici Azure veya ASP.NET kullanma konusunda deneyim varsayar.

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> Hello Web Apps bölümü hello karma bağlantılar özelliği yalnızca hello kullanılabilir [Azure Portal](https://portal.azure.com). toocreate BizTalk Services bağlantısında bkz [karma bağlantılar](http://go.microsoft.com/fwlink/p/?LinkID=397274).  
> 
> 

## <a name="prerequisites"></a>Ön koşullar
toocomplete Bu öğretici, ürünleri aşağıdaki hello gerekir. Azure için tamamen ücretsiz geliştirme başlatabilmeniz tüm boş sürümlerinde kullanılabilir.

* **Azure aboneliği** - ücretsiz bir abonelik için bkz: [Azure ücretsiz deneme sürümü](/pricing/free-trial/).
* **Visual Studio 2013** -Visual Studio 2013, ücretsiz bir deneme sürümünü toodownload bkz [Visual Studio indirmeleri](http://www.visualstudio.com/downloads/download-visual-studio-vs). Bu, devam etmeden önce yükleyin.
* **Microsoft .NET Framework 3.5 Service Pack 1** -işletim sisteminiz Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 veya Windows Server 2008 R2 ise, bu Denetim Masası'nda etkinleştirebilirsiniz > Programlar ve Özellikler > kapatma Windows özelliklerini aç veya kapat. Aksi durumda, hello indirebilirsiniz [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).
* **SQL Server 2014 Express araçları ile** -Microsoft SQL Server Express ücretsiz hello karşıdan [Microsoft Web Platformu veritabanı sayfası](http://www.microsoft.com/web/platform/database.aspx). Merhaba seçin **Express** (yerel veritabanı değil) sürümü. Merhaba **araçlarıyla Express** sürüm, bu öğreticide kullanacağı SQL Server Management Studio içerir.
* **SQL Server Management Studio Express** - yukarıda belirtilen araçları indirme ile Merhaba ile SQL Server 2014 Express dahil, ancak tooinstall gerekiyorsa, ayrı ayrı indirebilir ve hello yüklemek [SQL Server Express indirme sayfasının](http://www.microsoft.com/web/platform/database.aspx).

Başlangıç Öğreticisi, Visual Studio 2013 yüklediyseniz ve yüklenmemiş veya .NET Framework 3.5 etkin bir Azure aboneliğine sahip olduğunuzu varsayar. Merhaba öğretici nasıl tooinstall SQL Server 2014 Express iyi hello Azure karma bağlantılar ile çalışan bir yapılandırma özellik (varsayılan bir örnek statik bir TCP bağlantı noktası ile) gösterir. Merhaba öğreticiye başlamadan önce SQL Server 2014 Express araçları ile SQL Server yüklü yoksa, yukarıda belirtilen hello konumdan yükleyin.

### <a name="notes"></a>Notlar
toouse bir şirket içi SQL Server veya SQL Server Express veritabanı ile karma bağlantı, TCP/IP'yi statik bağlantı noktası üzerinde etkin toobe gerekir. Adlandırılmış örneklerin yapılamaz SQL Server'da varsayılan örnekleri statik bağlantı noktası 1433 kullanın.

Merhaba bilgisayar hello şirket içi karma Bağlantı Yöneticisi aracısı yükleyin:

* Giden bağlantı tooAzure üzerinden olması gerekir:

| Bağlantı noktası | Neden |
| --- | --- |
| 80 |**Gerekli** sertifika doğrulama ve isteğe bağlı olarak veri bağlantısı için HTTP bağlantı noktası. |
| 443 |**İsteğe bağlı** veri bağlantısı için. Giden bağlantı too443 kullanılamıyorsa, TCP bağlantı noktası 80 kullanılır. |
| 5671 ve 9352 |**Önerilen** ancak veri bağlantısı için isteğe bağlı. Bu mod genellikle daha yüksek verimlilik verir unutmayın. TCP bağlantı noktası 443 giden bağlantı toothese bağlantı noktalarını kullanılamıyorsa, kullanılır. |

* Mümkün tooreach hello olmalıdır *ana bilgisayar adı*:*BağlantıNoktasıNumarası* , şirket içi kaynak.

Bu makaledeki adımları Hello hello tarayıcı hello şirket içi karma bağlantı aracısını barındıracak bir hello bilgisayardan kullandığınızı varsayar.

Bir yapılandırma ve yukarıda açıklanan hello koşullara uyan bir ortamda yüklü SQL Server zaten varsa, İleri atlayabilirsiniz ve başlayın [şirket içi SQL Server veritabanı oluşturma](#CreateSQLDB).

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a>A. SQL Server Express'i yüklemek, TCP/IP'yi etkinleştirin ve şirket içi SQL Server veritabanı oluşturma
Bu bölümde, nasıl tooinstall SQL Server Express, TCP/IP'yi etkinleştirin ve bir veritabanı oluşturun, böylece web uygulamanızı hello Azure Portal ile çalışıp çalışmayacağını gösterir.

### <a name="install-sql-server-express"></a>SQL Server Express'i Yükleme
1. Merhaba çalıştırmak bir tooinstall SQL Server Express, **SQLEXPRWT_x64_ENU.exe** veya **SQLEXPR_x86_ENU.exe** indirdiğiniz dosya. Merhaba SQL Server Yükleme Merkezi'ni Sihirbazı görünür.
   
    ![SQL Server yükleme][SQLServerInstall]
2. Seçin **yeni SQL Server tek başına yükleme veya özellikler tooan mevcut yükleme eklemek**. Toohello elde edene kadar hello varsayılan seçenekleri ve ayarları, kabul etme hello yönergeleri **örnek Yapılandırması** sayfası.
3. Merhaba üzerinde **örnek Yapılandırması** sayfasında, **varsayılan örnek**.
   
    ![Varsayılan bir örnek seçin][ChooseDefaultInstance]
   
    Varsayılan olarak, hangi hello karma bağlantılar özellik gerektirir olduğu SQL Server statik bağlantı noktası 1433, istemcilerde gelen istekleri için hello varsayılan SQL Server örneğini dinler. Karma bağlantılar tarafından desteklenmeyen dinamik bağlantı noktaları ve UDP, adlandırılmış örnekleri kullanın.
4. Merhaba Hello varsayılanlarına kabul **sunucu yapılandırması** sayfası.
5. Merhaba üzerinde **veritabanı altyapısı Yapılandırması** sayfasında **kimlik doğrulama modu**, seçin **karma mod (SQL Server kimlik doğrulaması ve Windows kimlik doğrulaması)**ve sağlayın bir parola.
   
    ![Karma mod seçin][ChooseMixedMode]
   
    Bu öğreticide, SQL Server kimlik doğrulamasını kullanır. Sağlarsanız, emin tooremember hello parola olabilir, çünkü daha sonra ihtiyacınız olacak.
6. Merhaba Sihirbazı toocomplete hello yükleme Hello kullanılmadıkları adım.

### <a name="enable-tcpip"></a>TCP/IP'yi etkinleştirin
TCP/IP'yi tooenable, SQL Server Express yüklendiğinde, yüklü olduğu SQL Server Configuration Manager kullanır. Merhaba adımları [SQL Server TCP/IP ağ protokolünü etkinleştirin](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) devam etmeden önce.

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a>Şirket içi SQL Server veritabanı oluşturma
Visual Studio web uygulamanızı Azure tarafından erişilebilir bir üyelik veritabanı gerektirir. Bu bir SQL Server veya SQL Server Express veritabanı (, varsayılan MVC şablonu kullanan hello hello LocalDB veritabanını değil), gerektirir hello üyelik veritabanının sonraki oluşturmanız.

1. SQL Server Management Studio'da toohello yalnızca yüklü SQL Server bağlayın. (Merhaba, **tooServer bağlanmak** iletişim görünmez otomatik olarak gidin çok**Nesne Gezgini** hello sol bölmede **Bağlan**ve ardından **Veritabanı altyapısı**.) ![TooServer Bağlan][SSMSConnectToServer]
   
    İçin **sunucu türü**, seçin **veritabanı altyapısı**. İçin **sunucu adı**, kullanabileceğiniz **localhost** veya kullanmakta olduğunuz hello bilgisayarın hello adı. Seçin **SQL Server kimlik doğrulaması**ve ardından hello sa kullanıcı adı ve daha önce oluşturduğunuz hello parolayla oturum açın.
2. SQL Server Management Studio'yu kullanarak yeni bir veritabanı toocreate sağ **veritabanları** , Nesne Gezgini ve ardından **yeni veritabanı**.
   
    ![Yeni veritabanı oluştur][SSMScreateNewDB]
3. Merhaba, **yeni veritabanı** iletişim kutusunda, MembershipDB için hello veritabanı adı girin ve ardından **Tamam**.
   
    ![Veritabanı adı girin][SSMSprovideDBname]
   
    Herhangi bir değişiklik toohello veritabanı bu noktada yapmayın unutmayın. çalıştırdığınızda, web uygulamanız tarafından hello üyelik bilgilerini daha sonra otomatik olarak eklenir.
4. Nesne Gezgini'nde, genişletirseniz, **veritabanları**, hello üyelik veritabanının oluşturulan görürsünüz.
   
    ![Oluşturulan MembershipDB][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-hello-azure-portal"></a>B. Hello Azure portalı bir web uygulaması oluşturma
> [!NOTE]
> Merhaba toouse Bu öğretici için istediğiniz Azure Portal'ın bir web uygulaması zaten oluşturduysanız, şimdi çok atlayabilirsiniz[karma bağlantı ve bir BizTalk hizmeti oluşturma](#CreateHC) ve buradan devam edin.
> 
> 

1. Merhaba, [Azure Portal](https://portal.azure.com), tıklatın **yeni** > **Web + mobil** > **Web uygulaması**.
   
    ![Yeni düğmesi][New]
2. Web Uygulamanızı yapılandırmak ve ardından **oluşturma**.
   
    ![Web sitesi adı][WebsiteCreationBlade]
3. Birkaç dakika sonra hello web uygulaması oluşturuldu ve kendi web uygulaması dikey penceresi görünür. Merhaba dikey web uygulamanızı yönetmenizi sağlayan bir dikey olarak kaydırılabilir Pano ' dir.
   
    ![Çalışan Web sitesi][WebSiteRunningBlade]
   
    tooverify hello web uygulaması canlı, hello tıklayabilirsiniz **Gözat** simgesi toodisplay hello varsayılan sayfası.

Ardından, karma bir bağlantı ve BizTalk hizmeti hello web uygulaması için oluşturur.

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a>C. Karma bağlantı ve bir BizTalk hizmeti oluşturma
1. Geri toosettings hello Portal, Git ve tıklatın **ağ** > **karma bağlantı uç noktalarınızı yapılandırın**.
   
    ![Karma bağlantılar][CreateHCHCIcon]
2. Merhaba karma bağlantıları dikey penceresinde **Ekle** > **yeni karma bağlantı**.
3. Merhaba üzerinde **karma bağlantı oluşturmak** dikey penceresinde:
   
   * İçin **adı**, hello bağlantı için bir ad sağlayın.
   * İçin **ana bilgisayar adı**, SQL Server ana bilgisayarınız hello bilgisayar adını girin.
   * İçin **bağlantı noktası**, 1433 (hello için varsayılan bağlantı noktası SQL Server) girin.
   * Tıklatın **BizTalk hizmeti** > **yeni BizTalk hizmeti** ve hello BizTalk hizmeti için bir ad girin.
     
     ![Karma bağlantı oluşturma][TwinCreateHCBlades]
4. Tıklatın **Tamam** iki kez.
   
    Merhaba işlemi tamamlandığında, hello **bildirimleri** alanı yeşil flash **başarı** ve hello **karma bağlantı** dikey penceresinde hello yeni karma bağlantıyla gösterir Merhaba durumu olarak **bağlı**.
   
    ![Oluşturulan bir karma bağlantı][CreateHCOneConnectionCreated]

Bu noktada, hello bulut karma bağlantı altyapı önemli bir kısmını tamamladınız. Ardından, karşılık gelen bir şirket içi parça oluşturur.

<a name="InstallHCM"></a>

## <a name="d-install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a>D. Merhaba şirket içi karma Bağlantı Yöneticisi toocomplete hello Bağlantısı'nı yükleme
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

Bu hello karma bağlantı altyapı tamamlandı şimdi kullanan bir web uygulaması oluşturacaksınız.

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-hello-database-connection-string-and-run-hello-project-locally"></a>E. Temel bir ASP.NET web projesi oluşturma hello veritabanı bağlantı dizesi düzenleme ve Merhaba projeyi yerel olarak çalıştırma
### <a name="create-a-basic-aspnet-project"></a>Temel bir ASP.NET projesi oluşturma
1. Visual Studio'da, hello **dosya** menüsünde yeni bir proje oluşturun:
   
    ![Yeni Visual Studio projesi][HCVSNewProject]
2. Merhaba, **şablonları** hello bölümünü **yeni proje** iletişim kutusunda **Web** ve **ASP.NET Web uygulaması**ve 'ıtıklatın **Tamam**.
   
    ![ASP.NET Web uygulaması seçin][HCVSChooseASPNET]
3. Merhaba, **yeni ASP.NET projesi** iletişim kutusunda, seçin **MVC**ve ardından **Tamam**.
   
    ![MVC seçin][HCVSChooseMVC]
4. Başlangıç projesi oluşturduğunuzda hello uygulama Benioku sayfası görüntülenir. Merhaba web projesi henüz çalıştırmayın.
   
    ![Benioku sayfası][HCVSReadmePage]

### <a name="edit-hello-database-connection-string-for-hello-application"></a>Merhaba uygulaması için Hello veritabanı bağlantı dizesini Düzenle
Bu adımda, uygulamanızın söyler hello bağlantı dizesini Düzenle nerede toofind yerel SQL Server Express veritabanı. Merhaba uygulaması için yapılandırma bilgilerini içeren hello uygulamanın Web.config dosyasında Hello bağlantı dizesi değil.

> [!NOTE]
> SQL Server Express ve değil hello bir LocalDB Visual Studio'nun varsayılan oluşturduğunuz hello veritabanı uygulamanızın kullandığı tooensure, projenizin çalıştırmadan önce bu adımı tamamlamak önemlidir.
> 
> 

1. Çözüm Gezgini'nde hello Web.config dosyasına çift tıklayın.
   
    ![Web.config][HCVSChooseWebConfig]
2. Merhaba Düzenle **connectionStrings** bölüm toopoint toohello SQL Server veritabanı örneği aşağıdaki hello hello dizimini izleyerek, yerel makinenizde:
   
    ![Bağlantı dizesi][HCVSConnectionString]
   
    Merhaba bağlantı dizesi oluştururken hello aşağıdakileri göz önünde bulundurun:
   
   * Adlandırılmış örneği varsayılan örnek (örneğin, Sunucunuz\\sqlexpress) yerine tooa bağlanıyorsanız, SQL Server toouse statik bağlantı noktalarını yapılandırmanız gerekir. Statik bağlantı noktalarını yapılandırma hakkında daha fazla bilgi için bkz: [nasıl tooconfigure SQL Server toolisten belirli bir bağlantı noktası](http://support.microsoft.com/kb/823938). Varsayılan olarak, adlandırılmış örnekleri UDP ve karma bağlantılar tarafından desteklenmeyen dinamik bağlantı noktaları kullanır.
   * Merhaba belirtmeniz önerilir (Merhaba örnekte gösterildiği gibi varsayılan 1433) hello bağlantı dizesine bağlantı noktası, bu yerel SQL Server'ınızdaki sahip etkin TCP ve hello doğru bağlantı noktasını kullanarak emin olabilir.
   * Bağlantı dizenizi Hello kullanıcı kimliği ve parola belirterek toouse SQL Server kimlik doğrulaması tooconnect unutmayın.
3. Tıklatın **kaydetmek** Visual Studio toosave hello Web.config dosyasında.

### <a name="run-hello-project-locally-and-register-a-new-user"></a>Merhaba projeyi yerel olarak çalıştırın ve yeni bir kullanıcı kaydı
1. Şimdi, yeni web projeniz yerel olarak hata ayıklama altında hello Gözat düğmesine tıklayarak çalıştırın. Bu örnek, Internet Explorer kullanır.
   
    ![Projeyi çalıştırın][HCVSRunProject]
2. Merhaba sağ üst köşesinde hello varsayılan web sayfası üzerinde seçin **kaydetmek** tooregister yeni bir hesap:
   
    ![Yeni bir hesap Kaydet][HCVSRegisterLocally]
3. Bir kullanıcı adı ve parola girin:
   
    ![Kullanıcı adı ve parola girin][HCVSCreateNewAccount]
   
    Bu otomatik olarak bir veritabanı uygulamanız için hello üyelik bilgilerini tutan yerel SQL Server üzerinde oluşturur. Merhaba tablolardan biri (**dbo. AspNetUsers**) ayrı tutma web girdiğiniz olanları hello gibi uygulama kullanıcı kimlik bilgileri. Bu tablo daha sonra hello öğreticide görürsünüz.
4. Merhaba varsayılan web sayfasının Hello tarayıcı penceresini kapatın. Visual Studio'da hello durdurur.

Şimdi toopublish hello uygulama tooAzure olan hello sonraki adım için hazır ve test.

<a name="PubNTest"></a>

## <a name="f-publish-hello-web-application-tooazure-and-test-it"></a>F Yayımlama Hello web uygulama tooAzure ve test
Şimdi,, uygulama tooyour App Service web uygulaması yayımlama ve nasıl daha önce yapılandırdığınız hello karma bağlantıdır toosee test web uygulama toohello veritabanınızı yerel makinenizde kullanılan tooconnect bırakılıyor.

### <a name="publish-hello-web-application"></a>Merhaba web uygulaması yayımlama
1. Yayımlama profilinizi hello hello Azure Portal, App Service web uygulaması için yükleyebilirsiniz. Web uygulamanız için Hello dikey penceresinde **Get yayımlama profili**ve ardından hello dosya tooyour bilgisayara kaydedin.
   
    ![Yayım profili indirin][PortalDownloadPublishProfile]
   
    Ardından, Visual Studio web uygulamanıza bu dosyayı içeri aktaracak.
2. Visual Studio'da hello Çözüm Gezgini'nde proje adına sağ tıklayın ve seçin **Yayımla**.
   
    ![Select yayımlama][HCVSRightClickProjectSelectPublish]
3. Merhaba, **Web'i Yayımla** iletişim kutusunda, hello **profil** sekmesinde, seçin **alma**.
   
    ![İçeri Aktarma][HCVSPublishWebDialogImport]
4. Gözat tooyour indirdiğiniz yayımlama profili, onu seçin ve ardından **Tamam**.
   
    ![Tooprofile Gözat][HCVSBrowseToImportPubProfile]
5. Yayımlama bilgilerinizi içe aktarılır ve üzerinde hello görüntüler **bağlantı** hello iletişim sekmesinde.
   
    ![Yayınla'yı tıklatın][HCVSClickPublish]
   
    **Yayımla**’ta tıklayın.
   
    Yayımlama tamamlandıktan sonra tarayıcınızı başlatın ve şimdi hello Azure bulut dinamik olması dışında şimdi bilinen ASP.NET uygulamanızın--Göster!

Ardından, canlı web uygulama toosee eylemde karma bağlantısını kullanır.

### <a name="test-hello-completed-web-application-on-azure"></a>Azure web uygulamasına test hello tamamlandı
1. Merhaba üstte, web sayfasının sağ Azure üzerinde seçin **oturum**.
   
    ![Test oturum açma][HCTestLogIn]
2. Web uygulaması sunulmuştur uygulama hizmetiniz tooyour web uygulamasının üyelik veritabanının yerel makinenizde bağlı. tooverify hello hello yerel girdiğiniz aynı kimlik bilgileri veritabanına daha önce bu, oturum.
   
    ![Merhaba Karşılama][HCTestHelloContoso]
3. toofurther yeni karma bağlantınız sınamak için Azure web uygulamanızın dışına oturum ve başka bir kullanıcı olarak kaydedin. Yeni bir kullanıcı adı ve parolasını girin ve ardından **kaydetmek**.
   
    ![Test başka bir kullanıcı kaydetme][HCTestRegisterRelecloud]
4. Merhaba yeni kullanıcının kimlik bilgilerini yerel veritabanınızda karma bağlantınız üzerinden depolanmıştı tooverify, yerel bilgisayarınızda SQL Management Studio'yu açın. Merhaba, nesne Gezgini'nde genişletin **MembershipDB** veritabanı ve ardından **tabloları**. Sağ hello **dbo. AspNetUsers** üyelik tablosunda ve seçin **ilk 1000 satırı Seç** tooview hello sonuçları.
   
    ![Merhaba sonuçları görüntüleme][HCTestSSMSTree]
5. Yerel üyelik tablonuz şimdi her iki hesap - yerel olarak oluşturulmuş bir hello ve hello hello Azure bulut oluşturulmuş bir gösterir. Merhaba bulutta oluşturulmuş bir Hello Azure'nın karma bağlantı özelliği aracılığıyla tooyour şirket içi veritabanına kaydedildi.
   
    ![Şirket içi veritabanında kayıtlı kullanıcılar][HCTestShowMemberDb]

Artık oluşturduğunuz ve bir web uygulamasını hello Azure Bulut ve şirket içi SQL Server veritabanı arasında bir karma bağlantı kullanan bir ASP.NET web uygulaması dağıtılmış. Tebrikler!

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
