---
title: "aaaSubmit işleri tooan HPC paketi küme Azure'da | Microsoft Docs"
description: "Bir şirket içi bilgisayar toosubmit yukarı tooset tooan HPC Pack Azure kümesinde nasıl işler öğrenin"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 2918cf633917d8730487152e6a5ddb863eb8bb5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-tooan-hpc-pack-cluster-deployed-in-azure"></a><span data-ttu-id="0db55-103">Azure'da dağıtılan bir kümeden şirket içi bilgisayar tooan HPC Pack HPC iş gönderme</span><span class="sxs-lookup"><span data-stu-id="0db55-103">Submit HPC jobs from an on-premises computer tooan HPC Pack cluster deployed in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="0db55-104">Bir şirket içi istemci bilgisayar toosubmit işleri tooa yapılandırma [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) Azure kümesinde.</span><span class="sxs-lookup"><span data-stu-id="0db55-104">Configure an on-premises client computer toosubmit jobs tooa [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure.</span></span> <span data-ttu-id="0db55-105">Bu makalede, nasıl Azure toohello kümede HTTPS üzerinden toosubmit iş tooset yerel bir bilgisayar istemcisi ile araçları gösterir.</span><span class="sxs-lookup"><span data-stu-id="0db55-105">This article shows you how tooset up a local computer with client tools toosubmit job over HTTPS toohello cluster in Azure.</span></span> <span data-ttu-id="0db55-106">Bu şekilde, işleri tooa bulut tabanlı HPC paketi küme, birden çok küme kullanıcı gönderebilirsiniz ancak toohello üstbilgi düğüm VM'ine doğrudan bağlanma veya bir Azure aboneliği erişme.</span><span class="sxs-lookup"><span data-stu-id="0db55-106">In this way, several cluster users can submit jobs tooa cloud-based HPC Pack cluster, but without connecting directly toohello head node VM or accessing an Azure subscription.</span></span>

![Azure iş tooa kümede gönderme][jobsubmit]

