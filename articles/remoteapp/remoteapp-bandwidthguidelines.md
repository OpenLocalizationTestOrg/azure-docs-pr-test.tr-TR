---
title: "Azure RemoteApp ağ bant genişliği - genel yönergeleri | Microsoft Docs"
description: "Azure RemoteApp koleksiyonları ve uygulamalar için bazı temel ağ bant genişliği yönergeleri anlayın."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 529bf318-ae37-4c14-a11c-43fa703d68a3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 0b6521cc240556186890f0b797c6d80e431ac4be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a><span data-ttu-id="d3e6e-103">Azure RemoteApp ağ bant genişliği - (kendi test edilemez ise) genel yönergeleri</span><span class="sxs-lookup"><span data-stu-id="d3e6e-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d3e6e-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="d3e6e-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="d3e6e-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="d3e6e-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="d3e6e-106">Saati veya çalıştırmak için özelliği yoksa [ağ bant genişliği testleri](remoteapp-bandwidthtests.md) Azure RemoteApp için kullanıcı başına ağ bant genişliğini tahmin etmenize yardımcı olabilecek bazı oldukça genel yönergeler aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d3e6e-106">If you do not have the time or capability to run the [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.</span></span>

<span data-ttu-id="d3e6e-107">Bu senaryolar karışımı varsa, hiçbir şey küçük (veya eşittir) öneririz olmayan uzak bir ortamda Internet'e bağlı modern uygulamalar için en düşük ağ bant genişliği olarak 10 MB/sn.</span><span class="sxs-lookup"><span data-stu-id="d3e6e-107">If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as the MINIMUM network bandwidth for modern Internet-connected apps in a remote environment.</span></span> <span data-ttu-id="d3e6e-108">(Açıklandığı gibi bu daha iyi garanti değil de, ortalama kullanıcı deneyimi daha.)</span><span class="sxs-lookup"><span data-stu-id="d3e6e-108">(Although, as discussed, this will not guarantee a better than average user experience.)</span></span>

## <a name="complex-powerpoint-simple-powerpoint"></a><span data-ttu-id="d3e6e-109">Karmaşık PowerPoint, basit PowerPoint</span><span class="sxs-lookup"><span data-stu-id="d3e6e-109">Complex PowerPoint, simple PowerPoint</span></span>
<span data-ttu-id="d3e6e-110">Azure RemoteApp en iyi 100 MB LAN'da yapar.</span><span class="sxs-lookup"><span data-stu-id="d3e6e-110">Azure RemoteApp does best on 100 MB LAN.</span></span> <span data-ttu-id="d3e6e-111">10 MB/sn ağ profilde 120 ms yukarıda değişim birden fazla % 5, olduğunda kullanıcı ortalama bir deneyim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d3e6e-111">At the 10 MB/s network profile, when jitter above 120 ms is more than 5%, the user will see an average experience.</span></span> <span data-ttu-id="d3e6e-112">Çerçeve atlandığından farklı - Örneğin, bir slayt gösterisi glaring 1 MB/s kullanıcı animasyonlu geçişler hiç göremeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3e6e-112">At 1 MB/s the different is glaring - for example, in a slide show, the user might not see animated transitions at all because frames are skipped.</span></span>

## <a name="internet-explorer-mixed-pdf-pdf-text"></a><span data-ttu-id="d3e6e-113">Internet Explorer, karma PDF, PDF, metni</span><span class="sxs-lookup"><span data-stu-id="d3e6e-113">Internet Explorer, mixed PDF, PDF, Text</span></span>
<span data-ttu-id="d3e6e-114">10 MB/sn ağ yakın LAN birçok yönden profilidir.</span><span class="sxs-lookup"><span data-stu-id="d3e6e-114">10 MB/s network profile is close to LAN in most aspects.</span></span> <span data-ttu-id="d3e6e-115">Olabilir ancak bazı değişim ekranda görüntüleri durumdayken bir kullanıcı kaydırdığında 1 MB/sn Tamam bir deneyim sağlar.</span><span class="sxs-lookup"><span data-stu-id="d3e6e-115">1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on the screen.</span></span>

## <a name="flash-video-youtube"></a><span data-ttu-id="d3e6e-116">Flash video (YouTube)</span><span class="sxs-lookup"><span data-stu-id="d3e6e-116">Flash video (YouTube)</span></span>
<span data-ttu-id="d3e6e-117">10 MB/sn (kare hızıyla takip edin ancak artar değişimi kabul edilebilir anlamına gelir) durumdayken 100 MB/sn LAN en iyi deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="d3e6e-117">100 MB/s LAN provides the best experience, while 10 MB/s is acceptable (meaning we keep up with the frame rate but jitter increases).</span></span> <span data-ttu-id="d3e6e-118">1 MB/sn'ye değişim çok yüksek ve fark.</span><span class="sxs-lookup"><span data-stu-id="d3e6e-118">At 1 MB/s, jitter is very high and noticeable.</span></span>

## <a name="word-typing-word-remote-input"></a><span data-ttu-id="d3e6e-119">Word yazarak (Word uzak giriş)</span><span class="sxs-lookup"><span data-stu-id="d3e6e-119">Word typing (Word remote input)</span></span>
<span data-ttu-id="d3e6e-120">Düşük bant genişliği kullanım senaryosu budur.</span><span class="sxs-lookup"><span data-stu-id="d3e6e-120">This is a low-bandwidth usage scenario.</span></span> <span data-ttu-id="d3e6e-121">256 KB/sn'ye kadar iyi bir deneyim LAN olarak sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="d3e6e-121">At 256 KB/s we provide as good of an experience as LAN.</span></span>

## <a name="learn-more"></a><span data-ttu-id="d3e6e-122">Daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="d3e6e-122">Learn more</span></span>
* [<span data-ttu-id="d3e6e-123">Azure RemoteApp ağ bant genişliği kullanımını tahmin etme</span><span class="sxs-lookup"><span data-stu-id="d3e6e-123">Estimate Azure RemoteApp network bandwidth usage</span></span>](remoteapp-bandwidth.md)
* [<span data-ttu-id="d3e6e-124">Azure RemoteApp - nasıl ağ bant genişliği ve kalitesini iş birlikte yaşıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="d3e6e-124">Azure RemoteApp - how do network bandwidth and quality of experience work together?</span></span>](remoteapp-bandwidthexperience.md)
* [<span data-ttu-id="d3e6e-125">Azure RemoteApp - tseting bazı yaygın senaryolar ile ağ bant genişliği kullanımı</span><span class="sxs-lookup"><span data-stu-id="d3e6e-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios</span></span>](remoteapp-bandwidthtests.md)

