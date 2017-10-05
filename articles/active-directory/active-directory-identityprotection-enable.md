---
title: "Azure Active Directory kimlik koruması etkinleştirme | Microsoft Docs"
description: "Azure Active Directory kimlik koruması etkinleştirmeyi öğrenin."
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
ms.openlocfilehash: e0683e837086ca08f4b4b3f49695bdd2b4063ea4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="enabling-azure-active-directory-identity-protection"></a><span data-ttu-id="08e9b-104">Azure Active Directory kimlik koruması etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="08e9b-104">Enabling Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="08e9b-105">Azure Active Directory kimlik koruması bildirimleri, düzeltme önerileri ve risk tabanlı ilkeleri korumanıza yardımcı olur ve oturum açma kuşkulu etkinlikleri ve olası güvenlik açıklarını birleştirilmiş bir görünüm sağlayan yeni bir özellik olan işinizi.</span><span class="sxs-lookup"><span data-stu-id="08e9b-105">Azure Active Directory Identity Protection is a new capability that provides a consolidated view into suspicious sign-in activities and potential vulnerabilities and with notifications, remediation recommendations and risk-based policies helps you protect your business.</span></span> 

<span data-ttu-id="08e9b-106">Hizmet, son kullanıcı ve ayrıcalıklı (Yönetici) kimlikler şüpheli etkinlikleri oturum açmalar tanınmayan konumlardan etkilenen cihazlar, bu etkinlikler gerçek zamanlı karşı korumak için kimlik bilgileri, sızmasını, deneme yanılma saldırıları gibi sinyalleri temel algılar.</span><span class="sxs-lookup"><span data-stu-id="08e9b-106">The service detects suspicious activities for end user and privileged (admin) identities based on signals like brute force attacks, leaked credentials, sign ins from unfamiliar locations, infected devices, to protect against these activities in real-time.</span></span> <span data-ttu-id="08e9b-107">Daha da önemlisi, şüpheli etkinliklere dayalı olarak, bir kullanıcı risk önem derecesi hesaplanır ve risk tabanlı ilkeleri yapılandırılabilir ve otomatik olarak kuruluşunuzun kimlikleri korumak.</span><span class="sxs-lookup"><span data-stu-id="08e9b-107">More importantly, based on these suspicious activities, a user risk severity is computed and risk-based policies can be configured and automatically protect the identities of your organization.</span></span> <span data-ttu-id="08e9b-108">Daha fazla ayrıntı için bkz: [Azure Active Directory kimlik koruması](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="08e9b-108">For more details, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

<span data-ttu-id="08e9b-109">Bu konular, Azure Active Directory kimlik koruması etkinleştirme gösterir.</span><span class="sxs-lookup"><span data-stu-id="08e9b-109">This topics shows how to enable Azure Active Directory Identity Protection.</span></span>

## <a name="steps-to-enable-azure-active-directory-identity-protection"></a><span data-ttu-id="08e9b-110">Azure Active Directory kimlik koruması etkinleştirme adımları</span><span class="sxs-lookup"><span data-stu-id="08e9b-110">Steps to enable Azure Active Directory Identity Protection</span></span>
1. <span data-ttu-id="08e9b-111">[Oturum açma](https://ms.portal.azure.com/) , Azure portalına genel yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="08e9b-111">[Sign-on](https://ms.portal.azure.com/) to your Azure portal as global administrator.</span></span> 
2. <span data-ttu-id="08e9b-112">Azure portalında tıklatın **Market**.</span><span class="sxs-lookup"><span data-stu-id="08e9b-112">In the Azure portal, click **Marketplace**.</span></span>
   
    <span data-ttu-id="08e9b-113">![Oluşturma](./media/active-directory-identityprotection-enable/01.png "oluşturma")</span><span class="sxs-lookup"><span data-stu-id="08e9b-113">![Create](./media/active-directory-identityprotection-enable/01.png "Create")</span></span>
3. <span data-ttu-id="08e9b-114">Uygulamalar listesinde tıklayın **güvenlik + kimlik**.</span><span class="sxs-lookup"><span data-stu-id="08e9b-114">In the applications list, click **Security + Identity**.</span></span>
   
    <span data-ttu-id="08e9b-115">![Oluşturma](./media/active-directory-identityprotection-enable/02.png "oluşturma")</span><span class="sxs-lookup"><span data-stu-id="08e9b-115">![Create](./media/active-directory-identityprotection-enable/02.png "Create")</span></span>
4. <span data-ttu-id="08e9b-116">Tıklatın **Azure AD kimlik koruması**.</span><span class="sxs-lookup"><span data-stu-id="08e9b-116">Click **Azure AD Identity Protection**.</span></span>
   
    <span data-ttu-id="08e9b-117">![Oluşturma](./media/active-directory-identityprotection-enable/03.png "oluşturma")</span><span class="sxs-lookup"><span data-stu-id="08e9b-117">![Create](./media/active-directory-identityprotection-enable/03.png "Create")</span></span>
5. <span data-ttu-id="08e9b-118">Üzerinde **Azure AD Identity Protection** dikey penceresinde tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="08e9b-118">On the **Azure AD Identity Protection** blade, click **Create**.</span></span>
   
    <span data-ttu-id="08e9b-119">![Oluşturma](./media/active-directory-identityprotection-enable/04.png "oluşturma")</span><span class="sxs-lookup"><span data-stu-id="08e9b-119">![Create](./media/active-directory-identityprotection-enable/04.png "Create")</span></span>

## <a name="next-steps"></a><span data-ttu-id="08e9b-120">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="08e9b-120">Next Steps</span></span>
* [<span data-ttu-id="08e9b-121">Azure Active Directory kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="08e9b-121">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

