---
title: "azure'da Django ile aaaCreating web uygulamaları"
description: "Toorunning bir Python web uygulamasını Azure App Service Web Apps tanıtır Öğreticisi."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 9be1a05a-9460-49ae-94fb-9798f82c11cf
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 26a131da358748bd6fe4ee5c114d0a8f91b83cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a><span data-ttu-id="f8b4f-103">Azure’da Django ile web uygulamaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8b4f-103">Creating web apps with Django in Azure</span></span>
<span data-ttu-id="f8b4f-104">Bu öğretici tooget te Python çalıştırmaya nasıl başlatılacağını açıklar [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="f8b4f-104">This tutorial describes how tooget started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="f8b4f-105">Web Apps sınırlı ücretsiz barındırma ve hızlı dağıtım sağlar ve Python’u kullanmanıza olanak tanır!</span><span class="sxs-lookup"><span data-stu-id="f8b4f-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="f8b4f-106">Uygulamanız büyüdükçe, toopaid barındırma geçiş yapabilirsiniz ve tüm ile de tümleştirebilir gibi diğer Azure hizmetleriyle hello.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="f8b4f-107">Merhaba Django web altyapısını kullanarak bir uygulama oluşturacaksınız (Bu öğretici için alternatif sürümleri bkz [Flask](web-sites-python-create-deploy-flask-app.md) ve [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="f8b4f-107">You will create an application using hello Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span> <span data-ttu-id="f8b4f-108">Azure Market hello hello web uygulaması oluşturma, Git dağıtımı ayarlayacak ve hello depoyu yerel olarak kopyalayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-108">You will create hello web app from hello Azure Marketplace, set up Git deployment, and clone hello repository locally.</span></span> <span data-ttu-id="f8b4f-109">Ardından, hello uygulamayı yerel olarak çalıştırmak, değişiklik, yürütme ve bunları tooAzure gönderme.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-109">Then you will run hello application locally, make changes, commit and push them tooAzure.</span></span> <span data-ttu-id="f8b4f-110">Eğitmen gösterir nasıl hello toodo bu Windows veya Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="f8b4f-111">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f8b4f-112">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f8b4f-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f8b4f-113">Prerequisites</span></span>
* <span data-ttu-id="f8b4f-114">Windows, Mac veya Linux</span><span class="sxs-lookup"><span data-stu-id="f8b4f-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="f8b4f-115">Python 2.7 ya da 3.4</span><span class="sxs-lookup"><span data-stu-id="f8b4f-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="f8b4f-116">setuptools, pip, virtualenv (yalnızca Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="f8b4f-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="f8b4f-117">Git</span><span class="sxs-lookup"><span data-stu-id="f8b4f-117">Git</span></span>
* <span data-ttu-id="f8b4f-118">[Visual Studio için Python Araçları][Visual Studio için Python Araçları] (PTVS) - Not: Bu özellik isteğe bağlıdır</span><span class="sxs-lookup"><span data-stu-id="f8b4f-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="f8b4f-119">**Not**: TFS yayımlama şu anda Python projeleri için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="f8b4f-120">Windows</span><span class="sxs-lookup"><span data-stu-id="f8b4f-120">Windows</span></span>
<span data-ttu-id="f8b4f-121">Python 2.7 ya da 3.4 yüklü (32 bit) değilse, Web Platformu Yükleyicisi'ni kullanarak [Python 2.7 için Azure SDK] veya [Python 3.4 için Azure SDK]’yı yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="f8b4f-122">Bu, Python, setuptools, PIP, virtualenv, (32 bit Python hello Azure ana makinelerde yüklü olandır) "Merhaba 32-bit sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span> <span data-ttu-id="f8b4f-123">Alternatif olarak, Python’u [python.org] adresinden edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="f8b4f-124">Git için, [Windows için Git] veya [Windows için GitHub]’ı öneririz.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="f8b4f-125">Visual Studio kullanıyorsanız hello tümleşik Git desteğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="f8b4f-126">Ayrıca [Visual Studio için Python Araçları 2.2]’yi yüklemenizi öneririz </span><span class="sxs-lookup"><span data-stu-id="f8b4f-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="f8b4f-127">Bu isteğe bağlı, ancak varsa [Visual Studio]hello dahil olmak üzere ücretsiz Visual Studio Community 2013 veya Visual Studio Express 2013 Web sonra bu mükemmel bir Python IDE verir.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="f8b4f-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="f8b4f-128">Mac/Linux</span></span>
<span data-ttu-id="f8b4f-129">Python ve Git sizde zaten yüklü olmalıdır, ancak Python 2.7 veya 3.4 olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-portal"></a><span data-ttu-id="f8b4f-130">Portalda Web Uygulaması Oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8b4f-130">Web App Creation on Portal</span></span>
<span data-ttu-id="f8b4f-131">Merhaba uygulamanızı oluşturmanın ilk adımı olan toocreate hello web uygulaması hello aracılığıyla [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f8b4f-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="f8b4f-132">Oturum hello Azure Portal ve hello tıklatın **yeni** hello sol alt köşedeki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span>
2. <span data-ttu-id="f8b4f-133">Merhaba arama kutusuna "python" yazın.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-133">In hello search box, type "python".</span></span>
3. <span data-ttu-id="f8b4f-134">Merhaba arama sonuçlarında seçin **Django** (PTVS tarafından yayımlanan), ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-134">In hello search results, select **Django** (published by PTVS), then click **Create**.</span></span>
4. <span data-ttu-id="f8b4f-135">Yeni bir uygulama hizmeti planı ve yeni bir kaynak grubu oluşturma gibi hello yeni Django uygulamasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-135">Configure hello new Django app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="f8b4f-136">Sonra, **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="f8b4f-137">Merhaba yönergeleri izleyerek Git yayımlamayı yeni oluşturulan web uygulamanız için yapılandırma [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f8b4f-137">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="f8b4f-138">Uygulamaya Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f8b4f-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="f8b4f-139">Git deposu içeriği</span><span class="sxs-lookup"><span data-stu-id="f8b4f-139">Git repository contents</span></span>
<span data-ttu-id="f8b4f-140">Burada, hangi hello sonraki bölümde kopyalama hello ilk Git deposunda bulabilirsiniz hello dosyaları genel bir bakış verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-140">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \app\__init__.py
    \app\forms.py
    \app\models.py
    \app\tests.py
    \app\views.py
    \app\static\content\
    \app\static\fonts\
    \app\static\scripts\
    \app\templates\about.html
    \app\templates\contact.html
    \app\templates\index.html
    \app\templates\layout.html
    \app\templates\login.html
    \app\templates\loginpartial.html
    \DjangoWebProject\__init__.py
    \DjangoWebProject\settings.py
    \DjangoWebProject\urls.py
    \DjangoWebProject\wsgi.py

<span data-ttu-id="f8b4f-141">Merhaba uygulaması için ana kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-141">Main sources for hello application.</span></span> <span data-ttu-id="f8b4f-142">Ana düzenle birlikte 3 sayfadan (dizin, hakkında, iletişim) oluşur.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span> <span data-ttu-id="f8b4f-143">Statik içerik ve betikler bootstrap, jquery, modernize ve yanıtı içerir.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \manage.py

<span data-ttu-id="f8b4f-144">Yerel yönetim ve geliştirme sunucusu desteği.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-144">Local management and development server support.</span></span> <span data-ttu-id="f8b4f-145">Eşitleme hello veritabanı, vb., bu toorun hello uygulama yerel olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-145">Use this toorun hello application locally, synchronize hello database, etc.</span></span>

    \db.sqlite3

<span data-ttu-id="f8b4f-146">Varsayılan veritabanı.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-146">Default database.</span></span> <span data-ttu-id="f8b4f-147">Merhaba uygulama toorun Hello gerekli tabloları içerir, ancak (Merhaba veritabanı toocreate kullanıcı eşitleme) herhangi bir kullanıcı içermez.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-147">Includes hello necessary tables for hello application toorun, but does not contain any users (synchronize hello database toocreate a user).</span></span>

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

<span data-ttu-id="f8b4f-148">[Visual Studio için Python Araçları] ile birlikte kullanmak için proje dosyaları.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-148">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="f8b4f-149">Sanal ortamlar için IIS proxy ve PTVS uzaktan hata ayıklama desteği</span><span class="sxs-lookup"><span data-stu-id="f8b4f-149">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="f8b4f-150">Bu uygulamaya dış paketler gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-150">External packages needed by this application.</span></span> <span data-ttu-id="f8b4f-151">Bu dosyada listelenen yükleme hello paketleri Hello dağıtım betiği pip.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-151">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="f8b4f-152">IIS yapılandırma dosyaları.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-152">IIS configuration files.</span></span> <span data-ttu-id="f8b4f-153">Merhaba dağıtım betiği hello uygun Web.x.y.config'i kullanır ve bunu web.config olarak kopyalar.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-153">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="f8b4f-154">İsteğe bağlı dosyalar - Dağıtımı özelleştirme</span><span class="sxs-lookup"><span data-stu-id="f8b4f-154">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="f8b4f-155">İsteğe bağlı dosyalar - Python çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="f8b4f-155">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="f8b4f-156">Sunucu üzerindeki ek dosyalar</span><span class="sxs-lookup"><span data-stu-id="f8b4f-156">Additional files on server</span></span>
<span data-ttu-id="f8b4f-157">Bazı dosyalar hello sunucuda var, ancak toohello git deposuna eklenmez.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-157">Some files exist on hello server but are not added toohello git repository.</span></span> <span data-ttu-id="f8b4f-158">Bunlar hello dağıtım betiği tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-158">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="f8b4f-159">IIS yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-159">IIS configuration file.</span></span> <span data-ttu-id="f8b4f-160">Her dağıtımda web.x.y.config tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-160">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="f8b4f-161">Python sanal ortamı.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-161">Python virtual environment.</span></span> <span data-ttu-id="f8b4f-162">Dağıtım sırasında hello web uygulamasında uyumlu sanal ortamın zaten mevcut değilse oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-162">Created during deployment if a compatible virtual environment doesn't already exist on hello web app.</span></span> <span data-ttu-id="f8b4f-163">Requirements.txt içinde listelenen paketler pip yüklüdür, ancak hello paketler zaten yüklü ise pip yüklemeyi atlar.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="f8b4f-164">Merhaba sonraki 3 bölümde nasıl tooproceed hello ile web uygulaması geliştirme altında farklı 3 ortamda açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-164">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="f8b4f-165">Windows, Visual Studio için Python Araçları ile</span><span class="sxs-lookup"><span data-stu-id="f8b4f-165">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="f8b4f-166">Windows, komut satırı ile</span><span class="sxs-lookup"><span data-stu-id="f8b4f-166">Windows, with command line</span></span>
* <span data-ttu-id="f8b4f-167">Mac/Linux, komut satırı ile</span><span class="sxs-lookup"><span data-stu-id="f8b4f-167">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="f8b4f-168">Web uygulaması geliştirme - Windows - Visual Studio için Python Araçları</span><span class="sxs-lookup"><span data-stu-id="f8b4f-168">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="f8b4f-169">Kopya hello deposu</span><span class="sxs-lookup"><span data-stu-id="f8b4f-169">Clone hello repository</span></span>
<span data-ttu-id="f8b4f-170">İlk olarak, Azure Portal hello üzerinde sağlanan hello URL'yi kullanarak hello depoyu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-170">First, clone hello repository using hello URL provided on hello Azure Portal.</span></span> <span data-ttu-id="f8b4f-171">Daha fazla bilgi için bkz: [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f8b4f-171">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="f8b4f-172">Merhaba hello depo kök dizininde bulunan hello çözüm dosyasını (.sln) açın.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-172">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="f8b4f-173">Sanal ortamı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-173">Create virtual environment</span></span>
<span data-ttu-id="f8b4f-174">Şimdi, yerel geliştirme için sanal bir ortam oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-174">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="f8b4f-175">Sağ **Python Ortamları**’na sağ tıklayın **Sanal Ortam Ekle...** seçeneğini seçin.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="f8b4f-176">Merhaba ortamı Hello adı olduğundan emin olun `env`.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-176">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="f8b4f-177">Merhaba temel yorumlayıcıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-177">Select hello base interpreter.</span></span> <span data-ttu-id="f8b4f-178">Toouse hello web uygulamanız için seçilen Python ile aynı sürümü olduğundan emin olun (runtime.txt veya hello **uygulama ayarları** hello Azure Portal, web uygulamanızın dikey penceresinde).</span><span class="sxs-lookup"><span data-stu-id="f8b4f-178">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="f8b4f-179">Merhaba seçeneği toodownload ve yükleme paketleri işaretli olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-179">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="f8b4f-180">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-180">Click **Create**.</span></span> <span data-ttu-id="f8b4f-181">Bu işlem hello sanal ortam oluşturacak ve requirements.txt içinde listelenen bağımlılıkları yükler.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-181">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="create-a-superuser"></a><span data-ttu-id="f8b4f-182">Süper kullanıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8b4f-182">Create a superuser</span></span>
<span data-ttu-id="f8b4f-183">Merhaba uygulamayla birlikte gelen hello veritabanında tanımlı bir süper kullanıcı yok.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-183">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="f8b4f-184">Oturum açma sırası toouse hello işlev hello uygulama ya da hello Django yönetim arabirimi (tooenable karar verirseniz,), bir süper kullanıcı toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-184">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="f8b4f-185">Bu hello komut satırı, proje klasöründen çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-185">Run this from hello command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="f8b4f-186">Merhaba istemleri tooset hello kullanıcı adı, parola vb. izleyin.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-186">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="f8b4f-187">Geliştirme sunucusu kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="f8b4f-187">Run using development server</span></span>
<span data-ttu-id="f8b4f-188">Otomatik olarak hata ayıklama tuşuna F5 toostart ve web tarayıcınız yerel olarak çalışan toohello sayfasını açar.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-188">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

<span data-ttu-id="f8b4f-189">Kesme noktaları hello kaynakları, kullanım hello Gözcü pencerelerini, vb. ayarlayabilirsiniz. Merhaba bkz [Visual Studio belgeleri için Python Araçları] hakkında daha fazla bilgi için çeşitli özellikler hello.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-189">You can set breakpoints in hello sources, use hello watch windows, etc. See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="f8b4f-190">Değişiklik yapma</span><span class="sxs-lookup"><span data-stu-id="f8b4f-190">Make changes</span></span>
<span data-ttu-id="f8b4f-191">Şimdi değişiklikleri toohello uygulama kaynakları ve/veya şablonlarında yapmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-191">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="f8b4f-192">Değişikliklerinizi test ettikten sonra bunları toohello Git deposuna kaydedin:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-192">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a><span data-ttu-id="f8b4f-193">Daha fazla paket yükleme</span><span class="sxs-lookup"><span data-stu-id="f8b4f-193">Install more packages</span></span>
<span data-ttu-id="f8b4f-194">Uygulamanızın Python ve Django ötesinde bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-194">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="f8b4f-195">Pip kullanarak ek paketleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-195">You can install additional packages using pip.</span></span> <span data-ttu-id="f8b4f-196">bir paket tooinstall sağ tıklayın hello sanal ortam ve select **Python paketini Yükle**.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-196">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="f8b4f-197">Örneğin, tooinstall Merhaba, tooAzure depolama, service bus ve diğer Azure hizmetleriyle erişmenizi girin Python için Azure SDK `azure`:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-197">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

<span data-ttu-id="f8b4f-198">Merhaba sanal ortamda sağ tıklayıp **requirements.txt Oluştur** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-198">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="f8b4f-199">Ardından, hello değişiklikleri toorequirements.txt toohello Git deposuna uygulayın.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-199">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="f8b4f-200">TooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="f8b4f-200">Deploy tooAzure</span></span>
<span data-ttu-id="f8b4f-201">bir dağıtım tootrigger tıklayın **eşitleme** veya **anında**.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-201">tootrigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="f8b4f-202">Eşitleme, iletme ve çekme işlemini yapar.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-202">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

<span data-ttu-id="f8b4f-203">bir sanal ortam, yükleme paketleri vb. oluşturacağı gibi hello ilk dağıtım biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-203">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="f8b4f-204">Visual Studio hello hello dağıtımının ilerlemesini göstermez.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-204">Visual Studio doesn't show hello progress of hello deployment.</span></span> <span data-ttu-id="f8b4f-205">Tooreview hello çıkış isterseniz hello bölümüne bakarak [sorun giderme - dağıtım](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="f8b4f-205">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="f8b4f-206">Toohello Azure URL tooview değişikliklerinizi göz atın.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-206">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="f8b4f-207">Web uygulaması geliştirme - Windows - komut satırı</span><span class="sxs-lookup"><span data-stu-id="f8b4f-207">Web app development - Windows - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="f8b4f-208">Kopya hello deposu</span><span class="sxs-lookup"><span data-stu-id="f8b4f-208">Clone hello repository</span></span>
<span data-ttu-id="f8b4f-209">İlk olarak, Azure Portal hello üzerinde sağlanan hello URL'yi kullanarak hello depoyu kopyalayın ve uzak olarak hello Azure deposunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-209">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="f8b4f-210">Daha fazla bilgi için bkz: [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f8b4f-210">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="f8b4f-211">Sanal ortamı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-211">Create virtual environment</span></span>
<span data-ttu-id="f8b4f-212">(Bunu toohello depoya eklemeyin) geliştirme amacıyla yeni bir sanal ortam oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-212">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="f8b4f-213">Sanal ortamlar Hello uygulama üzerinde çalışan her geliştiricinin yerel olarak Kendininkini oluşturacağı şekilde python'daki, değildir.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-213">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="f8b4f-214">Toouse hello web uygulamanızda (runtime.txt veya hello uygulama ayarları dikey penceresinde hello Azure Portal kullanarak web uygulamanızda) için seçilen Python ile aynı sürümü emin olun.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-214">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="f8b4f-215">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-215">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="f8b4f-216">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-216">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="f8b4f-217">Uygulamanız için gereken herhangi bir dış paketi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-217">Install any external packages required by your application.</span></span> <span data-ttu-id="f8b4f-218">Sanal ortamınıza hello hello depo tooinstall hello paketleri kökünde hello requirements.txt dosyasını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-218">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="f8b4f-219">Süper kullanıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8b4f-219">Create a superuser</span></span>
<span data-ttu-id="f8b4f-220">Merhaba uygulamayla birlikte gelen hello veritabanında tanımlı bir süper kullanıcı yok.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-220">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="f8b4f-221">Oturum açma sırası toouse hello işlev hello uygulama ya da hello Django yönetim arabirimi (tooenable karar verirseniz,), bir süper kullanıcı toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-221">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="f8b4f-222">Bu hello komut satırı, proje klasöründen çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-222">Run this from hello command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="f8b4f-223">Merhaba istemleri tooset hello kullanıcı adı, parola vb. izleyin.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-223">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="f8b4f-224">Geliştirme sunucusu kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="f8b4f-224">Run using development server</span></span>
<span data-ttu-id="f8b4f-225">Komutu aşağıdaki hello ile Merhaba uygulaması geliştirme sunucusu altında başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-225">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python manage.py runserver

<span data-ttu-id="f8b4f-226">Merhaba konsol hello URL'si gösterilir ve bağlantı noktası hello sunucu dinler:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-226">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

<span data-ttu-id="f8b4f-227">Sonra web tarayıcısı toothat URL'nizi açın.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-227">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="f8b4f-228">Değişiklik yapma</span><span class="sxs-lookup"><span data-stu-id="f8b4f-228">Make changes</span></span>
<span data-ttu-id="f8b4f-229">Şimdi değişiklikleri toohello uygulama kaynakları ve/veya şablonlarında yapmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-229">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="f8b4f-230">Değişikliklerinizi test ettikten sonra bunları toohello Git deposuna kaydedin:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-230">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="f8b4f-231">Daha fazla paket yükleme</span><span class="sxs-lookup"><span data-stu-id="f8b4f-231">Install more packages</span></span>
<span data-ttu-id="f8b4f-232">Uygulamanızın Python ve Django ötesinde bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-232">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="f8b4f-233">Pip kullanarak ek paketleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-233">You can install additional packages using pip.</span></span> <span data-ttu-id="f8b4f-234">Örneğin, tooinstall Merhaba, imkanı sağlayan, Python için Azure SDK tooAzure depolama, service bus ve diğer Azure hizmetleriyle türü erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-234">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="f8b4f-235">Tooupdate requirements.txt emin olun:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-235">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="f8b4f-236">Merhaba değişiklikleri uygulayın:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-236">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="f8b4f-237">TooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="f8b4f-237">Deploy tooAzure</span></span>
<span data-ttu-id="f8b4f-238">bir dağıtım tootrigger, anında iletme hello tooAzure değiştirir:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-238">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="f8b4f-239">Merhaba Merhaba, sanal ortam oluşturma, paketleri yükleme, web.config oluşturma dahil dağıtım betiği çıktısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-239">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="f8b4f-240">Toohello Azure URL tooview değişikliklerinizi göz atın.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-240">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="f8b4f-241">Web uygulaması geliştirme - Mac/Linux - komut satırı</span><span class="sxs-lookup"><span data-stu-id="f8b4f-241">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="f8b4f-242">Kopya hello deposu</span><span class="sxs-lookup"><span data-stu-id="f8b4f-242">Clone hello repository</span></span>
<span data-ttu-id="f8b4f-243">İlk olarak, Azure Portal hello üzerinde sağlanan hello URL'yi kullanarak hello depoyu kopyalayın ve uzak olarak hello Azure deposunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-243">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="f8b4f-244">Daha fazla bilgi için bkz: [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f8b4f-244">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="f8b4f-245">Sanal ortamı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-245">Create virtual environment</span></span>
<span data-ttu-id="f8b4f-246">(Bunu toohello depoya eklemeyin) geliştirme amacıyla yeni bir sanal ortam oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-246">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="f8b4f-247">Sanal ortamlar Hello uygulama üzerinde çalışan her geliştiricinin yerel olarak Kendininkini oluşturacağı şekilde python'daki, değildir.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-247">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="f8b4f-248">Toouse hello web uygulamanızda (runtime.txt veya hello uygulama ayarları dikey penceresinde hello Azure Portal kullanarak web uygulamanızda) için seçilen Python ile aynı sürümü emin olun.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-248">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="f8b4f-249">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-249">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="f8b4f-250">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-250">For Python 3.4:</span></span>

    python -m venv env

<span data-ttu-id="f8b4f-251">or</span><span class="sxs-lookup"><span data-stu-id="f8b4f-251">or</span></span>

    pyvenv env

<span data-ttu-id="f8b4f-252">Uygulamanız için gereken herhangi bir dış paketi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-252">Install any external packages required by your application.</span></span> <span data-ttu-id="f8b4f-253">Sanal ortamınıza hello hello depo tooinstall hello paketleri kökünde hello requirements.txt dosyasını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-253">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="f8b4f-254">Süper kullanıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8b4f-254">Create a superuser</span></span>
<span data-ttu-id="f8b4f-255">Merhaba uygulamayla birlikte gelen hello veritabanında tanımlı bir süper kullanıcı yok.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-255">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="f8b4f-256">Oturum açma sırası toouse hello işlev hello uygulama ya da hello Django yönetim arabirimi (tooenable karar verirseniz,), bir süper kullanıcı toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-256">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="f8b4f-257">Bu hello komut satırı, proje klasöründen çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-257">Run this from hello command-line from your project folder:</span></span>

    env/bin/python manage.py createsuperuser

<span data-ttu-id="f8b4f-258">Merhaba istemleri tooset hello kullanıcı adı, parola vb. izleyin.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-258">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="f8b4f-259">Geliştirme sunucusu kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="f8b4f-259">Run using development server</span></span>
<span data-ttu-id="f8b4f-260">Komutu aşağıdaki hello ile Merhaba uygulaması geliştirme sunucusu altında başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-260">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python manage.py runserver

<span data-ttu-id="f8b4f-261">Merhaba konsol hello URL'si gösterilir ve bağlantı noktası hello sunucu dinler:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-261">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

<span data-ttu-id="f8b4f-262">Sonra web tarayıcısı toothat URL'nizi açın.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-262">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="f8b4f-263">Değişiklik yapma</span><span class="sxs-lookup"><span data-stu-id="f8b4f-263">Make changes</span></span>
<span data-ttu-id="f8b4f-264">Şimdi değişiklikleri toohello uygulama kaynakları ve/veya şablonlarında yapmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-264">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="f8b4f-265">Değişikliklerinizi test ettikten sonra bunları toohello Git deposuna kaydedin:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-265">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="f8b4f-266">Daha fazla paket yükleme</span><span class="sxs-lookup"><span data-stu-id="f8b4f-266">Install more packages</span></span>
<span data-ttu-id="f8b4f-267">Uygulamanızın Python ve Django ötesinde bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-267">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="f8b4f-268">Pip kullanarak ek paketleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-268">You can install additional packages using pip.</span></span> <span data-ttu-id="f8b4f-269">Örneğin, tooinstall Merhaba, imkanı sağlayan, Python için Azure SDK tooAzure depolama, service bus ve diğer Azure hizmetleriyle türü erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-269">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="f8b4f-270">Tooupdate requirements.txt emin olun:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-270">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="f8b4f-271">Merhaba değişiklikleri uygulayın:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-271">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="f8b4f-272">TooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="f8b4f-272">Deploy tooAzure</span></span>
<span data-ttu-id="f8b4f-273">bir dağıtım tootrigger, anında iletme hello tooAzure değiştirir:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-273">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="f8b4f-274">Merhaba Merhaba, sanal ortam oluşturma, paketleri yükleme, web.config oluşturma dahil dağıtım betiği çıktısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-274">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="f8b4f-275">Toohello Azure URL tooview değişikliklerinizi göz atın.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-275">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="f8b4f-276">Sorun giderme - Paket Yükleme</span><span class="sxs-lookup"><span data-stu-id="f8b4f-276">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="f8b4f-277">Sorun giderme - Sanal Ortam</span><span class="sxs-lookup"><span data-stu-id="f8b4f-277">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a><span data-ttu-id="f8b4f-278">Sorun giderme - Statik Dosyalar</span><span class="sxs-lookup"><span data-stu-id="f8b4f-278">Troubleshooting - Static Files</span></span>
<span data-ttu-id="f8b4f-279">Django statik dosyaları toplama hello kavramına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-279">Django has hello concept of collecting static files.</span></span> <span data-ttu-id="f8b4f-280">Bu tüm hello statik dosyaları özgün konumlarından alır ve bunları tooa tek klasörüne kopyalar.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-280">This takes all hello static files from their original location and copies them tooa single folder.</span></span> <span data-ttu-id="f8b4f-281">Bu uygulama için çok kopyalanırlar`/static`.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-281">For this application, they are copied too`/static`.</span></span>

<span data-ttu-id="f8b4f-282">Statik dosyalar farklı Django “uygulamalarından” gelebileceğinden bu yapılır.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-282">This is done because static files may come from different Django 'apps'.</span></span> <span data-ttu-id="f8b4f-283">Örneğin, hello Django yönetim arabirimlerindeki statik dosyalar hello hello sanal ortamdaki bir Django kitaplığı alt bulunur.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-283">For example, hello static files from hello Django admin interfaces are located in a Django library subfolder in hello virtual environment.</span></span> <span data-ttu-id="f8b4f-284">Bu uygulama tarafından tanımlanan statik dosyalar `/app/static` içinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-284">Static files defined by this application are located in `/app/static`.</span></span> <span data-ttu-id="f8b4f-285">Daha fazla Django “uygulamaları” kullandıkça, birden fazla yerde bulunan statik dosyalarınız olur.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-285">As you use more Django 'apps', you'll have static files located in multiple places.</span></span>

<span data-ttu-id="f8b4f-286">Merhaba uygulama hata ayıklama modunda çalışırken Merhaba uygulaması hello statik dosyaları özgün konumlarından işlevi görür.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-286">When running hello application in debug mode, hello application serves hello static files from their original location.</span></span>

<span data-ttu-id="f8b4f-287">Merhaba uygulama yayın modunda çalışırken Merhaba uygulaması mu **değil** hello statik dosyaları sunar.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-287">When running hello application in release mode, hello application does **not** serve hello static files.</span></span> <span data-ttu-id="f8b4f-288">Bunu hello hello web sunucusu tooserve hello dosyaları sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-288">It is hello responsibility of hello web server tooserve hello files.</span></span> <span data-ttu-id="f8b4f-289">Bu uygulama için IIS statik dosyaları hello hizmet `/static`.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-289">For this application, IIS will serve hello static files from `/static`.</span></span>

<span data-ttu-id="f8b4f-290">statik dosya Hello koleksiyonunu temizlenmesi hello dağıtım komut dosyası, daha önce toplanan parçası dosyalar halinde otomatik olarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-290">hello collection of static files is done automatically as part of hello deployment script, clearing previously collected files.</span></span> <span data-ttu-id="f8b4f-291">Bu hello koleksiyonu dağıtımı yavaşlattığı her dağıtımda meydana gelen ancak eski dosyaların olası bir güvenlik sorunu önlenerek kullanılabilir durumda olmaz sağlar anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-291">This means hello collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span></span>

<span data-ttu-id="f8b4f-292">Django uygulamanız için statik dosya tooskip koleksiyonunu istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-292">If you want tooskip collection of static files for your Django application:</span></span>

    \.skipDjango

<span data-ttu-id="f8b4f-293">Ardından toodo hello koleksiyonu yerel makinenizde el ile gerekir:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-293">Then you'll need toodo hello collection manually on your local machine:</span></span>

    env\scripts\python manage.py collectstatic

<span data-ttu-id="f8b4f-294">Merhaba kaldırmak `\static` klasöründen `.gitignore` ve toohello Git deposunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-294">Then remove hello `\static` folder from `.gitignore` and add it toohello Git repository.</span></span>

## <a name="troubleshooting---settings"></a><span data-ttu-id="f8b4f-295">Sorun giderme - Ayarlar</span><span class="sxs-lookup"><span data-stu-id="f8b4f-295">Troubleshooting - Settings</span></span>
<span data-ttu-id="f8b4f-296">Merhaba uygulama için çeşitli ayarları değiştirilebilir `DjangoWebProject/settings.py`.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-296">Various settings for hello application can be changed in `DjangoWebProject/settings.py`.</span></span>

<span data-ttu-id="f8b4f-297">Geliştiriciye kolaylık sağlamak için hata ayıklama modu etkindir.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-297">For developer convenience, debug mode is enabled.</span></span> <span data-ttu-id="f8b4f-298">Olumlu bir yan etkisi, yerel olarak toocollect statik dosyaları gerek kalmadan çalıştırırken mümkün toosee resimleri ve diğer statik içeriği olacak ' dir.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-298">One nice side effect of that is you'll be able toosee images and other static content when running locally, without having toocollect static files.</span></span>

<span data-ttu-id="f8b4f-299">toodisable hata ayıklama modu:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-299">toodisable debug mode:</span></span>

    DEBUG = False

<span data-ttu-id="f8b4f-300">Hata ayıklama devre dışı bırakıldığında, değeri hello `ALLOWED_HOSTS` gereksinimlerini toobe güncelleştirilmiş tooinclude hello Azure ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-300">When debug is disabled, hello value for `ALLOWED_HOSTS` needs toobe updated tooinclude hello Azure host name.</span></span> <span data-ttu-id="f8b4f-301">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-301">For example:</span></span>

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

<span data-ttu-id="f8b4f-302">veya tooenable herhangi:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-302">or tooenable any:</span></span>

    ALLOWED_HOSTS = (
        '*',
    )

<span data-ttu-id="f8b4f-303">Uygulamada, toodo arasında geçiş yapma ile daha karmaşık toodeal hata ayıklama ve sürüm modu ve alma hello ana bilgisayar adı isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-303">In practice, you may want toodo something more complex toodeal with switching between debug and release mode, and getting hello host name.</span></span>

<span data-ttu-id="f8b4f-304">Hello Azure portal aracılığıyla ortam değişkenlerini ayarlayabilirsiniz **yapılandırma** sayfasında hello **uygulama ayarları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-304">You can set environment variables through hello Azure portal **CONFIGURE** page, in hello **app settings** section.</span></span>  <span data-ttu-id="f8b4f-305">Bu değerler hello kaynaklarında (bağlantı dizeleri, parolalar vb.) tooappear istemeyebilirsiniz ya da Azure ile yerel makineniz arasında farklı tooset istediğiniz için faydalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-305">This can be useful for setting values that you may not want tooappear in hello sources (connection strings, passwords, etc), or that you want tooset differently between Azure and your local machine.</span></span> <span data-ttu-id="f8b4f-306">İçinde `settings.py`, kullanarak hello ortam değişkenlerini sorgulayabilirsiniz `os.getenv`.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-306">In `settings.py`, you can query hello environment variables using `os.getenv`.</span></span>

## <a name="using-a-database"></a><span data-ttu-id="f8b4f-307">Bir Veritabanını Kullanma</span><span class="sxs-lookup"><span data-stu-id="f8b4f-307">Using a Database</span></span>
<span data-ttu-id="f8b4f-308">Merhaba uygulama ile birlikte hello veritabanı bir sqlite veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-308">hello database that is included with hello application is a sqlite database.</span></span> <span data-ttu-id="f8b4f-309">Neredeyse hiçbir Kurulum gerektirmediğinden, geliştirme için kullanışlı ve faydalıdır veritabanı toouse budur.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-309">This is a convenient and useful default database toouse for development, as it requires almost no setup.</span></span> <span data-ttu-id="f8b4f-310">Merhaba veritabanı hello hello proje klasöründeki db.sqlite3 dosyasında depolanır.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-310">hello database is stored in hello db.sqlite3 file in hello project folder.</span></span>

<span data-ttu-id="f8b4f-311">Azure Django uygulamasından kolay toouse olan veritabanı hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-311">Azure provides database services which are easy toouse from a Django application.</span></span> <span data-ttu-id="f8b4f-312">Kullanma öğreticileri [SQL veritabanı] ve [MySQL] Django uygulamasından hello adımlar gerekli toocreate hello veritabanı hizmeti gösterir, hello veritabanı ayarlarını değiştirmek `DjangoWebProject/settings.py`ve hello kitaplıkları tooinstall gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show hello steps necessary toocreate hello database service, change hello database settings in `DjangoWebProject/settings.py`, and hello libraries required tooinstall.</span></span>

<span data-ttu-id="f8b4f-313">Elbette, kendi veritabanı sunucularınızı toomanage tercih ederseniz, bunu Windows veya Linux Azure üzerinde çalışan sanal makineleri kullanarak yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-313">Of course, if you prefer toomanage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span></span>

## <a name="django-admin-interface"></a><span data-ttu-id="f8b4f-314">Django Yönetim Arabirimi</span><span class="sxs-lookup"><span data-stu-id="f8b4f-314">Django Admin Interface</span></span>
<span data-ttu-id="f8b4f-315">Modellerinizi oluşturmaya başladıktan sonra toopopulate hello veritabanını bazı verilerle istersiniz.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-315">Once you start building your models, you'll want toopopulate hello database with some data.</span></span> <span data-ttu-id="f8b4f-316">Toouse hello Django yönetim arabirimini toodo ekleme ve etkileşimli olarak içerik düzenleme kolay bir yoludur..</span><span class="sxs-lookup"><span data-stu-id="f8b4f-316">An easy way toodo add and edit content interactively is toouse hello Django administration interface.</span></span>

<span data-ttu-id="f8b4f-317">hello yönetim arabirimi Hello kodunu hello uygulama kaynaklarında dışı bırakılmıştır, ancak bunu ('admin' arayın) kolayca etkinleştirebileceğiniz şekilde açıkça işaretlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-317">hello code for hello admin interface is commented out in hello application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span></span>

<span data-ttu-id="f8b4f-318">Etkinleştirildikten sonra hello veritabanını eşitleyin, hello uygulamayı çalıştırın ve çok gidin`/admin`.</span><span class="sxs-lookup"><span data-stu-id="f8b4f-318">After it's enabled, synchronize hello database, run hello application and navigate too`/admin`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8b4f-319">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="f8b4f-319">Next Steps</span></span>
<span data-ttu-id="f8b4f-320">Bu bağlantılar toolearn Django ve Python araçları hakkında daha fazla bilgi için Visual Studio izleyin:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-320">Follow these links toolearn more about Django and Python Tools for Visual Studio:</span></span>

* <span data-ttu-id="f8b4f-321">[Django Belgeleri]</span><span class="sxs-lookup"><span data-stu-id="f8b4f-321">[Django Documentation]</span></span>
* <span data-ttu-id="f8b4f-322">[Visual Studio belgeleri için Python Araçları]</span><span class="sxs-lookup"><span data-stu-id="f8b4f-322">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="f8b4f-323">SQL Database’i ve MySQL’i kullanma hakkında bilgi için:</span><span class="sxs-lookup"><span data-stu-id="f8b4f-323">For information on using SQL Database and MySQL:</span></span>

* <span data-ttu-id="f8b4f-324">[Visual Studio için Python Araçları ile Azure’da Django ve MySQL]</span><span class="sxs-lookup"><span data-stu-id="f8b4f-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="f8b4f-325">[Visual Studio için Python Araçları ile Azure’da Django ve SQL Veritabanı]</span><span class="sxs-lookup"><span data-stu-id="f8b4f-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="f8b4f-326">Daha fazla bilgi için bkz: Merhaba [Python Geliştirici Merkezi](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="f8b4f-326">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="f8b4f-327">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="f8b4f-327">What's changed</span></span>
* <span data-ttu-id="f8b4f-328">Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="f8b4f-328">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Visual Studio için Python Araçları ile Azure’da Django ve MySQL]: web-sites-python-ptvs-django-mysql.md
[Visual Studio için Python Araçları ile Azure’da Django ve SQL Veritabanı]: web-sites-python-ptvs-django-sql.md
[SQL veritabanı]: web-sites-python-ptvs-django-sql.md
[MySQL]: web-sites-python-ptvs-django-mysql.md

<!--External Link references-->
[Python 2.7 için Azure SDK]: http://go.microsoft.com/fwlink/?linkid=254281
[Python 3.4 için Azure SDK]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Windows için Git]: http://msysgit.github.io/
[Windows için GitHub]: https://windows.github.com/
[Visual Studio için Python Araçları]: http://aka.ms/ptvs
[Visual Studio için Python Araçları 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[Visual Studio belgeleri için Python Araçları]: http://aka.ms/ptvsdocs
[Django Belgeleri]: https://www.djangoproject.com/
