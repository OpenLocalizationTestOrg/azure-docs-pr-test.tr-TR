---
title: "Azure RemoteApp için özel bir görüntü aaaUpload | Microsoft Docs"
description: "Nasıl tooupload özel bir görüntü Azure RemoteApp için bilgi edinin"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a>Özel görüntü Azure RemoteApp için karşıya yükleme
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Özel şablon görüntünüzü oluşturmuş veya değişikliklerle güncelleştirdiniz göre bu görüntü tooyour Azure RemoteApp görüntü kitaplığı tooupload gerekir. Bu adımları kullanın.

## <a name="before-you-start"></a>Başlamadan önce
1. Özel görüntünüzü hello karşıladığını doğrulamak [görüntü gereksinimleri](remoteapp-imagereqs.md) ve [uygulama gereksinimleri](remoteapp-appreqs.md).
2. Merhaba yüklemek [Azure PowerShell Modülü](/powershell/azure/overview).

## <a name="step-by-step-on-how-tooupload-custom-image"></a>Adım adım izlenecek tooupload özel görüntü
1. Azure Yönetim Portalı'nı açın ve toohello RemoteApp sayfasına gidin.
2. Merhaba üzerinde **şablon görüntüleri** sekmesini tıklatın, **karşıya** hello sayfanın hello sonundaki.
3. Görüntü için kolay bir ad girin ve hello depolama hesap konumu belirtin. Başlangıç konumu hello olduğundan emin olun, RemoteApp koleksiyonu veya toocreate bir istediğiniz bir konuma aynı konumda.
4. İstendiğinde, hello betik tooyour karşıdan yerel bilgisayar.
5. Merhaba komut parametreleri hello metin kutusu tooyour panoya kopyalayın.
6. Yükseltilmiş bir Windows PowerShell penceresi açın.
7. Windows PowerShell penceresinde Hello yükseltilmiş toohello gidin hello komut dosyasını indirdiğiniz aynı dizin.
8. Yapıştır hello kopyalanan komutu ve tuşuna **Enter**.
   
   Merhaba karşıya yükleme işlemi başlar ve süre hello görüntünün boyutu ve ağ hızı dahil olmak üzere birçok faktöre bağlıdır
9. Karşıya yüklemeyi ağ kesintisi veya şeyler nedeniyle gibi başarılı olmazsa, her zaman, başlangıcından hello karşıya yükleme işlemi devam edebilir. Merhaba komut dosyasını kullanarak yeniden çalıştırmak tooresume bir karşıya yükleme hello aynı komut satırı.

> [!WARNING]
> Hiçbir zaman hello karşıya yükleme komut dosyasını değiştirin. Özel denetimler görüntü hello görüntü gereksinimlerini karşıladığını ve uygulama gereksinimleri hello uygulanan tooensure olmuştur.
> 
> 

## <a name="common-problems"></a>Sık karşılaşılan sorunları
* Windows PowerShell, Azure PowerShell kullandığınızdan emin olun. Belirli modüller hello karşıya yükleme işlemi sırasında gerekli olduğu için tooinstall hello Azure PowerShell modülü gerekir.
* Hiçbir zaman hello betik alter, size kolaylık olması için doğrulamaları vardır.
* Hello vhd dosyasını karşıya yükleme sırasında kilitli, hello dosyasını kopyalayın veya bunu tooa yeni konum girişimi karşıya yükleyin ve yeniden taşıyın. Karşıya yükleme engelliyor bazı Windows işlemi olabilir.  

