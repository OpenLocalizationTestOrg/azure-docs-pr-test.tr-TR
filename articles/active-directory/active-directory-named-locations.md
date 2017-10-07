---
title: "Azure Active Directory'de aaaNamed konumları | Microsoft Docs"
description: "Konumları adlı yapılandırarak IP sahip önleyebilirsiniz kuruluşunuz tarafından sahip olunan adresleri hello mümkün olmayan seyahat tooatypical konumları risk olay türü için hatalı pozitif sonuç oluşturur."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a>Azure Active Directory'de adlandırılmış konumları

Azure Active Directory konumları özelliği adlı hello ile kuruluşların güvenilir IP adres aralıklarını etiketleyebilirsiniz. Ortamınızda, adlandırılmış konumlarını hello algılanması hello bağlamda kullanabilirsiniz [risk olayları](active-directory-reporting-risk-events.md). Merhaba özelliği, hello hello için bildirilen hatalı pozitif uyarıların sayısını azaltmaya yardımcı olur *mümkün olmayan seyahat tooatypical konumları* risk olayı türü. 

## <a name="configuration"></a>Yapılandırma

tooconfigure adlandırılmış bir konumu:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) genel yönetici olarak.

2. Merhaba sol bölmede **Azure Active Directory**.

    ![Merhaba sol bölmede Hello Azure Active Directory bağlantısı](./media/active-directory-named-locations/01.png)

3. Merhaba üzerinde **Azure Active Directory** dikey penceresinde hello **güvenlik** 'yi tıklatın **koşullu erişim**.

    ![Merhaba koşullu erişim komutu](./media/active-directory-named-locations/05.png)


4. Merhaba üzerinde **koşullu erişim** dikey penceresinde hello **Yönet** 'yi tıklatın **konumları adlı**.

    ![Merhaba adlandırılmış konumları komutu](./media/active-directory-named-locations/06.png)


5. Merhaba üzerinde **konumları adlı** dikey penceresinde tıklatın **yeni konum**.

    ![Merhaba yeni konum komutu](./media/active-directory-named-locations/07.png)


6. Merhaba üzerinde **yeni** dikey penceresinde, aşağıdaki hello:

    ![Merhaba yeni dikey penceresi](./media/active-directory-named-locations/08.png)

    a. Merhaba, **adı** adlandırılmış konumunuz için bir ad yazın.

    b. Merhaba, **IP aralıkları** bir IP aralığı yazın. Merhaba IP aralığı gereken hello toobe *sınıfsız etki alanları arası yönlendirme* (CIDR) biçimi.  

    c. **Oluştur**'a tıklayın.



## <a name="what-you-should-know"></a>Bilmeniz gerekenler

**Toplu güncelleştirmeler**: oluşturduğunuzda veya toplu güncelleştirmeler için adlandırılmış konumlarını güncelleştirin karşıya yükleme veya hello IP aralıklarını içeren bir CSV dosyası indirme. Karşıya yükleme hello IP aralıkları hello listesi üzerine yerine hello dosya toohello listesinde ekler.

![Merhaba karşıya ve karşıdan yükleme bağlantıları](./media/active-directory-named-locations/09.png)


**Sınırlamalar**: en fazla 60 adlandırılmış konumları, bunların bir IP aralığı atanan tooeach ile tanımlayabilirsiniz. Yapılandırılmış tek bir adlandırılmış konumunuz varsa too500 IP aralıkları için tanımlayabilirsiniz.


## <a name="next-steps"></a>Sonraki adımlar

toolearn risk olaylar hakkında daha fazla bilgi görmek [Azure Active Directory risk olaylarını](active-directory-reporting-risk-events.md).

