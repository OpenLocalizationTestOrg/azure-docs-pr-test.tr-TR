---
title: "Excel ve SOA için aaaHPC paketi küme | Microsoft Docs"
description: "Büyük ölçekli Excel ve SOA iş yüklerini Azure HPC Pack kümede çalışan kullanmaya başlama"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="75b6b-103">Excel ve SOA iş yüklerini Azure HPC Pack kümede çalışan kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="75b6b-103">Get started running Excel and SOA workloads on an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="75b6b-104">Bu makalede nasıl toodeploy Microsoft HPC Pack 2012 R2 küme Azure sanal makinelerde bir Azure Hızlı Başlangıç şablonu veya isteğe bağlı olarak bir Azure PowerShell dağıtım komut dosyası kullanarak gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="75b6b-104">This article shows you how toodeploy a Microsoft HPC Pack 2012 R2 cluster on Azure virtual machines by using an Azure quickstart template, or optionally an Azure PowerShell deployment script.</span></span> <span data-ttu-id="75b6b-105">Merhaba küme Azure Market VM görüntüleri tasarlanmış toorun Microsoft Excel ya da hizmet odaklı mimari (SOA) iş yükleri ile HPC paketi kullanır.</span><span class="sxs-lookup"><span data-stu-id="75b6b-105">hello cluster uses Azure Marketplace VM images designed toorun Microsoft Excel or service-oriented architecture (SOA) workloads with HPC Pack.</span></span> <span data-ttu-id="75b6b-106">Merhaba küme toorun Excel HPC ve bir şirket içi istemci bilgisayarından SOA Hizmetleri'ni kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75b6b-106">You can use hello cluster toorun Excel HPC and SOA services from an on-premises client computer.</span></span> <span data-ttu-id="75b6b-107">Excel çalışma kitabı aktarma ve Excel kullanıcı tanımlı işlevler veya UDF'ler Hello Excel HPC hizmetleri içerir.</span><span class="sxs-lookup"><span data-stu-id="75b6b-107">hello Excel HPC services include Excel workbook offloading and Excel user-defined functions, or UDFs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="75b6b-108">Bu makalede özellikleri, şablonları ve komut dosyaları HPC Pack 2012 R2 için temel alır.</span><span class="sxs-lookup"><span data-stu-id="75b6b-108">This article is based on features, templates, and scripts for HPC Pack 2012 R2.</span></span> <span data-ttu-id="75b6b-109">Bu senaryo HPC Pack 2016'şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="75b6b-109">This scenario is not currently supported in HPC Pack 2016.</span></span>
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="75b6b-110">Yüksek bir düzeyde hello Aşağıdaki diyagramda hello HPC paketi küme oluşturduğunuz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="75b6b-110">At a high level, hello following diagram shows hello HPC Pack cluster you create.</span></span>

![Excel iş yükleri çalıştıran düğümlerle HPC Kümesi][scenario]

