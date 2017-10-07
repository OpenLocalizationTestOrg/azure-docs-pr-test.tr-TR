---
title: "aaaPublish kullanarak bir Docker kapsayıcısı hello Eclipse için Azure Araç Seti | Microsoft Docs"
description: "Bilgi nasıl toopublish bir web uygulaması tooMicrosoft kullanarak bir Docker kapsayıcısı olarak Azure hello Eclipse için Azure Araç Seti."
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
ms.openlocfilehash: 53ec3a7f7a171691024e03622fd48d6f1e257b50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="0cbd2-103">Eclipse için hello Azure Araç Seti kullanarak bir web uygulaması Docker kapsayıcısı Yayımla</span><span class="sxs-lookup"><span data-stu-id="0cbd2-103">Publish a web app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="0cbd2-104">Docker, web uygulamalarını dağıtmak için yaygın olarak kullanılan bir yöntem kapsayıcılardır.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="0cbd2-105">Docker kapsayıcıları kullanarak, geliştiricilerin kendi tüm proje dosyalarını ve dağıtım tooa sunucusu için tek bir paket bağımlılıkları birleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="0cbd2-106">Merhaba Eclipse için Azure Araç Seti basitleştirir bu işlem için Java geliştiricilerinin ekleyerek *Docker kapsayıcısı olarak Yayımla* dağıtım tooMicrosoft Azure özellikleri.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-106">hello Azure Toolkit for Eclipse simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="0cbd2-107">Bu makalede hello adımları gerekli toopublish Docker kapsayıcılar olarak uygulamaları tooAzure anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
> <span data-ttu-id="0cbd2-108">Docker hakkında daha fazla bilgi hello üzerinde kullanılabilir [Docker Web sitesi].</span><span class="sxs-lookup"><span data-stu-id="0cbd2-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="0cbd2-109">Web uygulaması tooAzure Docker kapsayıcısı kullanarak yayımlama</span><span class="sxs-lookup"><span data-stu-id="0cbd2-109">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="0cbd2-110">Web uygulaması projenizin Eclipse'te açın.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-110">Open your web app project in Eclipse.</span></span>

2. <span data-ttu-id="0cbd2-111">toostart hello **Docker kapsayıcısı olarak Yayımla** Sihirbazı'nı hello aşağıdakilerden birini yapın:</span><span class="sxs-lookup"><span data-stu-id="0cbd2-111">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="0cbd2-112">Merhaba, **Gezgini** görüntülemek, projenize sağ tıklayın, **Azure**ve ardından **Docker kapsayıcısı olarak Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-112">In hello **Navigator** view, right-click your project, click **Azure**, and then click **Publish as Docker Container**.</span></span>

      ![Gezgin Görünümü Docker kapsayıcısı komut olarak Yayımla][PUB01]

   * <span data-ttu-id="0cbd2-114">Merhaba Hello Eclipse araç çubuğunda tıklatın **Yayımla** düğmesine tıklayın ve ardından **Docker kapsayıcısı olarak Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-114">On hello Eclipse toolbar, click hello **Publish** button, and then click **Publish as Docker Container**.</span></span>

      ![Eclipse araç Docker kapsayıcısı komut olarak Yayımla][PUB02]
      
    <span data-ttu-id="0cbd2-116">Merhaba **azure'da dağıtmak Docker kapsayıcısı** Sihirbazı açılır.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-116">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

    ![Merhaba dağıtma Docker kapsayıcısı Azure Sihirbazı][PUB03]

