---
title: "Etkinleştirmek veya bir rolü devre dışı bırakma | Microsoft Docs"
description: "Azure Privileged Identity Management uygulaması ile ayrıcalıklı kimlikleri için rol etkinleştirme konusunda bilgi edinin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1ce9e2e7-452b-4f66-9588-0d9cd2539e45
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: a143fd78eae52fda0cbadb7e74fd8209f24629a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-activate-or-deactivate-roles-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="2378d-103">Etkinleştirmek veya Azure AD Privileged Identity Management rollerinde devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="2378d-103">How to activate or deactivate roles in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="2378d-104">Azure Active Directory (AD) Privileged Identity Management, kuruluşların kaynaklarına Azure AD'de ve Office 365 veya Microsoft Intune gibi diğer Microsoft online services ayrıcalıklı erişimi nasıl yönetmek basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="2378d-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="2378d-105">Bir yönetici rolü için uygun yapılmışsa, ayrıcalıklı eylemler gerçekleştirmek gerektiğinde bu rol etkinleştirebilirsiniz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="2378d-105">If you have been made eligible for an administrative role, that means you can activate that role when you need to perform privileged actions.</span></span> <span data-ttu-id="2378d-106">Office 365 özellikleri bazen yönetiyorsanız, bu rolü diğer hizmetler çok etkiler Örneğin, kuruluşunuzun ayrıcalıklı rol Yöneticiler kalıcı genel yönetici kararı değil.</span><span class="sxs-lookup"><span data-stu-id="2378d-106">For example, if you occasionally manage Office 365 features, your organization's privileged role administrators may not make you a permanent Global Administrator, since that role impacts other services, too.</span></span> <span data-ttu-id="2378d-107">Bunun yerine, bunlar, Exchange Online yönetici gibi Azure AD rolleri için uygun yapın.</span><span class="sxs-lookup"><span data-stu-id="2378d-107">Instead, they make you eligible for Azure AD roles such as Exchange Online Administrator.</span></span> <span data-ttu-id="2378d-108">Bu rol, ayrıcalıklarına sahip olmanız gerekir ve ardından önceden belirlenmiş bir süre için yönetici denetim gerekir etkinleştirmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2378d-108">You can request to activate that role when you need its privileges, and then you'll have admin control for a predetermined time period.</span></span>

<span data-ttu-id="2378d-109">Bu makalede, Azure AD Privileged Identity Management (PIM) içindeki rollerine etkinleştirmek için gereken yöneticileri içindir.</span><span class="sxs-lookup"><span data-stu-id="2378d-109">This article is for admins who need to activate their role in Azure AD Privileged Identity Management (PIM).</span></span> <span data-ttu-id="2378d-110">Bu izinlere sahip olmanız gerekir ve tamamladığınızda rolünü devre dışı bir rolü etkinleştirmek için adımlarda size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="2378d-110">It walks you through the steps to activate a role when you need the permissions, and deactivate the role when you're done.</span></span> <span data-ttu-id="2378d-111">Ayrıca, ayrıcalıklı rol yöneticileri rolü (Önizleme) etkinleştirmek için onay gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="2378d-111">In addition, privileged role administrators can require approval to activate a role (Preview).</span></span> <span data-ttu-id="2378d-112">Daha fazla bilgi edinmek [PIM onay iş akışları](./privileged-identity-management/azure-ad-pim-approval-workflow.md) burada.</span><span class="sxs-lookup"><span data-stu-id="2378d-112">Learn more about [PIM Approval Workflows](./privileged-identity-management/azure-ad-pim-approval-workflow.md) here.</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="2378d-113">Privileged Identity Management uygulamasını ekleme</span><span class="sxs-lookup"><span data-stu-id="2378d-113">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="2378d-114">Azure AD Privileged Identity Management uygulamada kullanmak [Azure portal](https://portal.azure.com/) başka bir portal veya PowerShell çalışmasına olmaya olsa bile bir rol etkinleştirme istemek için.</span><span class="sxs-lookup"><span data-stu-id="2378d-114">Use the Azure AD Privileged Identity Management application in the [Azure portal](https://portal.azure.com/) to request a role activation, even if you're going to operate in another portal or PowerShell.</span></span> <span data-ttu-id="2378d-115">Azure Portal'da Azure AD Privileged Identity Management uygulaması yoksa, başlamak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="2378d-115">If you don't have the Azure AD Privileged Identity Management application on your Azure portal, follow these steps to get started.</span></span>

