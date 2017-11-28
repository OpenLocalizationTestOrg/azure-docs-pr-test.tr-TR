---
title: "Linux sanal makineleri bir HPC paketi küme işlem | Microsoft Docs"
description: "Oluşturma ve Linux yüksek performanslı bilgi işlem (HPC) iş yükleri için Azure'da bir HPC Pack kümesi kullanma hakkında bilgi edinin"
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
ms.openlocfilehash: 809d3944311badf265117d353b65642e044d900c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="c2c32-103">Azure’daki bir HPC Pack kümesinde Linux işlem düğümleri kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c2c32-103">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="c2c32-104">Ayarlanmış bir [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) küme Windows Server ve birkaç çalıştıran bir baş düğüm içeren Azure işlem desteklenen Linux dağıtım çalışan düğümleri.</span><span class="sxs-lookup"><span data-stu-id="c2c32-104">Set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure that contains a head node running Windows Server and several compute nodes running a supported Linux distribution.</span></span> <span data-ttu-id="c2c32-105">Linux düğümleri ve kümenin Windows baş düğüm arasında verileri taşımak için seçeneklerini araştırın.</span><span class="sxs-lookup"><span data-stu-id="c2c32-105">Explore options to move data among the Linux nodes and the Windows head node of the cluster.</span></span> <span data-ttu-id="c2c32-106">Kümeye Linux HPC iş gönderme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c2c32-106">Learn how to submit Linux HPC jobs to the cluster.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="c2c32-107">Yüksek düzeyde, aşağıdaki diyagramda HPC paketi küme oluşturun ve çalışmak gösterir.</span><span class="sxs-lookup"><span data-stu-id="c2c32-107">At a high level, the following diagram shows the HPC Pack cluster you create and work with.</span></span>

![Linux düğümleri ile HPC Pack kümesi][scenario]

<span data-ttu-id="c2c32-109">Diğer Seçenekler Linux HPC iş yüklerini Azure'da çalışması, bkz: [toplu işlem ve yüksek performanslı bilgi işlem için teknik kaynaklar](../../../batch/big-compute-resources.md).</span><span class="sxs-lookup"><span data-stu-id="c2c32-109">For other options to run Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/big-compute-resources.md).</span></span>

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a><span data-ttu-id="c2c32-110">Linux işlem düğümlerini içeren bir HPC Pack kümeyi dağıtma</span><span class="sxs-lookup"><span data-stu-id="c2c32-110">Deploy an HPC Pack cluster with Linux compute nodes</span></span>
<span data-ttu-id="c2c32-111">Bu makale, Azure Linux HPC Pack kümede dağıtmak için iki seçenek işlem düğümleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="c2c32-111">This article shows you two options to deploy an HPC Pack cluster in Azure with Linux compute nodes.</span></span> <span data-ttu-id="c2c32-112">Her iki yöntem Windows Server'ın bir Market görüntüsü baş düğüm oluşturmak için HPC Pack ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="c2c32-112">Both methods use a Marketplace image of Windows Server with HPC Pack to create the head node.</span></span> 

* <span data-ttu-id="c2c32-113">**Azure Resource Manager şablonu** -Resource Manager dağıtım modelinde kümenin oluşturmayı otomatikleştirmek için bir şablonu Azure Marketi'nden veya topluluktan hızlı başlatma şablonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="c2c32-113">**Azure Resource Manager template** - Use a template from the Azure Marketplace, or a quickstart template from the community, to automate creation of the cluster in the Resource Manager deployment model.</span></span> <span data-ttu-id="c2c32-114">Örneğin, [Linux iş yükleri için HPC paketi küme](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) Azure Marketi şablonunda Linux HPC için eksiksiz bir HPC paketi küme altyapı iş yükleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c2c32-114">For example, the [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in the Azure Marketplace creates a complete HPC Pack cluster infrastructure for Linux HPC workloads.</span></span>
* <span data-ttu-id="c2c32-115">**PowerShell Betiği** -kullanım [Microsoft HPC Pack Iaas dağıtım betiği](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**yeni HpcIaaSCluster.ps1**) Klasik dağıtım modelinde bir tam küme dağıtımı otomatik hale getirmek için.</span><span class="sxs-lookup"><span data-stu-id="c2c32-115">**PowerShell script** - Use the [Microsoft HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) to automate a complete cluster deployment in the classic deployment model.</span></span> <span data-ttu-id="c2c32-116">Bu Azure PowerShell Betiği hızlı dağıtımı için Azure Marketi'nde bir HPC Pack VM görüntüsü kullanır ve Linux işlem düğümlerini dağıtmak için yapılandırma parametrelerini kapsamlı bir kümesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="c2c32-116">This Azure PowerShell script uses an HPC Pack VM image in the Azure Marketplace for fast deployment and provides a comprehensive set of configuration parameters to deploy Linux compute nodes.</span></span>

