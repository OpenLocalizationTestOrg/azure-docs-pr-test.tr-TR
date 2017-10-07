---
title: "aaaEnabling son tooend Azure uygulama ağ geçidi SSL | Microsoft Docs"
description: "Bu sayfa SSL desteği hello uygulama ağ geçidi son tooend genel bir bakış sağlar."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 3976399b-25ad-45eb-8eb3-fdb736a598c5
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: amsriva
ms.openlocfilehash: c5cb398a1e7d9a08662a3120baad98edb5575917
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-end-tooend-ssl-with-application-gateway"></a><span data-ttu-id="2bac3-103">Son tooend SSL ile uygulama ağ geçidi'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="2bac3-103">Overview of end tooend SSL with Application Gateway</span></span>

<span data-ttu-id="2bac3-104">Hangi trafik genellikle akar toohello arka uç sunucularına şifrelenmemiş sonra uygulama ağ geçidi hello ağ geçidi, SSL sonlandırmanın destekler.</span><span class="sxs-lookup"><span data-stu-id="2bac3-104">Application gateway supports SSL termination at hello gateway, after which traffic typically flows unencrypted toohello backend servers.</span></span> <span data-ttu-id="2bac3-105">Bu özellik web sunucuları toobe maliyetli şifreleme ve şifre çözme yükünü unburdened sağlar.</span><span class="sxs-lookup"><span data-stu-id="2bac3-105">This feature allows web servers toobe unburdened from costly encryption and decryption overhead.</span></span> <span data-ttu-id="2bac3-106">Ancak bazı müşteriler için şifrelenmemiş iletişimi toohello arka uç sunucularına bir kabul edilebilir seçenek değil.</span><span class="sxs-lookup"><span data-stu-id="2bac3-106">However for some customers unencrypted communication toohello backend servers is not an acceptable option.</span></span> <span data-ttu-id="2bac3-107">Merhaba uygulaması yalnızca güvenli bir bağlantı kabul edebilir veya bu şifrelenmemiş iletişim uyumluluk gereksinimleri, toosecurity gereksinimleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="2bac3-107">This unencrypted communication could be due toosecurity requirements, compliance requirements, or hello application may only accept a secure connection.</span></span> <span data-ttu-id="2bac3-108">Bu tür uygulamalar için uygulama ağ geçidi son tooend SSL destekleyen şifreleme.</span><span class="sxs-lookup"><span data-stu-id="2bac3-108">For such applications, application gateway supports end tooend SSL encryption.</span></span>

## <a name="overview"></a><span data-ttu-id="2bac3-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2bac3-109">Overview</span></span>

<span data-ttu-id="2bac3-110">Son tooend SSL verir toosecurely iletme hassas verileri toohello arka uç hala katman 7 Yük Dengeleme Özellikleri hello yararları hangi uygulama ağ geçidi yararlanarak sağlarken şifrelenmiş.</span><span class="sxs-lookup"><span data-stu-id="2bac3-110">End tooend SSL allows you toosecurely transmit sensitive data toohello backend encrypted while still taking advantage of hello benefits of Layer 7 load balancing features which application gateway provides.</span></span> <span data-ttu-id="2bac3-111">Yönlendirme siteleri veya özelliği tooinject - iletilen - X göre için tanımlama bilgisi tabanlı oturum benzeşimi, URL tabanlı yönlendirme, destek bu özelliklerden bazıları şunlardır * üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="2bac3-111">Some of these features are cookie-based session affinity, URL-based routing, support for routing based on sites, or ability tooinject X-Forwarded-* headers.</span></span>

