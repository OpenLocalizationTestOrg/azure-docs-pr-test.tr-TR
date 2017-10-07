---
title: "aaaDebug U-SQL işleri | Microsoft Docs"
description: "Nasıl toodebug U-SQL Visual Studio kullanarak köşe başarısız öğrenin."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: bcd0b01e-1755-4112-8e8a-a5cabdca4df2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 09/02/2016
ms.author: saveenr
ms.openlocfilehash: 092bffa1a59ed91c5837402d0276447480b923fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a>Hata ayıklama başarısız U-SQL işleri için kullanıcı tanımlı C# kodu

U-SQL, kod tooadd işlevselliği özel ayıklayıcısı veya reducer gibi yazma için C# kullanarak genişletilebilirlik modeli sağlar. toolearn daha, fazla [U-SQL Programlama Kılavuzu](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf). Uygulamada hata ayıklama herhangi bir kod gerekebilir ve büyük veri sistemlerini yalnızca sınırlı çalışma zamanı hata ayıklama günlük dosyaları gibi bilgileri sağlayabilir.

Visual Studio için Azure Data Lake araçları adlı bir özelliği sağlar **köşe hata ayıklama başarısız**, olanak sağlayan, hata ayıklama için hello bulut tooyour yerel makinedeki başarısız bir işi klonlayın. Merhaba yerel kopya hello tüm bulut ortamı, herhangi bir giriş veri ve kullanıcı kodu da dahil olmak üzere yakalar.

