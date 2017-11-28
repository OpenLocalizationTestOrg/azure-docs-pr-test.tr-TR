---
title: "kullanarak aaaTest ve hata ayıklama U-SQL işleri yerel çalıştırın ve Azure Data Lake U-SQL SDK hello | Microsoft Docs"
description: "Visual Studio ve hello Azure Data Lake U-SQL SDK tootest ve U-SQL hata ayıklama için toouse Azure Data Lake araçları yerel iş istasyonunda nasıl işler öğrenin."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/15/2016
ms.author: yanacai
ms.openlocfilehash: be04558a504acf6a088e207608ee2d4a011d3ffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-hello-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="5ccfc-103">Test ve U-SQL işleri yerel kullanılarak çalıştırması ve hello Azure Data Lake U-SQL SDK'sı tarafından hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="5ccfc-103">Test and debug U-SQL jobs by using local run and hello Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="5ccfc-104">Hello Azure Data Lake hizmetinde gibi Azure Data Lake araçları Visual Studio ve hello Azure Data Lake U-SQL SDK toorun U-SQL işleri için iş istasyonunuza, kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-104">You can use Azure Data Lake Tools for Visual Studio and hello Azure Data Lake U-SQL SDK toorun U-SQL jobs on your workstation, just as you can in hello Azure Data Lake service.</span></span> <span data-ttu-id="5ccfc-105">Bu iki yerel çalıştırma özelliği, U-SQL işlerinizi test etme ve hata ayıklama işlemlerinde size zaman kazandırır.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-105">These two local-run features save you time in testing and debugging your U-SQL jobs.</span></span>

## <a name="understand-hello-data-root-folder-and-hello-file-path"></a><span data-ttu-id="5ccfc-106">Merhaba veri kök klasör ve hello dosya yolu anlama</span><span class="sxs-lookup"><span data-stu-id="5ccfc-106">Understand hello data-root folder and hello file path</span></span>

<span data-ttu-id="5ccfc-107">Hem yerel çalıştırma hem de hello U-SQL SDK veri kök klasör gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-107">Both local run and hello U-SQL SDK require a data-root folder.</span></span> <span data-ttu-id="5ccfc-108">Merhaba veri kök klasörü "yerel depolama" Merhaba yerel işlem hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-108">hello data-root folder is a "local store" for hello local compute account.</span></span> <span data-ttu-id="5ccfc-109">Eşdeğer toohello Azure Data Lake Store hesabını Data Lake Analytics hesabı değil.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-109">It's equivalent toohello Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="5ccfc-110">Tooa geçiş farklı bir veri kök tooa farklı depolama hesabı yalnızca değiştirme gibi klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-110">Switching tooa different data-root folder is just like switching tooa different store account.</span></span> <span data-ttu-id="5ccfc-111">Farklı bir veri kök klasörlerle yaygın olarak paylaşılan veri tooaccess istiyorsanız, komut dosyalarınızı mutlak yollar kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-111">If you want tooaccess commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="5ccfc-112">Veya dosya sistemi sembolik bağlantılar oluşturun (örneğin, **mklink** NTFS) hello veri kök klasör toopoint toohello altında paylaşılan veri.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-112">Or, create file system symbolic links (for example, **mklink** on NTFS) under hello data-root folder toopoint toohello shared data.</span></span>

<span data-ttu-id="5ccfc-113">Merhaba veri kök klasör için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="5ccfc-113">hello data-root folder is used to:</span></span>

- <span data-ttu-id="5ccfc-114">Veritabanları, tablolar, tablo değerli işlevler (Tvf) ve derlemeler çeşitli meta verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-114">Store metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="5ccfc-115">Giriş hello ve U-SQL göreli yolda olarak tanımlanan çıkış yolları arayın.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-115">Look up hello input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="5ccfc-116">Göreli yollar kullanılarak kılar daha kolay toodeploy, U-SQL projeleri tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-116">Using relative paths makes it easier toodeploy your U-SQL projects tooAzure.</span></span>

