---
title: "Geçir: Veri ambarı geçiş yardımcı programı | Microsoft Docs"
description: "Veri ambarı tooSQL geçirin."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 4d7ad981-ef31-4513-b337-50bdc4709c09
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: c89909883fb42b0b04dd87a9973e5ee3e30d8f0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-warehouse-migration-utility-preview"></a>Veri ambarı geçiş yardımcı programı (Önizleme)
> [!div class="op_single_selector"]
> * [Geçiş yardımcı programı indir][Download Migration Utility]
> 
> 

Veri ambarı geçiş yardımcı programı Hello toomigrate şema ve SQL Server ve Azure SQL veritabanı tooAzure SQL Data Warehouse verilerini bir aracı tasarlanmış ' dir. Şema geçiş sırasında hello aracı hello karşılık gelen kaynak toodestination şemadan otomatik olarak eşlenir. Merhaba şema geçirildikten sonra hello Araçlar otomatik olarak oluşturulan komut ile Merhaba seçeneği toomove verileri sağlar.

Ayrıca tooschema ve veri geçişi, önleyen hello hedef ve kaynak örnekleri arasında uyumsuzluk özetleme seçeneği toogenerate Uyumluluk raporlarını hello aracı kazandırır geçiş hızlandırıldı.

## <a name="get-started"></a>başlarken
Yükleme için bir önkoşul olarak hello BCP komut satırı yardımcı programını toorun geçiş betikleri ve Office tooview hello uyumluluk raporu gerekir. Merhaba aracı yüklenmeden önce hello başlattıktan sonra istendiğinde tooaccept standart EULA karşıdan yüklediğiniz yürütülebilir olacaktır.

Ayrıca, toorun hello geçiş Utiliy, bir hello toomigrate aradığınız hello veritabanında aşağıdaki izinleri: veritabanı oluşturma, ALTER ANY DATABASE veya Görünüm herhangi TANIMI.

### <a name="launching-hello-tool-and-connecting"></a>Merhaba aracı başlatarak ve bağlanma
Post görünen hello Masaüstü simgesine tıklayarak başlatma hello aracını yükleyin. Merhaba aracı açıldığında, kaynak ve hedef hello geçiş aracı için seçebileceğiniz bir ilk bağlantı sayfasıyla istenir. Bu aşamada, SQL Server ve Azure SQL veritabanı kaynakları ve SQL Data Warehouse hedef olarak olarak destekliyoruz. Bu seçtikten sonra tooconnect tooyour kaynak sunucunun sunucu adını doldurma ve kimlik doğrulaması ve 'Bağlan' a tıklayarak istenir.

Kimlik doğrulandıktan sonra hello aracı bağlı hello sunucusunda mevcut olan veritabanlarının bir listesini gösterir. Toomigrate ve 'seçili geçirme üzerinde' e tıklayarak istediğiniz veritabanını seçerek hello geçişe başlayabilirsiniz.

## <a name="migration-report"></a>Geçiş raporu
'Veritabanı uyumluluğu denetle' hello aracında seçerek tüm nesne uyumsuzlukları özetleyen bir rapor oluşturacağını hello veritabanında toomigrate istedi. Merhaba SQL veri ambarı'nda mevcut SQL Server işlevselliği bazıları daha geniş bir listesi bulunabilir bizim [geçiş belgeleri][migration documentation]. Merhaba rapor oluşturulduktan sonra mümkün toosave ve Excel'de Aç hello rapor olacaktır.

Lütfen hello geçiş şeması, 'Nesnesi' siparişi tooallow hemen geçişte bu verilerin ayarlanacak olarak tanımlanan çoğu sorunların oluştururken unutmayın. Lütfen hello şema uygulamadan önce toomake ek ayarlamalar istemediğiniz hello değişiklikleri tooensure gözden geçirin.

## <a name="migrate-schema"></a>Geçiş şeması
Bağlandıktan sonra geçirme'Schema ' seçerek hello seçili tablo için şema geçiş komut dosyası oluşturur. Bu komut dosyası bağlantı noktalarını hello yapı Merhaba tablonun uyumlu veri türleri toomore uyumlu formları eşler ve bu hello geçiş ayarları hello kullanıcı tarafından belirtilirse, güvenlik kimlik bilgileri ve şema oluşturur. Bu kod hedeflenen hello SQL Data Warehouse örneğine karşı çalıştırabilirsiniz tooa dosyasını kaydettiğiniz tooyour Panoya kopyalanan veya daha fazla eylemi gerçekleştirmeden önce satır içi bile düzenlenebilir.  

Yukarıdaki şema gözden geçirme hello geçiş bu hello değiştiğinde belirtilenlerle aracı sipariş tooensure yaptı, tam olarak bunları anladığınızdan.  

## <a name="migrate-data"></a>Geçiş verileri
Merhaba 'Verileri geçirmek' seçeneğini tıklatarak, veri ilk tooflat dosyalarınızı sunucunuzda, taşınır BCP komut dosyaları oluşturabilir ve ardından SQL veri ambarı doğrudan. Küçük miktarda veri ve yeniden deneme olarak taşımak için bu işlemi yerleşik olmayan ve hataları hello ağ bağlantı kaybı oluşabilir öneririz. İçinde toorun Bu sipariş, toohave hello BCP komut satırı yardımcı programının yüklü olması gerekir ve hello veri hello şeması zaten oluşturulmuş olması gerekir.

Out Parametreleri hello doldurduktan sonra tooclick geçiş çalıştırmanız yeterlidir ve iki paket kümesini oluşturulur tooyour belirtilen konum. Merhaba dışarı aktarma dosyası sipariş tooexport verilerde geçiş kaynağınızdan düz dosyalarıyla çalıştırın ve hello içeri aktarma dosyası sipariş tooimport verilerinizi SQL Data Warehouse'a çalıştırın.

## <a name="next-steps"></a>Sonraki adımlar
Bazı verileri geçirdikten, nasıl çok denetleyin[geliştirmek][develop].

<!--Image references-->

<!--Article references-->
[migration documentation]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md

<!--Other Web references--> 
[Download Migration Utility]: https://migrhoststorage.blob.core.windows.net/sqldwsample/DataWarehouseMigrationUtility.zip
