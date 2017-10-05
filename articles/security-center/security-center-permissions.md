---
title: "Azure Güvenlik Merkezi'nde izinleri | Microsoft Docs"
description: "Bu makalede, rol tabanlı erişim denetimini Azure Güvenlik Merkezi kullanıcılara izinler atamak için nasıl kullandığını açıklar ve her rol için izin verilen eylemleri tanımlar."
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
ms.openlocfilehash: 0aaa99dda44d2020afd3e841e84020eb4ff87a85
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="permissions-in-azure-security-center"></a><span data-ttu-id="6bdb6-103">Azure Güvenlik Merkezi'nde izinleri</span><span class="sxs-lookup"><span data-stu-id="6bdb6-103">Permissions in Azure Security Center</span></span>

<span data-ttu-id="6bdb6-104">Azure Güvenlik Merkezi, Azure'daki kullanıcılara, gruplara ve hizmetlere atanabilen [yerleşik roller](../active-directory/role-based-access-built-in-roles.md) sağlayan [Rol Tabanlı Erişim Denetimi'ni (RBAC)](../active-directory/role-based-access-control-configure.md) kullanır.</span><span class="sxs-lookup"><span data-stu-id="6bdb6-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned to users, groups, and services in Azure.</span></span>

<span data-ttu-id="6bdb6-105">Güvenlik Merkezi güvenlik sorunları ve güvenlik açıklarını tanımlamak için kaynaklarınızı yapılandırmasını değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="6bdb6-105">Security Center assesses the configuration of your resources to identify security issues and vulnerabilities.</span></span> <span data-ttu-id="6bdb6-106">Güvenlik Merkezi'nde, yalnızca kaynak sahibi, katkıda bulunan veya okuyucu rolü abonelik veya kaynak ait olduğu kaynak grubu için atandığında ilgili bilgileri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bdb6-106">In Security Center, you only see information related to a resource when you are assigned the role of Owner, Contributor, or Reader for the subscription or resource group that a resource belongs to.</span></span>

<span data-ttu-id="6bdb6-107">Bu rollere ek olarak iki özel Güvenlik Merkezi rolü vardır:</span><span class="sxs-lookup"><span data-stu-id="6bdb6-107">In addition to these roles, there are two specific Security Center roles:</span></span>

* <span data-ttu-id="6bdb6-108">**Güvenlik okuyucu**: Bu role ait olan bir kullanıcı haklarını Güvenlik Merkezi'ne görüntüleme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="6bdb6-108">**Security Reader**: A user that belongs to this role has viewing rights to Security Center.</span></span> <span data-ttu-id="6bdb6-109">Kullanıcı öneriler, uyarılar, bir güvenlik ilkesi ve güvenlik durumları görüntüleyebilir ancak değişiklik yapamazsınız.</span><span class="sxs-lookup"><span data-stu-id="6bdb6-109">The user can view recommendations, alerts, a security policy, and security states, but cannot make changes.</span></span>
* <span data-ttu-id="6bdb6-110">**Güvenlik Yöneticisi**: Bu role ait bir kullanıcı güvenlik okuyucu aynı haklarına sahiptir ve ayrıca güvenlik ilkesini güncelleştirin ve uyarısı ve öneri yok sayın.</span><span class="sxs-lookup"><span data-stu-id="6bdb6-110">**Security Administrator**: A user that belongs to this role has the same rights as the Security Reader and can also update the security policy and dismiss alerts and recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="6bdb6-111">Güvenlik rolleri, güvenlik okuyucu ve Güvenlik Yöneticisi, yalnızca Güvenlik Merkezi'nde erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bdb6-111">The security roles, Security Reader and Security Administrator, have access only in Security Center.</span></span> <span data-ttu-id="6bdb6-112">Güvenlik rolleri, Azure depolama, Web ve mobil veya nesnelerin interneti gibi diğer hizmet alanlara erişimi yoktur.</span><span class="sxs-lookup"><span data-stu-id="6bdb6-112">The security roles do not have access to other service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>
>
>

