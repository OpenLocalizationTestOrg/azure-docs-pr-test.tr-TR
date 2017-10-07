---
title: "Azure Active Directory Domain Services: Sanal ağ oluşturma veya seçme | Microsoft Docs"
description: "Azure Active Directory etki alanı hello Klasik Azure portalı kullanarak Hizmetleri etkinleştir"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 212c741b20e846742d94f70342c4263ce8984153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a>Azure Active Directory Domain Services için sanal ağ oluşturma veya seçme
## <a name="before-you-begin"></a>Başlamadan önce
Çok başvuran[Azure Active Directory etki alanı Hizmetleri için ağ konuları](active-directory-ds-networking.md).

## <a name="task-2-create-an-azure-virtual-network"></a>Görev 2: Azure sanal ağı oluşturma
Merhaba sonraki yapılandırma görevi Azure sanal ağı ve bir alt ağ içindeki toocreate değil. Sanal ağınızdaki bu alt ağda Azure Active Directory Domain Services’ı etkinleştirin. Toouse tercih var olan bir sanal ağınız varsa, bu adımı atlayabilirsiniz.

> [!NOTE]
> Bu hello oluşturun veya Azure Active Directory etki alanı Hizmetleri ile toouse tooan Azure Active Directory etki alanı Hizmetleri tarafından desteklenen Azure bölgesine ait seçin Azure sanal ağı emin olun. tooascertain Azure Active Directory etki alanı Hizmetleri olduğu kullanılabilir Azure bölgeleri Merhaba, bkz: [bölgeye göre Azure Hizmetleri](https://azure.microsoft.com/regions/#services/).
>
>Bir sonraki yapılandırma adımında Azure Active Directory etki alanı Hizmetleri'ni etkinleştirdiğinizde hello doğru sanal ağı seçin hello sanal ağ tooensure Hello adını not edin.


toocreate tooenable Azure Active Directory etki alanı Hizmetleri, istediğiniz bir Azure sanal ağı bu yapılandırma yönergeleri izleyin:

1. Toohello Git [Klasik Azure portalı](https://manage.windowsazure.com).
2. Merhaba sol bölmesinde seçin **ağlar**.

    ![Ağlar düğümü](./media/active-directory-domain-services-getting-started/networks-node.png)  
    Merhaba **sanal ağlar** penceresi açılır.
3. Merhaba görev hello pencerenin hello altındaki bölmesinde **yeni**.

    ![Sanal ağlar penceresi](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. **Ağ Hizmetleri** düğümüne tıklayıp **Sanal Ağ** öğesini seçin.

    ![Sanal ağ - hızlı oluştur](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. bir sanal ağ toocreate tıklatın **hızlı Oluştur**.

6. Belirtin bir **adı** , sanal ağ ve hello aşağıdakileri yaparak göz önünde bulundurun:
    * Tooconfigure seçebilirsiniz **adres alanı** veya **maksimum VM sayısını** bu ağ için.
    * Merhaba bırakabilirsiniz **DNS sunucusu** olarak ayarlama **hiçbiri** şimdilik. Azure Active Directory etki alanı Hizmetleri'ni etkinleştirdikten sonra hello ayarı güncelleştirebilirsiniz.
7. Merhaba, **konumu** aşağı açılan listesinde, desteklenen bir Azure bölgesini seçin.  
    tooascertain Azure Active Directory etki alanı Hizmetleri olduğu kullanılabilir Azure bölgeleri Merhaba, bkz: [bölgeye göre Azure Hizmetleri](https://azure.microsoft.com/regions/#services/).
8. toocreate sanal ağınızı tıklatın **bir sanal ağ oluşturma**.

    ![Azure Active Directory Domain Services için sanal ağ oluşturma](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. Bir sanal ağ oluşturduktan sonra hello hello sanal ağın adını seçin ve hello ardından **yapılandırma** sekmesi.

    ![Alt ağ oluşturma](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. Altında **sanal ağ adres alanları**, tıklatın **alt ağ Ekle**ve ardından hello ada sahip bir alt ağ belirtip **AaddsSubnet**.

    ![Azure Active Directory Domain Services için alt ağ oluşturma](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. toocreate alt Merhaba, tıklatın **kaydetmek**.


## <a name="next-step"></a>Sonraki adım
[Görev 3: Azure Active Directory Domain Services'i etkinleştirme](active-directory-ds-getting-started-enableaadds.md)
