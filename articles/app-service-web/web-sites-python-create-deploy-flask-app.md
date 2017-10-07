---
title: "azure'da Flask ile aaaCreating web uygulamaları"
description: "Azure üzerinde bir Python web uygulaması toorunning tanıtır Öğreticisi."
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
ms.openlocfilehash: 3362047b3106b4380b5971e47cbd8042d38a792b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a>Azure'da Flask ile Web uygulamaları oluşturma
Bu öğretici tooget Python çalıştırmaya nasıl başlatılacağını açıklar [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).  Web Apps sınırlı ücretsiz barındırma ve hızlı dağıtım sağlar ve Python’u kullanmanıza olanak tanır!  Uygulamanız büyüdükçe, toopaid barındırma geçiş yapabilirsiniz ve tüm ile de tümleştirebilir gibi diğer Azure hizmetleriyle hello.

Merhaba Flask web altyapısını kullanarak bir uygulama oluşturacaksınız (Bu öğretici için alternatif sürümleri bkz [Django](web-sites-python-create-deploy-django-app.md) ve [Bottle](web-sites-python-create-deploy-bottle-app.md)).  Azure galerisinde hello hello Web sitesi oluşturma Git dağıtımı ayarlayacak ve hello depoyu yerel olarak kopyalayacaksınız.  Ardından, hello uygulamayı yerel olarak çalıştırmak, değişiklik, yürütme ve bunları tooAzure gönderme.  Eğitmen gösterir nasıl hello toodo bu Windows veya Mac/Linux.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
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
Python 2.7 ya da 3.4 yüklü (32 bit) değilse, Web Platformu Yükleyicisi'ni kullanarak [Python 2.7 için Azure SDK] veya [Python 3.4 için Azure SDK]’yı yüklemenizi öneririz.  Bu, Python, setuptools, PIP, virtualenv, (32 bit Python hello Azure ana makinelerde yüklü olandır) "Merhaba 32-bit sürümünü yükler.  Alternatif olarak, Python’u [python.org] adresinden edinebilirsiniz.

Git için, [Windows için Git] veya [Windows için GitHub]’ı öneririz.  Visual Studio kullanıyorsanız hello tümleşik Git desteğini kullanabilirsiniz.

Ayrıca [Visual Studio için Python Araçları 2.2]’yi yüklemenizi öneririz   Bu isteğe bağlı, ancak varsa [Visual Studio]hello dahil olmak üzere ücretsiz Visual Studio Community 2013 veya Visual Studio Express 2013 Web sonra bu mükemmel bir Python IDE verir.

### <a name="maclinux"></a>Mac/Linux
Python ve Git sizde zaten yüklü olmalıdır, ancak Python 2.7 veya 3.4 olduğundan emin olun.

