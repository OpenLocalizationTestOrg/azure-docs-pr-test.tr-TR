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
# <a name="django-hello-world-web-app-on-a-linux-vm"></a>Django Hello World web uygulamasında bir Linux VM
> [!div class="op_single_selector"]
> * [Windows](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [Mac/Linux](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

Bu öğretici Linux Azure Virtual Machines'de azure'da Django tabanlı Web sitesi barındırmak nasıl gösterir. Öğreticide, Azure ile konusunda deneyim varsayıyoruz. Öğreticiyi tamamladığınızda, Django tabanlı bir uygulamayı oluşturan ve bulutta çalışan sahip olabilir.

Şunları nasıl yapacağınızı öğrenin:

* Bir Azure sanal makinesi konağa Django ayarlayın. Bu öğretici, bunu yapmak açıklanmaktadır ancak **Linux**, Azure'da barındırılan bir Windows Server VM için aynı yapabilirsiniz. 
* Yeni bir Django uygulama içinde Linux oluşturun.

Öğretici, temel bir Hello World web uygulamasının nasıl oluşturulacağını gösterir. Uygulamayı bir Azure sanal makinesi barındırılır.

Aşağıdaki ekran görüntüsünde tamamlanan uygulama gösterilir:

![Bir tarayıcı penceresinde Hello World sayfası Azure'da görüntüler.](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-to-host-django"></a>Oluşturma ve bir Azure sanal makinesi konağa Django ayarlama

1. Ubuntu Server 14.04 LTS dağıtımı ile bir Azure sanal makinesini oluşturmak için bkz: [Azure portalında bir Linux sanal makine oluşturma](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Bir SSH ortak anahtarı kullanmak yerine parola kimlik doğrulaması da seçebilirsiniz.
2. Gelen HTTP trafiği 80 numaralı bağlantı noktasına izin vermek için ağ güvenlik grubu düzenlemek için bkz: [Azure portalında ağ güvenlik grupları oluşturma](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).
3. (İsteğe bağlı) Varsayılan olarak, yeni bir sanal makine bir tam etki alanı adı (FQDN) sahip değil.  Bir FQDN ile bir VM oluşturmak için bkz: [bir FQDN için bir Windows VM Azure portalında oluşturma](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Bu adım, bu öğreticiyi tamamlamak için gerekli değildir.

## <a id="setup"></a>Geliştirme ortamını ayarlama
> [!NOTE]
> Python yüklemek veya istemci kitaplıkları kullanmak istediğiniz görmek gerekirse [Python Yükleme Kılavuzu'na](../../python-how-to-install.md).

Ubuntu Linux VM için Python 2.7 önceden yüklenmiş olsa da, Apache veya Django ile birlikte gelmez. VM'nize bağlanmak ve Apache ve Django yüklemek için aşağıdaki adımları tamamlayın:

1. Yeni bir Terminal penceresi açın.
2. Azure VM'ye bağlanmak için aşağıdaki komutu girin. Bir FQDN oluşturmadıysanız, sanal makinede Azure portalında Özet görüntülenen ortak IP adresini kullanarak bağlanabilir.
   
       $ ssh yourusername@yourVmUrl
3. Django yüklemek için aşağıdaki komutları girin:
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. Apache mod-wsgı ile yüklemek için aşağıdaki komutu girin:
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a>Yeni bir Django uygulaması oluşturma
1. SSH VM erişmek üzere kullanmak için önceki bölümde kullanılan Terminal penceresi açın.
2. Yeni bir Django projesi oluşturmak için aşağıdaki komutları girin:
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   `django-admin.py` Betik Django tabanlı Web siteleri için basit bir yapı oluşturur:
   
   * `helloworld/manage.py`barındırma başlatmak ve durdurmak, Django tabanlı Web sitesi barındırma yardımcı olur.
   * `helloworld/helloworld/settings.py`Uygulamanız için Django ayarlarına sahiptir.
   * `helloworld/helloworld/urls.py`her URL ve kendi görünüm arasında eşleme koduna sahip.
3. /Var/www/helloworld/helloworld dizininde views.py adlı yeni bir dosya oluşturun. Bu dosya, "hello world" sayfasını işler görünüme sahiptir. Kod düzenleyicisinde, aşağıdaki komutları girin:
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. Urls.py dosyasının içeriğini aşağıdaki komutları ile değiştirin:
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a>Apache ayarlayın
1. /Etc/apache2/sites-available/helloworld.conf klasöründe bir Apache sanal ana bilgisayar yapılandırma dosyası oluşturun. İçeriği aşağıdaki değerleri ayarlayın. Değiştir *yourVmName* kullanmakta olduğunuz makinenin gerçek adıyla (örneğin, *pyubuntu*).
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. Siteyi etkinleştirmek için aşağıdaki komutu kullanın:
   
       $ sudo a2ensite helloworld
3. Apache yeniden başlatmak için aşağıdaki komutu kullanın:
   
       $ sudo service apache2 reload
4. Web tarayıcınızda yük:
   
   ![Bir tarayıcı penceresi Azure'da hello world sayfasını görüntüler](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a>Azure, sanal makineyi Kapat
Bu öğreticiyi tamamladığınızda, kapatıldı veya öğretici için oluşturduğunuz Azure VM Kaldır öneririz. Bu diğer öğreticileri için kaynakları serbest bırakır ve Azure kullanım ücretlerinin yansıtılmasını önleyebilirsiniz.

