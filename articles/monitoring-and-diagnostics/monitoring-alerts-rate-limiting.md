---
title: "SMS, e-postalar ve Web kancalarını aaaRate sınırlama | Microsoft Docs"
description: "Azure olası SMS, e-posta veya Web kancası bildirimleri bir eylem grubundan hello sayısını nasıl sınırlar anlayın."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 1cd08a5b982c82bb02e0bf93451aa1fcd9bc34af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a><span data-ttu-id="2f452-103">SMS iletileri, e-postalar ve Web kancası için gönderileri sınırlama oranı</span><span class="sxs-lookup"><span data-stu-id="2f452-103">Rate limiting for SMS messages, emails, and webhook posts</span></span>
<span data-ttu-id="2f452-104">Hız sınırlaması tooa belirli telefon numarası veya e-posta adresi çok fazla bildirimler gönderildiğinde oluşan bildirimleri ertelenmesi olur.</span><span class="sxs-lookup"><span data-stu-id="2f452-104">Rate limiting is a suspension of notifications that occurs when too many notifications are sent tooa particular phone number or email address.</span></span> <span data-ttu-id="2f452-105">Hız sınırlaması uyarıları yönetilebilir ve kullanılabilir olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="2f452-105">Rate limiting ensures that alerts are manageable and actionable.</span></span>

<span data-ttu-id="2f452-106">SMS ve e-posta için hello kuralları aynı hello.</span><span class="sxs-lookup"><span data-stu-id="2f452-106">hello rules for SMS and email are hello same.</span></span> <span data-ttu-id="2f452-107">Merhaba hızı sınırı eşik ise:</span><span class="sxs-lookup"><span data-stu-id="2f452-107">hello rate limit threshold is:</span></span>

 - <span data-ttu-id="2f452-108">**SMS**: bir saat içinde 10 iletileri.</span><span class="sxs-lookup"><span data-stu-id="2f452-108">**SMS**: 10 messages in an hour.</span></span>
 - <span data-ttu-id="2f452-109">**E-posta**: 100 iletileri bir saat içinde.</span><span class="sxs-lookup"><span data-stu-id="2f452-109">**Email**: 100 messages in an hour.</span></span>

## <a name="rate-limit-rules"></a><span data-ttu-id="2f452-110">Hızı sınırı kuralları</span><span class="sxs-lookup"><span data-stu-id="2f452-110">Rate limit rules</span></span>
- <span data-ttu-id="2f452-111">Belirli bir telefon numarası veya e-posta hello eşik izin verdiğinden daha fazla ileti aldığında sınırlı hızıdır.</span><span class="sxs-lookup"><span data-stu-id="2f452-111">A particular phone number or email is rate limited when it receives more messages than hello threshold allows.</span></span>
- <span data-ttu-id="2f452-112">Bir telefon numarası veya e-posta çok sayıda abonelikleri eylem gruplarının bir parçası olabilir.</span><span class="sxs-lookup"><span data-stu-id="2f452-112">A phone number or email can be part of action groups across many subscriptions.</span></span> <span data-ttu-id="2f452-113">Hız sınırlaması abonelikler arasında geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="2f452-113">Rate limiting applies across all subscriptions.</span></span> <span data-ttu-id="2f452-114">Merhaba eşiğe hemen birden çok aboneliklerden gönderilen iletileri olsa bile geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="2f452-114">It applies as soon as hello threshold is reached, even if messages are sent from multiple subscriptions.</span></span>  
- <span data-ttu-id="2f452-115">Bir telefon numarası veya e-posta oranı sınırlı olduğunda, başka bir bildirim toocommunicate gönderilir hız sınırlaması hello.</span><span class="sxs-lookup"><span data-stu-id="2f452-115">When a phone number or email is rate limited, an additional notification is sent toocommunicate hello rate limiting.</span></span> <span data-ttu-id="2f452-116">Merhaba durumları hello zaman sınırlaması oranı bildirim süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="2f452-116">hello notification states when hello rate limiting expires.</span></span>

## <a name="rate-limit-of-webhooks"></a><span data-ttu-id="2f452-117">Web kancası hızı sınırı</span><span class="sxs-lookup"><span data-stu-id="2f452-117">Rate limit of webhooks</span></span> ##
<span data-ttu-id="2f452-118">Web kancası için yerinde sınırlama kuru yoktur.</span><span class="sxs-lookup"><span data-stu-id="2f452-118">There is no rate limiting in place for webhooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f452-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2f452-119">Next steps</span></span> ##
* <span data-ttu-id="2f452-120">Daha fazla bilgi edinmek [SMS uyarı davranış](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="2f452-120">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>
* <span data-ttu-id="2f452-121">Alma bir [etkinlik günlüğü uyarıları genel bakış](monitoring-overview-alerts.md)ve öğrenin nasıl tooreceive uyarıları.</span><span class="sxs-lookup"><span data-stu-id="2f452-121">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span>  
* <span data-ttu-id="2f452-122">Nasıl çok öğrenin[hizmeti sistem durumu bildirimi gönderilen her uyarıları yapılandırmak](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="2f452-122">Learn how too[configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
