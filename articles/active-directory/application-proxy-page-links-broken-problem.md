---
title: "Sayfadaki bağlantıları için uygulama proxy'si uygulama çalışmıyor | Microsoft Docs"
description: "Azure AD ile tümleşik uygulama proxy'si uygulamaları kırık bağlantılı sorunlarını giderme"
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
ms.openlocfilehash: 83c4261fab0498541591c01f9bb692b396c7b751
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="links-on-the-page-dont-work-for-an-application-proxy-application"></a><span data-ttu-id="54156-103">Sayfadaki bağlantıları için uygulama proxy'si uygulama çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="54156-103">Links on the page don't work for an Application Proxy application</span></span>

<span data-ttu-id="54156-104">Bu makalede, Azure Active Directory Uygulama proxy'si uygulamanızın bağlantıları düzgün çalışmıyor neden sorun giderme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="54156-104">This article help you to troubleshoot why links on your Azure Active Directory Application Proxy application don't work correctly.</span></span>

## <a name="overview"></a><span data-ttu-id="54156-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="54156-105">Overview</span></span> 
<span data-ttu-id="54156-106">Uygulama proxy'si uygulama yayımlandıktan sonra varsayılan olarak uygulama iş yalnızca bağlantılar hedeflere yayımlanan kök URL'si içinde yer alan bağlantıları vardır.</span><span class="sxs-lookup"><span data-stu-id="54156-106">After publishing an Application Proxy app, the only links that work by default in the application are links to destinations contained within the published root URL.</span></span> <span data-ttu-id="54156-107">Uygulamaların içindeki bağlantılar çalışmayan, uygulama için iç URL büyük olasılıkla uygulamadaki bağlantıların tüm hedefler dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="54156-107">The links within the applications aren’t working, the internal URL for the application probably does not include all the destinations of links within the application.</span></span>

<span data-ttu-id="54156-108">**Bunun nedeni?**</span><span class="sxs-lookup"><span data-stu-id="54156-108">**Why does this happen?**</span></span> <span data-ttu-id="54156-109">Bir uygulama bir bağlantıya tıklandığında, uygulama proxy'si aynı uygulama içinde ya da bir iç URL veya bir harici URL'si olarak URL çözümlemeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="54156-109">When clicking a link in an application, Application Proxy tries to resolve the URL as either an internal URL within the same application, or as an externally available URL.</span></span> <span data-ttu-id="54156-110">Aynı uygulama içinde yer almayan bir iç URL için bağlantı noktaları, değil ya da bu demetlerin ait ve bulunamadı bir hata.</span><span class="sxs-lookup"><span data-stu-id="54156-110">If the link points to an internal URL that is not within the same application, it does not belong to either of these buckets and result in a not found error.</span></span>

## <a name="ways-you-can-resolve-broken-links"></a><span data-ttu-id="54156-111">Bağlantılar bozuk çözebilmek için yollar</span><span class="sxs-lookup"><span data-stu-id="54156-111">Ways you can resolve broken links</span></span>

<span data-ttu-id="54156-112">Bu sorunu çözmek için üç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="54156-112">There are three ways to resolve this issue.</span></span> <span data-ttu-id="54156-113">Aşağıdaki seçenekler karmaşıklık artan sırada listelenir.</span><span class="sxs-lookup"><span data-stu-id="54156-113">The choices below are in listed in increasing complexity.</span></span>

1.  <span data-ttu-id="54156-114">Uygulama için tüm bağlantılar içeren bir kök İç URL olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="54156-114">Make sure the internal URL is a root that contains all the relevant links for the application.</span></span> <span data-ttu-id="54156-115">Bu, aynı uygulama içinde yayımlanan içerik olarak çözümlenmesi tüm bağlantılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="54156-115">This allows all links to be resolved as content published within the same application.</span></span>

    <span data-ttu-id="54156-116">İç URL'sini değiştirebilirsiniz, ancak kullanıcılar için giriş sayfası değiştirmek istemiyorsanız, giriş sayfası URL'si önceden yayımlanmış dahili URL'yi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="54156-116">If you change the internal URL but don’t want to change the landing page for users, change the Home page URL to the previously published internal URL.</span></span> <span data-ttu-id="54156-117">Bu, "Azure Active Directory'ye" - giderek yapılabilir&gt; uygulama kayıtlar -&gt; - uygulamayı seçin&gt; özellikleri.</span><span class="sxs-lookup"><span data-stu-id="54156-117">This can be done by going to “Azure Active Directory” -&gt; App Registrations -&gt; select the application -&gt; Properties.</span></span> <span data-ttu-id="54156-118">Bu özellikler sekmesinde, istenen giriş sayfası olarak Ayarla "giriş sayfası URL'si" alanına bakın.</span><span class="sxs-lookup"><span data-stu-id="54156-118">In this properties tab, you see the field “Home Page URL” which you can adjust to be the desired landing page.</span></span>

