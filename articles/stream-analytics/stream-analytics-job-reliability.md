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
ms.openlocfilehash: 8dc19e1b37082c87d2990ad910d1af786f8b9280
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a><span data-ttu-id="b9dd8-103">Akış analizi işi güvenilirlik hizmet güncelleştirmeleri sırasında garanti</span><span class="sxs-lookup"><span data-stu-id="b9dd8-103">Guarantee Stream Analytics job reliability during service updates</span></span>

<span data-ttu-id="b9dd8-104">Tam olarak yönetilen bir hizmet olma yeteneği yeni hizmet işlevselliği ve hızlı bir hızda geliştirmeleri tanıtır bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="b9dd8-104">Part of being a fully managed service is the capability to introduce new service functionality and improvements at a rapid pace.</span></span> <span data-ttu-id="b9dd8-105">Sonuç olarak, Stream Analytics haftalık (veya daha sık) temelinde dağıtmak bir hizmet güncelleştirmesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="b9dd8-105">As a result, Stream Analytics can have a service update deploy on a weekly (or more frequent) basis.</span></span> <span data-ttu-id="b9dd8-106">Ne kadar test bitti olsun hala, var olan, çalışan bir iş bir hata giriş nedeniyle kesilebilir bir riski yoktur.</span><span class="sxs-lookup"><span data-stu-id="b9dd8-106">No matter how much testing is done there is still a risk that an existing, running job may break due to the introduction of a bug.</span></span> <span data-ttu-id="b9dd8-107">Kritik akış işleme işleri çalıştırma müşteriler için bu riskleri kaçınılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b9dd8-107">For customers who run critical streaming processing jobs these risks need to be avoided.</span></span> <span data-ttu-id="b9dd8-108">Müşteriler bu riskini azaltmak için kullanabileceğiniz bir Azure'nın mekanizmadır  **[eşleştirilmiş bölge](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  modeli.</span><span class="sxs-lookup"><span data-stu-id="b9dd8-108">A mechanism customers can use to reduce this risk is Azure’s **[paired region](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** model.</span></span> 

## <a name="how-do-azure-paired-regions-address-this-concern"></a><span data-ttu-id="b9dd8-109">Azure eşleştirilmiş bölgeleri bu sorunu nasıl ele?</span><span class="sxs-lookup"><span data-stu-id="b9dd8-109">How do Azure paired regions address this concern?</span></span>

<span data-ttu-id="b9dd8-110">Akış analizi işleri eşleştirilmiş bölgelerde ayrı toplu olarak güncelleştirilir güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="b9dd8-110">Stream Analytics guarantees jobs in paired regions are updated in separate batches.</span></span> <span data-ttu-id="b9dd8-111">Sonuç olarak olası sonu hataları belirlemek ve düzeltmek için güncelleştirmeleri arasında yeterli zaman aralığı yok.</span><span class="sxs-lookup"><span data-stu-id="b9dd8-111">As a result there is a sufficient time gap between the updates to identify potential breaking bugs and remediate them.</span></span>

<span data-ttu-id="b9dd8-112">_Orta Hindistan dışında_ (eşleştirilmiş, bölge, Güney Hindistan ve akış analizi varlığı yok), Stream Analytics için bir güncelleştirme dağıtımının eşleştirilmiş bölgeler kümesinde aynı zamanda oluşacak değil.</span><span class="sxs-lookup"><span data-stu-id="b9dd8-112">_With the exception of Central India_ (whose paired region, South India, does not have Stream Analytics presence), the deployment of an update to Stream Analytics would not occur at the same time in a set of paired regions.</span></span> <span data-ttu-id="b9dd8-113">Birden çok bölgeye dağıtımlarda **aynı gruptaki** oluşabilir **aynı anda**.</span><span class="sxs-lookup"><span data-stu-id="b9dd8-113">Deployments in multiple regions **in the same group** may occur **at the same time**.</span></span>

<span data-ttu-id="b9dd8-114">Makale  **[kullanılabilirlik ve eşleştirilmiş bölgeleri](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  üzerinde bölgeler eşleştirilmiş en güncel bilgileri içeriyor.</span><span class="sxs-lookup"><span data-stu-id="b9dd8-114">The article on **[availability and paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** has the most up-to-date information on which regions are paired.</span></span>

<span data-ttu-id="b9dd8-115">Müşteriler, aynı işleri hem eşleştirilmiş bölgelere dağıtmak için önerilir.</span><span class="sxs-lookup"><span data-stu-id="b9dd8-115">Customers are advised to deploy identical jobs to both paired regions.</span></span> <span data-ttu-id="b9dd8-116">İzleme kapasiteleri iç Stream Analytics yanı sıra müşterileri de işleri izlemek için önerilir gibi **her ikisi de** üretim işler.</span><span class="sxs-lookup"><span data-stu-id="b9dd8-116">In addition to Stream Analytics internal monitoring capabilities, customers are also advised to monitor the jobs as if **both** are production jobs.</span></span> <span data-ttu-id="b9dd8-117">Stream Analytics Hizmet güncelleştirmesi sonucu olarak bir sonu tanımladıysanız, uygun şekilde İlerlet ve herhangi bir aşağı akış tüketiciye sağlıklı iş çıktısı için yük.</span><span class="sxs-lookup"><span data-stu-id="b9dd8-117">If a break is identified to be a result of the Stream Analytics service update, escalate appropriately and fail over any downstream consumers to the healthy job output.</span></span> <span data-ttu-id="b9dd8-118">Yükseltme desteklemek için yeni dağıtım tarafından etkilenen eşleştirilmiş bölge önlemek ve eşleştirilmiş işleri bütünlüğünü.</span><span class="sxs-lookup"><span data-stu-id="b9dd8-118">Escalation to support will prevent the paired region from being affected by the new deployment and maintain the integrity of the paired jobs.</span></span>
