---
title: "Azure AD Connect: yükleme türünü seçin. | Microsoft Docs"
description: "Bu konu, nasıl tooselect hello yükleme yazın toouse Azure AD Connect için adım adım anlatılmaktadır"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a700e59eb05947ee1dbd9993141200c9340b2f1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="select-which-installation-type-toouse-for-azure-ad-connect"></a>Azure AD Connect için hangi yükleme türü toouse seçin
Azure AD Connect, yeni yükleme için iki yükleme türleri vardır: Express ve özelleştirilebilir. Bu konu, yükleme sırasında toouse seçeneği toodecide yardımcı olur.

## <a name="express"></a>Express
Hızlı Başlangıç en yaygın kullanılan bir seçenektir ve yaklaşık % 90'ını tarafından tüm yeni yüklemeler kullanılır. Tasarlanmış tooprovide hello en yaygın müşteri senaryoları için çalışan bir yapılandırma oluştu.

Bunu varsayılır:

- Şirket içi orman tek bir Active Directory var.
- Merhaba yükleme için kullanabileceğiniz bir kuruluş yöneticisi hesabına sahip.
- Şirket içi Active Directory 100. 000'den az nesneler var.

Şunları alırsınız:

- [Parola Eşitleme](active-directory-aadconnectsync-implement-password-synchronization.md) çoklu oturum açma için şirket içi tooAzure AD alanından.
- Eşitleyen bir yapılandırma [kullanıcılar, gruplar, kişiler ve Windows 10 bilgisayarlar](active-directory-aadconnectsync-understanding-default-configuration.md).
- Tüm etki alanlarını ve tüm OU'larda tüm uygun nesneleri eşitlenmesi.
- [Otomatik yükseltmeyi](active-directory-aadconnect-feature-automatic-upgrade.md) etkin toomake hello en son sürüme her zaman kullandığınızdan emin olan.

Seçenekler burada Express kullanmaya devam edebilirsiniz:

- Tüm OU'larda toosynchronize istemiyorsanız hala Express ve kullanabilirsiniz hello son sayfasında işaretini **hello eşitleme işlemini başlat...** *. Merhaba Yükleme Sihirbazı'nı yeniden çalıştırın ve hello OU'larda değiştirme [yapılandırma seçenekleri](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) ve zamanlanmış eşitleme etkinleştirin.
- Tooenable Azure AD Premium hello özelliklerden birini, parola geri yazma gibi istediğiniz. İlk tamamlandı express tooget hello ilk yükleme gidin. Merhaba Yükleme Sihirbazı'nı yeniden çalıştırın ve hello değiştirme [yapılandırma seçenekleri](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).

## <a name="custom"></a>Özel
Merhaba özelleştirilmiş yolu express daha pek çok seçenek sağlar. Burada express için önceki bölümde açıklanan hello yapılandırma, kuruluşunuz için temsili olmadığı tüm durumlarda kullanılmalıdır.

Şu durumlarda kullanın:

- Active Directory'de erişim tooan kuruluş yöneticisi hesabı yok.
- Birden çok orman veya hello gelecekteki birden fazla ormanda toosynchronize planlayın.
- Merhaba Bağlan sunucudan ulaşılabilir değil, ormanınızdaki etki alanları sahiptir.
- Toouse Federasyon veya kullanıcı oturum açma için doğrudan kimlik doğrulama planlayın.
- 100. 000'den fazla nesneleri ve toouse tam SQL Server gerekir.
- Grup tabanlı toouse filtreleme ve yalnızca etki alanı veya OU tabanlı filtreleme planlayın.

## <a name="upgrade-from-dirsync"></a>DirSync'ten yükseltme
Şu anda DirSync kullanıyorsanız, ardından hello adımları [Dirsync'ten yükseltme](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade varolan yapılandırmanızı. İki farklı yükseltme seçenekleri şunlardır:

- Yerinde yükseltme tooinstall bağlanmak hello üzerinde aynı sunucu.
- Merhaba mevcut DirSync sunucu hala çalışır durumdayken yeni bir sunucu üzerinde dağıtım tooinstall Bağlan paralel.

## <a name="upgrade-from-azure-ad-sync"></a>Azure AD eşitleme'den yükseltme
Azure AD eşitleme kullanmakta olduğunuz sonra hello izleyebilirsiniz [aynı adımları](active-directory-aadconnect-upgrade-previous-version.md) bir Bağlan sürüm tooa yeni yükselttiğinizde olarak. İki farklı yükseltme seçenekleri şunlardır:

- Yerinde yükseltme tooinstall bağlanmak hello üzerinde aynı sunucu.
- Merhaba var olan Azure AD eşitleme sunucusu sırasında yeni bir sunucu üzerinde esnek geçiş tooinstall Bağlan hala çalışır durumda.

## <a name="migrate-from-fim2010-or-mim2016"></a>Fım2010 veya MIM2016 geçirmek
Şu anda Forefront Identity Manager 2010 veya Microsoft Identity Manager 2016 hello Azure AD Bağlayıcısı ile kullanıyorsanız, tek seçeneğiniz bir geçiş değil. Açıklanan başlangıç adımları [esnek geçiş](active-directory-aadconnect-upgrade-previous-version.md#swing-migration). Merhaba adımlarda, Azure AD eşitleme herhangi Bahsetme fım2010/MIM2016 ile değiştirin.

## <a name="next-steps"></a>Sonraki adımlar
Toouse seçili Hello seçeneğine bağlı olarak, hello tabloyu kullanın içerik toohello sol toofind Makalenizi hello ile adımları ayrıntılı.
