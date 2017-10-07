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
# <a name="installing-python-and-hello-sdk"></a><span data-ttu-id="b2ed9-103">Python ve hello SDK yükleme</span><span class="sxs-lookup"><span data-stu-id="b2ed9-103">Installing Python and hello SDK</span></span>
<span data-ttu-id="b2ed9-104">Python kolay tooset açık Windows ve Mac, Linux, önceden yüklenmiş olarak gelir ve [Windows için Bash](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="b2ed9-104">Python is easy tooset up on Windows and comes pre-installed on Mac, Linux, and [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="b2ed9-105">Bu kılavuzda, yükleme ve makinenizi Azure ile kullanım için hazır hale anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-105">This guide walks you through installation and getting your machine ready for use with Azure.</span></span>

## <a name="whats-in-hello-python-azure-sdk"></a><span data-ttu-id="b2ed9-106">Ne olduğu, hello Python Azure SDK'sını?</span><span class="sxs-lookup"><span data-stu-id="b2ed9-106">What's in hello Python Azure SDK?</span></span>
<span data-ttu-id="b2ed9-107">Merhaba Python için Azure SDK toodevelop izin, dağıtmak ve Azure için Python uygulamaları yöneten bileşenleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-107">hello Azure SDK for Python includes components that allow you toodevelop, deploy, and manage Python applications for Azure.</span></span> <span data-ttu-id="b2ed9-108">Özellikle, Python için Azure SDK hello hello aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="b2ed9-108">Specifically, hello Azure SDK for Python includes hello following:</span></span>

* <span data-ttu-id="b2ed9-109">**Yönetim kitaplıklarını**.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-109">**Management libraries**.</span></span> <span data-ttu-id="b2ed9-110">Bu sınıf kitaplıkları depolama hesapları, sanal makineler gibi Azure kaynaklarını yönetme bir arabirim sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-110">These class libraries provide an interface managing Azure resources, such as storage accounts, virtual machines.</span></span>
* <span data-ttu-id="b2ed9-111">**Çalışma zamanı kitaplıkları**.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-111">**Runtime libraries**.</span></span> <span data-ttu-id="b2ed9-112">Bu sınıf kitaplıkları, depolama ve service bus gibi Azure özellikleri erişmek için bir arabirim sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-112">These class libraries provide an interface for accessing Azure features, such as storage and service bus.</span></span>

## <a name="which-python-and-which-version-toouse"></a><span data-ttu-id="b2ed9-113">Hangi Python ve hangi sürümü toouse</span><span class="sxs-lookup"><span data-stu-id="b2ed9-113">Which Python and which version toouse</span></span>
<span data-ttu-id="b2ed9-114">Python yorumlayıcılar çeşitli özellikleri kullanılabilir - örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b2ed9-114">There are several flavors of Python interpreters available - examples include:</span></span>

* <span data-ttu-id="b2ed9-115">CPython - hello standart ve en yaygın kullanılan Python yorumlayıcı</span><span class="sxs-lookup"><span data-stu-id="b2ed9-115">CPython - hello standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="b2ed9-116">PyPy - hızlı, uyumlu alternatif bir uygulama tooCPython</span><span class="sxs-lookup"><span data-stu-id="b2ed9-116">PyPy - fast, compliant alternative implementation tooCPython</span></span>
* <span data-ttu-id="b2ed9-117">IronPython - .net/CLR üzerinde çalışan Python yorumlayıcı</span><span class="sxs-lookup"><span data-stu-id="b2ed9-117">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="b2ed9-118">Jython - hello Java sanal makinesi üzerinde çalıştırılan Python yorumlayıcı</span><span class="sxs-lookup"><span data-stu-id="b2ed9-118">Jython - Python interpreter that runs on hello Java Virtual Machine</span></span>

<span data-ttu-id="b2ed9-119">**CPython** v2.7 veya v3.3 + ve PyPy 5.4.0 test edilmiş ve Python Azure SDK'sını hello için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-119">**CPython** v2.7 or v3.3+ and PyPy 5.4.0 are tested and supported for hello Python Azure SDK.</span></span>

## <a name="where-tooget-python"></a><span data-ttu-id="b2ed9-120">Burada tooget Python?</span><span class="sxs-lookup"><span data-stu-id="b2ed9-120">Where tooget Python?</span></span>
<span data-ttu-id="b2ed9-121">Çeşitli yolları tooget CPython vardır:</span><span class="sxs-lookup"><span data-stu-id="b2ed9-121">There are several ways tooget CPython:</span></span>

* <span data-ttu-id="b2ed9-122">Doğrudan [www.python.org][www.python.org]</span><span class="sxs-lookup"><span data-stu-id="b2ed9-122">Directly from [www.python.org][www.python.org]</span></span>
* <span data-ttu-id="b2ed9-123">Tanınmış distro gibi gelen [www.continuum.io][www.continuum.io], [www.enthought.com] [ www.enthought.com] veya [www.activestate.com][www.activestate.com]</span><span class="sxs-lookup"><span data-stu-id="b2ed9-123">From a reputable distro such as [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] or [www.activestate.com][www.activestate.com]</span></span>
* <span data-ttu-id="b2ed9-124">Kaynağından oluşturun!</span><span class="sxs-lookup"><span data-stu-id="b2ed9-124">Build from source!</span></span>

<span data-ttu-id="b2ed9-125">Belirli bir gereksiniminiz yoksa, ilk iki seçeneği hello öneririz.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-125">Unless you have a specific need, we recommend hello first two options.</span></span>

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a><span data-ttu-id="b2ed9-126">Windows, Linux ve MacOS (yalnızca istemci kitaplıkları) SDK yükleme</span><span class="sxs-lookup"><span data-stu-id="b2ed9-126">SDK Installation on Windows, Linux, and MacOS (client libraries only)</span></span>
<span data-ttu-id="b2ed9-127">Yüklü Python zaten varsa, PIP tooinstall bir paketin tüm hello istemci kitaplıklarının varolan Python 2.7 veya Python 3.3 + ortamı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-127">If you already have Python installed, you can use pip tooinstall a bundle of all hello client libraries in your existing Python 2.7 or Python 3.3+ environment.</span></span> <span data-ttu-id="b2ed9-128">Bu hello hello paketleri indirir [Python paket dizinini] [ Python Package Index] (Pypı).</span><span class="sxs-lookup"><span data-stu-id="b2ed9-128">This downloads hello packages from hello [Python Package Index][Python Package Index] (PyPI).</span></span>

<span data-ttu-id="b2ed9-129">Yönetici haklarına ihtiyacınız:</span><span class="sxs-lookup"><span data-stu-id="b2ed9-129">You may need administrator rights:</span></span>

* <span data-ttu-id="b2ed9-130">Linux ve MacOS, kullanın hello `sudo` komutu: `sudo pip install azure-mgmt-compute`.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-130">Linux and MacOS, use hello `sudo` command: `sudo pip install azure-mgmt-compute`.</span></span>
* <span data-ttu-id="b2ed9-131">Windows: PowerShell/komut istemini yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-131">Windows: open your PowerShell/Command prompt as an administrator</span></span>

<span data-ttu-id="b2ed9-132">Her Azure hizmet için ayrı ayrı her kitaplığı yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b2ed9-132">You can install individually each library for each Azure service:</span></span>

```console
   $ pip install azure-batch          # Install hello latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install hello latest Storage management library
```

<span data-ttu-id="b2ed9-133">Önizleme paketleri hello kullanılarak yüklenebilir `--pre` bayrağı:</span><span class="sxs-lookup"><span data-stu-id="b2ed9-133">Preview packages can be installed using hello `--pre` flag:</span></span>

```console
   $ pip install --pre azure-mgmt-compute # installs only hello latest Compute Management library
```

<span data-ttu-id="b2ed9-134">Azure kitaplıkları kümesi hello kullanarak tek bir satırda yükleyebilirsiniz `azure` meta paket.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-134">You can also install a set of Azure libraries in a single line using hello `azure` meta-package.</span></span> <span data-ttu-id="b2ed9-135">Bu meta paketteki tüm paketler henüz kararlı yayımlandığı tarihten sonra hello `azure` meta paketi hala önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-135">Since not all packages in this meta-package are published as stable yet, hello `azure` meta-package is still in preview.</span></span>
<span data-ttu-id="b2ed9-136">Bununla birlikte, kod kalitesini/bütünlük açılardan hello çekirdek paketleri şu anda "kararlı" kabul edilebilir</span><span class="sxs-lookup"><span data-stu-id="b2ed9-136">However, hello core packages, from code quality/completeness perspectives can be considered "stable" at this time</span></span>

* <span data-ttu-id="b2ed9-137">Bu resmi olarak şekilde eşitlenmiş diğer dilleri ile mümkün olan en kısa sürede etiketlenir.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-137">it is officially labeled as such in sync with other languages as soon as possible.</span></span>
  <span data-ttu-id="b2ed9-138">Biz hakkında daha fazla önemli değişikliklere o zamana kadar planladığınıza değil.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-138">We are not planning on any further major changes until then.</span></span>

<span data-ttu-id="b2ed9-139">Önizleme sürümü olduğundan, toouse hello gereksinim `--pre` bayrağı:</span><span class="sxs-lookup"><span data-stu-id="b2ed9-139">Since it's a preview release, you need toouse hello `--pre` flag:</span></span>

```console
   $ pip install --pre azure
```

<span data-ttu-id="b2ed9-140">veya doğrudan</span><span class="sxs-lookup"><span data-stu-id="b2ed9-140">or directly</span></span>

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a><span data-ttu-id="b2ed9-141">Daha fazla paket alma</span><span class="sxs-lookup"><span data-stu-id="b2ed9-141">Getting More Packages</span></span>
<span data-ttu-id="b2ed9-142">Merhaba [Python paket dizinini] [ Python Package Index] (Pypı) zengin Python kitaplıkları sahiptir.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-142">hello [Python Package Index][Python Package Index] (PyPI) has a rich selection of Python libraries.</span></span>  <span data-ttu-id="b2ed9-143">Bir Distro tooinstall seçerseniz, web geliştirme tooTechnical çeşitli senaryolarını BITS ilginç hello çoğunu zaten sahip olacaksınız Computing.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-143">If you chose tooinstall a Distro, you'll already have most of hello interesting bits for various scenarios from web development tooTechnical Computing.</span></span>

## <a name="python-tools-for-visual-studio"></a><span data-ttu-id="b2ed9-144">Visual Studio için Python Araçları</span><span class="sxs-lookup"><span data-stu-id="b2ed9-144">Python Tools for Visual Studio</span></span>
<span data-ttu-id="b2ed9-145">[Visual Studio için Python Araçları][Visual Studio için Python Araçları] (PTVS) olan bir ücretsiz OSS eklenti VS tam özellikli bir Python IDE içinde kapatır Microsoft:</span><span class="sxs-lookup"><span data-stu-id="b2ed9-145">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) is a free/OSS plugin from Microsoft, which turns VS into a full-fledged Python IDE:</span></span>

![How-to-Install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

<span data-ttu-id="b2ed9-147">PTVS kullanarak isteğe bağlıdır, ancak bu, Python ve Web Proje/çözüm desteği, hata ayıklama, profil oluşturma, etkileşimli pencere, şablonu düzenlemek ve IntelliSense sağlar önerilir.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-147">Using PTVS is optional, but is recommended as it gives you Python and Web Project/Solution support, debugging, profiling, interactive window, Template editing, and Intellisense.</span></span>

<span data-ttu-id="b2ed9-148">PTVS de kılar dağıtım desteği ile kolay toodeploy tooMicrosoft Azure, çok[bulut Hizmetleri](cloud-services/cloud-services-python-ptvs.md) ve [Web siteleri](app-service-web/web-sites-python-ptvs-django-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="b2ed9-148">PTVS also makes it easy toodeploy tooMicrosoft Azure, with support for deployment too[Cloud Services](cloud-services/cloud-services-python-ptvs.md) and [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span></span>

<span data-ttu-id="b2ed9-149">PTVS mevcut Visual Studio 2013, 2015 veya 2017 yüklemenizle birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-149">PTVS works with your existing Visual Studio 2013, 2015, or 2017 installation.</span></span>  <span data-ttu-id="b2ed9-150">Belgeler, indirme ve tartışma için bkz: [Visual Studio için Python Araçları].</span><span class="sxs-lookup"><span data-stu-id="b2ed9-150">For documentation, downloads and discussions, see [Python Tools for Visual Studio].</span></span>  

## <a name="python-azure-scenarios-for-linux-and-macos"></a><span data-ttu-id="b2ed9-151">Python Linux ve MacOS Azure senaryoları</span><span class="sxs-lookup"><span data-stu-id="b2ed9-151">Python Azure Scenarios for Linux and MacOS</span></span>
<span data-ttu-id="b2ed9-152">Linux veya MacOS, desteklenen ana Azure senaryoları için:</span><span class="sxs-lookup"><span data-stu-id="b2ed9-152">For Linux or MacOS, main Azure scenarios that are supported:</span></span>

1. <span data-ttu-id="b2ed9-153">Merhaba istemci kitaplıkları için Python kullanarak Azure Hizmetleri kullanma</span><span class="sxs-lookup"><span data-stu-id="b2ed9-153">Consuming Azure Services by using hello client libraries for Python</span></span>
2. <span data-ttu-id="b2ed9-154">Bir Linux VM uygulamanızı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b2ed9-154">Running your app in a Linux VM</span></span>
3. <span data-ttu-id="b2ed9-155">Geliştirme ve tooAzure Web siteleri yayımlama Git kullanma</span><span class="sxs-lookup"><span data-stu-id="b2ed9-155">Developing and publishing tooAzure Websites using Git</span></span>

<span data-ttu-id="b2ed9-156">Merhaba ilk senaryoda hello Azure PaaS yetenekleri gibi yararlanmak tooauthor zengin web uygulamaları etkinleştirir [blob depolama](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [kuyruk depolama](storage/queues/storage-python-how-to-use-queue-storage.md), [tablo depolama](cosmos-db/table-storage-how-to-use-python.md) vb. hello Azure REST API'lerini için Pythonic sarmalayıcıları aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-156">hello first scenario enables you tooauthor rich web apps that take advantage of hello Azure PaaS capabilities such as [blob storage](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [queue storage](storage/queues/storage-python-how-to-use-queue-storage.md), [table storage](cosmos-db/table-storage-how-to-use-python.md) etc. via Pythonic wrappers for hello Azure REST APIs.</span></span> <span data-ttu-id="b2ed9-157">Bunlar aynı Windows, Mac ve Linux üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-157">These work identically on Windows, Mac, and Linux.</span></span>  <span data-ttu-id="b2ed9-158">Bu istemci kitaplıkları, yerel geliştirme makinenizde veya Azure üzerinde çalışan bir Linux VM de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-158">You can also use these client libraries from your local development machine or a Linux VM running on Azure.</span></span>

<span data-ttu-id="b2ed9-159">Hello VM senaryosu için yalnızca bir Linux VM tercih ettiğiniz (Ubuntu, CentOS, Suse) Başlat ve Çalıştır/şeyleri yönetin.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-159">For hello VM scenario, you simply start a Linux VM of your choice (Ubuntu, CentOS, Suse) and run/manage what you like.</span></span>  <span data-ttu-id="b2ed9-160">Örnek olarak, çalıştırdığınız [IPython] [ IPython] REPL/dizüstü Mac/Windows/Linux makinesindeki ve tarayıcı tooa Linux veya Windows birden çok işlemci VM çalıştırılması hello Azure IPython altyapısında noktası.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-160">As an example, you can run [IPython][IPython] REPL/notebook on your Windows/Mac/Linux machine and point your browser tooa Linux or Windows multi-proc VM running hello IPython Engine on Azure.</span></span>

<span data-ttu-id="b2ed9-161">Hakkında bilgi için bir Linux VM yukarı tooset bkz hello [çalıştıran bir sanal makine Linux oluşturmak](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-161">For information on how tooset up a Linux VM, see hello [Create a Virtual Machine Running Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span></span>

<span data-ttu-id="b2ed9-162">Git dağıtımı kullanarak bir Python web uygulaması geliştirme ve herhangi bir işletim sisteminden tooan Azure Web sitesi yayımlama.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-162">Using Git deployment, you can develop a Python web application and publish it tooan Azure Website from any operating system.</span></span>  <span data-ttu-id="b2ed9-163">Depo tooAzure bastığınızda, bir sanal ortam otomatik olarak oluşturur ve gerekli paketleri pip yükler.</span><span class="sxs-lookup"><span data-stu-id="b2ed9-163">When you push your repository tooAzure, it automatically creates a virtual environment and pip installs your required packages.</span></span>

<span data-ttu-id="b2ed9-164">Merhaba öğreticileri için geliştirme ve Azure Web siteleri yayımlama hakkında daha fazla bilgi için bkz: [Django ile Web siteleri oluşturma](app-service-web/web-sites-python-create-deploy-django-app.md), [Bottle ile Web siteleri oluşturma](app-service-web/web-sites-python-create-deploy-bottle-app.md), ve [ile Web siteleri oluşturma Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span><span class="sxs-lookup"><span data-stu-id="b2ed9-164">For more information on developing and publishing Azure Websites, see hello tutorials for [Creating Websites with Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Creating Websites with Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), and [Creating Websites with Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span></span> <span data-ttu-id="b2ed9-165">Tüm WSGI uyumlu framework kullanma hakkında daha fazla genel bilgi için bkz: [yapılandırma Python Azure Web siteleri ile](app-service-web/web-sites-python-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b2ed9-165">For more general information on using any WSGI-compliant framework, see [Configuring Python with Azure Websites](app-service-web/web-sites-python-configure.md).</span></span>

## <a name="additional-software-and-resources"></a><span data-ttu-id="b2ed9-166">Ek yazılım ve kaynaklar:</span><span class="sxs-lookup"><span data-stu-id="b2ed9-166">Additional Software and Resources:</span></span>
* [<span data-ttu-id="b2ed9-167">Python ReadTheDocs için Azure SDK'sı</span><span class="sxs-lookup"><span data-stu-id="b2ed9-167">Azure SDK for Python ReadTheDocs</span></span>](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [<span data-ttu-id="b2ed9-168">Python GitHub için Azure SDK'sı</span><span class="sxs-lookup"><span data-stu-id="b2ed9-168">Azure SDK for Python GitHub</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="b2ed9-169">Python için resmi Azure örnekleri</span><span class="sxs-lookup"><span data-stu-id="b2ed9-169">Official Azure samples for Python</span></span>](https://azure.microsoft.com/documentation/samples/?platform=python)
* <span data-ttu-id="b2ed9-170">[Continuum Analytics Python dağıtımı][Continuum Analytics Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="b2ed9-170">[Continuum Analytics Python Distribution][Continuum Analytics Python Distribution]</span></span>
* <span data-ttu-id="b2ed9-171">[Enthought Python dağıtımı][Enthought Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="b2ed9-171">[Enthought Python Distribution][Enthought Python Distribution]</span></span>
* <span data-ttu-id="b2ed9-172">[ActiveState Python dağıtımı][ActiveState Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="b2ed9-172">[ActiveState Python Distribution][ActiveState Python Distribution]</span></span>
* <span data-ttu-id="b2ed9-173">[SciPy - suite bilimsel Python kitaplığı][SciPy - A suite of Scientific Python libraries]</span><span class="sxs-lookup"><span data-stu-id="b2ed9-173">[SciPy - A suite of Scientific Python libraries][SciPy - A suite of Scientific Python libraries]</span></span>
* <span data-ttu-id="b2ed9-174">[NumPy - Python için bir sayı kitaplığı][NumPy - A numerics library for Python]</span><span class="sxs-lookup"><span data-stu-id="b2ed9-174">[NumPy - A numerics library for Python][NumPy - A numerics library for Python]</span></span>
* <span data-ttu-id="b2ed9-175">[Django proje - bir yetişkin web framework/CMS][Django Project - A mature web framework/CMS]</span><span class="sxs-lookup"><span data-stu-id="b2ed9-175">[Django Project - A mature web framework/CMS][Django Project - A mature web framework/CMS]</span></span>
* <span data-ttu-id="b2ed9-176">[IPython - Python için Gelişmiş bir REPL/dizüstü][IPython - an advanced REPL/Notebook for Python]</span><span class="sxs-lookup"><span data-stu-id="b2ed9-176">[IPython - an advanced REPL/Notebook for Python][IPython - an advanced REPL/Notebook for Python]</span></span>
* <span data-ttu-id="b2ed9-177">[Github'da Visual Studio için Python araçları][Python Tools for Visual Studio on GitHub]</span><span class="sxs-lookup"><span data-stu-id="b2ed9-177">[Python Tools for Visual Studio on GitHub][Python Tools for Visual Studio on GitHub]</span></span>
* [<span data-ttu-id="b2ed9-178">Python Geliştirici Merkezi</span><span class="sxs-lookup"><span data-stu-id="b2ed9-178">Python Developer Center</span></span>](/develop/python/)

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
