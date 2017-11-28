---
title: "aaaMigrate, veri ambarı veri tooSQL | Microsoft Docs"
description: "Çözümleri geliştirmek için SQL veri ambarı veri tooAzure geçirmek için ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: d78f954a-f54c-4aa4-9040-919bc6414887
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/29/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: fe4c6b7e82094c59c45e06be6da225fee1b707ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data"></a><span data-ttu-id="06e4e-103">Verilerinizi geçirme</span><span class="sxs-lookup"><span data-stu-id="06e4e-103">Migrate Your Data</span></span>
<span data-ttu-id="06e4e-104">Veri çeşitli araçları ile SQL veri ambarında farklı kaynaklardan yeniden taşınabilir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span></span>  <span data-ttu-id="06e4e-105">ADF kopyalama, SSIS ve tüm bu hedef kullanılan tooachieve olarak bcp olabilir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-105">ADF Copy, SSIS, and bcp can all be used tooachieve this goal.</span></span> <span data-ttu-id="06e4e-106">Ancak, Hello veri miktarı arttıkça hello veri geçiş işlemi adımlara bölmek hakkında düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="06e4e-106">However, as hello amount of data increases you should think about breaking down hello data migration process into steps.</span></span> <span data-ttu-id="06e4e-107">Bu, ortaya koymaktadır her adım performans ve esneklik tooensure kesintisiz veri geçişi için Fırsat toooptimize hello.</span><span class="sxs-lookup"><span data-stu-id="06e4e-107">This affords you hello opportunity toooptimize each step both for performance and for resilience tooensure a smooth data migration.</span></span>

<span data-ttu-id="06e4e-108">Bu makalede, ilk ADF kopyalama, SSIS ve bcp hello basit geçiş senaryoları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="06e4e-108">This article first discusses hello simple migration scenarios of ADF Copy, SSIS, and bcp.</span></span> <span data-ttu-id="06e4e-109">Ardından, görünüm nasıl hello geçiş iyileştirilebilir içine biraz daha derin.</span><span class="sxs-lookup"><span data-stu-id="06e4e-109">It then look a little deeper into how hello migration can be optimized.</span></span>

