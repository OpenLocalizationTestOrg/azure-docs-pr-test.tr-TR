---
title: "Azure Application Gateway’de uçtan uca SSL’yi etkinleştirme | Microsoft Docs"
description: "Bu sayfada, Application Gateway uçtan uca SSL desteği için genel bir bakış sunulmuştur."
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
ms.openlocfilehash: 689ee54dc1db2ea371b08270718278fd98c65bb5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-end-to-end-ssl-with-application-gateway"></a><span data-ttu-id="425ad-103">Application Gateway ile uçtan uca SSL’ye genel bakış</span><span class="sxs-lookup"><span data-stu-id="425ad-103">Overview of end to end SSL with Application Gateway</span></span>

<span data-ttu-id="425ad-104">Application Gateway, ağ geçidinde SSL sonlandırmasını destekler. Bu sonlandırmanın ardından, trafik genelde arka uç sunucularına şifrelenmemiş olarak akar.</span><span class="sxs-lookup"><span data-stu-id="425ad-104">Application gateway supports SSL termination at the gateway, after which traffic typically flows unencrypted to the backend servers.</span></span> <span data-ttu-id="425ad-105">Bu özellik, web sunucularının maliyetli şifreleme ve şifre çözme ek yükünden kurtulmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="425ad-105">This feature allows web servers to be unburdened from costly encryption and decryption overhead.</span></span> <span data-ttu-id="425ad-106">Ancak arka uç sunucularıyla şifrelenmemiş iletişim, bazı müşteriler için kabul edilebilir bir seçenek değildir.</span><span class="sxs-lookup"><span data-stu-id="425ad-106">However for some customers unencrypted communication to the backend servers is not an acceptable option.</span></span> <span data-ttu-id="425ad-107">Bunun şifrelenmemiş iletişimin nedeni, güvenlik gereksinimleri, uyumluluk gereksinimleri veya uygulamanın yalnızca güvenli bağlantı kabul etmesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="425ad-107">This unencrypted communication could be due to security requirements, compliance requirements, or the application may only accept a secure connection.</span></span> <span data-ttu-id="425ad-108">Application Gateway, böyle uygulamalar için uçtan uca SSL şifrelemesini desteklemektedir.</span><span class="sxs-lookup"><span data-stu-id="425ad-108">For such applications, application gateway supports end to end SSL encryption.</span></span>

## <a name="overview"></a><span data-ttu-id="425ad-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="425ad-109">Overview</span></span>

<span data-ttu-id="425ad-110">Uçtan uca SSL, gizli verileri arka uca şifrelenmiş olarak güvenli bir şekilde aktarmanızı sağlar ve bu sırada Application Gateway'in sunduğu 7. Katman yük dengeleme özelliklerinin avantajlarından yararlanmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="425ad-110">End to end SSL allows you to securely transmit sensitive data to the backend encrypted while still taking advantage of the benefits of Layer 7 load balancing features which application gateway provides.</span></span> <span data-ttu-id="425ad-111">Bu özelliklerin bazıları tanımlama bilgisi temelli oturum benzeşimi, URL tabanlı yönlendirme, sitelere göre yönlendirme desteği veya X-Forwarded-* üst bilgilerini ekleyebilmedir.</span><span class="sxs-lookup"><span data-stu-id="425ad-111">Some of these features are cookie-based session affinity, URL-based routing, support for routing based on sites, or ability to inject X-Forwarded-* headers.</span></span>

