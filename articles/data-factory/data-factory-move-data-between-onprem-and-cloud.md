---
title: "aaaMove data - veri yönetimi ağ geçidi | Microsoft Docs"
description: "Şirket içi ve hello arasında veri ağ geçidi toomove veri ayarlama bulut. Veri Yönetimi ağ geçidi, verilerinizi Azure Data Factory toomove kullanın."
keywords: "Veri ağ geçidi, veri tümleştirme, veri, Ağ Geçidi kimlik taşıma"
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 314341c142d5260c785b7e82081774f044450e81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-between-on-premises-sources-and-hello-cloud-with-data-management-gateway"></a><span data-ttu-id="75f86-105">Şirket içi kaynakları ve veri yönetimi ağ geçidi ile Merhaba bulut arasında veri taşıma</span><span class="sxs-lookup"><span data-stu-id="75f86-105">Move data between on-premises sources and hello cloud with Data Management Gateway</span></span>
<span data-ttu-id="75f86-106">Bu makalede, şirket içi veri depoları ve veri fabrikası kullanarak bulut veri depoları arasında veri tümleştirme genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="75f86-106">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span></span> <span data-ttu-id="75f86-107">Merhaba üzerinde derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale ve diğer veri fabrikası temel kavramları makaleler: [veri kümeleri](data-factory-create-datasets.md) ve [ardışık düzen](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="75f86-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="data-management-gateway"></a><span data-ttu-id="75f86-108">Veri Yönetimi Ağ Geçidi</span><span class="sxs-lookup"><span data-stu-id="75f86-108">Data Management Gateway</span></span>
<span data-ttu-id="75f86-109">Bir şirket içi veri deposu denetleyicisinden verilerin taşınması, şirket içi makineyi tooenable veri yönetimi ağ geçidi yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="75f86-109">You must install Data Management Gateway on your on-premises machine tooenable moving data to/from an on-premises data store.</span></span> <span data-ttu-id="75f86-110">Merhaba ağ geçidi hello hello ağ geçidi toohello veri deposu bağlanabileceği sürece hello veri deposu olarak veya farklı bir makinede aynı makine üzerinde yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="75f86-110">hello gateway can be installed on hello same machine as hello data store or on a different machine as long as hello gateway can connect toohello data store.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75f86-111">Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) makale veri yönetimi ağ geçidi hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="75f86-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> 

<span data-ttu-id="75f86-112">Merhaba aşağıdaki örneklerde, nasıl gösterir toocreate data factory bir şirket içi veri taşır ardışık ile **SQL Server** veritabanı tooan Azure blob depolama.</span><span class="sxs-lookup"><span data-stu-id="75f86-112">hello following walkthrough shows you how toocreate a data factory with a pipeline that moves data from an on-premises **SQL Server** database tooan Azure blob storage.</span></span> <span data-ttu-id="75f86-113">Merhaba izlenecek bir parçası olarak yükleyin ve makinenizde hello veri yönetimi ağ geçidi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="75f86-113">As part of hello walkthrough, you install and configure hello Data Management Gateway on your machine.</span></span>

## <a name="walkthrough-copy-on-premises-data-toocloud"></a><span data-ttu-id="75f86-114">İzlenecek yol: şirket içi veri toocloud kopyalama</span><span class="sxs-lookup"><span data-stu-id="75f86-114">Walkthrough: copy on-premises data toocloud</span></span>
<span data-ttu-id="75f86-115">Bu izlenecek adımları izleyerek hello:</span><span class="sxs-lookup"><span data-stu-id="75f86-115">In this walkthrough you do hello following steps:</span></span> 

1. <span data-ttu-id="75f86-116">Veri Fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75f86-116">Create a data factory.</span></span>
2. <span data-ttu-id="75f86-117">Veri Yönetimi ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75f86-117">Create a data management gateway.</span></span> 
3. <span data-ttu-id="75f86-118">Kaynak ve havuz veri depoları için bağlantılı Hizmetleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75f86-118">Create linked services for source and sink data stores.</span></span>
4. <span data-ttu-id="75f86-119">Veri kümeleri toorepresent girişi oluşturun ve çıktı verilerini.</span><span class="sxs-lookup"><span data-stu-id="75f86-119">Create datasets toorepresent input and output data.</span></span>
5. <span data-ttu-id="75f86-120">Bir kopyalama etkinliği toomove hello verilerle bir işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75f86-120">Create a pipeline with a copy activity toomove hello data.</span></span>

## <a name="prerequisites-for-hello-tutorial"></a><span data-ttu-id="75f86-121">Başlangıç öğreticisi için Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="75f86-121">Prerequisites for hello tutorial</span></span>
<span data-ttu-id="75f86-122">Bu kılavuzda başlamadan önce aşağıdaki önkoşullar hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="75f86-122">Before you begin this walkthrough, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="75f86-123">**Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="75f86-123">**Azure subscription**.</span></span>  <span data-ttu-id="75f86-124">Bir aboneliğiniz yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75f86-124">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="75f86-125">Merhaba bkz [ücretsiz deneme](http://azure.microsoft.com/pricing/free-trial/) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="75f86-125">See hello [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="75f86-126">**Azure depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="75f86-126">**Azure Storage Account**.</span></span> <span data-ttu-id="75f86-127">Merhaba blob depolama alanı olarak kullandığınız bir **hedef/havuz** verileri depolamak Bu öğreticide.</span><span class="sxs-lookup"><span data-stu-id="75f86-127">You use hello blob storage as a **destination/sink** data store in this tutorial.</span></span> <span data-ttu-id="75f86-128">bir Azure depolama hesabınız yoksa, hello bkz [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) adımları toocreate bir makale.</span><span class="sxs-lookup"><span data-stu-id="75f86-128">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
* <span data-ttu-id="75f86-129">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="75f86-129">**SQL Server**.</span></span> <span data-ttu-id="75f86-130">Bir şirket içi SQL Server veritabanı olarak kullandığınız bir **kaynak** verileri depolamak Bu öğreticide.</span><span class="sxs-lookup"><span data-stu-id="75f86-130">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="75f86-131">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="75f86-131">Create data factory</span></span>
<span data-ttu-id="75f86-132">Bu adımda, kullandığınız hello Azure Data Factory örneğini adlı Azure portal toocreate **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="75f86-132">In this step, you use hello Azure portal toocreate an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span></span>

1. <span data-ttu-id="75f86-133">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="75f86-133">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="75f86-134">Tıklatın **+ yeni**, tıklatın **Intelligence + analiz**, tıklatıp **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="75f86-134">Click **+ NEW**, click **Intelligence + analytics**, and click **Data Factory**.</span></span>

   ![Yeni->DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. <span data-ttu-id="75f86-136">Merhaba, **yeni data factory** want **ADFTutorialOnPremDF** hello adı için.</span><span class="sxs-lookup"><span data-stu-id="75f86-136">In hello **New data factory** page, enter **ADFTutorialOnPremDF** for hello Name.</span></span>

    ![TooStartboard Ekle](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="75f86-138">Merhaba hello Azure veri fabrikasının adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="75f86-138">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="75f86-139">Merhaba hatayı alırsanız: **veri fabrikası adı "ADFTutorialOnPremDF" kullanılabilir değil**hello veri fabrikası (örneğin, yournameADFTutorialOnPremDF) hello adını değiştirin ve oluşturmayı yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="75f86-139">If you receive hello error: **Data factory name “ADFTutorialOnPremDF” is not available**, change hello name of hello data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span></span> <span data-ttu-id="75f86-140">Bu öğreticide adımları uygularken ADFTutorialOnPremDF yerine bu adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="75f86-140">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span></span>
   >
   > <span data-ttu-id="75f86-141">Merhaba veri fabrikasının Hello adı olarak kaydedilmesi bir **DNS** hello gelecekte olarak adlandırın ve bu nedenle herkese görünür hale gelmiştir.</span><span class="sxs-lookup"><span data-stu-id="75f86-141">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="75f86-142">Select hello **Azure aboneliği** oluşturulan hello veri fabrikası toobe istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="75f86-142">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="75f86-143">Mevcut bir **kaynak grubu** seçin ya da bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75f86-143">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="75f86-144">Merhaba öğretici için adlı bir kaynak grubu oluşturun: **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="75f86-144">For hello tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span></span>
6. <span data-ttu-id="75f86-145">Tıklatın **oluşturma** hello üzerinde **yeni data factory** sayfası.</span><span class="sxs-lookup"><span data-stu-id="75f86-145">Click **Create** on hello **New data factory** page.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="75f86-146">toocreate Data Factory örnekleri hello üyesi olmalıdır [veri fabrikası katkıda bulunan](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello abonelik/kaynak grubu düzeyinde rol.</span><span class="sxs-lookup"><span data-stu-id="75f86-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="75f86-147">Oluşturma işlemi tamamlandıktan sonra hello bkz **Data Factory** sayfasında hello görüntü aşağıdaki gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="75f86-147">After creation is complete, you see hello **Data Factory** page as shown in hello following image:</span></span>

   ![Data Factory giriş sayfası](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a><span data-ttu-id="75f86-149">Ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="75f86-149">Create gateway</span></span>
1. <span data-ttu-id="75f86-150">Merhaba, **Data Factory** sayfasında, **yazar ve dağıtma** döşeme toolaunch hello **Düzenleyicisi** hello veri fabrikası için.</span><span class="sxs-lookup"><span data-stu-id="75f86-150">In hello **Data Factory** page, click **Author and deploy** tile toolaunch hello **Editor** for hello data factory.</span></span>

    ![Geliştir ve Dağıt Kutucuğu](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. <span data-ttu-id="75f86-152">Hello Data Factory Düzenleyici'de, tıklatın **... Daha fazla** hello araç ve ardından **yeni veri ağ geçidi**.</span><span class="sxs-lookup"><span data-stu-id="75f86-152">In hello Data Factory Editor, click **... More** on hello toolbar and then click **New data gateway**.</span></span> <span data-ttu-id="75f86-153">Alternatif olarak, sağ tıklayarak **Data Gateways** hello ağaç görünümü ve tıklatın **yeni veri ağ geçidi**.</span><span class="sxs-lookup"><span data-stu-id="75f86-153">Alternatively, you can right-click **Data Gateways** in hello tree view, and click **New data gateway**.</span></span>

   ![Araç çubuğundaki yeni veri ağ geçidi](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. <span data-ttu-id="75f86-155">Merhaba, **oluşturma** want **adftutorialgateway** hello için **adı**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="75f86-155">In hello **Create** page, enter **adftutorialgateway** for hello **name**, and click **OK**.</span></span>     

    ![Ağ geçidi sayfası oluşturma](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > <span data-ttu-id="75f86-157">Bu kılavuzda, yalnızca bir düğümle (şirket içi Windows makine) hello mantıksal ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75f86-157">In this walkthrough, you create hello logical gateway with only one node (on-premises Windows machine).</span></span> <span data-ttu-id="75f86-158">Veri Yönetimi ağ geçidi hello ağ geçidi ile birden çok şirket içi makineler ilişkilendirerek ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75f86-158">You can scale out a data management gateway by associating multiple on-premises machines with hello gateway.</span></span> <span data-ttu-id="75f86-159">Ölçeklendirmek yukarı bir düğümde aynı anda çalıştırabilirsiniz veri taşıma işlerinin sayısını artırarak.</span><span class="sxs-lookup"><span data-stu-id="75f86-159">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="75f86-160">Bu özellik, tek bir düğüme sahip mantıksal bir ağ geçidi için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="75f86-160">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="75f86-161">Bkz: [ölçeklendirme veri yönetimi ağ geçidi Azure veri fabrikası'nda](data-factory-data-management-gateway-high-availability-scalability.md) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="75f86-161">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>  
4. <span data-ttu-id="75f86-162">Merhaba, **yapılandırma** sayfasında, **doğrudan bu bilgisayar Yükle**.</span><span class="sxs-lookup"><span data-stu-id="75f86-162">In hello **Configure** page, click **Install directly on this computer**.</span></span> <span data-ttu-id="75f86-163">Bu eylem hello ağ geçidi için hello yükleme paketi indirir, yükler, yapılandırır ve hello bilgisayarda hello ağ geçidi kaydeder.</span><span class="sxs-lookup"><span data-stu-id="75f86-163">This action downloads hello installation package for hello gateway, installs, configures, and registers hello gateway on hello computer.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="75f86-164">Internet Explorer veya Microsoft ClickOnce uyumlu bir web tarayıcısı kullanın.</span><span class="sxs-lookup"><span data-stu-id="75f86-164">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>
   >
   > <span data-ttu-id="75f86-165">Chrome kullanıyorsanız, toohello Git [Chrome web mağazası](https://chrome.google.com/webstore/), arama "ClickOnce" sözcüğünü, hello ClickOnce uzantıları birini seçin ve yükleyin.</span><span class="sxs-lookup"><span data-stu-id="75f86-165">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
   >
   > <span data-ttu-id="75f86-166">Firefox (yükleme eklenti) aynı hello.</span><span class="sxs-lookup"><span data-stu-id="75f86-166">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="75f86-167">Tıklatın **menü Aç** hello araç çubuğunda (**üç yatay çizgi** hello sağ üst köşesinde), tıklatın **eklentileri**, arama "ClickOnce" sözcüğünü, hello birini seçin ClickOnce uzantıları ve yükleyin.</span><span class="sxs-lookup"><span data-stu-id="75f86-167">Click **Open Menu** button on hello toolbar (**three horizontal lines** in hello top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>    
   >
   >

    ![Ağ geçidi - yapılandırma sayfası](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    <span data-ttu-id="75f86-169">Bu, en kolay yolu (tek tıklatmayla) toodownload Merhaba, yüklemek, yapılandırmak ve tek tek adımda hello ağ geçidini kaydetmek yoludur.</span><span class="sxs-lookup"><span data-stu-id="75f86-169">This way is hello easiest way (one-click) toodownload, install, configure, and register hello gateway in one single step.</span></span> <span data-ttu-id="75f86-170">Merhaba görebilirsiniz **Microsoft Veri Yönetimi ağ geçidi Yapılandırma Yöneticisi** uygulaması bilgisayarınızda yüklü.</span><span class="sxs-lookup"><span data-stu-id="75f86-170">You can see hello **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span></span> <span data-ttu-id="75f86-171">Merhaba yürütülebilir bulabileceğiniz **ConfigManager.exe** hello klasöründeki: **C:\Program Files\Microsoft veri yönetimi Gateway\2.0\Shared**.</span><span class="sxs-lookup"><span data-stu-id="75f86-171">You can also find hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span></span>

    <span data-ttu-id="75f86-172">Ayrıca indirebilir ve bu sayfada hello bağlantıları kullanarak ağ geçidini el ile yükleyin ve hello gösterilen hello anahtarı kullanarak kaydetmek **yeni anahtar** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="75f86-172">You can also download and install gateway manually by using hello links in this page and register it using hello key shown in hello **NEW KEY** text box.</span></span>

    <span data-ttu-id="75f86-173">Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) tüm hello ağ geçidi ayrıntılarını hello için makalesi.</span><span class="sxs-lookup"><span data-stu-id="75f86-173">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all hello details about hello gateway.</span></span>

   > [!NOTE]
   > <span data-ttu-id="75f86-174">Merhaba yerel bilgisayar tooinstall yönetici olmanız ve hello veri yönetimi ağ geçidi başarılı bir şekilde yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="75f86-174">You must be an administrator on hello local computer tooinstall and configure hello Data Management Gateway successfully.</span></span> <span data-ttu-id="75f86-175">Ek kullanıcılar toohello ekleyebilirsiniz **veri yönetimi ağ geçidi kullanıcıları** yerel Windows grubu.</span><span class="sxs-lookup"><span data-stu-id="75f86-175">You can add additional users toohello **Data Management Gateway Users** local Windows group.</span></span> <span data-ttu-id="75f86-176">Bu grubun üyeleri Hello hello veri yönetimi ağ geçidi Yapılandırma Yöneticisi Aracı tooconfigure hello ağ geçidi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75f86-176">hello members of this group can use hello Data Management Gateway Configuration Manager tool tooconfigure hello gateway.</span></span>
   >
   >
5. <span data-ttu-id="75f86-177">Birkaç dakika bekleyin ya da bildirim iletisi aşağıdaki hello görene kadar bekleyin:</span><span class="sxs-lookup"><span data-stu-id="75f86-177">Wait for a couple of minutes or wait until you see hello following notification message:</span></span>

    ![Ağ geçidi yükleme başarılı](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. <span data-ttu-id="75f86-179">Başlatma **veri yönetimi ağ geçidi Yapılandırma Yöneticisi** bilgisayarınızdaki uygulama.</span><span class="sxs-lookup"><span data-stu-id="75f86-179">Launch **Data Management Gateway Configuration Manager** application on your computer.</span></span> <span data-ttu-id="75f86-180">Merhaba, **arama** penceresinde, türü **veri yönetimi ağ geçidi** tooaccess bu yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="75f86-180">In hello **Search** window, type **Data Management Gateway** tooaccess this utility.</span></span> <span data-ttu-id="75f86-181">Merhaba yürütülebilir bulabileceğiniz **ConfigManager.exe** hello klasöründeki: **C:\Program Files\Microsoft veri yönetim Gateway\2.0\Shared**</span><span class="sxs-lookup"><span data-stu-id="75f86-181">You can also find hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span></span>

    ![Ağ geçidi Yapılandırma Yöneticisi](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. <span data-ttu-id="75f86-183">Gördüğünüzü onaylayın `adftutorialgateway is connected toohello cloud service` ileti.</span><span class="sxs-lookup"><span data-stu-id="75f86-183">Confirm that you see `adftutorialgateway is connected toohello cloud service` message.</span></span> <span data-ttu-id="75f86-184">Durum çubuğu hello alt görüntüler Hello **bağlı toohello bulut hizmeti** ile birlikte bir **yeşil onay işareti**.</span><span class="sxs-lookup"><span data-stu-id="75f86-184">hello status bar hello bottom displays **Connected toohello cloud service** along with a **green check mark**.</span></span>

    <span data-ttu-id="75f86-185">Merhaba üzerinde **giriş** sekmesinde de yapabilirsiniz hello işlemleri:</span><span class="sxs-lookup"><span data-stu-id="75f86-185">On hello **Home** tab, you can also do hello following operations:</span></span>

   * <span data-ttu-id="75f86-186">**Kayıt** bir ağ geçidi bir anahtarla hello hello kayıt düğmesini kullanarak Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="75f86-186">**Register** a gateway with a key from hello Azure portal by using hello Register button.</span></span>
   * <span data-ttu-id="75f86-187">**Durdur** veri yönetimi ağ geçidi ana bilgisayar hizmeti, ağ geçidi makine üzerinde çalışan hello.</span><span class="sxs-lookup"><span data-stu-id="75f86-187">**Stop** hello Data Management Gateway Host Service running on your gateway machine.</span></span>
   * <span data-ttu-id="75f86-188">**Zamanlama güncelleştirmeleri** toobe hello günün belirli bir zamanda yüklü.</span><span class="sxs-lookup"><span data-stu-id="75f86-188">**Schedule updates** toobe installed at a specific time of hello day.</span></span>
   * <span data-ttu-id="75f86-189">Merhaba ağ geçidi olduğu zaman görüntülemek **son güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="75f86-189">View when hello gateway was **last updated**.</span></span>
   * <span data-ttu-id="75f86-190">Bir güncelleştirme toohello ağ geçidi yüklenebilmesi için süreyi belirtin.</span><span class="sxs-lookup"><span data-stu-id="75f86-190">Specify time at which an update toohello gateway can be installed.</span></span>
8. <span data-ttu-id="75f86-191">Geçiş toohello **ayarları** hello belirtilen sekmesini hello sertifikası **sertifika** hello portalında belirttiğiniz hello şirket içi veri deposu için kullanılan tooencrypt/şifre çözme kimlik bilgilerini bir bölümdür.</span><span class="sxs-lookup"><span data-stu-id="75f86-191">Switch toohello **Settings** tab. hello certificate specified in hello **Certificate** section is used tooencrypt/decrypt credentials for hello on-premises data store that you specify on hello portal.</span></span> <span data-ttu-id="75f86-192">(isteğe bağlı) Tıklatın **değişiklik** toouse kullanarak kendi sertifikanızı yerine.</span><span class="sxs-lookup"><span data-stu-id="75f86-192">(optional) Click **Change** toouse your own certificate instead.</span></span> <span data-ttu-id="75f86-193">Varsayılan olarak, hello ağ geçidi hello Data Factory hizmeti tarafından otomatik olarak oluşturulan hello sertifika kullanır.</span><span class="sxs-lookup"><span data-stu-id="75f86-193">By default, hello gateway uses hello certificate that is auto-generated by hello Data Factory service.</span></span>

    ![Ağ geçidi sertifika yapılandırma](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    <span data-ttu-id="75f86-195">Ayrıca yapabilirsiniz hello hello eylemleri aşağıdaki **ayarları** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="75f86-195">You can also do hello following actions on hello **Settings** tab:</span></span>

   * <span data-ttu-id="75f86-196">Görüntülemek veya hello ağ geçidi tarafından kullanılan hello sertifikayı dışa aktarın.</span><span class="sxs-lookup"><span data-stu-id="75f86-196">View or export hello certificate being used by hello gateway.</span></span>
   * <span data-ttu-id="75f86-197">Merhaba HTTPS uç noktası Hello ağ geçidi tarafından kullanılan değiştirin.</span><span class="sxs-lookup"><span data-stu-id="75f86-197">Change hello HTTPS endpoint used by hello gateway.</span></span>    
   * <span data-ttu-id="75f86-198">Merhaba ağ geçidi tarafından kullanılan bir HTTP proxy toobe ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="75f86-198">Set an HTTP proxy toobe used by hello gateway.</span></span>     
9. <span data-ttu-id="75f86-199">(isteğe bağlı) Geçiş toohello **tanılama** sekmesinde, hello denetleyin **ayrıntılı günlük kaydını etkinleştir** tooenable ayrıntılı tootroubleshoot hello ağ geçidi ile ilgili sorunları kullanabilirsiniz günlüğü istiyorsanız seçeneği.</span><span class="sxs-lookup"><span data-stu-id="75f86-199">(optional) Switch toohello **Diagnostics** tab, check hello **Enable verbose logging** option if you want tooenable verbose logging that you can use tootroubleshoot any issues with hello gateway.</span></span> <span data-ttu-id="75f86-200">Merhaba günlük bilgileri bulunabilir **Olay Görüntüleyicisi'ni** altında **uygulama ve hizmet günlükleri** -> **veri yönetimi ağ geçidi** düğümü.</span><span class="sxs-lookup"><span data-stu-id="75f86-200">hello logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span></span>

    ![Tanılama sekmesi](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    <span data-ttu-id="75f86-202">Merhaba eylemleri aşağıdaki hello de gerçekleştirebilirsiniz **tanılama** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="75f86-202">You can also perform hello following actions in hello **Diagnostics** tab:</span></span>

   * <span data-ttu-id="75f86-203">Kullanım **Bağlantıyı Sına** bölüm tooan şirket içi veri kaynağı hello ağ geçidini kullanma.</span><span class="sxs-lookup"><span data-stu-id="75f86-203">Use **Test Connection** section tooan on-premises data source using hello gateway.</span></span>
   * <span data-ttu-id="75f86-204">Tıklatın **günlüklerini görüntüle** toosee hello veri yönetimi ağ geçidi bir Olay Görüntüleyici'de oturum açın.</span><span class="sxs-lookup"><span data-stu-id="75f86-204">Click **View Logs** toosee hello Data Management Gateway log in an Event Viewer window.</span></span>
   * <span data-ttu-id="75f86-205">Tıklatın **günlükleri Gönder** tooupload son yedi gün tooMicrosoft toofacilitate sorunları, sorun giderme günlük içeren bir zip dosyası.</span><span class="sxs-lookup"><span data-stu-id="75f86-205">Click **Send Logs** tooupload a zip file with logs of last seven days tooMicrosoft toofacilitate troubleshooting of your issues.</span></span>
10. <span data-ttu-id="75f86-206">Merhaba üzerinde **tanılama** sekmede hello **Bağlantıyı Sına** bölümünde, select **SqlServer** hello veri hello türü için depolamak, hello ad hello veritabanı sunucusunun adını girin Merhaba veritabanı, kimlik doğrulama türünü belirtin, kullanıcı adı ve parola girin ve tıklatın **Test** tootest hello ağ geçidi toohello veritabanı olup bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="75f86-206">On hello **Diagnostics** tab, in hello **Test Connection** section, select **SqlServer** for hello type of hello data store, enter hello name of hello database server, name of hello database, specify authentication type, enter user name, and password, and click **Test** tootest whether hello gateway can connect toohello database.</span></span>
11. <span data-ttu-id="75f86-207">Anahtar toohello web tarayıcısı ve hello **Azure portal**, tıklatın **Tamam** hello üzerinde **yapılandırma** sayfa ve ardından hello **yeni veri ağ geçidi** Sayfa.</span><span class="sxs-lookup"><span data-stu-id="75f86-207">Switch toohello web browser, and in hello **Azure portal**, click **OK** on hello **Configure** page and then on hello **New data gateway** page.</span></span>
12. <span data-ttu-id="75f86-208">Görmeniz gerekir **adftutorialgateway** altında **Data Gateways** hello hello soldaki ağaç görünümünde.</span><span class="sxs-lookup"><span data-stu-id="75f86-208">You should see **adftutorialgateway** under **Data Gateways** in hello tree view on hello left.</span></span>  <span data-ttu-id="75f86-209">Tıklarsanız, JSON hello ilişkili görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="75f86-209">If you click it, you should see hello associated JSON.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="75f86-210">Bağlı hizmetler oluşturma</span><span class="sxs-lookup"><span data-stu-id="75f86-210">Create linked services</span></span>
<span data-ttu-id="75f86-211">Bu adımda, iki bağlı hizmet oluşturma: **AzureStorageLinkedService** ve **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="75f86-211">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span></span> <span data-ttu-id="75f86-212">Merhaba **SqlServerLinkedService** bir şirket içi SQL Server veritabanı ve hello bağlantılar **AzureStorageLinkedService** bağlantılı hizmeti bir Azure blob depolama toohello data factory bağlar.</span><span class="sxs-lookup"><span data-stu-id="75f86-212">hello **SqlServerLinkedService** links an on-premises SQL Server database and hello **AzureStorageLinkedService** linked service links an Azure blob store toohello data factory.</span></span> <span data-ttu-id="75f86-213">Merhaba şirket içi SQL Server veritabanı toohello Azure blob depolama alanından verileri kopyalayan daha sonra bu kılavuzda bir işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75f86-213">You create a pipeline later in this walkthrough that copies data from hello on-premises SQL Server database toohello Azure blob store.</span></span>

#### <a name="add-a-linked-service-tooan-on-premises-sql-server-database"></a><span data-ttu-id="75f86-214">Bağlantılı hizmet tooan şirket içi SQL Server veritabanı ekleyin</span><span class="sxs-lookup"><span data-stu-id="75f86-214">Add a linked service tooan on-premises SQL Server database</span></span>
1. <span data-ttu-id="75f86-215">Merhaba, **Data Factory düzenleyici**, tıklatın **yeni veri deposu** hello araç ve seçim **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="75f86-215">In hello **Data Factory Editor**, click **New data store** on hello toolbar and select **SQL Server**.</span></span>

   ![Yeni SQL Server bağlantılı hizmeti](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. <span data-ttu-id="75f86-217">Merhaba, **JSON Düzenleyicisi** sağ hello üzerinde adımları hello:</span><span class="sxs-lookup"><span data-stu-id="75f86-217">In hello **JSON editor** on hello right, do hello following steps:</span></span>

   1. <span data-ttu-id="75f86-218">Hello için **gatewayName**, belirtin **adftutorialgateway**.</span><span class="sxs-lookup"><span data-stu-id="75f86-218">For hello **gatewayName**, specify **adftutorialgateway**.</span></span>    
   2. <span data-ttu-id="75f86-219">Merhaba, **connectionString**, adımları hello:</span><span class="sxs-lookup"><span data-stu-id="75f86-219">In hello **connectionString**, do hello following steps:</span></span>    

      1. <span data-ttu-id="75f86-220">İçin **servername**, hello hello SQL Server veritabanını barındıran hello sunucusunun adını girin.</span><span class="sxs-lookup"><span data-stu-id="75f86-220">For **servername**, enter hello name of hello server that hosts hello SQL Server database.</span></span>
      2. <span data-ttu-id="75f86-221">İçin **databasename**, hello hello veritabanının adını girin.</span><span class="sxs-lookup"><span data-stu-id="75f86-221">For **databasename**, enter hello name of hello database.</span></span>
      3. <span data-ttu-id="75f86-222">Tıklatın **şifrele** hello araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="75f86-222">Click **Encrypt** button on hello toolbar.</span></span> <span data-ttu-id="75f86-223">Merhaba kimlik bilgileri Yöneticisi uygulaması bakın.</span><span class="sxs-lookup"><span data-stu-id="75f86-223">You see hello Credentials Manager application.</span></span>

         ![Kimlik bilgileri Yöneticisi uygulaması](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. <span data-ttu-id="75f86-225">Merhaba, **kimlik bilgilerini ayarlama** iletişim kutusunda, kimlik doğrulama türü, kullanıcı adı ve parola belirtin ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="75f86-225">In hello **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span></span> <span data-ttu-id="75f86-226">Merhaba bağlantı başarılı olursa, hello JSON depolanan hello şifrelenmiş kimlik bilgileri ve hello iletişim kutusunu kapatır.</span><span class="sxs-lookup"><span data-stu-id="75f86-226">If hello connection is successful, hello encrypted credentials are stored in hello JSON and hello dialog box closes.</span></span>
      5. <span data-ttu-id="75f86-227">Merhaba iletişim kutusu otomatik olarak kapalı, başlatılan ve hello Azure portal ile toohello sekmesine geri dönmek hello boş tarayıcı sekmesinde kapatın.</span><span class="sxs-lookup"><span data-stu-id="75f86-227">Close hello empty browser tab that launched hello dialog box if it is not automatically closed and get back toohello tab with hello Azure portal.</span></span>

         <span data-ttu-id="75f86-228">Merhaba ağ geçidi makinesinde, bu kimlik bilgileri olan **şifrelenmiş** Data Factory hello bir sertifika kullanarak hizmetin sahibi.</span><span class="sxs-lookup"><span data-stu-id="75f86-228">On hello gateway machine, these credentials are **encrypted** by using a certificate that hello Data Factory service owns.</span></span> <span data-ttu-id="75f86-229">Bunun yerine hello veri yönetimi ağ geçidi ile ilişkili toouse hello sertifikası istiyorsanız, bkz: [kimlik bilgilerini güvenli bir şekilde ayarlamak](#set-credentials-and-security).</span><span class="sxs-lookup"><span data-stu-id="75f86-229">If you want toouse hello certificate that is associated with hello Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span></span>    
   3. <span data-ttu-id="75f86-230">Tıklatın **dağıtma** toodeploy hello SQL Server bağlantılı hizmet çubuğu hello komutu.</span><span class="sxs-lookup"><span data-stu-id="75f86-230">Click **Deploy** on hello command bar toodeploy hello SQL Server linked service.</span></span> <span data-ttu-id="75f86-231">Merhaba bağlantılı hizmet hello ağaç görünümünde görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="75f86-231">You should see hello linked service in hello tree view.</span></span>

      ![SQL Server bağlantılı hizmet hello ağaç görünümünde](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="75f86-233">Bir Azure depolama hesabı için bağlı hizmet ekleme</span><span class="sxs-lookup"><span data-stu-id="75f86-233">Add a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="75f86-234">Merhaba, **Data Factory düzenleyici**, tıklatın **yeni veri deposu** hello komut çubuğu ve tıklatın **Azure depolama**.</span><span class="sxs-lookup"><span data-stu-id="75f86-234">In hello **Data Factory Editor**, click **New data store** on hello command bar and click **Azure storage**.</span></span>
2. <span data-ttu-id="75f86-235">Merhaba, Azure depolama hesabınızın hello adı **hesap adı**.</span><span class="sxs-lookup"><span data-stu-id="75f86-235">Enter hello name of your Azure storage account for hello **Account name**.</span></span>
3. <span data-ttu-id="75f86-236">Merhaba, Azure depolama hesabınız için Hello anahtarını girin **hesap anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="75f86-236">Enter hello key for your Azure storage account for hello **Account key**.</span></span>
4. <span data-ttu-id="75f86-237">Tıklatın **dağıtma** toodeploy hello **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="75f86-237">Click **Deploy** toodeploy hello **AzureStorageLinkedService**.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="75f86-238">Veri kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="75f86-238">Create datasets</span></span>
<span data-ttu-id="75f86-239">Bu adımda, girdi oluşturun ve çıkış hello kopyalama işlemi için girdi ve çıktı verilerini temsil eden veri kümeleri (şirket içi SQL Server veritabanı = > Azure blob depolama).</span><span class="sxs-lookup"><span data-stu-id="75f86-239">In this step, you create input and output datasets that represent input and output data for hello copy operation (On-premises SQL Server database => Azure blob storage).</span></span> <span data-ttu-id="75f86-240">Veri kümeleri oluşturmadan önce aşağıdaki adımları (ayrıntılı adımları izler hello listesi) hello:</span><span class="sxs-lookup"><span data-stu-id="75f86-240">Before creating datasets, do hello following steps (detailed steps follows hello list):</span></span>

* <span data-ttu-id="75f86-241">Adlı bir tablo oluşturmak **emp** SQL Server veritabanı bağlantılı hizmet toohello veri fabrikası eklediğiniz hello ve birkaç örnek girdileri hello tabloya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="75f86-241">Create a table named **emp** in hello SQL Server Database you added as a linked service toohello data factory and insert a couple of sample entries into hello table.</span></span>
* <span data-ttu-id="75f86-242">Adlı bir blob kapsayıcı oluşturun **adftutorial** hello Azure blob depolama hesabı bir bağlantılı hizmet toohello veri fabrikası eklendi.</span><span class="sxs-lookup"><span data-stu-id="75f86-242">Create a blob container named **adftutorial** in hello Azure blob storage account you added as a linked service toohello data factory.</span></span>

### <a name="prepare-on-premises-sql-server-for-hello-tutorial"></a><span data-ttu-id="75f86-243">Şirket içi SQL Server hello öğretici için hazırlama</span><span class="sxs-lookup"><span data-stu-id="75f86-243">Prepare On-premises SQL Server for hello tutorial</span></span>
1. <span data-ttu-id="75f86-244">Merhaba içi SQL Server için belirttiğiniz hello veritabanında bağlantılı hizmetinin (**SqlServerLinkedService**), aşağıdaki SQL komut dosyası toocreate hello hello kullan **emp** hello veritabanındaki tablo.</span><span class="sxs-lookup"><span data-stu-id="75f86-244">In hello database you specified for hello on-premises SQL Server linked service (**SqlServerLinkedService**), use hello following SQL script toocreate hello **emp** table in hello database.</span></span>

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. <span data-ttu-id="75f86-245">Bazı örnek hello tabloya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="75f86-245">Insert some sample into hello table:</span></span>

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a><span data-ttu-id="75f86-246">Girdi veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="75f86-246">Create input dataset</span></span>

1. <span data-ttu-id="75f86-247">Merhaba, **Data Factory düzenleyici**, tıklatın **... Daha fazla**, tıklatın **yeni veri kümesi** hello komut çubuğunda ve'ı tıklatın **SQL Server tablosuna**.</span><span class="sxs-lookup"><span data-stu-id="75f86-247">In hello **Data Factory Editor**, click **... More**, click **New dataset** on hello command bar, and click **SQL Server table**.</span></span>
2. <span data-ttu-id="75f86-248">Merhaba sağ bölmedeki JSON Hello metin aşağıdaki hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="75f86-248">Replace hello JSON in hello right pane with hello following text:</span></span>

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   <span data-ttu-id="75f86-249">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="75f86-249">Note hello following points:</span></span>

   * <span data-ttu-id="75f86-250">**tür** çok ayarlanır**SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="75f86-250">**type** is set too**SqlServerTable**.</span></span>
   * <span data-ttu-id="75f86-251">**tableName** çok ayarlanır**emp**.</span><span class="sxs-lookup"><span data-stu-id="75f86-251">**tableName** is set too**emp**.</span></span>
   * <span data-ttu-id="75f86-252">**linkedServiceName** çok ayarlanır**SqlServerLinkedService** (Bu kılavuzda daha önce bu bağlı hizmetin oluşturmuştunuz.).</span><span class="sxs-lookup"><span data-stu-id="75f86-252">**linkedServiceName** is set too**SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span></span>
   * <span data-ttu-id="75f86-253">Azure Data Factory başka bir ardışık düzen tarafından üretilen olmayan bir giriş veri kümesi için ayarlamalısınız **dış** çok**doğru**.</span><span class="sxs-lookup"><span data-stu-id="75f86-253">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** too**true**.</span></span> <span data-ttu-id="75f86-254">Bu, üretilen dış toohello Azure Data Factory hizmetine hello giriş verisi olduğu gösterir.</span><span class="sxs-lookup"><span data-stu-id="75f86-254">It denotes hello input data is produced external toohello Azure Data Factory service.</span></span> <span data-ttu-id="75f86-255">İsteğe bağlı olarak hello kullanarak tüm dış veri ilkeleri belirtebilirsiniz **externalData** hello öğesinde **İlkesi** bölümü.</span><span class="sxs-lookup"><span data-stu-id="75f86-255">You can optionally specify any external data policies using hello **externalData** element in hello **Policy** section.</span></span>    

   <span data-ttu-id="75f86-256">Bkz: [/SQL Server'dan veri taşıma](data-factory-sqlserver-connector.md) JSON özellikleri hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="75f86-256">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="75f86-257">Tıklatın **dağıtma** toodeploy hello dataset çubuğu hello komutu.</span><span class="sxs-lookup"><span data-stu-id="75f86-257">Click **Deploy** on hello command bar toodeploy hello dataset.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="75f86-258">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="75f86-258">Create output dataset</span></span>

1. <span data-ttu-id="75f86-259">Merhaba, **Data Factory düzenleyici**, tıklatın **yeni veri kümesi** hello komut çubuğunda ve'ı tıklatın **Azure Blob Depolama**.</span><span class="sxs-lookup"><span data-stu-id="75f86-259">In hello **Data Factory Editor**, click **New dataset** on hello command bar, and click **Azure Blob storage**.</span></span>
2. <span data-ttu-id="75f86-260">Merhaba sağ bölmedeki JSON Hello metin aşağıdaki hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="75f86-260">Replace hello JSON in hello right pane with hello following text:</span></span>

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   <span data-ttu-id="75f86-261">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="75f86-261">Note hello following points:</span></span>

   * <span data-ttu-id="75f86-262">**tür** çok ayarlanır**AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="75f86-262">**type** is set too**AzureBlob**.</span></span>
   * <span data-ttu-id="75f86-263">**linkedServiceName** çok ayarlanır**AzureStorageLinkedService** (Bu bağlı hizmeti 2. adımda oluşturmuştunuz).</span><span class="sxs-lookup"><span data-stu-id="75f86-263">**linkedServiceName** is set too**AzureStorageLinkedService** (you had created this linked service in Step 2).</span></span>
   * <span data-ttu-id="75f86-264">**folderPath** çok ayarlanır**adftutorial/outfromonpremdf** outfromonpremdf hello adftutorial kapsayıcı hello klasöründe olduğu.</span><span class="sxs-lookup"><span data-stu-id="75f86-264">**folderPath** is set too**adftutorial/outfromonpremdf** where outfromonpremdf is hello folder in hello adftutorial container.</span></span> <span data-ttu-id="75f86-265">Merhaba oluşturma **adftutorial** zaten yoksa, kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="75f86-265">Create hello **adftutorial** container if it does not already exist.</span></span>
   * <span data-ttu-id="75f86-266">Merhaba **kullanılabilirlik** çok ayarlanır**saatlik** (**sıklığı** çok ayarlamak**saat** ve **aralığı** çok ayarlama **1**).</span><span class="sxs-lookup"><span data-stu-id="75f86-266">hello **availability** is set too**hourly** (**frequency** set too**hour** and **interval** set too**1**).</span></span>  <span data-ttu-id="75f86-267">Merhaba Data Factory hizmetinin her saat bir çıktı veri dilimi hello oluşturur **emp** hello Azure SQL veritabanı tablosunda.</span><span class="sxs-lookup"><span data-stu-id="75f86-267">hello Data Factory service generates an output data slice every hour in hello **emp** table in hello Azure SQL Database.</span></span>

   <span data-ttu-id="75f86-268">Belirtmezseniz, bir **fileName** için bir **çıktı tablosu**, hello oluşturulan hello dosyalarında **folderPath** biçimini izleyen hello adlı: veri.<Guid>. txt (örneğin:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="75f86-268">If you do not specify a **fileName** for an **output table**, hello generated files in hello **folderPath** are named in hello following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="75f86-269">tooset **folderPath** ve **fileName** hello göre dinamik olarak **SliceStart** zaman, hello partitionedBy özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="75f86-269">tooset **folderPath** and **fileName** dynamically based on hello **SliceStart** time, use hello partitionedBy property.</span></span> <span data-ttu-id="75f86-270">Hello, aşağıdaki örnekte, folderPath yıl, ay ve gün hello SliceStart (başlangıç saati hello dilimin işlenmekte olan) ve fileName saat SliceStart hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="75f86-270">In hello following example, folderPath uses Year, Month, and Day from hello SliceStart (start time of hello slice being processed) and fileName uses Hour from hello SliceStart.</span></span> <span data-ttu-id="75f86-271">Örneğin, dilim 2014 için üretilen-10-20T08:00:00, hello KlasörAdı toowikidatagateway/wikisampledataout/2014/10/20 ayarlanır ve hello fileName too08.csv ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="75f86-271">For example, if a slice is being produced for 2014-10-20T08:00:00, hello folderName is set toowikidatagateway/wikisampledataout/2014/10/20 and hello fileName is set too08.csv.</span></span>

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    <span data-ttu-id="75f86-272">Bkz: [/Azure Blob storage'da veri taşıma](data-factory-azure-blob-connector.md) JSON özellikleri hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="75f86-272">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="75f86-273">Tıklatın **dağıtma** toodeploy hello dataset çubuğu hello komutu.</span><span class="sxs-lookup"><span data-stu-id="75f86-273">Click **Deploy** on hello command bar toodeploy hello dataset.</span></span> <span data-ttu-id="75f86-274">Her iki hello veri kümeleri hello ağaç görünümünde gördüğünüzü onaylayın.</span><span class="sxs-lookup"><span data-stu-id="75f86-274">Confirm that you see both hello datasets in hello tree view.</span></span>  

## <a name="create-pipeline"></a><span data-ttu-id="75f86-275">İşlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="75f86-275">Create pipeline</span></span>
<span data-ttu-id="75f86-276">Bu adımda, oluşturduğunuz bir **ardışık düzen** biriyle **kopyalama etkinliği** kullanan **EmpOnPremSQLTable** giriş olarak ve **OutputBlobTable** olarak çıktı.</span><span class="sxs-lookup"><span data-stu-id="75f86-276">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span></span>

1. <span data-ttu-id="75f86-277">Veri Fabrikası Düzenleyicisi'nde tıklatın **... Daha fazla** ve **Yeni işlem hattı** öğelerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="75f86-277">In Data Factory Editor, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="75f86-278">Merhaba sağ bölmedeki JSON Hello metin aşağıdaki hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="75f86-278">Replace hello JSON in hello right pane with hello following text:</span></span>    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL tooAzure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server tooblob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
               }
             },
             "Policy": {
               "concurrency": 1,
               "executionPriorityOrder": "NewestFirst",
               "style": "StartOfInterval",
               "retry": 0,
               "timeout": "01:00:00"
             }
           }
         ],
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > <span data-ttu-id="75f86-279">Merhaba Hello değerini değiştirin **Başlat** hello geçerli gün özelliğiyle ve **son** hello sonraki gün değeri.</span><span class="sxs-lookup"><span data-stu-id="75f86-279">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span>
   >
   >

   <span data-ttu-id="75f86-280">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="75f86-280">Note hello following points:</span></span>

   * <span data-ttu-id="75f86-281">Merhaba etkinlikler bölümünde, yalnızca etkinliği yoktur, **türü** çok ayarlanır**kopya**.</span><span class="sxs-lookup"><span data-stu-id="75f86-281">In hello activities section, there is only activity whose **type** is set too**Copy**.</span></span>
   * <span data-ttu-id="75f86-282">**Giriş** hello etkinlik çok ayarlamak için**EmpOnPremSQLTable** ve **çıkış** hello etkinlik çok ayarlamak için**OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="75f86-282">**Input** for hello activity is set too**EmpOnPremSQLTable** and **output** for hello activity is set too**OutputBlobTable**.</span></span>
   * <span data-ttu-id="75f86-283">Merhaba, **typeProperties** bölümünde **SqlSource** hello belirtilen **kaynak türünü** ve ** BlobSink ** hello belirtilen **Havuz türü**.</span><span class="sxs-lookup"><span data-stu-id="75f86-283">In hello **typeProperties** section, **SqlSource** is specified as hello **source type** and **BlobSink **is specified as hello **sink type**.</span></span>
   * <span data-ttu-id="75f86-284">SQL sorgusu `select * from emp` Merhaba belirtilen **sqlReaderQuery** özelliği **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="75f86-284">SQL query `select * from emp` is specified for hello **sqlReaderQuery** property of **SqlSource**.</span></span>

   <span data-ttu-id="75f86-285">Başlangıç ve bitiş tarih saatleri [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601) olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="75f86-285">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="75f86-286">Örneğin: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="75f86-286">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="75f86-287">Merhaba **son** saati isteğe bağlıdır ancak biz Bu öğreticide kullanın.</span><span class="sxs-lookup"><span data-stu-id="75f86-287">hello **end** time is optional, but we use it in this tutorial.</span></span>

   <span data-ttu-id="75f86-288">Hello için değer belirtmezseniz, **son** özelliği olarak hesaplanır "**start + 48 saat**".</span><span class="sxs-lookup"><span data-stu-id="75f86-288">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="75f86-289">toorun hello ardışık kalıcı olarak belirtmek **9/9/9999** hello hello değeri olarak **son** özelliği.</span><span class="sxs-lookup"><span data-stu-id="75f86-289">toorun hello pipeline indefinitely, specify **9/9/9999** as hello value for hello **end** property.</span></span>

   <span data-ttu-id="75f86-290">Merhaba üzerinde göre hangi hello veri dilimleri işlenir süre hello tanımlama **kullanılabilirlik** her Azure Data Factory veri kümesi için tanımlanan özellikler.</span><span class="sxs-lookup"><span data-stu-id="75f86-290">You are defining hello time duration in which hello data slices are processed based on hello **Availability** properties that were defined for each Azure Data Factory dataset.</span></span>

   <span data-ttu-id="75f86-291">Merhaba örnekte vardır 24 veri dilimi her veri dilimi saatlik oluşturulduğundan.</span><span class="sxs-lookup"><span data-stu-id="75f86-291">In hello example, there are 24 data slices as each data slice is produced hourly.</span></span>        
3. <span data-ttu-id="75f86-292">Tıklatın **dağıtma** toodeploy hello dataset çubuğu hello komutunda (tablo dikdörtgen bir veri kümesi olur).</span><span class="sxs-lookup"><span data-stu-id="75f86-292">Click **Deploy** on hello command bar toodeploy hello dataset (table is a rectangular dataset).</span></span> <span data-ttu-id="75f86-293">Altında hello ağaç görünümünde bu hello ardışık düzen görüntülenir onaylayın **ardışık düzen** düğümü.</span><span class="sxs-lookup"><span data-stu-id="75f86-293">Confirm that hello pipeline shows up in hello tree view under **Pipelines** node.</span></span>  
4. <span data-ttu-id="75f86-294">Şimdi, **X** iki kez tooclose hello sayfa tooget geri toohello **Data Factory** hello için sayfa **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="75f86-294">Now, click **X** twice tooclose hello page tooget back toohello **Data Factory** page for hello **ADFTutorialOnPremDF**.</span></span>

<span data-ttu-id="75f86-295">**Tebrikler!**</span><span class="sxs-lookup"><span data-stu-id="75f86-295">**Congratulations!**</span></span> <span data-ttu-id="75f86-296">Bir Azure data factory, bağlı hizmetler, veri kümeleri ve ardışık düzen ve zamanlanmış hello ardışık düzen başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="75f86-296">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled hello pipeline.</span></span>

#### <a name="view-hello-data-factory-in-a-diagram-view"></a><span data-ttu-id="75f86-297">Görünüm hello data factory'de bir diyagram görünümü</span><span class="sxs-lookup"><span data-stu-id="75f86-297">View hello data factory in a Diagram View</span></span>
1. <span data-ttu-id="75f86-298">Merhaba, **Azure portal**, tıklatın **diyagramı** döşeme hello hello giriş sayfasında **ADFTutorialOnPremDF** veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="75f86-298">In hello **Azure portal**, click **Diagram** tile on hello home page for hello **ADFTutorialOnPremDF** data factory.</span></span> <span data-ttu-id="75f86-299">:</span><span class="sxs-lookup"><span data-stu-id="75f86-299">:</span></span>

    ![Diyagram bağlantı](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. <span data-ttu-id="75f86-301">Merhaba diyagramı benzer toohello görüntü aşağıdaki görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="75f86-301">You should see hello diagram similar toohello following image:</span></span>

    ![Diyagram Görünümü](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    <span data-ttu-id="75f86-303">Yakınlaştırma, yakınlaştırma too100% yakınlaştırma toofit, otomatik olarak konumu ardışık düzen ve veri kümeleri, yakınlaştırma ve çizgileri gösterebilirsiniz (Seçilen öğelerin Yukarı Akış ve aşağı akış öğelerini vurgular).</span><span class="sxs-lookup"><span data-stu-id="75f86-303">You can zoom in, zoom out, zoom too100%, zoom toofit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="75f86-304">Bir nesne (giriş/çıkış veri kümesi veya işlem hattı) toosee özellikleri için çift tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75f86-304">You can double-click an object (input/output dataset or pipeline) toosee properties for it.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="75f86-305">İşlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="75f86-305">Monitor pipeline</span></span>
<span data-ttu-id="75f86-306">Bu adımda, bir Azure data factory'de neler olduğunu Azure portal toomonitor hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="75f86-306">In this step, you use hello Azure portal toomonitor what’s going on in an Azure data factory.</span></span> <span data-ttu-id="75f86-307">PowerShell cmdlet'leri toomonitor veri kümeleri ve işlem hatlarını de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75f86-307">You can also use PowerShell cmdlets toomonitor datasets and pipelines.</span></span> <span data-ttu-id="75f86-308">İzleme hakkında daha fazla bilgi için bkz [izleme ve yönetme ardışık düzen](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="75f86-308">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span></span>

1. <span data-ttu-id="75f86-309">Merhaba şemada çift **EmpOnPremSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="75f86-309">In hello diagram, double-click **EmpOnPremSQLTable**.</span></span>  

    ![EmpOnPremSQLTable dilimleri](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. <span data-ttu-id="75f86-311">Tüm hello veri dilimi yukarı bildirimi olan **hazır** hello ardışık düzen süresi (başlangıç zamanı tooend süresi) hello geçmiş olduğundan belirtin.</span><span class="sxs-lookup"><span data-stu-id="75f86-311">Notice that all hello data slices up are in **Ready** state because hello pipeline duration (start time tooend time) is in hello past.</span></span> <span data-ttu-id="75f86-312">Hello SQL Server veritabanında hello veri ekledikten ve tüm hello zaman yoktur çünkü de olabilir.</span><span class="sxs-lookup"><span data-stu-id="75f86-312">It is also because you have inserted hello data in hello SQL Server database and it is there all hello time.</span></span> <span data-ttu-id="75f86-313">Hiç dilim hello gösterilmediğini onaylayın **sorunu dilimleri** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="75f86-313">Confirm that no slices show up in hello **Problem slices** section at hello bottom.</span></span> <span data-ttu-id="75f86-314">Tüm hello dilimler tooview tıklatın **daha görmek** hello altındaki dilimler hello listesi.</span><span class="sxs-lookup"><span data-stu-id="75f86-314">tooview all hello slices, click **See More** at hello bottom of hello list of slices.</span></span>
3. <span data-ttu-id="75f86-315">Merhaba, şimdi **veri kümeleri** sayfasında, **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="75f86-315">Now, In hello **Datasets** page, click **OutputBlobTable**.</span></span>

    ![OputputBlobTable dilimleri](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. <span data-ttu-id="75f86-317">Merhaba listeden herhangi bir veri dilimine tıklayın ve hello görmelisiniz **veri dilimi** sayfası.</span><span class="sxs-lookup"><span data-stu-id="75f86-317">Click any data slice from hello list and you should see hello **Data Slice** page.</span></span> <span data-ttu-id="75f86-318">Merhaba dilimle ilgili etkinlik çalışır bakın.</span><span class="sxs-lookup"><span data-stu-id="75f86-318">You see activity runs for hello slice.</span></span> <span data-ttu-id="75f86-319">Yalnızca bir etkinlik genellikle bakın.</span><span class="sxs-lookup"><span data-stu-id="75f86-319">You see only one activity run usually.</span></span>  

    ![Veri dilimi dikey penceresi](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    <span data-ttu-id="75f86-321">Merhaba dilim hello değilse **hazır** durumu, hazır olmayan ve geçerli dilimin yürütülmesini hello hello engelleme hello Yukarı Akış dilimleri görebilirsiniz **hazır olmayan Yukarı Akış dilimleri** listesi.</span><span class="sxs-lookup"><span data-stu-id="75f86-321">If hello slice is not in hello **Ready** state, you can see hello upstream slices that are not Ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span>
5. <span data-ttu-id="75f86-322">Merhaba tıklatın **etkinlik** hello alt toosee hello listesinden **etkinlik çalışma ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="75f86-322">Click hello **activity run** from hello list at hello bottom toosee **activity run details**.</span></span>

   ![Etkinlik çalışma Ayrıntıları sayfası](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   <span data-ttu-id="75f86-324">Verimlilik, süre ve hello ağ geçidi tootransfer hello veri kullanılan gibi bilgileri görür.</span><span class="sxs-lookup"><span data-stu-id="75f86-324">You would see information such as throughput, duration, and hello gateway used tootransfer hello data.</span></span>
6. <span data-ttu-id="75f86-325">Tıklatın **X** tooclose tüm sayfaları dek hello</span><span class="sxs-lookup"><span data-stu-id="75f86-325">Click **X** tooclose all hello pages until you</span></span>
7. <span data-ttu-id="75f86-326">Merhaba toohello giriş sayfasına geri dönmek **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="75f86-326">get back toohello home page for hello **ADFTutorialOnPremDF**.</span></span>
8. <span data-ttu-id="75f86-327">(isteğe bağlı) ' I tıklatın **ardışık düzen**, tıklatın **ADFTutorialOnPremDF**ve detaya girdi tablolarında (**tüketilen**) veya çıkış veri kümeleri (**üretilen**).</span><span class="sxs-lookup"><span data-stu-id="75f86-327">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span></span>
9. <span data-ttu-id="75f86-328">Gibi araçlar kullanın [Microsoft Storage Gezgini](http://storageexplorer.com/) tooverify her saat için bir blob/dosyası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="75f86-328">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) tooverify that a blob/file is created for each hour.</span></span>

   ![Azure Depolama Gezgini](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a><span data-ttu-id="75f86-330">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="75f86-330">Next steps</span></span>
* <span data-ttu-id="75f86-331">Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) tüm hello veri yönetimi ağ geçidi ayrıntılarını hello için makalesi.</span><span class="sxs-lookup"><span data-stu-id="75f86-331">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all hello details about hello Data Management Gateway.</span></span>
* <span data-ttu-id="75f86-332">Bkz: [SQL Azure Blob tooAzure veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) nasıl toouse kopyalama etkinliği toomove veri kaynağına veri tooa havuz veri deposunu hakkında toolearn.</span><span class="sxs-lookup"><span data-stu-id="75f86-332">See [Copy data from Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn about how toouse Copy Activity toomove data from a source data store tooa sink data store.</span></span>
