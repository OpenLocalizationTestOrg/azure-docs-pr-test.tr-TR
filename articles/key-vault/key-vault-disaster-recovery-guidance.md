---
title: "Azure anahtar kasası etkileyen bir Azure hizmet kesintisi hello olayı içinde aaaWhat toodo | Microsoft Docs"
description: "Azure anahtar kasası etkileyen bir Azure hizmet kesintisi hello olayı içinde hangi toodo öğrenin."
services: key-vault
documentationcenter: 
author: adamglick
manager: mbaldwin
editor: 
ms.assetid: 19a9af63-3032-447b-9d1a-b0125f384edb
ms.service: key-vault
ms.workload: key-vault
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: sumedhb;aglick
ms.openlocfilehash: 88eec82ada401a28323b3eea126168185ba4cdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a>Azure anahtar kasası kullanılabilirlik ve artıklık
Azure anahtar kasası artıklık toomake hello bileşenleri tek tek hizmet başarısız olsa bile, anahtarları ve gizli anahtarları kullanılabilir tooyour uygulama kalmasını çok katmanlı özellikleri.

Merhaba anahtar kasanızı içeriğini hello bölge ve tooa ikincil bölge içinde en az 150 mil hemen ancak hello içinde çoğaltılır aynı coğrafi konum. Bu anahtarları ve gizli anahtarları, yüksek dayanıklılık tutar. Merhaba bkz [Azure bölgeleri eşleştirilmiş](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) belirli bir bölge çiftleri hakkındaki ayrıntılar için belge.

Merhaba anahtar kasası hizmetinde bileşenleri tek tek başarısız olursa, diğer bileşenleri hello bölge içinde istek toomake işlevlerin düşüşü olmadan olduğundan emin tooserve içinde adım. Tüm eylem tootrigger tootake gerekmez bu. Otomatik olarak gerçekleşir ve saydam tooyou olacaktır.

Tüm bir Azure bölgesi kullanılamıyor hello ender olayda, bu bölgedeki Azure anahtar kasası, yaptığınız hello istekleri otomatik olarak yönlendirilir (*devredilir*) tooa ikincil bölge. Merhaba birincil bölge yeniden kullanılabilir duruma geldiğinde, istekleri geri yönlendirilir (*geri başarısız*) toohello birincil bölge. Yeniden, bu otomatik olarak gerçekleşir çünkü tootake herhangi bir eylem gerekmez.

Farkında birkaç uyarılar toobe vardır:

* Bir bölge yük devretme Hello olayda onu hello hizmet toofail birkaç dakika sürebilir. Merhaba yük devretme işlemi tamamlanana kadar bu süre boyunca olan istekler başarısız olabilir.
* Bir yük devretme işlemi tamamlandıktan sonra anahtar kasanızı salt okunur modda değil. Bu modda desteklenen istekleri şunlardır:
  * Anahtar kasalarının listesi
  * Anahtar kasalarını özelliklerini alır
  * Gizli anahtarları listeleme
  * Gizli kod dizeleri alma
  * Liste anahtarları
  * Get (özelliklerini) anahtarları
  * Şifreleme
  * Şifre çözme
  * Kaydırma
  * Kaydırma
  * Doğrulama
  * Oturum
  * Backup
* Bir yük devretme geri başarısız olduktan sonra tüm istek türleri (okuma dahil olmak üzere *ve* yazma isteklerine) kullanılabilir.

