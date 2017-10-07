---
title: "en iyi güvenlik uygulamalarını, aaaIoT | Microsoft Docs"
description: "IOT altyapınızın güvenliğini sağlamaya yönelik en iyi güvenlik uygulamaları"
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 24e7bda2-5f7b-44e3-b8af-761abd3276ff
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: yurid
ms.openlocfilehash: 3a546c67978a519446ab6c83917a0789675f1b52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-best-practices"></a>En iyi güvenlik uygulamalarını, nesnelerin interneti
bir nesnelerin interneti (IOT) altyapısı toosecure sıkı güvenlik derinlemesine stratejisi gerektirir. Bu strateji toosecure veri hello bulutta gerektirir, aktarım sırasında veri bütünlüğü koruma üzerinde genel internet hello ve güvenli bir şekilde cihazları'ni sağlayın. Her katman hello büyük güvenlik güvence derlemeler genel altyapı.

## <a name="secure-an-iot-infrastructure"></a>Güvenli bir IOT altyapı
Bu güvenlik derinlemesine strateji geliştirilmiş ve etkin bir katılım hello üretim, geliştirme ve IOT cihazları ve altyapı dağıtımı ile ilgili çeşitli Yürütücü ile yürütüldü. Bu oynatıcıları üst düzey bir açıklaması verilmiştir.  

* **IOT donanım üreticisinin/Tümleştirici**: IOT donanım çeşitli üreticileri ya da donanım üretilen bir IOT dağıtım için sağlama Üreticiler donanım atayarak tümleştiricileri dağıtılan hello üreticileri genellikle, bunlar veya başka üreticiler tarafından tümleşik.
* **IOT çözüm geliştirici**: hello geliştirme IOT çözümünün genellikle bir çözüm geliştirici tarafından yapılır. Bu Geliştirici parçası bir şirket içi team ya da bu etkinlikte uzmanlaşmış bir sistem Tümleştirici (SI). Merhaba IOT çözüm geliştirici hello IOT çözüm baştan çeşitli bileşenleri geliştirmek, çeşitli piyasada veya açık kaynak bileşenlerini tümleştirmek veya ikincil uyarlama önceden yapılandırılmış çözümlerle benimsemeyi.
* **IOT çözüm dağıtıcı**: sonra bir IOT çözüm geliştirilmiş, hello alanında dağıtılan toobe gerekiyor. Bu donanım, cihaz bağlantısı ve donanım aygıtları veya hello bulut çözümlerinde dağıtımını dağıtımını içerir.
* **IOT çözüm işleci**: Merhaba IOT çözüm dağıtıldıktan sonra izleme, yükseltme ve Bakım uzun vadeli işlemleri gerektirir. Bu bilgi teknolojisi uzmanları, donanım işlemler ve Bakım ekipleri ve hello doğru genel IOT altyapı davranışını izlemek etki alanı uzmanlarıyla oluşur bir şirket içi ekibi tarafından yapılabilir.

izleyin hello bölümler her bu oynatıcıları toohelp için en iyi uygulamaları geliştirmek, dağıtmak ve güvenli bir IOT altyapısı işletmek sağlar.

## <a name="iot-hardware-manufacturerintegrator"></a>IOT donanım üreticisinin/Tümleştirici
Merhaba, hello IOT donanım üreticileri ve donanım tümleştiricileri için en iyi yöntemler verilmiştir.

* **Kapsam donanım toominimum gereksinimleri**: hello donanım tasarımı hello donanım ve hiçbir şey daha fazla işlemi için gereken en düşük özellikleri hello içermelidir. Tooinclude USB bağlantı noktalarına yalnızca gerekirse hello işlemi hello cihazın örneğidir. Bu ek özellikler hello aygıt kaçınılmalıdır istenmeyen saldırı vektörlerinin için açın.
* **Kanıt değiştirmesine donanım olun**: mekanizmaları toodetect fiziksel, hello aygıt yüzünde açma veya hello aygıt parçası kaldırma gibi izinsiz olarak oluşturun. Bunlar sinyalleri değiştirmesine işleçleri bu olayların uyarı hello verileri karşıya akış toohello bulut, parçası olabilir.
* **Güvenli donanım yapı**: varsa SMM izin verir, güvenli ve şifrelenmiş depolama alanı gibi güvenlik özellikleri oluşturmak ya da önyükleme Güvenilir Platform Modülü (TPM) üzerinde temel işlevselliği. Daha güvenli ve korumaya yardımcı olmak bu özellikleri yapma cihazların genel IOT altyapı hello.
* **Yükseltmeler güvenli hale**: hello aygıt hello ömrü sırasında bellenim yükseltmeleri kaçınılmaz. Güvenli yolları aygıtlarla yükseltmeler ve şifreleme güvence bellenim sürümleri oluşturma hello aygıt toobe güvenli sırasında ve yükseltildikten sonra izin verir.

