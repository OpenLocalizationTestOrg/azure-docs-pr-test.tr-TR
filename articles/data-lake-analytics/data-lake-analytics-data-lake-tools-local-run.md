---
title: "Test ve U-SQL işleri yerel çalıştırma ve Azure Data Lake U-SQL SDK'sını kullanarak hata ayıklama | Microsoft Docs"
description: "Visual Studio ve Azure Data Lake U-SQL SDK'sı için Azure Data Lake araçları sınamak ve U-SQL işleri, yerel iş istasyonunda hatalarını ayıklamak için nasıl kullanılacağını öğrenin."
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
ms.openlocfilehash: 771a96df5cc66bac46e7144785be8cc072b57b31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-the-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="06af7-103">Test ve U-SQL işleri yerel kullanılarak çalıştırması ve Azure Data Lake U-SQL SDK'sı tarafından hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="06af7-103">Test and debug U-SQL jobs by using local run and the Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="06af7-104">İş istasyonunuzda U-SQL işleri çalıştırmak için, Azure Data Lake hizmetinde yaptığınız gibi Visual Studio için Azure Data Lake Araçları ve Azure Data Lake U-SQL SDK’sını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06af7-104">You can use Azure Data Lake Tools for Visual Studio and the Azure Data Lake U-SQL SDK to run U-SQL jobs on your workstation, just as you can in the Azure Data Lake service.</span></span> <span data-ttu-id="06af7-105">Bu iki yerel çalıştırma özelliği, U-SQL işlerinizi test etme ve hata ayıklama işlemlerinde size zaman kazandırır.</span><span class="sxs-lookup"><span data-stu-id="06af7-105">These two local-run features save you time in testing and debugging your U-SQL jobs.</span></span>

## <a name="understand-the-data-root-folder-and-the-file-path"></a><span data-ttu-id="06af7-106">Veri kök klasör ve dosya yolu anlama</span><span class="sxs-lookup"><span data-stu-id="06af7-106">Understand the data-root folder and the file path</span></span>

<span data-ttu-id="06af7-107">Yerel çalıştırma ve U-SQL SDK'sı veri kök klasör gerektirir.</span><span class="sxs-lookup"><span data-stu-id="06af7-107">Both local run and the U-SQL SDK require a data-root folder.</span></span> <span data-ttu-id="06af7-108">Veri kök klasörü "yerel depolama" yerel işlem hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="06af7-108">The data-root folder is a "local store" for the local compute account.</span></span> <span data-ttu-id="06af7-109">Bir Data Lake Analytics hesabı Azure Data Lake Store hesabına eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="06af7-109">It's equivalent to the Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="06af7-110">Farklı bir veri kök klasörüne değiştirme yalnızca farklı depolama hesabına geçişi gibi olur.</span><span class="sxs-lookup"><span data-stu-id="06af7-110">Switching to a different data-root folder is just like switching to a different store account.</span></span> <span data-ttu-id="06af7-111">Farklı bir veri kök klasörlerle yaygın olarak Paylaşılan verilere erişmek istiyorsanız, komut dosyalarınızı mutlak yollar kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="06af7-111">If you want to access commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="06af7-112">Veya dosya sistemi sembolik bağlantılar oluşturun (örneğin, **mklink** NTFS) için paylaşılan veri noktası için veri kök klasörü altında.</span><span class="sxs-lookup"><span data-stu-id="06af7-112">Or, create file system symbolic links (for example, **mklink** on NTFS) under the data-root folder to point to the shared data.</span></span>

<span data-ttu-id="06af7-113">Veri kök klasör için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="06af7-113">The data-root folder is used to:</span></span>

- <span data-ttu-id="06af7-114">Veritabanları, tablolar, tablo değerli işlevler (Tvf) ve derlemeler çeşitli meta verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="06af7-114">Store metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="06af7-115">U-SQL göreli yolda olarak tanımlanan giriş ve çıkış yol arayın.</span><span class="sxs-lookup"><span data-stu-id="06af7-115">Look up the input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="06af7-116">Göreli yollar kullanarak U-SQL projelerinizi Azure'a dağıtmak kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="06af7-116">Using relative paths makes it easier to deploy your U-SQL projects to Azure.</span></span>