Merhaba aşağıdaki videoda Azure Data Lake araçları Debug başarısız köşe için Visual Studio gösterilmektedir.

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> Visual Studio zaten yüklü değilse şu iki güncelleştirmeleri hello gerektirir: [Microsoft Visual C++ 2015 Redistributable güncelleştirme 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) ve [Evrensel C çalışma zamanı için Windows](https://www.microsoft.com/download/details.aspx?id=50410).

## <a name="download-failed-vertex-toolocal-machine"></a>Yükleme başarısız köşe toolocal makine

Visual Studio için Azure Data Lake araçları başarısız bir işi açtığınızda, sarı bir uyarı çubuğu hello hata sekmesinde ayrıntılı hata iletileri ile bakın.

1. Tıklatın **karşıdan** tüm hello toodownload gerekli kaynakları ve giriş akışları. Merhaba indirme tamamlanmazsa, tıklatın **yeniden**.

2. Tıklatın **açık** toogenerate yerel hata ayıklama ortamı hello yükleme tamamlandıktan sonra. Hata ayıklama çözümü olan yeni bir Visual Studio örneği otomatik olarak oluşturulan ve açılır.

![Azure Data Lake Analytics U-SQL hata ayıklama visual studio indirme köşe](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

İşlerini arka plan kodu kaynak dosyaları veya kayıtlı derlemeler içerebilir ve bu iki türlerinin farklı hata ayıklama senaryolar vardır.

- [Arka plan kodu ile başarısız bir işi hata ayıklama](#debug-job-failed-with-code-behind)
- [Başarısız bir işi derlemeleri ile hata ayıklama](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a>Hata ayıklama işi arka plan kodu ile başarısız oldu

U-SQL işi başarısız olursa ve hello işi kullanıcı kodu içerir (genellikle adlı `Script.usql.cs` U-SQL projesinde), kaynak kodu çözüm hata ayıklama hello alınır.  Buradan hello Visual Studio hata ayıklama araçları (izleme, değişkenleri, vb.) tootroubleshoot hello sorun kullanabilirsiniz.

> [!NOTE]
> Hata ayıklama önce emin toocheck olması **ortak dil çalışma zamanı özel durumları** hello özel ayarları penceresinde (**Ctrl + Alt + E**).

![Azure Data Lake Analytics U-SQL hata ayıklama visual studio ayarı](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. Tuşuna **F5** toorun hello arka plan kodu kodu. Bir özel durum tarafından durduruluncaya kadar çalışmayacaktır.

2. Açık hello `ADLTool_Codebehind.usql.cs` dosya ve kesme, tuşuna basarak **F5** toodebug hello kod adım adım.

    ![Azure Data Lake Analytics U-SQL hata ayıklama özel durumu](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a>Hata ayıklama işi derlemeleri ile başarısız oldu

U-SQL komut dosyanıza kayıtlı derlemeleri kullanırsanız, hello sistem hello kaynak kodu otomatik olarak alınamıyor. Bu durumda, hello derlemeleri kaynak kodu dosyaları toohello çözümü el ile ekleyin.

### <a name="configure-hello-solution"></a>Merhaba çözümünüzü yapılandırma

1. Sağ **çözüm 'VertexDebug' > Ekle > mevcut proje...**  toofind derlemelerin kaynak kodu hello ve çözüm hata ayıklama hello proje toohello ekleyin.

    ![Azure Data Lake Analytics U-SQL hata ayıklama proje ekleyin](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. Sağ **LocalVertexHost > Özellikler** hello çözüm ve kopyalama hello içinde **çalışma dizini** yolu.

3. Sağ **derleme kaynak kod projesi > Özellikleri**seçin hello **yapı** sekmesinde solda ve kopyalanan hello yolu olarak Yapıştır **çıkış > çıkış yolu**.

    ![Azure Data Lake Analytics U-SQL hata ayıklama pdb yolunu ayarlama](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. Tuşuna **Ctrl + Alt + E**, denetleme **ortak dil çalışma zamanı özel durumları** özel ayarları penceresinde.

### <a name="start-debug"></a>Hata ayıklama Başlat

1. Sağ **derleme kaynak kod projesi > yeniden** toooutput .pdb dosyaları toohello `LocalVertexHost` çalışma dizini.

2. Tuşuna **F5** ve başlangıç projesi bir özel durum tarafından durduruluncaya kadar çalışır. Güvenle yok sayabilirsiniz uyarı iletisi aşağıdaki hello görebilirsiniz. Tooa minute tooget toohello hata ayıklama ekranı alabilir.

    ![Azure Data Lake Analytics U-SQL hata ayıklama visual studio uyarı](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. Kaynak kodunuz açın ve kesme, tuşuna basarak **F5** toodebug hello kod adım adım.

Merhaba Visual Studio hata ayıklama araçları (izleme, değişkenleri, vb.) tootroubleshoot hello sorun de kullanabilirsiniz.

> [!NOTE]
> Merhaba derleme kaynak kod projesi hello kod güncelleştirilmiş toogenerate .pdb dosyaları değiştirdikten sonra her zaman yeniden oluşturun.

Hello Proje başarıyla tamamlarsa hata ayıklama sonra hello çıktı penceresinde hello iletiden gösterir:

```
hello Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Azure Data Lake Analytics U-SQL hata ayıklama başarılı](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-hello-job"></a>Merhaba işi yeniden gönderin

Hata ayıklama tamamladıktan sonra hello başarısız işi yeniden gönderin.

1. Arka plan kodu çözümleriyle işleri için C# kodu hello arka plan kodu kaynak dosyaya kopyalayın (genellikle `Script.usql.cs`).
2. Derlemeler ile işleri için güncelleştirilmiş hello .dll derlemelerine ADLA veritabanınızı kaydedin:
    1. Sunucu Gezgini veya Bulut Gezgini'nden, hello genişletin **ADLA hesabı > veritabanları** düğümü.
    2. Sağ **derlemeleri** ve yeni .dll derlemeleriniz hello ADLA veritabanı ile kaydetme: ![Azure Data Lake Analytics U-SQL hata ayıklama derlemesi kaydetme](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)
3. İşinizi yeniden gönderin.

## <a name="next-steps"></a>Sonraki adımlar

- [U-SQL Programlama Kılavuzu](data-lake-analytics-u-sql-programmability-guide.md)
- [Azure Data Lake Analytics işleri için U-SQL kullanıcı tanımlı işleçleri geliştirme](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [Öğretici: Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme](data-lake-analytics-data-lake-tools-get-started.md)
