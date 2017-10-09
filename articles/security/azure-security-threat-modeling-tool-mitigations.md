---
title: "aaaMitigations - Microsoft tehdit modelleme aracı - Azure | Microsoft Docs"
description: "En sunulan hello Microsoft tehdit modelleme aracı vurgulama olası çözümleri toohello için Azaltıcı Etkenler sayfası tehditleri oluşturulur."
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
ms.openlocfilehash: 000c0980d976b09fc9287e582e3776efaf7e390c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool-mitigations"></a>Microsoft tehdit modelleme aracı Azaltıcı Etkenler

Merhaba tehdit modelleme aracı hello Microsoft Security Development Lifecycle (SDL) temel öğesidir. Yazılım sağlar architects tooidentify ve görece kolay ve düşük maliyetli tooresolve olduklarında olası güvenlik sorunlarını erkenden, etkisini azaltır. Sonuç olarak, geliştirme hello toplam maliyetini büyük ölçüde azaltır. Ayrıca, biz uzmanlarla tehdit modelleme tüm geliştiriciler için oluşturma ve tehdit modelleri analiz etme konusunda açık yönergeler sağlayarak kolaylaştırma güvenlikle ilgili olmayan unutmayın, hello aracı tasarlanmıştır.

Merhaba ziyaret  **[tehdit modelleme aracı](./azure-security-threat-modeling-tool.md)**  tooget kullanmaya Bugün!

## <a name="mitigation-categories"></a>Azaltma kategorileri

Merhaba tehdit modelleme aracı Azaltıcı toohello hello aşağıdaki oluşur Web uygulaması güvenlik çerçeve göre ayrılır:

| Kategori | Açıklama |
| -------- | ----------- |
| **[Denetim ve günlük](./azure-security-threat-modeling-tool-auditing-and-logging.md)** | Kimin ne zaman ve ne oldu? Denetim ve günlüğü toohow uygulama kayıtları güvenlikle ilgili olayları bakın. |
| **[Kimlik doğrulaması](./azure-security-threat-modeling-tool-authentication.md)** | Kimsin? Kimlik doğrulaması burada bir varlık başka bir varlık, genellikle bir kullanıcı adı ve parola gibi kimlik bilgilerini aracılığıyla hello kimliğini kanıtlar hello işlemdir |
| **[Yetkilendirme](./azure-security-threat-modeling-tool-authorization.md)** | Ne yapabilirsiniz? Yetkilendirme, kaynakları ve işlemleri için uygulamanızı erişim denetimleri nasıl sağladığını gerçekleşir. |
| **[İletişim güvenliği](./azure-security-threat-modeling-tool-communication-security.md)** | Kim, konuşma? İletişim güvenliği yapılan tüm iletişimi olabildiğince güvenli sağlar |
| **[Yapılandırma Yönetimi](./azure-security-threat-modeling-tool-configuration-management.md)** | Kullanan uygulamanızı olarak çalışıyor mu? Hangi veritabanlarının bağlamak? Uygulamanızı nasıl yönetilir? Bu ayarları güvenliği nasıl? Yapılandırma yönetimi başvuruyor toohow işletimsel bu sorunlar uygulamanız işleme |
| **[Şifreleme](./azure-security-threat-modeling-tool-cryptography.md)** | Nasıl gizli (gizlilik) tutuyor musunuz? Yetkisiz değiştirmeye karşı sağlama şeklini veri veya kitaplıkları (bütünlüğü)? Nasıl oluştururken çekirdeği için şifreleme açısından güçlü rastgele değerler sağlama? Şifreleme toohow başvuruyor, uygulamanızın gizliliği ve bütünlük zorlar |
| **[Özel durum yönetimi](./azure-security-threat-modeling-tool-exception-management.md)** | Uygulamanızdaki bir yöntem çağrısı başarısız olduğunda, uygulamanızın ne yapar? Ne kadar ortaya? Bilgi tooend kullanıcılar kolay hata döndürür? Değerli özel durum bilgilerini geri toohello çağıran geçirdiğiniz? Uygulamanızın düzgün biçimde başarısız oluyor? |
| **[Giriş doğrulaması](./azure-security-threat-modeling-tool-input-validation.md)** | Nasıl hello giriş uygulamanızın alır Geçerli ve güvenli olduğunu biliyor musunuz? Giriş doğrulaması uygulamanızı filtreleri, scrubs veya ek işlemeden önce giriş reddeder toohow başvuruyor. Giriş noktaları üzerinden giriş sınırlama ve çıkış noktaları üzerinden çıktı kodlama göz önünde bulundurun. Veritabanları ve dosya paylaşımları gibi kaynaklardan veri güveniyor musunuz? |
| **[Hassas veriler](./azure-security-threat-modeling-tool-sensitive-data.md)** | Uygulamanızın hassas verileri nasıl işler? Hassas verileri uygulamanızı hello ağ üzerinden bellekte veya kalıcı depoları korunması gereken herhangi bir veri işleme toohow başvurur |
| **[Oturum yönetimi](./azure-security-threat-modeling-tool-session-management.md)** | Nasıl yapar, uygulamanızın işlemek ve kullanıcı oturumlarını korumak? Bir kullanıcı, Web uygulamanızın arasındaki ilgili etkileşimlerin tooa seri bir oturum başvurur |

Bu belirlemenize yardımcı olur:

* Merhaba yapılan en yaygın hataları nerede
* Merhaba en tıklatılabilir geliştirmeleri nerede

Sonuç olarak, bu kategoriler toofocus kullanın ve hello giriş doğrulama, kimlik doğrulama ve yetkilendirme kategorilerde hello en yaygın güvenlik sorunları ortaya biliyorsanız, var. başlayabilmeniz için güvenlik işinizin önceliğini. Daha fazla bilgi için ziyaret  **[bu patent bağlantı](https://www.google.com/patents/US7818788)**

## <a name="next-steps"></a>Sonraki adımlar

Ziyaret  **[tehdit modelleme aracı tehditleri](./azure-security-threat-modeling-tool-threats.md)**  toolearn hakkında daha fazla bilgi hello tehdit kategorileri hello aracı toogenerate olası tasarım tehditleri kullanır.
