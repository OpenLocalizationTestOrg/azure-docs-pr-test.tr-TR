---
title: aaaExecute hello Jenkins ile Azure CLI | Microsoft Docs
description: "Nasıl toouse Azure CLI toodeploy bir Java web uygulaması tooAzure Jenkins ardışık düzeninde öğrenin"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: jenkins
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 4bd1e12e6de1f010453ff51c835f84e7361962f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a><span data-ttu-id="dcf8d-103">TooAzure Jenkins ile uygulama hizmeti dağıtma ve Azure CLI hello</span><span class="sxs-lookup"><span data-stu-id="dcf8d-103">Deploy tooAzure App Service with Jenkins and hello Azure CLI</span></span>
<span data-ttu-id="dcf8d-104">toodeploy bir Java web uygulaması tooAzure, Azure CLI kullanabileceğiniz [Jenkins ardışık düzen](https://jenkins.io/doc/book/pipeline/).</span><span class="sxs-lookup"><span data-stu-id="dcf8d-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span></span> <span data-ttu-id="dcf8d-105">Bu öğreticide, Azure VM temelinde CI/CD işlem hattı oluşturmak için nasıl dahil:</span><span class="sxs-lookup"><span data-stu-id="dcf8d-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dcf8d-106">Jenkins VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="dcf8d-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="dcf8d-107">Jenkins yapılandırın</span><span class="sxs-lookup"><span data-stu-id="dcf8d-107">Configure Jenkins</span></span>
> * <span data-ttu-id="dcf8d-108">Bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="dcf8d-108">Create a web app in Azure</span></span>
> * <span data-ttu-id="dcf8d-109">GitHub depo hazırlama</span><span class="sxs-lookup"><span data-stu-id="dcf8d-109">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="dcf8d-110">Jenkins işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dcf8d-110">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="dcf8d-111">Merhaba ardışık düzen çalıştırın ve başlangıç web uygulaması doğrulayın</span><span class="sxs-lookup"><span data-stu-id="dcf8d-111">Run hello pipeline and verify hello web app</span></span>

<span data-ttu-id="dcf8d-112">Bu öğretici hello Azure CLI Sürüm 2.0.4 gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-112">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="dcf8d-113">çalıştırma toofind hello sürüm `az --version`.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-113">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="dcf8d-114">Tooupgrade gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dcf8d-114">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="dcf8d-115">Oluşturma ve yapılandırma Jenkins örneği</span><span class="sxs-lookup"><span data-stu-id="dcf8d-115">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="dcf8d-116">Jenkins asıl zaten yoksa, hello ile başlangıç [çözüm şablonu](install-jenkins-solution-template.md), gerekli hello içerir [Azure kimlik bilgilerini](https://plugins.jenkins.io/azure-credentials) varsayılan eklentisi.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-116">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes hello required [Azure Credentials](https://plugins.jenkins.io/azure-credentials) plugin by default.</span></span> 

<span data-ttu-id="dcf8d-117">Hello Azure kimlik bilgisi eklentisi içinde Jenkins toostore Microsoft Azure hizmet asıl kimlik bilgileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-117">hello Azure Credential plugin allows you toostore Microsoft Azure service principal credentials in Jenkins.</span></span> <span data-ttu-id="dcf8d-118">Bu Jenkins ardışık düzen hello Azure kimlik alabilmek için sürüm 1.2 biz hello desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-118">In version 1.2, we added hello support so that Jenkins Pipeline can get hello Azure credentials.</span></span> 

<span data-ttu-id="dcf8d-119">1.2 veya sonraki bir sürümü olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="dcf8d-119">Ensure you have version 1.2 or later:</span></span>
* <span data-ttu-id="dcf8d-120">Merhaba Jenkins Pano içinde tıklatın **Jenkins Yönet -> eklentisi Yöneticisi ->** arayın ve **Azure kimlik bilgisi**.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-120">Within hello Jenkins dashboard, click **Manage Jenkins -> Plugin Manager ->** and search for **Azure Credential**.</span></span> 
* <span data-ttu-id="dcf8d-121">Merhaba sürüm 1.2 eskiyse hello eklentisi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-121">Update hello plugin if hello version is earlier than 1.2.</span></span>

<span data-ttu-id="dcf8d-122">Ayrıca Java JDK ve Maven hello Jenkins yöneticisinde gereklidir.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-122">Java JDK and Maven are also required in hello Jenkins master.</span></span> <span data-ttu-id="dcf8d-123">tooinstall, SSH kullanarak tooJenkins yöneticisinde oturum ve hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="dcf8d-123">tooinstall, log in tooJenkins master using SSH and run hello following commands:</span></span>
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="dcf8d-124">Azure hizmet asıl tooJenkins kimlik bilgisi Ekle</span><span class="sxs-lookup"><span data-stu-id="dcf8d-124">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="dcf8d-125">Azure kimlik bilgisi gerekli tooexecute Azure CLI ' dir.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-125">An Azure credential is needed tooexecute Azure CLI.</span></span>

* <span data-ttu-id="dcf8d-126">Merhaba Jenkins Pano içinde tıklatın **kimlik bilgileri -> Sistem ->**.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-126">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="dcf8d-127">Tıklatın **genel credentials(unrestricted)**.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-127">Click **Global credentials(unrestricted)**.</span></span>
* <span data-ttu-id="dcf8d-128">Tıklatın **kimlik bilgilerini eklemek** tooadd bir [Microsoft Azure hizmet sorumlusu](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) hello abonelik kimliği, istemci kimliği, gizli ve OAuth 2.0 belirteç uç noktası doldurarak.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-128">Click **Add Credentials** tooadd a [Microsoft Azure service principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="dcf8d-129">Sonraki adımda kullanmak için bir kimlik belirtin.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-129">Provide an ID for use in subsequent step.</span></span>

![Kimlik bilgileri Ekle](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a><span data-ttu-id="dcf8d-131">Merhaba Java web uygulaması dağıtmak için bir Azure uygulama hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="dcf8d-131">Create an Azure App Service for deploying hello Java web app</span></span>

<span data-ttu-id="dcf8d-132">Merhaba ile bir Azure uygulama hizmeti planı oluştur **serbest** fiyatlandırma katmanı hello kullanarak [az uygulama hizmeti planı oluşturma](/cli/azure/appservice/plan#create) CLI komutu.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-132">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="dcf8d-133">Merhaba uygulama hizmeti planı hello kullanılan fiziksel kaynakları toohost uygulamalarınızı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-133">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="dcf8d-134">Tooan uygulama hizmeti planı atanan tüm uygulamaların birden fazla uygulama barındırdığında toosave maliyet izin vererek, bu kaynakları paylaşır.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-134">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="dcf8d-135">Hello planı hazır olduğunda, Azure CLI benzer gösterir hello aşağıdaki örneğine toohello çıktı:</span><span class="sxs-lookup"><span data-stu-id="dcf8d-135">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a><span data-ttu-id="dcf8d-136">Bir Azure Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="dcf8d-136">Create an Azure Web app</span></span>

 <span data-ttu-id="dcf8d-137">Kullanım hello [az webapp oluşturma](/cli/azure/appservice/web#create) CLI komutu toocreate bir web uygulaması tanımı'nda hello `myAppServicePlan` uygulama hizmeti planı.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-137">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="dcf8d-138">Merhaba web uygulaması tanımı URL tooaccess uygulamanızla sağlar ve çeşitli seçenekler toodeploy kod tooAzure yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-138">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="dcf8d-139">Yedek hello `<app_name>` kendi benzersiz uygulama adıyla yer tutucu.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-139">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="dcf8d-140">Merhaba adının toobe benzersiz azure'da tüm uygulamalarında gerekir böylece bu benzersiz bir ad hello varsayılan etki alanı adı hello web uygulaması için bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-140">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="dcf8d-141">Tooyour kullanıcılar kullanıma önce bir özel etki alanı adı girişi toohello web uygulaması eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-141">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="dcf8d-142">Merhaba web uygulaması tanımı hazır olduğunda, aşağıdaki örneğine bilgi benzer toohello hello Azure CLI gösterir:</span><span class="sxs-lookup"><span data-stu-id="dcf8d-142">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a><span data-ttu-id="dcf8d-143">Java yapılandırın</span><span class="sxs-lookup"><span data-stu-id="dcf8d-143">Configure Java</span></span> 

<span data-ttu-id="dcf8d-144">Uygulamanızın ile Merhaba gerektiğini hello Java Çalışma zamanı yapılandırma ayarlama [az appservice web yapılandırma güncelleştirmesi](/cli/azure/appservice/web/config#update) komutu.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-144">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="dcf8d-145">Merhaba aşağıdaki komutu hello web uygulama toorun üzerinde yeni bir Java 8 JDK yapılandırır ve [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-145">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a><span data-ttu-id="dcf8d-146">GitHub depo hazırlama</span><span class="sxs-lookup"><span data-stu-id="dcf8d-146">Prepare a GitHub Repository</span></span>
<span data-ttu-id="dcf8d-147">Açık hello [basit Java Web uygulaması için Azure](https://github.com/azure-devops/javawebappsample) deposu.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-147">Open hello [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo.</span></span> <span data-ttu-id="dcf8d-148">toofork hello depodaki tooyour GitHub hesabı sahibi, hello tıklatın **çatalı** hello üst sağ köşesindeki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-148">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

* <span data-ttu-id="dcf8d-149">GitHub web kullanıcı Arabirimi, açık **Jenkinsfile** dosya.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-149">In GitHub web UI, open **Jenkinsfile** file.</span></span> <span data-ttu-id="dcf8d-150">Hello Kurşun Kalem simgesini tooedit, bu dosya tooupdate hello kaynak grubu ve adı, web uygulamanızın 20 ve 21 satırındaki'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-150">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 20 and 21 respectively.</span></span>

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* <span data-ttu-id="dcf8d-151">Satırı 23 tooupdate kimlik bilgisi kimliği Jenkins Örneğinizde değiştirme</span><span class="sxs-lookup"><span data-stu-id="dcf8d-151">Change line 23 tooupdate credential ID in your Jenkins instance</span></span>

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a><span data-ttu-id="dcf8d-152">Jenkins işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dcf8d-152">Create Jenkins pipeline</span></span>
<span data-ttu-id="dcf8d-153">Jenkins bir web tarayıcısında açın, **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-153">Open Jenkins in a web browser, click **New Item**.</span></span> 

* <span data-ttu-id="dcf8d-154">Merhaba işi için bir ad sağlayın ve seçin **ardışık düzen**.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-154">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="dcf8d-155">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-155">Click **OK**.</span></span>
* <span data-ttu-id="dcf8d-156">Merhaba tıklatın **ardışık düzen** sekmesinde sonraki.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-156">Click hello **Pipeline** tab next.</span></span> 
* <span data-ttu-id="dcf8d-157">İçin **tanımı**seçin **kanal SCM betikten**.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-157">For **Definition**, select **Pipeline script from SCM**.</span></span>
* <span data-ttu-id="dcf8d-158">İçin **SCM**seçin **Git**.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-158">For **SCM**, select **Git**.</span></span>
* <span data-ttu-id="dcf8d-159">Merhaba GitHub URL forked depodaki girin: https:\<forked repo\>.git</span><span class="sxs-lookup"><span data-stu-id="dcf8d-159">Enter hello GitHub URL for your forked repo: https:\<your forked repo\>.git</span></span>
* <span data-ttu-id="dcf8d-160">Tıklatın **Kaydet**</span><span class="sxs-lookup"><span data-stu-id="dcf8d-160">Click **Save**</span></span>

## <a name="test-your-pipeline"></a><span data-ttu-id="dcf8d-161">İşlem hattınızı test</span><span class="sxs-lookup"><span data-stu-id="dcf8d-161">Test your pipeline</span></span>
* <span data-ttu-id="dcf8d-162">Oluşturduğunuz toohello ardışık gidin, tıklatın **şimdi derleme**</span><span class="sxs-lookup"><span data-stu-id="dcf8d-162">Go toohello pipeline you created, click **Build Now**</span></span>
* <span data-ttu-id="dcf8d-163">Birkaç saniye içinde bir yapı başarılı olması gerekir ve Git toohello yapı ve tıklatın **konsol çıktısı** toosee hello ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="dcf8d-163">A build should succeed in a few seconds, and you can go toohello build and click **Console Output** toosee hello details</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="dcf8d-164">Web uygulamanızı doğrulayın</span><span class="sxs-lookup"><span data-stu-id="dcf8d-164">Verify your web app</span></span>
<span data-ttu-id="dcf8d-165">tooverify hello WAR dosyası başarıyla dağıtılan tooyour web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-165">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="dcf8d-166">Bir web tarayıcısı açın:</span><span class="sxs-lookup"><span data-stu-id="dcf8d-166">Open a web browser:</span></span>

* <span data-ttu-id="dcf8d-167">Toohttp gidin: / /&lt;app_name >.azurewebsites.net/api/calculator/ping</span><span class="sxs-lookup"><span data-stu-id="dcf8d-167">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping</span></span>  
<span data-ttu-id="dcf8d-168">Görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="dcf8d-168">You see:</span></span>

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* <span data-ttu-id="dcf8d-169">Toohttp gidin: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (değiştirin &lt;x > ve &lt;y > sayılar içeren) tooget hello toplamını x ve y</span><span class="sxs-lookup"><span data-stu-id="dcf8d-169">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>

![Hesaplayıcı: Ekle](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a><span data-ttu-id="dcf8d-171">TooAzure Linux üzerinde Web uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="dcf8d-171">Deploy tooAzure Web App on Linux</span></span>
<span data-ttu-id="dcf8d-172">Nasıl toouse, Jenkins Azure CLI kanal bildiğinize göre hello betik toodeploy tooan Azure Web uygulaması Linux'ta değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-172">Now that you know how toouse Azure CLI in your Jenkins pipeline, you can modify hello script toodeploy tooan Azure Web App on Linux.</span></span>

<span data-ttu-id="dcf8d-173">Web uygulaması Linux'ta toouse Docker olan bir farklı bir şekilde toodo hello dağıtımını destekler.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-173">Web App on Linux supports a different way toodo hello deployment, which is toouse Docker.</span></span> <span data-ttu-id="dcf8d-174">toodeploy, tooprovide Docker görüntüsüne web uygulamanızı hizmet çalışma zamanı paketleri bir Dockerfile gerekir.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-174">toodeploy, you need tooprovide a Dockerfile that packages your web app with service runtime into a Docker image.</span></span> <span data-ttu-id="dcf8d-175">Merhaba eklentisi hello görüntüsünü oluşturabilirsiniz, tooa Docker kayıt defteri anında sonra hello görüntü tooyour web uygulaması dağıtma.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-175">hello plugin will then build hello image, push it tooa Docker registry and deploy hello image tooyour web app.</span></span>

* <span data-ttu-id="dcf8d-176">Merhaba adımları [burada](/azure/app-service-web/app-service-linux-how-to-create-web-app) Azure Web uygulaması Linux üzerinde çalışan bir toocreate.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-176">Follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate an Azure Web App running on Linux.</span></span>
* <span data-ttu-id="dcf8d-177">Bu hello yönergeleri izleyerek Jenkins örneğinde Docker yükleme [makale](https://docs.docker.com/engine/installation/linux/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="dcf8d-177">Install Docker on your Jenkins instance by following hello instructions in this [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span></span>
* <span data-ttu-id="dcf8d-178">Merhaba adımları kullanarak bir kapsayıcı kayıt defteri hello Azure portal oluşturma [burada](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dcf8d-178">Create a Container Registry in hello Azure portal by using hello steps [here](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
* <span data-ttu-id="dcf8d-179">İçinde aynı hello [basit Java Web uygulaması için Azure](https://github.com/azure-devops/javawebappsample) , çatallanmış, depodaki Düzenle hello **Jenkinsfile2** dosyası:</span><span class="sxs-lookup"><span data-stu-id="dcf8d-179">In hello same [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo you forked, edit hello **Jenkinsfile2** file:</span></span>
    * <span data-ttu-id="dcf8d-180">18-21 satır, kaynak grubu, web uygulaması ve ACR toohello adlarını sırasıyla güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-180">Line 18-21, update toohello names of your resource group, web app, and ACR respectively.</span></span> 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * <span data-ttu-id="dcf8d-181">Satır 24, güncelleştirme \<azsrvprincipal\> tooyour kimlik bilgisi kimliği</span><span class="sxs-lookup"><span data-stu-id="dcf8d-181">Line 24, update \<azsrvprincipal\> tooyour credential ID</span></span>
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* <span data-ttu-id="dcf8d-182">Windows, yalnızca bu kez, kullanım tooAzure web uygulamasında dağıtırken yaptığınız gibi yeni Jenkins işlem hattı oluşturma **Jenkinsfile2** yerine.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-182">Create a new Jenkins pipeline as you did when deploying tooAzure web app in Windows, only this time, use **Jenkinsfile2** instead.</span></span>
* <span data-ttu-id="dcf8d-183">Yeni işinizi çalıştırmak.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-183">Run your new job.</span></span>
* <span data-ttu-id="dcf8d-184">tooverify, Azure CLI'da çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="dcf8d-184">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="dcf8d-185">Sonuç aşağıdaki hello alın:</span><span class="sxs-lookup"><span data-stu-id="dcf8d-185">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="dcf8d-186">Toohttp gidin: / /&lt;app_name >.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-186">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="dcf8d-187">Selamlama iletisine bakın:</span><span class="sxs-lookup"><span data-stu-id="dcf8d-187">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="dcf8d-188">Toohttp gidin: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (değiştirin &lt;x > ve &lt;y > sayılar içeren) tooget hello toplamını x ve y</span><span class="sxs-lookup"><span data-stu-id="dcf8d-188">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="dcf8d-189">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dcf8d-189">Next steps</span></span>
<span data-ttu-id="dcf8d-190">Bu öğreticide, GitHub deposuna hello kaynak kodunda kullanıma Jenkins ardışık yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-190">In this tutorial, you configured a Jenkins pipeline that checks out hello source code in GitHub repo.</span></span> <span data-ttu-id="dcf8d-191">Maven toobuild war dosyasını çalıştırır ve Azure CLI toodeploy tooAzure uygulama hizmeti kullanır.</span><span class="sxs-lookup"><span data-stu-id="dcf8d-191">Runs Maven toobuild a war file and then uses Azure CLI toodeploy tooAzure App Service.</span></span> <span data-ttu-id="dcf8d-192">Şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="dcf8d-192">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dcf8d-193">Jenkins VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="dcf8d-193">Create a Jenkins VM</span></span>
> * <span data-ttu-id="dcf8d-194">Jenkins yapılandırın</span><span class="sxs-lookup"><span data-stu-id="dcf8d-194">Configure Jenkins</span></span>
> * <span data-ttu-id="dcf8d-195">Bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="dcf8d-195">Create a web app in Azure</span></span>
> * <span data-ttu-id="dcf8d-196">GitHub depo hazırlama</span><span class="sxs-lookup"><span data-stu-id="dcf8d-196">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="dcf8d-197">Jenkins işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dcf8d-197">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="dcf8d-198">Merhaba ardışık düzen çalıştırın ve başlangıç web uygulaması doğrulayın</span><span class="sxs-lookup"><span data-stu-id="dcf8d-198">Run hello pipeline and verify hello web app</span></span>
