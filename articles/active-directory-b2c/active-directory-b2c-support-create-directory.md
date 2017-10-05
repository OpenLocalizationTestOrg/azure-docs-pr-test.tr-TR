---
title: "Azure Active Directory B2C: oluşturma kiracılar sorunlarını giderme | Microsoft Docs"
description: "Sorunlar ve çözümleri bir Azure Active Directory veya Azure Active Directory B2C kiracısı oluşturma."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 7ba4c6b2-161b-45b5-b3bd-ccb662f5d7a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 81af4536fc223319369aff262d42149cfbf1a1e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a><span data-ttu-id="b3c66-103">Bir Azure Active Directory veya Azure Active Directory B2C kiracısı oluşturma sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="b3c66-103">Troubleshoot creating an Azure Active Directory or Azure Active Directory B2C tenant</span></span> 

## <a name="create-an-azure-ad-tenant"></a><span data-ttu-id="b3c66-104">Azure AD kiracısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b3c66-104">Create an Azure AD tenant</span></span>
<span data-ttu-id="b3c66-105">İlk denemede bir Azure Active Directory (Azure AD) Kiracı oluşturamıyorsanız, yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="b3c66-105">If you can't create an Azure Active Directory (Azure AD) tenant on the first attempt, try again.</span></span> <span data-ttu-id="b3c66-106">Sorun devam ederse, Azure desteğine başvurun.</span><span class="sxs-lookup"><span data-stu-id="b3c66-106">If the problem persists, contact Azure Support.</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="b3c66-107">Azure AD B2C kiracısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b3c66-107">Create an Azure AD B2C tenant</span></span>
<span data-ttu-id="b3c66-108">Sorunlarla karşılaşırsanız olduğunda, [bir Azure Active Directory B2C oluşturun (Azure AD B2C) Kiracı](active-directory-b2c-get-started.md), aşağıdaki seçenekleri deneyin:</span><span class="sxs-lookup"><span data-stu-id="b3c66-108">If you encounter issues when you [create an Azure Active Directory B2C (Azure AD B2C) tenant](active-directory-b2c-get-started.md), try the following options:</span></span>

* <span data-ttu-id="b3c66-109">Azure AD B2C kiracısı kiracılar listenizde göstermez, Kiracı oluşturmak yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="b3c66-109">If the Azure AD B2C tenant doesn't show up in your list of tenants, try again to create the tenant.</span></span>
* <span data-ttu-id="b3c66-110">Azure AD B2C kiracısı kiracılar listenizde göstermez ve aşağıdaki hata iletisini görüyorsanız, Kiracı silin ve yeniden oluşturun:</span><span class="sxs-lookup"><span data-stu-id="b3c66-110">If the Azure AD B2C tenant does show up in your list of tenants and you see the following  error message, delete the tenant and create it again:</span></span>

    <span data-ttu-id="b3c66-111">"'Contosob2c' B2C kiracısı oluşturma işlemini tamamlayamadı.</span><span class="sxs-lookup"><span data-stu-id="b3c66-111">"Could not complete the creation of the B2C tenant 'contosob2c'.</span></span> <span data-ttu-id="b3c66-112">Lütfen bu ziyaret [bağlantı](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) daha fazla yardım için. "</span><span class="sxs-lookup"><span data-stu-id="b3c66-112">Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance."</span></span>
* <span data-ttu-id="b3c66-113">Var olan Azure AD B2C kiracısı silin ve yeniden oluşturun aynı etki alanı adını kullanarak, bilinen sorunlar vardır.</span><span class="sxs-lookup"><span data-stu-id="b3c66-113">There are known issues when you delete an existing Azure AD B2C tenant and re-create it by using the same domain name.</span></span> <span data-ttu-id="b3c66-114">Yeni bir Azure AD B2C kiracısı oluşturduğunuzda, farklı etki alanı adı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3c66-114">When you create a new Azure AD B2C tenant, you must use a different domain name.</span></span>
* <span data-ttu-id="b3c66-115">Bu çözümler işe yaramazsa, Azure desteğine başvurun.</span><span class="sxs-lookup"><span data-stu-id="b3c66-115">If these resolutions don't work, contact Azure Support.</span></span> <span data-ttu-id="b3c66-116">Daha fazla bilgi için bkz: [Azure AD B2C için dosya desteği istekleri](active-directory-b2c-support.md).</span><span class="sxs-lookup"><span data-stu-id="b3c66-116">For more information, see [File support requests for Azure AD B2C](active-directory-b2c-support.md).</span></span>

