---
title: "azure'da Django ile aaaCreating web uygulamaları"
description: "Toorunning bir Python web uygulamasını Azure App Service Web Apps tanıtır Öğreticisi."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 9be1a05a-9460-49ae-94fb-9798f82c11cf
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 26a131da358748bd6fe4ee5c114d0a8f91b83cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a>Azure’da Django ile web uygulamaları oluşturma
Bu öğretici tooget te Python çalıştırmaya nasıl başlatılacağını açıklar [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714). Web Apps sınırlı ücretsiz barındırma ve hızlı dağıtım sağlar ve Python’u kullanmanıza olanak tanır! Uygulamanız büyüdükçe, toopaid barındırma geçiş yapabilirsiniz ve tüm ile de tümleştirebilir gibi diğer Azure hizmetleriyle hello.

Merhaba Django web altyapısını kullanarak bir uygulama oluşturacaksınız (Bu öğretici için alternatif sürümleri bkz [Flask](web-sites-python-create-deploy-flask-app.md) ve [Bottle](web-sites-python-create-deploy-bottle-app.md)). Azure Market hello hello web uygulaması oluşturma, Git dağıtımı ayarlayacak ve hello depoyu yerel olarak kopyalayacaksınız. Ardından, hello uygulamayı yerel olarak çalıştırmak, değişiklik, yürütme ve bunları tooAzure gönderme. Eğitmen gösterir nasıl hello toodo bu Windows veya Mac/Linux.

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
Python 2.7 ya da 3.4 yüklü (32 bit) değilse, Web Platformu Yükleyicisi'ni kullanarak [Python 2.7 için Azure SDK] veya [Python 3.4 için Azure SDK]’yı yüklemenizi öneririz. Bu, Python, setuptools, PIP, virtualenv, (32 bit Python hello Azure ana makinelerde yüklü olandır) "Merhaba 32-bit sürümünü yükler. Alternatif olarak, Python’u [python.org] adresinden edinebilirsiniz.

Git için, [Windows için Git] veya [Windows için GitHub]’ı öneririz. Visual Studio kullanıyorsanız hello tümleşik Git desteğini kullanabilirsiniz.

Ayrıca [Visual Studio için Python Araçları 2.2]’yi yüklemenizi öneririz  Bu isteğe bağlı, ancak varsa [Visual Studio]hello dahil olmak üzere ücretsiz Visual Studio Community 2013 veya Visual Studio Express 2013 Web sonra bu mükemmel bir Python IDE verir.

### <a name="maclinux"></a>Mac/Linux
Python ve Git sizde zaten yüklü olmalıdır, ancak Python 2.7 veya 3.4 olduğundan emin olun.

