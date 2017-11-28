---
title: "aaaPublish kullanarak bir Docker kapsayıcısı hello Azure Araç Seti için Intellij | Microsoft Docs"
description: "Bilgi nasıl toopublish bir web uygulaması tooMicrosoft kullanarak bir Docker kapsayıcısı olarak Azure hello Azure Araç Seti Intellij için."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: bee94cb269ea707ae7ad55232e23e915aec48c34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="1f728-103">Intellij için hello Azure Araç Seti kullanarak bir web uygulaması Docker kapsayıcısı Yayımla</span><span class="sxs-lookup"><span data-stu-id="1f728-103">Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="1f728-104">Docker, web uygulamalarını dağıtmak için yaygın olarak kullanılan bir yöntem kapsayıcılardır.</span><span class="sxs-lookup"><span data-stu-id="1f728-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="1f728-105">Docker kapsayıcıları kullanarak, geliştiricilerin kendi tüm proje dosyalarını ve dağıtım tooa sunucusu için tek bir paket bağımlılıkları birleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="1f728-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="1f728-106">Merhaba Intellij için Azure Araç Seti basitleştirir bu işlem için Java geliştiricilerinin ekleyerek *Docker kapsayıcısı olarak Yayımla* dağıtım tooMicrosoft Azure özellikleri.</span><span class="sxs-lookup"><span data-stu-id="1f728-106">hello Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="1f728-107">Bu makalede hello adımları gerekli toopublish Docker kapsayıcılar olarak uygulamaları tooAzure anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1f728-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="1f728-108">Docker hakkında daha fazla bilgi hello üzerinde kullanılabilir [Docker Web sitesi].</span><span class="sxs-lookup"><span data-stu-id="1f728-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="1f728-109">Web uygulaması tooAzure Docker kapsayıcısı kullanarak yayımlama</span><span class="sxs-lookup"><span data-stu-id="1f728-109">Publish your web app tooAzure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="1f728-110">toopublish web uygulamanızı bir dağıtım için hazır yapı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f728-110">toopublish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="1f728-111">toolearn daha, hello fazla [yapıları oluşturma hakkında ek bilgi](#artifacts) bölümü.</span><span class="sxs-lookup"><span data-stu-id="1f728-111">toolearn more, see hello [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="1f728-112">En az bir kez hello Dağıtım Sihirbazı'nı tamamladıktan sonra ayarlarınızı çoğunu hello Sihirbazı'nı yeniden çalıştırdığınızda varsayılan olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f728-112">After you have completed hello deployment wizard at least once, most of your settings are used as defaults when you run hello wizard again.</span></span>
>

1. <span data-ttu-id="1f728-113">Web uygulaması projenizin Intellij içinde açın.</span><span class="sxs-lookup"><span data-stu-id="1f728-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="1f728-114">toostart hello **Docker kapsayıcısı olarak Yayımla** Sihirbazı'nı hello aşağıdakilerden birini yapın:</span><span class="sxs-lookup"><span data-stu-id="1f728-114">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="1f728-115">Merhaba, **proje** araç penceresi, projenize sağ tıklayın, **Azure**ve ardından **Docker kapsayıcısı olarak Yayımla**:</span><span class="sxs-lookup"><span data-stu-id="1f728-115">In hello **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![Merhaba Docker kapsayıcısı komut olarak Yayımla][PUB01]

   * <span data-ttu-id="1f728-117">Merhaba Intellij araç çubuğunda hello tıklatın **Yayımla grup** düğmesine tıklayın ve ardından **Docker kapsayıcısı olarak Yayımla**:</span><span class="sxs-lookup"><span data-stu-id="1f728-117">On hello IntelliJ toolbar, click hello **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="1f728-118">![Merhaba Docker kapsayıcısı komut olarak Yayımla][PUB02]</span><span class="sxs-lookup"><span data-stu-id="1f728-118">![hello Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="1f728-119">Merhaba **azure'da dağıtmak Docker kapsayıcısı** Sihirbazı açılır.</span><span class="sxs-lookup"><span data-stu-id="1f728-119">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Merhaba dağıtma Docker kapsayıcısı Azure Sihirbazı][PUB03]

3. <span data-ttu-id="1f728-121">Merhaba, **bir görüntü adı yazın, hello yapı'nın yolu seçin ve kullanılan Docker ana toobe denetleyin** penceresinde, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="1f728-121">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span> 

   <span data-ttu-id="1f728-122">a.</span><span class="sxs-lookup"><span data-stu-id="1f728-122">a.</span></span> <span data-ttu-id="1f728-123">Merhaba, **Docker görüntü adı** kutusuna, Docker ana bilgisayar için benzersiz bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="1f728-123">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="1f728-124">(Merhaba Sihirbazı otomatik olarak bir ad oluşturur, ancak bunu değiştirebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="1f728-124">(hello wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="1f728-125">b.</span><span class="sxs-lookup"><span data-stu-id="1f728-125">b.</span></span> <span data-ttu-id="1f728-126">Merhaba **ana** alanı önceden oluşturmuş olduğunuz tüm Docker ana bilgisayarlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="1f728-126">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="1f728-127">Merhaba aşağıdakilerden birini yapın:</span><span class="sxs-lookup"><span data-stu-id="1f728-127">Do either of hello following:</span></span> 
      * <span data-ttu-id="1f728-128">Varolan bir Docker ana bilgisayara varsa, web uygulaması tooit dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f728-128">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
      * <span data-ttu-id="1f728-129">toocreate Docker ana hello yeşil artı işaretini tıklatın (**+**).</span><span class="sxs-lookup"><span data-stu-id="1f728-129">toocreate a Docker host, click hello green plus sign (**+**).</span></span>  
       <span data-ttu-id="1f728-130">Merhaba **oluşturma Docker ana** iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="1f728-130">hello **Create Docker Host** dialog box opens.</span></span> 

      ![Docker kapsayıcısı üzerinde Azure Sihirbazı'nı dağıtma][PUB04a]

4. <span data-ttu-id="1f728-132">Merhaba, **hello yeni sanal makine yapılandırma** penceresinde hello aşağıdaki Docker ana bilgisayarınız hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1f728-132">In hello **Configure hello new virtual machine** window, provide hello following information about your Docker host.</span></span> <span data-ttu-id="1f728-133">(hello sihirbaz sizin için hello bilgilerin çoğunu otomatik olarak oluşturur, ancak herhangi birini değiştirebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="1f728-133">(hello wizard automatically generates most of hello information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="1f728-134">a.</span><span class="sxs-lookup"><span data-stu-id="1f728-134">a.</span></span> <span data-ttu-id="1f728-135">Merhaba, **adı** kutusuna, hello Docker ana bilgisayar için benzersiz bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="1f728-135">In hello **Name** box, enter a unique name for hello Docker host.</span></span> <span data-ttu-id="1f728-136">(Bu, hello almak için değil, daha önce belirtilen Docker görüntü adı hello aynı olur.)</span><span class="sxs-lookup"><span data-stu-id="1f728-136">(It is not hello same as hello Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="1f728-137">b.</span><span class="sxs-lookup"><span data-stu-id="1f728-137">b.</span></span> <span data-ttu-id="1f728-138">Merhaba, **abonelik** kutusuna, hello ana bilgisayarınız için kullandığınız Azure aboneliğini girin.</span><span class="sxs-lookup"><span data-stu-id="1f728-138">In hello **Subscription** box, enter hello Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="1f728-139">c.</span><span class="sxs-lookup"><span data-stu-id="1f728-139">c.</span></span> <span data-ttu-id="1f728-140">Merhaba, **bölge** kutusuna, ana bilgisayarınız bulunduğu hello coğrafi girin.</span><span class="sxs-lookup"><span data-stu-id="1f728-140">In hello **Region** box, enter hello geographical region where your host is located.</span></span>
      
   <span data-ttu-id="1f728-141">d.</span><span class="sxs-lookup"><span data-stu-id="1f728-141">d.</span></span> <span data-ttu-id="1f728-142">Merhaba üzerinde **işletim sistemi ve boyutu** sekmesinde, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="1f728-142">On hello **OS and Size** tab, do hello following:</span></span>      
      * <span data-ttu-id="1f728-143">**Ana bilgisayar işletim sistemi**: hello işletim sistemi hello sanal makine için ana bilgisayarınız içeren girin.</span><span class="sxs-lookup"><span data-stu-id="1f728-143">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="1f728-144">**Boyutu**: ana bilgisayarınız için hello sanal makine boyutu girin.</span><span class="sxs-lookup"><span data-stu-id="1f728-144">**Size**: Enter hello virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="1f728-145">e.</span><span class="sxs-lookup"><span data-stu-id="1f728-145">e.</span></span> <span data-ttu-id="1f728-146">Merhaba üzerinde **kaynak grubu** sekmesinde, hello aşağıdakilerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="1f728-146">On hello **Resource Group** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="1f728-147">**Yeni kaynak grubu**: konağınız için bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1f728-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="1f728-148">**Varolan bir kaynak grubu**: Azure hesabınızdan var olan bir kaynak grubu belirtin.</span><span class="sxs-lookup"><span data-stu-id="1f728-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="1f728-149">f.</span><span class="sxs-lookup"><span data-stu-id="1f728-149">f.</span></span> <span data-ttu-id="1f728-150">Merhaba üzerinde **ağ** sekmesinde, hello aşağıdakilerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="1f728-150">On hello **Network** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="1f728-151">**Yeni sanal ağ**: konağınız için bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1f728-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="1f728-152">**Varolan bir sanal ağı**: Azure hesabınızdan var olan bir sanal ağ belirtin.</span><span class="sxs-lookup"><span data-stu-id="1f728-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="1f728-153">g.</span><span class="sxs-lookup"><span data-stu-id="1f728-153">g.</span></span> <span data-ttu-id="1f728-154">Merhaba üzerinde **depolama** sekmesinde, hello aşağıdakilerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="1f728-154">On hello **Storage** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="1f728-155">**Yeni depolama hesabı**: konağınız için bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1f728-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="1f728-156">**Varolan bir depolama hesabı**: Azure hesabınızdan mevcut bir depolama hesabını belirtin.</span><span class="sxs-lookup"><span data-stu-id="1f728-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="1f728-157">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1f728-157">Click **Next**.</span></span>  
     <span data-ttu-id="1f728-158">Merhaba **günlük kimlik bilgilerini yapılandırın ve bağlantı noktası ayarları** penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="1f728-158">hello **Configure log in credentials and port settings** window opens.</span></span>

      ![kimlik bilgileri ve bağlantı noktası ayarları penceresinde Hello Yapılandır günlük][PUB05]

6. <span data-ttu-id="1f728-160">Seçenekler aşağıdaki hello birini seçin:</span><span class="sxs-lookup"><span data-stu-id="1f728-160">Select one of hello following options:</span></span>

      * <span data-ttu-id="1f728-161">**Azure anahtar Kasası'kimlik bilgileri içe**: önceden kaydedilen bir Azure aboneliğinizde depolanan kimlik bilgileri kümesi belirtin.</span><span class="sxs-lookup"><span data-stu-id="1f728-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="1f728-162">Bir hesabın veya hizmet sorumlusu ile oluşturulan bir Azure anahtar kasası başka bir hesap veya hello abonelik paylaşan hizmet sorumlusu tarafından otomatik olarak erişilebilir değil.</span><span class="sxs-lookup"><span data-stu-id="1f728-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="1f728-163">tooallow başka bir hesap veya hizmet asıl toouse hello anahtar kasası, hello Azure portal tooadd hello hesabı ya da hizmet sorumlusu kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f728-163">tooallow another account or service principal toouse hello key vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

      * <span data-ttu-id="1f728-164">**Yeni oturum açma kimlik bilgileri**: yeni bir oturum açma kimlik bilgileri kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1f728-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="1f728-165">Bu seçeneği seçerseniz, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="1f728-165">If you select this option, do hello following:</span></span>

        <span data-ttu-id="1f728-166">a.</span><span class="sxs-lookup"><span data-stu-id="1f728-166">a.</span></span> <span data-ttu-id="1f728-167">Hello üzerinde **VM kimlik** sekmesinde, Docker ana bilgisayarınız hello sanal makinesi oturum açma kimlik bilgilerini aşağıdaki hello sağlayın: * **kullanıcıadı**: sanal makine oturumunuzla hello kullanıcı adı girin kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="1f728-167">On hello **VM Credentials** tab, provide hello following information for hello virtual-machine login credentials of your Docker host: * **Username**: Enter hello username for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="1f728-168">* **Parola** ve **Onayla**: hello parola için sanal makine oturum açma kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="1f728-168">* **Password** and **Confirm**: Enter hello password for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="1f728-169">* **SSH**: Docker ana bilgisayarınız hello güvenli Kabuk (SSH) ayarlarını girin.</span><span class="sxs-lookup"><span data-stu-id="1f728-169">* **SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="1f728-170">Seçenekler aşağıdaki hello birini seçebilirsiniz: * **hiçbiri**: sanal makineniz SSH bağlantılara izin vermiyor belirtir.</span><span class="sxs-lookup"><span data-stu-id="1f728-170">You can select one of hello following options: * **None**: Specifies that your virtual machine does not allow SSH connections.</span></span>
                <span data-ttu-id="1f728-171">* **Otomatik oluşturma**: hello SSH yoluyla bağlanmak için gerekli ayarları otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1f728-171">* **Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
                <span data-ttu-id="1f728-172">* **Dizine alma**: toospecify önceden kaydedilmiş SSH ayarları kümesini içeren bir dizini sağlar.</span><span class="sxs-lookup"><span data-stu-id="1f728-172">* **Import from directory**: Allows you toospecify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="1f728-173">Merhaba dizin, aşağıdaki iki dosyaları hello içermelidir:</span><span class="sxs-lookup"><span data-stu-id="1f728-173">hello directory must contain hello following two files:</span></span>
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        <span data-ttu-id="1f728-174">b.</span><span class="sxs-lookup"><span data-stu-id="1f728-174">b.</span></span> <span data-ttu-id="1f728-175">Merhaba üzerinde **Docker arka plan programı erişim** sekmesinde, aşağıdaki bilgilerle hello sağlayın:</span><span class="sxs-lookup"><span data-stu-id="1f728-175">On hello **Docker Daemon Access** tab, provide hello following information:</span></span>

          ![Docker konak oluştur][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. <span data-ttu-id="1f728-177">Merhaba gerekli bilgileri girdikten sonra tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="1f728-177">After you have entered hello required information, click **Finish**.</span></span>  
    <span data-ttu-id="1f728-178">Merhaba **azure'da dağıtmak Docker kapsayıcısı** Sihirbazı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1f728-178">hello **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Docker kapsayıcısı üzerinde Azure Sihirbazı'nı dağıtma][PUB07]

8. <span data-ttu-id="1f728-180">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1f728-180">Click **Next**.</span></span>  
    <span data-ttu-id="1f728-181">Merhaba **oluşturulan hello Docker kapsayıcısı toobe yapılandırma** penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="1f728-181">hello **Configure hello Docker container toobe created** window opens.</span></span>

   ![Merhaba yapılandırma hello Docker kapsayıcısı oluşturulan toobe penceresi][PUB08]

9. <span data-ttu-id="1f728-183">Merhaba, **oluşturulan hello Docker kapsayıcısı toobe yapılandırma** penceresinde, aşağıdaki bilgilerle hello sağlayın:</span><span class="sxs-lookup"><span data-stu-id="1f728-183">In hello **Configure hello Docker container toobe created** window, provide hello following information:</span></span> 

   <span data-ttu-id="1f728-184">a.</span><span class="sxs-lookup"><span data-stu-id="1f728-184">a.</span></span> <span data-ttu-id="1f728-185">Merhaba, **Docker kapsayıcısı adı** kutusuna, Docker kapsayıcısı için benzersiz bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="1f728-185">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="1f728-186">b.</span><span class="sxs-lookup"><span data-stu-id="1f728-186">b.</span></span> <span data-ttu-id="1f728-187">Docker görüntüleri aşağıdaki hello birini seçin:</span><span class="sxs-lookup"><span data-stu-id="1f728-187">Choose one of hello following Docker images:</span></span> 

      * <span data-ttu-id="1f728-188">**Önceden tanımlanmış Docker görüntü**: azure'dan önceden var olan bir Docker görüntüsü belirtin.</span><span class="sxs-lookup"><span data-stu-id="1f728-188">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="1f728-189">Bu kutu Docker görüntülerinde Hello listesi, birkaç görüntülerini oluşur Azure Araç Seti açıldı, hello toopatch yapılandırılmış, yapı otomatik olarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="1f728-189">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="1f728-190">**Özel Dockerfile**: yerel bilgisayarınızdan önceden kaydedilmiş bir Dockerfile belirtin.</span><span class="sxs-lookup"><span data-stu-id="1f728-190">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="1f728-191">Bu, kendi Dockerfile toodeploy isteyen geliştiriciler için daha gelişmiş bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="1f728-191">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="1f728-192">Ancak, kendi Dockerfile doğru bir şekilde yapıldığından bu seçeneği tooensure kullanan toodevelopers değildir.</span><span class="sxs-lookup"><span data-stu-id="1f728-192">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="1f728-193">Hello Azure Araç Seti özel bir Dockerfile hello içeriği doğrulamaz çünkü hello Dockerfile sorunları varsa hello dağıtım başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f728-193">Because hello Azure Toolkit does not validate hello content in a custom Dockerfile, hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="1f728-194">Ayrıca, Hello Azure Araç Seti hello özel Dockerfile toocontain bir web uygulaması yapı beklediği tooopen bir HTTP bağlantısı çalışır.</span><span class="sxs-lookup"><span data-stu-id="1f728-194">In addition, because hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, it attempts tooopen an HTTP connection.</span></span> <span data-ttu-id="1f728-195">Geliştiriciler farklı türde bir yapı yayımlarsanız, bunlar dağıtım sonrası zararsız hatalar alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f728-195">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="1f728-196">c.</span><span class="sxs-lookup"><span data-stu-id="1f728-196">c.</span></span> <span data-ttu-id="1f728-197">Merhaba, **bağlantı noktası ayarları** kutusuna, hello benzersiz TCP bağlantı noktası için bağlama, Docker kapsayıcısı girin.</span><span class="sxs-lookup"><span data-stu-id="1f728-197">In hello **Port settings** box, enter hello unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="1f728-198">Merhaba önceki adımları tamamladıktan sonra tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="1f728-198">After you have completed hello preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="1f728-199">Hello Azure araç seti, web uygulama tooAzure Docker kapsayıcısı içinde dağıtmaya başlar.</span><span class="sxs-lookup"><span data-stu-id="1f728-199">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> <span data-ttu-id="1f728-200">Dağıtılan hello arka planda Intellij toobe yapılandırmadığınız sürece bir **tooAzure dağıtma** ilerleme çubuğu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1f728-200">Unless you have configured IntelliJ toobe deployed in hello background, a **Deploying tooAzure** progress bar appears.</span></span> 

![Merhaba dağıtım ilerleme çubuğu][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="1f728-202">Yapıları oluşturma hakkında ek bilgi</span><span class="sxs-lookup"><span data-stu-id="1f728-202">Additional information about creating artifacts</span></span>

<span data-ttu-id="1f728-203">bir dağıtım için hazır yapı toocreate hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="1f728-203">toocreate a deployment-ready artifact, do hello following:</span></span>

1. <span data-ttu-id="1f728-204">Web uygulaması projenizin Intellij içinde açın.</span><span class="sxs-lookup"><span data-stu-id="1f728-204">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="1f728-205">Tıklatın **dosya**ve ardından **proje yapısını**.</span><span class="sxs-lookup"><span data-stu-id="1f728-205">Click **File**, and then click **Project Structure**.</span></span>

   ![Merhaba proje yapısını komutu][ART01]

3. <span data-ttu-id="1f728-207">tooadd yapı bir hello yeşil artı işaretini tıklatın (**+**) ve ardından **Web uygulaması: Arşiv**.</span><span class="sxs-lookup"><span data-stu-id="1f728-207">tooadd an artifact, click hello green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![Merhaba "Web uygulaması: arşivi" komutu][ART02]

4. <span data-ttu-id="1f728-209">Merhaba, **adı** kutusuna, yapı için bir ad girin (Merhaba içermez *.war* uzantısı) ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="1f728-209">In hello **Name** box, enter a name for your artifact (do not include hello *.war* extension), and then click **OK**.</span></span>

   ![Merhaba yapı adı kutusu][ART03]

<span data-ttu-id="1f728-211">Intellij yapıları oluşturma hakkında daha fazla bilgi için bkz: [yapıları yapılandırma] hello JetBrains Web sitesinde.</span><span class="sxs-lookup"><span data-stu-id="1f728-211">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on hello JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f728-212">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1f728-212">Next steps</span></span>
<span data-ttu-id="1f728-213">Java IDE hello Azure araç takımları hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="1f728-213">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="1f728-214">[Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="1f728-214">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="1f728-215">[Merhaba Eclipse için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="1f728-215">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="1f728-216">[Yükleme hello Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="1f728-216">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="1f728-217">[Oturum açma hello Eclipse için Azure Araç Seti için yönergeler]</span><span class="sxs-lookup"><span data-stu-id="1f728-217">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="1f728-218">[Eclipse'te Azure Hello World web uygulaması oluşturma]</span><span class="sxs-lookup"><span data-stu-id="1f728-218">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="1f728-219">[IntelliJ için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="1f728-219">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="1f728-220">[Merhaba Intellij için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="1f728-220">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="1f728-221">[Yükleme hello Intellij için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="1f728-221">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="1f728-222">[Oturum açma hello Azure Araç Seti için Intellij için yönergeler]</span><span class="sxs-lookup"><span data-stu-id="1f728-222">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="1f728-223">[Intellij Azure'da Hello World web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="1f728-223">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="1f728-224">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi] ve hello [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="1f728-224">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="1f728-225">Merhaba resmi Docker için ek kaynaklar için bkz: [Docker Web sitesi].</span><span class="sxs-lookup"><span data-stu-id="1f728-225">For additional resources for Docker, see hello official [Docker website].</span></span>

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md
[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md
[Eclipse'te Azure Hello World web uygulaması oluşturma]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Intellij Azure'da Hello World web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Yükleme hello Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse-installation.md
[Yükleme hello Intellij için Azure Araç Seti]: ./azure-toolkit-for-intellij-installation.md
[Oturum açma hello Eclipse için Azure Araç Seti için yönergeler]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Oturum açma hello Azure Araç Seti için Intellij için yönergeler]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Merhaba Eclipse için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-eclipse-whats-new.md
[Merhaba Intellij için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/

[Docker Web sitesi]: https://www.docker.com/
[yapıları yapılandırma]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
