---
title: "Azure Active Directory B2C: Azure Active Directory B2C kiracısı oluşturma | Microsoft Docs"
description: "Azure Active Directory B2C kiracısının nasıl oluşturulacağına ilişkin konu başlığı"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: swkrish
ms.openlocfilehash: 1a7eb94e3c74aa0dc187a6d203ba0cf885b97c4d
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/28/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-the-azure-portal"></a><span data-ttu-id="d7a32-103">Azure portalında bir Azure Active Directory B2C kiracısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d7a32-103">Create an Azure Active Directory B2C tenant in the Azure portal</span></span>

<span data-ttu-id="d7a32-104">Sipi tarafından düzenlenebilir.</span><span class="sxs-lookup"><span data-stu-id="d7a32-104">Edited by Sipi.</span></span>

<span data-ttu-id="d7a32-105">Bu Hızlı Başlangıç, yalnızca birkaç dakika içinde bir Microsoft Azure Active Directory (Azure AD) B2C Kiracı oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d7a32-105">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="d7a32-106">İşlemi tamamladığınızda, B2C uygulamaları kaydetmek için kullanılacak bir B2C kiracısına sahip.</span><span class="sxs-lookup"><span data-stu-id="d7a32-106">When you're finished, you have a B2C tenant to use for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7a32-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d7a32-107">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-to-azure"></a><span data-ttu-id="d7a32-108">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="d7a32-108">Log in to Azure</span></span>

<span data-ttu-id="d7a32-109">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d7a32-109">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="d7a32-110">Azure AD B2C kiracısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d7a32-110">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="d7a32-111">B2C özellikleri, var olan kiracılar etkinleştirilemez.</span><span class="sxs-lookup"><span data-stu-id="d7a32-111">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="d7a32-112">Azure AD B2C kiracısı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7a32-112">You need to create an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="d7a32-113">Tebrikler, Azure Active Directory B2C kiracısı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="d7a32-113">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="d7a32-114">Kiracı genel Yöneticisi olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="d7a32-114">You are a Global Administrator of the tenant.</span></span> <span data-ttu-id="d7a32-115">Gerektiğinde başka Genel Yöneticiler ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7a32-115">You can add other Global Administrators as required.</span></span> <span data-ttu-id="d7a32-116">Yeni Kiracı için geçiş yapmak için tıklatın *yeni Kiracı bağlantıyı Yönet*.</span><span class="sxs-lookup"><span data-stu-id="d7a32-116">To switch to your new tenant, click the *manage your new tenant link*.</span></span>

![Yeni Kiracı bağlantıyı Yönet](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="d7a32-118">Bir üretim uygulaması için bir B2C Kiracı kullanmayı planlıyorsanız, makaleyi okuyun [Önizleme B2C kiracılar ve üretim ölçekli](active-directory-b2c-reference-tenant-type.md).</span><span class="sxs-lookup"><span data-stu-id="d7a32-118">If you are planning to use a B2C tenant for a production app, read the article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="d7a32-119">Mevcut bir B2C Kiracı silin ve aynı etki alanı adıyla yeniden oluştururken bilinen sorunlar vardır.</span><span class="sxs-lookup"><span data-stu-id="d7a32-119">There are known issues when you delete an existing B2C tenant and re-create it with the same domain name.</span></span> <span data-ttu-id="d7a32-120">Farklı bir etki alanı adı ile bir B2C Kiracı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7a32-120">You need to create a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-to-your-subscription"></a><span data-ttu-id="d7a32-121">Kiracı aboneliğinize bağlantı</span><span class="sxs-lookup"><span data-stu-id="d7a32-121">Link your tenant to your subscription</span></span>

<span data-ttu-id="d7a32-122">Azure aboneliğiniz için kullanım ücretleri ödeme tüm B2C işlevselliğini etkinleştirmek için Azure AD B2C kiracınızın bağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7a32-122">You need to link your Azure AD B2C tenant to your Azure subscription to enable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="d7a32-123">Daha fazla bilgi edinmek için okuma [bu makalede](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="d7a32-123">To learn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="d7a32-124">Azure aboneliğinize Azure AD B2C kiracınızın bağlantı yok, bazı işlevler engellenir ve bir uyarı iletisi ("abonelik bu B2C Kiracı veya abonelik gereksinimlerinize, ilgilenilmesi gerekiyor. B2C ayarlarında bağlı") bakın.</span><span class="sxs-lookup"><span data-stu-id="d7a32-124">If you don't link your Azure AD B2C tenant to your Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked to this B2C tenant or the Subscription needs your attention.") in the B2C settings.</span></span> <span data-ttu-id="d7a32-125">Üretime uygulamalarınızı sevk önce bu adımı uygulamanız önemlidir.</span><span class="sxs-lookup"><span data-stu-id="d7a32-125">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-to-settings"></a><span data-ttu-id="d7a32-126">Kolay erişim ayarları</span><span class="sxs-lookup"><span data-stu-id="d7a32-126">Easy access to settings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="d7a32-127">Girerek dikey erişebilirsiniz `Azure AD B2C` içinde **arama kaynakları** portalı üstündeki.</span><span class="sxs-lookup"><span data-stu-id="d7a32-127">You can also access the blade by entering `Azure AD B2C` in **Search resources** at the top of the portal.</span></span> <span data-ttu-id="d7a32-128">Sonuçlar listesinde **Azure AD B2C** B2C ayarlar dikey erişmek için.</span><span class="sxs-lookup"><span data-stu-id="d7a32-128">In the results list, select **Azure AD B2C** to access the B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7a32-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d7a32-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d7a32-130">B2C Kiracı B2C uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="d7a32-130">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)
