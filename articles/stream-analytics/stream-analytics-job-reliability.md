---
title: "Azure Stream Analytics işleri hizmet kesintilerine uğramaması | Microsoft Docs"
description: "Stream Analytics yapma hakkında rehberlik yükseltme esnek işler."
services: stream-analytics
documentationCenter: 
authors: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3ac65c93ecb47e93e963dd9869a7af70f73b19c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a><span data-ttu-id="f1fb5-103">Akış analizi işi güvenilirlik hizmet güncelleştirmeleri sırasında garanti</span><span class="sxs-lookup"><span data-stu-id="f1fb5-103">Guarantee Stream Analytics job reliability during service updates</span></span>

<span data-ttu-id="f1fb5-104">Tam olarak yönetilen bir hizmet olan hello yetenek toointroduce yeni hizmeti işlevselliği ve hızlı bir hızda iyileştirmeleri parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="f1fb5-104">Part of being a fully managed service is hello capability toointroduce new service functionality and improvements at a rapid pace.</span></span> <span data-ttu-id="f1fb5-105">Sonuç olarak, Stream Analytics haftalık (veya daha sık) temelinde dağıtmak bir hizmet güncelleştirmesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="f1fb5-105">As a result, Stream Analytics can have a service update deploy on a weekly (or more frequent) basis.</span></span> <span data-ttu-id="f1fb5-106">Ne kadar test bitti olsun hala, var olan, çalışan bir iş hatanın toohello giriş kesilebilir bir riski yoktur.</span><span class="sxs-lookup"><span data-stu-id="f1fb5-106">No matter how much testing is done there is still a risk that an existing, running job may break due toohello introduction of a bug.</span></span> <span data-ttu-id="f1fb5-107">Kritik akış işleme işleri çalıştırma müşteriler için bu riskleri kaçınılması toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="f1fb5-107">For customers who run critical streaming processing jobs these risks need toobe avoided.</span></span> <span data-ttu-id="f1fb5-108">Bir mekanizma müşterileri tooreduce kullanabilir Azure'un bu riskidir  **[eşleştirilmiş bölge](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  modeli.</span><span class="sxs-lookup"><span data-stu-id="f1fb5-108">A mechanism customers can use tooreduce this risk is Azure’s **[paired region](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** model.</span></span> 

## <a name="how-do-azure-paired-regions-address-this-concern"></a><span data-ttu-id="f1fb5-109">Azure eşleştirilmiş bölgeleri bu sorunu nasıl ele?</span><span class="sxs-lookup"><span data-stu-id="f1fb5-109">How do Azure paired regions address this concern?</span></span>

<span data-ttu-id="f1fb5-110">Akış analizi işleri eşleştirilmiş bölgelerde ayrı toplu olarak güncelleştirilir güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="f1fb5-110">Stream Analytics guarantees jobs in paired regions are updated in separate batches.</span></span> <span data-ttu-id="f1fb5-111">Sonuç olarak tooidentify olası sonu hataları ve bunları düzeltmek hello güncelleştirmeleri arasında yeterli zaman aralığı yok.</span><span class="sxs-lookup"><span data-stu-id="f1fb5-111">As a result there is a sufficient time gap between hello updates tooidentify potential breaking bugs and remediate them.</span></span>

<span data-ttu-id="f1fb5-112">_Orta Hindistan hello özel_ (eşleştirilmiş, bölge, Güney Hindistan ve akış analizi varlığı yok), Analytics hello değil gerçekleşecek bir güncelleştirme tooStream hello dağıtımını aynı zaman eşleştirilmiş bölgeler kümesinde.</span><span class="sxs-lookup"><span data-stu-id="f1fb5-112">_With hello exception of Central India_ (whose paired region, South India, does not have Stream Analytics presence), hello deployment of an update tooStream Analytics would not occur at hello same time in a set of paired regions.</span></span> <span data-ttu-id="f1fb5-113">Birden çok bölgeye dağıtımlarda **hello içinde aynı grubu** oluşabilir **Merhaba, aynı anda**.</span><span class="sxs-lookup"><span data-stu-id="f1fb5-113">Deployments in multiple regions **in hello same group** may occur **at hello same time**.</span></span>

<span data-ttu-id="f1fb5-114">Merhaba makale üzerinde  **[kullanılabilirlik ve eşleştirilmiş bölgeleri](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  hello en güncel bilgileri üzerinde bölgeler eşleştirilmiş sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f1fb5-114">hello article on **[availability and paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** has hello most up-to-date information on which regions are paired.</span></span>

<span data-ttu-id="f1fb5-115">Müşterilerin tavsiye edilir toodeploy aynı işleri eşleştirilmiş tooboth bölgeler önerilir.</span><span class="sxs-lookup"><span data-stu-id="f1fb5-115">Customers are advised toodeploy identical jobs tooboth paired regions.</span></span> <span data-ttu-id="f1fb5-116">Ayrıca Analytics izleme kapasiteleri, müşterilerin iç olan de tooStream toomonitor hello işleri tavsiye gibi **her ikisi de** üretim işler.</span><span class="sxs-lookup"><span data-stu-id="f1fb5-116">In addition tooStream Analytics internal monitoring capabilities, customers are also advised toomonitor hello jobs as if **both** are production jobs.</span></span> <span data-ttu-id="f1fb5-117">Bir sonu tanımlanan toobe hello Stream Analytics Hizmet güncelleştirmesi sonucu ise, uygun şekilde İlerlet ve herhangi bir aşağı akış tüketicileri toohello sağlıklı proje çıktı başarısız.</span><span class="sxs-lookup"><span data-stu-id="f1fb5-117">If a break is identified toobe a result of hello Stream Analytics service update, escalate appropriately and fail over any downstream consumers toohello healthy job output.</span></span> <span data-ttu-id="f1fb5-118">Yükseltme toosupport hello yeni dağıtım tarafından etkilenen hello eşleştirilmiş bölge önlemek ve eşleştirilmiş hello işleri hello bütünlüğünü.</span><span class="sxs-lookup"><span data-stu-id="f1fb5-118">Escalation toosupport will prevent hello paired region from being affected by hello new deployment and maintain hello integrity of hello paired jobs.</span></span>
