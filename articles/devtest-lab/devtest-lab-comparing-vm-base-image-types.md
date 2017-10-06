---
title: "aaaComparing özel resimler ve DevTest Labs formüller | Microsoft Docs"
description: "Hangisinin ortamınıza en uygun karar vermem VM taban gibi hello özel resimler ve formülleri arasındaki farklar hakkında bilgi edinin."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tarcher
ms.openlocfilehash: 3c1d88dfe0ff94b8e825bb7a0b4aca3341c9330d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a>Özel resimler ve DevTest Labs formüller karşılaştırma
Her ikisi de [özel resimler](devtest-lab-create-template.md) ve [formüller](devtest-lab-manage-formulas.md) için tabanları olarak kullanılan [yeni VM'ler oluşturulan](devtest-lab-add-vm-with-artifacts.md). Ancak, özel resimler ve formülleri arasında hello anahtar fark özel görüntü yalnızca bir formül VHD dayanan bir görüntü olsa da bir VHD'de dayanan bir görüntü olmasıdır *ek olarak* ayarları - VM boyutunu, sanal ağ gibi önceden yapılandırılmış alt ağ ve yapıları. Bu önceden yapılandırılmış ayarlar hello VM oluşturma sırasında geçersiz kılınabilir varsayılan değerlerle ayarlanır. Bu makalede bazı hello avantajları (uzmanları için) açıklanır ve formülleri kullanma karşılaştırması (olumsuz) toousing özel resimler olumsuz.

## <a name="custom-image-pros-and-cons"></a>Özel görüntü Artıları ve eksileri
Özel resimler statik ve sabit bir yol toocreate istenen ortamından VM'ler sağlar. 

**Uzmanları**

* Merhaba görüntüden hiçbir şey değiştiğinde VM çalışmaya başlar hello sonra özel bir görüntüden sağlama VM hızlıdır. Diğer bir deyişle, yalnızca bir resim ayarları olmadan hello özel görüntü olarak hiçbir ayarları tooapply vardır. 
* Tek bir özel görüntüden oluşturulan VM'ler aynıdır.

**Simgeler**

* Bazı yönlerinin hello özel görüntü tooupdate gerekiyorsa, hello görüntü yeniden oluşturulmalıdır.  

## <a name="formula-pros-and-cons"></a>Formül Artıları ve eksileri
Formülleri dinamik şekilde toocreate VM'ler istenen hello yapılandırması/ayarlarını sağlayın.

**Uzmanları**

* Merhaba ortam değişiklikleri hello kolay bir şekilde yapıları aracılığıyla yakalanır. Merhaba en son sürüm hattınızı bitten yüklü olan bir VM istediğiniz veya hello en son kod, depodan listeleme, örneğin, yalnızca hello en son kod ile birlikte hello formülünde kaydeder veya hello son BITS dağıtan bir yapı belirleyebileceğiniz bir Hedef temel görüntü. Bu formülü kullanılan toocreate VM'ler olduğunda hello son BITS/kod toohello VM dağıtılan ve kayıtlı olan. 
* Formülleri özel resimler - VM boyutları ve sanal ağ ayarları gibi sağlayamaz varsayılan ayarlarını tanımlayabilirsiniz. 
* Formül kaydedilmiş hello ayarları varsayılan değerler olarak gösterilir, ancak hello VM oluşturulduğunda değiştirilebilir. 

**Simgeler**

* Bir formülünden bir VM oluşturma, özel bir görüntüden bir VM oluşturma değerinden daha uzun sürebilir.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>İlgili blog gönderileri
* [Özel resimler veya formüller?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a>Sonraki adımlar
- [DevTest Labs SSS](devtest-lab-faq.md)