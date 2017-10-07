---
title: "Service Fabric güvenilir durum Yöneticisi ve güvenilir koleksiyonu iç aaaAzure | Microsoft Docs"
description: "Derin Dalış güvenilir koleksiyonu kavramları ve Azure Service Fabric tasarımında."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 651bfb52785a2475e4840cd471e87220d1936391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a>Azure Service Fabric güvenilir durumu Yöneticisi ve güvenilir koleksiyonu dahili bileşenleri
Bu belge, çekirdek bileşenleri hello arka planda nasıl güvenilir durum Yöneticisi ve güvenilir koleksiyonları toosee içinde ilgili alır.

> [!NOTE]
> Bu belge iş sürüyor değil. Yorumlar toothis makale tootell bize eklemek hangi konu hakkında daha fazla toolearn istersiniz.
>

##  <a name="local-persistence-model-log-and-checkpoint"></a>Yerel Kalıcılık modeli: günlük ve denetim noktası
Merhaba güvenilir durum Yöneticisi ve güvenilir koleksiyonları günlük ve denetim noktası adlı Kalıcılık modeli izleyin.
Bu modelde, her bir durum değişikliği diskte önce oturum açmış ve bellekte uygulanır.
Merhaba tam durum kendisini nadiren (paketini kalıcı Denetim noktası).
Merhaba avantaj farkları içine sıralı yalnızca Ekle yazma diskteki Gelişmiş performans için açık emin olmalıdır.

toobetter hello günlük ve denetim noktası modeli anlamak, ilk hello sonsuz disk senaryosu bakalım.
çoğaltılana önce hello güvenilir durum Yöneticisi her işlemi günlüğe kaydeder.
Günlüğe kaydetme hello güvenilir koleksiyonları tooapply hello işlemi yalnızca bellekte sağlar.
Günlükleri kalıcı yaptığınızdan, hatta hello çoğaltma başarısız olur ve yeniden, toobe gerektiğinde Merhaba güvenilir durum Yöneticisi yeterli bilgi kendi günlük tooreplay hello çoğaltma kaybetti tüm hello işlemler var.
Merhaba disk sonsuz olduğu gibi hello güvenilir koleksiyonu toomanage yalnızca hello bellek içi durumunun gerekiyor ve günlük kayıtlarını hiçbir zaman kaldırılan toobe gerekir.

Şimdi hello sınırlı disk senaryosu bakalım.
Günlük kayıtlarını birleştirdiğinizde hello güvenilir durum Yöneticisi disk alanı yetersiz çalıştırın.
Gerçekleşmeden önce hello güvenilir durum Yöneticisi tootruncate hello yeni kayıtlar için kendi günlük toomake yer gerekir.
Güvenilir durum Yöneticisi isteklerine güvenilir koleksiyonları toocheckpoint kendi bellek içi durumu toodisk hello.
Bu noktada, hello güvenilir koleksiyonları bellek içi durumuna kalıcı.
Bunların denetim noktaları Hello güvenilir koleksiyonları tamamladıktan sonra hello güvenilir durum Yöneticisi hello günlük toofree disk alanı kısaltabilir.
Merhaba çoğaltma yeniden toobe gerektiğinde güvenilir koleksiyonları belirttiğinizde durumlarına kurtarmak ve hello güvenilir durum Yöneticisi kurtarır ve hello son denetim noktasının bu yana gerçekleşen tüm hello durum değişiklikleri geri kazanır.

Başka bir değer denetim noktası oluşturma ekleme olan yaygın senaryolar kurtarma sürelerini artırır. Günlük hello son denetim noktasının bu yana gerçekleşen tüm işlemleri içerir.
Bu nedenle, güvenilir sözlükte belirli bir satır için birden çok değer gibi bir öğede birden fazla sürümünü içerebilir.
Buna karşılık, güvenilir koleksiyonu kontrol noktalarını yalnızca bir anahtar için her bir değerin en son sürümünü hello.

## <a name="next-steps"></a>Sonraki adımlar
* [İşlemler ve kilitleri](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

