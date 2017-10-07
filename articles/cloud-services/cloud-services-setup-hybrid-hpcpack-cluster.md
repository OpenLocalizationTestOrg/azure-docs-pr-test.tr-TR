---
title: "karma bir HPC Pack yukarı aaaSet küme Azure'da | Microsoft Docs"
description: "Küçük, karma yüksek performanslı bilgi işlem (HPC) küme toouse Microsoft HPC Pack ve Azure tooset nasıl yukarı öğrenin"
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
ms.openlocfilehash: 5ad30d78dcd0c6a95d2a61f25015232edab3563c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a><span data-ttu-id="4f211-103">Bir karma yüksek performanslı bilgi işlem (HPC) küme Microsoft HPC Pack ve isteğe bağlı Azure işlem düğümleri ile ayarlama</span><span class="sxs-lookup"><span data-stu-id="4f211-103">Set up a hybrid high performance computing (HPC) cluster with Microsoft HPC Pack and on-demand Azure compute nodes</span></span>
<span data-ttu-id="4f211-104">Microsoft HPC Pack 2012 R2 ve bilgi işlem (HPC) küme küçük, karma yüksek performans ayarlama Azure tooset kullanın.</span><span class="sxs-lookup"><span data-stu-id="4f211-104">Use Microsoft HPC Pack 2012 R2 and Azure tooset up a small, hybrid high performance computing (HPC) cluster.</span></span> <span data-ttu-id="4f211-105">Bu makalede gösterilen hello küme bir şirket içi HPC Pack baş düğümüne oluşur ve bazı düğümler isteğe bağlı bir azure'da dağıtmak bulut hizmeti işlem.</span><span class="sxs-lookup"><span data-stu-id="4f211-105">hello cluster shown in this article consists of an on-premises HPC Pack head node and some compute nodes you deploy on-demand in an Azure cloud service.</span></span> <span data-ttu-id="4f211-106">Ardından, işlem işleri hello karma kümede çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f211-106">You can then run compute jobs on hello hybrid cluster.</span></span>

![Karma HPC Kümesi][Overview] 

<span data-ttu-id="4f211-108">Bu öğretici bir yaklaşım gösterir bazen küme "veri bloğu toohello bulut," toouse ölçeklenebilir, isteğe bağlı Azure kaynaklarını toorun yoğun uygulamalar çağrılır.</span><span class="sxs-lookup"><span data-stu-id="4f211-108">This tutorial shows one approach, sometimes called cluster "burst toohello cloud," toouse scalable, on-demand Azure resources toorun compute-intensive applications.</span></span>

