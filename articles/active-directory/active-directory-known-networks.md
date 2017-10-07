---
title: "Merhaba Klasik Azure portalı aaaKnown ağlarda | Microsoft Docs"
description: "Bilinen ağları yapılandırarak, birden çok coğrafyadan oturum ve şüpheli etkinlik raporları ile birlikte IP adreslerinden gerçekleştirilen oturum hello dahil, kuruluşunuzun sahip olduğu IP adreslerine sahip olmasına önleyebilirsiniz."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: ec636cdda172cd3baeb1e606dd8d6e1949fbc63b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="known-networks"></a>Bilinen ağlar

> [!div class="op_single_selector"]
> * [Klasik Azure Portalı](active-directory-known-networks.md)
> * [Azure portal](active-directory-known-networks-azure-portal.md)
> 
> 


Azure Active Directory'nin erişim ve kullanım raporları toogain görünürlük hello bütünlüğü ve güvenlik kuruluşunuzun dizininin kullanabilirsiniz. Bu bilgileri kullanarak bir dizin yönetici böylece bunlar yeterli bu riskleri toomitigate planlayabilirsiniz olası güvenlik riskleri burada bulunan daha iyi belirleyebilirsiniz.

Merhaba mümkün olan "*birden çok coğrafyadan oturum*"ve"*oturum açmalar IP adreslerinden şüpheli etkinliğe sahip*" raporları yanlış bayrak tarafından gerçekten ait IP adresleri, Kuruluş. 

Örneğin, gerçekleşebilir zaman: 

* Bir kullanıcı, Boston ofisinizde uzaktan tooyour veri merkezinde San Francisco Tetikleyicileri hello "Birden çok coğrafyadan oturum açmalar" rapor imzaladığı 
* Bir kullanıcı, kuruluşunuzun toosign açma birkaç kez yanlış parola Tetikleyicileri hello "Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum" rapor ile çalışır 

Bu oluşturma yanıltıcı güvenlik çalışmalarından tooprevent raporları, bilinen IP adres aralıkları toohello listesi, kuruluşunuzun ortak IP adresinin eklemeniz gerekir.    

### <a name="tooadd-your-organizations-public-ip-address-ranges-perform-hello-following-steps"></a>tooadd kuruluşunuzun ortak IP adresi aralıkları, hello aşağıdaki adımları gerçekleştirin:

1. Oturum açma toohello [Azure Yönetim Portalı](https://manage.windowsazure.com).

2. Merhaba sol bölmede **Active Directory**. 

    ![Bilinen ağlar](./media/active-directory-known-networks/known-netwoks-01.png)

3. Merhaba, **Directory** sekmesinde, dizininizi seçin.

4. Hello içinde hello üst menüsünde **yapılandırma**. 

    ![Bilinen ağlar](./media/active-directory-known-networks/known-netwoks-02.png)

5. Merhaba yapılandırma sekmesinde çok Git**, kuruluşların ortak IP adresi aralıkları** 

    ![Bilinen ağlar](./media/active-directory-known-networks/known-netwoks-03.png)

6. Tıklatın **bilinen IP adres aralıklarını ekleyin**.

7. Görüntülenen hello iletişim kutusunda, adres aralıklarını ekleyin ve işiniz bittiğinde hello onay düğmesine tıklayın. 

    ![Bilinen ağlar](./media/active-directory-known-networks/known-netwoks-04.png)

**Ek kaynaklar:**

* [Erişim ve kullanım raporlarınızı görüntüleme](active-directory-view-access-usage-reports.md)
* [Şüpheli etkinliğe sahip IP adreslerinden oturum açmalar](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [Birden çok coğrafyadan oturum](active-directory-reporting-sign-ins-from-multiple-geographies.md)

