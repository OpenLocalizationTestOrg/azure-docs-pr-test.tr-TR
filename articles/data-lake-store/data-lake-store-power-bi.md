---
title: Power BI kullanarak Data Lake Store'da verileri aaaAnalyze | Microsoft Docs
description: "Azure Data Lake Store içinde depolanan Power BI tooanalyze verileri kullanma"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57d19d27-e135-49d9-a7ea-46c48ef4e3bd
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 6a1bfa80fd1b0dda59b7eaaae9ca1585ba42783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-in-data-lake-store-by-using-power-bi"></a>Power BI'ı kullanarak Data Lake Store'da verilerin çözümleme
Bu makalede, öğreneceksiniz nasıl toouse Power BI Desktop tooanalyze ve Azure Data Lake Store içinde depolanan verileri görselleştirin.

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce hello şunlara sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).
* **Azure Data Lake Store hesabı**. Merhaba yönergeleri izleyin [Azure Data Lake hello Azure Portal kullanarak Store ile çalışmaya başlama](data-lake-store-get-started-portal.md). Bu makalede adlı bir Data Lake Store hesabı zaten oluşturduğunuzu varsayar **mybidatalakestore**ve bir örnek veri dosyasını karşıya (**Drivers.txt**) tooit. Bu örnek dosya Merkezi'nden edinilebilir [Azure Data Lake Git deposu](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).
* **Power BI Desktop**. Buradan indirebilirsiniz [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=45331). 

## <a name="create-a-report-in-power-bi-desktop"></a>Power BI Desktop'ta rapor oluşturma
1. Power BI Desktop bilgisayarınızda başlatın.
2. Merhaba gelen **giriş** Şerit, tıklatın **Veri Al**ve ardından daha fazla. Merhaba, **Veri Al** iletişim kutusu, tıklatın **Azure**, tıklatın **Azure Data Lake Store**ve ardından **Bağlan**.
   
    ![Connect tooData Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account.png "Bağlan tooData Lake deposu")
3. Bir geliştirme aşamasında olan hello Bağlayıcısı hakkında bir iletişim kutusu görürseniz, toocontinue kabul et.
4. Merhaba, **Microsoft Azure Data Lake Store** iletişim kutusu, hello URL tooyour Data Lake Store hesabı sağlayın ve ardından **Tamam**.
   
    ![Data Lake Store için URL](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "Data Lake Store için URL")
5. Merhaba sonraki iletişim kutusunda tıklatın **oturum** Data Lake Store hesabında toosign. Siz olacaksınız tooyour kuruluşunuzun oturum açma sayfasına yeniden yönlendirildi. Merhaba istemleri toosign hello dikkate izleyin.
   
    ![Data Lake Store içine oturum](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "oturum Data Lake Store açın")
6. Başarıyla oturum açtıktan sonra tıklayın **Bağlan**.
   
    ![Connect tooData Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "Bağlan tooData Lake deposu")
