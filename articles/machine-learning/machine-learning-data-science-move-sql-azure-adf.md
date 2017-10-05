---
title: "Azure Data Factory ile SQL Azure için bir şirket içi SQL Server'dan veri taşıma | Microsoft Docs"
description: "Bulutta içi veritabanları arasında verileri günlük olarak birlikte taşımak iki veri taşıma etkinlikleri oluşturur bir ADF ardışık ayarlayın."
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
ms.openlocfilehash: 39fe26d3388be8b558f05063a8965889c013a41e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-from-an-on-premises-sql-server-to-sql-azure-with-azure-data-factory"></a><span data-ttu-id="2bbff-103">Azure Data Factory ile SQL Azure için bir şirket içi SQL Server'dan veri taşıma</span><span class="sxs-lookup"><span data-stu-id="2bbff-103">Move data from an on-premises SQL server to SQL Azure with Azure Data Factory</span></span>
<span data-ttu-id="2bbff-104">Bu konu, Azure veri fabrikası (ADF) kullanarak verileri bir şirket içi SQL Server veritabanından bir SQL Azure veritabanına Azure Blob Storage nasıl taşınacağı gösterir.</span><span class="sxs-lookup"><span data-stu-id="2bbff-104">This topic shows how to move data from an on-premises SQL Server Database to a SQL Azure Database via Azure Blob Storage using the Azure Data Factory (ADF).</span></span>

