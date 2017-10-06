---
title: "İçerik Paketi hataları günlüğe Azure Active Directory etkinliği sorunlarını giderme | Microsoft Docs"
description: "Hello Azure Active Directory etkinliği İçerik Paketi ve adımları toofix hata iletilerinin bir listesini sağlar bunları."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 325de65ff1572a2f8f8319c0a52350bda03af3de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a><span data-ttu-id="9468c-103">İçerik Paketi hataları günlüklerini Azure Active Directory etkinliği sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="9468c-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span></span> 


<span data-ttu-id="9468c-104">Azure Active Directory Önizleme için Hello Power BI içerik paketi ile çalışırken, aşağıdaki hatalar hello çalıştırmak mümkündür:</span><span class="sxs-lookup"><span data-stu-id="9468c-104">When working with hello Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into hello following errors:</span></span> 

- [<span data-ttu-id="9468c-105">Yenileme başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="9468c-105">Refresh failed</span></span>](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [<span data-ttu-id="9468c-106">Başarısız tooupdate veri kaynağı kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="9468c-106">Failed tooupdate data source credentials</span></span>](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [<span data-ttu-id="9468c-107">Veri alma çok uzun sürüyor</span><span class="sxs-lookup"><span data-stu-id="9468c-107">Importing of data is taking too long</span></span>](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
<span data-ttu-id="9468c-108">Bu konu, hello olası nedenleri hakkında bilgi sağlar ve nasıl toofix bu hatalar.</span><span class="sxs-lookup"><span data-stu-id="9468c-108">This topic provides you with information about hello possible causes and how toofix these errors.</span></span>
 
## <a name="refresh-failed"></a><span data-ttu-id="9468c-109">Yenileme başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="9468c-109">Refresh failed</span></span> 
 
<span data-ttu-id="9468c-110">**Bu hatanın nasıl ortaya**: e-posta Power BI veya hello yenileme geçmişi başarısız durumda.</span><span class="sxs-lookup"><span data-stu-id="9468c-110">**How this error is surfaced**: Email from Power BI or failed status in hello refresh history.</span></span> 


| <span data-ttu-id="9468c-111">Nedeni</span><span class="sxs-lookup"><span data-stu-id="9468c-111">Cause</span></span> | <span data-ttu-id="9468c-112">Nasıl toofix</span><span class="sxs-lookup"><span data-stu-id="9468c-112">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="9468c-113">Toohello içerik paketi bağlanan hello kullanıcıları Hello kimlik bilgilerini sıfırlama ancak hello hello içerik paketi, bağlantı ayarlarını hello güncelleştirilmemiş hataları nedeniyle başarısız oldu yenileyin.</span><span class="sxs-lookup"><span data-stu-id="9468c-113">Refresh failure errors can be caused when hello credentials of hello users connecting toohello content pack have been reset but not updated in hello connection settings of hello of hello content pack.</span></span> | <span data-ttu-id="9468c-114">Power bı'da hello dataset karşılık gelen toohello Azure Active Directory etkinliği günlükleri Pano (Azure Active Directory etkinliği günlükleri) bulun, yenileme zamanlaması seçin ve ardından Azure AD kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="9468c-114">In Power BI, locate hello dataset corresponding toohello Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span></span> |
| <span data-ttu-id="9468c-115">Bir yenileme içerik paketi temel hello toodata sorunları nedeniyle başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="9468c-115">A refresh can fail due toodata issues in hello underlying content pack.</span></span> | <span data-ttu-id="9468c-116">Bir destek bileti dosya.</span><span class="sxs-lookup"><span data-stu-id="9468c-116">File a support ticket.</span></span> <span data-ttu-id="9468c-117">Daha fazla ayrıntı için bkz: [nasıl tooget desteklemek için Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="9468c-117">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 
 
## <a name="failed-tooupdate-data-source-credentials"></a><span data-ttu-id="9468c-118">Başarısız tooupdate veri kaynağı kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="9468c-118">Failed tooupdate data source credentials</span></span> 
 
<span data-ttu-id="9468c-119">**Bu hatanın nasıl ortaya**: Power toohello Azure Active Directory etkinliği günlükleri (Önizleme) İçerik Paketi bağlanırken BI'da.</span><span class="sxs-lookup"><span data-stu-id="9468c-119">**How this error is surfaced**: In Power BI, when you are connecting toohello Azure Active Directory Activity logs (preview) content pack.</span></span> 

| <span data-ttu-id="9468c-120">Nedeni</span><span class="sxs-lookup"><span data-stu-id="9468c-120">Cause</span></span> | <span data-ttu-id="9468c-121">Nasıl toofix</span><span class="sxs-lookup"><span data-stu-id="9468c-121">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="9468c-122">Genel yönetici veya bir güvenlik okuyucu veya bir güvenlik yöneticisine Hello bağlanan kullanıcının olduğu</span><span class="sxs-lookup"><span data-stu-id="9468c-122">hello connecting user is neither a global admin nor a security reader or a security admin.</span></span> | <span data-ttu-id="9468c-123">Genel yönetici veya bir güvenlik okuyucu veya bir güvenlik yönetici tooaccess hello içerik paketleri olan bir hesap kullanın.</span><span class="sxs-lookup"><span data-stu-id="9468c-123">Use an account that is either a global admin or a security reader or a security admin tooaccess hello content packs.</span></span> |
| <span data-ttu-id="9468c-124">Kiracı Premium Kiracı değil veya Premium lisansı dosya en az bir kullanıcı yok.</span><span class="sxs-lookup"><span data-stu-id="9468c-124">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span></span> | <span data-ttu-id="9468c-125">Bir destek bileti dosya.</span><span class="sxs-lookup"><span data-stu-id="9468c-125">File a support ticket.</span></span> <span data-ttu-id="9468c-126">Daha fazla ayrıntı için bkz: [nasıl tooget desteklemek için Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="9468c-126">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 

 

## <a name="importing-of-data-is-taking-too-long"></a><span data-ttu-id="9468c-127">Veri alma çok uzun sürüyor</span><span class="sxs-lookup"><span data-stu-id="9468c-127">Importing of data is taking too long</span></span> 
 
<span data-ttu-id="9468c-128">**Bu hatanın nasıl ortaya**: içerik paketiniz bağlandıktan sonra Power BI'da tooprepare hello veri içeri aktarma işlemi panonuz için Azure Active Directory etkinlik günlüğü başlatır.</span><span class="sxs-lookup"><span data-stu-id="9468c-128">**How this error is surfaced**: In Power BI, once you have connected your content pack, hello data import process starts tooprepare your dashboard for Azure Active Directory Activity log.</span></span> <span data-ttu-id="9468c-129">Merhaba iletisini görürsünüz: "*... veri alma* "</span><span class="sxs-lookup"><span data-stu-id="9468c-129">You see hello message: “*Importing data...*”</span></span>  

| <span data-ttu-id="9468c-130">Nedeni</span><span class="sxs-lookup"><span data-stu-id="9468c-130">Cause</span></span> | <span data-ttu-id="9468c-131">Nasıl toofix</span><span class="sxs-lookup"><span data-stu-id="9468c-131">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="9468c-132">Kiracı Hello boyutuna bağlı olarak, bu adım birkaç dakika too30 dakika arasında herhangi bir yere ele geçirebilir.</span><span class="sxs-lookup"><span data-stu-id="9468c-132">Depending on hello size of your tenant, this step could take anywhere from a few mins too30 minutes.</span></span> | <span data-ttu-id="9468c-133">Yalnızca endişelenmeyin.</span><span class="sxs-lookup"><span data-stu-id="9468c-133">Just be patient.</span></span> <span data-ttu-id="9468c-134">Merhaba ileti, bir saat içinde panonuz tooshowing değişmezse, Lütfen bir destek bileti dosya.</span><span class="sxs-lookup"><span data-stu-id="9468c-134">If hello message does not change tooshowing your dashboard within an hour, please file a support ticket.</span></span> <span data-ttu-id="9468c-135">Daha fazla ayrıntı için bkz: [nasıl tooget desteklemek için Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="9468c-135">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="9468c-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9468c-136">Next steps</span></span>

<span data-ttu-id="9468c-137">tooinstall hello Azure Active Directory Önizleme için Power BI içerik paketi tıklatın [burada](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span><span class="sxs-lookup"><span data-stu-id="9468c-137">tooinstall hello Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span></span>


