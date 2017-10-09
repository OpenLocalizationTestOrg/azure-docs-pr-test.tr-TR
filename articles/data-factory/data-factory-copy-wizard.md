---
title: "aaaCopy veri kopyalama Sihirbazı - Azure ile kolayca | Microsoft Docs"
description: "Nasıl toouse hello desteklenen veri kaynakları toosinks toocopy verileri Data Factory Kopyalama Sihirbazı hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f904972f-cd33-48db-9755-2b3196ae4168
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 99437ec16facf3b94c8be18487ec89e9f13acc9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-or-move-data-easily-with-azure-data-factory-copy-wizard"></a>Kopyalama veya Azure Data Factory Kopyalama Sihirbazı ile kolayca veri taşıma
Hello Azure Data Factory Kopyalama Sihirbazı'nı tooease Merhaba, genellikle bir uçtan uca veri tümleştirme senaryosunun ilk adımda veri alma işlemidir. Azure Data Factory Kopyalama Sihirbazı'nı Hello geçerken, toounderstand herhangi JSON tanımları bağlı hizmetler, veri kümeleri ve işlem hatlarını gerekmez. Ancak, hello Sihirbazı'ndaki tüm hello adımları tamamladıktan sonra Başlangıç Sihirbazı otomatik olarak bir ardışık düzen toocopy veri hello seçili veri kaynağı toohello seçilen hedef oluşturur. Ayrıca, kopyalama Sihirbazı zamanınızın çoğunu kaydeder, yazma, başlangıç zamanında alınan toovalidate hello verileri yardımcı hello özellikle zaman, veri hello için ilk kez hello veri kaynağından alma. toostart hello Kopyalama Sihirbazı'nı tıklatın hello **veri kopyalama** döşeme veri fabrikanızın hello giriş sayfasında.

