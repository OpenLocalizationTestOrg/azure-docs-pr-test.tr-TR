---
title: "Karma Runbook çalışanı: Bir runbook işi askıya alındı durumu ile sona erer. | Microsoft Docs"
description: "Belirtiler nedenleri ve çözümlemeleri için karma Runbook çalışanı iş sonlandırma hatası."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 02c6606e-8924-4328-a196-45630c2255e9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2016
ms.author: magoedte
ms.openlocfilehash: 7c6365b729d73f1c5b9bc57952b1723255d9e9f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="hybrid-runbook-worker-a-runbook-job-terminates-with-a-status-of-suspended"></a>Karma Runbook Çalışanı: Runbook işi Askıya Alındı durumuyla sonlandırılıyor.
## <a name="summary"></a>Özet
Runbook'unuzda üç kez yürütmek kısa bir süre içinde çalışırken askıya alınır. Runbook başarıyla tamamlanmasını kesintiye koşullar vardır ve ilgili hata iletisi nedenini gösteren ek bilgiler içermez. Bu makalede, karma Runbook çalışanı runbook yürütme hataları ile ilgili sorunları için sorun giderme adımları sağlar.

Bu makalede Azure sorunu ele alınmamışsa Azure forumları ziyaret [MSDN ve yığın taşması](https://azure.microsoft.com/support/forums/). Bu forumları veya çok sorununuzu nakledebilirsiniz [ @AzureSupport Twitter'da](https://twitter.com/AzureSupport). Ayrıca, size bir Azure destek isteği seçerek dosya **alma desteği** üzerinde [Azure Destek](https://azure.microsoft.com/support/options/) site.

## <a name="symptom"></a>Belirti
Runbook yürütme başarısız olur ve döndürülen hata, "iş işlem beklenmedik şekilde durdurulduğundan 'Etkinleştir' çalıştırılamıyor eylemi. İş eylemi 3 kez denendi."

## <a name="cause"></a>Nedeni
Hatanın birkaç olası nedenleri şunlardır: 

1. Karma çalışanı bir proxy veya güvenlik duvarı arkasında olduğunu
2. Karma çalışanı üzerinde çalıştığı bilgisayar en düşük donanım daha azı [gereksinimleri](automation-hybrid-runbook-worker.md#hybrid-runbook-worker-requirements) 
3. Runbook'lar yerel kaynakları ile kimlik doğrulaması yapamaz

## <a name="cause-1-hybrid-runbook-worker-is-behind-proxy-or-firewall"></a>: 1 karma Runbook çalışanı proxy veya güvenlik duvarının arkasındaysa nedeni
Karma Runbook çalışanı üzerinde çalıştığı bilgisayar güvenlik duvarı veya proxy sunucunun arkasında olduğu ve giden ağ erişimi izin verilen veya doğru şekilde yapılandırılmış.

### <a name="solution"></a>Çözüm
Bilgisayarın giden erişimi olduğunu doğrulayın *. bağlantı noktası 443, 9354 ve 30000 30199 üzerinde cloudapp.net. 

## <a name="cause-2-computer-has-less-than-minimum-hardware-requirements"></a>Neden 2: Bilgisayar değerinden en düşük donanım gereksinimleri vardır.
Karma Runbook çalışanı çalıştıran bilgisayarlar, bu özellik barındırmak için atamadan önce en düşük donanım gereksinimlerini karşılamalıdır. Aksi halde, kaynak kullanımı diğer arka plan işlemleri ve yürütme sırasında runbook'lar tarafından neden Çekişme bağlı olarak bilgisayar üzerinde kullanılan haline gelir ve runbook işi gecikmeler veya zaman aşımları neden. 

### <a name="solution"></a>Çözüm
İlk karma Runbook çalışanı özelliği yürütmek için atanan bilgisayarın en düşük donanım gereksinimlerini karşıladığını onaylayın.  Aşması durumunda, karma Runbook çalışanı işlemlerinin performansını ile Windows arasında herhangi bir bağıntı belirlemek için CPU ve bellek kullanımını izleyin.  Bellek veya CPU baskısı ise, bu yükseltme veya ek işlemciler ekleme ya da kaynak sorununu giderin ve hatayı gidermek için bellek artırmak için gereken gösteriyor olabilir. Alternatif olarak, iş yükü taleplerini artıştır gerekli belirttiğinizde, ölçek ve en düşük gereksinimleri destekleyebilen farklı işlem kaynak seçin.         

## <a name="cause-3-runbooks-cannot-authenticate-with-local-resources"></a>3. neden: Runbook'lar yerel kaynakları ile kimlik doğrulaması yapamaz
### <a name="solution"></a>Çözüm
Denetleme **Microsoft SMA** açıklama ile ilgili bir olayın olay günlüğünü *işlemi Win32 çıkış koduyla [4294967295]*.  Bu hatanın nedenini larınızda kimlik doğrulaması yapılandırılmış veya belirtilen karma çalışanı grubu için farklı çalıştır kimlik bilgileri henüz ' dir.  Lütfen gözden [Runbook izinleri](automation-hybrid-runbook-worker.md#runbook-permissions) doğru şekilde yapılandırdığınız kimlik doğrulaması runbook'larınızın onaylamak için.  

