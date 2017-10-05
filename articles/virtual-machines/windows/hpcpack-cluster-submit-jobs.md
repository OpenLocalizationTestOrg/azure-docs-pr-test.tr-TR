---
title: "HPC Pack işlerini küme Azure'da gönderme | Microsoft Docs"
description: "Azure'da bir HPC Pack kümeye iş göndermek için bir şirket içi bilgisayarı ayarlama öğrenin"
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
ms.openlocfilehash: d5953f1e1dd2deb4d871bd67352a6a5b2ae13dbf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-to-an-hpc-pack-cluster-deployed-in-azure"></a><span data-ttu-id="07f92-103">Şirket içindeki bir bilgisayardan Azure’da dağıtılmış bir HPC Pack kümesine HPC işleri gönderme</span><span class="sxs-lookup"><span data-stu-id="07f92-103">Submit HPC jobs from an on-premises computer to an HPC Pack cluster deployed in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="07f92-104">İşlerini göndermek için bir şirket içi istemci bilgisayarı yapılandırmak bir [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) Azure kümesinde.</span><span class="sxs-lookup"><span data-stu-id="07f92-104">Configure an on-premises client computer to submit jobs to a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure.</span></span> <span data-ttu-id="07f92-105">Bu makalede bir yerel bilgisayarda istemci araçları ile azure'da kümeye HTTPS üzerinden işi göndermek için nasıl ayarlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="07f92-105">This article shows you how to set up a local computer with client tools to submit job over HTTPS to the cluster in Azure.</span></span> <span data-ttu-id="07f92-106">Bu şekilde, birden çok küme kullanıcı işleri bulut tabanlı bir HPC Pack kümeye ancak doğrudan baş düğümüne VM bağlanmak veya bir Azure aboneliği erişme olmadan gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07f92-106">In this way, several cluster users can submit jobs to a cloud-based HPC Pack cluster, but without connecting directly to the head node VM or accessing an Azure subscription.</span></span>

