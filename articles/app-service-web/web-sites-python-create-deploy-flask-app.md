---
title: "azure'da Flask ile aaaCreating web uygulamaları"
description: "Azure üzerinde bir Python web uygulaması toorunning tanıtır Öğreticisi."
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
ms.openlocfilehash: 3362047b3106b4380b5971e47cbd8042d38a792b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a><span data-ttu-id="4c7b6-103">Azure'da Flask ile Web uygulamaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c7b6-103">Creating web apps with Flask in Azure</span></span>
<span data-ttu-id="4c7b6-104">Bu öğretici tooget Python çalıştırmaya nasıl başlatılacağını açıklar [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="4c7b6-104">This tutorial describes how tooget started running Python in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>  <span data-ttu-id="4c7b6-105">Web Apps sınırlı ücretsiz barındırma ve hızlı dağıtım sağlar ve Python’u kullanmanıza olanak tanır!</span><span class="sxs-lookup"><span data-stu-id="4c7b6-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span>  <span data-ttu-id="4c7b6-106">Uygulamanız büyüdükçe, toopaid barındırma geçiş yapabilirsiniz ve tüm ile de tümleştirebilir gibi diğer Azure hizmetleriyle hello.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="4c7b6-107">Merhaba Flask web altyapısını kullanarak bir uygulama oluşturacaksınız (Bu öğretici için alternatif sürümleri bkz [Django](web-sites-python-create-deploy-django-app.md) ve [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="4c7b6-107">You will create an application using hello Flask web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span>  <span data-ttu-id="4c7b6-108">Azure galerisinde hello hello Web sitesi oluşturma Git dağıtımı ayarlayacak ve hello depoyu yerel olarak kopyalayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-108">You will create hello website from hello Azure gallery, set up Git deployment, and clone hello repository locally.</span></span>  <span data-ttu-id="4c7b6-109">Ardından, hello uygulamayı yerel olarak çalıştırmak, değişiklik, yürütme ve bunları tooAzure gönderme.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-109">Then you will run hello application locally, make changes, commit and push them tooAzure.</span></span>  <span data-ttu-id="4c7b6-110">Eğitmen gösterir nasıl hello toodo bu Windows veya Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="4c7b6-111">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="4c7b6-112">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="4c7b6-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4c7b6-113">Prerequisites</span></span>
* <span data-ttu-id="4c7b6-114">Windows, Mac veya Linux</span><span class="sxs-lookup"><span data-stu-id="4c7b6-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="4c7b6-115">Python 2.7 ya da 3.4</span><span class="sxs-lookup"><span data-stu-id="4c7b6-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="4c7b6-116">setuptools, pip, virtualenv (yalnızca Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="4c7b6-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="4c7b6-117">Git</span><span class="sxs-lookup"><span data-stu-id="4c7b6-117">Git</span></span>
* <span data-ttu-id="4c7b6-118">[Visual Studio için Python Araçları][Visual Studio için Python Araçları] (PTVS) - Not: Bu özellik isteğe bağlıdır</span><span class="sxs-lookup"><span data-stu-id="4c7b6-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="4c7b6-119">**Not**: TFS yayımlama şu anda Python projeleri için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="4c7b6-120">Windows</span><span class="sxs-lookup"><span data-stu-id="4c7b6-120">Windows</span></span>
<span data-ttu-id="4c7b6-121">Python 2.7 ya da 3.4 yüklü (32 bit) değilse, Web Platformu Yükleyicisi'ni kullanarak [Python 2.7 için Azure SDK] veya [Python 3.4 için Azure SDK]’yı yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span>  <span data-ttu-id="4c7b6-122">Bu, Python, setuptools, PIP, virtualenv, (32 bit Python hello Azure ana makinelerde yüklü olandır) "Merhaba 32-bit sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span>  <span data-ttu-id="4c7b6-123">Alternatif olarak, Python’u [python.org] adresinden edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="4c7b6-124">Git için, [Windows için Git] veya [Windows için GitHub]’ı öneririz.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span>  <span data-ttu-id="4c7b6-125">Visual Studio kullanıyorsanız hello tümleşik Git desteğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="4c7b6-126">Ayrıca [Visual Studio için Python Araçları 2.2]’yi yüklemenizi öneririz </span><span class="sxs-lookup"><span data-stu-id="4c7b6-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span>  <span data-ttu-id="4c7b6-127">Bu isteğe bağlı, ancak varsa [Visual Studio]hello dahil olmak üzere ücretsiz Visual Studio Community 2013 veya Visual Studio Express 2013 Web sonra bu mükemmel bir Python IDE verir.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="4c7b6-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="4c7b6-128">Mac/Linux</span></span>
<span data-ttu-id="4c7b6-129">Python ve Git sizde zaten yüklü olmalıdır, ancak Python 2.7 veya 3.4 olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-create-on-hello-azure-portal"></a><span data-ttu-id="4c7b6-130">Azure Portal hello üzerinde Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c7b6-130">Web app create on hello Azure Portal</span></span>
<span data-ttu-id="4c7b6-131">Merhaba uygulamanızı oluşturmanın ilk adımı olan toocreate hello web uygulaması hello aracılığıyla [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4c7b6-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span> 

1. <span data-ttu-id="4c7b6-132">Oturum hello Azure Portal ve hello tıklatın **yeni** hello sol alt köşedeki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span> 
2. <span data-ttu-id="4c7b6-133">**Web + Mobil**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-133">Click **Web + Mobile**.</span></span>
3. <span data-ttu-id="4c7b6-134">Merhaba arama kutusuna "python" yazın.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-134">In hello search box, type "python".</span></span>
4. <span data-ttu-id="4c7b6-135">Merhaba arama sonuçlarında seçin **Flask**, ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-135">In hello search results, select **Flask**, then click **Create**.</span></span>
5. <span data-ttu-id="4c7b6-136">Yeni bir uygulama hizmeti planı ve yeni bir kaynak grubu oluşturma gibi hello yeni Flask uygulamasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-136">Configure hello new Flask app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="4c7b6-137">Sonra, **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-137">Then, click **Create**.</span></span>
6. <span data-ttu-id="4c7b6-138">Merhaba yönergeleri izleyerek Git yayımlamayı yeni oluşturulan web uygulamanız için yapılandırma [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="4c7b6-138">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="4c7b6-139">Uygulamaya Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="4c7b6-139">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="4c7b6-140">Git deposu içeriği</span><span class="sxs-lookup"><span data-stu-id="4c7b6-140">Git repository contents</span></span>
<span data-ttu-id="4c7b6-141">Burada, hangi hello sonraki bölümde kopyalama hello ilk Git deposunda bulabilirsiniz hello dosyaları genel bir bakış verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-141">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

<span data-ttu-id="4c7b6-142">Merhaba uygulaması için ana kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-142">Main sources for hello application.</span></span>  <span data-ttu-id="4c7b6-143">Ana düzenle birlikte 3 sayfadan (dizin, hakkında, iletişim) oluşur.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-143">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="4c7b6-144">Statik içerik ve betikler bootstrap, jquery, modernize ve yanıtı içerir.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-144">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \runserver.py

<span data-ttu-id="4c7b6-145">Yerel Geliştirme Sunucusu desteği.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-145">Local development server support.</span></span> <span data-ttu-id="4c7b6-146">Bu toorun hello uygulamayı yerel olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-146">Use this toorun hello application locally.</span></span>

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

<span data-ttu-id="4c7b6-147">[Visual Studio için Python Araçları] ile birlikte kullanmak için proje dosyaları.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-147">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="4c7b6-148">Sanal ortamlar için IIS proxy ve PTVS uzaktan hata ayıklama desteği</span><span class="sxs-lookup"><span data-stu-id="4c7b6-148">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="4c7b6-149">Bu uygulamaya dış paketler gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-149">External packages needed by this application.</span></span> <span data-ttu-id="4c7b6-150">Bu dosyada listelenen yükleme hello paketleri Hello dağıtım betiği pip.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-150">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="4c7b6-151">IIS yapılandırma dosyaları.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-151">IIS configuration files.</span></span>  <span data-ttu-id="4c7b6-152">Merhaba dağıtım betiği hello uygun Web.x.y.config'i kullanır ve bunu web.config olarak kopyalar.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-152">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="4c7b6-153">İsteğe bağlı dosyalar - Dağıtımı özelleştirme</span><span class="sxs-lookup"><span data-stu-id="4c7b6-153">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="4c7b6-154">İsteğe bağlı dosyalar - Python çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="4c7b6-154">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="4c7b6-155">Sunucu üzerindeki ek dosyalar</span><span class="sxs-lookup"><span data-stu-id="4c7b6-155">Additional files on server</span></span>
<span data-ttu-id="4c7b6-156">Bazı dosyalar hello sunucuda var, ancak toohello git deposuna eklenmez.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-156">Some files exist on hello server but are not added toohello git repository.</span></span>  <span data-ttu-id="4c7b6-157">Bunlar hello dağıtım betiği tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-157">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="4c7b6-158">IIS yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-158">IIS configuration file.</span></span>  <span data-ttu-id="4c7b6-159">Her dağıtımda web.x.y.config tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-159">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="4c7b6-160">Python sanal ortamı.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-160">Python virtual environment.</span></span>  <span data-ttu-id="4c7b6-161">Dağıtım sırasında hello uygulamasında uyumlu sanal ortamın zaten mevcut değilse oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-161">Created during deployment if a compatible virtual environment doesn't already exist on hello app.</span></span>  <span data-ttu-id="4c7b6-162">Requirements.txt içinde listelenen paketler pip yüklüdür, ancak hello paketler zaten yüklü ise pip yüklemeyi atlar.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-162">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="4c7b6-163">Merhaba sonraki 3 bölümde nasıl tooproceed hello ile web uygulaması geliştirme altında farklı 3 ortamda açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-163">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="4c7b6-164">Windows, Visual Studio için Python Araçları ile</span><span class="sxs-lookup"><span data-stu-id="4c7b6-164">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="4c7b6-165">Windows, komut satırı ile</span><span class="sxs-lookup"><span data-stu-id="4c7b6-165">Windows, with command line</span></span>
* <span data-ttu-id="4c7b6-166">Mac/Linux, komut satırı ile</span><span class="sxs-lookup"><span data-stu-id="4c7b6-166">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="4c7b6-167">Web uygulaması geliştirme - Windows - Visual Studio için Python Araçları</span><span class="sxs-lookup"><span data-stu-id="4c7b6-167">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="4c7b6-168">Kopya hello deposu</span><span class="sxs-lookup"><span data-stu-id="4c7b6-168">Clone hello repository</span></span>
<span data-ttu-id="4c7b6-169">İlk olarak, Azure Portal hello üzerinde sağlanan hello URL'yi kullanarak hello depoyu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-169">First, clone hello repository using hello URL provided on hello Azure Portal.</span></span> <span data-ttu-id="4c7b6-170">Daha fazla bilgi için bkz: [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="4c7b6-170">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="4c7b6-171">Merhaba hello depo kök dizininde bulunan hello çözüm dosyasını (.sln) açın.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-171">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="4c7b6-172">Sanal ortamı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-172">Create virtual environment</span></span>
<span data-ttu-id="4c7b6-173">Şimdi, yerel geliştirme için sanal bir ortam oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-173">Now we'll create a virtual environment for local development.</span></span>  <span data-ttu-id="4c7b6-174">Sağ **Python Ortamları**’na sağ tıklayın **Sanal Ortam Ekle...** seçeneğini seçin.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-174">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="4c7b6-175">Merhaba ortamı Hello adı olduğundan emin olun `env`.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-175">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="4c7b6-176">Merhaba temel yorumlayıcıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-176">Select hello base interpreter.</span></span>  <span data-ttu-id="4c7b6-177">Toouse hello web uygulamanız için seçilen Python ile aynı sürümü olduğundan emin olun (runtime.txt veya hello **uygulama ayarları** hello Azure Portal, web uygulamanızın dikey penceresinde).</span><span class="sxs-lookup"><span data-stu-id="4c7b6-177">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="4c7b6-178">Merhaba seçeneği toodownload ve yükleme paketleri işaretli olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-178">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="4c7b6-179">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-179">Click **Create**.</span></span>  <span data-ttu-id="4c7b6-180">Bu işlem hello sanal ortam oluşturacak ve requirements.txt içinde listelenen bağımlılıkları yükler.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-180">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="4c7b6-181">Geliştirme sunucusu kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="4c7b6-181">Run using development server</span></span>
<span data-ttu-id="4c7b6-182">Otomatik olarak hata ayıklama tuşuna F5 toostart ve web tarayıcınız yerel olarak çalışan toohello sayfasını açar.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-182">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

<span data-ttu-id="4c7b6-183">Kesme noktaları hello kaynakları, kullanım hello Gözcü pencerelerini, vb. ayarlayabilirsiniz.  Merhaba bkz [Visual Studio belgeleri için Python Araçları] hakkında daha fazla bilgi için çeşitli özellikler hello.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-183">You can set breakpoints in hello sources, use hello watch windows, etc.  See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="4c7b6-184">Değişiklik yapma</span><span class="sxs-lookup"><span data-stu-id="4c7b6-184">Make changes</span></span>
<span data-ttu-id="4c7b6-185">Şimdi değişiklikleri toohello uygulama kaynakları ve/veya şablonlarında yapmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-185">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="4c7b6-186">Değişikliklerinizi test ettikten sonra bunları toohello Git deposuna kaydedin:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-186">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a><span data-ttu-id="4c7b6-187">Daha fazla paket yükleme</span><span class="sxs-lookup"><span data-stu-id="4c7b6-187">Install more packages</span></span>
<span data-ttu-id="4c7b6-188">Uygulamanızın Python ve Flask ötesinde bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-188">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="4c7b6-189">Pip kullanarak ek paketleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-189">You can install additional packages using pip.</span></span>  <span data-ttu-id="4c7b6-190">bir paket tooinstall sağ tıklayın hello sanal ortam ve select **Python paketini Yükle**.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-190">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="4c7b6-191">Örneğin, tooinstall Merhaba, tooAzure depolama, service bus ve diğer Azure hizmetleriyle erişmenizi girin Python için Azure SDK `azure`:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-191">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

<span data-ttu-id="4c7b6-192">Merhaba sanal ortamda sağ tıklayıp **requirements.txt Oluştur** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-192">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="4c7b6-193">Ardından, hello değişiklikleri toorequirements.txt toohello Git deposuna uygulayın.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-193">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="4c7b6-194">TooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="4c7b6-194">Deploy tooAzure</span></span>
<span data-ttu-id="4c7b6-195">bir dağıtım tootrigger tıklayın **eşitleme** veya **anında**.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-195">tootrigger a deployment, click on **Sync** or **Push**.</span></span>  <span data-ttu-id="4c7b6-196">Eşitleme, iletme ve çekme işlemini yapar.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-196">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

<span data-ttu-id="4c7b6-197">bir sanal ortam, yükleme paketleri vb. oluşturacağı gibi hello ilk dağıtım biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-197">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="4c7b6-198">Visual Studio hello hello dağıtımının ilerlemesini göstermez.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-198">Visual Studio doesn't show hello progress of hello deployment.</span></span>  <span data-ttu-id="4c7b6-199">Tooreview hello çıkış isterseniz hello bölümüne bakarak [sorun giderme - dağıtım](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="4c7b6-199">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="4c7b6-200">Toohello Azure URL tooview değişikliklerinizi göz atın.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-200">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="4c7b6-201">Web uygulaması geliştirme - Windows - komut satırı</span><span class="sxs-lookup"><span data-stu-id="4c7b6-201">Web app development - Windows - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="4c7b6-202">Kopya hello deposu</span><span class="sxs-lookup"><span data-stu-id="4c7b6-202">Clone hello repository</span></span>
<span data-ttu-id="4c7b6-203">İlk olarak, Azure Portal hello üzerinde sağlanan hello URL'yi kullanarak hello depoyu kopyalayın ve uzak olarak hello Azure deposunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-203">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="4c7b6-204">Daha fazla bilgi için bkz: [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="4c7b6-204">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="4c7b6-205">Sanal ortamı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-205">Create virtual environment</span></span>
<span data-ttu-id="4c7b6-206">(Bunu toohello depoya eklemeyin) geliştirme amacıyla yeni bir sanal ortam oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-206">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span>  <span data-ttu-id="4c7b6-207">Sanal ortamlar Hello uygulama üzerinde çalışan her geliştiricinin yerel olarak Kendininkini oluşturacağı şekilde python'daki, değildir.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-207">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="4c7b6-208">Toouse hello web uygulamanız için seçilen Python ile aynı sürümü olduğundan emin olun (runtime.txt veya hello **uygulama ayarları** hello Azure Portal, web uygulamanızın dikey penceresinde).</span><span class="sxs-lookup"><span data-stu-id="4c7b6-208">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="4c7b6-209">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-209">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="4c7b6-210">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-210">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="4c7b6-211">Uygulamanız için gereken herhangi bir dış paketi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-211">Install any external packages required by your application.</span></span> <span data-ttu-id="4c7b6-212">Sanal ortamınıza hello hello depo tooinstall hello paketleri kökünde hello requirements.txt dosyasını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-212">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="4c7b6-213">Geliştirme sunucusu kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="4c7b6-213">Run using development server</span></span>
<span data-ttu-id="4c7b6-214">Komutu aşağıdaki hello ile Merhaba uygulaması geliştirme sunucusu altında başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-214">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python runserver.py

<span data-ttu-id="4c7b6-215">Merhaba konsol hello URL'si gösterilir ve bağlantı noktası hello sunucu dinler:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-215">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

<span data-ttu-id="4c7b6-216">Sonra web tarayıcısı toothat URL'nizi açın.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-216">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="4c7b6-217">Değişiklik yapma</span><span class="sxs-lookup"><span data-stu-id="4c7b6-217">Make changes</span></span>
<span data-ttu-id="4c7b6-218">Şimdi değişiklikleri toohello uygulama kaynakları ve/veya şablonlarında yapmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-218">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="4c7b6-219">Değişikliklerinizi test ettikten sonra bunları toohello Git deposuna kaydedin:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-219">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="4c7b6-220">Daha fazla paket yükleme</span><span class="sxs-lookup"><span data-stu-id="4c7b6-220">Install more packages</span></span>
<span data-ttu-id="4c7b6-221">Uygulamanızın Python ve Flask ötesinde bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-221">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="4c7b6-222">Pip kullanarak ek paketleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-222">You can install additional packages using pip.</span></span>  <span data-ttu-id="4c7b6-223">Örneğin, tooinstall Merhaba, imkanı sağlayan, Python için Azure SDK tooAzure depolama, service bus ve diğer Azure hizmetleriyle türü erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-223">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="4c7b6-224">Tooupdate requirements.txt emin olun:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-224">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="4c7b6-225">Merhaba değişiklikleri uygulayın:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-225">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="4c7b6-226">TooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="4c7b6-226">Deploy tooAzure</span></span>
<span data-ttu-id="4c7b6-227">bir dağıtım tootrigger, anında iletme hello tooAzure değiştirir:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-227">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="4c7b6-228">Merhaba Merhaba, sanal ortam oluşturma, paketleri yükleme, web.config oluşturma dahil dağıtım betiği çıktısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-228">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="4c7b6-229">Toohello Azure URL tooview değişikliklerinizi göz atın.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-229">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="4c7b6-230">Web uygulaması geliştirme - Mac/Linux - komut satırı</span><span class="sxs-lookup"><span data-stu-id="4c7b6-230">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="4c7b6-231">Kopya hello deposu</span><span class="sxs-lookup"><span data-stu-id="4c7b6-231">Clone hello repository</span></span>
<span data-ttu-id="4c7b6-232">İlk olarak, Azure Portal hello üzerinde sağlanan hello URL'yi kullanarak hello depoyu kopyalayın ve uzak olarak hello Azure deposunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-232">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="4c7b6-233">Daha fazla bilgi için bkz: [yerel Git dağıtımı tooAzure uygulama hizmeti](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="4c7b6-233">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="4c7b6-234">Sanal ortamı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-234">Create virtual environment</span></span>
<span data-ttu-id="4c7b6-235">(Bunu toohello depoya eklemeyin) geliştirme amacıyla yeni bir sanal ortam oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-235">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span>  <span data-ttu-id="4c7b6-236">Sanal ortamlar Hello uygulama üzerinde çalışan her geliştiricinin yerel olarak Kendininkini oluşturacağı şekilde python'daki, değildir.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-236">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="4c7b6-237">Toouse hello web uygulamanız için seçilen Python ile aynı sürümü olduğundan emin olun (runtime.txt veya hello **uygulama ayarları** hello Azure Portal, web uygulamanızın dikey penceresinde).</span><span class="sxs-lookup"><span data-stu-id="4c7b6-237">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="4c7b6-238">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-238">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="4c7b6-239">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-239">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="4c7b6-240">veya pyvenv env</span><span class="sxs-lookup"><span data-stu-id="4c7b6-240">or pyvenv env</span></span>

<span data-ttu-id="4c7b6-241">Uygulamanız için gereken herhangi bir dış paketi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-241">Install any external packages required by your application.</span></span> <span data-ttu-id="4c7b6-242">Sanal ortamınıza hello hello depo tooinstall hello paketleri kökünde hello requirements.txt dosyasını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-242">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="4c7b6-243">Geliştirme sunucusu kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="4c7b6-243">Run using development server</span></span>
<span data-ttu-id="4c7b6-244">Komutu aşağıdaki hello ile Merhaba uygulaması geliştirme sunucusu altında başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-244">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python runserver.py

<span data-ttu-id="4c7b6-245">Merhaba konsol hello URL'si gösterilir ve bağlantı noktası hello sunucu dinler:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-245">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

<span data-ttu-id="4c7b6-246">Sonra web tarayıcısı toothat URL'nizi açın.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-246">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="4c7b6-247">Değişiklik yapma</span><span class="sxs-lookup"><span data-stu-id="4c7b6-247">Make changes</span></span>
<span data-ttu-id="4c7b6-248">Şimdi değişiklikleri toohello uygulama kaynakları ve/veya şablonlarında yapmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-248">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="4c7b6-249">Değişikliklerinizi test ettikten sonra bunları toohello Git deposuna kaydedin:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-249">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="4c7b6-250">Daha fazla paket yükleme</span><span class="sxs-lookup"><span data-stu-id="4c7b6-250">Install more packages</span></span>
<span data-ttu-id="4c7b6-251">Uygulamanızın Python ve Flask ötesinde bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-251">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="4c7b6-252">Pip kullanarak ek paketleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-252">You can install additional packages using pip.</span></span>  <span data-ttu-id="4c7b6-253">Örneğin, tooinstall Merhaba, imkanı sağlayan, Python için Azure SDK tooAzure depolama, service bus ve diğer Azure hizmetleriyle türü erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-253">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="4c7b6-254">Tooupdate requirements.txt emin olun:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-254">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="4c7b6-255">Merhaba değişiklikleri uygulayın:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-255">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="4c7b6-256">TooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="4c7b6-256">Deploy tooAzure</span></span>
<span data-ttu-id="4c7b6-257">bir dağıtım tootrigger, anında iletme hello tooAzure değiştirir:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-257">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="4c7b6-258">Merhaba Merhaba, sanal ortam oluşturma, paketleri yükleme, web.config oluşturma dahil dağıtım betiği çıktısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-258">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="4c7b6-259">Toohello Azure URL tooview değişikliklerinizi göz atın.</span><span class="sxs-lookup"><span data-stu-id="4c7b6-259">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="4c7b6-260">Sorun giderme - Paket Yükleme</span><span class="sxs-lookup"><span data-stu-id="4c7b6-260">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="4c7b6-261">Sorun giderme - Sanal Ortam</span><span class="sxs-lookup"><span data-stu-id="4c7b6-261">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="4c7b6-262">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="4c7b6-262">Next Steps</span></span>
<span data-ttu-id="4c7b6-263">Bu bağlantılar toolearn Flask ve Python araçları hakkında daha fazla bilgi için Visual Studio izleyin:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-263">Follow these links toolearn more about Flask and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="4c7b6-264">[Flask belgeleri]</span><span class="sxs-lookup"><span data-stu-id="4c7b6-264">[Flask Documentation]</span></span>
* <span data-ttu-id="4c7b6-265">[Visual Studio belgeleri için Python Araçları]</span><span class="sxs-lookup"><span data-stu-id="4c7b6-265">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="4c7b6-266">Azure tablo depolaması ve MongoDB kullanma hakkında daha fazla bilgi için:</span><span class="sxs-lookup"><span data-stu-id="4c7b6-266">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="4c7b6-267">[Flask ve Visual Studio için Python araçları ile azure'da MongoDB]</span><span class="sxs-lookup"><span data-stu-id="4c7b6-267">[Flask and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="4c7b6-268">[Flask ve Visual Studio için Python araçları ile azure'da Azure tablo depolaması]</span><span class="sxs-lookup"><span data-stu-id="4c7b6-268">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="4c7b6-269">Daha fazla bilgi için hello Ayrıca bkz. [Python Geliştirici Merkezi](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="4c7b6-269">For more information, see also hello [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="4c7b6-270">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="4c7b6-270">What's changed</span></span>
* <span data-ttu-id="4c7b6-271">Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="4c7b6-271">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Flask ve Visual Studio için Python araçları ile azure'da MongoDB]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure
[Flask ve Visual Studio için Python araçları ile azure'da Azure tablo depolaması]: web-sites-python-ptvs-flask-table-storage.md

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
[Flask belgeleri]: http://flask.pocoo.org/ 

