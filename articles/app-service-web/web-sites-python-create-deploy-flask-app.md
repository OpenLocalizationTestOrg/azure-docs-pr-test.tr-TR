---
title: "Azure'da Flask ile Web uygulamaları oluşturma"
description: "Azure üzerinde bir Python web uygulaması çalıştırmayı gösteren bir öğretici."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: b7f4ca3a-0b52-4108-90a7-f7e07ac73da0
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/20/2016
ms.author: huvalo
ms.openlocfilehash: 29457a39ee3df0bbdbc9869cdce0e14bd85b7302
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a>Azure'da Flask ile Web uygulamaları oluşturma
Bu öğretici, Python çalıştırmaya başlamak açıklar [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).  Web Apps sınırlı ücretsiz barındırma ve hızlı dağıtım sağlar ve Python’u kullanmanıza olanak tanır!  Uygulamanız büyüdükçe, ücretli barındırmaya geçebilir ve aynı zamanda tüm diğer Azure hizmetleriyle tümleştirebilirsiniz.

Flask web altyapısını kullanarak bir uygulama oluşturacaksınız (Bu öğretici için alternatif sürümleri bkz [Django](web-sites-python-create-deploy-django-app.md) ve [Bottle](web-sites-python-create-deploy-bottle-app.md)).  Azure galerisinden Web sitesi oluşturma, Git dağıtımı ayarlayacak ve depoyu yerel olarak kopyalayın.  Sonra, uygulamayı yerel olarak çalıştıracak, değişiklikler yapacak, yürütecek ve bunları Azure'a ileteceksiniz.  Öğretici, Windows veya Mac/Linux’ta bunun nasıl yapıldığını gösterir.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="prerequisites"></a>Ön koşullar
* Windows, Mac veya Linux
* Python 2.7 ya da 3.4
* setuptools, pip, virtualenv (yalnızca Python 2.7)
* Git
* [Visual Studio için Python Araçları][Visual Studio için Python Araçları] (PTVS) - Not: Bu özellik isteğe bağlıdır

**Not**: TFS yayımlama şu anda Python projeleri için desteklenmiyor.

### <a name="windows"></a>Windows
Python 2.7 ya da 3.4 yüklü (32 bit) değilse, Web Platformu Yükleyicisi'ni kullanarak [Python 2.7 için Azure SDK] veya [Python 3.4 için Azure SDK]’yı yüklemenizi öneririz.  Bu, Python’un 32 bit sürümünü, setuptools, PIP, virtualenv vb.yükler (32 bit Python, Azure ana makinelerde yüklü olandır).  Alternatif olarak, Python’u [python.org] adresinden edinebilirsiniz.

Git için, [Windows için Git] veya [Windows için GitHub]’ı öneririz.  Visual Studio kullanıyorsanız, tümleşik Git desteğini kullanabilirsiniz.

Ayrıca [Visual Studio için Python Araçları 2.2]’yi yüklemenizi öneririz   Bu isteğe bağlıdır, ancak ücretsiz Visual Studio Community 2013 veya Web için Visual Studio Express 2013 içeren [Visual Studio] varsa, bu size mükemmel bir Python IDE verir.

### <a name="maclinux"></a>Mac/Linux
Python ve Git sizde zaten yüklü olmalıdır, ancak Python 2.7 veya 3.4 olduğundan emin olun.

