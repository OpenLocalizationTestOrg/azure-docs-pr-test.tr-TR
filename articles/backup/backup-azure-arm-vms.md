---
title: Azure Vm'leri yedekleme aaaBack | Microsoft Docs
description: "Bul kaydolun ve Azure sanal makineleri tooa kurtarma Hizmetleri kasasını yedekleyin."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "sanal makine yedeklemesi; sanal makineyi geri; Yedekleme ve olağanüstü durum kurtarma; ARM vm yedekleme"
ms.assetid: 5c68481d-7be3-4e68-b87c-0961c267053e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: trinadhk;jimpark;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a204a42726450a7fd89b5563a786b5070578b113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-tooa-recovery-services-vault"></a>Geri Azure sanal makinelerini tooa kurtarma Hizmetleri kasası
> [!div class="op_single_selector"]
> * [Sanal makineleri tooRecovery Hizmetleri kasasını yedekleyin](backup-azure-arm-vms.md)
> * [Sanal makineleri tooBackup kasasını yedekleyin](backup-azure-vms.md)
>
>

Bu makalede nasıl tooback yukarı Azure VM'ler (Resource Manager tarafından dağıtılan ve klasik dağıtılan) tooa kurtarma Hizmetleri kasası ayrıntıları verilmektedir. Vm'leri yedekleme için hello çalışmanın çoğu hello hazırlık olur. Yedeklemek veya VM koruma önce hello tamamlamalısınız [Önkoşullar](backup-azure-arm-vms-prepare.md) tooprepare Vm'lerinizi koruma için ortamınızı. Merhaba önkoşulları tamamladıktan sonra hello yedekleme işlemi tootake VM anlık görüntülerini işlemi başlatabilirsiniz.


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

Daha fazla bilgi için üzerinde hello makalelerine bakın [azure'da VM yedekleme altyapınızı planlama](backup-azure-vms-introduction.md) ve [Azure sanal makineleri](https://azure.microsoft.com/documentation/services/virtual-machines/).

## <a name="triggering-hello-backup-job"></a>Tetikleyici hello yedekleme işi
Kurtarma Hizmetleri kasası hello ile ilişkili hello yedekleme İlkesi hello Yedekleme işleminin ne sıklıkta ve ne zaman çalışması tanımlar. Varsayılan olarak, ilk zamanlanmış yedekleme hello hello ilk yedeklemedir. Merhaba ilk yedekleme gerçekleşene kadar son yedekleme durumu hello üzerinde hello **yedekleme işleri** dikey gösterildiğinden **uyarı (ilk yedekleme bekleme)**.

![Yedekleme beklemede](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

İlk yedeklemeniz son olmadığı sürece toobegin yakında önerilir, çalıştırmanız **Şimdi Yedekle**. Merhaba aşağıdaki yordamı hello kasası panodan başlatır. Bu yordam, tüm önkoşullar tamamladıktan sonra hello ilk yedekleme işini çalıştırmak için görev yapar. Merhaba ilk yedekleme işi zaten çalıştırıldıysa, bu yordam kullanılabilir değil. Merhaba ilişkili yedekleme İlkesi hello sonraki yedekleme işini belirler.  

toorun hello ilk yedekleme işini:

1. Merhaba kasa Panosu üzerinde hello numarasını altında tıklatın **yedekleme öğeleri**, veya hello **yedekleme öğeleri** döşeme. <br/>
  ![Ayarlar simgesi](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)

  Merhaba **yedekleme öğeleri** dikey pencere açılır.

  ![Öğeleri yedekleme](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. Merhaba üzerinde **yedekleme öğeleri** dikey penceresinde, select hello öğesi.

  ![Ayarlar simgesi](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  Merhaba **yedekleme öğeleri** listesi açılır. <br/>

  ![Tetiklenmiş yedekleme işi](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. Merhaba üzerinde **yedekleme öğeleri** listesinde, hello üç noktaya tıklayın **...**  tooopen hello bağlam menüsü.

  ![Bağlam menüsü](./media/backup-azure-vms-first-look-arm/context-menu.png)

  Merhaba bağlam menüsü görüntülenir.

  ![Bağlam menüsü](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. Merhaba bağlam menüsünde **Şimdi Yedekle**.

  ![Bağlam menüsü](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  Merhaba Şimdi Yedekle dikey pencere açılır.

  ![Merhaba Şimdi Yedekle dikey gösterir](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. Merhaba Şimdi Yedekle dikey penceresinde hello takvim simgesini tıklatın, hello Takvim denetimi tooselect hello bu kurtarma noktası korunur ve tıklatın son günü kullanın **yedekleme**.

  ![set hello son gün hello Şimdi Yedekle kurtarma noktası korunur](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Dağıtım bildirimleri hello yedekleme işi tetiklenir ve hello işinin ilerleme durumunu hello hello yedekleme işleri sayfasında izleyebilirsiniz size bildirmek. VM Hello boyutuna bağlı olarak, hello ilk yedek oluşturulması biraz zaman alabilir.

6. Merhaba üzerinde hello kasa Panosu üzerinde hello ilk yedekleme tooview veya iz hello durumunu **yedekleme işleri** döşeme tıklatın **devam eden**.

  ![Yedekleme İşleri kutucuğu](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  Merhaba yedekleme işleri dikey penceresi açılır.

  ![Yedekleme İşleri kutucuğu](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  Merhaba, **yedekleme işleri** dikey penceresinde hello tüm işlerin durumunu görebilirsiniz. Merhaba, VM için yedekleme işi devam ediyor veya sona erdi kontrol edin. Bir yedekleme işi tamamlandığında, hello durumudur *tamamlandı*.

  > [!NOTE]
  > Merhaba Yedekleme işleminin bir parçası olarak bir komut toohello yedekleme uzantısına tüm yazar ve tutarlı bir anlık görüntüsünü her VM tooflush hello Azure Backup hizmeti verir.
  >
  >

## <a name="troubleshooting-errors"></a>Sorun giderme
Sanal makineniz yedekleme sırasında sorunları içine çalıştırırsanız hello bkz [VM sorun giderme makalesi](backup-azure-vms-troubleshoot.md) Yardım.

## <a name="next-steps"></a>Sonraki adımlar
VM korumalı, makaleler toolearn VM yönetim görevleri hakkında aşağıdaki hello bakın ve nasıl toorestore VM'ler.

* [Sanal makinelerinizi yönetme ve izleme](backup-azure-manage-vms.md)
* [Sanal makineleri geri yükleme](backup-azure-arm-restore-vms.md)