![Kopyalama Sihirbazı](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="an-intuitive-wizard-for-copying-data"></a>Veri kopyalama için sezgisel bir Sihirbazı
Bu sihirbaz dakika içinde çok çeşitli kaynaklardan toodestinations tooeasily taşıma verileri sağlar. Merhaba sihirbazda geçtikten sonra kopyalama etkinliği ile işlem hattı otomatik olarak bağımlı Data Factory varlıklarını birlikte (bağlı hizmetler ve veri kümeleri) oluşturulur. Başka adım gerekli toocreate hello ardışık değildir.   

![Veri kaynağını seçin](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> Bkz: [Kopyalama Sihirbazı'nı öğretici](data-factory-copy-data-wizard-tutorial.md) için adım adım yönergeler toocreate bir Azure blob tooan Azure SQL veritabanı tablosu örnek ardışık düzen toocopy verilerden makalesi. 
> 
> 

Merhaba Sihirbazı hello başından aklınızda büyük veri tasarlanmıştır. Bu, klasörleri, dosyaları ya da tablo hello veri Kopyala Sihirbazı'nı kullanarak yüzlerce taşıma basit ve verimli tooauthor Data Factory işlem hatlarını olur. Merhaba Sihirbazı'nı destekleyen üç özellik aşağıdaki hello: otomatik veri Önizleme, şema yakalama ve eşleme ve verileri filtreleme. 

## <a name="automatic-data-preview"></a>Otomatik veri Önizleme
Merhaba Kopyalama Sihirbazı'nı hello hello olan veri sağ toocopy istediğiniz verileri olup olmadığını, tooreview parçası hello hello verileri veri kaynağı için toovalidate seçtiğiniz sağlar. Merhaba kaynak verileri bir metin dosyasında ise, ayrıca, hello Kopyalama Sihirbazı'nı hello metin dosyasında toolearn satır ve sütun sınırlayıcıları ve şema otomatik olarak ayrıştırır. 

![Dosya biçimi ayarları](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a>Şema yakalama ve eşleme
giriş verisi Hello şeması bazı durumlarda çıktı verilerini hello şeması eşleşmeyebilir. Bu senaryoda, hello kaynak şema toocolumns hello hedef şemasından toomap sütunlarından gerekir. 

Merhaba Kopyalama Sihirbazı'nı otomatik olarak hello kaynak şema toocolumns hello hedef şemasında sütunlarında eşler. Hello eşlemeleri hello açılan listeleri kullanarak geçersiz kılabilir (veya) bir sütun hello veri kopyalanırken atlandı toobe gerekip gerekmediğini belirtin.   

![Şema eşleme](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a>Verileri filtreleme
Merhaba sihirbaz kopyalanan toobe toohello hedef/havuz veri deposu gereken toofilter kaynak veri tooselect yalnızca hello verileri sağlar. Filtreleme veri depolamak ve bu nedenle hello kopyalama işlemi hello verimliliğini artırır hello veri toobe kopyalanan toohello havuzunu hello hacmini azaltır. SQL sorgu dili (veya) dosyaları bir Azure blob klasörüne kullanarak esnek bir şekilde toofilter veri ilişkisel bir veritabanındaki sağlar [Data Factory işlevleri ve değişkenler](data-factory-functions-variables.md).   

### <a name="filtering-of-data-in-a-database"></a>Bir veritabanında veri filtreleme
Merhaba örnekte hello hello SQL sorgusu kullanır `Text.Format` işlevi ve `WindowStart` değişkeni. 

![İfadeler doğrula](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a>Bir Azure blob klasöründe veri filtreleme
Merhaba klasör yolu toocopy verilerini temel çalışma zamanında belirlenir bir klasörden değişkenleri kullanabilirsiniz [sistem değişkenleri](data-factory-functions-variables.md#data-factory-system-variables). desteklenen hello değişkenleri: **{year}**, **{month}**, **{day}**, **{saat}**, **{dakika}**, ve **{özel}**. Örnek: inputfolder / {year} / {month} / {day}.

Biçim aşağıdaki hello klasörlerde giriş varsayın:

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

Hello tıklatın **Gözat** için düğmesini **dosya veya klasör**, bu klasörlerin tooone göz atın (örneğin, 2016 03 -> -> 01 02 ->) ve'ı tıklatın **Seç**. Görmeniz gerekir `2016/03/01/02` hello metin kutusuna. Şimdi değiştir **2016** ile **{year}**, **03** ile **{month}**, **01** ile **{day}**, ve **02** ile **{saat}**, SEKME tuşuna basın. Bu dört değişkenleri için aşağı açılır listeler tooselect hello biçimi görmeniz gerekir:

![Sistem değişkenleri kullanma](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

Hello ekran aşağıdaki gösterildiği gibi aynı zamanda kullanabilirsiniz bir **özel** değişkeni ve [biçim dizeleri desteklenen](https://msdn.microsoft.com/library/8kb3ddd4.aspx). tooselect yapıyı, kullanım hello sahip bir klasör **Gözat** ilk düğme. Bir değerle değiştirin **{özel}**, sekme toosee hello metin kutusu hello biçim dizesi yazabileceğiniz tuşuna basın.     

![Özel değişken kullanma](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="support-for-diverse-data-and-object-types"></a>Çeşitli veri ve nesne türleri için destek
Merhaba Kopyalama Sihirbazı'nı kullanarak, klasörleri, dosyaları ya da tablo yüzlerce verimli bir şekilde taşıyabilirsiniz.

![Hangi toocopy verilerden tabloları seçin](./media/data-factory-copy-wizard/select-tables-to-copy-data.png)

## <a name="scheduling-options"></a>Zamanlama Seçenekleri
Merhaba kopyalama işlemi bir kez veya bir zamanlamaya göre çalıştırabilirsiniz (saatlik, günlük, vb.). Bu seçeneklerin ikisi de hello bağlayıcılar hello derecesini için şirket içi, Bulut ve yerel Masaüstü kopya kullanılabilir.

Bir kerelik kopyalama işlemi yalnızca bir kez kaynak tooa hedef veri taşıma sağlar. Herhangi bir boyuta ve desteklenen bir biçim toodata geçerlidir. Zamanlanmış Başlangıç kopyası üzerinde önceden belirlenmiş bir yinelenme toocopy veri sağlar. Zengin ayarlarınızı (örneğin, yeniden deneme zaman aşımı ve uyarılar) kullanabileceğiniz tooconfigure hello zamanlanmış kopyalama.

![Zamanlama özellikleri](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a>Sonraki adımlar
Kopyalama etkinliği ile Merhaba Data Factory Kopyalama Sihirbazı toocreate bir ardışık düzen kullanarak hızlı kılavuz için bkz: [Öğreticisi: hello Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturmak](data-factory-copy-data-wizard-tutorial.md).

