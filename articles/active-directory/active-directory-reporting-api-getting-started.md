---
title: "hello Azure AD Klasik portalında hello Azure AD raporlama API'si ile çalışmaya aaaGetting | Microsoft Docs"
description: "Nasıl kullanmaya tooget hello Azure Active Directory raporlama API'si"
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
ms.openlocfilehash: 52e22d442650731fc6ed28991fc65f9182af0540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api-on-hello-azure-ad-classic-portal"></a><span data-ttu-id="c3f85-103">Hello Azure Active Directory hello Azure AD Klasik portalında raporlama API'si ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c3f85-103">Getting started with hello Azure Active Directory reporting API on hello Azure AD classic portal</span></span>
<span data-ttu-id="c3f85-104">*Bu konu hello parçasıdır [Azure Active Directory raporlama Kılavuzu](active-directory-reporting-guide.md).*</span><span class="sxs-lookup"><span data-stu-id="c3f85-104">*This topic is part of hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="c3f85-105">Azure Active Directory ile çok çeşitli raporlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="c3f85-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="c3f85-106">Bu raporların Hello veriler SIEM sistemleri, Denetim ve iş zekası araçları gibi çok kullanışlı tooyour uygulamalar olabilir.</span><span class="sxs-lookup"><span data-stu-id="c3f85-106">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="c3f85-107">bir dizi REST tabanlı API'ler aracılığıyla programlı erişim toohello veri API'leri sağlamak Hello Azure AD raporlama.</span><span class="sxs-lookup"><span data-stu-id="c3f85-107">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="c3f85-108">Çeşitli programlama dilleri ve araçlarından bu API'leri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3f85-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="c3f85-109">Bu makale hello Azure AD Raporlama ile çalışmaya tooget ihtiyacınız hello bilgilerle sağlar API'leri.</span><span class="sxs-lookup"><span data-stu-id="c3f85-109">This article provides you with hello information you need tooget started with hello Azure AD reporting APIs.</span></span>
<span data-ttu-id="c3f85-110">Merhaba sonraki bölümde hello kullanma hakkında daha fazla ayrıntı denetim ve oturum API bileşenini bulun.</span><span class="sxs-lookup"><span data-stu-id="c3f85-110">In hello next section, you find more details about using hello audit and sign-in APIs.</span></span> <span data-ttu-id="c3f85-111">Diğer tüm API'leri için hello bkz [Azure AD raporları ve events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c3f85-111">For all other APIs, see hello [Azure AD reports and events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="c3f85-112">Sorularınız, sorunları veya Geri bildiriminiz için lütfen başvurun [raporlama AAD Yardım](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="c3f85-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="c3f85-113">Öğrenme haritası</span><span class="sxs-lookup"><span data-stu-id="c3f85-113">Learning map</span></span>
1. <span data-ttu-id="c3f85-114">**Hazırlama** -API örneklerinizi test etmeden önce toocomplete hello gereksinim [Önkoşullar tooaccess hello Azure AD raporlama API'si](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="c3f85-114">**Prepare** - Before you can test your API samples, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="c3f85-115">**Araştır** -API'leri raporlama hello bir ilk izlenim alın:</span><span class="sxs-lookup"><span data-stu-id="c3f85-115">**Explore** - Get a first impression of hello reporting APIs:</span></span>
   
   * [<span data-ttu-id="c3f85-116">Merhaba örnekleri hello denetim API kullanma</span><span class="sxs-lookup"><span data-stu-id="c3f85-116">Using hello samples for hello audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="c3f85-117">Hello örnekleri için hello oturum açma etkinliği raporu API kullanma</span><span class="sxs-lookup"><span data-stu-id="c3f85-117">Using hello samples for hello sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="c3f85-118">**Özelleştirme** -kendi çözümü oluşturun:</span><span class="sxs-lookup"><span data-stu-id="c3f85-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="c3f85-119">Merhaba denetim API başvurusunu kullanma</span><span class="sxs-lookup"><span data-stu-id="c3f85-119">Using hello audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="c3f85-120">Merhaba oturum açma etkinliği raporu kullanarak API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="c3f85-120">Using hello sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="c3f85-121">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="c3f85-121">Next Steps</span></span>
<span data-ttu-id="c3f85-122">Merak toosee varsa tüm mevcut Azure AD Graph API uç noktaları çok giderek hello[https://graph.windows.net/tenant-name/reports/$ metadata? api-version beta =](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="c3f85-122">If you are curious toosee all of hello available Azure AD Graph API endpoints by navigating too[https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

