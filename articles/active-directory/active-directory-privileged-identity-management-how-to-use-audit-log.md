---
title: "Azure AD Privileged Identity Management aaaHow toouse hello Denetim günlüğüne | Microsoft Docs"
description: "Nasıl toouse hello denetim günlüğünü hello Azure Privileged Identity Management uzantısı'nda öğrenin."
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
ms.openlocfilehash: 36987eaab9fe02c5dd7b4f4705e487299430745d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-audit-log-in-pim"></a><span data-ttu-id="add1b-103">PIM içinde Hello denetim günlüğünü kullanma</span><span class="sxs-lookup"><span data-stu-id="add1b-103">Using hello audit log in PIM</span></span>
<span data-ttu-id="add1b-104">Belirli bir süre içinde tüm hello kullanıcısı atamalarını ve etkinleştirmeler hello ayrıcalıklı Kimlik Yönetimi (PIM) denetim günlüğü toosee'yı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="add1b-104">You can use hello Privileged Identity Management (PIM) audit log toosee all hello user assignments and activations within a given time period.</span></span> <span data-ttu-id="add1b-105">Yönetici, son kullanıcı ve eşitleme etkinliği de dahil olmak üzere, kiracınızda etkinliğinin toosee hello tam denetim geçmişi istiyorsanız hello kullanabilirsiniz [Azure Active Directory'ye erişim ve kullanım raporları.](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="add1b-105">If you want toosee hello full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use hello [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-toohello-audit-log"></a><span data-ttu-id="add1b-106">Toohello denetim günlüğü gidin</span><span class="sxs-lookup"><span data-stu-id="add1b-106">Navigate toohello audit log</span></span>
<span data-ttu-id="add1b-107">Merhaba gelen [Azure portal](https://portal.azure.com) Pano, select hello **Azure AD Privileged Identity Management** uygulama.</span><span class="sxs-lookup"><span data-stu-id="add1b-107">From hello [Azure portal](https://portal.azure.com) dashboard, select hello **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="add1b-108">Tıklayarak hello denetim günlüğü buradan, erişim **yönetmek ayrıcalıklı rolleri** > **denetim geçmişi** hello PIM panosunda.</span><span class="sxs-lookup"><span data-stu-id="add1b-108">From there, access hello audit log by clicking **Manage privileged roles** > **Audit history** in hello PIM dashboard.</span></span>

## <a name="hello-audit-log-graph"></a><span data-ttu-id="add1b-109">Merhaba denetim günlüğü grafiği</span><span class="sxs-lookup"><span data-stu-id="add1b-109">hello audit log graph</span></span>
<span data-ttu-id="add1b-110">Bir çizgi grafiğinde hello denetim günlüğü tooview hello toplam etkinleştirmeler, günde en çok etkinleştirmeleri ve gün başına ortalama etkinleştirmeleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="add1b-110">You can use hello audit log tooview hello total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="add1b-111">Merhaba denetim geçmişi birden fazla rol varsa hello veri role göre filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="add1b-111">You can also filter hello data by role if there is more than one role in hello audit history.</span></span>

<span data-ttu-id="add1b-112">Kullanım hello **zaman**, **eylem**, ve **rol** düğmeleri toosort hello günlük.</span><span class="sxs-lookup"><span data-stu-id="add1b-112">Use hello **time**, **action**, and **role** buttons toosort hello log.</span></span>

## <a name="hello-audit-log-list"></a><span data-ttu-id="add1b-113">Merhaba denetim günlüğü listesi</span><span class="sxs-lookup"><span data-stu-id="add1b-113">hello audit log list</span></span>
<span data-ttu-id="add1b-114">Merhaba denetim günlüğü listesinde Hello sütunlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="add1b-114">hello columns in hello audit log list are:</span></span>

* <span data-ttu-id="add1b-115">**İstek sahibi** -hello rol etkinleştirme veya değiştirme isteyen hello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="add1b-115">**Requestor** - hello user who requested hello role activation or change.</span></span>  <span data-ttu-id="add1b-116">Merhaba değer "Azure sistemi" ise, daha fazla bilgi için hello Azure denetim günlüğünü denetleyin.</span><span class="sxs-lookup"><span data-stu-id="add1b-116">If hello value is "Azure System", check hello Azure audit log for more information.</span></span>
* <span data-ttu-id="add1b-117">**Kullanıcı** -etkinleştiriyor veya tooa rolü atanmış hello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="add1b-117">**User** - hello user who is activating or assigned tooa role.</span></span>
* <span data-ttu-id="add1b-118">**Rol** -hello rolü atanmış veya hello kullanıcı tarafından etkinleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="add1b-118">**Role** - hello role assigned or activated by hello user.</span></span>
* <span data-ttu-id="add1b-119">**Eylem** - hello istek sahibi tarafından yapılan hello eylemler.</span><span class="sxs-lookup"><span data-stu-id="add1b-119">**Action** - hello actions taken by hello requestor.</span></span> <span data-ttu-id="add1b-120">Bu atama, atamayı kaldırma konusunda, etkinleştirme veya devre dışı bırakma içerebilir.</span><span class="sxs-lookup"><span data-stu-id="add1b-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="add1b-121">**Zaman** - hello eylem oluştuğunda.</span><span class="sxs-lookup"><span data-stu-id="add1b-121">**Time** - when hello action occurred.</span></span>
* <span data-ttu-id="add1b-122">**Akıl** -herhangi bir metin hello neden alanına etkinleştirme sırasında girilen varsa, burada gösterir.</span><span class="sxs-lookup"><span data-stu-id="add1b-122">**Reasoning** - if any text was entered into hello reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="add1b-123">**Sona erme** - rol etkinleştirmesi için yalnızca ilgili.</span><span class="sxs-lookup"><span data-stu-id="add1b-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-hello-audit-log"></a><span data-ttu-id="add1b-124">Filtre hello denetim günlüğü</span><span class="sxs-lookup"><span data-stu-id="add1b-124">Filter hello audit log</span></span>
<span data-ttu-id="add1b-125">Merhaba tıklayarak hello Denetim günlüğüne görüntülenir hello bilgileri filtreleyebilirsiniz **filtre** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="add1b-125">You can filter hello information that shows up in hello audit log by clicking hello **Filter** button.</span></span>  <span data-ttu-id="add1b-126">Merhaba **güncelleştirme Grafik Parametreler dikey** görünür.</span><span class="sxs-lookup"><span data-stu-id="add1b-126">hello **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="add1b-127">Merhaba filtreleri ayarladıktan sonra tıklayın **güncelleştirme** hello günlük toofilter hello verileri.</span><span class="sxs-lookup"><span data-stu-id="add1b-127">After you set hello filters, click **Update** toofilter hello data in hello log.</span></span>  <span data-ttu-id="add1b-128">Merhaba veri hemen görünmüyorsa, hello sayfayı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="add1b-128">If hello data doesn't appear right away, refresh hello page.</span></span>

### <a name="change-hello-date-range"></a><span data-ttu-id="add1b-129">Merhaba tarih aralığını Değiştir</span><span class="sxs-lookup"><span data-stu-id="add1b-129">Change hello date range</span></span>
<span data-ttu-id="add1b-130">Kullanım hello **Bugün**, **geçen hafta**, **geçen ay**, veya **özel** hello denetim günlüğü toochange hello zaman aralığını düğmeler.</span><span class="sxs-lookup"><span data-stu-id="add1b-130">Use hello **Today**, **Past Week**, **Past Month**, or **Custom** buttons toochange hello time range of hello audit log.</span></span>

<span data-ttu-id="add1b-131">Merhaba seçtiğinizde **özel** düğmesi, size sunulur bir **gelen** tarih alanı ve bir **için** alan toospecify hello günlüğü için tarih aralığını tarih.</span><span class="sxs-lookup"><span data-stu-id="add1b-131">When you choose hello **Custom** button, you will be given a **From** date field and a **To** date field toospecify a range of dates for hello log.</span></span>  <span data-ttu-id="add1b-132">AA/GG/YYYY biçiminde hello tarihleri girin veya üzerinde hello tıklatın **Takvim** simgesini ve bir takvimden hello tarih seçin.</span><span class="sxs-lookup"><span data-stu-id="add1b-132">You can either enter hello dates in MM/DD/YYYY format or click on hello **calendar** icon and choose hello date from a calendar.</span></span>

### <a name="change-hello-roles-included-in-hello-log"></a><span data-ttu-id="add1b-133">Merhaba günlüğüne dahil hello rollerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="add1b-133">Change hello roles included in hello log</span></span>
<span data-ttu-id="add1b-134">İşaretleyin veya işaretini kaldırın hello **rol** onay kutusunu sonraki tooeach rol tooinclude veya hariç tutma hello oturumunuzu.</span><span class="sxs-lookup"><span data-stu-id="add1b-134">Check or uncheck hello **Role** checkbox next tooeach role tooinclude or exclude it from hello log.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="add1b-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="add1b-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

