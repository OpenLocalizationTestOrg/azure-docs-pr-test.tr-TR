---
title: "Machine Learning için R dilde aaaQuickstart Öğreticisi | Microsoft Docs"
description: "Merhaba R dil Azure Machine Learning Studio toocreate tahmin çözümü hızlı bir şekilde kullanmaya öğretici tooget programlama bu R kullanın."
keywords: "Hızlı Başlangıç, r dil, r programlama dili, r programlama Öğreticisi"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 99a3a0fd-b359-481a-b236-66868deccd96
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9995f8728f4d7bf9a5c15412015e4cf769cdac96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-tutorial-for-hello-r-programming-language-for-azure-machine-learning"></a>Azure Machine Learning için hello R programlama dili için hızlı başlangıç Öğreticisi

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a>Giriş
Bu hızlı başlangıç Öğreticisi, Azure Machine Learning hello R programlama dilini kullanarak genişletme hızla başlamanıza yardımcı olur. Eğitmen toocreate programlama bu R izleyin, test ve Azure Machine Learning içinde R kodunu yürütün. Öğreticide çalışırken, Azure Machine Learning ile Merhaba R dilini kullanarak eksiksiz bir tahmin çözüm oluşturur.  

Microsoft Azure Machine Learning'de pek çok güçlü machine learning ve veri işleme modüller içerir. Merhaba güçlü R dil hello en yaygın kullanılan analytics, açıklanan. R kullanarak Azure Machine Learning analizi ve veri işleme sonsuza dek, Genişletilebilir Bu birleşimi hello ölçeklenebilirlik ve Azure Machine Learning dağıtımını kolaylığı hello esneklik ve r, derin analizi sağlar

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-hello-dataset"></a>Tahmin ve hello veri kümesi
Tahmin yaygın olarak kullanılan ve oldukça kullanışlıdır analitik yöntemidir. Genel en iyi stok düzeylerini, toopredicting macroeconomic değişkenleri belirleme Mevsimlik öğelerinin satış tahmin etmeye gelen aralığını kullanır. Tahmin genellikle zaman serisi modelleri ile yapılır.

Zaman serisi veri hello değerleri bir zaman dizine sahip verilerdir. Örneğin, her ay ya da her dakika Hello süre dizininin normal, olabilir veya düzensiz. Zaman serisi modeli zaman serisi verilerine dayalıdır. Merhaba R programlama dili esnek framework ve kapsamlı analizi için zaman serisi veri içerir.

Bu Hızlı Başlangıç Kılavuzu'nda biz California Süt ürün çalışma ve veri fiyatlandırma. Bu veriler hello üretim birkaç Süt ürünlerin ve hello fiyat sütlü FAT, kıyaslama Emtia aylık bilgi içerir.

Bu makalede, R betiklerini birlikte kullanılan hello veriler [burada indirilen][download]. Bu veriler başlangıçta hello University Wisconsin http://future.aae.wisc.edu/tab/production.html konumunda bulunan bilgilerden oluşturulan.

### <a name="organization"></a>Kuruluş
Nasıl toocreate, test ve hello Azure Machine Learning ortamında analizi ve veri işleme R kod yürütmek öğrenirken size çeşitli adımlarda ilerleyeceğini.  

* İlk biz hello temelleri hello Azure Machine Learning Studio ortamında hello R dilini kullanarak inceleyeceksiniz.
* Ardından biz toodiscussing çeşitli yönlerini g/ç için veri, R kodu ve grafik hello Azure Machine Learning ortamında ilerleme.
* Biz ardından tahmin çözümümüzdür hello ilk bölümü veri temizleme ve dönüştürme için kod oluşturarak oluşturmak.
* Hazırlanan bizim verilerle birkaç veri kümemizde hello değişkenlerin arasındaki hello bağıntıları analizini gerçekleştiririz.
* Son olarak, sütlü üretim için Mevsimlik zaman serisi tahmin modeli oluşturacağız.

## <a id="mlstudio"></a>Machine Learning Studio'da R dil ile etkileşim
Bu bölümde bazı temelleri hello R programlama dili hello Machine Learning Studio ortamında etkileşimde alır. Merhaba R dil bir güçlü bir araç özelleştirilmiş toocreate analizi ve veri işleme modülleri hello Azure Machine Learning ortamında sağlar.

Küçük ölçekte Rstudio'dan toodevelop, test ve hata ayıklama R kodunu kullanır. Bu kodu ardından kesme ve yapıştırma içine bir [R betiği yürütün] [ execute-r-script] Machine Learning Studio hazır toorun modülünde.  

