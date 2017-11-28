---
title: "Kapsam belirleme filtreleri ile uygulamalar sağlama | Microsoft Docs"
description: "Nesneleri nesneyi iş gereksinimlerinizi karşılamadığı, aslında sağlanacak otomatik kullanıcı sağlamayı destekleyen uygulamalarda önlemek için kapsam filtreleri kullanmayı öğrenin."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 109635052e2ded33831b050eb12d50745944091b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a><span data-ttu-id="490ec-103">Kapsam belirleme filtreleri ile öznitelik tabanlı uygulama sağlama</span><span class="sxs-lookup"><span data-stu-id="490ec-103">Attribute-based application provisioning with scoping filters</span></span>
<span data-ttu-id="490ec-104">Bu bölümün amacı, kapsam filtreleri hangi kullanıcıların uygulamayı sağlanan belirlemek öznitelik tabanlı kurallar tanımlamak için nasıl kullanılacağını açıklamaktadır sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="490ec-104">The objective of this section is to explain how to use scoping filters to define attribute-based rules that determine which users are provisioned to the application.</span></span>

## <a name="clauses-and-scope-groups"></a><span data-ttu-id="490ec-105">Yan tümceleri ve kapsam grupları</span><span class="sxs-lookup"><span data-stu-id="490ec-105">Clauses and Scope Groups</span></span>
![Kapsamı filtresi][1] 

<span data-ttu-id="490ec-107">Bir veya daha fazla kapsam filtreleri tanımlanmış **Kapsam grupları**, her bir veya daha fazla tut **yan tümceleri**.</span><span class="sxs-lookup"><span data-stu-id="490ec-107">Scoping filters are defined by one or more **scope groups**, each of which hold one or more **clauses**.</span></span> <span data-ttu-id="490ec-108">Belirli kapsam grubu için yan tümceleri görmek için grup adının solundaki oka tıklayarak genişletin.</span><span class="sxs-lookup"><span data-stu-id="490ec-108">To see the clauses for a particular scope group, expand it by clicking the arrow to the left of the group name.</span></span>

<span data-ttu-id="490ec-109">A **yan tümcesi** her kullanıcının öznitelikleri değerlendirerek kapsam filtresinden geçmesine izin verilen kullanıcıları belirler.</span><span class="sxs-lookup"><span data-stu-id="490ec-109">A **clause** determines which users are allowed to pass through the scoping filter by evaluating each user’s attributes.</span></span> <span data-ttu-id="490ec-110">Örneğin, yalnızca New York kullanıcıların uygulamaya sağlanan şekilde bir kullanıcının 'state' özniteliği, New York eşit gerektiren bir yan tümce olabilir.</span><span class="sxs-lookup"><span data-stu-id="490ec-110">For example, you might have one clause that requires that a user’s ‘state’ attribute equal New York, so only New York users are provisioned into the application.</span></span>

![Ölçüm grubu adı][2] 

<span data-ttu-id="490ec-112">Her **kapsam grubu** bir zorunlu ile başlayan **yan tümcesi**, yukarıdaki ekran görüntüsünde gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="490ec-112">Each **scope group** starts with one mandatory **clause**, as shown in the screenshot above.</span></span> <span data-ttu-id="490ec-113">Yalnızca durumları bu yan tümcesi, kapsam, filtreler tarafından değerlendirilir önce kullanıcının ilk uygulamaya atanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="490ec-113">This clause simply states that the user must first be assigned to the application before it’s evaluated by your scoping filters.</span></span> <span data-ttu-id="490ec-114">Bu yan tümce silinmiş veya değiştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="490ec-114">This clause cannot be deleted or modified.</span></span>

<span data-ttu-id="490ec-115">Uygun düğmesine basarak yeni yan tümcesi ya da Yeni Kapsam grupları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="490ec-115">You can add new clauses or new scope groups by pressing the appropriate button.</span></span> <span data-ttu-id="490ec-116">Her bir kapsam grubu düzenleyerek bir ad verin, **kapsam grup adı** özelliği.</span><span class="sxs-lookup"><span data-stu-id="490ec-116">You can give each scope group a name by editing its **Scope Group Name** property.</span></span>

