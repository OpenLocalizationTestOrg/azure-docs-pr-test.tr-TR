---
title: "aaaGetting hello Azure AD raporlama API'si ile çalışmaya | Microsoft Docs"
description: "Nasıl kullanmaya tooget hello Azure Active Directory raporlama API'si"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/18/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: bb7d72ba445daa367d7502889c38a605a16f26d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api"></a><span data-ttu-id="ae0d4-103">Hello Azure Active Directory raporlama API'si ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ae0d4-103">Getting started with hello Azure Active Directory reporting API</span></span>

<span data-ttu-id="ae0d4-104">Azure Active Directory ile çok çeşitli raporlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="ae0d4-104">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="ae0d4-105">Bu raporların Hello veriler SIEM sistemleri, Denetim ve iş zekası araçları gibi çok kullanışlı tooyour uygulamalar olabilir.</span><span class="sxs-lookup"><span data-stu-id="ae0d4-105">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="ae0d4-106">bir dizi REST tabanlı API'ler aracılığıyla programlı erişim toohello veri API'leri sağlamak Hello Azure AD raporlama.</span><span class="sxs-lookup"><span data-stu-id="ae0d4-106">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="ae0d4-107">Çeşitli programlama dilleri ve araçlarından bu API'leri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae0d4-107">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="ae0d4-108">Bu makale hello Azure AD Raporlama ile çalışmaya tooget ihtiyacınız hello bilgilerle sağlar API'leri.</span><span class="sxs-lookup"><span data-stu-id="ae0d4-108">This article provides you with hello information you need tooget started with hello Azure AD reporting APIs.</span></span>
<span data-ttu-id="ae0d4-109">Merhaba sonraki bölümde hello kullanma hakkında daha fazla ayrıntı denetim ve oturum API bileşenini bulun.</span><span class="sxs-lookup"><span data-stu-id="ae0d4-109">In hello next section, you find more details about using hello audit and sign-in APIs.</span></span> 

<span data-ttu-id="ae0d4-110">Sık sorulan sorular için okuma bizim [SSS](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span><span class="sxs-lookup"><span data-stu-id="ae0d4-110">For frequently asked questions,read our [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span></span> <span data-ttu-id="ae0d4-111">Sorunlar için lütfen [bir destek bileti dosya](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span><span class="sxs-lookup"><span data-stu-id="ae0d4-111">For issues, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span></span>

## <a name="learning-map"></a><span data-ttu-id="ae0d4-112">Öğrenme haritası</span><span class="sxs-lookup"><span data-stu-id="ae0d4-112">Learning map</span></span>
1. <span data-ttu-id="ae0d4-113">**Hazırlama** -API örneklerinizi test etmeden önce toocomplete hello gereksinim [Önkoşullar tooaccess hello Azure AD raporlama API'si](active-directory-reporting-api-prerequisites-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ae0d4-113">**Prepare** - Before you can test your API samples, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span></span>
2. <span data-ttu-id="ae0d4-114">**Araştır** -API'leri raporlama hello bir ilk izlenim alın:</span><span class="sxs-lookup"><span data-stu-id="ae0d4-114">**Explore** - Get a first impression of hello reporting APIs:</span></span>
   
   * [<span data-ttu-id="ae0d4-115">Merhaba örnekleri hello denetim API kullanma</span><span class="sxs-lookup"><span data-stu-id="ae0d4-115">Using hello samples for hello audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="ae0d4-116">Hello örnekleri için hello oturum açma etkinliği raporu API kullanma</span><span class="sxs-lookup"><span data-stu-id="ae0d4-116">Using hello samples for hello sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="ae0d4-117">**Özelleştirme** -kendi çözümü oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ae0d4-117">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="ae0d4-118">Merhaba denetim API başvurusunu kullanma</span><span class="sxs-lookup"><span data-stu-id="ae0d4-118">Using hello audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="ae0d4-119">Merhaba oturum açma etkinliği raporu kullanarak API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="ae0d4-119">Using hello sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="ae0d4-120">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="ae0d4-120">Next Steps</span></span>
<span data-ttu-id="ae0d4-121">Merak toosee varsa tüm mevcut Azure AD Graph API uç noktaları, bu bağlantıyı kullanın: [https://graph.windows.net/tenant-name/activities/$ metadata? api-version beta =](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="ae0d4-121">If you are curious toosee all available Azure AD Graph API endpoints, use this link: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span></span>

