---
title: ".NET Hadoop MapReduce hdınsight'ta Linux tabanlı - Azure ile kullanma | Microsoft Docs"
description: "Linux tabanlı Hdınsight üzerinde MapReduce akış için .NET uygulamaları kullanmayı öğrenin."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 6ad188fb752474ff5c7d8a3fb9d609eefe8c7a9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-to-linux-based-hdinsight"></a><span data-ttu-id="9c87a-103">Windows tabanlı Hdınsight Linux tabanlı hdınsight'a için .NET çözümleri geçirme</span><span class="sxs-lookup"><span data-stu-id="9c87a-103">Migrate .NET solutions for Windows-based HDInsight to Linux-based HDInsight</span></span>

<span data-ttu-id="9c87a-104">Linux tabanlı Hdınsight kümeleri kullanım [Mono (https://mono-project.com)](https://mono-project.com) .NET uygulamalarını çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="9c87a-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="9c87a-105">Mono, Linux tabanlı Hdınsight ile MapReduce uygulamalar gibi .NET bileşenleri kullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="9c87a-105">Mono allows you to use .NET components such as MapReduce applications with Linux-based HDInsight.</span></span> <span data-ttu-id="9c87a-106">Bu belgede, Windows tabanlı Hdınsight kümeleri Mono Linux tabanlı Hdınsight üzerinde çalışmak oluşturulan .NET çözümlerin geçirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="9c87a-106">In this document, learn how to migrate .NET solutions created for Windows-based HDInsight clusters to work with Mono on Linux-based HDInsight.</span></span>

## <a name="mono-compatibility-with-net"></a><span data-ttu-id="9c87a-107">.NET ile Mono uyumluluk</span><span class="sxs-lookup"><span data-stu-id="9c87a-107">Mono compatibility with .NET</span></span>

<span data-ttu-id="9c87a-108">Mono sürüm 4.2.1 Hdınsight sürüm 3.5 ile dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="9c87a-108">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="9c87a-109">Hdınsight ile dahil Mono sürümü hakkında daha fazla bilgi için bkz: [Hdınsight bileşen sürümü](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9c87a-109">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="9c87a-110">Mono belirli bir sürümünü yüklemek için bkz: [veya Mono güncelleştirmesini](hdinsight-hadoop-install-mono.md) belge.</span><span class="sxs-lookup"><span data-stu-id="9c87a-110">To install a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="9c87a-111">Mono ve .NET uyumluluğu hakkında ayrıntılı bilgi için bkz: [Mono uyumluluk (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) belge.</span><span class="sxs-lookup"><span data-stu-id="9c87a-111">For detailed information on compatibility between Mono and .NET, see the [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9c87a-112">SCP.NET framework Mono ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="9c87a-112">The SCP.NET framework is compatible with Mono.</span></span> <span data-ttu-id="9c87a-113">SCP.NET Mono ile kullanma hakkında daha fazla bilgi için bkz: [Hdınsight üzerinde Apache Storm için C# topolojileri geliştirme için Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="9c87a-113">For more information on using SCP.NET with Mono, see [Use Visual Studio to develop C# topologies for Apache Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="automated-portability-analysis"></a><span data-ttu-id="9c87a-114">Otomatik taşınabilirlik çözümleme</span><span class="sxs-lookup"><span data-stu-id="9c87a-114">Automated portability analysis</span></span>

<span data-ttu-id="9c87a-115">[.NET taşınabilirlik Çözümleyicisi](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) uygulama Mono arasındaki uyumsuzluklar raporunu oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9c87a-115">The [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used to generate a report of incompatibilities between your application and Mono.</span></span> <span data-ttu-id="9c87a-116">Mono taşınabilirlik için uygulamanızın denetlemek için Çözümleyicisi'ni yapılandırmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="9c87a-116">Use the following steps to configure the analyzer to check your application for Mono portability:</span></span>

1. <span data-ttu-id="9c87a-117">Yükleme [.NET taşınabilirlik Çözümleyicisi](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="9c87a-117">Install the [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span> <span data-ttu-id="9c87a-118">Yükleme sırasında kullanmak için Visual Studio sürümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="9c87a-118">During installation, select the version of Visual Studio to use.</span></span>

2. <span data-ttu-id="9c87a-119">Visual Studio 2015'ten seçin __Çözümle__ > __taşınabilirlik Çözümleyicisi ayarları__, emin olun __4.5__ iade __Mono__ bölümü.</span><span class="sxs-lookup"><span data-stu-id="9c87a-119">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in the __Mono__ section.</span></span>

    ![Mono bölümünde Çözümleyicisi ayarları için kontrol 4.5](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    <span data-ttu-id="9c87a-121">Seçin __Tamam__ yapılandırmayı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="9c87a-121">Select __OK__ to save the configuration.</span></span>

3. <span data-ttu-id="9c87a-122">Seçin __analiz__ > __derleme taşınabilirlik analiz__.</span><span class="sxs-lookup"><span data-stu-id="9c87a-122">Select __Analyze__ > __Analyze Assembly Portability__.</span></span> <span data-ttu-id="9c87a-123">Çözümünüzü içeren derlemenin seçin ve ardından __açık__ çözümleme işlemine başlamak için.</span><span class="sxs-lookup"><span data-stu-id="9c87a-123">Select the assembly that contains your solution, and then select __Open__ to begin analysis.</span></span>

4. <span data-ttu-id="9c87a-124">Analiz tamamlandığında seçin __Çözümle__ > __analiz raporları görüntülemek__.</span><span class="sxs-lookup"><span data-stu-id="9c87a-124">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span></span> <span data-ttu-id="9c87a-125">İçinde __taşınabilirlik çözümleme sonuçlarını__seçin __raporunu Aç__ bir raporu açın.</span><span class="sxs-lookup"><span data-stu-id="9c87a-125">In __Portability Analysis Results__, select __Open report__ to open a report.</span></span>

    ![Taşınabilirlik Çözümleyicisi sonuçları iletişim](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> <span data-ttu-id="9c87a-127">Çözümleyici çözümünüzün her sorun catch olamaz.</span><span class="sxs-lookup"><span data-stu-id="9c87a-127">The analyzer cannot catch every problem with your solution.</span></span> <span data-ttu-id="9c87a-128">Örneğin, bir dosya yolu `c:\temp\file.txt` Tamam, çünkü Mono Windows üzerinde çalışır ve yol bu bağlamda geçerli olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="9c87a-128">For example, a file path of `c:\temp\file.txt` is considered OK because Mono runs on Windows and the path is valid in that context.</span></span> <span data-ttu-id="9c87a-129">Ancak, yolun bir Linux platformda geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="9c87a-129">However, the path is not valid on a Linux platform.</span></span>

## <a name="manual-portability-analysis"></a><span data-ttu-id="9c87a-130">El ile Taşınabilirlik çözümleme</span><span class="sxs-lookup"><span data-stu-id="9c87a-130">Manual portability analysis</span></span>

<span data-ttu-id="9c87a-131">El ile denetim bilgileri kullanarak, kodunuzun gerçekleştirmek [uygulama taşınabilirliği (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) belge.</span><span class="sxs-lookup"><span data-stu-id="9c87a-131">Perform a manual audit of your code using the information in the [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span></span>

## <a name="modify-and-build"></a><span data-ttu-id="9c87a-132">Değiştirme ve oluşturma</span><span class="sxs-lookup"><span data-stu-id="9c87a-132">Modify and build</span></span>

<span data-ttu-id="9c87a-133">Visual Studio için Hdınsight .NET çözümlerinizi oluşturmaya kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c87a-133">You can continue to use Visual Studio to build your .NET solutions for HDInsight.</span></span> <span data-ttu-id="9c87a-134">Ancak projeyi .NET Framework 4.5 kullanacak şekilde yapılandırıldığından emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c87a-134">However, you must ensure that the project is configured to use .NET Framework 4.5.</span></span>

## <a name="deploy-and-test"></a><span data-ttu-id="9c87a-135">Dağıtma ve test etme</span><span class="sxs-lookup"><span data-stu-id="9c87a-135">Deploy and test</span></span>

<span data-ttu-id="9c87a-136">.NET taşınabilirlik Çözümleyicisi veya el ile çözümleme önerileri kullanarak çözümünüzü değiştirdiniz. sonra Hdınsight ile test etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c87a-136">Once you have modified your solution using the recommendations from the .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span></span> <span data-ttu-id="9c87a-137">Linux tabanlı Hdınsight kümesi çözümü test düzeltilmesi gereken Zarif sorun olduğunu gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="9c87a-137">Testing the solution on a Linux-based HDInsight cluster may reveal subtle problems that need to be corrected.</span></span> <span data-ttu-id="9c87a-138">Sınama sırasında uygulamanızda ek günlüğü etkinleştirmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="9c87a-138">We recommend that you enable additional logging in your application while testing it.</span></span>

<span data-ttu-id="9c87a-139">Günlükleri erişme ile ilgili daha fazla bilgi için aşağıdaki belgelere bakın:</span><span class="sxs-lookup"><span data-stu-id="9c87a-139">For more information on accessing logs, see the following documents:</span></span>

* [<span data-ttu-id="9c87a-140">Linux tabanlı HDInsight’ta YARN uygulama günlüklerine erişme</span><span class="sxs-lookup"><span data-stu-id="9c87a-140">Access YARN application logs on Linux-based HDInsight</span></span>](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a><span data-ttu-id="9c87a-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9c87a-141">Next steps</span></span>

* [<span data-ttu-id="9c87a-142">C# ile MapReduce hdınsight'ta kullanma</span><span class="sxs-lookup"><span data-stu-id="9c87a-142">Use C# with MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="9c87a-143">C# kullanıcı tanımlı işlevler Hive veya Pig kullanın</span><span class="sxs-lookup"><span data-stu-id="9c87a-143">Use C# user defined functions with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="9c87a-144">Hdınsight üzerinde Storm için C# topolojileri geliştirme</span><span class="sxs-lookup"><span data-stu-id="9c87a-144">Develop C# topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)