<span data-ttu-id="5ccfc-117">U-SQL betikleri göreli bir yol ve yerel bir mutlak yolu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-117">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="5ccfc-118">Merhaba göreli yolu göreli toohello belirtilen veri kök klasör yoludur.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-118">hello relative path is relative toohello specified data-root folder path.</span></span> <span data-ttu-id="5ccfc-119">Öneririz, kullan "/" olarak hello sunucu tarafı ile uyumlu komut dosyalarınızı yol ayırıcı toomake hello olduğunu.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-119">We recommend that you use "/" as hello path separator toomake your scripts compatible with hello server side.</span></span> <span data-ttu-id="5ccfc-120">Göreli yollar ve eşdeğer mutlak yollarına bazı örnekleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-120">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="5ccfc-121">Bu örneklerde, C:\LocalRunDataRoot hello veri kök klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-121">In these examples, C:\LocalRunDataRoot is hello data-root folder.</span></span>

|<span data-ttu-id="5ccfc-122">Göreli yolu</span><span class="sxs-lookup"><span data-stu-id="5ccfc-122">Relative path</span></span>|<span data-ttu-id="5ccfc-123">Mutlak yolu</span><span class="sxs-lookup"><span data-stu-id="5ccfc-123">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="5ccfc-124">/ABC/DEF/input.csv</span><span class="sxs-lookup"><span data-stu-id="5ccfc-124">/abc/def/input.csv</span></span> |<span data-ttu-id="5ccfc-125">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="5ccfc-125">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="5ccfc-126">ABC/DEF/input.csv</span><span class="sxs-lookup"><span data-stu-id="5ccfc-126">abc/def/input.csv</span></span>  |<span data-ttu-id="5ccfc-127">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="5ccfc-127">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="5ccfc-128">D:/ABC/DEF/input.csv</span><span class="sxs-lookup"><span data-stu-id="5ccfc-128">D:/abc/def/input.csv</span></span> |<span data-ttu-id="5ccfc-129">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="5ccfc-129">D:\abc\def\input.csv</span></span>|

## <a name="use-local-run-from-visual-studio"></a><span data-ttu-id="5ccfc-130">Kullanım yerel Visual Studio'dan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5ccfc-130">Use local run from Visual Studio</span></span>

<span data-ttu-id="5ccfc-131">Visual Studio için Data Lake araçları, Visual Studio'da U-SQL yerel çalıştırma deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-131">Data Lake Tools for Visual Studio provides a U-SQL local-run experience in Visual Studio.</span></span> <span data-ttu-id="5ccfc-132">Bu özelliği kullanarak şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5ccfc-132">By using this feature, you can:</span></span>

