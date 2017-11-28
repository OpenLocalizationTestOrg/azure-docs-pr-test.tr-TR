---
title: "aaaScale U-SQL yerel çalıştırma ve test etme, Azure Data Lake U-SQL SDK ile | Microsoft Docs"
description: "Nasıl toouse Azure Data Lake U-SQL SDK tooscale U-SQL işleri yerel çalıştırın ve komut satırı ve yerel istasyonunuzda programlama arabirimleri ile test öğrenin."
services: data-lake-analytics
documentationcenter: 
author: 
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: yanacai
ms.openlocfilehash: 2b0a16229789268e333f723ff6fc2c3efdc29905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="0f6c5-103">Ölçek U-SQL yerel çalıştırma ve test Azure Data Lake U-SQL SDK'sı</span><span class="sxs-lookup"><span data-stu-id="0f6c5-103">Scale U-SQL local run and test with Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="0f6c5-104">U-SQL betiği geliştirmeye genel toorun olduğundan ve yerel olarak test U-SQL betiği önce toocloud onu gönderin.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-104">When developing U-SQL script, it is common toorun and test U-SQL script locally before submit it toocloud.</span></span> <span data-ttu-id="0f6c5-105">Bu senaryo için Azure Data Lake U-SQL SDK adlı bir Nuget paketi Azure Data Lake sağlar, hangi, kolayca aracılığıyla U-SQL yerel çalıştırma ve test ölçeklendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-105">Azure Data Lake provides a Nuget package called Azure Data Lake U-SQL SDK for this scenario, through which you can easily scale U-SQL local run and test.</span></span> <span data-ttu-id="0f6c5-106">Ayrıca bu U-SQL test CI (sürekli tümleştirme) sistem tooautomate hello derleme ve test ile olası toointegrate olur.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-106">It is also possible toointegrate this U-SQL test with CI (Continuous Integration) system tooautomate hello compile and test.</span></span>

<span data-ttu-id="0f6c5-107">İlgilendiğiniz ise nasıl toomanually yerel çalıştırın ve Azure Data Lake araçları için Visual Studio için kullanabileceğiniz sonra U-SQL betiği GUI araçları ile hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-107">If you care about how toomanually local run and debug U-SQL script with GUI tooling, then you can use Azure Data Lake Tools for Visual Studio for that.</span></span> <span data-ttu-id="0f6c5-108">' Dan daha fazla bilgi edinebilirsiniz [burada](data-lake-analytics-data-lake-tools-local-run.md).</span><span class="sxs-lookup"><span data-stu-id="0f6c5-108">You can learn more from [here](data-lake-analytics-data-lake-tools-local-run.md).</span></span>

## <a name="install-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="0f6c5-109">Yükleme Azure Data Lake U-SQL SDK'sı</span><span class="sxs-lookup"><span data-stu-id="0f6c5-109">Install Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="0f6c5-110">Hello Azure Data Lake U-SQL SDK alabilirsiniz [burada](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) Nuget.org üzerinde. Ve kullanmadan önce aşağıdaki gibi bağımlılıklara sahip olduğunuzdan emin toomake gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-110">You can get hello Azure Data Lake U-SQL SDK [here](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) on Nuget.org. And before using it, you need toomake sure you have dependencies as follows.</span></span>

### <a name="dependencies"></a><span data-ttu-id="0f6c5-111">Bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="0f6c5-111">Dependencies</span></span>

<span data-ttu-id="0f6c5-112">Merhaba Data Lake U-SQL SDK bağımlılıklar aşağıdaki hello gerektirir:</span><span class="sxs-lookup"><span data-stu-id="0f6c5-112">hello Data Lake U-SQL SDK requires hello following dependencies:</span></span>

