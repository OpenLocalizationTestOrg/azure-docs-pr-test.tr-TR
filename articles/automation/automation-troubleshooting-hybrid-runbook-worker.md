---
title: "Azure Otomasyon karma Runbook çalışanı aaaTroubleshoot | Microsoft Docs"
description: "Merhaba belirtiler, nedenleri ve Azure Automation'da en yaygın karma Runbook çalışanı sorunları hello çözümlenmek açıklanmaktadır."
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
ms.date: 07/25/2017
ms.author: magoedte
ms.openlocfilehash: 292af517c88d1ffd21262a286ccc079e7270bfad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-tips-for-hybrid-runbook-worker"></a>Karma Runbook çalışanı için sorun giderme ipuçları

Bu makalede Otomasyon karma Runbook çalışanları ile karşılaşabilirsiniz ve olası çözümlerini tooresolve önerir hatalarında sorun giderme yardımı sunar bunları.

## <a name="a-runbook-job-terminates-with-a-status-of-suspended"></a>Bir runbook işi askıya alındı durumu ile sona erer

Kısa süre içinde tooexecute denemeden sonra runbook askıya, üç kez. Başarıyla tamamlanmasını hello runbook kesme koşullar vardır ve hello ilgili hata iletisi nedenini gösteren ek bilgiler içermez. Bu makalede sorunları ilgili toohello karma Runbook çalışanı runbook yürütme hataları için sorun giderme adımları sağlar.

Bu makalede Azure sorunu ele alınmamışsa ziyaret üzerinde Azure forumları hello [MSDN ve yığın taşması hello](https://azure.microsoft.com/support/forums/). Bu forumlar sorununuzu nakledebilirsiniz veya çok[ @AzureSupport Twitter'da](https://twitter.com/AzureSupport). Ayrıca, size bir Azure destek isteği seçerek dosya **alma desteği** hello üzerinde [Azure Destek](https://azure.microsoft.com/support/options/) site.

### <a name="symptom"></a>Belirti
Runbook yürütme başarısız olur ve hello hata döndürdü, "Merhaba işlem beklenmedik şekilde durdurulduğundan hello iş eylemi 'Etkinleştir', çalıştırılamaz. Merhaba iş eylemi 3 kez denendi."

Hello hatanın birkaç olası nedenleri şunlardır: 

1. bir proxy veya güvenlik duvarı arkasında Hello karma çalışanı olan
2. Merhaba bilgisayar hello karma çalışanı daha az üzerinde çalıştığı hello minimum daha [donanım gereksinimleri](automation-offering-get-started.md#hybrid-runbook-worker)  
3. Merhaba runbook'lar yerel kaynakları ile kimlik doğrulaması yapamaz

#### <a name="cause-1-hybrid-runbook-worker-is-behind-proxy-or-firewall"></a>: 1 karma Runbook çalışanı proxy veya güvenlik duvarının arkasındaysa nedeni
hello bilgisayar hello karma Runbook çalışanı üzerinde çalıştığı bir güvenlik duvarı veya proxy sunucunun arkasında olan ve giden ağ erişimi izin verilen veya doğru şekilde yapılandırılmış.

#### <a name="solution"></a>Çözüm
Merhaba bilgisayarın giden erişim too*.azure-automation.net bağlantı noktası 443 üzerinde olduğunu doğrulayın. 

#### <a name="cause-2-computer-has-less-than-minimum-hardware-requirements"></a>Neden 2: Bilgisayar değerinden en düşük donanım gereksinimleri vardır.
Karma Runbook çalışanı karşılamalıdır hello çalıştıran bilgisayarlar toohost atamadan önce en düşük donanım gereksinimleri hello bu özellik. Aksi takdirde, diğer arka plan işlemleri ve yürütme sırasında runbook'lar tarafından neden Çekişme hello kaynak kullanımı, bağlı olarak hello bilgisayar üzerinde kullanılan haline gelir ve runbook işi gecikmeler veya zaman aşımlarına neden. 

#### <a name="solution"></a>Çözüm
İlk toorun hello karma Runbook çalışanı özelliği belirlenmiş hello bilgisayar hello en düşük donanım gereksinimlerini karşılayan onaylayın.  Destekliyorsa, CPU ve bellek kullanımı toodetermine karma Runbook çalışanı işlemlerin hello performansını ile Windows arasında herhangi bir bağıntı izleyin.  Bellek veya CPU baskısı ise, bu hello gerek tooupgrade belirtmek veya ek işlemciler ekleme veya artış bellek tooaddress kaynak performans sorunu hello ve hello hatayı giderin. Alternatif olarak, hello en düşük gereksinimlerini destekleyen ve iş yükü taleplerini artıştır gerekli belirttiğinizde ölçeklendirme farklı işlem kaynak seçin.         

#### <a name="cause-3-runbooks-cannot-authenticate-with-local-resources"></a>3. neden: Runbook'lar yerel kaynakları ile kimlik doğrulaması yapamaz

#### <a name="solution"></a>Çözüm
Merhaba denetleyin **Microsoft SMA** açıklama ile ilgili bir olayın olay günlüğünü *işlemi Win32 çıkış koduyla [4294967295]*.  Bu hatanın nedenini Hello larınızda kimlik doğrulaması yapılandırılmış veya hello farklı çalıştır kimlik bilgileri hello karma çalışanı grubu için belirtilen henüz değil.  Lütfen gözden [Runbook izinleri](automation-hrw-run-runbooks.md#runbook-permissions) doğru şekilde yapılandırdığınız kimlik doğrulaması runbook'larınızın tooconfirm.  

## <a name="next-steps"></a>Sonraki adımlar

Otomasyon diğer sorunlarını giderme Yardımı için bkz [Azure Automation ile ilgili genel sorunları giderme](automation-troubleshooting-automation-errors.md) 