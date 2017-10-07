---
title: "Azure Active Directory kimlik koruması aaaEnabling | Microsoft Docs"
description: "Bilgi nasıl tooenable Azure Active Directory kimlik koruması."
services: active-directory
keywords: "Azure active directory kimlik koruması, cloud app discovery'yi, uygulamalar, güvenlik, risk, risk düzeyi, güvenlik açığı, güvenlik ilkesi yönetme"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f7a7ffaf-76bf-4cc7-96a1-86c944275c82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: d26f466f5c7d6a425528a277d98c2c4b341ff8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-active-directory-identity-protection"></a><span data-ttu-id="cf7ff-104">Azure Active Directory kimlik koruması etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="cf7ff-104">Enabling Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="cf7ff-105">Azure Active Directory kimlik koruması bildirimleri, düzeltme önerileri ve risk tabanlı ilkeleri korumanıza yardımcı olur ve oturum açma kuşkulu etkinlikleri ve olası güvenlik açıklarını birleştirilmiş bir görünüm sağlayan yeni bir özellik olan işinizi.</span><span class="sxs-lookup"><span data-stu-id="cf7ff-105">Azure Active Directory Identity Protection is a new capability that provides a consolidated view into suspicious sign-in activities and potential vulnerabilities and with notifications, remediation recommendations and risk-based policies helps you protect your business.</span></span> 

<span data-ttu-id="cf7ff-106">Merhaba hizmeti kuşkulu etkinlikleri saldırıları, son kullanıcı ve ayrıcalıklı (Yönetici) kimlikler sinyalleri kaba gibi temel zorlamak için sızmasını kimlik bilgileri, tanınmayan konumlardan oturum algılar etkilenen cihazlar, bu etkinlikler gerçek zamanlı karşı tooprotect.</span><span class="sxs-lookup"><span data-stu-id="cf7ff-106">hello service detects suspicious activities for end user and privileged (admin) identities based on signals like brute force attacks, leaked credentials, sign ins from unfamiliar locations, infected devices, tooprotect against these activities in real-time.</span></span> <span data-ttu-id="cf7ff-107">Daha da önemlisi, şüpheli etkinliklere dayalı olarak, bir kullanıcı risk önem derecesi hesaplanır ve risk tabanlı ilkeleri yapılandırılabilir ve hello kimlikleri, kuruluşunuzun otomatik olarak koruma.</span><span class="sxs-lookup"><span data-stu-id="cf7ff-107">More importantly, based on these suspicious activities, a user risk severity is computed and risk-based policies can be configured and automatically protect hello identities of your organization.</span></span> <span data-ttu-id="cf7ff-108">Daha fazla ayrıntı için bkz: [Azure Active Directory kimlik koruması](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="cf7ff-108">For more details, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

<span data-ttu-id="cf7ff-109">Bu konular gösterir nasıl tooenable Azure Active Directory kimlik koruması.</span><span class="sxs-lookup"><span data-stu-id="cf7ff-109">This topics shows how tooenable Azure Active Directory Identity Protection.</span></span>

## <a name="steps-tooenable-azure-active-directory-identity-protection"></a><span data-ttu-id="cf7ff-110">Adımları tooenable Azure Active Directory kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="cf7ff-110">Steps tooenable Azure Active Directory Identity Protection</span></span>
1. <span data-ttu-id="cf7ff-111">[Oturum açma](https://ms.portal.azure.com/) tooyour Azure portalına genel yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="cf7ff-111">[Sign-on](https://ms.portal.azure.com/) tooyour Azure portal as global administrator.</span></span> 
2. <span data-ttu-id="cf7ff-112">Hello Azure portal'ı tıklatın **Market**.</span><span class="sxs-lookup"><span data-stu-id="cf7ff-112">In hello Azure portal, click **Marketplace**.</span></span>
   
    <span data-ttu-id="cf7ff-113">![Oluşturma](./media/active-directory-identityprotection-enable/01.png "oluşturma")</span><span class="sxs-lookup"><span data-stu-id="cf7ff-113">![Create](./media/active-directory-identityprotection-enable/01.png "Create")</span></span>
3. <span data-ttu-id="cf7ff-114">Merhaba uygulamalar listesinde tıklayın **güvenlik + kimlik**.</span><span class="sxs-lookup"><span data-stu-id="cf7ff-114">In hello applications list, click **Security + Identity**.</span></span>
   
    <span data-ttu-id="cf7ff-115">![Oluşturma](./media/active-directory-identityprotection-enable/02.png "oluşturma")</span><span class="sxs-lookup"><span data-stu-id="cf7ff-115">![Create](./media/active-directory-identityprotection-enable/02.png "Create")</span></span>
4. <span data-ttu-id="cf7ff-116">Tıklatın **Azure AD kimlik koruması**.</span><span class="sxs-lookup"><span data-stu-id="cf7ff-116">Click **Azure AD Identity Protection**.</span></span>
   
    <span data-ttu-id="cf7ff-117">![Oluşturma](./media/active-directory-identityprotection-enable/03.png "oluşturma")</span><span class="sxs-lookup"><span data-stu-id="cf7ff-117">![Create](./media/active-directory-identityprotection-enable/03.png "Create")</span></span>
5. <span data-ttu-id="cf7ff-118">Merhaba üzerinde **Azure AD Identity Protection** dikey penceresinde tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="cf7ff-118">On hello **Azure AD Identity Protection** blade, click **Create**.</span></span>
   
    <span data-ttu-id="cf7ff-119">![Oluşturma](./media/active-directory-identityprotection-enable/04.png "oluşturma")</span><span class="sxs-lookup"><span data-stu-id="cf7ff-119">![Create](./media/active-directory-identityprotection-enable/04.png "Create")</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf7ff-120">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="cf7ff-120">Next Steps</span></span>
* [<span data-ttu-id="cf7ff-121">Azure Active Directory kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="cf7ff-121">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

