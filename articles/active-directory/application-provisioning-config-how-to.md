---
title: "Azure AD tooan galeri uygulama sağlama aaaHow tooconfigure kullanıcı | Microsoft Docs"
description: "Nasıl hızlı sağlama ve zaten hello Azure AD uygulama galerisinde listelenen tooapplications etkinleştirmektir zengin bir kullanıcı hesabı yapılandırabilirsiniz"
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
ms.openlocfilehash: 2c28e59a3ac8f221ed93b2f6b0b1221f7604af23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-user-provisioning-tooan-azure-ad-gallery-application"></a><span data-ttu-id="04a7a-103">Nasıl tooconfigure kullanıcı tooan Azure AD galeri uygulama sağlama</span><span class="sxs-lookup"><span data-stu-id="04a7a-103">How tooconfigure user provisioning tooan Azure AD Gallery application</span></span>

<span data-ttu-id="04a7a-104">*Kullanıcı hesabı sağlama* oluşturma, güncelleştirme ve/veya bir uygulamanın yerel kullanıcı profili deposundaki kullanıcı hesabı kayıtlarını devre dışı bırakma, hello işlemidir.</span><span class="sxs-lookup"><span data-stu-id="04a7a-104">*User account provisioning* is hello act of creating, updating, and/or disabling user account records in an application’s local user profile store.</span></span> <span data-ttu-id="04a7a-105">Çoğu Bulut ve SaaS uygulamaları hello kullanıcıların rol ve izinler kendi yerel kullanıcı profili deposunda saklar ve bu tür bir kullanıcı kaydı yerel depolarındaki varlığını olduğundan *gerekli* tek oturum açma ve erişim toowork için.</span><span class="sxs-lookup"><span data-stu-id="04a7a-105">Most cloud and SaaS applications store hello users role and permissions in their own local user profile store, and presence of such a user record in their local store is *required* for single sign-on and access toowork.</span></span>

<span data-ttu-id="04a7a-106">Hello Azure portal, hello **sağlama** hangi sağlama modları bu uygulama için desteklenen bir kuruluş uygulama görüntüler için hello sol gezinti bölmesinde sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="04a7a-106">In hello Azure portal, hello **Provisioning** tab in hello left navigation pane for an Enterprise App displays what provisioning modes are supported for that app.</span></span> <span data-ttu-id="04a7a-107">Bu iki değerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="04a7a-107">This can be one of two values:</span></span>

## <a name="configuring-an-application-for-manual-provisioning"></a><span data-ttu-id="04a7a-108">El ile sağlama için uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="04a7a-108">Configuring an application for Manual Provisioning</span></span>

<span data-ttu-id="04a7a-109">*El ile* sağlama anlamına gelir kullanıcı hesaplarını bu uygulama tarafından sağlanan hello yöntemleri kullanarak el ile oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="04a7a-109">*Manual* provisioning means that user accounts must be created manually using hello methods provided by that app.</span></span> <span data-ttu-id="04a7a-110">Bu uygulama için bir yönetim portalı oturum açma ve bir web tabanlı kullanıcı arabirimini kullanarak kullanıcı ekleme anlamına gelebilir.</span><span class="sxs-lookup"><span data-stu-id="04a7a-110">This could mean logging into an administrative portal for that app and adding users using a web-based user interface.</span></span> <span data-ttu-id="04a7a-111">Veya uygulama tarafından sağlanan bir mekanizma kullanarak, kullanıcı hesabı ayrıntı elektronik karşıya.</span><span class="sxs-lookup"><span data-stu-id="04a7a-111">Or it could be uploading a spreadsheet with user account detail, using a mechanism provided by that application.</span></span> <span data-ttu-id="04a7a-112">Merhaba uygulaması veya kişi hello uygulama geliştiricisi toodetermine wat mekanizmaları kullanılabilir olması koşuluyla hello belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="04a7a-112">Consult hello documentation provided by hello app, or contact hello app developer toodetermine wat mechanisms are available.</span></span>

<span data-ttu-id="04a7a-113">El ile hello yalnızca modu gösterilir belirli bir uygulama için bağlayıcı sağlama hiçbir otomatik Azure AD için başlangıç uygulaması henüz oluşturulduğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="04a7a-113">If Manual is hello only mode shown for a given application, it means that no automatic Azure AD provisioning connector has been created for hello app yet.</span></span> <span data-ttu-id="04a7a-114">Veya hello uygulama değil destek hello önkoşul kullanıcı yönetimi API hangi toobuild bağlı bir otomatik sağlama Bağlayıcısı mu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="04a7a-114">Or it means hello app does not support hello pre-requisite user management API upon which toobuild an automated provisioning connector.</span></span>