## <a name="roles-and-allowed-actions"></a><span data-ttu-id="6bdb6-113">Rol ve izin verilen eylemleri</span><span class="sxs-lookup"><span data-stu-id="6bdb6-113">Roles and allowed actions</span></span>

<span data-ttu-id="6bdb6-114">Aşağıdaki tabloda rollerini görüntüler ve Güvenlik Merkezi'nde Eylemler izin.</span><span class="sxs-lookup"><span data-stu-id="6bdb6-114">The following table displays roles and allowed actions in Security Center.</span></span> <span data-ttu-id="6bdb6-115">Bir X eylemi bu rol için izin verildiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="6bdb6-115">An X indicates that the action is allowed for that role.</span></span>

| <span data-ttu-id="6bdb6-116">Rol</span><span class="sxs-lookup"><span data-stu-id="6bdb6-116">Role</span></span> | <span data-ttu-id="6bdb6-117">Güvenlik ilkesini Düzenle</span><span class="sxs-lookup"><span data-stu-id="6bdb6-117">Edit security policy</span></span> | <span data-ttu-id="6bdb6-118">Bir kaynak için güvenlik önerilerini uygulama</span><span class="sxs-lookup"><span data-stu-id="6bdb6-118">Apply security recommendations for a resource</span></span> | <span data-ttu-id="6bdb6-119">Uyarılar ve öneriler kapatın</span><span class="sxs-lookup"><span data-stu-id="6bdb6-119">Dismiss alerts and recommendations</span></span> | <span data-ttu-id="6bdb6-120">Uyarıları görüntüle ve öneriler</span><span class="sxs-lookup"><span data-stu-id="6bdb6-120">View alerts and recommendations</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="6bdb6-121">Abonelik sahibi</span><span class="sxs-lookup"><span data-stu-id="6bdb6-121">Subscription Owner</span></span> | <span data-ttu-id="6bdb6-122">X</span><span class="sxs-lookup"><span data-stu-id="6bdb6-122">X</span></span> | <span data-ttu-id="6bdb6-123">X</span><span class="sxs-lookup"><span data-stu-id="6bdb6-123">X</span></span> | <span data-ttu-id="6bdb6-124">X</span><span class="sxs-lookup"><span data-stu-id="6bdb6-124">X</span></span> | <span data-ttu-id="6bdb6-125">X</span><span class="sxs-lookup"><span data-stu-id="6bdb6-125">X</span></span> |
| <span data-ttu-id="6bdb6-126">Abonelik katkıda bulunan</span><span class="sxs-lookup"><span data-stu-id="6bdb6-126">Subscription Contributor</span></span> | <span data-ttu-id="6bdb6-127">X</span><span class="sxs-lookup"><span data-stu-id="6bdb6-127">X</span></span> | <span data-ttu-id="6bdb6-128">X</span><span class="sxs-lookup"><span data-stu-id="6bdb6-128">X</span></span> | <span data-ttu-id="6bdb6-129">X</span><span class="sxs-lookup"><span data-stu-id="6bdb6-129">X</span></span> | <span data-ttu-id="6bdb6-130">X</span><span class="sxs-lookup"><span data-stu-id="6bdb6-130">X</span></span> |
| <span data-ttu-id="6bdb6-131">Kaynak grubunun sahibi</span><span class="sxs-lookup"><span data-stu-id="6bdb6-131">Resource Group Owner</span></span> | -- | <span data-ttu-id="6bdb6-132">X</span><span class="sxs-lookup"><span data-stu-id="6bdb6-132">X</span></span> | -- | <span data-ttu-id="6bdb6-133">X</span><span class="sxs-lookup"><span data-stu-id="6bdb6-133">X</span></span> |
| <span data-ttu-id="6bdb6-134">Kaynak grubu katkıda bulunan</span><span class="sxs-lookup"><span data-stu-id="6bdb6-134">Resource Group Contributor</span></span> | -- | <span data-ttu-id="6bdb6-135">X</span><span class="sxs-lookup"><span data-stu-id="6bdb6-135">X</span></span> | -- | <span data-ttu-id="6bdb6-136">X</span><span class="sxs-lookup"><span data-stu-id="6bdb6-136">X</span></span> |
| <span data-ttu-id="6bdb6-137">Okuyucu</span><span class="sxs-lookup"><span data-stu-id="6bdb6-137">Reader</span></span> | -- | -- | -- | <span data-ttu-id="6bdb6-138">X</span><span class="sxs-lookup"><span data-stu-id="6bdb6-138">X</span></span> |
| <span data-ttu-id="6bdb6-139">Güvenlik Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="6bdb6-139">Security Administrator</span></span> | <span data-ttu-id="6bdb6-140">X</span><span class="sxs-lookup"><span data-stu-id="6bdb6-140">X</span></span> | -- | <span data-ttu-id="6bdb6-141">X</span><span class="sxs-lookup"><span data-stu-id="6bdb6-141">X</span></span> | <span data-ttu-id="6bdb6-142">X</span><span class="sxs-lookup"><span data-stu-id="6bdb6-142">X</span></span> |
| <span data-ttu-id="6bdb6-143">Güvenlik okuyucusu</span><span class="sxs-lookup"><span data-stu-id="6bdb6-143">Security Reader</span></span> | -- | -- | -- | <span data-ttu-id="6bdb6-144">X</span><span class="sxs-lookup"><span data-stu-id="6bdb6-144">X</span></span> |

