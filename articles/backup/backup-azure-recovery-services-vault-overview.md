---
title: "Kurtarma Hizmetleri kasalarının aaaOverview | Microsoft Docs"
description: "Genel bir bakış ve kurtarma Hizmetleri kasalarının ve Azure yedekleme kasaları karşılaştırması."
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.assetid: 38d4078b-ebc8-41ff-9bc8-47acf256dc80
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/15/2017
ms.author: markgal;arunak
ms.openlocfilehash: 77dd9ece7fe86429cc6f9a47a68b5150a1f4af71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vaults-overview"></a>Kurtarma Hizmetleri kasaları genel bakış

Bu makalede, bir kurtarma Hizmetleri kasası hello özelliklerini açıklar. Kurtarma Hizmetleri kasası veri barındırıldığı Azure depolama varlıktır. Merhaba genellikle veri ya da sanal makineleri (VM'ler), iş yükleri, sunucular veya iş istasyonları için yapılandırma bilgilerini kopyalarını verilerdir. Kurtarma Hizmetleri kasası hello Resource Manager, bir yedekleme kasası sürümüdür. Microsoft önerir, size, toouse kurtarma Hizmetleri kasalarının ve tooconvert tooRecovery Hizmetleri kasalarının herhangi bir yedekleme kasaları.

## <a name="what-is-a-recovery-services-vault"></a>Kurtarma Hizmetleri kasası nedir?

Kurtarma Hizmetleri kasası Azure çevrimiçi depolama varlık toohold veri yedek kopyaları, Kurtarma noktaları ve yedekleme ilkeleri gibi kullanılır. Iaas VM'ler (Linux veya Windows) ve Azure SQL veritabanları gibi çeşitli Azure hizmetlerine kurtarma Hizmetleri kasaları toohold yedekleme verilerini kullanabilirsiniz. Kurtarma Hizmetleri kasaları destek System Center DPM, Windows Server, Azure yedekleme sunucusu ve daha fazlası. Kurtarma Hizmetleri kasaları kolay tooorganize sunun yönetim yükünü en aza çalışırken, yedekleme verilerinizi.

Bir Azure aboneliği istediğiniz sayıda kurtarma Hizmetleri kasalarının oluşturabilirsiniz.

## <a name="comparing-recovery-services-vaults-and-backup-vaults"></a>Karşılaştırma kurtarma Hizmetleri kasaları ve yedekleme kasaları

Yedekleme kasaları hello Azure Service Manager modele dayalı ancak kurtarma Hizmetleri kasaları üzerinde Azure, hello Azure Resource Manager modelini temel alır. Bir yedekleme kasası tooa kurtarma Hizmetleri kasası yükselttiğinizde hello yedek veri sırasında ve sonrasında hello yükseltme işlemi değişmeden kalır. Kurtarma Hizmetleri kasaları gibi yedekleme kasaları için kullanılamayan özellikleri sağlar:

- **Gelişmiş özellikleri toohelp güvenli yedekleme verilerini**: ile kurtarma Hizmetleri kasaları, Azure yedekleme sunar güvenlik özellikleri tooprotect bulut yedekleme. Bu güvenlik özellikleri Yedeklemelerinizin güvenli ve güvenli bir şekilde üretim ve yedekleme sunucuları tehlikeye olsa bile bulut yedeklemelerden veri kurtarmak emin olun. [Daha fazla bilgi](backup-azure-security-feature.md)

- **Karma BT ortamında Merkezi İzleme**: ile kurtarma Hizmetleri kasaları, izleyebilirsiniz yalnızca, [Azure Iaas Vm'leri](backup-azure-manage-vms.md) aynı zamanda, [içi varlıklar](backup-azure-manage-windows-server.md#manage-backup-items) merkezi bir gelen Portal. [Daha fazla bilgi](http://azure.microsoft.com/blog/alerting-and-monitoring-for-azure-backup)

- **Rol tabanlı erişim denetimi (RBAC)**: RBAC Azure ayrıntılı erişim yönetimi denetim sağlar. [Azure sağlayan çeşitli yerleşik roller](../active-directory/role-based-access-built-in-roles.md), ve Azure Backup sahip üç [yerleşik roller toomanage kurtarma noktaları](backup-rbac-rs-vault.md). Kurtarma Hizmetleri kasaları yedekleme kısıtlayan RBAC ile uyumludur ve erişim toohello tanımlanan kullanıcı rollerini kümesini geri yükleyin. [Daha fazla bilgi](backup-rbac-rs-vault.md)

- **Tüm yapılandırmaları Azure sanal makinelerin korunmasına**: Kurtarma Hizmetleri kasaları şunları korur Resource Manager tabanlı VM'ler Premium diskler, yönetilen diskleri ve şifrelenmiş VM'ler dahil olmak üzere. Bir yedekleme kasası tooa yükseltme, Service Manager tabanlı VM'ler tooResource Manager tabanlı VM'ler fırsat tooupgrade hello verir kurtarma Hizmetleri kasası. Merhaba kasası yükseltirken, Service Manager tabanlı VM kurtarma noktalarını korumak ve hello (Resource Manager etkin) VM'ler yükseltme için korumayı yapılandırın. [Daha fazla bilgi](http://azure.microsoft.com/blog/azure-backup-recovery-services-vault-ga)

- **Iaas VM'ler için anlık geri**: kullanarak kurtarma Hizmetleri kasaları, dosyaları geri yükleyebilir ve geri yükleme olmadan bir Iaas VM klasörlerinden hello daha hızlı geri yükleme süreleri sağlar tüm VM. Iaas VM'ler için anlık geri yükleme, Windows ve Linux VM'ler için kullanılabilir. [Daha fazla bilgi](http://azure.microsoft.com/blog/instant-file-recovery-from-azure-linux-vm-backup-using-azure-backup-preview)

## <a name="managing-your-recovery-services-vaults-in-hello-portal"></a>Merhaba Portalı'nda, Kurtarma Hizmetleri kasalarını yönetme
Oluşturulması ve kurtarma Hizmetleri kasalarının hello Azure portal, yönetimi kolay hello Backup hizmeti hello Azure ayarlar dikey tümleşik olduğundan. Bu tümleştirme oluşturmak veya bir kurtarma Hizmetleri kasası yönetmek anlamına gelir *hello hedef hizmet hello bağlamında*. Örneğin, bir VM için tooview hello kurtarma noktaları seçin ve tıklatın **yedekleme** hello ayarlar dikey penceresinde. Merhaba yedekleme bilgilerini belirli toothat VM görüntülenir. Örneğin, aşağıdaki hello içinde **ContosoVM** hello sanal makinenin hello adıdır. **ContosoVM demovault** kurtarma Hizmetleri kasası hello hello adıdır. Tooremember hello hello kurtarma noktalarını depolayan hello kurtarma Hizmetleri kasasının adını gerekmez, bu bilgileri hello sanal makineden erişebilir.  

![Kurtarma Hizmetleri kasası ayrıntıları VM](./media/backup-azure-recovery-services-vault-overview/rs-vault-in-context.png)

Birden çok sunucu hello kullanarak korunuyorsa aynı kurtarma Hizmetleri kasası, Kurtarma Hizmetleri kasası hello en fazla mantıksal toolook olabilir. Merhaba Abonelikteki tüm kurtarma Hizmetleri kasalarının aramak ve hello listesinden seçim yapın.

Merhaba aşağıdaki bölümler nasıl toouse bir kurtarma Hizmetleri kasası her etkinlik türünde açıklayan bağlantılar tooarticles içerir.

### <a name="back-up-data"></a>Verileri yedekleyin
- [Bir Azure VM'yi yedeklemek](backup-azure-vms-first-look-arm.md)
- [Windows Server veya Windows iş istasyonu yedekleyin](backup-try-azure-backup-in-10-mins.md)
- [DPM iş yüklerini tooAzure yedekleyin](backup-azure-dpm-introduction.md)
- [Azure yedekleme sunucusu kullanarak iş yüklerini tooback hazırlama](backup-azure-microsoft-azure-backup.md)

### <a name="manage-recovery-points"></a>Kurtarma noktalarını yönetin
- [Azure VM yedeklemeleri yönetme](backup-azure-manage-vms.md)
- [Dosyaları ve klasörleri yönetme](backup-azure-manage-windows-server.md)

### <a name="restore-data-from-hello-vault"></a>Merhaba kasadan veri geri yükleme
- [Tek tek dosyaların bir Azure sanal makineden kurtarma](backup-azure-restore-files-from-vm.md)
- [Bir Azure VM geri yükleme](backup-azure-arm-restore-vms.md)

### <a name="secure-hello-vault"></a>Güvenli hello kasası
- [Kurtarma Hizmetleri kasalarının bulut yedekleme verileri güvenli hale getirme](backup-azure-security-feature.md)



## <a name="next-steps"></a>Sonraki Adımlar
Makale için aşağıdaki hello kullan:</br>
[Bir Iaas VM'yi yedeklemek](backup-azure-arm-vms-prepare.md)</br>
[Bir Azure yedekleme sunucuyu yedekleme](backup-azure-microsoft-azure-backup.md)</br>
[Bir Windows Server'ı Yedekle](backup-configure-vault.md)