<span data-ttu-id="04a7a-115">Toorequest desteği için belirli bir uygulamanın otomatik sağlamayı istiyorsanız, bir isteğiyle doldurabilir <http://aka.ms/aadapprequest>.</span><span class="sxs-lookup"><span data-stu-id="04a7a-115">If you would like toorequest support for automatic provisioning for a given app, you can fill out a request at <http://aka.ms/aadapprequest>.</span></span>

## <a name="configuring-an-application-for-automatic-provisioning"></a><span data-ttu-id="04a7a-116">Otomatik sağlama için uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="04a7a-116">Configuring an application for Automatic Provisioning</span></span>

<span data-ttu-id="04a7a-117">*Otomatik* bağlayıcı sağlama Azure AD bu uygulama için geliştirilmiştir anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="04a7a-117">*Automatic* means that an Azure AD provisioning connector has been developed for this application.</span></span> <span data-ttu-id="04a7a-118">Azure AD hizmeti ve nasıl çalıştığı, sağlama hello hakkında daha fazla bilgi için bkz: [otomatikleştirmek kullanıcı hazırlama ve sağlamayı kaldırma işlemlerini tooSaaS Azure Active Directory ile uygulamaları](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span><span class="sxs-lookup"><span data-stu-id="04a7a-118">For more information on hello Azure AD provisioning service and how it works, see [Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span></span>

<span data-ttu-id="04a7a-119">Tooprovision belirli kullanıcılar ve gruplar tooan uygulama nasıl görürüm hakkında daha fazla bilgi için [kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span><span class="sxs-lookup"><span data-stu-id="04a7a-119">For more information on how tooprovision specific users and groups tooan application, see [Managing user account provisioning for enterprise apps](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span></span>

<span data-ttu-id="04a7a-120">Gerçek adımları gerekli tooenable hello ve yapılandırma otomatik sağlamayı hello uygulamaya bağlı olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="04a7a-120">hello actual steps required tooenable and configure automatic provisioning vary depending on hello application.</span></span>

>[!NOTE]
><span data-ttu-id="04a7a-121">Uygulamanız için sağlama yukarı Kurulum öğretici belirli toosetting hello ve bu adımları tooconfigure hello uygulama ve Azure AD toocreate sağlama bağlantı hello bularak başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="04a7a-121">You should start by finding hello setup tutorial specific toosetting up provisioning for your application, and following those steps tooconfigure both hello app and Azure AD toocreate hello provisioning connection.</span></span> 
>
>

<span data-ttu-id="04a7a-122">Uygulama öğreticileri bulunabilir [nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span><span class="sxs-lookup"><span data-stu-id="04a7a-122">App tutorials can be found at [List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span></span>

<span data-ttu-id="04a7a-123">Sağlama yukarı ayarı tooreview kullanırken önemli şey tooconsider hello öznitelik eşlemelerini ve hangi kullanıcı (veya grubu) özellikleri akışı Azure AD toohello uygulamasından tanımlamak iş akışları ve yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="04a7a-123">An important thing tooconsider when setting up provisioning be tooreview and configure hello attribute mappings and workflows that define which user (or group) properties flow from Azure AD toohello application.</span></span> <span data-ttu-id="04a7a-124">Bu hello "eşleşen özellik" ayarı içerir kullanılan toouniquely olması tanımlamak ve eşleşen kullanıcıları/grupları hello iki sistemleri arasında.</span><span class="sxs-lookup"><span data-stu-id="04a7a-124">This includes setting hello “matching property” that be used toouniquely identify and match users/groups between hello two systems.</span></span> <span data-ttu-id="04a7a-125">Bu önemli işlemi hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="04a7a-125">For more information on this important process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04a7a-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="04a7a-126">Next steps</span></span>
[<span data-ttu-id="04a7a-127">Kullanıcı Azure Active Directory'de SaaS uygulamaları için öznitelik eşlemelerini hazırlama özelleştirme</span><span class="sxs-lookup"><span data-stu-id="04a7a-127">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

