---
title: "Data - veri yönetimi ağ geçidi taşıma | Microsoft Docs"
description: "Şirket içi ve bulut arasında veri taşımak için veri ağ geçidi kurun ayarlayın. Veri Yönetimi ağ geçidi Azure Data Factory, verilerinizi taşımak için kullanın."
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
ms.openlocfilehash: 565091e24a8c0009793e2e2365fb95013cad5028
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-between-on-premises-sources-and-the-cloud-with-data-management-gateway"></a><span data-ttu-id="4c72b-105">Şirket içi kaynakları ve veri yönetimi ağ geçidi ile bulut arasında veri taşıma</span><span class="sxs-lookup"><span data-stu-id="4c72b-105">Move data between on-premises sources and the cloud with Data Management Gateway</span></span>
<span data-ttu-id="4c72b-106">Bu makalede, şirket içi veri depoları ve veri fabrikası kullanarak bulut veri depoları arasında veri tümleştirme genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="4c72b-106">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span></span> <span data-ttu-id="4c72b-107">Derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale ve diğer veri fabrikası temel kavramları makaleler: [veri kümeleri](data-factory-create-datasets.md) ve [ardışık düzen](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="4c72b-107">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="data-management-gateway"></a><span data-ttu-id="4c72b-108">Veri Yönetimi Ağ Geçidi</span><span class="sxs-lookup"><span data-stu-id="4c72b-108">Data Management Gateway</span></span>
<span data-ttu-id="4c72b-109">Şirket içi makinenizdeki bir şirket içi veri deposundaki/gruptan veri taşımayı etkinleştirmek için veri yönetimi ağ geçidi yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c72b-109">You must install Data Management Gateway on your on-premises machine to enable moving data to/from an on-premises data store.</span></span> <span data-ttu-id="4c72b-110">Ağ geçidi veri deposuna bağlanabileceği sürece ağ geçidi veri depolama alanı ile aynı makinede veya farklı bir makineye yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="4c72b-110">The gateway can be installed on the same machine as the data store or on a different machine as long as the gateway can connect to the data store.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4c72b-111">Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) makale veri yönetimi ağ geçidi hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="4c72b-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> 

<span data-ttu-id="4c72b-112">Aşağıdaki örneklerde bir şirket içi veri taşır bir komut zinciriyle data factory oluşturmak gösterilmiştir **SQL Server** Azure blob depolama veritabanına.</span><span class="sxs-lookup"><span data-stu-id="4c72b-112">The following walkthrough shows you how to create a data factory with a pipeline that moves data from an on-premises **SQL Server** database to an Azure blob storage.</span></span> <span data-ttu-id="4c72b-113">Adım adım kılavuzun bir parçası olarak makinenize Veri Yönetimi Ağ Geçidi yükleyip bunu yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="4c72b-113">As part of the walkthrough, you install and configure the Data Management Gateway on your machine.</span></span>

## <a name="walkthrough-copy-on-premises-data-to-cloud"></a><span data-ttu-id="4c72b-114">İzlenecek yol: Bulut için şirket içi veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="4c72b-114">Walkthrough: copy on-premises data to cloud</span></span>
<span data-ttu-id="4c72b-115">Bu kılavuzda aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="4c72b-115">In this walkthrough you do the following steps:</span></span> 

1. <span data-ttu-id="4c72b-116">Veri Fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4c72b-116">Create a data factory.</span></span>
2. <span data-ttu-id="4c72b-117">Veri Yönetimi ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4c72b-117">Create a data management gateway.</span></span> 
3. <span data-ttu-id="4c72b-118">Kaynak ve havuz veri depoları için bağlantılı Hizmetleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4c72b-118">Create linked services for source and sink data stores.</span></span>
4. <span data-ttu-id="4c72b-119">Girdi ve çıktı verilerini temsil edecek veri kümeleri oluşturma.</span><span class="sxs-lookup"><span data-stu-id="4c72b-119">Create datasets to represent input and output data.</span></span>
5. <span data-ttu-id="4c72b-120">Verileri taşımak için kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4c72b-120">Create a pipeline with a copy activity to move the data.</span></span>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="4c72b-121">Öğreticisi için Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="4c72b-121">Prerequisites for the tutorial</span></span>
<span data-ttu-id="4c72b-122">Bu kılavuzda başlamadan önce aşağıdaki önkoşullara sahip olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="4c72b-122">Before you begin this walkthrough, you must have the following prerequisites:</span></span>

* <span data-ttu-id="4c72b-123">**Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-123">**Azure subscription**.</span></span>  <span data-ttu-id="4c72b-124">Bir aboneliğiniz yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c72b-124">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4c72b-125">Bkz: [ücretsiz deneme](http://azure.microsoft.com/pricing/free-trial/) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="4c72b-125">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="4c72b-126">**Azure depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-126">**Azure Storage Account**.</span></span> <span data-ttu-id="4c72b-127">Blob depolama alanı olarak kullandığınız bir **hedef/havuz** verileri depolamak Bu öğreticide.</span><span class="sxs-lookup"><span data-stu-id="4c72b-127">You use the blob storage as a **destination/sink** data store in this tutorial.</span></span> <span data-ttu-id="4c72b-128">bir Azure depolama hesabınız yoksa bkz [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) makale oluşturmak adımlar.</span><span class="sxs-lookup"><span data-stu-id="4c72b-128">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
* <span data-ttu-id="4c72b-129">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-129">**SQL Server**.</span></span> <span data-ttu-id="4c72b-130">Bir şirket içi SQL Server veritabanı olarak kullandığınız bir **kaynak** verileri depolamak Bu öğreticide.</span><span class="sxs-lookup"><span data-stu-id="4c72b-130">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="4c72b-131">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c72b-131">Create data factory</span></span>
<span data-ttu-id="4c72b-132">Bu adımda, Azure portalında adlı bir Azure Data Factory örneğini oluşturmak için kullandığınız **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-132">In this step, you use the Azure portal to create an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span></span>

