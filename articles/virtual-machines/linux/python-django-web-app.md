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
# <a name="django-hello-world-web-app-on-a-linux-vm"></a>Django Hello World web uygulamasında bir Linux VM
> [!div class="op_single_selector"]
> * [Windows](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [Mac/Linux](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

Bu öğretici şunların nasıl yapıldığını gösterir toohost Linux Azure Virtual Machines'de azure'da Django tabanlı Web sitesi. Merhaba öğreticide, Azure ile konusunda deneyim varsayıyoruz. Merhaba öğreticiyi tamamladığınızda, Django tabanlı bir uygulamayı oluşturan ve hello bulutta çalışan sahip olabilir.

Şunları nasıl yapacağınızı öğrenin:

* Azure sanal makinesi toohost Django ayarlayın. Bu öğretici açıklar ancak nasıl toodo bu **Linux**, yapabileceğiniz aynı Azure üzerinde barındırılan bir Windows Server VM için hello. 
* Yeni bir Django uygulama içinde Linux oluşturun.

Merhaba öğretici nasıl toobuild temel bir Hello World web uygulaması gösterir. Merhaba uygulaması bir Azure sanal makinesi barındırılır.

Aşağıdaki ekran görüntüsü hello tamamlandı Merhaba uygulaması gösterir:

![Bir tarayıcı penceresinde hello Hello World sayfası Azure'da görüntüler.](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>Oluşturma ve Azure sanal makinesi toohost Django ayarlama

1. toocreate hello Ubuntu Server 14.04 LTS dağıtım, bir Azure sanal makinesi bkz [hello Azure portalında bir Linux sanal makine oluşturmak](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Bir SSH ortak anahtarı kullanmak yerine parola kimlik doğrulaması da seçebilirsiniz.
2. tooedit hello ağ güvenlik grubu tooallow gelen HTTP trafiği tooport 80 bkz [hello Azure portal ağ güvenlik grupları oluşturma](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).
3. (İsteğe bağlı) Varsayılan olarak, yeni bir sanal makine bir tam etki alanı adı (FQDN) sahip değil.  toocreate bir FQDN ile VM bkz [bir FQDN için bir Windows VM hello Azure portal oluşturma](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Bu adım, bu öğreticiyi tamamlamak için gerekli değildir.

## <a id="setup"></a>Hello geliştirme ortamını ayarlama
> [!NOTE]
> Merhaba tooinstall Python gerekir veya toouse hello istemci kitaplıkları istiyorsanız bkz [Python Yükleme Kılavuzu'na](../../python-how-to-install.md).

Merhaba Ubuntu Linux VM için Python 2.7 önceden yüklenmiş olsa da, Apache veya Django ile birlikte gelmez. Aşağıdaki adımları tooconnect tooyour VM hello tamamlamak ve Apache ve Django yükleyin:

1. Yeni bir Terminal penceresi açın.
2. tooconnect toohello Azure VM, komutu aşağıdaki hello girin. Bir FQDN oluşturmadıysanız, hello sanal makine hello Azure portal Özet görüntülenen hello ortak IP adresini kullanarak bağlanabilir.
   
       $ ssh yourusername@yourVmUrl
3. tooinstall Django, hello aşağıdaki komutları girin:
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. mod-wsgı ile tooinstall Apache hello aşağıdaki komutu girin:
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a>Yeni bir Django uygulaması oluşturma
1. toouse SSH tooaccess VM, açık hello Terminal penceresi bölüm önceki hello kullanılır.
2. toocreate yeni Django proje hello aşağıdaki komutları girin:
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   Merhaba `django-admin.py` betik Django tabanlı Web siteleri için basit bir yapı oluşturur:
   
   * `helloworld/manage.py`barındırma başlatmak ve durdurmak, Django tabanlı Web sitesi barındırma yardımcı olur.
   * `helloworld/helloworld/settings.py`Uygulamanız için Django ayarlarına sahiptir.
   * `helloworld/helloworld/urls.py`her URL ve kendi görünüm arasında Hello eşleme kodu vardır.
3. Merhaba /var/www/helloworld/helloworld dizininde views.py adlı yeni bir dosya oluşturun. Bu dosya hello "hello world" sayfasını işler hello görünüme sahiptir. Kod düzenleyicinizde hello aşağıdaki komutları girin:
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. Merhaba urls.py dosyasının Merhaba içeriğine komutları aşağıdaki hello ile değiştirin:
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a>Apache ayarlayın
1. Merhaba /etc/apache2/sites-available/helloworld.conf klasöründe bir Apache sanal ana bilgisayar yapılandırma dosyası oluşturun. Değerleri aşağıdaki hello içeriği toohello ayarlayın. Değiştir *yourVmName* kullanmakta olduğunuz hello makinenin hello gerçek adıyla (örneğin, *pyubuntu*).
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. tooactivate hello sitesi, komutu aşağıdaki kullanım hello:
   
       $ sudo a2ensite helloworld
3. toorestart Apache, komutu aşağıdaki hello kullan:
   
       $ sudo service apache2 reload
4. Merhaba Web tarayıcınızda yük:
   
   ![Bir tarayıcı penceresinde hello hello world sayfasını Azure'da görüntüler.](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a>Azure, sanal makineyi Kapat
Bu öğreticiyi tamamladığınızda, kapatıldı veya hello hello öğretici için oluşturduğunuz Azure VM Kaldır öneririz. Bu diğer öğreticileri için kaynakları serbest bırakır ve Azure kullanım ücretlerinin yansıtılmasını önleyebilirsiniz.

