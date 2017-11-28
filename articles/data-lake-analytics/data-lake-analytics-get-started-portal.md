---
title: "Azure portalını kullanarak Azure Data Lake Analytics ile çalışmaya başlama | Microsoft Docs"
description: "Bir Data Lake Analytics hesabı oluşturmak, U-SQL'yi kullanarak Data Lake Analytics işi oluşturmak ve bu işi göndermek için Azure portalının nasıl kullanılacağını öğrenin. "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 2722a2d72ed90ea0005362563ecaee30750c040a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a><span data-ttu-id="01f4e-103">Azure portalı kullanarak Azure Data Lake Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="01f4e-103">Get started with Azure Data Lake Analytics using Azure portal</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="01f4e-104">Azure Data Lake Analytics hesapları oluşturmak, [U-SQL](data-lake-analytics-u-sql-get-started.md) içinde işler tanımlamak ve Data Lake Analytics hizmetine iş göndermek için Azure portalının nasıl kullanılacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="01f4e-104">Learn how to use the Azure portal to create Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to the Data Lake Analytics service.</span></span> <span data-ttu-id="01f4e-105">Data Lake Analytics hakkında daha fazla bilgi için bkz. [Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="01f4e-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01f4e-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="01f4e-106">Prerequisites</span></span>

<span data-ttu-id="01f4e-107">Bu öğreticiye başlamadan önce bir **Azure aboneliğinizin** olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="01f4e-107">Before you begin this tutorial, you must have an **Azure subscription**.</span></span> <span data-ttu-id="01f4e-108">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="01f4e-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="01f4e-109">Data Lake Analytics hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="01f4e-109">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="01f4e-110">Şimdi aynı anda bir Data Lake Analytics ve Data Lake Store hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="01f4e-110">Now, you will create a Data Lake Analytics and a Data Lake Store account at the same time.</span></span>  <span data-ttu-id="01f4e-111">Bu basit bir adımdır ve tamamlanması yaklaşık olarak 60 saniye sürer.</span><span class="sxs-lookup"><span data-stu-id="01f4e-111">This step is simple and only takes about 60 seconds to finish.</span></span>

1. <span data-ttu-id="01f4e-112">[Azure portalı](https://portal.azure.com) üzerinde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="01f4e-112">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="01f4e-113">**Yeni** >  **Veri + Analiz** > **Data Lake Analytics**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01f4e-113">Click **New** >  **Data + Analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="01f4e-114">Aşağıdaki öğeler için değerleri seçin:</span><span class="sxs-lookup"><span data-stu-id="01f4e-114">Select values for the following items:</span></span>
   * <span data-ttu-id="01f4e-115">**Ad**: Data Lake Analytics hesabınızı adlandırın (Yalnızca küçük harf ve sayı kullanılabilir).</span><span class="sxs-lookup"><span data-stu-id="01f4e-115">**Name**: Name your Data Lake Analytics account (Only lower case letters and numbers allowed).</span></span>
   * <span data-ttu-id="01f4e-116">**Abonelik**: Analytics hesabı için kullanılan Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="01f4e-116">**Subscription**: Choose the Azure subscription used for the Analytics account.</span></span>
   * <span data-ttu-id="01f4e-117">**Kaynak Grubu**.</span><span class="sxs-lookup"><span data-stu-id="01f4e-117">**Resource Group**.</span></span> <span data-ttu-id="01f4e-118">Var olan bir Azure Kaynak Grubu'nu seçin veya yeni bir grup oluşturun.</span><span class="sxs-lookup"><span data-stu-id="01f4e-118">Select an existing Azure Resource Group or create a new one.</span></span>
   * <span data-ttu-id="01f4e-119">**Konum**.</span><span class="sxs-lookup"><span data-stu-id="01f4e-119">**Location**.</span></span> <span data-ttu-id="01f4e-120">Data Lake Analytics hesabı için bir Azure veri merkezi seçin.</span><span class="sxs-lookup"><span data-stu-id="01f4e-120">Select an Azure data center for the Data Lake Analytics account.</span></span>
   * <span data-ttu-id="01f4e-121">**Data Lake Store**: Yeni bir Data Lake Store hesabı oluşturmaya yönelik yönergeyi uygulayın veya var olan bir hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="01f4e-121">**Data Lake Store**: Follow the instruction to create a new Data Lake Store account, or select an existing one.</span></span> 
4. <span data-ttu-id="01f4e-122">İsteğe bağlı olarak Data Lake Analytics hesabınıza yönelik bir fiyatlandırma katmanı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01f4e-122">Optionally, select a pricing tier for your Data Lake Analytics account.</span></span>
5. <span data-ttu-id="01f4e-123">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01f4e-123">Click **Create**.</span></span> 


## <a name="your-first-u-sql-script"></a><span data-ttu-id="01f4e-124">İlk U-SQL betiğiniz</span><span class="sxs-lookup"><span data-stu-id="01f4e-124">Your first U-SQL script</span></span>

<span data-ttu-id="01f4e-125">Aşağıda basit bir U-SQL betiği gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="01f4e-125">The following text is a very simple U-SQL script.</span></span> <span data-ttu-id="01f4e-126">Betik içinde küçük bir veri kümesinin tanımlanmasına ve ardından söz konusu veri kümesinin varsayılan Data Lake Store'a `/data.csv` adlı bir dosya olarak yazılmasına yarar.</span><span class="sxs-lookup"><span data-stu-id="01f4e-126">All it does is define a small dataset within the script and then write that dataset out to the default Data Lake Store as a file called `/data.csv`.</span></span>

```
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
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="01f4e-127">U-SQL işi gönderme</span><span class="sxs-lookup"><span data-stu-id="01f4e-127">Submit a U-SQL job</span></span>

1. <span data-ttu-id="01f4e-128">Data Lake Analytics hesabında **Yeni İş**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01f4e-128">From the Data Lake Analytics account, click **New Job**.</span></span>
2. <span data-ttu-id="01f4e-129">Yukarıda gösterilen U-SQL betiğinin metnine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="01f4e-129">Paste in the text of the U-SQL script shown above.</span></span> 
3. <span data-ttu-id="01f4e-130">**İşi Gönder**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01f4e-130">Click **Submit Job**.</span></span>   
4. <span data-ttu-id="01f4e-131">İş durumu **Başarılı** olarak değiştirilene kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="01f4e-131">Wait until the job status changes to **Succeeded**.</span></span>
5. <span data-ttu-id="01f4e-132">İş başarısız olduysa bkz. [Data Lake Analytics işlerini izleme ve sorun giderme](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="01f4e-132">If the job failed, see [Monitor and troubleshoot Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>
6. <span data-ttu-id="01f4e-133">**Çıkış** sekmesine ve ardından `data.csv` öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01f4e-133">Click the **Output** tab, and then click `data.csv`.</span></span> 

## <a name="see-also"></a><span data-ttu-id="01f4e-134">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="01f4e-134">See also</span></span>

* <span data-ttu-id="01f4e-135">U-SQL uygulamalarını geliştirmeye başlamak için bkz. [Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="01f4e-135">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="01f4e-136">U-SQL öğrenmek için bkz. [Azure Data Lake Analytics U-SQL dili ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="01f4e-136">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="01f4e-137">Yönetim görevleri için bkz. [Azure portalı kullanarak Azure Data Lake Analytics'i yönetme](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="01f4e-137">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
