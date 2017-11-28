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
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a><span data-ttu-id="25a01-103">Windows Server VM üzerinde Django Hello World web uygulaması</span><span class="sxs-lookup"><span data-stu-id="25a01-103">Django Hello World web app on a Windows Server VM</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="25a01-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager ve hello Klasik dağıtım modeli](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="25a01-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and hello classic deployment model](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="25a01-105">Bu makalede hello Klasik dağıtım modeli açıklanır.</span><span class="sxs-lookup"><span data-stu-id="25a01-105">This article describes hello classic deployment model.</span></span> <span data-ttu-id="25a01-106">En yeni dağıtımların hello Resource Manager modelini kullanmasını öneririz.</span><span class="sxs-lookup"><span data-stu-id="25a01-106">We recommend that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="25a01-107">Bu öğretici şunların nasıl yapıldığını gösterir toohost Django tabanlı bir Web sitesi Windows Server'da Azure Virtual Machines'de.</span><span class="sxs-lookup"><span data-stu-id="25a01-107">This tutorial shows you how toohost a Django-based website in Windows Server in Azure Virtual Machines.</span></span> <span data-ttu-id="25a01-108">Merhaba öğreticide, Azure ile konusunda deneyim varsayıyoruz.</span><span class="sxs-lookup"><span data-stu-id="25a01-108">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="25a01-109">Merhaba öğreticiyi tamamladığınızda, Django tabanlı bir uygulamayı oluşturan ve hello bulutta çalışan sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="25a01-109">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="25a01-110">Şunları nasıl yapacağınızı öğrenin:</span><span class="sxs-lookup"><span data-stu-id="25a01-110">Learn how to:</span></span>

* <span data-ttu-id="25a01-111">Azure sanal makinesi toohost Django ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="25a01-111">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="25a01-112">Bu öğretici açıklar ancak nasıl toodo bu **Windows Server**, yapabileceğiniz Azure'da bir Linux VM barındırılan için aynı hello.</span><span class="sxs-lookup"><span data-stu-id="25a01-112">Although this tutorial explains how toodo this for **Windows Server**, you can do hello same for a Linux VM hosted in Azure.</span></span>
* <span data-ttu-id="25a01-113">Yeni bir Django uygulaması Windows oluşturun.</span><span class="sxs-lookup"><span data-stu-id="25a01-113">Create a new Django application in Windows.</span></span>

<span data-ttu-id="25a01-114">Merhaba öğretici nasıl toobuild temel bir Hello World web uygulaması gösterir.</span><span class="sxs-lookup"><span data-stu-id="25a01-114">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="25a01-115">Merhaba uygulaması bir Azure sanal makinesi barındırılır.</span><span class="sxs-lookup"><span data-stu-id="25a01-115">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="25a01-116">Aşağıdaki ekran görüntüsü hello tamamlandı Merhaba uygulaması gösterir:</span><span class="sxs-lookup"><span data-stu-id="25a01-116">hello following screenshot shows hello completed application:</span></span>

![Bir tarayıcı penceresinde hello hello world sayfasını Azure'da görüntüler.][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="25a01-118">Oluşturma ve Azure sanal makinesi toohost Django ayarlama</span><span class="sxs-lookup"><span data-stu-id="25a01-118">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="25a01-119">toocreate hello Windows Server 2012 R2 Datacenter dağıtım, bir Azure sanal makinesi bkz [Windows hello Azure portalı çalıştıran bir sanal makine oluşturma](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="25a01-119">toocreate an Azure virtual machine with hello Windows Server 2012 R2 Datacenter distribution, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>
2. <span data-ttu-id="25a01-120">Azure toodirect bağlantı noktası 80 trafiği hello sanal makineye hello web tooport 80 ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="25a01-120">Set Azure toodirect port 80 traffic from hello web tooport 80 on hello virtual machine:</span></span>
   
   1. <span data-ttu-id="25a01-121">Hello Azure portal, toohello Pano gidin ve yeni oluşturulan sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="25a01-121">In hello Azure portal, go toohello dashboard and select your newly created virtual machine.</span></span>
   2. <span data-ttu-id="25a01-122">**Uç noktaları**’na ve ardından **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="25a01-122">Click **Endpoints**, and then click **Add**.</span></span>

     ![Bir uç nokta ekleme](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. <span data-ttu-id="25a01-124">Merhaba üzerinde **uç nokta ekleme** sayfası için **adı**, girin **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="25a01-124">On hello **Add endpoint** page, for **Name**, enter **HTTP**.</span></span> <span data-ttu-id="25a01-125">Merhaba ortak ve özel TCP bağlantı noktası çok ayarlayın**80**.</span><span class="sxs-lookup"><span data-stu-id="25a01-125">Set hello public and private TCP ports too**80**.</span></span>

     ![Bir ad girin ve ortak ve özel bağlantı noktalarını ayarlayın](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. <span data-ttu-id="25a01-127">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="25a01-127">Click **OK**.</span></span>
     
3. <span data-ttu-id="25a01-128">Merhaba panosunda, VM'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="25a01-128">In hello dashboard, select your VM.</span></span> <span data-ttu-id="25a01-129">Azure sanal makine, yeni oluşturulan toohello içinde toouse Uzak Masaüstü Protokolü (RDP) tooremotely işaretini tıklatın **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="25a01-129">toouse Remote Desktop Protocol (RDP) tooremotely sign in toohello newly created Azure virtual machine, click **Connect**.</span></span>  

> [!IMPORTANT] 
> <span data-ttu-id="25a01-130">yönergeleri izleyerek hello toohello sanal makinede doğru şekilde imzalanmış varsayalım.</span><span class="sxs-lookup"><span data-stu-id="25a01-130">hello following instructions assume that you signed in toohello virtual machine correctly.</span></span> <span data-ttu-id="25a01-131">Ayrıca komutları hello sanal makine ve yerel bilgisayarınızda değil dağıttığınız varsayılmıştır.</span><span class="sxs-lookup"><span data-stu-id="25a01-131">They also assume that you are issuing commands in hello virtual machine and not on your local computer.</span></span>

## <span data-ttu-id="25a01-132"><a id="setup"></a>Python, Django ve Wfastcgı yükleyin</span><span class="sxs-lookup"><span data-stu-id="25a01-132"><a id="setup"> </a>Install Python, Django, and WFastCGI</span></span>
> [!NOTE]
> <span data-ttu-id="25a01-133">Internet Explorer kullanarak toodownload tooconfigure Internet Explorer olabilir **Artırılmış Güvenlik Yapılandırması** ayarlar.</span><span class="sxs-lookup"><span data-stu-id="25a01-133">toodownload by using Internet Explorer, you might have tooconfigure Internet Explorer **Enhanced Security Configuration** settings.</span></span> <span data-ttu-id="25a01-134">toodo bunu, **Başlat** > **Yönetimsel Araçlar** > **Sunucu Yöneticisi'ni** > **yerel sunucu**.</span><span class="sxs-lookup"><span data-stu-id="25a01-134">toodo this, click **Start** > **Administrative Tools** > **Server Manager** > **Local Server**.</span></span> <span data-ttu-id="25a01-135">Tıklatın **IE Artırılmış Güvenlik Yapılandırması**ve ardından **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="25a01-135">Click **IE Enhanced Security Configuration**, and then select **Off**.</span></span>

1. <span data-ttu-id="25a01-136">Python 2.7 veya Python 3.4 gelen en son sürümlerini Hello yüklemek [python.org][python.org].</span><span class="sxs-lookup"><span data-stu-id="25a01-136">Install hello latest versions of Python 2.7 or Python 3.4 from [python.org][python.org].</span></span>
2. <span data-ttu-id="25a01-137">Merhaba wfastcgı ve django paketler pip kullanarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="25a01-137">Install hello wfastcgi and django packages using pip.</span></span>
   
    <span data-ttu-id="25a01-138">Python 2.7 için komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="25a01-138">For Python 2.7, use hello following command:</span></span>
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    <span data-ttu-id="25a01-139">Python 3.4 için komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="25a01-139">For Python 3.4, use hello following command:</span></span>
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a><span data-ttu-id="25a01-140">IIS Fastcgı ile yükleme</span><span class="sxs-lookup"><span data-stu-id="25a01-140">Install IIS with FastCGI</span></span>
* <span data-ttu-id="25a01-141">Internet Information Services (IIS) Fastcgı desteğiyle yükleyin.</span><span class="sxs-lookup"><span data-stu-id="25a01-141">Install Internet Information Services (IIS) with FastCGI support.</span></span> <span data-ttu-id="25a01-142">Bu işlem birkaç dakika tooexecute sürebilir.</span><span class="sxs-lookup"><span data-stu-id="25a01-142">This might take several minutes tooexecute.</span></span>
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a><span data-ttu-id="25a01-143">Yeni bir Django uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="25a01-143">Create a new Django application</span></span>
1. <span data-ttu-id="25a01-144">C:\inetpub\wwwroot, yeni Django proje toocreate hello aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="25a01-144">In C:\inetpub\wwwroot, toocreate a new Django project, enter hello following command:</span></span>
   
   <span data-ttu-id="25a01-145">Python 2.7 için komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="25a01-145">For Python 2.7, use hello following command:</span></span>
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   <span data-ttu-id="25a01-146">Python 3.4 için komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="25a01-146">For Python 3.4, use hello following command:</span></span>
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![Merhaba New-AzureService komutunun Hello sonucu](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. <span data-ttu-id="25a01-148">Merhaba `django-admin` komutu Django tabanlı Web siteleri için basit bir yapı oluşturur:</span><span class="sxs-lookup"><span data-stu-id="25a01-148">hello `django-admin` command generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="25a01-149">`helloworld\manage.py`barındırma başlatmak ve durdurmak, Django tabanlı Web sitesi barındırma yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="25a01-149">`helloworld\manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="25a01-150">`helloworld\helloworld\settings.py`Uygulamanız için Django ayarlarına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="25a01-150">`helloworld\helloworld\settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="25a01-151">`helloworld\helloworld\urls.py`her URL ve kendi görünüm arasında Hello eşleme kodu vardır.</span><span class="sxs-lookup"><span data-stu-id="25a01-151">`helloworld\helloworld\urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="25a01-152">Merhaba C:\inetpub\wwwroot\helloworld\helloworld dizininde views.py adlı yeni bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="25a01-152">In hello C:\inetpub\wwwroot\helloworld\helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="25a01-153">Bu dosya hello "hello world" sayfasını işler hello görünüme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="25a01-153">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="25a01-154">Kod düzenleyicinizde hello aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="25a01-154">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="25a01-155">Merhaba urls.py dosyasının Merhaba içeriğine komutları aşağıdaki hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="25a01-155">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a><span data-ttu-id="25a01-156">ISS kurmak</span><span class="sxs-lookup"><span data-stu-id="25a01-156">Set up IIS</span></span>
1. <span data-ttu-id="25a01-157">Merhaba genel applicationhost.config dosyasında hello işleyicileri bölümün kilidini açın.</span><span class="sxs-lookup"><span data-stu-id="25a01-157">In hello global applicationhost.config file, unlock hello handlers section.</span></span>  <span data-ttu-id="25a01-158">Bu, web.config dosyası toouse hello Python işleyicisi sağlar.</span><span class="sxs-lookup"><span data-stu-id="25a01-158">This allows your web.config file toouse hello Python handler.</span></span> <span data-ttu-id="25a01-159">Bu komutu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="25a01-159">Add this command:</span></span>
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. <span data-ttu-id="25a01-160">Wfastcgı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="25a01-160">Activate WFastCGI.</span></span> <span data-ttu-id="25a01-161">Bu tooyour Python yorumlayıcı çalıştırılabilir ve hello wfastcgi.py betik başvuran bir uygulama toohello genel applicationhost.config dosyası ekler.</span><span class="sxs-lookup"><span data-stu-id="25a01-161">This adds an application toohello global applicationhost.config file, which refers tooyour Python interpreter executable and hello wfastcgi.py script.</span></span>
   
    <span data-ttu-id="25a01-162">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="25a01-162">In Python 2.7:</span></span>
   
        C:\python27\scripts\wfastcgi-enable
   
    <span data-ttu-id="25a01-163">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="25a01-163">In Python 3.4:</span></span>
   
        C:\python34\scripts\wfastcgi-enable
3. <span data-ttu-id="25a01-164">C:\inetpub\wwwroot\helloworld içinde bir web.config dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="25a01-164">In C:\inetpub\wwwroot\helloworld, create a web.config file.</span></span> <span data-ttu-id="25a01-165">Merhaba hello değerini `scriptProcessor` özniteliği, önceki adımı hello hello çıktısını eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="25a01-165">hello value of hello `scriptProcessor` attribute should match hello output from hello preceding step.</span></span> <span data-ttu-id="25a01-166">Merhaba wfastcgı ayarı hakkında daha fazla bilgi için bkz: [pypı wfastcgı][wfastcgi].</span><span class="sxs-lookup"><span data-stu-id="25a01-166">For more information about hello wfastcgi setting, see [pypi wfastcgi][wfastcgi].</span></span>
   
   <span data-ttu-id="25a01-167">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="25a01-167">In  Python 2.7:</span></span>
   
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
   
   <span data-ttu-id="25a01-168">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="25a01-168">In  Python 3.4:</span></span>
   
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
4. <span data-ttu-id="25a01-169">Merhaba hello IIS varsayılan Web sitesi toopoint toohello Django proje klasörünün konumunu güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="25a01-169">Update hello location of hello IIS default website toopoint toohello Django project folder:</span></span>
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. <span data-ttu-id="25a01-170">Merhaba Web tarayıcınızda yükleyin.</span><span class="sxs-lookup"><span data-stu-id="25a01-170">Load hello webpage in your browser.</span></span>

![Bir tarayıcı penceresinde hello hello world sayfasını Azure üzerinde görüntüler.][1]

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="25a01-172">Azure, sanal makineyi Kapat</span><span class="sxs-lookup"><span data-stu-id="25a01-172">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="25a01-173">Bu öğreticiyi tamamladığınızda, kapatıldı veya hello hello öğretici için oluşturduğunuz Azure VM Kaldır öneririz.</span><span class="sxs-lookup"><span data-stu-id="25a01-173">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="25a01-174">Bu diğer öğreticileri için kaynakları serbest bırakır ve Azure kullanım ücretlerinin yansıtılmasını önleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25a01-174">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
