---
title: "Azure Linux VM'de Django ile aaaPython web uygulaması | Microsoft Docs"
description: "Nasıl toohost Django tabanlı bir web uygulaması bir Linux VM kullanarak azure'da öğrenin."
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
ms.openlocfilehash: 520c47e19e8ffb4bb866f70772d506ddf76e242c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a><span data-ttu-id="67045-103">Django Hello World web uygulamasında bir Linux VM</span><span class="sxs-lookup"><span data-stu-id="67045-103">Django Hello World web app on a Linux VM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="67045-104">Windows</span><span class="sxs-lookup"><span data-stu-id="67045-104">Windows</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [<span data-ttu-id="67045-105">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="67045-105">Mac/Linux</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="67045-106">Bu öğretici şunların nasıl yapıldığını gösterir toohost Linux Azure Virtual Machines'de azure'da Django tabanlı Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="67045-106">This tutorial shows you how toohost a Django-based website in Linux in Azure Virtual Machines.</span></span> <span data-ttu-id="67045-107">Merhaba öğreticide, Azure ile konusunda deneyim varsayıyoruz.</span><span class="sxs-lookup"><span data-stu-id="67045-107">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="67045-108">Merhaba öğreticiyi tamamladığınızda, Django tabanlı bir uygulamayı oluşturan ve hello bulutta çalışan sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="67045-108">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="67045-109">Şunları nasıl yapacağınızı öğrenin:</span><span class="sxs-lookup"><span data-stu-id="67045-109">Learn how to:</span></span>

* <span data-ttu-id="67045-110">Azure sanal makinesi toohost Django ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="67045-110">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="67045-111">Bu öğretici açıklar ancak nasıl toodo bu **Linux**, yapabileceğiniz aynı Azure üzerinde barındırılan bir Windows Server VM için hello.</span><span class="sxs-lookup"><span data-stu-id="67045-111">Although this tutorial explains how toodo this for **Linux**, you can do hello same for a Windows Server VM hosted in Azure.</span></span> 
* <span data-ttu-id="67045-112">Yeni bir Django uygulama içinde Linux oluşturun.</span><span class="sxs-lookup"><span data-stu-id="67045-112">Create a new Django application in Linux.</span></span>

<span data-ttu-id="67045-113">Merhaba öğretici nasıl toobuild temel bir Hello World web uygulaması gösterir.</span><span class="sxs-lookup"><span data-stu-id="67045-113">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="67045-114">Merhaba uygulaması bir Azure sanal makinesi barındırılır.</span><span class="sxs-lookup"><span data-stu-id="67045-114">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="67045-115">Aşağıdaki ekran görüntüsü hello tamamlandı Merhaba uygulaması gösterir:</span><span class="sxs-lookup"><span data-stu-id="67045-115">hello following screenshot shows hello completed application:</span></span>

![Bir tarayıcı penceresinde hello Hello World sayfası Azure'da görüntüler.](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="67045-117">Oluşturma ve Azure sanal makinesi toohost Django ayarlama</span><span class="sxs-lookup"><span data-stu-id="67045-117">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="67045-118">toocreate hello Ubuntu Server 14.04 LTS dağıtım, bir Azure sanal makinesi bkz [hello Azure portalında bir Linux sanal makine oluşturmak](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="67045-118">toocreate an Azure virtual machine with hello Ubuntu Server 14.04 LTS distribution, see [Create a Linux virtual machine in hello Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="67045-119">Bir SSH ortak anahtarı kullanmak yerine parola kimlik doğrulaması da seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67045-119">You also can choose password authentication instead of using an SSH public key.</span></span>
2. <span data-ttu-id="67045-120">tooedit hello ağ güvenlik grubu tooallow gelen HTTP trafiği tooport 80 bkz [hello Azure portal ağ güvenlik grupları oluşturma](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="67045-120">tooedit hello network security group tooallow incoming HTTP traffic tooport 80, see [Create network security groups in hello Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>
3. <span data-ttu-id="67045-121">(İsteğe bağlı) Varsayılan olarak, yeni bir sanal makine bir tam etki alanı adı (FQDN) sahip değil.</span><span class="sxs-lookup"><span data-stu-id="67045-121">(Optional) By default, your new virtual machine doesn't have a fully qualified domain name (FQDN).</span></span>  <span data-ttu-id="67045-122">toocreate bir FQDN ile VM bkz [bir FQDN için bir Windows VM hello Azure portal oluşturma](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="67045-122">toocreate a VM with an FQDN, see [Create an FQDN in hello Azure portal for a Windows VM](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="67045-123">Bu adım, bu öğreticiyi tamamlamak için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="67045-123">This step is not required for completing this tutorial.</span></span>

## <span data-ttu-id="67045-124"><a id="setup"></a>Hello geliştirme ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="67045-124"><a id="setup"> </a>Set up hello development environment</span></span>
> [!NOTE]
> <span data-ttu-id="67045-125">Merhaba tooinstall Python gerekir veya toouse hello istemci kitaplıkları istiyorsanız bkz [Python Yükleme Kılavuzu'na](../../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="67045-125">If you need tooinstall Python or want toouse hello client libraries, see hello [Python installation guide](../../python-how-to-install.md).</span></span>

<span data-ttu-id="67045-126">Merhaba Ubuntu Linux VM için Python 2.7 önceden yüklenmiş olsa da, Apache veya Django ile birlikte gelmez.</span><span class="sxs-lookup"><span data-stu-id="67045-126">hello Ubuntu Linux VM has Python 2.7 preinstalled, but it doesn't come with Apache or Django.</span></span> <span data-ttu-id="67045-127">Aşağıdaki adımları tooconnect tooyour VM hello tamamlamak ve Apache ve Django yükleyin:</span><span class="sxs-lookup"><span data-stu-id="67045-127">Complete hello following steps tooconnect tooyour VM and install Apache and Django:</span></span>

1. <span data-ttu-id="67045-128">Yeni bir Terminal penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="67045-128">Open a new Terminal window.</span></span>
2. <span data-ttu-id="67045-129">tooconnect toohello Azure VM, komutu aşağıdaki hello girin.</span><span class="sxs-lookup"><span data-stu-id="67045-129">tooconnect toohello Azure VM, enter hello following command.</span></span> <span data-ttu-id="67045-130">Bir FQDN oluşturmadıysanız, hello sanal makine hello Azure portal Özet görüntülenen hello ortak IP adresini kullanarak bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="67045-130">If you didn't create an FQDN, you can connect by using hello public IP address that's displayed in hello virtual machine summary in hello Azure portal.</span></span>
   
       $ ssh yourusername@yourVmUrl
3. <span data-ttu-id="67045-131">tooinstall Django, hello aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="67045-131">tooinstall Django, enter hello following commands:</span></span>
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. <span data-ttu-id="67045-132">mod-wsgı ile tooinstall Apache hello aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="67045-132">tooinstall Apache with mod-wsgi, enter hello following command:</span></span>
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a><span data-ttu-id="67045-133">Yeni bir Django uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="67045-133">Create a new Django app</span></span>
1. <span data-ttu-id="67045-134">toouse SSH tooaccess VM, açık hello Terminal penceresi bölüm önceki hello kullanılır.</span><span class="sxs-lookup"><span data-stu-id="67045-134">toouse SSH tooaccess your VM, open hello Terminal window you used in hello preceding section.</span></span>
2. <span data-ttu-id="67045-135">toocreate yeni Django proje hello aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="67045-135">toocreate a new Django project, enter hello following commands:</span></span>
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   <span data-ttu-id="67045-136">Merhaba `django-admin.py` betik Django tabanlı Web siteleri için basit bir yapı oluşturur:</span><span class="sxs-lookup"><span data-stu-id="67045-136">hello `django-admin.py` script generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="67045-137">`helloworld/manage.py`barındırma başlatmak ve durdurmak, Django tabanlı Web sitesi barındırma yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="67045-137">`helloworld/manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="67045-138">`helloworld/helloworld/settings.py`Uygulamanız için Django ayarlarına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="67045-138">`helloworld/helloworld/settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="67045-139">`helloworld/helloworld/urls.py`her URL ve kendi görünüm arasında Hello eşleme kodu vardır.</span><span class="sxs-lookup"><span data-stu-id="67045-139">`helloworld/helloworld/urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="67045-140">Merhaba /var/www/helloworld/helloworld dizininde views.py adlı yeni bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="67045-140">In hello /var/www/helloworld/helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="67045-141">Bu dosya hello "hello world" sayfasını işler hello görünüme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="67045-141">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="67045-142">Kod düzenleyicinizde hello aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="67045-142">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="67045-143">Merhaba urls.py dosyasının Merhaba içeriğine komutları aşağıdaki hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="67045-143">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a><span data-ttu-id="67045-144">Apache ayarlayın</span><span class="sxs-lookup"><span data-stu-id="67045-144">Set up Apache</span></span>
1. <span data-ttu-id="67045-145">Merhaba /etc/apache2/sites-available/helloworld.conf klasöründe bir Apache sanal ana bilgisayar yapılandırma dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="67045-145">In hello /etc/apache2/sites-available/helloworld.conf folder, create an Apache virtual host configuration file.</span></span> <span data-ttu-id="67045-146">Değerleri aşağıdaki hello içeriği toohello ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="67045-146">Set hello contents toohello following values.</span></span> <span data-ttu-id="67045-147">Değiştir *yourVmName* kullanmakta olduğunuz hello makinenin hello gerçek adıyla (örneğin, *pyubuntu*).</span><span class="sxs-lookup"><span data-stu-id="67045-147">Replace *yourVmName* with hello actual name of hello machine you are using (for example, *pyubuntu*).</span></span>
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. <span data-ttu-id="67045-148">tooactivate hello sitesi, komutu aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="67045-148">tooactivate hello site, use hello following command:</span></span>
   
       $ sudo a2ensite helloworld
3. <span data-ttu-id="67045-149">toorestart Apache, komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="67045-149">toorestart Apache, use hello following command:</span></span>
   
       $ sudo service apache2 reload
4. <span data-ttu-id="67045-150">Merhaba Web tarayıcınızda yük:</span><span class="sxs-lookup"><span data-stu-id="67045-150">Load hello webpage in your browser:</span></span>
   
   ![Bir tarayıcı penceresinde hello hello world sayfasını Azure'da görüntüler.](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="67045-152">Azure, sanal makineyi Kapat</span><span class="sxs-lookup"><span data-stu-id="67045-152">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="67045-153">Bu öğreticiyi tamamladığınızda, kapatıldı veya hello hello öğretici için oluşturduğunuz Azure VM Kaldır öneririz.</span><span class="sxs-lookup"><span data-stu-id="67045-153">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="67045-154">Bu diğer öğreticileri için kaynakları serbest bırakır ve Azure kullanım ücretlerinin yansıtılmasını önleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67045-154">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