### <a name="hello-execute-r-script-module"></a>Merhaba R betiği yürütün Modülü
Machine Learning Studio'da R betiklerini hello içinde çalıştırılan [R betiği yürütün] [ execute-r-script] modülü. Merhaba örneği [R betiği yürütün] [ execute-r-script] Machine Learning Studio'da modülü, Şekil 1'de gösterilir.

 ![Programlama dili R: Machine Learning Studio'da seçili hello R betiği yürütün Modülü][1]

*Şekil 1 '. Seçili hello R betiği yürütün modülü gösteren hello Machine Learning Studio ortamı.*

TooFigure 1 başvuran, bazı parçalarının hello anahtar hello ile çalışmak için hello Machine Learning Studio ortamı bakalım [R betiği yürütün] [ execute-r-script] modülü.

* Merhaba deneme Hello modülleri hello merkezi bölmesinde gösterilir.
* Merhaba sağ bölmede üst kısmındaki Hello penceresi tooview içerir ve R komut dosyalarınızı düzenleyin.  
* sağ bölmede alt kısmı Hello gösterir hello bazı özellikleri [R betiği yürütün][execute-r-script]. Merhaba üzerindeki bu bölmesinin uygun noktaları tıklayarak hello hata ve Çıktı günlükleri görüntüleyebilirsiniz.

Biz doğal olarak, hello ele [R betiği yürütün] [ execute-r-script] hello kalan bu belgenin daha ayrıntılı.

Karmaşık R işlevleri ile çalışırken, t, düzenleme, test ve Rstudio'dan içinde hata ayıklama öneririz. Tüm yazılım geliştirme olduğu gibi kodunuzu artımlı olarak genişletmek ve küçük basit test çalışmalarını test. Ardından kesip işlevlerinizi hello R betiği penceresine hello [R betiği yürütün] [ execute-r-script] modülü. Bu yaklaşım, tooharness Rstudio'dan tümleşik geliştirme ortamı (IDE) hello hem Azure Machine Learning gücünü hello sağlar.  

#### <a name="execute-r-code"></a>R kodu yürütme
Merhaba bir R kodda [R betiği yürütün] [ execute-r-script] modülü üzerinde hello tıklayarak hello deneme çalıştırdığınızda, yürütülecek **çalıştırmak** düğmesi. Yürütme tamamlandığında, bir onay işareti hello üzerinde görünür [R betiği yürütün] [ execute-r-script] simgesi.

#### <a name="defensive-r-coding-for-azure-machine-learning"></a>Azure Machine Learning için savunma R kodlama
Azure Machine Learning kullanarak R kodu söyleyin, bir web hizmeti için geliştiriyorsanız, kesinlikle kodunuzu beklenmeyen veri giriş ve özel durumları nasıl ilgilenecektir planlamanız gerekir. toomaintain netlik ı çok hello denetleme veya özel durum işleme gösterilen hello kod örnekleri çoğunda eklemediniz. İlerlemeden gibi ancak ı size çeşitli işlevleri örnekleri R'ın özel durum işleme yeteneği kullanarak sunar.  

Daha eksiksiz bir R özel durum işleme işlenmesi gerekiyorsa, ı hello defteri listelenen Wickham tarafından hello uygun bölümleri okumanız önerilir [ek B - daha fazla bilgi](#appendixb).

#### <a name="debug-and-test-r-in-machine-learning-studio"></a>Hata ayıklama ve Machine Learning Studio'da R test
tooreiterate, test ve küçük ölçekte Rstudio'dan içinde R kodunuzdaki hataları ayıklamanıza öneririz. Ancak, burada gerekir hello R kodu sorunlarını aşağı tootrack durumlar vardır [R betiği yürütün] [ execute-r-script] kendisi. Buna ek olarak, iyi bir uygulama toocheck sonuçlarınızda olan Machine Learning Studio.

Merhaba yürütme R kodunuzu ve hello Azure Machine Learning platformunda çıktısını öncelikle içeren içinde bulunur. Bazı ek bilgiler error.log görülür.  

Machine Learning Studio'da R kodunuzu çalıştırılırken bir hata meydana gelirse, eylem, ilk seyri toolook error.log adresindeki olmalıdır. Bu dosya anlamak ve, hatayı düzeltmek yararlı hata iletileri toohelp içerebilir. tooview error.log, tıklatıldığında **hata günlüğü görüntüle** hello üzerinde **Özellikler bölmesinde** hello için [R betiği yürütün] [ execute-r-script] hello hata içeren.

Örneğin, içinde tanımlanmamış bir değişken y R kodu aşağıdaki hello çalıştırdım bir [R betiği yürütün] [ execute-r-script] Modülü:

    x <- 1.0
    z <- x + y

Bu kodu bir hata koşulu kaynaklanan tooexecute başarısız olur. Tıklayarak **hata günlüğü görüntüle** hello üzerinde **Özellikler bölmesinde** üretir hello Şekil 2'de gösterilen görüntüleme.

  ![Hata iletisi açılır][2]

*Şekil 2 '. Hata iletisi açılır.*

Toolook içeren toosee hello R hata iletisindeki ihtiyacımız gibi görünüyor. Hello üzerinde tıklatın [R betiği yürütün] [ execute-r-script] ve üzerinde hello ardından **içeren görüntülemek** hello öğede **Özellikler bölmesinde** toohello sağ. Yeni bir tarayıcı penceresi açar ve hello aşağıdakilere bakın.

    [Critical]     Error: Error 0063: hello following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

Bu hata iletisi yok beklenmeyen durumları içerir ve açıkça hello sorun tanımlar.

R herhangi bir nesne tooinspect hello değeri, bu değerler toohello içeren dosyası yazdırabilirsiniz. temelde değerlerdir nesne incelenmesinin hello kuralları aynı etkileşimli bir R oturumu olduğu gibi hello. Örneğin, bir satıra bir değişken adı yazın, hello nesnesinin başlangıç değeri yazdırılan toohello içeren dosya olacaktır.  

#### <a name="packages-in-machine-learning-studio"></a>Machine Learning Studio'da paketleri
Azure Machine Learning 350'den önceden yüklenmiş R dil paketleriyle birlikte gelir. Merhaba kodda aşağıdaki hello kullanabilirsiniz [R betiği yürütün] [ execute-r-script] modülü tooretrieve hello listesini önceden yüklenen paketler.

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

Merhaba şu anda bu kodu son satırının hello anlamadığınız okumaya devam edin. Bu belgenin Hello kalan yaygın hello Azure Machine Learning ortamda R kullanarak aşağıdakiler ele alınacaktır.

### <a name="introduction-toorstudio"></a>Giriş tooRStudio
R için yaygın olarak kullanılan bir IDE Rstudio'dan olduğu Rstudio'dan düzenleme, test ve bu Hızlı Başlangıç Kılavuzu'nda kullanılan hello R kodu bazıları hata ayıklama için kullanır. R kodu test edilmiş ve hazır olduğunda size kesip hello Rstudio'dan Düzenleyicisi'nden bir Machine Learning Studio'ya [R betiği yürütün] [ execute-r-script] modülü.  

Masaüstü makinenize yüklü hello R programlama dili yoksa, bunu şimdi yapın ı öneririz. Açık kaynak R dilinin ücretsiz indirme hello kapsamlı R arşiv ağ (CRAN) kullanılabilir en [http://www.r-project.org/](http://www.r-project.org/). Windows, Mac OS ve Linux/UNIX için kullanılabilir yüklemeler vardır. Yakındaki bir yansıtma seçin ve hello yükleme yönergeleri izleyin. Ayrıca, CRAN bol miktarda yararlı analizi ve veri işleme paketleri içerir.

Yeni tooRStudio varsa, indirin ve hello Masaüstü sürümünü yükleyin. Rstudio'dan http://www.rstudio.com/products/RStudio/ Windows, Mac OS ve Linux/UNIX indirmeleri hello bulabilirsiniz. Masaüstü makinenizde tooinstall Rstudio'dan sağlanan hello yönergeleri izleyin.  

Eğitmen giriş tooRStudio https://support.rstudio.com/hc/sections/200107586-Using-RStudio kullanılabilir.

I içinde Rstudio'dan kullanarak bazı ek bilgiler sağlayan [ek A][appendixa].  

## <a id="scriptmodule"></a>Merhaba R betiği yürütün modülü ve dışındaki veri al
Bu bölümde içine ve dışına hello veri nereden aşağıdakiler ele alınacaktır [R betiği yürütün] [ execute-r-script] modülü. Biz içine ve dışına hello toohandle çeşitli veri türlerini nasıl okuma incelenecek [R betiği yürütün] [ execute-r-script] modülü.

Merhaba tam bu bölümde daha önce indirdiğiniz hello zip dosyasında kodudur.

### <a name="load-and-check-data-in-machine-learning-studio"></a>Yük ve veri Machine Learning Studio'da denetleyin
#### <a id="loading"></a>Yük hello veri kümesi
Biz hello yükleyerek başlayacak **csdairydata.csv** Azure Machine Learning Studio dosyasına.

* Azure Machine Learning Studio ortamınızı başlatın.
* Tıklayın **+ yeni** hello seçin ve ekranın sol alt **Dataset**.
* Seçin **yerel dosyadan**ve ardından **Gözat** tooselect hello dosya.
* Seçtiğiniz emin olun **genel CSV dosyası (.csv) üstbilgiyle** hello veri kümesi için hello türü.
* Merhaba onay işaretine tıklayın.
* Merhaba dataset karşıya yüklendikten sonra hello üzerinde tıklayarak hello yeni veri kümesi görmelisiniz **veri kümeleri** sekmesi.  

#### <a name="create-an-experiment"></a>Bir deneme oluşturma
Machine Learning Studio'da sahip olduğumuz bazı verileri, toocreate deneme toodo hello analiz ihtiyacımız var.  

* Tıklayın **+ yeni** hello sol alt ve seçin **deneme**, ardından **boş deneme**.
* Seçerek denemenizi adlandırın ve değiştirme hello **deneme oluşturulan...**  hello sayfanın üst kısmındaki hello başlığı. Örneğin, çok değiştirme**CA günlük analizi**.
* Merhaba deneme sayfa Hello solda genişletin **kaydedilen veri kümeleri**ve ardından **My veri kümeleri**. Merhaba görmelisiniz **cadairydata.csv** daha önce yüklediğiniz.
* Sürükle ve bırak hello **csdairydata.csv dataset** hello deneme üzerine.
* Merhaba, **arama öğeleri denemeler** hello sol bölmede, türü hello üstündeki kutusunu [R betiği yürütün][execute-r-script]. Merhaba arama listede hello modülü görürsünüz.
* Sürükle ve bırak hello [R betiği yürütün] [ execute-r-script] , palet modülü.  
* Merhaba Hello çıkışına bağlayın **csdairydata.csv dataset** toohello soldaki giriş (**Dataset1**) Merhaba, [R betiği yürütün][execute-r-script].
* **'Kaydet' üzerinde tooclick unutmayın!**  

Bu noktada denemenizi Şekil 3 gibi görünmelidir.

![Merhaba CA günlük analizi denemeler veri kümesi ve R betiği yürütün Modülü][3]

*Şekil 3 '. Merhaba CA günlük analizi veri kümesi ve R betiği yürütün modülü ile deneyin.*

#### <a name="check-on-hello-data"></a>Merhaba veriyi denetle
Şimdi hello veri bizim deneme yüklemiş olduğunuz bir görünüme sahiptir. Merhaba denemesinde hello hello çıktısını tıklatın **cadairydata.csv dataset** seçip **görselleştirmek**. Şekil 4 gibi bir şey görmeniz gerekir.  

![Merhaba cadairydata.csv dataset özeti][4]

*Şekil 4 '. Merhaba cadairydata.csv dataset özeti.*

Bu görünümde çok sayıda yararlı bilgiler bakın. Görebiliriz bu veri kümesinin ilk birkaç satır hello. Biz bir sütun seçerseniz, hello istatistikleri bölüm hello sütun hakkında daha fazla bilgi gösterir. Örneğin, hello özellik türü satır bize Azure Machine Learning Studio atanmış bir toohello sütun hangi veri türlerini gösterir. Biz toodo herhangi bir önemli iş başlamadan önce bu gibi hızlı bir bakış sahip bir iyi sağlamlık olup olmadığını denetler.

### <a name="first-r-script"></a>İlk R betiği
Bir basit ilk R betiği tooexperiment ile Azure Machine Learning Studio'da oluşturalım. I oluşturduktan ve Rstudio'dan komut dosyası izleyen hello test.  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

Bu komut dosyası tooAzure Machine Learning Studio tootransfer ihtiyacım artık. Yalnızca kesin ve yapıştırın. Ancak, bu durumda, ı my R betiği bir zip dosyası aktarın.

### <a name="data-input-toohello-execute-r-script-module"></a>Veri giriş toohello R betiği yürütün Modülü
Şimdi hello girişleri toohello göz sahip [R betiği yürütün] [ execute-r-script] modülü. Bu örnekte, biz hello California Süt veri hello okuyacaksa [R betiği yürütün] [ execute-r-script] modülü.  

Hello için üç olası girişleri vardır [R betiği yürütün] [ execute-r-script] modülü. Herhangi bir ya da tüm bu girdi, uygulamaya bağlı olarak kullanabilir. Ayrıca, hiçbir giriş hiç alır mükemmel makul toouse bir R komut dosyasıdır.  

Her sol tooright giderek bu girdi bakalım. İmleç hello giriş yerleştirme ve hello araç ipucu okuma her hello girdi hello adlarını görebilirsiniz.  

#### <a name="script-bundle"></a>Komut dosyası paket
Merhaba betik paket giriş toopass Merhaba içeriğine bir zip dosyasına sağlar [R betiği yürütün] [ execute-r-script] modülü. R kodunuza komutları tooread hello hello ZIP dosyasının içeriğini aşağıdaki hello birini kullanabilirsiniz.

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> Azure Machine Learning hello src varsa gibi hello ZIP dosyaları işler / dizini ve bu nedenle, dosya adları bu dizin adı tooprefix gerekir. Örneğin, hello zip hello dosyaları varsa `yourfile.R` ve `yourData.rdata` hello zip hello kökte olarak adresini `src/yourfile.R` ve `src/yourData.rdata` kullanırken `source` ve `load`.
> 
> 

Biz zaten yükleme kümelerinde ele [hello dataset yüklenirken](#loading). Oluşturulan ve hello önceki bölümde gösterilen hello R betiği test sonra aşağıdaki hello:

1. Merhaba R komut dosyasına kaydedin bir. R dosyası. My komut dosyası "simpleplot. çağırın "R". Merhaba içeriği aşağıdadır.
   
        ## Only one of hello following two lines should be used
        ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
        ## If in RStudio, use hello second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## hello following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. Zip dosyası oluşturun ve komut dosyanızı Bu zip dosyasına kopyalayın. Windows hello dosyasını sağ tıklatın ve seçin **göndermek**ve ardından **sıkıştırılmış klasörü**. Bu hello "simpleplot. içeren yeni bir zip dosyası oluşturur R"dosyası.
3. Dosya toohello ekleme **veri kümeleri** hello türü olarak belirterek Machine Learning Studio'daki **zip**. Şimdi, veri kümelerinde hello zip dosyası görmeniz gerekir.
4. Sürükle ve bırak hello zip dosyasından **veri kümeleri** hello üzerine **ML Studio tuvale**.
5. Merhaba Hello çıkışına bağlayın **zip veri** simgesi toohello **betik paket** Merhaba, giriş [R betiği yürütün] [ execute-r-script] modülü.
6. Türü hello `source()` zip dosyası hello kod penceresine için adınızı hello işleviyle [R betiği yürütün] [ execute-r-script] modülü. My durumda yazdım `source("src/simpleplot.R")`.  
7. Tıklattığınız emin olun **kaydetmek**.

Bu adımları tamamlandıktan sonra hello [R betiği yürütün] [ execute-r-script] modülü yürütülecek hello R betiği hello zip dosyasında hello deneme çalıştırdığınızda. Bu noktada denemenizi Şekil 5 gibi görünmelidir.

![Daraltılmış R betiği kullanmayı deneyin][6]

*Şekil 5. Daraltılmış R betiği kullanmayı deneyin.*

#### <a name="dataset1"></a>DataSet1
Merhaba Dataset1 giriş kullanarak verileri tooyour R kodu dikdörtgen tablosu geçirebilirsiniz. Bizim basit bir komut dosyası hello içinde `maml.mapInputPort(1)` işlevi, bağlantı noktası 1 hello verileri okur. Bu verileri daha sonra kodunuzda tooa dataframe değişken adı atanır. Bizim basit komut dosyasında kodun ilk satırı hello hello atama gerçekleştirir.

    cadairydata <- maml.mapInputPort(1)

Merhaba üzerinde tıklayarak denemenizin yürütme **çalıştırmak** düğmesi. Merhaba üzerinde Hello yürütme bittiğinde, bilgisayarınızı [R betiği yürütün] [ execute-r-script] modülü ve ardından **çıkış Günlüğü Görüntüle** hello Özellikler bölmesi. Yeni bir sayfa hello hello içeren dosyanın içeriğini gösteren tarayıcınızda görüntülenmesi gerekir. Aşağı kaydırma yaptığınızda hello aşağıdaki gibi bir şey görmeniz gerekir.

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

Uzağa hello hello aşağıdaki gibi bir şey görünecektir hello sütunlar üzerinde daha ayrıntılı bilgi sayfasıdır.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput]
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput]
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month            : chr  "Jan" "Feb" "Mar" "Apr" ...
    [ModuleOutput]
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput]
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput]
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput]
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...

