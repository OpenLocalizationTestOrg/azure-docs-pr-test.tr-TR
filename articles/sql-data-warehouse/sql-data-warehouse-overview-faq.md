---
title: "aaaAzure SQL veri ambarı ile ilgili sık sorulan sorular | Microsoft Docs"
description: "Bu makalede Azure SQL veri ambarı hakkında sık sorulan sorular müşteriler ve geliştiricilerin çıkışı listeler"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 812CA525-3BF3-49DF-8DF3-FB4342464F4F
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 3/1/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 09fd3f65d9507b09fcb8f477742c7d020add2755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a>SQL veri ambarı sık sorulan sorular

## <a name="general"></a>Genel

Q. Ne SQL DW veri güvenliği için sunar?

A. SQL DW TDE gibi verileri korumak ve denetlemek için çeşitli çözümler sunar. Daha fazla bilgi için bkz: [güvenlik].

Q. Hangi yasal veya iş standartları SQL DW olduğunu uyumlu nereden bulabilirim?

A. Merhaba ziyaret [Microsoft Compliance] ürün SOC ve ISO gibi çeşitli uyumluluk sunumları için sayfa. İlk uyumluluk başlığı seçin, ardından Azure genişletin hangi hizmetler Azure hizmetlerdir hello içinde kapsam için Microsoft bulut Hizmetleri bölümünde hello sayfa toosee hello sağ tarafında uyumlu.

Q. Powerbı bağlayabilir miyim?

A. Evet! SQL DW ile doğrudan sorgu Powerbı destekler ancak çok sayıda kullanıcı veya gerçek zamanlı verileri için tasarlanmamıştır. Powerbı üretim kullanımı için Azure Analysis Services ya da analiz hizmeti Iaas üstünde Powerbı kullanmanızı öneririz. 

Q. SQL veri ambarı kapasite sınırları nelerdir?

A. Bizim geçerli bkz [kapasite limitlerini] sayfası. 

Q. Neden my ölçek/Duraklat/Sürdür çok uzun sürüyor?

A. Çeşitli etkenlere işlem yönetimi işlemleri için başlangıç saati etkileyebilir. Bir ortak işlemleri uzun süre çalışan işlem geri alma için durumda. Bir ölçek veya duraklatma işlemi başlatıldığında, tüm gelen oturumları engellenir ve sorguları boşaltmış. Bir işlem yeniden başlatılmadan önce sipariş tooleave hello sisteminde tutarlı bir durumda, işlemleri geri alınması gerekir. büyük hello sayısını ve işlemleri büyük hello günlük boyutunu Merhaba, hello sistem tooa kararlı durum geri hello uzun hello işlemi durduruldu.

## <a name="user-support"></a>Kullanıcı desteği

Q. Özellik isteği burada gönderme sahip miyim?

A. Özellik isteği varsa, üzerinde gönderme bizim [UserVoice] sayfası

Q. Nasıl yapabilirim x?

A. SQL veri ambarı ile geliştirilmesi konusunda daha fazla yardım için üzerinde sorular sorabilirsiniz bizim [yığın taşması] sayfası. 

Q. Bir destek bileti nasıl gönderilsin mi?

A. [Destek biletlerini Göster] Azure portalı üzerinden kaydedildi.

## <a name="sql-languagefeature-support"></a>SQL dil/özellik desteği 

Q. Hangi veri türleri SQL Data Warehouse destekliyor mu?

A. SQL veri ambarı bkz [veri türleri].

Q. Tablo özellikleri destekliyor?

A. SQL veri ambarı birçok özellik desteklerken, bazı desteklenmez ve belgelenmiştir [desteklenmeyen Tablo Özellikler].

## <a name="tooling-and-administration"></a>Araçları ve yönetim

Q. Visual Studio veritabanı projelerini desteklemez.

A. Şu anda veritabanı projeleri Visual Studio ile SQL Data Warehouse için desteklemiyoruz. Oy tooget toocast isterseniz bu özelliği, bizim kullanıcı sesi ziyaret [veritabanı projeleri özellik isteği].

Q. SQL Data Warehouse, REST API'leri destekliyor mu?

A. Evet. SQL veritabanı ile kullanılan çoğu REST işlevselliği de SQL Data Warehouse ile kullanılabilir. REST belge sayfalarının içinde API bilgi bulabilirsiniz veya [MSDN].


## <a name="loading"></a>Yükleniyor

Q. Hangi istemci sürücüleri destekliyor?

A. DW sürücü desteği hello üzerinde bulunabilir [bağlantı dizeleri] sayfası

S: hangi dosya biçimleri, SQL veri ambarı ile PolyBase tarafından desteklenir?

Y: Orc, RC, Parquet ve düz sınırlandırılmış metin

S: ne toofrom SQL DW Polybase'i kullanarak bağlanmak? 

Y: [Azure Data Lake Store] ve [Azure depolama BLOB'ları]

S: hesaplama aşağı itme olası tooAzure depolama BLOB veya ADLS bağlanırken mi? 

A: Hayır SQL DW PolyBase yalnızca hello depolama bileşenleri etkileşim kurar. 

S: tooHDI bağlanmak?

Y: HDI ADLS veya WASB hello HDFS katmanı olarak kullanabilirsiniz. HDFS katmanı olarak ya da varsa, bu verileri SQL DW yükleyebilirsiniz. Ancak, aşağı itme hesaplama toohello HDI örneği oluşturulamıyor. 

## <a name="next-steps"></a>Sonraki adımlar
Bir bütün olarak SQL Data Warehouse hakkında daha fazla bilgi için bkz: bizim [genel bakış] sayfası.


<!-- Article references -->
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[bağlantı dizeleri]: ./sql-data-warehouse-connection-strings.md
[yığın taşması]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Destek biletlerini Göster]: ./sql-data-warehouse-get-started-create-support-ticket.md
[güvenlik]: ./sql-data-warehouse-overview-manage-security.md
[Microsoft Compliance]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings
[kapasite limitlerini]: ./sql-data-warehouse-service-capacity-limits.md
[veri türleri]: ./sql-data-warehouse-tables-data-types.md
[desteklenmeyen Tablo Özellikler]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md
[Azure depolama BLOB'ları]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[veritabanı projeleri özellik isteği]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx
[genel bakış]: ./sql-data-warehouse-overview-faq.md