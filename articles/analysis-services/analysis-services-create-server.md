---
title: bir Analysis Services sunucusuna Azure aaaCreate | Microsoft Docs
description: "Nasıl toocreate bir Analysis Services sunucusu örneği Azure'da öğrenin."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a>Azure portalında bir Azure Analysis Services sunucusu oluşturma
Bu makalede, Azure aboneliğinizde bir Analysis Services sunucu kaynağı oluşturmada size anlatılmaktadır.

## <a name="before-you-begin"></a>Başlamadan önce
toocomplete Bu Hızlı Başlangıç, gerekir:

* **Azure aboneliği**: ziyaret [Azure ücretsiz deneme sürümü](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate bir hesap.
* **Azure Active Directory**: aboneliğinizi bir Azure Active Directory Kiracı ile ilişkilendirilmiş olması gerekir. Ve tooAzure içinde bu Azure Active Directory'de bir hesapla oturum toobe gerekir. Microsoft hesapları desteklenmez. toolearn daha, fazla [kimlik doğrulaması ve kullanıcı izinleri](analysis-services-manage-users.md).
* **Kaynak grubu**: zaten bir kaynak grubunu kullanın veya [yeni bir tane oluşturun](../azure-resource-manager/resource-group-overview.md).

> [!NOTE]
> Sunucu oluşturulması ek hizmet ücretlerine neden olabilir. toolearn daha, fazla [Analysis Services fiyatlandırma](https://azure.microsoft.com/pricing/details/analysis-services/).
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a>toocreate Azure portalında bir sunucu
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).  
2. Tıklatın **+ yeni** > **veri + analiz** > **Analysis Services**.
3. Merhaba, **Analysis Services** dikey penceresinde hello gerekli alanları doldurun ve sonra basın **oluşturma**.
   
    ![Sunucu oluşturma](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * **Sunucu adı**: kullanılan benzersiz bir ad tooreference hello sunucu yazın.
   * **Abonelik**: Bu sunucunun bills için hello abonelik seçin.
   * **Kaynak grubu**: Azure kaynağı koleksiyonunu yönetmenize tasarlanmış toohelp bu kapsayıcılardır. toolearn daha, fazla [kaynak grupları](../azure-resource-manager/resource-group-overview.md).
   * **Konum**: Bu Azure veri merkezi konum konakları hello sunucu. En büyük kullanıcı tabanınızı en yakın bir konum seçin.
   * **Fiyatlandırma katmanı**: bir fiyatlandırma katmanı seçin. Tablolu modeller too400 GB yukarı desteklenir. toolearn daha, fazla [Azure Analysis Services fiyatlandırma](https://azure.microsoft.com/pricing/details/analysis-services/).
4. **Oluştur**'a tıklayın.

Oluşturma genellikle bir dakika altında; alır genellikle yalnızca birkaç saniye sayısı. Seçtiyseniz **tooPortal ekleme**, yeni sunucunuzu tooyour portal toosee gidin. Ya da çok gidin**daha fazla hizmet** > **Analysis Services** sunucunuz hazır olup olmadığını toosee.

 ![Pano](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a>Sonraki adımlar
Sunucunuz oluşturduktan sonra [bir model dağıtma](analysis-services-deploy.md) tooit SSDT kullanarak veya SSMS ile.

Tooyour sunucu dağıttığınız bir model tooon içi veri kaynaklarına bağlanıyorsa, tooinstall gereken bir [şirket içi veri ağ geçidi](analysis-services-gateway.md) ağınızdaki bir bilgisayara.

