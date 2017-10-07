---
title: "Azure Güvenlik Merkezi'nde aaaPermissions | Microsoft Docs"
description: "Bu makalede Azure Güvenlik Merkezi rol tabanlı erişim denetimi tooassign izinleri toousers nasıl kullandığı açıklanmıştır ve Eylemler her rol için izin verilen hello tanımlar."
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a><span data-ttu-id="99f05-103">Azure Güvenlik Merkezi'nde izinleri</span><span class="sxs-lookup"><span data-stu-id="99f05-103">Permissions in Azure Security Center</span></span>

<span data-ttu-id="99f05-104">Azure Güvenlik Merkezi kullanan [rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-configure.md), sağlayan [yerleşik roller](../active-directory/role-based-access-built-in-roles.md) atanabilen toousers, grupları ve Azure Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="99f05-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned toousers, groups, and services in Azure.</span></span>

<span data-ttu-id="99f05-105">Güvenlik Merkezi kaynakları tooidentify güvenlik sorunları ve güvenlik açıkları hello yapılandırmasını değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="99f05-105">Security Center assesses hello configuration of your resources tooidentify security issues and vulnerabilities.</span></span> <span data-ttu-id="99f05-106">Güvenlik Merkezi'nde, yalnızca bilgi sahibi, katkıda bulunan veya okuyucu bir kaynağa ait hello abonelik veya kaynak grubu için hello rolüne atandığında ilgili tooa kaynak.</span><span class="sxs-lookup"><span data-stu-id="99f05-106">In Security Center, you only see information related tooa resource when you are assigned hello role of Owner, Contributor, or Reader for hello subscription or resource group that a resource belongs to.</span></span>

<span data-ttu-id="99f05-107">Toplama toothese rollerinde iki belirli Güvenlik Merkezi rolü vardır:</span><span class="sxs-lookup"><span data-stu-id="99f05-107">In addition toothese roles, there are two specific Security Center roles:</span></span>

* <span data-ttu-id="99f05-108">**Güvenlik okuyucu**: toothis role ait olan bir kullanıcı hakları tooSecurity merkezi görüntüleme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="99f05-108">**Security Reader**: A user that belongs toothis role has viewing rights tooSecurity Center.</span></span> <span data-ttu-id="99f05-109">Merhaba kullanıcı öneriler, uyarılar, bir güvenlik ilkesi ve güvenlik durumları görüntüleyebilir ancak değişiklik yapamazsınız.</span><span class="sxs-lookup"><span data-stu-id="99f05-109">hello user can view recommendations, alerts, a security policy, and security states, but cannot make changes.</span></span>
* <span data-ttu-id="99f05-110">**Güvenlik Yöneticisi**: toothis rolüne ait kullanıcı aynı hakları güvenlik okuyucu hello hello sahip ve aynı zamanda hello güvenlik ilkesi güncelleştirebilir ve uyarısı ve öneri yok sayın.</span><span class="sxs-lookup"><span data-stu-id="99f05-110">**Security Administrator**: A user that belongs toothis role has hello same rights as hello Security Reader and can also update hello security policy and dismiss alerts and recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="99f05-111">Merhaba güvenlik rolleri, güvenlik okuyucu ve Güvenlik Yöneticisi, yalnızca Güvenlik Merkezi'nde erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99f05-111">hello security roles, Security Reader and Security Administrator, have access only in Security Center.</span></span> <span data-ttu-id="99f05-112">Merhaba güvenlik rolleri Azure depolama, Web ve mobil veya nesnelerin interneti gibi erişim tooother hizmet alanlarına sahip değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="99f05-112">hello security roles do not have access tooother service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>
>
>

## <a name="roles-and-allowed-actions"></a><span data-ttu-id="99f05-113">Rol ve izin verilen eylemleri</span><span class="sxs-lookup"><span data-stu-id="99f05-113">Roles and allowed actions</span></span>

<span data-ttu-id="99f05-114">Merhaba aşağıdaki tabloda rollerini görüntüler ve Güvenlik Merkezi'nde Eylemler izin.</span><span class="sxs-lookup"><span data-stu-id="99f05-114">hello following table displays roles and allowed actions in Security Center.</span></span> <span data-ttu-id="99f05-115">Bir X hello eylem bu rol için izin verildiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="99f05-115">An X indicates that hello action is allowed for that role.</span></span>

