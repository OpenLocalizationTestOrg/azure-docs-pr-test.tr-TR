---
title: aaaDeploy tooAzure Jenkins eklentisi ile App Service | Microsoft Docs
description: "Nasıl toouse Azure App Service Jenkins eklentisi toodeploy bir Java web uygulaması tooAzure Jenkins içinde bilgi edinin"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 7/24/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 080be7277555ce7d688dccdf38eef309e7a7b194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-plugin"></a><span data-ttu-id="26e59-103">Uygulama hizmeti tooAzure Jenkins eklentisi ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="26e59-103">Deploy tooAzure App Service with Jenkins plugin</span></span> 
<span data-ttu-id="26e59-104">toodeploy bir Java web uygulaması tooAzure, Azure CLI kullanabilir [Jenkins ardışık düzen](/azure/jenkins/execute-cli-jenkins-pipeline) veya yapabilirsiniz hello kullan [Azure App Service Jenkins eklentisi](https://plugins.jenkins.io/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="26e59-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) or you can make use of hello [Azure App Service Jenkins plugin](https://plugins.jenkins.io/azure-app-service).</span></span> <span data-ttu-id="26e59-105">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="26e59-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="26e59-106">Jenkins toodeploy tooAzure FTP aracılığıyla uygulama hizmetini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="26e59-106">Configure Jenkins toodeploy tooAzure App Service through FTP</span></span> 
> * <span data-ttu-id="26e59-107">Docker aracılığıyla Linux'ta Jenkins toodeploy tooAzure uygulama hizmetini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="26e59-107">Configure Jenkins toodeploy tooAzure App Service on Linux through Docker</span></span> 

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="26e59-108">Oluşturma ve yapılandırma Jenkins örneği</span><span class="sxs-lookup"><span data-stu-id="26e59-108">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="26e59-109">Jenkins asıl zaten yoksa, hello ile başlangıç [çözüm şablonu](install-jenkins-solution-template.md), JDK8 ve gerekli eklentileri aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="26e59-109">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes JDK8 and hello following required plugins:</span></span>

* <span data-ttu-id="26e59-110">[Jenkins Git istemcisi eklentisi](https://plugins.jenkins.io/git-client) v.2.4.6</span><span class="sxs-lookup"><span data-stu-id="26e59-110">[Jenkins Git client plugin](https://plugins.jenkins.io/git-client) v.2.4.6</span></span> 
* <span data-ttu-id="26e59-111">[Docker Commons eklentisi](https://plugins.jenkins.io/docker-commons) v.1.4.0</span><span class="sxs-lookup"><span data-stu-id="26e59-111">[Docker Commons Plugin](https://plugins.jenkins.io/docker-commons) v.1.4.0</span></span>
* <span data-ttu-id="26e59-112">[Azure kimlik](https://plugins.jenkins.io/azure-credentials) v.1.2</span><span class="sxs-lookup"><span data-stu-id="26e59-112">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) v.1.2</span></span>
* <span data-ttu-id="26e59-113">[Azure uygulama hizmeti](https://plugins.jenkins.io/azure-app-server) v.0.1</span><span class="sxs-lookup"><span data-stu-id="26e59-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span></span>

<span data-ttu-id="26e59-114">Merhaba uygulama hizmeti eklentisi toodeploy Web uygulamasını Azure App Service tarafından desteklenen tüm dillerde (örneğin, C#, PHP, Java ve node.js vb.) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26e59-114">You can use hello App Service plugin toodeploy Web App in all languages (for instance, C#, PHP, Java, and node.js etc.) supported by Azure App Service.</span></span> <span data-ttu-id="26e59-115">Bu öğreticide, hello örnek Java uygulaması kullanıyoruz [basit Java Web uygulaması için Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="26e59-115">In this tutorial, we are using hello sample Java app, [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="26e59-116">toofork hello depodaki tooyour GitHub hesabı sahibi, hello tıklatın **çatalı** hello üst sağ köşesindeki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="26e59-116">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>  

<span data-ttu-id="26e59-117">Java JDK ve Maven hello Java projesi oluşturmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="26e59-117">Java JDK and Maven are required for building hello Java project.</span></span> <span data-ttu-id="26e59-118">Sürekli tümleştirme için kullanırsanız, hello bileşenleri hello Jenkins asıl veya hello VM Aracısı yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="26e59-118">Make sure you install hello components in hello Jenkins master or hello VM agent if you use one for continuous integration.</span></span> 

<span data-ttu-id="26e59-119">tooinstall, SSH kullanarak toohello Jenkins örneğinde oturum ve hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="26e59-119">tooinstall, log in toohello Jenkins instance using SSH and run hello following commands:</span></span>

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

<span data-ttu-id="26e59-120">TooApp Linux hizmet dağıtmak için tooinstall Docker hello Jenkins ana veya yapı için kullanılan hello VM Aracısı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="26e59-120">For deploying tooApp Service on Linux, you also need tooinstall Docker on hello Jenkins master or hello VM agent used for build.</span></span> <span data-ttu-id="26e59-121">Toothis makale tooinstall Docker bakın: https://docs.docker.com/engine/installation/linux/ubuntu/.</span><span class="sxs-lookup"><span data-stu-id="26e59-121">Refer toothis article tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span></span>

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="26e59-122">Azure hizmet asıl tooJenkins kimlik bilgisi Ekle</span><span class="sxs-lookup"><span data-stu-id="26e59-122">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="26e59-123">Bir Azure hizmet sorumlusu gerekli toodeploy tooAzure ' dir.</span><span class="sxs-lookup"><span data-stu-id="26e59-123">An Azure service principal is needed toodeploy tooAzure.</span></span> 

<ol>
<li><span data-ttu-id="26e59-124">Kullanım [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) veya [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate bir Azure hizmet sorumlusu</span><span class="sxs-lookup"><span data-stu-id="26e59-124">Use [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) or [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate an Azure service principal</span></span></li>
<li><span data-ttu-id="26e59-125">Merhaba Jenkins Pano içinde tıklatın **kimlik bilgileri -> Sistem ->**.</span><span class="sxs-lookup"><span data-stu-id="26e59-125">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="26e59-126">Tıklatın **genel credentials(unrestricted)**.</span><span class="sxs-lookup"><span data-stu-id="26e59-126">Click **Global credentials(unrestricted)**.</span></span></li>
<li><span data-ttu-id="26e59-127">Tıklatın **kimlik bilgilerini eklemek** tooadd hello abonelik kimliği, istemci kimliği, gizli ve OAuth 2.0 belirteç uç noktası doldurarak bir Microsoft Azure hizmet sorumlusu.</span><span class="sxs-lookup"><span data-stu-id="26e59-127">Click **Add Credentials** tooadd a Microsoft Azure service principal by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="26e59-128">Bir kimliği sağlayın **bileşene mySp**, sonraki adımlarda kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="26e59-128">Provide an ID, **mySp**, for use in subsequent steps.</span></span></li>
</ol>

## <a name="azure-app-service-plugin"></a><span data-ttu-id="26e59-129">Azure uygulama hizmeti eklentisi</span><span class="sxs-lookup"><span data-stu-id="26e59-129">Azure App Service plugin</span></span>

<span data-ttu-id="26e59-130">Azure uygulama hizmeti eklentisi v1.0 destekleyen sürekli dağıtım tooAzure Web uygulaması aracılığıyla:</span><span class="sxs-lookup"><span data-stu-id="26e59-130">Azure App Service plugin v1.0 supports continuous deployment tooAzure Web App through:</span></span>

* <span data-ttu-id="26e59-131">Git ve FTP</span><span class="sxs-lookup"><span data-stu-id="26e59-131">Git and FTP</span></span>
* <span data-ttu-id="26e59-132">Linux üzerinde Web uygulaması için docker</span><span class="sxs-lookup"><span data-stu-id="26e59-132">Docker for Web App on Linux</span></span>

## <a name="configure-jenkins-toodeploy-web-app-through-ftp-using-hello-jenkins-dashboard"></a><span data-ttu-id="26e59-133">Jenkins toodeploy hello Jenkins Panoyu kullanarak FTP üzerinden Web uygulaması yapılandırma</span><span class="sxs-lookup"><span data-stu-id="26e59-133">Configure Jenkins toodeploy Web App through FTP using hello Jenkins dashboard</span></span>

<span data-ttu-id="26e59-134">toodeploy, proje tooAzure Web uygulaması derleme yapıtları (örneğin, Java .war dosyası) karşıya yükleyebilir Git veya FTP kullanma.</span><span class="sxs-lookup"><span data-stu-id="26e59-134">toodeploy your project tooAzure Web App, you can upload your build artifacts (for example, .war file in Java) using Git or FTP.</span></span>

<span data-ttu-id="26e59-135">Jenkins hello işinde ayarlamadan önce çalışan hello Java uygulaması için bir Azure uygulama hizmeti planı ve bir Web uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="26e59-135">Before setting up hello job in Jenkins, you need an Azure App Service plan and a Web App for running hello Java app.</span></span>


1. <span data-ttu-id="26e59-136">Merhaba ile bir Azure uygulama hizmeti planı oluştur **serbest** fiyatlandırma katmanı hello kullanarak [az uygulama hizmeti planı oluşturma](/cli/azure/appservice/plan#create) CLI komutu.</span><span class="sxs-lookup"><span data-stu-id="26e59-136">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="26e59-137">Merhaba uygulama hizmeti planı hello kullanılan fiziksel kaynakları toohost uygulamalarınızı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="26e59-137">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="26e59-138">Tooan uygulama hizmeti planı atanan tüm uygulamaların birden fazla uygulama barındırdığında toosave maliyet izin vererek, bu kaynakları paylaşır.</span><span class="sxs-lookup"><span data-stu-id="26e59-138">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span>
2. <span data-ttu-id="26e59-139">Bir Web Uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="26e59-139">Create a Web App.</span></span> <span data-ttu-id="26e59-140">Ya da kullanım hello yapabilecekleriniz [Azure portal](/azure/app-service-web/web-sites-configure) veya kullanım hello aşağıdaki Az CLI komutu:</span><span class="sxs-lookup"><span data-stu-id="26e59-140">You can either use hello [Azure portal](/azure/app-service-web/web-sites-configure) or use hello following Az CLI command:</span></span>
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. <span data-ttu-id="26e59-141">Uygulamanız gereken hello Java Çalışma zamanı yapılandırmasını ayarladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="26e59-141">Make sure you set up hello Java runtime configuration that your app needs.</span></span> <span data-ttu-id="26e59-142">Azure CLI komutu aşağıdaki hello üzerinde yeni bir Java 8 JDK hello web uygulama toorun yapılandırır ve [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="26e59-142">hello following Azure CLI command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-hello-jenkins-job"></a><span data-ttu-id="26e59-143">Merhaba Jenkins iş ayarlayın</span><span class="sxs-lookup"><span data-stu-id="26e59-143">Set up hello Jenkins job</span></span>


1. <span data-ttu-id="26e59-144">Yeni bir **freestyle** Jenkins Pano projesinde</span><span class="sxs-lookup"><span data-stu-id="26e59-144">Create a new **freestyle** project in Jenkins Dashboard</span></span>
2. <span data-ttu-id="26e59-145">Yapılandırma **kaynak kodu Yönetimi** toouse, yerel, çatalı [basit Java Web uygulaması için Azure](https://github.com/azure-devops/javawebappsample) hello sağlayarak **depo URL'si**.</span><span class="sxs-lookup"><span data-stu-id="26e59-145">Configure **Source Code Management** toouse your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing hello **Repository URL**.</span></span> <span data-ttu-id="26e59-146">Örneğin: http://github.com/&lt;yourID > / javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="26e59-146">For example: http://github.com/&lt;yourID>/javawebappsample.</span></span>
3. <span data-ttu-id="26e59-147">Maven kullanarak bir derleme adımı toobuild hello projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="26e59-147">Add a Build step toobuild hello project using Maven.</span></span> <span data-ttu-id="26e59-148">Ekleyerek bunu bir **Kabuk yürütme**.</span><span class="sxs-lookup"><span data-stu-id="26e59-148">Do so by adding an **Execute shell**.</span></span> <span data-ttu-id="26e59-149">Bu örnekte, bir ek adım toorename hello *.war dosyasında hedef klasörü tooROOT.war gerekir.</span><span class="sxs-lookup"><span data-stu-id="26e59-149">For this example, we need an additional step toorename hello *.war file in target folder tooROOT.war.</span></span>   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. <span data-ttu-id="26e59-150">Bir oluşturma sonrası eylemi seçerek eklemek **Azure Web uygulaması yayımlama**.</span><span class="sxs-lookup"><span data-stu-id="26e59-150">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
5. <span data-ttu-id="26e59-151">Tedarik, "bileşene mySp", önceki adımda depolanan hello Azure hizmet sorumlusu.</span><span class="sxs-lookup"><span data-stu-id="26e59-151">Supply, "mySp", hello Azure service principal stored in previous step.</span></span>
6. <span data-ttu-id="26e59-152">İçinde **uygulama yapılandırması** bölümünde, aboneliğinizde hello kaynak grubu ve web uygulaması seçin.</span><span class="sxs-lookup"><span data-stu-id="26e59-152">In **App Configuration** section, choose hello resource group and web app in your subscription.</span></span> <span data-ttu-id="26e59-153">Merhaba eklentisi otomatik olarak algılar hello Web uygulaması Windows olup olmadığını veya Linux tabanlı.</span><span class="sxs-lookup"><span data-stu-id="26e59-153">hello plugin automatically detects whether hello Web App is Windows or Linux-based.</span></span> <span data-ttu-id="26e59-154">Bir Windows tabanlı Web uygulaması için "Yayımlama dosyalar" Merhaba seçeneği sunulur.</span><span class="sxs-lookup"><span data-stu-id="26e59-154">For a Windows-based Web App, hello option "Publish Files" is presented.</span></span>
7. <span data-ttu-id="26e59-155">Dolgu hello dosyalarında istediğiniz toodeploy (Java kullanıyorsanız, örneğin, bir war package.) Kaynak dizin ve hedef dizin isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="26e59-155">Fill in hello files you want toodeploy (for example, a war package if you're using Java.) Source Directory and Target Directory are optional.</span></span> <span data-ttu-id="26e59-156">Merhaba parametreler toospecify kaynak ve hedef klasörler, dosyaları karşıya yüklenirken sağlar.</span><span class="sxs-lookup"><span data-stu-id="26e59-156">hello parameters allow you toospecify source and target folders when uploading files.</span></span> <span data-ttu-id="26e59-157">Azure'da Java web uygulaması Tomcat Server'da çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="26e59-157">Java web app on Azure is run in a Tomcat server.</span></span> <span data-ttu-id="26e59-158">Karşıya yüklediğiniz şekilde, paket webapps klasörüne war.</span><span class="sxs-lookup"><span data-stu-id="26e59-158">So you upload you war package to webapps folder.</span></span> <span data-ttu-id="26e59-159">Bu örnek için set **kaynak dizin** çok "hedef" ve "webapps" sağlamak için **hedef dizin**.</span><span class="sxs-lookup"><span data-stu-id="26e59-159">For this example, set **Source Directory** too"target" and supply "webapps" for **Target Directory**.</span></span>
8. <span data-ttu-id="26e59-160">Üretim dışında toodeploy tooa yuvası isterseniz, ayrıca ayarlayabilirsiniz **yuvası** adı.</span><span class="sxs-lookup"><span data-stu-id="26e59-160">If you want toodeploy tooa slot other than production, you can also set **Slot** Name.</span></span>
9. <span data-ttu-id="26e59-161">Merhaba projeyi kaydedin ve onu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="26e59-161">Save hello project and build it.</span></span> <span data-ttu-id="26e59-162">Yapı tamamlandığında, web uygulamanızın dağıtılan tooAzure olur.</span><span class="sxs-lookup"><span data-stu-id="26e59-162">Your web app is deployed tooAzure when build is complete.</span></span>

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a><span data-ttu-id="26e59-163">Jenkins ardışık düzen kullanarak FTP üzerinden Web uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="26e59-163">Deploy Web App through FTP using Jenkins pipeline</span></span>

<span data-ttu-id="26e59-164">Merhaba eklentisi ardışık düzeni için hazır olur.</span><span class="sxs-lookup"><span data-stu-id="26e59-164">hello plugin is pipeline-ready.</span></span> <span data-ttu-id="26e59-165">Merhaba GitHub deposuna tooa örnek başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="26e59-165">You can refer tooa sample in hello GitHub repo.</span></span>

1. <span data-ttu-id="26e59-166">GitHub web kullanıcı Arabirimi, açık **Jenkinsfile_ftp_plugin** dosya.</span><span class="sxs-lookup"><span data-stu-id="26e59-166">In GitHub web UI, open **Jenkinsfile_ftp_plugin** file.</span></span> <span data-ttu-id="26e59-167">Hello Kurşun Kalem simgesini tooedit, bu dosya tooupdate hello kaynak grubu ve adı, web uygulamanızın 11 ve 12 satırındaki'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="26e59-167">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="26e59-168">Jenkins Örneğinizde satır 14 tooupdate kimlik bilgisi Kimliğini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="26e59-168">Change line 14 tooupdate credential ID in your Jenkins instance.</span></span>    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a><span data-ttu-id="26e59-169">Jenkins işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="26e59-169">Create a Jenkins pipeline</span></span>

1. <span data-ttu-id="26e59-170">Jenkins bir web tarayıcısında açın, **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="26e59-170">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="26e59-171">Merhaba işi için bir ad sağlayın ve seçin **ardışık düzen**.</span><span class="sxs-lookup"><span data-stu-id="26e59-171">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="26e59-172">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="26e59-172">Click **OK**.</span></span>
3. <span data-ttu-id="26e59-173">Merhaba tıklatın **ardışık düzen** sekmesinde sonraki.</span><span class="sxs-lookup"><span data-stu-id="26e59-173">Click hello **Pipeline** tab next.</span></span>
4. <span data-ttu-id="26e59-174">İçin **tanımı**seçin **kanal SCM betikten**.</span><span class="sxs-lookup"><span data-stu-id="26e59-174">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="26e59-175">İçin **SCM**seçin **Git**.</span><span class="sxs-lookup"><span data-stu-id="26e59-175">For **SCM**, select **Git**.</span></span> <span data-ttu-id="26e59-176">Merhaba GitHub URL forked depodaki girin: https:&lt;forked depodaki > .git</span><span class="sxs-lookup"><span data-stu-id="26e59-176">Enter hello GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span>
6. <span data-ttu-id="26e59-177">Güncelleştirme **betik yolu** çok "Jenkinsfile_ftp_plugin"</span><span class="sxs-lookup"><span data-stu-id="26e59-177">Update **Script Path** too"Jenkinsfile_ftp_plugin"</span></span>
7. <span data-ttu-id="26e59-178">Tıklatın **kaydetmek** ve çalışma hello işi.</span><span class="sxs-lookup"><span data-stu-id="26e59-178">Click **Save** and run hello job.</span></span>

## <a name="configure-jenkins-toodeploy-web-app-on-linux-through-docker"></a><span data-ttu-id="26e59-179">Docker aracılığıyla Linux'ta Jenkins toodeploy Web uygulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="26e59-179">Configure Jenkins toodeploy Web App on Linux through Docker</span></span>

<span data-ttu-id="26e59-180">Git/FTP dışında Linux üzerinde Web uygulaması Docker kullanarak dağıtımı destekler.</span><span class="sxs-lookup"><span data-stu-id="26e59-180">Apart from Git/FTP, Web App on Linux supports deployment using Docker.</span></span> <span data-ttu-id="26e59-181">Docker, kullanarak toodeploy tooprovide docker görüntüsüne web uygulamanızı hizmet çalışma zamanı paketleri bir Dockerfile gerekir.</span><span class="sxs-lookup"><span data-stu-id="26e59-181">toodeploy using Docker, you need tooprovide a Dockerfile that packages your web app with service runtime into a docker image.</span></span> <span data-ttu-id="26e59-182">Ardından hello eklentisi hello görüntü oluşturur, tooa docker kayıt defteri iter ve hello görüntü tooyour web uygulamasına dağıtır.</span><span class="sxs-lookup"><span data-stu-id="26e59-182">Then hello plugin builds hello image, pushes it tooa docker registry and deploys hello image tooyour web app.</span></span>

<span data-ttu-id="26e59-183">Web uygulaması Linux'ta geleneksel yolları Git ve FTP gibi ancak yalnızca yerleşik dilleri (.NET Core, Node.js, PHP ve Ruby) da destekler.</span><span class="sxs-lookup"><span data-stu-id="26e59-183">Web App on Linux also supports traditional ways like Git and FTP, but only for built-in languages (.NET Core, Node.js, PHP, and Ruby).</span></span> <span data-ttu-id="26e59-184">Diğer diller için toopackage, uygulama kodu ve hizmet çalışma zamanı birlikte docker görüntüsüne gerekir ve docker toodeploy kullanın.</span><span class="sxs-lookup"><span data-stu-id="26e59-184">For other languages, you need toopackage your application code and service runtime together into a docker image and use docker toodeploy.</span></span>

<span data-ttu-id="26e59-185">Jenkins hello işinde ayarlamadan önce bir Azure uygulama hizmeti Linux'ta gerekir.</span><span class="sxs-lookup"><span data-stu-id="26e59-185">Before setting up hello job in Jenkins, you need an Azure app service on Linux.</span></span> <span data-ttu-id="26e59-186">Bir kapsayıcı kayıt defteri zamanda gerekli toostore ve özel Docker kapsayıcısı görüntülerinizi yönetin.</span><span class="sxs-lookup"><span data-stu-id="26e59-186">A container registry is also needed toostore and manage your private Docker container images.</span></span> <span data-ttu-id="26e59-187">DockerHub kullanabilirsiniz; Bu örnek için Azure kapsayıcı kayıt defteri kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="26e59-187">You can use DockerHub; we are using Azure Container Registry for this example.</span></span>

* <span data-ttu-id="26e59-188">Merhaba adımları izleyebilirsiniz [burada](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate Linux üzerinde bir Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="26e59-188">You can follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate a Web App on Linux</span></span> 
* <span data-ttu-id="26e59-189">Azure kapsayıcı kayıt defteri olan bir yönetilen [Docker kayıt defteri] göre (https://docs.docker.com/registry/) hizmeti hello açık kaynak Docker kayıt defteri 2.0.</span><span class="sxs-lookup"><span data-stu-id="26e59-189">Azure Container Registry is a managed [Docker registry] (https://docs.docker.com/registry/) service based on hello open-source Docker Registry 2.0.</span></span> <span data-ttu-id="26e59-190">[Burada] Hello adımları izleyin (/ azure/container-registry/container-registry-get-started-azure-cli) konusunda daha fazla yardım için toodo şekilde.</span><span class="sxs-lookup"><span data-stu-id="26e59-190">Follow hello steps [here] (/azure/container-registry/container-registry-get-started-azure-cli) for more guidance on how toodo so.</span></span> <span data-ttu-id="26e59-191">DockerHub de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26e59-191">You can also use DockerHub.</span></span>

### <a name="toodeploy-using-docker"></a><span data-ttu-id="26e59-192">docker kullanarak toodeploy:</span><span class="sxs-lookup"><span data-stu-id="26e59-192">toodeploy using docker:</span></span>

1. <span data-ttu-id="26e59-193">Yeni bir Serbest stilde projesi Jenkins panosunda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="26e59-193">Create a new freestyle project in Jenkins Dashboard.</span></span>
2. <span data-ttu-id="26e59-194">Yapılandırma **kaynak kodu Yönetimi** toouse, yerel, çatalı [basit Java Web uygulaması için Azure](https://github.com/azure-devops/javawebappsample) hello sağlayarak **depo URL'si**.</span><span class="sxs-lookup"><span data-stu-id="26e59-194">Configure **Source Code Management** toouse your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing hello **Repository URL**.</span></span> <span data-ttu-id="26e59-195">Örneğin: http://github.com/&lt;yourid > / javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="26e59-195">For example: http://github.com/&lt;yourid>/javawebappsample.</span></span>
<span data-ttu-id="26e59-196">Maven kullanarak bir derleme adımı toobuild hello projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="26e59-196">Add a Build step toobuild hello project using Maven.</span></span> <span data-ttu-id="26e59-197">Ekleyerek bunu bir **Kabuk yürütme** ve satırında aşağıdaki hello ekleyin **komutu**:</span><span class="sxs-lookup"><span data-stu-id="26e59-197">Do so by adding an **Execute shell** and add hello following line in **Command**:</span></span>    
```bash
mvn clean package
```

3. <span data-ttu-id="26e59-198">Bir oluşturma sonrası eylemi seçerek eklemek **Azure Web uygulaması yayımlama**.</span><span class="sxs-lookup"><span data-stu-id="26e59-198">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
4. <span data-ttu-id="26e59-199">Tedarik, **bileşene mySp**, önceki adımda Azure kimlik bilgileri olarak depolanan hello Azure hizmet sorumlusu.</span><span class="sxs-lookup"><span data-stu-id="26e59-199">Supply, **mySp**, hello Azure service principal stored in previous step as Azure Credentials.</span></span>
5. <span data-ttu-id="26e59-200">İçinde **uygulama yapılandırması** bölümünde, aboneliğinizde hello kaynak grubu ve Linux web uygulaması seçin.</span><span class="sxs-lookup"><span data-stu-id="26e59-200">In **App Configuration** section, choose hello resource group and a Linux web app in your subscription.</span></span>
6. <span data-ttu-id="26e59-201">Seçin Docker yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="26e59-201">Choose Publish via Docker.</span></span>
7. <span data-ttu-id="26e59-202">Doldurmak **Dockerfile** yolu.</span><span class="sxs-lookup"><span data-stu-id="26e59-202">Fill in **Dockerfile** path.</span></span> <span data-ttu-id="26e59-203">Merhaba varsayılan koruyabilirsiniz "/ Dockerfile" için **Docker kayıt defteri URL**, https:// hello biçiminde sağlar&lt;myRegistry >. Azure kapsayıcı kayıt defteri kullanırsanız azurecr.io.</span><span class="sxs-lookup"><span data-stu-id="26e59-203">You can keep hello default "/Dockerfile" For **Docker registry URL**, supply in hello format of https://&lt;myRegistry>.azurecr.io if you use Azure Container Registry.</span></span> <span data-ttu-id="26e59-204">DockerHub kullanıyorsanız, boş bırakın.</span><span class="sxs-lookup"><span data-stu-id="26e59-204">Leave it blank if you use DockerHub.</span></span>
8. <span data-ttu-id="26e59-205">İçin **kayıt defteri kimlik bilgilerini**, hello Azure kapsayıcı kayıt defteri için hello kimlik bilgisi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="26e59-205">For **Registry credentials**, add hello credential for hello Azure Container Registry.</span></span> <span data-ttu-id="26e59-206">Azure CLI komutları aşağıdaki hello çalıştırarak hello kullanıcı kimliği ve parola alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26e59-206">You can get hello userid and password by running hello following commands in Azure CLI.</span></span> <span data-ttu-id="26e59-207">Merhaba ilk komut hello yönetici hesabını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="26e59-207">hello first command enables hello administrator account.</span></span>    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. <span data-ttu-id="26e59-208">Merhaba docker görüntü adı ve etiketinde **Gelişmiş** sekmesi isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="26e59-208">hello docker image name and tag in **Advanced** tab are optional.</span></span> <span data-ttu-id="26e59-209">Varsayılan olarak, görüntü adı elde edilir hello görüntüden Azure portal (inç Docker kapsayıcısı ayarı) hello etiketinde yapılandırılmış ad $BUILD_NUMBER oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="26e59-209">By default, image name is obtained from hello image name you configured in Azure portal (in Docker Container setting.) hello tag is generated from $BUILD_NUMBER.</span></span> <span data-ttu-id="26e59-210">Emin olun ya da Azure portalında hello görüntü adı belirtin veya için bir değer sağlamanız **Docker görüntü** içinde **Gelişmiş** sekmesi. Bu örnekte, tedarik "&lt;yourRegistry >.azurecr.io/calculator" için **Docker görüntü** bırakıp **Docker resim etiketi** boş.</span><span class="sxs-lookup"><span data-stu-id="26e59-210">Make sure you specify hello image name in either Azure portal or supply a value for **Docker Image** in **Advanced** tab. For this example, supply "&lt;yourRegistry>.azurecr.io/calculator" for **Docker image** and leave **Docker Image Tag** blank.</span></span>
10. <span data-ttu-id="26e59-211">Yerleşik Docker görüntü ayarını kullanırsanız Not dağıtımı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="26e59-211">Note deployment fails if you use built-in Docker image setting.</span></span> <span data-ttu-id="26e59-212">Docker config toouse özel görüntüyü Azure portalında Docker kapsayıcısı ayarında değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="26e59-212">Make sure you change docker config toouse custom image in Docker Container setting in Azure portal.</span></span> <span data-ttu-id="26e59-213">Yerleşik görüntü için dosya karşıya yükleme yaklaşımını toodeploy kullanın.</span><span class="sxs-lookup"><span data-stu-id="26e59-213">For built-in image, use file upload approach toodeploy.</span></span>
11. <span data-ttu-id="26e59-214">Benzer toofile karşıya yükleme yaklaşım, üretim dışındaki başka bir yuvaya seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26e59-214">Similar toofile upload approach, you can choose a different slot other than production.</span></span>
12. <span data-ttu-id="26e59-215">Kaydedin ve Merhaba projeyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="26e59-215">Save and build hello project.</span></span> <span data-ttu-id="26e59-216">Kapsayıcı görüntünüzü tooyour kayıt defteri gönderilir ve web uygulama bakın.</span><span class="sxs-lookup"><span data-stu-id="26e59-216">You see your container image is pushed tooyour registry and web app is deployed.</span></span>

### <a name="deploy-tooweb-app-on-linux-through-docker-using-jenkins-pipeline"></a><span data-ttu-id="26e59-217">TooWeb Docker kullanılarak Jenkins ardışık düzeni aracılığıyla Linux'ta uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="26e59-217">Deploy tooWeb App on Linux through Docker using Jenkins pipeline</span></span>

1. <span data-ttu-id="26e59-218">GitHub web kullanıcı Arabirimi, açık **Jenkinsfile_container_plugin** dosya.</span><span class="sxs-lookup"><span data-stu-id="26e59-218">In GitHub web UI, open **Jenkinsfile_container_plugin** file.</span></span> <span data-ttu-id="26e59-219">Hello Kurşun Kalem simgesini tooedit, bu dosya tooupdate hello kaynak grubu ve adı, web uygulamanızın 11 ve 12 satırındaki'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="26e59-219">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="26e59-220">Satır 13 tooyour kapsayıcı kayıt sunucusunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="26e59-220">Change line 13 tooyour container registry server</span></span>    
```java
def registryServer = '<registryURL>'
```    

3. <span data-ttu-id="26e59-221">Satır 16 tooupdate kimlik bilgisi kimliği Jenkins Örneğinizde değiştirme</span><span class="sxs-lookup"><span data-stu-id="26e59-221">Change line 16 tooupdate credential ID in your Jenkins instance</span></span>    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a><span data-ttu-id="26e59-222">Jenkins işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="26e59-222">Create Jenkins pipeline</span></span>    

1. <span data-ttu-id="26e59-223">Jenkins bir web tarayıcısında açın, **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="26e59-223">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="26e59-224">Merhaba işi için bir ad sağlayın ve seçin **ardışık düzen**.</span><span class="sxs-lookup"><span data-stu-id="26e59-224">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="26e59-225">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="26e59-225">Click **OK**.</span></span>
3. <span data-ttu-id="26e59-226">Merhaba tıklatın **ardışık düzen** sekmesinde sonraki.</span><span class="sxs-lookup"><span data-stu-id="26e59-226">Click hello **Pipeline** tab next.</span></span>
4. <span data-ttu-id="26e59-227">İçin **tanımı**seçin **kanal SCM betikten**.</span><span class="sxs-lookup"><span data-stu-id="26e59-227">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="26e59-228">İçin **SCM**seçin **Git**.</span><span class="sxs-lookup"><span data-stu-id="26e59-228">For **SCM**, select **Git**.</span></span>
6. <span data-ttu-id="26e59-229">Merhaba GitHub URL forked depodaki girin: https:&lt;forked depodaki > .git</span><span class="sxs-lookup"><span data-stu-id="26e59-229">Enter hello GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span></li>
<span data-ttu-id="26e59-230">7, güncelleştirme **betik yolu** çok "Jenkinsfile_container_plugin"</span><span class="sxs-lookup"><span data-stu-id="26e59-230">7, Update **Script Path** too"Jenkinsfile_container_plugin"</span></span>
8. <span data-ttu-id="26e59-231">Tıklatın **kaydetmek** ve çalışma hello işi.</span><span class="sxs-lookup"><span data-stu-id="26e59-231">Click **Save** and run hello job.</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="26e59-232">Web uygulamanızı doğrulayın</span><span class="sxs-lookup"><span data-stu-id="26e59-232">Verify your web app</span></span>

1. <span data-ttu-id="26e59-233">tooverify hello WAR dosyası başarıyla dağıtılan tooyour web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="26e59-233">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="26e59-234">Bir web tarayıcısı açın.</span><span class="sxs-lookup"><span data-stu-id="26e59-234">Open a web browser.</span></span>
2. <span data-ttu-id="26e59-235">Toohttp gidin: / /&lt;app_name >.azurewebsites.net/api/calculator/ping görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="26e59-235">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping You see:</span></span>    
     <span data-ttu-id="26e59-236">TooJava Web uygulaması'na Hoş Geldiniz!!!</span><span class="sxs-lookup"><span data-stu-id="26e59-236">Welcome tooJava Web App!!!</span></span> <span data-ttu-id="26e59-237">Bu güncelleştirilmiş!</span><span class="sxs-lookup"><span data-stu-id="26e59-237">This is updated!</span></span>
   <span data-ttu-id="26e59-238">Sun Haz 17 16:39:10 UTC 2017</span><span class="sxs-lookup"><span data-stu-id="26e59-238">Sun Jun 17 16:39:10 UTC 2017</span></span>
3. <span data-ttu-id="26e59-239">Toohttp gidin: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (değiştirin &lt;x > ve &lt;y > sayılar içeren) tooget hello toplamını x ve y</span><span class="sxs-lookup"><span data-stu-id="26e59-239">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>        
    ![Hesaplayıcı: Ekle](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a><span data-ttu-id="26e59-241">Linux için uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="26e59-241">For App service on Linux</span></span>

* <span data-ttu-id="26e59-242">tooverify, Azure CLI'da çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="26e59-242">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="26e59-243">Sonuç aşağıdaki hello alın:</span><span class="sxs-lookup"><span data-stu-id="26e59-243">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="26e59-244">Toohttp gidin: / /&lt;app_name >.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="26e59-244">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="26e59-245">Selamlama iletisine bakın:</span><span class="sxs-lookup"><span data-stu-id="26e59-245">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="26e59-246">Toohttp gidin: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (değiştirin &lt;x > ve &lt;y > sayılar içeren) tooget hello toplamını x ve y</span><span class="sxs-lookup"><span data-stu-id="26e59-246">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="26e59-247">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="26e59-247">Next steps</span></span>

<span data-ttu-id="26e59-248">Bu öğreticide, hello Azure uygulama hizmeti eklentisi toodeploy tooAzure kullanın.</span><span class="sxs-lookup"><span data-stu-id="26e59-248">In this tutorial, you use hello Azure App Service plugin toodeploy tooAzure.</span></span>

<span data-ttu-id="26e59-249">Size nasıl öğrenilen için:</span><span class="sxs-lookup"><span data-stu-id="26e59-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="26e59-250">Jenkins toodeploy FTP aracılığıyla Azure uygulama hizmeti yapılandırın</span><span class="sxs-lookup"><span data-stu-id="26e59-250">Configure Jenkins toodeploy Azure App Service through FTP</span></span> 
> * <span data-ttu-id="26e59-251">Docker aracılığıyla Linux'ta Jenkins toodeploy tooAzure uygulama hizmetini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="26e59-251">Configure Jenkins toodeploy tooAzure App Service on Linux through Docker</span></span> 
