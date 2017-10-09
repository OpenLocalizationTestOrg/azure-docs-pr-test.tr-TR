---
title: "aaaRun OpenFOAM Linux VM'ler üzerinde HPC Pack ile | Microsoft Docs"
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
ms.openlocfilehash: 1a51ffe6804abb5156f01d580c9b7a4a9649377a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="87127-103">Azure’daki bir Linux RDMA kümesinde Microsoft HPC Pack ile OpenFoam çalıştırma</span><span class="sxs-lookup"><span data-stu-id="87127-103">Run OpenFoam with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="87127-104">Bu makalede, Azure sanal makinelerinde tek yönlü toorun OpenFoam gösterir.</span><span class="sxs-lookup"><span data-stu-id="87127-104">This article shows you one way toorun OpenFoam in Azure virtual machines.</span></span> <span data-ttu-id="87127-105">Bir Microsoft HPC Pack kümesinde Linux işlem düğümleri ile Azure ve Çalıştır burada dağıttığınız bir [OpenFoam](http://openfoam.com/) Intel MPI işlemiyle.</span><span class="sxs-lookup"><span data-stu-id="87127-105">Here, you deploy a Microsoft HPC Pack cluster with Linux compute nodes on Azure and run an [OpenFoam](http://openfoam.com/) job with Intel MPI.</span></span> <span data-ttu-id="87127-106">Böylece Hello işlem düğümleri hello Azure RDMA ağ üzerinden iletişim RDMA özellikli Azure VM'ler, hello işlem düğümleri için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87127-106">You can use RDMA-capable Azure VMs for hello compute nodes, so that hello compute nodes communicate over hello Azure RDMA network.</span></span> <span data-ttu-id="87127-107">Ticari görüntüleri hello UberCloud'ın gibi Market kullanılabilir diğer seçenekleri toorun azure'da OpenFoam dahil tam olarak yapılandırılmış [OpenFoam 2.3 CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/)ve çalıştırarak [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span><span class="sxs-lookup"><span data-stu-id="87127-107">Other options toorun OpenFoam in Azure include fully configured commercial images available in hello Marketplace, such as UberCloud's [OpenFoam 2.3 on CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), and by running on [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="87127-108">(İçin alan işlemi açın ve düzenleme) OpenFOAM mühendislik ve Bilim hem ticari hem de akademik kuruluşlarda yaygın olarak kullanılan bir açık kaynak hesaplama sıvı dinamiği (CFD) yazılım paketidir.</span><span class="sxs-lookup"><span data-stu-id="87127-108">OpenFOAM (for Open Field Operation and Manipulation) is an open-source computational fluid dynamics (CFD) software package that is used widely in engineering and science, in both commercial and academic organizations.</span></span> <span data-ttu-id="87127-109">Meshing, özellikle snappyHexMesh, bir parallelized mesher karmaşık CAD geometri ve öncesi ve sonrası işleme için Araçlar içerir.</span><span class="sxs-lookup"><span data-stu-id="87127-109">It includes tools for meshing, notably snappyHexMesh, a parallelized mesher for complex CAD geometries, and for pre- and post-processing.</span></span> <span data-ttu-id="87127-110">Neredeyse tüm işlemleri kullanıcılar tootake tam anlamıyla kendi elden bilgisayar donanımı etkinleştirme paralel olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="87127-110">Almost all processes run in parallel, enabling users tootake full advantage of computer hardware at their disposal.</span></span>  

<span data-ttu-id="87127-111">Microsoft HPC Pack sağlayan özellikler toorun büyük ölçekli HPC ve Microsoft Azure sanal makinelerin kümelerde MPI uygulamaları da dahil olmak üzere paralel uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="87127-111">Microsoft HPC Pack provides features toorun large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="87127-112">HPC Pack de uygulamaların Linux işlem düğümü VM'ler bir HPC Pack kümede dağıtılmış çalışan Linux HPC destekler.</span><span class="sxs-lookup"><span data-stu-id="87127-112">HPC Pack also supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="87127-113">Bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md) için bir giriş toousing Linux işlem düğümlerini HPC paketi ile.</span><span class="sxs-lookup"><span data-stu-id="87127-113">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction toousing Linux compute nodes with HPC Pack.</span></span>

> [!NOTE]
> <span data-ttu-id="87127-114">Bu makalede gösterilmektedir nasıl toorun Linux MPI iş yükü HPC paketi ile.</span><span class="sxs-lookup"><span data-stu-id="87127-114">This article illustrates how toorun a Linux MPI workload with HPC Pack.</span></span> <span data-ttu-id="87127-115">Bu, Linux sistem yönetimi ile Linux kümelerinde MPI iş yükleri çalıştıran bazı benzer olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="87127-115">It assumes you have some familiarity with Linux system administration and with running MPI workloads on Linux clusters.</span></span> <span data-ttu-id="87127-116">MPI ve OpenFOAM hello bu makalede gösterilen olanları farklı sürümlerini kullanıyorsanız, bazı yükleme ve yapılandırma adımlarının toomodify olabilir.</span><span class="sxs-lookup"><span data-stu-id="87127-116">If you use versions of MPI and OpenFOAM different from hello ones shown in this article, you might have toomodify some installation and configuration steps.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="87127-117">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="87127-117">Prerequisites</span></span>
* <span data-ttu-id="87127-118">**HPC Pack küme RDMA özellikli Linux işlem düğümlerini** - HPC paketi küme boyutu A8, A9, H16r, dağıtmak veya H16rm Linux işlem düğümlerini kullanarak bir [Azure Resource Manager şablonu](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) veya bir [Azure PowerShell Betiği](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="87127-118">**HPC Pack cluster with RDMA-capable Linux compute nodes** - Deploy an HPC Pack cluster with size A8, A9, H16r, or H16rm Linux compute nodes using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="87127-119">Bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md) hello Önkoşullar ve adımlar her iki seçenek için.</span><span class="sxs-lookup"><span data-stu-id="87127-119">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for hello prerequisites and steps for either option.</span></span> <span data-ttu-id="87127-120">Merhaba PowerShell komut dosyası dağıtım seçeneği seçerseniz, bu makalenin hello sonunda hello örnek dosyalarında hello örnek yapılandırma dosyasına bakın.</span><span class="sxs-lookup"><span data-stu-id="87127-120">If you choose hello PowerShell script deployment option, see hello sample configuration file in hello sample files at hello end of this article.</span></span> <span data-ttu-id="87127-121">2 boyutu A8 SUSE Linux Enterprise Server 12 işlem düğümlerini ve boyutu A8 Windows Server 2012 R2 baş düğümü oluşan bu yapılandırma toodeploy Azure tabanlı HPC paketi küme kullanın.</span><span class="sxs-lookup"><span data-stu-id="87127-121">Use this configuration toodeploy an Azure-based HPC Pack cluster consisting of a size A8 Windows Server 2012 R2 head node and 2 size A8 SUSE Linux Enterprise Server 12 compute nodes.</span></span> <span data-ttu-id="87127-122">Aboneliği ve hizmet adları için uygun değerleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="87127-122">Substitute appropriate values for your subscription and service names.</span></span> 
  
  <span data-ttu-id="87127-123">**Ek işlemler tooknow**</span><span class="sxs-lookup"><span data-stu-id="87127-123">**Additional things tooknow**</span></span>
  
  * <span data-ttu-id="87127-124">Linux RDMA ağ ön koşulu için Azure bkz [yüksek performanslı işlem VM boyutları](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="87127-124">For Linux RDMA networking prerequisites in Azure, see [High performance compute VM sizes](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  * <span data-ttu-id="87127-125">Merhaba Powershell komut dosyası dağıtım seçeneğini kullanırsanız, bir bulut hizmeti toouse hello RDMA ağ bağlantısı içindeki tüm hello Linux işlem düğümlerini dağıtın.</span><span class="sxs-lookup"><span data-stu-id="87127-125">If you use hello Powershell script deployment option, deploy all hello Linux compute nodes within one cloud service toouse hello RDMA network connection.</span></span>
  * <span data-ttu-id="87127-126">Merhaba Linux düğümleri dağıttıktan sonra ek yönetim görevleri tarafından SSH tooperform bağlayın.</span><span class="sxs-lookup"><span data-stu-id="87127-126">After deploying hello Linux nodes, connect by SSH tooperform any additional administrative tasks.</span></span> <span data-ttu-id="87127-127">Merhaba SSH bağlantı ayrıntıları için her bir Linux VM hello Azure portalı bulun.</span><span class="sxs-lookup"><span data-stu-id="87127-127">Find hello SSH connection details for each Linux VM in hello Azure portal.</span></span>  
* <span data-ttu-id="87127-128">**Intel MPI** -toorun OpenFOAM SLES 12 HPC üzerinde işlem düğümlerini Azure, tooinstall hello Intel MPI kitaplığı 5 çalışma zamanı hello gelen gerek [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span><span class="sxs-lookup"><span data-stu-id="87127-128">**Intel MPI** - toorun OpenFOAM on SLES 12 HPC compute nodes in Azure, you need tooinstall hello Intel MPI Library 5 runtime from hello [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span></span> <span data-ttu-id="87127-129">(Intel MPI 5 CentOS tabanlı HPC görüntülerinde önceden yüklenir.)  Bir sonraki adımda gerekiyorsa, Linux işlem düğümlerinde Intel MPI yükleyin.</span><span class="sxs-lookup"><span data-stu-id="87127-129">(Intel MPI 5 is preinstalled on CentOS-based HPC images.)  In a later step, if necessary, install Intel MPI on your Linux compute nodes.</span></span> <span data-ttu-id="87127-130">Bu adım için tooprepare Intel ile kaydettikten sonra hello onay e-posta toohello ilgili web sayfası hello bağlantıyı izleyin.</span><span class="sxs-lookup"><span data-stu-id="87127-130">tooprepare for this step, after you register with Intel, follow hello link in hello confirmation email toohello related web page.</span></span> <span data-ttu-id="87127-131">Ardından, kopyalama hello hello .tgz dosyası Intel MPI hello uygun sürümü için bağlantısını indirin.</span><span class="sxs-lookup"><span data-stu-id="87127-131">Then, copy hello download link for hello .tgz file for hello appropriate version of Intel MPI.</span></span> <span data-ttu-id="87127-132">Bu makalede, Intel MPI sürüm 5.0.3.048 temel alır.</span><span class="sxs-lookup"><span data-stu-id="87127-132">This article is based on Intel MPI version 5.0.3.048.</span></span>
* <span data-ttu-id="87127-133">**OpenFOAM kaynak paketi** -indirme hello OpenFOAM kaynak paketi yazılım Linux için hello [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span><span class="sxs-lookup"><span data-stu-id="87127-133">**OpenFOAM Source Pack** - Download hello OpenFOAM Source Pack software for Linux from hello [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span></span> <span data-ttu-id="87127-134">Bu makalede kaynak paketi sürümü 2.3.1, indirme için kullanılabilir OpenFOAM 2.3.1.tgz temel alır.</span><span class="sxs-lookup"><span data-stu-id="87127-134">This article is based on Source Pack version 2.3.1, available for download as OpenFOAM-2.3.1.tgz.</span></span> <span data-ttu-id="87127-135">Daha sonra bu makalede toounpack Hello yönergeleri izleyin ve OpenFOAM hello Linux işlem düğümlerinde derleyin.</span><span class="sxs-lookup"><span data-stu-id="87127-135">Follow hello instructions later in this article toounpack and compile OpenFOAM on hello Linux compute nodes.</span></span>
* <span data-ttu-id="87127-136">**EnSight** (isteğe bağlı) - toosee hello OpenFOAM benzetim, sonuçlarını yükleyip hello [EnSight](https://www.ceisoftware.com/download/) Görselleştirme ve analiz program.</span><span class="sxs-lookup"><span data-stu-id="87127-136">**EnSight** (optional) - toosee hello results of your OpenFOAM simulation, download and install hello [EnSight](https://www.ceisoftware.com/download/) visualization and analysis program.</span></span> <span data-ttu-id="87127-137">Merhaba EnSight sitede lisans ve yükleme bilgileri var.</span><span class="sxs-lookup"><span data-stu-id="87127-137">Licensing and download information are at hello EnSight site.</span></span>

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="87127-138">İşlem düğümleri arasında karşılıklı güven ayarlama</span><span class="sxs-lookup"><span data-stu-id="87127-138">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="87127-139">Bir geçici düğüm işi birden çok Linux düğümler üzerinde çalışan gerektirir hello düğümleri tootrust birbirine (tarafından **rsh** veya **ssh**).</span><span class="sxs-lookup"><span data-stu-id="87127-139">Running a cross-node job on multiple Linux nodes requires hello nodes tootrust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="87127-140">Microsoft HPC Pack Iaas dağıtım betiği hello ile Merhaba HPC Pack kümesi oluşturduğunuzda, hello betik kalıcı karşılıklı güven belirttiğiniz hello yönetici hesabı için otomatik olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="87127-140">When you create hello HPC Pack cluster with hello Microsoft HPC Pack IaaS deployment script, hello script automatically sets up permanent mutual trust for hello administrator account you specify.</span></span> <span data-ttu-id="87127-141">Bir iş toothem ayrılır ve hello işi tamamlandıktan sonra hello ilişki destroy hello kümenin etki alanında oluşturduğunuz yönetici olmayan kullanıcılar için tooset hello düğümler arasında geçici karşılıklı güveni vardır.</span><span class="sxs-lookup"><span data-stu-id="87127-141">For non-administrator users you create in hello cluster's domain, you have tooset up temporary mutual trust among hello nodes when a job is allocated toothem, and destroy hello relationship after hello job is complete.</span></span> <span data-ttu-id="87127-142">Her kullanıcı için tooestablish güven HPC Pack Merhaba güven ilişkisi kullanan bir RSA anahtar çifti toohello kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="87127-142">tooestablish trust for each user, provide an RSA key pair toohello cluster that HPC Pack uses for hello trust relationship.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="87127-143">RSA anahtar çifti oluşturma</span><span class="sxs-lookup"><span data-stu-id="87127-143">Generate an RSA key pair</span></span>
<span data-ttu-id="87127-144">Kolay toogenerate bir ortak anahtar ve özel anahtarı içeren bir RSA anahtar çifti, Linux hello çalıştırarak **ssh-keygen** komutu.</span><span class="sxs-lookup"><span data-stu-id="87127-144">It's easy toogenerate an RSA key pair, which contains a public key and a private key, by running hello Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="87127-145">Üzerinde tooa Linux bilgisayarda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="87127-145">Log on tooa Linux computer.</span></span>
2. <span data-ttu-id="87127-146">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="87127-146">Run hello following command:</span></span>
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="87127-147">Tuşuna **Enter** hello komut tamamlanıncaya kadar toouse hello varsayılan ayarlar.</span><span class="sxs-lookup"><span data-stu-id="87127-147">Press **Enter** toouse hello default settings until hello command is completed.</span></span> <span data-ttu-id="87127-148">Burada bir parola girmeyin; için bir parola istendiğinde, yalnızca basın **Enter**.</span><span class="sxs-lookup"><span data-stu-id="87127-148">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![RSA anahtar çifti oluşturma][keygen]
3. <span data-ttu-id="87127-150">Dizin toohello ~/.ssh dizini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="87127-150">Change directory toohello ~/.ssh directory.</span></span> <span data-ttu-id="87127-151">Merhaba özel anahtarı id_rsa.pub id_rsa ve hello ortak anahtarında depolanır.</span><span class="sxs-lookup"><span data-stu-id="87127-151">hello private key is stored in id_rsa and hello public key in id_rsa.pub.</span></span>
   
   ![Özel ve genel anahtarlar][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a><span data-ttu-id="87127-153">Merhaba anahtar çifti toohello HPC paketi küme ekleme</span><span class="sxs-lookup"><span data-stu-id="87127-153">Add hello key pair toohello HPC Pack cluster</span></span>
1. <span data-ttu-id="87127-154">Bir Uzak Masaüstü Bağlantısı tooyour baş düğüm HPC Pack Yönetici hesabınızla (Merhaba dağıtım betiğini çalıştırdığınızda ayarladığınız hello yönetici hesabı) olun.</span><span class="sxs-lookup"><span data-stu-id="87127-154">Make a Remote Desktop connection tooyour head node with your HPC Pack administrator account (hello administrator account you set up when you ran hello deployment script).</span></span>
2. <span data-ttu-id="87127-155">Standart Windows Server yordamları toocreate bir etki alanı kullanıcı hesabı hello kümenin Active Directory etki alanında kullanın.</span><span class="sxs-lookup"><span data-stu-id="87127-155">Use standard Windows Server procedures toocreate a domain user account in hello cluster's Active Directory domain.</span></span> <span data-ttu-id="87127-156">Örneğin, hello baş düğümünde hello Active Directory Kullanıcıları ve Bilgisayarları aracını kullanın.</span><span class="sxs-lookup"><span data-stu-id="87127-156">For example, use hello Active Directory User and Computers tool on hello head node.</span></span> <span data-ttu-id="87127-157">Bu makaledeki örneklerde Hello hpclab\hpcuser adlı bir etki alanı kullanıcısı oluşturun varsayalım.</span><span class="sxs-lookup"><span data-stu-id="87127-157">hello examples in this article assume you create a domain user named hpclab\hpcuser.</span></span>
3. <span data-ttu-id="87127-158">C:\cred.XML ve kopyalama hello RSA anahtar verilerini içine adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="87127-158">Create a file named C:\cred.xml and copy hello RSA key data into it.</span></span> <span data-ttu-id="87127-159">Bir örnek cred.xml hello bu makalenin sonundaki dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="87127-159">A sample cred.xml file is at hello end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. <span data-ttu-id="87127-160">Bir komut istemi açın ve tooset hello veri hello hpclab\hpcuser hesabı için kimlik bilgileri komutu aşağıdaki hello girin.</span><span class="sxs-lookup"><span data-stu-id="87127-160">Open a Command Prompt and enter hello following command tooset hello credentials data for hello hpclab\hpcuser account.</span></span> <span data-ttu-id="87127-161">Merhaba kullandığınız **extendeddata** parametresi toopass hello hello anahtar verileri için oluşturduğunuz C:\cred.xml dosyasının adı.</span><span class="sxs-lookup"><span data-stu-id="87127-161">You use hello **extendeddata** parameter toopass hello name of C:\cred.xml file you created for hello key data.</span></span>
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="87127-162">Bu komut çıktısı başarıyla tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="87127-162">This command completes successfully without output.</span></span> <span data-ttu-id="87127-163">Toorun işleri ihtiyacınız hello kullanıcı hesapları için hello kimlik bilgilerini ayarlama sonra hello cred.xml dosyayı güvenli bir konumda depolayın veya silin.</span><span class="sxs-lookup"><span data-stu-id="87127-163">After setting hello credentials for hello user accounts you need toorun jobs, store hello cred.xml file in a secure location, or delete it.</span></span>
5. <span data-ttu-id="87127-164">Linux düğümlerinden biri üzerinde hello RSA anahtar çifti oluşturursa, bunları kullanmayı bitirdikten sonra toodelete hello anahtarları unutmayın.</span><span class="sxs-lookup"><span data-stu-id="87127-164">If you generated hello RSA key pair on one of your Linux nodes, remember toodelete hello keys after you finish using them.</span></span> <span data-ttu-id="87127-165">HPC Pack varolan id_rsa dosyaya veya id_rsa.pub dosyası bulursa, karşılıklı güven ayarlı değil.</span><span class="sxs-lookup"><span data-stu-id="87127-165">If HPC Pack finds an existing id_rsa file or id_rsa.pub file, it does not set up mutual trust.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="87127-166">Bir yönetici tarafından gönderilen bir işin hello kök hesapta hello Linux düğümleri üzerinde çalıştığı için Linux iş paylaşılan bir kümede bir Küme Yöneticisi olarak çalışan öneririz yok.</span><span class="sxs-lookup"><span data-stu-id="87127-166">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under hello root account on hello Linux nodes.</span></span> <span data-ttu-id="87127-167">Ancak, yönetici olmayan bir kullanıcı tarafından gönderilen bir işi hello aynı hello işi kullanıcı adı ile bir yerel Linux kullanıcı hesabı altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="87127-167">However, a job submitted by a non-administrator user runs under a local Linux user account with hello same name as hello job user.</span></span> <span data-ttu-id="87127-168">Bu durumda, HPC Pack bu Linux kullanıcı için karşılıklı güven toohello iş ayrılan hello düğümlere ayarlar.</span><span class="sxs-lookup"><span data-stu-id="87127-168">In this case, HPC Pack sets up mutual trust for this Linux user across hello nodes allocated toohello job.</span></span> <span data-ttu-id="87127-169">Merhaba Linux kullanıcı hello Linux düğümlerde el ile Merhaba işi çalıştırmadan önce ayarlayabilirsiniz veya hello iş gönderildiğinde HPC Pack Merhaba kullanıcı otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="87127-169">You can set up hello Linux user manually on hello Linux nodes before running hello job, or HPC Pack creates hello user automatically when hello job is submitted.</span></span> <span data-ttu-id="87127-170">HPC Pack Merhaba kullanıcı oluşturursa, HPC Pack Merhaba işi tamamlandıktan sonra onu siler.</span><span class="sxs-lookup"><span data-stu-id="87127-170">If HPC Pack creates hello user, HPC Pack deletes it after hello job completes.</span></span> <span data-ttu-id="87127-171">tooreduce güvenlik tehditlerine karşı HPC Pack Merhaba anahtarları işi tamamlandıktan sonra kaldırır.</span><span class="sxs-lookup"><span data-stu-id="87127-171">tooreduce security threats, HPC Pack removes hello keys after job completion.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="87127-172">Linux düğümleri için bir dosya paylaşımı ayarlama</span><span class="sxs-lookup"><span data-stu-id="87127-172">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="87127-173">Şimdi hello baş düğüm üzerinde bir klasör standart bir SMB paylaşımında ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="87127-173">Now set up a standard SMB share on a folder on hello head node.</span></span> <span data-ttu-id="87127-174">tooallow hello Linux düğümleri tooaccess uygulama dosyalarını ortak bir yol ile bağlama hello paylaşılan klasörün hello Linux düğümlerde'ü tıklatın.</span><span class="sxs-lookup"><span data-stu-id="87127-174">tooallow hello Linux nodes tooaccess application files with a common path, mount hello shared folder on hello Linux nodes.</span></span> <span data-ttu-id="87127-175">İsterseniz, başka bir dosya paylaşımı gibi birçok senaryo - ya da bir NFS paylaşımına için önerilen bir Azure dosya paylaşımı - seçeneği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87127-175">If you want, you can use another file sharing option, such as an Azure Files share - recommended for many scenarios - or an NFS share.</span></span> <span data-ttu-id="87127-176">Merhaba dosya bilgileri ve ayrıntılı adımlar paylaşımı bkz [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="87127-176">See hello file sharing information and detailed steps in [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="87127-177">Merhaba baş düğüm üzerinde bir klasör oluşturun ve okuma/yazma ayrıcalıklarına ayarlayarak tooEveryone paylaşın.</span><span class="sxs-lookup"><span data-stu-id="87127-177">Create a folder on hello head node, and share it tooEveryone by setting Read/Write privileges.</span></span> <span data-ttu-id="87127-178">Örneğin, hello baş düğümü olarak C:\OpenFOAM paylaşım \\ \\SUSE12RDMA HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="87127-178">For example, share C:\OpenFOAM on hello head node as \\\\SUSE12RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="87127-179">Burada, *SUSE12RDMA HN* hello baş düğümü hello ana bilgisayar adıdır.</span><span class="sxs-lookup"><span data-stu-id="87127-179">Here, *SUSE12RDMA-HN* is hello host name of hello head node.</span></span>
2. <span data-ttu-id="87127-180">Bir Windows PowerShell penceresi açın ve hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="87127-180">Open a Windows PowerShell window and run hello following commands:</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

<span data-ttu-id="87127-181">Merhaba ilk komut hello LinuxNodes grubundaki tüm düğümlerde /openfoam adlı bir klasör oluşturur.</span><span class="sxs-lookup"><span data-stu-id="87127-181">hello first command creates a folder named /openfoam on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="87127-182">Merhaba ikinci komut hello paylaşılan klasör //SUSE12RDMA-HN/OpenFOAM dir_mode ve file_mode BITS kümesi too777 ile Merhaba Linux düğümlerde bağlar.</span><span class="sxs-lookup"><span data-stu-id="87127-182">hello second command mounts hello shared folder //SUSE12RDMA-HN/OpenFOAM on hello Linux nodes with dir_mode and file_mode bits set too777.</span></span> <span data-ttu-id="87127-183">Merhaba *kullanıcıadı* ve *parola* hello komutu hello baş düğüm üzerinde bir kullanıcının kimlik bilgilerini hello olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="87127-183">hello *username* and *password* in hello command should be hello credentials of a user on hello head node.</span></span>

> [!NOTE]
> <span data-ttu-id="87127-184">Merhaba "\\`" Merhaba ikinci komut dosyasındaki simge olan PowerShell bir kaçış simgesi.</span><span class="sxs-lookup"><span data-stu-id="87127-184">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="87127-185">"\\`,"anlamına gelir hello"," (virgül karakteri) hello komutu bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="87127-185">“\\`,” means hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

## <a name="install-mpi-and-openfoam"></a><span data-ttu-id="87127-186">MPI ve OpenFOAM yükleyin</span><span class="sxs-lookup"><span data-stu-id="87127-186">Install MPI and OpenFOAM</span></span>
<span data-ttu-id="87127-187">toorun OpenFOAM MPI işi hello RDMA ağ üzerinde toocompile OpenFOAM hello Intel MPI kitaplıklarla gerekir.</span><span class="sxs-lookup"><span data-stu-id="87127-187">toorun OpenFOAM as an MPI job on hello RDMA network, you need toocompile OpenFOAM with hello Intel MPI libraries.</span></span> 

<span data-ttu-id="87127-188">Öncelikle birkaç çalıştırın **clusrun** Linux düğümlerinde (henüz yüklenmemişse) tooinstall Intel MPI kitaplıkları ve OpenFOAM komutları.</span><span class="sxs-lookup"><span data-stu-id="87127-188">First, run several **clusrun** commands tooinstall Intel MPI libraries (if not already installed) and OpenFOAM on your Linux nodes.</span></span> <span data-ttu-id="87127-189">Kullanım hello baş düğüm paylaşımı tooshare hello yükleme dosyalarını hello Linux düğümleri arasında daha önce yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="87127-189">Use hello head node share configured previously tooshare hello installation files among hello Linux nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="87127-190">Bu yükleme ve derleniyor adımları verilebilir.</span><span class="sxs-lookup"><span data-stu-id="87127-190">These installation and compiling steps are examples.</span></span> <span data-ttu-id="87127-191">Bazı Linux sistem yönetim tooensure bağımlı derleyicileri ve kitaplıklarını düzgün yüklendiğini bilgisine gerekir.</span><span class="sxs-lookup"><span data-stu-id="87127-191">You need some knowledge of Linux system administration tooensure that dependent compilers and libraries are installed correctly.</span></span> <span data-ttu-id="87127-192">Intel MPI ve OpenFOAM sürümü için belirli ortam değişkenleri veya diğer ayarları toomodify gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="87127-192">You might need toomodify certain environment variables or other settings for your versions of Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="87127-193">Ayrıntılar için bkz [Linux Yükleme Kılavuzu için Intel MPI Kitaplığı](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) ve [OpenFOAM kaynak paketi yüklemesi](http://openfoam.org/download/2-3-1-source/) ortamınız için.</span><span class="sxs-lookup"><span data-stu-id="87127-193">For details, see [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) and [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) for your environment.</span></span>
> 
> 

### <a name="install-intel-mpi"></a><span data-ttu-id="87127-194">Intel MPI yükleyin</span><span class="sxs-lookup"><span data-stu-id="87127-194">Install Intel MPI</span></span>
<span data-ttu-id="87127-195">Bu dosya /openfoam Hello Linux düğümleri erişebilmesi hello karşıdan yükleme paketi C:\OpenFoam içinde Intel MPI (Bu örnekte l_mpi_p_5.0.3.048.tgz) için hello baş düğümünde kaydedin.</span><span class="sxs-lookup"><span data-stu-id="87127-195">Save hello downloaded installation package for Intel MPI (l_mpi_p_5.0.3.048.tgz in this example) in C:\OpenFoam on hello head node so that hello Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="87127-196">Ardından çalıştırın **clusrun** tüm hello Linux düğümlerde tooinstall Intel MPI kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="87127-196">Then run **clusrun** tooinstall Intel MPI library on all hello Linux nodes.</span></span>

1. <span data-ttu-id="87127-197">Merhaba aşağıdaki komutları kopyasını hello yükleme paketini ve çok/opt/her bir düğümde Intel ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="87127-197">hello following commands copy hello installation package and extract it too/opt/intel on each node.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. <span data-ttu-id="87127-198">tooinstall Intel MPI kitaplığı sessizce silent.cfg dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="87127-198">tooinstall Intel MPI Library silently, use a silent.cfg file.</span></span> <span data-ttu-id="87127-199">Bu makalenin hello sonunda örnek dosyalarını hello bir örnek bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87127-199">You can find an example in hello sample files at hello end of this article.</span></span> <span data-ttu-id="87127-200">Merhaba bu dosyada yer klasörü /openfoam paylaşılan.</span><span class="sxs-lookup"><span data-stu-id="87127-200">Place this file in hello shared folder /openfoam.</span></span> <span data-ttu-id="87127-201">Merhaba silent.cfg dosyası hakkında daha fazla ayrıntı için bkz: [Linux Yükleme Kılavuzu - sessiz yükleme için Intel MPI Kitaplığı](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span><span class="sxs-lookup"><span data-stu-id="87127-201">For details about hello silent.cfg file, see [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="87127-202">Silent.cfg dosyanız Linux sahip bir metin dosyası olarak kaydettiğinizde satır sonlarını (yalnızca LF, CR LF) emin olun.</span><span class="sxs-lookup"><span data-stu-id="87127-202">Make sure that you save your silent.cfg file as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="87127-203">Bu adım, düzgün şekilde hello Linux düğümlerinde çalıştığını sağlar.</span><span class="sxs-lookup"><span data-stu-id="87127-203">This step ensures that it runs properly on hello Linux nodes.</span></span>
   > 
   > 
3. <span data-ttu-id="87127-204">Intel MPI kitaplığı sessiz modda yükleyin.</span><span class="sxs-lookup"><span data-stu-id="87127-204">Install Intel MPI Library in silent mode.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a><span data-ttu-id="87127-205">MPI yapılandırın</span><span class="sxs-lookup"><span data-stu-id="87127-205">Configure MPI</span></span>
<span data-ttu-id="87127-206">Test etmek için her hello Linux düğümleri satırları toohello /etc/security/limits.conf aşağıdaki hello eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="87127-206">For testing, you should add hello following lines toohello /etc/security/limits.conf on each of hello Linux nodes:</span></span>

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


<span data-ttu-id="87127-207">Merhaba limits.conf dosya güncelleştirdikten sonra hello Linux düğümleri yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="87127-207">Restart hello Linux nodes after you update hello limits.conf file.</span></span> <span data-ttu-id="87127-208">Örneğin, hello aşağıdaki kullanın **clusrun** komutu:</span><span class="sxs-lookup"><span data-stu-id="87127-208">For example, use hello following **clusrun** command:</span></span>

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

<span data-ttu-id="87127-209">Yeniden başlattıktan sonra hello paylaşılan klasörü /openfoam bağlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="87127-209">After restarting, ensure that hello shared folder is mounted as /openfoam.</span></span>

### <a name="compile-and-install-openfoam"></a><span data-ttu-id="87127-210">Derleme ve OpenFOAM yükleyin</span><span class="sxs-lookup"><span data-stu-id="87127-210">Compile and install OpenFOAM</span></span>
<span data-ttu-id="87127-211">Bu dosya /openfoam Hello Linux düğümleri erişebilmesi hello karşıdan yükleme paketi hello OpenFOAM kaynak paketi (Bu örnekte, OpenFOAM-2.3.1.tgz) tooC:\OpenFoam için hello baş düğümünde kaydedin.</span><span class="sxs-lookup"><span data-stu-id="87127-211">Save hello downloaded installation package for hello OpenFOAM Source Pack (OpenFOAM-2.3.1.tgz in this example) tooC:\OpenFoam on hello head node so that hello Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="87127-212">Ardından çalıştırın **clusrun** toocompile OpenFOAM tüm hello Linux düğümleri komutları.</span><span class="sxs-lookup"><span data-stu-id="87127-212">Then run **clusrun** commands toocompile OpenFOAM on all hello Linux nodes.</span></span>

1. <span data-ttu-id="87127-213">Bir klasör /opt/OpenFOAM her Linux düğümde kopyalama hello paket toothis, kaynak klasörü oluşturun ve orada ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="87127-213">Create a folder /opt/OpenFOAM on each Linux node, copy hello source package toothis folder, and extract it there.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. <span data-ttu-id="87127-214">ilk Intel MPI ve OpenFOAM için bazı ortam değişkenlerini ayarlamak hello Intel MPI kitaplığı ile toocompile OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="87127-214">toocompile OpenFOAM with hello Intel MPI Library, first set up some environment variables for both Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="87127-215">Settings.sh tooset hello değişkenleri olarak adlandırılan bir bash komut dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="87127-215">Use a bash script called settings.sh tooset hello variables.</span></span> <span data-ttu-id="87127-216">Bu makalenin hello sonunda örnek dosyalarını hello bir örnek bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87127-216">You can find an example in hello sample files at hello end of this article.</span></span> <span data-ttu-id="87127-217">Yerleştir (Linux satır sonları ile kaydedilmiş) bu dosyada hello klasörü /openfoam paylaşılan.</span><span class="sxs-lookup"><span data-stu-id="87127-217">Place this file (saved with Linux line endings) in hello shared folder /openfoam.</span></span> <span data-ttu-id="87127-218">Bu dosya ayrıca hello MPI ve OpenFOAM çalışma zamanları sonraki toorun OpenFOAM iş kullanmak için ayarları içerir.</span><span class="sxs-lookup"><span data-stu-id="87127-218">This file also contains settings for hello MPI and OpenFOAM runtimes that you use later toorun an OpenFOAM job.</span></span>
3. <span data-ttu-id="87127-219">Gerekli bağımlı paketler toocompile OpenFOAM yükleyin.</span><span class="sxs-lookup"><span data-stu-id="87127-219">Install dependent packages needed toocompile OpenFOAM.</span></span> <span data-ttu-id="87127-220">Linux dağıtımınız bağlı olarak, ilk tooadd depo gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="87127-220">Depending on your Linux distribution, you might first need tooadd a repository.</span></span> <span data-ttu-id="87127-221">Çalıştırma **clusrun** benzer toohello aşağıdaki komutlar:</span><span class="sxs-lookup"><span data-stu-id="87127-221">Run **clusrun** commands similar toohello following:</span></span>
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    <span data-ttu-id="87127-222">Gerekirse, SSH tooeach Linux düğümü toorun hello düzgün çalışması tooconfirm komutları.</span><span class="sxs-lookup"><span data-stu-id="87127-222">If necessary, SSH tooeach Linux node toorun hello commands tooconfirm that they run properly.</span></span>
4. <span data-ttu-id="87127-223">Çalışma hello aşağıdaki toocompile OpenFOAM komutu.</span><span class="sxs-lookup"><span data-stu-id="87127-223">Run hello following command toocompile OpenFOAM.</span></span> <span data-ttu-id="87127-224">Merhaba derleme işlemi biraz zaman toocomplete alır ve büyük miktarda günlük bilgileri toostandard çıkışını oluşturur, bu nedenle hello kullanın **/ araya eklemeli** seçeneği, araya eklemeli toodisplay hello çıktı.</span><span class="sxs-lookup"><span data-stu-id="87127-224">hello compilation process takes some time toocomplete and generates a large amount of log information toostandard output, so use hello **/interleaved** option toodisplay hello output interleaved.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > <span data-ttu-id="87127-225">Merhaba "\\`" hello komut dosyasındaki simge olan PowerShell bir kaçış simgesi.</span><span class="sxs-lookup"><span data-stu-id="87127-225">hello “\\`” symbol in hello command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="87127-226">"\\`&" anlamına gelir Merhaba "&" Merhaba komutu, bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="87127-226">“\\`&” means hello “&” is a part of hello command.</span></span>
   > 
   > 

## <a name="prepare-toorun-an-openfoam-job"></a><span data-ttu-id="87127-227">Toorun OpenFOAM iş hazırlama</span><span class="sxs-lookup"><span data-stu-id="87127-227">Prepare toorun an OpenFOAM job</span></span>
<span data-ttu-id="87127-228">Şimdi get hazır toorun MPI iş hello OpenFoam örnekleri olan sloshingTank3D iki Linux düğümlerinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="87127-228">Now get ready toorun an MPI job called sloshingTank3D, which is one of hello OpenFoam samples, on two Linux nodes.</span></span> 

### <a name="set-up-hello-runtime-environment"></a><span data-ttu-id="87127-229">Merhaba çalışma zamanı ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="87127-229">Set up hello runtime environment</span></span>
<span data-ttu-id="87127-230">tooset düğümlerde hello baş düğümünde komutu bir Windows PowerShell penceresinde aşağıdaki hello çalıştırmak hello Linux hello çalışma zamanı ortamları MPI ve OpenFOAM için ayarlama.</span><span class="sxs-lookup"><span data-stu-id="87127-230">tooset up hello runtime environments for MPI and OpenFOAM on hello Linux nodes, run hello following command in a Windows PowerShell window on hello head node.</span></span> <span data-ttu-id="87127-231">(Bu komut, yalnızca SUSE Linux için geçerlidir.)</span><span class="sxs-lookup"><span data-stu-id="87127-231">(This command is valid for SUSE Linux only.)</span></span>

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a><span data-ttu-id="87127-232">Örnek verileri hazırlama</span><span class="sxs-lookup"><span data-stu-id="87127-232">Prepare sample data</span></span>
<span data-ttu-id="87127-233">Kullanım hello baş düğüm Paylaşımı (/openfoam takılı) hello Linux düğümleri arasında tooshare dosyaları daha önce yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="87127-233">Use hello head node share you configured previously tooshare files among hello Linux nodes (mounted as /openfoam).</span></span>

1. <span data-ttu-id="87127-234">SSH tooone, Linux işlem düğümlerini.</span><span class="sxs-lookup"><span data-stu-id="87127-234">SSH tooone of your Linux compute nodes.</span></span>
2. <span data-ttu-id="87127-235">Bunu zaten yapmadıysanız komutu tooset hello OpenFOAM çalışma zamanı ortamı kurma aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="87127-235">Run hello following command tooset up hello OpenFOAM runtime environment, if you haven’t already done this.</span></span>
   
   ```
   $ source /openfoam/settings.sh
   ```
3. <span data-ttu-id="87127-236">Merhaba sloshingTank3D örnek toohello paylaşılan klasöre kopyalayın ve tooit gidin.</span><span class="sxs-lookup"><span data-stu-id="87127-236">Copy hello sloshingTank3D sample toohello shared folder and navigate tooit.</span></span>
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. <span data-ttu-id="87127-237">Bu örnek hello varsayılan parametrelerini kullandığınızda, toomodify isteyebilirsiniz şekilde bunu dakika toorun onlarca çalıştırmak daha hızlı bazı parametreler toomake alabilir.</span><span class="sxs-lookup"><span data-stu-id="87127-237">When you use hello default parameters of this sample, it can take tens of minutes toorun, so you might want toomodify some parameters toomake it run faster.</span></span> <span data-ttu-id="87127-238">Bir basit toomodify hello zaman adım değişkenleri deltaT ve writeInterval hello sistem/controlDict dosyasındaki bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="87127-238">One simple choice is toomodify hello time step variables deltaT and writeInterval in hello system/controlDict file.</span></span> <span data-ttu-id="87127-239">Bu dosya toohello denetim saati ve okuma ve çözüm veri yazma ile ilgili tüm giriş verilerini depolar.</span><span class="sxs-lookup"><span data-stu-id="87127-239">This file stores all input data relating toohello control of time and reading and writing solution data.</span></span> <span data-ttu-id="87127-240">Örneğin, 0,05 too0.5 gelen deltaT hello değerini ve 0,05 too0.5 gelen writeInterval hello değerini değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="87127-240">For example, you could change hello value of deltaT from 0.05 too0.5 and hello value of writeInterval from 0.05 too0.5.</span></span>
   
   ![Adım değişkenleri değiştirin][step_variables]
5. <span data-ttu-id="87127-242">Merhaba sistem/decomposeParDict dosyasında hello değişkenleri için istenen değerleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="87127-242">Specify desired values for hello variables in hello system/decomposeParDict file.</span></span> <span data-ttu-id="87127-243">Bu örnek iki kullanır Linux düğümleri her 8 çekirdek sahip olacak şekilde ayarlamanız numberOfSubdomains too16 ve hierarchicalCoeffs n too(1 1 16), 16 süreçleri ile paralel OpenFOAM anlamına çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="87127-243">This example uses two Linux nodes each with 8 cores, so set numberOfSubdomains too16 and n of hierarchicalCoeffs too(1 1 16), which means run OpenFOAM in parallel with 16 processes.</span></span> <span data-ttu-id="87127-244">Daha fazla bilgi için bkz: [OpenFOAM Kullanıcı Kılavuzu: paralel 3.4 çalışan uygulamaları](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span><span class="sxs-lookup"><span data-stu-id="87127-244">For more information, see [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span></span>
   
   ![İşlemler parçalayın][decompose]
6. <span data-ttu-id="87127-246">Merhaba sloshingTank3D directory tooprepare hello örnek verilerden komutları aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="87127-246">Run hello following commands from hello sloshingTank3D directory tooprepare hello sample data.</span></span>
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. <span data-ttu-id="87127-247">Merhaba baş düğümünde hello örnek veri dosyalarını C:\OpenFoam\sloshingTank3D kopyalanır görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="87127-247">On hello head node, you should see hello sample data files are copied into C:\OpenFoam\sloshingTank3D.</span></span> <span data-ttu-id="87127-248">(C:\OpenFoam hello paylaşılan hello baş düğümünde klasörüdür.)</span><span class="sxs-lookup"><span data-stu-id="87127-248">(C:\OpenFoam is hello shared folder on hello head node.)</span></span>
   
   ![Merhaba baş düğüm üzerinde veri dosyaları][data_files]

### <a name="host-file-for-mpirun"></a><span data-ttu-id="87127-250">Ana bilgisayar dosyası mpirun için</span><span class="sxs-lookup"><span data-stu-id="87127-250">Host file for mpirun</span></span>
<span data-ttu-id="87127-251">Bu adımda, bir ana bilgisayar dosyası (işlem düğümleri listesi) hangi hello oluşturduğunuz **mpirun** komutunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="87127-251">In this step, you create a host file (a list of compute nodes) which hello **mpirun** command uses.</span></span>

1. <span data-ttu-id="87127-252">Merhaba Linux düğümleri her birinde bu dosyayı /openfoam/hostfile tüm Linux düğümlerde üzerinde erişilebilir şekilde /openfoam altında hostfile adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="87127-252">On one of hello Linux nodes, create a file named hostfile under /openfoam, so this file can be reached at /openfoam/hostfile on all Linux nodes.</span></span>
2. <span data-ttu-id="87127-253">Linux düğüm adları bu dosyaya yazma.</span><span class="sxs-lookup"><span data-stu-id="87127-253">Write your Linux node names into this file.</span></span> <span data-ttu-id="87127-254">Bu örnekte, adları aşağıdaki hello hello dosya içerir:</span><span class="sxs-lookup"><span data-stu-id="87127-254">In this example, hello file contains hello following names:</span></span>
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > <span data-ttu-id="87127-255">Bu dosya C:\OpenFoam\hostfile hello baş düğümünde de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87127-255">You can also create this file at C:\OpenFoam\hostfile on hello head node.</span></span> <span data-ttu-id="87127-256">Bu seçeneği seçerseniz, Linux bir metin dosyası olarak kaydedin (yalnızca LF, CR LF) satır sonlarını.</span><span class="sxs-lookup"><span data-stu-id="87127-256">If you choose this option, save it as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="87127-257">Bu, düzgün şekilde hello Linux düğümlerinde çalıştığını sağlar.</span><span class="sxs-lookup"><span data-stu-id="87127-257">This ensures that it runs properly on hello Linux nodes.</span></span>
   > 
   > 
   
   <span data-ttu-id="87127-258">**Bash betik sarmalayıcı**</span><span class="sxs-lookup"><span data-stu-id="87127-258">**Bash script wrapper**</span></span>
   
   <span data-ttu-id="87127-259">Hangi düğümlerin tooyour iş ayrılır tanımadığınız birçok Linux düğümleri varsa ve bazı yalnızca, iş toorun istediğiniz sabit bir ana bilgisayar dosya, iyi bir fikir toouse değildir, çünkü.</span><span class="sxs-lookup"><span data-stu-id="87127-259">If you have many Linux nodes and you want your job toorun on only some of them, it’s not a good idea toouse a fixed host file, because you don’t know which nodes will be allocated tooyour job.</span></span> <span data-ttu-id="87127-260">Bu durumda, bir bash betik sarmalayıcı için yazma **mpirun** toocreate hello ana bilgisayar dosyası otomatik olarak.</span><span class="sxs-lookup"><span data-stu-id="87127-260">In this case, write a bash script wrapper for **mpirun** toocreate hello host file automatically.</span></span> <span data-ttu-id="87127-261">Bu makalenin hello sonunda hpcimpirun.sh olarak adlandırılan bir örnek bash betik sarmalayıcı bulmak ve /openfoam/hpcimpirun.sh kaydedin. Bu örnek komut aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="87127-261">You can find an example bash script wrapper called hpcimpirun.sh at hello end of this article, and save it as /openfoam/hpcimpirun.sh. This example script does hello following:</span></span>
   
   1. <span data-ttu-id="87127-262">Merhaba ortam değişkenleri için ayarlar **mpirun**ve bazı ek komut parametreleri toorun hello MPI iş hello RDMA ağ üzerinden.</span><span class="sxs-lookup"><span data-stu-id="87127-262">Sets up hello environment variables for **mpirun**, and some addition command parameters toorun hello MPI job through hello RDMA network.</span></span> <span data-ttu-id="87127-263">Bu durumda, değişkenleri aşağıdaki hello ayarlar:</span><span class="sxs-lookup"><span data-stu-id="87127-263">In this case, it sets hello following variables:</span></span>
      
      * <span data-ttu-id="87127-264">I_MPI_FABRICS shm:dapl =</span><span class="sxs-lookup"><span data-stu-id="87127-264">I_MPI_FABRICS=shm:dapl</span></span>
      * <span data-ttu-id="87127-265">I_MPI_DAPL_PROVIDER bir v2 ib0 =</span><span class="sxs-lookup"><span data-stu-id="87127-265">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span></span>
      * <span data-ttu-id="87127-266">I_MPI_DYNAMIC_CONNECTION = 0</span><span class="sxs-lookup"><span data-stu-id="87127-266">I_MPI_DYNAMIC_CONNECTION=0</span></span>
   2. <span data-ttu-id="87127-267">Toohello ortam değişkeni $ göre bir ana bilgisayar dosyası oluşturur hello iş etkinleştirildiğinde, hello HPC baş düğümü tarafından ayarlanan CCP_NODES_CORES.</span><span class="sxs-lookup"><span data-stu-id="87127-267">Creates a host file according toohello environment variable $CCP_NODES_CORES, which is set by hello HPC head node when hello job is activated.</span></span>
      
      <span data-ttu-id="87127-268">Merhaba $CCP_NODES_CORES biçimlerinin bu deseni izler:</span><span class="sxs-lookup"><span data-stu-id="87127-268">hello format of $CCP_NODES_CORES follows this pattern:</span></span>
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      <span data-ttu-id="87127-269">Burada</span><span class="sxs-lookup"><span data-stu-id="87127-269">where</span></span>
      
      * <span data-ttu-id="87127-270">`<Number of nodes>`-hello düğüm sayısını ayrılan toothis işi.</span><span class="sxs-lookup"><span data-stu-id="87127-270">`<Number of nodes>` - hello number of nodes allocated toothis job.</span></span>  
      * <span data-ttu-id="87127-271">`<Name of node_n_...>`-her düğümün hello adı ayrılmış toothis işi.</span><span class="sxs-lookup"><span data-stu-id="87127-271">`<Name of node_n_...>` - hello name of each node allocated toothis job.</span></span>
      * <span data-ttu-id="87127-272">`<Cores of node_n_...>`-hello hello düğüm ayrılmış toothis işinde çekirdek sayısı.</span><span class="sxs-lookup"><span data-stu-id="87127-272">`<Cores of node_n_...>` - hello number of cores on hello node allocated toothis job.</span></span>
      
      <span data-ttu-id="87127-273">Örneğin, Hello iş iki düğüm toorun gerekirse, $CCP_NODES_CORES benzer.</span><span class="sxs-lookup"><span data-stu-id="87127-273">For example, if hello job needs two nodes toorun, $CCP_NODES_CORES is similar to</span></span>
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. <span data-ttu-id="87127-274">Çağrıları hello **mpirun** komut ve iki parametreleri toohello komut satırı ekler.</span><span class="sxs-lookup"><span data-stu-id="87127-274">Calls hello **mpirun** command and appends two parameters toohello command line.</span></span>
      
      * <span data-ttu-id="87127-275">`--hostfile <hostfilepath>: <hostfilepath>`-hello ana bilgisayar dosyası hello betiği hello yolunu oluşturur</span><span class="sxs-lookup"><span data-stu-id="87127-275">`--hostfile <hostfilepath>: <hostfilepath>` - hello path of hello host file hello script creates</span></span>
      * <span data-ttu-id="87127-276">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`-Toplam çekirdek sayısı hello depolayan hello HPC paketi üstbilgi düğümü tarafından ayarlanmış bir ortam değişkeni toothis iş ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="87127-276">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - an environment variable set by hello HPC Pack head node, which stores hello number of total cores allocated toothis job.</span></span> <span data-ttu-id="87127-277">Bu durumda, işlemler için hello sayısını belirtir **mpirun**.</span><span class="sxs-lookup"><span data-stu-id="87127-277">In this case, it specifies hello number of processes for **mpirun**.</span></span>

## <a name="submit-an-openfoam-job"></a><span data-ttu-id="87127-278">Bir OpenFOAM işi gönderin</span><span class="sxs-lookup"><span data-stu-id="87127-278">Submit an OpenFOAM job</span></span>
<span data-ttu-id="87127-279">Şimdi bir işi HPC Küme Yöneticisi'nde gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87127-279">Now you can submit a job in HPC Cluster Manager.</span></span> <span data-ttu-id="87127-280">Bazı hello iş görevleri için toopass hello betik hpcimpirun.sh hello komut satırlarında gerekir.</span><span class="sxs-lookup"><span data-stu-id="87127-280">You need toopass hello script hpcimpirun.sh in hello command lines for some of hello job tasks.</span></span>

1. <span data-ttu-id="87127-281">Tooyour küme baş düğümüne bağlanmak ve HPC Küme Yöneticisi'ni başlatın.</span><span class="sxs-lookup"><span data-stu-id="87127-281">Connect tooyour cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="87127-282">**Kaynak Yönetimi'nde**, hello Linux işlem düğümlerini hello olduğundan emin olun **çevrimiçi** durumu.</span><span class="sxs-lookup"><span data-stu-id="87127-282">**In Resource Management**, ensure that hello Linux compute nodes are in hello **Online** state.</span></span> <span data-ttu-id="87127-283">Değilse, bunları seçin ve tıklatın **çevrimiçine**.</span><span class="sxs-lookup"><span data-stu-id="87127-283">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="87127-284">İçinde **iş yönetimi**, tıklatın **yeni iş**.</span><span class="sxs-lookup"><span data-stu-id="87127-284">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="87127-285">İş için bir ad girin *sloshingTank3D*.</span><span class="sxs-lookup"><span data-stu-id="87127-285">Enter a name for job such as *sloshingTank3D*.</span></span>
   
   ![İş ayrıntıları][job_details]
5. <span data-ttu-id="87127-287">İçinde **iş kaynakları**, kaynak olarak "Düğümü" Merhaba türünü seçin ve hello Minimum too2 ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="87127-287">In **Job resources**, choose hello type of resource as “Node” and set hello Minimum too2.</span></span> <span data-ttu-id="87127-288">Bu yapılandırma, bu örnekte, her biri sekiz çekirdeği olması iki Linux düğümlerde hello işi çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="87127-288">This configuration runs hello job on two Linux nodes, each of which has eight cores in this example.</span></span>
   
   ![İş kaynakları][job_resources]
6. <span data-ttu-id="87127-290">Tıklatın **Düzenle görevleri** hello sol gezinti bölmesinde ve ardından **Ekle** tooadd görev toohello işi.</span><span class="sxs-lookup"><span data-stu-id="87127-290">Click **Edit Tasks** in hello left navigation, and then click **Add** tooadd a task toohello job.</span></span> <span data-ttu-id="87127-291">Merhaba dört görevleri toohello işlemiyle Ekle komut satırları ve ayarlar aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="87127-291">Add four tasks toohello job with hello following command lines and settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="87127-292">Çalışan `source /openfoam/settings.sh` her görevleri aşağıdaki hello OpenFOAM komutu hello önce çağırır hello OpenFOAM ve MPI çalışma zamanı ortamları, ayarlar.</span><span class="sxs-lookup"><span data-stu-id="87127-292">Running `source /openfoam/settings.sh` sets up hello OpenFOAM and MPI runtime environments, so each of hello following tasks calls it before hello OpenFOAM command.</span></span>
   > 
   > 
   
   * <span data-ttu-id="87127-293">**Görev 1**.</span><span class="sxs-lookup"><span data-stu-id="87127-293">**Task 1**.</span></span> <span data-ttu-id="87127-294">Çalıştırma **decomposePar** toogenerate veri dosyalarını çalıştırmak için **interDyMFoam** paralel.</span><span class="sxs-lookup"><span data-stu-id="87127-294">Run **decomposePar** toogenerate data files for running **interDyMFoam** in parallel.</span></span>
     
     * <span data-ttu-id="87127-295">Bir düğüm toohello görev atama</span><span class="sxs-lookup"><span data-stu-id="87127-295">Assign one node toohello task</span></span>
     * <span data-ttu-id="87127-296">**Komut satırı** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="87127-296">**Command line** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="87127-297">**Çalışma dizini** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="87127-297">**Working directory** - /openfoam/sloshingTank3D</span></span>
     
     <span data-ttu-id="87127-298">Aşağıdaki şekilde hello bakın.</span><span class="sxs-lookup"><span data-stu-id="87127-298">See hello following figure.</span></span> <span data-ttu-id="87127-299">Merhaba kalan görevlere benzer şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="87127-299">You configure hello remaining tasks similarly.</span></span>
     
     ![Görev 1 ayrıntıları][task_details1]
   * <span data-ttu-id="87127-301">**Görev 2**.</span><span class="sxs-lookup"><span data-stu-id="87127-301">**Task 2**.</span></span> <span data-ttu-id="87127-302">Çalıştırma **interDyMFoam** paralel toocompute hello örnek.</span><span class="sxs-lookup"><span data-stu-id="87127-302">Run **interDyMFoam** in parallel toocompute hello sample.</span></span>
     
     * <span data-ttu-id="87127-303">İki düğüm toohello görev atama</span><span class="sxs-lookup"><span data-stu-id="87127-303">Assign two nodes toohello task</span></span>
     * <span data-ttu-id="87127-304">**Komut satırı** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="87127-304">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="87127-305">**Çalışma dizini** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="87127-305">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="87127-306">**Görev 3**.</span><span class="sxs-lookup"><span data-stu-id="87127-306">**Task 3**.</span></span> <span data-ttu-id="87127-307">Çalıştırma **reconstructPar** toomerge hello her processor_N_ dizininden zaman dizinleri tek kümesi olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="87127-307">Run **reconstructPar** toomerge hello sets of time directories from each processor_N_ directory into a single set.</span></span>
     
     * <span data-ttu-id="87127-308">Bir düğüm toohello görev atama</span><span class="sxs-lookup"><span data-stu-id="87127-308">Assign one node toohello task</span></span>
     * <span data-ttu-id="87127-309">**Komut satırı** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="87127-309">**Command line** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="87127-310">**Çalışma dizini** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="87127-310">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="87127-311">**Görev 4**.</span><span class="sxs-lookup"><span data-stu-id="87127-311">**Task 4**.</span></span> <span data-ttu-id="87127-312">Çalıştırma **foamToEnsight** paralel tooconvert EnSight hello OpenFOAM sonuç dosyalarıyla biçimlendirmek ve hello servis talebi dizinde Ensight adlı bir dizin hello EnSight dosyaları yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="87127-312">Run **foamToEnsight** in parallel tooconvert hello OpenFOAM result files into EnSight format and place hello EnSight files in a directory named Ensight in hello case directory.</span></span>
     
     * <span data-ttu-id="87127-313">İki düğüm toohello görev atama</span><span class="sxs-lookup"><span data-stu-id="87127-313">Assign two nodes toohello task</span></span>
     * <span data-ttu-id="87127-314">**Komut satırı** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="87127-314">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="87127-315">**Çalışma dizini** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="87127-315">**Working directory** - /openfoam/sloshingTank3D</span></span>
7. <span data-ttu-id="87127-316">Bağımlılıklar toothese görevler, görev sırası artan düzende ekleyin.</span><span class="sxs-lookup"><span data-stu-id="87127-316">Add dependencies toothese tasks in ascending task order.</span></span>
   
   ![Görev bağımlılıkları][task_dependencies]
8. <span data-ttu-id="87127-318">Tıklatın **gönderme** toorun bu işi.</span><span class="sxs-lookup"><span data-stu-id="87127-318">Click **Submit** toorun this job.</span></span>
   
   <span data-ttu-id="87127-319">Varsayılan olarak, HPC Pack Merhaba iş geçerli oturum açmış kullanıcı hesabınız olarak gönderir.</span><span class="sxs-lookup"><span data-stu-id="87127-319">By default, HPC Pack submits hello job as your current logged-on user account.</span></span> <span data-ttu-id="87127-320">Tıklattıktan sonra **gönderme**, tooenter hello kullanıcı adı ve parola isteyen bir iletişim kutusu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87127-320">After you click **Submit**, you might see a dialog box prompting you tooenter hello user name and password.</span></span>
   
   ![İş kimlik bilgileri][creds]
   
   <span data-ttu-id="87127-322">Bazı koşullarda HPC Pack önce giriş ve bu iletişim kutusunu göstermez hello kullanıcı bilgilerini hatırlıyor.</span><span class="sxs-lookup"><span data-stu-id="87127-322">Under some conditions, HPC Pack remembers hello user information you input before and doesn’t show this dialog box.</span></span> <span data-ttu-id="87127-323">toomake HPC paketi yeniden göstermek, komutu bir komut isteminde aşağıdaki hello girin ve hello işi göndermek.</span><span class="sxs-lookup"><span data-stu-id="87127-323">toomake HPC Pack show it again, enter hello following command at a Command prompt and then submit hello job.</span></span>
   
   ```
   hpccred delcreds
   ```
9. <span data-ttu-id="87127-324">Merhaba iş hello örnek için ayarladığınız toohello parametreleri göre dakika tooseveral saat onlarca arasında geçen süredir.</span><span class="sxs-lookup"><span data-stu-id="87127-324">hello job takes from tens of minutes tooseveral hours according toohello parameters you have set for hello sample.</span></span> <span data-ttu-id="87127-325">Merhaba ısı Haritası hello Linux düğümleri üzerinde çalışan hello işi bakın.</span><span class="sxs-lookup"><span data-stu-id="87127-325">In hello heat map, you see hello job running on hello Linux nodes.</span></span> 
   
   ![Isı Haritası][heat_map]
   
   <span data-ttu-id="87127-327">Her düğümde sekiz işlemleri başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="87127-327">On each node, eight processes are started.</span></span>
   
   ![Linux işlemleri][linux_processes]
10. <span data-ttu-id="87127-329">Merhaba işi tamamlandığında hello iş sonuçları C:\OpenFoam\sloshingTank3D ve C:\OpenFoam hello günlüğü dosyalarını altındaki klasörleri bulun.</span><span class="sxs-lookup"><span data-stu-id="87127-329">When hello job finishes, find hello job results in folders under C:\OpenFoam\sloshingTank3D, and hello log files at C:\OpenFoam.</span></span>

## <a name="view-results-in-ensight"></a><span data-ttu-id="87127-330">EnSight görünümü sonuçları</span><span class="sxs-lookup"><span data-stu-id="87127-330">View results in EnSight</span></span>
<span data-ttu-id="87127-331">İsteğe bağlı olarak kullanmak [EnSight](https://www.ceisoftware.com/) toovisualize ve hello OpenFOAM iş hello sonuçlarını çözümleyin.</span><span class="sxs-lookup"><span data-stu-id="87127-331">Optionally use [EnSight](https://www.ceisoftware.com/) toovisualize and analyze hello results of hello OpenFOAM job.</span></span> <span data-ttu-id="87127-332">Bu Görselleştirme ve EnSight animasyonda hakkında daha fazla bilgi için bkz [video Kılavuzu](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span><span class="sxs-lookup"><span data-stu-id="87127-332">For more about visualization and animation in EnSight, see this [video guide](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span></span>

1. <span data-ttu-id="87127-333">Merhaba baş düğümünde EnSight yükledikten sonra başlatın.</span><span class="sxs-lookup"><span data-stu-id="87127-333">After you install EnSight on hello head node, start it.</span></span>
2. <span data-ttu-id="87127-334">C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case açın.</span><span class="sxs-lookup"><span data-stu-id="87127-334">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span></span>
   
   <span data-ttu-id="87127-335">Merhaba Görüntüleyicisi'nde tank bakın.</span><span class="sxs-lookup"><span data-stu-id="87127-335">You see a tank in hello viewer.</span></span>
   
   ![EnSight tank][tank]
3. <span data-ttu-id="87127-337">Oluşturma bir **Isosurface** gelen **internalMesh**ve ardından hello değişkeni **alpha_water**.</span><span class="sxs-lookup"><span data-stu-id="87127-337">Create an **Isosurface** from **internalMesh**, and then choose hello variable **alpha_water**.</span></span>
   
   ![Bir isosurface oluşturma][isosurface]
4. <span data-ttu-id="87127-339">Merhaba rengini ayarlama **Isosurface_part** hello önceki adımda oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="87127-339">Set hello color for **Isosurface_part** created in hello previous step.</span></span> <span data-ttu-id="87127-340">Örneğin, toowater mavi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="87127-340">For example, set it toowater blue.</span></span>
   
   ![İsosurface renk Düzenle][isosurface_color]
5. <span data-ttu-id="87127-342">Oluşturma bir **ISO hacimli** gelen **duvarları** seçerek **duvarları** hello içinde **bölümleri** panel ve Başlangıç'ı tıklatın **Isosurfaces**  hello araç çubuğu düğmesi.</span><span class="sxs-lookup"><span data-stu-id="87127-342">Create an **Iso-volume** from **walls** by selecting **walls** in hello **Parts** panel and click hello **Isosurfaces** button in hello toolbar.</span></span>
6. <span data-ttu-id="87127-343">Merhaba iletişim kutusunda seçin **türü** olarak **Isovolume** ve minimum hello **Isovolume aralığı** too0.5.</span><span class="sxs-lookup"><span data-stu-id="87127-343">In hello dialog box, select **Type** as **Isovolume** and set hello Min of **Isovolume range** too0.5.</span></span> <span data-ttu-id="87127-344">toocreate isovolume Merhaba, tıklatın **Create seçilen parçaları ile**.</span><span class="sxs-lookup"><span data-stu-id="87127-344">toocreate hello isovolume, click **Create with selected parts**.</span></span>
7. <span data-ttu-id="87127-345">Merhaba rengini ayarlama **Iso_volume_part** hello önceki adımda oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="87127-345">Set hello color for **Iso_volume_part** created in hello previous step.</span></span> <span data-ttu-id="87127-346">Örneğin, toodeep su mavi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="87127-346">For example, set it toodeep water blue.</span></span>
8. <span data-ttu-id="87127-347">Merhaba rengini ayarlama **duvarları**.</span><span class="sxs-lookup"><span data-stu-id="87127-347">Set hello color for **walls**.</span></span> <span data-ttu-id="87127-348">Örneğin, tootransparent beyaz ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="87127-348">For example, set it tootransparent white.</span></span>
9. <span data-ttu-id="87127-349">Şimdi **yürütmek** hello benzetimi toosee hello sonuçları.</span><span class="sxs-lookup"><span data-stu-id="87127-349">Now click **Play** toosee hello results of hello simulation.</span></span>
   
    ![Tank sonucu][tank_result]

## <a name="sample-files"></a><span data-ttu-id="87127-351">Örnek dosyaları</span><span class="sxs-lookup"><span data-stu-id="87127-351">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="87127-352">PowerShell komut dosyası tarafından küme dağıtımı için örnek XML yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="87127-352">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
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

### <a name="sample-credxml-file"></a><span data-ttu-id="87127-353">Örnek cred.xml dosyası</span><span class="sxs-lookup"><span data-stu-id="87127-353">Sample cred.xml file</span></span>
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
### <a name="sample-silentcfg-file-tooinstall-mpi"></a><span data-ttu-id="87127-354">Örnek silent.cfg dosya tooinstall MPI</span><span class="sxs-lookup"><span data-stu-id="87127-354">Sample silent.cfg file tooinstall MPI</span></span>
```
# Patterns used toocheck silent configuration file
#
# anythingpat - any string
# filepat     - hello file location pattern (/file/location/to/license.lic)
# lspat       - hello license server address pattern (0123@hostname)
# snpat       - hello serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components tooinstall, valid values are: {ALL, DEFAULTS, anythingpat}
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

# Path toohello cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes tooenable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes tooupdate ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a><span data-ttu-id="87127-355">Örnek settings.sh komut dosyası</span><span class="sxs-lookup"><span data-stu-id="87127-355">Sample settings.sh script</span></span>
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


### <a name="sample-hpcimpirunsh-script"></a><span data-ttu-id="87127-356">Örnek hpcimpirun.sh komut dosyası</span><span class="sxs-lookup"><span data-stu-id="87127-356">Sample hpcimpirun.sh script</span></span>
```
#!/bin/bash

# hello path of this script
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
    # CCP_NODES_CORES is not found or is empty, just run hello mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into hello hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello mpirun with hostfile arg
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