Bu sonuçları 228 gözlemleri ve hello dataframe 9 sütunlarında beklendiği gibi genellikle olur. Merhaba sütun adları, hello R veri türü ve her sütunun bir örnek görebiliriz.

> [!NOTE]
> Bu aynı çıktılar rahat hello R aygıt çıktısını hello kullanılabilir [R betiği yürütün] [ execute-r-script] modülü. Merhaba hello çıkışları aşağıdakiler ele alınacaktır [R betiği yürütün] [ execute-r-script] hello sonraki bölümde modülü.  
> 
> 

#### <a name="dataset2"></a>Dataset2
Merhaba hello Dataset2 giriş Dataset1, aynı toothat davranıştır. Bu girdi kullanarak R kodunuza ikinci bir dikdörtgen tablo veri geçirebilirsiniz. Merhaba işlevi `maml.mapInputPort(2)`, 2 hello bağımsız değişkeniyle, kullanılan toopass bu verilerdir.  

### <a name="execute-r-script-outputs"></a>R betiği çıkışları yürütme
#### <a name="output-a-dataframe"></a>Bir dataframe çıkış
Hello kullanarak hello sonuç Dataset1 bağlantı noktası üzerinden dikdörtgen tablo olarak bir R dataframe Merhaba içeriğine çıkarabilirsiniz `maml.mapOutputPort()` işlevi. Bizim basit R betiği bu satırı aşağıdaki hello tarafından gerçekleştirilir.

    maml.mapOutputPort('cadairydata')

Çalışan hello deneme sonrasında hello üzerinde sonuç Dataset1 çıkış bağlantı noktasına tıklayın ve tıklayın **Görselleştir**. Şekil 6 gibi bir şey görmeniz gerekir.

![Merhaba görsel olarak hello California Süt veri hello çıktısı][7]

*Şekil 6. Merhaba California Süt veri hello çıktısını Hello görselleştirme.*

Bu çıktı bekliyorduk tam olarak aynı toohello giriş arar.  

### <a name="r-device-output"></a>R cihaz çıktısı
Merhaba aygıt çıktısını hello [R betiği yürütün] [ execute-r-script] modülü iletileri ve grafik çıktısı içerir. Her iki standart çıktı ve standart hata iletilerden R toohello R aygıt çıkış bağlantı noktasına gönderilir.  

tooview hello R çıkışı, cihaz tıklatın hello bağlantı noktası ve ardından **Görselleştir**. Biz hello standart çıktı ve standart hata Şekil 7'de hello R betikten bakın.

![Standart çıktı ve standart hata hello R aygıtı bağlantı noktası][8]

*Şekil 7. Standart çıktı ve standart hata hello R aygıtı bağlantı noktası.*

Bkz: Şekil 8'deki bizim R betiği hello grafik çıktısı biz kaydırma.  

![Grafik çıktısı hello R aygıtı bağlantı noktası][9]

*Şekil 8'de. R aygıtı bağlantı noktası Hello çıktı grafik.*  

## <a id="filtering"></a>Verileri filtreleme ve dönüştürme
Bu bölümde biz bazı temel verileri filtreleme ve hello California Süt veri dönüştürme işlemlerini gerçekleştirir. Bu bölümde Hello ucu tarafından analitik bir model oluşturmak için uygun bir biçim biz veri sahip olur.  

Daha açık belirtmek gerekirse, bu bölümde birkaç ortak veri temizleme ve dönüştürme görevleri gerçekleştiririz: tür dönüştürme, yeni hesaplanan sütunlar ekleme dataframes üzerinde filtreleme ve değer dönüşümler. Bu arka plan gerçek dünyadaki sorunları karşılaştı pek çok Çeşitleme hello ile ilgilenir yardımcı olmalıdır.

Bu bölüm için tam R kod Hello hello zip dosyasında daha önce indirdiğiniz kullanılabilir.

### <a name="type-transformations"></a>Tür dönüştürmeleri
Biz hello hello R koda hello California Süt verileri okuyabilir göre [R betiği yürütün] [ execute-r-script] modül ihtiyacımız hello sütunlardaki hello verileri hedeflenen hello türünü ve biçimini olduğunu tooensure.  

