---
title: "aaaNo çalışma bağlayıcı grubu için uygulama proxy'si uygulama bulundu | Microsoft Docs"
description: "Hiç çalışma bağlayıcı hello Azure AD uygulama proxy'si ile uygulamanız için bir bağlayıcı grubunda olduğunda, karşılaşabileceğiniz sorunları"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4c4baf296b316db131929c9a7c618fb9960713e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a>Hiç çalışma bağlayıcı grubu için uygulama proxy'si uygulama bulunamadı

Bu makale Yardım, tooresolve hello sık karşılaşılan sorunları için uygulama proxy'si uygulama algılanan bir bağlayıcı olmadığında karşılaştığı Azure Active Directory ile tümleştirilmiştir.

## <a name="overview-of-steps"></a>Adımlara genel bakış
Hiç çalışma uygulamanız için bir bağlayıcı grubundaki bağlayıcı ise, birkaç yolu tooresolve hello sorunu vardır:

-   Bağlayıcılar hello grubunda varsa, şunları yapabilirsiniz:

    -   Merhaba sağ şirket içi sunucuda yeni bir bağlayıcı indirin ve toothis grubu atama

    -   Etkin bir bağlayıcı hello grubuna taşıyın

-   Merhaba grubunda active bağlayıcılar varsa, şunları yapabilirsiniz:

    -   Merhaba neden Bağlayıcınızı etkin değil tanımlama ve giderme

    -   Etkin bir bağlayıcı hello grubuna taşıyın

olan bu hello sorunu tooknow uygulamanızda hello "Uygulama proxy'si" menüsünü açın ve hello bağlayıcı Grup uyarı iletisini arayın. Bunu o hello grubun en az bir bağlayıcı (hiçbiri hello grubunda olması) gerekiyor veya (büyük olasılıkla etkin olmayan bağlayıcılar elinizde rağmen) etkin bağlayıcılar olduğunu belirtin.

   ![Azure Portalı'nda bağlayıcı Grup Seçimi](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

Bu seçeneklerin her biri hakkında daha fazla bilgi için hello karşılık gelen bölümüne bakın. Bunların her biri hello bağlayıcı yönetim sayfasından başlayarak olduğunu varsayar. Merhaba hata ileti yukarıdaki arıyorsanız, hello uyarı iletisi tıklayarak toothis sayfasına gidebilirsiniz. Aksi takdirde bu çok giderek bulunabilir**Azure Active Directory**, üzerinde tıklatmak **kurumsal uygulamalar**, ardından **uygulama proxy'si.**

   ![Azure Portalı'nda bağlayıcı Grup Yönetimi](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a>Yeni bir bağlayıcı indirin

toodownload yeni bir bağlayıcı hello hello sayfanın başında hello "Bağlayıcısı'nı indir" düğmesini kullanın.

toobe doğrudan görüş toohello arka uç uygulaması olan bir makinede yüklü ve genellikle yerleştirildiği Not hello bağlayıcı gereksinimlerini Merhaba uygulaması aynı sunucuya hello. Merhaba bağlayıcı indirdikten sonra bu menüsünde görüntülenmelidir. Merhaba Connector'ı tıklatın ve hello "Bağlayıcı grubu" açılan toomake toohello sağ grubuna ait olduğundan emin kullanın. Merhaba değişikliği kaydedin.

   ![Merhaba bağlayıcı hello Azure Portalı ' indirin](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a>Etkin bir Bağlayıcıyı taşıma

Toohello grubuna ait olması gerekir ve görüş toohello hedef arka uç uygulaması olan bir active bağlayıcısı varsa, atanan hello grubuna hello bağlayıcı taşıyabilirsiniz. toodo, bu nedenle, hello bağlayıcı tıklayın. Merhaba "Bağlayıcı grubu" alanında hello açılan tooselect hello doğru Grup kullanın ve Kaydet'i tıklatın.

## <a name="resolve-an-inactive-connector"></a>Etkin olmayan bir bağlayıcı çözümleyin

Bağlayıcılar hello grubundaki etkin olmayan yalnızca hello olmayan bir makineye büyük olasılıkla olmaları durumunda tüm hello gerekli bağlantı noktaları engeli kaldırılmış.

Başlangıç noktaları Bkz: Bu sorunu araştırmaya ile ilgili ayrıntılar için sorun giderme belgesi.

## <a name="next-steps"></a>Sonraki adımlar
[Azure AD uygulama proxy'si bağlayıcılar anlama](application-proxy-understand-connectors.md)


