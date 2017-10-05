---
title: "Lisanssız kullanım raporu | Microsoft Docs"
description: "Kullanmakta olduğunuz lisanssız kullanıcıları tanımlamak lisanssız kullanım raporu yardımcı olur, Azure AD özelliklerini Ücretli."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: c0b4f455f067e825362bdecc02ea62d7984f0d31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="1e46a-103">Lisanssız kullanım raporu</span><span class="sxs-lookup"><span data-stu-id="1e46a-103">Unlicensed usage report</span></span>
<span data-ttu-id="1e46a-104">Kullanmakta olduğunuz lisanssız kullanıcıları tanımlamak lisanssız kullanım raporu yardımcı olur, Azure AD özelliklerini Ücretli.</span><span class="sxs-lookup"><span data-stu-id="1e46a-104">The unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="1e46a-105">Bu, daha iyi hale getirmek için satın aldığınız lisansların kullanmanız ve Ek lisanslar gerekebilir tanımlamak için çalıştığınızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="1e46a-105">This allows you to make better use of licenses that you have purchased and to identify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="1e46a-106">Rapor son 30 gün içinde Ücretli özellikler etkin kullanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="1e46a-106">The report shows active usage of the paid features in the last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="1e46a-107">Rapor yapısı</span><span class="sxs-lookup"><span data-stu-id="1e46a-107">Report structure</span></span>
| <span data-ttu-id="1e46a-108">Sütun adı</span><span class="sxs-lookup"><span data-stu-id="1e46a-108">Column name</span></span> | <span data-ttu-id="1e46a-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e46a-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1e46a-110">Lisanssız kullanıcı</span><span class="sxs-lookup"><span data-stu-id="1e46a-110">Unlicensed User</span></span> |<span data-ttu-id="1e46a-111">Kullanıcının adı</span><span class="sxs-lookup"><span data-stu-id="1e46a-111">Name of the user</span></span> |
| <span data-ttu-id="1e46a-112">Özellik</span><span class="sxs-lookup"><span data-stu-id="1e46a-112">Feature</span></span> |<span data-ttu-id="1e46a-113">Özellik adı.</span><span class="sxs-lookup"><span data-stu-id="1e46a-113">The feature name.</span></span> <span data-ttu-id="1e46a-114">Örneğin: koşullu erişim</span><span class="sxs-lookup"><span data-stu-id="1e46a-114">For example: conditional access</span></span> |
| <span data-ttu-id="1e46a-115">Erişilen uygulama</span><span class="sxs-lookup"><span data-stu-id="1e46a-115">Application Accessed</span></span> |<span data-ttu-id="1e46a-116">Özelliği ile erişilen uygulamanın adı.</span><span class="sxs-lookup"><span data-stu-id="1e46a-116">The name of the application that is being accessed with the feature.</span></span> <span data-ttu-id="1e46a-117">Örneğin: Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="1e46a-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="1e46a-118">Bir kullanıcı hesabı silindiyse 'Lisanssız kullanıcı' sütunu, 1003000090D8B285 gibi bir kimliği kullanılarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="1e46a-118">If a user account has been deleted the ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="1e46a-119">Koşullu erişim özelliği</span><span class="sxs-lookup"><span data-stu-id="1e46a-119">Conditional access feature</span></span>
<span data-ttu-id="1e46a-120">Bir Azure AD Premium lisansı yoksa uygulanan koşullu erişim ilkesine sahip bir hizmeti eriştiklerinde lisanssız kullanıcılar işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="1e46a-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="1e46a-121">Bu MFA için geçerlidir / aygıt yanı sıra konumu ilkeleri ilkeler, Intune kullanın.</span><span class="sxs-lookup"><span data-stu-id="1e46a-121">This applies to MFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="1e46a-122">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="1e46a-122">See also</span></span>
* [<span data-ttu-id="1e46a-123">Office 365 ve diğer Azure Active Directory ile koşullu erişim kullanarak bağlı uygulamalar</span><span class="sxs-lookup"><span data-stu-id="1e46a-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="1e46a-124">Azure AD koşullu erişimi kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="1e46a-124">Getting started with conditional access to Azure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