R veri türleri gerektiği gibi bir tooanother gelen yüklenen anlamına gelir dinamik olarak yazılan bir dildir. R Hello atomik veri türü sayısal, mantıksal ve karakter içerir. Merhaba faktörü kullanılan toocompactly deposu kategorik veri türüdür. Merhaba başvurularında veri türleri hakkında daha fazla bilgi bulabilirsiniz [ek B - daha fazla bilgi](#appendixb).

Tablo verisi R bir dış kaynaktan içine okunduğunda her zaman hello sütunları türlerinde kaynaklanan bir fikir toocheck hello gerçekleşir. Bir sütun türü karakterinin isteyebilirsiniz, ancak çoğu durumda bu faktör olarak (veya tersi) görünür. Diğer durumlarda bir sütun olması düşündüğünüz sayısal karakter verileri tarafından örneğin temsil edilir bir kayan olarak 1,23 yerine '1,23' nokta sayısı.  

Neyse ki, eşleme mümkündür sürece kolay tooconvert bir türü tooanother değildir. Örneğin, sayısal bir değer 'Nevada'ya' dönüştürülemiyor ancak tooa faktörü (kategorik değişken) dönüştürebilirsiniz. Başka bir örnek olarak, bir karakter '1' ya da bir faktör sayısal 1 dönüştürebilirsiniz.  

Merhaba diziminin dönüştürmeler basittir: `as.datatype()`. Bu tür dönüştürme işlevleri hello şunları içerir.

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

Merhaba önceki bölümde giriyoruz hello sütunların veri türlerini hello bakarak: türü sayısal, türü karakteri olan'Month ' etiketli hello sütun dışında tüm sütunlar:. Şimdi bu tooa faktörü dönüştürün ve test hello sonuçları.  

Merhaba scatterplot matris oluşturulur ve hello 'Month' sütun tooa faktörü dönüştürme bir satır eklenir hello satır silindi. Denememe t yalnızca hello R kod kesip hello kod penceresine hello [R betiği yürütün] [ execute-r-script] modülü. Ayrıca hello zip dosyasını güncelleştirme ve tooAzure Machine Learning Studio karşıya yükleme, ancak bu çeşitli adımları gerçekleştirir.  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check hello result
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

Şimdi bu kodu yürütür ve hello R betiği için hello çıktı günlüğüne bakın. Şekil 9'Hello ilgili verileri hello günlüğünden gösterilir.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 14 levels "Apr","April",..: 6 5 9 1 11 8 7 3 14 13 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Şekil 9. Merhaba dataframe faktörü değişkeniyle özeti.*

Merhaba türü ay için şimdi söyleyin '**14 düzeyleri içeren faktörü**'. Merhaba yıl içinde yalnızca 12 ay olduğundan bu bir sorundur. Türü hello toosee kontrol edebilirsiniz, **Görselleştir** hello sonuç veri kümesi bağlantı noktası olduğundan '**Categorical**'.

Merhaba, bu sütun sistematik olarak kodlanmış değil'Month ' hello sorunudur. Bazı durumlarda bir ay Nisan adı verilir ve diğerleri Apr kısaltılır. Merhaba dize too3 karakterleri kırpma tarafından size bu sorunu çözebilirsiniz. Merhaba satırlık bir kod artık hello aşağıdaki gibi görünür:

    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

Merhaba deneme yeniden çalıştırın ve hello çıktı günlüğüne bakın. Merhaba, sonuçları Şekil 10'da gösterilen bekleniyordu.  

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Şekil 10. Merhaba dataframe faktörü düzeyleri doğru sayısıyla özeti.*

Bizim faktörü değişkeni istenen hello 12 düzeyleri artık sahiptir.

### <a name="basic-data-frame-filtering"></a>Çerçeve temel verileri filtreleme
R dataframes güçlü filtreleme yetenekleri için destek. Veri kümeleri, satır veya sütun üzerinde mantıksal filtreleri kullanarak alt kümelenmiş olabilir. Çoğu durumda, karmaşık filtre ölçütlerini gerekli olacaktır. Merhaba başvuran [ek B - daha fazla bilgi](#appendixb) dataframes filtreleme kapsamlı örnekleri içerir.  

Bir bit yoktur filtre biz kümemize üzerinde yapmalısınız. Merhaba cadairydata dataframe hello sütunlarında bakarsanız, iki gereksiz sütunları görürsünüz. Merhaba ilk sütun yalnızca çok kullanışlı değil bir satır numarası tutar. Merhaba ikinci sütun, Year.Month, yedek bilgiler içerir. Biz kolayca bu sütunları R koddan hello kullanarak hariç tutabilirsiniz.

> [!NOTE]
> Üzerinde bu bölümde, ı yalnızca gösterecektir artık gelen, ı hello ekleme ek kod hello [R betiği yürütün] [ execute-r-script] modülü. Her yeni satır ekleyeceğim **önce** hello `str()` işlevi. Bu işlev tooverify Azure Machine Learning Studio'da my sonuçları kullanın.
> 
> 

Satır toomy R kodu hello hello eklemek [R betiği yürütün] [ execute-r-script] modülü.

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

Denemenizde bu kodu çalıştırmak ve hello sonucundan hello çıktı günlüğüne bakın. Bu sonuçları Şekil 11'de gösterilmiştir.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  7 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Şekil 11. İki sütun ile Merhaba dataframe özetini kaldırıldı.*

İyi haber! Biz hello beklenen sonuçları alın.

### <a name="add-a-new-column"></a>Yeni bir sütun ekleyin
toocreate zaman serisi modeli içeren bir sütun hello aydan hello zaman serisi hello başlangıcı beri uygun toohave olacaktır. Yeni bir sütun 'Month.Count' oluşturacağız.

toohelp biz bizim ilk basit işlevi oluşturacak hello kod düzenleme `num.month()`. Biz bu işlevi toocreate hello dataframe yeni bir sütunda sonra uygulanır. Merhaba yeni kod aşağıdaki gibidir.

    ## Create a new column with hello month count
    ## Function toofind hello number of months from hello first
    ## month of hello time series
    num.month <- function(Year, Month) {
      ## Find hello starting year
      min.year  <- min(Year)

      ## Compute hello number of months from hello start of hello time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute hello new column for hello dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

Şimdi güncelleştirilmiş hello denemeyi çalıştırın ve hello çıktı günlük tooview hello sonuçları kullanın. Şekil 12'de bu sonuçları gösterilmektedir.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Şekil 12. Merhaba dataframe hello ek sütunla özeti.*

Her şey çalışıyor gibi görünüyor. Bizim dataframe yeni bir sütun hello hello beklenen değerlerle sahibiz.

### <a name="value-transformations"></a>Değer dönüşümler
Bu bölümde biz bizim dataframe hello sütunlarının bazıları hello değerleri bazı basit dönüşümleri gerçekleştirir. Merhaba R dil neredeyse rastgele değeri dönüşümleri destekler. Merhaba başvuran [ek B - daha fazla bilgi](#appendixb) kapsamlı örnekler içeriyor.

Bizim dataframe hello özetlerini hello değerleri bakarsanız tek bir şey burada görmeniz gerekir. Daha fazla dondurma sütlü daha İzmir'de oluşturulur? Bu hiçbir mantıklı gibi Hayır, Kuşkusuz bu olgu olarak üzücü toosome bizi dondurma lovers olmayabilir. Merhaba birimleri farklıdır. Merhaba birimleri BİZE pound, olan 1 M birimlerinde ABD pound, dondurma 1.000 birimlerinde BİZE galon ve cottage Peynir 1.000 ABD pound birimlerinde sütlü fiyatıdır. Dondurma hafiftir galon başına yaklaşık 6.5 pound varsayıldığında, biz kolayca tüm eşit, biriminde 1.000 pound; bu nedenle bu değerleri çarpma tooconvert hello.

Tahmin modelimiz için çarpma modeli eğilim ve bu verileri Mevsimlik düzeltilmesi için kullanırız. Bir günlük dönüştürmesi bize toouse bu işlem basitleştirme doğrusal bir model sağlar. Biz hello günlük aynı hello çarpanı burada uygulanan işlevi hello dönüşümünde uygulayabilirsiniz.

Koddan hello ı yeni bir işlev tanımlayın `log.transform()`ve hello sayısal değerleri içeren toohello satırları uygulayın. Merhaba R `Map()` işlevidir kullanılan tooapply hello `log.transform()` işlevi toohello seçili hello dataframe sütunlarının. `Map()`çok benzer`apply()` ancak bağımsız değişken toohello işlevi birden fazla listesini verir. Not çarpanları listesini hello ikinci bağımsız değişkeni toohello sağlayan `log.transform()` işlevi. Merhaba `na.omit()` işlevi bir bit temizleme tooensure biz eksik yok veya tanımsız değerlerde hello dataframe olarak kullanılır.

    log.transform <- function(invec, multiplier = 1) {
      ## Function for hello transformation, which is hello log
      ## of hello input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments toofunction log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier toofuncition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check hello input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap hello multiplication in tryCatch
      ## If there is an exception, print hello warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply hello transformation function toohello 4 columns
    ## of hello dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

Merhaba içinde oldukça bit oluşmasını yoktur `log.transform()` işlevi. Bu kod çoğu hello bağımsız değişkenleri ile ilgili olası sorunları denetleme veya hala hello hesaplamalar sırasında ortaya çıkabilecek özel durumlarla birlikte ele alma. Bu kod yalnızca birkaç satırlık gerçekte hesaplamalar hello.

Merhaba hello savunma programlama tooprevent hello hata işleme devam etmesini engelleyen tek bir işlevin hedefidir. Uzun süre çalışan çözümleme ani bir başarısızlığını kullanıcılar için oldukça can sıkıcı olabilir. Bu durumda, varsayılan dönüş değerleri seçilmelidir sınırlar tooavoid toodownstream işleme zarar verebilir. Bir ileti ayrıca bir şeyler yanlış geçti üretilen tooalert kullanıcı sayısıdır.

R kullanılan toodefensive programlamada değil varsa, bu kod bir bit bunaltıcı görünebilir. I hello ana adımlarda size yol gösterir:

1. Vektör dört iletilerinin tanımlanır. Bu iletiler, bazı hello olası hatalar ve bu kodu ile oluşan özel durumlar hakkında kullanılan toocommunicate bilgilerdir.
2. I BELİRTİLMEYEN değeri her bir olay döndürür. Daha az yan etkileri olabilir diğer birçok olasılık vardır. Vektör sıfır değerini veya hello özgün giriş vektör, örneğin dönüş.
3. Denetimleri hello bağımsız değişkenleri toohello işlevi üzerinde gerçekleştirilir. Her durumda, bir hata algılandığında, varsayılan bir değer döndürülür ve bir ileti hello tarafından üretilen `warning()` işlevi. Kullanıyorum `warning()` yerine `stop()` hello sonraki yürütme, tam olarak neyi çalışıyorum sonlandıracak gibi tooavoid. I bu kodu bu durumda olduğu gibi bir yordam stili karmaşık ve belirsiz seemed işlevsel bir yaklaşım yazılmış olduğunu unutmayın.
4. Merhaba günlük hesaplamalar sarılır `tryCatch()` böylece özel durumlar ani durdurmak tooprocessing neden olmaz. Olmadan `tryCatch()` hataların çoğu bunu yapan bir durdurma sinyali R işlevleri sonucu olarak gerçekleşti.

Bu R kodu denemenizde yürütün ve hello göz hello içeren dosyasındaki çıktıyı yazdırılan. Şekil 13'te gösterildiği gibi şimdi hello hello dört sütun oturum, dönüştürülmüş hello değerlerini görürsünüz.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Şekil 13. Merhaba özetini hello dataframe değerleri dönüştürüldüğünde.*

Merhaba değerleri dönüştürülen bakın. Şimdi sütlü üretim büyük ölçüde şimdi günlük ölçekte arıyoruz, geri çağırma tüm diğer Süt ürün üretim aşıyor.

Bu noktada verilerimizi temizlenir ve biz bazı modelleme için hazır olursunuz. Sonuç veri kümesini çıktı olarak hello için Özet hello görselleştirme bakarak bizim [R betiği yürütün] [ execute-r-script] modül hello 'Month' sütundur 'Categorical' 12 benzersiz değerlerle yeniden, biz istediği gibi görürsünüz .

## <a id="timeseries"></a>Zaman serisi nesneleri ve bağıntı çözümleme
Bu bölümde biz birkaç temel R zaman serisi nesneleri keşfedin ve bazı hello değişkenler arasındaki hello bağıntıları analiz edin. Amacımız toooutput bir dataframe hello pairwise bağıntı bilgi içeren birkaç gecikmelere adresindeki ' dir.

Merhaba tam R Bu bölümde daha önce indirdiğiniz hello zip dosyasında kodudur.

### <a name="time-series-objects-in-r"></a>R zaman serisi nesneleri
Yukarıda belirtildiği gibi zaman serisinin zaten zamanına göre dizine veri değerleri bir dizi olduğundan. R zaman serisi nesneleri kullanılan toocreate ve hello zaman dizinini yönetme. Birkaç avantaj toousing zaman serisi nesneleri vardır. Zaman serisi nesneleri hello nesnesinde kapsüllenmiş hello zaman serisi dizini değerleri yönetme birçok ayrıntıları hello boş. Ayrıca, zaman serisi nesneler yazdırma, modelleme, vb., toouse hello Çizdirmek, çoğu zaman serisi yöntemleri sağlar.

Merhaba POSIXct zaman serisi sınıfı yaygın olarak kullanılır ve görece daha basittir. Bu zaman serisi sınıf hello hello dönem, 1 Ocak 1970'ten başından süreyi ölçer. Bu örnekte POSIXct zaman serisi nesneleri kullanacağız. Diğer yaygın olarak kullanılan R zaman serisi nesne sınıfları zoo ve xts, Genişletilebilir zaman serisi içerir.
<!-- Additional information on R time series objects is provided in hello references in Section 5.7. [commenting because this section doesn't exist, even in hello original] -->

### <a name="time-series-object-example"></a>Zaman serisi nesnesi örneği
Bizim örneğimizde ile başlayalım. Sürükleme ve bırakma bir **yeni** [R betiği yürütün] [ execute-r-script] denemenizi modüle. Merhaba varolan hello sonuç Dataset1 çıkış bağlantı noktasına bağlanmak [R betiği yürütün] [ execute-r-script] modülü toohello Dataset1 giriş hello yeni bağlantı noktası [R betiği yürütün] [ execute-r-script] modülü.

Merhaba ilk örnekler için yaptığınız gibi biz yapacağınızı gösterir bazı noktalarda hello örnek ilerlemeyi yalnızca hello artımlı ek kod satırı bulunmaktadır R her adımında.  

#### <a name="reading-hello-dataframe"></a>Merhaba dataframe okuma
İlk adım olarak şimdi bir dataframe okuyun ve biz hello beklenen sonuçları elde emin olun. Merhaba aşağıdaki kodu yapmalısınız hello işi.

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check hello results

Şimdi, hello denemeyi çalıştırın. Merhaba günlük hello yeni R betiği yürütün şeklin Şekil 14 gibi görünmelidir.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...

*Şekil 14. Merhaba dataframe hello R betiği yürütün modülünde özeti.*

Bu, beklenen hello türleri ve biçimde verilerdir. Merhaba 'Month' sütun türü faktörü olduğunu ve hello düzey sayısı beklenen sahip unutmayın.

#### <a name="creating-a-time-series-object"></a>Zaman serisi nesnesi oluşturma
Bir zaman serisi nesne tooour dataframe tooadd ihtiyacımız var. Merhaba geçerli kod POSIXct sınıfının yeni bir sütun ekler hello şununla değiştirin.

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check hello results

Şimdi, hello günlüğünü denetleyin. Şekil 15 gibi görünmelidir.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

*Şekil 15. Bir zaman serisi nesnesiyle hello dataframe özeti.*

Bu hello yeni bir sütun aslında POSIXct sınıfıdır hello Özet görebiliriz.

### <a name="exploring-and-transforming-hello-data"></a>Keşfetmek ve hello veri dönüştürme
Bu veri kümesinde hello değişkenlerinin bazıları inceleyelim. Scatterplot matrisini en iyi yolu tooproduce hızlı bir görünümünü verir. Merhaba değiştirme `str()` hello önceki R kod satırı aşağıdaki hello ile işlevinde.

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

Bu kodu çalıştırmak ve ne olduğunu gözleyin. R aygıtı bağlantı noktası Hello üretilen hello çizim Şekil 16 gibi görünmelidir.

![Seçili değişkenleri Scatterplot Matrisi][17]

*Şekil 16. Seçili değişkenleri Scatterplot matrisi.*

Bu değişkenler arasında hello ilişkilerde bazı garip görünüşlü yapısı yoktur. Belki de bu hello verilerindeki eğilimleri ve biz hello değişkenleri standartlaşmış değil, hello olgu ortaya çıkar.

### <a name="correlation-analysis"></a>Bağıntı çözümleme
tooboth ihtiyacımız tooperform bağıntı çözümleme XML'deki eğilimi ve hello değişkenleri standart hale getirme. Biz yalnızca hello R kullanabilirsiniz `scale()` merkezleri hem değişkenleri ölçeklendirir işlevi. Bu işlev iyi daha hızlı çalışabilir. Ancak, tooshow istiyorum, r içinde savunma programing örneği

Merhaba `ts.detrend()` aşağıda gösterilen işlevi bu işlemlerin her ikisini de gerçekleştirir. Merhaba aşağıdaki iki satır kod hello veri XML'deki eğilimi ve hello değerleri standart hale getirme.

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function toode-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time toohave hello same length',
                    'ERROR: ts.detrend requires argument ts toobe of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros tooreturn as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # hello input arguments are not of hello same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If hello ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If hello ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that hello Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend hello time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply hello detrend.ts function toohello variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot hello results toolook at hello relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

Merhaba içinde oldukça bit oluşmasını yoktur `ts.detrend()` işlevi. Bu kod çoğu hello bağımsız değişkenleri ile ilgili olası sorunları denetleme veya hala hello hesaplamalar sırasında ortaya çıkabilecek özel durumlarla birlikte ele alma. Bu kod yalnızca birkaç satırlık gerçekte hesaplamalar hello.

Biz zaten savunma programlamada örneği ele alınan [değer dönüşümler](#valuetransformations). Her iki hesaplama blokları kaydırılır `tryCatch()`. İsteğe bağlı olarak bazı hatalar için anlamlı tooreturn hello özgün giriş vektör yapar ve diğer durumlarda, ı vektör sıfır değerini döndürür.  

Merhaba doğrusal regresyon XML'deki eğilimleri belirlemek için kullanılan bir zaman serisi gerileme olduğuna dikkat edin. Merhaba bir göstergesi olduğu değişken bir zaman serisi nesnesidir.  

Bir kez `ts.detrend()` tanımlanmış biz bizim dataframe ilgi toohello değişkenlerinin uygulayın. Tarafından oluşturulan hello sonuç listesini coerce gerekir `lapply()` kullanarak toodata dataframe `as.data.frame()`. Savunma yönlerini nedeniyle `ts.detrend()`, hello değişkenlerinden biri engellemez hatası tooprocess başkalarının hello işlenmesini düzeltin.  

kodun son satırı Hello pairwise scatterplot oluşturur. Merhaba R kodu çalıştırdıktan sonra hello scatterplot hello sonuçlarını şekil 17'de gösterilmektedir.

![XML'deki koleksiyonunuzdaki ve standartlaştırılmış zaman serisinin pairwise scatterplot][18]

*Şekil 17. Pairwise scatterplot XML'deki koleksiyonunuzdaki ve standartlaştırılmış zaman serisinin.*

Şekil 16'da gösterilen bu sonuçları toothose karşılaştırabilirsiniz. Merhaba eğilimi kaldırıldı ve hello değişkenleri standartlaştırılmış, biz bu değişkenleri arasındaki hello ilişkileri çok daha az yapısında bakın.

Merhaba kod toocompute hello bağıntıları R ccf nesneler olarak aşağıdaki gibidir.

    ## A function toocompute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of hello pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute hello list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

Bu kodu çalıştırmak Şekil 18'de gösterilen hello günlük üretir.

    [ModuleOutput] Loading objects:
    [ModuleOutput]   port1
    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] [[1]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.148 0.358 0.317 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[2]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.395 -0.186 -0.238 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[3]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.059 -0.089 -0.127 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[4]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.140 0.294 0.293 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[5]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.002 -0.074 -0.124 

*Şekil 18. Ccf listesi hello pairwise bağıntı çözümlemesinden nesneleri.*

Her gecikme için bir bağıntı değer yoktur. Bu bağıntı değerleri hiçbiri büyüklükte toobe önemli değildir. Biz biz her bir değişken bağımsız olarak model oluşturabilirsiniz, bu nedenle tamamlanabilmesi.

### <a name="output-a-dataframe"></a>Bir dataframe çıkış
Biz hello pairwise bağıntıları R ccf nesneleri listesi olarak hesaplanan. Merhaba sonuç veri kümesinin çıkış bağlantı noktasına bir dataframe gerçekten gerektirdiğinden bu biraz bir sorunu gösterir. Ayrıca, hello ccf nesnesi kendisini listesini ve yalnızca hello değerleri bu listenin hello bağıntıları hello adresindeki hello ilk öğesindeki çeşitli gecikmelere istiyoruz.

kod ayıklar hello gecikme değerleri hello kendilerini listeleridir ccf nesneleri listesinden aşağıdaki hello.

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with hello row names column and the
    ## correlation data frame and assign hello column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## hello following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

Merhaba ilk satırının kod biraz zor olduğu ve bazı açıklama onu anlamanıza yardımcı olabilir. Hello içinde dışarı çalışma biz hello aşağıdaki vardır:

1. Merhaba '**[[**'işleci' hello bağımsız değişkeniyle**1**' seçer hello hello gecikmelere hello ccf nesne listesinin hello ilk öğeden adresindeki bağıntıları vektörü.
2. Merhaba `do.call()` işlevi uygular hello `rbind()` hello listesinin hello öğelerini üzerinden işlevi döndürür tarafından `lapply()`.
3. Merhaba `data.frame()` işlevi tarafından üretilen hello sonuç olacak şekilde zorlar `do.call()` tooa dataframe.

Merhaba satır adlarını hello dataframe sütununda olduğunu unutmayın. Bunun yapılması korur hello satır adlarını hello çıktısını olduklarında [R betiği yürütün][execute-r-script].

Merhaba kod çalıştırmasını çıktılar şekil 19'gösterilen hello zaman ı **Görselleştir** hello çıktıyı hello sonuç Dataset bağlantı noktası. Merhaba satır hello ilk sütunda, beklendiği gibi adlardır.

![Merhaba bağıntı analiz sonuçları çıktısı][20]

*Şekil 19. Merhaba bağıntı çözümlemesinden çıktı sonuçları.*

## <a id="seasonalforecasting"></a>Zaman serisi örnek: Mevsimlik tahmin
Bizim veri analizi için uygun bir biçimde sunulmuştur ve hello değişkenleri arasındaki önemli hiçbir bağıntıları vardır belirledik. Şimdi geçmek ve bir zaman serisi modeli tahmin oluşturun. Bu modeli kullanarak biz California sütlü üretim hello için 2013 12 ay tahmin.

Tahmin modelimizi eğilim bileşeni ve Mevsimlik bileşeni olmak üzere iki bileşenden sahip olur. Merhaba tam tahmin, bu iki bileşenden hello üründür. Bu model türüne çarpma model olarak bilinir. Merhaba, ek bir model alternatiftir. Biz bu çözümleme tractable yapar ilgi günlük dönüştürme toohello değişkenlerinin zaten uyguladınız.

Merhaba tam R Bu bölümde daha önce indirdiğiniz hello zip dosyasında kodudur.

### <a name="creating-hello-dataframe-for-analysis"></a>Merhaba dataframe çözümleme için oluşturma
Başlangıç ekleyerek bir **yeni** [R betiği yürütün] [ execute-r-script] modülü tooyour deneme. Merhaba bağlanmak **sonuç Dataset** hello varolan çıktı [R betiği yürütün] [ execute-r-script] modülü toohello **Dataset1** hello yeni modülünün giriş. Merhaba sonuç Şekil 20 gibi görünmelidir.

![Merhaba eklenen hello yeni R betiği yürütün modülüyle denemeler][21]

*Şekil 20. Merhaba eklenen hello yeni R betiği yürütün modülüyle deneyin.*

Gibi hello bağıntı çözümlemesi biz yalnızca tamamlandı, biz tooadd POSIXct zaman serisi nesne içeren bir sütun gerekir. koddan hello yalnızca bunu yapın.

    # If running in Machine Learning Studio, uncomment hello first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

Bu kodu çalıştırmak ve hello günlüğüne bakın. Merhaba sonuç şekil 21 gibi görünmelidir.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

*Şekil 21. Merhaba dataframe özeti.*

Bu sonuçla duyuyoruz hazır toostart bizim çözümleme.

### <a name="create-a-training-dataset"></a>Bir eğitim veri kümesi oluşturma
Oluşturulan hello dataframe ile toocreate bir eğitim veri kümesi gerekir. Bu verileri tüm 2013 hello yılın son 12 hello dışında hello gözlemleri test kümemize olduğu içerir. Merhaba aşağıdaki alt kümelerini hello dataframe kod ve çizimler hello Süt üretim ve değişkenlerin fiyat oluşturur. I, ardından hello çizimleri dört üretim ve fiyat değişkenleri oluşturun. Adsız bir işlev bazı güçlendirir çizim için kullanılan toodefine olan ve hello hello listesi yineleme diğer iki bağımsız değişkenlerle `Map()`. Size, düşünüyor varsa bir döngü ince burada çalışılan için doğru. Ancak, R ı işlevsel bir yaklaşım gösteren işlevsel bir dili olduğundan.

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

Hello kodu çalıştırmak hello R aygıt çıktısından Şekil 22'de gösterilen zaman serisi serisi çizer hello üretir. Bu hello zaman ekseni tarihleri, yöntemi seriyi çizmek hello zaman iyi bir yararı birimlerinde olduğuna dikkat edin.

![Zaman serisi çizimleri California Süt üretim ve fiyat verilerinin ilk](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![Zaman serisi çizimleri California Süt üretim ve fiyat veri saniyesi](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![Zaman serisi çizimleri California Süt üretim ve fiyat veri üçüncü](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![Zaman serisi çizimleri California Süt üretim ve fiyat veri dördüncü](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

*Şekil 22. Zaman serisi çizimleri California Süt üretim ve fiyat verileri.*

### <a name="a-trend-model"></a>Eğilim modeli
Bir zaman serisi nesnesi ve hello veri gördüğünüze oluşturulduktan sonra tooconstruct hello California sütlü üretim verileri için bir eğilim modeli başlayalım. Zaman serisi regresyon ile biz bunu yapabilirsiniz. Ancak biz eğimi ve ıntercept tooaccurately birden fazla hello eğitim verilerini eğilimi gözlenen hello model olduğunu temizleyin hello çizim olur.

Hello küçük ölçekli hello veri verildiğinde, t Rstudio'dan eğilimi hello model oluşturmak ve ardından kesip hello sonuç olarak oluşan model Azure Machine Learning yapıştırabilirsiniz. Rstudio'dan etkileşimli analiz bu tür için etkileşimli bir ortam sağlar.

Bir ilk girişimi ı polinom regresyon too3 yukarı powers ile çalışacaktır. Bu tür modelleri aşırı sığdırma, gerçek bir tehlike yoktur. Bu nedenle en iyi tooavoid yüksek sipariş terimler olur. Merhaba `I()` işlevi engeller hello içeriği yorumu ('olduğundan' hello içeriği yorumlar) ve bir regresyon denklemi toowrite tam anlamıyla yorumlanan işlevi sağlar.

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

Merhaba aşağıdaki oluşturur.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3),
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12667 -0.02730  0.00236  0.02943  0.10586
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.33e+00   1.45e-01   43.60   <2e-16 ***
    ## Time              1.63e-09   1.72e-10    9.47   <2e-16 ***
    ## I(Month.Count^2) -1.71e-06   4.89e-06   -0.35    0.726
    ## I(Month.Count^3) -3.24e-08   1.49e-08   -2.17    0.031 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0418 on 212 degrees of freedom
    ## Multiple R-squared:  0.941,    Adjusted R-squared:  0.94
    ## F-statistic: 1.12e+03 on 3 and 212 DF,  p-value: <2e-16

P değerlerinden (Pr (> | t |)) bu çıktısında bu hello görebiliriz squared terim belirgin olmayabilir. Merhaba kullanacağım `update()` bu modeli bırakma hello tarafından kare terimi toomodify işlev.

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

Merhaba aşağıdaki oluşturur.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12597 -0.02659  0.00185  0.02963  0.10696
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.38e+00   4.07e-02   156.6   <2e-16 ***
    ## Time              1.57e-09   4.32e-11    36.3   <2e-16 ***
    ## I(Month.Count^3) -3.76e-08   2.50e-09   -15.1   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0417 on 213 degrees of freedom
    ## Multiple R-squared:  0.941,  Adjusted R-squared:  0.94
    ## F-statistic: 1.69e+03 on 2 and 213 DF,  p-value: <2e-16

Bu, daha iyi görünür. Merhaba koşullarının tamamını önemlidir. Ancak, hello 2e-16 değeri varsayılan değerdir ve çok ciddi alınmamalıdır.  

Sağlamlık test olarak bir zaman serisi çizim hello California Süt üretim verileri, gösterilen hello eğilimi eğri olalım. Hello Azure Machine Learning kodda aşağıdaki hello eklemiş olduğunuz [R betiği yürütün] [ execute-r-script] modeli (değil Rstudio'dan) toocreate hello modeli ve bir çizim yapın. Merhaba sonuç şekil 23'te gösterilir.

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![California sütlü üretim verileri ile gösterilen eğilimi modeli](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

*Şekil 23. California sütlü üretim verileriyle gösterilen eğilimi modeli.*

Merhaba eğilimi modeli hello veri oldukça iyi uygun gibi görünüyor. Ayrıca, değil gözükmüyor atlayarak sığdırma toobe kanıtı gibi hello modeli eğrisindeki tek wiggles.  

### <a name="seasonal-model"></a>Mevsimlik modeli
Bir eğilim modelinde el ile toopush gereken ve hello Mevsimlik efektleri içerir. Merhaba Doğrusal model toocapture hello ay ay etkisi kukla bir değişkende olarak hello yılın hello ayı kullanacağız. Bir modele faktörü değişkenleri aldığımızda, hello ıntercept'in değil hesaplanan gerekir unutmayın. Bunu yapmazsanız, hello formülü aşırı belirtilen ise ve R bırakacaktır hello birini Etkenler istenen ancak hello ıntercept terim tutun.

Biz tatmin edici eğilimi modeline sahip olduğundan biz hello kullanabilir `update()` işlevi tooadd hello yeni koşulları toohello varolan modeli. Merhaba -1 hello güncelleştirme formülünde hello ıntercept terim bırakır. İçinde Rstudio'dan hello şu anda devam:

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

Merhaba aşağıdaki oluşturur.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3) + Month - 1,
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.06879 -0.01693  0.00346  0.01543  0.08726
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## Time              1.57e-09   2.72e-11    57.7   <2e-16 ***
    ## I(Month.Count^3) -3.74e-08   1.57e-09   -23.8   <2e-16 ***
    ## MonthApr          6.40e+00   2.63e-02   243.3   <2e-16 ***
    ## MonthAug          6.38e+00   2.63e-02   242.2   <2e-16 ***
    ## MonthDec          6.38e+00   2.64e-02   241.9   <2e-16 ***
    ## MonthFeb          6.31e+00   2.63e-02   240.1   <2e-16 ***
    ## MonthJan          6.39e+00   2.63e-02   243.1   <2e-16 ***
    ## MonthJul          6.39e+00   2.63e-02   242.6   <2e-16 ***
    ## MonthJun          6.38e+00   2.63e-02   242.4   <2e-16 ***
    ## MonthMar          6.42e+00   2.63e-02   244.2   <2e-16 ***
    ## MonthMay          6.43e+00   2.63e-02   244.3   <2e-16 ***
    ## MonthNov          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## MonthOct          6.37e+00   2.63e-02   241.8   <2e-16 ***
    ## MonthSep          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0263 on 202 degrees of freedom
    ## Multiple R-squared:     1,    Adjusted R-squared:     1
    ## F-statistic: 1.42e+06 on 14 and 202 DF,  p-value: <2e-16

Biz bu hello modeli artık bir kesme noktası terim ve 12 önemli ay Etkenler sahip bakın. Bu tam biz istedik olduğundan toosee.

Merhaba California Süt üretim verileri toosee hello Mevsimlik modeli ne kadar iyi çalıştığı, başka bir zaman serisi çizim olalım. Hello Azure Machine Learning kodda aşağıdaki hello eklemiş olduğunuz [R betiği yürütün] [ execute-r-script] toocreate hello modeli ve bir çizim yapın.

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

Azure Machine Learning ile bu kodu çalıştırmak hello çizim şekil 24'te gösterilen üretir.

![California sütlü üretim Mevsimlik efektler dahil modeli](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

*Şekil 24. California sütlü üretim Mevsimlik efektler dahil modeli.*

Merhaba şekil 24'te gösterilen uygun toohello yerine encouraging verilerdir. Merhaba eğilim ve hello Mevsimlik etkili (aylık değişim) makul arayın.

Bizim model üzerinde başka bir onay, şirketinizdeki hello Kalanlar göz vardır. Merhaba aşağıdaki kodu hesaplar bizim iki modeli tahmin edilen değerler hello hello Kalanlar hello Mevsimlik modeli için hesaplar ve bu Kalanlar hello eğitim verileri için çizer.

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot hello residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

Merhaba fazlalık çizim şekil 25 gösterilir.

![Kalanlar hello Mevsimlik modelinin hello eğitim verileri](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

*Şekil 25. Kalanlar hello Mevsimlik modelinin hello eğitim verileri.*

Bu Kalanlar makul arayın. Bizim modeli için hesaplamaz hello 2008-2009 recession hello etkisini dışında hiçbir belirli yapısı yoktur özellikle iyi.

Merhaba çizim şekil 25 gösterilen herhangi zamana bağımlı desenleri hello Kalanlar algılamak için yararlı olur. hello açık yaklaşım, hesaplama ve kullandım hello çizme hello çizim zaman siparişte hello Kalanlar yerleştirir. Merhaba diğer yandan, ı çizilen, `milk.lm$residuals`, hello çizim süre sırada değil olabilirdi.

Aynı zamanda `plot.lm()` tooproduce tanılama çizimler bir dizi.

    ## Show hello diagnostic plots for hello model
    plot(milk.lm2, ask = FALSE)

Bu kod, bir dizi şekil 26'da gösterilen tanılama çizimleri üretir.

![Merhaba Mevsimlik modeli için tanılama çizimleri ilk](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Tanılama çizimleri ikinci hello Mevsimlik modeli için](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Merhaba Mevsimlik modeli için tanılama çizimleri üçüncü](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Merhaba Mevsimlik modeli için tanılama çizimleri dördüncü](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

*Şekil 26. Tanılama hello Mevsimlik model için çizer.*

Bu çizimler, ancak hiçbir şey tanımlanan birkaç yüksek etkili noktası toocause harika sorun. Ayrıca, biz hello Normal Q-Q çizim hello Kalanlar dağıtılmış, Kapat toonormally doğrusal modeller için önemli varsayılır olduğunu görebilirsiniz.

### <a name="forecasting-and-model-evaluation"></a>Tahmin ve model değerlendirme
Bizim örneğimizde tek daha fazla şey toodo toocomplete yoktur. Biz toocompute tahminleri gerekir ve hello hata hello gerçek veri karşı ölçebilirsiniz. Bizim tahmin Merhaba 2013 12 ay olacaktır. Biz eğitim kümemize parçası olmayan bu tahmin toohello gerçek veri için bir hata ölçü hesaplayabilirsiniz. Ayrıca, biz hello performansı test verilerinin 12 ay eğitim veri toohello 18 yıllık karşılaştırabilirsiniz.  

Ölçümleri sayısı kullanılan toomeasure hello zaman serisi modelleri performansını. Örneğimizde hello kök Ortalama kare (RMS) hata kullanacağız. Merhaba aşağıdaki işlevi iki serinin arasındaki hello RMS hatası hesaplar.  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function toocompute hello RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments toofunction RMS.error of wrong type encountered",
                    "ERROR: Input vector toofunction RMS.error is too short",
                    "ERROR: Input vectors toofunction RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check hello arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate hello values, else just copy
      if(is.log) {
        tryCatch( {
          temp1 <- exp(series1)
          temp2 <- exp(series2) },
          error = function(e){warning(messages[4]); NA}
        )
      } else {
        temp1 <- series1
        temp2 <- series2
      }

     ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute hello RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

Merhaba olduğu gibi `log.transform()` biz ele alınmıştır işlevi Merhaba "dönüşümleri değer" bölümü, oldukça çok sayıda hata denetimi ve özel durum kurtarma kodu Bu işlevde yoktur. işe hello ilkeleri olan hello aynı. Merhaba iş sarmalanmış iki yerde yapılır `tryCatch()`. İlk olarak, biz hello değerleri hello günlükleriyle çalışma olduğundan hello zaman serisi exponentiated, ' dir. İkinci olarak, hello gerçek RMS hatası hesaplanır.  

Bir işlev toomeasure hello RMS hatası ile donatılmış, şimdi oluşturun ve hello RMS hata içeren bir dataframe çıktı. Merhaba eğilimi model tek başına koşulları ve hello tam Mevsimlik Etkenler modeliyle dahil edilir. Merhaba aşağıdaki kodu iş biz oluşturulan hello iki doğrusal modellerin kullanarak hello.

    ## Compute hello RMS error in a dataframe
    ## Include hello row names in hello first column so they will
    ## appear in hello output of hello Execute R Script
    RMS.df  <-  data.frame(
    rowNames = c("Trend Model", "Seasonal Model"),
      Traing = c(
      RMS.error(predict1[1:216], cadairydata$Milk.Prod[1:216]),
      RMS.error(predict2[1:216], cadairydata$Milk.Prod[1:216])),
      Forecast = c(
        RMS.error(predict1[217:228], cadairydata$Milk.Prod[217:228]),
        RMS.error(predict2[217:228], cadairydata$Milk.Prod[217:228]))
    )
    RMS.df

    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

Bu kodu çalıştırmak sonuç veri kümesinin çıkış bağlantı noktasına hello şekil 27'de gösterilen hello çıkışı üretir.

![Merhaba modelleri için RMS hataları karşılaştırması][26]

*Şekil 27. Karşılaştırma hello modelleri için RMS hata sayısı.*

Bu sonuçlarından hello Mevsimlik Etkenler toohello ekleme modeli hello RMS hatası önemli ölçüde azaltır, bkz. Çok edilebileceği hello RMS hata verileri eğitim hello için biraz küçük Merhaba tahmin.

## <a id="appendixa"></a>Ek A: Kılavuzu tooRStudio
Bu ekte ı bazı bağlantılar toohello başlattığınız hello Rstudio'dan belgelerine tooget anahtar bölümlerini sağlayacak şekilde Rstudio'dan oldukça iyi belgelenmiştir.

1. Proje oluşturma
   
   Düzenleyebilir ve Rstudio'dan kullanarak R kodunuzu projelere yönetin. projeleri kullanan hello belgelerine https://support.rstudio.com/hc/articles/200526207-Using-Projects bulunabilir.
   
   I bu yönergeleri izleyin ve bu belgede hello R kod örnekleri için bir proje oluşturun öneririz.  
2. Düzenleme ve R kodu çalıştırma
   
   Rstudio'dan düzenleme ve R kod yürütmek için tümleşik bir ortam sağlar. Belge https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code bulunabilir.
3. Hata ayıklama
   
   Rstudio'dan güçlü hata ayıklama özellikleri içerir. Bu özellikler için belgeleri https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio ' dir.
   
   Merhaba kesme noktası sorun giderme özellikleri https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting belgelenmiştir.

## <a id="appendixb"></a>Ek B: Daha fazla bilgi
Eğitmen kapsar hello temel programlama bu R hangi, Azure Machine Learning Studio'da R dil toouse hello. R ile bilmiyorsanız, iki tanıtımları CRAN üzerinde kullanılabilir:

* R Emmanuel Paradis tarafından yeni başlayanlar için http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf en iyi toostart ' dir.  
* Bir giriş tooR W. n tarafından Venables et. Al. biraz daha derinliğinde, http://cran.r-project.org/doc/manuals/R-intro.html geçer.

Başlamanıza yardımcı olabilecek R birçok books vardır. Yararlı bulabilirim birkaç şunlardır:

* Merhaba resim R Programming: A Tur, istatistiksel yazılım Norman Matloff tarafından tasarımdır mükemmel giriş tooprogramming r içinde  
* R Kılavuzu Paul Teetor tarafından bir sorunu ve çözümü yaklaşım toousing r sağlar  
* Eylem Robert Kabacoff tarafından R başka yararlı tanıtım Rehberi ' dir. Merhaba Yardımcısı hızlı R Web sitesi http://www.statmethods.net/ en kullanışlı bir kaynaktır.
* R Inferno CAN yanıklara tarafından r hello Defteri'nde programlamada karşılaştı hassas ve zor konular sayısıyla ilgilidir şaşırtıcı esprili bir kitap ücretsiz http://www.burns-stat.com/documents/books/the-r-inferno/ kullanılabilir.
* Derinlemesine Gelişmiş konular R, içine istiyorsanız hello defteri Gelişmiş R Hadley Wickham tarafından bakmak gerekir. Bu kitap çevrimiçi sürümünü Hello ücretsiz http://adv-r.had.co.nz/ kullanılabilir.

Merhaba CRAN görev görünümü zaman serisi çözümleme için bir katalog R zaman serisi paketlerin bulunabilir: http://cran.r-project.org/web/views/TimeSeries.html. Belirli bir zaman serisi nesnesi paketleri hakkında daha fazla bilgi için bu paket için toohello belgelerine başvurmalıdır.

Merhaba kitap Paul Cowpertwait ve Barış Metcalfe r Giriş zaman serisi zaman serisi çözümleme için giriş toousing R sağlar. Çok fazla teorik metinleri R örnekleri sağlar.

Harika bazı Internet kaynakların:

* DataCamp: Hello rahatlık tarayıcınızın video dersleri ve kodlama alıştırmaları içinde R DataCamp öğretir. Etkileşimli öğreticiler hello son R teknikleri ve paketleri vardır. Merhaba ücretsiz etkileşimli R https://www.datacamp.com/courses/introduction-to-r Öğreticisi
* Bir alma üzerinde R ile Programiz https://www.programiz.com/r-programming Kılavuzu
* Bir hızlı R Öğreticisi tarafından Kelly siyah Clarkson University http://www.cyclismo.org/tutorial/R/ gelen
* R http://www.ComputerWorld.com/article/2497464/Business-intelligence-60-r-Resources-to-improve-Your-Data-skills.HTML listelenen 60 + kaynakları

<!--Image references-->
[1]: ./media/machine-learning-r-quickstart/fig1.png
[2]: ./media/machine-learning-r-quickstart/fig2.png
[3]: ./media/machine-learning-r-quickstart/fig3.png
[4]: ./media/machine-learning-r-quickstart/fig4.png
[5]: ./media/machine-learning-r-quickstart/fig5.png
[6]: ./media/machine-learning-r-quickstart/fig6.png
[7]: ./media/machine-learning-r-quickstart/fig7.png
[8]: ./media/machine-learning-r-quickstart/fig8.png
[9]: ./media/machine-learning-r-quickstart/fig9.png
[10]: ./media/machine-learning-r-quickstart/fig10.png
[11]: ./media/machine-learning-r-quickstart/fig11.png
[12]: ./media/machine-learning-r-quickstart/fig12.png
[13]: ./media/machine-learning-r-quickstart/fig13.png
[14]: ./media/machine-learning-r-quickstart/fig14.png
[15]: ./media/machine-learning-r-quickstart/fig15.png
[16]: ./media/machine-learning-r-quickstart/fig16.png
[17]: ./media/machine-learning-r-quickstart/fig17.png
[18]: ./media/machine-learning-r-quickstart/fig18.png
[19]: ./media/machine-learning-r-quickstart/fig19.png
[20]: ./media/machine-learning-r-quickstart/fig20.png
[21]: ./media/machine-learning-r-quickstart/fig21.png
[22]: ./media/machine-learning-r-quickstart/fig22.png

[26]: ./media/machine-learning-r-quickstart/fig26.png

<!--links-->
[appendixa]: #appendixa
[download]: https://azurebigdatatutorials.blob.core.windows.net/rquickstart/RFiles.zip


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
