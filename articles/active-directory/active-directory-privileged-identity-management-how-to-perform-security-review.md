---
title: "aaaHow tooperform erişim gözden geçirme | Microsoft Docs"
description: "Nasıl bir gözden geçirme ile tooperform hello Azure Privileged Identity Management uygulaması hakkında bilgi edinin."
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
ms.openlocfilehash: 301a5e9f97b68fedfbf4954e0bd7dadb7f0fc510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="9c1b9-103">Nasıl tooperform access gözden Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="9c1b9-103">How tooperform an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="9c1b9-104">Azure Active Directory (AD) Privileged Identity Management, ayrıcalıklı erişim tooresources Azure AD'de ve Office 365 veya Microsoft Intune gibi diğer Microsoft online services kuruluşların nasıl yönettiğini basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="9c1b9-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access tooresources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="9c1b9-105">Tooan Yönetici rolü atanmışsa, kuruluşunuzun ayrıcalıklı Rol Yöneticisi isteyebilir tooregularly onaylayın bu rol hala işiniz için gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c1b9-105">If you are assigned tooan administrative role, your organization's privileged role administrator may ask you tooregularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="9c1b9-106">Bir bağlantı içeren bir e-posta alabilirsiniz veya düz toohello gidebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9c1b9-106">You might get an email that includes a link, or you can go straight toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9c1b9-107">Bu makale tooperform atanan rollerinizi Self gözden Hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="9c1b9-107">Follow hello steps in this article tooperform a self-review of your assigned roles.</span></span>

<span data-ttu-id="9c1b9-108">Erişim incelemeler ilgilenen bir ayrıcalıklı rol yöneticisi değilseniz, daha fazla bilgi almak [toostart erişimini nasıl gözden](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="9c1b9-108">If you're a privileged role administrator interested in access reviews, get more details at [How toostart an access review](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="add-hello-privileged-identity-management-application"></a><span data-ttu-id="9c1b9-109">Merhaba Privileged Identity Management uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="9c1b9-109">Add hello Privileged Identity Management application</span></span>
<span data-ttu-id="9c1b9-110">Merhaba Azure AD Privileged Identity Management (PIM) uygulaması hello kullanabilirsiniz [Azure portal](https://portal.azure.com/) tooperform gözden geçirilecek.</span><span class="sxs-lookup"><span data-stu-id="9c1b9-110">You can use hello Azure AD Privileged Identity Management (PIM) application in hello [Azure portal](https://portal.azure.com/) tooperform your review.</span></span>  <span data-ttu-id="9c1b9-111">Portalınızda hello Azure AD Privileged Identity Management uygulaması yoksa, bu adımları tooget başlatılan izleyin.</span><span class="sxs-lookup"><span data-stu-id="9c1b9-111">If you don't have hello Azure AD Privileged Identity Management application on your portal, follow these steps tooget started.</span></span>

1. <span data-ttu-id="9c1b9-112">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9c1b9-112">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9c1b9-113">Kullanıcı adınıza hello sağ üst köşesinde hello Azure portal ve burada şunları yapacaksınız, select hello dizin işletim seçin.</span><span class="sxs-lookup"><span data-stu-id="9c1b9-113">Select your username in hello upper right-hand corner of hello Azure portal, and select hello directory where you will you be operating.</span></span>
3. <span data-ttu-id="9c1b9-114">Seçin **daha fazla hizmet** ve hello filtre textbox toosearch **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="9c1b9-114">Select **More services** and use hello Filter textbox toosearch for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="9c1b9-115">Denetleme **PIN toodashboard** ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="9c1b9-115">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="9c1b9-116">Merhaba Privileged Identity Management uygulaması açılır.</span><span class="sxs-lookup"><span data-stu-id="9c1b9-116">hello Privileged Identity Management application will open.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="9c1b9-117">Onaylamak veya erişim engelle</span><span class="sxs-lookup"><span data-stu-id="9c1b9-117">Approve or deny access</span></span>
<span data-ttu-id="9c1b9-118">Onaylama ya da erişimini yalnızca hello İnceleme bu rolü veya kullanmaya devam olup olmadığını belirten.</span><span class="sxs-lookup"><span data-stu-id="9c1b9-118">When you approve or deny access, you're just telling hello reviewer whether you still use this role or not.</span></span> <span data-ttu-id="9c1b9-119">Seçin **Onayla** toostay hello rolündeki istiyorsanız veya **reddetme** erişim artık hello yoktur.</span><span class="sxs-lookup"><span data-stu-id="9c1b9-119">Choose **Approve** if you want toostay in hello role, or **Deny** if you don't need hello access anymore.</span></span> <span data-ttu-id="9c1b9-120">Merhaba İnceleme hello sonuçları geçerli olana kadar durumunuzu hemen değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="9c1b9-120">Your status won't change right away, until hello reviewer applies hello results.</span></span>
<span data-ttu-id="9c1b9-121">Bu adımları toofind izleyin ve hello erişim gözden geçirme tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="9c1b9-121">Follow these steps toofind and complete hello access review:</span></span>

1. <span data-ttu-id="9c1b9-122">Hello PIM uygulama, seçin **gözden geçirme ayrıcalıklı erişim**.</span><span class="sxs-lookup"><span data-stu-id="9c1b9-122">In hello PIM application, select **Review privileged access**.</span></span> <span data-ttu-id="9c1b9-123">Tüm bekleyen erişim incelemeler varsa, Azure AD erişim dikey incelemeleri hello görünür.</span><span class="sxs-lookup"><span data-stu-id="9c1b9-123">If you have any pending access reviews, they appear in hello Azure AD Access reviews blade.</span></span>
2. <span data-ttu-id="9c1b9-124">Merhaba gözden toocomplete istediğiniz seçin.</span><span class="sxs-lookup"><span data-stu-id="9c1b9-124">Select hello review you want toocomplete.</span></span>
3. <span data-ttu-id="9c1b9-125">Merhaba gözden geçirme oluşturduğunuz sürece, yalnızca hello gözden geçirme kullanıcı hello gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="9c1b9-125">Unless you created hello review, you appear as hello only user in hello review.</span></span> <span data-ttu-id="9c1b9-126">Merhaba onay işareti sonraki tooyour adını seçin.</span><span class="sxs-lookup"><span data-stu-id="9c1b9-126">Select hello check mark next tooyour name.</span></span>
4. <span data-ttu-id="9c1b9-127">Ya da seçin **onaylama** veya **Reddet**.</span><span class="sxs-lookup"><span data-stu-id="9c1b9-127">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="9c1b9-128">Tooinclude kararınızı hello içinde nedeni gerekebilir **bir gerekçe sağlamasını** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="9c1b9-128">You may need tooinclude a reason for your decision in hello **Provide a reason** text box.</span></span>  
5. <span data-ttu-id="9c1b9-129">Kapat hello **gözden geçirme Azure AD rolleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="9c1b9-129">Close hello **Review Azure AD roles** blade.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="9c1b9-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9c1b9-130">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