> [!NOTE]
> <span data-ttu-id="6bdb6-145">Kullanıcılara, görevlerini tamamlamak için gereken rolleri en alt seviyede esneklik sunacak şekilde atamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="6bdb6-145">We recommend that you assign the least permissive role needed for users to complete their tasks.</span></span> <span data-ttu-id="6bdb6-146">Örneğin, yalnızca bir kaynak güvenlik durumu hakkındaki bilgileri görüntüleyebilir, ancak önerileri uygulamak veya ilkeleri düzenleme gibi bir eylemde bulunmamasını gereken kullanıcılar için okuyucu rolüne atayın.</span><span class="sxs-lookup"><span data-stu-id="6bdb6-146">For example, assign the Reader role to users who only need to view information about the security health of a resource but not take action, such as applying recommendations or editing policies.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="6bdb6-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6bdb6-147">Next steps</span></span>
<span data-ttu-id="6bdb6-148">Bu makalede RBAC Güvenlik Merkezi kullanıcılara izinler atamak için nasıl kullandığı açıklanmıştır ve her rol için izin verilen eylemleri tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="6bdb6-148">This article explained how Security Center uses RBAC to assign permissions to users and identified the allowed actions for each role.</span></span> <span data-ttu-id="6bdb6-149">Aboneliğinizi güvenlik durumunu izlemek için gerekli rol atamalarını ile tanıdık, güvenlik ilkeleri, düzenleme ve önerileri geçerlidir, öğrenme nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="6bdb6-149">Now that you're familiar with the role assignments needed to monitor the security state of your subscription, edit security policies, and apply recommendations, learn how to:</span></span>

- [<span data-ttu-id="6bdb6-150">Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="6bdb6-150">Set security policies in Security Center</span></span>](security-center-policies.md)
- [<span data-ttu-id="6bdb6-151">Güvenlik Merkezi'nde güvenlik önerilerini yönetme</span><span class="sxs-lookup"><span data-stu-id="6bdb6-151">Manage security recommendations in Security Center</span></span>](security-center-recommendations.md)
- [<span data-ttu-id="6bdb6-152">Azure kaynaklarınızın güvenlik durumunu izleme</span><span class="sxs-lookup"><span data-stu-id="6bdb6-152">Monitor the security health of your Azure resources</span></span>](security-center-monitoring.md)
- [<span data-ttu-id="6bdb6-153">Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama</span><span class="sxs-lookup"><span data-stu-id="6bdb6-153">Manage and respond to security alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
- [<span data-ttu-id="6bdb6-154">İş ortağı güvenlik çözümlerini izleme</span><span class="sxs-lookup"><span data-stu-id="6bdb6-154">Monitor partner security solutions</span></span>](security-center-partner-solutions.md)
