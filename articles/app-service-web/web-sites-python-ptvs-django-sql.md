---
title: "Visual Studio için Python Araçları 2.2 ile Azure’da Django ve SQL Veritabanı"
description: "SQL veritabanı örneğinde veri depolayan bir Django web uygulaması oluşturmak için Visual Studio için Python araçlarını kullanmayı öğrenin ve Azure App Service Web Apps için dağıtın."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 65b59dee2b7bddca77d31c692dab713c68d67e24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a>Visual Studio için Python Araçları 2.2 ile Azure’da Django ve SQL Veritabanı
Bu öğreticide, kullanacağız [Visual Studio için Python Araçları] yoklamalar web uygulaması PTVS örnek şablonlarından birini kullanarak basit bir oluşturmak için. Bu öğretici olarak da kullanılabilir bir [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).

Biz Azure üzerinde barındırılan bir SQL veritabanı kullanmayı, bir SQL veritabanını kullanmak için web uygulamasını yapılandırma ve web uygulaması'na yayımlamak nasıl öğreneceksiniz [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

Bkz: [Python Geliştirici Merkezi] Bottle kullanarak PTVS ile Azure App Service Web Apps geliştirmeyi kapsayan diğer makaleler için Flask ve Django web altyapılarını Azure Table Storage, MySQL ve SQL Database hizmetleriyle. Bu makale App Service’e odaklanmakla birlikte, [Azure Cloud Services]’i geliştirirken adımlar benzerdir.

## <a name="prerequisites"></a>Ön koşullar
* Visual Studio 2015
* [Python 2.7 32 bit]
* [Visual Studio için Python Araçları 2.2]
* [Visual Studio Örnekleri VSIX için Python Tools 2.2]
* [VS 2015 için Azure SDK Araçları]
* Django 1.9 veya üzeri

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin. Kredi kartı ve taahhüt gerekmez.
>
>

## <a name="create-the-project"></a>Proje oluşturma
Bu bölümde, örnek şablonu kullanarak bir Visual Studio projesi oluşturacağız. Biz sanal ortam oluşturacak ve gerekli paketleri yükleyeceksiniz. Sqlite kullanarak yerel bir veritabanı oluşturacağız. Ardından web uygulamasını yerel olarak çalıştıracaksınız.

