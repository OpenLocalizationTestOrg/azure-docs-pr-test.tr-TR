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
# <a name="configuring-python-with-azure-app-service-web-apps"></a><span data-ttu-id="fa4ce-103">Azure App Service Web Apps ile Python yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fa4ce-103">Configuring Python with Azure App Service Web Apps</span></span>
<span data-ttu-id="fa4ce-104">Bu öğretici geliştirme ve temel bir Web sunucusu Ağ Geçidi Arabirimi (WSGI) uyumlu Python uygulaması yapılandırma seçenekleri açıklanmaktadır [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="fa4ce-104">This tutorial describes options for authoring and configuring a basic Web Server Gateway Interface (WSGI) compliant Python application on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="fa4ce-105">Sanal ortam ve requirements.txt kullanarak paket yükleme gibi Git dağıtımı ek özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-105">It describes additional features of Git deployment, such as virtual environment and package installation using requirements.txt.</span></span>

## <a name="bottle-django-or-flask"></a><span data-ttu-id="fa4ce-106">Bottle, Django veya Flask?</span><span class="sxs-lookup"><span data-stu-id="fa4ce-106">Bottle, Django or Flask?</span></span>
<span data-ttu-id="fa4ce-107">Hello Azure Marketi hello Bottle, Django ve Flask çerçeveler için şablonlar içerir.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-107">hello Azure Marketplace contains templates for hello Bottle, Django and Flask frameworks.</span></span> <span data-ttu-id="fa4ce-108">İlk web uygulamanızı Azure App Service'te geliştirdiğiniz veya Git ile tanıdık olmayan, Git dağıtımı kullanarak hello galerisinden çalışan bir uygulama oluşturmaya yönelik adım adım talimatları içerir şu öğreticilerden birine izlemenizi öneririz Windows veya Mac:</span><span class="sxs-lookup"><span data-stu-id="fa4ce-108">If you are developing your first web app in Azure App Service, or you are not familiar with Git, we recommend that you follow one of these tutorials, which include step-by-step instructions for building a working application from hello gallery using Git deployment from Windows or Mac:</span></span>

* [<span data-ttu-id="fa4ce-109">Bottle ile Web uygulamaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa4ce-109">Creating web apps with Bottle</span></span>](web-sites-python-create-deploy-bottle-app.md)
* [<span data-ttu-id="fa4ce-110">Django ile Web uygulamaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa4ce-110">Creating web apps with Django</span></span>](web-sites-python-create-deploy-django-app.md)
* [<span data-ttu-id="fa4ce-111">Flask ile Web uygulamaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa4ce-111">Creating web apps with Flask</span></span>](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a><span data-ttu-id="fa4ce-112">Azure Portal Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa4ce-112">Web app creation on Azure Portal</span></span>
<span data-ttu-id="fa4ce-113">Bu öğretici bir var olan Azure aboneliği ve erişim toohello Azure Portal varsayar.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-113">This tutorial assumes an existing Azure subscription and access toohello Azure Portal.</span></span>

<span data-ttu-id="fa4ce-114">Var olan bir web uygulamasının yoksa hello birinden oluşturabilirsiniz [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fa4ce-114">If you do not have an existing web app, you can create one from hello [Azure Portal](https://portal.azure.com).</span></span>  <span data-ttu-id="fa4ce-115">Merhaba sol üst köşesinde Hello yeni düğmesini tıklayın ve ardından **Web + mobil** > **Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-115">Click hello NEW button in hello top left corner, then click **Web + Mobile** > **Web app**.</span></span>

## <a name="git-publishing"></a><span data-ttu-id="fa4ce-116">Git yayımlamayı</span><span class="sxs-lookup"><span data-stu-id="fa4ce-116">Git Publishing</span></span>
<span data-ttu-id="fa4ce-117">Merhaba yönergeleri izleyerek Git yayımlamayı yeni oluşturulan web uygulamanız için yapılandırma [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="fa4ce-117">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="fa4ce-118">Bu öğretici Git toocreate kullanır, yönetmek ve bizim Python web uygulaması tooAzure uygulama hizmeti yayımlama.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-118">This tutorial uses Git toocreate, manage, and publish our Python web app tooAzure App Service.</span></span>

<span data-ttu-id="fa4ce-119">Git yayımlamayı ayarladıktan sonra bir Git deposu oluşturulur ve web uygulamanızı ile ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-119">Once Git publishing is set up, a Git repository will be created and associated with your web app.</span></span> <span data-ttu-id="fa4ce-120">Merhaba deposunun URL'sini görüntülenir ve hello yerel geliştirme ortamı toohello bulut kullanılan toopush verileri henceforth olabilir.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-120">hello repository's URL will be displayed and can henceforth be used toopush data from hello local development environment toohello cloud.</span></span> <span data-ttu-id="fa4ce-121">Git, üzerinden toopublish uygulamaları Git istemcisi de yüklenir ve kullanım hello yönergeleri, web uygulaması içerik tooAzure uygulama hizmeti toopush sağlanan emin olun.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-121">toopublish applications via Git, make sure a Git client is also installed and use hello instructions provided toopush your web app content tooAzure App Service.</span></span>

## <a name="application-overview"></a><span data-ttu-id="fa4ce-122">Uygulamaya Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="fa4ce-122">Application Overview</span></span>
<span data-ttu-id="fa4ce-123">Merhaba sonraki bölümlerde, aşağıdaki dosyaları hello oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-123">In hello next sections, hello following files are created.</span></span> <span data-ttu-id="fa4ce-124">Merhaba hello Git deposu kökünde yerleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-124">They should be placed in hello root of hello Git repository.</span></span>

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a><span data-ttu-id="fa4ce-125">WSGI işleyicisi</span><span class="sxs-lookup"><span data-stu-id="fa4ce-125">WSGI Handler</span></span>
<span data-ttu-id="fa4ce-126">WSGI olan tarafından açıklanan bir Python standart [CESARETLENDİRİCİ 3333](http://www.python.org/dev/peps/pep-3333/) hello web sunucusu ve Python arasında bir arabirim tanımlama.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-126">WSGI is a Python standard described by [PEP 3333](http://www.python.org/dev/peps/pep-3333/) defining an interface between hello web server and Python.</span></span> <span data-ttu-id="fa4ce-127">Bunu çeşitli web uygulamaları ve Python kullanarak çerçeveleri yazmak için standartlaştırılmış bir arabirim sağlar.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-127">It provides a standardized interface for writing various web applications and frameworks using Python.</span></span> <span data-ttu-id="fa4ce-128">Popüler Python web çerçeveleri bugün WSGI kullanın.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-128">Popular Python web frameworks today use WSGI.</span></span> <span data-ttu-id="fa4ce-129">Azure App Service Web Apps verir; bu tür bir çerçeveler için destek Merhaba özel işleyici hello WSGI belirtimi yönergeleri izleyen sürece ek olarak, İleri düzey kullanıcılar bile kendi yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-129">Azure App Service Web Apps gives you support for any such frameworks; in addition, advanced users can even author their own as long as hello custom handler follows hello WSGI specification guidelines.</span></span>

<span data-ttu-id="fa4ce-130">Bir örneği burada verilmiştir bir `app.py` özel işleyici tanımlar:</span><span class="sxs-lookup"><span data-stu-id="fa4ce-130">Here's an example of an `app.py` that defines a custom handler:</span></span>

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

<span data-ttu-id="fa4ce-131">Bu uygulama ile yerel olarak çalıştırabilirsiniz `python app.py`, çok Gözat`http://localhost:5555` web tarayıcınızda.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-131">You can run this application locally with `python app.py`, then browse too`http://localhost:5555` in your web browser.</span></span>

## <a name="virtual-environment"></a><span data-ttu-id="fa4ce-132">Sanal ortam</span><span class="sxs-lookup"><span data-stu-id="fa4ce-132">Virtual Environment</span></span>
<span data-ttu-id="fa4ce-133">Merhaba örnek uygulaması yukarıdaki herhangi bir dış paketi gerektirmez rağmen uygulamanızın bazı gerektirecektir olasıdır.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-133">Although hello example app above doesn't require any external packages, it is likely that your application will require some.</span></span>

<span data-ttu-id="fa4ce-134">toohelp dış Paket bağımlılıklarını yönetebilir, Azure Git dağıtımı sanal ortamlar hello oluşturmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-134">toohelp manage external package dependencies, Azure Git deployment supports hello creation of virtual environments.</span></span>

<span data-ttu-id="fa4ce-135">Azure hello hello deposu kökünde bir requirements.txt algıladığında adlı bir sanal ortam otomatik olarak oluşturduğu `env`.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-135">When Azure detects a requirements.txt in hello root of hello repository, it automatically creates a virtual environment named `env`.</span></span> <span data-ttu-id="fa4ce-136">Bu yalnızca hello ilk dağıtımda oluşur veya seçilen Python çalışma zamanı hello sonra herhangi bir dağıtımı sırasında değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-136">This only occurs on hello first deployment, or during any deployment after hello selected Python runtime has changed.</span></span>

<span data-ttu-id="fa4ce-137">Toocreate yerel geliştirme için sanal bir ortam istemenizdir, ancak Git deponuzu dahil etmeyin.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-137">You will probably want toocreate a virtual environment locally for development, but don't include it in your Git repository.</span></span>

## <a name="package-management"></a><span data-ttu-id="fa4ce-138">Paket Yönetimi</span><span class="sxs-lookup"><span data-stu-id="fa4ce-138">Package Management</span></span>
<span data-ttu-id="fa4ce-139">Requirements.txt içinde listelenen paketleri pip kullanılarak hello sanal ortamda otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-139">Packages listed in requirements.txt will be installed automatically in hello virtual environment using pip.</span></span> <span data-ttu-id="fa4ce-140">Bu her dağıtımda gerçekleşir, ancak bir paket zaten yüklü ise pip yüklemeyi atlar.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-140">This happens on every deployment, but pip will skip installation if a package is already installed.</span></span>

<span data-ttu-id="fa4ce-141">Örnek `requirements.txt`:</span><span class="sxs-lookup"><span data-stu-id="fa4ce-141">Example `requirements.txt`:</span></span>

    azure==0.8.4


## <a name="python-version"></a><span data-ttu-id="fa4ce-142">Python sürümü</span><span class="sxs-lookup"><span data-stu-id="fa4ce-142">Python Version</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

<span data-ttu-id="fa4ce-143">Örnek `runtime.txt`:</span><span class="sxs-lookup"><span data-stu-id="fa4ce-143">Example `runtime.txt`:</span></span>

    python-2.7


## <a name="webconfig"></a><span data-ttu-id="fa4ce-144">Web.config</span><span class="sxs-lookup"><span data-stu-id="fa4ce-144">Web.config</span></span>
<span data-ttu-id="fa4ce-145">Toocreate bir web.config dosyası toospecify gerekir hello sunucu istekleri nasıl yöneteceğini.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-145">You'll need toocreate a web.config file toospecify how hello server should handle requests.</span></span>

<span data-ttu-id="fa4ce-146">X.y eşleştiği deponuz içinde bir Web.x.y.config'i dosyanız varsa hello Python çalışma zamanı seçili sonra Azure otomatik olarak hello uygun dosyayı web.config olarak kopyalar unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-146">Note that if you have a web.x.y.config file in your repository, where x.y matches hello selected Python runtime, then Azure will automatically copy hello appropriate file as web.config.</span></span>

<span data-ttu-id="fa4ce-147">Merhaba aşağıdaki web.config örnekler hello sonraki bölümde açıklanan bir sanal ortam proxy betiği kullanır.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-147">hello following web.config examples rely on a virtual environment proxy script, which is described in hello next section.</span></span>  <span data-ttu-id="fa4ce-148">Merhaba örnekte kullanılan hello WSGI işleyicisi çalışmak `app.py` üstünde.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-148">They work with hello WSGI handler used in hello example `app.py` above.</span></span>

<span data-ttu-id="fa4ce-149">Örnek `web.config` Python 2.7 için:</span><span class="sxs-lookup"><span data-stu-id="fa4ce-149">Example `web.config` for Python 2.7:</span></span>

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


<span data-ttu-id="fa4ce-150">Örnek `web.config` Python 3.4 için:</span><span class="sxs-lookup"><span data-stu-id="fa4ce-150">Example `web.config` for Python 3.4:</span></span>

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


<span data-ttu-id="fa4ce-151">Statik dosyalar hello web sunucusu tarafından doğrudan, Gelişmiş performans için Python kodu üzerinden geçmeden ele alınacaktır.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-151">Static files will be handled by hello web server directly, without going through Python code, for improved performance.</span></span>

<span data-ttu-id="fa4ce-152">Örnekleri yukarıda Hello hello statik dosyaların diskteki hello konumu hello URL hello konumda eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-152">In hello above examples, hello location of hello static files on disk should match hello location in hello URL.</span></span> <span data-ttu-id="fa4ce-153">Bir istek için buna `http://pythonapp.azurewebsites.net/static/site.css` hello dosya diskte görecek `\static\site.css`.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-153">This means that a request for `http://pythonapp.azurewebsites.net/static/site.css` will serve hello file on disk at `\static\site.css`.</span></span>

<span data-ttu-id="fa4ce-154">`WSGI_ALT_VIRTUALENV_HANDLER`Merhaba WSGI işleyici belirlediğiniz olur.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-154">`WSGI_ALT_VIRTUALENV_HANDLER` is where you specify hello WSGI handler.</span></span> <span data-ttu-id="fa4ce-155">Örnekler, yukarıda hello içinde olan `app.wsgi_app` hello işleyici adlı bir işlev olduğundan `wsgi_app` içinde `app.py` hello kök klasöründe.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-155">In hello above examples, it's `app.wsgi_app` because hello handler is a function named `wsgi_app` in `app.py` in hello root folder.</span></span>

<span data-ttu-id="fa4ce-156">`PYTHONPATH`özelleştirilebilir, ancak requirements.txt içinde belirterek hello sanal ortamda tüm bağımlılıkları yüklerseniz, toochange gerekir döndürmemelidir onu.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-156">`PYTHONPATH` can be customized, but if you install all your dependencies in hello virtual environment by specifying them in requirements.txt, you shouldn't need toochange it.</span></span>

## <a name="virtual-environment-proxy"></a><span data-ttu-id="fa4ce-157">Sanal ortam Proxy</span><span class="sxs-lookup"><span data-stu-id="fa4ce-157">Virtual Environment Proxy</span></span>
<span data-ttu-id="fa4ce-158">komut dosyası izleyen hello kullanılan tooretrieve hello WSGI işleyici, hello sanal ortamı ve günlük hataları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-158">hello following script is used tooretrieve hello WSGI handler, activate hello virtual environment and log errors.</span></span> <span data-ttu-id="fa4ce-159">Genel ve değişiklik olmadan kullanılan tasarlanmış toobe olur.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-159">It is designed toobe generic and used without modifications.</span></span>

<span data-ttu-id="fa4ce-160">İçeriği `ptvs_virtualenv_proxy.py`:</span><span class="sxs-lookup"><span data-stu-id="fa4ce-160">Contents of `ptvs_virtualenv_proxy.py`:</span></span>

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


## <a name="customize-git-deployment"></a><span data-ttu-id="fa4ce-161">Git dağıtımı özelleştirme</span><span class="sxs-lookup"><span data-stu-id="fa4ce-161">Customize Git deployment</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="fa4ce-162">Sorun giderme - Paket Yükleme</span><span class="sxs-lookup"><span data-stu-id="fa4ce-162">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="fa4ce-163">Sorun giderme - Sanal Ortam</span><span class="sxs-lookup"><span data-stu-id="fa4ce-163">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="fa4ce-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fa4ce-164">Next steps</span></span>
<span data-ttu-id="fa4ce-165">Daha fazla bilgi için bkz: Merhaba [Python Geliştirici Merkezi](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="fa4ce-165">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

> [!NOTE]
> <span data-ttu-id="fa4ce-166">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-166">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="fa4ce-167">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="fa4ce-167">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="fa4ce-168">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="fa4ce-168">What's changed</span></span>
* <span data-ttu-id="fa4ce-169">Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="fa4ce-169">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