<span data-ttu-id="2bbff-105">Bir Azure SQL veritabanına veri taşıma için çeşitli seçenekler özetler bir tablo için bkz: [veri taşıma bir Azure SQL veritabanına Azure Machine Learning için](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="2bbff-105">For a table that summarizes various options for moving data to an Azure SQL Database, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

## <span data-ttu-id="2bbff-106"><a name="intro"></a>Giriş: ADF nedir ve ne zaman, verileri geçirmek için kullanılmalı?</span><span class="sxs-lookup"><span data-stu-id="2bbff-106"><a name="intro"></a>Introduction: What is ADF and when should it be used to migrate data?</span></span>
<span data-ttu-id="2bbff-107">Azure Data Factory düzenler ve taşınmasını ve dönüştürülmesini veri otomatikleştiren bir bulut tabanlı tam olarak yönetilen bir veri tümleştirme hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="2bbff-107">Azure Data Factory is a fully managed cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="2bbff-108">Anahtar ADF modelinde ardışık düzen kavramdır.</span><span class="sxs-lookup"><span data-stu-id="2bbff-108">The key concept in the ADF model is pipeline.</span></span> <span data-ttu-id="2bbff-109">Bir işlem hattı her biri veri kümelerinde bulunan veriler üzerinde gerçekleştirilecek eylemleri tanımlar mantıksal etkinlikleri grubudur.</span><span class="sxs-lookup"><span data-stu-id="2bbff-109">A pipeline is a logical grouping of Activities, each of which defines the actions to perform on the data contained in Datasets.</span></span> <span data-ttu-id="2bbff-110">Bağlı hizmetler, veri fabrikası'nın veri kaynaklarına bağlanmak için gereken bilgileri tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2bbff-110">Linked services are used to define the information needed for Data Factory to connect to the data resources.</span></span>

<span data-ttu-id="2bbff-111">ADF ile mevcut veri işleme hizmetlerini bulutta yüksek oranda kullanılabilir ve yönetilen veri ardışık içine birleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="2bbff-111">With ADF, existing data processing services can be composed into data pipelines that are highly available and managed in the cloud.</span></span> <span data-ttu-id="2bbff-112">Bu veri ardışık alma, hazırlamak, dönüştürmek, analiz ve veri yayımlamak için zamanlanabilir ve ADF yönetir ve karmaşık veri ve işleme bağımlılıkları yönetir.</span><span class="sxs-lookup"><span data-stu-id="2bbff-112">These data pipelines can be scheduled to ingest, prepare, transform, analyze, and publish data, and ADF manages and orchestrates the complex data and processing dependencies.</span></span> <span data-ttu-id="2bbff-113">Çözümleri hızlı bir şekilde oluşturulur ve şirket içi artan sayıda bağlanma buluta dağıtılan ve bulut veri kaynakları.</span><span class="sxs-lookup"><span data-stu-id="2bbff-113">Solutions can be quickly built and deployed in the cloud, connecting a growing number of on-premises and cloud data sources.</span></span>

<span data-ttu-id="2bbff-114">ADF kullanmayı dikkate alın:</span><span class="sxs-lookup"><span data-stu-id="2bbff-114">Consider using ADF:</span></span>

* <span data-ttu-id="2bbff-115">sürekli olarak geçirilecek verilere ihtiyaç duyduğunda her ikisi de erişen karma bir senaryoda şirket içi ve bulut kaynakları</span><span class="sxs-lookup"><span data-stu-id="2bbff-115">when data needs to be continually migrated in a hybrid scenario that accesses both on-premises and cloud resources</span></span>
* <span data-ttu-id="2bbff-116">ne zaman veri işlem yapılan işlem veya değiştirilmiş veya iş mantığı kendisine geçirilen zaman eklenmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2bbff-116">when the data is transacted or needs to be modified or have business logic added to it when being migrated.</span></span>

<span data-ttu-id="2bbff-117">ADF zamanlama ve işleri düzenli aralıklarla veri hareketini yönetmek basit JSON komut dosyaları kullanarak izlenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="2bbff-117">ADF allows for the scheduling and monitoring of jobs using simple JSON scripts that manage the movement of data on a periodic basis.</span></span> <span data-ttu-id="2bbff-118">ADF karmaşık işlemleri için destek gibi diğer özellikleri de vardır.</span><span class="sxs-lookup"><span data-stu-id="2bbff-118">ADF also has other capabilities such as support for complex operations.</span></span> <span data-ttu-id="2bbff-119">Adresindeki ADF hakkında daha fazla bilgi için bkz: [Azure veri fabrikası (ADF)](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="2bbff-119">For more information on ADF, see the documentation at [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span></span>

## <span data-ttu-id="2bbff-120"><a name="scenario"></a>Senaryo</span><span class="sxs-lookup"><span data-stu-id="2bbff-120"><a name="scenario"></a>The Scenario</span></span>
<span data-ttu-id="2bbff-121">İki veri taşıma etkinlikleri oluşturur bir ADF ardışık ayarlarız.</span><span class="sxs-lookup"><span data-stu-id="2bbff-121">We set up an ADF pipeline that composes two data migration activities.</span></span> <span data-ttu-id="2bbff-122">Birlikte bunlar verileri günlük olarak bir şirket içi SQL database ve Azure SQL Database'i bulutta arasında taşıyın.</span><span class="sxs-lookup"><span data-stu-id="2bbff-122">Together they move data on a daily basis between an on-premises SQL database and an Azure SQL Database in the cloud.</span></span> <span data-ttu-id="2bbff-123">İki etkinlik şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2bbff-123">The two activities are:</span></span>

* <span data-ttu-id="2bbff-124">bir Azure Blob Storage hesabı için bir şirket içi SQL Server veritabanından veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="2bbff-124">copy data from an on-premises SQL Server database to an Azure Blob Storage account</span></span>
* <span data-ttu-id="2bbff-125">verileri Azure Blob Depolama hesabından bir Azure SQL veritabanına kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="2bbff-125">copy data from the Azure Blob Storage account to an Azure SQL Database.</span></span>

> [!NOTE]
> <span data-ttu-id="2bbff-126">Burada olmuştur ADF ekibi tarafından sağlanan daha ayrıntılı öğreticiden uyarlanmış gösterilen adımlar: [şirket içi kaynakları ve veri yönetimi ağ geçidi ile bulut arasında veri taşıma](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) uygun olduğunda bu konusunun ilgili bölümlerine başvurular sağlanır.</span><span class="sxs-lookup"><span data-stu-id="2bbff-126">The steps shown here have been adapted from the more detailed tutorial provided by the ADF team: [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) References to the relevant sections of that topic are provided when appropriate.</span></span>
>
>

## <span data-ttu-id="2bbff-127"><a name="prereqs"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="2bbff-127"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="2bbff-128">Bu öğretici, sahip olduğunuz varsayılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="2bbff-128">This tutorial assumes you have:</span></span>

* <span data-ttu-id="2bbff-129">Bir **Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="2bbff-129">An **Azure subscription**.</span></span> <span data-ttu-id="2bbff-130">Bir aboneliğiniz yoksa [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2bbff-130">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2bbff-131">Bir **Azure depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="2bbff-131">An **Azure storage account**.</span></span> <span data-ttu-id="2bbff-132">Bu öğreticide verileri depolamak için bir Azure depolama hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2bbff-132">You use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="2bbff-133">Azure depolama hesabınız yoksa [Depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="2bbff-133">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="2bbff-134">Depolama hesabını oluşturduktan sonra, depolamaya erişmek için kullanılan hesap anahtarını edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2bbff-134">After you have created the storage account, you need to obtain the account key used to access the storage.</span></span> <span data-ttu-id="2bbff-135">Bkz: [depolama erişim tuşlarınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="2bbff-135">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="2bbff-136">Erişim bir **Azure SQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="2bbff-136">Access to an **Azure SQL Database**.</span></span> <span data-ttu-id="2bbff-137">Bir Azure SQL veritabanı, tpoic ayarlanması, [Microsoft Azure SQL veritabanı ile çalışmaya başlama ](../sql-database/sql-database-get-started.md) bir Azure SQL veritabanına yeni bir örneğini sağlayacak bilgiler verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="2bbff-137">If you must set up an Azure SQL Database, the tpoic [Getting Started with Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) provides information on how to provision a new instance of an Azure SQL Database.</span></span>
* <span data-ttu-id="2bbff-138">Yüklenmiş ve yapılandırılmış **Azure PowerShell** yerel olarak.</span><span class="sxs-lookup"><span data-stu-id="2bbff-138">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="2bbff-139">Yönergeler için bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2bbff-139">For instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!NOTE]
> <span data-ttu-id="2bbff-140">Bu yordamı kullanır [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2bbff-140">This procedure uses the [Azure portal](https://portal.azure.com/).</span></span>
>
>

## <span data-ttu-id="2bbff-141"><a name="upload-data"></a>Şirket içi SQL Server'ınızı veri yükleme</span><span class="sxs-lookup"><span data-stu-id="2bbff-141"><a name="upload-data"></a> Upload the data to your on-premises SQL Server</span></span>
<span data-ttu-id="2bbff-142">Kullanırız [NYC ücreti dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) geçiş işlemini göstermek için.</span><span class="sxs-lookup"><span data-stu-id="2bbff-142">We use the [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) to demonstrate the migration process.</span></span> <span data-ttu-id="2bbff-143">NYC ücreti dataset Azure blob depolama o post belirtildiği gibi kullanılabilir [NYC ücreti verileri](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="2bbff-143">The NYC Taxi dataset is available, as noted in that post, on Azure blob storage [NYC Taxi Data](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="2bbff-144">Verileri iki dosya, seyahat ayrıntılarını içeren, trip_data.csv dosya ve her seyahat için ödenen ücreti ayrıntılarını içeren trip_far.csv dosyası vardır.</span><span class="sxs-lookup"><span data-stu-id="2bbff-144">The data has two files, the trip_data.csv file, which contains trip details, and the  trip_far.csv file, which contains details of the fare paid for each trip.</span></span> <span data-ttu-id="2bbff-145">Bir örnek ve bu dosyaların açıklaması sağlanan [NYC ücreti dönüşleri veri kümesi tanımı](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span><span class="sxs-lookup"><span data-stu-id="2bbff-145">A sample and description of these files are provided in [NYC Taxi Trips Dataset Description](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span></span>

<span data-ttu-id="2bbff-146">Burada, kendi veri kümesi için sağlanan yordamı uyarlamak veya NYC ücreti dataset kullanarak açıklanan adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="2bbff-146">You can either adapt the procedure provided here to a set of your own data or follow the steps as described by using the NYC Taxi dataset.</span></span> <span data-ttu-id="2bbff-147">NYC ücreti veri kümesi şirket içi SQL Server veritabanınıza karşıya yüklemek için özetlenen yordamı izleyin [toplu içeri aktarma verileri SQL Server veritabanına](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span><span class="sxs-lookup"><span data-stu-id="2bbff-147">To upload the NYC Taxi dataset into your on-premises SQL Server database, follow the procedure outlined in [Bulk Import Data into SQL Server Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span></span> <span data-ttu-id="2bbff-148">SQL Server üzerinde bir Azure sanal makine için bu yönergeleri bağlıdır, ancak şirket içi SQL Server'a yükleme yordamı aynıdır.</span><span class="sxs-lookup"><span data-stu-id="2bbff-148">These instructions are for a SQL Server on an Azure Virtual Machine, but the procedure for uploading to the on-premises SQL Server is the same.</span></span>

## <span data-ttu-id="2bbff-149"><a name="create-adf"></a>Bir Azure Data Factory oluşturma</span><span class="sxs-lookup"><span data-stu-id="2bbff-149"><a name="create-adf"></a> Create an Azure Data Factory</span></span>
<span data-ttu-id="2bbff-150">Yeni bir Azure Data Factory ve bir kaynak grubu oluşturmak için yönergeleri [Azure portal](https://portal.azure.com/) sağlanan [bir Azure Data Factory oluşturmak](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span><span class="sxs-lookup"><span data-stu-id="2bbff-150">The instructions for creating a new Azure Data Factory and a resource group in the [Azure portal](https://portal.azure.com/) are provided [Create an Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span></span> <span data-ttu-id="2bbff-151">Yeni ADF örnek adı *adfdsp* ve oluşturulan kaynak grubu adı *adfdsprg*.</span><span class="sxs-lookup"><span data-stu-id="2bbff-151">Name the new ADF instance *adfdsp* and name the resource group created *adfdsprg*.</span></span>

## <a name="install-and-configure-up-the-data-management-gateway"></a><span data-ttu-id="2bbff-152">Yükleme ve veri yönetimi ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2bbff-152">Install and configure up the Data Management Gateway</span></span>
<span data-ttu-id="2bbff-153">Bir şirket içi SQL Server ile çalışmak için bir Azure data factory'de işlem hatlarınızı etkinleştirmek için bu data factory bağlantılı bir hizmet olarak eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2bbff-153">To enable your pipelines in an Azure data factory to work with an on-premises SQL Server, you need to add it as a Linked Service to the data factory.</span></span> <span data-ttu-id="2bbff-154">Bir şirket içi SQL Server için bağlı hizmet oluşturmak için şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="2bbff-154">To create a Linked Service for an on-premises SQL Server, you must:</span></span>

* <span data-ttu-id="2bbff-155">indirin ve Microsoft Veri Yönetimi ağ geçidi şirket içi bilgisayara yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2bbff-155">download and install Microsoft Data Management Gateway onto the on-premises computer.</span></span>
* <span data-ttu-id="2bbff-156">bağlantılı hizmeti ağ geçidini kullanmak için şirket içi veri kaynağı için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2bbff-156">configure the linked service for the on-premises data source to use the gateway.</span></span>

<span data-ttu-id="2bbff-157">Veri Yönetimi ağ geçidi serileştirir ve burada barındırılan bilgisayar üzerinde kaynak ve havuz verileri seri durumdan çıkarır.</span><span class="sxs-lookup"><span data-stu-id="2bbff-157">The Data Management Gateway serializes and deserializes the source and sink data on the computer where it is hosted.</span></span>

<span data-ttu-id="2bbff-158">Kurulum yönergeleri ve veri yönetimi ağ geçidi hakkında ayrıntılar için bkz: [şirket içi kaynakları ve veri yönetimi ağ geçidi ile bulut arasında veri taşıma](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="2bbff-158">For set-up instructions and details on Data Management Gateway, see [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span></span>

## <span data-ttu-id="2bbff-159"><a name="adflinkedservices"></a>Veri kaynaklarına bağlanmak için bağlı hizmetler oluşturma</span><span class="sxs-lookup"><span data-stu-id="2bbff-159"><a name="adflinkedservices"></a>Create linked services to connect to the data resources</span></span>
<span data-ttu-id="2bbff-160">Bağlı hizmet Azure veri fabrikası'nın bir veri kaynağına bağlanmak için gereken bilgileri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2bbff-160">A linked service defines the information needed for Azure Data Factory to connect to a data resource.</span></span> <span data-ttu-id="2bbff-161">Bağlı hizmetler oluşturmak için adım adım yordam sağlanan [bağlı hizmetler oluşturma](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span><span class="sxs-lookup"><span data-stu-id="2bbff-161">The step-by-step procedure for creating linked services is provided in [Create linked services](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span></span>

<span data-ttu-id="2bbff-162">Bağlı hizmetler gerekli olan bu senaryoda üç kaynakları sahibiz.</span><span class="sxs-lookup"><span data-stu-id="2bbff-162">We have three resources in this scenario for which linked services are needed.</span></span>

1. [<span data-ttu-id="2bbff-163">Şirket içi SQL Server için bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="2bbff-163">Linked service for on-premises SQL Server</span></span>](#adf-linked-service-onprem-sql)
2. [<span data-ttu-id="2bbff-164">Azure Blob Storage için bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="2bbff-164">Linked service for Azure Blob Storage</span></span>](#adf-linked-service-blob-store)
3. [<span data-ttu-id="2bbff-165">Azure SQL database için bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="2bbff-165">Linked service for Azure SQL database</span></span>](#adf-linked-service-azure-sql)

### <span data-ttu-id="2bbff-166"><a name="adf-linked-service-onprem-sql"></a>Şirket içi SQL Server database için bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="2bbff-166"><a name="adf-linked-service-onprem-sql"></a>Linked service for on-premises SQL Server database</span></span>
<span data-ttu-id="2bbff-167">Şirket içi SQL Server için bağlı hizmet oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="2bbff-167">To create the linked service for the on-premises SQL Server:</span></span>

* <span data-ttu-id="2bbff-168">tıklatın **veri deposu** Klasik Azure portalı üzerinde ADF giriş sayfasındaki</span><span class="sxs-lookup"><span data-stu-id="2bbff-168">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="2bbff-169">seçin **SQL** ve girin *kullanıcıadı* ve *parola* şirket içi SQL Server için kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="2bbff-169">select **SQL** and enter the *username* and *password* credentials for the on-premises SQL Server.</span></span> <span data-ttu-id="2bbff-170">Servername olarak girmeniz gereken bir **tam servername ters eğik çizgi örnek adı (Sunucuadı\örnekadı)**.</span><span class="sxs-lookup"><span data-stu-id="2bbff-170">You need to enter the servername as a **fully qualified servername backslash instance name (servername\instancename)**.</span></span> <span data-ttu-id="2bbff-171">Bağlı hizmetin adı *adfonpremsql*.</span><span class="sxs-lookup"><span data-stu-id="2bbff-171">Name the linked service *adfonpremsql*.</span></span>

### <span data-ttu-id="2bbff-172"><a name="adf-linked-service-blob-store"></a>Blob için bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="2bbff-172"><a name="adf-linked-service-blob-store"></a>Linked service for Blob</span></span>
<span data-ttu-id="2bbff-173">Azure Blob Storage hesabı için bağlı hizmet oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="2bbff-173">To create the linked service for the Azure Blob Storage account:</span></span>

* <span data-ttu-id="2bbff-174">tıklatın **veri deposu** Klasik Azure portalı üzerinde ADF giriş sayfasındaki</span><span class="sxs-lookup"><span data-stu-id="2bbff-174">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="2bbff-175">seçin **Azure depolama hesabı**</span><span class="sxs-lookup"><span data-stu-id="2bbff-175">select **Azure Storage Account**</span></span>
* <span data-ttu-id="2bbff-176">Azure Blob Depolama hesabı anahtarı ve kapsayıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="2bbff-176">enter the Azure Blob Storage account key and container name.</span></span> <span data-ttu-id="2bbff-177">Bağlı hizmetin adı *adfds*.</span><span class="sxs-lookup"><span data-stu-id="2bbff-177">Name the Linked Service *adfds*.</span></span>

### <span data-ttu-id="2bbff-178"><a name="adf-linked-service-azure-sql"></a>Azure SQL database için bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="2bbff-178"><a name="adf-linked-service-azure-sql"></a>Linked service for Azure SQL database</span></span>
<span data-ttu-id="2bbff-179">Azure SQL Database için bağlı hizmet oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="2bbff-179">To create the linked service for the Azure SQL Database:</span></span>

* <span data-ttu-id="2bbff-180">tıklatın **veri deposu** Klasik Azure portalı üzerinde ADF giriş sayfasındaki</span><span class="sxs-lookup"><span data-stu-id="2bbff-180">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="2bbff-181">seçin **Azure SQL** ve girin *kullanıcıadı* ve *parola* Azure SQL veritabanı için kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="2bbff-181">select **Azure SQL** and enter the *username* and *password* credentials for the Azure SQL Database.</span></span> <span data-ttu-id="2bbff-182">*Kullanıcıadı* olarak belirtilmelidir  *user@servername* .</span><span class="sxs-lookup"><span data-stu-id="2bbff-182">The *username* must be specified as *user@servername*.</span></span>   

## <span data-ttu-id="2bbff-183"><a name="adf-tables"></a>Tanımlama ve veri kümeleri erişmek nasıl belirlemek için tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="2bbff-183"><a name="adf-tables"></a>Define and create tables to specify how to access the datasets</span></span>
<span data-ttu-id="2bbff-184">Aşağıdaki betik tabanlı yordamları yapısını, konum ve veri kümelerinin kullanılabilirliğini belirtin tablolar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2bbff-184">Create tables that specify the structure, location, and availability of the datasets with the following script-based procedures.</span></span> <span data-ttu-id="2bbff-185">JSON dosyaları tabloları tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2bbff-185">JSON files are used to define the tables.</span></span> <span data-ttu-id="2bbff-186">Bu dosyalar yapısı hakkında daha fazla bilgi için bkz: [veri kümeleri](../data-factory/data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="2bbff-186">For more information on the structure of these files, see [Datasets](../data-factory/data-factory-create-datasets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2bbff-187">Yürütme `Add-AzureAccount` yürütmeden önce cmdlet [yeni AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet'ini sağ Azure aboneliği için komut yürütme seçili olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="2bbff-187">You should execute the `Add-AzureAccount` cmdlet before executing the [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet to confirm that the right Azure subscription is selected for the command execution.</span></span> <span data-ttu-id="2bbff-188">Bu cmdlet belgeleri için bkz: [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="2bbff-188">For documentation of this cmdlet, see [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span></span>
>
>

<span data-ttu-id="2bbff-189">Tablolar JSON tabanlı tanımlarında aşağıdaki adları kullanın:</span><span class="sxs-lookup"><span data-stu-id="2bbff-189">The JSON-based definitions in the tables use the following names:</span></span>

* <span data-ttu-id="2bbff-190">**tablo adı** şirket içi SQL sunucusudur *nyctaxi_data*</span><span class="sxs-lookup"><span data-stu-id="2bbff-190">the **table name** in the on-premises SQL server is *nyctaxi_data*</span></span>
* <span data-ttu-id="2bbff-191">**kapsayıcı adı** Azure Blob Storage'da hesabıdır *kapsayıcı adı*</span><span class="sxs-lookup"><span data-stu-id="2bbff-191">the **container name** in the Azure Blob Storage account is *containername*</span></span>  

<span data-ttu-id="2bbff-192">Üç tablo tanımları bu ADF ardışık düzeni için gereklidir:</span><span class="sxs-lookup"><span data-stu-id="2bbff-192">Three table definitions are needed for this ADF pipeline:</span></span>

1. [<span data-ttu-id="2bbff-193">SQL şirket içi tablosu</span><span class="sxs-lookup"><span data-stu-id="2bbff-193">SQL on-premises Table</span></span>](#adf-table-onprem-sql)
2. [<span data-ttu-id="2bbff-194">BLOB tablosu</span><span class="sxs-lookup"><span data-stu-id="2bbff-194">Blob Table </span></span>](#adf-table-blob-store)
3. [<span data-ttu-id="2bbff-195">SQL Azure tablo</span><span class="sxs-lookup"><span data-stu-id="2bbff-195">SQL Azure Table</span></span>](#adf-table-azure-sql)

> [!NOTE]
> <span data-ttu-id="2bbff-196">Tanımlama ve ADF etkinlikleri oluşturmak için Azure PowerShell Bu yordamları kullanın.</span><span class="sxs-lookup"><span data-stu-id="2bbff-196">These procedures use Azure PowerShell to define and create the ADF activities.</span></span> <span data-ttu-id="2bbff-197">Ancak bu görevleri Azure Portalı'nı kullanarak da gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="2bbff-197">But these tasks can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="2bbff-198">Ayrıntılar için bkz [veri kümeleri oluşturma](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span><span class="sxs-lookup"><span data-stu-id="2bbff-198">For details, see [Create datasets](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span></span>
>
>

### <span data-ttu-id="2bbff-199"><a name="adf-table-onprem-sql"></a>SQL şirket içi tablosu</span><span class="sxs-lookup"><span data-stu-id="2bbff-199"><a name="adf-table-onprem-sql"></a>SQL on-premises Table</span></span>
<span data-ttu-id="2bbff-200">Şirket içi SQL Server için tablo tanımı aşağıdaki JSON dosyasında belirtilir:</span><span class="sxs-lookup"><span data-stu-id="2bbff-200">The table definition for the on-premises SQL Server is specified in the following JSON file:</span></span>

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

<span data-ttu-id="2bbff-201">Sütun adlarını buraya dahil değil.</span><span class="sxs-lookup"><span data-stu-id="2bbff-201">The column names were not included here.</span></span> <span data-ttu-id="2bbff-202">Sütun adları burada ekleyerek alt seçebilirsiniz (Ayrıntılar için denetleyin [ADF belgelerine](../data-factory/data-factory-data-movement-activities.md) konu.</span><span class="sxs-lookup"><span data-stu-id="2bbff-202">You can sub-select on the column names by including them here (for details check the [ADF documentation](../data-factory/data-factory-data-movement-activities.md) topic.</span></span>

<span data-ttu-id="2bbff-203">Tablosunun JSON tanımını bir dosyaya adlı kopya *onpremtabledef.json* dosya ve bilinen bir konuma kaydedin (burada varsayılır *C:\temp\onpremtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="2bbff-203">Copy the JSON definition of the table into a file called *onpremtabledef.json* file and save it to a known location (here assumed to be *C:\temp\onpremtabledef.json*).</span></span> <span data-ttu-id="2bbff-204">Tablo içinde ADF aşağıdaki Azure PowerShell cmdlet'iyle oluşturun:</span><span class="sxs-lookup"><span data-stu-id="2bbff-204">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <span data-ttu-id="2bbff-205"><a name="adf-table-blob-store"></a>BLOB tablosu</span><span class="sxs-lookup"><span data-stu-id="2bbff-205"><a name="adf-table-blob-store"></a>Blob Table</span></span>
<span data-ttu-id="2bbff-206">Tablosu için çıkış blob konumu tanımıdır (Bu eşler şirket içi Azure blob alınan verileri) aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="2bbff-206">Definition for the table for the output blob location is in the following (this maps the ingested data from on-premises to Azure blob):</span></span>

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

<span data-ttu-id="2bbff-207">Tablosunun JSON tanımını bir dosyaya adlı kopya *bloboutputtabledef.json* dosya ve bilinen bir konuma kaydedin (burada varsayılır *C:\temp\bloboutputtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="2bbff-207">Copy the JSON definition of the table into a file called *bloboutputtabledef.json* file and save it to a known location (here assumed to be *C:\temp\bloboutputtabledef.json*).</span></span> <span data-ttu-id="2bbff-208">Tablo içinde ADF aşağıdaki Azure PowerShell cmdlet'iyle oluşturun:</span><span class="sxs-lookup"><span data-stu-id="2bbff-208">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <span data-ttu-id="2bbff-209"><a name="adf-table-azure-sq"></a>SQL Azure tablo</span><span class="sxs-lookup"><span data-stu-id="2bbff-209"><a name="adf-table-azure-sq"></a>SQL Azure Table</span></span>
<span data-ttu-id="2bbff-210">SQL Azure tablo tanımı çıkış (Bu şemayı eşlemeleri blobundan gelen veriler) aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="2bbff-210">Definition for the table for the SQL Azure output is in the following (this schema maps the data coming from the blob):</span></span>

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

<span data-ttu-id="2bbff-211">Tablosunun JSON tanımını bir dosyaya adlı kopya *AzureSqlTable.json* dosya ve bilinen bir konuma kaydedin (burada varsayılır *C:\temp\AzureSqlTable.json*).</span><span class="sxs-lookup"><span data-stu-id="2bbff-211">Copy the JSON definition of the table into a file called *AzureSqlTable.json* file and save it to a known location (here assumed to be *C:\temp\AzureSqlTable.json*).</span></span> <span data-ttu-id="2bbff-212">Tablo içinde ADF aşağıdaki Azure PowerShell cmdlet'iyle oluşturun:</span><span class="sxs-lookup"><span data-stu-id="2bbff-212">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <span data-ttu-id="2bbff-213"><a name="adf-pipeline"></a>Tanımlama ve işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2bbff-213"><a name="adf-pipeline"></a>Define and create the pipeline</span></span>
<span data-ttu-id="2bbff-214">Ardışık düzene ait olan ve aşağıdaki komut dosyası tabanlı yordamları ile işlem hattı oluşturma etkinlikleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="2bbff-214">Specify the activities that belong to the pipeline and create the pipeline with the following script-based procedures.</span></span> <span data-ttu-id="2bbff-215">Bir JSON dosyası ardışık düzen özelliklerini tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2bbff-215">A JSON file is used to define the pipeline properties.</span></span>

* <span data-ttu-id="2bbff-216">Komut dosyası varsayar **ardışık düzen adı** olan *AMLDSProcessPipeline*.</span><span class="sxs-lookup"><span data-stu-id="2bbff-216">The script assumes that the **pipeline name** is *AMLDSProcessPipeline*.</span></span>
* <span data-ttu-id="2bbff-217">Ayrıca, günlük olarak yürütülen ve varsayılan yürütme süresi işi (00: 00 UTC) kullanmak için ardışık düzen periyodikliğini ayarlarız unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2bbff-217">Also note that we set the periodicity of the pipeline to be executed on daily basis and use the default execution time for the job (12 am UTC).</span></span>

> [!NOTE]
> <span data-ttu-id="2bbff-218">Aşağıdaki yordamlar tanımlayın ve ADF ardışık düzen oluşturmak için Azure PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="2bbff-218">The following procedures use Azure PowerShell to define and create the ADF pipeline.</span></span> <span data-ttu-id="2bbff-219">Ancak, bu görevi Azure Portalı'nı kullanarak da gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="2bbff-219">But this task can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="2bbff-220">Ayrıntılar için bkz [oluşturma ardışık düzen](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span><span class="sxs-lookup"><span data-stu-id="2bbff-220">For details, see [Create pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span></span>
>
>

<span data-ttu-id="2bbff-221">Daha önce sağlanan tablo tanımları kullanarak ADF ardışık düzen tanımı gibi belirtilir:</span><span class="sxs-lookup"><span data-stu-id="2bbff-221">Using the table definitions provided previously, the pipeline definition for the ADF is specified as follows:</span></span>

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL to Azure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server to blob",     
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
                        "description": "Push data to Sql Azure",        
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

<span data-ttu-id="2bbff-222">Bu ardışık düzen JSON tanımı dosyasına adlı kopya *pipelinedef.json* dosya ve bilinen bir konuma kaydedin (burada varsayılır *C:\temp\pipelinedef.json*).</span><span class="sxs-lookup"><span data-stu-id="2bbff-222">Copy this JSON definition of the pipeline into a file called *pipelinedef.json* file and save it to a known location (here assumed to be *C:\temp\pipelinedef.json*).</span></span> <span data-ttu-id="2bbff-223">Ardışık Düzen ADF içinde aşağıdaki Azure PowerShell cmdlet'iyle oluşturun:</span><span class="sxs-lookup"><span data-stu-id="2bbff-223">Create the pipeline in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

<span data-ttu-id="2bbff-224">(Diyagram tıklattığınızda) aşağıdaki gibi görünmesini Azure Klasik Portalı'nda ADF ardışık gördüğünüzü onaylayın</span><span class="sxs-lookup"><span data-stu-id="2bbff-224">Confirm that you can see the pipeline on the ADF in the Azure Classic Portal show up as following (when you click the diagram)</span></span>

![ADF ardışık düzen](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <span data-ttu-id="2bbff-226"><a name="adf-pipeline-start"></a>Ardışık Düzen Başlat</span><span class="sxs-lookup"><span data-stu-id="2bbff-226"><a name="adf-pipeline-start"></a>Start the Pipeline</span></span>
<span data-ttu-id="2bbff-227">Ardışık Düzen aşağıdaki komutu kullanarak şimdi çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2bbff-227">The pipeline can now be run using the following command:</span></span>

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

<span data-ttu-id="2bbff-228">*Startdate* ve *enddate* parametre değerlerini çalıştırmak için ardışık düzen arasında istediğiniz gerçek tarihleri ile değiştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2bbff-228">The *startdate* and *enddate* parameter values need to be replaced with the actual dates between which you want the pipeline to run.</span></span>

<span data-ttu-id="2bbff-229">Ardışık Düzen yürütür sonra blob, günde bir dosya için seçilen kapsayıcıdaki görünmesini verileri görmek görebilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2bbff-229">Once the pipeline executes, you should be able to see the data show up in the container selected for the blob, one file per day.</span></span>

<span data-ttu-id="2bbff-230">Biz tarafından ADF kanal veri için artımlı olarak sağlanan işlevselliği işlevden olmayan olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2bbff-230">Note that we have not leveraged the functionality provided by ADF to pipe data incrementally.</span></span> <span data-ttu-id="2bbff-231">Bu ve ADF tarafından sağlanan diğer özellikleri hakkında daha fazla bilgi için bkz: [ADF belgelerine](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="2bbff-231">For more information on how to do this and other capabilities provided by ADF, see the [ADF documentation](https://azure.microsoft.com/services/data-factory/).</span></span>
