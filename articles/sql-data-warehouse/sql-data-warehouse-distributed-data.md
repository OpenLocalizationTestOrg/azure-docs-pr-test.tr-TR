---
title: "aaaHow dağıtılmış Azure SQL Data Warehouse veri çalışır | Microsoft Docs"
description: "Veri tabloları Azure SQL veri ambarı ve paralel veri ambarı dağıtmak için yüksek düzeyde paralel işleme (MPP) ve hello seçenekleri için nasıl dağıtıldığını öğrenin."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: bae494a6-7ac5-4c38-8ca3-ab2696c63a9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/12/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 9a712d8d5251e4391ede245105918283aaa4b193
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="distributed-data-and-distributed-tables-for-massively-parallel-processing-mpp"></a>Dağıtılmış veri ve dağıtılmış tablolar için yüksek düzeyde paralel işleme (MPP)
Azure SQL veri ambarı ve paralel veri ambarı, Microsoft'un yüksek düzeyde paralel işleme (MPP) sistemleri olan kullanıcı verilerini nasıl dağıtıldığını öğrenin. Veri ambarı toouse tasarlama Dağıtılmış veri etkili bir şekilde hello MPP mimarisi avantajları, tooachieve hello sorgu işleme yardımcı olur. Birkaç veritabanı tasarım seçenekleri sorgu performansını iyileştirme üzerinde önemli bir etkisi olabilir.  