<span data-ttu-id="06af7-117">U-SQL betikleri göreli bir yol ve yerel bir mutlak yolu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06af7-117">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="06af7-118">Göreli yolu göreli belirtilen veri kök klasör yoludur.</span><span class="sxs-lookup"><span data-stu-id="06af7-118">The relative path is relative to the specified data-root folder path.</span></span> <span data-ttu-id="06af7-119">Kullanmanızı öneririz "/" komut dosyalarınızı sunucu tarafı ile uyumlu hale getirmek için yol ayırıcısı olarak.</span><span class="sxs-lookup"><span data-stu-id="06af7-119">We recommend that you use "/" as the path separator to make your scripts compatible with the server side.</span></span> <span data-ttu-id="06af7-120">Göreli yollar ve eşdeğer mutlak yollarına bazı örnekleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="06af7-120">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="06af7-121">Bu örneklerde, C:\LocalRunDataRoot veri kök klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="06af7-121">In these examples, C:\LocalRunDataRoot is the data-root folder.</span></span>

|<span data-ttu-id="06af7-122">Göreli yolu</span><span class="sxs-lookup"><span data-stu-id="06af7-122">Relative path</span></span>|<span data-ttu-id="06af7-123">Mutlak yolu</span><span class="sxs-lookup"><span data-stu-id="06af7-123">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="06af7-124">/ABC/DEF/input.csv</span><span class="sxs-lookup"><span data-stu-id="06af7-124">/abc/def/input.csv</span></span> |<span data-ttu-id="06af7-125">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="06af7-125">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="06af7-126">ABC/DEF/input.csv</span><span class="sxs-lookup"><span data-stu-id="06af7-126">abc/def/input.csv</span></span>  |<span data-ttu-id="06af7-127">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="06af7-127">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="06af7-128">D:/ABC/DEF/input.csv</span><span class="sxs-lookup"><span data-stu-id="06af7-128">D:/abc/def/input.csv</span></span> |<span data-ttu-id="06af7-129">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="06af7-129">D:\abc\def\input.csv</span></span>|

## <a name="use-local-run-from-visual-studio"></a><span data-ttu-id="06af7-130">Kullanım yerel Visual Studio'dan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="06af7-130">Use local run from Visual Studio</span></span>

<span data-ttu-id="06af7-131">Visual Studio için Data Lake araçları, Visual Studio'da U-SQL yerel çalıştırma deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="06af7-131">Data Lake Tools for Visual Studio provides a U-SQL local-run experience in Visual Studio.</span></span> <span data-ttu-id="06af7-132">Bu özelliği kullanarak şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="06af7-132">By using this feature, you can:</span></span>