<span data-ttu-id="2bac3-112">Son tooend SSL iletişimi modu ile yapılandırıldığında, uygulama ağ geçidi hello SSL oturumları hello ağ geçidinde sonlandırır ve kullanıcı trafiğinin şifresini çözer.</span><span class="sxs-lookup"><span data-stu-id="2bac3-112">When configured with end tooend SSL communication mode, application gateway terminates hello SSL sessions at hello gateway and decrypts user traffic.</span></span> <span data-ttu-id="2bac3-113">Ardından yapılandırılmış hello kuralları tooselect bir uygun arka uç havuzu örnek tooroute trafiği için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="2bac3-113">It then applies hello configured rules tooselect an appropriate backend pool instance tooroute traffic to.</span></span> <span data-ttu-id="2bac3-114">Uygulama ağ geçidi, ardından yeni bir SSL bağlantısı toohello arka uç sunucu başlatır ve veri hello isteği toohello arka uç iletmeden önce hello arka uç sunucunun ortak anahtar sertifikası kullanılarak yeniden şifreler.</span><span class="sxs-lookup"><span data-stu-id="2bac3-114">Application gateway then initiates a new SSL connection toohello backend server and re-encrypts data using hello backend server's public key certificate before transmitting hello request toohello backend.</span></span> <span data-ttu-id="2bac3-115">SSL protokolünü ise BackendHTTPSetting tooHTTPS ayarlayarak etkin uç tooend tooa arka uç havuzu uygulanır.</span><span class="sxs-lookup"><span data-stu-id="2bac3-115">End tooend SSL is enabled by setting protocol setting in BackendHTTPSetting tooHTTPS, which is then applied tooa backend pool.</span></span> <span data-ttu-id="2bac3-116">SSL etkin uç tooend ile Merhaba arka uç havuzundaki her arka uç sunucu sertifikası tooallow güvenli bir bağlantı ile yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2bac3-116">Each backend server in hello backend pool with end tooend SSL enabled must be configured with a certificate tooallow secure communication.</span></span>

![Son tooend ssl senaryosu][1]

<span data-ttu-id="2bac3-118">Bu örnekte, TLS1.2 kullanan isteklerinin son tooend SSL kullanarak yönlendirilmiş toobackend Pool1 sunucularıdır.</span><span class="sxs-lookup"><span data-stu-id="2bac3-118">In this example, requests using TLS1.2 are routed toobackend servers in Pool1 using end tooend SSL.</span></span>

## <a name="end-tooend-ssl-and-whitelisting-of-certificates"></a><span data-ttu-id="2bac3-119">Tooend SSL ve uygulamaları güvenilir listeye almayı sertifikaların bitiş</span><span class="sxs-lookup"><span data-stu-id="2bac3-119">End tooend SSL and whitelisting of certificates</span></span>

<span data-ttu-id="2bac3-120">Uygulama ağ geçidi, yalnızca kendi sertifika hello uygulama ağ geçidi ile Güvenilenler listesine sahip bilinen arka uç örnekleri ile iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="2bac3-120">Application gateway only communicates with known backend instances that have whitelisted their certificate with hello application gateway.</span></span> <span data-ttu-id="2bac3-121">tooenable uygulamaları güvenilir listeye almayı sertifikaların, arka uç sunucu sertifikaları toohello uygulama ağ geçidi (Merhaba kök sertifikanın değil) ortak anahtarı hello yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2bac3-121">tooenable whitelisting of certificates, you must upload hello public key of backend server certificates toohello application gateway (not hello root certificate).</span></span> <span data-ttu-id="2bac3-122">Yalnızca bağlantıları tooknown ve Güvenilenler listesine arka uçlarını sonra izin verilir.</span><span class="sxs-lookup"><span data-stu-id="2bac3-122">Only connections tooknown and whitelisted backends are then allowed.</span></span> <span data-ttu-id="2bac3-123">arka uçlarını kalan hello bir ağ geçidi hatayla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="2bac3-123">hello remaining backends results in a gateway error.</span></span> <span data-ttu-id="2bac3-124">Otomatik olarak imzalanan sertifikalar, yalnızca test amaçlarına yöneliktir ve üretim iş yükleri için önerilmez.</span><span class="sxs-lookup"><span data-stu-id="2bac3-124">Self-signed certificates are for test purposes only and not recommended for production workloads.</span></span> <span data-ttu-id="2bac3-125">Bu tür sertifikaların kullanılabilmesi için önce adımları önceki hello açıklandığı gibi hello uygulama ağ geçidi ile toobe Güvenilenler listesine vardır.</span><span class="sxs-lookup"><span data-stu-id="2bac3-125">Such certificates have toobe whitelisted with hello application gateway as described in hello preceding steps before they can be used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bac3-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2bac3-126">Next steps</span></span>

<span data-ttu-id="2bac3-127">Son tooend SSL hakkında daha fazla bilgi sonra çok gidin[uygulama ağ geçidi üzerinde son tooend SSL etkinleştirmek](application-gateway-end-to-end-ssl-powershell.md) kullanarak bir uygulama ağ geçidi toocreate tooend SSL bitmelidir.</span><span class="sxs-lookup"><span data-stu-id="2bac3-127">After learning about end tooend SSL, go too[enable end tooend SSL on application gateway](application-gateway-end-to-end-ssl-powershell.md) toocreate an application gateway using end tooend SSL.</span></span>

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
