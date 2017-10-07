---
title: SQL Data Warehouse verilerini aaaLoad terabayt | Microsoft Docs
description: "Azure Data Factory ile altında 15 dakika nasıl 1 TB'lık veriyi Azure SQL Data Warehouse'a yüklenebilir gösterir"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: a6c133c0-ced2-463c-86f0-a07b00c9e37f
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e63f60461b082b0e3979004cb631dbf4a6710de3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a><span data-ttu-id="d6b2b-103">1 TB altında 15 dakika Data Factory ile Azure SQL Data Warehouse'a veri yükleme</span><span class="sxs-lookup"><span data-stu-id="d6b2b-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Data Factory</span></span>
<span data-ttu-id="d6b2b-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) bir bulut tabanlı genişleme büyük miktarda veriyi, ilişkisel ve ilişkisel olmayan işleyebilen veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span>  <span data-ttu-id="d6b2b-105">SQL Data Warehouse, yüksek düzeyde paralel işleme (MPP) mimarisi üzerine kurulu, kurumsal veri ambarı iş yükleri için optimize edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-105">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span></span>  <span data-ttu-id="d6b2b-106">Bulut esneklik hello esneklik tooscale depolama ile ve bağımsız olarak işlem sunar.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-106">It offers cloud elasticity with hello flexibility tooscale storage and compute independently.</span></span>

<span data-ttu-id="d6b2b-107">Azure SQL Data Warehouse ile çalışmaya başlama artık her zamankinden kullanmaktan daha kolay **Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-107">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span></span>  <span data-ttu-id="d6b2b-108">Azure Data Factory kullanılan toopopulate hello verileri var olan sisteminizden ve SQL Data Warehouse değerlendirmek ve analizlerinizi oluşturma, değerli zamandan kaydetme ile SQL Data Warehouse olabilen bir bulut tabanlı tam olarak yönetilen bir veri tümleştirme hizmetidir çözümleri.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-108">Azure Data Factory is a fully managed cloud-based data integration service, which can be used toopopulate a SQL Data Warehouse with hello data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions.</span></span> <span data-ttu-id="d6b2b-109">Azure SQL Data Azure Data Factory kullanarak Warehouse'a veri yükleme hello avantajları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d6b2b-109">Here are hello key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span></span>

* <span data-ttu-id="d6b2b-110">**Yukarı kolay tooset**: 5-adım sezgisel Sihirbazı ile gerekli komut dosyası yok.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-110">**Easy tooset up**: 5-step intuitive wizard with no scripting required.</span></span>
* <span data-ttu-id="d6b2b-111">**Zengin veri depolamak Destek**: zengin bir şirket içi ve bulut tabanlı veri depoları için yerleşik destek.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-111">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span></span>
* <span data-ttu-id="d6b2b-112">**Güvenli ve uyumlu**: veriler HTTPS veya ExpressRoute üzerinden aktarılır ve küresel hizmet varlığı sağlar, verilerinizin hiçbir zaman hello coğrafi sınır bırakır</span><span class="sxs-lookup"><span data-stu-id="d6b2b-112">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves hello geographical boundary</span></span>
* <span data-ttu-id="d6b2b-113">**PolyBase kullanarak benzersiz performansı** – Polybase kullanarak hello en verimli şekilde toomove verilerin Azure SQL veri ambarında eder.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-113">**Unparalleled performance by using PolyBase** – Using Polybase is hello most efficient way toomove data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d6b2b-114">BLOB özelliği hazırlama hello kullanarak yüksek yük hızları, varsayılan olarak Polybase destekler hello veri depolarına Azure Blob Depolama yanı sıra tüm türlerinden elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-114">Using hello staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which hello Polybase supports by default.</span></span>

<span data-ttu-id="d6b2b-115">Bu makale size nasıl gösterir toouse Itanium tabanlı sistemler için Data Factory Kopyalama Sihirbazı tooload 1 TB veri Azure SQL veri ambarında Azure Blob Depolama'dan üzerinde 1,2 GB/sn üretilen işi en altında 15 dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-115">This article shows you how toouse Data Factory Copy Wizard tooload 1-TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span></span>

<span data-ttu-id="d6b2b-116">Bu makalede hello Kopyalama Sihirbazı'nı kullanarak Azure SQL Data Warehouse'a veri taşımak için adım adım yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-116">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using hello Copy Wizard.</span></span>

