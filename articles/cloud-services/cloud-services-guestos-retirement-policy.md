---
title: "Azure konuk işletim sistemi için aaaSupportability ve kullanımdan kaldırma İlkesi Kılavuzu | Microsoft Docs"
description: "Microsoft Azure konuk işletim sistemi bulut Hizmetleri tarafından kullanılan toohello göre destekleyecek hakkında bilgi sağlar."
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 919dd781-4dc6-4e50-bda8-9632966c5458
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/26/2017
ms.author: raiye
ms.openlocfilehash: 6a86c42ac95d12bbf116d900b7afb26fc3fe34e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-guest-os-supportability-and-retirement-policy"></a>Azure konuk işletim sistemi desteklenebilirlik ve kullanımdan kaldırma İlkesi
Bu sayfada Hello bilgileri ilişkili toohello Azure konuk işletim sistemi ([konuk işletim sistemi](cloud-services-guestos-update-matrix.md)) bulut Hizmetleri worker ve web rolleri (PaaS). TooVirtual makineler (Iaas) uygulanmaz.

Microsoft olan bir yayımlanan [hello konuk işletim sistemi için destek ilkesi](http://support.microsoft.com/gp/azure-cloud-lifecycle-faq). okumakta olduğunuz hello sayfası artık hello İlkesi nasıl uygulandığı açıklanmaktadır.

Hello İlkesi

1. Microsoft destekleneceğini **en az, en son iki hello konuk işletim sistemi aileleri hello**. Bir aile devre dışı bırakıldığında, müşterilerin hello resmi sona erme tarihi tooupdate tooa yeni desteklenen konuk işletim sistemi ailesi 12 ay sahip.
2. Microsoft destekleneceğini **en az, en son iki sürüm hello desteklenen konuk işletim sistemi ailelerinin hello**.
3. Microsoft destekleneceğini **en az, en son iki sürümü hello Azure SDK'sı hello**. SDK Çekildi hello sürümü, müşterilerin hello resmi sona erme tarihi tooupdate tooa daha yeni sürüm 12 ay olur.

Bazen, birden çok iki ailesi ya da sürümlerden desteklenmiyor olabilir. Resmi konuk işletim sistemi destek bilgileri hello üzerinde görünür [Azure konuk işletim sistemi sürümleri ve SDK uyumluluk matrisi](cloud-services-guestos-update-matrix.md).

## <a name="when-a-guest-os-family-or-version-is-retired"></a>Bir konuk işletim sistemi ailesi veya sürüm ne zaman devre dışı bırakıldı
Yeni bir konuk işletim sistemi **ailesi** hello Windows Server işletim sisteminin yeni bir resmi sürüm süre hello yayımlandıktan sonra sunulmuştur. Yeni bir konuk işletim sistemi ailesi sunulan olduğunda, Microsoft hello eski konuk işletim sistemi ailesi devre dışı bırakma.

Yeni konuk işletim sistemi **sürümleri** her ay tooincorporate hello son MSRC ilgili güncelleştirmeler sunulmuştur. Merhaba normal aylık nedeniyle, bir konuk işletim sistemi sürümü normalde devre dışı 60 gün sonra yayınlandığı güncelleştirmesidir. Bu etkinlik kullanılabilir her ailesi için en az iki konuk işletim sistemi sürümleri tutar.

### <a name="process-during-a-guest-os-family-retirement"></a>İşlem sırasında bir konuk işletim sistemi ailesi devre dışı bırakma
Merhaba devre dışı bırakma duyurdu sonra müşterilerin hello eski ailesi resmi olarak hizmetinden kaldırılmadan önce bir 12 ay "geçiş" süresine sahip. Bu geçiş süresi, Microsoft hello kümeleri genişletilmiş. Güncelleştirmeleri üzerinde hello gönderilecektir [Azure konuk işletim sistemi sürümleri ve SDK uyumluluk matrisi](cloud-services-guestos-update-matrix.md).

Aşamalı devre dışı bırakma işlemi altı (6) ay hello geçiş dilimine başlar. Bu süre boyunca:

1. Microsoft, müşterilerinin hello devre dışı bırakma size bildirir.
2. hello Azure SDK'ın daha yeni sürümü Hello Çekildi hello konuk işletim sistemi ailesi Destek olmaz.
3. Yeni dağıtımları ve bulut Hizmetleri redeployments Çekildi hello ailesinde izin verilmiyor

Microsoft hello hello geçiş süresi, hello "sona erme tarihi" bilinen son gününü kadar hello son MSRC güncelleştirmeleri ekleme toointroduce yeni konuk işletim sistemi sürümü devam edecektir. Merhaba sona erme tarihini, bulut hala çalışan hizmetleri hello Azure SLA altında desteklenmeyen. Microsoft, yükseltme, silin veya bu tarihten sonra bu hizmetleri durdurun hello tedbirli tooforce sahiptir.

### <a name="process-during-a-guest-os-version-retirement"></a>İşlem sırasında bir konuk işletim sistemi sürümü devre dışı bırakma
Müşteriler, konuk işletim sistemi tooautomatically güncelleştirme ayarlarsanız, hiçbir zaman tooworry konuk işletim sistemi sürümleri yapılacağı hakkında sahiptirler. Bunlar her zaman hello son konuk işletim sistemi sürümünü kullanacak.

Konuk işletim sistemi sürümleri her ayda bir yayınlanır. Nedeniyle Hello oranı normal sürümlerin her sürümü sabit bir kullanım ömrü vardır.

Merhaba kullanım ömrü içine 60 günde bir sürümüdür "*devre dışı*". "Devre dışı" Merhaba sürümünün hello Portal'dan kaldırılan anlamına gelir. Merhaba sürümü artık hello CSCFG yapılandırma dosyasından ayarlayabilirsiniz. Var olan dağıtımlar çalıştıran bırakılır. Ancak yeni dağıtımları ve kod ve yapılandırma güncelleştirmeleri tooexisting dağıtımları değil izin verilecek.

Bir süre sonra "devre dışı olma", konuk işletim sistemi sürümü hello "*süresi*" ve hala bu sürümünü çalıştıran herhangi bir yüklemesi yükseltilmiş ve tooautomatically güncelleştirme hello konuk işletim sistemi hello gelecekteki ayarlayın zorla. Merhaba süreyi disablement tooexpiration değişebilir şekilde sona erme toplu olarak gerçekleştirilir.

Bu nokta Microsoft'un tedbirli tooease müşteri geçişleri uzun yapılabilir. Herhangi bir değişiklik hello üzerinde duyurulacaktır [Azure konuk işletim sistemi sürümleri ve SDK uyumluluk matrisi](cloud-services-guestos-update-matrix.md).

### <a name="notifications-during-retirement"></a>Devre dışı bırakma sırasında bildirimleri
* **Aile devre dışı bırakma** <br>Microsoft, blog gönderileri ve portal bildirim kullanır. Devre dışı bırakılan bir konuk işletim sistemi ailesi hala kullanan müşteriler (e-posta, portal iletileri, telefon araması) doğrudan iletişim tooassigned hizmet yöneticileri bildirilir. Tüm değişiklikleri hello bu sayfanın başında listelenen toothis sayfası ve hello RSS akışı nakledilir.
* **Sürüm devre dışı bırakma** <br>Tüm değişiklikleri ve bunlar ortaya hello tarihleri hello sürüm, devre dışı bırakıldı ve sona erme dahil olmak üzere, bu sayfanın başında listelenen toothis sayfası ve hello RSS akışı nakledilir. Devre dışı konuk işletim sistemi sürümü veya ailesi üzerinde çalışan dağıtımları varsa Hizmetleri Yöneticiler e-postaları alır. Bu e-postaları Hello zamanlamasını farklılık gösterebilir. Bu zamanlama resmi bir SLA olmasa da genellikle en az bir ay disablement önce oldukları.

## <a name="frequently-asked-questions"></a>Sık sorulan sorular
**Merhaba etkileri geçiş işleminin nasıl en aza indirebileceğiniz?**

Bulut Hizmetleri Tasarlama için en son konuk işletim sistemi ailesi kullanmanızı öneririz.

1. Geçiş tooa daha yeni ailenize erken planlama başlatın.
2. Geçici test dağıtımları tootest hello yeni ailesi üzerinde çalışan bulut hizmetiniz ayarlayın.
3. Konuk işletim sistemi sürümünüz çok ayarlamak**otomatik** (osVersion = * hello içinde [.cscfg](cloud-services-model-and-package.md#cscfg) dosyası) hello geçiş toonew konuk işletim sistemi sürümleri oluşmaz otomatik olarak.

**Ne web Uygulamam hello işletim sistemi ile daha derin tümleştirme gerektiriyor?**

Web uygulama Mimarinizi hello işletim sisteminin temel özelliklerine bağlıdır, desteklenen platform özelliklerini gibi kullandığınız [başlangıç görevleri](cloud-services-startup-tasks.md) veya diğer genişletilebilirlik mekanizması. Alternatif olarak, ayrıca kullanabileceğiniz [Azure sanal makineleri](https://azure.microsoft.com/documentation/scenarios/virtual-machines/) (Iaas – hizmet olarak altyapı), işletim sistemi temelindeki hello bakımından sorumlu olduğu.

## <a name="next-steps"></a>Sonraki adımlar
Gözden geçirme hello son [konuk işletim sistemi sürümleri](cloud-services-guestos-update-matrix.md).
