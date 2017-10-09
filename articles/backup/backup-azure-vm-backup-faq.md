---
title: aaaAzure VM Backup ile ilgili SSS | Microsoft Docs
description: "Hakkında toocommon soruları yanıtlar: Azure VM yedekleme çalışır, sınırlamalar ve ne olacağını nasıl değişiklikleri toopolicy ortaya çıktığında"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "azure vm yedeklemesi, azure vm geri yükleme, yedekleme ilkesi"
ms.assetid: c4cd7ff6-8206-45a3-adf5-787f64dbd7e1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: a1ad2cb3a379577a8c4258c8207ce75809e11a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-vm-backup-service"></a>Hello Azure VM Backup hizmeti hakkında sorular
Bu makalede yanıtlar toocommon sorular toohelp hızlı bir şekilde hello Azure VM Backup bileşenlerini anlama sahiptir. Bazı hello yanıtlar kapsamlı bilgiler bağlantılar toohello makaleler vardır. Hello Azure Backup hizmeti hakkında sorular hello nakledebilirsiniz [tartışma Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="configure-backup"></a>Yedeklemeyi yapılandırma
### <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>Kurtarma Hizmetleri kasaları, klasik VM’leri mi Resource Manager tabanlı VM’leri mi destekler? <br/>
Kurtarma Hizmetleri kasaları iki modeli de destekler.  (Merhaba Klasik Portalı'nda oluşturulan) klasik bir VM veya kurtarma Hizmetleri kasası Kaynak Yöneticisi'ni (hello Azure portalında oluşturulan) VM tooa yedekleyebilirsiniz.

### <a name="what-configurations-are-not-supported-by-azure-vm-backup-"></a>Azure VM yedeklemesinde hangi yapılandırmalar desteklenmez?
Lütfen [Desteklenen işletim sistemleri](backup-azure-arm-vms-prepare.md#supported-operating-system-for-backup) ve [VM yedeklemesinin sınırları](backup-azure-arm-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) konularını inceleyin.

### <a name="why-cant-i-see-my-vm-in-configure-backup-wizard"></a>Yedeklemeyi yapılandırma sihirbazında sanal makinemi neden göremiyorum?
Yedeklemeyi yapılandırma sihirbazında, Azure Backup yalnızca şu sanal makineleri listeler:
* Zaten korumalı - tooVM dikey gidip hello dikey ayarları menüsünden yedekleme durumu denetimi hello VM yedekleme durumunu doğrulayabilirsiniz. Çok konusunda daha fazla bilgi edinin[bir VM yedekleme durumunu denetleme](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-vm-management-blade)
* VM olarak toosame bölgeye ait

## <a name="backup"></a>Backup
### <a name="will-on-demand-backup-job-follow-same-retention-schedule-as-scheduled-backups"></a>İsteğe bağlı yedekleme işi zamanlanmış yedeklemelerle aynı bekletme zamanlamasına mı uyar?
Hayır. Toospecify hello saklama aralığı için bir talep üzerine yedekleme işi gerekir. Varsayılan olarak, portaldan tetiklendiğinde 30 gün bekletilir. 

### <a name="i-recently-enabled-azure-disk-encryption-on-some-vms-will-my-backups-continue-toowork"></a>Kısa süre önce bazı sanal makinelerde Azure Disk Şifrelemesi'ni etkinleştirdim. Yedeklerim toowork devam eder?
Azure Backup hizmeti tooaccess anahtar kasası toogive izinlerinizin olması gerekir. [PowerShell](backup-azure-vms-automation.md) belgelerinin *Yedeklemeyi Etkinleştirme* bölümünde belirtilen adımları kullanarak, PowerShell'de bu izinleri sağlayabilirsiniz.

### <a name="i-migrated-disks-of-a-vm-toomanaged-disks-will-my-backups-continue-toowork"></a>I diskleri VM toomanaged disklerin geçirildi. Yedeklerim toowork devam eder?
Evet, yedekleme sorunsuz bir şekilde çalışır ve hiçbir gerek toore-yedeklemeyi yapılandırın. 

## <a name="restore"></a>Geri Yükleme
### <a name="how-do-i-decide-between-restoring-disks-versus-full-vm-restore"></a>Diskleri geri yüklemekle tam sanal makine geri yüklemesi yapmak arasında nasıl seçim yapabilirim?
Azure tam sanal makine geri yüklemesini, geri yüklenmiş sanal makine için hızlı oluşturma seçeneği sağlayan bir yol olarak düşünün. VM geri yükleme seçeneği diskleri hello adlarını değiştirmek, kapsayıcıları, VM oluşturmanın bir parçası oluşturulan kaynakları benzersizliğini adları diskler, genel IP adresleri, ağ arabirimi tarafından kullanılır. Ayrıca hello VM tooavailability kümesi eklemez. 

Aşağıdakileri yapmak için diskleri geri yükleme seçeneğini kullanın:
* Başlangıç zamanı yapılandırması yedekleme yapılandırmasından hello boyutunu değiştirme gibi noktasından oluşturulan VM özelleştirme
* Yedekleme hello aynı anda mevcut olmayan yapılandırmalarını ekleme 
* Oluşturulan kaynakları için Denetim hello adlandırma kuralı
* VM tooavailability kümesi Ekle
* Yalnızca PowerShell/bildirim temelli bir şablon tanımı kullanılarak gerçekleştirilebilen bir yapılandırmanız olması durumunda

## <a name="manage-vm-backups"></a>VM yedeklemelerini yönetme
### <a name="what-happens-when-i-change-a-backup-policy-on-vms"></a>Sanal makinelerde yedekleme ilkesini değiştirdiğimde ne olur?
Sanal makine üzerinde yeni bir ilke uygulandığında, zamanlama ve saklama hello yeni ilkenin izlenir. Bekletme genişletilirse, var olan kurtarma noktalarının tookeep işaretlenecek bunları yeni ilke göredir. Bekletme azaltıldığında için ayıklama hello sonraki temizleme işi işaretlenir ve silinir. 
