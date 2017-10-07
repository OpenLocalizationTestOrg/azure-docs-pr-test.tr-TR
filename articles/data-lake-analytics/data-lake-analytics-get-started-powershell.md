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
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="d48c7-103">Azure PowerShell'i kullanarak Azure Data Lake Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d48c7-103">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="d48c7-104">Nasıl toouse Azure PowerShell toocreate Azure Data Lake Analytics hesapları göndermek ve U-SQL işleri çalıştırma öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d48c7-104">Learn how toouse Azure PowerShell toocreate Azure Data Lake Analytics accounts and then submit and run U-SQL jobs.</span></span> <span data-ttu-id="d48c7-105">Data Lake Analytics hakkında daha fazla bilgi için bkz. [Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d48c7-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d48c7-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d48c7-106">Prerequisites</span></span>

<span data-ttu-id="d48c7-107">Bu öğreticiye başlamadan önce aşağıdaki bilgilerle hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d48c7-107">Before you begin this tutorial, you must have hello following information:</span></span>

* <span data-ttu-id="d48c7-108">**Azure Data Lake Analytics hesabı**.</span><span class="sxs-lookup"><span data-stu-id="d48c7-108">**An Azure Data Lake Analytics account**.</span></span> <span data-ttu-id="d48c7-109">Bkz. [Data Lake Analytics ile çalışmaya başlama](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="d48c7-109">See [Get started with Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span></span>
* <span data-ttu-id="d48c7-110">**Azure PowerShell içeren bir iş istasyonu**.</span><span class="sxs-lookup"><span data-stu-id="d48c7-110">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="d48c7-111">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d48c7-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="d48c7-112">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="d48c7-112">Log in tooAzure</span></span>

<span data-ttu-id="d48c7-113">Bu öğreticide, Azure PowerShell kullanımıyla ilgili bilgi sahibi olduğunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="d48c7-113">This tutorial assumes you are already familiar with using Azure PowerShell.</span></span> <span data-ttu-id="d48c7-114">Özellikle, tooknow nasıl gereksinim tooAzure toolog.</span><span class="sxs-lookup"><span data-stu-id="d48c7-114">In particular, you need tooknow how toolog in tooAzure.</span></span> <span data-ttu-id="d48c7-115">Merhaba bkz [Azure PowerShell ile çalışmaya başlama](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) yardıma gereksinim duyarsanız.</span><span class="sxs-lookup"><span data-stu-id="d48c7-115">See hello [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) if you need help.</span></span>

<span data-ttu-id="d48c7-116">Abonelik adı oturum toolog:</span><span class="sxs-lookup"><span data-stu-id="d48c7-116">toolog in with a subscription name:</span></span>

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

<span data-ttu-id="d48c7-117">Merhaba abonelik adı yerine bir abonelik kimliği toolog içinde de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d48c7-117">Instead of hello subscription name, you can also use a subscription id toolog in:</span></span>

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

<span data-ttu-id="d48c7-118">Başarılı olursa, bu komutun çıktısı hello hello metin aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="d48c7-118">If  successful, hello output of this command looks like hello following text:</span></span>

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-hello-tutorial"></a><span data-ttu-id="d48c7-119">Merhaba öğretici için hazırlama</span><span class="sxs-lookup"><span data-stu-id="d48c7-119">Preparing for hello tutorial</span></span>

<span data-ttu-id="d48c7-120">Bu öğreticide Hello PowerShell parçacıkları bu değişkenleri toostore bu bilgileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="d48c7-120">hello PowerShell snippets in this tutorial use these variables toostore this information:</span></span>

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="d48c7-121">Bir Data Lake Analytics hesabı hakkında bilgi edinme</span><span class="sxs-lookup"><span data-stu-id="d48c7-121">Get information about a Data Lake Analytics account</span></span>

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="d48c7-122">U-SQL işi gönderme</span><span class="sxs-lookup"><span data-stu-id="d48c7-122">Submit a U-SQL job</span></span>

<span data-ttu-id="d48c7-123">Bir PowerShell değişken toohold hello U-SQL betiği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d48c7-123">Create a PowerShell variable toohold hello U-SQL script.</span></span>

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

<span data-ttu-id="d48c7-124">Merhaba betik gönderin.</span><span class="sxs-lookup"><span data-stu-id="d48c7-124">Submit hello script.</span></span>

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

<span data-ttu-id="d48c7-125">Alternatif olarak, hello komut dosyası olarak kaydedin ve komut aşağıdaki hello ile gönderin:</span><span class="sxs-lookup"><span data-stu-id="d48c7-125">Alternatively, you could save hello script as a file and submit with hello following command:</span></span>

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


<span data-ttu-id="d48c7-126">Belirli bir iş Hello durumunu alın.</span><span class="sxs-lookup"><span data-stu-id="d48c7-126">Get hello status of a specific job.</span></span> <span data-ttu-id="d48c7-127">Hello iş yapılır görene kadar bu cmdlet'i kullanarak tutun.</span><span class="sxs-lookup"><span data-stu-id="d48c7-127">Keep using this cmdlet until you see hello job is done.</span></span>

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

<span data-ttu-id="d48c7-128">Bir işi tamamlanana kadar Get-AdlAnalyticsJob tekrar tekrar çağırmak yerine, hello bekleme AdlJob cmdlet'ini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d48c7-128">Instead of calling Get-AdlAnalyticsJob over and over until a job finishes, you can use hello Wait-AdlJob cmdlet.</span></span>

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

<span data-ttu-id="d48c7-129">Merhaba çıktı dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="d48c7-129">Download hello output file.</span></span>

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a><span data-ttu-id="d48c7-130">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d48c7-130">See also</span></span>
* <span data-ttu-id="d48c7-131">toosee hello aynı öğreticiyi diğer araçları kullanarak, hello sekmesini seçiciler hello sayfasının hello üstte'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d48c7-131">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
* <span data-ttu-id="d48c7-132">U-SQL, toolearn bkz [Azure Data Lake Analytics U-SQL dili ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d48c7-132">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="d48c7-133">Yönetim görevleri için bkz. [Azure portalı kullanarak Azure Data Lake Analytics'i yönetme](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d48c7-133">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
