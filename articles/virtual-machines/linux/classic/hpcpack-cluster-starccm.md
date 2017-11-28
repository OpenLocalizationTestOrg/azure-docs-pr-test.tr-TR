---
title: "aaaRun yıldız-CCM + Linux VM'ler üzerinde HPC Pack ile | Microsoft Docs"
description: "Azure üzerinde Microsoft HPC Pack küme dağıtma ve bir yıldız çalıştırma-CCM + işi birden çok Linux işlem düğümlerini bir RDMA ağ üzerinden."
services: virtual-machines-linux
documentationcenter: 
author: xpillons
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 75523406-d268-4623-ac3e-811c7b74de4b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 09/13/2016
ms.author: xpillons
ms.openlocfilehash: 8265013cb295f53d6d4354ab2f100ef20d9f4c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="ec52e-103">Yıldız Çalıştır-CCM + Linux RDMA üzerinde Microsoft HPC Pack ile Azure'da küme</span><span class="sxs-lookup"><span data-stu-id="ec52e-103">Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="ec52e-104">Bu makale size nasıl toodeploy Microsoft HPC Pack küme Azure ve Çalıştır gösterir. bir [CD adapco yıldız-CCM +](http://www.cd-adapco.com/products/star-ccm%C2%AE) InfiniBand ile bağlandığına birden çok Linux işlem düğümlerinde iş.</span><span class="sxs-lookup"><span data-stu-id="ec52e-104">This article shows you how toodeploy a Microsoft HPC Pack cluster on Azure and run a [CD-adapco STAR-CCM+](http://www.cd-adapco.com/products/star-ccm%C2%AE) job on multiple Linux compute nodes that are interconnected with InfiniBand.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="ec52e-105">Microsoft HPC Pack büyük ölçekli HPC ve paralel uygulamalar, Microsoft Azure sanal makinelerin kümelerde MPI uygulamaları da dahil olmak üzere çeşitli özellikler toorun sağlar.</span><span class="sxs-lookup"><span data-stu-id="ec52e-105">Microsoft HPC Pack provides features toorun a variety of large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="ec52e-106">HPC Pack çalışan Linux HPC uygulamaları bir HPC Pack kümede dağıtılan Linux işlem düğümü vm'lerde de destekler.</span><span class="sxs-lookup"><span data-stu-id="ec52e-106">HPC Pack also supports running Linux HPC applications on Linux compute-node VMs that are deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="ec52e-107">Bir giriş toousing Linux işlem düğümleri HPC paketi ile bakın [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="ec52e-107">For an introduction toousing Linux compute nodes with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="set-up-an-hpc-pack-cluster"></a><span data-ttu-id="ec52e-108">Bir HPC Pack kümesi</span><span class="sxs-lookup"><span data-stu-id="ec52e-108">Set up an HPC Pack cluster</span></span>
<span data-ttu-id="ec52e-109">Hello Hello HPC Pack Iaas dağıtım betikleri indirin [Yükleme Merkezi'nden](https://www.microsoft.com/en-us/download/details.aspx?id=44949) ve yerel olarak ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-109">Download hello HPC Pack IaaS deployment scripts from hello [Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=44949) and extract them locally.</span></span>

<span data-ttu-id="ec52e-110">Azure PowerShell önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="ec52e-110">Azure PowerShell is a prerequisite.</span></span> <span data-ttu-id="ec52e-111">PowerShell yerel makinenizde yapılandırılmamışsa, lütfen hello makaleyi okuyun [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ec52e-111">If PowerShell is not configured on your local machine, please read hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="ec52e-112">Bu yazma Hello anda hello Linux hello (içeren hello InfiniBand sürücüleri için Azure) Azure Marketi görüntülerden SLES 12, CentOS 6.5 ve CentOS 7.1 içindir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-112">At hello time of this writing, hello Linux images from hello Azure Marketplace (which contains hello InfiniBand drivers for Azure) are for SLES 12, CentOS 6.5, and CentOS 7.1.</span></span> <span data-ttu-id="ec52e-113">Bu makalede, SLES 12 hello kullanımını temel alır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-113">This article is based on hello usage of SLES 12.</span></span> <span data-ttu-id="ec52e-114">tooretrieve hello adı hello Market HPC destekleyen tüm Linux görüntülerin hello aşağıdaki PowerShell komutunu çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ec52e-114">tooretrieve hello name of all Linux images that support HPC in hello Marketplace, you can run hello following PowerShell command:</span></span>

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

<span data-ttu-id="ec52e-115">Merhaba çıkış listeler bu görüntüleri kullanılabilir olduğunu ve hello görüntü adı hello konumu (**görüntü adı**) daha sonra hello dağıtım şablonda kullanılan toobe.</span><span class="sxs-lookup"><span data-stu-id="ec52e-115">hello output lists hello location in which these images are available and hello image name (**ImageName**) toobe used in hello deployment template later.</span></span>

<span data-ttu-id="ec52e-116">Merhaba küme dağıtmadan önce bir HPC paketi dağıtım şablon dosyası toobuild sahip.</span><span class="sxs-lookup"><span data-stu-id="ec52e-116">Before you deploy hello cluster, you have toobuild an HPC Pack deployment template file.</span></span> <span data-ttu-id="ec52e-117">Küçük bir küme hedefleme olduğundan, hello baş düğüm hello etki alanı denetleyicisi olması ve yerel bir SQL veritabanı ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="ec52e-117">Because we're targeting a small cluster, hello head node will be hello domain controller and host a local SQL database.</span></span>

<span data-ttu-id="ec52e-118">Merhaba aşağıdaki şablon böyle bir baş düğüm dağıtmak, adlı bir XML dosyası oluşturma **MyCluster.xml**ve hello değerlerini değiştirme **Subscriptionıd**, **StorageAccount**,  **Konum**, **VMName**, ve **ServiceName** sizin ile.</span><span class="sxs-lookup"><span data-stu-id="ec52e-118">hello following template will deploy such a head node, create an XML file named **MyCluster.xml**, and replace hello values of **SubscriptionId**, **StorageAccount**, **Location**, **VMName**, and **ServiceName** with yours.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <IaaSClusterConfig>
      <Subscription>
        <SubscriptionId>99999999-9999-9999-9999-999999999999</SubscriptionId>
        <StorageAccount>mystorageaccount</StorageAccount>
      </Subscription>
      <Location>North Europe</Location>
      <VNet>
        <VNetName>hpcvnetne</VNetName>
        <SubnetName>subnet-hpc</SubnetName>
      </VNet>
      <Domain>
        <DCOption>HeadNodeAsDC</DCOption>
        <DomainFQDN>hpc.local</DomainFQDN>
      </Domain>
      <Database>
        <DBOption>LocalDB</DBOption>
      </Database>
      <HeadNode>
        <VMName>myhpchn</VMName>
        <ServiceName>myhpchn</ServiceName>
        <VMSize>Standard_D4</VMSize>
      </HeadNode>
      <LinuxComputeNodes>
        <VMNamePattern>lnxcn-%0001%</VMNamePattern>
        <ServiceNamePattern>mylnxcn%01%</ServiceNamePattern>
        <MaxNodeCountPerService>20</MaxNodeCountPerService>
        <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
        <VMSize>A9</VMSize>
        <NodeCount>0</NodeCount>
        <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
      </LinuxComputeNodes>
    </IaaSClusterConfig>

<span data-ttu-id="ec52e-119">Merhaba baş düğüm oluşturma, yükseltilmiş bir komut istemi'nde hello PowerShell komutunu çalıştırarak başlatın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-119">Start hello head-node creation by running hello PowerShell command in an elevated command prompt:</span></span>

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

<span data-ttu-id="ec52e-120">20 too30 dakika sonra hello baş düğüm hazır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-120">After 20 too30 minutes, hello head node should be ready.</span></span> <span data-ttu-id="ec52e-121">Merhaba tıklatarak hello Azure portal ' tooit bağlanabilirsiniz **Bağlan** hello sanal makinenin simgesi.</span><span class="sxs-lookup"><span data-stu-id="ec52e-121">You can connect tooit from hello Azure portal by clicking hello **Connect** icon of hello virtual machine.</span></span>

<span data-ttu-id="ec52e-122">Sonunda toofix hello DNS ileticisi olabilir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-122">You might eventually have toofix hello DNS forwarder.</span></span> <span data-ttu-id="ec52e-123">toodo, bu nedenle, DNS Yöneticisi'ni başlatın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-123">toodo so, start DNS Manager.</span></span>

1. <span data-ttu-id="ec52e-124">Sağ hello sunucu adının DNS Yöneticisi ' nde seçin **özellikleri**ve ardından hello **İleticiler** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ec52e-124">Right-click hello server name in DNS Manager, select **Properties**, and then click hello **Forwarders** tab.</span></span>
2. <span data-ttu-id="ec52e-125">Merhaba tıklatın **Düzenle** tooremove herhangi ileticiler düğmesine tıklayın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ec52e-125">Click hello **Edit** button tooremove any forwarders, and then click **OK**.</span></span>
3. <span data-ttu-id="ec52e-126">Bu hello emin olun **hiçbir ileticiler mevcutsa, kök ipuçlarını kullanacak** onay kutusu seçilidir ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ec52e-126">Make sure that hello **Use root hints if no forwarders are available** check box is selected, and then click **OK**.</span></span>

## <a name="set-up-linux-compute-nodes"></a><span data-ttu-id="ec52e-127">Linux işlem düğümlerini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ec52e-127">Set up Linux compute nodes</span></span>
<span data-ttu-id="ec52e-128">Hello kullanarak hello Linux işlem düğümlerini dağıtmak toocreate hello baş düğüm kullanılan aynı dağıtım şablonu.</span><span class="sxs-lookup"><span data-stu-id="ec52e-128">You deploy hello Linux compute nodes by using hello same deployment template that you used toocreate hello head node.</span></span>

<span data-ttu-id="ec52e-129">Merhaba dosya Kopyala **MyCluster.xml** yerel makine toohello baş düğüm ve güncelleştirme hello **NodeCount** toodeploy istediğiniz düğümlerin sayısını hello etiketi (< = 20).</span><span class="sxs-lookup"><span data-stu-id="ec52e-129">Copy hello file **MyCluster.xml** from your local machine toohello head node, and update hello **NodeCount** tag with hello number of nodes that you want toodeploy (<=20).</span></span> <span data-ttu-id="ec52e-130">Dikkatli toohave kullanılabilir yeterli çekirdek Azure kotanızı ile olması her A9 örneği aboneliğinizde 16 çekirdeğe tüketir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-130">Be careful toohave enough available cores in your Azure quota, because each A9 instance will consume 16 cores in your subscription.</span></span> <span data-ttu-id="ec52e-131">Daha fazla VM hello toouse istiyorsanız A8 örnekleri (8 çekirdek) yerine A9 kullanabilirsiniz aynı bütçeyi.</span><span class="sxs-lookup"><span data-stu-id="ec52e-131">You can use A8 instances (8 cores) instead of A9 if you want toouse more VMs in hello same budget.</span></span>

<span data-ttu-id="ec52e-132">Merhaba baş düğümünde hello HPC Pack Iaas dağıtım betikleri kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-132">On hello head node, copy hello HPC Pack IaaS deployment scripts.</span></span>

<span data-ttu-id="ec52e-133">Yükseltilmiş bir komut istemi'de Azure PowerShell komutlarını aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-133">Run hello following Azure PowerShell commands in an elevated command prompt:</span></span>

1. <span data-ttu-id="ec52e-134">Çalıştırma **Add-AzureAccount** tooconnect tooyour Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="ec52e-134">Run **Add-AzureAccount** tooconnect tooyour Azure subscription.</span></span>
2. <span data-ttu-id="ec52e-135">Birden çok aboneliğiniz varsa çalıştırmak **Get-AzureSubscription** toolist bunları.</span><span class="sxs-lookup"><span data-stu-id="ec52e-135">If you have multiple subscriptions, run **Get-AzureSubscription** toolist them.</span></span>
3. <span data-ttu-id="ec52e-136">Varsayılan bir abonelik hello çalıştırarak ayarlayın **Select-AzureSubscription - varlığıyla SubscriptionName xxxx-varsayılan** komutu.</span><span class="sxs-lookup"><span data-stu-id="ec52e-136">Set a default subscription by running hello **Select-AzureSubscription -SubscriptionName xxxx -Default** command.</span></span>
4. <span data-ttu-id="ec52e-137">Çalıştırma **.\New-HPCIaaSCluster.ps1 - ConfigFile MyCluster.xml** toostart Linux işlem düğümlerini dağıtma.</span><span class="sxs-lookup"><span data-stu-id="ec52e-137">Run **.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml** toostart deploying Linux compute nodes.</span></span>
   
   ![Baş düğüm dağıtım eylem][hndeploy]

<span data-ttu-id="ec52e-139">Merhaba HPC Pack Küme Yöneticisi aracını açın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-139">Open hello HPC Pack Cluster Manager tool.</span></span> <span data-ttu-id="ec52e-140">Birkaç dakika sonra Linux işlem düğümlerini düzenli olarak küme işlem düğümleri listede görünür.</span><span class="sxs-lookup"><span data-stu-id="ec52e-140">After few minutes, Linux compute nodes will regularly appear in list of cluster compute nodes.</span></span> <span data-ttu-id="ec52e-141">Merhaba Klasik dağıtım modeliyle Iaas VM'ler sıralı olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ec52e-141">With hello classic deployment mode, IaaS VMs are created sequentially.</span></span> <span data-ttu-id="ec52e-142">Düğüm sayısını Hello önemliyse, böylece tüm dağıtılan alma önemli miktarda zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-142">So if hello number of nodes is important, getting them all deployed can take a significant amount of time.</span></span>

![Linux düğümleri HPC Pack Küme Yöneticisi'nde][clustermanager]

<span data-ttu-id="ec52e-144">Tüm düğüm hello kümede hazır ve çalışır olduğundan, ek Altyapı ayarlarını toomake vardır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-144">Now that all nodes are up and running in hello cluster, there are additional infrastructure settings toomake.</span></span>

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a><span data-ttu-id="ec52e-145">Windows ve Linux düğümleri için bir Azure dosya paylaşımı ayarlama</span><span class="sxs-lookup"><span data-stu-id="ec52e-145">Set up an Azure File share for Windows and Linux nodes</span></span>
<span data-ttu-id="ec52e-146">Hello Azure dosya hizmeti toostore komut dosyaları, uygulama paketleri ve veri dosyalarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec52e-146">You can use hello Azure File service toostore scripts, application packages, and data files.</span></span> <span data-ttu-id="ec52e-147">Azure dosya kalıcı deposu olarak Azure Blob Depolama CIFS işlevleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="ec52e-147">Azure File provides CIFS capabilities on top of Azure Blob storage as a persistent store.</span></span> <span data-ttu-id="ec52e-148">Bu hello en ölçeklenebilir bir çözüm değildir, ancak hello basit bir olduğundan ve özel VM'ler gerektirmeyen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-148">Be aware that this is not hello most scalable solution, but it is hello simplest one and doesn’t require dedicated VMs.</span></span>

<span data-ttu-id="ec52e-149">Merhaba makaledeki hello yönergeleri izleyerek bir Azure dosya paylaşımı oluşturmak [Windows Azure File storage ile çalışmaya başlama](../../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="ec52e-149">Create an Azure File share by following hello instructions in hello article [Get started with Azure File storage on Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="ec52e-150">Depolama hesabınız olarak Hello adını tutmak **saname**, hello dosya paylaşımı adı olarak **sharename**ve hello depolama hesabı anahtarı olarak **sakey**.</span><span class="sxs-lookup"><span data-stu-id="ec52e-150">Keep hello name of your storage account as **saname**, hello file share name as **sharename**, and hello storage account key as **sakey**.</span></span>

### <a name="mount-hello-azure-file-share-on-hello-head-node"></a><span data-ttu-id="ec52e-151">Merhaba baş düğümünde Hello Azure dosya paylaşımını bağlama</span><span class="sxs-lookup"><span data-stu-id="ec52e-151">Mount hello Azure File share on hello head node</span></span>
<span data-ttu-id="ec52e-152">Yükseltilmiş bir komut istemi açın ve komut toostore hello hello yerel makine kasa kimlik bilgilerini aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-152">Open an elevated command prompt and run hello following command toostore hello credentials in hello local machine vault:</span></span>

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

<span data-ttu-id="ec52e-153">Çalıştırma ardından toomount hello Azure dosya paylaşımı:</span><span class="sxs-lookup"><span data-stu-id="ec52e-153">Then, toomount hello Azure File share, run:</span></span>

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-hello-azure-file-share-on-linux-compute-nodes"></a><span data-ttu-id="ec52e-154">Linux işlem düğümlerinde Hello Azure dosya paylaşımını bağlama</span><span class="sxs-lookup"><span data-stu-id="ec52e-154">Mount hello Azure File share on Linux compute nodes</span></span>
<span data-ttu-id="ec52e-155">HPC paketi ile birlikte gelen bir yararlı aracı hello clusrun araçtır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-155">One useful tool that comes with HPC Pack is hello clusrun tool.</span></span> <span data-ttu-id="ec52e-156">İşlem düğümleri kümesi üzerinde aynı anda aynı komutu bu komut satırı aracı toorun hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec52e-156">You can use this command-line tool toorun hello same command simultaneously on a set of compute nodes.</span></span> <span data-ttu-id="ec52e-157">Bu örnekte, toomount hello Azure dosya paylaşımı kullandı ve toosurvive yeniden başlatmalar kalır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-157">In our case, it's used toomount hello Azure File share and persist it toosurvive reboots.</span></span>
<span data-ttu-id="ec52e-158">Merhaba baş düğümünde yükseltilmiş bir komut istemi içinde hello aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-158">In an elevated command prompt on hello head node, run hello following commands.</span></span>

<span data-ttu-id="ec52e-159">toocreate hello bağlama dizini:</span><span class="sxs-lookup"><span data-stu-id="ec52e-159">toocreate hello mount directory:</span></span>

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

<span data-ttu-id="ec52e-160">toomount hello Azure dosya paylaşımı:</span><span class="sxs-lookup"><span data-stu-id="ec52e-160">toomount hello Azure File share:</span></span>

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

<span data-ttu-id="ec52e-161">toopersist hello bağlama paylaşımı:</span><span class="sxs-lookup"><span data-stu-id="ec52e-161">toopersist hello mount share:</span></span>

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a><span data-ttu-id="ec52e-162">Yıldız yükle-CCM +</span><span class="sxs-lookup"><span data-stu-id="ec52e-162">Install STAR-CCM+</span></span>
<span data-ttu-id="ec52e-163">Azure VM örnekleri A8 ve A9 InfiniBand destek ve RDMA yetenekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="ec52e-163">Azure VM instances A8 and A9 provide InfiniBand support and RDMA capabilities.</span></span> <span data-ttu-id="ec52e-164">Bu özellikleri etkinleştirmek hello çekirdek sürücüler, Windows Server 2012 R2, SUSE 12, CentOS 6.5 ve hello Azure Marketi CentOS 7.1 görüntüleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-164">hello kernel drivers that enable those capabilities are available for Windows Server 2012 R2, SUSE 12, CentOS 6.5, and CentOS 7.1 images in hello Azure Marketplace.</span></span> <span data-ttu-id="ec52e-165">Microsoft MPI ve Intel MPI (5.x sürümü), bu sürücüleri Azure'da destekleyen hello iki MPI kitaplıkları var.</span><span class="sxs-lookup"><span data-stu-id="ec52e-165">Microsoft MPI and Intel MPI (release 5.x) are hello two MPI libraries that support those drivers in Azure.</span></span>

<span data-ttu-id="ec52e-166">CD adapco yıldız-CCM + 11.x bırakın ve daha sonra Intel MPI sürümüyle birlikte Azure InfiniBand desteği dahil olacak şekilde 5.x.</span><span class="sxs-lookup"><span data-stu-id="ec52e-166">CD-adapco STAR-CCM+ release 11.x and later is bundled with Intel MPI version 5.x, so InfiniBand support for Azure is included.</span></span>

<span data-ttu-id="ec52e-167">Merhaba Linux64 alma yıldız-CCM + hello paketinden [CD adapco portal](https://steve.cd-adapco.com).</span><span class="sxs-lookup"><span data-stu-id="ec52e-167">Get hello Linux64 STAR-CCM+ package from hello [CD-adapco portal](https://steve.cd-adapco.com).</span></span> <span data-ttu-id="ec52e-168">Örneğimizde, karma duyarlık 11.02.010 sürümünde kullandık.</span><span class="sxs-lookup"><span data-stu-id="ec52e-168">In our case, we used version 11.02.010 in mixed precision.</span></span>

<span data-ttu-id="ec52e-169">Merhaba baş düğümünde, hello **/hpcdata** Azure dosya paylaşımı, adlandırılmış bir kabuk betiği oluşturmak **setupstarccm.sh** içeriği aşağıdaki hello ile.</span><span class="sxs-lookup"><span data-stu-id="ec52e-169">On hello head node, in hello **/hpcdata** Azure File share, create a shell script named **setupstarccm.sh** with hello following content.</span></span> <span data-ttu-id="ec52e-170">Bu komut dosyasını her işlem düğümü tooset yıldız yukarı üzerinde çalıştırmak-CCM + yerel olarak.</span><span class="sxs-lookup"><span data-stu-id="ec52e-170">This script will be run on each compute node tooset up STAR-CCM+ locally.</span></span>

#### <a name="sample-setupstarcmsh-script"></a><span data-ttu-id="ec52e-171">Örnek setupstarcm.sh komut dosyası</span><span class="sxs-lookup"><span data-stu-id="ec52e-171">Sample setupstarcm.sh script</span></span>
```
    #!/bin/bash
    # setupstarcm.sh tooset up STAR-CCM+ locally

    # Create hello CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy hello STAR-CCM package from hello file share toohello local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract hello package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without hello FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
<span data-ttu-id="ec52e-172">Şimdi, tooset yıldız yukarı-CCM + tüm Linux işlem düğümleri, yükseltilmiş bir komut istemi açın ve hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-172">Now, tooset up STAR-CCM+ on all your Linux compute nodes, open an elevated command prompt and run hello following command:</span></span>

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

<span data-ttu-id="ec52e-173">Hello komutu çalışırken hello ısı Haritası Küme Yöneticisi'nin kullanarak hello CPU kullanımını izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec52e-173">While hello command is running, you can monitor hello CPU usage by using hello heat map of Cluster Manager.</span></span> <span data-ttu-id="ec52e-174">Birkaç dakika sonra tüm düğümleri doğru şekilde ayarlanmış olması.</span><span class="sxs-lookup"><span data-stu-id="ec52e-174">After few minutes, all nodes should be correctly set up.</span></span>

## <a name="run-star-ccm-jobs"></a><span data-ttu-id="ec52e-175">Yıldız Çalıştır-CCM + işleri</span><span class="sxs-lookup"><span data-stu-id="ec52e-175">Run STAR-CCM+ jobs</span></span>
<span data-ttu-id="ec52e-176">HPC Pack iş Zamanlayıcı yeteneklerini sipariş toorun yıldız için kullanıldığından-CCM + işler.</span><span class="sxs-lookup"><span data-stu-id="ec52e-176">HPC Pack is used for its job scheduler capabilities in order toorun STAR-CCM+ jobs.</span></span> <span data-ttu-id="ec52e-177">toodo bu nedenle, biz kullanılan toostart hello iş ve yıldız çalıştırmak birkaç komut dosyalarının destek hello-CCM +.</span><span class="sxs-lookup"><span data-stu-id="ec52e-177">toodo so, we need hello support of a few scripts that are used toostart hello job and run STAR-CCM+.</span></span> <span data-ttu-id="ec52e-178">Merhaba giriş verisi hello Azure dosya paylaşımında kolaylık olması için ilk olarak tutulur.</span><span class="sxs-lookup"><span data-stu-id="ec52e-178">hello input data is kept on hello Azure File share first for simplicity.</span></span>

<span data-ttu-id="ec52e-179">PowerShell Betiği aşağıdaki hello olduğu kullanılan tooqueue bir yıldız-CCM + işi.</span><span class="sxs-lookup"><span data-stu-id="ec52e-179">hello following PowerShell script is used tooqueue a STAR-CCM+ job.</span></span> <span data-ttu-id="ec52e-180">Üç bağımsız değişkeni alır:</span><span class="sxs-lookup"><span data-stu-id="ec52e-180">It takes three arguments:</span></span>

* <span data-ttu-id="ec52e-181">Merhaba model adı</span><span class="sxs-lookup"><span data-stu-id="ec52e-181">hello model name</span></span>
* <span data-ttu-id="ec52e-182">kullanılan düğümlerin toobe Hello sayısı</span><span class="sxs-lookup"><span data-stu-id="ec52e-182">hello number of nodes toobe used</span></span>
* <span data-ttu-id="ec52e-183">Merhaba kullanılan her düğüm toobe üzerinde çekirdek sayısı</span><span class="sxs-lookup"><span data-stu-id="ec52e-183">hello number of cores on each node toobe used</span></span>

<span data-ttu-id="ec52e-184">Çünkü yıldız-CCM + hello bellek bant genişliği doldurabilirsiniz, daha az çekirdek başına, genellikle daha iyi toouse işlem düğümleri ve yeni düğümler ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-184">Because STAR-CCM+ can fill hello memory bandwidth, it's usually better toouse fewer cores per compute nodes and add new nodes.</span></span> <span data-ttu-id="ec52e-185">Merhaba tam düğümü başına çekirdek sayısı hello işlemci ailesi ve hello bağlantı hızı değişir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-185">hello exact number of cores per node will depend on hello processor family and hello interconnect speed.</span></span>

<span data-ttu-id="ec52e-186">Merhaba düğümleri özel olarak hello iş için ayrılmış ve diğer işlemlerle paylaşılamaz.</span><span class="sxs-lookup"><span data-stu-id="ec52e-186">hello nodes are allocated exclusively for hello job and can’t be shared with other jobs.</span></span> <span data-ttu-id="ec52e-187">Merhaba iş MPI iş olarak doğrudan başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="ec52e-187">hello job is not started as an MPI job directly.</span></span> <span data-ttu-id="ec52e-188">Merhaba **runstarccm.sh** Kabuk betiği hello MPI Başlatıcısı başlayacak.</span><span class="sxs-lookup"><span data-stu-id="ec52e-188">hello **runstarccm.sh** shell script will start hello MPI launcher.</span></span>

<span data-ttu-id="ec52e-189">Merhaba giriş modeli ve hello **runstarccm.sh** betik hello depolanan **/hpcdata** daha önce oluşturulmuş paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="ec52e-189">hello input model and hello **runstarccm.sh** script are stored in hello **/hpcdata** share that was previously mounted.</span></span>

<span data-ttu-id="ec52e-190">Günlük dosyaları hello iş kimliği ile aynı ada sahiptir ve hello depolanan **/hpcdata paylaşımı**, hello yıldız birlikte-CCM + çıkış dosyaları.</span><span class="sxs-lookup"><span data-stu-id="ec52e-190">Log files are named with hello job ID and are stored in hello **/hpcdata share**, along with hello STAR-CCM+ output files.</span></span>

#### <a name="sample-submitstarccmjobps1-script"></a><span data-ttu-id="ec52e-191">Örnek SubmitStarccmJob.ps1 komut dosyası</span><span class="sxs-lookup"><span data-stu-id="ec52e-191">Sample SubmitStarccmJob.ps1 script</span></span>
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us hello job ID that's used tooidentify hello name of hello uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit hello job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
<span data-ttu-id="ec52e-192">Değiştir **runner.java** , tercih edilen yıldız ile-CCM + Java modeli Başlatıcısı ve günlük kodu.</span><span class="sxs-lookup"><span data-stu-id="ec52e-192">Replace **runner.java** with your preferred STAR-CCM+ Java model launcher and logging code.</span></span>

#### <a name="sample-runstarccmsh-script"></a><span data-ttu-id="ec52e-193">Örnek runstarccm.sh komut dosyası</span><span class="sxs-lookup"><span data-stu-id="ec52e-193">Sample runstarccm.sh script</span></span>
```
    #!/bin/bash
    echo "start"
    # hello path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set hello mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into hello hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with hello hostfile argument
    #  
    ${STARCCM} -np ${NBCORES} -machinefile ${NODELIST_PATH} \
        -power -podkey "<yourkey>" -rsh ssh \
        -mpi intel -fabric UDAPL -cpubind bandwidth,v \
        -mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0" \
        -batch $2 $3
    RTNSTS=$?
    rm -f ${NODELIST_PATH}

    exit ${RTNSTS}
```

<span data-ttu-id="ec52e-194">Testimizde, bir isteğe bağlı güç lisans belirteci kullandık.</span><span class="sxs-lookup"><span data-stu-id="ec52e-194">In our test, we used a Power-On-Demand license token.</span></span> <span data-ttu-id="ec52e-195">Bu bir belirteç tooset hello sahip **$CDLMD_LICENSE_FILE** ortam değişkeni çok **1999@flex.cd-adapco.com**  ve hello hello anahtarında **- podkey** hello komut satırı seçeneği .</span><span class="sxs-lookup"><span data-stu-id="ec52e-195">For that token, you have tooset hello **$CDLMD_LICENSE_FILE** environment variable too**1999@flex.cd-adapco.com** and hello key in hello **-podkey** option of hello command line.</span></span>

<span data-ttu-id="ec52e-196">Bazı başlatma hello betik ayıklar--hello **$CCP_NODES_CORES** HPC Pack ayarlanan--ortam değişkenlerini hello MPI Başlatıcısı hello hostfile kullanan düğümleri toobuild listesi.</span><span class="sxs-lookup"><span data-stu-id="ec52e-196">After some initialization, hello script extracts--from hello **$CCP_NODES_CORES** environment variables that HPC Pack set--hello list of nodes toobuild a hostfile that hello MPI launcher uses.</span></span> <span data-ttu-id="ec52e-197">Bu hostfile hello hello işi, satır başına bir ad için kullanılan işlem düğümü adlarının listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-197">This hostfile will contain hello list of compute node names that are used for hello job, one name per line.</span></span>

<span data-ttu-id="ec52e-198">Merhaba biçimi **$CCP_NODES_CORES** bu deseni izler:</span><span class="sxs-lookup"><span data-stu-id="ec52e-198">hello format of **$CCP_NODES_CORES** follows this pattern:</span></span>

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

<span data-ttu-id="ec52e-199">Konumlar:</span><span class="sxs-lookup"><span data-stu-id="ec52e-199">Where:</span></span>

* <span data-ttu-id="ec52e-200">`<Number of nodes>`toothis iş ayrılan düğümler Hello sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-200">`<Number of nodes>` is hello number of nodes allocated toothis job.</span></span>
* <span data-ttu-id="ec52e-201">`<Name of node_n_...>`Merhaba toothis iş ayrılan her düğümün adıdır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-201">`<Name of node_n_...>` is hello name of each node allocated toothis job.</span></span>
* <span data-ttu-id="ec52e-202">`<Cores of node_n_...>`Çekirdek toothis iş ayrılan hello düğümde Hello sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-202">`<Cores of node_n_...>` is hello number of cores on hello node allocated toothis job.</span></span>

<span data-ttu-id="ec52e-203">Merhaba çekirdek sayısı (**$NBCORES**) de hesaplanan göre hello düğüm sayısı: (**$NBNODES**) ve hello düğümü başına çekirdek sayısı (parametre olarak sağlanan **$NBCORESPERNODE**).</span><span class="sxs-lookup"><span data-stu-id="ec52e-203">hello number of cores (**$NBCORES**) is also calculated based on hello number of nodes (**$NBNODES**) and hello number of cores per node (provided as parameter **$NBCORESPERNODE**).</span></span>

<span data-ttu-id="ec52e-204">Merhaba MPI seçenekler için hello Azure üzerinde Intel MPI ile kullanılan olanları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ec52e-204">For hello MPI options, hello ones that are used with Intel MPI on Azure are:</span></span>

* <span data-ttu-id="ec52e-205">`-mpi intel`Intel MPI toospecify.</span><span class="sxs-lookup"><span data-stu-id="ec52e-205">`-mpi intel` toospecify Intel MPI.</span></span>
* <span data-ttu-id="ec52e-206">`-fabric UDAPL`toouse Azure InfiniBand fiilleri.</span><span class="sxs-lookup"><span data-stu-id="ec52e-206">`-fabric UDAPL` toouse Azure InfiniBand verbs.</span></span>
* <span data-ttu-id="ec52e-207">`-cpubind bandwidth,v`YILDIZ ile MPI için toooptimize bant genişliği-CCM +.</span><span class="sxs-lookup"><span data-stu-id="ec52e-207">`-cpubind bandwidth,v` toooptimize bandwidth for MPI with STAR-CCM+.</span></span>
* <span data-ttu-id="ec52e-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"`toomake Intel MPI iş ile Azure InfiniBand ve tooset hello düğümü başına çekirdek sayısı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` toomake Intel MPI work with Azure InfiniBand, and tooset hello required number of cores per node.</span></span>
* <span data-ttu-id="ec52e-209">`-batch`toostart yıldız-CCM + toplu iş modunda kullanıcı Arabirimi ile.</span><span class="sxs-lookup"><span data-stu-id="ec52e-209">`-batch` toostart STAR-CCM+ in batch mode with no UI.</span></span>

<span data-ttu-id="ec52e-210">Son olarak, toostart bir işin, düğümlerin ve çalışıyor olduğundan ve Küme Yöneticisi'nde çevrimiçi olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ec52e-210">Finally, toostart a job, make sure that your nodes are up and running and are online in Cluster Manager.</span></span> <span data-ttu-id="ec52e-211">Ardından bir PowerShell komut isteminde bu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-211">Then from a PowerShell command prompt, run this:</span></span>

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a><span data-ttu-id="ec52e-212">Düğümler durdurun</span><span class="sxs-lookup"><span data-stu-id="ec52e-212">Stop nodes</span></span>
<span data-ttu-id="ec52e-213">Daha sonra testlerinizi ile işiniz bittiğinde sonra HPC Pack PowerShell komutları toostop aşağıdaki hello kullanın ve düğümleri başlatın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-213">Later on, after you're done with your tests, you can use hello following HPC Pack PowerShell commands toostop and start nodes:</span></span>

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a><span data-ttu-id="ec52e-214">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ec52e-214">Next steps</span></span>
<span data-ttu-id="ec52e-215">Diğer Linux iş yükleri çalıştırmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-215">Try running other Linux workloads.</span></span> <span data-ttu-id="ec52e-216">Örneğin, bakın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-216">For example, see:</span></span>

* [<span data-ttu-id="ec52e-217">Linux işlem düğümlerinde Azure ile birlikte Microsoft HPC Pack NAMD çalıştırın</span><span class="sxs-lookup"><span data-stu-id="ec52e-217">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
* [<span data-ttu-id="ec52e-218">OpenFOAM, azure'da bir Linux RDMA kümede Microsoft HPC Pack ile çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-218">Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