- <span data-ttu-id="06af7-133">C# derlemeleri'nin yanı sıra yerel olarak bir U-SQL komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="06af7-133">Run a U-SQL script locally, along with C# assemblies.</span></span>
- <span data-ttu-id="06af7-134">Bir C# derleme yerel olarak hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="06af7-134">Debug a C# assembly locally.</span></span>
- <span data-ttu-id="06af7-135">Oluşturun, görüntüleyin ve U-SQL katalogları (yerel veritabanlarını, derlemeleri, şemaları ve tabloları) Server Explorer'dan silin.</span><span class="sxs-lookup"><span data-stu-id="06af7-135">Create, view, and delete U-SQL catalogs (local databases, assemblies, schemas, and tables) from Server Explorer.</span></span> <span data-ttu-id="06af7-136">Yerel katalog de ayrıca ve Sunucu Gezgini'nden bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06af7-136">You can also find the local catalog also from Server Explorer.</span></span>

    ![Visual Studio yerel çalıştırma yerel katalog için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

<span data-ttu-id="06af7-138">Data Lake araçları yükleyici varsayılan veri kök klasör olarak kullanılacak bir C:\LocalRunRoot klasör oluşturur.</span><span class="sxs-lookup"><span data-stu-id="06af7-138">The Data Lake Tools installer creates a C:\LocalRunRoot folder to be used as the default data-root folder.</span></span> <span data-ttu-id="06af7-139">Varsayılan yerel çalıştırma paralellik 1'dir.</span><span class="sxs-lookup"><span data-stu-id="06af7-139">The default local-run parallelism is 1.</span></span>

### <a name="to-configure-local-run-in-visual-studio"></a><span data-ttu-id="06af7-140">Visual Studio'da yerel çalıştırma yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="06af7-140">To configure local run in Visual Studio</span></span>

1. <span data-ttu-id="06af7-141">Visual Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="06af7-141">Open Visual Studio.</span></span>
2. <span data-ttu-id="06af7-142">Açık **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="06af7-142">Open **Server Explorer**.</span></span>
3. <span data-ttu-id="06af7-143">Genişletme **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="06af7-143">Expand **Azure** > **Data Lake Analytics**.</span></span>
4. <span data-ttu-id="06af7-144">Tıklatın **Data Lake** menüsüne ve ardından **seçenekleri ve ayarları**.</span><span class="sxs-lookup"><span data-stu-id="06af7-144">Click the **Data Lake** menu, and then click **Options and Settings**.</span></span>
5. <span data-ttu-id="06af7-145">Sol ağacında **Azure Data Lake**, genişletin ve ardından **genel**.</span><span class="sxs-lookup"><span data-stu-id="06af7-145">In the left tree, expand **Azure Data Lake**, and then expand **General**.</span></span>

    ![Yerel çalıştırma Visual Studio için Data Lake araçları ayarlarını yapılandırma](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

<span data-ttu-id="06af7-147">Visual Studio U-SQL projesi çalıştırma yerel gerçekleştirmek için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="06af7-147">A Visual Studio U-SQL project is required for performing local run.</span></span> <span data-ttu-id="06af7-148">Bu bölümü, U-SQL betikleri Azure'dan çalışmasını farklıdır.</span><span class="sxs-lookup"><span data-stu-id="06af7-148">This part is different from running U-SQL scripts from Azure.</span></span>

### <a name="to-run-a-u-sql-script-locally"></a><span data-ttu-id="06af7-149">U-SQL komut dosyasını yerel olarak çalıştırmak için</span><span class="sxs-lookup"><span data-stu-id="06af7-149">To run a U-SQL script locally</span></span>
1. <span data-ttu-id="06af7-150">Visual Studio'dan U-SQL projenizi açın.</span><span class="sxs-lookup"><span data-stu-id="06af7-150">From Visual Studio, open your U-SQL project.</span></span>   
2. <span data-ttu-id="06af7-151">Çözüm Gezgini'nde U-SQL komut dosyasını sağ tıklatın ve ardından **betiği Gönder**.</span><span class="sxs-lookup"><span data-stu-id="06af7-151">Right-click a U-SQL script in Solution Explorer, and then click **Submit Script**.</span></span>
3. <span data-ttu-id="06af7-152">Seçin **(yerel)** , komut yerel olarak çalıştırmak için Analytics hesabı olarak.</span><span class="sxs-lookup"><span data-stu-id="06af7-152">Select **(Local)** as the Analytics account to run your script locally.</span></span>
<span data-ttu-id="06af7-153">Tıklatarak **(yerel)** hesap komut dosyası penceresinin üst kısmında ve ardından **gönderme** (veya Ctrl + F5 kullanın klavye kısayolu).</span><span class="sxs-lookup"><span data-stu-id="06af7-153">You can also click the **(Local)** account on the top of script window, and then click **Submit** (or use the Ctrl + F5 keyboard shortcut).</span></span>

    ![Visual Studio yerel çalıştırma gönderme işleri için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a><span data-ttu-id="06af7-155">Betikler ve C# derlemeleri üzerinde yerel olarak hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="06af7-155">Debug scripts and C# assemblies locally</span></span>

<span data-ttu-id="06af7-156">C# derlemeleri göndererek ve Azure Data Lake Analytics Hizmeti'ne kaydetme ayıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06af7-156">You can debug C# assemblies without submitting and registering it to Azure Data Lake Analytics Service.</span></span> <span data-ttu-id="06af7-157">Hem dosyanın arkasındaki kodda hem de başvuruda bulunulan bir C# projesinde kesme noktaları ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06af7-157">You can set breakpoints in both the code behind file and in a referenced C# project.</span></span>

#### <a name="to-debug-local-code-in-code-behind-file"></a><span data-ttu-id="06af7-158">Dosyanın arkasındaki kodda yerel kod hatalarını ayıklamak için</span><span class="sxs-lookup"><span data-stu-id="06af7-158">To debug local code in code behind file</span></span>

1. <span data-ttu-id="06af7-159">Dosyanın arkasındaki kodda kesme noktaları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="06af7-159">Set breakpoints in the code behind file.</span></span>
2. <span data-ttu-id="06af7-160">Betik üzerinde yerel olarak hata ayıklama için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="06af7-160">Press F5 to debug the script locally.</span></span>

> [!NOTE]
   > <span data-ttu-id="06af7-161">Aşağıdaki yordam yalnızca Visual Studio 2015'te çalışır.</span><span class="sxs-lookup"><span data-stu-id="06af7-161">The following procedure only works in Visual Studio 2015.</span></span> <span data-ttu-id="06af7-162">Daha eski Visual Studio sürümlerinde, pdb dosyalarını kendiniz eklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="06af7-162">In older Visual Studio you may need to manually add the pdb files.</span></span>  
   >
   >

#### <a name="to-debug-local-code-in-a-referenced-c-project"></a><span data-ttu-id="06af7-163">Başvuruda bulunulan bir C# projesinde yerel kod hatalarını ayıklamak için</span><span class="sxs-lookup"><span data-stu-id="06af7-163">To debug local code in a referenced C# project</span></span>

1. <span data-ttu-id="06af7-164">Bir C# Derleme projesi oluşturun ve projeyi çıktı dll'sini üretmek üzere oluşturun.</span><span class="sxs-lookup"><span data-stu-id="06af7-164">Create a C# Assembly project, and build it to generate the output dll.</span></span>
2. <span data-ttu-id="06af7-165">U-SQL deyimi kullanarak dll'yi kaydetme:</span><span class="sxs-lookup"><span data-stu-id="06af7-165">Register the dll using a U-SQL statement:</span></span>

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. <span data-ttu-id="06af7-166">C# kodunda kesme noktalarını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="06af7-166">Set breakpoints in the C# code.</span></span>
4. <span data-ttu-id="06af7-167">C# DLL'sine yerel olarak başvuran ile komut dosyası hata ayıklamak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="06af7-167">Press F5 to debug the script with referencing the C# dll locally.</span></span>

## <a name="use-local-run-from-the-data-lake-u-sql-sdk"></a><span data-ttu-id="06af7-168">Data Lake U-SQL SDK'dan çalıştırmak yerel kullan</span><span class="sxs-lookup"><span data-stu-id="06af7-168">Use local run from the Data Lake U-SQL SDK</span></span>

<span data-ttu-id="06af7-169">Visual Studio kullanarak yerel olarak U-SQL betikleri çalıştırmanın yanı sıra, U-SQL betiklerini yerel olarak komut satırı ve programlama arabirimleri ile çalıştırmak için Azure Data Lake U-SQL SDK'sını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06af7-169">In addition to running U-SQL scripts locally by using Visual Studio, you can use the Azure Data Lake U-SQL SDK to run U-SQL scripts locally with command-line and programming interfaces.</span></span> <span data-ttu-id="06af7-170">Bunlar arasında U-SQL yerel testinizi ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06af7-170">Through these, you can scale your U-SQL local test.</span></span>

<span data-ttu-id="06af7-171">Daha fazla bilgi edinmek [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="06af7-171">Learn more about [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="06af7-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="06af7-172">Next steps</span></span>

* <span data-ttu-id="06af7-173">Daha karmaşık bir sorgu görmek için bkz: [Azure Data Lake Analytics'i kullanarak Web sitesi günlüklerini çözümleme](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="06af7-173">To see a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="06af7-174">İş ayrıntılarını görüntülemek için bkz: [kullanım iş tarayıcı ve Azure Data Lake Analytics işleri için iş görünümünde](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="06af7-174">To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="06af7-175">Köşe yürütme görünümü kullanmak için bkz: [köşe yürütme görünümü Visual Studio için Data Lake araçları kullanmak](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="06af7-175">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
