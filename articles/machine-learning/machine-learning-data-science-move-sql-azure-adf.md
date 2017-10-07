---
title: "bir şirket içi SQL Server tooSQL Azure Data Factory ile Azure aaaMove verilerden | Microsoft Docs"
description: "Merhaba bulutta içi veritabanları arasında verileri günlük olarak birlikte taşımak iki veri taşıma etkinlikleri oluşturur bir ADF ardışık ayarlayın."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 7f7e78c7a84a259539221d3235b76bb5a3cf9866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-sql-server-toosql-azure-with-azure-data-factory"></a><span data-ttu-id="cddbc-103">Bir şirket içi SQL server tooSQL Azure Azure Data Factory ile veri taşıma</span><span class="sxs-lookup"><span data-stu-id="cddbc-103">Move data from an on-premises SQL server tooSQL Azure with Azure Data Factory</span></span>
<span data-ttu-id="cddbc-104">Bu konu, Azure Blob Storage kullanarak aracılığıyla bir şirket içi SQL Server veritabanı tooa SQL Azure veritabanı toomove verileri Azure veri fabrikası (ADF) nasıl hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="cddbc-104">This topic shows how toomove data from an on-premises SQL Server Database tooa SQL Azure Database via Azure Blob Storage using hello Azure Data Factory (ADF).</span></span>

