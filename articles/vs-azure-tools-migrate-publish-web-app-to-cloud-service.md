---
title: "aaaHow tooMigrate ve Yayımla Web uygulaması tooan Azure bulut hizmeti Visual Studio'dan | Microsoft Docs"
description: "Bilgi nasıl toomigrate ve web uygulama tooan Azure bulut hizmeti Visual Studio kullanarak yayımlayabilirsiniz."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9394adfd-a645-4664-9354-dd5df08e8c91
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: a2832c37d2ebdbc1e69a307d16b65b1c87e9070c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-migrate-and-publish-a-web-application-tooan-azure-cloud-service-from-visual-studio"></a>Nasıl yapılır: geçirmek ve Web uygulaması tooan Azure bulut hizmeti Visual Studio'da yayımlama
barındırma hizmetleri ve Azure ölçeklenebilirliğini tootake avantajlarından Merhaba, toomigrate istediğiniz ve web uygulama tooan Azure bulut hizmetinizi yayımlayın. Azure'da küçük değişiklikler tooyour varolan bir uygulama ile bir web uygulaması çalıştırabilirsiniz.

> [!NOTE]
> Bu konu, toocloud Hizmetleri, değil tooweb siteleri dağıtma hakkında ' dir. Tooweb siteleri dağıtma hakkında daha fazla bilgi için bkz: [Azure App Service'te bir web uygulaması dağıtma](app-service-web/web-sites-deploy.md).
>
>

Merhaba bölüm hem Visual C# ve Visual Basic için desteklenen belirli şablonları listesi için bkz **desteklenen proje şablonları** bu konuda daha sonra.

İlk web uygulamanız için Azure Visual Studio'dan etkinleştirmeniz gerekir. Aşağıdaki çizimde hello hello anahtar adımları toopublish dağıtımı için bir Azure projesi toouse ekleyerek varolan web uygulamanızı gösterir. Bu işlem gerekli hello web rolü tooyour çözümü ile bir Azure projesi ekler. Sahip olduğunuz web projesi hello türüne bağlı olarak, Hello hizmet paketi dağıtım için ek derlemeler gerektiriyorsa hello derlemeler için proje özellikleri de güncellenir.

![Bir Web uygulaması tooMicrosoft Azure yayımlama](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC748917.png)

