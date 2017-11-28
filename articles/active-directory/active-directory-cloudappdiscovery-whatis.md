---
title: "aaaFinding yönetilmeyen bulut uygulamaları Cloud App Discovery ile | Microsoft Docs"
description: "Bulma ve Cloud App Discovery, hello avantajları nelerdir ve nasıl çalıştığı ile uygulamaları yönetme hakkında bilgi sağlar."
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
ms.openlocfilehash: 50c24af9bb400e4be11f4ad2d1de13d26f5467bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="8f6dd-104">Cloud App Discovery ile bulma yönetilmeyen bulut uygulamaları</span><span class="sxs-lookup"><span data-stu-id="8f6dd-104">Finding unmanaged cloud applications with Cloud App Discovery</span></span>
## <a name="overview"></a><span data-ttu-id="8f6dd-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="8f6dd-105">Overview</span></span>
<span data-ttu-id="8f6dd-106">Modern kuruluşlarda, BT departmanları kuruluşu üyelerini işlerine toodo kullanmak tüm hello bulut uygulamaları tanımaz genellikle.</span><span class="sxs-lookup"><span data-stu-id="8f6dd-106">In modern enterprises, IT departments are often not aware of all hello cloud applications that members of their organization use toodo their work.</span></span> <span data-ttu-id="8f6dd-107">Yöneticiler yetkisiz erişim toocorporate verileri, olası veri sıkıntılarına ve diğer güvenlik risklerine endişeniz neden olurdu kolay toosee olur.</span><span class="sxs-lookup"><span data-stu-id="8f6dd-107">It is easy toosee why administrators would have concerns about unauthorized access toocorporate data, possible data leakage and other security risks.</span></span> <span data-ttu-id="8f6dd-108">Bu tanıma olmaması, bu güvenlik riskleri postalarla göründüğü için göz korkutucu bir plan oluşturma yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f6dd-108">This lack of awareness can make creating a plan for dealing with these security risks seem daunting.</span></span>

<span data-ttu-id="8f6dd-109">Cloud App Discovery, kuruluşunuzda hello kişiler tarafından kullanılan toodiscover bulut uygulamalarını sağlayan Azure Active Directory (AD) Premium özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="8f6dd-109">Cloud App Discovery is a feature of Azure Active Directory (AD) Premium that enables you toodiscover cloud applications being used by hello people in your organization.</span></span>

<span data-ttu-id="8f6dd-110">**Cloud App Discovery ile şunları yapabilirsiniz:**</span><span class="sxs-lookup"><span data-stu-id="8f6dd-110">**With Cloud App Discovery, you can:**</span></span>

* <span data-ttu-id="8f6dd-111">Kullanılan hello bulut uygulamalarını bulmak ve bu kullanım kullanıcı sayısı, trafik veya web istekleri toohello uygulama sayısı birim göre ölçün.</span><span class="sxs-lookup"><span data-stu-id="8f6dd-111">Find hello cloud applications being used and measure that usage by number of users, volume of traffic or number of web requests toohello application.</span></span>
* <span data-ttu-id="8f6dd-112">Bir uygulama kullanarak hello kullanıcıları belirleyin.</span><span class="sxs-lookup"><span data-stu-id="8f6dd-112">Identify hello users that are using an application.</span></span>
* <span data-ttu-id="8f6dd-113">Çevrimdışı analiz için verileri dışa aktarın.</span><span class="sxs-lookup"><span data-stu-id="8f6dd-113">Export data for offline analysis.</span></span>
* <span data-ttu-id="8f6dd-114">Bu uygulamalar BT denetimindeki getirin ve kullanıcı yönetimi için çoklu oturum açmayı etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="8f6dd-114">Bring these applications under IT control and enable single sign on for user management.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="8f6dd-115">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="8f6dd-115">How it works</span></span>
1. <span data-ttu-id="8f6dd-116">Uygulama kullanımı aracıları kullanıcının bilgisayarlara yüklenir.</span><span class="sxs-lookup"><span data-stu-id="8f6dd-116">Application usage agents are installed on user's computers.</span></span>
2. <span data-ttu-id="8f6dd-117">Merhaba uygulama kullanım bilgilerini Hello aracıları tarafından yakalanan bir güvenli ve şifrelenmiş bir kanal toohello bulut uygulama bulma hizmeti gönderilir.</span><span class="sxs-lookup"><span data-stu-id="8f6dd-117">hello application usage information captured by hello agents is sent over a secure, encrypted channel toohello cloud app discovery service.</span></span>
3. <span data-ttu-id="8f6dd-118">Merhaba Cloud App Discovery hizmetine hello veri değerlendirir ve raporları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8f6dd-118">hello Cloud App Discovery service evaluates hello data and generates reports.</span></span>

![Cloud App Discovery diyagramı](./media/active-directory-cloudappdiscovery/cad01.png)

<span data-ttu-id="8f6dd-120">cloud App Discovery ile başlatılan tooget bakın [alma başlatılmış olan Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span><span class="sxs-lookup"><span data-stu-id="8f6dd-120">tooget started with Cloud App Discovery, see [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span></span>

## <a name="related-articles"></a><span data-ttu-id="8f6dd-121">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="8f6dd-121">Related articles</span></span>
* [<span data-ttu-id="8f6dd-122">Cloud App Discovery güvenlik ve gizlilik konuları</span><span class="sxs-lookup"><span data-stu-id="8f6dd-122">Cloud App Discovery Security and Privacy Considerations</span></span>](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [<span data-ttu-id="8f6dd-123">Cloud App Discovery Grup İlkesi Dağıtım Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="8f6dd-123">Cloud App Discovery Group Policy Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [<span data-ttu-id="8f6dd-124">Cloud App Discovery System Center Dağıtım Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="8f6dd-124">Cloud App Discovery System Center Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [<span data-ttu-id="8f6dd-125">Özel bağlantı noktaları ile Proxy sunucuları için bulut uygulama bulma kayıt defteri ayarları</span><span class="sxs-lookup"><span data-stu-id="8f6dd-125">Cloud App Discovery Registry Settings for Proxy Servers with Custom Ports</span></span>](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [<span data-ttu-id="8f6dd-126">Cloud App Discovery Aracısı değişim günlüğü</span><span class="sxs-lookup"><span data-stu-id="8f6dd-126">Cloud App Discovery Agent Changelog </span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [<span data-ttu-id="8f6dd-127">Cloud App Discovery sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="8f6dd-127">Cloud App Discovery Frequently Asked Questions</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [<span data-ttu-id="8f6dd-128">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="8f6dd-128">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

