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
# <a name="migrate-net-solutions-for-windows-based-hdinsight-toolinux-based-hdinsight"></a>Windows tabanlı Hdınsight .NET çözümleri geçirmek tooLinux tabanlı Hdınsight

Linux tabanlı Hdınsight kümeleri kullanım [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET uygulamaları. Mono Linux tabanlı Hdınsight ile MapReduce uygulamalar gibi toouse .NET bileşenleri sağlar. Bu belgede, Linux tabanlı Hdınsight üzerinde Mono ile Windows tabanlı Hdınsight kümeleri toowork için toomigrate .NET çözümleri nasıl oluşturulacağını öğrenin.

## <a name="mono-compatibility-with-net"></a>.NET ile Mono uyumluluk

Mono sürüm 4.2.1 Hdınsight sürüm 3.5 ile dahil edilir. Hdınsight ile dahil Mono hello sürümü hakkında daha fazla bilgi için bkz: [Hdınsight bileşen sürümü](hdinsight-component-versioning.md). tooinstall Mono, belirli bir sürümünü görmek hello [yükleme veya güncelleştirme Mono](hdinsight-hadoop-install-mono.md) belge.

Mono ve .NET uyumluluğu hakkında ayrıntılı bilgi için bkz: Merhaba [Mono uyumluluk (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) belge.

> [!IMPORTANT]
> Merhaba SCP.NET framework Mono ile uyumludur. SCP.NET Mono ile kullanma hakkında daha fazla bilgi için bkz: [Hdınsight üzerinde Apache Storm için Visual Studio'yu kullanın toodevelop C# topolojileri](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="automated-portability-analysis"></a>Otomatik taşınabilirlik çözümleme

Merhaba [.NET taşınabilirlik Çözümleyicisi](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) kullanılan toogenerate uygulama Mono arasındaki uyumsuzluklar raporunu olabilir. Aşağıdaki adımları tooconfigure hello Çözümleyicisi toocheck hello uygulamanız için Mono taşınabilirlik kullanın:

1. Merhaba yüklemek [.NET taşınabilirlik Çözümleyicisi](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer). Yükleme sırasında Visual Studio toouse hello sürümünü seçin.

2. Visual Studio 2015'ten seçin __Çözümle__ > __taşınabilirlik Çözümleyicisi ayarları__, emin olun __4.5__ hello denetlenir __Mono__  bölümü.

    ![Mono bölümünde hello Çözümleyicisi ayarları için kontrol 4.5](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    Seçin __Tamam__ toosave hello yapılandırma.

3. Seçin __analiz__ > __derleme taşınabilirlik analiz__. Çözümünüzü içeren hello derleme seçin ve ardından __açık__ toobegin çözümleme.

4. Analiz tamamlandığında seçin __Çözümle__ > __analiz raporları görüntülemek__. İçinde __taşınabilirlik çözümleme sonuçlarını__seçin __raporunu Aç__ tooopen bir rapor.

    ![Taşınabilirlik Çözümleyicisi sonuçları iletişim](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> Merhaba Çözümleyicisi çözümünüzün her sorun catch olamaz. Örneğin, bir dosya yolu `c:\temp\file.txt` Tamam, çünkü Mono Windows üzerinde çalışır ve hello yol bu bağlamda geçerli olarak kabul edilir. Ancak, hello yolu Linux platformu üzerinde geçerli değil.

## <a name="manual-portability-analysis"></a>El ile Taşınabilirlik çözümleme

El ile denetim hello hello bilgileri kullanarak, kodunuzun gerçekleştirmek [uygulama taşınabilirliği (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) belge.

## <a name="modify-and-build"></a>Değiştirme ve oluşturma

Hdınsight için Visual Studio toobuild toouse .NET çözümlerinizi devam edebilirsiniz. Ancak, yapılandırılmış toouse .NET Framework 4.5 hello proje olduğundan emin olmalısınız.

## <a name="deploy-and-test"></a>Dağıtma ve test etme

Merhaba önerileri hello .NET taşınabilirlik Çözümleyicisi veya el ile çözümleme kullanarak çözümünüzü değiştirdiniz. sonra Hdınsight ile test etmeniz gerekir. Linux tabanlı Hdınsight kümesi üzerinde Hello çözüm test ediliyor düzeltildi toobe gereken Zarif sorunlarını olduğunu gösterebilir. Sınama sırasında uygulamanızda ek günlüğü etkinleştirmenizi öneririz.

Günlükleri erişme ile ilgili daha fazla bilgi için aşağıdaki belgeleri hello bakın:

* [Linux tabanlı HDInsight’ta YARN uygulama günlüklerine erişme](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a>Sonraki adımlar

* [C# ile MapReduce hdınsight'ta kullanma](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [C# kullanıcı tanımlı işlevler Hive veya Pig kullanın](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [Hdınsight üzerinde Storm için C# topolojileri geliştirme](hdinsight-storm-develop-csharp-visual-studio-topology.md)