> [!NOTE]
> Merhaba **Dönüştür**, **tooAzure bulut hizmeti projesini Dönüştür** komutu yalnızca çözümünüzdeki hello web projesi için görüntülenir. Örneğin, hello komut çözümünüzdeki Silverlight projesi için kullanılabilir değil.
> Bir hizmet paketi oluşturduğunuzda ya da uygulama tooAzure yayımlama uyarılar veya hatalar oluşabilir. Bu uyarıları ve hataları tooAzure dağıtmadan önce sorunları çözmenize yardımcı olabilir. Örneğin, eksik bir derleme hakkında bir uyarı alabilirsiniz. Tüm uyarıları hata olarak nasıl tootreat gördükleri hakkında daha fazla bilgi için [bir Azure bulut hizmeti projesi ile Visual Studio'yu yapılandırma](vs-azure-tools-configuring-an-azure-project.md). Uygulamanızı çalıştırın hello işlem öykünücüsü kullanarak yerel olarak veya tooAzure yayımlama hello hata aşağıdaki hello görebilirsiniz **hata listesi** penceresi: **hello belirtilen yol, dosya adı veya her ikisini birden çok uzun** . Merhaba hello tam Azure projesi adı çok uzun olduğundan bu hata oluşur. Merhaba tam yolunu da içeren hello proje adı Hello uzunluğu birden fazla 146 karakterler olamaz. Örneğin, bu Silverlight uygulaması için oluşturulmuş bir Azure projesi için dosya yolu da dahil olmak üzere hello tam proje adıdır: `c:\users\<user name>\documents\visual studio 2015\Projects\SilverlightApplication4\SilverlightApplication4.Web.Azure.ccproj`. Merhaba tam proje adının daha kısa bir yol tooreduce hello uzunluğu olan çözüm tooa farklı dizin toomove olabilir.
>
>

toomigrate ve bir web uygulaması tooAzure Visual Studio'dan yayımlamak, şu adımları izleyin.

## <a name="enable-a-web-application-for-deployment-tooazure"></a>Bir Web uygulaması için dağıtım tooAzure etkinleştir
### <a name="tooenable-a-web-application-for-deployment-tooazure"></a>tooenable dağıtım tooAzure için bir web uygulaması
1. tooenable web uygulamanız için dağıtım tooAzure, bir web açık hello kısayol menüsünü çözümünüzde proje ve Azure dağıtım projesi eklemek seçin.

    hello aşağıdaki eylemler gerçekleşir:

   * Bir Azure projesi adlı `<name of hello web project>.Azure` toohello çözüm uygulamanız için eklenir.
   * Web rolü hello web projesi için toothis Azure projesi eklenir.
   * Merhaba **kopya yerel** özelliği, MVC 2, MVC 3, MVC 4 ve Silverlight iş uygulamaları için gerekli olan tüm derlemeler için tootrue ayarlanır. Bu dağıtım için kullanılan bu derlemeler toohello hizmet paketi ekler.

   > [!IMPORTANT]
   > Diğer derlemeler veya bu web uygulaması için gerekli olan dosyalar varsa, bu dosyalar için hello özellikleri el ile ayarlamanız gerekir. Tooset bu özellikleri nasıl görürüm hakkında bilgi için hello bölüm **hello hizmet paketi dahil dosyalarında** bu makalenin ilerisinde yer.
   >
   > [!NOTE]
   > Web rolü belirli web projesi için bir Azure projesi hello çözümde zaten varsa **Dönüştür**, **tooAzure bulut hizmeti projesini Dönüştür** bu web projesi için hello kısayol menüsünde gösterilmez .
   >
   >

   Birden çok web projeleri, web uygulamanızda varsa ve her web projesi için toocreate web rolleri istediğiniz her web projesi için bu yordamdaki hello adımları uygulamanız gerekir. Bu, her bir web rolü için ayrı Azure proje oluşturur. Her web projesi ayrı olarak yayımlanabilir. Alternatif olarak, web uygulamanızda başka bir web rolü tooan mevcut Azure projesi el ile ekleyebilirsiniz. toodo hello için bu, açık hello kısayol menüsü **rolleri** Azure projenizdeki klasörü seçin **Ekle**, sonra **çözüm Web rolü projesinde**, bir Web projesi tooadd hello seçin Rol ve ardından hello **Tamam** düğmesi.

## <a name="use-an-azure-sql-database-for-your-application"></a>Uygulamanız için bir Azure SQL veritabanını kullan
Merhaba şirket içinde bir SQL Server veritabanını kullanan web uygulamanız için bir bağlantı dizesi varsa, bu bağlantı dizesi toouse SQL veritabanı örneği yerine Azure barındıran değiştirmelisiniz.

> [!IMPORTANT]
> Aboneliğinizi toouse SQL veritabanı etkinleştirmeniz gerekir. Aboneliğinizi hello erişim [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885), aboneliğinizi sağlar hangi hizmetlerin belirleyebilirsiniz. Merhaba aşağıdaki yönergeleri uygulayın yayımlanan toohello [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885). Merhaba kullanıyorsanız [Azure portal](http://portal.microsoft.com), toohello sonraki yordamı atlayın.
>
>

### <a name="toouse-a-sql-database-instance-in-your-web-role-for-your-connection-string"></a>toouse web rolünüz bağlantı dizenizi için SQL veritabanı örneğinde
1. toocreate hello SQL veritabanı örneğinde [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885), aşağıdaki makaleye bakın hello hello adımları izleyin: [bir SQL veritabanı sunucusu oluşturmak](http://go.microsoft.com/fwlink/?LinkId=225109).

   > [!NOTE]
   > SQL veritabanı Örneğiniz için hello güvenlik duvarı kuralları ayarlamak, hello seçmelisiniz **bu sunucu diğer Azure Hizmetleri tooaccess izin** onay kutusu.
   >
   >
2. bağlantı dizenizi için SQL veritabanı toouse ait bir örnek toocreate aşağıdaki makaleye bakın hello sonraki bölümünde hello hello adımları izleyin: [bir SQL veritabanı oluşturma](http://go.microsoft.com/fwlink/?LinkId=225110).
3. bağlantı dizenizi için toocopy hello ADO.NET bağlantı dizesi toouse gerçekleştirmek hello adımlarını izleyerek hello [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885).  

   1. Merhaba seçin **veritabanı** düğmesine ve ardından açık hello düğümü SQL veritabanı örneğiniz toocreate kullanılan hello abonelik için.
   2. SQL veritabanı'nın toodisplay hello kullanılabilir örnekler seçin hello **SQL veritabanları** düğümü.
   3. Merhaba veritabanının toodisplay hello özelliklerini hello veritabanı seçin. Merhaba **özellikleri** görünümü görüntülenir.

      > [!NOTE]
      > Merhaba, **özellikleri** görünüm görünmüyor, ayırıcı kullanarak hello tooopen gerekebilir.
      >
      >
   4. toodisplay hello bağlantı dizeleri, hello üç nokta (...) düğmesini sonraki tooView seçin.

      Merhaba **bağlantı dizeleri** iletişim kutusu görüntülenir.
   5. toocopy hello ADO.NET bağlantı dizesi, hello metni vurgulayın ve hello Ctrl + C tuşlarını seçin.
   6. tooclose hello iletişim kutusunda, hello seçin **Kapat** düğmesi.
4. tooreplace hello bağlantı hello web.config dosyası toouse SQL veritabanı'nın bu örneğinin dize hello web.config dosyasını açın, hello varolan bağlantı dizesi girişi vurgulayın ve hello Ctrl + V tuşlarını seçin. Merhaba hello SQL veritabanı örneği için ADO.NET bağlantı dizesi hello varolan bağlantı dizesi değiştirir.
5. Merhaba parametresini eklemeniz gerekir `MultipleActiveResultSets=True` toohello bağlantı dizesi. Merhaba bağlantı dizesi biçimi aşağıdaki hello olmalıdır:

    ```
    connectionString=”Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"
    ```
6. (İsteğe bağlı) Bir alternatif bir yöntem toochanging hello bağlantı doğrudan hello web.config dosyasında tooadd toocreate, hizmet paketi kullanmak hello yapı yapılandırmasına bağlı olarak hello web.config dönüşümü dosyalardan birini bölüme dizedir. Merhaba Web.Debug.Config dosyasını veya hello Web.Release.Config dosyasını açın. Bu bölümde aşağıdaki hello ekleyin:

    ```
    XMLCopy<connectionStrings><addname="DefaultConnection"connectionString="Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"xdt:Transform="SetAttributes"xdt:Locator="Match(name)"/></connectionStrings>
    ```
7. Değiştirdiğiniz hello dosyasını kaydedin ve uygulamanızı yeniden yayımlayın.

### <a name="toouse-an-instance-of-sql-database-by-using-hello-azure-classic-portal"></a>toouse hello Klasik Azure portalı kullanarak SQL veritabanı örneği
1. Merhaba, [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885), hello SQL veritabanları düğümünü seçin.

   * SQL veritabanı toouse istediğiniz Hello örneği varsa, tooopen seçin.
   * Hiç örneği oluşturmadıysanız, hello uygun bağlantıyı seçin ve ardından bir örneği oluşturun.
2. Açın veya bir veritabanı örneği oluşturmayı sonra hello seçin **bağlantı dizeleri** bağlantı.
3. Merhaba hello sayfanın sonundaki, hello bağlantı tooconfigure güvenlik duvarı ayarlarını seçin ve hello varsayılan değerleri kabul edin veya gereksinim duyduğunuz hello değerleri yapılandırın.
4. Merhaba ADO.NET bağlantı dizesini kopyalayın, hello şirket içi veritabanı için eski bağlantı dizesi hello üzerinden web.config dosyasına yapıştırın ve emin tooadd olması `MultipleActiveResultSets=True`.

## <a name="publish-a-web-application-tooazure"></a>Bir Web uygulaması tooAzure yayımlama
### <a name="toopublish-a-web-application-tooazure"></a>bir Web uygulaması tooAzure toopublish
1. tootest Merhaba uygulaması hello Azure işlem öykünücüsü kullanarak hello yerel geliştirme ortamında hello Azure için açık hello kısayol menüsü proje hello web rolü için ve seçin **başlangıç projesi olarak ayarla**. Ardından **hata ayıklama**, **hata ayıklamayı Başlat** (klavye: **F5**).

    Merhaba **başlangıç hello Azure hata ayıklama ortamı** iletişim kutusu açılır ve Merhaba uygulaması hello tarayıcıda başlatır. Merhaba web uygulamasında toostart her nasıl türü hakkında belirli Ayrıntılar için işlem öykünücüsü, bu bölümdeki hello tablosuna bakın.
2. tooset hello hizmetlerini uygulama toopublish tooAzure için bir Microsoft hesabı ve bir Azure aboneliğinizin olması gerekir. Kullanım hello adımları konu tooset hizmetlerinizi yukarı aşağıdaki hello: [toopublish hazırlayın veya Visual Studio'dan Azure bir uygulamayı dağıtmak](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md).
3. toopublish hello web uygulama tooAzure hello web projesi için hello kısayol menüsünü açın ve seçin **tooAzure yayımlama**.

    Merhaba **Azure uygulamasını Yayımla** iletişim kutusu açılır ve Visual Studio hello dağıtım işlemi başlatır. Merhaba bölüm nasıl toopublish hello uygulama hakkında daha fazla bilgi için bkz: **Visual Studio'dan Azure uygulamasını Yayımla** içinde [yayımlama hello Azure araçlarını kullanarak bir bulut hizmeti](vs-azure-tools-publishing-a-cloud-service.md).

   > [!NOTE]
   > Hello Azure projesi hello web uygulamasından yayımlayabilirsiniz. toodo bunu hello Azure projesi için hello kısayol menüsünü açın ve seçin **Yayımla**.
   >
   >
4. toosee hello ilerleme hello dağıtımının hello görüntüleyebilir **Azure etkinlik günlüğü** penceresi. Bu günlük Hello dağıtım işlemi başlatıldığında otomatik olarak görüntülenir. Merhaba etkinlik günlüğü hello kalem genişletebilirsiniz tooshow ayrıntılı bilgileri hello aşağıdaki çizimde gösterildiği gibi:

    ![VST_AzureActivityLog](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744149.png)
5. (İsteğe bağlı) toocancel hello dağıtım işlemi, hello etkinlik günlüğünde hello satır öğenin hello kısayol menüsünü açın ve seçin **iptal et ve Kaldır**. Bu hello dağıtım işlemi durdurur ve Azure'dan hello dağıtım ortamı siler.

   > [!NOTE]
   > Bu dağıtım ortamı sonraki tooremove süredir dağıtıldı, hello kullanmalısınız [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885).
   >
   >
6. (İsteğe bağlı) Rolü örneklerinizi başlattıktan sonra Visual Studio hello dağıtım ortamı hello otomatik olarak gösterir. **Azure işlem** düğümünde **Cloud Explorer** veya **Sunucu Gezgini**. Buradan hello tek rol örneklerini hello durumunu görüntüleyebilirsiniz.

    Merhaba aşağıda gösterilmiştir hello rol örneklerinin **Sunucu Gezgini** hala hello başlatılıyor durumu çalışırken:

    ![VST_DeployComputeNode](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744134.png)
7. tooaccess dağıtımı sonra uygulamanızı seçin hello ok sonraki tooyour dağıtım durumunu zaman **tamamlandı** hello görünür **Azure etkinlik günlüğü**. Bu, Azure'da hello URL web uygulamanız için görüntüler. Merhaba aşağıdaki tablonun nasıl toostart belirli bir türü Azure web uygulamasından hakkında hello Ayrıntılar için bkz.

    Aşağıdaki tablonun hello nasıl toostart belirli web uygulamaları Azure veya toorun veya bir web uygulaması hello Azure işlem öykünücüsü kullanarak yerel olarak hata ayıklama hakkında hello ayrıntılarını listeler:

   | Web uygulaması türü | Merhaba işlem öykünücüsü kullanarak yerel olarak çalıştır/Hata Ayıkla | Azure'da çalışan |
   | --- | --- | --- |
   | ASP.NET Web uygulaması |Merhaba menü çubuğunda seçin **hata ayıklama**, **hata ayıklamayı Başlat** (klavye: hello seçin **F5** anahtar.). |Hello görüntülenen hello URL köprü seçin **dağıtım** hello sekmesi **Azure etkinlik günlüğü** tooload hello başlangıç sayfasını hello tarayıcıda. |
   | ASP.NET MVC 2 Web uygulaması |Merhaba menü çubuğunda seçin **hata ayıklama**, **hata ayıklamayı Başlat** (klavye: hello seçin **F5** anahtar.). |Hello görüntülenen hello URL köprü seçin **dağıtım** hello sekmesi **Azure etkinlik günlüğü** tooload hello başlangıç sayfasını hello tarayıcıda. |
   | ASP.NET MVC 3 Web uygulaması |Merhaba menü çubuğunda seçin **hata ayıklama**, **hata ayıklamayı Başlat** (klavye: hello seçin **F5** anahtar.). |Hello görüntülenen hello URL köprü seçin **dağıtım** hello sekmesi **Azure etkinlik günlüğü** tooload hello başlangıç sayfasını hello tarayıcıda. |
   | ASP.NET MVC 4 Web uygulaması |Merhaba menü çubuğunda seçin **hata ayıklama**, **hata ayıklamayı Başlat** (klavye: hello seçin **F5** anahtar.). |Hello görüntülenen hello URL köprü seçin **dağıtım** hello sekmesi **Azure etkinlik günlüğü** tooload hello başlangıç sayfasını hello tarayıcıda. |
   | ASP.NET boş Web uygulaması |Web projeniz için hello başlangıç sayfası olarak ayarlamak, uygulamanızdaki bir .aspx sayfasında eklemeniz gerekir. Merhaba menü çubuğunda seçin **hata ayıklama**, **hata ayıklamayı Başlat** (klavye: hello seçin **F5** anahtar.). |Uygulamanıza varsayılan bir .aspx sayfası varsa, hello görüntülenen hello URL köprü seçin **dağıtım** hello sekmesi **Azure etkinlik günlüğü** ve bu sayfayı hello tarayıcıda yüklenir. Farklı .aspx sayfa varsa, toonavigate toothis belirli sayfa, url biçimi aşağıdaki hello kullanarak gerekir:`<url for deployment>/<name of page>.aspx` |
   | Silverlight uygulaması |Merhaba menü çubuğunda seçin **hata ayıklama**, **hata ayıklamayı Başlat** (klavye: hello seçin **F5** anahtar.). |Merhaba, url biçimi aşağıdaki kullanarak uygulamanız için toonavigate toohello belirli sayfa gerekir:`<url for deployment>/<name of page>.aspx` |
   | Silverlight iş uygulaması |Merhaba menü çubuğunda seçin **hata ayıklama**, **hata ayıklamayı Başlat** (klavye: hello seçin **F5** anahtar.). |Merhaba, url biçimi aşağıdaki kullanarak uygulamanız için toonavigate toohello belirli sayfa gerekir:`<url for deployment>/<name of page>.aspx` |
   | Silverlight gezinti uygulaması |Merhaba menü çubuğunda seçin **hata ayıklama**, **hata ayıklamayı Başlat** (klavye: hello seçin **F5** anahtar.). |Merhaba, url biçimi aşağıdaki kullanarak uygulamanız için toonavigate toohello belirli sayfa gerekir:`<url for deployment>/<name of page>.aspx` |
   | WCF hizmet uygulaması |Merhaba başlangıç olarak WCF Hizmeti projeniz için sayfa hello .svc dosya ayarlamanız gerekir. Merhaba menü çubuğunda seçin **hata ayıklama**, **hata ayıklamayı Başlat** (klavye: hello seçin **F5** anahtar.). |Merhaba, url biçimi aşağıdaki kullanarak uygulamanız için toonavigate toohello svc dosya gerekir:`<url for deployment>/<name of service file>.svc` |
   | WCF iş akışı hizmeti uygulaması |Merhaba başlangıç olarak WCF Hizmeti projeniz için sayfa hello .svc dosya ayarlamanız gerekir. Merhaba menü çubuğunda seçin **hata ayıklama**, **hata ayıklamayı Başlat** (klavye: hello seçin **F5** anahtar.). |Merhaba, url biçimi aşağıdaki kullanarak uygulamanız için toonavigate toohello svc dosya gerekir:`<url for deployment>/<name of service file>.svc` |
   | ASP.NET dinamik varlıklar |Merhaba menü çubuğunda seçin **hata ayıklama**, **hata ayıklamayı Başlat** (klavye: hello seçin **F5** anahtar.). |Merhaba bağlantı dizesini güncellemeniz gerekir (sonraki bölüme bakın). Ayrıca, url biçimi aşağıdaki hello kullanarak uygulamanız için toonavigate toohello belirli sayfa gerekir:`<url for deployment>/<name of page>.aspx` |
   | ASP.NET dinamik veri LINQ tooSQL |Merhaba menü çubuğunda seçin **hata ayıklama**, **hata ayıklamayı Başlat** (klavye: hello seçin **F5** anahtar.). |Bu yordamdaki hello adımları izlemelisiniz: uygulamanız için bir SQL Azure veritabanı kullanın (Bu konuda önceki bölüme bakın). Ayrıca, url biçimi aşağıdaki hello kullanarak uygulamanız için toonavigate toohello belirli sayfa gerekir:`<url for deployment>/<name of page>.aspx` |

## <a name="update-a-connection-string-for-aspnet-dynamic-entities"></a>ASP.NET dinamik varlıklar için bir bağlantı dizesi güncelleştir
### <a name="tooupdate-a-connection-string-for-aspnet-dynamic-entities"></a>tooUpdate ASP.NET dinamik varlıklar için bir bağlantı dizesi
1. toocreate dinamik varlıklar ASP.NET web uygulaması için kullanılabilir bir SQL Azure veritabanı adımları hello hello yordamdaki **uygulamanız için bir SQL Azure veritabanı kullan** bu konuda daha önce.
2. Merhaba tabloları ve bu veritabanından hello için gereksinim duyduğunuz alanları ekleme [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885).
3. Bu tür bir uygulama için Hello bağlantı dizesi biçimi hello web.config dosyasında aşağıdaki hello sahiptir:  

    ```
    <addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=<server name>\SQLEXPRESS;initial catalog=<database name>;integrated security=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```

    Güncelleştirme hello *connectionString* hello ADO.NET bağlantı dizesi SQL Azure veritabanı ile aşağıdaki gibi değer:

    ```
    XMLCopy<addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;Server=tcp:<SQL Azure server name>.database.windows.net,1433;Database=<database name>;User ID=<user name>;Password=<password>;Trusted_Connection=False;Encrypt=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```
4. toosave hello web.config dosyasını seçin toohello bağlantı dizesi, hello menü çubuğunda yaptığınız hello değişikliklerle **dosya**, **web.config kaydetmek**.

## <a name="supported-project-templates"></a>Desteklenen proje şablonları
bir web uygulaması tooAzure toopublish, Merhaba uygulaması hello proje şablonlarından birini C# veya Visual Basic'hello aşağıdaki tabloda listelenen kullanması gerekir.

| Proje şablonu grubu | Proje şablonu |
| --- | --- |
| Web |ASP.NET Web uygulaması |
| Web |ASP.NET MVC 2 Web uygulaması |
| Web |ASP.NET MVC 3 Web uygulaması |
| Web |ASP.NET MVC4 Web uygulaması |
| Web |ASP.NET boş Web uygulaması |
| Web |ASP.NET MVC 2 boş Web uygulaması |
| Web |ASP.NET dinamik veri varlıkları Web uygulaması |
| Web |ASP.NET dinamik veri LINQ tooSQL Web uygulaması |
| Silverlight |Silverlight uygulaması |
| Silverlight |Silverlight iş uygulaması |
| Silverlight |Silverlight gezinti uygulaması |
| WCF |WCF hizmet uygulaması |
| WCF |WCF iş akışı hizmeti uygulaması |
| İş akışı |WCF iş akışı hizmeti uygulaması |

## <a name="next-steps"></a>Sonraki Adımlar
Yayımlama hakkında daha fazla bilgi için bkz: [tooPublish hazırlayın veya Visual Studio'dan Azure uygulama dağıtmak](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md). Ayrıca kullanıma [ayarı yukarı adlı kimlik doğrulama bilgilerini](vs-azure-tools-setting-up-named-authentication-credentials.md).
