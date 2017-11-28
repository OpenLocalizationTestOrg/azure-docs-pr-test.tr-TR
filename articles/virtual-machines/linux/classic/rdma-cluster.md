---
title: "bir Linux RDMA küme toorun MPI uygulamaları aaaSet | Microsoft Docs"
description: "Linux kümesi boyutu H16r, H16mr, A8 veya A9 Vm'lerde toouse hello Azure RDMA ağ toorun MPI uygulamaları oluşturma"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 01834bad-c8e6-48a3-b066-7f1719047dd2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.openlocfilehash: 3199317a37b095e80718d6724954687d30aea3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-linux-rdma-cluster-toorun-mpi-applications"></a><span data-ttu-id="958cb-103">Bir Linux RDMA küme toorun MPI uygulama ayarlama</span><span class="sxs-lookup"><span data-stu-id="958cb-103">Set up a Linux RDMA cluster toorun MPI applications</span></span>
<span data-ttu-id="958cb-104">Azure ile Linux RDMA yukarı tooset nasıl kümesi öğrenin [yüksek performanslı işlem VM boyutları](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun paralel ileti geçirme arabirimi (MPI) uygulamalarını.</span><span class="sxs-lookup"><span data-stu-id="958cb-104">Learn how tooset up a Linux RDMA cluster in Azure with [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun parallel Message Passing Interface (MPI) applications.</span></span> <span data-ttu-id="958cb-105">Bu makale, bir kümede Linux HPC görüntü toorun Intel MPI adımları tooprepare sağlar.</span><span class="sxs-lookup"><span data-stu-id="958cb-105">This article provides steps tooprepare a Linux HPC image toorun Intel MPI on a cluster.</span></span> <span data-ttu-id="958cb-106">Hazırlık sonra bu görüntü ve hello RDMA özellikli Azure VM boyutlarını (şu anda H16r, H16mr, A8 veya A9) birini kullanarak sanal makineleri bir küme dağıtın.</span><span class="sxs-lookup"><span data-stu-id="958cb-106">After preparation, you deploy a cluster of VMs using this image and one of hello RDMA-capable Azure VM sizes (currently H16r, H16mr, A8, or A9).</span></span> <span data-ttu-id="958cb-107">Doğrudan uzak bellek erişimi (RDMA) teknolojisine dayalı düşük gecikmeli, yüksek verimlilik bir ağ üzerinden verimli bir şekilde iletişim hello küme toorun MPI uygulamaları kullanın.</span><span class="sxs-lookup"><span data-stu-id="958cb-107">Use hello cluster toorun MPI applications that communicate efficiently over a low-latency, high-throughput network based on remote direct memory access (RDMA) technology.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="958cb-108">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager](../../../resource-manager-deployment-model.md) ve klasik.</span><span class="sxs-lookup"><span data-stu-id="958cb-108">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="958cb-109">Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="958cb-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="958cb-110">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="958cb-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

## <a name="cluster-deployment-options"></a><span data-ttu-id="958cb-111">Küme dağıtım seçenekleri</span><span class="sxs-lookup"><span data-stu-id="958cb-111">Cluster deployment options</span></span>
<span data-ttu-id="958cb-112">Aşağıdaki yöntemlerdir ile veya iş Zamanlayıcı olmadan toocreate Linux RDMA küme kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="958cb-112">Following are methods you can use toocreate a Linux RDMA cluster with or without a job scheduler.</span></span>

* <span data-ttu-id="958cb-113">**Azure CLI betikleri**: Bu makalenin sonraki bölümlerinde gösterildiği gibi hello kullanın [Azure komut satırı arabirimi](../../../cli-install-nodejs.md) (CLI) tooscript hello RDMA özellikli VM'lerin bir küme dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="958cb-113">**Azure CLI scripts**: As shown later in this article, use hello [Azure command-line interface](../../../cli-install-nodejs.md) (CLI) tooscript hello deployment of a cluster of RDMA-capable VMs.</span></span> <span data-ttu-id="958cb-114">çok sayıda işlem düğümleri dağıtma birkaç dakika sürebilir için hizmet yönetimi modu hello CLI hello küme düğümleri seri olarak hello Klasik dağıtım modelinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="958cb-114">hello CLI in Service Management mode creates hello cluster nodes serially in hello classic deployment model, so deploying many compute nodes might take several minutes.</span></span> <span data-ttu-id="958cb-115">tooenable hello hello Klasik dağıtım modeli kullandığınızda RDMA ağ bağlantısı dağıtma hello VM'ler hello aynı bulut hizmeti.</span><span class="sxs-lookup"><span data-stu-id="958cb-115">tooenable hello RDMA network connection when you use hello classic deployment model, deploy hello VMs in hello same cloud service.</span></span>
* <span data-ttu-id="958cb-116">**Azure Resource Manager şablonları**: hello Resource Manager dağıtım modeli toodeploy toohello RDMA ağ bağlanır RDMA özellikli VM'ler oluşan bir küme de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="958cb-116">**Azure Resource Manager templates**: You can also use hello Resource Manager deployment model toodeploy a cluster of RDMA-capable VMs that connects toohello RDMA network.</span></span> <span data-ttu-id="958cb-117">Yapabilecekleriniz [kendi şablonunuzu oluşturun](../../../resource-group-authoring-templates.md), veya hello denetleyin [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates/) istediğiniz Microsoft veya hello topluluk toodeploy hello çözümü tarafından katkıda bulunan şablonları için.</span><span class="sxs-lookup"><span data-stu-id="958cb-117">You can [create your own template](../../../resource-group-authoring-templates.md), or check hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/) for templates contributed by Microsoft or hello community toodeploy hello solution you want.</span></span> <span data-ttu-id="958cb-118">Resource Manager şablonları hızlı ve güvenilir bir yol toodeploy Linux kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="958cb-118">Resource Manager templates can provide a fast and reliable way toodeploy a Linux cluster.</span></span> <span data-ttu-id="958cb-119">tooenable hello hello Resource Manager dağıtım modeli kullandığınızda RDMA ağ bağlantısı dağıtma hello hello Vm'lerde aynı kullanılabilirlik kümesi.</span><span class="sxs-lookup"><span data-stu-id="958cb-119">tooenable hello RDMA network connection when you use hello Resource Manager deployment model, deploy hello VMs in hello same availability set.</span></span>
* <span data-ttu-id="958cb-120">**HPC Pack**: Microsoft HPC Pack küme oluşturmayı ve desteklenen bir Linux dağıtım tooaccess hello RDMA ağ Çalıştır RDMA özellikli işlem düğümleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="958cb-120">**HPC Pack**: Create a Microsoft HPC Pack cluster in Azure and add RDMA-capable compute nodes that run a supported Linux distribution tooaccess hello RDMA network.</span></span> <span data-ttu-id="958cb-121">Daha fazla bilgi için bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="958cb-121">For more information, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="sample-deployment-steps-in-hello-classic-model"></a><span data-ttu-id="958cb-122">Merhaba Klasik modelde örnek dağıtım adımları</span><span class="sxs-lookup"><span data-stu-id="958cb-122">Sample deployment steps in hello classic model</span></span>
<span data-ttu-id="958cb-123">Merhaba aşağıdaki adımlar nasıl toouse hello Azure CLI toodeploy hello Azure Marketi SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM'den özelleştirebilir ve özel bir VM görüntüsü oluşturma gösterir.</span><span class="sxs-lookup"><span data-stu-id="958cb-123">hello following steps show how toouse hello Azure CLI toodeploy a SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM from hello Azure Marketplace, customize it, and create a custom VM image.</span></span> <span data-ttu-id="958cb-124">Daha sonra hello görüntü tooscript hello RDMA özellikli sanal makineleri bir küme dağıtımını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="958cb-124">Then you can use hello image tooscript hello deployment of a cluster of RDMA-capable VMs.</span></span>

> [!TIP]
> <span data-ttu-id="958cb-125">RDMA yeteneğine sahip sanal makineleri bir küme hello Azure Marketi CentOS tabanlı HPC görüntülerinde temel benzer adımları toodeploy kullanın.</span><span class="sxs-lookup"><span data-stu-id="958cb-125">Use similar steps toodeploy a cluster of RDMA-capable VMs based on CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="958cb-126">Bazı adımlar belirtildiği gibi biraz daha farklı.</span><span class="sxs-lookup"><span data-stu-id="958cb-126">Some steps differ slightly, as noted.</span></span> 
>
>

### <a name="prerequisites"></a><span data-ttu-id="958cb-127">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="958cb-127">Prerequisites</span></span>
* <span data-ttu-id="958cb-128">**İstemci bilgisayar**: Azure ile Mac, Linux veya Windows istemci bilgisayarı toocommunicate gerekir.</span><span class="sxs-lookup"><span data-stu-id="958cb-128">**Client computer**: You need a Mac, Linux, or Windows client computer toocommunicate with Azure.</span></span> <span data-ttu-id="958cb-129">Bu adımlarda Linux istemci kullandığınız varsayılır.</span><span class="sxs-lookup"><span data-stu-id="958cb-129">These steps assume you are using a Linux client.</span></span>
* <span data-ttu-id="958cb-130">**Azure aboneliği**: bir aboneliğiniz yoksa oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="958cb-130">**Azure subscription**: If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span> <span data-ttu-id="958cb-131">Daha büyük kümeleri için Kullandıkça Öde aboneliğine veya diğer satın alma seçenekleri göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="958cb-131">For larger clusters, consider a pay-as-you-go subscription or other purchase options.</span></span>
* <span data-ttu-id="958cb-132">**VM boyutu kullanılabilirlik**: örnek boyutları aşağıdaki hello RDMA özelliğine sahip olan: H16r, H16mr, A8 ve A9.</span><span class="sxs-lookup"><span data-stu-id="958cb-132">**VM size availability**: hello following instance sizes are RDMA capable: H16r, H16mr, A8, and A9.</span></span> <span data-ttu-id="958cb-133">Denetleme [bölgeye göre ürünleri](https://azure.microsoft.com/regions/services/) Azure bölgelerindeki kullanılabilirlik.</span><span class="sxs-lookup"><span data-stu-id="958cb-133">Check [Products available by region](https://azure.microsoft.com/regions/services/) for availability in Azure regions.</span></span>
* <span data-ttu-id="958cb-134">**Çekirdek kota**: çekirdek toodeploy işlem yoğunluklu VM'ler oluşan bir küme tooincrease hello kotası gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="958cb-134">**Cores quota**: You might need tooincrease hello quota of cores toodeploy a cluster of compute-intensive VMs.</span></span> <span data-ttu-id="958cb-135">Örneğin, bu makaledeki gösterildiği gibi toodeploy 8 A9 Vm'lerde istiyorsanız en az 128 çekirdek gerekir.</span><span class="sxs-lookup"><span data-stu-id="958cb-135">For example, you need at least 128 cores if you want toodeploy 8 A9 VMs as shown in this article.</span></span> <span data-ttu-id="958cb-136">Aboneliğinizi de hello hello H-serisi dahil olmak üzere belirli VM boyutu aileleri, dağıtabilirsiniz çekirdek sayısını sınırlayabilir.</span><span class="sxs-lookup"><span data-stu-id="958cb-136">Your subscription might also limit hello number of cores you can deploy in certain VM size families, including hello H-series.</span></span> <span data-ttu-id="958cb-137">toorequest kota artırma, [bir çevrimiçi müşteri destek isteği açma](../../../azure-supportability/how-to-create-azure-support-request.md) herhangi bir ücret alınmaz.</span><span class="sxs-lookup"><span data-stu-id="958cb-137">toorequest a quota increase, [open an online customer support request](../../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
* <span data-ttu-id="958cb-138">**Azure CLI**: [yükleme](../../../cli-install-nodejs.md) Azure CLI hello ve [tooyour Azure aboneliğine bağlanma](../../../xplat-cli-connect.md) hello istemci bilgisayardan.</span><span class="sxs-lookup"><span data-stu-id="958cb-138">**Azure CLI**: [Install](../../../cli-install-nodejs.md) hello Azure CLI and [connect tooyour Azure subscription](../../../xplat-cli-connect.md) from hello client computer.</span></span>

### <a name="provision-an-sles-12-sp1-hpc-vm"></a><span data-ttu-id="958cb-139">SLES 12 SP1 HPC VM sağlama</span><span class="sxs-lookup"><span data-stu-id="958cb-139">Provision an SLES 12 SP1 HPC VM</span></span>
<span data-ttu-id="958cb-140">TooAzure hello Azure CLI ile oturum sonra çalıştırmak `azure config list` çıktı hello tooconfirm hizmet yönetimi modu gösterir.</span><span class="sxs-lookup"><span data-stu-id="958cb-140">After signing in tooAzure with hello Azure CLI, run `azure config list` tooconfirm that hello output shows Service Management mode.</span></span> <span data-ttu-id="958cb-141">Yoksa, şu komutu çalıştırarak hello modunu ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="958cb-141">If it does not, set hello mode by running this command:</span></span>

    azure config mode asm


<span data-ttu-id="958cb-142">Toolist aşağıdaki hello yetkili toouse olduğunuz tüm hello abonelikleri yazın:</span><span class="sxs-lookup"><span data-stu-id="958cb-142">Type hello following toolist all hello subscriptions you are authorized toouse:</span></span>

    azure account list

<span data-ttu-id="958cb-143">Merhaba geçerli etkin bir aboneliğiniz ile tanımlanan `Current` çok ayarlamak`true`.</span><span class="sxs-lookup"><span data-stu-id="958cb-143">hello current active subscription is identified with `Current` set too`true`.</span></span> <span data-ttu-id="958cb-144">Bu abonelik hello değilse, bir toouse toocreate hello küme istediğiniz, hello uygun abonelik kimliği etkin bir aboneliğiniz hello ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="958cb-144">If this subscription isn't hello one you want toouse toocreate hello cluster, set hello appropriate subscription ID as hello active subscription:</span></span>

    azure account set <subscription-Id>

<span data-ttu-id="958cb-145">toosee Merhaba, kabuk ortam desteklediği varsayarak, aşağıdakileri hello gibi bir komut çalıştırmak Azure genel kullanıma açık SLES 12 SP1 HPC görüntülerinde **grep**:</span><span class="sxs-lookup"><span data-stu-id="958cb-145">toosee hello publicly available SLES 12 SP1 HPC images in Azure, run a command like hello following, assuming your shell environment supports **grep**:</span></span>

    azure vm image list | grep "suse.*hpc"

<span data-ttu-id="958cb-146">SLES 12 SP1 HPC görüntüsü ile RDMA özellikli bir VM hello aşağıdaki gibi bir komutu çalıştırarak sağlayın:</span><span class="sxs-lookup"><span data-stu-id="958cb-146">Provision an RDMA-capable VM with a SLES 12 SP1 HPC image by running a command like hello following:</span></span>

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

<span data-ttu-id="958cb-147">Konumlar:</span><span class="sxs-lookup"><span data-stu-id="958cb-147">Where:</span></span>

* <span data-ttu-id="958cb-148">Merhaba boyutu (Bu örnekte A9) hello RDMA özelliğine sahip VM boyutları biridir.</span><span class="sxs-lookup"><span data-stu-id="958cb-148">hello size (A9 in this example) is one of hello RDMA-capable VM sizes.</span></span>
* <span data-ttu-id="958cb-149">Merhaba dış SSH bağlantı noktası numarası (Bu örnekte, hello SSH varsayılan olan 22) tüm geçerli bağlantı noktası numarasıdır.</span><span class="sxs-lookup"><span data-stu-id="958cb-149">hello external SSH port number (22 in this example, which is hello SSH default) is any valid port number.</span></span> <span data-ttu-id="958cb-150">Merhaba iç SSH bağlantı noktası numarası too22 ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="958cb-150">hello internal SSH port number is set too22.</span></span>
* <span data-ttu-id="958cb-151">Yeni bir bulut hizmeti hello hello konumu tarafından belirtilen Azure bölgesi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="958cb-151">A new cloud service is created in hello Azure region specified by hello location.</span></span> <span data-ttu-id="958cb-152">Merhaba VM boyutu seçtiğiniz kullanılabilir bir konum belirtin.</span><span class="sxs-lookup"><span data-stu-id="958cb-152">Specify a location in which hello VM size you choose is available.</span></span>
* <span data-ttu-id="958cb-153">(Bu, ek ücret doğurur) SUSE öncelik desteği için hello SLES 12 SP1 görüntü adı şu anda olabilir bu iki seçenekten birini:</span><span class="sxs-lookup"><span data-stu-id="958cb-153">For SUSE priority support (which incurs additional charges), hello SLES 12 SP1 image name currently can be one of these two options:</span></span> 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-hello-vm"></a><span data-ttu-id="958cb-154">Merhaba VM özelleştirme</span><span class="sxs-lookup"><span data-stu-id="958cb-154">Customize hello VM</span></span>
<span data-ttu-id="958cb-155">Merhaba VM Sağlama tamamlandıktan sonra kullanarak SSH toohello VM VM'ın dış IP adresi (veya DNS adı) hello ve yapılandırılmış ve bu özelleştirme harici bağlantı noktası numarası hello.</span><span class="sxs-lookup"><span data-stu-id="958cb-155">After hello VM finishes provisioning, SSH toohello VM by using hello VM's external IP address (or DNS name) and hello external port number you configured, and then customize it.</span></span> <span data-ttu-id="958cb-156">Bağlantı ayrıntıları için bkz: [nasıl toolog Linux çalıştıran tooa sanal makine üzerinde](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="958cb-156">For connection details, see [How toolog on tooa virtual machine running Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="958cb-157">Gerekli toocomplete bir adım kök erişimi olmadığı sürece komutları hello VM üzerinde yapılandırılmış hello kullanıcı olarak gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="958cb-157">Perform commands as hello user you configured on hello VM, unless root access is required toocomplete a step.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="958cb-158">Microsoft Azure tooLinux VM'ler kök erişimi sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="958cb-158">Microsoft Azure does not provide root access tooLinux VMs.</span></span> <span data-ttu-id="958cb-159">komutları kullanarak çalışacak bir kullanıcı toohello VM olarak bağlanıldığında toogain yönetimsel erişim `sudo`.</span><span class="sxs-lookup"><span data-stu-id="958cb-159">toogain administrative access when connected as a user toohello VM, run commands by using `sudo`.</span></span>
>
>

* <span data-ttu-id="958cb-160">**Güncelleştirmeleri**: zypper kullanarak güncelleştirmeleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="958cb-160">**Updates**: Install updates by using zypper.</span></span> <span data-ttu-id="958cb-161">Ayrıca tooinstall NFS yardımcı programları isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="958cb-161">You might also want tooinstall NFS utilities.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="958cb-162">SLES 12 SP1 HPC VM ile sürücüleri hello Linux RDMA ile sorunlara neden olabilir çekirdek güncelleştirmeleri uygulanmaz öneririz.</span><span class="sxs-lookup"><span data-stu-id="958cb-162">In a SLES 12 SP1 HPC VM, we recommend that you don't apply kernel updates, which can cause issues with hello Linux RDMA drivers.</span></span>
  >
  >
* <span data-ttu-id="958cb-163">**Intel MPI**: hello aşağıdaki komutu çalıştırarak hello SLES 12 SP1 HPC VM Intel MPI hello yüklemesini tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="958cb-163">**Intel MPI**: Complete hello installation of Intel MPI on hello SLES 12 SP1 HPC VM by running hello following command:</span></span>

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* <span data-ttu-id="958cb-164">**Bellek kilitleme**: MPI kodları toolock hello bellek RDMA için ekleme veya hello /etc/security/limits.conf dosyasındaki ayarları aşağıdaki hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="958cb-164">**Lock memory**: For MPI codes toolock hello memory available for RDMA, add or change hello following settings in hello /etc/security/limits.conf file.</span></span> <span data-ttu-id="958cb-165">Bu dosya kök erişimi tooedit gerekir.</span><span class="sxs-lookup"><span data-stu-id="958cb-165">You need root access tooedit this file.</span></span>

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > <span data-ttu-id="958cb-166">Test amacıyla, memlock toounlimited de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="958cb-166">For testing purposes, you can also set memlock toounlimited.</span></span> <span data-ttu-id="958cb-167">Örneğin: `<User or group name>    hard    memlock unlimited`.</span><span class="sxs-lookup"><span data-stu-id="958cb-167">For example: `<User or group name>    hard    memlock unlimited`.</span></span> <span data-ttu-id="958cb-168">Daha fazla bilgi için bkz: [ayarı için bilinen en iyi yöntemleri kilitli bellek boyutu](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span><span class="sxs-lookup"><span data-stu-id="958cb-168">For more information, see [Best known methods for setting locked memory size](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span></span>
  >
  >
* <span data-ttu-id="958cb-169">**SLES VM'ler için SSH anahtarları**: oluşturmak SSH anahtarları tooestablish güven hello arasında kullanıcı hesabınız için işlem hello SLES küme düğümünde MPI işlerini çalıştırırken.</span><span class="sxs-lookup"><span data-stu-id="958cb-169">**SSH keys for SLES VMs**: Generate SSH keys tooestablish trust for your user account among hello compute nodes in hello SLES cluster when running MPI jobs.</span></span> <span data-ttu-id="958cb-170">CentOS tabanlı HPC VM dağıttıysanız, bu adımı izlemeyin.</span><span class="sxs-lookup"><span data-stu-id="958cb-170">If you deployed a CentOS-based HPC VM, don't follow this step.</span></span> <span data-ttu-id="958cb-171">Merhaba görüntüsünü yakalamak ve hello küme dağıttıktan sonra daha sonra bu makalede tooset hello küme düğümleri arasında passwordless SSH güveni yönergeleri bakın.</span><span class="sxs-lookup"><span data-stu-id="958cb-171">See instructions later in this article tooset up passwordless SSH trust among hello cluster nodes after you capture hello image and deploy hello cluster.</span></span>

    <span data-ttu-id="958cb-172">toocreate SSH anahtarları, komutu aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="958cb-172">toocreate SSH keys, run hello following command.</span></span> <span data-ttu-id="958cb-173">Giriş için istendiğinde seçin **Enter** toogenerate hello anahtarları bir parola ayarlama olmadan hello varsayılan konumu.</span><span class="sxs-lookup"><span data-stu-id="958cb-173">When you are prompted for input, select **Enter** toogenerate hello keys in hello default location without setting a password.</span></span>

        ssh-keygen

    <span data-ttu-id="958cb-174">Bilinen ortak anahtarları için Hello ortak anahtar toohello authorized_keys dosyası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="958cb-174">Append hello public key toohello authorized_keys file for known public keys.</span></span>

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    <span data-ttu-id="958cb-175">Merhaba ~/.ssh dizininde düzenleyin veya hello yapılandırma dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="958cb-175">In hello ~/.ssh directory, edit or create hello config file.</span></span> <span data-ttu-id="958cb-176">Başlangıç IP adresi aralığı hello özel ağ (Bu örnekte 10.32.0.0/16) azure'da toouse planlama sağlar:</span><span class="sxs-lookup"><span data-stu-id="958cb-176">Provide hello IP address range of hello private network that you plan toouse in Azure (10.32.0.0/16 in this example):</span></span>

        host 10.32.0.*
        StrictHostKeyChecking no

    <span data-ttu-id="958cb-177">Alternatif olarak, aşağıdaki gibi hello özel ağ IP adresi, kümedeki her bir VM listesi:</span><span class="sxs-lookup"><span data-stu-id="958cb-177">Alternatively, list hello private network IP address of each VM in your cluster as follows:</span></span>

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > <span data-ttu-id="958cb-178">Yapılandırma `StrictHostKeyChecking no` belirli IP adreslerini veya aralığını belirtilmediyse, bir güvenlik riski oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="958cb-178">Configuring `StrictHostKeyChecking no` can create a potential security risk when a specific IP address or range is not specified.</span></span>
  >
  >
* <span data-ttu-id="958cb-179">**Uygulamaları**: hello görüntüyü yakalamadan önce diğer özelleştirmeleri gerçekleştirin veya gerektiğini tüm uygulamaları yükleyin.</span><span class="sxs-lookup"><span data-stu-id="958cb-179">**Applications**: Install any applications you need or perform other customizations before you capture hello image.</span></span>

### <a name="capture-hello-image"></a><span data-ttu-id="958cb-180">Merhaba görüntü yakalama</span><span class="sxs-lookup"><span data-stu-id="958cb-180">Capture hello image</span></span>
<span data-ttu-id="958cb-181">ilk komut hello Linux VM üzerinde aşağıdaki hello çalıştırma toocapture hello resim.</span><span class="sxs-lookup"><span data-stu-id="958cb-181">toocapture hello image, first run hello following command on hello Linux VM.</span></span> <span data-ttu-id="958cb-182">Bu komut hello VM deprovisions ancak kullanıcı hesapları ve ayarladığınız SSH anahtarları korur.</span><span class="sxs-lookup"><span data-stu-id="958cb-182">This command deprovisions hello VM but maintains user accounts and SSH keys that you set up.</span></span>

```
sudo waagent -deprovision
```

<span data-ttu-id="958cb-183">İstemci bilgisayarından, Azure CLI komutları toocapture hello görüntü aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="958cb-183">From your client computer, run hello following Azure CLI commands toocapture hello image.</span></span> <span data-ttu-id="958cb-184">Daha fazla bilgi için bkz: [nasıl toocapture klasik bir Linux sanal makinesini görüntü olarak](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="958cb-184">For more information, see [How toocapture a classic Linux virtual machine as an image](capture-image.md).</span></span>  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

<span data-ttu-id="958cb-185">Bu komutları çalıştırdıktan sonra hello VM görüntüsü kullanımınız için yakalanır ve hello VM silinir.</span><span class="sxs-lookup"><span data-stu-id="958cb-185">After you run these commands, hello VM image is captured for your use and hello VM is deleted.</span></span> <span data-ttu-id="958cb-186">Şimdi bir küme, özel görüntü hazır toodeploy sahip.</span><span class="sxs-lookup"><span data-stu-id="958cb-186">Now you have your custom image ready toodeploy a cluster.</span></span>

### <a name="deploy-a-cluster-with-hello-image"></a><span data-ttu-id="958cb-187">Hello görüntüsü olan bir kümeyi dağıtma</span><span class="sxs-lookup"><span data-stu-id="958cb-187">Deploy a cluster with hello image</span></span>
<span data-ttu-id="958cb-188">Ortamınız için uygun değerlerle Bash komut dosyası izleyen hello değiştirin ve istemci bilgisayardan çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="958cb-188">Modify hello following Bash script with appropriate values for your environment and run it from your client computer.</span></span> <span data-ttu-id="958cb-189">Azure hello VM'ler hello Klasik dağıtım modelinde seri olarak dağıtır çünkü toodeploy hello bu komut dosyasını önerilen sekiz A9 Vm'lerde birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="958cb-189">Because Azure deploys hello VMs serially in hello classic deployment model, it takes a few minutes toodeploy hello eight A9 VMs suggested in this script.</span></span>

```
#!/bin/bash -x
# Script toocreate a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where hello VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All hello compute-intensive instances need toobe in hello same cloud service for Linux RDMA toowork across InfiniBand.
# Note: hello current maximum number of VMs in a cloud service is 50. If you need tooprovision more than 50 VMs in hello same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want tooturn off external ports and use only internal ports toocommunicate between compute nodes via port 22, don’t use this option. Since port numbers up too10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 toocluster18. Specify your captured image in <image-name>. Specify hello username and password you used when creating hello SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment tooprovision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a><span data-ttu-id="958cb-190">CentOS HPC Kümesi için ilgili önemli noktalar</span><span class="sxs-lookup"><span data-stu-id="958cb-190">Considerations for a CentOS HPC cluster</span></span>
<span data-ttu-id="958cb-191">Tooset birini hello Azure Marketi SLES 12 yerine hello CentOS tabanlı HPC görüntüleri için HPC temel alarak kümesi istiyorsanız, önceki bölümde hello hello genel adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="958cb-191">If you want tooset up a cluster based on one of hello CentOS-based HPC images in hello Azure Marketplace instead of SLES 12 for HPC, follow hello general steps in hello preceding section.</span></span> <span data-ttu-id="958cb-192">Farkları sağlamak ve hello VM yapılandırdığınızda aşağıdaki hello dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="958cb-192">Note hello following differences when you provision and configure hello VM:</span></span>

- <span data-ttu-id="958cb-193">Intel MPI CentOS tabanlı HPC görüntüden sağlanan bir VM üzerinde zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="958cb-193">Intel MPI is already installed on a VM provisioned from a CentOS-based HPC image.</span></span>
- <span data-ttu-id="958cb-194">Kilit bellek ayarları hello VM'in /etc/security/limits.conf dosyasında zaten eklendi.</span><span class="sxs-lookup"><span data-stu-id="958cb-194">Lock memory settings are already added in hello VM's /etc/security/limits.conf file.</span></span>
- <span data-ttu-id="958cb-195">Yakalama için SSH anahtarları hello sağlamanız VM üzerinde oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="958cb-195">Do not generate SSH keys on hello VM you provision for capture.</span></span> <span data-ttu-id="958cb-196">Merhaba küme dağıttıktan sonra bunun yerine, kullanıcı tabanlı kimlik doğrulaması kurma öneririz.</span><span class="sxs-lookup"><span data-stu-id="958cb-196">Instead, we recommend setting up user-based authentication after you deploy hello cluster.</span></span> <span data-ttu-id="958cb-197">Daha fazla bilgi için bölümden hello bakın.</span><span class="sxs-lookup"><span data-stu-id="958cb-197">For more information, see hello following section.</span></span>  

### <a name="set-up-passwordless-ssh-trust-on-hello-cluster"></a><span data-ttu-id="958cb-198">Merhaba kümede passwordless SSH güven ayarlama</span><span class="sxs-lookup"><span data-stu-id="958cb-198">Set up passwordless SSH trust on hello cluster</span></span>
<span data-ttu-id="958cb-199">CentOS tabanlı HPC küme üzerinde hello işlem düğümleri arasında güven kurulması için iki yöntem vardır: ana bilgisayar tabanlı kimlik doğrulama ve kullanıcı tabanlı kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="958cb-199">On a CentOS-based HPC cluster, there are two methods for establishing trust between hello compute nodes: host-based authentication and user-based authentication.</span></span> <span data-ttu-id="958cb-200">Ana bilgisayar tabanlı kimlik doğrulaması bu makalenin kapsamı dışında hello ve genellikle dağıtımı sırasında bir uzantı komut dosyası yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="958cb-200">Host-based authentication is outside of hello scope of this article and generally must be done through an extension script during deployment.</span></span> <span data-ttu-id="958cb-201">Kullanıcı tabanlı kimlik doğrulaması dağıtımdan sonra güven kurulması için uygundur ve işlem hello kümedeki düğümler hello oluşturma ve SSH anahtarları hello arasında paylaşılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="958cb-201">User-based authentication is convenient for establishing trust after deployment and requires hello generation and sharing of SSH keys among hello compute nodes in hello cluster.</span></span> <span data-ttu-id="958cb-202">Bu yöntem genellikle passwordless SSH oturumu açma olarak bilinen ve MPI işlerini çalıştırma durumlarda gereklidir.</span><span class="sxs-lookup"><span data-stu-id="958cb-202">This method is commonly known as passwordless SSH login and is required when running MPI jobs.</span></span>

<span data-ttu-id="958cb-203">Merhaba topluluktan katkıda bulunan bir örnek komut dosyası edinilebilir [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) CentOS tabanlı HPC küme tooenable kolay kullanıcı kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="958cb-203">A sample script contributed from hello community is available on [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable easy user authentication on a CentOS-based HPC cluster.</span></span> <span data-ttu-id="958cb-204">Karşıdan yükle ve hello aşağıdaki adımları kullanarak bu betiği kullanın.</span><span class="sxs-lookup"><span data-stu-id="958cb-204">Download and use this script by using hello following steps.</span></span> <span data-ttu-id="958cb-205">Ayrıca, bu komut dosyasını değiştirin veya herhangi diğer yöntemi tooestablish passwordless SSH kimlik doğrulaması hello küme işlem düğümleri arasında kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="958cb-205">You can also modify this script or use any other method tooestablish passwordless SSH authentication between hello cluster compute nodes.</span></span>

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

<span data-ttu-id="958cb-206">toorun hello betik tooknow hello öneki için alt ağ IP adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="958cb-206">toorun hello script, you need tooknow hello prefix for your subnet IP addresses.</span></span> <span data-ttu-id="958cb-207">Merhaba önek hello hello küme düğümlerinden biri üzerinde aşağıdaki komutu çalıştırarak alın.</span><span class="sxs-lookup"><span data-stu-id="958cb-207">Get hello prefix by running hello following command on one of hello cluster nodes.</span></span> <span data-ttu-id="958cb-208">Çıktı gibi 10.1.3.5 görünmelidir ve hello önek hello 10.1.3 bölümüdür.</span><span class="sxs-lookup"><span data-stu-id="958cb-208">Your output should look something like 10.1.3.5, and hello prefix is hello 10.1.3 portion.</span></span>

    ifconfig eth0 | grep -w inet | awk '{print $2}'

<span data-ttu-id="958cb-209">Artık üç parametrelerini kullanarak hello komut dosyasını çalıştırın: hello hello ortak kullanıcı adına işlem düğümlerini, hello ortak parola hello bu kullanıcıya işlem düğümlerini ve hello alt ağ önek döndürüldü hello önceki komutu.</span><span class="sxs-lookup"><span data-stu-id="958cb-209">Now run hello script using three parameters: hello common user name on hello compute nodes, hello common password for that user on hello compute nodes, and hello subnet prefix that was returned from hello previous command.</span></span>

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

<span data-ttu-id="958cb-210">Bu komut dosyası izleyen hello:</span><span class="sxs-lookup"><span data-stu-id="958cb-210">This script does hello following:</span></span>

* <span data-ttu-id="958cb-211">Merhaba konak düğümde .ssh, passwordless oturum açma için gerekli olduğu adlı bir dizin oluşturur.</span><span class="sxs-lookup"><span data-stu-id="958cb-211">Creates a directory on hello host node named .ssh, which is required for passwordless login.</span></span>
* <span data-ttu-id="958cb-212">Merhaba kümedeki herhangi bir düğümden passwordless oturum açma tooallow oturum açma bildirir hello .ssh dizininde bir yapılandırma dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="958cb-212">Creates a configuration file in hello .ssh directory that instructs passwordless login tooallow login from any node in hello cluster.</span></span>
* <span data-ttu-id="958cb-213">Merhaba düğüm adı ve düğüm IP adresleri hello kümedeki tüm hello düğümler için içeren dosyaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="958cb-213">Creates files containing hello node names and node IP addresses for all hello nodes in hello cluster.</span></span> <span data-ttu-id="958cb-214">Daha sonra başvurmak için Hello betiği çalıştırdıktan sonra bu dosyaları bırakılır.</span><span class="sxs-lookup"><span data-stu-id="958cb-214">These files are left after hello script is run for later reference.</span></span>
* <span data-ttu-id="958cb-215">(Merhaba ana bilgisayar düğümü dahil) her küme düğümü için özel ve ortak anahtar çifti oluşturur ve girişleri hello authorized_keys dosyasında oluşturur.</span><span class="sxs-lookup"><span data-stu-id="958cb-215">Creates a private and public key pair for each cluster node (including hello host node) and creates entries in hello authorized_keys file.</span></span>

> [!WARNING]
> <span data-ttu-id="958cb-216">Bu komut dosyasını çalıştıran bir güvenlik riski oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="958cb-216">Running this script can create a potential security risk.</span></span> <span data-ttu-id="958cb-217">Ortak anahtar bilgileri ~/.ssh Hello değil dağıtılmış emin olun.</span><span class="sxs-lookup"><span data-stu-id="958cb-217">Ensure that hello public key information in ~/.ssh is not distributed.</span></span>
>
>

## <a name="configure-intel-mpi"></a><span data-ttu-id="958cb-218">Intel MPI yapılandırın</span><span class="sxs-lookup"><span data-stu-id="958cb-218">Configure Intel MPI</span></span>
<span data-ttu-id="958cb-219">Azure Linux RDMA toorun MPI uygulamaları, tooconfigure gereken belirli ortam değişkenleri belirli tooIntel MPI.</span><span class="sxs-lookup"><span data-stu-id="958cb-219">toorun MPI applications on Azure Linux RDMA, you need tooconfigure certain environment variables specific tooIntel MPI.</span></span> <span data-ttu-id="958cb-220">Bir uygulama bir örnek komut dosyası tooconfigure Bash hello gerekli değişkenleri toorun aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="958cb-220">Here is a sample Bash script tooconfigure hello variables needed toorun an application.</span></span> <span data-ttu-id="958cb-221">Merhaba yolu toompivars.sh Intel MPI yüklemeniz için gerektiği gibi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="958cb-221">Change hello path toompivars.sh as needed for your installation of Intel MPI.</span></span>

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting hello variable tooshm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line toorun hello job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path toohello application exe> <arguments specific toohello application>

#end
```

<span data-ttu-id="958cb-222">Merhaba ana bilgisayar dosyası Hello biçimi aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="958cb-222">hello format of hello host file is as follows.</span></span> <span data-ttu-id="958cb-223">Kümedeki her düğüm için bir satır ekleyin.</span><span class="sxs-lookup"><span data-stu-id="958cb-223">Add one line for each node in your cluster.</span></span> <span data-ttu-id="958cb-224">Hello sanal ağdan özel IP adresleri daha önce tanımlanan DNS adlarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="958cb-224">Specify private IP addresses from hello virtual network defined earlier, not DNS names.</span></span> <span data-ttu-id="958cb-225">Örneğin, IP adresleriyle 10.32.0.1 ve 10.32.0.2 için iki ana hello dosya hello aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="958cb-225">For example, for two hosts with IP addresses 10.32.0.1 and 10.32.0.2, hello file contains hello following:</span></span>

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a><span data-ttu-id="958cb-226">Temel iki düğümlü bir küme üzerinde MPI çalıştırın</span><span class="sxs-lookup"><span data-stu-id="958cb-226">Run MPI on a basic two-node cluster</span></span>
<span data-ttu-id="958cb-227">İlk zaten yapmadıysanız, Intel MPI hello ortamını ayarlama.</span><span class="sxs-lookup"><span data-stu-id="958cb-227">If you haven't already done so, first set up hello environment for Intel MPI.</span></span>

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a><span data-ttu-id="958cb-228">MPI komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="958cb-228">Run an MPI command</span></span>
<span data-ttu-id="958cb-229">Bir MPI komutu MPI düzgün bir şekilde yüklendiğini ve iletişim kurabilir hello işlem düğümleri tooshow birinde en az iki işlem düğümleri arasında çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="958cb-229">Run an MPI command on one of hello compute nodes tooshow that MPI is installed properly and can communicate between at least two compute nodes.</span></span> <span data-ttu-id="958cb-230">Merhaba aşağıdaki **mpirun** komutu çalıştırır hello **ana bilgisayar adı** iki düğüm üzerinde komutu.</span><span class="sxs-lookup"><span data-stu-id="958cb-230">hello following **mpirun** command runs hello **hostname** command on two nodes.</span></span>

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
<span data-ttu-id="958cb-231">Çıktı için giriş olarak geçirilen tüm hello düğümlerinin hello adlarını listelenmelidir `-hosts`.</span><span class="sxs-lookup"><span data-stu-id="958cb-231">Your output should list hello names of all hello nodes that you passed as input for `-hosts`.</span></span> <span data-ttu-id="958cb-232">Örneğin, bir **mpirun** iki düğüm komutuyla hello aşağıdaki gibi bir çıktı döndürür:</span><span class="sxs-lookup"><span data-stu-id="958cb-232">For example, an **mpirun** command with two nodes returns output like hello following:</span></span>

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a><span data-ttu-id="958cb-233">MPI Kıyaslama çalıştırması</span><span class="sxs-lookup"><span data-stu-id="958cb-233">Run an MPI benchmark</span></span>
<span data-ttu-id="958cb-234">Intel MPI komutu aşağıdaki hello pingpong Kıyaslama tooverify hello küme yapılandırması ve bağlantı toohello RDMA ağ çalışır.</span><span class="sxs-lookup"><span data-stu-id="958cb-234">hello following Intel MPI command runs a pingpong benchmark tooverify hello cluster configuration and connection toohello RDMA network.</span></span>

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

<span data-ttu-id="958cb-235">İki düğümle bir çalışma kümesinde hello aşağıdaki gibi bir çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="958cb-235">On a working cluster with two nodes, you should see output like hello following.</span></span> <span data-ttu-id="958cb-236">Hello Azure RDMA ağ üzerinde gecikme düzeyinde veya altında 3 mikrosaniye too512 bayt ileti boyutları için bekler.</span><span class="sxs-lookup"><span data-stu-id="958cb-236">On hello Azure RDMA network, expect latency at or below 3 microseconds for message sizes up too512 bytes.</span></span>

```
#------------------------------------------------------------
#    Intel (R) MPI Benchmarks 4.0 Update 1, MPI-1 part
#------------------------------------------------------------
# Date                  : Fri Jul 17 23:16:46 2015
# Machine               : x86_64
# System                : Linux
# Release               : 3.12.39-44-default
# Version               : #5 SMP Thu Jun 25 22:45:24 UTC 2015
# MPI Version           : 3.0
# MPI Thread Environment:
# New default behavior from Version 3.2 on:
# hello number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected toobe exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through hello flag => -time

# Calling sequence was:
# /opt/intel/impi_latest/bin64/IMB-MPI1 pingpong
# Minimum message length in bytes:   0
# Maximum message length in bytes:   4194304
#
# MPI_Datatype                   :   MPI_BYTE
# MPI_Datatype for reductions    :   MPI_FLOAT
# MPI_Op                         :   MPI_SUM
#
#
# List of Benchmarks toorun:
# PingPong
#---------------------------------------------------
# Benchmarking PingPong
# #processes = 2
#---------------------------------------------------
       #bytes #repetitions      t[usec]   Mbytes/sec
            0         1000         2.23         0.00
            1         1000         2.26         0.42
            2         1000         2.26         0.85
            4         1000         2.26         1.69
            8         1000         2.26         3.38
           16         1000         2.36         6.45
           32         1000         2.57        11.89
           64         1000         2.36        25.81
          128         1000         2.64        46.19
          256         1000         2.73        89.30
          512         1000         3.09       157.99
         1024         1000         3.60       271.53
         2048         1000         4.46       437.57
         4096         1000         6.11       639.23
         8192         1000         7.49      1043.47
        16384         1000         9.76      1600.76
        32768         1000        14.98      2085.77
        65536          640        25.99      2405.08
       131072          320        50.68      2466.64
       262144          160        80.62      3101.01
       524288           80       145.86      3427.91
      1048576           40       279.06      3583.42
      2097152           20       543.37      3680.71
      4194304           10      1082.94      3693.63

# All processes entering MPI_Finalize

```



## <a name="next-steps"></a><span data-ttu-id="958cb-237">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="958cb-237">Next steps</span></span>
* <span data-ttu-id="958cb-238">Dağıtın ve Linux MPI uygulamaları Linux kümenizde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="958cb-238">Deploy and run your Linux MPI applications on your Linux cluster.</span></span>
* <span data-ttu-id="958cb-239">Merhaba bkz [Intel MPI kitaplığı belgeleri](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) Intel MPI hakkında yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="958cb-239">See hello [Intel MPI Library documentation](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) for guidance on Intel MPI.</span></span>
* <span data-ttu-id="958cb-240">Deneyin bir [hızlı başlatma şablonunu](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate bir Intel Lustre küme CentOS tabanlı HPC görüntüsünü kullanarak.</span><span class="sxs-lookup"><span data-stu-id="958cb-240">Try a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate an Intel Lustre cluster by using a CentOS-based HPC image.</span></span> <span data-ttu-id="958cb-241">Ayrıntılar için bkz [dağıtma Intel bulut Edition için Microsoft Azure üzerinde Lustre](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span><span class="sxs-lookup"><span data-stu-id="958cb-241">For details, see [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span></span>
