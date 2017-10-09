---
title: "aaaSQL veri ambarına kapasite limitlerini | Microsoft Docs"
description: "Bağlantılar, veritabanları, tablolar ve SQL Data Warehouse için sorguları için en yüksek değerleri."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: e1eac122-baee-4200-a2ed-f38bfa0f67ce
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 8619cb997f0955d649d447cb8ca15cd742cc70b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-capacity-limits"></a>SQL Data Warehouse kapasite sınırları
Merhaba aşağıdaki tablolarda Azure SQL Data Warehouse çeşitli bileşenler için izin verilen en yüksek değerleri hello içerir.

## <a name="workload-management"></a>İş yükü yönetimi
| Kategori | Açıklama | Maksimum |
|:--- |:--- |:--- |
| [Veri ambarı birimi (DWU)][Data Warehouse Units (DWU)] |Tek bir SQL Data Warehouse için en fazla DWU |6000 |
| [Veri ambarı birimi (DWU)][Data Warehouse Units (DWU)] |Tek bir SQL server için en fazla DWU |Varsayılan olarak 6000<br/><br/> Varsayılan olarak, her bir SQL server (örneğin myserver.database.windows.net) DTU too6000 DWU sağlayan kotası 45,000 sahiptir. Bu kota yalnızca bir güvenlik sınırıdır. Tarafından kotayı artırabilir [bir destek bileti oluşturma] [ creating a support ticket] ve seçerek *kota* hello istek türü.  DTU Çarp gereksinimlerini toocalculate DWU gerekli hello toplamda 7.5 hello. Geçerli bir DTU tüketimi hello SQL server dikey penceresinden hello Portalı'nda görüntüleyebilirsiniz. Duraklatıldı ve duraklatılmamış veritabanları hello DTU kota doğru sayısı. |
| Veritabanı bağlantısı |Eşzamanlı açık oturum |1024<br/><br/>En fazla 1024 etkin bağlantı, her biri istekleri tooa SQL veri ambarı veritabanını hello gönderebilir destekliyoruz aynı anda. Aslında aynı anda yürütebilir sorgu hello sayısı sınırları olduğunu unutmayın. Merhaba eşzamanlılık sınırı aşıldığında hello istek bir iç sıra burada işlenen toobe bekler gider. |
| Veritabanı bağlantısı |Hazırlanmış deyimleri için en fazla belleği |20 MB |
| [İş yükü yönetimi][Workload management] |En fazla eş zamanlı sorgular |32<br/><br/> Varsayılan olarak, SQL Data Warehouse en fazla 32 eş zamanlı sorgular ve sorguları kalan sıraları yürütebilir.<br/><br/>Merhaba eşzamanlılık düzeyi kullanıcılar tooa daha yüksek kaynak sınıfı atandığında veya SQL Data Warehouse ile düşük DWU yapılandırıldığında azaltabilir. DMV sorgu gibi bazı sorgular toorun her zaman izin verilir. |
| [Tempdb][Tempdb] |Tempdb en büyük boyutu |DW100 başına 399 GB. Bu nedenle DWU1000 Tempdb boyutlu too3.99 TB'dir |

