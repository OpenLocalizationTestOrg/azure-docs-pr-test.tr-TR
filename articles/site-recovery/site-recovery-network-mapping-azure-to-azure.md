---
title: "Azure Site kurtarma iki Azure bölgeleri arasında aaaNetwork eşleme | Microsoft Docs"
description: "Azure Site Recovery hello çoğaltma, yük devretme ve sanal makinelerin ve fiziksel sunucuları kurtarma düzenler. Yük devretme tooAzure veya ikincil veri merkezine hakkında bilgi edinin."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 4f80c44e3f94eaf446bc01a7041d91fe34aa78d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="network-mapping-between-two-azure-regions"></a>İki Azure bölgeleri arasında ağ eşlemesi


Bu makalede nasıl toomap Azure sanal ağlar birbirlerine iki Azure bölgelerinin. Ağ eşlemesi çoğaltılmış sanal makine hello hedef Azure bölgesi oluşturduğunuzda, onu eşlenen toovirtual ağ hello kaynak sanal makinenin hello sanal ağ üzerinde oluşturulur sağlar.  

## <a name="prerequisites"></a>Ön koşullar
Eşledikten önce ağları oluşturduğunuzdan emin olun [Azure sanal ağlar](../virtual-network/virtual-networks-overview.md) hem de kaynak ve hedef Azure bölgeleri.

## <a name="map-networks"></a>Ağ eşleme

toomap bir Azure sanal ağı bir Azure bölgesi tooanother sanal ağdaki başka bir bölgede gidin tooSite kurtarma altyapı ağ eşlemesi (Azure Virtual Machines için) -> ve bir ağ eşlemesi oluşturun.

![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


Hello aşağıdaki sanal Makinem Doğu Asya bölgesinde çalıştığından ve yüklenmekte olan örnek tooSoutheast Asya çoğaltılan.

Merhaba kaynak ve hedef ağ seçin ve Tamam toocreate Doğu Asya tooSoutheast Asya arasında ağ eşlemesi'ye tıklayın.

![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


Aynı şey toocreate Güneydoğu Asya tooEast Asya arasında ağ eşlemesi hello.  
![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a>Çoğaltma etkinleştirirken eşleme ağ

Bir sanal makine için hello ilk saat biçiminde bir Azure bölgesi tooanother çoğaltırken ağ eşlemesi yapılmazsa sonra hedef ağ hello bir parçası olarak seçebileceğiniz aynı işlemi. Site Recovery ağ eşlemeleri Kaynak bölgesi tootarget bölge ve bu seçime dayalı hedef bölge toosource bölgesi oluşturur.   

![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

Varsayılan olarak, Site Recovery ağ aynı toohello kaynak ağ hello hedef bölgesi ve ekleyerek oluşturur '-asr' hello kaynak ağ bir sonek toohello adından farklı. Önceden oluşturulmuş bir ağ Özelleştir'i tıklatarak seçebilirsiniz.

![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


Merhaba ağ eşlemesi zaten yapıldığında, çoğaltmayı etkinleştirirken hello hedef sanal ağ değiştiremezsiniz. toochange, mevcut ağ eşlemesini değiştirin.  

![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Ağ eşlemesi](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> Bölge 1 tooregion-2 ağ eşlemesini değiştirirseniz, bölge 2 tooregion-1'de hello ağ eşlemesi değiştirdiğinizden emin olun.
>
>


## <a name="subnet-selection"></a>Alt ağ seçimi
Merhaba hedef sanal makinenin hello hello alt hello kaynak sanal makinenin adına göre seçilir. Merhaba alt ise hello hedef sanal makine için seçilen sonra aynı hello kaynak sanal makinenin hello hedef ağ kullanılabilir olarak adlandırın. Merhaba bir alt ağ ise alfabetik olarak ilk alt ağ hedef alt hello olarak seçilen aynı hello hedef ağ adı. Bu alt ağ tooCompute ve hello sanal makinesinin ağ ayarları giderek değiştirebilirsiniz.

![Alt ağ değiştirme](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a>IP adresi

Her hello ağ arabiriminin hello hedef sanal makine için IP adresi gibi seçilir:

### <a name="dhcp"></a>DHCP
Merhaba ağ arabirimi hello kaynak sanal makinenin DHCP kullanıyorsanız, hello hedef sanal makinenin ağ arabirimi Ayrıca DHCP ayarlanır.

### <a name="static-ip"></a>Statik IP
Merhaba ağ arabirimi hello kaynak sanal makinenin statik IP kullanıyorsanız, ağ arabiriminin hello hedef sanal makine de toouse statik IP ayarlanır. Statik IP şu şekilde seçilir:

#### <a name="same-address-space"></a>Aynı adres alanı

Merhaba kaynak alt ağı ve hello hedef alt hello varsa, hedef IP hello IP hello ağ arabiriminin hello kaynak sanal makinenin aynı ayarlayın daha sonra aynı adres alanı. Aynı IP kullanılabilir durumda değilse, başka bir kullanılabilir IP hello hedef IP ayarlanır.

#### <a name="different-address-space"></a>Farklı bir adres alanı

Merhaba kaynak alt ağı ve hello hedef alt farklı bir adres alanı varsa, hedef IP hello hedef alt ağda kullanılabilir herhangi bir IP'yi olarak ayarlanır.

Her ağ arabiriminde hello hedef IP tooCompute ve hello sanal makinesinin ağ ayarları giderek değiştirebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

- Hakkında bilgi edinin [Azure Vm'lerini çoğaltma kılavuz ağ](site-recovery-azure-to-azure-networking-guidance.md).