![Azure'da bir küme için bir iş gönderme][jobsubmit]

## <a name="prerequisites"></a><span data-ttu-id="07f92-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="07f92-108">Prerequisites</span></span>
* <span data-ttu-id="07f92-109">**Bir Azure VM dağıtılan HPC paketi üstbilgi düğümü** -otomatik araçları gibi kullanmanızı öneririz bir [Azure Hızlı Başlangıç şablonu](https://azure.microsoft.com/documentation/templates/) veya bir [Azure PowerShell Betiği](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) baş düğümü dağıtma ve Küme.</span><span class="sxs-lookup"><span data-stu-id="07f92-109">**HPC Pack head node deployed in an Azure VM** - We recommend that you use automated tools such as an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/) or an [Azure PowerShell script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to deploy the head node and cluster.</span></span> <span data-ttu-id="07f92-110">Baş düğüm DNS adını ve bu makaledeki adımları tamamlamak için bir Küme Yöneticisi kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="07f92-110">You need the DNS name of the head node and the credentials of a cluster administrator to complete the steps in this article.</span></span>
* <span data-ttu-id="07f92-111">**İstemci bilgisayar** -HPC Pack istemci yardımcı programları çalıştırmak bir Windows veya Windows Server istemci bilgisayar gerekir (bkz [sistem gereksinimleri](https://technet.microsoft.com/library/dn535781.aspx)).</span><span class="sxs-lookup"><span data-stu-id="07f92-111">**Client computer** - You need a Windows or Windows Server client computer that can run HPC Pack client utilities (see [system requirements](https://technet.microsoft.com/library/dn535781.aspx)).</span></span> <span data-ttu-id="07f92-112">Yalnızca iş göndermek için HPC Pack web portalı veya REST API'yi kullanmak istiyorsanız, tercih ettiğiniz herhangi bir istemci bilgisayarı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07f92-112">If you only want to use the HPC Pack web portal or REST API to submit jobs, you can use any client computer of your choice.</span></span>
* <span data-ttu-id="07f92-113">**HPC Pack yükleme medyasını** - HPC Pack (HPC Pack 2012 R2) en son sürümünü kullanılabilir HPC Pack istemci yardımcı programları, ücretsiz yükleme paketini yüklemek için [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="07f92-113">**HPC Pack installation media** - To install the HPC Pack client utilities, the free installation package for the latest version of HPC Pack (HPC Pack 2012 R2) is available from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="07f92-114">VM baş düğümünde yüklü HPC Pack aynı sürümünü yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="07f92-114">Make sure that you download the same version of HPC Pack that is installed on the head node VM.</span></span>

## <a name="step-1-install-and-configure-the-web-components-on-the-head-node"></a><span data-ttu-id="07f92-115">Adım 1: Yükleme ve web bileşenleri baş düğümünde yapılandırın</span><span class="sxs-lookup"><span data-stu-id="07f92-115">Step 1: Install and configure the web components on the head node</span></span>
<span data-ttu-id="07f92-116">HTTPS üzerinden kümeye iş göndermek bir REST arabirimini etkinleştirmek için HPC paketi web bileşenleri HPC paketi üstbilgi düğümü üzerinde yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="07f92-116">To enable a REST interface to submit jobs to the cluster over HTTPS, ensure that the HPC Pack web components are configured on the HPC Pack head node.</span></span> <span data-ttu-id="07f92-117">Bunlar zaten yüklü değilse, ilk HpcWebComponents.msi yükleme dosyasını çalıştırarak web bileşenleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="07f92-117">If they aren't already installed, first install the web components by running the HpcWebComponents.msi installation file.</span></span> <span data-ttu-id="07f92-118">Ardından, HPC PowerShell betiğini çalıştırarak bileşenlerini yapılandırma **kümesi HPCWebComponents.ps1**.</span><span class="sxs-lookup"><span data-stu-id="07f92-118">Then, configure the components by running the HPC PowerShell script **Set-HPCWebComponents.ps1**.</span></span>

<span data-ttu-id="07f92-119">Ayrıntılı yordamlar için bkz: [Microsoft HPC Pack Web bileşenleri yüklemeniz](http://technet.microsoft.com/library/hh314627.aspx).</span><span class="sxs-lookup"><span data-stu-id="07f92-119">For detailed procedures, see [Install the Microsoft HPC Pack Web Components](http://technet.microsoft.com/library/hh314627.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="07f92-120">HPC Pack için belirli Azure hızlı başlangıç şablonlarını yükleyin ve web bileşenleri otomatik olarak yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="07f92-120">Certain Azure quickstart templates for HPC Pack install and configure the web components automatically.</span></span> <span data-ttu-id="07f92-121">Kullanırsanız [HPC Pack Iaas dağıtım betiği](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) küme oluşturmak için isteğe bağlı olarak yükleyebilir ve web bileşenleri dağıtımının bir parçası yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="07f92-121">If you use the [HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to create the cluster, you can optionally install and configure the web components as part of the deployment.</span></span>
> 
> 

<span data-ttu-id="07f92-122">**Web bileşenleri yüklemek için**</span><span class="sxs-lookup"><span data-stu-id="07f92-122">**To install the web components**</span></span>

1. <span data-ttu-id="07f92-123">Baş düğüm VM, bir Küme Yöneticisi kimlik bilgilerini kullanarak bağlanın.</span><span class="sxs-lookup"><span data-stu-id="07f92-123">Connect to the head node VM by using the credentials of a cluster administrator.</span></span>
2. <span data-ttu-id="07f92-124">HPC Pack kurulum klasöründen HpcWebComponents.msi baş düğümünde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="07f92-124">From the HPC Pack Setup folder, run HpcWebComponents.msi on the head node.</span></span>
3. <span data-ttu-id="07f92-125">Web bileşenleri yüklemek için sihirbazdaki adımları izleyin</span><span class="sxs-lookup"><span data-stu-id="07f92-125">Follow the steps in the wizard to install the web components</span></span>

<span data-ttu-id="07f92-126">**Web bileşenleri yapılandırmak için**</span><span class="sxs-lookup"><span data-stu-id="07f92-126">**To configure the web components**</span></span>

1. <span data-ttu-id="07f92-127">Baş düğümünde HPC PowerShell'i yönetici olarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="07f92-127">On the head node, start HPC PowerShell as an administrator.</span></span>
2. <span data-ttu-id="07f92-128">Dizin yapılandırma komut dosyası konumunu değiştirmek için aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="07f92-128">To change directory to the location of the configuration script, type the following command:</span></span>
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. <span data-ttu-id="07f92-129">REST arabirimi yapılandırmak ve HPC Web hizmetini başlatmak için aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="07f92-129">To configure the REST interface and start the HPC Web Service, type the following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. <span data-ttu-id="07f92-130">Bir sertifika seçmeniz istendiğinde baş düğüm ortak DNS adına karşılık gelen sertifika seçin.</span><span class="sxs-lookup"><span data-stu-id="07f92-130">When prompted to select a certificate, choose the certificate that corresponds to the public DNS name of the head node.</span></span> <span data-ttu-id="07f92-131">Baş düğüm Klasik dağıtım modeli kullanarak VM dağıtmak, örneğin, sertifika adı CN gibi durur =&lt;*HeadNodeDnsName*&gt;. cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="07f92-131">For example, if you deploy the head node VM using the classic deployment model, the certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net.</span></span> <span data-ttu-id="07f92-132">Resource Manager dağıtım modeli kullanırsanız, sertifika adı CN gibi görünüyor =&lt;*HeadNodeDnsName*&gt;.&lt; *bölge*&gt;. cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="07f92-132">If you use the Resource Manager deployment model, the certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.&lt;*region*&gt;.cloudapp.azure.com.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="07f92-133">Bir şirket içi bilgisayardan baş düğüme işleri gönderdiğinizde, bu sertifika daha sonra seçin.</span><span class="sxs-lookup"><span data-stu-id="07f92-133">You select this certificate later when you submit jobs to the head node from an on-premises computer.</span></span> <span data-ttu-id="07f92-134">Yok seçin veya Active Directory etki alanındaki baş düğüm bilgisayar adına karşılık gelen bir sertifika yapılandırın (örneğin, CN =*MyHPCHeadNode.HpcAzure.local*).</span><span class="sxs-lookup"><span data-stu-id="07f92-134">Don't select or configure a certificate that corresponds to the computer name of the head node in the Active Directory domain (for example, CN=*MyHPCHeadNode.HpcAzure.local*).</span></span>
   > 
   > 
5. <span data-ttu-id="07f92-135">İş gönderme web portalı yapılandırmak için aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="07f92-135">To configure the web portal for job submission, type the following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. <span data-ttu-id="07f92-136">Betik tamamlandıktan sonra durdurmak ve aşağıdaki komutları yazarak HPC İş Zamanlayıcısı hizmetini yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="07f92-136">After the script completes, stop and restart the HPC Job Scheduler Service by typing the following commands:</span></span>
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-the-hpc-pack-client-utilities-on-an-on-premises-computer"></a><span data-ttu-id="07f92-137">2. adım: bir şirket içi bilgisayar HPC Pack istemci yardımcı programları yükle</span><span class="sxs-lookup"><span data-stu-id="07f92-137">Step 2: Install the HPC Pack client utilities on an on-premises computer</span></span>
<span data-ttu-id="07f92-138">HPC Pack istemci yardımcı programları bilgisayarınıza yüklemek istiyorsanız, HPC paketi Kurulum dosyaları (tam yükleme) indirin [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="07f92-138">If you want to install the HPC Pack client utilities on your computer, download the HPC Pack setup files (full installation) from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="07f92-139">Yüklemeye başlamak için kurulum seçeneğini seçin **HPC Pack istemci yardımcı programları**.</span><span class="sxs-lookup"><span data-stu-id="07f92-139">When you begin the installation, choose the setup option for the **HPC Pack client utilities**.</span></span>

<span data-ttu-id="07f92-140">Üstbilgi düğüm VM'ine işleri göndermek için HPC Pack istemci araçları kullanmak için ayrıca baş düğümünden bir sertifika verin ve istemci bilgisayara yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="07f92-140">To use the HPC Pack client tools to submit jobs to the head node VM, you also need to export a certificate from the head node and install it on the client computer.</span></span> <span data-ttu-id="07f92-141">Sertifika olması gerekir. CER biçimi.</span><span class="sxs-lookup"><span data-stu-id="07f92-141">The certificate must be in .CER format.</span></span>

<span data-ttu-id="07f92-142">**Sertifika baş düğümünden dışarı aktarma**</span><span class="sxs-lookup"><span data-stu-id="07f92-142">**To export the certificate from the head node**</span></span>

1. <span data-ttu-id="07f92-143">Baş düğümünde yerel bilgisayar hesabı için bir Microsoft Yönetim Konsolu için Sertifikalar ek bileşenini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="07f92-143">On the head node, add the Certificates snap-in to a Microsoft Management Console for the Local Computer account.</span></span> <span data-ttu-id="07f92-144">Ek bileşenini eklemek adımlar için bkz: [Sertifikalar ek bileşenini MMC'ye ekleme](https://technet.microsoft.com/library/cc754431.aspx).</span><span class="sxs-lookup"><span data-stu-id="07f92-144">For steps to add the snap-in, see [Add the Certificates Snap-in to an MMC](https://technet.microsoft.com/library/cc754431.aspx).</span></span>
2. <span data-ttu-id="07f92-145">Konsol ağacında **sertifikalar – yerel bilgisayar** > **kişisel**ve ardından **Sertifikalar**.</span><span class="sxs-lookup"><span data-stu-id="07f92-145">In the console tree, expand **Certificates – Local Computer** > **Personal**, and then click **Certificates**.</span></span>
3. <span data-ttu-id="07f92-146">HPC Pack web bileşenleri için yapılandırılmış sertifikayı bulun [adım 1: yükleme ve web bileşenleri baş düğümünde yapılandırma](#step-1:-install-and-configure-the-web-components-on-the-head-node) (örneğin, CN =&lt;*HeadNodeDnsName* &gt;. cloudapp.net).</span><span class="sxs-lookup"><span data-stu-id="07f92-146">Locate the certificate that you configured for the HPC Pack web components in [Step 1: Install and configure the web components on the head node](#step-1:-install-and-configure-the-web-components-on-the-head-node) (for example, CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net).</span></span>
4. <span data-ttu-id="07f92-147">Sertifikayı sağ tıklatın ve **tüm görevler** > **verme**.</span><span class="sxs-lookup"><span data-stu-id="07f92-147">Right-click the certificate, and click **All Tasks** > **Export**.</span></span>
5. <span data-ttu-id="07f92-148">Sertifika Dışarı Aktarma Sihirbazı'nda tıklatın **sonraki**ve emin **Hayır, özel anahtarı verme** seçilir.</span><span class="sxs-lookup"><span data-stu-id="07f92-148">In the Certificate Export Wizard, click **Next**, and ensure that **No, do not export the private key** is selected.</span></span>
6. <span data-ttu-id="07f92-149">DER ile kodlanmış ikili X.509 sertifikasını dışarı aktarmak için sihirbazın kalan adımları izleyin (. CER) biçimi.</span><span class="sxs-lookup"><span data-stu-id="07f92-149">Follow the remaining steps of the wizard to export the certificate in DER encoded binary X.509 (.CER) format.</span></span>

<span data-ttu-id="07f92-150">**İstemci bilgisayara sertifikayı içeri aktarmak için**</span><span class="sxs-lookup"><span data-stu-id="07f92-150">**To import the certificate on the client computer**</span></span>

1. <span data-ttu-id="07f92-151">İstemci bilgisayarı üzerindeki bir klasöre baş düğümünden dışarı aktardığınız sertifikayı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="07f92-151">Copy the certificate that you exported from the head node to a folder on the client computer.</span></span>
2. <span data-ttu-id="07f92-152">İstemci bilgisayarda certmgr.msc çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="07f92-152">On the client computer, run certmgr.msc.</span></span>
3. <span data-ttu-id="07f92-153">Sertifika Yöneticisi'nde **Sertifikalar – Geçerli kullanıcı** > **güvenilen kök sertifika yetkilileri**, sağ **sertifikaları**ve ardından tıklatın **tüm görevler** > **alma**.</span><span class="sxs-lookup"><span data-stu-id="07f92-153">In Certificate Manager, expand **Certificates – Current user** > **Trusted Root Certification Authorities**, right-click **Certificates**, and then click **All Tasks** > **Import**.</span></span>
4. <span data-ttu-id="07f92-154">Sertifika Alma Sihirbazı'nda tıklatın **sonraki** baş düğümünden güvenilen kök sertifika yetkilileri deposuna dışarı aktardığınız sertifikayı almak için adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="07f92-154">In the Certificate Import Wizard, click **Next** and follow the steps to import the certificate that you exported from the head node to the Trusted Root Certification Authorities store.</span></span>

> [!TIP]
> <span data-ttu-id="07f92-155">Baş düğümüne sertifika yetkilisinde istemci bilgisayar tarafından tanınmadığından bir güvenlik uyarısı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07f92-155">You might see a security warning, because the certification authority on the head node isn't recognized by the client computer.</span></span> <span data-ttu-id="07f92-156">Test amacıyla, bu uyarıyı yok sayın ve sertifika alma tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="07f92-156">For testing purposes, you can ignore this warning and complete the certificate import.</span></span>
> 
> 

## <a name="step-3-run-test-jobs-on-the-cluster"></a><span data-ttu-id="07f92-157">3. adım: Çalıştır test işleri küme üzerinde</span><span class="sxs-lookup"><span data-stu-id="07f92-157">Step 3: Run test jobs on the cluster</span></span>
<span data-ttu-id="07f92-158">Yapılandırmanızı doğrulamak için şirket içi bilgisayarından Azure kümesinde işleri çalıştırmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="07f92-158">To verify your configuration, try running jobs on the cluster in Azure from the on-premises computer.</span></span> <span data-ttu-id="07f92-159">Örneğin, kümeye iş göndermek için HPC Pack GUI araçları veya komut satırı komutlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07f92-159">For example, you can use HPC Pack GUI tools or command-line commands to submit jobs to the cluster.</span></span> <span data-ttu-id="07f92-160">İşlerini göndermek için web tabanlı portal de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07f92-160">You can also use a web-based portal to submit jobs.</span></span>

<span data-ttu-id="07f92-161">**İstemci bilgisayarda iş gönderme komutları çalıştırmak için**</span><span class="sxs-lookup"><span data-stu-id="07f92-161">**To run job submission commands on the client computer**</span></span>

1. <span data-ttu-id="07f92-162">HPC Pack istemci yardımcı programları yüklü olduğu bir istemci bilgisayarda bir komut istemi başlatın.</span><span class="sxs-lookup"><span data-stu-id="07f92-162">On a client computer where the HPC Pack client utilities are installed, start a Command Prompt.</span></span>
2. <span data-ttu-id="07f92-163">Bir örnek komutu yazın.</span><span class="sxs-lookup"><span data-stu-id="07f92-163">Type a sample command.</span></span> <span data-ttu-id="07f92-164">Örneğin, kümedeki tüm işleri listelemek için tam DNS adı baş düğümü bağlı olarak aşağıdakilerden birini benzeyen bir komut yazın:</span><span class="sxs-lookup"><span data-stu-id="07f92-164">For example, to list all jobs on the cluster, type a command similar to one of the following, depending on the full DNS name of the head node:</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    <span data-ttu-id="07f92-165">or</span><span class="sxs-lookup"><span data-stu-id="07f92-165">or</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > <span data-ttu-id="07f92-166">Baş düğüm, IP adresi değil tam DNS adını Zamanlayıcı URL'yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="07f92-166">Use the full DNS name of the head node, not the IP address, in the scheduler URL.</span></span> <span data-ttu-id="07f92-167">IP adresi belirtirseniz, bir hata "sunucu sertifikası ya da geçerli bir güven zinciri veya güvenilir kök deposuna yerleştirilecek gerekiyor." benzer görünür</span><span class="sxs-lookup"><span data-stu-id="07f92-167">If you specify the IP address, an error appears similar to "The server certificate needs to either have a valid chain of trust or to be placed in the trusted root store."</span></span>
   > 
   > 
3. <span data-ttu-id="07f92-168">İstendiğinde, kullanıcı adını yazın (biçiminde &lt;DomainName&gt;\\&lt;kullanıcıadı&gt;) ve HPC Küme Yöneticisi ya da yapılandırdığınız başka bir küme kullanıcının parolası.</span><span class="sxs-lookup"><span data-stu-id="07f92-168">When prompted, type the user name (in the form &lt;DomainName&gt;\\&lt;UserName&gt;) and password of the HPC cluster administrator or another cluster user that you configured.</span></span> <span data-ttu-id="07f92-169">Yerel olarak daha fazla iş işlemleri için kimlik bilgilerini depolamak üzere seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07f92-169">You can choose to store the credentials locally for more job operations.</span></span>
   
    <span data-ttu-id="07f92-170">İşlerini listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="07f92-170">A list of jobs appears.</span></span>

<span data-ttu-id="07f92-171">**İstemci bilgisayarda HPC İş Yöneticisi'ni kullanmak için**</span><span class="sxs-lookup"><span data-stu-id="07f92-171">**To use HPC Job Manager on the client computer**</span></span>

1. <span data-ttu-id="07f92-172">Daha önce bir küme kullanıcının etki alanı kimlik bilgilerini bir işi gönderirken depoladığınız alamadık, kimlik bilgileri Yöneticisi'nde kimlik bilgileri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07f92-172">If you didn't previously store domain credentials for a cluster user when submitting a job, you can add the credentials in Credential Manager.</span></span>
   
    <span data-ttu-id="07f92-173">a.</span><span class="sxs-lookup"><span data-stu-id="07f92-173">a.</span></span> <span data-ttu-id="07f92-174">İstemci bilgisayardaki Denetim Masası'ndaki kimlik bilgisi Yöneticisi'ni başlatın.</span><span class="sxs-lookup"><span data-stu-id="07f92-174">In Control Panel on the client computer, start Credential Manager.</span></span>
   
    <span data-ttu-id="07f92-175">b.</span><span class="sxs-lookup"><span data-stu-id="07f92-175">b.</span></span> <span data-ttu-id="07f92-176">Tıklatın **Windows kimlik bilgileri** > **genel bir kimlik bilgisi Ekle**.</span><span class="sxs-lookup"><span data-stu-id="07f92-176">Click **Windows Credentials** > **Add a generic credential**.</span></span>
   
    <span data-ttu-id="07f92-177">c.</span><span class="sxs-lookup"><span data-stu-id="07f92-177">c.</span></span> <span data-ttu-id="07f92-178">Internet adresini belirtin (örneğin, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler veya https://&lt;HeadNodeDnsName&gt;.&lt; Bölge&gt;.cloudapp.azure.com/HpcScheduler) ve kullanıcı adı (&lt;DomainName&gt;\\&lt;kullanıcıadı&gt;) ve Küme Yöneticisi veya başka bir parola yapılandırdığınız küme kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="07f92-178">Specify the Internet address (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com/HpcScheduler), and the user name (&lt;DomainName&gt;\\&lt;UserName&gt;) and password of the cluster administrator or another cluster user that you configured.</span></span>
2. <span data-ttu-id="07f92-179">İstemci bilgisayarda HPC İş Yöneticisi'ni başlatın.</span><span class="sxs-lookup"><span data-stu-id="07f92-179">On the client computer, start HPC Job Manager.</span></span>
3. <span data-ttu-id="07f92-180">İçinde **baş düğüm Seç** iletişim kutusunda, Azure'da baş düğüm URL'sini yazın (örneğin, https://&lt;HeadNodeDnsName&gt;. cloudapp.net veya https://&lt;HeadNodeDnsName&gt;.&lt; Bölge&gt;. cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="07f92-180">In the **Select Head Node** dialog box, type the URL to the head node in Azure (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com).</span></span>
   
    <span data-ttu-id="07f92-181">HPC İş Yöneticisi'ni açar ve baş düğümünde işlerin bir listesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="07f92-181">HPC Job Manager opens and shows a list of jobs on the head node.</span></span>

<span data-ttu-id="07f92-182">**Baş düğüm üzerinde çalışan web portalı kullanmak için**</span><span class="sxs-lookup"><span data-stu-id="07f92-182">**To use the web portal running on the head node**</span></span>

1. <span data-ttu-id="07f92-183">İstemci bilgisayarda bir web tarayıcı başlatmak ve baş düğüm tam DNS adını bağlı olarak aşağıdaki adresleri birini girin:</span><span class="sxs-lookup"><span data-stu-id="07f92-183">Start a web browser on the client computer, and enter one of the following addresses, depending on the full DNS name of the head node:</span></span>
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    <span data-ttu-id="07f92-184">or</span><span class="sxs-lookup"><span data-stu-id="07f92-184">or</span></span>
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. <span data-ttu-id="07f92-185">Görüntülenen güvenlik iletişim kutusunda HPC Küme Yöneticisi etki alanı kimlik bilgilerini yazın.</span><span class="sxs-lookup"><span data-stu-id="07f92-185">In the security dialog box that appears, type the domain credentials of the HPC cluster administrator.</span></span> <span data-ttu-id="07f92-186">(Diğer küme kullanıcılar da farklı rolleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07f92-186">(You can also add other cluster users in different roles.</span></span> <span data-ttu-id="07f92-187">Bkz: [küme kullanıcıları yönetme](https://technet.microsoft.com/library/ff919335.aspx).)</span><span class="sxs-lookup"><span data-stu-id="07f92-187">See [Managing Cluster Users](https://technet.microsoft.com/library/ff919335.aspx).)</span></span>
   
    <span data-ttu-id="07f92-188">Web portalı iş liste görünümü açılır.</span><span class="sxs-lookup"><span data-stu-id="07f92-188">The web portal opens to the job list view.</span></span>
3. <span data-ttu-id="07f92-189">"Hello World" dizesi kümeden döndüren bir örnek işi göndermek için tıklatın **yeni iş** sol gezinti içinde.</span><span class="sxs-lookup"><span data-stu-id="07f92-189">To submit a sample job that returns the string “Hello World” from the cluster, click **New job** in the left-hand navigation.</span></span>
4. <span data-ttu-id="07f92-190">Üzerinde **yeni iş** sayfasında **gönderme sayfalarından**, tıklatın **HelloWorld**.</span><span class="sxs-lookup"><span data-stu-id="07f92-190">On the **New Job** page, under **From submission pages**, click **HelloWorld**.</span></span> <span data-ttu-id="07f92-191">İş gönderme sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="07f92-191">The job submission page appears.</span></span>
5. <span data-ttu-id="07f92-192">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="07f92-192">Click **Submit**.</span></span> <span data-ttu-id="07f92-193">İstenirse, HPC Küme Yöneticisi etki alanı kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="07f92-193">If prompted, provide the domain credentials of the HPC cluster administrator.</span></span> <span data-ttu-id="07f92-194">İş gönderildiğinde ve iş kimliği kasasındaki **İşlerim** sayfası.</span><span class="sxs-lookup"><span data-stu-id="07f92-194">The job is submitted, and the job ID appears on the **My Jobs** page.</span></span>
6. <span data-ttu-id="07f92-195">Gönderdiğiniz iş sonuçlarını görüntülemek için iş kimliği'ni tıklatın ve ardından **görünümü görevleri** komut çıktısı görüntülemek için (altında **çıkış**).</span><span class="sxs-lookup"><span data-stu-id="07f92-195">To view the results of the job that you submitted, click the job ID, and then click **View Tasks** to view the command output (under **Output**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="07f92-196">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="07f92-196">Next steps</span></span>
* <span data-ttu-id="07f92-197">Ayrıca Azure kümeye ile iş gönderebilirsiniz [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="07f92-197">You can also submit jobs to the Azure cluster with the [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span>
* <span data-ttu-id="07f92-198">Bir Linux istemciden kümeye iş göndermek istiyorsanız, Python örnekte bkz [HPC Pack 2012 R2 SDK'sı ve örnek kod](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="07f92-198">If you want to submit cluster jobs from a Linux client, see the Python sample in the [HPC Pack 2012 R2 SDK and Sample Code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span>

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
