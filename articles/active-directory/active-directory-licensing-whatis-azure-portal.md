---
title: "Grup tabanlı Azure Active Directory'de lisans aaaWhat mi? | Microsoft Belgeleri"
description: "Azure Active Directory grup tabanlı lisans, nasıl çalıştığı ve en iyi yöntemler açıklaması"
services: active-directory
keywords: Azure AD lisanslama
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/29/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 11647de6b76022cd2393751fcafc67ce671aeba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="group-based-licensing-basics-in-azure-active-directory"></a>Azure Active Directory'de Grup tabanlı lisans temelleri

Microsoft Office 365, Enterprise Mobility + güvenlik, Dynamics CRM ve benzer diğer ürünler gibi bulut Hizmetleri Ücretli kullanma lisansı gerektirir. Bu lisanslar erişim toothese Hizmetleri gereken tooeach kullanıcılar atanır. toomanage lisansları, yöneticiler hello yönetim portallarını (Office veya Azure) ve PowerShell cmdlet'leri birini kullanın. Azure Active Directory (Azure AD) olan tüm Microsoft bulut Hizmetleri için Kimlik Yönetimi destekleyen hello altyapının. Azure AD kullanıcıları için lisans Atama durumları hakkında bilgi depolar.

Şimdiye kadar lisansları yalnızca güçleştirebilir büyük ölçekli yönetim hello bireysel kullanıcı düzeyinde atanabilir. Örneğin, kuruluş ya da bir bölüm birleştirme veya bırakarak kullanıcı hello gibi kuruluş değişikliklere dayalı tooadd veya kaldırma kullanıcı lisansları yönetici genellikle karmaşık bir PowerShell komut dosyası yazmanız gerekir. Bu komut dosyası çağrıları tek tek toohello bulut hizmeti sağlar.

Bu sorunlar, tooaddress artık Azure AD, Grup tabanlı lisans içerir. Bir veya daha fazla ürün lisansları tooa grubu atayabilirsiniz. Azure AD hello lisansları tooall grubunun üyeleri, hello atanmasını sağlar. Merhaba gruba katılma herhangi bir yeni üyeler hello uygun lisansları atanır. Merhaba grubu bırakın, bu lisansların kaldırılır. Bu, lisans yönetimi hello kuruluş ve kullanıcı başına temelinde departman yapısı PowerShell tooreflect yapılan değişiklikleri aracılığıyla otomatikleştirmek için hello gereksinimini ortadan kaldırır.

## <a name="features"></a>Özellikler

Grup tabanlı lisansı hello önemli özellikleri şunlardır:

- Lisansları tooany güvenlik grubu, Azure AD'de atanabilir. Güvenlik grupları, Azure AD Connect kullanarak eşitlenen şirket olabilir. Güvenlik grupları (yalnızca bulut grupları olarak da bilinir) doğrudan Azure AD'de veya otomatik olarak hello Azure AD dinamik grup özelliği aracılığıyla da oluşturabilirsiniz.

- Bir ürün lisans tooa Grup atandığında, Merhaba yönetici bir veya daha fazla hizmet planları hello üründeki devre dışı bırakabilirsiniz. Genellikle, Hello Kuruluşunuz henüz bir ürüne hizmetini kullanarak hazır toostart olmadığında bu yapılır. Örneğin, Merhaba yönetici Office 365 tooa departmanı atarsanız, ancak geçici olarak hello Yammer hizmetini devre dışı bırakın.

- Kullanıcı düzeyinde lisans gerektiren tüm Microsoft bulut hizmetlerine desteklenir. Bu, tüm Office 365 ürünler, Enterprise Mobility + güvenlik ve Dynamics CRM içerir.

- Grup tabanlı lisans edinilebilir şu anda yalnızca [Azure portal hello](https://portal.azure.com). Kullanıcı ve Grup Yönetimi, hello Office 365 portalı gibi diğer yönetim portalları öncelikle kullanırsanız, bu nedenle toodo devam edebilirsiniz. Ancak grup düzeyinde hello Azure portal toomanage lisansları kullanmanız gerekir.

- Azure AD, grup üyeliği değişikliklerden kaynaklanan lisans değişiklikler otomatik olarak yönetir. Genellikle, bir üyelik değişiklik dakika içinde lisans değişiklikler etkili olur.

- Bir kullanıcı belirtilen lisans ilkelerini sahip birden fazla grup üyesi olabilir. Bir kullanıcı, doğrudan, dışında herhangi bir grup atanmış bazı lisanslar da sağlayabilirsiniz. kullanıcı durumunu kaynaklanan hello tüm atanan ürün ve hizmet lisansı birleşimidir.

- Bazı durumlarda, tooa kullanıcı lisansları atanamaz. Örneğin, olmayabilir kullanılabilir yeterli lisans hello kiracısında veya çakışan Hizmetleri atanan hello aynı saat. Yöneticiler, kendisi için Azure AD tam Grup lisansları işleyemedi kullanıcılar hakkında erişim tooinformation sahiptir. Bunlar daha sonra bu bilgilere dayanarak düzeltme eylemi alabilir.

- Genel Önizleme sırasında hello Kiracı toouse grup tabanlı Lisans Yönetimi'nde ücretli veya deneme aboneliği Azure AD temel veya Premium sürümleri için gereklidir.

## <a name="next-steps"></a>Sonraki adımlar

Grup tabanlı lisans aracılığıyla lisans yönetimi için diğer senaryolar hakkında daha fazla toolearn bakın:

* [Azure Active Directory lisansları kullanmaya başlama](active-directory-licensing-get-started-azure-portal.md)
* [Azure Active Directory'de lisansları tooa grup atama](active-directory-licensing-group-assignment-azure-portal.md)
* [Azure Active Directory'deki bir gruba lisans sorunlarını tanımlama ve](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Toomigrate tek tek kullanıcılar toogroup tabanlı Azure Active Directory'de lisanslama nasıl lisanslı](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory grup tabanlı ilave senaryolar lisanslama](active-directory-licensing-group-advanced.md)
