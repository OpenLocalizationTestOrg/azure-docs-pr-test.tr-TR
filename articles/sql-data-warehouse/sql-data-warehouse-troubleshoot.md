---
title: Azure SQL Data Warehouse aaaTroubleshooting | Microsoft Docs
description: "Azure SQL veri ambarı sorunlarını giderme."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 51f1e444-9ef7-4e30-9a88-598946c45196
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/30/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 3c53a39f77057fe0bcc053a0b896555abf397515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-sql-data-warehouse"></a>Azure SQL veri ambarı sorunlarını giderme
Bu konu, bazı bizim Müşterilerden aldığımız daha yaygın sorun giderme soruları hello listeler.

## <a name="connecting"></a>Bağlanma
| Sorun | Çözüm |
|:--- |:--- |
| Oturum açma 'NT Yetkili\Anonim Oturum açma' kullanıcısı için başarısız oldu. (Microsoft SQL Server, hata: 18456) |Bu hata bir AAD kullanıcı tooconnect toohello ana veritabanı çalışır, ancak bir kullanıcının yöneticisinde yok oluşur.  Bu sorunu ya da belirtin toocorrect tooconnect tooat bağlantı süresi istiyor veya hello kullanıcı toohello ana veritabanı Ekle SQL Data Warehouse hello.  Bkz: [güvenliğine genel bakış] [ Security overview] daha fazla ayrıntı için makale. |
| Merhaba sunucusu asıl "KullanıcıAdım" değil mümkün tooaccess hello veritabanı "ana" Merhaba geçerli güvenlik bağlamı altında. Kullanıcının varsayılan veritabanı açılamıyor. Oturum açma başarısız oldu. Oturum açma 'KullanıcıAdım' kullanıcısı için başarısız oldu. (Microsoft SQL Server, hata: 916) |Bu hata bir AAD kullanıcı tooconnect toohello ana veritabanı çalışır, ancak bir kullanıcının yöneticisinde yok oluşur.  Bu sorunu ya da belirtin toocorrect tooconnect tooat bağlantı süresi istiyor veya hello kullanıcı toohello ana veritabanı Ekle SQL Data Warehouse hello.  Bkz: [güvenliğine genel bakış] [ Security overview] daha fazla ayrıntı için makale. |
| CTAIP hata |Bir oturum açma hello SQL server ana veritabanı üzerinde ancak hello SQL Data Warehouse veritabanı oluşturulduğunda bu hata oluşabilir.  Bu hatayla karşılaşırsanız, hello bakalım [güvenliğine genel bakış] [ Security overview] makalesi.  Bu makalede toocreate oluşturma nasıl oturum açma ve kullanıcı asıl ve ardından nasıl toocreate kullanıcı bir SQL Data Warehouse veritabanı hello açıklanmaktadır. |
| Güvenlik Duvarı tarafından engellendi |Azure SQL veritabanları yalnızca bilinen IP adresleri erişim tooa veritabanı sunucusu ve veritabanı düzeyi güvenlik duvarları tooensure tarafından korunur. bağlanmadan önce hello güvenlik duvarları, açıkça etkinleştirmelisiniz anlamına gelir varsayılan ve IP adresi veya adres aralığı ile güvenlidir.  tooconfigure erişimi, güvenlik duvarınızın izleyin hello adımlarda [sunucusu güvenlik duvarı erişimi için istemci IP yapılandırma] [ Configure server firewall access for your client IP] hello içinde [yönergeleri sağlama] [Provisioning instructions]. |
| Aracı veya sürücüsü ile bağlantı kurulamıyor |SQL veri ambarı önerir kullanarak [SSMS][SSMS], [Visual Studio için SSDT][SSDT for Visual Studio], veya [sqlcmd] [ sqlcmd] tooquery verilerinizi. Sürücüleri ve bağlantı tooSQL veri ambarı hakkında daha fazla bilgi için bkz: [Azure SQL Data Warehouse için sürücüleri] [ Drivers for Azure SQL Data Warehouse] ve [tooAzure SQL Data Warehouse bağlanmak] [ Connect tooAzure SQL Data Warehouse] makaleleri. |

