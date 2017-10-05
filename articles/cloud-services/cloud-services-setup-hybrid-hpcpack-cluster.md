---
title: "Azure karma HPC Pack kümedeki ayarlamak | Microsoft Docs"
description: "Küçük bir, karma yüksek performanslı bilgi işlem (HPC) küme ayarlamak için Microsoft HPC Pack ve Azure kullanmayı öğrenin"
services: cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: hpc-pack
ms.assetid: 
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: f6dc9657e64160be1e68a7356863b53131e9b3c3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a><span data-ttu-id="e6666-103">Bir karma yüksek performanslı bilgi işlem (HPC) küme Microsoft HPC Pack ve isteğe bağlı Azure işlem düğümleri ile ayarlama</span><span class="sxs-lookup"><span data-stu-id="e6666-103">Set up a hybrid high performance computing (HPC) cluster with Microsoft HPC Pack and on-demand Azure compute nodes</span></span>
<span data-ttu-id="e6666-104">Microsoft HPC Pack 2012 R2 ve Azure (HPC) küme bir küçük, karma yüksek performanslı bilgi işlem ayarlamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6666-104">Use Microsoft HPC Pack 2012 R2 and Azure to set up a small, hybrid high performance computing (HPC) cluster.</span></span> <span data-ttu-id="e6666-105">Bu makalede gösterilen küme bir şirket içi HPC Pack baş düğümüne oluşur ve bazı düğümler isteğe bağlı bir azure'da dağıtmak bulut hizmeti işlem.</span><span class="sxs-lookup"><span data-stu-id="e6666-105">The cluster shown in this article consists of an on-premises HPC Pack head node and some compute nodes you deploy on-demand in an Azure cloud service.</span></span> <span data-ttu-id="e6666-106">Karma küme üzerinde işlem işleri sonra çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6666-106">You can then run compute jobs on the hybrid cluster.</span></span>

![Karma HPC Kümesi][Overview] 

<span data-ttu-id="e6666-108">Bu öğretici bir yaklaşım, küme "bulut için veri bloğu" olarak da adlandırılan gösterir yoğun uygulamaları çalıştırmak için ölçeklenebilir, isteğe bağlı Azure kaynaklarını kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="e6666-108">This tutorial shows one approach, sometimes called cluster "burst to the cloud," to use scalable, on-demand Azure resources to run compute-intensive applications.</span></span>

<span data-ttu-id="e6666-109">Bu öğretici hesaplama kümeleri veya HPC paketi ile konusunda deneyim varsayar.</span><span class="sxs-lookup"><span data-stu-id="e6666-109">This tutorial assumes no prior experience with compute clusters or HPC Pack.</span></span> <span data-ttu-id="e6666-110">Yalnızca tanıtım amacıyla hızla karma işlem kümesi dağıtmanıza yardımcı olmak için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e6666-110">It is intended only to help you deploy a hybrid compute cluster quickly for demonstration purposes.</span></span> <span data-ttu-id="e6666-111">Değerlendirmeler ve adımlar bir karma HPC Pack devretme büyük ölçekli bir üretim ortamında dağıtmak veya HPC Pack 2016 kullanmak için bkz: [ayrıntılı yönergeler](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="e6666-111">For considerations and steps to deploy a hybrid HPC Pack cluster at greater scale in a production environment, or to use HPC Pack 2016, see the [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span> <span data-ttu-id="e6666-112">HPC paketi ile diğer senaryolar için Azure sanal makineleri küme dağıtımında otomatik dahil olmak üzere, bkz: [azure'da Microsoft HPC paketi ile HPC küme seçenekleri](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e6666-112">For other scenarios with HPC Pack, including automated cluster deployment in Azure virtual machines, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6666-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e6666-113">Prerequisites</span></span>
* <span data-ttu-id="e6666-114">**Azure aboneliği** -bir Azure aboneliğiniz yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="e6666-114">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>
* <span data-ttu-id="e6666-115">**Windows Server 2012 R2 veya Windows Server 2012 çalıştıran bir şirket içi bilgisayar** -HPC küme baş düğümü olarak bu bilgisayarı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6666-115">**An on-premises computer running Windows Server 2012 R2 or Windows Server 2012** - Use this computer as the head node of the HPC cluster.</span></span> <span data-ttu-id="e6666-116">Windows Server zaten çalıştırmıyor değilse, yükleme indirin ve bir [Değerlendirme sürümü](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span><span class="sxs-lookup"><span data-stu-id="e6666-116">If you aren't already running Windows Server, you can download and install an [evaluation version](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span></span>
  
  * <span data-ttu-id="e6666-117">Bilgisayar bir Active Directory etki alanına katılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6666-117">The computer must be joined to an Active Directory domain.</span></span> <span data-ttu-id="e6666-118">Test amaçları için baş düğümü bilgisayarının bir etki alanı denetleyicisi olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6666-118">For test purposes, you can configure the head node computer as a domain controller.</span></span> <span data-ttu-id="e6666-119">Baş düğüm bilgisayarı bir etki alanı denetleyicisi olarak Yükselt ve Active Directory etki alanı Hizmetleri sunucu rolü eklemek için Windows Server belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="e6666-119">To add the Active Directory Domain Services server role and promote the head node computer as a domain controller, see the documentation for Windows Server.</span></span>
  * <span data-ttu-id="e6666-120">HPC Pack desteklemek için işletim sisteminin bu dillerden birinde yüklenmelidir: İngilizce, Japonca veya Çince (Basitleştirilmiş).</span><span class="sxs-lookup"><span data-stu-id="e6666-120">To support HPC Pack, the operating system must be installed in one of these languages: English, Japanese, or Chinese (Simplified).</span></span>
  * <span data-ttu-id="e6666-121">Önemli ve kritik güncelleştirmelerin yüklü olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e6666-121">Verify that important and critical updates are installed.</span></span>