1. <span data-ttu-id="2378d-116">[Azure Portal](https://portal.azure.com/) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2378d-116">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2378d-117">Azure portalı ve burada şunları yapacaksınız, dizin seçin, sağ köşedeki kullanıcı adınıza işletim seçin.</span><span class="sxs-lookup"><span data-stu-id="2378d-117">Select your username in the upper right-hand corner of the Azure portal, and select the directory where you will you be operating.</span></span>
3. <span data-ttu-id="2378d-118">**Daha fazla hizmet** seçeneğini belirleyin ve **Azure AD Privileged Identity Management** araması yapmak için Filtre metin kutusunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="2378d-118">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="2378d-119">**Panoya sabitle**'yi işaretleyin ve ardından **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2378d-119">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="2378d-120">Privileged Identity Management uygulaması açılır.</span><span class="sxs-lookup"><span data-stu-id="2378d-120">The Privileged Identity Management application opens.</span></span>

## <a name="activate-a-role"></a><span data-ttu-id="2378d-121">Bir rolü etkinleştirmesi</span><span class="sxs-lookup"><span data-stu-id="2378d-121">Activate a role</span></span>
<span data-ttu-id="2378d-122">Bir rolü üstlenmesine gerektiğinde seçerek etkinleştirme isteyebilir **My rolleri** Azure AD Privileged Identity Management uygulaması Gezinti seçeneğinde sol gezinti sütun.</span><span class="sxs-lookup"><span data-stu-id="2378d-122">When you need to take on a role, you can request activation by selecting the **My Roles** navigation option in the Azure AD Privileged Identity Management application's left navigation column.</span></span>

1. <span data-ttu-id="2378d-123">Oturum [Azure portal](https://portal.azure.com/) ve Azure AD Privileged Identity Management kutucuk seçin.</span><span class="sxs-lookup"><span data-stu-id="2378d-123">Sign in to the [Azure portal](https://portal.azure.com/) and select the Azure AD Privileged Identity Management tile.</span></span>
2. <span data-ttu-id="2378d-124">Seçin **My rolleri**.</span><span class="sxs-lookup"><span data-stu-id="2378d-124">Select **My Roles**.</span></span> <span data-ttu-id="2378d-125">Sayfanın üst kısmındaki gruplandırmasında atanmış uygun rollerinizi listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2378d-125">A list of your assigned eligible roles appear in the grouping at the top of the page.</span></span>
3. <span data-ttu-id="2378d-126">Etkinleştirmek için bir rol seçin.</span><span class="sxs-lookup"><span data-stu-id="2378d-126">Select a role to activate.</span></span>
4. <span data-ttu-id="2378d-127">Seçin **etkinleştirme**.</span><span class="sxs-lookup"><span data-stu-id="2378d-127">Select **Activate**.</span></span> <span data-ttu-id="2378d-128">**Rol etkinleştirme isteği** dikey penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="2378d-128">The **Request role activation** blade appears.</span></span>
5. <span data-ttu-id="2378d-129">Bazı roller, rol etkinleştirilebilmesi için çok faktörlü kimlik doğrulama (MFA) gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2378d-129">Some roles require Multi-Factor Authentication (MFA) before you can activate the role.</span></span> <span data-ttu-id="2378d-130">Yalnızca bir kez oturum başına kimlik doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2378d-130">You only have to authenticate once per session.</span></span>
   
    ![MFA ile rol etkinleştirme - ekran görüntüsü önce doğrulayın][2]
6. <span data-ttu-id="2378d-132">Etkinleştirme isteğinin nedenini metin alanına girin.</span><span class="sxs-lookup"><span data-stu-id="2378d-132">Enter the reason for the activation request in the text field.</span></span>  <span data-ttu-id="2378d-133">Bazı roller, sorun bileti numarası girmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2378d-133">Some roles require you to supply a trouble ticket number.</span></span>
7. <span data-ttu-id="2378d-134">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="2378d-134">Select **OK**.</span></span>  <span data-ttu-id="2378d-135">Rol onay gerektirmiyorsa, şimdi etkinleştirilir ve rol (doğrudan listesinin altındaki uygun rol atamalarını) etkin rollerinin listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2378d-135">If the role does not require approval, it is now activated, and the role appears in the list of active roles (directly below the list of eligible role assignments).</span></span> <span data-ttu-id="2378d-136">Varsa [rolünü onay gerektiren](./privileged-identity-management/azure-ad-pim-approval-workflow.md) etkinleştirmek için bildirim kısaca isteğidir onay bekleyen bildiren tarayıcınızın sağ üst köşesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2378d-136">If the [role requires approval](./privileged-identity-management/azure-ad-pim-approval-workflow.md) to activate, a toast notification will briefly appear in the upper right-hand corner of your browser informing you the request is pending approval.</span></span>

    ![Bildirim - ekran görüntüsü istek][3]

## <a name="deactivate-a-role"></a><span data-ttu-id="2378d-138">Bir rolü devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="2378d-138">Deactivate a role</span></span>
<span data-ttu-id="2378d-139">Bir rolü etkinleştirildikten sonra süresi sınırına (uygun süresi) ulaşıldığında otomatik olarak devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="2378d-139">Once a role has been activated, it automatically deactivates when its time limit (eligible duration) is reached.</span></span>

<span data-ttu-id="2378d-140">Yönetim görevlerinizi erken tamamlarsanız, bir rolde el ile Azure AD Privileged Identity Management uygulaması devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2378d-140">If you complete your admin tasks early, you can also deactivate a role manually in the Azure AD Privileged Identity Management application.</span></span>  <span data-ttu-id="2378d-141">Seçin **My rolleri**, tamamladıktan rolünü seçin gelen kullanarak **etkin rol atamalarını** gruplandırma ve select **devre dışı bırak**.</span><span class="sxs-lookup"><span data-stu-id="2378d-141">Select **My Roles**, choose the role you're done using from the **Active role assignments** grouping, and select **Deactivate**.</span></span>  

## <a name="cancel-a-pending-request"></a><span data-ttu-id="2378d-142">Bekleyen isteği iptal et</span><span class="sxs-lookup"><span data-stu-id="2378d-142">Cancel a pending request</span></span>
<span data-ttu-id="2378d-143">Onay gerektiren bir rolü etkinleştirmesi gerektirmeyen durumunda herhangi bir zamanda bekleyen isteği iptal edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2378d-143">In the event you do not require activation of a role that requires approval, you may cancel a pending request at any time.</span></span> <span data-ttu-id="2378d-144">Yalnızca select **My rolleri** Azure AD Privileged Identity Management uygulaması Gezinti seçeneğinde sol gezinti sütun.</span><span class="sxs-lookup"><span data-stu-id="2378d-144">Simply select the **My Roles** navigation option in the Azure AD Privileged Identity Management application's left navigation column.</span></span>

1. <span data-ttu-id="2378d-145">Oturum [Azure portal](https://portal.azure.com/) ve Azure AD Privileged Identity Management kutucuk seçin.</span><span class="sxs-lookup"><span data-stu-id="2378d-145">Sign in to the [Azure portal](https://portal.azure.com/) and select the Azure AD Privileged Identity Management tile.</span></span>
2. <span data-ttu-id="2378d-146">Seçin **My rolleri**.</span><span class="sxs-lookup"><span data-stu-id="2378d-146">Select **My Roles**.</span></span> <span data-ttu-id="2378d-147">Sayfanın üst kısmındaki gruplandırmasında atanmış uygun rollerinizi listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2378d-147">A list of your assigned eligible roles appear in the grouping at the top of the page.</span></span>
3. <span data-ttu-id="2378d-148">Bir rol seçin.</span><span class="sxs-lookup"><span data-stu-id="2378d-148">Select a role.</span></span>
4. <span data-ttu-id="2378d-149">Seçin **etkinleştirme durumda onay bekleyen** rol etkinleştirme ayrıntıları dikey penceresinde başlık.</span><span class="sxs-lookup"><span data-stu-id="2378d-149">Select the **Activation is pending approval** banner on the role activation details blade.</span></span>
5. <span data-ttu-id="2378d-150">Seçin **iptal** en üstündeki **onay bekleyen** dikey.</span><span class="sxs-lookup"><span data-stu-id="2378d-150">Select **Cancel** at the top of the **Pending approval** blade.</span></span>

   ![Bekleyen isteği ekran iptal et][4]

## <a name="next-steps"></a><span data-ttu-id="2378d-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2378d-152">Next steps</span></span>
<span data-ttu-id="2378d-153">Azure AD Privileged Identity Management hakkında daha fazla bilgi edinmek isterseniz, aşağıdaki bağlantılardan daha fazla bilgi sahip.</span><span class="sxs-lookup"><span data-stu-id="2378d-153">If you're interested in learning more about Azure AD Privileged Identity Management, the following links have more information.</span></span>

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_activation_MFA.png
[3]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Toast2.png
[4]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Banner_Cancel.png
