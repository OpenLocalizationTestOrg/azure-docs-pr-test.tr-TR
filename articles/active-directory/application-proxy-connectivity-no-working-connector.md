---
title: "aaaNo çalışma bağlayıcı grubu için uygulama proxy'si uygulama bulundu | Microsoft Docs"
description: "Hiç çalışma bağlayıcı hello Azure AD uygulama proxy'si ile uygulamanız için bir bağlayıcı grubunda olduğunda, karşılaşabileceğiniz sorunları"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4c4baf296b316db131929c9a7c618fb9960713e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a><span data-ttu-id="b4cf7-103">Hiç çalışma bağlayıcı grubu için uygulama proxy'si uygulama bulunamadı</span><span class="sxs-lookup"><span data-stu-id="b4cf7-103">No working connector group found for an Application Proxy application</span></span>

<span data-ttu-id="b4cf7-104">Bu makale Yardım, tooresolve hello sık karşılaşılan sorunları için uygulama proxy'si uygulama algılanan bir bağlayıcı olmadığında karşılaştığı Azure Active Directory ile tümleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-104">This article help you tooresolve hello common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span></span>

## <a name="overview-of-steps"></a><span data-ttu-id="b4cf7-105">Adımlara genel bakış</span><span class="sxs-lookup"><span data-stu-id="b4cf7-105">Overview of steps</span></span>
<span data-ttu-id="b4cf7-106">Hiç çalışma uygulamanız için bir bağlayıcı grubundaki bağlayıcı ise, birkaç yolu tooresolve hello sorunu vardır:</span><span class="sxs-lookup"><span data-stu-id="b4cf7-106">If there is no working Connector in a Connector Group for your application, there are a few ways tooresolve hello problem:</span></span>

-   <span data-ttu-id="b4cf7-107">Bağlayıcılar hello grubunda varsa, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b4cf7-107">If you have no connectors in hello group, you can:</span></span>

    -   <span data-ttu-id="b4cf7-108">Merhaba sağ şirket içi sunucuda yeni bir bağlayıcı indirin ve toothis grubu atama</span><span class="sxs-lookup"><span data-stu-id="b4cf7-108">Download a new Connector on hello right on-prem server, and assign it toothis group</span></span>

    -   <span data-ttu-id="b4cf7-109">Etkin bir bağlayıcı hello grubuna taşıyın</span><span class="sxs-lookup"><span data-stu-id="b4cf7-109">Move an active Connector into hello group</span></span>

-   <span data-ttu-id="b4cf7-110">Merhaba grubunda active bağlayıcılar varsa, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b4cf7-110">If you have no active connectors in hello group, you can:</span></span>

    -   <span data-ttu-id="b4cf7-111">Merhaba neden Bağlayıcınızı etkin değil tanımlama ve giderme</span><span class="sxs-lookup"><span data-stu-id="b4cf7-111">Identify hello reason your Connector is inactive and resolve</span></span>

    -   <span data-ttu-id="b4cf7-112">Etkin bir bağlayıcı hello grubuna taşıyın</span><span class="sxs-lookup"><span data-stu-id="b4cf7-112">Move an active Connector into hello group</span></span>

