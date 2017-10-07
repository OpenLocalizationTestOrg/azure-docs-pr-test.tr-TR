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
# <a name="install-or-update-mono-on-hdinsight"></a>Yükleme veya Mono hdınsight'ta güncelleştir

Bilgi nasıl tooinstall belirli bir sürümü, [Mono](https://www.mono-project.com) Hdınsight 3.4 veya daha yüksek.

Mono Hdınsight 3.4 ve daha yüksek yüklü ve kullanılan toorun .NET uygulamaları. Her Hdınsight sürümü ile birlikte verilen Mono hello sürümü hakkında daha fazla bilgi için bkz: [Hdınsight bileşen sürümü oluşturma](hdinsight-component-versioning.md). tooinstall kullanım hello betik eylemi bu belgedeki kümenizdeki farklı bir sürüm. 

## <a name="how-it-works"></a>Nasıl çalışır?

Bu komut dosyası parametresi aşağıdaki hello kabul eder:

* __Mono sürüm numarası__: Mono tooinstall hello sürümü. Merhaba sürümü kullanılabilir olmalıdır [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).

Merhaba betik Mono paketleri aşağıdaki hello yükler:

* __Mono tamamlayın__

* __CA sertifikaları mono__

## <a name="hello-script"></a>Merhaba komut dosyası

__Komut dosyası konumu__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)

__Gereksinimleri__:

* Merhaba üzerinde Hello betik uygulanan __baş düğümler__ ve __çalışan düğümleri__.

## <a name="toouse-hello-script"></a>toouse hello komut dosyası

Bu komut dosyası, Hdınsight ile toouse nasıl görürüm bilgi hello [özelleştirme Linux tabanlı Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) belge. Merhaba betik hello Azure portal, Azure PowerShell aracılığıyla veya Azure CLI hello kullanabilirsiniz.

Aşağıdaki betik eylemi belge hello yaparken, URI aşağıdaki hello kullanın:

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> Hdınsight ile bu komut dosyası yapılandırırken hello komut dosyası olarak işaretlemek __kalıcı__. Bu ayar Hdınsight tooapply operations ölçeklendirme aracılığıyla eklenen hello betik tooworker düğümleri sağlar.


## <a name="next-steps"></a>Sonraki adımlar

Öğrendiğiniz nasıl tooupgrade veya Hdınsight'ta Mono belirli bir sürümünü yükleyin. Mono hdınsight'ta .NET uygulamalarını kullanarak daha fazla bilgi için aşağıdaki belgeleri hello bakın:

* [Hdınsight üzerinde MapReduce akış için .NET kullanın](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [Hive veya Pig hdınsight'ta ile .NET kullanın](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [C# hdınsight'ta Storm çözümleri geliştirme](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [.NET çözümleri geçirmek tooLinux tabanlı Hdınsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)

Betik eylemleri kullanma hakkında daha fazla bilgi için bkz: [özelleştirme Linux tabanlı Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md)