<span data-ttu-id="cddbc-105">Taşıma veri tooan Azure SQL veritabanı için çeşitli seçenekler özetler bir tablo için bkz: [Azure Machine Learning için verileri tooan Azure SQL veritabanı taşıma](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="cddbc-105">For a table that summarizes various options for moving data tooan Azure SQL Database, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

## <span data-ttu-id="cddbc-106"><a name="intro"></a>Giriş: ADF nedir ve ne zaman kullanılan toomigrate veriler olmalıdır?</span><span class="sxs-lookup"><span data-stu-id="cddbc-106"><a name="intro"></a>Introduction: What is ADF and when should it be used toomigrate data?</span></span>
<span data-ttu-id="cddbc-107">Azure Data Factory düzenler ve hello taşınmasını ve dönüştürülmesini veri otomatikleştiren bir bulut tabanlı tam olarak yönetilen bir veri tümleştirme hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="cddbc-107">Azure Data Factory is a fully managed cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="cddbc-108">Merhaba anahtar hello ADF modelinde ardışık düzen kavramdır.</span><span class="sxs-lookup"><span data-stu-id="cddbc-108">hello key concept in hello ADF model is pipeline.</span></span> <span data-ttu-id="cddbc-109">Bir ardışık düzen veri kümelerinde bulunan hello verileri üzerindeki hello Eylemler tooperform tanımlar, her biri bir mantıksal etkinlikleri gruplandırmasıdır.</span><span class="sxs-lookup"><span data-stu-id="cddbc-109">A pipeline is a logical grouping of Activities, each of which defines hello actions tooperform on hello data contained in Datasets.</span></span> <span data-ttu-id="cddbc-110">Bağlı hizmetler Data Factory tooconnect toohello veri kaynakları için gerekli kullanılan toodefine hello bilgilerdir.</span><span class="sxs-lookup"><span data-stu-id="cddbc-110">Linked services are used toodefine hello information needed for Data Factory tooconnect toohello data resources.</span></span>

<span data-ttu-id="cddbc-111">ADF ile mevcut veri işleme Hizmetleri hello bulutta yüksek oranda kullanılabilir ve yönetilen veri ardışık içine birleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="cddbc-111">With ADF, existing data processing services can be composed into data pipelines that are highly available and managed in hello cloud.</span></span> <span data-ttu-id="cddbc-112">Bu veri ardışık zamanlanmış tooingest olması, hazırlamak, dönüştürmek, analiz ve verilerini yayımlamak ve ADF yönetir ve hello karmaşık veri ve işleme bağımlılıkları yönetir.</span><span class="sxs-lookup"><span data-stu-id="cddbc-112">These data pipelines can be scheduled tooingest, prepare, transform, analyze, and publish data, and ADF manages and orchestrates hello complex data and processing dependencies.</span></span> <span data-ttu-id="cddbc-113">Çözümleri hızla yerleşik ve içinde dağıtılan hello bulut, şirket içi artan sayıda bağlanma ve veri kaynakları bulut değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cddbc-113">Solutions can be quickly built and deployed in hello cloud, connecting a growing number of on-premises and cloud data sources.</span></span>

<span data-ttu-id="cddbc-114">ADF kullanmayı dikkate alın:</span><span class="sxs-lookup"><span data-stu-id="cddbc-114">Consider using ADF:</span></span>

* <span data-ttu-id="cddbc-115">ne zaman gereksinimlerini toobe sürekli olarak her ikisi de erişen bir karma senaryoda geçirilen verileri şirket içi ve bulut kaynakları</span><span class="sxs-lookup"><span data-stu-id="cddbc-115">when data needs toobe continually migrated in a hybrid scenario that accesses both on-premises and cloud resources</span></span>
* <span data-ttu-id="cddbc-116">ne zaman hello veri işlem yapılan işlem veya gereksinimlerini toobe değiştirilmiş veya iş mantığı sahip Geçirilmekte olan tooit eklenmesi.</span><span class="sxs-lookup"><span data-stu-id="cddbc-116">when hello data is transacted or needs toobe modified or have business logic added tooit when being migrated.</span></span>

<span data-ttu-id="cddbc-117">Zamanlama ve düzenli aralıklarla veri hello hareketini yönetmek basit JSON komut dosyalarını kullanarak iş izleme hello ADF sağlar.</span><span class="sxs-lookup"><span data-stu-id="cddbc-117">ADF allows for hello scheduling and monitoring of jobs using simple JSON scripts that manage hello movement of data on a periodic basis.</span></span> <span data-ttu-id="cddbc-118">ADF karmaşık işlemleri için destek gibi diğer özellikleri de vardır.</span><span class="sxs-lookup"><span data-stu-id="cddbc-118">ADF also has other capabilities such as support for complex operations.</span></span> <span data-ttu-id="cddbc-119">Hello belgelerine ADF hakkında daha fazla bilgi için bkz: [Azure veri fabrikası (ADF)](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="cddbc-119">For more information on ADF, see hello documentation at [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span></span>

## <span data-ttu-id="cddbc-120"><a name="scenario"></a>Merhaba senaryosu</span><span class="sxs-lookup"><span data-stu-id="cddbc-120"><a name="scenario"></a>hello Scenario</span></span>
<span data-ttu-id="cddbc-121">İki veri taşıma etkinlikleri oluşturur bir ADF ardışık ayarlarız.</span><span class="sxs-lookup"><span data-stu-id="cddbc-121">We set up an ADF pipeline that composes two data migration activities.</span></span> <span data-ttu-id="cddbc-122">Birlikte bunlar verileri günlük olarak bir şirket içi SQL database ve Azure SQL Database hello bulutta arasında taşıyın.</span><span class="sxs-lookup"><span data-stu-id="cddbc-122">Together they move data on a daily basis between an on-premises SQL database and an Azure SQL Database in hello cloud.</span></span> <span data-ttu-id="cddbc-123">Merhaba iki etkinlik şunlardır:</span><span class="sxs-lookup"><span data-stu-id="cddbc-123">hello two activities are:</span></span>

* <span data-ttu-id="cddbc-124">bir şirket içi SQL Server veritabanı tooan Azure Blob Storage hesabı veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="cddbc-124">copy data from an on-premises SQL Server database tooan Azure Blob Storage account</span></span>
* <span data-ttu-id="cddbc-125">verileri hello Azure Blob Storage hesabı tooan ' Azure SQL veritabanı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="cddbc-125">copy data from hello Azure Blob Storage account tooan Azure SQL Database.</span></span>

> [!NOTE]
> <span data-ttu-id="cddbc-126">Merhaba burada olmuştur hello ADF ekibi tarafından sağlanan öğretici ayrıntılı hello gelen uyarlanmış gösterilen adımlar: [şirket içi kaynakları ve veri yönetimi ağ geçidi ile bulut arasında veri taşıma](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) başvuran toohello bu konunun ilgili bölümleri uygun olduğunda sağlanır.</span><span class="sxs-lookup"><span data-stu-id="cddbc-126">hello steps shown here have been adapted from hello more detailed tutorial provided by hello ADF team: [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) References toohello relevant sections of that topic are provided when appropriate.</span></span>
>
>

## <span data-ttu-id="cddbc-127"><a name="prereqs"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="cddbc-127"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="cddbc-128">Bu öğretici, sahip olduğunuz varsayılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="cddbc-128">This tutorial assumes you have:</span></span>

* <span data-ttu-id="cddbc-129">Bir **Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="cddbc-129">An **Azure subscription**.</span></span> <span data-ttu-id="cddbc-130">Bir aboneliğiniz yoksa [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cddbc-130">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="cddbc-131">Bir **Azure depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="cddbc-131">An **Azure storage account**.</span></span> <span data-ttu-id="cddbc-132">Bu öğreticide hello verileri depolamak için bir Azure depolama hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="cddbc-132">You use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="cddbc-133">Bir Azure depolama hesabınız yoksa, hello bkz [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) makalesi.</span><span class="sxs-lookup"><span data-stu-id="cddbc-133">If you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="cddbc-134">Merhaba depolama hesabı oluşturduktan sonra anahtarı tooaccess hello depolama kullanılan tooobtain hello hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cddbc-134">After you have created hello storage account, you need tooobtain hello account key used tooaccess hello storage.</span></span> <span data-ttu-id="cddbc-135">Bkz: [depolama erişim tuşlarınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="cddbc-135">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="cddbc-136">Erişim tooan **Azure SQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="cddbc-136">Access tooan **Azure SQL Database**.</span></span> <span data-ttu-id="cddbc-137">Bir Azure SQL veritabanı ayarlanması, tpoic hello [Microsoft Azure SQL veritabanı ile çalışmaya başlama ](../sql-database/sql-database-get-started.md) ilgili bilgiler verilmektedir tooprovision bir Azure SQL veritabanına yeni bir örneğini.</span><span class="sxs-lookup"><span data-stu-id="cddbc-137">If you must set up an Azure SQL Database, hello tpoic [Getting Started with Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) provides information on how tooprovision a new instance of an Azure SQL Database.</span></span>
* <span data-ttu-id="cddbc-138">Yüklenmiş ve yapılandırılmış **Azure PowerShell** yerel olarak.</span><span class="sxs-lookup"><span data-stu-id="cddbc-138">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="cddbc-139">Yönergeler için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cddbc-139">For instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!NOTE]
> <span data-ttu-id="cddbc-140">Bu yordam hello kullanır [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cddbc-140">This procedure uses hello [Azure portal](https://portal.azure.com/).</span></span>
>
>

## <span data-ttu-id="cddbc-141"><a name="upload-data"></a>Karşıya yükleme hello veri tooyour içi SQL Server</span><span class="sxs-lookup"><span data-stu-id="cddbc-141"><a name="upload-data"></a> Upload hello data tooyour on-premises SQL Server</span></span>
<span data-ttu-id="cddbc-142">Merhaba kullanırız [NYC ücreti dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) toodemonstrate hello geçiş işlemi.</span><span class="sxs-lookup"><span data-stu-id="cddbc-142">We use hello [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) toodemonstrate hello migration process.</span></span> <span data-ttu-id="cddbc-143">Merhaba NYC ücreti dataset Azure blob depolama o post belirtildiği gibi kullanılabilir [NYC ücreti verileri](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="cddbc-143">hello NYC Taxi dataset is available, as noted in that post, on Azure blob storage [NYC Taxi Data](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="cddbc-144">Hello veri iki dosya, seyahat ayrıntılarını içeren, hello trip_data.csv dosyası ve her seyahat için ücretli hello ücreti ayrıntılarını içeren hello trip_far.csv dosyası vardır.</span><span class="sxs-lookup"><span data-stu-id="cddbc-144">hello data has two files, hello trip_data.csv file, which contains trip details, and hello  trip_far.csv file, which contains details of hello fare paid for each trip.</span></span> <span data-ttu-id="cddbc-145">Bir örnek ve bu dosyaların açıklaması sağlanan [NYC ücreti dönüşleri veri kümesi tanımı](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span><span class="sxs-lookup"><span data-stu-id="cddbc-145">A sample and description of these files are provided in [NYC Taxi Trips Dataset Description](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span></span>

<span data-ttu-id="cddbc-146">Burada, kendi veri kümesini tooa sağlanan hello yordamı uyarlamak veya hello NYC ücreti dataset kullanarak açıklandığı gibi hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="cddbc-146">You can either adapt hello procedure provided here tooa set of your own data or follow hello steps as described by using hello NYC Taxi dataset.</span></span> <span data-ttu-id="cddbc-147">tooupload Merhaba, şirket içi SQL Server veritabanınızın NYC ücreti kümesine özetlenen hello yordamı izleyin [toplu içeri aktarma verileri SQL Server veritabanına](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span><span class="sxs-lookup"><span data-stu-id="cddbc-147">tooupload hello NYC Taxi dataset into your on-premises SQL Server database, follow hello procedure outlined in [Bulk Import Data into SQL Server Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span></span> <span data-ttu-id="cddbc-148">SQL Server üzerinde bir Azure sanal makine için bu yönergeleri bağlıdır, ancak şirket içi SQL Server toohello yüklemeyle hello yordamı hello aynı.</span><span class="sxs-lookup"><span data-stu-id="cddbc-148">These instructions are for a SQL Server on an Azure Virtual Machine, but hello procedure for uploading toohello on-premises SQL Server is hello same.</span></span>

## <span data-ttu-id="cddbc-149"><a name="create-adf"></a>Bir Azure Data Factory oluşturma</span><span class="sxs-lookup"><span data-stu-id="cddbc-149"><a name="create-adf"></a> Create an Azure Data Factory</span></span>
<span data-ttu-id="cddbc-150">Merhaba hello yeni bir Azure Data Factory ve bir kaynak grubu oluşturmak için yönergeler [Azure portal](https://portal.azure.com/) sağlanan [bir Azure Data Factory oluşturmak](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span><span class="sxs-lookup"><span data-stu-id="cddbc-150">hello instructions for creating a new Azure Data Factory and a resource group in hello [Azure portal](https://portal.azure.com/) are provided [Create an Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span></span> <span data-ttu-id="cddbc-151">Ad hello yeni ADF örnek *adfdsp* ve oluşturulan ad hello kaynak grubu *adfdsprg*.</span><span class="sxs-lookup"><span data-stu-id="cddbc-151">Name hello new ADF instance *adfdsp* and name hello resource group created *adfdsprg*.</span></span>

## <a name="install-and-configure-up-hello-data-management-gateway"></a><span data-ttu-id="cddbc-152">Yükleme ve veri yönetimi ağ geçidi hello yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cddbc-152">Install and configure up hello Data Management Gateway</span></span>
<span data-ttu-id="cddbc-153">tooenable hatlarınızı tooadd gereken bir şirket içi SQL Server ile bir Azure data factory toowork içinde bir bağlantılı hizmet toohello veri fabrikası olarak.</span><span class="sxs-lookup"><span data-stu-id="cddbc-153">tooenable your pipelines in an Azure data factory toowork with an on-premises SQL Server, you need tooadd it as a Linked Service toohello data factory.</span></span> <span data-ttu-id="cddbc-154">Bağlantılı hizmeti bir şirket içi SQL Server için bir toocreate, şunları yapmalısınız:</span><span class="sxs-lookup"><span data-stu-id="cddbc-154">toocreate a Linked Service for an on-premises SQL Server, you must:</span></span>

* <span data-ttu-id="cddbc-155">indirin ve Microsoft Veri Yönetimi ağ geçidi hello şirket içi bilgisayara yükleyin.</span><span class="sxs-lookup"><span data-stu-id="cddbc-155">download and install Microsoft Data Management Gateway onto hello on-premises computer.</span></span>
* <span data-ttu-id="cddbc-156">Merhaba bağlantılı hizmeti hello şirket içi veri kaynağı toouse hello ağ geçidi için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cddbc-156">configure hello linked service for hello on-premises data source toouse hello gateway.</span></span>

<span data-ttu-id="cddbc-157">Veri Yönetimi ağ geçidi Hello serileştirir ve burada barındırılan hello bilgisayardaki hello kaynak ve havuz verileri seri durumdan çıkarır.</span><span class="sxs-lookup"><span data-stu-id="cddbc-157">hello Data Management Gateway serializes and deserializes hello source and sink data on hello computer where it is hosted.</span></span>

<span data-ttu-id="cddbc-158">Kurulum yönergeleri ve veri yönetimi ağ geçidi hakkında ayrıntılar için bkz: [şirket içi kaynakları ve veri yönetimi ağ geçidi ile bulut arasında veri taşıma](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="cddbc-158">For set-up instructions and details on Data Management Gateway, see [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span></span>

## <span data-ttu-id="cddbc-159"><a name="adflinkedservices"></a>Bağlı hizmetler tooconnect toohello veri kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="cddbc-159"><a name="adflinkedservices"></a>Create linked services tooconnect toohello data resources</span></span>
<span data-ttu-id="cddbc-160">Bağlı hizmet Azure Data Factory tooconnect tooa veri kaynağı için gerekli hello bilgilerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="cddbc-160">A linked service defines hello information needed for Azure Data Factory tooconnect tooa data resource.</span></span> <span data-ttu-id="cddbc-161">bağlı hizmetler oluşturmak için adım adım yordam hello sağlanır [bağlı hizmetler oluşturma](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span><span class="sxs-lookup"><span data-stu-id="cddbc-161">hello step-by-step procedure for creating linked services is provided in [Create linked services](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span></span>

<span data-ttu-id="cddbc-162">Bağlı hizmetler gerekli olan bu senaryoda üç kaynakları sahibiz.</span><span class="sxs-lookup"><span data-stu-id="cddbc-162">We have three resources in this scenario for which linked services are needed.</span></span>

1. [<span data-ttu-id="cddbc-163">Şirket içi SQL Server için bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="cddbc-163">Linked service for on-premises SQL Server</span></span>](#adf-linked-service-onprem-sql)
2. [<span data-ttu-id="cddbc-164">Azure Blob Storage için bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="cddbc-164">Linked service for Azure Blob Storage</span></span>](#adf-linked-service-blob-store)
3. [<span data-ttu-id="cddbc-165">Azure SQL database için bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="cddbc-165">Linked service for Azure SQL database</span></span>](#adf-linked-service-azure-sql)

### <span data-ttu-id="cddbc-166"><a name="adf-linked-service-onprem-sql"></a>Şirket içi SQL Server database için bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="cddbc-166"><a name="adf-linked-service-onprem-sql"></a>Linked service for on-premises SQL Server database</span></span>
<span data-ttu-id="cddbc-167">toocreate hello bağlantılı hizmeti hello için SQL Server içi:</span><span class="sxs-lookup"><span data-stu-id="cddbc-167">toocreate hello linked service for hello on-premises SQL Server:</span></span>

* <span data-ttu-id="cddbc-168">Merhaba tıklatın **veri deposu** hello ADF giriş sayfasında Klasik Azure portalı üzerinde</span><span class="sxs-lookup"><span data-stu-id="cddbc-168">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="cddbc-169">seçin **SQL** ve hello girin *kullanıcıadı* ve *parola* hello SQL Server şirket için kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="cddbc-169">select **SQL** and enter hello *username* and *password* credentials for hello on-premises SQL Server.</span></span> <span data-ttu-id="cddbc-170">Tooenter hello servername olarak gereken bir **tam servername ters eğik çizgi örnek adı (Sunucuadı\örnekadı)**.</span><span class="sxs-lookup"><span data-stu-id="cddbc-170">You need tooenter hello servername as a **fully qualified servername backslash instance name (servername\instancename)**.</span></span> <span data-ttu-id="cddbc-171">Ad hello bağlantılı hizmeti *adfonpremsql*.</span><span class="sxs-lookup"><span data-stu-id="cddbc-171">Name hello linked service *adfonpremsql*.</span></span>

### <span data-ttu-id="cddbc-172"><a name="adf-linked-service-blob-store"></a>Blob için bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="cddbc-172"><a name="adf-linked-service-blob-store"></a>Linked service for Blob</span></span>
<span data-ttu-id="cddbc-173">toocreate hello Azure Blob Storage hesabı için bağlı hizmet hello:</span><span class="sxs-lookup"><span data-stu-id="cddbc-173">toocreate hello linked service for hello Azure Blob Storage account:</span></span>

* <span data-ttu-id="cddbc-174">Merhaba tıklatın **veri deposu** hello ADF giriş sayfasında Klasik Azure portalı üzerinde</span><span class="sxs-lookup"><span data-stu-id="cddbc-174">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="cddbc-175">seçin **Azure depolama hesabı**</span><span class="sxs-lookup"><span data-stu-id="cddbc-175">select **Azure Storage Account**</span></span>
* <span data-ttu-id="cddbc-176">Merhaba, Azure Blob Depolama hesabı anahtarı ve kapsayıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="cddbc-176">enter hello Azure Blob Storage account key and container name.</span></span> <span data-ttu-id="cddbc-177">Bağlantılı hizmet adı hello *adfds*.</span><span class="sxs-lookup"><span data-stu-id="cddbc-177">Name hello Linked Service *adfds*.</span></span>

### <span data-ttu-id="cddbc-178"><a name="adf-linked-service-azure-sql"></a>Azure SQL database için bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="cddbc-178"><a name="adf-linked-service-azure-sql"></a>Linked service for Azure SQL database</span></span>
<span data-ttu-id="cddbc-179">toocreate hello Azure SQL Database için bağlı hizmet hello:</span><span class="sxs-lookup"><span data-stu-id="cddbc-179">toocreate hello linked service for hello Azure SQL Database:</span></span>

* <span data-ttu-id="cddbc-180">Merhaba tıklatın **veri deposu** hello ADF giriş sayfasında Klasik Azure portalı üzerinde</span><span class="sxs-lookup"><span data-stu-id="cddbc-180">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="cddbc-181">seçin **Azure SQL** ve hello girin *kullanıcıadı* ve *parola* hello Azure SQL veritabanı için kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="cddbc-181">select **Azure SQL** and enter hello *username* and *password* credentials for hello Azure SQL Database.</span></span> <span data-ttu-id="cddbc-182">Merhaba *kullanıcıadı* olarak belirtilmelidir  *user@servername* .</span><span class="sxs-lookup"><span data-stu-id="cddbc-182">hello *username* must be specified as *user@servername*.</span></span>   

## <span data-ttu-id="cddbc-183"><a name="adf-tables"></a>Tanımlayın ve tabloları toospecify oluşturun nasıl tooaccess veri kümeleri hello</span><span class="sxs-lookup"><span data-stu-id="cddbc-183"><a name="adf-tables"></a>Define and create tables toospecify how tooaccess hello datasets</span></span>
<span data-ttu-id="cddbc-184">Betik tabanlı yordamları izleyerek hello ile hello yapısı, konumu ve hello DataSet kullanılabilirliği belirtin tablolar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cddbc-184">Create tables that specify hello structure, location, and availability of hello datasets with hello following script-based procedures.</span></span> <span data-ttu-id="cddbc-185">Kullanılan toodefine hello tablolar JSON dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="cddbc-185">JSON files are used toodefine hello tables.</span></span> <span data-ttu-id="cddbc-186">Bu dosyaları hello yapısı hakkında daha fazla bilgi için bkz: [veri kümeleri](../data-factory/data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="cddbc-186">For more information on hello structure of these files, see [Datasets](../data-factory/data-factory-create-datasets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="cddbc-187">Merhaba yürütülecek `Add-AzureAccount` hello yürütmeden önce cmdlet [yeni AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) sağ Azure aboneliği hello cmdlet tooconfirm hello komutu yürütme için seçilen.</span><span class="sxs-lookup"><span data-stu-id="cddbc-187">You should execute hello `Add-AzureAccount` cmdlet before executing hello [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet tooconfirm that hello right Azure subscription is selected for hello command execution.</span></span> <span data-ttu-id="cddbc-188">Bu cmdlet belgeleri için bkz: [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="cddbc-188">For documentation of this cmdlet, see [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span></span>
>
>

<span data-ttu-id="cddbc-189">Merhaba JSON tabanlı tanımları hello tablolardaki adlarından hello kullan:</span><span class="sxs-lookup"><span data-stu-id="cddbc-189">hello JSON-based definitions in hello tables use hello following names:</span></span>

* <span data-ttu-id="cddbc-190">Merhaba **tablo adı** hello şirket içi SQL server, *nyctaxi_data*</span><span class="sxs-lookup"><span data-stu-id="cddbc-190">hello **table name** in hello on-premises SQL server is *nyctaxi_data*</span></span>
* <span data-ttu-id="cddbc-191">Merhaba **kapsayıcı adı** hello Azure Blob Depolama hesabıdır *kapsayıcı adı*</span><span class="sxs-lookup"><span data-stu-id="cddbc-191">hello **container name** in hello Azure Blob Storage account is *containername*</span></span>  

<span data-ttu-id="cddbc-192">Üç tablo tanımları bu ADF ardışık düzeni için gereklidir:</span><span class="sxs-lookup"><span data-stu-id="cddbc-192">Three table definitions are needed for this ADF pipeline:</span></span>

1. [<span data-ttu-id="cddbc-193">SQL şirket içi tablosu</span><span class="sxs-lookup"><span data-stu-id="cddbc-193">SQL on-premises Table</span></span>](#adf-table-onprem-sql)
2. [<span data-ttu-id="cddbc-194">BLOB tablosu</span><span class="sxs-lookup"><span data-stu-id="cddbc-194">Blob Table </span></span>](#adf-table-blob-store)
3. [<span data-ttu-id="cddbc-195">SQL Azure tablo</span><span class="sxs-lookup"><span data-stu-id="cddbc-195">SQL Azure Table</span></span>](#adf-table-azure-sql)

> [!NOTE]
> <span data-ttu-id="cddbc-196">Bu yordamları Azure PowerShell toodefine kullanın ve ADF etkinlikleri hello oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cddbc-196">These procedures use Azure PowerShell toodefine and create hello ADF activities.</span></span> <span data-ttu-id="cddbc-197">Ancak bu görevleri hello Azure portalı kullanılarak da gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="cddbc-197">But these tasks can also be accomplished using hello Azure portal.</span></span> <span data-ttu-id="cddbc-198">Ayrıntılar için bkz [veri kümeleri oluşturma](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span><span class="sxs-lookup"><span data-stu-id="cddbc-198">For details, see [Create datasets](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span></span>
>
>

### <span data-ttu-id="cddbc-199"><a name="adf-table-onprem-sql"></a>SQL şirket içi tablosu</span><span class="sxs-lookup"><span data-stu-id="cddbc-199"><a name="adf-table-onprem-sql"></a>SQL on-premises Table</span></span>
<span data-ttu-id="cddbc-200">Merhaba tablo tanımı hello için SQL Server aşağıdaki JSON dosyasına hello belirtilen şirket içi:</span><span class="sxs-lookup"><span data-stu-id="cddbc-200">hello table definition for hello on-premises SQL Server is specified in hello following JSON file:</span></span>

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

<span data-ttu-id="cddbc-201">Merhaba sütun adları buraya dahil değil.</span><span class="sxs-lookup"><span data-stu-id="cddbc-201">hello column names were not included here.</span></span> <span data-ttu-id="cddbc-202">Merhaba sütun adlarına göre burada ekleyerek alt seçebilirsiniz (Merhaba ayrıntıları denetlemek için [ADF belgelerine](../data-factory/data-factory-data-movement-activities.md) konu.</span><span class="sxs-lookup"><span data-stu-id="cddbc-202">You can sub-select on hello column names by including them here (for details check hello [ADF documentation](../data-factory/data-factory-data-movement-activities.md) topic.</span></span>

<span data-ttu-id="cddbc-203">Merhaba JSON tanımını Merhaba tablonun adlı bir dosyaya kopyalama *onpremtabledef.json* dosya ve konum bilinen tooa kaydedin (burada toobe kabul *C:\temp\onpremtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="cddbc-203">Copy hello JSON definition of hello table into a file called *onpremtabledef.json* file and save it tooa known location (here assumed toobe *C:\temp\onpremtabledef.json*).</span></span> <span data-ttu-id="cddbc-204">Merhaba tablo içinde ADF ile Azure PowerShell cmdlet'i aşağıdaki hello oluşturun:</span><span class="sxs-lookup"><span data-stu-id="cddbc-204">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <span data-ttu-id="cddbc-205"><a name="adf-table-blob-store"></a>BLOB tablosu</span><span class="sxs-lookup"><span data-stu-id="cddbc-205"><a name="adf-table-blob-store"></a>Blob Table</span></span>
<span data-ttu-id="cddbc-206">(Şirket içi tooAzure blob hello alınan verileri eşler) hello aşağıdaki blob konumdur tanımı hello tablosu hello için çıktı:</span><span class="sxs-lookup"><span data-stu-id="cddbc-206">Definition for hello table for hello output blob location is in hello following (this maps hello ingested data from on-premises tooAzure blob):</span></span>

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

<span data-ttu-id="cddbc-207">Merhaba JSON tanımını Merhaba tablonun adlı bir dosyaya kopyalama *bloboutputtabledef.json* dosya ve konum bilinen tooa kaydedin (burada toobe kabul *C:\temp\bloboutputtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="cddbc-207">Copy hello JSON definition of hello table into a file called *bloboutputtabledef.json* file and save it tooa known location (here assumed toobe *C:\temp\bloboutputtabledef.json*).</span></span> <span data-ttu-id="cddbc-208">Merhaba tablo içinde ADF ile Azure PowerShell cmdlet'i aşağıdaki hello oluşturun:</span><span class="sxs-lookup"><span data-stu-id="cddbc-208">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <span data-ttu-id="cddbc-209"><a name="adf-table-azure-sq"></a>SQL Azure tablo</span><span class="sxs-lookup"><span data-stu-id="cddbc-209"><a name="adf-table-azure-sq"></a>SQL Azure Table</span></span>
<span data-ttu-id="cddbc-210">Merhaba tablosu hello SQL Azure çıkışı için (Bu şemayı hello blobundan gelen hello veri eşlemeleri) hello aşağıdaki tanımıdır:</span><span class="sxs-lookup"><span data-stu-id="cddbc-210">Definition for hello table for hello SQL Azure output is in hello following (this schema maps hello data coming from hello blob):</span></span>

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

<span data-ttu-id="cddbc-211">Merhaba JSON tanımını Merhaba tablonun adlı bir dosyaya kopyalama *AzureSqlTable.json* dosya ve konum bilinen tooa kaydedin (burada toobe kabul *C:\temp\AzureSqlTable.json*).</span><span class="sxs-lookup"><span data-stu-id="cddbc-211">Copy hello JSON definition of hello table into a file called *AzureSqlTable.json* file and save it tooa known location (here assumed toobe *C:\temp\AzureSqlTable.json*).</span></span> <span data-ttu-id="cddbc-212">Merhaba tablo içinde ADF ile Azure PowerShell cmdlet'i aşağıdaki hello oluşturun:</span><span class="sxs-lookup"><span data-stu-id="cddbc-212">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <span data-ttu-id="cddbc-213"><a name="adf-pipeline"></a>Tanımlama ve hello işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cddbc-213"><a name="adf-pipeline"></a>Define and create hello pipeline</span></span>
<span data-ttu-id="cddbc-214">Toohello ait hello etkinlikleri kanal ve aşağıdaki komut dosyası tabanlı yordamlarını hello ile Merhaba işlem hattı oluşturma belirtin.</span><span class="sxs-lookup"><span data-stu-id="cddbc-214">Specify hello activities that belong toohello pipeline and create hello pipeline with hello following script-based procedures.</span></span> <span data-ttu-id="cddbc-215">Kullanılan toodefine hello ardışık düzen özellikleri bir JSON dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="cddbc-215">A JSON file is used toodefine hello pipeline properties.</span></span>

* <span data-ttu-id="cddbc-216">Merhaba betik varsayar bu hello **ardışık düzen adı** olan *AMLDSProcessPipeline*.</span><span class="sxs-lookup"><span data-stu-id="cddbc-216">hello script assumes that hello **pipeline name** is *AMLDSProcessPipeline*.</span></span>
* <span data-ttu-id="cddbc-217">Ayrıca, günlük olarak ve kullanım hello varsayılan yürütme süresi hello işi (00: 00 UTC) yürütülen hello ardışık düzen toobe hello periyodikliğini ayarlarız unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cddbc-217">Also note that we set hello periodicity of hello pipeline toobe executed on daily basis and use hello default execution time for hello job (12 am UTC).</span></span>

> [!NOTE]
> <span data-ttu-id="cddbc-218">Merhaba aşağıdaki yordamları Azure PowerShell toodefine kullanın ve hello ADF işlem hattını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cddbc-218">hello following procedures use Azure PowerShell toodefine and create hello ADF pipeline.</span></span> <span data-ttu-id="cddbc-219">Ancak, bu görevi Azure Portalı'nı kullanarak da gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="cddbc-219">But this task can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="cddbc-220">Ayrıntılar için bkz [oluşturma ardışık düzen](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span><span class="sxs-lookup"><span data-stu-id="cddbc-220">For details, see [Create pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span></span>
>
>

<span data-ttu-id="cddbc-221">Merhaba tablo tanımları kullanarak hello ardışık düzen tanımı ADF gibi belirtilir hello için daha önce sağlanan:</span><span class="sxs-lookup"><span data-stu-id="cddbc-221">Using hello table definitions provided previously, hello pipeline definition for hello ADF is specified as follows:</span></span>

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL tooAzure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server tooblob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data tooSql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

<span data-ttu-id="cddbc-222">Bu JSON tanımını hello ardışık olarak adlandırılan bir dosyaya kopyalayın *pipelinedef.json* dosya ve konum bilinen tooa kaydedin (burada toobe kabul *C:\temp\pipelinedef.json*).</span><span class="sxs-lookup"><span data-stu-id="cddbc-222">Copy this JSON definition of hello pipeline into a file called *pipelinedef.json* file and save it tooa known location (here assumed toobe *C:\temp\pipelinedef.json*).</span></span> <span data-ttu-id="cddbc-223">Merhaba ardışık düzen içinde ADF ile Azure PowerShell cmdlet'i aşağıdaki hello oluşturun:</span><span class="sxs-lookup"><span data-stu-id="cddbc-223">Create hello pipeline in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

<span data-ttu-id="cddbc-224">(Merhaba diyagramı tıklattığınızda) hello ardışık düzen ADF hello Klasik Azure Portalı'nda gösterilmesi hello üzerinde aşağıdaki gibi gördüğünüzden onaylayın</span><span class="sxs-lookup"><span data-stu-id="cddbc-224">Confirm that you can see hello pipeline on hello ADF in hello Azure Classic Portal show up as following (when you click hello diagram)</span></span>

![ADF ardışık düzen](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <span data-ttu-id="cddbc-226"><a name="adf-pipeline-start"></a>Merhaba ardışık düzen Başlat</span><span class="sxs-lookup"><span data-stu-id="cddbc-226"><a name="adf-pipeline-start"></a>Start hello Pipeline</span></span>
<span data-ttu-id="cddbc-227">Merhaba ardışık düzen komutu aşağıdaki hello kullanarak şimdi çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cddbc-227">hello pipeline can now be run using hello following command:</span></span>

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

<span data-ttu-id="cddbc-228">Merhaba *startdate* ve *enddate* parametre değerlerini hello ardışık düzen toorun arasında istediğiniz hello gerçek tarihlerle yerini toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="cddbc-228">hello *startdate* and *enddate* parameter values need toobe replaced with hello actual dates between which you want hello pipeline toorun.</span></span>

<span data-ttu-id="cddbc-229">Merhaba ardışık düzen yürütür sonra Itanium tabanlı sistemler için mümkün toosee hello veri Göster yukarı hello blob, günde bir dosya için seçtiğiniz hello kapsayıcıda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cddbc-229">Once hello pipeline executes, you should be able toosee hello data show up in hello container selected for hello blob, one file per day.</span></span>

<span data-ttu-id="cddbc-230">Biz ADF toopipe verilerle artımlı olarak sağlanan hello işlevselliği işlevden olmayan olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cddbc-230">Note that we have not leveraged hello functionality provided by ADF toopipe data incrementally.</span></span> <span data-ttu-id="cddbc-231">Bu ve diğer özellikleri ADF tarafından sağlanan toodo nasıl görürüm hakkında daha fazla bilgi için hello [ADF belgelerine](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="cddbc-231">For more information on how toodo this and other capabilities provided by ADF, see hello [ADF documentation](https://azure.microsoft.com/services/data-factory/).</span></span>
