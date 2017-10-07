---
title: "aaaGet Azure Data Lake Azure PowerShell kullanarak Analytics ile çalışmaya | Microsoft Docs"
description: "Azure PowerShell toocreate Data Lake Analytics hesabı kullanın, U-SQL'yi kullanarak Data Lake Analytics işi oluşturmak ve hello işi gönderin. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 8a4e901e-9656-4a60-90d0-d78ff2f00656
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: edmaca
ms.openlocfilehash: cb9b35352d1cc9a78337448b1d6835875a212e08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a>Azure PowerShell'i kullanarak Azure Data Lake Analytics ile çalışmaya başlama
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Nasıl toouse Azure PowerShell toocreate Azure Data Lake Analytics hesapları göndermek ve U-SQL işleri çalıştırma öğrenin. Data Lake Analytics hakkında daha fazla bilgi için bkz. [Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md).

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticiye başlamadan önce aşağıdaki bilgilerle hello sahip olmanız gerekir:

* **Azure Data Lake Analytics hesabı**. Bkz. [Data Lake Analytics ile çalışmaya başlama](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).
* **Azure PowerShell içeren bir iş istasyonu**. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

## <a name="log-in-tooazure"></a>İçinde tooAzure oturum

Bu öğreticide, Azure PowerShell kullanımıyla ilgili bilgi sahibi olduğunuz varsayılır. Özellikle, tooknow nasıl gereksinim tooAzure toolog. Merhaba bkz [Azure PowerShell ile çalışmaya başlama](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) yardıma gereksinim duyarsanız.

Abonelik adı oturum toolog:

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

Merhaba abonelik adı yerine bir abonelik kimliği toolog içinde de kullanabilirsiniz:

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

Başarılı olursa, bu komutun çıktısı hello hello metin aşağıdaki gibi görünür:

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-hello-tutorial"></a>Merhaba öğretici için hazırlama

Bu öğreticide Hello PowerShell parçacıkları bu değişkenleri toostore bu bilgileri kullanın:

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a>Bir Data Lake Analytics hesabı hakkında bilgi edinme

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a>U-SQL işi gönderme

Bir PowerShell değişken toohold hello U-SQL betiği oluşturun.

```
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();

"@
```

Merhaba betik gönderin.

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

Alternatif olarak, hello komut dosyası olarak kaydedin ve komut aşağıdaki hello ile gönderin:

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


Belirli bir iş Hello durumunu alın. Hello iş yapılır görene kadar bu cmdlet'i kullanarak tutun.

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

Bir işi tamamlanana kadar Get-AdlAnalyticsJob tekrar tekrar çağırmak yerine, hello bekleme AdlJob cmdlet'ini kullanabilirsiniz.

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

Merhaba çıktı dosyasını indirin.

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a>Ayrıca bkz.
* toosee hello aynı öğreticiyi diğer araçları kullanarak, hello sekmesini seçiciler hello sayfasının hello üstte'ı tıklatın.
* U-SQL, toolearn bkz [Azure Data Lake Analytics U-SQL dili ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md).
* Yönetim görevleri için bkz. [Azure portalı kullanarak Azure Data Lake Analytics'i yönetme](data-lake-analytics-manage-use-portal.md).
