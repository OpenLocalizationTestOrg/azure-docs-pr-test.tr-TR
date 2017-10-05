---
title: "Bir Windows Server Azure VM'de Django web uygulaması | Microsoft Docs"
description: "Bir Windows Server 2012 R2 Datacenter VM ile klasik dağıtım modelini kullanarak azure'da Django tabanlı bir Web sitesi barındırma öğrenin."
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
ms.openlocfilehash: 283a296fb39863c2801be1093cc4f56904786abd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a><span data-ttu-id="e609e-103">Windows Server VM üzerinde Django Hello World web uygulaması</span><span class="sxs-lookup"><span data-stu-id="e609e-103">Django Hello World web app on a Windows Server VM</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="e609e-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager ve klasik dağıtım modeli](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e609e-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and the classic deployment model](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e609e-105">Bu makalede Klasik dağıtım modeli açıklanır.</span><span class="sxs-lookup"><span data-stu-id="e609e-105">This article describes the classic deployment model.</span></span> <span data-ttu-id="e609e-106">En yeni dağıtımların Resource Manager modelini kullanmasını öneririz.</span><span class="sxs-lookup"><span data-stu-id="e609e-106">We recommend that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="e609e-107">Bu öğretici, Azure Virtual Machines'de Windows Server'daki Django tabanlı bir Web sitesi barındırmak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="e609e-107">This tutorial shows you how to host a Django-based website in Windows Server in Azure Virtual Machines.</span></span> <span data-ttu-id="e609e-108">Öğreticide, Azure ile konusunda deneyim varsayıyoruz.</span><span class="sxs-lookup"><span data-stu-id="e609e-108">In the tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="e609e-109">Öğreticiyi tamamladığınızda, Django tabanlı bir uygulamayı oluşturan ve bulutta çalışan sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="e609e-109">When you finish the tutorial, you can have a Django-based application up and running in the cloud.</span></span>

<span data-ttu-id="e609e-110">Şunları nasıl yapacağınızı öğrenin:</span><span class="sxs-lookup"><span data-stu-id="e609e-110">Learn how to:</span></span>

* <span data-ttu-id="e609e-111">Bir Azure sanal makinesi konağa Django ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e609e-111">Set up an Azure virtual machine to host Django.</span></span> <span data-ttu-id="e609e-112">Bu öğretici, bunu yapmak açıklanmaktadır ancak **Windows Server**, Azure'da bir Linux VM barındırılan için aynı yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e609e-112">Although this tutorial explains how to do this for **Windows Server**, you can do the same for a Linux VM hosted in Azure.</span></span>
* <span data-ttu-id="e609e-113">Yeni bir Django uygulaması Windows oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e609e-113">Create a new Django application in Windows.</span></span>

<span data-ttu-id="e609e-114">Öğretici, temel bir Hello World web uygulamasının nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e609e-114">The tutorial shows you how to build a basic Hello World web application.</span></span> <span data-ttu-id="e609e-115">Uygulamayı bir Azure sanal makinesi barındırılır.</span><span class="sxs-lookup"><span data-stu-id="e609e-115">The application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="e609e-116">Aşağıdaki ekran görüntüsünde tamamlanan uygulama gösterilir:</span><span class="sxs-lookup"><span data-stu-id="e609e-116">The following screenshot shows the completed application:</span></span>