## <a name="azure-data-factory-adf-copy"></a><span data-ttu-id="06e4e-110">Azure veri fabrikası (ADF) kopyalama</span><span class="sxs-lookup"><span data-stu-id="06e4e-110">Azure Data Factory (ADF) copy</span></span>
<span data-ttu-id="06e4e-111">[ADF kopyalama] [ ADF Copy] parçası olan [Azure Data Factory][Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="06e4e-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span></span> <span data-ttu-id="06e4e-112">Azure blob depolama alanındaki veya SQL Data Warehouse doğrudan tooremote düz dosyalar tutulan yerel depolama alanında bulunan veri tooflat dosyalarınızı ADF kopyalama tooexport kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06e4e-112">You can use ADF Copy tooexport your data tooflat files residing on local storage, tooremote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span></span>

<span data-ttu-id="06e4e-113">Verilerinizi düz dosyalarda başlatır sonra ilk tootransfer gerekir, yükü başlatmadan önce tooAzure depolama blobu SQL Data Warehouse içine.</span><span class="sxs-lookup"><span data-stu-id="06e4e-113">If your data starts in flat files, then you will first need tootransfer it tooAzure storage blob before initiating a load it into SQL Data Warehouse.</span></span> <span data-ttu-id="06e4e-114">Azure blob depolama alanına aktarılan Hello verileri sonra toouse seçebilirsiniz [ADF kopyalama] [ ADF Copy] yeniden toopush hello verileri SQL veri ambarı.</span><span class="sxs-lookup"><span data-stu-id="06e4e-114">Once hello data is transferred into Azure blob storage you can choose toouse [ADF Copy][ADF Copy] again toopush hello data into SQL Data Warehouse.</span></span>

<span data-ttu-id="06e4e-115">PolyBase aynı zamanda hello veri yükleme için yüksek performanslı seçeneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="06e4e-115">PolyBase also provides a high-performance option for loading hello data.</span></span> <span data-ttu-id="06e4e-116">Ancak, iki tane yerine araçlarla anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="06e4e-116">However, that does mean using two tools instead of one.</span></span> <span data-ttu-id="06e4e-117">PolyBase kullanan yeniden hello en iyi performansı gerekiyor durumunda.</span><span class="sxs-lookup"><span data-stu-id="06e4e-117">If you need hello best performance then use PolyBase.</span></span> <span data-ttu-id="06e4e-118">Bir tek aracı deneyimi istediğiniz (ve hello veri yoğun değil) sonra ADF yanıtınız olur.</span><span class="sxs-lookup"><span data-stu-id="06e4e-118">If you want a single tool experience (and hello data is not massive) then ADF is your answer.</span></span>


> 
> 

<span data-ttu-id="06e4e-119">Makale için bazı harika aşağıdaki toohello üzerinden baş [ADF örnekleri][ADF samples].</span><span class="sxs-lookup"><span data-stu-id="06e4e-119">Head over toohello following article for some great [ADF samples][ADF samples].</span></span>

## <a name="integration-services"></a><span data-ttu-id="06e4e-120">Tümleştirme Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="06e4e-120">Integration Services</span></span>
<span data-ttu-id="06e4e-121">Integration Services (SSIS) karmaşık iş akışları, veri dönüştürme ve birkaç veri yükleme seçeneklerini destekleyen bir güçlü ve esnek ayıklamak dönüştürme ve yükleme (ETL) aracıdır.</span><span class="sxs-lookup"><span data-stu-id="06e4e-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span></span> <span data-ttu-id="06e4e-122">SSIS toosimply aktarımı veri tooAzure kullanın veya daha geniş bir geçişin parçası olarak.</span><span class="sxs-lookup"><span data-stu-id="06e4e-122">Use SSIS toosimply transfer data tooAzure or as part of a broader migration.</span></span>

> [!NOTE]
> <span data-ttu-id="06e4e-123">SSIS tooUTF-8 hello dosyasındaki hello Unicode bayt sırası işareti olmadan dışa aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06e4e-123">SSIS can export tooUTF-8 without hello byte order mark in hello file.</span></span> <span data-ttu-id="06e4e-124">Bu ilk hello kullanmalısınız sütun bileşen tooconvert hello karakter verileri türetilmiş tooconfigure hello veri akışı toouse hello 65001 UTF-8 kod sayfası.</span><span class="sxs-lookup"><span data-stu-id="06e4e-124">tooconfigure this you must first use hello derived column component tooconvert hello character data in hello data flow toouse hello 65001 UTF-8 code page.</span></span> <span data-ttu-id="06e4e-125">Merhaba sütunları dönüştürüldükten sonra hello veri toohello düz dosya hedef bağdaştırıcı 65001 hello hello dosyası için kod sayfası olarak da seçilmiş sağlama yazma.</span><span class="sxs-lookup"><span data-stu-id="06e4e-125">Once hello columns have been converted, write hello data toohello flat file destination adapter ensuring that 65001 has also been selected as hello code page for hello file.</span></span>
> 
> 

<span data-ttu-id="06e4e-126">Yalnızca bu tooa SQL Server dağıtımı bağlandığınız gibi tooSQL veri ambarı SSIS bağlanır.</span><span class="sxs-lookup"><span data-stu-id="06e4e-126">SSIS connects tooSQL Data Warehouse just as it would connect tooa SQL Server deployment.</span></span> <span data-ttu-id="06e4e-127">Ancak, bağlantılarınızı bir ADO.NET Bağlantı Yöneticisi'ni kullanarak toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-127">However, your connections will need toobe using an ADO.NET connection manager.</span></span> <span data-ttu-id="06e4e-128">Ayrıca tooconfigure hello "Kullanım toplu ekleme kullanılabilir olduğunda" ilgilenebilmek ayarı toomaximize işleme.</span><span class="sxs-lookup"><span data-stu-id="06e4e-128">You should also take care tooconfigure hello "Use bulk insert when available" setting toomaximize throughput.</span></span> <span data-ttu-id="06e4e-129">Lütfen toohello bakın [ADO.NET hedef bağdaştırıcı] [ ADO.NET destination adapter] makale toolearn bu özellik hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="06e4e-129">Please refer toohello [ADO.NET destination adapter][ADO.NET destination adapter] article toolearn more about this property</span></span>

> [!NOTE]
> <span data-ttu-id="06e4e-130">OLEDB kullanarak SQL Data Warehouse tooAzure bağlanması desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="06e4e-130">Connecting tooAzure SQL Data Warehouse by using OLEDB is not supported.</span></span>
> 
> 

<span data-ttu-id="06e4e-131">Ayrıca, olduğundan her zaman bir paket başarısız olabilir hello olasılığı toothrottling veya ağ sorunları nedeniyle.</span><span class="sxs-lookup"><span data-stu-id="06e4e-131">In addition, there is always hello possibility that a package might fail due toothrottling or network issues.</span></span> <span data-ttu-id="06e4e-132">Tasarım paketleri bunlar olmadan hatası, hello noktada ettirilebilir şekilde yineleme, iş, hello hatasından önce tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="06e4e-132">Design packages so they can be resumed at hello point of failure, without redoing work that completed before hello failure.</span></span>

<span data-ttu-id="06e4e-133">Daha fazla bilgi için hello başvurun [SSIS belgelerine][SSIS documentation].</span><span class="sxs-lookup"><span data-stu-id="06e4e-133">For more information consult hello [SSIS documentation][SSIS documentation].</span></span>

## <a name="bcp"></a><span data-ttu-id="06e4e-134">bcp</span><span class="sxs-lookup"><span data-stu-id="06e4e-134">bcp</span></span>
<span data-ttu-id="06e4e-135">BCP düz dosya verileri içeri ve dışarı aktarma için tasarlanmış bir komut satırı yardımcı programıdır.</span><span class="sxs-lookup"><span data-stu-id="06e4e-135">bcp is a command-line utility that is designed for flat file data import and export.</span></span> <span data-ttu-id="06e4e-136">Bazı dönüştürme veri dışa aktarma sırasında gerçekleşebilir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-136">Some transformation can take place during data export.</span></span> <span data-ttu-id="06e4e-137">tooperform basit dönüşümleri hello veri dönüştürme ve bir sorgu tooselect kullanın.</span><span class="sxs-lookup"><span data-stu-id="06e4e-137">tooperform simple transformations use a query tooselect and transform hello data.</span></span> <span data-ttu-id="06e4e-138">Dışarı sonra hello düz dosyalar ardından doğrudan hello hedef hello SQL Data Warehouse veritabanına yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-138">Once exported, hello flat files can then be loaded directly into hello target hello SQL Data Warehouse database.</span></span>

> [!NOTE]
> <span data-ttu-id="06e4e-139">Genellikle, hello kaynak sistemde bir görünümdeki verileri sırasında kullanılan dönüşümleri verme iyi bir fikir tooencapsulate hello olur.</span><span class="sxs-lookup"><span data-stu-id="06e4e-139">It is often a good idea tooencapsulate hello transformations used during data export in a view on hello source system.</span></span> <span data-ttu-id="06e4e-140">Bu hello mantığı korunur ve hello işlem tekrarlanabilir sağlar.</span><span class="sxs-lookup"><span data-stu-id="06e4e-140">This ensures that hello logic is retained and hello process is repeatable.</span></span>
> 
> 

<span data-ttu-id="06e4e-141">Bcp avantajları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="06e4e-141">Advantages of bcp are:</span></span>

* <span data-ttu-id="06e4e-142">Basitlik.</span><span class="sxs-lookup"><span data-stu-id="06e4e-142">Simplicity.</span></span> <span data-ttu-id="06e4e-143">BCP komutları basit toobuild olan ve yürütme</span><span class="sxs-lookup"><span data-stu-id="06e4e-143">bcp commands are simple toobuild and execute</span></span>
* <span data-ttu-id="06e4e-144">Yeniden başlatılabilir yükleme işlemi.</span><span class="sxs-lookup"><span data-stu-id="06e4e-144">Re-startable load process.</span></span> <span data-ttu-id="06e4e-145">Bir kez dışarı aktarılan hello yük olabilir kez herhangi bir sayıda yürütülebilir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-145">Once exported hello load can be executed any number of times</span></span>

<span data-ttu-id="06e4e-146">Bcp sınırlamaları vardır:</span><span class="sxs-lookup"><span data-stu-id="06e4e-146">Limitations of bcp are:</span></span>

* <span data-ttu-id="06e4e-147">BCP tabloda düz dosyalarıyla yalnızca çalışır.</span><span class="sxs-lookup"><span data-stu-id="06e4e-147">bcp works with tabulated flat files only.</span></span> <span data-ttu-id="06e4e-148">Xml veya JSON gibi dosyalarla çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="06e4e-148">It does not work with files such as xml or JSON</span></span>
* <span data-ttu-id="06e4e-149">Veri dönüştürme özellikleri yalnızca sınırlı toohello verme aşama ve doğası gereği basit</span><span class="sxs-lookup"><span data-stu-id="06e4e-149">Data transformation capabilities are limited toohello export stage only and are simple in nature</span></span>
* <span data-ttu-id="06e4e-150">Internet üzerinden verileri yükleme hello zaman bcp uyarlanmış toobe sağlam yedeklenmedi.</span><span class="sxs-lookup"><span data-stu-id="06e4e-150">bcp has not been adapted toobe robust when loading data over hello internet.</span></span> <span data-ttu-id="06e4e-151">Ağ kararsızlığa yük hataya neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-151">Any network instability may cause a load error.</span></span>
* <span data-ttu-id="06e4e-152">BCP hello hedef veritabanı önceki toohello yük bulunmasına hello şema kullanır</span><span class="sxs-lookup"><span data-stu-id="06e4e-152">bcp relies on hello schema being present in hello target database prior toohello load</span></span>

<span data-ttu-id="06e4e-153">Daha fazla bilgi için bkz: [bcp tooload verileri SQL Data Warehouse'a kullanmak][Use bcp tooload data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="06e4e-153">For more information, see [Use bcp tooload data into SQL Data Warehouse][Use bcp tooload data into SQL Data Warehouse].</span></span>

## <a name="optimizing-data-migration"></a><span data-ttu-id="06e4e-154">Veri geçişi en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="06e4e-154">Optimizing data migration</span></span>
<span data-ttu-id="06e4e-155">Bir SQLDW veri taşıma işlemi, üç ayrı adımları etkili bir şekilde ayrılabilir:</span><span class="sxs-lookup"><span data-stu-id="06e4e-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span></span>

1. <span data-ttu-id="06e4e-156">Kaynak verileri dışa aktarma</span><span class="sxs-lookup"><span data-stu-id="06e4e-156">Export of source data</span></span>
2. <span data-ttu-id="06e4e-157">Veri tooAzure aktarımını</span><span class="sxs-lookup"><span data-stu-id="06e4e-157">Transfer of data tooAzure</span></span>
3. <span data-ttu-id="06e4e-158">Merhaba hedef SQLDW veritabanına yükleyin</span><span class="sxs-lookup"><span data-stu-id="06e4e-158">Load into hello target SQLDW database</span></span>

<span data-ttu-id="06e4e-159">Her adım tek başına en iyi duruma getirilmiş toocreate her adımı performansı en üst düzeye çıkaran güçlü, yeniden başlatılabilir ve esnek geçiş işlemi olabilir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-159">Each step can be individually optimized toocreate a robust, re-startable and resilient migration process that maximizes performance at each step.</span></span>

## <a name="optimizing-data-load"></a><span data-ttu-id="06e4e-160">En iyi duruma getirme veri yükleme</span><span class="sxs-lookup"><span data-stu-id="06e4e-160">Optimizing data load</span></span>
<span data-ttu-id="06e4e-161">Bu bir süre için ters sırada bakarak; Merhaba en hızlı yolu tooload PolyBase verilerdir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-161">Looking at these in reverse order for a moment; hello fastest way tooload data is via PolyBase.</span></span> <span data-ttu-id="06e4e-162">PolyBase yükleme işlemi için en iyi duruma getirme Önkoşullar en iyi toounderstand olması için bu adımları önceki hello üzerinde ön yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-162">Optimizing for a PolyBase load process places prerequisites on hello preceding steps so it's best toounderstand this upfront.</span></span> <span data-ttu-id="06e4e-163">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="06e4e-163">They are:</span></span>

1. <span data-ttu-id="06e4e-164">Veri dosyaları kodlama</span><span class="sxs-lookup"><span data-stu-id="06e4e-164">Encoding of data files</span></span>
2. <span data-ttu-id="06e4e-165">Veri dosyalarının biçimi</span><span class="sxs-lookup"><span data-stu-id="06e4e-165">Format of data files</span></span>
3. <span data-ttu-id="06e4e-166">Veri dosyalarının konumu</span><span class="sxs-lookup"><span data-stu-id="06e4e-166">Location of data files</span></span>

### <a name="encoding"></a><span data-ttu-id="06e4e-167">Encoding</span><span class="sxs-lookup"><span data-stu-id="06e4e-167">Encoding</span></span>
<span data-ttu-id="06e4e-168">PolyBase, veri dosyalarını toobe UTF-8 veya UTF-16FE gerektirir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-168">PolyBase requires data files toobe UTF-8 or UTF-16FE.</span></span> 



### <a name="format-of-data-files"></a><span data-ttu-id="06e4e-169">Veri dosyalarının biçimi</span><span class="sxs-lookup"><span data-stu-id="06e4e-169">Format of data files</span></span>
<span data-ttu-id="06e4e-170">PolyBase sabit satır Sonlandırıcı \n ya da yeni satır olması zorunlu tutulmuştur.</span><span class="sxs-lookup"><span data-stu-id="06e4e-170">PolyBase mandates a fixed row terminator of \n or newline.</span></span> <span data-ttu-id="06e4e-171">Veri dosyalarınızı toothis standart uygun olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="06e4e-171">Your data files must conform toothis standard.</span></span> <span data-ttu-id="06e4e-172">Dize veya sütun sonlandırıcılar üzerinde herhangi bir kısıtlamanın değil.</span><span class="sxs-lookup"><span data-stu-id="06e4e-172">There aren't any restrictions on string or column terminators.</span></span>

<span data-ttu-id="06e4e-173">PolyBase, dış tablosunda bir parçası olarak yararlı hello dosyasındaki her sütun toodefine gerekir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-173">You will have toodefine every column in hello file as part of your external table in PolyBase.</span></span> <span data-ttu-id="06e4e-174">Dışarı aktarılan tüm sütunları gereklidir ve hello türleri gerekli toohello standartlarına uygun emin olun.</span><span class="sxs-lookup"><span data-stu-id="06e4e-174">Make sure that all exported columns are required and that hello types conform toohello required standards.</span></span>

<span data-ttu-id="06e4e-175">Lütfen toohello bakın [şemanızı geçir] makale desteklenen veri türleri hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="06e4e-175">Please refer back toohello [migrate your schema] article for detail on supported data types.</span></span>

### <a name="location-of-data-files"></a><span data-ttu-id="06e4e-176">Veri dosyalarının konumu</span><span class="sxs-lookup"><span data-stu-id="06e4e-176">Location of data files</span></span>
<span data-ttu-id="06e4e-177">SQL veri ambarı PolyBase tooload verileri Azure Blob depolama biriminden yalnızca kullanır.</span><span class="sxs-lookup"><span data-stu-id="06e4e-177">SQL Data Warehouse uses PolyBase tooload data from Azure Blob Storage exclusively.</span></span> <span data-ttu-id="06e4e-178">Sonuç olarak, hello veri ilk blob depolama alanına aktarıldı gerekir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-178">Consequently, hello data must have been first transferred into blob storage.</span></span>

## <a name="optimizing-data-transfer"></a><span data-ttu-id="06e4e-179">En iyi duruma getirme veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="06e4e-179">Optimizing data transfer</span></span>
<span data-ttu-id="06e4e-180">Merhaba yavaş bölümleri veri geçişinin hello veri tooAzure hello aktarımını biridir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-180">One of hello slowest parts of data migration is hello transfer of hello data tooAzure.</span></span> <span data-ttu-id="06e4e-181">Yalnızca ağ bant genişliği bir sorun olabilir ancak aynı zamanda ağ güvenilirlik ciddi ilerlemesini.</span><span class="sxs-lookup"><span data-stu-id="06e4e-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span></span> <span data-ttu-id="06e4e-182">Varsayılan olarak geçirme verilerini tooAzure Internet şekilde hello makul olasılığı olan oluşan aktarımı hatalar olasılığını hello ' dir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-182">By default migrating data tooAzure is over hello internet so hello chances of transfer errors occurring are reasonably likely.</span></span> <span data-ttu-id="06e4e-183">Ancak, bu hataları tamamen veya kısmen yeniden gönderilen veri toobe gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-183">However, these errors may require data toobe re-sent either in whole or in part.</span></span>

<span data-ttu-id="06e4e-184">Neyse ki, çeşitli seçenekleri tooimprove hello hızı ve bu işlemin esnekliği vardır:</span><span class="sxs-lookup"><span data-stu-id="06e4e-184">Fortunately you have several options tooimprove hello speed and resilience of this process:</span></span>

### <a name="expressrouteexpressroute"></a><span data-ttu-id="06e4e-185">[ExpressRoute][ExpressRoute]</span><span class="sxs-lookup"><span data-stu-id="06e4e-185">[ExpressRoute][ExpressRoute]</span></span>
<span data-ttu-id="06e4e-186">Tooconsider kullanarak isteyebilirsiniz [ExpressRoute] [ ExpressRoute] toospeed hello aktarımı ayarlama.</span><span class="sxs-lookup"><span data-stu-id="06e4e-186">You may want tooconsider using [ExpressRoute][ExpressRoute] toospeed up hello transfer.</span></span> <span data-ttu-id="06e4e-187">[ExpressRoute] [ ExpressRoute] bir özel bağlantı tooAzure sizinle hello bağlantı geçmez şekilde hello genel internet sağlar.</span><span class="sxs-lookup"><span data-stu-id="06e4e-187">[ExpressRoute][ExpressRoute] provides you with an established private connection tooAzure so hello connection does not go over hello public internet.</span></span> <span data-ttu-id="06e4e-188">Bu halinde zorunlu bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="06e4e-188">This is by no means a mandatory step.</span></span> <span data-ttu-id="06e4e-189">Ancak, bu işleme bir şirket içi veri tooAzure Ftp'den zaman artırır veya ortak yerleşim tesisi.</span><span class="sxs-lookup"><span data-stu-id="06e4e-189">However, it will improve throughput when pushing data tooAzure from an on-premises or co-location facility.</span></span>

<span data-ttu-id="06e4e-190">Merhaba kullanmanın yararları [ExpressRoute] [ ExpressRoute] şunlardır:</span><span class="sxs-lookup"><span data-stu-id="06e4e-190">hello benefits of using [ExpressRoute][ExpressRoute] are:</span></span>

1. <span data-ttu-id="06e4e-191">Daha fazla güvenilirlik</span><span class="sxs-lookup"><span data-stu-id="06e4e-191">Increased reliability</span></span>
2. <span data-ttu-id="06e4e-192">Daha hızlı ağ hızı</span><span class="sxs-lookup"><span data-stu-id="06e4e-192">Faster network speed</span></span>
3. <span data-ttu-id="06e4e-193">Alt ağ gecikmesi</span><span class="sxs-lookup"><span data-stu-id="06e4e-193">Lower network latency</span></span>
4. <span data-ttu-id="06e4e-194">daha yüksek ağ güvenliği</span><span class="sxs-lookup"><span data-stu-id="06e4e-194">higher network security</span></span>

<span data-ttu-id="06e4e-195">[ExpressRoute] [ ExpressRoute] çeşitli senaryoları için faydalıdır; yalnızca, geçiş hello.</span><span class="sxs-lookup"><span data-stu-id="06e4e-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just hello migration.</span></span>

<span data-ttu-id="06e4e-196">İlginizi çekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="06e4e-196">Interested?</span></span> <span data-ttu-id="06e4e-197">Lütfen fiyatlandırma ve daha fazla bilgi için ziyaret hello [ExpressRoute belgeleri][ExpressRoute documentation].</span><span class="sxs-lookup"><span data-stu-id="06e4e-197">For more information and pricing please visit hello [ExpressRoute documentation][ExpressRoute documentation].</span></span>

### <a name="azure-import-and-export-service"></a><span data-ttu-id="06e4e-198">Azure içeri ve dışarı aktarma hizmeti</span><span class="sxs-lookup"><span data-stu-id="06e4e-198">Azure Import and Export Service</span></span>
<span data-ttu-id="06e4e-199">Hello Azure içe aktarma ve dışarı aktarma hizmeti olan büyük (GB ++) toomassive (TB ++) veri aktarımlarını Azure içine için tasarlanmış bir veri aktarım işlemi.</span><span class="sxs-lookup"><span data-stu-id="06e4e-199">hello Azure Import and Export Service is a data transfer process designed for large (GB++) toomassive (TB++) transfers of data into Azure.</span></span> <span data-ttu-id="06e4e-200">Veri toodisks yazma ve tooan Azure veri merkezine sevkiyat içerir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-200">It involves writing your data toodisks and shipping them tooan Azure data center.</span></span> <span data-ttu-id="06e4e-201">Merhaba disk içeriği sizin adınıza ardından Azure Storage Bloblarında yüklenir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-201">hello disk contents will then be loaded into Azure Storage Blobs on your behalf.</span></span>

<span data-ttu-id="06e4e-202">Üst düzey bir görünümünü hello alma dışa aktarma işlemi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="06e4e-202">A high-level view of hello import export process is as follows:</span></span>

1. <span data-ttu-id="06e4e-203">Bir Azure Blob Storage kapsayıcısı tooreceive hello verileri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="06e4e-203">Configure an Azure Blob Storage container tooreceive hello data</span></span>
2. <span data-ttu-id="06e4e-204">Veri toolocal deponuzda dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="06e4e-204">Export your data toolocal storage</span></span>
3. <span data-ttu-id="06e4e-205">Merhaba veri too3.5 inç SATA II/III sabit disk hello [Azure içeri/dışarı aktarma aracı] kullanarak sürücüleri kopyalayın</span><span class="sxs-lookup"><span data-stu-id="06e4e-205">Copy hello data too3.5 inch SATA II/III hard disk drives using hello [Azure Import/Export Tool]</span></span>
4. <span data-ttu-id="06e4e-206">Hello Azure içe aktarma ve dışarı aktarma [Azure içeri/dışarı aktarma aracı] hello tarafından üretilen hello günlük dosyaları sağlama hizmeti kullanılarak bir içeri aktarma işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="06e4e-206">Create an Import Job using hello Azure Import and Export Service providing hello journal files produced by hello [Azure Import/Export Tool]</span></span>
5. <span data-ttu-id="06e4e-207">Önerilen Azure veri merkezinizin sevk hello diskler</span><span class="sxs-lookup"><span data-stu-id="06e4e-207">Ship hello disks your nominated Azure data center</span></span>
6. <span data-ttu-id="06e4e-208">Verilerinizi aktarılan tooyour Azure Blob Storage kapsayıcıdır</span><span class="sxs-lookup"><span data-stu-id="06e4e-208">Your data is transferred tooyour Azure Blob Storage container</span></span>
7. <span data-ttu-id="06e4e-209">Polybase'i kullanarak SQLDW içine hello veri yükleme</span><span class="sxs-lookup"><span data-stu-id="06e4e-209">Load hello data into SQLDW using PolyBase</span></span>

### <a name="azcopyazcopy-utility"></a><span data-ttu-id="06e4e-210">[AZCopy][AZCopy] yardımcı programı</span><span class="sxs-lookup"><span data-stu-id="06e4e-210">[AZCopy][AZCopy] utility</span></span>
<span data-ttu-id="06e4e-211">Merhaba [AZCopy][AZCopy] Azure Storage Bloblarında aktarılan verilerinizi almak için harika bir aracı programıdır.</span><span class="sxs-lookup"><span data-stu-id="06e4e-211">hello [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span></span> <span data-ttu-id="06e4e-212">Küçük (MB ++) toovery büyük (GB ++) veri aktarımları için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="06e4e-212">It is designed for small (MB++) toovery large (GB++) data transfers.</span></span> <span data-ttu-id="06e4e-213">[AZCopy] veri tooAzure ve bunu aktarma hello veri aktarımı adım için harika bir seçim olduğunda tasarlanmış tooprovide iyi dayanıklı verimlilik olmuştur.</span><span class="sxs-lookup"><span data-stu-id="06e4e-213">[AZCopy] has also been designed tooprovide good resilient throughput when transferring data tooAzure and so is a great choice for hello data transfer step.</span></span> <span data-ttu-id="06e4e-214">Bir kez aktarılan hello verileri SQL Data Warehouse'a PolyBase kullanarak yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06e4e-214">Once transferred you can load hello data using PolyBase into SQL Data Warehouse.</span></span> <span data-ttu-id="06e4e-215">Ayrıca, bir "Yürütme işlemi" görevini kullanarak, SSIS paketleri AZCopy dahil edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06e4e-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span></span>

<span data-ttu-id="06e4e-216">toouse AZCopy ilk toodownload ve gerekir yükleyin.</span><span class="sxs-lookup"><span data-stu-id="06e4e-216">toouse AZCopy you will first need toodownload and install it.</span></span> <span data-ttu-id="06e4e-217">Var olan bir [üretim sürümü] [ production version] ve [Önizleme sürümü] [ preview version] kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-217">There is a [production version][production version] and a [preview version][preview version] available.</span></span>

<span data-ttu-id="06e4e-218">tooupload bir dosyanın dosya sisteminizi aşağıda bir hello gibi bir komutu gerekir:</span><span class="sxs-lookup"><span data-stu-id="06e4e-218">tooupload a file from your file system you will need a command like hello one below:</span></span>

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="06e4e-219">Bir üst düzey işlem özeti aşağıdakilerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="06e4e-219">A high-level process summary could be:</span></span>

1. <span data-ttu-id="06e4e-220">Bir Azure depolama blob kapsayıcısını tooreceive hello verileri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="06e4e-220">Configure an Azure storage blob container tooreceive hello data</span></span>
2. <span data-ttu-id="06e4e-221">Veri toolocal deponuzda dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="06e4e-221">Export your data toolocal storage</span></span>
3. <span data-ttu-id="06e4e-222">AZCopy verilerinizi hello Azure Blob Storage kapsayıcısı</span><span class="sxs-lookup"><span data-stu-id="06e4e-222">AZCopy your data in hello Azure Blob Storage container</span></span>
4. <span data-ttu-id="06e4e-223">Hello veri PolyBase kullanarak SQL Data Warehouse'a veri yükleme</span><span class="sxs-lookup"><span data-stu-id="06e4e-223">Load hello data into SQL Data Warehouse using PolyBase</span></span>

<span data-ttu-id="06e4e-224">Tam belgeleri kullanılabilir: [AZCopy][AZCopy].</span><span class="sxs-lookup"><span data-stu-id="06e4e-224">Full documentation available: [AZCopy][AZCopy].</span></span>

## <a name="optimizing-data-export"></a><span data-ttu-id="06e4e-225">En iyi duruma getirme verileri dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="06e4e-225">Optimizing data export</span></span>
<span data-ttu-id="06e4e-226">Ayrıca hello verme, PolyBase tarafından düzenlendiği toohello gereksinimlerine uyan tooensuring de toooptimize hello verme işleminin hello veri tooimprove hello daha fazla arama.</span><span class="sxs-lookup"><span data-stu-id="06e4e-226">In addition tooensuring that hello export conforms toohello requirements laid out by PolyBase you can also seek toooptimize hello export of hello data tooimprove hello process further.</span></span>



### <a name="data-compression"></a><span data-ttu-id="06e4e-227">Veri sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="06e4e-227">Data compression</span></span>
<span data-ttu-id="06e4e-228">PolyBase gzip sıkıştırılmış verileri okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-228">PolyBase can read gzip compressed data.</span></span> <span data-ttu-id="06e4e-229">Daha sonra veri toogzip dosyalarınızı hello hello ağ üzerinden gönderilen veri miktarını en aza indirmiş olursunuz mümkün toocompress varsa.</span><span class="sxs-lookup"><span data-stu-id="06e4e-229">If you are able toocompress your data toogzip files then you will minimize hello amount of data being pushed over hello network.</span></span>

### <a name="multiple-files"></a><span data-ttu-id="06e4e-230">Birden çok dosya</span><span class="sxs-lookup"><span data-stu-id="06e4e-230">Multiple files</span></span>
<span data-ttu-id="06e4e-231">Büyük tablolara pek çok dosya sonu yalnızca değil hızı verme tooimprove yardımcı olur, ayrıca ile re-startability aktarmak ve bir kez hello Azure blob depolama alanındaki hello verilerin genel yönetilebilirlik hello yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="06e4e-231">Breaking up large tables into several files not only helps tooimprove export speed, it also helps with transfer re-startability, and hello overall manageability of hello data once in hello Azure blob storage.</span></span> <span data-ttu-id="06e4e-232">PolyBase iyi özelliklerinin çoğu olduğundan, tüm okuyacaksa hello biri bir klasör içindeki dosyaları hello ve bir tablo olarak ele alın.</span><span class="sxs-lookup"><span data-stu-id="06e4e-232">One of hello many nice features of PolyBase is that it will read all hello files inside a folder and treat it as one table.</span></span> <span data-ttu-id="06e4e-233">Bu nedenle, bir fikir tooisolate hello dosyaları her tablo kendi klasörüne içindir.</span><span class="sxs-lookup"><span data-stu-id="06e4e-233">It is therefore a good idea tooisolate hello files for each table into its own folder.</span></span>

<span data-ttu-id="06e4e-234">PolyBase "özyinelemeli klasör geçişinin" bilinen bir özellik de destekler.</span><span class="sxs-lookup"><span data-stu-id="06e4e-234">PolyBase also supports a feature known as "recursive folder traversal".</span></span> <span data-ttu-id="06e4e-235">Bu özelliği kullanabilmek için toofurther geliştirmek, dışarı aktarılan verileri tooimprove hello organizasyonu, veri yönetimi.</span><span class="sxs-lookup"><span data-stu-id="06e4e-235">You can use this feature toofurther enhance hello organization of your exported data tooimprove your data management.</span></span>

<span data-ttu-id="06e4e-236">PolyBase ile veri yükleme hakkında daha fazla toolearn bkz [kullanım PolyBase tooload verileri SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="06e4e-236">toolearn more about loading data with PolyBase, see [Use PolyBase tooload data into SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].</span></span>

## <a name="next-steps"></a><span data-ttu-id="06e4e-237">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="06e4e-237">Next steps</span></span>
<span data-ttu-id="06e4e-238">Geçiş hakkında daha fazla bilgi için bkz: [, çözüm tooSQL veri ambarına geçirme][Migrate your solution tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="06e4e-238">For more about migration, see [Migrate your solution tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse].</span></span>
<span data-ttu-id="06e4e-239">Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].</span><span class="sxs-lookup"><span data-stu-id="06e4e-239">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution tooSQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp tooload data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase tooload data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
