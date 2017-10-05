---
title: "Python web uygulaması Azure Linux VM'de Django ile | Microsoft Docs"
description: "Bir Linux VM kullanarak azure'da Django tabanlı web uygulaması konağı öğrenin."
services: virtual-machines-linux
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-resource-manager
ms.assetid: 00ad4c2c-4316-4f9a-913f-f7f49b158db7
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 6e2ab8c7da7496d0e2b567a4bdc9341adcf01552
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a><span data-ttu-id="7f6d6-103">Django Hello World web uygulamasında bir Linux VM</span><span class="sxs-lookup"><span data-stu-id="7f6d6-103">Django Hello World web app on a Linux VM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f6d6-104">Windows</span><span class="sxs-lookup"><span data-stu-id="7f6d6-104">Windows</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [<span data-ttu-id="7f6d6-105">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="7f6d6-105">Mac/Linux</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="7f6d6-106">Bu öğretici Linux Azure Virtual Machines'de azure'da Django tabanlı Web sitesi barındırmak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-106">This tutorial shows you how to host a Django-based website in Linux in Azure Virtual Machines.</span></span> <span data-ttu-id="7f6d6-107">Öğreticide, Azure ile konusunda deneyim varsayıyoruz.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-107">In the tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="7f6d6-108">Öğreticiyi tamamladığınızda, Django tabanlı bir uygulamayı oluşturan ve bulutta çalışan sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-108">When you finish the tutorial, you can have a Django-based application up and running in the cloud.</span></span>

<span data-ttu-id="7f6d6-109">Şunları nasıl yapacağınızı öğrenin:</span><span class="sxs-lookup"><span data-stu-id="7f6d6-109">Learn how to:</span></span>

* <span data-ttu-id="7f6d6-110">Bir Azure sanal makinesi konağa Django ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-110">Set up an Azure virtual machine to host Django.</span></span> <span data-ttu-id="7f6d6-111">Bu öğretici, bunu yapmak açıklanmaktadır ancak **Linux**, Azure'da barındırılan bir Windows Server VM için aynı yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-111">Although this tutorial explains how to do this for **Linux**, you can do the same for a Windows Server VM hosted in Azure.</span></span> 
* <span data-ttu-id="7f6d6-112">Yeni bir Django uygulama içinde Linux oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-112">Create a new Django application in Linux.</span></span>

<span data-ttu-id="7f6d6-113">Öğretici, temel bir Hello World web uygulamasının nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-113">The tutorial shows you how to build a basic Hello World web application.</span></span> <span data-ttu-id="7f6d6-114">Uygulamayı bir Azure sanal makinesi barındırılır.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-114">The application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="7f6d6-115">Aşağıdaki ekran görüntüsünde tamamlanan uygulama gösterilir:</span><span class="sxs-lookup"><span data-stu-id="7f6d6-115">The following screenshot shows the completed application:</span></span>

