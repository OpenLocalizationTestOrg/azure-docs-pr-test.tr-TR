---
title: "aaaDjango ve Visual Studio için Python araçları 2.2 ile azure'da SQL veritabanı"
description: "Nasıl toouse hello Python araçları Visual Studio toocreate için bir SQL veritabanı örneğinde veri depolayan bir Django web uygulaması öğrenin ve tooAzure App Service Web Apps dağıtın."
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
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a>Visual Studio için Python Araçları 2.2 ile Azure’da Django ve SQL Veritabanı
Bu öğreticide, kullanacağız [Visual Studio için Python Araçları] toocreate basit bir web uygulamasına hello PTVS örnek şablonlarından birini kullanarak yoklar. Bu öğretici olarak da kullanılabilir bir [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).

Biz nasıl toouse bir SQL veritabanı Azure üzerinde barındırılan, nasıl tooconfigure hello web uygulama toouse bir SQL veritabanı ve nasıl toopublish hello web uygulaması çok öğreneceksiniz[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

Merhaba bkz [Python Geliştirici Merkezi] Bottle kullanarak PTVS ile Azure App Service Web Apps geliştirmeyi kapsayan diğer makaleler için Flask ve Django web altyapılarını Azure Table Storage, MySQL ve SQL Database hizmetleriyle. Bu makale App Service'e odaklanmakla birlikte hello adımlar geliştirirken benzer [Azure Cloud Services].

## <a name="prerequisites"></a>Ön koşullar
* Visual Studio 2015
* [Python 2.7 32 bit]
* [Visual Studio için Python Araçları 2.2]
* [Visual Studio Örnekleri VSIX için Python araçları 2.2]
* [VS 2015 için Azure SDK Araçları]
* Django 1.9 veya üzeri

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
>
>

## <a name="create-hello-project"></a>Başlangıç projesi oluşturma
Bu bölümde, örnek şablonu kullanarak bir Visual Studio projesi oluşturacağız. Biz sanal ortam oluşturacak ve gerekli paketleri yükleyeceksiniz. Sqlite kullanarak yerel bir veritabanı oluşturacağız. Ardından hello web uygulamasını yerel olarak çalıştıracaksınız.

1. Visual Studio'da, **Dosya**, **Yeni Proje**’yi seçin.
2. Proje şablonlarını hello hello [Visual Studio Örnekleri VSIX için Python araçları 2.2] altında kullanılabilir **Python**, **örnekleri**. Seçin **yoklamalar Django Web projesi** ve Tamam toocreate hello proje'yi tıklatın.

     ![Yeni Proje İletişim Kutusu](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. İstendiğinde tooinstall dış paketler olacaktır. **Sanal bir ortama yükle**’yi seçin.

     ![Dış Paketler İletişim Kutusu](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. Seçin **Python 2.7** hello temel yorumlayıcı olarak.

     ![Sanal Ortama Ekle İletişim Kutusu](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. İçinde **Çözüm Gezgini**, hello proje düğümüne sağ tıklayın ve seçin **Python**ve ardından **Django geçirmek**.  Ardından **Django Yetkili Kullanıcısı Oluşturma**’yı seçin.
6. Bu, Django yönetim konsolunu açın ve hello proje klasöründe bir sqlite veritabanı oluşturun. Merhaba istemleri toocreate kullanıcı izleyin.
7. Merhaba uygulaması tuşlarına basarak çalıştığını onaylayın <kbd>F5</kbd>.
8. Tıklatın **oturum** hello gezinti çubuğunda hello üstünde.

     ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. Hello veritabanını eşitlediğinizde, oluşturduğunuz hello kullanıcı için Hello kimlik bilgilerini girin.

     ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. **Örnek Yoklamalar Oluştur**’a tıklayın.

      ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. Bir yoklamaya tıklayın ve oy verin.

      ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a>SQL Veritabanı oluşturma
Merhaba veritabanı için bir Azure SQL veritabanı oluşturacağız.

Aşağıdaki adımları izleyerek bir veritabanı oluşturabilirsiniz.

1. Merhaba günlüğüne [Azure Portal].
2. Merhaba Gezinti bölmesinin Hello altında tıklatın **yeni**. , tıklatın **veri + depolama** > **SQL veritabanı**.
3. Yapılandırma yeni bir kaynak grubu oluşturarak yeni SQL veritabanı hello ve hello uygun bir konum seçin.
4. Merhaba SQL veritabanı oluşturulduktan sonra tıklatın **Visual Studio'da Aç** hello veritabanı dikey penceresinde.
5. Tıklatın **güvenlik duvarınızı yapılandırma**.
6. Merhaba, **güvenlik duvarı ayarlarını** dikey penceresinde ile güvenlik duvarı kuralı ekleyin **başlangıç IP** ve **bitiş IP** geliştirme makinenizde toohello genel IP adresi ayarlayın. **Kaydet** düğmesine tıklayın.

   Bu bağlantıları toohello veritabanı geliştirme makinenizde sunucusundan olanak tanır.
7. Geri hello veritabanı dikey penceresinde tıklayın **özellikleri**, ardından **veritabanı bağlantı dizelerini Göster**.
8. Merhaba Kopyala düğmesine tooput hello değerini kullanın **ADO.NET** hello Panosu'nda.

## <a name="configure-hello-project"></a>Merhaba projeyi yapılandırma
Bu bölümde, yeni oluşturduğumuz bizim web uygulama toouse hello SQL veritabanı yapılandıracağız. Ek Python paketlerini gerekli toouse SQL veritabanlarını da Django ile yükleyeceksiniz. Ardından hello web uygulamasını yerel olarak çalıştıracaksınız.

1. Visual Studio'da açın **ProjectName**, hello gelen *ProjectName* klasör. Geçici olarak hello Düzenleyicisi'nde hello bağlantı dizesini yapıştırın. Merhaba bağlantı dizesi bu biçimdedir:

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

Merhaba tanımını Düzenle `DATABASES` toouse hello değerleri yukarıdaki.

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

1. Çözüm Gezgini'nde, altında **Python ortamları**, hello sanal ortamda sağ tıklayıp **Python paketini Yükle**.
2. Merhaba paketini Yükle `pyodbc` kullanarak **PIP**.

     ![Python paketi Yükle iletişim kutusu](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. Merhaba paketini Yükle `django-pyodbc-azure` kullanarak **PIP**.

     ![Python paketi Yükle iletişim kutusu](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. İçinde **Çözüm Gezgini**, hello proje düğümüne sağ tıklayın ve seçin **Python**ve ardından **Django geçirmek**.  Ardından **Django Yetkili Kullanıcısı Oluşturma**’yı seçin.

   Bu hello önceki bölümde oluşturduğumuz hello SQL veritabanı için hello tabloları oluşturur. Merhaba istemleri toocreate toomatch hello kullanıcının hello ilk bölümünde oluşturulan hello sqlite veritabanındaki yoksa bir kullanıcı izleyin.
5. Merhaba uygulamayla çalıştırmak `F5`. İle oluşturulan yoklamalar **örnek yoklamalar Oluştur** ve oy vermeyle gönderilen hello veri hello SQL veritabanında seri.

## <a name="publish-hello-web-app-tooazure-app-service"></a>Yayımlama Hello web uygulama tooAzure uygulama hizmeti
Hello Azure .NET SDK'sı, web web uygulama tooAzure App Service Web Apps kolay bir yolu toodeploy sağlar.

1. İçinde **Çözüm Gezgini**, hello proje düğümüne sağ tıklayın ve seçin **Yayımla**.

     ![Web Yayımlama İletişim Kutusu](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. **Microsoft Azure Web Apps** ’e tıklayın.
3. Tıklayın **yeni** toocreate yeni bir web uygulaması.
4. Hello aşağıdaki alanları doldurun ve **oluşturma**.

   * **Web Uygulaması adı**
   * **App Service planı**
   * **Kaynak grubu**
   * **Bölge**
   * Bırakın **veritabanı sunucusu** çok ayarlamak**veritabanı yok**
5. Diğer tüm varsayılanları kabul edin ve **Yayımla**’ya tıklayın.
6. Web tarayıcınız toohello yayımlanan web uygulamasına otomatik olarak açılır. Hello kullanarak, beklendiği gibi hello web uygulama çalışma görmelisiniz **SQL** Azure üzerinde barındırılan veritabanı.

   Tebrikler!

     ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a>Sonraki adımlar
Visual Studio, Django ve SQL veritabanı için Python araçları hakkında daha fazla bu bağlantılar toolearn izleyin.

* [Visual Studio için Python Araçları Belgeleri]
  * [Web Projeleri]
  * [Bulut Hizmeti Projeleri]
  * [Microsoft Azure’da Uzaktan Hata Ayıklama]
* [Django Belgeleri]
* [SQL Veritabanı]

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Python Geliştirici Merkezi]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Visual Studio için Python Araçları]: http://aka.ms/ptvs
[Visual Studio için Python Araçları 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio Örnekleri VSIX için Python araçları 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025
[VS 2015 için Azure SDK Araçları]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517190
[Visual Studio için Python Araçları Belgeleri]: http://aka.ms/ptvsdocs
[Microsoft Azure’da Uzaktan Hata Ayıklama]: http://go.microsoft.com/fwlink/?LinkId=624026
[Web Projeleri]: http://go.microsoft.com/fwlink/?LinkId=624027
[Bulut Hizmeti Projeleri]: http://go.microsoft.com/fwlink/?LinkId=624028
[Django Belgeleri]: https://www.djangoproject.com/
[SQL Veritabanı]: /documentation/services/sql-database/
