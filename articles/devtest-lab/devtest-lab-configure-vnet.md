---
title: "Azure DevTest Labs sanal bir ağa aaaConfigure | Microsoft Docs"
description: "Bilgi nasıl tooconfigure bir varolan sanal ağ ve alt ağ ve bunları Azure DevTest Labs bir VM'de kullanın"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: a11ce8315e3c540e44aeacc9c5ee3dde014d4621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a>Azure DevTest Labs'de sanal ağ yapılandırma
Merhaba makalesinde açıklandığı gibi [yapıları tooa Laboratuvar'yle bir VM'yi eklemek](devtest-lab-add-vm-with-artifacts.md), bir laboratuar ortamında bir VM oluştururken yapılandırılmış bir sanal ağ belirtin. Bunu yapmak için bir tooaccess gerekiyorsa corpnet kaynaklarınızdan kullanarak, Vm'lerde ExpressRoute veya siteden siteye VPN ile yapılandırılmış sanal ağ hello senaryodur. Merhaba aşağıdaki bölümlerde göstermeye nasıl tooadd varolan sanal ağınıza onun kullanılabilir toochoose Vm'leri oluştururken, böylece bir laboratuvar ait sanal ağ ayarları.

## <a name="configure-a-virtual-network-for-a-lab-using-hello-azure-portal"></a>Hello Azure portal kullanarak bir laboratuvar için bir sanal ağ yapılandırma
Merhaba aşağıdaki adımlar, böylece bir VM hello oluşturulurken kullanılabilir var olan sanal ağ (ve alt ağ) tooa Laboratuvar eklerken size yol aynı Laboratuvar. 

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.
3. Merhaba istenen Laboratuvar labs Hello listeden seçin. 
4. Merhaba Laboratuvar'ın dikey penceresinde, seçin **yapılandırma**.
5. Merhaba Laboratuvar'ın üzerinde **yapılandırma** dikey penceresinde, select **sanal ağlar**.
6. Merhaba üzerinde **sanal ağlar** dikey penceresinde hello geçerli Laboratuvar ve bunun yanı sıra, laboratuvarınız için oluşturulan hello varsayılan sanal ağ için yapılandırılan sanal ağların bir listesini görürsünüz. 
7. Seçin **+ Ekle**.
   
    ![Varolan bir sanal ağ tooyour Laboratuvar ekleme](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. Merhaba üzerinde **sanal ağ** dikey penceresinde, select **[Select sanal ağ]**.
   
    ![Varolan bir sanal ağı seçin](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. Merhaba üzerinde **Seç sanal ağ** dikey penceresinde, select hello istenen sanal ağı. Merhaba dikey gösterir altında aynı hello olan tüm hello sanal ağları hello Laboratuvar olarak hello Abonelikteki bölge.  
10. Bir sanal ağı seçtikten sonra toohello döndürülür **sanal ağ** hello dikey penceresinde hello sonundaki hello listesinde hello alt ağ'ı tıklatın.

    ![Alt ağ listesi](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    Merhaba Laboratuvar alt dikey penceresinde görüntülenir.

    ![Laboratuvar alt dikey penceresi](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. Belirtin bir **Laboratuvar alt ağ adı**.
12. VM oluşturma, Laboratuvar içinde kullanılan bir alt ağ toobe tooallow seçin **sanal makine oluşturma kullanımda**.
13. tooenable bir [genel IP adresi paylaşılan](devtest-lab-shared-ip.md)seçin **etkinleştir paylaşılan ortak IP**.
14. tooallow genel IP adresleri bir alt ağ seçin **ortak IP oluşturmaya izin**.
15. Merhaba, **kullanıcı başına en fazla sanal makine** alanında, belirtin her alt ağ için kullanıcı başına en fazla VMs hello. Sanal makineleri sınırsız sayıda istiyorsanız bu alanı boş bırakın.
16. Seçin **Tamam** tooclose hello Laboratuvar alt dikey.
17. Seçin **kaydetmek** tooclose hello sanal ağ dikey.
18. Merhaba sanal ağı yapılandırılır, bir VM oluşturulurken seçilebilir. 
    toosee nasıl toocreate VM ve bir sanal ağ belirtin, toohello makalesine başvurun [yapıları tooa Laboratuvar'yle bir VM'yi eklemek](devtest-lab-add-vm-with-artifacts.md). 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Sonraki adımlar
Merhaba istenen sanal ağ tooyour Laboratuvar ekledikten sonra hello sonraki çok adımdır[VM tooyour Laboratuvar ekleme](devtest-lab-add-vm-with-artifacts.md).

