---
title: "aaaThreats - Microsoft tehdit modelleme aracı - Azure | Microsoft Docs"
description: "Tehdit kategori sayfası hello Microsoft tehdit modelleme aracı için kullanıma sunulan tüm kategorileri içeren tehditleri oluşturulur."
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 0bd51f81370b6385ff1ac9769e34fc089e1dfc9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool-threats"></a>Microsoft tehdit modelleme aracı tehditleri

Merhaba tehdit modelleme aracı hello Microsoft Security Development Lifecycle (SDL) temel öğesidir. Yazılım sağlar architects tooidentify ve görece kolay ve düşük maliyetli tooresolve olduklarında olası güvenlik sorunlarını erkenden, etkisini azaltır. Sonuç olarak, geliştirme hello toplam maliyetini büyük ölçüde azaltır. Ayrıca, biz uzmanlarla tehdit modelleme tüm geliştiriciler için oluşturma ve tehdit modelleri analiz etme konusunda açık yönergeler sağlayarak kolaylaştırma güvenlikle ilgili olmayan unutmayın, hello aracı tasarlanmıştır.

> Merhaba ziyaret  **[tehdit modelleme aracı](./azure-security-threat-modeling-tool.md)**  tooget kullanmaya Bugün!

Merhaba tehdit modelleme aracı hello olanları aşağıdaki gibi belirli soruları yanıtlamanıza yardımcı olur:

* Nasıl bir saldırganın hello kimlik doğrulama verileri değiştirebilir miyim?
* Bir saldırgan hello kullanıcı profili verilerini okuyabiliyorsanız hello etkisi nedir?
* Toohello kullanıcı profili veritabanı erişimi reddedilirse ne olur?

## <a name="stride-model"></a>STRIDE modeli

işaret sorular, hangi tehditleri farklı türlerde kategorilere ayırır ve basitleştiren Microsoft kullanır hello STRIDE modeli, bu tür formüle toobetter Yardım hello genel güvenlik görüşmeleri.

| Kategori | Açıklama |
| -------- | ----------- |
| **Kimlik sahtekarlığı** | Yasadışı erişme ve kullanıcı adı ve parola gibi başka bir kullanıcının kimlik bilgileri kullanılarak içerir |
| **Oynama** | Merhaba kötü amaçlı veri değiştirilmesini içerir. Bir veritabanı ve veri hello değişikliğinin hello Internet gibi açık bir ağ üzerinden iki bilgisayar arasında akıp tutulan gibi toopersistent verilerde yapılan yetkisiz değişiklikler örnekler |
| **Geri çevirme** | Aksi takdirde hiçbir şekilde tooprove sahip diğer taraflar eylemi gerçekleştirme Reddet kullanıcılarıyla ilişkili — Örneğin, bir kullanıcı hello özelliği tootrace yasaklanmış hello işlemleri eksik bir sistemde geçersiz bir işlem gerçekleştirir. İnkar sistem toocounter ret tehditleri toohello yeteneğini gösterir. Örneğin, bir öğe satın alan bir kullanıcı hello öğeyi alındığında toosign olabilir. Kullanım hello giriş hello kullanıcı hello paket aldınız kanıt olarak imzalanmış hello satıcı seçebilir |
| **Bilgilerin açığa çıkmasına** | Toohave erişim tooit görmemesi bilgi tooindividuals Hello riskini içerir — örneğin, kullanıcılar tooread bunlar bulunmayan bir dosya hello yeteneklerini çok veya hello aktarım iki bilgisayar arasında bir saldırgan tarafından tooread verileri yeteneklerini erişim |
| **Hizmet reddi** | Hizmet (DoS) saldırısı reddi Reddet service toovalid kullanıcıları — Örneğin, yaparak bir Web sunucusu geçici olarak kullanılamıyor veya kullanılamaz. Belirli türde bir DoS karşı korumanız gerekir yalnızca tooimprove sistem kullanılabilirliği ve güvenilirliği tehditler |
| **Ayrıcalık yükseltme** | Ayrıcalıksız bir kullanıcı ayrıcalıklı erişim kazanır ve böylece yeterli erişim toocompromise sahip veya hello tüm sistem yok. Ayrıcalık tehditleri ayrıcalıkların dahil, bir saldırganın etkili bir şekilde tüm sistem savunma penetrated ve güvenilir hello sistem kendisini gerçekten tehlikeli olabilecek bir durum parçası haline bu durumlar |

## <a name="next-steps"></a>Sonraki adımlar

Çok devam**[tehdit modelleme aracı Azaltıcı](./azure-security-threat-modeling-tool-mitigations.md)**  toolearn hello farklı şekillerde Azure ile bu tehditleri azaltmak.
