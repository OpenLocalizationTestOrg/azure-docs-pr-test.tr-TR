---
title: "bir SQL Server veritabanı tooSQL VM sunucuda aaaMigrate | Microsoft Docs"
description: "Nasıl toomigrate bir şirket içi kullanıcı veritabanı tooSQL sunucu bir Azure sanal makinesinde hakkında bilgi edinin."
services: virtual-machines-windows
documentationcenter: 
author: sabotta
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 00fd08c6-98fa-4d62-a3b8-ca20aa5246b1
ms.service: virtual-machines-sql
ms.workload: iaas-sql-server
ms.tgt_pltfrm: vm-windows-sql-server
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: carlasab
ms.openlocfilehash: 9c7aba30304ea40796412d2ddc885f6d4a58be2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-sql-server-database-toosql-server-in-an-azure-vm"></a>Bir SQL Server veritabanı tooSQL sunucusu Azure VM'deki geçirme

Bir şirket içi SQL Server kullanıcı veritabanı tooSQL sunucusu Azure VM'deki yöntemleri toomigrate dizi vardır. Bu makalede, kısa bir süre çeşitli yöntemlerle ele almaktadır ve hello en iyi yöntem çeşitli senaryolar için önerilir.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="what-are-hello-primary-migration-methods"></a>Merhaba birincil geçiş yöntemleri nelerdir?
Merhaba birincil geçiş yöntemler şunlardır:

