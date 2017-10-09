---
title: "belirli bir kullanıcı mümkün tooaccess uygulamanın ne zaman olacağını çıkışı aaaFind | Microsoft Docs"
description: "Nasıl oldukça önemli bir kullanıcı mümkün tooaccess uygulamanın ne zaman olması çıkışı toofind kullanıcı Azure AD ile sağlamak için yapılandırdığınız"
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
ms.openlocfilehash: bb9520499dcc8bbbe6fae05c5238c8852815ea0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-tooaccess-an-application"></a><span data-ttu-id="bdc66-103">Belirli bir kullanıcı mümkün tooaccess bir uygulamayı kullanırken öğrenin</span><span class="sxs-lookup"><span data-stu-id="bdc66-103">Find out when a specific user will be able tooaccess an application</span></span>
<span data-ttu-id="bdc66-104">Bir uygulama ile otomatik kullanıcı sağlamayı kullanırken, Azure AD uygulama sağlama ve güncelleştirme kullanıcı hesapları gibi şeyleri temel alınarak otomatik olarak [kullanıcı ve grup atama](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) genellikle her 10 dakikada bir düzenli olarak zamanlanan saat aralığında.</span><span class="sxs-lookup"><span data-stu-id="bdc66-104">When using automatic user provisioning with an application, Azure AD automatically provision and update user accounts in an app based on things like [user and group assignment](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) at a regularly scheduled time interval, typically every 10 minutes.</span></span>

## <a name="how-long-does-it-take"></a><span data-ttu-id="bdc66-105">Ne kadar sürer?</span><span class="sxs-lookup"><span data-stu-id="bdc66-105">How long does it take?</span></span>

<span data-ttu-id="bdc66-106">Merhaba süresini sağlanan verilen kullanıcı toobe için çoğunlukla desteklemediğini ilk bir "tam" eşitleme zaten oluştu üzerinde bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="bdc66-106">hello time it takes for a given user toobe provisioned depends mainly on whether or not an initial “full” sync has already occurred.</span></span>

<span data-ttu-id="bdc66-107">Merhaba ilk eşitleme Azure AD arasında ve bir uygulamayı herhangi bir yere hello boyutunu hello Azure AD dizini ve hello sayısı, kullanıcı sağlama kapsamında bağlı olarak 20 dakika tooseveral saat sürebilir.</span><span class="sxs-lookup"><span data-stu-id="bdc66-107">hello first sync between Azure AD and an app can take anywhere from 20 minutes tooseveral hours, depending on hello size of hello Azure AD directory and hello number of users in scope for provisioning.</span></span> 

<span data-ttu-id="bdc66-108">Hizmet sağlama hello sonraki eşitlemeler performansını iyileştirme hello ilk eşitleme sonrasında her iki sistemle hello durumunu temsil filigranlar depolar hello ilk eşitleme sonrasında sonraki eşitlemeler (örn. 10 dakika içinde), daha hızlı olması.</span><span class="sxs-lookup"><span data-stu-id="bdc66-108">Subsequent syncs after hello initial sync be faster (e.g. within 10 minutes), as hello provisioning service stores watermarks that represent hello state of both systems after hello initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-toocheck-hello-status-of-a-user"></a><span data-ttu-id="bdc66-109">Nasıl toocheck hello kullanıcı durumu</span><span class="sxs-lookup"><span data-stu-id="bdc66-109">How toocheck hello status of a user</span></span>

<span data-ttu-id="bdc66-110">Seçili bir kullanıcı için toosee hello sağlama durumu hello Azure AD'de denetim günlüklerini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="bdc66-110">toosee hello provisioning status for a selected user, consult hello Audit logs in Azure AD.</span></span>

<span data-ttu-id="bdc66-111">Denetim günlüklerini sağlama hello hello Azure portalında, hello erişilebilir **Azure Active Directory &gt; Kurumsal uygulamaları &gt; \[uygulama adı\] &gt; denetim günlükleri**sekmesi. Filtre hello hello üzerinde oturum **hesap sağlama** kategori tooonly olayları bu uygulama için sağlama hello bakın.</span><span class="sxs-lookup"><span data-stu-id="bdc66-111">hello provisioning audit logs can be accessed in hello Azure portal, in hello **Azure Active Directory &gt; Enterprise Apps &gt; \[Application Name\] &gt; Audit Logs** tab. Filter hello logs on hello **Account Provisioning** category tooonly see hello provisioning events for that app.</span></span> <span data-ttu-id="bdc66-112">"Hello öznitelik eşlemelerini kendileri için yapılandırılan hello eşleşen ID" temel alarak kullanıcılara arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdc66-112">You can search for users based on hello “matching ID” that was configured for them in hello attribute mappings.</span></span> 

<span data-ttu-id="bdc66-113">Örneğin hello "kullanıcı asıl adı" veya "Merhaba Azure AD tarafında özniteliği eşleşen hello olarak e-posta adresi" yapılandırılmış ve değil sağlama hello kullanıcı değerine sahip "audrey@contoso.com", için arama hello denetim günlüklerini"audrey@contoso.com" ve gözden geçirin girişleri döndürdü.</span><span class="sxs-lookup"><span data-stu-id="bdc66-113">For example, if you configured hello “user principal name” or “email address” as hello matching attribute on hello Azure AD side, and hello user not being provisioning has a value of “audrey@contoso.com”, then search hello audit logs for “audrey@contoso.com” and review then entries returned.</span></span>

<span data-ttu-id="bdc66-114">Denetim sağlama hello tüm hello hizmeti sağlama hello tarafından gerçekleştirilen işlemler kayıt günlüklerini de dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="bdc66-114">hello provisioning audit logs record all hello operations performed by hello provisioning service, including:</span></span>

* <span data-ttu-id="bdc66-115">Azure AD sağlama kapsamında atanan kullanıcılar için sorgulama</span><span class="sxs-lookup"><span data-stu-id="bdc66-115">Querying Azure AD for assigned users that are in scope for provisioning</span></span>
* <span data-ttu-id="bdc66-116">Merhaba hedef uygulama kullanıcılarla hello varlığı sorgulama</span><span class="sxs-lookup"><span data-stu-id="bdc66-116">Querying hello target app for hello existence of those users</span></span>
* <span data-ttu-id="bdc66-117">Merhaba sistem arasında Hello kullanıcı nesneleri karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="bdc66-117">Comparing hello user objects between hello system</span></span>
* <span data-ttu-id="bdc66-118">Ekleme, güncelleştirme veya hello karşılaştırma üzerine dayalı hello hedef sistemdeki hello kullanıcı hesabı devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="bdc66-118">Adding, updating, or disabling hello user account in hello target system based on hello comparison</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdc66-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bdc66-119">Next steps</span></span>
<span data-ttu-id="bdc66-120">[Kullanıcı hazırlama ve sağlamayı kaldırma işlemlerini tooSaaS Azure Active Directory ile uygulamaları otomatikleştirmek](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span><span class="sxs-lookup"><span data-stu-id="bdc66-120">[Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span></span>
