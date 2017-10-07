---
title: "Azure AD Connect: Önizleme özellikleri | Microsoft Docs"
description: "Bu konuda, Azure AD Connect önizlemede olan daha fazla ayrıntı özellikleri açıklanmaktadır."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a>Önizleme özellikleri hakkında daha fazla ayrıntı
Bu konuda, şu anda önizlemede nasıl toouse özellikleri açıklanmaktadır.

## <a name="group-writeback"></a>Grup geri yazma
İsteğe bağlı özellikler grup geri yazma için Hello seçenek sağlar, toowriteback **Office 365 grupları** yüklü olan Exchange ile tooa orman. Bu, her zaman hello bulutta yönetilir grubudur. Şirket içi Exchange varsa, böylece kullanıcılar bir şirket içi Exchange posta ile göndermek ve bu gruplardan e-postaları sonra geri bu grupları tooon içi yazabilirsiniz.

Office 365 grupları ve nasıl toouse bunları bulunabilir hakkında daha fazla bilgi [burada](http://aka.ms/O365g).

Bir Office 365 grup şirket içi bir dağıtım grubu olarak temsil edilen AD DS. Şirket içi Exchange server'ınızı Exchange 2013 toplu güncelleştirme (Mart 2015'te yayımlanan) 8 veya Exchange 2016 toorecognize bu yeni grup türü olmalıdır.

**Merhaba Önizleme sırasında notları**

* Merhaba adres defteri özniteliği hello Önizleme'de şu anda doldurulmamış. Bu öznitelik olmadan hello Grup hello GAL görünür değil. en kolay yolu toopopulate hello toouse hello Exchange PowerShell cmdlet'ini bu özniteliktir `update-recipient`.
* Yalnızca hello Exchange şema ormanlarla gruplar için geçerli hedefleri ' dir. Hiçbir Exchange algılandı, sonra Grup geri yazma olası tooenable değildir.
* Şu anda yalnızca tek orman Exchange kuruluşu dağıtımlar desteklenir. Birden fazla kuruluşun şirket içi Exchange varsa, daha sonra şirket içi GALSync çözümünü bu grupları tooappear için diğer ormanlara gerekir.
* Merhaba grup geri yazma özelliği, güvenlik grubu veya dağıtım grubu işlemez.

> [!NOTE]
> Grup geri yazma için bir abonelik tooAzure AD Premium gereklidir.
> 
>

## <a name="user-writeback"></a>Kullanıcı geri yazma
> [!IMPORTANT]
> Merhaba kullanıcı geri yazma önizleme özelliği hello Ağustos 2015 güncelleştirmesi tooAzure AD kaldırıldı Bağlan. Ardından etkinleştirdiyseniz, bu özellik devre dışı bırakmalısınız.
>
>

## <a name="next-steps"></a>Sonraki adımlar
Devam etmek, [Azure AD Connect özel yüklemesi](active-directory-aadconnect-get-started-custom.md).

[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.
