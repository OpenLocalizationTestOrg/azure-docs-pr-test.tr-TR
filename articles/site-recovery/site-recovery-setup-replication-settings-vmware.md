---
title: "Azure Site Recovery için çoğaltma ayarlarını aaaSet | Microsoft Docs"
description: "Nasıl toodeploy Site Recovery tooorchestrate çoğaltma, yük devretme ve kurtarma Hyper-V vm'lerinde VMM Bulutu tooAzure açıklar."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 618e92e42411732a2a1bb75c5e5ea8a433cd7d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-replication-policy-for-vmware-tooazure"></a>VMware tooAzure için çoğaltma ilkesini yönetme


## <a name="create-a-replication-policy"></a>Çoğaltma ilkesi oluşturma

1. **Yönet** > **Site Recovery Altyapısı**’nı seçin.
2. **VMware ve Fiziksel makineler için** altındaki **Çoğaltma ilkeleri**’ni seçin.
3. **+Çoğaltma ilkesi**’ni seçin.

    ![Çoğaltma ilkesi oluşturma](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. Hello ilkesi adı girin.

5. İçinde **RPO eşik**, hello RPO sınırını belirtin. Sürekli çoğaltma bu limiti aşarsa uyarılar oluşturulur.
6. İçinde **kurtarma noktası bekletme**, (saat olarak) belirtin hello hello bekletme penceresinin süresi her kurtarma noktası. Korumalı makineler olabilir bir bekletme aralığı içinde tooany noktası kurtarıldı.

    > [!NOTE]
    > Bekletme too24 saatleri makineler çoğaltılmış toopremium depolama için desteklenir. Bekletme too72 saatleri makineler çoğaltılmış toostandard depolama için desteklenir.

    > [!NOTE]
    > Yeniden çalışmaya yönelik bir çoğaltma ilkesi otomatik olarak oluşturulur.

7. **Uygulamayla tutarlı anlık görüntü sıklığı** kısmında, uygulamayla tutarlı anlık görüntüleri içeren kurtarma noktalarının hangi sıklıkta oluşturulacağını (dakika cinsinden) belirtin.

8. **Tamam** düğmesine tıklayın. Hello İlkesi 30 too60 saniye içinde oluşturulmalıdır.

![Çoğaltma ilkesi üretme](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a>Yapılandırma sunucusunu çoğaltma ilkesi ile ilişkilendirme
1. Merhaba çoğaltma ilkesi toowhich seçin tooassociate hello yapılandırma sunucusu istiyor.
2. **İlişkilendir**’e tıklayın.
![Yapılandırma sunucusunu ilişkilendirme](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)

3. Merhaba yapılandırma sunucusu hello sunucuların listesinden seçin.
4. **Tamam** düğmesine tıklayın. Merhaba yapılandırma sunucusu bir tootwo dakika cinsinden ilişkilendirilmesi.

![Yapılandırma sunucusu ilişkilendirme](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a>Çoğaltma ilkesini düzenleme
1. Tooedit çoğaltma ayarları istediğiniz hello çoğaltma ilkesi seçin.
![Çoğaltma ilkesini düzenleme](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)

2. **Ayarları Düzenle**’ye tıklayın.
![Çoğaltma ilkesi ayarlarını düzenleme](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)

3. Gereksinimleri temelinde hello ayarlarını değiştirin.
4. **Kaydet** düğmesine tıklayın. Hello İlkesi iki toofive dakika içinde kaydedilmelidir, kaç tane sanal makineleri bağlı olarak bu çoğaltma ilkesini kullanarak.

![Çoğaltma ilkesini kaydetme](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a>Yapılandırma sunucusunun çoğaltma ilkesi ile ilişkisini kaldırma
1. Merhaba çoğaltma ilkesi toowhich seçin tooassociate hello yapılandırma sunucusu istiyor.
2. **İlişkilendirmeyi Kaldır**’a tıklayın.
3. Merhaba yapılandırma sunucusu hello sunucuların listesinden seçin.
4. **Tamam** düğmesine tıklayın. Merhaba yapılandırma sunucusu bir tootwo dakika içinde ilkenin ilişkisi.

    > [!NOTE]
    > Hello İlkesi'ni kullanarak en az bir çoğaltılmış öğe ise bir yapılandırma sunucusu ilişkilendirmesini olamaz. Merhaba yapılandırma sunucusu ilişkilendirmesini önce hello İlkesi'ni kullanarak çoğaltılan öğe olmadığından emin olun.

## <a name="delete-a-replication-policy"></a>Çoğaltma ilkesini silme

1. Merhaba çoğaltma ilkesi seçin toodelete istiyor.
2. **Sil**'e tıklayın. Hello İlkesi 30 too60 saniye içinde silinmesi gerekir.

    > [!NOTE]
    > En az bir yapılandırma sunucusu ilişkili tooit varsa, bir çoğaltma ilkesi silemezsiniz. Hello İlkesi kullanılarak çoğaltılan öğe yok ve hello İlkesi silmeden önce tüm hello delete yapılandırma sunucularına ilişkili emin olun.