## <a name="how-scoping-filters-are-evaluated"></a><span data-ttu-id="490ec-117">Kapsam belirleme filtreleri nasıl değerlendirilir</span><span class="sxs-lookup"><span data-stu-id="490ec-117">How Scoping Filters are Evaluated</span></span>
<span data-ttu-id="490ec-118">Sağlama işlemi sırasında Biz bu kullanıcının uygulamaya erişim hak varsa belirlemek için her atanan kullanıcı kapsam filtrelerinizi karşı test edin.</span><span class="sxs-lookup"><span data-stu-id="490ec-118">During provisioning, we test every assigned user against your scoping filters to determine if that user deserves access to the application.</span></span> <span data-ttu-id="490ec-119">Her yan tümcesi kullanıcının filtrelenmelidir önlemek sırayla geçirilmelidir bir test olarak düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="490ec-119">You can think of each clause as being a test that must be passed in order for the user to avoid getting filtered out.</span></span> 

<span data-ttu-id="490ec-120">Tanımlanan birden çok kapsam gruplarınız varsa, her kullanıcının uygulamaya erişim için en az biri geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="490ec-120">If you have multiple scope groups defined, each user must pass at least one of them to access the application.</span></span> <span data-ttu-id="490ec-121">Her bir kapsam grubunda ancak, bu belirli kapsam grubu geçirmek için her yan tümcesi kullanıcı geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="490ec-121">Within each scope group, however, the user must pass every clause to pass that specific scope group.</span></span> 

<span data-ttu-id="490ec-122">Diğer bir deyişle, kapsam grubu olarak düşünebilirsiniz veya birlikte and'lenir ve olarak yan tümceleri içinde bunları düşünebilirsiniz ve birlikte and'lenir.</span><span class="sxs-lookup"><span data-stu-id="490ec-122">In other words, you can think of scope groups as being OR’d together, and you can think of the clauses within them as being AND’d together.</span></span> <span data-ttu-id="490ec-123">Örneğin, aşağıdaki ölçüm filtre göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="490ec-123">For example, consider the scoping filter below:</span></span>

![Ölçüm grubu adı][3]  

<span data-ttu-id="490ec-125">Bu kapsam filtresi göre kullanıcılar sağlanacak aşağıdaki ölçütleri karşılamalıdır:</span><span class="sxs-lookup"><span data-stu-id="490ec-125">According to this scoping filter, users must satisfy the following criteria, to be provisioned:</span></span>

1. <span data-ttu-id="490ec-126">Uygulamaya atanmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="490ec-126">They must be assigned to the application.</span></span>
2. <span data-ttu-id="490ec-127">Mühendislik departmanında çalışmanız gerekir</span><span class="sxs-lookup"><span data-stu-id="490ec-127">They must work in the Engineering department</span></span>
3. <span data-ttu-id="490ec-128">İş olmalıdır San Francisco veya Kanada.</span><span class="sxs-lookup"><span data-stu-id="490ec-128">They must be work in either San Francisco or Canada.</span></span>

## <a name="related-articles"></a><span data-ttu-id="490ec-129">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="490ec-129">Related Articles</span></span>
* [<span data-ttu-id="490ec-130">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="490ec-130">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="490ec-131">Sağlama ve SaaS uygulamaları etkinleştirmektir kullanıcı otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="490ec-131">Automate User Provisioning and Deprovisioning to SaaS Applications</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="490ec-132">Kullanıcı sağlama öznitelik eşlemelerini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="490ec-132">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="490ec-133">Özellik eşlemeleri için ifade yazma</span><span class="sxs-lookup"><span data-stu-id="490ec-133">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="490ec-134">Hesap sağlama bildirimleri</span><span class="sxs-lookup"><span data-stu-id="490ec-134">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="490ec-135">Kullanıcıların ve grupların Azure Active Directory'den uygulamalara otomatik olarak hazırlanmasını etkinleştirmek için SCIM'yi kullanma</span><span class="sxs-lookup"><span data-stu-id="490ec-135">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="490ec-136">SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="490ec-136">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
