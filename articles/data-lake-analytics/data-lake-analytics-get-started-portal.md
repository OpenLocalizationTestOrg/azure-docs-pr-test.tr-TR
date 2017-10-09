---
title: "Azure portal kullanarak Azure Data Lake Analytics ile başlatıldı aaaGet | Microsoft Docs"
description: "Toouse hello Azure portal toocreate Data Lake Analytics hesabı, U-SQL'yi kullanarak Data Lake Analytics işi oluşturma ve hello işi göndermek öğrenin. "
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
ms.openlocfilehash: 6bb54404fa42cfed25b18bc2bfb7c72e6c361149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a><span data-ttu-id="766ae-103">Azure portalı kullanarak Azure Data Lake Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="766ae-103">Get started with Azure Data Lake Analytics using Azure portal</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="766ae-104">Nasıl toouse hello Azure portal toocreate Azure Data Lake Analytics hesapları öğrenin, işleri tanımlayın [U-SQL](data-lake-analytics-u-sql-get-started.md)ve işleri toohello Data Lake Analytics hizmeti gönderin.</span><span class="sxs-lookup"><span data-stu-id="766ae-104">Learn how toouse hello Azure portal toocreate Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs toohello Data Lake Analytics service.</span></span> <span data-ttu-id="766ae-105">Data Lake Analytics hakkında daha fazla bilgi için bkz. [Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="766ae-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="766ae-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="766ae-106">Prerequisites</span></span>

<span data-ttu-id="766ae-107">Bu öğreticiye başlamadan önce bir **Azure aboneliğinizin** olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="766ae-107">Before you begin this tutorial, you must have an **Azure subscription**.</span></span> <span data-ttu-id="766ae-108">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="766ae-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="766ae-109">Data Lake Analytics hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="766ae-109">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="766ae-110">Şimdi, bir Data Lake Analytics oluşturacak ve bir Data Lake Store hesabı hello aynı saat.</span><span class="sxs-lookup"><span data-stu-id="766ae-110">Now, you will create a Data Lake Analytics and a Data Lake Store account at hello same time.</span></span>  <span data-ttu-id="766ae-111">Bu adım, basit bir işlemdir ve yalnızca 60 saniye toofinish alır.</span><span class="sxs-lookup"><span data-stu-id="766ae-111">This step is simple and only takes about 60 seconds toofinish.</span></span>

1. <span data-ttu-id="766ae-112">Toohello üzerinde oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="766ae-112">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="766ae-113">**Yeni** >  **Veri + Analiz** > **Data Lake Analytics**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="766ae-113">Click **New** >  **Data + Analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="766ae-114">Aşağıdaki öğelerindeki hello için değerleri seçin:</span><span class="sxs-lookup"><span data-stu-id="766ae-114">Select values for hello following items:</span></span>
   * <span data-ttu-id="766ae-115">**Ad**: Data Lake Analytics hesabınızı adlandırın (Yalnızca küçük harf ve sayı kullanılabilir).</span><span class="sxs-lookup"><span data-stu-id="766ae-115">**Name**: Name your Data Lake Analytics account (Only lower case letters and numbers allowed).</span></span>
   * <span data-ttu-id="766ae-116">**Abonelik**: hello hello Analytics hesabı için kullanılan Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="766ae-116">**Subscription**: Choose hello Azure subscription used for hello Analytics account.</span></span>
   * <span data-ttu-id="766ae-117">**Kaynak Grubu**.</span><span class="sxs-lookup"><span data-stu-id="766ae-117">**Resource Group**.</span></span> <span data-ttu-id="766ae-118">Var olan bir Azure Kaynak Grubu'nu seçin veya yeni bir grup oluşturun.</span><span class="sxs-lookup"><span data-stu-id="766ae-118">Select an existing Azure Resource Group or create a new one.</span></span>
   * <span data-ttu-id="766ae-119">**Konum**.</span><span class="sxs-lookup"><span data-stu-id="766ae-119">**Location**.</span></span> <span data-ttu-id="766ae-120">Merhaba Data Lake Analytics hesabı için bir Azure veri merkezi seçin.</span><span class="sxs-lookup"><span data-stu-id="766ae-120">Select an Azure data center for hello Data Lake Analytics account.</span></span>
   * <span data-ttu-id="766ae-121">**Data Lake Store**: hello yönerge toocreate yeni bir Data Lake Store hesabı izleyin veya varolan bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="766ae-121">**Data Lake Store**: Follow hello instruction toocreate a new Data Lake Store account, or select an existing one.</span></span> 
4. <span data-ttu-id="766ae-122">İsteğe bağlı olarak Data Lake Analytics hesabınıza yönelik bir fiyatlandırma katmanı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="766ae-122">Optionally, select a pricing tier for your Data Lake Analytics account.</span></span>
5. <span data-ttu-id="766ae-123">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="766ae-123">Click **Create**.</span></span> 


## <a name="your-first-u-sql-script"></a><span data-ttu-id="766ae-124">İlk U-SQL betiğiniz</span><span class="sxs-lookup"><span data-stu-id="766ae-124">Your first U-SQL script</span></span>

<span data-ttu-id="766ae-125">metin aşağıdaki hello çok basit bir U-SQL komut dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="766ae-125">hello following text is a very simple U-SQL script.</span></span> <span data-ttu-id="766ae-126">Tüm mevcut olan hello komut içinde küçük bir veri kümesini tanımlayın ve ardından bu veri kümesi toohello varsayılan Data Lake Store çıkışı adlı bir dosya yazma `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="766ae-126">All it does is define a small dataset within hello script and then write that dataset out toohello default Data Lake Store as a file called `/data.csv`.</span></span>

```
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
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="766ae-127">U-SQL işi gönderme</span><span class="sxs-lookup"><span data-stu-id="766ae-127">Submit a U-SQL job</span></span>

1. <span data-ttu-id="766ae-128">Data Lake Analytics hesabı Hello tıklatın **yeni iş**.</span><span class="sxs-lookup"><span data-stu-id="766ae-128">From hello Data Lake Analytics account, click **New Job**.</span></span>
2. <span data-ttu-id="766ae-129">Merhaba Hello metinde yukarıda gösterilen U-SQL betiğini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="766ae-129">Paste in hello text of hello U-SQL script shown above.</span></span> 
3. <span data-ttu-id="766ae-130">**İşi Gönder**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="766ae-130">Click **Submit Job**.</span></span>   
4. <span data-ttu-id="766ae-131">Merhaba iş durumu değişinceye kadar çok bekleyin**başarılı**.</span><span class="sxs-lookup"><span data-stu-id="766ae-131">Wait until hello job status changes too**Succeeded**.</span></span>
5. <span data-ttu-id="766ae-132">Merhaba işi başarısız olduysa bkz [İzleyici ve Data Lake Analytics işlerini sorun giderme](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="766ae-132">If hello job failed, see [Monitor and troubleshoot Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>
6. <span data-ttu-id="766ae-133">Merhaba tıklatın **çıkış** sekmesini ve ardından `data.csv`.</span><span class="sxs-lookup"><span data-stu-id="766ae-133">Click hello **Output** tab, and then click `data.csv`.</span></span> 

## <a name="see-also"></a><span data-ttu-id="766ae-134">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="766ae-134">See also</span></span>

* <span data-ttu-id="766ae-135">U-SQL uygulamalarını geliştirmeye başlatılan tooget bkz [Visual Studio için Data Lake Araçları'nı kullanarak geliştirme U-SQL betikleri](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="766ae-135">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="766ae-136">U-SQL, toolearn bkz [Azure Data Lake Analytics U-SQL dili ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="766ae-136">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="766ae-137">Yönetim görevleri için bkz. [Azure portalı kullanarak Azure Data Lake Analytics'i yönetme](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="766ae-137">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