## <a name="database-objects"></a>Veritabanı nesneleri
| Kategori | Açıklama | Maksimum |
|:--- |:--- |:--- |
| Database |En büyük boyutu |Disk üzerinde sıkıştırılmış 240 TB<br/><br/>Bu alanı tempdb ya da günlük alanının bağımsızdır ve bu nedenle bu ayrılmış toopermanent tabloları alanıdır.  Kümelenmiş columnstore sıkıştırma 5 X tahmin.  Tüm tabloları kümelenmiş columnstore (Merhaba varsayılan tablo türü) olduğunda bu sıkıştırma hello veritabanı toogrow tooapproximately 1 PB sağlar. |
| Tablo |En büyük boyutu |60 disk üzerinde sıkıştırılmış TB |
| Tablo |Her bir veritabanı tabloları |2 milyara |
| Tablo |Tablo başına sütun |1024 sütunları |
| Tablo |Sütun başına bayt sayısı |Sütun bağımlı [veri türü][data type].  Karakter veri türleri için 8000 nvarchar 4000 ya da en büyük veri türleri için 2 GB sınırıdır. |
| Tablo |Satır, tanımlanmış boyut başına bayt sayısı |Açıklama 8060 baytlık<br/><br/>Satır başına bayt sayısı Hello hello hesaplanan sayfa sıkıştırması ile aynı şekilde olan SQL Server için. SQL Server gibi SQL veri ambarı sağlayan satır taşma depolama destekleyen **değişken uzunluğu sütununa** toobe satır dışı gönderilir. Değişken uzunlukta satır satır dışı basıldığında yalnızca 24-bayt kök hello ana kayıtta depolanır. Daha fazla bilgi için bkz: Merhaba [satır taşma veri aşan 8 KB] [ Row-Overflow Data Exceeding 8 KB] MSDN makalesine. |
| Tablo |Tablo başına bölüm |15,000<br/><br/>Yüksek performans, hello sayısını en aza indirmenizi öneririz bölümlerini hala iş gereksinimlerinizi destekleyen while. Hello bölüm sayısı büyüdükçe, hello yükünü veri tanımlama dili (DDL) ve veri işleme dili (DML) işlemleri büyüdükçe ve performans neden olur. |
| Tablo |Karakter başına bölüm sınır değeri. |4000 |
| Dizin |Tablo başına olmayan Kümelenmiş dizinler. |999<br/><br/>Yalnızca toorowstore tablolar için geçerlidir. |
| Dizin |Tablo başına Kümelenmiş dizinler. |1<br><br/>Tooboth rowstore ve columnstore tabloları geçerlidir. |
| Dizin |Dizin anahtarı boyutu. |900 bayt sayısı.<br/><br/>Yalnızca toorowstore dizinler için geçerlidir.<br/><br/>Merhaba dizin oluşturulduğunda hello sütunlardaki var olan verileri hello 900 bayt aşmayan, dizinleri birden fazla 900 bayt maksimum boyuta sahip varchar sütunlarda oluşturulabilir. Ancak, daha sonra ekleme veya güncelleştirme eylemleri hello toplam boyutu tooexceed 900 bayt neden hello sütunlarda başarısız olur. |
| Dizin |Dizin başına anahtar sütun. |16<br/><br/>Yalnızca toorowstore dizinler için geçerlidir. Kümelenmiş columnstore dizinleri tüm sütunları içerir. |
| İstatistikler |Merhaba boyutunu sütun değerlerini birleştirilmiş. |900 bayt sayısı. |
| İstatistikler |Sütun istatistikleri nesne başına. |32 |
| İstatistikler |Tablo başına sütunlar üzerinde oluşturulan istatistikleri. |30,000 |
| Saklı Yordamlar |İç içe geçme en yüksek düzeyde. |8 |
| Görünüm |Görünüm başına sütun |1,024 |

## <a name="loads"></a>Yükler
| Kategori | Açıklama | Maksimum |
|:--- |:--- |:--- |
| Polybase yükler |Satır başına MB |1<br/><br/>Polybase yükleri sınırlı tooloading satırlarının hem 1 MB'tan küçük ve tooVARCHR(MAX), yüklenemiyor NVARCHAR(MAX) veya VARBINARY(MAX).<br/><br/> |

