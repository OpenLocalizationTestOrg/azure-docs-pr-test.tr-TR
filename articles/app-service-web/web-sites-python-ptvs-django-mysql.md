---
title: "aaaDjango ve Visual Studio için Python araçları 2.2 ile azure'da MySQL"
description: "Nasıl toouse hello Python araçları Visual Studio toocreate için bir MySQL veritabanı örneğinde veri depolayan bir Django web uygulaması öğrenin ve tooAzure App Service Web Apps dağıtın."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: c60a50b5-8b5e-4818-a442-16362273dabb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1597c391d20c8e8ef629b4e4d05c9eb64c83bffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a>Visual Studio için Python Araçları 2.2 ile Azure’da Django ve MySQL
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Bu öğreticide kullanacaksınız [Visual Studio için Python Araçları](https://www.visualstudio.com/vs/python) toocreate basit bir web uygulamasına hello PTVS örnek şablonlarından birini kullanarak yoklar. Nasıl toouse MySQL hizmeti Azure üzerinde barındırılan, nasıl tooconfigure hello web uygulama toouse MySQL ve nasıl toopublish hello web uygulaması çok öğreneceksiniz[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

> [!NOTE]
> Bu öğreticide yer alan hello bilgi de video aşağıdaki hello bulunmaktadır:
> 
> [PTVS 2.1: MySQL ile Django uygulaması][video]
> 
> 

Merhaba bkz [Python Geliştirici Merkezi] Bottle kullanarak PTVS ile Azure App Service Web Apps geliştirmeyi kapsayan diğer makaleler için Flask ve Django web altyapılarını Azure Table Storage, MySQL ve SQL Database hizmetleriyle. Bu makale App Service'e odaklanmakla birlikte hello adımlar geliştirirken benzer [Azure Cloud Services].

## <a name="prerequisites"></a>Ön koşullar
* Visual Studio 2015
* [Python 2.7 32 bit] veya [Python 3.4 32 bit]
* [Visual Studio için Python Araçları 2.2]
* [Visual Studio Örnekleri VSIX için Python araçları 2.2]
* [VS 2015 için Azure SDK Araçları]
* Django 1.9 veya üzeri

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of hello hello previous include. -->

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekli değildir.
> 
> 

## <a name="create-hello-project"></a>Başlangıç projesi oluşturma
Bu bölümde, örnek şablonu kullanarak bir Visual Studio projesi oluşturacaksınız. Bir sanal ortam oluşturacak ve gerekli paketleri yükleyeceksiniz. Sqlite kullanarak yerel bir veritabanı oluşturacaksınız. Ardından hello uygulamayı yerel olarak çalışacaksınız.

1. Visual Studio'da, **Dosya**, **Yeni Proje**’yi seçin.
2. Proje şablonlarını hello hello [Visual Studio Örnekleri VSIX için Python araçları 2.2] altında kullanılabilir **Python**, **örnekleri**. Seçin **yoklamalar Django Web projesi** ve Tamam toocreate hello proje'yi tıklatın.
   
    ![Yeni Proje İletişim Kutusu](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. İstendiğinde tooinstall dış paketler olacaktır. **Sanal bir ortama yükle**’yi seçin.
   
    ![Dış Paketler İletişim Kutusu](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. Seçin **Python 2.7** veya **Python 3.4** hello temel yorumlayıcı olarak.
   
    ![Sanal Ortama Ekle İletişim Kutusu](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. İçinde **Çözüm Gezgini**, hello proje düğümüne sağ tıklayın ve seçin **Python**ve ardından **Django geçirmek**.  Ardından **Django Yetkili Kullanıcısı Oluşturma**’yı seçin.
6. Bu, Django yönetim konsolunu açın ve hello proje klasöründe bir sqlite veritabanı oluşturun. Merhaba istemleri toocreate kullanıcı izleyin.
7. Merhaba uygulaması tuşlarına basarak çalıştığını onaylayın `F5`.
8. Tıklatın **oturum** hello gezinti çubuğunda hello üstünde.
   
    ![Django Gezinti Çubuğu](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. Hello veritabanını eşitlediğinizde, oluşturduğunuz hello kullanıcı için Hello kimlik bilgilerini girin.
   
    ![Oturum Açma Formu](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. **Örnek Yoklamalar Oluştur**’a tıklayın.
    
     ![Örnek Yoklamalar Oluştur](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. Bir yoklamaya tıklayın ve oy verin.
    
     ![Örnek Yoklamalarda Oy Verme](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a>MySQL Veritabanı Oluşturma
Merhaba veritabanı için Azure'da ClearDB MySQL barındırılan veritabanı oluşturacaksınız.

Alternatif olarak, Azure'da çalışan kendi sanal makinenizi oluşturabilir ve ardından MySQL’i kendiniz yönetebilirsiniz.

Aşağıdaki adımları izleyerek, boş bir plan ile bir veritabanı oluşturabilirsiniz.

1. İçinde toohello oturum [Azure Portal].
2. Merhaba hello Gezinti bölmesinin üst kısmında tıklatın **yeni**, ardından **veri + depolama**ve ardından **MySQL veritabanı**.
3. Yeni bir kaynak grubu oluşturarak yeni MySQL veritabanı Hello yapılandırın ve hello uygun bir konum seçin.
4. Merhaba MySQL veritabanı oluşturulduktan sonra tıklatın **özellikleri** hello veritabanı dikey penceresinde.
5. Merhaba Kopyala düğmesine tooput hello değerini kullanın **bağlantı DİZESİ** hello Panosu'nda.

## <a name="configure-hello-project"></a>Merhaba projeyi yapılandırma
Bu bölümde, az önce oluşturduğunuz web uygulaması toouse hello MySQL Veritabanımıza yapılandıracaksınız. Ek Python paketlerini gerekli toouse MySQL veritabanlarını Django ile de yükleyeceksiniz. Ardından hello web uygulamasını yerel olarak çalıştıracaksınız.

1. Visual Studio'da açın **ProjectName**, hello gelen *ProjectName* klasör. Geçici olarak hello Düzenleyicisi'nde hello bağlantı dizesini yapıştırın. Merhaba bağlantı dizesi bu biçimdedir:
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    Değişiklik hello varsayılan veritabanı **altyapısı** toouse MySQL ve kümesi hello değerlerini **adı**, **kullanıcı**, **parola** ve  **Ana bilgisayar** hello gelen **CONNECTIONSTRING**.
   
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': '<Database>',
                'USER': '<User Id>',
                'PASSWORD': '<Password>',
                'HOST': '<Data Source>',
                'PORT': '',
            }
        }
2. Çözüm Gezgini'nde, altında **Python ortamları**, hello sanal ortamda sağ tıklayıp **Python paketini Yükle**.
3. Merhaba paketini Yükle `mysqlclient` kullanarak **PIP**.
   
    ![Paketi Yükle İletişim Kutusu](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. İçinde **Çözüm Gezgini**, hello proje düğümüne sağ tıklayın ve seçin **Python**ve ardından **Django geçirmek**.  Ardından **Django Yetkili Kullanıcısı Oluşturma**’yı seçin.
   
    Bu hello tablolar için hello önceki bölümde oluşturduğunuz hello MySQL veritabanı oluşturur. Merhaba istemleri toocreate toomatch hello kullanıcının bu makalenin hello ilk bölümünde oluşturulan hello sqlite veritabanındaki yoksa bir kullanıcı izleyin.
5. Merhaba uygulamayla çalıştırmak `F5`. İle oluşturulan yoklamalar **örnek yoklamalar Oluştur** ve oy vermeyle gönderilen hello veri hello MySQL veritabanında seri.

## <a name="publish-hello-web-app-tooazure-app-service"></a>Yayımlama Hello web uygulama tooAzure uygulama hizmeti
Hello Azure .NET SDK'sını kolay bir yolu toodeploy web uygulama tooAzure uygulama hizmeti sağlar.

1. İçinde **Çözüm Gezgini**, hello proje düğümüne sağ tıklayın ve seçin **Yayımla**.
   
    ![Web Yayımlama İletişim Kutusu](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. **Microsoft Azure Uygulama Hizmeti**’ne tıklayın.
3. Tıklayın **yeni** toocreate yeni bir web uygulaması.
4. Hello aşağıdaki alanları doldurun ve **oluşturma**:
   
   * **Web Uygulaması adı**
   * **App Service planı**
   * **Kaynak grubu**
   * **Bölge**
   * Bırakın **veritabanı sunucusu** çok ayarlamak**veritabanı yok**
5. Diğer tüm varsayılanları kabul edin ve **Yayımla**’ya tıklayın.
6. Web tarayıcınız toohello yayımlanan web uygulamasına otomatik olarak açılır. Hello kullanarak, beklendiği gibi hello web uygulama çalışma görmelisiniz **MySQL** Azure üzerinde barındırılan veritabanı.
   
    ![Web Tarayıcısı](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    Tebrikler! MySQL tabanlı web uygulama tooAzure başarıyla yayımladınız.

## <a name="next-steps"></a>Sonraki adımlar
Visual Studio, Django ve MySQL için Python araçları hakkında daha fazla bu bağlantılar toolearn izleyin.

* [Visual Studio için Python Araçları Belgeleri]
  * [Web Projeleri]
  * [Bulut Hizmeti Projeleri]
  * [Microsoft Azure’da Uzaktan Hata Ayıklama]
* [Django Belgeleri]
* [MySQL]

Daha fazla bilgi için bkz: Merhaba [Python Geliştirici Merkezi](/develop/python/).

<!--Link references-->

[Python Geliştirici Merkezi]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Azure Portal]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Visual Studio için Python Araçları 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio Örnekleri VSIX için Python araçları 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025
[VS 2015 için Azure SDK Araçları]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32 bit]: http://go.microsoft.com/fwlink/?LinkId=517191
[Visual Studio için Python Araçları Belgeleri]: http://aka.ms/ptvsdocs
[Microsoft Azure’da Uzaktan Hata Ayıklama]: http://go.microsoft.com/fwlink/?LinkId=624026
[Web Projeleri]: http://go.microsoft.com/fwlink/?LinkId=624027
[Bulut Hizmeti Projeleri]: http://go.microsoft.com/fwlink/?LinkId=624028
[Django Belgeleri]: https://www.djangoproject.com/
[MySQL]: http://www.mysql.com/
[video]: http://youtu.be/oKCApIrS0Lo