- <span data-ttu-id="0f6c5-113">[Microsoft .NET Framework 4.6 veya daha yeni](https://www.microsoft.com/download/details.aspx?id=17851).</span><span class="sxs-lookup"><span data-stu-id="0f6c5-113">[Microsoft .NET Framework 4.6 or newer](https://www.microsoft.com/download/details.aspx?id=17851).</span></span>
- <span data-ttu-id="0f6c5-114">Microsoft Visual C++ 14 ve Windows SDK 10.0.10240.0 ya da daha yeni (adlandırılan CppSDK bu makalede).</span><span class="sxs-lookup"><span data-stu-id="0f6c5-114">Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0 or newer (which is called CppSDK in this article).</span></span> <span data-ttu-id="0f6c5-115">İki yolu tooget CppSDK vardır:</span><span class="sxs-lookup"><span data-stu-id="0f6c5-115">There are two ways tooget CppSDK:</span></span>

    - <span data-ttu-id="0f6c5-116">Yükleme [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span><span class="sxs-lookup"><span data-stu-id="0f6c5-116">Install [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span></span> <span data-ttu-id="0f6c5-117">Merhaba Program dosyaları klasörü--Örneğin, C:\Program Files (x86) \Windows Kits\10\ altında \Windows Kits\10 klasörü sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-117">You'll have a \Windows Kits\10 folder under hello Program Files folder--for example, C:\Program Files (x86)\Windows Kits\10\.</span></span> <span data-ttu-id="0f6c5-118">Ayrıca hello Windows 10 SDK sürüm \Windows Kits\10\Lib altında bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-118">You'll also find hello Windows 10 SDK version under \Windows Kits\10\Lib.</span></span> <span data-ttu-id="0f6c5-119">Bu klasörler görmüyorsanız, Visual Studio'yu yeniden yükleyin ve hello yükleme sırasında emin tooselect hello Windows 10 SDK olması.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-119">If you don’t see these folders, reinstall Visual Studio and be sure tooselect hello Windows 10 SDK during hello installation.</span></span> <span data-ttu-id="0f6c5-120">Bu Visual Studio ile yüklü varsa, hello U-SQL yerel derleyici onu otomatik olarak bulur.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-120">If you have this installed with Visual Studio, hello U-SQL local compiler will find it automatically.</span></span>

    ![Visual Studio için Data Lake araçları yerel Windows 10 SDK çalıştırma](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - <span data-ttu-id="0f6c5-122">Yükleme [Visual Studio için Data Lake Araçları](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="0f6c5-122">Install [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="0f6c5-123">Merhaba C:\Program Files (x86) \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK Visual C++ ve Windows SDK dosyalarını paketlenmiş bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-123">You can find hello prepackaged Visual C++ and Windows SDK files at C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span></span> <span data-ttu-id="0f6c5-124">Bu durumda, hello U-SQL yerel derleyici hello bağımlılıkları otomatik olarak bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-124">In this case, hello U-SQL local compiler cannot find hello dependencies automatically.</span></span> <span data-ttu-id="0f6c5-125">Bunun için toospecify hello CppSDK yol gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-125">You need toospecify hello CppSDK path for it.</span></span> <span data-ttu-id="0f6c5-126">Merhaba dosyaları tooanother konumu kopyalayabilir veya olduğu gibi kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-126">You can either copy hello files tooanother location or use it as is.</span></span>

## <a name="understand-basic-concepts"></a><span data-ttu-id="0f6c5-127">Temel kavramları anlama</span><span class="sxs-lookup"><span data-stu-id="0f6c5-127">Understand basic concepts</span></span>

### <a name="data-root"></a><span data-ttu-id="0f6c5-128">Veri kökü</span><span class="sxs-lookup"><span data-stu-id="0f6c5-128">Data root</span></span>

<span data-ttu-id="0f6c5-129">Merhaba veri kök klasörü "yerel depolama" Merhaba yerel işlem hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-129">hello data-root folder is a "local store" for hello local compute account.</span></span> <span data-ttu-id="0f6c5-130">Eşdeğer toohello Azure Data Lake Store hesabını Data Lake Analytics hesabı değil.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-130">It's equivalent toohello Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="0f6c5-131">Tooa geçiş farklı bir veri kök tooa farklı depolama hesabı yalnızca değiştirme gibi klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-131">Switching tooa different data-root folder is just like switching tooa different store account.</span></span> <span data-ttu-id="0f6c5-132">Farklı bir veri kök klasörlerle yaygın olarak paylaşılan veri tooaccess istiyorsanız, komut dosyalarınızı mutlak yollar kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-132">If you want tooaccess commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="0f6c5-133">Veya dosya sistemi sembolik bağlantılar oluşturun (örneğin, **mklink** NTFS) hello veri kök klasör toopoint toohello altında paylaşılan veri.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-133">Or, create file system symbolic links (for example, **mklink** on NTFS) under hello data-root folder toopoint toohello shared data.</span></span>

<span data-ttu-id="0f6c5-134">Merhaba veri kök klasör için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="0f6c5-134">hello data-root folder is used to:</span></span>

- <span data-ttu-id="0f6c5-135">Veritabanları, tablolar, tablo değerli işlevler (Tvf) ve derlemeleri de dahil olmak üzere, yerel meta verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-135">Store local metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="0f6c5-136">Giriş hello ve U-SQL göreli yolda olarak tanımlanan çıkış yolları arayın.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-136">Look up hello input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="0f6c5-137">Göreli yollar kullanılarak kılar daha kolay toodeploy, U-SQL projeleri tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-137">Using relative paths makes it easier toodeploy your U-SQL projects tooAzure.</span></span>

### <a name="file-path-in-u-sql"></a><span data-ttu-id="0f6c5-138">U-SQL dosya yolu</span><span class="sxs-lookup"><span data-stu-id="0f6c5-138">File path in U-SQL</span></span>

<span data-ttu-id="0f6c5-139">U-SQL betikleri göreli bir yol ve yerel bir mutlak yolu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-139">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="0f6c5-140">Merhaba göreli yolu göreli toohello belirtilen veri kök klasör yoludur.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-140">hello relative path is relative toohello specified data-root folder path.</span></span> <span data-ttu-id="0f6c5-141">Öneririz, kullan "/" olarak hello sunucu tarafı ile uyumlu komut dosyalarınızı yol ayırıcı toomake hello olduğunu.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-141">We recommend that you use "/" as hello path separator toomake your scripts compatible with hello server side.</span></span> <span data-ttu-id="0f6c5-142">Göreli yollar ve eşdeğer mutlak yollarına bazı örnekleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-142">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="0f6c5-143">Bu örneklerde, C:\LocalRunDataRoot hello veri kök klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-143">In these examples, C:\LocalRunDataRoot is hello data-root folder.</span></span>

|<span data-ttu-id="0f6c5-144">Göreli yolu</span><span class="sxs-lookup"><span data-stu-id="0f6c5-144">Relative path</span></span>|<span data-ttu-id="0f6c5-145">Mutlak yolu</span><span class="sxs-lookup"><span data-stu-id="0f6c5-145">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="0f6c5-146">/ABC/DEF/input.csv</span><span class="sxs-lookup"><span data-stu-id="0f6c5-146">/abc/def/input.csv</span></span> |<span data-ttu-id="0f6c5-147">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="0f6c5-147">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="0f6c5-148">ABC/DEF/input.csv</span><span class="sxs-lookup"><span data-stu-id="0f6c5-148">abc/def/input.csv</span></span>  |<span data-ttu-id="0f6c5-149">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="0f6c5-149">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="0f6c5-150">D:/ABC/DEF/input.csv</span><span class="sxs-lookup"><span data-stu-id="0f6c5-150">D:/abc/def/input.csv</span></span> |<span data-ttu-id="0f6c5-151">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="0f6c5-151">D:\abc\def\input.csv</span></span>|

### <a name="working-directory"></a><span data-ttu-id="0f6c5-152">Çalışma dizini</span><span class="sxs-lookup"><span data-stu-id="0f6c5-152">Working directory</span></span>

<span data-ttu-id="0f6c5-153">Merhaba U-SQL komut dosyası yerel olarak çalışırken, bir çalışma dizini geçerli çalışma dizini altında derleme sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-153">When running hello U-SQL script locally, a working directory is created during compilation under current running directory.</span></span> <span data-ttu-id="0f6c5-154">Ayrıca toohello derleme çıkarır, hello çalışma zamanı dosyalarını yerel yürütme için gölge kopyalanan toothis çalışma dizini olacaktır.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-154">In addition toohello compilation outputs, hello needed runtime files for local execution will be shadow copied toothis working directory.</span></span> <span data-ttu-id="0f6c5-155">Çalışma dizini kök klasörünü hello "ScopeWorkDir" adı verilir ve hello dosyaları hello çalışma dizini altında aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="0f6c5-155">hello working directory root folder is called "ScopeWorkDir" and hello files under hello working directory are as follows:</span></span>

|<span data-ttu-id="0f6c5-156">Dizin/dosya</span><span class="sxs-lookup"><span data-stu-id="0f6c5-156">Directory/file</span></span>|<span data-ttu-id="0f6c5-157">Dizin/dosya</span><span class="sxs-lookup"><span data-stu-id="0f6c5-157">Directory/file</span></span>|<span data-ttu-id="0f6c5-158">Dizin/dosya</span><span class="sxs-lookup"><span data-stu-id="0f6c5-158">Directory/file</span></span>|<span data-ttu-id="0f6c5-159">Tanım</span><span class="sxs-lookup"><span data-stu-id="0f6c5-159">Definition</span></span>|<span data-ttu-id="0f6c5-160">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0f6c5-160">Description</span></span>|
|--------------|--------------|--------------|----------|-----------|
|<span data-ttu-id="0f6c5-161">C6A101DDCB470506</span><span class="sxs-lookup"><span data-stu-id="0f6c5-161">C6A101DDCB470506</span></span>| | |<span data-ttu-id="0f6c5-162">Karma dize çalışma zamanı sürümü</span><span class="sxs-lookup"><span data-stu-id="0f6c5-162">Hash string of runtime version</span></span>|<span data-ttu-id="0f6c5-163">Çalışma zamanı dosyalarını yerel yürütme için gerekli gölge kopyası</span><span class="sxs-lookup"><span data-stu-id="0f6c5-163">Shadow copy of runtime files needed for local execution</span></span>|
| |<span data-ttu-id="0f6c5-164">Script_66AE4909AA0ED06C</span><span class="sxs-lookup"><span data-stu-id="0f6c5-164">Script_66AE4909AA0ED06C</span></span>| |<span data-ttu-id="0f6c5-165">Ad script + betik yolu dizesi karma</span><span class="sxs-lookup"><span data-stu-id="0f6c5-165">Script name + hash string of script path</span></span>|<span data-ttu-id="0f6c5-166">Derleme çıktı ve yürütme günlüğü adım</span><span class="sxs-lookup"><span data-stu-id="0f6c5-166">Compilation outputs and execution step logging</span></span>|
| | |<span data-ttu-id="0f6c5-167">\_komut dosyası\_.abr</span><span class="sxs-lookup"><span data-stu-id="0f6c5-167">\_script\_.abr</span></span>|<span data-ttu-id="0f6c5-168">Derleyici çıktısı</span><span class="sxs-lookup"><span data-stu-id="0f6c5-168">Compiler output</span></span>|<span data-ttu-id="0f6c5-169">Cebiri dosyası</span><span class="sxs-lookup"><span data-stu-id="0f6c5-169">Algebra file</span></span>|
| | |<span data-ttu-id="0f6c5-170">\_ScopeCodeGen\_. *</span><span class="sxs-lookup"><span data-stu-id="0f6c5-170">\_ScopeCodeGen\_.*</span></span>|<span data-ttu-id="0f6c5-171">Derleyici çıktısı</span><span class="sxs-lookup"><span data-stu-id="0f6c5-171">Compiler output</span></span>|<span data-ttu-id="0f6c5-172">Oluşturulan yönetilen kod</span><span class="sxs-lookup"><span data-stu-id="0f6c5-172">Generated managed code</span></span>|
| | |<span data-ttu-id="0f6c5-173">\_ScopeCodeGenEngine\_. *</span><span class="sxs-lookup"><span data-stu-id="0f6c5-173">\_ScopeCodeGenEngine\_.*</span></span>|<span data-ttu-id="0f6c5-174">Derleyici çıktısı</span><span class="sxs-lookup"><span data-stu-id="0f6c5-174">Compiler output</span></span>|<span data-ttu-id="0f6c5-175">Oluşturulan yerel kod</span><span class="sxs-lookup"><span data-stu-id="0f6c5-175">Generated native code</span></span>|
| | |<span data-ttu-id="0f6c5-176">Başvurulan derlemeler</span><span class="sxs-lookup"><span data-stu-id="0f6c5-176">referenced assemblies</span></span>|<span data-ttu-id="0f6c5-177">Derleme başvurusu</span><span class="sxs-lookup"><span data-stu-id="0f6c5-177">Assembly reference</span></span>|<span data-ttu-id="0f6c5-178">Başvurulan derleme dosyaları</span><span class="sxs-lookup"><span data-stu-id="0f6c5-178">Referenced assembly files</span></span>|
| | |<span data-ttu-id="0f6c5-179">deployed_resources</span><span class="sxs-lookup"><span data-stu-id="0f6c5-179">deployed_resources</span></span>|<span data-ttu-id="0f6c5-180">Kaynak dağıtma</span><span class="sxs-lookup"><span data-stu-id="0f6c5-180">Resource deployment</span></span>|<span data-ttu-id="0f6c5-181">Kaynak dağıtım dosyaları</span><span class="sxs-lookup"><span data-stu-id="0f6c5-181">Resource deployment files</span></span>|
| | |<span data-ttu-id="0f6c5-182">xxxxxxxx.xxx[1..n]\_\*. *</span><span class="sxs-lookup"><span data-stu-id="0f6c5-182">xxxxxxxx.xxx[1..n]\_\*.*</span></span>|<span data-ttu-id="0f6c5-183">Yürütme günlüğü</span><span class="sxs-lookup"><span data-stu-id="0f6c5-183">Execution log</span></span>|<span data-ttu-id="0f6c5-184">Günlük yürütme adımları</span><span class="sxs-lookup"><span data-stu-id="0f6c5-184">Log of execution steps</span></span>|


## <a name="use-hello-sdk-from-hello-command-line"></a><span data-ttu-id="0f6c5-185">Merhaba SDK hello komut satırından kullanma</span><span class="sxs-lookup"><span data-stu-id="0f6c5-185">Use hello SDK from hello command line</span></span>

### <a name="command-line-interface-of-hello-helper-application"></a><span data-ttu-id="0f6c5-186">Merhaba Yardımcısı uygulamasının komut satırı arabirimi</span><span class="sxs-lookup"><span data-stu-id="0f6c5-186">Command-line interface of hello helper application</span></span>

<span data-ttu-id="0f6c5-187">SDK directory\build\runtime altında LocalRunHelper.exe arabirimleri yaygın olarak kullanılan Merhaba, yerel çalıştırma toomost işlevleri sağlayan hello komut satırı yardımcı uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-187">Under SDK directory\build\runtime, LocalRunHelper.exe is hello command-line helper application that provides interfaces toomost of hello commonly used local-run functions.</span></span> <span data-ttu-id="0f6c5-188">Her ikisi de komut hello ve hello değişken anahtarları büyük/küçük harfe duyarlıdır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-188">Note that both hello command and hello argument switches are case-sensitive.</span></span> <span data-ttu-id="0f6c5-189">tooinvoke onu:</span><span class="sxs-lookup"><span data-stu-id="0f6c5-189">tooinvoke it:</span></span>

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

<span data-ttu-id="0f6c5-190">Bağımsız değişkenler olmadan veya hello LocalRunHelper.exe çalıştırın **yardımcı** geçiş tooshow hello Yardım bilgileri:</span><span class="sxs-lookup"><span data-stu-id="0f6c5-190">Run LocalRunHelper.exe without arguments or with hello **help** switch tooshow hello help information:</span></span>

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile hello script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

<span data-ttu-id="0f6c5-191">Hello bilgi yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="0f6c5-191">In hello help information:</span></span>

-  <span data-ttu-id="0f6c5-192">**Komut** hello komut adını verir.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-192">**Command** gives hello command’s name.</span></span>  
-  <span data-ttu-id="0f6c5-193">**Bağımsız değişkeni gerekli** sağlanmalıdır bağımsız değişkenleri listeler.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-193">**Required Argument** lists arguments that must be supplied.</span></span>  
-  <span data-ttu-id="0f6c5-194">**İsteğe bağlı bağımsız değişkeni** varsayılan değerlerle isteğe bağlı bağımsız değişkenler listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-194">**Optional Argument** lists arguments that are optional, with default values.</span></span>  <span data-ttu-id="0f6c5-195">Boole isteğe bağlı bağımsız değişkenler parametreleri yoktur ve negatif tootheir varsayılan değer, görünümlerini anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-195">Optional Boolean arguments don’t have parameters, and their appearances mean negative tootheir default value.</span></span>

### <a name="return-value-and-logging"></a><span data-ttu-id="0f6c5-196">Dönüş değeri ve günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="0f6c5-196">Return value and logging</span></span>

<span data-ttu-id="0f6c5-197">Merhaba yardımcı uygulama döndürür **0** başarı için ve **-1** hatası.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-197">hello helper application returns **0** for success and **-1** for failure.</span></span> <span data-ttu-id="0f6c5-198">Varsayılan olarak, tüm iletileri toohello geçerli konsol hello Yardımcısı gönderir.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-198">By default, hello helper sends all messages toohello current console.</span></span> <span data-ttu-id="0f6c5-199">Ancak, hello hello komutlarının çoğunu destekler **- MessageOut path_to_log_file** hello yönlendiren isteğe bağlı bağımsız değişkeni tooa günlük dosyasına çıkarır.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-199">However, most of hello commands support hello **-MessageOut path_to_log_file** optional argument that redirects hello outputs tooa log file.</span></span>

### <a name="environment-variable-configuring"></a><span data-ttu-id="0f6c5-200">Ortam değişkeni yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0f6c5-200">Environment variable configuring</span></span>

<span data-ttu-id="0f6c5-201">U-SQL yerel ihtiyaçlarını bağımlılıklar için belirtilen CppSDK yolu yanı sıra yerel depolama hesabı olarak belirtilen veri kök çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-201">U-SQL local run needs a specified data root as local storage account, as well as a specified CppSDK path for dependencies.</span></span> <span data-ttu-id="0f6c5-202">Bunlar için her iki kümesi hello bağımsız komut satırı veya ayarlanan ortam değişkeninde olabilir.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-202">You can both set hello argument in command-line or set environment variable for them.</span></span>

- <span data-ttu-id="0f6c5-203">Set hello **SCOPE_CPP_SDK** ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-203">Set hello **SCOPE_CPP_SDK** environment variable.</span></span>

    <span data-ttu-id="0f6c5-204">Visual Studio için Data Lake araçları yükleyerek Microsoft Visual C++ ve Windows SDK hello alırsanız klasörü aşağıdaki hello sahip olduğunu doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="0f6c5-204">If you get Microsoft Visual C++ and hello Windows SDK by installing Data Lake Tools for Visual Studio, verify that you have hello following folder:</span></span>

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    <span data-ttu-id="0f6c5-205">Adlı yeni bir ortam değişkeni tanımlamak **SCOPE_CPP_SDK** toopoint toothis dizini.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-205">Define a new environment variable called **SCOPE_CPP_SDK** toopoint toothis directory.</span></span> <span data-ttu-id="0f6c5-206">Veya hello klasörü toohello başka bir konuma kopyalayın ve belirtin **SCOPE_CPP_SDK** olarak.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-206">Or copy hello folder toohello other location and specify **SCOPE_CPP_SDK** as that.</span></span>

    <span data-ttu-id="0f6c5-207">Toplama toosetting hello ortam değişkeninde hello belirtebilirsiniz **- CppSDK** hello komut satırı kullanırken bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-207">In addition toosetting hello environment variable, you can specify hello **-CppSDK** argument when you're using hello command line.</span></span> <span data-ttu-id="0f6c5-208">Bu bağımsız değişken varsayılan CppSDK ortam değişkeni üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-208">This argument overwrites your default CppSDK environment variable.</span></span>

- <span data-ttu-id="0f6c5-209">Set hello **LOCALRUN_DATAROOT** ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-209">Set hello **LOCALRUN_DATAROOT** environment variable.</span></span>

    <span data-ttu-id="0f6c5-210">Adlı yeni bir ortam değişkeni tanımlamak **LOCALRUN_DATAROOT** toohello veri kök işaret.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-210">Define a new environment variable called **LOCALRUN_DATAROOT** that points toohello data root.</span></span>

    <span data-ttu-id="0f6c5-211">Toplama toosetting hello ortam değişkeninde hello belirtebilirsiniz **- DataRoot** bağımsız değişkeni ile komut satırını kullanırken hello veri kök yolu.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-211">In addition toosetting hello environment variable, you can specify hello **-DataRoot** argument with hello data-root path when you're using a command line.</span></span> <span data-ttu-id="0f6c5-212">Bu bağımsız değişken varsayılan veri kök ortam değişkeni üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-212">This argument overwrites your default data-root environment variable.</span></span> <span data-ttu-id="0f6c5-213">Böylece hello varsayılan veri kök ortam değişkeni tüm işlemleri için üzerine çalıştırıyorsanız bu bağımsız değişken tooevery komut satırı tooadd gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-213">You need tooadd this argument tooevery command line you're running so that you can overwrite hello default data-root environment variable for all operations.</span></span>

### <a name="sdk-command-line-usage-samples"></a><span data-ttu-id="0f6c5-214">SDK komut satırı kullanım örnekleri</span><span class="sxs-lookup"><span data-stu-id="0f6c5-214">SDK command line usage samples</span></span>

#### <a name="compile-and-run"></a><span data-ttu-id="0f6c5-215">Derleyin ve çalıştırın</span><span class="sxs-lookup"><span data-stu-id="0f6c5-215">Compile and run</span></span>

<span data-ttu-id="0f6c5-216">Merhaba **çalıştırmak** komutu kullanıldığında toocompile hello komut dosyası ve sonra derlenmiş sonuçları yürütün.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-216">hello **run** command is used toocompile hello script and then execute compiled results.</span></span> <span data-ttu-id="0f6c5-217">Komut satırı bağımsız değişkenlerini olanlardan birleşimidir **derleme** ve **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-217">Its command-line arguments are a combination of those from **compile** and **execute**.</span></span>

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="0f6c5-218">Hello için isteğe bağlı bağımsız değişkenler şunlardır **çalıştırmak**:</span><span class="sxs-lookup"><span data-stu-id="0f6c5-218">hello following are optional arguments for **run**:</span></span>


|<span data-ttu-id="0f6c5-219">Bağımsız değişken</span><span class="sxs-lookup"><span data-stu-id="0f6c5-219">Argument</span></span>|<span data-ttu-id="0f6c5-220">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="0f6c5-220">Default value</span></span>|<span data-ttu-id="0f6c5-221">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0f6c5-221">Description</span></span>|
|--------|-------------|-----------|
|<span data-ttu-id="0f6c5-222">-Arkasındaki koda</span><span class="sxs-lookup"><span data-stu-id="0f6c5-222">-CodeBehind</span></span>|<span data-ttu-id="0f6c5-223">False</span><span class="sxs-lookup"><span data-stu-id="0f6c5-223">False</span></span>|<span data-ttu-id="0f6c5-224">arka plan .cs kod Hello komut dosyası var</span><span class="sxs-lookup"><span data-stu-id="0f6c5-224">hello script has .cs code behind</span></span>|
|<span data-ttu-id="0f6c5-225">-CppSDK</span><span class="sxs-lookup"><span data-stu-id="0f6c5-225">-CppSDK</span></span>| |<span data-ttu-id="0f6c5-226">CppSDK dizini</span><span class="sxs-lookup"><span data-stu-id="0f6c5-226">CppSDK Directory</span></span>|
|<span data-ttu-id="0f6c5-227">-DataRoot</span><span class="sxs-lookup"><span data-stu-id="0f6c5-227">-DataRoot</span></span>| <span data-ttu-id="0f6c5-228">DataRoot ortam değişkeni</span><span class="sxs-lookup"><span data-stu-id="0f6c5-228">DataRoot environment variable</span></span>|<span data-ttu-id="0f6c5-229">DataRoot yerel çalıştırma için varsayılan çok 'LOCALRUN_DATAROOT' ortam değişkeni</span><span class="sxs-lookup"><span data-stu-id="0f6c5-229">DataRoot for local run, default too'LOCALRUN_DATAROOT' environment variable</span></span>|
|<span data-ttu-id="0f6c5-230">-MessageOut</span><span class="sxs-lookup"><span data-stu-id="0f6c5-230">-MessageOut</span></span>| |<span data-ttu-id="0f6c5-231">Konsol tooa dosyası iletilerde dökümü</span><span class="sxs-lookup"><span data-stu-id="0f6c5-231">Dump messages on console tooa file</span></span>|
|<span data-ttu-id="0f6c5-232">-Paralel</span><span class="sxs-lookup"><span data-stu-id="0f6c5-232">-Parallel</span></span>|<span data-ttu-id="0f6c5-233">1</span><span class="sxs-lookup"><span data-stu-id="0f6c5-233">1</span></span>|<span data-ttu-id="0f6c5-234">Merhaba çalıştırmak hello planla belirtilen paralellik</span><span class="sxs-lookup"><span data-stu-id="0f6c5-234">Run hello plan with hello specified parallelism</span></span>|
|<span data-ttu-id="0f6c5-235">-Başvurular</span><span class="sxs-lookup"><span data-stu-id="0f6c5-235">-References</span></span>| |<span data-ttu-id="0f6c5-236">Tarafından ayrılmış bir listesini yolları tooextra başvuru derlemeleri veya arka plan, kod veri dosyaları ';'</span><span class="sxs-lookup"><span data-stu-id="0f6c5-236">List of paths tooextra reference assemblies or data files of code behind, separated by ';'</span></span>|
|<span data-ttu-id="0f6c5-237">-UdoRedirect</span><span class="sxs-lookup"><span data-stu-id="0f6c5-237">-UdoRedirect</span></span>|<span data-ttu-id="0f6c5-238">False</span><span class="sxs-lookup"><span data-stu-id="0f6c5-238">False</span></span>|<span data-ttu-id="0f6c5-239">Udo derleme yeniden yönlendirme yapılandırması oluşturma</span><span class="sxs-lookup"><span data-stu-id="0f6c5-239">Generate Udo assembly redirect config</span></span>|
|<span data-ttu-id="0f6c5-240">-UseDatabase</span><span class="sxs-lookup"><span data-stu-id="0f6c5-240">-UseDatabase</span></span>|<span data-ttu-id="0f6c5-241">ana</span><span class="sxs-lookup"><span data-stu-id="0f6c5-241">master</span></span>|<span data-ttu-id="0f6c5-242">Veritabanı toouse geçici derleme kaydı arka plan kod için</span><span class="sxs-lookup"><span data-stu-id="0f6c5-242">Database toouse for code behind temporary assembly registration</span></span>|
|<span data-ttu-id="0f6c5-243">-Verbose</span><span class="sxs-lookup"><span data-stu-id="0f6c5-243">-Verbose</span></span>|<span data-ttu-id="0f6c5-244">False</span><span class="sxs-lookup"><span data-stu-id="0f6c5-244">False</span></span>|<span data-ttu-id="0f6c5-245">Çalışma zamanı ayrıntılı çıkışlarından Göster</span><span class="sxs-lookup"><span data-stu-id="0f6c5-245">Show detailed outputs from runtime</span></span>|
|<span data-ttu-id="0f6c5-246">-WorkDir</span><span class="sxs-lookup"><span data-stu-id="0f6c5-246">-WorkDir</span></span>|<span data-ttu-id="0f6c5-247">Geçerli dizin</span><span class="sxs-lookup"><span data-stu-id="0f6c5-247">Current Directory</span></span>|<span data-ttu-id="0f6c5-248">Derleyici kullanım ve çıktı dizini</span><span class="sxs-lookup"><span data-stu-id="0f6c5-248">Directory for compiler usage and outputs</span></span>|
|<span data-ttu-id="0f6c5-249">-RunScopeCEP</span><span class="sxs-lookup"><span data-stu-id="0f6c5-249">-RunScopeCEP</span></span>|<span data-ttu-id="0f6c5-250">0</span><span class="sxs-lookup"><span data-stu-id="0f6c5-250">0</span></span>|<span data-ttu-id="0f6c5-251">ScopeCEP modu toouse</span><span class="sxs-lookup"><span data-stu-id="0f6c5-251">ScopeCEP mode toouse</span></span>|
|<span data-ttu-id="0f6c5-252">-ScopeCEPTempPath</span><span class="sxs-lookup"><span data-stu-id="0f6c5-252">-ScopeCEPTempPath</span></span>|<span data-ttu-id="0f6c5-253">Temp</span><span class="sxs-lookup"><span data-stu-id="0f6c5-253">temp</span></span>|<span data-ttu-id="0f6c5-254">Veri akışı için Geçici yol toouse</span><span class="sxs-lookup"><span data-stu-id="0f6c5-254">Temp path toouse for streaming data</span></span>|
|<span data-ttu-id="0f6c5-255">-OptFlags</span><span class="sxs-lookup"><span data-stu-id="0f6c5-255">-OptFlags</span></span>| |<span data-ttu-id="0f6c5-256">İyileştirici bayrakların virgülle ayrılmış listesi</span><span class="sxs-lookup"><span data-stu-id="0f6c5-256">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="0f6c5-257">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="0f6c5-257">Here's an example:</span></span>

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

<span data-ttu-id="0f6c5-258">Birleştirme yanı sıra **derleme** ve **yürütme**, derleyip derlenmiş hello yürütülebilir dosyalar ayrı ayrı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-258">Besides combining **compile** and **execute**, you can compile and execute hello compiled executables separately.</span></span>

#### <a name="compile-a-u-sql-script"></a><span data-ttu-id="0f6c5-259">U-SQL komut dosyası derleme</span><span class="sxs-lookup"><span data-stu-id="0f6c5-259">Compile a U-SQL script</span></span>

<span data-ttu-id="0f6c5-260">Merhaba **derleme** kullanılan toocompile U-SQL komut dosyası tooexecutables komutudur.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-260">hello **compile** command is used toocompile a U-SQL script tooexecutables.</span></span>

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="0f6c5-261">Hello için isteğe bağlı bağımsız değişkenler şunlardır **derleme**:</span><span class="sxs-lookup"><span data-stu-id="0f6c5-261">hello following are optional arguments for **compile**:</span></span>


|<span data-ttu-id="0f6c5-262">Bağımsız değişken</span><span class="sxs-lookup"><span data-stu-id="0f6c5-262">Argument</span></span>|<span data-ttu-id="0f6c5-263">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0f6c5-263">Description</span></span>|
|--------|-----------|
| <span data-ttu-id="0f6c5-264">-Arkasındaki koda [varsayılan değer 'False']</span><span class="sxs-lookup"><span data-stu-id="0f6c5-264">-CodeBehind [default value 'False']</span></span>|<span data-ttu-id="0f6c5-265">arka plan .cs kod Hello komut dosyası var</span><span class="sxs-lookup"><span data-stu-id="0f6c5-265">hello script has .cs code behind</span></span>|
| <span data-ttu-id="0f6c5-266">-CppSDK [varsayılan değer '']</span><span class="sxs-lookup"><span data-stu-id="0f6c5-266">-CppSDK [default value '']</span></span>|<span data-ttu-id="0f6c5-267">CppSDK dizini</span><span class="sxs-lookup"><span data-stu-id="0f6c5-267">CppSDK Directory</span></span>|
| <span data-ttu-id="0f6c5-268">-DataRoot [varsayılan değer 'DataRoot ortam değişkeni']</span><span class="sxs-lookup"><span data-stu-id="0f6c5-268">-DataRoot [default value 'DataRoot environment variable']</span></span>|<span data-ttu-id="0f6c5-269">DataRoot yerel çalıştırma için varsayılan çok 'LOCALRUN_DATAROOT' ortam değişkeni</span><span class="sxs-lookup"><span data-stu-id="0f6c5-269">DataRoot for local run, default too'LOCALRUN_DATAROOT' environment variable</span></span>|
| <span data-ttu-id="0f6c5-270">-MessageOut [varsayılan değer '']</span><span class="sxs-lookup"><span data-stu-id="0f6c5-270">-MessageOut [default value '']</span></span>|<span data-ttu-id="0f6c5-271">Konsol tooa dosyası iletilerde dökümü</span><span class="sxs-lookup"><span data-stu-id="0f6c5-271">Dump messages on console tooa file</span></span>|
| <span data-ttu-id="0f6c5-272">-Başvuran [varsayılan değer '']</span><span class="sxs-lookup"><span data-stu-id="0f6c5-272">-References [default value '']</span></span>|<span data-ttu-id="0f6c5-273">Tarafından ayrılmış bir listesini yolları tooextra başvuru derlemeleri veya arka plan, kod veri dosyaları ';'</span><span class="sxs-lookup"><span data-stu-id="0f6c5-273">List of paths tooextra reference assemblies or data files of code behind, separated by ';'</span></span>|
| <span data-ttu-id="0f6c5-274">-Basit [varsayılan değer 'False']</span><span class="sxs-lookup"><span data-stu-id="0f6c5-274">-Shallow [default value 'False']</span></span>|<span data-ttu-id="0f6c5-275">Basit derleme</span><span class="sxs-lookup"><span data-stu-id="0f6c5-275">Shallow compile</span></span>|
| <span data-ttu-id="0f6c5-276">-UdoRedirect [varsayılan değer 'False']</span><span class="sxs-lookup"><span data-stu-id="0f6c5-276">-UdoRedirect [default value 'False']</span></span>|<span data-ttu-id="0f6c5-277">Udo derleme yeniden yönlendirme yapılandırması oluşturma</span><span class="sxs-lookup"><span data-stu-id="0f6c5-277">Generate Udo assembly redirect config</span></span>|
| <span data-ttu-id="0f6c5-278">-UseDatabase [varsayılan değer 'master']</span><span class="sxs-lookup"><span data-stu-id="0f6c5-278">-UseDatabase [default value 'master']</span></span>|<span data-ttu-id="0f6c5-279">Veritabanı toouse geçici derleme kaydı arka plan kod için</span><span class="sxs-lookup"><span data-stu-id="0f6c5-279">Database toouse for code behind temporary assembly registration</span></span>|
| <span data-ttu-id="0f6c5-280">-WorkDir [varsayılan değer 'Geçerli dizin']</span><span class="sxs-lookup"><span data-stu-id="0f6c5-280">-WorkDir [default value 'Current Directory']</span></span>|<span data-ttu-id="0f6c5-281">Derleyici kullanım ve çıktı dizini</span><span class="sxs-lookup"><span data-stu-id="0f6c5-281">Directory for compiler usage and outputs</span></span>|
| <span data-ttu-id="0f6c5-282">-RunScopeCEP [varsayılan değer '0']</span><span class="sxs-lookup"><span data-stu-id="0f6c5-282">-RunScopeCEP [default value '0']</span></span>|<span data-ttu-id="0f6c5-283">ScopeCEP modu toouse</span><span class="sxs-lookup"><span data-stu-id="0f6c5-283">ScopeCEP mode toouse</span></span>|
| <span data-ttu-id="0f6c5-284">-ScopeCEPTempPath [varsayılan değer 'temp']</span><span class="sxs-lookup"><span data-stu-id="0f6c5-284">-ScopeCEPTempPath [default value 'temp']</span></span>|<span data-ttu-id="0f6c5-285">Veri akışı için Geçici yol toouse</span><span class="sxs-lookup"><span data-stu-id="0f6c5-285">Temp path toouse for streaming data</span></span>|
| <span data-ttu-id="0f6c5-286">-OptFlags [varsayılan değer '']</span><span class="sxs-lookup"><span data-stu-id="0f6c5-286">-OptFlags [default value '']</span></span>|<span data-ttu-id="0f6c5-287">İyileştirici bayrakların virgülle ayrılmış listesi</span><span class="sxs-lookup"><span data-stu-id="0f6c5-287">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="0f6c5-288">Bazı kullanım örnekleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-288">Here are some usage examples.</span></span>

<span data-ttu-id="0f6c5-289">U-SQL komut dosyası derleme:</span><span class="sxs-lookup"><span data-stu-id="0f6c5-289">Compile a U-SQL script:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql

<span data-ttu-id="0f6c5-290">U-SQL komut dosyasını derleyin ve hello veri kök klasörünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-290">Compile a U-SQL script and set hello data-root folder.</span></span> <span data-ttu-id="0f6c5-291">Bu hello kümesi ortam değişkeni üzerine yazacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-291">Note that this will overwrite hello set environment variable.</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

<span data-ttu-id="0f6c5-292">U-SQL betiği derlemek ve bir çalışma dizini, referans derlemesini ve veritabanı ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="0f6c5-292">Compile a U-SQL script and set a working directory, reference assembly, and database:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a><span data-ttu-id="0f6c5-293">Derlenmiş sonuçları yürütme</span><span class="sxs-lookup"><span data-stu-id="0f6c5-293">Execute compiled results</span></span>

<span data-ttu-id="0f6c5-294">Merhaba **yürütme** derlenmiş kullanılan tooexecute sonuçları bir komuttur.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-294">hello **execute** command is used tooexecute compiled results.</span></span>   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

<span data-ttu-id="0f6c5-295">Hello için isteğe bağlı bağımsız değişkenler şunlardır **yürütme**:</span><span class="sxs-lookup"><span data-stu-id="0f6c5-295">hello following are optional arguments for **execute**:</span></span>

|<span data-ttu-id="0f6c5-296">Bağımsız değişken</span><span class="sxs-lookup"><span data-stu-id="0f6c5-296">Argument</span></span>|<span data-ttu-id="0f6c5-297">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0f6c5-297">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="0f6c5-298">-DataRoot [varsayılan değer '']</span><span class="sxs-lookup"><span data-stu-id="0f6c5-298">-DataRoot [default value '']</span></span>|<span data-ttu-id="0f6c5-299">Meta veri yürütme için veri kökü.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-299">Data root for metadata execution.</span></span> <span data-ttu-id="0f6c5-300">Toohello varsayılan olarak **LOCALRUN_DATAROOT** ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-300">It defaults toohello **LOCALRUN_DATAROOT** environment variable.</span></span>|
|<span data-ttu-id="0f6c5-301">-MessageOut [varsayılan değer '']</span><span class="sxs-lookup"><span data-stu-id="0f6c5-301">-MessageOut [default value '']</span></span>|<span data-ttu-id="0f6c5-302">Merhaba konsol tooa dosyası iletilerde dökümü.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-302">Dump messages on hello console tooa file.</span></span>|
|<span data-ttu-id="0f6c5-303">-Paralel [varsayılan değeri '1']</span><span class="sxs-lookup"><span data-stu-id="0f6c5-303">-Parallel [default value '1']</span></span>|<span data-ttu-id="0f6c5-304">Gösterge toorun oluşturulan hello yerel çalıştırma hello adımlara paralellik düzeyi belirtilen.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-304">Indicator toorun hello generated local-run steps with hello specified parallelism level.</span></span>|
|<span data-ttu-id="0f6c5-305">-Verbose [varsayılan değer 'False']</span><span class="sxs-lookup"><span data-stu-id="0f6c5-305">-Verbose [default value 'False']</span></span>|<span data-ttu-id="0f6c5-306">Gösterge tooshow çalışma zamanı çıkışlarından ayrıntılı.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-306">Indicator tooshow detailed outputs from runtime.</span></span>|

<span data-ttu-id="0f6c5-307">Kullanım örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="0f6c5-307">Here's a usage example:</span></span>

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-hello-sdk-with-programming-interfaces"></a><span data-ttu-id="0f6c5-308">Merhaba SDK ile programlama arabirimleri kullanın</span><span class="sxs-lookup"><span data-stu-id="0f6c5-308">Use hello SDK with programming interfaces</span></span>

<span data-ttu-id="0f6c5-309">Merhaba programlama arabirimleri tüm hello LocalRunHelper.exe bulunur.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-309">hello programming interfaces are all located in hello LocalRunHelper.exe.</span></span> <span data-ttu-id="0f6c5-310">U-SQL komut dosyası yerel test C# test framework tooscale hello ve bunları toointegrate hello hello U-SQL SDK işlevselliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-310">You can use them toointegrate hello functionality of hello U-SQL SDK and hello C# test framework tooscale your U-SQL script local test.</span></span> <span data-ttu-id="0f6c5-311">Bu makalede, hello standart C# birim testi projesi tooshow nasıl kullanacağım toouse bu tootest, U-SQL komut dosyası arabirimleri.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-311">In this article, I will use hello standard C# unit test project tooshow how toouse these interfaces tootest your U-SQL script.</span></span>

### <a name="step-1-create-c-unit-test-project-and-configuration"></a><span data-ttu-id="0f6c5-312">1. adım: C# birim testi projesi ve yapılandırma oluşturma</span><span class="sxs-lookup"><span data-stu-id="0f6c5-312">Step 1: Create C# unit test project and configuration</span></span>

- <span data-ttu-id="0f6c5-313">Dosyası aracılığıyla bir C# birim testi projesi oluşturma > Yeni > Proje > Visual C# > Test > birim testi projesi.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-313">Create a C# unit test project through File > New > Project > Visual C# > Test > Unit Test Project.</span></span>
- <span data-ttu-id="0f6c5-314">Başlangıç projesi için bir başvuru olarak LocalRunHelper.exe ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-314">Add LocalRunHelper.exe as a reference for hello project.</span></span> <span data-ttu-id="0f6c5-315">Merhaba LocalRunHelper.exe \build\runtime\LocalRunHelper.exe Nuget paketi bulunur.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-315">hello LocalRunHelper.exe is located at \build\runtime\LocalRunHelper.exe in Nuget package.</span></span>

    ![Azure Data Lake U-SQL SDK'sı başvurusu ekleme](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- <span data-ttu-id="0f6c5-317">U-SQL SDK **yalnızca** destek x64 ortamı, yapma emin tooset yapı platform hedefi x64 olarak.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-317">U-SQL SDK **only** support x64 environment, make sure tooset build platform target as x64.</span></span> <span data-ttu-id="0f6c5-318">Bu proje özelliği üzerinden ayarlayabilirsiniz > Yapı > Platform hedefi.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-318">You can set that through Project Property > Build > Platform target.</span></span>

    ![Azure Data Lake U-SQL SDK'sını yapılandırmak x64 proje](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- <span data-ttu-id="0f6c5-320">Test ortamınızı emin tooset x64 olun.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-320">Make sure tooset your test environment as x64.</span></span> <span data-ttu-id="0f6c5-321">Visual Studio'da Test ayarlayabilirsiniz > Test Ayarları > Varsayılan İşlemci mimarisi > x64.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-321">In Visual Studio, you can set it through Test > Test Settings > Default Processor Architecture > x64.</span></span>

    ![Azure Data Lake U-SQL SDK'sını yapılandırmak x64 Test Ortamı](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- <span data-ttu-id="0f6c5-323">Emin toocopy genellikle ProjectFolder\bin\x64\Debug altında olan NugetPackage\build\runtime\ tooproject çalışma dizini altındaki tüm bağımlılık dosyaları olun.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-323">Make sure toocopy all dependency files under NugetPackage\build\runtime\ tooproject working directory which is usually under ProjectFolder\bin\x64\Debug.</span></span>

### <a name="step-2-create-u-sql-script-test-case"></a><span data-ttu-id="0f6c5-324">2. adım: U-SQL betiği test çalışması oluşturma</span><span class="sxs-lookup"><span data-stu-id="0f6c5-324">Step 2: Create U-SQL script test case</span></span>

<span data-ttu-id="0f6c5-325">U-SQL betiği testi için hello örnek kod aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-325">Below is hello sample code for U-SQL script test.</span></span> <span data-ttu-id="0f6c5-326">Test etmek için tooprepare komut dosyaları, gereken giriş dosyaları ve beklenen çıktı dosyaları.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-326">For testing, you need tooprepare scripts, input files and expected output files.</span></span>

    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System.IO;
    using System.Text;
    using System.Security.Cryptography;
    using Microsoft.Analytics.LocalRun;

    namespace UnitTestProject1
    {
        [TestClass]
        public class USQLUnitTest
        {
            [TestMethod]
            public void TestUSQLScript()
            {
                //Specify hello local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure hello DateRoot path, Script Path and CPPSDK path
                localrun.DataRoot = "../../../";
                localrun.ScriptPath = "../../../Script/Script.usql";
                localrun.CppSdkDir = "../../../CppSDK";

                //Run U-SQL script
                localrun.DoRun();

                //Script output 
                string Result = Path.Combine(localrun.DataRoot, "Output/result.csv");

                //Expected script output
                string ExpectedResult = "../../../ExpectedOutput/result.csv";

                Test.Helpers.FileAssert.AreEqual(Result, ExpectedResult);

                //Don't forget tooclose MessageOutput tooget logs into file
                MessageOutput.Close();
            }
        }
    }

    namespace Test.Helpers
    {
        public static class FileAssert
        {
            static string GetFileHash(string filename)
            {
                Assert.IsTrue(File.Exists(filename));

                using (var hash = new SHA1Managed())
                {
                    var clearBytes = File.ReadAllBytes(filename);
                    var hashedBytes = hash.ComputeHash(clearBytes);
                    return ConvertBytesToHex(hashedBytes);
                }
            }

            static string ConvertBytesToHex(byte[] bytes)
            {
                var sb = new StringBuilder();

                for (var i = 0; i < bytes.Length; i++)
                {
                    sb.Append(bytes[i].ToString("x"));
                }
                return sb.ToString();
            }

            public static void AreEqual(string filename1, string filename2)
            {
                string hash1 = GetFileHash(filename1);
                string hash2 = GetFileHash(filename2);

                Assert.AreEqual(hash1, hash2);
            }
        }
    }


### <a name="programming-interfaces-in-localrunhelperexe"></a><span data-ttu-id="0f6c5-327">LocalRunHelper.exe programlama arabirimleri</span><span class="sxs-lookup"><span data-stu-id="0f6c5-327">Programming interfaces in LocalRunHelper.exe</span></span>

<span data-ttu-id="0f6c5-328">Programlama arabirimleri çalıştırmak U-SQL yerel derleme için hello LocalRunHelper.exe sağlar, vb. hello arabirimleri aşağıda listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-328">LocalRunHelper.exe provides hello programming interfaces for U-SQL local compile, run, etc. hello interfaces are listed as follows.</span></span>

<span data-ttu-id="0f6c5-329">**Oluşturucusu**</span><span class="sxs-lookup"><span data-stu-id="0f6c5-329">**Constructor**</span></span>

<span data-ttu-id="0f6c5-330">Ortak LocalRunHelper ([System.IO.TextWriter messageOutput = null])</span><span class="sxs-lookup"><span data-stu-id="0f6c5-330">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span></span>

|<span data-ttu-id="0f6c5-331">Parametre</span><span class="sxs-lookup"><span data-stu-id="0f6c5-331">Parameter</span></span>|<span data-ttu-id="0f6c5-332">Tür</span><span class="sxs-lookup"><span data-stu-id="0f6c5-332">Type</span></span>|<span data-ttu-id="0f6c5-333">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0f6c5-333">Description</span></span>|
|---------|----|-----------|
|<span data-ttu-id="0f6c5-334">messageOutput</span><span class="sxs-lookup"><span data-stu-id="0f6c5-334">messageOutput</span></span>|<span data-ttu-id="0f6c5-335">System.IO.TextWriter</span><span class="sxs-lookup"><span data-stu-id="0f6c5-335">System.IO.TextWriter</span></span>|<span data-ttu-id="0f6c5-336">Çıktı iletileri için toonull toouse konsol Ayarla</span><span class="sxs-lookup"><span data-stu-id="0f6c5-336">for output messages, set toonull toouse Console</span></span>|

<span data-ttu-id="0f6c5-337">**Özellikleri**</span><span class="sxs-lookup"><span data-stu-id="0f6c5-337">**Properties**</span></span>

|<span data-ttu-id="0f6c5-338">Özellik</span><span class="sxs-lookup"><span data-stu-id="0f6c5-338">Property</span></span>|<span data-ttu-id="0f6c5-339">Tür</span><span class="sxs-lookup"><span data-stu-id="0f6c5-339">Type</span></span>|<span data-ttu-id="0f6c5-340">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0f6c5-340">Description</span></span>|
|--------|----|-----------|
|<span data-ttu-id="0f6c5-341">AlgebraPath</span><span class="sxs-lookup"><span data-stu-id="0f6c5-341">AlgebraPath</span></span>|<span data-ttu-id="0f6c5-342">Dize</span><span class="sxs-lookup"><span data-stu-id="0f6c5-342">string</span></span>|<span data-ttu-id="0f6c5-343">Merhaba yol tooalgebra dosyası (cebiri dosya biridir hello derleme sonuçları)</span><span class="sxs-lookup"><span data-stu-id="0f6c5-343">hello path tooalgebra file (algebra file is one of hello compilation results)</span></span>|
|<span data-ttu-id="0f6c5-344">CodeBehindReferences</span><span class="sxs-lookup"><span data-stu-id="0f6c5-344">CodeBehindReferences</span></span>|<span data-ttu-id="0f6c5-345">Dize</span><span class="sxs-lookup"><span data-stu-id="0f6c5-345">string</span></span>|<span data-ttu-id="0f6c5-346">Merhaba komut dosyası başvuruları arkasında ek kodu varsa, ile ayrılmış hello yollarını belirtin ';'</span><span class="sxs-lookup"><span data-stu-id="0f6c5-346">If hello script has additional code behind references, specify hello paths separated with ';'</span></span>|
|<span data-ttu-id="0f6c5-347">CppSdkDir</span><span class="sxs-lookup"><span data-stu-id="0f6c5-347">CppSdkDir</span></span>|<span data-ttu-id="0f6c5-348">Dize</span><span class="sxs-lookup"><span data-stu-id="0f6c5-348">string</span></span>|<span data-ttu-id="0f6c5-349">CppSDK dizini</span><span class="sxs-lookup"><span data-stu-id="0f6c5-349">CppSDK directory</span></span>|
|<span data-ttu-id="0f6c5-350">CurrentDir</span><span class="sxs-lookup"><span data-stu-id="0f6c5-350">CurrentDir</span></span>|<span data-ttu-id="0f6c5-351">Dize</span><span class="sxs-lookup"><span data-stu-id="0f6c5-351">string</span></span>|<span data-ttu-id="0f6c5-352">Geçerli dizin</span><span class="sxs-lookup"><span data-stu-id="0f6c5-352">Current directory</span></span>|
|<span data-ttu-id="0f6c5-353">DataRoot</span><span class="sxs-lookup"><span data-stu-id="0f6c5-353">DataRoot</span></span>|<span data-ttu-id="0f6c5-354">Dize</span><span class="sxs-lookup"><span data-stu-id="0f6c5-354">string</span></span>|<span data-ttu-id="0f6c5-355">Veri kök yolu</span><span class="sxs-lookup"><span data-stu-id="0f6c5-355">Data root path</span></span>|
|<span data-ttu-id="0f6c5-356">DebuggerMailPath</span><span class="sxs-lookup"><span data-stu-id="0f6c5-356">DebuggerMailPath</span></span>|<span data-ttu-id="0f6c5-357">Dize</span><span class="sxs-lookup"><span data-stu-id="0f6c5-357">string</span></span>|<span data-ttu-id="0f6c5-358">Merhaba yolu toodebugger yuvası</span><span class="sxs-lookup"><span data-stu-id="0f6c5-358">hello path toodebugger mailslot</span></span>|
|<span data-ttu-id="0f6c5-359">GenerateUdoRedirect</span><span class="sxs-lookup"><span data-stu-id="0f6c5-359">GenerateUdoRedirect</span></span>|<span data-ttu-id="0f6c5-360">bool</span><span class="sxs-lookup"><span data-stu-id="0f6c5-360">bool</span></span>|<span data-ttu-id="0f6c5-361">Biz toogenerate derleme yüklenirken istiyorsanız yeniden yönlendirme geçersiz kılma yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0f6c5-361">If we want toogenerate assembly loading redirection override config</span></span>|
|<span data-ttu-id="0f6c5-362">HasCodeBehind</span><span class="sxs-lookup"><span data-stu-id="0f6c5-362">HasCodeBehind</span></span>|<span data-ttu-id="0f6c5-363">bool</span><span class="sxs-lookup"><span data-stu-id="0f6c5-363">bool</span></span>|<span data-ttu-id="0f6c5-364">Merhaba betik arka plan kodu varsa</span><span class="sxs-lookup"><span data-stu-id="0f6c5-364">If hello script has code behind</span></span>|
|<span data-ttu-id="0f6c5-365">InputDir</span><span class="sxs-lookup"><span data-stu-id="0f6c5-365">InputDir</span></span>|<span data-ttu-id="0f6c5-366">Dize</span><span class="sxs-lookup"><span data-stu-id="0f6c5-366">string</span></span>|<span data-ttu-id="0f6c5-367">Giriş verileri için dizin</span><span class="sxs-lookup"><span data-stu-id="0f6c5-367">Directory for input data</span></span>|
|<span data-ttu-id="0f6c5-368">MessagePath</span><span class="sxs-lookup"><span data-stu-id="0f6c5-368">MessagePath</span></span>|<span data-ttu-id="0f6c5-369">Dize</span><span class="sxs-lookup"><span data-stu-id="0f6c5-369">string</span></span>|<span data-ttu-id="0f6c5-370">İleti döküm dosyası yolu</span><span class="sxs-lookup"><span data-stu-id="0f6c5-370">Message dump file path</span></span>|
|<span data-ttu-id="0f6c5-371">OutputDir</span><span class="sxs-lookup"><span data-stu-id="0f6c5-371">OutputDir</span></span>|<span data-ttu-id="0f6c5-372">Dize</span><span class="sxs-lookup"><span data-stu-id="0f6c5-372">string</span></span>|<span data-ttu-id="0f6c5-373">Çıktı verileri için dizin</span><span class="sxs-lookup"><span data-stu-id="0f6c5-373">Directory for output data</span></span>|
|<span data-ttu-id="0f6c5-374">Paralellik</span><span class="sxs-lookup"><span data-stu-id="0f6c5-374">Parallelism</span></span>|<span data-ttu-id="0f6c5-375">Int</span><span class="sxs-lookup"><span data-stu-id="0f6c5-375">int</span></span>|<span data-ttu-id="0f6c5-376">Paralellik toorun hello cebiri</span><span class="sxs-lookup"><span data-stu-id="0f6c5-376">Parallelism toorun hello algebra</span></span>|
|<span data-ttu-id="0f6c5-377">ParentPid</span><span class="sxs-lookup"><span data-stu-id="0f6c5-377">ParentPid</span></span>|<span data-ttu-id="0f6c5-378">Int</span><span class="sxs-lookup"><span data-stu-id="0f6c5-378">int</span></span>|<span data-ttu-id="0f6c5-379">PID hello üst üzerinde hangi hello tooexit, kümesi too0 veya negatif tooignore izler</span><span class="sxs-lookup"><span data-stu-id="0f6c5-379">PID of hello parent on which hello service monitors tooexit, set too0 or negative tooignore</span></span>|
|<span data-ttu-id="0f6c5-380">ResultPath</span><span class="sxs-lookup"><span data-stu-id="0f6c5-380">ResultPath</span></span>|<span data-ttu-id="0f6c5-381">Dize</span><span class="sxs-lookup"><span data-stu-id="0f6c5-381">string</span></span>|<span data-ttu-id="0f6c5-382">Sonuç döküm dosyası yolu</span><span class="sxs-lookup"><span data-stu-id="0f6c5-382">Result dump file path</span></span>|
|<span data-ttu-id="0f6c5-383">RuntimeDir</span><span class="sxs-lookup"><span data-stu-id="0f6c5-383">RuntimeDir</span></span>|<span data-ttu-id="0f6c5-384">Dize</span><span class="sxs-lookup"><span data-stu-id="0f6c5-384">string</span></span>|<span data-ttu-id="0f6c5-385">Çalışma zamanı dizini</span><span class="sxs-lookup"><span data-stu-id="0f6c5-385">Runtime directory</span></span>|
|<span data-ttu-id="0f6c5-386">scriptPath</span><span class="sxs-lookup"><span data-stu-id="0f6c5-386">ScriptPath</span></span>|<span data-ttu-id="0f6c5-387">Dize</span><span class="sxs-lookup"><span data-stu-id="0f6c5-387">string</span></span>|<span data-ttu-id="0f6c5-388">Burada toofind hello komut dosyası</span><span class="sxs-lookup"><span data-stu-id="0f6c5-388">Where toofind hello script</span></span>|
|<span data-ttu-id="0f6c5-389">Basit</span><span class="sxs-lookup"><span data-stu-id="0f6c5-389">Shallow</span></span>|<span data-ttu-id="0f6c5-390">bool</span><span class="sxs-lookup"><span data-stu-id="0f6c5-390">bool</span></span>|<span data-ttu-id="0f6c5-391">Derleme veya basit</span><span class="sxs-lookup"><span data-stu-id="0f6c5-391">Shallow compile or not</span></span>|
|<span data-ttu-id="0f6c5-392">TempDir</span><span class="sxs-lookup"><span data-stu-id="0f6c5-392">TempDir</span></span>|<span data-ttu-id="0f6c5-393">Dize</span><span class="sxs-lookup"><span data-stu-id="0f6c5-393">string</span></span>|<span data-ttu-id="0f6c5-394">Geçici dizin</span><span class="sxs-lookup"><span data-stu-id="0f6c5-394">Temp directory</span></span>|
|<span data-ttu-id="0f6c5-395">UseDataBase</span><span class="sxs-lookup"><span data-stu-id="0f6c5-395">UseDataBase</span></span>|<span data-ttu-id="0f6c5-396">Dize</span><span class="sxs-lookup"><span data-stu-id="0f6c5-396">string</span></span>|<span data-ttu-id="0f6c5-397">Geçici derleme kaydı, varsayılan olarak ana arka plan kod için Hello veritabanı toouse belirtin</span><span class="sxs-lookup"><span data-stu-id="0f6c5-397">Specify hello database toouse for code behind temporary assembly registration, master by default</span></span>|
|<span data-ttu-id="0f6c5-398">WorkDir</span><span class="sxs-lookup"><span data-stu-id="0f6c5-398">WorkDir</span></span>|<span data-ttu-id="0f6c5-399">Dize</span><span class="sxs-lookup"><span data-stu-id="0f6c5-399">string</span></span>|<span data-ttu-id="0f6c5-400">Tercih edilen çalışma dizini</span><span class="sxs-lookup"><span data-stu-id="0f6c5-400">Preferred working directory</span></span>|


<span data-ttu-id="0f6c5-401">**Yöntemi**</span><span class="sxs-lookup"><span data-stu-id="0f6c5-401">**Method**</span></span>

|<span data-ttu-id="0f6c5-402">Yöntem</span><span class="sxs-lookup"><span data-stu-id="0f6c5-402">Method</span></span>|<span data-ttu-id="0f6c5-403">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0f6c5-403">Description</span></span>|<span data-ttu-id="0f6c5-404">Döndür</span><span class="sxs-lookup"><span data-stu-id="0f6c5-404">Return</span></span>|<span data-ttu-id="0f6c5-405">Parametre</span><span class="sxs-lookup"><span data-stu-id="0f6c5-405">Parameter</span></span>|
|------|-----------|------|---------|
|<span data-ttu-id="0f6c5-406">Ortak bool DoCompile()</span><span class="sxs-lookup"><span data-stu-id="0f6c5-406">public bool DoCompile()</span></span>|<span data-ttu-id="0f6c5-407">Merhaba U-SQL komut dosyası derleme</span><span class="sxs-lookup"><span data-stu-id="0f6c5-407">Compile hello U-SQL script</span></span>|<span data-ttu-id="0f6c5-408">Başarı true</span><span class="sxs-lookup"><span data-stu-id="0f6c5-408">True on success</span></span>| |
|<span data-ttu-id="0f6c5-409">Ortak bool DoExec()</span><span class="sxs-lookup"><span data-stu-id="0f6c5-409">public bool DoExec()</span></span>|<span data-ttu-id="0f6c5-410">Derlenmiş hello sonuç yürütme</span><span class="sxs-lookup"><span data-stu-id="0f6c5-410">Execute hello compiled result</span></span>|<span data-ttu-id="0f6c5-411">Başarı true</span><span class="sxs-lookup"><span data-stu-id="0f6c5-411">True on success</span></span>| |
|<span data-ttu-id="0f6c5-412">Ortak bool DoRun()</span><span class="sxs-lookup"><span data-stu-id="0f6c5-412">public bool DoRun()</span></span>|<span data-ttu-id="0f6c5-413">(Derleme + Execute) Hello U-SQL komut dosyasını çalıştır</span><span class="sxs-lookup"><span data-stu-id="0f6c5-413">Run hello U-SQL script (Compile + Execute)</span></span>|<span data-ttu-id="0f6c5-414">Başarı true</span><span class="sxs-lookup"><span data-stu-id="0f6c5-414">True on success</span></span>| |
|<span data-ttu-id="0f6c5-415">Ortak bool IsValidRuntimeDir (dize yolu)</span><span class="sxs-lookup"><span data-stu-id="0f6c5-415">public bool IsValidRuntimeDir(string path)</span></span>|<span data-ttu-id="0f6c5-416">Belirtilen yol hello geçerli çalışma zamanı yolu olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="0f6c5-416">Check if hello given path is valid runtime path</span></span>|<span data-ttu-id="0f6c5-417">TRUE olarak geçerli</span><span class="sxs-lookup"><span data-stu-id="0f6c5-417">True for valid</span></span>|<span data-ttu-id="0f6c5-418">çalışma zamanı dizinin Hello yolu</span><span class="sxs-lookup"><span data-stu-id="0f6c5-418">hello path of runtime directory</span></span>|


## <a name="faq-about-common-issue"></a><span data-ttu-id="0f6c5-419">Yaygın sorun hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="0f6c5-419">FAQ about common issue</span></span>

### <a name="error-1"></a><span data-ttu-id="0f6c5-420">1. hata:</span><span class="sxs-lookup"><span data-stu-id="0f6c5-420">Error 1:</span></span>
<span data-ttu-id="0f6c5-421">E_CSC_SYSTEM_INTERNAL: İç hata oluştu!</span><span class="sxs-lookup"><span data-stu-id="0f6c5-421">E_CSC_SYSTEM_INTERNAL: Internal error!</span></span> <span data-ttu-id="0f6c5-422">Dosya veya derleme 'ScopeEngineManaged.dll' ya da bağımlılıklarından biri yüklenemedi.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-422">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span></span> <span data-ttu-id="0f6c5-423">Merhaba Belirtilen modül bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-423">hello specified module could not be found.</span></span>

<span data-ttu-id="0f6c5-424">Merhaba aşağıdakileri denetleyin:</span><span class="sxs-lookup"><span data-stu-id="0f6c5-424">Please check hello following:</span></span>

- <span data-ttu-id="0f6c5-425">X64 olduğundan emin olun ortamı.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-425">Make sure you have x64 environment.</span></span> <span data-ttu-id="0f6c5-426">Merhaba yapı hedef platformu ve hello test ortamı x64 olması, çok bakın**1. adım: oluşturmak C# birim testi projesi ve yapılandırma** üstünde.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-426">hello build target platform and hello test environment should be x64, refer too**Step 1: Create C# unit test project and configuration** above.</span></span>
- <span data-ttu-id="0f6c5-427">NugetPackage\build\runtime\ tooproject çalışma dizini altındaki tüm bağımlılık dosyaları kopyalandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="0f6c5-427">Make sure you have copied all dependency files under NugetPackage\build\runtime\ tooproject working directory.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0f6c5-428">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0f6c5-428">Next steps</span></span>

* <span data-ttu-id="0f6c5-429">U-SQL, toolearn bkz [Azure Data Lake Analytics U-SQL dili ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0f6c5-429">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="0f6c5-430">toolog tanılama bilgileri bkz [Azure Data Lake Analytics için tanılama günlükleri erişme](data-lake-analytics-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="0f6c5-430">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span></span>
* <span data-ttu-id="0f6c5-431">toosee daha karmaşık bir sorgu görmek [Azure Data Lake Analytics'i kullanarak Web sitesi günlüklerini çözümleme](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="0f6c5-431">toosee a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="0f6c5-432">tooview iş ayrıntılarını görmek [kullanım iş tarayıcı ve Azure Data Lake Analytics işleri için iş görünümünde](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="0f6c5-432">tooview job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="0f6c5-433">toouse hello köşe yürütme görünümü bkz [kullanım hello köşe yürütme görünümü Visual Studio için Data Lake araçları içinde](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="0f6c5-433">toouse hello vertex execution view, see [Use hello Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
