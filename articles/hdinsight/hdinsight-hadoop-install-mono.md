---
title: "aaaInstall veya hdınsight'ta - Azure Mono güncelleştirme | Microsoft Docs"
description: "Bilgi nasıl toouse Mono belirli bir sürümü Hdınsight kümesi ile. Mono Linux tabanlı Hdınsight kümelerinde kullanılan toorun .NET uygulamaları ' dir."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: hdinsightactive
ms.openlocfilehash: 1e8a8aaeff231c93a9e232379448517b326da965
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a><span data-ttu-id="06fbf-104">Yükleme veya Mono hdınsight'ta güncelleştir</span><span class="sxs-lookup"><span data-stu-id="06fbf-104">Install or update Mono on HDInsight</span></span>

<span data-ttu-id="06fbf-105">Bilgi nasıl tooinstall belirli bir sürümü, [Mono](https://www.mono-project.com) Hdınsight 3.4 veya daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="06fbf-105">Learn how tooinstall a specific version of [Mono](https://www.mono-project.com) on HDInsight 3.4 or higher.</span></span>

<span data-ttu-id="06fbf-106">Mono Hdınsight 3.4 ve daha yüksek yüklü ve kullanılan toorun .NET uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="06fbf-106">Mono is installed on HDInsight 3.4 and higher, and is used toorun .NET applications.</span></span> <span data-ttu-id="06fbf-107">Her Hdınsight sürümü ile birlikte verilen Mono hello sürümü hakkında daha fazla bilgi için bkz: [Hdınsight bileşen sürümü oluşturma](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="06fbf-107">For information on hello version of Mono included with each HDInsight version, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="06fbf-108">tooinstall kullanım hello betik eylemi bu belgedeki kümenizdeki farklı bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="06fbf-108">tooinstall a different version on your cluster, use hello script action in this document.</span></span> 

## <a name="how-it-works"></a><span data-ttu-id="06fbf-109">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="06fbf-109">How it works</span></span>

<span data-ttu-id="06fbf-110">Bu komut dosyası parametresi aşağıdaki hello kabul eder:</span><span class="sxs-lookup"><span data-stu-id="06fbf-110">This script accepts hello following parameter:</span></span>

* <span data-ttu-id="06fbf-111">__Mono sürüm numarası__: Mono tooinstall hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="06fbf-111">__Mono version number__: hello version of Mono tooinstall.</span></span> <span data-ttu-id="06fbf-112">Merhaba sürümü kullanılabilir olmalıdır [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span><span class="sxs-lookup"><span data-stu-id="06fbf-112">hello version must be available from [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span></span>

<span data-ttu-id="06fbf-113">Merhaba betik Mono paketleri aşağıdaki hello yükler:</span><span class="sxs-lookup"><span data-stu-id="06fbf-113">hello script installs hello following Mono packages:</span></span>

* <span data-ttu-id="06fbf-114">__Mono tamamlayın__</span><span class="sxs-lookup"><span data-stu-id="06fbf-114">__mono-complete__</span></span>

* <span data-ttu-id="06fbf-115">__CA sertifikaları mono__</span><span class="sxs-lookup"><span data-stu-id="06fbf-115">__ca-certificates-mono__</span></span>

## <a name="hello-script"></a><span data-ttu-id="06fbf-116">Merhaba komut dosyası</span><span class="sxs-lookup"><span data-stu-id="06fbf-116">hello script</span></span>

<span data-ttu-id="06fbf-117">__Komut dosyası konumu__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span><span class="sxs-lookup"><span data-stu-id="06fbf-117">__Script location__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span></span>

<span data-ttu-id="06fbf-118">__Gereksinimleri__:</span><span class="sxs-lookup"><span data-stu-id="06fbf-118">__Requirements__:</span></span>

* <span data-ttu-id="06fbf-119">Merhaba üzerinde Hello betik uygulanan __baş düğümler__ ve __çalışan düğümleri__.</span><span class="sxs-lookup"><span data-stu-id="06fbf-119">hello script must be applied on hello __head nodes__ and __worker nodes__.</span></span>

## <a name="toouse-hello-script"></a><span data-ttu-id="06fbf-120">toouse hello komut dosyası</span><span class="sxs-lookup"><span data-stu-id="06fbf-120">toouse hello script</span></span>

<span data-ttu-id="06fbf-121">Bu komut dosyası, Hdınsight ile toouse nasıl görürüm bilgi hello [özelleştirme Linux tabanlı Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) belge.</span><span class="sxs-lookup"><span data-stu-id="06fbf-121">For information on how toouse this script with HDInsight, see hello [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span> <span data-ttu-id="06fbf-122">Merhaba betik hello Azure portal, Azure PowerShell aracılığıyla veya Azure CLI hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06fbf-122">You can use hello script through hello Azure portal, Azure PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="06fbf-123">Aşağıdaki betik eylemi belge hello yaparken, URI aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="06fbf-123">While following hello script action document, use hello following URI:</span></span>

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> <span data-ttu-id="06fbf-124">Hdınsight ile bu komut dosyası yapılandırırken hello komut dosyası olarak işaretlemek __kalıcı__.</span><span class="sxs-lookup"><span data-stu-id="06fbf-124">When configuring HDInsight with this script, mark hello script as __Persisted__.</span></span> <span data-ttu-id="06fbf-125">Bu ayar Hdınsight tooapply operations ölçeklendirme aracılığıyla eklenen hello betik tooworker düğümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="06fbf-125">This setting allows HDInsight tooapply hello script tooworker nodes added through scaling operations.</span></span>


## <a name="next-steps"></a><span data-ttu-id="06fbf-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="06fbf-126">Next steps</span></span>

<span data-ttu-id="06fbf-127">Öğrendiğiniz nasıl tooupgrade veya Hdınsight'ta Mono belirli bir sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="06fbf-127">You have learned how tooupgrade or install a specific version of Mono on HDInsight.</span></span> <span data-ttu-id="06fbf-128">Mono hdınsight'ta .NET uygulamalarını kullanarak daha fazla bilgi için aşağıdaki belgeleri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="06fbf-128">For more information on using .NET applications with Mono on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="06fbf-129">Hdınsight üzerinde MapReduce akış için .NET kullanın</span><span class="sxs-lookup"><span data-stu-id="06fbf-129">Use .NET for streaming MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [<span data-ttu-id="06fbf-130">Hive veya Pig hdınsight'ta ile .NET kullanın</span><span class="sxs-lookup"><span data-stu-id="06fbf-130">Use .NET with Hive and Pig on HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [<span data-ttu-id="06fbf-131">C# hdınsight'ta Storm çözümleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="06fbf-131">Develop C# solutions with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="06fbf-132">.NET çözümleri geçirmek tooLinux tabanlı Hdınsight</span><span class="sxs-lookup"><span data-stu-id="06fbf-132">Migrate .NET solutions tooLinux-based HDInsight</span></span>](hdinsight-hadoop-migrate-dotnet-to-linux.md)

<span data-ttu-id="06fbf-133">Betik eylemleri kullanma hakkında daha fazla bilgi için bkz: [özelleştirme Linux tabanlı Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="06fbf-133">For more information on using script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>