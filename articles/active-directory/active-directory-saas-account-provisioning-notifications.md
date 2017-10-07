---
title: "sağlama bildirimleri aaaAccount | Microsoft Docs"
description: "Nasıl toouser hesap sağlama bildirimleri etkinleştirerek dikkat etmeniz gereken sağlama sorunları bildirilir tooensure ilgili bilgi edinin."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a637aac7-f06b-48ef-a66d-639835a8edec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: e33d1dd806fff43fc96f843a9dcddd7375d2e3c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="account-provisioning-notifications"></a><span data-ttu-id="3474b-103">Hesap Sağlama Bildirimleri</span><span class="sxs-lookup"><span data-stu-id="3474b-103">Account Provisioning Notifications</span></span>
<span data-ttu-id="3474b-104">Kullanıcı sağlama ile üçüncü taraf SaaS uygulamalarında kullanıcıları yönetme hello işlemi otomatikleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3474b-104">With user provisioning, you can automate hello process of managing users in third party SaaS applications.</span></span> <br>
<span data-ttu-id="3474b-105">Bu otomatik bir işlem olmakla birlikte, bu işlem ile etkileşim gerekli zaman tootime ' dir.</span><span class="sxs-lookup"><span data-stu-id="3474b-105">While this is an automated process, your interaction with this process is from time tootime required.</span></span> <br>
<span data-ttu-id="3474b-106">Bu yapıldığında, örneğin hello durumda, üçüncü ile tooexchange veri yapılandırmış olduğunuz hello hesabı hello parola taraf SaaS uygulama süresi doldu.</span><span class="sxs-lookup"><span data-stu-id="3474b-106">This is, for example hello case, when hello password of hello account you have configured tooexchange data with a third party SaaS application has expired.</span></span> 

<span data-ttu-id="3474b-107">Hesap sağlama bildirimleri etkinleştirerek sorunları ilgili toouser dikkat etmeniz gereken hazırlama, bildirim aldığından emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3474b-107">By enabling account provisioning notifications, you can ensure that you are notified of issues related toouser provisioning that require your attention.</span></span>

<span data-ttu-id="3474b-108">Etkinleştirmek veya hesap sağlama bildirimleri yapılandırma bir üçüncü taraf SaaS uygulaması için sağlama, kullanıcı bir parçası olarak devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="3474b-108">You activate or deactivate account provisioning notifications as part of your user provisioning configuration for a third party SaaS application.</span></span>

![Kullanıcı hazırlama][1] 

<span data-ttu-id="3474b-110">tooactivate hesap sağlama bildirimleri, select hello hello ilgili onay kutusuna **onay** iletişim sayfası ve hello alıcı türü hello e-posta diğer adı.</span><span class="sxs-lookup"><span data-stu-id="3474b-110">tooactivate account provisioning notifications, select hello related checkbox on hello **Confirmation** dialog page, and then type hello email alias of hello recipient.</span></span>

![Hesap Sağlama Bildirimleri][2]

<span data-ttu-id="3474b-112">Bir dağıtım listesi alıcısı olarak girebilirsiniz. Ancak, önemli toonote hello bildirim e-posta yalnızca hello Azure AD yöneticiler tarafından erişilebilir bağlantılar tooreports içerdiğinden emin olur.</span><span class="sxs-lookup"><span data-stu-id="3474b-112">You can enter a distribution list as recipient; however, it is important toonote that hello notification email contains links tooreports that are only accessible by hello Azure AD administrators.</span></span>

<span data-ttu-id="3474b-113">Hesap sağlama bildirimleri etkin varsa, ilgili toouser sağlama olan kritik sorunlar hakkında postaları alır.</span><span class="sxs-lookup"><span data-stu-id="3474b-113">If you have account provisioning notifications enabled, you will receive emails about critical issues that are related toouser provisioning.</span></span> <span data-ttu-id="3474b-114">Ancak, bir e-posta aşırı tooavoid, yalnızca bir bildirim e-posta günde uygulama hello bildirim e-posta etkinleştirilmiş her SaaS için alırsınız.</span><span class="sxs-lookup"><span data-stu-id="3474b-114">However, tooavoid an email overload, you will only receive one notification email per day for each SaaS application hello notification email is enabled for.</span></span>

## <a name="related-articles"></a><span data-ttu-id="3474b-115">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="3474b-115">Related Articles</span></span>
* [<span data-ttu-id="3474b-116">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="3474b-116">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="3474b-117">Kullanıcı hazırlama/sağlama kaldırmayı tooSaaS uygulamaları otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="3474b-117">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="3474b-118">Kullanıcı sağlama öznitelik eşlemelerini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="3474b-118">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="3474b-119">Özellik eşlemeleri için ifade yazma</span><span class="sxs-lookup"><span data-stu-id="3474b-119">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="3474b-120">Kapsam belirleme filtreleri kullanıcı sağlama</span><span class="sxs-lookup"><span data-stu-id="3474b-120">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="3474b-121">SCIM'yi tooenable otomatik kullanıcıların ve grupların Azure Active Directory tooapplications sağlama kullanma</span><span class="sxs-lookup"><span data-stu-id="3474b-121">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="3474b-122">İlgili nasıl öğreticiler listesi tooIntegrate SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="3474b-122">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-account-provisioning-notifications/ic766307.png
[2]: ./media/active-directory-saas-account-provisioning-notifications/ic766308.png
