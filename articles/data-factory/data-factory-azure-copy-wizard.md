---
title: "aaaData Fabrika Azure Kopyalama Sihirbazı'nı | Microsoft Docs"
description: "Nasıl toouse hello veri fabrikası Azure Kopyalama Sihirbazı'nı toocopy desteklenen veri kaynakları toosinks verilerden hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 0974eb40-db98-4149-a50d-48db46817076
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: 188b3ae15f937b84a58aec1b979347ac8090abf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory-copy-wizard"></a>Azure Data Factory Kopyalama Sihirbazı
Hello Azure Data Factory Kopyalama Sihirbazı, genellikle bir uçtan uca veri tümleştirme senaryosunun ilk adımda veri alma hello işlemini kolaylaştırır. Azure Data Factory Kopyalama Sihirbazı'nı Hello geçerken, toounderstand herhangi JSON tanımları bağlı hizmetler, veri kümeleri ve işlem hatlarını gerekmez. Başlangıç Sihirbazı'nı bir ardışık düzen toocopy veri hello seçili veri kaynağı toohello seçili hedeften otomatik olarak oluşturur. Ayrıca, hello Kopyalama Sihirbazı'nı toovalidate hello veri yazma hello zamanında alınan yardımcı olur. Bu süre, tasarruf özellikle zaman, alma hello için verileri ilk kez hello veri kaynağından. toostart hello Kopyalama Sihirbazı'nı tıklatın hello **veri kopyalama** döşeme veri fabrikanızın hello giriş sayfasında.

