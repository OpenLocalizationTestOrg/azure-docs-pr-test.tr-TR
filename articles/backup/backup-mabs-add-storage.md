---
title: Azure yedekleme sunucusu v2 ile Modern yedekleme depolama aaaUse | Microsoft Docs
description: "Azure yedekleme sunucusu v2 hello yeni özellikler hakkında bilgi edinin. Bu makalede nasıl tooupgrade yedekleme sunucusu yüklemenizi."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a>Depolama tooAzure yedekleme sunucusu v2 ekleme

Azure yedekleme sunucusu v2 System Center 2016 veri koruma Yöneticisi Modern yedekleme depolama ile birlikte gelir. Modern yedekleme depolama alanı yüzde 50, üç kez daha hızlı ve daha verimli depolama yedeklemeler depolama alanından tasarruf etmenizi sağlar. Ayrıca, iş yükü algılayan depolama sunar. 

> [!NOTE]
> toouse Modern yedekleme depolama, Windows Server 2016 yedekleme sunucusu v2 çalıştırmanız gerekir. Windows Server'ın önceki bir sürümünü yedekleme sunucusu v2 çalıştırırsanız, Azure yedekleme sunucusu Modern yedekleme depolama yararlanamaz. Bunun yerine, yedekleme sunucusu v1 ile yaptığı gibi iş yüklerini korur. Merhaba yedekleme sunucusu sürümü daha fazla bilgi için bkz: [koruma matris](backup-mabs-protection-matrix.md).

## <a name="volumes-in-backup-server-v2"></a>Yedek sunucu v2 birimleri

Yedek sunucu v2 depolama birimleri kabul eder. Bir birim eklediğinizde, yedekleme sunucusu hello birim tooResilient dosya Modern yedekleme depolama gerektiren sistemi (ReFS) biçimlendirir. tooadd bir birim ve tooexpand daha sonra gerekirse, bu iş akışı kullanmanızı öneririz:

1.  Bir VM üzerinde yedekleme sunucusu v2 ayarlayın.
2.  Bir depolama havuzunda bir sanal disk üzerinde bir birim oluşturun:
    1.  Bir disk tooa depolama havuzunu ekleyin ve Basit Düzen sanal disk oluşturma.
    2.  Ek bir disk ekleyin ve hello sanal diski genişletme.
    3.  Birim üzerindeki hello sanal diski oluşturun.
3.  Merhaba birimleri tooBackup sunucu ekleyin.
4.  İş yükü algılayan depolama yapılandırın.

## <a name="create-a-volume-for-modern-backup-storage"></a>Modern yedekleme depolama bir birim oluşturun

Yedekleme sunucusu v2 birimlerle kullanarak disk depolaması, depolama üzerinde denetim tutmanıza yardımcı olabilir. Bir birim, tek bir disk olabilir. Ancak, hello tooextend depolama gelecekteki istiyorsanız, depolama alanları kullanılarak oluşturulan bir disk dışında bir birim oluşturun. Yedekleme depolaması için tooexpand hello birim istiyorsanız bu yardımcı olabilir. Bu bölümde, bu kurulum ile bir birim oluşturmak için en iyi yöntemler sunar.

1. Sunucu Yöneticisi'nde seçin **dosya ve depolama hizmetleri** > **birimleri** > **depolama havuzları**. Altında **FİZİKSEL DİSKLER**seçin **yeni depolama havuzu**. 

    ![Yeni bir depolama havuzu oluşturma](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. Merhaba, **görevleri** açılan kutusunda **Yeni Sanal Disk**.

    ![Sanal disk ekleme](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. Merhaba depolama havuzunu seçin ve ardından **Fiziksel Disk Ekle**.

    ![Fiziksel disk ekleme](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. Merhaba fiziksel diski seçin ve ardından **sanal diski Genişlet**.

    ![Merhaba sanal diski Genişlet](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. Merhaba sanal diski seçin ve ardından **yeni birim**.

    ![Yeni bir birim oluşturun](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. Merhaba, **hello sunucu ve disk seçin** iletişim, select hello sunucu ve hello yeni disk. Ardından, seçin **sonraki**.

    ![Merhaba sunucu ve disk seçin](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a>Birimleri tooBackup Server disk depolama ekleme

tooadd hello bir birim tooBackup sunucu **Yönetim** bölmesinde hello depolama yeniden tarayın ve ardından **Ekle**. Tüm hello birimler kullanılabilir toobe yedekleme sunucusu depolama alanına eklenen listesi görüntülenir. Kullanılabilir birimleri toohello seçili birimlerin listesini eklendikten sonra bunları yönetmek bir kolay ad toohelp verebilirsiniz. Yedekleme sunucusu Modern yedekleme depolama hello yararları kullanabilmek için bu birimleri tooReFS seçin tooformat **Tamam**.

![Kullanılabilir birimleri ekleyin](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a>İş yükü algılayan depolama alanı ayarlama

İş yükü uyumlu depolama ile tercihen belirli türdeki iş yüklerini depolama hello birimleri seçebilirsiniz. Örneğin, çok sayıda sık, yüksek hacimli yedeklemeler gerektiren ikinci (IOPS) toostore yalnızca hello iş yükleri başına girdi/çıktı işlemleri destekleyen pahalı birimler ayarlayabilirsiniz. SQL Server ile işlem günlükleri örneğidir. Toolow maliyetli birimleri VM'ler gibi daha az sıklıkta yedeklenen diğer iş yükleri yedeklenebilir.

### <a name="update-dpmdiskstorage"></a>Güncelleştirme DPMDiskStorage

Data Protection Manager sunucusunda hello depolama havuzundaki bir birimin hello özelliklerini güncelleştiren güncelleştirme-DPMDiskStorage hello PowerShell cmdlet'ini kullanarak iş yükü algılayan depolama alanı ayarlayabilirsiniz.

Sözdizimi:

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
Merhaba aşağıdaki ekran görüntüsü hello güncelleştirme DPMDiskStorage cmdlet hello PowerShell penceresinde gösterir.

![Merhaba hello PowerShell penceresinde güncelleştirme DPMDiskStorage komutu](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

PowerShell kullanarak yaptığınız hello değişiklikler hello yedekleme Sunucu Yöneticisi konsolu yansıtılır.

![Diskleri ve birimleri hello Yönetici Konsolu](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a>Sonraki adımlar
Yedekleme sunucusu yükledikten sonra bilgi nasıl tooprepare sunucunuz veya bir iş yükü korumaya başlamak.

- [Yedekleme sunucusu iş yükleri hazırlama](backup-azure-microsoft-azure-backup.md)
- [Bir VMware sunucusu yedekleme sunucusu tooback kullanın](backup-azure-backup-server-vmware.md)
- [SQL Server Yedekleme Sunucusu tooback kullanın](backup-azure-sql-mabs.md)

