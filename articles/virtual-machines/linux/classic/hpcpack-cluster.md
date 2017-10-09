---
title: "aaaLinux bir HPC Pack kümede sanal makineleri işlem | Microsoft Docs"
description: "Nasıl toocreate ve kullanım bir HPC Pack Linux yüksek performanslı bilgi işlem (HPC) iş yükleri için Azure'da küme öğrenin"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="00225-103">Azure’daki bir HPC Pack kümesinde Linux işlem düğümleri kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="00225-103">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="00225-104">Ayarlanmış bir [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) küme Windows Server ve birkaç çalıştıran bir baş düğüm içeren Azure işlem desteklenen Linux dağıtım çalışan düğümleri.</span><span class="sxs-lookup"><span data-stu-id="00225-104">Set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure that contains a head node running Windows Server and several compute nodes running a supported Linux distribution.</span></span> <span data-ttu-id="00225-105">Merhaba Linux düğümleri ve hello Windows hello küme baş düğümüne arasındaki seçenekleri toomove verileri keşfedin.</span><span class="sxs-lookup"><span data-stu-id="00225-105">Explore options toomove data among hello Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="00225-106">Nasıl toohello küme toosubmit Linux HPC iş öğrenin.</span><span class="sxs-lookup"><span data-stu-id="00225-106">Learn how toosubmit Linux HPC jobs toohello cluster.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="00225-107">Yüksek bir düzeyde hello Aşağıdaki diyagramda hello HPC paketi küme oluşturun ve çalışmak gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="00225-107">At a high level, hello following diagram shows hello HPC Pack cluster you create and work with.</span></span>

![Linux düğümleri ile HPC Pack kümesi][scenario]

<span data-ttu-id="00225-109">Diğer Seçenekler toorun Linux HPC için azure'da iş yüklerini bkz [toplu işlem ve yüksek performanslı bilgi işlem için teknik kaynaklar](../../../batch/big-compute-resources.md).</span><span class="sxs-lookup"><span data-stu-id="00225-109">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/big-compute-resources.md).</span></span>

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a><span data-ttu-id="00225-110">Linux işlem düğümlerini içeren bir HPC Pack kümeyi dağıtma</span><span class="sxs-lookup"><span data-stu-id="00225-110">Deploy an HPC Pack cluster with Linux compute nodes</span></span>
<span data-ttu-id="00225-111">Bu makalede, iki seçenek toodeploy bir HPC paketi küme Linux işlem düğümleri ile Azure'da gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="00225-111">This article shows you two options toodeploy an HPC Pack cluster in Azure with Linux compute nodes.</span></span> <span data-ttu-id="00225-112">İki yöntem HPC Pack toocreate hello baş düğüm ile Windows Server Market görüntüsünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="00225-112">Both methods use a Marketplace image of Windows Server with HPC Pack toocreate hello head node.</span></span> 

* <span data-ttu-id="00225-113">**Azure Resource Manager şablonu** -hello Azure Marketi bir şablondan ya da hello topluluktan hello Resource Manager dağıtım modelinde hello kümesinin tooautomate oluşturulması hızlı başlatma şablonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="00225-113">**Azure Resource Manager template** - Use a template from hello Azure Marketplace, or a quickstart template from hello community, tooautomate creation of hello cluster in hello Resource Manager deployment model.</span></span> <span data-ttu-id="00225-114">Örneğin, hello [Linux iş yükleri için HPC paketi küme](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) hello Azure Marketi şablonunda Linux HPC için eksiksiz bir HPC paketi küme altyapı iş yükleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="00225-114">For example, hello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace creates a complete HPC Pack cluster infrastructure for Linux HPC workloads.</span></span>
* <span data-ttu-id="00225-115">**PowerShell Betiği** -kullanım hello [Microsoft HPC Pack Iaas dağıtım betiği](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**yeni HpcIaaSCluster.ps1**) tooautomate hello Klasik dağıtım modeli tam küme dağıtımında.</span><span class="sxs-lookup"><span data-stu-id="00225-115">**PowerShell script** - Use hello [Microsoft HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) tooautomate a complete cluster deployment in hello classic deployment model.</span></span> <span data-ttu-id="00225-116">Bu Azure PowerShell komut dosyasını bir HPC Pack VM görüntüsü hello Azure Marketi hızlı dağıtımı için kullanır ve Linux işlem düğümlerini yapılandırma parametreleri toodeploy kapsamlı bir kümesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="00225-116">This Azure PowerShell script uses an HPC Pack VM image in hello Azure Marketplace for fast deployment and provides a comprehensive set of configuration parameters toodeploy Linux compute nodes.</span></span>

