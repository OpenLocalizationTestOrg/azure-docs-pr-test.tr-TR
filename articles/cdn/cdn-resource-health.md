---
title: "Azure CDN kaynakları aaaMonitor hello durumunu | Microsoft Docs"
description: "Nasıl toomonitor hello Azure kaynak durumu kullanarak Azure CDN kaynaklarınızın sistem durumunu öğrenin."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0a77e56d2fecae4bde6c83730c05375853a6638a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hello-health-of-azure-cdn-resources"></a><span data-ttu-id="61ae8-103">Azure CDN kaynakları Hello durumunu izleme</span><span class="sxs-lookup"><span data-stu-id="61ae8-103">Monitor hello health of Azure CDN resources</span></span>
  
<span data-ttu-id="61ae8-104">Azure CDN kaynak durumu olan bir alt kümesini [Azure kaynak durumu](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="61ae8-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="61ae8-105">Azure kaynak sistem durumu toomonitor hello CDN kaynakların durumunu kullanın ve tıklatılabilir Kılavuzu tootroubleshoot sorunları alırsınız.</span><span class="sxs-lookup"><span data-stu-id="61ae8-105">You can use Azure resource health toomonitor hello health of CDN resources and receive actionable guidance tootroubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="61ae8-106">Azure CDN kaynak durumu hello ve sistem durumu genel CDN teslim API özellikleri için yalnızca şu anda hesapları.</span><span class="sxs-lookup"><span data-stu-id="61ae8-106">Azure CDN resource health only currently accounts for hello health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="61ae8-107">Azure CDN kaynak durumu tek tek CDN uç noktası doğrulamaz.</span><span class="sxs-lookup"><span data-stu-id="61ae8-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="61ae8-108">Azure CDN kaynak durumu akışı hello sinyalleri too15 dakikada Gecikmeli olabilir.</span><span class="sxs-lookup"><span data-stu-id="61ae8-108">hello signals that feed Azure CDN resource health may be up too15 minutes delayed.</span></span>

## <a name="how-toofind-azure-cdn-resource-health"></a><span data-ttu-id="61ae8-109">Nasıl toofind Azure CDN kaynak durumu</span><span class="sxs-lookup"><span data-stu-id="61ae8-109">How toofind Azure CDN resource health</span></span>

1. <span data-ttu-id="61ae8-110">Merhaba, [Azure portal](https://portal.azure.com), tooyour CDN profili göz atın.</span><span class="sxs-lookup"><span data-stu-id="61ae8-110">In hello [Azure portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>

2. <span data-ttu-id="61ae8-111">Merhaba tıklatın **ayarları** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="61ae8-111">Click hello **Settings** button.</span></span>

    ![Ayarlar düğmesi](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="61ae8-113">Altında *destek + sorun giderme*, tıklatın **kaynak durumu**.</span><span class="sxs-lookup"><span data-stu-id="61ae8-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![CDN kaynak durumu](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="61ae8-115">Hello listelenen CDN kaynakları bulabileceğiniz *kaynak durumu* döşeme hello *Yardım + Destek* dikey.</span><span class="sxs-lookup"><span data-stu-id="61ae8-115">You can also find CDN resources listed in hello *Resource health* tile in hello *Help + support* blade.</span></span>  <span data-ttu-id="61ae8-116">Hızlı çok alabilirsiniz*Yardım + Destek* yuvarlak içine alınmıştır hello tıklayarak **?**</span><span class="sxs-lookup"><span data-stu-id="61ae8-116">You can quickly get too*Help + support* by clicking hello circled **?**</span></span> <span data-ttu-id="61ae8-117">Merhaba sağ üst köşedeki hello portalı.</span><span class="sxs-lookup"><span data-stu-id="61ae8-117">in hello upper right corner of hello portal.</span></span>
>
> ![Yardım + destek](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="61ae8-119">Azure CDN özgü iletileri</span><span class="sxs-lookup"><span data-stu-id="61ae8-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="61ae8-120">Aşağıda durumları ilgili tooAzure CDN kaynak durumu bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="61ae8-120">Statuses related tooAzure CDN resource health can be found below.</span></span>

|<span data-ttu-id="61ae8-121">İleti</span><span class="sxs-lookup"><span data-stu-id="61ae8-121">Message</span></span> | <span data-ttu-id="61ae8-122">Önerilen eylem</span><span class="sxs-lookup"><span data-stu-id="61ae8-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="61ae8-123">Durdurulmuş, kaldırıldı veya bir veya daha fazla CDN uç noktalarınızı yanlış</span><span class="sxs-lookup"><span data-stu-id="61ae8-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="61ae8-124">Durduruldu, kaldırıldı veya bir veya daha fazla CDN uç noktalarınızı yanlış.</span><span class="sxs-lookup"><span data-stu-id="61ae8-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="61ae8-125">Özür dileriz, hello CDN yönetim hizmeti şu anda kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="61ae8-125">We are sorry, hello CDN management service is currently unavailable</span></span> | <span data-ttu-id="61ae8-126">Geri durum güncelleştirmeleri için burayı tıklatın; Çözümleme süresi Hello beklenen sonra sorun devam ederse, desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="61ae8-126">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span>|
|<span data-ttu-id="61ae8-127">CDN uç noktalarınızı bazı bizim CDN sağlayıcıları ile devam eden sorunları tarafından etkilenebilir ne yazık ki</span><span class="sxs-lookup"><span data-stu-id="61ae8-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="61ae8-128">Geri durum güncelleştirmeleri için burayı tıklatın; Merhaba sorun giderme aracı toolearn kullanma tootest kaynağı ve CDN uç noktası; Çözümleme süresi Hello beklenen sonra sorun devam ederse, desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="61ae8-128">Check back here for status updates; Use hello Troubleshoot tool toolearn how tootest your origin and CDN endpoint; If your problem persists after hello expected resolution time, contact support.</span></span> |
|<span data-ttu-id="61ae8-129">CDN uç noktası yapılandırma değişikliklerini yayma gecikmeleri yaşıyor ne yazık ki</span><span class="sxs-lookup"><span data-stu-id="61ae8-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="61ae8-130">Geri durum güncelleştirmeleri için burayı tıklatın; Yapılandırma değişikliklerini tam olarak beklenen hello zamanında yayılmaz ederse Destek'e başvurun.</span><span class="sxs-lookup"><span data-stu-id="61ae8-130">Check back here for status updates; If your configuration changes are not fully propagated in hello expected time, contact support.</span></span>|
|<span data-ttu-id="61ae8-131">Biz hello ek portal yükleme sorunları yaşamaktadır ne yazık ki</span><span class="sxs-lookup"><span data-stu-id="61ae8-131">We're sorry, we are experiencing issues loading hello supplemental portal</span></span> | <span data-ttu-id="61ae8-132">Geri durum güncelleştirmeleri için burayı tıklatın; Çözümleme süresi Hello beklenen sonra sorun devam ederse, desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="61ae8-132">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span>|
<span data-ttu-id="61ae8-133">Üzgünüz, şu bizim CDN sağlayıcıları bazı sorunlar yaşıyoruz</span><span class="sxs-lookup"><span data-stu-id="61ae8-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="61ae8-134">Geri durum güncelleştirmeleri için burayı tıklatın; Çözümleme süresi Hello beklenen sonra sorun devam ederse, desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="61ae8-134">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="61ae8-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="61ae8-135">Next steps</span></span>

- [<span data-ttu-id="61ae8-136">Azure kaynak durumu genel bir bakış okuma</span><span class="sxs-lookup"><span data-stu-id="61ae8-136">Read an overview of Azure resource health</span></span>](../resource-health/resource-health-overview.md)
- [<span data-ttu-id="61ae8-137">CDN sıkıştırma ile ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="61ae8-137">Troubleshoot issues with CDN compression</span></span>](./cdn-troubleshoot-compression.md)
- [<span data-ttu-id="61ae8-138">404 hataları ile ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="61ae8-138">Troubleshoot issues with 404 errors</span></span>](./cdn-troubleshoot-endpoint.md)