## <a name="queries"></a>Sorgular
| Kategori | Açıklama | Maksimum |
|:--- |:--- |:--- |
| Sorgu |Kullanıcı tablolar üzerinde sıraya alınan sorgular. |1000 |
| Sorgu |Sistem görünümleri eş zamanlı sorguları. |100 |
| Sorgu |Sıraya alınan sorgularına ilişkin sistem görünümleri |1000 |
| Sorgu |En fazla parametreleri |2098 |
| Batch |En büyük boyutu |65,536*4096 |
| SELECT sonuçları |Satır başına sütun |4096<br/><br/>Hiçbir zaman sonuç seçin hello satır başına birden fazla 4096 sütun olabilir. 4096 her zaman olabilir garantisi yoktur. Merhaba sorgu planı geçici bir tablo gerektiriyorsa, en fazla tablo başına hello 1024 sütun uygulanabilir. |
| SEÇİN |İç içe alt sorgular |32<br/><br/>Bu gibi durumlarda, 32'den fazla iç içe alt sorgulara hiçbir zaman bir SELECT deyimi içinde olabilir. 32 her zaman olabilir garantisi yoktur. Örneğin, bir birleştirme alt sorgu hello sorgu planı tanıtabilirsiniz. alt sorgular Hello sayısı tarafından kullanılabilir bellek sınırlı olabilir. |
| SEÇİN |BİRLEŞİM başına sütun |1024 sütunları<br/><br/>Bu gibi durumlarda, 1024'ten fazla sütun hiçbir zaman hello birleşim olabilir. 1024 her zaman olabilir garantisi yoktur. Merhaba birleşim planı hello birleştirme sonucu çok sütun içeren geçici bir tablo gerektiriyorsa, hello 1024 sınırı toohello geçici tablo uygulanır. |
| SEÇİN |GROUP BY sütun başına bayt sayısı. |8060<br/><br/>Merhaba sütun hello GROUP BY yan tümcesinde en fazla Açıklama 8060 baytlık olabilir. |
| SEÇİN |ORDER BY sütun başına bayt sayısı |Açıklama 8060 baytlık.<br/><br/>Merhaba sütun hello ORDER BY yan tümcesinde en fazla Açıklama 8060 baytlık olabilir. |
| Tanımlayıcıları ve deyimi başına sabitleri |Başvurulan tanımlayıcıları ve sabitleri sayısı. |65,535<br/><br/>SQL veri ambarı tanımlayıcıları ve tek bir sorgu ifadesinde bulunan sabitler hello sayısını sınırlar. Bu sınırı 65. 535'dir. SQL Server hatası 8632 numara bu sonuçlarında aşıyor. Daha fazla bilgi için bkz: [iç hata: deyim Hizmetleri sınırına ulaşıldı][Internal error: An expression services limit has been reached]. |

## <a name="metadata"></a>Meta Veriler
| Sistem Görünümü | En fazla satır |
|:--- |:--- |
| sys.dm_pdw_component_health_alerts |10,000 |
| sys.dm_pdw_dms_cores |100 |
| sys.dm_pdw_dms_workers |SQL istekleri DMS çalışanları hello en son 1000 için toplam sayısı. |
| sys.dm_pdw_errors |10,000 |
| sys.dm_pdw_exec_requests |10,000 |
| sys.dm_pdw_exec_sessions |10,000 |
| sys.dm_pdw_request_steps |Adımları sys.dm_pdw_exec_requests içinde depolanan hello en son 1000 SQL istekleri için toplam sayısı. |
| sys.dm_pdw_os_event_logs |10,000 |
| sys.dm_pdw_sql_requests |sys.dm_pdw_exec_requests içinde depolanan hello en son 1000 SQL istek sayısı. |

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla başvuru bilgileri için bkz: [SQL Data Warehouse başvuru genel bakış][SQL Data Warehouse reference overview].

<!--Image references-->

<!--Article references-->
[Data Warehouse Units (DWU)]: ./sql-data-warehouse-overview-what-is.md
[SQL Data Warehouse reference overview]: ./sql-data-warehouse-overview-reference.md
[Workload management]: ./sql-data-warehouse-develop-concurrency.md
[Tempdb]: ./sql-data-warehouse-tables-temporary.md
[data type]: ./sql-data-warehouse-tables-data-types.md
[creating a support ticket]: /sql-data-warehouse-get-started-create-support-ticket.md

<!--MSDN references-->
[Row-Overflow Data Exceeding 8 KB]: https://msdn.microsoft.com/library/ms186981.aspx
[Internal error: An expression services limit has been reached]: https://support.microsoft.com/kb/913050
