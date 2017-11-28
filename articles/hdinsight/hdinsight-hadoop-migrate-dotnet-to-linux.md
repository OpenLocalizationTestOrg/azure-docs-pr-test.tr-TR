---
title: "aaaUse .NET Hadoop MapReduce hdınsight'ta Linux tabanlı - Azure ile | Microsoft Docs"
description: "Bilgi nasıl Linux tabanlı Hdınsight üzerinde MapReduce akışla toouse .NET uygulamaları."
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
ms.openlocfilehash: 5a4e6dc1b4dafa8cc40780e3371fa4b8ba3e3d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-toolinux-based-hdinsight"></a><span data-ttu-id="d5130-103">Windows tabanlı Hdınsight .NET çözümleri geçirmek tooLinux tabanlı Hdınsight</span><span class="sxs-lookup"><span data-stu-id="d5130-103">Migrate .NET solutions for Windows-based HDInsight tooLinux-based HDInsight</span></span>

<span data-ttu-id="d5130-104">Linux tabanlı Hdınsight kümeleri kullanım [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="d5130-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="d5130-105">Mono Linux tabanlı Hdınsight ile MapReduce uygulamalar gibi toouse .NET bileşenleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="d5130-105">Mono allows you toouse .NET components such as MapReduce applications with Linux-based HDInsight.</span></span> <span data-ttu-id="d5130-106">Bu belgede, Linux tabanlı Hdınsight üzerinde Mono ile Windows tabanlı Hdınsight kümeleri toowork için toomigrate .NET çözümleri nasıl oluşturulacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d5130-106">In this document, learn how toomigrate .NET solutions created for Windows-based HDInsight clusters toowork with Mono on Linux-based HDInsight.</span></span>

## <a name="mono-compatibility-with-net"></a><span data-ttu-id="d5130-107">.NET ile Mono uyumluluk</span><span class="sxs-lookup"><span data-stu-id="d5130-107">Mono compatibility with .NET</span></span>

<span data-ttu-id="d5130-108">Mono sürüm 4.2.1 Hdınsight sürüm 3.5 ile dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="d5130-108">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="d5130-109">Hdınsight ile dahil Mono hello sürümü hakkında daha fazla bilgi için bkz: [Hdınsight bileşen sürümü](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="d5130-109">For more information on hello version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="d5130-110">tooinstall Mono, belirli bir sürümünü görmek hello [yükleme veya güncelleştirme Mono](hdinsight-hadoop-install-mono.md) belge.</span><span class="sxs-lookup"><span data-stu-id="d5130-110">tooinstall a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="d5130-111">Mono ve .NET uyumluluğu hakkında ayrıntılı bilgi için bkz: Merhaba [Mono uyumluluk (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) belge.</span><span class="sxs-lookup"><span data-stu-id="d5130-111">For detailed information on compatibility between Mono and .NET, see hello [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5130-112">Merhaba SCP.NET framework Mono ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="d5130-112">hello SCP.NET framework is compatible with Mono.</span></span> <span data-ttu-id="d5130-113">SCP.NET Mono ile kullanma hakkında daha fazla bilgi için bkz: [Hdınsight üzerinde Apache Storm için Visual Studio'yu kullanın toodevelop C# topolojileri](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="d5130-113">For more information on using SCP.NET with Mono, see [Use Visual Studio toodevelop C# topologies for Apache Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="automated-portability-analysis"></a><span data-ttu-id="d5130-114">Otomatik taşınabilirlik çözümleme</span><span class="sxs-lookup"><span data-stu-id="d5130-114">Automated portability analysis</span></span>

<span data-ttu-id="d5130-115">Merhaba [.NET taşınabilirlik Çözümleyicisi](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) kullanılan toogenerate uygulama Mono arasındaki uyumsuzluklar raporunu olabilir.</span><span class="sxs-lookup"><span data-stu-id="d5130-115">hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used toogenerate a report of incompatibilities between your application and Mono.</span></span> <span data-ttu-id="d5130-116">Aşağıdaki adımları tooconfigure hello Çözümleyicisi toocheck hello uygulamanız için Mono taşınabilirlik kullanın:</span><span class="sxs-lookup"><span data-stu-id="d5130-116">Use hello following steps tooconfigure hello analyzer toocheck your application for Mono portability:</span></span>

1. <span data-ttu-id="d5130-117">Merhaba yüklemek [.NET taşınabilirlik Çözümleyicisi](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="d5130-117">Install hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span> <span data-ttu-id="d5130-118">Yükleme sırasında Visual Studio toouse hello sürümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="d5130-118">During installation, select hello version of Visual Studio toouse.</span></span>

2. <span data-ttu-id="d5130-119">Visual Studio 2015'ten seçin __Çözümle__ > __taşınabilirlik Çözümleyicisi ayarları__, emin olun __4.5__ hello denetlenir __Mono__  bölümü.</span><span class="sxs-lookup"><span data-stu-id="d5130-119">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in hello __Mono__ section.</span></span>

    ![Mono bölümünde hello Çözümleyicisi ayarları için kontrol 4.5](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    <span data-ttu-id="d5130-121">Seçin __Tamam__ toosave hello yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="d5130-121">Select __OK__ toosave hello configuration.</span></span>

3. <span data-ttu-id="d5130-122">Seçin __analiz__ > __derleme taşınabilirlik analiz__.</span><span class="sxs-lookup"><span data-stu-id="d5130-122">Select __Analyze__ > __Analyze Assembly Portability__.</span></span> <span data-ttu-id="d5130-123">Çözümünüzü içeren hello derleme seçin ve ardından __açık__ toobegin çözümleme.</span><span class="sxs-lookup"><span data-stu-id="d5130-123">Select hello assembly that contains your solution, and then select __Open__ toobegin analysis.</span></span>

4. <span data-ttu-id="d5130-124">Analiz tamamlandığında seçin __Çözümle__ > __analiz raporları görüntülemek__.</span><span class="sxs-lookup"><span data-stu-id="d5130-124">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span></span> <span data-ttu-id="d5130-125">İçinde __taşınabilirlik çözümleme sonuçlarını__seçin __raporunu Aç__ tooopen bir rapor.</span><span class="sxs-lookup"><span data-stu-id="d5130-125">In __Portability Analysis Results__, select __Open report__ tooopen a report.</span></span>

    ![Taşınabilirlik Çözümleyicisi sonuçları iletişim](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> <span data-ttu-id="d5130-127">Merhaba Çözümleyicisi çözümünüzün her sorun catch olamaz.</span><span class="sxs-lookup"><span data-stu-id="d5130-127">hello analyzer cannot catch every problem with your solution.</span></span> <span data-ttu-id="d5130-128">Örneğin, bir dosya yolu `c:\temp\file.txt` Tamam, çünkü Mono Windows üzerinde çalışır ve hello yol bu bağlamda geçerli olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="d5130-128">For example, a file path of `c:\temp\file.txt` is considered OK because Mono runs on Windows and hello path is valid in that context.</span></span> <span data-ttu-id="d5130-129">Ancak, hello yolu Linux platformu üzerinde geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="d5130-129">However, hello path is not valid on a Linux platform.</span></span>

## <a name="manual-portability-analysis"></a><span data-ttu-id="d5130-130">El ile Taşınabilirlik çözümleme</span><span class="sxs-lookup"><span data-stu-id="d5130-130">Manual portability analysis</span></span>

<span data-ttu-id="d5130-131">El ile denetim hello hello bilgileri kullanarak, kodunuzun gerçekleştirmek [uygulama taşınabilirliği (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) belge.</span><span class="sxs-lookup"><span data-stu-id="d5130-131">Perform a manual audit of your code using hello information in hello [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span></span>

## <a name="modify-and-build"></a><span data-ttu-id="d5130-132">Değiştirme ve oluşturma</span><span class="sxs-lookup"><span data-stu-id="d5130-132">Modify and build</span></span>

<span data-ttu-id="d5130-133">Hdınsight için Visual Studio toobuild toouse .NET çözümlerinizi devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5130-133">You can continue toouse Visual Studio toobuild your .NET solutions for HDInsight.</span></span> <span data-ttu-id="d5130-134">Ancak, yapılandırılmış toouse .NET Framework 4.5 hello proje olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="d5130-134">However, you must ensure that hello project is configured toouse .NET Framework 4.5.</span></span>

## <a name="deploy-and-test"></a><span data-ttu-id="d5130-135">Dağıtma ve test etme</span><span class="sxs-lookup"><span data-stu-id="d5130-135">Deploy and test</span></span>

<span data-ttu-id="d5130-136">Merhaba önerileri hello .NET taşınabilirlik Çözümleyicisi veya el ile çözümleme kullanarak çözümünüzü değiştirdiniz. sonra Hdınsight ile test etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d5130-136">Once you have modified your solution using hello recommendations from hello .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span></span> <span data-ttu-id="d5130-137">Linux tabanlı Hdınsight kümesi üzerinde Hello çözüm test ediliyor düzeltildi toobe gereken Zarif sorunlarını olduğunu gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="d5130-137">Testing hello solution on a Linux-based HDInsight cluster may reveal subtle problems that need toobe corrected.</span></span> <span data-ttu-id="d5130-138">Sınama sırasında uygulamanızda ek günlüğü etkinleştirmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="d5130-138">We recommend that you enable additional logging in your application while testing it.</span></span>

<span data-ttu-id="d5130-139">Günlükleri erişme ile ilgili daha fazla bilgi için aşağıdaki belgeleri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="d5130-139">For more information on accessing logs, see hello following documents:</span></span>

* [<span data-ttu-id="d5130-140">Linux tabanlı HDInsight’ta YARN uygulama günlüklerine erişme</span><span class="sxs-lookup"><span data-stu-id="d5130-140">Access YARN application logs on Linux-based HDInsight</span></span>](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a><span data-ttu-id="d5130-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d5130-141">Next steps</span></span>

* [<span data-ttu-id="d5130-142">C# ile MapReduce hdınsight'ta kullanma</span><span class="sxs-lookup"><span data-stu-id="d5130-142">Use C# with MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="d5130-143">C# kullanıcı tanımlı işlevler Hive veya Pig kullanın</span><span class="sxs-lookup"><span data-stu-id="d5130-143">Use C# user defined functions with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="d5130-144">Hdınsight üzerinde Storm için C# topolojileri geliştirme</span><span class="sxs-lookup"><span data-stu-id="d5130-144">Develop C# topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)