![Bir tarayıcı penceresi Azure'da hello world sayfasını görüntüler][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-to-host-django"></a><span data-ttu-id="e609e-118">Oluşturma ve bir Azure sanal makinesi konağa Django ayarlama</span><span class="sxs-lookup"><span data-stu-id="e609e-118">Create and set up an Azure virtual machine to host Django</span></span>

1. <span data-ttu-id="e609e-119">Bir Azure sanal makinesi ile Windows Server 2012 R2 Datacenter dağıtımı oluşturmak için bkz: [Azure portalında Windows çalıştıran bir sanal makine oluşturma](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="e609e-119">To create an Azure virtual machine with the Windows Server 2012 R2 Datacenter distribution, see [Create a virtual machine running Windows in the Azure portal](tutorial.md).</span></span>
2. <span data-ttu-id="e609e-120">Bağlantı noktası 80 trafiğinden web sanal makinede 80 numaralı bağlantı noktasına yönlendirmek için Azure ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="e609e-120">Set Azure to direct port 80 traffic from the web to port 80 on the virtual machine:</span></span>
   
   1. <span data-ttu-id="e609e-121">Azure portalında panoya gidin ve yeni oluşturulan sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="e609e-121">In the Azure portal, go to the dashboard and select your newly created virtual machine.</span></span>
   2. <span data-ttu-id="e609e-122">**Uç noktaları**’na ve ardından **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e609e-122">Click **Endpoints**, and then click **Add**.</span></span>

     ![Bir uç nokta ekleme](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. <span data-ttu-id="e609e-124">Üzerinde **uç nokta ekleme** sayfası için **adı**, girin **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="e609e-124">On the **Add endpoint** page, for **Name**, enter **HTTP**.</span></span> <span data-ttu-id="e609e-125">Ortak ve özel TCP bağlantı noktaları kümesine **80**.</span><span class="sxs-lookup"><span data-stu-id="e609e-125">Set the public and private TCP ports to **80**.</span></span>

     ![Bir ad girin ve ortak ve özel bağlantı noktalarını ayarlayın](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. <span data-ttu-id="e609e-127">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e609e-127">Click **OK**.</span></span>
     
3. <span data-ttu-id="e609e-128">Panosunda, VM'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e609e-128">In the dashboard, select your VM.</span></span> <span data-ttu-id="e609e-129">Yeni oluşturulan Azure sanal makineye uzaktan oturum açmak için Uzak Masaüstü Protokolü (RDP) kullanmak için tıklatın **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="e609e-129">To use Remote Desktop Protocol (RDP) to remotely sign in to the newly created Azure virtual machine, click **Connect**.</span></span>  

> [!IMPORTANT] 
> <span data-ttu-id="e609e-130">Aşağıdaki yönergeler, sanal makineye doğru şekilde oturum açtığına varsayalım.</span><span class="sxs-lookup"><span data-stu-id="e609e-130">The following instructions assume that you signed in to the virtual machine correctly.</span></span> <span data-ttu-id="e609e-131">Ayrıca komutları sanal makine ve yerel bilgisayarınızda değil dağıttığınız varsayılmıştır.</span><span class="sxs-lookup"><span data-stu-id="e609e-131">They also assume that you are issuing commands in the virtual machine and not on your local computer.</span></span>

## <span data-ttu-id="e609e-132"><a id="setup"></a>Python, Django ve Wfastcgı yükleyin</span><span class="sxs-lookup"><span data-stu-id="e609e-132"><a id="setup"> </a>Install Python, Django, and WFastCGI</span></span>
> [!NOTE]
> <span data-ttu-id="e609e-133">Internet Explorer kullanarak indirmek için Internet Explorer yapılandırmanız gerekebilir **Artırılmış Güvenlik Yapılandırması** ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e609e-133">To download by using Internet Explorer, you might have to configure Internet Explorer **Enhanced Security Configuration** settings.</span></span> <span data-ttu-id="e609e-134">Bunu yapmak için tıklatın **Başlat** > **Yönetimsel Araçlar** > **Sunucu Yöneticisi'ni** > **yerel sunucu**.</span><span class="sxs-lookup"><span data-stu-id="e609e-134">To do this, click **Start** > **Administrative Tools** > **Server Manager** > **Local Server**.</span></span> <span data-ttu-id="e609e-135">Tıklatın **IE Artırılmış Güvenlik Yapılandırması**ve ardından **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="e609e-135">Click **IE Enhanced Security Configuration**, and then select **Off**.</span></span>

1. <span data-ttu-id="e609e-136">Python 2.7 veya Python 3.4 gelen en son sürümlerini yüklemek [python.org][python.org].</span><span class="sxs-lookup"><span data-stu-id="e609e-136">Install the latest versions of Python 2.7 or Python 3.4 from [python.org][python.org].</span></span>
2. <span data-ttu-id="e609e-137">PIP kullanarak wfastcgı ve django paketleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e609e-137">Install the wfastcgi and django packages using pip.</span></span>
   
    <span data-ttu-id="e609e-138">Python 2.7 için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="e609e-138">For Python 2.7, use the following command:</span></span>
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    <span data-ttu-id="e609e-139">Python 3.4 için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="e609e-139">For Python 3.4, use the following command:</span></span>
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a><span data-ttu-id="e609e-140">IIS Fastcgı ile yükleme</span><span class="sxs-lookup"><span data-stu-id="e609e-140">Install IIS with FastCGI</span></span>
* <span data-ttu-id="e609e-141">Internet Information Services (IIS) Fastcgı desteğiyle yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e609e-141">Install Internet Information Services (IIS) with FastCGI support.</span></span> <span data-ttu-id="e609e-142">Bu yürütmek için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="e609e-142">This might take several minutes to execute.</span></span>
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a><span data-ttu-id="e609e-143">Yeni bir Django uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e609e-143">Create a new Django application</span></span>
1. <span data-ttu-id="e609e-144">C:\inetpub\wwwroot içinde yeni bir Django projesi oluşturmak için aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="e609e-144">In C:\inetpub\wwwroot, to create a new Django project, enter the following command:</span></span>
   
   <span data-ttu-id="e609e-145">Python 2.7 için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="e609e-145">For Python 2.7, use the following command:</span></span>
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   <span data-ttu-id="e609e-146">Python 3.4 için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="e609e-146">For Python 3.4, use the following command:</span></span>
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![New-AzureService komutunun sonucu](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. <span data-ttu-id="e609e-148">`django-admin` Komutu Django tabanlı Web siteleri için basit bir yapı oluşturur:</span><span class="sxs-lookup"><span data-stu-id="e609e-148">The `django-admin` command generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="e609e-149">`helloworld\manage.py`barındırma başlatmak ve durdurmak, Django tabanlı Web sitesi barındırma yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e609e-149">`helloworld\manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="e609e-150">`helloworld\helloworld\settings.py`Uygulamanız için Django ayarlarına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e609e-150">`helloworld\helloworld\settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="e609e-151">`helloworld\helloworld\urls.py`her URL ve kendi görünüm arasında eşleme koduna sahip.</span><span class="sxs-lookup"><span data-stu-id="e609e-151">`helloworld\helloworld\urls.py` has the mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="e609e-152">C:\inetpub\wwwroot\helloworld\helloworld dizininde views.py adlı yeni bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e609e-152">In the C:\inetpub\wwwroot\helloworld\helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="e609e-153">Bu dosya, "hello world" sayfasını işler görünüme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e609e-153">This file has the view that renders the "hello world" page.</span></span> <span data-ttu-id="e609e-154">Kod düzenleyicisinde, aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="e609e-154">In your code editor, enter the following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="e609e-155">Urls.py dosyasının içeriğini aşağıdaki komutları ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="e609e-155">Replace the contents of the urls.py file with the following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a><span data-ttu-id="e609e-156">ISS kurmak</span><span class="sxs-lookup"><span data-stu-id="e609e-156">Set up IIS</span></span>
1. <span data-ttu-id="e609e-157">Genel applicationhost.config dosyasında işleyicileri bölümün kilidini açın.</span><span class="sxs-lookup"><span data-stu-id="e609e-157">In the global applicationhost.config file, unlock the handlers section.</span></span>  <span data-ttu-id="e609e-158">Bu, Python işleyicisi kullanmak web.config dosyanızın sağlar.</span><span class="sxs-lookup"><span data-stu-id="e609e-158">This allows your web.config file to use the Python handler.</span></span> <span data-ttu-id="e609e-159">Bu komutu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e609e-159">Add this command:</span></span>
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. <span data-ttu-id="e609e-160">Wfastcgı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e609e-160">Activate WFastCGI.</span></span> <span data-ttu-id="e609e-161">Bu yürütülebilir, Python yorumlayıcı ve wfastcgi.py betik başvuran genel applicationhost.config dosyasının bir uygulama ekler.</span><span class="sxs-lookup"><span data-stu-id="e609e-161">This adds an application to the global applicationhost.config file, which refers to your Python interpreter executable and the wfastcgi.py script.</span></span>
   
    <span data-ttu-id="e609e-162">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="e609e-162">In Python 2.7:</span></span>
   
        C:\python27\scripts\wfastcgi-enable
   
    <span data-ttu-id="e609e-163">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="e609e-163">In Python 3.4:</span></span>
   
        C:\python34\scripts\wfastcgi-enable
3. <span data-ttu-id="e609e-164">C:\inetpub\wwwroot\helloworld içinde bir web.config dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e609e-164">In C:\inetpub\wwwroot\helloworld, create a web.config file.</span></span> <span data-ttu-id="e609e-165">Değeri `scriptProcessor` özniteliği, önceki adımdaki çıktı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="e609e-165">The value of the `scriptProcessor` attribute should match the output from the preceding step.</span></span> <span data-ttu-id="e609e-166">Wfastcgı ayarı hakkında daha fazla bilgi için bkz: [pypı wfastcgı][wfastcgi].</span><span class="sxs-lookup"><span data-stu-id="e609e-166">For more information about the wfastcgi setting, see [pypi wfastcgi][wfastcgi].</span></span>
   
   <span data-ttu-id="e609e-167">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="e609e-167">In  Python 2.7:</span></span>
   
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
   
   <span data-ttu-id="e609e-168">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="e609e-168">In  Python 3.4:</span></span>
   
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
4. <span data-ttu-id="e609e-169">Django proje klasöre işaret IIS varsayılan Web sitesi konumunu güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="e609e-169">Update the location of the IIS default website to point to the Django project folder:</span></span>
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. <span data-ttu-id="e609e-170">Web tarayıcınızda yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e609e-170">Load the webpage in your browser.</span></span>

![Bir tarayıcı penceresinde hello world sayfasını Azure üzerinde görüntüler.][1]

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="e609e-172">Azure, sanal makineyi Kapat</span><span class="sxs-lookup"><span data-stu-id="e609e-172">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="e609e-173">Bu öğreticiyi tamamladığınızda, kapatıldı veya öğretici için oluşturduğunuz Azure VM Kaldır öneririz.</span><span class="sxs-lookup"><span data-stu-id="e609e-173">When you're done with this tutorial, we recommend that you shut down or remove the Azure VM you created for the tutorial.</span></span> <span data-ttu-id="e609e-174">Bu diğer öğreticileri için kaynakları serbest bırakır ve Azure kullanım ücretlerinin yansıtılmasını önleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e609e-174">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
