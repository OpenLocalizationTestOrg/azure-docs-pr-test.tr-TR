---
title: "Azure AD öznitelik eşlemelerini aaaCustomizing | Microsoft Docs"
description: "Hangi öznitelik eşlemelerini Azure Active Directory'de SaaS uygulamaları için nasıl bunları tooaddress işletmenizin değiştirebilirsiniz olduğunu öğrenin gerekiyor."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14db5303f06fc8df3b07a0a8b75713312e71bbfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a><span data-ttu-id="c7eb0-103">Kullanıcı Azure Active Directory'de SaaS uygulamaları için öznitelik eşlemelerini hazırlama özelleştirme</span><span class="sxs-lookup"><span data-stu-id="c7eb0-103">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>
<span data-ttu-id="c7eb0-104">Microsoft Azure AD Kullanıcı hazırlama Salesforce, Google Apps ve diğerleri gibi toothird taraf SaaS uygulamaları için destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-104">Microsoft Azure AD provides support for user provisioning toothird-party SaaS applications such as Salesforce, Google Apps and others.</span></span> <span data-ttu-id="c7eb0-105">Etkin bir üçüncü taraf SaaS uygulaması için sağlama kullanıcınız varsa, öznitelik değerleri "özellik eşlemesi." adlı bir yapılandırma biçiminde hello Azure Yönetim Portalı denetler</span><span class="sxs-lookup"><span data-stu-id="c7eb0-105">If you have user provisioning for a third-party SaaS application enabled, hello Azure Management Portal controls its attribute values in form of a configuration called “attribute mapping.”</span></span>

<span data-ttu-id="c7eb0-106">Önceden yapılandırılmış öznitelik eşlemelerini Azure AD kullanıcı ve her SaaS uygulamanın kullanıcı nesneleri arasında birtakım yoktur.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-106">There is a preconfigured set of attribute mappings between Azure AD user objects and each SaaS app’s user objects.</span></span> <span data-ttu-id="c7eb0-107">Bazı uygulamalar, diğer grupların veya kişilerin gibi nesne türlerini yönetin.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-107">Some apps manage other types of objects, such as Groups or Contacts.</span></span> <br> 
 <span data-ttu-id="c7eb0-108">Merhaba varsayılan öznitelik eşlemelerini tooyour iş gereksinimlerinize göre özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-108">You can customize hello default attribute mappings according tooyour business needs.</span></span> <span data-ttu-id="c7eb0-109">Bu anlamına gelir, değiştirin veya varolan öznitelik eşlemelerini silebilir veya yeni öznitelik eşlemelerini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-109">This means, you can change or delete existing attribute mappings or create new attribute mappings.</span></span>

<span data-ttu-id="c7eb0-110">Hello Azure AD Portalı'nda tıklatarak bu özellik erişebilirsiniz bir **eşlemeleri** yapılandırmada **sağlama** hello içinde **Yönet** bölümünü bir  **Kuruluş uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-110">In hello Azure AD portal, you can access this feature by clicking a **Mappings** configuration under **Provisioning** in hello **Manage** section of an **Enterprise application**.</span></span>


![Salesforce][5] 

<span data-ttu-id="c7eb0-112">Tıklatarak bir **eşlemeleri** yapılandırma, ilgili hello açılır **eşleme özniteliği** dikey.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-112">Clicking a **Mappings** configuration, opens hello related **Attribute Mapping** blade.</span></span>  
<span data-ttu-id="c7eb0-113">Bir SaaS uygulaması toofunction tarafından doğru şekilde gerekli öznitelik eşlemelerini vardır.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-113">There are attribute mappings that are required by a SaaS application toofunction correctly.</span></span> <span data-ttu-id="c7eb0-114">Gerekli öznitelikler için hello **silmek** özelliği kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-114">For required attributes, hello **Delete** feature is unavailable.</span></span>


![Salesforce][6]  

<span data-ttu-id="c7eb0-116">Merhaba yukarıdaki örnekte, bu hello görebilirsiniz **kullanıcıadı** Salesforce içinde yönetilen bir nesnenin öznitelik hello ile doldurulur **userPrincipalName** hello değerini bağlı Azure Active Directory nesnesi.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-116">In hello example above, you can see that hello **Username** attribute of a managed object in Salesforce is populated with hello **userPrincipalName** value of hello linked Azure Active Directory Object.</span></span>

<span data-ttu-id="c7eb0-117">Varolan özelleştirebilirsiniz **öznitelik eşlemelerini** eşleme tıklatarak.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-117">You can customize existing **Attribute Mappings** by clicking a mapping.</span></span> <span data-ttu-id="c7eb0-118">Merhaba açılır **öznitelik Düzenle** dikey.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-118">This opens hello **Edit Attribute** blade.</span></span>

