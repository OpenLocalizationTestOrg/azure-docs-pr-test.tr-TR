---
title: "Azure Active Directory etki alanı Hizmetleri: Başlarken | Microsoft Docs"
description: "Azure Active Directory etki alanı hello Azure portal (Önizleme) kullanarak Hizmetleri etkinleştir"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 79cbb21c4a50194f5ad8ca1a4a8493ee4a260a9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Azure Active Directory etki alanı hello Azure portal (Önizleme) kullanarak Hizmetleri etkinleştir
Bu makalede, Azure portal tooenable Azure Active Directory etki alanı kullanarak Hizmetleri (Azure AD DS) nasıl hello gösterilmektedir.


toolaunch hello **etkinleştirmek Azure AD etki alanı Hizmetleri** aşağıdaki adımları sihirbazında, tam hello:

1. Toohello Git [Azure portal](https://portal.azure.com).
2. Merhaba sol bölmede tıklayın **yeni**.
3. Merhaba, **yeni** dikey penceresinde, türü **etki alanı Hizmetleri** hello arama çubuğunu içine.

    ![Etki Alanı Hizmetleri için arama](./media/getting-started/search-domain-services.png)

4. Tooselect tıklatın **Azure AD etki alanı Hizmetleri** arama önerileri hello listesinden. Merhaba üzerinde **Azure AD etki alanı Hizmetleri** dikey penceresinde hello tıklatın **oluşturma** düğmesi.

    ![Etki Alanı Hizmetleri dikey penceresini](./media/getting-started/domain-services-blade.png)

5. Merhaba **etkinleştirmek Azure AD etki alanı Hizmetleri** Sihirbazı başlatıldığında.


## <a name="task-1-configure-basic-settings"></a>Görev 1: temel ayarlarını yapılandırma
Merhaba, **Temelleri** sayfa hello Sihirbazı'nın hello yönetilen etki alanı için hello DNS etki alanı adı belirtebilirsiniz. Merhaba kaynak grubunu da seçebilirsiniz ve Azure konumu toowhich hello yönetilen etki alanı dağıtılmalıdır.

![Temel yapılandırma](./media/getting-started/domain-services-blade-basics.png)

1. Merhaba seçin **DNS etki alanı adı** yönetilen etki alanınız için.

   * Merhaba dizinin Hello varsayılan etki alanı adı (ile bir **. onmicrosoft.com** soneki) varsayılan olarak belirtilir.

   * Ayrıca, bir özel etki alanı adını yazabilirsiniz. Bu örnekte, hello özel etki alanı adıdır *contoso100.com*.

     > [!WARNING]
     > Belirtilen etki alanı adınızı Hello önek (örneğin, *contoso100* hello içinde *contoso100.com* etki alanı adı) 15 veya daha az karakter içermelidir. 15 karakterden daha uzun bir önek ile yönetilen bir etki alanı oluşturamazsınız.
     >
     >

2. Etki alanı zaten hello sanal ağında yok, yönetilen hello için seçtiğiniz bu hello DNS etki alanı adını sağlayın. Özellikle, denetleme olup olmadığını:

   * Merhaba sahip bir etki alanı zaten hello sanal ağda aynı DNS etki alanı adı.

   * Burada tooenable hello yönetilen etki alanı planlama hello sanal ağ ile şirket içi ağınıza bir VPN bağlantısı vardır. Bu senaryoda, yok hello olan bir etki alanında olduğundan emin olun, şirket içi ağınızda aynı DNS etki alanı adı.

   * Bu ada sahip olan bir bulut hizmetini hello sanal ağda bulunan.

3. Merhaba seçin **sanal ağ türü**. Varsayılan olarak, hello **Resource Manager** sanal ağ türü seçilidir. Bu sanal ağ türü yönetilen etki alanları yeni oluşturulan tüm kullanmanızı öneririz.

4. Select hello Azure **abonelik** toocreate hello yönetilen etki alanı içinde istediğinizi.

5. Select hello **kaynak grubu** toowhich hello yönetilen etki alanına ait olmalıdır. Her iki hello seçebilirsiniz **Yeni Oluştur** veya **var olanı kullan** seçenekleri tooselect hello kaynak grubu.

6. Hello Azure'ı seçin **konumu** hangi hello yönetilen etki alanı oluşturulması gerekir. Merhaba üzerinde **ağ** sayfa hello Sihirbazı'nın, seçtiğiniz toohello konumu ait yalnızca sanal ağlar görürsünüz.

7. İşiniz bittiğinde tıklatın **Tamam** toohello üzerinde toomove **ağ** hello sihirbazın sayfası.


## <a name="next-step"></a>Sonraki adım
[2. Görev: Ağ ayarlarını yapılandırma](active-directory-ds-getting-started-network.md)
