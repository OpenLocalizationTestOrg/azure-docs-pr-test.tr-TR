---
title: "Hesap sağlama bildirimleri | Microsoft Docs"
description: "Hesap sağlama bildirimleri etkinleştirerek dikkat etmeniz gereken kullanıcı sağlamak için ilgili sorunların bildirim aldığından emin olmak öğrenin."
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
ms.openlocfilehash: b99037fc28eca1a3ebffefb9e99991e74f52c9a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="account-provisioning-notifications"></a><span data-ttu-id="fb7de-103">Hesap Sağlama Bildirimleri</span><span class="sxs-lookup"><span data-stu-id="fb7de-103">Account Provisioning Notifications</span></span>
<span data-ttu-id="fb7de-104">Kullanıcı sağlama ile üçüncü taraf SaaS uygulamalarında kullanıcıları yönetme sürecini otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb7de-104">With user provisioning, you can automate the process of managing users in third party SaaS applications.</span></span> <br>
<span data-ttu-id="fb7de-105">Bu otomatik bir işlem olmakla birlikte, bu işlem ile etkileşim zaman zaman gereklidir.</span><span class="sxs-lookup"><span data-stu-id="fb7de-105">While this is an automated process, your interaction with this process is from time to time required.</span></span> <br>
<span data-ttu-id="fb7de-106">Bu yapıldığında, örneğin durumu üçüncü ile veri değişimi için yapılandırdığınız hesabı için parola taraf SaaS uygulama süresi doldu.</span><span class="sxs-lookup"><span data-stu-id="fb7de-106">This is, for example the case, when the password of the account you have configured to exchange data with a third party SaaS application has expired.</span></span> 

<span data-ttu-id="fb7de-107">Hesap sağlama bildirimleri etkinleştirerek, dikkat etmeniz gereken kullanıcı sağlamak için ilgili sorunlar bildirim aldığından emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb7de-107">By enabling account provisioning notifications, you can ensure that you are notified of issues related to user provisioning that require your attention.</span></span>

<span data-ttu-id="fb7de-108">Etkinleştirmek veya hesap sağlama bildirimleri yapılandırma bir üçüncü taraf SaaS uygulaması için sağlama, kullanıcı bir parçası olarak devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="fb7de-108">You activate or deactivate account provisioning notifications as part of your user provisioning configuration for a third party SaaS application.</span></span>

![Kullanıcı hazırlama][1] 

<span data-ttu-id="fb7de-110">Hesap sağlama bildirimleri etkinleştirmek için ilgili onay kutusunu seçin **onay** iletişim sayfası ve alıcının e-posta diğer adı sonra yazın.</span><span class="sxs-lookup"><span data-stu-id="fb7de-110">To activate account provisioning notifications, select the related checkbox on the **Confirmation** dialog page, and then type the email alias of the recipient.</span></span>

![Hesap Sağlama Bildirimleri][2]

<span data-ttu-id="fb7de-112">Bir dağıtım listesi alıcısı olarak girebilirsiniz. Ancak, bildirim e-posta yalnızca Azure AD yöneticileri tarafından erişilebilir olan raporlar bağlar olduğunu dikkate almak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="fb7de-112">You can enter a distribution list as recipient; however, it is important to note that the notification email contains links to reports that are only accessible by the Azure AD administrators.</span></span>

<span data-ttu-id="fb7de-113">Hesap sağlama bildirimleri etkin varsa, kullanıcı sağlama için ilgili önemli sorunları hakkında postaları alır.</span><span class="sxs-lookup"><span data-stu-id="fb7de-113">If you have account provisioning notifications enabled, you will receive emails about critical issues that are related to user provisioning.</span></span> <span data-ttu-id="fb7de-114">Ancak, bir e-posta aşırı önlemek için yalnızca bir bildirim e-posta her SaaS uygulaması için bildirim e-posta etkinleştirilmiş günde alırsınız.</span><span class="sxs-lookup"><span data-stu-id="fb7de-114">However, to avoid an email overload, you will only receive one notification email per day for each SaaS application the notification email is enabled for.</span></span>

## <a name="related-articles"></a><span data-ttu-id="fb7de-115">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="fb7de-115">Related Articles</span></span>
* [<span data-ttu-id="fb7de-116">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="fb7de-116">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="fb7de-117">Kullanıcı sağlama/sağlamayı SaaS uygulamaları için otomatik hale getirme</span><span class="sxs-lookup"><span data-stu-id="fb7de-117">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="fb7de-118">Kullanıcı sağlama öznitelik eşlemelerini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="fb7de-118">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="fb7de-119">Özellik eşlemeleri için ifade yazma</span><span class="sxs-lookup"><span data-stu-id="fb7de-119">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="fb7de-120">Kapsam belirleme filtreleri kullanıcı sağlama</span><span class="sxs-lookup"><span data-stu-id="fb7de-120">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="fb7de-121">Kullanıcıların ve grupların Azure Active Directory'den uygulamalara otomatik olarak hazırlanmasını etkinleştirmek için SCIM'yi kullanma</span><span class="sxs-lookup"><span data-stu-id="fb7de-121">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="fb7de-122">SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="fb7de-122">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-account-provisioning-notifications/ic766307.png
[2]: ./media/active-directory-saas-account-provisioning-notifications/ic766308.png