![Salesforce][7]  


  

## <a name="understanding-attribute-mapping-types"></a><span data-ttu-id="c7eb0-120">Öznitelik eşleme türlerini anlama</span><span class="sxs-lookup"><span data-stu-id="c7eb0-120">Understanding attribute mapping types</span></span>
<span data-ttu-id="c7eb0-121">Öznitelik eşlemelerini ile öznitelikleri bir üçüncü taraf SaaS uygulamasına nasıl doldurulur denetler.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-121">With attribute mappings, you control how attributes are populated in a third-party SaaS application.</span></span> <span data-ttu-id="c7eb0-122">Desteklenen dört farklı eşleme türleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c7eb0-122">There are four different mapping types supported:</span></span>

* <span data-ttu-id="c7eb0-123">**Doğrudan** – hello target özniteliği, Azure AD'de hello bağlantılı nesne özniteliği hello değeri ile doldurulur.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-123">**Direct** – hello target attribute is populated with hello value of an attribute of hello linked object in Azure AD.</span></span>
* <span data-ttu-id="c7eb0-124">**Sabit** – hello target özniteliği, belirttiğiniz için belirli bir dizeyi doldurulur.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-124">**Constant** – hello target attribute is populated with a specific string you have specified.</span></span>
* <span data-ttu-id="c7eb0-125">**İfade** -hello target özniteliği hello sonucuna göre bir betik benzeri ifadesi doldurulur.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-125">**Expression** - hello target attribute is populated based on hello result of a script-like expression.</span></span> 
  <span data-ttu-id="c7eb0-126">Daha fazla bilgi için bkz: [Azure Active Directory'de özellik eşlemeleri için ifade yazma](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="c7eb0-126">For more information, see [Writing Expressions for Attribute Mappings in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>
* <span data-ttu-id="c7eb0-127">**Hiçbiri** -hello target özniteliği değişmeden değiştirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-127">**None** - hello target attribute is left unmodified.</span></span> <span data-ttu-id="c7eb0-128">Ancak, Hello Hedef öznitelik sürekli boşsa, belirttiğiniz hello varsayılan değeri ile doldurulur.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-128">However, if hello target attribute is ever empty, it is populated with hello Default value that you specify.</span></span>

<span data-ttu-id="c7eb0-129">Toplama toothese dört temel özniteliği eşleme türlerinde, özel öznitelik eşlemelerini isteğe bağlı bir hello kavramı Destek **varsayılan** değer atama.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-129">In addition toothese four basic attribute mapping types, custom attribute mappings support hello concept of an optional **default** value assignment.</span></span> <span data-ttu-id="c7eb0-130">Merhaba varsayılan değer atama hello hedef nesne ya da Azure AD'de hiçbiri bir değer varsa bir target özniteliği değeri ile doldurulur sağlar.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-130">hello default value assignment ensures that a target attribute is populated with a value if there is neither a value in Azure AD nor on hello target object.</span></span> <span data-ttu-id="c7eb0-131">Merhaba en yaygın tooleave bu boş bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-131">hello most common configuration is tooleave this blank.</span></span>


## <a name="understanding-attribute-mapping-properties"></a><span data-ttu-id="c7eb0-132">Öznitelik Eşleme Özellikleri Anlama</span><span class="sxs-lookup"><span data-stu-id="c7eb0-132">Understanding attribute mapping properties</span></span>

<span data-ttu-id="c7eb0-133">Merhaba önceki bölümde sunulan toohello öznitelik eşleme türü özelliği zaten silinmiş.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-133">In hello previous section, you have already been introduced toohello attribute mapping type property.</span></span>
<span data-ttu-id="c7eb0-134">Toplama toothis özelliğinde öznitelik eşlemelerini de öznitelikleri aşağıdaki hello destekler:</span><span class="sxs-lookup"><span data-stu-id="c7eb0-134">In addition toothis property, attribute mappings do also support hello following attributes:</span></span>

- <span data-ttu-id="c7eb0-135">**Kaynak özniteliği** -hello kullanıcı özniteliği hello kaynak sistemden (örn: Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="c7eb0-135">**Source attribute** - hello user attribute from hello source system (e.g.: Azure Active Directory).</span></span>
- <span data-ttu-id="c7eb0-136">**Hedef öznitelik** – hello kullanıcı özniteliği hello hedef sisteminde (örn: ServiceNow).</span><span class="sxs-lookup"><span data-stu-id="c7eb0-136">**Target attribute** – hello user attribute in hello target system (e.g.: ServiceNow).</span></span>
- <span data-ttu-id="c7eb0-137">**Eşleşen nesneleri bu öznitelik kullanarak** – Bu eşleme kullanılmalıdır olup olmadığına bakılmaksızın toouniquely kullanıcılar hello kaynak ve hedef sistemler arasında tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-137">**Match objects using this attribute** – Whether or not this mapping should be used toouniquely identify users between hello source and target systems.</span></span> <span data-ttu-id="c7eb0-138">Bu, genellikle hello userPrincipalName üzerinde ayarlanır veya posta özniteliğinin genellikle Azure AD'de bir hedef uygulama tooa kullanıcı adı alanı eşlenir.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-138">This is typically set on hello userPrincipalName or mail attribute in Azure AD, which is typically mapped tooa username field in a target application.</span></span>
- <span data-ttu-id="c7eb0-139">**Öncelik eşleşen** – birden çok öznitelikleri eşleşen ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-139">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="c7eb0-140">Olduğunda birden çok, bu alana göre tanımlanan hello sırayla değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-140">When there are multiple, they are evaluated in hello order defined by this field.</span></span> <span data-ttu-id="c7eb0-141">Bir eşleşme olarak başka eşleştirme öznitelikleri değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-141">As soon as a match is found, no further matching attributes are evaluated.</span></span>
- <span data-ttu-id="c7eb0-142">**Bu eşleme Uygula**</span><span class="sxs-lookup"><span data-stu-id="c7eb0-142">**Apply this mapping**</span></span>
    - <span data-ttu-id="c7eb0-143">**Her zaman** – hem kullanıcı oluşturulması bu eşleme uygulamak ve güncelleştirme eylemleri</span><span class="sxs-lookup"><span data-stu-id="c7eb0-143">**Always** – Apply this mapping on both user creation and update actions</span></span>
    - <span data-ttu-id="c7eb0-144">**Yalnızca oluşturma sırasında** -bu eşlemenin yalnızca kullanıcı oluşturma eylemlerini uygulamak</span><span class="sxs-lookup"><span data-stu-id="c7eb0-144">**Only during creation** - Apply this mapping only on user creation actions</span></span>


## <a name="what-you-should-know"></a><span data-ttu-id="c7eb0-145">Bilmeniz gerekenler</span><span class="sxs-lookup"><span data-stu-id="c7eb0-145">What you should know</span></span>

<span data-ttu-id="c7eb0-146">Microsoft Azure AD eşitleme işlemini verimli bir uygulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-146">Microsoft Azure AD provides an efficient implementation of a synchronization process.</span></span> <span data-ttu-id="c7eb0-147">Başlatılmış bir ortamda, bir eşitleme döngüsü sırasında yalnızca güncelleştirmeleri gerektiren nesneler işlenir.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-147">In an initialized environment, only objects requiring updates are processed during a synchronization cycle.</span></span> <span data-ttu-id="c7eb0-148">Öznitelik eşlemelerini güncelleştirme bir eşitleme döngüsü hello performans üzerinde bir etkisi vardır.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-148">Updating attribute mappings has an impact on hello performance of a synchronization cycle.</span></span> <span data-ttu-id="c7eb0-149">Bir güncelleştirme toohello özniteliği eşleme yapılandırmasını yeniden değerlendirimiş tüm yönetilen nesneleri toobe gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-149">An update toohello attribute mapping configuration requires all managed objects toobe reevaluated.</span></span> <span data-ttu-id="c7eb0-150">Bu bir önerilen en iyi yöntem tookeep hello ardışık değişiklikleri tooyour öznitelik eşlemelerini en az sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="c7eb0-150">It is a recommended best practice tookeep hello number of consecutive changes tooyour attribute mappings at a minimum.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7eb0-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c7eb0-151">Next steps</span></span>

* [<span data-ttu-id="c7eb0-152">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="c7eb0-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="c7eb0-153">Kullanıcı hazırlama/sağlama kaldırmayı tooSaaS uygulamaları otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="c7eb0-153">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="c7eb0-154">Özellik eşlemeleri için ifade yazma</span><span class="sxs-lookup"><span data-stu-id="c7eb0-154">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="c7eb0-155">Kapsam belirleme filtreleri kullanıcı sağlama</span><span class="sxs-lookup"><span data-stu-id="c7eb0-155">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="c7eb0-156">SCIM'yi tooenable otomatik kullanıcıların ve grupların Azure Active Directory tooapplications sağlama kullanma</span><span class="sxs-lookup"><span data-stu-id="c7eb0-156">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="c7eb0-157">Hesap sağlama bildirimleri</span><span class="sxs-lookup"><span data-stu-id="c7eb0-157">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="c7eb0-158">İlgili nasıl öğreticiler listesi tooIntegrate SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="c7eb0-158">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

