---
title: "azure'da Bottle ile aaaPython web uygulamaları"
description: "Toorunning bir Python web uygulamasını Azure App Service Web Apps tanıtır Öğreticisi."
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
ms.openlocfilehash: 98acd7d8fcdbba326625121c20f9237d2663ea1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a><span data-ttu-id="c17b9-103">Azure'da Bottle ile Web uygulamaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="c17b9-103">Creating web apps with Bottle in Azure</span></span>
<span data-ttu-id="c17b9-104">Bu öğretici, Azure App Service Web uygulamalarında Python çalıştırmaya tooget nasıl başlatılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="c17b9-104">This tutorial describes how tooget started running Python in Azure App Service Web Apps.</span></span> <span data-ttu-id="c17b9-105">Web Apps sınırlı ücretsiz barındırma ve hızlı dağıtım sağlar ve Python’u kullanmanıza olanak tanır!</span><span class="sxs-lookup"><span data-stu-id="c17b9-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="c17b9-106">Uygulamanız büyüdükçe, toopaid barındırma geçiş yapabilirsiniz ve tüm ile de tümleştirebilir gibi diğer Azure hizmetleriyle hello.</span><span class="sxs-lookup"><span data-stu-id="c17b9-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="c17b9-107">Merhaba Bottle web çerçevesi kullanarak bir web uygulaması oluşturacaksınız (Bu öğretici için alternatif sürümleri bkz [Django](web-sites-python-create-deploy-django-app.md) ve [Flask](web-sites-python-create-deploy-flask-app.md)).</span><span class="sxs-lookup"><span data-stu-id="c17b9-107">You will create a web app using hello Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span></span> <span data-ttu-id="c17b9-108">Azure Market hello hello web uygulaması oluşturma, Git dağıtımı ayarlayacak ve hello depoyu yerel olarak kopyalayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c17b9-108">You will create hello web app from hello Azure Marketplace, set up Git deployment, and clone hello repository locally.</span></span> <span data-ttu-id="c17b9-109">Hello web uygulamasını yerel olarak çalıştırmak, değişiklik, yürütme ve bunları çok gönderme sonra[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="c17b9-109">Then you will run hello web app locally, make changes, commit and push them too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="c17b9-110">Eğitmen gösterir nasıl hello toodo bu Windows veya Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="c17b9-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="c17b9-111">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c17b9-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c17b9-112">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c17b9-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c17b9-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c17b9-113">Prerequisites</span></span>
* <span data-ttu-id="c17b9-114">Windows, Mac veya Linux</span><span class="sxs-lookup"><span data-stu-id="c17b9-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="c17b9-115">Python 2.7 ya da 3.4</span><span class="sxs-lookup"><span data-stu-id="c17b9-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="c17b9-116">setuptools, pip, virtualenv (yalnızca Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="c17b9-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="c17b9-117">Git</span><span class="sxs-lookup"><span data-stu-id="c17b9-117">Git</span></span>
* <span data-ttu-id="c17b9-118">[Visual Studio için Python Araçları 2.2][Visual Studio için Python Araçları 2.2] (PTVS) - Not: Bu seçenek isteğe bağlıdır</span><span class="sxs-lookup"><span data-stu-id="c17b9-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="c17b9-119">**Not**: TFS yayımlama şu anda Python projeleri için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="c17b9-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="c17b9-120">Windows</span><span class="sxs-lookup"><span data-stu-id="c17b9-120">Windows</span></span>
<span data-ttu-id="c17b9-121">Python 2.7 ya da 3.4 yüklü (32 bit) değilse, Web Platformu Yükleyicisi'ni kullanarak [Python 2.7 için Azure SDK] veya [Python 3.4 için Azure SDK]’yı yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="c17b9-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="c17b9-122">Bu, Python, setuptools, PIP, virtualenv, (32 bit Python hello Azure ana makinelerde yüklü olandır) "Merhaba 32-bit sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="c17b9-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span> <span data-ttu-id="c17b9-123">Alternatif olarak, Python’u [python.org] adresinden edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c17b9-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="c17b9-124">Git için, [Windows için Git] veya [Windows için GitHub]’ı öneririz.</span><span class="sxs-lookup"><span data-stu-id="c17b9-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="c17b9-125">Visual Studio kullanıyorsanız hello tümleşik Git desteğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c17b9-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="c17b9-126">Ayrıca [Visual Studio için Python Araçları 2.2]’yi yüklemenizi öneririz </span><span class="sxs-lookup"><span data-stu-id="c17b9-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="c17b9-127">Bu isteğe bağlı, ancak varsa [Visual Studio]hello dahil olmak üzere ücretsiz Visual Studio Community 2013 veya Visual Studio Express 2013 Web sonra bu mükemmel bir Python IDE verir.</span><span class="sxs-lookup"><span data-stu-id="c17b9-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="c17b9-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="c17b9-128">Mac/Linux</span></span>
<span data-ttu-id="c17b9-129">Python ve Git sizde zaten yüklü olmalıdır, ancak Python 2.7 veya 3.4 olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c17b9-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-hello-azure-portal"></a><span data-ttu-id="c17b9-130">Hello Azure Portal Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="c17b9-130">Web app creation on hello Azure Portal</span></span>
<span data-ttu-id="c17b9-131">Merhaba uygulamanızı oluşturmanın ilk adımı olan toocreate hello web uygulaması hello aracılığıyla [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c17b9-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span>  

1. <span data-ttu-id="c17b9-132">Oturum hello Azure Portal ve hello tıklatın **yeni** hello sol alt köşedeki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="c17b9-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span> 
2. <span data-ttu-id="c17b9-133">Merhaba arama kutusuna "python" yazın.</span><span class="sxs-lookup"><span data-stu-id="c17b9-133">In hello search box, type "python".</span></span>
3. <span data-ttu-id="c17b9-134">Merhaba arama sonuçlarında seçin **Bottle**, ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="c17b9-134">In hello search results, select **Bottle**, then click **Create**.</span></span>
4. <span data-ttu-id="c17b9-135">Yeni bir uygulama hizmeti planı ve yeni bir kaynak grubu oluşturma gibi hello yeni Bottle uygulamasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c17b9-135">Configure hello new Bottle app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="c17b9-136">Sonra, **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c17b9-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="c17b9-137">Merhaba yönergeleri izleyerek Git yayımlamayı yeni oluşturulan web uygulamanız için yapılandırma [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c17b9-137">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="c17b9-138">Uygulamaya Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c17b9-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="c17b9-139">Git deposu içeriği</span><span class="sxs-lookup"><span data-stu-id="c17b9-139">Git repository contents</span></span>
<span data-ttu-id="c17b9-140">Burada, hangi hello sonraki bölümde kopyalama hello ilk Git deposunda bulabilirsiniz hello dosyaları genel bir bakış verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c17b9-140">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

<span data-ttu-id="c17b9-141">Merhaba uygulaması için ana kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="c17b9-141">Main sources for hello application.</span></span> <span data-ttu-id="c17b9-142">Ana düzenle birlikte 3 sayfadan (dizin, hakkında, iletişim) oluşur.</span><span class="sxs-lookup"><span data-stu-id="c17b9-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="c17b9-143">Statik içerik ve betikler bootstrap, jquery, modernize ve yanıtı içerir.</span><span class="sxs-lookup"><span data-stu-id="c17b9-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \app.py

<span data-ttu-id="c17b9-144">Yerel Geliştirme Sunucusu desteği.</span><span class="sxs-lookup"><span data-stu-id="c17b9-144">Local development server support.</span></span> <span data-ttu-id="c17b9-145">Bu toorun hello uygulamayı yerel olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="c17b9-145">Use this toorun hello application locally.</span></span>

    \BottleWebProject.pyproj
    \BottleWebProject.sln

<span data-ttu-id="c17b9-146">[Visual Studio için Python Araçları] ile birlikte kullanmak için proje dosyaları.</span><span class="sxs-lookup"><span data-stu-id="c17b9-146">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="c17b9-147">Sanal ortamlar için IIS proxy ve PTVS uzaktan hata ayıklama desteği</span><span class="sxs-lookup"><span data-stu-id="c17b9-147">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="c17b9-148">Bu uygulamaya dış paketler gerekir.</span><span class="sxs-lookup"><span data-stu-id="c17b9-148">External packages needed by this application.</span></span> <span data-ttu-id="c17b9-149">Bu dosyada listelenen yükleme hello paketleri Hello dağıtım betiği pip.</span><span class="sxs-lookup"><span data-stu-id="c17b9-149">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="c17b9-150">IIS yapılandırma dosyaları.</span><span class="sxs-lookup"><span data-stu-id="c17b9-150">IIS configuration files.</span></span> <span data-ttu-id="c17b9-151">Merhaba dağıtım betiği hello uygun Web.x.y.config'i kullanır ve bunu web.config olarak kopyalar.</span><span class="sxs-lookup"><span data-stu-id="c17b9-151">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="c17b9-152">İsteğe bağlı dosyalar - Dağıtımı özelleştirme</span><span class="sxs-lookup"><span data-stu-id="c17b9-152">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="c17b9-153">İsteğe bağlı dosyalar - Python çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="c17b9-153">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="c17b9-154">Sunucu üzerindeki ek dosyalar</span><span class="sxs-lookup"><span data-stu-id="c17b9-154">Additional files on server</span></span>
<span data-ttu-id="c17b9-155">Bazı dosyalar hello sunucuda var, ancak toohello git deposuna eklenmez.</span><span class="sxs-lookup"><span data-stu-id="c17b9-155">Some files exist on hello server but are not added toohello git repository.</span></span> <span data-ttu-id="c17b9-156">Bunlar hello dağıtım betiği tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c17b9-156">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="c17b9-157">IIS yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="c17b9-157">IIS configuration file.</span></span> <span data-ttu-id="c17b9-158">Her dağıtımda web.x.y.config tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c17b9-158">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="c17b9-159">Python sanal ortamı.</span><span class="sxs-lookup"><span data-stu-id="c17b9-159">Python virtual environment.</span></span> <span data-ttu-id="c17b9-160">Dağıtım sırasında hello web uygulamasında uyumlu sanal ortamın zaten mevcut değilse oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c17b9-160">Created during deployment if a compatible virtual environment doesn't already exist on hello web app.</span></span>  <span data-ttu-id="c17b9-161">Requirements.txt içinde listelenen paketler pip yüklüdür, ancak hello paketler zaten yüklü ise pip yüklemeyi atlar.</span><span class="sxs-lookup"><span data-stu-id="c17b9-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="c17b9-162">Merhaba sonraki 3 bölümde nasıl tooproceed hello ile web uygulaması geliştirme altında farklı 3 ortamda açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="c17b9-162">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="c17b9-163">Windows, Visual Studio için Python Araçları ile</span><span class="sxs-lookup"><span data-stu-id="c17b9-163">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="c17b9-164">Windows, komut satırı ile</span><span class="sxs-lookup"><span data-stu-id="c17b9-164">Windows, with command line</span></span>
* <span data-ttu-id="c17b9-165">Mac/Linux, komut satırı ile</span><span class="sxs-lookup"><span data-stu-id="c17b9-165">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="c17b9-166">Web uygulaması geliştirme - Windows - Visual Studio için Python araçları</span><span class="sxs-lookup"><span data-stu-id="c17b9-166">Web App development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="c17b9-167">Kopya hello deposu</span><span class="sxs-lookup"><span data-stu-id="c17b9-167">Clone hello repository</span></span>
<span data-ttu-id="c17b9-168">İlk olarak, Azure Portal hello üzerinde sağlanan hello URL'yi kullanarak hello depoyu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c17b9-168">First, clone hello repository using hello url provided on hello Azure Portal.</span></span> <span data-ttu-id="c17b9-169">Daha fazla bilgi için bkz: [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c17b9-169">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="c17b9-170">Merhaba hello depo kök dizininde bulunan hello çözüm dosyasını (.sln) açın.</span><span class="sxs-lookup"><span data-stu-id="c17b9-170">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="c17b9-171">Sanal ortamı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c17b9-171">Create virtual environment</span></span>
<span data-ttu-id="c17b9-172">Şimdi, yerel geliştirme için sanal bir ortam oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="c17b9-172">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="c17b9-173">Sağ **Python Ortamları**’na sağ tıklayın **Sanal Ortam Ekle...** seçeneğini seçin.</span><span class="sxs-lookup"><span data-stu-id="c17b9-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="c17b9-174">Merhaba ortamı Hello adı olduğundan emin olun `env`.</span><span class="sxs-lookup"><span data-stu-id="c17b9-174">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="c17b9-175">Merhaba temel yorumlayıcıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="c17b9-175">Select hello base interpreter.</span></span> <span data-ttu-id="c17b9-176">Toouse hello web uygulamanız için seçilen Python ile aynı sürümü olduğundan emin olun (runtime.txt veya hello **uygulama ayarları** hello Azure Portal, web uygulamanızın dikey penceresinde).</span><span class="sxs-lookup"><span data-stu-id="c17b9-176">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="c17b9-177">Merhaba seçeneği toodownload ve yükleme paketleri işaretli olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c17b9-177">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="c17b9-178">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c17b9-178">Click **Create**.</span></span> <span data-ttu-id="c17b9-179">Bu işlem hello sanal ortam oluşturacak ve requirements.txt içinde listelenen bağımlılıkları yükler.</span><span class="sxs-lookup"><span data-stu-id="c17b9-179">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="c17b9-180">Geliştirme sunucusu kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c17b9-180">Run using development server</span></span>
<span data-ttu-id="c17b9-181">Otomatik olarak hata ayıklama tuşuna F5 toostart ve web tarayıcınız yerel olarak çalışan toohello sayfasını açar.</span><span class="sxs-lookup"><span data-stu-id="c17b9-181">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

<span data-ttu-id="c17b9-182">Kesme noktaları hello kaynakları, kullanım hello Gözcü pencerelerini, vb. ayarlayabilirsiniz. Merhaba bkz [Visual Studio belgeleri için Python Araçları] hakkında daha fazla bilgi için çeşitli özellikler hello.</span><span class="sxs-lookup"><span data-stu-id="c17b9-182">You can set breakpoints in hello sources, use hello watch windows, etc. See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="c17b9-183">Değişiklik yapma</span><span class="sxs-lookup"><span data-stu-id="c17b9-183">Make changes</span></span>
<span data-ttu-id="c17b9-184">Şimdi değişiklikleri toohello uygulama kaynakları ve/veya şablonlarında yapmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c17b9-184">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="c17b9-185">Değişikliklerinizi test ettikten sonra bunları toohello Git deposuna kaydedin:</span><span class="sxs-lookup"><span data-stu-id="c17b9-185">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a><span data-ttu-id="c17b9-186">Daha fazla paket yükleme</span><span class="sxs-lookup"><span data-stu-id="c17b9-186">Install more packages</span></span>
<span data-ttu-id="c17b9-187">Uygulamanızın Python ve Bottle ötesinde bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="c17b9-187">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="c17b9-188">Pip kullanarak ek paketleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c17b9-188">You can install additional packages using pip.</span></span> <span data-ttu-id="c17b9-189">bir paket tooinstall sağ tıklayın hello sanal ortam ve select **Python paketini Yükle**.</span><span class="sxs-lookup"><span data-stu-id="c17b9-189">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="c17b9-190">Örneğin, tooinstall Merhaba, tooAzure depolama, service bus ve diğer Azure hizmetleriyle erişmenizi girin Python için Azure SDK `azure`:</span><span class="sxs-lookup"><span data-stu-id="c17b9-190">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

<span data-ttu-id="c17b9-191">Merhaba sanal ortamda sağ tıklayıp **requirements.txt Oluştur** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="c17b9-191">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="c17b9-192">Ardından, hello değişiklikleri toorequirements.txt toohello Git deposuna uygulayın.</span><span class="sxs-lookup"><span data-stu-id="c17b9-192">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="c17b9-193">TooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="c17b9-193">Deploy tooAzure</span></span>
<span data-ttu-id="c17b9-194">bir dağıtım tootrigger tıklayın **eşitleme** veya **anında**.</span><span class="sxs-lookup"><span data-stu-id="c17b9-194">tootrigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="c17b9-195">Eşitleme, iletme ve çekme işlemini yapar.</span><span class="sxs-lookup"><span data-stu-id="c17b9-195">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

<span data-ttu-id="c17b9-196">bir sanal ortam, yükleme paketleri vb. oluşturacağı gibi hello ilk dağıtım biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="c17b9-196">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="c17b9-197">Visual Studio hello hello dağıtımının ilerlemesini göstermez.</span><span class="sxs-lookup"><span data-stu-id="c17b9-197">Visual Studio doesn't show hello progress of hello deployment.</span></span> <span data-ttu-id="c17b9-198">Tooreview hello çıkış isterseniz hello bölümüne bakarak [sorun giderme - dağıtım](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="c17b9-198">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="c17b9-199">Toohello Azure URL tooview değişikliklerinizi göz atın.</span><span class="sxs-lookup"><span data-stu-id="c17b9-199">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="c17b9-200">Web uygulaması geliştirme - Windows - komut satırı</span><span class="sxs-lookup"><span data-stu-id="c17b9-200">Web app development - Windows - Command Line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="c17b9-201">Kopya hello deposu</span><span class="sxs-lookup"><span data-stu-id="c17b9-201">Clone hello repository</span></span>
<span data-ttu-id="c17b9-202">İlk olarak, Azure Portal hello üzerinde sağlanan hello URL'yi kullanarak hello depoyu kopyalayın ve uzak olarak hello Azure deposunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c17b9-202">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="c17b9-203">Daha fazla bilgi için bkz: [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c17b9-203">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="c17b9-204">Sanal ortamı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c17b9-204">Create virtual environment</span></span>
<span data-ttu-id="c17b9-205">(Bunu toohello depoya eklemeyin) geliştirme amacıyla yeni bir sanal ortam oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="c17b9-205">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="c17b9-206">Sanal ortamlar Hello uygulama üzerinde çalışan her geliştiricinin yerel olarak Kendininkini oluşturacağı şekilde python'daki, değildir.</span><span class="sxs-lookup"><span data-stu-id="c17b9-206">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="c17b9-207">Toouse hello web uygulamanızda (runtime.txt veya hello uygulama ayarları dikey penceresinde hello Azure Portal, web uygulaması) için seçilen Python ile aynı sürümü olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="c17b9-207">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade for your web app in hello Azure Portal)</span></span>

<span data-ttu-id="c17b9-208">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="c17b9-208">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="c17b9-209">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="c17b9-209">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="c17b9-210">Uygulamanız için gereken herhangi bir dış paketi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c17b9-210">Install any external packages required by your application.</span></span> <span data-ttu-id="c17b9-211">Sanal ortamınıza hello hello depo tooinstall hello paketleri kökünde hello requirements.txt dosyasını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c17b9-211">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="c17b9-212">Geliştirme sunucusu kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c17b9-212">Run using development server</span></span>
<span data-ttu-id="c17b9-213">Komutu aşağıdaki hello ile Merhaba uygulaması geliştirme sunucusu altında başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c17b9-213">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python app.py

<span data-ttu-id="c17b9-214">Merhaba konsol hello URL'si gösterilir ve bağlantı noktası hello sunucu dinler:</span><span class="sxs-lookup"><span data-stu-id="c17b9-214">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

<span data-ttu-id="c17b9-215">Sonra web tarayıcısı toothat URL'nizi açın.</span><span class="sxs-lookup"><span data-stu-id="c17b9-215">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="c17b9-216">Değişiklik yapma</span><span class="sxs-lookup"><span data-stu-id="c17b9-216">Make changes</span></span>
<span data-ttu-id="c17b9-217">Şimdi değişiklikleri toohello uygulama kaynakları ve/veya şablonlarında yapmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c17b9-217">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="c17b9-218">Değişikliklerinizi test ettikten sonra bunları toohello Git deposuna kaydedin:</span><span class="sxs-lookup"><span data-stu-id="c17b9-218">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="c17b9-219">Daha fazla paket yükleme</span><span class="sxs-lookup"><span data-stu-id="c17b9-219">Install more packages</span></span>
<span data-ttu-id="c17b9-220">Uygulamanızın Python ve Bottle ötesinde bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="c17b9-220">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="c17b9-221">Pip kullanarak ek paketleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c17b9-221">You can install additional packages using pip.</span></span> <span data-ttu-id="c17b9-222">Örneğin, tooinstall Merhaba, imkanı sağlayan, Python için Azure SDK tooAzure depolama, service bus ve diğer Azure hizmetleriyle türü erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c17b9-222">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="c17b9-223">Tooupdate requirements.txt emin olun:</span><span class="sxs-lookup"><span data-stu-id="c17b9-223">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="c17b9-224">Merhaba değişiklikleri uygulayın:</span><span class="sxs-lookup"><span data-stu-id="c17b9-224">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="c17b9-225">TooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="c17b9-225">Deploy tooAzure</span></span>
<span data-ttu-id="c17b9-226">bir dağıtım tootrigger, anında iletme hello tooAzure değiştirir:</span><span class="sxs-lookup"><span data-stu-id="c17b9-226">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="c17b9-227">Merhaba Merhaba, sanal ortam oluşturma, paketleri yükleme, web.config oluşturma dahil dağıtım betiği çıktısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c17b9-227">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="c17b9-228">Toohello Azure URL tooview değişikliklerinizi göz atın.</span><span class="sxs-lookup"><span data-stu-id="c17b9-228">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="c17b9-229">Web uygulaması geliştirme - Mac/Linux - komut satırı</span><span class="sxs-lookup"><span data-stu-id="c17b9-229">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="c17b9-230">Kopya hello deposu</span><span class="sxs-lookup"><span data-stu-id="c17b9-230">Clone hello repository</span></span>
<span data-ttu-id="c17b9-231">İlk olarak, Azure Portal hello üzerinde sağlanan hello URL'yi kullanarak hello depoyu kopyalayın ve uzak olarak hello Azure deposunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c17b9-231">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="c17b9-232">Daha fazla bilgi için bkz: [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c17b9-232">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="c17b9-233">Sanal ortamı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c17b9-233">Create virtual environment</span></span>
<span data-ttu-id="c17b9-234">(Bunu toohello depoya eklemeyin) geliştirme amacıyla yeni bir sanal ortam oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="c17b9-234">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="c17b9-235">Sanal ortamlar Hello uygulama üzerinde çalışan her geliştiricinin yerel olarak Kendininkini oluşturacağı şekilde python'daki, değildir.</span><span class="sxs-lookup"><span data-stu-id="c17b9-235">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="c17b9-236">Toouse hello web uygulamanızda (runtime.txt veya hello uygulama ayarları dikey penceresinde hello Azure Portal kullanarak web uygulamanızda) için seçilen Python ile aynı sürümü emin olun.</span><span class="sxs-lookup"><span data-stu-id="c17b9-236">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="c17b9-237">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="c17b9-237">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="c17b9-238">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="c17b9-238">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="c17b9-239">veya pyvenv env</span><span class="sxs-lookup"><span data-stu-id="c17b9-239">or pyvenv env</span></span>

<span data-ttu-id="c17b9-240">Uygulamanız için gereken herhangi bir dış paketi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c17b9-240">Install any external packages required by your application.</span></span> <span data-ttu-id="c17b9-241">Sanal ortamınıza hello hello depo tooinstall hello paketleri kökünde hello requirements.txt dosyasını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c17b9-241">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="c17b9-242">Geliştirme sunucusu kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c17b9-242">Run using development server</span></span>
<span data-ttu-id="c17b9-243">Komutu aşağıdaki hello ile Merhaba uygulaması geliştirme sunucusu altında başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c17b9-243">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python app.py

<span data-ttu-id="c17b9-244">Merhaba konsol hello URL'si gösterilir ve bağlantı noktası hello sunucu dinler:</span><span class="sxs-lookup"><span data-stu-id="c17b9-244">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

<span data-ttu-id="c17b9-245">Sonra web tarayıcısı toothat URL'nizi açın.</span><span class="sxs-lookup"><span data-stu-id="c17b9-245">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="c17b9-246">Değişiklik yapma</span><span class="sxs-lookup"><span data-stu-id="c17b9-246">Make changes</span></span>
<span data-ttu-id="c17b9-247">Şimdi değişiklikleri toohello uygulama kaynakları ve/veya şablonlarında yapmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c17b9-247">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="c17b9-248">Değişikliklerinizi test ettikten sonra bunları toohello Git deposuna kaydedin:</span><span class="sxs-lookup"><span data-stu-id="c17b9-248">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="c17b9-249">Daha fazla paket yükleme</span><span class="sxs-lookup"><span data-stu-id="c17b9-249">Install more packages</span></span>
<span data-ttu-id="c17b9-250">Uygulamanızın Python ve Bottle ötesinde bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="c17b9-250">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="c17b9-251">Pip kullanarak ek paketleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c17b9-251">You can install additional packages using pip.</span></span> <span data-ttu-id="c17b9-252">Örneğin, tooinstall Merhaba, imkanı sağlayan, Python için Azure SDK tooAzure depolama, service bus ve diğer Azure hizmetleriyle türü erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c17b9-252">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="c17b9-253">Tooupdate requirements.txt emin olun:</span><span class="sxs-lookup"><span data-stu-id="c17b9-253">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="c17b9-254">Merhaba değişiklikleri uygulayın:</span><span class="sxs-lookup"><span data-stu-id="c17b9-254">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="c17b9-255">TooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="c17b9-255">Deploy tooAzure</span></span>
<span data-ttu-id="c17b9-256">bir dağıtım tootrigger, anında iletme hello tooAzure değiştirir:</span><span class="sxs-lookup"><span data-stu-id="c17b9-256">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="c17b9-257">Merhaba Merhaba, sanal ortam oluşturma, paketleri yükleme, web.config oluşturma dahil dağıtım betiği çıktısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c17b9-257">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="c17b9-258">Toohello Azure URL tooview değişikliklerinizi göz atın.</span><span class="sxs-lookup"><span data-stu-id="c17b9-258">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="c17b9-259">Sorun giderme - Paket Yükleme</span><span class="sxs-lookup"><span data-stu-id="c17b9-259">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="c17b9-260">Sorun giderme - Sanal Ortam</span><span class="sxs-lookup"><span data-stu-id="c17b9-260">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="c17b9-261">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="c17b9-261">Next Steps</span></span>
<span data-ttu-id="c17b9-262">Bu bağlantılar toolearn Bottle ve Python araçları hakkında daha fazla bilgi için Visual Studio izleyin:</span><span class="sxs-lookup"><span data-stu-id="c17b9-262">Follow these links toolearn more about Bottle and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="c17b9-263">[Bottle belgeleri]</span><span class="sxs-lookup"><span data-stu-id="c17b9-263">[Bottle Documentation]</span></span>
* <span data-ttu-id="c17b9-264">[Visual Studio belgeleri için Python Araçları]</span><span class="sxs-lookup"><span data-stu-id="c17b9-264">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="c17b9-265">Azure tablo depolaması ve MongoDB kullanma hakkında daha fazla bilgi için:</span><span class="sxs-lookup"><span data-stu-id="c17b9-265">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="c17b9-266">[Bottle ve Visual Studio için Python araçları ile azure'da MongoDB]</span><span class="sxs-lookup"><span data-stu-id="c17b9-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="c17b9-267">[Bottle ve Visual Studio için Python araçları ile azure'da Azure tablo depolaması]</span><span class="sxs-lookup"><span data-stu-id="c17b9-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="c17b9-268">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="c17b9-268">What's changed</span></span>
* <span data-ttu-id="c17b9-269">Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="c17b9-269">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Bottle ve Visual Studio için Python araçları ile azure'da MongoDB]: web-sites-python-ptvs-bottle-table-storage.md
[Bottle ve Visual Studio için Python araçları ile azure'da Azure tablo depolaması]: web-sites-python-ptvs-bottle-table-storage.md

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
[Bottle belgeleri]: http://bottlepy.org/docs/dev/index.html