## <a name="prerequisites"></a><span data-ttu-id="0db55-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0db55-108">Prerequisites</span></span>
* <span data-ttu-id="0db55-109">**Bir Azure VM dağıtılan HPC paketi üstbilgi düğümü** -otomatik araçları gibi kullanmanızı öneririz bir [Azure Hızlı Başlangıç şablonu](https://azure.microsoft.com/documentation/templates/) veya bir [Azure PowerShell Betiği](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toodeploy hello baş düğüm ve Küme.</span><span class="sxs-lookup"><span data-stu-id="0db55-109">**HPC Pack head node deployed in an Azure VM** - We recommend that you use automated tools such as an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/) or an [Azure PowerShell script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toodeploy hello head node and cluster.</span></span> <span data-ttu-id="0db55-110">Hello DNS ad hello baş düğümü ve bu makaledeki hello adımları tamamlamak için bir Küme Yöneticisi kimlik bilgilerini hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="0db55-110">You need hello DNS name of hello head node and hello credentials of a cluster administrator to complete hello steps in this article.</span></span>
* <span data-ttu-id="0db55-111">**İstemci bilgisayar** -HPC Pack istemci yardımcı programları çalıştırmak bir Windows veya Windows Server istemci bilgisayar gerekir (bkz [sistem gereksinimleri](https://technet.microsoft.com/library/dn535781.aspx)).</span><span class="sxs-lookup"><span data-stu-id="0db55-111">**Client computer** - You need a Windows or Windows Server client computer that can run HPC Pack client utilities (see [system requirements](https://technet.microsoft.com/library/dn535781.aspx)).</span></span> <span data-ttu-id="0db55-112">Yalnızca toouse hello HPC paketi web portalı veya REST API toosubmit işleri istiyorsanız, tercih ettiğiniz herhangi bir istemci bilgisayarı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0db55-112">If you only want toouse hello HPC Pack web portal or REST API toosubmit jobs, you can use any client computer of your choice.</span></span>
* <span data-ttu-id="0db55-113">**HPC Pack yükleme medyasını** -tooinstall hello HPC Pack istemci yardımcı programları ' hello ücretsiz yükleme paketinin en son sürümünü HPC Pack (HPC Pack 2012 R2) kullanılabilir için [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="0db55-113">**HPC Pack installation media** - tooinstall hello HPC Pack client utilities, hello free installation package for the latest version of HPC Pack (HPC Pack 2012 R2) is available from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="0db55-114">Merhaba yüklediğinizden emin olun hello baş düğümünde VM yüklü HPC Pack aynı sürümü.</span><span class="sxs-lookup"><span data-stu-id="0db55-114">Make sure that you download hello same version of HPC Pack that is installed on hello head node VM.</span></span>

## <a name="step-1-install-and-configure-hello-web-components-on-hello-head-node"></a><span data-ttu-id="0db55-115">1. adım: Yükleme ve hello baş düğümünde hello web bileşenleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0db55-115">Step 1: Install and configure hello web components on hello head node</span></span>
<span data-ttu-id="0db55-116">tooenable, HTTPS üzerinden REST arabirimi toosubmit işleri toohello küme hello HPC paketi web bileşenleri hello HPC paketi üstbilgi düğümü üzerinde yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="0db55-116">tooenable a REST interface toosubmit jobs toohello cluster over HTTPS, ensure that hello HPC Pack web components are configured on hello HPC Pack head node.</span></span> <span data-ttu-id="0db55-117">Bunlar zaten yüklü değilse, ilk hello HpcWebComponents.msi yükleme dosyasını çalıştırarak hello web bileşenlerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0db55-117">If they aren't already installed, first install hello web components by running hello HpcWebComponents.msi installation file.</span></span> <span data-ttu-id="0db55-118">Ardından, hello HPC PowerShell betiğini çalıştırarak hello bileşenlerini yapılandırma **kümesi HPCWebComponents.ps1**.</span><span class="sxs-lookup"><span data-stu-id="0db55-118">Then, configure hello components by running hello HPC PowerShell script **Set-HPCWebComponents.ps1**.</span></span>

<span data-ttu-id="0db55-119">Ayrıntılı yordamlar için bkz: [yükleme hello Microsoft HPC Pack Web Bileşenleri](http://technet.microsoft.com/library/hh314627.aspx).</span><span class="sxs-lookup"><span data-stu-id="0db55-119">For detailed procedures, see [Install hello Microsoft HPC Pack Web Components](http://technet.microsoft.com/library/hh314627.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="0db55-120">HPC Pack için belirli Azure hızlı başlangıç şablonlarını yükleyin ve hello web bileşenleri otomatik olarak yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0db55-120">Certain Azure quickstart templates for HPC Pack install and configure hello web components automatically.</span></span> <span data-ttu-id="0db55-121">Merhaba kullanırsanız [HPC Pack Iaas dağıtım betiği](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate hello küme, isteğe bağlı olarak yükleyebilir ve hello web bileşenleri hello dağıtımının bir parçası yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0db55-121">If you use hello [HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate hello cluster, you can optionally install and configure hello web components as part of hello deployment.</span></span>
> 
> 

<span data-ttu-id="0db55-122">**tooinstall hello web bileşenleri**</span><span class="sxs-lookup"><span data-stu-id="0db55-122">**tooinstall hello web components**</span></span>

1. <span data-ttu-id="0db55-123">Toohello üstbilgi düğüm VM'ine hello bir Küme Yöneticisi kimlik bilgilerini kullanarak bağlanın.</span><span class="sxs-lookup"><span data-stu-id="0db55-123">Connect toohello head node VM by using hello credentials of a cluster administrator.</span></span>
2. <span data-ttu-id="0db55-124">Merhaba HPC Pack kurulum klasöründen HpcWebComponents.msi hello baş düğümünde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0db55-124">From hello HPC Pack Setup folder, run HpcWebComponents.msi on hello head node.</span></span>
3. <span data-ttu-id="0db55-125">Merhaba Sihirbazı tooinstall hello web bileşenleri Hello adımları izleyin</span><span class="sxs-lookup"><span data-stu-id="0db55-125">Follow hello steps in hello wizard tooinstall hello web components</span></span>

<span data-ttu-id="0db55-126">**tooconfigure hello web bileşenleri**</span><span class="sxs-lookup"><span data-stu-id="0db55-126">**tooconfigure hello web components**</span></span>

1. <span data-ttu-id="0db55-127">Merhaba baş düğümünde HPC PowerShell'i yönetici olarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="0db55-127">On hello head node, start HPC PowerShell as an administrator.</span></span>
2. <span data-ttu-id="0db55-128">toochange dizin toohello konumu hello yapılandırma komut dosyası, komut aşağıdaki türü hello:</span><span class="sxs-lookup"><span data-stu-id="0db55-128">toochange directory toohello location of hello configuration script, type hello following command:</span></span>
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. <span data-ttu-id="0db55-129">tooconfigure REST arabirimi hello ve hello HPC Web hizmeti, komutu aşağıdaki türü hello başlatın:</span><span class="sxs-lookup"><span data-stu-id="0db55-129">tooconfigure hello REST interface and start hello HPC Web Service, type hello following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. <span data-ttu-id="0db55-130">İstendiğinde tooselect bir sertifika hello sertifika seçtiğinizde, toohello Genel DNS adı hello baş düğümü karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="0db55-130">When prompted tooselect a certificate, choose hello certificate that corresponds toohello public DNS name of hello head node.</span></span> <span data-ttu-id="0db55-131">Örneğin, hello baş düğüm hello Klasik dağıtım modeli, hello sertifika adını kullanarak VM CN gibi görünüyor dağıtırsanız =&lt;*HeadNodeDnsName*&gt;. cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="0db55-131">For example, if you deploy hello head node VM using hello classic deployment model, hello certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net.</span></span> <span data-ttu-id="0db55-132">Merhaba Resource Manager dağıtım modeli kullanırsanız hello sertifika adı CN gibi görünüyor =&lt;*HeadNodeDnsName*&gt;.&lt; *bölge*&gt;. cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="0db55-132">If you use hello Resource Manager deployment model, hello certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.&lt;*region*&gt;.cloudapp.azure.com.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0db55-133">Bir şirket içi bilgisayardan toohello baş düğüm işleri gönderdiğinizde, bu sertifika daha sonra seçin.</span><span class="sxs-lookup"><span data-stu-id="0db55-133">You select this certificate later when you submit jobs toohello head node from an on-premises computer.</span></span> <span data-ttu-id="0db55-134">Verme seçin veya hello baş düğümü hello Active Directory etki alanındaki toohello bilgisayar adına karşılık gelen bir sertifika yapılandırın (örneğin, CN =*MyHPCHeadNode.HpcAzure.local*).</span><span class="sxs-lookup"><span data-stu-id="0db55-134">Don't select or configure a certificate that corresponds toohello computer name of hello head node in hello Active Directory domain (for example, CN=*MyHPCHeadNode.HpcAzure.local*).</span></span>
   > 
   > 
5. <span data-ttu-id="0db55-135">İş gönderme, komutu aşağıdaki türü hello için tooconfigure hello web portalı:</span><span class="sxs-lookup"><span data-stu-id="0db55-135">tooconfigure hello web portal for job submission, type hello following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. <span data-ttu-id="0db55-136">Merhaba betik tamamlandıktan sonra durdurmak ve komutları aşağıdaki hello yazarak hello HPC İş Zamanlayıcısı hizmeti yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="0db55-136">After hello script completes, stop and restart hello HPC Job Scheduler Service by typing hello following commands:</span></span>
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-hello-hpc-pack-client-utilities-on-an-on-premises-computer"></a><span data-ttu-id="0db55-137">2. adım: bir şirket içi bilgisayar hello HPC Pack istemci yardımcı programları yükle</span><span class="sxs-lookup"><span data-stu-id="0db55-137">Step 2: Install hello HPC Pack client utilities on an on-premises computer</span></span>
<span data-ttu-id="0db55-138">Tooinstall hello HPC Pack istemci yardımcı programları istiyorsanız, HPC paketi Kurulum dosyaları (tam yükleme) hello karşıdan [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="0db55-138">If you want tooinstall hello HPC Pack client utilities on your computer, download the HPC Pack setup files (full installation) from hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="0db55-139">Merhaba yükleme başladığınızda, hello Kurulum hello için seçeneği **HPC Pack istemci yardımcı programları**.</span><span class="sxs-lookup"><span data-stu-id="0db55-139">When you begin hello installation, choose hello setup option for hello **HPC Pack client utilities**.</span></span>

<span data-ttu-id="0db55-140">toosubmit işleri toohello üstbilgi düğüm VM'ine toouse hello HPC Pack istemcisi araçları, ayrıca tooexport hello baş düğümünden bir sertifika gerekir ve hello istemci bilgisayara yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0db55-140">toouse hello HPC Pack client tools toosubmit jobs toohello head node VM, you also need tooexport a certificate from hello head node and install it on hello client computer.</span></span> <span data-ttu-id="0db55-141">Merhaba sertifika olması gerekir. CER biçimi.</span><span class="sxs-lookup"><span data-stu-id="0db55-141">hello certificate must be in .CER format.</span></span>

<span data-ttu-id="0db55-142">**Merhaba baş düğümünden tooexport hello sertifika**</span><span class="sxs-lookup"><span data-stu-id="0db55-142">**tooexport hello certificate from hello head node**</span></span>

1. <span data-ttu-id="0db55-143">Merhaba baş düğümünde hello Sertifikalar ek bileşenini tooa Microsoft Yönetim Konsolu için hello yerel bilgisayar hesabı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0db55-143">On hello head node, add hello Certificates snap-in tooa Microsoft Management Console for hello Local Computer account.</span></span> <span data-ttu-id="0db55-144">Tooadd hello ek bileşenini adımlar için bkz: [Sertifikalar ek bileşenini tooan hello MMC eklemek](https://technet.microsoft.com/library/cc754431.aspx).</span><span class="sxs-lookup"><span data-stu-id="0db55-144">For steps tooadd hello snap-in, see [Add hello Certificates Snap-in tooan MMC](https://technet.microsoft.com/library/cc754431.aspx).</span></span>
2. <span data-ttu-id="0db55-145">Merhaba konsol ağacında **sertifikalar – yerel bilgisayar** > **kişisel**ve ardından **Sertifikalar**.</span><span class="sxs-lookup"><span data-stu-id="0db55-145">In hello console tree, expand **Certificates – Local Computer** > **Personal**, and then click **Certificates**.</span></span>
3. <span data-ttu-id="0db55-146">Merhaba HPC paketi web bileşenleri için yapılandırılmış hello sertifikayı bulun [1. adım: yükleme ve hello baş düğümünde hello web bileşenleri yapılandırma](#step-1:-install-and-configure-the-web-components-on-the-head-node) (örneğin, CN =&lt;*HeadNodeDnsName* &gt;. cloudapp.net).</span><span class="sxs-lookup"><span data-stu-id="0db55-146">Locate hello certificate that you configured for hello HPC Pack web components in [Step 1: Install and configure hello web components on hello head node](#step-1:-install-and-configure-the-web-components-on-the-head-node) (for example, CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net).</span></span>
4. <span data-ttu-id="0db55-147">Merhaba sertifikayı sağ tıklatın ve **tüm görevler** > **verme**.</span><span class="sxs-lookup"><span data-stu-id="0db55-147">Right-click hello certificate, and click **All Tasks** > **Export**.</span></span>
5. <span data-ttu-id="0db55-148">Hello Sertifika Verme Sihirbazı'nı tıklatın **sonraki**ve emin **Hayır, hello özel anahtarı verme** seçilir.</span><span class="sxs-lookup"><span data-stu-id="0db55-148">In hello Certificate Export Wizard, click **Next**, and ensure that **No, do not export hello private key** is selected.</span></span>
6. <span data-ttu-id="0db55-149">Merhaba Sihirbazı tooexport hello DER sertifikada adımlardan kalan izleyin hello ile kodlanmış ikili X.509 (. CER) biçimi.</span><span class="sxs-lookup"><span data-stu-id="0db55-149">Follow hello remaining steps of hello wizard tooexport hello certificate in DER encoded binary X.509 (.CER) format.</span></span>

<span data-ttu-id="0db55-150">**Merhaba istemci bilgisayarda tooimport hello sertifika**</span><span class="sxs-lookup"><span data-stu-id="0db55-150">**tooimport hello certificate on hello client computer**</span></span>

1. <span data-ttu-id="0db55-151">Merhaba istemci bilgisayarda hello baş düğüm tooa klasöründen dışarı hello sertifika kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0db55-151">Copy hello certificate that you exported from hello head node tooa folder on hello client computer.</span></span>
2. <span data-ttu-id="0db55-152">Merhaba istemci bilgisayarda certmgr.msc çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0db55-152">On hello client computer, run certmgr.msc.</span></span>
3. <span data-ttu-id="0db55-153">Sertifika Yöneticisi'nde **Sertifikalar – Geçerli kullanıcı** > **güvenilen kök sertifika yetkilileri**, sağ **sertifikaları**ve ardından tıklatın **tüm görevler** > **alma**.</span><span class="sxs-lookup"><span data-stu-id="0db55-153">In Certificate Manager, expand **Certificates – Current user** > **Trusted Root Certification Authorities**, right-click **Certificates**, and then click **All Tasks** > **Import**.</span></span>
4. <span data-ttu-id="0db55-154">Hello Sertifika Alma Sihirbazı'nı tıklatın **sonraki** ve dışarı aktardığınız güvenilen kök sertifika yetkilileri deposuna hello baş düğüm toohello izleyin hello adımları tooimport hello sertifikası.</span><span class="sxs-lookup"><span data-stu-id="0db55-154">In hello Certificate Import Wizard, click **Next** and follow hello steps tooimport hello certificate that you exported from hello head node toohello Trusted Root Certification Authorities store.</span></span>

> [!TIP]
> <span data-ttu-id="0db55-155">Merhaba baş düğümüne sertifika yetkilisinde Hello hello istemci bilgisayar tarafından tanınmadığından bir güvenlik uyarısı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0db55-155">You might see a security warning, because hello certification authority on hello head node isn't recognized by hello client computer.</span></span> <span data-ttu-id="0db55-156">Test amacıyla, bu uyarı ve tam hello sertifika alma yoksayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0db55-156">For testing purposes, you can ignore this warning and complete hello certificate import.</span></span>
> 
> 

## <a name="step-3-run-test-jobs-on-hello-cluster"></a><span data-ttu-id="0db55-157">3. adım: Çalıştır test işleri hello kümede</span><span class="sxs-lookup"><span data-stu-id="0db55-157">Step 3: Run test jobs on hello cluster</span></span>
<span data-ttu-id="0db55-158">Merhaba üzerinde çalışan işleri deneyin yapılandırmanızı küme Azure'da hello tooverify bilgisayar şirket içi.</span><span class="sxs-lookup"><span data-stu-id="0db55-158">tooverify your configuration, try running jobs on hello cluster in Azure from hello on-premises computer.</span></span> <span data-ttu-id="0db55-159">Örneğin, HPC Pack GUI araçları veya komut satırı komutlarını toosubmit işleri toohello küme kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0db55-159">For example, you can use HPC Pack GUI tools or command-line commands toosubmit jobs toohello cluster.</span></span> <span data-ttu-id="0db55-160">Bir web tabanlı portal toosubmit işleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0db55-160">You can also use a web-based portal toosubmit jobs.</span></span>

<span data-ttu-id="0db55-161">**Merhaba istemci bilgisayarda toorun iş gönderme komutları**</span><span class="sxs-lookup"><span data-stu-id="0db55-161">**toorun job submission commands on hello client computer**</span></span>

1. <span data-ttu-id="0db55-162">Merhaba HPC Pack istemci yardımcı programları yüklü olduğu bir istemci bilgisayarda bir komut istemi başlatın.</span><span class="sxs-lookup"><span data-stu-id="0db55-162">On a client computer where hello HPC Pack client utilities are installed, start a Command Prompt.</span></span>
2. <span data-ttu-id="0db55-163">Bir örnek komutu yazın.</span><span class="sxs-lookup"><span data-stu-id="0db55-163">Type a sample command.</span></span> <span data-ttu-id="0db55-164">Örneğin, toolist hello küme üzerindeki tüm işleri yazın komutu benzer tooone, hello tam DNS adı hello baş düğümü bağlı olarak aşağıdaki hello olarak:</span><span class="sxs-lookup"><span data-stu-id="0db55-164">For example, toolist all jobs on hello cluster, type a command similar tooone of hello following, depending on hello full DNS name of hello head node:</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    <span data-ttu-id="0db55-165">or</span><span class="sxs-lookup"><span data-stu-id="0db55-165">or</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > <span data-ttu-id="0db55-166">Merhaba Zamanlayıcı URL'de Hello hello baş düğüm, başlangıç IP adresi değil, tam DNS adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="0db55-166">Use hello full DNS name of hello head node, not hello IP address, in hello scheduler URL.</span></span> <span data-ttu-id="0db55-167">Başlangıç IP adresi belirtirseniz, bir hata çok benzer görünür "Merhaba sunucu sertifikası tooeither gereken güven veya hello güvenilir kök deposuna yerleştirilen toobe geçerli zincirine sahip."</span><span class="sxs-lookup"><span data-stu-id="0db55-167">If you specify hello IP address, an error appears similar too"hello server certificate needs tooeither have a valid chain of trust or toobe placed in hello trusted root store."</span></span>
   > 
   > 
3. <span data-ttu-id="0db55-168">İstendiğinde, hello kullanıcı adını yazın (hello formunda &lt;DomainName&gt;\\&lt;kullanıcı adı&gt;) ve hello HPC Küme Yöneticisi ya da yapılandırdığınız başka bir küme kullanıcının parolası.</span><span class="sxs-lookup"><span data-stu-id="0db55-168">When prompted, type hello user name (in hello form &lt;DomainName&gt;\\&lt;UserName&gt;) and password of hello HPC cluster administrator or another cluster user that you configured.</span></span> <span data-ttu-id="0db55-169">Merhaba kimlik bilgileri yerel olarak daha fazla iş işlemlerini toostore seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0db55-169">You can choose toostore hello credentials locally for more job operations.</span></span>
   
    <span data-ttu-id="0db55-170">İşlerini listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0db55-170">A list of jobs appears.</span></span>

<span data-ttu-id="0db55-171">**Merhaba istemci bilgisayarda toouse HPC İş Yöneticisi**</span><span class="sxs-lookup"><span data-stu-id="0db55-171">**toouse HPC Job Manager on hello client computer**</span></span>

1. <span data-ttu-id="0db55-172">Daha önce bir küme kullanıcının etki alanı kimlik bilgilerini bir işi gönderirken depoladığınız alamadık, kimlik bilgileri Yöneticisi'nde hello kimlik bilgileri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0db55-172">If you didn't previously store domain credentials for a cluster user when submitting a job, you can add hello credentials in Credential Manager.</span></span>
   
    <span data-ttu-id="0db55-173">a.</span><span class="sxs-lookup"><span data-stu-id="0db55-173">a.</span></span> <span data-ttu-id="0db55-174">Merhaba istemci bilgisayardaki Denetim Masası'ndaki kimlik bilgisi Yöneticisi'ni başlatın.</span><span class="sxs-lookup"><span data-stu-id="0db55-174">In Control Panel on hello client computer, start Credential Manager.</span></span>
   
    <span data-ttu-id="0db55-175">b.</span><span class="sxs-lookup"><span data-stu-id="0db55-175">b.</span></span> <span data-ttu-id="0db55-176">Tıklatın **Windows kimlik bilgileri** > **genel bir kimlik bilgisi Ekle**.</span><span class="sxs-lookup"><span data-stu-id="0db55-176">Click **Windows Credentials** > **Add a generic credential**.</span></span>
   
    <span data-ttu-id="0db55-177">c.</span><span class="sxs-lookup"><span data-stu-id="0db55-177">c.</span></span> <span data-ttu-id="0db55-178">Merhaba Internet adresi belirtin (örneğin, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler veya https://&lt;HeadNodeDnsName&gt;.&lt; Bölge&gt;.cloudapp.azure.com/HpcScheduler) ve hello kullanıcı adı (&lt;DomainName&gt;\\&lt;kullanıcıadı&gt;) ve hello Küme Yöneticisi veya başka bir parola yapılandırdığınız küme kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="0db55-178">Specify hello Internet address (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com/HpcScheduler), and hello user name (&lt;DomainName&gt;\\&lt;UserName&gt;) and password of hello cluster administrator or another cluster user that you configured.</span></span>
2. <span data-ttu-id="0db55-179">Merhaba istemci bilgisayarda, HPC İş Yöneticisi'ni başlatın.</span><span class="sxs-lookup"><span data-stu-id="0db55-179">On hello client computer, start HPC Job Manager.</span></span>
3. <span data-ttu-id="0db55-180">Merhaba, **baş düğüm Seç** iletişim kutusu, türü hello URL toohello baş düğümünde Azure (örneğin, https://&lt;HeadNodeDnsName&gt;. cloudapp.net veya https://&lt;HeadNodeDnsName&gt;. &lt;bölge&gt;. cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0db55-180">In hello **Select Head Node** dialog box, type hello URL toohello head node in Azure (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com).</span></span>
   
    <span data-ttu-id="0db55-181">HPC İş Yöneticisi'ni açar ve hello baş düğümünde işlerin bir listesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="0db55-181">HPC Job Manager opens and shows a list of jobs on hello head node.</span></span>

<span data-ttu-id="0db55-182">**Merhaba baş düğüm üzerinde çalışan toouse hello web portalı**</span><span class="sxs-lookup"><span data-stu-id="0db55-182">**toouse hello web portal running on hello head node**</span></span>

1. <span data-ttu-id="0db55-183">Merhaba istemci bilgisayarda bir web tarayıcı başlatmak ve adresleri hello tam DNS adı hello baş düğümü bağlı olarak aşağıdaki hello birini girin:</span><span class="sxs-lookup"><span data-stu-id="0db55-183">Start a web browser on hello client computer, and enter one of hello following addresses, depending on hello full DNS name of hello head node:</span></span>
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    <span data-ttu-id="0db55-184">or</span><span class="sxs-lookup"><span data-stu-id="0db55-184">or</span></span>
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. <span data-ttu-id="0db55-185">Görüntülenen hello güvenlik iletişim kutusunda, hello HPC Küme Yöneticisi hello etki alanı kimlik bilgilerini yazın.</span><span class="sxs-lookup"><span data-stu-id="0db55-185">In hello security dialog box that appears, type hello domain credentials of hello HPC cluster administrator.</span></span> <span data-ttu-id="0db55-186">(Diğer küme kullanıcılar da farklı rolleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0db55-186">(You can also add other cluster users in different roles.</span></span> <span data-ttu-id="0db55-187">Bkz: [küme kullanıcıları yönetme](https://technet.microsoft.com/library/ff919335.aspx).)</span><span class="sxs-lookup"><span data-stu-id="0db55-187">See [Managing Cluster Users](https://technet.microsoft.com/library/ff919335.aspx).)</span></span>
   
    <span data-ttu-id="0db55-188">Merhaba web portalı toohello iş liste görünümü açılır.</span><span class="sxs-lookup"><span data-stu-id="0db55-188">hello web portal opens toohello job list view.</span></span>
3. <span data-ttu-id="0db55-189">"Hello World" Merhaba kümeden hello dizesi döndüren bir örnek iş toosubmit tıklatın **yeni iş** hello sol gezinti içinde.</span><span class="sxs-lookup"><span data-stu-id="0db55-189">toosubmit a sample job that returns hello string “Hello World” from hello cluster, click **New job** in hello left-hand navigation.</span></span>
4. <span data-ttu-id="0db55-190">Merhaba üzerinde **yeni iş** sayfasında **gönderme sayfalarından**, tıklatın **HelloWorld**.</span><span class="sxs-lookup"><span data-stu-id="0db55-190">On hello **New Job** page, under **From submission pages**, click **HelloWorld**.</span></span> <span data-ttu-id="0db55-191">Merhaba iş gönderme sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0db55-191">hello job submission page appears.</span></span>
5. <span data-ttu-id="0db55-192">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="0db55-192">Click **Submit**.</span></span> <span data-ttu-id="0db55-193">İstenirse, hello HPC Küme Yöneticisi hello etki alanı kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="0db55-193">If prompted, provide hello domain credentials of hello HPC cluster administrator.</span></span> <span data-ttu-id="0db55-194">Merhaba iş gönderildi ve hello iş kimliği üzerinde hello görünür **İşlerim** sayfası.</span><span class="sxs-lookup"><span data-stu-id="0db55-194">hello job is submitted, and hello job ID appears on hello **My Jobs** page.</span></span>
6. <span data-ttu-id="0db55-195">gönderdiğiniz, hello iş tooview hello sonuçlarını hello iş kimliği'ni tıklatın ve ardından **görünümü görevleri** tooview hello komut çıktısı (altında **çıkış**).</span><span class="sxs-lookup"><span data-stu-id="0db55-195">tooview hello results of hello job that you submitted, click hello job ID, and then click **View Tasks** tooview hello command output (under **Output**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0db55-196">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0db55-196">Next steps</span></span>
* <span data-ttu-id="0db55-197">İşlerini toohello hello Azure kümeyle gönderebilmek için [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="0db55-197">You can also submit jobs toohello Azure cluster with hello [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span>
* <span data-ttu-id="0db55-198">Bir Linux istemciden toosubmit küme işleri istiyorsanız hello Python bakın hello örnek [HPC Pack 2012 R2 SDK'sı ve örnek kod](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="0db55-198">If you want toosubmit cluster jobs from a Linux client, see hello Python sample in hello [HPC Pack 2012 R2 SDK and Sample Code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span>

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
