---
title: "Azure Machine Learning için gelişmiş analizler senaryolarını belirle | Microsoft Docs"
description: "Tahmine dayalı analiz takım veri bilimi işlemine Gelişmiş yapmak için uygun senaryolar seçin."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: fe4f74f2e0602d13eedb6ca186480291a9a5724f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="41c23-103">Azure Machine Learning’de gelişmiş analiz senaryoları</span><span class="sxs-lookup"><span data-stu-id="41c23-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="41c23-104">Bu makalede birçok örnek veri kaynakları ve tarafından işlenen hedef senaryoları özetlenmektedir [takım veri bilimi işlem (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="41c23-104">This article outlines the variety of sample data sources and target scenarios that can be handled by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span> <span data-ttu-id="41c23-105">TDSP akıllı uygulamaları derleme işbirliği yapmak ekipler için sistematik bir yaklaşım sağlar.</span><span class="sxs-lookup"><span data-stu-id="41c23-105">The TDSP provides a systematic approach for teams to collaborate on building intelligent applications.</span></span> <span data-ttu-id="41c23-106">Burada sunulan senaryoları veri özellikleri, kaynak konumları ve Azure hedef depoları bağlıdır veri işleme iş akışı içinde kullanılabilir seçenekler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="41c23-106">The scenarios presented here illustrate options available in the data processing workflow that depend on the data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="41c23-107">**Karar ağacı** veri ve hedefi için uygun olan örnek senaryolar seçerek son bölümde sunulan için.</span><span class="sxs-lookup"><span data-stu-id="41c23-107">The **decision tree** for selecting the sample scenarios that is appropriate for your data and objective is presented in the last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="41c23-108">Aşağıdaki bölümlerde bir örnek senaryo sunar.</span><span class="sxs-lookup"><span data-stu-id="41c23-108">Each of the following sections presents a sample scenario.</span></span> <span data-ttu-id="41c23-109">Her senaryo, olası veri bilimi veya gelişmiş analizler için akışı ve Azure kaynaklarını destekleyen listelenir.</span><span class="sxs-lookup"><span data-stu-id="41c23-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="41c23-110">**Aşağıdaki senaryoların tümünde için şunları yapmanız gerekir:**
> </span><span class="sxs-lookup"><span data-stu-id="41c23-110">**For all of the following scenarios, you need to:**
</span></span><br/>
> 
> * <span data-ttu-id="41c23-111">[Depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md)
>   </span><span class="sxs-lookup"><span data-stu-id="41c23-111">[Create a storage account](../storage/common/storage-create-storage-account.md)
</span></span><br/>
> * [<span data-ttu-id="41c23-112">Bir Azure Machine Learning çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="41c23-112">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
> 
> 

## <span data-ttu-id="41c23-113"><a name="smalllocal"></a>Senaryo \#1: küçük ve orta tablolu bir veri kümesini yerel dosyaları</span><span class="sxs-lookup"><span data-stu-id="41c23-113"><a name="smalllocal"></a>Scenario \#1: Small to medium tabular dataset in a local files</span></span>
![Küçük ve orta yerel dosyaları][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="41c23-115">Ek Azure kaynaklarını: yok</span><span class="sxs-lookup"><span data-stu-id="41c23-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="41c23-116">Oturum [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="41c23-116">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="41c23-117">Bir veri kümesi karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="41c23-117">Upload a dataset.</span></span>
3. <span data-ttu-id="41c23-118">Karşıya yüklenen veri kümeleri ile başlayan bir Azure Machine Learning deneme akışı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41c23-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <span data-ttu-id="41c23-119"><a name="smalllocalprocess"></a>Senaryo \#2: küçük ve orta dataset işleme gerektiren yerel dosyaları</span><span class="sxs-lookup"><span data-stu-id="41c23-119"><a name="smalllocalprocess"></a>Scenario \#2: Small to medium dataset of local files that require processing</span></span>
![Küçük ve orta yerel dosyaları işleme ile][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="41c23-121">Ek Azure kaynaklarını: Azure sanal makinesi (IPython not defteri sunucusu)</span><span class="sxs-lookup"><span data-stu-id="41c23-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="41c23-122">IPython dizüstü çalıştıran bir Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41c23-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="41c23-123">Verileri bir Azure depolama kapsayıcısı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="41c23-123">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="41c23-124">Önceden işleyebilir ve verileri Azure depolama kapsayıcıdan verilere IPython not defterinde Temizle.</span><span class="sxs-lookup"><span data-stu-id="41c23-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
4. <span data-ttu-id="41c23-125">Temizlenen için tablo form verileri dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="41c23-125">Transform data to cleaned, tabular form.</span></span>
5. <span data-ttu-id="41c23-126">Dönüştürülen veriler Azure BLOB'ları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="41c23-126">Save transformed data in Azure blobs.</span></span>
6. <span data-ttu-id="41c23-127">Oturum [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="41c23-127">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
7. <span data-ttu-id="41c23-128">Verileri kullanarak Azure bloblarından okuma [veri içeri aktarma] [ import-data] modülü.</span><span class="sxs-lookup"><span data-stu-id="41c23-128">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
8. <span data-ttu-id="41c23-129">Alınan veri kümeleri ile başlayan bir Azure Machine Learning deneme akışı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41c23-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="41c23-130"><a name="largelocal"></a>Senaryo \#3: büyük veri kümesi yerel dosyaların Azure BLOB'ları hedefleme</span><span class="sxs-lookup"><span data-stu-id="41c23-130"><a name="largelocal"></a>Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![Büyük yerel dosyaları][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="41c23-132">Ek Azure kaynaklarını: Azure sanal makinesi (IPython not defteri sunucusu)</span><span class="sxs-lookup"><span data-stu-id="41c23-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="41c23-133">IPython dizüstü çalıştıran bir Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41c23-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="41c23-134">Verileri bir Azure depolama kapsayıcısı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="41c23-134">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="41c23-135">Önceden işleyebilir ve IPython Azure bloblarından verilere dizüstü bilgisayar, veri temizleme.</span><span class="sxs-lookup"><span data-stu-id="41c23-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
4. <span data-ttu-id="41c23-136">Gerekirse temizlenmesi için Tablo formunda, verileri dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="41c23-136">Transform data to cleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="41c23-137">Verileri araştırmak ve Özellikler gerektiği şekilde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41c23-137">Explore data, and create features as needed.</span></span>
6. <span data-ttu-id="41c23-138">Küçük ve orta veri örneği ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="41c23-138">Extract a small-to-medium data sample.</span></span>
7. <span data-ttu-id="41c23-139">Örneklenen verileri Azure BLOB'ları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="41c23-139">Save the sampled data in Azure blobs.</span></span>
8. <span data-ttu-id="41c23-140">Oturum [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="41c23-140">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="41c23-141">Verileri kullanarak Azure bloblarından okuma [veri içeri aktarma] [ import-data] modülü.</span><span class="sxs-lookup"><span data-stu-id="41c23-141">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
10. <span data-ttu-id="41c23-142">Alınan veri kümeleri ile başlayan Azure Machine Learning deneme akış oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41c23-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="41c23-143"><a name="smalllocaltodb"></a>Senaryo \#4: küçük ve orta dataset yerel dosyaları, SQL Server içinde bir Azure sanal makine hedefleme</span><span class="sxs-lookup"><span data-stu-id="41c23-143"><a name="smalllocaltodb"></a>Scenario \#4: Small to medium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![Küçük ve orta yerel SQL Azure DB'de dosyaları][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="41c23-145">Ek Azure kaynaklarını: Azure sanal makinesi (SQL Server / IPython dizüstü sunucu)</span><span class="sxs-lookup"><span data-stu-id="41c23-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="41c23-146">SQL Server + IPython dizüstü çalıştıran bir Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41c23-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
2. <span data-ttu-id="41c23-147">Verileri bir Azure depolama kapsayıcısı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="41c23-147">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="41c23-148">Önceden işleyebilir ve IPython Not Defteri kullanarak Azure depolama kapsayıcısının verileri temizleyin.</span><span class="sxs-lookup"><span data-stu-id="41c23-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
4. <span data-ttu-id="41c23-149">Gerekirse temizlenmesi için Tablo formunda, verileri dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="41c23-149">Transform data to cleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="41c23-150">VM yerel dosyalar için verileri kaydetmek (IPython dizüstü bilgisayar, VM üzerinde çalıştığından, yerel sürücülere VM sürücülere bakın).</span><span class="sxs-lookup"><span data-stu-id="41c23-150">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
6. <span data-ttu-id="41c23-151">Bir Azure VM'de çalışan SQL Server veritabanına veri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="41c23-151">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="41c23-152">Seçenek \#1: SQL Server Management Studio'yu kullanarak.</span><span class="sxs-lookup"><span data-stu-id="41c23-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="41c23-153">SQL Server'da VM oturum açma</span><span class="sxs-lookup"><span data-stu-id="41c23-153">Login to SQL Server VM</span></span>
   * <span data-ttu-id="41c23-154">SQL Server Management Studio'yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="41c23-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="41c23-155">Veritabanı ve hedef tablolar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41c23-155">Create database and target tables.</span></span>
   * <span data-ttu-id="41c23-156">Toplu birini kullanın VM yerel dosyalarından veri yüklemek için yöntemleri içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="41c23-156">Use one of the bulk import methods to load the data from VM-local files.</span></span>
   
   <span data-ttu-id="41c23-157">Seçenek \#2: kullanarak IPython not defteri – Orta ve büyük veri kümeleri için değil önerilir</span><span class="sxs-lookup"><span data-stu-id="41c23-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="41c23-158">SQL Server VM üzerinde erişmek için ODBC bağlantı dizesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="41c23-158">Use ODBC connection string to access SQL Server on VM.</span></span>
   * <span data-ttu-id="41c23-159">Veritabanı ve hedef tablolar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41c23-159">Create database and target tables.</span></span>
   * <span data-ttu-id="41c23-160">Toplu birini kullanın VM yerel dosyalarından veri yüklemek için yöntemleri içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="41c23-160">Use one of the bulk import methods to load the data from VM-local files.</span></span>
7. <span data-ttu-id="41c23-161">Özellikler gerektiği şekilde oluşturun, verileri keşfedin.</span><span class="sxs-lookup"><span data-stu-id="41c23-161">Explore data, create features as needed.</span></span> <span data-ttu-id="41c23-162">Özellikleri veritabanı tablolarında gerçekleştirilmesi gerekmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="41c23-162">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="41c23-163">Yalnızca bunları oluşturmak için gerekli sorgu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="41c23-163">Only note the necessary query to create them.</span></span>
8. <span data-ttu-id="41c23-164">Gerekli ve/veya istenen veri örnek boyutu üzerinde karar.</span><span class="sxs-lookup"><span data-stu-id="41c23-164">Decide on a data sample size, if needed and/or desired.</span></span>
9. <span data-ttu-id="41c23-165">Oturum [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="41c23-165">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
10. <span data-ttu-id="41c23-166">SQL Server kullanarak doğrudan gelen verileri okumak [veri içeri aktarma] [ import-data] modülü.</span><span class="sxs-lookup"><span data-stu-id="41c23-166">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="41c23-167">Alanları ayıklar, özellikleri oluşturur ve veri doğrudan gerekirse örnekleri gerekli sorgu Yapıştır [veri içeri aktarma] [ import-data] sorgu.</span><span class="sxs-lookup"><span data-stu-id="41c23-167">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
11. <span data-ttu-id="41c23-168">Alınan veri kümeleri ile başlayan Azure Machine Learning deneme akış oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41c23-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="41c23-169"><a name="largelocaltodb"></a>Senaryo \#5: yerel dosyaları büyük bir veri kümesini hedef Azure VM'deki SQL Server</span><span class="sxs-lookup"><span data-stu-id="41c23-169"><a name="largelocaltodb"></a>Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![SQL Azure DB'de büyük yerel dosyalar][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="41c23-171">Ek Azure kaynaklarını: Azure sanal makinesi (SQL Server / IPython dizüstü sunucu)</span><span class="sxs-lookup"><span data-stu-id="41c23-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="41c23-172">SQL Server ve IPython dizüstü server çalıştıran bir Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41c23-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="41c23-173">Verileri bir Azure depolama kapsayıcısı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="41c23-173">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="41c23-174">(İsteğe bağlı) Önceden işleyebilir ve veri temizleme.</span><span class="sxs-lookup"><span data-stu-id="41c23-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="41c23-175">a.</span><span class="sxs-lookup"><span data-stu-id="41c23-175">a.</span></span>  <span data-ttu-id="41c23-176">Önceden işleyebilir ve IPython Azure'dan verilere dizüstü bilgisayar, veri temizleme</span><span class="sxs-lookup"><span data-stu-id="41c23-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="41c23-177">b.</span><span class="sxs-lookup"><span data-stu-id="41c23-177">b.</span></span>  <span data-ttu-id="41c23-178">Gerekirse temizlenmesi için Tablo formunda, verileri dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="41c23-178">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="41c23-179">c.</span><span class="sxs-lookup"><span data-stu-id="41c23-179">c.</span></span>  <span data-ttu-id="41c23-180">VM yerel dosyalar için verileri kaydetmek (IPython dizüstü bilgisayar, VM üzerinde çalıştığından, yerel sürücülere VM sürücülere bakın).</span><span class="sxs-lookup"><span data-stu-id="41c23-180">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
4. <span data-ttu-id="41c23-181">Bir Azure VM'de çalışan SQL Server veritabanına veri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="41c23-181">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="41c23-182">a.</span><span class="sxs-lookup"><span data-stu-id="41c23-182">a.</span></span>  <span data-ttu-id="41c23-183">SQL Server VM oturum açın.</span><span class="sxs-lookup"><span data-stu-id="41c23-183">Login to SQL Server VM.</span></span>
   
   <span data-ttu-id="41c23-184">b.</span><span class="sxs-lookup"><span data-stu-id="41c23-184">b.</span></span>  <span data-ttu-id="41c23-185">Veri zaten kaydedilmemişse, veri dosyalarını Azure'dan indirir.</span><span class="sxs-lookup"><span data-stu-id="41c23-185">If data not saved already, download data files from Azure</span></span>
   
       storage container to local-VM folder.
   
   <span data-ttu-id="41c23-186">c.</span><span class="sxs-lookup"><span data-stu-id="41c23-186">c.</span></span>  <span data-ttu-id="41c23-187">SQL Server Management Studio'yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="41c23-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="41c23-188">d.</span><span class="sxs-lookup"><span data-stu-id="41c23-188">d.</span></span>  <span data-ttu-id="41c23-189">Veritabanı ve hedef tablolar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41c23-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="41c23-190">e.</span><span class="sxs-lookup"><span data-stu-id="41c23-190">e.</span></span>  <span data-ttu-id="41c23-191">Verileri yüklemek için yöntemleri içe toplu birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="41c23-191">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="41c23-192">f.</span><span class="sxs-lookup"><span data-stu-id="41c23-192">f.</span></span>  <span data-ttu-id="41c23-193">Tablo birleştirme gerekirse, birleştirmeler hızlandırmak için dizinler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41c23-193">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="41c23-194">Büyük veri boyutları hızlı yükleme için bölümlenmiş tabloları oluşturma ve toplu içeri aktarma verileri paralel önerilir.</span><span class="sxs-lookup"><span data-stu-id="41c23-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import the data in parallel.</span></span> <span data-ttu-id="41c23-195">Daha fazla bilgi için bkz: [paralel veri içe aktarma SQL bölümlenmiş tablolar](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="41c23-195">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="41c23-196">Özellikler gerektiği şekilde oluşturun, verileri keşfedin.</span><span class="sxs-lookup"><span data-stu-id="41c23-196">Explore data, create features as needed.</span></span> <span data-ttu-id="41c23-197">Özellikleri veritabanı tablolarında gerçekleştirilmesi gerekmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="41c23-197">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="41c23-198">Yalnızca bunları oluşturmak için gerekli sorgu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="41c23-198">Only note the necessary query to create them.</span></span>
6. <span data-ttu-id="41c23-199">Gerekli ve/veya istenen veri örnek boyutu üzerinde karar.</span><span class="sxs-lookup"><span data-stu-id="41c23-199">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="41c23-200">Oturum [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="41c23-200">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="41c23-201">SQL Server kullanarak doğrudan gelen verileri okumak [veri içeri aktarma] [ import-data] modülü.</span><span class="sxs-lookup"><span data-stu-id="41c23-201">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="41c23-202">Alanları ayıklar, özellikleri oluşturur ve veri doğrudan gerekirse örnekleri gerekli sorgu Yapıştır [veri içeri aktarma] [ import-data] sorgu.</span><span class="sxs-lookup"><span data-stu-id="41c23-202">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="41c23-203">Karşıya yüklenen veri kümesi ile başlayan basit Azure Machine Learning deneme akışı</span><span class="sxs-lookup"><span data-stu-id="41c23-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <span data-ttu-id="41c23-204"><a name="largedbtodb"></a>Senaryo \#6: bir SQL Server veritabanı SQL Server içinde bir Azure sanal makine hedefleme şirket içi, büyük bir veri kümesini</span><span class="sxs-lookup"><span data-stu-id="41c23-204"><a name="largedbtodb"></a>Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![Büyük SQL DB şirket içi SQL Azure DB'de için][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="41c23-206">Ek Azure kaynaklarını: Azure sanal makinesi (SQL Server / IPython dizüstü sunucu)</span><span class="sxs-lookup"><span data-stu-id="41c23-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="41c23-207">SQL Server ve IPython dizüstü server çalıştıran bir Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41c23-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="41c23-208">Veri birini kullanın veri döküm dosyaları için SQL Server'dan dışarı aktarmak için yöntemleri verin.</span><span class="sxs-lookup"><span data-stu-id="41c23-208">Use one of the data export methods to export the data from SQL Server to dump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="41c23-209">Şirket içi veritabanından azure'da SQL Server örneği için tam veritabanını taşımak için bir alternatif (hızlı) yöntemi tüm verileri taşımaya karar verirseniz.</span><span class="sxs-lookup"><span data-stu-id="41c23-209">If you decide to move all data from the on-prem database, an alternate (faster) method to move the full database to the SQL Server instance in Azure.</span></span> <span data-ttu-id="41c23-210">Verileri dışarı aktarma, veritabanı, oluşturma ve yük/hedef veritabanına veri içeri aktarma ve Alternatif yöntem izleyin adımları atlayın.</span><span class="sxs-lookup"><span data-stu-id="41c23-210">Skip the steps to export data, create database, and load/import data to the target database and follow the alternate method.</span></span>
   > 
   > 
3. <span data-ttu-id="41c23-211">Azure depolama kapsayıcısı için döküm dosyalarını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="41c23-211">Upload dump files to Azure storage container.</span></span>
4. <span data-ttu-id="41c23-212">Bir Azure sanal makinede çalışan SQL Server veritabanına veri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="41c23-212">Load the data to a SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="41c23-213">a.</span><span class="sxs-lookup"><span data-stu-id="41c23-213">a.</span></span>  <span data-ttu-id="41c23-214">SQL Server VM oturum açın.</span><span class="sxs-lookup"><span data-stu-id="41c23-214">Login to the SQL Server VM.</span></span>
   
   <span data-ttu-id="41c23-215">b.</span><span class="sxs-lookup"><span data-stu-id="41c23-215">b.</span></span>  <span data-ttu-id="41c23-216">Veri dosyaları bir Azure depolama kapsayıcıdan VM yerel klasöre yükleyin.</span><span class="sxs-lookup"><span data-stu-id="41c23-216">Download data files from an Azure storage container to the local-VM folder.</span></span>
   
   <span data-ttu-id="41c23-217">c.</span><span class="sxs-lookup"><span data-stu-id="41c23-217">c.</span></span>  <span data-ttu-id="41c23-218">SQL Server Management Studio'yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="41c23-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="41c23-219">d.</span><span class="sxs-lookup"><span data-stu-id="41c23-219">d.</span></span>  <span data-ttu-id="41c23-220">Veritabanı ve hedef tablolar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41c23-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="41c23-221">e.</span><span class="sxs-lookup"><span data-stu-id="41c23-221">e.</span></span>  <span data-ttu-id="41c23-222">Verileri yüklemek için yöntemleri içe toplu birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="41c23-222">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="41c23-223">f.</span><span class="sxs-lookup"><span data-stu-id="41c23-223">f.</span></span>  <span data-ttu-id="41c23-224">Tablo birleştirme gerekirse, birleştirmeler hızlandırmak için dizinler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41c23-224">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="41c23-225">Büyük veri boyutları, hızlı yükleme oluşturmak için bölümlenmiş tablolar ve toplu paralel veri içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="41c23-225">For faster loading of large data sizes, create partitioned tables and to bulk import the data in parallel.</span></span> <span data-ttu-id="41c23-226">Daha fazla bilgi için bkz: [paralel veri içe aktarma SQL bölümlenmiş tablolar](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="41c23-226">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="41c23-227">Özellikler gerektiği şekilde oluşturun, verileri keşfedin.</span><span class="sxs-lookup"><span data-stu-id="41c23-227">Explore data, create features as needed.</span></span> <span data-ttu-id="41c23-228">Özellikleri veritabanı tablolarında gerçekleştirilmesi gerekmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="41c23-228">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="41c23-229">Yalnızca bunları oluşturmak için gerekli sorgu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="41c23-229">Only note the necessary query to create them.</span></span>
6. <span data-ttu-id="41c23-230">Gerekli ve/veya istenen veri örnek boyutu üzerinde karar.</span><span class="sxs-lookup"><span data-stu-id="41c23-230">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="41c23-231">Oturum [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="41c23-231">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="41c23-232">SQL Server kullanarak doğrudan gelen verileri okumak [veri içeri aktarma] [ import-data] modülü.</span><span class="sxs-lookup"><span data-stu-id="41c23-232">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="41c23-233">Alanları ayıklar, özellikleri oluşturur ve veri doğrudan gerekirse örnekleri gerekli sorgu Yapıştır [veri içeri aktarma] [ import-data] sorgu.</span><span class="sxs-lookup"><span data-stu-id="41c23-233">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="41c23-234">Basit Azure Machine Learning ile karşıya yüklenen dataset başlangıç akışı deneyin.</span><span class="sxs-lookup"><span data-stu-id="41c23-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-to-copy-a-full-database-from-an-on-premises--sql-server-to-azure-sql-database"></a><span data-ttu-id="41c23-235">Tam bir veritabanı bir şirket içi SQL Server'dan Azure SQL veritabanına kopyalamak için alternatif yöntemi</span><span class="sxs-lookup"><span data-stu-id="41c23-235">Alternate method to copy a full database from an on-premises  SQL Server to Azure SQL Database</span></span>
![Yerel DB detach ve Azure SQL DB ekleme][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="41c23-237">Ek Azure kaynaklarını: Azure sanal makinesi (SQL Server / IPython dizüstü sunucu)</span><span class="sxs-lookup"><span data-stu-id="41c23-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="41c23-238">SQL Server VM'nize tüm SQL Server veritabanında çoğaltmak için bir veritabanı bir konum/sunucudan diğerine veritabanı geçici olarak çevrimdışı duruma olduğunu varsayarak kopyalamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="41c23-238">To replicate the entire SQL Server database in your SQL Server VM, you should copy a database from one location/server to another, assuming that the database can be taken temporarily offline.</span></span> <span data-ttu-id="41c23-239">Bu SQL Server Management Studio Object Explorer veya eşdeğer Transact-SQL komutlarını kullanarak yapın.</span><span class="sxs-lookup"><span data-stu-id="41c23-239">You do this in the SQL Server Management Studio Object Explorer, or using the equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="41c23-240">Kaynak konumda veritabanı ayrılmadı.</span><span class="sxs-lookup"><span data-stu-id="41c23-240">Detach the database at the source location.</span></span> <span data-ttu-id="41c23-241">Daha fazla bilgi için bkz: [bir veritabanını ayırma](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="41c23-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
2. <span data-ttu-id="41c23-242">Windows Explorer ya da Windows komut istemi penceresinde, ayrılmış veritabanına dosya veya dosyalar ve günlük dosyasının veya dosyalarının azure'da SQL Server VM üzerinde hedef konuma kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="41c23-242">In Windows Explorer or Windows Command Prompt window, copy the detached database file or files and log file or files to the target location on the SQL Server VM in Azure.</span></span>
3. <span data-ttu-id="41c23-243">Kopyalanan dosyalar hedef SQL Server örneğine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="41c23-243">Attach the copied files to the target SQL Server instance.</span></span> <span data-ttu-id="41c23-244">Daha fazla bilgi için bkz: [bir veritabanını](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="41c23-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="41c23-245">[Kullanarak bir veritabanı ayırma ve (Transact-SQL) ekleme taşıma](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="41c23-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <span data-ttu-id="41c23-246"><a name="largedbtohive"></a>Senaryo \#7: yerel dosyalarında büyük veri hedef Azure Hdınsight Hadoop kümeleri Hive veritabanında</span><span class="sxs-lookup"><span data-stu-id="41c23-246"><a name="largedbtohive"></a>Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![Yerel hedef Hive büyük verileri][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="41c23-248">Ek Azure kaynaklarını: Azure Hdınsight Hadoop kümesi ve Azure sanal makine (IPython not defteri sunucusu)</span><span class="sxs-lookup"><span data-stu-id="41c23-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="41c23-249">IPython dizüstü server çalıştıran bir Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41c23-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
2. <span data-ttu-id="41c23-250">Bir Azure Hdınsight Hadoop kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41c23-250">Create an Azure HDInsight Hadoop cluster.</span></span>
3. <span data-ttu-id="41c23-251">(İsteğe bağlı) Önceden işleyebilir ve veri temizleme.</span><span class="sxs-lookup"><span data-stu-id="41c23-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="41c23-252">a.</span><span class="sxs-lookup"><span data-stu-id="41c23-252">a.</span></span>  <span data-ttu-id="41c23-253">Önceden işleyebilir ve IPython Azure'dan verilere dizüstü bilgisayar, veri temizleme</span><span class="sxs-lookup"><span data-stu-id="41c23-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="41c23-254">b.</span><span class="sxs-lookup"><span data-stu-id="41c23-254">b.</span></span>  <span data-ttu-id="41c23-255">Gerekirse temizlenmesi için Tablo formunda, verileri dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="41c23-255">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="41c23-256">c.</span><span class="sxs-lookup"><span data-stu-id="41c23-256">c.</span></span>  <span data-ttu-id="41c23-257">VM yerel dosyalar için verileri kaydetmek (IPython dizüstü bilgisayar, VM üzerinde çalıştığından, yerel sürücülere VM sürücülere bakın).</span><span class="sxs-lookup"><span data-stu-id="41c23-257">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
4. <span data-ttu-id="41c23-258">2. adımda seçilen Hadoop kümesi varsayılan kapsayıcı için veri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="41c23-258">Upload data to the default container of the Hadoop cluster selected in the step 2.</span></span>
5. <span data-ttu-id="41c23-259">Azure Hdınsight Hadoop kümesindeki Hive veritabanına veri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="41c23-259">Load data to Hive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="41c23-260">a.</span><span class="sxs-lookup"><span data-stu-id="41c23-260">a.</span></span>  <span data-ttu-id="41c23-261">Hadoop küme baş düğümüne oturum açın</span><span class="sxs-lookup"><span data-stu-id="41c23-261">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="41c23-262">b.</span><span class="sxs-lookup"><span data-stu-id="41c23-262">b.</span></span>  <span data-ttu-id="41c23-263">Hadoop komut satırı açın.</span><span class="sxs-lookup"><span data-stu-id="41c23-263">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="41c23-264">c.</span><span class="sxs-lookup"><span data-stu-id="41c23-264">c.</span></span>  <span data-ttu-id="41c23-265">Komutu tarafından Hive kök dizini girin `cd %hive_home%\bin` , Hadoop komut satırı.</span><span class="sxs-lookup"><span data-stu-id="41c23-265">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="41c23-266">d.</span><span class="sxs-lookup"><span data-stu-id="41c23-266">d.</span></span>  <span data-ttu-id="41c23-267">Veritabanı ve tablo oluşturmak için Hive sorguları çalıştırmak ve verileri blob depolama alanından Hive tablolara yüklemek.</span><span class="sxs-lookup"><span data-stu-id="41c23-267">Run the Hive queries to create database and tables, and load data from blob storage to Hive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="41c23-268">Verileri büyük ise, kullanıcıların bölümlerle Hive tablosu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41c23-268">If the data is big, users can create the Hive table with partitions.</span></span> <span data-ttu-id="41c23-269">Kullanıcılar daha sonra kullanabileceğiniz bir `for` döngü içinde Hadoop bölüm bölümlenmiş Hive tablosu verileri yüklemek için komut satırını baş düğüm.</span><span class="sxs-lookup"><span data-stu-id="41c23-269">Then, users can use a `for` loop in the Hadoop Command Line on the head node to load data into the Hive table partitioned by partition.</span></span>
   > 
   > 
6. <span data-ttu-id="41c23-270">Verileri araştırmak ve özellikleri Hadoop komut satırında gerektiği şekilde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41c23-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="41c23-271">Özellikleri veritabanı tablolarında gerçekleştirilmesi gerekmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="41c23-271">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="41c23-272">Yalnızca bunları oluşturmak için gerekli sorgu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="41c23-272">Only note the necessary query to create them.</span></span>
   
   <span data-ttu-id="41c23-273">a.</span><span class="sxs-lookup"><span data-stu-id="41c23-273">a.</span></span>  <span data-ttu-id="41c23-274">Hadoop küme baş düğümüne oturum açın</span><span class="sxs-lookup"><span data-stu-id="41c23-274">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="41c23-275">b.</span><span class="sxs-lookup"><span data-stu-id="41c23-275">b.</span></span>  <span data-ttu-id="41c23-276">Hadoop komut satırı açın.</span><span class="sxs-lookup"><span data-stu-id="41c23-276">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="41c23-277">c.</span><span class="sxs-lookup"><span data-stu-id="41c23-277">c.</span></span>  <span data-ttu-id="41c23-278">Komutu tarafından Hive kök dizini girin `cd %hive_home%\bin` , Hadoop komut satırı.</span><span class="sxs-lookup"><span data-stu-id="41c23-278">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="41c23-279">d.</span><span class="sxs-lookup"><span data-stu-id="41c23-279">d.</span></span>  <span data-ttu-id="41c23-280">Hive sorguları Hadoop komut satırında verileri araştırmak ve gerektiği gibi özellikleri oluşturmak için Hadoop kümesi baş düğümünde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="41c23-280">Run the Hive queries in Hadoop Command Line on the head node of the Hadoop cluster to explore the data and create features as needed.</span></span>
7. <span data-ttu-id="41c23-281">Gerekli ve/veya istenen, Azure Machine Learning Studio'da sığması için veri örneği.</span><span class="sxs-lookup"><span data-stu-id="41c23-281">If needed and/or desired, sample the data to fit in Azure Machine Learning Studio.</span></span>
8. <span data-ttu-id="41c23-282">Oturum [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="41c23-282">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="41c23-283">Verileri doğrudan okumak `Hive Queries` kullanarak [veri içeri aktarma] [ import-data] modülü.</span><span class="sxs-lookup"><span data-stu-id="41c23-283">Read the data directly from the `Hive Queries` using the [Import Data][import-data] module.</span></span> <span data-ttu-id="41c23-284">Alanları ayıklar, özellikleri oluşturur ve veri doğrudan gerekirse örnekleri gerekli sorgu Yapıştır [veri içeri aktarma] [ import-data] sorgu.</span><span class="sxs-lookup"><span data-stu-id="41c23-284">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
10. <span data-ttu-id="41c23-285">Basit Azure Machine Learning ile karşıya yüklenen dataset başlangıç akışı deneyin.</span><span class="sxs-lookup"><span data-stu-id="41c23-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <span data-ttu-id="41c23-286"><a name="decisiontree"></a>Senaryo seçimi için karar ağacı</span><span class="sxs-lookup"><span data-stu-id="41c23-286"><a name="decisiontree"></a>Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="41c23-287">Aşağıdaki diyagramda, yukarıda açıklanan senaryoları ve Gelişmiş analiz işlem ve teknoloji seçimleri dökümü senaryoları için aldığınız yapılan özetler.</span><span class="sxs-lookup"><span data-stu-id="41c23-287">The following diagram summarizes the scenarios described above and the Advanced Analytics Process and Technology choices made that take you to each of the itemized scenarios.</span></span> <span data-ttu-id="41c23-288">Veri işleme, keşfi, özellik Mühendisliği ve örnekleme alabileceğini unutmayın, bir veya daha fazla yöntem/ortam--kaynaktaki, Ara, ve/veya hedef ortamları – içinde yerleştirin ve gerektiğinde tekrarlayarak devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41c23-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at the source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="41c23-289">Diyagram yalnızca bazı olası akışlarının çizim görev yapar ve kapsamlı bir numaralandırma sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="41c23-289">The diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![DS işlemi izlenecek senaryolar][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="41c23-291">Gelişmiş analizler eylem örnekleri</span><span class="sxs-lookup"><span data-stu-id="41c23-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="41c23-292">Gelişmiş Analytics işlemi ve ortak veri kümeleri kullanarak teknolojisi kullanan uçtan uca Azure Machine Learning talimatlar için bkz:</span><span class="sxs-lookup"><span data-stu-id="41c23-292">For end-to-end Azure Machine Learning walkthroughs that employ the Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="41c23-293">[Veri bilimi işlemi eylemde ekip: SQL Server'ı kullanarak](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="41c23-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>
* <span data-ttu-id="41c23-294">[Veri bilimi işlemi eylemde ekip: Hdınsight Hadoop kümeleri kullanarak](machine-learning-data-science-process-hive-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="41c23-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
