---
title: "en iyi güvenlik uygulamalarını, şeyler aaaInternet | Microsoft Docs"
description: "Merhaba makale seçkin Microsoft Internet şeyler en iyi güvenlik uygulamaları ve genel öneriler listesini sağlar."
services: security
documentationcenter: na
author: TomShinder
manager: StevenPo
editor: TomSh
ms.assetid: 2d5598c5-4c30-481d-b8f4-51ee024ea9a7
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: yurid
ms.openlocfilehash: 7ee31c912e8ac230ffa5efcd5b4c2b0b0713584f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-best-practices"></a>En iyi güvenlik uygulamalarını, noktalar, Internet
Güvenliğini sağlama hello nesnelerin interneti (IOT) altyapısı çözümlere dahil herkes için kritik bir iş değil. Merhaba ve cihazı dahil Hello sayısı nedeniyle, bu cihazların Merhaba etkisi bir güvenlik olayı dağıtılan yapı toocompromise milyonlarca IOT cihazları Önemsiz olmayan ve yaygın etkisi olabilir ilgili.

Bu nedenle, bir güvenlik derinlemesine yaklaşım IOT güvenlik gerekir. Veri gereksinimlerini toobe güvenli hello bulutta ve şekliyle özel ve genel ağları üzerinden taşır. Yöntemleri yer toosecurely hello IOT cihazları sağlamak kendilerini toobe gerekir. Aygıt, toonetwork, toocloud arka uç her katman güçlü güvenlik çıkışların gerekir.

IOT en iyi yöntemler hello yolu aşağıdaki kategorilere ayrılabilir:

* IOT donanım üreticisi veya Tümleştirici
* IOT Çözüm geliştiricisi
* IOT çözüm dağıtıcı
* IOT çözüm işleci

Bu makalede özetlenmektedir [Internet, şeyler en iyi güvenlik uygulamaları](../iot-suite/iot-security-best-practices.md). Daha ayrıntılı bilgi için lütfen toothat makalesine bakın.

## <a name="iot-hardware-manufacturer-or-integrator"></a>IOT donanım üreticisi veya Tümleştirici
Bir IOT donanım üreticisine veya donanım Tümleştirici varsa hello aşağıdaki en iyi uygulamaları izleyin:

* **Kapsam donanım toominimum gereksinimleri**: hello donanım tasarımı hello donanım ve hiçbir şey daha fazla işlem için gereken en düşük özellikleri içermelidir. 
* **Kanıt değiştirmesine donanım olun**: mekanizmaları toodetect fiziksel hello aygıt, vb. parçası kaldırma hello aygıt Kapak açma gibi donanım, izinsiz olarak oluşturun. 
* **Güvenli donanım yapı**: varsa [SMM](https://en.wikipedia.org/wiki/Cost_of_goods_sold) izin, güvenli ve şifrelenmiş depolama ve Güvenilir Platform Modülü TPM tabanlı önyükleme işlevleri gibi güvenlik özellikleri yapı.
* **Yükseltmeler güvenli hale**: hello aygıt ömrü boyunca bellenimi yükseltmek kaçınılmaz.

## <a name="iot-solution-developer"></a>IOT Çözüm geliştiricisi
Bir IOT çözüm geliştirici iseniz hello aşağıdaki en iyi uygulamaları izleyin:

* **Güvenli yazılım geliştirme metodolojisini izleyin**: Güvenli yazılım geliştirme başından başlayarak yukarı hello projesinin hello başlangıcından güvenliği hakkında tüm hello yolu tooits uygulaması, test ve dağıtım düşünüyorum gerektirir.
* **Açık kaynak yazılımının dikkatle seçin**: açık kaynak yazılımının fırsatı sağlar tooquickly çözümleri geliştirin.
* **Dikkatli tümleştirmek**: hello yazılım güvenlik açıkları çoğunu kitaplıklarını ve API'lerini hello sınırında mevcut. 

## <a name="iot-solution-deployer"></a>IOT çözüm dağıtıcı
Bir IOT çözüm dağıtıcı varsa hello aşağıdaki en iyi uygulamaları izleyin:

* **Donanım güvenli bir şekilde dağıtmak**: IOT dağıtımları ortak alanları ya da Denetimsiz yerel ayarlara olduğu gibi güvenli olmayan konumlarda dağıtılan donanım toobe gerektirebilir.
* **Kimlik doğrulama anahtarlarını güvenli kalmasına**: dağıtım sırasında her aygıt cihaz kimlikleri gerektirir ve hello bulut hizmeti tarafından oluşturulan kimlik doğrulaması anahtarlarla ilişkili. Bu anahtarları bile hello dağıtımdan sonra fiziksel olarak güvenli tutun. Güvenliği aşılmış bir tuşa mevcut bir cihazın kötü amaçlı aygıt toomasquerade tarafından kullanılabilir.

## <a name="iot-solution-operator"></a>IOT çözüm işleci
Bir IOT çözüm işleç varsa hello aşağıdaki en iyi uygulamaları izleyin:

* **Toodate sistemi tutmak**: cihaz işletim sistemleri ve tüm aygıt sürücülerini güncelleştirilmiş toohello en son sürümleri olduğundan emin olun. 
* **Kötü amaçlı etkinliği karşı koruma**: hello işletim sistemi izin veriliyorsa, her cihaz işletim sisteminde hello son virüsten koruma ve kötü amaçlı yazılımdan özellikleri yerleştirin. 
* **Sık denetim**: güvenlik sorunları olduğunda anahtar toosecurity olaylara yanıt ilgili IOT altyapı denetleme.
* **Fiziksel olarak hello IOT altyapısını koruma**: hello güvenlik saldırılarına karşı IOT altyapı başlatılan fiziksel erişimi toodevices kullanarak en kötü.
* **Bulut kimlik bilgileri korumaya**: Bulut kimlik doğrulaması kimlik bilgilerini yapılandırmak ve bir IOT dağıtım işletim için kullanılan büyük olasılıkla hello en kolay yolu toogain erişimi olan ve bir IOT sistemden. 

