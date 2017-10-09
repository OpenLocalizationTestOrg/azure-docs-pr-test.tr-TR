---
title: "Linux sanal makineleri üzerinde Microsoft HPC paketi ile aaaNAMD | Microsoft Docs"
description: "Azure Microsoft HPC Pack kümede dağıtmak ve NAMD benzetimi charmrun ile birden çok Linux işlem düğümlerinde çalışacak."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 76072c6b-ac35-4729-ba67-0d16f9443bd7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/13/2016
ms.author: danlep
ms.openlocfilehash: 90c722f66b494335a62c0613079366ae99002076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a><span data-ttu-id="9952b-103">Azure’daki Linux işlem düğümlerinde Microsoft HPC Pack ile NAMD çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9952b-103">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>
<span data-ttu-id="9952b-104">Bu makalede tek yönlü toorun Linux yüksek performanslı bilgi işlem (HPC) iş yükü Azure sanal makinelerde gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9952b-104">This article shows you one way toorun a Linux high-performance computing (HPC) workload on Azure virtual machines.</span></span> <span data-ttu-id="9952b-105">Burada ayarladığınız bir [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) Azure üzerinde Linux işlem düğümü ile küme ve Çalıştır bir [NAMD](http://www.ks.uiuc.edu/Research/namd/) benzetimi toocalculate ve büyük biomolecular sistem hello yapısını görselleştirin.</span><span class="sxs-lookup"><span data-stu-id="9952b-105">Here, you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster on Azure with Linux compute nodes and run a [NAMD](http://www.ks.uiuc.edu/Research/namd/) simulation toocalculate and visualize hello structure of a large biomolecular system.</span></span>  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* <span data-ttu-id="9952b-106">**NAMD** (Nanoscale Molecular Dynamics programı) olan büyük biomolecular sistemleri yüksek performanslı benzetimi için tasarlanmış bir paralel molecular dynamics paketini içeren Atom toomillions.</span><span class="sxs-lookup"><span data-stu-id="9952b-106">**NAMD** (for Nanoscale Molecular Dynamics program) is a parallel molecular dynamics package designed for high-performance simulation of large biomolecular systems containing up toomillions of atoms.</span></span> <span data-ttu-id="9952b-107">Bu sistemlere örnek olarak, virüsler, hücre yapıları ve büyük proteins içerir.</span><span class="sxs-lookup"><span data-stu-id="9952b-107">Examples of these systems include viruses, cell structures, and large proteins.</span></span> <span data-ttu-id="9952b-108">NAMD toohundreds tipik benzetimleri ve hello en büyük benzetimleri 500.000 çekirdeği daha toomore için çekirdek ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="9952b-108">NAMD scales toohundreds of cores for typical simulations and toomore than 500,000 cores for hello largest simulations.</span></span>
* <span data-ttu-id="9952b-109">**Microsoft HPC Pack** özellikleri toorun sağlar büyük ölçekli HPC ve şirket içi bilgisayarları veya Azure sanal makineleri kümelerinde paralel uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="9952b-109">**Microsoft HPC Pack** provides features toorun large-scale HPC and parallel applications in clusters of on-premises computers or Azure virtual machines.</span></span> <span data-ttu-id="9952b-110">İlk olarak Windows HPC iş yükleri, HPC paketi için bir çözüm olarak geliştirilen şimdi Linux HPC uygulamaları Linux üzerinde çalışan destekleyen bir HPC Pack kümede dağıtılan düğümü VM'ler işlem.</span><span class="sxs-lookup"><span data-stu-id="9952b-110">Originally developed as a solution for Windows HPC workloads, HPC Pack now supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="9952b-111">Bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md) giriş.</span><span class="sxs-lookup"><span data-stu-id="9952b-111">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction.</span></span>

