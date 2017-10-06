---
title: "Azure Active Directory'de aaaDedicated gruplarını | Microsoft Docs"
description: "Azure Active Directory ve nasıl oluşturulduğunu nasıl ayrılmış gruplar işlerinde genel bakış."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="e872a-103">Azure Active Directory'de ayrılmış gruplar</span><span class="sxs-lookup"><span data-stu-id="e872a-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="e872a-104">Azure Active Directory'de (Azure AD), hello ayrılmış gruplar özelliği otomatik olarak oluşturur ve önceden tanımlanmış Azure AD grupları üyeliğini doldurur.</span><span class="sxs-lookup"><span data-stu-id="e872a-104">In Azure Active Directory (Azure AD), hello dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="e872a-105">Ayrılmış gruplarının üyeleri eklenemez veya kaldırılan kullanarak hello Azure Klasik portalı, Windows PowerShell cmdlet'lerini veya program aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="e872a-105">Members of dedicated groups cannot be added or removed using hello Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="e872a-106">Bir Azure AD Premium lisansı atanmış ayrılmış gruplar gerektirir</span><span class="sxs-lookup"><span data-stu-id="e872a-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="e872a-107">Merhaba grupta kuralı yöneten hello Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="e872a-107">hello administrator who manages hello rule on a group</span></span>
> * <span data-ttu-id="e872a-108">toobe hello grubunun bir üyesi tarafından hello seçilen tüm kullanıcılar kural</span><span class="sxs-lookup"><span data-stu-id="e872a-108">all users who are selected by hello rule toobe a member of hello group</span></span>
>
>

<span data-ttu-id="e872a-109">**ayrılmış tooenable grupları**</span><span class="sxs-lookup"><span data-stu-id="e872a-109">**tooenable dedicated groups**</span></span>

1. <span data-ttu-id="e872a-110">Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com)seçin **Active Directory**ve ardından, kuruluşunuzun dizininde açın.</span><span class="sxs-lookup"><span data-stu-id="e872a-110">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="e872a-111">Select hello **grupları** sekmesini ve ardından açık hello grubu tooedit.</span><span class="sxs-lookup"><span data-stu-id="e872a-111">Select hello **Groups** tab, and then open hello group you want tooedit.</span></span>
3. <span data-ttu-id="e872a-112">Select hello **yapılandırma** sekmesini tıklatın ve ardından **ayrılmış gruplar etkinleştirmek** çok**Evet**.</span><span class="sxs-lookup"><span data-stu-id="e872a-112">Select hello **Configure** tab, and then set **Enable Dedicated Groups** too**Yes**.</span></span>

<span data-ttu-id="e872a-113">Ayrılmış gruplar etkinleştirmek geçiş hello çok ayarlandıktan sonra**Evet**, daha fazla etkinleştirebilirsiniz hello dizin tooautomatically ayarı hello tarafından hello tüm kullanıcılar ayrılmış Grup Oluştur **etkinleştir "Tüm kullanıcılar" grubu** çok geçiş**Evet**.</span><span class="sxs-lookup"><span data-stu-id="e872a-113">Once hello Enable Dedicated Groups switch is set too**Yes**, you can further enable hello directory tooautomatically create hello All Users dedicated group by setting hello **Enable “All Users” Group** switch too**Yes**.</span></span> <span data-ttu-id="e872a-114">Sonra da bu adanmış grubunun hello adı hello yazarak düzenleyebilirsiniz **"Tüm kullanıcılar" için görünen ad grup** alan.</span><span class="sxs-lookup"><span data-stu-id="e872a-114">You can then also edit hello name of this dedicated group by typing it in hello **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="e872a-115">Merhaba tüm kullanıcılar Grup kullanılabilir tooassign hello dizininizdeki aynı izinleri tooall hello kullanıcılara.</span><span class="sxs-lookup"><span data-stu-id="e872a-115">hello All Users group can be used tooassign hello same permissions tooall hello users in your directory.</span></span> <span data-ttu-id="e872a-116">Örneğin, hello tüm kullanıcılar ayrılmış Grup toothis uygulama için erişim atayarak tüm kullanıcılar, dizin erişim tooa SaaS uygulamasına verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e872a-116">For example, you can grant all users in your directory access tooa SaaS application by assigning access for hello All Users dedicated group toothis application.</span></span>

<span data-ttu-id="e872a-117">ayrılmış hello tüm kullanıcılar Grup konuklar ve dış kullanıcılar dahil olmak üzere hello dizinde tüm kullanıcıları içerir.</span><span class="sxs-lookup"><span data-stu-id="e872a-117">hello dedicated All Users group includes all users in hello directory, including guests and external users.</span></span> <span data-ttu-id="e872a-118">Bir grup ihtiyacınız varsa, dış kullanıcılar hariç, ardından bir öznitelik tabanlı dinamik kuralı ile Merhaba aşağıdaki gibi bir grup oluşturarak bunu gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e872a-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as hello following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="e872a-119">Tüm konuklar dışlar bir grup için bir kural hello aşağıdaki gibi kullanın:</span><span class="sxs-lookup"><span data-stu-id="e872a-119">For a group that excludes all Guests, use a rule such as hello following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="e872a-120">konusunda toolearn toocreate *Gelişmiş* kuralları (birden çok karşılaştırma içeren kurallar) dinamik grup üyeliği için bkz: [öznitelikleri toocreate kullanarak gelişmiş kurallar](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="e872a-120">toolearn about how toocreate *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes toocreate advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="e872a-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e872a-121">Next steps</span></span>
<span data-ttu-id="e872a-122">Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e872a-122">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="e872a-123">Azure Active Directory grupları ile erişim tooresources yönetme</span><span class="sxs-lookup"><span data-stu-id="e872a-123">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="e872a-124">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="e872a-124">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="e872a-125">Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e872a-125">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="e872a-126">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="e872a-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