<span data-ttu-id="425ad-112">Application Gateway uçtan uca SSL iletişimi modu ile yapılandırıldığında, ağ geçidindeki SSL oturumlarını sonlandırır ve kullanıcı trafiğinin şifresini çözer.</span><span class="sxs-lookup"><span data-stu-id="425ad-112">When configured with end to end SSL communication mode, application gateway terminates the SSL sessions at the gateway and decrypts user traffic.</span></span> <span data-ttu-id="425ad-113">Ardından trafiğin yönlendirileceği uygun arka uç havuzunu seçmek için yapılandırılan kuralları uygular.</span><span class="sxs-lookup"><span data-stu-id="425ad-113">It then applies the configured rules to select an appropriate backend pool instance to route traffic to.</span></span> <span data-ttu-id="425ad-114">Ardından Application Gateway, arka uç sunucusuyla yeni bir SSL bağlantısı başlatır ve isteği arka uca aktarmadan önce arka uç sunucusunun ortak anahtar sertifikasını kullanarak verileri yeniden şifreler.</span><span class="sxs-lookup"><span data-stu-id="425ad-114">Application gateway then initiates a new SSL connection to the backend server and re-encrypts data using the backend server's public key certificate before transmitting the request to the backend.</span></span> <span data-ttu-id="425ad-115">Uçtan uca SSL, BackendHTTPSetting’de protokol ayarı HTTPS yapılarak etkinleştirilir. Bu ayar, daha sonra arka uç havuzuna uygulanır.</span><span class="sxs-lookup"><span data-stu-id="425ad-115">End to end SSL is enabled by setting protocol setting in BackendHTTPSetting to HTTPS, which is then applied to a backend pool.</span></span> <span data-ttu-id="425ad-116">Arka uç sunucusunda uçtan uca SSL’nin etkin olduğu her arka uç sunucusunun, güvenli iletişime izin veren bir sertifikayla yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="425ad-116">Each backend server in the backend pool with end to end SSL enabled must be configured with a certificate to allow secure communication.</span></span>

![uçtan uca SSL senaryosu][1]

<span data-ttu-id="425ad-118">Bu örnekte, TLS1.2 kullanan istekler, uçtan uca SSL kullanılarak Pool1'deki sunuculara yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="425ad-118">In this example, requests using TLS1.2 are routed to backend servers in Pool1 using end to end SSL.</span></span>

## <a name="end-to-end-ssl-and-whitelisting-of-certificates"></a><span data-ttu-id="425ad-119">Uçtan uca SSL ve sertifikaların güvenilir listeye alınması</span><span class="sxs-lookup"><span data-stu-id="425ad-119">End to end SSL and whitelisting of certificates</span></span>

<span data-ttu-id="425ad-120">Uygulama ağ geçidi, yalnızca sertifikalarını uygulama ağ geçidiyle güvenilir listeye aldırmış, bilinen arka uç örnekleriyle iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="425ad-120">Application gateway only communicates with known backend instances that have whitelisted their certificate with the application gateway.</span></span> <span data-ttu-id="425ad-121">Sertifikaların güvenilir listeye alınmasını etkinleştirmek için, arka uç sunucusu sertifikalarının ortak anahtarlarını uygulama ağ geçidine (kök sertifika değil) yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="425ad-121">To enable whitelisting of certificates, you must upload the public key of backend server certificates to the application gateway (not the root certificate).</span></span> <span data-ttu-id="425ad-122">Bunun ardından, yalnızca bilinen ve güvenilir listeye alınmış arka uçlara yönelik bağlantılara izin verilir.</span><span class="sxs-lookup"><span data-stu-id="425ad-122">Only connections to known and whitelisted backends are then allowed.</span></span> <span data-ttu-id="425ad-123">Geriye kalan arka uçlar, ağ geçidi hatasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="425ad-123">The remaining backends results in a gateway error.</span></span> <span data-ttu-id="425ad-124">Otomatik olarak imzalanan sertifikalar, yalnızca test amaçlarına yöneliktir ve üretim iş yükleri için önerilmez.</span><span class="sxs-lookup"><span data-stu-id="425ad-124">Self-signed certificates are for test purposes only and not recommended for production workloads.</span></span> <span data-ttu-id="425ad-125">Bunun gibi sertifikaların kullanılabilmesi için, önceki adımlarda açıklandığı şekilde uygulama ağ geçidiyle güvenilir listeye alınmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="425ad-125">Such certificates have to be whitelisted with the application gateway as described in the preceding steps before they can be used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="425ad-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="425ad-126">Next steps</span></span>

<span data-ttu-id="425ad-127">Uçtan uca SSL hakkında bilgi edindikten sonra uçtan uca SSL kullanan uygulama ağ geçidi oluşturmak için [Uygulama ağ geçidinde uçtan uca SSL'yi etkinleştirme](application-gateway-end-to-end-ssl-powershell.md) bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="425ad-127">After learning about end to end SSL, go to [enable end to end SSL on application gateway](application-gateway-end-to-end-ssl-powershell.md) to create an application gateway using end to end SSL.</span></span>

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