<span data-ttu-id="4f211-109">Bu öğretici hesaplama kümeleri veya HPC paketi ile konusunda deneyim varsayar.</span><span class="sxs-lookup"><span data-stu-id="4f211-109">This tutorial assumes no prior experience with compute clusters or HPC Pack.</span></span> <span data-ttu-id="4f211-110">Tanıtım amacıyla hızla karma işlem kümesi dağıtma hedeflenen yalnızca toohelp olur.</span><span class="sxs-lookup"><span data-stu-id="4f211-110">It is intended only toohelp you deploy a hybrid compute cluster quickly for demonstration purposes.</span></span> <span data-ttu-id="4f211-111">Konuları ve adımları toodeploy karma HPC paketi küme büyük ölçekli bir üretim ortamında ya da toouse HPC Pack 2016 hello görmek için [ayrıntılı yönergeler](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="4f211-111">For considerations and steps toodeploy a hybrid HPC Pack cluster at greater scale in a production environment, or toouse HPC Pack 2016, see hello [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span> <span data-ttu-id="4f211-112">HPC paketi ile diğer senaryolar için Azure sanal makineleri küme dağıtımında otomatik dahil olmak üzere, bkz: [azure'da Microsoft HPC paketi ile HPC küme seçenekleri](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4f211-112">For other scenarios with HPC Pack, including automated cluster deployment in Azure virtual machines, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f211-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4f211-113">Prerequisites</span></span>
* <span data-ttu-id="4f211-114">**Azure aboneliği** -bir Azure aboneliğiniz yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="4f211-114">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>
* <span data-ttu-id="4f211-115">**Windows Server 2012 R2 veya Windows Server 2012 çalıştıran bir şirket içi bilgisayar** -hello baş düğümüne hello HPC Kümesi bu bilgisayarı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4f211-115">**An on-premises computer running Windows Server 2012 R2 or Windows Server 2012** - Use this computer as hello head node of hello HPC cluster.</span></span> <span data-ttu-id="4f211-116">Windows Server zaten çalıştırmıyor değilse, yükleme indirin ve bir [Değerlendirme sürümü](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span><span class="sxs-lookup"><span data-stu-id="4f211-116">If you aren't already running Windows Server, you can download and install an [evaluation version](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span></span>
  
  * <span data-ttu-id="4f211-117">Merhaba bilgisayarın Active Directory etki alanına katılmış tooan olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f211-117">hello computer must be joined tooan Active Directory domain.</span></span> <span data-ttu-id="4f211-118">Test amaçları için hello baş düğümü bilgisayarının bir etki alanı denetleyicisi olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f211-118">For test purposes, you can configure hello head node computer as a domain controller.</span></span> <span data-ttu-id="4f211-119">tooadd Active Directory etki alanı Hizmetleri sunucu rolünü Merhaba ve hello baş düğümü bilgisayarının bir etki alanı denetleyicisi olarak Yükselt, Windows Server hello belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="4f211-119">tooadd hello Active Directory Domain Services server role and promote hello head node computer as a domain controller, see hello documentation for Windows Server.</span></span>
  * <span data-ttu-id="4f211-120">Bu dillerden birinde toosupport HPC Pack Merhaba işletim sistemi yüklenmelidir: İngilizce, Japonca veya Çince (Basitleştirilmiş).</span><span class="sxs-lookup"><span data-stu-id="4f211-120">toosupport HPC Pack, hello operating system must be installed in one of these languages: English, Japanese, or Chinese (Simplified).</span></span>
  * <span data-ttu-id="4f211-121">Önemli ve kritik güncelleştirmelerin yüklü olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="4f211-121">Verify that important and critical updates are installed.</span></span>
* <span data-ttu-id="4f211-122">**HPC Pack 2012 R2** - [karşıdan](http://go.microsoft.com/fwlink/p/?linkid=328024) hello yükleme paketi hello en son sürümünü gider ve kopyalama hello dosyaları toohello baş düğüm bilgisayarı boş.</span><span class="sxs-lookup"><span data-stu-id="4f211-122">**HPC Pack 2012 R2** - [Download](http://go.microsoft.com/fwlink/p/?linkid=328024) hello installation package for hello latest version free of charge and copy hello files toohello head node computer.</span></span> <span data-ttu-id="4f211-123">Yükleme dosyaları hello aynı seçin dili olarak Windows Server yüklemenizin.</span><span class="sxs-lookup"><span data-stu-id="4f211-123">Choose installation files in hello same language as your installation of Windows Server.</span></span>

    >[!NOTE]
    > <span data-ttu-id="4f211-124">HPC Pack 2012 R2 yerine toouse HPC Pack 2016 istiyorsanız, ek yapılandırma gerekmez.</span><span class="sxs-lookup"><span data-stu-id="4f211-124">If you want toouse HPC Pack 2016 instead of HPC Pack 2012 R2, additional configuration is needed.</span></span> <span data-ttu-id="4f211-125">Merhaba bkz [ayrıntılı yönergeler](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="4f211-125">See hello [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
    > 
* <span data-ttu-id="4f211-126">**Etki alanı hesabı** -bu hesap yerel yönetici izinleri hello baş düğüm tooinstall HPC Pack ile yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f211-126">**Domain account** - This account must be configured with local Administrator permissions on hello head node tooinstall HPC Pack.</span></span>
* <span data-ttu-id="4f211-127">**TCP bağlantı noktası 443 üzerinden** hello baş düğüm tooAzure gelen.</span><span class="sxs-lookup"><span data-stu-id="4f211-127">**TCP connectivity on port 443** from hello head node tooAzure.</span></span>

## <a name="install-hpc-pack-on-hello-head-node"></a><span data-ttu-id="4f211-128">HPC Pack Merhaba baş düğüme yükleyin</span><span class="sxs-lookup"><span data-stu-id="4f211-128">Install HPC Pack on hello head node</span></span>
<span data-ttu-id="4f211-129">Microsoft HPC Pack ilk Windows Server çalıştıran şirket içi bilgisayarınıza yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4f211-129">You first install Microsoft HPC Pack on your on-premises computer running Windows Server.</span></span> <span data-ttu-id="4f211-130">Bu bilgisayar hello küme baş düğümüne hello haline gelir.</span><span class="sxs-lookup"><span data-stu-id="4f211-130">This computer becomes hello head node of hello cluster.</span></span>

1. <span data-ttu-id="4f211-131">Toohello baş düğümünde yerel yönetici izinlerine sahip bir etki alanı hesabı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4f211-131">Log on toohello head node by using a domain account that has local Administrator permissions.</span></span>

2. <span data-ttu-id="4f211-132">Merhaba HPC Pack yükleme dosyalarından Setup.exe çalıştırarak Hello HPC Pack Yükleme Sihirbazı'nı başlatın.</span><span class="sxs-lookup"><span data-stu-id="4f211-132">Start hello HPC Pack Installation Wizard by running Setup.exe from hello HPC Pack installation files.</span></span>

3. <span data-ttu-id="4f211-133">Merhaba üzerinde **HPC Pack 2012 R2 Kurulum** ekranında **yeni yükleme veya yeni özellikler tooan mevcut yükleme ekleme**.</span><span class="sxs-lookup"><span data-stu-id="4f211-133">On hello **HPC Pack 2012 R2 Setup** screen, click **New installation or add new features tooan existing installation**.</span></span>

    ![HPC Pack 2012 Kurulumu][install_hpc1]

4. <span data-ttu-id="4f211-135">Merhaba üzerinde **Microsoft yazılım kullanıcı Sözleşmesi sayfası**, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4f211-135">On hello **Microsoft Software User Agreement page**, click **Next**.</span></span>

5. <span data-ttu-id="4f211-136">Merhaba üzerinde **yükleme türünü seç** sayfasında, **bir baş düğüm oluşturarak yeni bir HPC kümesi oluşturma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4f211-136">On hello **Select Installation Type** page, click **Create a new HPC cluster by creating a head node**, and then click **Next**.</span></span>

6. <span data-ttu-id="4f211-137">Merhaba Sihirbazı çeşitli ön yükleme testleri çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="4f211-137">hello wizard runs several pre-installation tests.</span></span> <span data-ttu-id="4f211-138">Tıklatın **sonraki** hello üzerinde **yükleme kuralları** tüm testleri geçerse sayfa.</span><span class="sxs-lookup"><span data-stu-id="4f211-138">Click **Next** on hello **Installation Rules** page if all tests pass.</span></span> <span data-ttu-id="4f211-139">Aksi takdirde, sağlanan hello bilgileri gözden geçirin ve ortamınızda gerekli değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="4f211-139">Otherwise, review hello information provided and make any necessary changes in your environment.</span></span> <span data-ttu-id="4f211-140">Daha sonra yeniden hello testler veya gerekli başlangıç Yükleme Sihirbazı'nı yeniden hello varsa çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4f211-140">Then run hello tests again or if necessary start hello Installation Wizard again.</span></span>
7. <span data-ttu-id="4f211-141">Merhaba üzerinde **HPC DB yapılandırma** sayfasında, emin olun **baş düğüm** tüm HPC veritabanları için seçilir ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4f211-141">On hello **HPC DB Configuration** page, make sure **Head Node** is selected for all HPC databases, and then click **Next**.</span></span> 

    ![DB yapılandırma][install_hpc4]

8. <span data-ttu-id="4f211-143">Merhaba sihirbazın hello kalan sayfalarındaki varsayılan seçimleri kabul edin.</span><span class="sxs-lookup"><span data-stu-id="4f211-143">Accept default selections on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="4f211-144">Merhaba üzerinde **gerekli bileşenleri yüklemek** sayfasında, **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="4f211-144">On hello **Install Required Components** page, click **Install**.</span></span>
   
    ![Yükleme][install_hpc6]

9. <span data-ttu-id="4f211-146">Merhaba yükleme tamamlandıktan sonra işaretini **HPC Küme Yöneticisi'ni başlatın** ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="4f211-146">After hello installation completes, uncheck **Start HPC Cluster Manager** and then click **Finish**.</span></span> <span data-ttu-id="4f211-147">(Bir sonraki adımda HPC Küme Yöneticisi'ni başlatın.)</span><span class="sxs-lookup"><span data-stu-id="4f211-147">(You start HPC Cluster Manager in a later step.)</span></span>
   
    ![Son][install_hpc7]

## <a name="prepare-hello-azure-subscription"></a><span data-ttu-id="4f211-149">Hello Azure aboneliği hazırlama</span><span class="sxs-lookup"><span data-stu-id="4f211-149">Prepare hello Azure subscription</span></span>
<span data-ttu-id="4f211-150">Merhaba adımlarını izleyerek hello gerçekleştirmek [Azure portal](https://portal.azure.com) Azure aboneliğinizle.</span><span class="sxs-lookup"><span data-stu-id="4f211-150">Perform hello following steps in hello [Azure portal](https://portal.azure.com) with your Azure subscription.</span></span> <span data-ttu-id="4f211-151">Bu adımları tamamladıktan sonra Azure düğümleri hello şirket içi baş düğümünden dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f211-151">After completing these steps, you can deploy Azure nodes from hello on-premises head node.</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="4f211-152">Ayrıca, daha sonra ihtiyacınız Azure abonelik Kimliğinizi not edin.</span><span class="sxs-lookup"><span data-stu-id="4f211-152">Also make a note of your Azure subscription ID, which you need later.</span></span> <span data-ttu-id="4f211-153">Merhaba Kimliğinde Bul **abonelikleri** hello Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="4f211-153">Find hello ID in **Subscriptions** in hello portal.</span></span>
  > 

### <a name="upload-hello-default-management-certificate"></a><span data-ttu-id="4f211-154">Merhaba varsayılan yönetim sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="4f211-154">Upload hello default management certificate</span></span>
<span data-ttu-id="4f211-155">HPC Pack Merhaba baş düğüm Azure yönetim sertifikası karşıya yükleyebilir hello Microsoft HPC Azure Management varsayılan sertifika olarak adlandırılan, kendinden imzalı bir sertifika yükler.</span><span class="sxs-lookup"><span data-stu-id="4f211-155">HPC Pack installs a self-signed certificate on hello head node, called hello Default Microsoft HPC Azure Management certificate, that you can upload as an Azure management certificate.</span></span> <span data-ttu-id="4f211-156">Bu sertifikayı test etmek için sağlanır ve kavram kanıtı dağıtımları toosecure hello bağlantı arasındaki hello baş düğüm ve Azure.</span><span class="sxs-lookup"><span data-stu-id="4f211-156">This certificate is provided for testing and proof-of-concept deployments toosecure hello connection between hello head node and Azure.</span></span>

1. <span data-ttu-id="4f211-157">Merhaba baş düğüm bilgisayardan toohello içinde oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4f211-157">From hello head node computer, sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="4f211-158">Tıklatın **abonelikleri** > *your_subscription_name*.</span><span class="sxs-lookup"><span data-stu-id="4f211-158">Click **Subscriptions** > *your_subscription_name*.</span></span>

3. <span data-ttu-id="4f211-159">Tıklatın **yönetim sertifikaları** > **karşıya**.4.</span><span class="sxs-lookup"><span data-stu-id="4f211-159">Click **Management certificates** > **Upload**.4.</span></span> <span data-ttu-id="4f211-160">Merhaba baş düğümünde hello dosyası C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer için göz atın.</span><span class="sxs-lookup"><span data-stu-id="4f211-160">Browse on hello head node for hello file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span></span> <span data-ttu-id="4f211-161">Ardından **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="4f211-161">Then, click **Upload**.</span></span>

   
<span data-ttu-id="4f211-162">Merhaba **HPC Azure Management'ı varsayılan** sertifika hello yönetim sertifikaları listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="4f211-162">hello **Default HPC Azure Management** certificate appears in hello list of management certificates.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="4f211-163">Bir Azure bulut hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f211-163">Create an Azure cloud service</span></span>
> [!NOTE]
> <span data-ttu-id="4f211-164">En iyi performans için hello bulut hizmeti hello depolama hesabında (bir sonraki adımda) hello oluşturup aynı coğrafi bölgede.</span><span class="sxs-lookup"><span data-stu-id="4f211-164">For best performance, create hello cloud service and hello storage account (in a later step) in hello same geographic region.</span></span>
> 
> 

1. <span data-ttu-id="4f211-165">Merhaba Portalı'nda tıklatın **bulut hizmetlerini (Klasik)** > **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4f211-165">In hello portal, click **Cloud services (classic)** > **+Add**.</span></span>

2.  <span data-ttu-id="4f211-166">Merhaba hizmeti için bir DNS adı yazın, bir kaynak grubu ve bir konum seçin ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="4f211-166">Type a DNS name for hello service, choose a resource group and a location, and then click **Create**.</span></span>


### <a name="create-an-azure-storage-account"></a><span data-ttu-id="4f211-167">Azure Storage hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f211-167">Create an Azure storage account</span></span>
1. <span data-ttu-id="4f211-168">Merhaba Portalı'nda tıklatın **depolama hesapları (Klasik)** > **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4f211-168">In hello portal, click **Storage accounts (classic)** > **+Add**.</span></span>

2. <span data-ttu-id="4f211-169">Merhaba hesabı için bir ad yazın ve seçin hello **Klasik** dağıtım modeli.</span><span class="sxs-lookup"><span data-stu-id="4f211-169">Type a name for hello account, and select hello **Classic** deployment model.</span></span>

3. <span data-ttu-id="4f211-170">Bir kaynak grubu ve bir konum seçin ve diğer ayarları varsayılan değerlerinde bırakın.</span><span class="sxs-lookup"><span data-stu-id="4f211-170">Choose a resource group and a location, and leave other settings at default values.</span></span> <span data-ttu-id="4f211-171">Sonra **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4f211-171">Then click **Create**.</span></span>

## <a name="configure-hello-head-node"></a><span data-ttu-id="4f211-172">Merhaba baş düğüm yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4f211-172">Configure hello head node</span></span>
<span data-ttu-id="4f211-173">HPC Küme Yöneticisi'ni toodeploy toouse Azure düğümleri ve toosubmit işleri önce bazı gerekli küme yapılandırma adımlarını gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="4f211-173">toouse HPC Cluster Manager toodeploy Azure nodes and toosubmit jobs, first perform some required cluster configuration steps.</span></span>

1. <span data-ttu-id="4f211-174">Merhaba baş düğümünde HPC Küme Yöneticisi'ni başlatın.</span><span class="sxs-lookup"><span data-stu-id="4f211-174">On hello head node, start HPC Cluster Manager.</span></span> <span data-ttu-id="4f211-175">Merhaba, **baş düğüm Seç** iletişim kutusu görüntülenirse, tıklatın **yerel bilgisayar**.</span><span class="sxs-lookup"><span data-stu-id="4f211-175">If hello **Select Head Node** dialog box appears, click **Local Computer**.</span></span> <span data-ttu-id="4f211-176">Merhaba **dağıtım Yapılacaklar listesi** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4f211-176">hello **Deployment To-do List** appears.</span></span>

2. <span data-ttu-id="4f211-177">Altında **gerekli dağıtım görevlerini**, tıklatın **ağınızı yapılandırmak**.</span><span class="sxs-lookup"><span data-stu-id="4f211-177">Under **Required deployment tasks**, click **Configure your network**.</span></span>
   
    ![Ağ yapılandırma][config_hpc2]

3. <span data-ttu-id="4f211-179">Hello Ağ Yapılandırma Sihirbazı'nı seçin **yalnızca bir kurumsal ağ üzerindeki tüm düğümleri** (topoloji 5).</span><span class="sxs-lookup"><span data-stu-id="4f211-179">In hello Network Configuration Wizard, select **All nodes only on an enterprise network** (Topology 5).</span></span> <span data-ttu-id="4f211-180">Bu ağ hello tanıtım amacıyla basit bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="4f211-180">This network configuration is hello simplest for demonstration purposes.</span></span>
   
    ![Topoloji 5][config_hpc3]
   
4. <span data-ttu-id="4f211-182">Tıklatın **sonraki** hello Sihirbazı sayfaları kalan hello tooaccept varsayılan değerler.</span><span class="sxs-lookup"><span data-stu-id="4f211-182">Click **Next** tooaccept default values on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="4f211-183">Ardından, hello **gözden geçirme** sekmesini tıklatın, **yapılandırma** toocomplete hello ağ yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="4f211-183">Then, on hello **Review** tab, click **Configure** toocomplete hello network configuration.</span></span>

5. <span data-ttu-id="4f211-184">Merhaba, **dağıtım Yapılacaklar listesi**, tıklatın **yükleme kimlik bilgileri sağlamak**.</span><span class="sxs-lookup"><span data-stu-id="4f211-184">In hello **Deployment To-do List**, click **Provide installation credentials**.</span></span>

6. <span data-ttu-id="4f211-185">Merhaba, **yükleme kimlik bilgileri** iletişim kutusu, tooinstall HPC Pack kullanılan hello etki alanı hesabının hello kimlik bilgilerini yazın.</span><span class="sxs-lookup"><span data-stu-id="4f211-185">In hello **Installation Credentials** dialog box, type hello credentials of hello domain account that you used tooinstall HPC Pack.</span></span> <span data-ttu-id="4f211-186">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4f211-186">Then click **OK**.</span></span> 
   
    ![Yükleme kimlik bilgileri][config_hpc6]
   
7. <span data-ttu-id="4f211-188">Merhaba, **dağıtım Yapılacaklar listesi**, tıklatın **yeni düğümlerinin hello adlandırma yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="4f211-188">In hello **Deployment To-do List**, click **Configure hello naming of new nodes**.</span></span>

8. <span data-ttu-id="4f211-189">Merhaba, **düğümü adlandırma serisi belirtin** iletişim kutusunda, hello varsayılan serisi ve tıklatın adlandırma kabul **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4f211-189">In hello **Specify Node Naming Series** dialog box, accept hello default naming series and click **OK**.</span></span> <span data-ttu-id="4f211-190">Hello Azure düğümleri Bu öğreticide Ekle otomatik olarak adlandırılmış olsa da bu adımı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="4f211-190">Complete this step even though hello Azure nodes you add in this tutorial are named automatically.</span></span>
   
    ![Düğüm adlandırma][config_hpc8]
   
9. <span data-ttu-id="4f211-192">Merhaba, **dağıtım Yapılacaklar listesi**, tıklatın **düğüm şablonu oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="4f211-192">In hello **Deployment To-do List**, click **Create a node template**.</span></span> <span data-ttu-id="4f211-193">Daha sonra hello öğreticide hello düğüm şablonu tooadd Azure düğümleri toohello küme kullanın.</span><span class="sxs-lookup"><span data-stu-id="4f211-193">Later in hello tutorial, you use hello node template tooadd Azure nodes toohello cluster.</span></span>

10. <span data-ttu-id="4f211-194">İçinde düğüm şablonu oluşturma Sihirbazı Merhaba, aşağıdaki hello yapın:</span><span class="sxs-lookup"><span data-stu-id="4f211-194">In hello Create Node Template Wizard, do hello following:</span></span>
    
    <span data-ttu-id="4f211-195">a.</span><span class="sxs-lookup"><span data-stu-id="4f211-195">a.</span></span> <span data-ttu-id="4f211-196">Merhaba üzerinde **düğümü şablon türünü seç** sayfasında, **Windows Azure düğüm şablonu**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4f211-196">On hello **Choose Node Template Type** page, click **Windows Azure node template**, and then click **Next**.</span></span>
    
    ![Düğüm şablonu][config_hpc10]
    
    <span data-ttu-id="4f211-198">b.</span><span class="sxs-lookup"><span data-stu-id="4f211-198">b.</span></span> <span data-ttu-id="4f211-199">Tıklatın **sonraki** tooaccept hello varsayılan şablon adı.</span><span class="sxs-lookup"><span data-stu-id="4f211-199">Click **Next** tooaccept hello default template name.</span></span>
    
    <span data-ttu-id="4f211-200">c.</span><span class="sxs-lookup"><span data-stu-id="4f211-200">c.</span></span> <span data-ttu-id="4f211-201">Merhaba üzerinde **abonelik bilgilerini gir** sayfasında, Azure abonelik Kimliğinizi (Azure hesap bilgilerinizi kullanılabilir) girin.</span><span class="sxs-lookup"><span data-stu-id="4f211-201">On hello **Provide Subscription Information** page, enter your Azure subscription ID (available in your Azure account information).</span></span> <span data-ttu-id="4f211-202">Ardından **yönetim sertifikası**, göz **varsayılan Microsoft HPC Azure yönetimi.**</span><span class="sxs-lookup"><span data-stu-id="4f211-202">Then, in **Management certificate**, browse for **Default Microsoft HPC Azure Management.**</span></span> <span data-ttu-id="4f211-203">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4f211-203">Then click **Next**.</span></span>
    
    ![Düğüm şablonu][config_hpc12]
    
    <span data-ttu-id="4f211-205">d.</span><span class="sxs-lookup"><span data-stu-id="4f211-205">d.</span></span> <span data-ttu-id="4f211-206">Merhaba üzerinde **hizmet bilgileri sağlayan** sayfası, select hello bulut hizmeti ve bir önceki adımda oluşturduğunuz hello depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="4f211-206">On hello **Provide Service Information** page, select hello cloud service and hello storage account that you created in a previous step.</span></span> <span data-ttu-id="4f211-207">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4f211-207">Then click **Next**.</span></span>
    
    ![Düğüm şablonu][config_hpc13]
    
    <span data-ttu-id="4f211-209">e.</span><span class="sxs-lookup"><span data-stu-id="4f211-209">e.</span></span> <span data-ttu-id="4f211-210">Tıklatın **sonraki** hello Sihirbazı sayfaları kalan hello tooaccept varsayılan değerler.</span><span class="sxs-lookup"><span data-stu-id="4f211-210">Click **Next** tooaccept default values on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="4f211-211">Ardından, hello **gözden geçirme** sekmesini tıklatın, **oluşturma** toocreate hello düğüm şablonu.</span><span class="sxs-lookup"><span data-stu-id="4f211-211">Then, on hello **Review** tab, click **Create** toocreate hello node template.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="4f211-212">Varsayılan olarak, hello Azure düğüm şablonu (sağlayamaz) toostart ve durdurma hello düğümleri ayarlarını el ile HPC Küme Yöneticisi'ni kullanarak içerir.</span><span class="sxs-lookup"><span data-stu-id="4f211-212">By default, hello Azure node template includes settings for you toostart (provision) and stop hello nodes manually, using HPC Cluster Manager.</span></span> <span data-ttu-id="4f211-213">İsteğe bağlı olarak bir zamanlama toostart yapılandırabilirsiniz ve Azure düğümleri otomatik olarak hello durdurun.</span><span class="sxs-lookup"><span data-stu-id="4f211-213">You can optionally configure a schedule toostart and stop hello Azure nodes automatically.</span></span>
    > 
    > 

## <a name="add-azure-nodes-toohello-cluster"></a><span data-ttu-id="4f211-214">Azure düğümleri toohello küme ekleme</span><span class="sxs-lookup"><span data-stu-id="4f211-214">Add Azure nodes toohello cluster</span></span>
<span data-ttu-id="4f211-215">Şimdi hello düğüm şablonu tooadd Azure düğümleri toohello küme kullanın.</span><span class="sxs-lookup"><span data-stu-id="4f211-215">Now use hello node template tooadd Azure nodes toohello cluster.</span></span> <span data-ttu-id="4f211-216">Hello düğümleri toohello küme (sağlayamaz) başlayabilmeniz için yapılandırma bilgilerini depolayan ekleme hello bulut hizmetindeki herhangi bir zamanda bunları.</span><span class="sxs-lookup"><span data-stu-id="4f211-216">Adding hello nodes toohello cluster stores their configuration information so that you can start (provision) them at any time in hello cloud service.</span></span> <span data-ttu-id="4f211-217">Merhaba örnekleri hello bulut hizmetinde çalışan sonra aboneliğinizi yalnızca Azure düğümleri için sizden ücret.</span><span class="sxs-lookup"><span data-stu-id="4f211-217">Your subscription only gets charged for Azure nodes after hello instances are running in hello cloud service.</span></span>

<span data-ttu-id="4f211-218">Bu adımları tooadd iki küçük düğümler izleyin.</span><span class="sxs-lookup"><span data-stu-id="4f211-218">Follow these steps tooadd two Small nodes.</span></span>

1. <span data-ttu-id="4f211-219">HPC Küme Yöneticisi'nde **düğüm Yönetimi** (adlı **kaynak yönetimi** HPC Pack geçerli sürümlerinde) > **düğüm Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4f211-219">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack) > **Add Node**.</span></span>
   
    ![Düğüm Ekle][add_node1]

2. <span data-ttu-id="4f211-221">İçinde Düğüm Ekleme Sihirbazı, üzerinde hello hello **dağıtım yöntemini seçin** sayfasında, **Ekle Windows Azure düğümleri**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4f211-221">In hello Add Node Wizard, on hello **Select Deployment Method** page, click **Add Windows Azure nodes**, and then click **Next**.</span></span>
   
    ![Azure düğüm Ekle][add_node1_1]

3. <span data-ttu-id="4f211-223">Merhaba üzerinde **belirtin yeni düğümler** sayfası, önceden oluşturduğunuz select hello Azure düğüm şablonu (varsayılan olarak adlandırılan **varsayılan AzureNode şablonu**).</span><span class="sxs-lookup"><span data-stu-id="4f211-223">On hello **Specify New Nodes** page, select hello Azure node template you created previously (called by default **Default AzureNode Template**).</span></span> <span data-ttu-id="4f211-224">Ardından belirtin **2** boyutu düğümlerinin **küçük**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4f211-224">Then specify **2** nodes of size **Small**, and then click **Next**.</span></span>
   
    ![Düğüm belirtin][add_node2]
   
4. <span data-ttu-id="4f211-226">Merhaba üzerinde **Düğüm Ekleme Sihirbazı Tamamlanıyor hello** sayfasında, **son**.</span><span class="sxs-lookup"><span data-stu-id="4f211-226">On hello **Completing hello Add Node Wizard** page, click **Finish**.</span></span>
    
     <span data-ttu-id="4f211-227">Adlı iki Azure düğümleri **AzureCN 0001** ve **AzureCN 0002**, artık HPC Küme Yöneticisi'nde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4f211-227">Two Azure nodes, named **AzureCN-0001** and **AzureCN-0002**, now appear in HPC Cluster Manager.</span></span> <span data-ttu-id="4f211-228">Her ikisi de hello olan **değil dağıtılan** durumu.</span><span class="sxs-lookup"><span data-stu-id="4f211-228">Both are in hello **Not-Deployed** state.</span></span>
   
    ![Eklenen düğümlerine][add_node3]

## <a name="start-hello-azure-nodes"></a><span data-ttu-id="4f211-230">Başlangıç Azure düğümleri hello</span><span class="sxs-lookup"><span data-stu-id="4f211-230">Start hello Azure nodes</span></span>
<span data-ttu-id="4f211-231">İstediğiniz zaman toouse hello küme kaynakları Azure, kullanım HPC Küme Yöneticisi'ni toostart (sağlayamaz) Azure düğümleri hello ve çevrimiçi duruma getirin.</span><span class="sxs-lookup"><span data-stu-id="4f211-231">When you want toouse hello cluster resources in Azure, use HPC Cluster Manager toostart (provision) hello Azure nodes and bring them online.</span></span>

1. <span data-ttu-id="4f211-232">HPC Küme Yöneticisi'nde **düğüm Yönetimi** (adlı **kaynak yönetimi** HPC Pack geçerli sürümlerinde), ve hello Azure düğümleri seçin.</span><span class="sxs-lookup"><span data-stu-id="4f211-232">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack), and select hello Azure nodes.</span></span>

2. <span data-ttu-id="4f211-233">Tıklatın **Başlat**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4f211-233">Click **Start**, and then click **OK**.</span></span>
   
   ![Düğümleri Başlat][add_node4]
   
    <span data-ttu-id="4f211-235">Merhaba düğümleri geçiş toohello **sağlama** durumu.</span><span class="sxs-lookup"><span data-stu-id="4f211-235">hello nodes transition toohello **Provisioning** state.</span></span> <span data-ttu-id="4f211-236">Görünüm hello sağlama ilerleme durumu günlük tootrack hello sağlama.</span><span class="sxs-lookup"><span data-stu-id="4f211-236">View hello provisioning log tootrack hello provisioning progress.</span></span>
   
    ![Sağlama düğümler][add_node6]

3. <span data-ttu-id="4f211-238">Birkaç dakika sonra hello Azure düğümleri sağlama tamamladığınızda ve hello **çevrimdışı** durumu.</span><span class="sxs-lookup"><span data-stu-id="4f211-238">After a few minutes, hello Azure nodes finish provisioning and are in hello **Offline** state.</span></span> <span data-ttu-id="4f211-239">Bu durumda, hello rol örnekleri çalıştıran ancak henüz küme işlerini kabul edemez.</span><span class="sxs-lookup"><span data-stu-id="4f211-239">In this state, hello role instances are running but cannot yet accept cluster jobs.</span></span>

4. <span data-ttu-id="4f211-240">Rol örnekleri hello tooconfirm çalışıyorsa, hello Azure Portalı'na tıklayın **bulut Hizmetleri (Klasik)** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="4f211-240">tooconfirm that hello role instances are running, in hello Azure portal, click **Cloud Services (classic)** > *your_cloud_service_name*.</span></span>
   
   <span data-ttu-id="4f211-241">İki görmelisiniz **HpcWorkerRole** hello Hizmeti'nde çalışan örnekleri (düğümler).</span><span class="sxs-lookup"><span data-stu-id="4f211-241">You should see two **HpcWorkerRole** instances (nodes) running in hello service.</span></span> <span data-ttu-id="4f211-242">HPC Pack ayrıca otomatik olarak dağıtan iki **HpcProxy** örnekleri (boyutu Orta) toohandle iletişimi hello baş düğüm ve Azure arasında.</span><span class="sxs-lookup"><span data-stu-id="4f211-242">HPC Pack also automatically deploys two **HpcProxy** instances (size Medium) toohandle communication between hello head node and Azure.</span></span>

   ![Çalışan örnekleri][view_instances1]

5. <span data-ttu-id="4f211-244">işlerini, select hello düğümleri, sağ tıklatın ve ardından toobring hello Azure düğümleri çevrimiçi toorun küme **çevrimiçine**.</span><span class="sxs-lookup"><span data-stu-id="4f211-244">toobring hello Azure nodes online toorun cluster jobs, select hello nodes, right-click, and then click **Bring Online**.</span></span>
   
    ![Çevrimdışı düğümler][add_node7]
   
    <span data-ttu-id="4f211-246">HPC Küme Yöneticisi'ni gösterir hello düğümlerin hello olduğunu **çevrimiçi** durumu.</span><span class="sxs-lookup"><span data-stu-id="4f211-246">HPC Cluster Manager indicates that hello nodes are in hello **Online** state.</span></span>

## <a name="run-a-command-across-hello-cluster"></a><span data-ttu-id="4f211-247">Merhaba küme üzerinde bir komutu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="4f211-247">Run a command across hello cluster</span></span>
<span data-ttu-id="4f211-248">toocheck hello yükleme, kullanım hello HPC Pack **clusrun** komutu toorun bir komutu veya bir veya daha fazla küme düğümlerinde uygulama.</span><span class="sxs-lookup"><span data-stu-id="4f211-248">toocheck hello installation, use hello HPC Pack **clusrun** command toorun a command or application on one or more cluster nodes.</span></span> <span data-ttu-id="4f211-249">Basit bir örnek olarak kullanın **clusrun** tooget hello IP yapılandırması hello Azure düğümleri.</span><span class="sxs-lookup"><span data-stu-id="4f211-249">As a simple example, use **clusrun** tooget hello IP configuration of hello Azure nodes.</span></span>

1. <span data-ttu-id="4f211-250">Merhaba baş düğümünde yönetici olarak bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="4f211-250">On hello head node, open a command prompt as an administrator.</span></span>

2. <span data-ttu-id="4f211-251">Merhaba aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="4f211-251">Type hello following command:</span></span>
   
    `clusrun /nodes:azurecn* ipconfig`

3. <span data-ttu-id="4f211-252">İstenirse, Küme Yönetici parolanızı girin.</span><span class="sxs-lookup"><span data-stu-id="4f211-252">If prompted, enter your cluster administrator password.</span></span> <span data-ttu-id="4f211-253">Benzer toohello aşağıdaki komut çıktısı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f211-253">You should see command output similar toohello following.</span></span>
   
    ![Clusrun][clusrun1]

## <a name="run-a-test-job"></a><span data-ttu-id="4f211-255">Bir test işini çalıştır</span><span class="sxs-lookup"><span data-stu-id="4f211-255">Run a test job</span></span>
<span data-ttu-id="4f211-256">Şimdi hello karma kümede çalışan bir test işi gönderin.</span><span class="sxs-lookup"><span data-stu-id="4f211-256">Now submit a test job that runs on hello hybrid cluster.</span></span> <span data-ttu-id="4f211-257">Bu, bir basit parametrik tarama işi (doğası gereği Paralel hesaplama türü) örneğidir.</span><span class="sxs-lookup"><span data-stu-id="4f211-257">This example is a simple parametric sweep job (a type of intrinsically parallel computation).</span></span> <span data-ttu-id="4f211-258">Bu örnek bir tamsayı tooitself hello kullanarak eklemek görevleri çalıştırır **/a ayarlamak** komutu.</span><span class="sxs-lookup"><span data-stu-id="4f211-258">This example runs subtasks that add an integer tooitself by using hello **set /a** command.</span></span> <span data-ttu-id="4f211-259">Merhaba kümedeki tüm düğümlerin hello toofinishing hello görevleri tamsayılar 1 too100 katkıda.</span><span class="sxs-lookup"><span data-stu-id="4f211-259">All hello nodes in hello cluster contribute toofinishing hello subtasks for integers from 1 too100.</span></span>

1. <span data-ttu-id="4f211-260">HPC Küme Yöneticisi'nde **iş yönetimi** > **yeni parametrik Sweep işi**.</span><span class="sxs-lookup"><span data-stu-id="4f211-260">In HPC Cluster Manager, click **Job Management** > **New Parametric Sweep Job**.</span></span>
   
    ![Yeni Proje][test_job1]

2. <span data-ttu-id="4f211-262">Merhaba, **yeni parametrik Sweep işi** iletişim kutusunda **komut satırı**, türü `set /a *+*` (görünür hello varsayılan komut satırı üzerine).</span><span class="sxs-lookup"><span data-stu-id="4f211-262">In hello **New Parametric Sweep Job** dialog box, in **Command line**, type `set /a *+*` (overwriting hello default command line that appears).</span></span> <span data-ttu-id="4f211-263">Ayarları kalan hello için varsayılan değerleri bırakın ve ardından **gönderme** toosubmit hello işi.</span><span class="sxs-lookup"><span data-stu-id="4f211-263">Leave default values for hello remaining settings, and then click **Submit** toosubmit hello job.</span></span>
   
    ![Parametrik tarama][param_sweep1]

3. <span data-ttu-id="4f211-265">Merhaba işi bittiğinde hello çift **My Sweep görev** iş.</span><span class="sxs-lookup"><span data-stu-id="4f211-265">When hello job is finished, double-click hello **My Sweep Task** job.</span></span>

4. <span data-ttu-id="4f211-266">Tıklatın **görünümü görevleri**ve o alt alt tooview hesaplanan hello çıktısını'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4f211-266">Click **View Tasks**, and then click a subtask tooview hello calculated output of that subtask.</span></span>
   
    ![Görev sonuçları][view_job361]

5. <span data-ttu-id="4f211-268">hangi düğümün gerçekleştirilen hello hesaplama o alt görev için toosee tıklatın **ayrılan düğümler**.</span><span class="sxs-lookup"><span data-stu-id="4f211-268">toosee which node performed hello calculation for that subtask, click **Allocated Nodes**.</span></span> <span data-ttu-id="4f211-269">(Kümeniz farklı bir düğüme adını gösterebilir.)</span><span class="sxs-lookup"><span data-stu-id="4f211-269">(Your cluster might show a different node name.)</span></span>
   
    ![Görev sonuçları][view_job362]

## <a name="stop-hello-azure-nodes"></a><span data-ttu-id="4f211-271">Durdur Azure düğümleri hello</span><span class="sxs-lookup"><span data-stu-id="4f211-271">Stop hello Azure nodes</span></span>
<span data-ttu-id="4f211-272">Merhaba küme çalıştıktan sonra hello Azure düğümleri tooavoid gereksiz ücretleri tooyour hesabı durdurun.</span><span class="sxs-lookup"><span data-stu-id="4f211-272">After you try out hello cluster, stop hello Azure nodes tooavoid unnecessary charges tooyour account.</span></span> <span data-ttu-id="4f211-273">Bu adım hello bulut hizmetini durdurur ve hello Azure rol örneklerini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="4f211-273">This step stops hello cloud service and removes hello Azure role instances.</span></span>

1. <span data-ttu-id="4f211-274">HPC Küme Yöneticisi ' nde, **düğüm Yönetimi** (adlı **kaynak yönetimi** HPC Pack önceki sürümlerinde), hem Azure düğümleri seçin.</span><span class="sxs-lookup"><span data-stu-id="4f211-274">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in previous versions of HPC Pack), select both Azure nodes.</span></span> <span data-ttu-id="4f211-275">Ardından **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="4f211-275">Then, click **Stop**.</span></span>
   
    ![Düğümler durdurun][stop_node1]

2. <span data-ttu-id="4f211-277">Merhaba, **durdurmak Windows Azure düğümleri** iletişim kutusu, tıklatın **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="4f211-277">In hello **Stop Windows Azure nodes** dialog box, click **Stop**.</span></span> 
   
3. <span data-ttu-id="4f211-278">Merhaba düğümleri geçiş toohello **durdurma** durumu.</span><span class="sxs-lookup"><span data-stu-id="4f211-278">hello nodes transition toohello **Stopping** state.</span></span> <span data-ttu-id="4f211-279">Birkaç dakika sonra hello düğümlerinin HPC Küme Yöneticisi'ni gösterir **değil dağıtılan**.</span><span class="sxs-lookup"><span data-stu-id="4f211-279">After a few minutes, HPC Cluster Manager shows that hello nodes are **Not-Deployed**.</span></span>
   
    ![Dağıtılmadı düğümler][stop_node4]

4. <span data-ttu-id="4f211-281">Merhaba rol örnekleri artık Azure üzerinde çalışan tooconfirm hello Azure portal'ı tıklatın **bulut hizmetlerini (Klasik)** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="4f211-281">tooconfirm that hello role instances are no longer running in Azure, in hello Azure portal, click **Cloud services (classic)** > *your_cloud_service_name*.</span></span> <span data-ttu-id="4f211-282">Hiçbir örneği hello üretim ortamına dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="4f211-282">No instances are deployed in hello production environment.</span></span> 
   
    <span data-ttu-id="4f211-283">Başlangıç Öğreticisi tamamlar.</span><span class="sxs-lookup"><span data-stu-id="4f211-283">This completes hello tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f211-284">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4f211-284">Next steps</span></span>
* <span data-ttu-id="4f211-285">Merhaba belgelerine keşfedin [HPC Pack](https://technet.microsoft.com/library/cc514029).</span><span class="sxs-lookup"><span data-stu-id="4f211-285">Explore hello documentation for [HPC Pack](https://technet.microsoft.com/library/cc514029).</span></span>
* <span data-ttu-id="4f211-286">karma bir HPC paketi Küme dağıtımı büyük ölçekte yukarı tooset bkz [Microsoft HPC paketi ile tooAzure çalışan rolü örneklerine veri bloğu](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="4f211-286">tooset up a hybrid HPC Pack cluster deployment at greater scale, see [Burst tooAzure Worker Role Instances with Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
* <span data-ttu-id="4f211-287">Azure Resource Manager şablonları kullanarak diğer yolları toocreate Azure bir HPC paketi küme için de dahil olmak üzere bkz [azure'da Microsoft HPC paketi ile HPC küme seçenekleri](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4f211-287">For other ways toocreate an HPC Pack cluster in Azure, including using Azure Resource Manager templates, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


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