## <a name="tools"></a>Araçlar
| Sorun | Çözüm |
|:--- |:--- |
| Visual Studio Nesne Gezgini AAD kullanıcılarını eksik |Bu bilinen bir sorundur.  Geçici bir çözüm olarak hello kullanıcılar görüntülemek [sys.database_principals][sys.database_principals].  Bkz: [kimlik doğrulaması tooAzure SQL Data Warehouse] [ Authentication tooAzure SQL Data Warehouse] toolearn SQL Data Warehouse ile Azure Active Directory kullanma hakkında daha fazla. |
|Komut dosyası, hello komut dosyası oluşturma Sihirbazı'nı kullanarak veya SSMS ile bağlanma kılavuzdur, yavaş, askıdaki veya üretmeye hataları| Lütfen kullanıcıların hello ana veritabanında oluşturduğunuz emin olun. Komut dosyası seçenekleri, ayrıca hello altyapı sürümü "Microsoft Azure SQL veri ambarı Edition" olarak ayarlanır ve "Microsoft Azure SQL veritabanı" altyapısı türü olduğundan emin olun.|

## <a name="performance"></a>Performans
| Sorun | Çözüm |
|:--- |:--- |
| Sorgu performans sorunlarını giderme |Belirli bir sorgu tootroubleshoot çalışıyorsanız başlayın [öğrenme nasıl toomonitor sorgularınızı][Learning how toomonitor your queries]. |
| Zayıf sorgu performansı ve planları eksik istatistikleri sonucunu görülür |Merhaba en yaygın performansın tablolarınızı istatistiklerle eksikliği nedenidir.  Bkz: [tablo istatistikleri koruma] [ Statistics] hakkında ayrıntılar için toocreate istatistikleri ve kritik tooyour performans oldukları neden. |
| Düşük eşzamanlılık / sorguları sıraya alındı |Anlama [iş yükü Yönetim] [ Workload management] nasıl sipariş toounderstand önemlidir eşzamanlılık ile toobalance bellek ayırma. |
| Nasıl tooimplement en iyi uygulamalar |Merhaba en iyi yeri toostart toolearn yolları tooimprove sorgu performansı olan [SQL veri ambarı en iyi yöntemler] [ SQL Data Warehouse best practices] makalesi. |
| Nasıl ölçeklendirme tooimprove performans |Bazen hello çözüm tooimproving performans toosimply olduğundan daha fazla işlem gücü tooyour sorgular tarafından eklemek [SQL veri ambarı ölçeklendirme][Scaling your SQL Data Warehouse]. |
| Zayıf dizin kalitesi zayıf sorgu performansı |Bazı kez sorgular için yavaşlama nedeniyle [zayıf columnstore dizini kalite][Poor columnstore index quality].  Bu makalede daha fazla bilgi için bkz: ve nasıl çok[yeniden dizinler tooimprove segment kalite][Rebuild indexes tooimprove segment quality]. |

## <a name="system-management"></a>Sistem Yönetimi
| Sorun | Çözüm |
|:--- |:--- |
| Msg 40847: sunucu 45000 veritabanı işlem birimi kotası izin hello aşacağından hello işlem gerçekleştirilemedi. |Ya da hello azaltmak [DWU] [ DWU] hello veritabanı toocreate çalıştığınız veya [kota artışı isteği][request a quota increase]. |
| Alan kullanımı araştırma |Bkz: [tablo boyutları] [ Table sizes] toounderstand hello alan kullanımının sisteminizin. |
| Yönetme konusunda Yardım tabloları |Merhaba bkz [tablo genel bakışı] [ Overview] tablolarınızı yönetme konusunda yardım için makale.  Bu makalede içine gibi daha ayrıntılı konulara bağlantılar da içerir. [tablo veri türleri][Data types], [tablo dağıtma][Distribute], [tablo dizin][Index], [bir tablo bölümleme][Partition], [tablo istatistikleri koruma] [ Statistics] ve [geçici tablolar][Temporary]. |
|Saydam veri şifreleme (TDE) ilerleme çubuğu hello Azure Portal güncelleştirilmiyor|TDE hello durumunu görüntüleyebilirsiniz [powershell](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption).|

## <a name="polybase"></a>Polybase
| Sorun | Çözüm |
|:--- |:--- |
| Büyük satırları nedeniyle yükleme başarısız |Şu anda büyük satır desteği için Polybase kullanılabilir değil.  Tablonuz, VARCHAR(MAX), NVARCHAR(MAX) veya VARBINARY(MAX) içeriyorsa, dış tablolara olamaz yani verilerinizi kullanılan tooload olabilir.  Büyük satırları yükleri şu anda yalnızca Azure Data Factory (BCP), Azure akış analizi, SSIS, BCP veya hello .NET SQLBulkCopy sınıfı desteklenir. PolyBase destek büyük satırlar için gelecekteki bir sürümde eklenecek. |
| en büyük veri türüne sahip tablosunun BCP yükleme başarısız oluyor |VARCHAR(MAX), NVARCHAR(MAX) veya VARBINARY(MAX) Bazı senaryolarda Merhaba tablonun hello sonunda yerleştirilmesi gerektiren bilinen bir sorun yoktur.  Merhaba tablo, maksimum sütun toohello sonuna taşımayı deneyin. |