<span data-ttu-id="c2c32-117">Azure içindeki HPC paketi küme dağıtım seçenekleri hakkında daha fazla bilgi için bkz: [küme oluşturmak ve yüksek performanslı hesaplama (HPC) yönetmek için seçenekleri Microsoft HPC Pack ile azure'da](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c2c32-117">For more information about HPC Pack cluster deployment options in Azure, see [Options to create and manage a high-performance computing (HPC) cluster in Azure with Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c2c32-118">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c2c32-118">Prerequisites</span></span>
* <span data-ttu-id="c2c32-119">**Azure aboneliği** -Azure genel veya Azure Çin hizmetinde bir aboneliği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2c32-119">**Azure subscription** - You can use a subscription in either the Azure Global or Azure China service.</span></span> <span data-ttu-id="c2c32-120">Bir hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="c2c32-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="c2c32-121">**Çekirdek kota** -özellikle çok çekirdekli VM boyutları birkaç küme düğümleri dağıtmak isterseniz, çekirdek, Kotayı artırmak gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c2c32-121">**Cores quota** - You might need to increase the quota of cores, especially if you choose to deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="c2c32-122">Bir Kotayı artırmak için ücretsiz bir çevrimiçi müşteri destek isteği açın.</span><span class="sxs-lookup"><span data-stu-id="c2c32-122">To increase a quota, open an online customer support request at no charge.</span></span>
* <span data-ttu-id="c2c32-123">**Linux dağıtımları** -şu anda HPC Pack aşağıdaki Linux dağıtımları için işlem düğümlerine destekler.</span><span class="sxs-lookup"><span data-stu-id="c2c32-123">**Linux distributions** - Currently HPC Pack supports the following Linux distributions for compute nodes.</span></span> <span data-ttu-id="c2c32-124">Bu dağıtımları Market sürümleri kullanılabiliyorsa kullanın veya kendi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="c2c32-124">You can use Marketplace versions of these distributions where available, or supply your own.</span></span>
  
  * <span data-ttu-id="c2c32-125">**CentOS tabanlı**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span><span class="sxs-lookup"><span data-stu-id="c2c32-125">**CentOS-based**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span></span>
  * <span data-ttu-id="c2c32-126">**Red Hat Enterprise Linux**: 6.7, 6,8, 7.2</span><span class="sxs-lookup"><span data-stu-id="c2c32-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span></span>
  * <span data-ttu-id="c2c32-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 HPC, SLES 12 HPC (Premium) için için</span><span class="sxs-lookup"><span data-stu-id="c2c32-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 for HPC, SLES 12 for HPC (Premium)</span></span>
  * <span data-ttu-id="c2c32-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="c2c32-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span></span>
    
    > [!TIP]
    > <span data-ttu-id="c2c32-129">Azure RDMA ağ RDMA özelliğine sahip VM boyutları biri ile kullanmak için Azure Marketi'nden bir SUSE Linux Enterprise Server 12 HPC veya CentOS tabanlı HPC görüntüsü belirtin.</span><span class="sxs-lookup"><span data-stu-id="c2c32-129">To use the Azure RDMA network with one of the RDMA-capable VM sizes, specify a SUSE Linux Enterprise Server 12 HPC or CentOS-based HPC image from the Azure Marketplace.</span></span> <span data-ttu-id="c2c32-130">Daha fazla bilgi için bkz: [yüksek performanslı işlem VM boyutları](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c2c32-130">For more information, see [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

<span data-ttu-id="c2c32-131">HPC Pack Iaas dağıtım komut dosyası kullanarak küme dağıtmak için ek önkoşulları:</span><span class="sxs-lookup"><span data-stu-id="c2c32-131">Additional prerequisites to deploy the cluster by using the HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="c2c32-132">**İstemci bilgisayar** -küme dağıtım betiğini çalıştırmak için bir Windows tabanlı bir istemci bilgisayar gerekir.</span><span class="sxs-lookup"><span data-stu-id="c2c32-132">**Client computer** - You need a Windows-based client computer to run the cluster deployment script.</span></span>
* <span data-ttu-id="c2c32-133">**Azure PowerShell** - [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview) (sürüm 0.8.10 veya üzeri) istemci bilgisayarınızda.</span><span class="sxs-lookup"><span data-stu-id="c2c32-133">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="c2c32-134">**HPC Pack Iaas dağıtım betiği** - karşıdan yükleme ve komut dosyasını en son sürümünü paket [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="c2c32-134">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="c2c32-135">Komut dosyasının sürümünü çalıştırarak denetleyebilirsiniz `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="c2c32-135">You can check the version of the script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="c2c32-136">Bu makalede, sürüm 4.4.1 veya daha sonra komut dosyasını temel alır.</span><span class="sxs-lookup"><span data-stu-id="c2c32-136">This article is based on version 4.4.1 or later of the script.</span></span>

### <a name="deployment-option-1-use-a-resource-manager-template"></a><span data-ttu-id="c2c32-137">Dağıtım seçeneği 1.</span><span class="sxs-lookup"><span data-stu-id="c2c32-137">Deployment option 1.</span></span> <span data-ttu-id="c2c32-138">Resource Manager şablonu kullanın</span><span class="sxs-lookup"><span data-stu-id="c2c32-138">Use a Resource Manager template</span></span>
1. <span data-ttu-id="c2c32-139">Git [Linux iş yükleri için HPC paketi küme](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) Azure Marketi ve tıklatın şablonunda **dağıtma**.</span><span class="sxs-lookup"><span data-stu-id="c2c32-139">Go to the [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in the Azure Marketplace, and click **Deploy**.</span></span>
2. <span data-ttu-id="c2c32-140">Azure Portalı'ndaki bilgileri gözden geçirin ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="c2c32-140">In the Azure portal, review the information and then click **Create**.</span></span>
   
    ![Portal oluşturma][portal]
3. <span data-ttu-id="c2c32-142">Üzerinde **Temelleri** dikey penceresinde de üstbilgi düğüm VM'ine adları küme için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="c2c32-142">On the **Basics** blade, enter a name for the cluster, which also names the head node VM.</span></span> <span data-ttu-id="c2c32-143">Varolan bir kaynak grubu seçin veya bir grup dağıtımı için kullanabileceğiniz bir konumda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c2c32-143">You can choose an existing resource group or create a group for the deployment in a location that's available to you.</span></span> <span data-ttu-id="c2c32-144">Konumun belirli VM boyutları ve diğer Azure hizmetleriyle kullanılabilirliğini etkiler (bkz [bölgeye göre ürünleri](https://azure.microsoft.com/regions/services/)).</span><span class="sxs-lookup"><span data-stu-id="c2c32-144">The location affects the availability of certain VM sizes and other Azure services (see [Products available by region](https://azure.microsoft.com/regions/services/)).</span></span>
4. <span data-ttu-id="c2c32-145">Üzerinde **düğümü ayarları Head** dikey penceresinde, ilk dağıtım için genellikle varsayılan ayarları kabul edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2c32-145">On the **Head node settings** blade, for a first deployment, you can generally accept the default settings.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="c2c32-146">**Sonrası yapılandırma betiği URL'si** çalışmaya başladıktan sonra baş düğümünde VM çalıştırmak istediğiniz genel kullanıma açık bir Windows PowerShell komut dosyasını belirtmek için isteğe bağlı bir ayardır.</span><span class="sxs-lookup"><span data-stu-id="c2c32-146">The **Post-configuration script URL** is an optional setting to specify a publicly available Windows PowerShell script that you want to run on the head node VM after it is running.</span></span> 
   > 
   > 
5. <span data-ttu-id="c2c32-147">Üzerinde **düğümü ayarları işlem** bir adlandırma deseni dikey penceresinde, select düğümleri, sayısını ve boyutunu düğümleri ve Linux dağıtım dağıtmak.</span><span class="sxs-lookup"><span data-stu-id="c2c32-147">On the **Compute node settings** blade, select a naming pattern for the nodes, the number and size of the nodes, and the Linux distribution to deploy.</span></span>
6. <span data-ttu-id="c2c32-148">Üzerinde **Altyapı ayarlarını** dikey penceresinde, sanal ağ ve Active Directory adlarını girin etki alanı, etki alanı ve VM yönetici kimlik bilgileri ve depolama hesapları için bir adlandırma deseni.</span><span class="sxs-lookup"><span data-stu-id="c2c32-148">On the **Infrastructure settings** blade, enter names for the virtual network and Active Directory domain, domain and VM administrator credentials, and a naming pattern for the storage accounts.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c2c32-149">HPC Pack Active Directory etki alanı küme kullanıcıların kimliklerini doğrulamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="c2c32-149">HPC Pack uses the Active Directory domain to authenticate cluster users.</span></span> 
   > 
   > 
7. <span data-ttu-id="c2c32-150">Doğrulama testlerini çalıştırmak ve kullanım koşullarını gözden geçirin sonra tıklayın **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="c2c32-150">After the validation tests run and you review the terms of use, click **Purchase**.</span></span>

### <a name="deployment-option-2-use-the-iaas-deployment-script"></a><span data-ttu-id="c2c32-151">Dağıtım seçeneği 2.</span><span class="sxs-lookup"><span data-stu-id="c2c32-151">Deployment option 2.</span></span> <span data-ttu-id="c2c32-152">Iaas dağıtım komut dosyası kullan</span><span class="sxs-lookup"><span data-stu-id="c2c32-152">Use the IaaS deployment script</span></span>
<span data-ttu-id="c2c32-153">HPC Pack Iaas dağıtım komut dosyası kullanarak küme dağıtmak için ek ön koşullar aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="c2c32-153">Following are additional prerequisites to deploy the cluster by using the HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="c2c32-154">**İstemci bilgisayar** -küme dağıtım betiğini çalıştırmak için bir Windows tabanlı bir istemci bilgisayar gerekir.</span><span class="sxs-lookup"><span data-stu-id="c2c32-154">**Client computer** - You need a Windows-based client computer to run the cluster deployment script.</span></span>
* <span data-ttu-id="c2c32-155">**Azure PowerShell** - [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview) (sürüm 0.8.10 veya üzeri) istemci bilgisayarınızda.</span><span class="sxs-lookup"><span data-stu-id="c2c32-155">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="c2c32-156">**HPC Pack Iaas dağıtım betiği** - karşıdan yükleme ve komut dosyasını en son sürümünü paket [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="c2c32-156">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="c2c32-157">Komut dosyasının sürümünü çalıştırarak denetleyebilirsiniz `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="c2c32-157">You can check the version of the script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="c2c32-158">Bu makalede, sürüm 4.4.1 veya daha sonra komut dosyasını temel alır.</span><span class="sxs-lookup"><span data-stu-id="c2c32-158">This article is based on version 4.4.1 or later of the script.</span></span>

<span data-ttu-id="c2c32-159">**XML yapılandırma dosyası**</span><span class="sxs-lookup"><span data-stu-id="c2c32-159">**XML configuration file**</span></span>

<span data-ttu-id="c2c32-160">HPC Pack Iaas dağıtım betiği HPC küme açıklamak için giriş olarak bir XML yapılandırma dosyasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="c2c32-160">The HPC Pack IaaS deployment script uses an XML configuration file as input to describe the  HPC cluster.</span></span> <span data-ttu-id="c2c32-161">Aşağıdaki örnek yapılandırma dosyası bir HPC paketi üstbilgi düğümü ve iki boyutu A7 CentOS 7.0 Linux işlem düğümleri oluşan küçük bir küme belirtir.</span><span class="sxs-lookup"><span data-stu-id="c2c32-161">The following sample configuration file specifies a small cluster consisting of an HPC Pack head node and two size A7 CentOS 7.0 Linux compute nodes.</span></span> 

<span data-ttu-id="c2c32-162">Dosya ortamınız ve istenen küme yapılandırması için gereken şekilde değiştirin ve HPCDemoConfig.xml gibi bir adla kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c2c32-162">Modify the file as needed for your environment and desired cluster configuration, and save it with a name such as HPCDemoConfig.xml.</span></span> <span data-ttu-id="c2c32-163">Örneğin, abonelik adı ve benzersiz depolama hesabı adı girin ve hizmet adı bulut gerekir.</span><span class="sxs-lookup"><span data-stu-id="c2c32-163">For example, you need to supply your subscription name and a unique storage account name and cloud service name.</span></span> <span data-ttu-id="c2c32-164">Ayrıca, işlem düğümleri için farklı bir desteklenen Linux görüntüsü seçin isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2c32-164">Additionally, you might want to choose a different supported Linux image for the compute nodes.</span></span> <span data-ttu-id="c2c32-165">Yapılandırma dosyasındaki öğeler hakkında daha fazla bilgi için komut dosyası klasöründeki Manual.rtf dosyasına bakın ve [HPC Kümesi ile HPC Pack Iaas dağıtım komut dosyası oluşturma](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c2c32-165">For more information about the elements in the configuration file, see the Manual.rtf file in the script folder and [Create an HPC cluster with the HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

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

<span data-ttu-id="c2c32-166">**HPC Pack Iaas dağıtım betiğini çalıştırmak için**</span><span class="sxs-lookup"><span data-stu-id="c2c32-166">**To run the HPC Pack IaaS deployment script**</span></span>

1. <span data-ttu-id="c2c32-167">Windows PowerShell istemci bilgisayarda yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="c2c32-167">Open Windows PowerShell on the client computer as an administrator.</span></span>
2. <span data-ttu-id="c2c32-168">Değişiklik komut dosyasının olduğu klasöre directory (Bu örnekte E:\IaaSClusterScript) yüklü.</span><span class="sxs-lookup"><span data-stu-id="c2c32-168">Change directory to the folder where the script is installed (E:\IaaSClusterScript in this example).</span></span>
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. <span data-ttu-id="c2c32-169">HPC Pack küme dağıtmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c2c32-169">Run the following command to deploy the HPC Pack cluster.</span></span> <span data-ttu-id="c2c32-170">Bu örnekte, yapılandırma dosyası E:\HPCDemoConfig.xml içinde bulunduğu varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c2c32-170">This example assumes that the configuration file is located in E:\HPCDemoConfig.xml</span></span>
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    <span data-ttu-id="c2c32-171">a.</span><span class="sxs-lookup"><span data-stu-id="c2c32-171">a.</span></span> <span data-ttu-id="c2c32-172">Çünkü **Admınpassword** önceki komutta, sorulur kullanıcı için parolayı girmek için belirtilmemiş *MyAdminName*.</span><span class="sxs-lookup"><span data-stu-id="c2c32-172">Because the **AdminPassword** is not specified in the preceding command, you are prompted to enter the password for user *MyAdminName*.</span></span>
   
    <span data-ttu-id="c2c32-173">b.</span><span class="sxs-lookup"><span data-stu-id="c2c32-173">b.</span></span> <span data-ttu-id="c2c32-174">Yapılandırma dosyasını doğrulamak komut dosyası sonra başlar.</span><span class="sxs-lookup"><span data-stu-id="c2c32-174">The script then starts to validate the configuration file.</span></span> <span data-ttu-id="c2c32-175">Bu ağ bağlantısı bağlı olarak birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="c2c32-175">It can take up to several minutes depending on the network connection.</span></span>
   
    ![Doğrulama][validate]
   
    <span data-ttu-id="c2c32-177">c.</span><span class="sxs-lookup"><span data-stu-id="c2c32-177">c.</span></span> <span data-ttu-id="c2c32-178">Doğrulama geçirmek sonra komut dosyasını oluşturmak için küme kaynaklarını listeler.</span><span class="sxs-lookup"><span data-stu-id="c2c32-178">After validations pass, the script lists the cluster resources to create.</span></span> <span data-ttu-id="c2c32-179">Girin *Y* devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="c2c32-179">Enter *Y* to continue.</span></span>
   
    ![Kaynaklar][resources]
   
    <span data-ttu-id="c2c32-181">d.</span><span class="sxs-lookup"><span data-stu-id="c2c32-181">d.</span></span> <span data-ttu-id="c2c32-182">Komut dosyası HPC paketi küme dağıtmak başlar ve daha fazla el ile adımlar olmadan yapılandırmasını tamamlar.</span><span class="sxs-lookup"><span data-stu-id="c2c32-182">The script starts to deploy the HPC Pack cluster and completes the configuration without further manual steps.</span></span> <span data-ttu-id="c2c32-183">Komut dosyası için birkaç dakika çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="c2c32-183">The script can run for several minutes.</span></span>
   
    ![Dağıtma][deploy]
   
   > [!NOTE]
   > <span data-ttu-id="c2c32-185">Otomatik olarak beri bir günlük dosyası bu örnekte, komut dosyasını oluşturur **- günlük dosyası** parametresinde değil.</span><span class="sxs-lookup"><span data-stu-id="c2c32-185">In this example, the script generates a log file automatically since the **-LogFile** parameter isn't specified.</span></span> <span data-ttu-id="c2c32-186">Günlükler gerçek zamanlı olarak yazılmış değil, ancak doğrulama ve dağıtımını sonunda toplanır.</span><span class="sxs-lookup"><span data-stu-id="c2c32-186">The logs aren't written in real time, but are collected at the end of the validation and the deployment.</span></span> <span data-ttu-id="c2c32-187">Komut dosyası çalışırken PowerShell işlem durursa, bazı günlükleri kaybolur.</span><span class="sxs-lookup"><span data-stu-id="c2c32-187">If the PowerShell process is stopped while the script is running, some logs are lost.</span></span>
   > 
   > 

## <a name="connect-to-the-head-node"></a><span data-ttu-id="c2c32-188">Baş düğümüne bağlanmak</span><span class="sxs-lookup"><span data-stu-id="c2c32-188">Connect to the head node</span></span>
<span data-ttu-id="c2c32-189">Azure, HPC Pack kümede dağıttıktan sonra [tarafından Uzak Masaüstü Bağlantısı](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) kümeyi dağıttığınızda sağlanan üstbilgi düğüm VM'ine etki alanını kullanarak, kimlik bilgileri (örneğin, *hpc\\clusteradmin*).</span><span class="sxs-lookup"><span data-stu-id="c2c32-189">After you deploy the HPC Pack cluster in Azure, [connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to the head node VM using the domain credentials you provided when you deployed the cluster (for example, *hpc\\clusteradmin*).</span></span> <span data-ttu-id="c2c32-190">Küme baş düğümünden yönetin.</span><span class="sxs-lookup"><span data-stu-id="c2c32-190">You manage the cluster from the head node.</span></span>

<span data-ttu-id="c2c32-191">Baş düğümünde HPC paketi küme durumunu denetlemek için HPC Küme Yöneticisi'ni başlatın.</span><span class="sxs-lookup"><span data-stu-id="c2c32-191">On the head node, start HPC Cluster Manager to check the status of the HPC Pack cluster.</span></span> <span data-ttu-id="c2c32-192">Linux işlem düğümlerini Windows ile çalışacak şekilde İzleyici işlem düğümlerini ve, yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2c32-192">You can manage and monitor Linux compute nodes the same way you work with Windows compute nodes.</span></span> <span data-ttu-id="c2c32-193">Örneğin, listelenen Linux düğümleri bkz **kaynak yönetimi** (Bu düğümler dağıtılan **LinuxNode** şablonu).</span><span class="sxs-lookup"><span data-stu-id="c2c32-193">For example, you see the Linux nodes listed in **Resource Management** (these nodes are deployed with the **LinuxNode** template).</span></span>

![Düğüm Yönetimi][management]

<span data-ttu-id="c2c32-195">Ayrıca Linux düğümleri bkz **ısı Haritası** görünümü.</span><span class="sxs-lookup"><span data-stu-id="c2c32-195">You also see the Linux nodes in the **Heat Map** view.</span></span>

![Isı Haritası][heatmap]

## <a name="how-to-move-data-in-a-cluster-with-linux-nodes"></a><span data-ttu-id="c2c32-197">Linux düğümleri ile bir kümede veri taşıma</span><span class="sxs-lookup"><span data-stu-id="c2c32-197">How to move data in a cluster with Linux nodes</span></span>
<span data-ttu-id="c2c32-198">Linux düğümleri ve kümenin Windows baş düğüm arasında verileri taşımak için birkaç seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="c2c32-198">You have several choices to move data among Linux nodes and the Windows head node of the cluster.</span></span> <span data-ttu-id="c2c32-199">Aşağıdaki bölümlerde daha ayrıntılı açıklanan üç yaygın yöntemleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c2c32-199">Here are three common methods, described in more detail in the following sections:</span></span>

* <span data-ttu-id="c2c32-200">**Azure dosya** -Azure depolama alanında veri dosyalarını depolamak için yönetilen bir SMB dosya paylaşımı kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="c2c32-200">**Azure File** - Exposes a managed SMB file share to store data files in Azure storage.</span></span> <span data-ttu-id="c2c32-201">Farklı sanal ağlarda dağıtmış olsa bile Windows düğümleri ve Linux düğümleri bir Azure dosya paylaşımı bir sürücü veya klasöre aynı anda bağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="c2c32-201">Windows nodes and Linux nodes can mount an Azure File share as a drive or folder at the same time, even if they're deployed in different virtual networks.</span></span>
* <span data-ttu-id="c2c32-202">**Baş düğüm SMB paylaşımı** -Linux düğümleri üzerinde Windows standart bir paylaşılan klasör baş düğümü bağlar.</span><span class="sxs-lookup"><span data-stu-id="c2c32-202">**Head node SMB share** - Mounts a standard Windows shared folder of the head node on Linux nodes.</span></span>
* <span data-ttu-id="c2c32-203">**Baş düğüm NFS sunucusu** -karma Windows ve Linux ortamı için bir dosya paylaşımı çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="c2c32-203">**Head node NFS server**  - Provides a file-sharing solution for a mixed Windows and Linux environment.</span></span>

### <a name="azure-file-storage"></a><span data-ttu-id="c2c32-204">Azure dosya depolama</span><span class="sxs-lookup"><span data-stu-id="c2c32-204">Azure File storage</span></span>
<span data-ttu-id="c2c32-205">[Azure dosya](https://azure.microsoft.com/services/storage/files/) hizmetini standart SMB 2.1 protokolünü kullanan dosya paylaşımları sunar.</span><span class="sxs-lookup"><span data-stu-id="c2c32-205">The [Azure File](https://azure.microsoft.com/services/storage/files/) service exposes file shares using the standard SMB 2.1 protocol.</span></span> <span data-ttu-id="c2c32-206">Azure VM'ler ve cloud services bağlı paylaşımlar üzerinden uygulama bileşenleri arasında dosya verileri paylaşabilir ve şirket içi uygulamalara File storage API'si dosya verilerine erişebilir.</span><span class="sxs-lookup"><span data-stu-id="c2c32-206">Azure VMs and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share through the File storage API.</span></span> 

<span data-ttu-id="c2c32-207">Bir Azure dosya paylaşımı oluşturmak ve baş düğümünde bağlamak ayrıntılı adımlar için bkz: [Windows Azure File storage ile çalışmaya başlama](../../../storage/files/storage-how-to-use-files-windows.md).</span><span class="sxs-lookup"><span data-stu-id="c2c32-207">For detailed steps to create an Azure File share and mount it on the head node, see [Get started with Azure File storage on Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span></span> <span data-ttu-id="c2c32-208">Azure dosya paylaşımını Linux düğümlerinde bağlama için bkz: [Azure File storage'ı Linux ile kullanma konusunda](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c2c32-208">To mount the Azure File share on the Linux nodes, see [How to use Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="c2c32-209">Kalıcı bağlantıları kurmak için bkz: [Persisting bağlantıları Microsoft Azure dosyaları](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2c32-209">To set up persisting connections, see [Persisting connections to Microsoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span></span>

<span data-ttu-id="c2c32-210">Aşağıdaki örnekte, bir Azure dosya paylaşımı bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c2c32-210">In the following example, create an Azure File share on a storage account.</span></span> <span data-ttu-id="c2c32-211">Baş düğümünde ve paylaşımı bağlamak için bir komut istemi açın ve aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="c2c32-211">To mount the share on the head node, open a Command Prompt and enter the following commands:</span></span>

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

<span data-ttu-id="c2c32-212">Bu örnekte, depolama hesabınızın adını allvhdsje olduğundan, depolama alanı hesabı anahtarınız storageaccountkey ise ve rdma Azure dosya paylaşım adıdır.</span><span class="sxs-lookup"><span data-stu-id="c2c32-212">In this example, allvhdsje is your storage account name, storageaccountkey is your storage account key, and rdma is the Azure File share name.</span></span> <span data-ttu-id="c2c32-213">Azure dosya paylaşımı Z: baş düğümünde bağlı.</span><span class="sxs-lookup"><span data-stu-id="c2c32-213">The Azure File share is mounted as Z: on the head node.</span></span>

<span data-ttu-id="c2c32-214">Azure dosya paylaşımını Linux düğümleri üzerinde bağlama için çalıştırın bir **clusrun** baş düğüm komutu.</span><span class="sxs-lookup"><span data-stu-id="c2c32-214">To mount the Azure File share on Linux nodes, run a **clusrun** command on the head node.</span></span> <span data-ttu-id="c2c32-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)**  birden çok düğüm üzerinde yönetim görevlerini gerçekleştirmek için yararlı bir HPC Pack araçtır.</span><span class="sxs-lookup"><span data-stu-id="c2c32-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** is a useful HPC Pack tool to carry out administrative tasks on multiple nodes.</span></span> <span data-ttu-id="c2c32-216">(Ayrıca bkz. [Clusrun Linux düğümleri için](#Clusrun-for-Linux-nodes) bu makalede.)</span><span class="sxs-lookup"><span data-stu-id="c2c32-216">(See also [Clusrun for Linux nodes](#Clusrun-for-Linux-nodes) in this article.)</span></span>

<span data-ttu-id="c2c32-217">Bir Windows PowerShell penceresi açın ve aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="c2c32-217">Open a Windows PowerShell window and enter the following commands:</span></span>

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

<span data-ttu-id="c2c32-218">İlk komut LinuxNodes grubundaki tüm düğümlerde /rdma adlı bir klasör oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c2c32-218">The first command creates a folder named /rdma on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="c2c32-219">İkinci komut dir /rdma klasörüyle üzerine Azure dosya paylaşımı allvhdsjw.file.core.windows.net/rdma bağlar ve dosya modu BITS 777 ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c2c32-219">The second command mounts the Azure File share allvhdsjw.file.core.windows.net/rdma onto the /rdma folder with dir and file mode bits set to 777.</span></span> <span data-ttu-id="c2c32-220">İkinci komut içinde allvhdsje depolama hesabınızın adını ve storageaccountkey depolama hesabı anahtarınızı.</span><span class="sxs-lookup"><span data-stu-id="c2c32-220">In the second command, allvhdsje is your storage account name and storageaccountkey is your storage account key.</span></span>

> [!NOTE]
> <span data-ttu-id="c2c32-221">"\\`" İkinci komut dosyasındaki simge olan bir PowerShell kaçış simgesi.</span><span class="sxs-lookup"><span data-stu-id="c2c32-221">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="c2c32-222">"\\`," "," (virgül karakteri) komutun bir parçası olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c2c32-222">“\\`,” means that the “,” (comma character) is a part of the command.</span></span>
> 
> 

### <a name="head-node-share"></a><span data-ttu-id="c2c32-223">Baş düğüm paylaşımı</span><span class="sxs-lookup"><span data-stu-id="c2c32-223">Head node share</span></span>
<span data-ttu-id="c2c32-224">Alternatif olarak, paylaşılan bir klasöre baş düğümü Linux düğümleri üzerinde bağlayın.</span><span class="sxs-lookup"><span data-stu-id="c2c32-224">Alternatively, mount a shared folder of the head node on Linux nodes.</span></span> <span data-ttu-id="c2c32-225">Bir paylaşımı, dosyaları paylaşmak için en basit yolu sağlar, ancak baş düğüm ve tüm Linux düğümler aynı sanal ağda dağıtılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c2c32-225">A share provides the simplest way to share files, but the head node and all Linux nodes must be deployed in the same virtual network.</span></span> <span data-ttu-id="c2c32-226">Adımlar şunlardır.</span><span class="sxs-lookup"><span data-stu-id="c2c32-226">Here are the steps.</span></span>

1. <span data-ttu-id="c2c32-227">Baş düğüm üzerinde bir klasör oluşturun ve herkese okuma/yazma izinleri ile paylaşın.</span><span class="sxs-lookup"><span data-stu-id="c2c32-227">Create a folder on the head node and share it to Everyone with Read/Write permissions.</span></span> <span data-ttu-id="c2c32-228">Örneğin, baş düğüm D:\OpenFOAM paylaşmak \\CentOS7RDMA HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="c2c32-228">For example, share D:\OpenFOAM on the head node as \\CentOS7RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="c2c32-229">Burada CentOS7RDMA HN baş düğüm barındırıcı adıdır.</span><span class="sxs-lookup"><span data-stu-id="c2c32-229">Here CentOS7RDMA-HN is the hostname of the head node.</span></span>
   
    ![Dosya paylaşım izinleri][fileshareperms]
   
    ![Dosya Paylaşımı][filesharing]
2. <span data-ttu-id="c2c32-232">Bir Windows PowerShell penceresi açın ve aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c2c32-232">Open a Windows PowerShell window and run the following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="c2c32-233">İlk komut LinuxNodes grubundaki tüm düğümlerde /openfoam adlı bir klasör oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c2c32-233">The first command creates a folder named /openfoam on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="c2c32-234">İkinci komut dir klasörüyle üzerine paylaşılan klasör //CentOS7RDMA-HN/OpenFOAM bağlar ve dosya modu BITS 777 ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c2c32-234">The second command mounts the shared folder //CentOS7RDMA-HN/OpenFOAM onto the folder with dir and file mode bits set to 777.</span></span> <span data-ttu-id="c2c32-235">Kullanıcı adı ve parola komut kullanıcı adı ve parola bir küme kullanıcının baş düğüm olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c2c32-235">The username and password in the command should be the username and password of a cluster user on the head node.</span></span> <span data-ttu-id="c2c32-236">(Bkz [ekleme veya kaldırma küme kullanıcılar](https://technet.microsoft.com/library/ff919330.aspx).)</span><span class="sxs-lookup"><span data-stu-id="c2c32-236">(See [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).)</span></span>

> [!NOTE]
> <span data-ttu-id="c2c32-237">"\\`" İkinci komut dosyasındaki simge olan bir PowerShell kaçış simgesi.</span><span class="sxs-lookup"><span data-stu-id="c2c32-237">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="c2c32-238">"\\`," "," (virgül karakteri) komutun bir parçası olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c2c32-238">“\\`,” means that the “,” (comma character) is a part of the command.</span></span>
> 
> 

### <a name="nfs-server"></a><span data-ttu-id="c2c32-239">NFS sunucusu</span><span class="sxs-lookup"><span data-stu-id="c2c32-239">NFS server</span></span>
<span data-ttu-id="c2c32-240">NFS hizmeti paylaşma ve dosyaları SMB protokolünü kullanan Windows Server 2012 işletim sistemi çalıştıran bilgisayarlarda ve NFS protokolünü kullanarak Linux tabanlı bilgisayarlar arasında geçirmek etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="c2c32-240">The NFS service enables you to share and migrate files between computers running the Windows Server 2012 operating system using the SMB protocol and Linux-based computers using the NFS protocol.</span></span> <span data-ttu-id="c2c32-241">NFS sunucusu ve diğer tüm düğümlere aynı sanal ağda dağıtılmış gerekir.</span><span class="sxs-lookup"><span data-stu-id="c2c32-241">The NFS server and all other nodes have to be deployed in the same virtual network.</span></span> <span data-ttu-id="c2c32-242">Linux düğümleriyle SMB paylaşımı ile karşılaştırıldığında daha iyi uyumluluk sağlar.</span><span class="sxs-lookup"><span data-stu-id="c2c32-242">It provides better compatibility with Linux nodes compared with an SMB share.</span></span> <span data-ttu-id="c2c32-243">Örneğin, dosya bağlantıları destekler.</span><span class="sxs-lookup"><span data-stu-id="c2c32-243">For example, it supports file links.</span></span>

1. <span data-ttu-id="c2c32-244">Yüklemek ve bir NFS sunucusu kurmak için adımları [sunucusu için ağ dosya sistemi ilk paylaşımını uçtan uca](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2c32-244">To install and set up an NFS server, follow the steps in [Server for Network File System First Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span></span>
   
    <span data-ttu-id="c2c32-245">Örneğin, aşağıdaki özelliklere sahip nfs adlı bir NFS paylaşımına oluşturun:</span><span class="sxs-lookup"><span data-stu-id="c2c32-245">For example, create an NFS share named nfs with the following properties:</span></span>
   
    ![NFS yetkilendirme][nfsauth]
   
    ![NFS paylaşım izinlerini][nfsshare]
   
    ![NFS NTFS izinleri][nfsperm]
   
    ![NFS yönetim özellikleri][nfsmanage]
2. <span data-ttu-id="c2c32-250">Bir Windows PowerShell penceresi açın ve aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c2c32-250">Open a Windows PowerShell window and run the following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   <span data-ttu-id="c2c32-251">İlk komut LinuxNodes grubundaki tüm düğümlerde /nfsshared adlı bir klasör oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c2c32-251">The first command creates a folder named /nfsshared on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="c2c32-252">İkinci komut bir NFS paylaşımına CentOS7RDMA HN bağlar: / klasör üzerine nfs.</span><span class="sxs-lookup"><span data-stu-id="c2c32-252">The second command mounts the NFS share CentOS7RDMA-HN:/nfs onto the folder.</span></span> <span data-ttu-id="c2c32-253">Burada CentOS7RDMA HN: / nfs NFS paylaşımınızın uzak yoludur.</span><span class="sxs-lookup"><span data-stu-id="c2c32-253">Here CentOS7RDMA-HN:/nfs is the remote path of your NFS share.</span></span>

## <a name="how-to-submit-jobs"></a><span data-ttu-id="c2c32-254">İşlerini gönderme</span><span class="sxs-lookup"><span data-stu-id="c2c32-254">How to submit jobs</span></span>
<span data-ttu-id="c2c32-255">HPC Pack kümeye iş göndermek için birkaç yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="c2c32-255">There are several ways to submit jobs to the HPC Pack cluster:</span></span>

* <span data-ttu-id="c2c32-256">HPC Küme Yöneticisi'ni veya HPC İş Yöneticisi GUI</span><span class="sxs-lookup"><span data-stu-id="c2c32-256">HPC Cluster Manager or HPC Job Manager GUI</span></span>
* <span data-ttu-id="c2c32-257">HPC web portalı</span><span class="sxs-lookup"><span data-stu-id="c2c32-257">HPC web portal</span></span>
* <span data-ttu-id="c2c32-258">REST API</span><span class="sxs-lookup"><span data-stu-id="c2c32-258">REST API</span></span>

<span data-ttu-id="c2c32-259">HPC Pack GUI araçları ve HPC web Portalı aracılığıyla Azure kümeye iş gönderme olan Windows aynı işlem düğümleri.</span><span class="sxs-lookup"><span data-stu-id="c2c32-259">Job submission to the cluster in Azure via HPC Pack GUI tools and the HPC web portal are the same as for Windows compute nodes.</span></span> <span data-ttu-id="c2c32-260">Bkz: [HPC Pack İş Yöneticisi](https://technet.microsoft.com/library/ff919691.aspx) ve [bir şirket içi istemci bilgisayarından işlerini göndermek nasıl](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c2c32-260">See [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) and [How to submit jobs from an on-premises client computer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="c2c32-261">REST API aracılığıyla iş göndermek için bkz [oluşturma ve gönderme Microsoft HPC Pack REST API kullanarak işleri](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2c32-261">To submit jobs via the REST API, refer to [Creating and Submitting Jobs by Using the REST API in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span> <span data-ttu-id="c2c32-262">Bir Linux istemciden işlerini göndermek için de Python örnekte bkz [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span><span class="sxs-lookup"><span data-stu-id="c2c32-262">To submit jobs from a Linux client, also refer to the Python sample in the [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span></span>

## <a name="clusrun-for-linux-nodes"></a><span data-ttu-id="c2c32-263">Linux düğümleri için Clusrun</span><span class="sxs-lookup"><span data-stu-id="c2c32-263">Clusrun for Linux nodes</span></span>
<span data-ttu-id="c2c32-264">HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) aracı, Linux düğümleri ya da bir komut istemini veya HPC Küme Yöneticisi aracılığıyla komut yürütmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c2c32-264">The HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) tool can be used to execute commands on Linux nodes either through a Command Prompt or HPC Cluster Manager.</span></span> <span data-ttu-id="c2c32-265">Temel bazı örnekler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c2c32-265">Following are some basic examples.</span></span>

* <span data-ttu-id="c2c32-266">Kümedeki tüm düğümlerde geçerli kullanıcı adlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c2c32-266">Show current user names on all nodes in the cluster.</span></span>
  
    ```command
    clusrun whoami
    ```
* <span data-ttu-id="c2c32-267">Yükleme **gdb** hata ayıklayıcısı aracı ile **yum** tüm linuxnodes düğümler grup ve ardından düğümler 10 dakika sonra yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="c2c32-267">Install the **gdb** debugger tool with **yum** on all nodes in the linuxnodes group and then restart the nodes after 10 minutes.</span></span>
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* <span data-ttu-id="c2c32-268">Kümedeki her numarası 1 ile 10 her Linux düğümde bir saniye için görüntüleme bir kabuk betiği oluşturma çalıştırın ve çıkış düğümlerden hemen göster.</span><span class="sxs-lookup"><span data-stu-id="c2c32-268">Create a shell script displaying each number 1 through 10 for one second on each Linux node in the cluster, run it, and show output from the nodes immediately.</span></span>
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> <span data-ttu-id="c2c32-269">Belirli kaçış karakterleri gerekebilir **clusrun** komutları.</span><span class="sxs-lookup"><span data-stu-id="c2c32-269">You might need to use certain escape characters in **clusrun** commands.</span></span> <span data-ttu-id="c2c32-270">Bu örnekte gösterildiği gibi kullanın ^ kaçınmak için bir komut isteminde ">" simgesi.</span><span class="sxs-lookup"><span data-stu-id="c2c32-270">As shown in this example, use ^ in a Command Prompt to escape the ">" symbol.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c2c32-271">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c2c32-271">Next steps</span></span>
* <span data-ttu-id="c2c32-272">Fazla sayıda düğüm kümeye ölçeklendirme deneyin veya küme üzerinde bir Linux iş yükü çalıştırmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="c2c32-272">Try scaling up the cluster to a larger number of nodes, or try running a Linux workload on the cluster.</span></span> <span data-ttu-id="c2c32-273">Bir örnek için bkz: [çalıştırmak NAMD Microsoft HPC Pack Linux işlem düğümlerini Azure](hpcpack-cluster-namd.md).</span><span class="sxs-lookup"><span data-stu-id="c2c32-273">For an example, see [Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure](hpcpack-cluster-namd.md).</span></span>
* <span data-ttu-id="c2c32-274">Bir küme ile deneyin [RDMA özellikli, işlem yoğunluklu VM'ler](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) MPI iş yüklerini çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="c2c32-274">Try a cluster with [RDMA-capable, compute-intensive VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to run MPI workloads.</span></span> <span data-ttu-id="c2c32-275">Bir örnek için bkz: [çalıştırmak OpenFOAM Linux RDMA üzerinde Microsoft HPC Pack ile küme Azure'da](hpcpack-cluster-openfoam.md).</span><span class="sxs-lookup"><span data-stu-id="c2c32-275">For an example, see [Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](hpcpack-cluster-openfoam.md).</span></span>
* <span data-ttu-id="c2c32-276">İçinde bir şirket içi HPC Pack kümesindeki Linux düğümleri ile çalışma ilgileniyorsanız bkz [TechNet Kılavuzu](https://technet.microsoft.com/library/mt595803.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2c32-276">If you are interested in working with Linux nodes in an on-premises HPC Pack cluster, see the [TechNet guidance](https://technet.microsoft.com/library/mt595803.aspx).</span></span>

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
