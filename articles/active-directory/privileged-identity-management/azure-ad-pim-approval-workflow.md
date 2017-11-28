---
title: "aaaAzure Privileged Identity Management onay iş akışları | Microsoft Docs"
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
ms.openlocfilehash: 4afaf5c138798a803eb3d3b7905b9361d65792cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="approvals-preview"></a><span data-ttu-id="2753b-103">Onaylar (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="2753b-103">Approvals (Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="2753b-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2753b-104">Overview</span></span>

<span data-ttu-id="2753b-105">Onaylarıyla Privileged Identity Management için rolleri toorequire onay etkinleştirme için yapılandırmak ve bir veya birden çok kullanıcı veya grup olarak yetkilendirilmiş onaylayanlar seçin.</span><span class="sxs-lookup"><span data-stu-id="2753b-105">With Approvals for Privileged Identity Management, you can configure roles toorequire approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="2753b-106">Toolearn nasıl okumaya devam edin tooconfigure roller ve onaylayanlar seçin.</span><span class="sxs-lookup"><span data-stu-id="2753b-106">Keep reading toolearn how tooconfigure roles and select approvers.</span></span>

>[!NOTE]
<span data-ttu-id="2753b-107">Lütfen bu özelliği geliştirilme aşamasındadır göz önünde bulundurun ve hatalar karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2753b-107">Please keep in mind this feature is still in development, and you may encounter bugs.</span></span> <span data-ttu-id="2753b-108">Merhaba işlevselliği, metin dahil ve adlandırma kuralları değiştirilebilir ve son düşünülmemelidir.</span><span class="sxs-lookup"><span data-stu-id="2753b-108">hello functionality, including text and naming conventions are subject to change, and should not be considered final.</span></span>


## <a name="key-terminology"></a><span data-ttu-id="2753b-109">Anahtar terminolojisi</span><span class="sxs-lookup"><span data-stu-id="2753b-109">Key Terminology</span></span>

<span data-ttu-id="2753b-110">*Uygun rol kullanıcı* – kuruluşunuzdaki tooan Azure AD rolü uygun olarak atanmış bir kullanıcı bir uygun rol olduğu (Rol etkinleştirmesi gerekir).</span><span class="sxs-lookup"><span data-stu-id="2753b-110">*Eligible Role User* – An eligible role user is a user within your organization that’s been assigned tooan Azure AD role as eligible (role requires activation).</span></span>

<span data-ttu-id="2753b-111">*Onaylayan temsilci* – bir temsilci onaylayan bir veya birden çok kişiler rol etkinleştirme isteklerini onaylama için sorumlu olan grupları, Azure AD içinde mi.</span><span class="sxs-lookup"><span data-stu-id="2753b-111">*Delegated Approver* – A delegated approver is one or multiple individuals or groups within your Azure AD who are responsible for approving requests for role activation.</span></span>

## <a name="scenarios"></a><span data-ttu-id="2753b-112">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="2753b-112">Scenarios</span></span>

<span data-ttu-id="2753b-113">Merhaba özel Önizleme hello aşağıdaki senaryoları destekler:</span><span class="sxs-lookup"><span data-stu-id="2753b-113">hello private preview supports hello following scenarios:</span></span>

<span data-ttu-id="2753b-114">**Bir ayrıcalıklı Rol Yöneticisi (PRA) olarak şunları yapabilirsiniz:**</span><span class="sxs-lookup"><span data-stu-id="2753b-114">**As a Privileged Role Administrator (PRA) you can:**</span></span>

-   [<span data-ttu-id="2753b-115">belirli roller onayını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="2753b-115">enable approval for specific roles</span></span>](#enable-approval-for-specific-roles)

-   [<span data-ttu-id="2753b-116">Onaylayan kullanıcılara ve/veya grupları tooapprove istekleri belirtin</span><span class="sxs-lookup"><span data-stu-id="2753b-116">specify approver users and/or groups tooapprove requests</span></span>](#specify-approver-users-and/or-groups-to-approve-requests)

-   [<span data-ttu-id="2753b-117">tüm ayrıcalıklı rolleri için istek ve onay geçmişini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="2753b-117">view request and approval history for all privileged roles</span></span>](#view-request-and-approval-history-for-all-privileged-roles)

<span data-ttu-id="2753b-118">**Belirlenen onaylayıcı olarak, şunları yapabilirsiniz:**</span><span class="sxs-lookup"><span data-stu-id="2753b-118">**As a designated approver, you can:**</span></span>

-   [<span data-ttu-id="2753b-119">Bekleyen onaylar (istek) görüntüleme</span><span class="sxs-lookup"><span data-stu-id="2753b-119">view pending approvals (requests)</span></span>](#view-pending-approvals-requests)

-   [<span data-ttu-id="2753b-120">onaylama veya reddetme rol yükseltme (tek ve/veya toplu) istekleri</span><span class="sxs-lookup"><span data-stu-id="2753b-120">approve or reject requests for role elevation (single and/or bulk)</span></span>](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [<span data-ttu-id="2753b-121">my onay/reddetme için gerekçe</span><span class="sxs-lookup"><span data-stu-id="2753b-121">provide justification for my approval/rejection</span></span>](#provide-justification-for-my-approval/rejection) 

<span data-ttu-id="2753b-122">**Uygun bir Role kullanıcı olarak şunları yapabilirsiniz:**</span><span class="sxs-lookup"><span data-stu-id="2753b-122">**As an Eligible Role User you can:**</span></span>

-   [<span data-ttu-id="2753b-123">onay gerektiren bir rolü etkinleştirme isteği</span><span class="sxs-lookup"><span data-stu-id="2753b-123">request activation of a role that requires approval</span></span>](#request-activation-of-a-role-that-requires-approval)

-   [<span data-ttu-id="2753b-124">İstek tooactivate hello durumunu görüntüleme</span><span class="sxs-lookup"><span data-stu-id="2753b-124">view hello status of your request tooactivate</span></span>](#view-the-status-of-your-request-to-activate)

-   [<span data-ttu-id="2753b-125">etkinleştirme onaylanırsa Azure AD'de Görevinizi tamamlamak</span><span class="sxs-lookup"><span data-stu-id="2753b-125">complete your task in Azure AD if activation was approved</span></span>](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a><span data-ttu-id="2753b-126">Gezinme</span><span class="sxs-lookup"><span data-stu-id="2753b-126">Navigation</span></span>

<span data-ttu-id="2753b-127">Biz hello Gezinti toosupport onayları güncelleştirdikten</span><span class="sxs-lookup"><span data-stu-id="2753b-127">We've updated hello navigation toosupport approvals</span></span>

![](media/azure-ad-pim-approval-workflow/image001.png)

<span data-ttu-id="2753b-128">Merhaba varsayılan giriş sayfası PIM ve hello yeni onayları belgeler hakkında uygun erişim tooinformation sağlar.</span><span class="sxs-lookup"><span data-stu-id="2753b-128">hello default landing page provides convenient access tooinformation about PIM and hello new approvals documentation.</span></span>

![](media/azure-ad-pim-approval-workflow/image002.png)

<span data-ttu-id="2753b-129">PIM, 'My denetim Geçmişi' tüm kullanıcılar için yeni bir bölüm de ekledik.</span><span class="sxs-lookup"><span data-stu-id="2753b-129">We’ve also added a new section for all users of PIM, ‘My Audit History’.</span></span> <span data-ttu-id="2753b-130">Burada tüm hello bilgi ilgili tooyour kimlik bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2753b-130">Here you can find all hello information relevant tooyour identity.</span></span> <span data-ttu-id="2753b-131">Bu seçenek, tüm bekleyen ve tamamlanmış istekleri, çözümlemeniz hello istekleri hakkında yaptığınız kararları ve tüm son rol etkinleştirme tek bir konumda içerir.</span><span class="sxs-lookup"><span data-stu-id="2753b-131">This includes all your pending and completed requests, any decisions you’ve made about hello requests you resolve, and all your past role activations in one convenient location.</span></span>

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a><span data-ttu-id="2753b-132">Belirli roller onayını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="2753b-132">Enable approval for specific roles</span></span>

<span data-ttu-id="2753b-133">belirli bir rol tooenable onaya hello sol gezinti bölmesinden ilk dizin rol seçin.</span><span class="sxs-lookup"><span data-stu-id="2753b-133">tooenable approval for a specific role, first select Directory Roles from hello left navigation.</span></span>

![](media/azure-ad-pim-approval-workflow/image004.png)

<span data-ttu-id="2753b-134">Bulma ve hello Directory rolleri sol gezinti ayarlarını seçin</span><span class="sxs-lookup"><span data-stu-id="2753b-134">Find and select settings in hello Directory Roles left navigation</span></span>

![](media/azure-ad-pim-approval-workflow/image006.png)

<span data-ttu-id="2753b-135">Ayrıcalıklı rolleri seçin:</span><span class="sxs-lookup"><span data-stu-id="2753b-135">Select privileged Roles:</span></span>

![](media/azure-ad-pim-approval-workflow/image009.png)

<span data-ttu-id="2753b-136">Hello seçin "Etkinleştir" onay bölümüne gerektirir:</span><span class="sxs-lookup"><span data-stu-id="2753b-136">Select “Enable” in hello Require approval section:</span></span>

![](media/azure-ad-pim-approval-workflow/image011.png)

<span data-ttu-id="2753b-137">Bir kez etkinleştirildikten sonra hello dikey penceresinde aşağıdaki ayrıntılara tooshow hello genişletin:</span><span class="sxs-lookup"><span data-stu-id="2753b-137">Once enabled, hello blade will expand tooshow hello following details:</span></span>

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
<span data-ttu-id="2753b-138">VERMEYİN herhangi onaylayanlar belirtirseniz, hello PRA(s) hello varsayılan approver(s) haline gelir.</span><span class="sxs-lookup"><span data-stu-id="2753b-138">If you DO NOT specify any approvers, hello PRA(s) become hello default approver(s).</span></span> <span data-ttu-id="2753b-139">Bu rol için tüm etkinleştirme istekleri gerekli tooapprove pra(s) olacaktır.</span><span class="sxs-lookup"><span data-stu-id="2753b-139">PRA(s) would be required tooapprove ALL activation requests for this role.</span></span>

### <a name="specify-approver-users-andor-groups-tooapprove-requests"></a><span data-ttu-id="2753b-140">Onaylayan kullanıcılara ve/veya grupları tooapprove istekleri belirtin</span><span class="sxs-lookup"><span data-stu-id="2753b-140">Specify approver users and/or groups tooapprove requests</span></span>

<span data-ttu-id="2753b-141">toodelegate onay hello seçeneğini çok onaylayanlar "Seç":</span><span class="sxs-lookup"><span data-stu-id="2753b-141">toodelegate approval, click hello option too“Select approvers”:</span></span>

![](media/azure-ad-pim-approval-workflow/image015.png)

<span data-ttu-id="2753b-142">Merhaba Select onaylayanlar dikey yüklediğinde, belirli bir kullanıcı veya grup hello üst veya hello önceden doldurulmuş haldedir listeden seçerek hello arama çubuğunu kullanarak arayın ve sonra "bittiğinde," Seç:</span><span class="sxs-lookup"><span data-stu-id="2753b-142">When hello Select approvers blade loads, you may search for a specific user or group using hello search bar at hello top, or selecting from hello pre-populated list, then click “Select” when finished:</span></span>

![](media/azure-ad-pim-approval-workflow/image017.png)

<span data-ttu-id="2753b-143">Not: Bir defada birden çok kullanıcı veya grup seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2753b-143">Note: You may select multiple users or groups at a time.</span></span>

<span data-ttu-id="2753b-144">Seçiminiz hello seçili onaylayanlar listesinde aşağıda görüldüğü gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="2753b-144">Your selection will appear in hello list of selected approvers as seen below:</span></span>

![](media/azure-ad-pim-approval-workflow/image019.png)

<span data-ttu-id="2753b-145">tooremove onaylayıcı, yalnızca hello Kaldır düğmesini sonraki tootheir adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2753b-145">tooremove an approver, simply click hello Remove button next tootheir name.</span></span>

<span data-ttu-id="2753b-146">tooadd ek onaylayanlar, yineleme hello işlemi.</span><span class="sxs-lookup"><span data-stu-id="2753b-146">tooadd additional approvers, repeat hello process.</span></span>

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a><span data-ttu-id="2753b-147">Tüm ayrıcalıklı rolleri için istek ve onay geçmişini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="2753b-147">View request and approval history for all privileged roles</span></span>

<span data-ttu-id="2753b-148">tüm ayrıcalıklı rolleri için tooview istek ve onay geçmişini hello panodan denetim geçmişi seçin:</span><span class="sxs-lookup"><span data-stu-id="2753b-148">tooview request and approval history for all privileged roles, select Audit History from hello dashboard:</span></span>

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
<span data-ttu-id="2753b-149">Eylem tarafından hello verileri sıralamak ve "Etkinleştirme onaylanmış" bakın</span><span class="sxs-lookup"><span data-stu-id="2753b-149">You can sort hello data by Action, and look for “Activation Approved”</span></span>

### <a name="view-pending-approvals-requests"></a><span data-ttu-id="2753b-150">Bekleyen onaylar (istek) görüntüleme</span><span class="sxs-lookup"><span data-stu-id="2753b-150">View pending approvals (requests)</span></span>

<span data-ttu-id="2753b-151">Onayınızı bekleyen istek olduğunda, bir temsilci onaylayan e-posta bildirimleri alırsınız.</span><span class="sxs-lookup"><span data-stu-id="2753b-151">As a delegated approver, you’ll receive email notifications when a request is pending your approval.</span></span> <span data-ttu-id="2753b-152">tooview bu istekleri hello panosunda (Merhaba yeni gezinti) select hello "beklemedeki onay istekleri" sekmesinden hello PIM portalında gezinti çubuğu kalmadı.</span><span class="sxs-lookup"><span data-stu-id="2753b-152">tooview these requests in hello PIM portal, from the dashboard (in hello new navigation) select hello “Pending Approval Requests” tab in hello left navigation bar.</span></span>

![](media/azure-ad-pim-approval-workflow/image023.png)

<span data-ttu-id="2753b-153">Burada, onay bekleyen isteklerin listesini görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="2753b-153">From there, you’ll see a list of requests pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a><span data-ttu-id="2753b-154">Onaylama veya reddetme rol yükseltme (tek ve/veya toplu) istekleri</span><span class="sxs-lookup"><span data-stu-id="2753b-154">Approve or reject requests for role elevation (single and/or bulk)</span></span>

<span data-ttu-id="2753b-155">Tooapprove istediğiniz ya da reddetme hello isteklerini seçin ve kararınızı ile karşılık gelen eylem çubuğunda hello düğmesini tıklatın:</span><span class="sxs-lookup"><span data-stu-id="2753b-155">Select hello requests you wish tooapprove or deny, and click hello button in the action bar that corresponds with your decision:</span></span>

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a><span data-ttu-id="2753b-156">My onay/reddetme için gerekçe</span><span class="sxs-lookup"><span data-stu-id="2753b-156">Provide justification for my approval/rejection</span></span>

<span data-ttu-id="2753b-157">Bu yeni bir dikey tooapprove açın veya birden çok isteği aynı anda reddedin.</span><span class="sxs-lookup"><span data-stu-id="2753b-157">This will open a new blade tooapprove or deny multiple requests at once.</span></span> <span data-ttu-id="2753b-158">Kararınızı için bir gerekçe girin ve Onayla (veya reddetme) hello alt veya hello dikey:</span><span class="sxs-lookup"><span data-stu-id="2753b-158">Enter a justification for your decision, and click approve (or deny) at hello bottom or hello blade:</span></span>

![](media/azure-ad-pim-approval-workflow/image029.png)

<span data-ttu-id="2753b-159">Merhaba isteği işlemi tamamlandığında, hello durum simgesinde yaptığınız karar yansıtılacaktır (Bu örnekte, hello onaylama karardır):</span><span class="sxs-lookup"><span data-stu-id="2753b-159">When hello request process is complete, hello status symbol will reflect the decision you made (in this example, hello decision is approve):</span></span>

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a><span data-ttu-id="2753b-160">Onay gerektiren bir rolü etkinleştirme isteği</span><span class="sxs-lookup"><span data-stu-id="2753b-160">Request activation of a role that requires approval</span></span>

<span data-ttu-id="2753b-161">Etkinleştirme ya da hello eski PIM hello yeni gezinti veya onay başlatılabilir gerektiren bir rolün isteyen, rol etkinleştirme kalır hello işlem olarak aynı hello.</span><span class="sxs-lookup"><span data-stu-id="2753b-161">Requesting activation of a role that requires approval may be initiated from either hello old PIM navigation, or hello new navigation, as hello process for role activation remains hello same.</span></span> <span data-ttu-id="2753b-162">Yalnızca bir rolü etkinleştirmek için roller hello listeden seçin:</span><span class="sxs-lookup"><span data-stu-id="2753b-162">Simply select a role from hello list of roles to activate:</span></span>

![](media/azure-ad-pim-approval-workflow/image033.png)

<span data-ttu-id="2753b-163">Ayrıcalıklı rol çok faktörlü kimlik doğrulaması gerektiriyorsa, önce bu görevi tamamlamak için istenir:</span><span class="sxs-lookup"><span data-stu-id="2753b-163">If a privileged role requires Multi-Factor Authentication, you’ll be prompted to complete that task first:</span></span>

![](media/azure-ad-pim-approval-workflow/image035.png)

<span data-ttu-id="2753b-164">Tamamlandıktan sonra Etkinleştir'i tıklatın ve bir gerekçe (gerekliyse):</span><span class="sxs-lookup"><span data-stu-id="2753b-164">Once complete, click Activate and provide a justification (if required):</span></span>

![](media/azure-ad-pim-approval-workflow/image037.png)

<span data-ttu-id="2753b-165">Merhaba istek sahibi onay bekleyen istek hello bir bildirim olduğunu görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="2753b-165">hello requestor will see a notification that hello request is pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-hello-status-of-your-request-tooactivate"></a><span data-ttu-id="2753b-166">İstek tooactivate hello durumunu görüntüleme</span><span class="sxs-lookup"><span data-stu-id="2753b-166">View hello status of your request tooactivate</span></span>

<span data-ttu-id="2753b-167">Bekleyen isteği tooactivate Hello durumunu görüntüleme yeni gezinti bölmesinden erişilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2753b-167">Viewing hello status of a pending request tooactivate must be accessed from the new navigation.</span></span> <span data-ttu-id="2753b-168">Merhaba sol gezinti çubuğu'ndan hello "İsteklerim" sekmesini seçin:</span><span class="sxs-lookup"><span data-stu-id="2753b-168">From hello left navigation bar, select hello “My Requests” tab:</span></span>

![](media/azure-ad-pim-approval-workflow/image041.png)

<span data-ttu-id="2753b-169">Merhaba istek durumu varsayılan olarak çok "Bekliyor", ancak tüm toosee geçiş yapabilir veya reddedilen istek sayısı.</span><span class="sxs-lookup"><span data-stu-id="2753b-169">hello request state defaults too“Pending”, but you can toggle toosee all or denied requests.</span></span>

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a><span data-ttu-id="2753b-170">Etkinleştirme onaylanırsa Azure AD'de Görevinizi tamamlamak</span><span class="sxs-lookup"><span data-stu-id="2753b-170">Complete your task in Azure AD if activation was approved</span></span>

<span data-ttu-id="2753b-171">Merhaba istek onaylandıktan sonra hello rolü etkin ve bu rol gerektiren herhangi bir iş ile devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2753b-171">Once hello request is approved, hello role is active and you may proceed with any work that requires this role.</span></span>

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a><span data-ttu-id="2753b-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2753b-172">Next steps</span></span>

<span data-ttu-id="2753b-173">Geri bildiriminiz değerlidir toous.</span><span class="sxs-lookup"><span data-stu-id="2753b-173">Your feedback is valuable toous.</span></span> <span data-ttu-id="2753b-174">Lütfen ücretsiz tooshare açıklamaları veya Geri bildiriminiz bizim için burada eşitleyerek!</span><span class="sxs-lookup"><span data-stu-id="2753b-174">Please feel free tooshare comments or feedback with us here!</span></span>
