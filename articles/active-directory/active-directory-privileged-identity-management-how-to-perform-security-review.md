---
title: "Bir erişim incelemesi gerçekleştirme | Microsoft Docs"
description: "Azure Privileged Identity Management uygulaması ile incelemesi gerçekleştirme öğrenin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 49ee2feb-7d2e-4acf-82c1-40ff23062862
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: a98ed60221eeba1d9c92df846aeae2deafb8ae60
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-perform-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="fb6d4-103">Azure AD Privileged Identity Management erişim incelemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="fb6d4-103">How to perform an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="fb6d4-104">Azure Active Directory (AD) Privileged Identity Management, kuruluşların kaynaklarına Azure AD'de ve Office 365 veya Microsoft Intune gibi diğer Microsoft online services ayrıcalıklı erişimi nasıl yönetmek basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="fb6d4-105">Bir yönetici rolü atanmışsa, kuruluşunuzun ayrıcalıklı Rol Yöneticisi düzenli olarak bu rol hala işiniz için ihtiyacınız doğrulamanızı isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-105">If you are assigned to an administrative role, your organization's privileged role administrator may ask you to regularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="fb6d4-106">Bir bağlantı içeren bir e-posta alabilirsiniz veya doğrudan gidebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fb6d4-106">You might get an email that includes a link, or you can go straight to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fb6d4-107">Atanan rollerinizi Self gözden gerçekleştirmek için bu makaledeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-107">Follow the steps in this article to perform a self-review of your assigned roles.</span></span>

<span data-ttu-id="fb6d4-108">Erişim incelemeler ilgilenen bir ayrıcalıklı rol yöneticisi değilseniz, daha fazla bilgi almak [erişim incelemesi başlatma](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="fb6d4-108">If you're a privileged role administrator interested in access reviews, get more details at [How to start an access review](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="fb6d4-109">Privileged Identity Management uygulamasını ekleme</span><span class="sxs-lookup"><span data-stu-id="fb6d4-109">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="fb6d4-110">Azure AD Privileged Identity Management (PIM) uygulamasında kullanabileceğiniz [Azure portal](https://portal.azure.com/) incelemeniz gerçekleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-110">You can use the Azure AD Privileged Identity Management (PIM) application in the [Azure portal](https://portal.azure.com/) to perform your review.</span></span>  <span data-ttu-id="fb6d4-111">Azure AD Privileged Identity Management uygulaması portalınızda yoksa başlamak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-111">If you don't have the Azure AD Privileged Identity Management application on your portal, follow these steps to get started.</span></span>

1. <span data-ttu-id="fb6d4-112">[Azure Portal](https://portal.azure.com/) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-112">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fb6d4-113">Azure portalı ve burada şunları yapacaksınız, dizin seçin, sağ köşedeki kullanıcı adınıza işletim seçin.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-113">Select your username in the upper right-hand corner of the Azure portal, and select the directory where you will you be operating.</span></span>
3. <span data-ttu-id="fb6d4-114">**Daha fazla hizmet** seçeneğini belirleyin ve **Azure AD Privileged Identity Management** araması yapmak için Filtre metin kutusunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-114">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="fb6d4-115">**Panoya sabitle**'yi işaretleyin ve ardından **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-115">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="fb6d4-116">Privileged Identity Management uygulaması açılır.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-116">The Privileged Identity Management application will open.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="fb6d4-117">Onaylamak veya erişim engelle</span><span class="sxs-lookup"><span data-stu-id="fb6d4-117">Approve or deny access</span></span>
<span data-ttu-id="fb6d4-118">Onaylama ya da erişimini yalnızca İnceleme bu rolü veya kullanmaya devam olup olmadığını belirten.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-118">When you approve or deny access, you're just telling the reviewer whether you still use this role or not.</span></span> <span data-ttu-id="fb6d4-119">Seçin **Onayla** rolünde olmak istiyorsanız veya **reddetme** erişim artık ihtiyaç duymuyorsanız.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-119">Choose **Approve** if you want to stay in the role, or **Deny** if you don't need the access anymore.</span></span> <span data-ttu-id="fb6d4-120">İnceleme sonuçları geçerli olana kadar durumunuzu hemen değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-120">Your status won't change right away, until the reviewer applies the results.</span></span>
<span data-ttu-id="fb6d4-121">Bul ve erişim gözden geçirme tamamlamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="fb6d4-121">Follow these steps to find and complete the access review:</span></span>

1. <span data-ttu-id="fb6d4-122">PIM uygulamada seçin **gözden geçirme ayrıcalıklı erişim**.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-122">In the PIM application, select **Review privileged access**.</span></span> <span data-ttu-id="fb6d4-123">Tüm bekleyen erişim incelemeler varsa, bunlar Azure AD erişim incelemeler dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-123">If you have any pending access reviews, they appear in the Azure AD Access reviews blade.</span></span>
2. <span data-ttu-id="fb6d4-124">Tamamlamak için istediğiniz gözden geçirme seçin.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-124">Select the review you want to complete.</span></span>
3. <span data-ttu-id="fb6d4-125">Gözden geçirme oluşturduğunuz sürece, yalnızca kullanıcı gözden olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-125">Unless you created the review, you appear as the only user in the review.</span></span> <span data-ttu-id="fb6d4-126">Adınızın yanındaki onay işaretini seçin.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-126">Select the check mark next to your name.</span></span>
4. <span data-ttu-id="fb6d4-127">Ya da seçin **onaylama** veya **Reddet**.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-127">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="fb6d4-128">Kararınızı içinde nedeni eklemeniz gerekebilir **bir gerekçe sağlamasını** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-128">You may need to include a reason for your decision in the **Provide a reason** text box.</span></span>  
5. <span data-ttu-id="fb6d4-129">Kapat **gözden geçirme Azure AD rolleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="fb6d4-129">Close the **Review Azure AD roles** blade.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="fb6d4-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fb6d4-130">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
