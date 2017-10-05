---
title: "Azure RemoteApp görüntü gereksinimleri | Microsoft Docs"
description: "Azure RemoteApp ile kullanılacak görüntüleri oluşturmak için gereksinimleri hakkında bilgi edinin"
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
ms.openlocfilehash: 75b0f8d6b25a80f11002b683152cfb294cbb68bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a>Azure RemoteApp görüntüleri için gereksinimleri
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Azure RemoteApp, kullanıcılarınız ile paylaşmak istediğiniz tüm programlar barındırmak için bir Windows Server 2012 R2 görüntüsünü kullanır. Özel bir görüntü oluşturmak için varolan bir görüntüyle başlatabilirsiniz veya [yeni bir tane oluşturun](remoteapp-create-custom-image.md).

> [!TIP]
> Azure RemoteApp aboneliğiniz Windows Server 2012 R2 görüntüsünü kendi şablon görüntüsü oluşturmak için kullanabilirsiniz Azure VM galerisinde erişmenizi olduğunu biliyor muydunuz? [Kullanıma](remoteapp-image-on-azurevm.md).  
> 
> 

Azure RemoteApp ile kullanılmak üzere yüklenen görüntü için gereksinimleri şunlardır:

* Özel uygulamalar veri görüntüde yerel olarak depolamayın. Bu görüntüler, durum bilgisiz ve uygulamalar yalnızca içermelidir.
* Görüntü kaybedilen veri içermiyor.
* Görüntü boyutu, MB katları olmalıdır. Tam katı değil görüntüyü karşıya yüklemeye karşıya yükleme başarısız olur.
* Görüntü boyutu 127 GB olmalıdır ya da daha küçük.
* Bir VHD dosyası üzerinde olmalıdır (VHDX dosyaları şu anda desteklenmiyor).
* 2. nesil sanal makine VHD olmamalıdır.
* VHD'yi sabit boyutlu veya dinamik olarak genişletilen olabilir. Azure için bir sabit boyutlu VHD dosyasının karşıya yüklemek için daha az zaman alır çünkü dinamik olarak genişleyen bir VHD önerilir.
* Disk bölümleme stilini ana önyükleme kaydı (MBR) kullanarak başlatılması gerekir. GUID bölümleme tablosu (GPT) bölümleme stilini desteklenmiyor.
* VHD'yi tek bir Windows Server 2012 R2 yüklemesini içermesi gerekir. Windows yüklemesini içeren birden çok birim, ancak yalnızca bir içerebilir.
* Uzak Masaüstü oturumu ana bilgisayarı (RDSH) rolü ve Masaüstü Deneyimi özelliği yüklü olmalıdır.
* Uzak Masaüstü Bağlantı Aracısı rol gerekir *değil* yüklü olmalıdır.
* Şifreleme Dosya Sistemi (EFS) devre dışı bırakılması gerekir.
* Resmin parametrelerini kullanarak bir Sysprep uygulanmış olması gerekir **/oobe / generalize/shutdown** (vermeyin kullanım **/mode:vm** parametresi).
* Bir anlık görüntü zinciri, VHD'den karşıya yükleme desteklenmez.

Bkz: [Azure RemoteApp görüntüsü oluşturma](remoteapp-imageoptions.md) Azure RemoteApp için görüntüleri oluşturma hakkında daha fazla bilgi.

