---
title: "Visual Studio ve C# - Azure Hdınsight'ta Apache Storm topolojileri | Microsoft Docs"
description: "Storm topolojilerini C# ' ta oluşturmayı öğrenin. Basit word count topolojisi için Visual Studio Hadoop araçlarını kullanarak Visual Studio'da oluşturun."
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
ms.openlocfilehash: 3ee89b6644ba395e0a6c28ecc2c082c2f7393ac8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-the-data-lake-tools-for-visual-studio"></a><span data-ttu-id="adf6b-104">Visual Studio için Data Lake araçları kullanarak Apache Storm için C# topolojileri geliştirme</span><span class="sxs-lookup"><span data-stu-id="adf6b-104">Develop C# topologies for Apache Storm by using the Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="adf6b-105">Visual Studio için Azure Data Lake (Hadoop) araçları kullanarak C# Storm topolojisini oluşturmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="adf6b-105">Learn how to create a C# Storm topology by using the Azure Data Lake (Hadoop) tools for Visual Studio.</span></span> <span data-ttu-id="adf6b-106">Bu belge Visual Studio'da bir Storm projesi oluşturma, yerel olarak test ve Azure Hdınsight kümesi üzerinde Apache Storm dağıtma işleminin adım adım anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="adf6b-106">This document walks through the process of creating a Storm project in Visual Studio, testing it locally, and deploying it to an Apache Storm on Azure HDInsight cluster.</span></span>

<span data-ttu-id="adf6b-107">Ayrıca C# ve Java bileşenlerini kullanan karma topolojiler oluşturmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="adf6b-107">You also learn how to create hybrid topologies that use C# and Java components.</span></span>

> [!NOTE]
> <span data-ttu-id="adf6b-108">Bu belgede yer alan adımlar Windows geliştirme ortamına Visual Studio ile kullanır, ancak bir Linux veya Windows tabanlı Hdınsight kümesine derlenmiş proje gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-108">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to either a Linux or Windows-based HDInsight cluster.</span></span> <span data-ttu-id="adf6b-109">Yalnızca Linux tabanlı kümelerde 28 Ekim 2016'dan sonra oluşturulan SCP.NET topolojileri destekler.</span><span class="sxs-lookup"><span data-stu-id="adf6b-109">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="adf6b-110">Linux tabanlı bir kümeyle bir C# topolojisi kullanmak için sürüm 0.10.0.6 için projeniz tarafından kullanılan veya üzeri Microsoft.SCP.Net.SDK NuGet paketini güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-110">To use a C# topology with a Linux-based cluster, you must update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or later.</span></span> <span data-ttu-id="adf6b-111">Paketin sürümünün ayrıca HDInsight üzerinde yüklü olan Storm ana sürümüyle eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-111">The version of the package must also match the major version of Storm installed on HDInsight.</span></span>

| <span data-ttu-id="adf6b-112">Hdınsight sürümü</span><span class="sxs-lookup"><span data-stu-id="adf6b-112">HDInsight version</span></span> | <span data-ttu-id="adf6b-113">Storm sürüm</span><span class="sxs-lookup"><span data-stu-id="adf6b-113">Storm version</span></span> | <span data-ttu-id="adf6b-114">SCP.NET sürüm</span><span class="sxs-lookup"><span data-stu-id="adf6b-114">SCP.NET version</span></span> | <span data-ttu-id="adf6b-115">Varsayılan Mono sürümü</span><span class="sxs-lookup"><span data-stu-id="adf6b-115">Default Mono version</span></span> |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| <span data-ttu-id="adf6b-116">3.3</span><span class="sxs-lookup"><span data-stu-id="adf6b-116">3.3</span></span> |<span data-ttu-id="adf6b-117">0.10.x</span><span class="sxs-lookup"><span data-stu-id="adf6b-117">0.10.x</span></span> |<span data-ttu-id="adf6b-118">0.10.x.x</span><span class="sxs-lookup"><span data-stu-id="adf6b-118">0.10.x.x</span></span></br><span data-ttu-id="adf6b-119">(yalnızca Windows tabanlı Hdınsight üzerinde)</span><span class="sxs-lookup"><span data-stu-id="adf6b-119">(only on Windows-based HDInsight)</span></span> | <span data-ttu-id="adf6b-120">NA</span><span class="sxs-lookup"><span data-stu-id="adf6b-120">NA</span></span> |
| <span data-ttu-id="adf6b-121">3.4</span><span class="sxs-lookup"><span data-stu-id="adf6b-121">3.4</span></span> | <span data-ttu-id="adf6b-122">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="adf6b-122">0.10.0.x</span></span> | <span data-ttu-id="adf6b-123">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="adf6b-123">0.10.0.x</span></span> | <span data-ttu-id="adf6b-124">3.2.8</span><span class="sxs-lookup"><span data-stu-id="adf6b-124">3.2.8</span></span> |
| <span data-ttu-id="adf6b-125">3,5</span><span class="sxs-lookup"><span data-stu-id="adf6b-125">3.5</span></span> | <span data-ttu-id="adf6b-126">1.0.2.x</span><span class="sxs-lookup"><span data-stu-id="adf6b-126">1.0.2.x</span></span> | <span data-ttu-id="adf6b-127">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="adf6b-127">1.0.0.x</span></span> | <span data-ttu-id="adf6b-128">4.2.1</span><span class="sxs-lookup"><span data-stu-id="adf6b-128">4.2.1</span></span> |
| <span data-ttu-id="adf6b-129">3.6</span><span class="sxs-lookup"><span data-stu-id="adf6b-129">3.6</span></span> | <span data-ttu-id="adf6b-130">1.1.0.x</span><span class="sxs-lookup"><span data-stu-id="adf6b-130">1.1.0.x</span></span> | <span data-ttu-id="adf6b-131">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="adf6b-131">1.0.0.x</span></span> | <span data-ttu-id="adf6b-132">4.2.8</span><span class="sxs-lookup"><span data-stu-id="adf6b-132">4.2.8</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="adf6b-133">Linux tabanlı kümelerdeki C# topolojilerinin .NET 4.5 kullanması ve HDInsight kümesi üzerinde çalışması için Mono kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-133">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span></span> <span data-ttu-id="adf6b-134">Denetleme [Mono Uyumluluk](http://www.mono-project.com/docs/about-mono/compatibility/) olası uyumsuzlukları için.</span><span class="sxs-lookup"><span data-stu-id="adf6b-134">Check [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) for potential incompatibilities.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="adf6b-135">Visual Studio yükleme</span><span class="sxs-lookup"><span data-stu-id="adf6b-135">Install Visual Studio</span></span>

<span data-ttu-id="adf6b-136">Visual Studio aşağıdaki sürümlerinden birini kullanarak C# topolojileri SCP.NET ile geliştirme yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="adf6b-136">You can develop C# topologies with SCP.NET by using one of the following versions of Visual Studio:</span></span>

