---
title: "Azure Data Lake Analytics işleri için U-SQL aaaDevelop derlemeleri | Microsoft Docs"
description: "Nasıl toodevelop derlemeleri toobe kullanılan ve Data Lake Analytics işleri yeniden öğrenin. "
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/30/2016
ms.author: jejiang
ms.openlocfilehash: 86dd17b25e0967306ed36bb5b7f3178d9409d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a>Azure Data Lake Analytics işleri için U-SQL derlemeleri geliştirin
Nasıl tooturn arka plan kod içinde kullanılan ve Data Lake Analytics işleri yeniden derlemeleri toobe öğrenin. 

U-SQL, kendi özel kod kolay tooadd C#, VB.Net veya F # gibi .net dillerinde kolaylaştırır. Bu gibi durumlarda, kendi çalışma zamanı toosupport bile diğer dillerde dağıtabilirsiniz.

Merhaba en kolay yolu toouse özel toouse hello Data Lake araçları, Visual Studio'nun arka plan kodu özellikleri kodudur. Daha fazla bilgi için bkz: [öğretici: Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme](data-lake-analytics-data-lake-tools-get-started.md). Arka plan kodu kullanmanın birkaç dezavantajları vardır:

- Merhaba kaynak kodu her komut dosyası gönderi için karşıya.
- arka plan kodu diğer işlemlerle paylaşılamaz.

tooaddress bu dezavantajları arka plan kodu derlemelerine açmak ve hello derlemeleri toohello Data Lake Analytics Kataloğu kaydedin.

## <a name="prerequisites"></a>Ön koşullar
* Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 4 veya Visual Studio 2012 Visual C++ yüklü güncelleştirme
* .NET sürüm 2.5 veya üzeri için Microsoft Azure SDK.  Merhaba Web Platformu yükleyicisi veya Visual Studio Yükleyicisi'ni kullanarak yükleme
* Bir Data Lake Analytics hesabı.  Bkz. [Azure portalını kullanarak Azure Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-portal.md).
* Merhaba aracılığıyla gidin [Azure Data Lake Analytics U-SQL Studio ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md) Öğreticisi.
* TooAzure bağlanın.
* Merhaba kaynak verileri yüklemek için bkz: [Azure Data Lake Analytics U-SQL Studio ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md). 

## <a name="develop-assemblies-for-u-sql"></a>U-SQL derlemelerde geliştirin

**toocreate ve U-SQL işi gönderin**

1. Merhaba gelen **dosya** menüsünde tıklatın **yeni**ve ardından **proje**.
2. Genişletme **yüklü**, **şablonları**, **Azure Data Lake**, **U-SQL(ADLA)**seçin hello **sınıf kitaplığı (için U-SQL Uygulama)** şablonu ve ardından **Tamam**.
3. Kodunuzu Class1.cs içinde yazın.  Merhaba, bir kod örneği verilmiştir.

        using Microsoft.Analytics.Interfaces;

        namespace USQLApplication_codebehind
        {
            [SqlUserDefinedProcessor]
            public class MyProcessor : IProcessor
            {
                public override IRow Process(IRow input, IUpdatableRow output)
                {
                    output.Set(0, input.Get<string>(0));
                    output.Set(0, input.Get<string>(0));
                    return output.AsReadOnly();
                }
            }
        }
4. Merhaba tıklatın **yapı** menüsüne ve ardından **yapı çözümü** toocreate hello dll.

## <a name="register-assemblies"></a>Derlemeleri kaydetme

Bkz: [kullanım Data Lake Analytics(U-SQL) katalog](data-lake-analytics-use-u-sql-catalog.md).


## <a name="use-hello-assemblies"></a>Merhaba derlemeleri kullanma

Bkz: [hello Azure Data Lake araçları kullanmak için Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).

## <a name="see-also"></a>Ayrıca bkz.
* [PowerShell kullanarak Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-powershell.md)
* [Hello Azure portal kullanarak Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-portal.md)
* [U-SQL uygulamalarını geliştirmek için Visual Studio için Data Lake araçları kullanın](data-lake-analytics-data-lake-tools-get-started.md)
* [Kullanım Data Lake Analytics(U-SQL) Kataloğu](data-lake-analytics-use-u-sql-catalog.md)
* [Hello Azure Data Lake araçları Visual Studio kodunu kullanın](data-lake-analytics-data-lake-tools-for-vscode.md)
