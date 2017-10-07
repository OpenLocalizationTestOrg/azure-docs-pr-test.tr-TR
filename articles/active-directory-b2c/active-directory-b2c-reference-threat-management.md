---
title: "Azure Active Directory B2C: Tehdit Yönetimi | Microsoft Docs"
description: "Hizmet reddi saldırılarını ve Azure Active Directory B2C parola saldırılarını algılama ve azaltma teknikleri hakkında bilgi edinin."
services: active-directory-b2c
documentationcenter: 
author: vigunase
manager: Ajith Alexander
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2016
ms.author: 
ms.openlocfilehash: 60bc0cc392b332cc4e9741ddb97dfa58e68ed420
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a>Azure Active Directory B2C: Tehdit Yönetimi

Tehdit yönetimi, sistem ve ağ karşı saldırılarına karşı koruma için planlamayı içerir. Hizmet reddi saldırılarını kaynakları kullanılamıyor toointended kullanıcılar yapabilir. Parola saldırılarını sağlama toounauthorized erişim tooresources. Azure Active Directory B2C (Azure AD B2C) verilerinizi birden çok yolla bu tehditlere karşı korumanıza yardımcı olabilecek yerleşik özelliklere sahiptir.

## <a name="denial-of-service-attacks"></a>Hizmet reddi saldırıları

Azure AD B2C Eşitlemeye tanımlama bilgileri ve hizmet reddi saldırılarına karşı kaynakları temel oranı ve bağlantı sınırları tooprotect gibi algılama ve azaltma teknikleri kullanır.

## <a name="password-attacks"></a>Parola saldırıları

Azure AD B2C azaltma teknikleri parola saldırılarını için yerinde de vardır. Parola yanılma saldırıları ve sözlük parola saldırılarını azaltma içerir. Kullanıcılar tarafından ayarlanan parolaları gerekli toobe makul karmaşık ' dir. Çeşitli sinyalleri kullanarak, Azure AD B2C istekleri hello bütünlüğünü analiz eder. Azure AD B2C tasarlanmıştır toointelligently ayırt hedeflenen kullanıcılar bilgisayar korsanlarının ve botnets. Azure AD B2C, saldırının hello olasılığını içinde girilen hello parolalar göre hesapları Gelişmiş stratejisi toolock sağlar.

Daha fazla bilgi için hello ziyaret [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).
