---
title: "bir Linux sanal makine üzerinde Apache Tomcat yukarı aaaSet | Microsoft Docs"
description: "Bilgi nasıl Linux çalıştıran Azure sanal makineler kullanarak tooset Apache tomcat7'yi ayarlama."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 45ecc89c-1cb0-4e80-8944-bd0d0bbedfdc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: ningk
ms.openlocfilehash: b837a73e91fcb25d5459d993a0e93ceef1a1fc8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a><span data-ttu-id="f38fa-103">Azure ile Linux sanal makine tomcat7'yi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="f38fa-103">Set up Tomcat7 on a Linux virtual machine with Azure</span></span>
<span data-ttu-id="f38fa-104">Apache Tomcat (veya yalnızca Cakarta Tomcat adıysa ayrıca Tomcat) bir açık kaynak web sunucusu ve hello Apache yazılım Foundation (ASF) tarafından geliştirilmiş servlet kapsayıcı değil.</span><span class="sxs-lookup"><span data-stu-id="f38fa-104">Apache Tomcat (or simply Tomcat, also formerly called Jakarta Tomcat) is an open source web server and servlet container developed by hello Apache Software Foundation (ASF).</span></span> <span data-ttu-id="f38fa-105">Tomcat hello Java Servlet ve Sun Microsystems hello JavaServer sayfaları (JSP) belirtimlerine uygular.</span><span class="sxs-lookup"><span data-stu-id="f38fa-105">Tomcat implements hello Java Servlet and hello JavaServer Pages (JSP) specifications from Sun Microsystems.</span></span> <span data-ttu-id="f38fa-106">Tomcat hangi toorun Java kod içinde saf Java HTTP web sunucusu ortamı sağlar.</span><span class="sxs-lookup"><span data-stu-id="f38fa-106">Tomcat provides a pure Java HTTP web server environment in which toorun Java code.</span></span> <span data-ttu-id="f38fa-107">Merhaba basit yapılandırmada, Tomcat tek işletim sistemi işleminde çalışır.</span><span class="sxs-lookup"><span data-stu-id="f38fa-107">In hello simplest configuration, Tomcat runs in a single operating system process.</span></span> <span data-ttu-id="f38fa-108">Bu işlem, Java sanal makinesi (JVM) çalışır.</span><span class="sxs-lookup"><span data-stu-id="f38fa-108">This process runs a Java virtual machine (JVM).</span></span> <span data-ttu-id="f38fa-109">Her bir tarayıcı tooTomcat HTTP isteğinden hello Tomcat işleminde ayrı bir iş parçacığı olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="f38fa-109">Every HTTP request from a browser tooTomcat is processed as a separate thread in hello Tomcat process.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="f38fa-110">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f38fa-110">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f38fa-111">Bu makalede, nasıl toouse hello Klasik dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="f38fa-111">This article covers how toouse hello classic deployment model.</span></span> <span data-ttu-id="f38fa-112">En yeni dağıtımların hello Resource Manager modelini kullanmasını öneririz.</span><span class="sxs-lookup"><span data-stu-id="f38fa-112">We recommend that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="f38fa-113">toouse bir Resource Manager şablonu toodeploy bir Ubuntu VM açık JDK ve Tomcat, bkz: [bu makalede](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span><span class="sxs-lookup"><span data-stu-id="f38fa-113">toouse a Resource Manager template toodeploy an Ubuntu VM with Open JDK and Tomcat, see [this article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span></span>

<span data-ttu-id="f38fa-114">Bu makalede, Linux görüntüde tomcat7'yi yükleyin ve Azure'da dağıtın.</span><span class="sxs-lookup"><span data-stu-id="f38fa-114">In this article, you will install Tomcat7 on a Linux image and deploy it in Azure.</span></span>  

<span data-ttu-id="f38fa-115">Şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="f38fa-115">You will learn:</span></span>  

* <span data-ttu-id="f38fa-116">Nasıl toocreate azure'da bir sanal makine.</span><span class="sxs-lookup"><span data-stu-id="f38fa-116">How toocreate a virtual machine in Azure.</span></span>
* <span data-ttu-id="f38fa-117">Nasıl tooprepare hello sanal makine için tomcat7'yi.</span><span class="sxs-lookup"><span data-stu-id="f38fa-117">How tooprepare hello virtual machine for Tomcat7.</span></span>
* <span data-ttu-id="f38fa-118">Nasıl tooinstall tomcat7'yi.</span><span class="sxs-lookup"><span data-stu-id="f38fa-118">How tooinstall Tomcat7.</span></span>

<span data-ttu-id="f38fa-119">Bir Azure aboneliği zaten sahip olduğunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="f38fa-119">It is assumed that you already have an Azure subscription.</span></span>  <span data-ttu-id="f38fa-120">Ücretsiz deneme için kaydolabilirsiniz değil, varsa [Azure Web sitesi hello](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="f38fa-120">If not, you can sign up for a free trial at [hello Azure website](https://azure.microsoft.com/).</span></span> <span data-ttu-id="f38fa-121">Bir MSDN aboneliğiniz varsa, bkz: [Microsoft Azure özel fiyatlandırma: MSDN, MPN ve BizSpark avantajları](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span><span class="sxs-lookup"><span data-stu-id="f38fa-121">If you have an MSDN subscription, see [Microsoft Azure Special Pricing: MSDN, MPN, and BizSpark Benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span></span> <span data-ttu-id="f38fa-122">Azure, hakkında daha fazla toolearn bkz [Azure nedir?](https://azure.microsoft.com/overview/what-is-azure/).</span><span class="sxs-lookup"><span data-stu-id="f38fa-122">toolearn more about Azure, see [What is Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span></span>

<span data-ttu-id="f38fa-123">Bu makalede, Tomcat ve Linux temel bilgiye sahip olduğunuz varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f38fa-123">This article assumes that you have a basic working knowledge of Tomcat and Linux.</span></span>  

## <a name="phase-1-create-an-image"></a><span data-ttu-id="f38fa-124">1. Aşama: görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="f38fa-124">Phase 1: Create an image</span></span>
<span data-ttu-id="f38fa-125">Bu aşamada, Azure'da bir Linux görüntüsü kullanarak bir sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f38fa-125">In this phase, you will create a virtual machine by using a Linux image in Azure.</span></span>  

### <a name="step-1-generate-an-ssh-authentication-key"></a><span data-ttu-id="f38fa-126">1. adım: bir SSH kimlik doğrulama anahtarı oluştur</span><span class="sxs-lookup"><span data-stu-id="f38fa-126">Step 1: Generate an SSH authentication key</span></span>
<span data-ttu-id="f38fa-127">SSH, sistem yöneticileri için önemli bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="f38fa-127">SSH is an important tool for system administrators.</span></span> <span data-ttu-id="f38fa-128">Ancak, insan tarafından belirlenen bir parola tabanlı erişim güvenlik yapılandırma önerilmez.</span><span class="sxs-lookup"><span data-stu-id="f38fa-128">However, configuring access security based on a human-determined password is not recommended.</span></span> <span data-ttu-id="f38fa-129">Kötü niyetli kullanıcılar, bir kullanıcı adı ve zayıf bir parolaya göre sisteminizi içine bozulabilir.</span><span class="sxs-lookup"><span data-stu-id="f38fa-129">Malicious users can break into your system based on a username and a weak password.</span></span>

<span data-ttu-id="f38fa-130">Merhaba iyi haber tooleave uzaktan erişim açın ve parolalar hakkında endişelenmeniz olmayan bir yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="f38fa-130">hello good news is that there is a way tooleave remote access open and not worry about passwords.</span></span> <span data-ttu-id="f38fa-131">Bu yöntem, asimetrik şifreleme ile kimlik doğrulaması oluşur.</span><span class="sxs-lookup"><span data-stu-id="f38fa-131">This method consists of authentication with asymmetric cryptography.</span></span> <span data-ttu-id="f38fa-132">Merhaba kullanıcının özel hello hello kimlik doğrulaması veren bir anahtardır.</span><span class="sxs-lookup"><span data-stu-id="f38fa-132">hello user’s private key is hello one that grants hello authentication.</span></span> <span data-ttu-id="f38fa-133">Merhaba kullanıcının hesabı bile kilitleyebilirsiniz toonot izin parola kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="f38fa-133">You can even lock hello user’s account toonot allow password authentication.</span></span>

<span data-ttu-id="f38fa-134">Bu yöntemin başka bir avantajı, farklı parolalar toosign toodifferent sunucularında gerekmez ' dir.</span><span class="sxs-lookup"><span data-stu-id="f38fa-134">Another advantage of this method is that you do not need different passwords toosign in toodifferent servers.</span></span> <span data-ttu-id="f38fa-135">Merhaba kişisel özel anahtarı tüm sunucularda, tooremember birkaç parolaların önleyen kullanılarak doğrulanabilir.</span><span class="sxs-lookup"><span data-stu-id="f38fa-135">You can authenticate by using hello personal private key on all servers, which prevents you from having tooremember several passwords.</span></span>



<span data-ttu-id="f38fa-136">Bu adımları toogenerate hello SSH kimlik doğrulama anahtarı izleyin.</span><span class="sxs-lookup"><span data-stu-id="f38fa-136">Follow these steps toogenerate hello SSH authentication key.</span></span>

1. <span data-ttu-id="f38fa-137">PuTTYgen konumu aşağıdaki hello yükleyip: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="f38fa-137">Download and install PuTTYgen from hello following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="f38fa-138">Puttygen.exe çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f38fa-138">Run Puttygen.exe.</span></span>
3. <span data-ttu-id="f38fa-139">Tıklatın **Generate** toogenerate hello anahtarları.</span><span class="sxs-lookup"><span data-stu-id="f38fa-139">Click **Generate** toogenerate hello keys.</span></span> <span data-ttu-id="f38fa-140">Merhaba işleminde hello penceresinde hello boş alanı üzerinden taşıma hello fareyle rastgele artırabilir.</span><span class="sxs-lookup"><span data-stu-id="f38fa-140">In hello process, you can increase randomness by moving hello mouse over hello blank area in hello window.</span></span>  
   <span data-ttu-id="f38fa-141">![Yeni anahtar düğmesi hello gösteren puTTY anahtar Oluşturucu ekran görüntüsü oluştur][1]</span><span class="sxs-lookup"><span data-stu-id="f38fa-141">![PuTTY Key Generator screenshot that shows hello generate new key button][1]</span></span>
4. <span data-ttu-id="f38fa-142">İşlem Hello oluşturduktan sonra yeni bir ortak anahtar Puttygen.exe gösterir.</span><span class="sxs-lookup"><span data-stu-id="f38fa-142">After hello generate process, Puttygen.exe will show your new public key.</span></span>  
   ![Merhaba yeni ortak anahtar ve özel anahtar düğmesi kaydetme hello gösteren puTTY anahtar Oluşturucu ekran görüntüsü][2]
5. <span data-ttu-id="f38fa-144">Seçin ve hello ortak anahtarı kopyalayın ve publicKey.pem adlı bir dosyaya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f38fa-144">Select and copy hello public key, and save it in a file named publicKey.pem.</span></span> <span data-ttu-id="f38fa-145">Tıklamayın **ortak anahtarı Kaydet**, ortak anahtarın dosya biçimi kaydedilmiş hello istiyoruz hello ortak anahtarından farklı olduğu için.</span><span class="sxs-lookup"><span data-stu-id="f38fa-145">Don’t click **Save public key**, because hello saved public key’s file format is different from hello public key we want.</span></span>
6. <span data-ttu-id="f38fa-146">Tıklatın **özel anahtarı Kaydet**ve privateKey.ppk adlı bir dosyaya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f38fa-146">Click **Save private key**, and save it in a file named privateKey.ppk.</span></span>

### <a name="step-2-create-hello-image-in-hello-azure-portal"></a><span data-ttu-id="f38fa-147">2. adım: hello Azure portal hello görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="f38fa-147">Step 2: Create hello image in hello Azure portal</span></span>
1. <span data-ttu-id="f38fa-148">Merhaba, [portal](https://portal.azure.com/), tıklatın **yeni** hello toocreate görüntüyü görev.</span><span class="sxs-lookup"><span data-stu-id="f38fa-148">In hello [portal](https://portal.azure.com/), click **New** in hello task bar toocreate an image.</span></span> <span data-ttu-id="f38fa-149">Ardından gereksinimlerinize göre hello Linux görüntü seçin.</span><span class="sxs-lookup"><span data-stu-id="f38fa-149">Then choose hello Linux image that is based on your needs.</span></span> <span data-ttu-id="f38fa-150">Merhaba aşağıdaki örnek hello Ubuntu 14.04 görüntüyü kullanır.</span><span class="sxs-lookup"><span data-stu-id="f38fa-150">hello following example uses hello Ubuntu 14.04 image.</span></span>
<span data-ttu-id="f38fa-151">![Merhaba portalının hello yeni düğmesini gösteren ekran görüntüsü][3]</span><span class="sxs-lookup"><span data-stu-id="f38fa-151">![Screenshot of hello portal that shows hello New button][3]</span></span>

2. <span data-ttu-id="f38fa-152">İçin **ana bilgisayar adı**, tooaccess ve Internet istemcileri bu sanal makine kullanır hello URL için hello adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="f38fa-152">For **Host Name**, specify hello name for hello URL that you and Internet clients will use tooaccess this virtual machine.</span></span> <span data-ttu-id="f38fa-153">Merhaba DNS adı, örneğin, tomcatdemo son parçası Hello tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="f38fa-153">Define hello last part of hello DNS name, for example, tomcatdemo.</span></span> <span data-ttu-id="f38fa-154">Azure, ardından tomcatdemo.cloudapp.net hello URL oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f38fa-154">Azure will then generate hello URL as tomcatdemo.cloudapp.net.</span></span>  

3. <span data-ttu-id="f38fa-155">İçin **SSH kimlik doğrulama anahtarı**, PuTTYgen tarafından oluşturulan hello ortak anahtarı içeren hello publicKey.pem dosyasından hello anahtar değerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="f38fa-155">For **SSH Authentication Key**, copy hello key value from hello publicKey.pem file, which contains hello public key generated by PuTTYgen.</span></span>  
<span data-ttu-id="f38fa-156">![SSH kimlik doğrulama anahtarı hello Portalı'nda kutusu][4]</span><span class="sxs-lookup"><span data-stu-id="f38fa-156">![SSH Authentication Key box in hello portal][4]</span></span>

4. <span data-ttu-id="f38fa-157">Diğer ayarları gerektiği gibi yapılandırın ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="f38fa-157">Configure other settings as needed, and then click **Create**.</span></span>  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a><span data-ttu-id="f38fa-158">2. Aşama: sanal makineniz tomcat7'yi için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="f38fa-158">Phase 2: Prepare your virtual machine for Tomcat7</span></span>
<span data-ttu-id="f38fa-159">Bu aşamada, Tomcat trafiği için bir uç nokta yapılandırmak ve tooyour yeni bir sanal makine bağlayın.</span><span class="sxs-lookup"><span data-stu-id="f38fa-159">In this phase, you will configure an endpoint for Tomcat traffic, and then connect tooyour new virtual machine.</span></span>

### <a name="step-1-open-hello-http-port-tooallow-web-access"></a><span data-ttu-id="f38fa-160">1. adım: hello HTTP bağlantı noktası tooallow web erişimi'ni açın</span><span class="sxs-lookup"><span data-stu-id="f38fa-160">Step 1: Open hello HTTP port tooallow web access</span></span>
<span data-ttu-id="f38fa-161">Azure uç noktaları ile birlikte bir ortak ve özel bağlantı noktası TCP veya UDP protokolünü oluşur.</span><span class="sxs-lookup"><span data-stu-id="f38fa-161">Endpoints in Azure consist of a TCP or UDP protocol, along with a public and private port.</span></span> <span data-ttu-id="f38fa-162">Merhaba özel bağlantı noktası hello hizmetinin tooon hello sanal makine dinlediğini hello bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="f38fa-162">hello private port is hello port that hello service is listening tooon hello virtual machine.</span></span> <span data-ttu-id="f38fa-163">tooexternally gelen, Internet tabanlı trafiği için Azure bulut hizmeti hello hello bağlantı noktasını dinler Hello genel bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="f38fa-163">hello public port is hello port that hello Azure cloud service listens tooexternally for incoming, Internet-based traffic.</span></span>  

<span data-ttu-id="f38fa-164">TCP bağlantı noktası 8080 Tomcat toolisten kullandığını hello varsayılan bağlantı noktası numarasıdır.</span><span class="sxs-lookup"><span data-stu-id="f38fa-164">TCP port 8080 is hello default port number that Tomcat uses toolisten.</span></span> <span data-ttu-id="f38fa-165">Bu bağlantı noktası ile Azure bir uç nokta açıldıysa, sizin ve diğer Internet istemcileri Tomcat sayfalarına erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f38fa-165">If this port is opened with an Azure endpoint, you and other Internet clients can access Tomcat pages.</span></span>  

1. <span data-ttu-id="f38fa-166">Hello Portalı'nda tıklatın **Gözat** > **sanal makineler**ve ardından oluşturduğunuz hello sanal makineyi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f38fa-166">In hello portal, click **Browse** > **Virtual machines**, and then click hello virtual machine that you created.</span></span>  
   <span data-ttu-id="f38fa-167">![Merhaba sanal makineleri dizininin ekran görüntüsü][5]</span><span class="sxs-lookup"><span data-stu-id="f38fa-167">![Screenshot of hello Virtual machines directory][5]</span></span>
2. <span data-ttu-id="f38fa-168">tooadd bir uç nokta tooyour sanal makine tıklatın hello **uç noktaları** kutusu.</span><span class="sxs-lookup"><span data-stu-id="f38fa-168">tooadd an endpoint tooyour virtual machine, click hello **Endpoints** box.</span></span>
   <span data-ttu-id="f38fa-169">![Merhaba uç noktaları kutusunu gösteren ekran görüntüsü][6]</span><span class="sxs-lookup"><span data-stu-id="f38fa-169">![Screenshot that shows hello Endpoints box][6]</span></span>
3. <span data-ttu-id="f38fa-170">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f38fa-170">Click **Add**.</span></span>  

   1. <span data-ttu-id="f38fa-171">Merhaba uç noktası için bir hello uç adı **Endpoint**ve 80 enter **genel bağlantı noktası**.</span><span class="sxs-lookup"><span data-stu-id="f38fa-171">For hello endpoint, enter a name for hello endpoint in **Endpoint**, and then enter 80 in **Public Port**.</span></span>  

      <span data-ttu-id="f38fa-172">Too80 ayarlarsanız tooinclude hello bağlantı noktası numarası kullanılan tooaccess Tomcat hello URL gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f38fa-172">If you set it too80, you don’t need tooinclude hello port number in hello URL that is used tooaccess Tomcat.</span></span> <span data-ttu-id="f38fa-173">Örneğin, http://tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="f38fa-173">For example, http://tomcatdemo.cloudapp.net.</span></span>    

      <span data-ttu-id="f38fa-174">81 gibi tooanother değerini ayarlarsanız tooadd hello bağlantı noktası numarası toohello URL tooaccess Tomcat gerekir.</span><span class="sxs-lookup"><span data-stu-id="f38fa-174">If you set it tooanother value, such as 81, you need tooadd hello port number toohello URL tooaccess Tomcat.</span></span> <span data-ttu-id="f38fa-175">Örneğin, http://tomcatdemo.cloudapp.net:81 /.</span><span class="sxs-lookup"><span data-stu-id="f38fa-175">For example,  http://tomcatdemo.cloudapp.net:81/.</span></span>
   2. <span data-ttu-id="f38fa-176">İçinde 8080 girin **özel bağlantı noktası**.</span><span class="sxs-lookup"><span data-stu-id="f38fa-176">Enter 8080 in **Private Port**.</span></span> <span data-ttu-id="f38fa-177">Varsayılan olarak, TCP bağlantı noktası 8080 Tomcat dinler.</span><span class="sxs-lookup"><span data-stu-id="f38fa-177">By default, Tomcat listens on TCP port 8080.</span></span> <span data-ttu-id="f38fa-178">Merhaba varsayılan dinleme Tomcat bağlantı noktasını değiştirdiyseniz, güncelleştirmelidir **özel bağlantı noktası** toobe hello Tomcat dinleme bağlantı noktası hello aynı.</span><span class="sxs-lookup"><span data-stu-id="f38fa-178">If you changed hello default listen port of Tomcat, you should update **Private Port** toobe hello same as hello Tomcat listen port.</span></span>  
      <span data-ttu-id="f38fa-179">![Ekran görüntüsü, Ekle komutu, genel bağlantı noktası ve özel bağlantı noktası gösteren kullanıcı Arabirimi][7]</span><span class="sxs-lookup"><span data-stu-id="f38fa-179">![Screenshot of UI that shows Add command, Public Port, and Private Port][7]</span></span>
4. <span data-ttu-id="f38fa-180">Tıklatın **Tamam** tooadd hello uç nokta tooyour sanal makine.</span><span class="sxs-lookup"><span data-stu-id="f38fa-180">Click **OK** tooadd hello endpoint tooyour virtual machine.</span></span>

### <a name="step-2-connect-toohello-image-you-created"></a><span data-ttu-id="f38fa-181">2. adım: oluşturduğunuz toohello görüntü Bağlan</span><span class="sxs-lookup"><span data-stu-id="f38fa-181">Step 2: Connect toohello image you created</span></span>
<span data-ttu-id="f38fa-182">SSH aracı tooconnect tooyour sanal makine seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f38fa-182">You can choose any SSH tool tooconnect tooyour virtual machine.</span></span> <span data-ttu-id="f38fa-183">Bu örnekte, PuTTY kullanın.</span><span class="sxs-lookup"><span data-stu-id="f38fa-183">In this example, we use PuTTY.</span></span>  

1. <span data-ttu-id="f38fa-184">Sanal makinenizin Hello DNS adı hello portaldan alın.</span><span class="sxs-lookup"><span data-stu-id="f38fa-184">Get hello DNS name of your virtual machine from hello portal.</span></span>
    1. <span data-ttu-id="f38fa-185">Tıklatın **Gözat** > **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="f38fa-185">Click **Browse** > **Virtual machines**.</span></span>
    2. <span data-ttu-id="f38fa-186">Merhaba, sanal makinenin adını seçin ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="f38fa-186">Select hello name of your virtual machine, and then click **Properties**.</span></span>
    3. <span data-ttu-id="f38fa-187">Merhaba, **özellikleri** döşeme, hello bakın **etki alanı adı** kutusunu tooget hello DNS adı.</span><span class="sxs-lookup"><span data-stu-id="f38fa-187">In hello **Properties** tile, look in hello **Domain Name** box tooget hello DNS name.</span></span>  

2. <span data-ttu-id="f38fa-188">Merhaba SSH bağlantılarında Hello bağlantı noktası numarası alma **SSH** kutusu.</span><span class="sxs-lookup"><span data-stu-id="f38fa-188">Get hello port number for SSH connections from hello **SSH** box.</span></span>  
<span data-ttu-id="f38fa-189">![Merhaba SSH bağlantı noktası gösteren ekran görüntüsü][8]</span><span class="sxs-lookup"><span data-stu-id="f38fa-189">![Screenshot that shows hello SSH connection port number][8]</span></span>

3. <span data-ttu-id="f38fa-190">Karşıdan [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="f38fa-190">Download [PuTTY](http://www.putty.org/).</span></span>  

4. <span data-ttu-id="f38fa-191">İndirdikten sonra hello yürütülebilir dosya Putty.exe'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f38fa-191">After downloading, click hello executable file Putty.exe.</span></span> <span data-ttu-id="f38fa-192">PuTTY yapılandırması hello ana bilgisayar adıyla hello temel seçeneklerini yapılandırmak ve bağlantı noktası, sanal makinenize hello özelliklerinden elde sayısını.</span><span class="sxs-lookup"><span data-stu-id="f38fa-192">In PuTTY configuration, configure hello basic options with hello host name and port number that is obtained from hello properties of your virtual machine.</span></span>   
![Merhaba PuTTY yapılandırması ana bilgisayar adı ve bağlantı noktası seçeneklerini gösteren ekran görüntüsü][9]

5. <span data-ttu-id="f38fa-194">Merhaba sol bölmede **bağlantı** > **SSH** > **Auth**ve ardından **Gözat** toospecify Merhaba privateKey.ppk dosyasının başlangıç konumu.</span><span class="sxs-lookup"><span data-stu-id="f38fa-194">In hello left pane, click **Connection** > **SSH** > **Auth**, and then click **Browse** toospecify hello location of hello privateKey.ppk file.</span></span> <span data-ttu-id="f38fa-195">Hello privateKey.ppk dosyasını önceki hello PuTTYgen tarafından oluşturulan hello özel anahtarı içeren "1. Aşama: görüntü oluşturma" bölümünde bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="f38fa-195">hello privateKey.ppk file contains hello private key that is generated by PuTTYgen earlier in hello "Phase 1: Create an image" section of this article.</span></span>  
<span data-ttu-id="f38fa-196">![Merhaba bağlantı dizin hiyerarşisi ve Gözat düğmesini gösteren ekran görüntüsü][10]</span><span class="sxs-lookup"><span data-stu-id="f38fa-196">![Screenshot that shows hello Connection directory hierarchy and Browse button][10]</span></span>

6. <span data-ttu-id="f38fa-197">Tıklatın **açık**.</span><span class="sxs-lookup"><span data-stu-id="f38fa-197">Click **Open**.</span></span> <span data-ttu-id="f38fa-198">Bir ileti kutusu tarafından uyarı.</span><span class="sxs-lookup"><span data-stu-id="f38fa-198">You might be alerted by a message box.</span></span> <span data-ttu-id="f38fa-199">Yapılandırılan hello DNS adı ve bağlantı noktası numarası doğru değilse, tıklatın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="f38fa-199">If you have configured hello DNS name and port number correctly, click **Yes**.</span></span>
<span data-ttu-id="f38fa-200">![Merhaba bildirim gösteren ekran görüntüsü][11]</span><span class="sxs-lookup"><span data-stu-id="f38fa-200">![Screenshot that shows hello notification][11]</span></span>

7. <span data-ttu-id="f38fa-201">Kullanıcı adınızı istendiğinde tooenter şunlardır.</span><span class="sxs-lookup"><span data-stu-id="f38fa-201">You are prompted tooenter your username.</span></span>  
![Where gösteren ekran görüntüsü tooenter kullanıcı adı][12]

8. <span data-ttu-id="f38fa-203">Hello toocreate hello sanal makine kullanılan hello kullanıcı adı girin "1. Aşama: görüntü oluşturma" bölümünde bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="f38fa-203">Enter hello username that you used toocreate hello virtual machine in hello "Phase 1: Create an image" section earlier in this article.</span></span> <span data-ttu-id="f38fa-204">Merhaba aşağıdaki gibi bir şey görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="f38fa-204">You will see something like hello following:</span></span>  
![Merhaba kimlik doğrulama onay gösteren ekran görüntüsü][13]

## <a name="phase-3-install-software"></a><span data-ttu-id="f38fa-206">3. Aşama: Yazılımı yükleme</span><span class="sxs-lookup"><span data-stu-id="f38fa-206">Phase 3: Install software</span></span>
<span data-ttu-id="f38fa-207">Bu aşamada hello Java Çalışma zamanı ortamı, tomcat7'yi ve diğer tomcat7'yi bileşenlerini yükler.</span><span class="sxs-lookup"><span data-stu-id="f38fa-207">In this phase, you install hello Java runtime environment, Tomcat7, and other Tomcat7 components.</span></span>  

### <a name="java-runtime-environment"></a><span data-ttu-id="f38fa-208">Java Çalışma zamanı ortamı</span><span class="sxs-lookup"><span data-stu-id="f38fa-208">Java runtime environment</span></span>
<span data-ttu-id="f38fa-209">Tomcat Java'da yazılmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f38fa-209">Tomcat is written in Java.</span></span> <span data-ttu-id="f38fa-210">Java geliştirme setleri (JDKs), OpenJDK ve Oracle JDK iki tür vardır.</span><span class="sxs-lookup"><span data-stu-id="f38fa-210">There are two kinds of Java Development Kits (JDKs), OpenJDK and Oracle JDK.</span></span> <span data-ttu-id="f38fa-211">Merhaba istediğinizi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f38fa-211">You can choose hello one you want.</span></span>  

> [!NOTE]
> <span data-ttu-id="f38fa-212">Hem JDKs neredeyse aynı hello sınıflarda hello Java API için kod hello sahip, ancak hello kod hello sanal makine için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="f38fa-212">Both JDKs have almost hello same code for hello classes in hello Java API, but hello code for hello virtual machine is different.</span></span> <span data-ttu-id="f38fa-213">OpenJDK toouse açık kitaplıkları eğilimlidir, Oracle JDK eğilimlidir sırada toouse olanları kapalı.</span><span class="sxs-lookup"><span data-stu-id="f38fa-213">OpenJDK tends toouse open libraries, while Oracle JDK tends toouse closed ones.</span></span> <span data-ttu-id="f38fa-214">Oracle JDK sahip daha sınıfları ve bazı düzeltilen hatalar ve Oracle JDK OpenJDK daha fazla kararlı.</span><span class="sxs-lookup"><span data-stu-id="f38fa-214">Oracle JDK has more classes and some fixed bugs, and Oracle JDK is more stable than OpenJDK.</span></span>

#### <a name="install-openjdk"></a><span data-ttu-id="f38fa-215">OpenJDK yükleyin</span><span class="sxs-lookup"><span data-stu-id="f38fa-215">Install OpenJDK</span></span>  

<span data-ttu-id="f38fa-216">Aşağıdaki komut toodownload OpenJDK hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="f38fa-216">Use hello following command toodownload OpenJDK.</span></span>   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* <span data-ttu-id="f38fa-217">toocreate dizin toocontain JDK dosyaları hello:</span><span class="sxs-lookup"><span data-stu-id="f38fa-217">toocreate a directory toocontain hello JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="f38fa-218">tooextract hello JDK dosyalarıyla hello/usr/lib/jvm/directory:</span><span class="sxs-lookup"><span data-stu-id="f38fa-218">tooextract hello JDK files into hello /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a><span data-ttu-id="f38fa-219">Oracle JDK yükleyin</span><span class="sxs-lookup"><span data-stu-id="f38fa-219">Install Oracle JDK</span></span>


<span data-ttu-id="f38fa-220">Komut toodownload Oracle JDK hello Oracle Web sitesinden aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="f38fa-220">Use hello following command toodownload Oracle JDK from hello Oracle website.</span></span>  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* <span data-ttu-id="f38fa-221">toocreate dizin toocontain JDK dosyaları hello:</span><span class="sxs-lookup"><span data-stu-id="f38fa-221">toocreate a directory toocontain hello JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="f38fa-222">tooextract hello JDK dosyalarıyla hello/usr/lib/jvm/directory:</span><span class="sxs-lookup"><span data-stu-id="f38fa-222">tooextract hello JDK files into hello /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* <span data-ttu-id="f38fa-223">Oracle varsayılan Java sanal makinesi hello gibi JDK tooset:</span><span class="sxs-lookup"><span data-stu-id="f38fa-223">tooset Oracle JDK as hello default Java virtual machine:</span></span>  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a><span data-ttu-id="f38fa-224">Java yüklemenin başarılı olduğunu onaylayın</span><span class="sxs-lookup"><span data-stu-id="f38fa-224">Confirm that Java installation is successful</span></span>
<span data-ttu-id="f38fa-225">Merhaba Java Çalışma zamanı ortamı düzgün yüklenmediyse tootest aşağıdaki hello gibi bir komutu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f38fa-225">You can use a command like hello following tootest if hello Java runtime environment is installed correctly:</span></span>  

    java -version  

<span data-ttu-id="f38fa-226">OpenJDK yüklediyseniz, hello aşağıdaki gibi bir ileti görürsünüz: ![başarılı OpenJDK yükleme iletisi][14]</span><span class="sxs-lookup"><span data-stu-id="f38fa-226">If you installed OpenJDK, you should see a message like hello following: ![Successful OpenJDK installation message][14]</span></span>

<span data-ttu-id="f38fa-227">Oracle JDK yüklediyseniz, hello aşağıdaki gibi bir ileti görürsünüz: ![başarılı Oracle JDK yükleme iletisi][15]</span><span class="sxs-lookup"><span data-stu-id="f38fa-227">If you installed Oracle JDK, you should see a message like hello following: ![Successful Oracle JDK installation message][15]</span></span>

### <a name="install-tomcat7"></a><span data-ttu-id="f38fa-228">Tomcat7'yi yükleme</span><span class="sxs-lookup"><span data-stu-id="f38fa-228">Install Tomcat7</span></span>
<span data-ttu-id="f38fa-229">Komut tooinstall tomcat7'yi aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="f38fa-229">Use hello following command tooinstall Tomcat7.</span></span>  

    sudo apt-get install tomcat7  

<span data-ttu-id="f38fa-230">Tomcat7'yi kullanmıyorsanız, bu komutun uygun varyasyonunu hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="f38fa-230">If you are not using Tomcat7, use hello appropriate variation of this command.</span></span>  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a><span data-ttu-id="f38fa-231">Tomcat7'yi yükleme işleminin başarılı olduğunu doğrulayın</span><span class="sxs-lookup"><span data-stu-id="f38fa-231">Confirm that Tomcat7 installation is successful</span></span>
<span data-ttu-id="f38fa-232">toocheck tomcat7'yi başarıyla yüklediyseniz, tooyour Tomcat sunucusunun DNS adı gözatın.</span><span class="sxs-lookup"><span data-stu-id="f38fa-232">toocheck if Tomcat7 is successfully installed, browse tooyour Tomcat server’s DNS name.</span></span> <span data-ttu-id="f38fa-233">Bu makalede, http://tomcatexample.cloudapp.net/ hello örnek URL'dir.</span><span class="sxs-lookup"><span data-stu-id="f38fa-233">In this article, hello example URL is http://tomcatexample.cloudapp.net/.</span></span> <span data-ttu-id="f38fa-234">Merhaba aşağıdaki gibi bir ileti görürseniz, tomcat7'yi doğru bir şekilde yüklendi.</span><span class="sxs-lookup"><span data-stu-id="f38fa-234">If you see a message like hello following, Tomcat7 is installed correctly.</span></span>
<span data-ttu-id="f38fa-235">![Başarılı tomcat7'yi yükleme iletisi][16]</span><span class="sxs-lookup"><span data-stu-id="f38fa-235">![Successful Tomcat7 installation message][16]</span></span>

### <a name="install-other-tomcat7-components"></a><span data-ttu-id="f38fa-236">Diğer tomcat7'yi bileşenlerini yükle</span><span class="sxs-lookup"><span data-stu-id="f38fa-236">Install other Tomcat7 components</span></span>
<span data-ttu-id="f38fa-237">Yükleyebileceğiniz isteğe bağlı diğer Tomcat bileşenleri vardır.</span><span class="sxs-lookup"><span data-stu-id="f38fa-237">There are other optional Tomcat components that you can install.</span></span>  

<span data-ttu-id="f38fa-238">Kullanım hello **sudo önbellek apt arama tomcat7'yi** komutu toosee hello kullanılabilir bileşenlerinin tümünü.</span><span class="sxs-lookup"><span data-stu-id="f38fa-238">Use hello **sudo apt-cache search tomcat7** command toosee all of hello available components.</span></span> <span data-ttu-id="f38fa-239">Aşağıdaki komutları tooinstall hello bazı yararlı bileşenlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f38fa-239">Use hello following commands tooinstall some useful components.</span></span>  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools toocreate user instances  

## <a name="phase-4-configure-tomcat7"></a><span data-ttu-id="f38fa-240">4. Aşama: Tomcat7'yi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f38fa-240">Phase 4: Configure Tomcat7</span></span>
<span data-ttu-id="f38fa-241">Bu aşamada, Tomcat yönetin.</span><span class="sxs-lookup"><span data-stu-id="f38fa-241">In this phase, you administer Tomcat.</span></span>

### <a name="start-and-stop-tomcat7"></a><span data-ttu-id="f38fa-242">Tomcat7'yi durdurup başlatın</span><span class="sxs-lookup"><span data-stu-id="f38fa-242">Start and stop Tomcat7</span></span>
<span data-ttu-id="f38fa-243">Merhaba tomcat7'yi sunucusu yüklediğinizde otomatik olarak başlatır.</span><span class="sxs-lookup"><span data-stu-id="f38fa-243">hello Tomcat7 server automatically starts when you install it.</span></span> <span data-ttu-id="f38fa-244">Bu komutu aşağıdaki hello ile de başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f38fa-244">You can also start it with hello following command:</span></span>   

    sudo /etc/init.d/tomcat7 start

<span data-ttu-id="f38fa-245">toostop tomcat7'yi:</span><span class="sxs-lookup"><span data-stu-id="f38fa-245">toostop Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 stop

<span data-ttu-id="f38fa-246">tomcat7'yi tooview hello durumu:</span><span class="sxs-lookup"><span data-stu-id="f38fa-246">tooview hello status of Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 status

<span data-ttu-id="f38fa-247">toorestart Tomcat Hizmetleri:</span><span class="sxs-lookup"><span data-stu-id="f38fa-247">toorestart Tomcat services:</span></span> 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a><span data-ttu-id="f38fa-248">Tomcat7'yi Yönetim</span><span class="sxs-lookup"><span data-stu-id="f38fa-248">Tomcat7 administration</span></span>
<span data-ttu-id="f38fa-249">Yönetici kimlik bilgilerinizi hello Tomcat kullanıcı yapılandırma dosyası tooset düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f38fa-249">You can edit hello Tomcat user configuration file tooset up your admin credentials.</span></span> <span data-ttu-id="f38fa-250">Merhaba aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="f38fa-250">Use hello following command:</span></span>  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

<span data-ttu-id="f38fa-251">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f38fa-251">Here is an example:</span></span>  
![Merhaba sudo VI komut çıktısı gösteren ekran görüntüsü][17]  

> [!NOTE]
> <span data-ttu-id="f38fa-253">Merhaba yönetici kullanıcı adı için güçlü bir parola oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f38fa-253">Create a strong password for hello admin username.</span></span>  

<span data-ttu-id="f38fa-254">Bu dosyasını düzenledikten sonra tomcat7'yi Hizmetleri hello değişiklikler etkili komutu tooensure aşağıdaki hello ile yeniden başlatmanız:</span><span class="sxs-lookup"><span data-stu-id="f38fa-254">After editing this file, you should restart Tomcat7 services with hello following command tooensure that hello changes take effect:</span></span>  

    sudo /etc/init.d/tomcat7 restart  

<span data-ttu-id="f38fa-255">Tarayıcınızı açın ve girin **http://<your tomcat server DNS name>/Yöneticisi/html** URL hello gibi.</span><span class="sxs-lookup"><span data-stu-id="f38fa-255">Open your browser, and enter **http://<your tomcat server DNS name>/manager/html** as hello URL.</span></span> <span data-ttu-id="f38fa-256">Bu makalede Hello örneğin hello http://tomcatexample.cloudapp.net/manager/html URL'dir.</span><span class="sxs-lookup"><span data-stu-id="f38fa-256">For hello example in this article, hello URL is http://tomcatexample.cloudapp.net/manager/html.</span></span>  

<span data-ttu-id="f38fa-257">Bağlandıktan sonra benzeri toohello aşağıdaki görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f38fa-257">After connecting, you should see something similar toohello following:</span></span>  
![Merhaba Tomcat Web Uygulama Yöneticisi ekran görüntüsü][18]

## <a name="common-issues"></a><span data-ttu-id="f38fa-259">Genel sorunlar</span><span class="sxs-lookup"><span data-stu-id="f38fa-259">Common issues</span></span>
### <a name="cant-access-hello-virtual-machine-with-tomcat-and-moodle-from-hello-internet"></a><span data-ttu-id="f38fa-260">Merhaba sanal makineyle Tomcat ve Moodle Internet hello erişemiyor</span><span class="sxs-lookup"><span data-stu-id="f38fa-260">Can't access hello virtual machine with Tomcat and Moodle from hello Internet</span></span>
#### <a name="symptom"></a><span data-ttu-id="f38fa-261">Belirti</span><span class="sxs-lookup"><span data-stu-id="f38fa-261">Symptom</span></span>  
  <span data-ttu-id="f38fa-262">Tomcat çalışıyor ancak tarayıcınızla hello Tomcat varsayılan sayfa göremez.</span><span class="sxs-lookup"><span data-stu-id="f38fa-262">Tomcat is running but you can’t see hello Tomcat default page with your browser.</span></span>
#### <a name="possible-root-cause"></a><span data-ttu-id="f38fa-263">Olası temel nedeni</span><span class="sxs-lookup"><span data-stu-id="f38fa-263">Possible root cause</span></span>   

  * <span data-ttu-id="f38fa-264">Merhaba Tomcat dinleme bağlantı noktası olan değil hello hello sanal makinenizin uç noktasının Tomcat trafiği için özel bağlantı noktası ile aynı.</span><span class="sxs-lookup"><span data-stu-id="f38fa-264">hello Tomcat listen port is not hello same as hello private port of your virtual machine's endpoint for Tomcat traffic.</span></span>  

     <span data-ttu-id="f38fa-265">Genel bağlantı noktası ve özel bağlantı noktası bitiş noktası ayarları ve hello özel bağlantı noktası aynı Tomcat hello hello olduğundan emin olun onay bağlantı noktasını dinler.</span><span class="sxs-lookup"><span data-stu-id="f38fa-265">Check your public port and private port endpoint settings and make sure hello private port is hello same as hello Tomcat listen port.</span></span> <span data-ttu-id="f38fa-266">Bkz: "1. Aşama: görüntü oluşturma" uç noktaları, sanal makine için yapılandırma hakkında yönergeler için bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="f38fa-266">See "Phase 1: Create an image" section of this article for instructions on configuring endpoints for your virtual machine.</span></span>  

     <span data-ttu-id="f38fa-267">toodetermine hello Tomcat dinleme bağlantı noktası, /etc/httpd/conf/httpd.conf (Red Hat sürüm) veya /etc/tomcat7/server.xml (Debian sürüm) açın.</span><span class="sxs-lookup"><span data-stu-id="f38fa-267">toodetermine hello Tomcat listen port, open /etc/httpd/conf/httpd.conf (Red Hat release), or /etc/tomcat7/server.xml (Debian release).</span></span> <span data-ttu-id="f38fa-268">Varsayılan olarak, hello Tomcat dinleme bağlantı noktası 8080'dir.</span><span class="sxs-lookup"><span data-stu-id="f38fa-268">By default, hello Tomcat listen port is 8080.</span></span> <span data-ttu-id="f38fa-269">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f38fa-269">Here is an example:</span></span>  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     <span data-ttu-id="f38fa-270">Toochange hello varsayılan bağlantı noktası, Tomcat dinleme (örneğin 8081) Debian ve Ubuntu ve istediğiniz gibi bir sanal makine kullanıyorsanız, hello işletim sistemi için başlangıç bağlantı noktası açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f38fa-270">If you are using a virtual machine like Debian or Ubuntu and you want toochange hello default port of Tomcat Listen (for example 8081), you should also open hello port for hello operating system.</span></span> <span data-ttu-id="f38fa-271">İlk olarak, hello profil açın:</span><span class="sxs-lookup"><span data-stu-id="f38fa-271">First, open hello profile:</span></span>  

        sudo vi /etc/default/tomcat7  

     <span data-ttu-id="f38fa-272">Ardından hello son satırı açıklamadan çıkarın ve "Hayır" çok "Evet" değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f38fa-272">Then uncomment hello last line and change “no” too“yes”.</span></span>  

        AUTHBIND=yes
  2. <span data-ttu-id="f38fa-273">Merhaba dinleme bağlantı noktası, Tomcat Hello Güvenlik Duvarı'nı devre dışı.</span><span class="sxs-lookup"><span data-stu-id="f38fa-273">hello firewall has disabled hello listen port of Tomcat.</span></span>

     <span data-ttu-id="f38fa-274">Yalnızca hello Tomcat varsayılan hello yerel ana sayfasından da görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f38fa-274">You can only see hello Tomcat default page from hello local host.</span></span> <span data-ttu-id="f38fa-275">Merhaba sorunudur büyük olasılıkla kulak tooby Tomcat olan, başlangıç bağlantı noktası hello güvenlik duvarı tarafından engellenir.</span><span class="sxs-lookup"><span data-stu-id="f38fa-275">hello problem is most likely that hello port, which is listened tooby Tomcat, is blocked by hello firewall.</span></span> <span data-ttu-id="f38fa-276">Merhaba w3m aracı toobrowse hello Web sayfasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f38fa-276">You can use hello w3m tool toobrowse hello webpage.</span></span> <span data-ttu-id="f38fa-277">Merhaba aşağıdaki komutları w3m yükleyin ve toohello Tomcat varsayılan sayfasına göz atın:</span><span class="sxs-lookup"><span data-stu-id="f38fa-277">hello following commands install w3m and browse toohello Tomcat default page:</span></span>  


        <span data-ttu-id="f38fa-278">sudo yum yükleme w3m w3m-img</span><span class="sxs-lookup"><span data-stu-id="f38fa-278">sudo yum  install w3m w3m-img</span></span>


        <span data-ttu-id="f38fa-279">w3m http://localhost: 8080</span><span class="sxs-lookup"><span data-stu-id="f38fa-279">w3m http://localhost:8080</span></span>  
#### <a name="solution"></a><span data-ttu-id="f38fa-280">Çözüm</span><span class="sxs-lookup"><span data-stu-id="f38fa-280">Solution</span></span>

  * <span data-ttu-id="f38fa-281">Merhaba Tomcat dinleme bağlantı noktası hello değil, aynı hello hello uç noktasının trafiği toohello sanal makine için özel bağlantı noktası olarak hello özel bağlantı noktası değiştirmek toobe hello Tomcat dinleme bağlantı noktası hello aynı.</span><span class="sxs-lookup"><span data-stu-id="f38fa-281">If hello Tomcat listen port is not hello same as hello private port of hello endpoint for traffic toohello virtual machine, you need change hello private port toobe hello same as hello Tomcat listen port.</span></span>   
  2. <span data-ttu-id="f38fa-282">Güvenlik Duvarı/iptables tarafından Hello sorunu neden olursa, aşağıdaki satırları çok/etc/sysconfig/iptables hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f38fa-282">If hello issue is caused by firewall/iptables, add hello following lines too/etc/sysconfig/iptables.</span></span> <span data-ttu-id="f38fa-283">Merhaba ikinci satır yalnızca https trafiği için gereklidir:</span><span class="sxs-lookup"><span data-stu-id="f38fa-283">hello second line is only needed for https traffic:</span></span>  

      <span data-ttu-id="f38fa-284">-A -p tcp -m tcp--dport 80 -j kabul giriş</span><span class="sxs-lookup"><span data-stu-id="f38fa-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span></span>

      <span data-ttu-id="f38fa-285">-A -p tcp -m tcp--dport 443 -j kabul giriş</span><span class="sxs-lookup"><span data-stu-id="f38fa-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span></span>  

     > [!IMPORTANT]
     > <span data-ttu-id="f38fa-286">Merhaba önceki satırları hello aşağıdaki gibi erişim genel kısıtlar satırları yukarıda konumlandırıldığı emin olun: - bir giriş -j--Reddet-with ICMP konak yasaklanmış REDDET</span><span class="sxs-lookup"><span data-stu-id="f38fa-286">Make sure hello previous lines are positioned above any lines that would globally restrict access, such as hello following: -A INPUT -j REJECT --reject-with icmp-host-prohibited</span></span>



<span data-ttu-id="f38fa-287">tooreload hello iptables, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f38fa-287">tooreload hello iptables, run hello following command:</span></span>

    service iptables restart

<span data-ttu-id="f38fa-288">Bu CentOS 6.3 test edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f38fa-288">This has been tested on CentOS 6.3.</span></span>

### <a name="permission-denied-when-you-upload-project-files-toovarlibtomcat7webapps"></a><span data-ttu-id="f38fa-289">Proje yüklediğinizde reddedildi dosyaları çok/var/lib/tomcat7'yi / webapps /</span><span class="sxs-lookup"><span data-stu-id="f38fa-289">Permission denied when you upload project files too/var/lib/tomcat7/webapps/</span></span>
#### <a name="symptom"></a><span data-ttu-id="f38fa-290">Belirti</span><span class="sxs-lookup"><span data-stu-id="f38fa-290">Symptom</span></span>
  <span data-ttu-id="f38fa-291">Ne zaman bir SFTP (örneğin, FileZilla) istemci tooconnect tooyour sanal makine kullanmanız ve çok/var/lib/tomcat7'yi / webapps gidin/toopublish, sitenizi bir hata iletisi benzer toohello aşağıdaki alın:</span><span class="sxs-lookup"><span data-stu-id="f38fa-291">When you use an SFTP client (such as FileZilla) tooconnect tooyour virtual machine and navigate too/var/lib/tomcat7/webapps/ toopublish your site, you get an error message similar toohello following:</span></span>  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a><span data-ttu-id="f38fa-292">Olası temel nedeni</span><span class="sxs-lookup"><span data-stu-id="f38fa-292">Possible root cause</span></span>
  <span data-ttu-id="f38fa-293">Hiçbir izinleri tooaccess hello /var/lib/tomcat7/webapps klasör sahip.</span><span class="sxs-lookup"><span data-stu-id="f38fa-293">You have no permissions tooaccess hello /var/lib/tomcat7/webapps folder.</span></span>  
#### <a name="solution"></a><span data-ttu-id="f38fa-294">Çözüm</span><span class="sxs-lookup"><span data-stu-id="f38fa-294">Solution</span></span>  
  <span data-ttu-id="f38fa-295">Merhaba kök hesap tooget izni gerekir.</span><span class="sxs-lookup"><span data-stu-id="f38fa-295">You need tooget permission from hello root account.</span></span> <span data-ttu-id="f38fa-296">Bu klasör hello sahipliğini hello makine sağladığında, kullanılan kök toohello kullanıcı adından değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f38fa-296">You can change hello ownership of that folder from root toohello username you used when you provisioned hello machine.</span></span> <span data-ttu-id="f38fa-297">Merhaba azureuser hesap adı ile örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f38fa-297">Here is an example with hello azureuser account name:</span></span>  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  <span data-ttu-id="f38fa-298">Merhaba -R seçeneği tooapply hello izinleri çok bir dizin içinde tüm dosyalar için kullanın.</span><span class="sxs-lookup"><span data-stu-id="f38fa-298">Use hello -R option tooapply hello permissions for all files inside of a directory too.</span></span>  

  <span data-ttu-id="f38fa-299">Bu komut, dizinler için de çalışır.</span><span class="sxs-lookup"><span data-stu-id="f38fa-299">This command also works for directories.</span></span> <span data-ttu-id="f38fa-300">Merhaba -R seçeneği değişiklikleri tüm dosyaları ve dizinleri hello dizin içinde izinlerini hello.</span><span class="sxs-lookup"><span data-stu-id="f38fa-300">hello -R option changes hello permissions for all files and directories inside hello directory.</span></span> <span data-ttu-id="f38fa-301">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f38fa-301">Here is an example:</span></span>  

     sudo chown -R username:group directory  

  <span data-ttu-id="f38fa-302">Bu komut, tüm dosyaları ve hello dizini içinde olan dizinleri (kullanıcı ve grup) sahipliği değiştirir.</span><span class="sxs-lookup"><span data-stu-id="f38fa-302">This command changes ownership (both user and group) for all files and directories that are inside hello directory.</span></span>  

  <span data-ttu-id="f38fa-303">Merhaba aşağıdaki komut yalnızca hello izni hello klasörü dizininin değiştirir.</span><span class="sxs-lookup"><span data-stu-id="f38fa-303">hello following command only changes hello permission of hello folder directory.</span></span> <span data-ttu-id="f38fa-304">Merhaba dosya ve klasörleri hello dizin içinde değiştirilmez.</span><span class="sxs-lookup"><span data-stu-id="f38fa-304">hello files and folders inside hello directory are not changed.</span></span>  

     sudo chown username:group directory

[1]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-01.png
[2]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-02.png
[3]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-03.png
[4]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-04.png
[5]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-05.png
[6]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-06.png
[7]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-07.png
[8]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-08.png
[9]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-09.png
[10]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-10.png
[11]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-11.png
[12]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-12.png
[13]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-13.png
[14]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-14.png
[15]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-15.png
[16]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-16.png
[17]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-17.png
[18]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-18.png
