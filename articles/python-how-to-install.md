---
title: aaaInstall Python ve hello SDK - Azure
description: "Bilgi nasıl tooinstall Python ve hello SDK toouse Azure ile."
services: 
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: f36294be-daeb-4caf-9129-fce18130f552
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 09/06/2016
ms.author: lmazuel
ms.openlocfilehash: c1b394770f9abd3e654a23d79ae179a9af89e2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="installing-python-and-hello-sdk"></a>Python ve hello SDK yükleme
Python kolay tooset açık Windows ve Mac, Linux, önceden yüklenmiş olarak gelir ve [Windows için Bash](https://msdn.microsoft.com/commandline/wsl/about). Bu kılavuzda, yükleme ve makinenizi Azure ile kullanım için hazır hale anlatılmaktadır.

## <a name="whats-in-hello-python-azure-sdk"></a>Ne olduğu, hello Python Azure SDK'sını?
Merhaba Python için Azure SDK toodevelop izin, dağıtmak ve Azure için Python uygulamaları yöneten bileşenleri içerir. Özellikle, Python için Azure SDK hello hello aşağıdakileri içerir:

* **Yönetim kitaplıklarını**. Bu sınıf kitaplıkları depolama hesapları, sanal makineler gibi Azure kaynaklarını yönetme bir arabirim sağlar.
* **Çalışma zamanı kitaplıkları**. Bu sınıf kitaplıkları, depolama ve service bus gibi Azure özellikleri erişmek için bir arabirim sağlar.

## <a name="which-python-and-which-version-toouse"></a>Hangi Python ve hangi sürümü toouse
Python yorumlayıcılar çeşitli özellikleri kullanılabilir - örnekler şunlardır:

* CPython - hello standart ve en yaygın kullanılan Python yorumlayıcı
* PyPy - hızlı, uyumlu alternatif bir uygulama tooCPython
* IronPython - .net/CLR üzerinde çalışan Python yorumlayıcı
* Jython - hello Java sanal makinesi üzerinde çalıştırılan Python yorumlayıcı

**CPython** v2.7 veya v3.3 + ve PyPy 5.4.0 test edilmiş ve Python Azure SDK'sını hello için desteklenir.

## <a name="where-tooget-python"></a>Burada tooget Python?
Çeşitli yolları tooget CPython vardır:

* Doğrudan [www.python.org][www.python.org]
* Tanınmış distro gibi gelen [www.continuum.io][www.continuum.io], [www.enthought.com] [ www.enthought.com] veya [www.activestate.com][www.activestate.com]
* Kaynağından oluşturun!

Belirli bir gereksiniminiz yoksa, ilk iki seçeneği hello öneririz.

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a>Windows, Linux ve MacOS (yalnızca istemci kitaplıkları) SDK yükleme
Yüklü Python zaten varsa, PIP tooinstall bir paketin tüm hello istemci kitaplıklarının varolan Python 2.7 veya Python 3.3 + ortamı kullanabilirsiniz. Bu hello hello paketleri indirir [Python paket dizinini] [ Python Package Index] (Pypı).

Yönetici haklarına ihtiyacınız:

* Linux ve MacOS, kullanın hello `sudo` komutu: `sudo pip install azure-mgmt-compute`.
* Windows: PowerShell/komut istemini yönetici olarak açın.

Her Azure hizmet için ayrı ayrı her kitaplığı yükleyebilirsiniz:

```console
   $ pip install azure-batch          # Install hello latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install hello latest Storage management library
```

Önizleme paketleri hello kullanılarak yüklenebilir `--pre` bayrağı:

```console
   $ pip install --pre azure-mgmt-compute # installs only hello latest Compute Management library
```

Azure kitaplıkları kümesi hello kullanarak tek bir satırda yükleyebilirsiniz `azure` meta paket. Bu meta paketteki tüm paketler henüz kararlı yayımlandığı tarihten sonra hello `azure` meta paketi hala önizlemede değil.
Bununla birlikte, kod kalitesini/bütünlük açılardan hello çekirdek paketleri şu anda "kararlı" kabul edilebilir

* Bu resmi olarak şekilde eşitlenmiş diğer dilleri ile mümkün olan en kısa sürede etiketlenir.
  Biz hakkında daha fazla önemli değişikliklere o zamana kadar planladığınıza değil.

Önizleme sürümü olduğundan, toouse hello gereksinim `--pre` bayrağı:

```console
   $ pip install --pre azure
```

veya doğrudan

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a>Daha fazla paket alma
Merhaba [Python paket dizinini] [ Python Package Index] (Pypı) zengin Python kitaplıkları sahiptir.  Bir Distro tooinstall seçerseniz, web geliştirme tooTechnical çeşitli senaryolarını BITS ilginç hello çoğunu zaten sahip olacaksınız Computing.

## <a name="python-tools-for-visual-studio"></a>Visual Studio için Python Araçları
[Visual Studio için Python Araçları][Visual Studio için Python Araçları] (PTVS) olan bir ücretsiz OSS eklenti VS tam özellikli bir Python IDE içinde kapatır Microsoft:

![How-to-Install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

PTVS kullanarak isteğe bağlıdır, ancak bu, Python ve Web Proje/çözüm desteği, hata ayıklama, profil oluşturma, etkileşimli pencere, şablonu düzenlemek ve IntelliSense sağlar önerilir.

PTVS de kılar dağıtım desteği ile kolay toodeploy tooMicrosoft Azure, çok[bulut Hizmetleri](cloud-services/cloud-services-python-ptvs.md) ve [Web siteleri](app-service-web/web-sites-python-ptvs-django-mysql.md).

PTVS mevcut Visual Studio 2013, 2015 veya 2017 yüklemenizle birlikte çalışır.  Belgeler, indirme ve tartışma için bkz: [Visual Studio için Python Araçları].  

## <a name="python-azure-scenarios-for-linux-and-macos"></a>Python Linux ve MacOS Azure senaryoları
Linux veya MacOS, desteklenen ana Azure senaryoları için:

1. Merhaba istemci kitaplıkları için Python kullanarak Azure Hizmetleri kullanma
2. Bir Linux VM uygulamanızı çalıştırma
3. Geliştirme ve tooAzure Web siteleri yayımlama Git kullanma

Merhaba ilk senaryoda hello Azure PaaS yetenekleri gibi yararlanmak tooauthor zengin web uygulamaları etkinleştirir [blob depolama](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [kuyruk depolama](storage/queues/storage-python-how-to-use-queue-storage.md), [tablo depolama](cosmos-db/table-storage-how-to-use-python.md) vb. hello Azure REST API'lerini için Pythonic sarmalayıcıları aracılığıyla. Bunlar aynı Windows, Mac ve Linux üzerinde çalışır.  Bu istemci kitaplıkları, yerel geliştirme makinenizde veya Azure üzerinde çalışan bir Linux VM de kullanabilirsiniz.

Hello VM senaryosu için yalnızca bir Linux VM tercih ettiğiniz (Ubuntu, CentOS, Suse) Başlat ve Çalıştır/şeyleri yönetin.  Örnek olarak, çalıştırdığınız [IPython] [ IPython] REPL/dizüstü Mac/Windows/Linux makinesindeki ve tarayıcı tooa Linux veya Windows birden çok işlemci VM çalıştırılması hello Azure IPython altyapısında noktası.

Hakkında bilgi için bir Linux VM yukarı tooset bkz hello [çalıştıran bir sanal makine Linux oluşturmak](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Öğreticisi.

Git dağıtımı kullanarak bir Python web uygulaması geliştirme ve herhangi bir işletim sisteminden tooan Azure Web sitesi yayımlama.  Depo tooAzure bastığınızda, bir sanal ortam otomatik olarak oluşturur ve gerekli paketleri pip yükler.

Merhaba öğreticileri için geliştirme ve Azure Web siteleri yayımlama hakkında daha fazla bilgi için bkz: [Django ile Web siteleri oluşturma](app-service-web/web-sites-python-create-deploy-django-app.md), [Bottle ile Web siteleri oluşturma](app-service-web/web-sites-python-create-deploy-bottle-app.md), ve [ile Web siteleri oluşturma Flask](app-service-web/web-sites-python-create-deploy-flask-app.md). Tüm WSGI uyumlu framework kullanma hakkında daha fazla genel bilgi için bkz: [yapılandırma Python Azure Web siteleri ile](app-service-web/web-sites-python-configure.md).

## <a name="additional-software-and-resources"></a>Ek yazılım ve kaynaklar:
* [Python ReadTheDocs için Azure SDK'sı](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [Python GitHub için Azure SDK'sı](https://github.com/Azure/azure-sdk-for-python)
* [Python için resmi Azure örnekleri](https://azure.microsoft.com/documentation/samples/?platform=python)
* [Continuum Analytics Python dağıtımı][Continuum Analytics Python Distribution]
* [Enthought Python dağıtımı][Enthought Python Distribution]
* [ActiveState Python dağıtımı][ActiveState Python Distribution]
* [SciPy - suite bilimsel Python kitaplığı][SciPy - A suite of Scientific Python libraries]
* [NumPy - Python için bir sayı kitaplığı][NumPy - A numerics library for Python]
* [Django proje - bir yetişkin web framework/CMS][Django Project - A mature web framework/CMS]
* [IPython - Python için Gelişmiş bir REPL/dizüstü][IPython - an advanced REPL/Notebook for Python]
* [Github'da Visual Studio için Python araçları][Python Tools for Visual Studio on GitHub]
* [Python Geliştirici Merkezi](/develop/python/)

[Continuum Analytics Python Distribution]: http://continuum.io
[Enthought Python Distribution]: http://www.enthought.com
[ActiveState Python Distribution]: http://www.activestate.com
[www.python.org]: http://www.python.org
[www.continuum.io]: http://continuum.io
[www.enthought.com]: http://www.enthought.com
[www.activestate.com]: http://www.activestate.com
[SciPy - A suite of Scientific Python libraries]: http://www.scipy.org
[NumPy - A numerics library for Python]: http://www.numpy.org
[Django Project - A mature web framework/CMS]: http://www.djangoproject.com
[IPython - an advanced REPL/Notebook for Python]: http://ipython.org
[IPython]: http://ipython.org
[IPython Notebook on Azure]: virtual-machines-linux-jupyter-notebook.md
[Cloud Services]: cloud-services-python-ptvs.md
[Websites]: web-sites-python-ptvs-django-mysql.md
[Visual Studio için Python Araçları]: http://aka.ms/ptvs
[Python Tools for Visual Studio on GitHub]: https://github.com/microsoft/ptvs
[Python Package Index]: http://pypi.python.org/pypi
[Microsoft Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?LinkId=254281
[Microsoft Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?LinkID=516990
[Setting up a Linux VM via hello Azure portal]: create-and-configure-opensuse-vm-in-portal.md
[How toouse hello Azure Command-Line Interface]: crossplat-cmd-tools.md
[Create a Virtual Machine Running Linux]: virtual-machines-linux-quick-create-cli.md
[Creating Websites with Django]: web-sites-python-create-deploy-django-app.md
[Creating Websites with Bottle]: web-sites-python-create-deploy-bottle-app.md
[Creating Websites with Flask]: web-sites-python-create-deploy-flask-app.md
[Configuring Python with Azure Websites]: web-sites-python-configure.md
[table storage]: storage-python-how-to-use-table-storage.md
[queue storage]: storage-python-how-to-use-queue-storage.md
[blob storage]:storage/blobs/storage-python-how-to-use-blob-storage.md
