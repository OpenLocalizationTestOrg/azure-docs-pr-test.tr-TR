---
title: Kapsam belirleme filtreleri ile aaaProvisioning uygulamalar | Microsoft Docs
description: "Toouse kapsamı tooprevent nesneleri nesneyi iş gereksinimlerinizi karşılamadığı, aslında sağlanacak otomatik kullanıcı sağlamayı destekleyen uygulamaları nasıl filtreler hakkında bilgi edinin."
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
ms.openlocfilehash: f0299390dc3fdb70aa9d271e835069a08827d635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a><span data-ttu-id="64cc4-103">Kapsam belirleme filtreleri ile öznitelik tabanlı uygulama sağlama</span><span class="sxs-lookup"><span data-stu-id="64cc4-103">Attribute-based application provisioning with scoping filters</span></span>
<span data-ttu-id="64cc4-104">Merhaba amacı, bu bölümde, hangi kullanıcıların belirlemek toodefine öznitelik tabanlı kurallar toouse kapsamı nasıl filtreler tooexplain toohello uygulama sağlanan ' dir.</span><span class="sxs-lookup"><span data-stu-id="64cc4-104">hello objective of this section is tooexplain how toouse scoping filters toodefine attribute-based rules that determine which users are provisioned toohello application.</span></span>

## <a name="clauses-and-scope-groups"></a><span data-ttu-id="64cc4-105">Yan tümceleri ve kapsam grupları</span><span class="sxs-lookup"><span data-stu-id="64cc4-105">Clauses and Scope Groups</span></span>
![Kapsamı filtresi][1] 

<span data-ttu-id="64cc4-107">Bir veya daha fazla kapsam filtreleri tanımlanmış **Kapsam grupları**, her bir veya daha fazla tut **yan tümceleri**.</span><span class="sxs-lookup"><span data-stu-id="64cc4-107">Scoping filters are defined by one or more **scope groups**, each of which hold one or more **clauses**.</span></span> <span data-ttu-id="64cc4-108">Belirli kapsam grubu için toosee hello yan tümceleri genişletin, hello ok toohello sol hello grup adının tıklayarak.</span><span class="sxs-lookup"><span data-stu-id="64cc4-108">toosee hello clauses for a particular scope group, expand it by clicking hello arrow toohello left of hello group name.</span></span>

<span data-ttu-id="64cc4-109">A **yan tümcesi** toopass her kullanıcının öznitelikleri değerlendirerek kapsamı filtresi hello aracılığıyla izin verilen kullanıcıları belirler.</span><span class="sxs-lookup"><span data-stu-id="64cc4-109">A **clause** determines which users are allowed toopass through hello scoping filter by evaluating each user’s attributes.</span></span> <span data-ttu-id="64cc4-110">Örneğin, yalnızca New York kullanıcıların hello uygulamasına sağlanan şekilde bir kullanıcının 'state' özniteliği eşit New York, gerektiren bir yan tümce olabilir.</span><span class="sxs-lookup"><span data-stu-id="64cc4-110">For example, you might have one clause that requires that a user’s ‘state’ attribute equal New York, so only New York users are provisioned into hello application.</span></span>

![Ölçüm grubu adı][2] 

<span data-ttu-id="64cc4-112">Her **kapsam grubu** bir zorunlu ile başlayan **yan tümcesi**, yukarıdaki hello ekran görüntüsünde gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="64cc4-112">Each **scope group** starts with one mandatory **clause**, as shown in hello screenshot above.</span></span> <span data-ttu-id="64cc4-113">Yalnızca durumları bu yan tümcesi, kapsam, filtreler tarafından değerlendirilir önce hello kullanıcının ilk toohello uygulama atanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="64cc4-113">This clause simply states that hello user must first be assigned toohello application before it’s evaluated by your scoping filters.</span></span> <span data-ttu-id="64cc4-114">Bu yan tümce silinmiş veya değiştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="64cc4-114">This clause cannot be deleted or modified.</span></span>

<span data-ttu-id="64cc4-115">Merhaba uygun düğmesine basarak yeni yan tümcesi ya da Yeni Kapsam grupları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64cc4-115">You can add new clauses or new scope groups by pressing hello appropriate button.</span></span> <span data-ttu-id="64cc4-116">Her bir kapsam grubu düzenleyerek bir ad verin, **kapsam grup adı** özelliği.</span><span class="sxs-lookup"><span data-stu-id="64cc4-116">You can give each scope group a name by editing its **Scope Group Name** property.</span></span>

