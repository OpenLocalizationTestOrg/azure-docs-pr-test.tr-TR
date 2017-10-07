---
title: "kullanarak aaaTest ve hata ayıklama U-SQL işleri yerel çalıştırın ve Azure Data Lake U-SQL SDK hello | Microsoft Docs"
description: "Visual Studio ve hello Azure Data Lake U-SQL SDK tootest ve U-SQL hata ayıklama için toouse Azure Data Lake araçları yerel iş istasyonunda nasıl işler öğrenin."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/15/2016
ms.author: yanacai
ms.openlocfilehash: be04558a504acf6a088e207608ee2d4a011d3ffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-hello-azure-data-lake-u-sql-sdk"></a>Test ve U-SQL işleri yerel kullanılarak çalıştırması ve hello Azure Data Lake U-SQL SDK'sı tarafından hata ayıklama

Hello Azure Data Lake hizmetinde gibi Azure Data Lake araçları Visual Studio ve hello Azure Data Lake U-SQL SDK toorun U-SQL işleri için iş istasyonunuza, kullanabilirsiniz. Bu iki yerel çalıştırma özelliği, U-SQL işlerinizi test etme ve hata ayıklama işlemlerinde size zaman kazandırır.

## <a name="understand-hello-data-root-folder-and-hello-file-path"></a>Merhaba veri kök klasör ve hello dosya yolu anlama

Hem yerel çalıştırma hem de hello U-SQL SDK veri kök klasör gerektirir. Merhaba veri kök klasörü "yerel depolama" Merhaba yerel işlem hesabıdır. Eşdeğer toohello Azure Data Lake Store hesabını Data Lake Analytics hesabı değil. Tooa geçiş farklı bir veri kök tooa farklı depolama hesabı yalnızca değiştirme gibi klasörüdür. Farklı bir veri kök klasörlerle yaygın olarak paylaşılan veri tooaccess istiyorsanız, komut dosyalarınızı mutlak yollar kullanmanız gerekir. Veya dosya sistemi sembolik bağlantılar oluşturun (örneğin, **mklink** NTFS) hello veri kök klasör toopoint toohello altında paylaşılan veri.

Merhaba veri kök klasör için kullanılır:

- Veritabanları, tablolar, tablo değerli işlevler (Tvf) ve derlemeler çeşitli meta verileri depolar.
- Giriş hello ve U-SQL göreli yolda olarak tanımlanan çıkış yolları arayın. Göreli yollar kullanılarak kılar daha kolay toodeploy, U-SQL projeleri tooAzure.

U-SQL betikleri göreli bir yol ve yerel bir mutlak yolu kullanabilirsiniz. Merhaba göreli yolu göreli toohello belirtilen veri kök klasör yoludur. Öneririz, kullan "/" olarak hello sunucu tarafı ile uyumlu komut dosyalarınızı yol ayırıcı toomake hello olduğunu. Göreli yollar ve eşdeğer mutlak yollarına bazı örnekleri aşağıda verilmiştir. Bu örneklerde, C:\LocalRunDataRoot hello veri kök klasörüdür.

|Göreli yolu|Mutlak yolu|
|-------------|-------------|
|/ABC/DEF/input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|ABC/DEF/input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/ABC/DEF/input.csv |D:\abc\def\input.csv|

## <a name="use-local-run-from-visual-studio"></a>Kullanım yerel Visual Studio'dan çalıştırma

Visual Studio için Data Lake araçları, Visual Studio'da U-SQL yerel çalıştırma deneyimi sağlar. Bu özelliği kullanarak şunları yapabilirsiniz:

- C# derlemeleri'nin yanı sıra yerel olarak bir U-SQL komut dosyasını çalıştırın.
- Bir C# derleme yerel olarak hata ayıklama.
- Oluşturun, görüntüleyin ve U-SQL katalogları (yerel veritabanlarını, derlemeleri, şemaları ve tabloları) Server Explorer'dan silin. Merhaba yerel katalog de ayrıca ve Sunucu Gezgini'nden bulabilirsiniz.

    ![Visual Studio yerel çalıştırma yerel katalog için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

Merhaba Data Lake araçları yükleyici hello varsayılan veri kök klasör olarak kullanılan bir C:\LocalRunRoot klasörü toobe oluşturur. Merhaba varsayılan yerel çalıştırma paralellik 1'dir.

### <a name="tooconfigure-local-run-in-visual-studio"></a>tooconfigure yerel Visual Studio'da çalıştırın

1. Visual Studio'yu açın.
2. Açık **Sunucu Gezgini**.
3. Genişletme **Azure** > **Data Lake Analytics**.
4. Merhaba tıklatın **Data Lake** menüsüne ve ardından **seçenekleri ve ayarları**.
5. Merhaba sol ağacında **Azure Data Lake**, genişletin ve ardından **genel**.

    ![Yerel çalıştırma Visual Studio için Data Lake araçları ayarlarını yapılandırma](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

Visual Studio U-SQL projesi çalıştırma yerel gerçekleştirmek için gerekli değildir. Bu bölümü, U-SQL betikleri Azure'dan çalışmasını farklıdır.

### <a name="toorun-a-u-sql-script-locally"></a>yerel olarak toorun U-SQL komut dosyası
1. Visual Studio'dan U-SQL projenizi açın.   
2. Çözüm Gezgini'nde U-SQL komut dosyasını sağ tıklatın ve ardından **betiği Gönder**.
3. Seçin **(yerel)** hello Analytics toorun kodunuzu yerel hesap olarak.
Merhaba tıklatarak **(yerel)** hesap komut penceresinde hello üstündeki ve ardından **gönderme** (veya Merhaba Ctrl + F5 klavye kısayolunu kullanın).

    ![Visual Studio yerel çalıştırma gönderme işleri için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a>Betikler ve C# derlemeleri üzerinde yerel olarak hata ayıklama

C# derlemeleri gönderme ve tooAzure Data Lake Analytics Hizmeti'ne kaydetme ayıklayabilirsiniz. Hem dosyanın arkasındaki hello kodda ve başvuruda bulunulan bir C# projesinde kesme noktaları ayarlayabilirsiniz.

#### <a name="toodebug-local-code-in-code-behind-file"></a>dosyanın arkasındaki kodda yerel kod toodebug

1. Dosyanın arkasındaki hello kodda kesme noktalarını ayarlayın.
2. F5 toodebug hello komut dosyası yerel olarak tuşuna basın.

> [!NOTE]
   > Aşağıdaki yordam yalnızca works Visual Studio 2015'hello. Eski Visual Studio'da gerekebilir toomanually hello pdb dosyalarını ekleyin.  
   >
   >

#### <a name="toodebug-local-code-in-a-referenced-c-project"></a>başvuruda bulunulan bir C# projesinde toodebug yerel kod

1. Bir C# derleme projesi oluşturun ve toogenerate hello çıkış DLL'sini oluşturun.
2. U-SQL deyimi kullanarak hello DLL'yi kaydetme:

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. Merhaba C# kodunda kesme noktalarını ayarlayın.
4. Hello C# DLL'sine yerel olarak başvuran ile toodebug hello betik F5 tuşuna basın.

## <a name="use-local-run-from-hello-data-lake-u-sql-sdk"></a>Data Lake U-SQL SDK Hello çalıştırmak yerel kullanın

Ayrıca Visual Studio kullanarak yerel olarak toorunning U-SQL komut dosyaları, komut satırı ve programlama arabirimleri ile yerel olarak hello Azure Data Lake U-SQL SDK toorun U-SQL betiklerini kullanabilirsiniz. Bunlar arasında U-SQL yerel testinizi ölçeklendirebilirsiniz.

Daha fazla bilgi edinmek [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).


## <a name="next-steps"></a>Sonraki adımlar

* toosee daha karmaşık bir sorgu görmek [Azure Data Lake Analytics'i kullanarak Web sitesi günlüklerini çözümleme](data-lake-analytics-analyze-weblogs.md).
* tooview iş ayrıntılarını görmek [kullanım iş tarayıcı ve Azure Data Lake Analytics işleri için iş görünümünde](data-lake-analytics-data-lake-tools-view-jobs.md).
* toouse hello köşe yürütme görünümü bkz [kullanım hello köşe yürütme görünümü Visual Studio için Data Lake araçları içinde](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).
