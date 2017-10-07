---
title: "Hyper-V çoğaltma tooa Azure Site Recovery ile ikincil site için bir çoğaltma ilkesi aaaSet | Microsoft Docs"
description: "Nasıl tooset Hyper-V VM çoğaltma tooa İlkesi ikincil VMM sitesi Azure Site Recovery ile açıklar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5d9b79cf-89f2-4af9-ac8e-3a32ad8c6c4d
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 6d008e3bb3fa0b666e91678cf6de3693dd712ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy"></a>8. adım: Bir çoğaltma ilkesi ayarlama

Yapılandırdıktan sonra [ağ eşlemesi](vmm-to-vmm-walkthrough-network-mapping.md), Hyper-V sanal makine (VM) çoğaltma tooa ikincil site için bu makale tooset bir çoğaltma ilkesi kullanmak kullanarak [Azure Site Recovery](site-recovery-overview.md).

Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Başlamadan önce

- Bir çoğaltma ilkesi oluşturduğunuzda, tüm ana bilgisayarlar hello İlkesi'ni kullanarak gerekir sahip hello aynı işletim sistemi. Windows Server'ın farklı sürümlerini çalıştıran Hyper-V konakları Hello VMM bulut içerebilir ancak bu durumda, birden fazla çoğaltma ilkesi gerekir.
- Çevrimdışı ilk çoğaltma hello gerçekleştirebilirsiniz.

## <a name="configure-replication-settings"></a>Çoğaltma ayarlarını yapılandırma

1. Yeni bir çoğaltma ilkesi toocreate tıklatın **altyapıyı hazırlama** > **çoğaltma ayarları** > **+ oluştur ve ilişkilendir**.

    ![Ağ](./media/vmm-to-vmm-walkthrough-replication/gs-replication.png)
2. **İlke oluştur ve ilişkilendir** bölümünde bir ilke adı belirtin. Merhaba kaynak ve hedef türü olmalıdır. **Hyper-V**.
3. İçinde **Hyper-V konak sürümü**, hello konakta çalıştırdığı işletim sistemi seçin.
4. İçinde **kimlik doğrulama türü** ve **kimlik doğrulama bağlantı noktası**, hello birincil ve kurtarma Hyper-V ana bilgisayar sunucuları arasında trafik kimliğinin nasıl belirtin. Seçin **sertifika** çalışan bir Kerberos ortam yoksa. Azure Site Recovery, HTTPS kimlik doğrulaması için sertifikaları otomatik olarak yapılandırır. Toodo herhangi bir şey el ile gerek yoktur. Varsayılan olarak, bağlantı noktası 8083 ve 8084 (Sertifikalar) hello Hyper-V ana bilgisayar sunucuları üzerinde Windows Güvenlik Duvarı hello açılacak. Seçerseniz **Kerberos**, Kerberos bileti hello konak sunucularının karşılıklı kimlik doğrulaması için kullanılacak. Bu ayar yalnızca Windows Server 2012 R2'de çalışan Hyper-V konak sunucuları için geçerli olduğunu unutmayın.
5. İçinde **kopyalama sıklığı**, ne sıklıkta hello ilk çoğaltma (her 30 saniyede, 5 veya 15 dakika) sonra tooreplicate değişim verileri istediğinizi belirtin.
6. İçinde **kurtarma noktası bekletme**, saat cinsinden ne kadar süreyle hello bekletme penceresi belirtin her kurtarma noktası için olabilir. Korumalı makineler olabilir bir pencere içinde tooany noktası kurtarıldı.
7. İçinde **uygulamayla tutarlı anlık görüntü sıklığı**, ne sıklıkla (1-12 saat) içeren uygulamayla tutarlı anlık görüntüleri kurtarma noktalarını belirtin oluşturulur. Hyper-V iki çeşit anlık kullanır — bir artımlı hello tüm sanal makinenin anlık görüntüsünü sunan standart anlık görüntü ve zaman içinde nokta verilerin bir anlık görüntüsünü hello uygulama hello sanal makine içinde geçen uygulama tutarlı bir anlık görüntü. Uygulamayla tutarlı anlık görüntüleri hello anlık görüntü alınırken uygulamaların tutarlı bir durumda olan birim gölge kopyası hizmeti (VSS) tooensure kullanın. Uygulamayla tutarlı anlık görüntüleri etkinleştirirseniz kaynak sanal makinelerde çalışan uygulamaların hello performansını etkiler. Ayarladığınız hello değeri, yapılandırdığınız ilave kurtarma noktası hello sayısından daha az olduğundan emin olun.
8. İçinde **veri aktarımı sıkıştırma**, aktarılan çoğaltılmış verilerin sıkıştırılmasının gerekli olup olmadığını belirtin.
9. Seçin **çoğaltmayı Sil VM**, hello kaynak VM için korumayı devre dışı bırakırsanız çoğaltma sanal makinesi hello toospecify'nin silinmesi. Merhaba kaynak hello Site Recovery konsolundan kaldırılan VM için korumayı devre dışı bıraktığınızda bu ayarı etkinleştirirseniz, hello VMM için Site Recovery ayarları hello VMM konsolundan kaldırılır ve hello çoğaltma silinir.
10. İçinde **ilk çoğaltma yöntemini**, hello ağ üzerinden çoğaltıyorsanız toostart ilk çoğaltma hello veya zamanlamak belirtin. toosave ağ bant genişliği, tooschedule isteyebileceğiniz meşgul saatleriniz dışında. Daha sonra, **Tamam**'a tıklayın.

     ![Çoğaltma ilkesi](./media/vmm-to-vmm-walkthrough-replication/gs-replication2.png)
