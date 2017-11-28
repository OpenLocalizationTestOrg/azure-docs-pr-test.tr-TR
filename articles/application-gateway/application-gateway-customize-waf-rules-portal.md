---
title: "aaaCustomize web uygulaması güvenlik duvarı kuralları Azure uygulama ağ geçidi - Azure portalı | Microsoft Docs"
description: "Bu makalede, nasıl toocustomize web uygulaması güvenlik duvarı uygulama ağ geçidi'nde hello Azure portal ile kurallar hakkında bilgi sağlar."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 1159500b-17ba-41e7-88d6-b96986795084
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: gwallace
ms.openlocfilehash: 36a999279e0370b9f803e12257856a56753b23a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="da201-103">Web uygulaması güvenlik duvarı kuralları hello Azure portal aracılığıyla özelleştirme</span><span class="sxs-lookup"><span data-stu-id="da201-103">Customize web application firewall rules through hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="da201-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="da201-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="da201-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="da201-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="da201-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="da201-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="da201-107">Hello Azure uygulama ağ geçidi web uygulaması Güvenlik Duvarı (WAF) web uygulamaları için koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="da201-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="da201-108">Bu korumalar hello açık Web uygulaması güvenlik proje (OWASP) çekirdek kuralı ayarlayın (CR) tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="da201-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="da201-109">Bazı kurallar hatalı pozitif sonuç neden ve gerçek trafiği engelle.</span><span class="sxs-lookup"><span data-stu-id="da201-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="da201-110">Bu nedenle, uygulama ağ geçidi hello yetenek toocustomize Kural gruplarını ve kurallarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="da201-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="da201-111">Merhaba belirli kuralı grupları ve kuralları hakkında daha fazla bilgi için bkz: [web uygulaması güvenlik duvarı CRS Kural gruplarını ve kurallarını listesi](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="da201-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

>[!NOTE]
> <span data-ttu-id="da201-112">Uygulama ağ geçidiniz hello WAF katmanı kullanmıyorsa hello seçeneği tooupgrade hello uygulama ağ geçidi toohello WAF katmanı hello sağ bölmede görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="da201-112">If your application gateway is not using hello WAF tier, hello option tooupgrade hello application gateway toohello WAF tier appears in hello right pane.</span></span> 

![WAF etkinleştir][fig1]

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="da201-114">Görünüm kural gruplar ve kurallar</span><span class="sxs-lookup"><span data-stu-id="da201-114">View rule groups and rules</span></span>

<span data-ttu-id="da201-115">**tooview kural gruplar ve kurallar**</span><span class="sxs-lookup"><span data-stu-id="da201-115">**tooview rule groups and rules**</span></span>
   1. <span data-ttu-id="da201-116">Toohello uygulama ağ geçidi göz atın ve ardından **Web uygulaması güvenlik duvarı**.</span><span class="sxs-lookup"><span data-stu-id="da201-116">Browse toohello application gateway, and then select **Web application firewall**.</span></span>  
   2. <span data-ttu-id="da201-117">Seçin **Gelişmiş kural yapılandırmasını**.</span><span class="sxs-lookup"><span data-stu-id="da201-117">Select **Advanced rule configuration**.</span></span>  
   <span data-ttu-id="da201-118">Bu görünüm, kural kümesi seçilen hello ile sağlanan tüm hello Kural gruplarını hello sayfasında bir tablo gösterir.</span><span class="sxs-lookup"><span data-stu-id="da201-118">This view shows a table on hello page of all hello rule groups provided with hello chosen rule set.</span></span> <span data-ttu-id="da201-119">Tüm hello kuralın onay kutularını seçilir.</span><span class="sxs-lookup"><span data-stu-id="da201-119">All of hello rule's check boxes are selected.</span></span>

![Devre dışı kurallarını yapılandırma][1]

## <a name="search-for-rules-toodisable"></a><span data-ttu-id="da201-121">Kuralları toodisable arayın</span><span class="sxs-lookup"><span data-stu-id="da201-121">Search for rules toodisable</span></span>

<span data-ttu-id="da201-122">Merhaba **Web uygulaması güvenlik duvarı ayarlarını** dikey metin arama toofilter hello kurallarla hello yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="da201-122">hello **Web application firewall settings** blade provides hello capability toofilter hello rules through a text search.</span></span> <span data-ttu-id="da201-123">Hello sonucu yalnızca hello kuralı grupları ve aradığınız hello metin içeren kurallarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="da201-123">hello result displays only hello rule groups and rules that contain hello text you searched for.</span></span>

![Kuralları arayın][2]

## <a name="disable-rule-groups-and-rules"></a><span data-ttu-id="da201-125">Kural gruplarını ve kurallarını devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="da201-125">Disable rule groups and rules</span></span>

<span data-ttu-id="da201-126">Olduğunda, olduğunuz kuralları devre dışı bırakma, tüm kural grubu veya bir veya daha fazla kural grubu altında belirli kurallar devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da201-126">When your're disabling rules, you can disable an entire rule group or specific rules under one or more rule groups.</span></span> 

<span data-ttu-id="da201-127">**toodisable kuralı grupları veya belirli kurallar**</span><span class="sxs-lookup"><span data-stu-id="da201-127">**toodisable rule groups or specific rules**</span></span>

   1. <span data-ttu-id="da201-128">Merhaba kuralları veya toodisable istediğiniz kuralı grupları arayın.</span><span class="sxs-lookup"><span data-stu-id="da201-128">Search for hello rules or rule groups that you want toodisable.</span></span>
   2. <span data-ttu-id="da201-129">Merhaba toodisable istediğiniz kuralları için hello onay kutularını temizleyin.</span><span class="sxs-lookup"><span data-stu-id="da201-129">Clear hello check boxes for hello rules that you want toodisable.</span></span> 
   2. <span data-ttu-id="da201-130">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="da201-130">Select **Save**.</span></span> 

![Değişiklikleri Kaydet][3]

## <a name="next-steps"></a><span data-ttu-id="da201-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="da201-132">Next steps</span></span>

<span data-ttu-id="da201-133">Devre dışı kurallarınızı yapılandırdıktan sonra öğrenebilirsiniz nasıl tooview WAF günlüklerinizi.</span><span class="sxs-lookup"><span data-stu-id="da201-133">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="da201-134">Daha fazla bilgi için bkz: [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="da201-134">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