- <span data-ttu-id="5ccfc-133">C# derlemeleri'nin yanı sıra yerel olarak bir U-SQL komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-133">Run a U-SQL script locally, along with C# assemblies.</span></span>
- <span data-ttu-id="5ccfc-134">Bir C# derleme yerel olarak hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-134">Debug a C# assembly locally.</span></span>
- <span data-ttu-id="5ccfc-135">Oluşturun, görüntüleyin ve U-SQL katalogları (yerel veritabanlarını, derlemeleri, şemaları ve tabloları) Server Explorer'dan silin.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-135">Create, view, and delete U-SQL catalogs (local databases, assemblies, schemas, and tables) from Server Explorer.</span></span> <span data-ttu-id="5ccfc-136">Merhaba yerel katalog de ayrıca ve Sunucu Gezgini'nden bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-136">You can also find hello local catalog also from Server Explorer.</span></span>

    ![Visual Studio yerel çalıştırma yerel katalog için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

<span data-ttu-id="5ccfc-138">Merhaba Data Lake araçları yükleyici hello varsayılan veri kök klasör olarak kullanılan bir C:\LocalRunRoot klasörü toobe oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-138">hello Data Lake Tools installer creates a C:\LocalRunRoot folder toobe used as hello default data-root folder.</span></span> <span data-ttu-id="5ccfc-139">Merhaba varsayılan yerel çalıştırma paralellik 1'dir.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-139">hello default local-run parallelism is 1.</span></span>

### <a name="tooconfigure-local-run-in-visual-studio"></a><span data-ttu-id="5ccfc-140">tooconfigure yerel Visual Studio'da çalıştırın</span><span class="sxs-lookup"><span data-stu-id="5ccfc-140">tooconfigure local run in Visual Studio</span></span>

1. <span data-ttu-id="5ccfc-141">Visual Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-141">Open Visual Studio.</span></span>
2. <span data-ttu-id="5ccfc-142">Açık **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-142">Open **Server Explorer**.</span></span>
3. <span data-ttu-id="5ccfc-143">Genişletme **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-143">Expand **Azure** > **Data Lake Analytics**.</span></span>
4. <span data-ttu-id="5ccfc-144">Merhaba tıklatın **Data Lake** menüsüne ve ardından **seçenekleri ve ayarları**.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-144">Click hello **Data Lake** menu, and then click **Options and Settings**.</span></span>
5. <span data-ttu-id="5ccfc-145">Merhaba sol ağacında **Azure Data Lake**, genişletin ve ardından **genel**.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-145">In hello left tree, expand **Azure Data Lake**, and then expand **General**.</span></span>

    ![Yerel çalıştırma Visual Studio için Data Lake araçları ayarlarını yapılandırma](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

<span data-ttu-id="5ccfc-147">Visual Studio U-SQL projesi çalıştırma yerel gerçekleştirmek için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-147">A Visual Studio U-SQL project is required for performing local run.</span></span> <span data-ttu-id="5ccfc-148">Bu bölümü, U-SQL betikleri Azure'dan çalışmasını farklıdır.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-148">This part is different from running U-SQL scripts from Azure.</span></span>

### <a name="toorun-a-u-sql-script-locally"></a><span data-ttu-id="5ccfc-149">yerel olarak toorun U-SQL komut dosyası</span><span class="sxs-lookup"><span data-stu-id="5ccfc-149">toorun a U-SQL script locally</span></span>
1. <span data-ttu-id="5ccfc-150">Visual Studio'dan U-SQL projenizi açın.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-150">From Visual Studio, open your U-SQL project.</span></span>   
2. <span data-ttu-id="5ccfc-151">Çözüm Gezgini'nde U-SQL komut dosyasını sağ tıklatın ve ardından **betiği Gönder**.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-151">Right-click a U-SQL script in Solution Explorer, and then click **Submit Script**.</span></span>
3. <span data-ttu-id="5ccfc-152">Seçin **(yerel)** hello Analytics toorun kodunuzu yerel hesap olarak.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-152">Select **(Local)** as hello Analytics account toorun your script locally.</span></span>
<span data-ttu-id="5ccfc-153">Merhaba tıklatarak **(yerel)** hesap komut penceresinde hello üstündeki ve ardından **gönderme** (veya Merhaba Ctrl + F5 klavye kısayolunu kullanın).</span><span class="sxs-lookup"><span data-stu-id="5ccfc-153">You can also click hello **(Local)** account on hello top of script window, and then click **Submit** (or use hello Ctrl + F5 keyboard shortcut).</span></span>

    ![Visual Studio yerel çalıştırma gönderme işleri için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a><span data-ttu-id="5ccfc-155">Betikler ve C# derlemeleri üzerinde yerel olarak hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="5ccfc-155">Debug scripts and C# assemblies locally</span></span>

<span data-ttu-id="5ccfc-156">C# derlemeleri gönderme ve tooAzure Data Lake Analytics Hizmeti'ne kaydetme ayıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-156">You can debug C# assemblies without submitting and registering it tooAzure Data Lake Analytics Service.</span></span> <span data-ttu-id="5ccfc-157">Hem dosyanın arkasındaki hello kodda ve başvuruda bulunulan bir C# projesinde kesme noktaları ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-157">You can set breakpoints in both hello code behind file and in a referenced C# project.</span></span>

#### <a name="toodebug-local-code-in-code-behind-file"></a><span data-ttu-id="5ccfc-158">dosyanın arkasındaki kodda yerel kod toodebug</span><span class="sxs-lookup"><span data-stu-id="5ccfc-158">toodebug local code in code behind file</span></span>

1. <span data-ttu-id="5ccfc-159">Dosyanın arkasındaki hello kodda kesme noktalarını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-159">Set breakpoints in hello code behind file.</span></span>
2. <span data-ttu-id="5ccfc-160">F5 toodebug hello komut dosyası yerel olarak tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-160">Press F5 toodebug hello script locally.</span></span>

> [!NOTE]
   > <span data-ttu-id="5ccfc-161">Aşağıdaki yordam yalnızca works Visual Studio 2015'hello.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-161">hello following procedure only works in Visual Studio 2015.</span></span> <span data-ttu-id="5ccfc-162">Eski Visual Studio'da gerekebilir toomanually hello pdb dosyalarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-162">In older Visual Studio you may need toomanually add hello pdb files.</span></span>  
   >
   >

#### <a name="toodebug-local-code-in-a-referenced-c-project"></a><span data-ttu-id="5ccfc-163">başvuruda bulunulan bir C# projesinde toodebug yerel kod</span><span class="sxs-lookup"><span data-stu-id="5ccfc-163">toodebug local code in a referenced C# project</span></span>

1. <span data-ttu-id="5ccfc-164">Bir C# derleme projesi oluşturun ve toogenerate hello çıkış DLL'sini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-164">Create a C# Assembly project, and build it toogenerate hello output dll.</span></span>
2. <span data-ttu-id="5ccfc-165">U-SQL deyimi kullanarak hello DLL'yi kaydetme:</span><span class="sxs-lookup"><span data-stu-id="5ccfc-165">Register hello dll using a U-SQL statement:</span></span>

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. <span data-ttu-id="5ccfc-166">Merhaba C# kodunda kesme noktalarını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-166">Set breakpoints in hello C# code.</span></span>
4. <span data-ttu-id="5ccfc-167">Hello C# DLL'sine yerel olarak başvuran ile toodebug hello betik F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-167">Press F5 toodebug hello script with referencing hello C# dll locally.</span></span>

## <a name="use-local-run-from-hello-data-lake-u-sql-sdk"></a><span data-ttu-id="5ccfc-168">Data Lake U-SQL SDK Hello çalıştırmak yerel kullanın</span><span class="sxs-lookup"><span data-stu-id="5ccfc-168">Use local run from hello Data Lake U-SQL SDK</span></span>

<span data-ttu-id="5ccfc-169">Ayrıca Visual Studio kullanarak yerel olarak toorunning U-SQL komut dosyaları, komut satırı ve programlama arabirimleri ile yerel olarak hello Azure Data Lake U-SQL SDK toorun U-SQL betiklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-169">In addition toorunning U-SQL scripts locally by using Visual Studio, you can use hello Azure Data Lake U-SQL SDK toorun U-SQL scripts locally with command-line and programming interfaces.</span></span> <span data-ttu-id="5ccfc-170">Bunlar arasında U-SQL yerel testinizi ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ccfc-170">Through these, you can scale your U-SQL local test.</span></span>

<span data-ttu-id="5ccfc-171">Daha fazla bilgi edinmek [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="5ccfc-171">Learn more about [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="5ccfc-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5ccfc-172">Next steps</span></span>

* <span data-ttu-id="5ccfc-173">toosee daha karmaşık bir sorgu görmek [Azure Data Lake Analytics'i kullanarak Web sitesi günlüklerini çözümleme](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="5ccfc-173">toosee a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="5ccfc-174">tooview iş ayrıntılarını görmek [kullanım iş tarayıcı ve Azure Data Lake Analytics işleri için iş görünümünde](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="5ccfc-174">tooview job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="5ccfc-175">toouse hello köşe yürütme görünümü bkz [kullanım hello köşe yürütme görünümü Visual Studio için Data Lake araçları içinde](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="5ccfc-175">toouse hello vertex execution view, see [Use hello Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
