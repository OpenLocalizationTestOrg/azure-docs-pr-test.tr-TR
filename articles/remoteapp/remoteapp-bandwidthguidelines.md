---
title: "aaaAzure RemoteApp ağ bant genişliği - genel yönergeleri | Microsoft Docs"
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
ms.openlocfilehash: d3407eea71e2e8ac524787ee680cfd870c800864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a><span data-ttu-id="7a959-103">Azure RemoteApp ağ bant genişliği - (kendi test edilemez ise) genel yönergeleri</span><span class="sxs-lookup"><span data-stu-id="7a959-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7a959-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="7a959-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="7a959-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="7a959-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="7a959-106">Başlangıç saati veya özelliği toorun hello yoksa [ağ bant genişliği testleri](remoteapp-bandwidthtests.md) Azure RemoteApp için kullanıcı başına ağ bant genişliğini tahmin etmenize yardımcı olabilecek bazı oldukça genel yönergeler aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7a959-106">If you do not have hello time or capability toorun hello [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.</span></span>

<span data-ttu-id="7a959-107">Bu senaryolar karışımı varsa, her şeyi (veya buna eşit) daha öneririz yok 10 MB/uzak bir ortamda Internet'e bağlı modern uygulamalar için en düşük ağ bant genişliği hello gibi s.</span><span class="sxs-lookup"><span data-stu-id="7a959-107">If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as hello MINIMUM network bandwidth for modern Internet-connected apps in a remote environment.</span></span> <span data-ttu-id="7a959-108">(Açıklandığı gibi bu daha iyi garanti değil de, ortalama kullanıcı deneyimi daha.)</span><span class="sxs-lookup"><span data-stu-id="7a959-108">(Although, as discussed, this will not guarantee a better than average user experience.)</span></span>

## <a name="complex-powerpoint-simple-powerpoint"></a><span data-ttu-id="7a959-109">Karmaşık PowerPoint, basit PowerPoint</span><span class="sxs-lookup"><span data-stu-id="7a959-109">Complex PowerPoint, simple PowerPoint</span></span>
<span data-ttu-id="7a959-110">Azure RemoteApp en iyi 100 MB LAN'da yapar.</span><span class="sxs-lookup"><span data-stu-id="7a959-110">Azure RemoteApp does best on 100 MB LAN.</span></span> <span data-ttu-id="7a959-111">Konumundaki 10 MB hello/s ağ profili 120 ms yukarıda değişim birden fazla % 5, hello kullanıcı olduğunda, ortalama bir deneyim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7a959-111">At hello 10 MB/s network profile, when jitter above 120 ms is more than 5%, hello user will see an average experience.</span></span> <span data-ttu-id="7a959-112">1 MB/sn hello adresindeki farklı - Örneğin, slayt gösterisi glaring, çerçeve atlandığından hello kullanıcı animasyonlu geçişler hiç göremeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a959-112">At 1 MB/s hello different is glaring - for example, in a slide show, hello user might not see animated transitions at all because frames are skipped.</span></span>

## <a name="internet-explorer-mixed-pdf-pdf-text"></a><span data-ttu-id="7a959-113">Internet Explorer, karma PDF, PDF, metni</span><span class="sxs-lookup"><span data-stu-id="7a959-113">Internet Explorer, mixed PDF, PDF, Text</span></span>
<span data-ttu-id="7a959-114">10 MB/sn ağ profilini birçok yönüyle içinde Kapat tooLAN ' dir.</span><span class="sxs-lookup"><span data-stu-id="7a959-114">10 MB/s network profile is close tooLAN in most aspects.</span></span> <span data-ttu-id="7a959-115">Olabilir ancak bazı değişim Merhaba ekranında görüntüleri durumdayken bir kullanıcı kaydırdığında 1 MB/sn Tamam bir deneyim sağlar.</span><span class="sxs-lookup"><span data-stu-id="7a959-115">1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on hello screen.</span></span>

## <a name="flash-video-youtube"></a><span data-ttu-id="7a959-116">Flash video (YouTube)</span><span class="sxs-lookup"><span data-stu-id="7a959-116">Flash video (YouTube)</span></span>
<span data-ttu-id="7a959-117">10 MB/sn (Merhaba kare hızıyla takip edin ancak artar değişimi kabul edilebilir anlamına gelir) durumdayken 100 MB/sn LAN hello en iyi deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7a959-117">100 MB/s LAN provides hello best experience, while 10 MB/s is acceptable (meaning we keep up with hello frame rate but jitter increases).</span></span> <span data-ttu-id="7a959-118">1 MB/sn'ye değişim çok yüksek ve fark.</span><span class="sxs-lookup"><span data-stu-id="7a959-118">At 1 MB/s, jitter is very high and noticeable.</span></span>

## <a name="word-typing-word-remote-input"></a><span data-ttu-id="7a959-119">Word yazarak (Word uzak giriş)</span><span class="sxs-lookup"><span data-stu-id="7a959-119">Word typing (Word remote input)</span></span>
<span data-ttu-id="7a959-120">Düşük bant genişliği kullanım senaryosu budur.</span><span class="sxs-lookup"><span data-stu-id="7a959-120">This is a low-bandwidth usage scenario.</span></span> <span data-ttu-id="7a959-121">256 KB/sn'ye kadar iyi bir deneyim LAN olarak sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="7a959-121">At 256 KB/s we provide as good of an experience as LAN.</span></span>

## <a name="learn-more"></a><span data-ttu-id="7a959-122">Daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="7a959-122">Learn more</span></span>
* [<span data-ttu-id="7a959-123">Azure RemoteApp ağ bant genişliği kullanımını tahmin etme</span><span class="sxs-lookup"><span data-stu-id="7a959-123">Estimate Azure RemoteApp network bandwidth usage</span></span>](remoteapp-bandwidth.md)
* [<span data-ttu-id="7a959-124">Azure RemoteApp - nasıl ağ bant genişliği ve kalitesini iş birlikte yaşıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="7a959-124">Azure RemoteApp - how do network bandwidth and quality of experience work together?</span></span>](remoteapp-bandwidthexperience.md)
* [<span data-ttu-id="7a959-125">Azure RemoteApp - tseting bazı yaygın senaryolar ile ağ bant genişliği kullanımı</span><span class="sxs-lookup"><span data-stu-id="7a959-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios</span></span>](remoteapp-bandwidthtests.md)