## <a name="prerequisites"></a><span data-ttu-id="75b6b-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="75b6b-112">Prerequisites</span></span>
* <span data-ttu-id="75b6b-113">**İstemci bilgisayar** -bir Windows tabanlı bir istemci bilgisayar toosubmit örnek Excel ve SOA işleri toohello kümesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="75b6b-113">**Client computer** - You need a Windows-based client computer toosubmit sample Excel and SOA jobs toohello cluster.</span></span> <span data-ttu-id="75b6b-114">(Bu dağıtım yöntemi seçerseniz) bir Windows bilgisayar toorun hello Azure PowerShell küme dağıtım betiğini de gerekir.</span><span class="sxs-lookup"><span data-stu-id="75b6b-114">You also need a Windows computer toorun hello Azure PowerShell cluster deployment script (if you choose that deployment method).</span></span>
* <span data-ttu-id="75b6b-115">**Azure aboneliği** -bir Azure aboneliğiniz yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="75b6b-115">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="75b6b-116">**Çekirdek kota** -özellikle çok çekirdekli VM boyutları birkaç küme düğümleri dağıtırsanız tooincrease hello kota çekirdek, gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="75b6b-116">**Cores quota** - You might need tooincrease hello quota of cores, especially if you deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="75b6b-117">Hello çekirdek kota Kaynağı Yöneticisi'nde bir Azure Hızlı Başlangıç şablonu kullanıyorsanız, Azure bölgesidir.</span><span class="sxs-lookup"><span data-stu-id="75b6b-117">If you are using an Azure quickstart template, hello cores quota in Resource Manager is per Azure region.</span></span> <span data-ttu-id="75b6b-118">Bu durumda, belirli bir bölgedeki tooincrease hello kota gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="75b6b-118">In that case, you might need tooincrease hello quota in a specific region.</span></span> <span data-ttu-id="75b6b-119">Bkz: [Azure aboneliği sınırları, kotaları ve kısıtlamaları](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="75b6b-119">See [Azure subscription limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="75b6b-120">tooincrease bir kota [bir çevrimiçi müşteri destek isteği açma](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) herhangi bir ücret alınmaz.</span><span class="sxs-lookup"><span data-stu-id="75b6b-120">tooincrease a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>
* <span data-ttu-id="75b6b-121">**Microsoft Office lisansı** - işlem düğümleri, Microsoft Excel ile bir Market HPC Pack 2012 R2 VM görüntüsü kullanarak Microsoft Excel Professional Plus 2013 30 günlük değerlendirme sürümü yüklüyse dağıtırsanız.</span><span class="sxs-lookup"><span data-stu-id="75b6b-121">**Microsoft Office license** - If you deploy compute nodes using a Marketplace HPC Pack 2012 R2 VM image with Microsoft Excel, a 30-day evaluation version of Microsoft Excel Professional Plus 2013 is installed.</span></span> <span data-ttu-id="75b6b-122">Merhaba değerlendirme süresinden sonra tooprovide bir geçerli Microsoft Office lisansı tooactivate Excel toocontinue toorun iş yükleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="75b6b-122">After hello evaluation period, you need tooprovide a valid Microsoft Office license tooactivate Excel toocontinue toorun workloads.</span></span> <span data-ttu-id="75b6b-123">Bkz: [Excel etkinleştirme](#excel-activation) bu makalenin ilerisinde yer.</span><span class="sxs-lookup"><span data-stu-id="75b6b-123">See [Excel activation](#excel-activation) later in this article.</span></span> 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="75b6b-124">1. Adım</span><span class="sxs-lookup"><span data-stu-id="75b6b-124">Step 1.</span></span> <span data-ttu-id="75b6b-125">Azure HPC Pack kümede ayarlama</span><span class="sxs-lookup"><span data-stu-id="75b6b-125">Set up an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="75b6b-126">İki seçenek tooset hello HPC Pack 2012 R2 kümesi gösteriyoruz: ilk, bir Azure Hızlı Başlangıç şablonu ile hello Azure Portalı '; ve ikincisi, bir Azure PowerShell dağıtım komut dosyası kullanarak.</span><span class="sxs-lookup"><span data-stu-id="75b6b-126">We show two options tooset up hello HPC Pack 2012 R2 cluster: first, using an Azure quickstart template and hello Azure portal; and second, using an Azure PowerShell deployment script.</span></span>

### <a name="option-1-use-a-quickstart-template"></a><span data-ttu-id="75b6b-127">Seçenek 1.</span><span class="sxs-lookup"><span data-stu-id="75b6b-127">Option 1.</span></span> <span data-ttu-id="75b6b-128">Hızlı Başlatma şablonunu kullanma</span><span class="sxs-lookup"><span data-stu-id="75b6b-128">Use a quickstart template</span></span>
<span data-ttu-id="75b6b-129">Kullanım Azure Hızlı Başlangıç şablonu tooquickly hello Azure portal HPC Pack kümede dağıtın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-129">Use an Azure quickstart template tooquickly deploy an HPC Pack cluster in hello Azure portal.</span></span> <span data-ttu-id="75b6b-130">Merhaba Portalı'nda hello şablonu açtığınızda hello ayarları, kümeniz için girdiğiniz basit bir kullanıcı Arabirimi alma.</span><span class="sxs-lookup"><span data-stu-id="75b6b-130">When you open hello template in hello portal, you get a simple UI where you enter hello settings for your cluster.</span></span> <span data-ttu-id="75b6b-131">Merhaba adımlar şunlardır.</span><span class="sxs-lookup"><span data-stu-id="75b6b-131">Here are hello steps.</span></span> 

> [!TIP]
> <span data-ttu-id="75b6b-132">İsterseniz, kullanın bir [Azure Marketi şablonu](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) özellikle Excel iş yükleri için benzer bir küme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="75b6b-132">If you want, use an [Azure Marketplace template](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) that creates a similar cluster specifically for Excel workloads.</span></span> <span data-ttu-id="75b6b-133">Merhaba adımları hello aşağıdakiler arasından biraz farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="75b6b-133">hello steps differ slightly from hello following.</span></span>
> 
> 

1. <span data-ttu-id="75b6b-134">Merhaba ziyaret [HPC küme oluşturma şablonu GitHub sayfasında](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span><span class="sxs-lookup"><span data-stu-id="75b6b-134">Visit hello [Create HPC Cluster template page on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span></span> <span data-ttu-id="75b6b-135">İsterseniz, hello şablon ve hello kaynak kodu hakkında bilgileri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-135">If you want, review information about hello template and hello source code.</span></span>
2. <span data-ttu-id="75b6b-136">Tıklatın **tooAzure dağıtmak** toostart hello şablon hello Azure portal ile bir dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="75b6b-136">Click **Deploy tooAzure** toostart a deployment with hello template in hello Azure portal.</span></span>
   
   ![Şablon tooAzure dağıtma][github]
3. <span data-ttu-id="75b6b-138">Merhaba Portalı'nda hello HPC küme şablon için bu adımları tooenter hello parametreleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-138">In hello portal, follow these steps tooenter hello parameters for hello HPC cluster template.</span></span>
   
   <span data-ttu-id="75b6b-139">a.</span><span class="sxs-lookup"><span data-stu-id="75b6b-139">a.</span></span> <span data-ttu-id="75b6b-140">Merhaba üzerinde **parametreleri** sayfasında, girin veya hello şablon parametreleri için değerleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-140">On hello **Parameters** page, enter or modify values for hello template parameters.</span></span> <span data-ttu-id="75b6b-141">(Merhaba simgesi sonraki tooeach ayarı Yardım bilgileri için tıklatın.) Örnek değerler ekran aşağıdaki hello gösterilir.</span><span class="sxs-lookup"><span data-stu-id="75b6b-141">(Click hello icon next tooeach setting for help information.) Sample values are shown in hello following screen.</span></span> <span data-ttu-id="75b6b-142">Bu örnek adlı bir küme oluşturur *hpc01* hello içinde *hpc.local* bir baş düğüm ve 2 oluşan etki alanı işlem düğümlerini.</span><span class="sxs-lookup"><span data-stu-id="75b6b-142">This example creates a cluster named *hpc01* in hello *hpc.local* domain consisting of a head node and 2 compute nodes.</span></span> <span data-ttu-id="75b6b-143">Merhaba işlem düğümleri, Microsoft Excel içeren bir HPC Pack VM görüntüden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="75b6b-143">hello compute nodes are created from an HPC Pack VM image that includes Microsoft Excel.</span></span>
   
   ![Parametreleri girin][parameters-new-portal]
   
   > [!NOTE]
   > <span data-ttu-id="75b6b-145">VM hello otomatik olarak oluşturulur hello baş düğüm [son Market görüntüsü](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) HPC paketi 2012 R2'in Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="75b6b-145">hello head node VM is created automatically from hello [latest Marketplace image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) of HPC Pack 2012 R2 on Windows Server 2012 R2.</span></span> <span data-ttu-id="75b6b-146">Şu anda hello görüntü HPC Pack 2012 R2 güncelleştirme 3 ' temel alır.</span><span class="sxs-lookup"><span data-stu-id="75b6b-146">Currently hello image is based on HPC Pack 2012 R2 Update 3.</span></span>
   > 
   > <span data-ttu-id="75b6b-147">İşlem düğümü VM'ler hello son seçili hello işlem düğümü ailesi görüntüden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="75b6b-147">Compute node VMs are created from hello latest image of hello selected compute node family.</span></span> <span data-ttu-id="75b6b-148">Select hello **ComputeNodeWithExcel** Microsoft Excel Professional Plus 2013'in değerlendirme sürümünü içeren hello son HPC Pack işlem düğümü görüntüsü seçeneği.</span><span class="sxs-lookup"><span data-stu-id="75b6b-148">Select hello **ComputeNodeWithExcel** option for hello latest HPC Pack compute node image that includes an evaluation version of Microsoft Excel Professional Plus 2013.</span></span> <span data-ttu-id="75b6b-149">toodeploy genel SOA oturumları veya Excel UDF aktarması, bir küme seçin hello **ComputeNode** (Excel yüklü olmadan) seçeneği.</span><span class="sxs-lookup"><span data-stu-id="75b6b-149">toodeploy a cluster for general SOA sessions or for Excel UDF offloading, choose hello **ComputeNode** option (without Excel installed).</span></span>
   > 
   > 
   
   <span data-ttu-id="75b6b-150">b.</span><span class="sxs-lookup"><span data-stu-id="75b6b-150">b.</span></span> <span data-ttu-id="75b6b-151">Merhaba abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-151">Choose hello subscription.</span></span>
   
   <span data-ttu-id="75b6b-152">c.</span><span class="sxs-lookup"><span data-stu-id="75b6b-152">c.</span></span> <span data-ttu-id="75b6b-153">Merhaba küme için bir kaynak grubu oluşturun *hpc01RG*.</span><span class="sxs-lookup"><span data-stu-id="75b6b-153">Create a resource group for hello cluster, such as *hpc01RG*.</span></span>
   
   <span data-ttu-id="75b6b-154">d.</span><span class="sxs-lookup"><span data-stu-id="75b6b-154">d.</span></span> <span data-ttu-id="75b6b-155">Orta ABD gibi hello kaynak grubu için bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-155">Choose a location for hello resource group, such as Central US.</span></span>
   
   <span data-ttu-id="75b6b-156">e.</span><span class="sxs-lookup"><span data-stu-id="75b6b-156">e.</span></span> <span data-ttu-id="75b6b-157">Merhaba üzerinde **yasal koşulları** sayfasında, hello koşullarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-157">On hello **Legal terms** page, review hello terms.</span></span> <span data-ttu-id="75b6b-158">Kabul ediyorsa **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="75b6b-158">If you agree, click **Purchase**.</span></span> <span data-ttu-id="75b6b-159">Merhaba şablonu için başlangıç değerlerini ayarlama işiniz bittiğinde, ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="75b6b-159">Then, when you are finished setting hello values for hello template, click **Create**.</span></span>
4. <span data-ttu-id="75b6b-160">Merhaba dağıtım tamamlandığında (genellikle yaklaşık 30 dakika sürer), hello küme baş düğümünden export hello küme sertifika dosyası.</span><span class="sxs-lookup"><span data-stu-id="75b6b-160">When hello deployment completes (it typically takes around 30 minutes), export hello cluster certificate file from hello cluster head node.</span></span> <span data-ttu-id="75b6b-161">Bir sonraki adımda hello istemci bilgisayar tooprovide hello sunucu tarafı kimlik doğrulaması için Güvenli HTTP bağlama üzerinde ortak bu sertifikayı içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-161">In a later step, you import this public certificate on hello client computer tooprovide hello server-side authentication for secure HTTP binding.</span></span>
   
   <span data-ttu-id="75b6b-162">a.</span><span class="sxs-lookup"><span data-stu-id="75b6b-162">a.</span></span> <span data-ttu-id="75b6b-163">Hello Azure portal, toohello Pano, select hello baş düğümüne gidin ve'ı tıklatın **Bağlan** Uzak Masaüstü kullanarak hello sayfa tooconnect hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="75b6b-163">In hello Azure portal, go toohello dashboard, select hello head node, and click **Connect** at hello top of hello page tooconnect using Remote Desktop.</span></span>
   
    <!-- ![Connect toohello head node][connect] -->
   
   <span data-ttu-id="75b6b-164">b.</span><span class="sxs-lookup"><span data-stu-id="75b6b-164">b.</span></span> <span data-ttu-id="75b6b-165">Sertifika Yöneticisi tooexport hello baş düğümüne sertifika (Cert: \LocalMachine\My altında bulunur) standart yordamları hello özel anahtar olmadan kullanın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-165">Use standard procedures in Certificate Manager tooexport hello head node certificate (located under Cert:\LocalMachine\My) without hello private key.</span></span> <span data-ttu-id="75b6b-166">Bu örnekte, verme *CN = hpc01.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="75b6b-166">In this example, export *CN = hpc01.eastus.cloudapp.azure.com*.</span></span>
   
   ![Merhaba sertifikasını dışarı aktarma][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="75b6b-168">Seçenek 2.</span><span class="sxs-lookup"><span data-stu-id="75b6b-168">Option 2.</span></span> <span data-ttu-id="75b6b-169">Merhaba HPC Pack Iaas dağıtım betiği kullanın</span><span class="sxs-lookup"><span data-stu-id="75b6b-169">Use hello HPC Pack IaaS Deployment script</span></span>
<span data-ttu-id="75b6b-170">Merhaba HPC Pack Iaas dağıtım komut dosyası başka bir verimli şekilde toodeploy bir HPC paketi küme sağlar.</span><span class="sxs-lookup"><span data-stu-id="75b6b-170">hello HPC Pack IaaS deployment script provides another versatile way toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="75b6b-171">Merhaba şablonu hello Azure Resource Manager dağıtım modeli kullanır ancak hello Klasik dağıtım modelinde, bir küme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="75b6b-171">It creates a cluster in hello classic deployment model, whereas hello template uses hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="75b6b-172">Ayrıca, hello betik hello Azure genel veya Azure Çin hizmetinde bir abonelik ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="75b6b-172">Also, hello script is compatible with a subscription in either hello Azure Global or Azure China service.</span></span>

<span data-ttu-id="75b6b-173">**Ek önkoşulları**</span><span class="sxs-lookup"><span data-stu-id="75b6b-173">**Additional prerequisites**</span></span>

* <span data-ttu-id="75b6b-174">**Azure PowerShell** - [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview) (sürüm 0.8.10 veya üzeri) istemci bilgisayarınızda.</span><span class="sxs-lookup"><span data-stu-id="75b6b-174">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="75b6b-175">**HPC Pack Iaas dağıtım betiği** - karşıdan yükle ve en son sürümünü hello hello betikten hello paket [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="75b6b-175">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="75b6b-176">Merhaba betik Hello sürümünü çalıştırarak denetleme `New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="75b6b-176">Check hello version of hello script by running `New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="75b6b-177">Bu makalede, sürüm 4.5.0 veya daha sonra hello komut dosyasının temel alır.</span><span class="sxs-lookup"><span data-stu-id="75b6b-177">This article is based on version 4.5.0 or later of hello script.</span></span>

<span data-ttu-id="75b6b-178">**Merhaba yapılandırma dosyası oluşturma**</span><span class="sxs-lookup"><span data-stu-id="75b6b-178">**Create hello configuration file**</span></span>

 <span data-ttu-id="75b6b-179">Merhaba HPC Pack Iaas dağıtım betiği bir XML yapılandırma dosyasını hello HPC küme altyapısı hello açıklayan giriş olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="75b6b-179">hello HPC Pack IaaS deployment script uses an XML configuration file as input that describes hello infrastructure of hello HPC cluster.</span></span> <span data-ttu-id="75b6b-180">bir baş düğüm ve 18 oluşan bir küme işlem düğümlerini Microsoft Excel içeren hello işlem düğümü görüntüden oluşturulan toodeploy aşağıdaki örnek yapılandırma dosyasına hello ortamınıza değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-180">toodeploy a cluster consisting of a head node and 18 compute nodes created from hello compute node image that includes Microsoft Excel, substitute values for your environment into hello following sample configuration file.</span></span> <span data-ttu-id="75b6b-181">Hello yapılandırma dosyası hakkında daha fazla bilgi için bkz: hello betik klasöründeki hello Manual.rtf dosyasını ve [hello HPC Pack Iaas dağıtım betiği ile bir HPC kümesi oluşturma](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="75b6b-181">For more information about hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="75b6b-182">**Merhaba yapılandırma dosyası ile ilgili notlar**</span><span class="sxs-lookup"><span data-stu-id="75b6b-182">**Notes about hello configuration file**</span></span>

* <span data-ttu-id="75b6b-183">Merhaba **VMName** hello baş düğümü **gerekir** olması hello aynı hello **ServiceName**, veya SOA işleri toorun başarısız.</span><span class="sxs-lookup"><span data-stu-id="75b6b-183">hello **VMName** of hello head node **MUST** be hello same as hello **ServiceName**, or SOA jobs fail toorun.</span></span>
* <span data-ttu-id="75b6b-184">Belirttiğinizden emin olun **EnableWebPortal** hello baş düğümüne sertifika oluşturulan dışarı aktarılır ve böylece.</span><span class="sxs-lookup"><span data-stu-id="75b6b-184">Make sure you specify **EnableWebPortal** so that hello head node certificate is generated and exported.</span></span>
* <span data-ttu-id="75b6b-185">bir yapılandırma sonrası PowerShell komut dosyası hello baş düğüm üzerinde çalışır PostConfig.ps1 Hello dosyayı belirtir.</span><span class="sxs-lookup"><span data-stu-id="75b6b-185">hello file specifies a post-configuration PowerShell script PostConfig.ps1 that runs on hello head node.</span></span> <span data-ttu-id="75b6b-186">Aşağıdaki örnek betik hello hello Azure depolama bağlantı dizesi yapılandırır, hello bilgi işlem düğümü rolü hello baş düğümünden kaldırır ve bunlar dağıtıldığında tüm düğümlerin çevrimiçi duruma getirir.</span><span class="sxs-lookup"><span data-stu-id="75b6b-186">hello following sample script configures hello Azure storage connection string, removes hello compute node role from hello head node, and brings all nodes online when they are deployed.</span></span> 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

<span data-ttu-id="75b6b-187">**Merhaba komut dosyasını çalıştır**</span><span class="sxs-lookup"><span data-stu-id="75b6b-187">**Run hello script**</span></span>

1. <span data-ttu-id="75b6b-188">Merhaba PowerShell konsolunu hello istemci bilgisayarda yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-188">Open hello PowerShell console on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="75b6b-189">Dizin toohello komut dosyası klasörünü Değiştir (Bu örnekte E:\IaaSClusterScript).</span><span class="sxs-lookup"><span data-stu-id="75b6b-189">Change directory toohello script folder (E:\IaaSClusterScript in this example).</span></span>
   
   ```
   cd E:\IaaSClusterScript
   ```
3. <span data-ttu-id="75b6b-190">komutu aşağıdaki hello çalıştırmak toodeploy hello HPC Pack kümesi.</span><span class="sxs-lookup"><span data-stu-id="75b6b-190">toodeploy hello HPC Pack cluster, run hello following command.</span></span> <span data-ttu-id="75b6b-191">Bu örnek hello yapılandırma dosyasının E:\HPCDemoConfig.xml içinde bulunan varsayar.</span><span class="sxs-lookup"><span data-stu-id="75b6b-191">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml.</span></span>
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

<span data-ttu-id="75b6b-192">Merhaba HPC paketi dağıtım betiği süre için çalışır.</span><span class="sxs-lookup"><span data-stu-id="75b6b-192">hello HPC Pack deployment script runs for some time.</span></span> <span data-ttu-id="75b6b-193">Bir şey hello komut dosyasının yaptığını tooexport ve hello küme sertifikayı indirin ve hello geçerli kullanıcının Belgeler klasöründe hello istemci bilgisayara kaydedin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-193">One thing hello script does is tooexport and download hello cluster certificate and save it in hello current user’s Documents folder on hello client computer.</span></span> <span data-ttu-id="75b6b-194">ileti benzer toohello aşağıdaki Hello komut dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="75b6b-194">hello script generates a message similar toohello following.</span></span> <span data-ttu-id="75b6b-195">Aşağıdaki adımda, hello sertifikasını hello uygun sertifika deposuna aktarın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-195">In a following step, you import hello certificate in hello appropriate certificate store.</span></span>    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a><span data-ttu-id="75b6b-196">2. Adım</span><span class="sxs-lookup"><span data-stu-id="75b6b-196">Step 2.</span></span> <span data-ttu-id="75b6b-197">Excel çalışma kitaplarını boşaltması ve bir şirket içi istemciden UDF'ler çalıştırın</span><span class="sxs-lookup"><span data-stu-id="75b6b-197">Offload Excel workbooks and run UDFs from an on-premises client</span></span>
### <a name="excel-activation"></a><span data-ttu-id="75b6b-198">Excel etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="75b6b-198">Excel activation</span></span>
<span data-ttu-id="75b6b-199">Merhaba ComputeNodeWithExcel VM görüntüsü üretim iş yükleri için kullanılırken, tooprovide bir geçerli Microsoft Office lisans anahtar tooactivate Excel hello işlem düğümlerinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="75b6b-199">When using hello ComputeNodeWithExcel VM image for production workloads, you need tooprovide a valid Microsoft Office license key tooactivate Excel on hello compute nodes.</span></span> <span data-ttu-id="75b6b-200">Aksi takdirde Excel hello Değerlendirme sürümü 30 gün sonra süresi dolar ve Excel çalışma kitaplarını çalıştıran hello COMException (0x800AC472) ile başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="75b6b-200">Otherwise, hello evaluation version of Excel expires after 30 days, and running Excel workbooks will fail with hello COMException (0x800AC472).</span></span> 

<span data-ttu-id="75b6b-201">Excel başka bir sonraki 30 gün için değerlendirme süresi rearm: toohello baş düğüm ve clusrun oturum `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` tüm Excel işlem düğümleri aracılığıyla HPC Küme Yöneticisi.</span><span class="sxs-lookup"><span data-stu-id="75b6b-201">You can rearm Excel for another 30 days of evaluation time: Log on toohello head node and clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` on all Excel compute nodes via HPC Cluster Manager.</span></span> <span data-ttu-id="75b6b-202">En fazla iki kez yeniden etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-202">You can rearm a maximum of two times.</span></span> <span data-ttu-id="75b6b-203">Bundan sonra geçerli bir Office lisans anahtarı sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="75b6b-203">After that, you must provide a valid Office license key.</span></span>

<span data-ttu-id="75b6b-204">Merhaba Office Professional Plus 2013 hello VM görüntüsü üzerinde yüklü bir birim bir genel toplu lisans anahtarı (GVLK) ile sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="75b6b-204">hello Office Professional Plus 2013 installed on hello VM image is a volume edition with a Generic Volume License Key (GVLK).</span></span> <span data-ttu-id="75b6b-205">Anahtar Yönetim Hizmeti (KMS) aracılığıyla etkinleştirebilir / etkinleştirmeyi (AD BA) veya çoklu etkinleştirme anahtarı (MAK).</span><span class="sxs-lookup"><span data-stu-id="75b6b-205">You can activate it via Key Management Service (KMS)/Active Directory-Based Activation (AD-BA) or Multiple Activation Key (MAK).</span></span> 

    * <span data-ttu-id="75b6b-206">toouse KMS/AD-BA, var olan bir KMS sunucusu kullanın veya yeni bir Microsoft Office 2013 toplu lisans paketi hello kullanarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-206">toouse KMS/AD-BA, use an existing KMS server or set up a new one by using hello Microsoft Office 2013 Volume License Pack.</span></span> <span data-ttu-id="75b6b-207">(İstiyorsanız, hello baş düğüm hello sunucuda ayarlayın.) Ardından hello KMS ana bilgisayar anahtarı hello Internet üzerinden veya telefonla etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-207">(If you want to, set up hello server on hello head node.) Then, activate hello KMS host key via hello Internet or telephone.</span></span> <span data-ttu-id="75b6b-208">Ardından clusrun `ospp.vbs` tooset KMS sunucusunu ve bağlantı noktası hello ve tüm hello Excel işlem düğümlerinde Office etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-208">Then clusrun `ospp.vbs` tooset hello KMS server and port and activate Office on all hello Excel compute nodes.</span></span> 

    * <span data-ttu-id="75b6b-209">MAK, ilk clusrun toouse `ospp.vbs` tooinput hello anahtarı ve tüm hello Excel işlem düğümlerini hello Internet veya telefon aracılığıyla etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-209">toouse MAK, first clusrun `ospp.vbs` tooinput hello key and then activate all hello Excel compute nodes via hello Internet or telephone.</span></span> 

> [!NOTE]
> <span data-ttu-id="75b6b-210">Office Professional Plus 2013 için perakende ürün anahtarlarını bu VM görüntüsü ile kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="75b6b-210">Retail product keys for Office Professional Plus 2013 cannot be used with this VM image.</span></span> <span data-ttu-id="75b6b-211">Geçerli anahtarlar ve Office veya Excel sürümü bu Office Professional Plus 2013 toplu edition dışında bir yükleme medyası varsa, bunun yerine kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75b6b-211">If you have valid keys and installation media for Office or Excel editions other than this Office Professional Plus 2013 volume edition, you can use them instead.</span></span> <span data-ttu-id="75b6b-212">Önce bu birimin sürümü kaldırın ve sahip hello sürümü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-212">First uninstall this volume edition and install hello edition that you have.</span></span> <span data-ttu-id="75b6b-213">Merhaba, özelleştirilmiş bir VM görüntüsü toouse bir dağıtımda ölçekli olarak işlem düğümü yakalanabilir Excel yeniden.</span><span class="sxs-lookup"><span data-stu-id="75b6b-213">hello reinstalled Excel compute node can be captured as a customized VM image toouse in a deployment at scale.</span></span>
> 
> 

### <a name="offload-excel-workbooks"></a><span data-ttu-id="75b6b-214">Excel çalışma kitaplarını boşaltma</span><span class="sxs-lookup"><span data-stu-id="75b6b-214">Offload Excel workbooks</span></span>
<span data-ttu-id="75b6b-215">Azure'da hello HPC Pack kümesinde çalışır, bu adımları toooffload bir Excel çalışma kitabı izleyin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-215">Follow these steps toooffload an Excel workbook so that it runs on hello HPC Pack cluster in Azure.</span></span> <span data-ttu-id="75b6b-216">toodo Bu, Excel 2010 veya 2013 hello istemci bilgisayarda zaten yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="75b6b-216">toodo this, you must have Excel 2010 or 2013 already installed on hello client computer.</span></span>

1. <span data-ttu-id="75b6b-217">İşlem düğümü görüntü 1. adım toodeploy hello Excel ile bir HPC Pack kümesi hello seçeneklerinde birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-217">Use one of hello options in Step 1 toodeploy an HPC Pack cluster with hello Excel compute node image.</span></span> <span data-ttu-id="75b6b-218">Merhaba küme sertifika dosyasını (.cer) ve küme kullanıcı adı ve parola edinin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-218">Obtain hello cluster certificate file (.cer) and cluster username and password.</span></span>
2. <span data-ttu-id="75b6b-219">Merhaba istemci bilgisayarda Cert: \CurrentUser\Root altında hello küme sertifikasını içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-219">On hello client computer, import hello cluster certificate under Cert:\CurrentUser\Root.</span></span>
3. <span data-ttu-id="75b6b-220">Excel yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="75b6b-220">Make sure Excel is installed.</span></span> <span data-ttu-id="75b6b-221">Merhaba içeriğine aşağıdaki hello ile Excel.exe.config dosyası oluşturmak Excel.exe aynı klasöre hello istemci bilgisayarda.</span><span class="sxs-lookup"><span data-stu-id="75b6b-221">Create an Excel.exe.config file with hello following contents in hello same folder as Excel.exe on hello client computer.</span></span> <span data-ttu-id="75b6b-222">Bu adım, bu hello HPC Pack 2012 R2 Excel COM eklentisi başarıyla yükleyen sağlar.</span><span class="sxs-lookup"><span data-stu-id="75b6b-222">This step ensures that hello HPC Pack 2012 R2 Excel COM add-in loads successfully.</span></span>
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. <span data-ttu-id="75b6b-223">Merhaba istemci toosubmit işleri toohello HPC Pack kümesi.</span><span class="sxs-lookup"><span data-stu-id="75b6b-223">Set up hello client toosubmit jobs toohello HPC Pack cluster.</span></span> <span data-ttu-id="75b6b-224">Bir seçenektir toodownload hello tam [HPC Pack 2012 R2 güncelleştirme 3'ü yükleme](http://www.microsoft.com/download/details.aspx?id=49922) ve hello HPC Pack istemcisini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-224">One option is toodownload hello full [HPC Pack 2012 R2 Update 3 installation](http://www.microsoft.com/download/details.aspx?id=49922) and install hello HPC Pack client.</span></span> <span data-ttu-id="75b6b-225">Alternatif olarak, karşıdan yüklenip hello [HPC Pack 2012 R2 güncelleştirme 3 istemci yardımcı programları](https://www.microsoft.com/download/details.aspx?id=49923) ve uygun Visual C++ 2010 bilgisayarınızı yeniden dağıtılabilir hello ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span><span class="sxs-lookup"><span data-stu-id="75b6b-225">Alternatively, download and install hello [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923) and hello appropriate Visual C++ 2010 redistributable for your computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span></span>
5. <span data-ttu-id="75b6b-226">Bu örnekte, ConvertiblePricing_Complete.xlsb adlandırılmış bir örnek Excel çalışma kitabı kullanırız.</span><span class="sxs-lookup"><span data-stu-id="75b6b-226">In this example, we use a sample Excel workbook named ConvertiblePricing_Complete.xlsb.</span></span> <span data-ttu-id="75b6b-227">Karşıdan yükleyebileceğiniz [burada](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span><span class="sxs-lookup"><span data-stu-id="75b6b-227">You can download it [here](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span></span>
6. <span data-ttu-id="75b6b-228">Merhaba Excel çalışma kitabı tooa çalışma klasörü D:\Excel\Run gibi kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-228">Copy hello Excel workbook tooa working folder such as D:\Excel\Run.</span></span>
7. <span data-ttu-id="75b6b-229">Merhaba Excel çalışma kitabı açın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-229">Open hello Excel workbook.</span></span> <span data-ttu-id="75b6b-230">Merhaba üzerinde **geliştirme** Şerit, tıklatın **COM eklentileri** ve o hello HPC Pack Excel COM eklentisi başarıyla yüklendi onaylayın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-230">On hello **Develop** ribbon, click **COM Add-Ins** and confirm that hello HPC Pack Excel COM add-in is loaded successfully.</span></span>
   
   ![HPC Pack eklentisi excel][addin]
8. <span data-ttu-id="75b6b-232">Düzen hello VBA makrosu'hello değiştirerek Excel'de HPCControlMacros satırları hello betik aşağıdaki gösterildiği gibi açıklamalı.</span><span class="sxs-lookup"><span data-stu-id="75b6b-232">Edit hello VBA macro HPCControlMacros in Excel by changing hello commented lines as shown in hello following script.</span></span> <span data-ttu-id="75b6b-233">Ortamınız için uygun değerleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-233">Substitute appropriate values for your environment.</span></span>
   
   ![HPC Pack için Excel makrosu][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. <span data-ttu-id="75b6b-235">Merhaba Excel çalışma kitabı tooan karşıya yükleme dizini D:\Excel\Upload gibi kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-235">Copy hello Excel workbook tooan upload directory such as D:\Excel\Upload.</span></span> <span data-ttu-id="75b6b-236">Bu dizin hello VBA makrosu hello HPC_DependsFiles sabiti belirtildi.</span><span class="sxs-lookup"><span data-stu-id="75b6b-236">This directory is specified in hello HPC_DependsFiles constant in hello VBA macro.</span></span>
10. <span data-ttu-id="75b6b-237">toorun hello çalışma kitabı, azure'da hello kümede tıklatın hello **küme** hello çalışma sayfası üzerinde düğmesi.</span><span class="sxs-lookup"><span data-stu-id="75b6b-237">toorun hello workbook on hello cluster in Azure, click hello **Cluster** button on hello worksheet.</span></span>

### <a name="run-excel-udfs"></a><span data-ttu-id="75b6b-238">Excel UDF'leri çalıştırın</span><span class="sxs-lookup"><span data-stu-id="75b6b-238">Run Excel UDFs</span></span>
<span data-ttu-id="75b6b-239">toorun Excel UDF'leri, 1-3'ü tooset hello istemci bilgisayarı hello önceki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-239">toorun Excel UDFs, follow hello preceding steps 1 – 3 tooset up hello client computer.</span></span> <span data-ttu-id="75b6b-240">Excel UDF'leri için işlem düğümlerinde yüklü toohave hello Excel uygulaması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="75b6b-240">For Excel UDFs, you don't need toohave hello Excel application installed on compute nodes.</span></span> <span data-ttu-id="75b6b-241">Düğümler, küme oluşturma işlem zaman seçebilir böylece normal işlem düğümü görüntü hello yerine Excel düğümü görüntüsüyle işlem.</span><span class="sxs-lookup"><span data-stu-id="75b6b-241">So, when creating your cluster compute nodes, you could choose a normal compute node image instead of hello compute node image with Excel.</span></span>

> [!NOTE]
> <span data-ttu-id="75b6b-242">Bir 34 karakter limiti hello Excel 2010 ve 2013 Küme Bağlayıcısı iletişim kutusu yok.</span><span class="sxs-lookup"><span data-stu-id="75b6b-242">There is a 34 character limit in hello Excel 2010 and 2013 cluster connector dialog box.</span></span> <span data-ttu-id="75b6b-243">Merhaba UDF'ler çalıştıran bu iletişim kutusunu toospecify hello kümesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-243">You use this dialog box toospecify hello cluster that runs hello UDFs.</span></span> <span data-ttu-id="75b6b-244">Merhaba tam küme adı uzunsa (örneğin, hpcexcelhn01.southeastasia.cloudapp.azure.com) hello iletişim kutusunda uygun değildir.</span><span class="sxs-lookup"><span data-stu-id="75b6b-244">If hello full cluster name is longer (for example, hpcexcelhn01.southeastasia.cloudapp.azure.com), it does not fit in hello dialog box.</span></span> <span data-ttu-id="75b6b-245">Merhaba geçici çözüm tooset bir makineye gibi değişkendir *CCP_IAASHN* hello uzun küme adı hello değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="75b6b-245">hello workaround is tooset a machine-wide variable such as *CCP_IAASHN* with hello value of hello long cluster name.</span></span> <span data-ttu-id="75b6b-246">Ardından, girin *CCP_IAASHN %* hello iletişim kutusunda hello küme baş düğüm adı.</span><span class="sxs-lookup"><span data-stu-id="75b6b-246">Then, enter *%CCP_IAASHN%* in hello dialog box as hello cluster head node name.</span></span> 
> 
> 

<span data-ttu-id="75b6b-247">Merhaba küme başarıyla dağıtıldıktan sonra aşağıdaki adımları toorun hello ile örnek yerleşik devam Excel UDF.</span><span class="sxs-lookup"><span data-stu-id="75b6b-247">After hello cluster is successfully deployed, continue with hello following steps toorun a sample built-in Excel UDF.</span></span> <span data-ttu-id="75b6b-248">Özelleştirilmiş Excel UDF'leri görmek [kaynakları](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild XLL'ler hello ve bunları hello Iaas kümede dağıtın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-248">For customized Excel UDFs, see these [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild hello XLLs and deploy them on hello IaaS cluster.</span></span>

1. <span data-ttu-id="75b6b-249">Yeni bir Excel çalışma kitabı açın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-249">Open a new Excel workbook.</span></span> <span data-ttu-id="75b6b-250">Merhaba üzerinde **geliştirme** Şerit, tıklatın **eklentileri**. Merhaba iletişim kutusunda, ardından **Gözat**toohello %CCP_HOME%Bin\XLL32 klasörüne gidin ve hello örnek ClusterUDF32.xll seçin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-250">On hello **Develop** ribbon, click **Add-Ins**. Then, in hello dialog box, click **Browse**, navigate toohello %CCP_HOME%Bin\XLL32 folder, and select hello sample ClusterUDF32.xll.</span></span> <span data-ttu-id="75b6b-251">Merhaba ClusterUDF32 hello istemci makinede yoksa, hello baş düğümünde hello %CCP_HOME%Bin\XLL32 klasöründen kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-251">If hello ClusterUDF32 doesn't exist on hello client machine, copy it from hello %CCP_HOME%Bin\XLL32 folder on hello head node.</span></span>
   
   ![Merhaba UDF seçin][udf]
2. <span data-ttu-id="75b6b-253">Tıklatın **dosya** > **seçenekleri** > **Gelişmiş**.</span><span class="sxs-lookup"><span data-stu-id="75b6b-253">Click **File** > **Options** > **Advanced**.</span></span> <span data-ttu-id="75b6b-254">Altında **formüller**, denetleme **XLL işlevleri toorun kullanıcı tanımlı bir işlem kümesi izin**.</span><span class="sxs-lookup"><span data-stu-id="75b6b-254">Under **Formulas**, check **Allow user-defined XLL functions toorun a compute cluster**.</span></span> <span data-ttu-id="75b6b-255">Ardından **seçenekleri** ve hello tam küme adı girin **küme baş düğüm adı**.</span><span class="sxs-lookup"><span data-stu-id="75b6b-255">Then click **Options** and enter hello full cluster name in **Cluster head node name**.</span></span> <span data-ttu-id="75b6b-256">(Bir uzun küme adını değil sığar belirtildiği gibi daha önce bu giriş kutusu sınırlı too34 karakterden oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="75b6b-256">(As noted previously this input box is limited too34 characters, so a long cluster name may not fit.</span></span> <span data-ttu-id="75b6b-257">"Bir makineye değişken uzun küme adı için kullanabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="75b6b-257">You may use a machine-wide variable here for a long cluster name.)</span></span>
   
   ![Merhaba UDF yapılandırın][options]
3. <span data-ttu-id="75b6b-259">toorun hello hello kümede UDF Hesaplama değeri =XllGetComputerNameC() ile Merhaba hücreyi tıklatın ve Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-259">toorun hello UDF calculation on hello cluster, click hello cell with value =XllGetComputerNameC() and press Enter.</span></span> <span data-ttu-id="75b6b-260">Hello işlevi yalnızca hello işlem düğümü üzerinde hangi hello UDF çalıştıran hello adını alır.</span><span class="sxs-lookup"><span data-stu-id="75b6b-260">hello function simply retrieves hello name of hello compute node on which hello UDF runs.</span></span> <span data-ttu-id="75b6b-261">İlk çalıştırma Merhaba hello kullanıcı adı ve parola tooconnect toohello Iaas küme için bir kimlik bilgileri iletişim kutusu ister.</span><span class="sxs-lookup"><span data-stu-id="75b6b-261">For hello first run, a credentials dialog box prompts for hello username and password tooconnect toohello IaaS cluster.</span></span>
   
   ![UDF çalıştırın][run]
   
   <span data-ttu-id="75b6b-263">Çok sayıda hücre toocalculate olduğunda Alt Shift Ctrl + F9 toorun hello hesaplama tüm hücreleri tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-263">When there are many cells toocalculate, press Alt-Shift-Ctrl + F9 toorun hello calculation on all cells.</span></span>

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a><span data-ttu-id="75b6b-264">3. Adım</span><span class="sxs-lookup"><span data-stu-id="75b6b-264">Step 3.</span></span> <span data-ttu-id="75b6b-265">Bir şirket içi istemciden bir SOA iş yükü çalıştırın</span><span class="sxs-lookup"><span data-stu-id="75b6b-265">Run a SOA workload from an on-premises client</span></span>
<span data-ttu-id="75b6b-266">toorun genel SOA uygulamaları hello HPC Pack Iaas kümede ilk yöntemlerden birini kullanın hello 1. adım toodeploy hello kümede.</span><span class="sxs-lookup"><span data-stu-id="75b6b-266">toorun general SOA applications on hello HPC Pack IaaS cluster, first use one of hello methods in Step 1 toodeploy hello cluster.</span></span> <span data-ttu-id="75b6b-267">Merhaba işlem düğümlerinde Excel gerekmediği için bir genel işlem düğümü görüntüsü bu durumda, belirtin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-267">Specify a generic compute node image in this case, because you do not need Excel on hello compute nodes.</span></span> <span data-ttu-id="75b6b-268">Ardından aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-268">Then follow these steps.</span></span>

1. <span data-ttu-id="75b6b-269">Merhaba küme sertifikası aldıktan sonra onu Cert: \CurrentUser\Root altında hello istemci bilgisayarda içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-269">After retrieving hello cluster certificate, import it on hello client computer under Cert:\CurrentUser\Root.</span></span>
2. <span data-ttu-id="75b6b-270">Merhaba yüklemek [HPC Pack 2012 R2 güncelleştirme 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) ve [HPC Pack 2012 R2 güncelleştirme 3 istemci yardımcı programları](https://www.microsoft.com/download/details.aspx?id=49923).</span><span class="sxs-lookup"><span data-stu-id="75b6b-270">Install hello [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) and [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923).</span></span> <span data-ttu-id="75b6b-271">Bu araçları toodevelop etkinleştirin ve SOA istemci uygulamaları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-271">These tools enable you toodevelop and run SOA client applications.</span></span>
3. <span data-ttu-id="75b6b-272">Merhaba HelloWorldR2 karşıdan [örnek koduna](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="75b6b-272">Download hello HelloWorldR2 [sample code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span> <span data-ttu-id="75b6b-273">Merhaba HelloWorldR2.sln Visual Studio 2010 veya 2012 açın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-273">Open hello HelloWorldR2.sln in Visual Studio 2010 or 2012.</span></span> <span data-ttu-id="75b6b-274">(Bu örnek, Visual Studio'nun daha yeni sürümleri ile şu anda uyumlu değildir.)</span><span class="sxs-lookup"><span data-stu-id="75b6b-274">(This sample is not currently compatible with more recent versions of Visual Studio.)</span></span>
4. <span data-ttu-id="75b6b-275">Merhaba EchoService projeyi önce oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75b6b-275">Build hello EchoService project first.</span></span> <span data-ttu-id="75b6b-276">Ardından, hello hizmeti toohello Iaas kümesini dağıtma hello tooan dağıttığınız şekilde küme içi.</span><span class="sxs-lookup"><span data-stu-id="75b6b-276">Then, deploy hello service toohello IaaS cluster in hello same way you deploy tooan on-premises cluster.</span></span> <span data-ttu-id="75b6b-277">Ayrıntılı adımlar için hello HelloWordR2 Benioku.doc bakın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-277">For detailed steps, see hello Readme.doc in HelloWordR2.</span></span> <span data-ttu-id="75b6b-278">Değiştirebilir ve bir Azure Iaas kümede çalışan bölüm toogenerate hello SOA istemci uygulamaları aşağıdaki hello açıklandığı gibi hello HellWorldR2 ve diğer projeler derleme.</span><span class="sxs-lookup"><span data-stu-id="75b6b-278">Modify and build hello HellWorldR2 and other projects as described in hello following section toogenerate hello SOA client applications that run on an Azure IaaS cluster.</span></span>

### <a name="use-http-binding-with-azure-storage-queue"></a><span data-ttu-id="75b6b-279">HTTP bağlaması ile Azure depolama kuyruğu kullanın</span><span class="sxs-lookup"><span data-stu-id="75b6b-279">Use Http binding with Azure storage queue</span></span>
<span data-ttu-id="75b6b-280">bir Azure depolama kuyruğu ile toouse Http bağlama toohello örnek kod birkaç değişiklik yapın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-280">toouse Http binding with an Azure storage queue, make a few changes toohello sample code.</span></span>

* <span data-ttu-id="75b6b-281">Merhaba küme adını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="75b6b-281">Update hello cluster name.</span></span>
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* <span data-ttu-id="75b6b-282">İsteğe bağlı olarak, SessionStartInfo içinde hello varsayılan TransportScheme kullanın veya açıkça tooHttp ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-282">Optionally, use hello default TransportScheme in SessionStartInfo or explicitly set it tooHttp.</span></span>

```
    info.TransportScheme = TransportScheme.Http;
```

* <span data-ttu-id="75b6b-283">Varsayılan bağlama BrokerClient hello için kullanın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-283">Use default binding for hello BrokerClient.</span></span>
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    <span data-ttu-id="75b6b-284">Veya açıkça hello basicHttpBinding kullanarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-284">Or set explicitly using hello basicHttpBinding.</span></span>
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* <span data-ttu-id="75b6b-285">İsteğe bağlı olarak, hello UseAzureQueue bayrağı tootrue SessionStartInfo ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-285">Optionally, set hello UseAzureQueue flag tootrue in SessionStartInfo.</span></span> <span data-ttu-id="75b6b-286">Aksi durumda kümesi, bu tootrue varsayılan olarak Azure etki alanı sonekleri hello küme adına sahip ve hello TransportScheme Http olduğunda ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="75b6b-286">If not set, it will be set tootrue by default when hello cluster name has Azure domain suffixes and hello TransportScheme is Http.</span></span>
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a><span data-ttu-id="75b6b-287">Azure depolama kuyruğu olmadan HTTP bağlaması kullanın</span><span class="sxs-lookup"><span data-stu-id="75b6b-287">Use Http binding without Azure storage queue</span></span>
<span data-ttu-id="75b6b-288">bir Azure depolama kuyruğu, açıkça kümesi hello UseAzureQueue bayrağı toofalse hello SessionStartInfo içinde olmadan toouse Http bağlama.</span><span class="sxs-lookup"><span data-stu-id="75b6b-288">toouse Http binding without an Azure storage queue, explicitly set hello UseAzureQueue flag toofalse in hello SessionStartInfo.</span></span>

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a><span data-ttu-id="75b6b-289">NetTcp bağlama kullanın</span><span class="sxs-lookup"><span data-stu-id="75b6b-289">Use NetTcp binding</span></span>
<span data-ttu-id="75b6b-290">toouse NetTcp bağlama, hello benzer tooconnecting tooan şirket içi küme yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="75b6b-290">toouse NetTcp binding, hello configuration is similar tooconnecting tooan on-premises cluster.</span></span> <span data-ttu-id="75b6b-291">Merhaba baş düğüm VM üzerindeki birkaç uç noktaları tooopen gerekir.</span><span class="sxs-lookup"><span data-stu-id="75b6b-291">You need tooopen a few endpoints on hello head node VM.</span></span> <span data-ttu-id="75b6b-292">Örneğin, hello HPC Pack Iaas dağıtım komut dosyası toocreate hello küme kullandıysanız, Azure portalında şu şekilde kümesi hello uç noktalarını hello.</span><span class="sxs-lookup"><span data-stu-id="75b6b-292">If you used hello HPC Pack IaaS deployment script toocreate hello cluster, for example, set hello endpoints in hello Azure portal as follows.</span></span>

1. <span data-ttu-id="75b6b-293">Merhaba VM durdurun.</span><span class="sxs-lookup"><span data-stu-id="75b6b-293">Stop hello VM.</span></span>
2. <span data-ttu-id="75b6b-294">Merhaba TCP bağlantı noktaları 9090, 9087, ekleme 9091, 9094 hello oturumu için Aracısı, alt ve Veri Hizmetleri, sırasıyla Aracısı</span><span class="sxs-lookup"><span data-stu-id="75b6b-294">Add hello TCP ports 9090, 9087, 9091, 9094 for hello Session, Broker, Broker worker, and Data services, respectively</span></span>
   
    ![Uç noktaları yapılandırma][endpoint-new-portal]
3. <span data-ttu-id="75b6b-296">Merhaba VM başlatın.</span><span class="sxs-lookup"><span data-stu-id="75b6b-296">Start hello VM.</span></span>

<span data-ttu-id="75b6b-297">Merhaba SOA istemci uygulaması hello baş toohello Iaas küme tam adı değiştirme dışında herhangi bir değişiklik gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="75b6b-297">hello SOA client application requires no changes except altering hello head name toohello IaaS cluster full name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75b6b-298">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="75b6b-298">Next steps</span></span>
* <span data-ttu-id="75b6b-299">Bkz: [bu kaynakları](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) Excel iş yükleri HPC paketi ile çalıştırma hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="75b6b-299">See [these resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) for more information about running Excel workloads with HPC Pack.</span></span>
* <span data-ttu-id="75b6b-300">Bkz: [SOA Hizmetleri'nde yönetme Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) dağıtma ve SOA Hizmetleri HPC paketi ile yönetme hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="75b6b-300">See [Managing SOA Services in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) for more about deploying and managing SOA services with HPC Pack.</span></span>

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png
