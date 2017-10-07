---
title: "aaaAzure RemoteApp görüntü gereksinimleri | Microsoft Docs"
description: "Azure RemoteApp ile kullanılan görüntüleri toobe oluşturmak için hello gereksinimleri hakkında bilgi edinin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7cbb90f4-6dc9-462c-a429-088cdb57414e
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 4e35203eb93a866d4e0bd591d42b34746c7ffa4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a>Azure RemoteApp görüntüleri için gereksinimleri
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Azure RemoteApp Kullanıcılarınızla tooshare istediğiniz tüm hello programlar Windows Server 2012 R2 görüntüsünü toohost kullanır. özel görüntü toocreate, varolan bir görüntüyle başlayabilir veya [yeni bir tane oluşturun](remoteapp-create-custom-image.md).

> [!TIP]
> Tooa Windows Server 2012 R2 görüntüsünde, Azure RemoteApp abonelik erişmenizi kendi şablon görüntüsü toocreate kullanabileceğiniz Azure VM galeri hello biliyor muydunuz? [Kullanıma](remoteapp-image-on-azurevm.md).  
> 
> 

Azure RemoteApp ile kullanılmak üzere karşıya hello görüntüsü için Hello gereksinimleri şunlardır:

* Özel uygulamalar veri hello görüntüde yerel olarak depolamayın. Bu görüntüler, durum bilgisiz ve uygulamalar yalnızca içermelidir.
* Merhaba görüntü kaybedilen veri içermiyor.
* Merhaba görüntü boyutu, MB katları olmalıdır. Tooupload tam katı değil bir görüntü deneyin hello karşıya yükleme başarısız olur.
* Merhaba görüntü boyutu 127 GB olmalıdır ya da daha küçük.
* Bir VHD dosyası üzerinde olmalıdır (VHDX dosyaları şu anda desteklenmiyor).
* Merhaba VHD 2. nesil sanal makine olmaması gerekir.
* Merhaba VHD sabit boyutlu veya dinamik olarak genişletilen olabilir. Bir sabit boyutlu VHD dosyası'den daha az zaman tooupload tooAzure aldığından dinamik olarak genişleyen bir VHD önerilir.
* Merhaba ana önyükleme kaydı (MBR) bölümleme stilini kullanarak Hello disk başlatılması gerekir. Merhaba GUID bölümleme tablosu (GPT) bölümleme stilini desteklenmiyor.
* Merhaba VHD tek bir Windows Server 2012 R2 yüklemesini içermesi gerekir. Windows yüklemesini içeren birden çok birim, ancak yalnızca bir içerebilir.
* Merhaba Uzak Masaüstü oturumu ana bilgisayarı (RDSH) rolü ve hello Masaüstü Deneyimi özelliği yüklü olmalıdır.
* Merhaba Uzak Masaüstü Bağlantı Aracısı rol gerekir *değil* yüklü olmalıdır.
* Merhaba şifreleme dosya sistemi (EFS) devre dışı bırakılması gerekir.
* Merhaba görüntüsü hello parametrelerini kullanarak bir Sysprep uygulanmış olması gerekir **/oobe / generalize/shutdown** (yapmak kullanmaz hello **/mode:vm** parametresi).
* Bir anlık görüntü zinciri, VHD'den karşıya yükleme desteklenmez.

Bkz: [Azure RemoteApp görüntüsü oluşturma](remoteapp-imageoptions.md) Azure RemoteApp için görüntüleri oluşturma hakkında daha fazla bilgi.