## <a name="web-app-creation-on-portal"></a>Portalda Web Uygulaması Oluşturma
Merhaba uygulamanızı oluşturmanın ilk adımı olan toocreate hello web uygulaması hello aracılığıyla [Azure Portal](https://portal.azure.com).

1. Oturum hello Azure Portal ve hello tıklatın **yeni** hello sol alt köşedeki düğmesini.
2. Merhaba arama kutusuna "python" yazın.
3. Merhaba arama sonuçlarında seçin **Django** (PTVS tarafından yayımlanan), ardından **oluşturma**.
4. Yeni bir uygulama hizmeti planı ve yeni bir kaynak grubu oluşturma gibi hello yeni Django uygulamasını yapılandırın. Sonra, **Oluştur**’a tıklayın.
5. Merhaba yönergeleri izleyerek Git yayımlamayı yeni oluşturulan web uygulamanız için yapılandırma [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md).

## <a name="application-overview"></a>Uygulamaya Genel Bakış
### <a name="git-repository-contents"></a>Git deposu içeriği
Burada, hangi hello sonraki bölümde kopyalama hello ilk Git deposunda bulabilirsiniz hello dosyaları genel bir bakış verilmiştir.

    \app\__init__.py
    \app\forms.py
    \app\models.py
    \app\tests.py
    \app\views.py
    \app\static\content\
    \app\static\fonts\
    \app\static\scripts\
    \app\templates\about.html
    \app\templates\contact.html
    \app\templates\index.html
    \app\templates\layout.html
    \app\templates\login.html
    \app\templates\loginpartial.html
    \DjangoWebProject\__init__.py
    \DjangoWebProject\settings.py
    \DjangoWebProject\urls.py
    \DjangoWebProject\wsgi.py

Merhaba uygulaması için ana kaynaklar. Ana düzenle birlikte 3 sayfadan (dizin, hakkında, iletişim) oluşur. Statik içerik ve betikler bootstrap, jquery, modernize ve yanıtı içerir.

    \manage.py

Yerel yönetim ve geliştirme sunucusu desteği. Eşitleme hello veritabanı, vb., bu toorun hello uygulama yerel olarak kullanın.

    \db.sqlite3

Varsayılan veritabanı. Merhaba uygulama toorun Hello gerekli tabloları içerir, ancak (Merhaba veritabanı toocreate kullanıcı eşitleme) herhangi bir kullanıcı içermez.

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

[Visual Studio için Python Araçları] ile birlikte kullanmak için proje dosyaları.

    \ptvs_virtualenv_proxy.py

Sanal ortamlar için IIS proxy ve PTVS uzaktan hata ayıklama desteği

    \requirements.txt

Bu uygulamaya dış paketler gerekir. Bu dosyada listelenen yükleme hello paketleri Hello dağıtım betiği pip.

    \web.2.7.config
    \web.3.4.config

IIS yapılandırma dosyaları. Merhaba dağıtım betiği hello uygun Web.x.y.config'i kullanır ve bunu web.config olarak kopyalar.

### <a name="optional-files---customizing-deployment"></a>İsteğe bağlı dosyalar - Dağıtımı özelleştirme
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a>İsteğe bağlı dosyalar - Python çalışma zamanı
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a>Sunucu üzerindeki ek dosyalar
Bazı dosyalar hello sunucuda var, ancak toohello git deposuna eklenmez. Bunlar hello dağıtım betiği tarafından oluşturulur.

    \web.config

IIS yapılandırma dosyası. Her dağıtımda web.x.y.config tarafından oluşturulur.

    \env\

Python sanal ortamı. Dağıtım sırasında hello web uygulamasında uyumlu sanal ortamın zaten mevcut değilse oluşturulur. Requirements.txt içinde listelenen paketler pip yüklüdür, ancak hello paketler zaten yüklü ise pip yüklemeyi atlar.

Merhaba sonraki 3 bölümde nasıl tooproceed hello ile web uygulaması geliştirme altında farklı 3 ortamda açıklanmaktadır:

* Windows, Visual Studio için Python Araçları ile
* Windows, komut satırı ile
* Mac/Linux, komut satırı ile

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a>Web uygulaması geliştirme - Windows - Visual Studio için Python Araçları
### <a name="clone-hello-repository"></a>Kopya hello deposu
İlk olarak, Azure Portal hello üzerinde sağlanan hello URL'yi kullanarak hello depoyu kopyalayın. Daha fazla bilgi için bkz: [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md).

Merhaba hello depo kök dizininde bulunan hello çözüm dosyasını (.sln) açın.

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a>Sanal ortamı oluşturun.
Şimdi, yerel geliştirme için sanal bir ortam oluşturacağız. Sağ **Python Ortamları**’na sağ tıklayın **Sanal Ortam Ekle...** seçeneğini seçin.

* Merhaba ortamı Hello adı olduğundan emin olun `env`.
* Merhaba temel yorumlayıcıyı seçin. Toouse hello web uygulamanız için seçilen Python ile aynı sürümü olduğundan emin olun (runtime.txt veya hello **uygulama ayarları** hello Azure Portal, web uygulamanızın dikey penceresinde).
* Merhaba seçeneği toodownload ve yükleme paketleri işaretli olduğundan emin olun.

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

**Oluştur**'a tıklayın. Bu işlem hello sanal ortam oluşturacak ve requirements.txt içinde listelenen bağımlılıkları yükler.

### <a name="create-a-superuser"></a>Süper kullanıcı oluşturma
Merhaba uygulamayla birlikte gelen hello veritabanında tanımlı bir süper kullanıcı yok. Oturum açma sırası toouse hello işlev hello uygulama ya da hello Django yönetim arabirimi (tooenable karar verirseniz,), bir süper kullanıcı toocreate gerekir.

Bu hello komut satırı, proje klasöründen çalıştırın:

    env\scripts\python manage.py createsuperuser

Merhaba istemleri tooset hello kullanıcı adı, parola vb. izleyin.

### <a name="run-using-development-server"></a>Geliştirme sunucusu kullanarak çalıştırma
Otomatik olarak hata ayıklama tuşuna F5 toostart ve web tarayıcınız yerel olarak çalışan toohello sayfasını açar.

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

Kesme noktaları hello kaynakları, kullanım hello Gözcü pencerelerini, vb. ayarlayabilirsiniz. Merhaba bkz [Visual Studio belgeleri için Python Araçları] hakkında daha fazla bilgi için çeşitli özellikler hello.

### <a name="make-changes"></a>Değişiklik yapma
Şimdi değişiklikleri toohello uygulama kaynakları ve/veya şablonlarında yapmayı deneyebilirsiniz.

Değişikliklerinizi test ettikten sonra bunları toohello Git deposuna kaydedin:

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a>Daha fazla paket yükleme
Uygulamanızın Python ve Django ötesinde bağımlılıkları olabilir.

Pip kullanarak ek paketleri yükleyebilirsiniz. bir paket tooinstall sağ tıklayın hello sanal ortam ve select **Python paketini Yükle**.

Örneğin, tooinstall Merhaba, tooAzure depolama, service bus ve diğer Azure hizmetleriyle erişmenizi girin Python için Azure SDK `azure`:

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

Merhaba sanal ortamda sağ tıklayıp **requirements.txt Oluştur** tooupdate requirements.txt.

Ardından, hello değişiklikleri toorequirements.txt toohello Git deposuna uygulayın.

### <a name="deploy-tooazure"></a>TooAzure dağıtma
bir dağıtım tootrigger tıklayın **eşitleme** veya **anında**. Eşitleme, iletme ve çekme işlemini yapar.

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

bir sanal ortam, yükleme paketleri vb. oluşturacağı gibi hello ilk dağıtım biraz zaman alabilir.

Visual Studio hello hello dağıtımının ilerlemesini göstermez. Tooreview hello çıkış isterseniz hello bölümüne bakarak [sorun giderme - dağıtım](#troubleshooting-deployment).

Toohello Azure URL tooview değişikliklerinizi göz atın.

## <a name="web-app-development---windows---command-line"></a>Web uygulaması geliştirme - Windows - komut satırı
### <a name="clone-hello-repository"></a>Kopya hello deposu
İlk olarak, Azure Portal hello üzerinde sağlanan hello URL'yi kullanarak hello depoyu kopyalayın ve uzak olarak hello Azure deposunu ekleyin. Daha fazla bilgi için bkz: [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a>Sanal ortamı oluşturun.
(Bunu toohello depoya eklemeyin) geliştirme amacıyla yeni bir sanal ortam oluşturacağız. Sanal ortamlar Hello uygulama üzerinde çalışan her geliştiricinin yerel olarak Kendininkini oluşturacağı şekilde python'daki, değildir.

Toouse hello web uygulamanızda (runtime.txt veya hello uygulama ayarları dikey penceresinde hello Azure Portal kullanarak web uygulamanızda) için seçilen Python ile aynı sürümü emin olun.

Python 2.7:

    c:\python27\python.exe -m virtualenv env

Python 3.4:

    c:\python34\python.exe -m venv env

Uygulamanız için gereken herhangi bir dış paketi yükleyin. Sanal ortamınıza hello hello depo tooinstall hello paketleri kökünde hello requirements.txt dosyasını kullanabilirsiniz:

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a>Süper kullanıcı oluşturma
Merhaba uygulamayla birlikte gelen hello veritabanında tanımlı bir süper kullanıcı yok. Oturum açma sırası toouse hello işlev hello uygulama ya da hello Django yönetim arabirimi (tooenable karar verirseniz,), bir süper kullanıcı toocreate gerekir.

Bu hello komut satırı, proje klasöründen çalıştırın:

    env\scripts\python manage.py createsuperuser

Merhaba istemleri tooset hello kullanıcı adı, parola vb. izleyin.

### <a name="run-using-development-server"></a>Geliştirme sunucusu kullanarak çalıştırma
Komutu aşağıdaki hello ile Merhaba uygulaması geliştirme sunucusu altında başlatabilirsiniz:

    env\scripts\python manage.py runserver

Merhaba konsol hello URL'si gösterilir ve bağlantı noktası hello sunucu dinler:

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

Sonra web tarayıcısı toothat URL'nizi açın.

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a>Değişiklik yapma
Şimdi değişiklikleri toohello uygulama kaynakları ve/veya şablonlarında yapmayı deneyebilirsiniz.

Değişikliklerinizi test ettikten sonra bunları toohello Git deposuna kaydedin:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Daha fazla paket yükleme
Uygulamanızın Python ve Django ötesinde bağımlılıkları olabilir.

Pip kullanarak ek paketleri yükleyebilirsiniz. Örneğin, tooinstall Merhaba, imkanı sağlayan, Python için Azure SDK tooAzure depolama, service bus ve diğer Azure hizmetleriyle türü erişebilirsiniz:

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
(Bunu toohello depoya eklemeyin) geliştirme amacıyla yeni bir sanal ortam oluşturacağız. Sanal ortamlar Hello uygulama üzerinde çalışan her geliştiricinin yerel olarak Kendininkini oluşturacağı şekilde python'daki, değildir.

Toouse hello web uygulamanızda (runtime.txt veya hello uygulama ayarları dikey penceresinde hello Azure Portal kullanarak web uygulamanızda) için seçilen Python ile aynı sürümü emin olun.

Python 2.7:

    python -m virtualenv env

Python 3.4:

    python -m venv env

or

    pyvenv env

Uygulamanız için gereken herhangi bir dış paketi yükleyin. Sanal ortamınıza hello hello depo tooinstall hello paketleri kökünde hello requirements.txt dosyasını kullanabilirsiniz:

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a>Süper kullanıcı oluşturma
Merhaba uygulamayla birlikte gelen hello veritabanında tanımlı bir süper kullanıcı yok. Oturum açma sırası toouse hello işlev hello uygulama ya da hello Django yönetim arabirimi (tooenable karar verirseniz,), bir süper kullanıcı toocreate gerekir.

Bu hello komut satırı, proje klasöründen çalıştırın:

    env/bin/python manage.py createsuperuser

Merhaba istemleri tooset hello kullanıcı adı, parola vb. izleyin.

### <a name="run-using-development-server"></a>Geliştirme sunucusu kullanarak çalıştırma
Komutu aşağıdaki hello ile Merhaba uygulaması geliştirme sunucusu altında başlatabilirsiniz:

    env/bin/python manage.py runserver

Merhaba konsol hello URL'si gösterilir ve bağlantı noktası hello sunucu dinler:

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

Sonra web tarayıcısı toothat URL'nizi açın.

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a>Değişiklik yapma
Şimdi değişiklikleri toohello uygulama kaynakları ve/veya şablonlarında yapmayı deneyebilirsiniz.

Değişikliklerinizi test ettikten sonra bunları toohello Git deposuna kaydedin:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Daha fazla paket yükleme
Uygulamanızın Python ve Django ötesinde bağımlılıkları olabilir.

Pip kullanarak ek paketleri yükleyebilirsiniz. Örneğin, tooinstall Merhaba, imkanı sağlayan, Python için Azure SDK tooAzure depolama, service bus ve diğer Azure hizmetleriyle türü erişebilirsiniz:

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

## <a name="troubleshooting---static-files"></a>Sorun giderme - Statik Dosyalar
Django statik dosyaları toplama hello kavramına sahiptir. Bu tüm hello statik dosyaları özgün konumlarından alır ve bunları tooa tek klasörüne kopyalar. Bu uygulama için çok kopyalanırlar`/static`.

Statik dosyalar farklı Django “uygulamalarından” gelebileceğinden bu yapılır. Örneğin, hello Django yönetim arabirimlerindeki statik dosyalar hello hello sanal ortamdaki bir Django kitaplığı alt bulunur. Bu uygulama tarafından tanımlanan statik dosyalar `/app/static` içinde bulunur. Daha fazla Django “uygulamaları” kullandıkça, birden fazla yerde bulunan statik dosyalarınız olur.

Merhaba uygulama hata ayıklama modunda çalışırken Merhaba uygulaması hello statik dosyaları özgün konumlarından işlevi görür.

Merhaba uygulama yayın modunda çalışırken Merhaba uygulaması mu **değil** hello statik dosyaları sunar. Bunu hello hello web sunucusu tooserve hello dosyaları sorumluluğundadır. Bu uygulama için IIS statik dosyaları hello hizmet `/static`.

statik dosya Hello koleksiyonunu temizlenmesi hello dağıtım komut dosyası, daha önce toplanan parçası dosyalar halinde otomatik olarak yapılır. Bu hello koleksiyonu dağıtımı yavaşlattığı her dağıtımda meydana gelen ancak eski dosyaların olası bir güvenlik sorunu önlenerek kullanılabilir durumda olmaz sağlar anlamına gelir.

Django uygulamanız için statik dosya tooskip koleksiyonunu istiyorsanız:

    \.skipDjango

Ardından toodo hello koleksiyonu yerel makinenizde el ile gerekir:

    env\scripts\python manage.py collectstatic

Merhaba kaldırmak `\static` klasöründen `.gitignore` ve toohello Git deposunu ekleyin.

## <a name="troubleshooting---settings"></a>Sorun giderme - Ayarlar
Merhaba uygulama için çeşitli ayarları değiştirilebilir `DjangoWebProject/settings.py`.

Geliştiriciye kolaylık sağlamak için hata ayıklama modu etkindir. Olumlu bir yan etkisi, yerel olarak toocollect statik dosyaları gerek kalmadan çalıştırırken mümkün toosee resimleri ve diğer statik içeriği olacak ' dir.

toodisable hata ayıklama modu:

    DEBUG = False

Hata ayıklama devre dışı bırakıldığında, değeri hello `ALLOWED_HOSTS` gereksinimlerini toobe güncelleştirilmiş tooinclude hello Azure ana bilgisayar adı. Örneğin:

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

veya tooenable herhangi:

    ALLOWED_HOSTS = (
        '*',
    )

Uygulamada, toodo arasında geçiş yapma ile daha karmaşık toodeal hata ayıklama ve sürüm modu ve alma hello ana bilgisayar adı isteyebilirsiniz.

Hello Azure portal aracılığıyla ortam değişkenlerini ayarlayabilirsiniz **yapılandırma** sayfasında hello **uygulama ayarları** bölümü.  Bu değerler hello kaynaklarında (bağlantı dizeleri, parolalar vb.) tooappear istemeyebilirsiniz ya da Azure ile yerel makineniz arasında farklı tooset istediğiniz için faydalı olabilir. İçinde `settings.py`, kullanarak hello ortam değişkenlerini sorgulayabilirsiniz `os.getenv`.

## <a name="using-a-database"></a>Bir Veritabanını Kullanma
Merhaba uygulama ile birlikte hello veritabanı bir sqlite veritabanıdır. Neredeyse hiçbir Kurulum gerektirmediğinden, geliştirme için kullanışlı ve faydalıdır veritabanı toouse budur. Merhaba veritabanı hello hello proje klasöründeki db.sqlite3 dosyasında depolanır.

Azure Django uygulamasından kolay toouse olan veritabanı hizmetleri sağlar. Kullanma öğreticileri [SQL veritabanı] ve [MySQL] Django uygulamasından hello adımlar gerekli toocreate hello veritabanı hizmeti gösterir, hello veritabanı ayarlarını değiştirmek `DjangoWebProject/settings.py`ve hello kitaplıkları tooinstall gereklidir.

Elbette, kendi veritabanı sunucularınızı toomanage tercih ederseniz, bunu Windows veya Linux Azure üzerinde çalışan sanal makineleri kullanarak yapabilirsiniz.

## <a name="django-admin-interface"></a>Django Yönetim Arabirimi
Modellerinizi oluşturmaya başladıktan sonra toopopulate hello veritabanını bazı verilerle istersiniz. Toouse hello Django yönetim arabirimini toodo ekleme ve etkileşimli olarak içerik düzenleme kolay bir yoludur..

hello yönetim arabirimi Hello kodunu hello uygulama kaynaklarında dışı bırakılmıştır, ancak bunu ('admin' arayın) kolayca etkinleştirebileceğiniz şekilde açıkça işaretlenmiştir.

Etkinleştirildikten sonra hello veritabanını eşitleyin, hello uygulamayı çalıştırın ve çok gidin`/admin`.

## <a name="next-steps"></a>Sonraki Adımlar
Bu bağlantılar toolearn Django ve Python araçları hakkında daha fazla bilgi için Visual Studio izleyin:

* [Django Belgeleri]
* [Visual Studio belgeleri için Python Araçları]

SQL Database’i ve MySQL’i kullanma hakkında bilgi için:

* [Visual Studio için Python Araçları ile Azure’da Django ve MySQL]
* [Visual Studio için Python Araçları ile Azure’da Django ve SQL Veritabanı]

Daha fazla bilgi için bkz: Merhaba [Python Geliştirici Merkezi](/develop/python/).

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Visual Studio için Python Araçları ile Azure’da Django ve MySQL]: web-sites-python-ptvs-django-mysql.md
[Visual Studio için Python Araçları ile Azure’da Django ve SQL Veritabanı]: web-sites-python-ptvs-django-sql.md
[SQL veritabanı]: web-sites-python-ptvs-django-sql.md
[MySQL]: web-sites-python-ptvs-django-mysql.md

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
[Django Belgeleri]: https://www.djangoproject.com/
