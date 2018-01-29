---
title: "Hdınsight'ta - Azure PowerShell ile Hadoop Hive kullanma | Microsoft Docs"
description: "Hdınsight'ta Hadoop Hive sorguları çalıştırmak için PowerShell kullanın."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cb795b7c-bcd0-497a-a7f0-8ed18ef49195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/27/2017
ms.author: larryfr
ms.openlocfilehash: 95bfab18a6a8a9ad9eb547179a3205ae4b186213
ms.sourcegitcommit: f847fcbf7f89405c1e2d327702cbd3f2399c4bc2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2017
---
# <a name="run-hive-queries-using-powershell"></a>PowerShell kullanarak Hive sorguları çalıştırma
[!INCLUDE [hive-selector](../../../includes/hdinsight-selector-use-hive.md)]

Bu belge, Hdınsight kümesinde bir Hadoop Hive sorguları çalıştırmak için Azure kaynak grubu modunda Azure PowerShell kullanarak bir örnek sağlar.

> [!NOTE]
> Bu belgedeki örneklerde kullanılan HiveQL ifadelerini ne ayrıntılı bir açıklama sağlamaz. Bu örnekte kullanılan HiveQL hakkında daha fazla bilgi için bkz: [hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md).

**Önkoşullar**

* **Azure Hdınsight kümesi**: küme Windows olup olmaması önemli değil ya da Linux tabanlı.

  > [!IMPORTANT]
  > Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](../hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Azure PowerShell içeren bir iş istasyonu**.

[!INCLUDE [upgrade-powershell](../../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a>Azure PowerShell kullanarak Hive sorguları çalıştırma

Azure PowerShell sağlar *cmdlet'leri* uzaktan Hdınsight'ta Hive sorguları çalıştırmanıza izin verir. Dahili olarak, cmdlet'ler REST çağrı yapmak [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) Hdınsight kümesinde.

Aşağıdaki cmdlet, Hive sorguları bir uzak Hdınsight kümesinde çalıştırılırken kullanılır:

* **Add-AzureRmAccount**: Azure PowerShell'i Azure aboneliğinize kimliğini doğrular.
* **AzureRmHDInsightHiveJobDefinition yeni**: oluşturur bir *iş tanımı* belirtilen HiveQL ifadelerini kullanarak.
* **Başlangıç AzureRmHDInsightJob**: iş tanımı için Hdınsight gönderir ve işini başlatır. A *iş* nesne döndürülür.
* **Bekleme AzureRmHDInsightJob**: iş nesnesi işinin durumunu denetlemek için kullanır. İş tamamlandığında veya bekleme süresi aşılırsa kadar bekler.
* **Get-AzureRmHDInsightJobOutput**: işlemin çıktısını almak için kullanılır.
* **Çağırma AzureRmHDInsightHiveJob**: HiveQL ifadelerini çalıştırmak için kullanılır. Bu cmdlet blokları sorgu tamamlandıktan sonra sonuçları döndürür.
* **Kullanım AzureRmHDInsightCluster**: için kullanılacak geçerli küme ayarlar **Invoke-AzureRmHDInsightHiveJob** komutu.

Aşağıdaki adımlarda, bu cmdlet'ler, Hdınsight kümesinde bir işi çalıştırmak için nasıl kullanılacağı gösterilmektedir:

1. Bir düzenleyici kullanarak aşağıdaki kodu olarak Kaydet **hivejob.ps1**.

    [!code-powershell[main](../../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. Yeni bir **Azure PowerShell** komut istemi. Dizin konumuna değiştirme **hivejob.ps1** dosya sonra komut dosyasını çalıştırmak için aşağıdaki komutu kullanın:

        .\hivejob.ps1

    Komut dosyası çalıştığında, küme için küme adı ve HTTPS/yönetici hesabı kimlik bilgileri girmeniz istenir. Ayrıca Azure aboneliğinizde oturum istenebilir.

3. İş tamamlandığında, bilgileri aşağıdaki metni benzer döndürür:

        Display the standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. Daha önce belirtildiği gibi **Invoke-Hive** bir sorgu çalıştırın ve yanıt için beklemek için kullanılabilir. Invoke-Hive nasıl çalıştığını görmek için aşağıdaki komut dosyasını kullanın:

    [!code-powershell[main](../../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    Çıktı aşağıdaki metni gibi görünür:

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > Uzun HiveQL sorgular için Azure PowerShell'i kullanabilirsiniz **burada dizeleri** cmdlet veya HiveQL komut dosyaları. Aşağıdaki kod parçacığını nasıl kullanılacağını gösterir **Invoke-Hive** cmdlet'ini HiveQL komut dosyasını çalıştırın. HiveQL komut dosyası için wasb yüklenmelidir: / /.
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > Hakkında daha fazla bilgi için **burada dizeleri**, bkz: <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">kullanarak Windows PowerShell burada-dizeleri</a>.

## <a name="troubleshooting"></a>Sorun giderme

İş tamamlandığında hiçbir bilgi döndürülürse, hata günlüklerine bakın. Bu işi için hata bilgilerini görüntülemek için aşağıdaki sonuna ekleyin **hivejob.ps1** dosya, dosyayı kaydedin ve yeniden çalıştırın.

```powershell
# Print the output of the Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

Bu cmdlet STDERR iş işleme sırasında yazılır bilgiler döndürür.

## <a name="summary"></a>Özet

Gördüğünüz gibi Azure PowerShell bir Hdınsight kümesi Hive sorgularını çalıştırma, iş durumunu izleyebilir ve çıkış almak için kolay bir yol sağlar.

## <a name="next-steps"></a>Sonraki adımlar

Hdınsight'ta Hive hakkında genel bilgi için:

* [Hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md)

Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:

* [Hdınsight'ta Hadoop ile pig kullanma](hdinsight-use-pig.md)
* [Hdınsight'ta Hadoop ile MapReduce kullanma](hdinsight-use-mapreduce.md)