1. <span data-ttu-id="4c72b-133">[Azure Portal](https://portal.azure.com)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4c72b-133">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4c72b-134">Tıklatın **+ yeni**, tıklatın **Intelligence + analiz**, tıklatıp **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-134">Click **+ NEW**, click **Intelligence + analytics**, and click **Data Factory**.</span></span>

   ![Yeni->DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. <span data-ttu-id="4c72b-136">İçinde **yeni data factory** want **ADFTutorialOnPremDF** adı.</span><span class="sxs-lookup"><span data-stu-id="4c72b-136">In the **New data factory** page, enter **ADFTutorialOnPremDF** for the Name.</span></span>

    ![Panosuna Ekle](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="4c72b-138">Azure veri fabrikasının adı genel olarak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4c72b-138">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="4c72b-139">Hatayı alırsanız: **veri fabrikası adı "ADFTutorialOnPremDF" kullanılabilir değil**, veri fabrikası (örneğin, yournameADFTutorialOnPremDF) adını değiştirin ve oluşturmayı yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="4c72b-139">If you receive the error: **Data factory name “ADFTutorialOnPremDF” is not available**, change the name of the data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span></span> <span data-ttu-id="4c72b-140">Bu öğreticide adımları uygularken ADFTutorialOnPremDF yerine bu adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4c72b-140">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span></span>
   >
   > <span data-ttu-id="4c72b-141">Data factory adı gelecekte bir **DNS** adı olarak kaydedilmiş olabilir; bu nedenle herkese görünür hale gelmiştir.</span><span class="sxs-lookup"><span data-stu-id="4c72b-141">The name of the data factory may be registered as a **DNS** name in the future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="4c72b-142">Data factory’yi oluşturmak istediğiniz **Azure aboneliği**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="4c72b-142">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="4c72b-143">Mevcut bir **kaynak grubu** seçin ya da bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4c72b-143">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="4c72b-144">Adlı bir kaynak grubu öğretici için oluşturduğunuz: **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-144">For the tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span></span>
6. <span data-ttu-id="4c72b-145">Tıklatın **oluşturma** üzerinde **yeni data factory** sayfası.</span><span class="sxs-lookup"><span data-stu-id="4c72b-145">Click **Create** on the **New data factory** page.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4c72b-146">Data Factory örnekleri oluşturmak için abonelik/kaynak grubu düzeyinde [Data Factory Katılımcısı](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rolünün üyesi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c72b-146">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="4c72b-147">Oluşturma işlemi tamamlandıktan sonra gördüğünüz **Data Factory** sayfasında aşağıdaki resimde gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="4c72b-147">After creation is complete, you see the **Data Factory** page as shown in the following image:</span></span>

   ![Data Factory giriş sayfası](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a><span data-ttu-id="4c72b-149">Ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c72b-149">Create gateway</span></span>
1. <span data-ttu-id="4c72b-150">İçinde **Data Factory** sayfasında, **yazar ve dağıtma** başlatmak için döşeme **Düzenleyicisi** data factory için.</span><span class="sxs-lookup"><span data-stu-id="4c72b-150">In the **Data Factory** page, click **Author and deploy** tile to launch the **Editor** for the data factory.</span></span>

    ![Geliştir ve Dağıt Kutucuğu](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. <span data-ttu-id="4c72b-152">Data Factory Düzenleyici'yi tıklatın **... Daha fazla** araç ve ardından **yeni veri ağ geçidi**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-152">In the Data Factory Editor, click **... More** on the toolbar and then click **New data gateway**.</span></span> <span data-ttu-id="4c72b-153">Alternatif olarak, sağ tıklayarak **Data Gateways** ağaç görünümünde ve tıklatın **yeni veri ağ geçidi**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-153">Alternatively, you can right-click **Data Gateways** in the tree view, and click **New data gateway**.</span></span>

   ![Araç çubuğundaki yeni veri ağ geçidi](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. <span data-ttu-id="4c72b-155">İçinde **oluşturma** want **adftutorialgateway** için **adı**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-155">In the **Create** page, enter **adftutorialgateway** for the **name**, and click **OK**.</span></span>     

    ![Ağ geçidi sayfası oluşturma](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > <span data-ttu-id="4c72b-157">Bu kılavuzda, yalnızca bir düğümle (şirket içi Windows makine) mantıksal ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4c72b-157">In this walkthrough, you create the logical gateway with only one node (on-premises Windows machine).</span></span> <span data-ttu-id="4c72b-158">Ağ geçidi ile birden çok şirket içi makineler ilişkilendirerek veri yönetimi ağ geçidi ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c72b-158">You can scale out a data management gateway by associating multiple on-premises machines with the gateway.</span></span> <span data-ttu-id="4c72b-159">Ölçeklendirmek yukarı bir düğümde aynı anda çalıştırabilirsiniz veri taşıma işlerinin sayısını artırarak.</span><span class="sxs-lookup"><span data-stu-id="4c72b-159">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="4c72b-160">Bu özellik, tek bir düğüme sahip mantıksal bir ağ geçidi için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4c72b-160">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="4c72b-161">Bkz: [ölçeklendirme veri yönetimi ağ geçidi Azure veri fabrikası'nda](data-factory-data-management-gateway-high-availability-scalability.md) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="4c72b-161">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>  
4. <span data-ttu-id="4c72b-162">İçinde **yapılandırma** sayfasında, **doğrudan bu bilgisayar Yükle**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-162">In the **Configure** page, click **Install directly on this computer**.</span></span> <span data-ttu-id="4c72b-163">Bu eylem ağ geçidi yükleme paketi indirir, yükler, yapılandırır ve bilgisayarda ağ geçidi kaydeder.</span><span class="sxs-lookup"><span data-stu-id="4c72b-163">This action downloads the installation package for the gateway, installs, configures, and registers the gateway on the computer.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="4c72b-164">Internet Explorer veya Microsoft ClickOnce uyumlu bir web tarayıcısı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4c72b-164">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>
   >
   > <span data-ttu-id="4c72b-165">Chrome kullanıyorsanız, [Chrome web mağazasına](https://chrome.google.com/webstore/) gidin, “ClickOnce” araması yapın, ClickOnce uzantılarından birini seçin ve yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4c72b-165">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>
   >
   > <span data-ttu-id="4c72b-166">Aynı Firefox (yükleme eklenti) yapın.</span><span class="sxs-lookup"><span data-stu-id="4c72b-166">Do the same for Firefox (install add-in).</span></span> <span data-ttu-id="4c72b-167">Tıklatın **menü Aç** araç çubuğunda (**üç yatay çizgi** sağ üst köşesinde), tıklatın **eklentileri**, arama "ClickOnce" sözcüğünü, aşağıdakilerden birini seçin ClickOnce uzantıları ve yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4c72b-167">Click **Open Menu** button on the toolbar (**three horizontal lines** in the top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>    
   >
   >

    ![Ağ geçidi - yapılandırma sayfası](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    <span data-ttu-id="4c72b-169">Bu şekilde, indirme, yükleme, yapılandırma ve tek tek adımda ağ geçidini kaydetmek için en kolay yolu (tek tıklatmayla) olur.</span><span class="sxs-lookup"><span data-stu-id="4c72b-169">This way is the easiest way (one-click) to download, install, configure, and register the gateway in one single step.</span></span> <span data-ttu-id="4c72b-170">Gördüğünüz **Microsoft Veri Yönetimi ağ geçidi Yapılandırma Yöneticisi** uygulaması bilgisayarınızda yüklü.</span><span class="sxs-lookup"><span data-stu-id="4c72b-170">You can see the **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span></span> <span data-ttu-id="4c72b-171">Yürütülebilir dosya bulabileceğiniz **ConfigManager.exe** klasöründeki: **C:\Program Files\Microsoft veri yönetimi Gateway\2.0\Shared**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-171">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span></span>

    <span data-ttu-id="4c72b-172">Ayrıca indirebilir ve bu sayfada bağlantıları kullanarak ağ geçidini el ile yükleyin ve gösterilen anahtarı kullanarak kaydetmek **yeni anahtar** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="4c72b-172">You can also download and install gateway manually by using the links in this page and register it using the key shown in the **NEW KEY** text box.</span></span>

    <span data-ttu-id="4c72b-173">Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) ağ geçidi hakkında tüm ayrıntılar için makalenin.</span><span class="sxs-lookup"><span data-stu-id="4c72b-173">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the gateway.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4c72b-174">Yüklemek ve veri yönetimi ağ geçidi başarıyla yapılandırmak için yerel bilgisayarda yönetici olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c72b-174">You must be an administrator on the local computer to install and configure the Data Management Gateway successfully.</span></span> <span data-ttu-id="4c72b-175">Ek kullanıcı eklemek **veri yönetimi ağ geçidi kullanıcıları** yerel Windows grubu.</span><span class="sxs-lookup"><span data-stu-id="4c72b-175">You can add additional users to the **Data Management Gateway Users** local Windows group.</span></span> <span data-ttu-id="4c72b-176">Bu grubun üyeleri, ağ geçidini yapılandırmak için veri yönetimi ağ geçidi Yapılandırma Yöneticisi aracını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c72b-176">The members of this group can use the Data Management Gateway Configuration Manager tool to configure the gateway.</span></span>
   >
   >
5. <span data-ttu-id="4c72b-177">Birkaç dakika bekleyin ya da aşağıdaki bildirim iletisini görene kadar bekleyin:</span><span class="sxs-lookup"><span data-stu-id="4c72b-177">Wait for a couple of minutes or wait until you see the following notification message:</span></span>

    ![Ağ geçidi yükleme başarılı](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. <span data-ttu-id="4c72b-179">Başlatma **veri yönetimi ağ geçidi Yapılandırma Yöneticisi** bilgisayarınızdaki uygulama.</span><span class="sxs-lookup"><span data-stu-id="4c72b-179">Launch **Data Management Gateway Configuration Manager** application on your computer.</span></span> <span data-ttu-id="4c72b-180">İçinde **arama** penceresinde, türü **veri yönetimi ağ geçidi** bu yardımcı program erişmek için.</span><span class="sxs-lookup"><span data-stu-id="4c72b-180">In the **Search** window, type **Data Management Gateway** to access this utility.</span></span> <span data-ttu-id="4c72b-181">Yürütülebilir dosya bulabileceğiniz **ConfigManager.exe** klasöründeki: **C:\Program Files\Microsoft veri yönetim Gateway\2.0\Shared**</span><span class="sxs-lookup"><span data-stu-id="4c72b-181">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span></span>

    ![Ağ geçidi Yapılandırma Yöneticisi](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. <span data-ttu-id="4c72b-183">Gördüğünüzü onaylayın `adftutorialgateway is connected to the cloud service` ileti.</span><span class="sxs-lookup"><span data-stu-id="4c72b-183">Confirm that you see `adftutorialgateway is connected to the cloud service` message.</span></span> <span data-ttu-id="4c72b-184">Durum çubuğu alt görüntüler **bulut hizmetine bağlı** ile birlikte bir **yeşil onay işareti**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-184">The status bar the bottom displays **Connected to the cloud service** along with a **green check mark**.</span></span>

    <span data-ttu-id="4c72b-185">Üzerinde **giriş** sekmesinde da aşağıdaki işlemleri yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4c72b-185">On the **Home** tab, you can also do the following operations:</span></span>

   * <span data-ttu-id="4c72b-186">**Kayıt** kayıt düğmesini kullanarak Azure portalından bir anahtara sahip bir ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="4c72b-186">**Register** a gateway with a key from the Azure portal by using the Register button.</span></span>
   * <span data-ttu-id="4c72b-187">**Durdur** veri yönetimi ağ geçidi ana bilgisayar, ağ geçidi makine üzerinde çalışan hizmeti.</span><span class="sxs-lookup"><span data-stu-id="4c72b-187">**Stop** the Data Management Gateway Host Service running on your gateway machine.</span></span>
   * <span data-ttu-id="4c72b-188">**Zamanlama güncelleştirmeleri** günün belirli bir zamanda yüklenecek.</span><span class="sxs-lookup"><span data-stu-id="4c72b-188">**Schedule updates** to be installed at a specific time of the day.</span></span>
   * <span data-ttu-id="4c72b-189">Ağ geçidi olduğu zaman görüntülemek **son güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-189">View when the gateway was **last updated**.</span></span>
   * <span data-ttu-id="4c72b-190">Ağ geçidi için bir güncelleştirme yüklenebilmesi için süreyi belirtin.</span><span class="sxs-lookup"><span data-stu-id="4c72b-190">Specify time at which an update to the gateway can be installed.</span></span>
8. <span data-ttu-id="4c72b-191">Geçiş **ayarları** sekmesi. Belirtilen sertifika **sertifika** bölüm portalda belirttiğiniz şirket içi veri depolama alanı için kimlik bilgilerini şifreleme/şifre çözme için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4c72b-191">Switch to the **Settings** tab. The certificate specified in the **Certificate** section is used to encrypt/decrypt credentials for the on-premises data store that you specify on the portal.</span></span> <span data-ttu-id="4c72b-192">(isteğe bağlı) Tıklatın **değişiklik** kullanarak kendi sertifikanızı kullanmayı.</span><span class="sxs-lookup"><span data-stu-id="4c72b-192">(optional) Click **Change** to use your own certificate instead.</span></span> <span data-ttu-id="4c72b-193">Varsayılan olarak, ağ geçidinin Data Factory hizmeti tarafından otomatik olarak oluşturulan sertifikayı kullanır.</span><span class="sxs-lookup"><span data-stu-id="4c72b-193">By default, the gateway uses the certificate that is auto-generated by the Data Factory service.</span></span>

    ![Ağ geçidi sertifika yapılandırma](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    <span data-ttu-id="4c72b-195">Üzerinde aşağıdaki işlemleri yapabilirsiniz **ayarları** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="4c72b-195">You can also do the following actions on the **Settings** tab:</span></span>

   * <span data-ttu-id="4c72b-196">Görüntülemek veya ağ geçidi tarafından kullanılan sertifikanın dışa aktarın.</span><span class="sxs-lookup"><span data-stu-id="4c72b-196">View or export the certificate being used by the gateway.</span></span>
   * <span data-ttu-id="4c72b-197">Ağ Geçidi tarafından kullanılan HTTPS uç noktası değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4c72b-197">Change the HTTPS endpoint used by the gateway.</span></span>    
   * <span data-ttu-id="4c72b-198">Ağ Geçidi tarafından kullanılacak bir HTTP proxy ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4c72b-198">Set an HTTP proxy to be used by the gateway.</span></span>     
9. <span data-ttu-id="4c72b-199">(isteğe bağlı) Geçiş **tanılama** sekmesi, onay **ayrıntılı günlük kaydını etkinleştir** ağ geçidi ile ilgili tüm sorunları gidermek için kullanabileceğiniz ayrıntılı günlük kaydını etkinleştirmek istiyorsanız, seçeneği.</span><span class="sxs-lookup"><span data-stu-id="4c72b-199">(optional) Switch to the **Diagnostics** tab, check the **Enable verbose logging** option if you want to enable verbose logging that you can use to troubleshoot any issues with the gateway.</span></span> <span data-ttu-id="4c72b-200">Günlük kaydı bilgileri bulunabilir **Olay Görüntüleyicisi'ni** altında **uygulama ve hizmet günlükleri** -> **veri yönetimi ağ geçidi** düğümü.</span><span class="sxs-lookup"><span data-stu-id="4c72b-200">The logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span></span>

    ![Tanılama sekmesi](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    <span data-ttu-id="4c72b-202">Ayrıca aşağıdaki eylemleri gerçekleştirebilirsiniz **tanılama** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="4c72b-202">You can also perform the following actions in the **Diagnostics** tab:</span></span>

   * <span data-ttu-id="4c72b-203">Kullanım **Bağlantıyı Sına** ağ geçidini kullanarak şirket içi veri kaynağına bölümü.</span><span class="sxs-lookup"><span data-stu-id="4c72b-203">Use **Test Connection** section to an on-premises data source using the gateway.</span></span>
   * <span data-ttu-id="4c72b-204">Tıklatın **günlüklerini görüntüle** veri yönetimi ağ geçidi günlüğüne bir Olay Görüntüleyici penceresinde görmek için.</span><span class="sxs-lookup"><span data-stu-id="4c72b-204">Click **View Logs** to see the Data Management Gateway log in an Event Viewer window.</span></span>
   * <span data-ttu-id="4c72b-205">Tıklatın **günlükleri Gönder** sorunları, sorun giderme kolaylaştırmak üzere Microsoft'a günlük son yedi gün içeren bir zip dosyası karşıya yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="4c72b-205">Click **Send Logs** to upload a zip file with logs of last seven days to Microsoft to facilitate troubleshooting of your issues.</span></span>
10. <span data-ttu-id="4c72b-206">Üzerinde **tanılama** sekmesinde **Bağlantıyı Sına** bölümünde, select **SqlServer** veri deposu türü için veritabanı sunucusu, veritabanı adını adını girin kimlik doğrulama türünü belirtin, kullanıcı adı ve parola girin ve tıklatın **Test** ağ geçidi veritabanına bağlanıp bağlanamadığınızı test etmek için.</span><span class="sxs-lookup"><span data-stu-id="4c72b-206">On the **Diagnostics** tab, in the **Test Connection** section, select **SqlServer** for the type of the data store, enter the name of the database server, name of the database, specify authentication type, enter user name, and password, and click **Test** to test whether the gateway can connect to the database.</span></span>
11. <span data-ttu-id="4c72b-207">Web tarayıcısı ve de geçiş **Azure portal**, tıklatın **Tamam** üzerinde **yapılandırma** sayfa ve daha sonra **yeni veri ağ geçidi** sayfası.</span><span class="sxs-lookup"><span data-stu-id="4c72b-207">Switch to the web browser, and in the **Azure portal**, click **OK** on the **Configure** page and then on the **New data gateway** page.</span></span>
12. <span data-ttu-id="4c72b-208">Görmeniz gerekir **adftutorialgateway** altında **Data Gateways** soldaki ağaç görünümünde.</span><span class="sxs-lookup"><span data-stu-id="4c72b-208">You should see **adftutorialgateway** under **Data Gateways** in the tree view on the left.</span></span>  <span data-ttu-id="4c72b-209">Tıklarsanız, ilişkili JSON görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c72b-209">If you click it, you should see the associated JSON.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="4c72b-210">Bağlı hizmetler oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c72b-210">Create linked services</span></span>
<span data-ttu-id="4c72b-211">Bu adımda, iki bağlı hizmet oluşturma: **AzureStorageLinkedService** ve **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-211">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span></span> <span data-ttu-id="4c72b-212">**SqlServerLinkedService** bir şirket içi SQL Server veritabanına bağlar ve **AzureStorageLinkedService** bağlantılı hizmeti bir Azure blob deposu data factory bağlar.</span><span class="sxs-lookup"><span data-stu-id="4c72b-212">The **SqlServerLinkedService** links an on-premises SQL Server database and the **AzureStorageLinkedService** linked service links an Azure blob store to the data factory.</span></span> <span data-ttu-id="4c72b-213">Azure blob deposuna şirket içi SQL Server veritabanından veri kopyalayan daha sonra bu kılavuzda bir işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4c72b-213">You create a pipeline later in this walkthrough that copies data from the on-premises SQL Server database to the Azure blob store.</span></span>

#### <a name="add-a-linked-service-to-an-on-premises-sql-server-database"></a><span data-ttu-id="4c72b-214">Bir şirket içi SQL Server veritabanına bağlı hizmet ekleme</span><span class="sxs-lookup"><span data-stu-id="4c72b-214">Add a linked service to an on-premises SQL Server database</span></span>
1. <span data-ttu-id="4c72b-215">İçinde **Data Factory düzenleyici**, tıklatın **yeni veri deposu** seçin ve araç **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-215">In the **Data Factory Editor**, click **New data store** on the toolbar and select **SQL Server**.</span></span>

   ![Yeni SQL Server bağlantılı hizmeti](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. <span data-ttu-id="4c72b-217">İçinde **JSON Düzenleyicisi** sağ tarafta aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="4c72b-217">In the **JSON editor** on the right, do the following steps:</span></span>

   1. <span data-ttu-id="4c72b-218">İçin **gatewayName**, belirtin **adftutorialgateway**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-218">For the **gatewayName**, specify **adftutorialgateway**.</span></span>    
   2. <span data-ttu-id="4c72b-219">İçinde **connectionString**, aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="4c72b-219">In the **connectionString**, do the following steps:</span></span>    

      1. <span data-ttu-id="4c72b-220">İçin **servername**, SQL Server veritabanını barındıran sunucunun adını girin.</span><span class="sxs-lookup"><span data-stu-id="4c72b-220">For **servername**, enter the name of the server that hosts the SQL Server database.</span></span>
      2. <span data-ttu-id="4c72b-221">İçin **databasename**, veritabanının adını girin.</span><span class="sxs-lookup"><span data-stu-id="4c72b-221">For **databasename**, enter the name of the database.</span></span>
      3. <span data-ttu-id="4c72b-222">Tıklatın **şifrele** araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="4c72b-222">Click **Encrypt** button on the toolbar.</span></span> <span data-ttu-id="4c72b-223">Kimlik bilgileri Yöneticisi uygulama bakın.</span><span class="sxs-lookup"><span data-stu-id="4c72b-223">You see the Credentials Manager application.</span></span>

         ![Kimlik bilgileri Yöneticisi uygulaması](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. <span data-ttu-id="4c72b-225">İçinde **kimlik bilgilerini ayarlama** iletişim kutusunda, kimlik doğrulama türü, kullanıcı adı ve parola belirtin ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-225">In the **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span></span> <span data-ttu-id="4c72b-226">Bağlantı başarılı olursa, JSON içinde depolanan şifrelenmiş kimlik bilgileri ve iletişim kutusunu kapatır.</span><span class="sxs-lookup"><span data-stu-id="4c72b-226">If the connection is successful, the encrypted credentials are stored in the JSON and the dialog box closes.</span></span>
      5. <span data-ttu-id="4c72b-227">Otomatik olarak kapalı, iletişim kutusu başlatılan boş tarayıcı sekmesinde kapatın ve Azure portal ile sekmesine geri alın.</span><span class="sxs-lookup"><span data-stu-id="4c72b-227">Close the empty browser tab that launched the dialog box if it is not automatically closed and get back to the tab with the Azure portal.</span></span>

         <span data-ttu-id="4c72b-228">Bu kimlik bilgileri ağ geçidi makinesi üzerinde olan **şifrelenmiş** Data Factory hizmetine sahip olan bir sertifikayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="4c72b-228">On the gateway machine, these credentials are **encrypted** by using a certificate that the Data Factory service owns.</span></span> <span data-ttu-id="4c72b-229">Bunun yerine veri yönetimi ağ geçidi ile ilişkili sertifika kullanmak istiyorsanız bkz [kimlik bilgilerini güvenli bir şekilde ayarlamak](#set-credentials-and-security).</span><span class="sxs-lookup"><span data-stu-id="4c72b-229">If you want to use the certificate that is associated with the Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span></span>    
   3. <span data-ttu-id="4c72b-230">Tıklatın **dağıtma** hizmeti SQL Server dağıtımı için komut çubuğunda bağlı.</span><span class="sxs-lookup"><span data-stu-id="4c72b-230">Click **Deploy** on the command bar to deploy the SQL Server linked service.</span></span> <span data-ttu-id="4c72b-231">Bağlantılı hizmet ağaç görünümünde görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c72b-231">You should see the linked service in the tree view.</span></span>

      ![SQL Server bağlantılı hizmet ağaç görünümünde](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="4c72b-233">Bir Azure depolama hesabı için bağlı hizmet ekleme</span><span class="sxs-lookup"><span data-stu-id="4c72b-233">Add a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="4c72b-234">İçinde **Data Factory düzenleyici**, tıklatın **yeni veri deposu** tıklatın ve komut çubuğunda **Azure depolama**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-234">In the **Data Factory Editor**, click **New data store** on the command bar and click **Azure storage**.</span></span>
2. <span data-ttu-id="4c72b-235">Azure depolama hesabınızın adını girin **hesap adı**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-235">Enter the name of your Azure storage account for the **Account name**.</span></span>
3. <span data-ttu-id="4c72b-236">Azure depolama hesabınız için anahtarını girin **hesap anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-236">Enter the key for your Azure storage account for the **Account key**.</span></span>
4. <span data-ttu-id="4c72b-237">Tıklatın **dağıtma** dağıtmak için **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-237">Click **Deploy** to deploy the **AzureStorageLinkedService**.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="4c72b-238">Veri kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c72b-238">Create datasets</span></span>
<span data-ttu-id="4c72b-239">Bu adımda, girdi oluşturun ve çıkış kopyalama işlemi için girdi ve çıktı verilerini temsil eden veri kümeleri (şirket içi SQL Server veritabanı = > Azure blob depolama).</span><span class="sxs-lookup"><span data-stu-id="4c72b-239">In this step, you create input and output datasets that represent input and output data for the copy operation (On-premises SQL Server database => Azure blob storage).</span></span> <span data-ttu-id="4c72b-240">Veri kümeleri oluşturmadan önce (ayrıntılı adımları izler listesi) aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="4c72b-240">Before creating datasets, do the following steps (detailed steps follows the list):</span></span>

* <span data-ttu-id="4c72b-241">Adlı bir tablo oluşturmak **emp** SQL Server veritabanında data factory bağlantılı bir hizmet olarak eklendi ve birkaç örnek girdileri tabloya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4c72b-241">Create a table named **emp** in the SQL Server Database you added as a linked service to the data factory and insert a couple of sample entries into the table.</span></span>
* <span data-ttu-id="4c72b-242">Adlı bir blob kapsayıcı oluşturun **adftutorial** Azure blob depolama hesabı data factory bağlantılı bir hizmet olarak eklendi.</span><span class="sxs-lookup"><span data-stu-id="4c72b-242">Create a blob container named **adftutorial** in the Azure blob storage account you added as a linked service to the data factory.</span></span>

### <a name="prepare-on-premises-sql-server-for-the-tutorial"></a><span data-ttu-id="4c72b-243">Şirket içi SQL Server öğretici için hazırlama</span><span class="sxs-lookup"><span data-stu-id="4c72b-243">Prepare On-premises SQL Server for the tutorial</span></span>
1. <span data-ttu-id="4c72b-244">Şirket içi için belirtilen veritabanında SQL Server hizmeti bağlı (**SqlServerLinkedService**), oluşturmak için aşağıdaki SQL betiğini kullanın **emp** veritabanındaki tablo.</span><span class="sxs-lookup"><span data-stu-id="4c72b-244">In the database you specified for the on-premises SQL Server linked service (**SqlServerLinkedService**), use the following SQL script to create the **emp** table in the database.</span></span>

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
2. <span data-ttu-id="4c72b-245">Bazı örnek tabloya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4c72b-245">Insert some sample into the table:</span></span>

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a><span data-ttu-id="4c72b-246">Girdi veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c72b-246">Create input dataset</span></span>

1. <span data-ttu-id="4c72b-247">**Data Factory Düzenleyicisi**’nde komut çubuğundaki **... Daha fazla**, tıklatın **yeni veri kümesi** komut çubuğu ve tıklatın **SQL Server tablosuna**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-247">In the **Data Factory Editor**, click **... More**, click **New dataset** on the command bar, and click **SQL Server table**.</span></span>
2. <span data-ttu-id="4c72b-248">Sağ bölmedeki JSON aşağıdaki metinle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4c72b-248">Replace the JSON in the right pane with the following text:</span></span>

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
   <span data-ttu-id="4c72b-249">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="4c72b-249">Note the following points:</span></span>

   * <span data-ttu-id="4c72b-250">**tür** ayarlanır **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-250">**type** is set to **SqlServerTable**.</span></span>
   * <span data-ttu-id="4c72b-251">**tableName** ayarlanır **emp**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-251">**tableName** is set to **emp**.</span></span>
   * <span data-ttu-id="4c72b-252">**linkedServiceName** ayarlanır **SqlServerLinkedService** (Bu kılavuzda daha önce bu bağlı hizmetin oluşturmuştunuz.).</span><span class="sxs-lookup"><span data-stu-id="4c72b-252">**linkedServiceName** is set to **SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span></span>
   * <span data-ttu-id="4c72b-253">Azure Data Factory başka bir ardışık düzen tarafından üretilen olmayan bir giriş veri kümesi için ayarlamalısınız **dış** için **doğru**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-253">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** to **true**.</span></span> <span data-ttu-id="4c72b-254">Bu girdi verileri Azure Data Factory hizmetine dış üretilen gösterir.</span><span class="sxs-lookup"><span data-stu-id="4c72b-254">It denotes the input data is produced external to the Azure Data Factory service.</span></span> <span data-ttu-id="4c72b-255">İsteğe bağlı olarak tüm dış veri ilkeleri kullanılarak belirtebilirsiniz **externalData** öğesinde **İlkesi** bölümü.</span><span class="sxs-lookup"><span data-stu-id="4c72b-255">You can optionally specify any external data policies using the **externalData** element in the **Policy** section.</span></span>    

   <span data-ttu-id="4c72b-256">Bkz: [/SQL Server'dan veri taşıma](data-factory-sqlserver-connector.md) JSON özellikleri hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="4c72b-256">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="4c72b-257">Tıklatın **dağıtma** veri kümesini dağıtmak için komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="4c72b-257">Click **Deploy** on the command bar to deploy the dataset.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="4c72b-258">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c72b-258">Create output dataset</span></span>

1. <span data-ttu-id="4c72b-259">İçinde **Data Factory düzenleyici**, tıklatın **yeni veri kümesi** komut çubuğu ve tıklatın **Azure Blob Depolama**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-259">In the **Data Factory Editor**, click **New dataset** on the command bar, and click **Azure Blob storage**.</span></span>
2. <span data-ttu-id="4c72b-260">Sağ bölmedeki JSON aşağıdaki metinle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4c72b-260">Replace the JSON in the right pane with the following text:</span></span>

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
   <span data-ttu-id="4c72b-261">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="4c72b-261">Note the following points:</span></span>

   * <span data-ttu-id="4c72b-262">**tür** ayarlanır **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-262">**type** is set to **AzureBlob**.</span></span>
   * <span data-ttu-id="4c72b-263">**linkedServiceName** ayarlanır **AzureStorageLinkedService** (Bu bağlı hizmeti 2. adımda oluşturmuştunuz).</span><span class="sxs-lookup"><span data-stu-id="4c72b-263">**linkedServiceName** is set to **AzureStorageLinkedService** (you had created this linked service in Step 2).</span></span>
   * <span data-ttu-id="4c72b-264">**folderPath** ayarlanır **adftutorial/outfromonpremdf** outfromonpremdf adftutorial kapsayıcı klasöründe olduğu.</span><span class="sxs-lookup"><span data-stu-id="4c72b-264">**folderPath** is set to **adftutorial/outfromonpremdf** where outfromonpremdf is the folder in the adftutorial container.</span></span> <span data-ttu-id="4c72b-265">Oluşturma **adftutorial** zaten yoksa, kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="4c72b-265">Create the **adftutorial** container if it does not already exist.</span></span>
   * <span data-ttu-id="4c72b-266">**availability** **hourly** olarak ayarlanmıştır (**frequency** **hour**, **interval** de **1** olarak ayarlanmıştır).</span><span class="sxs-lookup"><span data-stu-id="4c72b-266">The **availability** is set to **hourly** (**frequency** set to **hour** and **interval** set to **1**).</span></span>  <span data-ttu-id="4c72b-267">Data Factory hizmetinin her saat bir çıktı veri dilimi oluşturur **emp** Azure SQL veritabanı tablosunda.</span><span class="sxs-lookup"><span data-stu-id="4c72b-267">The Data Factory service generates an output data slice every hour in the **emp** table in the Azure SQL Database.</span></span>

   <span data-ttu-id="4c72b-268">Belirtmezseniz, bir **fileName** için bir **çıktı tablosu**, de oluşturulan dosyaları **folderPath** şu biçimde adlandırılır: Data.<Guid>. txt (örneğin:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="4c72b-268">If you do not specify a **fileName** for an **output table**, the generated files in the **folderPath** are named in the following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="4c72b-269">Ayarlamak için **folderPath** ve **fileName** göre dinamik olarak **SliceStart** zaman, partitionedBy özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4c72b-269">To set **folderPath** and **fileName** dynamically based on the **SliceStart** time, use the partitionedBy property.</span></span> <span data-ttu-id="4c72b-270">Aşağıdaki örnekte, folderPath SliceStart’taki (işlemdeki dilimin başlangıç zamanı) Yıl, Ay ve Gün öğelerini, fileName ise SliceStart’taki Saat öğesini kullanır.</span><span class="sxs-lookup"><span data-stu-id="4c72b-270">In the following example, folderPath uses Year, Month, and Day from the SliceStart (start time of the slice being processed) and fileName uses Hour from the SliceStart.</span></span> <span data-ttu-id="4c72b-271">Örneğin, dilim 2014-10-20T08:00:00 için oluşturulduysa, folderName wikidatagateway/wikisampledataout/2014/10/20, fileName de 08.csv olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="4c72b-271">For example, if a slice is being produced for 2014-10-20T08:00:00, the folderName is set to wikidatagateway/wikisampledataout/2014/10/20 and the fileName is set to 08.csv.</span></span>

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

    <span data-ttu-id="4c72b-272">Bkz: [/Azure Blob storage'da veri taşıma](data-factory-azure-blob-connector.md) JSON özellikleri hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="4c72b-272">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="4c72b-273">Tıklatın **dağıtma** veri kümesini dağıtmak için komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="4c72b-273">Click **Deploy** on the command bar to deploy the dataset.</span></span> <span data-ttu-id="4c72b-274">Her iki veri kümelerinin ağaç görünümünde gördüğünüzü onaylayın.</span><span class="sxs-lookup"><span data-stu-id="4c72b-274">Confirm that you see both the datasets in the tree view.</span></span>  

## <a name="create-pipeline"></a><span data-ttu-id="4c72b-275">İşlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c72b-275">Create pipeline</span></span>
<span data-ttu-id="4c72b-276">Bu adımda, oluşturduğunuz bir **ardışık düzen** biriyle **kopyalama etkinliği** kullanan **EmpOnPremSQLTable** giriş olarak ve **OutputBlobTable** olarak çıktı.</span><span class="sxs-lookup"><span data-stu-id="4c72b-276">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span></span>

1. <span data-ttu-id="4c72b-277">Veri Fabrikası Düzenleyicisi'nde tıklatın **... Daha fazla** ve **Yeni işlem hattı** öğelerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c72b-277">In Data Factory Editor, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="4c72b-278">Sağ bölmedeki JSON aşağıdaki metinle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4c72b-278">Replace the JSON in the right pane with the following text:</span></span>    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL to Azure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server to blob",
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
   > <span data-ttu-id="4c72b-279">**start** özelliğinin değerini geçerli günle, **end** değerini de sonraki günle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4c72b-279">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span>
   >
   >

   <span data-ttu-id="4c72b-280">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="4c72b-280">Note the following points:</span></span>

   * <span data-ttu-id="4c72b-281">Etkinlikler bölümünde, yalnızca etkinliği yoktur, **türü** ayarlanır **kopya**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-281">In the activities section, there is only activity whose **type** is set to **Copy**.</span></span>
   * <span data-ttu-id="4c72b-282">**Giriş** etkinlik için **EmpOnPremSQLTable** ve **çıkış** etkinlik için **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-282">**Input** for the activity is set to **EmpOnPremSQLTable** and **output** for the activity is set to **OutputBlobTable**.</span></span>
   * <span data-ttu-id="4c72b-283">İçinde **typeProperties** bölümünde **SqlSource** olarak belirtilen **kaynak türünü** ve ** BlobSink ** olarak belirtilen **Havuz türü**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-283">In the **typeProperties** section, **SqlSource** is specified as the **source type** and **BlobSink **is specified as the **sink type**.</span></span>
   * <span data-ttu-id="4c72b-284">SQL sorgusu `select * from emp` için belirtilen **sqlReaderQuery** özelliği **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-284">SQL query `select * from emp` is specified for the **sqlReaderQuery** property of **SqlSource**.</span></span>

   <span data-ttu-id="4c72b-285">Başlangıç ve bitiş tarih saatleri [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601) olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4c72b-285">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="4c72b-286">Örneğin: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="4c72b-286">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="4c72b-287">**End** zamanı isteğe bağlıdır; ancak bu öğreticide bunu kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="4c72b-287">The **end** time is optional, but we use it in this tutorial.</span></span>

   <span data-ttu-id="4c72b-288">**end** özelliği için değer belirtmezseniz "**start + 48 hours**" olarak hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="4c72b-288">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="4c72b-289">İşlem hattını süresiz olarak çalıştırmak için **end** özelliği değerini **9/9/9999** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4c72b-289">To run the pipeline indefinitely, specify **9/9/9999** as the value for the **end** property.</span></span>

   <span data-ttu-id="4c72b-290">Temel veri dilimlerinin işlenir süre tanımlama **kullanılabilirlik** her Azure Data Factory veri kümesi için tanımlanan özellikler.</span><span class="sxs-lookup"><span data-stu-id="4c72b-290">You are defining the time duration in which the data slices are processed based on the **Availability** properties that were defined for each Azure Data Factory dataset.</span></span>

   <span data-ttu-id="4c72b-291">Örnekte, her veri dilimi saatlik oluşturulduğundan 24 veri dilimi vardır.</span><span class="sxs-lookup"><span data-stu-id="4c72b-291">In the example, there are 24 data slices as each data slice is produced hourly.</span></span>        
3. <span data-ttu-id="4c72b-292">Tıklatın **dağıtma** veri kümesini dağıtmak için komut çubuğunda (tablo dikdörtgen bir veri kümesi olur).</span><span class="sxs-lookup"><span data-stu-id="4c72b-292">Click **Deploy** on the command bar to deploy the dataset (table is a rectangular dataset).</span></span> <span data-ttu-id="4c72b-293">İşlem hattını ağaç görünümünde altında gösterildiğini onaylayın **ardışık düzen** düğümü.</span><span class="sxs-lookup"><span data-stu-id="4c72b-293">Confirm that the pipeline shows up in the tree view under **Pipelines** node.</span></span>  
4. <span data-ttu-id="4c72b-294">Şimdi, **X** iki kez geri almak için sayfayı kapatmak için **Data Factory** için sayfa **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-294">Now, click **X** twice to close the page to get back to the **Data Factory** page for the **ADFTutorialOnPremDF**.</span></span>

<span data-ttu-id="4c72b-295">**Tebrikler!**</span><span class="sxs-lookup"><span data-stu-id="4c72b-295">**Congratulations!**</span></span> <span data-ttu-id="4c72b-296">Başarıyla bir Azure data factory, bağlı hizmetler, veri kümeleri ve işlem hattı oluşturulan ve işlem hattını zamanladınız.</span><span class="sxs-lookup"><span data-stu-id="4c72b-296">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled the pipeline.</span></span>

#### <a name="view-the-data-factory-in-a-diagram-view"></a><span data-ttu-id="4c72b-297">Data factory’yi Diyagram Görünümünde görüntüleme</span><span class="sxs-lookup"><span data-stu-id="4c72b-297">View the data factory in a Diagram View</span></span>
1. <span data-ttu-id="4c72b-298">İçinde **Azure portal**, tıklatın **diyagramı** döşeme için giriş sayfasındaki **ADFTutorialOnPremDF** veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="4c72b-298">In the **Azure portal**, click **Diagram** tile on the home page for the **ADFTutorialOnPremDF** data factory.</span></span> <span data-ttu-id="4c72b-299">:</span><span class="sxs-lookup"><span data-stu-id="4c72b-299">:</span></span>

    ![Diyagram bağlantı](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. <span data-ttu-id="4c72b-301">Aşağıdaki görüntüye benzer bir diyagram görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="4c72b-301">You should see the diagram similar to the following image:</span></span>

    ![Diyagram Görünümü](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    <span data-ttu-id="4c72b-303">Yakınlaştırma, uzaklaştırma, % 100, uygun, otomatik olarak ardışık düzen ve veri kümeleri, konum ve çizgileri gösterebilirsiniz (Seçilen öğelerin Yukarı Akış ve aşağı akış öğelerini vurgular) Yakınlaştır.</span><span class="sxs-lookup"><span data-stu-id="4c72b-303">You can zoom in, zoom out, zoom to 100%, zoom to fit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="4c72b-304">Bir nesne (giriş/çıkış veri kümesi veya işlem hattı) özelliklerini görmek için çift tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c72b-304">You can double-click an object (input/output dataset or pipeline) to see properties for it.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="4c72b-305">İşlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="4c72b-305">Monitor pipeline</span></span>
<span data-ttu-id="4c72b-306">Bu adımda, Azure data factory’de neler olduğunu izlemek için Azure Portal kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="4c72b-306">In this step, you use the Azure portal to monitor what’s going on in an Azure data factory.</span></span> <span data-ttu-id="4c72b-307">Veri kümelerini ve işlem hatlarını izlemek için de PowerShell cmdlet'lerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c72b-307">You can also use PowerShell cmdlets to monitor datasets and pipelines.</span></span> <span data-ttu-id="4c72b-308">İzleme hakkında daha fazla bilgi için bkz [izleme ve yönetme ardışık düzen](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="4c72b-308">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span></span>

1. <span data-ttu-id="4c72b-309">Diyagramda çift **EmpOnPremSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-309">In the diagram, double-click **EmpOnPremSQLTable**.</span></span>  

    ![EmpOnPremSQLTable dilimleri](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. <span data-ttu-id="4c72b-311">Tüm veri dilimi yukarı içinde olduğuna dikkat edin **hazır** (başlangıç saati bitiş saati için) ardışık düzen süresi geçmiş olduğundan belirtin.</span><span class="sxs-lookup"><span data-stu-id="4c72b-311">Notice that all the data slices up are in **Ready** state because the pipeline duration (start time to end time) is in the past.</span></span> <span data-ttu-id="4c72b-312">SQL Server veritabanında veri ekledikten ve bunu her zaman için de olabilir.</span><span class="sxs-lookup"><span data-stu-id="4c72b-312">It is also because you have inserted the data in the SQL Server database and it is there all the time.</span></span> <span data-ttu-id="4c72b-313">Hiç dilim gösterilmediğini onaylayın **sorunu dilimleri** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="4c72b-313">Confirm that no slices show up in the **Problem slices** section at the bottom.</span></span> <span data-ttu-id="4c72b-314">Tüm dilimleri görmek için tıklatın **daha görmek** dilimler listesinin altındaki.</span><span class="sxs-lookup"><span data-stu-id="4c72b-314">To view all the slices, click **See More** at the bottom of the list of slices.</span></span>
3. <span data-ttu-id="4c72b-315">Şimdi **veri kümeleri** sayfasında, **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-315">Now, In the **Datasets** page, click **OutputBlobTable**.</span></span>

    ![OputputBlobTable dilimleri](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. <span data-ttu-id="4c72b-317">Listeden herhangi bir veri dilimine tıklayın ve görmeniz gerekir **veri dilimi** sayfası.</span><span class="sxs-lookup"><span data-stu-id="4c72b-317">Click any data slice from the list and you should see the **Data Slice** page.</span></span> <span data-ttu-id="4c72b-318">Dilimin etkinlik çalışır bakın.</span><span class="sxs-lookup"><span data-stu-id="4c72b-318">You see activity runs for the slice.</span></span> <span data-ttu-id="4c72b-319">Yalnızca bir etkinlik genellikle bakın.</span><span class="sxs-lookup"><span data-stu-id="4c72b-319">You see only one activity run usually.</span></span>  

    ![Veri dilimi dikey penceresi](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    <span data-ttu-id="4c72b-321">Dilim **Hazır** durumunda değilse, Hazır olmayan ve geçerli dilimin yürütülmesini engelleyen yukarı akış dilimlerini **Hazır olmayan yukarı akış dilimleri** listesinde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c72b-321">If the slice is not in the **Ready** state, you can see the upstream slices that are not Ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span>
5. <span data-ttu-id="4c72b-322">Tıklatın **etkinlik** görmek için altındaki listeden **etkinlik çalışma ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-322">Click the **activity run** from the list at the bottom to see **activity run details**.</span></span>

   ![Etkinlik çalışma Ayrıntıları sayfası](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   <span data-ttu-id="4c72b-324">Verimlilik, süre ve veri aktarımı için kullanılan ağ geçidi gibi bilgileri görür.</span><span class="sxs-lookup"><span data-stu-id="4c72b-324">You would see information such as throughput, duration, and the gateway used to transfer the data.</span></span>
6. <span data-ttu-id="4c72b-325">Tıklatın **X** tüm sayfaları dek kapatmak için</span><span class="sxs-lookup"><span data-stu-id="4c72b-325">Click **X** to close all the pages until you</span></span>
7. <span data-ttu-id="4c72b-326">Giriş sayfasına geri dönmek **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="4c72b-326">get back to the home page for the **ADFTutorialOnPremDF**.</span></span>
8. <span data-ttu-id="4c72b-327">(isteğe bağlı) ' I tıklatın **ardışık düzen**, tıklatın **ADFTutorialOnPremDF**ve detaya girdi tablolarında (**tüketilen**) veya çıkış veri kümeleri (**üretilen**).</span><span class="sxs-lookup"><span data-stu-id="4c72b-327">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span></span>
9. <span data-ttu-id="4c72b-328">Gibi araçlar kullanın [Microsoft Storage Gezgini](http://storageexplorer.com/) blob/dosya her saat oluşturulduğunu doğrulamak için.</span><span class="sxs-lookup"><span data-stu-id="4c72b-328">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to verify that a blob/file is created for each hour.</span></span>

   ![Azure Depolama Gezgini](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a><span data-ttu-id="4c72b-330">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4c72b-330">Next steps</span></span>
* <span data-ttu-id="4c72b-331">Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) makale için veri yönetimi ağ geçidi ile ilgili tüm ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="4c72b-331">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the Data Management Gateway.</span></span>
* <span data-ttu-id="4c72b-332">Bkz: [kopyalama verileri Azure Blob'tan Azure SQL'e](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği bir havuz veri deposu için bir kaynak veri deposundan verileri taşımak için nasıl kullanılacağı hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="4c72b-332">See [Copy data from Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to learn about how to use Copy Activity to move data from a source data store to a sink data store.</span></span>
