---
title: "Azure AD Connect: Önizleme özellikleri | Microsoft Docs"
description: "Bu konuda, Azure AD Connect önizlemede olan daha fazla ayrıntı özellikleri açıklanmaktadır."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a><span data-ttu-id="daca9-103">Önizleme özellikleri hakkında daha fazla ayrıntı</span><span class="sxs-lookup"><span data-stu-id="daca9-103">More details about features in preview</span></span>
<span data-ttu-id="daca9-104">Bu konuda, şu anda önizlemede nasıl toouse özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="daca9-104">This topic describes how toouse features currently in preview.</span></span>

## <a name="group-writeback"></a><span data-ttu-id="daca9-105">Grup geri yazma</span><span class="sxs-lookup"><span data-stu-id="daca9-105">Group writeback</span></span>
<span data-ttu-id="daca9-106">İsteğe bağlı özellikler grup geri yazma için Hello seçenek sağlar, toowriteback **Office 365 grupları** yüklü olan Exchange ile tooa orman.</span><span class="sxs-lookup"><span data-stu-id="daca9-106">hello option for group writeback in optional features allows you toowriteback **Office 365 Groups** tooa forest with Exchange installed.</span></span> <span data-ttu-id="daca9-107">Bu, her zaman hello bulutta yönetilir grubudur.</span><span class="sxs-lookup"><span data-stu-id="daca9-107">This is a group that is always mastered in hello cloud.</span></span> <span data-ttu-id="daca9-108">Şirket içi Exchange varsa, böylece kullanıcılar bir şirket içi Exchange posta ile göndermek ve bu gruplardan e-postaları sonra geri bu grupları tooon içi yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="daca9-108">If you have Exchange on-premises, then you can write back these groups tooon-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span></span>

<span data-ttu-id="daca9-109">Office 365 grupları ve nasıl toouse bunları bulunabilir hakkında daha fazla bilgi [burada](http://aka.ms/O365g).</span><span class="sxs-lookup"><span data-stu-id="daca9-109">More information about Office 365 Groups and how toouse them can be found [here](http://aka.ms/O365g).</span></span>

<span data-ttu-id="daca9-110">Bir Office 365 grup şirket içi bir dağıtım grubu olarak temsil edilen AD DS.</span><span class="sxs-lookup"><span data-stu-id="daca9-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span></span> <span data-ttu-id="daca9-111">Şirket içi Exchange server'ınızı Exchange 2013 toplu güncelleştirme (Mart 2015'te yayımlanan) 8 veya Exchange 2016 toorecognize bu yeni grup türü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="daca9-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 toorecognize this new group type.</span></span>

<span data-ttu-id="daca9-112">**Merhaba Önizleme sırasında notları**</span><span class="sxs-lookup"><span data-stu-id="daca9-112">**Notes during hello preview**</span></span>

* <span data-ttu-id="daca9-113">Merhaba adres defteri özniteliği hello Önizleme'de şu anda doldurulmamış.</span><span class="sxs-lookup"><span data-stu-id="daca9-113">hello address book attribute is currently not populated in hello preview.</span></span> <span data-ttu-id="daca9-114">Bu öznitelik olmadan hello Grup hello GAL görünür değil.</span><span class="sxs-lookup"><span data-stu-id="daca9-114">Without this attribute, hello group is not visible in hello GAL.</span></span> <span data-ttu-id="daca9-115">en kolay yolu toopopulate hello toouse hello Exchange PowerShell cmdlet'ini bu özniteliktir `update-recipient`.</span><span class="sxs-lookup"><span data-stu-id="daca9-115">hello easiest way toopopulate this attribute is toouse hello Exchange PowerShell cmdlet `update-recipient`.</span></span>
* <span data-ttu-id="daca9-116">Yalnızca hello Exchange şema ormanlarla gruplar için geçerli hedefleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="daca9-116">Only forests with hello Exchange schema are valid targets for groups.</span></span> <span data-ttu-id="daca9-117">Hiçbir Exchange algılandı, sonra Grup geri yazma olası tooenable değildir.</span><span class="sxs-lookup"><span data-stu-id="daca9-117">If no Exchange was detected, then group writeback is not possible tooenable.</span></span>
* <span data-ttu-id="daca9-118">Şu anda yalnızca tek orman Exchange kuruluşu dağıtımlar desteklenir.</span><span class="sxs-lookup"><span data-stu-id="daca9-118">Only single-forest Exchange organization deployments are currently supported.</span></span> <span data-ttu-id="daca9-119">Birden fazla kuruluşun şirket içi Exchange varsa, daha sonra şirket içi GALSync çözümünü bu grupları tooappear için diğer ormanlara gerekir.</span><span class="sxs-lookup"><span data-stu-id="daca9-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups tooappear in your other forests.</span></span>
* <span data-ttu-id="daca9-120">Merhaba grup geri yazma özelliği, güvenlik grubu veya dağıtım grubu işlemez.</span><span class="sxs-lookup"><span data-stu-id="daca9-120">hello Group writeback feature does not handle security groups or distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="daca9-121">Grup geri yazma için bir abonelik tooAzure AD Premium gereklidir.</span><span class="sxs-lookup"><span data-stu-id="daca9-121">A subscription tooAzure AD Premium is required for group writeback.</span></span>
> 
>

## <a name="user-writeback"></a><span data-ttu-id="daca9-122">Kullanıcı geri yazma</span><span class="sxs-lookup"><span data-stu-id="daca9-122">User writeback</span></span>
> [!IMPORTANT]
> <span data-ttu-id="daca9-123">Merhaba kullanıcı geri yazma önizleme özelliği hello Ağustos 2015 güncelleştirmesi tooAzure AD kaldırıldı Bağlan.</span><span class="sxs-lookup"><span data-stu-id="daca9-123">hello user writeback preview feature was removed in hello August 2015 update tooAzure AD Connect.</span></span> <span data-ttu-id="daca9-124">Ardından etkinleştirdiyseniz, bu özellik devre dışı bırakmalısınız.</span><span class="sxs-lookup"><span data-stu-id="daca9-124">If you have enabled it, then you should disable this feature.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="daca9-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="daca9-125">Next steps</span></span>
<span data-ttu-id="daca9-126">Devam etmek, [Azure AD Connect özel yüklemesi](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="daca9-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

<span data-ttu-id="daca9-127">[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="daca9-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
