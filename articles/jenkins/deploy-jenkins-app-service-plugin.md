---
title: "Jenkins eklentisi ile Azure App Service'e dağıtma | Microsoft Docs"
description: "Java web uygulaması Jenkins Azure'da dağıtmak için Azure App Service Jenkins eklentisi kullanmayı öğrenin"
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
ms.openlocfilehash: 646daad1785f3de067544b6dd38abfcb6bc67d4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-app-service-with-jenkins-plugin"></a><span data-ttu-id="53b41-103">Jenkins eklentisi ile Azure App Service'e dağıtma</span><span class="sxs-lookup"><span data-stu-id="53b41-103">Deploy to Azure App Service with Jenkins plugin</span></span> 
<span data-ttu-id="53b41-104">Java web uygulaması Azure'a dağıtmak için Azure CLI kullanabileceğiniz [Jenkins ardışık düzen](/azure/jenkins/execute-cli-jenkins-pipeline) veya yapabileceğiniz kullanımı [Azure App Service Jenkins eklentisi](https://plugins.jenkins.io/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="53b41-104">To deploy a Java web app to Azure, you can use Azure CLI in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) or you can make use of the [Azure App Service Jenkins plugin](https://plugins.jenkins.io/azure-app-service).</span></span> <span data-ttu-id="53b41-105">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="53b41-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="53b41-106">FTP aracılığıyla Azure uygulama hizmeti dağıtmak için Jenkins yapılandırın</span><span class="sxs-lookup"><span data-stu-id="53b41-106">Configure Jenkins to deploy to Azure App Service through FTP</span></span> 
> * <span data-ttu-id="53b41-107">Azure uygulama hizmeti Docker aracılığıyla Linux'ta dağıtmak için Jenkins yapılandırın</span><span class="sxs-lookup"><span data-stu-id="53b41-107">Configure Jenkins to deploy to Azure App Service on Linux through Docker</span></span> 

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="53b41-108">Oluşturma ve yapılandırma Jenkins örneği</span><span class="sxs-lookup"><span data-stu-id="53b41-108">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="53b41-109">Jenkins asıl zaten yoksa başlayın [çözüm şablonu](install-jenkins-solution-template.md), JDK8 ve aşağıdaki gerekli eklentileri içerir:</span><span class="sxs-lookup"><span data-stu-id="53b41-109">If you do not already have a Jenkins master, start with the [Solution Template](install-jenkins-solution-template.md), which includes JDK8 and the following required plugins:</span></span>

