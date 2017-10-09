---
title: "Stream Analytics sorguları için uyarılar aaaSet | Microsoft Docs"
description: "Uyarı anlama akış analizi"
keywords: "Uyarıları ayarlayın"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/26/2017
ms.author: jeffstok
ms.openlocfilehash: 7b1d90d1468311186567c8518e0283ea6b88c3f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a><span data-ttu-id="b4c1b-104">Azure Stream Analytics işleri için uyarıları ayarlama</span><span class="sxs-lookup"><span data-stu-id="b4c1b-104">Set up alerts for Azure Stream Analytics jobs</span></span>
## <a name="introduction-monitor-page"></a><span data-ttu-id="b4c1b-105">Giriş: İzleme sayfası</span><span class="sxs-lookup"><span data-stu-id="b4c1b-105">Introduction: Monitor page</span></span>
<span data-ttu-id="b4c1b-106">Ölçüm belirttiğiniz bir koşul ulaştığında bir uyarı uyarılar tootrigger ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4c1b-106">You can set up alerts tootrigger an alert when a metric reaches a condition that you specify.</span></span> <span data-ttu-id="b4c1b-107">Örneğin, bir uyarı için bir koşul hello aşağıdaki gibi ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b4c1b-107">For example, you might set up an alert for a condition like hello following:</span></span>

`If there are zero input events in hello last 5 minutes, send email notification toosa-admin@example.com`

<span data-ttu-id="b4c1b-108">Kuralları hello portal üzerinden ölçümleri üzerinde ayarlanabilir veya yapılandırılabilir [program aracılığıyla](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) işlem günlükleri veriler üzerinde.</span><span class="sxs-lookup"><span data-stu-id="b4c1b-108">Rules can be set up on metrics through hello portal, or can be configured [programmatically](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) over Operation Logs data.</span></span>

## <a name="set-up-alerts-in-hello-azure-portal"></a><span data-ttu-id="b4c1b-109">Hello Azure portal'te uyarıları ayarlama</span><span class="sxs-lookup"><span data-stu-id="b4c1b-109">Set up alerts in hello Azure portal</span></span>
1. <span data-ttu-id="b4c1b-110">Hello Azure portal, hello Stream Analytics işi için bir uyarı toocreate istediğiniz açın.</span><span class="sxs-lookup"><span data-stu-id="b4c1b-110">In hello Azure portal, open hello Stream Analytics job you want toocreate an alert for.</span></span> 

2. <span data-ttu-id="b4c1b-111">Merhaba, **iş** dikey penceresinde hello tıklatın **izleme** bölümü.</span><span class="sxs-lookup"><span data-stu-id="b4c1b-111">In hello **Job** blade, click hello **Monitoring** section.</span></span>  

3. <span data-ttu-id="b4c1b-112">Merhaba, **ölçüm** dikey penceresinde hello tıklatın **uyarı Ekle** komutu.</span><span class="sxs-lookup"><span data-stu-id="b4c1b-112">In hello **Metric** blade, click hello **Add alert** command.</span></span>

      ![Azure portal Kurulumu](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. <span data-ttu-id="b4c1b-114">Bir ad ve açıklama girin.</span><span class="sxs-lookup"><span data-stu-id="b4c1b-114">Enter a name and a description.</span></span>

5. <span data-ttu-id="b4c1b-115">Merhaba seçiciler toodefine hello koşul altında hangi hello uyarı gönderilir kullanın.</span><span class="sxs-lookup"><span data-stu-id="b4c1b-115">Use hello selectors toodefine hello condition under which hello alert will be sent.</span></span>

6. <span data-ttu-id="b4c1b-116">Merhaba uyarı nereye hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b4c1b-116">Provide information about where hello alert should go.</span></span>

      ![Bir Azure akış analizi işi için bir uyarı ayarlama](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

<span data-ttu-id="b4c1b-118">Uyarıları hello Azure portal yapılandırma hakkında daha ayrıntılı bilgi için bkz: [uyarı bildirimleri alma](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="b4c1b-118">For more detail on configuring alerts in hello Azure portal, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>  


## <a name="get-help"></a><span data-ttu-id="b4c1b-119">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="b4c1b-119">Get help</span></span>
<span data-ttu-id="b4c1b-120">Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.</span><span class="sxs-lookup"><span data-stu-id="b4c1b-120">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4c1b-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b4c1b-121">Next steps</span></span>
* [<span data-ttu-id="b4c1b-122">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="b4c1b-122">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="b4c1b-123">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b4c1b-123">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="b4c1b-124">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="b4c1b-124">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="b4c1b-125">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="b4c1b-125">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="b4c1b-126">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="b4c1b-126">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

