---
title: 'Lisans: Azure AD SSPR''yi | Microsoft Docs'
description: "Lisans gereksinimlerini Azure AD Self Servis parola sıfırlama"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 9cecaaac429165346f7082f1965dc8a21063fe7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a>Lisans gereksinimleri için Azure AD Self Servis parola sıfırlama

Azure AD parola sıfırlama toofunction sırada, **kuruluşunuzda atanan en az bir Lisansı olmalıdır**. Kullanıcı başına hello parola sıfırlama deneyimi lisans uygulamaz. Microsoft lisans sözleşmenize uyumluluğun toomaintain, premium özellikleri kullanmanız tooassign lisansları tooany kullanıcıların gerekir.

* **Yalnızca kullanıcıların bulut** -Office 365 (O365) herhangi bir SKU veya Azure AD temel Ücretli
* **Bulut** ve/veya **şirket içi kullanıcıların** -Azure AD Premium P1 veya P2, Enterprise Mobility + Security (EMS) veya güvenli üretken Enterprise (Parametreyi)

## <a name="licenses-required-for-password-writeback"></a>Parola geri yazma için gerekli lisansları

toouse parola geri yazma, kiracınızda atanan lisansları aşağıdaki hello birine sahip olmalıdır.

* Azure AD Premium P1
* Azure AD Premium P2
* Enterprise Mobility + Security E3
* Enterprise Mobility + Security E5
* Secure Productive Enterprise E3
* Secure Productive Enterprise E5

> [!NOTE]
> Tek başına Office 365 planları lisans **parola geri yazma desteklemeyen** ve bu işlevselliği toowork planları önceki hello birini gerektirir.

Maliyetleri dahil olmak üzere ek lisans bilgilerine sayfaları aşağıdaki hello üzerinde bulunabilir.

* [Azure Active Directory fiyatlandırma site](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Güvenli üretken Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a>Grup veya kullanıcı tabanlı lisans etkinleştirme

Artık Azure AD, Grup tabanlı lisans izin Yöneticiler tooassign lisanslar toplu tooa grubundaki kullanıcılar yerine bir seferde bir atama destekler. [Ata, doğrulayın ve lisans sorunları gidermek](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

Bazı Microsoft Hizmetleri tüm konumlarda kullanılabilir değil. Hello Yöneticisi tooa kullanıcıya bir lisans atanabilir önce hello "Kullanım konumu" özelliği hello kullanıcı belirtmeniz gerekir. Lisans atama kullanıcı altında yapılabilir > Profil > hello Azure Portalı'ndaki ayarları. **Grup lisans atamasını kullanırken, belirtilen bir kullanım konumu olmayan tüm kullanıcılar hello dizininin hello konumu devralır.**

## <a name="next-steps"></a>Sonraki adımlar

bağlantılar aşağıdaki hello parola sıfırlama ve Azure AD kullanma ile ilgili ek bilgiler sağlar

* [**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın 
* [**Veri** ](active-directory-passwords-data.md) - gereklidir hello verileri anlamak ve nasıl kullanıldığı için parola yönetimi
* [**Sunum** ](active-directory-passwords-best-practices.md) -planlama ve burada bulunan hello kılavuzu kullanarak SSPR tooyour kullanıcılara dağıtma
* [**Özelleştirme** ](active-directory-passwords-customize.md) -hello görünümüne hello SSPR deneyimi, şirketiniz için özelleştirebilirsiniz.
* [**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin
* [**Teknik derinlemesine** ](active-directory-passwords-how-it-works.md) -hello perdenin toounderstand nasıl çalıştığını gidin
* [**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl? Neden? Ne? Nerede? Kim? Ne zaman? -Her zaman tooask istediğinizi tooquestions yanıtlar
* [**Sorun giderme** ](active-directory-passwords-troubleshoot.md) -nasıl biz SSPR ile bkz tooresolve ortak sorunları öğrenin

