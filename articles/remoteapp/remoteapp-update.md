---
title: aaaUpdate Azure RemoteApp koleksiyonunuzun | Microsoft Docs
description: "Bilgi nasıl tooupdate Azure RemoteApp koleksiyonunuzun"
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
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a>Azure RemoteApp koleksiyonunda güncelleştir
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Tooupdate hello uygulamaları veya görüntü Azure RemoteApp koleksiyonunuzda gerektiğinde bir zaman kaçınılmaz olarak, gelen. Bir bulut veya karma koleksiyonunda Azure RemoteApp aboneliğiniz ile birlikte gelen hello görüntülerden birini kullanıyorsanız, tüm güncelleştirmeleri kolay tuttuğunuzda şekilde Azure RemoteApp tarafından kendisine ele alınır.

Ancak, özel bir görüntü (sıfırdan yerleşik veya bizim görüntülerden birini değiştirerek oluşturulan) kullanıyorsanız, hello görüntü ve uygulamaların güncelliğini sorumlu değildir. Görüntünüzü ya da herhangi bir hello uygulamalar içindeki tooupdate gerekiyorsa, bu yeni güncelleştirilmiş görüntüsü ile koleksiyonunuza ', hello görüntü ve Değiştir hello mevcut görüntü yeni ve güncelleştirilmiş sürümü toocreate ihtiyacı vardır.

Bu nedenle, nasıl gittiğiniz koleksiyonunuzu güncelleştirme hakkında? Bu oldukça basittir:

1. Koleksiyonunuzda kullanılan hello görüntü güncelleştirin. Herhangi bir düzeltme ekleri veya gerekli güncelleştirmeleri uygulamak ve yeni bir adla kaydedin.
2. [Karşıya yükleme](remoteapp-uploadimage.md) veya [alma](remoteapp-image-on-azurevm.md) bu görüntü tooRemoteApp.
3. Şimdi, hello koleksiyonu sayfasında, tıklatın **güncelleştirme**.
4. Hello Hello yeni görüntü Seç **şablon görüntüsü** listesi.
5. Hello hassas bölümü İşte - toodecide nasıl gereken bir uygulamayı hello koleksiyonunda kullanmakta olduğunuz tüm kullanıcılarla toodeal. Seçenekler aşağıdaki hello vardır:
   
   * **Kullanıcılara hello güncelleştirmeden sonra 60 dakika ver**. Merhaba Güncelleştirme tamamlandıktan hemen sonra Azure RemoteApp iş ve oturum kapatma ve tekrar oturum toosave söyleyen bir ileti tooany active bir kullanıcıları görüntüler. 60 dakika sonra kapattınız olmayan herhangi bir etkin kullanıcılar otomatik olarak oturumunuz kapatılacak. Kullanıcılar hemen oturum açın.
   * **Kullanıcıların oturumunu hemen kapat**. Merhaba Güncelleştirme tamamlandıktan hemen sonra herhangi bir uyarı olmadan otomatik olarak tüm kullanıcıların oturumunu. Bu seçeneği seçerseniz, kullanıcılar veri kaybedebilir. Ancak, bunlar toohello uygulama hemen bağlanabilirsiniz.
6. Merhaba onay işareti toostart hello Güncelleştir'i tıklatın.

