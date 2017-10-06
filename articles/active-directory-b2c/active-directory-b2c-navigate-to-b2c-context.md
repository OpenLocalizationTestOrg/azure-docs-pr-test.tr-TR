---
title: "Azure Active Directory B2C: Geçiş tooa B2C Kiracı | Microsoft Docs"
description: "Active Directory B2C Merhaba içeriğine içine tooswitch nasıl Kiracı"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 0eb1b198-44d3-4065-9fae-16591a8d3eae
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/13/2017
ms.author: parakhj
ms.openlocfilehash: 572f9ab283ecac68d284bb04fdfc98575bcf9393
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="switching-tooyour-azure-ad-b2c-tenant"></a><span data-ttu-id="b3722-103">Tooyour Azure AD B2C Kiracı değiştirme</span><span class="sxs-lookup"><span data-stu-id="b3722-103">Switching tooyour Azure AD B2C tenant</span></span>

<span data-ttu-id="b3722-104">Sipariş tooconfigure Azure AD B2C'da, Azure AD B2C kiracınızın hello bağlamda toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3722-104">In order tooconfigure Azure AD B2C, you need toobe in hello context of your Azure AD B2C tenant.</span></span>

## <a name="log-into-azure-ad-b2c-tenant"></a><span data-ttu-id="b3722-105">Azure AD B2C kiracınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b3722-105">Log into Azure AD B2C tenant</span></span>

<span data-ttu-id="b3722-106">Azure AD B2C toonavigate tooyour Kiracı, Azure portal hello hello Azure AD B2C kiracısının genel yönetici olarak oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3722-106">toonavigate tooyour Azure AD B2C tenant, you must be logged into hello Azure portal as a global administrator of hello Azure AD B2C tenant.</span></span>

1. <span data-ttu-id="b3722-107">Merhaba içine oturum [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b3722-107">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
1. <span data-ttu-id="b3722-108">Kiracılar, e-posta adresi veya resim hello sağ üst köşedeki tıklayarak geçin.</span><span class="sxs-lookup"><span data-stu-id="b3722-108">Switch tenants by clicking your email address or picture in hello top-right corner.</span></span>
1. <span data-ttu-id="b3722-109">Merhaba, `Directory` , toomanage istediğiniz select hello Azure AD B2C Kiracı görünür listesi.</span><span class="sxs-lookup"><span data-stu-id="b3722-109">In hello `Directory` list that appears, select hello Azure AD B2C tenant that you wish toomanage.</span></span>

<span data-ttu-id="b3722-110">Hello Azure Portal yenilenecektir.</span><span class="sxs-lookup"><span data-stu-id="b3722-110">hello Azure Portal will refresh.</span></span>  <span data-ttu-id="b3722-111">Şimdi hello Azure Portal, Azure AD B2C kiracısı hello bağlamında oturum açtınız.</span><span class="sxs-lookup"><span data-stu-id="b3722-111">Now you are signed into hello Azure Portal in hello context of your Azure AD B2C tenant.</span></span>

## <a name="navigate-toohello-b2c-features-blade"></a><span data-ttu-id="b3722-112">Toohello B2C özellikleri dikey penceresine gidin</span><span class="sxs-lookup"><span data-stu-id="b3722-112">Navigate toohello B2C features blade</span></span>

1. <span data-ttu-id="b3722-113">Tıklatın **Gözat** hello sol taraftaki gezinti çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="b3722-113">Click **Browse** on hello left hand navigation.</span></span>
1. <span data-ttu-id="b3722-114">Tıklatın **> daha fazla hizmet** arayın ve sonra `Azure AD B2C` hello sol gezinti bölmesindeki.</span><span class="sxs-lookup"><span data-stu-id="b3722-114">Click **> More services** and then search for `Azure AD B2C` in hello left navigation pane.</span></span>  <span data-ttu-id="b3722-115">(toopin tooyour sol Sabitle hello yıldız toohello sol Azure AD B2C'yi tıklatın)</span><span class="sxs-lookup"><span data-stu-id="b3722-115">(toopin tooyour left-hand Startboard, click hello star toohello left of Azure AD B2C)</span></span>
1. <span data-ttu-id="b3722-116">Tıklatın **Azure AD B2C** tooaccess hello B2C özellikleri dikey penceresi.</span><span class="sxs-lookup"><span data-stu-id="b3722-116">Click **Azure AD B2C** tooaccess hello B2C features blade.</span></span>
   
    ![Gözat tooB2C özellikleri dikey penceresi ekran görüntüsü](./media/active-directory-b2c-get-started/b2c-browse.png)

> [!IMPORTANT]
> <span data-ttu-id="b3722-118">Toobe hello B2C Kiracı toobe mümkün tooaccess hello B2C özellikleri dikey genel Yöneticisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3722-118">You need toobe a Global Administrator of hello B2C tenant toobe able tooaccess hello B2C features blade.</span></span> <span data-ttu-id="b3722-119">Başka bir kiracının Genel Yöneticisi veya başka bir kiracıdan gelen bir kullanıcı, dikey pencereye erişemez.</span><span class="sxs-lookup"><span data-stu-id="b3722-119">A Global Administrator from any other tenant or a user from any tenant cannot access it.</span></span>  <span data-ttu-id="b3722-120">Merhaba sağ üst köşesinde hello Azure portalı içinde hello Kiracı değiştirici kullanarak tooyour B2C Kiracı geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3722-120">You can switch tooyour B2C tenant by using hello tenant switcher in hello top right corner of hello Azure portal.</span></span>