## <a name="differences-from-sql-database"></a>SQL veritabanı arasındaki farklar
| Sorun | Çözüm |
|:--- |:--- |
| Desteklenmeyen SQL veritabanı özellikleri |Bkz: [desteklenmeyen tablo özellikleri][Unsupported table features]. |
| Desteklenmeyen SQL veritabanı veri türleri |Bkz: [desteklenmeyen veri türleri][Unsupported data types]. |
| SİLME ve güncelleştirme sınırlamaları |Bkz: [güncelleştirme geçici çözümler][UPDATE workarounds], [DELETE geçici çözümler] [ DELETE workarounds] ve [kullanarak CTAS toowork desteklenmeyen güncelleştirme geçici ve DELETE sözdizimi][Using CTAS toowork around unsupported UPDATE and DELETE syntax]. |
| MERGE deyimi desteklenmiyor |Bkz: [birleştirme geçici çözümler][MERGE workarounds]. |
| Saklı yordam sınırlamaları |Bkz: [depolanan yordamı sınırlamaları] [ Stored procedure limitations] toounderstand bazı saklı yordamlar hello sınırlamaları. |
| UDF'ler SELECT deyimleri desteklemiyor |Bu bizim UDF'ler geçerli bir kısıtlamasıdır.  Bkz: [CREATE FUNCTION] [ CREATE FUNCTION] hello sözdizimi destekliyoruz. |

## <a name="next-steps"></a>Sonraki adımlar
Kullanıyorsanız oluşturulamıyor toofind bir çözüm tooyour sorunu olan yukarıdaki deneyebilirsiniz bazı kaynaklar şunlardır.

* [Bloglar]
* [Özellik istekleri]
* [Videolar]
* [CAT ekibi blogları]
* [Destek bileti oluşturma]
* [MSDN forumu]
* [Stack Overflow forumu]
* [Twitter]

<!--Image references-->

<!--Article references-->
[Security overview]: ./sql-data-warehouse-overview-manage-security.md
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx
[SSDT for Visual Studio]: ./sql-data-warehouse-install-visual-studio.md
[Drivers for Azure SQL Data Warehouse]: ./sql-data-warehouse-connection-strings.md
[Connect tooAzure SQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Destek bileti oluşturma]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Scaling your SQL Data Warehouse]: ./sql-data-warehouse-manage-compute-overview.md
[DWU]: ./sql-data-warehouse-overview-what-is.md
[request a quota increase]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Learning how toomonitor your queries]: ./sql-data-warehouse-manage-monitor.md
[Provisioning instructions]: ./sql-data-warehouse-get-started-provision.md
[Configure server firewall access for your client IP]: ./sql-data-warehouse-get-started-provision.md#create-a-server-level-firewall-rule-in-the-azure-portal
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[Table sizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries
[Unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuild indexes tooimprove segment quality]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Workload management]: ./sql-data-warehouse-develop-concurrency.md
[Using CTAS toowork around unsupported UPDATE and DELETE syntax]: ./sql-data-warehouse-develop-ctas.md#using-ctas-to-work-around-unsupported-features
[UPDATE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[DELETE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[MERGE workarounds]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[Stored procedure limitations]: ./sql-data-warehouse-develop-stored-procedures.md#limitations
[Authentication tooAzure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md
[Working around hello PolyBase UTF-8 requirement]: ./sql-data-warehouse-load-polybase-guide.md#working-around-the-polybase-utf-8-requirement

<!--MSDN references-->
[sys.database_principals]: https://msdn.microsoft.com/library/ms187328.aspx
[CREATE FUNCTION]: https://msdn.microsoft.com/library/mt203952.aspx
[sqlcmd]: https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-get-started-connect-sqlcmd/

<!--Other Web references-->
[Bloglar]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[CAT ekibi blogları]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[Özellik istekleri]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[MSDN forumu]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse
[Stack Overflow forumu]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[Videolar]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
