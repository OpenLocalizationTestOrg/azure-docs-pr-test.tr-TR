---
title: "Hassas verileri özel görüntülerinde Azure RemoteApp için hiçbir zaman depolamak | Microsoft Docs"
description: "Azure remoteapp'te özel görüntü verilerini depolamak için yönergeleri hakkında bilgi edinin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 5a19903b-15f9-49d9-9bc1-ae80f2671aa1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 75d5415d33324d957617426e75909a6c6c58b1f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a>Hiçbir zaman deposu hassas verileri özel görüntüleri
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Azure RemoteApp, kendi uygulamanızda barındırdığınızda, ilk adım özel bir görüntü oluşturmaktır. Kullanıcılarınıza, uygulamalarınızı hizmet VM örnekleri oluşturmak için özel görüntü kullanırız. Özel görüntü yalnızca uygulamaları ve SQL veritabanları, personel dosyaları ya da QuickBooks şirket dosyaları gibi özel veri dosyaları gibi kayıp olabilecek hiçbir zaman hassas verileri içermelidir. Tüm gizli verilerin başka bir Azure VM, bir dosya sunucusunda veya SQL Azure Azure RemoteApp harici bulunmalıdır. Görüntü yalnızca veri kaynağına bağlanır ve verileri sunan uygulama ana bilgisayar. Gözden geçirme [Azure RemoteApp görüntüleri için gereksinimleri](remoteapp-imagereqs.md) daha fazla bilgi için. 

Neden, hassas verileri depolamamayı anlamak için Azure RemoteApp nasıl çalıştığını anlamanız gerekir. Ne zaman bir koleksiyon oluşturulur veya güncelleştirilir, arka planda birden çok klonlar veya görüntü kopyası oluşturulur. Tüm VM örnekleri özel görüntü tam çoğaltmalarının; yine de uygun istiyor musunuz? Kullanıcıların uygulamaları başlattığında bunlar bu VM örnekleri birine bağlanır. Ancak aynı örneğini garanti edilmez ve kalıcı olmayan olduklarından önemli değil. Uygulamaları barındıran VM örnekleri kalıcı değildir ve yok veya silinebilir tabanlı, örneğin, koleksiyon güncelleştirme sırasında. 

Koleksiyon sağlanan ve kullanıcıların Başlat Vm'lere bağlanması sonra kullanıcı verilerini kalıcı olan ve sizi arayarak bir VHD içinde ayrı bir depolama üzerinde kaydedildiğinden korumalı bir [kullanıcı profili diski (UPD)](remoteapp-upd.md), c:\users kullanıcı profilinde olduğu\<USERPROFILE >. Bir uygulama başlatıldığında UPD bağlanır ve yalnızca yerel kullanıcı profili gibi işletim sistemi tarafından kabul edilir. Nasıl hakkında daha fazla bilgiyi [Azure RemoteApp kullanıcı verilerini ve ayarlarını kaydeder](remoteapp-upd.md).

Görüntüde yer almalıdır. değil örnek verileri:

* Paylaşılan veri erişmeleri kullanıcılara
* SQL DB ya da QuickBooks DB
* D:\ içinde herhangi bir veri

Tüm kullanıcıların UPD kopyalanacak varsayılan profili bulunabilir örnek verileri:

* Kullanıcı başına yapılandırma dosyaları
* Kendi UPD korunur kullanıcılar gerekir komut dosyaları

Önemli noktaları:

* Görüntüde oluşturulurken özel bir görüntü kaybedilen hiçbir zaman deposu hassas veriler.
* Hassas verileri her zaman ayrı bir dosya sunucusunda, ayrı Azure VM, Bulut ve her zaman dış uygulamalarınızı Azure RemoteApp içinde barındırma VM örnekleri yer almalıdır. 
* Kullanıcı verileri kaydedilir ve kullanıcı profili diski (UPD) devam ettirir

