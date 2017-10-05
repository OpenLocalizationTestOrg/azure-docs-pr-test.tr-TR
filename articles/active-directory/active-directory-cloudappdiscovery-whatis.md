---
title: "Cloud App Discovery ile yönetilmeyen bulut uygulamaları bulma | Microsoft Docs"
description: "Bulma ve Cloud App Discovery, avantajları nelerdir ve nasıl çalıştığı ile uygulamaları yönetme hakkında bilgi sağlar."
services: active-directory
keywords: "cloud app discovery'yi, uygulamaları yönetme"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6284ff5bac8edbc19561d0916adef153526dfbe3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="20bb2-104">Cloud App Discovery ile bulma yönetilmeyen bulut uygulamaları</span><span class="sxs-lookup"><span data-stu-id="20bb2-104">Finding unmanaged cloud applications with Cloud App Discovery</span></span>
## <a name="overview"></a><span data-ttu-id="20bb2-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="20bb2-105">Overview</span></span>
<span data-ttu-id="20bb2-106">Modern kuruluşlarda, BT departmanları işlerini yapmak için kuruluşları üyeleri kullanan tüm bulut uygulamaları tanımaz genellikle.</span><span class="sxs-lookup"><span data-stu-id="20bb2-106">In modern enterprises, IT departments are often not aware of all the cloud applications that members of their organization use to do their work.</span></span> <span data-ttu-id="20bb2-107">Yöneticileri Kurumsal verileri, olası veri sıkıntılarına ve diğer güvenlik risklerine yetkisiz erişimi endişeniz neden olurdu görmek kolaydır.</span><span class="sxs-lookup"><span data-stu-id="20bb2-107">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span></span> <span data-ttu-id="20bb2-108">Bu tanıma olmaması, bu güvenlik riskleri postalarla göründüğü için göz korkutucu bir plan oluşturma yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20bb2-108">This lack of awareness can make creating a plan for dealing with these security risks seem daunting.</span></span>

<span data-ttu-id="20bb2-109">Cloud App Discovery, kuruluşunuzdaki kişiler tarafından kullanılan bulut uygulamalarını keşfetmek sağlayan Azure Active Directory (AD) Premium özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="20bb2-109">Cloud App Discovery is a feature of Azure Active Directory (AD) Premium that enables you to discover cloud applications being used by the people in your organization.</span></span>

<span data-ttu-id="20bb2-110">**Cloud App Discovery ile şunları yapabilirsiniz:**</span><span class="sxs-lookup"><span data-stu-id="20bb2-110">**With Cloud App Discovery, you can:**</span></span>

* <span data-ttu-id="20bb2-111">Kullanılan bulut uygulamalarını bulmak ve bu kullanım ölçme kullanıcı sayısı, akış hacmine veya uygulamaya web isteklerinin sayısı.</span><span class="sxs-lookup"><span data-stu-id="20bb2-111">Find the cloud applications being used and measure that usage by number of users, volume of traffic or number of web requests to the application.</span></span>
* <span data-ttu-id="20bb2-112">Bir uygulama kullanarak kullanıcıları belirleyin.</span><span class="sxs-lookup"><span data-stu-id="20bb2-112">Identify the users that are using an application.</span></span>
* <span data-ttu-id="20bb2-113">Çevrimdışı analiz için verileri dışa aktarın.</span><span class="sxs-lookup"><span data-stu-id="20bb2-113">Export data for offline analysis.</span></span>
* <span data-ttu-id="20bb2-114">Bu uygulamalar BT denetimindeki getirin ve kullanıcı yönetimi için çoklu oturum açmayı etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="20bb2-114">Bring these applications under IT control and enable single sign on for user management.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="20bb2-115">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="20bb2-115">How it works</span></span>
1. <span data-ttu-id="20bb2-116">Uygulama kullanımı aracıları kullanıcının bilgisayarlara yüklenir.</span><span class="sxs-lookup"><span data-stu-id="20bb2-116">Application usage agents are installed on user's computers.</span></span>
2. <span data-ttu-id="20bb2-117">Aracıları tarafından yakalanan uygulama kullanım bilgilerini bulut uygulama bulma hizmeti için güvenli, şifrelenmiş bir kanal üzerinden gönderilir.</span><span class="sxs-lookup"><span data-stu-id="20bb2-117">The application usage information captured by the agents is sent over a secure, encrypted channel to the cloud app discovery service.</span></span>
3. <span data-ttu-id="20bb2-118">Cloud App Discovery hizmetine veri değerlendirir ve raporları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="20bb2-118">The Cloud App Discovery service evaluates the data and generates reports.</span></span>

![Cloud App Discovery diyagramı](./media/active-directory-cloudappdiscovery/cad01.png)

<span data-ttu-id="20bb2-120">Cloud App Discovery'yi kullanmaya başlamak için bkz: [alma başlatılmış olan Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span><span class="sxs-lookup"><span data-stu-id="20bb2-120">To get started with Cloud App Discovery, see [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span></span>

## <a name="related-articles"></a><span data-ttu-id="20bb2-121">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="20bb2-121">Related articles</span></span>
* [<span data-ttu-id="20bb2-122">Cloud App Discovery güvenlik ve gizlilik konuları</span><span class="sxs-lookup"><span data-stu-id="20bb2-122">Cloud App Discovery Security and Privacy Considerations</span></span>](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [<span data-ttu-id="20bb2-123">Cloud App Discovery Grup İlkesi Dağıtım Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="20bb2-123">Cloud App Discovery Group Policy Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [<span data-ttu-id="20bb2-124">Cloud App Discovery System Center Dağıtım Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="20bb2-124">Cloud App Discovery System Center Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [<span data-ttu-id="20bb2-125">Özel bağlantı noktaları ile Proxy sunucuları için bulut uygulama bulma kayıt defteri ayarları</span><span class="sxs-lookup"><span data-stu-id="20bb2-125">Cloud App Discovery Registry Settings for Proxy Servers with Custom Ports</span></span>](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [<span data-ttu-id="20bb2-126">Cloud App Discovery Aracısı değişim günlüğü</span><span class="sxs-lookup"><span data-stu-id="20bb2-126">Cloud App Discovery Agent Changelog </span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [<span data-ttu-id="20bb2-127">Cloud App Discovery sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="20bb2-127">Cloud App Discovery Frequently Asked Questions</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [<span data-ttu-id="20bb2-128">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="20bb2-128">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

