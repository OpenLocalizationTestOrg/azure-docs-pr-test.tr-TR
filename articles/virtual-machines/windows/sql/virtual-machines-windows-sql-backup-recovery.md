---
title: "aaaBackup ve SQL Server için geri yükleme | Microsoft Docs"
description: "Azure sanal makinelerde çalışan SQL Server veritabanları için yedekleme ve geri yükleme noktaları açıklar."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-management
ms.assetid: 95a89072-0edf-49b5-88ed-584891c0e066
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 11/15/2016
ms.author: mikeray
ms.openlocfilehash: f85248fecdd5867d91d09650a1a34ad7c7caa920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore-for-sql-server-in-azure-virtual-machines"></a>Azure Sanal Makineler’de SQL Server için Yedekleme ve Geri Yükleme
## <a name="overview"></a>Genel Bakış
Azure depolama, veri kaybı veya fiziksel veri bozulmasına karşı her Azure VM disk tooguarantee koruma 3 kopyasını tutar. Bu nedenle, şirket içi farklı olarak, bunlar hakkında tooworry gerek yoktur. Ancak, uygulama veya kullanıcıya hataları (yanlış veri ekleme ya da bir tablo silme örneğin) karşı SQL Server veritabanları tooprotect hala yedeklemeniz gerekir ve mümkün toorestore olan tooa bir nokta.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Azure Vm'lerinde çalışan SQL Server için yerel yedekleme kullanın ve teknikleri hello yedekleme dosyalarını hello hedef için kullanıma açılan diskler kullanarak geri yükleyin. Ancak, bir toohello sayısı sınırı tooan Azure sanal makinesi üzerinde hello dayalı iliştirebilirsiniz diskleri yoktur [hello sanal makine boyutu](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Disk yönetimi tooconsider hello yükünü yoktur.

