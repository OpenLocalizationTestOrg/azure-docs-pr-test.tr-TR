---
title: Azure Active Directory rapor bekletme ilkeleri | Microsoft Docs
description: Rapor verileri Azure Active Directory'de bekletme ilkeleri
services: active-directory
documentationcenter: 
author: MarkusVi
manager: mtillman
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: identity
ms.date: 12/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 61d3e8fbe26ab24ba0b551e52be0769228f09a11
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/16/2017
---
# <a name="azure-active-directory-report-retention-policies"></a>Azure Active Directory rapor bekletme ilkeleri


Bu konu, Azure Active Directory'de farklı etkinlik raporları için veri saklama ile birlikte en yaygın sorulara yanıtlar sağlar. 

**S: nasıl başlatılan etkinliği veri koleksiyonunu alabilir miyim?**

**A:**

| Azure AD Edition | Koleksiyon Başlat |
| :--              | :--   |
| Azure AD Premium P1 <br /> Azure AD Premium P2 | Olduğunda, bir abonelik için kaydolma |
| Azure AD Ücretsiz | İlk açtığınızda [Azure Active Directory dikey](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) veya [API'leri raporlama](https://aka.ms/aadreports)  |

---
**S: etkinlik verilerinizi Azure portalında kullanılabilir olduğunda?**

**A:**

- **Hemen** -, zaten Azure portalında raporları ile birlikte çalışıyorsanız
- **2 saat içinde** -, raporlama Azure portalında açmadıysanız

---
**S: nasıl başlatılan güvenlik sinyal koleksiyonu alabilir miyim?**  

**Y:** , kimlik koruma Merkezi'ni kullanmayı katılımı güvenlik sinyalleri için toplama işlemi başlatılır. 


---
**S: toplanan veriler ne kadar süreyle depolanır?**

**A:**

**Etkinlik raporları**    

| Rapor                 | Azure AD Ücretsiz | Azure AD Premium P1 | Azure AD Premium P2 |
| :--                    | :--           | :--                 | :--                 |
| Dizin Denetimi        | 7 gün        | 30 gün             | 30 gün             |
| Oturum Açma Etkinliği       | Yok           | 30 gün             | 30 gün             |
| Azure MFA kullanımı        | 30 gün       | 30 gün             | 30 gün             |

**Güvenlik sinyalleri**

| Rapor         | Azure AD Ücretsiz | Azure AD Premium P1 | Azure AD Premium P2 |
| :--            | :--           | :--                 | :--                 |
| Risk altındaki kullanıcılar  | 7 gün        | 30 gün             | 90 gün             |
| Riskli oturum açma işlemleri | 7 gün        | 30 gün             | 90 gün             |

---
