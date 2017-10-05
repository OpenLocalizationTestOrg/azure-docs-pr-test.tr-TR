---
title: "Azure PowerShell'i kullanarak Azure Data Lake Analytics ile çalışmaya başlama | Microsoft Belgeleri"
description: "Azure PowerShell kullanarak bir Data Lake Analytics hesabı oluşturun, U-SQL'yi kullanarak Data Lake Analytics işi oluşturun ve bu işi gönderin. "
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
ms.openlocfilehash: 4f73e27c733edae658d1ea3bdabe48076328279b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="14777-103">Azure PowerShell'i kullanarak Azure Data Lake Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="14777-103">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="14777-104">Azure PowerShell kullanarak Azure Data Lake Analytics hesapları oluşturma ve sonra U-SQL işleri gönderip çalıştırma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="14777-104">Learn how to use Azure PowerShell to create Azure Data Lake Analytics accounts and then submit and run U-SQL jobs.</span></span> <span data-ttu-id="14777-105">Data Lake Analytics hakkında daha fazla bilgi için bkz. [Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="14777-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14777-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="14777-106">Prerequisites</span></span>

<span data-ttu-id="14777-107">Bu öğreticiye başlamadan önce aşağıdaki bilgilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="14777-107">Before you begin this tutorial, you must have the following information:</span></span>

* <span data-ttu-id="14777-108">**Azure Data Lake Analytics hesabı**.</span><span class="sxs-lookup"><span data-stu-id="14777-108">**An Azure Data Lake Analytics account**.</span></span> <span data-ttu-id="14777-109">Bkz. [Data Lake Analytics ile çalışmaya başlama](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="14777-109">See [Get started with Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span></span>
* <span data-ttu-id="14777-110">**Azure PowerShell içeren bir iş istasyonu**.</span><span class="sxs-lookup"><span data-stu-id="14777-110">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="14777-111">Bkz. [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="14777-111">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="14777-112">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="14777-112">Log in to Azure</span></span>

<span data-ttu-id="14777-113">Bu öğreticide, Azure PowerShell kullanımıyla ilgili bilgi sahibi olduğunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="14777-113">This tutorial assumes you are already familiar with using Azure PowerShell.</span></span> <span data-ttu-id="14777-114">Özellikle Azure'da oturum açmayı bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="14777-114">In particular, you need to know how to log in to Azure.</span></span> <span data-ttu-id="14777-115">Yardıma ihtiyacınız varsa bkz. [Azure PowerShell ile çalışmaya başlama](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="14777-115">See the [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) if you need help.</span></span>

<span data-ttu-id="14777-116">Abonelik adı ile oturum açmak için:</span><span class="sxs-lookup"><span data-stu-id="14777-116">To log in with a subscription name:</span></span>

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

<span data-ttu-id="14777-117">Oturum açmak için abonelik adı yerine abonelik kimliğini de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="14777-117">Instead of the subscription name, you can also use a subscription id to log in:</span></span>

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

<span data-ttu-id="14777-118">Başarılı olması halinde bu komutun çıkışı şu metin gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="14777-118">If  successful, the output of this command looks like the following text:</span></span>

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-the-tutorial"></a><span data-ttu-id="14777-119">Öğreticiye hazırlanma</span><span class="sxs-lookup"><span data-stu-id="14777-119">Preparing for the tutorial</span></span>

<span data-ttu-id="14777-120">Bu öğreticideki PowerShell kod parçacıkları bu bilgileri depolamak için aşağıdaki değişkenleri kullanır:</span><span class="sxs-lookup"><span data-stu-id="14777-120">The PowerShell snippets in this tutorial use these variables to store this information:</span></span>

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="14777-121">Bir Data Lake Analytics hesabı hakkında bilgi edinme</span><span class="sxs-lookup"><span data-stu-id="14777-121">Get information about a Data Lake Analytics account</span></span>

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="14777-122">U-SQL işi gönderme</span><span class="sxs-lookup"><span data-stu-id="14777-122">Submit a U-SQL job</span></span>

<span data-ttu-id="14777-123">U-SQL betiğini tutmak için bir PowerShell değişkeni oluşturun.</span><span class="sxs-lookup"><span data-stu-id="14777-123">Create a PowerShell variable to hold the U-SQL script.</span></span>

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
    TO "/data.csv"
    USING Outputters.Csv();

"@
```

<span data-ttu-id="14777-124">Betiği gönderin.</span><span class="sxs-lookup"><span data-stu-id="14777-124">Submit the script.</span></span>

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

<span data-ttu-id="14777-125">Alternatif olarak, betiği dosya olarak kaydedebilir ve şu komutla gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="14777-125">Alternatively, you could save the script as a file and submit with the following command:</span></span>

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


<span data-ttu-id="14777-126">Belirli bir işin durumunu alın.</span><span class="sxs-lookup"><span data-stu-id="14777-126">Get the status of a specific job.</span></span> <span data-ttu-id="14777-127">İş tamamlanana kadar bu cmdlet'i kullanmaya devam edin.</span><span class="sxs-lookup"><span data-stu-id="14777-127">Keep using this cmdlet until you see the job is done.</span></span>

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

<span data-ttu-id="14777-128">Bir iş tamamlanana kadar Get-AdlAnalyticsJob yöntemini tekrar tekrar çağırmak yerine, Wait-AdlJob cmdlet’ini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14777-128">Instead of calling Get-AdlAnalyticsJob over and over until a job finishes, you can use the Wait-AdlJob cmdlet.</span></span>

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

<span data-ttu-id="14777-129">Çıkış dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="14777-129">Download the output file.</span></span>

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a><span data-ttu-id="14777-130">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="14777-130">See also</span></span>
* <span data-ttu-id="14777-131">Aynı öğreticiyi diğer araçları kullanarak görmek için sayfanın üst kısmındaki sekme seçicilerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="14777-131">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
* <span data-ttu-id="14777-132">U-SQL öğrenmek için bkz. [Azure Data Lake Analytics U-SQL dili ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="14777-132">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="14777-133">Yönetim görevleri için bkz. [Azure portalı kullanarak Azure Data Lake Analytics'i yönetme](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="14777-133">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