<span data-ttu-id="9952b-112">Diğer Seçenekler toorun Linux HPC için azure'da iş yüklerini bkz [toplu işlem ve yüksek performanslı bilgi işlem için teknik kaynaklar](../../../batch/batch-hpc-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="9952b-112">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/batch-hpc-solutions.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9952b-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9952b-113">Prerequisites</span></span>
* <span data-ttu-id="9952b-114">**HPC Pack küme Linux işlem düğümlerini** -ya da kullanarak Azure Linux işlem düğümlerini içeren bir HPC Pack kümeyi dağıtma bir [Azure Resource Manager şablonu](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) veya bir [Azure PowerShell Betiği](hpcpack-cluster-powershell-script.md) .</span><span class="sxs-lookup"><span data-stu-id="9952b-114">**HPC Pack cluster with Linux compute nodes** - Deploy an HPC Pack cluster with Linux compute nodes on Azure using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="9952b-115">Bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md) hello Önkoşullar ve adımlar her iki seçenek için.</span><span class="sxs-lookup"><span data-stu-id="9952b-115">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for hello prerequisites and steps for either option.</span></span> <span data-ttu-id="9952b-116">Merhaba PowerShell komut dosyası dağıtım seçeneği seçerseniz, bu makalenin hello sonunda hello örnek dosyalarında hello örnek yapılandırma dosyasına bakın.</span><span class="sxs-lookup"><span data-stu-id="9952b-116">If you choose hello PowerShell script deployment option, see hello sample configuration file in hello sample files at hello end of this article.</span></span> <span data-ttu-id="9952b-117">Bu dosya bir Windows Server 2012 R2 baş düğüm ve dört boyutu büyük CentOS 6.6 işlem düğümleri oluşan bir HPC Pack Azure tabanlı küme yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="9952b-117">This file configures an Azure-based HPC Pack cluster consisting of a Windows Server 2012 R2 head node and four size Large CentOS 6.6 compute nodes.</span></span> <span data-ttu-id="9952b-118">Bu dosya, ortamınız için gerektiği gibi özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="9952b-118">Customize this file as needed for your environment.</span></span>
* <span data-ttu-id="9952b-119">**NAMD yazılım ve öğretici dosyaları** -karşıdan NAMD yazılımlardan Linux için hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (kayıt gerekli).</span><span class="sxs-lookup"><span data-stu-id="9952b-119">**NAMD software and tutorial files** - Download NAMD software for Linux from hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registration required).</span></span> <span data-ttu-id="9952b-120">Bu makalede sürüm 2.10 NAMD üzerinde temel alır ve kullandığı hello [Linux-x86_64 (64-bit Intel/AMD Ethernet ile)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) arşiv.</span><span class="sxs-lookup"><span data-stu-id="9952b-120">This article is based on NAMD version 2.10, and uses hello [Linux-x86_64 (64-bit Intel/AMD with Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive.</span></span> <span data-ttu-id="9952b-121">Merhaba de karşıdan [NAMD öğreticileri](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span><span class="sxs-lookup"><span data-stu-id="9952b-121">Also download hello [NAMD tutorial files](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span></span> <span data-ttu-id="9952b-122">Merhaba yüklemeleri .tar dosyalarıdır ve bir Windows aracı tooextract hello dosyalarını hello küme baş düğümüne gerekir.</span><span class="sxs-lookup"><span data-stu-id="9952b-122">hello downloads are .tar files, and you need a Windows tool tooextract hello files on hello cluster head node.</span></span> <span data-ttu-id="9952b-123">tooextract hello dosyaları, bu makalenin sonraki bölümlerinde hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="9952b-123">tooextract hello files, follow hello instructions later in this article.</span></span> 
* <span data-ttu-id="9952b-124">**VMD** (isteğe bağlı) - NAMD işinizin toosee hello sonuçları yükleyip hello molecular görselleştirme program [VMD](http://www.ks.uiuc.edu/Research/vmd/) tercih ettiğiniz bir bilgisayarda.</span><span class="sxs-lookup"><span data-stu-id="9952b-124">**VMD** (optional) - toosee hello results of your NAMD job, download and install hello molecular visualization program [VMD](http://www.ks.uiuc.edu/Research/vmd/) on a computer of your choice.</span></span> <span data-ttu-id="9952b-125">Merhaba geçerli 1.9.2 sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="9952b-125">hello current version is 1.9.2.</span></span> <span data-ttu-id="9952b-126">VMD karşıdan başlatılan site tooget hello bakın.</span><span class="sxs-lookup"><span data-stu-id="9952b-126">See hello VMD download site tooget started.</span></span>  

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="9952b-127">İşlem düğümleri arasında karşılıklı güven ayarlama</span><span class="sxs-lookup"><span data-stu-id="9952b-127">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="9952b-128">Bir geçici düğüm işi birden çok Linux düğümler üzerinde çalışan gerektirir hello düğümleri tootrust birbirine (tarafından **rsh** veya **ssh**).</span><span class="sxs-lookup"><span data-stu-id="9952b-128">Running a cross-node job on multiple Linux nodes requires hello nodes tootrust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="9952b-129">Microsoft HPC Pack Iaas dağıtım betiği hello ile Merhaba HPC Pack kümesi oluşturduğunuzda, hello betik kalıcı karşılıklı güven belirttiğiniz hello yönetici hesabı için otomatik olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="9952b-129">When you create hello HPC Pack cluster with hello Microsoft HPC Pack IaaS deployment script, hello script automatically sets up permanent mutual trust for hello administrator account you specify.</span></span> <span data-ttu-id="9952b-130">Bir iş toothem ayrılan hello kümenin etki alanında oluşturduğunuz yönetici olmayan kullanıcılar için tooset hello düğümler arasında geçici karşılıklı güveni vardır.</span><span class="sxs-lookup"><span data-stu-id="9952b-130">For non-administrator users you create in hello cluster's domain, you have tooset up temporary mutual trust among hello nodes when a job is allocated toothem.</span></span> <span data-ttu-id="9952b-131">Ardından, Hello işi tamamlandıktan sonra hello ilişkisi yok.</span><span class="sxs-lookup"><span data-stu-id="9952b-131">Then, destroy hello relationship after hello job is complete.</span></span> <span data-ttu-id="9952b-132">toodo bu her kullanıcı için sağlayan bir RSA anahtar çifti toohello küme hangi HPC Pack tooestablish hello güven ilişkisi kullanır.</span><span class="sxs-lookup"><span data-stu-id="9952b-132">toodo this for each user, provide an RSA key pair toohello cluster which HPC Pack uses tooestablish hello trust relationship.</span></span> <span data-ttu-id="9952b-133">Yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="9952b-133">Instructions follow.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="9952b-134">RSA anahtar çifti oluşturma</span><span class="sxs-lookup"><span data-stu-id="9952b-134">Generate an RSA key pair</span></span>
<span data-ttu-id="9952b-135">Kolay toogenerate bir ortak anahtar ve özel anahtarı içeren bir RSA anahtar çifti, Linux hello çalıştırarak **ssh-keygen** komutu.</span><span class="sxs-lookup"><span data-stu-id="9952b-135">It's easy toogenerate an RSA key pair, which contains a public key and a private key, by running hello Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="9952b-136">Üzerinde tooa Linux bilgisayarda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9952b-136">Log on tooa Linux computer.</span></span>
2. <span data-ttu-id="9952b-137">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9952b-137">Run hello following command:</span></span>
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="9952b-138">Tuşuna **Enter** hello komut tamamlanıncaya kadar toouse hello varsayılan ayarlar.</span><span class="sxs-lookup"><span data-stu-id="9952b-138">Press **Enter** toouse hello default settings until hello command is completed.</span></span> <span data-ttu-id="9952b-139">Burada bir parola girmeyin; için bir parola istendiğinde, yalnızca basın **Enter**.</span><span class="sxs-lookup"><span data-stu-id="9952b-139">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![RSA anahtar çifti oluşturma][keygen]
3. <span data-ttu-id="9952b-141">Dizin toohello ~/.ssh dizini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9952b-141">Change directory toohello ~/.ssh directory.</span></span> <span data-ttu-id="9952b-142">Merhaba özel anahtarı id_rsa.pub id_rsa ve hello ortak anahtarında depolanır.</span><span class="sxs-lookup"><span data-stu-id="9952b-142">hello private key is stored in id_rsa and hello public key in id_rsa.pub.</span></span>
   
   ![Özel ve genel anahtarlar][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a><span data-ttu-id="9952b-144">Merhaba anahtar çifti toohello HPC paketi küme ekleme</span><span class="sxs-lookup"><span data-stu-id="9952b-144">Add hello key pair toohello HPC Pack cluster</span></span>
1. <span data-ttu-id="9952b-145">[Tarafından Uzak Masaüstü Bağlantısı](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello baş düğüm VM kullanarak hello hello kümeyi (örneğin, hpc\clusteradmin) dağıttığınızda sağlanan etki alanı kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="9952b-145">[Connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, hpc\clusteradmin).</span></span> <span data-ttu-id="9952b-146">Merhaba küme hello baş düğümünden yönetin.</span><span class="sxs-lookup"><span data-stu-id="9952b-146">You manage hello cluster from hello head node.</span></span>
2. <span data-ttu-id="9952b-147">Standart Windows Server yordamları toocreate bir etki alanı kullanıcı hesabı hello kümenin Active Directory etki alanında kullanın.</span><span class="sxs-lookup"><span data-stu-id="9952b-147">Use standard Windows Server procedures toocreate a domain user account in hello cluster's Active Directory domain.</span></span> <span data-ttu-id="9952b-148">Örneğin, hello baş düğümünde hello Active Directory Kullanıcıları ve Bilgisayarları aracını kullanın.</span><span class="sxs-lookup"><span data-stu-id="9952b-148">For example, use hello Active Directory User and Computers tool on hello head node.</span></span> <span data-ttu-id="9952b-149">Bu makaledeki örneklerde Hello hpcuser hello hpclab etki alanında (hpclab\hpcuser) adlı bir etki alanı kullanıcısı oluşturun varsayalım.</span><span class="sxs-lookup"><span data-stu-id="9952b-149">hello examples in this article assume you create a domain user named hpcuser in hello hpclab domain (hpclab\hpcuser).</span></span>
3. <span data-ttu-id="9952b-150">Merhaba etki alanı kullanıcı toohello HPC paketi Küme Küme kullanıcı olarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9952b-150">Add hello domain user toohello HPC Pack cluster as a cluster user.</span></span> <span data-ttu-id="9952b-151">Yönergeler için bkz: [ekleme veya kaldırma küme kullanıcılar](https://technet.microsoft.com/library/ff919330.aspx).</span><span class="sxs-lookup"><span data-stu-id="9952b-151">For instructions, see [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).</span></span>
4. <span data-ttu-id="9952b-152">C:\cred.XML ve kopyalama hello RSA anahtar verilerini içine adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9952b-152">Create a file named C:\cred.xml and copy hello RSA key data into it.</span></span> <span data-ttu-id="9952b-153">Bu makalenin hello sonunda örnek dosyalarını hello bir örnek bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9952b-153">You can find an example in hello sample files at hello end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. <span data-ttu-id="9952b-154">Bir komut istemi açın ve tooset hello veri hello hpclab\hpcuser hesabı için kimlik bilgileri komutu aşağıdaki hello girin.</span><span class="sxs-lookup"><span data-stu-id="9952b-154">Open a Command Prompt and enter hello following command tooset hello credentials data for hello hpclab\hpcuser account.</span></span> <span data-ttu-id="9952b-155">Merhaba kullandığınız **extendeddata** parametresi toopass hello dosyasının adı oluşturduğunuz hello C:\cred.xml hello anahtar veriler için.</span><span class="sxs-lookup"><span data-stu-id="9952b-155">You use hello **extendeddata** parameter toopass hello name of hello C:\cred.xml file you created for hello key data.</span></span>
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="9952b-156">Bu komut çıktısı başarıyla tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="9952b-156">This command completes successfully without output.</span></span> <span data-ttu-id="9952b-157">Toorun işleri ihtiyacınız hello kullanıcı hesapları için hello kimlik bilgilerini ayarlama sonra hello cred.xml dosyayı güvenli bir konumda depolayın veya silin.</span><span class="sxs-lookup"><span data-stu-id="9952b-157">After setting hello credentials for hello user accounts you need toorun jobs, store hello cred.xml file in a secure location, or delete it.</span></span>
6. <span data-ttu-id="9952b-158">Linux düğümlerinden biri üzerinde hello RSA anahtar çifti oluşturursa, bunları kullanmayı bitirdikten sonra toodelete hello anahtarları unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9952b-158">If you generated hello RSA key pair on one of your Linux nodes, remember toodelete hello keys after you finish using them.</span></span> <span data-ttu-id="9952b-159">Varolan bir id_rsa dosya veya id_rsa.pub dosyası bulursa, HPC Pack karşılıklı güven ayarlı değil.</span><span class="sxs-lookup"><span data-stu-id="9952b-159">HPC Pack does not set up mutual trust if it finds an existing id_rsa file or id_rsa.pub file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9952b-160">Bir yönetici tarafından gönderilen bir işin hello kök hesapta hello Linux düğümleri üzerinde çalıştığı için Linux iş paylaşılan bir kümede bir Küme Yöneticisi olarak çalışan öneririz yok.</span><span class="sxs-lookup"><span data-stu-id="9952b-160">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under hello root account on hello Linux nodes.</span></span> <span data-ttu-id="9952b-161">Yönetici olmayan bir kullanıcı tarafından gönderilen bir işi hello aynı hello işi kullanıcı adı ile bir yerel Linux kullanıcı hesabı altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="9952b-161">A job submitted by a non-administrator user runs under a local Linux user account with hello same name as hello job user.</span></span> <span data-ttu-id="9952b-162">Bu durumda, HPC Pack bu Linux kullanıcı için karşılıklı güven toohello iş ayrılan tüm hello düğümlere ayarlar.</span><span class="sxs-lookup"><span data-stu-id="9952b-162">In this case, HPC Pack sets up mutual trust for this Linux user across all hello nodes allocated toohello job.</span></span> <span data-ttu-id="9952b-163">Merhaba Linux kullanıcı hello Linux düğümlerde el ile Merhaba işi çalıştırmadan önce ayarlayabilirsiniz veya hello iş gönderildiğinde HPC Pack Merhaba kullanıcı otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9952b-163">You can set up hello Linux user manually on hello Linux nodes before running hello job, or HPC Pack creates hello user automatically when hello job is submitted.</span></span> <span data-ttu-id="9952b-164">HPC Pack Merhaba kullanıcı oluşturursa, HPC Pack Merhaba işi tamamlandıktan sonra onu siler.</span><span class="sxs-lookup"><span data-stu-id="9952b-164">If HPC Pack creates hello user, HPC Pack deletes it after hello job completes.</span></span> <span data-ttu-id="9952b-165">tooreduce güvenlik tehdidi, hello hello düğümlerinde hello işi tamamlandıktan sonra anahtarları kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="9952b-165">tooreduce security threat, hello keys are removed after hello job completes on hello nodes.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="9952b-166">Linux düğümleri için bir dosya paylaşımı ayarlama</span><span class="sxs-lookup"><span data-stu-id="9952b-166">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="9952b-167">Şimdi bir SMB dosya paylaşımı ayarlama ve tüm dosyalarda Linux düğümleri tooallow hello Linux düğümleri tooaccess NAMD ortak bir yol ile Merhaba paylaşılan klasöre bağlayın.</span><span class="sxs-lookup"><span data-stu-id="9952b-167">Now set up an SMB file share, and mount hello shared folder on all Linux nodes tooallow hello Linux nodes tooaccess NAMD files with a common path.</span></span> <span data-ttu-id="9952b-168">Adımları toomount hello baş düğüm üzerinde paylaşılan bir klasöre aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="9952b-168">Following are steps toomount a shared folder on hello head node.</span></span> <span data-ttu-id="9952b-169">Bir paylaşım için CentOS 6.6 gibi hello Azure dosya hizmeti şu anda desteklenmiyor dağıtımları önerilir.</span><span class="sxs-lookup"><span data-stu-id="9952b-169">A share is recommended for distributions such as CentOS 6.6 that currently don’t support hello Azure File service.</span></span> <span data-ttu-id="9952b-170">Linux düğümleri bir Azure dosya paylaşımı desteği olup [nasıl toouse Linux Azure File storage](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9952b-170">If your Linux nodes support an Azure File share, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="9952b-171">Ek dosya paylaşımı ile HPC Pack seçenekleri için bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="9952b-171">For additional file sharing options with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="9952b-172">Merhaba baş düğüm üzerinde bir klasör oluşturun ve okuma/yazma ayrıcalıklarına ayarlayarak tooEveryone paylaşın.</span><span class="sxs-lookup"><span data-stu-id="9952b-172">Create a folder on hello head node, and share it tooEveryone by setting Read/Write privileges.</span></span> <span data-ttu-id="9952b-173">Bu örnekte, \\ \\CentOS66HN\Namd CentOS66HN hello baş düğümü hello ana bilgisayar adı olduğu hello klasörünün hello adı değil.</span><span class="sxs-lookup"><span data-stu-id="9952b-173">In this example, \\\\CentOS66HN\Namd is hello name of hello folder, where CentOS66HN is hello host name of hello head node.</span></span>
2. <span data-ttu-id="9952b-174">Merhaba paylaşılan klasörde namd2 adlı bir alt klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9952b-174">Create a subfolder named namd2 in hello shared folder.</span></span> <span data-ttu-id="9952b-175">Namd2 içinde namdsample adlı başka bir alt klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9952b-175">In namd2, create another subfolder named namdsample.</span></span>
3. <span data-ttu-id="9952b-176">Bir Windows sürümünü kullanarak hello klasördeki Hello NAMD dosyaları ayıklayın **tar** veya .tar arşivler üzerinde çalıştığı başka bir Windows yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="9952b-176">Extract hello NAMD files in hello folder by using a Windows version of **tar** or another Windows utility that operates on .tar archives.</span></span> 
   
   * <span data-ttu-id="9952b-177">Merhaba NAMD tar arşiv çok ayıklamak\\\\CentOS66HN\Namd\namd2.</span><span class="sxs-lookup"><span data-stu-id="9952b-177">Extract hello NAMD tar archive too\\\\CentOS66HN\Namd\namd2.</span></span>
   * <span data-ttu-id="9952b-178">Merhaba öğreticileri altında ayıklamak \\ \\CentOS66HN\Namd\namd2\namdsample.</span><span class="sxs-lookup"><span data-stu-id="9952b-178">Extract hello tutorial files under \\\\CentOS66HN\Namd\namd2\namdsample.</span></span>
4. <span data-ttu-id="9952b-179">Bir Windows PowerShell penceresi açın ve toomount hello hello Linux düğümleri paylaşılan klasör komutları aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9952b-179">Open a Windows PowerShell window and run hello following commands toomount hello shared folder on hello Linux nodes.</span></span>
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="9952b-180">Merhaba ilk komut hello LinuxNodes grubundaki tüm düğümlerde /namd2 adlı bir klasör oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9952b-180">hello first command creates a folder named /namd2 on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="9952b-181">Merhaba ikinci komut hello paylaşılan klasör //CentOS66HN/Namd/namd2 dir_mode ve file_mode BITS kümesi too777 hello klasörüyle üzerine bağlar.</span><span class="sxs-lookup"><span data-stu-id="9952b-181">hello second command mounts hello shared folder //CentOS66HN/Namd/namd2 onto hello folder with dir_mode and file_mode bits set too777.</span></span> <span data-ttu-id="9952b-182">Merhaba *kullanıcıadı* ve *parola* hello komutu hello baş düğüm üzerinde bir kullanıcının kimlik bilgilerini hello olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9952b-182">hello *username* and *password* in hello command should be hello credentials of a user on hello head node.</span></span>

> [!NOTE]
> <span data-ttu-id="9952b-183">Merhaba "\\`" Merhaba ikinci komut dosyasındaki simge olan PowerShell bir kaçış simgesi.</span><span class="sxs-lookup"><span data-stu-id="9952b-183">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="9952b-184">"\\`,"anlamına gelir hello"," (virgül karakteri) hello komutu bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="9952b-184">“\\`,” means hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

## <a name="create-a-bash-script-toorun-a-namd-job"></a><span data-ttu-id="9952b-185">Bir Bash betik toorun NAMD işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="9952b-185">Create a Bash script toorun a NAMD job</span></span>
<span data-ttu-id="9952b-186">NAMD işinizi gereken bir *listesi* dosya **charmrun** toodetermine hello NAMD işlemleri başlatırken düğümleri toouse sayısı.</span><span class="sxs-lookup"><span data-stu-id="9952b-186">Your NAMD job needs a *nodelist* file for **charmrun** toodetermine hello number of nodes toouse when starting NAMD processes.</span></span> <span data-ttu-id="9952b-187">Merhaba listesi dosyası oluşturur ve çalışan bir Bash komut dosyası kullanarak **charmrun** bu listesi dosyayla.</span><span class="sxs-lookup"><span data-stu-id="9952b-187">You use a Bash script that generates hello nodelist file and runs **charmrun** with this nodelist file.</span></span> <span data-ttu-id="9952b-188">Ardından NAMD işi HPC Kümesi bu komut dosyasını çağıran Yöneticisi'nde gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9952b-188">You can then submit a NAMD job in HPC Cluster Manager that calls this script.</span></span>

<span data-ttu-id="9952b-189">Tercih ettiğiniz bir metin düzenleyicisi kullanarak hello /namd2 klasöründe hello NAMD program dosyalarını içeren bir Bash komut dosyası oluşturabilir ve hpccharmrun.sh adlandırın. Hızlı bir kavram kanıtı için hello örnek hpccharmrun.sh hello bu makalenin sonunda sağlanan komut dosyasını kopyalayın ve çok Git[NAMD işi göndermek](#submit-a-namd-job).</span><span class="sxs-lookup"><span data-stu-id="9952b-189">Using a text editor of your choice, create a Bash script in hello /namd2 folder containing hello NAMD program files and name it hpccharmrun.sh. For a quick proof of concept, copy hello example hpccharmrun.sh script provided at hello end of this article and go too[Submit a NAMD job](#submit-a-namd-job).</span></span>

> [!TIP]
> <span data-ttu-id="9952b-190">Satır sonlarını (yalnızca LF, CR LF) kodunuzu Linux bir metin dosyası olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9952b-190">Save your script as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="9952b-191">Bu, düzgün şekilde hello Linux düğümlerinde çalıştığını sağlar.</span><span class="sxs-lookup"><span data-stu-id="9952b-191">This ensures that it runs properly on hello Linux nodes.</span></span>
> 
> 

<span data-ttu-id="9952b-192">Bu bash betiğin yaptığı hakkında ayrıntılar verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="9952b-192">Following are details about what this bash script does.</span></span> 

1. <span data-ttu-id="9952b-193">Bazı değişkenleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="9952b-193">Define some variables.</span></span>
   
   ```bash
   #!/bin/bash
   
   # hello path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. <span data-ttu-id="9952b-194">Düğüm bilgi hello ortam değişkenlerinin alın.</span><span class="sxs-lookup"><span data-stu-id="9952b-194">Get node information from hello environment variables.</span></span> <span data-ttu-id="9952b-195">$NODESCORES $CCP_NODES_CORES bölünmüş sözcükleri listesini depolar.</span><span class="sxs-lookup"><span data-stu-id="9952b-195">$NODESCORES stores a list of split words from $CCP_NODES_CORES.</span></span> <span data-ttu-id="9952b-196">$COUNT $NODESCORES hello boyutudur.</span><span class="sxs-lookup"><span data-stu-id="9952b-196">$COUNT is hello size of $NODESCORES.</span></span>
   
   ```
   # Get node information from hello environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   <span data-ttu-id="9952b-197">Merhaba $CCP_NODES_CORES değişkeni için Hello biçimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9952b-197">hello format for hello $CCP_NODES_CORES variable is as follows:</span></span>
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   <span data-ttu-id="9952b-198">Bu değişken düğümler, düğüm adı ve her düğümde toohello iş ayrılan çekirdek sayısı toplam sayısı hello listeler.</span><span class="sxs-lookup"><span data-stu-id="9952b-198">This variable lists hello total number of nodes, node names, and number of cores on each node that are allocated toohello job.</span></span> <span data-ttu-id="9952b-199">Merhaba iş 10 çekirdekler toorun gerekirse, örneğin, $CCP_NODES_CORES hello değerini benzer:</span><span class="sxs-lookup"><span data-stu-id="9952b-199">For example, if hello job needs 10 cores toorun, hello value of $CCP_NODES_CORES is similar to:</span></span>
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. <span data-ttu-id="9952b-200">Merhaba $CCP_NODES_CORES değişken ayarlanmamışsa, başlangıç **charmrun** doğrudan.</span><span class="sxs-lookup"><span data-stu-id="9952b-200">If hello $CCP_NODES_CORES variable is not set, start **charmrun** directly.</span></span> <span data-ttu-id="9952b-201">(Bu komut dosyasını doğrudan Linux düğümlerinde çalıştırdığınızda bu yalnızca olmalıdır.)</span><span class="sxs-lookup"><span data-stu-id="9952b-201">(This should only occur when you run this script directly on your Linux nodes.)</span></span>
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. <span data-ttu-id="9952b-202">Veya bir listesi dosyası oluşturma **charmrun**.</span><span class="sxs-lookup"><span data-stu-id="9952b-202">Or create a nodelist file for **charmrun**.</span></span>
   
   ```
   else
     # Create hello nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write hello head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into hello nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. <span data-ttu-id="9952b-203">Çalıştırma **charmrun** hello listesi dosyayla dönüş durumunu almak ve hello listesi dosyasını hello sonunda kaldırın.</span><span class="sxs-lookup"><span data-stu-id="9952b-203">Run **charmrun** with hello nodelist file, get its return status, and remove hello nodelist file at hello end.</span></span>
   
   <span data-ttu-id="9952b-204">${CCP_NUMCPUS} hello HPC paketi üstbilgi düğümü tarafından ayarlanmış başka bir ortam değişkenidir.</span><span class="sxs-lookup"><span data-stu-id="9952b-204">${CCP_NUMCPUS} is another environment variable set by hello HPC Pack head node.</span></span> <span data-ttu-id="9952b-205">Merhaba toothis iş ayrılan toplam çekirdek sayısı depolar.</span><span class="sxs-lookup"><span data-stu-id="9952b-205">It stores hello number of total cores allocated toothis job.</span></span> <span data-ttu-id="9952b-206">Bu işlem toospecify hello sayısı charmrun için kullanırız.</span><span class="sxs-lookup"><span data-stu-id="9952b-206">We use it toospecify hello number of processes for charmrun.</span></span>
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. <span data-ttu-id="9952b-207">Merhaba çıkış **charmrun** dönüş durumu.</span><span class="sxs-lookup"><span data-stu-id="9952b-207">Exit with hello **charmrun** return status.</span></span>
   
   ```
   exit ${RTNSTS}
   ```

<span data-ttu-id="9952b-208">Merhaba bilgilerini hello listesi dosyasına hangi hello komut dosyası oluşturur, aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9952b-208">Following is hello information in hello nodelist file, which hello script generates:</span></span>

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

<span data-ttu-id="9952b-209">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="9952b-209">For example:</span></span>

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a><span data-ttu-id="9952b-210">NAMD işi gönderin</span><span class="sxs-lookup"><span data-stu-id="9952b-210">Submit a NAMD job</span></span>
<span data-ttu-id="9952b-211">Artık hazır toosubmit NAMD işi HPC Küme Yöneticisi'nde bulunur.</span><span class="sxs-lookup"><span data-stu-id="9952b-211">Now you are ready toosubmit a NAMD job in HPC Cluster Manager.</span></span>

1. <span data-ttu-id="9952b-212">Tooyour küme baş düğümüne bağlanmak ve HPC Küme Yöneticisi'ni başlatın.</span><span class="sxs-lookup"><span data-stu-id="9952b-212">Connect tooyour cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="9952b-213">İçinde **kaynak yönetimi**, hello Linux işlem düğümlerini hello olduğundan emin olun **çevrimiçi** durumu.</span><span class="sxs-lookup"><span data-stu-id="9952b-213">In **Resource Management**, ensure that hello Linux compute nodes are in hello **Online** state.</span></span> <span data-ttu-id="9952b-214">Değilse, bunları seçin ve tıklatın **çevrimiçine**.</span><span class="sxs-lookup"><span data-stu-id="9952b-214">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="9952b-215">İçinde **iş yönetimi**, tıklatın **yeni iş**.</span><span class="sxs-lookup"><span data-stu-id="9952b-215">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="9952b-216">İş için bir ad girin *hpccharmrun*.</span><span class="sxs-lookup"><span data-stu-id="9952b-216">Enter a name for job such as *hpccharmrun*.</span></span>
   
   ![Yeni HPC iş][namd_job]
5. <span data-ttu-id="9952b-218">Hello üzerinde **iş ayrıntılarını** sayfasında **iş kaynakları**, kaynak olarak hello türünü seçin **düğümü** ve kümesi hello **Minimum** too3.</span><span class="sxs-lookup"><span data-stu-id="9952b-218">On hello **Job Details** page, under **Job Resources**, select hello type of resource as **Node** and set hello **Minimum** too3.</span></span> <span data-ttu-id="9952b-219">, şu üç Linux düğümlerinde hello işini çalıştırın ve her düğümün dört çekirdeğe sahip.</span><span class="sxs-lookup"><span data-stu-id="9952b-219">, we run hello job on three Linux nodes and each node has four cores.</span></span>
   
   ![İş kaynakları][job_resources]
6. <span data-ttu-id="9952b-221">Tıklatın **Düzenle görevleri** hello sol gezinti bölmesinde ve ardından **Ekle** tooadd görev toohello işi.</span><span class="sxs-lookup"><span data-stu-id="9952b-221">Click **Edit Tasks** in hello left navigation, and then click **Add** tooadd a task toohello job.</span></span>    
7. <span data-ttu-id="9952b-222">Merhaba üzerinde **görev ayrıntılarını ve g/ç yönlendirmesi** sayfasında, aşağıdaki değerleri kümesi hello:</span><span class="sxs-lookup"><span data-stu-id="9952b-222">On hello **Task Details and I/O Redirection** page, set hello following values:</span></span>
   
   * <span data-ttu-id="9952b-223">**Komut satırı**-
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span><span class="sxs-lookup"><span data-stu-id="9952b-223">**Command line** -
`/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span></span>
     
     > [!TIP]
     > <span data-ttu-id="9952b-224">Merhaba önceki komut satır sonu olmayan tek bir komut satırıdır.</span><span class="sxs-lookup"><span data-stu-id="9952b-224">hello preceding command line is a single command without line breaks.</span></span> <span data-ttu-id="9952b-225">Birkaç satırdaki altında tooappear sarmalar **komut satırı**.</span><span class="sxs-lookup"><span data-stu-id="9952b-225">It wraps tooappear on several lines under **Command line**.</span></span>
     > 
     > 
   * <span data-ttu-id="9952b-226">**Çalışma dizini** -/namd2</span><span class="sxs-lookup"><span data-stu-id="9952b-226">**Working directory** - /namd2</span></span>
   * <span data-ttu-id="9952b-227">**Minimum** - 3</span><span class="sxs-lookup"><span data-stu-id="9952b-227">**Minimum** - 3</span></span>
     
     ![Görev Ayrıntıları][task_details]
     
     > [!NOTE]
     > <span data-ttu-id="9952b-229">Çünkü hello çalışma dizini Burada ayarlanan **charmrun** toonavigate toohello çalışır her düğümde aynı çalışma dizini.</span><span class="sxs-lookup"><span data-stu-id="9952b-229">You set hello working directory here because **charmrun** tries toonavigate toohello same working directory on each node.</span></span> <span data-ttu-id="9952b-230">HPC Pack Merhaba komut Hello çalışma dizini ayarlanmamışsa hello Linux düğümlerinden biri üzerinde oluşturduğunuz rastgele adlandırılmış bir klasördeki başlatır.</span><span class="sxs-lookup"><span data-stu-id="9952b-230">If hello working directory isn't set, HPC Pack starts hello command in a randomly named folder created on one of hello Linux nodes.</span></span> <span data-ttu-id="9952b-231">Bu, diğer düğümlere hello üzerinde aşağıdaki hata hello neden olur: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid bu sorunu hello çalışma dizini olarak tüm düğümler tarafından erişilebilen bir klasör yolu belirtin.</span><span class="sxs-lookup"><span data-stu-id="9952b-231">This causes hello following error on hello other nodes: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid this problem, specify a folder path that can be accessed by all nodes as hello working directory.</span></span>
     > 
     > 
8. <span data-ttu-id="9952b-232">Tıklatın **Tamam** ve ardından **gönderme** toorun bu işi.</span><span class="sxs-lookup"><span data-stu-id="9952b-232">Click **OK** and then click **Submit** toorun this job.</span></span>
   
   <span data-ttu-id="9952b-233">Varsayılan olarak, HPC Pack Merhaba iş geçerli oturum açmış kullanıcı hesabınız olarak gönderir.</span><span class="sxs-lookup"><span data-stu-id="9952b-233">By default, HPC Pack submits hello job as your current logged-on user account.</span></span> <span data-ttu-id="9952b-234">Tıklattıktan sonra bir iletişim kutusu tooenter hello kullanıcı adı ve parola isteyebilir **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="9952b-234">A dialog box might prompt you tooenter hello user name and password after you click **Submit**.</span></span>
   
   ![İş kimlik bilgileri][creds]
   
   <span data-ttu-id="9952b-236">Bazı koşullarda HPC Pack önce giriş ve bu iletişim kutusunu göstermez hello kullanıcı bilgilerini hatırlıyor.</span><span class="sxs-lookup"><span data-stu-id="9952b-236">Under some conditions, HPC Pack remembers hello user information you input before and doesn't show this dialog box.</span></span> <span data-ttu-id="9952b-237">toomake HPC paketi yeniden göstermek, komutu bir komut isteminde aşağıdaki hello girin ve hello işi göndermek.</span><span class="sxs-lookup"><span data-stu-id="9952b-237">toomake HPC Pack show it again, enter hello following command at a Command Prompt and then submit hello job.</span></span>
   
   ```command
   hpccred delcreds
   ```
9. <span data-ttu-id="9952b-238">Merhaba işi birkaç dakika toofinish alır.</span><span class="sxs-lookup"><span data-stu-id="9952b-238">hello job takes several minutes toofinish.</span></span>
10. <span data-ttu-id="9952b-239">Merhaba iş günlüğü Bul \\ <headnodeName>\Namd\namd2\namd2_hpccharmrun.log ve hello çıkış dosyalarında \\ <headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span><span class="sxs-lookup"><span data-stu-id="9952b-239">Find hello job log at \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log and hello output files in \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span></span>
11. <span data-ttu-id="9952b-240">İsteğe bağlı olarak, VMD tooview iş sonuçlarınızı başlatın.</span><span class="sxs-lookup"><span data-stu-id="9952b-240">Optionally, start VMD tooview your job results.</span></span> <span data-ttu-id="9952b-241">Merhaba NAMD çıktı dosyaları (Bu durumda, su küre içinde ubiquitin protein molecule) görselleştirme için hello bu makalenin kapsamı dışındadır hello adımlardır.</span><span class="sxs-lookup"><span data-stu-id="9952b-241">hello steps for visualizing hello NAMD output files (in this case, a ubiquitin protein molecule in a water sphere) are beyond hello scope of this article.</span></span> <span data-ttu-id="9952b-242">Bkz: [NAMD öğretici](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="9952b-242">See [NAMD Tutorial](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) for details.</span></span>
    
    ![İş sonuçları][vmd_view]

## <a name="sample-files"></a><span data-ttu-id="9952b-244">Örnek dosyaları</span><span class="sxs-lookup"><span data-stu-id="9952b-244">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="9952b-245">PowerShell komut dosyası tarafından küme dağıtımı için örnek XML yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="9952b-245">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
      <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS66HN</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS66LN-%00%</VMNamePattern>
    <ServiceName>MyLnxCNService</ServiceName>
     <VMSize>Large</VMSize>
     <NodeCount>4</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-66-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>    
```

### <a name="sample-credxml-file"></a><span data-ttu-id="9952b-246">Örnek cred.xml dosyası</span><span class="sxs-lookup"><span data-stu-id="9952b-246">Sample cred.xml file</span></span>
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

### <a name="sample-hpccharmrunsh-script"></a><span data-ttu-id="9952b-247">Örnek hpccharmrun.sh komut dosyası</span><span class="sxs-lookup"><span data-stu-id="9952b-247">Sample hpccharmrun.sh script</span></span>
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
# Charmrun command
CHARMRUN=${SCRIPT_PATH}/charmrun
# Argument of ++nodelist
NODELIST_OPT="++nodelist"
# Argument of ++p
NUMPROCESS="+p"

# Get node information from ENVs
# CCP_NODES_CORES=3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 4
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # If CCP_NODES_CORES is not found or is empty, just run hello charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create hello nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write hello head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into hello nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello charmrun with nodelist arg
    #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
    ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}
```

 

<!--Image references-->
[keygen]:media/hpcpack-cluster-namd/keygen.png
[keys]:media/hpcpack-cluster-namd/keys.png
[namd_job]:media/hpcpack-cluster-namd/namd_job.png
[job_resources]:media/hpcpack-cluster-namd/job_resources.png
[creds]:media/hpcpack-cluster-namd/creds.png
[task_details]:media/hpcpack-cluster-namd/task_details.png
[vmd_view]:media/hpcpack-cluster-namd/vmd_view.png
