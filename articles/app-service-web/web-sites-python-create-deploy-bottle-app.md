---
title: Azure'da Bottle uygulamalarla Python web
description: "Azure App Service Web Apps’te bir Python web uygulaması çalıştırmayı gösteren bir öğretici."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 84f043b8-9d05-479f-a9d0-d0d9a32a0bb9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: de5831defc395cd8a4033be8c1fc5dc6cbc9d683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a><span data-ttu-id="09684-103">Azure'da Bottle ile Web uygulamaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="09684-103">Creating web apps with Bottle in Azure</span></span>
<span data-ttu-id="09684-104">Bu öğretici, Azure App Service Web uygulamalarında Python çalıştırmaya başlamak açıklar.</span><span class="sxs-lookup"><span data-stu-id="09684-104">This tutorial describes how to get started running Python in Azure App Service Web Apps.</span></span> <span data-ttu-id="09684-105">Web Apps sınırlı ücretsiz barındırma ve hızlı dağıtım sağlar ve Python’u kullanmanıza olanak tanır!</span><span class="sxs-lookup"><span data-stu-id="09684-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="09684-106">Uygulamanız büyüdükçe, ücretli barındırmaya geçebilir ve aynı zamanda tüm diğer Azure hizmetleriyle tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09684-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="09684-107">Bottle web çerçevesi kullanarak bir web uygulaması oluşturacaksınız (Bu öğretici için alternatif sürümleri bkz [Django](web-sites-python-create-deploy-django-app.md) ve [Flask](web-sites-python-create-deploy-flask-app.md)).</span><span class="sxs-lookup"><span data-stu-id="09684-107">You will create a web app using the Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span></span> <span data-ttu-id="09684-108">Azure Marketi'nde bir web uygulaması oluşturacak, Git dağıtımı ayarlayacak ve depoyu yerel olarak kopyalayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="09684-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="09684-109">Sonra web uygulamasını yerel olarak çalışacak, değişiklik, yürütme ve bunları için gönderme [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="09684-109">Then you will run the web app locally, make changes, commit and push them to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="09684-110">Öğretici, Windows veya Mac/Linux’ta bunun nasıl yapıldığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="09684-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="09684-111">Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="09684-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="09684-112">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="09684-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="09684-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="09684-113">Prerequisites</span></span>
* <span data-ttu-id="09684-114">Windows, Mac veya Linux</span><span class="sxs-lookup"><span data-stu-id="09684-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="09684-115">Python 2.7 ya da 3.4</span><span class="sxs-lookup"><span data-stu-id="09684-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="09684-116">setuptools, pip, virtualenv (yalnızca Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="09684-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="09684-117">Git</span><span class="sxs-lookup"><span data-stu-id="09684-117">Git</span></span>
* <span data-ttu-id="09684-118">[Visual Studio için Python Araçları 2.2][Visual Studio için Python Araçları 2.2] (PTVS) - Not: Bu seçenek isteğe bağlıdır</span><span class="sxs-lookup"><span data-stu-id="09684-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="09684-119">**Not**: TFS yayımlama şu anda Python projeleri için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="09684-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="09684-120">Windows</span><span class="sxs-lookup"><span data-stu-id="09684-120">Windows</span></span>
<span data-ttu-id="09684-121">Python 2.7 ya da 3.4 yüklü (32 bit) değilse, Web Platformu Yükleyicisi'ni kullanarak [Python 2.7 için Azure SDK] veya [Python 3.4 için Azure SDK]’yı yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="09684-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="09684-122">Bu, Python’un 32 bit sürümünü, setuptools, PIP, virtualenv vb.yükler (32 bit Python, Azure ana makinelerde yüklü olandır).</span><span class="sxs-lookup"><span data-stu-id="09684-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="09684-123">Alternatif olarak, Python’u [python.org] adresinden edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09684-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="09684-124">Git için, [Windows için Git] veya [Windows için GitHub]’ı öneririz.</span><span class="sxs-lookup"><span data-stu-id="09684-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="09684-125">Visual Studio kullanıyorsanız, tümleşik Git desteğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09684-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="09684-126">Ayrıca [Visual Studio için Python Araçları 2.2]’yi yüklemenizi öneririz </span><span class="sxs-lookup"><span data-stu-id="09684-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="09684-127">Bu isteğe bağlıdır, ancak ücretsiz Visual Studio Community 2013 veya Web için Visual Studio Express 2013 içeren [Visual Studio] varsa, bu size mükemmel bir Python IDE verir.</span><span class="sxs-lookup"><span data-stu-id="09684-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="09684-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="09684-128">Mac/Linux</span></span>
<span data-ttu-id="09684-129">Python ve Git sizde zaten yüklü olmalıdır, ancak Python 2.7 veya 3.4 olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="09684-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-the-azure-portal"></a><span data-ttu-id="09684-130">Azure Portal'da Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="09684-130">Web app creation on the Azure Portal</span></span>
<span data-ttu-id="09684-131">Uygulamanızı oluşturmanın ilk adımı, [Azure Portal](https://portal.azure.com) aracılığıyla web uygulaması oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="09684-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>  

1. <span data-ttu-id="09684-132">Azure Portal’da oturum açın ve sol alt köşede **NEW** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="09684-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span> 
2. <span data-ttu-id="09684-133">Arama kutusuna, "python" yazın.</span><span class="sxs-lookup"><span data-stu-id="09684-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="09684-134">Arama sonuçlarında seçin **Bottle**, ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="09684-134">In the search results, select **Bottle**, then click **Create**.</span></span>
4. <span data-ttu-id="09684-135">Yeni bir uygulama hizmeti planı ve yeni bir kaynak grubu oluşturma gibi yeni Bottle uygulamasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="09684-135">Configure the new Bottle app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="09684-136">Sonra, **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="09684-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="09684-137">Yeni oluşturulan web uygulamanız için, [Azure Uygulama Hizmeti’nde Yerel Git Dağıtımı](app-service-deploy-local-git.md) başlığındaki yönergeleri izleyerek Git yayımlamayı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="09684-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="09684-138">Uygulamaya Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="09684-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="09684-139">Git deposu içeriği</span><span class="sxs-lookup"><span data-stu-id="09684-139">Git repository contents</span></span>
<span data-ttu-id="09684-140">Burada, sonraki bölümde kopyalayacağımız, ilk Git deposunda bulacağınız dosyalara bir genel bakış yer alır.</span><span class="sxs-lookup"><span data-stu-id="09684-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

<span data-ttu-id="09684-141">Uygulama için ana kaynaklar</span><span class="sxs-lookup"><span data-stu-id="09684-141">Main sources for the application.</span></span> <span data-ttu-id="09684-142">Ana düzenle birlikte 3 sayfadan (dizin, hakkında, iletişim) oluşur.</span><span class="sxs-lookup"><span data-stu-id="09684-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="09684-143">Statik içerik ve betikler bootstrap, jquery, modernize ve yanıtı içerir.</span><span class="sxs-lookup"><span data-stu-id="09684-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \app.py

<span data-ttu-id="09684-144">Yerel Geliştirme Sunucusu desteği.</span><span class="sxs-lookup"><span data-stu-id="09684-144">Local development server support.</span></span> <span data-ttu-id="09684-145">Uygulamayı yerel olarak çalıştırmak için bunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="09684-145">Use this to run the application locally.</span></span>

    \BottleWebProject.pyproj
    \BottleWebProject.sln

<span data-ttu-id="09684-146">[Visual Studio için Python Araçları] ile birlikte kullanmak için proje dosyaları.</span><span class="sxs-lookup"><span data-stu-id="09684-146">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="09684-147">Sanal ortamlar için IIS proxy ve PTVS uzaktan hata ayıklama desteği</span><span class="sxs-lookup"><span data-stu-id="09684-147">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="09684-148">Bu uygulamaya dış paketler gerekir.</span><span class="sxs-lookup"><span data-stu-id="09684-148">External packages needed by this application.</span></span> <span data-ttu-id="09684-149">Dağıtım betiği pip bu dosyada listelenen paketleri pip yükler.</span><span class="sxs-lookup"><span data-stu-id="09684-149">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="09684-150">IIS yapılandırma dosyaları.</span><span class="sxs-lookup"><span data-stu-id="09684-150">IIS configuration files.</span></span> <span data-ttu-id="09684-151">Dağıtım betiği, uygun web.x.y.config’i kullanır ve bunu web.config olarak kopyalar.</span><span class="sxs-lookup"><span data-stu-id="09684-151">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="09684-152">İsteğe bağlı dosyalar - Dağıtımı özelleştirme</span><span class="sxs-lookup"><span data-stu-id="09684-152">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="09684-153">İsteğe bağlı dosyalar - Python çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="09684-153">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="09684-154">Sunucu üzerindeki ek dosyalar</span><span class="sxs-lookup"><span data-stu-id="09684-154">Additional files on server</span></span>
<span data-ttu-id="09684-155">Bazı dosyalar sunucuda yer alır ancak git deposuna eklenmez.</span><span class="sxs-lookup"><span data-stu-id="09684-155">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="09684-156">Bunlar dağıtım betiği tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="09684-156">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="09684-157">IIS yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="09684-157">IIS configuration file.</span></span> <span data-ttu-id="09684-158">Her dağıtımda web.x.y.config tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="09684-158">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="09684-159">Python sanal ortamı.</span><span class="sxs-lookup"><span data-stu-id="09684-159">Python virtual environment.</span></span> <span data-ttu-id="09684-160">Web uygulamasında uyumlu sanal ortam zaten yoksa, dağıtım ırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="09684-160">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span>  <span data-ttu-id="09684-161">Requirements.txt içinde listelenen paketler pip yüklüdür, ancak paketler zaten yüklü ise pip yüklemeyi atlar.</span><span class="sxs-lookup"><span data-stu-id="09684-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="09684-162">Sonraki 3 bölümde farklı 3 ortamda web uygulaması geliştirmeye devam etme açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="09684-162">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="09684-163">Windows, Visual Studio için Python Araçları ile</span><span class="sxs-lookup"><span data-stu-id="09684-163">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="09684-164">Windows, komut satırı ile</span><span class="sxs-lookup"><span data-stu-id="09684-164">Windows, with command line</span></span>
* <span data-ttu-id="09684-165">Mac/Linux, komut satırı ile</span><span class="sxs-lookup"><span data-stu-id="09684-165">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="09684-166">Web uygulaması geliştirme - Windows - Visual Studio için Python araçları</span><span class="sxs-lookup"><span data-stu-id="09684-166">Web App development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="09684-167">Depoyu kopyalama</span><span class="sxs-lookup"><span data-stu-id="09684-167">Clone the repository</span></span>
<span data-ttu-id="09684-168">İlk olarak, Azure Portal'da sağlanan URL'yi kullanarak depoyu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="09684-168">First, clone the repository using the url provided on the Azure Portal.</span></span> <span data-ttu-id="09684-169">Daha fazla bilgi için bkz. [Azure Uygulama Hizmeti’nde Yerel Git Dağıtımı](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="09684-169">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="09684-170">Depo kök dizininde bulunan çözüm dosyasını (.sln) açın.</span><span class="sxs-lookup"><span data-stu-id="09684-170">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="09684-171">Sanal ortamı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09684-171">Create virtual environment</span></span>
<span data-ttu-id="09684-172">Şimdi, yerel geliştirme için sanal bir ortam oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="09684-172">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="09684-173">Sağ **Python Ortamları**’na sağ tıklayın **Sanal Ortam Ekle...** seçeneğini seçin.</span><span class="sxs-lookup"><span data-stu-id="09684-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="09684-174">Ortam adının `env` olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="09684-174">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="09684-175">Temel yorumlayıcıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="09684-175">Select the base interpreter.</span></span> <span data-ttu-id="09684-176">Web uygulamanız için seçilen Python ile aynı sürümü kullandığınızdan emin olun (runtime.txt içinde veya Azure Portal’da uygulamanızın **Uygulama Ayarları** dikey penceresinde).</span><span class="sxs-lookup"><span data-stu-id="09684-176">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="09684-177">Paketleri indirme ve yükleme seçeneğinin işaretli olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="09684-177">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="09684-178">**Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="09684-178">Click **Create**.</span></span> <span data-ttu-id="09684-179">Bu, sanal ortamı oluşturur ve requirements.txt içinde listelenen bağımlılıkları yükler.</span><span class="sxs-lookup"><span data-stu-id="09684-179">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="09684-180">Geliştirme sunucusu kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="09684-180">Run using development server</span></span>
<span data-ttu-id="09684-181">Hata ayıklamayı başlatmak için F5 tuşuna basın, böylece web tarayıcınız yerel olarak çalışan sayfaya otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="09684-181">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

<span data-ttu-id="09684-182">Kaynaklarda kesme noktalarını ayarlayabilir, gözcü pencerelerini kullanabilirsiniz vb. Çeşitli özellikler hakkında daha fazla bilgi için bkz. [Visual Studio Belgeleri için Python Araçları].</span><span class="sxs-lookup"><span data-stu-id="09684-182">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="09684-183">Değişiklik yapma</span><span class="sxs-lookup"><span data-stu-id="09684-183">Make changes</span></span>
<span data-ttu-id="09684-184">Şimdi uygulama kaynakları ve/veya şablonlarında değişiklikler yapmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09684-184">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="09684-185">Değişikliklerinizi test ettikten sonra bunları Git deposuna kaydedin:</span><span class="sxs-lookup"><span data-stu-id="09684-185">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a><span data-ttu-id="09684-186">Daha fazla paket yükleme</span><span class="sxs-lookup"><span data-stu-id="09684-186">Install more packages</span></span>
<span data-ttu-id="09684-187">Uygulamanızın Python ve Bottle ötesinde bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="09684-187">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="09684-188">Pip kullanarak ek paketleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09684-188">You can install additional packages using pip.</span></span> <span data-ttu-id="09684-189">Bir paketi yüklemek için, sanal ortamda sağ tıklayıp **Python Paketini Yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="09684-189">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="09684-190">Örneğin, size Azure Storage, Service Bus ve diğer Azure hizmetleri için erişim imkanı sağlayan, Python için Azure SDK'yı yüklemek için şunu girin: `azure`</span><span class="sxs-lookup"><span data-stu-id="09684-190">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

<span data-ttu-id="09684-191">Sanal ortamda sağ tıklayıp **requirements.txt oluştur**’u seçerek requirements.txt dosyasını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="09684-191">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="09684-192">Ardından, requirements.txt dosyasındaki değişiklikleri Git deposuna uygulayın.</span><span class="sxs-lookup"><span data-stu-id="09684-192">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="09684-193">Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="09684-193">Deploy to Azure</span></span>
<span data-ttu-id="09684-194">Bir dağıtımı tetiklemek için tıklatın **Eşitle** veya **İlet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="09684-194">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="09684-195">Eşitleme, iletme ve çekme işlemini yapar.</span><span class="sxs-lookup"><span data-stu-id="09684-195">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

<span data-ttu-id="09684-196">Sanal ortam, yükleme paketleri vb. oluşturacağında, ilk dağıtımın gerçekleşmesi biraz zaman alır.</span><span class="sxs-lookup"><span data-stu-id="09684-196">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="09684-197">Visual Studio dağıtımın ilerleme durumunu göstermez.</span><span class="sxs-lookup"><span data-stu-id="09684-197">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="09684-198">Çıktıyı gözden geçirmek isterseniz, üzerinde bakın [Sorun Giderme - Dağıtım](#troubleshooting-deployment)’daki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="09684-198">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="09684-199">Yaptığınız değişiklikleri görmek için Azure URL'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="09684-199">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="09684-200">Web uygulaması geliştirme - Windows - komut satırı</span><span class="sxs-lookup"><span data-stu-id="09684-200">Web app development - Windows - Command Line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="09684-201">Depoyu kopyalama</span><span class="sxs-lookup"><span data-stu-id="09684-201">Clone the repository</span></span>
<span data-ttu-id="09684-202">İlk olarak, Azure Portal'da sağlanan URL'yi kullanarak depoyu kopyalayın ve uzak olarak Azure deposunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="09684-202">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="09684-203">Daha fazla bilgi için bkz. [Azure Uygulama Hizmeti’nde Yerel Git Dağıtımı](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="09684-203">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="09684-204">Sanal ortamı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09684-204">Create virtual environment</span></span>
<span data-ttu-id="09684-205">Geliştirme amacına yönelik yeni bir sanal ortam oluşturacağız (bunu depoya eklemeyin).</span><span class="sxs-lookup"><span data-stu-id="09684-205">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="09684-206">Uygulama üzerinde çalışan her geliştiricinin yerel olarak kendininkini oluşturacağı şekilde, Python’daki sanal ortamlar yeniden yerleştirilebilir değildir.</span><span class="sxs-lookup"><span data-stu-id="09684-206">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="09684-207">Web uygulamanız (runtime.txt veya Azure Portal'da web uygulamanız için uygulama ayarları dikey) için seçilen Python aynı sürümü kullandığınızdan emin olun</span><span class="sxs-lookup"><span data-stu-id="09684-207">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade for your web app in the Azure Portal)</span></span>

<span data-ttu-id="09684-208">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="09684-208">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="09684-209">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="09684-209">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="09684-210">Uygulamanız için gereken herhangi bir dış paketi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="09684-210">Install any external packages required by your application.</span></span> <span data-ttu-id="09684-211">Sanal ortamınıza paketleri yüklemek için depo kökündeki requirements.txt dosyasını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="09684-211">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="09684-212">Geliştirme sunucusu kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="09684-212">Run using development server</span></span>
<span data-ttu-id="09684-213">Aşağıdaki komutla bir geliştirme sunucusu altında uygulamayı başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="09684-213">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python app.py

<span data-ttu-id="09684-214">Konsol URL’yi ve sunucunun dinlediği bağlantı noktasını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="09684-214">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

<span data-ttu-id="09684-215">Sonra, bu URL için web tarayıcınızı açın.</span><span class="sxs-lookup"><span data-stu-id="09684-215">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="09684-216">Değişiklik yapma</span><span class="sxs-lookup"><span data-stu-id="09684-216">Make changes</span></span>
<span data-ttu-id="09684-217">Şimdi uygulama kaynakları ve/veya şablonlarında değişiklikler yapmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09684-217">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="09684-218">Değişikliklerinizi test ettikten sonra bunları Git deposuna kaydedin:</span><span class="sxs-lookup"><span data-stu-id="09684-218">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="09684-219">Daha fazla paket yükleme</span><span class="sxs-lookup"><span data-stu-id="09684-219">Install more packages</span></span>
<span data-ttu-id="09684-220">Uygulamanızın Python ve Bottle ötesinde bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="09684-220">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="09684-221">Pip kullanarak ek paketleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09684-221">You can install additional packages using pip.</span></span> <span data-ttu-id="09684-222">Örneğin, size Azure Storage, Service Bus ve diğer Azure hizmetleri için erişim imkanı sağlayan, Python için Azure SDK'yı yüklemek için aşağıdakileri yazın:</span><span class="sxs-lookup"><span data-stu-id="09684-222">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="09684-223">Requirements.txt dosyasını güncelleştirdiğinizden emin olun:</span><span class="sxs-lookup"><span data-stu-id="09684-223">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="09684-224">Değişiklikleri uygulayın:</span><span class="sxs-lookup"><span data-stu-id="09684-224">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="09684-225">Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="09684-225">Deploy to Azure</span></span>
<span data-ttu-id="09684-226">Bir dağıtımı tetiklemek için, değişiklikleri Azure’a gönderin:</span><span class="sxs-lookup"><span data-stu-id="09684-226">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="09684-227">Sanal ortam oluşturma, paketleri yükleme, web.config oluşturma dahil dağıtım betiği çıktısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="09684-227">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="09684-228">Yaptığınız değişiklikleri görmek için Azure URL'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="09684-228">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="09684-229">Web uygulaması geliştirme - Mac/Linux - komut satırı</span><span class="sxs-lookup"><span data-stu-id="09684-229">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="09684-230">Depoyu kopyalama</span><span class="sxs-lookup"><span data-stu-id="09684-230">Clone the repository</span></span>
<span data-ttu-id="09684-231">İlk olarak, Azure Portal'da sağlanan URL'yi kullanarak depoyu kopyalayın ve uzak olarak Azure deposunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="09684-231">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="09684-232">Daha fazla bilgi için bkz. [Azure Uygulama Hizmeti’nde Yerel Git Dağıtımı](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="09684-232">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="09684-233">Sanal ortamı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09684-233">Create virtual environment</span></span>
<span data-ttu-id="09684-234">Geliştirme amacına yönelik yeni bir sanal ortam oluşturacağız (bunu depoya eklemeyin).</span><span class="sxs-lookup"><span data-stu-id="09684-234">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="09684-235">Uygulama üzerinde çalışan her geliştiricinin yerel olarak kendininkini oluşturacağı şekilde, Python’daki sanal ortamlar yeniden yerleştirilebilir değildir.</span><span class="sxs-lookup"><span data-stu-id="09684-235">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="09684-236">Web uygulamanız için seçilen Python ile aynı sürümü kullandığınızdan emin olun (runtime.txt içinde veya Azure Portal’da uygulamanızın Uygulama Ayarları dikey penceresinde).</span><span class="sxs-lookup"><span data-stu-id="09684-236">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="09684-237">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="09684-237">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="09684-238">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="09684-238">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="09684-239">veya pyvenv env</span><span class="sxs-lookup"><span data-stu-id="09684-239">or pyvenv env</span></span>

<span data-ttu-id="09684-240">Uygulamanız için gereken herhangi bir dış paketi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="09684-240">Install any external packages required by your application.</span></span> <span data-ttu-id="09684-241">Sanal ortamınıza paketleri yüklemek için depo kökündeki requirements.txt dosyasını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="09684-241">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="09684-242">Geliştirme sunucusu kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="09684-242">Run using development server</span></span>
<span data-ttu-id="09684-243">Aşağıdaki komutla bir geliştirme sunucusu altında uygulamayı başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="09684-243">You can launch the application under a development server with the following command:</span></span>

    env/bin/python app.py

<span data-ttu-id="09684-244">Konsol URL’yi ve sunucunun dinlediği bağlantı noktasını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="09684-244">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

<span data-ttu-id="09684-245">Sonra, bu URL için web tarayıcınızı açın.</span><span class="sxs-lookup"><span data-stu-id="09684-245">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="09684-246">Değişiklik yapma</span><span class="sxs-lookup"><span data-stu-id="09684-246">Make changes</span></span>
<span data-ttu-id="09684-247">Şimdi uygulama kaynakları ve/veya şablonlarında değişiklikler yapmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09684-247">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="09684-248">Değişikliklerinizi test ettikten sonra bunları Git deposuna kaydedin:</span><span class="sxs-lookup"><span data-stu-id="09684-248">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="09684-249">Daha fazla paket yükleme</span><span class="sxs-lookup"><span data-stu-id="09684-249">Install more packages</span></span>
<span data-ttu-id="09684-250">Uygulamanızın Python ve Bottle ötesinde bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="09684-250">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="09684-251">Pip kullanarak ek paketleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09684-251">You can install additional packages using pip.</span></span> <span data-ttu-id="09684-252">Örneğin, size Azure Storage, Service Bus ve diğer Azure hizmetleri için erişim imkanı sağlayan, Python için Azure SDK'yı yüklemek için aşağıdakileri yazın:</span><span class="sxs-lookup"><span data-stu-id="09684-252">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="09684-253">Requirements.txt dosyasını güncelleştirdiğinizden emin olun:</span><span class="sxs-lookup"><span data-stu-id="09684-253">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="09684-254">Değişiklikleri uygulayın:</span><span class="sxs-lookup"><span data-stu-id="09684-254">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="09684-255">Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="09684-255">Deploy to Azure</span></span>
<span data-ttu-id="09684-256">Bir dağıtımı tetiklemek için, değişiklikleri Azure’a gönderin:</span><span class="sxs-lookup"><span data-stu-id="09684-256">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="09684-257">Sanal ortam oluşturma, paketleri yükleme, web.config oluşturma dahil dağıtım betiği çıktısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="09684-257">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="09684-258">Yaptığınız değişiklikleri görmek için Azure URL'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="09684-258">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="09684-259">Sorun giderme - Paket Yükleme</span><span class="sxs-lookup"><span data-stu-id="09684-259">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="09684-260">Sorun giderme - Sanal Ortam</span><span class="sxs-lookup"><span data-stu-id="09684-260">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="09684-261">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="09684-261">Next Steps</span></span>
<span data-ttu-id="09684-262">Visual Studio için Bottle ve Python araçları hakkında daha fazla bilgi için aşağıdaki bağlantıları izleyin:</span><span class="sxs-lookup"><span data-stu-id="09684-262">Follow these links to learn more about Bottle and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="09684-263">[Bottle belgeleri]</span><span class="sxs-lookup"><span data-stu-id="09684-263">[Bottle Documentation]</span></span>
* <span data-ttu-id="09684-264">[Visual Studio Belgeleri için Python Araçları]</span><span class="sxs-lookup"><span data-stu-id="09684-264">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="09684-265">Azure tablo depolaması ve MongoDB kullanma hakkında daha fazla bilgi için:</span><span class="sxs-lookup"><span data-stu-id="09684-265">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="09684-266">[Bottle ve Visual Studio için Python araçları ile azure'da MongoDB]</span><span class="sxs-lookup"><span data-stu-id="09684-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="09684-267">[Bottle ve Visual Studio için Python araçları ile azure'da Azure tablo depolaması]</span><span class="sxs-lookup"><span data-stu-id="09684-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="09684-268">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="09684-268">What's changed</span></span>
* <span data-ttu-id="09684-269">Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="09684-269">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="09684-270">[Bottle ve Visual Studio için Python araçları ile azure'da MongoDB]: web-sites-python-ptvs-bottle-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="09684-270">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span></span>
<span data-ttu-id="09684-271">[Bottle ve Visual Studio için Python araçları ile azure'da Azure tablo depolaması]: web-sites-python-ptvs-bottle-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="09684-271">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span></span>

<!--External Link references-->
<span data-ttu-id="09684-272">[Python 2.7 için Azure SDK]: http://go.microsoft.com/fwlink/?linkid=254281</span><span class="sxs-lookup"><span data-stu-id="09684-272">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span></span>
<span data-ttu-id="09684-273">[Python 3.4 için Azure SDK]: http://go.microsoft.com/fwlink/?linkid=516990</span><span class="sxs-lookup"><span data-stu-id="09684-273">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span></span>
<span data-ttu-id="09684-274">[python.org]: http://www.python.org/</span><span class="sxs-lookup"><span data-stu-id="09684-274">[python.org]: http://www.python.org/</span></span>
<span data-ttu-id="09684-275">[Windows için Git]: http://msysgit.github.io/</span><span class="sxs-lookup"><span data-stu-id="09684-275">[Git for Windows]: http://msysgit.github.io/</span></span>
<span data-ttu-id="09684-276">[Windows için GitHub]: https://windows.github.com/</span><span class="sxs-lookup"><span data-stu-id="09684-276">[GitHub for Windows]: https://windows.github.com/</span></span>
<span data-ttu-id="09684-277">[Visual Studio için Python Araçları]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="09684-277">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="09684-278">[Visual Studio için Python Araçları 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="09684-278">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="09684-279">[Visual Studio]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="09684-279">[Visual Studio]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="09684-280">[Visual Studio Belgeleri için Python Araçları]: http://aka.ms/ptvsdocs </span><span class="sxs-lookup"><span data-stu-id="09684-280">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs </span></span>
<span data-ttu-id="09684-281">[Bottle belgeleri]: http://bottlepy.org/docs/dev/index.html</span><span class="sxs-lookup"><span data-stu-id="09684-281">[Bottle Documentation]: http://bottlepy.org/docs/dev/index.html</span></span>

