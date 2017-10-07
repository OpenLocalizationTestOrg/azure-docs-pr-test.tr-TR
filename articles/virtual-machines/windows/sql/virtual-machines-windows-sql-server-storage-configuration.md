---
title: "SQL Server VM'ler için aaaStorage yapılandırma | Microsoft Docs"
description: "Bu konu, nasıl Azure depolama için SQL Server Vm'lerinin (Resource Manager dağıtım modeli) sağlama sırasında yapılandırır açıklar. Ayrıca, depolama, var olan SQL Server VM'ler için nasıl yapılandırabileceğiniz açıklanmaktadır."
services: virtual-machines-windows
documentationcenter: na
author: ninarn
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 169fc765-3269-48fa-83f1-9fe3e4e40947
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: ninarn
ms.openlocfilehash: b50dbd698828780cfc044fa0966e8f4e2f3bb6c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storage-configuration-for-sql-server-vms"></a>SQL Server VM'ler için depolama yapılandırması
Azure'da bir SQL Server sanal makine görüntüsü yapılandırdığınızda hello Portal tooautomate depolama yapılandırmanıza yardımcı olur. Bu depolama toohello o depolama erişilebilir tooSQL sunucu yapma ve belirli bir performans gereksinimlerinizi toooptimize yapılandırma VM ekleme içerir.

Bu konu, nasıl Azure depolama, SQL Server VM'ler için sağlama sırasında hem var olan VM'ler için yapılandırır açıklar. Bu yapılandırma üzerinde hello dayalıdır [performansı en iyi uygulamaları](virtual-machines-windows-sql-performance.md) Azure SQL Server çalıştıran VM'ler için.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Ön koşullar
toouse hello depolama yapılandırma ayarlarını otomatik, sanal makinenizin özelliklerini aşağıdaki hello gerektirir:

* İle sağlanan bir [SQL Server galeri görüntüsü](virtual-machines-windows-sql-server-iaas-overview.md#option-1-create-a-sql-vm-with-per-minute-licensing).
* Kullandığı hello [Resource Manager dağıtım modeli](../../../azure-resource-manager/resource-manager-deployment-model.md).
* Kullanan [Premium depolama](../../../storage/common/storage-premium-storage.md).

## <a name="new-vms"></a>Yeni sanal makineleri
Merhaba aşağıdaki bölümlerde nasıl tooconfigure depolama yeni SQL Server sanal makineler için.

### <a name="azure-portal"></a>Azure Portal
Bir SQL Server galeri görüntüsü kullanarak bir Azure VM ayrılırken seçebileceğiniz tooautomatically hello depolama yeni VM için yapılandırın. Merhaba depolama boyutunu, performans sınırlarını ve iş yükü türünü belirtin. Merhaba aşağıdaki ekran görüntüsü SQL VM sırasında kullanılan hello depolama yapılandırma dikey sağlama gösterir.

![Sağlama sırasında SQL Server VM depolama yapılandırması](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-provisioning.png)

Üzerinde yaptığınız seçimlere göre Azure depolama yapılandırma görevleri hello VM oluşturduktan sonra aşağıdaki hello gerçekleştirir:

* Oluşturur ve premium depolama veri diskleri toohello sanal makineye iliştirir.
* Merhaba veri diskleri toobe erişilebilir tooSQL sunucusu yapılandırır.
* Bir depolama alanına Hello veri diskleri yapılandırır hello üzerinde temel havuzu belirtilen boyutu ve performans (IOPS ve üretilen iş) gereksinimleri.
* Merhaba depolama havuzu hello sanal makine üzerinde yeni bir sürücü ilişkilendirir.
* (Veri ambarı hareket işleme veya genel), belirtilen iş yükü türüne bağlı olarak bu yeni bir sürücüye en iyi duruma getirir.

Merhaba nasıl Azure depolama ayarlarını yapılandırır hakkında daha fazla ayrıntı için bkz: [depolama yapılandırma bölümü](#storage-configuration). Toocreate SQL Server VM hello Azure Portal ile nasıl görürüm tam bir kılavuz [öğretici sağlama hello](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="resource-manage-templates"></a>Kaynak Yönet şablonları
Resource Manager şablonları aşağıdaki hello kullanırsanız, iki premium diskleri varsayılan olarak, hiçbir depolama havuzu yapılandırması ile ilişkilendirilir. Ancak, ekli toohello sanal makine premium veri disklerinin bu şablonları toochange hello sayısını özelleştirebilirsiniz.

* [Otomatik yedekleme ile VM oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autobackup)
* [Otomatik düzeltme eki uygulama ile VM oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autopatching)
* [AKV tümleştirme ile VM oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-keyvault)

## <a name="existing-vms"></a>Var olan sanal makineleri
Var olan SQL Server VM'ler için hello Azure portal bazı depolama ayarlarını değiştirebilirsiniz. VM'yi seçin, toohello ayarlar alanına gidin ve ardından SQL Server yapılandırma seçin. Merhaba SQL Server yapılandırma dikey penceresinde hello geçerli depolama kullanımı vm'nizin gösterir. VM'ın mevcut tüm sürücülerde Bu grafikte görüntülenir. Her bir sürücü için dört bölümlerde hello depolama alanı görüntüler:

* SQL veri
* SQL günlüğü
* Diğer (SQL dışı depolama)
* Kullanılabilir

![Var olan SQL Server VM için depolama yapılandırma](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-existing.png)

tooconfigure depolama tooadd yeni bir sürücüye Merhaba veya var olan sürücüsüne genişletmek, hello grafik yukarıda hello Düzenle bağlantısına tıklayın.

Bu özellik önce olup olmadığını kullanmış bağlı olarak değişir bkz hello yapılandırma seçenekleri. Merhaba ilk kez kullanırken, depolama gereksinimleriniz için yeni bir sürücü belirtebilirsiniz. Bu özellik toocreate bir sürücü daha önce kullandıysanız, sürücünün depolama tooextend seçebilirsiniz.

### <a name="use-for-hello-first-time"></a>Merhaba ilk kez kullanıma
Bu özelliği kullanarak ilk kez doğruysa, belirtebilmeniz için yeni bir sürücü için depolama boyutu ve performans sınırlarını hello. Zaman sağlama sırasında göreceğiniz benzer toowhat deneyimidir. Merhaba ana toospecify hello iş yükü türüne izin verilmiyor farktır. Bu kısıtlama, var olan tüm SQL Server yapılandırmaları hello sanal makinedeki kesintiye engeller.

![SQL Server depolama kaydırıcılar yapılandırın](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-usage-sliders.png)

Azure, belirtimlere bağlı yeni bir sürücüye oluşturur. Bu senaryoda, Azure depolama yapılandırma görevleri aşağıdaki hello gerçekleştirir:

* Oluşturur ve premium depolama veri diskleri toohello sanal makineye iliştirir.
* Merhaba veri diskleri toobe erişilebilir tooSQL sunucusu yapılandırır.
* Bir depolama alanına Hello veri diskleri yapılandırır hello üzerinde temel havuzu belirtilen boyutu ve performans (IOPS ve üretilen iş) gereksinimleri.
* Merhaba depolama havuzu hello sanal makine üzerinde yeni bir sürücü ilişkilendirir.

Merhaba nasıl Azure depolama ayarlarını yapılandırır hakkında daha fazla ayrıntı için bkz: [depolama yapılandırma bölümü](#storage-configuration).

### <a name="add-a-new-drive"></a>Yeni bir sürücü ekleyin
SQL Server VM'nize depolama zaten yapılandırdıysanız, depolama alanını genişletmeyi iki yeni seçeneklerini getirir. Merhaba ilk tooadd VM hello performans düzeyini artırabilirsiniz yeni bir sürücüye seçenektir.

![Yeni bir sürücü tooa SQL VM ekleme](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-add-new-drive.png)

Ancak, hello sürücü eklendikten sonra bazı ek el ile yapılandırma tooachieve hello performans artışı gerçekleştirmeniz gerekir.

### <a name="extend-hello-drive"></a>Merhaba sürücü genişletme
Merhaba depolama alanını genişletmeyi için başka bir seçeneğin tooextend hello varolan sürücüdür. Hello kullanılabilir depolama alanı sürücünüz için bu seçeneği artırır, ancak performans artırmaz. Depolama havuzlarıyla Hello depolama havuzu oluşturulduktan sonra hello sütun sayısı değiştirilemiyor. sütun sayısı Hello hello veri disklere yayılarak paralel yazma hello sayısını belirler. Bu nedenle, olan ek veri disklerinin performans artırılamıyor. Bunlar yalnızca yazılan hello veri için daha fazla depolama alanı sağlayabilir. Bu sınırlama hello sürücü genişletirken hello sütun sayısı hello minimum ekleyebileceğiniz veri diski sayısı belirlediğini anlamına gelir. Dört veri diskleri ile bir depolama havuzunda oluşturursanız, bu nedenle hello sütunları da dört sayısıdır. Merhaba depolama, genişletmek istediğiniz zaman, en az dört veri diskleri eklemeniz gerekir.

![Bir sürücü için bir SQL VM genişletme](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-extend-a-drive.png)

## <a name="storage-configuration"></a>Depolama yapılandırması
Bu bölümde, Azure SQL VM sağlama veya hello Azure Portal yapılandırması sırasında otomatik olarak gerçekleştirir hello depolama yapılandırma değişiklikleri için bir başvuru sağlar.

* Azure VM için depolama ikiden TBs seçtiyseniz, depolama havuzu oluşturmaz.
* VM için en az iki TBs depolama seçtiyseniz, Azure depolama havuzu yapılandırır. Bu konunun sonraki bölümlerinde Hello hello depolama havuzu yapılandırması hello ayrıntılarını sağlar.
* Her zaman otomatik depolama yapılandırmasını kullanan [premium depolama](../../../storage/common/storage-premium-storage.md) P30 veri diski. Sonuç olarak, 1:1 eşleme terabayt seçili sayısı arasında ve veri diski sayısı hello tooyour VM bağlı.

Merhaba fiyatlandırma bilgileri için bkz: [depolama fiyatlandırma](https://azure.microsoft.com/pricing/details/storage) hello sayfasında **Disk Depolama** sekmesi.

### <a name="creation-of-hello-storage-pool"></a>Merhaba depolama havuzu oluşturma
Azure SQL Server Vm'lerinde ayarları toocreate hello depolama havuzu aşağıdaki hello kullanır.

| Ayar | Değer |
| --- | --- |
| Şerit boyutu |256 KB (veri ambarı); 64 KB (işlem) |
| Disk boyutları |1 TB |
| Önbellek |Okuma |
| Ayırma boyutu |64 KB NTFS ayırma birimi boyutu |
| Anında dosya başlatma |Etkin |
| Bellekteki sayfaları kilitle |Etkin |
| Kurtarma |Basit kurtarma (esnekliği yok) |
| Sütun sayısı |Veri diski sayısı<sup>1</sup> |
| TempDB konumu |Veri disklerinde depolanan<sup>2</sup> |

<sup>1</sup> hello depolama havuzu oluşturulduktan sonra hello hello depolama havuzundaki sütun sayısı değiştirilemiyor.

<sup>2</sup> Bu ayar yalnızca hello depolama yapılandırma özelliğini kullanarak oluşturduğunuz ilk sürücü toohello geçerlidir.

## <a name="workload-optimization-settings"></a>İş yükü iyileştirme ayarları
Merhaba aşağıdaki tabloda hello üç iş yükü türü seçenekleri ve bunların karşılık gelen iyileştirmeler açıklanmaktadır:

| İş yükü türü | Açıklama | En iyi duruma getirme |
| --- | --- | --- |
| **Genel** |Çoğu iş yükünü destekler varsayılan ayarı |None |
| **İşlem işleme** |Merhaba depolama geleneksel veritabanı OLTP iş yükleri için en iyi duruma getirir |İzleme bayrağı 1117<br/>İzleme bayrağı 1118 |
| **Veri ambarı** |Merhaba depolama çözümleme ve raporlama iş yükleri için en iyi duruma getirir |İzleme bayrağı 610<br/>İzleme bayrağı 1117 |

> [!NOTE]
> Merhaba depolama yapılandırması adımda seçerek SQL sanal makinesi sağladığınızda, yalnızca hello iş yükü türünü belirtebilirsiniz.
>
>

## <a name="next-steps"></a>Sonraki adımlar
Azure vm'lerinde SQL Server toorunning ilgili diğer konular için bkz: [Azure Virtual Machines'de SQL Server](virtual-machines-windows-sql-server-iaas-overview.md).
