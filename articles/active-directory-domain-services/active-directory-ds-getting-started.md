---
title: "Azure Active Directory etki alanı Hizmetleri: Başlarken | Microsoft Docs"
description: "Azure Active Directory etki alanı (Önizleme) Azure portalını kullanarak Hizmetleri etkinleştir"
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
ms.openlocfilehash: 47507096a6245d4f1ba57a652ddf5167b3776ae9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a>Azure Active Directory etki alanı (Önizleme) Azure portalını kullanarak Hizmetleri etkinleştir
Bu makalede, Azure Active Directory etki alanı Azure portalını kullanarak hizmetlerin (Azure AD DS) nasıl etkinleştirileceği gösterilmektedir.


Başlatmak için **etkinleştirmek Azure AD etki alanı Hizmetleri** Sihirbazı, aşağıdaki adımları tamamlayın:

1. [Azure Portal](https://portal.azure.com) gidin.
2. Sol bölmede tıklayın **yeni**.
3. İçinde **yeni** dikey penceresinde, türü **etki alanı Hizmetleri** arama çubuğunu içine.

    ![Etki Alanı Hizmetleri için arama](./media/getting-started/search-domain-services.png)

4. Seçmek için tıklatın **Azure AD etki alanı Hizmetleri** arama önerileri listesinden. Üzerinde **Azure AD etki alanı Hizmetleri** dikey penceresinde tıklatın **oluşturma** düğmesi.

    ![Etki Alanı Hizmetleri dikey penceresini](./media/getting-started/domain-services-blade.png)

5. **Etkinleştirmek Azure AD etki alanı Hizmetleri** Sihirbazı başlatıldığında.


## <a name="task-1-configure-basic-settings"></a>Görev 1: temel ayarlarını yapılandırma
İçinde **Temelleri** Sayfa Sihirbazı'nın, yönetilen etki alanı için DNS etki alanı adı belirtebilirsiniz. Ayrıca, yönetilen etki alanı dağıtılmalıdır Azure konumu ve kaynak grubu seçebilirsiniz.

![Temel yapılandırma](./media/getting-started/domain-services-blade-basics.png)

1. Seçin **DNS etki alanı adı** yönetilen etki alanınız için.

   * Dizinin varsayılan etki alanı adını (ile bir **. onmicrosoft.com** soneki) varsayılan olarak belirtilir.

   * Ayrıca, bir özel etki alanı adını yazabilirsiniz. Bu örnekte özel etki alanı adı *contoso100.com* şeklindedir.

     > [!WARNING]
     > Belirttiğiniz etki alanı adının ön eki (örneğin, *contoso100.com* etki alanı adında *contoso100*) 15 veya daha az karakter içermelidir. 15 karakterden daha uzun bir önek ile yönetilen bir etki alanı oluşturamazsınız.
     >
     >

2. Yönetilen etki alanı için seçtiğiniz DNS etki alanı adının sanal ağda zaten bulunmadığından emin olun. Özellikle, denetleme olup olmadığını:

   * Sanal ağda aynı DNS etki alanı adına sahip bir etki alanınız zaten varsa.

   * Yönetilen etki alanını etkinleştirmek planladığınız sanal ağ ile şirket içi ağınıza bir VPN bağlantısı vardır. Bu senaryoda, şirket içi ağınızda aynı DNS etki alanı adına sahip bir etki alanı olmadığından emin olun.

   * Sanal ağda bu ada sahip bir bulut hizmetiniz zaten varsa.

3. Seçin **sanal ağ türü**. Varsayılan olarak, **Resource Manager** sanal ağ türü seçilidir. Bu sanal ağ türü yönetilen etki alanları yeni oluşturulan tüm kullanmanızı öneririz.

4. Azure seçin **abonelik** , yönetilen etki alanı oluşturmak istediğinizi içinde.

5. Seçin **kaynak grubu** için yönetilen etki alanına ait olması gerekir. Ya da seçebilirsiniz **Yeni Oluştur** veya **var olanı kullan** seçenekleri kaynak grubunu seçin.

6. Azure seçin **konumu** , yönetilen etki alanında oluşturulmalıdır. Üzerinde **ağ** sayfasında sihirbazın, seçtiğiniz konuma ait yalnızca sanal ağlar görürsünüz.

7. İşiniz bittiğinde tıklatın **Tamam** üzerinde taşımayı **ağ** Sihirbazı sayfası.


## <a name="next-step"></a>Sonraki adım
[2. Görev: Ağ ayarlarını yapılandırma](active-directory-ds-getting-started-network.md)