* <span data-ttu-id="e6666-122">**HPC Pack 2012 R2** - [karşıdan](http://go.microsoft.com/fwlink/p/?linkid=328024) yükleme paketini en son sürüm için ücretsiz ve dosyaları baş düğüm bilgisayara kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="e6666-122">**HPC Pack 2012 R2** - [Download](http://go.microsoft.com/fwlink/p/?linkid=328024) the installation package for the latest version free of charge and copy the files to the head node computer.</span></span> <span data-ttu-id="e6666-123">Windows Server yüklemenizin aynı dilde yükleme dosyalarını seçin.</span><span class="sxs-lookup"><span data-stu-id="e6666-123">Choose installation files in the same language as your installation of Windows Server.</span></span>

    >[!NOTE]
    > <span data-ttu-id="e6666-124">HPC Pack 2016 HPC Pack 2012 R2 yerine kullanmak istediğiniz ek yapılandırma gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="e6666-124">If you want to use HPC Pack 2016 instead of HPC Pack 2012 R2, additional configuration is needed.</span></span> <span data-ttu-id="e6666-125">Bkz: [ayrıntılı yönergeler](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="e6666-125">See the [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
    > 
* <span data-ttu-id="e6666-126">**Etki alanı hesabı** -bu hesap HPC paketini yüklemek için yerel yönetici izinleri ile baş düğüm yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6666-126">**Domain account** - This account must be configured with local Administrator permissions on the head node to install HPC Pack.</span></span>
* <span data-ttu-id="e6666-127">**TCP bağlantı noktası 443 üzerinden** Azure baş düğümünden.</span><span class="sxs-lookup"><span data-stu-id="e6666-127">**TCP connectivity on port 443** from the head node to Azure.</span></span>

## <a name="install-hpc-pack-on-the-head-node"></a><span data-ttu-id="e6666-128">HPC Pack baş düğümüne yükleyin</span><span class="sxs-lookup"><span data-stu-id="e6666-128">Install HPC Pack on the head node</span></span>
<span data-ttu-id="e6666-129">Microsoft HPC Pack ilk Windows Server çalıştıran şirket içi bilgisayarınıza yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e6666-129">You first install Microsoft HPC Pack on your on-premises computer running Windows Server.</span></span> <span data-ttu-id="e6666-130">Bu bilgisayar kümenin baş düğümüne haline gelir.</span><span class="sxs-lookup"><span data-stu-id="e6666-130">This computer becomes the head node of the cluster.</span></span>

1. <span data-ttu-id="e6666-131">Baş düğümünde yerel yönetici izinlerine sahip bir etki alanı hesabı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e6666-131">Log on to the head node by using a domain account that has local Administrator permissions.</span></span>

2. <span data-ttu-id="e6666-132">HPC Pack yükleme dosyalarından Setup.exe çalıştırarak HPC Pack Yükleme Sihirbazı'nı başlatın.</span><span class="sxs-lookup"><span data-stu-id="e6666-132">Start the HPC Pack Installation Wizard by running Setup.exe from the HPC Pack installation files.</span></span>

3. <span data-ttu-id="e6666-133">Üzerinde **HPC Pack 2012 R2 Kurulum** ekranında **yeni yükleme veya mevcut bir yüklemeye yeni özelliklere**.</span><span class="sxs-lookup"><span data-stu-id="e6666-133">On the **HPC Pack 2012 R2 Setup** screen, click **New installation or add new features to an existing installation**.</span></span>

    ![HPC Pack 2012 Kurulumu][install_hpc1]

4. <span data-ttu-id="e6666-135">Üzerinde **Microsoft yazılım kullanıcı Sözleşmesi sayfası**, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e6666-135">On the **Microsoft Software User Agreement page**, click **Next**.</span></span>

5. <span data-ttu-id="e6666-136">Üzerinde **yükleme türünü seç** sayfasında, **bir baş düğüm oluşturarak yeni bir HPC kümesi oluşturma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e6666-136">On the **Select Installation Type** page, click **Create a new HPC cluster by creating a head node**, and then click **Next**.</span></span>

6. <span data-ttu-id="e6666-137">Sihirbazı çeşitli ön yükleme testleri çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="e6666-137">The wizard runs several pre-installation tests.</span></span> <span data-ttu-id="e6666-138">Tıklatın **sonraki** üzerinde **yükleme kuralları** tüm testleri geçerse sayfa.</span><span class="sxs-lookup"><span data-stu-id="e6666-138">Click **Next** on the **Installation Rules** page if all tests pass.</span></span> <span data-ttu-id="e6666-139">Aksi takdirde, sağlanan bilgileri gözden geçirin ve ortamınızda gerekli değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="e6666-139">Otherwise, review the information provided and make any necessary changes in your environment.</span></span> <span data-ttu-id="e6666-140">Testleri yeniden çalıştırın veya gerekiyorsa Yükleme Sihirbazı'nı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="e6666-140">Then run the tests again or if necessary start the Installation Wizard again.</span></span>
7. <span data-ttu-id="e6666-141">Üzerinde **HPC DB yapılandırma** sayfasında, emin olun **baş düğüm** tüm HPC veritabanları için seçilir ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e6666-141">On the **HPC DB Configuration** page, make sure **Head Node** is selected for all HPC databases, and then click **Next**.</span></span> 

    ![DB yapılandırma][install_hpc4]

8. <span data-ttu-id="e6666-143">Sihirbazın sonraki sayfalarındaki varsayılan seçimleri kabul edin.</span><span class="sxs-lookup"><span data-stu-id="e6666-143">Accept default selections on the remaining pages of the wizard.</span></span> <span data-ttu-id="e6666-144">Üzerinde **gerekli bileşenleri yüklemek** sayfasında, **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="e6666-144">On the **Install Required Components** page, click **Install**.</span></span>
   
    ![Yükleme][install_hpc6]

9. <span data-ttu-id="e6666-146">Yükleme tamamlandıktan sonra işaretini **HPC Küme Yöneticisi'ni başlatın** ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="e6666-146">After the installation completes, uncheck **Start HPC Cluster Manager** and then click **Finish**.</span></span> <span data-ttu-id="e6666-147">(Bir sonraki adımda HPC Küme Yöneticisi'ni başlatın.)</span><span class="sxs-lookup"><span data-stu-id="e6666-147">(You start HPC Cluster Manager in a later step.)</span></span>
   
    ![Son][install_hpc7]

## <a name="prepare-the-azure-subscription"></a><span data-ttu-id="e6666-149">Azure aboneliği hazırlama</span><span class="sxs-lookup"><span data-stu-id="e6666-149">Prepare the Azure subscription</span></span>
<span data-ttu-id="e6666-150">Aşağıdaki adımlarda gerçekleştirmek [Azure portal](https://portal.azure.com) Azure aboneliğinizle.</span><span class="sxs-lookup"><span data-stu-id="e6666-150">Perform the following steps in the [Azure portal](https://portal.azure.com) with your Azure subscription.</span></span> <span data-ttu-id="e6666-151">Bu adımları tamamladıktan sonra şirket içi baş düğümünden Azure düğümleri dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6666-151">After completing these steps, you can deploy Azure nodes from the on-premises head node.</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="e6666-152">Ayrıca, daha sonra ihtiyacınız Azure abonelik Kimliğinizi not edin.</span><span class="sxs-lookup"><span data-stu-id="e6666-152">Also make a note of your Azure subscription ID, which you need later.</span></span> <span data-ttu-id="e6666-153">Kimliğinde Bul **abonelikleri** Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="e6666-153">Find the ID in **Subscriptions** in the portal.</span></span>
  > 

### <a name="upload-the-default-management-certificate"></a><span data-ttu-id="e6666-154">Varsayılan yönetim sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="e6666-154">Upload the default management certificate</span></span>
<span data-ttu-id="e6666-155">HPC Pack kendinden imzalı bir sertifika bir Azure yönetim sertifikası olarak yükleyebileceğiniz varsayılan Microsoft HPC Azure yönetim sertifikası adlı baş düğümüne yükler.</span><span class="sxs-lookup"><span data-stu-id="e6666-155">HPC Pack installs a self-signed certificate on the head node, called the Default Microsoft HPC Azure Management certificate, that you can upload as an Azure management certificate.</span></span> <span data-ttu-id="e6666-156">Bu sertifika için sağlanan baş düğüm ile Azure arasındaki bağlantının güvenli hale getirmek için test etme ve kavram kanıtı dağıtımları.</span><span class="sxs-lookup"><span data-stu-id="e6666-156">This certificate is provided for testing and proof-of-concept deployments to secure the connection between the head node and Azure.</span></span>

1. <span data-ttu-id="e6666-157">Baş düğüm bilgisayardan oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e6666-157">From the head node computer, sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="e6666-158">Tıklatın **abonelikleri** > *your_subscription_name*.</span><span class="sxs-lookup"><span data-stu-id="e6666-158">Click **Subscriptions** > *your_subscription_name*.</span></span>

3. <span data-ttu-id="e6666-159">Tıklatın **yönetim sertifikaları** > **karşıya**.4.</span><span class="sxs-lookup"><span data-stu-id="e6666-159">Click **Management certificates** > **Upload**.4.</span></span> <span data-ttu-id="e6666-160">Baş düğüm dosyası C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer için göz atın.</span><span class="sxs-lookup"><span data-stu-id="e6666-160">Browse on the head node for the file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span></span> <span data-ttu-id="e6666-161">Ardından **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="e6666-161">Then, click **Upload**.</span></span>

   
<span data-ttu-id="e6666-162">**HPC Azure Management'ı varsayılan** sertifika yönetim sertifikaları listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="e6666-162">The **Default HPC Azure Management** certificate appears in the list of management certificates.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="e6666-163">Bir Azure bulut hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6666-163">Create an Azure cloud service</span></span>
> [!NOTE]
> <span data-ttu-id="e6666-164">En iyi performans için aynı coğrafi bölgede bulut hizmetini ve (sonraki adımda) depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e6666-164">For best performance, create the cloud service and the storage account (in a later step) in the same geographic region.</span></span>
> 
> 

1. <span data-ttu-id="e6666-165">Portalı'nda tıklatın **bulut hizmetlerini (Klasik)** > **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e6666-165">In the portal, click **Cloud services (classic)** > **+Add**.</span></span>

2.  <span data-ttu-id="e6666-166">Hizmet için bir DNS adı yazın, bir kaynak grubu ve bir konum seçin ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="e6666-166">Type a DNS name for the service, choose a resource group and a location, and then click **Create**.</span></span>


### <a name="create-an-azure-storage-account"></a><span data-ttu-id="e6666-167">Azure Storage hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6666-167">Create an Azure storage account</span></span>
1. <span data-ttu-id="e6666-168">Portalı'nda tıklatın **depolama hesapları (Klasik)** > **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e6666-168">In the portal, click **Storage accounts (classic)** > **+Add**.</span></span>

2. <span data-ttu-id="e6666-169">Hesap için bir ad yazın ve seçin **Klasik** dağıtım modeli.</span><span class="sxs-lookup"><span data-stu-id="e6666-169">Type a name for the account, and select the **Classic** deployment model.</span></span>

3. <span data-ttu-id="e6666-170">Bir kaynak grubu ve bir konum seçin ve diğer ayarları varsayılan değerlerinde bırakın.</span><span class="sxs-lookup"><span data-stu-id="e6666-170">Choose a resource group and a location, and leave other settings at default values.</span></span> <span data-ttu-id="e6666-171">Sonra **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e6666-171">Then click **Create**.</span></span>

## <a name="configure-the-head-node"></a><span data-ttu-id="e6666-172">Baş düğüm yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e6666-172">Configure the head node</span></span>
<span data-ttu-id="e6666-173">Azure düğümleri dağıtmak ve iş göndermek için HPC Küme Yöneticisi'ni kullanmak için önce bazı gerekli küme yapılandırma adımlarını uygulayın.</span><span class="sxs-lookup"><span data-stu-id="e6666-173">To use HPC Cluster Manager to deploy Azure nodes and to submit jobs, first perform some required cluster configuration steps.</span></span>

1. <span data-ttu-id="e6666-174">Baş düğümünde HPC Küme Yöneticisi'ni başlatın.</span><span class="sxs-lookup"><span data-stu-id="e6666-174">On the head node, start HPC Cluster Manager.</span></span> <span data-ttu-id="e6666-175">Varsa **baş düğüm Seç** iletişim kutusu görüntülenirse, tıklatın **yerel bilgisayar**.</span><span class="sxs-lookup"><span data-stu-id="e6666-175">If the **Select Head Node** dialog box appears, click **Local Computer**.</span></span> <span data-ttu-id="e6666-176">**Dağıtım Yapılacaklar listesi** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e6666-176">The **Deployment To-do List** appears.</span></span>

2. <span data-ttu-id="e6666-177">Altında **gerekli dağıtım görevlerini**, tıklatın **ağınızı yapılandırmak**.</span><span class="sxs-lookup"><span data-stu-id="e6666-177">Under **Required deployment tasks**, click **Configure your network**.</span></span>
   
    ![Ağ yapılandırma][config_hpc2]

3. <span data-ttu-id="e6666-179">Ağ Yapılandırma Sihirbazı'nda seçin **yalnızca bir kurumsal ağ üzerindeki tüm düğümleri** (topoloji 5).</span><span class="sxs-lookup"><span data-stu-id="e6666-179">In the Network Configuration Wizard, select **All nodes only on an enterprise network** (Topology 5).</span></span> <span data-ttu-id="e6666-180">Bu ağ yapılandırması tanıtım amacıyla en kolayıdır.</span><span class="sxs-lookup"><span data-stu-id="e6666-180">This network configuration is the simplest for demonstration purposes.</span></span>
   
    ![Topoloji 5][config_hpc3]
   
4. <span data-ttu-id="e6666-182">Tıklatın **sonraki** Sihirbazı'nın kalan sayfalarındaki varsayılan değerleri kabul etmek için.</span><span class="sxs-lookup"><span data-stu-id="e6666-182">Click **Next** to accept default values on the remaining pages of the wizard.</span></span> <span data-ttu-id="e6666-183">Ardından **gözden geçirme** sekmesini tıklatın, **yapılandırma** ağ yapılandırmasını tamamlamak için.</span><span class="sxs-lookup"><span data-stu-id="e6666-183">Then, on the **Review** tab, click **Configure** to complete the network configuration.</span></span>

5. <span data-ttu-id="e6666-184">İçinde **dağıtım Yapılacaklar listesi**, tıklatın **yükleme kimlik bilgileri sağlamak**.</span><span class="sxs-lookup"><span data-stu-id="e6666-184">In the **Deployment To-do List**, click **Provide installation credentials**.</span></span>

6. <span data-ttu-id="e6666-185">İçinde **yükleme kimlik bilgileri** iletişim kutusunda, HPC paketi yüklemek için kullanılan etki alanı hesabının kimlik bilgilerini yazın.</span><span class="sxs-lookup"><span data-stu-id="e6666-185">In the **Installation Credentials** dialog box, type the credentials of the domain account that you used to install HPC Pack.</span></span> <span data-ttu-id="e6666-186">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e6666-186">Then click **OK**.</span></span> 
   
    ![Yükleme kimlik bilgileri][config_hpc6]
   
7. <span data-ttu-id="e6666-188">İçinde **dağıtım Yapılacaklar listesi**, tıklatın **adlandırma yeni düğümleri yapılandırmak**.</span><span class="sxs-lookup"><span data-stu-id="e6666-188">In the **Deployment To-do List**, click **Configure the naming of new nodes**.</span></span>

8. <span data-ttu-id="e6666-189">İçinde **belirtin düğümü adlandırma serisi** iletişim kutusunda, adlandırma serisi ve'ı tıklatın varsayılanı kabul **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e6666-189">In the **Specify Node Naming Series** dialog box, accept the default naming series and click **OK**.</span></span> <span data-ttu-id="e6666-190">Bu öğreticide eklemek Azure düğümleri otomatik olarak adlandırılmış olsa da bu adımı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="e6666-190">Complete this step even though the Azure nodes you add in this tutorial are named automatically.</span></span>
   
    ![Düğüm adlandırma][config_hpc8]
   
9. <span data-ttu-id="e6666-192">İçinde **dağıtım Yapılacaklar listesi**, tıklatın **düğüm şablonu oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="e6666-192">In the **Deployment To-do List**, click **Create a node template**.</span></span> <span data-ttu-id="e6666-193">Öğreticide daha sonra düğüm şablonu kümesine Azure düğümleri eklemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6666-193">Later in the tutorial, you use the node template to add Azure nodes to the cluster.</span></span>

10. <span data-ttu-id="e6666-194">Oluşturma düğüm Şablonu Sihirbazı'nda, aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="e6666-194">In the Create Node Template Wizard, do the following:</span></span>
    
    <span data-ttu-id="e6666-195">a.</span><span class="sxs-lookup"><span data-stu-id="e6666-195">a.</span></span> <span data-ttu-id="e6666-196">Üzerinde **düğümü şablon türünü seç** sayfasında, **Windows Azure düğüm şablonu**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e6666-196">On the **Choose Node Template Type** page, click **Windows Azure node template**, and then click **Next**.</span></span>
    
    ![Düğüm şablonu][config_hpc10]
    
    <span data-ttu-id="e6666-198">b.</span><span class="sxs-lookup"><span data-stu-id="e6666-198">b.</span></span> <span data-ttu-id="e6666-199">Tıklatın **sonraki** varsayılan şablonu adını kabul etmek için.</span><span class="sxs-lookup"><span data-stu-id="e6666-199">Click **Next** to accept the default template name.</span></span>
    
    <span data-ttu-id="e6666-200">c.</span><span class="sxs-lookup"><span data-stu-id="e6666-200">c.</span></span> <span data-ttu-id="e6666-201">Üzerinde **abonelik bilgilerini gir** sayfasında, Azure abonelik Kimliğinizi (Azure hesap bilgilerinizi kullanılabilir) girin.</span><span class="sxs-lookup"><span data-stu-id="e6666-201">On the **Provide Subscription Information** page, enter your Azure subscription ID (available in your Azure account information).</span></span> <span data-ttu-id="e6666-202">Ardından **yönetim sertifikası**, göz **varsayılan Microsoft HPC Azure yönetimi.**</span><span class="sxs-lookup"><span data-stu-id="e6666-202">Then, in **Management certificate**, browse for **Default Microsoft HPC Azure Management.**</span></span> <span data-ttu-id="e6666-203">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e6666-203">Then click **Next**.</span></span>
    
    ![Düğüm şablonu][config_hpc12]
    
    <span data-ttu-id="e6666-205">d.</span><span class="sxs-lookup"><span data-stu-id="e6666-205">d.</span></span> <span data-ttu-id="e6666-206">Üzerinde **hizmet bilgileri sağlayan** sayfasında, bulut hizmeti ve bir önceki adımda oluşturduğunuz depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="e6666-206">On the **Provide Service Information** page, select the cloud service and the storage account that you created in a previous step.</span></span> <span data-ttu-id="e6666-207">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e6666-207">Then click **Next**.</span></span>
    
    ![Düğüm şablonu][config_hpc13]
    
    <span data-ttu-id="e6666-209">e.</span><span class="sxs-lookup"><span data-stu-id="e6666-209">e.</span></span> <span data-ttu-id="e6666-210">Tıklatın **sonraki** Sihirbazı'nın kalan sayfalarındaki varsayılan değerleri kabul etmek için.</span><span class="sxs-lookup"><span data-stu-id="e6666-210">Click **Next** to accept default values on the remaining pages of the wizard.</span></span> <span data-ttu-id="e6666-211">Ardından **gözden geçirme** sekmesini tıklatın, **oluşturma** düğüm şablonu oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="e6666-211">Then, on the **Review** tab, click **Create** to create the node template.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="e6666-212">Varsayılan olarak, Azure düğüm şablonu HPC Küme Yöneticisi'ni kullanarak (sağlayamaz) başlatmanızı ve düğümler el ile durdurun ayarlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="e6666-212">By default, the Azure node template includes settings for you to start (provision) and stop the nodes manually, using HPC Cluster Manager.</span></span> <span data-ttu-id="e6666-213">İsteğe bağlı olarak Azure düğümleri otomatik olarak durdurmak ve başlatmak için bir zamanlama yapılandırabilir.</span><span class="sxs-lookup"><span data-stu-id="e6666-213">You can optionally configure a schedule to start and stop the Azure nodes automatically.</span></span>
    > 
    > 

## <a name="add-azure-nodes-to-the-cluster"></a><span data-ttu-id="e6666-214">Azure düğümleri kümeye ekleme</span><span class="sxs-lookup"><span data-stu-id="e6666-214">Add Azure nodes to the cluster</span></span>
<span data-ttu-id="e6666-215">Şimdi düğüm şablonu kümesine Azure düğümleri eklemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6666-215">Now use the node template to add Azure nodes to the cluster.</span></span> <span data-ttu-id="e6666-216">Kümenin düğümleri eklemek depolar, yapılandırma bilgilerini (sağlayamaz) başlayabilmeniz için bulut hizmetindeki herhangi bir zamanda bunları.</span><span class="sxs-lookup"><span data-stu-id="e6666-216">Adding the nodes to the cluster stores their configuration information so that you can start (provision) them at any time in the cloud service.</span></span> <span data-ttu-id="e6666-217">Örnekler bulut hizmetinde çalışan sonra aboneliğinizi yalnızca Azure düğümleri için sizden ücret.</span><span class="sxs-lookup"><span data-stu-id="e6666-217">Your subscription only gets charged for Azure nodes after the instances are running in the cloud service.</span></span>

<span data-ttu-id="e6666-218">İki küçük düğümleri eklemek için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="e6666-218">Follow these steps to add two Small nodes.</span></span>

1. <span data-ttu-id="e6666-219">HPC Küme Yöneticisi'nde **düğüm Yönetimi** (adlı **kaynak yönetimi** HPC Pack geçerli sürümlerinde) > **düğüm Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e6666-219">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack) > **Add Node**.</span></span>
   
    ![Düğüm Ekle][add_node1]

2. <span data-ttu-id="e6666-221">Düğüm Ekleme Sihirbazı içinde üzerinde **dağıtım yöntemini seçin** sayfasında, **Ekle Windows Azure düğümleri**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e6666-221">In the Add Node Wizard, on the **Select Deployment Method** page, click **Add Windows Azure nodes**, and then click **Next**.</span></span>
   
    ![Azure düğüm Ekle][add_node1_1]

3. <span data-ttu-id="e6666-223">Üzerinde **belirtin yeni düğümler** sayfasında, daha önce oluşturduğunuz Azure düğüm şablonu seçin (varsayılan olarak adlandırılan **varsayılan AzureNode şablonu**).</span><span class="sxs-lookup"><span data-stu-id="e6666-223">On the **Specify New Nodes** page, select the Azure node template you created previously (called by default **Default AzureNode Template**).</span></span> <span data-ttu-id="e6666-224">Ardından belirtin **2** boyutu düğümlerinin **küçük**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e6666-224">Then specify **2** nodes of size **Small**, and then click **Next**.</span></span>
   
    ![Düğüm belirtin][add_node2]
   
4. <span data-ttu-id="e6666-226">Üzerinde **Düğüm Ekleme Sihirbazı'nı tamamlama** sayfasında, **son**.</span><span class="sxs-lookup"><span data-stu-id="e6666-226">On the **Completing the Add Node Wizard** page, click **Finish**.</span></span>
    
     <span data-ttu-id="e6666-227">Adlı iki Azure düğümleri **AzureCN 0001** ve **AzureCN 0002**, artık HPC Küme Yöneticisi'nde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e6666-227">Two Azure nodes, named **AzureCN-0001** and **AzureCN-0002**, now appear in HPC Cluster Manager.</span></span> <span data-ttu-id="e6666-228">Her ikisi de bulunan **değil dağıtılan** durumu.</span><span class="sxs-lookup"><span data-stu-id="e6666-228">Both are in the **Not-Deployed** state.</span></span>
   
    ![Eklenen düğümlerine][add_node3]

## <a name="start-the-azure-nodes"></a><span data-ttu-id="e6666-230">Azure düğümleri Başlat</span><span class="sxs-lookup"><span data-stu-id="e6666-230">Start the Azure nodes</span></span>
<span data-ttu-id="e6666-231">Azure'da küme kaynaklarını kullanmak istediğinizde (sağlayamaz) Azure düğümleri başlatmak ve çevrimiçi duruma getirmek için HPC Küme Yöneticisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6666-231">When you want to use the cluster resources in Azure, use HPC Cluster Manager to start (provision) the Azure nodes and bring them online.</span></span>

1. <span data-ttu-id="e6666-232">HPC Küme Yöneticisi'nde **düğüm Yönetimi** (adlı **kaynak yönetimi** HPC Pack geçerli sürümlerinde) ve Azure düğümleri seçin.</span><span class="sxs-lookup"><span data-stu-id="e6666-232">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack), and select the Azure nodes.</span></span>

2. <span data-ttu-id="e6666-233">Tıklatın **Başlat**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e6666-233">Click **Start**, and then click **OK**.</span></span>
   
   ![Düğümleri Başlat][add_node4]
   
    <span data-ttu-id="e6666-235">Düğümler için geçiş **sağlama** durumu.</span><span class="sxs-lookup"><span data-stu-id="e6666-235">The nodes transition to the **Provisioning** state.</span></span> <span data-ttu-id="e6666-236">Sağlama ilerleme durumunu izlemek için sağlama günlüğünü görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="e6666-236">View the provisioning log to track the provisioning progress.</span></span>
   
    ![Sağlama düğümler][add_node6]

3. <span data-ttu-id="e6666-238">Birkaç dakika sonra Azure düğümleri sağlama tamamladığınızda ve içinde **çevrimdışı** durumu.</span><span class="sxs-lookup"><span data-stu-id="e6666-238">After a few minutes, the Azure nodes finish provisioning and are in the **Offline** state.</span></span> <span data-ttu-id="e6666-239">Bu durumda, rolü örneklerini çalıştıran ancak henüz küme işlerini kabul edemez.</span><span class="sxs-lookup"><span data-stu-id="e6666-239">In this state, the role instances are running but cannot yet accept cluster jobs.</span></span>

4. <span data-ttu-id="e6666-240">Rol örnekleri, Azure portalında çalıştığını doğrulamak için tıklatın **bulut Hizmetleri (Klasik)** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="e6666-240">To confirm that the role instances are running, in the Azure portal, click **Cloud Services (classic)** > *your_cloud_service_name*.</span></span>
   
   <span data-ttu-id="e6666-241">İki görmelisiniz **HpcWorkerRole** Hizmeti'nde çalışan örnekleri (düğümler).</span><span class="sxs-lookup"><span data-stu-id="e6666-241">You should see two **HpcWorkerRole** instances (nodes) running in the service.</span></span> <span data-ttu-id="e6666-242">HPC Pack ayrıca otomatik olarak dağıtan iki **HpcProxy** baş düğüm ile Azure arasındaki iletişimi işlemek için örnekleri (boyutu Orta).</span><span class="sxs-lookup"><span data-stu-id="e6666-242">HPC Pack also automatically deploys two **HpcProxy** instances (size Medium) to handle communication between the head node and Azure.</span></span>

   ![Çalışan örnekleri][view_instances1]

5. <span data-ttu-id="e6666-244">Küme işlerini çalıştırmak için Azure düğümleri çevrimiçi duruma getirmek için düğüm, sağ tıklatın ve ardından seçin **çevrimiçine**.</span><span class="sxs-lookup"><span data-stu-id="e6666-244">To bring the Azure nodes online to run cluster jobs, select the nodes, right-click, and then click **Bring Online**.</span></span>
   
    ![Çevrimdışı düğümler][add_node7]
   
    <span data-ttu-id="e6666-246">HPC Küme Yöneticisi'ni gösterir düğümleri olduğundan **çevrimiçi** durumu.</span><span class="sxs-lookup"><span data-stu-id="e6666-246">HPC Cluster Manager indicates that the nodes are in the **Online** state.</span></span>

## <a name="run-a-command-across-the-cluster"></a><span data-ttu-id="e6666-247">Küme üzerinde bir komutu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e6666-247">Run a command across the cluster</span></span>
<span data-ttu-id="e6666-248">Yükleme denetimi için HPC Pack kullanın **clusrun** bir komutu veya uygulama bir veya daha fazla küme düğümleri üzerinde çalıştırmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="e6666-248">To check the installation, use the HPC Pack **clusrun** command to run a command or application on one or more cluster nodes.</span></span> <span data-ttu-id="e6666-249">Basit bir örnek olarak kullanın **clusrun** Azure düğümleri IP yapılandırması alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="e6666-249">As a simple example, use **clusrun** to get the IP configuration of the Azure nodes.</span></span>

1. <span data-ttu-id="e6666-250">Baş düğümünde yönetici olarak bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="e6666-250">On the head node, open a command prompt as an administrator.</span></span>

2. <span data-ttu-id="e6666-251">Aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="e6666-251">Type the following command:</span></span>
   
    `clusrun /nodes:azurecn* ipconfig`

3. <span data-ttu-id="e6666-252">İstenirse, Küme Yönetici parolanızı girin.</span><span class="sxs-lookup"><span data-stu-id="e6666-252">If prompted, enter your cluster administrator password.</span></span> <span data-ttu-id="e6666-253">Komut çıktısı şuna benzer görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6666-253">You should see command output similar to the following.</span></span>
   
    ![Clusrun][clusrun1]

## <a name="run-a-test-job"></a><span data-ttu-id="e6666-255">Bir test işini çalıştır</span><span class="sxs-lookup"><span data-stu-id="e6666-255">Run a test job</span></span>
<span data-ttu-id="e6666-256">Şimdi karma kümede çalışan bir test işi gönderin.</span><span class="sxs-lookup"><span data-stu-id="e6666-256">Now submit a test job that runs on the hybrid cluster.</span></span> <span data-ttu-id="e6666-257">Bu, bir basit parametrik tarama işi (doğası gereği Paralel hesaplama türü) örneğidir.</span><span class="sxs-lookup"><span data-stu-id="e6666-257">This example is a simple parametric sweep job (a type of intrinsically parallel computation).</span></span> <span data-ttu-id="e6666-258">Bu örnek bir tamsayı kendisine kullanarak eklemeyi görevleri çalıştırır **/a ayarlamak** komutu.</span><span class="sxs-lookup"><span data-stu-id="e6666-258">This example runs subtasks that add an integer to itself by using the **set /a** command.</span></span> <span data-ttu-id="e6666-259">Kümedeki tüm düğümler için 1'den 100'e tamamlama tamsayılar görevleri katkıda.</span><span class="sxs-lookup"><span data-stu-id="e6666-259">All the nodes in the cluster contribute to finishing the subtasks for integers from 1 to 100.</span></span>

1. <span data-ttu-id="e6666-260">HPC Küme Yöneticisi'nde **iş yönetimi** > **yeni parametrik Sweep işi**.</span><span class="sxs-lookup"><span data-stu-id="e6666-260">In HPC Cluster Manager, click **Job Management** > **New Parametric Sweep Job**.</span></span>
   
    ![Yeni Proje][test_job1]

2. <span data-ttu-id="e6666-262">İçinde **yeni parametrik Sweep işi** iletişim kutusunda **komut satırı**, türü `set /a *+*` (görünür varsayılan komut satırı üzerine).</span><span class="sxs-lookup"><span data-stu-id="e6666-262">In the **New Parametric Sweep Job** dialog box, in **Command line**, type `set /a *+*` (overwriting the default command line that appears).</span></span> <span data-ttu-id="e6666-263">Diğer ayarlar için varsayılan değerleri bırakın ve ardından **gönderme** işi göndermek için.</span><span class="sxs-lookup"><span data-stu-id="e6666-263">Leave default values for the remaining settings, and then click **Submit** to submit the job.</span></span>
   
    ![Parametrik tarama][param_sweep1]

3. <span data-ttu-id="e6666-265">İş tamamlandığında, çift **My Sweep görev** iş.</span><span class="sxs-lookup"><span data-stu-id="e6666-265">When the job is finished, double-click the **My Sweep Task** job.</span></span>

4. <span data-ttu-id="e6666-266">Tıklatın **görünümü görevleri**ve o alt hesaplanan çıktısını görüntülemek için bir alt'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e6666-266">Click **View Tasks**, and then click a subtask to view the calculated output of that subtask.</span></span>
   
    ![Görev sonuçları][view_job361]

5. <span data-ttu-id="e6666-268">Hangi düğümün hesaplama için bu alt gerçekleştirilen görmek için tıklatın **ayrılan düğümler**.</span><span class="sxs-lookup"><span data-stu-id="e6666-268">To see which node performed the calculation for that subtask, click **Allocated Nodes**.</span></span> <span data-ttu-id="e6666-269">(Kümeniz farklı bir düğüme adını gösterebilir.)</span><span class="sxs-lookup"><span data-stu-id="e6666-269">(Your cluster might show a different node name.)</span></span>
   
    ![Görev sonuçları][view_job362]

## <a name="stop-the-azure-nodes"></a><span data-ttu-id="e6666-271">Azure düğümleri Durdur</span><span class="sxs-lookup"><span data-stu-id="e6666-271">Stop the Azure nodes</span></span>
<span data-ttu-id="e6666-272">Küme çalıştıktan sonra hesabınıza gereksiz ücret yazılmaması için Azure düğümleri durdurun.</span><span class="sxs-lookup"><span data-stu-id="e6666-272">After you try out the cluster, stop the Azure nodes to avoid unnecessary charges to your account.</span></span> <span data-ttu-id="e6666-273">Bu adım bulut hizmetini durdurur ve Azure rol örneklerini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="e6666-273">This step stops the cloud service and removes the Azure role instances.</span></span>

1. <span data-ttu-id="e6666-274">HPC Küme Yöneticisi ' nde, **düğüm Yönetimi** (adlı **kaynak yönetimi** HPC Pack önceki sürümlerinde), hem Azure düğümleri seçin.</span><span class="sxs-lookup"><span data-stu-id="e6666-274">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in previous versions of HPC Pack), select both Azure nodes.</span></span> <span data-ttu-id="e6666-275">Ardından **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="e6666-275">Then, click **Stop**.</span></span>
   
    ![Düğümler durdurun][stop_node1]

2. <span data-ttu-id="e6666-277">İçinde **durdurmak Windows Azure düğümleri** iletişim kutusu, tıklatın **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="e6666-277">In the **Stop Windows Azure nodes** dialog box, click **Stop**.</span></span> 
   
3. <span data-ttu-id="e6666-278">Düğümler için geçiş **durdurma** durumu.</span><span class="sxs-lookup"><span data-stu-id="e6666-278">The nodes transition to the **Stopping** state.</span></span> <span data-ttu-id="e6666-279">Birkaç dakika sonra HPC Küme Yöneticisi'ni düğümlerin olduğunu gösterir **değil dağıtılan**.</span><span class="sxs-lookup"><span data-stu-id="e6666-279">After a few minutes, HPC Cluster Manager shows that the nodes are **Not-Deployed**.</span></span>
   
    ![Dağıtılmadı düğümler][stop_node4]

4. <span data-ttu-id="e6666-281">Azure portalında, Azure'da çalışan rolü örnekleri artık olduğunu doğrulamak için tıklatın **bulut hizmetlerini (Klasik)** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="e6666-281">To confirm that the role instances are no longer running in Azure, in the Azure portal, click **Cloud services (classic)** > *your_cloud_service_name*.</span></span> <span data-ttu-id="e6666-282">Hiçbir örneği üretim ortamında dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="e6666-282">No instances are deployed in the production environment.</span></span> 
   
    <span data-ttu-id="e6666-283">Bu öğreticiyi tamamlar.</span><span class="sxs-lookup"><span data-stu-id="e6666-283">This completes the tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6666-284">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e6666-284">Next steps</span></span>
* <span data-ttu-id="e6666-285">Belgelerine keşfedin [HPC Pack](https://technet.microsoft.com/library/cc514029).</span><span class="sxs-lookup"><span data-stu-id="e6666-285">Explore the documentation for [HPC Pack](https://technet.microsoft.com/library/cc514029).</span></span>
* <span data-ttu-id="e6666-286">Karma bir HPC paketi Küme dağıtımı büyük ölçekli ayarlamak için bkz: [Microsoft HPC paketi ile Azure çalışan rolü örneklerine veri bloğu](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="e6666-286">To set up a hybrid HPC Pack cluster deployment at greater scale, see [Burst to Azure Worker Role Instances with Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
* <span data-ttu-id="e6666-287">Azure Resource Manager şablonları kullanarak Azure'da bir HPC paketi küme oluşturmak diğer yolları için de dahil olmak üzere bkz [azure'da Microsoft HPC paketi ile HPC küme seçenekleri](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e6666-287">For other ways to create an HPC Pack cluster in Azure, including using Azure Resource Manager templates, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png
