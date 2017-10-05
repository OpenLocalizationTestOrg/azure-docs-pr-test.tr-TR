---
title: "Intellij için Azure araç setini kullanarak bir Docker kapsayıcısı yayımlama | Microsoft Docs"
description: "Docker kapsayıcısı Microsoft Azure Intellij için Azure araç setini kullanarak bir web uygulaması yayımlama öğrenin."
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
ms.openlocfilehash: 96680319a6c4c0f0a4673cd6303a5b172f428797
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="9170f-103">Intellij için Azure araç setini kullanarak bir web uygulaması Docker kapsayıcısı Yayımla</span><span class="sxs-lookup"><span data-stu-id="9170f-103">Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="9170f-104">Docker, web uygulamalarını dağıtmak için yaygın olarak kullanılan bir yöntem kapsayıcılardır.</span><span class="sxs-lookup"><span data-stu-id="9170f-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="9170f-105">Docker kapsayıcıları kullanarak, geliştiricilerin kendi tüm proje dosyalarını ve tek bir paket için bir sunucu dağıtımı için bağımlılıkları birleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="9170f-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="9170f-106">Intellij için Azure araç seti, ekleyerek Java geliştiriciler için bu işlemi basitleştirir *Docker kapsayıcısı olarak Yayımla* Microsoft Azure dağıtım özellikleri.</span><span class="sxs-lookup"><span data-stu-id="9170f-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="9170f-107">Bu makalede, Azure, uygulamalarınızı Docker kapsayıcı olarak yayımlamak için gereken adımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9170f-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9170f-108">Docker hakkında daha fazla bilgi edinilebilir [Docker Web sitesi].</span><span class="sxs-lookup"><span data-stu-id="9170f-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="9170f-109">Docker kapsayıcısı kullanarak Azure için web uygulamanızı yayınlama</span><span class="sxs-lookup"><span data-stu-id="9170f-109">Publish your web app to Azure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="9170f-110">Web uygulamanızı yayımlamak için bir dağıtım için hazır yapı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9170f-110">To publish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="9170f-111">Daha fazla bilgi için bkz: [yapıları oluşturma hakkında ek bilgi](#artifacts) bölümü.</span><span class="sxs-lookup"><span data-stu-id="9170f-111">To learn more, see the [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="9170f-112">En az bir kez Dağıtım Sihirbazı'nı tamamladıktan sonra sihirbazı yeniden çalıştırın, ayarların çoğu varsayılanları olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9170f-112">After you have completed the deployment wizard at least once, most of your settings are used as defaults when you run the wizard again.</span></span>
>

1. <span data-ttu-id="9170f-113">Web uygulaması projenizin Intellij içinde açın.</span><span class="sxs-lookup"><span data-stu-id="9170f-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="9170f-114">Başlatmak için **Docker kapsayıcısı olarak Yayımla** Sihirbazı, aşağıdakilerden birini yapın:</span><span class="sxs-lookup"><span data-stu-id="9170f-114">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="9170f-115">İçinde **proje** araç penceresi, projenize sağ tıklayın, **Azure**ve ardından **Docker kapsayıcısı olarak Yayımla**:</span><span class="sxs-lookup"><span data-stu-id="9170f-115">In the **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![Docker kapsayıcısı komut olarak Yayımla][PUB01]

   * <span data-ttu-id="9170f-117">Intellij araç çubuğunda tıklatın **Yayımla grup** düğmesine tıklayın ve ardından **Docker kapsayıcısı olarak Yayımla**:</span><span class="sxs-lookup"><span data-stu-id="9170f-117">On the IntelliJ toolbar, click the **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="9170f-118">![Docker kapsayıcısı komut olarak Yayımla][PUB02]</span><span class="sxs-lookup"><span data-stu-id="9170f-118">![The Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="9170f-119">**Azure'da dağıtmak Docker kapsayıcısı** Sihirbazı açılır.</span><span class="sxs-lookup"><span data-stu-id="9170f-119">The **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Azure Sihirbazı dağıtmak Docker kapsayıcısı][PUB03]

3. <span data-ttu-id="9170f-121">İçinde **bir görüntü adı yazın, yapı'nın yolu seçin ve kullanılacak bir Docker ana denetleyin** penceresinde aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="9170f-121">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span> 

   <span data-ttu-id="9170f-122">a.</span><span class="sxs-lookup"><span data-stu-id="9170f-122">a.</span></span> <span data-ttu-id="9170f-123">İçinde **Docker görüntü adı** kutusuna, Docker ana bilgisayar için benzersiz bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="9170f-123">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="9170f-124">(Sihirbaz otomatik olarak bir ad oluşturur, ancak bunu değiştirebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="9170f-124">(The wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="9170f-125">b.</span><span class="sxs-lookup"><span data-stu-id="9170f-125">b.</span></span> <span data-ttu-id="9170f-126">**Ana** alanı önceden oluşturmuş olduğunuz tüm Docker ana bilgisayarlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9170f-126">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="9170f-127">Aşağıdakilerden birini yapın:</span><span class="sxs-lookup"><span data-stu-id="9170f-127">Do either of the following:</span></span> 
      * <span data-ttu-id="9170f-128">Varolan bir Docker ana bilgisayara varsa, web uygulamanızı dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9170f-128">If you have an existing Docker host, you can deploy your web app to it.</span></span>
      * <span data-ttu-id="9170f-129">Docker ana bilgisayar oluşturmak için yeşil artı işaretini tıklatın (**+**).</span><span class="sxs-lookup"><span data-stu-id="9170f-129">To create a Docker host, click the green plus sign (**+**).</span></span>  
       <span data-ttu-id="9170f-130">**Oluşturma Docker ana** iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="9170f-130">The **Create Docker Host** dialog box opens.</span></span> 

      ![Docker kapsayıcısı üzerinde Azure Sihirbazı'nı dağıtma][PUB04a]

4. <span data-ttu-id="9170f-132">İçinde **yeni sanal makine yapılandırma** penceresinde, Docker ana bilgisayarınız hakkında aşağıdaki bilgileri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="9170f-132">In the **Configure the new virtual machine** window, provide the following information about your Docker host.</span></span> <span data-ttu-id="9170f-133">(Sihirbaz için bu bilgileri çoğunu otomatik olarak oluşturur, ancak herhangi birini değiştirebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="9170f-133">(The wizard automatically generates most of the information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="9170f-134">a.</span><span class="sxs-lookup"><span data-stu-id="9170f-134">a.</span></span> <span data-ttu-id="9170f-135">İçinde **adı** kutusuna, Docker ana bilgisayar için benzersiz bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="9170f-135">In the **Name** box, enter a unique name for the Docker host.</span></span> <span data-ttu-id="9170f-136">(Bu, daha önce belirttiğiniz Docker görüntü adı ile aynı değildir.)</span><span class="sxs-lookup"><span data-stu-id="9170f-136">(It is not the same as the Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="9170f-137">b.</span><span class="sxs-lookup"><span data-stu-id="9170f-137">b.</span></span> <span data-ttu-id="9170f-138">İçinde **abonelik** kutusuna, ana bilgisayarınız için kullandığınız Azure aboneliğini girin.</span><span class="sxs-lookup"><span data-stu-id="9170f-138">In the **Subscription** box, enter the Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="9170f-139">c.</span><span class="sxs-lookup"><span data-stu-id="9170f-139">c.</span></span> <span data-ttu-id="9170f-140">İçinde **bölge** kutusuna, ana bilgisayarınız bulunduğu coğrafi bölge girin.</span><span class="sxs-lookup"><span data-stu-id="9170f-140">In the **Region** box, enter the geographical region where your host is located.</span></span>
      
   <span data-ttu-id="9170f-141">d.</span><span class="sxs-lookup"><span data-stu-id="9170f-141">d.</span></span> <span data-ttu-id="9170f-142">Üzerinde **işletim sistemi ve boyutu** sekmesinde, aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="9170f-142">On the **OS and Size** tab, do the following:</span></span>      
      * <span data-ttu-id="9170f-143">**Ana bilgisayar işletim sistemi**: ana bilgisayarınız içeren sanal makine için işletim sistemi girin.</span><span class="sxs-lookup"><span data-stu-id="9170f-143">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="9170f-144">**Boyutu**: ana bilgisayarınız için sanal makine boyutu girin.</span><span class="sxs-lookup"><span data-stu-id="9170f-144">**Size**: Enter the virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="9170f-145">e.</span><span class="sxs-lookup"><span data-stu-id="9170f-145">e.</span></span> <span data-ttu-id="9170f-146">Üzerinde **kaynak grubu** sekmesinde, aşağıdakilerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="9170f-146">On the **Resource Group** tab, select either of the following:</span></span>      
      * <span data-ttu-id="9170f-147">**Yeni kaynak grubu**: konağınız için bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9170f-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="9170f-148">**Varolan bir kaynak grubu**: Azure hesabınızdan var olan bir kaynak grubu belirtin.</span><span class="sxs-lookup"><span data-stu-id="9170f-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="9170f-149">f.</span><span class="sxs-lookup"><span data-stu-id="9170f-149">f.</span></span> <span data-ttu-id="9170f-150">Üzerinde **ağ** sekmesinde, aşağıdakilerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="9170f-150">On the **Network** tab, select either of the following:</span></span>      
      * <span data-ttu-id="9170f-151">**Yeni sanal ağ**: konağınız için bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9170f-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="9170f-152">**Varolan bir sanal ağı**: Azure hesabınızdan var olan bir sanal ağ belirtin.</span><span class="sxs-lookup"><span data-stu-id="9170f-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="9170f-153">g.</span><span class="sxs-lookup"><span data-stu-id="9170f-153">g.</span></span> <span data-ttu-id="9170f-154">Üzerinde **depolama** sekmesinde, aşağıdakilerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="9170f-154">On the **Storage** tab, select either of the following:</span></span>      
      * <span data-ttu-id="9170f-155">**Yeni depolama hesabı**: konağınız için bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9170f-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="9170f-156">**Varolan bir depolama hesabı**: Azure hesabınızdan mevcut bir depolama hesabını belirtin.</span><span class="sxs-lookup"><span data-stu-id="9170f-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="9170f-157">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9170f-157">Click **Next**.</span></span>  
     <span data-ttu-id="9170f-158">**Günlük kimlik bilgilerini yapılandırın ve bağlantı noktası ayarları** penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="9170f-158">The **Configure log in credentials and port settings** window opens.</span></span>

      ![Yapılandırma oturum açma kimlik bilgileri ve bağlantı noktası ayarları penceresi][PUB05]

6. <span data-ttu-id="9170f-160">Aşağıdaki seçeneklerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="9170f-160">Select one of the following options:</span></span>

      * <span data-ttu-id="9170f-161">**Azure anahtar Kasası'kimlik bilgileri içe**: önceden kaydedilen bir Azure aboneliğinizde depolanan kimlik bilgileri kümesi belirtin.</span><span class="sxs-lookup"><span data-stu-id="9170f-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="9170f-162">Bir hesabın veya hizmet sorumlusu ile oluşturulan bir Azure anahtar kasası başka bir hesap veya abonelik paylaşan hizmet sorumlusu tarafından otomatik olarak erişilebilir değil.</span><span class="sxs-lookup"><span data-stu-id="9170f-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="9170f-163">Başka bir hesap veya hizmet asıl anahtar kasası kullanmaya izin vermek için hesabı veya hizmet sorumlusu eklemek için Azure Portalı'nı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9170f-163">To allow another account or service principal to use the key vault, you must use the Azure portal to add the account or service principal.</span></span>

      * <span data-ttu-id="9170f-164">**Yeni oturum açma kimlik bilgileri**: yeni bir oturum açma kimlik bilgileri kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9170f-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="9170f-165">Bu seçeneği seçerseniz, aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="9170f-165">If you select this option, do the following:</span></span>

        <span data-ttu-id="9170f-166">a.</span><span class="sxs-lookup"><span data-stu-id="9170f-166">a.</span></span> <span data-ttu-id="9170f-167">Üzerinde **VM kimlik** sekmesinde, Docker ana bilgisayarın sanal makine oturum açma kimlik bilgileri için aşağıdaki bilgileri sağlayın: * **kullanıcıadı**: kullanıcı için sanal makine oturum açma kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="9170f-167">On the **VM Credentials** tab, provide the following information for the virtual-machine login credentials of your Docker host: * **Username**: Enter the username for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="9170f-168">* **Parola** ve **Onayla**: parola için sanal makine oturum açma kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="9170f-168">* **Password** and **Confirm**: Enter the password for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="9170f-169">* **SSH**: Docker ana bilgisayarınız Güvenli Kabuk (SSH) ayarlarını girin.</span><span class="sxs-lookup"><span data-stu-id="9170f-169">* **SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="9170f-170">Aşağıdaki seçeneklerden birini seçebilirsiniz: * **hiçbiri**: sanal makineniz SSH bağlantılara izin vermiyor belirtir.</span><span class="sxs-lookup"><span data-stu-id="9170f-170">You can select one of the following options: * **None**: Specifies that your virtual machine does not allow SSH connections.</span></span>
                <span data-ttu-id="9170f-171">* **Otomatik oluşturma**: SSH yoluyla bağlanmak için gerekli ayarları otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9170f-171">* **Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span>
                <span data-ttu-id="9170f-172">* **Dizine alma**: önceden kaydedilmiş SSH ayarları kümesini içeren bir dizini belirtmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="9170f-172">* **Import from directory**: Allows you to specify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="9170f-173">Dizin, aşağıdaki iki dosyada içermelidir:</span><span class="sxs-lookup"><span data-stu-id="9170f-173">The directory must contain the following two files:</span></span>
                
                  * *id_rsa*: Contains the RSA identification for a user.
                  * *id_rsa.pub*: Contains the RSA public key that is used for authentication.
            
        <span data-ttu-id="9170f-174">b.</span><span class="sxs-lookup"><span data-stu-id="9170f-174">b.</span></span> <span data-ttu-id="9170f-175">Üzerinde **Docker arka plan programı erişim** sekmesinde, aşağıdaki bilgileri sağlayın:</span><span class="sxs-lookup"><span data-stu-id="9170f-175">On the **Docker Daemon Access** tab, provide the following information:</span></span>

          ![Docker konak oluştur][PUB06]
    
             * **Docker Daemon port**: Enter the unique TCP port for your Docker host.
             * **TLS Security**: Enter the Transport Layer Security settings for your Docker host. You can choose from the following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates the requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. The directory must contain the following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain the client certificate and public key that is used for TLS authentication.

7. <span data-ttu-id="9170f-177">Gerekli bilgileri girdikten sonra tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="9170f-177">After you have entered the required information, click **Finish**.</span></span>  
    <span data-ttu-id="9170f-178">**Azure'da dağıtmak Docker kapsayıcısı** Sihirbazı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9170f-178">The **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Docker kapsayıcısı üzerinde Azure Sihirbazı'nı dağıtma][PUB07]

8. <span data-ttu-id="9170f-180">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9170f-180">Click **Next**.</span></span>  
    <span data-ttu-id="9170f-181">**Oluşturulacak Docker kapsayıcısı yapılandırma** penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="9170f-181">The **Configure the Docker container to be created** window opens.</span></span>

   ![Pencere oluşturulması için Docker kapsayıcısı Yapılandır][PUB08]

9. <span data-ttu-id="9170f-183">İçinde **oluşturulacak Docker kapsayıcısı yapılandırma** penceresinde, aşağıdaki bilgileri sağlayın:</span><span class="sxs-lookup"><span data-stu-id="9170f-183">In the **Configure the Docker container to be created** window, provide the following information:</span></span> 

   <span data-ttu-id="9170f-184">a.</span><span class="sxs-lookup"><span data-stu-id="9170f-184">a.</span></span> <span data-ttu-id="9170f-185">İçinde **Docker kapsayıcısı adı** kutusuna, Docker kapsayıcısı için benzersiz bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="9170f-185">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="9170f-186">b.</span><span class="sxs-lookup"><span data-stu-id="9170f-186">b.</span></span> <span data-ttu-id="9170f-187">Aşağıdaki Docker görüntülerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="9170f-187">Choose one of the following Docker images:</span></span> 

      * <span data-ttu-id="9170f-188">**Önceden tanımlanmış Docker görüntü**: azure'dan önceden var olan bir Docker görüntüsü belirtin.</span><span class="sxs-lookup"><span data-stu-id="9170f-188">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="9170f-189">Bu kutu Docker görüntülerinde listesi, Azure Araç Seti için yapılandırılmış birden fazla görüntülerinin oluşur, yapı otomatik olarak dağıtılır böylece düzeltme eki.</span><span class="sxs-lookup"><span data-stu-id="9170f-189">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="9170f-190">**Özel Dockerfile**: yerel bilgisayarınızdan önceden kaydedilmiş bir Dockerfile belirtin.</span><span class="sxs-lookup"><span data-stu-id="9170f-190">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="9170f-191">Bu, kendi Dockerfile dağıtmak isteyen geliştiriciler için daha gelişmiş bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="9170f-191">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="9170f-192">Ancak, kendi Dockerfile doğru bir şekilde yapıldığından emin olmak için bu seçeneği kullanın geliştiriciler kadar olur.</span><span class="sxs-lookup"><span data-stu-id="9170f-192">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="9170f-193">Azure Araç Seti özel bir Dockerfile içeriği doğrulamaz çünkü Dockerfile sorunları varsa dağıtım başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="9170f-193">Because the Azure Toolkit does not validate the content in a custom Dockerfile, the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="9170f-194">Ayrıca, Azure Araç Seti web uygulama yapı içerecek şekilde özel Dockerfile beklediği bir HTTP bağlantısı açmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="9170f-194">In addition, because the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, it attempts to open an HTTP connection.</span></span> <span data-ttu-id="9170f-195">Geliştiriciler farklı türde bir yapı yayımlarsanız, bunlar dağıtım sonrası zararsız hatalar alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9170f-195">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="9170f-196">c.</span><span class="sxs-lookup"><span data-stu-id="9170f-196">c.</span></span> <span data-ttu-id="9170f-197">İçinde **bağlantı noktası ayarları** kutusuna, Docker kapsayıcısı için benzersiz TCP bağlantı noktası bağlama girin.</span><span class="sxs-lookup"><span data-stu-id="9170f-197">In the **Port settings** box, enter the unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="9170f-198">Yukarıdaki adımları tamamladıktan sonra tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="9170f-198">After you have completed the preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="9170f-199">Azure Araç Seti Azure Docker kapsayıcısı içinde web uygulamanızı dağıtmaya başlar.</span><span class="sxs-lookup"><span data-stu-id="9170f-199">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> <span data-ttu-id="9170f-200">Arka planda dağıtılacak Intellij yapılandırmadığınız sürece bir **Azure'a dağıtan** ilerleme çubuğu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9170f-200">Unless you have configured IntelliJ to be deployed in the background, a **Deploying to Azure** progress bar appears.</span></span> 

![Dağıtım ilerleme çubuğu][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="9170f-202">Yapıları oluşturma hakkında ek bilgi</span><span class="sxs-lookup"><span data-stu-id="9170f-202">Additional information about creating artifacts</span></span>

<span data-ttu-id="9170f-203">Bir dağıtım için hazır yapı oluşturmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="9170f-203">To create a deployment-ready artifact, do the following:</span></span>

1. <span data-ttu-id="9170f-204">Web uygulaması projenizin Intellij içinde açın.</span><span class="sxs-lookup"><span data-stu-id="9170f-204">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="9170f-205">Tıklatın **dosya**ve ardından **proje yapısını**.</span><span class="sxs-lookup"><span data-stu-id="9170f-205">Click **File**, and then click **Project Structure**.</span></span>

   ![Proje yapısı komutu][ART01]

3. <span data-ttu-id="9170f-207">Bir yapı eklemek için yeşil artı işaretini tıklatın (**+**) ve ardından **Web uygulaması: Arşiv**.</span><span class="sxs-lookup"><span data-stu-id="9170f-207">To add an artifact, click the green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   !["Web uygulaması: arşivi" komutu][ART02]

4. <span data-ttu-id="9170f-209">İçinde **adı** kutusuna, yapı için bir ad girin (içermeyen *.war* uzantısı) ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="9170f-209">In the **Name** box, enter a name for your artifact (do not include the *.war* extension), and then click **OK**.</span></span>

   ![Yapı adı kutusu][ART03]

<span data-ttu-id="9170f-211">Intellij yapıları oluşturma hakkında daha fazla bilgi için bkz: [yapıları yapılandırma] JetBrains Web sitesinde.</span><span class="sxs-lookup"><span data-stu-id="9170f-211">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on the JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9170f-212">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9170f-212">Next steps</span></span>
<span data-ttu-id="9170f-213">Java IDE Azure araç takımları hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="9170f-213">For more information about the Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="9170f-214">[Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="9170f-214">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9170f-215">[Eclipse için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="9170f-215">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9170f-216">[Eclipse için Azure Araç Setini Yükleme]</span><span class="sxs-lookup"><span data-stu-id="9170f-216">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9170f-217">[Eclipse için Azure Araç Seti için oturum açma yönergeleri]</span><span class="sxs-lookup"><span data-stu-id="9170f-217">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9170f-218">[Eclipse'te Azure Hello World web uygulaması oluşturma]</span><span class="sxs-lookup"><span data-stu-id="9170f-218">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="9170f-219">[IntelliJ için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="9170f-219">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9170f-220">[Intellij için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="9170f-220">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9170f-221">[IntelliJ için Azure Araç Setini Yükleme]</span><span class="sxs-lookup"><span data-stu-id="9170f-221">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9170f-222">[Oturum açma Azure Araç Seti için Intellij için yönergeler]</span><span class="sxs-lookup"><span data-stu-id="9170f-222">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9170f-223">[Intellij Azure'da Hello World web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="9170f-223">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="9170f-224">Azure’u Java ile kullanma hakkında daha fazla bilgi edinmek için bkz. [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="9170f-224">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="9170f-225">Resmi Docker için ek kaynaklar için bkz: [Docker Web sitesi].</span><span class="sxs-lookup"><span data-stu-id="9170f-225">For additional resources for Docker, see the official [Docker website].</span></span>

<!-- URL List -->

<span data-ttu-id="9170f-226">[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="9170f-226">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="9170f-227">[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="9170f-227">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="9170f-228">[Eclipse'te Azure Hello World web uygulaması oluşturma]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="9170f-228">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="9170f-229">[Intellij Azure'da Hello World web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="9170f-229">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="9170f-230">[Eclipse için Azure Araç Setini Yükleme]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="9170f-230">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="9170f-231">[IntelliJ için Azure Araç Setini Yükleme]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="9170f-231">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="9170f-232">[Eclipse için Azure Araç Seti için oturum açma yönergeleri]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="9170f-232">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="9170f-233">[Oturum açma Azure Araç Seti için Intellij için yönergeler]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="9170f-233">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="9170f-234">[Eclipse için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="9170f-234">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="9170f-235">[Intellij için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="9170f-235">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="9170f-236">[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="9170f-236">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="9170f-237">[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="9170f-237">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="9170f-238">[Docker Web sitesi]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="9170f-238">[Docker website]: https://www.docker.com/</span></span>
<span data-ttu-id="9170f-239">[yapıları yapılandırma]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html</span><span class="sxs-lookup"><span data-stu-id="9170f-239">[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html</span></span>

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
