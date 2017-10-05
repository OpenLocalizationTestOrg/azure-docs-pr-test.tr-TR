---
title: "Eclipse için Azure araç setini kullanarak bir Docker kapsayıcısı yayımlama | Microsoft Docs"
description: "Eclipse için Azure araç setini kullanarak bir web uygulaması için Microsoft Azure Docker kapsayıcısı yayımlamak öğrenin."
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
ms.openlocfilehash: 746bb0a073396b84fa8592adda6748a2a5692ee8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="9dd54-103">Eclipse için Azure araç setini kullanarak bir web uygulaması Docker kapsayıcısı Yayımla</span><span class="sxs-lookup"><span data-stu-id="9dd54-103">Publish a web app as a Docker container by using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="9dd54-104">Docker, web uygulamalarını dağıtmak için yaygın olarak kullanılan bir yöntem kapsayıcılardır.</span><span class="sxs-lookup"><span data-stu-id="9dd54-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="9dd54-105">Docker kapsayıcıları kullanarak, geliştiricilerin kendi tüm proje dosyalarını ve tek bir paket için bir sunucu dağıtımı için bağımlılıkları birleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="9dd54-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="9dd54-106">Eclipse için Azure araç seti, ekleyerek Java geliştiriciler için bu işlemi basitleştirir *Docker kapsayıcısı olarak Yayımla* Microsoft Azure dağıtım özellikleri.</span><span class="sxs-lookup"><span data-stu-id="9dd54-106">The Azure Toolkit for Eclipse simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="9dd54-107">Bu makalede, Azure, uygulamalarınızı Docker kapsayıcı olarak yayımlamak için gereken adımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9dd54-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
> <span data-ttu-id="9dd54-108">Docker hakkında daha fazla bilgi edinilebilir [Docker Web sitesi].</span><span class="sxs-lookup"><span data-stu-id="9dd54-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="9dd54-109">Docker kapsayıcısı kullanarak Azure için web uygulamanızı yayınlama</span><span class="sxs-lookup"><span data-stu-id="9dd54-109">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="9dd54-110">Web uygulaması projenizin Eclipse'te açın.</span><span class="sxs-lookup"><span data-stu-id="9dd54-110">Open your web app project in Eclipse.</span></span>

2. <span data-ttu-id="9dd54-111">Başlatmak için **Docker kapsayıcısı olarak Yayımla** Sihirbazı, aşağıdakilerden birini yapın:</span><span class="sxs-lookup"><span data-stu-id="9dd54-111">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="9dd54-112">İçinde **Gezgini** görüntülemek, projenize sağ tıklayın, **Azure**ve ardından **Docker kapsayıcısı olarak Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="9dd54-112">In the **Navigator** view, right-click your project, click **Azure**, and then click **Publish as Docker Container**.</span></span>

      ![Gezgin Görünümü Docker kapsayıcısı komut olarak Yayımla][PUB01]

   * <span data-ttu-id="9dd54-114">Eclipse araç çubuğunda tıklatın **Yayımla** düğmesine tıklayın ve ardından **Docker kapsayıcısı olarak Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="9dd54-114">On the Eclipse toolbar, click the **Publish** button, and then click **Publish as Docker Container**.</span></span>

      ![Eclipse araç Docker kapsayıcısı komut olarak Yayımla][PUB02]
      
    <span data-ttu-id="9dd54-116">**Azure'da dağıtmak Docker kapsayıcısı** Sihirbazı açılır.</span><span class="sxs-lookup"><span data-stu-id="9dd54-116">The **Deploy Docker Container on Azure** wizard opens.</span></span>

    ![Azure Sihirbazı dağıtmak Docker kapsayıcısı][PUB03]

