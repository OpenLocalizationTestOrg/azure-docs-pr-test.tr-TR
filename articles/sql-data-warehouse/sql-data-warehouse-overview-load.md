---
title: "Azure SQL Data Warehouse'a veri yükleme | Microsoft Docs"
description: "Veri SQL Data Warehouse'a veri yükleme için genel senaryolar hakkında bilgi edinin. Bunlar PolyBase, Azure blob depolama, düz dosyalar ve disk sevkiyat kullanarak içerir. Üçüncü taraf araçları da kullanabilirsiniz."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: c4199a387f5cdbd477a5e348e48ba8e8b5900075
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="12d00-105">Azure SQL Data Warehouse'a veri yükleme</span><span class="sxs-lookup"><span data-stu-id="12d00-105">Load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="12d00-106">Senaryo seçenekleri ve SQL Data Warehouse'a veri yükleme ile ilgili öneriler özeti.</span><span class="sxs-lookup"><span data-stu-id="12d00-106">A summary of the scenario options and recommendations for loading data into SQL Data Warehouse.</span></span>

<span data-ttu-id="12d00-107">Verileri yükleme en zor parçası genellikle verileri için yük hazırlanıyor.</span><span class="sxs-lookup"><span data-stu-id="12d00-107">The hardest part of loading data is usually preparing the data for the load.</span></span> <span data-ttu-id="12d00-108">Azure basitleştirir yükleme ortak bir veri deposu olarak birçok Hizmetleri için Azure blob storage kullanarak ve Azure hizmetleri arasında iletişim ve veri taşıma düzenlemek için Azure Data Factory kullanarak.</span><span class="sxs-lookup"><span data-stu-id="12d00-108">Azure simplifies loading by using Azure blob storage as a common data store for many of the services, and using Azure Data Factory to orchestrate communication and data movement between the Azure services.</span></span> <span data-ttu-id="12d00-109">Bu işlemler, verileri paralel verileri Azure blob depolama alanından SQL Data Warehouse'a veri yüklemek için yüksek düzeyde paralel işleme (MPP) kullanan PolyBase teknolojisi ile tümleştirilir.</span><span class="sxs-lookup"><span data-stu-id="12d00-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) to load data in parallel from Azure blob storage into SQL Data Warehouse.</span></span> 

<span data-ttu-id="12d00-110">Örnek veritabanları yükleme öğreticileri için bkz: [örnek veritabanları yükleme][Load sample databases].</span><span class="sxs-lookup"><span data-stu-id="12d00-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span></span>

## <a name="load-from-azure-blob-storage"></a><span data-ttu-id="12d00-111">Azure blob depolama alanından yükleme</span><span class="sxs-lookup"><span data-stu-id="12d00-111">Load from Azure blob storage</span></span>
<span data-ttu-id="12d00-112">SQL Data Warehouse'a veri almak için en hızlı yolu, Azure blob depolama alanından verileri yüklemek için PolyBase kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="12d00-112">The fastest way to import data into SQL Data Warehouse is to use PolyBase to load data from Azure blob storage.</span></span> <span data-ttu-id="12d00-113">PolyBase, Azure blob depolama alanından verileri paralel yüklemek için SQL Data Warehouse'un yüksek düzeyde paralel işleme (MPP) tasarım kullanır.</span><span class="sxs-lookup"><span data-stu-id="12d00-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design to load data in parallel from Azure blob storage.</span></span> <span data-ttu-id="12d00-114">PolyBase kullanmak için T-SQL komutlarıyla veya bir Azure Data Factory işlem hattı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12d00-114">To use PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span></span>

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="12d00-115">1. PolyBase ve T-SQL kullanın</span><span class="sxs-lookup"><span data-stu-id="12d00-115">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="12d00-116">Yükleme işlemi özeti:</span><span class="sxs-lookup"><span data-stu-id="12d00-116">Summary of loading process:</span></span>

1. <span data-ttu-id="12d00-117">Verileriniz Azure blob depolama veya Azure Data Lake Store taşıyın ve metin dosyalarında saklayın.</span><span class="sxs-lookup"><span data-stu-id="12d00-117">Move your data to Azure blob storage or Azure Data Lake Store and store it in text files.</span></span>
2. <span data-ttu-id="12d00-118">Veri biçimi ve konumunu tanımlamak için SQL veri ambarında dış nesneleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="12d00-118">Configure external objects in SQL Data Warehouse to define the location and format of the data</span></span>
3. <span data-ttu-id="12d00-119">Yeni bir veritabanı tablosuna paralel veri yüklemek için bir T-SQL komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="12d00-119">Run a T-SQL command to load the data in parallel into a new database table.</span></span>

