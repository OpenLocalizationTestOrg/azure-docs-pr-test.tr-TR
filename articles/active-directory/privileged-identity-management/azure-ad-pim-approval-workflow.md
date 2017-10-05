---
title: "Azure Privileged Identity Management onay iş akışları | Microsoft Docs"
description: "Onay iş akışları ayrıcalıklı Kimlik Yönetimi'nın (PIM) hakkında bilgi edinin"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: cf6a9213fa0a1cba8725aabb42abe51b805ece7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="approvals-preview"></a><span data-ttu-id="a495f-103">Onaylar (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="a495f-103">Approvals (Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="a495f-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="a495f-104">Overview</span></span>

<span data-ttu-id="a495f-105">Privileged Identity Management için onayları sayesinde, etkinleştirme için onay gerektirmesini rollerini yapılandırın ve bir veya birden çok kullanıcı veya grup temsilci onaylayanlar olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="a495f-105">With Approvals for Privileged Identity Management, you can configure roles to require approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="a495f-106">Rollerini yapılandırın ve onaylayanlar seçin öğrenmek için okuma tutun.</span><span class="sxs-lookup"><span data-stu-id="a495f-106">Keep reading to learn how to configure roles and select approvers.</span></span>

>[!NOTE]
<span data-ttu-id="a495f-107">Lütfen bu özelliği geliştirilme aşamasındadır göz önünde bulundurun ve hatalar karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a495f-107">Please keep in mind this feature is still in development, and you may encounter bugs.</span></span> <span data-ttu-id="a495f-108">İşlevselliği metin dahil ve adlandırma kuralları değiştirilebilir ve son düşünülmemelidir.</span><span class="sxs-lookup"><span data-stu-id="a495f-108">The functionality, including text and naming conventions are subject to change, and should not be considered final.</span></span>


## <a name="key-terminology"></a><span data-ttu-id="a495f-109">Anahtar terminolojisi</span><span class="sxs-lookup"><span data-stu-id="a495f-109">Key Terminology</span></span>

<span data-ttu-id="a495f-110">*Uygun rol kullanıcı* – kuruluşunuzdaki uygun olarak bir Azure AD rolüne atanmış bir kullanıcı bir uygun rol olduğu (Rol etkinleştirmesi gerekir).</span><span class="sxs-lookup"><span data-stu-id="a495f-110">*Eligible Role User* – An eligible role user is a user within your organization that’s been assigned to an Azure AD role as eligible (role requires activation).</span></span>

<span data-ttu-id="a495f-111">*Onaylayan temsilci* – bir temsilci onaylayan bir veya birden çok kişiler rol etkinleştirme isteklerini onaylama için sorumlu olan grupları, Azure AD içinde mi.</span><span class="sxs-lookup"><span data-stu-id="a495f-111">*Delegated Approver* – A delegated approver is one or multiple individuals or groups within your Azure AD who are responsible for approving requests for role activation.</span></span>

## <a name="scenarios"></a><span data-ttu-id="a495f-112">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="a495f-112">Scenarios</span></span>

<span data-ttu-id="a495f-113">Özel önizleme aşağıdaki senaryoları destekler:</span><span class="sxs-lookup"><span data-stu-id="a495f-113">The private preview supports the following scenarios:</span></span>

<span data-ttu-id="a495f-114">**Bir ayrıcalıklı Rol Yöneticisi (PRA) olarak şunları yapabilirsiniz:**</span><span class="sxs-lookup"><span data-stu-id="a495f-114">**As a Privileged Role Administrator (PRA) you can:**</span></span>

-   [<span data-ttu-id="a495f-115">belirli roller onayını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a495f-115">enable approval for specific roles</span></span>](#enable-approval-for-specific-roles)

-   [<span data-ttu-id="a495f-116">Onaylayan kullanıcılara ve/veya grupları istekleri onaylanacak belirtin</span><span class="sxs-lookup"><span data-stu-id="a495f-116">specify approver users and/or groups to approve requests</span></span>](#specify-approver-users-and/or-groups-to-approve-requests)

-   [<span data-ttu-id="a495f-117">tüm ayrıcalıklı rolleri için istek ve onay geçmişini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="a495f-117">view request and approval history for all privileged roles</span></span>](#view-request-and-approval-history-for-all-privileged-roles)

<span data-ttu-id="a495f-118">**Belirlenen onaylayıcı olarak, şunları yapabilirsiniz:**</span><span class="sxs-lookup"><span data-stu-id="a495f-118">**As a designated approver, you can:**</span></span>

-   [<span data-ttu-id="a495f-119">Bekleyen onaylar (istek) görüntüleme</span><span class="sxs-lookup"><span data-stu-id="a495f-119">view pending approvals (requests)</span></span>](#view-pending-approvals-requests)

-   [<span data-ttu-id="a495f-120">onaylama veya reddetme rol yükseltme (tek ve/veya toplu) istekleri</span><span class="sxs-lookup"><span data-stu-id="a495f-120">approve or reject requests for role elevation (single and/or bulk)</span></span>](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [<span data-ttu-id="a495f-121">my onay/reddetme için gerekçe</span><span class="sxs-lookup"><span data-stu-id="a495f-121">provide justification for my approval/rejection</span></span>](#provide-justification-for-my-approval/rejection) 

<span data-ttu-id="a495f-122">**Uygun bir Role kullanıcı olarak şunları yapabilirsiniz:**</span><span class="sxs-lookup"><span data-stu-id="a495f-122">**As an Eligible Role User you can:**</span></span>

-   [<span data-ttu-id="a495f-123">onay gerektiren bir rolü etkinleştirme isteği</span><span class="sxs-lookup"><span data-stu-id="a495f-123">request activation of a role that requires approval</span></span>](#request-activation-of-a-role-that-requires-approval)

-   [<span data-ttu-id="a495f-124">İsteğiniz etkinleştirme durumunu görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="a495f-124">view the status of your request to activate</span></span>](#view-the-status-of-your-request-to-activate)

-   [<span data-ttu-id="a495f-125">etkinleştirme onaylanırsa Azure AD'de Görevinizi tamamlamak</span><span class="sxs-lookup"><span data-stu-id="a495f-125">complete your task in Azure AD if activation was approved</span></span>](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a><span data-ttu-id="a495f-126">Gezinme</span><span class="sxs-lookup"><span data-stu-id="a495f-126">Navigation</span></span>

<span data-ttu-id="a495f-127">Biz onayları desteklemek için Gezinti güncelleştirdik</span><span class="sxs-lookup"><span data-stu-id="a495f-127">We've updated the navigation to support approvals</span></span>

![](media/azure-ad-pim-approval-workflow/image001.png)

<span data-ttu-id="a495f-128">Giriş sayfasında varsayılan PIM ve yeni onayları belgeleri hakkında bilgi için uygun erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="a495f-128">The default landing page provides convenient access to information about PIM and the new approvals documentation.</span></span>

![](media/azure-ad-pim-approval-workflow/image002.png)

<span data-ttu-id="a495f-129">PIM, 'My denetim Geçmişi' tüm kullanıcılar için yeni bir bölüm de ekledik.</span><span class="sxs-lookup"><span data-stu-id="a495f-129">We’ve also added a new section for all users of PIM, ‘My Audit History’.</span></span> <span data-ttu-id="a495f-130">Burada tüm bilgileri kimliğinizi ilgili bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a495f-130">Here you can find all the information relevant to your identity.</span></span> <span data-ttu-id="a495f-131">Bu seçenek, tüm bekleyen ve tamamlanmış istekleri, çözümlemeniz istekleri hakkında yaptığınız kararları ve tüm son rol etkinleştirme tek bir konumda içerir.</span><span class="sxs-lookup"><span data-stu-id="a495f-131">This includes all your pending and completed requests, any decisions you’ve made about the requests you resolve, and all your past role activations in one convenient location.</span></span>

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a><span data-ttu-id="a495f-132">Belirli roller onayını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a495f-132">Enable approval for specific roles</span></span>

<span data-ttu-id="a495f-133">Belirli bir rol için onay etkinleştirmek için önce sol gezinti bölmesinden Directory rolleri seçin.</span><span class="sxs-lookup"><span data-stu-id="a495f-133">To enable approval for a specific role, first select Directory Roles from the left navigation.</span></span>

![](media/azure-ad-pim-approval-workflow/image004.png)

<span data-ttu-id="a495f-134">Bulma ve Dizin rolleri sol gezinti bölmesinde ayarlarını seçin</span><span class="sxs-lookup"><span data-stu-id="a495f-134">Find and select settings in the Directory Roles left navigation</span></span>

![](media/azure-ad-pim-approval-workflow/image006.png)

<span data-ttu-id="a495f-135">Ayrıcalıklı rolleri seçin:</span><span class="sxs-lookup"><span data-stu-id="a495f-135">Select privileged Roles:</span></span>

![](media/azure-ad-pim-approval-workflow/image009.png)

<span data-ttu-id="a495f-136">Seçin "Etkinleştir" onay bölümüne gerektirir:</span><span class="sxs-lookup"><span data-stu-id="a495f-136">Select “Enable” in the Require approval section:</span></span>

![](media/azure-ad-pim-approval-workflow/image011.png)

<span data-ttu-id="a495f-137">Bir kez etkinleştirildikten sonra dikey aşağıdaki ayrıntıları gösterecek şekilde genişletir:</span><span class="sxs-lookup"><span data-stu-id="a495f-137">Once enabled, the blade will expand to show the following details:</span></span>

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
<span data-ttu-id="a495f-138">VERMEYİN herhangi onaylayanlar belirtirseniz, PRA(s) varsayılan approver(s) haline gelir.</span><span class="sxs-lookup"><span data-stu-id="a495f-138">If you DO NOT specify any approvers, the PRA(s) become the default approver(s).</span></span> <span data-ttu-id="a495f-139">PRA(s) Bu rol için tüm etkinleştirme isteklerinin onaylanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a495f-139">PRA(s) would be required to approve ALL activation requests for this role.</span></span>

### <a name="specify-approver-users-andor-groups-to-approve-requests"></a><span data-ttu-id="a495f-140">Onaylayan kullanıcılara ve/veya grupları istekleri onaylanacak belirtin</span><span class="sxs-lookup"><span data-stu-id="a495f-140">Specify approver users and/or groups to approve requests</span></span>

<span data-ttu-id="a495f-141">Onay temsilci seçmek için "Select onaylayanlar" seçeneğine tıklayın:</span><span class="sxs-lookup"><span data-stu-id="a495f-141">To delegate approval, click the option to “Select approvers”:</span></span>

![](media/azure-ad-pim-approval-workflow/image015.png)

<span data-ttu-id="a495f-142">Select onaylayanlar dikey yüklediğinde, belirli bir kullanıcı veya üstünde arama çubuğunu kullanarak veya önceden doldurulmuş haldedir listeden seçerek grubu arayın ve sonra "bittiğinde," Seç:</span><span class="sxs-lookup"><span data-stu-id="a495f-142">When the Select approvers blade loads, you may search for a specific user or group using the search bar at the top, or selecting from the pre-populated list, then click “Select” when finished:</span></span>

![](media/azure-ad-pim-approval-workflow/image017.png)

<span data-ttu-id="a495f-143">Not: Bir defada birden çok kullanıcı veya grup seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a495f-143">Note: You may select multiple users or groups at a time.</span></span>

<span data-ttu-id="a495f-144">Seçiminiz seçili onaylayanlar listesinde aşağıda görüldüğü gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="a495f-144">Your selection will appear in the list of selected approvers as seen below:</span></span>

![](media/azure-ad-pim-approval-workflow/image019.png)

<span data-ttu-id="a495f-145">Onaylayıcı kaldırmak için Kaldır düğmesini adının yanındaki kutuyu tıklamanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="a495f-145">To remove an approver, simply click the Remove button next to their name.</span></span>

<span data-ttu-id="a495f-146">Ek onaylayanlar eklemek için işlemi yineleyin.</span><span class="sxs-lookup"><span data-stu-id="a495f-146">To add additional approvers, repeat the process.</span></span>

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a><span data-ttu-id="a495f-147">Tüm ayrıcalıklı rolleri için istek ve onay geçmişini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="a495f-147">View request and approval history for all privileged roles</span></span>

<span data-ttu-id="a495f-148">Tüm ayrıcalıklı rolleri istek ve onay geçmişini görüntülemek için panodan denetim geçmişi seçin:</span><span class="sxs-lookup"><span data-stu-id="a495f-148">To view request and approval history for all privileged roles, select Audit History from the dashboard:</span></span>

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
<span data-ttu-id="a495f-149">Eyleme göre verileri sıralamak ve "Etkinleştirme onaylanmış" bakın</span><span class="sxs-lookup"><span data-stu-id="a495f-149">You can sort the data by Action, and look for “Activation Approved”</span></span>

### <a name="view-pending-approvals-requests"></a><span data-ttu-id="a495f-150">Bekleyen onaylar (istek) görüntüleme</span><span class="sxs-lookup"><span data-stu-id="a495f-150">View pending approvals (requests)</span></span>

<span data-ttu-id="a495f-151">Onayınızı bekleyen istek olduğunda, bir temsilci onaylayan e-posta bildirimleri alırsınız.</span><span class="sxs-lookup"><span data-stu-id="a495f-151">As a delegated approver, you’ll receive email notifications when a request is pending your approval.</span></span> <span data-ttu-id="a495f-152">PIM Portalı'nda bu istekleri görüntülemek için Panoda (Yeni Gezinti) "Beklemedeki onay istekleri" sekmesini sol gezinti çubuğunda seçin.</span><span class="sxs-lookup"><span data-stu-id="a495f-152">To view these requests in the PIM portal, from the dashboard (in the new navigation) select the “Pending Approval Requests” tab in the left navigation bar.</span></span>

![](media/azure-ad-pim-approval-workflow/image023.png)

<span data-ttu-id="a495f-153">Burada, onay bekleyen isteklerin listesini görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="a495f-153">From there, you’ll see a list of requests pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a><span data-ttu-id="a495f-154">Onaylama veya reddetme rol yükseltme (tek ve/veya toplu) istekleri</span><span class="sxs-lookup"><span data-stu-id="a495f-154">Approve or reject requests for role elevation (single and/or bulk)</span></span>

<span data-ttu-id="a495f-155">Onaylamak veya reddetmek istediğiniz isteklerini seçin ve kararınızı ile karşılık gelen eylem çubuğunda düğmesini tıklatın:</span><span class="sxs-lookup"><span data-stu-id="a495f-155">Select the requests you wish to approve or deny, and click the button in the action bar that corresponds with your decision:</span></span>

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a><span data-ttu-id="a495f-156">My onay/reddetme için gerekçe</span><span class="sxs-lookup"><span data-stu-id="a495f-156">Provide justification for my approval/rejection</span></span>

<span data-ttu-id="a495f-157">Bu onaylamak veya birden çok isteği aynı anda reddetmek için yeni bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="a495f-157">This will open a new blade to approve or deny multiple requests at once.</span></span> <span data-ttu-id="a495f-158">Kararınızı için bir gerekçe girin ve Onayla (veya reddetme) alt veya dikey:</span><span class="sxs-lookup"><span data-stu-id="a495f-158">Enter a justification for your decision, and click approve (or deny) at the bottom or the blade:</span></span>

![](media/azure-ad-pim-approval-workflow/image029.png)

<span data-ttu-id="a495f-159">İstek işlemi tamamlandığında, durum simgesinde yaptığınız karar yansıtılacaktır (Bu örnekte, onaylama karardır):</span><span class="sxs-lookup"><span data-stu-id="a495f-159">When the request process is complete, the status symbol will reflect the decision you made (in this example, the decision is approve):</span></span>

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a><span data-ttu-id="a495f-160">Onay gerektiren bir rolü etkinleştirme isteği</span><span class="sxs-lookup"><span data-stu-id="a495f-160">Request activation of a role that requires approval</span></span>

<span data-ttu-id="a495f-161">İşlem rol etkinleştirmesi için aynı kalır gibi onay gerektiren bir rolün etkinleştirme isteyen eski PIM gezinti ya da yeni gezinti başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="a495f-161">Requesting activation of a role that requires approval may be initiated from either the old PIM navigation, or the new navigation, as the process for role activation remains the same.</span></span> <span data-ttu-id="a495f-162">Yalnızca bir rolü etkinleştirmek için roller listeden seçin:</span><span class="sxs-lookup"><span data-stu-id="a495f-162">Simply select a role from the list of roles to activate:</span></span>

![](media/azure-ad-pim-approval-workflow/image033.png)

<span data-ttu-id="a495f-163">Ayrıcalıklı rol çok faktörlü kimlik doğrulaması gerektiriyorsa, önce bu görevi tamamlamak için istenir:</span><span class="sxs-lookup"><span data-stu-id="a495f-163">If a privileged role requires Multi-Factor Authentication, you’ll be prompted to complete that task first:</span></span>

![](media/azure-ad-pim-approval-workflow/image035.png)

<span data-ttu-id="a495f-164">Tamamlandıktan sonra Etkinleştir'i tıklatın ve bir gerekçe (gerekliyse):</span><span class="sxs-lookup"><span data-stu-id="a495f-164">Once complete, click Activate and provide a justification (if required):</span></span>

![](media/azure-ad-pim-approval-workflow/image037.png)

<span data-ttu-id="a495f-165">İstek sahibi onay bekleyen istek ise bir bildirim görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="a495f-165">The requestor will see a notification that the request is pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-the-status-of-your-request-to-activate"></a><span data-ttu-id="a495f-166">İsteğiniz etkinleştirme durumunu görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="a495f-166">View the status of your request to activate</span></span>

<span data-ttu-id="a495f-167">Etkinleştirmek için bekleyen bir isteğiniz durumunu görüntüleme yeni gezinti bölmesinden erişilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a495f-167">Viewing the status of a pending request to activate must be accessed from the new navigation.</span></span> <span data-ttu-id="a495f-168">Sol Gezinti Çubuğu'ndan "İsteklerim" sekmesini seçin:</span><span class="sxs-lookup"><span data-stu-id="a495f-168">From the left navigation bar, select the “My Requests” tab:</span></span>

![](media/azure-ad-pim-approval-workflow/image041.png)

<span data-ttu-id="a495f-169">İstek durumu "Bekliyor" varsayılan olarak, ancak tüm görmek için geçiş yapabilir veya reddedilen istek sayısı.</span><span class="sxs-lookup"><span data-stu-id="a495f-169">The request state defaults to “Pending”, but you can toggle to see all or denied requests.</span></span>

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a><span data-ttu-id="a495f-170">Etkinleştirme onaylanırsa Azure AD'de Görevinizi tamamlamak</span><span class="sxs-lookup"><span data-stu-id="a495f-170">Complete your task in Azure AD if activation was approved</span></span>

<span data-ttu-id="a495f-171">İstek onaylandıktan sonra rol etkindir ve bu rol gerektiren herhangi bir iş ile devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a495f-171">Once the request is approved, the role is active and you may proceed with any work that requires this role.</span></span>

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a><span data-ttu-id="a495f-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a495f-172">Next steps</span></span>

<span data-ttu-id="a495f-173">Görüşleriniz bizim için değerlidir.</span><span class="sxs-lookup"><span data-stu-id="a495f-173">Your feedback is valuable to us.</span></span> <span data-ttu-id="a495f-174">Lütfen bizimle burada açıklamaları ya da geribildirim paylaşmak çekinmeyin!</span><span class="sxs-lookup"><span data-stu-id="a495f-174">Please feel free to share comments or feedback with us here!</span></span>
