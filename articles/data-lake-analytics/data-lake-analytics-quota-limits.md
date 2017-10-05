---
title: "Azure Data Lake Analytics kota sınırları | Microsoft Docs"
description: "Ayarlama ve Azure Data Lake Analytics (ADLA) hesaplarındaki kota sınırları artırmak hakkında bilgi edinin."
services: data-lake-analytics
keywords: Azure Data Lake Analytics
documentationcenter: 
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: omidm
ms.openlocfilehash: 957f306ea0e80b5830ad64e5ef06c6d122d9eccc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a><span data-ttu-id="99a13-104">Azure Data Lake Analytics kota sınırları</span><span class="sxs-lookup"><span data-stu-id="99a13-104">Azure Data Lake Analytics Quota Limits</span></span>

<span data-ttu-id="99a13-105">Ayarlama ve Azure Data Lake Analytics (ADLA) hesaplarındaki kota sınırları artırmak hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="99a13-105">Learn how to adjust and increase quota limits in Azure Data Lake Analytics (ADLA) accounts.</span></span> <span data-ttu-id="99a13-106">Bu sınırlar bilerek, U-SQL işi davranışı anlamanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="99a13-106">Knowing these limits may help you understand your U-SQL job behavior.</span></span> <span data-ttu-id="99a13-107">Bize ulaşmasını tarafından maksimum sınırları artırmak için tüm kota sınırları yumuşak,.</span><span class="sxs-lookup"><span data-stu-id="99a13-107">All quota limits are soft, so you can increase the maximum limits by reaching out to us.</span></span>

## <a name="azure-subscriptions-limits"></a><span data-ttu-id="99a13-108">Azure abonelikleri sınırları</span><span class="sxs-lookup"><span data-stu-id="99a13-108">Azure subscriptions limits</span></span>