<!-- 5. Schedule and run a loading job. --> 

<span data-ttu-id="12d00-120">Bir öğretici için bkz: [veri yükleme Azure blob depolama alanından SQL Data Warehouse'a (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="12d00-120">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

### <a name="2-use-azure-data-factory"></a><span data-ttu-id="12d00-121">2. Azure Data Factory'i kullanma</span><span class="sxs-lookup"><span data-stu-id="12d00-121">2. Use Azure Data Factory</span></span>
<span data-ttu-id="12d00-122">PolyBase kullanmak için daha basit yol için verileri Azure blob depolama alanından SQL Data Warehouse'a veri yüklemek için PolyBase kullanan bir Azure Data Factory işlem hattı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12d00-122">For a simpler way to use PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase to load data from Azure blob storage into SQL Data Warehouse.</span></span> <span data-ttu-id="12d00-123">T-SQL nesneleri tanımlamak gerekmeyen beri yapılandırmak için hızlı budur.</span><span class="sxs-lookup"><span data-stu-id="12d00-123">This is fast to configure since you don't need to define the T-SQL objects.</span></span> <span data-ttu-id="12d00-124">Dış veri içe aktarmadan sorgu gerekiyorsa, T-SQL kullanın.</span><span class="sxs-lookup"><span data-stu-id="12d00-124">If you need to query the external data without importing it, use T-SQL.</span></span> 

<span data-ttu-id="12d00-125">Yükleme işlemi özeti:</span><span class="sxs-lookup"><span data-stu-id="12d00-125">Summary of loading process:</span></span>

1. <span data-ttu-id="12d00-126">Verilerinizi Azure blob depolama alanına taşıma ve metin dosyalarında saklayın.</span><span class="sxs-lookup"><span data-stu-id="12d00-126">Move your data to Azure blob storage and store it in text files.</span></span> <span data-ttu-id="12d00-127">Azure Data Factory şu anda PolyBase ile ADLS bağlantısı desteklemez).</span><span class="sxs-lookup"><span data-stu-id="12d00-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span></span>
2. <span data-ttu-id="12d00-128">Veri alma için bir Azure Data Factory işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="12d00-128">Create an Azure Data Factory pipeline to ingest the data.</span></span> <span data-ttu-id="12d00-129">PolyBase seçeneğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="12d00-129">Use the PolyBase option.</span></span>
4. <span data-ttu-id="12d00-130">Zamanlama ve ardışık düzen çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="12d00-130">Schedule and run the pipeline.</span></span>

