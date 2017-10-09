---
title: Active Directory raporlama gecikmeleri aaaAzure | Microsoft Docs
description: "Olayları tooshow ayarlama, Azure Active Directory'ye raporlama için geçen süre"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 346b14f8-d16d-4b07-8211-e6c5eec07062
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 14367d21dfb28359f991037cc924d416420be456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-latencies"></a>Azure Active Directory rapor gecikmeleri
*Bu belge hello parçası olan [Azure Active Directory raporlama Kılavuzu](active-directory-reporting-guide.md).*

| Rapor | Minimum | Ortalama | Maksimum |
| --- | --- | --- | --- |
| **Güvenlik raporları** | | | |
| Düzensiz oturum açma etkinliği |2 saat |4 saat |8 saat |
| Bilinmeyen kaynaklardan gerçekleştirilen oturum açma işlemleri |2 saat |4 saat |8 saat |
| Birden çok hatadan sonra gerçekleştirilen oturum açma işlemleri |2 saat |4 saat |8 saat |
| Birden çok coğrafyadan gerçekleştirilen oturum açma işlemleri |2 saat |4 saat |8 saat |
| Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum açma işlemleri |2 saat |4 saat |8 saat |
| Muhtemelen virüs bulaşmış cihazlardan gerçekleştirilen oturum açma işlemleri |2 saat |4 saat |8 saat |
| Anormal oturum açma etkinliği gösteren kullanıcılar |2 saat |4 saat |8 saat |
| Sızan kimlik bilgilerine sahip kullanıcılar |2 saat |4 saat |8 saat |
| Tüm kullanıcı oturum açma etkinliği |2 saat |4 saat |8 saat |
| **Uygulama raporları** | | | |
| Hesap etkinlik sağlama |2 saat |4 saat |8 saat |
| Hesap hazırlama hataları |2 saat |4 saat |8 saat |
| Uygulama kullanımı |2 saat |4 saat |8 saat |
| Parola rollover durumu |2 saat |4 saat |8 saat |
| **Denetim ve etkinlik raporları** | | | |
| Denetim raporu |1 dakika |15 dakika |30 dakika |
| Parola sıfırlama etkinliği (Azure AD) |2 saat |4 saat |8 saat |
| Parola sıfırlama etkinliği (Identity Manager) |2 saat |4 saat |8 saat |
| Parola sıfırlama kaydı etkinliği (Azure AD) |2 saat |4 saat |8 saat |
| Parola sıfırlama kaydı etkinliği (Identity Manager) |2 saat |4 saat |8 saat |
| Self Servis Grup etkinliği (Azure AD) |2 saat |4 saat |8 saat |
| Self Servis Grup etkinliği (Identity Manager) |2 saat |4 saat |8 saat |
| **RMS raporları** | | | |
| En etkin RMS kullanıcıları |2 saat |4 saat |8 saat |
| RMS kullanımı |2 saat |4 saat |8 saat |
| RMS Aygıt kullanımı |2 saat |4 saat |8 saat |
| RMS özellikli uygulama kullanımı |2 saat |4 saat |8 saat |

