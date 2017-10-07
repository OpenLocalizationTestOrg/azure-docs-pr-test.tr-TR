---
title: "Azure Cosmos DB bağlayıcı için aaaPower BI Öğreticisi | Microsoft Docs"
description: "Bu Power BI öğretici tooimport JSON kullanın, ayrıntılı raporları oluşturmak ve hello Azure Cosmos DB ve Power BI Bağlayıcısı'nı kullanarak verileri Görselleştir"
keywords: "power BI öğretici, verileri, power BI Bağlayıcısı görselleştirin"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: cd1b7f70-ef99-40b7-ab1c-f5f3e97641f7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: mimig
ms.openlocfilehash: ca0bb8b76db8ef2ec936722b682af6a9488a3501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="power-bi-tutorial-for-azure-cosmos-db-visualize-data-using-hello-power-bi-connector"></a>Azure Cosmos DB için Power BI Öğreticisi: hello Power BI Bağlayıcısı'nı kullanarak verileri Görselleştir
[Powerbı.com adresinde](https://powerbi.microsoft.com/) nerede oluşturmak ve paylaşmak için kullanabileceğiniz panolar ve raporlar önemli tooyou ve kuruluşunuz verilerle çevrimiçi bir hizmettir.  Power BI Desktop, ayrılmış bir tooretrieve verileri çeşitli veri kaynaklarından rapor yazma sağlar aracı, birleştirme ve hello veri dönüştürme, güçlü raporları ve görselleştirmeleri oluşturma ve yayımlama hello raporları tooPower BI ' dir.  Merhaba en son sürümüyle Power BI Desktop, hello Cosmos DB bağlayıcısı aracılığıyla tooyour Cosmos DB hesap için Power BI şimdi bağlanabilir.   

Bu Power BI öğreticideki biz hello adımları tooconnect tooa Power BI Desktop Cosmos DB hesabında yol, hello Gezgini, Power BI Desktop sorgu kullanarak tablo biçime dönüştürme JSON verilerini kullanarak tooextract hello verileri nerede istiyoruz tooa koleksiyonu gidin Düzenleyici, yapı ve rapor tooPowerBI.com yayımlayın.

Bu Power BI öğreticiyi tamamladıktan sonra aşağıdaki soruları mümkün tooanswer hello olması:  

* Nasıl ı veri raporlarla Cosmos DB'den Power BI Desktop kullanarak oluşturabilir miyim?
* Power BI Desktop tooa Cosmos DB hesabında nasıl bağlanabilir miyim?
* Nasıl Power BI Desktop'ta koleksiyonundan ı verileri alabilir?
* İç içe geçmiş JSON verilerini Power BI Desktop'ta nasıl dönüştürme?
* Nasıl yayımlama ve paylaşma raporlarım powerbı.com'da?

> [!NOTE]
> Merhaba Power BI Bağlayıcısı Azure Cosmos DB için ayıklama ve veri dönüştürme için BI Desktop tooPower bağlanır. Power BI Desktop'ta oluşturulan raporlar sonra yayımlanan tooPowerBI.com olabilir. Powerbi.com'u doğrudan ayıklama ve Azure Cosmos DB veri dönüştürme gerçekleştirilemiyor. 

## <a name="prerequisites"></a>Ön koşullar
Bu Power BI öğreticide Hello yönergeleri izlemeden önce aşağıdaki kaynaklara erişim toohello sahip olduğundan emin olun:

* [Power BI Desktop en son sürümünü Hello](https://powerbi.microsoft.com/desktop).
* Erişim tooour demo hesabı veya Cosmos DB hesabınızdaki veriler.
  * Merhaba demo hesabını, bu öğreticide gösterilen hello volcano verilerle doldurulur. Bu demo hesap tarafından herhangi bir SLA bağlı değil ve yalnızca tanıtım amacıyla tasarlanmıştır.  Merhaba sağ toomake değişiklikleri toothis demo hesabı dahil yedek ancak bunlarla sınırlı olmamak kaydıyla, hesabı, değiştirme, erişimini hello anahtarının değiştirilmesi hello sonlandırıp önceden veya neden olmadan herhangi bir zamanda hello verilerini sil.
    * URL: https://analytics.documents.azure.com
    * Salt okunur anahtar: MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR + YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw ==
  * Veya, toocreate kendi hesabınızı bkz [hello Azure portal kullanarak bir Azure Cosmos DB veritabanı hesabı oluşturma](https://azure.microsoft.com/documentation/articles/create-account/). Ardından, benzer toowhat's tooget örnek volcano verileri Bu öğreticide kullanılan (ancak hello GeoJSON blokları içermiyor), hello bkz [NOAA site](https://www.ngdc.noaa.gov/nndc/struts/form?t=102557&s=5&d=5) ve hello kullanarak hello veri içeri aktarma [Azure Cosmos DB veri geçişi Aracı](import-data.md).

tooshare raporlarınızı Powerbi.com'u, Powerbi.com'u bir hesabınızın olması gerekir.  Ücretsiz ve Power BI Pro için Power BI hakkında daha fazla toolearn ziyaret [https://powerbi.microsoft.com/pricing](https://powerbi.microsoft.com/pricing).

## <a name="lets-get-started"></a>Başlayalım
Bu öğreticide, şimdi Merhaba Dünya volkanlar kavramlarını geologist olduğunuzu varsayalım.  Merhaba volcano veri Cosmos DB hesabında depolanır ve örnek bir belge aşağıdaki hello gibi hello JSON belgelerini arayın.

    {
        "Volcano Name": "Rainier",
           "Country": "United States",
          "Region": "US-Washington",
          "Location": {
            "type": "Point",
            "coordinates": [
              -121.758,
              46.87
            ]
          },
          "Elevation": 4392,
          "Type": "Stratovolcano",
          "Status": "Dendrochronology",
          "Last Known Eruption": "Last known eruption from 1800-1899, inclusive"
    }

Merhaba Cosmos DB tooretrieve hello volcano verileri hesap ve etkileşimli bir Power BI raporu rapor aşağıdaki hello gibi verileri görselleştirmek istediğiniz.

![Bu Power BI öğretici hello Power BI Bağlayıcısı ile tamamlayarak hello Power BI Desktop volcano rapor mümkün toovisualize verilerle olacaktır](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

Hazır toogive deneyin bir BT? Haydi başlayalım.

1. Power BI Desktop iş istasyonunuza çalıştırın.
2. Power BI Desktop başlatıldıktan sonra bir *Hoş Geldiniz* ekranı görüntülenir.
   
    ![Power BI Desktop Hoş Geldiniz ekranı - Power BI Bağlayıcısı](./media/powerbi-visualize/power_bi_connector_welcome.png)
3. Yapabilecekleriniz **Veri Al**, bkz: **son kaynakları**, veya **açık diğer rapor** hello doğrudan *Hoş Geldiniz* ekran.  Merhaba X hello sağ üst köşedeki tooclose Merhaba ekranında'ı tıklatın. Merhaba **rapor** Power BI Desktop görünümü görüntülenir.
   
    ![Power BI Desktop rapor görünümü - Power BI Bağlayıcısı](./media/powerbi-visualize/power_bi_connector_pbireportview.png)
4. Select hello **giriş** Şerit sonra tıklayın **Veri Al**.  Merhaba **Veri Al** penceresi görünmelidir.
5. Tıklayın **Azure**seçin **Microsoft Azure DocumentDB (Beta)**ve ardından **Bağlan**. 

    ![Power BI Desktop, Power BI Bağlayıcısı - veri alma](./media/powerbi-visualize/power_bi_connector_pbigetdata.png)   
6. Merhaba üzerinde **Önizleme bağlayıcı** sayfasında, **devam**. Merhaba **Microsoft Azure DocumentDB Connect** penceresi görüntülenir.
7. Aşağıda gösterildiği gibi tooretrieve hello verilerden ister ve ardından hello Cosmos DB hesap uç noktasının URL'sini belirtin **Tamam**. toouse kendi hesabınızı hello URI URL'den kutusunda hello hello alabilir  **[anahtarları](manage-account.md#keys)**  hello Azure portal dikey. toouse hello gösteri hesabı, girin `https://analytics.documents.azure.com` hello URL. 
   
    Bu alanlar isteğe bağlı olarak hello veritabanı adı, koleksiyon adı ve SQL deyimi boş bırakın.  Bunun yerine, hello veri nereden geldiğini hello Gezgini tooselect hello veritabanı ve koleksiyonu tooidentify kullanacağız.
   
    ![Power BI öğretici Azure Cosmos DB Power BI Bağlayıcısı - masaüstü penceresinde bağlanmak için](./media/powerbi-visualize/power_bi_connector_pbiconnectwindow.png)
8. İlk kez toothis uç noktası hello için bağlanıyorsanız hello hesap anahtarı için istenir. Kendi hesabınızı için hello anahtarı hello alıp **birincil anahtar** hello kutusunda  **[salt okunur anahtarları](manage-account.md#keys)**  hello Azure portal dikey. Hello tanıtımı için başlangıç anahtarı hesabıdır `MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==`. Merhaba uygun anahtarını girin ve ardından **Bağlan**.
   
    Raporları oluştururken hello salt okunur anahtarı kullanmanızı öneririz.  Bu hello ana anahtar toopotential güvenlik riskleri gereksiz riskini engeller. Merhaba salt okunur anahtar hello kullanılabilir [anahtarları](manage-account.md#keys) hello Azure portal veya dikey penceresinde, yukarıda verilen hello demo hesap bilgileri kullanabilirsiniz.
   
    ![Power BI öğretici Azure Cosmos DB Power BI Bağlayıcısı - hesap anahtarı](./media/powerbi-visualize/power_bi_connector_pbidocumentdbkey.png)
    
    > [!NOTE] 
    > Bildiren bir hata alırsanız "Merhaba belirtilen veritabanı bulunamadı." Merhaba geçici çözüm bu adımlarına bakın [Power BI sorunu](https://community.powerbi.com/t5/Issues/Document-DB-Power-BI/idi-p/208200).
    
9. Merhaba hesabı başarıyla bağlandığında hello **Gezgini** görünür.  Merhaba **Gezgini** hello hesabı altında veritabanlarının bir listesini gösterir.
10. ' I tıklatın ve hello veri hello demo hesabını kullanıyorsanız, hello raporu, gelecek için select where hello veritabanını genişletin **volcanodb**.   
11. Şimdi, hello verileri alacak bir koleksiyon seçin. Merhaba demo hesabını kullanıyorsanız, seçin **volcano1**.
    
    Merhaba önizleme bölmesinde listesini gösterir **kaydı** öğeleri.  Bir belge olarak temsil edilen bir **kaydı** Power bı'da türü. Benzer şekilde, bir belge içindeki iç içe geçmiş bir JSON blok da olan bir **kaydı**.
    
    ![Power BI öğretici Azure Cosmos DB Power BI Bağlayıcısı - Gezgini penceresi](./media/powerbi-visualize/power_bi_connector_pbinavigator.png)
12. Tıklatın **Düzenle** toolaunch hello sorgu Düzenleyicisi'ni yeni bir pencere tootransform hello verileri.

## <a name="flattening-and-transforming-json-documents"></a>Düzleştirme ve JSON belgelerini dönüştürme
1. Merhaba burada toohello Power BI sorgu Düzenleyicisi penceresini geçiş **belge** hello orta bölmesinde sütun.
   ![Power BI Desktop sorgu Düzenleyicisi](./media/powerbi-visualize/power_bi_connector_pbiqueryeditor.png)
2. Merhaba genişletici hello hello sağ tarafındaki tıklayın **belge** sütun başlığı.  alanların listesini ile Merhaba bağlam menüsü görüntülenir.  Örneği için rapor için ihtiyacınız hello alanları, Volcano adı, ülke, bölge, konum, yükseltme, türü, durumu ve son bilmeniz patlama ve ardından seçin **Tamam**.
   
    ![Power BI öğretici Azure Cosmos DB Power BI Bağlayıcısı için - belgeleri genişletin](./media/powerbi-visualize/power_bi_connector_pbiqueryeditorexpander.png)
3. Merhaba Orta bölmede seçili hello alanlarla hello sonuç önizlemesini görüntüler.
   
    ![Power BI öğretici Azure Cosmos DB Power BI Bağlayıcısı için - sonuçları düzleştirme](./media/powerbi-visualize/power_bi_connector_pbiresultflatten.png)
4. Bizim örneğimizde, hello konum özelliği, belgedeki bir GeoJSON taşıdır.  Gördüğünüz gibi konumu olarak temsil edilen bir **kaydı** Power BI Desktop'ta türü.  
5. Hello genişletici hello sağ tarafında hello konumu sütun başlığına tıklayın.  tür ve koordinatları alanları ile Merhaba bağlam menüsü görüntülenir.  Şimdi hello koordinatları alan tıklatıp **Tamam**.
   
    ![Power BI öğretici Azure Cosmos DB Power BI Bağlayıcısı - konumu kaydı](./media/powerbi-visualize/power_bi_connector_pbilocationrecord.png)
6. Merhaba bölmeyi şimdi koordinatları sütunu gösterir **listesi** türü.  Başlangıç Öğreticisi Hello başında gösterildiği gibi hello bu öğreticideki GeoJSON veri noktası hello koordinatları dizisinde kaydedilen enlem ve boylam değerlerle türüdür.
   
    [1] koordinatları temsil ederken, enlem hello koordinatları [0] öğesi boylam temsil eder.
    ![Power BI öğretici Azure Cosmos DB Power BI Bağlayıcısı - koordinatları listesi](./media/powerbi-visualize/power_bi_connector_pbiresultflattenlist.png)
7. tooflatten hello dizi koordinatları, oluşturacağız bir **özel sütun** LatLong çağrılır.  Select hello **Sütun Ekle** Şerit ve tıklayın **özel Sütun Ekle**.  Merhaba **özel Sütun Ekle** penceresi görünmelidir.
8. Merhaba yeni sütun, örneğin LatLong için bir ad sağlayın.
9. Ardından, hello özel formül hello yeni bir sütun için belirtin.  Bizim örneğimizde, biz formülü aşağıdaki hello kullanarak aşağıda gösterildiği gibi virgülle ayrılmış hello enlem ve boylam değerlerini birleştirme: `Text.From([coordinates]{1})&","&Text.From([coordinates]{0})`. **Tamam** düğmesine tıklayın.
   
    Üzerinde veri analizi ifadeleri (DAX işlevleri dahil olmak üzere DAX) daha fazla bilgi için lütfen ziyaret [DAX temel Power BI Desktop'ta](https://support.powerbi.com/knowledgebase/articles/554619-dax-basics-in-power-bi-desktop).
   
    ![Power BI öğretici Azure Cosmos DB Power BI Bağlayıcısı - özel sütun eklemek için](./media/powerbi-visualize/power_bi_connector_pbicustomlatlong.png)
10. Şimdi, hello bölmeyi hello hello enlem ile doldurulan yeni LatLong sütun ve virgülle ayrılmış boylam değerleri gösterir.
    
    ![Power BI öğretici Azure Cosmos DB Power BI Bağlayıcısı - özel LatLong sütun için](./media/powerbi-visualize/power_bi_connector_pbicolumnlatlong.png)
    
    Yeni bir sütun hello içinde bir hata alırsanız, sorgu ayarları altında uygulanan hello adımları aşağıdaki şekilde hello eşleştiğinden emin olun:
    
    ![Uygulanan adımlar olması gereken kaynak, gezinti, genişletilmiş belgenin, genişletilmiş Document.Location, eklenen özel](./media/powerbi-visualize/power-bi-applied-steps.png)
    
    Adımlarınızı farklıysa, silme ek adımlar hello ve hello özel sütun yeniden eklemeyi deneyin. 
11. Düzleştirme hello veri artık tablo biçiminde tamamladınız.  Cosmos DB veri dönüştürme ve tüm hello özellikler hello sorgu Düzenleyicisi'ni tooshape kullanılabilir yararlanın.  Merhaba örnek kullanıyorsanız, hello veri türü için yükseltme çok değiştirme**tamsayı** hello değiştirerek **veri türü** hello üzerinde **giriş** Şerit.
    
    ![Power BI öğretici Azure Cosmos DB Power BI Bağlayıcısı - sütun türünü değiştir](./media/powerbi-visualize/power_bi_connector_pbichangetype.png)
12. Tıklatın **kapatın ve geçerli** toosave hello veri modeli.
    
    ![Power BI öğretici Azure Cosmos DB Power BI Bağlayıcısı - Kapat & Uygula](./media/powerbi-visualize/power_bi_connector_pbicloseapply.png)

<a id="build-the-reports"></a>
## <a name="build-hello-reports"></a>Merhaba raporları oluşturma
Power BI Desktop rapor görünümü toovisualize veri raporları oluşturma başlayabileceğiniz ' dir.  Alanları hello bırakarak raporlar oluşturabilirsiniz **rapor** tuvale.

![Power BI Desktop rapor görünümü - Power BI Bağlayıcısı](./media/powerbi-visualize/power_bi_connector_pbireportview2.png)

Hello rapor görünümü, bulduğunuz:

1. Merhaba **alanları** bölmesinde, veri modelleri raporlarınız için kullanabileceğiniz alanlarla listesini burada görürsünüz budur.
2. Merhaba **görselleştirmeleri** bölmesi. Bir raporu, tek bir veya birden çok görselleştirmeleri içerebilir.  Merhaba visual türleri gereksinimlerinizi hello gelen sığdırma çekme **görselleştirmeleri** bölmesi.
3. Merhaba **rapor** tuvale, burada raporunuzun hello görselleri oluşturacaksınız budur.
4. Merhaba **rapor** sayfası. Power BI Desktop'ta birden çok rapor sayfaları ekleyebilirsiniz.

Merhaba aşağıdaki basit bir etkileşimli harita görünümü rapor oluşturma hello temel adımlar gösterilmektedir.

1. Bizim örneğimizde, her volcano hello konumunu gösteren bir harita görünüm oluşturacağız.  Merhaba, **görselleştirmeleri** bölmesinde, hello harita görsel türü hello ekran görüntüsü yukarıdaki vurgulandığı'ı tıklatın.  Merhaba harita görsel türü üzerinde hello boyandığında görmelisiniz **rapor** tuvale.  Merhaba **görselleştirme** bölmesinde özellikleri ilgili toohello harita visual türünü birtakım ayrıca görüntülenmelidir.
2. Şimdi, sürükleyip hello LatLong alan hello **alanları** bölmesinde toohello **konumu** özelliğinde **görselleştirmeleri** bölmesi.
3. Merhaba Volcano ad alanı toohello ardından, sürükleyip **gösterge** özelliği.  
4. Merhaba ayrıcalık alan toohello sonra sürükleyip **boyutu** özelliği.  
5. Merhaba harita balonları her volcano hello hello volcano toohello ayrıcalıkların bağıntı hello Kabarcık boyutunu ile Merhaba konumunu belirten bir dizi gösteren visual görmelisiniz.
6. Temel bir rapor oluşturdunuz.  Daha fazla görselleştirmeleri ekleyerek hello raporu daha fazla özelleştirebilirsiniz.  Örneğimizde, biz Volcano türü dilimleyici toomake hello rapor etkileşimli eklendi.  
   
    ![Merhaba son Power BI Desktop rapor Azure Cosmos DB için hello Power BI öğretici tamamlanmasıyla ekran görüntüsü](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

## <a name="publish-and-share-your-report"></a>Yayımlama ve raporunuzu paylaşma
tooshare raporunuzu Powerbi.com'u bir hesabınızın olması gerekir.

1. Hello Power BI Desktop, üzerinde hello tıklatın **giriş** Şerit.
2. **Yayımla**’ta tıklayın.  Powerbı.com adresinde hesabınız için istendiğinde tooenter hello kullanıcı adı ve parola olacaktır.
3. Merhaba kimlik bilgileri doğrulandıktan sonra seçtiğiniz yayımlanmış tooyour hedef hello rapor eder.
4. Tıklatın **Power bı'da Aç 'PowerBITutorial.pbix'** toosee ve raporunuzda PowerBI.com paylaşın.
   
    ![Yayımlama tooPower BI başarılı! Power bı'da Aç Öğreticisi](./media/powerbi-visualize/power_bi_connector_open_in_powerbi.png)

## <a name="create-a-dashboard-in-powerbicom"></a>Powerbi.com'u bir pano oluşturun
Bir rapor sahip olduğunuza göre işlem Powerbı.com adresinde paylaşmak olanak tanır

Power BI Desktop tooPowerBI.com, rapordan yayımladığınızda, oluşturur bir **rapor** ve **Dataset** PowerBI.com kiracınızda. Örneğin, sonra yayımladığınız adlı bir raporu **PowerBITutorial** tooPowerBI.com, her iki hello PowerBITutorial görürsünüz **raporları** ve **veri kümeleri** üzerinde bölümler Powerbı.com adresinde.

   ![Ekran görüntüsü hello yeni rapor ve veri kümesi powerbı.com'da](./media/powerbi-visualize/powerbi-reports-datasets.png)

toocreate paylaşılabilen bir Pano tıklatın hello **PIN Canlı sayfa** PowerBI.com raporunuzu düğmesinde.

   ![Ekran görüntüsü hello yeni rapor ve veri kümesi powerbı.com'da](./media/powerbi-visualize/power-bi-pin-live-tile.png)

Merhaba yönergeleri izleyin [bir raporundan bir kutucuğu sabitleyin](https://powerbi.microsoft.com/documentation/powerbi-service-pin-a-tile-to-a-dashboard-from-a-report/#pin-a-tile-from-a-report) toocreate yeni bir Pano. 

Bir Pano oluşturmadan önce geçici değişiklikler tooreport da yapabilirsiniz. Ancak, Power BI Desktop tooperform hello değişiklikler kullanın ve hello rapor tooPowerBI.com yeniden yayımlamanız önerilir.

## <a name="refresh-data-in-powerbicom"></a>Powerbı.com'da veri yenileme
Toorefresh veri, geçici ve zamanlanmış iki yolu vardır.

Geçici bir yenileme için hello eclipses (...) tarafından hello tıklamanız yeterlidir **Dataset**, örneğin PowerBITutorial. Dahil olmak üzere eylemlerin bir listesini görmelisiniz **Şimdi Yenile**. Tıklatın **Şimdi Yenile** toorefresh hello veri.

![Şimdi powerbı.com'da yenileme ekran görüntüsü](./media/powerbi-visualize/power-bi-refresh-now.png)

İçin zamanlanan yenileme, aşağıdaki hello.

1. Tıklatın **Yenileme zamanlaması** hello eylem listesinde. 

    ![Merhaba Yenileme zamanlaması powerbı.com'da ekran görüntüsü](./media/powerbi-visualize/power-bi-schedule-refresh.png)
2. Merhaba, **ayarları** sayfasında **veri kaynağı kimlik bilgileri**. 
3. Tıklayın **kimlik bilgilerini Düzenle**. 
   
    Merhaba yapılandırma açılan görüntülenir. 
4. Bu veri kümesi için Hello anahtar tooconnect toohello Cosmos DB hesabı girin ve ardından **oturum**. 
5. Genişletme **Yenileme zamanlaması** ve hello zamanlama ayarlamak toorefresh hello dataset istiyor. 
6. Tıklatın **Uygula** ve tamamladığınızda hello zamanlanmış yenilemeyi ayarlama.

## <a name="next-steps"></a>Sonraki adımlar
* Power BI hakkında daha fazla toolearn bkz [Power BI ile çalışmaya başlama](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/).
* toolearn Cosmos DB hakkında daha fazla bilgi görmek hello [Azure Cosmos DB belge giriş sayfasının](https://azure.microsoft.com/documentation/services/documentdb/).