<span data-ttu-id="00225-117">Azure içindeki HPC paketi küme dağıtım seçenekleri hakkında daha fazla bilgi için bkz: [seçenekleri toocreate ve Microsoft HPC paketi ile Azure yüksek performanslı bilgi işlem (HPC) bir kümede yönetmek](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="00225-117">For more information about HPC Pack cluster deployment options in Azure, see [Options toocreate and manage a high-performance computing (HPC) cluster in Azure with Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="00225-118">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="00225-118">Prerequisites</span></span>
* <span data-ttu-id="00225-119">**Azure aboneliği** -ya da hello Azure genel ya da Azure Çin hizmeti bir aboneliği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00225-119">**Azure subscription** - You can use a subscription in either hello Azure Global or Azure China service.</span></span> <span data-ttu-id="00225-120">Bir hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="00225-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="00225-121">**Çekirdek kota** -özellikle çok çekirdekli VM boyutları birkaç küme düğümleri toodeploy seçerseniz tooincrease hello kota çekirdek, gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="00225-121">**Cores quota** - You might need tooincrease hello quota of cores, especially if you choose toodeploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="00225-122">tooincrease bir kota ücretsiz bir çevrimiçi müşteri destek isteği açın.</span><span class="sxs-lookup"><span data-stu-id="00225-122">tooincrease a quota, open an online customer support request at no charge.</span></span>
* <span data-ttu-id="00225-123">**Linux dağıtımları** -şu anda HPC Pack Merhaba işlem düğümleri için Linux dağıtımları aşağıdaki destekler.</span><span class="sxs-lookup"><span data-stu-id="00225-123">**Linux distributions** - Currently HPC Pack supports hello following Linux distributions for compute nodes.</span></span> <span data-ttu-id="00225-124">Bu dağıtımları Market sürümleri kullanılabiliyorsa kullanın veya kendi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="00225-124">You can use Marketplace versions of these distributions where available, or supply your own.</span></span>
  
  * <span data-ttu-id="00225-125">**CentOS tabanlı**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span><span class="sxs-lookup"><span data-stu-id="00225-125">**CentOS-based**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span></span>
  * <span data-ttu-id="00225-126">**Red Hat Enterprise Linux**: 6.7, 6,8, 7.2</span><span class="sxs-lookup"><span data-stu-id="00225-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span></span>
  * <span data-ttu-id="00225-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 HPC, SLES 12 HPC (Premium) için için</span><span class="sxs-lookup"><span data-stu-id="00225-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 for HPC, SLES 12 for HPC (Premium)</span></span>
  * <span data-ttu-id="00225-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="00225-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span></span>
    
    > [!TIP]
    > <span data-ttu-id="00225-129">toouse hello Azure RDMA ağ hello RDMA özelliğine sahip VM boyutları, biri ile bir SUSE Linux Enterprise Server 12 HPC veya CentOS tabanlı HPC hello Azure Market görüntüsünden belirtin.</span><span class="sxs-lookup"><span data-stu-id="00225-129">toouse hello Azure RDMA network with one of hello RDMA-capable VM sizes, specify a SUSE Linux Enterprise Server 12 HPC or CentOS-based HPC image from hello Azure Marketplace.</span></span> <span data-ttu-id="00225-130">Daha fazla bilgi için bkz: [yüksek performanslı işlem VM boyutları](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="00225-130">For more information, see [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

<span data-ttu-id="00225-131">Merhaba HPC Pack Iaas dağıtım komut dosyası kullanarak toodeploy hello küme ek önkoşulları:</span><span class="sxs-lookup"><span data-stu-id="00225-131">Additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="00225-132">**İstemci bilgisayar** -bir Windows tabanlı bir istemci bilgisayar toorun hello küme dağıtım betiğinin gerekir.</span><span class="sxs-lookup"><span data-stu-id="00225-132">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="00225-133">**Azure PowerShell** - [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview) (sürüm 0.8.10 veya üzeri) istemci bilgisayarınızda.</span><span class="sxs-lookup"><span data-stu-id="00225-133">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="00225-134">**HPC Pack Iaas dağıtım betiği** - karşıdan yükle ve en son sürümünü hello hello betikten hello paket [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="00225-134">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="00225-135">Merhaba komut dosyasının hello sürümünü çalıştırarak denetleyebilirsiniz `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="00225-135">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="00225-136">Bu makalede, sürüm 4.4.1 veya daha sonra hello komut dosyasının temel alır.</span><span class="sxs-lookup"><span data-stu-id="00225-136">This article is based on version 4.4.1 or later of hello script.</span></span>

### <a name="deployment-option-1-use-a-resource-manager-template"></a><span data-ttu-id="00225-137">Dağıtım seçeneği 1.</span><span class="sxs-lookup"><span data-stu-id="00225-137">Deployment option 1.</span></span> <span data-ttu-id="00225-138">Resource Manager şablonu kullanın</span><span class="sxs-lookup"><span data-stu-id="00225-138">Use a Resource Manager template</span></span>
1. <span data-ttu-id="00225-139">Toohello Git [Linux iş yükleri için HPC paketi küme](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) şablonunda Azure Marketi hello öğesini tıklatıp **dağıtma**.</span><span class="sxs-lookup"><span data-stu-id="00225-139">Go toohello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace, and click **Deploy**.</span></span>
2. <span data-ttu-id="00225-140">İçinde Azure portal Merhaba, hello bilgileri gözden geçirin ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="00225-140">In hello Azure portal, review hello information and then click **Create**.</span></span>
   
    ![Portal oluşturma][portal]
3. <span data-ttu-id="00225-142">Merhaba üzerinde **Temelleri** dikey penceresinde de hello baş düğüm VM adları hello küme için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="00225-142">On hello **Basics** blade, enter a name for hello cluster, which also names hello head node VM.</span></span> <span data-ttu-id="00225-143">Varolan bir kaynak grubu seçin veya kullanılabilir tooyou olan bir konuma hello dağıtım için bir grup oluşturun.</span><span class="sxs-lookup"><span data-stu-id="00225-143">You can choose an existing resource group or create a group for hello deployment in a location that's available tooyou.</span></span> <span data-ttu-id="00225-144">Merhaba konumu hello kullanılabilirliğini belirli VM boyutları ve diğer Azure hizmetleriyle etkiler (bkz [bölgeye göre ürünleri](https://azure.microsoft.com/regions/services/)).</span><span class="sxs-lookup"><span data-stu-id="00225-144">hello location affects hello availability of certain VM sizes and other Azure services (see [Products available by region](https://azure.microsoft.com/regions/services/)).</span></span>
4. <span data-ttu-id="00225-145">Merhaba üzerinde **düğümü ayarları Head** dikey penceresinde, ilk dağıtım için genellikle hello varsayılan ayarları kabul edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00225-145">On hello **Head node settings** blade, for a first deployment, you can generally accept hello default settings.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="00225-146">Merhaba **sonrası yapılandırma betiği URL'si** isteğe bağlı bir toospecify çalışmaya başladıktan sonra hello baş düğümünde VM toorun istediğiniz genel kullanıma açık bir Windows PowerShell komut dosyası da ayarlıyor.</span><span class="sxs-lookup"><span data-stu-id="00225-146">hello **Post-configuration script URL** is an optional setting toospecify a publicly available Windows PowerShell script that you want toorun on hello head node VM after it is running.</span></span> 
   > 
   > 
5. <span data-ttu-id="00225-147">Merhaba üzerinde **düğümü ayarları işlem** dikey penceresinde hello düğümleri, hello sayısını ve boyutunu hello düğümler için bir adlandırma deseni seçin ve Linux dağıtım toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="00225-147">On hello **Compute node settings** blade, select a naming pattern for hello nodes, hello number and size of hello nodes, and hello Linux distribution toodeploy.</span></span>
6. <span data-ttu-id="00225-148">Merhaba üzerinde **Altyapı ayarlarını** dikey penceresinde hello sanal ağ ve Active Directory adlarını girin etki alanı, etki alanı ve VM yönetici kimlik bilgileri ve hello depolama hesapları için bir adlandırma deseni.</span><span class="sxs-lookup"><span data-stu-id="00225-148">On hello **Infrastructure settings** blade, enter names for hello virtual network and Active Directory domain, domain and VM administrator credentials, and a naming pattern for hello storage accounts.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="00225-149">HPC Pack Merhaba Active Directory etki alanı tooauthenticate küme kullanıcıları kullanır.</span><span class="sxs-lookup"><span data-stu-id="00225-149">HPC Pack uses hello Active Directory domain tooauthenticate cluster users.</span></span> 
   > 
   > 
7. <span data-ttu-id="00225-150">Merhaba doğrulama testlerini çalıştırmak ve hello kullanım koşullarını gözden geçirin sonra tıklayın **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="00225-150">After hello validation tests run and you review hello terms of use, click **Purchase**.</span></span>

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a><span data-ttu-id="00225-151">Dağıtım seçeneği 2.</span><span class="sxs-lookup"><span data-stu-id="00225-151">Deployment option 2.</span></span> <span data-ttu-id="00225-152">Merhaba Iaas dağıtım betiği kullanın</span><span class="sxs-lookup"><span data-stu-id="00225-152">Use hello IaaS deployment script</span></span>
<span data-ttu-id="00225-153">Aşağıda hello HPC Pack Iaas dağıtım komut dosyası kullanarak ek önkoşulları toodeploy hello küme verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="00225-153">Following are additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="00225-154">**İstemci bilgisayar** -bir Windows tabanlı bir istemci bilgisayar toorun hello küme dağıtım betiğinin gerekir.</span><span class="sxs-lookup"><span data-stu-id="00225-154">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="00225-155">**Azure PowerShell** - [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview) (sürüm 0.8.10 veya üzeri) istemci bilgisayarınızda.</span><span class="sxs-lookup"><span data-stu-id="00225-155">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="00225-156">**HPC Pack Iaas dağıtım betiği** - karşıdan yükle ve en son sürümünü hello hello betikten hello paket [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="00225-156">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="00225-157">Merhaba komut dosyasının hello sürümünü çalıştırarak denetleyebilirsiniz `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="00225-157">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="00225-158">Bu makalede, sürüm 4.4.1 veya daha sonra hello komut dosyasının temel alır.</span><span class="sxs-lookup"><span data-stu-id="00225-158">This article is based on version 4.4.1 or later of hello script.</span></span>

<span data-ttu-id="00225-159">**XML yapılandırma dosyası**</span><span class="sxs-lookup"><span data-stu-id="00225-159">**XML configuration file**</span></span>

<span data-ttu-id="00225-160">Merhaba HPC Pack Iaas dağıtım betiği giriş toodescribe hello HPC kümesi olarak bir XML yapılandırma dosyasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="00225-160">hello HPC Pack IaaS deployment script uses an XML configuration file as input toodescribe hello  HPC cluster.</span></span> <span data-ttu-id="00225-161">Merhaba aşağıdaki örnek yapılandırma dosyası bir HPC paketi üstbilgi düğümü ve iki boyutu A7 CentOS 7.0 Linux işlem düğümleri oluşan küçük bir küme belirtir.</span><span class="sxs-lookup"><span data-stu-id="00225-161">hello following sample configuration file specifies a small cluster consisting of an HPC Pack head node and two size A7 CentOS 7.0 Linux compute nodes.</span></span> 

<span data-ttu-id="00225-162">Merhaba dosya ortamınız ve istenen küme yapılandırması için gereken şekilde değiştirin ve HPCDemoConfig.xml gibi bir adla kaydedin.</span><span class="sxs-lookup"><span data-stu-id="00225-162">Modify hello file as needed for your environment and desired cluster configuration, and save it with a name such as HPCDemoConfig.xml.</span></span> <span data-ttu-id="00225-163">Örneğin, toosupply abonelik adı ve benzersiz depolama hesabı adı ve bulut hizmeti adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="00225-163">For example, you need toosupply your subscription name and a unique storage account name and cloud service name.</span></span> <span data-ttu-id="00225-164">Ayrıca, farklı bir toochoose Linux görüntü hello işlem düğümleri için desteklenen isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00225-164">Additionally, you might want toochoose a different supported Linux image for hello compute nodes.</span></span> <span data-ttu-id="00225-165">Hello yapılandırma dosyasında hello öğeler hakkında daha fazla bilgi için bkz: hello betik klasöründeki hello Manual.rtf dosyasını ve [hello HPC Pack Iaas dağıtım betiği ile bir HPC kümesi oluşturma](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="00225-165">For more information about hello elements in hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="00225-166">**toorun hello HPC Pack Iaas dağıtım komut dosyası**</span><span class="sxs-lookup"><span data-stu-id="00225-166">**toorun hello HPC Pack IaaS deployment script**</span></span>

1. <span data-ttu-id="00225-167">Windows PowerShell hello istemci bilgisayarda yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="00225-167">Open Windows PowerShell on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="00225-168">Değişiklik hello betik olduğu dizin toohello klasörü yüklü (Bu örnekte E:\IaaSClusterScript).</span><span class="sxs-lookup"><span data-stu-id="00225-168">Change directory toohello folder where hello script is installed (E:\IaaSClusterScript in this example).</span></span>
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. <span data-ttu-id="00225-169">Komut toodeploy hello HPC paketi küme aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="00225-169">Run hello following command toodeploy hello HPC Pack cluster.</span></span> <span data-ttu-id="00225-170">Bu örnekte hello yapılandırma dosyasının E:\HPCDemoConfig.xml içinde bulunan varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="00225-170">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml</span></span>
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    <span data-ttu-id="00225-171">a.</span><span class="sxs-lookup"><span data-stu-id="00225-171">a.</span></span> <span data-ttu-id="00225-172">Çünkü hello **Admınpassword** belirtilmezse komut önceki hello olduğunuz istendiğinde tooenter hello kullanıcının parolasını *MyAdminName*.</span><span class="sxs-lookup"><span data-stu-id="00225-172">Because hello **AdminPassword** is not specified in hello preceding command, you are prompted tooenter hello password for user *MyAdminName*.</span></span>
   
    <span data-ttu-id="00225-173">b.</span><span class="sxs-lookup"><span data-stu-id="00225-173">b.</span></span> <span data-ttu-id="00225-174">Merhaba betik sonra toovalidate hello yapılandırma dosyasını başlatır.</span><span class="sxs-lookup"><span data-stu-id="00225-174">hello script then starts toovalidate hello configuration file.</span></span> <span data-ttu-id="00225-175">Yukarı hello ağ bağlantısı bağlı olarak tooseveral dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="00225-175">It can take up tooseveral minutes depending on hello network connection.</span></span>
   
    ![Doğrulama][validate]
   
    <span data-ttu-id="00225-177">c.</span><span class="sxs-lookup"><span data-stu-id="00225-177">c.</span></span> <span data-ttu-id="00225-178">Doğrulama geçirmek sonra hello betik hello küme kaynakları toocreate listeler.</span><span class="sxs-lookup"><span data-stu-id="00225-178">After validations pass, hello script lists hello cluster resources toocreate.</span></span> <span data-ttu-id="00225-179">Girin *Y* toocontinue.</span><span class="sxs-lookup"><span data-stu-id="00225-179">Enter *Y* toocontinue.</span></span>
   
    ![Kaynaklar][resources]
   
    <span data-ttu-id="00225-181">d.</span><span class="sxs-lookup"><span data-stu-id="00225-181">d.</span></span> <span data-ttu-id="00225-182">Merhaba betik toodeploy hello HPC paketi küme başlar ve daha fazla el ile adımlar olmadan hello yapılandırmasını tamamlar.</span><span class="sxs-lookup"><span data-stu-id="00225-182">hello script starts toodeploy hello HPC Pack cluster and completes hello configuration without further manual steps.</span></span> <span data-ttu-id="00225-183">Merhaba komut dosyası için birkaç dakika çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="00225-183">hello script can run for several minutes.</span></span>
   
    ![Dağıtma][deploy]
   
   > [!NOTE]
   > <span data-ttu-id="00225-185">Bu örnekte, hello komut dosyası günlük dosyası otomatik olarak bu yana hello oluşturur **- günlük dosyası** parametresinde değil.</span><span class="sxs-lookup"><span data-stu-id="00225-185">In this example, hello script generates a log file automatically since hello **-LogFile** parameter isn't specified.</span></span> <span data-ttu-id="00225-186">Merhaba günlükleri gerçek zamanlı olarak yazılmış değil, ancak hello sonunda hello doğrulama ve başlangıç dağıtım toplanır.</span><span class="sxs-lookup"><span data-stu-id="00225-186">hello logs aren't written in real time, but are collected at hello end of hello validation and hello deployment.</span></span> <span data-ttu-id="00225-187">Merhaba betik çalışırken hello PowerShell işlem durursa, bazı günlükleri kaybolur.</span><span class="sxs-lookup"><span data-stu-id="00225-187">If hello PowerShell process is stopped while hello script is running, some logs are lost.</span></span>
   > 
   > 

## <a name="connect-toohello-head-node"></a><span data-ttu-id="00225-188">Toohello baş düğümüne bağlanmak</span><span class="sxs-lookup"><span data-stu-id="00225-188">Connect toohello head node</span></span>
<span data-ttu-id="00225-189">Azure'da hello HPC paketi küme dağıttıktan sonra [tarafından Uzak Masaüstü Bağlantısı](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello baş düğüm VM kullanarak hello hello kümeyi dağıttığınızda sağlanan etki alanı kimlik bilgilerini (örneğin, *hpc\\ clusteradmin*).</span><span class="sxs-lookup"><span data-stu-id="00225-189">After you deploy hello HPC Pack cluster in Azure, [connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, *hpc\\clusteradmin*).</span></span> <span data-ttu-id="00225-190">Merhaba küme hello baş düğümünden yönetin.</span><span class="sxs-lookup"><span data-stu-id="00225-190">You manage hello cluster from hello head node.</span></span>

<span data-ttu-id="00225-191">Merhaba baş düğümünde HPC Küme Yöneticisi'ni toocheck hello hello HPC paketi küme durumunu başlatın.</span><span class="sxs-lookup"><span data-stu-id="00225-191">On hello head node, start HPC Cluster Manager toocheck hello status of hello HPC Pack cluster.</span></span> <span data-ttu-id="00225-192">Yönetme ve Linux işlem düğümlerini izleme hello Windows ile birlikte çalıştığınız aynı şekilde işlem düğümlerini.</span><span class="sxs-lookup"><span data-stu-id="00225-192">You can manage and monitor Linux compute nodes hello same way you work with Windows compute nodes.</span></span> <span data-ttu-id="00225-193">Örneğin, listelenen hello Linux düğümleri bkz **kaynak yönetimi** (Bu düğümler hello ile dağıtılan **LinuxNode** şablonu).</span><span class="sxs-lookup"><span data-stu-id="00225-193">For example, you see hello Linux nodes listed in **Resource Management** (these nodes are deployed with hello **LinuxNode** template).</span></span>

![Düğüm Yönetimi][management]

<span data-ttu-id="00225-195">Merhaba hello Linux düğümleri Ayrıca bkz: **ısı Haritası** görünümü.</span><span class="sxs-lookup"><span data-stu-id="00225-195">You also see hello Linux nodes in hello **Heat Map** view.</span></span>

![Isı Haritası][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a><span data-ttu-id="00225-197">Nasıl Linux düğümleri ile bir kümede toomove veri</span><span class="sxs-lookup"><span data-stu-id="00225-197">How toomove data in a cluster with Linux nodes</span></span>
<span data-ttu-id="00225-198">Linux düğümleri ve hello Windows hello küme baş düğümüne arasında birkaç seçenek toomove veri içeriyor.</span><span class="sxs-lookup"><span data-stu-id="00225-198">You have several choices toomove data among Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="00225-199">Merhaba aşağıdaki bölümlerde daha ayrıntılı açıklanan üç yaygın yöntemleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="00225-199">Here are three common methods, described in more detail in hello following sections:</span></span>

* <span data-ttu-id="00225-200">**Azure dosya** -yönetilen bir SMB dosya paylaşımı toostore verileri Azure depolama alanında dosyaları açığa çıkarır.</span><span class="sxs-lookup"><span data-stu-id="00225-200">**Azure File** - Exposes a managed SMB file share toostore data files in Azure storage.</span></span> <span data-ttu-id="00225-201">Windows düğümleri ve Linux düğümleri takma bir Azure dosya paylaşımı bir sürücü veya klasöre hello olarak aynı zaman, farklı sanal ağlarda dağıtmış olsa bile.</span><span class="sxs-lookup"><span data-stu-id="00225-201">Windows nodes and Linux nodes can mount an Azure File share as a drive or folder at hello same time, even if they're deployed in different virtual networks.</span></span>
* <span data-ttu-id="00225-202">**Baş düğüm SMB paylaşımı** -Linux düğümleri üzerinde Windows standart bir paylaşılan klasör hello baş düğümü bağlar.</span><span class="sxs-lookup"><span data-stu-id="00225-202">**Head node SMB share** - Mounts a standard Windows shared folder of hello head node on Linux nodes.</span></span>
* <span data-ttu-id="00225-203">**Baş düğüm NFS sunucusu** -karma Windows ve Linux ortamı için bir dosya paylaşımı çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="00225-203">**Head node NFS server**  - Provides a file-sharing solution for a mixed Windows and Linux environment.</span></span>

### <a name="azure-file-storage"></a><span data-ttu-id="00225-204">Azure dosya depolama</span><span class="sxs-lookup"><span data-stu-id="00225-204">Azure File storage</span></span>
<span data-ttu-id="00225-205">Merhaba [Azure dosya](https://azure.microsoft.com/services/storage/files/) hizmetini hello standart SMB 2.1 protokolünü kullanan dosya paylaşımları sunar.</span><span class="sxs-lookup"><span data-stu-id="00225-205">hello [Azure File](https://azure.microsoft.com/services/storage/files/) service exposes file shares using hello standard SMB 2.1 protocol.</span></span> <span data-ttu-id="00225-206">Azure VM'ler ve cloud services bağlı paylaşımlar üzerinden uygulama bileşenleri arasında dosya verileri paylaşabilir ve şirket içi uygulamalara hello File storage API'si dosya verilerine erişebilir.</span><span class="sxs-lookup"><span data-stu-id="00225-206">Azure VMs and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share through hello File storage API.</span></span> 

<span data-ttu-id="00225-207">Bir Azure dosya paylaşımı ve hello baş düğümünde bağlama ayrıntılı adımlar toocreate için bkz: [Windows Azure File storage ile çalışmaya başlama](../../../storage/files/storage-how-to-use-files-windows.md).</span><span class="sxs-lookup"><span data-stu-id="00225-207">For detailed steps toocreate an Azure File share and mount it on hello head node, see [Get started with Azure File storage on Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span></span> <span data-ttu-id="00225-208">Merhaba Linux düğümleri toomount hello Azure dosya paylaşımında bkz [nasıl toouse Linux Azure File storage](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="00225-208">toomount hello Azure File share on hello Linux nodes, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="00225-209">kalıcı bağlantılar kurma tooset bkz [Persisting bağlantıları tooMicrosoft Azure dosyaları](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span><span class="sxs-lookup"><span data-stu-id="00225-209">tooset up persisting connections, see [Persisting connections tooMicrosoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span></span>

<span data-ttu-id="00225-210">Aşağıdaki örneğine hello Azure dosya paylaşımı bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="00225-210">In hello following example, create an Azure File share on a storage account.</span></span> <span data-ttu-id="00225-211">toomount hello hello baş düğümünde, açık bir komut istemi paylaşma ve hello aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="00225-211">toomount hello share on hello head node, open a Command Prompt and enter hello following commands:</span></span>

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

<span data-ttu-id="00225-212">Bu örnekte, depolama hesabınızın adını allvhdsje olduğundan, depolama alanı hesabı anahtarınız storageaccountkey ise ve rdma hello Azure dosya paylaşımı adı..</span><span class="sxs-lookup"><span data-stu-id="00225-212">In this example, allvhdsje is your storage account name, storageaccountkey is your storage account key, and rdma is hello Azure File share name.</span></span> <span data-ttu-id="00225-213">Hello Azure dosya paylaşımı Z: hello baş düğümünde bağlı.</span><span class="sxs-lookup"><span data-stu-id="00225-213">hello Azure File share is mounted as Z: on hello head node.</span></span>

<span data-ttu-id="00225-214">çalıştırma Linux düğümleri toomount hello Azure dosya paylaşımında bir **clusrun** hello baş düğümünde komutu.</span><span class="sxs-lookup"><span data-stu-id="00225-214">toomount hello Azure File share on Linux nodes, run a **clusrun** command on hello head node.</span></span> <span data-ttu-id="00225-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)**  yararlı bir HPC Pack aracı toocarry yönetim görevlerini birden çok düğümde değil.</span><span class="sxs-lookup"><span data-stu-id="00225-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** is a useful HPC Pack tool toocarry out administrative tasks on multiple nodes.</span></span> <span data-ttu-id="00225-216">(Ayrıca bkz. [Clusrun Linux düğümleri için](#Clusrun-for-Linux-nodes) bu makalede.)</span><span class="sxs-lookup"><span data-stu-id="00225-216">(See also [Clusrun for Linux nodes](#Clusrun-for-Linux-nodes) in this article.)</span></span>

<span data-ttu-id="00225-217">Bir Windows PowerShell penceresi açın ve aşağıdaki komutları hello girin:</span><span class="sxs-lookup"><span data-stu-id="00225-217">Open a Windows PowerShell window and enter hello following commands:</span></span>

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

<span data-ttu-id="00225-218">Merhaba ilk komut hello LinuxNodes grubundaki tüm düğümlerde /rdma adlı bir klasör oluşturur.</span><span class="sxs-lookup"><span data-stu-id="00225-218">hello first command creates a folder named /rdma on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="00225-219">Merhaba ikinci komut hello Azure dosya paylaşımı allvhdsjw.file.core.windows.net/rdma hello /rdma dir ve dosya modu BITS kümesi too777 klasörüyle üzerine bağlar.</span><span class="sxs-lookup"><span data-stu-id="00225-219">hello second command mounts hello Azure File share allvhdsjw.file.core.windows.net/rdma onto hello /rdma folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="00225-220">Merhaba ikinci komutta allvhdsje depolama hesabınızın adını ve storageaccountkey depolama hesabı anahtarınızı.</span><span class="sxs-lookup"><span data-stu-id="00225-220">In hello second command, allvhdsje is your storage account name and storageaccountkey is your storage account key.</span></span>

> [!NOTE]
> <span data-ttu-id="00225-221">Merhaba "\\`" Merhaba ikinci komut dosyasındaki simge olan PowerShell bir kaçış simgesi.</span><span class="sxs-lookup"><span data-stu-id="00225-221">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="00225-222">"\\`,"anlamına gelir, hello"," (virgül karakteri) hello komutu bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="00225-222">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="head-node-share"></a><span data-ttu-id="00225-223">Baş düğüm paylaşımı</span><span class="sxs-lookup"><span data-stu-id="00225-223">Head node share</span></span>
<span data-ttu-id="00225-224">Alternatif olarak, paylaşılan bir klasöre hello baş düğümü Linux düğümleri üzerinde bağlayın.</span><span class="sxs-lookup"><span data-stu-id="00225-224">Alternatively, mount a shared folder of hello head node on Linux nodes.</span></span> <span data-ttu-id="00225-225">Bir paylaşım hello en basit yolu tooshare dosyaları sağlar, ancak hello baş düğümü ve tüm Linux düğümleri hello dağıtılmalıdır aynı sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="00225-225">A share provides hello simplest way tooshare files, but hello head node and all Linux nodes must be deployed in hello same virtual network.</span></span> <span data-ttu-id="00225-226">Merhaba adımlar şunlardır.</span><span class="sxs-lookup"><span data-stu-id="00225-226">Here are hello steps.</span></span>

1. <span data-ttu-id="00225-227">Merhaba baş düğüm üzerinde bir klasör oluşturun ve okuma/yazma izinlerine sahip tooEveryone paylaşın.</span><span class="sxs-lookup"><span data-stu-id="00225-227">Create a folder on hello head node and share it tooEveryone with Read/Write permissions.</span></span> <span data-ttu-id="00225-228">Örneğin, hello baş düğümü olarak D:\OpenFOAM paylaşım \\CentOS7RDMA HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="00225-228">For example, share D:\OpenFOAM on hello head node as \\CentOS7RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="00225-229">Burada CentOS7RDMA HN hello baş düğüm hello barındırıcı adıdır.</span><span class="sxs-lookup"><span data-stu-id="00225-229">Here CentOS7RDMA-HN is hello hostname of hello head node.</span></span>
   
    ![Dosya paylaşım izinleri][fileshareperms]
   
    ![Dosya Paylaşımı][filesharing]
2. <span data-ttu-id="00225-232">Bir Windows PowerShell penceresi açın ve hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="00225-232">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="00225-233">Merhaba ilk komut hello LinuxNodes grubundaki tüm düğümlerde /openfoam adlı bir klasör oluşturur.</span><span class="sxs-lookup"><span data-stu-id="00225-233">hello first command creates a folder named /openfoam on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="00225-234">Merhaba ikinci komut hello paylaşılan klasör //CentOS7RDMA-HN/OpenFOAM dir ve dosya modu BITS kümesi too777 hello klasörüyle üzerine bağlar.</span><span class="sxs-lookup"><span data-stu-id="00225-234">hello second command mounts hello shared folder //CentOS7RDMA-HN/OpenFOAM onto hello folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="00225-235">Merhaba kullanıcı adı ve parola hello komutta hello kullanıcı adı ve parola bir küme kullanıcının hello baş düğüm üzerinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="00225-235">hello username and password in hello command should be hello username and password of a cluster user on hello head node.</span></span> <span data-ttu-id="00225-236">(Bkz [ekleme veya kaldırma küme kullanıcılar](https://technet.microsoft.com/library/ff919330.aspx).)</span><span class="sxs-lookup"><span data-stu-id="00225-236">(See [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).)</span></span>

> [!NOTE]
> <span data-ttu-id="00225-237">Merhaba "\\`" Merhaba ikinci komut dosyasındaki simge olan PowerShell bir kaçış simgesi.</span><span class="sxs-lookup"><span data-stu-id="00225-237">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="00225-238">"\\`,"anlamına gelir, hello"," (virgül karakteri) hello komutu bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="00225-238">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="nfs-server"></a><span data-ttu-id="00225-239">NFS sunucusu</span><span class="sxs-lookup"><span data-stu-id="00225-239">NFS server</span></span>
<span data-ttu-id="00225-240">Merhaba NFS hizmeti ve dosyalar hello SMB protokolünü kullanarak hello Windows Server 2012 işletim sistemi çalıştıran bilgisayarlar ile hello NFS protokolünü kullanarak Linux tabanlı bilgisayarlar arasında geçirmek tooshare sağlar.</span><span class="sxs-lookup"><span data-stu-id="00225-240">hello NFS service enables you tooshare and migrate files between computers running hello Windows Server 2012 operating system using hello SMB protocol and Linux-based computers using hello NFS protocol.</span></span> <span data-ttu-id="00225-241">Merhaba NFS sunucusu ve diğer tüm düğümlere dağıtılan hello toobe sahip aynı sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="00225-241">hello NFS server and all other nodes have toobe deployed in hello same virtual network.</span></span> <span data-ttu-id="00225-242">Linux düğümleriyle SMB paylaşımı ile karşılaştırıldığında daha iyi uyumluluk sağlar.</span><span class="sxs-lookup"><span data-stu-id="00225-242">It provides better compatibility with Linux nodes compared with an SMB share.</span></span> <span data-ttu-id="00225-243">Örneğin, dosya bağlantıları destekler.</span><span class="sxs-lookup"><span data-stu-id="00225-243">For example, it supports file links.</span></span>

1. <span data-ttu-id="00225-244">tooinstall ve bir NFS sunucusunun ayarlama izleyin hello adımlarda [sunucusu için ağ dosya sistemi ilk paylaşımını uçtan uca](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span><span class="sxs-lookup"><span data-stu-id="00225-244">tooinstall and set up an NFS server, follow hello steps in [Server for Network File System First Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span></span>
   
    <span data-ttu-id="00225-245">Örneğin, aşağıdaki özelliklere hello ile nfs adlı bir NFS paylaşımına oluşturun:</span><span class="sxs-lookup"><span data-stu-id="00225-245">For example, create an NFS share named nfs with hello following properties:</span></span>
   
    ![NFS yetkilendirme][nfsauth]
   
    ![NFS paylaşım izinlerini][nfsshare]
   
    ![NFS NTFS izinleri][nfsperm]
   
    ![NFS yönetim özellikleri][nfsmanage]
2. <span data-ttu-id="00225-250">Bir Windows PowerShell penceresi açın ve hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="00225-250">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   <span data-ttu-id="00225-251">Merhaba ilk komut hello LinuxNodes grubundaki tüm düğümlerde /nfsshared adlı bir klasör oluşturur.</span><span class="sxs-lookup"><span data-stu-id="00225-251">hello first command creates a folder named /nfsshared on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="00225-252">Merhaba ikinci komutu başlatmalar hello NFS paylaşım CentOS7RDMA HN: / nfs üzerine hello klasör.</span><span class="sxs-lookup"><span data-stu-id="00225-252">hello second command mounts hello NFS share CentOS7RDMA-HN:/nfs onto hello folder.</span></span> <span data-ttu-id="00225-253">Burada CentOS7RDMA HN: nfs olduğu, bir NFS paylaşımına hello uzak yolu.</span><span class="sxs-lookup"><span data-stu-id="00225-253">Here CentOS7RDMA-HN:/nfs is hello remote path of your NFS share.</span></span>

## <a name="how-toosubmit-jobs"></a><span data-ttu-id="00225-254">Nasıl toosubmit işleri</span><span class="sxs-lookup"><span data-stu-id="00225-254">How toosubmit jobs</span></span>
<span data-ttu-id="00225-255">Çeşitli yolları toosubmit işleri toohello HPC paketi küme vardır:</span><span class="sxs-lookup"><span data-stu-id="00225-255">There are several ways toosubmit jobs toohello HPC Pack cluster:</span></span>

* <span data-ttu-id="00225-256">HPC Küme Yöneticisi'ni veya HPC İş Yöneticisi GUI</span><span class="sxs-lookup"><span data-stu-id="00225-256">HPC Cluster Manager or HPC Job Manager GUI</span></span>
* <span data-ttu-id="00225-257">HPC web portalı</span><span class="sxs-lookup"><span data-stu-id="00225-257">HPC web portal</span></span>
* <span data-ttu-id="00225-258">REST API</span><span class="sxs-lookup"><span data-stu-id="00225-258">REST API</span></span>

<span data-ttu-id="00225-259">HPC Pack GUI araçları ve hello HPC web Portalı aracılığıyla Azure toohello küme olan hello aynı Windows işlem düğümleri için olduğu gibi iş gönderme.</span><span class="sxs-lookup"><span data-stu-id="00225-259">Job submission toohello cluster in Azure via HPC Pack GUI tools and hello HPC web portal are hello same as for Windows compute nodes.</span></span> <span data-ttu-id="00225-260">Bkz: [HPC Pack İş Yöneticisi](https://technet.microsoft.com/library/ff919691.aspx) ve [nasıl toosubmit bir şirket içi istemci bilgisayarından işleri](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="00225-260">See [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) and [How toosubmit jobs from an on-premises client computer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="00225-261">Merhaba REST API aracılığıyla toosubmit işleri başvurmak çok[oluşturma ve gönderme işleri kullanarak REST API Microsoft HPC Pack Merhaba](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="00225-261">toosubmit jobs via hello REST API, refer too[Creating and Submitting Jobs by Using hello REST API in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span> <span data-ttu-id="00225-262">bir Linux istemciden toosubmit işleri ayrıca hello toohello Python örnek başvuru [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span><span class="sxs-lookup"><span data-stu-id="00225-262">toosubmit jobs from a Linux client, also refer toohello Python sample in hello [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span></span>

## <a name="clusrun-for-linux-nodes"></a><span data-ttu-id="00225-263">Linux düğümleri için Clusrun</span><span class="sxs-lookup"><span data-stu-id="00225-263">Clusrun for Linux nodes</span></span>
<span data-ttu-id="00225-264">HPC Pack Merhaba [clusrun](https://technet.microsoft.com/library/cc947685.aspx) aracı Linux düğümleri ya da bir komut istemini veya HPC Küme Yöneticisi aracılığıyla kullanılan tooexecute komutlarını olabilir.</span><span class="sxs-lookup"><span data-stu-id="00225-264">hello HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) tool can be used tooexecute commands on Linux nodes either through a Command Prompt or HPC Cluster Manager.</span></span> <span data-ttu-id="00225-265">Temel bazı örnekler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="00225-265">Following are some basic examples.</span></span>

* <span data-ttu-id="00225-266">Merhaba kümedeki tüm düğümlerde geçerli kullanıcı adlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="00225-266">Show current user names on all nodes in hello cluster.</span></span>
  
    ```command
    clusrun whoami
    ```
* <span data-ttu-id="00225-267">Merhaba yüklemek **gdb** hata ayıklayıcısı aracı ile **yum** linuxnodes grup ve hello düğümleri 10 dakika sonra yeniden hello tüm düğümlerde.</span><span class="sxs-lookup"><span data-stu-id="00225-267">Install hello **gdb** debugger tool with **yum** on all nodes in hello linuxnodes group and then restart hello nodes after 10 minutes.</span></span>
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* <span data-ttu-id="00225-268">Hello kümedeki her numarası 1 ile 10 her Linux düğümde bir saniye için görüntüleme bir kabuk betiği oluşturmak, çalıştırmak ve çıktı hello düğümlerinden hemen göster.</span><span class="sxs-lookup"><span data-stu-id="00225-268">Create a shell script displaying each number 1 through 10 for one second on each Linux node in hello cluster, run it, and show output from hello nodes immediately.</span></span>
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> <span data-ttu-id="00225-269">Toouse gerekebilecek belirli kaçış karakterleri **clusrun** komutları.</span><span class="sxs-lookup"><span data-stu-id="00225-269">You might need toouse certain escape characters in **clusrun** commands.</span></span> <span data-ttu-id="00225-270">Bu örnekte gösterildiği gibi kullanın ^ bir komut istemi tooescape hello içinde ">" simgesi.</span><span class="sxs-lookup"><span data-stu-id="00225-270">As shown in this example, use ^ in a Command Prompt tooescape hello ">" symbol.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="00225-271">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="00225-271">Next steps</span></span>
* <span data-ttu-id="00225-272">Merhaba küme tooa fazla sayıda düğüm ölçeklendirme deneyin veya Linux iş yükü hello kümede çalıştırmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="00225-272">Try scaling up hello cluster tooa larger number of nodes, or try running a Linux workload on hello cluster.</span></span> <span data-ttu-id="00225-273">Bir örnek için bkz: [çalıştırmak NAMD Microsoft HPC Pack Linux işlem düğümlerini Azure](hpcpack-cluster-namd.md).</span><span class="sxs-lookup"><span data-stu-id="00225-273">For an example, see [Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure](hpcpack-cluster-namd.md).</span></span>
* <span data-ttu-id="00225-274">Bir küme ile deneyin [RDMA özellikli, işlem yoğunluklu VM'ler](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI iş yükleri.</span><span class="sxs-lookup"><span data-stu-id="00225-274">Try a cluster with [RDMA-capable, compute-intensive VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI workloads.</span></span> <span data-ttu-id="00225-275">Bir örnek için bkz: [çalıştırmak OpenFOAM Linux RDMA üzerinde Microsoft HPC Pack ile küme Azure'da](hpcpack-cluster-openfoam.md).</span><span class="sxs-lookup"><span data-stu-id="00225-275">For an example, see [Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](hpcpack-cluster-openfoam.md).</span></span>
* <span data-ttu-id="00225-276">İçinde bir şirket içi HPC Pack kümesindeki Linux düğümleri ile çalışma ilgileniyorsanız hello bkz [TechNet Kılavuzu](https://technet.microsoft.com/library/mt595803.aspx).</span><span class="sxs-lookup"><span data-stu-id="00225-276">If you are interested in working with Linux nodes in an on-premises HPC Pack cluster, see hello [TechNet guidance](https://technet.microsoft.com/library/mt595803.aspx).</span></span>

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png
