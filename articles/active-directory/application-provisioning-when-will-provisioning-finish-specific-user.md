---
title: "Ne zaman belirli bir kullanıcı bir uygulamaya erişim kuramaz çıkışı Bul | Microsoft Docs"
description: "Kritik düzeyde önemli bir kullanıcı, kullanıcı Azure AD ile sağlamak için yapılandırdığınız uygulama erişebilmeleri zaman öğrenmek nasıl"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: fcefb31904cfb77022db0358e9feee6a0479db81
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-to-access-an-application"></a><span data-ttu-id="894f1-103">Belirli bir kullanıcı bir uygulamaya erişim mümkün olduğunda öğrenin</span><span class="sxs-lookup"><span data-stu-id="894f1-103">Find out when a specific user will be able to access an application</span></span>
<span data-ttu-id="894f1-104">Bir uygulama ile otomatik kullanıcı sağlamayı kullanırken, Azure AD uygulama sağlama ve güncelleştirme kullanıcı hesapları gibi şeyleri temel alınarak otomatik olarak [kullanıcı ve grup atama](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) genellikle her 10 dakikada bir düzenli olarak zamanlanan saat aralığında.</span><span class="sxs-lookup"><span data-stu-id="894f1-104">When using automatic user provisioning with an application, Azure AD automatically provision and update user accounts in an app based on things like [user and group assignment](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) at a regularly scheduled time interval, typically every 10 minutes.</span></span>

## <a name="how-long-does-it-take"></a><span data-ttu-id="894f1-105">Ne kadar sürer?</span><span class="sxs-lookup"><span data-stu-id="894f1-105">How long does it take?</span></span>

<span data-ttu-id="894f1-106">Sağlanacak belirli bir kullanıcı için geçen süre, çoğunlukla desteklemediğini ilk bir "tam" eşitleme zaten oluştu üzerinde bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="894f1-106">The time it takes for a given user to be provisioned depends mainly on whether or not an initial “full” sync has already occurred.</span></span>

<span data-ttu-id="894f1-107">İlk eşitleme Azure AD arasında ve bir uygulama herhangi bir yere Azure AD dizini ve sayısı, kullanıcı sağlama kapsamında boyutuna bağlı olarak birkaç saat 20 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="894f1-107">The first sync between Azure AD and an app can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span></span> 

<span data-ttu-id="894f1-108">Sonraki eşitlemeler performansını iyileştirme ilk eşitleme sonrasında her iki sistem durumunu temsil filigranlar sağlama hizmeti depolar ilk eşitleme sonrasında sonraki eşitlemeler (örn. 10 dakika içinde), daha hızlı olması.</span><span class="sxs-lookup"><span data-stu-id="894f1-108">Subsequent syncs after the initial sync be faster (e.g. within 10 minutes), as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-to-check-the-status-of-a-user"></a><span data-ttu-id="894f1-109">Kullanıcı durumunu denetleme</span><span class="sxs-lookup"><span data-stu-id="894f1-109">How to check the status of a user</span></span>

<span data-ttu-id="894f1-110">Seçilen kullanıcı için sağlama durumunu görmek için Azure AD'de denetim günlüklerine bakın.</span><span class="sxs-lookup"><span data-stu-id="894f1-110">To see the provisioning status for a selected user, consult the Audit logs in Azure AD.</span></span>

<span data-ttu-id="894f1-111">Sağlama denetim günlüklerini Azure portalında erişilebilen **Azure Active Directory &gt; Kurumsal uygulamaları &gt; \[uygulama adı\] &gt; denetim günlüklerini** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="894f1-111">The provisioning audit logs can be accessed in the Azure portal, in the **Azure Active Directory &gt; Enterprise Apps &gt; \[Application Name\] &gt; Audit Logs** tab.</span></span> <span data-ttu-id="894f1-112">Günlükleri filtre **hesap sağlama** yalnızca bu uygulama için sağlama olayları görmek için kategori.</span><span class="sxs-lookup"><span data-stu-id="894f1-112">Filter the logs on the **Account Provisioning** category to only see the provisioning events for that app.</span></span> <span data-ttu-id="894f1-113">"İçinde öznitelik eşlemelerini kendileri için yapılandırılan eşleşen ID" temel alarak kullanıcılara arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="894f1-113">You can search for users based on the “matching ID” that was configured for them in the attribute mappings.</span></span> 

<span data-ttu-id="894f1-114">Örneğin "kullanıcı asıl adı" veya "Azure AD tarafında eşleşen öznitelik olarak e-posta adresi" yapılandırılmış ve değil sağlama kullanıcı değerine sahip "audrey@contoso.com", denetim günlüklerini arama "audrey@contoso.com" ve gözden geçirin, ardından girdi döndü.</span><span class="sxs-lookup"><span data-stu-id="894f1-114">For example, if you configured the “user principal name” or “email address” as the matching attribute on the Azure AD side, and the user not being provisioning has a value of “audrey@contoso.com”, then search the audit logs for “audrey@contoso.com” and review then entries returned.</span></span>

<span data-ttu-id="894f1-115">Sağlama denetim günlüklerini sağlama hizmeti tarafından gerçekleştirilen tüm işlemlerin kayıt dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="894f1-115">The provisioning audit logs record all the operations performed by the provisioning service, including:</span></span>

* <span data-ttu-id="894f1-116">Azure AD sağlama kapsamında atanan kullanıcılar için sorgulama</span><span class="sxs-lookup"><span data-stu-id="894f1-116">Querying Azure AD for assigned users that are in scope for provisioning</span></span>
* <span data-ttu-id="894f1-117">Hedef uygulama kullanıcılarla varlığı için sorgulama</span><span class="sxs-lookup"><span data-stu-id="894f1-117">Querying the target app for the existence of those users</span></span>
* <span data-ttu-id="894f1-118">Sistem arasında kullanıcı nesneleri karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="894f1-118">Comparing the user objects between the system</span></span>
* <span data-ttu-id="894f1-119">Ekleme, güncelleştirme ya da karşılaştırma üzerine dayalı hedef sistem kullanıcı hesabı devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="894f1-119">Adding, updating, or disabling the user account in the target system based on the comparison</span></span>

## <a name="next-steps"></a><span data-ttu-id="894f1-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="894f1-120">Next steps</span></span>
<span data-ttu-id="894f1-121">[Kullanıcı sağlama ve Azure Active Directory ile SaaS uygulamalarına sağlamayı otomatikleştirmek](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span><span class="sxs-lookup"><span data-stu-id="894f1-121">[Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span></span>
