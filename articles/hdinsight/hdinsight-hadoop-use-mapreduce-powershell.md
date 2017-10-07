---
title: "aaaUse MapReduce ve Hadoop - Azure Hdınsight ile PowerShell | Microsoft Docs"
description: "Toouse PowerShell tooremotely çalışma şeklini MapReduce işleri Hadoop ile Hdınsight'ta öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21b56d32-1785-4d44-8ae8-94467c12cfba
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 59524f0e8813d4c017f92bccb2e50d4c018acf71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a>PowerShell kullanarak Hdınsight'ta Hadoop ile MapReduce işleri çalıştırma

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Bu belge, Hdınsight kümesinde bir Hadoop bir MapReduce işi Azure PowerShell toorun kullanmaya ilişkin bir örnek sağlar.

## <a id="prereq"></a>Önkoşullar

* **Azure Hdınsight (Hadoop hdınsight) kümesi**

  > [!IMPORTANT]
  > Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Azure PowerShell içeren bir iş istasyonu**.

## <a id="powershell"></a>Azure PowerShell kullanarak bir MapReduce işi çalıştırma

Azure PowerShell sağlar *cmdlet'leri* olanak tanıyacak şekilde çalıştırın tooremotely MapReduce işleri Hdınsight'ta. Dahili olarak, bu çok REST çağrılarını kullanarak gerçekleştirilir[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (Templeton adıysa) Hdınsight kümesi hello üzerinde çalışan.

Merhaba aşağıdaki cmdlet'ler MapReduce işleri uzaktan Hdınsight kümesinde çalıştırılırken kullanılır.

* **Login-AzureRmAccount**: Azure PowerShell kimliğini doğrulayan tooyour Azure aboneliği.

* **AzureRmHDInsightMapReduceJobDefinition yeni**: yeni bir *iş tanımı* hello kullanarak belirtilen MapReduce bilgi.

* **Başlangıç AzureRmHDInsightJob**: hello iş tanımı tooHDInsight gönderir, hello işini başlatır ve döndürür bir *iş* kullanılan toocheck hello hello işinin durumunu olabilir nesnesi.

* **Bekleme AzureRmHDInsightJob**: hello iş nesnesi toocheck hello hello işinin durumunu kullanır. Merhaba işi tamamlar veya hello bekleme süresi aşılırsa kadar bekler.

* **Get-AzureRmHDInsightJobOutput**: tooretrieve hello çıktısını hello kullanılır.

Merhaba aşağıdaki adımları göstermek nasıl toouse bu cmdlet'leri toorun Hdınsight kümenizdeki bir işi.

1. Bir düzenleyici kullanarak Kaydet kodu olarak aşağıdaki hello **mapreducejob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. Yeni bir **Azure PowerShell** komut istemi. Dizinleri toohello hello konumunu değiştirme **mapreducejob.ps1** dosya sonra toorun hello komut aşağıdaki hello kullanın:

        .\mapreducejob.ps1

    Merhaba komut çalıştırdığınızda hello hello Hdınsight küme adını ve hello HTTPS/Yönetici hesap adı ve parola hello kümesi için istenir. İstendiğinde tooauthenticate tooyour Azure aboneliği de olabilir.

3. Merhaba işi tamamlandığında, çıkış benzer toohello metin aşağıdaki alırsınız:

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    Bu çıktı, o hello işi başarıyla tamamlandı gösterir.

    > [!NOTE]
    > Merhaba, **ExitCode** bir değer 0'dan bkz [sorun giderme](#troubleshooting).

    Bu örnek ayrıca hello indirilen dosyaları tooan depolar **çýktý.txt** hello dizinindeki hello komut dosyasından çalıştırın.

### <a name="view-output"></a>Görünüm çıktı

Açık hello **çýktý.txt** bir metin düzenleyicisi toosee hello dosyasında sözcükleri ve hello iş tarafından üretilen sayar.

> [!NOTE]
> Merhaba çıktı dosyalarını bir MapReduce işi değişmez. Bu nedenle, bu örnek çalıştırırsanız, toochange hello hello çıktı dosyası adını gerekir.

## <a id="troubleshooting"></a>Sorun giderme

Merhaba işi tamamlandığında hiçbir bilgi döndürülürse, işleme sırasında bir hata oluşmuş olabilir. Bu iş için tooview hata bilgilerini Ekle komutu toohello hello sonuna aşağıdaki hello **mapreducejob.ps1** dosya, dosyayı kaydedin ve yeniden çalıştırın.

```powershell
# Print hello output of hello WordCount job.
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

Bu cmdlet hello işi çalıştırdığınızda, tooSTDERR hello sunucuda yazıldı hello bilgiler döndürür ve hello iş neden başarısız olduğunu belirlemenize yardımcı.

## <a id="summary"></a>Özet

Gördüğünüz gibi bir Hdınsight kümesi, hello iş durumunu izleyin ve alma hello çıktı Azure PowerShell kolay bir yolu toorun MapReduce işleri sağlar.

## <a id="nextsteps"></a>Sonraki adımlar

Hdınsight'ta MapReduce işleri hakkında genel bilgi için:

* [Hdınsight Hadoop MapReduce kullanın](hdinsight-use-mapreduce.md)

Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:

* [Hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md)
* [Hdınsight'ta Hadoop ile pig kullanma](hdinsight-use-pig.md)