## <a name="iot-solution-developer"></a>IOT Çözüm geliştiricisi
Merhaba, hello IOT çözüm geliştiriciler için en iyi yöntemler şunlardır:

* **Güvenli yazılım geliştirme metodolojisini izleyin**: Güvenli yazılım geliştirme başından başlayarak yukarı hello projesinin hello başlangıcından güvenliği ile ilgili tüm hello yolu tooits uygulaması, test ve dağıtım düşünüyorum gerektirir. Platform, dil ve araçları Hello seçimleri tüm bu yöntemleri ile etkilenir. Merhaba Microsoft güvenlik geliştirme yaşam döngüsü, bir adım adım bir yaklaşım toobuilding güvenli yazılım sağlar.
* **Açık kaynaklı yazılım dikkatle seçin**: açık kaynaklı yazılım fırsatı sağlar tooquickly çözümleri geliştirin. Açık kaynaklı yazılım seçerken her bir açık kaynak bileşenin hello topluluk hello etkinlik düzeyini göz önünde bulundurun. Etkin bir topluluk yazılım desteklenir ve sorunları bulunan ve ele sağlar. Alternatif olarak, bir belirsiz ve etkin olmayan açık kaynaklı yazılım desteklenmiyor ve sorun büyük olasılıkla bulunacaktır.
* **Dikkatli tümleştirmek**: kitaplıklarını ve API'lerini hello sınırında birçok yazılım güvenlik açıkları vardır. Merhaba geçerli dağıtım için gerekli olmayabilir işlevselliği hala bir API katmanı kullanılabilir. tooensure genel güvenlik güvenlik açıkları için tümleştirilmiş bileşenlerinin tüm arabirimler toocheck emin olun.      

## <a name="iot-solution-deployer"></a>IOT çözüm dağıtıcı
Merhaba, IOT çözüm dağıtımcılar için en iyi yöntemler şunlardır:

* **Donanım güvenli bir şekilde dağıtmak**: IOT dağıtımları ortak alanları ya da Denetimsiz yerel ayarlara olduğu gibi güvenli olmayan konumlarda dağıtılan donanım toobe gerektirebilir. Böyle durumlarda, donanım dağıtım yetkisiz değiştirmeye karşı kanıt toohello azami ölçüde olduğundan emin olun. Merhaba donanımda USB veya diğer bağlantı noktaları varsa, bunlar güvenli bir şekilde ele emin olun. Birçok saldırı vektörüne giriş noktaları olarak kullanabilirsiniz.
* **Kimlik doğrulama anahtarlarını güvenli kalmasına**: dağıtım sırasında her aygıt cihaz kimlikleri gerektirir ve hello bulut hizmeti tarafından oluşturulan kimlik doğrulaması anahtarlarla ilişkili. Bu anahtarları bile hello dağıtımdan sonra fiziksel olarak güvenli tutun. Güvenliği aşılmış bir tuşa mevcut bir cihazın kötü amaçlı aygıt toomasquerade tarafından kullanılabilir.

## <a name="iot-solution-operator"></a>IOT çözüm işleci
Merhaba, IOT çözüm işleçleri için hello en iyi yöntemler şunlardır:

* **Toodate Hello sistemi tutmak**: cihaz işletim sistemleri ve tüm aygıt sürücülerini yükseltilmiş toohello en son sürümleri olduğundan emin olun. Windows 10 (IOT veya diğer SKU'ları) otomatik güncelleştirmeler kapatırsanız, Microsoft toodate IOT cihazları için güvenli bir işletim sistemi sağlama sürdürür. Toodate Yukarı (Linux gibi) diğer işletim sistemlerinin kalmasını sağlamaya yardımcı olur bunlar aynı zamanda kötü amaçlı saldırılara karşı korunur.
* **Kötü amaçlı etkinliği karşı koruma**: hello işletim sistemi izin veriliyorsa, hello son virüsten koruma ve kötü amaçlı yazılımdan koruma özellikleri her cihaz işletim sistemine yükleyin. Bu, en dış tehditlerin azaltılmasına yardımcı olabilir. Uygun adımları uygulayarak Çoğu modern işletim sistemi tehditlere karşı koruyabilirsiniz.
* **Sık denetim**: toosecurity olaylara yanıt verirken denetim IOT altyapı güvenlikle ilgili sorunlar için anahtarıdır. Çoğu işletim sistemi olmalıdır yerleşik olay günlüğü sık toomake hiçbir güvenlik ihlali oluştu emin gözden sağlar. Denetim bilgilerini nerede çözümlenmesi ayrı telemetri akışı toohello bulut hizmeti olarak gönderilebilir.
* **Fiziksel olarak hello IOT altyapısını koruma**: hello güvenlik saldırılarına karşı IOT altyapı başlatılan fiziksel erişimi toodevices kullanarak en kötü. Bir önemli güvenlik tooprotect USB bağlantı noktalarına ve diğer fiziksel erişim kötü niyetli kullanımına karşı bir uygulamadır. Oluşmuş olabilir bir anahtar toouncovering ihlallerinden USB bağlantı noktası kullanımı gibi fiziksel erişim günlüğü. Yeniden, Windows 10 (IOT ve diğer SKU'ları) bu olayların ayrıntılı günlük kaydını etkinleştirir.
* **Bulut kimlik bilgileri korumaya**: Bulut kimlik doğrulaması kimlik bilgilerini yapılandırmak ve bir IOT dağıtım işletim için kullanılan büyük olasılıkla hello en kolay yolu toogain erişimi olan ve bir IOT sistemden. Merhaba parola sık değiştirerek Hello kimlik bilgileri korumak ve ortak makinelerde bu kimlik bilgileri kullanılarak kullanmamalıdır.

Farklı IOT cihaz özelliklerini farklılık gösterir. Bazı aygıtlar ortak masaüstü işletim sistemlerini çalıştıran bilgisayarlar olabilir ve bazı cihazların çok hafif işletim sistemlerini çalıştıran. açıklanan hello en iyi güvenlik uygulamaları önceden değişen derece cinsinden geçerli toothese cihazlar olabilir. Sağlanırsa, ek güvenlik ve dağıtım en iyi uygulamalar, bu cihazların Merhaba üreticilerin gelmelidir.

Bazı eski ve kısıtlı cihazlar IOT dağıtımı için özellikle tasarlanmış olabilir değil. Bu cihazların Merhaba yetenek tooencrypt veri eksikliği, Internet hello ile bağlanmak veya gelişmiş denetim sağlayın. Bu durumlarda, modern ve güvenli alan ağ geçidi eski cihazlardan veri toplama ve hello Internet bu cihazlar bağlanmak için gereken hello güvenlik sağlar. Alan ağ geçitleri, güvenli kimlik doğrulaması, şifrelenmiş oturumlarının anlaşma, hello Bulut ve birçok güvenlik özelliği komutları alınmasını sağlayabilir.

## <a name="see-also"></a>Ayrıca bkz.
IOT çözümünüzün güvenliğini sağlama hakkında daha fazla toolearn bakın:

* [IOT güvenlik mimarisi][lnk-security-architecture]
* [IOT dağıtımınızın güvenliğini][lnk-security-deployment]

Merhaba bazıları diğer özellikleri ve yetenekleri hello IOT paketi önceden yapılandırılmış çözümleri ayrıca keşfedebilirsiniz:

* [Önceden yapılandırılmış Tahmine dayalı bakım çözümüne genel bakış][lnk-predictive-overview]
* [Azure IOT paketi için sık sorulan sorular][lnk-faq]

IOT hub'ı güvenlik konusunda okuyabilirsiniz [Denetim erişim tooIoT Hub] [ lnk-devguide-security] hello IOT Hub Geliştirici Kılavuzu'nda.

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md

[lnk-security-architecture]: iot-security-architecture.md
[lnk-security-deployment]: iot-suite-security-deployment.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md
