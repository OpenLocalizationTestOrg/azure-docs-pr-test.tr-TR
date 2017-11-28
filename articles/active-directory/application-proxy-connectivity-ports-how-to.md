---
title: "bir uygulama proxy'si uygulama için gerekli aaaHow tooopen hello güvenlik duvarı bağlantı noktaları | Microsoft Docs"
description: "Hangi bağlantı noktalarının tooopen hello Azure AD uygulama proxy'si toowork için doğru öğrenin"
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
ms.openlocfilehash: cdc7badb7c15591689a3bfd6bb26da182b00fb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-hello-firewall-ports-required-for-an-application-proxy-application"></a><span data-ttu-id="a3bdd-103">Nasıl tooopen hello uygulama proxy'si uygulama için gerekli güvenlik duvarı bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="a3bdd-103">How tooopen hello firewall ports required for an Application Proxy application</span></span>

<span data-ttu-id="a3bdd-104">toosee hello gerekli bağlantı noktaları ve her bağlantı noktası hello işlevi tam bir listesi hello hello Önkoşullar bölümüne bakın [uygulama proxy'si belgelerine](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span><span class="sxs-lookup"><span data-stu-id="a3bdd-104">toosee a full list of hello required ports and hello function of each port, see hello prerequisites section of hello [Application Proxy documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span></span> <span data-ttu-id="a3bdd-105">Uygulama proxy'si yalnızca giden bağlantı noktalarını kullandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a3bdd-105">note that Application Proxy only uses outbound ports.</span></span>

<span data-ttu-id="a3bdd-106">Açma hello tarafından tüm gerekli hello bağlantı noktalarının açık yüklü olup olmadığını da denetleyebilirsiniz [Bağlayıcısı bağlantı noktaları Test aracı](https://aadap-portcheck.connectorporttest.msappproxy.net/) şirket içi ağınızdan.</span><span class="sxs-lookup"><span data-stu-id="a3bdd-106">You can also check whether you have all hello required ports open by opening hello [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network.</span></span> <span data-ttu-id="a3bdd-107">Daha fazla yeşil onay işaretleri büyük esneklik anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a3bdd-107">More green checkmarks means greater resiliency.</span></span> 

## <a name="app-proxy-regions"></a><span data-ttu-id="a3bdd-108">Uygulama proxy'si bölgeleri</span><span class="sxs-lookup"><span data-stu-id="a3bdd-108">App Proxy regions</span></span>

<span data-ttu-id="a3bdd-109">Bu bölgeler hangisinin bildiğiniz toolet toobe yeşil sizin için gereken şekilde üzerinde çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="a3bdd-109">We are working on a way toolet you know which of these regions needs toobe green for you.</span></span> <span data-ttu-id="a3bdd-110">Şimdilik, tüm olduklarından emin olun.</span><span class="sxs-lookup"><span data-stu-id="a3bdd-110">For now, make sure they all are.</span></span> <span data-ttu-id="a3bdd-111">Orta ABD Ayrıca hangi bölgeyi bağımsız olarak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a3bdd-111">Central US is also required regardless of which region you are in.</span></span>

<span data-ttu-id="a3bdd-112">doğru sonuçlar hello toomake emin hello aracı verir için emin olun:</span><span class="sxs-lookup"><span data-stu-id="a3bdd-112">toomake sure hello tool gives you hello right results, be sure to:</span></span>

-   <span data-ttu-id="a3bdd-113">Merhaba bağlayıcısını yüklediğiniz hello sunucudan Hello aracını kullanarak bir tarayıcı açın.</span><span class="sxs-lookup"><span data-stu-id="a3bdd-113">Open hello tool on a browser from hello server where you have installed hello Connector.</span></span>

-   <span data-ttu-id="a3bdd-114">Bağlayıcı olan ayrıca tüm proxy'leri veya güvenlik duvarları geçerli tooyour toothis sayfa uygulanan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a3bdd-114">Ensure that any proxies or firewalls applicable tooyour Connector are also applied toothis page.</span></span> <span data-ttu-id="a3bdd-115">Internet Explorer'da bu yapılabilir çok giderek**ayarları**  - &gt; **Internet Seçenekleri**  - &gt; **bağlantıları**  - &gt; **Lan ayarları**.</span><span class="sxs-lookup"><span data-stu-id="a3bdd-115">This can be done in Internet Explorer by going too**Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**.</span></span> <span data-ttu-id="a3bdd-116">Bu sayfada hello alan "Kullan bir Proxy sunucu için bilgisayarınızı LAN" konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="a3bdd-116">On this page, you see hello field “Use a Proxy Server for your LAN”.</span></span> <span data-ttu-id="a3bdd-117">Bu kutuyu işaretleyin ve hello proxy adresi hello "Adres" alanına yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="a3bdd-117">Select this box, and put hello proxy address into hello “Address” field.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3bdd-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a3bdd-118">Next steps</span></span>
[<span data-ttu-id="a3bdd-119">Azure AD uygulama proxy'si bağlayıcılar anlama</span><span class="sxs-lookup"><span data-stu-id="a3bdd-119">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
