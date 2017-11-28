---
title: "Visual Studio ve C# - Azure Hdınsight ile aaaApache Storm topolojileri | Microsoft Docs"
description: "Bilgi nasıl toocreate Storm topolojilerini C#. Basit word count topolojisi için Visual Studio hello Hadoop araçları kullanarak Visual Studio'da oluşturun."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 380d804f-a8c5-4b20-9762-593ec4da5a0d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: larryfr
ms.openlocfilehash: b3fb01a4dda144fd7fb4141e624e31e667f93753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-hello-data-lake-tools-for-visual-studio"></a><span data-ttu-id="6adc8-104">Visual Studio için hello Data Lake araçları kullanarak Apache Storm için C# topolojileri geliştirme</span><span class="sxs-lookup"><span data-stu-id="6adc8-104">Develop C# topologies for Apache Storm by using hello Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="6adc8-105">Nasıl toocreate hello Azure Data Lake (Hadoop) kullanarak C# Storm topolojisini için Visual Studio Araçları hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="6adc8-105">Learn how toocreate a C# Storm topology by using hello Azure Data Lake (Hadoop) tools for Visual Studio.</span></span> <span data-ttu-id="6adc8-106">Bu belge Visual Studio'da bir Storm projesi oluşturma, yerel olarak test etme ve Azure Hdınsight kümesi üzerinde Apache Storm tooan dağıtma hello işleminde size yol göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-106">This document walks through hello process of creating a Storm project in Visual Studio, testing it locally, and deploying it tooan Apache Storm on Azure HDInsight cluster.</span></span>

<span data-ttu-id="6adc8-107">Da bilgi nasıl C# ve Java bileşenlerini kullanan karma topolojiler toocreate.</span><span class="sxs-lookup"><span data-stu-id="6adc8-107">You also learn how toocreate hybrid topologies that use C# and Java components.</span></span>

> [!NOTE]
> <span data-ttu-id="6adc8-108">Visual Studio ile Windows geliştirme ortamına Hello adımları bu belgede Bel hello derlenmiş proje gönderilen tooeither bir Linux veya Windows tabanlı Hdınsight kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-108">While hello steps in this document rely on a Windows development environment with Visual Studio, hello compiled project can be submitted tooeither a Linux or Windows-based HDInsight cluster.</span></span> <span data-ttu-id="6adc8-109">Yalnızca Linux tabanlı kümelerde 28 Ekim 2016'dan sonra oluşturulan SCP.NET topolojileri destekler.</span><span class="sxs-lookup"><span data-stu-id="6adc8-109">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="6adc8-110">toouse C# topolojisi Linux tabanlı bir küme ile Merhaba Microsoft.SCP.Net.SDK NuGet paketi, proje tooversion 0.10.0.6 tarafından kullanılan veya üzeri güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-110">toouse a C# topology with a Linux-based cluster, you must update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or later.</span></span> <span data-ttu-id="6adc8-111">Merhaba hello paketin sürümü yüklü Hdınsight üzerinde Storm hello ana sürümüne de eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-111">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span>

| <span data-ttu-id="6adc8-112">Hdınsight sürümü</span><span class="sxs-lookup"><span data-stu-id="6adc8-112">HDInsight version</span></span> | <span data-ttu-id="6adc8-113">Storm sürüm</span><span class="sxs-lookup"><span data-stu-id="6adc8-113">Storm version</span></span> | <span data-ttu-id="6adc8-114">SCP.NET sürüm</span><span class="sxs-lookup"><span data-stu-id="6adc8-114">SCP.NET version</span></span> | <span data-ttu-id="6adc8-115">Varsayılan Mono sürümü</span><span class="sxs-lookup"><span data-stu-id="6adc8-115">Default Mono version</span></span> |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| <span data-ttu-id="6adc8-116">3.3</span><span class="sxs-lookup"><span data-stu-id="6adc8-116">3.3</span></span> |<span data-ttu-id="6adc8-117">0.10.x</span><span class="sxs-lookup"><span data-stu-id="6adc8-117">0.10.x</span></span> |<span data-ttu-id="6adc8-118">0.10.x.x</span><span class="sxs-lookup"><span data-stu-id="6adc8-118">0.10.x.x</span></span></br><span data-ttu-id="6adc8-119">(yalnızca Windows tabanlı Hdınsight üzerinde)</span><span class="sxs-lookup"><span data-stu-id="6adc8-119">(only on Windows-based HDInsight)</span></span> | <span data-ttu-id="6adc8-120">NA</span><span class="sxs-lookup"><span data-stu-id="6adc8-120">NA</span></span> |
| <span data-ttu-id="6adc8-121">3.4</span><span class="sxs-lookup"><span data-stu-id="6adc8-121">3.4</span></span> | <span data-ttu-id="6adc8-122">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="6adc8-122">0.10.0.x</span></span> | <span data-ttu-id="6adc8-123">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="6adc8-123">0.10.0.x</span></span> | <span data-ttu-id="6adc8-124">3.2.8</span><span class="sxs-lookup"><span data-stu-id="6adc8-124">3.2.8</span></span> |
| <span data-ttu-id="6adc8-125">3,5</span><span class="sxs-lookup"><span data-stu-id="6adc8-125">3.5</span></span> | <span data-ttu-id="6adc8-126">1.0.2.x</span><span class="sxs-lookup"><span data-stu-id="6adc8-126">1.0.2.x</span></span> | <span data-ttu-id="6adc8-127">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="6adc8-127">1.0.0.x</span></span> | <span data-ttu-id="6adc8-128">4.2.1</span><span class="sxs-lookup"><span data-stu-id="6adc8-128">4.2.1</span></span> |
| <span data-ttu-id="6adc8-129">3.6</span><span class="sxs-lookup"><span data-stu-id="6adc8-129">3.6</span></span> | <span data-ttu-id="6adc8-130">1.1.0.x</span><span class="sxs-lookup"><span data-stu-id="6adc8-130">1.1.0.x</span></span> | <span data-ttu-id="6adc8-131">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="6adc8-131">1.0.0.x</span></span> | <span data-ttu-id="6adc8-132">4.2.8</span><span class="sxs-lookup"><span data-stu-id="6adc8-132">4.2.8</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="6adc8-133">C# topolojileri Linux tabanlı kümelerde .NET 4.5 kullanın ve hello Hdınsight kümesinde Mono toorun kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-133">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="6adc8-134">Denetleme [Mono Uyumluluk](http://www.mono-project.com/docs/about-mono/compatibility/) olası uyumsuzlukları için.</span><span class="sxs-lookup"><span data-stu-id="6adc8-134">Check [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) for potential incompatibilities.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="6adc8-135">Visual Studio yükleme</span><span class="sxs-lookup"><span data-stu-id="6adc8-135">Install Visual Studio</span></span>

<span data-ttu-id="6adc8-136">Visual Studio sürümleri aşağıdaki hello birini kullanarak C# topolojileri SCP.NET ile geliştirme yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6adc8-136">You can develop C# topologies with SCP.NET by using one of hello following versions of Visual Studio:</span></span>

