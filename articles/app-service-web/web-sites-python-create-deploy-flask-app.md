---
title: "Azure'da Flask ile Web uygulamaları oluşturma"
description: "Azure üzerinde bir Python web uygulaması çalıştırmayı gösteren bir öğretici."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: b7f4ca3a-0b52-4108-90a7-f7e07ac73da0
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/20/2016
ms.author: huvalo
ms.openlocfilehash: 29457a39ee3df0bbdbc9869cdce0e14bd85b7302
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a><span data-ttu-id="721ae-103">Azure'da Flask ile Web uygulamaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="721ae-103">Creating web apps with Flask in Azure</span></span>
<span data-ttu-id="721ae-104">Bu öğretici, Python çalıştırmaya başlamak açıklar [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="721ae-104">This tutorial describes how to get started running Python in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>  <span data-ttu-id="721ae-105">Web Apps sınırlı ücretsiz barındırma ve hızlı dağıtım sağlar ve Python’u kullanmanıza olanak tanır!</span><span class="sxs-lookup"><span data-stu-id="721ae-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span>  <span data-ttu-id="721ae-106">Uygulamanız büyüdükçe, ücretli barındırmaya geçebilir ve aynı zamanda tüm diğer Azure hizmetleriyle tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="721ae-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="721ae-107">Flask web altyapısını kullanarak bir uygulama oluşturacaksınız (Bu öğretici için alternatif sürümleri bkz [Django](web-sites-python-create-deploy-django-app.md) ve [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="721ae-107">You will create an application using the Flask web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span>  <span data-ttu-id="721ae-108">Azure galerisinden Web sitesi oluşturma, Git dağıtımı ayarlayacak ve depoyu yerel olarak kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="721ae-108">You will create the website from the Azure gallery, set up Git deployment, and clone the repository locally.</span></span>  <span data-ttu-id="721ae-109">Sonra, uygulamayı yerel olarak çalıştıracak, değişiklikler yapacak, yürütecek ve bunları Azure'a ileteceksiniz.</span><span class="sxs-lookup"><span data-stu-id="721ae-109">Then you will run the application locally, make changes, commit and push them to Azure.</span></span>  <span data-ttu-id="721ae-110">Öğretici, Windows veya Mac/Linux’ta bunun nasıl yapıldığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="721ae-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="721ae-111">Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="721ae-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="721ae-112">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="721ae-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="721ae-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="721ae-113">Prerequisites</span></span>
* <span data-ttu-id="721ae-114">Windows, Mac veya Linux</span><span class="sxs-lookup"><span data-stu-id="721ae-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="721ae-115">Python 2.7 ya da 3.4</span><span class="sxs-lookup"><span data-stu-id="721ae-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="721ae-116">setuptools, pip, virtualenv (yalnızca Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="721ae-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="721ae-117">Git</span><span class="sxs-lookup"><span data-stu-id="721ae-117">Git</span></span>
* <span data-ttu-id="721ae-118">[Visual Studio için Python Araçları][Visual Studio için Python Araçları] (PTVS) - Not: Bu özellik isteğe bağlıdır</span><span class="sxs-lookup"><span data-stu-id="721ae-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="721ae-119">**Not**: TFS yayımlama şu anda Python projeleri için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="721ae-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="721ae-120">Windows</span><span class="sxs-lookup"><span data-stu-id="721ae-120">Windows</span></span>
<span data-ttu-id="721ae-121">Python 2.7 ya da 3.4 yüklü (32 bit) değilse, Web Platformu Yükleyicisi'ni kullanarak [Python 2.7 için Azure SDK] veya [Python 3.4 için Azure SDK]’yı yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="721ae-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span>  <span data-ttu-id="721ae-122">Bu, Python’un 32 bit sürümünü, setuptools, PIP, virtualenv vb.yükler (32 bit Python, Azure ana makinelerde yüklü olandır).</span><span class="sxs-lookup"><span data-stu-id="721ae-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span>  <span data-ttu-id="721ae-123">Alternatif olarak, Python’u [python.org] adresinden edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="721ae-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="721ae-124">Git için, [Windows için Git] veya [Windows için GitHub]’ı öneririz.</span><span class="sxs-lookup"><span data-stu-id="721ae-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span>  <span data-ttu-id="721ae-125">Visual Studio kullanıyorsanız, tümleşik Git desteğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="721ae-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="721ae-126">Ayrıca [Visual Studio için Python Araçları 2.2]’yi yüklemenizi öneririz </span><span class="sxs-lookup"><span data-stu-id="721ae-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span>  <span data-ttu-id="721ae-127">Bu isteğe bağlıdır, ancak ücretsiz Visual Studio Community 2013 veya Web için Visual Studio Express 2013 içeren [Visual Studio] varsa, bu size mükemmel bir Python IDE verir.</span><span class="sxs-lookup"><span data-stu-id="721ae-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="721ae-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="721ae-128">Mac/Linux</span></span>
<span data-ttu-id="721ae-129">Python ve Git sizde zaten yüklü olmalıdır, ancak Python 2.7 veya 3.4 olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="721ae-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-create-on-the-azure-portal"></a><span data-ttu-id="721ae-130">Web uygulaması oluşturma Azure portalında</span><span class="sxs-lookup"><span data-stu-id="721ae-130">Web app create on the Azure Portal</span></span>
<span data-ttu-id="721ae-131">Uygulamanızı oluşturmanın ilk adımı, [Azure Portal](https://portal.azure.com) aracılığıyla web uygulaması oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="721ae-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span> 

1. <span data-ttu-id="721ae-132">Azure Portal’da oturum açın ve sol alt köşede **NEW** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="721ae-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span> 
2. <span data-ttu-id="721ae-133">**Web + Mobil**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="721ae-133">Click **Web + Mobile**.</span></span>
3. <span data-ttu-id="721ae-134">Arama kutusuna, "python" yazın.</span><span class="sxs-lookup"><span data-stu-id="721ae-134">In the search box, type "python".</span></span>
4. <span data-ttu-id="721ae-135">Arama sonuçlarında seçin **Flask**, ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="721ae-135">In the search results, select **Flask**, then click **Create**.</span></span>
5. <span data-ttu-id="721ae-136">Yeni bir uygulama hizmeti planı ve yeni bir kaynak grubu oluşturma gibi yeni Flask uygulamasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="721ae-136">Configure the new Flask app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="721ae-137">Sonra, **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="721ae-137">Then, click **Create**.</span></span>
6. <span data-ttu-id="721ae-138">Yeni oluşturulan web uygulamanız için, [Azure Uygulama Hizmeti’nde Yerel Git Dağıtımı](app-service-deploy-local-git.md) başlığındaki yönergeleri izleyerek Git yayımlamayı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="721ae-138">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="721ae-139">Uygulamaya Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="721ae-139">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="721ae-140">Git deposu içeriği</span><span class="sxs-lookup"><span data-stu-id="721ae-140">Git repository contents</span></span>
<span data-ttu-id="721ae-141">Burada, sonraki bölümde kopyalayacağımız, ilk Git deposunda bulacağınız dosyalara bir genel bakış yer alır.</span><span class="sxs-lookup"><span data-stu-id="721ae-141">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

<span data-ttu-id="721ae-142">Uygulama için ana kaynaklar</span><span class="sxs-lookup"><span data-stu-id="721ae-142">Main sources for the application.</span></span>  <span data-ttu-id="721ae-143">Ana düzenle birlikte 3 sayfadan (dizin, hakkında, iletişim) oluşur.</span><span class="sxs-lookup"><span data-stu-id="721ae-143">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="721ae-144">Statik içerik ve betikler bootstrap, jquery, modernize ve yanıtı içerir.</span><span class="sxs-lookup"><span data-stu-id="721ae-144">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \runserver.py

<span data-ttu-id="721ae-145">Yerel Geliştirme Sunucusu desteği.</span><span class="sxs-lookup"><span data-stu-id="721ae-145">Local development server support.</span></span> <span data-ttu-id="721ae-146">Uygulamayı yerel olarak çalıştırmak için bunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="721ae-146">Use this to run the application locally.</span></span>

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

<span data-ttu-id="721ae-147">[Visual Studio için Python Araçları] ile birlikte kullanmak için proje dosyaları.</span><span class="sxs-lookup"><span data-stu-id="721ae-147">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="721ae-148">Sanal ortamlar için IIS proxy ve PTVS uzaktan hata ayıklama desteği</span><span class="sxs-lookup"><span data-stu-id="721ae-148">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="721ae-149">Bu uygulamaya dış paketler gerekir.</span><span class="sxs-lookup"><span data-stu-id="721ae-149">External packages needed by this application.</span></span> <span data-ttu-id="721ae-150">Dağıtım betiği pip bu dosyada listelenen paketleri pip yükler.</span><span class="sxs-lookup"><span data-stu-id="721ae-150">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="721ae-151">IIS yapılandırma dosyaları.</span><span class="sxs-lookup"><span data-stu-id="721ae-151">IIS configuration files.</span></span>  <span data-ttu-id="721ae-152">Dağıtım betiği, uygun web.x.y.config’i kullanır ve bunu web.config olarak kopyalar.</span><span class="sxs-lookup"><span data-stu-id="721ae-152">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="721ae-153">İsteğe bağlı dosyalar - Dağıtımı özelleştirme</span><span class="sxs-lookup"><span data-stu-id="721ae-153">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="721ae-154">İsteğe bağlı dosyalar - Python çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="721ae-154">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="721ae-155">Sunucu üzerindeki ek dosyalar</span><span class="sxs-lookup"><span data-stu-id="721ae-155">Additional files on server</span></span>
<span data-ttu-id="721ae-156">Bazı dosyalar sunucuda yer alır ancak git deposuna eklenmez.</span><span class="sxs-lookup"><span data-stu-id="721ae-156">Some files exist on the server but are not added to the git repository.</span></span>  <span data-ttu-id="721ae-157">Bunlar dağıtım betiği tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="721ae-157">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="721ae-158">IIS yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="721ae-158">IIS configuration file.</span></span>  <span data-ttu-id="721ae-159">Her dağıtımda web.x.y.config tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="721ae-159">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="721ae-160">Python sanal ortamı.</span><span class="sxs-lookup"><span data-stu-id="721ae-160">Python virtual environment.</span></span>  <span data-ttu-id="721ae-161">Uygulamasında uyumlu sanal ortam zaten yoksa dağıtım ırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="721ae-161">Created during deployment if a compatible virtual environment doesn't already exist on the app.</span></span>  <span data-ttu-id="721ae-162">Requirements.txt içinde listelenen paketler pip yüklüdür, ancak paketler zaten yüklü ise pip yüklemeyi atlar.</span><span class="sxs-lookup"><span data-stu-id="721ae-162">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="721ae-163">Sonraki 3 bölümde farklı 3 ortamda web uygulaması geliştirmeye devam etme açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="721ae-163">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="721ae-164">Windows, Visual Studio için Python Araçları ile</span><span class="sxs-lookup"><span data-stu-id="721ae-164">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="721ae-165">Windows, komut satırı ile</span><span class="sxs-lookup"><span data-stu-id="721ae-165">Windows, with command line</span></span>
* <span data-ttu-id="721ae-166">Mac/Linux, komut satırı ile</span><span class="sxs-lookup"><span data-stu-id="721ae-166">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="721ae-167">Web uygulaması geliştirme - Windows - Visual Studio için Python Araçları</span><span class="sxs-lookup"><span data-stu-id="721ae-167">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="721ae-168">Depoyu kopyalama</span><span class="sxs-lookup"><span data-stu-id="721ae-168">Clone the repository</span></span>
<span data-ttu-id="721ae-169">İlk olarak, Azure Portal'da sağlanan URL'yi kullanarak depoyu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="721ae-169">First, clone the repository using the URL provided on the Azure Portal.</span></span> <span data-ttu-id="721ae-170">Daha fazla bilgi için bkz. [Azure Uygulama Hizmeti’nde Yerel Git Dağıtımı](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="721ae-170">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="721ae-171">Depo kök dizininde bulunan çözüm dosyasını (.sln) açın.</span><span class="sxs-lookup"><span data-stu-id="721ae-171">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="721ae-172">Sanal ortamı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="721ae-172">Create virtual environment</span></span>
<span data-ttu-id="721ae-173">Şimdi, yerel geliştirme için sanal bir ortam oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="721ae-173">Now we'll create a virtual environment for local development.</span></span>  <span data-ttu-id="721ae-174">Sağ **Python Ortamları**’na sağ tıklayın **Sanal Ortam Ekle...** seçeneğini seçin.</span><span class="sxs-lookup"><span data-stu-id="721ae-174">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="721ae-175">Ortam adının `env` olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="721ae-175">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="721ae-176">Temel yorumlayıcıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="721ae-176">Select the base interpreter.</span></span>  <span data-ttu-id="721ae-177">Web uygulamanız için seçilen Python ile aynı sürümü kullandığınızdan emin olun (runtime.txt içinde veya Azure Portal’da uygulamanızın **Uygulama Ayarları** dikey penceresinde).</span><span class="sxs-lookup"><span data-stu-id="721ae-177">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="721ae-178">Paketleri indirme ve yükleme seçeneğinin işaretli olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="721ae-178">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="721ae-179">**Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="721ae-179">Click **Create**.</span></span>  <span data-ttu-id="721ae-180">Bu, sanal ortamı oluşturur ve requirements.txt içinde listelenen bağımlılıkları yükler.</span><span class="sxs-lookup"><span data-stu-id="721ae-180">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="721ae-181">Geliştirme sunucusu kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="721ae-181">Run using development server</span></span>
<span data-ttu-id="721ae-182">Hata ayıklamayı başlatmak için F5 tuşuna basın, böylece web tarayıcınız yerel olarak çalışan sayfaya otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="721ae-182">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

<span data-ttu-id="721ae-183">Kaynaklarda kesme noktalarını ayarlayabilir, gözcü pencerelerini kullanabilirsiniz vb.  Çeşitli özellikler hakkında daha fazla bilgi için bkz. [Visual Studio Belgeleri için Python Araçları].</span><span class="sxs-lookup"><span data-stu-id="721ae-183">You can set breakpoints in the sources, use the watch windows, etc.  See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="721ae-184">Değişiklik yapma</span><span class="sxs-lookup"><span data-stu-id="721ae-184">Make changes</span></span>
<span data-ttu-id="721ae-185">Şimdi uygulama kaynakları ve/veya şablonlarında değişiklikler yapmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="721ae-185">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="721ae-186">Değişikliklerinizi test ettikten sonra bunları Git deposuna kaydedin:</span><span class="sxs-lookup"><span data-stu-id="721ae-186">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a><span data-ttu-id="721ae-187">Daha fazla paket yükleme</span><span class="sxs-lookup"><span data-stu-id="721ae-187">Install more packages</span></span>
<span data-ttu-id="721ae-188">Uygulamanızın Python ve Flask ötesinde bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="721ae-188">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="721ae-189">Pip kullanarak ek paketleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="721ae-189">You can install additional packages using pip.</span></span>  <span data-ttu-id="721ae-190">Bir paketi yüklemek için, sanal ortamda sağ tıklayıp **Python Paketini Yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="721ae-190">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="721ae-191">Örneğin, size Azure Storage, Service Bus ve diğer Azure hizmetleri için erişim imkanı sağlayan, Python için Azure SDK'yı yüklemek için şunu girin: `azure`</span><span class="sxs-lookup"><span data-stu-id="721ae-191">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

<span data-ttu-id="721ae-192">Sanal ortamda sağ tıklayıp **requirements.txt oluştur**’u seçerek requirements.txt dosyasını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="721ae-192">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="721ae-193">Ardından, requirements.txt dosyasındaki değişiklikleri Git deposuna uygulayın.</span><span class="sxs-lookup"><span data-stu-id="721ae-193">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="721ae-194">Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="721ae-194">Deploy to Azure</span></span>
<span data-ttu-id="721ae-195">Bir dağıtımı tetiklemek için tıklatın **Eşitle** veya **İlet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="721ae-195">To trigger a deployment, click on **Sync** or **Push**.</span></span>  <span data-ttu-id="721ae-196">Eşitleme, iletme ve çekme işlemini yapar.</span><span class="sxs-lookup"><span data-stu-id="721ae-196">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

<span data-ttu-id="721ae-197">Sanal ortam, yükleme paketleri vb. oluşturacağında, ilk dağıtımın gerçekleşmesi biraz zaman alır.</span><span class="sxs-lookup"><span data-stu-id="721ae-197">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="721ae-198">Visual Studio dağıtımın ilerleme durumunu göstermez.</span><span class="sxs-lookup"><span data-stu-id="721ae-198">Visual Studio doesn't show the progress of the deployment.</span></span>  <span data-ttu-id="721ae-199">Çıktıyı gözden geçirmek isterseniz, üzerinde bakın [Sorun Giderme - Dağıtım](#troubleshooting-deployment)’daki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="721ae-199">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="721ae-200">Yaptığınız değişiklikleri görmek için Azure URL'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="721ae-200">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="721ae-201">Web uygulaması geliştirme - Windows - komut satırı</span><span class="sxs-lookup"><span data-stu-id="721ae-201">Web app development - Windows - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="721ae-202">Depoyu kopyalama</span><span class="sxs-lookup"><span data-stu-id="721ae-202">Clone the repository</span></span>
<span data-ttu-id="721ae-203">İlk olarak, Azure Portal'da sağlanan URL'yi kullanarak depoyu kopyalayın ve uzak olarak Azure deposunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="721ae-203">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="721ae-204">Daha fazla bilgi için bkz. [Azure Uygulama Hizmeti’nde Yerel Git Dağıtımı](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="721ae-204">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="721ae-205">Sanal ortamı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="721ae-205">Create virtual environment</span></span>
<span data-ttu-id="721ae-206">Geliştirme amacına yönelik yeni bir sanal ortam oluşturacağız (bunu depoya eklemeyin).</span><span class="sxs-lookup"><span data-stu-id="721ae-206">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span>  <span data-ttu-id="721ae-207">Uygulama üzerinde çalışan her geliştiricinin yerel olarak kendininkini oluşturacağı şekilde, Python’daki sanal ortamlar yeniden yerleştirilebilir değildir.</span><span class="sxs-lookup"><span data-stu-id="721ae-207">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="721ae-208">Web uygulamanız için seçilen Python ile aynı sürümü kullandığınızdan emin olun (runtime.txt içinde veya Azure Portal’da uygulamanızın **Uygulama Ayarları** dikey penceresinde).</span><span class="sxs-lookup"><span data-stu-id="721ae-208">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="721ae-209">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="721ae-209">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="721ae-210">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="721ae-210">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="721ae-211">Uygulamanız için gereken herhangi bir dış paketi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="721ae-211">Install any external packages required by your application.</span></span> <span data-ttu-id="721ae-212">Sanal ortamınıza paketleri yüklemek için depo kökündeki requirements.txt dosyasını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="721ae-212">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="721ae-213">Geliştirme sunucusu kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="721ae-213">Run using development server</span></span>
<span data-ttu-id="721ae-214">Aşağıdaki komutla bir geliştirme sunucusu altında uygulamayı başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="721ae-214">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python runserver.py

<span data-ttu-id="721ae-215">Konsol URL’yi ve sunucunun dinlediği bağlantı noktasını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="721ae-215">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

<span data-ttu-id="721ae-216">Sonra, bu URL için web tarayıcınızı açın.</span><span class="sxs-lookup"><span data-stu-id="721ae-216">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="721ae-217">Değişiklik yapma</span><span class="sxs-lookup"><span data-stu-id="721ae-217">Make changes</span></span>
<span data-ttu-id="721ae-218">Şimdi uygulama kaynakları ve/veya şablonlarında değişiklikler yapmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="721ae-218">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="721ae-219">Değişikliklerinizi test ettikten sonra bunları Git deposuna kaydedin:</span><span class="sxs-lookup"><span data-stu-id="721ae-219">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="721ae-220">Daha fazla paket yükleme</span><span class="sxs-lookup"><span data-stu-id="721ae-220">Install more packages</span></span>
<span data-ttu-id="721ae-221">Uygulamanızın Python ve Flask ötesinde bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="721ae-221">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="721ae-222">Pip kullanarak ek paketleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="721ae-222">You can install additional packages using pip.</span></span>  <span data-ttu-id="721ae-223">Örneğin, size Azure Storage, Service Bus ve diğer Azure hizmetleri için erişim imkanı sağlayan, Python için Azure SDK'yı yüklemek için aşağıdakileri yazın:</span><span class="sxs-lookup"><span data-stu-id="721ae-223">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="721ae-224">Requirements.txt dosyasını güncelleştirdiğinizden emin olun:</span><span class="sxs-lookup"><span data-stu-id="721ae-224">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="721ae-225">Değişiklikleri uygulayın:</span><span class="sxs-lookup"><span data-stu-id="721ae-225">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="721ae-226">Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="721ae-226">Deploy to Azure</span></span>
<span data-ttu-id="721ae-227">Bir dağıtımı tetiklemek için, değişiklikleri Azure’a gönderin:</span><span class="sxs-lookup"><span data-stu-id="721ae-227">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="721ae-228">Sanal ortam oluşturma, paketleri yükleme, web.config oluşturma dahil dağıtım betiği çıktısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="721ae-228">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="721ae-229">Yaptığınız değişiklikleri görmek için Azure URL'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="721ae-229">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="721ae-230">Web uygulaması geliştirme - Mac/Linux - komut satırı</span><span class="sxs-lookup"><span data-stu-id="721ae-230">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="721ae-231">Depoyu kopyalama</span><span class="sxs-lookup"><span data-stu-id="721ae-231">Clone the repository</span></span>
<span data-ttu-id="721ae-232">İlk olarak, Azure Portal'da sağlanan URL'yi kullanarak depoyu kopyalayın ve uzak olarak Azure deposunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="721ae-232">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="721ae-233">Daha fazla bilgi için bkz. [Azure Uygulama Hizmeti’nde Yerel Git Dağıtımı](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="721ae-233">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="721ae-234">Sanal ortamı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="721ae-234">Create virtual environment</span></span>
<span data-ttu-id="721ae-235">Geliştirme amacına yönelik yeni bir sanal ortam oluşturacağız (bunu depoya eklemeyin).</span><span class="sxs-lookup"><span data-stu-id="721ae-235">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span>  <span data-ttu-id="721ae-236">Uygulama üzerinde çalışan her geliştiricinin yerel olarak kendininkini oluşturacağı şekilde, Python’daki sanal ortamlar yeniden yerleştirilebilir değildir.</span><span class="sxs-lookup"><span data-stu-id="721ae-236">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="721ae-237">Web uygulamanız için seçilen Python ile aynı sürümü kullandığınızdan emin olun (runtime.txt içinde veya Azure Portal’da uygulamanızın **Uygulama Ayarları** dikey penceresinde).</span><span class="sxs-lookup"><span data-stu-id="721ae-237">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="721ae-238">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="721ae-238">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="721ae-239">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="721ae-239">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="721ae-240">veya pyvenv env</span><span class="sxs-lookup"><span data-stu-id="721ae-240">or pyvenv env</span></span>

<span data-ttu-id="721ae-241">Uygulamanız için gereken herhangi bir dış paketi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="721ae-241">Install any external packages required by your application.</span></span> <span data-ttu-id="721ae-242">Sanal ortamınıza paketleri yüklemek için depo kökündeki requirements.txt dosyasını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="721ae-242">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="721ae-243">Geliştirme sunucusu kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="721ae-243">Run using development server</span></span>
<span data-ttu-id="721ae-244">Aşağıdaki komutla bir geliştirme sunucusu altında uygulamayı başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="721ae-244">You can launch the application under a development server with the following command:</span></span>

    env/bin/python runserver.py

<span data-ttu-id="721ae-245">Konsol URL’yi ve sunucunun dinlediği bağlantı noktasını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="721ae-245">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

<span data-ttu-id="721ae-246">Sonra, bu URL için web tarayıcınızı açın.</span><span class="sxs-lookup"><span data-stu-id="721ae-246">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="721ae-247">Değişiklik yapma</span><span class="sxs-lookup"><span data-stu-id="721ae-247">Make changes</span></span>
<span data-ttu-id="721ae-248">Şimdi uygulama kaynakları ve/veya şablonlarında değişiklikler yapmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="721ae-248">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="721ae-249">Değişikliklerinizi test ettikten sonra bunları Git deposuna kaydedin:</span><span class="sxs-lookup"><span data-stu-id="721ae-249">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="721ae-250">Daha fazla paket yükleme</span><span class="sxs-lookup"><span data-stu-id="721ae-250">Install more packages</span></span>
<span data-ttu-id="721ae-251">Uygulamanızın Python ve Flask ötesinde bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="721ae-251">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="721ae-252">Pip kullanarak ek paketleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="721ae-252">You can install additional packages using pip.</span></span>  <span data-ttu-id="721ae-253">Örneğin, size Azure Storage, Service Bus ve diğer Azure hizmetleri için erişim imkanı sağlayan, Python için Azure SDK'yı yüklemek için aşağıdakileri yazın:</span><span class="sxs-lookup"><span data-stu-id="721ae-253">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="721ae-254">Requirements.txt dosyasını güncelleştirdiğinizden emin olun:</span><span class="sxs-lookup"><span data-stu-id="721ae-254">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="721ae-255">Değişiklikleri uygulayın:</span><span class="sxs-lookup"><span data-stu-id="721ae-255">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="721ae-256">Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="721ae-256">Deploy to Azure</span></span>
<span data-ttu-id="721ae-257">Bir dağıtımı tetiklemek için, değişiklikleri Azure’a gönderin:</span><span class="sxs-lookup"><span data-stu-id="721ae-257">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="721ae-258">Sanal ortam oluşturma, paketleri yükleme, web.config oluşturma dahil dağıtım betiği çıktısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="721ae-258">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="721ae-259">Yaptığınız değişiklikleri görmek için Azure URL'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="721ae-259">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="721ae-260">Sorun giderme - Paket Yükleme</span><span class="sxs-lookup"><span data-stu-id="721ae-260">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="721ae-261">Sorun giderme - Sanal Ortam</span><span class="sxs-lookup"><span data-stu-id="721ae-261">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="721ae-262">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="721ae-262">Next Steps</span></span>
<span data-ttu-id="721ae-263">Visual Studio için Flask ve Python araçları hakkında daha fazla bilgi için aşağıdaki bağlantıları izleyin:</span><span class="sxs-lookup"><span data-stu-id="721ae-263">Follow these links to learn more about Flask and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="721ae-264">[Flask belgeleri]</span><span class="sxs-lookup"><span data-stu-id="721ae-264">[Flask Documentation]</span></span>
* <span data-ttu-id="721ae-265">[Visual Studio Belgeleri için Python Araçları]</span><span class="sxs-lookup"><span data-stu-id="721ae-265">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="721ae-266">Azure tablo depolaması ve MongoDB kullanma hakkında daha fazla bilgi için:</span><span class="sxs-lookup"><span data-stu-id="721ae-266">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="721ae-267">[Flask ve Visual Studio için Python araçları ile azure'da MongoDB]</span><span class="sxs-lookup"><span data-stu-id="721ae-267">[Flask and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="721ae-268">[Flask ve Visual Studio için Python araçları ile azure'da Azure tablo depolaması]</span><span class="sxs-lookup"><span data-stu-id="721ae-268">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="721ae-269">Daha fazla bilgi için Ayrıca bkz. [Python Geliştirici Merkezi](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="721ae-269">For more information, see also the [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="721ae-270">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="721ae-270">What's changed</span></span>
* <span data-ttu-id="721ae-271">Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="721ae-271">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="721ae-272">[Flask ve Visual Studio için Python araçları ile azure'da MongoDB]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure</span><span class="sxs-lookup"><span data-stu-id="721ae-272">[Flask and MongoDB on Azure with Python Tools for Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure</span></span>
<span data-ttu-id="721ae-273">[Flask ve Visual Studio için Python araçları ile azure'da Azure tablo depolaması]: web-sites-python-ptvs-flask-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="721ae-273">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-flask-table-storage.md</span></span>

<!--External Link references-->
<span data-ttu-id="721ae-274">[Python 2.7 için Azure SDK]: http://go.microsoft.com/fwlink/?linkid=254281</span><span class="sxs-lookup"><span data-stu-id="721ae-274">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span></span>
<span data-ttu-id="721ae-275">[Python 3.4 için Azure SDK]: http://go.microsoft.com/fwlink/?linkid=516990</span><span class="sxs-lookup"><span data-stu-id="721ae-275">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span></span>
<span data-ttu-id="721ae-276">[python.org]: http://www.python.org/</span><span class="sxs-lookup"><span data-stu-id="721ae-276">[python.org]: http://www.python.org/</span></span>
<span data-ttu-id="721ae-277">[Windows için Git]: http://msysgit.github.io/</span><span class="sxs-lookup"><span data-stu-id="721ae-277">[Git for Windows]: http://msysgit.github.io/</span></span>
<span data-ttu-id="721ae-278">[Windows için GitHub]: https://windows.github.com/</span><span class="sxs-lookup"><span data-stu-id="721ae-278">[GitHub for Windows]: https://windows.github.com/</span></span>
<span data-ttu-id="721ae-279">[Visual Studio için Python Araçları]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="721ae-279">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="721ae-280">[Visual Studio için Python Araçları 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="721ae-280">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="721ae-281">[Visual Studio]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="721ae-281">[Visual Studio]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="721ae-282">[Visual Studio Belgeleri için Python Araçları]: http://aka.ms/ptvsdocs</span><span class="sxs-lookup"><span data-stu-id="721ae-282">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs</span></span>
<span data-ttu-id="721ae-283">[Flask belgeleri]: http://flask.pocoo.org/</span><span class="sxs-lookup"><span data-stu-id="721ae-283">[Flask Documentation]: http://flask.pocoo.org/</span></span> 

