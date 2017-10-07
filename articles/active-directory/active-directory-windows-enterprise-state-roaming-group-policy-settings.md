---
title: "aaaGroup ilke ve MDM ayarlarını | Microsoft Docs"
description: "Şirkete ait cihazlarda kullanılmalıdır Yönetimi (MDM) ayarları Grup İlkesi ve mobil cihaz hakkında bilgi sağlar. Bu ilkeler, uygulanan toohello kullanıcının tüm aygıt olan."
services: active-directory
keywords: "Grup İlkesi ve kurumsal durumda dolaşım, Kurumsal durumda dolaşım, windows bulut için MDM ayarları nelerdir"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 6471a9b3-8dd4-4237-89d1-bfbeca9f8252
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 762419b47014b1fb4d92ac528785e20078afe689
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="group-policy-and-mdm-settings"></a>Grup İlkesi ve MDM ayarları
Bu ilkeler uygulanan toohello kullanıcının tüm aygıt olduğundan bu Grup İlkesi ve mobil cihaz Yönetimi (MDM) ayarları yalnızca şirkete ait cihazlarda kullanır. Kişisel bir MDM İlkesi toodisable ayarları eşitleme uygulama, kullanıcının sahip olduğu cihaz bu aygıtın hello kullanımını olumsuz etkiler. Ayrıca, diğer kullanıcı hesapları hello aygıtta hello İlkesi tarafından etkilenmez.

Kişisel (yönetilmeyen) cihazlar için gezici toomanage kullanmak istediğiniz kuruluşların Azure portal tooenable hello veya Grup İlkesi veya MDM kullanmak yerine gezici devre dışı bırakma
tabloları aşağıdaki hello hello İlkesi ayarları açıklanır.

## <a name="mdm-settings"></a>MDM ayarları
tooboth Windows 10 ve Windows 10 Mobile Hello MDM ilke ayarlarını uygulayın.  Windows 10 Mobile destek kullanıcının OneDrive hesabına gezici dayalı yalnızca Microsoft hesabı yok.  Lütfen Azure AD için hangi cihazlar desteklenir ile ilgili ayrıntılar için "Aygıtları ve uç noktaları" bölümü çok temel eşitleniyor.

| Ad | Açıklama |
| --- | --- |
| Microsoft hesabı bağlantıya izin ver |Merhaba cihazda bir Microsoft hesabı kullanarak kullanıcıların tooauthenticate sağlar |
| Ayarlarımı eşitlemesine izin ver |Kullanıcı tooroam Windows ayarları ve uygulama verilerini sağlar; Bu ilkeyi devre dışı bırakma eşitleme yanı sıra, mobil cihazlarda yedeklemelerinin devre dışı bırakır |

## <a name="group-policy-settings"></a>Grup İlkesi ayarları
Active Directory etki alanına katılmış tooan tooWindows 10 aygıtları Hello Grup İlkesi ayarlarını uygulayın. Merhaba Tablo ayrıca 'hello açıklamasında kullanmayın ile' belirtilmiştir toomanage eşitleme ayarları görünür, ancak kuruluş durumu Dolaşım için Windows 10 için çalışmaz eski ayarları içerir.

| Ad | Açıklama |
| --- | --- |
| Hesaplar: Blok Microsoft hesapları |Bu ilke ayarı, kullanıcıların bu bilgisayarda yeni Microsoft hesapları eklemesini engeller |
| Eşitleme değil |Kullanıcı tooroam Windows ayarları ve uygulama verilerini engeller |
| Eşitleme kişiselleştirme |Devre dışı bırakır hello Temalar grubunun eşitleniyor |
| Tarayıcı ayarlarını eşitlemesini değil |Devre dışı bırakır hello Internet Explorer grubunun eşitleniyor |
| Parola Eşitleme yok |Parolaları grubu devre dışı bırakır eşitleniyor |
| Diğer Windows ayarları eşitleme değil |Diğer Windows Ayarları grubu devre dışı bırakır eşitleniyor |
| Masaüstü kişiselleştirme eşitleme değil |Kullanmayın; hiçbir etkisi yoktur |
| Ölçülen bağlantılarında eşitleme değil |Dolaşım devre dışı bırakır tarifeli cep telefonu 3 G gibi bağlantısı |
| Uygulamaları eşitleme değil |Kullanmayın; hiçbir etkisi yoktur |
| Uygulama ayarları eşitleme değil |Devre dışı bırakır uygulama verileri dolaşımı |
| Başlangıç ayarları eşitleme değil |Kullanmayın; hiçbir etkisi yoktur |

## <a name="related-topics"></a>İlgili konular
* [Kurumsal durumda Dolaşım genel bakış](active-directory-windows-enterprise-state-roaming-overview.md)
* [Azure Active Directory'de gezici Kurumsal durumunu etkinleştir](active-directory-windows-enterprise-state-roaming-enable.md)
* [Ayarlar ve veri dolaşımı SSS](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Windows 10 Dolaşım ayarları başvurusu](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Sorun giderme](active-directory-windows-enterprise-state-roaming-troubleshooting.md)

