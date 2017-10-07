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
ms.openlocfilehash: 513a90d144e7ade9c21cd7f3b718578989702c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-runbook-worker-a-runbook-job-terminates-with-a-status-of-suspended"></a>Karma Runbook Çalışanı: Runbook işi Askıya Alındı durumuyla sonlandırılıyor.
## <a name="summary"></a>Özet
Kısa süre içinde tooexecute denemeden sonra runbook askıya, üç kez. Başarıyla tamamlanmasını hello runbook kesme koşullar vardır ve hello ilgili hata iletisi nedenini gösteren ek bilgiler içermez. Bu makalede sorunları ilgili toohello karma Runbook çalışanı runbook yürütme hataları için sorun giderme adımları sağlar.

Bu makalede Azure sorunu ele alınmamışsa ziyaret üzerinde Azure forumları hello [MSDN ve yığın taşması hello](https://azure.microsoft.com/support/forums/). Bu forumlar sorununuzu nakledebilirsiniz veya çok[ @AzureSupport Twitter'da](https://twitter.com/AzureSupport). Ayrıca, size bir Azure destek isteği seçerek dosya **alma desteği** hello üzerinde [Azure Destek](https://azure.microsoft.com/support/options/) site.

## <a name="symptom"></a>Belirti
Runbook yürütme başarısız olur ve hello hata döndürdü, "Merhaba işlem beklenmedik şekilde durdurulduğundan hello iş eylemi 'Etkinleştir', çalıştırılamaz. Merhaba iş eylemi 3 kez denendi."

## <a name="cause"></a>Nedeni
Hello hatanın birkaç olası nedenleri şunlardır: 

1. bir proxy veya güvenlik duvarı arkasında Hello karma çalışanı olan
2. Merhaba bilgisayar hello karma çalışanı daha az üzerinde çalıştığı hello en düşük donanım daha [gereksinimleri](automation-hybrid-runbook-worker.md#hybrid-runbook-worker-requirements) 
3. Merhaba runbook'lar yerel kaynakları ile kimlik doğrulaması yapamaz

## <a name="cause-1-hybrid-runbook-worker-is-behind-proxy-or-firewall"></a>: 1 karma Runbook çalışanı proxy veya güvenlik duvarının arkasındaysa nedeni
hello bilgisayar hello karma Runbook çalışanı üzerinde çalıştığı bir güvenlik duvarı veya proxy sunucunun arkasında olan ve giden ağ erişimi izin verilen veya doğru şekilde yapılandırılmış.

### <a name="solution"></a>Çözüm
Merhaba bilgisayarın giden erişim too*.cloudapp olduğunu doğrulayın bağlantı noktası 443, 9354 ve 30000 30199 .net. 

## <a name="cause-2-computer-has-less-than-minimum-hardware-requirements"></a>Neden 2: Bilgisayar değerinden en düşük donanım gereksinimleri vardır.
Karma Runbook çalışanı karşılamalıdır hello çalıştıran bilgisayarlar toohost atamadan önce en düşük donanım gereksinimleri hello bu özellik. Aksi takdirde, diğer arka plan işlemleri ve yürütme sırasında runbook'lar tarafından neden Çekişme hello kaynak kullanımı, bağlı olarak hello bilgisayar üzerinde kullanılan haline gelir ve runbook işi gecikmeler veya zaman aşımlarına neden. 

### <a name="solution"></a>Çözüm
İlk toorun hello karma Runbook çalışanı özelliği belirlenmiş hello bilgisayar hello en düşük donanım gereksinimlerini karşılayan onaylayın.  Destekliyorsa, CPU ve bellek kullanımı toodetermine karma Runbook çalışanı işlemlerin hello performansını ile Windows arasında herhangi bir bağıntı izleyin.  Bellek veya CPU baskısı ise, bu hello gerek tooupgrade belirtmek veya ek işlemciler ekleme veya artış bellek tooaddress kaynak performans sorunu hello ve hello hatayı giderin. Alternatif olarak, hello en düşük gereksinimlerini destekleyen ve iş yükü taleplerini artıştır gerekli belirttiğinizde ölçeklendirme farklı işlem kaynak seçin.         

## <a name="cause-3-runbooks-cannot-authenticate-with-local-resources"></a>3. neden: Runbook'lar yerel kaynakları ile kimlik doğrulaması yapamaz
### <a name="solution"></a>Çözüm
Merhaba denetleyin **Microsoft SMA** açıklama ile ilgili bir olayın olay günlüğünü *işlemi Win32 çıkış koduyla [4294967295]*.  Bu hatanın nedenini Hello larınızda kimlik doğrulaması yapılandırılmış veya hello farklı çalıştır kimlik bilgileri hello karma çalışanı grubu için belirtilen henüz değil.  Lütfen gözden [Runbook izinleri](automation-hybrid-runbook-worker.md#runbook-permissions) doğru şekilde yapılandırdığınız kimlik doğrulaması runbook'larınızın tooconfirm.  

