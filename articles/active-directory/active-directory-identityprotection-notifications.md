---
title: "aaaAzure Active Directory kimlik koruması bildirimleri | Microsoft Docs"
description: "Bildirimleri araştırma etkinliklerinizi'ı nasıl desteklediğini öğrenin."
services: active-directory
keywords: "Azure active directory kimlik koruması, cloud app discovery'yi, uygulamalar, güvenlik, risk, risk düzeyi, güvenlik açığı, güvenlik ilkesi yönetme"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 65ca79b9-4da1-4d5b-bebd-eda776cc32c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 19e62374873f034591c658a779f97d935766c612
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a><span data-ttu-id="75555-104">Azure Active Directory kimlik koruması bildirimleri</span><span class="sxs-lookup"><span data-stu-id="75555-104">Azure Active Directory Identity Protection notifications</span></span>
<span data-ttu-id="75555-105">Azure AD kimlik koruması iki tür otomatik bildirim e-postalar yönettiğiniz toohelp kullanıcı risk ve risk olaylarını gönderir:</span><span class="sxs-lookup"><span data-stu-id="75555-105">Azure AD Identity Protection sends two types of automated notification emails toohelp you manage user risk and risk events:</span></span>

* <span data-ttu-id="75555-106">Kullanıcı uyarı e-posta güvenliği</span><span class="sxs-lookup"><span data-stu-id="75555-106">User compromised alert email</span></span>
* <span data-ttu-id="75555-107">Haftalık Özet e-posta</span><span class="sxs-lookup"><span data-stu-id="75555-107">Weekly digest email</span></span>

## <a name="user-compromised-alert-email"></a><span data-ttu-id="75555-108">Kullanıcı uyarı e-posta güvenliği</span><span class="sxs-lookup"><span data-stu-id="75555-108">User compromised alert email</span></span>
<span data-ttu-id="75555-109">Azure AD Identity Protection tehlikeye gibi bir hesap belirlediğinde kullanıcı güvenliği aşılmış bir e-posta uyarısı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="75555-109">A user compromised email alert is generated when Azure AD Identity Protection identifies an account as compromised.</span></span> <span data-ttu-id="75555-110">Merhaba e-posta bayrak eklenen kullanıcılar hello Identity Protection panosunda risk rapor için bir bağlantı toohello içerir.</span><span class="sxs-lookup"><span data-stu-id="75555-110">hello email includes a link toohello Users flagged for risk report in hello Identity Protection dashboard.</span></span> <span data-ttu-id="75555-111">Güvenliği aşılmış hesapları bildirimleri hemen araştırın öneririz.</span><span class="sxs-lookup"><span data-stu-id="75555-111">We recommend that you immediately investigate notifications of compromised accounts.</span></span>

## <a name="weekly-digest-email"></a><span data-ttu-id="75555-112">Haftalık Özet e-posta</span><span class="sxs-lookup"><span data-stu-id="75555-112">Weekly digest email</span></span>
<span data-ttu-id="75555-113">Merhaba Haftalık Özet e-posta yeni risk olaylarını özetini içerir.</span><span class="sxs-lookup"><span data-stu-id="75555-113">hello weekly digest email contains a summary of new risk events.</span></span><br>
<span data-ttu-id="75555-114">Aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="75555-114">It includes:</span></span>

* <span data-ttu-id="75555-115">Risk altındaki kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="75555-115">Users at risk</span></span>
* <span data-ttu-id="75555-116">Kuşkulu etkinlikler</span><span class="sxs-lookup"><span data-stu-id="75555-116">Suspicious activities</span></span>
* <span data-ttu-id="75555-117">Algılanan güvenlik açıkları</span><span class="sxs-lookup"><span data-stu-id="75555-117">Detected vulnerabilities</span></span>
* <span data-ttu-id="75555-118">Kimlik koruması raporlarda bağlantılar toohello ilgili</span><span class="sxs-lookup"><span data-stu-id="75555-118">Links toohello related reports in Identity Protection</span></span>

<br><span data-ttu-id="75555-119">
![Düzeltme](./media/active-directory-identityprotection-notifications/400.png "düzeltme")
</span><span class="sxs-lookup"><span data-stu-id="75555-119">
![Remediation](./media/active-directory-identityprotection-notifications/400.png "Remediation")
</span></span><br>

<span data-ttu-id="75555-120">Haftalık Özet e-posta gönderme devre dışı geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75555-120">You can switch sending a weekly digest email off.</span></span>
<br><br><span data-ttu-id="75555-121">
![Kullanıcı riskleri](./media/active-directory-identityprotection-notifications/62.png "kullanıcı riskleri")
</span><span class="sxs-lookup"><span data-stu-id="75555-121">
![User risks](./media/active-directory-identityprotection-notifications/62.png "User risks")
</span></span><br>

<span data-ttu-id="75555-122">**tooopen hello ilgili yapılandırma iletişim**:</span><span class="sxs-lookup"><span data-stu-id="75555-122">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="75555-123">Merhaba üzerinde **Azure AD Identity Protection** dikey penceresinde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="75555-123">On hello **Azure AD Identity Protection** blade, click **Settings**.</span></span>
   <br><br><span data-ttu-id="75555-124">
   ![Kullanıcı risk ilkesine](./media/active-directory-identityprotection-notifications/401.png "kullanıcı risk İlkesi")
   </span><span class="sxs-lookup"><span data-stu-id="75555-124">
![User risk policy](./media/active-directory-identityprotection-notifications/401.png "User risk policy")
</span></span><br>
2. <span data-ttu-id="75555-125">Merhaba, **genel** 'yi tıklatın **bildirimleri**.</span><span class="sxs-lookup"><span data-stu-id="75555-125">In hello **General** section, click **Notifications**.</span></span>
   <br><br><span data-ttu-id="75555-126">
   ![Kullanıcı risk ilkesine](./media/active-directory-identityprotection-notifications/405.png "kullanıcı risk İlkesi")
   </span><span class="sxs-lookup"><span data-stu-id="75555-126">
![User risk policy](./media/active-directory-identityprotection-notifications/405.png "User risk policy")
</span></span><br>

## <a name="see-also"></a><span data-ttu-id="75555-127">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="75555-127">See also</span></span>
* [<span data-ttu-id="75555-128">Azure Active Directory kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="75555-128">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
