---
title: "Azure Active Directory B2C: B2C kiracısına geçiş | Microsoft Belgeleri"
description: "Active Directory B2C kiracınızın bağlamına geçiş yapma"
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
ms.openlocfilehash: 40d8d57d974a949fbdc0a06eeceb2d06bfbaa09f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="switching-to-your-azure-ad-b2c-tenant"></a><span data-ttu-id="24207-103">Azure AD B2C kiracınıza geçiş yapma</span><span class="sxs-lookup"><span data-stu-id="24207-103">Switching to your Azure AD B2C tenant</span></span>

<span data-ttu-id="24207-104">Azure AD B2C’yi yapılandırmak için Azure AD B2C kiracınızın bağlamında olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="24207-104">In order to configure Azure AD B2C, you need to be in the context of your Azure AD B2C tenant.</span></span>

## <a name="log-into-azure-ad-b2c-tenant"></a><span data-ttu-id="24207-105">Azure AD B2C kiracınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="24207-105">Log into Azure AD B2C tenant</span></span>

<span data-ttu-id="24207-106">Azure AD B2C kiracınıza gitmek için Azure portalında Azure AD B2C kiracısının genel yöneticisi olarak oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="24207-106">To navigate to your Azure AD B2C tenant, you must be logged into the Azure portal as a global administrator of the Azure AD B2C tenant.</span></span>

1. <span data-ttu-id="24207-107">[Azure portal](http://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="24207-107">Sign into the [Azure portal](http://portal.azure.com).</span></span>
1. <span data-ttu-id="24207-108">E-posta adresinize veya sağ üst köşedeki resme tıklayarak kiracılar arasında geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24207-108">Switch tenants by clicking your email address or picture in the top-right corner.</span></span>
1. <span data-ttu-id="24207-109">Görünecek `Directory` listesinden, yönetmek istediğiniz Azure AD B2C kiracısını seçin.</span><span class="sxs-lookup"><span data-stu-id="24207-109">In the `Directory` list that appears, select the Azure AD B2C tenant that you wish to manage.</span></span>

<span data-ttu-id="24207-110">Azure Portal yenilenir.</span><span class="sxs-lookup"><span data-stu-id="24207-110">The Azure Portal will refresh.</span></span>  <span data-ttu-id="24207-111">Azure Portal'da Azure AD B2C kiracınızın bağlamında oturum açmış olursunuz.</span><span class="sxs-lookup"><span data-stu-id="24207-111">Now you are signed into the Azure Portal in the context of your Azure AD B2C tenant.</span></span>

## <a name="navigate-to-the-b2c-features-blade"></a><span data-ttu-id="24207-112">B2C özellikleri dikey penceresine gitme</span><span class="sxs-lookup"><span data-stu-id="24207-112">Navigate to the B2C features blade</span></span>

1. <span data-ttu-id="24207-113">Gezinti bölmesinin sol tarafındaki **Gözat** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="24207-113">Click **Browse** on the left hand navigation.</span></span>
1. <span data-ttu-id="24207-114">**> Daha fazla hizmet**’e tıklayın ve sol gezinti bölmesinde `Azure AD B2C` seçeneğini bulun.</span><span class="sxs-lookup"><span data-stu-id="24207-114">Click **> More services** and then search for `Azure AD B2C` in the left navigation pane.</span></span>  <span data-ttu-id="24207-115">(Sol taraftaki başlangıç panonuza sabitlemek için Azure AD B2C’nin solundaki yıldıza tıklayın)</span><span class="sxs-lookup"><span data-stu-id="24207-115">(To pin to your left-hand Startboard, click the star to the left of Azure AD B2C)</span></span>
1. <span data-ttu-id="24207-116">B2C özellikleri dikey penceresine erişmek için **Azure AD B2C** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="24207-116">Click **Azure AD B2C** to access the B2C features blade.</span></span>
   
    ![B2C özelliklerine göz atma dikey penceresi ekran görüntüsü](./media/active-directory-b2c-get-started/b2c-browse.png)

> [!IMPORTANT]
> <span data-ttu-id="24207-118">B2C özellikleri dikey penceresine erişebilmek için B2C kiracısının Genel Yöneticisi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="24207-118">You need to be a Global Administrator of the B2C tenant to be able to access the B2C features blade.</span></span> <span data-ttu-id="24207-119">Başka bir kiracının Genel Yöneticisi veya başka bir kiracıdan gelen bir kullanıcı, dikey pencereye erişemez.</span><span class="sxs-lookup"><span data-stu-id="24207-119">A Global Administrator from any other tenant or a user from any tenant cannot access it.</span></span>  <span data-ttu-id="24207-120">Azure portalının sağ üst köşesindeki kiracı değiştiriciyi kullanarak B2C kiracınıza geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24207-120">You can switch to your B2C tenant by using the tenant switcher in the top right corner of the Azure portal.</span></span>
