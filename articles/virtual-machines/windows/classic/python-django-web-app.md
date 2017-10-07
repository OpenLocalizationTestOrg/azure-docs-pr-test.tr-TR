---
title: "bir Windows Server Azure VM'de aaaDjango web uygulaması | Microsoft Docs"
description: "Bilgi nasıl toohost bir Windows Server 2012 R2 Datacenter VM ile Merhaba Klasik dağıtım modelini kullanarak azure'da Django tabanlı bir Web sitesi."
services: virtual-machines-windows
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-service-management
ms.assetid: e36484d1-afbf-47f5-b755-5e65397dc1c3
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 55847e3c6d6769965be29077e8d4eeebad914637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a>Windows Server VM üzerinde Django Hello World web uygulaması

> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager ve hello Klasik dağıtım modeli](../../../resource-manager-deployment-model.md). Bu makalede hello Klasik dağıtım modeli açıklanır. En yeni dağıtımların hello Resource Manager modelini kullanmasını öneririz.

Bu öğretici şunların nasıl yapıldığını gösterir toohost Django tabanlı bir Web sitesi Windows Server'da Azure Virtual Machines'de. Merhaba öğreticide, Azure ile konusunda deneyim varsayıyoruz. Merhaba öğreticiyi tamamladığınızda, Django tabanlı bir uygulamayı oluşturan ve hello bulutta çalışan sahip olabilir.

Şunları nasıl yapacağınızı öğrenin:

* Azure sanal makinesi toohost Django ayarlayın. Bu öğretici açıklar ancak nasıl toodo bu **Windows Server**, yapabileceğiniz Azure'da bir Linux VM barındırılan için aynı hello.
* Yeni bir Django uygulaması Windows oluşturun.

Merhaba öğretici nasıl toobuild temel bir Hello World web uygulaması gösterir. Merhaba uygulaması bir Azure sanal makinesi barındırılır.

Aşağıdaki ekran görüntüsü hello tamamlandı Merhaba uygulaması gösterir:

![Bir tarayıcı penceresinde hello hello world sayfasını Azure'da görüntüler.][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>Oluşturma ve Azure sanal makinesi toohost Django ayarlama

1. toocreate hello Windows Server 2012 R2 Datacenter dağıtım, bir Azure sanal makinesi bkz [Windows hello Azure portalı çalıştıran bir sanal makine oluşturma](tutorial.md).
2. Azure toodirect bağlantı noktası 80 trafiği hello sanal makineye hello web tooport 80 ayarlayın:
   
   1. Hello Azure portal, toohello Pano gidin ve yeni oluşturulan sanal makineyi seçin.
   2. **Uç noktaları**’na ve ardından **Ekle**’ye tıklayın.

     ![Bir uç nokta ekleme](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. Merhaba üzerinde **uç nokta ekleme** sayfası için **adı**, girin **HTTP**. Merhaba ortak ve özel TCP bağlantı noktası çok ayarlayın**80**.

     ![Bir ad girin ve ortak ve özel bağlantı noktalarını ayarlayın](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. **Tamam** düğmesine tıklayın.
     
3. Merhaba panosunda, VM'yi seçin. Azure sanal makine, yeni oluşturulan toohello içinde toouse Uzak Masaüstü Protokolü (RDP) tooremotely işaretini tıklatın **Bağlan**.  

> [!IMPORTANT] 
> yönergeleri izleyerek hello toohello sanal makinede doğru şekilde imzalanmış varsayalım. Ayrıca komutları hello sanal makine ve yerel bilgisayarınızda değil dağıttığınız varsayılmıştır.

## <a id="setup"></a>Python, Django ve Wfastcgı yükleyin
> [!NOTE]
> Internet Explorer kullanarak toodownload tooconfigure Internet Explorer olabilir **Artırılmış Güvenlik Yapılandırması** ayarlar. toodo bunu, **Başlat** > **Yönetimsel Araçlar** > **Sunucu Yöneticisi'ni** > **yerel sunucu**. Tıklatın **IE Artırılmış Güvenlik Yapılandırması**ve ardından **devre dışı**.

1. Python 2.7 veya Python 3.4 gelen en son sürümlerini Hello yüklemek [python.org][python.org].
2. Merhaba wfastcgı ve django paketler pip kullanarak yükleyin.
   
    Python 2.7 için komutu aşağıdaki hello kullan:
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    Python 3.4 için komutu aşağıdaki hello kullan:
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a>IIS Fastcgı ile yükleme
* Internet Information Services (IIS) Fastcgı desteğiyle yükleyin. Bu işlem birkaç dakika tooexecute sürebilir.
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a>Yeni bir Django uygulaması oluşturma
1. C:\inetpub\wwwroot, yeni Django proje toocreate hello aşağıdaki komutu girin:
   
   Python 2.7 için komutu aşağıdaki hello kullan:
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   Python 3.4 için komutu aşağıdaki hello kullan:
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![Merhaba New-AzureService komutunun Hello sonucu](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. Merhaba `django-admin` komutu Django tabanlı Web siteleri için basit bir yapı oluşturur:
   
   * `helloworld\manage.py`barındırma başlatmak ve durdurmak, Django tabanlı Web sitesi barındırma yardımcı olur.
   * `helloworld\helloworld\settings.py`Uygulamanız için Django ayarlarına sahiptir.
   * `helloworld\helloworld\urls.py`her URL ve kendi görünüm arasında Hello eşleme kodu vardır.
3. Merhaba C:\inetpub\wwwroot\helloworld\helloworld dizininde views.py adlı yeni bir dosya oluşturun. Bu dosya hello "hello world" sayfasını işler hello görünüme sahiptir. Kod düzenleyicinizde hello aşağıdaki komutları girin:
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. Merhaba urls.py dosyasının Merhaba içeriğine komutları aşağıdaki hello ile değiştirin:
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a>ISS kurmak
1. Merhaba genel applicationhost.config dosyasında hello işleyicileri bölümün kilidini açın.  Bu, web.config dosyası toouse hello Python işleyicisi sağlar. Bu komutu ekleyin:
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. Wfastcgı etkinleştirin. Bu tooyour Python yorumlayıcı çalıştırılabilir ve hello wfastcgi.py betik başvuran bir uygulama toohello genel applicationhost.config dosyası ekler.
   
    Python 2.7:
   
        C:\python27\scripts\wfastcgi-enable
   
    Python 3.4:
   
        C:\python34\scripts\wfastcgi-enable
3. C:\inetpub\wwwroot\helloworld içinde bir web.config dosyası oluşturun. Merhaba hello değerini `scriptProcessor` özniteliği, önceki adımı hello hello çıktısını eşleşmelidir. Merhaba wfastcgı ayarı hakkında daha fazla bilgi için bkz: [pypı wfastcgı][wfastcgi].
   
   Python 2.7:
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python27\python.exe|C:\Python27\Lib\site-packages\wfastcgi.pyc" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
   
   Python 3.4:
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python34\python.exe|C:\Python34\Lib\site-packages\wfastcgi.py" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
4. Merhaba hello IIS varsayılan Web sitesi toopoint toohello Django proje klasörünün konumunu güncelleştirin:
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. Merhaba Web tarayıcınızda yükleyin.

![Bir tarayıcı penceresinde hello hello world sayfasını Azure üzerinde görüntüler.][1]

## <a name="shut-down-your-azure-virtual-machine"></a>Azure, sanal makineyi Kapat
Bu öğreticiyi tamamladığınızda, kapatıldı veya hello hello öğretici için oluşturduğunuz Azure VM Kaldır öneririz. Bu diğer öğreticileri için kaynakları serbest bırakır ve Azure kullanım ücretlerinin yansıtılmasını önleyebilirsiniz.

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