2.  <span data-ttu-id="54156-119">Uygulamalarınızı tam etki alanı adlarını (FQDN) kullanıyorsanız, [özel etki alanlarını](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) uygulamalarınızı yayımlamak için.</span><span class="sxs-lookup"><span data-stu-id="54156-119">If your applications use fully qualified domain names (FQDNs), use [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) to publish your applications.</span></span> <span data-ttu-id="54156-120">Bu özellik hem dahili olarak kullanılan ve dışarıdan aynı URL'ye sağlar.</span><span class="sxs-lookup"><span data-stu-id="54156-120">This feature allows the same URL to be used both internally and externally.</span></span>

    <span data-ttu-id="54156-121">Bu seçenek iç URL'leri uygulamaya içindeki bağlantılar da dışarıdan tanınır beri uygulamanızı bağlantıları uygulama proxy'si aracılığıyla harici erişilebilir olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="54156-121">This option ensures that the links in your application are externally accessible through Application Proxy since the links within the application to internal URLs are also recognized externally.</span></span> <span data-ttu-id="54156-122">Tüm bağlantılar hala yayımlanan uygulamaya ait olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="54156-122">Note that all links still need to belong to a published application.</span></span> <span data-ttu-id="54156-123">Ancak, bu seçenek ile bağlantıları aynı uygulamaya ait gerek yoktur ve birden çok uygulamalara ait olabilir.</span><span class="sxs-lookup"><span data-stu-id="54156-123">However, with this option the links do not need to belong to the same application and can belong to multiple applications.</span></span>

3.  <span data-ttu-id="54156-124">Bu seçeneklerin ikisi uygun varsa, URL çevirisi/yeniden yazma işlemi yapan yeni bir özellik için Önizleme katılın.</span><span class="sxs-lookup"><span data-stu-id="54156-124">If neither of these options are feasible, you join the preview for a new feature that do URL translation/rewriting.</span></span> <span data-ttu-id="54156-125">Bu seçenek ile iç URL'leri uygulamalarınızı HTML gövdesinde mevcut bağlantıları çevrilmiş veya "Eşlenen, yayımlanan dış uygulama Proxy URL'lerini".</span><span class="sxs-lookup"><span data-stu-id="54156-125">With this option, internal URLs or links that exist in the HTML body of your applications be translated, or “mapped”, to the published external App Proxy URLs.</span></span> <span data-ttu-id="54156-126">Bu yalnızca HTML veya CSS bağlantıları için çalışır ve bu yardımcı bağlantı JS oluşturulursa.</span><span class="sxs-lookup"><span data-stu-id="54156-126">This only works for links in the HTML or CSS, and this not help if your link is generated through JS.</span></span> 

<span data-ttu-id="54156-127">Sonuç olarak, kullanarak tavsiye [özel etki alanlarını](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) mümkünse çözümü.</span><span class="sxs-lookup"><span data-stu-id="54156-127">As a result, we strongly recommend using the [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution if possible.</span></span> <span data-ttu-id="54156-128">Önizleme katılmak istiyorsanız, e-posta < aadapfeedback@microsoft.com > applicationId(s) ile.</span><span class="sxs-lookup"><span data-stu-id="54156-128">If you do want to join the preview, email <aadapfeedback@microsoft.com> with the applicationId(s).</span></span>

## <a name="next-steps"></a><span data-ttu-id="54156-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="54156-129">Next steps</span></span>
[<span data-ttu-id="54156-130">Mevcut şirket içi proxy sunucuları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="54156-130">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)

