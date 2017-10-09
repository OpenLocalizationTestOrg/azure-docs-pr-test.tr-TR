---
title: "Azure RemoteApp için özel görüntülerinde aaaNever deposu hassas verileri | Microsoft Docs"
description: "Azure remoteapp'te özel görüntü verilerini depolamak için hello yönergeleri hakkında bilgi edinin"
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
ms.openlocfilehash: 86a0fea218f8826d6d25f50d3c4c36e368e26fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a>Hiçbir zaman deposu hassas verileri özel görüntüleri
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Azure RemoteApp, kendi uygulamanızda barındırdığınızda hello ilk toocreate özel bir görüntü adımdır. Uygulamalarınızı tooyour kullanıcılar hizmet bu özel görüntü toocreate VM örnekleri kullanırız. Merhaba özel görüntü yalnızca uygulamaları ve SQL veritabanları, personel dosyaları ya da QuickBooks şirket dosyaları gibi özel veri dosyaları gibi kayıp olabilecek hiçbir zaman hassas verileri içermelidir. Tüm gizli veriler dış tooAzure RemoteApp başka bir Azure VM, bir dosya sunucusunda veya SQL Azure bulunmalıdır. Merhaba görüntü toohello veri kaynağına bağlanan ve hello verileri sunan yalnızca konak Merhaba uygulaması gerekir. Gözden geçirme [Azure RemoteApp görüntüleri için gereksinimleri](remoteapp-imagereqs.md) daha fazla bilgi için. 

neden değil depoladığınız hassas verileri toounderstand Azure RemoteApp nasıl çalıştığını toounderstand gerekir. Bir koleksiyonu oluşturulmuş veya güncelleştirilmiş hello arka planda birden çok klonlar veya hello görüntü kopyası oluşturulur. Tüm VM örnekleri hello özel görüntü tam çoğaltmalarının; yine de uygun istiyor musunuz? Kullanıcıların uygulamaları başlattığınızda bu VM örnekleri bağlı tooone oldukları. Ancak hello aynı örneği garanti edilmez ve kalıcı olmayan olduklarından önemli değil. Örneğin, koleksiyon güncelleştirme sırasında temel yok veya silinmiş barındırma hello uygulamaları kalıcı olmayan ve olabilir VM örnekleri hello. 

Merhaba koleksiyonu hazırlanır ve kullanıcıların başlangıç bağlantı toohello VM'ler sonra kullanıcı verilerini kalıcı olan ve sizi arayarak bir VHD içinde ayrı bir depolama üzerinde kaydedildiğinden korumalı bir [kullanıcı profili diski (UPD)](remoteapp-upd.md), hello kullanıcı profili olduğu c:\users içinde\<USERPROFILE >. Bir uygulama başlatıldığında hello UPD bağlanır ve yalnızca yerel kullanıcı profili gibi hello işletim sistemi tarafından kabul edilir. Nasıl hakkında daha fazla bilgiyi [Azure RemoteApp kullanıcı verilerini ve ayarlarını kaydeder](remoteapp-upd.md).

Merhaba görüntüde bulunmalıdır değil örnek verileri:

* Kullanıcıların tooaccess için paylaşılan veri
* SQL DB ya da QuickBooks DB
* D:\ içinde herhangi bir veri

Tüm kullanıcıların UPD kopyalanan hello varsayılan profili toobe bulunabilir örnek verileri:

* Kullanıcı başına yapılandırma dosyaları
* Kendi UPD korunur kullanıcılar gerekir komut dosyaları

Önemli noktaları:

* Hiçbir zaman hello görüntüyü özel görüntü oluşturulurken kayıp hassas verileri depolar.
* Hassas verileri her zaman ayrı bir dosya sunucusunda bulunan, hello Bulut ve uygulamalarınızı Azure RemoteApp içinde barındıran her zaman dış toohello VM örneklerinin Azure VM ayırın. 
* Kullanıcı verileri kaydedilir ve hello kullanıcı profili diski (UPD) devam ettirir

