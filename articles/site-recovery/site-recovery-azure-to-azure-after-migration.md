---
title: "Site Recovery kullanarak geçiş tooAzure sonra Azure bölgeler arasında olağanüstü durum kurtarma yukarı aaaPrepare makineler tooset | Microsoft Docs"
description: "Bu makalede, Azure Site Recovery kullanarak geçiş tooAzure sonra Azure bölgeler arasında olağanüstü durum kurtarma yukarı tooset nasıl tooprepare makineleri açıklanmaktadır."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ponatara
ms.openlocfilehash: b6274e3df210c1d8a7b8289cc85868ee6414e523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a>Azure Site Recovery kullanarak geçiş tooAzure sonra Azure Vm'lerinin tooanother bölge çoğaltma

>[!NOTE]
> Azure sanal makineleri (VM'ler) için Azure Site Recovery çoğaltma şu anda önizlemede değil.

## <a name="overview"></a>Genel Bakış

Bu makalede, Azure sanal makineleri Azure Site Recovery kullanarak bir şirket içi ortamına tooAzure bu makineler geçirildikten sonra iki Azure bölgeler arasında çoğaltma hazırlamanıza yardımcı olur.

## <a name="disaster-recovery-and-compliance"></a>Olağanüstü durum kurtarma ve uyumluluk
Bugün, daha da fazla kuruluşların kendi iş yükleri tooAzure taşıyor. Kritik şirket içi üretim taşıma kuruluşlara iş yükleri tooAzure, bu iş yükleri için olağanüstü durum kurtarma ayarlama uyumluluk ve bir Azure bölgesindeki kesintileri karşı toosafeguard için zorunludur.

## <a name="steps-for-preparing-migrated-machines-for-replication"></a>Geçirilen makineleri çoğaltma için hazırlama adımları
tooprepare çoğaltma tooanother Azure bölgesini ayarlamak için makineler geçişi:

1. Geçişi tamamlayın.
2. Merhaba gerekirse Azure aracısını yükleyin.
3. Merhaba Mobility hizmeti kaldırın.  
4. Merhaba VM yeniden başlatın.

Aşağıdaki bölümlerde hello bölümlerinde daha ayrıntılı adımları açıklanmaktadır.

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a>Adım 1: Hyper-V sanal makineleri, VMware Vm'lerini ve fiziksel sunucuları toorun Azure vm'lerinde çalışan iş yüklerini geçirme

tooset ayarlama çoğaltma ve, şirket içi Hyper-V, VMware ve fiziksel iş yükleri tooAzure hello adımları hello içinde geçirmek [Azure Site Recovery ile Azure bölgeler arasında geçirmek Azure Iaas sanal makineleri](site-recovery-migrate-to-azure.md) makalesi. 

Geçişten sonra toocommit gerek yok veya bir yük devretme silin. Bunun yerine, hello seçin **tam geçiş** seçeneği toomigrate istediğiniz her makine için:
1. İçinde **çoğaltılan öğeler**, hello VM sağ tıklayın ve **tam geçiş**. Tıklatın **Tamam** toocomplete hello adım. Merhaba tam geçiş işine izleyerek hello VM Özellikleri'nde ilerleme durumunu izleyebilirsiniz **Site Recovery işleri**.
2. Merhaba **tam geçiş** eylem hello geçiş işlemi tamamlanır, hello makinesi için çoğaltma kaldırır ve hello makine için Site Recovery Faturalaması durdurulur.

   ![tamgeçiş](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a>2. adım: hello Azure VM Aracısı hello sanal makineye yükleyin.
Hello Azure [VM Aracısı](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) hello Site Recovery uzantısı toowork ve toohelp hello VM korumak için hello sanal makineye yüklenmesi gerekir.

>[!IMPORTANT]
>Sürüm 9.7.0.0, Windows sanal makinelerde itibaren hello Mobility hizmeti yükleyicisinin hello en son kullanılabilir Azure VM Aracısı de yükler. Geçiş üzerinde aracı yüklemesi hello Site Recovery uzantısı dahil olmak üzere, herhangi bir VM uzantısı kullanılarak için önkoşul hello sanal makine karşılar. yalnızca hello Mobility hizmeti hello üzerinde yüklü makine geçirdiyseniz el ile yüklenen hello Azure VM Aracısı gereksinimlerini toobe 9.6 veya önceki bir sürümü var.

Merhaba aşağıdaki tabloda hello VM Aracısı yükleme ve yüklü olduğu doğrulanıyor hakkında ek bilgi sağlar:

| **İşlem** | **Windows** | **Linux** |
| --- | --- | --- |
| Merhaba VM Aracısı yükleniyor |Merhaba yükleyip [aracı MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Yönetici ayrıcalıkları toocomplete hello yüklemesi gerekir. |Merhaba son yükleme [Linux Aracısı](../virtual-machines/linux/agent-user-guide.md). Yönetici ayrıcalıkları toocomplete hello yüklemesi gerekir. Dağıtım depodan hello aracı yüklemenizi öneririz. Biz *değil önerilir* doğrudan Github'dan hello Linux VM Aracısı yükleme.  |
| Merhaba VM Aracısı yüklemesini doğrulama |1. Hello Azure VM toohello C:\WindowsAzure\Packages klasörüne göz atın. Görmeniz gerekir hello WaAppAgent.exe dosyasını. <br>2. Merhaba dosyaya sağ tıklayın, çok Git**özellikleri**seçip hello **ayrıntıları** sekmesini hello **ürün sürümü** alanı 2.6.1198.718 olmalıdır ya da daha yüksek. |Yok |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a>3. adım: Sanal makine Kaldır hello hello Mobility hizmetinden geçişi

Şirket içi VMware makineleri veya fiziksel Windows/Linux sunucularda geçirdiyseniz, toomanually kaldırmak/hello Mobility hizmetinden hello geçirilen sanal makine gerekir.

>[!IMPORTANT]
>Bu adım için Hyper-V sanal makineleri geçirilen tooAzure gerekli değildir.

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a>Windows Server VM üzerinde Hello Mobility hizmetini kaldırma
Bir Windows Server bilgisayarında yöntemleri toouninstall hello Mobility hizmeti aşağıdaki hello birini kullanın.

##### <a name="uninstall-by-using-hello-windows-ui"></a>Merhaba Windows kullanıcı arabirimini kullanarak kaldırma
1. Hello Denetim Masası'da, seçin **programlar**.
2. Seçin **Microsoft Azure Site Recovery Mobility hizmeti/ana hedef sunucu**ve ardından **kaldırma**.

##### <a name="uninstall-at-a-command-prompt"></a>Bir komut isteminde kaldırma
1. Yönetici olarak bir komut istemi penceresi açın.
2. toouninstall Mobility hizmeti Merhaba, hello aşağıdaki komutu çalıştırın:

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a>Bir Linux bilgisayarda Hello Mobility hizmetini kaldırma
1. Linux sunucunuzda olarak oturum açın bir **kök** kullanıcı.
2. Bir terminale çok/kullanıcı/yerel/ASR gidin.
3. toouninstall Mobility hizmeti Merhaba, hello aşağıdaki komutu çalıştırın:

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a>4. adım: hello VM yeniden başlatma

Merhaba Mobility hizmeti kaldırdıktan sonra önce yeniden başlatma hello VM çoğaltma tooanother Azure bölgesi ayarlayın.


## <a name="next-steps"></a>Sonraki adımlar
- İş yükleri tarafından korumaya başlamak [Azure sanal makineleri çoğaltmak](site-recovery-azure-to-azure.md).
- Daha fazla bilgi edinmek [Azure sanal makineleri çoğaltmak için kılavuz ağ](site-recovery-azure-to-azure-networking-guidance.md).