3. <span data-ttu-id="9dd54-118">İçinde **bir görüntü adı yazın, yapı'nın yolu seçin ve kullanılacak bir Docker ana denetleyin** penceresinde aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="9dd54-118">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span>

    <span data-ttu-id="9dd54-119">a.</span><span class="sxs-lookup"><span data-stu-id="9dd54-119">a.</span></span> <span data-ttu-id="9dd54-120">İçinde **Docker görüntü adı** kutusuna, Docker ana bilgisayar için benzersiz bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="9dd54-120">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="9dd54-121">(Sihirbaz otomatik olarak bir ad oluşturur, ancak bunu değiştirebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="9dd54-121">(The wizard automatically creates a name, but you can modify it.)</span></span>

    <span data-ttu-id="9dd54-122">b.</span><span class="sxs-lookup"><span data-stu-id="9dd54-122">b.</span></span> <span data-ttu-id="9dd54-123">**Ana** alanı önceden oluşturmuş olduğunuz tüm Docker ana bilgisayarlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9dd54-123">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="9dd54-124">Aşağıdakilerden birini yapın:</span><span class="sxs-lookup"><span data-stu-id="9dd54-124">Do either of the following:</span></span>

    * <span data-ttu-id="9dd54-125">Varolan bir Docker ana bilgisayara varsa, web uygulamanızı dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9dd54-125">If you have an existing Docker host, you can deploy your web app to it.</span></span>
    * <span data-ttu-id="9dd54-126">Yeni bir Docker ana bilgisayar oluşturmak için tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="9dd54-126">To create a new Docker host, click **Add**.</span></span>  
      
    <span data-ttu-id="9dd54-127">**Oluşturma Docker ana** iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="9dd54-127">The **Create Docker Host** dialog box opens.</span></span>

    ![Docker kapsayıcısı üzerinde Azure Sihirbazı'nı dağıtma][PUB04a]

4. <span data-ttu-id="9dd54-129">İçinde **yeni sanal makine yapılandırma** penceresinde, Docker ana bilgisayarınız için aşağıdaki seçenekleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="9dd54-129">In the **Configure the new virtual machine** window, specify the following options for your Docker host.</span></span> <span data-ttu-id="9dd54-130">(Sihirbaz için seçenekler çoğunu otomatik olarak oluşturur, ancak herhangi birini değiştirebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="9dd54-130">(The wizard automatically generates most of the options for you, but you can modify any of them.)</span></span>

   <span data-ttu-id="9dd54-131">a.</span><span class="sxs-lookup"><span data-stu-id="9dd54-131">a.</span></span> <span data-ttu-id="9dd54-132">**Ad**: Docker ana bilgisayar için benzersiz bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="9dd54-132">**Name**: Enter a unique name for the Docker host.</span></span> <span data-ttu-id="9dd54-133">(Bu, daha önce belirttiğiniz Docker görüntü adı ile aynı değildir.)</span><span class="sxs-lookup"><span data-stu-id="9dd54-133">(It is not the same as the Docker image name that you specified earlier.)</span></span>

   <span data-ttu-id="9dd54-134">b.</span><span class="sxs-lookup"><span data-stu-id="9dd54-134">b.</span></span> <span data-ttu-id="9dd54-135">**Abonelik**: ana bilgisayarınız için kullandığınız Azure aboneliğini girin.</span><span class="sxs-lookup"><span data-stu-id="9dd54-135">**Subscription**: Enter the Azure subscription that you use for your host.</span></span>

   <span data-ttu-id="9dd54-136">c.</span><span class="sxs-lookup"><span data-stu-id="9dd54-136">c.</span></span> <span data-ttu-id="9dd54-137">**Bölge**: ana bilgisayarınız bulunduğu coğrafi bölge girin.</span><span class="sxs-lookup"><span data-stu-id="9dd54-137">**Region**: Enter the geographical region where your host is located.</span></span>

   <span data-ttu-id="9dd54-138">d.</span><span class="sxs-lookup"><span data-stu-id="9dd54-138">d.</span></span> <span data-ttu-id="9dd54-139">Üzerinde **ana bilgisayar işletim sistemi ve boyutu** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="9dd54-139">On the **Host OS and Size** tab:</span></span>
     * <span data-ttu-id="9dd54-140">**Ana bilgisayar işletim sistemi**: ana bilgisayarınız içeren sanal makine için işletim sistemi girin.</span><span class="sxs-lookup"><span data-stu-id="9dd54-140">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span>
     * <span data-ttu-id="9dd54-141">**Boyutu**: ana bilgisayarınız için sanal makine boyutu girin.</span><span class="sxs-lookup"><span data-stu-id="9dd54-141">**Size**: Enter the virtual-machine size for your host.</span></span>

   <span data-ttu-id="9dd54-142">e.</span><span class="sxs-lookup"><span data-stu-id="9dd54-142">e.</span></span> <span data-ttu-id="9dd54-143">Üzerinde **kaynak grubu** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="9dd54-143">On the **Resource Group** tab:</span></span>
     * <span data-ttu-id="9dd54-144">**Yeni kaynak grubu**: ana bilgisayarınız için yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9dd54-144">**New resource group**: Create a new resource group for your host.</span></span>
     * <span data-ttu-id="9dd54-145">**Varolan bir kaynak grubu**: Azure hesabınızdan varolan bir kaynak grubu girin.</span><span class="sxs-lookup"><span data-stu-id="9dd54-145">**Existing resource group**: Enter an existing resource group from your Azure account.</span></span>

   <span data-ttu-id="9dd54-146">f.</span><span class="sxs-lookup"><span data-stu-id="9dd54-146">f.</span></span> <span data-ttu-id="9dd54-147">Üzerinde **ağ** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="9dd54-147">On the **Network** tab:</span></span>
     * <span data-ttu-id="9dd54-148">**Yeni sanal ağ**: ana bilgisayarınız için yeni bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9dd54-148">**New virtual network**: Create a new virtual network for your host.</span></span>
     * <span data-ttu-id="9dd54-149">**Varolan bir sanal ağı**: varolan bir sanal ağı Azure hesabınızı girin.</span><span class="sxs-lookup"><span data-stu-id="9dd54-149">**Existing virtual network**: Enter an existing virtual network from your Azure account.</span></span>

   <span data-ttu-id="9dd54-150">g.</span><span class="sxs-lookup"><span data-stu-id="9dd54-150">g.</span></span> <span data-ttu-id="9dd54-151">Üzerinde **depolama** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="9dd54-151">On the **Storage** tab:</span></span>
     * <span data-ttu-id="9dd54-152">**Yeni depolama hesabı**: ana bilgisayarınız için yeni bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9dd54-152">**New storage account**: Create a new storage account for your host.</span></span>
     * <span data-ttu-id="9dd54-153">**Varolan bir depolama hesabı**: Azure hesabınızdan mevcut bir depolama hesabını girin.</span><span class="sxs-lookup"><span data-stu-id="9dd54-153">**Existing storage account**: Enter an existing storage account from your Azure account.</span></span>

5. <span data-ttu-id="9dd54-154">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9dd54-154">Click **Next**.</span></span>

6. <span data-ttu-id="9dd54-155">İçinde **günlük kimlik bilgilerini yapılandırın ve bağlantı noktası ayarları** penceresinde, aşağıdaki seçeneklerden birini belirleyin:</span><span class="sxs-lookup"><span data-stu-id="9dd54-155">In the **Configure log in credentials and port settings** window, select one of the following options:</span></span>

    * <span data-ttu-id="9dd54-156">**Azure anahtar Kasası'kimlik bilgileri içe**: önceden kaydedilen bir Azure aboneliğinizde depolanan kimlik bilgileri kümesi belirtir.</span><span class="sxs-lookup"><span data-stu-id="9dd54-156">**Import credentials from Azure Key Vault**: Specifies a previously saved set of credentials that are stored in your Azure subscription.</span></span>

      >[!NOTE]
      ><span data-ttu-id="9dd54-157">Bir hesabın veya hizmet sorumlusu ile oluşturulan bir Azure anahtar kasası başka bir hesap veya abonelik paylaşan hizmet sorumlusu tarafından otomatik olarak erişilebilir değil.</span><span class="sxs-lookup"><span data-stu-id="9dd54-157">An Azure Key Vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="9dd54-158">Başka bir hesap veya hizmet asıl anahtar kasası kullanmaya izin vermek için hesabı veya hizmet sorumlusu eklemek için Azure Portalı'nı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9dd54-158">To allow another account or service principal to use the Key Vault, you must use the Azure portal to add the account or service principal.</span></span>

    * <span data-ttu-id="9dd54-159">**Yeni oturum açma kimlik bilgileri**: yeni bir oturum açma kimlik bilgileri kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9dd54-159">**New log in credentials**: Creates a new set of login credentials.</span></span> <span data-ttu-id="9dd54-160">Bu seçeneği seçerseniz, aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="9dd54-160">If you select this option, do the following:</span></span>
    
      * <span data-ttu-id="9dd54-161">Üzerinde **VM kimlik** sekmesinde, aşağıdaki seçenekler, Docker ana bilgisayar sanal makinesi oturum açma kimlik bilgilerini seçin:</span><span class="sxs-lookup"><span data-stu-id="9dd54-161">On the **VM Credentials** tab, choose one of the following options for the virtual-machine login credentials of your Docker host:</span></span>

          * <span data-ttu-id="9dd54-162">**Kullanıcı adı**: kullanıcı için sanal makine oturum açma kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="9dd54-162">**Username**: Enter the username for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="9dd54-163">**Parola** ve **Onayla**: parola için sanal makine oturum açma kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="9dd54-163">**Password** and **Confirm**: Enter the password for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="9dd54-164">**SSH**: Docker ana bilgisayarınız Güvenli Kabuk (SSH) ayarlarını girin.</span><span class="sxs-lookup"><span data-stu-id="9dd54-164">**SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="9dd54-165">Aşağıdaki seçenekler arasından seçim yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9dd54-165">You can choose from the following options:</span></span>
            * <span data-ttu-id="9dd54-166">**Hiçbiri**: sanal makineniz SSH bağlantılara izin vermez belirtir.</span><span class="sxs-lookup"><span data-stu-id="9dd54-166">**None**: Specifies that your virtual machine will not allow SSH connections.</span></span>
            * <span data-ttu-id="9dd54-167">**Otomatik oluşturma**: SSH yoluyla bağlanmak için gerekli ayarları otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9dd54-167">**Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span>
            * <span data-ttu-id="9dd54-168">**Dizine alma**: önceden kaydedilmiş SSH ayarları kümesini içeren bir dizini belirtir.</span><span class="sxs-lookup"><span data-stu-id="9dd54-168">**Import from directory**: Specifies a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="9dd54-169">Dizin, aşağıdaki iki dosyada içermelidir:</span><span class="sxs-lookup"><span data-stu-id="9dd54-169">The directory must contain the following two files:</span></span>
                * <span data-ttu-id="9dd54-170">*id_rsa*: bir kullanıcı için RSA kimliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="9dd54-170">*id_rsa*: Contains the RSA identification for a user.</span></span>
                * <span data-ttu-id="9dd54-171">*id_rsa.pub*: kimlik doğrulaması için kullanılan RSA ortak anahtarı içerir.</span><span class="sxs-lookup"><span data-stu-id="9dd54-171">*id_rsa.pub*: Contains the RSA public key that is used for authentication.</span></span>
        
        ![Docker konak oluştur][PUB05]

      * <span data-ttu-id="9dd54-173">Üzerinde **Docker arka plan programı kimlik** sekmesinde, aşağıdaki seçenekleri belirtin:</span><span class="sxs-lookup"><span data-stu-id="9dd54-173">On the **Docker Daemon Credentials** tab, specify the following options:</span></span>

          * <span data-ttu-id="9dd54-174">**Docker arka plan programı bağlantı noktası**: Docker ana bilgisayarınız için benzersiz TCP bağlantı noktasını girin.</span><span class="sxs-lookup"><span data-stu-id="9dd54-174">**Docker Daemon port**: Enter the unique TCP port for your Docker host.</span></span>
          * <span data-ttu-id="9dd54-175">**TLS güvenlik**: Docker ana bilgisayarınız için Aktarım Katmanı Güvenliği ayarlarını girin.</span><span class="sxs-lookup"><span data-stu-id="9dd54-175">**TLS Security**: Enter the Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="9dd54-176">Aşağıdaki seçenekler arasından seçim yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9dd54-176">You can choose from the following options:</span></span>
            * <span data-ttu-id="9dd54-177">**Hiçbiri**: sanal makineniz TLS bağlantılara izin vermez belirtir.</span><span class="sxs-lookup"><span data-stu-id="9dd54-177">**None**: Specifies that your virtual machine will not allow TLS connections.</span></span>
            * <span data-ttu-id="9dd54-178">**Otomatik oluşturma**: TLS bağlanmak için gerekli ayarları otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9dd54-178">**Auto-generate**: Automatically creates the requisite settings for connecting via TLS.</span></span>
            * <span data-ttu-id="9dd54-179">**Dizine alma**: önceden kaydedilmiş TLS ayarları kümesini içeren bir dizini belirtir.</span><span class="sxs-lookup"><span data-stu-id="9dd54-179">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="9dd54-180">Daha açık belirtmek gerekirse dizin aşağıdaki altı dosyaları içermelidir:</span><span class="sxs-lookup"><span data-stu-id="9dd54-180">More specifically, the directory must contain the following six files:</span></span>
                * <span data-ttu-id="9dd54-181">*CA.pem* ve *ca key.pem*: TLS sertifika yetkilisi sertifika ve ortak anahtarı içerir.</span><span class="sxs-lookup"><span data-stu-id="9dd54-181">*ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.</span></span>
                * <span data-ttu-id="9dd54-182">*CERT.pem* ve *key.pem*: istemci sertifikası ve TLS kimlik doğrulaması için kullanılan ortak anahtar içerir.</span><span class="sxs-lookup"><span data-stu-id="9dd54-182">*cert.pem* and *key.pem*: Contain the client certificate and public key that is used for TLS authentication.</span></span>
                * <span data-ttu-id="9dd54-183">*Server.pem* ve *server key.pem*: ana bilgisayar için sunucu sertifikası ve ortak anahtar içerir.</span><span class="sxs-lookup"><span data-stu-id="9dd54-183">*server.pem* and *server-key.pem*: Contain the server certificate and public key for the host.</span></span>

        ![Docker konak oluştur][PUB06]

7. <span data-ttu-id="9dd54-185">Yukarıdaki bilgilerin tümünü girdikten sonra tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="9dd54-185">After you have entered all of the preceding information, click **Finish**.</span></span>

8. <span data-ttu-id="9dd54-186">İçinde **dağıtmak Docker kapsayıcısı Azure üzerinde** Sihirbazı'nı tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="9dd54-186">In the **Deploy Docker Container on Azure** wizard, click **Next**.</span></span>

   ![Azure Sihirbazı dağıtmak Docker kapsayıcısı][PUB07]

9. <span data-ttu-id="9dd54-188">İçinde **oluşturulacak Docker kapsayıcısı yapılandırma** penceresinde aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="9dd54-188">In the **Configure the Docker container to be created** window, do the following:</span></span>

   <span data-ttu-id="9dd54-189">a.</span><span class="sxs-lookup"><span data-stu-id="9dd54-189">a.</span></span> <span data-ttu-id="9dd54-190">İçinde **Docker kapsayıcısı adı** kutusuna, Docker kapsayıcısı için benzersiz bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="9dd54-190">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="9dd54-191">b.</span><span class="sxs-lookup"><span data-stu-id="9dd54-191">b.</span></span> <span data-ttu-id="9dd54-192">Aşağıdaki Docker görüntülerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="9dd54-192">Choose one of the following Docker images:</span></span>
     * <span data-ttu-id="9dd54-193">**Önceden tanımlanmış Docker görüntü**: Azure önceden var olan bir Docker görüntüsünden belirtir.</span><span class="sxs-lookup"><span data-stu-id="9dd54-193">**Predefined Docker image**: Specifies a pre-existing Docker image from Azure.</span></span>

       >[!NOTE]
       ><span data-ttu-id="9dd54-194">Bu kutu Docker görüntülerinde listesi, Azure Araç Seti için yapılandırılmış birden fazla görüntülerinin oluşur, yapı otomatik olarak dağıtılır böylece düzeltme eki.</span><span class="sxs-lookup"><span data-stu-id="9dd54-194">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span>

     * <span data-ttu-id="9dd54-195">**Özel Dockerfile**: yerel bilgisayarınızdan önceden kaydedilmiş bir Dockerfile belirtir.</span><span class="sxs-lookup"><span data-stu-id="9dd54-195">**Custom Dockerfile**: Specifies a previously saved Dockerfile from your local computer.</span></span>

       >[!NOTE]
       ><span data-ttu-id="9dd54-196">Bu, kendi Dockerfile dağıtmak isteyen geliştiriciler için daha gelişmiş bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="9dd54-196">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="9dd54-197">Ancak, kendi Dockerfile doğru bir şekilde yapıldığından emin olmak için bu seçeneği kullanın geliştiriciler kadar olur.</span><span class="sxs-lookup"><span data-stu-id="9dd54-197">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="9dd54-198">Dockerfile sorunları varsa dağıtım başarısız olabilir şekilde Azure Araç Seti özel bir Dockerfile içeriği doğrulamaz.</span><span class="sxs-lookup"><span data-stu-id="9dd54-198">The Azure Toolkit does not validate the content in a custom Dockerfile, so the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="9dd54-199">Ayrıca, bir web uygulaması yapı içerecek şekilde özel Dockerfile Azure Araç Seti bekliyor ve bir HTTP bağlantısı açmayı dener.</span><span class="sxs-lookup"><span data-stu-id="9dd54-199">In addition, the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, and it will attempt to open an HTTP connection.</span></span> <span data-ttu-id="9dd54-200">Geliştiriciler farklı türde bir yapı yayımlarsanız, bunlar dağıtım sonrası zararsız hatalar alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9dd54-200">If developers publish a different type of artifact, they may receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="9dd54-201">c.</span><span class="sxs-lookup"><span data-stu-id="9dd54-201">c.</span></span> <span data-ttu-id="9dd54-202">**Bağlantı noktası ayarları**: Docker kapsayıcısı için benzersiz TCP bağlantı noktası bağlama girin.</span><span class="sxs-lookup"><span data-stu-id="9dd54-202">**Port settings**: Enter the unique TCP port binding for your Docker container.</span></span>

     ![Pencere oluşturulması için Docker kapsayıcısı Yapılandır][PUB08]

10. <span data-ttu-id="9dd54-204">Önceki tüm adımları tamamladıktan sonra tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="9dd54-204">After you have completed all of the preceding steps, click **Finish**.</span></span>

<span data-ttu-id="9dd54-205">Azure Araç Seti Azure Docker kapsayıcısı içinde web uygulamanızı dağıtmaya başlar.</span><span class="sxs-lookup"><span data-stu-id="9dd54-205">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9dd54-206">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9dd54-206">Next steps</span></span>
<span data-ttu-id="9dd54-207">Java IDE Azure araç takımları hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="9dd54-207">For more information about the Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="9dd54-208">[Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="9dd54-208">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9dd54-209">[Eclipse için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="9dd54-209">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9dd54-210">[Eclipse için Azure Araç Setini Yükleme]</span><span class="sxs-lookup"><span data-stu-id="9dd54-210">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9dd54-211">[Eclipse için Azure Araç Seti için oturum açma yönergeleri]</span><span class="sxs-lookup"><span data-stu-id="9dd54-211">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9dd54-212">[Eclipse'te Azure Hello World web uygulaması oluşturma]</span><span class="sxs-lookup"><span data-stu-id="9dd54-212">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="9dd54-213">[IntelliJ için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="9dd54-213">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9dd54-214">[Intellij için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="9dd54-214">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9dd54-215">[IntelliJ için Azure Araç Setini Yükleme]</span><span class="sxs-lookup"><span data-stu-id="9dd54-215">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9dd54-216">[Oturum açma Azure Araç Seti için Intellij için yönergeler]</span><span class="sxs-lookup"><span data-stu-id="9dd54-216">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9dd54-217">[Intellij Azure'da Hello World web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="9dd54-217">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="9dd54-218">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="9dd54-218">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="9dd54-219">Resmi Docker için ek kaynaklar için bkz: [Docker Web sitesi].</span><span class="sxs-lookup"><span data-stu-id="9dd54-219">For additional resources for Docker, see the official [Docker website].</span></span>

<!-- URL List -->

<span data-ttu-id="9dd54-220">[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="9dd54-220">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="9dd54-221">[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="9dd54-221">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="9dd54-222">[Eclipse'te Azure Hello World web uygulaması oluşturma]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="9dd54-222">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="9dd54-223">[Intellij Azure'da Hello World web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="9dd54-223">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="9dd54-224">[Eclipse için Azure Araç Setini Yükleme]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="9dd54-224">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="9dd54-225">[IntelliJ için Azure Araç Setini Yükleme]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="9dd54-225">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="9dd54-226">[Eclipse için Azure Araç Seti için oturum açma yönergeleri]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="9dd54-226">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="9dd54-227">[Oturum açma Azure Araç Seti için Intellij için yönergeler]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="9dd54-227">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="9dd54-228">[Eclipse için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="9dd54-228">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="9dd54-229">[Intellij için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="9dd54-229">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="9dd54-230">[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="9dd54-230">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="9dd54-231">[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="9dd54-231">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="9dd54-232">[Docker Web sitesi]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="9dd54-232">[Docker website]: https://www.docker.com/</span></span>

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png