* Azure sanal makinesi hello sıkıştırma ve el ile kopyalama hello yedekleme dosyası kullanarak şirket içi yedekleme gerçekleştirin
* Yedekleme tooURL gerçekleştirmek ve hello Azure sanal makinesi hello URL'den içine geri yükleme
* Ayırma ve hello veri ve günlük dosyaları tooAzure blob depolama kopyalayın ve ardından tooSQL sunucusu Azure VM'deki URL'den ekleyin
* Şirket içi fiziksel Dönüştür tooHyper-V VHD makine, tooAzure Blob Depolama karşıya yükleyin ve sonra yeni VM kullanarak VHD karşıya olarak dağıtma
* Sevk sabit sürücü Windows içeri/dışarı aktarma hizmeti kullanma
* Varsa bir AlwaysOn dağıtımını şirket içi, hello kullan [Azure çoğaltma Ekleme Sihirbazı'nı](../classic/sql-onprem-availability.md) toocreate Azure ve ardından kullanıcılar toohello Azure veritabanı örneğini işaret eden bir yük devretme, çoğaltma
* SQL Server kullanmak [işlemsel çoğaltma](https://msdn.microsoft.com/library/ms151176.aspx) tooconfigure hello Azure SQL Server örneği bir abone olarak ve kullanıcıların toohello Azure veritabanı örneğini işaret eden çoğaltma devre dışı bırak

> [!TIP]
> Bu aynı teknikleri toomove veritabanları arasında Azure SQL Server Vm'lerinin de kullanabilirsiniz. Örneğin, hiçbir desteklenen şekilde tooupgrade bir sürümü/yayını tooanother bir SQL Server galeri görüntüsü VM'den yoktur. Bu durumda, hello yeni sürümü/yayını ile yeni bir SQL Server VM oluşturun ve hello geçiş tekniklerden birini Bu makale toomove veritabanlarınızı kullanın gerekir. 

## <a name="choosing-your-migration-method"></a>Geçiş yöntemini seçme
Optimum veri aktarımı performansının için hello veritabanı dosyaları sıkıştırılmış bir yedekleme dosyası kullanarak bir Azure VM hello geçirin.

Merhaba veritabanı geçiş işlemi sırasında toominimize kesinti süresi hello AlwaysOn seçeneğini veya hello işlemsel çoğaltma seçeneğini kullanın.

El ile olası toouse hello yöntemleri yukarıda değilse, veritabanınızı geçirin. Bu yöntemi kullanarak, genellikle Azure'da hello Veritabanı yedeğinin bir kopyası tarafından izlenen bir veritabanı yedeği başlayın ve ardından bir veritabanını geri yükleme gerçekleştirin. Ayrıca Azure'da hello veritabanı dosyaları kendilerini kopyalayın ve ardından bunları ekleyin. Bir veritabanı bir Azure VM geçirme bu el ile işlem gerçekleştirmek çeşitli yöntemler vardır.

> [!NOTE]
> SQL Server'ın eski sürümlerini tooSQL Server 2014 veya SQL Server 2016 yükseltme yaptığınızda, değişiklikler gerekip gerekmediğini düşünmelisiniz. Geçiş projenizin bir parçası olarak hello yeni SQL Server sürümü tarafından desteklenmeyen özellikleri tüm bağımlılıkları adres öneririz. Senaryolar ve hello desteklenen sürümleri hakkında daha fazla bilgi için bkz: [tooSQL Server yükseltme](https://msdn.microsoft.com/library/bb677622.aspx).

Aşağıdaki tablonun hello hello birincil geçiş yöntemlerinin her birini listeler ve her yöntemin hello kullanımını en uygun olduğunda anlatır.

| Yöntem | Kaynak veritabanı sürümü | Hedef veritabanı sürümü | Kaynak veritabanı yedekleme boyutu kısıtlaması | Notlar |
| --- | --- | --- | --- | --- |
| [Azure sanal makinesi hello sıkıştırma ve el ile kopyalama hello yedekleme dosyası kullanarak şirket içi yedekleme gerçekleştirin](#backup-and-restore) |SQL Server 2005 veya üzeri |SQL Server 2005 veya üzeri |[Azure VM depolama sınırı](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) | Makine genelinde veritabanlarını taşıma çok basit ve iyi sınanmış bir yöntem budur. |
| [Yedekleme tooURL gerçekleştirmek ve hello Azure sanal makinesi hello URL'den içine geri yükleme](#backup-to-url-and-restore) |SQL Server 2012 SP1 CU2 veya daha büyük |SQL Server 2012 SP1 CU2 veya daha büyük |< 12,8 TB SQL Server 2016, aksi takdirde < 1 TB | Bu yöntem yalnızca başka bir şekilde toomove hello yedekleme dosyası toohello VM olduğu Azure storage kullanma. |
| [Detach ve hello veri ve günlük dosyaları tooAzure blob depolama kopyalayın ve ardından Azure sanal makinesinde tooSQL sunucu URL'SİNDEN ekleyin](#detach-and-attach-from-url) |SQL Server 2005 veya üzeri |SQL Server 2014 veya üzeri |[Azure VM depolama sınırı](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Çok planlarken bu yöntemi kullanın[hello Azure Blob Depolama hizmetini kullanarak bu dosyaları saklamak](https://msdn.microsoft.com/library/dn385720.aspx) ve tooSQL sunucu iliştirmek özellikle çok büyük veritabanları ile bir Azure VM çalışıyor |
| [Dönüştürme şirket içi tooHyper-V VHD makine tooAzure Blob Depolama yükleme ve karşıya yüklenen VHD kullanarak yeni bir sanal makine dağıtma](#convert-to-vm-and-upload-to-url-and-deploy-as-new-vm) |SQL Server 2005 veya üzeri |SQL Server 2005 veya üzeri |[Azure VM depolama sınırı](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Şu durumlarda kullanın [kendi SQL Server lisansınızı getiren](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md), SQL Server'ın eski bir sürümünde çalışacak bir veritabanını geçirme veya geçirme sistemi ve kullanıcı veritabanlarını birlikte bir parçası olarak veritabanı diğerine bağımlı geçişini hello kullanıcı veritabanlarını ve/veya sistem veritabanları. |
| [Sevk sabit sürücü Windows içeri/dışarı aktarma hizmeti kullanma](#ship-hard-drive) |SQL Server 2005 veya üzeri |SQL Server 2005 veya üzeri |[Azure VM depolama sınırı](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Kullanım hello [Windows içeri/dışarı aktarma hizmeti](../../../storage/common/storage-import-export-service.md) el ile kopyalama yöntemi olduğunda çok büyük veritabanları ile çok yavaşsa, gibi |
| [Kullanım hello Azure çoğaltma Ekleme Sihirbazı](../classic/sql-onprem-availability.md) |SQL Server 2012 veya daha büyük |SQL Server 2012 veya daha büyük |[Azure VM depolama sınırı](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |AlwaysOn şirket içi dağıtıma sahip olduğunuzda kullanın kapalı kalma süresi en aza indirir |
| [SQL Server işlem çoğaltma kullanın](https://msdn.microsoft.com/library/ms151176.aspx) |SQL Server 2005 veya üzeri |SQL Server 2005 veya üzeri |[Azure VM depolama sınırı](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Toominimize kapalı kalma süresi gerekir ve bir AlwaysOn şirket içi dağıtım olmayan olduğunda kullanın |

## <a name="backup-and-restore"></a>Yedekleme ve geri yükleme
Veritabanınızı sıkıştırmayla yedekleyin hello yedekleme toohello VM kopyalayın ve hello veritabanını geri yükleyin. Yedekleme dosyanızı 1 TB'den büyükse, bir VM disk hello en büyük boyutu 1 TB olduğundan bu şeritler gerekir. Bu el ile yükleme yöntemini kullanarak bir kullanıcı veritabanı genel adımlar toomigrate aşağıdaki hello kullan:

1. Tam veritabanı yedekleme tooan şirket içi konumu gerçekleştirin.
2. Oluşturun veya hello SQL Server sürümü, istenen ile bir sanal makineye yükleyin.
3. Bağlantı gereksinimlerinize göre ayarlayın. Bkz: [tooa Azure (Kaynak Yöneticisi) üzerinde SQL Server sanal makinesine bağlanmak](virtual-machines-windows-sql-connect.md).
4. Yedekleme dosyaları tooyour VM kopyalama kullanarak bir komut isteminden Uzak Masaüstü, Windows Gezgini veya hello kopyalama komutu.

## <a name="backup-toourl-and-restore"></a>Yedekleme tooURL ve geri yükleme
Tooa yerel dosyasını yedekleme yerine hello kullanabilirsiniz [yedekleme tooURL](https://msdn.microsoft.com/library/dn435916.aspx) ve URL toohello VM geri yükleyin. Şeritli yedekleme kümelerini desteklenen SQL Server 2016 ile performans için önerilen ve tooexceed hello boyutu sınırları blob başına gerekli. Çok büyük veritabanları için hello kullanımını hello [Windows içeri/dışarı aktarma hizmeti](../../../storage/common/storage-import-export-service.md) önerilir.

## <a name="detach-and-attach-from-url"></a>Ayırma ve URL'den ekleme
Veritabanı ve günlük dosyalarınızı detach ve çok aktarma[Azure Blob Depolama](https://msdn.microsoft.com/library/dn385720.aspx). Ardından, Azure VM'de hello URL'den hello veritabanı ekleyin. Merhaba fiziksel veritabanı dosyaları tooreside Blob depolamada isterseniz bunu kullanın. Bu, çok büyük veritabanları için yararlı olabilir. Bu el ile yükleme yöntemini kullanarak bir kullanıcı veritabanı genel adımlar toomigrate aşağıdaki hello kullan:

1. Merhaba şirket içi veritabanı örneği Hello veritabanı dosyalarından kullanımdan çıkarın.
2. Hello kullanarak Azure blob depolama alanına ayrılmış hello veritabanı dosyalarını kopyalamak [AZCopy komut satırı yardımcı programı](../../../storage/common/storage-use-azcopy.md).
3. Hello Azure URL toohello SQL Server örneğinde hello Azure VM gelen Hello veritabanı dosyalarını ekleyin.

## <a name="convert-toovm-and-upload-toourl-and-deploy-as-new-vm"></a>TooVM dönüştürmek ve tooURL karşıya yükleme ve yeni VM olarak dağıtma
Bu yöntem toomigrate tüm sistem ve kullanıcı veritabanlarını bir şirket içi SQL Server örneği tooAzure sanal makinede kullanın. Genel adımlar toomigrate el ile bu yöntemi kullanarak bir SQL Server örneğinin aşağıdaki hello kullan:

1. Dönüştürme fiziksel veya sanal makineleri tooHyper-V VHD kullanarak [Microsoft Virtual Machine Converter](https://technet.microsoft.com/library/dn874008(v=ws.11).aspx).
2. VHD dosyaları tooAzure depolama hello kullanarak karşıya [Ekle-AzureVHD cmdlet'i](https://msdn.microsoft.com/library/windowsazure/dn495173.aspx).
3. Yeni bir dağıtmak hello kullanarak sanal makine VHD karşıya yüklendi.

> [!NOTE]
> toomigrate tüm bir uygulamayı düşünün [Azure Site Recovery](../../../site-recovery/site-recovery-overview.md)].

## <a name="ship-hard-drive"></a>Sevk sabit sürücü
Kullanım hello [Windows içeri/dışarı aktarma hizmeti yöntemi](../../../storage/common/storage-import-export-service.md) dosya veri tooAzure Blob Depolama hello ağ üzerinden karşıya olduğu şekilde basımı karşılamayacak kadar pahalı veya değil uygun durumlarda büyük miktarlarda tootransfer. Bu hizmeti ile bir göndermek veya tooyour depolama hesabı verilerinizi burada olacaktır, veri tooan Azure veri merkezi içeren daha fazla sabit sürücüler karşıya.

## <a name="next-steps"></a>Sonraki Adımlar
SQL Server Azure sanal makinelerde çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makinelere genel bakış SQL Server'da](virtual-machines-windows-sql-server-iaas-overview.md).

Yakalanan görüntüden bir Azure SQL Server sanal makine oluşturma ile ilgili yönergeler için bkz: [ipuçları ve püf noktaları 'yakalanan görüntülerin Azure SQL sanal makineleri kopyalama'](https://blogs.msdn.microsoft.com/psssql/2016/07/06/tips-tricks-on-cloning-azure-sql-virtual-machines-from-captured-images/) hello CSS SQL Server mühendisleri blogunda.