## <a name="web-app-create-on-the-azure-portal"></a>Web uygulaması oluşturma Azure portalında
Uygulamanızı oluşturmanın ilk adımı, [Azure Portal](https://portal.azure.com) aracılığıyla web uygulaması oluşturmaktır. 

1. Azure Portal’da oturum açın ve sol alt köşede **NEW** düğmesine tıklayın. 
2. **Web + Mobil**’e tıklayın.
3. Arama kutusuna, "python" yazın.
4. Arama sonuçlarında seçin **Flask**, ardından **oluşturma**.
5. Yeni bir uygulama hizmeti planı ve yeni bir kaynak grubu oluşturma gibi yeni Flask uygulamasını yapılandırın. Sonra, **Oluştur**’a tıklayın.
6. Yeni oluşturulan web uygulamanız için, [Azure Uygulama Hizmeti’nde Yerel Git Dağıtımı](app-service-deploy-local-git.md) başlığındaki yönergeleri izleyerek Git yayımlamayı yapılandırın.

## <a name="application-overview"></a>Uygulamaya Genel Bakış
### <a name="git-repository-contents"></a>Git deposu içeriği
Burada, sonraki bölümde kopyalayacağımız, ilk Git deposunda bulacağınız dosyalara bir genel bakış yer alır.

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

Uygulama için ana kaynaklar  Ana düzenle birlikte 3 sayfadan (dizin, hakkında, iletişim) oluşur.  Statik içerik ve betikler bootstrap, jquery, modernize ve yanıtı içerir.

    \runserver.py

Yerel Geliştirme Sunucusu desteği. Uygulamayı yerel olarak çalıştırmak için bunu kullanın.

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

[Visual Studio için Python Araçları] ile birlikte kullanmak için proje dosyaları.

    \ptvs_virtualenv_proxy.py

Sanal ortamlar için IIS proxy ve PTVS uzaktan hata ayıklama desteği

    \requirements.txt

Bu uygulamaya dış paketler gerekir. Dağıtım betiği pip bu dosyada listelenen paketleri pip yükler.

    \web.2.7.config
    \web.3.4.config

IIS yapılandırma dosyaları.  Dağıtım betiği, uygun web.x.y.config’i kullanır ve bunu web.config olarak kopyalar.

### <a name="optional-files---customizing-deployment"></a>İsteğe bağlı dosyalar - Dağıtımı özelleştirme
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a>İsteğe bağlı dosyalar - Python çalışma zamanı
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a>Sunucu üzerindeki ek dosyalar
Bazı dosyalar sunucuda yer alır ancak git deposuna eklenmez.  Bunlar dağıtım betiği tarafından oluşturulur.

    \web.config

IIS yapılandırma dosyası.  Her dağıtımda web.x.y.config tarafından oluşturulur.

    \env\

Python sanal ortamı.  Uygulamasında uyumlu sanal ortam zaten yoksa dağıtım ırasında oluşturulur.  Requirements.txt içinde listelenen paketler pip yüklüdür, ancak paketler zaten yüklü ise pip yüklemeyi atlar.

Sonraki 3 bölümde farklı 3 ortamda web uygulaması geliştirmeye devam etme açıklanmaktadır:

* Windows, Visual Studio için Python Araçları ile
* Windows, komut satırı ile
* Mac/Linux, komut satırı ile

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a>Web uygulaması geliştirme - Windows - Visual Studio için Python Araçları
### <a name="clone-the-repository"></a>Depoyu kopyalama
İlk olarak, Azure Portal'da sağlanan URL'yi kullanarak depoyu kopyalayın. Daha fazla bilgi için bkz. [Azure Uygulama Hizmeti’nde Yerel Git Dağıtımı](app-service-deploy-local-git.md).

Depo kök dizininde bulunan çözüm dosyasını (.sln) açın.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a>Sanal ortamı oluşturun.
Şimdi, yerel geliştirme için sanal bir ortam oluşturacağız.  Sağ **Python Ortamları**’na sağ tıklayın **Sanal Ortam Ekle...** seçeneğini seçin.

* Ortam adının `env` olduğundan emin olun.
* Temel yorumlayıcıyı seçin.  Web uygulamanız için seçilen Python ile aynı sürümü kullandığınızdan emin olun (runtime.txt içinde veya Azure Portal’da uygulamanızın **Uygulama Ayarları** dikey penceresinde).
* Paketleri indirme ve yükleme seçeneğinin işaretli olduğundan emin olun.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

**Oluştur**’a tıklayın.  Bu, sanal ortamı oluşturur ve requirements.txt içinde listelenen bağımlılıkları yükler.

### <a name="run-using-development-server"></a>Geliştirme sunucusu kullanarak çalıştırma
Hata ayıklamayı başlatmak için F5 tuşuna basın, böylece web tarayıcınız yerel olarak çalışan sayfaya otomatik olarak açılır.

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

Kaynaklarda kesme noktalarını ayarlayabilir, gözcü pencerelerini kullanabilirsiniz vb.  Çeşitli özellikler hakkında daha fazla bilgi için bkz. [Visual Studio Belgeleri için Python Araçları].

### <a name="make-changes"></a>Değişiklik yapma
Şimdi uygulama kaynakları ve/veya şablonlarında değişiklikler yapmayı deneyebilirsiniz.

Değişikliklerinizi test ettikten sonra bunları Git deposuna kaydedin:

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a>Daha fazla paket yükleme
Uygulamanızın Python ve Flask ötesinde bağımlılıkları olabilir.

Pip kullanarak ek paketleri yükleyebilirsiniz.  Bir paketi yüklemek için, sanal ortamda sağ tıklayıp **Python Paketini Yükle**’yi seçin.

Örneğin, size Azure Storage, Service Bus ve diğer Azure hizmetleri için erişim imkanı sağlayan, Python için Azure SDK'yı yüklemek için şunu girin: `azure`

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

Sanal ortamda sağ tıklayıp **requirements.txt oluştur**’u seçerek requirements.txt dosyasını güncelleştirin.

Ardından, requirements.txt dosyasındaki değişiklikleri Git deposuna uygulayın.

### <a name="deploy-to-azure"></a>Azure’a dağıtma
Bir dağıtımı tetiklemek için tıklatın **Eşitle** veya **İlet**’e tıklayın.  Eşitleme, iletme ve çekme işlemini yapar.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

Sanal ortam, yükleme paketleri vb. oluşturacağında, ilk dağıtımın gerçekleşmesi biraz zaman alır.

Visual Studio dağıtımın ilerleme durumunu göstermez.  Çıktıyı gözden geçirmek isterseniz, üzerinde bakın [Sorun Giderme - Dağıtım](#troubleshooting-deployment)’daki bölüme bakın.

Yaptığınız değişiklikleri görmek için Azure URL'sine gidin.

## <a name="web-app-development---windows---command-line"></a>Web uygulaması geliştirme - Windows - komut satırı
### <a name="clone-the-repository"></a>Depoyu kopyalama
İlk olarak, Azure Portal'da sağlanan URL'yi kullanarak depoyu kopyalayın ve uzak olarak Azure deposunu ekleyin. Daha fazla bilgi için bkz. [Azure Uygulama Hizmeti’nde Yerel Git Dağıtımı](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>Sanal ortamı oluşturun.
Geliştirme amacına yönelik yeni bir sanal ortam oluşturacağız (bunu depoya eklemeyin).  Uygulama üzerinde çalışan her geliştiricinin yerel olarak kendininkini oluşturacağı şekilde, Python’daki sanal ortamlar yeniden yerleştirilebilir değildir.

Web uygulamanız için seçilen Python ile aynı sürümü kullandığınızdan emin olun (runtime.txt içinde veya Azure Portal’da uygulamanızın **Uygulama Ayarları** dikey penceresinde).

Python 2.7:

    c:\python27\python.exe -m virtualenv env

Python 3.4:

    c:\python34\python.exe -m venv env

Uygulamanız için gereken herhangi bir dış paketi yükleyin. Sanal ortamınıza paketleri yüklemek için depo kökündeki requirements.txt dosyasını kullanabilirsiniz:

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a>Geliştirme sunucusu kullanarak çalıştırma
Aşağıdaki komutla bir geliştirme sunucusu altında uygulamayı başlatabilirsiniz:

    env\scripts\python runserver.py

Konsol URL’yi ve sunucunun dinlediği bağlantı noktasını görüntüler:

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

Sonra, bu URL için web tarayıcınızı açın.

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a>Değişiklik yapma
Şimdi uygulama kaynakları ve/veya şablonlarında değişiklikler yapmayı deneyebilirsiniz.

Değişikliklerinizi test ettikten sonra bunları Git deposuna kaydedin:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Daha fazla paket yükleme
Uygulamanızın Python ve Flask ötesinde bağımlılıkları olabilir.

Pip kullanarak ek paketleri yükleyebilirsiniz.  Örneğin, size Azure Storage, Service Bus ve diğer Azure hizmetleri için erişim imkanı sağlayan, Python için Azure SDK'yı yüklemek için aşağıdakileri yazın:

    env\scripts\pip install azure

Requirements.txt dosyasını güncelleştirdiğinizden emin olun:

    env\scripts\pip freeze > requirements.txt

Değişiklikleri uygulayın:

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a>Azure’a dağıtma
Bir dağıtımı tetiklemek için, değişiklikleri Azure’a gönderin:

    git push azure master

Sanal ortam oluşturma, paketleri yükleme, web.config oluşturma dahil dağıtım betiği çıktısını görürsünüz.

Yaptığınız değişiklikleri görmek için Azure URL'sine gidin.

## <a name="web-app-development---maclinux---command-line"></a>Web uygulaması geliştirme - Mac/Linux - komut satırı
### <a name="clone-the-repository"></a>Depoyu kopyalama
İlk olarak, Azure Portal'da sağlanan URL'yi kullanarak depoyu kopyalayın ve uzak olarak Azure deposunu ekleyin. Daha fazla bilgi için bkz. [Azure Uygulama Hizmeti’nde Yerel Git Dağıtımı](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>Sanal ortamı oluşturun.
Geliştirme amacına yönelik yeni bir sanal ortam oluşturacağız (bunu depoya eklemeyin).  Uygulama üzerinde çalışan her geliştiricinin yerel olarak kendininkini oluşturacağı şekilde, Python’daki sanal ortamlar yeniden yerleştirilebilir değildir.

Web uygulamanız için seçilen Python ile aynı sürümü kullandığınızdan emin olun (runtime.txt içinde veya Azure Portal’da uygulamanızın **Uygulama Ayarları** dikey penceresinde).

Python 2.7:

    python -m virtualenv env

Python 3.4:

    python -m venv env
veya pyvenv env

Uygulamanız için gereken herhangi bir dış paketi yükleyin. Sanal ortamınıza paketleri yüklemek için depo kökündeki requirements.txt dosyasını kullanabilirsiniz:

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a>Geliştirme sunucusu kullanarak çalıştırma
Aşağıdaki komutla bir geliştirme sunucusu altında uygulamayı başlatabilirsiniz:

    env/bin/python runserver.py

Konsol URL’yi ve sunucunun dinlediği bağlantı noktasını görüntüler:

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

Sonra, bu URL için web tarayıcınızı açın.

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a>Değişiklik yapma
Şimdi uygulama kaynakları ve/veya şablonlarında değişiklikler yapmayı deneyebilirsiniz.

Değişikliklerinizi test ettikten sonra bunları Git deposuna kaydedin:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Daha fazla paket yükleme
Uygulamanızın Python ve Flask ötesinde bağımlılıkları olabilir.

Pip kullanarak ek paketleri yükleyebilirsiniz.  Örneğin, size Azure Storage, Service Bus ve diğer Azure hizmetleri için erişim imkanı sağlayan, Python için Azure SDK'yı yüklemek için aşağıdakileri yazın:

    env/bin/pip install azure

Requirements.txt dosyasını güncelleştirdiğinizden emin olun:

    env/bin/pip freeze > requirements.txt

Değişiklikleri uygulayın:

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a>Azure’a dağıtma
Bir dağıtımı tetiklemek için, değişiklikleri Azure’a gönderin:

    git push azure master

Sanal ortam oluşturma, paketleri yükleme, web.config oluşturma dahil dağıtım betiği çıktısını görürsünüz.

Yaptığınız değişiklikleri görmek için Azure URL'sine gidin.

## <a name="troubleshooting---package-installation"></a>Sorun giderme - Paket Yükleme
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>Sorun giderme - Sanal Ortam
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>Sonraki Adımlar
Visual Studio için Flask ve Python araçları hakkında daha fazla bilgi için aşağıdaki bağlantıları izleyin: 

* [Flask belgeleri]
* [Visual Studio Belgeleri için Python Araçları]

Azure tablo depolaması ve MongoDB kullanma hakkında daha fazla bilgi için:

* [Flask ve Visual Studio için Python araçları ile azure'da MongoDB]
* [Flask ve Visual Studio için Python araçları ile azure'da Azure tablo depolaması]

Daha fazla bilgi için Ayrıca bkz. [Python Geliştirici Merkezi](/develop/python/).

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Flask ve Visual Studio için Python araçları ile azure'da MongoDB]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure
[Flask ve Visual Studio için Python araçları ile azure'da Azure tablo depolaması]: web-sites-python-ptvs-flask-table-storage.md

<!--External Link references-->
[Python 2.7 için Azure SDK]: http://go.microsoft.com/fwlink/?linkid=254281
[Python 3.4 için Azure SDK]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Windows için Git]: http://msysgit.github.io/
[Windows için GitHub]: https://windows.github.com/
[Visual Studio için Python Araçları]: http://aka.ms/ptvs
[Visual Studio için Python Araçları 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[Visual Studio Belgeleri için Python Araçları]: http://aka.ms/ptvsdocs
[Flask belgeleri]: http://flask.pocoo.org/ 

