---
title: "Azure Machine Learning için Gelişmiş analitik senaryoları aaaIdentify | Microsoft Docs"
description: "Merhaba uygun senaryolar hello takım veri bilimi işlemi ile Tahmine dayalı analiz Gelişmiş yapmak için seçin."
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
ms.openlocfilehash: 52c6bb10d6df4f640a4f66cf17cf4993cc1067b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="39041-103">Azure Machine Learning’de gelişmiş analiz senaryoları</span><span class="sxs-lookup"><span data-stu-id="39041-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="39041-104">Bu makalede hello birçok örnek veri kaynakları ve hello tarafından işlenebilir hedef senaryoları özetlenmektedir [takım veri bilimi işlem (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="39041-104">This article outlines hello variety of sample data sources and target scenarios that can be handled by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span> <span data-ttu-id="39041-105">Merhaba TDSP akıllı uygulamaları derleme üzerinde takımlar toocollaborate sistematik bir yaklaşım sağlar.</span><span class="sxs-lookup"><span data-stu-id="39041-105">hello TDSP provides a systematic approach for teams toocollaborate on building intelligent applications.</span></span> <span data-ttu-id="39041-106">Burada sunulan hello senaryoları hello veri özellikleri, kaynak konumları ve Azure hedef depoları bağlıdır hello veri işleme iş akışında kullanılabilir seçenekler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="39041-106">hello scenarios presented here illustrate options available in hello data processing workflow that depend on hello data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="39041-107">Merhaba **karar ağacı** hello son bölümde sunulan veri ve hedefi için uygun hello Örnek senaryo seçmek için.</span><span class="sxs-lookup"><span data-stu-id="39041-107">hello **decision tree** for selecting hello sample scenarios that is appropriate for your data and objective is presented in hello last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="39041-108">Hello bölümleri aşağıdaki her bir örnek senaryo sunar.</span><span class="sxs-lookup"><span data-stu-id="39041-108">Each of hello following sections presents a sample scenario.</span></span> <span data-ttu-id="39041-109">Her senaryo, olası veri bilimi veya gelişmiş analizler için akışı ve Azure kaynaklarını destekleyen listelenir.</span><span class="sxs-lookup"><span data-stu-id="39041-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="39041-110">**Tüm senaryoları aşağıdaki hello için şunları yapmanız gerekir:**
> </span><span class="sxs-lookup"><span data-stu-id="39041-110">**For all of hello following scenarios, you need to:**
</span></span><br/>
> 
> * <span data-ttu-id="39041-111">[Depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md)
>   </span><span class="sxs-lookup"><span data-stu-id="39041-111">[Create a storage account](../storage/common/storage-create-storage-account.md)
</span></span><br/>
> * [<span data-ttu-id="39041-112">Bir Azure Machine Learning çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="39041-112">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
> 
> 

## <span data-ttu-id="39041-113"><a name="smalllocal"></a>Senaryo \#1: küçük toomedium tablo yerel bir dosya kümesinde</span><span class="sxs-lookup"><span data-stu-id="39041-113"><a name="smalllocal"></a>Scenario \#1: Small toomedium tabular dataset in a local files</span></span>
![Küçük toomedium yerel dosyaları][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="39041-115">Ek Azure kaynaklarını: yok</span><span class="sxs-lookup"><span data-stu-id="39041-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="39041-116">İçinde toohello oturum [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="39041-116">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="39041-117">Bir veri kümesi karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="39041-117">Upload a dataset.</span></span>
3. <span data-ttu-id="39041-118">Karşıya yüklenen veri kümeleri ile başlayan bir Azure Machine Learning deneme akışı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39041-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <span data-ttu-id="39041-119"><a name="smalllocalprocess"></a>Senaryo \#2: küçük toomedium dataset işleme gerektiren yerel dosyaları</span><span class="sxs-lookup"><span data-stu-id="39041-119"><a name="smalllocalprocess"></a>Scenario \#2: Small toomedium dataset of local files that require processing</span></span>
![Küçük toomedium yerel dosyaları işleme ile][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="39041-121">Ek Azure kaynaklarını: Azure sanal makinesi (IPython not defteri sunucusu)</span><span class="sxs-lookup"><span data-stu-id="39041-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="39041-122">IPython dizüstü çalıştıran bir Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39041-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="39041-123">Veri tooan Azure depolama kapsayıcısı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="39041-123">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="39041-124">Önceden işleyebilir ve verileri Azure depolama kapsayıcıdan verilere IPython not defterinde Temizle.</span><span class="sxs-lookup"><span data-stu-id="39041-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
4. <span data-ttu-id="39041-125">Veri toocleaned, Tablo formunda dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="39041-125">Transform data toocleaned, tabular form.</span></span>
5. <span data-ttu-id="39041-126">Dönüştürülen veriler Azure BLOB'ları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="39041-126">Save transformed data in Azure blobs.</span></span>
6. <span data-ttu-id="39041-127">İçinde toohello oturum [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="39041-127">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
7. <span data-ttu-id="39041-128">Hello kullanarak Azure bloblarından Hello veri okuma [veri içeri aktarma] [ import-data] modülü.</span><span class="sxs-lookup"><span data-stu-id="39041-128">Read hello data from Azure blobs using hello [Import Data][import-data] module.</span></span>
8. <span data-ttu-id="39041-129">Alınan veri kümeleri ile başlayan bir Azure Machine Learning deneme akışı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39041-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="39041-130"><a name="largelocal"></a>Senaryo \#3: büyük veri kümesi yerel dosyaların Azure BLOB'ları hedefleme</span><span class="sxs-lookup"><span data-stu-id="39041-130"><a name="largelocal"></a>Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![Büyük yerel dosyaları][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="39041-132">Ek Azure kaynaklarını: Azure sanal makinesi (IPython not defteri sunucusu)</span><span class="sxs-lookup"><span data-stu-id="39041-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="39041-133">IPython dizüstü çalıştıran bir Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39041-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="39041-134">Veri tooan Azure depolama kapsayıcısı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="39041-134">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="39041-135">Önceden işleyebilir ve IPython Azure bloblarından verilere dizüstü bilgisayar, veri temizleme.</span><span class="sxs-lookup"><span data-stu-id="39041-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
4. <span data-ttu-id="39041-136">Veri toocleaned, Tablo formunda, gerekirse dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="39041-136">Transform data toocleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="39041-137">Verileri araştırmak ve Özellikler gerektiği şekilde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39041-137">Explore data, and create features as needed.</span></span>
6. <span data-ttu-id="39041-138">Küçük ve orta veri örneği ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="39041-138">Extract a small-to-medium data sample.</span></span>
7. <span data-ttu-id="39041-139">Merhaba örneklenen verileri Azure BLOB'ları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="39041-139">Save hello sampled data in Azure blobs.</span></span>
8. <span data-ttu-id="39041-140">İçinde toohello oturum [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="39041-140">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="39041-141">Hello kullanarak Azure bloblarından Hello veri okuma [veri içeri aktarma] [ import-data] modülü.</span><span class="sxs-lookup"><span data-stu-id="39041-141">Read hello data from Azure blobs using hello [Import Data][import-data] module.</span></span>
10. <span data-ttu-id="39041-142">Alınan veri kümeleri ile başlayan Azure Machine Learning deneme akış oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39041-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="39041-143"><a name="smalllocaltodb"></a>Senaryo \#4: küçük toomedium dataset yerel dosyaları, SQL Server içinde bir Azure sanal makine hedefleme</span><span class="sxs-lookup"><span data-stu-id="39041-143"><a name="smalllocaltodb"></a>Scenario \#4: Small toomedium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![Azure'da küçük toomedium yerel dosyaları tooSQL DB][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="39041-145">Ek Azure kaynaklarını: Azure sanal makinesi (SQL Server / IPython dizüstü sunucu)</span><span class="sxs-lookup"><span data-stu-id="39041-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="39041-146">SQL Server + IPython dizüstü çalıştıran bir Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39041-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
2. <span data-ttu-id="39041-147">Veri tooan Azure depolama kapsayıcısı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="39041-147">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="39041-148">Önceden işleyebilir ve IPython Not Defteri kullanarak Azure depolama kapsayıcısının verileri temizleyin.</span><span class="sxs-lookup"><span data-stu-id="39041-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
4. <span data-ttu-id="39041-149">Veri toocleaned, Tablo formunda, gerekirse dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="39041-149">Transform data toocleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="39041-150">Veri tooVM yerel dosyaları kaydetme (IPython dizüstü bilgisayar, VM üzerinde çalıştığından, yerel sürücülere tooVM sürücüleri bakın).</span><span class="sxs-lookup"><span data-stu-id="39041-150">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
6. <span data-ttu-id="39041-151">Bir Azure VM'de çalıştırılan veri tooSQL sunucu veritabanı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="39041-151">Load data tooSQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="39041-152">Seçenek \#1: SQL Server Management Studio'yu kullanarak.</span><span class="sxs-lookup"><span data-stu-id="39041-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="39041-153">Oturum açma tooSQL Server VM</span><span class="sxs-lookup"><span data-stu-id="39041-153">Login tooSQL Server VM</span></span>
   * <span data-ttu-id="39041-154">SQL Server Management Studio'yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="39041-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="39041-155">Veritabanı ve hedef tablolar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39041-155">Create database and target tables.</span></span>
   * <span data-ttu-id="39041-156">Merhaba toplu birini kullanın yöntemleri tooload hello veri VM yerel dosyalarından içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="39041-156">Use one of hello bulk import methods tooload hello data from VM-local files.</span></span>
   
   <span data-ttu-id="39041-157">Seçenek \#2: kullanarak IPython not defteri – Orta ve büyük veri kümeleri için değil önerilir</span><span class="sxs-lookup"><span data-stu-id="39041-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="39041-158">ODBC bağlantı dizesi tooaccess SQL Server VM üzerinde kullanın.</span><span class="sxs-lookup"><span data-stu-id="39041-158">Use ODBC connection string tooaccess SQL Server on VM.</span></span>
   * <span data-ttu-id="39041-159">Veritabanı ve hedef tablolar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39041-159">Create database and target tables.</span></span>
   * <span data-ttu-id="39041-160">Merhaba toplu birini kullanın yöntemleri tooload hello veri VM yerel dosyalarından içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="39041-160">Use one of hello bulk import methods tooload hello data from VM-local files.</span></span>
7. <span data-ttu-id="39041-161">Özellikler gerektiği şekilde oluşturun, verileri keşfedin.</span><span class="sxs-lookup"><span data-stu-id="39041-161">Explore data, create features as needed.</span></span> <span data-ttu-id="39041-162">Merhaba özellikleri hello veritabanı tablolarında gerçekleştirilip toobe gerekmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="39041-162">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="39041-163">Yalnızca hello gerekli sorgu toocreate Not bunları.</span><span class="sxs-lookup"><span data-stu-id="39041-163">Only note hello necessary query toocreate them.</span></span>
8. <span data-ttu-id="39041-164">Gerekli ve/veya istenen veri örnek boyutu üzerinde karar.</span><span class="sxs-lookup"><span data-stu-id="39041-164">Decide on a data sample size, if needed and/or desired.</span></span>
9. <span data-ttu-id="39041-165">İçinde toohello oturum [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="39041-165">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
10. <span data-ttu-id="39041-166">Okuma hello verileri doğrudan gelen hello hello kullanarak SQL Server [veri içeri aktarma] [ import-data] modülü.</span><span class="sxs-lookup"><span data-stu-id="39041-166">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="39041-167">Alanlar, ayıklayan Yapıştır hello gerekli sorgu özellikleri oluşturur ve veri doğrudan hello gerekirse örnekleri [veri içeri aktarma] [ import-data] sorgu.</span><span class="sxs-lookup"><span data-stu-id="39041-167">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
11. <span data-ttu-id="39041-168">Alınan veri kümeleri ile başlayan Azure Machine Learning deneme akış oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39041-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="39041-169"><a name="largelocaltodb"></a>Senaryo \#5: yerel dosyaları büyük bir veri kümesini hedef Azure VM'deki SQL Server</span><span class="sxs-lookup"><span data-stu-id="39041-169"><a name="largelocaltodb"></a>Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![Azure'da büyük yerel dosyaları tooSQL DB][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="39041-171">Ek Azure kaynaklarını: Azure sanal makinesi (SQL Server / IPython dizüstü sunucu)</span><span class="sxs-lookup"><span data-stu-id="39041-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="39041-172">SQL Server ve IPython dizüstü server çalıştıran bir Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39041-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="39041-173">Veri tooan Azure depolama kapsayıcısı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="39041-173">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="39041-174">(İsteğe bağlı) Önceden işleyebilir ve veri temizleme.</span><span class="sxs-lookup"><span data-stu-id="39041-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="39041-175">a.</span><span class="sxs-lookup"><span data-stu-id="39041-175">a.</span></span>  <span data-ttu-id="39041-176">Önceden işleyebilir ve IPython Azure'dan verilere dizüstü bilgisayar, veri temizleme</span><span class="sxs-lookup"><span data-stu-id="39041-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="39041-177">b.</span><span class="sxs-lookup"><span data-stu-id="39041-177">b.</span></span>  <span data-ttu-id="39041-178">Veri toocleaned, Tablo formunda, gerekirse dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="39041-178">Transform data toocleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="39041-179">c.</span><span class="sxs-lookup"><span data-stu-id="39041-179">c.</span></span>  <span data-ttu-id="39041-180">Veri tooVM yerel dosyaları kaydetme (IPython dizüstü bilgisayar, VM üzerinde çalıştığından, yerel sürücülere tooVM sürücüleri bakın).</span><span class="sxs-lookup"><span data-stu-id="39041-180">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
4. <span data-ttu-id="39041-181">Bir Azure VM'de çalıştırılan veri tooSQL sunucu veritabanı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="39041-181">Load data tooSQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="39041-182">a.</span><span class="sxs-lookup"><span data-stu-id="39041-182">a.</span></span>  <span data-ttu-id="39041-183">Oturum açma tooSQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="39041-183">Login tooSQL Server VM.</span></span>
   
   <span data-ttu-id="39041-184">b.</span><span class="sxs-lookup"><span data-stu-id="39041-184">b.</span></span>  <span data-ttu-id="39041-185">Veri zaten kaydedilmemişse, veri dosyalarını Azure'dan indirir.</span><span class="sxs-lookup"><span data-stu-id="39041-185">If data not saved already, download data files from Azure</span></span>
   
       storage container toolocal-VM folder.
   
   <span data-ttu-id="39041-186">c.</span><span class="sxs-lookup"><span data-stu-id="39041-186">c.</span></span>  <span data-ttu-id="39041-187">SQL Server Management Studio'yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="39041-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="39041-188">d.</span><span class="sxs-lookup"><span data-stu-id="39041-188">d.</span></span>  <span data-ttu-id="39041-189">Veritabanı ve hedef tablolar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39041-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="39041-190">e.</span><span class="sxs-lookup"><span data-stu-id="39041-190">e.</span></span>  <span data-ttu-id="39041-191">Merhaba toplu birini kullanın yöntemleri tooload hello veri içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="39041-191">Use one of hello bulk import methods tooload hello data.</span></span>
   
   <span data-ttu-id="39041-192">f.</span><span class="sxs-lookup"><span data-stu-id="39041-192">f.</span></span>  <span data-ttu-id="39041-193">Tablo birleştirme gerekirse, dizinleri tooexpedite birleştirmeler oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="39041-193">If table joins are required, create indexes tooexpedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="39041-194">Büyük veri boyutları hızlı yükleme için bölümlenmiş tabloları oluşturma ve içeri aktarma hello verilerini paralel toplu önerilir.</span><span class="sxs-lookup"><span data-stu-id="39041-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import hello data in parallel.</span></span> <span data-ttu-id="39041-195">Daha fazla bilgi için bkz: [paralel veri alma tooSQL bölümlenmiş tabloları](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="39041-195">For more information, see [Parallel Data Import tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="39041-196">Özellikler gerektiği şekilde oluşturun, verileri keşfedin.</span><span class="sxs-lookup"><span data-stu-id="39041-196">Explore data, create features as needed.</span></span> <span data-ttu-id="39041-197">Merhaba özellikleri hello veritabanı tablolarında gerçekleştirilip toobe gerekmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="39041-197">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="39041-198">Yalnızca hello gerekli sorgu toocreate Not bunları.</span><span class="sxs-lookup"><span data-stu-id="39041-198">Only note hello necessary query toocreate them.</span></span>
6. <span data-ttu-id="39041-199">Gerekli ve/veya istenen veri örnek boyutu üzerinde karar.</span><span class="sxs-lookup"><span data-stu-id="39041-199">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="39041-200">İçinde toohello oturum [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="39041-200">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="39041-201">Okuma hello verileri doğrudan gelen hello hello kullanarak SQL Server [veri içeri aktarma] [ import-data] modülü.</span><span class="sxs-lookup"><span data-stu-id="39041-201">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="39041-202">Alanlar, ayıklayan Yapıştır hello gerekli sorgu özellikleri oluşturur ve veri doğrudan hello gerekirse örnekleri [veri içeri aktarma] [ import-data] sorgu.</span><span class="sxs-lookup"><span data-stu-id="39041-202">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="39041-203">Karşıya yüklenen veri kümesi ile başlayan basit Azure Machine Learning deneme akışı</span><span class="sxs-lookup"><span data-stu-id="39041-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <span data-ttu-id="39041-204"><a name="largedbtodb"></a>Senaryo \#6: bir SQL Server veritabanı SQL Server içinde bir Azure sanal makine hedefleme şirket içi, büyük bir veri kümesini</span><span class="sxs-lookup"><span data-stu-id="39041-204"><a name="largedbtodb"></a>Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![Azure'da büyük SQL DB şirket içi tooSQL DB][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="39041-206">Ek Azure kaynaklarını: Azure sanal makinesi (SQL Server / IPython dizüstü sunucu)</span><span class="sxs-lookup"><span data-stu-id="39041-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="39041-207">SQL Server ve IPython dizüstü server çalıştıran bir Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39041-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="39041-208">Merhaba veri birini kullanın, SQL Server toodump dosyalarından yöntemleri tooexport hello veri verin.</span><span class="sxs-lookup"><span data-stu-id="39041-208">Use one of hello data export methods tooexport hello data from SQL Server toodump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="39041-209">Merhaba şirket içi veritabanındaki bir alternatif (hızlı) yöntemi toomove hello tam veritabanı toothe SQL Server örneğinde Azure tüm verileri toomove karar verirseniz.</span><span class="sxs-lookup"><span data-stu-id="39041-209">If you decide toomove all data from hello on-prem database, an alternate (faster) method toomove hello full database toothe SQL Server instance in Azure.</span></span> <span data-ttu-id="39041-210">Merhaba adımları tooexport verileri atlayabilirsiniz, veritabanı ve yük/içe aktarma veri toohello hedef veritabanı oluşturun ve hello Alternatif yöntem izleyin.</span><span class="sxs-lookup"><span data-stu-id="39041-210">Skip hello steps tooexport data, create database, and load/import data toohello target database and follow hello alternate method.</span></span>
   > 
   > 
3. <span data-ttu-id="39041-211">Döküm dosyaları tooAzure depolama kapsayıcısı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="39041-211">Upload dump files tooAzure storage container.</span></span>
4. <span data-ttu-id="39041-212">Bir Azure sanal makinede çalışan yük hello veri tooa SQL Server veritabanı.</span><span class="sxs-lookup"><span data-stu-id="39041-212">Load hello data tooa SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="39041-213">a.</span><span class="sxs-lookup"><span data-stu-id="39041-213">a.</span></span>  <span data-ttu-id="39041-214">Oturum açma toohello SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="39041-214">Login toohello SQL Server VM.</span></span>
   
   <span data-ttu-id="39041-215">b.</span><span class="sxs-lookup"><span data-stu-id="39041-215">b.</span></span>  <span data-ttu-id="39041-216">Veri dosyaları bir Azure depolama kapsayıcısı toohello yerel VM klasöründen yükleyin.</span><span class="sxs-lookup"><span data-stu-id="39041-216">Download data files from an Azure storage container toohello local-VM folder.</span></span>
   
   <span data-ttu-id="39041-217">c.</span><span class="sxs-lookup"><span data-stu-id="39041-217">c.</span></span>  <span data-ttu-id="39041-218">SQL Server Management Studio'yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="39041-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="39041-219">d.</span><span class="sxs-lookup"><span data-stu-id="39041-219">d.</span></span>  <span data-ttu-id="39041-220">Veritabanı ve hedef tablolar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39041-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="39041-221">e.</span><span class="sxs-lookup"><span data-stu-id="39041-221">e.</span></span>  <span data-ttu-id="39041-222">Merhaba toplu birini kullanın yöntemleri tooload hello veri içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="39041-222">Use one of hello bulk import methods tooload hello data.</span></span>
   
   <span data-ttu-id="39041-223">f.</span><span class="sxs-lookup"><span data-stu-id="39041-223">f.</span></span>  <span data-ttu-id="39041-224">Tablo birleştirme gerekirse, dizinleri tooexpedite birleştirmeler oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="39041-224">If table joins are required, create indexes tooexpedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="39041-225">Büyük veri boyutları hızlı yükleme için bölümlenmiş tablolar ve toobulk alma hello verileri paralel olarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39041-225">For faster loading of large data sizes, create partitioned tables and toobulk import hello data in parallel.</span></span> <span data-ttu-id="39041-226">Daha fazla bilgi için bkz: [paralel veri alma tooSQL bölümlenmiş tabloları](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="39041-226">For more information, see [Parallel Data Import tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="39041-227">Özellikler gerektiği şekilde oluşturun, verileri keşfedin.</span><span class="sxs-lookup"><span data-stu-id="39041-227">Explore data, create features as needed.</span></span> <span data-ttu-id="39041-228">Merhaba özellikleri hello veritabanı tablolarında gerçekleştirilip toobe gerekmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="39041-228">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="39041-229">Yalnızca hello gerekli sorgu toocreate Not bunları.</span><span class="sxs-lookup"><span data-stu-id="39041-229">Only note hello necessary query toocreate them.</span></span>
6. <span data-ttu-id="39041-230">Gerekli ve/veya istenen veri örnek boyutu üzerinde karar.</span><span class="sxs-lookup"><span data-stu-id="39041-230">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="39041-231">İçinde toohello oturum [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="39041-231">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="39041-232">Okuma hello verileri doğrudan gelen hello hello kullanarak SQL Server [veri içeri aktarma] [ import-data] modülü.</span><span class="sxs-lookup"><span data-stu-id="39041-232">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="39041-233">Alanlar, ayıklayan Yapıştır hello gerekli sorgu özellikleri oluşturur ve veri doğrudan hello gerekirse örnekleri [veri içeri aktarma] [ import-data] sorgu.</span><span class="sxs-lookup"><span data-stu-id="39041-233">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="39041-234">Basit Azure Machine Learning ile karşıya yüklenen dataset başlangıç akışı deneyin.</span><span class="sxs-lookup"><span data-stu-id="39041-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-toocopy-a-full-database-from-an-on-premises--sql-server-tooazure-sql-database"></a><span data-ttu-id="39041-235">Alternatif yöntem toocopy bir şirket içi SQL Server tooAzure SQL veritabanını tam bir veritabanından</span><span class="sxs-lookup"><span data-stu-id="39041-235">Alternate method toocopy a full database from an on-premises  SQL Server tooAzure SQL Database</span></span>
![Yerel DB detach ve Azure DB tooSQL ekleme][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="39041-237">Ek Azure kaynaklarını: Azure sanal makinesi (SQL Server / IPython dizüstü sunucu)</span><span class="sxs-lookup"><span data-stu-id="39041-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="39041-238">tooreplicate hello tüm SQL Server veritabanında SQL Server VM'nize hello veritabanı geçici olarak çevrimdışı duruma getirilebilen varsayarak bir veritabanı bir konum/sunucu tooanother kopyalamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="39041-238">tooreplicate hello entire SQL Server database in your SQL Server VM, you should copy a database from one location/server tooanother, assuming that hello database can be taken temporarily offline.</span></span> <span data-ttu-id="39041-239">Bu SQL Server Management Studio Object Explorer hello veya hello eşdeğer Transact-SQL komutlarını kullanarak yapın.</span><span class="sxs-lookup"><span data-stu-id="39041-239">You do this in hello SQL Server Management Studio Object Explorer, or using hello equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="39041-240">Merhaba kaynak konumda Hello veritabanı ayrılmadı.</span><span class="sxs-lookup"><span data-stu-id="39041-240">Detach hello database at hello source location.</span></span> <span data-ttu-id="39041-241">Daha fazla bilgi için bkz: [bir veritabanını ayırma](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="39041-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
2. <span data-ttu-id="39041-242">Windows Gezgini veya Windows komut istemi penceresinde, veritabanı dosyası veya dosya ve günlük dosyası veya dosyaları toohello hedef konumu'hello Azure'nın SQL Server VM üzerinde kopyalama hello ayrıldı.</span><span class="sxs-lookup"><span data-stu-id="39041-242">In Windows Explorer or Windows Command Prompt window, copy hello detached database file or files and log file or files toohello target location on hello SQL Server VM in Azure.</span></span>
3. <span data-ttu-id="39041-243">Kopyalanan hello dosyaları toohello hedef SQL Server örneği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="39041-243">Attach hello copied files toohello target SQL Server instance.</span></span> <span data-ttu-id="39041-244">Daha fazla bilgi için bkz: [bir veritabanını](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="39041-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="39041-245">[Kullanarak bir veritabanı ayırma ve (Transact-SQL) ekleme taşıma](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="39041-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <span data-ttu-id="39041-246"><a name="largedbtohive"></a>Senaryo \#7: yerel dosyalarında büyük veri hedef Azure Hdınsight Hadoop kümeleri Hive veritabanında</span><span class="sxs-lookup"><span data-stu-id="39041-246"><a name="largedbtohive"></a>Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![Yerel hedef Hive büyük verileri][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="39041-248">Ek Azure kaynaklarını: Azure Hdınsight Hadoop kümesi ve Azure sanal makine (IPython not defteri sunucusu)</span><span class="sxs-lookup"><span data-stu-id="39041-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="39041-249">IPython dizüstü server çalıştıran bir Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39041-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
2. <span data-ttu-id="39041-250">Bir Azure Hdınsight Hadoop kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39041-250">Create an Azure HDInsight Hadoop cluster.</span></span>
3. <span data-ttu-id="39041-251">(İsteğe bağlı) Önceden işleyebilir ve veri temizleme.</span><span class="sxs-lookup"><span data-stu-id="39041-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="39041-252">a.</span><span class="sxs-lookup"><span data-stu-id="39041-252">a.</span></span>  <span data-ttu-id="39041-253">Önceden işleyebilir ve IPython Azure'dan verilere dizüstü bilgisayar, veri temizleme</span><span class="sxs-lookup"><span data-stu-id="39041-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="39041-254">b.</span><span class="sxs-lookup"><span data-stu-id="39041-254">b.</span></span>  <span data-ttu-id="39041-255">Veri toocleaned, Tablo formunda, gerekirse dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="39041-255">Transform data toocleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="39041-256">c.</span><span class="sxs-lookup"><span data-stu-id="39041-256">c.</span></span>  <span data-ttu-id="39041-257">Veri tooVM yerel dosyaları kaydetme (IPython dizüstü bilgisayar, VM üzerinde çalıştığından, yerel sürücülere tooVM sürücüleri bakın).</span><span class="sxs-lookup"><span data-stu-id="39041-257">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
4. <span data-ttu-id="39041-258">Veri toohello varsayılan kapsayıcı hello adım 2 seçili hello Hadoop kümesi karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="39041-258">Upload data toohello default container of hello Hadoop cluster selected in hello step 2.</span></span>
5. <span data-ttu-id="39041-259">Azure Hdınsight Hadoop kümesindeki verileri tooHive veritabanı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="39041-259">Load data tooHive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="39041-260">a.</span><span class="sxs-lookup"><span data-stu-id="39041-260">a.</span></span>  <span data-ttu-id="39041-261">Toohello baş hello Hadoop küme düğümünde oturum</span><span class="sxs-lookup"><span data-stu-id="39041-261">Log in toohello head node of hello Hadoop cluster</span></span>
   
   <span data-ttu-id="39041-262">b.</span><span class="sxs-lookup"><span data-stu-id="39041-262">b.</span></span>  <span data-ttu-id="39041-263">Merhaba Hadoop komut satırı açın.</span><span class="sxs-lookup"><span data-stu-id="39041-263">Open hello Hadoop Command Line.</span></span>
   
   <span data-ttu-id="39041-264">c.</span><span class="sxs-lookup"><span data-stu-id="39041-264">c.</span></span>  <span data-ttu-id="39041-265">Komutu tarafından Hello Hive kök dizini girin `cd %hive_home%\bin` , Hadoop komut satırı.</span><span class="sxs-lookup"><span data-stu-id="39041-265">Enter hello Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="39041-266">d.</span><span class="sxs-lookup"><span data-stu-id="39041-266">d.</span></span>  <span data-ttu-id="39041-267">Merhaba Hive sorguları toocreate veritabanı ve tablo çalıştırın ve blob depolama tooHive tablolarından veri yükleme.</span><span class="sxs-lookup"><span data-stu-id="39041-267">Run hello Hive queries toocreate database and tables, and load data from blob storage tooHive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="39041-268">Merhaba veri büyük ise, kullanıcıların bölümlerle hello Hive tablosu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="39041-268">If hello data is big, users can create hello Hive table with partitions.</span></span> <span data-ttu-id="39041-269">Kullanıcılar daha sonra kullanabileceğiniz bir `for` hello Hadoop komut satırı hello baş düğüm tooload verileri hello Hive tablosu tarafından bölüm bölümlenmiş bir döngüde.</span><span class="sxs-lookup"><span data-stu-id="39041-269">Then, users can use a `for` loop in hello Hadoop Command Line on hello head node tooload data into hello Hive table partitioned by partition.</span></span>
   > 
   > 
6. <span data-ttu-id="39041-270">Verileri araştırmak ve özellikleri Hadoop komut satırında gerektiği şekilde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39041-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="39041-271">Merhaba özellikleri hello veritabanı tablolarında gerçekleştirilip toobe gerekmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="39041-271">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="39041-272">Yalnızca hello gerekli sorgu toocreate Not bunları.</span><span class="sxs-lookup"><span data-stu-id="39041-272">Only note hello necessary query toocreate them.</span></span>
   
   <span data-ttu-id="39041-273">a.</span><span class="sxs-lookup"><span data-stu-id="39041-273">a.</span></span>  <span data-ttu-id="39041-274">Toohello baş hello Hadoop küme düğümünde oturum</span><span class="sxs-lookup"><span data-stu-id="39041-274">Log in toohello head node of hello Hadoop cluster</span></span>
   
   <span data-ttu-id="39041-275">b.</span><span class="sxs-lookup"><span data-stu-id="39041-275">b.</span></span>  <span data-ttu-id="39041-276">Merhaba Hadoop komut satırı açın.</span><span class="sxs-lookup"><span data-stu-id="39041-276">Open hello Hadoop Command Line.</span></span>
   
   <span data-ttu-id="39041-277">c.</span><span class="sxs-lookup"><span data-stu-id="39041-277">c.</span></span>  <span data-ttu-id="39041-278">Komutu tarafından Hello Hive kök dizini girin `cd %hive_home%\bin` , Hadoop komut satırı.</span><span class="sxs-lookup"><span data-stu-id="39041-278">Enter hello Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="39041-279">d.</span><span class="sxs-lookup"><span data-stu-id="39041-279">d.</span></span>  <span data-ttu-id="39041-280">Merhaba Hive sorguları Hadoop komut satırında hello baş hello Hadoop küme tooexplore hello verileri düğümde çalıştırın ve gerektiği gibi özellikleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39041-280">Run hello Hive queries in Hadoop Command Line on hello head node of hello Hadoop cluster tooexplore hello data and create features as needed.</span></span>
7. <span data-ttu-id="39041-281">Gerekli ve/veya istenen, Azure Machine Learning Studio'da hello veri toofit örnek.</span><span class="sxs-lookup"><span data-stu-id="39041-281">If needed and/or desired, sample hello data toofit in Azure Machine Learning Studio.</span></span>
8. <span data-ttu-id="39041-282">İçinde toohello oturum [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="39041-282">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="39041-283">Doğrudan hello Hello veri okuma `Hive Queries` hello kullanarak [veri içeri aktarma] [ import-data] modülü.</span><span class="sxs-lookup"><span data-stu-id="39041-283">Read hello data directly from hello `Hive Queries` using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="39041-284">Alanlar, ayıklayan Yapıştır hello gerekli sorgu özellikleri oluşturur ve veri doğrudan hello gerekirse örnekleri [veri içeri aktarma] [ import-data] sorgu.</span><span class="sxs-lookup"><span data-stu-id="39041-284">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
10. <span data-ttu-id="39041-285">Basit Azure Machine Learning ile karşıya yüklenen dataset başlangıç akışı deneyin.</span><span class="sxs-lookup"><span data-stu-id="39041-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <span data-ttu-id="39041-286"><a name="decisiontree"></a>Senaryo seçimi için karar ağacı</span><span class="sxs-lookup"><span data-stu-id="39041-286"><a name="decisiontree"></a>Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="39041-287">Merhaba Aşağıdaki diyagramda yukarıda açıklanan hello senaryoları ve tooeach dökümü hello senaryoların atmanız yapılan hello Advanced Analytics işlemi ve teknoloji seçimler özetler.</span><span class="sxs-lookup"><span data-stu-id="39041-287">hello following diagram summarizes hello scenarios described above and hello Advanced Analytics Process and Technology choices made that take you tooeach of hello itemized scenarios.</span></span> <span data-ttu-id="39041-288">Veri işleme, keşfi, özellik Mühendisliği ve örnekleme alabileceğini unutmayın, bir veya daha fazla yöntem/ortam--kaynaktaki Merhaba, Ara, ve/veya hedef ortamları – içinde yerleştirin ve gerektiğinde tekrarlayarak devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="39041-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at hello source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="39041-289">Merhaba diyagram yalnızca bazı olası akışlarının çizim görev yapar ve kapsamlı bir numaralandırma sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="39041-289">hello diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![DS işlemi izlenecek senaryolar][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="39041-291">Gelişmiş analizler eylem örnekleri</span><span class="sxs-lookup"><span data-stu-id="39041-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="39041-292">Ortak veri kümeleri kullanarak, kullanan uçtan uca Azure Machine Learning izlenecek yollar için Gelişmiş analiz işlem ve teknoloji Merhaba, bkz:</span><span class="sxs-lookup"><span data-stu-id="39041-292">For end-to-end Azure Machine Learning walkthroughs that employ hello Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="39041-293">[Veri bilimi işlemi eylemde ekip: SQL Server'ı kullanarak](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="39041-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>
* <span data-ttu-id="39041-294">[Veri bilimi işlemi eylemde ekip: Hdınsight Hadoop kümeleri kullanarak](machine-learning-data-science-process-hive-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="39041-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span></span>

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
