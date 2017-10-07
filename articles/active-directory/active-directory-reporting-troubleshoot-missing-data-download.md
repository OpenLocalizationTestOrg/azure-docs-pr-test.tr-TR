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
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a>Herhangi bir veri indirmiş olan hello Azure Active Directory etkinlik günlükleri bulunamıyor


## <a name="symptoms"></a>Belirtiler

Merhaba etkinlik günlükleri (Denetim veya oturum açma işlemleri) indirilir ve tüm hello kayıtları seçtiğim hello süredir görmüyorum. Neden? 

 ![Raporlama](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a>Nedeni

Etkinlik günlükleri hello Azure portal'ın yüklediğinizde, biz hello ölçek too120K kayıtları, çoğu tarafından sıralanan sınırlamak son. 

## <a name="resolution"></a>Çözüm

Yararlanabileceğiniz [Azure AD raporlama API'leri](active-directory-reporting-api-getting-started.md) toofetch tooa milyon kayıtları verilen herhangi bir noktada yukarı. Bizim önerilen bir komut dosyası hello raporlama API'leri toofetch çağıran bir zamanlama temelinde bir süre boyunca artımlı bir şekilde kaydeder toorun (örneğin, günlük veya haftalık) yaklaşımdır.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba bkz [Azure Active Directory raporlama](active-directory-reporting-faq.md).

