---
title: "Sorun giderme: Azure Active Directory etkinlik günlüklerindeki eksik veriler | Microsoft Docs"
description: "Azure Active Directory’de kullanılabilen çeşitli raporları listeler"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: mtillman
editor: 
ms.assetid: 7cbe4337-bb77-4ee0-b254-3e368be06db7
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 01/15/2018
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 55587fb4ff6d8a2130eb838782a65788fb2dd2b3
ms.sourcegitcommit: 384d2ec82214e8af0fc4891f9f840fb7cf89ef59
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/16/2018
---
# <a name="i-cant-find-some-actions-that-i-performed-in-the-azure-active-directory-activity-log"></a>Azure Active Directory etkinlik günlüğünde gerçekleştirdiğim bazı eylemleri bulamıyorum


## <a name="symptoms"></a>Belirtiler

Azure portalında bazı eylemler gerçekleştirdim ve bu eylemlerin denetim günlüklerini `Activity logs > Audit Logs` dikey penceresinde görmeyi umuyordum, ancak bulamıyorum.

 ![Raporlama](./media/active-directory-reporting-troubleshoot-missing-audit-data/01.png)
 

## <a name="cause"></a>Nedeni

Eylemler, Etkinlik Denetim günlüğünde hemen görünmez. Denetim günlüklerinin portalda görünmesi, işlemin gerçekleştirilmesinden sonra 15 dakika ile 1 saat arasında sürebilir.

## <a name="resolution"></a>Çözüm

15 dakika bekleyin ve eylemlerin günlükte görüntülenip görüntülenmediğine bakın. Hala görmüyorsanız, lütfen bir destek bileti gönderin ve sorunu inceleyelim.


## <a name="next-steps"></a>Sonraki adımlar
Bkz. [Azure Active Directory raporlama hakkında SSS](active-directory-reporting-faq.md).

