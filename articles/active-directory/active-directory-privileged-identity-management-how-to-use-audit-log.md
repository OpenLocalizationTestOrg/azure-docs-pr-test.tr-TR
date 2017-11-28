---
title: "Azure AD Privileged Identity Management denetim günlüğünü kullanma | Microsoft Docs"
description: "Azure Privileged Identity Management uzantısı'nda denetim günlüğü kullanmayı öğrenin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 7d9a5255a64d46c1388d328a606b3f297d61262b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-audit-log-in-pim"></a><span data-ttu-id="38ba9-103">PIM içinde denetim günlüğünü kullanma</span><span class="sxs-lookup"><span data-stu-id="38ba9-103">Using the audit log in PIM</span></span>
<span data-ttu-id="38ba9-104">Belirli bir süre içinde tüm kullanıcı atamaları ve etkinleştirmeler görmek için ayrıcalıklı Kimlik Yönetimi (PIM) denetim günlüğünü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38ba9-104">You can use the Privileged Identity Management (PIM) audit log to see all the user assignments and activations within a given time period.</span></span> <span data-ttu-id="38ba9-105">Yönetici, son kullanıcı ve eşitleme etkinliği de dahil olmak üzere, Kiracı etkinliğinde tam denetim geçmişini görmek istiyorsanız kullanabileceğiniz [Azure Active Directory'ye erişim ve kullanım raporları.](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="38ba9-105">If you want to see the full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use the [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-to-the-audit-log"></a><span data-ttu-id="38ba9-106">Denetim günlüğü gidin</span><span class="sxs-lookup"><span data-stu-id="38ba9-106">Navigate to the audit log</span></span>
<span data-ttu-id="38ba9-107">Gelen [Azure portal](https://portal.azure.com) Pano, select **Azure AD Privileged Identity Management** uygulama.</span><span class="sxs-lookup"><span data-stu-id="38ba9-107">From the [Azure portal](https://portal.azure.com) dashboard, select the **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="38ba9-108">Buradan, Denetim günlüğü tıklayarak erişim **yönetmek ayrıcalıklı rolleri** > **denetim geçmişi** PIM panosunda.</span><span class="sxs-lookup"><span data-stu-id="38ba9-108">From there, access the audit log by clicking **Manage privileged roles** > **Audit history** in the PIM dashboard.</span></span>

## <a name="the-audit-log-graph"></a><span data-ttu-id="38ba9-109">Denetim günlüğü grafiği</span><span class="sxs-lookup"><span data-stu-id="38ba9-109">The audit log graph</span></span>
<span data-ttu-id="38ba9-110">Toplam etkinleştirmeler, günde en çok etkinleştirmeleri ve gün başına ortalama etkinleştirmeleri bir çizgi grafiğinde görüntülemek için denetim günlüğünü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38ba9-110">You can use the audit log to view the total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="38ba9-111">Denetim geçmişi birden fazla rol ise, veri role göre de filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38ba9-111">You can also filter the data by role if there is more than one role in the audit history.</span></span>

<span data-ttu-id="38ba9-112">Kullanım **zaman**, **eylem**, ve **rol** günlük sıralamak için düğmeler.</span><span class="sxs-lookup"><span data-stu-id="38ba9-112">Use the **time**, **action**, and **role** buttons to sort the log.</span></span>

## <a name="the-audit-log-list"></a><span data-ttu-id="38ba9-113">Denetim günlüğü listesi</span><span class="sxs-lookup"><span data-stu-id="38ba9-113">The audit log list</span></span>
<span data-ttu-id="38ba9-114">Denetim günlüğü listesindeki sütun şunlardır:</span><span class="sxs-lookup"><span data-stu-id="38ba9-114">The columns in the audit log list are:</span></span>

* <span data-ttu-id="38ba9-115">**İstek sahibi** -rol etkinleştirme veya değiştirme isteyen kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="38ba9-115">**Requestor** - the user who requested the role activation or change.</span></span>  <span data-ttu-id="38ba9-116">Değer "Azure sistemi" ise, daha fazla bilgi için Azure denetim günlüğünü denetleyin.</span><span class="sxs-lookup"><span data-stu-id="38ba9-116">If the value is "Azure System", check the Azure audit log for more information.</span></span>
* <span data-ttu-id="38ba9-117">**Kullanıcı** -etkinleştiren veya bir role atanmış olan kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="38ba9-117">**User** - the user who is activating or assigned to a role.</span></span>
* <span data-ttu-id="38ba9-118">**Rol** -role atanmış veya kullanıcı tarafından etkinleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="38ba9-118">**Role** - the role assigned or activated by the user.</span></span>
* <span data-ttu-id="38ba9-119">**Eylem** - istek sahibi tarafından gerçekleştirilen eylemler.</span><span class="sxs-lookup"><span data-stu-id="38ba9-119">**Action** - the actions taken by the requestor.</span></span> <span data-ttu-id="38ba9-120">Bu atama, atamayı kaldırma konusunda, etkinleştirme veya devre dışı bırakma içerebilir.</span><span class="sxs-lookup"><span data-stu-id="38ba9-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="38ba9-121">**Zaman** - eylem oluştuğunda.</span><span class="sxs-lookup"><span data-stu-id="38ba9-121">**Time** - when the action occurred.</span></span>
* <span data-ttu-id="38ba9-122">**Akıl** -herhangi bir metin neden alana etkinleştirme sırasında girilen varsa, burada gösterir.</span><span class="sxs-lookup"><span data-stu-id="38ba9-122">**Reasoning** - if any text was entered into the reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="38ba9-123">**Sona erme** - rol etkinleştirmesi için yalnızca ilgili.</span><span class="sxs-lookup"><span data-stu-id="38ba9-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-the-audit-log"></a><span data-ttu-id="38ba9-124">Denetim günlüğü Filtrele</span><span class="sxs-lookup"><span data-stu-id="38ba9-124">Filter the audit log</span></span>
<span data-ttu-id="38ba9-125">Denetim günlüğüne tıklayarak görünür bilgileri filtreleyebilirsiniz **filtre** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="38ba9-125">You can filter the information that shows up in the audit log by clicking the **Filter** button.</span></span>  <span data-ttu-id="38ba9-126">**Güncelleştirme Grafik Parametreler dikey** görünür.</span><span class="sxs-lookup"><span data-stu-id="38ba9-126">The **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="38ba9-127">Filtreleri ayarladıktan sonra tıklayın **güncelleştirme** günlük verileri filtrelemek için.</span><span class="sxs-lookup"><span data-stu-id="38ba9-127">After you set the filters, click **Update** to filter the data in the log.</span></span>  <span data-ttu-id="38ba9-128">Veriler hemen görünmüyorsa, sayfayı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="38ba9-128">If the data doesn't appear right away, refresh the page.</span></span>

### <a name="change-the-date-range"></a><span data-ttu-id="38ba9-129">Tarih aralığını değiştirme</span><span class="sxs-lookup"><span data-stu-id="38ba9-129">Change the date range</span></span>
<span data-ttu-id="38ba9-130">Kullanım **Bugün**, **geçen hafta**, **geçen ay**, veya **özel** denetim günlüğünü zaman aralığını değiştirmek için düğmeler.</span><span class="sxs-lookup"><span data-stu-id="38ba9-130">Use the **Today**, **Past Week**, **Past Month**, or **Custom** buttons to change the time range of the audit log.</span></span>

<span data-ttu-id="38ba9-131">Seçtiğinizde **özel** düğmesi, size sunulur bir **gelen** tarih alanı ve bir **için** tarih alanı günlüğü için tarih aralığını belirtin.</span><span class="sxs-lookup"><span data-stu-id="38ba9-131">When you choose the **Custom** button, you will be given a **From** date field and a **To** date field to specify a range of dates for the log.</span></span>  <span data-ttu-id="38ba9-132">Tarih GG/AA/YYYY biçiminde girin veya tıklayın **Takvim** simgeyi ve bir takvimden tarihi seçin.</span><span class="sxs-lookup"><span data-stu-id="38ba9-132">You can either enter the dates in MM/DD/YYYY format or click on the **calendar** icon and choose the date from a calendar.</span></span>

### <a name="change-the-roles-included-in-the-log"></a><span data-ttu-id="38ba9-133">Günlüğüne dahil rollerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="38ba9-133">Change the roles included in the log</span></span>
<span data-ttu-id="38ba9-134">İşaretleyin veya işaretini kaldırın **rol** eklemek veya günlükten dışlamak için her rolün yanındaki onay kutusunu.</span><span class="sxs-lookup"><span data-stu-id="38ba9-134">Check or uncheck the **Role** checkbox next to each role to include or exclude it from the log.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="38ba9-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="38ba9-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