> [!NOTE]
> Azure SQL veri ambarı ve paralel veri ambarı kullanım hello aynı yüksek düzeyde paralel işleme (MPP) tasarımı, ancak platform temel hello nedeniyle bazı farklar sahiptirler. SQL Data Warehouse Azure üzerinde çalışan hizmet (PaaS) olarak platformudur. Paralel veri ambarı üzerinde Analytics Platform System (Windows Server çalıştıran bir şirket içi gereç olan AP'ler) çalışır.
> 
> 

## <a name="what-is-distributed-data"></a>Dağıtılmış veri nedir?
SQL veri ambarı ve paralel veri ambarı, Dağıtılmış veri hello MPP sistem birden fazla konumda depolanan toouser verileri ifade eder. Konumların her birini bağımsız depolama ve hello veri kendi kısmı sorguları çalıştırır işleme birimi olarak çalışır. Paralel tooachieve yüksek sorgu performansı temel toorunning sorgularda dağıtılmış verilerdir.

toodistribute verileri, her satır bir kullanıcı tablosu dağıtılmış tooone konumunun hello veri ambarı atar.  Bir karma dağıtım veya hepsini yöntemini tablolarla dağıtabilirsiniz. Merhaba dağıtım yöntemini hello CREATE TABLE deyimi belirtildi. 

## <a name="hash-distributed-tables"></a>Karma dağıtılmış tabloları
Aşağıdaki diyagramda hello (dağıtılmış olmayan tablo) tam karma dağıtılmış bir tablo olarak nasıl depolanır gösterilmektedir. Belirleyici işlevi her satır toobelong tooone dağıtım atar. Hello tablo tanımı hello sütunlardan biri hello dağıtım sütunu olarak atanmış. Merhaba karma işlevi her satır tooa dağıtım hello dağıtım sütun tooassign hello değeri kullanır.

Distinctness, veri eğme ve hello sistemde sorgu türleri hello gibi bir dağıtım sütunun hello seçimi için başarım düşünceleri vardır.

![Dağıtılmış tablo](media/sql-data-warehouse-distributed-data/hash-distributed-table.png "dağıtılmış tablo")  

* Her satır tooone dağıtım aittir.  
* Belirleyici karma algoritma her satır tooone dağıtım atar.  
* Merhaba dağıtım başına tablo satır sayısı tarafından hello farklı boyutlarda tabloların gösterildiği gibi değişir.

## <a name="round-robin-distributed-tables"></a>Hepsini dağıtılmış tabloları
Hepsini dağıtılmış tablo sıralı bir şekilde her satır tooa dağıtım atayarak hello satırları dağıtır. Hızlı tooload veri hepsini tabloya değil, ancak sorgu performansı daha yavaş olabilir.  Genellikle bir hepsini tablo birleştirme hello satırları tooenable hello sorgu tooproduce Süren doğru bir sonuç reshuffling gerektirir.

## <a name="distributed-storage-locations-are-called-distributions"></a>Dağıtılmış depolama konumları dağıtımları adlandırılır
Dağıtılmış her konum bir dağıtım adı verilir. Bir sorgu paralel olarak çalıştırıldığında, her dağıtım hello veri kendi kısmı üzerinde bir SQL sorgusu gerçekleştirir. SQL veri ambarı SQL veritabanı toorun hello sorgusu kullanır. Paralel veri ambarı SQL Server toorun hello sorgusu kullanır. Temel tooachieving genişleme bu hiçbir şey paylaşılmayan mimarisi tasarımdır paralel bilgi işlem.

### <a name="can-i-view-hello-distributions"></a>Merhaba dağıtımları görüntüleyebilir miyim?
Her dağıtım bir dağıtım Kimliğine sahip ve tooSQL veri ambarı ve paralel veri ambarı ilgilidir sistem görünümlerde görülebilir. Merhaba dağıtım kimliği tootroubleshoot sorgu performansını ve başka sorunlara kullanabilirsiniz. Merhaba hello sistem görünümleri listesi için bkz: [MPP sistem görünümü](sql-data-warehouse-reference-tsql-statements.md).

## <a name="difference-between-a-distribution-and-a-compute-node"></a>Bir dağıtım ve işlem düğümü arasındaki fark
Bir dağıtım hello temel Dağıtılmış veri depolamak ve paralel sorgular için birimidir. Dağıtımları işlem düğümlerinde gruplandırılır. Her işlem düğümünde bir veya daha fazla dağıtımları izler.  

* Analiz platformu sistemi işlem düğümleri hello donanım mimarisi ve genişleme özellikleri merkezi bir bileşeni olarak kullanır. Her zaman işlem düğümü başına sekiz dağıtımları karma dağıtılmış tablolar için hello diyagramda gösterildiği gibi kullanır. İşlem düğümü sayısını hello ve bu nedenle dağıtımları sayısı Merhaba, işlem düğümleri hello Gereci için satın aldığınız hello sayısı tarafından belirlenir. Örneğin, sekiz işlem düğümleri satın aldığınız durumlarda 64 dağıtımları (8 işlem düğümleri x 8 dağıtımları/düğümü) alın. 
* SQL veri ambarı sabit sayıda 60 dağıtımları ve esnek bir işlem düğümü sayısını vardır. Merhaba işlem düğümlerini Azure bilgi işlem ve depolama kaynakları ile uygulanır. İşlem düğümü sayısını Hello according toohello arka uç hizmeti iş yükü ve hello veri ambarı için belirttiğiniz hello bilgi işlem kapasitesi (Dwu) değiştirebilirsiniz. İşlem düğümü sayısını Hello değiştiğinde işlem düğümü başına dağıtımları hello sayısı da değişir. 

### <a name="can-i-view-hello-compute-nodes"></a>Merhaba işlem düğümleri görüntüleyebilir miyim?
Her işlem düğümü, bir düğüm kimliği var ve tooSQL veri ambarı ve paralel veri ambarı ilgilidir sistem görünümlerde görülebilir.  Merhaba node_id sütun adları sys.pdw_nodes ile başlayan sistem görünümleri için bakarak hello işlem düğümünde görebilirsiniz. Merhaba hello sistem görünümleri listesi için bkz: [MPP sistem görünümü](sql-data-warehouse-reference-tsql-statements.md).

## <a name="Replicated"></a>Çoğaltılmış tablolar
Çoğaltılan bir tablo içeren bir Merhaba tablonun kopyasını her işlem düğümü üzerinde tam olarak depolanır. Tablo çoğaltma JOIN veya toplama önce işlem düğümleri arasında hello gerek tootransfer verileri kaldırır. Çoğaltılmış tablolar yalnızca küçük tablolarla uygun hello nedeniyle ek depolama alanı gerekli toostore hello tam tablosunda her işlem düğümü.  

Merhaba Aşağıdaki diyagramda her işlem düğümü üzerinde depolanan çoğaltılmış bir tablo gösterir. SQL Data Warehouse için hello çoğaltılmış tablo tam kopyalanan tooa dağıtım her işlem düğümünde veritabanıdır. Paralel veri ambarı için hello çoğaltılmış tablo toohello işlem düğümü atanan tüm disklerde depolanır.  Bu disk strateji, SQL Server dosya grupları kullanılarak uygulanır.  

![Yinelenmiş tablo](media/sql-data-warehouse-distributed-data/replicated-table.png "yinelenmiş tablosu") 

## <a name="next-steps"></a>Sonraki adımlar
bkz: Dağıtılmış toouse tabloları etkili bir şekilde [SQL Data Warehouse tablolarda dağıtma](sql-data-warehouse-tables-distribute.md)  