* <span data-ttu-id="6adc8-137">Visual Studio 2012 ile [güncelleştirme 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="6adc8-137">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

* <span data-ttu-id="6adc8-138">Visual Studio 2013 [güncelleştirme 4](http://www.microsoft.com/download/details.aspx?id=44921) veya [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="6adc8-138">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>

* <span data-ttu-id="6adc8-139">Visual Studio 2015 veya [Visual Studio 2015 topluluk](https://go.microsoft.com/fwlink/?LinkId=532606)</span><span class="sxs-lookup"><span data-stu-id="6adc8-139">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span></span>

* <span data-ttu-id="6adc8-140">Visual Studio 2017 (herhangi bir sürümünü)</span><span class="sxs-lookup"><span data-stu-id="6adc8-140">Visual Studio 2017 (any edition)</span></span>

## <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="6adc8-141">Visual Studio için yükleme Data Lake araçları</span><span class="sxs-lookup"><span data-stu-id="6adc8-141">Install Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="6adc8-142">Visual Studio için Data Lake araçları tooinstall izleyin hello adımlarda [Visual Studio için Data Lake araçları kullanarak çalışmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6adc8-142">tooinstall Data Lake tools for Visual Studio, follow hello steps in [Get started using Data Lake tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

## <a name="install-java"></a><span data-ttu-id="6adc8-143">Java'yı yükleme</span><span class="sxs-lookup"><span data-stu-id="6adc8-143">Install Java</span></span>

<span data-ttu-id="6adc8-144">Visual Studio'dan bir Storm topolojisinin gönderdiğinizde, SCP.NET hello topoloji ve bağımlılıklarını içeren bir zip dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6adc8-144">When you submit a Storm topology from Visual Studio, SCP.NET generates a zip file that contains hello topology and dependencies.</span></span> <span data-ttu-id="6adc8-145">Java kullanılan toocreate olduğundan daha Linux tabanlı kümelerde ile uyumlu bir biçimde kullandığından bu dosyaları zip.</span><span class="sxs-lookup"><span data-stu-id="6adc8-145">Java is used toocreate these zip files, because it uses a format that is more compatible with Linux-based clusters.</span></span>

1. <span data-ttu-id="6adc8-146">Geliştirme ortamınızı Hello Java Geliştirme Seti (JDK) 7 veya sonraki bir sürümü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6adc8-146">Install hello Java Developer Kit (JDK) 7 or later on your development environment.</span></span> <span data-ttu-id="6adc8-147">Alabileceğiniz Oracle JDK gelen hello [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="6adc8-147">You can get hello Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span> <span data-ttu-id="6adc8-148">Aynı zamanda [diğer Java dağıtımları](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="6adc8-148">You can also use [other Java distributions](http://openjdk.java.net/).</span></span>

2. <span data-ttu-id="6adc8-149">Merhaba `JAVA_HOME` Java içeren ortam değişkeni gereken noktası toohello dizini.</span><span class="sxs-lookup"><span data-stu-id="6adc8-149">hello `JAVA_HOME` environment variable must point toohello directory that contains Java.</span></span>

3. <span data-ttu-id="6adc8-150">Merhaba `PATH` ortam değişkeni hello içermelidir `%JAVA_HOME%\bin` dizin.</span><span class="sxs-lookup"><span data-stu-id="6adc8-150">hello `PATH` environment variable must include hello `%JAVA_HOME%\bin` directory.</span></span>

<span data-ttu-id="6adc8-151">Konsol uygulaması Java ve hello JDK düzgün yüklendiğini C# tooverify aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6adc8-151">You can use hello following C# console application tooverify that Java and hello JDK are correctly installed:</span></span>

```csharp
using System;
using System.IO;
namespace ConsoleApplication2
{
   class Program
   {
       static void Main(string[] args)
       {
           string javaHome = Environment.GetEnvironmentVariable(“JAVA_HOME”);
           if (!string.IsNullOrEmpty(javaHome))
           {
               string jarExe = Path.Combine(javaHome + @”\bin”, “jar.exe”);
               if (File.Exists(jarExe))
               {
                   Console.WriteLine(“JAVA Is Installed properly”);
                    return;
               }
               else
               {
                   Console.WriteLine(“A valid JAVA JDK is not found. Looks like JRE is installed instead of JDK.”);
               }
           }
           else
           {
             Console.WriteLine(“A valid JAVA JDK is not found. JAVA_HOME environment variable is not set.”);
           }
       }  
   }
}
```

## <a name="storm-templates"></a><span data-ttu-id="6adc8-152">Storm şablonları</span><span class="sxs-lookup"><span data-stu-id="6adc8-152">Storm templates</span></span>

<span data-ttu-id="6adc8-153">Visual Studio için Data Lake araçları Hello şablonları aşağıdaki hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="6adc8-153">hello Data Lake tools for Visual Studio provide hello following templates:</span></span>

| <span data-ttu-id="6adc8-154">Proje türü</span><span class="sxs-lookup"><span data-stu-id="6adc8-154">Project type</span></span> | <span data-ttu-id="6adc8-155">Gösterir</span><span class="sxs-lookup"><span data-stu-id="6adc8-155">Demonstrates</span></span> |
| --- | --- |
| <span data-ttu-id="6adc8-156">Storm uygulaması</span><span class="sxs-lookup"><span data-stu-id="6adc8-156">Storm Application</span></span> |<span data-ttu-id="6adc8-157">Boş bir Storm topolojisini projesi.</span><span class="sxs-lookup"><span data-stu-id="6adc8-157">An empty Storm topology project.</span></span> |
| <span data-ttu-id="6adc8-158">Storm Azure SQL yazıcı örnek</span><span class="sxs-lookup"><span data-stu-id="6adc8-158">Storm Azure SQL Writer Sample</span></span> |<span data-ttu-id="6adc8-159">Nasıl toowrite tooAzure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="6adc8-159">How toowrite tooAzure SQL Database.</span></span> |
| <span data-ttu-id="6adc8-160">Storm Azure Cosmos DB okuyucu örneği</span><span class="sxs-lookup"><span data-stu-id="6adc8-160">Storm Azure Cosmos DB Reader Sample</span></span> |<span data-ttu-id="6adc8-161">Nasıl tooread Azure Cosmos DB'den.</span><span class="sxs-lookup"><span data-stu-id="6adc8-161">How tooread from Azure Cosmos DB.</span></span> |
| <span data-ttu-id="6adc8-162">Storm Azure Cosmos DB yazan örnek</span><span class="sxs-lookup"><span data-stu-id="6adc8-162">Storm Azure Cosmos DB Writer Sample</span></span> |<span data-ttu-id="6adc8-163">Nasıl toowrite tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6adc8-163">How toowrite tooAzure Cosmos DB.</span></span> |
| <span data-ttu-id="6adc8-164">Storm EventHub okuyucu örneği</span><span class="sxs-lookup"><span data-stu-id="6adc8-164">Storm EventHub Reader Sample</span></span> |<span data-ttu-id="6adc8-165">Nasıl tooread Azure Event hubs'tan.</span><span class="sxs-lookup"><span data-stu-id="6adc8-165">How tooread from Azure Event Hubs.</span></span> |
| <span data-ttu-id="6adc8-166">Storm EventHub yazan örnek</span><span class="sxs-lookup"><span data-stu-id="6adc8-166">Storm EventHub Writer Sample</span></span> |<span data-ttu-id="6adc8-167">Nasıl toowrite tooAzure olay hub'ları.</span><span class="sxs-lookup"><span data-stu-id="6adc8-167">How toowrite tooAzure Event Hubs.</span></span> |
| <span data-ttu-id="6adc8-168">Storm HBase okuyucu örneği</span><span class="sxs-lookup"><span data-stu-id="6adc8-168">Storm HBase Reader Sample</span></span> |<span data-ttu-id="6adc8-169">Hdınsight'ta HBase gelen tooread nasıl kümeleri.</span><span class="sxs-lookup"><span data-stu-id="6adc8-169">How tooread from HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="6adc8-170">Storm HBase yazan örnek</span><span class="sxs-lookup"><span data-stu-id="6adc8-170">Storm HBase Writer Sample</span></span> |<span data-ttu-id="6adc8-171">Nasıl toowrite tooHBase hdınsight kümeleri.</span><span class="sxs-lookup"><span data-stu-id="6adc8-171">How toowrite tooHBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="6adc8-172">Storm karma örnek</span><span class="sxs-lookup"><span data-stu-id="6adc8-172">Storm Hybrid Sample</span></span> |<span data-ttu-id="6adc8-173">Nasıl toouse bir Java bileşeni.</span><span class="sxs-lookup"><span data-stu-id="6adc8-173">How toouse a Java component.</span></span> |
| <span data-ttu-id="6adc8-174">Storm örnek</span><span class="sxs-lookup"><span data-stu-id="6adc8-174">Storm Sample</span></span> |<span data-ttu-id="6adc8-175">Temel word count topolojisi.</span><span class="sxs-lookup"><span data-stu-id="6adc8-175">A basic word count topology.</span></span> |

> [!WARNING]
> <span data-ttu-id="6adc8-176">Tüm Şablonları Linux tabanlı Hdınsight ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="6adc8-176">Not all templates will work with Linux-based HDInsight.</span></span> <span data-ttu-id="6adc8-177">Merhaba şablonları tarafından kullanılan Nuget paketleri Mono ile uyumlu olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-177">Nuget packages used by hello templates may not be compatible with Mono.</span></span> <span data-ttu-id="6adc8-178">Merhaba denetleyin [Mono Uyumluluk](http://www.mono-project.com/docs/about-mono/compatibility/) belge ve hello kullan [.NET taşınabilirlik Çözümleyicisi](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify olası sorunları.</span><span class="sxs-lookup"><span data-stu-id="6adc8-178">Check hello [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document and use hello [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify potential problems.</span></span>

<span data-ttu-id="6adc8-179">Bu belgedeki Hello adımlarda hello temel Storm uygulaması proje türü toocreate bir topoloji kullanın.</span><span class="sxs-lookup"><span data-stu-id="6adc8-179">In hello steps in this document, you use hello basic Storm Application project type toocreate a topology.</span></span>

### <a name="hbase-templates-notes"></a><span data-ttu-id="6adc8-180">HBase şablonları notları</span><span class="sxs-lookup"><span data-stu-id="6adc8-180">HBase templates notes</span></span>

<span data-ttu-id="6adc8-181">Merhaba HBase okuyucu ve yazıcı şablonları hello HBase REST API değil hello HBase Java API, Hdınsight kümesinde bir HBase ile toocommunicate kullanın.</span><span class="sxs-lookup"><span data-stu-id="6adc8-181">hello HBase reader and writer templates use hello HBase REST API, not hello HBase Java API, toocommunicate with an HBase on HDInsight cluster.</span></span>

### <a name="eventhub-templates-notes"></a><span data-ttu-id="6adc8-182">EventHub şablonları notları</span><span class="sxs-lookup"><span data-stu-id="6adc8-182">EventHub templates notes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6adc8-183">Merhaba Java tabanlı EventHub spout EventHub okuyucu şablon sürüm 3.5 veya sonrasını hdınsight'ta Storm çalışmayabilir hello ile birlikte gelen bileşeni.</span><span class="sxs-lookup"><span data-stu-id="6adc8-183">hello Java-based EventHub spout component included with hello EventHub Reader template may not work with Storm on HDInsight version 3.5 or later.</span></span> <span data-ttu-id="6adc8-184">Bu bileşen güncelleştirilmiş bir sürümü kullanılabilir [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span><span class="sxs-lookup"><span data-stu-id="6adc8-184">An updated version of this component is available at [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span></span>

<span data-ttu-id="6adc8-185">Bu kullanan örnek bir topoloji için bkz: bileşen ve Hdınsight 3.5 üzerinde Storm ile works [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="6adc8-185">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

## <a name="create-a-c-topology"></a><span data-ttu-id="6adc8-186">Bir C# topolojisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="6adc8-186">Create a C# topology</span></span>

1. <span data-ttu-id="6adc8-187">Visual Studio'ni açın, **dosya** > **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-187">Open Visual Studio, select **File** > **New**, and then select **Project**.</span></span>

2. <span data-ttu-id="6adc8-188">Merhaba gelen **yeni proje** penceresinde genişletin **yüklü** > **şablonları**seçip **Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-188">From hello **New Project** window, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span></span> <span data-ttu-id="6adc8-189">Merhaba şablonları listesinden **Storm uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-189">From hello list of templates, select **Storm Application**.</span></span> <span data-ttu-id="6adc8-190">Merhaba ekranında Hello altındaki girin **WordCount** Merhaba uygulaması hello adından farklı.</span><span class="sxs-lookup"><span data-stu-id="6adc8-190">At hello bottom of hello screen, enter **WordCount** as hello name of hello application.</span></span>

    ![Yeni Proje penceresinin ekran penceresi](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. <span data-ttu-id="6adc8-192">Başlangıç projesi oluşturduktan sonra aşağıdaki dosyaları hello olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="6adc8-192">After you have created hello project, you should have hello following files:</span></span>

   * <span data-ttu-id="6adc8-193">**Program.cs**: hello topoloji projeniz için bu dosyayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6adc8-193">**Program.cs**: This file defines hello topology for your project.</span></span> <span data-ttu-id="6adc8-194">Bir spout ve bir Cıvata oluşan bir varsayılan topolojisi varsayılan olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6adc8-194">A default topology that consists of one spout and one bolt is created by default.</span></span>

   * <span data-ttu-id="6adc8-195">**Spout.cs**: rastgele sayılar yayar bir örnek spout.</span><span class="sxs-lookup"><span data-stu-id="6adc8-195">**Spout.cs**: An example spout that emits random numbers.</span></span>

   * <span data-ttu-id="6adc8-196">**Bolt.cs**: hello spout'un gösterilen sayıların sayısı tutan bir örnek Cıvata.</span><span class="sxs-lookup"><span data-stu-id="6adc8-196">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by hello spout.</span></span>

     <span data-ttu-id="6adc8-197">Başlangıç projesi oluşturduğunuzda, NuGet yüklemeleri son hello [SCP.NET paket](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span><span class="sxs-lookup"><span data-stu-id="6adc8-197">When you create hello project, NuGet downloads hello latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span></span>

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-hello-spout"></a><span data-ttu-id="6adc8-198">Uygulama hello spout</span><span class="sxs-lookup"><span data-stu-id="6adc8-198">Implement hello spout</span></span>

1. <span data-ttu-id="6adc8-199">Açık **Spout.cs**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-199">Open **Spout.cs**.</span></span> <span data-ttu-id="6adc8-200">Spout'lar, bir dış kaynaktan topolojisinde kullanılan tooread verilerdir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-200">Spouts are used tooread data in a topology from an external source.</span></span> <span data-ttu-id="6adc8-201">bir spout için Hello ana bileşeni vardır:</span><span class="sxs-lookup"><span data-stu-id="6adc8-201">hello main components for a spout are:</span></span>

   * <span data-ttu-id="6adc8-202">**NextTuple**: Merhaba spout tooemit yeni diziler izin verildiğinde Storm tarafından çağrılır.</span><span class="sxs-lookup"><span data-stu-id="6adc8-202">**NextTuple**: Called by Storm when hello spout is allowed tooemit new tuples.</span></span>

   * <span data-ttu-id="6adc8-203">**ACK** (yalnızca işlem topolojisi): hello spout gönderilen diziler için başlangıç topolojisinde başka bileşenler tarafından başlatılan onayları işler.</span><span class="sxs-lookup"><span data-stu-id="6adc8-203">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in hello topology for tuples sent from hello spout.</span></span> <span data-ttu-id="6adc8-204">Bir tanımlama grubu aktarımının aşağı akış bileşenleri tarafından başarıyla işlendi bilmeniz hello spout olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="6adc8-204">Acknowledging a tuple lets hello spout know that it was processed successfully by downstream components.</span></span>

   * <span data-ttu-id="6adc8-205">**Başarısız** (yalnızca işlem topolojisi): işleme, başarısız hello topoloji içindeki diğer bileşenlere işleme tanımlama grubu.</span><span class="sxs-lookup"><span data-stu-id="6adc8-205">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in hello topology.</span></span> <span data-ttu-id="6adc8-206">Başarısız yöntemi uygulama verir toore-yeniden işlenebilir böylece hello tanımlama grubu yayma.</span><span class="sxs-lookup"><span data-stu-id="6adc8-206">Implementing a Fail method allows you toore-emit hello tuple so that it can be processed again.</span></span>

2. <span data-ttu-id="6adc8-207">Merhaba Hello içeriğini değiştirin **Spout** metin aşağıdaki hello sınıfıyla.</span><span class="sxs-lookup"><span data-stu-id="6adc8-207">Replace hello contents of hello **Spout** class with hello following text.</span></span> <span data-ttu-id="6adc8-208">Bu spout bir cümle rastgele hello topoloji yayar.</span><span class="sxs-lookup"><span data-stu-id="6adc8-208">This spout randomly emits a sentence into hello topology.</span></span>

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "hello cow jumped over hello moon",
        "an apple a day keeps hello doctor away",
        "four score and seven years ago",
        "snow white and hello seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set hello instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // hello schema for hello default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of hello spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // hello sentence toobe emitted
        string sentence;

        // Get a random sentence
        sentence = sentences[r.Next(0, sentences.Length - 1)];
        Context.Logger.Info("Emit: {0}", sentence);
        // Emit it
        this.ctx.Emit(new Values(sentence));

        Context.Logger.Info("NextTuple exit");
    }

    public void Ack(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }
    ```

### <a name="implement-hello-bolts"></a><span data-ttu-id="6adc8-209">Merhaba Cıvatalar uygulama</span><span class="sxs-lookup"><span data-stu-id="6adc8-209">Implement hello bolts</span></span>

1. <span data-ttu-id="6adc8-210">Merhaba varolan silme **Bolt.cs** hello proje dosyasından.</span><span class="sxs-lookup"><span data-stu-id="6adc8-210">Delete hello existing **Bolt.cs** file from hello project.</span></span>

2. <span data-ttu-id="6adc8-211">İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve seçin **Ekle** > **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-211">In **Solution Explorer**, right-click hello project, and select **Add** > **New item**.</span></span> <span data-ttu-id="6adc8-212">Merhaba listesinden **Storm Cıvata**ve girin **Splitter.cs** hello adı.</span><span class="sxs-lookup"><span data-stu-id="6adc8-212">From hello list, select **Storm Bolt**, and enter **Splitter.cs** as hello name.</span></span> <span data-ttu-id="6adc8-213">İkinci Cıvata adlı bu işlem toocreate yineleyin **Counter.cs**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-213">Repeat this process toocreate a second bolt named **Counter.cs**.</span></span>

   * <span data-ttu-id="6adc8-214">**Splitter.cs**: cümleleri tek tek sözcüklere böler ve yeni akış sözcüklerin yayar Cıvata uygular.</span><span class="sxs-lookup"><span data-stu-id="6adc8-214">**Splitter.cs**: Implements a bolt that splits sentences into individual words, and emits a new stream of words.</span></span>

   * <span data-ttu-id="6adc8-215">**Counter.cs**: her sözcüğün sayar ve sözcükleri ve hello sayısı her sözcüğün için yeni bir akış yayar Cıvata uygular.</span><span class="sxs-lookup"><span data-stu-id="6adc8-215">**Counter.cs**: Implements a bolt that counts each word, and emits a new stream of words and hello count for each word.</span></span>

     > [!NOTE]
     > <span data-ttu-id="6adc8-216">Bu Cıvatalar toostreams okuyup, ancak bir veritabanı veya hizmet gibi kaynakları ile Cıvata toocommunicate de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6adc8-216">These bolts read and write toostreams, but you can also use a bolt toocommunicate with sources such as a database or service.</span></span>

3. <span data-ttu-id="6adc8-217">Açık **Splitter.cs**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-217">Open **Splitter.cs**.</span></span> <span data-ttu-id="6adc8-218">Varsayılan olarak yalnızca bir yöntemi vardır: **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-218">It has only one method by default: **Execute**.</span></span> <span data-ttu-id="6adc8-219">Merhaba Cıvata işlemek için bir tanımlama grubu aldığında hello yürütme yöntemi adı verilir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-219">hello Execute method is called when hello bolt receives a tuple for processing.</span></span> <span data-ttu-id="6adc8-220">Burada, okuma ve gelen diziler işlemek ve giden tanımlama grubu yayma.</span><span class="sxs-lookup"><span data-stu-id="6adc8-220">Here, you can read and process incoming tuples, and emit outbound tuples.</span></span>

4. <span data-ttu-id="6adc8-221">Merhaba Hello içeriğini değiştirin **Bölümlendirici** koddan hello sınıfıyla:</span><span class="sxs-lookup"><span data-stu-id="6adc8-221">Replace hello contents of hello **Splitter** class with hello following code:</span></span>

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (hello sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (hello word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of hello bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello sentence from hello tuple
        string sentence = tuple.GetString(0);
        // Split at space characters
        foreach (string word in sentence.Split(' '))
        {
            Context.Logger.Info("Emit: {0}", word);
            //Emit each word
            this.ctx.Emit(new Values(word));
        }

        Context.Logger.Info("Execute exit");
    }
    ```

5. <span data-ttu-id="6adc8-222">Açık **Counter.cs**ve hello sınıfı içeriği hello şununla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="6adc8-222">Open **Counter.cs**, and replace hello class contents with hello following:</span></span>

    ```csharp
    private Context ctx;

    // Dictionary for holding words and counts
    private Dictionary<string, int> counts = new Dictionary<string, int>();

    // Constructor
    public Counter(Context ctx)
    {
        Context.Logger.Info("Counter constructor called");
        // Set instance context
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string field - hello word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - hello word and hello word count
        outputSchema.Add("default", new List<Type>() { typeof(string), typeof(int) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance
    public static Counter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Counter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello word from hello tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for hello word in hello dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment hello count
        count++;
        // Update hello count in hello dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit hello word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-hello-topology"></a><span data-ttu-id="6adc8-223">Merhaba topolojisi tanımlayın</span><span class="sxs-lookup"><span data-stu-id="6adc8-223">Define hello topology</span></span>

<span data-ttu-id="6adc8-224">Spout'lar ve Cıvatalar bileşenler arasında hello veri akışını tanımlayan bir grafik halinde düzenlenir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-224">Spouts and bolts are arranged in a graph, which defines how hello data flows between components.</span></span> <span data-ttu-id="6adc8-225">Bu topoloji, hello grafiği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="6adc8-225">For this topology, hello graph is as follows:</span></span>

![Bileşenleri nasıl düzenlenir diyagramı](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

<span data-ttu-id="6adc8-227">Cümleleri hello spout yayılan ve hello Bölümlendirici Cıvata, dağıtılmış tooinstances demektir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-227">Sentences are emitted from hello spout, and are distributed tooinstances of hello Splitter bolt.</span></span> <span data-ttu-id="6adc8-228">Merhaba Bölümlendirici Cıvata hello cümleleri dağıtılmış toohello sayaç Cıvata olan sözcüklere keser.</span><span class="sxs-lookup"><span data-stu-id="6adc8-228">hello Splitter bolt breaks hello sentences into words, which are distributed toohello Counter bolt.</span></span>

<span data-ttu-id="6adc8-229">Sözcük sayısını yerel olarak hello sayaç örneğinde tutulmadığından toomake belirli kelimeleri toohello akış emin istiyoruz aynı sayacı Cıvata örneği.</span><span class="sxs-lookup"><span data-stu-id="6adc8-229">Because word count is held locally in hello Counter instance, we want toomake sure that specific words flow toohello same Counter bolt instance.</span></span> <span data-ttu-id="6adc8-230">Her bir örnek, belirli kelimeleri izler.</span><span class="sxs-lookup"><span data-stu-id="6adc8-230">Each instance keeps track of specific words.</span></span> <span data-ttu-id="6adc8-231">Merhaba Bölümlendirici Cıvata hiçbir durumunu koruyan olduğundan, gerçekten hello Bölümlendirici hangi örneğinin hangi tümceyi alır önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-231">Since hello Splitter bolt maintains no state, it really doesn't matter which instance of hello splitter receives which sentence.</span></span>

<span data-ttu-id="6adc8-232">Açık **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-232">Open **Program.cs**.</span></span> <span data-ttu-id="6adc8-233">Merhaba önemli yöntemi **GetTopologyBuilder**, hangi olduğu kullanılan toodefine hello topoloji tooStorm gönderildi.</span><span class="sxs-lookup"><span data-stu-id="6adc8-233">hello important method is **GetTopologyBuilder**, which is used toodefine hello topology that is submitted tooStorm.</span></span> <span data-ttu-id="6adc8-234">Merhaba Değiştir **GetTopologyBuilder** kod tooimplement hello topoloji daha önce açıklanan aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="6adc8-234">Replace hello contents of **GetTopologyBuilder** with hello following code tooimplement hello topology described previously:</span></span>

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add hello spout toohello topology.
// Name hello component 'sentences'
// Name hello field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add hello splitter bolt toohello topology.
// Name hello component 'splitter'
// Name hello field that is emitted 'word'
// Use suffleGrouping toodistribute incoming tuples
//   from hello 'sentences' spout across instances
//   of hello splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add hello counter bolt toohello topology.
// Name hello component 'counter'
// Name hello fields that are emitted 'word' and 'count'
// Use fieldsGrouping tooensure that tuples are routed
//   toocounter instances based on hello contents of field
//   position 0 (hello word). This could also have been
//   List<string>(){"word"}.
//   This ensures that hello word 'jumped', for example, will always
//   go toohello same instance
topologyBuilder.SetBolt(
    "counter",
    Counter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word", "count"}}
    },
    1).fieldsGrouping("splitter", new List<int>() { 0 });

// Add topology config
topologyBuilder.SetTopologyConfig(new Dictionary<string, string>()
{
    {"topology.kryo.register","[\"[B\"]"}
});

return topologyBuilder;
```

## <a name="submit-hello-topology"></a><span data-ttu-id="6adc8-235">Merhaba topoloji gönderme</span><span class="sxs-lookup"><span data-stu-id="6adc8-235">Submit hello topology</span></span>

1. <span data-ttu-id="6adc8-236">İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve seçin **hdınsight'ta tooStorm gönderme**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-236">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6adc8-237">İstenirse, Azure aboneliğinizin hello kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="6adc8-237">If prompted, enter hello credentials for your Azure subscription.</span></span> <span data-ttu-id="6adc8-238">Birden fazla aboneliğiniz varsa, toohello Hdınsight kümesi üzerinde Storm'a içeren bir oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6adc8-238">If you have more than one subscription, sign in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="6adc8-239">Hdınsight kümesi üzerinde Storm'a hello seçin **Storm kümesi** aşağı açılan listeyi ve ardından **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-239">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="6adc8-240">Merhaba gönderimi hello kullanarak başarılı olursa, izleyebilirsiniz **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="6adc8-240">You can monitor if hello submission is successful by using hello **Output** window.</span></span>

3. <span data-ttu-id="6adc8-241">Merhaba topoloji başarıyla gönderildi, hello **Storm topolojilerini** hello küme görünür.</span><span class="sxs-lookup"><span data-stu-id="6adc8-241">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="6adc8-242">Select hello **WordCount** topoloji topoloji çalıştıran hello hakkında hello listesi tooview bilgi.</span><span class="sxs-lookup"><span data-stu-id="6adc8-242">Select hello **WordCount** topology from hello list tooview information about hello running topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6adc8-243">Ayrıca görüntüleyebilirsiniz **Storm topolojilerini** gelen **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-243">You can also view **Storm Topologies** from **Server Explorer**.</span></span> <span data-ttu-id="6adc8-244">Genişletme **Azure** > **Hdınsight**, Hdınsight kümesinde bir Storm sağ tıklayın ve ardından **görünüm Storm topolojilerini**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-244">Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span></span>

    <span data-ttu-id="6adc8-245">Merhaba topolojisinde hello bileşenler hakkında bilgi tooview hello diyagramı hello bileşeninde çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6adc8-245">tooview information about hello components in hello topology, double-click hello component in hello diagram.</span></span>

4. <span data-ttu-id="6adc8-246">Merhaba gelen **topoloji özeti** görüntülemek için tıklatın **KILL** toostop hello topolojisi.</span><span class="sxs-lookup"><span data-stu-id="6adc8-246">From hello **Topology Summary** view, click **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6adc8-247">Storm topolojilerini toorun devre dışı bırakılır veya hello küme silinene kadar devam eder.</span><span class="sxs-lookup"><span data-stu-id="6adc8-247">Storm topologies continue toorun until they are deactivated, or hello cluster is deleted.</span></span>

## <a name="transactional-topology"></a><span data-ttu-id="6adc8-248">İşlem topolojisi</span><span class="sxs-lookup"><span data-stu-id="6adc8-248">Transactional topology</span></span>

<span data-ttu-id="6adc8-249">Merhaba önceki işlem olmayan topolojidir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-249">hello previous topology is non-transactional.</span></span> <span data-ttu-id="6adc8-250">Merhaba bileşenleri hello topolojisinde işlevselliği tooreplaying iletileri kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="6adc8-250">hello components in hello topology do not implement functionality tooreplaying messages.</span></span> <span data-ttu-id="6adc8-251">Bir işlem topolojisi ilişkin bir örnek, bir proje oluşturmak ve **Storm örnek** hello proje türü olarak.</span><span class="sxs-lookup"><span data-stu-id="6adc8-251">For an example of a transactional topology, create a project and select **Storm Sample** as hello project type.</span></span>

<span data-ttu-id="6adc8-252">İşlem topolojileri toosupport yeniden yürütme veri aşağıdaki hello uygulayın:</span><span class="sxs-lookup"><span data-stu-id="6adc8-252">Transactional topologies implement hello following toosupport replay of data:</span></span>

* <span data-ttu-id="6adc8-253">**Meta verileri önbelleğe alma**: Merhaba spout yayılan hello verileri alınır ve bir hata oluşursa yeniden yayılan böylece hello veriler hakkındaki meta verileri depolamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-253">**Metadata caching**: hello spout must store metadata about hello data emitted, so that hello data can be retrieved and emitted again if a failure occurs.</span></span> <span data-ttu-id="6adc8-254">Merhaba örnek tarafından yayılan hello veriler küçük olduğundan hello ham verileri her tanımlama grubu için bir sözlük yeniden yürütme için depolanır.</span><span class="sxs-lookup"><span data-stu-id="6adc8-254">Because hello data emitted by hello sample is small, hello raw data for each tuple is stored in a dictionary for replay.</span></span>

* <span data-ttu-id="6adc8-255">**ACK**: hello topolojisinde her Cıvata çağırabilirsiniz `this.ctx.Ack(tuple)` bir tanımlama grubu başarıyla işlediği tooacknowledge.</span><span class="sxs-lookup"><span data-stu-id="6adc8-255">**Ack**: Each bolt in hello topology can call `this.ctx.Ack(tuple)` tooacknowledge that it has successfully processed a tuple.</span></span> <span data-ttu-id="6adc8-256">Tüm Cıvatalar acked hello tanımlama grubu varsa, hello `Ack` hello spout yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="6adc8-256">When all bolts have acked hello tuple, hello `Ack` method of hello spout is invoked.</span></span> <span data-ttu-id="6adc8-257">Merhaba `Ack` yöntemi yeniden yürütme için önbelleğe hello spout tooremove veri sağlar.</span><span class="sxs-lookup"><span data-stu-id="6adc8-257">hello `Ack` method allows hello spout tooremove data that was cached for replay.</span></span>

* <span data-ttu-id="6adc8-258">**Başarısız**: her Cıvata çağırabilirsiniz `this.ctx.Fail(tuple)` tooindicate bu işlem için bir tanımlama grubu yapamadı.</span><span class="sxs-lookup"><span data-stu-id="6adc8-258">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` tooindicate that processing has failed for a tuple.</span></span> <span data-ttu-id="6adc8-259">Merhaba hatası yayar toohello `Fail` burada hello tanımlama grubu yeniden kullanarak hello spout yöntemi önbelleğe alınan meta verileri.</span><span class="sxs-lookup"><span data-stu-id="6adc8-259">hello failure propagates toohello `Fail` method of hello spout, where hello tuple can be replayed by using cached metadata.</span></span>

* <span data-ttu-id="6adc8-260">**Sıra kimliği**: bir tanımlama grubu yayma, benzersiz sıra kimliği belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-260">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span></span> <span data-ttu-id="6adc8-261">Bu değer hello tanımlama grubu yeniden yürütme (Ack ve başarısız) işleme tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6adc8-261">This value identifies hello tuple for replay (Ack and Fail) processing.</span></span> <span data-ttu-id="6adc8-262">Örneğin, hello spout hello **Storm örnek** project veri yayma zaman hello şunları kullanır:</span><span class="sxs-lookup"><span data-stu-id="6adc8-262">For example, hello spout in hello **Storm Sample** project uses hello following when emitting data:</span></span>

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    <span data-ttu-id="6adc8-263">Bu kod içinde yer alan hello sırası kimliği değeri olan bir cümle toohello varsayılan akış içeren bir tanımlama grubu yayar **lastSeqId**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-263">This code emits a tuple that contains a sentence toohello default stream, with hello sequence ID value contained in **lastSeqId**.</span></span> <span data-ttu-id="6adc8-264">Bu örnek için **lastSeqId** gösterilen her bir tanımlama grubu için artırılır.</span><span class="sxs-lookup"><span data-stu-id="6adc8-264">For this example, **lastSeqId** is incremented for every tuple emitted.</span></span>

<span data-ttu-id="6adc8-265">Hello gösterildiği gibi **Storm örnek** proje, bir bileşenin işlem olup yapılandırmasını temel alarak zamanında ayarlanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-265">As demonstrated in hello **Storm Sample** project, whether a component is transactional can be set at runtime, based on configuration.</span></span>

## <a name="hybrid-topology-with-c-and-java"></a><span data-ttu-id="6adc8-266">C# ve Java ile karma topolojisi</span><span class="sxs-lookup"><span data-stu-id="6adc8-266">Hybrid topology with C# and Java</span></span>

<span data-ttu-id="6adc8-267">Burada bazı bileşenleri C# ve diğerleri Java Visual Studio toocreate karma topolojiler için Data Lake Araçları'nı da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6adc8-267">You can also use Data Lake tools for Visual Studio toocreate hybrid topologies, where some components are C# and others are Java.</span></span>

<span data-ttu-id="6adc8-268">Bir karma topolojisi ilişkin bir örnek, bir proje oluşturmak ve **Storm karma örnek**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-268">For an example of a hybrid topology, create a project and select **Storm Hybrid Sample**.</span></span> <span data-ttu-id="6adc8-269">Bu örnek türü kavramları aşağıdaki hello gösterir:</span><span class="sxs-lookup"><span data-stu-id="6adc8-269">This sample type demonstrates hello following concepts:</span></span>

* <span data-ttu-id="6adc8-270">**Java spout** ve **C# Cıvata**: tanımlıysa **HybridTopology_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-270">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**.</span></span>

    * <span data-ttu-id="6adc8-271">İşlem sürüm tanımlanan **HybridTopologyTx_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-271">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**.</span></span>

* <span data-ttu-id="6adc8-272">**C# spout** ve **Java Cıvata**: tanımlıysa **HybridTopology_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-272">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**.</span></span>

    * <span data-ttu-id="6adc8-273">İşlem sürüm tanımlanan **HybridTopologyTx_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-273">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="6adc8-274">Bu sürüm ayrıca nasıl toouse Clojure kod bir Java bileşeni olarak bir metin dosyasından gösterir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-274">This version also demonstrates how toouse Clojure code from a text file as a Java component.</span></span>


<span data-ttu-id="6adc8-275">Merhaba proje gönderildiğinde, kullanılan tooswitch hello topoloji yalnızca hello taşıma `[Active(true)]` toohello küme göndermeden önce toouse, istediğiniz deyimi toohello topolojisi.</span><span class="sxs-lookup"><span data-stu-id="6adc8-275">tooswitch hello topology that is used when hello project is submitted, simply move hello `[Active(true)]` statement toohello topology you want toouse, before submitting it toohello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="6adc8-276">Gerekli tüm hello Java dosyaları hello bu projede bir parçası olarak sağlanan **JavaDependency** klasör.</span><span class="sxs-lookup"><span data-stu-id="6adc8-276">All hello Java files that are required are provided as part of this project in hello **JavaDependency** folder.</span></span>

<span data-ttu-id="6adc8-277">Oluştururken ve karma topolojisi gönderme hello aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="6adc8-277">Consider hello following when you are creating and submitting a hybrid topology:</span></span>

* <span data-ttu-id="6adc8-278">Kullanmalısınız **JavaComponentConstructor** toocreate hello spout veya Cıvata için Java sınıfı örneği.</span><span class="sxs-lookup"><span data-stu-id="6adc8-278">You must use **JavaComponentConstructor** toocreate an instance of hello Java class for a spout or bolt.</span></span>

* <span data-ttu-id="6adc8-279">Kullanmanız gereken **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooserialize veri içine veya Java bileşenleri Java'dan dışında tooJSON nesneleri.</span><span class="sxs-lookup"><span data-stu-id="6adc8-279">You should use **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooserialize data into or out of Java components from Java objects tooJSON.</span></span>

* <span data-ttu-id="6adc8-280">Merhaba topoloji toohello sunucu gönderirken hello kullanmalısınız **ek yapılandırmalar** seçeneği toospecify hello **Java dosya yolları**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-280">When submitting hello topology toohello server, you must use hello **Additional configurations** option toospecify hello **Java File paths**.</span></span> <span data-ttu-id="6adc8-281">Belirtilen hello yolu Java sınıfları içeren hello JAR dosyalarını içeren hello dizin olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6adc8-281">hello path specified should be hello directory that contains hello JAR files that contain your Java classes.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="6adc8-282">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="6adc8-282">Azure Event Hubs</span></span>

<span data-ttu-id="6adc8-283">SCP.NET sürüm 0.9.4.203 bir yeni sınıf ve hello olay hub'ı spout (olay hub'larından okuyan bir Java spout) ile çalışmak için özellikle yöntemi sunar.</span><span class="sxs-lookup"><span data-stu-id="6adc8-283">SCP.NET version 0.9.4.203 introduces a new class and method specifically for working with hello Event Hub spout (a Java spout that reads from Event Hubs).</span></span> <span data-ttu-id="6adc8-284">Bir olay hub'ı spout kullanan bir topolojisi oluşturduğunuzda, hello aşağıdaki yöntemleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="6adc8-284">When you create a topology that uses an Event Hub spout, use hello following methods:</span></span>

* <span data-ttu-id="6adc8-285">**EventHubSpoutConfig** sınıfı: Merhaba spout bileşeni için hello yapılandırma içeren bir nesne oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6adc8-285">**EventHubSpoutConfig** class: Creates an object that contains hello configuration for hello spout component.</span></span>

* <span data-ttu-id="6adc8-286">**TopologyBuilder.SetEventHubSpout** yöntemi: hello olay hub'ı spout bileşen toohello topoloji ekler.</span><span class="sxs-lookup"><span data-stu-id="6adc8-286">**TopologyBuilder.SetEventHubSpout** method: Adds hello Event Hub spout component toohello topology.</span></span>

> [!NOTE]
> <span data-ttu-id="6adc8-287">Merhaba hala kullanmalısınız **CustomizedInteropJSONSerializer** üretilen hello spout'un tooserialize veriler.</span><span class="sxs-lookup"><span data-stu-id="6adc8-287">You must still use hello **CustomizedInteropJSONSerializer** tooserialize data produced by hello spout.</span></span>

## <span data-ttu-id="6adc8-288"><a id="configurationmanager"></a>ConfigurationManager kullanın</span><span class="sxs-lookup"><span data-stu-id="6adc8-288"><a id="configurationmanager"></a>Use ConfigurationManager</span></span>

<span data-ttu-id="6adc8-289">Kullanmayan **ConfigurationManager** tooretrieve yapılandırma değerleri Cıvata ve bileşenleri spout.</span><span class="sxs-lookup"><span data-stu-id="6adc8-289">Don't use **ConfigurationManager** tooretrieve configuration values from bolt and spout components.</span></span> <span data-ttu-id="6adc8-290">Bunun yapılması bir null işaretçi özel durumu neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-290">Doing so can cause a null pointer exception.</span></span> <span data-ttu-id="6adc8-291">Bunun yerine, hello yapılandırma projeniz için bir anahtar ve değer çifti hello topoloji bağlamda olarak hello Storm topolojisini geçirilir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-291">Instead, hello configuration for your project is passed into hello Storm topology as a key and value pair in hello topology context.</span></span> <span data-ttu-id="6adc8-292">Yapılandırma değerlerini kullanır her bileşenin bunları başlatma sırasında hello bağlamından almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-292">Each component that relies on configuration values must retrieve them from hello context during initialization.</span></span>

<span data-ttu-id="6adc8-293">Merhaba aşağıdaki kodu gösterir nasıl tooretrieve bu değerler:</span><span class="sxs-lookup"><span data-stu-id="6adc8-293">hello following code demonstrates how tooretrieve these values:</span></span>

```csharp
public class MyComponent : ISCPBolt
{
    // toohold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of hello context for this component instance
        this.ctx = ctx;
        // If it exists, load hello configuration for hello component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve hello value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

<span data-ttu-id="6adc8-294">Kullanırsanız, bir `Get` yöntemi tooreturn bileşeniniz ait bir örnek sağlamanız hem hello geçirir `Context` ve `Dictionary<string, Object>` parametreleri toohello Oluşturucusu.</span><span class="sxs-lookup"><span data-stu-id="6adc8-294">If you use a `Get` method tooreturn an instance of your component, you must ensure that it passes both hello `Context` and `Dictionary<string, Object>` parameters toohello constructor.</span></span> <span data-ttu-id="6adc8-295">Merhaba aşağıdaki temel bir örnektir `Get` düzgün bu değerleri geçirir yöntemi:</span><span class="sxs-lookup"><span data-stu-id="6adc8-295">hello following example is a basic `Get` method that properly passes these values:</span></span>

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-tooupdate-scpnet"></a><span data-ttu-id="6adc8-296">Nasıl tooupdate SCP.NET</span><span class="sxs-lookup"><span data-stu-id="6adc8-296">How tooupdate SCP.NET</span></span>

<span data-ttu-id="6adc8-297">Paket yükseltmesi NuGet aracılığıyla SCP.NET en son sürümleri destekler.</span><span class="sxs-lookup"><span data-stu-id="6adc8-297">Recent releases of SCP.NET support package upgrade through NuGet.</span></span> <span data-ttu-id="6adc8-298">Yeni bir güncelleştirme kullanılabilir olduğunda, bir yükseltme bildirimi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="6adc8-298">When a new update is available, you receive an upgrade notification.</span></span> <span data-ttu-id="6adc8-299">toomanually denetleyin, yükseltme için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="6adc8-299">toomanually check for an upgrade, follow these steps:</span></span>

1. <span data-ttu-id="6adc8-300">İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve seçin **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-300">In **Solution Explorer**, right-click hello project, and select **Manage NuGet Packages**.</span></span>

2. <span data-ttu-id="6adc8-301">Merhaba Paket Yöneticisi'nden seçin **güncelleştirmeleri**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-301">From hello package manager, select **Updates**.</span></span> <span data-ttu-id="6adc8-302">Bir güncelleştirme olup olmadığını listelenir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-302">If an update is available, it is listed.</span></span> <span data-ttu-id="6adc8-303">Tıklatın **güncelleştirme** hello paket tooinstall için bunu.</span><span class="sxs-lookup"><span data-stu-id="6adc8-303">Click **Update** for hello package tooinstall it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6adc8-304">Projenizin NuGet kullanmadı SCP.NET önceki bir sürümüyle oluşturulduysa, aşağıdaki adımları tooupdate tooa daha yeni sürüm hello gerçekleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="6adc8-304">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform hello following steps tooupdate tooa newer version:</span></span>
>
> 1. <span data-ttu-id="6adc8-305">İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve seçin **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-305">In **Solution Explorer**, right-click hello project, and select **Manage NuGet Packages**.</span></span>
> 2. <span data-ttu-id="6adc8-306">Hello kullanarak **arama** alanına arayın ve ardından ekleyin, **Microsoft.SCP.Net.SDK** toohello projesi.</span><span class="sxs-lookup"><span data-stu-id="6adc8-306">Using hello **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** toohello project.</span></span>

## <a name="troubleshoot-common-issues-with-topologies"></a><span data-ttu-id="6adc8-307">Topolojileri ile ilgili genel sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="6adc8-307">Troubleshoot common issues with topologies</span></span>

### <a name="null-pointer-exceptions"></a><span data-ttu-id="6adc8-308">Null işaretçi özel durumlar</span><span class="sxs-lookup"><span data-stu-id="6adc8-308">Null pointer exceptions</span></span>

<span data-ttu-id="6adc8-309">Bir C# topolojisi ile Linux tabanlı Hdınsight kümesi kullanırken, Cıvata ve kullanan bileşenleri spout **ConfigurationManager** tooread yapılandırma ayarlarını çalışma zamanında null işaretçi özel durumlar döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-309">When you are using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use **ConfigurationManager** tooread configuration settings at runtime may return null pointer exceptions.</span></span>

<span data-ttu-id="6adc8-310">projeniz için Hello yapılandırma hello Storm topolojisini hello topoloji bağlamında bir anahtar ve değer çifti olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-310">hello configuration for your project is passed into hello Storm topology as a key and value pair in hello topology context.</span></span> <span data-ttu-id="6adc8-311">Bunlar hazırlarken, tooyour bileşenleri geçirilen hello dictionary nesnesinden alınabilir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-311">It can be retrieved from hello dictionary object that is passed tooyour components when they are initialized.</span></span>

<span data-ttu-id="6adc8-312">Daha fazla bilgi için bkz: Merhaba [ConfigurationManager](#configurationmanager) bu belgenin bölüm.</span><span class="sxs-lookup"><span data-stu-id="6adc8-312">For more information, see hello [ConfigurationManager](#configurationmanager) section of this document.</span></span>

### <a name="systemtypeloadexception"></a><span data-ttu-id="6adc8-313">System.TypeLoadException</span><span class="sxs-lookup"><span data-stu-id="6adc8-313">System.TypeLoadException</span></span>

<span data-ttu-id="6adc8-314">Bir C# topolojisi ile Linux tabanlı Hdınsight kümesi kullanırken, aşağıdaki hata hello karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6adc8-314">When you are using a C# topology with a Linux-based HDInsight cluster, you may encounter hello following error:</span></span>

    System.TypeLoadException: Failure has occurred while loading a type.

<span data-ttu-id="6adc8-315">Mono destekleyen .NET hello sürümü ile uyumlu olmayan bir ikili kullandığınızda bu hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="6adc8-315">This error occurs when you use a binary that is not compatible with hello version of .NET that Mono supports.</span></span>

<span data-ttu-id="6adc8-316">Linux tabanlı Hdınsight kümeleri için projeniz .NET 4. 5'için derlenmiş ikili dosyaları kullandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="6adc8-316">For Linux-based HDInsight clusters, make sure that your project uses binaries compiled for .NET 4.5.</span></span>

### <a name="test-a-topology-locally"></a><span data-ttu-id="6adc8-317">Bir topoloji yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="6adc8-317">Test a topology locally</span></span>

<span data-ttu-id="6adc8-318">Kolay toodeploy bazı durumlarda, bir topoloji tooa küme olmasına rağmen tootest yerel olarak bir topoloji gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-318">Although it is easy toodeploy a topology tooa cluster, in some cases, you may need tootest a topology locally.</span></span> <span data-ttu-id="6adc8-319">Bu öğreticide yerel geliştirme ortamınızı hello örnek topoloji test ve adımları toorun aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="6adc8-319">Use hello following steps toorun and test hello example topology in this tutorial locally in your development environment.</span></span>

> [!WARNING]
> <span data-ttu-id="6adc8-320">Yerel test yalnızca çalışır için basic, C#-yalnızca topolojileri.</span><span class="sxs-lookup"><span data-stu-id="6adc8-320">Local testing only works for basic, C#-only topologies.</span></span> <span data-ttu-id="6adc8-321">Karma topolojiler veya birden çok akış kullanmak Topolojileri için yerel test kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="6adc8-321">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span></span>

1. <span data-ttu-id="6adc8-322">İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-322">In **Solution Explorer**, right-click hello project, and select **Properties**.</span></span> <span data-ttu-id="6adc8-323">Merhaba Proje Özellikleri'nde hello değiştirme **çıktı türü** çok**konsol uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-323">In hello project properties, change hello **Output type** too**Console Application**.</span></span>

    ![Vurgulanan çıktı türü ile Proje Özellikleri'nin ekran görüntüsü](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > <span data-ttu-id="6adc8-325">Toochange hello unutmayın **çıktı türü** çok geri**sınıf kitaplığı** hello topoloji tooa küme dağıtmadan önce.</span><span class="sxs-lookup"><span data-stu-id="6adc8-325">Remember toochange hello **Output type** back too**Class Library** before you deploy hello topology tooa cluster.</span></span>

2. <span data-ttu-id="6adc8-326">İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve ardından **Ekle** > **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-326">In **Solution Explorer**, right-click hello project, and then select **Add** > **New Item**.</span></span> <span data-ttu-id="6adc8-327">Seçin **sınıfı**ve girin **LocalTest.cs** hello sınıfı adı.</span><span class="sxs-lookup"><span data-stu-id="6adc8-327">Select **Class**, and enter **LocalTest.cs** as hello class name.</span></span> <span data-ttu-id="6adc8-328">Son olarak, tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-328">Finally, click **Add**.</span></span>

3. <span data-ttu-id="6adc8-329">Açık **LocalTest.cs**ve hello aşağıdakileri ekleyin **kullanarak** hello üstünde deyimi:</span><span class="sxs-lookup"><span data-stu-id="6adc8-329">Open **LocalTest.cs**, and add hello following **using** statement at hello top:</span></span>

    ```csharp
    using Microsoft.SCP;
    ```

4. <span data-ttu-id="6adc8-330">Kullanım hello aşağıdaki kod hello Merhaba içeriğine **LocalTest** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="6adc8-330">Use hello following code as hello contents of hello **LocalTest** class:</span></span>

    ```csharp
    // Drives hello topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test hello spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of hello spout, using hello local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext toopersist hello data stream toofile
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test hello splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set hello data stream toohello data created by hello spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test hello counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set hello data stream toohello data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    <span data-ttu-id="6adc8-331">Şu anda tooread hello kod açıklamaları aracılığıyla alın.</span><span class="sxs-lookup"><span data-stu-id="6adc8-331">Take a moment tooread through hello code comments.</span></span> <span data-ttu-id="6adc8-332">Bu kodu kullanır **LocalContext** toorun hello bileşenlerinde hello geliştirme ortamını ve hello veri akışı bileşenleri tootext dosyaları hello yerel sürücüde arasında devam ettirir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-332">This code uses **LocalContext** toorun hello components in hello development environment, and it persists hello data stream between components tootext files on hello local drive.</span></span>

1. <span data-ttu-id="6adc8-333">Açık **Program.cs**ve toohello aşağıdaki hello ekleyin **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="6adc8-333">Open **Program.cs**, and add hello following toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize hello runtime
    SCPRuntime.Initialize();

    //If we are not running under hello local context, throw an error
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)
    {
        throw new Exception(string.Format("unexpected pluginType: {0}", Context.pluginType));
    }
    // Create test instance
    LocalTest tests = new LocalTest();
    // Run tests
    tests.RunTestCase();
    Console.WriteLine("Tests finished");
    Console.ReadKey();
    ```

2. <span data-ttu-id="6adc8-334">Merhaba değişiklikleri kaydedin ve ardından **F5** veya seçin **hata ayıklama** > **hata ayıklamayı Başlat** toostart hello projesi.</span><span class="sxs-lookup"><span data-stu-id="6adc8-334">Save hello changes, and then click **F5** or select **Debug** > **Start Debugging** toostart hello project.</span></span> <span data-ttu-id="6adc8-335">Bir konsol penceresi görünür ve günlük hello testleri ilerleme durumunun gerekir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-335">A console window should appear, and log status as hello tests progress.</span></span> <span data-ttu-id="6adc8-336">Zaman **testleri tamamlandı** görüntülenirse, herhangi bir anahtar tooclose hello penceresi tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="6adc8-336">When **Tests finished** appears, press any key tooclose hello window.</span></span>

3. <span data-ttu-id="6adc8-337">Kullanım **Windows Explorer** projenizi içeren toolocate başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="6adc8-337">Use **Windows Explorer** toolocate hello directory that contains your project.</span></span> <span data-ttu-id="6adc8-338">Örneğin: **C:\Users\<your_user_name > \Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-338">For example: **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span></span> <span data-ttu-id="6adc8-339">Bu dizinde açmak **Bin**ve ardından **hata ayıklama**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-339">In this directory, open **Bin**, and then click **Debug**.</span></span> <span data-ttu-id="6adc8-340">Merhaba testlerini çalıştırdığınızda oluşturulamadığı hello metin dosyaları görmeniz gerekir: sentences.txt, counter.txt ve splitter.txt.</span><span class="sxs-lookup"><span data-stu-id="6adc8-340">You should see hello text files that were produced when hello tests ran: sentences.txt, counter.txt, and splitter.txt.</span></span> <span data-ttu-id="6adc8-341">Her metin dosyasını açın ve hello veri inceleyin.</span><span class="sxs-lookup"><span data-stu-id="6adc8-341">Open each text file and inspect hello data.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6adc8-342">Dize verilerini bu dosyalardaki ondalık değerleri dizisi olarak devam ettirir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-342">String data persists as an array of decimal values in these files.</span></span> <span data-ttu-id="6adc8-343">Örneğin, \[[97,103,111]] hello içinde **splitter.txt** dosyasıdır hello word *ve*.</span><span class="sxs-lookup"><span data-stu-id="6adc8-343">For example, \[[97,103,111]] in hello **splitter.txt** file is hello word *and*.</span></span>

> [!NOTE]
> <span data-ttu-id="6adc8-344">Emin tooset hello olması **proje türü** çok geri**sınıf kitaplığı** Hdınsight kümesinde Storm tooa dağıtmadan önce.</span><span class="sxs-lookup"><span data-stu-id="6adc8-344">Be sure tooset hello **Project type** back too**Class Library** before deploying tooa Storm on HDInsight cluster.</span></span>

### <a name="log-information"></a><span data-ttu-id="6adc8-345">Günlük bilgileri</span><span class="sxs-lookup"><span data-stu-id="6adc8-345">Log information</span></span>

<span data-ttu-id="6adc8-346">Kolayca bilgi topoloji bileşenlerinizi kullanarak oturum `Context.Logger`.</span><span class="sxs-lookup"><span data-stu-id="6adc8-346">You can easily log information from your topology components by using `Context.Logger`.</span></span> <span data-ttu-id="6adc8-347">Örneğin, hello aşağıdaki bilgilendirici günlük girişi oluşturur:</span><span class="sxs-lookup"><span data-stu-id="6adc8-347">For example, hello following creates an informational log entry:</span></span>

```csharp
Context.Logger.Info("Component started");
```

<span data-ttu-id="6adc8-348">Günlüğe kaydedilen bilgileri hello görüntülenebilir **Hadoop hizmeti günlüğünü**, içinde bulunan **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-348">Logged information can be viewed from hello **Hadoop Service Log**, which is found in **Server Explorer**.</span></span> <span data-ttu-id="6adc8-349">Hdınsight kümesi üzerinde Storm'a için Hello girişi genişletin ve ardından **Hadoop hizmeti günlüğünü**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-349">Expand hello entry for your Storm on HDInsight cluster, and then expand **Hadoop Service Log**.</span></span> <span data-ttu-id="6adc8-350">Son olarak, hello günlük dosyası tooview seçin.</span><span class="sxs-lookup"><span data-stu-id="6adc8-350">Finally, select hello log file tooview.</span></span>

> [!NOTE]
> <span data-ttu-id="6adc8-351">Merhaba günlükleri Merhaba, küme tarafından kullanılan Azure depolama hesabı depolanır.</span><span class="sxs-lookup"><span data-stu-id="6adc8-351">hello logs are stored in hello Azure storage account that is used by your cluster.</span></span> <span data-ttu-id="6adc8-352">Visual Studio'da tooview hello günlükleri, toohello hello depolama hesabı sahibi Azure aboneliği oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-352">tooview hello logs in Visual Studio, you must sign in toohello Azure subscription that owns hello storage account.</span></span>

### <a name="view-error-information"></a><span data-ttu-id="6adc8-353">Hata bilgilerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="6adc8-353">View error information</span></span>

<span data-ttu-id="6adc8-354">çalışan bir topoloji oluşmuş tooview hataları hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="6adc8-354">tooview errors that have occurred in a running topology, use hello following steps:</span></span>

1. <span data-ttu-id="6adc8-355">Gelen **Sunucu Gezgini**, Hdınsight kümesinde Storm hello sağ tıklatın ve seçin **görünüm Storm topolojilerini**.</span><span class="sxs-lookup"><span data-stu-id="6adc8-355">From **Server Explorer**, right-click hello Storm on HDInsight cluster, and select **View Storm topologies**.</span></span>

2. <span data-ttu-id="6adc8-356">Hello için **Spout** ve **Cıvatalar**, hello **son hata** sütun hello son hata hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="6adc8-356">For hello **Spout** and **Bolts**, hello **Last Error** column contains information on hello last error.</span></span>

3. <span data-ttu-id="6adc8-357">Select hello **Spout kimliği** veya **Cıvata kimliği** listelenen hatalı hello bileşeni için.</span><span class="sxs-lookup"><span data-stu-id="6adc8-357">Select hello **Spout Id** or **Bolt Id** for hello component that has an error listed.</span></span> <span data-ttu-id="6adc8-358">Görüntülenen, ek hata hello Ayrıntıları sayfasında hello listelenen bilgileri **hataları** hello sayfanın hello kısmına.</span><span class="sxs-lookup"><span data-stu-id="6adc8-358">On hello details page that is displayed, additional error information is listed in hello **Errors** section at hello bottom of hello page.</span></span>

4. <span data-ttu-id="6adc8-359">tooobtain daha fazla bilgi, select bir **bağlantı noktası** hello gelen **yürütücüler** hello sayfasının bölümünde, toosee hello Storm çalışan günlük hello son birkaç dakika için.</span><span class="sxs-lookup"><span data-stu-id="6adc8-359">tooobtain more information, select a **Port** from hello **Executors** section of hello page, toosee hello Storm worker log for hello last few minutes.</span></span>

### <a name="errors-submitting-topologies"></a><span data-ttu-id="6adc8-360">Topolojileri gönderme hataları</span><span class="sxs-lookup"><span data-stu-id="6adc8-360">Errors submitting topologies</span></span>

<span data-ttu-id="6adc8-361">Topoloji tooHDInsight gönderilirken hatalarla karşılaşırsanız, Hdınsight kümenize topoloji gönderimini işlemek hello sunucu tarafı bileşenleri için günlükleri bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6adc8-361">If you encounter errors submitting a topology tooHDInsight, you can find logs for hello server-side components that handle topology submission on your HDInsight cluster.</span></span> <span data-ttu-id="6adc8-362">Bu günlükleri, komutu bir komut satırından aşağıdaki kullanım hello tooretrieve:</span><span class="sxs-lookup"><span data-stu-id="6adc8-362">tooretrieve these logs, use hello following command from a command line:</span></span>

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

<span data-ttu-id="6adc8-363">Değiştir __sshuser__ hello hello küme için SSH kullanıcı hesabı ile.</span><span class="sxs-lookup"><span data-stu-id="6adc8-363">Replace __sshuser__ with hello SSH user account for hello cluster.</span></span> <span data-ttu-id="6adc8-364">Değiştir __clustername__ hello Hdınsight kümesi hello adı.</span><span class="sxs-lookup"><span data-stu-id="6adc8-364">Replace __clustername__ with hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="6adc8-365">Kullanma hakkında daha fazla bilgi için `scp` ve `ssh` Hdınsight ile bkz [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6adc8-365">For more information on using `scp` and `ssh` with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="6adc8-366">Gönderimleri birden çok nedenlerden dolayı başarısız olabilir:</span><span class="sxs-lookup"><span data-stu-id="6adc8-366">Submissions can fail for multiple reasons:</span></span>

* <span data-ttu-id="6adc8-367">JDK yüklü değil veya hello yolunda değil.</span><span class="sxs-lookup"><span data-stu-id="6adc8-367">JDK is not installed or is not in hello path.</span></span>
* <span data-ttu-id="6adc8-368">Gerekli Java bağımlılıkları hello gönderisine dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="6adc8-368">Required Java dependencies are not included in hello submission.</span></span>
* <span data-ttu-id="6adc8-369">Uyumsuz bağımlılıkları.</span><span class="sxs-lookup"><span data-stu-id="6adc8-369">Incompatible dependencies.</span></span>
* <span data-ttu-id="6adc8-370">Yinelenen topoloji adları.</span><span class="sxs-lookup"><span data-stu-id="6adc8-370">Duplicate topology names.</span></span>

<span data-ttu-id="6adc8-371">Merhaba, `hdinsight-scpwebapi.out` günlük içeren bir `FileNotFoundException`, bu koşullar aşağıdaki hello tarafından kaynaklanabilir:</span><span class="sxs-lookup"><span data-stu-id="6adc8-371">If hello `hdinsight-scpwebapi.out` log contains a `FileNotFoundException`, this might be caused by hello following conditions:</span></span>

* <span data-ttu-id="6adc8-372">Merhaba JDK hello geliştirme ortamı hello yolu değil.</span><span class="sxs-lookup"><span data-stu-id="6adc8-372">hello JDK is not in hello path on hello development environment.</span></span> <span data-ttu-id="6adc8-373">JDK yüklü hello geliştirme ortamını ve, o hello doğrulayın `%JAVA_HOME%/bin` hello yoludur.</span><span class="sxs-lookup"><span data-stu-id="6adc8-373">Verify that hello JDK is installed in hello development environment, and that `%JAVA_HOME%/bin` is in hello path.</span></span>
* <span data-ttu-id="6adc8-374">Java bağımlılığı eksik.</span><span class="sxs-lookup"><span data-stu-id="6adc8-374">You are missing a Java dependency.</span></span> <span data-ttu-id="6adc8-375">Tüm gerekli .jar dosyalar hello gönderimi bir parçası olarak dahil emin olun.</span><span class="sxs-lookup"><span data-stu-id="6adc8-375">Make sure you are including any required .jar files as part of hello submission.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6adc8-376">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6adc8-376">Next steps</span></span>

<span data-ttu-id="6adc8-377">Bir örnek veriler işlenirken için Event hubs, bkz: [işlem Hdınsight üzerinde Storm ile Azure Event Hubs olaylarından](hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="6adc8-377">For an example of processing data from Event Hubs, see [Process events from Azure Event Hubs with Storm on HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span>

<span data-ttu-id="6adc8-378">Veri akışı birden çok akışlara böler bir C# topolojisi örneği için bkz: [C# Storm örnek](https://github.com/Blackmist/csharp-storm-example).</span><span class="sxs-lookup"><span data-stu-id="6adc8-378">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span></span>

<span data-ttu-id="6adc8-379">C# topolojileri, oluşturma hakkında daha fazla bilgi toodiscover bkz [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span><span class="sxs-lookup"><span data-stu-id="6adc8-379">toodiscover more information about creating C# topologies, see [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span></span>

<span data-ttu-id="6adc8-380">Hdınsight ile daha fazla yol toowork ve Hdınsight örnekleri üzerinde daha fazla Storm için belgeler aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="6adc8-380">For more ways toowork with HDInsight and more Storm on HDInsight samples, see hello following documents:</span></span>

<span data-ttu-id="6adc8-381">**Microsoft SCP.NET**</span><span class="sxs-lookup"><span data-stu-id="6adc8-381">**Microsoft SCP.NET**</span></span>

* [<span data-ttu-id="6adc8-382">SCP Programlama Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="6adc8-382">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)

<span data-ttu-id="6adc8-383">**Hdınsight üzerinde Apache Storm**</span><span class="sxs-lookup"><span data-stu-id="6adc8-383">**Apache Storm on HDInsight**</span></span>

* [<span data-ttu-id="6adc8-384">Dağıtma ve hdınsight'ta Apache Storm topolojileri izleme</span><span class="sxs-lookup"><span data-stu-id="6adc8-384">Deploy and monitor topologies with Apache Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)
* [<span data-ttu-id="6adc8-385">HDInsight üzerinde Storm için örnek topolojiler</span><span class="sxs-lookup"><span data-stu-id="6adc8-385">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

<span data-ttu-id="6adc8-386">**Hdınsight'ta Apache Hadoop**</span><span class="sxs-lookup"><span data-stu-id="6adc8-386">**Apache Hadoop on HDInsight**</span></span>

* [<span data-ttu-id="6adc8-387">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="6adc8-387">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="6adc8-388">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="6adc8-388">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="6adc8-389">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="6adc8-389">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="6adc8-390">**Hdınsight üzerinde Apache HBase**</span><span class="sxs-lookup"><span data-stu-id="6adc8-390">**Apache HBase on HDInsight**</span></span>

* [<span data-ttu-id="6adc8-391">Hdınsight'ta HBase ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="6adc8-391">Getting started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