![Bir tarayıcı penceresinde Hello World sayfası Azure'da görüntüler.](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-to-host-django"></a><span data-ttu-id="7f6d6-117">Oluşturma ve bir Azure sanal makinesi konağa Django ayarlama</span><span class="sxs-lookup"><span data-stu-id="7f6d6-117">Create and set up an Azure virtual machine to host Django</span></span>

1. <span data-ttu-id="7f6d6-118">Ubuntu Server 14.04 LTS dağıtımı ile bir Azure sanal makinesini oluşturmak için bkz: [Azure portalında bir Linux sanal makine oluşturma](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7f6d6-118">To create an Azure virtual machine with the Ubuntu Server 14.04 LTS distribution, see [Create a Linux virtual machine in the Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="7f6d6-119">Bir SSH ortak anahtarı kullanmak yerine parola kimlik doğrulaması da seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-119">You also can choose password authentication instead of using an SSH public key.</span></span>
2. <span data-ttu-id="7f6d6-120">Gelen HTTP trafiği 80 numaralı bağlantı noktasına izin vermek için ağ güvenlik grubu düzenlemek için bkz: [Azure portalında ağ güvenlik grupları oluşturma](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="7f6d6-120">To edit the network security group to allow incoming HTTP traffic to port 80, see [Create network security groups in the Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>
3. <span data-ttu-id="7f6d6-121">(İsteğe bağlı) Varsayılan olarak, yeni bir sanal makine bir tam etki alanı adı (FQDN) sahip değil.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-121">(Optional) By default, your new virtual machine doesn't have a fully qualified domain name (FQDN).</span></span>  <span data-ttu-id="7f6d6-122">Bir FQDN ile bir VM oluşturmak için bkz: [bir FQDN için bir Windows VM Azure portalında oluşturma](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7f6d6-122">To create a VM with an FQDN, see [Create an FQDN in the Azure portal for a Windows VM](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="7f6d6-123">Bu adım, bu öğreticiyi tamamlamak için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-123">This step is not required for completing this tutorial.</span></span>

## <span data-ttu-id="7f6d6-124"><a id="setup"></a>Geliştirme ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="7f6d6-124"><a id="setup"> </a>Set up the development environment</span></span>
> [!NOTE]
> <span data-ttu-id="7f6d6-125">Python yüklemek veya istemci kitaplıkları kullanmak istediğiniz görmek gerekirse [Python Yükleme Kılavuzu'na](../../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="7f6d6-125">If you need to install Python or want to use the client libraries, see the [Python installation guide](../../python-how-to-install.md).</span></span>

<span data-ttu-id="7f6d6-126">Ubuntu Linux VM için Python 2.7 önceden yüklenmiş olsa da, Apache veya Django ile birlikte gelmez.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-126">The Ubuntu Linux VM has Python 2.7 preinstalled, but it doesn't come with Apache or Django.</span></span> <span data-ttu-id="7f6d6-127">VM'nize bağlanmak ve Apache ve Django yüklemek için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="7f6d6-127">Complete the following steps to connect to your VM and install Apache and Django:</span></span>

1. <span data-ttu-id="7f6d6-128">Yeni bir Terminal penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-128">Open a new Terminal window.</span></span>
2. <span data-ttu-id="7f6d6-129">Azure VM'ye bağlanmak için aşağıdaki komutu girin.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-129">To connect to the Azure VM, enter the following command.</span></span> <span data-ttu-id="7f6d6-130">Bir FQDN oluşturmadıysanız, sanal makinede Azure portalında Özet görüntülenen ortak IP adresini kullanarak bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-130">If you didn't create an FQDN, you can connect by using the public IP address that's displayed in the virtual machine summary in the Azure portal.</span></span>
   
       $ ssh yourusername@yourVmUrl
3. <span data-ttu-id="7f6d6-131">Django yüklemek için aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="7f6d6-131">To install Django, enter the following commands:</span></span>
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. <span data-ttu-id="7f6d6-132">Apache mod-wsgı ile yüklemek için aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="7f6d6-132">To install Apache with mod-wsgi, enter the following command:</span></span>
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a><span data-ttu-id="7f6d6-133">Yeni bir Django uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f6d6-133">Create a new Django app</span></span>
1. <span data-ttu-id="7f6d6-134">SSH VM erişmek üzere kullanmak için önceki bölümde kullanılan Terminal penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-134">To use SSH to access your VM, open the Terminal window you used in the preceding section.</span></span>
2. <span data-ttu-id="7f6d6-135">Yeni bir Django projesi oluşturmak için aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="7f6d6-135">To create a new Django project, enter the following commands:</span></span>
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   <span data-ttu-id="7f6d6-136">`django-admin.py` Betik Django tabanlı Web siteleri için basit bir yapı oluşturur:</span><span class="sxs-lookup"><span data-stu-id="7f6d6-136">The `django-admin.py` script generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="7f6d6-137">`helloworld/manage.py`barındırma başlatmak ve durdurmak, Django tabanlı Web sitesi barındırma yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-137">`helloworld/manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="7f6d6-138">`helloworld/helloworld/settings.py`Uygulamanız için Django ayarlarına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-138">`helloworld/helloworld/settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="7f6d6-139">`helloworld/helloworld/urls.py`her URL ve kendi görünüm arasında eşleme koduna sahip.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-139">`helloworld/helloworld/urls.py` has the mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="7f6d6-140">/Var/www/helloworld/helloworld dizininde views.py adlı yeni bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-140">In the /var/www/helloworld/helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="7f6d6-141">Bu dosya, "hello world" sayfasını işler görünüme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-141">This file has the view that renders the "hello world" page.</span></span> <span data-ttu-id="7f6d6-142">Kod düzenleyicisinde, aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="7f6d6-142">In your code editor, enter the following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="7f6d6-143">Urls.py dosyasının içeriğini aşağıdaki komutları ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="7f6d6-143">Replace the contents of the urls.py file with the following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a><span data-ttu-id="7f6d6-144">Apache ayarlayın</span><span class="sxs-lookup"><span data-stu-id="7f6d6-144">Set up Apache</span></span>
1. <span data-ttu-id="7f6d6-145">/Etc/apache2/sites-available/helloworld.conf klasöründe bir Apache sanal ana bilgisayar yapılandırma dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-145">In the /etc/apache2/sites-available/helloworld.conf folder, create an Apache virtual host configuration file.</span></span> <span data-ttu-id="7f6d6-146">İçeriği aşağıdaki değerleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-146">Set the contents to the following values.</span></span> <span data-ttu-id="7f6d6-147">Değiştir *yourVmName* kullanmakta olduğunuz makinenin gerçek adıyla (örneğin, *pyubuntu*).</span><span class="sxs-lookup"><span data-stu-id="7f6d6-147">Replace *yourVmName* with the actual name of the machine you are using (for example, *pyubuntu*).</span></span>
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. <span data-ttu-id="7f6d6-148">Siteyi etkinleştirmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7f6d6-148">To activate the site, use the following command:</span></span>
   
       $ sudo a2ensite helloworld
3. <span data-ttu-id="7f6d6-149">Apache yeniden başlatmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7f6d6-149">To restart Apache, use the following command:</span></span>
   
       $ sudo service apache2 reload
4. <span data-ttu-id="7f6d6-150">Web tarayıcınızda yük:</span><span class="sxs-lookup"><span data-stu-id="7f6d6-150">Load the webpage in your browser:</span></span>
   
   ![Bir tarayıcı penceresi Azure'da hello world sayfasını görüntüler](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="7f6d6-152">Azure, sanal makineyi Kapat</span><span class="sxs-lookup"><span data-stu-id="7f6d6-152">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="7f6d6-153">Bu öğreticiyi tamamladığınızda, kapatıldı veya öğretici için oluşturduğunuz Azure VM Kaldır öneririz.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-153">When you're done with this tutorial, we recommend that you shut down or remove the Azure VM you created for the tutorial.</span></span> <span data-ttu-id="7f6d6-154">Bu diğer öğreticileri için kaynakları serbest bırakır ve Azure kullanım ücretlerinin yansıtılmasını önleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f6d6-154">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