11. Yeni bir ilke oluşturduğunuzda, otomatik olarak hello VMM Bulutu ile ilişkili. İçinde **Çoğaltma İlkesi**, tıklatın **Tamam**. Bu çoğaltma ilkesini ek VMM Bulutları (ve bunlara hello VM'ler) ilişkilendirebilirsiniz **çoğaltma** > ilke adı > **VMM Bulutu ile ilişkilendir**.

     ![Çoğaltma ilkesi](./media/vmm-to-vmm-walkthrough-replication/policy-associate.png)



## <a name="prepare-for-offline-initial-replication"></a>Çevrimdışı ilk çoğaltma için hazırlama

Merhaba ilk veri kopyalama için Çevrimdışı çoğaltma yapabilirsiniz. Bu şekilde hazırlayabilirsiniz:

* Hello kaynak sunucuda hangi hello verileri dışarı aktarma devre dışı gerçekleşecek bir yolu konumunu belirtin. Tam Denetim toohello VMM hizmeti hello dışarı aktarma yolundaki NTFS ve paylaşım izinlerini atayın. Merhaba hedef sunucuda içinden hello verileri içeri bir yolu konumuna oluşacaktır belirtin. Merhaba, bu alma yolu aynı izinleri atayın.
* Merhaba içe veya dışa aktarma yolu paylaşılan, hello VMM hizmet hesabı hello uzak bilgisayarda yönetici, Power User, Print Operator veya sunucu işleci grup üyeliği atamak paylaşılan hangi hello bulunur.
* Tüm farklı çalıştır hesapları tooadd konaklar kullanıyorsanız, hello içeri aktarma ve dışarı aktarma yollarındaki, okuma atayın ve VMM'de toohello farklı çalıştır hesapları yazma izinleri.
* Merhaba içeri aktarma ve dışarı aktarma paylaşımları geri döngü yapılandırma Hyper-V tarafından desteklenmediği için Hyper-V konak sunucusu olarak kullanılan herhangi bir bilgisayarda bulunmalıdır değil.
* Her Hyper-V ana bilgisayar sunucusunda tooprotect, istediğiniz sanal makineleri içeren Active Directory'de etkinleştirme ve yapılandırma Kısıtlı temsilci tootrust hello uzak bilgisayarları hangi hello içeri ve dışarı aktarma yollarının bulunduğu, aşağıdaki gibidir:
  1. Merhaba etki alanı denetleyicisinde açın **Active Directory Kullanıcıları ve Bilgisayarları**.
  2. Merhaba konsol ağacında **DomainName** > **bilgisayarlar**.
  3. Sağ hello Hyper-V ana bilgisayarı sunucusu adı > **özellikleri**.
  4. Merhaba üzerinde **temsilci** sekmesini tıklatın, **bu bilgisayara yalnızca temsilci toospecified Hizmetleri için güven**.
  5. Tıklatın **herhangi bir kimlik doğrulama protokolünü kullan**.
  6. Tıklatın **ekleme** > **kullanıcıları ve Bilgisayarları**.
  7. Merhaba verme yolu barındıran hello bilgisayarın türü hello adı > **Tamam**. Kullanılabilir hizmetler listeden Merhaba, hello CTRL tuşunu basılı tutun ve **CIFS** > **Tamam**. Merhaba hello bilgisayarın adını konakları hello alma yol yineleyin. Ek Hyper-V konak sunucuları için gerektiği kadar yineleyin.



## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 9: çoğaltmasını etkinleştir](vmm-to-vmm-walkthrough-enable-replication.md).
