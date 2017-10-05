---
title: "Azure’da bir Jenkins sunucusu oluşturma"
description: "Jenkins çözüm şablonundan Azure Linux sanal makinesine Jenkins’i yükleyin ve örnek bir Java uygulaması oluşturun."
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 7bb74f297d52fb25171817175cce64187b397c38
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-the-azure-portal"></a><span data-ttu-id="04b5f-103">Azure portalından Azure Linux VM'de bir Jenkins sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="04b5f-103">Create a Jenkins server on an Azure Linux VM from the Azure portal</span></span>

<span data-ttu-id="04b5f-104">Bu hızlı başlangıç, Ubuntu Linux VM'de araçları ve eklentileri Azure ile çalışmak için yapılandırılmış [Jenkins](https://jenkins.io)’in nasıl yükleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="04b5f-104">This quickstart shows how to install [Jenkins](https://jenkins.io) on an Ubuntu Linux VM with the tools and plug-ins configured to work with Azure.</span></span> <span data-ttu-id="04b5f-105">İşlemi tamamladığınızda, Azure‘da çalışan bir Jenkins sunucusuna sahip ve [GitHub](https://github.com)’dan örnek bir Java uygulaması oluşturmuş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="04b5f-105">When you're finished, you have a Jenkins server running in Azure building a sample Java app from [GitHub](https://github.com).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04b5f-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="04b5f-106">Prerequisites</span></span>

* <span data-ttu-id="04b5f-107">Bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="04b5f-107">An Azure subscription</span></span>
* <span data-ttu-id="04b5f-108">Bilgisayarınızın komut satırından (Bash kabuğu veya [PuTTY](http://www.putty.org/) gibi) SSH’ye erişin.</span><span class="sxs-lookup"><span data-stu-id="04b5f-108">Access to SSH on your computer's command line (such as the Bash shell or [PuTTY](http://www.putty.org/))</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-the-jenkins-vm-from-the-solution-template"></a><span data-ttu-id="04b5f-109">Çözüm şablonundan Jenkins VM’si oluşturma</span><span class="sxs-lookup"><span data-stu-id="04b5f-109">Create the Jenkins VM from the solution template</span></span>

<span data-ttu-id="04b5f-110">Web tarayıcınızda [Jenkins için mağaza görüntüsü](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) adresine gidin ve sayfanın sol tarafındaki **ŞİMDİ EDİN** bağlantısını seçin.</span><span class="sxs-lookup"><span data-stu-id="04b5f-110">Open the [marketplace image for Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) in your web browser and select  **GET IT NOW** from the left-hand side of the page.</span></span> <span data-ttu-id="04b5f-111">Fiyatlandırma ayrıntılarını gözden geçirin ve **Devam**’ı seçin, ardından Azure portalında Jenkins sunucusunu yapılandırmak için **Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="04b5f-111">Review the pricing details and select **Continue**, then select **Create** to configure the Jenkins server in the Azure portal.</span></span> 
   
![Azure portalı iletişim kutusu](./media/install-jenkins-solution-template/ap-create.png)

<span data-ttu-id="04b5f-113">**Temel ayarları yapılandırma** sekmesinde, aşağıdaki alanları doldurun:</span><span class="sxs-lookup"><span data-stu-id="04b5f-113">In the **Configure basic settings** tab, fill in the following fields:</span></span>

![Temel ayarları yapılandırma](./media/install-jenkins-solution-template/ap-basic.png)

* <span data-ttu-id="04b5f-115">**Ad** olarak **Jenkins** yazın.</span><span class="sxs-lookup"><span data-stu-id="04b5f-115">Use **Jenkins** for **Name**.</span></span>
* <span data-ttu-id="04b5f-116">Bir **Kullanıcı adı** girin.</span><span class="sxs-lookup"><span data-stu-id="04b5f-116">Enter a **User name**.</span></span> <span data-ttu-id="04b5f-117">Kullanıcı adı [belirli gereksinimleri](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm) karşılamalıdır.</span><span class="sxs-lookup"><span data-stu-id="04b5f-117">The user name must meet [specific requirements](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span></span>
* <span data-ttu-id="04b5f-118">**Kimlik doğrulama türü** olarak **Parola**’yı seçin ve bir parola girin.</span><span class="sxs-lookup"><span data-stu-id="04b5f-118">Select **Password** as the **Authentication type** and enter a password.</span></span> <span data-ttu-id="04b5f-119">Parola bir büyük harf karakter, bir sayı ve bir özel karakter içermelidir.</span><span class="sxs-lookup"><span data-stu-id="04b5f-119">The password must have an upper case character, a number, and one special character.</span></span>
* <span data-ttu-id="04b5f-120">**Kaynak grubu** için **myJenkinsResourceGroup** değerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="04b5f-120">Use **myJenkinsResourceGroup** for the **Resource Group**.</span></span>
* <span data-ttu-id="04b5f-121">**Konum** açılır menüsünden **Doğu ABD** [Azure bölgesini](https://azure.microsoft.com/regions/) seçin.</span><span class="sxs-lookup"><span data-stu-id="04b5f-121">Choose the **East US** [Azure region](https://azure.microsoft.com/regions/) from the **Location** drop-down.</span></span>

<span data-ttu-id="04b5f-122">**Ek seçenekleri yapılandırma** sekmesine geçmek için **Tamam**’ı seçin. Jenkins sunucusunu belirtecek benzersiz bir etki alanı adı girin ve **Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="04b5f-122">Select **OK** to proceed to the **Configure additional options** tab. Enter a unique domain name to identify the Jenkins server and select **OK**.</span></span>

![Ek seçenekleri ayarlama](./media/install-jenkins-solution-template/ap-addtional.png)  

 <span data-ttu-id="04b5f-124">Doğrulama başarılı olduktan sonra **Özet** sekmesinde tekrar **Tamam**’ı seçin. Son olarak da Jenkins VM’sini oluşturmak için **Satın al**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="04b5f-124">Once validation passes, select **OK** again from the **Summary** tab. Finally, select **Purchase** to create the Jenkins VM.</span></span> <span data-ttu-id="04b5f-125">Sunucunuz hazır olduğunda, Azure portalında bir bildirim alırsınız:</span><span class="sxs-lookup"><span data-stu-id="04b5f-125">When your server is ready, you get a notification in the Azure portal:</span></span>   

![Jenkins hazır bildirimi](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-to-jenkins"></a><span data-ttu-id="04b5f-127">Jenkins’e bağlanma</span><span class="sxs-lookup"><span data-stu-id="04b5f-127">Connect to Jenkins</span></span>

<span data-ttu-id="04b5f-128">Web tarayıcınızdan sanal makinenize (örneğin http://jenkins2517454.eastus.cloudapp.azure.com/) gidin.</span><span class="sxs-lookup"><span data-stu-id="04b5f-128">Navigate to your virtual machine (for example, http://jenkins2517454.eastus.cloudapp.azure.com/) in  your web browser.</span></span> <span data-ttu-id="04b5f-129">Jenkins konsoluna güvenli olmayan HTTP üzerinden erişilemeyeceğinden Jenkins konsoluna bilgisayarınızdan SSH tüneli kullanarak güvenli bir şekilde erişmek için yönergeler bu sayfada sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="04b5f-129">The Jenkins console is inaccessible through unsecured HTTP so instructions are provided on the page to access the Jenkins console securely from your computer using an SSH tunnel.</span></span>

![Jenkins’in kilidini açma](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

<span data-ttu-id="04b5f-131">Komut satırından `ssh` komutunu kullanarak tüneli ayarlayın. `username` değerini çözüm şablonundan sanal makineyi ayarlarken seçtiğiniz sanal makine yönetici kullanıcısının adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="04b5f-131">Set up the tunnel using the `ssh` command on the page from the command line, replacing `username` with the name of the virtual machine admin user chosen earlier when setting up the virtual machine from the solution template.</span></span>

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

<span data-ttu-id="04b5f-132">Tüneli başlattıktan sonra, yerel makinenizde http://localhost:8080/ adresine gidin.</span><span class="sxs-lookup"><span data-stu-id="04b5f-132">After you have started the tunnel, navigate to http://localhost:8080/ on your local machine.</span></span> 

<span data-ttu-id="04b5f-133">İlk parolayı Jenkins VM’ye SSH üzerinden bağlanırken bir komut satırında aşağıdaki komutu çalıştırarak alın.</span><span class="sxs-lookup"><span data-stu-id="04b5f-133">Get the initial password by running the following command in the command line while connected through SSH to the Jenkins VM.</span></span>

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

<span data-ttu-id="04b5f-134">Bu ilk yönetici parolasıyla Jenkins panosunun kilidini ilk kez açın.</span><span class="sxs-lookup"><span data-stu-id="04b5f-134">Unlock the Jenkins dashboard for the first time using this initial password.</span></span>

![Jenkins’in kilidini açma](./media/install-jenkins-solution-template/jenkins-unlock.png)

<span data-ttu-id="04b5f-136">Sonraki sayfada **Önerilen eklentileri yükle**’yi seçin ve Jenkins panosuna erişmek için kullanılacak bir Jenkins yönetici kullanıcısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="04b5f-136">Select **Install suggested plugins** on the next page and then create a Jenkins admin user used to access the Jenkins dashboard.</span></span>

![Jenkins hazır!](./media/install-jenkins-solution-template/jenkins-welcome.png)

<span data-ttu-id="04b5f-138">Jenkins sunucusu artık kod oluşturmak için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="04b5f-138">The Jenkins server is now ready to build code.</span></span>

## <a name="create-your-first-job"></a><span data-ttu-id="04b5f-139">İlk işinizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="04b5f-139">Create your first job</span></span>

<span data-ttu-id="04b5f-140">Jenkins konsolundan **Yeni iş oluştur**’u seçin, ardından işi **mySampleApp** olarak adlandırıp **Serbest tarzda proje**seçeneğini belirleyin ve **Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="04b5f-140">Select **Create new jobs** from the Jenkins console, then name it **mySampleApp** and select **Freestyle project**, then select **OK**.</span></span>

![Yeni bir iş oluşturma](./media/install-jenkins-solution-template/jenkins-new-job.png) 

<span data-ttu-id="04b5f-142">**Kaynak Kod Yönetimi** sekmesini seçin, **Git**’i etkinleştirin ve **Depo URL'si** alanına aşağıdaki URL'yi girin :`https://github.com/spring-guides/gs-spring-boot.git`</span><span class="sxs-lookup"><span data-stu-id="04b5f-142">Select the **Source Code Management** tab, enable **Git**, and enter the following URL in **Repository URL**  field: `https://github.com/spring-guides/gs-spring-boot.git`</span></span>

![Git deposunu tanımlayın](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

<span data-ttu-id="04b5f-144">**Yapı** sekmesini ve ardından **Yapı ekleme adımı**’nı ve **Gradle betiğini başlat**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="04b5f-144">Select the **Build** tab, then select **Add build step**, **Invoke Gradle script**.</span></span> <span data-ttu-id="04b5f-145">**Gradle sarmalayıcıyı kullan**’ı seçin, ardından **Sarmalayıcı konumu**’na `complete` değerini, **Görevler** için `build` değerini girin.</span><span class="sxs-lookup"><span data-stu-id="04b5f-145">Select **Use Gradle Wrapper**, then enter `complete` in **Wrapper location** and `build` for **Tasks**.</span></span>

![Derlemek için Gradle sarmalayıcıyı kullanma](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

<span data-ttu-id="04b5f-147">**Gelişmiş...**’i seçin</span><span class="sxs-lookup"><span data-stu-id="04b5f-147">Select **Advanced..**</span></span> <span data-ttu-id="04b5f-148">ve ardından **Kök Yapı betiği** alanına `complete` değerini girin.</span><span class="sxs-lookup"><span data-stu-id="04b5f-148">and then enter `complete` in the **Root Build script** field.</span></span> <span data-ttu-id="04b5f-149">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="04b5f-149">Select **Save**.</span></span>

![Gradle sarmalayıcısı derleme adımında Gelişmiş ayarları belirleme](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-the-code"></a><span data-ttu-id="04b5f-151">Kodu oluşturma</span><span class="sxs-lookup"><span data-stu-id="04b5f-151">Build the code</span></span>

<span data-ttu-id="04b5f-152">Kodu derlemek ve örnek uygulamayı paketlemek için **Şimdi Derle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="04b5f-152">Select **Build Now** to compile the code and package the sample app.</span></span> <span data-ttu-id="04b5f-153">Yapınız tamamlandığında proje için **Çalışma alanı** bağlantısını seçin.</span><span class="sxs-lookup"><span data-stu-id="04b5f-153">When your build completes, select the **Workspace** link for the project.</span></span>

![Derlemeden JAR dosyasını almak için çalışma alanına göz atma](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

<span data-ttu-id="04b5f-155">Yapınızın başarılı olduğunu doğrulamak için `complete/build/libs` konumuna gidin ve `gs-spring-boot-0.1.0.jar` dosyasının olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="04b5f-155">Navigate to `complete/build/libs` and ensure the `gs-spring-boot-0.1.0.jar` is there to verify that your build was successful.</span></span> <span data-ttu-id="04b5f-156">Jenkins sunucunuz artık Azure’da projelerinizi derlemeye hazırdır.</span><span class="sxs-lookup"><span data-stu-id="04b5f-156">Your Jenkins server is now ready to build your own projects in Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04b5f-157">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="04b5f-157">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="04b5f-158">Jenkins aracıları olarak Azure VM'leri ekleme</span><span class="sxs-lookup"><span data-stu-id="04b5f-158">Add Azure VMs as Jenkins agents</span></span>](jenkins-azure-vm-agents.md)
