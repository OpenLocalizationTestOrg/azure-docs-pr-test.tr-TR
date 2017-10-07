---
title: "aaaUse Hadoop Hive hdınsight'ta - Azure PowerShell ile | Microsoft Docs"
description: "Hdınsight'ta Hadoop PowerShell toorun Hive sorguları kullanın."
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
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 9e0b72a25c5b12431f837b1a34a63ecc06223528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-powershell"></a>PowerShell kullanarak Hive sorguları çalıştırma
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Bu belge hello Azure kaynak grubu modu toorun Hive sorguları Hdınsight kümesinde bir Hadoop Azure PowerShell kullanarak bir örnek sağlar.

> [!NOTE]
> Bu belgede ayrıntılı açıklamasını hello örneklerde kullanılan hello HiveQL ifadelerini ne sağlamaz. Bu örnekte kullanılan HiveQL hello hakkında daha fazla bilgi için bkz: [hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md).

**Önkoşullar**

* **Azure Hdınsight kümesi**: Windows hello kümedir önemi değil veya Linux tabanlı.

  > [!IMPORTANT]
  > Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Azure PowerShell içeren bir iş istasyonu**.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a>Azure PowerShell kullanarak Hive sorguları çalıştırma

Azure PowerShell sağlar *cmdlet'leri* olanak tanıyacak şekilde çalıştırın tooremotely Hive sorguları Hdınsight'ta. Dahili olarak, hello cmdlet'leri REST çok aramalarda[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) hello Hdınsight kümesi üzerinde.

Merhaba aşağıdaki cmdlet'leri Hive sorguları bir uzak Hdınsight kümesinde çalıştırılırken kullanılır:

* **Add-AzureRmAccount**: Azure PowerShell kimliğini doğrulayan tooyour Azure aboneliği
* **AzureRmHDInsightHiveJobDefinition yeni**: oluşturur bir *iş tanımı* hello kullanılarak HiveQL ifadelerini belirtilen
* **Başlangıç AzureRmHDInsightJob**: hello iş tanımı tooHDInsight gönderir, hello işini başlatır ve döndürür bir *iş* kullanılan toocheck hello hello işinin durumunu olabilir nesnesi
* **Bekleme AzureRmHDInsightJob**: hello iş nesnesi toocheck hello hello işinin durumunu kullanır. Merhaba işi tamamlar veya hello bekleme süresi aşılırsa kadar bekler.
* **Get-AzureRmHDInsightJobOutput**: tooretrieve hello çıktısını hello kullanılan
* **Çağırma AzureRmHDInsightHiveJob**: toorun HiveQL ifadelerini kullanılır. Bu cmdlet blokları hello sorgu tamamlandıktan sonra hello sonuçlar döndürür
* **Kullanım AzureRmHDInsightCluster**: kümeleri hello hello için geçerli küme toouse **Invoke-AzureRmHDInsightHiveJob** komutu

Merhaba aşağıdaki adımları göstermek nasıl toouse bu cmdlet'leri toorun Hdınsight kümenize işinde:

1. Bir düzenleyici kullanarak Kaydet kodu olarak aşağıdaki hello **hivejob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. Yeni bir **Azure PowerShell** komut istemi. Dizinleri toohello hello konumunu değiştirme **hivejob.ps1** dosya sonra toorun hello komut aşağıdaki hello kullanın:

        .\hivejob.ps1

    Merhaba komut dosyası çalıştığında, istendiğinde tooenter hello küme adını ve hello HTTPS/yönetici hesabı kimlik bilgilerini hello küme demektir. İstendiğinde toolog tooyour Azure aboneliği içindeki de olabilir.

3. Merhaba işi tamamlandığında thext aşağıdaki bilgileri benzer toohello döndürür:

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. Daha önce belirtildiği gibi **Invoke-Hive** sorguda kullanılan toorun kullanılabilir ve hello yanıtı bekleyin. Invoke-Hive nasıl çalıştığını betik toosee aşağıdaki hello kullan:

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    Merhaba çıktı hello metin aşağıdaki gibi görünür:

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > Uzun HiveQL sorgularında hello Azure PowerShell kullanabilirsiniz **burada dizeleri** cmdlet veya HiveQL komut dosyaları. kod parçacığında gösterildiği nasıl aşağıdaki hello toouse hello **Invoke-Hive** cmdlet toorun HiveQL komut dosyası. Merhaba komut dosyası olmalıdır HiveQL karşıya toowasb: / /.
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > Hakkında daha fazla bilgi için **burada dizeleri**, bkz: <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">kullanarak Windows PowerShell burada-dizeleri</a>.

## <a name="troubleshooting"></a>Sorun giderme

Merhaba işi tamamlandığında hiçbir bilgi döndürülürse, işleme sırasında bir hata oluşmuş olabilir. Bu iş için tooview hata bilgilerini ekleyin hello toohello sonuna aşağıdaki hello **hivejob.ps1** dosya, dosyayı kaydedin ve yeniden çalıştırın.

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

Bu cmdlet hello iş çalıştırdığınızda tooSTDERR hello sunucusuna yazılır hello bilgileri döndürür.

## <a name="summary"></a>Özet

Gördüğünüz gibi Azure PowerShell kolay bir yolu toorun bir Hdınsight kümesindeki Hive sorguları sağlar, İzleyicisi Merhaba durumu iş ve hello çıkış almak.

## <a name="next-steps"></a>Sonraki adımlar

Hdınsight'ta Hive hakkında genel bilgi için:

* [Hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md)

Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:

* [Hdınsight'ta Hadoop ile pig kullanma](hdinsight-use-pig.md)
* [Hdınsight'ta Hadoop ile MapReduce kullanma](hdinsight-use-mapreduce.md)
