---
title: "Azure’da Django ile web uygulamaları oluşturma"
description: "Azure App Service Web Apps’te bir Python web uygulaması çalıştırmayı gösteren bir öğretici."
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
ms.openlocfilehash: 388a2db21dd1669b48b3204aaa322d7915905506
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a><span data-ttu-id="6613f-103">Azure’da Django ile web uygulamaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="6613f-103">Creating web apps with Django in Azure</span></span>
<span data-ttu-id="6613f-104">Bu öğretici, çalışan, [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714)’te Python çalıştırmaya nasıl başlayacağınızı açıklar.</span><span class="sxs-lookup"><span data-stu-id="6613f-104">This tutorial describes how to get started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="6613f-105">Web Apps sınırlı ücretsiz barındırma ve hızlı dağıtım sağlar ve Python’u kullanmanıza olanak tanır!</span><span class="sxs-lookup"><span data-stu-id="6613f-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="6613f-106">Uygulamanız büyüdükçe, ücretli barındırmaya geçebilir ve aynı zamanda tüm diğer Azure hizmetleriyle tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6613f-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="6613f-107">Django web altyapısını kullanarak bir uygulama oluşturacaksınız (bu öğreticinin diğer sürümleri için bkz. [Flask](web-sites-python-create-deploy-flask-app.md) ve [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="6613f-107">You will create an application using the Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span> <span data-ttu-id="6613f-108">Azure Marketi'nde bir web uygulaması oluşturacak, Git dağıtımı ayarlayacak ve depoyu yerel olarak kopyalayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="6613f-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="6613f-109">Sonra, uygulamayı yerel olarak çalıştıracak, değişiklikler yapacak, yürütecek ve bunları Azure'a ileteceksiniz.</span><span class="sxs-lookup"><span data-stu-id="6613f-109">Then you will run the application locally, make changes, commit and push them to Azure.</span></span> <span data-ttu-id="6613f-110">Öğretici, Windows veya Mac/Linux’ta bunun nasıl yapıldığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="6613f-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="6613f-111">Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="6613f-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="6613f-112">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6613f-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="6613f-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6613f-113">Prerequisites</span></span>
* <span data-ttu-id="6613f-114">Windows, Mac veya Linux</span><span class="sxs-lookup"><span data-stu-id="6613f-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="6613f-115">Python 2.7 ya da 3.4</span><span class="sxs-lookup"><span data-stu-id="6613f-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="6613f-116">setuptools, pip, virtualenv (yalnızca Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="6613f-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="6613f-117">Git</span><span class="sxs-lookup"><span data-stu-id="6613f-117">Git</span></span>
* <span data-ttu-id="6613f-118">[Visual Studio için Python Araçları][Visual Studio için Python Araçları] (PTVS) - Not: Bu özellik isteğe bağlıdır</span><span class="sxs-lookup"><span data-stu-id="6613f-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="6613f-119">**Not**: TFS yayımlama şu anda Python projeleri için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="6613f-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="6613f-120">Windows</span><span class="sxs-lookup"><span data-stu-id="6613f-120">Windows</span></span>
<span data-ttu-id="6613f-121">Python 2.7 ya da 3.4 yüklü (32 bit) değilse, Web Platformu Yükleyicisi'ni kullanarak [Python 2.7 için Azure SDK] veya [Python 3.4 için Azure SDK]’yı yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="6613f-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="6613f-122">Bu, Python’un 32 bit sürümünü, setuptools, PIP, virtualenv vb.yükler (32 bit Python, Azure ana makinelerde yüklü olandır).</span><span class="sxs-lookup"><span data-stu-id="6613f-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="6613f-123">Alternatif olarak, Python’u [python.org] adresinden edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6613f-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="6613f-124">Git için, [Windows için Git] veya [Windows için GitHub]’ı öneririz.</span><span class="sxs-lookup"><span data-stu-id="6613f-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="6613f-125">Visual Studio kullanıyorsanız, tümleşik Git desteğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6613f-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="6613f-126">Ayrıca [Visual Studio için Python Araçları 2.2]’yi yüklemenizi öneririz </span><span class="sxs-lookup"><span data-stu-id="6613f-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="6613f-127">Bu isteğe bağlıdır, ancak ücretsiz Visual Studio Community 2013 veya Web için Visual Studio Express 2013 içeren [Visual Studio] varsa, bu size mükemmel bir Python IDE verir.</span><span class="sxs-lookup"><span data-stu-id="6613f-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="6613f-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="6613f-128">Mac/Linux</span></span>
<span data-ttu-id="6613f-129">Python ve Git sizde zaten yüklü olmalıdır, ancak Python 2.7 veya 3.4 olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="6613f-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-portal"></a><span data-ttu-id="6613f-130">Portalda Web Uygulaması Oluşturma</span><span class="sxs-lookup"><span data-stu-id="6613f-130">Web App Creation on Portal</span></span>
<span data-ttu-id="6613f-131">Uygulamanızı oluşturmanın ilk adımı, [Azure Portal](https://portal.azure.com) aracılığıyla web uygulaması oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="6613f-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="6613f-132">Azure Portal’da oturum açın ve sol alt köşede **NEW** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6613f-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span>
2. <span data-ttu-id="6613f-133">Arama kutusuna, "python" yazın.</span><span class="sxs-lookup"><span data-stu-id="6613f-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="6613f-134">Arama sonuçlarında **Django**’yu (PTVS tarafından yayımlanır) seçin ve ardından **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6613f-134">In the search results, select **Django** (published by PTVS), then click **Create**.</span></span>
4. <span data-ttu-id="6613f-135">Yeni bir App Service planı ve bunun için yeni bir kaynak grubu oluşturma şeklinde, yeni Django uygulamasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6613f-135">Configure the new Django app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="6613f-136">Sonra, **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6613f-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="6613f-137">Yeni oluşturulan web uygulamanız için, [Azure Uygulama Hizmeti’nde Yerel Git Dağıtımı](app-service-deploy-local-git.md) başlığındaki yönergeleri izleyerek Git yayımlamayı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6613f-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="6613f-138">Uygulamaya Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="6613f-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="6613f-139">Git deposu içeriği</span><span class="sxs-lookup"><span data-stu-id="6613f-139">Git repository contents</span></span>
<span data-ttu-id="6613f-140">Burada, sonraki bölümde kopyalayacağımız, ilk Git deposunda bulacağınız dosyalara bir genel bakış yer alır.</span><span class="sxs-lookup"><span data-stu-id="6613f-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

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

<span data-ttu-id="6613f-141">Uygulama için ana kaynaklar</span><span class="sxs-lookup"><span data-stu-id="6613f-141">Main sources for the application.</span></span> <span data-ttu-id="6613f-142">Ana düzenle birlikte 3 sayfadan (dizin, hakkında, iletişim) oluşur.</span><span class="sxs-lookup"><span data-stu-id="6613f-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span> <span data-ttu-id="6613f-143">Statik içerik ve betikler bootstrap, jquery, modernize ve yanıtı içerir.</span><span class="sxs-lookup"><span data-stu-id="6613f-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \manage.py

<span data-ttu-id="6613f-144">Yerel yönetim ve geliştirme sunucusu desteği.</span><span class="sxs-lookup"><span data-stu-id="6613f-144">Local management and development server support.</span></span> <span data-ttu-id="6613f-145">Uygulamayı yerel olarak çalıştırmak, veritabanını eşitlemek vb. için bunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="6613f-145">Use this to run the application locally, synchronize the database, etc.</span></span>

    \db.sqlite3

<span data-ttu-id="6613f-146">Varsayılan veritabanı.</span><span class="sxs-lookup"><span data-stu-id="6613f-146">Default database.</span></span> <span data-ttu-id="6613f-147">Uygulamanın çalıştırılması için gerekli tabloları içerir, ancak herhangi bir kullanıcı içermez (kullanıcı oluşturmak için veritabanını eşitleyin) içermiyor.</span><span class="sxs-lookup"><span data-stu-id="6613f-147">Includes the necessary tables for the application to run, but does not contain any users (synchronize the database to create a user).</span></span>

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

<span data-ttu-id="6613f-148">[Visual Studio için Python Araçları] ile birlikte kullanmak için proje dosyaları.</span><span class="sxs-lookup"><span data-stu-id="6613f-148">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="6613f-149">Sanal ortamlar için IIS proxy ve PTVS uzaktan hata ayıklama desteği</span><span class="sxs-lookup"><span data-stu-id="6613f-149">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="6613f-150">Bu uygulamaya dış paketler gerekir.</span><span class="sxs-lookup"><span data-stu-id="6613f-150">External packages needed by this application.</span></span> <span data-ttu-id="6613f-151">Dağıtım betiği pip bu dosyada listelenen paketleri pip yükler.</span><span class="sxs-lookup"><span data-stu-id="6613f-151">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="6613f-152">IIS yapılandırma dosyaları.</span><span class="sxs-lookup"><span data-stu-id="6613f-152">IIS configuration files.</span></span> <span data-ttu-id="6613f-153">Dağıtım betiği, uygun web.x.y.config’i kullanır ve bunu web.config olarak kopyalar.</span><span class="sxs-lookup"><span data-stu-id="6613f-153">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="6613f-154">İsteğe bağlı dosyalar - Dağıtımı özelleştirme</span><span class="sxs-lookup"><span data-stu-id="6613f-154">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="6613f-155">İsteğe bağlı dosyalar - Python çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="6613f-155">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="6613f-156">Sunucu üzerindeki ek dosyalar</span><span class="sxs-lookup"><span data-stu-id="6613f-156">Additional files on server</span></span>
<span data-ttu-id="6613f-157">Bazı dosyalar sunucuda yer alır ancak git deposuna eklenmez.</span><span class="sxs-lookup"><span data-stu-id="6613f-157">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="6613f-158">Bunlar dağıtım betiği tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6613f-158">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="6613f-159">IIS yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="6613f-159">IIS configuration file.</span></span> <span data-ttu-id="6613f-160">Her dağıtımda web.x.y.config tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6613f-160">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="6613f-161">Python sanal ortamı.</span><span class="sxs-lookup"><span data-stu-id="6613f-161">Python virtual environment.</span></span> <span data-ttu-id="6613f-162">Web uygulamasında uyumlu sanal ortam zaten yoksa, dağıtım ırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6613f-162">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span> <span data-ttu-id="6613f-163">Requirements.txt içinde listelenen paketler pip yüklüdür, ancak paketler zaten yüklü ise pip yüklemeyi atlar.</span><span class="sxs-lookup"><span data-stu-id="6613f-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="6613f-164">Sonraki 3 bölümde farklı 3 ortamda web uygulaması geliştirmeye devam etme açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="6613f-164">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="6613f-165">Windows, Visual Studio için Python Araçları ile</span><span class="sxs-lookup"><span data-stu-id="6613f-165">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="6613f-166">Windows, komut satırı ile</span><span class="sxs-lookup"><span data-stu-id="6613f-166">Windows, with command line</span></span>
* <span data-ttu-id="6613f-167">Mac/Linux, komut satırı ile</span><span class="sxs-lookup"><span data-stu-id="6613f-167">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="6613f-168">Web uygulaması geliştirme - Windows - Visual Studio için Python Araçları</span><span class="sxs-lookup"><span data-stu-id="6613f-168">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="6613f-169">Depoyu kopyalama</span><span class="sxs-lookup"><span data-stu-id="6613f-169">Clone the repository</span></span>
<span data-ttu-id="6613f-170">İlk olarak, Azure Portal'da sağlanan URL'yi kullanarak depoyu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="6613f-170">First, clone the repository using the URL provided on the Azure Portal.</span></span> <span data-ttu-id="6613f-171">Daha fazla bilgi için bkz. [Azure Uygulama Hizmeti’nde Yerel Git Dağıtımı](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="6613f-171">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="6613f-172">Depo kök dizininde bulunan çözüm dosyasını (.sln) açın.</span><span class="sxs-lookup"><span data-stu-id="6613f-172">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="6613f-173">Sanal ortamı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6613f-173">Create virtual environment</span></span>
<span data-ttu-id="6613f-174">Şimdi, yerel geliştirme için sanal bir ortam oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="6613f-174">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="6613f-175">Sağ **Python Ortamları**’na sağ tıklayın **Sanal Ortam Ekle...** seçeneğini seçin.</span><span class="sxs-lookup"><span data-stu-id="6613f-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="6613f-176">Ortam adının `env` olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="6613f-176">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="6613f-177">Temel yorumlayıcıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="6613f-177">Select the base interpreter.</span></span> <span data-ttu-id="6613f-178">Web uygulamanız için seçilen Python ile aynı sürümü kullandığınızdan emin olun (runtime.txt içinde veya Azure Portal’da uygulamanızın **Uygulama Ayarları** dikey penceresinde).</span><span class="sxs-lookup"><span data-stu-id="6613f-178">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="6613f-179">Paketleri indirme ve yükleme seçeneğinin işaretli olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="6613f-179">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="6613f-180">**Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6613f-180">Click **Create**.</span></span> <span data-ttu-id="6613f-181">Bu, sanal ortamı oluşturur ve requirements.txt içinde listelenen bağımlılıkları yükler.</span><span class="sxs-lookup"><span data-stu-id="6613f-181">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="create-a-superuser"></a><span data-ttu-id="6613f-182">Süper kullanıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6613f-182">Create a superuser</span></span>
<span data-ttu-id="6613f-183">Uygulamayla birlikte gelen veritabanında tanımlı bir süper kullanıcı yoktur.</span><span class="sxs-lookup"><span data-stu-id="6613f-183">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="6613f-184">Uygulamadaki oturum açma işlevini ya da Django yönetim arabirimini (etkinleştirmeye karar verirseniz) kullanmak için, bir süper kullanıcı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6613f-184">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="6613f-185">Proje klasörünüzdeki komut satırından bunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6613f-185">Run this from the command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="6613f-186">Kullanıcı adı, parola vb. ayarlamak için yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="6613f-186">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="6613f-187">Geliştirme sunucusu kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="6613f-187">Run using development server</span></span>
<span data-ttu-id="6613f-188">Hata ayıklamayı başlatmak için F5 tuşuna basın, böylece web tarayıcınız yerel olarak çalışan sayfaya otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="6613f-188">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

<span data-ttu-id="6613f-189">Kaynaklarda kesme noktalarını ayarlayabilir, gözcü pencerelerini kullanabilirsiniz vb. Çeşitli özellikler hakkında daha fazla bilgi için bkz. [Visual Studio Belgeleri için Python Araçları].</span><span class="sxs-lookup"><span data-stu-id="6613f-189">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="6613f-190">Değişiklik yapma</span><span class="sxs-lookup"><span data-stu-id="6613f-190">Make changes</span></span>
<span data-ttu-id="6613f-191">Şimdi uygulama kaynakları ve/veya şablonlarında değişiklikler yapmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6613f-191">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="6613f-192">Değişikliklerinizi test ettikten sonra bunları Git deposuna kaydedin:</span><span class="sxs-lookup"><span data-stu-id="6613f-192">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a><span data-ttu-id="6613f-193">Daha fazla paket yükleme</span><span class="sxs-lookup"><span data-stu-id="6613f-193">Install more packages</span></span>
<span data-ttu-id="6613f-194">Uygulamanızın Python ve Django ötesinde bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="6613f-194">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="6613f-195">Pip kullanarak ek paketleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6613f-195">You can install additional packages using pip.</span></span> <span data-ttu-id="6613f-196">Bir paketi yüklemek için, sanal ortamda sağ tıklayıp **Python Paketini Yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="6613f-196">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="6613f-197">Örneğin, size Azure Storage, Service Bus ve diğer Azure hizmetleri için erişim imkanı sağlayan, Python için Azure SDK'yı yüklemek için şunu girin: `azure`</span><span class="sxs-lookup"><span data-stu-id="6613f-197">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

<span data-ttu-id="6613f-198">Sanal ortamda sağ tıklayıp **requirements.txt oluştur**’u seçerek requirements.txt dosyasını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6613f-198">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="6613f-199">Ardından, requirements.txt dosyasındaki değişiklikleri Git deposuna uygulayın.</span><span class="sxs-lookup"><span data-stu-id="6613f-199">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="6613f-200">Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="6613f-200">Deploy to Azure</span></span>
<span data-ttu-id="6613f-201">Bir dağıtımı tetiklemek için tıklatın **Eşitle** veya **İlet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6613f-201">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="6613f-202">Eşitleme, iletme ve çekme işlemini yapar.</span><span class="sxs-lookup"><span data-stu-id="6613f-202">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

<span data-ttu-id="6613f-203">Sanal ortam, yükleme paketleri vb. oluşturacağında, ilk dağıtımın gerçekleşmesi biraz zaman alır.</span><span class="sxs-lookup"><span data-stu-id="6613f-203">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="6613f-204">Visual Studio dağıtımın ilerleme durumunu göstermez.</span><span class="sxs-lookup"><span data-stu-id="6613f-204">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="6613f-205">Çıktıyı gözden geçirmek isterseniz, üzerinde bakın [Sorun Giderme - Dağıtım](#troubleshooting-deployment)’daki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="6613f-205">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="6613f-206">Yaptığınız değişiklikleri görmek için Azure URL'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="6613f-206">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="6613f-207">Web uygulaması geliştirme - Windows - komut satırı</span><span class="sxs-lookup"><span data-stu-id="6613f-207">Web app development - Windows - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="6613f-208">Depoyu kopyalama</span><span class="sxs-lookup"><span data-stu-id="6613f-208">Clone the repository</span></span>
<span data-ttu-id="6613f-209">İlk olarak, Azure Portal'da sağlanan URL'yi kullanarak depoyu kopyalayın ve uzak olarak Azure deposunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6613f-209">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="6613f-210">Daha fazla bilgi için bkz. [Azure Uygulama Hizmeti’nde Yerel Git Dağıtımı](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="6613f-210">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="6613f-211">Sanal ortamı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6613f-211">Create virtual environment</span></span>
<span data-ttu-id="6613f-212">Geliştirme amacına yönelik yeni bir sanal ortam oluşturacağız (bunu depoya eklemeyin).</span><span class="sxs-lookup"><span data-stu-id="6613f-212">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="6613f-213">Uygulama üzerinde çalışan her geliştiricinin yerel olarak kendininkini oluşturacağı şekilde, Python’daki sanal ortamlar yeniden yerleştirilebilir değildir.</span><span class="sxs-lookup"><span data-stu-id="6613f-213">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="6613f-214">Web uygulamanız için seçilen Python ile aynı sürümü kullandığınızdan emin olun (runtime.txt içinde veya Azure Portal’da uygulamanızın Uygulama Ayarları dikey penceresinde).</span><span class="sxs-lookup"><span data-stu-id="6613f-214">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="6613f-215">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="6613f-215">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="6613f-216">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="6613f-216">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="6613f-217">Uygulamanız için gereken herhangi bir dış paketi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6613f-217">Install any external packages required by your application.</span></span> <span data-ttu-id="6613f-218">Sanal ortamınıza paketleri yüklemek için depo kökündeki requirements.txt dosyasını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6613f-218">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="6613f-219">Süper kullanıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6613f-219">Create a superuser</span></span>
<span data-ttu-id="6613f-220">Uygulamayla birlikte gelen veritabanında tanımlı bir süper kullanıcı yoktur.</span><span class="sxs-lookup"><span data-stu-id="6613f-220">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="6613f-221">Uygulamadaki oturum açma işlevini ya da Django yönetim arabirimini (etkinleştirmeye karar verirseniz) kullanmak için, bir süper kullanıcı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6613f-221">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="6613f-222">Proje klasörünüzdeki komut satırından bunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6613f-222">Run this from the command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="6613f-223">Kullanıcı adı, parola vb. ayarlamak için yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="6613f-223">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="6613f-224">Geliştirme sunucusu kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="6613f-224">Run using development server</span></span>
<span data-ttu-id="6613f-225">Aşağıdaki komutla bir geliştirme sunucusu altında uygulamayı başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6613f-225">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python manage.py runserver

<span data-ttu-id="6613f-226">Konsol URL’yi ve sunucunun dinlediği bağlantı noktasını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="6613f-226">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

<span data-ttu-id="6613f-227">Sonra, bu URL için web tarayıcınızı açın.</span><span class="sxs-lookup"><span data-stu-id="6613f-227">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="6613f-228">Değişiklik yapma</span><span class="sxs-lookup"><span data-stu-id="6613f-228">Make changes</span></span>
<span data-ttu-id="6613f-229">Şimdi uygulama kaynakları ve/veya şablonlarında değişiklikler yapmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6613f-229">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="6613f-230">Değişikliklerinizi test ettikten sonra bunları Git deposuna kaydedin:</span><span class="sxs-lookup"><span data-stu-id="6613f-230">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="6613f-231">Daha fazla paket yükleme</span><span class="sxs-lookup"><span data-stu-id="6613f-231">Install more packages</span></span>
<span data-ttu-id="6613f-232">Uygulamanızın Python ve Django ötesinde bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="6613f-232">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="6613f-233">Pip kullanarak ek paketleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6613f-233">You can install additional packages using pip.</span></span> <span data-ttu-id="6613f-234">Örneğin, size Azure Storage, Service Bus ve diğer Azure hizmetleri için erişim imkanı sağlayan, Python için Azure SDK'yı yüklemek için aşağıdakileri yazın:</span><span class="sxs-lookup"><span data-stu-id="6613f-234">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="6613f-235">Requirements.txt dosyasını güncelleştirdiğinizden emin olun:</span><span class="sxs-lookup"><span data-stu-id="6613f-235">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="6613f-236">Değişiklikleri uygulayın:</span><span class="sxs-lookup"><span data-stu-id="6613f-236">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="6613f-237">Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="6613f-237">Deploy to Azure</span></span>
<span data-ttu-id="6613f-238">Bir dağıtımı tetiklemek için, değişiklikleri Azure’a gönderin:</span><span class="sxs-lookup"><span data-stu-id="6613f-238">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="6613f-239">Sanal ortam oluşturma, paketleri yükleme, web.config oluşturma dahil dağıtım betiği çıktısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6613f-239">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="6613f-240">Yaptığınız değişiklikleri görmek için Azure URL'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="6613f-240">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="6613f-241">Web uygulaması geliştirme - Mac/Linux - komut satırı</span><span class="sxs-lookup"><span data-stu-id="6613f-241">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="6613f-242">Depoyu kopyalama</span><span class="sxs-lookup"><span data-stu-id="6613f-242">Clone the repository</span></span>
<span data-ttu-id="6613f-243">İlk olarak, Azure Portal'da sağlanan URL'yi kullanarak depoyu kopyalayın ve uzak olarak Azure deposunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6613f-243">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="6613f-244">Daha fazla bilgi için bkz. [Azure Uygulama Hizmeti’nde Yerel Git Dağıtımı](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="6613f-244">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="6613f-245">Sanal ortamı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6613f-245">Create virtual environment</span></span>
<span data-ttu-id="6613f-246">Geliştirme amacına yönelik yeni bir sanal ortam oluşturacağız (bunu depoya eklemeyin).</span><span class="sxs-lookup"><span data-stu-id="6613f-246">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="6613f-247">Uygulama üzerinde çalışan her geliştiricinin yerel olarak kendininkini oluşturacağı şekilde, Python’daki sanal ortamlar yeniden yerleştirilebilir değildir.</span><span class="sxs-lookup"><span data-stu-id="6613f-247">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="6613f-248">Web uygulamanız için seçilen Python ile aynı sürümü kullandığınızdan emin olun (runtime.txt içinde veya Azure Portal’da uygulamanızın Uygulama Ayarları dikey penceresinde).</span><span class="sxs-lookup"><span data-stu-id="6613f-248">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="6613f-249">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="6613f-249">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="6613f-250">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="6613f-250">For Python 3.4:</span></span>

    python -m venv env

<span data-ttu-id="6613f-251">or</span><span class="sxs-lookup"><span data-stu-id="6613f-251">or</span></span>

    pyvenv env

<span data-ttu-id="6613f-252">Uygulamanız için gereken herhangi bir dış paketi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6613f-252">Install any external packages required by your application.</span></span> <span data-ttu-id="6613f-253">Sanal ortamınıza paketleri yüklemek için depo kökündeki requirements.txt dosyasını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6613f-253">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="6613f-254">Süper kullanıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6613f-254">Create a superuser</span></span>
<span data-ttu-id="6613f-255">Uygulamayla birlikte gelen veritabanında tanımlı bir süper kullanıcı yoktur.</span><span class="sxs-lookup"><span data-stu-id="6613f-255">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="6613f-256">Uygulamadaki oturum açma işlevini ya da Django yönetim arabirimini (etkinleştirmeye karar verirseniz) kullanmak için, bir süper kullanıcı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6613f-256">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="6613f-257">Proje klasörünüzdeki komut satırından bunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6613f-257">Run this from the command-line from your project folder:</span></span>

    env/bin/python manage.py createsuperuser

<span data-ttu-id="6613f-258">Kullanıcı adı, parola vb. ayarlamak için yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="6613f-258">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="6613f-259">Geliştirme sunucusu kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="6613f-259">Run using development server</span></span>
<span data-ttu-id="6613f-260">Aşağıdaki komutla bir geliştirme sunucusu altında uygulamayı başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6613f-260">You can launch the application under a development server with the following command:</span></span>

    env/bin/python manage.py runserver

<span data-ttu-id="6613f-261">Konsol URL’yi ve sunucunun dinlediği bağlantı noktasını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="6613f-261">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

<span data-ttu-id="6613f-262">Sonra, bu URL için web tarayıcınızı açın.</span><span class="sxs-lookup"><span data-stu-id="6613f-262">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="6613f-263">Değişiklik yapma</span><span class="sxs-lookup"><span data-stu-id="6613f-263">Make changes</span></span>
<span data-ttu-id="6613f-264">Şimdi uygulama kaynakları ve/veya şablonlarında değişiklikler yapmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6613f-264">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="6613f-265">Değişikliklerinizi test ettikten sonra bunları Git deposuna kaydedin:</span><span class="sxs-lookup"><span data-stu-id="6613f-265">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="6613f-266">Daha fazla paket yükleme</span><span class="sxs-lookup"><span data-stu-id="6613f-266">Install more packages</span></span>
<span data-ttu-id="6613f-267">Uygulamanızın Python ve Django ötesinde bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="6613f-267">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="6613f-268">Pip kullanarak ek paketleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6613f-268">You can install additional packages using pip.</span></span> <span data-ttu-id="6613f-269">Örneğin, size Azure Storage, Service Bus ve diğer Azure hizmetleri için erişim imkanı sağlayan, Python için Azure SDK'yı yüklemek için aşağıdakileri yazın:</span><span class="sxs-lookup"><span data-stu-id="6613f-269">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="6613f-270">Requirements.txt dosyasını güncelleştirdiğinizden emin olun:</span><span class="sxs-lookup"><span data-stu-id="6613f-270">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="6613f-271">Değişiklikleri uygulayın:</span><span class="sxs-lookup"><span data-stu-id="6613f-271">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="6613f-272">Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="6613f-272">Deploy to Azure</span></span>
<span data-ttu-id="6613f-273">Bir dağıtımı tetiklemek için, değişiklikleri Azure’a gönderin:</span><span class="sxs-lookup"><span data-stu-id="6613f-273">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="6613f-274">Sanal ortam oluşturma, paketleri yükleme, web.config oluşturma dahil dağıtım betiği çıktısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6613f-274">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="6613f-275">Yaptığınız değişiklikleri görmek için Azure URL'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="6613f-275">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="6613f-276">Sorun giderme - Paket Yükleme</span><span class="sxs-lookup"><span data-stu-id="6613f-276">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="6613f-277">Sorun giderme - Sanal Ortam</span><span class="sxs-lookup"><span data-stu-id="6613f-277">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a><span data-ttu-id="6613f-278">Sorun giderme - Statik Dosyalar</span><span class="sxs-lookup"><span data-stu-id="6613f-278">Troubleshooting - Static Files</span></span>
<span data-ttu-id="6613f-279">Django statik dosyaları toplama kavramına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="6613f-279">Django has the concept of collecting static files.</span></span> <span data-ttu-id="6613f-280">Bu, tüm statik dosyaları özgün konumlarından alır ve tek bir klasöre kopyalar.</span><span class="sxs-lookup"><span data-stu-id="6613f-280">This takes all the static files from their original location and copies them to a single folder.</span></span> <span data-ttu-id="6613f-281">Bu uygulama için, bunlar `/static` klasörüne kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="6613f-281">For this application, they are copied to `/static`.</span></span>

<span data-ttu-id="6613f-282">Statik dosyalar farklı Django “uygulamalarından” gelebileceğinden bu yapılır.</span><span class="sxs-lookup"><span data-stu-id="6613f-282">This is done because static files may come from different Django 'apps'.</span></span> <span data-ttu-id="6613f-283">Örneğin, Django yönetim arabirimlerindeki statik dosyalar sanal ortamdaki bir Django kitaplığı alt klasöründe yer alır.</span><span class="sxs-lookup"><span data-stu-id="6613f-283">For example, the static files from the Django admin interfaces are located in a Django library subfolder in the virtual environment.</span></span> <span data-ttu-id="6613f-284">Bu uygulama tarafından tanımlanan statik dosyalar `/app/static` içinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="6613f-284">Static files defined by this application are located in `/app/static`.</span></span> <span data-ttu-id="6613f-285">Daha fazla Django “uygulamaları” kullandıkça, birden fazla yerde bulunan statik dosyalarınız olur.</span><span class="sxs-lookup"><span data-stu-id="6613f-285">As you use more Django 'apps', you'll have static files located in multiple places.</span></span>

<span data-ttu-id="6613f-286">Uygulamayı hata ayıklama modunda çalıştırdığınızda, uygulama statik dosyaları özgün konumlarından işleme alır.</span><span class="sxs-lookup"><span data-stu-id="6613f-286">When running the application in debug mode, the application serves the static files from their original location.</span></span>

<span data-ttu-id="6613f-287">Uygulama yayın modunda çalışırken, uygulama statik dosyaları işleme **almaz**.</span><span class="sxs-lookup"><span data-stu-id="6613f-287">When running the application in release mode, the application does **not** serve the static files.</span></span> <span data-ttu-id="6613f-288">Dosyaları işleme almak web sunucusunun sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="6613f-288">It is the responsibility of the web server to serve the files.</span></span> <span data-ttu-id="6613f-289">Bu uygulama için, IIS statik dosyaları `/static` konumundan işleme alır.</span><span class="sxs-lookup"><span data-stu-id="6613f-289">For this application, IIS will serve the static files from `/static`.</span></span>

<span data-ttu-id="6613f-290">Statik dosyaların toplanması işlemi önceden toplanan dosyalar temizlenerek, dağıtım betiğinin bir parçası olarak otomatik yapılır</span><span class="sxs-lookup"><span data-stu-id="6613f-290">The collection of static files is done automatically as part of the deployment script, clearing previously collected files.</span></span> <span data-ttu-id="6613f-291">Bu, her dağıtımda meydana gelen toplamanın dağıtımı yavaşlattığı anlamına gelir ancak, potansiyel bir güvenlik sorunu önlenerek eski dosyaların kullanılmamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="6613f-291">This means the collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span></span>

<span data-ttu-id="6613f-292">Django uygulamanız için statik dosya toplamayı atlamak istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="6613f-292">If you want to skip collection of static files for your Django application:</span></span>

    \.skipDjango

<span data-ttu-id="6613f-293">Toplamayı yerel makinenizde el ile yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6613f-293">Then you'll need to do the collection manually on your local machine:</span></span>

    env\scripts\python manage.py collectstatic

<span data-ttu-id="6613f-294">Sonra, `.gitignore` içindeki `\static` klasörünü kaldırmanız ve Git deposuna eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6613f-294">Then remove the `\static` folder from `.gitignore` and add it to the Git repository.</span></span>

## <a name="troubleshooting---settings"></a><span data-ttu-id="6613f-295">Sorun giderme - Ayarlar</span><span class="sxs-lookup"><span data-stu-id="6613f-295">Troubleshooting - Settings</span></span>
<span data-ttu-id="6613f-296">Uygulama için çeşitli ayarlar`DjangoWebProject/settings.py` içinde değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="6613f-296">Various settings for the application can be changed in `DjangoWebProject/settings.py`.</span></span>

<span data-ttu-id="6613f-297">Geliştiriciye kolaylık sağlamak için hata ayıklama modu etkindir.</span><span class="sxs-lookup"><span data-stu-id="6613f-297">For developer convenience, debug mode is enabled.</span></span> <span data-ttu-id="6613f-298">Bunun olumlu bir yan etkisi, yerle olarak çalıştırırken, statik dosyaları toplamak zorunda kalmadan, resimleri ve diğer statik içeriği görebilecek olmanızdır.</span><span class="sxs-lookup"><span data-stu-id="6613f-298">One nice side effect of that is you'll be able to see images and other static content when running locally, without having to collect static files.</span></span>

<span data-ttu-id="6613f-299">Hata ayıklama modunu devre dışı bırakmak için:</span><span class="sxs-lookup"><span data-stu-id="6613f-299">To disable debug mode:</span></span>

    DEBUG = False

<span data-ttu-id="6613f-300">Hata ayıklama devre dışı bırakıldığında, `ALLOWED_HOSTS` değerinin Azure ana bilgisayar adını içerecek şekilde güncelleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="6613f-300">When debug is disabled, the value for `ALLOWED_HOSTS` needs to be updated to include the Azure host name.</span></span> <span data-ttu-id="6613f-301">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="6613f-301">For example:</span></span>

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

<span data-ttu-id="6613f-302">veya herhangi birini etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="6613f-302">or to enable any:</span></span>

    ALLOWED_HOSTS = (
        '*',
    )

<span data-ttu-id="6613f-303">Uygulamada, hata ayıklama ile yayımlama modu arasında geçiş yapma ve ana bilgisayar adını almakla uğraşmak için daha karmaşık bir şey yapmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6613f-303">In practice, you may want to do something more complex to deal with switching between debug and release mode, and getting the host name.</span></span>

<span data-ttu-id="6613f-304">Azure Portal aracılığıyla, **CONFIGURE** sayfasında, **uygulaması ayarları** bölümünde ortam değişkenlerini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6613f-304">You can set environment variables through the Azure portal **CONFIGURE** page, in the **app settings** section.</span></span>  <span data-ttu-id="6613f-305">Bu, kaynaklarda (bağlantı dizeleri, parolalar vb.) görünmesini istemeyebileceğini ya da Azure ile yerel makineniz arasında farklı ayarlamak isteyeceğiniz değerler için faydalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="6613f-305">This can be useful for setting values that you may not want to appear in the sources (connection strings, passwords, etc), or that you want to set differently between Azure and your local machine.</span></span> <span data-ttu-id="6613f-306">`settings.py` içinde, `os.getenv` kullanarak ortam değişkenlerini sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6613f-306">In `settings.py`, you can query the environment variables using `os.getenv`.</span></span>

## <a name="using-a-database"></a><span data-ttu-id="6613f-307">Bir Veritabanını Kullanma</span><span class="sxs-lookup"><span data-stu-id="6613f-307">Using a Database</span></span>
<span data-ttu-id="6613f-308">Uygulama ile birlikte gelen veritabanı bir sqlite veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="6613f-308">The database that is included with the application is a sqlite database.</span></span> <span data-ttu-id="6613f-309">Neredeyse hiçbir kurulum gerektirmediğinden, geliştirme için kullanmak üzere kullanışlı ve faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="6613f-309">This is a convenient and useful default database to use for development, as it requires almost no setup.</span></span> <span data-ttu-id="6613f-310">Veritabanı proje klasöründeki db.sqlite3 dosyasında depolanır.</span><span class="sxs-lookup"><span data-stu-id="6613f-310">The database is stored in the db.sqlite3 file in the project folder.</span></span>

<span data-ttu-id="6613f-311">Azure Django uygulamasından kullanımı kolay olan veritabanı hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="6613f-311">Azure provides database services which are easy to use from a Django application.</span></span> <span data-ttu-id="6613f-312">Django uygulamasından [SQL Database] ve [MySQL] kullanma öğreticileri, veritabanı hizmeti oluşturmak, `DjangoWebProject/settings.py` içinde veritabanı ayarlarını değiştirmek için gerekli adımları ve yükleme için gerekli kitaplıkları gösterir.</span><span class="sxs-lookup"><span data-stu-id="6613f-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show the steps necessary to create the database service, change the database settings in `DjangoWebProject/settings.py`, and the libraries required to install.</span></span>

<span data-ttu-id="6613f-313">Elbette, kendi veritabanı sunucularınızı yönetmek isterseniz, bunu Windows veya Linux Azure üzerinde çalışan sanal makineleri kullanarak yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6613f-313">Of course, if you prefer to manage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span></span>

## <a name="django-admin-interface"></a><span data-ttu-id="6613f-314">Django Yönetim Arabirimi</span><span class="sxs-lookup"><span data-stu-id="6613f-314">Django Admin Interface</span></span>
<span data-ttu-id="6613f-315">Modellerinizi oluşturmaya başladıktan sonra, veritabanını bazı verilerle doldurmak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="6613f-315">Once you start building your models, you'll want to populate the database with some data.</span></span> <span data-ttu-id="6613f-316">Etkileşimli olarak içerik ekleme ve düzenleme işlemi yapmanın kolay bir yolu Django yönetim arabirimini kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="6613f-316">An easy way to do add and edit content interactively is to use the Django administration interface.</span></span>

<span data-ttu-id="6613f-317">Yönetim arabirimi kodu, uygulama kaynaklarında açıklanmıştır ve kolayca etkinleştirebileceğiniz şekilde açıkça işaretlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="6613f-317">The code for the admin interface is commented out in the application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span></span>

<span data-ttu-id="6613f-318">Etkinleştirildikten sonra, veritabanını eşitleyin, uygulamayı çalıştırın ve `/admin` konumuna gidin.</span><span class="sxs-lookup"><span data-stu-id="6613f-318">After it's enabled, synchronize the database, run the application and navigate to `/admin`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6613f-319">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="6613f-319">Next Steps</span></span>
<span data-ttu-id="6613f-320">Visual Studio için Django ve Python Araçları hakkında daha fazla bilgi için bu bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="6613f-320">Follow these links to learn more about Django and Python Tools for Visual Studio:</span></span>

* <span data-ttu-id="6613f-321">[Django Belgeleri]</span><span class="sxs-lookup"><span data-stu-id="6613f-321">[Django Documentation]</span></span>
* <span data-ttu-id="6613f-322">[Visual Studio Belgeleri için Python Araçları]</span><span class="sxs-lookup"><span data-stu-id="6613f-322">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="6613f-323">SQL Database’i ve MySQL’i kullanma hakkında bilgi için:</span><span class="sxs-lookup"><span data-stu-id="6613f-323">For information on using SQL Database and MySQL:</span></span>

* <span data-ttu-id="6613f-324">[Visual Studio için Python Araçları ile Azure’da Django ve MySQL]</span><span class="sxs-lookup"><span data-stu-id="6613f-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="6613f-325">[Visual Studio için Python Araçları ile Azure’da Django ve SQL Veritabanı]</span><span class="sxs-lookup"><span data-stu-id="6613f-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="6613f-326">Daha fazla bilgi için bkz. [Python Geliştirici Merkezi](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="6613f-326">For more information, see the [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="6613f-327">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="6613f-327">What's changed</span></span>
* <span data-ttu-id="6613f-328">Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="6613f-328">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Visual Studio için Python Araçları ile Azure’da Django ve MySQL]: web-sites-python-ptvs-django-mysql.md
[Visual Studio için Python Araçları ile Azure’da Django ve SQL Veritabanı]: web-sites-python-ptvs-django-sql.md
[SQL Database]: web-sites-python-ptvs-django-sql.md
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
[Visual Studio Belgeleri için Python Araçları]: http://aka.ms/ptvsdocs
[Django Belgeleri]: https://www.djangoproject.com/