3. <span data-ttu-id="0cbd2-118">Merhaba, **bir görüntü adı yazın, hello yapı'nın yolu seçin ve kullanılan Docker ana toobe denetleyin** penceresinde, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="0cbd2-118">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span>

    <span data-ttu-id="0cbd2-119">a.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-119">a.</span></span> <span data-ttu-id="0cbd2-120">Merhaba, **Docker görüntü adı** kutusuna, Docker ana bilgisayar için benzersiz bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-120">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="0cbd2-121">(Merhaba Sihirbazı otomatik olarak bir ad oluşturur, ancak bunu değiştirebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="0cbd2-121">(hello wizard automatically creates a name, but you can modify it.)</span></span>

    <span data-ttu-id="0cbd2-122">b.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-122">b.</span></span> <span data-ttu-id="0cbd2-123">Merhaba **ana** alanı önceden oluşturmuş olduğunuz tüm Docker ana bilgisayarlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-123">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="0cbd2-124">Merhaba aşağıdakilerden birini yapın:</span><span class="sxs-lookup"><span data-stu-id="0cbd2-124">Do either of hello following:</span></span>

    * <span data-ttu-id="0cbd2-125">Varolan bir Docker ana bilgisayara varsa, web uygulaması tooit dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-125">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
    * <span data-ttu-id="0cbd2-126">Yeni bir Docker ana bilgisayar toocreate tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-126">toocreate a new Docker host, click **Add**.</span></span>  
      
    <span data-ttu-id="0cbd2-127">Merhaba **oluşturma Docker ana** iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-127">hello **Create Docker Host** dialog box opens.</span></span>

    ![Docker kapsayıcısı üzerinde Azure Sihirbazı'nı dağıtma][PUB04a]

4. <span data-ttu-id="0cbd2-129">Merhaba, **hello yeni sanal makine yapılandırma** penceresinde, aşağıdaki seçenekleri, Docker ana bilgisayar için şu hello belirtin.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-129">In hello **Configure hello new virtual machine** window, specify hello following options for your Docker host.</span></span> <span data-ttu-id="0cbd2-130">(Merhaba seçenekler çoğunu hello Sihirbazı otomatik olarak oluşturur, ancak herhangi birini değiştirebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="0cbd2-130">(hello wizard automatically generates most of hello options for you, but you can modify any of them.)</span></span>

   <span data-ttu-id="0cbd2-131">a.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-131">a.</span></span> <span data-ttu-id="0cbd2-132">**Ad**: Merhaba Docker ana bilgisayar için benzersiz bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-132">**Name**: Enter a unique name for hello Docker host.</span></span> <span data-ttu-id="0cbd2-133">(Bu, hello almak için değil, daha önce belirtilen Docker görüntü adı hello aynı olur.)</span><span class="sxs-lookup"><span data-stu-id="0cbd2-133">(It is not hello same as hello Docker image name that you specified earlier.)</span></span>

   <span data-ttu-id="0cbd2-134">b.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-134">b.</span></span> <span data-ttu-id="0cbd2-135">**Abonelik**: hello ana bilgisayarınız için kullandığınız Azure aboneliğini girin.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-135">**Subscription**: Enter hello Azure subscription that you use for your host.</span></span>

   <span data-ttu-id="0cbd2-136">c.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-136">c.</span></span> <span data-ttu-id="0cbd2-137">**Bölge**: ana bilgisayarınız bulunduğu hello coğrafi girin.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-137">**Region**: Enter hello geographical region where your host is located.</span></span>

   <span data-ttu-id="0cbd2-138">d.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-138">d.</span></span> <span data-ttu-id="0cbd2-139">Merhaba üzerinde **ana bilgisayar işletim sistemi ve boyutu** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="0cbd2-139">On hello **Host OS and Size** tab:</span></span>
     * <span data-ttu-id="0cbd2-140">**Ana bilgisayar işletim sistemi**: hello işletim sistemi hello sanal makine için ana bilgisayarınız içeren girin.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-140">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span>
     * <span data-ttu-id="0cbd2-141">**Boyutu**: ana bilgisayarınız için hello sanal makine boyutu girin.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-141">**Size**: Enter hello virtual-machine size for your host.</span></span>

   <span data-ttu-id="0cbd2-142">e.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-142">e.</span></span> <span data-ttu-id="0cbd2-143">Merhaba üzerinde **kaynak grubu** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="0cbd2-143">On hello **Resource Group** tab:</span></span>
     * <span data-ttu-id="0cbd2-144">**Yeni kaynak grubu**: ana bilgisayarınız için yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-144">**New resource group**: Create a new resource group for your host.</span></span>
     * <span data-ttu-id="0cbd2-145">**Varolan bir kaynak grubu**: Azure hesabınızdan varolan bir kaynak grubu girin.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-145">**Existing resource group**: Enter an existing resource group from your Azure account.</span></span>

   <span data-ttu-id="0cbd2-146">f.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-146">f.</span></span> <span data-ttu-id="0cbd2-147">Merhaba üzerinde **ağ** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="0cbd2-147">On hello **Network** tab:</span></span>
     * <span data-ttu-id="0cbd2-148">**Yeni sanal ağ**: ana bilgisayarınız için yeni bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-148">**New virtual network**: Create a new virtual network for your host.</span></span>
     * <span data-ttu-id="0cbd2-149">**Varolan bir sanal ağı**: varolan bir sanal ağı Azure hesabınızı girin.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-149">**Existing virtual network**: Enter an existing virtual network from your Azure account.</span></span>

   <span data-ttu-id="0cbd2-150">g.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-150">g.</span></span> <span data-ttu-id="0cbd2-151">Merhaba üzerinde **depolama** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="0cbd2-151">On hello **Storage** tab:</span></span>
     * <span data-ttu-id="0cbd2-152">**Yeni depolama hesabı**: ana bilgisayarınız için yeni bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-152">**New storage account**: Create a new storage account for your host.</span></span>
     * <span data-ttu-id="0cbd2-153">**Varolan bir depolama hesabı**: Azure hesabınızdan mevcut bir depolama hesabını girin.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-153">**Existing storage account**: Enter an existing storage account from your Azure account.</span></span>

5. <span data-ttu-id="0cbd2-154">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-154">Click **Next**.</span></span>

6. <span data-ttu-id="0cbd2-155">Merhaba, **günlük kimlik bilgilerini yapılandırın ve bağlantı noktası ayarları** penceresinde, aşağıdaki seçenekleri şu hello birini seçin:</span><span class="sxs-lookup"><span data-stu-id="0cbd2-155">In hello **Configure log in credentials and port settings** window, select one of hello following options:</span></span>

    * <span data-ttu-id="0cbd2-156">**Azure anahtar Kasası'kimlik bilgileri içe**: önceden kaydedilen bir Azure aboneliğinizde depolanan kimlik bilgileri kümesi belirtir.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-156">**Import credentials from Azure Key Vault**: Specifies a previously saved set of credentials that are stored in your Azure subscription.</span></span>

      >[!NOTE]
      ><span data-ttu-id="0cbd2-157">Bir hesabın veya hizmet sorumlusu ile oluşturulan bir Azure anahtar kasası başka bir hesap veya hello abonelik paylaşan hizmet sorumlusu tarafından otomatik olarak erişilebilir değil.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-157">An Azure Key Vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="0cbd2-158">tooallow başka bir hesap veya hizmet asıl toouse anahtar kasası Merhaba, hello Azure portal tooadd hello hesabı ya da hizmet sorumlusu kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-158">tooallow another account or service principal toouse hello Key Vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

    * <span data-ttu-id="0cbd2-159">**Yeni oturum açma kimlik bilgileri**: yeni bir oturum açma kimlik bilgileri kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-159">**New log in credentials**: Creates a new set of login credentials.</span></span> <span data-ttu-id="0cbd2-160">Bu seçeneği seçerseniz, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="0cbd2-160">If you select this option, do hello following:</span></span>
    
      * <span data-ttu-id="0cbd2-161">Merhaba üzerinde **VM kimlik** sekmesinde, hello sanal makinesi oturum açma kimlik bilgileri, Docker ana bilgisayarın seçenekleri hello aşağıdakilerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="0cbd2-161">On hello **VM Credentials** tab, choose one of hello following options for hello virtual-machine login credentials of your Docker host:</span></span>

          * <span data-ttu-id="0cbd2-162">**Kullanıcı adı**: hello kullanıcı için sanal makine oturum açma kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-162">**Username**: Enter hello username for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="0cbd2-163">**Parola** ve **Onayla**: hello parola için sanal makine oturum açma kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-163">**Password** and **Confirm**: Enter hello password for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="0cbd2-164">**SSH**: Docker ana bilgisayarınız hello güvenli Kabuk (SSH) ayarlarını girin.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-164">**SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="0cbd2-165">Seçenekler aşağıdaki hello seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0cbd2-165">You can choose from hello following options:</span></span>
            * <span data-ttu-id="0cbd2-166">**Hiçbiri**: sanal makineniz SSH bağlantılara izin vermez belirtir.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-166">**None**: Specifies that your virtual machine will not allow SSH connections.</span></span>
            * <span data-ttu-id="0cbd2-167">**Otomatik oluşturma**: hello SSH yoluyla bağlanmak için gerekli ayarları otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-167">**Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
            * <span data-ttu-id="0cbd2-168">**Dizine alma**: önceden kaydedilmiş SSH ayarları kümesini içeren bir dizini belirtir.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-168">**Import from directory**: Specifies a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="0cbd2-169">Merhaba dizin, aşağıdaki iki dosyaları hello içermelidir:</span><span class="sxs-lookup"><span data-stu-id="0cbd2-169">hello directory must contain hello following two files:</span></span>
                * <span data-ttu-id="0cbd2-170">*id_rsa*: bir kullanıcı için hello RSA kimliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-170">*id_rsa*: Contains hello RSA identification for a user.</span></span>
                * <span data-ttu-id="0cbd2-171">*id_rsa.pub*: kimlik doğrulaması için kullanılan hello RSA ortak anahtarı içerir.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-171">*id_rsa.pub*: Contains hello RSA public key that is used for authentication.</span></span>
        
        ![Docker konak oluştur][PUB05]

      * <span data-ttu-id="0cbd2-173">Merhaba üzerinde **Docker arka plan programı kimlik** sekmesinde, aşağıdaki seçenekleri şu hello belirtin:</span><span class="sxs-lookup"><span data-stu-id="0cbd2-173">On hello **Docker Daemon Credentials** tab, specify hello following options:</span></span>

          * <span data-ttu-id="0cbd2-174">**Docker arka plan programı bağlantı noktası**: Docker ana bilgisayarınız için hello benzersiz TCP bağlantı noktası girin.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-174">**Docker Daemon port**: Enter hello unique TCP port for your Docker host.</span></span>
          * <span data-ttu-id="0cbd2-175">**TLS güvenlik**: Docker ana bilgisayarınız hello Aktarım Katmanı Güvenliği ayarlarını girin.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-175">**TLS Security**: Enter hello Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="0cbd2-176">Seçenekler aşağıdaki hello seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0cbd2-176">You can choose from hello following options:</span></span>
            * <span data-ttu-id="0cbd2-177">**Hiçbiri**: sanal makineniz TLS bağlantılara izin vermez belirtir.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-177">**None**: Specifies that your virtual machine will not allow TLS connections.</span></span>
            * <span data-ttu-id="0cbd2-178">**Otomatik oluşturma**: hello TLS bağlanmak için gerekli ayarları otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-178">**Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.</span></span>
            * <span data-ttu-id="0cbd2-179">**Dizine alma**: önceden kaydedilmiş TLS ayarları kümesini içeren bir dizini belirtir.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-179">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="0cbd2-180">Daha açık belirtmek gerekirse hello dizini aşağıdaki altı dosyaları hello içermelidir:</span><span class="sxs-lookup"><span data-stu-id="0cbd2-180">More specifically, hello directory must contain hello following six files:</span></span>
                * <span data-ttu-id="0cbd2-181">*CA.pem* ve *ca key.pem*: hello sertifika ve ortak anahtar hello TLS sertifika yetkilisi için içerir.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-181">*ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.</span></span>
                * <span data-ttu-id="0cbd2-182">*CERT.pem* ve *key.pem*: hello istemci sertifikası ve TLS kimlik doğrulaması için kullanılan ortak anahtar içerir.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-182">*cert.pem* and *key.pem*: Contain hello client certificate and public key that is used for TLS authentication.</span></span>
                * <span data-ttu-id="0cbd2-183">*Server.pem* ve *server key.pem*: hello sunucu sertifikası ve hello ana bilgisayarı için ortak anahtar içerir.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-183">*server.pem* and *server-key.pem*: Contain hello server certificate and public key for hello host.</span></span>

        ![Docker konak oluştur][PUB06]

7. <span data-ttu-id="0cbd2-185">Tüm önceki bilgilere hello girdikten sonra tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-185">After you have entered all of hello preceding information, click **Finish**.</span></span>

8. <span data-ttu-id="0cbd2-186">Merhaba, **dağıtmak Docker kapsayıcısı Azure üzerinde** Sihirbazı'nı tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-186">In hello **Deploy Docker Container on Azure** wizard, click **Next**.</span></span>

   ![Merhaba dağıtma Docker kapsayıcısı Azure Sihirbazı][PUB07]

9. <span data-ttu-id="0cbd2-188">Merhaba, **oluşturulan hello Docker kapsayıcısı toobe yapılandırma** penceresinde, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="0cbd2-188">In hello **Configure hello Docker container toobe created** window, do hello following:</span></span>

   <span data-ttu-id="0cbd2-189">a.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-189">a.</span></span> <span data-ttu-id="0cbd2-190">Merhaba, **Docker kapsayıcısı adı** kutusuna, Docker kapsayıcısı için benzersiz bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-190">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="0cbd2-191">b.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-191">b.</span></span> <span data-ttu-id="0cbd2-192">Docker görüntüleri aşağıdaki hello birini seçin:</span><span class="sxs-lookup"><span data-stu-id="0cbd2-192">Choose one of hello following Docker images:</span></span>
     * <span data-ttu-id="0cbd2-193">**Önceden tanımlanmış Docker görüntü**: Azure önceden var olan bir Docker görüntüsünden belirtir.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-193">**Predefined Docker image**: Specifies a pre-existing Docker image from Azure.</span></span>

       >[!NOTE]
       ><span data-ttu-id="0cbd2-194">Bu kutu Docker görüntülerinde Hello listesi, birkaç görüntülerini oluşur Azure Araç Seti açıldı, hello toopatch yapılandırılmış, yapı otomatik olarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-194">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span>

     * <span data-ttu-id="0cbd2-195">**Özel Dockerfile**: yerel bilgisayarınızdan önceden kaydedilmiş bir Dockerfile belirtir.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-195">**Custom Dockerfile**: Specifies a previously saved Dockerfile from your local computer.</span></span>

       >[!NOTE]
       ><span data-ttu-id="0cbd2-196">Bu, kendi Dockerfile toodeploy isteyen geliştiriciler için daha gelişmiş bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-196">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="0cbd2-197">Ancak, kendi Dockerfile doğru bir şekilde yapıldığından bu seçeneği tooensure kullanan toodevelopers değildir.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-197">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="0cbd2-198">Merhaba Dockerfile sorunları varsa hello dağıtım başarısız olabilir şekilde hello Azure Araç Seti özel bir Dockerfile hello içeriği doğrulamaz.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-198">hello Azure Toolkit does not validate hello content in a custom Dockerfile, so hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="0cbd2-199">Ayrıca, hello Azure Araç Seti hello özel Dockerfile toocontain bir web uygulaması yapı bekler ve tooopen bir HTTP bağlantısı deneyecek.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-199">In addition, hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, and it will attempt tooopen an HTTP connection.</span></span> <span data-ttu-id="0cbd2-200">Geliştiriciler farklı türde bir yapı yayımlarsanız, bunlar dağıtım sonrası zararsız hatalar alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-200">If developers publish a different type of artifact, they may receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="0cbd2-201">c.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-201">c.</span></span> <span data-ttu-id="0cbd2-202">**Bağlantı noktası ayarları**: hello benzersiz TCP bağlantı noktası için bağlama, Docker kapsayıcısı girin.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-202">**Port settings**: Enter hello unique TCP port binding for your Docker container.</span></span>

     ![Merhaba yapılandırma hello Docker kapsayıcısı oluşturulan toobe penceresi][PUB08]

10. <span data-ttu-id="0cbd2-204">Tüm adımları önceki hello tamamladıktan sonra tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-204">After you have completed all of hello preceding steps, click **Finish**.</span></span>

<span data-ttu-id="0cbd2-205">Hello Azure araç seti, web uygulama tooAzure Docker kapsayıcısı içinde dağıtmaya başlar.</span><span class="sxs-lookup"><span data-stu-id="0cbd2-205">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0cbd2-206">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0cbd2-206">Next steps</span></span>
<span data-ttu-id="0cbd2-207">Java IDE hello Azure araç takımları hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="0cbd2-207">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="0cbd2-208">[Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="0cbd2-208">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="0cbd2-209">[Merhaba Eclipse için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="0cbd2-209">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="0cbd2-210">[Yükleme hello Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="0cbd2-210">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="0cbd2-211">[Oturum açma hello Eclipse için Azure Araç Seti için yönergeler]</span><span class="sxs-lookup"><span data-stu-id="0cbd2-211">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="0cbd2-212">[Eclipse'te Azure Hello World web uygulaması oluşturma]</span><span class="sxs-lookup"><span data-stu-id="0cbd2-212">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="0cbd2-213">[IntelliJ için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="0cbd2-213">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="0cbd2-214">[Merhaba Intellij için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="0cbd2-214">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="0cbd2-215">[Yükleme hello Intellij için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="0cbd2-215">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="0cbd2-216">[Oturum açma hello Azure Araç Seti için Intellij için yönergeler]</span><span class="sxs-lookup"><span data-stu-id="0cbd2-216">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="0cbd2-217">[Intellij Azure'da Hello World web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="0cbd2-217">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="0cbd2-218">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="0cbd2-218">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="0cbd2-219">Merhaba resmi Docker için ek kaynaklar için bkz: [Docker Web sitesi].</span><span class="sxs-lookup"><span data-stu-id="0cbd2-219">For additional resources for Docker, see hello official [Docker website].</span></span>

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