* <span data-ttu-id="adf6b-137">Visual Studio 2012 ile [güncelleştirme 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="adf6b-137">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

* <span data-ttu-id="adf6b-138">Visual Studio 2013 [güncelleştirme 4](http://www.microsoft.com/download/details.aspx?id=44921) veya [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="adf6b-138">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>

* <span data-ttu-id="adf6b-139">Visual Studio 2015 veya [Visual Studio 2015 topluluk](https://go.microsoft.com/fwlink/?LinkId=532606)</span><span class="sxs-lookup"><span data-stu-id="adf6b-139">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span></span>

* <span data-ttu-id="adf6b-140">Visual Studio 2017 (herhangi bir sürümünü)</span><span class="sxs-lookup"><span data-stu-id="adf6b-140">Visual Studio 2017 (any edition)</span></span>

## <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="adf6b-141">Visual Studio için yükleme Data Lake araçları</span><span class="sxs-lookup"><span data-stu-id="adf6b-141">Install Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="adf6b-142">Visual Studio için Data Lake Araçları'nı yüklemek için adımları [Visual Studio için Data Lake araçları kullanarak çalışmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="adf6b-142">To install Data Lake tools for Visual Studio, follow the steps in [Get started using Data Lake tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

## <a name="install-java"></a><span data-ttu-id="adf6b-143">Java'yı yükleme</span><span class="sxs-lookup"><span data-stu-id="adf6b-143">Install Java</span></span>

<span data-ttu-id="adf6b-144">Visual Studio'dan bir Storm topolojisinin gönderdiğinizde, SCP.NET topoloji ve bağımlılıklarını içeren bir zip dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="adf6b-144">When you submit a Storm topology from Visual Studio, SCP.NET generates a zip file that contains the topology and dependencies.</span></span> <span data-ttu-id="adf6b-145">Linux tabanlı kümelerde ile daha uyumlu bir biçimde kullandığından Java bu ZIP dosyaları oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="adf6b-145">Java is used to create these zip files, because it uses a format that is more compatible with Linux-based clusters.</span></span>

1. <span data-ttu-id="adf6b-146">Geliştirme ortamınızı Java Geliştirme Seti (JDK) 7 veya sonraki bir sürümü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="adf6b-146">Install the Java Developer Kit (JDK) 7 or later on your development environment.</span></span> <span data-ttu-id="adf6b-147">Oracle JDK dan alabileceğiniz [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="adf6b-147">You can get the Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span> <span data-ttu-id="adf6b-148">Aynı zamanda [diğer Java dağıtımları](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="adf6b-148">You can also use [other Java distributions](http://openjdk.java.net/).</span></span>

2. <span data-ttu-id="adf6b-149">`JAVA_HOME` Ortam değişkeni Java içeren dizine işaret etmelidir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-149">The `JAVA_HOME` environment variable must point to the directory that contains Java.</span></span>

3. <span data-ttu-id="adf6b-150">`PATH` Ortam değişkeni içermelidir `%JAVA_HOME%\bin` dizin.</span><span class="sxs-lookup"><span data-stu-id="adf6b-150">The `PATH` environment variable must include the `%JAVA_HOME%\bin` directory.</span></span>

<span data-ttu-id="adf6b-151">Aşağıdaki C# konsol uygulaması, Java ve JDK düzgün yüklendiğini doğrulamak için kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="adf6b-151">You can use the following C# console application to verify that Java and the JDK are correctly installed:</span></span>

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

## <a name="storm-templates"></a><span data-ttu-id="adf6b-152">Storm şablonları</span><span class="sxs-lookup"><span data-stu-id="adf6b-152">Storm templates</span></span>

<span data-ttu-id="adf6b-153">Visual Studio için Data Lake araçları aşağıdaki şablonlar sağlar:</span><span class="sxs-lookup"><span data-stu-id="adf6b-153">The Data Lake tools for Visual Studio provide the following templates:</span></span>

| <span data-ttu-id="adf6b-154">Proje türü</span><span class="sxs-lookup"><span data-stu-id="adf6b-154">Project type</span></span> | <span data-ttu-id="adf6b-155">Gösterir</span><span class="sxs-lookup"><span data-stu-id="adf6b-155">Demonstrates</span></span> |
| --- | --- |
| <span data-ttu-id="adf6b-156">Storm uygulaması</span><span class="sxs-lookup"><span data-stu-id="adf6b-156">Storm Application</span></span> |<span data-ttu-id="adf6b-157">Boş bir Storm topolojisini projesi.</span><span class="sxs-lookup"><span data-stu-id="adf6b-157">An empty Storm topology project.</span></span> |
| <span data-ttu-id="adf6b-158">Storm Azure SQL yazıcı örnek</span><span class="sxs-lookup"><span data-stu-id="adf6b-158">Storm Azure SQL Writer Sample</span></span> |<span data-ttu-id="adf6b-159">Azure SQL veritabanına yazmak nasıl.</span><span class="sxs-lookup"><span data-stu-id="adf6b-159">How to write to Azure SQL Database.</span></span> |
| <span data-ttu-id="adf6b-160">Storm Azure Cosmos DB okuyucu örneği</span><span class="sxs-lookup"><span data-stu-id="adf6b-160">Storm Azure Cosmos DB Reader Sample</span></span> |<span data-ttu-id="adf6b-161">Azure Cosmos DB'den okumak nasıl.</span><span class="sxs-lookup"><span data-stu-id="adf6b-161">How to read from Azure Cosmos DB.</span></span> |
| <span data-ttu-id="adf6b-162">Storm Azure Cosmos DB yazan örnek</span><span class="sxs-lookup"><span data-stu-id="adf6b-162">Storm Azure Cosmos DB Writer Sample</span></span> |<span data-ttu-id="adf6b-163">Azure Cosmos DB yazma yapma.</span><span class="sxs-lookup"><span data-stu-id="adf6b-163">How to write to Azure Cosmos DB.</span></span> |
| <span data-ttu-id="adf6b-164">Storm EventHub okuyucu örneği</span><span class="sxs-lookup"><span data-stu-id="adf6b-164">Storm EventHub Reader Sample</span></span> |<span data-ttu-id="adf6b-165">Azure olay hub'larından okumayı yapma.</span><span class="sxs-lookup"><span data-stu-id="adf6b-165">How to read from Azure Event Hubs.</span></span> |
| <span data-ttu-id="adf6b-166">Storm EventHub yazan örnek</span><span class="sxs-lookup"><span data-stu-id="adf6b-166">Storm EventHub Writer Sample</span></span> |<span data-ttu-id="adf6b-167">Azure Event Hubs'a yazmak nasıl.</span><span class="sxs-lookup"><span data-stu-id="adf6b-167">How to write to Azure Event Hubs.</span></span> |
| <span data-ttu-id="adf6b-168">Storm HBase okuyucu örneği</span><span class="sxs-lookup"><span data-stu-id="adf6b-168">Storm HBase Reader Sample</span></span> |<span data-ttu-id="adf6b-169">Hdınsight'ta HBase okuma kümeleri.</span><span class="sxs-lookup"><span data-stu-id="adf6b-169">How to read from HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="adf6b-170">Storm HBase yazan örnek</span><span class="sxs-lookup"><span data-stu-id="adf6b-170">Storm HBase Writer Sample</span></span> |<span data-ttu-id="adf6b-171">Hdınsight'ta HBase için yazma kümeleri.</span><span class="sxs-lookup"><span data-stu-id="adf6b-171">How to write to HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="adf6b-172">Storm karma örnek</span><span class="sxs-lookup"><span data-stu-id="adf6b-172">Storm Hybrid Sample</span></span> |<span data-ttu-id="adf6b-173">Bir Java bileşeni kullanma</span><span class="sxs-lookup"><span data-stu-id="adf6b-173">How to use a Java component.</span></span> |
| <span data-ttu-id="adf6b-174">Storm örnek</span><span class="sxs-lookup"><span data-stu-id="adf6b-174">Storm Sample</span></span> |<span data-ttu-id="adf6b-175">Temel word count topolojisi.</span><span class="sxs-lookup"><span data-stu-id="adf6b-175">A basic word count topology.</span></span> |

> [!WARNING]
> <span data-ttu-id="adf6b-176">Tüm Şablonları Linux tabanlı Hdınsight ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="adf6b-176">Not all templates will work with Linux-based HDInsight.</span></span> <span data-ttu-id="adf6b-177">Şablonlar tarafından kullanılan Nuget paketleri Mono ile uyumlu olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-177">Nuget packages used by the templates may not be compatible with Mono.</span></span> <span data-ttu-id="adf6b-178">Denetleme [Mono Uyumluluk](http://www.mono-project.com/docs/about-mono/compatibility/) belge ve kullanma [.NET taşınabilirlik Çözümleyicisi](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) olası bir sorunu belirlemek için.</span><span class="sxs-lookup"><span data-stu-id="adf6b-178">Check the [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document and use the [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) to identify potential problems.</span></span>

<span data-ttu-id="adf6b-179">Bu belgede aşağıdaki adımlarda, bir topoloji oluşturmak için temel Storm uygulaması proje türü kullanın.</span><span class="sxs-lookup"><span data-stu-id="adf6b-179">In the steps in this document, you use the basic Storm Application project type to create a topology.</span></span>

### <a name="hbase-templates-notes"></a><span data-ttu-id="adf6b-180">HBase şablonları notları</span><span class="sxs-lookup"><span data-stu-id="adf6b-180">HBase templates notes</span></span>

<span data-ttu-id="adf6b-181">HBase okuyucu ve yazıcı şablonları, Hdınsight kümesinde bir HBase ile iletişim kurmak için değil HBase Java API HBase REST API kullanın.</span><span class="sxs-lookup"><span data-stu-id="adf6b-181">The HBase reader and writer templates use the HBase REST API, not the HBase Java API, to communicate with an HBase on HDInsight cluster.</span></span>

### <a name="eventhub-templates-notes"></a><span data-ttu-id="adf6b-182">EventHub şablonları notları</span><span class="sxs-lookup"><span data-stu-id="adf6b-182">EventHub templates notes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="adf6b-183">EventHub okuyucu şablonu ile birlikte gelen Java tabanlı EventHub spout bileşen sürüm 3.5 veya sonrasını hdınsight'ta Storm çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-183">The Java-based EventHub spout component included with the EventHub Reader template may not work with Storm on HDInsight version 3.5 or later.</span></span> <span data-ttu-id="adf6b-184">Bu bileşen güncelleştirilmiş bir sürümü kullanılabilir [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span><span class="sxs-lookup"><span data-stu-id="adf6b-184">An updated version of this component is available at [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span></span>

<span data-ttu-id="adf6b-185">Bu kullanan örnek bir topoloji için bkz: bileşen ve Hdınsight 3.5 üzerinde Storm ile works [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="adf6b-185">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

## <a name="create-a-c-topology"></a><span data-ttu-id="adf6b-186">Bir C# topolojisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="adf6b-186">Create a C# topology</span></span>

1. <span data-ttu-id="adf6b-187">Visual Studio'ni açın, **dosya** > **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-187">Open Visual Studio, select **File** > **New**, and then select **Project**.</span></span>

2. <span data-ttu-id="adf6b-188">Gelen **yeni proje** penceresinde genişletin **yüklü** > **şablonları**seçip **Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-188">From the **New Project** window, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span></span> <span data-ttu-id="adf6b-189">Şablonları listesinden seçin **Storm uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-189">From the list of templates, select **Storm Application**.</span></span> <span data-ttu-id="adf6b-190">Ekranın alt kısmındaki girin **WordCount** uygulamanın adı.</span><span class="sxs-lookup"><span data-stu-id="adf6b-190">At the bottom of the screen, enter **WordCount** as the name of the application.</span></span>

    ![Yeni Proje penceresinin ekran penceresi](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. <span data-ttu-id="adf6b-192">Proje oluşturduktan sonra aşağıdaki dosyaları sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="adf6b-192">After you have created the project, you should have the following files:</span></span>

   * <span data-ttu-id="adf6b-193">**Program.cs**: Bu dosya, projeniz için topoloji tanımlar.</span><span class="sxs-lookup"><span data-stu-id="adf6b-193">**Program.cs**: This file defines the topology for your project.</span></span> <span data-ttu-id="adf6b-194">Bir spout ve bir Cıvata oluşan bir varsayılan topolojisi varsayılan olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="adf6b-194">A default topology that consists of one spout and one bolt is created by default.</span></span>

   * <span data-ttu-id="adf6b-195">**Spout.cs**: rastgele sayılar yayar bir örnek spout.</span><span class="sxs-lookup"><span data-stu-id="adf6b-195">**Spout.cs**: An example spout that emits random numbers.</span></span>

   * <span data-ttu-id="adf6b-196">**Bolt.cs**: spout'un gösterilen sayıların sayısı tutan bir örnek Cıvata.</span><span class="sxs-lookup"><span data-stu-id="adf6b-196">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by the spout.</span></span>

     <span data-ttu-id="adf6b-197">NuGet proje oluşturduğunuzda, en son yüklemeleri [SCP.NET paket](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span><span class="sxs-lookup"><span data-stu-id="adf6b-197">When you create the project, NuGet downloads the latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span></span>

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-the-spout"></a><span data-ttu-id="adf6b-198">Spout uygulama</span><span class="sxs-lookup"><span data-stu-id="adf6b-198">Implement the spout</span></span>

1. <span data-ttu-id="adf6b-199">Açık **Spout.cs**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-199">Open **Spout.cs**.</span></span> <span data-ttu-id="adf6b-200">Spout'lar bir dış kaynaktan topolojisinde verileri okumak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="adf6b-200">Spouts are used to read data in a topology from an external source.</span></span> <span data-ttu-id="adf6b-201">Bir spout için ana bileşeni vardır:</span><span class="sxs-lookup"><span data-stu-id="adf6b-201">The main components for a spout are:</span></span>

   * <span data-ttu-id="adf6b-202">**NextTuple**: spout yeni tanımlama grubu yayma izin Storm tarafından çağrılır.</span><span class="sxs-lookup"><span data-stu-id="adf6b-202">**NextTuple**: Called by Storm when the spout is allowed to emit new tuples.</span></span>

   * <span data-ttu-id="adf6b-203">**ACK** (yalnızca işlem topolojisi): spout gönderilen diziler için topolojideki başka bileşenler tarafından başlatılan onayları işler.</span><span class="sxs-lookup"><span data-stu-id="adf6b-203">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in the topology for tuples sent from the spout.</span></span> <span data-ttu-id="adf6b-204">Bir tanımlama grubu aktarımının aşağı akış bileşenleri tarafından başarıyla işlendi bilmeniz spout olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="adf6b-204">Acknowledging a tuple lets the spout know that it was processed successfully by downstream components.</span></span>

   * <span data-ttu-id="adf6b-205">**Başarısız** (yalnızca işlem topolojisi): işleme, başarısız topoloji içindeki diğer bileşenlere işleme tanımlama grubu.</span><span class="sxs-lookup"><span data-stu-id="adf6b-205">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in the topology.</span></span> <span data-ttu-id="adf6b-206">Başarısız yöntemi uygulama, böylece yeniden işlenebilir tanımlama grubu yeniden yayma olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="adf6b-206">Implementing a Fail method allows you to re-emit the tuple so that it can be processed again.</span></span>

2. <span data-ttu-id="adf6b-207">Değiştir **Spout** aşağıdaki metinle sınıfı.</span><span class="sxs-lookup"><span data-stu-id="adf6b-207">Replace the contents of the **Spout** class with the following text.</span></span> <span data-ttu-id="adf6b-208">Bu spout bir cümle rastgele topoloji yayar.</span><span class="sxs-lookup"><span data-stu-id="adf6b-208">This spout randomly emits a sentence into the topology.</span></span>

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "the cow jumped over the moon",
        "an apple a day keeps the doctor away",
        "four score and seven years ago",
        "snow white and the seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set the instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // The schema for the default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of the spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // The sentence to be emitted
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

### <a name="implement-the-bolts"></a><span data-ttu-id="adf6b-209">Cıvatalar uygulama</span><span class="sxs-lookup"><span data-stu-id="adf6b-209">Implement the bolts</span></span>

1. <span data-ttu-id="adf6b-210">Varolan silme **Bolt.cs** proje dosyasından.</span><span class="sxs-lookup"><span data-stu-id="adf6b-210">Delete the existing **Bolt.cs** file from the project.</span></span>

2. <span data-ttu-id="adf6b-211">İçinde **Çözüm Gezgini**, projeye sağ tıklayın ve seçin **Ekle** > **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-211">In **Solution Explorer**, right-click the project, and select **Add** > **New item**.</span></span> <span data-ttu-id="adf6b-212">Listesinden **Storm Cıvata**ve girin **Splitter.cs** adı.</span><span class="sxs-lookup"><span data-stu-id="adf6b-212">From the list, select **Storm Bolt**, and enter **Splitter.cs** as the name.</span></span> <span data-ttu-id="adf6b-213">Adlı ikinci bir Cıvata oluşturmak için bu işlemi yineleyin **Counter.cs**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-213">Repeat this process to create a second bolt named **Counter.cs**.</span></span>

   * <span data-ttu-id="adf6b-214">**Splitter.cs**: cümleleri tek tek sözcüklere böler ve yeni akış sözcüklerin yayar Cıvata uygular.</span><span class="sxs-lookup"><span data-stu-id="adf6b-214">**Splitter.cs**: Implements a bolt that splits sentences into individual words, and emits a new stream of words.</span></span>

   * <span data-ttu-id="adf6b-215">**Counter.cs**: her sözcüğün sayar ve sözcükleri ve sayısı her sözcüğün için yeni bir akış yayar Cıvata uygular.</span><span class="sxs-lookup"><span data-stu-id="adf6b-215">**Counter.cs**: Implements a bolt that counts each word, and emits a new stream of words and the count for each word.</span></span>

     > [!NOTE]
     > <span data-ttu-id="adf6b-216">Bu Cıvatalar okuma ve akışlara yazma, ancak bir veritabanı veya hizmet gibi kaynakları ile iletişim kurmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="adf6b-216">These bolts read and write to streams, but you can also use a bolt to communicate with sources such as a database or service.</span></span>

3. <span data-ttu-id="adf6b-217">Açık **Splitter.cs**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-217">Open **Splitter.cs**.</span></span> <span data-ttu-id="adf6b-218">Varsayılan olarak yalnızca bir yöntemi vardır: **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-218">It has only one method by default: **Execute**.</span></span> <span data-ttu-id="adf6b-219">Execute yöntemi Cıvata işlemek için bir tanımlama grubu aldığında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="adf6b-219">The Execute method is called when the bolt receives a tuple for processing.</span></span> <span data-ttu-id="adf6b-220">Burada, okuma ve gelen diziler işlemek ve giden tanımlama grubu yayma.</span><span class="sxs-lookup"><span data-stu-id="adf6b-220">Here, you can read and process incoming tuples, and emit outbound tuples.</span></span>

4. <span data-ttu-id="adf6b-221">Değiştir **Bölümlendirici** aşağıdaki kodla sınıfı:</span><span class="sxs-lookup"><span data-stu-id="adf6b-221">Replace the contents of the **Splitter** class with the following code:</span></span>

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (the sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (the word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of the bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get the sentence from the tuple
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

5. <span data-ttu-id="adf6b-222">Açık **Counter.cs**ve sınıf içeriğini aşağıdakilerle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="adf6b-222">Open **Counter.cs**, and replace the class contents with the following:</span></span>

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
        // A tuple containing a string field - the word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - the word and the word count
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

        // Get the word from the tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for the word in the dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment the count
        count++;
        // Update the count in the dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit the word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-the-topology"></a><span data-ttu-id="adf6b-223">Topolojisi tanımlayın</span><span class="sxs-lookup"><span data-stu-id="adf6b-223">Define the topology</span></span>

<span data-ttu-id="adf6b-224">Spout'lar ve Cıvatalar bileşenler arasında veri akışını tanımlayan bir grafik halinde düzenlenir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-224">Spouts and bolts are arranged in a graph, which defines how the data flows between components.</span></span> <span data-ttu-id="adf6b-225">Bu topoloji, grafiği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="adf6b-225">For this topology, the graph is as follows:</span></span>

![Bileşenleri nasıl düzenlenir diyagramı](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

<span data-ttu-id="adf6b-227">Cümleleri spout yayılan ve Bölümlendirici Cıvata örneklerine dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="adf6b-227">Sentences are emitted from the spout, and are distributed to instances of the Splitter bolt.</span></span> <span data-ttu-id="adf6b-228">Bölümlendirici Cıvata cümleleri sayaç Cıvata dağıtılmış sözcükler içine keser.</span><span class="sxs-lookup"><span data-stu-id="adf6b-228">The Splitter bolt breaks the sentences into words, which are distributed to the Counter bolt.</span></span>

<span data-ttu-id="adf6b-229">Sözcük sayısını yerel olarak sayaç örneğinde tutulmadığından belirli kelimeleri aynı sayacı Cıvata örneğini akış emin olmak istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="adf6b-229">Because word count is held locally in the Counter instance, we want to make sure that specific words flow to the same Counter bolt instance.</span></span> <span data-ttu-id="adf6b-230">Her bir örnek, belirli kelimeleri izler.</span><span class="sxs-lookup"><span data-stu-id="adf6b-230">Each instance keeps track of specific words.</span></span> <span data-ttu-id="adf6b-231">Bölümlendirici Cıvata hiçbir durumunu koruyan olduğundan, gerçekten Bölümlendirici hangi örneğinin hangi tümceyi alır önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-231">Since the Splitter bolt maintains no state, it really doesn't matter which instance of the splitter receives which sentence.</span></span>

<span data-ttu-id="adf6b-232">Açık **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-232">Open **Program.cs**.</span></span> <span data-ttu-id="adf6b-233">Önemli yöntemi **GetTopologyBuilder**, Storm için gönderilen topoloji tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="adf6b-233">The important method is **GetTopologyBuilder**, which is used to define the topology that is submitted to Storm.</span></span> <span data-ttu-id="adf6b-234">Değiştir **GetTopologyBuilder** daha önce açıklanan topoloji uygulamak için aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="adf6b-234">Replace the contents of **GetTopologyBuilder** with the following code to implement the topology described previously:</span></span>

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add the spout to the topology.
// Name the component 'sentences'
// Name the field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add the splitter bolt to the topology.
// Name the component 'splitter'
// Name the field that is emitted 'word'
// Use suffleGrouping to distribute incoming tuples
//   from the 'sentences' spout across instances
//   of the splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add the counter bolt to the topology.
// Name the component 'counter'
// Name the fields that are emitted 'word' and 'count'
// Use fieldsGrouping to ensure that tuples are routed
//   to counter instances based on the contents of field
//   position 0 (the word). This could also have been
//   List<string>(){"word"}.
//   This ensures that the word 'jumped', for example, will always
//   go to the same instance
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

## <a name="submit-the-topology"></a><span data-ttu-id="adf6b-235">Topoloji gönderme</span><span class="sxs-lookup"><span data-stu-id="adf6b-235">Submit the topology</span></span>

1. <span data-ttu-id="adf6b-236">İçinde **Çözüm Gezgini**, projeye sağ tıklayın ve seçin **Hdınsight üzerinde Storm Gönder**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-236">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="adf6b-237">İstenirse, Azure aboneliğiniz için kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="adf6b-237">If prompted, enter the credentials for your Azure subscription.</span></span> <span data-ttu-id="adf6b-238">Birden fazla aboneliğiniz varsa, Hdınsight kümesi üzerinde Storm'a içeren oturum açın.</span><span class="sxs-lookup"><span data-stu-id="adf6b-238">If you have more than one subscription, sign in to the one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="adf6b-239">Hdınsight küme üzerinde Storm'a seçin **Storm kümesi** aşağı açılan listeyi ve ardından **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-239">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="adf6b-240">Gönderim kullanarak başarılı olursa, izleyebilirsiniz **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="adf6b-240">You can monitor if the submission is successful by using the **Output** window.</span></span>

3. <span data-ttu-id="adf6b-241">Topoloji başarıyla gönderildi, **Storm topolojilerini** küme görünür.</span><span class="sxs-lookup"><span data-stu-id="adf6b-241">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span></span> <span data-ttu-id="adf6b-242">Seçin **WordCount** çalışan topolojisi ile ilgili bilgileri görüntülemek için listeden topolojisi.</span><span class="sxs-lookup"><span data-stu-id="adf6b-242">Select the **WordCount** topology from the list to view information about the running topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="adf6b-243">Ayrıca görüntüleyebilirsiniz **Storm topolojilerini** gelen **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-243">You can also view **Storm Topologies** from **Server Explorer**.</span></span> <span data-ttu-id="adf6b-244">Genişletme **Azure** > **Hdınsight**, Hdınsight kümesinde bir Storm sağ tıklayın ve ardından **görünüm Storm topolojilerini**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-244">Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span></span>

    <span data-ttu-id="adf6b-245">Topolojide bileşenleri hakkında bilgi görüntülemek için diyagramdaki bileşeni çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="adf6b-245">To view information about the components in the topology, double-click the component in the diagram.</span></span>

4. <span data-ttu-id="adf6b-246">Gelen **topoloji özeti** görüntülemek için tıklatın **KILL** topoloji durdurmak için.</span><span class="sxs-lookup"><span data-stu-id="adf6b-246">From the **Topology Summary** view, click **Kill** to stop the topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="adf6b-247">Storm topolojilerini devre dışı bırakılır veya küme silinene kadar çalışmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="adf6b-247">Storm topologies continue to run until they are deactivated, or the cluster is deleted.</span></span>

## <a name="transactional-topology"></a><span data-ttu-id="adf6b-248">İşlem topolojisi</span><span class="sxs-lookup"><span data-stu-id="adf6b-248">Transactional topology</span></span>

<span data-ttu-id="adf6b-249">Önceki işlem olmayan topolojidir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-249">The previous topology is non-transactional.</span></span> <span data-ttu-id="adf6b-250">Topoloji bileşenlerinde iletileri yeniden oynatmak için işlevsellik kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="adf6b-250">The components in the topology do not implement functionality to replaying messages.</span></span> <span data-ttu-id="adf6b-251">Bir işlem topolojisi ilişkin bir örnek, bir proje oluşturmak ve **Storm örnek** proje türü olarak.</span><span class="sxs-lookup"><span data-stu-id="adf6b-251">For an example of a transactional topology, create a project and select **Storm Sample** as the project type.</span></span>

<span data-ttu-id="adf6b-252">İşlem topolojileri yeniden yürütme veri desteklemek için aşağıdakileri uygulayın:</span><span class="sxs-lookup"><span data-stu-id="adf6b-252">Transactional topologies implement the following to support replay of data:</span></span>

* <span data-ttu-id="adf6b-253">**Meta verileri önbelleğe alma**: spout meta verileri alınır ve bir hata oluşursa yeniden yayılan böylece yayılan veriler hakkında depolamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-253">**Metadata caching**: The spout must store metadata about the data emitted, so that the data can be retrieved and emitted again if a failure occurs.</span></span> <span data-ttu-id="adf6b-254">Örnek tarafından yayılan veriler küçük olduğundan, her tanımlama grubu için ham verileri yeniden yürütme için bir sözlük depolanır.</span><span class="sxs-lookup"><span data-stu-id="adf6b-254">Because the data emitted by the sample is small, the raw data for each tuple is stored in a dictionary for replay.</span></span>

* <span data-ttu-id="adf6b-255">**ACK**: her Cıvata topolojisi içinde çağırabilirsiniz `this.ctx.Ack(tuple)` bir tanımlama grubu başarıyla işlediği bildiremedi.</span><span class="sxs-lookup"><span data-stu-id="adf6b-255">**Ack**: Each bolt in the topology can call `this.ctx.Ack(tuple)` to acknowledge that it has successfully processed a tuple.</span></span> <span data-ttu-id="adf6b-256">Tüm Cıvatalar tuple acked olduğunda `Ack` spout yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="adf6b-256">When all bolts have acked the tuple, the `Ack` method of the spout is invoked.</span></span> <span data-ttu-id="adf6b-257">`Ack` Spout yeniden yürütme için önbelleğe verileri kaldırmak bir yöntem sağlar.</span><span class="sxs-lookup"><span data-stu-id="adf6b-257">The `Ack` method allows the spout to remove data that was cached for replay.</span></span>

* <span data-ttu-id="adf6b-258">**Başarısız**: her Cıvata çağırabilirsiniz `this.ctx.Fail(tuple)` işleme için bir tanımlama grubu başarısız olduğunu belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="adf6b-258">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` to indicate that processing has failed for a tuple.</span></span> <span data-ttu-id="adf6b-259">İçin hata yayar `Fail` burada yer alan tanımlama grubu yeniden kullanarak spout yöntemi önbelleğe alınan meta verileri.</span><span class="sxs-lookup"><span data-stu-id="adf6b-259">The failure propagates to the `Fail` method of the spout, where the tuple can be replayed by using cached metadata.</span></span>

* <span data-ttu-id="adf6b-260">**Sıra kimliği**: bir tanımlama grubu yayma, benzersiz sıra kimliği belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-260">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span></span> <span data-ttu-id="adf6b-261">Bu değer tanımlama grubu yeniden yürütme (Ack ve başarısız) işleme tanımlar.</span><span class="sxs-lookup"><span data-stu-id="adf6b-261">This value identifies the tuple for replay (Ack and Fail) processing.</span></span> <span data-ttu-id="adf6b-262">Spout Örneğin, **Storm örnek** project veri yayma olduğunda aşağıdaki kullanır:</span><span class="sxs-lookup"><span data-stu-id="adf6b-262">For example, the spout in the **Storm Sample** project uses the following when emitting data:</span></span>

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    <span data-ttu-id="adf6b-263">Bu kod içinde yer alan sırası kimliği değerine sahip bir cümle varsayılan akışa içeren bir tanımlama grubu yayar **lastSeqId**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-263">This code emits a tuple that contains a sentence to the default stream, with the sequence ID value contained in **lastSeqId**.</span></span> <span data-ttu-id="adf6b-264">Bu örnek için **lastSeqId** gösterilen her bir tanımlama grubu için artırılır.</span><span class="sxs-lookup"><span data-stu-id="adf6b-264">For this example, **lastSeqId** is incremented for every tuple emitted.</span></span>

<span data-ttu-id="adf6b-265">Örnekte gösterildiği şekilde **Storm örnek** proje, bir bileşenin işlem olup yapılandırmasını temel alarak zamanında ayarlanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-265">As demonstrated in the **Storm Sample** project, whether a component is transactional can be set at runtime, based on configuration.</span></span>

## <a name="hybrid-topology-with-c-and-java"></a><span data-ttu-id="adf6b-266">C# ve Java ile karma topolojisi</span><span class="sxs-lookup"><span data-stu-id="adf6b-266">Hybrid topology with C# and Java</span></span>

<span data-ttu-id="adf6b-267">Burada bazı bileşenleri C# ve diğerleri Java karma topolojiler oluşturmak için Visual Studio için Data Lake araçları da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="adf6b-267">You can also use Data Lake tools for Visual Studio to create hybrid topologies, where some components are C# and others are Java.</span></span>

<span data-ttu-id="adf6b-268">Bir karma topolojisi ilişkin bir örnek, bir proje oluşturmak ve **Storm karma örnek**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-268">For an example of a hybrid topology, create a project and select **Storm Hybrid Sample**.</span></span> <span data-ttu-id="adf6b-269">Bu örnek türü aşağıdaki kavramları göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="adf6b-269">This sample type demonstrates the following concepts:</span></span>

* <span data-ttu-id="adf6b-270">**Java spout** ve **C# Cıvata**: tanımlıysa **HybridTopology_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-270">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**.</span></span>

    * <span data-ttu-id="adf6b-271">İşlem sürüm tanımlanan **HybridTopologyTx_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-271">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**.</span></span>

* <span data-ttu-id="adf6b-272">**C# spout** ve **Java Cıvata**: tanımlıysa **HybridTopology_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-272">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**.</span></span>

    * <span data-ttu-id="adf6b-273">İşlem sürüm tanımlanan **HybridTopologyTx_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-273">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="adf6b-274">Bu sürüm ayrıca Clojure kodu bir metin dosyasından bir Java bileşeni olarak kullanımı gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-274">This version also demonstrates how to use Clojure code from a text file as a Java component.</span></span>


<span data-ttu-id="adf6b-275">Proje gönderildiğinde, kullanılan topoloji geçiş yapmak için yalnızca taşıma `[Active(true)]` kümeye göndermeden önce kullanmak istediğiniz topoloji ifadesine.</span><span class="sxs-lookup"><span data-stu-id="adf6b-275">To switch the topology that is used when the project is submitted, simply move the `[Active(true)]` statement to the topology you want to use, before submitting it to the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="adf6b-276">Gerekli olan tüm Java dosyalar bu projede bir parçası olarak sağlanan **JavaDependency** klasör.</span><span class="sxs-lookup"><span data-stu-id="adf6b-276">All the Java files that are required are provided as part of this project in the **JavaDependency** folder.</span></span>

<span data-ttu-id="adf6b-277">Oluşturma ve karma topolojisi gönderme aşağıdakileri dikkate alın:</span><span class="sxs-lookup"><span data-stu-id="adf6b-277">Consider the following when you are creating and submitting a hybrid topology:</span></span>

* <span data-ttu-id="adf6b-278">Kullanmalısınız **JavaComponentConstructor** bir spout için Java sınıfının bir örneği oluşturulamadı veya Cıvata.</span><span class="sxs-lookup"><span data-stu-id="adf6b-278">You must use **JavaComponentConstructor** to create an instance of the Java class for a spout or bolt.</span></span>

* <span data-ttu-id="adf6b-279">Kullanmanız gereken **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** verilerini içine veya dışına Java nesnelerini Java bileşenlerini JSON için seri hale getirmek için.</span><span class="sxs-lookup"><span data-stu-id="adf6b-279">You should use **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** to serialize data into or out of Java components from Java objects to JSON.</span></span>

* <span data-ttu-id="adf6b-280">Sunucuya topoloji gönderirken kullanmalısınız **ek yapılandırmalar** belirtmek için seçeneği **Java dosya yolları**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-280">When submitting the topology to the server, you must use the **Additional configurations** option to specify the **Java File paths**.</span></span> <span data-ttu-id="adf6b-281">Belirtilen yol, Java sınıfları içeren JAR dosyaları içeren dizini olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="adf6b-281">The path specified should be the directory that contains the JAR files that contain your Java classes.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="adf6b-282">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="adf6b-282">Azure Event Hubs</span></span>

<span data-ttu-id="adf6b-283">SCP.NET sürüm 0.9.4.203 bir yeni sınıf ve olay hub'ı spout (olay hub'larından okuyan bir Java spout) ile çalışmak için özellikle yöntemi sunar.</span><span class="sxs-lookup"><span data-stu-id="adf6b-283">SCP.NET version 0.9.4.203 introduces a new class and method specifically for working with the Event Hub spout (a Java spout that reads from Event Hubs).</span></span> <span data-ttu-id="adf6b-284">Bir olay hub'ı spout kullanan bir topolojisi oluşturduğunuzda, aşağıdaki yöntemleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="adf6b-284">When you create a topology that uses an Event Hub spout, use the following methods:</span></span>

* <span data-ttu-id="adf6b-285">**EventHubSpoutConfig** sınıfı: spout bileşeni için yapılandırma içeren bir nesne oluşturur.</span><span class="sxs-lookup"><span data-stu-id="adf6b-285">**EventHubSpoutConfig** class: Creates an object that contains the configuration for the spout component.</span></span>

* <span data-ttu-id="adf6b-286">**TopologyBuilder.SetEventHubSpout** yöntemi: olay hub'ı spout bileşeni topolojiye ekler.</span><span class="sxs-lookup"><span data-stu-id="adf6b-286">**TopologyBuilder.SetEventHubSpout** method: Adds the Event Hub spout component to the topology.</span></span>

> [!NOTE]
> <span data-ttu-id="adf6b-287">Hala kullanmalısınız **CustomizedInteropJSONSerializer** spout tarafından üretilen veri seri hale getirilemedi.</span><span class="sxs-lookup"><span data-stu-id="adf6b-287">You must still use the **CustomizedInteropJSONSerializer** to serialize data produced by the spout.</span></span>

## <span data-ttu-id="adf6b-288"><a id="configurationmanager"></a>ConfigurationManager kullanın</span><span class="sxs-lookup"><span data-stu-id="adf6b-288"><a id="configurationmanager"></a>Use ConfigurationManager</span></span>

<span data-ttu-id="adf6b-289">Kullanmayan **ConfigurationManager** Cıvata yapılandırma değerlerini almak ve bileşenleri spout.</span><span class="sxs-lookup"><span data-stu-id="adf6b-289">Don't use **ConfigurationManager** to retrieve configuration values from bolt and spout components.</span></span> <span data-ttu-id="adf6b-290">Bunun yapılması bir null işaretçi özel durumu neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-290">Doing so can cause a null pointer exception.</span></span> <span data-ttu-id="adf6b-291">Bunun yerine, projeniz için yapılandırma Storm topolojisini topoloji bağlamında bir anahtar ve değer çifti olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-291">Instead, the configuration for your project is passed into the Storm topology as a key and value pair in the topology context.</span></span> <span data-ttu-id="adf6b-292">Yapılandırma değerlerini kullanır her bileşenin bunları başlatma sırasında bağlamdan almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-292">Each component that relies on configuration values must retrieve them from the context during initialization.</span></span>

<span data-ttu-id="adf6b-293">Aşağıdaki kod, bu değerleri almaya gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="adf6b-293">The following code demonstrates how to retrieve these values:</span></span>

```csharp
public class MyComponent : ISCPBolt
{
    // To hold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of the context for this component instance
        this.ctx = ctx;
        // If it exists, load the configuration for the component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve the value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

<span data-ttu-id="adf6b-294">Kullanırsanız, bir `Get` , bileşeninin bir örneğini döndürülecek yöntemi her ikisi de geçirir emin olmalısınız `Context` ve `Dictionary<string, Object>` Oluşturucusu parametrelerinin.</span><span class="sxs-lookup"><span data-stu-id="adf6b-294">If you use a `Get` method to return an instance of your component, you must ensure that it passes both the `Context` and `Dictionary<string, Object>` parameters to the constructor.</span></span> <span data-ttu-id="adf6b-295">Aşağıdaki örnek temel olan `Get` düzgün bu değerleri geçirir yöntemi:</span><span class="sxs-lookup"><span data-stu-id="adf6b-295">The following example is a basic `Get` method that properly passes these values:</span></span>

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-to-update-scpnet"></a><span data-ttu-id="adf6b-296">SCP.NET güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="adf6b-296">How to update SCP.NET</span></span>

<span data-ttu-id="adf6b-297">Paket yükseltmesi NuGet aracılığıyla SCP.NET en son sürümleri destekler.</span><span class="sxs-lookup"><span data-stu-id="adf6b-297">Recent releases of SCP.NET support package upgrade through NuGet.</span></span> <span data-ttu-id="adf6b-298">Yeni bir güncelleştirme kullanılabilir olduğunda, bir yükseltme bildirimi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="adf6b-298">When a new update is available, you receive an upgrade notification.</span></span> <span data-ttu-id="adf6b-299">El ile yükseltme için denetlemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="adf6b-299">To manually check for an upgrade, follow these steps:</span></span>

1. <span data-ttu-id="adf6b-300">İçinde **Çözüm Gezgini**, projeye sağ tıklayın ve seçin **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-300">In **Solution Explorer**, right-click the project, and select **Manage NuGet Packages**.</span></span>

2. <span data-ttu-id="adf6b-301">Paket Yöneticisi'nden seçin **güncelleştirmeleri**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-301">From the package manager, select **Updates**.</span></span> <span data-ttu-id="adf6b-302">Bir güncelleştirme olup olmadığını listelenir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-302">If an update is available, it is listed.</span></span> <span data-ttu-id="adf6b-303">Tıklatın **güncelleştirme** paketi yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="adf6b-303">Click **Update** for the package to install it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="adf6b-304">Projenizin NuGet kullanmadı SCP.NET önceki bir sürümüyle oluşturulduysa, daha yeni bir sürüme güncelleştirmek için aşağıdaki adımları gerçekleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="adf6b-304">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform the following steps to update to a newer version:</span></span>
>
> 1. <span data-ttu-id="adf6b-305">İçinde **Çözüm Gezgini**, projeye sağ tıklayın ve seçin **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-305">In **Solution Explorer**, right-click the project, and select **Manage NuGet Packages**.</span></span>
> 2. <span data-ttu-id="adf6b-306">Kullanarak **arama** alanına arayın ve ardından ekleyin, **Microsoft.SCP.Net.SDK** projeye.</span><span class="sxs-lookup"><span data-stu-id="adf6b-306">Using the **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** to the project.</span></span>

## <a name="troubleshoot-common-issues-with-topologies"></a><span data-ttu-id="adf6b-307">Topolojileri ile ilgili genel sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="adf6b-307">Troubleshoot common issues with topologies</span></span>

### <a name="null-pointer-exceptions"></a><span data-ttu-id="adf6b-308">Null işaretçi özel durumlar</span><span class="sxs-lookup"><span data-stu-id="adf6b-308">Null pointer exceptions</span></span>

<span data-ttu-id="adf6b-309">Bir C# topolojisi ile Linux tabanlı Hdınsight kümesi kullanırken, Cıvata ve kullanan bileşenleri spout **ConfigurationManager** yapılandırma ayarlarını çalışma zamanında null işaretçi özel durumlar döndürebilir okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="adf6b-309">When you are using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use **ConfigurationManager** to read configuration settings at runtime may return null pointer exceptions.</span></span>

<span data-ttu-id="adf6b-310">Projeniz için yapılandırma Storm topolojisini topoloji bağlamında bir anahtar ve değer çifti olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-310">The configuration for your project is passed into the Storm topology as a key and value pair in the topology context.</span></span> <span data-ttu-id="adf6b-311">Bunlar hazırlarken bileşenlerinizin geçirilen sözlük nesnesi alınabilir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-311">It can be retrieved from the dictionary object that is passed to your components when they are initialized.</span></span>

<span data-ttu-id="adf6b-312">Daha fazla bilgi için bkz: [ConfigurationManager](#configurationmanager) bu belgenin bölüm.</span><span class="sxs-lookup"><span data-stu-id="adf6b-312">For more information, see the [ConfigurationManager](#configurationmanager) section of this document.</span></span>

### <a name="systemtypeloadexception"></a><span data-ttu-id="adf6b-313">System.TypeLoadException</span><span class="sxs-lookup"><span data-stu-id="adf6b-313">System.TypeLoadException</span></span>

<span data-ttu-id="adf6b-314">Bir C# topolojisi ile Linux tabanlı Hdınsight kümesi kullanırken, şu hatayla karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="adf6b-314">When you are using a C# topology with a Linux-based HDInsight cluster, you may encounter the following error:</span></span>

    System.TypeLoadException: Failure has occurred while loading a type.

<span data-ttu-id="adf6b-315">Mono destekleyen .NET sürümü ile uyumlu olmayan bir ikili kullandığınızda bu hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="adf6b-315">This error occurs when you use a binary that is not compatible with the version of .NET that Mono supports.</span></span>

<span data-ttu-id="adf6b-316">Linux tabanlı Hdınsight kümeleri için projeniz .NET 4. 5'için derlenmiş ikili dosyaları kullandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="adf6b-316">For Linux-based HDInsight clusters, make sure that your project uses binaries compiled for .NET 4.5.</span></span>

### <a name="test-a-topology-locally"></a><span data-ttu-id="adf6b-317">Bir topoloji yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="adf6b-317">Test a topology locally</span></span>

<span data-ttu-id="adf6b-318">Bazı durumlarda, bir küme için bir topolojisi dağıtmak kolay olmasına rağmen bir topoloji yerel olarak test gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-318">Although it is easy to deploy a topology to a cluster, in some cases, you may need to test a topology locally.</span></span> <span data-ttu-id="adf6b-319">Ve geliştirme ortamınızı yerel olarak bu öğreticideki örnek topoloji test çalıştırmak için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="adf6b-319">Use the following steps to run and test the example topology in this tutorial locally in your development environment.</span></span>

> [!WARNING]
> <span data-ttu-id="adf6b-320">Yerel test yalnızca çalışır için basic, C#-yalnızca topolojileri.</span><span class="sxs-lookup"><span data-stu-id="adf6b-320">Local testing only works for basic, C#-only topologies.</span></span> <span data-ttu-id="adf6b-321">Karma topolojiler veya birden çok akış kullanmak Topolojileri için yerel test kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="adf6b-321">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span></span>

1. <span data-ttu-id="adf6b-322">İçinde **Çözüm Gezgini**, projeye sağ tıklayın ve seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-322">In **Solution Explorer**, right-click the project, and select **Properties**.</span></span> <span data-ttu-id="adf6b-323">Proje Özellikleri'nde değiştirme **çıktı türü** için **konsol uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-323">In the project properties, change the **Output type** to **Console Application**.</span></span>

    ![Vurgulanan çıktı türü ile Proje Özellikleri'nin ekran görüntüsü](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > <span data-ttu-id="adf6b-325">Değiştirmeyi unutmayın **çıktı türü** başa **sınıf kitaplığı** bir kümeye topoloji dağıtmadan önce.</span><span class="sxs-lookup"><span data-stu-id="adf6b-325">Remember to change the **Output type** back to **Class Library** before you deploy the topology to a cluster.</span></span>

2. <span data-ttu-id="adf6b-326">İçinde **Çözüm Gezgini**projeye sağ tıklayın ve ardından **Ekle** > **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-326">In **Solution Explorer**, right-click the project, and then select **Add** > **New Item**.</span></span> <span data-ttu-id="adf6b-327">Seçin **sınıfı**ve girin **LocalTest.cs** sınıfı adı.</span><span class="sxs-lookup"><span data-stu-id="adf6b-327">Select **Class**, and enter **LocalTest.cs** as the class name.</span></span> <span data-ttu-id="adf6b-328">Son olarak, tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-328">Finally, click **Add**.</span></span>

3. <span data-ttu-id="adf6b-329">Açık **LocalTest.cs**ve aşağıdakileri ekleyin **kullanarak** deyimini dosyanın üst:</span><span class="sxs-lookup"><span data-stu-id="adf6b-329">Open **LocalTest.cs**, and add the following **using** statement at the top:</span></span>

    ```csharp
    using Microsoft.SCP;
    ```

4. <span data-ttu-id="adf6b-330">Aşağıdaki kod içeriğini kullanmak **LocalTest** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="adf6b-330">Use the following code as the contents of the **LocalTest** class:</span></span>

    ```csharp
    // Drives the topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test the spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of the spout, using the local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext to persist the data stream to file
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test the splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of the bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set the data stream to the data created by the spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from the stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in the batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext to persist the data stream to file
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test the counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of the bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set the data stream to the data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from the stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in the batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext to persist the data stream to file
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    <span data-ttu-id="adf6b-331">Kod açıklamaları okumak için bir dakikanızı ayırın.</span><span class="sxs-lookup"><span data-stu-id="adf6b-331">Take a moment to read through the code comments.</span></span> <span data-ttu-id="adf6b-332">Bu kodu kullanır **LocalContext** bileşenleri geliştirme ortamını ve bunu çalıştırmak için yerel sürücü üzerindeki metin dosyaları için bileşenler arasındaki veri akışını devam ettirir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-332">This code uses **LocalContext** to run the components in the development environment, and it persists the data stream between components to text files on the local drive.</span></span>

1. <span data-ttu-id="adf6b-333">Açık **Program.cs**ve aşağıdakileri ekleyin **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="adf6b-333">Open **Program.cs**, and add the following to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize the runtime
    SCPRuntime.Initialize();

    //If we are not running under the local context, throw an error
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

2. <span data-ttu-id="adf6b-334">Değişiklikleri kaydetmek ve ardından **F5** veya seçin **hata ayıklama** > **hata ayıklamayı Başlat** projeyi başlatın.</span><span class="sxs-lookup"><span data-stu-id="adf6b-334">Save the changes, and then click **F5** or select **Debug** > **Start Debugging** to start the project.</span></span> <span data-ttu-id="adf6b-335">Bir konsol penceresi görünür ve günlük testleri ilerleme durumunun gerekir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-335">A console window should appear, and log status as the tests progress.</span></span> <span data-ttu-id="adf6b-336">Zaman **testleri tamamlandı** görünür, pencereyi kapatmak için herhangi bir tuşa basın.</span><span class="sxs-lookup"><span data-stu-id="adf6b-336">When **Tests finished** appears, press any key to close the window.</span></span>

3. <span data-ttu-id="adf6b-337">Kullanım **Windows Explorer** projenizi içeren dizini bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="adf6b-337">Use **Windows Explorer** to locate the directory that contains your project.</span></span> <span data-ttu-id="adf6b-338">Örneğin: **C:\Users\<your_user_name > \Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-338">For example: **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span></span> <span data-ttu-id="adf6b-339">Bu dizinde açmak **Bin**ve ardından **hata ayıklama**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-339">In this directory, open **Bin**, and then click **Debug**.</span></span> <span data-ttu-id="adf6b-340">Testleri çalıştırdığınızda üretilmiş olan metin dosyaları görmeniz gerekir: sentences.txt, counter.txt ve splitter.txt.</span><span class="sxs-lookup"><span data-stu-id="adf6b-340">You should see the text files that were produced when the tests ran: sentences.txt, counter.txt, and splitter.txt.</span></span> <span data-ttu-id="adf6b-341">Her metin dosyasını açın ve verileri inceleyin.</span><span class="sxs-lookup"><span data-stu-id="adf6b-341">Open each text file and inspect the data.</span></span>

   > [!NOTE]
   > <span data-ttu-id="adf6b-342">Dize verilerini bu dosyalardaki ondalık değerleri dizisi olarak devam ettirir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-342">String data persists as an array of decimal values in these files.</span></span> <span data-ttu-id="adf6b-343">Örneğin, \[[97,103,111]] içinde **splitter.txt** dosyasıdır word *ve*.</span><span class="sxs-lookup"><span data-stu-id="adf6b-343">For example, \[[97,103,111]] in the **splitter.txt** file is the word *and*.</span></span>

> [!NOTE]
> <span data-ttu-id="adf6b-344">Ayarladığınızdan emin olun **proje türü** başa **sınıf kitaplığı** Hdınsight kümesinde bir Storm dağıtmadan önce.</span><span class="sxs-lookup"><span data-stu-id="adf6b-344">Be sure to set the **Project type** back to **Class Library** before deploying to a Storm on HDInsight cluster.</span></span>

### <a name="log-information"></a><span data-ttu-id="adf6b-345">Günlük bilgileri</span><span class="sxs-lookup"><span data-stu-id="adf6b-345">Log information</span></span>

<span data-ttu-id="adf6b-346">Kolayca bilgi topoloji bileşenlerinizi kullanarak oturum `Context.Logger`.</span><span class="sxs-lookup"><span data-stu-id="adf6b-346">You can easily log information from your topology components by using `Context.Logger`.</span></span> <span data-ttu-id="adf6b-347">Örneğin, aşağıdaki bilgilendirici günlük girişi oluşturur:</span><span class="sxs-lookup"><span data-stu-id="adf6b-347">For example, the following creates an informational log entry:</span></span>

```csharp
Context.Logger.Info("Component started");
```

<span data-ttu-id="adf6b-348">Günlüğe kaydedilen bilgileri alanından görüntülenebilir **Hadoop hizmeti günlüğünü**, içinde bulunan **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-348">Logged information can be viewed from the **Hadoop Service Log**, which is found in **Server Explorer**.</span></span> <span data-ttu-id="adf6b-349">Hdınsight kümesi üzerinde Storm'a giriş'i genişletin ve ardından genişletin **Hadoop hizmeti günlüğünü**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-349">Expand the entry for your Storm on HDInsight cluster, and then expand **Hadoop Service Log**.</span></span> <span data-ttu-id="adf6b-350">Son olarak, günlük dosyasını görüntülemek için seçin.</span><span class="sxs-lookup"><span data-stu-id="adf6b-350">Finally, select the log file to view.</span></span>

> [!NOTE]
> <span data-ttu-id="adf6b-351">Günlükler, küme tarafından kullanılan Azure depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="adf6b-351">The logs are stored in the Azure storage account that is used by your cluster.</span></span> <span data-ttu-id="adf6b-352">Visual Studio'da günlükleri görüntülemek için depolama hesabı sahibi Azure aboneliği ile oturum gerekir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-352">To view the logs in Visual Studio, you must sign in to the Azure subscription that owns the storage account.</span></span>

### <a name="view-error-information"></a><span data-ttu-id="adf6b-353">Hata bilgilerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="adf6b-353">View error information</span></span>

<span data-ttu-id="adf6b-354">Çalışan bir topoloji oluşan hataları görüntülemek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="adf6b-354">To view errors that have occurred in a running topology, use the following steps:</span></span>

1. <span data-ttu-id="adf6b-355">Gelen **Sunucu Gezgini**, Hdınsight kümesinde Storm sağ tıklatın ve seçin **görünüm Storm topolojilerini**.</span><span class="sxs-lookup"><span data-stu-id="adf6b-355">From **Server Explorer**, right-click the Storm on HDInsight cluster, and select **View Storm topologies**.</span></span>

2. <span data-ttu-id="adf6b-356">İçin **Spout** ve **Cıvatalar**, **son hata** sütun son hata hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="adf6b-356">For the **Spout** and **Bolts**, the **Last Error** column contains information on the last error.</span></span>

3. <span data-ttu-id="adf6b-357">Seçin **Spout kimliği** veya **Cıvata kimliği** listelenen hatalı bileşeni için.</span><span class="sxs-lookup"><span data-stu-id="adf6b-357">Select the **Spout Id** or **Bolt Id** for the component that has an error listed.</span></span> <span data-ttu-id="adf6b-358">Ayrıntıları sayfasında görüntülenen, ek hata bilgileri listede **hataları** sayfanın alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="adf6b-358">On the details page that is displayed, additional error information is listed in the **Errors** section at the bottom of the page.</span></span>

4. <span data-ttu-id="adf6b-359">Daha fazla bilgi edinmek için seçin bir **bağlantı noktası** gelen **yürütücüler** Storm çalışan günlük için son birkaç dakikada görmek için bu sayfasının bölümünde.</span><span class="sxs-lookup"><span data-stu-id="adf6b-359">To obtain more information, select a **Port** from the **Executors** section of the page, to see the Storm worker log for the last few minutes.</span></span>

### <a name="errors-submitting-topologies"></a><span data-ttu-id="adf6b-360">Topolojileri gönderme hataları</span><span class="sxs-lookup"><span data-stu-id="adf6b-360">Errors submitting topologies</span></span>

<span data-ttu-id="adf6b-361">Bir topolojiyi hdınsight'a gönderilirken hatalarla karşılaşırsanız, Hdınsight kümenize topoloji gönderimini işlemek sunucu tarafı bileşenleri için günlükleri bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="adf6b-361">If you encounter errors submitting a topology to HDInsight, you can find logs for the server-side components that handle topology submission on your HDInsight cluster.</span></span> <span data-ttu-id="adf6b-362">Bu günlükler almak için bir komut satırından aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="adf6b-362">To retrieve these logs, use the following command from a command line:</span></span>

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

<span data-ttu-id="adf6b-363">Değiştir __sshuser__ küme için SSH kullanıcı hesabıyla.</span><span class="sxs-lookup"><span data-stu-id="adf6b-363">Replace __sshuser__ with the SSH user account for the cluster.</span></span> <span data-ttu-id="adf6b-364">Değiştir __clustername__ Hdınsight kümesi adı.</span><span class="sxs-lookup"><span data-stu-id="adf6b-364">Replace __clustername__ with the name of the HDInsight cluster.</span></span> <span data-ttu-id="adf6b-365">Kullanma hakkında daha fazla bilgi için `scp` ve `ssh` Hdınsight ile bkz [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="adf6b-365">For more information on using `scp` and `ssh` with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="adf6b-366">Gönderimleri birden çok nedenlerden dolayı başarısız olabilir:</span><span class="sxs-lookup"><span data-stu-id="adf6b-366">Submissions can fail for multiple reasons:</span></span>

* <span data-ttu-id="adf6b-367">JDK yüklü değil veya yolu değil.</span><span class="sxs-lookup"><span data-stu-id="adf6b-367">JDK is not installed or is not in the path.</span></span>
* <span data-ttu-id="adf6b-368">Gerekli Java bağımlılıkları gönderisine dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="adf6b-368">Required Java dependencies are not included in the submission.</span></span>
* <span data-ttu-id="adf6b-369">Uyumsuz bağımlılıkları.</span><span class="sxs-lookup"><span data-stu-id="adf6b-369">Incompatible dependencies.</span></span>
* <span data-ttu-id="adf6b-370">Yinelenen topoloji adları.</span><span class="sxs-lookup"><span data-stu-id="adf6b-370">Duplicate topology names.</span></span>

<span data-ttu-id="adf6b-371">Varsa `hdinsight-scpwebapi.out` günlük içeren bir `FileNotFoundException`, bunun aşağıdaki koşullardan nedeni olabilir:</span><span class="sxs-lookup"><span data-stu-id="adf6b-371">If the `hdinsight-scpwebapi.out` log contains a `FileNotFoundException`, this might be caused by the following conditions:</span></span>

* <span data-ttu-id="adf6b-372">JDK geliştirme ortamı yolunda değil.</span><span class="sxs-lookup"><span data-stu-id="adf6b-372">The JDK is not in the path on the development environment.</span></span> <span data-ttu-id="adf6b-373">JDK geliştirme ortamını ve, yüklü olduğunu doğrulayın `%JAVA_HOME%/bin` yolunda olduğundan.</span><span class="sxs-lookup"><span data-stu-id="adf6b-373">Verify that the JDK is installed in the development environment, and that `%JAVA_HOME%/bin` is in the path.</span></span>
* <span data-ttu-id="adf6b-374">Java bağımlılığı eksik.</span><span class="sxs-lookup"><span data-stu-id="adf6b-374">You are missing a Java dependency.</span></span> <span data-ttu-id="adf6b-375">Tüm gerekli .jar dosyalar gönderim bir parçası olarak dahil emin olun.</span><span class="sxs-lookup"><span data-stu-id="adf6b-375">Make sure you are including any required .jar files as part of the submission.</span></span>

## <a name="next-steps"></a><span data-ttu-id="adf6b-376">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="adf6b-376">Next steps</span></span>

<span data-ttu-id="adf6b-377">Bir örnek veriler işlenirken için Event hubs, bkz: [işlem Hdınsight üzerinde Storm ile Azure Event Hubs olaylarından](hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="adf6b-377">For an example of processing data from Event Hubs, see [Process events from Azure Event Hubs with Storm on HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span>

<span data-ttu-id="adf6b-378">Veri akışı birden çok akışlara böler bir C# topolojisi örneği için bkz: [C# Storm örnek](https://github.com/Blackmist/csharp-storm-example).</span><span class="sxs-lookup"><span data-stu-id="adf6b-378">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span></span>

<span data-ttu-id="adf6b-379">C# topolojileri oluşturma hakkında daha fazla bilgi bulmak için bkz: [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span><span class="sxs-lookup"><span data-stu-id="adf6b-379">To discover more information about creating C# topologies, see [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span></span>

<span data-ttu-id="adf6b-380">Hdınsight ile çalışmak daha fazla yolunu ve Hdınsight örnekleri üzerinde daha fazla Storm için aşağıdaki belgelere bakın:</span><span class="sxs-lookup"><span data-stu-id="adf6b-380">For more ways to work with HDInsight and more Storm on HDInsight samples, see the following documents:</span></span>

<span data-ttu-id="adf6b-381">**Microsoft SCP.NET**</span><span class="sxs-lookup"><span data-stu-id="adf6b-381">**Microsoft SCP.NET**</span></span>

* [<span data-ttu-id="adf6b-382">SCP Programlama Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="adf6b-382">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)

<span data-ttu-id="adf6b-383">**Hdınsight üzerinde Apache Storm**</span><span class="sxs-lookup"><span data-stu-id="adf6b-383">**Apache Storm on HDInsight**</span></span>

* [<span data-ttu-id="adf6b-384">Dağıtma ve hdınsight'ta Apache Storm topolojileri izleme</span><span class="sxs-lookup"><span data-stu-id="adf6b-384">Deploy and monitor topologies with Apache Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)
* [<span data-ttu-id="adf6b-385">HDInsight üzerinde Storm için örnek topolojiler</span><span class="sxs-lookup"><span data-stu-id="adf6b-385">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

<span data-ttu-id="adf6b-386">**Hdınsight'ta Apache Hadoop**</span><span class="sxs-lookup"><span data-stu-id="adf6b-386">**Apache Hadoop on HDInsight**</span></span>

* [<span data-ttu-id="adf6b-387">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="adf6b-387">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="adf6b-388">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="adf6b-388">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="adf6b-389">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="adf6b-389">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="adf6b-390">**Hdınsight üzerinde Apache HBase**</span><span class="sxs-lookup"><span data-stu-id="adf6b-390">**Apache HBase on HDInsight**</span></span>

* [<span data-ttu-id="adf6b-391">Hdınsight'ta HBase ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="adf6b-391">Getting started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