* <span data-ttu-id="53b41-110">[Jenkins Git istemcisi eklentisi](https://plugins.jenkins.io/git-client) v.2.4.6</span><span class="sxs-lookup"><span data-stu-id="53b41-110">[Jenkins Git client plugin](https://plugins.jenkins.io/git-client) v.2.4.6</span></span> 
* <span data-ttu-id="53b41-111">[Docker Commons eklentisi](https://plugins.jenkins.io/docker-commons) v.1.4.0</span><span class="sxs-lookup"><span data-stu-id="53b41-111">[Docker Commons Plugin](https://plugins.jenkins.io/docker-commons) v.1.4.0</span></span>
* <span data-ttu-id="53b41-112">[Azure kimlik](https://plugins.jenkins.io/azure-credentials) v.1.2</span><span class="sxs-lookup"><span data-stu-id="53b41-112">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) v.1.2</span></span>
* <span data-ttu-id="53b41-113">[Azure uygulama hizmeti](https://plugins.jenkins.io/azure-app-server) v.0.1</span><span class="sxs-lookup"><span data-stu-id="53b41-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span></span>

<span data-ttu-id="53b41-114">Uygulama hizmeti eklentisi, Web uygulamasını Azure App Service tarafından desteklenen tüm dillerde (örneğin, C#, PHP, Java ve node.js vb.) dağıtmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53b41-114">You can use the App Service plugin to deploy Web App in all languages (for instance, C#, PHP, Java, and node.js etc.) supported by Azure App Service.</span></span> <span data-ttu-id="53b41-115">Bu öğreticide, örnek Java uygulaması kullanıyoruz [basit Java Web uygulaması için Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="53b41-115">In this tutorial, we are using the sample Java app, [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="53b41-116">Kendi GitHub hesabınızda depoyu çatallaştırma için tıklatın **çatalı** sağ üst köşesindeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="53b41-116">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>  

<span data-ttu-id="53b41-117">Java JDK ve Maven Java projesi oluşturmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="53b41-117">Java JDK and Maven are required for building the Java project.</span></span> <span data-ttu-id="53b41-118">Sürekli tümleştirme için kullanırsanız, bileşenlerin Jenkins asıl veya VM Aracısı yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="53b41-118">Make sure you install the components in the Jenkins master or the VM agent if you use one for continuous integration.</span></span> 

<span data-ttu-id="53b41-119">Yüklemek için SSH kullanarak Jenkins örneğine oturum açın ve aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="53b41-119">To install, log in to the Jenkins instance using SSH and run the following commands:</span></span>

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

<span data-ttu-id="53b41-120">Uygulama hizmeti Linux'ta dağıtmak için aynı zamanda Docker Jenkins asıl veya yapı için kullanılan VM aracısı yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="53b41-120">For deploying to App Service on Linux, you also need to install Docker on the Jenkins master or the VM agent used for build.</span></span> <span data-ttu-id="53b41-121">Docker yüklemek için bu makaleye bakın: https://docs.docker.com/engine/installation/linux/ubuntu/.</span><span class="sxs-lookup"><span data-stu-id="53b41-121">Refer to this article to install Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span></span>

## <a name="add-azure-service-principal-to-jenkins-credential"></a><span data-ttu-id="53b41-122">Azure hizmet sorumlusu için Jenkins kimlik bilgileri ekleme</span><span class="sxs-lookup"><span data-stu-id="53b41-122">Add Azure service principal to Jenkins credential</span></span>

<span data-ttu-id="53b41-123">Bir Azure hizmet sorumlusu Azure'a dağıtmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="53b41-123">An Azure service principal is needed to deploy to Azure.</span></span> 

<ol>
<li><span data-ttu-id="53b41-124">Kullanım [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) veya [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) bir Azure hizmet sorumlusu oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="53b41-124">Use [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) or [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) to create an Azure service principal</span></span></li>
<li><span data-ttu-id="53b41-125">Jenkins Pano içinde tıklatın **kimlik bilgileri -> Sistem ->**.</span><span class="sxs-lookup"><span data-stu-id="53b41-125">Within the Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="53b41-126">Tıklatın **genel credentials(unrestricted)**.</span><span class="sxs-lookup"><span data-stu-id="53b41-126">Click **Global credentials(unrestricted)**.</span></span></li>
<li><span data-ttu-id="53b41-127">Tıklatın **kimlik bilgilerini eklemek** abonelik kimliği, istemci kimliği, gizli ve OAuth 2.0 belirteç uç noktası doldurarak bir Microsoft Azure hizmet sorumlusu eklemek için.</span><span class="sxs-lookup"><span data-stu-id="53b41-127">Click **Add Credentials** to add a Microsoft Azure service principal by filling out the Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="53b41-128">Bir kimliği sağlayın **bileşene mySp**, sonraki adımlarda kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="53b41-128">Provide an ID, **mySp**, for use in subsequent steps.</span></span></li>
</ol>

## <a name="azure-app-service-plugin"></a><span data-ttu-id="53b41-129">Azure uygulama hizmeti eklentisi</span><span class="sxs-lookup"><span data-stu-id="53b41-129">Azure App Service plugin</span></span>

<span data-ttu-id="53b41-130">Azure uygulama hizmeti eklentisi v1.0 Azure Web uygulaması için sürekli dağıtım destekler:</span><span class="sxs-lookup"><span data-stu-id="53b41-130">Azure App Service plugin v1.0 supports continuous deployment to Azure Web App through:</span></span>

* <span data-ttu-id="53b41-131">Git ve FTP</span><span class="sxs-lookup"><span data-stu-id="53b41-131">Git and FTP</span></span>
* <span data-ttu-id="53b41-132">Linux üzerinde Web uygulaması için docker</span><span class="sxs-lookup"><span data-stu-id="53b41-132">Docker for Web App on Linux</span></span>

## <a name="configure-jenkins-to-deploy-web-app-through-ftp-using-the-jenkins-dashboard"></a><span data-ttu-id="53b41-133">Jenkins Panoyu kullanarak FTP üzerinden Web uygulaması dağıtma Jenkins yapılandırın</span><span class="sxs-lookup"><span data-stu-id="53b41-133">Configure Jenkins to deploy Web App through FTP using the Jenkins dashboard</span></span>

<span data-ttu-id="53b41-134">Projenizi Azure Web uygulamasına dağıtmak için derleme yapıtları (örneğin, Java .war dosyası) karşıya yükleyebilir Git veya FTP kullanma.</span><span class="sxs-lookup"><span data-stu-id="53b41-134">To deploy your project to Azure Web App, you can upload your build artifacts (for example, .war file in Java) using Git or FTP.</span></span>

<span data-ttu-id="53b41-135">Jenkins işinde ayarlamadan önce Azure App Service planı ve bir Web uygulaması Java uygulaması çalıştırmak için gerekir.</span><span class="sxs-lookup"><span data-stu-id="53b41-135">Before setting up the job in Jenkins, you need an Azure App Service plan and a Web App for running the Java app.</span></span>


1. <span data-ttu-id="53b41-136">İle bir Azure uygulama hizmeti planı oluştur **serbest** fiyatlandırma katmanı kullanarak [az uygulama hizmeti planı oluşturma](/cli/azure/appservice/plan#create) CLI komutu.</span><span class="sxs-lookup"><span data-stu-id="53b41-136">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="53b41-137">Uygulama hizmeti planı, uygulamalarınızı barındırmak için kullanılan fiziksel kaynakları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="53b41-137">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="53b41-138">Bir uygulama hizmeti planı atanan tüm uygulamalar maliyet birden fazla uygulama barındırdığında kaydetmenize izin vererek, bu kaynakları paylaşır.</span><span class="sxs-lookup"><span data-stu-id="53b41-138">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span>
2. <span data-ttu-id="53b41-139">Bir Web Uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="53b41-139">Create a Web App.</span></span> <span data-ttu-id="53b41-140">Kullanabilir [Azure portal](/azure/app-service-web/web-sites-configure) veya aşağıdaki Az CLI komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="53b41-140">You can either use the [Azure portal](/azure/app-service-web/web-sites-configure) or use the following Az CLI command:</span></span>
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. <span data-ttu-id="53b41-141">Uygulamanızın gerektiğini Java Çalışma zamanı yapılandırma ayarladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="53b41-141">Make sure you set up the Java runtime configuration that your app needs.</span></span> <span data-ttu-id="53b41-142">Yeni bir Java 8 JDK üzerinde çalıştırmak için web uygulama aşağıdaki Azure CLI komutu yapılandırır ve [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="53b41-142">The following Azure CLI command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-the-jenkins-job"></a><span data-ttu-id="53b41-143">Jenkins iş ayarlayın</span><span class="sxs-lookup"><span data-stu-id="53b41-143">Set up the Jenkins job</span></span>


1. <span data-ttu-id="53b41-144">Yeni bir **freestyle** Jenkins Pano projesinde</span><span class="sxs-lookup"><span data-stu-id="53b41-144">Create a new **freestyle** project in Jenkins Dashboard</span></span>
2. <span data-ttu-id="53b41-145">Yapılandırma **kaynak kodu Yönetimi** , yerel çatalı, kullanılacak [basit Java Web uygulaması için Azure](https://github.com/azure-devops/javawebappsample) sağlayarak **depo URL'si**.</span><span class="sxs-lookup"><span data-stu-id="53b41-145">Configure **Source Code Management** to use your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing the **Repository URL**.</span></span> <span data-ttu-id="53b41-146">Örneğin: http://github.com/&lt;yourID > / javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="53b41-146">For example: http://github.com/&lt;yourID>/javawebappsample.</span></span>
3. <span data-ttu-id="53b41-147">Maven kullanarak Projeyi derlemek için derleme adımı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="53b41-147">Add a Build step to build the project using Maven.</span></span> <span data-ttu-id="53b41-148">Ekleyerek bunu bir **Kabuk yürütme**.</span><span class="sxs-lookup"><span data-stu-id="53b41-148">Do so by adding an **Execute shell**.</span></span> <span data-ttu-id="53b41-149">Bu örnekte, hedef klasör *.war dosyasında ROOT.war için yeniden adlandırmak için ek bir adım gerekir.</span><span class="sxs-lookup"><span data-stu-id="53b41-149">For this example, we need an additional step to rename the *.war file in target folder to ROOT.war.</span></span>   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. <span data-ttu-id="53b41-150">Bir oluşturma sonrası eylemi seçerek eklemek **Azure Web uygulaması yayımlama**.</span><span class="sxs-lookup"><span data-stu-id="53b41-150">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
5. <span data-ttu-id="53b41-151">, Önceki adımda depolanan Azure hizmet sorumlusu "bileşene" mySp sağlayın.</span><span class="sxs-lookup"><span data-stu-id="53b41-151">Supply, "mySp", the Azure service principal stored in previous step.</span></span>
6. <span data-ttu-id="53b41-152">İçinde **uygulama yapılandırması** bölümünde, aboneliğinizde kaynak grubu ve web uygulaması seçin.</span><span class="sxs-lookup"><span data-stu-id="53b41-152">In **App Configuration** section, choose the resource group and web app in your subscription.</span></span> <span data-ttu-id="53b41-153">Web uygulaması Windows olup olmadığını eklentisi otomatik olarak algılar ve Linux tabanlı.</span><span class="sxs-lookup"><span data-stu-id="53b41-153">The plugin automatically detects whether the Web App is Windows or Linux-based.</span></span> <span data-ttu-id="53b41-154">Windows tabanlı Web uygulaması'için bir seçenek "yayımlama dosyaları" sunulur.</span><span class="sxs-lookup"><span data-stu-id="53b41-154">For a Windows-based Web App, the option "Publish Files" is presented.</span></span>
7. <span data-ttu-id="53b41-155">(Örneğin, Java kullanılıyorsa bir war paketi.) dağıtmak istediğiniz dosyaları doldurun Kaynak dizin ve hedef dizin isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="53b41-155">Fill in the files you want to deploy (for example, a war package if you're using Java.) Source Directory and Target Directory are optional.</span></span> <span data-ttu-id="53b41-156">Parametreler kaynak ve hedef klasörler dosyaları karşıya yüklenirken belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="53b41-156">The parameters allow you to specify source and target folders when uploading files.</span></span> <span data-ttu-id="53b41-157">Azure'da Java web uygulaması Tomcat Server'da çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="53b41-157">Java web app on Azure is run in a Tomcat server.</span></span> <span data-ttu-id="53b41-158">Karşıya yüklediğiniz şekilde, paket webapps klasörüne war.</span><span class="sxs-lookup"><span data-stu-id="53b41-158">So you upload you war package to webapps folder.</span></span> <span data-ttu-id="53b41-159">Bu örnek için set **kaynak dizin** "hedef" ve "webapps" sağlamanız için **hedef dizin**.</span><span class="sxs-lookup"><span data-stu-id="53b41-159">For this example, set **Source Directory** to "target" and supply "webapps" for **Target Directory**.</span></span>
8. <span data-ttu-id="53b41-160">Bir yuva üretim dışında dağıtmak istiyorsanız, ayrıca ayarlayabilirsiniz **yuvası** adı.</span><span class="sxs-lookup"><span data-stu-id="53b41-160">If you want to deploy to a slot other than production, you can also set **Slot** Name.</span></span>
9. <span data-ttu-id="53b41-161">Projeyi kaydedin ve onu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="53b41-161">Save the project and build it.</span></span> <span data-ttu-id="53b41-162">Yapı tamamlandığında, web uygulamanızı Azure'a dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="53b41-162">Your web app is deployed to Azure when build is complete.</span></span>

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a><span data-ttu-id="53b41-163">Jenkins ardışık düzen kullanarak FTP üzerinden Web uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="53b41-163">Deploy Web App through FTP using Jenkins pipeline</span></span>

<span data-ttu-id="53b41-164">Eklenti ardışık düzeni için hazır olur.</span><span class="sxs-lookup"><span data-stu-id="53b41-164">The plugin is pipeline-ready.</span></span> <span data-ttu-id="53b41-165">GitHub depo örnekte başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53b41-165">You can refer to a sample in the GitHub repo.</span></span>

1. <span data-ttu-id="53b41-166">GitHub web kullanıcı Arabirimi, açık **Jenkinsfile_ftp_plugin** dosya.</span><span class="sxs-lookup"><span data-stu-id="53b41-166">In GitHub web UI, open **Jenkinsfile_ftp_plugin** file.</span></span> <span data-ttu-id="53b41-167">Web uygulamanızı 11 ve 12 satırındaki adını ve kaynak grubu sırasıyla güncelleştirmek için bu dosyayı düzenlemek için Kalem simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="53b41-167">Click the pencil icon to edit this file to update the resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="53b41-168">Satır kimlik bilgisi kimliği Jenkins Örneğinizde güncelleştirmek için 14 değiştirin.</span><span class="sxs-lookup"><span data-stu-id="53b41-168">Change line 14 to update credential ID in your Jenkins instance.</span></span>    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a><span data-ttu-id="53b41-169">Jenkins işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="53b41-169">Create a Jenkins pipeline</span></span>

1. <span data-ttu-id="53b41-170">Jenkins bir web tarayıcısında açın, **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="53b41-170">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="53b41-171">Seçin ve iş için bir ad **ardışık düzen**.</span><span class="sxs-lookup"><span data-stu-id="53b41-171">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="53b41-172">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="53b41-172">Click **OK**.</span></span>
3. <span data-ttu-id="53b41-173">Tıklatın **ardışık düzen** sekmesinde sonraki.</span><span class="sxs-lookup"><span data-stu-id="53b41-173">Click the **Pipeline** tab next.</span></span>
4. <span data-ttu-id="53b41-174">İçin **tanımı**seçin **kanal SCM betikten**.</span><span class="sxs-lookup"><span data-stu-id="53b41-174">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="53b41-175">İçin **SCM**seçin **Git**.</span><span class="sxs-lookup"><span data-stu-id="53b41-175">For **SCM**, select **Git**.</span></span> <span data-ttu-id="53b41-176">Forked, depodaki için GitHub URL'yi girin: https:&lt;forked depodaki > .git</span><span class="sxs-lookup"><span data-stu-id="53b41-176">Enter the GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span>
6. <span data-ttu-id="53b41-177">Güncelleştirme **komut dosyası yolu** "Jenkinsfile_ftp_plugin" için</span><span class="sxs-lookup"><span data-stu-id="53b41-177">Update **Script Path** to "Jenkinsfile_ftp_plugin"</span></span>
7. <span data-ttu-id="53b41-178">Tıklatın **kaydetmek** ve işini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="53b41-178">Click **Save** and run the job.</span></span>

## <a name="configure-jenkins-to-deploy-web-app-on-linux-through-docker"></a><span data-ttu-id="53b41-179">Web uygulaması Docker aracılığıyla Linux'ta dağıtma Jenkins yapılandırın</span><span class="sxs-lookup"><span data-stu-id="53b41-179">Configure Jenkins to deploy Web App on Linux through Docker</span></span>

<span data-ttu-id="53b41-180">Git/FTP dışında Linux üzerinde Web uygulaması Docker kullanarak dağıtımı destekler.</span><span class="sxs-lookup"><span data-stu-id="53b41-180">Apart from Git/FTP, Web App on Linux supports deployment using Docker.</span></span> <span data-ttu-id="53b41-181">Docker kullanarak dağıtmak için web uygulamanızı hizmet çalışma zamanı docker görüntüsüne paketleri bir Dockerfile sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="53b41-181">To deploy using Docker, you need to provide a Dockerfile that packages your web app with service runtime into a docker image.</span></span> <span data-ttu-id="53b41-182">Ardından eklentisi görüntü oluşturur, docker kayıt defterine iter ve web uygulamanıza görüntüyü dağıtır.</span><span class="sxs-lookup"><span data-stu-id="53b41-182">Then the plugin builds the image, pushes it to a docker registry and deploys the image to your web app.</span></span>

<span data-ttu-id="53b41-183">Web uygulaması Linux'ta geleneksel yolları Git ve FTP gibi ancak yalnızca yerleşik dilleri (.NET Core, Node.js, PHP ve Ruby) da destekler.</span><span class="sxs-lookup"><span data-stu-id="53b41-183">Web App on Linux also supports traditional ways like Git and FTP, but only for built-in languages (.NET Core, Node.js, PHP, and Ruby).</span></span> <span data-ttu-id="53b41-184">Diğer diller için uygulama kodu ve hizmet çalışma zamanı birlikte docker görüntüsüne paketini ve dağıtmak için docker kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="53b41-184">For other languages, you need to package your application code and service runtime together into a docker image and use docker to deploy.</span></span>

<span data-ttu-id="53b41-185">Jenkins işinde ayarlamadan önce bir Azure uygulama hizmeti Linux'ta gerekir.</span><span class="sxs-lookup"><span data-stu-id="53b41-185">Before setting up the job in Jenkins, you need an Azure app service on Linux.</span></span> <span data-ttu-id="53b41-186">Bir kapsayıcı kayıt defteri, depolamak ve özel Docker kapsayıcısı görüntülerinizi yönetmek için de gereklidir.</span><span class="sxs-lookup"><span data-stu-id="53b41-186">A container registry is also needed to store and manage your private Docker container images.</span></span> <span data-ttu-id="53b41-187">DockerHub kullanabilirsiniz; Bu örnek için Azure kapsayıcı kayıt defteri kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="53b41-187">You can use DockerHub; we are using Azure Container Registry for this example.</span></span>

* <span data-ttu-id="53b41-188">Adımları izleyebilirsiniz [burada](/azure/app-service-web/app-service-linux-how-to-create-web-app) Linux üzerinde bir Web uygulaması oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="53b41-188">You can follow the steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) to create a Web App on Linux</span></span> 
* <span data-ttu-id="53b41-189">Azure kapsayıcı kayıt defteri olan bir yönetilen [Docker kayıt defteri] (https://docs.docker.com/registry/) hizmet tabanlı açık kaynak Docker kayıt defteri 2.0.</span><span class="sxs-lookup"><span data-stu-id="53b41-189">Azure Container Registry is a managed [Docker registry] (https://docs.docker.com/registry/) service based on the open-source Docker Registry 2.0.</span></span> <span data-ttu-id="53b41-190">[Burada] adımları (/ azure/container-registry/container-registry-get-started-azure-cli) bunun nasıl yapılacağı hakkında daha fazla yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="53b41-190">Follow the steps [here] (/azure/container-registry/container-registry-get-started-azure-cli) for more guidance on how to do so.</span></span> <span data-ttu-id="53b41-191">DockerHub de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53b41-191">You can also use DockerHub.</span></span>

### <a name="to-deploy-using-docker"></a><span data-ttu-id="53b41-192">Docker kullanarak dağıtmak için:</span><span class="sxs-lookup"><span data-stu-id="53b41-192">To deploy using docker:</span></span>

1. <span data-ttu-id="53b41-193">Yeni bir Serbest stilde projesi Jenkins panosunda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="53b41-193">Create a new freestyle project in Jenkins Dashboard.</span></span>
2. <span data-ttu-id="53b41-194">Yapılandırma **kaynak kodu Yönetimi** , yerel çatalı, kullanılacak [basit Java Web uygulaması için Azure](https://github.com/azure-devops/javawebappsample) sağlayarak **depo URL'si**.</span><span class="sxs-lookup"><span data-stu-id="53b41-194">Configure **Source Code Management** to use your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing the **Repository URL**.</span></span> <span data-ttu-id="53b41-195">Örneğin: http://github.com/&lt;yourid > / javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="53b41-195">For example: http://github.com/&lt;yourid>/javawebappsample.</span></span>
<span data-ttu-id="53b41-196">Maven kullanarak Projeyi derlemek için derleme adımı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="53b41-196">Add a Build step to build the project using Maven.</span></span> <span data-ttu-id="53b41-197">Ekleyerek bunu bir **Kabuk yürütme** ve aşağıdaki satırı ekleyin **komutu**:</span><span class="sxs-lookup"><span data-stu-id="53b41-197">Do so by adding an **Execute shell** and add the following line in **Command**:</span></span>    
```bash
mvn clean package
```

3. <span data-ttu-id="53b41-198">Bir oluşturma sonrası eylemi seçerek eklemek **Azure Web uygulaması yayımlama**.</span><span class="sxs-lookup"><span data-stu-id="53b41-198">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
4. <span data-ttu-id="53b41-199">Tedarik, **bileşene mySp**, önceki adımda Azure kimlik bilgileri olarak depolanan Azure hizmet sorumlusu.</span><span class="sxs-lookup"><span data-stu-id="53b41-199">Supply, **mySp**, the Azure service principal stored in previous step as Azure Credentials.</span></span>
5. <span data-ttu-id="53b41-200">İçinde **uygulama yapılandırması** bölümünde, aboneliğinizde kaynak grubu ve Linux web uygulaması seçin.</span><span class="sxs-lookup"><span data-stu-id="53b41-200">In **App Configuration** section, choose the resource group and a Linux web app in your subscription.</span></span>
6. <span data-ttu-id="53b41-201">Seçin Docker yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="53b41-201">Choose Publish via Docker.</span></span>
7. <span data-ttu-id="53b41-202">Doldurmak **Dockerfile** yolu.</span><span class="sxs-lookup"><span data-stu-id="53b41-202">Fill in **Dockerfile** path.</span></span> <span data-ttu-id="53b41-203">Varsayılan koruyabilirsiniz "/ Dockerfile" için **Docker kayıt defteri URL**, https:// biçiminde sağlar&lt;myRegistry >. Azure kapsayıcı kayıt defteri kullanırsanız azurecr.io.</span><span class="sxs-lookup"><span data-stu-id="53b41-203">You can keep the default "/Dockerfile" For **Docker registry URL**, supply in the format of https://&lt;myRegistry>.azurecr.io if you use Azure Container Registry.</span></span> <span data-ttu-id="53b41-204">DockerHub kullanıyorsanız, boş bırakın.</span><span class="sxs-lookup"><span data-stu-id="53b41-204">Leave it blank if you use DockerHub.</span></span>
8. <span data-ttu-id="53b41-205">İçin **kayıt defteri kimlik bilgilerini**, Azure kapsayıcı kayıt için kimlik bilgisi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="53b41-205">For **Registry credentials**, add the credential for the Azure Container Registry.</span></span> <span data-ttu-id="53b41-206">Azure CLI aşağıdaki komutları çalıştırarak kullanıcı kimliği ve parola alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53b41-206">You can get the userid and password by running the following commands in Azure CLI.</span></span> <span data-ttu-id="53b41-207">İlk komut yönetici hesabını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="53b41-207">The first command enables the administrator account.</span></span>    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. <span data-ttu-id="53b41-208">Docker görüntü adı ve etiketinde **Gelişmiş** sekmesi isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="53b41-208">The docker image name and tag in **Advanced** tab are optional.</span></span> <span data-ttu-id="53b41-209">Varsayılan olarak, Azure portalında (Docker kapsayıcısı ayarı.) için yapılandırdığınız görüntü adından görüntü adı elde edilir Etiket $BUILD_NUMBER oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="53b41-209">By default, image name is obtained from the image name you configured in Azure portal (in Docker Container setting.) The tag is generated from $BUILD_NUMBER.</span></span> <span data-ttu-id="53b41-210">Emin olun ya da Azure Portalı'nda Görüntü adı belirtin veya için bir değer sağlamanız **Docker görüntü** içinde **Gelişmiş** sekmesi. Bu örnekte, tedarik "&lt;yourRegistry >.azurecr.io/calculator" için **Docker görüntü** bırakıp **Docker resim etiketi** boş.</span><span class="sxs-lookup"><span data-stu-id="53b41-210">Make sure you specify the image name in either Azure portal or supply a value for **Docker Image** in **Advanced** tab. For this example, supply "&lt;yourRegistry>.azurecr.io/calculator" for **Docker image** and leave **Docker Image Tag** blank.</span></span>
10. <span data-ttu-id="53b41-211">Yerleşik Docker görüntü ayarını kullanırsanız Not dağıtımı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="53b41-211">Note deployment fails if you use built-in Docker image setting.</span></span> <span data-ttu-id="53b41-212">Azure portalında Docker kapsayıcısı ayarında özel görüntü kullanmak için docker config değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="53b41-212">Make sure you change docker config to use custom image in Docker Container setting in Azure portal.</span></span> <span data-ttu-id="53b41-213">Yerleşik görüntü için dosya karşıya yükleme yaklaşımı dağıtmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="53b41-213">For built-in image, use file upload approach to deploy.</span></span>
11. <span data-ttu-id="53b41-214">Benzer şekilde dosya karşıya yükleme yaklaşım, üretim dışındaki başka bir yuvaya seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53b41-214">Similar to file upload approach, you can choose a different slot other than production.</span></span>
12. <span data-ttu-id="53b41-215">Kaydedin ve projeyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="53b41-215">Save and build the project.</span></span> <span data-ttu-id="53b41-216">Kapsayıcı görüntünüzü kayıt defterine gönderilir ve web uygulama bakın.</span><span class="sxs-lookup"><span data-stu-id="53b41-216">You see your container image is pushed to your registry and web app is deployed.</span></span>

### <a name="deploy-to-web-app-on-linux-through-docker-using-jenkins-pipeline"></a><span data-ttu-id="53b41-217">Docker kullanılarak Jenkins ardışık düzeni aracılığıyla Linux'ta Web uygulamasına dağıtma</span><span class="sxs-lookup"><span data-stu-id="53b41-217">Deploy to Web App on Linux through Docker using Jenkins pipeline</span></span>

1. <span data-ttu-id="53b41-218">GitHub web kullanıcı Arabirimi, açık **Jenkinsfile_container_plugin** dosya.</span><span class="sxs-lookup"><span data-stu-id="53b41-218">In GitHub web UI, open **Jenkinsfile_container_plugin** file.</span></span> <span data-ttu-id="53b41-219">Web uygulamanızı 11 ve 12 satırındaki adını ve kaynak grubu sırasıyla güncelleştirmek için bu dosyayı düzenlemek için Kalem simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="53b41-219">Click the pencil icon to edit this file to update the resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="53b41-220">Kapsayıcı kayıt defteri sunucunuza satır 13 değiştirme</span><span class="sxs-lookup"><span data-stu-id="53b41-220">Change line 13 to your container registry server</span></span>    
```java
def registryServer = '<registryURL>'
```    

3. <span data-ttu-id="53b41-221">Satır kimlik bilgisi kimliği Jenkins Örneğinizde güncelleştirmek için 16 değiştirme</span><span class="sxs-lookup"><span data-stu-id="53b41-221">Change line 16 to update credential ID in your Jenkins instance</span></span>    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a><span data-ttu-id="53b41-222">Jenkins işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="53b41-222">Create Jenkins pipeline</span></span>    

1. <span data-ttu-id="53b41-223">Jenkins bir web tarayıcısında açın, **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="53b41-223">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="53b41-224">Seçin ve iş için bir ad **ardışık düzen**.</span><span class="sxs-lookup"><span data-stu-id="53b41-224">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="53b41-225">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="53b41-225">Click **OK**.</span></span>
3. <span data-ttu-id="53b41-226">Tıklatın **ardışık düzen** sekmesinde sonraki.</span><span class="sxs-lookup"><span data-stu-id="53b41-226">Click the **Pipeline** tab next.</span></span>
4. <span data-ttu-id="53b41-227">İçin **tanımı**seçin **kanal SCM betikten**.</span><span class="sxs-lookup"><span data-stu-id="53b41-227">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="53b41-228">İçin **SCM**seçin **Git**.</span><span class="sxs-lookup"><span data-stu-id="53b41-228">For **SCM**, select **Git**.</span></span>
6. <span data-ttu-id="53b41-229">Forked, depodaki için GitHub URL'yi girin: https:&lt;forked depodaki > .git</span><span class="sxs-lookup"><span data-stu-id="53b41-229">Enter the GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span></li>
<span data-ttu-id="53b41-230">7, güncelleştirme **komut dosyası yolu** "Jenkinsfile_container_plugin" için</span><span class="sxs-lookup"><span data-stu-id="53b41-230">7, Update **Script Path** to "Jenkinsfile_container_plugin"</span></span>
8. <span data-ttu-id="53b41-231">Tıklatın **kaydetmek** ve işini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="53b41-231">Click **Save** and run the job.</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="53b41-232">Web uygulamanızı doğrulayın</span><span class="sxs-lookup"><span data-stu-id="53b41-232">Verify your web app</span></span>

1. <span data-ttu-id="53b41-233">WAR doğrulamak için dosyası, web uygulamanızın başarıyla dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="53b41-233">To verify the WAR file is deployed successfully to your web app.</span></span> <span data-ttu-id="53b41-234">Bir web tarayıcısı açın.</span><span class="sxs-lookup"><span data-stu-id="53b41-234">Open a web browser.</span></span>
2. <span data-ttu-id="53b41-235">Http:// gidin&lt;app_name >.azurewebsites.net/api/calculator/ping görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="53b41-235">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping You see:</span></span>    
     <span data-ttu-id="53b41-236">Java Web uygulaması'na Hoş!!!</span><span class="sxs-lookup"><span data-stu-id="53b41-236">Welcome to Java Web App!!!</span></span> <span data-ttu-id="53b41-237">Bu güncelleştirilmiş!</span><span class="sxs-lookup"><span data-stu-id="53b41-237">This is updated!</span></span>
   <span data-ttu-id="53b41-238">Sun Haz 17 16:39:10 UTC 2017</span><span class="sxs-lookup"><span data-stu-id="53b41-238">Sun Jun 17 16:39:10 UTC 2017</span></span>
3. <span data-ttu-id="53b41-239">Http:// gidin&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (alternatif &lt;x > ve &lt;y > sayılar içeren) x toplamını almak için ve y</span><span class="sxs-lookup"><span data-stu-id="53b41-239">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>        
    ![Hesaplayıcı: Ekle](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a><span data-ttu-id="53b41-241">Linux için uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="53b41-241">For App service on Linux</span></span>

* <span data-ttu-id="53b41-242">, Azure CLI'da doğrulamak için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="53b41-242">To verify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="53b41-243">Aşağıdaki sonucu alın:</span><span class="sxs-lookup"><span data-stu-id="53b41-243">You get the following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="53b41-244">Http:// gidin&lt;app_name >.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="53b41-244">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="53b41-245">İletiyi görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="53b41-245">You see the message:</span></span> 
    
        Welcome to Java Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="53b41-246">Http:// gidin&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (alternatif &lt;x > ve &lt;y > sayılar içeren) x toplamını almak için ve y</span><span class="sxs-lookup"><span data-stu-id="53b41-246">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="53b41-247">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="53b41-247">Next steps</span></span>

<span data-ttu-id="53b41-248">Bu öğreticide, Azure App Service eklentisi Azure'a dağıtmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="53b41-248">In this tutorial, you use the Azure App Service plugin to deploy to Azure.</span></span>

<span data-ttu-id="53b41-249">Size nasıl öğrenilen için:</span><span class="sxs-lookup"><span data-stu-id="53b41-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="53b41-250">FTP aracılığıyla Azure uygulama hizmeti dağıtmak için Jenkins yapılandırın</span><span class="sxs-lookup"><span data-stu-id="53b41-250">Configure Jenkins to deploy Azure App Service through FTP</span></span> 
> * <span data-ttu-id="53b41-251">Azure uygulama hizmeti Docker aracılığıyla Linux'ta dağıtmak için Jenkins yapılandırın</span><span class="sxs-lookup"><span data-stu-id="53b41-251">Configure Jenkins to deploy to Azure App Service on Linux through Docker</span></span> 