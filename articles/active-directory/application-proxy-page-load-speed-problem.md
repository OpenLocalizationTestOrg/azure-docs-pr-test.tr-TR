---
title: "Uygulama proxy'si uygulama aaaAn çok uzun tooload alır | Microsoft Docs"
description: "Hello Azure AD uygulama proxy'si sayfa yükleme performans sorunlarını giderme"
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
ms.openlocfilehash: 4c7a51f96840966a1d88933fa4e30f39479d8a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="an-application-proxy-application-takes-too-long-tooload"></a><span data-ttu-id="46a2b-103">Uygulama proxy'si uygulamanın çok uzun tooload alır</span><span class="sxs-lookup"><span data-stu-id="46a2b-103">An Application Proxy application takes too long tooload</span></span>

<span data-ttu-id="46a2b-104">Bu makale neden bir Azure AD uygulama proxy'si uygulama sürebilir uzun süre tooload ve ne toounderstand yardımcı bu sorunu tooresolve yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46a2b-104">This article help you toounderstand why an Azure AD Application Proxy application may take a long time tooload, and what you can do tooresolve this issue.</span></span>

## <a name="overview"></a><span data-ttu-id="46a2b-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="46a2b-105">Overview</span></span>
<span data-ttu-id="46a2b-106">Uygulamalarınızı çalışıyoruz ancak uzun bir gecikme bkz, ağ topolojinizi tooimprove hello hızını göz önünde bulundurabilirsiniz bazı küçük tweaks olabilir.</span><span class="sxs-lookup"><span data-stu-id="46a2b-106">If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider tooimprove hello speed.</span></span> <span data-ttu-id="46a2b-107">Hello farklı topolojilerinin değerlendirme için bkz: [ağ konuları belge](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span><span class="sxs-lookup"><span data-stu-id="46a2b-107">For an evaluation of different topologies, see hello [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span></span>

<span data-ttu-id="46a2b-108">Bu konuları yardımcı olmuyorsa, biz ne yazık ki şu anda yoksa performans ayarlaması için diğer öneriler.</span><span class="sxs-lookup"><span data-stu-id="46a2b-108">If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning.</span></span> <span data-ttu-id="46a2b-109">Merhaba uygulama proxy'si hizmeti daha yakından tooyou olabilir toomore veri merkezleri genişletir gibi geliştirilmiş toosee gecikme doğrudan başlayabilir.</span><span class="sxs-lookup"><span data-stu-id="46a2b-109">As hello Application Proxy service expands toomore data centers that may be closer tooyou, you may start toosee improved latency directly.</span></span> <span data-ttu-id="46a2b-110">toosee hello tam listesini Azure veri merkezleri, hello görebilirsiniz [gecikme test sayfası](http://www.azurespeed.com/Azure/Latency).</span><span class="sxs-lookup"><span data-stu-id="46a2b-110">toosee hello full list of Azure data centers, you can see hello [latency test page](http://www.azurespeed.com/Azure/Latency).</span></span> 

<span data-ttu-id="46a2b-111">Merhaba hello uygulama proxy'si hizmeti ile veri merkezleri ile Merhaba bulunabilir [Bağlayıcısı bağlantı noktaları Test aracı](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span><span class="sxs-lookup"><span data-stu-id="46a2b-111">hello data centers with hello Application Proxy service can be found with hello [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span></span> 

## <a name="feedback-on-application-proxy-data-center-locations"></a><span data-ttu-id="46a2b-112">Uygulama proxy'si veri merkezi konumlarını geri bildirimi</span><span class="sxs-lookup"><span data-stu-id="46a2b-112">Feedback on Application Proxy data center locations</span></span> 
<span data-ttu-id="46a2b-113">Uygulama proxy'si olarak henüz içerme ancak tooa harika gecikme geliştirme, sunulmasını Azure veri merkezlerinde olabilir.</span><span class="sxs-lookup"><span data-stu-id="46a2b-113">There may be Azure data centers that don’t as yet include Application Proxy but would lead tooa great latency improvement for you.</span></span> <span data-ttu-id="46a2b-114">Merhaba veri merkezi konumda < aadapfeedback@microsoft.com > biz genişletin gibi biz geri bildirim tooplan kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46a2b-114">hello data center location at <aadapfeedback@microsoft.com> so we can use your feedback tooplan as we expand.</span></span>

<span data-ttu-id="46a2b-115">Biz hello gecikme süresi şu anda uzun gecikme bkz kiracılar için geliştirilmesine yardımcı olun bazı ek özellikler üzerinde çalıştığınız ve emin tooshare belgeleri kullanılabilir sonra olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="46a2b-115">We are working on some additional capabilities that help improve hello latency for tenants that currently see long latencies, and be sure tooshare documentation once available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46a2b-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="46a2b-116">Next steps</span></span>
[<span data-ttu-id="46a2b-117">Mevcut şirket içi proxy sunucuları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="46a2b-117">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)