![Kopyalama Sihirbazı](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="designed-for-big-data"></a>Büyük veriler için tasarlanmış
Bu sihirbaz dakika içinde çok çeşitli kaynaklardan toodestinations tooeasily taşıma verileri sağlar. Merhaba sihirbazda olduktan sonra kopyalama etkinliği ile işlem hattı otomatik olarak sizin için bağımlı Data Factory varlıklarını birlikte (bağlı hizmetler ve veri kümeleri) oluşturulur. Başka adım gerekli toocreate hello ardışık değildir.   

![Veri kaynağını seçin](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> Adım adım yönergeler toocreate bir Azure blob tooan Azure SQL veritabanı tablosu örnek ardışık düzen toocopy verilerden hello bkz [Kopyalama Sihirbazı'nı Öğreticisi](data-factory-copy-data-wizard-tutorial.md).
>
>

Merhaba Sihirbazı çeşitli veri ve nesne türleri için destek ile Merhaba başından aklınızda büyük veri tasarlanmıştır. Klasörleri, dosyaları ya da tablo yüzlerce taşıma Data Factory işlem hatlarını yazabilirsiniz. Başlangıç Sihirbazı otomatik veri Önizleme, şema yakalama ve eşleme ve verileri filtreleme destekler.

## <a name="automatic-data-preview"></a>Otomatik veri Önizleme
Merhaba veri istediğinizi olup hello seçili veri kaynağından sipariş toovalidate hello verilerin bir kısmını önizleyebilirsiniz toocopy. Merhaba kaynak verileri bir metin dosyasında ise, ayrıca, hello Kopyalama Sihirbazı'nı hello metin dosyasında toolearn hello satır ve sütun sınırlayıcıları ve şema otomatik olarak ayrıştırır.

![Dosya biçimi ayarları](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a>Şema yakalama ve eşleme
giriş verisi Hello şeması bazı durumlarda çıktı verilerini hello şeması eşleşmeyebilir. Bu senaryoda, hello kaynak şema toocolumns hello hedef şemasından toomap sütunlarından gerekir.

> [!TIP]
> SQL Server veya hello tablo hello hedef depo, veri fabrikası yoksa, Azure SQL Data Warehouse, Azure SQL veritabanına veri kopyalamayı kaynağının şemasını kullanarak Otomatik Tablo oluşturma desteği. ' Dan daha fazla bilgi edinin [Azure SQL veri Azure Data Factory kullanarak ambarından veri tooand taşıma](./data-factory-azure-sql-data-warehouse-connector.md).
>

Aşağı açılan liste tooselect hello kaynak şema toomap tooa sütunu sütundan hello hedef şemada kullanın. Merhaba Kopyalama Sihirbazı, düzeni sütun eşlemesi için toounderstand çalışır. Tooselect her hello sütunların ayrı ayrı gerekmediği için aynı düzeni toohello rest hello sütunlarının hello uygular toocomplete hello şema eşleme. Tercih ederseniz, bu eşlemelerin hello açılan listeleri toomap hello sütunları tek tek kullanarak geçersiz kılabilirsiniz. Merhaba düzeni daha fazla sütun eşlemesi olarak daha doğru olur. Merhaba Kopyalama Sihirbazı'nı sürekli hello düzeni güncelleştirir ve sonuçta ulaştığında hello sağ desen eşlemeyi hello sütun için istediğiniz tooachieve.     

![Şema eşleme](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a>Verileri filtreleme
Kopyalanan toobe toohello havuz veri deposu gereken kaynak veri tooselect hello veriler yalnızca filtre uygulayabilirsiniz. Filtreleme veri depolamak ve bu nedenle hello kopyalama işlemi hello verimliliğini artırır hello veri toobe kopyalanan toohello havuzunu hello hacmini azaltır. Esnek bir şekilde toofilter veri ilişkisel bir veritabanındaki hello SQL sorgu dili kullanarak sağlar veya kullanarak bir Azure blob klasördeki dosyaları [Data Factory işlevleri ve değişkenler](data-factory-functions-variables.md).   

### <a name="filtering-of-data-in-a-database"></a>Bir veritabanında veri filtreleme
Merhaba aşağıdaki ekran gösterilir hello kullanarak bir SQL sorgusu `Text.Format` işlevi ve `WindowStart` değişkeni.

![İfadeler doğrula](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a>Bir Azure blob klasöründe veri filtreleme
Merhaba klasör yolu toocopy verilerini temel çalışma zamanında belirlenir bir klasörden değişkenleri kullanabilirsiniz [sistem değişkenleri](data-factory-functions-variables.md#data-factory-system-variables). desteklenen hello değişkenleri: **{year}**, **{month}**, **{day}**, **{saat}**, **{dakika}**, ve **{özel}**. Örneğin: inputfolder / {year} / {month} / {day}.

Biçim aşağıdaki hello klasörlerde giriş varsayın:

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

Hello tıklatın **Gözat** için düğmesini **dosya veya klasör**, bu klasörlerin tooone göz atın (örneğin, 2016 03 -> -> 01 02 ->) ve'ı tıklatın **Seç**. Görmeniz gerekir `2016/03/01/02` hello metin kutusuna. Şimdi değiştir **2016** ile **{year}**, **03** ile **{month}**, **01** ile **{day} **, ve **02** ile **{saat}**ve tuşuna hello **sekmesini** anahtarı. Bu dört değişkenleri için aşağı açılır listeler tooselect hello biçimi görmeniz gerekir:

![Sistem değişkenleri kullanma](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

Hello ekran aşağıdaki gösterildiği gibi aynı zamanda kullanabilirsiniz bir **özel** değişkeni ve [biçim dizeleri desteklenen](https://msdn.microsoft.com/library/8kb3ddd4.aspx). tooselect yapıyı, kullanım hello sahip bir klasör **Gözat** ilk düğme. Bir değerle değiştirin **{özel}**ve tuşuna hello **sekmesini** hello biçim dizesi yazabileceğiniz anahtar toosee hello metin kutusu.     

![Özel değişken kullanma](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="scheduling-options"></a>Zamanlama Seçenekleri
Merhaba kopyalama işlemi bir kez veya bir zamanlamaya göre çalıştırabilirsiniz (saatlik, günlük, vb.). Bu seçeneklerin ikisi de şirket içi ve bulut yerel Masaüstü kopya çeşitli ortamlar genelinde hello bağlayıcılar hello derecesini için kullanılabilir.

Bir kerelik kopyalama işlemi yalnızca bir kez kaynak tooa hedef veri taşıma sağlar. Herhangi bir boyuta ve desteklenen bir biçim toodata geçerlidir. Zamanlanmış Başlangıç kopyası üzerinde önceden belirlenmiş bir yinelenme toocopy veri sağlar. Zengin ayarlarınızı (örneğin, yeniden deneme zaman aşımı ve uyarılar) kullanabileceğiniz tooconfigure hello zamanlanmış kopyalama.

![Zamanlama özellikleri](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a>Sonraki adımlar
Kopyalama etkinliği ile Merhaba Data Factory Kopyalama Sihirbazı toocreate bir ardışık düzen kullanarak hızlı kılavuz için bkz: [Öğreticisi: hello Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturmak](data-factory-copy-data-wizard-tutorial.md).
