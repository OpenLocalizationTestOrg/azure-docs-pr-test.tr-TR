---
title: aaaCreate Azure Jenkins sunucuda
description: "Merhaba Jenkins çözüm şablonu Azure Linux sanal makineden Jenkins yükleyin ve bir örnek Java uygulaması oluşturma."
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 82ab2ac52594acba131414b449b608978591d4b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-hello-azure-portal"></a><span data-ttu-id="714ef-103">Azure Linux VM'de hello Azure Portalı'ndan bir Jenkins sunucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="714ef-103">Create a Jenkins server on an Azure Linux VM from hello Azure portal</span></span>

<span data-ttu-id="714ef-104">Bu hızlı başlangıç gösterir nasıl tooinstall [Jenkins](https://jenkins.io) hello Araçlar ve eklentiler yapılandırılmış toowork Ubuntu Linux VM'de Azure ile.</span><span class="sxs-lookup"><span data-stu-id="714ef-104">This quickstart shows how tooinstall [Jenkins](https://jenkins.io) on an Ubuntu Linux VM with hello tools and plug-ins configured toowork with Azure.</span></span> <span data-ttu-id="714ef-105">İşlemi tamamladığınızda, Azure‘da çalışan bir Jenkins sunucusuna sahip ve [GitHub](https://github.com)’dan örnek bir Java uygulaması oluşturmuş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="714ef-105">When you're finished, you have a Jenkins server running in Azure building a sample Java app from [GitHub](https://github.com).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="714ef-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="714ef-106">Prerequisites</span></span>

* <span data-ttu-id="714ef-107">Bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="714ef-107">An Azure subscription</span></span>
* <span data-ttu-id="714ef-108">Bilgisayarınızın komut satırında erişim tooSSH (Merhaba gibi Kabuk Bash veya [PuTTY](http://www.putty.org/))</span><span class="sxs-lookup"><span data-stu-id="714ef-108">Access tooSSH on your computer's command line (such as hello Bash shell or [PuTTY](http://www.putty.org/))</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-jenkins-vm-from-hello-solution-template"></a><span data-ttu-id="714ef-109">Merhaba Jenkins VM hello çözüm Şablondan Oluştur</span><span class="sxs-lookup"><span data-stu-id="714ef-109">Create hello Jenkins VM from hello solution template</span></span>

<span data-ttu-id="714ef-110">Açık hello [Market görüntüsü için Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) web tarayıcısı ve seçin **BT almak artık** hello sayfasının sol taraftaki hello.</span><span class="sxs-lookup"><span data-stu-id="714ef-110">Open hello [marketplace image for Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) in your web browser and select  **GET IT NOW** from hello left-hand side of hello page.</span></span> <span data-ttu-id="714ef-111">Gözden geçirme hello fiyatlandırma ayrıntıları ve select **devam**seçeneğini belirleyip **oluşturma** tooconfigure hello Jenkins hello Azure portal Server'da.</span><span class="sxs-lookup"><span data-stu-id="714ef-111">Review hello pricing details and select **Continue**, then select **Create** tooconfigure hello Jenkins server in hello Azure portal.</span></span> 
   
![Azure portalı iletişim kutusu](./media/install-jenkins-solution-template/ap-create.png)

<span data-ttu-id="714ef-113">Merhaba, **temel ayarları yapılandırmanız** sekmesinde, hello aşağıdaki alanları doldurun:</span><span class="sxs-lookup"><span data-stu-id="714ef-113">In hello **Configure basic settings** tab, fill in hello following fields:</span></span>

![Temel ayarları yapılandırma](./media/install-jenkins-solution-template/ap-basic.png)

* <span data-ttu-id="714ef-115">**Ad** olarak **Jenkins** yazın.</span><span class="sxs-lookup"><span data-stu-id="714ef-115">Use **Jenkins** for **Name**.</span></span>
* <span data-ttu-id="714ef-116">Bir **Kullanıcı adı** girin.</span><span class="sxs-lookup"><span data-stu-id="714ef-116">Enter a **User name**.</span></span> <span data-ttu-id="714ef-117">Merhaba kullanıcı adı karşılamalıdır [belirli gereksinimleri](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="714ef-117">hello user name must meet [specific requirements](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span></span>
* <span data-ttu-id="714ef-118">Seçin **parola** hello olarak **kimlik doğrulama türü** ve bir parola girin.</span><span class="sxs-lookup"><span data-stu-id="714ef-118">Select **Password** as hello **Authentication type** and enter a password.</span></span> <span data-ttu-id="714ef-119">Merhaba parolası, bir büyük harf karakter, sayı ve bir özel karakter olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="714ef-119">hello password must have an upper case character, a number, and one special character.</span></span>
* <span data-ttu-id="714ef-120">Kullanım **myJenkinsResourceGroup** hello için **kaynak grubu**.</span><span class="sxs-lookup"><span data-stu-id="714ef-120">Use **myJenkinsResourceGroup** for hello **Resource Group**.</span></span>
* <span data-ttu-id="714ef-121">Merhaba seçin **Doğu ABD** [Azure bölgesi](https://azure.microsoft.com/regions/) hello gelen **konumu** açılır.</span><span class="sxs-lookup"><span data-stu-id="714ef-121">Choose hello **East US** [Azure region](https://azure.microsoft.com/regions/) from hello **Location** drop-down.</span></span>

<span data-ttu-id="714ef-122">Seçin **Tamam** tooproceed toohello **ek seçenekleri yapılandırmak** sekmesi. Benzersiz etki alanı adı tooidentify hello Jenkins sunucusu girin ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="714ef-122">Select **OK** tooproceed toohello **Configure additional options** tab. Enter a unique domain name tooidentify hello Jenkins server and select **OK**.</span></span>

![Ek seçenekleri ayarlama](./media/install-jenkins-solution-template/ap-addtional.png)  

 <span data-ttu-id="714ef-124">Doğrulama başarılı sonra seçeneğini **Tamam** yeniden hello gelen **Özet** sekmesi. Son olarak, seçin **satın alma** toocreate hello Jenkins VM.</span><span class="sxs-lookup"><span data-stu-id="714ef-124">Once validation passes, select **OK** again from hello **Summary** tab. Finally, select **Purchase** toocreate hello Jenkins VM.</span></span> <span data-ttu-id="714ef-125">Sunucunuz hazır olduğunda, hello Azure portalında bir bildirim alın:</span><span class="sxs-lookup"><span data-stu-id="714ef-125">When your server is ready, you get a notification in hello Azure portal:</span></span>   

![Jenkins hazır bildirimi](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-toojenkins"></a><span data-ttu-id="714ef-127">TooJenkins Bağlan</span><span class="sxs-lookup"><span data-stu-id="714ef-127">Connect tooJenkins</span></span>

<span data-ttu-id="714ef-128">Web tarayıcınızda tooyour sanal makine (örneğin, http://jenkins2517454.eastus.cloudapp.azure.com/) gidin.</span><span class="sxs-lookup"><span data-stu-id="714ef-128">Navigate tooyour virtual machine (for example, http://jenkins2517454.eastus.cloudapp.azure.com/) in  your web browser.</span></span> <span data-ttu-id="714ef-129">Merhaba Jenkins konsol güvenli olmayan HTTP erişilemez olduğundan hello sayfa tooaccess hello Jenkins konsolunda bilgisayarınızdan SSH tüneli kullanarak güvenli bir şekilde yönergeler sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="714ef-129">hello Jenkins console is inaccessible through unsecured HTTP so instructions are provided on hello page tooaccess hello Jenkins console securely from your computer using an SSH tunnel.</span></span>

![Jenkins’in kilidini açma](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

<span data-ttu-id="714ef-131">Hello kullanarak hello tünel ayarlamak `ssh` hello komut satırından hello sayfasında komutu değiştirme `username` hello hello sanal Makine'yi hello çözüm şablondan ayarlarken daha önce seçilen hello sanal makine yönetici kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="714ef-131">Set up hello tunnel using hello `ssh` command on hello page from hello command line, replacing `username` with hello name of hello virtual machine admin user chosen earlier when setting up hello virtual machine from hello solution template.</span></span>

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

<span data-ttu-id="714ef-132">Merhaba tünel başlattıktan sonra toohttp://localhost:8080 gidin / yerel makinenizde.</span><span class="sxs-lookup"><span data-stu-id="714ef-132">After you have started hello tunnel, navigate toohttp://localhost:8080/ on your local machine.</span></span> 

<span data-ttu-id="714ef-133">Merhaba ilk parola hello komut satırında SSH toohello Jenkins VM bağlıyken komutu aşağıdaki hello çalıştırarak alın.</span><span class="sxs-lookup"><span data-stu-id="714ef-133">Get hello initial password by running hello following command in hello command line while connected through SSH toohello Jenkins VM.</span></span>

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

<span data-ttu-id="714ef-134">Merhaba Hello Jenkins panosunu ilk bu parolayı kullanarak ilk kez kilidini açın.</span><span class="sxs-lookup"><span data-stu-id="714ef-134">Unlock hello Jenkins dashboard for hello first time using this initial password.</span></span>

![Jenkins’in kilidini açma](./media/install-jenkins-solution-template/jenkins-unlock.png)

<span data-ttu-id="714ef-136">Seçin **önerilen Eklentileri yüklemek** hello sonraki sayfa ve bir Jenkins yönetici kullanıcı kullanılan tooaccess hello Jenkins pano oluşturun.</span><span class="sxs-lookup"><span data-stu-id="714ef-136">Select **Install suggested plugins** on hello next page and then create a Jenkins admin user used tooaccess hello Jenkins dashboard.</span></span>

![Jenkins hazır!](./media/install-jenkins-solution-template/jenkins-welcome.png)

<span data-ttu-id="714ef-138">Merhaba Jenkins sunucu şimdi hazır toobuild kodudur.</span><span class="sxs-lookup"><span data-stu-id="714ef-138">hello Jenkins server is now ready toobuild code.</span></span>

## <a name="create-your-first-job"></a><span data-ttu-id="714ef-139">İlk işinizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="714ef-139">Create your first job</span></span>

<span data-ttu-id="714ef-140">Seçin **yeni iş oluşturma** hello Jenkins konsolundan adını **mySampleApp** seçip **Serbest stilde proje**seçeneğini belirleyip **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="714ef-140">Select **Create new jobs** from hello Jenkins console, then name it **mySampleApp** and select **Freestyle project**, then select **OK**.</span></span>

![Yeni bir iş oluşturma](./media/install-jenkins-solution-template/jenkins-new-job.png) 

<span data-ttu-id="714ef-142">Select hello **kaynak kodu Yönetimi** sekmesinde, etkinleştirme **Git**, URL'de aşağıdaki hello girin **depo URL'si** alan:`https://github.com/spring-guides/gs-spring-boot.git`</span><span class="sxs-lookup"><span data-stu-id="714ef-142">Select hello **Source Code Management** tab, enable **Git**, and enter hello following URL in **Repository URL**  field: `https://github.com/spring-guides/gs-spring-boot.git`</span></span>

![Merhaba Git deposuna tanımlayın](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

<span data-ttu-id="714ef-144">Select hello **yapı** sekmesini ve ardından **Ekle derleme adımı**, **çağırma Gradle betik**.</span><span class="sxs-lookup"><span data-stu-id="714ef-144">Select hello **Build** tab, then select **Add build step**, **Invoke Gradle script**.</span></span> <span data-ttu-id="714ef-145">**Gradle sarmalayıcıyı kullan**’ı seçin, ardından **Sarmalayıcı konumu**’na `complete` değerini, **Görevler** için `build` değerini girin.</span><span class="sxs-lookup"><span data-stu-id="714ef-145">Select **Use Gradle Wrapper**, then enter `complete` in **Wrapper location** and `build` for **Tasks**.</span></span>

![Merhaba Gradle sarmalayıcı toobuild kullanın](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

<span data-ttu-id="714ef-147">**Gelişmiş...**’i seçin</span><span class="sxs-lookup"><span data-stu-id="714ef-147">Select **Advanced..**</span></span> <span data-ttu-id="714ef-148">ve ardından girin `complete` hello içinde **kök yapı betik** alan.</span><span class="sxs-lookup"><span data-stu-id="714ef-148">and then enter `complete` in hello **Root Build script** field.</span></span> <span data-ttu-id="714ef-149">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="714ef-149">Select **Save**.</span></span>

![Merhaba Gradle sarmalayıcı yapı adımda Gelişmiş ayarlar](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-hello-code"></a><span data-ttu-id="714ef-151">Merhaba kodu derleme</span><span class="sxs-lookup"><span data-stu-id="714ef-151">Build hello code</span></span>

<span data-ttu-id="714ef-152">Seçin **şimdi yapı** toocompile hello kodu ve paket hello örnek uygulama.</span><span class="sxs-lookup"><span data-stu-id="714ef-152">Select **Build Now** toocompile hello code and package hello sample app.</span></span> <span data-ttu-id="714ef-153">Merhaba, yapı tamamlandıktan sonra seçin **çalışma** hello projesi için bağlantı.</span><span class="sxs-lookup"><span data-stu-id="714ef-153">When your build completes, select hello **Workspace** link for hello project.</span></span>

![Toohello çalışma tooget hello JAR dosyasını hello yapıdan Gözat](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

<span data-ttu-id="714ef-155">Çok gidin`complete/build/libs` ve hello olun `gs-spring-boot-0.1.0.jar` yapınızın başarılı tooverify yoktur.</span><span class="sxs-lookup"><span data-stu-id="714ef-155">Navigate too`complete/build/libs` and ensure hello `gs-spring-boot-0.1.0.jar` is there tooverify that your build was successful.</span></span> <span data-ttu-id="714ef-156">Sunucu artık oldu, Jenkins toobuild kendi Azure projelerinde hazır.</span><span class="sxs-lookup"><span data-stu-id="714ef-156">Your Jenkins server is now ready toobuild your own projects in Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="714ef-157">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="714ef-157">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="714ef-158">Jenkins aracıları olarak Azure VM'leri ekleme</span><span class="sxs-lookup"><span data-stu-id="714ef-158">Add Azure VMs as Jenkins agents</span></span>](jenkins-azure-vm-agents.md)
