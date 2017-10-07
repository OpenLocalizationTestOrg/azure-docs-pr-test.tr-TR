---
title: aaaConfiguring Python ile Azure App Service Web Apps
description: "Bu öğretici geliştirme ve Azure App Service Web Apps üzerinde temel bir Web sunucusu Ağ Geçidi Arabirimi (WSGI) uyumlu Python uygulama yapılandırmak için seçenekleri açıklar."
services: app-service
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: fd00dc91-9935-4331-b955-4bd71e66d518
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/26/2016
ms.author: huvalo
ms.openlocfilehash: 00d49fb01491e9adb4b6fededfb95669a8dbd485
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-python-with-azure-app-service-web-apps"></a>Azure App Service Web Apps ile Python yapılandırma
Bu öğretici geliştirme ve temel bir Web sunucusu Ağ Geçidi Arabirimi (WSGI) uyumlu Python uygulaması yapılandırma seçenekleri açıklanmaktadır [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

Sanal ortam ve requirements.txt kullanarak paket yükleme gibi Git dağıtımı ek özelliklerini açıklar.

## <a name="bottle-django-or-flask"></a>Bottle, Django veya Flask?
Hello Azure Marketi hello Bottle, Django ve Flask çerçeveler için şablonlar içerir. İlk web uygulamanızı Azure App Service'te geliştirdiğiniz veya Git ile tanıdık olmayan, Git dağıtımı kullanarak hello galerisinden çalışan bir uygulama oluşturmaya yönelik adım adım talimatları içerir şu öğreticilerden birine izlemenizi öneririz Windows veya Mac:

* [Bottle ile Web uygulamaları oluşturma](web-sites-python-create-deploy-bottle-app.md)
* [Django ile Web uygulamaları oluşturma](web-sites-python-create-deploy-django-app.md)
* [Flask ile Web uygulamaları oluşturma](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a>Azure Portal Web uygulaması oluşturma
Bu öğretici bir var olan Azure aboneliği ve erişim toohello Azure Portal varsayar.

Var olan bir web uygulamasının yoksa hello birinden oluşturabilirsiniz [Azure Portal](https://portal.azure.com).  Merhaba sol üst köşesinde Hello yeni düğmesini tıklayın ve ardından **Web + mobil** > **Web uygulaması**.

## <a name="git-publishing"></a>Git yayımlamayı
Merhaba yönergeleri izleyerek Git yayımlamayı yeni oluşturulan web uygulamanız için yapılandırma [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md). Bu öğretici Git toocreate kullanır, yönetmek ve bizim Python web uygulaması tooAzure uygulama hizmeti yayımlama.

Git yayımlamayı ayarladıktan sonra bir Git deposu oluşturulur ve web uygulamanızı ile ilişkilendirilmiş. Merhaba deposunun URL'sini görüntülenir ve hello yerel geliştirme ortamı toohello bulut kullanılan toopush verileri henceforth olabilir. Git, üzerinden toopublish uygulamaları Git istemcisi de yüklenir ve kullanım hello yönergeleri, web uygulaması içerik tooAzure uygulama hizmeti toopush sağlanan emin olun.

## <a name="application-overview"></a>Uygulamaya Genel Bakış
Merhaba sonraki bölümlerde, aşağıdaki dosyaları hello oluşturulur. Merhaba hello Git deposu kökünde yerleştirilmelidir.

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a>WSGI işleyicisi
WSGI olan tarafından açıklanan bir Python standart [CESARETLENDİRİCİ 3333](http://www.python.org/dev/peps/pep-3333/) hello web sunucusu ve Python arasında bir arabirim tanımlama. Bunu çeşitli web uygulamaları ve Python kullanarak çerçeveleri yazmak için standartlaştırılmış bir arabirim sağlar. Popüler Python web çerçeveleri bugün WSGI kullanın. Azure App Service Web Apps verir; bu tür bir çerçeveler için destek Merhaba özel işleyici hello WSGI belirtimi yönergeleri izleyen sürece ek olarak, İleri düzey kullanıcılar bile kendi yazabilirsiniz.

Bir örneği burada verilmiştir bir `app.py` özel işleyici tanımlar:

    def wsgi_app(environ, start_response):
        status = '200 OK'
        response_headers = [('Content-type', 'text/plain')]
        start_response(status, response_headers)
        response_body = 'Hello World'
        yield response_body.encode()

    if __name__ == '__main__':
        from wsgiref.simple_server import make_server

        httpd = make_server('localhost', 5555, wsgi_app)
        httpd.serve_forever()

Bu uygulama ile yerel olarak çalıştırabilirsiniz `python app.py`, çok Gözat`http://localhost:5555` web tarayıcınızda.

## <a name="virtual-environment"></a>Sanal ortam
Merhaba örnek uygulaması yukarıdaki herhangi bir dış paketi gerektirmez rağmen uygulamanızın bazı gerektirecektir olasıdır.

toohelp dış Paket bağımlılıklarını yönetebilir, Azure Git dağıtımı sanal ortamlar hello oluşturmayı destekler.

Azure hello hello deposu kökünde bir requirements.txt algıladığında adlı bir sanal ortam otomatik olarak oluşturduğu `env`. Bu yalnızca hello ilk dağıtımda oluşur veya seçilen Python çalışma zamanı hello sonra herhangi bir dağıtımı sırasında değiştirildi.

Toocreate yerel geliştirme için sanal bir ortam istemenizdir, ancak Git deponuzu dahil etmeyin.

## <a name="package-management"></a>Paket Yönetimi
Requirements.txt içinde listelenen paketleri pip kullanılarak hello sanal ortamda otomatik olarak yüklenir. Bu her dağıtımda gerçekleşir, ancak bir paket zaten yüklü ise pip yüklemeyi atlar.

Örnek `requirements.txt`:

    azure==0.8.4


## <a name="python-version"></a>Python sürümü
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

Örnek `runtime.txt`:

    python-2.7


## <a name="webconfig"></a>Web.config
Toocreate bir web.config dosyası toospecify gerekir hello sunucu istekleri nasıl yöneteceğini.

X.y eşleştiği deponuz içinde bir Web.x.y.config'i dosyanız varsa hello Python çalışma zamanı seçili sonra Azure otomatik olarak hello uygun dosyayı web.config olarak kopyalar unutmayın.

Merhaba aşağıdaki web.config örnekler hello sonraki bölümde açıklanan bir sanal ortam proxy betiği kullanır.  Merhaba örnekte kullanılan hello WSGI işleyicisi çalışmak `app.py` üstünde.

Örnek `web.config` Python 2.7 için:

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\activate_this.py" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_virtualenv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python27\python.exe|D:\Python27\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite"
                      url="handler.fcgi/{R:1}"
                      appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


Örnek `web.config` Python 3.4 için:

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\python.exe" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_venv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python34\python.exe|D:\Python34\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite" url="handler.fcgi/{R:1}" appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


Statik dosyalar hello web sunucusu tarafından doğrudan, Gelişmiş performans için Python kodu üzerinden geçmeden ele alınacaktır.

Örnekleri yukarıda Hello hello statik dosyaların diskteki hello konumu hello URL hello konumda eşleşmesi gerekir. Bir istek için buna `http://pythonapp.azurewebsites.net/static/site.css` hello dosya diskte görecek `\static\site.css`.

`WSGI_ALT_VIRTUALENV_HANDLER`Merhaba WSGI işleyici belirlediğiniz olur. Örnekler, yukarıda hello içinde olan `app.wsgi_app` hello işleyici adlı bir işlev olduğundan `wsgi_app` içinde `app.py` hello kök klasöründe.

`PYTHONPATH`özelleştirilebilir, ancak requirements.txt içinde belirterek hello sanal ortamda tüm bağımlılıkları yüklerseniz, toochange gerekir döndürmemelidir onu.

## <a name="virtual-environment-proxy"></a>Sanal ortam Proxy
komut dosyası izleyen hello kullanılan tooretrieve hello WSGI işleyici, hello sanal ortamı ve günlük hataları etkinleştirin. Genel ve değişiklik olmadan kullanılan tasarlanmış toobe olur.

İçeriği `ptvs_virtualenv_proxy.py`:

     # ############################################################################
     #
     # Copyright (c) Microsoft Corporation. 
     #
     # This source code is subject tooterms and conditions of hello Apache License, Version 2.0. A 
     # copy of hello license can be found in hello License.html file at hello root of this distribution. If 
     # you cannot locate hello Apache License, Version 2.0, please send an email too
     # vspython@microsoft.com. By using this source code in any fashion, you are agreeing toobe bound 
     # by hello terms of hello Apache License, Version 2.0.
     #
     # You must not remove this notice, or any other, from this software.
     #
     # ###########################################################################

    import datetime
    import os
    import sys
    import traceback

    if sys.version_info[0] == 3:
        def to_str(value):
            return value.decode(sys.getfilesystemencoding())

        def execfile(path, global_dict):
            """Execute a file"""
            with open(path, 'r') as f:
                code = f.read()
            code = code.replace('\r\n', '\n') + '\n'
            exec(code, global_dict)
    else:
        def to_str(value):
            return value.encode(sys.getfilesystemencoding())

    def log(txt):
        """Logs fatal errors tooa log file if WSGI_LOG env var is defined"""
        log_file = os.environ.get('WSGI_LOG')
        if log_file:
            f = open(log_file, 'a+')
            try:
                f.write('%s: %s' % (datetime.datetime.now(), txt))
            finally:
                f.close()

    ptvsd_secret = os.getenv('WSGI_PTVSD_SECRET')
    if ptvsd_secret:
        log('Enabling ptvsd ...\n')
        try:
            import ptvsd
            try:
                ptvsd.enable_attach(ptvsd_secret)
                log('ptvsd enabled.\n')
            except: 
                log('ptvsd.enable_attach failed\n')
        except ImportError:
            log('error importing ptvsd.\n')

    def get_wsgi_handler(handler_name):
        if not handler_name:
            raise Exception('WSGI_ALT_VIRTUALENV_HANDLER env var must be set')

        if not isinstance(handler_name, str):
            handler_name = to_str(handler_name)

        module_name, _, callable_name = handler_name.rpartition('.')
        should_call = callable_name.endswith('()')
        callable_name = callable_name[:-2] if should_call else callable_name
        name_list = [(callable_name, should_call)]
        handler = None
        last_tb = ''

        while module_name:
            try:
                handler = __import__(module_name, fromlist=[name_list[0][0]])
                last_tb = ''
                for name, should_call in name_list:
                    handler = getattr(handler, name)
                    if should_call:
                        handler = handler()
                break
            except ImportError:
                module_name, _, callable_name = module_name.rpartition('.')
                should_call = callable_name.endswith('()')
                callable_name = callable_name[:-2] if should_call else callable_name
                name_list.insert(0, (callable_name, should_call))
                handler = None
                last_tb = ': ' + traceback.format_exc()

        if handler is None:
            raise ValueError('"%s" could not be imported%s' % (handler_name, last_tb))

        return handler

    activate_this = os.getenv('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS')
    if not activate_this:
        raise Exception('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS is not set')

    def get_virtualenv_handler():
        log('Activating virtualenv with %s\n' % activate_this)
        execfile(activate_this, dict(__file__=activate_this))

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler

    def get_venv_handler():
        log('Activating venv with executable at %s\n' % activate_this)
        import site
        sys.executable = activate_this
        old_sys_path, sys.path = sys.path, []

        site.main()

        sys.path.insert(0, '')
        for item in old_sys_path:
            if item not in sys.path:
                sys.path.append(item)

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler


## <a name="customize-git-deployment"></a>Git dağıtımı özelleştirme
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a>Sorun giderme - Paket Yükleme
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>Sorun giderme - Sanal Ortam
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için bkz: Merhaba [Python Geliştirici Merkezi](/develop/python/).

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

