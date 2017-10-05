---
title: "Azure MFA için lisans atama | Microsoft Docs"
description: "Microsoft Azure Multi-Factor Authentication için kullanıcı lisansları atama hakkında bilgi edinin."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 514ef423-8ee6-4987-8a4e-80d5dc394cf9
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/13/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ROBOTS: NOINDEX
ms.openlocfilehash: 45522bf526c4aeab1d6ccc8891a55a0436ff9320
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="assigning-an-azure-mfa-azure-ad-premium-or-enterprise-mobility-license-to-users"></a><span data-ttu-id="22567-103">Kullanıcılara Azure MFA, Azure AD Premium veya Enterprise Mobility lisansı atama</span><span class="sxs-lookup"><span data-stu-id="22567-103">Assigning an Azure MFA, Azure AD Premium, or Enterprise Mobility license to users</span></span>
<span data-ttu-id="22567-104">Azure MFA, Azure AD Premium veya Enterprise Mobility Suite lisansları satın aldıysanız Multi-Factor Auth sağlayıcısı oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="22567-104">If you have purchased Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses, you do not need to create a Multi-Factor Auth provider.</span></span> <span data-ttu-id="22567-105">Kullanıcılarınıza lisansları atadıktan sonra, kullanıcılarınızı MFA için etkinleştirmeye başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22567-105">Once you assign the licenses to your users, you can begin enabling them for MFA.</span></span>

## <a name="to-assign-a-license"></a><span data-ttu-id="22567-106">Lisans atamak için</span><span class="sxs-lookup"><span data-stu-id="22567-106">To assign a license</span></span>
1. <span data-ttu-id="22567-107">[Klasik Azure portalında](https://manage.windowsazure.com) yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="22567-107">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator.</span></span>
2. <span data-ttu-id="22567-108">Sol taraftaki **Active Directory** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="22567-108">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="22567-109">Active Directory sayfasında, etkinleştirmek istediğiniz kullanıcıları içeren dizine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="22567-109">On the Active Directory page, double-click the directory that has the users you wish to enable.</span></span>
4. <span data-ttu-id="22567-110">Dizin sayfasının en üst kısmındaki **Lisanslar** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="22567-110">At the top of the directory page, select **Licenses**.</span></span>
   <span data-ttu-id="22567-111">![Lisansları Atama](./media/multi-factor-authentication-get-started-assign-licenses/assign1.png)</span><span class="sxs-lookup"><span data-stu-id="22567-111">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign1.png)</span></span>
5. <span data-ttu-id="22567-112">Lisanslar sayfasında **Azure Multi-Factor Authentication**, **Active Directory Premium** veya **Enterprise Mobility Suite** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="22567-112">On the Licenses page, select **Azure Multi-Factor Authentication**, **Active Directory Premium**, or **Enterprise Mobility Suite**.</span></span>  <span data-ttu-id="22567-113">Yalnızca bir lisansınız varsa otomatik olarak seçilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="22567-113">If you only have one, then it should be selected automatically.</span></span>
6. <span data-ttu-id="22567-114">Sayfanın alt kısmındaki **Ata**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="22567-114">At the bottom of the page, click **Assign**.</span></span>
   <span data-ttu-id="22567-115">![Lisansları Atama](./media/multi-factor-authentication-get-started-assign-licenses/assign3.png)</span><span class="sxs-lookup"><span data-stu-id="22567-115">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign3.png)</span></span>
7. <span data-ttu-id="22567-116">Açılan kutuda lisans atamak istediğiniz kullanıcıların veya grupların yanına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="22567-116">In the box that comes up, click next to the users or groups you want to assign licenses to.</span></span>  <span data-ttu-id="22567-117">Yeşil bir onay işareti görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="22567-117">You should see a green check mark appear.</span></span>
8. <span data-ttu-id="22567-118">Değişiklikleri kaydetmek için onay işareti simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="22567-118">Click the check mark icon to save the changes.</span></span>
   <span data-ttu-id="22567-119">![Lisansları Atama](./media/multi-factor-authentication-get-started-assign-licenses/assign4.png)</span><span class="sxs-lookup"><span data-stu-id="22567-119">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign4.png)</span></span>
9. <span data-ttu-id="22567-120">Kaç tane lisansın atandığını ve kaç tanesinin başarısız olduğunu belirten bir ileti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="22567-120">You should see a message saying how many licenses were assigned and how many may have failed.</span></span>  <span data-ttu-id="22567-121">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="22567-121">Click **Ok**.</span></span>
   <span data-ttu-id="22567-122">![Lisansları Atama](./media/multi-factor-authentication-get-started-assign-licenses/assign5.png)</span><span class="sxs-lookup"><span data-stu-id="22567-122">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign5.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="22567-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="22567-123">Next steps</span></span>

- <span data-ttu-id="22567-124">Daha fazla bilgi için bkz. [Microsoft Azure Active Directory lisansı nedir?](../active-directory/active-directory-licensing-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="22567-124">For more information, see [What is Microsoft Azure Active Directory licensing?](../active-directory/active-directory-licensing-what-is.md)</span></span>
