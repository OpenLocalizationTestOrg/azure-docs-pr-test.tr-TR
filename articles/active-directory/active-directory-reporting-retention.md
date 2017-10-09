---
title: aaaAzure Active Directory rapor bekletme ilkeleri | Microsoft Docs
description: Rapor verileri Azure Active Directory'de bekletme ilkeleri
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c46a68198cb34e9c92662b2f8461010745392c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-retention-policies"></a>Azure Active Directory rapor bekletme ilkeleri


Bu konuda yanıtlarla toohello en yaygın sorular hello veri saklama için Azure Active Directory'de hello farklı etkinlik raporları ile birlikte sağlanır. 

**S: nasıl etkinlik verileri başlatılan hello koleksiyonu alabilir miyim?**

**A:**

| Azure AD Edition | Koleksiyon Başlat |
| :--              | :--   |
| Azure AD Premium P1 <br /> Azure AD Premium P2 | Olduğunda, bir abonelik için kaydolma |
| Azure AD Ücretsiz | Merhaba ilk kez açtığınızda hello [Azure Active Directory dikey](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) veya hello [API'leri raporlama](https://aka.ms/aadreports)  |

---
**S: etkinlik verilerinizi hello Azure portalında kullanılabilir olduğunda?**

**A:**

- **Hemen** -, zaten hello Klasik Azure portalı raporlarında ile çalışıyorsanız
- **2 saat içinde** -, raporlama hello Klasik Azure portalı açmadıysanız

---
**S: nasıl başlatılan güvenlik sinyal hello koleksiyonu alabilir miyim?**  

**Y:** , toouse hello Identity Protection Center katılımı güvenlik sinyalleri için hello toplama işlemi başlatılır. 


---
**S: ne kadar süreyle hello toplanan veriler depolanır?**

**A:**

**Etkinlik raporları**    

| Rapor                 | Azure AD Ücretsiz | Azure AD Premium P1 | Azure AD Premium P2 |
| :--                    | :--           | :--                 | :--                 |
| Dizin Denetimi        | 7 gün        | 30 gün             | 30 gün             |
| Oturum Açma Etkinliği       | 7 gün        | 30 gün             | 30 gün             |

**Güvenlik sinyalleri**

| Rapor         | Azure AD Ücretsiz | Azure AD Premium P1 | Azure AD Premium P2 |
| :--            | :--           | :--                 | :--                 |
| Risk altındaki kullanıcılar  | 7 gün        | 30 gün             | 90 gün             |
| Riskli oturum açma işlemleri | 7 gün        | 30 gün             | 90 gün             |

---