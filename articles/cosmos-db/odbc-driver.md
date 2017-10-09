---
title: "aaaConnect tooAzure Cosmos DB BI analiz araçları kullanarak | Microsoft Docs"
description: "Nasıl toouse hello Azure Cosmos DB ODBC sürücüsü toocreate tabloları ve görünümleri normalleştirilmiş veri BI ve veri analizi yazılımda görüntülenebilir böylece öğrenin."
keywords: "ODBC, odbc sürücüsü"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 9967f4e5-4b71-4cd7-8324-221a8c789e6b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.openlocfilehash: e12a70f7805445f09fac01411e4bfbccc9a29c7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-cosmos-db-using-bi-analytics-tools-with-hello-odbc-driver"></a>TooAzure Cosmos DB bağlanmak BI analiz araçları hello ODBC sürücüsü ile kullanma

Böylece çözümlemek ve Azure Cosmos DB verilerinizin de görselleştirmelerinin, tooconnect tooAzure Cosmos DB BI analizi kullanarak SQL Server Integration Services, Power BI Desktop ve Tableau gibi araçları hello Azure Cosmos DB ODBC sürücüsü etkinleştirir çözümleri.

Hello Azure Cosmos DB ODBC sürücüsü ODBC 3.8 uyumlu olduğundan ve ANSI SQL-92 sözdizimini destekler. verileri Azure Cosmos veritabanı renormalize sürücü teklifleri Zengin özellikleri toohelp hello. Merhaba sürücüsü kullanarak, Azure Cosmos veritabanı veri tabloları ve görünümleri olarak gösterebilir. Merhaba sürücü tooperform SQL işlemlerini hello tabloları ve görünümleri grupla sorguları, ekleme, güncelleştirme ve silme de dahil olmak üzere karşı sağlar.

## <a name="why-do-i-need-toonormalize-my-data"></a>Verilerimi neden toonormalize gerekiyor?
Azure Cosmos DB veritabanında, uygulamaları tooiterate etkinleştirerek uygulamaların hızlı geliştirme sağlar şekilde verilerini hello anında model ve bunları sınırlamak tooa kesin şema yok. Tek bir Azure Cosmos DB veritabanı çeşitli yapıların JSON belgeleri içerebilir. Bu hızlı uygulama geliştirme için harikadır, ancak tooanalyze istediğiniz ve veri analizi ve BI araçları kullanarak verilerinizi raporlarını oluştururken hello veri genellikle düzleştirilmiş toobe gerekir ve tooa belirli şema uyması.

Merhaba ODBC sürücüsü nereden geldiğini budur. Merhaba ODBC sürücüsünü kullanarak, verisine Azure Cosmos veritabanı tabloları ve görünümleri tooyour veri çözümleme ve raporlama sığdırma renormalized artık gerekir. renormalized hello şemaları arka plandaki veri hello üzerinde hiçbir etkisi ve geliştiricilerin tooadhere toothem sınırlamak değil, bunlar yalnızca, tooleverage ODBC uyumlu araçları tooaccess hello veri sağlar. Artık Azure Cosmos DB veritabanınızı yalnızca Geliştirme ekibiniz için sık kullanılan olmayacak, ancak veri çözümleyiciler memnuniyet çok.

Şimdi sağlar hello ODBC sürücüsü ile çalışmaya başlayın.

## <a id="install"></a>1. adım: hello Azure Cosmos DB ODBC sürücüsünü yükleme

