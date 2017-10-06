---
title: "Azure Active Directory aaaCharacteristics Kiracı intercaction | Microsoft Docs"
description: "Azure Active Kiracı kiracılarınız kiracılarınız tamamen bağımsız kaynaklar olarak anlayarak yönetme"
services: active-tenant
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 2b862b75-14df-45f2-a8ab-2a3ff1e2eb08
ms.service: active-tenant
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: 57b677665c7cb4aee63f518c39d26754fe71a999
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a><span data-ttu-id="cabe7-103">Birden çok Azure Active Directory kiracıları etkileşim anlama</span><span class="sxs-lookup"><span data-stu-id="cabe7-103">Understand how multiple Azure Active Directory tenants interact</span></span>

<span data-ttu-id="cabe7-104">Azure Active Directory (Azure AD), her Kiracı tamamen bağımsız bir kaynaktır: mantıksal olarak bağımsızdır bir eş hello yönettiğiniz diğer kiracılar.</span><span class="sxs-lookup"><span data-stu-id="cabe7-104">In Azure Active Directory (Azure AD), each tenent is a fully independent resource: a peer that is logically independent from hello other tenants that you manage.</span></span> <span data-ttu-id="cabe7-105">Kiracılar arasında üst-alt ilişkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="cabe7-105">There is no parent-child relationship between tenants.</span></span> <span data-ttu-id="cabe7-106">Kiracılar arasındaki bu bağımsızlığa kaynak bağımsızlığı, yönetim bağımsızlığı ve eşitleme bağımsızlığı dahildir.</span><span class="sxs-lookup"><span data-stu-id="cabe7-106">This independence between tenants includes resource independence, administrative independence, and synchronization independence.</span></span>

## <a name="resource-independence"></a><span data-ttu-id="cabe7-107">Kaynak bağımsızlığı</span><span class="sxs-lookup"><span data-stu-id="cabe7-107">Resource independence</span></span>
* <span data-ttu-id="cabe7-108">Oluşturursanız veya bir kiracı kaynak silin, dış kullanıcıların hello kısmi durumla başka bir kiracı herhangi bir kaynak üzerinde hiçbir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="cabe7-108">If you create or delete a resource in one tenant, it has no impact on any resource in another tenant, with hello partial exception of external users.</span></span> 
* <span data-ttu-id="cabe7-109">Bir kiracı ile etki alanı adlarından birini kullanırsanız, başka hiçbir kiracıyla kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="cabe7-109">If you use one of your domain names with one tenant, it cannot be used with any other tenant.</span></span>

## <a name="administrative-independence"></a><span data-ttu-id="cabe7-110">Yönetim bağımsızlığı</span><span class="sxs-lookup"><span data-stu-id="cabe7-110">Administrative independence</span></span>
<span data-ttu-id="cabe7-111">Kiracı 'Contoso' yönetici olmayan bir kullanıcı bir test Kiracı 'Test' ardından oluşturursa:</span><span class="sxs-lookup"><span data-stu-id="cabe7-111">If a non-administrative user of tenant 'Contoso' creates a test tenant 'Test,' then:</span></span>

* <span data-ttu-id="cabe7-112">Varsayılan olarak, bir kiracı oluşturur hello kullanıcının bir dış kullanıcı, yeni Kiracı ve Kiracı içinde atanan hello genel yönetici rolü olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="cabe7-112">By default, hello user who creates a tenant is added as an external user in that new tenant, and assigned hello global administrator role in that tenant.</span></span>
* <span data-ttu-id="cabe7-113">bir yönetici 'Test' özellikle vermediği sürece Kiracı 'Contoso' hello Yöneticiler hiçbir doğrudan yönetim ayrıcalıkları tootenant 'Test' sahiptir.</span><span class="sxs-lookup"><span data-stu-id="cabe7-113">hello administrators of tenant 'Contoso' have no direct administrative privileges tootenant 'Test,' unless an administrator of 'Test' specifically grants them these privileges.</span></span> <span data-ttu-id="cabe7-114">Ancak, 'Test' oluşturulan hello kullanıcı hesabı denetimi yöneticileri olarak 'Contoso' erişim tootenant 'Test' denetleyebilir</span><span class="sxs-lookup"><span data-stu-id="cabe7-114">However, administrators of 'Contoso' can control access tootenant 'Test' if they control hello user account that created 'Test.'</span></span>
* <span data-ttu-id="cabe7-115">Eklemek veya bir kullanıcı bir kiracı Yönetici rolü Kaldır, hello değişiklik değil etkileyen hello yönetici rolleri o hello yapar. kullanıcı başka bir kiracı sahiptir.</span><span class="sxs-lookup"><span data-stu-id="cabe7-115">If you add/remove an administrator role for a user in one tenant, hello change does not affect hello administrator roles that hello user has in another tenant.</span></span>