7. Merhaba sonraki iletişim kutusunda, tooyour Data Lake Store hesabı karşıya hello dosyasını gösterir. Merhaba bilgileri doğrulayın ve ardından **yük**.
   
    ![Data Lake Deposu'ndan veri veri yükleme](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "veri Data Lake Deposu'ndan veri yükleme")
8. Merhaba veri Power BI başarıyla yüklendikten sonra hello alanlara aşağıdaki hello görürsünüz **alanları** sekmesi.
   
    ![Alınan alanları](./media/data-lake-store-power-bi/imported-fields.png "içe alanlar")
   
    Ancak, toovisualize ve hello veri çözümleme, biz hello veri toobe alanları izleyen hello kullanılabilir tercih
   
    ![Alanları istenen](./media/data-lake-store-power-bi/desired-fields.png "alanları istenen")
   
    Merhaba sonraki adımlarda hello istenen biçiminde hello sorgu tooconvert içeri hello veri güncelleştireceğiz.
9. Merhaba gelen **giriş** Şerit, tıklatın **Düzenle sorguları**.
   
    ![Sorguları düzenleme](./media/data-lake-store-power-bi/edit-queries.png "sorgularını düzenleme")
10. Merhaba altında hello sorgu Düzenleyicisi içindeki **içerik** sütun tıklatın **ikili**.
    
    ![Sorguları düzenleme](./media/data-lake-store-power-bi/convert-query1.png "sorgularını düzenleme")
11. Merhaba temsil eden bir dosya simgesini görürsünüz **Drivers.txt** karşıya dosya. Merhaba dosyasını sağ tıklatın ve **CSV**.    
    
    ![Sorguları düzenleme](./media/data-lake-store-power-bi/convert-query2.png "sorgularını düzenleme")
12. Aşağıda gösterildiği gibi bir çıktı görmeniz gerekir. Verilerinizi toocreate görselleştirmeleri kullanabileceğiniz bir biçimde kullanıma sunulmuştur.
    
    ![Sorguları düzenleme](./media/data-lake-store-power-bi/convert-query3.png "sorgularını düzenleme")
13. Merhaba gelen **giriş** Şerit'ye tıklayın **kapatın ve geçerli**ve ardından **kapatın ve geçerli**.
    
    ![Sorguları düzenleme](./media/data-lake-store-power-bi/load-edited-query.png "sorgularını düzenleme")
14. Merhaba sorgu güncelleştirildikten sonra hello **alanları** sekmesini hello görselleştirme için kullanılabilir yeni alanları gösterir.
    
    ![Alanları güncelleştirilmiş](./media/data-lake-store-power-bi/updated-query-fields.png "alanları güncelleştirildi")
15. Bize pasta grafik toorepresent her şehir için belirli bir ülke hello sürücüleri oluşturun. toodo, bu nedenle, aşağıdaki seçimler hello olun.
    
    1. Merhaba görselleştirmeleri sekmesinden pasta grafiği için hello simgeyi tıklatın.
       
        ![Pasta grafiği oluşturmak](./media/data-lake-store-power-bi/create-pie-chart.png "pasta grafik oluşturma")
    2. toouse olduğumuz hello sütunları **sütun 4** (Merhaba şehrin adı) ve **sütun 7** (Merhaba ülke adı). Bu sütunlardan sürükleyin **alanları** çok sekmesinde**görselleştirmeleri** sekmesinde aşağıda gösterildiği gibi.
       
        ![Görselleştirmelerinin](./media/data-lake-store-power-bi/create-visualizations.png "görselleştirmeler oluşturun")
    3. Merhaba pasta grafik şimdi hello biri aşağıda gösterildiği gibi benzer olmalıdır.
       
        ![Pasta grafik](./media/data-lake-store-power-bi/pie-chart.png "görselleştirmeler oluşturun")
16. Belirli bir ülkeye hello sayfa düzeyi filtreleri seçerek hello sürücü sayısı her şehrinde seçilmiş hello ülkenin şimdi görebilirsiniz. Örneğin, hello altında **görselleştirmeleri** sekmesinde, altında **sayfa düzeyi filtreleri**seçin **Brezilya**.
    
    ![Bir ülke seçin](./media/data-lake-store-power-bi/select-country.png "bir ülke seçin")
17. Merhaba pasta grafik otomatik olarak güncelleştirilen toodisplay hello sürücüleri Brezilya hello şehirlerde ' dir.
    
    ![Sürücüleri bir ülkede](./media/data-lake-store-power-bi/driver-per-country.png "ülke başına sürücüleri")
18. Merhaba gelen **dosya** menüsünde tıklatın **kaydetmek** toosave hello görselleştirme Power BI Desktop dosyası olarak.

## <a name="publish-report-toopower-bi-service"></a>Rapor tooPower BI hizmet yayımlama
Power BI Desktop'ta hello görselleştirmeleri oluşturduktan sonra bunu başkalarıyla toohello Power BI hizmetinde yayımlayarak paylaşabilirsiniz. Yönergeler için bkz: toodo [Power BI masaüstünden Yayımla](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/).

## <a name="see-also"></a>Ayrıca bkz.
* [Data Lake Analytics kullanarak Data Lake Store içinde verileri analiz etme](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