<span data-ttu-id="12d00-131">Bir öğretici için bkz: [veri yükleme Azure blob depolama alanından SQL Data Warehouse'a (Azure Data Factory)][Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)].</span><span class="sxs-lookup"><span data-stu-id="12d00-131">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)].</span></span>

## <a name="load-from-sql-server"></a><span data-ttu-id="12d00-132">SQL Server'dan yükleme</span><span class="sxs-lookup"><span data-stu-id="12d00-132">Load from SQL Server</span></span>
<span data-ttu-id="12d00-133">SQL Server'dan SQL Data Warehouse'a veri yüklemek için Integration Services (SSIS), aktarım düz dosyalar veya Microsoft sevk disk kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12d00-133">To load data from SQL Server to SQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks to Microsoft.</span></span> <span data-ttu-id="12d00-134">Bkz: farklı özetini açın okuma işlemleri ve öğreticiler bağlantılar yükleniyor.</span><span class="sxs-lookup"><span data-stu-id="12d00-134">Read on to see a summary of the different loading processes and links to tutorials.</span></span>

<span data-ttu-id="12d00-135">SQL veri ambarı SQL Server'dan tam veri geçiş planlamak için bkz: [geçişine genel bakış][Migration overview].</span><span class="sxs-lookup"><span data-stu-id="12d00-135">To plan a full data migration from SQL Server to SQL Data Warehouse, see the [Migration overview][Migration overview].</span></span> 

### <a name="use-integration-services-ssis"></a><span data-ttu-id="12d00-136">Integration Services (SSIS) kullanın</span><span class="sxs-lookup"><span data-stu-id="12d00-136">Use Integration Services (SSIS)</span></span>
<span data-ttu-id="12d00-137">SQL Server'a yüklemek için zaten Integration Services (SSIS) paketleri kullanıyorsanız, hedef olarak SQL Server SQL veri ambarı ve kaynak kullanmak için paketlerinizi güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12d00-137">If you are already using Integration Services (SSIS) packages to load into SQL Server, you can update your packages to use SQL Server as the source and SQL Data Warehouse as the destination.</span></span> <span data-ttu-id="12d00-138">Bunu yapmak, kolay ve hızlı ve verileri bulutta zaten kullanmak için yükleme işlemi geçirmek çalışmıyorsanız iyi bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="12d00-138">This is quick and easy to do, and is a good choice if you are not trying to migrate your loading process to use data already in the cloud.</span></span> <span data-ttu-id="12d00-139">Kolaylığını yük bu SSIS paralel olarak yük gerçekleştirmez çünkü PolyBase kullanmaktan daha yavaş olacaktır ' dir.</span><span class="sxs-lookup"><span data-stu-id="12d00-139">The tradeoff is the load will be slower than using PolyBase because this SSIS does not perform the load in parallel.</span></span>

<span data-ttu-id="12d00-140">Yükleme işlemi özeti:</span><span class="sxs-lookup"><span data-stu-id="12d00-140">Summary of loading process:</span></span>

1. <span data-ttu-id="12d00-141">SQL Server örneği için kaynak ve hedef için SQL Data Warehouse veritabanına işaret edecek şekilde Integration Services paketinizi gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="12d00-141">Revise your Integration Services package to point to the SQL Server instance for the source and the SQL Data Warehouse database for the destination.</span></span>
2. <span data-ttu-id="12d00-142">Bunu zaten yoksa şemanızı SQL veri ambarı'na geçirin.</span><span class="sxs-lookup"><span data-stu-id="12d00-142">Migrate your schema to SQL Data Warehouse, if it is not there already.</span></span>
3. <span data-ttu-id="12d00-143">Değişiklik paketlerinizi eşlemesinde yalnızca SQL Data Warehouse tarafından desteklenen veri türlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="12d00-143">Change the mapping in your packages use only the data types that are supported by SQL Data Warehouse.</span></span>
4. <span data-ttu-id="12d00-144">Zamanlama ve paket çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="12d00-144">Schedule and run the package.</span></span>

<span data-ttu-id="12d00-145">Bir öğretici için bkz: [veri yükleme SQL Server'dan Azure SQL veri ambarı (SSIS)][Load data from SQL Server to Azure SQL Data Warehouse (SSIS)].</span><span class="sxs-lookup"><span data-stu-id="12d00-145">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (SSIS)][Load data from SQL Server to Azure SQL Data Warehouse (SSIS)].</span></span>

### <a name="use-azcopy-recommended-for--10-tb-data"></a><span data-ttu-id="12d00-146">AZCopy (< 10 TB veri için önerilir) kullanın</span><span class="sxs-lookup"><span data-stu-id="12d00-146">Use AZCopy (recommended for < 10 TB data)</span></span>
<span data-ttu-id="12d00-147">Veri boyutu < 10 TB ise, verileri SQL Server'dan düz dosyalara dışarı aktarabilir, Azure blob depolama alanına kopyalayın ve verileri SQL Data Warehouse'a veri yüklemek için Polybase'i kullanın</span><span class="sxs-lookup"><span data-stu-id="12d00-147">If your data size is < 10 TB, you can export the data from SQL Server to flat files, copy the files to Azure blob storage, and then use PolyBase to load the data into SQL Data Warehouse</span></span>

<span data-ttu-id="12d00-148">Yükleme işlemi özeti:</span><span class="sxs-lookup"><span data-stu-id="12d00-148">Summary of loading process:</span></span>

1. <span data-ttu-id="12d00-149">Verileri SQL Server'dan düz dosyalara dışarı aktarmak için bcp komut satırı yardımcı programını kullanın.</span><span class="sxs-lookup"><span data-stu-id="12d00-149">Use the bcp command-line utility to export data from SQL Server to flat files.</span></span>
2. <span data-ttu-id="12d00-150">Azure blob depolama alanına düz dosyalardan veri kopyalamak için AZCopy komut satırı yardımcı programını kullanın.</span><span class="sxs-lookup"><span data-stu-id="12d00-150">Use the AZCopy command-line utility to copy data from flat files to Azure blob storage.</span></span>
3. <span data-ttu-id="12d00-151">SQL Data Warehouse'a veri yüklemek için Polybase'i kullanın.</span><span class="sxs-lookup"><span data-stu-id="12d00-151">Use PolyBase to load into SQL Data Warehouse.</span></span>

<span data-ttu-id="12d00-152">Bir öğretici için bkz: [veri yükleme Azure blob depolama alanından SQL Data Warehouse'a (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="12d00-152">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

### <a name="use-bcp"></a><span data-ttu-id="12d00-153">BCP kullanın</span><span class="sxs-lookup"><span data-stu-id="12d00-153">Use bcp</span></span>
<span data-ttu-id="12d00-154">Az miktarda veriniz varsa, doğrudan Azure SQL Data Warehouse'a veri yüklemek için bcp kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12d00-154">If you have a small amount of data you can use bcp to load directly into Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="12d00-155">Yükleme işlemi özeti:</span><span class="sxs-lookup"><span data-stu-id="12d00-155">Summary of loading process:</span></span>

1. <span data-ttu-id="12d00-156">Verileri SQL Server'dan düz dosyalara dışarı aktarmak için bcp komut satırı yardımcı programını kullanın.</span><span class="sxs-lookup"><span data-stu-id="12d00-156">Use the bcp command-line utility to export data from SQL Server to flat files.</span></span>
2. <span data-ttu-id="12d00-157">Düz dosyalardan doğrudan SQL Data Warehouse'a veri yüklemek için BCP kullanın.</span><span class="sxs-lookup"><span data-stu-id="12d00-157">Use bcp to load data from flat files directly to SQL Data Warehouse.</span></span>

<span data-ttu-id="12d00-158">Bir öğretici için bkz: [veri yükleme SQL Server'dan Azure SQL veri ambarı'na (bcp)][Load data from SQL Server to Azure SQL Data Warehouse (bcp)].</span><span class="sxs-lookup"><span data-stu-id="12d00-158">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (bcp)][Load data from SQL Server to Azure SQL Data Warehouse (bcp)].</span></span>

### <a name="use-importexport-recommended-for--10-tb-data"></a><span data-ttu-id="12d00-159">İçeri/dışarı aktarma (> 10 TB veri için önerilir) kullanın</span><span class="sxs-lookup"><span data-stu-id="12d00-159">Use Import/Export (recommended for > 10 TB data)</span></span>
<span data-ttu-id="12d00-160">Veri boyutu > 10 TB ise ve Azure'a taşımak istediğiniz hizmet sevkiyat bizim disk kullanmanızı öneririz [içeri/dışarı aktarma][Import/Export].</span><span class="sxs-lookup"><span data-stu-id="12d00-160">If your data size is > 10 TB and you want to move it to Azure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span></span> 

<span data-ttu-id="12d00-161">Yükleme işlemi özeti</span><span class="sxs-lookup"><span data-stu-id="12d00-161">Summary of loading process</span></span>

1. <span data-ttu-id="12d00-162">Aktarılabilir disklerde düz dosyalar için SQL Server'dan veri aktarmak için bcp komut satırı yardımcı programını kullanın.</span><span class="sxs-lookup"><span data-stu-id="12d00-162">Use the bcp command-line utility to export data from SQL Server to flat files on transferrable disks.</span></span>
2. <span data-ttu-id="12d00-163">Microsoft disklere birlikte.</span><span class="sxs-lookup"><span data-stu-id="12d00-163">Ship the disks to Microsoft.</span></span>
3. <span data-ttu-id="12d00-164">Microsoft verileri SQL Data Warehouse'a veri yükler.</span><span class="sxs-lookup"><span data-stu-id="12d00-164">Microsoft loads the data into SQL Data Warehouse</span></span>

## <a name="load-from-hdinsight"></a><span data-ttu-id="12d00-165">Hdınsight'ta yükleme</span><span class="sxs-lookup"><span data-stu-id="12d00-165">Load from HDInsight</span></span>
<span data-ttu-id="12d00-166">SQL veri ambarı veri PolyBase aracılığıyla hdınsight'tan destekler.</span><span class="sxs-lookup"><span data-stu-id="12d00-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span></span> <span data-ttu-id="12d00-167">Azure Blob depolama alanından verileri yükleniyor - Hdınsight'a verileri yüklemek için bağlanmak için Polybase'i kullanarak aynı işlemidir.</span><span class="sxs-lookup"><span data-stu-id="12d00-167">The process is the same as loading data from Azure Blob Storage - using PolyBase to connect to HDInsight to load data.</span></span> 

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="12d00-168">1. PolyBase ve T-SQL kullanın</span><span class="sxs-lookup"><span data-stu-id="12d00-168">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="12d00-169">Yükleme işlemi özeti:</span><span class="sxs-lookup"><span data-stu-id="12d00-169">Summary of loading process:</span></span>

1. <span data-ttu-id="12d00-170">Hdınsight'a verilerinizi taşıma ve metin dosyalarını saklamak ORC veya Parquet biçimi.</span><span class="sxs-lookup"><span data-stu-id="12d00-170">Move your data to HDInsight and store it in text files, ORC or Parquet format.</span></span>
2. <span data-ttu-id="12d00-171">Dış nesne veri biçimi ve konumunu tanımlamak için SQL veri ambarında yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="12d00-171">Configure external objects in SQL Data Warehouse to define the location and format of the data.</span></span>
3. <span data-ttu-id="12d00-172">Yeni bir veritabanı tablosuna paralel veri yüklemek için bir T-SQL komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="12d00-172">Run a T-SQL command to load the data in parallel into a new database table.</span></span>

<span data-ttu-id="12d00-173">Bir öğretici için bkz: [veri yükleme Azure blob depolama alanından SQL Data Warehouse'a (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="12d00-173">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

## <a name="recommendations"></a><span data-ttu-id="12d00-174">Öneriler</span><span class="sxs-lookup"><span data-stu-id="12d00-174">Recommendations</span></span>
<span data-ttu-id="12d00-175">Ortaklarımızın çoğunun çözümleri yüklenirken vardır.</span><span class="sxs-lookup"><span data-stu-id="12d00-175">Many of our partners have loading solutions.</span></span> <span data-ttu-id="12d00-176">Daha fazla bilgi bulmak için bir listesini görmek bizim [çözüm ortakları][solution partners].</span><span class="sxs-lookup"><span data-stu-id="12d00-176">To find out more, see a list of our [solution partners][solution partners].</span></span> 

<span data-ttu-id="12d00-177">Verilerinizi ilişkisel olmayan bir kaynaktan geldiğinden ve SQL Data Warehouse'a veri yüklemek istiyorsanız, yükleme önce satırlar ve sütunlar halinde dönüştürmek gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="12d00-177">If your data is coming from a non-relational source and you want to load it into SQL Data Warehouse you will need to transform it into rows and columns before you load it.</span></span> <span data-ttu-id="12d00-178">Dönüştürülmüş verileri bir veritabanına depolanmasını gerektirmez, metin dosyalarından depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="12d00-178">The transformed data doesn't need to be stored in a database, it can be stored in text files.</span></span>

<span data-ttu-id="12d00-179">Yeni yüklenen verilere ilişkin istatistikler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="12d00-179">Create statistics on newly loaded data.</span></span> <span data-ttu-id="12d00-180">Azure SQL Data Warehouse henüz istatistiklerin otomatik olarak oluşturulup güncelleştirilmesini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="12d00-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="12d00-181">Sorgularınızdan en iyi performansı alabilmek için ilk yükleme işleminden sonra tüm tabloların tüm sütunlarda istatistikler oluşturmak önemli olduğunu veya verilerdeki önemli değişikliklerden.</span><span class="sxs-lookup"><span data-stu-id="12d00-181">In order to get the best performance from your queries, it's important to create statistics on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="12d00-182">Ayrıntılar için bkz [istatistikleri][Statistics].</span><span class="sxs-lookup"><span data-stu-id="12d00-182">For details, see [Statistics][Statistics].</span></span>

## <a name="next-steps"></a><span data-ttu-id="12d00-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="12d00-183">Next steps</span></span>
<span data-ttu-id="12d00-184">Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].</span><span class="sxs-lookup"><span data-stu-id="12d00-184">For more development tips, see the [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage to SQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server to Azure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server to Azure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server to Azure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