## <a name="web-app-create-on-hello-azure-portal"></a>Azure Portal hello üzerinde Web uygulaması oluşturma
Merhaba uygulamanızı oluşturmanın ilk adımı olan toocreate hello web uygulaması hello aracılığıyla [Azure Portal](https://portal.azure.com). 

1. Oturum hello Azure Portal ve hello tıklatın **yeni** hello sol alt köşedeki düğmesini. 
2. **Web + Mobil**’e tıklayın.
3. Merhaba arama kutusuna "python" yazın.
4. Merhaba arama sonuçlarında seçin **Flask**, ardından **oluşturma**.
5. Yeni bir uygulama hizmeti planı ve yeni bir kaynak grubu oluşturma gibi hello yeni Flask uygulamasını yapılandırın. Sonra, **Oluştur**’a tıklayın.
6. Merhaba yönergeleri izleyerek Git yayımlamayı yeni oluşturulan web uygulamanız için yapılandırma [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md).

## <a name="application-overview"></a>Uygulamaya Genel Bakış
### <a name="git-repository-contents"></a>Git deposu içeriği
Burada, hangi hello sonraki bölümde kopyalama hello ilk Git deposunda bulabilirsiniz hello dosyaları genel bir bakış verilmiştir.

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

Merhaba uygulaması için ana kaynaklar.  Ana düzenle birlikte 3 sayfadan (dizin, hakkında, iletişim) oluşur.  Statik içerik ve betikler bootstrap, jquery, modernize ve yanıtı içerir.

    \runserver.py

Yerel Geliştirme Sunucusu desteği. Bu toorun hello uygulamayı yerel olarak kullanın.

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

[Visual Studio için Python Araçları] ile birlikte kullanmak için proje dosyaları.

    \ptvs_virtualenv_proxy.py

Sanal ortamlar için IIS proxy ve PTVS uzaktan hata ayıklama desteği

    \requirements.txt

Bu uygulamaya dış paketler gerekir. Bu dosyada listelenen yükleme hello paketleri Hello dağıtım betiği pip.

    \web.2.7.config
    \web.3.4.config

IIS yapılandırma dosyaları.  Merhaba dağıtım betiği hello uygun Web.x.y.config'i kullanır ve bunu web.config olarak kopyalar.

### <a name="optional-files---customizing-deployment"></a>İsteğe bağlı dosyalar - Dağıtımı özelleştirme
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a>İsteğe bağlı dosyalar - Python çalışma zamanı
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a>Sunucu üzerindeki ek dosyalar
Bazı dosyalar hello sunucuda var, ancak toohello git deposuna eklenmez.  Bunlar hello dağıtım betiği tarafından oluşturulur.

    \web.config

IIS yapılandırma dosyası.  Her dağıtımda web.x.y.config tarafından oluşturulur.

    \env\

Python sanal ortamı.  Dağıtım sırasında hello uygulamasında uyumlu sanal ortamın zaten mevcut değilse oluşturulur.  Requirements.txt içinde listelenen paketler pip yüklüdür, ancak hello paketler zaten yüklü ise pip yüklemeyi atlar.

Merhaba sonraki 3 bölümde nasıl tooproceed hello ile web uygulaması geliştirme altında farklı 3 ortamda açıklanmaktadır:

* Windows, Visual Studio için Python Araçları ile
* Windows, komut satırı ile
* Mac/Linux, komut satırı ile

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a>Web uygulaması geliştirme - Windows - Visual Studio için Python Araçları
### <a name="clone-hello-repository"></a>Kopya hello deposu
İlk olarak, Azure Portal hello üzerinde sağlanan hello URL'yi kullanarak hello depoyu kopyalayın. Daha fazla bilgi için bkz: [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md).

Merhaba hello depo kök dizininde bulunan hello çözüm dosyasını (.sln) açın.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a>Sanal ortamı oluşturun.
Şimdi, yerel geliştirme için sanal bir ortam oluşturacağız.  Sağ **Python Ortamları**’na sağ tıklayın **Sanal Ortam Ekle...** seçeneğini seçin.

* Merhaba ortamı Hello adı olduğundan emin olun `env`.
* Merhaba temel yorumlayıcıyı seçin.  Toouse hello web uygulamanız için seçilen Python ile aynı sürümü olduğundan emin olun (runtime.txt veya hello **uygulama ayarları** hello Azure Portal, web uygulamanızın dikey penceresinde).
* Merhaba seçeneği toodownload ve yükleme paketleri işaretli olduğundan emin olun.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

**Oluştur**'a tıklayın.  Bu işlem hello sanal ortam oluşturacak ve requirements.txt içinde listelenen bağımlılıkları yükler.

### <a name="run-using-development-server"></a>Geliştirme sunucusu kullanarak çalıştırma
Otomatik olarak hata ayıklama tuşuna F5 toostart ve web tarayıcınız yerel olarak çalışan toohello sayfasını açar.

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

Kesme noktaları hello kaynakları, kullanım hello Gözcü pencerelerini, vb. ayarlayabilirsiniz.  Merhaba bkz [Visual Studio belgeleri için Python Araçları] hakkında daha fazla bilgi için çeşitli özellikler hello.

### <a name="make-changes"></a>Değişiklik yapma
Şimdi değişiklikleri toohello uygulama kaynakları ve/veya şablonlarında yapmayı deneyebilirsiniz.

Değişikliklerinizi test ettikten sonra bunları toohello Git deposuna kaydedin:

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a>Daha fazla paket yükleme
Uygulamanızın Python ve Flask ötesinde bağımlılıkları olabilir.

Pip kullanarak ek paketleri yükleyebilirsiniz.  bir paket tooinstall sağ tıklayın hello sanal ortam ve select **Python paketini Yükle**.

Örneğin, tooinstall Merhaba, tooAzure depolama, service bus ve diğer Azure hizmetleriyle erişmenizi girin Python için Azure SDK `azure`:

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

Merhaba sanal ortamda sağ tıklayıp **requirements.txt Oluştur** tooupdate requirements.txt.

Ardından, hello değişiklikleri toorequirements.txt toohello Git deposuna uygulayın.

### <a name="deploy-tooazure"></a>TooAzure dağıtma
bir dağıtım tootrigger tıklayın **eşitleme** veya **anında**.  Eşitleme, iletme ve çekme işlemini yapar.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

bir sanal ortam, yükleme paketleri vb. oluşturacağı gibi hello ilk dağıtım biraz zaman alabilir.

Visual Studio hello hello dağıtımının ilerlemesini göstermez.  Tooreview hello çıkış isterseniz hello bölümüne bakarak [sorun giderme - dağıtım](#troubleshooting-deployment).

Toohello Azure URL tooview değişikliklerinizi göz atın.

## <a name="web-app-development---windows---command-line"></a>Web uygulaması geliştirme - Windows - komut satırı
### <a name="clone-hello-repository"></a>Kopya hello deposu
İlk olarak, Azure Portal hello üzerinde sağlanan hello URL'yi kullanarak hello depoyu kopyalayın ve uzak olarak hello Azure deposunu ekleyin. Daha fazla bilgi için bkz: [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>Sanal ortamı oluşturun.
(Bunu toohello depoya eklemeyin) geliştirme amacıyla yeni bir sanal ortam oluşturacağız.  Sanal ortamlar Hello uygulama üzerinde çalışan her geliştiricinin yerel olarak Kendininkini oluşturacağı şekilde python'daki, değildir.

Toouse hello web uygulamanız için seçilen Python ile aynı sürümü olduğundan emin olun (runtime.txt veya hello **uygulama ayarları** hello Azure Portal, web uygulamanızın dikey penceresinde).

Python 2.7:

    c:\python27\python.exe -m virtualenv env

Python 3.4:

    c:\python34\python.exe -m venv env

Uygulamanız için gereken herhangi bir dış paketi yükleyin. Sanal ortamınıza hello hello depo tooinstall hello paketleri kökünde hello requirements.txt dosyasını kullanabilirsiniz:

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a>Geliştirme sunucusu kullanarak çalıştırma
Komutu aşağıdaki hello ile Merhaba uygulaması geliştirme sunucusu altında başlatabilirsiniz:

    env\scripts\python runserver.py

Merhaba konsol hello URL'si gösterilir ve bağlantı noktası hello sunucu dinler:

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

Sonra web tarayıcısı toothat URL'nizi açın.

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a>Değişiklik yapma
Şimdi değişiklikleri toohello uygulama kaynakları ve/veya şablonlarında yapmayı deneyebilirsiniz.

Değişikliklerinizi test ettikten sonra bunları toohello Git deposuna kaydedin:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Daha fazla paket yükleme
Uygulamanızın Python ve Flask ötesinde bağımlılıkları olabilir.

Pip kullanarak ek paketleri yükleyebilirsiniz.  Örneğin, tooinstall Merhaba, imkanı sağlayan, Python için Azure SDK tooAzure depolama, service bus ve diğer Azure hizmetleriyle türü erişebilirsiniz:

    env\scripts\pip install azure

Tooupdate requirements.txt emin olun:

    env\scripts\pip freeze > requirements.txt

Merhaba değişiklikleri uygulayın:

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>TooAzure dağıtma
bir dağıtım tootrigger, anında iletme hello tooAzure değiştirir:

    git push azure master

Merhaba Merhaba, sanal ortam oluşturma, paketleri yükleme, web.config oluşturma dahil dağıtım betiği çıktısını görürsünüz.

Toohello Azure URL tooview değişikliklerinizi göz atın.

## <a name="web-app-development---maclinux---command-line"></a>Web uygulaması geliştirme - Mac/Linux - komut satırı
### <a name="clone-hello-repository"></a>Kopya hello deposu
İlk olarak, Azure Portal hello üzerinde sağlanan hello URL'yi kullanarak hello depoyu kopyalayın ve uzak olarak hello Azure deposunu ekleyin. Daha fazla bilgi için bkz: [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>Sanal ortamı oluşturun.
(Bunu toohello depoya eklemeyin) geliştirme amacıyla yeni bir sanal ortam oluşturacağız.  Sanal ortamlar Hello uygulama üzerinde çalışan her geliştiricinin yerel olarak Kendininkini oluşturacağı şekilde python'daki, değildir.

Toouse hello web uygulamanız için seçilen Python ile aynı sürümü olduğundan emin olun (runtime.txt veya hello **uygulama ayarları** hello Azure Portal, web uygulamanızın dikey penceresinde).

Python 2.7:

    python -m virtualenv env

Python 3.4:

    python -m venv env
veya pyvenv env

Uygulamanız için gereken herhangi bir dış paketi yükleyin. Sanal ortamınıza hello hello depo tooinstall hello paketleri kökünde hello requirements.txt dosyasını kullanabilirsiniz:

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a>Geliştirme sunucusu kullanarak çalıştırma
Komutu aşağıdaki hello ile Merhaba uygulaması geliştirme sunucusu altında başlatabilirsiniz:

    env/bin/python runserver.py

Merhaba konsol hello URL'si gösterilir ve bağlantı noktası hello sunucu dinler:

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

Sonra web tarayıcısı toothat URL'nizi açın.

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a>Değişiklik yapma
Şimdi değişiklikleri toohello uygulama kaynakları ve/veya şablonlarında yapmayı deneyebilirsiniz.

Değişikliklerinizi test ettikten sonra bunları toohello Git deposuna kaydedin:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Daha fazla paket yükleme
Uygulamanızın Python ve Flask ötesinde bağımlılıkları olabilir.

Pip kullanarak ek paketleri yükleyebilirsiniz.  Örneğin, tooinstall Merhaba, imkanı sağlayan, Python için Azure SDK tooAzure depolama, service bus ve diğer Azure hizmetleriyle türü erişebilirsiniz:

    env/bin/pip install azure

Tooupdate requirements.txt emin olun:

    env/bin/pip freeze > requirements.txt

Merhaba değişiklikleri uygulayın:

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>TooAzure dağıtma
bir dağıtım tootrigger, anında iletme hello tooAzure değiştirir:

    git push azure master

Merhaba Merhaba, sanal ortam oluşturma, paketleri yükleme, web.config oluşturma dahil dağıtım betiği çıktısını görürsünüz.

Toohello Azure URL tooview değişikliklerinizi göz atın.

## <a name="troubleshooting---package-installation"></a>Sorun giderme - Paket Yükleme
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>Sorun giderme - Sanal Ortam
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>Sonraki Adımlar
Bu bağlantılar toolearn Flask ve Python araçları hakkında daha fazla bilgi için Visual Studio izleyin: 

* [Flask belgeleri]
* [Visual Studio belgeleri için Python Araçları]

Azure tablo depolaması ve MongoDB kullanma hakkında daha fazla bilgi için:

* [Flask ve Visual Studio için Python araçları ile azure'da MongoDB]
* [Flask ve Visual Studio için Python araçları ile azure'da Azure tablo depolaması]

Daha fazla bilgi için hello Ayrıca bkz. [Python Geliştirici Merkezi](/develop/python/).

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

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
[Visual Studio belgeleri için Python Araçları]: http://aka.ms/ptvsdocs
[Flask belgeleri]: http://flask.pocoo.org/ 

