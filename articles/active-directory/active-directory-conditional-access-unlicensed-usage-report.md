---
title: "aaaUnlicensed kullanım raporu | Microsoft Docs"
description: "Azure AD özelliklerini kullanan lisanssız kullanıcılar tanımlamak yardımcı Ücretli lisanssız kullanım raporu hello."
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
ms.openlocfilehash: c44d1756b4641d7ca88434017eedb6c5e2567cb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="82310-103">Lisanssız kullanım raporu</span><span class="sxs-lookup"><span data-stu-id="82310-103">Unlicensed usage report</span></span>
<span data-ttu-id="82310-104">Azure AD özelliklerini kullanan lisanssız kullanıcılar tanımlamak yardımcı Ücretli lisanssız kullanım raporu hello.</span><span class="sxs-lookup"><span data-stu-id="82310-104">hello unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="82310-105">Bu, satın aldığınız lisansların ve Ek lisanslar gerektiğinde bildiğiniz tooidentify daha iyi kullanımını toomake sağlar.</span><span class="sxs-lookup"><span data-stu-id="82310-105">This allows you toomake better use of licenses that you have purchased and tooidentify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="82310-106">Merhaba rapor özelliklerini hello son 30 gün Ücretli hello etkin kullanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="82310-106">hello report shows active usage of hello paid features in hello last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="82310-107">Rapor yapısı</span><span class="sxs-lookup"><span data-stu-id="82310-107">Report structure</span></span>
| <span data-ttu-id="82310-108">Sütun adı</span><span class="sxs-lookup"><span data-stu-id="82310-108">Column name</span></span> | <span data-ttu-id="82310-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="82310-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="82310-110">Lisanssız kullanıcı</span><span class="sxs-lookup"><span data-stu-id="82310-110">Unlicensed User</span></span> |<span data-ttu-id="82310-111">Merhaba kullanıcının adı</span><span class="sxs-lookup"><span data-stu-id="82310-111">Name of hello user</span></span> |
| <span data-ttu-id="82310-112">Özellik</span><span class="sxs-lookup"><span data-stu-id="82310-112">Feature</span></span> |<span data-ttu-id="82310-113">Merhaba özellik adı.</span><span class="sxs-lookup"><span data-stu-id="82310-113">hello feature name.</span></span> <span data-ttu-id="82310-114">Örneğin: koşullu erişim</span><span class="sxs-lookup"><span data-stu-id="82310-114">For example: conditional access</span></span> |
| <span data-ttu-id="82310-115">Erişilen uygulama</span><span class="sxs-lookup"><span data-stu-id="82310-115">Application Accessed</span></span> |<span data-ttu-id="82310-116">Merhaba özelliğiyle erişilen hello uygulamasının Hello adı.</span><span class="sxs-lookup"><span data-stu-id="82310-116">hello name of hello application that is being accessed with hello feature.</span></span> <span data-ttu-id="82310-117">Örneğin: Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="82310-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="82310-118">'Lisanssız sütunu doldurulur kullanıcı' 1003000090D8B285 gibi bir Kimliğe sahip bir kullanıcı hesabı silindiyse hello</span><span class="sxs-lookup"><span data-stu-id="82310-118">If a user account has been deleted hello ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="82310-119">Koşullu erişim özelliği</span><span class="sxs-lookup"><span data-stu-id="82310-119">Conditional access feature</span></span>
<span data-ttu-id="82310-120">Bir Azure AD Premium lisansı yoksa uygulanan koşullu erişim ilkesine sahip bir hizmeti eriştiklerinde lisanssız kullanıcılar işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="82310-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="82310-121">Bu tooMFA geçerlidir / aygıt yanı sıra konumu ilkeleri ilkeler, Intune kullanın.</span><span class="sxs-lookup"><span data-stu-id="82310-121">This applies tooMFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="82310-122">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="82310-122">See also</span></span>
* [<span data-ttu-id="82310-123">Office 365 ve diğer Azure Active Directory ile koşullu erişim kullanarak bağlı uygulamalar</span><span class="sxs-lookup"><span data-stu-id="82310-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="82310-124">Koşullu erişim tooAzure AD ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="82310-124">Getting started with conditional access tooAzure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

