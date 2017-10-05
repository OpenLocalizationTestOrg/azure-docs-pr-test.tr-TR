---
title: "Özel görüntü Azure RemoteApp için karşıya yükleme | Microsoft Docs"
description: "Özel görüntü Azure RemoteApp için karşıya yükleme öğrenin"
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
ms.openlocfilehash: 5a235fac88d6e95ea294bda197641108acb4a09f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a>Özel görüntü Azure RemoteApp için karşıya yükleme
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Özel şablon görüntünüzü oluşturmuş veya değişikliklerle güncelleştirdiniz göre bu görüntüyü Azure RemoteApp görüntüsü kitaplığınıza karşıya gerekir. Bu adımları kullanın.

## <a name="before-you-start"></a>Başlamadan önce
1. Özel görüntünüzü karşıladığını doğrulamak [görüntü gereksinimleri](remoteapp-imagereqs.md) ve [uygulama gereksinimleri](remoteapp-appreqs.md).
2. Yükleme [Azure PowerShell Modülü](/powershell/azure/overview).

## <a name="step-by-step-on-how-to-upload-custom-image"></a>Özel görüntü karşıya yüklemek adım adım hakkında
1. Azure Yönetim Portalı'nı açın ve RemoteApp sayfasına gidin.
2. Üzerinde **şablon görüntüleri** sekmesini tıklatın, **karşıya** sayfanın sonundaki.
3. Görüntü için kolay bir ad girin ve depolama hesabı konumu belirtin. RemoteApp koleksiyonunuzun aynı konuma veya oluşturmak için istediğiniz bir konuma konumu olduğundan emin olun.
4. İstendiğinde, komut dosyasını yerel bilgisayarınıza indirin.
5. Komut parametreleri metin kutusuna panonuza kopyalayın.
6. Yükseltilmiş bir Windows PowerShell penceresi açın.
7. Yükseltilmiş Windows PowerShell penceresinden betik indirdiğiniz dizinine gidin.
8. Tuşuna basın ve kopyalanan komutu yapıştırın **Enter**.
   
   Karşıya yükleme işlemi başlar ve süre ağ hızı ve görüntünün boyutuna dahil olmak üzere birçok faktöre bağlıdır
9. Karşıya yüklemeyi ağ kesintisi veya şeyler nedeniyle gibi başarısız olursa, her zaman, başlangıcından karşıya yükleme işlemi devam edebilir. Karşıya yükleme sürdürmek için aynı komut satırını kullanarak yeniden komut dosyasını çalıştırın.

> [!WARNING]
> Hiçbir zaman karşıya yükleme komut dosyasını değiştirin. Görüntünün görüntü gereksinimleri ve uygulama gereksinimleri karşıladığından emin olmak için belirli denetimleri uygulanmamış olabilir.
> 
> 

## <a name="common-problems"></a>Sık karşılaşılan sorunları
* Windows PowerShell, Azure PowerShell kullandığınızdan emin olun. Belirli modüller karşıya yükleme işlemi sırasında gerekli olduğu için Azure PowerShell modülünü yüklemeniz gerekir.
* Komut dosyası hiçbir zaman alter, size kolaylık olması için doğrulamaları vardır.
* Vhd dosyasını karşıya yükleme sırasında kilitli, dosya kopyalama veya bunu yeni bir konum ve girişimi yüklemek üzere yeniden taşıyın. Karşıya yükleme engelliyor bazı Windows işlemi olabilir.  