<span data-ttu-id="b4cf7-113">olan bu hello sorunu tooknow uygulamanızda hello "Uygulama proxy'si" menüsünü açın ve hello bağlayıcı Grup uyarı iletisini arayın.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-113">tooknow which of these is hello issue, open hello “Application Proxy” menu in your Application, and look at hello Connector Group warning message.</span></span> <span data-ttu-id="b4cf7-114">Bunu o hello grubun en az bir bağlayıcı (hiçbiri hello grubunda olması) gerekiyor veya (büyük olasılıkla etkin olmayan bağlayıcılar elinizde rağmen) etkin bağlayıcılar olduğunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-114">It specify either that hello group needs at least one Connector (you have none in hello group) or that it has no active Connectors (though you likely have inactive Connectors).</span></span>

   ![Azure Portalı'nda bağlayıcı Grup Seçimi](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

<span data-ttu-id="b4cf7-116">Bu seçeneklerin her biri hakkında daha fazla bilgi için hello karşılık gelen bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-116">For details on each of these options, see hello corresponding section below.</span></span> <span data-ttu-id="b4cf7-117">Bunların her biri hello bağlayıcı yönetim sayfasından başlayarak olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-117">Each of these assumes that you are starting from hello Connector management page.</span></span> <span data-ttu-id="b4cf7-118">Merhaba hata ileti yukarıdaki arıyorsanız, hello uyarı iletisi tıklayarak toothis sayfasına gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-118">If you are looking at hello error message above, you can go toothis page by clicking on hello warning message.</span></span> <span data-ttu-id="b4cf7-119">Aksi takdirde bu çok giderek bulunabilir**Azure Active Directory**, üzerinde tıklatmak **kurumsal uygulamalar**, ardından **uygulama proxy'si.**</span><span class="sxs-lookup"><span data-stu-id="b4cf7-119">Otherwise this can be found by going too**Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span></span>

   ![Azure Portalı'nda bağlayıcı Grup Yönetimi](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a><span data-ttu-id="b4cf7-121">Yeni bir bağlayıcı indirin</span><span class="sxs-lookup"><span data-stu-id="b4cf7-121">Download a new Connector</span></span>

<span data-ttu-id="b4cf7-122">toodownload yeni bir bağlayıcı hello hello sayfanın başında hello "Bağlayıcısı'nı indir" düğmesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-122">toodownload a new Connector, use hello “Download Connector” button at hello top of hello page.</span></span>

<span data-ttu-id="b4cf7-123">toobe doğrudan görüş toohello arka uç uygulaması olan bir makinede yüklü ve genellikle yerleştirildiği Not hello bağlayıcı gereksinimlerini Merhaba uygulaması aynı sunucuya hello.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-123">note hello Connector needs toobe installed on a machine with direct line of sight toohello backend application, and is typically placed on hello same server as hello application.</span></span> <span data-ttu-id="b4cf7-124">Merhaba bağlayıcı indirdikten sonra bu menüsünde görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-124">After downloading, hello Connector should appear in this menu.</span></span> <span data-ttu-id="b4cf7-125">Merhaba Connector'ı tıklatın ve hello "Bağlayıcı grubu" açılan toomake toohello sağ grubuna ait olduğundan emin kullanın.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-125">click hello Connector, and use hello “Connector Group” drop-down toomake sure it belongs toohello right group.</span></span> <span data-ttu-id="b4cf7-126">Merhaba değişikliği kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-126">Save hello change.</span></span>

   ![Merhaba bağlayıcı hello Azure Portalı ' indirin](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a><span data-ttu-id="b4cf7-128">Etkin bir Bağlayıcıyı taşıma</span><span class="sxs-lookup"><span data-stu-id="b4cf7-128">Move an Active Connector</span></span>

<span data-ttu-id="b4cf7-129">Toohello grubuna ait olması gerekir ve görüş toohello hedef arka uç uygulaması olan bir active bağlayıcısı varsa, atanan hello grubuna hello bağlayıcı taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-129">If you have an active Connector that should belong toohello group and has line of sight toohello target backend application, you can move hello Connector into hello assigned group.</span></span> <span data-ttu-id="b4cf7-130">toodo, bu nedenle, hello bağlayıcı tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-130">toodo so, click hello Connector.</span></span> <span data-ttu-id="b4cf7-131">Merhaba "Bağlayıcı grubu" alanında hello açılan tooselect hello doğru Grup kullanın ve Kaydet'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-131">In hello “Connector Group” field, use hello drop-down tooselect hello correct group, and click Save.</span></span>

## <a name="resolve-an-inactive-connector"></a><span data-ttu-id="b4cf7-132">Etkin olmayan bir bağlayıcı çözümleyin</span><span class="sxs-lookup"><span data-stu-id="b4cf7-132">Resolve an inactive Connector</span></span>

<span data-ttu-id="b4cf7-133">Bağlayıcılar hello grubundaki etkin olmayan yalnızca hello olmayan bir makineye büyük olasılıkla olmaları durumunda tüm hello gerekli bağlantı noktaları engeli kaldırılmış.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-133">If hello only Connectors in hello group are inactive, they are likely on a machine that does not have all hello necessary ports unblocked.</span></span>

<span data-ttu-id="b4cf7-134">Başlangıç noktaları Bkz: Bu sorunu araştırmaya ile ilgili ayrıntılar için sorun giderme belgesi.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-134">see hello ports Troubleshoot document for details on investigating this problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4cf7-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b4cf7-135">Next steps</span></span>
[<span data-ttu-id="b4cf7-136">Azure AD uygulama proxy'si bağlayıcılar anlama</span><span class="sxs-lookup"><span data-stu-id="b4cf7-136">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)


