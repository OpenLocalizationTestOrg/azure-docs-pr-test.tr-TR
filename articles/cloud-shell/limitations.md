---
title: "aaaAzure bulut Kabuğu (Önizleme) kısıtlamaları | Microsoft Docs"
description: "Azure bulut Kabuk sınırlamaları genel bakış"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 8462b0b9850fcde790a386433009439bbab52c0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-cloud-shell"></a>Azure bulut Kabuk sınırlamaları
Azure bulut Kabuk hello aşağıdaki bilinen sınırlamalara sahiptir:

## <a name="system-state-and-persistence"></a>Sistem durumu ve sürdürme
Bulut Kabuk oturumunuz sağlar hello makine geçicidir ve oturumunuz için 20 dakika etkin değil sonra geri dönüştürüldüğünde. Bulut Kabuk takılı bir dosya paylaşımı toobe gerektirir. Sonuç olarak, aboneliğiniz depolama kaynakları tooaccess bulut Kabuk yukarı mümkün tooset olması gerekir. Diğer konular şunlardır:
* Takılı depolamayla yalnızca değişiklikleri içinde `$Home` dizin veya `clouddrive` dizin kaldı.
* Dosya paylaşımları takılı yalnızca içinden, [bölgeye atanan](persisting-shell-storage.md#mount-a-new-clouddrive).
* Azure dosyaları yalnızca yerel olarak yedekli depolama ve coğrafi olarak yedekli depolama hesaplarını destekler.

## <a name="user-permissions"></a>Kullanıcı izinleri
İzinler, sudo erişimi olmadan normal kullanıcı olarak ayarlanır. Dışında herhangi bir yüklemesi, `$Home` dizin kalıcı olarak tutmayacaktır.
İçinde bazı komutlar hello rağmen `clouddrive` gibi dizin `git clone`, uygun izinlere sahip değilsiniz, `$Home` dizin izinlere sahiptir.

## <a name="browser-support"></a>Tarayıcı desteği
Bulut Kabuğu'nu Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox ve Apple Safari hello en son sürümlerini destekler. Safari özel modunda desteklenmiyor.

## <a name="copy-and-paste"></a>Kopyala ve Yapıştır
CTRL + C ve Ctrl + V kopyalayıp kısayolları bulut Kabuğu'nda Windows makinelerde yapıştırın, Ctrl + INSERT ve üst karakter + INSERT toocopy kullanın ve sırasıyla yapıştırmak gibi çalışmaz.

Sağ tıklama Kopyala ve Yapıştır seçeneklerini de kullanılabilir, ancak konu toobrowser özgü Pano erişim sağ işlevdir.

## <a name="editing-bashrc"></a>.Bashrc düzenleme
Bunun yapılması .bashrc düzenleme beklenmeyen hatalara bulut Kabuğu'nda neden olabilir. uyarı alın.

## <a name="bashhistory"></a>.bash_history
Geçmişinizi bash komutların bulut Kabuk oturum kesintisi veya eşzamanlı oturum nedeniyle tutarsız olabilir.

## <a name="usage-limits"></a>Kullanım sınırları
Bulut Kabuk etkileşimli kullanım durumları için tasarlanmıştır. Sonuç olarak, tüm uzun süre çalışan etkileşimli olmayan oturumlar uyarmadan sonlandırılır.

## <a name="network-connectivity"></a>Ağ bağlantısı
Bulut Kabuğu'ndaki tüm gecikme konu toolocal internet bağlantısı, bulut Kabuk tooattempt toocarry gönderilen yönergeleri çıkışı devam eder.

## <a name="next-steps"></a>Sonraki adımlar
[Bulut Kabuk hızlı başlangıç](quickstart.md)