## <a name="synchronization-independence"></a><span data-ttu-id="cabe7-116">Eşitleme bağımsızlığı</span><span class="sxs-lookup"><span data-stu-id="cabe7-116">Synchronization independence</span></span>
<span data-ttu-id="cabe7-117">Her Azure yapılandırabilirsiniz AD Kiracı bağımsız olarak herhangi birinin tek bir örneğinden tooget verileri:</span><span class="sxs-lookup"><span data-stu-id="cabe7-117">You can configure each Azure AD tenant independently tooget data synchronized from a single instance of either:</span></span>

* <span data-ttu-id="cabe7-118">Hello Azure AD Connect aracı, tek bir AD ormanında toosynchronize verilerle.</span><span class="sxs-lookup"><span data-stu-id="cabe7-118">hello Azure AD Connect tool, toosynchronize data with a single AD forest.</span></span>
* <span data-ttu-id="cabe7-119">Azure Active Kiracı bağlayıcı için Forefront Identity Manager, bir toosynchronize verilerle hello veya daha fazla şirket içi ormanları ve/veya Azure olmayan AD veri kaynakları.</span><span class="sxs-lookup"><span data-stu-id="cabe7-119">hello Azure Active tenant Connector for Forefront Identity Manager, toosynchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span></span>

## <a name="add-an-azure-ad-tenant"></a><span data-ttu-id="cabe7-120">Azure AD kiracısı ekleme</span><span class="sxs-lookup"><span data-stu-id="cabe7-120">Add an Azure AD tenant</span></span>
<span data-ttu-id="cabe7-121">tooadd hello Azure portal, Azure AD kiracısında oturum çok[Azure portal hello](https://portal.azure.com) Azure AD genel yönetici olan bir hesapla, hello sol, seçin ve **yeni**.</span><span class="sxs-lookup"><span data-stu-id="cabe7-121">tooadd an Azure AD tenant in hello Azure portal, sign in too[hello Azure portal](https://portal.azure.com) with an account that is an Azure AD global administrator, and, on hello left, select **New**.</span></span>

> [!NOTE]
> <span data-ttu-id="cabe7-122">Diğer Azure kaynaklarının aksine, kiracılar bir Azure aboneliğinin alt kaynakları değildir.</span><span class="sxs-lookup"><span data-stu-id="cabe7-122">Unlike other Azure resources, your tenants are not child resources of an Azure subscription.</span></span> <span data-ttu-id="cabe7-123">Azure aboneliğinizin süresi doldu veya iptal edilirse, Kiracı verilerinizi Azure PowerShell, hello Azure grafik API'sini veya hello Office 365 Yönetim merkezini kullanarak erişmeye devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cabe7-123">If your Azure subscription is canceled or expired, you can still access your tenant data using Azure PowerShell, hello Azure Graph API, or hello Office 365 Admin Center.</span></span> <span data-ttu-id="cabe7-124">Ayrıca, başka bir abonelik hello Kiracı ile ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cabe7-124">You can also associate another subscription with hello tenant.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="cabe7-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cabe7-125">Next steps</span></span>
<span data-ttu-id="cabe7-126">Azure AD lisans sorunları ve en iyi yöntemler genel bakış için bkz: [ne olduğu Azure Active Kiracı lisans?](active-directory-licensing-whatis-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="cabe7-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active tenant licensing?](active-directory-licensing-whatis-azure-portal.md)</span></span>
