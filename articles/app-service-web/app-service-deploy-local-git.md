---
title: "aaaLocal Git dağıtımı tooAzure uygulama hizmeti"
description: "Bilgi nasıl tooenable yerel Git dağıtım tooAzure uygulama hizmeti."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 1905e0b7acd58d8dd6496a14f6e4f38f9f8c0212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="local-git-deployment-tooazure-app-service"></a><span data-ttu-id="282a0-103">Yerel Git dağıtımı tooAzure uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="282a0-103">Local Git Deployment tooAzure App Service</span></span>
<span data-ttu-id="282a0-104">Bu öğretici şunların nasıl yapıldığını gösterir toodeploy uygulamanızı çok[Azure App Service] yerel bilgisayarınızdaki bir Git deposundan.</span><span class="sxs-lookup"><span data-stu-id="282a0-104">This tutorial shows you how toodeploy your app too[Azure App Service] from a Git repository on your local computer.</span></span> <span data-ttu-id="282a0-105">Uygulama hizmetini destekleyen hello bu yaklaşımı **yerel Git** hello dağıtım seçeneği [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="282a0-105">App Service supports this approach with hello **Local Git** deployment option in hello [Azure Portal].</span></span>  
<span data-ttu-id="282a0-106">Bu makalede açıklanan hello Git komutların çoğu hello kullanarak bir uygulama hizmeti uygulaması oluştururken, otomatik olarak gerçekleştirilir [Azure komut satırı arabirimi] açıklandığı gibi [burada](app-service-web-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="282a0-106">Many of hello Git commands described in this article are performed automatically when creating an App Service app using hello [Azure Command-Line Interface] as described [here](app-service-web-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="282a0-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="282a0-107">Prerequisites</span></span>
<span data-ttu-id="282a0-108">toocomplete Bu öğretici, gerekir:</span><span class="sxs-lookup"><span data-stu-id="282a0-108">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="282a0-109">Git.</span><span class="sxs-lookup"><span data-stu-id="282a0-109">Git.</span></span> <span data-ttu-id="282a0-110">Merhaba yükleme ikili indirebilirsiniz [burada](http://www.git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="282a0-110">You can download hello installation binary [here](http://www.git-scm.com/downloads).</span></span>  
* <span data-ttu-id="282a0-111">Git temel bilgiye.</span><span class="sxs-lookup"><span data-stu-id="282a0-111">Basic knowledge of Git.</span></span>
* <span data-ttu-id="282a0-112">Bir Microsoft Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="282a0-112">A Microsoft Azure account.</span></span> <span data-ttu-id="282a0-113">Bir hesabınız yoksa, [ücretsiz deneme için kaydolabilir](https://azure.microsoft.com/pricing/free-trial) veya [Visual Studio abone avantajlarınızı etkinleştirebilirsiniz.](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)</span><span class="sxs-lookup"><span data-stu-id="282a0-113">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span></span>

> [!NOTE]
> <span data-ttu-id="282a0-114">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="282a0-114">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service.</span></span> <span data-ttu-id="282a0-115">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="282a0-115">No credit cards required; no commitments.</span></span>  
> 
> 

## <span data-ttu-id="282a0-116"><a name="Step1"></a>1. adım: yerel bir havuz oluşturma</span><span class="sxs-lookup"><span data-stu-id="282a0-116"><a name="Step1"></a>Step 1: Create a local repository</span></span>
<span data-ttu-id="282a0-117">Aşağıdaki görevler toocreate yeni bir Git deposu hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="282a0-117">Perform hello following tasks toocreate a new Git repository.</span></span>

1. <span data-ttu-id="282a0-118">Bir komut satırı aracı gibi başlatın **Gitbash'i** (Windows) veya **Bash** (UNIX kabuğu).</span><span class="sxs-lookup"><span data-stu-id="282a0-118">Start a command-line tool, such as **GitBash** (Windows) or **Bash** (Unix Shell).</span></span> <span data-ttu-id="282a0-119">OS X sistemleri üzerinde hello komut satırı hello erişebilirsiniz **Terminal** uygulama.</span><span class="sxs-lookup"><span data-stu-id="282a0-119">On OS X systems you can access hello command-line through hello **Terminal** application.</span></span>
2. <span data-ttu-id="282a0-120">Merhaba içerik toodeploy bulunduğu olduğu toohello dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="282a0-120">Navigate toohello directory where hello content toodeploy would be located.</span></span>
3. <span data-ttu-id="282a0-121">Komut tooinitialize yeni bir Git deposu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="282a0-121">Use hello following command tooinitialize a new Git repository:</span></span>

```bash  
git init
```

## <span data-ttu-id="282a0-122"><a name="Step2"></a>2. adım: içeriğinizi Yürüt</span><span class="sxs-lookup"><span data-stu-id="282a0-122"><a name="Step2"></a>Step 2: Commit your content</span></span>
<span data-ttu-id="282a0-123">Uygulama hizmeti çeşitli programlama dillerini içinde oluşturulan uygulamaları destekler.</span><span class="sxs-lookup"><span data-stu-id="282a0-123">App Service supports applications created in a variety of programming languages.</span></span> 

1. <span data-ttu-id="282a0-124">Deponuzda zaten içerik Atla içeriyorsa, bu işaret ve toopoint 2 aşağıdaki taşıyın.</span><span class="sxs-lookup"><span data-stu-id="282a0-124">If your repository already includes content skip this point and move toopoint 2 below.</span></span> <span data-ttu-id="282a0-125">Deponuzda zaten içeriği yalnızca içermiyorsa statik .html dosyasıyla gibi doldurun:</span><span class="sxs-lookup"><span data-stu-id="282a0-125">If your repository does not already include content simply populate with a static .html file as follows:</span></span> 
   
   * <span data-ttu-id="282a0-126">Bir metin düzenleyicisi kullanarak adlı yeni bir dosya oluşturun **index.html** hello Git deposunu hello kökü</span><span class="sxs-lookup"><span data-stu-id="282a0-126">Using a text editor, create a new file named **index.html** at hello root of hello Git repository</span></span>
   * <span data-ttu-id="282a0-127">Hello içeriği hello index.html için dosya ve kaydedin gibi metin aşağıdaki hello ekleyin: *Hello Git!*</span><span class="sxs-lookup"><span data-stu-id="282a0-127">Add hello following text as hello contents for hello index.html file and save it: *Hello Git!*</span></span>
2. <span data-ttu-id="282a0-128">Komut satırı Hello, Git deponuzu hello kök altında olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="282a0-128">From hello command-line, verify that you are under hello root of your Git repository.</span></span> <span data-ttu-id="282a0-129">Ardından komutu tooadd dosyaları tooyour deposu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="282a0-129">Then use hello following command tooadd files tooyour repository:</span></span>

```bash  
git add -A
```
3. <span data-ttu-id="282a0-130">Ardından, komutu aşağıdaki hello kullanarak hello değişiklikleri toohello depo Yürüt:</span><span class="sxs-lookup"><span data-stu-id="282a0-130">Next, commit hello changes toohello repository by using hello following command:</span></span>

```bash  
git commit -m "Hello Azure App Service"
```  

## <span data-ttu-id="282a0-131"><a name="Step3"></a>3. adım: hello uygulama hizmeti uygulama havuzu etkinleştir</span><span class="sxs-lookup"><span data-stu-id="282a0-131"><a name="Step3"></a>Step 3: Enable hello App Service app repository</span></span>
<span data-ttu-id="282a0-132">Aşağıdaki adımları tooenable App Service uygulamanız için bir Git deposu hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="282a0-132">Perform hello following steps tooenable a Git repository for your App Service app.</span></span>

1. <span data-ttu-id="282a0-133">İçinde toohello oturum [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="282a0-133">Log in toohello [Azure Portal].</span></span>
2. <span data-ttu-id="282a0-134">App Service uygulamanızın dikey penceresinde tıklayın **ayarlar > dağıtım kaynağı**.</span><span class="sxs-lookup"><span data-stu-id="282a0-134">In your App Service app's blade, click **Settings > Deployment source**.</span></span> <span data-ttu-id="282a0-135">Tıklatın **Kaynak Seç**, ardından **yerel Git deposu**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="282a0-135">Click **Choose source**, then click **Local Git Repository**, and then click **OK**.</span></span>  
   
    ![Yerel Git deposu](./media/app-service-deploy-local-git/local_git_selection.png)
3. <span data-ttu-id="282a0-137">İlk zaman ayarınız Azure deposunu varsa, toocreate oturum açma kimlik bilgileri için gerekir.</span><span class="sxs-lookup"><span data-stu-id="282a0-137">If this is your first time setting up a repository in Azure, you need toocreate login credentials for it.</span></span> <span data-ttu-id="282a0-138">Bunları hello Azure deposunu içine toolog ve anında iletme değişiklikler yerel Git deposundan kullanın.</span><span class="sxs-lookup"><span data-stu-id="282a0-138">You will use them toolog into hello Azure repository and push changes from your local Git repository.</span></span> <span data-ttu-id="282a0-139">Uygulamanızın dikey penceresinden tıklayın **ayarlar > Dağıtım kimlik bilgileri**, dağıtım kullanıcı adı ve parola yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="282a0-139">From your app's blade, click **Settings > Deployment credentials**, then configure your deployment username and password.</span></span> <span data-ttu-id="282a0-140">İşiniz bittiğinde tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="282a0-140">When you're done, click **Save**.</span></span>
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <span data-ttu-id="282a0-141"><a name="Step4"></a>Adım 4: projenizi dağıtma</span><span class="sxs-lookup"><span data-stu-id="282a0-141"><a name="Step4"></a>Step 4: Deploy your project</span></span>
<span data-ttu-id="282a0-142">Aşağıdaki adımları toopublish Merhaba, uygulama tooApp yerel Git kullanarak hizmeti kullanın.</span><span class="sxs-lookup"><span data-stu-id="282a0-142">Use hello following steps toopublish your app tooApp Service using Local Git.</span></span>

1. <span data-ttu-id="282a0-143">Hello Azure Portalı'nda, uygulamanızın dikey penceresinde tıklayın **ayarlar > Özellikler** hello için **Git URL'si**.</span><span class="sxs-lookup"><span data-stu-id="282a0-143">In your app's blade in hello Azure Portal, click **Settings > Properties** for hello **Git URL**.</span></span>
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    <span data-ttu-id="282a0-144">**Git URL'si** hello uzak başvuru toodeploy toofrom, yerel bir depodur.</span><span class="sxs-lookup"><span data-stu-id="282a0-144">**Git URL** is hello remote reference toodeploy toofrom your local repository.</span></span> <span data-ttu-id="282a0-145">Bu URL aşağıdaki adımları hello kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="282a0-145">You'll use this URL in hello following steps.</span></span>
2. <span data-ttu-id="282a0-146">Merhaba komut satırı kullanarak, yerel Git deponuzu hello kök dizininde olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="282a0-146">Using hello command-line, verify that you are in hello root of your local Git repository.</span></span>
3. <span data-ttu-id="282a0-147">Kullanım `git remote` tooadd hello uzak başvuru listelenen **Git URL'si** adım 1.</span><span class="sxs-lookup"><span data-stu-id="282a0-147">Use `git remote` tooadd hello remote reference listed in **Git URL** from step 1.</span></span> <span data-ttu-id="282a0-148">Komutunuzu benzer toohello aşağıdaki görünür:</span><span class="sxs-lookup"><span data-stu-id="282a0-148">Your command will look similar toohello following:</span></span>
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > <span data-ttu-id="282a0-149">Merhaba **uzak** komut adlandırılmış başvuru tooa uzak bir depo ekler.</span><span class="sxs-lookup"><span data-stu-id="282a0-149">hello **remote** command adds a named reference tooa remote repository.</span></span> <span data-ttu-id="282a0-150">Bu örnekte, web uygulamanızın depo için 'azure' adlı bir başvuru oluşturur.</span><span class="sxs-lookup"><span data-stu-id="282a0-150">In this example, it creates a reference named 'azure' for your web app's repository.</span></span>
   > 
   > 
4. <span data-ttu-id="282a0-151">İçerik tooApp hizmet itme hello kullanarak yeni **azure** uzak oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="282a0-151">Push your content tooApp Service using hello new **azure** remote you just created.</span></span>

```bash  
git push azure master
```
    You will be prompted for hello password you created earlier when you reset your deployment credentials in hello Azure Portal. Enter hello password (note that Gitbash does not echo asterisks toohello console as you type your password). 
5. <span data-ttu-id="282a0-152">Hello Azure Portal tooyour uygulamaya geri dönün.</span><span class="sxs-lookup"><span data-stu-id="282a0-152">Go back tooyour app in hello Azure Portal.</span></span> <span data-ttu-id="282a0-153">En son gönderme, bir günlük girişi hello görüntülenmelidir **dağıtımları** dikey.</span><span class="sxs-lookup"><span data-stu-id="282a0-153">A log entry of your most recent push should be displayed in hello **Deployments** blade.</span></span> 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. <span data-ttu-id="282a0-154">Merhaba tıklatın **Gözat** düğmesi hello uygulamanın dikey tooverify hello içerik hello üstündeki dağıtılan.</span><span class="sxs-lookup"><span data-stu-id="282a0-154">Click hello **Browse** button at hello top of hello app's blade tooverify hello content has been deployed.</span></span> 

## <span data-ttu-id="282a0-155"><a name="Step5"></a>Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="282a0-155"><a name="Step5"></a>Troubleshooting</span></span>
<span data-ttu-id="282a0-156">Merhaba Git toopublish tooan App Service uygulaması Azure'da kullanırken sık karşılaşılan sorunları veya hatalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="282a0-156">hello following are errors or problems commonly encountered when using Git toopublish tooan App Service app in Azure:</span></span>

- - -
<span data-ttu-id="282a0-157">**Belirti**: oluşturulamıyor tooaccess [siteURL]: tooconnect çok başarısız [scmAddress]</span><span class="sxs-lookup"><span data-stu-id="282a0-157">**Symptom**: Unable tooaccess '[siteURL]': Failed tooconnect too[scmAddress]</span></span>

<span data-ttu-id="282a0-158">**Neden**: hello uygulama hazır ve çalışır değilse bu hata oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="282a0-158">**Cause**: This error can occur if hello app is not up and running.</span></span>

<span data-ttu-id="282a0-159">**Çözümleme**: Başlangıç hello hello Azure Portal uygulamasında.</span><span class="sxs-lookup"><span data-stu-id="282a0-159">**Resolution**: Start hello app in hello Azure Portal.</span></span> <span data-ttu-id="282a0-160">Merhaba uygulama çalışmıyorsa Git dağıtımı çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="282a0-160">Git deployment will not work unless hello app is running.</span></span> 

- - -
<span data-ttu-id="282a0-161">**Belirti**: ana bilgisayar 'hostname' çözümleyemedik</span><span class="sxs-lookup"><span data-stu-id="282a0-161">**Symptom**: Couldn't resolve host 'hostname'</span></span>

<span data-ttu-id="282a0-162">**Neden**: hello adres bilgilerini oluştururken girdiyseniz bu hata hello 'azure' uzak yanlış oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="282a0-162">**Cause**: This error can occur if hello address information entered when creating hello 'azure' remote was incorrect.</span></span>

<span data-ttu-id="282a0-163">**Çözümleme**: kullanım hello `git remote -v` toolist hello ilişkili URL ile birlikte tüm uzaktan kumandalar komutu.</span><span class="sxs-lookup"><span data-stu-id="282a0-163">**Resolution**: Use hello `git remote -v` command toolist all remotes, along with hello associated URL.</span></span> <span data-ttu-id="282a0-164">Merhaba 'azure' uzak Hello URL'sini doğru olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="282a0-164">Verify that hello URL for hello 'azure' remote is correct.</span></span> <span data-ttu-id="282a0-165">Gerekirse, kaldırın ve bu uzak hello doğru URL'yi kullanarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="282a0-165">If needed, remove and recreate this remote using hello correct URL.</span></span>

- - -
<span data-ttu-id="282a0-166">**Belirti**: ortak hiçbir refs ve hiçbiri belirtilen; hiçbir şey yapılması.</span><span class="sxs-lookup"><span data-stu-id="282a0-166">**Symptom**: No refs in common and none specified; doing nothing.</span></span> <span data-ttu-id="282a0-167">Belki 'master' gibi bir dal belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="282a0-167">Perhaps you should specify a branch such as 'master'.</span></span>

<span data-ttu-id="282a0-168">**Neden**:, değil git itme işlemi gerçekleştirirken bir dal belirtin ve Git tarafından kullanılan ayarlanmamış hello push.default değerine varsa bu hata oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="282a0-168">**Cause**: This error can occur if you do not specify a branch when performing a git push operation, and have not set hello push.default value used by Git.</span></span>

<span data-ttu-id="282a0-169">**Çözümleme**: hello ana dala belirtme hello gönderme işlemi yeniden gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="282a0-169">**Resolution**: Perform hello push operation again, specifying hello master branch.</span></span> <span data-ttu-id="282a0-170">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="282a0-170">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="282a0-171">**Belirti**: src refspec [branchname] herhangi eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="282a0-171">**Symptom**: src refspec [branchname] does not match any.</span></span>

<span data-ttu-id="282a0-172">**Neden**: toopush tooa şube hello 'azure' uzak yöneticisinde dışında çalışırsanız, bu hata oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="282a0-172">**Cause**: This error can occur if you attempt toopush tooa branch other than master on hello 'azure' remote.</span></span>

<span data-ttu-id="282a0-173">**Çözümleme**: hello ana dala belirtme hello gönderme işlemi yeniden gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="282a0-173">**Resolution**: Perform hello push operation again, specifying hello master branch.</span></span> <span data-ttu-id="282a0-174">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="282a0-174">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="282a0-175">**Belirti**: RPC başarısız oldu; yol = 22, HTTP kodu 502 =.</span><span class="sxs-lookup"><span data-stu-id="282a0-175">**Symptom**: RPC failed; result=22, HTTP code = 502.</span></span>

<span data-ttu-id="282a0-176">**Neden**: HTTPS üzerinden toopush büyük git deposu çalışırsanız, bu hata oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="282a0-176">**Cause**: This error can occur if you attempt toopush a large git repository over HTTPS.</span></span>

<span data-ttu-id="282a0-177">**Çözümleme**: hello yerel makine toomake hello postBuffer büyük üzerinde hello git yapılandırmasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="282a0-177">**Resolution**: Change hello git configuration on hello local machine toomake hello postBuffer bigger</span></span>

```bash  
git config --global http.postBuffer 524288000
```
- - -
<span data-ttu-id="282a0-178">**Belirti**: hata - web uygulamanızı güncelleştirilmemiş ancak değişiklikleri taahhüt tooremote deposu.</span><span class="sxs-lookup"><span data-stu-id="282a0-178">**Symptom**: Error - Changes committed tooremote repository but your web app not updated.</span></span>

<span data-ttu-id="282a0-179">**Neden**: ek gerekli modüllerini belirten bir package.json dosyası içeren bir Node.js uygulaması dağıtıyorsanız bu hata oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="282a0-179">**Cause**: This error can occur if you are deploying a Node.js app containing a package.json file that specifies additional required modules.</span></span>

<span data-ttu-id="282a0-180">**Çözümleme**: 'npm hata!' içeren ek iletiler</span><span class="sxs-lookup"><span data-stu-id="282a0-180">**Resolution**: Additional messages containing 'npm ERR!'</span></span> <span data-ttu-id="282a0-181">günlüğe kaydedilen önceki toothis hata olmalıdır ve ek bağlam hello hatada sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="282a0-181">should be logged prior toothis error, and can provide additional context on hello failure.</span></span> <span data-ttu-id="282a0-182">Merhaba aşağıdaki bu hatanın nedeni bilinen ve karşılık gelen 'npm hata!' hello</span><span class="sxs-lookup"><span data-stu-id="282a0-182">hello following are known causes of this error and hello corresponding 'npm ERR!'</span></span> <span data-ttu-id="282a0-183">İleti:</span><span class="sxs-lookup"><span data-stu-id="282a0-183">message:</span></span>

* <span data-ttu-id="282a0-184">**Hatalı biçimlendirilmiş package.json dosyası**: npm hata!</span><span class="sxs-lookup"><span data-stu-id="282a0-184">**Malformed package.json file**: npm ERR!</span></span> <span data-ttu-id="282a0-185">Bağımlılıklar okunamadı.</span><span class="sxs-lookup"><span data-stu-id="282a0-185">Couldn't read dependencies.</span></span>
* <span data-ttu-id="282a0-186">**İkili bir dağıtım için Windows olmayan yerel modül**:</span><span class="sxs-lookup"><span data-stu-id="282a0-186">**Native module that does not have a binary distribution for Windows**:</span></span>
  
  * <span data-ttu-id="282a0-187">npm hata!</span><span class="sxs-lookup"><span data-stu-id="282a0-187">npm ERR!</span></span> <span data-ttu-id="282a0-188">\`cmd "/ c" "düğümü gyp yeniden oluşturma"\` 1 ile başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="282a0-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span></span>
    
      <span data-ttu-id="282a0-189">OR</span><span class="sxs-lookup"><span data-stu-id="282a0-189">OR</span></span>
  * <span data-ttu-id="282a0-190">npm hata!</span><span class="sxs-lookup"><span data-stu-id="282a0-190">npm ERR!</span></span> <span data-ttu-id="282a0-191">[modulename@version] önceden: \`olun || gmake\`</span><span class="sxs-lookup"><span data-stu-id="282a0-191">[modulename@version] preinstall: \`make || gmake\`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="282a0-192">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="282a0-192">Additional Resources</span></span>
* [<span data-ttu-id="282a0-193">Git belgeleri</span><span class="sxs-lookup"><span data-stu-id="282a0-193">Git documentation</span></span>](http://git-scm.com/documentation)
* [<span data-ttu-id="282a0-194">Proje Kudu belgeleri</span><span class="sxs-lookup"><span data-stu-id="282a0-194">Project Kudu documentation</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="282a0-195">Sürekli dağıtım tooAzure uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="282a0-195">Continous Deployment tooAzure App Service</span></span>](app-service-continuous-deployment.md)
* [<span data-ttu-id="282a0-196">Nasıl toouse Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="282a0-196">How toouse PowerShell for Azure</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="282a0-197">Nasıl toouse hello Azure komut satırı arabirimi</span><span class="sxs-lookup"><span data-stu-id="282a0-197">How toouse hello Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)

[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[Azure Portal]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Azure komut satırı arabirimi]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
