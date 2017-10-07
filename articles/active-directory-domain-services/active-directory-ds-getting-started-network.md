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
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Azure Active Directory etki alanı hello Azure portal (Önizleme) kullanarak Hizmetleri etkinleştir


## <a name="before-you-begin"></a>Başlamadan önce
Çok başvuran[Azure Active Directory etki alanı Hizmetleri için ağ konuları](active-directory-ds-networking.md).


## <a name="task-2-configure-network-settings"></a>Görev 2: ağ ayarlarını yapılandırma
Merhaba sonraki yapılandırma görevi bir Azure sanal ağı ve ayrılmış bir alt ağ içindeki toocreate değil. Sanal ağınızdaki bu alt ağda Azure Active Directory Domain Services’ı etkinleştirin. Ayrıca varolan bir sanal ağı seçin ve ayrılmış hello alt ağ içindeki oluşturmak.

1. Tıklatın **sanal ağ** tooselect bir sanal ağ.
2. Merhaba üzerinde **Seç sanal ağ** dikey penceresinde, var olan tüm sanal ağları bakın. Merhaba üzerinde seçtiğiniz toohello kaynak grubu ve Azure konumuna ait yalnızca hello sanal ağlar bkz **Temelleri** sihirbaz sayfası.

3. Azure AD etki alanı Hizmetleri etkinleştirilmelidir hello sanal ağ seçin. Tıklatın **Yeni Oluştur**, toocreate yeni bir sanal ağ tercih ederseniz. Ayrılmış bir alt ağ için Azure AD Etki Alanı Hizmetleri'ni kullanarak öneririz. Mevcut bir sanal ağı seçerseniz [hello sanal ağlar uzantısını kullanarak ayrılmış bir alt ağ oluşturmak](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) ve bu alt ağ seçin. 

    ![Sanal ağ seçin](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. Tıklatın **alt** toopick hello içinde hangi tooenable yeni yönetilen etki alanı bu sanal ağ içinde ayrılmış bir alt ağ. Merhaba, **alt ağ oluşturmak** dikey penceresinde hello alt ağ için bir ad belirtin ve tıklatın **Tamam** tamamladığınızda. Örneğin, 'DomainServices' diğer yöneticiler toounderstand hello alt ağda dağıtılan kolaylaştırır, hello adında bir alt ağ oluşturun.

    ![Merhaba sanal ağ içindeki alt ağ seçin](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > **Bir alt seçme yönergeleri**
  > 1. Ayrılmış bir alt ağ için Azure AD Etki Alanı Hizmetleri'ni kullanın. Diğer bir sanal makine toothis alt dağıtmayın. Bu yapılandırma, yönetilen etki alanınız kesintiye uğratmadan iş yükleri/sanal makineleriniz için tooconfigure ağ güvenlik grupları (Nsg'ler) etkinleştirir. Ayrıntılar için bkz [konuları Azure Active Directory etki alanı Hizmetleri için ağ](active-directory-ds-networking.md).
  2. Desteklenen bir yapılandırma olduğundan Azure AD etki alanı Hizmetleri dağıtmak için ağ geçidi alt ağı hello seçmeyin.
  3. Seçtiğiniz hello alt yeterli kullanılabilir adres alanı - en az 3-5 kullanılabilir IP adresleri olduğundan emin olun.
  >

5. İşiniz bittiğinde tıklatın **Tamam** toohello üzerinde toomove **yönetici grubuna** hello Sihirbazı sayfası.


## <a name="next-step"></a>Sonraki adım
[Görev 3: yönetim grubunu yapılandırın ve Azure AD Etki Alanı Hizmetleri'ni etkinleştirme](active-directory-ds-getting-started-admingroup.md)