## <a name="how-scoping-filters-are-evaluated"></a><span data-ttu-id="64cc4-117">Kapsam belirleme filtreleri nasıl değerlendirilir</span><span class="sxs-lookup"><span data-stu-id="64cc4-117">How Scoping Filters are Evaluated</span></span>
<span data-ttu-id="64cc4-118">Bu kullanıcının erişim toohello uygulama hak varsa sağlama işlemi sırasında biz kapsam, filtreler toodetermine karşı atanan her kullanıcı sınayın.</span><span class="sxs-lookup"><span data-stu-id="64cc4-118">During provisioning, we test every assigned user against your scoping filters toodetermine if that user deserves access toohello application.</span></span> <span data-ttu-id="64cc4-119">Her yan tümcesinin filtrelenmelidir hello kullanıcı tooavoid geçirilmesi gereken bir test olarak düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64cc4-119">You can think of each clause as being a test that must be passed in order for hello user tooavoid getting filtered out.</span></span> 

<span data-ttu-id="64cc4-120">Tanımlanan birden çok kapsam gruplarınız varsa, her kullanıcı en az biri tooaccess Merhaba uygulaması geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="64cc4-120">If you have multiple scope groups defined, each user must pass at least one of them tooaccess hello application.</span></span> <span data-ttu-id="64cc4-121">Her bir kapsam grubunda ancak hello kullanıcı her yan tümcesi toopass bu belirli kapsam grubu geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="64cc4-121">Within each scope group, however, hello user must pass every clause toopass that specific scope group.</span></span> 

<span data-ttu-id="64cc4-122">Diğer bir deyişle, kapsam grubu olarak düşünebilirsiniz veya birlikte and'lenir ve bunların içindeki hello tümceleri olarak düşünebilirsiniz ve birlikte and'lenir.</span><span class="sxs-lookup"><span data-stu-id="64cc4-122">In other words, you can think of scope groups as being OR’d together, and you can think of hello clauses within them as being AND’d together.</span></span> <span data-ttu-id="64cc4-123">Örneğin, aşağıdaki filtre kapsamı hello göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="64cc4-123">For example, consider hello scoping filter below:</span></span>

![Ölçüm grubu adı][3]  

<span data-ttu-id="64cc4-125">Filtre kapsamı toothis göre kullanıcıların hello aşağıdaki getirmelidir ölçütleri, sağlanan toobe:</span><span class="sxs-lookup"><span data-stu-id="64cc4-125">According toothis scoping filter, users must satisfy hello following criteria, toobe provisioned:</span></span>

1. <span data-ttu-id="64cc4-126">Toohello uygulama atanmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="64cc4-126">They must be assigned toohello application.</span></span>
2. <span data-ttu-id="64cc4-127">Merhaba mühendislik departmanı çalışmanız gerekir</span><span class="sxs-lookup"><span data-stu-id="64cc4-127">They must work in hello Engineering department</span></span>
3. <span data-ttu-id="64cc4-128">İş olmalıdır San Francisco veya Kanada.</span><span class="sxs-lookup"><span data-stu-id="64cc4-128">They must be work in either San Francisco or Canada.</span></span>

## <a name="related-articles"></a><span data-ttu-id="64cc4-129">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="64cc4-129">Related Articles</span></span>
* [<span data-ttu-id="64cc4-130">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="64cc4-130">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="64cc4-131">Kullanıcı hazırlama ve sağlamayı kaldırma işlemlerini tooSaaS uygulamaları otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="64cc4-131">Automate User Provisioning and Deprovisioning tooSaaS Applications</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="64cc4-132">Kullanıcı sağlama öznitelik eşlemelerini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="64cc4-132">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="64cc4-133">Özellik eşlemeleri için ifade yazma</span><span class="sxs-lookup"><span data-stu-id="64cc4-133">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="64cc4-134">Hesap sağlama bildirimleri</span><span class="sxs-lookup"><span data-stu-id="64cc4-134">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="64cc4-135">SCIM'yi tooenable otomatik kullanıcıların ve grupların Azure Active Directory tooapplications sağlama kullanma</span><span class="sxs-lookup"><span data-stu-id="64cc4-135">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="64cc4-136">İlgili nasıl öğreticiler listesi tooIntegrate SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="64cc4-136">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
