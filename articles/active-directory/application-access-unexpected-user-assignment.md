---
title: "Uygulamalar için atama kullanıcılara nasıl | Microsoft Docs"
description: "Uygulamaya kiracınızda kullanıcılara nasıl atanacağını anlama"
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
ms.openlocfilehash: 916238ba402a2555bac620d7f08e02799d981ae0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-assign-users-to-applications"></a><span data-ttu-id="54102-103">Kullanıcılar uygulamalara atama</span><span class="sxs-lookup"><span data-stu-id="54102-103">How to assign users to applications</span></span>

<span data-ttu-id="54102-104">Bu makalede uygulamaya kiracınızda kullanıcılara nasıl atanacağını anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="54102-104">This article help you to understand how users get assigned to an application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-to-an-application-in-azure-ad"></a><span data-ttu-id="54102-105">Nasıl kullanıcılar Azure AD'de bir uygulamaya atanır?</span><span class="sxs-lookup"><span data-stu-id="54102-105">How do users get assigned to an application in Azure AD?</span></span>

<span data-ttu-id="54102-106">Bir kullanıcı bir uygulamaya erişmek öncelikle ona herhangi bir yolla atanmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="54102-106">For a user to access an application, they must first be assigned to it in some way.</span></span> <span data-ttu-id="54102-107">Atama bir yönetici, bir iş temsilci veya kullanıcı tarafından bazı durumlarda, kendilerini gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="54102-107">Assignment can be performed by an administrator, a business delegate, or sometimes, the user themselves.</span></span> <span data-ttu-id="54102-108">Aşağıda kullanıcılar uygulamalarına atanan yolları açıklanır:</span><span class="sxs-lookup"><span data-stu-id="54102-108">Below describes the ways users can get assigned to applications:</span></span>

1.  <span data-ttu-id="54102-109">Bir yönetici [kullanıcı atar](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) uygulamaya doğrudan</span><span class="sxs-lookup"><span data-stu-id="54102-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) to the application directly</span></span>

2.  <span data-ttu-id="54102-110">Bir yönetici [bir grup atar](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) kullanıcının uygulamaya bir üyesi olduğunu da dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="54102-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that the user is a member of to the application, including:</span></span>

  * <span data-ttu-id="54102-111">Şirket içi eşitlendiği bir grup</span><span class="sxs-lookup"><span data-stu-id="54102-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="54102-112">Bulutta oluşturulan bir statik güvenlik grubu</span><span class="sxs-lookup"><span data-stu-id="54102-112">A static security group created in the cloud</span></span>

  * <span data-ttu-id="54102-113">A [dinamik güvenlik grubu](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) bulutta oluşturulan</span><span class="sxs-lookup"><span data-stu-id="54102-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in the cloud</span></span>

  * <span data-ttu-id="54102-114">Bulutta oluşturulan bir Office 365 Grup</span><span class="sxs-lookup"><span data-stu-id="54102-114">An Office 365 group created in the cloud</span></span>

  * <span data-ttu-id="54102-115">[Tüm kullanıcılar](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) grubu</span><span class="sxs-lookup"><span data-stu-id="54102-115">The [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="54102-116">Yöneticinin paylaşılan [Self Servis uygulamaya erişim](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) kullanarak bir uygulama eklemek bir kullanıcı izin vermek için [uygulama erişim Paneli'ne](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **uygulama Ekle** özelliği **iş onayı olmadan**</span><span class="sxs-lookup"><span data-stu-id="54102-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="54102-117">Yöneticinin paylaşılan [Self Servis uygulamaya erişim](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) kullanarak bir uygulama eklemek bir kullanıcı izin vermek için [uygulama erişim Paneli'ne](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **uygulama Ekle** özellik, ancak yalnızca w**i önceki onay iş onaylayanlar seçili kümesinden**</span><span class="sxs-lookup"><span data-stu-id="54102-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="54102-118">Yöneticinin paylaşılan [Self Servis Grup Yönetimi](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) uygulamanın atandığı bir gruba katılması bir kullanıcı izin vermek için **iş onayı olmadan**</span><span class="sxs-lookup"><span data-stu-id="54102-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to **without business approval**</span></span>

6.  <span data-ttu-id="54102-119">Yöneticinin paylaşılan [Self Servis Grup Yönetimi](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) bir kullanıcı bir uygulama için ancak yalnızca atanmış bir gruba katılmak izin vermek için **iş onaylayanlar seçili kümesinden önceki onay ile**</span><span class="sxs-lookup"><span data-stu-id="54102-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="54102-120">Yönetici bir lisans doğrudan birinci taraf uygulama için bir kullanıcı gibi atar [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="54102-120">An administrator assigns a license to a user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="54102-121">Bir yönetici, kullanıcı gibi birinci taraf uygulama için bir üyesi olan bir gruba bir lisans atar [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="54102-121">An administrator assigns a license to a group that the user is a member of to a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="54102-122">Bir [yönetici uygulamaya izin](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) tüm kullanıcılar ve sonra bir kullanıcı tarafından kullanılmak üzere oturum açtığında uygulamaya</span><span class="sxs-lookup"><span data-stu-id="54102-122">An [administrator consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to be used by all users and then a user signs in to the application</span></span>

10. <span data-ttu-id="54102-123">Bir kullanıcı [izin uygulamaya](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) tek başına uygulamayı oturum açma</span><span class="sxs-lookup"><span data-stu-id="54102-123">A user [consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in to the application</span></span>

## <a name="next-steps"></a><span data-ttu-id="54102-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="54102-124">Next steps</span></span>
[<span data-ttu-id="54102-125">Azure Active Directory ile uygulamaları yönetme</span><span class="sxs-lookup"><span data-stu-id="54102-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