1. Ortamınız için Hello sürücüleri yükleyin:

    * [Microsoft Azure Cosmos DB ODBC 64-bit.msi](https://aka.ms/documentdb-odbc-64x64) 64-bit Windows için
    * [Microsoft Azure Cosmos DB ODBC 32 x 64-bit.msi](https://aka.ms/documentdb-odbc-32x64) 32-bit 64-bit Windows için
    * [Microsoft Azure Cosmos DB ODBC 32-bit.msi](https://aka.ms/documentdb-odbc-32x32) 32-bit Windows için

    Çalışma hello MSI dosyası yerel olarak hangi başlatır hello **Microsoft Azure Cosmos DB ODBC sürücüsünü Yükleme Sihirbazı'nı**. 
2. Merhaba varsayılan giriş tooinstall hello ODBC sürücüsünü kullanarak hello Yükleme Sihirbazı'nı tamamlayın.
3. Açık hello **ODBC Veri Kaynağı Yöneticisi** bilgisayarınızda uygulama, bunu yapabilirsiniz yazarak **ODBC veri kaynakları** hello Windows Arama kutusu. 
    Hello sürücü hello tıklayarak yüklendiğini doğrulayabilirsiniz **sürücüleri** sekmesi ve sağlama **Microsoft Azure Cosmos DB ODBC sürücüsü** listelenir.

    ![Azure Cosmos DB ODBC Veri Kaynağı Yöneticisi](./media/odbc-driver/odbc-driver.png)

## <a id="connect"></a>2. adım: tooyour Azure Cosmos DB veritabanına bağlanın

1. Sonra [yükleme hello Azure Cosmos DB ODBC sürücüsü](#install), hello içinde **ODBC Veri Kaynağı Yöneticisi** penceresinde tıklatın **Ekle**. Bir kullanıcı veya sistem DSN oluşturabilirsiniz. Bu örnekte, bir kullanıcı DSN'si oluşturuyoruz.
2. Merhaba, **yeni veri kaynağı oluştur** penceresinde, seçin **Microsoft Azure Cosmos DB ODBC sürücüsü**ve ardından **son**.
3. Merhaba, **Azure Cosmos DB ODBC sürücüsü SDN Kurulum** penceresinde hello aşağıdakileri doldurun: 

    ![Azure Cosmos DB ODBC sürücüsü DSN Kurulum penceresi](./media/odbc-driver/odbc-driver-dsn-setup.png)
    - **Veri kaynağı adı**: hello ODBC DSN için kendi kolay ad. Bu ad benzersiz tooyour Azure Cosmos DB hesabı, birden çok hesabı varsa, bu nedenle uygun şekilde adlandırın.
    - **Açıklama**: hello veri kaynağı kısa bir açıklaması.
    - **Ana bilgisayar**: Azure Cosmos DB hesabınız için URI. Bu hello Azure Cosmos DB anahtarlar dikey penceresinde hello Azure Portalı'ndan hello ekran aşağıdaki gösterildiği gibi alabilirsiniz. 
    - **Erişim tuşu**: hello ekran aşağıdaki gösterildiği gibi birincil veya ikincil, okuma-yazma veya salt okunur anahtarından hello Azure Cosmos DB anahtarlar dikey penceresinde hello Azure portal hello. Merhaba DSN salt okunur veri işleme ve raporlama için kullanılıyorsa hello salt okunur anahtarı kullanmanızı öneririz.
    ![Azure Cosmos DB anahtarlar dikey penceresi](./media/odbc-driver/odbc-driver-keys.png)
    - **Erişim anahtarı şifrelemek**: Bu makinenin hello kullanıcı temelli hello en iyi seçenek seçin. 
4. Merhaba tıklatın **Test** düğmesini toomake bağlantı tooyour Azure Cosmos DB hesabı emin. 
5. Tıklatın **Gelişmiş Seçenekler** ve kümesi hello aşağıdaki değerler:
    - **Sorgu tutarlılık**: Select hello [tutarlılık düzeyi](consistency-levels.md) işlemleriniz için. Merhaba, oturum varsayılandır.
    - **Yeniden deneme sayısı**: hello sayısı girin tooretry hello ilk istek tooservice azaltma nedeniyle tamamlanmazsa bir işlem.
    - **Şema dosyası**: çeşitli seçenekler burada sahip.
        - Varsayılan olarak, bu girdi (boş), olduğu gibi bırakarak hello sürücü hello ilk sayfa verileri her koleksiyonun tüm koleksiyonlar toodetermine hello şeması için tarar. Bu koleksiyon eşleme bilinir. Tanımlanan bir şema dosyası olmadan hello sürücü her bir sürücü oturumu için tooperform hello tarama ve daha yüksek başlama hello DSN kullanarak bir uygulama süresi neden olabilir. Bir şema dosyası her zaman için DSN ilişkilendirmek öneririz.
        - Bir şema dosyası zaten varsa (kullanılarak oluşturulan bir büyük olasılıkla hello [şema Düzenleyicisi](#schema-editor)), tıklayabilirsiniz **Gözat**, tooyour dosya gidin, tıklatın **kaydetmek**ve ardından **Tamam**.
        - Yeni bir şema toocreate istiyorsanız, **Tamam**ve ardından **şema Düzenleyicisi** hello ana penceresinde. Toohello devam [şema Düzenleyicisi](#schema-editor) bilgi. Hello yeni şema dosyası oluşturduktan sonra lütfen toogo geri toohello unutmayın **Gelişmiş Seçenekler** penceresi tooinclude yeni oluşturulan hello şema dosyası.

6. Tamamlayıp kapattığınızda hello sonra **Azure Cosmos DB ODBC sürücüsü DSN Kurulum** penceresinde, yeni kullanıcı DSN hello toohello Kullanıcı DSN sekmesi eklendi.

    ![Yeni Azure Cosmos DB ODBC DSN hello kullanıcı DSN'si sekmesindeki](./media/odbc-driver/odbc-driver-user-dsn.png)

## <a id="#collection-mapping"></a>3. adım: hello koleksiyonu eşleme yöntemini kullanarak bir şema tanımı oluşturma

İki tür kullanabileceğiniz örnekleme yöntemi vardır: **koleksiyonu eşleme** veya **tablo sınırlayıcıları**. Bir örnekleme oturumu örnekleme yöntemlerin her ikisi de kullanabilir, ancak her koleksiyon yalnızca belirli örnekleme yöntemini kullanabilirsiniz. Merhaba adımları hello veri için bir şema hello koleksiyonu eşleme yöntemini kullanarak bir veya daha fazla içinde koleksiyonlar oluşturun. Bu örnekleme yöntemini hello veri toplama toodetermine hello yapısını hello sayfasındaki hello verileri alır. Bu, bir koleksiyon tooa tabloda hello ODBC yan ye dönüştürür. Bir koleksiyondaki Hello veriler homojen olduğunda bu örnekleme verimli ve hızlı yöntemdir. Bir koleksiyon heterogenous türdeki veriler içeriyorsa, hello kullanmanız önerilir [tablo sınırlayıcıları yöntemi eşleme](#table-mapping) toodetermine hello veri yapılarını hello koleksiyonundaki daha sağlam örnekleme yöntemini sağladığı gibi. 

1. Adım 1-4'te tamamladıktan sonra [Bağlan tooyour Azure Cosmos DB veritabanı](#connect),'ı tıklatın **şema Düzenleyicisi** hello içinde **Azure Cosmos DB ODBC sürücüsü DSN Kurulum** penceresi.

    ![Hello Azure Cosmos DB ODBC sürücüsü DSN Kurulumu penceresinde şema Düzenleyici düğmesi](./media/odbc-driver/odbc-driver-schema-editor.png)
2. Merhaba, **şema Düzenleyicisi** penceresinde tıklatın **Yeni Oluştur**.
    Merhaba **oluşturmak şema** penceresinde hello Azure Cosmos DB hesabı tüm hello koleksiyonları görüntüler. 
3. Bir veya daha fazla koleksiyon toosample seçin ve ardından **örnek**. 
4. Merhaba, **Tasarım görünümünde** sekmesi, hello veritabanı, şema ve tablo temsil edilen. Merhaba Tablo görünümünde hello tarama hello sütun adları (SQL adı, kaynak adı, vb.) ile ilişkili özellikleri hello kümesini görüntüler.
    Her sütun için değiştirebileceğiniz hello sütun SQL adı, hello SQL türü SQL uzunluğu (varsa), Ölçek (varsa), duyarlık (varsa) ve null atanabilir.
    - Ayarlayabileceğiniz **sütunu gizle** çok**doğru** , sorgu sonuçları sütundan tooexclude istiyorsanız. Sütunları gizleme sütun işaretli = true hala hello şema bir parçası olsa seçimi ve yansıtma, döndürülmez. Örneğin, "_" ile başlayan hello Azure Cosmos DB sistem gerekli özelliklerinin tümü gizleyebilirsiniz.
    - Merhaba **kimliği** hello normalleştirilmiş şemasında hello birincil anahtarı olarak kullanılan gizlenemez hello yalnızca alan bir sütundur. 
5. Merhaba şemasını tanımlama tamamladıktan sonra tıklatın **dosya** | **kaydetmek**toohello directory toosave hello şeması gidin ve ardından **kaydetmek**.

    Hello gelecekteki toouse istiyorsanız bu şema bir DSN ile hello Azure Cosmos DB ODBC sürücüsü DSN Kurulum penceresi (aracılığıyla ODBC Veri Kaynağı Yöneticisi hello) açın, Gelişmiş Seçenekler'i tıklatın ve ardından şema kaydedilmiş toohello hello şema dosyası kutusuna gidin. Bir şema dosyası tooan var olan bir DSN hello DSN bağlantı tooscope toohello veri ve şema tarafından tanımlanan yapısını değiştirir.

## <a id="table-mapping"></a>4. adım: hello tablo-sınırlayıcıları bir şema tanımı oluşturma yöntemi eşleme

İki tür kullanabileceğiniz örnekleme yöntemi vardır: **koleksiyonu eşleme** veya **tablo sınırlayıcıları**. Bir örnekleme oturumu örnekleme yöntemlerin her ikisi de kullanabilir, ancak her koleksiyon yalnızca belirli örnekleme yöntemini kullanabilirsiniz. 

Merhaba aşağıdaki adımları hello veri için bir şema hello kullanarak bir veya daha fazla koleksiyon oluşturmanıza **tablo sınırlayıcıları** yöntemi eşleme. Koleksiyonunuz heterojen türdeki veriler içerdiğinde bu örnekleme yöntemini kullanmanızı öneririz. Bu yöntem tooscope hello tooa dizi öznitelikleri ve karşılık gelen değerler örnekleme kullanabilirsiniz. Örneğin, bir belgeyi "Type" özelliği içeriyorsa, bu özelliğin hello örnekleme toohello değerlerini kapsamını belirleyebilirsiniz. Merhaba örnekleme Hello nihai sonucu, belirttiğiniz türü için hello değerlerin her birini için tablo kümesini olacaktır. Örneğin, yazın = araba araba tablosu türü işlenirken oluşturacak = düzlemi bir düz tablo oluşturmak.

1. Adım 1-4'te tamamladıktan sonra [Bağlan tooyour Azure Cosmos DB veritabanı](#connect), tıklatın **şema Düzenleyicisi** hello Azure Cosmos DB ODBC sürücüsü DSN Kurulumu penceresinde.
2. Merhaba, **şema Düzenleyicisi** penceresinde tıklatın **Yeni Oluştur**.
    Merhaba **oluşturmak şema** penceresinde hello Azure Cosmos DB hesabı tüm hello koleksiyonları görüntüler. 
3. Merhaba üzerinde bir koleksiyon seçin **Sample View** sekmede hello **eşleme tanımı** sütunu hello koleksiyon için tıklatın **Düzenle**. Merhaba sonra **eşleme tanımı** penceresinde, seçin **tablo sınırlayıcıları** yöntemi. Ardından aşağıdaki hello:

    a. Merhaba, **öznitelikleri** kutusu, bir sınırlayıcı özelliğinin türü hello adı. Bu örneği için istediğiniz tooscope hello örnekleme için belgeyi Şehir özelliğinde ve ENTER tuşuna basın. 

    b. Girdiğiniz hello özniteliği için yalnızca tooscope hello örnekleme toocertain değerlerini istiyorsanız hello özniteliği hello seçim kutusunu seçin ve ardından hello bir değer girin **değeri** kutusu, örneğin, Seattle ve ENTER tuşuna basın. Öznitelikler için birden çok değer tooadd devam edebilirsiniz. Yalnızca bu hello öznitelik değerleri girerken seçili doğru emin olun.

    Örneğin, dahil ederseniz bir **öznitelikleri** Şehir ve değerini istediğiniz toolimit tablo tooonly New York ve Dubai bir şehir değerle satır içerir, şehir hello öznitelikler kutusu ve New York sonra Dubai hello girersiniz **Değerleri** kutusu.
4. **Tamam** düğmesine tıklayın. 
5. Merhaba eşleme tanımlarını hello koleksiyonlar için tamamladıktan sonra hello içinde toosample istediğiniz **şema Düzenleyicisi** penceresinde tıklatın **örnek**.
     Her sütun için değiştirebileceğiniz hello sütun SQL adı, hello SQL türü SQL uzunluğu (varsa), Ölçek (varsa), duyarlık (varsa) ve null atanabilir.
    - Ayarlayabileceğiniz **sütunu gizle** çok**doğru** , sorgu sonuçları sütundan tooexclude istiyorsanız. Sütunları gizleme sütun işaretli = true hala hello şema bir parçası olsa seçimi ve yansıtma, döndürülmez. Örneğin, "_" ile başlayan tüm hello Azure Cosmos DB gerekli sistem özellikleri gizleyebilirsiniz.
    - Merhaba **kimliği** hello normalleştirilmiş şemasında hello birincil anahtarı olarak kullanılan gizlenemez hello yalnızca alan bir sütundur. 
6. Merhaba şemasını tanımlama tamamladıktan sonra tıklatın **dosya** | **kaydetmek**toohello directory toosave hello şeması gidin ve ardından **kaydetmek**.
7. Merhaba edilene **Azure Cosmos DB ODBC sürücüsü DSN Kurulum** penceresinde tıklatın ** Gelişmiş Seçenekleri **. Ardından hello **şema dosyası** kutusuna kaydedilmiş toohello şema dosyası gidin ve tıklatın **Tamam**. Tıklatın **Tamam** yeniden toosave hello DSN. Bu kaydeder hello şema toohello DSN oluşturuldu. 

## <a name="optional-creating-views"></a>(İsteğe bağlı) Görünümler oluşturma
Tanımlayın ve görünümler hello örnekleme işleminin bir parçası oluşturun. Bu görünümler eşdeğer tooSQL görünümlerdir. Bunlar salt okunurdur ve kapsam hello seçimleri ve Azure Cosmos DB SQL tanımlanan hello yansıtmaların. 

toocreate Merhaba, verileriniz için bir görünüm **şema Düzenleyicisi** penceresinde hello **görünüm tanımları** sütun, tıklatın **Ekle** hello koleksiyonu toosample hello satırının üzerinde. Merhaba sonra **görünüm tanımları** penceresinde, aşağıdaki hello:
1. Tıklatın **yeni**, hello görünümü, örneğin, EmployeesfromSeattleView için bir ad girin ve ardından **Tamam**.
2. Merhaba, **düzenleme görünümü** penceresinde, bir Azure Cosmos DB sorgusu girin. Bu Azure Cosmos DB SQL sorgusu, örneğin olmalıdır`SELECT c.City, c.EmployeeName, c.Level, c.Age, c.Gender, c.Manager FROM c WHERE c.City = “Seattle”`ve ardından **Tamam**.

Dilediğiniz gibi birçok görünümler oluşturabilirsiniz. Tanımlama hello görünümleri tamamladıktan sonra ardından hello veri örnek oluşturabilirsiniz. 

## <a name="step-5-view-your-data-in-bi-tools-such-as-power-bi-desktop"></a>5. adım: verilerinizi Power BI Desktop gibi BI araçları görüntülemek

Bu adım yalnızca, nasıl gösterir, yeni DSN tooconnect DocumentADB herhangi ODBC uyumlu bir aracı ile - kullanabilirsiniz tooconnect tooPower BI Desktop ve Power BI görselleştirme oluşturun.

1. Power BI Desktop açın.
2. Tıklatın **veri alma**.
3. Merhaba, **Veri Al** penceresinde tıklatın **diğer** | **ODBC** | **Bağlan**.
4. Merhaba, **gelen ODBC** penceresinde, oluşturduğunuz ve ardından select hello veri kaynağı adı **Tamam**. Merhaba bırakabilirsiniz **Gelişmiş Seçenekler** girişleri boş.
5. Merhaba, **ODBC sürücüsü kullanarak bir veri kaynağına erişim** penceresinde, seçin **varsayılan veya özel** ve ardından **Bağlan**. Tooinclude hello gerekmez **kimlik bilgisi bağlantı dizesi özellikleri**.
6. Merhaba, **Gezgini** hello veritabanı, hello şema ve ardından hello Tablo penceresinde hello sol bölmede, genişletin. Merhaba sonuçlar bölmesinde, oluşturduğunuz hello Şeması'nı kullanarak hello verileri içerir.
7. Power BI Desktop'ta toovisualize hello veri hello tablo adı önünde hello kutuyu işaretleyin ve ardından **yük**.
8. Power BI Desktop'ta kadar sol hello üzerinde hello veri sekmesini seçin. ![Power BI Desktop'ta veri sekmesi](./media/odbc-driver/odbc-driver-data-tab.png) tooconfirm verilerinizi içeri aktarıldı.
9. Artık hello rapor sekmesinde tıklayarak Power BI kullanan görseller oluşturabilirsiniz ![Power BI Desktop rapor sekmesinde](./media/odbc-driver/odbc-driver-report-tab.png)a **yeni Visual**ve ardından kutucuğunuzun özelleştirme. Power BI Desktop'ta görselleştirmeleri oluşturma hakkında daha fazla bilgi için bkz: [görselleştirme türlerinin Power bı'da](https://powerbi.microsoft.com/documentation/powerbi-service-visualization-types-for-reports-and-q-and-a/).

## <a name="troubleshooting"></a>Sorun giderme

Hello aşağıdaki hata alırsanız, hello olun **konak** ve **erişim tuşu** kopyaladığınız değerleri hello Azure portalında [2. adım](#connect) doğru olduğunu onaylayın ve ardından yeniden deneyin. Merhaba kopyalama düğmeleri toohello hello sağında kullanmak **konak** ve **erişim tuşu** hello Azure portal toocopy hello değerleri hata boş değerler.

    [HY000]: [Microsoft][Azure Cosmos DB] (401) HTTP 401 Authentication Error: {"code":"Unauthorized","message":"hello input authorization token can't serve hello request. Please check that hello expected payload is built as per hello protocol, and check hello key being used. Server used hello following payload toosign: 'get\ndbs\n\nfri, 20 jan 2017 03:43:55 gmt\n\n'\r\nActivityId: 9acb3c0d-cb31-4b78-ac0a-413c8d33e373"}`

## <a name="next-steps"></a>Sonraki adımlar

toolearn Azure Cosmos DB hakkında daha fazla bilgi görmek [Azure Cosmos DB nedir?](introduction.md).
