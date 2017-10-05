---
title: "OpenFOAM HPC paketi ile Linux VM'ler üzerinde çalıştırın. | Microsoft Docs"
description: "Azure Microsoft HPC Pack kümede dağıtın ve bir RDMA ağ üzerinden birden çok Linux işlem düğümlerinde OpenFOAM işi çalıştırın."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: ef124a8983fa112d499252460bff9ed2fcccc02b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="89cdf-103">Azure’daki bir Linux RDMA kümesinde Microsoft HPC Pack ile OpenFoam çalıştırma</span><span class="sxs-lookup"><span data-stu-id="89cdf-103">Run OpenFoam with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="89cdf-104">Bu makalede, Azure sanal makinelerinde OpenFoam çalıştırmak için bir yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="89cdf-104">This article shows you one way to run OpenFoam in Azure virtual machines.</span></span> <span data-ttu-id="89cdf-105">Bir Microsoft HPC Pack kümesinde Linux işlem düğümleri ile Azure ve Çalıştır burada dağıttığınız bir [OpenFoam](http://openfoam.com/) Intel MPI işlemiyle.</span><span class="sxs-lookup"><span data-stu-id="89cdf-105">Here, you deploy a Microsoft HPC Pack cluster with Linux compute nodes on Azure and run an [OpenFoam](http://openfoam.com/) job with Intel MPI.</span></span> <span data-ttu-id="89cdf-106">Böylece işlem düğümlerini Azure RDMA ağ üzerinden iletişim RDMA özellikli Azure Vm'lerde işlem düğümleri için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89cdf-106">You can use RDMA-capable Azure VMs for the compute nodes, so that the compute nodes communicate over the Azure RDMA network.</span></span> <span data-ttu-id="89cdf-107">Azure'da OpenFoam çalıştırmak için diğer seçenekleri UberCloud'ın gibi Market kullanılabilir tam olarak yapılandırılmış ticari görüntüleri dahil [OpenFoam 2.3 CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/)ve çalıştırarak [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span><span class="sxs-lookup"><span data-stu-id="89cdf-107">Other options to run OpenFoam in Azure include fully configured commercial images available in the Marketplace, such as UberCloud's [OpenFoam 2.3 on CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), and by running on [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="89cdf-108">(İçin alan işlemi açın ve düzenleme) OpenFOAM mühendislik ve Bilim hem ticari hem de akademik kuruluşlarda yaygın olarak kullanılan bir açık kaynak hesaplama sıvı dinamiği (CFD) yazılım paketidir.</span><span class="sxs-lookup"><span data-stu-id="89cdf-108">OpenFOAM (for Open Field Operation and Manipulation) is an open-source computational fluid dynamics (CFD) software package that is used widely in engineering and science, in both commercial and academic organizations.</span></span> <span data-ttu-id="89cdf-109">Meshing, özellikle snappyHexMesh, bir parallelized mesher karmaşık CAD geometri ve öncesi ve sonrası işleme için Araçlar içerir.</span><span class="sxs-lookup"><span data-stu-id="89cdf-109">It includes tools for meshing, notably snappyHexMesh, a parallelized mesher for complex CAD geometries, and for pre- and post-processing.</span></span> <span data-ttu-id="89cdf-110">Neredeyse tüm işlemler en bilgisayar donanımı tam anlamıyla yararlanabilmek kullanıcıları etkinleştirme paralel olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="89cdf-110">Almost all processes run in parallel, enabling users to take full advantage of computer hardware at their disposal.</span></span>  

<span data-ttu-id="89cdf-111">Microsoft HPC Pack büyük ölçekli HPC ve Microsoft Azure sanal makinelerin kümelerde MPI uygulamaları da dahil olmak üzere paralel uygulamaları çalıştırmak için özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="89cdf-111">Microsoft HPC Pack provides features to run large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="89cdf-112">HPC Pack de uygulamaların Linux işlem düğümü VM'ler bir HPC Pack kümede dağıtılmış çalışan Linux HPC destekler.</span><span class="sxs-lookup"><span data-stu-id="89cdf-112">HPC Pack also supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="89cdf-113">Bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md) işlem düğümleri HPC paketi ile Linux kullanmaya giriş bilgileri için.</span><span class="sxs-lookup"><span data-stu-id="89cdf-113">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction to using Linux compute nodes with HPC Pack.</span></span>

> [!NOTE]
> <span data-ttu-id="89cdf-114">Bu makalede nasıl HPC paketi ile Linux MPI iş yükü çalıştırılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="89cdf-114">This article illustrates how to run a Linux MPI workload with HPC Pack.</span></span> <span data-ttu-id="89cdf-115">Bu, Linux sistem yönetimi ile Linux kümelerinde MPI iş yükleri çalıştıran bazı benzer olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="89cdf-115">It assumes you have some familiarity with Linux system administration and with running MPI workloads on Linux clusters.</span></span> <span data-ttu-id="89cdf-116">MPI ve OpenFOAM bu makalede gösterilen olanları farklı sürümlerini kullanıyorsanız, bazı yükleme ve yapılandırma adımları değiştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="89cdf-116">If you use versions of MPI and OpenFOAM different from the ones shown in this article, you might have to modify some installation and configuration steps.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="89cdf-117">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="89cdf-117">Prerequisites</span></span>
* <span data-ttu-id="89cdf-118">**HPC Pack küme RDMA özellikli Linux işlem düğümlerini** - HPC paketi küme boyutu A8, A9, H16r, dağıtmak veya H16rm Linux işlem düğümlerini kullanarak bir [Azure Resource Manager şablonu](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) veya bir [Azure PowerShell Betiği](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="89cdf-118">**HPC Pack cluster with RDMA-capable Linux compute nodes** - Deploy an HPC Pack cluster with size A8, A9, H16r, or H16rm Linux compute nodes using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="89cdf-119">Bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md) Önkoşullar ve adımlar her iki seçenek için.</span><span class="sxs-lookup"><span data-stu-id="89cdf-119">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for the prerequisites and steps for either option.</span></span> <span data-ttu-id="89cdf-120">PowerShell komut dosyası dağıtım seçeneği seçerseniz, bu makalenin sonunda örnek dosyalarını örnek yapılandırma dosyasına bakın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-120">If you choose the PowerShell script deployment option, see the sample configuration file in the sample files at the end of this article.</span></span> <span data-ttu-id="89cdf-121">Bu yapılandırma, bir boyut A8 Windows Server 2012 R2 baş düğüm ve 2 boyutu A8 SUSE Linux Enterprise Server 12 işlem düğümleri oluşan bir HPC Pack Azure tabanlı küme dağıtmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-121">Use this configuration to deploy an Azure-based HPC Pack cluster consisting of a size A8 Windows Server 2012 R2 head node and 2 size A8 SUSE Linux Enterprise Server 12 compute nodes.</span></span> <span data-ttu-id="89cdf-122">Aboneliği ve hizmet adları için uygun değerleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="89cdf-122">Substitute appropriate values for your subscription and service names.</span></span> 
  
  <span data-ttu-id="89cdf-123">**Ek bilmeniz gerekenler**</span><span class="sxs-lookup"><span data-stu-id="89cdf-123">**Additional things to know**</span></span>
  
  * <span data-ttu-id="89cdf-124">Linux RDMA ağ ön koşulu için Azure bkz [yüksek performanslı işlem VM boyutları](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="89cdf-124">For Linux RDMA networking prerequisites in Azure, see [High performance compute VM sizes](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  * <span data-ttu-id="89cdf-125">Powershell komut dosyası dağıtım seçeneği kullanırsanız, RDMA ağ bağlantısı kullanmak için bir bulut hizmeti içindeki tüm Linux işlem düğümlerini dağıtın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-125">If you use the Powershell script deployment option, deploy all the Linux compute nodes within one cloud service to use the RDMA network connection.</span></span>
  * <span data-ttu-id="89cdf-126">Linux düğümleri dağıttıktan sonra ek yönetim görevleri gerçekleştirmek için SSH tarafından bağlayın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-126">After deploying the Linux nodes, connect by SSH to perform any additional administrative tasks.</span></span> <span data-ttu-id="89cdf-127">SSH bağlantı ayrıntıları her bir Linux VM için Azure portalında bulun.</span><span class="sxs-lookup"><span data-stu-id="89cdf-127">Find the SSH connection details for each Linux VM in the Azure portal.</span></span>  
* <span data-ttu-id="89cdf-128">**Intel MPI** - Azure, SLES 12 HPC işlem düğümlerinde OpenFOAM çalıştırmak için Intel MPI kitaplığı 5 çalışma zamanını şuradan yüklemenize gerek [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span><span class="sxs-lookup"><span data-stu-id="89cdf-128">**Intel MPI** - To run OpenFOAM on SLES 12 HPC compute nodes in Azure, you need to install the Intel MPI Library 5 runtime from the [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span></span> <span data-ttu-id="89cdf-129">(Intel MPI 5 CentOS tabanlı HPC görüntülerinde önceden yüklenir.)  Bir sonraki adımda gerekiyorsa, Linux işlem düğümlerinde Intel MPI yükleyin.</span><span class="sxs-lookup"><span data-stu-id="89cdf-129">(Intel MPI 5 is preinstalled on CentOS-based HPC images.)  In a later step, if necessary, install Intel MPI on your Linux compute nodes.</span></span> <span data-ttu-id="89cdf-130">Intel ile kaydettikten sonra bu adım için hazırlamak için ilgili web sayfasına onay e-postadaki bağlantıyı izleyin.</span><span class="sxs-lookup"><span data-stu-id="89cdf-130">To prepare for this step, after you register with Intel, follow the link in the confirmation email to the related web page.</span></span> <span data-ttu-id="89cdf-131">Ardından, Intel MPI uygun sürümünü .tgz dosyası için indirme bağlantısı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-131">Then, copy the download link for the .tgz file for the appropriate version of Intel MPI.</span></span> <span data-ttu-id="89cdf-132">Bu makalede, Intel MPI sürüm 5.0.3.048 temel alır.</span><span class="sxs-lookup"><span data-stu-id="89cdf-132">This article is based on Intel MPI version 5.0.3.048.</span></span>
* <span data-ttu-id="89cdf-133">**OpenFOAM kaynak paketi** -Linux OpenFOAM kaynak paketi yazılımını indirmek [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span><span class="sxs-lookup"><span data-stu-id="89cdf-133">**OpenFOAM Source Pack** - Download the OpenFOAM Source Pack software for Linux from the [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span></span> <span data-ttu-id="89cdf-134">Bu makalede kaynak paketi sürümü 2.3.1, indirme için kullanılabilir OpenFOAM 2.3.1.tgz temel alır.</span><span class="sxs-lookup"><span data-stu-id="89cdf-134">This article is based on Source Pack version 2.3.1, available for download as OpenFOAM-2.3.1.tgz.</span></span> <span data-ttu-id="89cdf-135">Paketini açın ve Linux işlem düğümlerinde OpenFOAM derlemek için bu makalenin sonraki bölümlerinde'ndaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="89cdf-135">Follow the instructions later in this article to unpack and compile OpenFOAM on the Linux compute nodes.</span></span>
* <span data-ttu-id="89cdf-136">**EnSight** (isteğe bağlı) - OpenFOAM benzetimi, indirme ve yükleme sonuçları görmek için [EnSight](https://www.ceisoftware.com/download/) Görselleştirme ve analiz program.</span><span class="sxs-lookup"><span data-stu-id="89cdf-136">**EnSight** (optional) - To see the results of your OpenFOAM simulation, download and install the [EnSight](https://www.ceisoftware.com/download/) visualization and analysis program.</span></span> <span data-ttu-id="89cdf-137">Lisans ve yükleme bilgilerini EnSight sitede şunlardır.</span><span class="sxs-lookup"><span data-stu-id="89cdf-137">Licensing and download information are at the EnSight site.</span></span>

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="89cdf-138">İşlem düğümleri arasında karşılıklı güven ayarlama</span><span class="sxs-lookup"><span data-stu-id="89cdf-138">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="89cdf-139">Bir geçici düğüm işi birden çok Linux düğümler üzerinde çalışan düğümleri birbirine güvenen gerektirir (tarafından **rsh** veya **ssh**).</span><span class="sxs-lookup"><span data-stu-id="89cdf-139">Running a cross-node job on multiple Linux nodes requires the nodes to trust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="89cdf-140">Microsoft HPC Pack Iaas dağıtım komut dosyası ile HPC Pack kümesi oluşturduğunuzda, betik kalıcı karşılıklı güven belirttiğiniz yönetici hesabı için otomatik olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="89cdf-140">When you create the HPC Pack cluster with the Microsoft HPC Pack IaaS deployment script, the script automatically sets up permanent mutual trust for the administrator account you specify.</span></span> <span data-ttu-id="89cdf-141">Yönetici olmayan kullanıcılar, kümenin etki alanında oluşturmak için bir iş için ayrılmış düğümler arasında geçici karşılıklı güven ayarlamak sahip ve iş tamamlandıktan sonra ilişki yok.</span><span class="sxs-lookup"><span data-stu-id="89cdf-141">For non-administrator users you create in the cluster's domain, you have to set up temporary mutual trust among the nodes when a job is allocated to them, and destroy the relationship after the job is complete.</span></span> <span data-ttu-id="89cdf-142">Her kullanıcı için güven için bir RSA anahtar çifti için güven ilişkisi HPC Pack kullanan kümesi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-142">To establish trust for each user, provide an RSA key pair to the cluster that HPC Pack uses for the trust relationship.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="89cdf-143">RSA anahtar çifti oluşturma</span><span class="sxs-lookup"><span data-stu-id="89cdf-143">Generate an RSA key pair</span></span>
<span data-ttu-id="89cdf-144">Linux çalıştırarak bir ortak anahtar ve özel anahtarı içeren bir RSA anahtar çifti oluşturmak kolaydır **ssh-keygen** komutu.</span><span class="sxs-lookup"><span data-stu-id="89cdf-144">It's easy to generate an RSA key pair, which contains a public key and a private key, by running the Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="89cdf-145">Bir Linux bilgisayara oturum açın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-145">Log on to a Linux computer.</span></span>
2. <span data-ttu-id="89cdf-146">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="89cdf-146">Run the following command:</span></span>
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="89cdf-147">Tuşuna **Enter** komut tamamlanıncaya kadar varsayılan ayarları kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="89cdf-147">Press **Enter** to use the default settings until the command is completed.</span></span> <span data-ttu-id="89cdf-148">Burada bir parola girmeyin; için bir parola istendiğinde, yalnızca basın **Enter**.</span><span class="sxs-lookup"><span data-stu-id="89cdf-148">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![RSA anahtar çifti oluşturma][keygen]
3. <span data-ttu-id="89cdf-150">Dizin ~/.ssh dizine geçin.</span><span class="sxs-lookup"><span data-stu-id="89cdf-150">Change directory to the ~/.ssh directory.</span></span> <span data-ttu-id="89cdf-151">Özel anahtar id_rsa ve id_rsa.pub ortak anahtarında depolanır.</span><span class="sxs-lookup"><span data-stu-id="89cdf-151">The private key is stored in id_rsa and the public key in id_rsa.pub.</span></span>
   
   ![Özel ve genel anahtarlar][keys]

### <a name="add-the-key-pair-to-the-hpc-pack-cluster"></a><span data-ttu-id="89cdf-153">Anahtar çiftini HPC Pack kümeye ekleme</span><span class="sxs-lookup"><span data-stu-id="89cdf-153">Add the key pair to the HPC Pack cluster</span></span>
1. <span data-ttu-id="89cdf-154">Bir Uzak Masaüstü Bağlantısı, baş düğümüne HPC Pack Yönetici hesabınızla (dağıtım betiğini çalıştırdığınızda ayarladığınız yönetici hesabı) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="89cdf-154">Make a Remote Desktop connection to your head node with your HPC Pack administrator account (the administrator account you set up when you ran the deployment script).</span></span>
2. <span data-ttu-id="89cdf-155">Kümenin Active Directory etki alanında bir etki alanı kullanıcı hesabı oluşturmak için standart Windows Server yordamları kullanın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-155">Use standard Windows Server procedures to create a domain user account in the cluster's Active Directory domain.</span></span> <span data-ttu-id="89cdf-156">Örneğin, Active Directory Kullanıcıları ve Bilgisayarları aracını baş düğümünde kullanın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-156">For example, use the Active Directory User and Computers tool on the head node.</span></span> <span data-ttu-id="89cdf-157">Bu makaledeki örneklerde, hpclab\hpcuser adlı bir etki alanı kullanıcısı oluşturun varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="89cdf-157">The examples in this article assume you create a domain user named hpclab\hpcuser.</span></span>
3. <span data-ttu-id="89cdf-158">C:\cred.xml adlı bir dosya oluşturun ve RSA anahtar veri dosyasını buraya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-158">Create a file named C:\cred.xml and copy the RSA key data into it.</span></span> <span data-ttu-id="89cdf-159">Bir örnek cred.xml bu makalenin sonundaki dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="89cdf-159">A sample cred.xml file is at the end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy the contents of private key here</PrivateKey>
     <PublicKey>Copy the contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. <span data-ttu-id="89cdf-160">Bir komut istemi açın ve hpclab\hpcuser hesabı için kimlik bilgilerini veri kümesi için aşağıdaki komutu girin.</span><span class="sxs-lookup"><span data-stu-id="89cdf-160">Open a Command Prompt and enter the following command to set the credentials data for the hpclab\hpcuser account.</span></span> <span data-ttu-id="89cdf-161">Kullandığınız **extendeddata** dosyasının adı oluşturduğunuz C:\cred.xml anahtar verilerini geçirmek için parametre.</span><span class="sxs-lookup"><span data-stu-id="89cdf-161">You use the **extendeddata** parameter to pass the name of C:\cred.xml file you created for the key data.</span></span>
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="89cdf-162">Bu komut çıktısı başarıyla tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="89cdf-162">This command completes successfully without output.</span></span> <span data-ttu-id="89cdf-163">İşlerini çalıştırmak için gereken kullanıcı hesapları için kimlik bilgilerini ayarlama sonra cred.xml dosyayı güvenli bir konumda depolayın veya silin.</span><span class="sxs-lookup"><span data-stu-id="89cdf-163">After setting the credentials for the user accounts you need to run jobs, store the cred.xml file in a secure location, or delete it.</span></span>
5. <span data-ttu-id="89cdf-164">RSA anahtar çifti Linux düğümlerinden biri üzerinde oluşturursa, bunları kullanmayı bitirdikten sonra anahtarlarını silin unutmayın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-164">If you generated the RSA key pair on one of your Linux nodes, remember to delete the keys after you finish using them.</span></span> <span data-ttu-id="89cdf-165">HPC Pack varolan id_rsa dosyaya veya id_rsa.pub dosyası bulursa, karşılıklı güven ayarlı değil.</span><span class="sxs-lookup"><span data-stu-id="89cdf-165">If HPC Pack finds an existing id_rsa file or id_rsa.pub file, it does not set up mutual trust.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89cdf-166">Bir yönetici tarafından gönderilen bir işin Linux düğümleri kök hesapta çalıştığından Linux iş paylaşılan bir kümede bir Küme Yöneticisi olarak çalışan öneririz yok.</span><span class="sxs-lookup"><span data-stu-id="89cdf-166">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under the root account on the Linux nodes.</span></span> <span data-ttu-id="89cdf-167">Ancak, yönetici olmayan bir kullanıcı tarafından gönderilen bir işi işi kullanıcı aynı ada sahip bir yerel Linux kullanıcı hesabı altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="89cdf-167">However, a job submitted by a non-administrator user runs under a local Linux user account with the same name as the job user.</span></span> <span data-ttu-id="89cdf-168">Bu durumda, HPC Pack karşılıklı güven bu Linux kullanıcı için iş için ayrılan düğümler arasında ayarlar.</span><span class="sxs-lookup"><span data-stu-id="89cdf-168">In this case, HPC Pack sets up mutual trust for this Linux user across the nodes allocated to the job.</span></span> <span data-ttu-id="89cdf-169">Linux kullanıcı el ile Linux düğümleri üzerinde iş çalıştırmadan önce ayarlayabilirsiniz veya iş gönderildiğinde HPC Pack kullanıcı otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="89cdf-169">You can set up the Linux user manually on the Linux nodes before running the job, or HPC Pack creates the user automatically when the job is submitted.</span></span> <span data-ttu-id="89cdf-170">HPC Pack kullanıcı oluşturursa, HPC Pack işi tamamlandıktan sonra onu siler.</span><span class="sxs-lookup"><span data-stu-id="89cdf-170">If HPC Pack creates the user, HPC Pack deletes it after the job completes.</span></span> <span data-ttu-id="89cdf-171">Güvenlik tehditleri azaltmak için HPC Pack işi tamamlandıktan sonra anahtarlarını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="89cdf-171">To reduce security threats, HPC Pack removes the keys after job completion.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="89cdf-172">Linux düğümleri için bir dosya paylaşımı ayarlama</span><span class="sxs-lookup"><span data-stu-id="89cdf-172">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="89cdf-173">Baş düğüm üzerinde bir klasör standart bir SMB paylaşımında şimdi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-173">Now set up a standard SMB share on a folder on the head node.</span></span> <span data-ttu-id="89cdf-174">Ortak yoluna sahip uygulama dosyalara erişmek Linux düğümleri izin vermek için Linux düğümlerinde paylaşılan klasöre bağlayın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-174">To allow the Linux nodes to access application files with a common path, mount the shared folder on the Linux nodes.</span></span> <span data-ttu-id="89cdf-175">İsterseniz, başka bir dosya paylaşımı gibi birçok senaryo - ya da bir NFS paylaşımına için önerilen bir Azure dosya paylaşımı - seçeneği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89cdf-175">If you want, you can use another file sharing option, such as an Azure Files share - recommended for many scenarios - or an NFS share.</span></span> <span data-ttu-id="89cdf-176">Dosya bilgileri ve ayrıntılı adımlar paylaşımı bkz [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="89cdf-176">See the file sharing information and detailed steps in [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="89cdf-177">Baş düğüm üzerinde bir klasör oluşturun ve herkese okuma/yazma ayrıcalıklarına ayarlayarak paylaşın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-177">Create a folder on the head node, and share it to Everyone by setting Read/Write privileges.</span></span> <span data-ttu-id="89cdf-178">Örneğin, baş düğüm C:\OpenFOAM paylaşmak \\ \\SUSE12RDMA HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="89cdf-178">For example, share C:\OpenFOAM on the head node as \\\\SUSE12RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="89cdf-179">Burada, *SUSE12RDMA HN* baş düğüm ana bilgisayar adıdır.</span><span class="sxs-lookup"><span data-stu-id="89cdf-179">Here, *SUSE12RDMA-HN* is the host name of the head node.</span></span>
2. <span data-ttu-id="89cdf-180">Bir Windows PowerShell penceresi açın ve aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="89cdf-180">Open a Windows PowerShell window and run the following commands:</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

<span data-ttu-id="89cdf-181">İlk komut LinuxNodes grubundaki tüm düğümlerde /openfoam adlı bir klasör oluşturur.</span><span class="sxs-lookup"><span data-stu-id="89cdf-181">The first command creates a folder named /openfoam on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="89cdf-182">İkinci komut dir_mode ile Linux düğümlerdeki paylaşılan klasör //SUSE12RDMA-HN/OpenFOAM bağlar ve file_mode BITS 777 ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-182">The second command mounts the shared folder //SUSE12RDMA-HN/OpenFOAM on the Linux nodes with dir_mode and file_mode bits set to 777.</span></span> <span data-ttu-id="89cdf-183">*Kullanıcıadı* ve *parola* komutta baş düğüm bir kullanıcının kimlik bilgileri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="89cdf-183">The *username* and *password* in the command should be the credentials of a user on the head node.</span></span>

> [!NOTE]
> <span data-ttu-id="89cdf-184">"\\`" İkinci komut dosyasındaki simge olan bir PowerShell kaçış simgesi.</span><span class="sxs-lookup"><span data-stu-id="89cdf-184">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="89cdf-185">"\\`," "," (virgül karakteri) anlamına gelir komutu, bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="89cdf-185">“\\`,” means the “,” (comma character) is a part of the command.</span></span>
> 
> 

## <a name="install-mpi-and-openfoam"></a><span data-ttu-id="89cdf-186">MPI ve OpenFOAM yükleyin</span><span class="sxs-lookup"><span data-stu-id="89cdf-186">Install MPI and OpenFOAM</span></span>
<span data-ttu-id="89cdf-187">OpenFOAM RDMA ağ üzerinde bir MPI iş olarak çalıştırmak için Intel MPI kitaplıklarıyla OpenFOAM derlemek gerekir.</span><span class="sxs-lookup"><span data-stu-id="89cdf-187">To run OpenFOAM as an MPI job on the RDMA network, you need to compile OpenFOAM with the Intel MPI libraries.</span></span> 

<span data-ttu-id="89cdf-188">Öncelikle birkaç çalıştırın **clusrun** Intel MPI kitaplıkları (henüz yüklenmemişse) yüklemek için komutları ve Linux düğümleri üzerinde OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="89cdf-188">First, run several **clusrun** commands to install Intel MPI libraries (if not already installed) and OpenFOAM on your Linux nodes.</span></span> <span data-ttu-id="89cdf-189">Yükleme dosyaları Linux düğümleri arasında paylaşmak için önceden yapılandırılmış baş düğüm paylaşımı kullanın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-189">Use the head node share configured previously to share the installation files among the Linux nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89cdf-190">Bu yükleme ve derleniyor adımları verilebilir.</span><span class="sxs-lookup"><span data-stu-id="89cdf-190">These installation and compiling steps are examples.</span></span> <span data-ttu-id="89cdf-191">Bazı bağımlı derleyicileri ve kitaplıklarını doğru şekilde yüklendiğinden emin olmak için Linux sistem yönetim bilgisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="89cdf-191">You need some knowledge of Linux system administration to ensure that dependent compilers and libraries are installed correctly.</span></span> <span data-ttu-id="89cdf-192">Belirli ortam değişkenleri veya Intel MPI ve OpenFOAM sürümü için diğer ayarları değiştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="89cdf-192">You might need to modify certain environment variables or other settings for your versions of Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="89cdf-193">Ayrıntılar için bkz [Linux Yükleme Kılavuzu için Intel MPI Kitaplığı](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) ve [OpenFOAM kaynak paketi yüklemesi](http://openfoam.org/download/2-3-1-source/) ortamınız için.</span><span class="sxs-lookup"><span data-stu-id="89cdf-193">For details, see [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) and [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) for your environment.</span></span>
> 
> 

### <a name="install-intel-mpi"></a><span data-ttu-id="89cdf-194">Intel MPI yükleyin</span><span class="sxs-lookup"><span data-stu-id="89cdf-194">Install Intel MPI</span></span>
<span data-ttu-id="89cdf-195">Linux düğümleri bu dosyayı /openfoam erişebilmesi için indirilen yükleme paketi Intel MPI (Bu örnekte l_mpi_p_5.0.3.048.tgz) için C:\OpenFoam baş düğümünde kaydedin.</span><span class="sxs-lookup"><span data-stu-id="89cdf-195">Save the downloaded installation package for Intel MPI (l_mpi_p_5.0.3.048.tgz in this example) in C:\OpenFoam on the head node so that the Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="89cdf-196">Ardından çalıştırın **clusrun** Intel MPI kitaplığı tüm Linux düğümlerine yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="89cdf-196">Then run **clusrun** to install Intel MPI library on all the Linux nodes.</span></span>

1. <span data-ttu-id="89cdf-197">Aşağıdaki komutları yükleme paketini kopyalayın ve her düğümde /opt/intel ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-197">The following commands copy the installation package and extract it to /opt/intel on each node.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. <span data-ttu-id="89cdf-198">Intel MPI kitaplığı sessizce yüklemek için silent.cfg dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-198">To install Intel MPI Library silently, use a silent.cfg file.</span></span> <span data-ttu-id="89cdf-199">Bu makalenin sonunda örnek dosyalarını bir örnek bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89cdf-199">You can find an example in the sample files at the end of this article.</span></span> <span data-ttu-id="89cdf-200">Bu dosyayı paylaşılan klasör /openfoam yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="89cdf-200">Place this file in the shared folder /openfoam.</span></span> <span data-ttu-id="89cdf-201">Silent.cfg dosyası hakkında daha fazla ayrıntı için bkz: [Linux Yükleme Kılavuzu - sessiz yükleme için Intel MPI Kitaplığı](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span><span class="sxs-lookup"><span data-stu-id="89cdf-201">For details about the silent.cfg file, see [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="89cdf-202">Silent.cfg dosyanız Linux sahip bir metin dosyası olarak kaydettiğinizde satır sonlarını (yalnızca LF, CR LF) emin olun.</span><span class="sxs-lookup"><span data-stu-id="89cdf-202">Make sure that you save your silent.cfg file as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="89cdf-203">Bu adım, düzgün şekilde Linux düğümlerinde çalıştığını sağlar.</span><span class="sxs-lookup"><span data-stu-id="89cdf-203">This step ensures that it runs properly on the Linux nodes.</span></span>
   > 
   > 
3. <span data-ttu-id="89cdf-204">Intel MPI kitaplığı sessiz modda yükleyin.</span><span class="sxs-lookup"><span data-stu-id="89cdf-204">Install Intel MPI Library in silent mode.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a><span data-ttu-id="89cdf-205">MPI yapılandırın</span><span class="sxs-lookup"><span data-stu-id="89cdf-205">Configure MPI</span></span>
<span data-ttu-id="89cdf-206">Test etmek için aşağıdaki satırları /etc/security/limits.conf her Linux düğümleri için eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="89cdf-206">For testing, you should add the following lines to the /etc/security/limits.conf on each of the Linux nodes:</span></span>

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


<span data-ttu-id="89cdf-207">Limits.conf dosya güncelleştirdikten sonra Linux düğümleri yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-207">Restart the Linux nodes after you update the limits.conf file.</span></span> <span data-ttu-id="89cdf-208">Örneğin, aşağıdaki kullanın **clusrun** komutu:</span><span class="sxs-lookup"><span data-stu-id="89cdf-208">For example, use the following **clusrun** command:</span></span>

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

<span data-ttu-id="89cdf-209">Yeniden başlattıktan sonra paylaşılan klasör /openfoam bağlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="89cdf-209">After restarting, ensure that the shared folder is mounted as /openfoam.</span></span>

### <a name="compile-and-install-openfoam"></a><span data-ttu-id="89cdf-210">Derleme ve OpenFOAM yükleyin</span><span class="sxs-lookup"><span data-stu-id="89cdf-210">Compile and install OpenFOAM</span></span>
<span data-ttu-id="89cdf-211">Linux düğümleri bu dosyayı /openfoam erişebilmesi için indirilen yükleme paketi C:\OpenFoam OpenFOAM kaynak paketine (Bu örnekte, OpenFOAM-2.3.1.tgz) için baş düğümünde kaydedin.</span><span class="sxs-lookup"><span data-stu-id="89cdf-211">Save the downloaded installation package for the OpenFOAM Source Pack (OpenFOAM-2.3.1.tgz in this example) to C:\OpenFoam on the head node so that the Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="89cdf-212">Ardından çalıştırın **clusrun** OpenFOAM tüm Linux düğümlerine derlemek için komutları.</span><span class="sxs-lookup"><span data-stu-id="89cdf-212">Then run **clusrun** commands to compile OpenFOAM on all the Linux nodes.</span></span>

1. <span data-ttu-id="89cdf-213">Her bir Linux düğümde bir klasör /opt/OpenFOAM oluşturma kaynak paketi bu klasöre kopyalayın ve var. ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-213">Create a folder /opt/OpenFOAM on each Linux node, copy the source package to this folder, and extract it there.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. <span data-ttu-id="89cdf-214">Intel MPI kitaplığıyla OpenFOAM derlemek için önce bazı ortam değişkenleri Intel MPI hem OpenFOAM ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-214">To compile OpenFOAM with the Intel MPI Library, first set up some environment variables for both Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="89cdf-215">Settings.sh adlı bir bash komut dosyası değişkenleri ayarlamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-215">Use a bash script called settings.sh to set the variables.</span></span> <span data-ttu-id="89cdf-216">Bu makalenin sonunda örnek dosyalarını bir örnek bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89cdf-216">You can find an example in the sample files at the end of this article.</span></span> <span data-ttu-id="89cdf-217">(Linux satır sonları ile kaydedilen) Bu dosya paylaşılan klasör /openfoam yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="89cdf-217">Place this file (saved with Linux line endings) in the shared folder /openfoam.</span></span> <span data-ttu-id="89cdf-218">Bu dosya ayrıca daha sonra bir OpenFOAM işi çalıştırmak için kullandığınız MPI ve OpenFOAM çalışma zamanları ayarlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="89cdf-218">This file also contains settings for the MPI and OpenFOAM runtimes that you use later to run an OpenFOAM job.</span></span>
3. <span data-ttu-id="89cdf-219">Bağımlı paketler OpenFOAM derlemek için gereken yükleyin.</span><span class="sxs-lookup"><span data-stu-id="89cdf-219">Install dependent packages needed to compile OpenFOAM.</span></span> <span data-ttu-id="89cdf-220">Linux dağıtımınız bağlı olarak, önce bir havuz eklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="89cdf-220">Depending on your Linux distribution, you might first need to add a repository.</span></span> <span data-ttu-id="89cdf-221">Çalıştırma **clusrun** komutları aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="89cdf-221">Run **clusrun** commands similar to the following:</span></span>
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    <span data-ttu-id="89cdf-222">Gerekirse, bunların düzgün çalıştığını doğrulamak için komutları çalıştırmak için SSH her Linux düğümü.</span><span class="sxs-lookup"><span data-stu-id="89cdf-222">If necessary, SSH to each Linux node to run the commands to confirm that they run properly.</span></span>
4. <span data-ttu-id="89cdf-223">OpenFOAM derlemek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-223">Run the following command to compile OpenFOAM.</span></span> <span data-ttu-id="89cdf-224">Derleme işlemi tamamlanması biraz zaman alır ve büyük miktarda standart çıktı için günlük bilgilerini oluşturur, böylece kullanma **/ araya eklemeli** araya eklemeli çıktı görüntülemek için seçeneği.</span><span class="sxs-lookup"><span data-stu-id="89cdf-224">The compilation process takes some time to complete and generates a large amount of log information to standard output, so use the **/interleaved** option to display the output interleaved.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > <span data-ttu-id="89cdf-225">"\\`" Komutta simgenin olup PowerShell bir kaçış simgesi.</span><span class="sxs-lookup"><span data-stu-id="89cdf-225">The “\\`” symbol in the command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="89cdf-226">"\\`&" anlamına gelir "&" komutu, bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="89cdf-226">“\\`&” means the “&” is a part of the command.</span></span>
   > 
   > 

## <a name="prepare-to-run-an-openfoam-job"></a><span data-ttu-id="89cdf-227">Bir OpenFOAM işi çalıştırmak hazırlama</span><span class="sxs-lookup"><span data-stu-id="89cdf-227">Prepare to run an OpenFOAM job</span></span>
<span data-ttu-id="89cdf-228">Şimdi, iki Linux düğümlerinde OpenFoam örnekleri olan sloshingTank3D adlı bir MPI işi çalıştırmak hazırlanın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-228">Now get ready to run an MPI job called sloshingTank3D, which is one of the OpenFoam samples, on two Linux nodes.</span></span> 

### <a name="set-up-the-runtime-environment"></a><span data-ttu-id="89cdf-229">Çalışma zamanı ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="89cdf-229">Set up the runtime environment</span></span>
<span data-ttu-id="89cdf-230">Çalışma zamanı ortamı MPI ve OpenFOAM için Linux düğümleri üzerinde ayarlamak için baş düğüm üzerinde bir Windows PowerShell penceresinde aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-230">To set up the runtime environments for MPI and OpenFOAM on the Linux nodes, run the following command in a Windows PowerShell window on the head node.</span></span> <span data-ttu-id="89cdf-231">(Bu komut, yalnızca SUSE Linux için geçerlidir.)</span><span class="sxs-lookup"><span data-stu-id="89cdf-231">(This command is valid for SUSE Linux only.)</span></span>

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a><span data-ttu-id="89cdf-232">Örnek verileri hazırlama</span><span class="sxs-lookup"><span data-stu-id="89cdf-232">Prepare sample data</span></span>
<span data-ttu-id="89cdf-233">Daha önce (/openfoam takılı) Linux düğümleri arasında dosya paylaşmak üzere yapılandırılmış baş düğüm paylaşımı kullanın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-233">Use the head node share you configured previously to share files among the Linux nodes (mounted as /openfoam).</span></span>

1. <span data-ttu-id="89cdf-234">SSH bir, Linux işlem düğümlerini.</span><span class="sxs-lookup"><span data-stu-id="89cdf-234">SSH to one of your Linux compute nodes.</span></span>
2. <span data-ttu-id="89cdf-235">Bunu zaten yapmadıysanız OpenFOAM çalışma zamanı ortamı, ayarlamak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-235">Run the following command to set up the OpenFOAM runtime environment, if you haven’t already done this.</span></span>
   
   ```
   $ source /openfoam/settings.sh
   ```
3. <span data-ttu-id="89cdf-236">SloshingTank3D örneği paylaşılan klasöre kopyalayın ve kendisine gidin.</span><span class="sxs-lookup"><span data-stu-id="89cdf-236">Copy the sloshingTank3D sample to the shared folder and navigate to it.</span></span>
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. <span data-ttu-id="89cdf-237">Bu örnek varsayılan parametrelerini kullandığınızda, daha hızlı çalışmasını sağlamak için bazı parametreler değiştirmek isteyebilirsiniz onlarca çalıştırmak için dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="89cdf-237">When you use the default parameters of this sample, it can take tens of minutes to run, so you might want to modify some parameters to make it run faster.</span></span> <span data-ttu-id="89cdf-238">Bir basit zaman adım değişkenleri deltaT ve sistem/controlDict dosyasında writeInterval değiştirmek için bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="89cdf-238">One simple choice is to modify the time step variables deltaT and writeInterval in the system/controlDict file.</span></span> <span data-ttu-id="89cdf-239">Bu dosyayı saat ve okuma ve çözüm veri yazma denetim ile ilgili tüm giriş verilerini depolar.</span><span class="sxs-lookup"><span data-stu-id="89cdf-239">This file stores all input data relating to the control of time and reading and writing solution data.</span></span> <span data-ttu-id="89cdf-240">Örneğin, 0,05 gelen deltaT 0,5 değeri ve 0,05 gelen writeInterval 0,5 değeri değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="89cdf-240">For example, you could change the value of deltaT from 0.05 to 0.5 and the value of writeInterval from 0.05 to 0.5.</span></span>
   
   ![Adım değişkenleri değiştirin][step_variables]
5. <span data-ttu-id="89cdf-242">Sistem/decomposeParDict dosyasında değişkenleri için istenen değerleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="89cdf-242">Specify desired values for the variables in the system/decomposeParDict file.</span></span> <span data-ttu-id="89cdf-243">Bu örnek iki Linux düğümleri her 8 çekirdeğiyle kullanır, böylece numberOfSubdomains 16 hierarchicalCoeffs için n ayarlayın (1 1 16), 16 süreçleri ile paralel OpenFOAM anlamına çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-243">This example uses two Linux nodes each with 8 cores, so set numberOfSubdomains to 16 and n of hierarchicalCoeffs to (1 1 16), which means run OpenFOAM in parallel with 16 processes.</span></span> <span data-ttu-id="89cdf-244">Daha fazla bilgi için bkz: [OpenFOAM Kullanıcı Kılavuzu: paralel 3.4 çalışan uygulamaları](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span><span class="sxs-lookup"><span data-stu-id="89cdf-244">For more information, see [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span></span>
   
   ![İşlemler parçalayın][decompose]
6. <span data-ttu-id="89cdf-246">Örnek verileri hazırlamak için sloshingTank3D dizininden aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-246">Run the following commands from the sloshingTank3D directory to prepare the sample data.</span></span>
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. <span data-ttu-id="89cdf-247">Baş düğümünde örnek veri dosyalarını C:\OpenFoam\sloshingTank3D kopyalanır görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="89cdf-247">On the head node, you should see the sample data files are copied into C:\OpenFoam\sloshingTank3D.</span></span> <span data-ttu-id="89cdf-248">(C:\OpenFoam paylaşılan baş düğüm klasörüdür.)</span><span class="sxs-lookup"><span data-stu-id="89cdf-248">(C:\OpenFoam is the shared folder on the head node.)</span></span>
   
   ![Baş düğüm veri dosyaları][data_files]

### <a name="host-file-for-mpirun"></a><span data-ttu-id="89cdf-250">Ana bilgisayar dosyası mpirun için</span><span class="sxs-lookup"><span data-stu-id="89cdf-250">Host file for mpirun</span></span>
<span data-ttu-id="89cdf-251">Bu adımda, bir ana bilgisayar dosyası (işlem düğümleri listesi) oluşturmak, **mpirun** komutunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="89cdf-251">In this step, you create a host file (a list of compute nodes) which the **mpirun** command uses.</span></span>

1. <span data-ttu-id="89cdf-252">Linux düğümleri her birinde bu dosyayı /openfoam/hostfile tüm Linux düğümlerde üzerinde erişilebilir şekilde /openfoam altında hostfile adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="89cdf-252">On one of the Linux nodes, create a file named hostfile under /openfoam, so this file can be reached at /openfoam/hostfile on all Linux nodes.</span></span>
2. <span data-ttu-id="89cdf-253">Linux düğüm adları bu dosyaya yazma.</span><span class="sxs-lookup"><span data-stu-id="89cdf-253">Write your Linux node names into this file.</span></span> <span data-ttu-id="89cdf-254">Bu örnekte, dosya aşağıdaki adları içerir:</span><span class="sxs-lookup"><span data-stu-id="89cdf-254">In this example, the file contains the following names:</span></span>
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > <span data-ttu-id="89cdf-255">Bu dosya C:\OpenFoam\hostfile baş düğümünde de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89cdf-255">You can also create this file at C:\OpenFoam\hostfile on the head node.</span></span> <span data-ttu-id="89cdf-256">Bu seçeneği seçerseniz, Linux bir metin dosyası olarak kaydedin (yalnızca LF, CR LF) satır sonlarını.</span><span class="sxs-lookup"><span data-stu-id="89cdf-256">If you choose this option, save it as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="89cdf-257">Bu, düzgün şekilde Linux düğümlerinde çalıştığını sağlar.</span><span class="sxs-lookup"><span data-stu-id="89cdf-257">This ensures that it runs properly on the Linux nodes.</span></span>
   > 
   > 
   
   <span data-ttu-id="89cdf-258">**Bash betik sarmalayıcı**</span><span class="sxs-lookup"><span data-stu-id="89cdf-258">**Bash script wrapper**</span></span>
   
   <span data-ttu-id="89cdf-259">Hangi düğümlerin işinize ayrılır tanımadığınız için birçok Linux düğümleri varsa ve işinizin yalnızca bunlardan bazıları üzerinde çalıştırmak istediğiniz, onu bir sabit ana bilgisayar dosyası kullanmak için iyi bir fikir değil.</span><span class="sxs-lookup"><span data-stu-id="89cdf-259">If you have many Linux nodes and you want your job to run on only some of them, it’s not a good idea to use a fixed host file, because you don’t know which nodes will be allocated to your job.</span></span> <span data-ttu-id="89cdf-260">Bu durumda, bir bash betik sarmalayıcı için yazma **mpirun** ana bilgisayar dosyası otomatik olarak oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="89cdf-260">In this case, write a bash script wrapper for **mpirun** to create the host file automatically.</span></span> <span data-ttu-id="89cdf-261">Bu makalenin sonunda hpcimpirun.sh olarak adlandırılan bir örnek bash betik sarmalayıcı bulmak ve /openfoam/hpcimpirun.sh kaydedin.</span><span class="sxs-lookup"><span data-stu-id="89cdf-261">You can find an example bash script wrapper called hpcimpirun.sh at the end of this article, and save it as /openfoam/hpcimpirun.sh.</span></span> <span data-ttu-id="89cdf-262">Bu örnek komut dosyası şunları yapar:</span><span class="sxs-lookup"><span data-stu-id="89cdf-262">This example script does the following:</span></span>
   
   1. <span data-ttu-id="89cdf-263">İçin ortam değişkenleri ayarlar **mpirun**ve RDMA ağ üzerinden MPI işi çalıştırmak için bazı ek komut parametreleri.</span><span class="sxs-lookup"><span data-stu-id="89cdf-263">Sets up the environment variables for **mpirun**, and some addition command parameters to run the MPI job through the RDMA network.</span></span> <span data-ttu-id="89cdf-264">Bu durumda, aşağıdaki değişkenleri ayarlar:</span><span class="sxs-lookup"><span data-stu-id="89cdf-264">In this case, it sets the following variables:</span></span>
      
      * <span data-ttu-id="89cdf-265">I_MPI_FABRICS shm:dapl =</span><span class="sxs-lookup"><span data-stu-id="89cdf-265">I_MPI_FABRICS=shm:dapl</span></span>
      * <span data-ttu-id="89cdf-266">I_MPI_DAPL_PROVIDER bir v2 ib0 =</span><span class="sxs-lookup"><span data-stu-id="89cdf-266">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span></span>
      * <span data-ttu-id="89cdf-267">I_MPI_DYNAMIC_CONNECTION = 0</span><span class="sxs-lookup"><span data-stu-id="89cdf-267">I_MPI_DYNAMIC_CONNECTION=0</span></span>
   2. <span data-ttu-id="89cdf-268">Ortam göre bir ana bilgisayar dosyası oluşturur değişken $ iş etkinleştirildiğinde, HPC baş düğümü tarafından ayarlanan CCP_NODES_CORES.</span><span class="sxs-lookup"><span data-stu-id="89cdf-268">Creates a host file according to the environment variable $CCP_NODES_CORES, which is set by the HPC head node when the job is activated.</span></span>
      
      <span data-ttu-id="89cdf-269">$CCP_NODES_CORES biçimlerinin bu deseni izler:</span><span class="sxs-lookup"><span data-stu-id="89cdf-269">The format of $CCP_NODES_CORES follows this pattern:</span></span>
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      <span data-ttu-id="89cdf-270">Burada</span><span class="sxs-lookup"><span data-stu-id="89cdf-270">where</span></span>
      
      * <span data-ttu-id="89cdf-271">`<Number of nodes>`-Bu iş için ayrılmış düğüm sayısı.</span><span class="sxs-lookup"><span data-stu-id="89cdf-271">`<Number of nodes>` - the number of nodes allocated to this job.</span></span>  
      * <span data-ttu-id="89cdf-272">`<Name of node_n_...>`-Bu iş için ayrılmış her düğümün adı.</span><span class="sxs-lookup"><span data-stu-id="89cdf-272">`<Name of node_n_...>` - the name of each node allocated to this job.</span></span>
      * <span data-ttu-id="89cdf-273">`<Cores of node_n_...>`-Bu iş için ayrılmış düğümünde çekirdek sayısı.</span><span class="sxs-lookup"><span data-stu-id="89cdf-273">`<Cores of node_n_...>` - the number of cores on the node allocated to this job.</span></span>
      
      <span data-ttu-id="89cdf-274">Örneğin, işi çalıştırmak için iki düğüm gerekirse, $CCP_NODES_CORES benzer.</span><span class="sxs-lookup"><span data-stu-id="89cdf-274">For example, if the job needs two nodes to run, $CCP_NODES_CORES is similar to</span></span>
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. <span data-ttu-id="89cdf-275">Çağrıları **mpirun** komut ve iki parametre için komut satırını ekler.</span><span class="sxs-lookup"><span data-stu-id="89cdf-275">Calls the **mpirun** command and appends two parameters to the command line.</span></span>
      
      * <span data-ttu-id="89cdf-276">`--hostfile <hostfilepath>: <hostfilepath>`-komut dosyası oluşturur ana bilgisayar dosyasının yolu</span><span class="sxs-lookup"><span data-stu-id="89cdf-276">`--hostfile <hostfilepath>: <hostfilepath>` - the path of the host file the script creates</span></span>
      * <span data-ttu-id="89cdf-277">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`-Bu iş için ayrılan toplam çekirdek sayısı depolar HPC paketi üstbilgi düğümü tarafından ayarlanan bir ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="89cdf-277">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - an environment variable set by the HPC Pack head node, which stores the number of total cores allocated to this job.</span></span> <span data-ttu-id="89cdf-278">Bu durumda, işlemler için sayısını belirtir **mpirun**.</span><span class="sxs-lookup"><span data-stu-id="89cdf-278">In this case, it specifies the number of processes for **mpirun**.</span></span>

## <a name="submit-an-openfoam-job"></a><span data-ttu-id="89cdf-279">Bir OpenFOAM işi gönderin</span><span class="sxs-lookup"><span data-stu-id="89cdf-279">Submit an OpenFOAM job</span></span>
<span data-ttu-id="89cdf-280">Şimdi bir işi HPC Küme Yöneticisi'nde gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89cdf-280">Now you can submit a job in HPC Cluster Manager.</span></span> <span data-ttu-id="89cdf-281">Komut satırlarında bazı iş görevleri için komut dosyası hpcimpirun.sh geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="89cdf-281">You need to pass the script hpcimpirun.sh in the command lines for some of the job tasks.</span></span>

1. <span data-ttu-id="89cdf-282">Küme baş düğümüne bağlanmak ve HPC Küme Yöneticisi'ni başlatın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-282">Connect to your cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="89cdf-283">**Kaynak Yönetimi'nde**, Linux işlem düğümü olduğundan emin olun **çevrimiçi** durumu.</span><span class="sxs-lookup"><span data-stu-id="89cdf-283">**In Resource Management**, ensure that the Linux compute nodes are in the **Online** state.</span></span> <span data-ttu-id="89cdf-284">Değilse, bunları seçin ve tıklatın **çevrimiçine**.</span><span class="sxs-lookup"><span data-stu-id="89cdf-284">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="89cdf-285">İçinde **iş yönetimi**, tıklatın **yeni iş**.</span><span class="sxs-lookup"><span data-stu-id="89cdf-285">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="89cdf-286">İş için bir ad girin *sloshingTank3D*.</span><span class="sxs-lookup"><span data-stu-id="89cdf-286">Enter a name for job such as *sloshingTank3D*.</span></span>
   
   ![İş ayrıntıları][job_details]
5. <span data-ttu-id="89cdf-288">İçinde **iş kaynakları**, "Düğümü" olarak kaynak türünü seçin ve en az 2'ye ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-288">In **Job resources**, choose the type of resource as “Node” and set the Minimum to 2.</span></span> <span data-ttu-id="89cdf-289">Bu yapılandırma, bu örnekte, her biri sekiz çekirdeği olması iki Linux düğümlerde işi çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="89cdf-289">This configuration runs the job on two Linux nodes, each of which has eight cores in this example.</span></span>
   
   ![İş kaynakları][job_resources]
6. <span data-ttu-id="89cdf-291">Tıklatın **Düzenle görevleri** sol gezinti ve ardından **Ekle** iş için bir görev eklemek için.</span><span class="sxs-lookup"><span data-stu-id="89cdf-291">Click **Edit Tasks** in the left navigation, and then click **Add** to add a task to the job.</span></span> <span data-ttu-id="89cdf-292">Aşağıdaki komut satırları ve ayarlar işlemiyle dört görevleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="89cdf-292">Add four tasks to the job with the following command lines and settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="89cdf-293">Çalışan `source /openfoam/settings.sh` her aşağıdaki görevlerden önce OpenFOAM komutunu çağırır OpenFOAM ve MPI çalışma zamanı ortamları ayarlar.</span><span class="sxs-lookup"><span data-stu-id="89cdf-293">Running `source /openfoam/settings.sh` sets up the OpenFOAM and MPI runtime environments, so each of the following tasks calls it before the OpenFOAM command.</span></span>
   > 
   > 
   
   * <span data-ttu-id="89cdf-294">**Görev 1**.</span><span class="sxs-lookup"><span data-stu-id="89cdf-294">**Task 1**.</span></span> <span data-ttu-id="89cdf-295">Çalıştırma **decomposePar** çalıştırmak için veri dosyaları oluşturmak için **interDyMFoam** paralel.</span><span class="sxs-lookup"><span data-stu-id="89cdf-295">Run **decomposePar** to generate data files for running **interDyMFoam** in parallel.</span></span>
     
     * <span data-ttu-id="89cdf-296">Bir düğüm göreve atayın</span><span class="sxs-lookup"><span data-stu-id="89cdf-296">Assign one node to the task</span></span>
     * <span data-ttu-id="89cdf-297">**Komut satırı** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="89cdf-297">**Command line** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="89cdf-298">**Çalışma dizini** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="89cdf-298">**Working directory** - /openfoam/sloshingTank3D</span></span>
     
     <span data-ttu-id="89cdf-299">Aşağıdaki şekle bakın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-299">See the following figure.</span></span> <span data-ttu-id="89cdf-300">Kalan görevlere benzer şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-300">You configure the remaining tasks similarly.</span></span>
     
     ![Görev 1 ayrıntıları][task_details1]
   * <span data-ttu-id="89cdf-302">**Görev 2**.</span><span class="sxs-lookup"><span data-stu-id="89cdf-302">**Task 2**.</span></span> <span data-ttu-id="89cdf-303">Çalıştırma **interDyMFoam** paralel işlem örnek.</span><span class="sxs-lookup"><span data-stu-id="89cdf-303">Run **interDyMFoam** in parallel to compute the sample.</span></span>
     
     * <span data-ttu-id="89cdf-304">İki düğüm göreve atayın</span><span class="sxs-lookup"><span data-stu-id="89cdf-304">Assign two nodes to the task</span></span>
     * <span data-ttu-id="89cdf-305">**Komut satırı** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="89cdf-305">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="89cdf-306">**Çalışma dizini** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="89cdf-306">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="89cdf-307">**Görev 3**.</span><span class="sxs-lookup"><span data-stu-id="89cdf-307">**Task 3**.</span></span> <span data-ttu-id="89cdf-308">Çalıştırma **reconstructPar** tek bir kümesine her processor_N_ dizini zaman dizinlerden kümeleri birleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="89cdf-308">Run **reconstructPar** to merge the sets of time directories from each processor_N_ directory into a single set.</span></span>
     
     * <span data-ttu-id="89cdf-309">Bir düğüm göreve atayın</span><span class="sxs-lookup"><span data-stu-id="89cdf-309">Assign one node to the task</span></span>
     * <span data-ttu-id="89cdf-310">**Komut satırı** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="89cdf-310">**Command line** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="89cdf-311">**Çalışma dizini** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="89cdf-311">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="89cdf-312">**Görev 4**.</span><span class="sxs-lookup"><span data-stu-id="89cdf-312">**Task 4**.</span></span> <span data-ttu-id="89cdf-313">Çalıştırma **foamToEnsight** OpenFOAM sonuç dönüştürmek için paralel EnSight dosyalarıyla biçimlendirmek ve büyük/küçük harfe dizinde Ensight adlı bir dizin EnSight dosyaları yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="89cdf-313">Run **foamToEnsight** in parallel to convert the OpenFOAM result files into EnSight format and place the EnSight files in a directory named Ensight in the case directory.</span></span>
     
     * <span data-ttu-id="89cdf-314">İki düğüm göreve atayın</span><span class="sxs-lookup"><span data-stu-id="89cdf-314">Assign two nodes to the task</span></span>
     * <span data-ttu-id="89cdf-315">**Komut satırı** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="89cdf-315">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="89cdf-316">**Çalışma dizini** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="89cdf-316">**Working directory** - /openfoam/sloshingTank3D</span></span>
7. <span data-ttu-id="89cdf-317">Bu görevleri görev artan bağımlılıkları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="89cdf-317">Add dependencies to these tasks in ascending task order.</span></span>
   
   ![Görev bağımlılıkları][task_dependencies]
8. <span data-ttu-id="89cdf-319">Tıklatın **gönderme** bu işi çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="89cdf-319">Click **Submit** to run this job.</span></span>
   
   <span data-ttu-id="89cdf-320">Varsayılan olarak, geçerli oturum açmış kullanıcı hesabınız olarak işi HPC paketi gönderir.</span><span class="sxs-lookup"><span data-stu-id="89cdf-320">By default, HPC Pack submits the job as your current logged-on user account.</span></span> <span data-ttu-id="89cdf-321">Tıklattıktan sonra **gönderme**, kullanıcı adını ve parolasını girmenizi isteyen bir iletişim kutusu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89cdf-321">After you click **Submit**, you might see a dialog box prompting you to enter the user name and password.</span></span>
   
   ![İş kimlik bilgileri][creds]
   
   <span data-ttu-id="89cdf-323">Bazı koşullarda HPC Pack önce giriş ve bu iletişim kutusunu göstermez kullanıcı bilgilerini hatırlıyor.</span><span class="sxs-lookup"><span data-stu-id="89cdf-323">Under some conditions, HPC Pack remembers the user information you input before and doesn’t show this dialog box.</span></span> <span data-ttu-id="89cdf-324">HPC Pack yeniden Göster yapmak için bir komut isteminde aşağıdaki komutu girin ve sonra işi göndermek.</span><span class="sxs-lookup"><span data-stu-id="89cdf-324">To make HPC Pack show it again, enter the following command at a Command prompt and then submit the job.</span></span>
   
   ```
   hpccred delcreds
   ```
9. <span data-ttu-id="89cdf-325">İş dakika onlarca örnek için ayarladığınız parametrelere göre birkaç saat sürer.</span><span class="sxs-lookup"><span data-stu-id="89cdf-325">The job takes from tens of minutes to several hours according to the parameters you have set for the sample.</span></span> <span data-ttu-id="89cdf-326">Isı Haritası Linux düğümleri üzerinde iş bakın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-326">In the heat map, you see the job running on the Linux nodes.</span></span> 
   
   ![Isı Haritası][heat_map]
   
   <span data-ttu-id="89cdf-328">Her düğümde sekiz işlemleri başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="89cdf-328">On each node, eight processes are started.</span></span>
   
   ![Linux işlemleri][linux_processes]
10. <span data-ttu-id="89cdf-330">İş tamamlandığında iş sonuçlarını C:\OpenFoam\sloshingTank3D ve günlük dosyalarını C:\OpenFoam altındaki klasörleri bulun.</span><span class="sxs-lookup"><span data-stu-id="89cdf-330">When the job finishes, find the job results in folders under C:\OpenFoam\sloshingTank3D, and the log files at C:\OpenFoam.</span></span>

## <a name="view-results-in-ensight"></a><span data-ttu-id="89cdf-331">EnSight görünümü sonuçları</span><span class="sxs-lookup"><span data-stu-id="89cdf-331">View results in EnSight</span></span>
<span data-ttu-id="89cdf-332">İsteğe bağlı olarak kullanmak [EnSight](https://www.ceisoftware.com/) görselleştirmek ve OpenFOAM iş sonuçlarını analiz etmek için.</span><span class="sxs-lookup"><span data-stu-id="89cdf-332">Optionally use [EnSight](https://www.ceisoftware.com/) to visualize and analyze the results of the OpenFOAM job.</span></span> <span data-ttu-id="89cdf-333">Bu Görselleştirme ve EnSight animasyonda hakkında daha fazla bilgi için bkz [video Kılavuzu](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span><span class="sxs-lookup"><span data-stu-id="89cdf-333">For more about visualization and animation in EnSight, see this [video guide](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span></span>

1. <span data-ttu-id="89cdf-334">Baş düğümünde EnSight yükledikten sonra başlatın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-334">After you install EnSight on the head node, start it.</span></span>
2. <span data-ttu-id="89cdf-335">C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case açın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-335">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span></span>
   
   <span data-ttu-id="89cdf-336">Tank Görüntüleyicisi'ndeki bakın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-336">You see a tank in the viewer.</span></span>
   
   ![EnSight tank][tank]
3. <span data-ttu-id="89cdf-338">Oluşturma bir **Isosurface** gelen **internalMesh**ve ardından değişkeni **alpha_water**.</span><span class="sxs-lookup"><span data-stu-id="89cdf-338">Create an **Isosurface** from **internalMesh**, and then choose the variable **alpha_water**.</span></span>
   
   ![Bir isosurface oluşturma][isosurface]
4. <span data-ttu-id="89cdf-340">Rengini ayarlama **Isosurface_part** önceki adımda oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="89cdf-340">Set the color for **Isosurface_part** created in the previous step.</span></span> <span data-ttu-id="89cdf-341">Örneğin, su için mavi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-341">For example, set it to water blue.</span></span>
   
   ![İsosurface renk Düzenle][isosurface_color]
5. <span data-ttu-id="89cdf-343">Oluşturma bir **ISO hacimli** gelen **duvarları** seçerek **duvarları** içinde **bölümleri** panel ve'ı tıklatın **Isosurfaces** araç çubuğu düğmesini.</span><span class="sxs-lookup"><span data-stu-id="89cdf-343">Create an **Iso-volume** from **walls** by selecting **walls** in the **Parts** panel and click the **Isosurfaces** button in the toolbar.</span></span>
6. <span data-ttu-id="89cdf-344">İletişim kutusunda **türü** olarak **Isovolume** ve en küçük **Isovolume aralığı** 0,5.</span><span class="sxs-lookup"><span data-stu-id="89cdf-344">In the dialog box, select **Type** as **Isovolume** and set the Min of **Isovolume range** to 0.5.</span></span> <span data-ttu-id="89cdf-345">İsovolume oluşturmak için tıklatın **Create seçilen parçaları ile**.</span><span class="sxs-lookup"><span data-stu-id="89cdf-345">To create the isovolume, click **Create with selected parts**.</span></span>
7. <span data-ttu-id="89cdf-346">Rengini ayarlama **Iso_volume_part** önceki adımda oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="89cdf-346">Set the color for **Iso_volume_part** created in the previous step.</span></span> <span data-ttu-id="89cdf-347">Örneğin, derin su mavi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-347">For example, set it to deep water blue.</span></span>
8. <span data-ttu-id="89cdf-348">Rengini ayarlama **duvarları**.</span><span class="sxs-lookup"><span data-stu-id="89cdf-348">Set the color for **walls**.</span></span> <span data-ttu-id="89cdf-349">Örneğin, saydam beyaza ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="89cdf-349">For example, set it to transparent white.</span></span>
9. <span data-ttu-id="89cdf-350">Şimdi **Yürüt** benzetimi sonuçlarını görmek için.</span><span class="sxs-lookup"><span data-stu-id="89cdf-350">Now click **Play** to see the results of the simulation.</span></span>
   
    ![Tank sonucu][tank_result]

## <a name="sample-files"></a><span data-ttu-id="89cdf-352">Örnek dosyaları</span><span class="sxs-lookup"><span data-stu-id="89cdf-352">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="89cdf-353">PowerShell komut dosyası tarafından küme dağıtımı için örnek XML yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="89cdf-353">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

### <a name="sample-credxml-file"></a><span data-ttu-id="89cdf-354">Örnek cred.xml dosyası</span><span class="sxs-lookup"><span data-stu-id="89cdf-354">Sample cred.xml file</span></span>
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```
### <a name="sample-silentcfg-file-to-install-mpi"></a><span data-ttu-id="89cdf-355">Örnek silent.cfg dosyası MPI yüklemek için</span><span class="sxs-lookup"><span data-stu-id="89cdf-355">Sample silent.cfg file to install MPI</span></span>
```
# Patterns used to check silent configuration file
#
# anythingpat - any string
# filepat     - the file location pattern (/file/location/to/license.lic)
# lspat       - the license server address pattern (0123@hostname)
# snpat       - the serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components to install, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path to the cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes to enable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes to update ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a><span data-ttu-id="89cdf-356">Örnek settings.sh komut dosyası</span><span class="sxs-lookup"><span data-stu-id="89cdf-356">Sample settings.sh script</span></span>
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a><span data-ttu-id="89cdf-357">Örnek hpcimpirun.sh komut dosyası</span><span class="sxs-lookup"><span data-stu-id="89cdf-357">Sample hpcimpirun.sh script</span></span>
```
#!/bin/bash

# The path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run the mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create the hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into the hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run the mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png
