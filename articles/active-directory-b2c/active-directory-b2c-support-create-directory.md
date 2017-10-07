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
ms.openlocfilehash: 4bb7ec6ec67d3368a0e36c098f290f582510714a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a><span data-ttu-id="7c417-103">Bir Azure Active Directory veya Azure Active Directory B2C kiracısı oluşturma sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="7c417-103">Troubleshoot creating an Azure Active Directory or Azure Active Directory B2C tenant</span></span> 

## <a name="create-an-azure-ad-tenant"></a><span data-ttu-id="7c417-104">Azure AD kiracısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c417-104">Create an Azure AD tenant</span></span>
<span data-ttu-id="7c417-105">Bir Azure Active Directory (Azure AD) Kiracı hello ilk denemede oluşturulamıyor, yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="7c417-105">If you can't create an Azure Active Directory (Azure AD) tenant on hello first attempt, try again.</span></span> <span data-ttu-id="7c417-106">Merhaba sorun devam ederse, Azure desteğine başvurun.</span><span class="sxs-lookup"><span data-stu-id="7c417-106">If hello problem persists, contact Azure Support.</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="7c417-107">Azure AD B2C kiracısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c417-107">Create an Azure AD B2C tenant</span></span>
<span data-ttu-id="7c417-108">Sorunlarla karşılaşırsanız olduğunda, [bir Azure Active Directory B2C oluşturun (Azure AD B2C) Kiracı](active-directory-b2c-get-started.md), aşağıdaki seçenekleri şu hello deneyin:</span><span class="sxs-lookup"><span data-stu-id="7c417-108">If you encounter issues when you [create an Azure Active Directory B2C (Azure AD B2C) tenant](active-directory-b2c-get-started.md), try hello following options:</span></span>

* <span data-ttu-id="7c417-109">Hello Azure AD B2C Kiracı kiracılar listenizde göstermez, toocreate hello Kiracı yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="7c417-109">If hello Azure AD B2C tenant doesn't show up in your list of tenants, try again toocreate hello tenant.</span></span>
* <span data-ttu-id="7c417-110">Hello Azure AD B2C Kiracı kiracılar listenizde göstermez ve hello aşağıdaki hata iletisini görüyorsanız hello Kiracı silin ve yeniden oluşturun:</span><span class="sxs-lookup"><span data-stu-id="7c417-110">If hello Azure AD B2C tenant does show up in your list of tenants and you see hello following  error message, delete hello tenant and create it again:</span></span>

    <span data-ttu-id="7c417-111">"Hello B2C kiracısının 'contosob2c' hello oluşturma işlemini tamamlayamadı.</span><span class="sxs-lookup"><span data-stu-id="7c417-111">"Could not complete hello creation of hello B2C tenant 'contosob2c'.</span></span> <span data-ttu-id="7c417-112">Lütfen bu ziyaret [bağlantı](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) daha fazla yardım için. "</span><span class="sxs-lookup"><span data-stu-id="7c417-112">Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance."</span></span>
* <span data-ttu-id="7c417-113">Var olan bir Azure AD B2C sildiğinizde sorunları Kiracı ve hello kullanarak yeniden oluşturun bilinen vardır aynı etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="7c417-113">There are known issues when you delete an existing Azure AD B2C tenant and re-create it by using hello same domain name.</span></span> <span data-ttu-id="7c417-114">Yeni bir Azure AD B2C kiracısı oluşturduğunuzda, farklı etki alanı adı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c417-114">When you create a new Azure AD B2C tenant, you must use a different domain name.</span></span>
* <span data-ttu-id="7c417-115">Bu çözümler işe yaramazsa, Azure desteğine başvurun.</span><span class="sxs-lookup"><span data-stu-id="7c417-115">If these resolutions don't work, contact Azure Support.</span></span> <span data-ttu-id="7c417-116">Daha fazla bilgi için bkz: [Azure AD B2C için dosya desteği istekleri](active-directory-b2c-support.md).</span><span class="sxs-lookup"><span data-stu-id="7c417-116">For more information, see [File support requests for Azure AD B2C](active-directory-b2c-support.md).</span></span>