| <span data-ttu-id="99f05-116">Rol</span><span class="sxs-lookup"><span data-stu-id="99f05-116">Role</span></span> | <span data-ttu-id="99f05-117">Güvenlik ilkesini Düzenle</span><span class="sxs-lookup"><span data-stu-id="99f05-117">Edit security policy</span></span> | <span data-ttu-id="99f05-118">Bir kaynak için güvenlik önerilerini uygulama</span><span class="sxs-lookup"><span data-stu-id="99f05-118">Apply security recommendations for a resource</span></span> | <span data-ttu-id="99f05-119">Uyarılar ve öneriler kapatın</span><span class="sxs-lookup"><span data-stu-id="99f05-119">Dismiss alerts and recommendations</span></span> | <span data-ttu-id="99f05-120">Uyarıları görüntüle ve öneriler</span><span class="sxs-lookup"><span data-stu-id="99f05-120">View alerts and recommendations</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="99f05-121">Abonelik sahibi</span><span class="sxs-lookup"><span data-stu-id="99f05-121">Subscription Owner</span></span> | <span data-ttu-id="99f05-122">X</span><span class="sxs-lookup"><span data-stu-id="99f05-122">X</span></span> | <span data-ttu-id="99f05-123">X</span><span class="sxs-lookup"><span data-stu-id="99f05-123">X</span></span> | <span data-ttu-id="99f05-124">X</span><span class="sxs-lookup"><span data-stu-id="99f05-124">X</span></span> | <span data-ttu-id="99f05-125">X</span><span class="sxs-lookup"><span data-stu-id="99f05-125">X</span></span> |
| <span data-ttu-id="99f05-126">Abonelik katkıda bulunan</span><span class="sxs-lookup"><span data-stu-id="99f05-126">Subscription Contributor</span></span> | <span data-ttu-id="99f05-127">X</span><span class="sxs-lookup"><span data-stu-id="99f05-127">X</span></span> | <span data-ttu-id="99f05-128">X</span><span class="sxs-lookup"><span data-stu-id="99f05-128">X</span></span> | <span data-ttu-id="99f05-129">X</span><span class="sxs-lookup"><span data-stu-id="99f05-129">X</span></span> | <span data-ttu-id="99f05-130">X</span><span class="sxs-lookup"><span data-stu-id="99f05-130">X</span></span> |
| <span data-ttu-id="99f05-131">Kaynak grubunun sahibi</span><span class="sxs-lookup"><span data-stu-id="99f05-131">Resource Group Owner</span></span> | -- | <span data-ttu-id="99f05-132">X</span><span class="sxs-lookup"><span data-stu-id="99f05-132">X</span></span> | -- | <span data-ttu-id="99f05-133">X</span><span class="sxs-lookup"><span data-stu-id="99f05-133">X</span></span> |
| <span data-ttu-id="99f05-134">Kaynak grubu katkıda bulunan</span><span class="sxs-lookup"><span data-stu-id="99f05-134">Resource Group Contributor</span></span> | -- | <span data-ttu-id="99f05-135">X</span><span class="sxs-lookup"><span data-stu-id="99f05-135">X</span></span> | -- | <span data-ttu-id="99f05-136">X</span><span class="sxs-lookup"><span data-stu-id="99f05-136">X</span></span> |
| <span data-ttu-id="99f05-137">Okuyucu</span><span class="sxs-lookup"><span data-stu-id="99f05-137">Reader</span></span> | -- | -- | -- | <span data-ttu-id="99f05-138">X</span><span class="sxs-lookup"><span data-stu-id="99f05-138">X</span></span> |
| <span data-ttu-id="99f05-139">Güvenlik Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="99f05-139">Security Administrator</span></span> | <span data-ttu-id="99f05-140">X</span><span class="sxs-lookup"><span data-stu-id="99f05-140">X</span></span> | -- | <span data-ttu-id="99f05-141">X</span><span class="sxs-lookup"><span data-stu-id="99f05-141">X</span></span> | <span data-ttu-id="99f05-142">X</span><span class="sxs-lookup"><span data-stu-id="99f05-142">X</span></span> |
| <span data-ttu-id="99f05-143">Güvenlik okuyucusu</span><span class="sxs-lookup"><span data-stu-id="99f05-143">Security Reader</span></span> | -- | -- | -- | <span data-ttu-id="99f05-144">X</span><span class="sxs-lookup"><span data-stu-id="99f05-144">X</span></span> |

> [!NOTE]
> <span data-ttu-id="99f05-145">Merhaba atamanızı öneririz az izin veren rol görevlerini kullanıcılar toocomplete için gerekli.</span><span class="sxs-lookup"><span data-stu-id="99f05-145">We recommend that you assign hello least permissive role needed for users toocomplete their tasks.</span></span> <span data-ttu-id="99f05-146">Örneğin, bir kaynak hello güvenlik durumu hakkındaki bilgileri tooview yeterlidir ancak önerileri uygulamak veya ilkeleri düzenleme gibi bir eylemde bulunmamasını hello okuyucu rolü toousers atayın.</span><span class="sxs-lookup"><span data-stu-id="99f05-146">For example, assign hello Reader role toousers who only need tooview information about hello security health of a resource but not take action, such as applying recommendations or editing policies.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="99f05-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="99f05-147">Next steps</span></span>
<span data-ttu-id="99f05-148">Bu makalede, Güvenlik Merkezi RBAC tooassign izinleri toousers nasıl kullandığı açıklanmıştır ve Eylemler her rol için izin verilen hello tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="99f05-148">This article explained how Security Center uses RBAC tooassign permissions toousers and identified hello allowed actions for each role.</span></span> <span data-ttu-id="99f05-149">Toomonitor hello aboneliğinizi güvenlik durumunu hello rol atamalarını ile tanıdık, güvenlik ilkeleri, düzenleme ve önerileri geçerlidir, öğrenme nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="99f05-149">Now that you're familiar with hello role assignments needed toomonitor hello security state of your subscription, edit security policies, and apply recommendations, learn how to:</span></span>

- [<span data-ttu-id="99f05-150">Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="99f05-150">Set security policies in Security Center</span></span>](security-center-policies.md)
- [<span data-ttu-id="99f05-151">Güvenlik Merkezi'nde güvenlik önerilerini yönetme</span><span class="sxs-lookup"><span data-stu-id="99f05-151">Manage security recommendations in Security Center</span></span>](security-center-recommendations.md)
- [<span data-ttu-id="99f05-152">Hello Azure kaynaklarınızın güvenlik durumunu izleme</span><span class="sxs-lookup"><span data-stu-id="99f05-152">Monitor hello security health of your Azure resources</span></span>](security-center-monitoring.md)
- [<span data-ttu-id="99f05-153">Yönetme ve Güvenlik Merkezi'nde toosecurity uyarılarını yanıtlama</span><span class="sxs-lookup"><span data-stu-id="99f05-153">Manage and respond toosecurity alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
- [<span data-ttu-id="99f05-154">İş ortağı güvenlik çözümlerini izleme</span><span class="sxs-lookup"><span data-stu-id="99f05-154">Monitor partner security solutions</span></span>](security-center-partner-solutions.md)