SQL Server 2014 ile başlayarak, yedekleme ve tooMicrosoft Azure Blob Depolama geri yükleyin. SQL Server 2016 de bu seçenek için geliştirmeler içerir. Ayrıca, Microsoft Azure Blob depolamada depolanan veritabanı dosyaları için SQL Server 2016 bir seçenek neredeyse anlık yedeklemeler için ve Azure anlık görüntülerini kullanarak hızlı geri yüklemeler için sağlar. Bu makalede bu seçeneklerine genel bakış sağlar ve ek bilgiler bulunabilir [SQL Server Yedekleme ve geri yükleme ile Microsoft Azure Blob Depolama hizmetinin](https://msdn.microsoft.com/library/jj919148.aspx).

> [!NOTE]
> Çok büyük veritabanlarını yedekleme için başlangıç seçeneklerini tartışma için bkz [çoklu terabayt SQL Server veritabanı yedekleme stratejilerini Azure Virtual Machines için](http://blogs.msdn.com/b/igorpag/archive/2015/07/28/multi-terabyte-sql-server-database-backup-strategies-for-azure-virtual-machines.aspx).
> 
> 

Aşağıdaki bölümler Hello bilgi belirli toohello farklı sürümleri bir Azure sanal makinesi desteklenen bir SQL Server içerir.

## <a name="sql-server-virtual-machines"></a>SQL Server sanal makineler
Bir Azure sanal makinesinde SQL Server örneğinizi çalıştırırken, veritabanı dosyalarınızı veri disklerde Azure'da zaten bulunur. Bu diskleri Azure Blob depolama alanına dinamik. Bu nedenle hello veritabanı ve hello yaklaşımlar yedekleme biraz değişiklik etkin nedenleri. Merhaba aşağıdakileri göz önünde bulundurun. 

* Microsoft Azure hello Microsoft Azure hizmet parçası olarak bu koruma sağladığından, artık tooperform veritabanı yedeklemeleri tooprovide koruması donanım ve medya arızasına karşı gerekir.
* Yine tooperform veritabanı yedeklemeleri tooprovide Koruması kullanıcı hataları karşı ya da arşivleme amacıyla, yasal nedenlerden veya yönetim amacıyla gerekir.
* Doğrudan Azure'da hello yedekleme dosyası depolayabilirsiniz. Daha fazla bilgi için SQL Server'ın farklı sürümleri hello için kılavuzluk bölümleri aşağıdaki hello bakın.

## <a name="sql-server-2016"></a>SQL Server 2016
Microsoft SQL Server 2016 destekleyen [yedekleme ve geri yükleme ile Azure BLOB'ları](https://msdn.microsoft.com/library/jj919148.aspx) özellikleri SQL Server 2014'te bulundu. Ancak, ayrıca hello aşağıdaki geliştirmeleri içerir:

| 2016 geliştirme | Ayrıntılar |
| --- | --- |
| **Şeritleme** |Azure blob depolama tooMicrosoft yedeklerken, SQL Server 2016 12,8 TB tooa maksimum yukarı büyük veritabanlarını yedeklemek toomultiple BLOB'lar tooenable yedekleme destekler. |
| **Anlık görüntü yedekleme** |Azure anlık görüntüleri Hello kullanımla neredeyse anlık yedeklemeler ve hızlı geri yüklemeler hello Azure Blob Depolama hizmetini kullanarak depolanan veritabanı dosyaları için SQL Server dosya anlık görüntüsü yedekleme sağlar. Bu özellik, toosimplify yedekleme ve geri yükleme ilkelerinizi sağlar. Dosya anlık görüntüsü yedekleme, geri yükleme noktası da destekler. Daha fazla bilgi için bkz: [azure'da veritabanı dosyaları için anlık görüntü yedeklerini](https://msdn.microsoft.com/library/mt169363%28v=sql.130%29.aspx). |
| **Yedekleme zamanlaması yönetilen** |SQL Server yönetilen yedekleme tooAzure artık özel zamanlamaları destekler. Daha fazla bilgi için bkz: [SQL Server yönetilen yedekleme tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx). |

Azure Blob Depolama kullanırken SQL Server 2016 hello yeteneklerini öğretici için bkz [Öğreticisi: SQL Server 2016 veritabanlarıyla hello Microsoft Azure Blob Depolama hizmetinin kullanarak](https://msdn.microsoft.com/library/dn466438.aspx).

## <a name="sql-server-2014"></a>SQL Server 2014
SQL Server 2014 hello aşağıdaki geliştirmeleri içerir:

1. **Yedekleme ve geri yükleme tooAzure**:
   
   * *SQL Server Yedekleme tooURL* desteği SQL Server Management Studio'da artık sahiptir. Merhaba seçeneği tooback tooAzure yukarı SQL Server Management Studio'da yedekleme veya geri yükleme görev ya da bakım planı oluşturma sihirbazını kullanırken, kullanıma sunulmuştur. Daha fazla bilgi için bkz: [SQL Server Yedekleme tooURL](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx).
   * *SQL Server yönetilen yedekleme tooAzure* otomatik yedekleme yönetim sağlayan yeni işlevselliğe sahiptir. Bir Azure makinede çalışan SQL Server 2014 örnekleri için Yedekleme Yönetimi otomatikleştirmek için özellikle yararlıdır. Daha fazla bilgi için bkz: [SQL Server yönetilen yedekleme tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496%28v=sql.120%29.aspx).
   * *Otomatik yedekleme* ek Otomasyon tooautomatically etkinleştir sağlar *SQL Server yönetilen yedekleme tooAzure* tüm mevcut ve yeni veritabanları için azure'da bir SQL Server VM üzerinde. Daha fazla bilgi için bkz. [Azure Virtual Machines’de SQL Server için Otomatik Yedekleme](virtual-machines-windows-sql-automated-backup.md).
   * SQL Server 2014 yedekleme tooAzure için tüm hello seçeneklerine genel bakış için bkz: [SQL Server Yedekleme ve geri yükleme ile Microsoft Azure Blob Depolama hizmetinin](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx).
2. **Şifreleme**: SQL Server 2014'ü destekleyen bir yedek oluştururken veri şifreleme. Birçok şifreleme algoritmalarını destekler ve bir sertifika veya asimetrik anahtar osf hello kullanın. Daha fazla bilgi için bkz: [yedekleme şifreleme](https://msdn.microsoft.com/library/dn449489%28v=sql.120%29.aspx).

## <a name="sql-server-2012"></a>SQL Server 2012
SQL Server Yedekleme ve geri yükleme SQL Server 2012'de hakkında ayrıntılı bilgi için bkz: [yedekleme ve geri yükleme, SQL Server veritabanları (SQL Server 2012)](https://msdn.microsoft.com/library/ms187048%28v=sql.110%29.aspx).

SQL Server 2012 SP1 toplu güncelleştirme 2'de başlayarak, Azure Blob Depolama hizmetinin hello tooand geri yükleme yedekleyebilirsiniz. Bu geliştirme, bir Azure sanal makine veya bir şirket içi örneği üzerinde çalışan bir SQL Server üzerinde SQL Server veritabanlarını kullanılan tooback olabilir. Daha fazla bilgi için bkz: [SQL Server Yedekleme ve geri yükleme ile Azure Blob Depolama hizmetinin](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx).

Bazı hello Azure Blob Depolama hizmetinin kullanmanın yararları hello hello özelliği toobypass hello 16 disk sınırını bağlı diskler, yönetim, hello doğrudan hello yedekleme dosyası tooanother örnek bir Azure üzerinde çalışan SQL Server örneğinin kullanılabilirliğini kolaylığı içerir sanal makine veya şirket içi örneğini geçiş veya olağanüstü durum kurtarma amacıyla. Merhaba avantajları toousing bir Azure blob depolama hizmetinin SQL Server yedekleri için tam bir listesi için bkz *avantajları* bölümüne [SQL Server Yedekleme ve geri yükleme ile Azure Blob Depolama hizmetinin](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx).

En iyi uygulama önerileri ve sorun giderme bilgileri için bkz: [yedekleme ve geri yükleme en iyi yöntemler (Azure Blob Depolama hizmetinin)](https://msdn.microsoft.com/library/jj919149%28v=sql.110%29.aspx).

## <a name="sql-server-2008"></a>SQL Server 2008
SQL Server Yedekleme ve geri yükleme SQL Server 2008 R2 için bkz: [yedekleme ve geri yükleme veritabanlarını SQL Server (SQL Server 2008 R2)](https://msdn.microsoft.com/library/ms187048%28v=sql.105%29.aspx).

SQL Server Yedekleme ve geri yükleme SQL Server 2008 için bkz: [yedekleme ve geri yükleme veritabanlarını SQL Server (SQL Server 2008)](https://msdn.microsoft.com/library/ms187048%28v=sql.100%29.aspx).

## <a name="next-steps"></a>Sonraki adımlar
Dağıtımınızı Azure VM'deki SQL Server'ın planlıyorsanız, öğreticiyi izleyerek hello sağlama yönergeler bulabilirsiniz: [Azure Resource Manager ile Azure SQL Server sanal makineye sağlama](virtual-machines-windows-portal-sql-server-provision.md).

Ancak yedekleme ve geri yükleme kullanılan toomigrate verilerinizi olabilir, potansiyel olarak daha kolay veri geçiş yolları tooSQL bir Azure VM sunucuda vardır. Geçiş seçenekleri ve öneriler tam bir tartışma için bkz: [veritabanı tooSQL bir Azure VM sunucuda geçiş](virtual-machines-windows-migrate-sql.md).

Diğer gözden [SQL Server Azure sanal makinelerde çalışan kaynakları](virtual-machines-windows-sql-server-iaas-overview.md).

