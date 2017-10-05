---
title: "Bir uygulama proxy'si uygulama için gerekli güvenlik duvarı bağlantı noktalarının nasıl açılacağı | Microsoft Docs"
description: "Hangi Azure AD düzgün çalışması için uygulama proxy'si açmak için bağlantı noktalarını kullanıma Bul"
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
ms.openlocfilehash: 8ecd6d7e666d362194126a4abba7a65f2c7b8b6b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-open-the-firewall-ports-required-for-an-application-proxy-application"></a><span data-ttu-id="ea689-103">Bir uygulama proxy'si uygulama için gerekli güvenlik duvarı bağlantı noktalarının nasıl açılacağı</span><span class="sxs-lookup"><span data-stu-id="ea689-103">How to open the firewall ports required for an Application Proxy application</span></span>

<span data-ttu-id="ea689-104">Gerekli bağlantı noktalarını ve her bağlantı noktası işlevi tam listesini görmek için Önkoşullar bölümüne bakın. [uygulama proxy'si belgelerine](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span><span class="sxs-lookup"><span data-stu-id="ea689-104">To see a full list of the required ports and the function of each port, see the prerequisites section of the [Application Proxy documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span></span> <span data-ttu-id="ea689-105">Uygulama proxy'si yalnızca giden bağlantı noktalarını kullandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ea689-105">note that Application Proxy only uses outbound ports.</span></span>

<span data-ttu-id="ea689-106">Tüm gerekli bağlantı noktalarını açın açarak yüklü olup olmadığını da denetleyebilirsiniz [Bağlayıcısı bağlantı noktaları Test aracı](https://aadap-portcheck.connectorporttest.msappproxy.net/) şirket içi ağınızdan.</span><span class="sxs-lookup"><span data-stu-id="ea689-106">You can also check whether you have all the required ports open by opening the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network.</span></span> <span data-ttu-id="ea689-107">Daha fazla yeşil onay işaretleri büyük esneklik anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ea689-107">More green checkmarks means greater resiliency.</span></span> 

## <a name="app-proxy-regions"></a><span data-ttu-id="ea689-108">Uygulama proxy'si bölgeleri</span><span class="sxs-lookup"><span data-stu-id="ea689-108">App Proxy regions</span></span>

<span data-ttu-id="ea689-109">Bu bölgeler hangisinin sizin için yeşil olması gereken size bildirmek için bir yol üzerinde çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="ea689-109">We are working on a way to let you know which of these regions needs to be green for you.</span></span> <span data-ttu-id="ea689-110">Şimdilik, tüm olduklarından emin olun.</span><span class="sxs-lookup"><span data-stu-id="ea689-110">For now, make sure they all are.</span></span> <span data-ttu-id="ea689-111">Orta ABD Ayrıca hangi bölgeyi bağımsız olarak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ea689-111">Central US is also required regardless of which region you are in.</span></span>

<span data-ttu-id="ea689-112">Aracının doğru sonuçlar verir emin olmak için emin olun:</span><span class="sxs-lookup"><span data-stu-id="ea689-112">To make sure the tool gives you the right results, be sure to:</span></span>

-   <span data-ttu-id="ea689-113">Bir tarayıcı araç Bağlayıcısı'nı yüklediğiniz sunucudan açın.</span><span class="sxs-lookup"><span data-stu-id="ea689-113">Open the tool on a browser from the server where you have installed the Connector.</span></span>

-   <span data-ttu-id="ea689-114">Herhangi bir proxy veya güvenlik duvarları Bağlayıcınızı için uygulanabilir de bu sayfaya uygulandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="ea689-114">Ensure that any proxies or firewalls applicable to your Connector are also applied to this page.</span></span> <span data-ttu-id="ea689-115">Internet Explorer'da bu yapılabilir giderek **ayarları**  - &gt; **Internet Seçenekleri**  - &gt; **bağlantıları**  - &gt; **Lan ayarları**.</span><span class="sxs-lookup"><span data-stu-id="ea689-115">This can be done in Internet Explorer by going to **Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**.</span></span> <span data-ttu-id="ea689-116">Bu sayfada, alanın "Kullan bir Proxy sunucu için bilgisayarınızı LAN" konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="ea689-116">On this page, you see the field “Use a Proxy Server for your LAN”.</span></span> <span data-ttu-id="ea689-117">Bu kutuyu seçin ve "Adres" alanına proxy adresi yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="ea689-117">Select this box, and put the proxy address into the “Address” field.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea689-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ea689-118">Next steps</span></span>
[<span data-ttu-id="ea689-119">Azure AD uygulama proxy'si bağlayıcılar anlama</span><span class="sxs-lookup"><span data-stu-id="ea689-119">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