> [!NOTE]
>  <span data-ttu-id="d6b2b-117">Veri taşımada/Azure SQL Data Warehouse genel veri fabrikasının özellikleri hakkında bilgi için bkz: [Azure SQL veri Azure Data Factory kullanarak ambarından veri tooand taşıma](data-factory-azure-sql-data-warehouse-connector.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-117">For general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse, see [Move data tooand from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article.</span></span>
>
> <span data-ttu-id="d6b2b-118">Ayrıca, Azure portalı, Visual Studio, PowerShell kullanılarak işlem hatlarını oluşturabilirsiniz vs. Bkz: [Öğreticisi: Azure Blob tooAzure SQL veritabanı ' veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) hızlı bir kılavuz hello kopya etkinliği Azure Data Factory kullanarak için adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-118">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob tooAzure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using hello Copy Activity in Azure Data Factory.</span></span>  
>
>

## <a name="prerequisites"></a><span data-ttu-id="d6b2b-119">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d6b2b-119">Prerequisites</span></span>
* <span data-ttu-id="d6b2b-120">Azure Blob Storage: TPC-H sınama veri kümesi depolamak için bu denemeyi Azure Blob Depolama (GRS) kullanır.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-120">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span></span>  <span data-ttu-id="d6b2b-121">Azure depolama hesabınız yoksa, bilgi [nasıl toocreate bir depolama hesabı](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="d6b2b-121">If you do not have an Azure storage account, learn [how toocreate a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="d6b2b-122">[TPC-H](http://www.tpc.org/tpch/) veri: biz toouse TPC-H sınama veri kümesi hello gibi yapacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-122">[TPC-H](http://www.tpc.org/tpch/) data: we are going toouse TPC-H as hello testing dataset.</span></span>  <span data-ttu-id="d6b2b-123">toouse gerekir, toodo `dbgen` TPC-H araç setinin yardımcı olan, hello veri kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-123">toodo that, you need toouse `dbgen` from TPC-H toolkit, which helps you generate hello dataset.</span></span>  <span data-ttu-id="d6b2b-124">Kaynak kodu ya da indirebilirsiniz `dbgen` gelen [TPC Araçları](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) ve kendinize veya indirme derlenmiş hello ikiliden derleme [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span><span class="sxs-lookup"><span data-stu-id="d6b2b-124">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download hello compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span></span>  <span data-ttu-id="d6b2b-125">Merhaba aşağıdaki ile çalışma dbgen.exe komutları toogenerate 1 TB düz dosya için `lineitem` yayılan 10 dosyalardaki tablosu:</span><span class="sxs-lookup"><span data-stu-id="d6b2b-125">Run dbgen.exe with hello following commands toogenerate 1 TB flat file for `lineitem` table spread across 10 files:</span></span>

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * <span data-ttu-id="d6b2b-126">…</span><span class="sxs-lookup"><span data-stu-id="d6b2b-126">…</span></span>
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    <span data-ttu-id="d6b2b-127">Şimdi dosyaları tooAzure Blob kopyalama hello oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-127">Now copy hello generated files tooAzure Blob.</span></span>  <span data-ttu-id="d6b2b-128">Çok başvuran[taşıma veri tooand bir şirket içi dosya sisteminden Azure Data Factory kullanarak](data-factory-onprem-file-system-connector.md) nasıl toodo, ADF kopyalama kullanarak.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-128">Refer too[Move data tooand from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how toodo that using ADF Copy.</span></span>    
* <span data-ttu-id="d6b2b-129">Azure SQL Data Warehouse: Azure SQL Data Warehouse 6,000 Dwu ile oluşturulan veri bu deneme yükler</span><span class="sxs-lookup"><span data-stu-id="d6b2b-129">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span></span>

    <span data-ttu-id="d6b2b-130">Çok başvuran[bir Azure SQL Data Warehouse oluşturma](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) veritabanı nasıl toocreate SQL veri ambarı hakkında ayrıntılı yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-130">Refer too[Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how toocreate a SQL Data Warehouse database.</span></span>  <span data-ttu-id="d6b2b-131">tooget hello en iyi olası yük performans Polybase kullanarak SQL Data Warehouse, veri ambarı birimlerini (Dwu'lar) 6,000 Dwu olan hello performans ayarında, izin verilen en fazla sayısını seçin.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-131">tooget hello best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in hello Performance setting, which is 6,000 DWUs.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d6b2b-132">Azure Blob'tan yüklenirken hello veri performans yükleme orantılı toohello hello SQL veri ambarı hakkında yapılandırma Dwu sayısıdır:</span><span class="sxs-lookup"><span data-stu-id="d6b2b-132">When loading from Azure Blob, hello data loading performance is directly proportional toohello number of DWUs you configure on hello SQL Data Warehouse:</span></span>
  >
  > <span data-ttu-id="d6b2b-133">1 TB 1.000 yüklenirken DWU SQL Data Warehouse 87 dakika (~ 200 MB/sn verim) yükleme 1 TB 14 dakika (~1.2 GB/sn verim) alır 46 dakika (~ 380 MB/sn verim) yükleme 1 TB 6,000 DWU SQL veri ambarında sürer 2.000 DWU SQL Data Warehouse'a alır</span><span class="sxs-lookup"><span data-stu-id="d6b2b-133">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87 minutes (~200 MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46 minutes (~380 MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14 minutes (~1.2 GBps throughput)</span></span>
  >
  >

    <span data-ttu-id="d6b2b-134">toocreate SQL Data Warehouse 6,000 dwu'larla Taşı hello performans kaydırıcı tüm hello yolu toohello sağ:</span><span class="sxs-lookup"><span data-stu-id="d6b2b-134">toocreate a SQL Data Warehouse with 6,000 DWUs, move hello Performance slider all hello way toohello right:</span></span>

    ![Performans kaydırıcı](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    <span data-ttu-id="d6b2b-136">6000 Dwu ile yapılandırılmamış bir var olan veritabanı için bunu Azure portal kullanarak ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-136">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span></span>  <span data-ttu-id="d6b2b-137">Azure portalında toohello veritabanı gidin ve var olan bir **ölçek** hello düğmesini **genel bakış** görüntü aşağıdaki hello gösterilen paneli:</span><span class="sxs-lookup"><span data-stu-id="d6b2b-137">Navigate toohello database in Azure portal, and there is a **Scale** button in hello **Overview** panel shown in hello following image:</span></span>

    ![Ölçek düğmesi](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    <span data-ttu-id="d6b2b-139">Hello tıklatın **ölçek** düğmesini tooopen hello aşağıdaki panel, hello kaydırıcı toohello en büyük değer taşıyın ve tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-139">Click hello **Scale** button tooopen hello following panel, move hello slider toohello maximum value, and click **Save** button.</span></span>

    ![Ölçek iletişim](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    <span data-ttu-id="d6b2b-141">Azure SQL Data Warehouse kullanarak verileri bu deneme yükler `xlargerc` kaynak sınıfı.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-141">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span></span>

    <span data-ttu-id="d6b2b-142">tooachieve en iyi olası verimlilik, kopyalama gereken çok ait olan bir SQL Data Warehouse kullanıcı kullanılarak gerçekleştirilen toobe`xlargerc` kaynak sınıfı.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-142">tooachieve best possible throughput, copy needs toobe performed using a SQL Data Warehouse user belonging too`xlargerc` resource class.</span></span>  <span data-ttu-id="d6b2b-143">Bilgi nasıl toodo, izleyerek [kullanıcı kaynak sınıfı örneğini değiştirmek](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="d6b2b-143">Learn how toodo that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>  
* <span data-ttu-id="d6b2b-144">Hedef Tablo şemasını Azure SQL veri ambarı veritabanında DDL deyimi aşağıdaki hello çalıştırarak oluşturun:</span><span class="sxs-lookup"><span data-stu-id="d6b2b-144">Create destination table schema in Azure SQL Data Warehouse database, by running hello following DDL statement:</span></span>

    ```SQL  
    CREATE TABLE [dbo].[lineitem]
    (
        [L_ORDERKEY] [bigint] NOT NULL,
        [L_PARTKEY] [bigint] NOT NULL,
        [L_SUPPKEY] [bigint] NOT NULL,
        [L_LINENUMBER] [int] NOT NULL,
        [L_QUANTITY] [decimal](15, 2) NULL,
        [L_EXTENDEDPRICE] [decimal](15, 2) NULL,
        [L_DISCOUNT] [decimal](15, 2) NULL,
        [L_TAX] [decimal](15, 2) NULL,
        [L_RETURNFLAG] [char](1) NULL,
        [L_LINESTATUS] [char](1) NULL,
        [L_SHIPDATE] [date] NULL,
        [L_COMMITDATE] [date] NULL,
        [L_RECEIPTDATE] [date] NULL,
        [L_SHIPINSTRUCT] [char](25) NULL,
        [L_SHIPMODE] [char](10) NULL,
        [L_COMMENT] [varchar](44) NULL
    )
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    ```
<span data-ttu-id="d6b2b-145">Tamamlanan hello önkoşul adımları ile artık hazır tooconfigure hello kopyalama etkinliği hello Kopyalama Sihirbazı'nı kullanarak duyuyoruz.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-145">With hello prerequisite steps completed, we are now ready tooconfigure hello copy activity using hello Copy Wizard.</span></span>

## <a name="launch-copy-wizard"></a><span data-ttu-id="d6b2b-146">Kopyalama Sihirbazı'nı başlatma</span><span class="sxs-lookup"><span data-stu-id="d6b2b-146">Launch Copy Wizard</span></span>
1. <span data-ttu-id="d6b2b-147">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d6b2b-147">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d6b2b-148">Tıklatın **+ yeni** hello sol üst köşeden tıklatın **Intelligence + analiz**, tıklatıp **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-148">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="d6b2b-149">Merhaba, **yeni data factory** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="d6b2b-149">In hello **New data factory** blade:</span></span>

   1. <span data-ttu-id="d6b2b-150">Girin **LoadIntoSQLDWDataFactory** hello için **adı**.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-150">Enter **LoadIntoSQLDWDataFactory** for hello **name**.</span></span>
       <span data-ttu-id="d6b2b-151">Merhaba hello Azure veri fabrikasının adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-151">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="d6b2b-152">Merhaba hatayı alırsanız: **veri fabrikası adı "LoadIntoSQLDWDataFactory" kullanılabilir değil**hello veri fabrikası (örneğin, yournameLoadIntoSQLDWDataFactory) hello adını değiştirin ve oluşturmayı yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-152">If you receive hello error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change hello name of hello data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span></span> <span data-ttu-id="d6b2b-153">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
   2. <span data-ttu-id="d6b2b-154">Azure **aboneliğinizi** seçin.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-154">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="d6b2b-155">Kaynak grubu için aşağıdaki adımları hello birini yapın:</span><span class="sxs-lookup"><span data-stu-id="d6b2b-155">For Resource Group, do one of hello following steps:</span></span>
      1. <span data-ttu-id="d6b2b-156">Seçin **var olanı kullan** tooselect varolan bir kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-156">Select **Use existing** tooselect an existing resource group.</span></span>
      2. <span data-ttu-id="d6b2b-157">Seçin **Yeni Oluştur** tooenter bir kaynak grubu için bir ad.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-157">Select **Create new** tooenter a name for a resource group.</span></span>
   4. <span data-ttu-id="d6b2b-158">Seçin bir **konumu** hello veri fabrikası için.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-158">Select a **location** for hello data factory.</span></span>
   5. <span data-ttu-id="d6b2b-159">Seçin **PIN toodashboard** hello dikey penceresinde hello altındaki onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-159">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>  
   6. <span data-ttu-id="d6b2b-160">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-160">Click **Create**.</span></span>
4. <span data-ttu-id="d6b2b-161">Merhaba oluşturma işlemi tamamlandıktan sonra hello bkz **Data Factory** dikey penceresini hello görüntü aşağıdaki gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="d6b2b-161">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image:</span></span>

   ![Data factory giriş sayfası](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. <span data-ttu-id="d6b2b-163">Merhaba Hello Data Factory giriş sayfasında, tıklatın **veri kopyalama** toolaunch döşeme **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-163">On hello Data Factory home page, click hello **Copy data** tile toolaunch **Copy Wizard**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d6b2b-164">Bu hello web tarayıcısının "Yetkilendiriliyor..." takılmış görürseniz, devre dışı bırakın/işaretini kaldırın **üçüncü taraf tanımlama bilgilerini engelleyebilir ve site verileri** ayarlama (veya) etkin ve oluşturmak için bir özel durum **login.microsoftonline.com**ve hello Sihirbazı yeniden başlatmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-164">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a><span data-ttu-id="d6b2b-165">1. adım: veri zamanlama yükleme yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d6b2b-165">Step 1: Configure data loading schedule</span></span>
<span data-ttu-id="d6b2b-166">Merhaba ilk adımı Zamanlama yüklenirken tooconfigure hello verilerdir.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-166">hello first step is tooconfigure hello data loading schedule.</span></span>  

<span data-ttu-id="d6b2b-167">Merhaba, **özellikleri** sayfa:</span><span class="sxs-lookup"><span data-stu-id="d6b2b-167">In hello **Properties** page:</span></span>

1. <span data-ttu-id="d6b2b-168">Girin **CopyFromBlobToAzureSqlDataWarehouse** için **görev adı**</span><span class="sxs-lookup"><span data-stu-id="d6b2b-168">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span></span>
2. <span data-ttu-id="d6b2b-169">Seçin **kez Şimdi Çalıştır** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-169">Select **Run once now** option.</span></span>   
3. <span data-ttu-id="d6b2b-170">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-170">Click **Next**.</span></span>  

    ![Kopyalama Sihirbazı - Özellikler sayfası](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a><span data-ttu-id="d6b2b-172">2. adım: kaynak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d6b2b-172">Step 2: Configure source</span></span>
<span data-ttu-id="d6b2b-173">Adımları tooconfigure hello kaynak hello bu bölümü gösterir: Azure Blob içeren hello 1 TB TPC-H satır öğesi dosyaları.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-173">This section shows you hello steps tooconfigure hello source: Azure Blob containing hello 1-TB TPC-H line item files.</span></span>

1. <span data-ttu-id="d6b2b-174">Select hello **Azure Blob Storage** hello veri depolamak ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-174">Select hello **Azure Blob Storage** as hello data store and click **Next**.</span></span>

    ![Kopyalama Sihirbazı - Kaynak Seç sayfası](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. <span data-ttu-id="d6b2b-176">Hello Azure Blob Depolama hesabı hello bağlantı bilgileri girin ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-176">Fill in hello connection information for hello Azure Blob storage account, and click **Next**.</span></span>

    ![Kopyalama Sihirbazı - kaynağı bağlantı bilgileri](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. <span data-ttu-id="d6b2b-178">Merhaba seçin **klasörü** hello TPC-H satırını içeren öğe dosyaları ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-178">Choose hello **folder** containing hello TPC-H line item files and click **Next**.</span></span>

    ![Kopyalama Sihirbazı - giriş klasörü seçin](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. <span data-ttu-id="d6b2b-180">Tıklatarak bağlı **sonraki**, hello dosya biçimi ayarları otomatik olarak algılanır.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-180">Upon clicking **Next**, hello file format settings are detected automatically.</span></span>  <span data-ttu-id="d6b2b-181">Bu sütun sınırlayıcı emin toomake denetleyin ' | 'yerine hello varsayılan virgül','.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-181">Check toomake sure that column delimiter is ‘|’ instead of hello default comma ‘,’.</span></span>  <span data-ttu-id="d6b2b-182">Tıklatın **sonraki** hello veri önizlemesi sonra.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-182">Click **Next** after you have previewed hello data.</span></span>

    ![Kopyalama Sihirbazı - dosya biçimi ayarları](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a><span data-ttu-id="d6b2b-184">3. adım: hedef yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d6b2b-184">Step 3: Configure destination</span></span>
<span data-ttu-id="d6b2b-185">Bu bölümde, nasıl tooconfigure hello hedef gösterir: `lineitem` hello Azure SQL Data Warehouse veritabanı tablosunda.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-185">This section shows you how tooconfigure hello destination: `lineitem` table in hello Azure SQL Data Warehouse database.</span></span>

1. <span data-ttu-id="d6b2b-186">Seçin **Azure SQL Data Warehouse** hello hedef olarak depolamak ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-186">Choose **Azure SQL Data Warehouse** as hello destination store and click **Next**.</span></span>

    ![Kopyalama Sihirbazı - select hedef veri deposu](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. <span data-ttu-id="d6b2b-188">Azure SQL Data Warehouse hello bağlantı bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-188">Fill in hello connection information for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="d6b2b-189">Hello rolünün bir üyesi olan hello kullanıcının belirttiğinizden emin olun `xlargerc` (Merhaba bkz **önkoşulları** ayrıntılı yönergeler için bölüm), tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-189">Make sure you specify hello user that is a member of hello role `xlargerc` (see hello **prerequisites** section for detailed instructions), and click **Next**.</span></span>

    ![Kopyalama Sihirbazı - hedef bağlantı bilgileri](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. <span data-ttu-id="d6b2b-191">Merhaba hedef tablo seçin ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-191">Choose hello destination table and click **Next**.</span></span>

    ![Kopyalama Sihirbazı - Tablo eşleme sayfası](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. <span data-ttu-id="d6b2b-193">Şema Eşleme sayfasında "Sütun eşlemesi uygulama" seçeneği işaretsiz bırakın ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-193">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span></span>

## <a name="step-4-performance-settings"></a><span data-ttu-id="d6b2b-194">4. adım: Performans ayarları</span><span class="sxs-lookup"><span data-stu-id="d6b2b-194">Step 4: Performance settings</span></span>

<span data-ttu-id="d6b2b-195">**Polybase izin** varsayılan olarak işaretli.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-195">**Allow polybase** is checked by default.</span></span>  <span data-ttu-id="d6b2b-196">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-196">Click **Next**.</span></span>

![Kopyalama Sihirbazı - şema eşleme sayfası](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a><span data-ttu-id="d6b2b-198">5. adım: Dağıtma ve yükleme sonuçları izleme</span><span class="sxs-lookup"><span data-stu-id="d6b2b-198">Step 5: Deploy and monitor load results</span></span>
1. <span data-ttu-id="d6b2b-199">Tıklatın **son** düğmesini toodeploy.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-199">Click **Finish** button toodeploy.</span></span>

    ![Kopyalama Sihirbazı - Özet sayfası](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. <span data-ttu-id="d6b2b-201">Merhaba dağıtım tamamlandıktan sonra tıklayın `Click here toomonitor copy pipeline` toomonitor hello kopyalama ilerleme çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-201">After hello deployment is complete, click `Click here toomonitor copy pipeline` toomonitor hello copy run progress.</span></span> <span data-ttu-id="d6b2b-202">Select hello kopyalama işlem hattını hello oluşturduğunuz **etkinlik Windows** listesi.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-202">Select hello copy pipeline you created in hello **Activity Windows** list.</span></span>

    ![Kopyalama Sihirbazı - Özet sayfası](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    <span data-ttu-id="d6b2b-204">Ayrıntı hello çalıştırın hello kopyalama görüntüleyebilirsiniz **etkinlik penceresini Explorer** panelinde kaynaktan okunan ve hedef, süre ve hello ortalama verimi hello çalıştırmak için yazılan hello veri birimi içeren hello doğru.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-204">You can view hello copy run details in hello **Activity Window Explorer** in hello right panel, including hello data volume read from source and written into destination, duration, and hello average throughput for hello run.</span></span>

    <span data-ttu-id="d6b2b-205">Aşağıdaki ekran görüntüsü, 1 TB Azure Blob depolama alanından SQL Data Warehouse'a veri kopyalama hello gelen gördüğünüz etkili bir şekilde 1.22 GBps verimlilik elde 14 dakika sürdü!</span><span class="sxs-lookup"><span data-stu-id="d6b2b-205">As you can see from hello following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span></span>

    ![Kopyalama Sihirbazı - başarılı oldu, iletişim kutusu](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a><span data-ttu-id="d6b2b-207">En iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="d6b2b-207">Best practices</span></span>
<span data-ttu-id="d6b2b-208">Azure SQL Data Warehouse veritabanınızı çalıştırmak için birkaç en iyi uygulamalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d6b2b-208">Here are a few best practices for running your Azure SQL Data Warehouse database:</span></span>

* <span data-ttu-id="d6b2b-209">Daha büyük bir kaynak sınıfı, bir kümelenmiş COLUMNSTORE DİZİNİNE yüklerken kullanın.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-209">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span></span>
* <span data-ttu-id="d6b2b-210">Daha verimli birleştirmeler için hepsini bir kez deneme dağıtımı varsayılan yerine select bir sütuna göre karma dağıtım kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-210">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span></span>
* <span data-ttu-id="d6b2b-211">İçin daha hızlı yük hızları, geçici verileri öbek kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-211">For faster load speeds, consider using heap for transient data.</span></span>
* <span data-ttu-id="d6b2b-212">Azure SQL Data Warehouse yüklemeyi bitirdikten sonra İstatistikler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-212">Create statistics after you finish loading Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="d6b2b-213">Bkz: [en iyi uygulamalar Azure SQL Data Warehouse için](../sql-data-warehouse/sql-data-warehouse-best-practices.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-213">See [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6b2b-214">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d6b2b-214">Next steps</span></span>
* <span data-ttu-id="d6b2b-215">[Data Factory Kopyalama Sihirbazı](data-factory-copy-wizard.md) -bu makalede hello Kopyalama Sihirbazı hakkında ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about hello Copy Wizard.</span></span>
* <span data-ttu-id="d6b2b-216">[Etkinlik performans ve ayarlama Kılavuzu kopyalama](data-factory-copy-activity-performance.md) -bu makalede hello başvuru performans ölçümleri ve ayarlama kılavuzu içerir.</span><span class="sxs-lookup"><span data-stu-id="d6b2b-216">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains hello reference performance measurements and tuning guide.</span></span>