1. Visual Studio'da, **Dosya**, **Yeni Proje**’yi seçin.
2. [Visual Studio Örnekleri VSIX için Python Tools 2.2] proje şablonlarını **Python**, **Örnekler** altında bulabilirsiniz. **Yoklamalar Django Web Projesi**’ni seçin ve projeyi oluşturmak için Tamam’a tıklayın.

     ![Yeni Proje İletişim Kutusu](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. Dış paketleri yüklemeniz istenir. **Sanal bir ortama yükle**’yi seçin.

     ![Dış Paketler İletişim Kutusu](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. Temel yorumlayıcı olarak **Python 2.7**’yi seçin.

     ![Sanal Ortama Ekle İletişim Kutusu](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. **Çözüm Gezgini**’nde, proje düğümüne sağ tıklayın ve **Python**’u ve ardından **Django Geçişi**’ni seçin.  Ardından **Django Yetkili Kullanıcısı Oluşturma**’yı seçin.
6. Bu, Django yönetim konsolunu açar ve proje klasöründe bir sqlite veritabanı oluşturur. Bir kullanıcı oluşturmak için istemleri takip edin.
7. Uygulama tuşlarına basarak çalıştığını onaylayın <kbd>F5</kbd>.
8. Üst kısımdaki gezinti çubuğunda **Oturum Aç**’a tıklayın.

     ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. Veritabanını eşitlediğinizde, oluşturduğunuz kullanıcı için kimlik bilgilerini girin.

     ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. **Örnek Yoklamalar Oluştur**’a tıklayın.

      ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. Bir yoklamaya tıklayın ve oy verin.

      ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a>SQL Veritabanı oluşturma
Veritabanı için Azure SQL veritabanını oluşturacağız.

Aşağıdaki adımları izleyerek bir veritabanı oluşturabilirsiniz.

1. İçine oturum [Azure Portal].
2. Gezinti bölmesinin en altında tıklatın **yeni**. , tıklatın **veri + depolama** > **SQL veritabanı**.
3. Yeni bir kaynak grubu oluşturarak yeni SQL veritabanı yapılandırın ve uygun bir konum seçin.
4. SQL veritabanı oluşturulduktan sonra tıklatın **Visual Studio'da Aç** veri tabanı dikey.
5. Tıklatın **güvenlik duvarınızı yapılandırma**.
6. İçinde **güvenlik duvarı ayarlarını** dikey penceresinde sahip bir güvenlik duvarı kuralı ekleme **başlangıç IP** ve **bitiş IP** geliştirme makinenizde ortak IP adresi olarak ayarlayın. **Kaydet** düğmesine tıklayın.

   Bu işlem, geliştirme makinenizden veritabanı sunucusuna bağlantılar sağlar.
7. Geri veritabanı dikey penceresinde tıklayın **özellikleri**, ardından **veritabanı bağlantı dizelerini Göster**.
8. Değeri koymak için Kopyala düğmesini kullanın **ADO.NET** panoya.

## <a name="configure-the-project"></a>Projeyi Yapılandırma
Bu bölümde, yeni oluşturduğumuz SQL veritabanını kullanmak için web uygulamamızı yapılandıracağız. Biz de SQL veritabanlarını Django ile birlikte kullanmak için gerekli ek Python paketlerini de yükleyeceksiniz. Ardından web uygulamasını yerel olarak çalıştıracaksınız.

1. Visual Studio'da, *ProjectName* klasöründe **settings.py** dosyasını açın. Geçici olarak bağlantı dizesini düzenleyiciye yapıştırın. Bağlantı dizesi bu biçimdedir:

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

Tanımını Düzenle `DATABASES` yukarıdaki değerleri kullanmak için.

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. Çözüm Gezgini'nde, **Python Ortamları** altında, sanal ortama sağ tıklayın ve **Python Paketini Yükle**’yi seçin.
2. **pip** kullanarak `pyodbc` paketini yükleyin.

     ![Python paketi Yükle iletişim kutusu](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. **pip** kullanarak `django-pyodbc-azure` paketini yükleyin.

     ![Python paketi Yükle iletişim kutusu](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. **Çözüm Gezgini**’nde, proje düğümüne sağ tıklayın ve **Python**’u ve ardından **Django Geçişi**’ni seçin.  Ardından **Django Yetkili Kullanıcısı Oluşturma**’yı seçin.

   Bu önceki bölümde oluşturduğumuz SQL veritabanı için tablo oluşturur. Kullanıcının ilk bölümünde oluşturulan sqlite veritabanındaki kullanıcıyla eşleşmesi gerekmeyen bir kullanıcı oluşturmak için istemleri izleyin.
5. Uygulamayı `F5` ile çalıştırın. İle oluşturulan yoklamalar **örnek yoklamalar Oluştur** ve oy vermeyle gönderilen veriler SQL veritabanında seri hale getirilir.

## <a name="publish-the-web-app-to-azure-app-service"></a>Web uygulamasını Azure App Service’te yayımlama
Azure .NET SDK'sı Azure App Service Web Apps için web web uygulamanızı dağıtmak için kolay bir yol sağlar.

1. **Çözüm Gezgini**’nde, proje düğümüne sağ tıklayın ve **Yayımla**’yı seçin.

     ![Web Yayımlama İletişim Kutusu](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. **Microsoft Azure Web Apps** ’e tıklayın.
3. Yeni bir web uygulaması oluşturmak için **Yeni**’ye tıklayın.
4. Aşağıdaki alanları doldurun ve **oluşturma**.

   * **Web Uygulaması adı**
   * **App Service planı**
   * **Kaynak grubu**
   * **Bölge**
   * **Veritabanı sunucusu**nu **Veritabanı yok** olarak bırakın.
5. Diğer tüm varsayılanları kabul edin ve **Yayımla**’ya tıklayın.
6. Web tarayıcınız yayımlanan web uygulamasına otomatik olarak açılır. Web uygulaması kullanarak, beklendiği gibi çalıştığını görmelisiniz **SQL** Azure üzerinde barındırılan veritabanı.

   Tebrikler!

     ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a>Sonraki adımlar
Visual Studio, Django ve SQL veritabanı için Python araçları hakkında daha fazla bilgi için aşağıdaki bağlantıları izleyin.

* [Visual Studio için Python Araçları Belgeleri]
  * [Web Projeleri]
  * [Bulut Hizmeti Projeleri]
  * [Microsoft Azure’da Uzaktan Hata Ayıklama]
* [Django Belgeleri]
* [SQL Veritabanı]

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Python Geliştirici Merkezi]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Visual Studio için Python Araçları]: http://aka.ms/ptvs
[Visual Studio için Python Araçları 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio Örnekleri VSIX için Python Tools 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025
[VS 2015 için Azure SDK Araçları]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517190
[Visual Studio için Python Araçları Belgeleri]: http://aka.ms/ptvsdocs
[Microsoft Azure’da Uzaktan Hata Ayıklama]: http://go.microsoft.com/fwlink/?LinkId=624026
[Web Projeleri]: http://go.microsoft.com/fwlink/?LinkId=624027
[Bulut Hizmeti Projeleri]: http://go.microsoft.com/fwlink/?LinkId=624028
[Django Belgeleri]: https://www.djangoproject.com/
[SQL Veritabanı]: /documentation/services/sql-database/
