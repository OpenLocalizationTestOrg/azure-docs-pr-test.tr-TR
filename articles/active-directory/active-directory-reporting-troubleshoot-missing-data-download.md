---
title: "Sorun giderme: Hello eksik verileri Azure Active Directory etkinlik günlükleri indirilen | Microsoft Docs"
description: "İndirilen Azure Active Directory etkinlik günlükleri bir çözüm toomissing verilerle sağlar."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 027b70e6efc570f81d3c836f50ee52aaa89be71a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a><span data-ttu-id="56c7a-103">Herhangi bir veri indirmiş olan hello Azure Active Directory etkinlik günlükleri bulunamıyor</span><span class="sxs-lookup"><span data-stu-id="56c7a-103">I can’t find any data in hello Azure Active Directory activity logs I have downloaded</span></span>


## <a name="symptoms"></a><span data-ttu-id="56c7a-104">Belirtiler</span><span class="sxs-lookup"><span data-stu-id="56c7a-104">Symptoms</span></span>

<span data-ttu-id="56c7a-105">Merhaba etkinlik günlükleri (Denetim veya oturum açma işlemleri) indirilir ve tüm hello kayıtları seçtiğim hello süredir görmüyorum.</span><span class="sxs-lookup"><span data-stu-id="56c7a-105">I downloaded hello activity logs (audit or sign-ins) and I don’t see all hello records for hello time I chose.</span></span> <span data-ttu-id="56c7a-106">Neden?</span><span class="sxs-lookup"><span data-stu-id="56c7a-106">Why?</span></span> 

 ![Raporlama](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a><span data-ttu-id="56c7a-108">Nedeni</span><span class="sxs-lookup"><span data-stu-id="56c7a-108">Cause</span></span>

<span data-ttu-id="56c7a-109">Etkinlik günlükleri hello Azure portal'ın yüklediğinizde, biz hello ölçek too120K kayıtları, çoğu tarafından sıralanan sınırlamak son.</span><span class="sxs-lookup"><span data-stu-id="56c7a-109">When you download activity logs in hello Azure portal, we limit hello scale too120K records, sorted by most recent.</span></span> 

## <a name="resolution"></a><span data-ttu-id="56c7a-110">Çözüm</span><span class="sxs-lookup"><span data-stu-id="56c7a-110">Resolution</span></span>

<span data-ttu-id="56c7a-111">Yararlanabileceğiniz [Azure AD raporlama API'leri](active-directory-reporting-api-getting-started.md) toofetch tooa milyon kayıtları verilen herhangi bir noktada yukarı.</span><span class="sxs-lookup"><span data-stu-id="56c7a-111">You can leverage [Azure AD Reporting APIs](active-directory-reporting-api-getting-started.md) toofetch up tooa million records at any given point.</span></span> <span data-ttu-id="56c7a-112">Bizim önerilen bir komut dosyası hello raporlama API'leri toofetch çağıran bir zamanlama temelinde bir süre boyunca artımlı bir şekilde kaydeder toorun (örneğin, günlük veya haftalık) yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="56c7a-112">Our recommended approach is toorun a script on a scheduled basis that calls hello reporting APIs toofetch records in an incremental fashion over a period of time (e.g., daily or weekly).</span></span>

## <a name="next-steps"></a><span data-ttu-id="56c7a-113">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="56c7a-113">Next steps</span></span>
<span data-ttu-id="56c7a-114">Merhaba bkz [Azure Active Directory raporlama](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="56c7a-114">See hello [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

