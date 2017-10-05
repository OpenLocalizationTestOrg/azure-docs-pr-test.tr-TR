---
title: "Azure RemoteApp koleksiyonunuzun güncelleştirme | Microsoft Docs"
description: "Azure RemoteApp koleksiyonunuzun güncelleştirme konusunda bilgi edinin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 454d78445d6092aec9eaa383e4c50cf15195848c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a>Azure RemoteApp koleksiyonunda güncelleştir
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Uygulamaları veya Azure RemoteApp koleksiyonunuzun görüntüde güncelleştirmek için gerektiğinde bir zaman kaçınılmaz olarak, gelen. Bir bulut veya karma koleksiyonunda Azure RemoteApp aboneliğiniz ile birlikte gelen görüntülerden birini kullanıyorsanız, tüm güncelleştirmeleri kolay tuttuğunuzda şekilde Azure RemoteApp tarafından kendisine ele alınır.

Ancak, özel bir görüntü (sıfırdan yerleşik veya bizim görüntülerden birini değiştirerek oluşturulan) kullanıyorsanız, görüntü ve uygulamaların güncelliğini sorumlu değildir. Görüntünüzü veya diğer uygulamalar içindeki güncellemeniz gerekiyorsa, görüntüyü yeni ve güncelleştirilmiş bir sürümünü oluşturur ve ardından mevcut koleksiyonunuzdaki bu yeni güncelleştirilmiş görüntünüzle değiştirin gerekir.

Bu nedenle, nasıl gittiğiniz koleksiyonunuzu güncelleştirme hakkında? Bu oldukça basittir:

1. Koleksiyonda kullanılan görüntüyü güncelleştirin. Herhangi bir düzeltme ekleri veya gerekli güncelleştirmeleri uygulamak ve yeni bir adla kaydedin.
2. [Karşıya yükleme](remoteapp-uploadimage.md) veya [alma](remoteapp-image-on-azurevm.md) RemoteApp görüntüsünü.
3. Şimdi, koleksiyon sayfasında, tıklatın **güncelleştirme**.
4. Yeni görüntüden seçin **şablon görüntüsü** listesi.
5. Hassas bölümü İşte - koleksiyonda bir uygulama kullanmakta olduğunuz herhangi bir kullanıcının uğraşmanız nasıl karar vermeniz gerekir. İçin şu seçenekleriniz vardır:
   
   * **Kullanıcılara güncelleştirmeden sonra 60 dakika ver**. Güncelleştirme tamamlandıktan hemen sonra Azure RemoteApp çalışmalarını kaydetmeleri ve oturumu kapatın ve tekrar oturum açmak için onları belirten etkin hiçbir kullanıcı bir ileti görüntülenir. 60 dakika sonra kapattınız olmayan herhangi bir etkin kullanıcılar otomatik olarak oturumunuz kapatılacak. Kullanıcılar hemen oturum açın.
   * **Kullanıcıların oturumunu hemen kapat**. Güncelleştirme tamamlandıktan hemen sonra herhangi bir uyarı olmadan otomatik olarak tüm kullanıcıların oturumunu. Bu seçeneği seçerseniz, kullanıcılar veri kaybedebilir. Ancak, bunlar uygulamaya hemen bağlanabilirsiniz.
6. Güncelleştirmeyi başlatmak için onay işaretine tıklayın.

