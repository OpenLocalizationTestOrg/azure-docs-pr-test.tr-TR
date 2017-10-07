---
title: "Azure Active Directory B2C: Azure Active Directory B2C kiracısı oluşturma | Microsoft Docs"
description: "Nasıl toocreate bir Azure Active Directory B2C Kiracı üzerinde bir konu"
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
ms.openlocfilehash: e8b257d66c1f66ffb84f5d3d21b30b42eddcbac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-hello-azure-portal"></a><span data-ttu-id="d7f1c-103">Hello Azure portalında bir Azure Active Directory B2C kiracısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d7f1c-103">Create an Azure Active Directory B2C tenant in hello Azure portal</span></span>

<span data-ttu-id="d7f1c-104">Sipi tarafından düzenlenebilir.</span><span class="sxs-lookup"><span data-stu-id="d7f1c-104">Edited by Sipi.</span></span>

<span data-ttu-id="d7f1c-105">Bu Hızlı Başlangıç, yalnızca birkaç dakika içinde bir Microsoft Azure Active Directory (Azure AD) B2C Kiracı oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d7f1c-105">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="d7f1c-106">İşlemi tamamladığınızda, B2C uygulamaları kaydettirmek için B2C Kiracı toouse sahip.</span><span class="sxs-lookup"><span data-stu-id="d7f1c-106">When you're finished, you have a B2C tenant toouse for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7f1c-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d7f1c-107">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-tooazure"></a><span data-ttu-id="d7f1c-108">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="d7f1c-108">Log in tooAzure</span></span>

<span data-ttu-id="d7f1c-109">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d7f1c-109">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="d7f1c-110">Azure AD B2C kiracısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d7f1c-110">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="d7f1c-111">B2C özellikleri, var olan kiracılar etkinleştirilemez.</span><span class="sxs-lookup"><span data-stu-id="d7f1c-111">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="d7f1c-112">Toocreate Azure AD B2C kiracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7f1c-112">You need toocreate an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="d7f1c-113">Tebrikler, Azure Active Directory B2C kiracısı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="d7f1c-113">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="d7f1c-114">Merhaba Kiracı genel Yöneticisi olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="d7f1c-114">You are a Global Administrator of hello tenant.</span></span> <span data-ttu-id="d7f1c-115">Gerektiğinde başka Genel Yöneticiler ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7f1c-115">You can add other Global Administrators as required.</span></span> <span data-ttu-id="d7f1c-116">tooswitch tooyour yeni Kiracı, hello tıklatın *yeni Kiracı bağlantıyı Yönet*.</span><span class="sxs-lookup"><span data-stu-id="d7f1c-116">tooswitch tooyour new tenant, click hello *manage your new tenant link*.</span></span>

![Yeni Kiracı bağlantıyı Yönet](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="d7f1c-118">Toouse bir üretim uygulaması için bir B2C Kiracı planlıyorsanız hello makaleyi okuyun [Önizleme B2C kiracılar ve üretim ölçekli](active-directory-b2c-reference-tenant-type.md).</span><span class="sxs-lookup"><span data-stu-id="d7f1c-118">If you are planning toouse a B2C tenant for a production app, read hello article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="d7f1c-119">Var. Varolan bir B2C sildiğinizde Kiracı bilinen sorunlar ve hello ile yeniden oluşturmanız aynı etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="d7f1c-119">There are known issues when you delete an existing B2C tenant and re-create it with hello same domain name.</span></span> <span data-ttu-id="d7f1c-120">B2C Kiracı farklı etki alanı adı ile toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7f1c-120">You need toocreate a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-tooyour-subscription"></a><span data-ttu-id="d7f1c-121">Kiracı tooyour aboneliğinizi Bağla</span><span class="sxs-lookup"><span data-stu-id="d7f1c-121">Link your tenant tooyour subscription</span></span>

<span data-ttu-id="d7f1c-122">Toolink gereken Azure AD B2C tooyour Azure aboneliği tooenable tüm B2C işlevselliği Kiracı ve kullanım ücretleri için ödeme yaparsınız.</span><span class="sxs-lookup"><span data-stu-id="d7f1c-122">You need toolink your Azure AD B2C tenant tooyour Azure subscription tooenable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="d7f1c-123">toolearn daha fazlasını okuyun [bu makalede](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="d7f1c-123">toolearn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="d7f1c-124">Azure AD B2C Kiracı tooyour Azure aboneliği bağlarsanız yok, bazı işlevler engellenir ve bir uyarı iletisi ("bağlantılı toothis B2C Kiracı veya abonelik hello abonelik, ilgilenilmesi gerekiyor. hello B2C ayarlarında gerekir") bakın.</span><span class="sxs-lookup"><span data-stu-id="d7f1c-124">If you don't link your Azure AD B2C tenant tooyour Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked toothis B2C tenant or hello Subscription needs your attention.") in hello B2C settings.</span></span> <span data-ttu-id="d7f1c-125">Üretime uygulamalarınızı sevk önce bu adımı uygulamanız önemlidir.</span><span class="sxs-lookup"><span data-stu-id="d7f1c-125">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-toosettings"></a><span data-ttu-id="d7f1c-126">Kolay erişim toosettings</span><span class="sxs-lookup"><span data-stu-id="d7f1c-126">Easy access toosettings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="d7f1c-127">Girerek hello dikey erişebilirsiniz `Azure AD B2C` içinde **arama kaynakları** hello portal hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="d7f1c-127">You can also access hello blade by entering `Azure AD B2C` in **Search resources** at hello top of hello portal.</span></span> <span data-ttu-id="d7f1c-128">Merhaba sonuçları listesinden seçmek **Azure AD B2C** tooaccess hello B2C ayarlar dikey penceresi.</span><span class="sxs-lookup"><span data-stu-id="d7f1c-128">In hello results list, select **Azure AD B2C** tooaccess hello B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7f1c-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d7f1c-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d7f1c-130">B2C Kiracı B2C uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="d7f1c-130">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)
