---
title: "aaaUse Hadoop Pig hdınsight'ta - Azure PowerShell ile | Microsoft Docs"
description: "Nasıl toosubmit Pig işleri tooa Hadoop küme Azure PowerShell kullanarak Hdınsight'ta öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 737089c1-b494-4387-9def-7b4dac3be532
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 771617df203011eaec715a0dba6f5014a42877f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toorun-pig-jobs-with-hdinsight"></a>Hdınsight ile Azure PowerShell toorun Pig işleri kullanma

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Bu belge, Azure PowerShell toosubmit Pig işleri tooa Hadoop Hdınsight kümesinde kullanmaya ilişkin bir örnek sağlar. Pig veri dönüşümleri modeller bir dili (Pig Latin) kullanılarak toowrite MapReduce işleri verir yerine harita ve işlevleri azaltır.

> [!NOTE]
> Bu belgede ayrıntılı açıklamasını hello örneklerde kullanılan hello Pig Latin ifadeleri ne sağlamaz. Bu örnekte kullanılan Pig Latin hello hakkında daha fazla bilgi için bkz: [hdınsight'ta Hadoop ile Pig kullanma](hdinsight-use-pig.md).

## <a id="prereq"></a>Önkoşullar

* **Azure Hdınsight kümesi**

  > [!IMPORTANT]
  > Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Azure PowerShell içeren bir iş istasyonu**.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a id="powershell"></a>PowerShell kullanarak Pig işleri çalıştırma

Azure PowerShell sağlar *cmdlet'leri* olanak tanıyacak şekilde çalıştırın tooremotely Pig işleri Hdınsight'ta. Dahili olarak, PowerShell REST çağrılarını çok kullanır[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) hello Hdınsight kümesinde çalışan.

Merhaba aşağıdaki cmdlet'leri uzak bir Hdınsight kümesine Pig işleri çalıştırma sırasında kullanılır:

* **Login-AzureRmAccount**: Azure PowerShell kimliğini doğrulayan tooyour Azure aboneliği
* **AzureRmHDInsightPigJobDefinition yeni**: oluşturur bir *iş tanımı* hello kullanarak belirtilen Pig Latin deyimleri
* **Başlangıç AzureRmHDInsightJob**: hello iş tanımı tooHDInsight gönderir, hello işini başlatır ve döndürür bir *iş* kullanılan toocheck hello hello işinin durumunu olabilir nesnesi
* **Bekleme AzureRmHDInsightJob**: hello iş nesnesi toocheck hello hello işinin durumunu kullanır. Merhaba işi tamamlandı veya hello bekleme zamanı aşıldı kadar bekler.
* **Get-AzureRmHDInsightJobOutput**: tooretrieve hello çıktısını hello kullanılan

Merhaba aşağıdaki adımları göstermek nasıl toouse bu cmdlet'leri toorun, Hdınsight kümesinde bir işi.

1. Bir düzenleyici kullanarak Kaydet kodu olarak aşağıdaki hello **pigjob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. Yeni bir Windows PowerShell komut istemi açın. Dizinleri toohello hello konumunu değiştirme **pigjob.ps1** dosya sonra toorun hello komut aşağıdaki hello kullanın:

        .\pigjob.ps1

    İstendiğinde toolog tooyour Azure aboneliği içindeki var. Ardından, hello HTTPs/Yönetici hesap adı ve parola hello Hdınsight kümesi için istenir.

2. Merhaba işi tamamlandığında, metin aşağıdaki bilgileri benzer toohello döndürmesi gerekir:

        Start hello Pig job ...
        Wait for hello Pig job toocomplete ...
        Display hello standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="troubleshooting"></a>Sorun giderme

Merhaba işi tamamlandığında hiçbir bilgi döndürülürse, işleme sırasında bir hata oluşmuş olabilir. Bu iş için tooview hata bilgilerini Ekle komutu toohello hello sonuna aşağıdaki hello **pigjob.ps1** dosya, dosyayı kaydedin ve yeniden çalıştırın.

    # Print hello output of hello Pig job.
    Write-Host "Display hello standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

Bu hello iş çalıştırdığınızda tooSTDERR hello sunucuda yazıldı hello bilgileri döndürür ve hello iş neden başarısız olduğunu belirlemenize yardımcı.

## <a id="summary"></a>Özet
Gördüğünüz gibi bir Hdınsight kümesi, hello iş durumunu izleyin ve alma hello çıktı Azure PowerShell kolay bir yolu toorun Pig işleri sağlar.

## <a id="nextsteps"></a>Sonraki adımlar
Hdınsight'ta Pig hakkında genel bilgi için:

* [Hdınsight'ta Hadoop ile pig kullanma](hdinsight-use-pig.md)

Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:

* [Hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md)
* [Hdınsight'ta Hadoop ile MapReduce kullanma](hdinsight-use-mapreduce.md)
