---
title: "aaaHow tooAssign kullanıcılar tooapplications | Microsoft Docs"
description: "Kullanıcılar Kiracı tooan uygulamada nasıl atanır anlama"
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
ms.openlocfilehash: 4df60c7d723140d0d1bbd6ba8b34aa4e762d1138
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-tooapplications"></a><span data-ttu-id="3454f-103">Nasıl tooassign kullanıcılar tooapplications</span><span class="sxs-lookup"><span data-stu-id="3454f-103">How tooassign users tooapplications</span></span>

<span data-ttu-id="3454f-104">Bu makale toounderstand yardımcı kullanıcılar Kiracı tooan uygulamada nasıl atanır.</span><span class="sxs-lookup"><span data-stu-id="3454f-104">This article help you toounderstand how users get assigned tooan application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-tooan-application-in-azure-ad"></a><span data-ttu-id="3454f-105">Nasıl kullanıcılar Azure AD'de tooan uygulama atanır?</span><span class="sxs-lookup"><span data-stu-id="3454f-105">How do users get assigned tooan application in Azure AD?</span></span>

<span data-ttu-id="3454f-106">Bir kullanıcı tooaccess bir uygulama için önce bir şekilde tooit atanmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="3454f-106">For a user tooaccess an application, they must first be assigned tooit in some way.</span></span> <span data-ttu-id="3454f-107">Atama bir yönetici, bir iş temsilci veya hello kullanıcı tarafından bazı durumlarda, kendilerini gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="3454f-107">Assignment can be performed by an administrator, a business delegate, or sometimes, hello user themselves.</span></span> <span data-ttu-id="3454f-108">Aşağıda kullanıcılar tooapplications atanan hello yolları açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="3454f-108">Below describes hello ways users can get assigned tooapplications:</span></span>

1.  <span data-ttu-id="3454f-109">Bir yönetici [kullanıcı atar](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) doğrudan toohello uygulama</span><span class="sxs-lookup"><span data-stu-id="3454f-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) toohello application directly</span></span>

2.  <span data-ttu-id="3454f-110">Bir yönetici [bir grup atar](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) bu hello kullanıcının toohello uygulama üyesi olduğu da dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="3454f-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that hello user is a member of toohello application, including:</span></span>

  * <span data-ttu-id="3454f-111">Şirket içi eşitlendiği bir grup</span><span class="sxs-lookup"><span data-stu-id="3454f-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="3454f-112">Merhaba bulutta oluşturulan bir statik güvenlik grubu</span><span class="sxs-lookup"><span data-stu-id="3454f-112">A static security group created in hello cloud</span></span>

  * <span data-ttu-id="3454f-113">A [dinamik güvenlik grubu](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) hello bulutta oluşturulan</span><span class="sxs-lookup"><span data-stu-id="3454f-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in hello cloud</span></span>

  * <span data-ttu-id="3454f-114">Merhaba bulutta oluşturulan bir Office 365 Grup</span><span class="sxs-lookup"><span data-stu-id="3454f-114">An Office 365 group created in hello cloud</span></span>

  * <span data-ttu-id="3454f-115">Merhaba [tüm kullanıcılar](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) grubu</span><span class="sxs-lookup"><span data-stu-id="3454f-115">hello [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="3454f-116">Yöneticinin paylaşılan [Self Servis uygulamaya erişim](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) kullanarak bir uygulama bir kullanıcı tooadd hello tooallow [uygulama erişim Paneli'ne](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **uygulama Ekle** özelliği **iş onayı olmadan**</span><span class="sxs-lookup"><span data-stu-id="3454f-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow a user tooadd an application using hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="3454f-117">Yöneticinin paylaşılan [Self Servis uygulamaya erişim](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) kullanarak bir uygulama bir kullanıcı tooadd hello tooallow [uygulama erişim Paneli'ne](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **uygulama Ekle** özellik, ancak yalnızca w **iş onaylayanlar seçili kümesinden i önceki onayı**</span><span class="sxs-lookup"><span data-stu-id="3454f-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow a user tooadd an application using hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="3454f-118">Yöneticinin paylaşılan [Self Servis Grup Yönetimi](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow kullanıcı toojoin uygulamanın çok atanmış bir gruba**iş onayı olmadan**</span><span class="sxs-lookup"><span data-stu-id="3454f-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow a user toojoin a group that an application is assigned too**without business approval**</span></span>

6.  <span data-ttu-id="3454f-119">Yöneticinin yerel veya uzak [Self Servis Grup Yönetimi](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow kullanıcı toojoin bir uygulama için ancak yalnızca atanmış bir gruba **iş onaylayanlar seçili kümesinden önceki Onayla**</span><span class="sxs-lookup"><span data-stu-id="3454f-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow a user toojoin a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="3454f-120">Bir yönetici gibi bir lisans tooa kullanıcı birinci taraf uygulama için doğrudan atar [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="3454f-120">An administrator assigns a license tooa user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="3454f-121">Kullanıcı hello lisans tooa grubunun bir üyesidir tooa birinci taraf uygulama gibi bir yönetici atar [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="3454f-121">An administrator assigns a license tooa group that hello user is a member of tooa first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="3454f-122">Bir [yönetici izin tooan uygulama](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe tüm kullanıcılar tarafından kullanılan ve toohello uygulamada bir kullanıcı oturum açtığında</span><span class="sxs-lookup"><span data-stu-id="3454f-122">An [administrator consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe used by all users and then a user signs in toohello application</span></span>

10. <span data-ttu-id="3454f-123">Bir kullanıcı [tooan uygulama izin](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) kendilerini toohello uygulamada oturum açarak</span><span class="sxs-lookup"><span data-stu-id="3454f-123">A user [consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in toohello application</span></span>

## <a name="next-steps"></a><span data-ttu-id="3454f-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3454f-124">Next steps</span></span>
[<span data-ttu-id="3454f-125">Azure Active Directory ile uygulamaları yönetme</span><span class="sxs-lookup"><span data-stu-id="3454f-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
