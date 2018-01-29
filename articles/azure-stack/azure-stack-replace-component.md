---
title: "Bir Azure yığın ölçek birimi düğümünde bir donanım bileşeni Değiştir | Microsoft Docs"
description: "Bir Azure tümleşik yığını sistemde donanım bileşeni Değiştir öğrenin."
services: azure-stack
documentationcenter: 
author: mattbriggs
manager: femila
editor: 
ms.assetid: c6e036bf-8c80-48b5-b2d2-aa7390c1b7c9
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2017
ms.author: mabrigg
ms.openlocfilehash: 4937b7725c8f39314ccc41584a8646b7197f6bdf
ms.sourcegitcommit: 6fb44d6fbce161b26328f863479ef09c5303090f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/10/2018
---
# <a name="replace-a-hardware-component-on-an-azure-stack-scale-unit-node"></a>Bir Azure yığın ölçek birimi düğümünde bir donanım bileşeni Değiştir

*Uygulandığı öğe: Azure yığın tümleşik sistemleri*

Bu makalede olmayan hot Swap donanım bileşenleri değiştirmek için genel işlem açıklanır. Gerçek değiştirme adımları farklılık özgün donanım üreticisi (OEM) donanım satıcınıza temel. Azure tümleşik yığını sisteme özgü ayrıntılı adımlar için satıcınızın alan değiştirilebilen biriminin (FRU) belgelerine bakın.

Olmayan hot Swap bileşenleri şunları içerir:

- CPU *
- Bellek *
- Ana/temel kart yönetim denetleyicisi (BMC) / video kartı
- Disk denetleyicisi/ana bilgisayar veri yolu bağdaştırıcısı (HBA) / devre kartı
- Ağ bağdaştırıcısı (NIC)
- İşletim sistemi disk *
- Veri sürücüleri (sık kullanılan takas, örneğin PCI-e-eklentisini kartı desteklemeyen sürücüler) *

* Bu bileşenlerin sık kullanılan takas desteklemiyor olabilir, ancak satıcı mantığınız göre değişebilir. Ayrıntılı adımlar için OEM satıcınızın FRU belgelerine bakın.

Aşağıdaki akış diyagramı olmayan hot Swap donanım bileşeni değiştirmek için genel FRU işlemi gösterilmektedir.

![Akış bileşeni değiştirme akışını gösteren diyagram](media/azure-stack-replace-component/replacecomponentflow.PNG)

* Bu eylem donanım fiziksel koşula göre gerekli olmayabilir.

** Olup OEM donanım satıcınıza bileşen değiştirme işlemi gerçekleştirir ve bellenim güncelleştirmeleri göre değişir üzerinde sözleşme destekler.

## <a name="review-alert-information"></a>Uyarı bilgileri gözden geçirin

Azure yığın sistem durumunu ve izleme sistemi ağ bağdaştırıcıları ve veri sürücüleri depolama alanları doğrudan tarafından denetlenen sistem durumunu izler. Diğer donanım bileşenleri izlemez. Diğer tüm donanım bileşenleri için donanım yaşam döngüsü konakta çalışan çözüm izleme satıcıya özgü donanım uyarılar oluşturulur.

## <a name="component-replacement-process"></a>Bileşen değiştirme işlemi

Aşağıdaki adımlar bileşeni değiştirme işlemi üst düzey bir genel bakış sağlar. OEM tarafından sağlanan FRU belgelerinize bakarak olmadan adımları izlemeyin.

1. Kullanım [boşaltma](azure-stack-node-actions.md#scale-unit-node-actions) ölçek birimi düğümü bakım moduna eylem. Bu eylem donanım fiziksel koşula göre gerekli olmayabilir.

   > [!NOTE]
   > Herhangi bir durumda, yalnızca tek bir düğüme boşaltmış ve değiştirebilirsiniz aynı anda S2D bozmadan kapalı (depolama alanları doğrudan).

2. Ölçek birimi düğüm bakım modunda olduğunda kullanın [kapatmak](azure-stack-node-actions.md#scale-unit-node-actions) eylem. Bu eylem donanım fiziksel koşula göre gerekli olmayabilir.
 
   > [!NOTE]
   > Eylem kapatma işe yaramazsa olası durumda da, temel kart yönetim denetleyicisi (BMC) web arabirimi kullanın.

3. Bozuk donanım bileşeni değiştirin. OEM donanım satıcınıza bileşen değiştirme gerçekleştirip gerçekleştirmediğini, destek sözleşmenize göre değişir.  
4. Bellenim güncelleştirin. Düzeyi uygulanan onaylanan bellenim değiştirilen donanım bileşeni olduğundan emin olmak için donanım yaşam döngüsü konağı kullanmayı, satıcıya özgü bellenim güncelleştirme işlemini izleyin. OEM donanım satıcınıza bu adımı gerçekleştirip gerçekleştirmediğini, destek sözleşmenize göre değişir.  
5. Kullanım [onarım](azure-stack-node-actions.md#scale-unit-node-actions) ölçek birimi düğümü Ölçek birimine geri getirmek için eylem.
6. Ayrıcalıklı uç noktasına kullanmak [sanal disk onarım durumunu denetleme](azure-stack-replace-disk.md#check-the-status-of-virtual-disk-repair). Yeni bir veri sürücüsü ile tam depolama onarım iş sistem yükü bağlı olarak birkaç saat sürebilir ve alan tüketilen.
7. Onarım işlemi tamamlandıktan sonra tüm etkin uyarıları otomatik olarak kapatılan doğrulayın.

## <a name="next-steps"></a>Sonraki adımlar

- Hot Swap fiziksel disk değiştirme hakkında daha fazla bilgi için bkz: [disk değiştirme](azure-stack-replace-disk.md).
- Bir fiziksel düğüm değiştirme hakkında daha fazla bilgi için bkz: [bir ölçek birimi düğümü yerine](azure-stack-replace-node.md).
- 
