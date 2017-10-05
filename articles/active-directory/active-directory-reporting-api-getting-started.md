---
title: "Azure AD Azure AD Klasik portalında raporlama API'si ile çalışmaya başlama | Microsoft Docs"
description: "Azure Active raporlama API'si ile dizinde nereden başlayacaksınız"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/18/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 5e98b660fe19bb8abebf1c3b996b6295a6c4e728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api-on-the-azure-ad-classic-portal"></a><span data-ttu-id="b6937-103">Azure Active Directory'ı Azure AD Klasik portalında raporlama API'si ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b6937-103">Getting started with the Azure Active Directory reporting API on the Azure AD classic portal</span></span>
<span data-ttu-id="b6937-104">*Bu konuda yer [Azure Active Directory raporlama Kılavuzu](active-directory-reporting-guide.md).*</span><span class="sxs-lookup"><span data-stu-id="b6937-104">*This topic is part of the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="b6937-105">Azure Active Directory ile çok çeşitli raporlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6937-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="b6937-106">Bu raporların verileri SIEM sistemleri, denetim ve iş zekası araçları gibi uygulamalarınız için çok yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b6937-106">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="b6937-107">Azure AD raporlama API'leri, bir dizi REST tabanlı API aracılığıyla verilere programlı erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6937-107">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="b6937-108">Çeşitli programlama dilleri ve araçlarından bu API'leri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6937-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="b6937-109">Bu makalede, Azure AD ile çalışmaya başlamak gereken bilgilerle API'leri raporlama sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6937-109">This article provides you with the information you need to get started with the Azure AD reporting APIs.</span></span>
<span data-ttu-id="b6937-110">Sonraki bölümde, Denetim kullanma hakkında daha fazla ayrıntı ve API oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b6937-110">In the next section, you find more details about using the audit and sign-in APIs.</span></span> <span data-ttu-id="b6937-111">Diğer tüm API'leri için bkz: [Azure AD raporları ve events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) makalesi.</span><span class="sxs-lookup"><span data-stu-id="b6937-111">For all other APIs, see the [Azure AD reports and events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="b6937-112">Sorularınız, sorunları veya Geri bildiriminiz için lütfen başvurun [raporlama AAD Yardım](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b6937-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="b6937-113">Öğrenme haritası</span><span class="sxs-lookup"><span data-stu-id="b6937-113">Learning map</span></span>
1. <span data-ttu-id="b6937-114">**Hazırlama** -API örneklerinizi test etmeden önce tamamlamanız gereken [Azure AD raporlama API'si erişmek için Önkoşullar](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="b6937-114">**Prepare** - Before you can test your API samples, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="b6937-115">**Araştır** -raporlama API'leri bir ilk izlenim alın:</span><span class="sxs-lookup"><span data-stu-id="b6937-115">**Explore** - Get a first impression of the reporting APIs:</span></span>
   
   * [<span data-ttu-id="b6937-116">Denetim API'si örnekleri kullanma</span><span class="sxs-lookup"><span data-stu-id="b6937-116">Using the samples for the audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="b6937-117">Oturum açma etkinliği raporu API örnekleri kullanma</span><span class="sxs-lookup"><span data-stu-id="b6937-117">Using the samples for the sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="b6937-118">**Özelleştirme** -kendi çözümü oluşturun:</span><span class="sxs-lookup"><span data-stu-id="b6937-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="b6937-119">API Başvurusu denetim kullanma</span><span class="sxs-lookup"><span data-stu-id="b6937-119">Using the audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="b6937-120">Oturum açma etkinliği raporu API başvurusunu kullanma</span><span class="sxs-lookup"><span data-stu-id="b6937-120">Using the sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="b6937-121">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="b6937-121">Next Steps</span></span>
<span data-ttu-id="b6937-122">Tüm mevcut Azure AD Graph API uç noktaları giderek görmek merak ediyorsanız [https://graph.windows.net/tenant-name/reports/$ metadata? api-version beta =](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="b6937-122">If you are curious to see all of the available Azure AD Graph API endpoints by navigating to [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