<span data-ttu-id="99a13-109">**ADLA en fazla abonelik başına hesapları:** 5</span><span class="sxs-lookup"><span data-stu-id="99a13-109">**Maximum number of ADLA accounts per subscription:**  5</span></span>

 <span data-ttu-id="99a13-110">Bu ADLA hesapları abonelik başına oluşturabileceğiniz en fazla sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="99a13-110">This is the maximum number of ADLA accounts you can create per subscription.</span></span> <span data-ttu-id="99a13-111">Altıncı bir ADLA hesabı oluşturmayı denerseniz, "en fazla izin Data Lake Analytics hesabı sayısını (5) altında abonelik adını bölgesindeki ulaştığınız" bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="99a13-111">If you try to create a sixth ADLA account, you will get an error "You have reached the maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name".</span></span> <span data-ttu-id="99a13-112">Bu durumda, tüm kullanılmayan ADLA hesapları silmek ya da tarafımızca ulaşmak [bir destek bileti açmadan](#increase-maximum-quota-limits).</span><span class="sxs-lookup"><span data-stu-id="99a13-112">In this case, either delete any unused ADLA accounts, or reach out to us by [opening a support ticket](#increase-maximum-quota-limits).</span></span>

## <a name="adla-account-limits"></a><span data-ttu-id="99a13-113">ADLA hesabı sınırları</span><span class="sxs-lookup"><span data-stu-id="99a13-113">ADLA account limits</span></span>

<span data-ttu-id="99a13-114">**Hesap başına en fazla Analytics birimi (Avustralya) sayısı:** 250</span><span class="sxs-lookup"><span data-stu-id="99a13-114">**Maximum number of Analytics Units (AUs) per account:** 250</span></span>

<span data-ttu-id="99a13-115">Hesabınızı çalışabilir Avustralya üst sınırını budur.</span><span class="sxs-lookup"><span data-stu-id="99a13-115">This is the maximum number of AUs that can run concurrently in your account.</span></span> <span data-ttu-id="99a13-116">Avustralya toplam tüm işleri arasında bu sınırı aşarsa, yeni işleri otomatik olarak kuyruğa alınır.</span><span class="sxs-lookup"><span data-stu-id="99a13-116">If your total running AUs across all jobs exceeds this limit, newer jobs are queued automatically.</span></span> <span data-ttu-id="99a13-117">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="99a13-117">For example:</span></span>

* <span data-ttu-id="99a13-118">Yalnızca bir işe varsa 250 ile ikinci bir gönderdiğinizde Avustralya, işi çalıştırılırken iş kuyruğundaki ilk iş tamamlanana kadar bekler.</span><span class="sxs-lookup"><span data-stu-id="99a13-118">If you have only one job running with 250 AUs, when you submit a second job it will wait in the job queue until the first job completes.</span></span>
* <span data-ttu-id="99a13-119">Çalışan beş işleri zaten varsa ve her 50 kullanarak 20 gereken altıncı bir işi gönderdiğinizde Avustralya kalmayana kadar 20 iş kuyruğundaki bekler Avustralya Avustralya kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="99a13-119">If you already have five jobs running and each is using 50 AUs, when you submit a sixth job that needs 20 AUs it waits in the job queue until there are 20 AUs available.</span></span>

<span data-ttu-id="99a13-120">**Hesap başına eşzamanlı U-SQL işi sayısı üst sınırı:** 20</span><span class="sxs-lookup"><span data-stu-id="99a13-120">**Maximum number of concurrent U-SQL jobs per account:** 20</span></span>

<span data-ttu-id="99a13-121">Maksimum sayıda hesabınızda çalışabilir işi budur.</span><span class="sxs-lookup"><span data-stu-id="99a13-121">This is the maximum number of jobs that can run concurrently in your account.</span></span> <span data-ttu-id="99a13-122">Bu değer yeni işleri otomatik olarak kuyruğa alınır.</span><span class="sxs-lookup"><span data-stu-id="99a13-122">Above this value, newer jobs are queued automatically.</span></span>

## <a name="adjust-adla-quota-limits-per-account"></a><span data-ttu-id="99a13-123">Hesap başına ADLA kota sınırları ayarlama</span><span class="sxs-lookup"><span data-stu-id="99a13-123">Adjust ADLA quota limits per account</span></span>

1. <span data-ttu-id="99a13-124">[Azure portalı](https://portal.azure.com) üzerinde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="99a13-124">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="99a13-125">Varolan ADLA hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="99a13-125">Choose an existing ADLA account.</span></span>
3. <span data-ttu-id="99a13-126">**Özellikler**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="99a13-126">Click **Properties**.</span></span>
4. <span data-ttu-id="99a13-127">Ayarlama **paralellik** ve **eşzamanlı iş** gereksinimlerinize uygun olarak.</span><span class="sxs-lookup"><span data-stu-id="99a13-127">Adjust **Parallelism** and **Concurrent Jobs** to suit your needs.</span></span>

    ![Azure Data Lake Analytics portalı dikey penceresi](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a><span data-ttu-id="99a13-129">En yüksek kota sınırları artırmak</span><span class="sxs-lookup"><span data-stu-id="99a13-129">Increase maximum quota limits</span></span>

1. <span data-ttu-id="99a13-130">Azure portalında bir destek isteği açın.</span><span class="sxs-lookup"><span data-stu-id="99a13-130">Open a support request in Azure Portal.</span></span>

    ![Azure Data Lake Analytics portalı dikey penceresi](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Azure Data Lake Analytics portalı dikey penceresi](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. <span data-ttu-id="99a13-133">Sorun türü seçin **kota**.</span><span class="sxs-lookup"><span data-stu-id="99a13-133">Select the issue type **Quota**.</span></span>
3. <span data-ttu-id="99a13-134">Seçin, **abonelik** ("Deneme" aboneliği olmadığından emin olun).</span><span class="sxs-lookup"><span data-stu-id="99a13-134">Select your **Subscription** (make sure it is not a "trial" subscription).</span></span>
4. <span data-ttu-id="99a13-135">Kota türü seçin **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="99a13-135">Select quota type **Data Lake Analytics**.</span></span>

    ![Azure Data Lake Analytics portalı dikey penceresi](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. <span data-ttu-id="99a13-137">Sorun dikey penceresinde istenen artış sınırınızı açıklayan **ayrıntıları** bu ek kapasite neden ihtiyacınız olan.</span><span class="sxs-lookup"><span data-stu-id="99a13-137">In the problem blade, explain your requested increase limit with **Details** of why you need this extra capacity.</span></span>

    ![Azure Data Lake Analytics portalı dikey penceresi](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. <span data-ttu-id="99a13-139">İletişim bilgilerinizi doğrulayın ve destek isteği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="99a13-139">Verify your contact information and create the support request.</span></span>

<span data-ttu-id="99a13-140">Microsoft, isteğinizi gözden geçirir ve mümkün olan en kısa sürede iş gereksinimlerinizi karşılamak çalışır.</span><span class="sxs-lookup"><span data-stu-id="99a13-140">Microsoft reviews your request and tries to accommodate your business needs as soon as possible.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99a13-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="99a13-141">Next steps</span></span>

* [<span data-ttu-id="99a13-142">Microsoft Azure Data Lake Analytics'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="99a13-142">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="99a13-143">Azure Data Lake Analytics'i Azure PowerShell'i kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="99a13-143">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="99a13-144">Azure portalını kullanarak Azure Data Lake Analytics işlerini izleme ve sorun giderme</span><span class="sxs-lookup"><span data-stu-id="99a13-144">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
