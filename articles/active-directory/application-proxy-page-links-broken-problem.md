---
title: "Merhaba sayfasında aaaLinks için uygulama proxy'si uygulama çalışmıyor | Microsoft Docs"
description: "Azure AD ile tümleşik uygulama proxy'si uygulamaları bağlantıların nasıl tootroubleshoot sorunlar"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 77c1e22d27c7a6436d8e57e105037c2328180481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="links-on-hello-page-dont-work-for-an-application-proxy-application"></a>Merhaba sayfadaki bağlantıları için uygulama proxy'si uygulama çalışmıyor

Bu makale yardımcı, tootroubleshoot neden bağlantılar, Azure Active Directory Uygulama proxy'si uygulamanızın üzerinde düzgün çalışmıyor.

## <a name="overview"></a>Genel Bakış 
Uygulama proxy'si uygulama yayımlandıktan sonra yayımlanan kök URL'si hello yalnızca bağlantılar hello uygulamadaki varsayılan çalışma hello içinde yer alan bağlantıları toodestinations gerektirir. Merhaba uygulamalar içindeki Hello bağlantılar çalışmayan, hello İç URL Merhaba uygulaması için büyük olasılıkla hello uygulamadaki bağlantıların tüm hello hedefler dahil değildir.

**Bunun nedeni?** Bir uygulama bir bağlantıya tıklandığında, uygulama proxy'si çalıştığında tooresolve hello URL içinde ya da bir iç URL olarak hello aynı uygulaması veya farklı bir harici URL'si olarak. İçinde değil tooan İç URL Hello bağlantı noktaları, aynı hello uygulama değil Bu demetlerin tooeither ait ve sonucu bir bulunamadı hatası.

## <a name="ways-you-can-resolve-broken-links"></a>Bağlantılar bozuk çözebilmek için yollar

Bu sorunu üç yolu tooresolve vardır. Merhaba aşağıdaki içinde listelenen artan karmaşıklık seçimlerdir.

1.  Merhaba uygulama için tüm hello ilgili bağlantıları içeren bir kök Hello İç URL olduğundan emin olun. Bu içerik hello içinde aynı yayımlanmış olarak çözümlendi tüm bağlantılar toobe sağlar uygulama.

    Merhaba iç URL'sini değiştirebilirsiniz, ancak giriş sayfasında kullanıcılar için toochange hello istemiyorsanız değişiklik hello giriş sayfası URL'si toohello daha önce İç URL yayımladı. Bu çok giderek yapılabilir "Azure Active Directory" -&gt; uygulama kayıtlar -&gt; hello uygulama - seçin&gt; özellikleri. Bu özellikler sekmesinde, gördüğünüz hello alan ayarlayabileceğiniz "giriş sayfası URL'si" toobe hello istenen giriş sayfası.

2.  Uygulamalarınızı tam etki alanı adlarını (FQDN) kullanıyorsanız, [özel etki alanlarını](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) toopublish uygulamalarınızı. Bu özellik hello aynı URL toobe hem dahili olarak kullanılır ve harici sağlar.

    Bu seçenek hello uygulama toointernal URL'leri içindeki hello bağlantılar da dışarıdan tanınır beri hello bağlantılar, uygulamanızda uygulama proxy'si aracılığıyla harici erişilebilir olmasını sağlar. Tüm bağlantılar hala toobelong tooa gerektiğini unutmayın uygulama yayımlanır. Ancak, bu seçenek hello ile bağlantılar toobelong toohello gerekmez aynı uygulama ve toomultiple uygulamaları ait olabilir.

3.  Bu seçeneklerin ikisi uygun varsa, URL çevirisi/yeniden yazma işlemi yapan yeni bir özellik için hello Önizleme katılın. Bu seçenek ile iç URL'leri veya uygulamalarınızı hello HTML gövdesinde mevcut bağlantıları olması çevrilen veya "eşlenir", dış uygulama Proxy URL'lerini toohello yayımlanan. Bu yalnızca hello HTML veya CSS bağlantılar için çalışır ve bu yardımcı bağlantı JS oluşturulursa. 

Sonuç olarak, hello kullanarak tavsiye [özel etki alanlarını](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) mümkünse çözümü. Toojoin hello Önizleme istiyorsanız, e-posta < aadapfeedback@microsoft.com > hello applicationId(s) ile.

## <a name="next-steps"></a>Sonraki adımlar
[Mevcut şirket içi proxy sunucuları ile çalışma](application-proxy-working-with-proxy-servers.md)

