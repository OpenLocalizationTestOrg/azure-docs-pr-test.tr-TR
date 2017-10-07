---
title: "Merhaba Linux veri bilimi sanal makine üzerinde aaaData Bilim | Microsoft Docs"
description: "Nasıl tooperform birçok ortak veri bilimi hello Linux veri bilimi VM ile görevler."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: 78764825f2e834fa4ddb7fdc2f59418dbe736e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-on-hello-linux-data-science-virtual-machine"></a>Veri bilimi hello Linux veri bilimi sanal makine üzerinde
Bu anlatımda tooperform birçok ortak veri bilimi hello Linux veri bilimi VM ile nasıl görevler gösterilir. Merhaba Linux veri bilimi sanal makine (DSVM) veri analizi ve makine öğrenme için yaygın olarak kullanılan bir araç koleksiyonu ile önceden yüklenmiş olan Azure üzerinde kullanılabilir bir sanal makine görüntüdür. Merhaba anahtar yazılım bileşenleri hello dökümü [sağlama hello Linux veri bilimi sanal makine](machine-learning-data-science-linux-dsvm-intro.md) konu. Merhaba VM görüntüsü kolay tooget kolaylaştırır tooinstall gerek kalmadan dakika cinsinden veri bilimi yapılması başlatıldı ve hello araçların her biri ayrı ayrı yapılandırın. Kolayca VM hello gerekirse ölçekleme ve uygulamayı kullanılmadığında durdurun. Bu nedenle bu kaynak, esnek ve ekonomik içindir.

Merhaba bu kılavuzda gösterilen veri bilimi görevleri hello özetlenen hello adımları [takım veri bilimi işlemi](https://azure.microsoft.com/documentation/learning-paths/data-science-process/). Bu işlem, veri bilimcilerine tooeffectively işbirliği akıllı uygulamaları oluşturma hello ömrü ekiplerin sağlayan sistematik bir yaklaşım toodata bilimsel sunar. Merhaba veri bilimi işlemi da bir kişi tarafından izlenebilir veri bilimi için yinelemeli bir çerçeve sağlar.

Biz hello analiz [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) bu kılavuzda veri kümesi. Bu e-postaların istenmeyen posta ya da (olmadıkları istenmeyen posta anlamına gelir) ham, olarak işaretlenmiş kümesidir ve ayrıca bazı istatistiklerle hello e-postaları Merhaba içeriğine içerir. Merhaba istatistikleri dahil hello sonraki bir bölümü ele alınmıştır.

## <a name="prerequisites"></a>Ön koşullar
Linux veri bilimi sanal makine kullanmadan önce hello şunlara sahip olmanız gerekir:

* Bir **Azure aboneliği**. Zaten bir yoksa, bkz: [ücretsiz Azure hesabınızı bugün oluşturmak](https://azure.microsoft.com/free/).
* A [ **Linux veri bilimi VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm). Bu VM sağlama hakkında daha fazla bilgi için bkz: [sağlama hello Linux veri bilimi sanal makine](machine-learning-data-science-linux-dsvm-intro.md).
* [X2Go](http://wiki.x2go.org/doku.php) bilgisayarınızda yüklü ve bir XFCE oturumu açılır. Yükleme ve yapılandırma hakkında bilgi için bir **X2Go istemci**, bkz: [yükleme ve yapılandırma X2Go istemci](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client). 
* Bir **AzureML hesap**. Bir hello en yeni bir kayıt zaten yoksa, [AzureML giriş sayfası](https://studio.azureml.net/). Kullanmaya başlama ücretsiz kullanım katmanı toohelp yoktur.

## <a name="download-hello-spambase-dataset"></a>Merhaba spambase dataset indirin
Merhaba [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) veri kümesi yalnızca 4601 örnekleri içeren veri görece küçük kümesidir. Bu kullanışlı boyutu toouse hello veri bilimi VM şekilde hello önemli özelliklerinden bazıları tutmasını hello kaynak gereksinimlerini uygun gösteren durumdur.

> [!NOTE]
> Bu kılavuz bir D2 v2 ölçekli Linux veri bilimi sanal makinede oluşturuldu. Bu boyut DSVM hello yordamları bu kılavuzda işleyebilir.
>
>

Daha fazla depolama alanı gerekiyorsa, ek diskleri oluşturma ve bunları tooyour VM ekleyin. Hello sunucu bile sağlama verilerini son korunur şekilde bu diskleri kalıcı Azure depolama kullanan tooresizing veya kapatılır. tooadd bir disk ve tooyour VM ekleme, hello yönergeleri izleyin [disk tooa Linux VM eklemek](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Bu adımları hello DSVM hello üzerinde önceden yüklenmiş Azure komut satırı arabirimi (Azure CLI) kullanın. Bu nedenle bu yordamları tamamen hello VM kendisini ' yapılabilir. Başka bir seçenek tooincrease depolama toouse olan [Azure dosyaları](../storage/files/storage-how-to-use-files-linux.md).

toodownload hello verileri, bir terminal penceresi açın ve şu komutu çalıştırın:

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

Merhaba indirilen dosya bir başlık satırı yok, sağlandığından üstbilgi sahip başka bir dosya oluşturun. Bu komut toocreate hello uygun üst bilgilerle bir dosya çalıştırın:

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

Ardından hello komutu ile birlikte hello iki dosyaları birleştirme:

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

Hello dataset istatistikleri çeşitli türlerde her e-postaya sahiptir:

* Sütunları ister ***word\_freq\_WORD*** eşleşen hello e-posta sözcükleri hello yüzdesini belirtmek *WORD*. Örneğin, varsa *word\_freq\_olun* %1 hello e-posta içindeki tüm sözcükleri bundan sonra 1 ' dir *olun*.
* Sütunları ister ***char\_freq\_CHAR*** olan tüm hello e-posta karakter hello yüzdesini belirtmek *CHAR*.
* ***büyük\_çalıştırmak\_uzunluğu\_uzun*** hello uzun büyük harf bir dizi uzunluğu.
* ***büyük\_çalıştırmak\_uzunluğu\_ortalama*** büyük harfle tüm sıralarının hello ortalama uzunluğudur.
* ***büyük\_çalıştırmak\_uzunluğu\_toplam*** büyük harfle tüm sıralarının hello toplam uzunluğu.
* ***istenmeyen posta*** hello e-posta istenmeyen posta kabul olup olmadığını gösterir (1 istenmeyen posta, 0 = değil istenmeyen posta =).

## <a name="explore-hello-dataset-with-microsoft-r-open"></a>Microsoft R açık Hello kümesiyle keşfedin
Şimdi hello verileri incelemek ve bazı temel machine learning ile veri bilimi VM ile birlikte gelen r hello yapın [Microsoft R açık](https://mran.revolutionanalytics.com/open/) önceden yüklenmiş. Merhaba birden çok iş parçacıklı matematik kitaplıkları R bu sürümündeki çeşitli tek iş parçacıklı sürümleri daha iyi performans sunar. Microsoft R açık de yeniden Üretilebilirlik hello CRAN Paket Deposu görüntüsünü kullanarak sağlar.

Merhaba tooget kopyalarını kod örnekleri bu kılavuzda, kopya hello kullanılan **Azure-Machine-Learning-Data-Bilim** hello VM üzerinde önceden yüklenmiş olduğu git, kullanarak deposu. Merhaba git komut satırından çalıştırın:

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

Bir terminal penceresi açın ve hello R etkileşimli konsolu ile yeni bir R oturumu başlatın.

> [!NOTE]
> Rstudio'dan yordamları izleyerek hello için de kullanabilirsiniz. tooinstall Rstudio'dan, bir terminal, bu komutu yürütün:`./Desktop/DSVM\ tools/installRStudio.sh`
>
>

tooimport hello veri ve hello ortamı kurma çalıştırın:

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

Her sütunun hakkında özet istatistikleri toosee:

    summary(data)

Merhaba verileri farklı bir görünüm için:

    str(data)

Bu, her bir değişken türü hello ve ilk birkaç değerleri hello kümesindeki hello gösterir.

Merhaba *istenmeyen posta* sütun bir tamsayı olarak okundu, ancak gerçekte kategorik olan değişkeni (veya faktörü). tooset türü:

    data$spam <- as.factor(data$spam)

toodo bazı keşif analiz, kullanım hello [ggplot2](http://ggplot2.org/) paketini, hello VM üzerinde zaten yüklü R için popüler bir grafik kitaplığı. , Daha önce görüntülenen hello Özet verilerden biz Özet istatistikleri hello ünlem işareti karakteri hello sıklığını sahip olduğunu unutmayın. Şimdi bu sıklıklarını burada komutları aşağıdaki hello çizimi:

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Şimdi Hello sıfır çubuğu hello çizim eğriltme olduğundan, bunu kurtulun:

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Önemsiz olmayan yoğunluğu ilginç görünüyor 1 yukarıda yoktur. Bu verileri yalnızca bakalım:

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Ardından istenmeyen posta vs ham tarafından böl:

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

Bu örnekler, toomake benzer çizimleri Merhaba, diğer sütunları tooexplore etkinleştirmelisiniz hello içerdikleri veriler.

## <a name="train-and-test-an-ml-model"></a>Eğitme ve test ML modeli
Şimdi tren birkaç machine learning tooclassify hello hello dataset postalarda modeller artık ya da içerecek şekilde span veya ham. Biz karar ağacı modeli ve bu bölümdeki rastgele orman modeli eğitmek ve kendi tahminleri kendi doğruluğunu test edin.

> [!NOTE]
> koddan hello kullanılan hello rpart (özyinelemeli bölümlendirme ve regresyon ağaçlarında) paket hello veri bilimi VM üzerinde zaten yüklü.
>
>

İlk olarak, şimdi hello dataset eğitim ve test ayarlar böl:

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

Ve ardından e-postaları karar ağacı tooclassify hello oluşturun.

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

Merhaba sonuç şöyledir:

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

ne kadar iyi üzerinde hello eğitim gerçekleştirir toodetermine ayarlamak, koddan hello kullanın:

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

toodetermine ne kadar iyi hello test kümesinde gerçekleştirir:

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

Ayrıca bir rastgele orman modeli deneyelim. Rastgele ormanları karar ağaçları çok sayıda eğitmek ve tüm hello ayrı ayrı karar ağaçları hello sınıflandırmaları hello modunun bir sınıf çıkış. Karar ağacı modeli toooverfit bir eğitim veri kümesi hello eğilimi için düzeltirken yaklaşım öğrenme daha güçlü bir makine sağlarlar.

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-tooazure-ml"></a>Model tooAzure ML dağıtma
[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML), kolay toobuild kolaylaştırır ve Tahmine dayalı analiz modelleriniz dağıtan bir bulut hizmetidir. AzureML iyi özelliklerini hello herhangi R işlev bir web hizmeti olarak kendi yeteneği toopublish biridir. Merhaba AzureML R paketi dağıtımı kolay toodo DSVM hello üzerinde bizim R oturumundan sağ hale getirir.

toodeploy hello karar ağacı kod hello önceki bölümdeki tooAzure Machine Learning Studio toosign gerekir. Çalışma alanı Kimliğinizi ve bir yetkilendirme belirteci toosign gerekir. toofind bu değerleri ve onlarla Initialize hello AzureML değişkenleri:

Seçin **ayarları** hello sol menüdeki. Not, **çalışma alanı kimliği**. ![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)

Seçin **yetkilendirme belirteçleri** hello genel gider menüsünden ve Not, **birincil yetkilendirme belirteci**.![ 3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)

Yük hello **AzureML** paketini ve belirteç ve çalışma alanı Kimliğiniz ile Merhaba değişkenlerin değerleri R oturumunuzda DSVM hello üzerinde ayarlayın:

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


Şimdi bu tanıtımı daha kolay tooimplement hello modeli toomake basitleştirin. Merhaba üç değişkenleri hello karar ağacı en yakın toohello kök dizininde seçin ve yalnızca bu üç değişkenin kullanarak yeni bir ağaç yapılandırın:

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

Merhaba özellikleri bir girdi olarak alır tahmin işlevinde ihtiyacımız ve tahmin edilen değerler döndürür hello:

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

Yayımlama Hello kullanarak hello predictSpam işlevi tooAzureML **publishWebService** işlevi:

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

Bu işlev hello alır **predictSpam** işlev, adlı bir web hizmeti oluşturur **spamWebService** girişleri ve çıkışları ile tanımlanan ve hello yeni uç noktası hakkında bilgi verir.

Merhaba ayrıntılarını görüntüleme web hizmeti, kendi API uç noktası ve erişim anahtarları hello komutuyla dahil yayımlanan:

    spamWebService[[2]]

tootry, çıkışı hello hello test kümesinin ilk 10 satır:

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a>Kullanılabilir diğer araçlarını kullanma
Merhaba kalan bölümleri nasıl hello araçlardan bazıları yüklü toouse hello Linux veri bilimi VM gösterir. Açıklanan araçları hello listesi aşağıdadır:

* XGBoost
* Python
* Jupyterhub
* Çıngırağı
* PostgreSQL & Squirrel SQL
* SQL Server veri ambarı

## <a name="xgboost"></a>XGBoost
[XGBoost](https://xgboost.readthedocs.org/en/latest/) hızlı ve doğru boosted ağaç uygulaması sağlayan bir araçtır.

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

XGBoost, python veya bir komut satırından da çağırabilirsiniz.

## <a name="python"></a>Python
Python kullanarak geliştirme için hello Anaconda Python dağıtımları 2.7 ve 3.5 hello DSVM yüklenmiş.

> [!NOTE]
> Merhaba Anaconda dağıtım içeren [Condas](http://conda.pydata.org/docs/index.html), hangi kullanılan toocreate farklı sürümlerini ve/veya bunları yüklü olan paketleri sahip Python için özel ortamları olabilir.
>
>

Şimdi hello spambase dataset bazıları okuyun ve Destek vektör scikit makinelerinizde ile Merhaba e-postaları sınıflandırmak-öğrenin:

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

toomake tahminleri:

    clf.predict(X.ix[0:20, :])

tooshow nasıl toopublish bir AzureML uç nokta, şimdi yapma daha basit bir model hello üç değişkenleri olarak biz hello R modeli önceden yayımlandığında yaptığımız.

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

toopublish hello modeli tooAzureML:

    # Publish hello model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about hello resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call hello model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> Bu, yalnızca python 2.7 için kullanılabilir ve 3.5 henüz desteklenmiyor. Çalıştırma **/anaconda/bin/python2.7**.
>
>

## <a name="jupyterhub"></a>Jupyterhub
Merhaba Anaconda hello dağıtımlarında DSVM Jupyter Not Defteri, platformlar arası ortamda tooshare Python, R veya Jale kodunu ve analiz ile birlikte gelir. Merhaba Jupyter not defteri JupyterHub erişilir. Yerel Linux kullanıcı adı ve parola kullanarak oturum ***https://\<VM DNS adı veya IP adresi\>: 8000 /***. Tüm yapılandırma dosyalarını JupyterHub için dizinde bulunan **/etc/jupyterhub**.

Birkaç örnek not defterlerini hello VM üzerinde zaten yüklenir:

* Merhaba bkz [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) bir örnek Python not defteri için.
* Bkz: [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) bir örnek için **R** dizüstü bilgisayar.
* Merhaba bkz [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) başka bir örnek için **Python** dizüstü bilgisayar.

> [!NOTE]
> Merhaba Jale dil hello Linux veri bilimi VM üzerinde hello komut satırından da mevcuttur.
>
>

## <a name="rattle"></a>Çıngırağı
[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (R analitik aracı tooLearn kolayca hello) veri araştırma için grafiksel bir R aracıdır. Kolay tooload kolaylaştırır sezgisel bir arabirim sahip, keşfetmek, veri dönüştürme ve yapı ve modelleri değerlendirin.  Merhaba makale [Rattle: bir veri madenciliği GUI r](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) özelliklerini gösteren bir kılavuz sağlar.

Yükleyin ve aşağıdaki komutları hello ile Çıngırağı başlatın:

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> Yükleme DSVM hello üzerinde gerekli değildir. Ancak Çıngırağı onu yüklediğinde tooinstall ek paketler isteyebilir.
>
>

Çıngırağı sekmesini tabanlı bir arabirim kullanır. Merhaba sekmeleri çoğunu karşılık hello toosteps [veri bilimi işlemi](https://azure.microsoft.com/documentation/learning-paths/data-science-process/)veri yükleme veya araştırma gibi. Sol tooright hello sekmeleri üzerinden gelen Hello veri bilimi işlemi akar. Ancak hello R komutlarını tarafından Çıngırağı Çalıştır günlüğünü hello son sekme içerir.

tooload ve hello dataset yapılandırın:

* tooload hello dosya, select hello **veri** sekmesinde, ardından
* Merhaba Seçici sonraki çok seçin**Filename** ve **spambaseHeaders.data**.
* tooload hello dosyası. seçin **yürütme** düğmelerinin üst satırda hello. Bir giriş, bir hedef veya başka bir değişken türü ve benzersiz değerlerin sayısını hello olup olmadığını, belirtilen veri türü de dahil olmak üzere her bir sütunun özetini görmeniz gerekir.
* Çıngırağı hello doğru tanımlanan **istenmeyen posta** hello hedefi olarak sütun. Select hello istenmeyen posta sütun sonra kümesi hello **hedef veri türü** çok**Categoric**.

tooexplore hello verileri:

* Select hello **Araştır** sekmesi.
* Tıklatın **Özet**, ardından **yürütme**, toosee hello değişken türleri ve bazı Özet istatistikleri hakkında bazı bilgiler.
* tooview her bir değişken hakkındaki istatistiklerdir diğer türleri gibi diğer seçenekleri seçin **açıklayın** veya **Temelleri**.

Merhaba **Araştır** sekme ayrıca ayrıntılı birçok çizer toogenerate, sağlar. tooplot hello verilerin bir histogram oluşturur:

* Seçin **dağıtımları**.
* Denetleme **Histogram** için **word_freq_remove** ve **word_freq_you**.
* Seçin **yürütme**. Her iki yoğunluğu Temizle olduğu bir tek grafik penceresinde "siz" Kaldır"den" e-postalarda çok daha sık görünür bu hello word çizer görmeniz gerekir.

Merhaba bağıntı çizimler, ayrıca ilginç. toocreate biri:

* Seçin **bağıntı** hello olarak **türü**, ardından
* Seçin **yürütme**.
* Çıngırağı, en çok 40 değişkenleri önerir sizi uyarır. Seçin **Evet** tooview hello çizim.

Gündeme bazı ilginç bağıntıları vardır: "teknolojisinin" kesinlikle bağıntılı çok "HP" ve "labs" Örneğin. Ayrıca kesinlikle bağıntılı çok "650", hello alan kodu hello dataset bağışta 650 olduğundan.

sözcükler arasındaki hello bağıntıları Hello sayısal değerleri hello Araştır penceresi için kullanılabilir. Bu ilginç "teknolojisinin" olumsuz "sizin" bağıntılı, örneğin toonote ve "para" olur.

Çıngırağı hello dataset toohandle bazı yaygın sorunlar dönüştürebilirsiniz. Örneğin, toorescale özelliklerini tanır, eksik değerleri impute, aykırı değerlerini işlemek ve değişkenleri veya eksik verilerle gözlemleri kaldırın. Çıngırağı gözlemleri ve/veya değişkenleri arasındaki ilişkilendirme kuralları da tanımlayabilirsiniz. Bu sekme, bu tanıtıcı kılavuz için kapsam dışına:.

Çıngırağı küme analiz de gerçekleştirebilirsiniz. Şimdi bazı özellikleri toomake hello çıktı daha kolay tooread dışlayın. Merhaba üzerinde **veri** sekmesinde, seçin **Yoksay** on bu öğeler dışında hello değişkenlerin sonraki tooeach:

* word_freq_hp
* word_freq_technology
* word_freq_george
* word_freq_remove
* word_freq_your
* word_freq_dollar
* word_freq_money
* capital_run_length_longest
* word_freq_business
* istenmeyen posta

Toohello geri dönün **küme** sekmesinde, seçin **KMeans**ve kümesi hello *küme sayısı* too4. Ardından **yürütme**. Merhaba sonuçlar hello çıktı penceresinde görüntülenir. Bir küme yüksek sıklığı "Hasan" ve "hp" vardır ve büyük olasılıkla yasal iş e-posta olur.

toobuild basit karar ağacı machine learning modelini:

* Select hello **modeli** sekmesi
* Seçin **ağaç** hello olarak **türü**.
* Seçin **yürütme** toodisplay hello metin biçiminde hello ağacında çıktı penceresi.
* Select hello **çizin** düğmesini tooview grafik bir sürüm. Bu oldukça benzer toohello ağaç elde daha önce kullanarak arar *rpart*.

Biri hello iyi Çıngırağı özelliklerini kendi yeteneği toorun birkaç machine learning yöntemleri ve bunları hızlı bir şekilde değerlendirin. Merhaba yordamı şöyledir:

* Seçin **tüm** hello için **türü**.
* Seçin **yürütme**.
* Sona erdikten sonra tüm tek tıklatabilirsiniz **türü**gibi **SVM**ve hello sonuçları görüntüleyin.
* Merhaba kullanılarak ayarlanan hello doğrulama hello modellerinde hello performansını de karşılaştırabilirsiniz **değerlendir** sekmesi. Örneğin, hello **hata matris** seçimi gösterir, hello karışıklığı matrisi, genel hata ve her model için ortalama sınıfı hata hello doğrulama kümesinde.
* Ayrıca ROC eğriler çizme, duyarlılık çözümlemesi ve diğer türleri modeli değerlendirmeleri yapın.

Model oluşturmaya yaptıktan sonra hello seçeneğini **günlük** sekmesinde tooview hello R kodu tarafından Çıngırağı oturumunuz sırasında çalıştırın. Merhaba seçebilirsiniz **verme** düğmesini toosave onu.

> [!NOTE]
> Çıngırağı geçerli sürümde bir hata var. toomodify hello komut dosyası veya toorepeat kullanın adımlarınızı daha sonra # karakterini önüne eklemeniz gerekir *... Bu günlüğünü Dışarı Aktar * hello günlüğünün hello metin.
>
>

## <a name="postgresql--squirrel-sql"></a>PostgreSQL & Squirrel SQL
Merhaba DSVM yüklü PostgreSQL ile birlikte gelir. PostgreSQL Gelişmiş, açık kaynak ilişkisel veritabanıdır. Bu bölümde gösterilmiştir nasıl tooload bizim PostgreSQL dataset istenmeyen posta göndermek ve ardından sorgu.

Merhaba veri yükleyebilir önce hello localhost tooallow parola kimlik doğrulamasını gerekir. Bir komut isteminde:

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

Merhaba yapılandırma dosyası Hello altına bağlantılara izin hello ayrıntı birden çok satıra şunlardır:

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

Biz bir kullanıcı adı ve parola kullanarak oturum şekilde hello "IPv4 yerel bağlantılar" satırı toouse md5 plainname, yerine değiştirin:

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

Ve hello postgres hizmetini yeniden başlatın:

    sudo systemctl restart postgresql

toolaunch psql, etkileşimli terminal hello yerleşik postgres kullanıcı olarak, PostgreSQL için komutu bir isteminden aşağıdaki hello çalıştırın:

    sudo -u postgres psql

Yeni bir kullanıcı hesabı oluşturma, kullanarak aynı kullanıcı adı şu anda olarak oturum açtınız Linux hesabı hello gibi hello ve parola verin:

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

Ardından toopsql, kullanıcı olarak oturum açın:

    psql

Ve yeni bir veritabanına hello veri içeri aktarın:

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

Şimdi, şimdi hello verileri araştırırken kullanarak bazı sorgular çalıştırmak **Squirrel SQL**, JDBC sürücüsü aracılığıyla veritabanlarıyla etkileşim olanak sağlayan bir grafik aracıdır.

tooget başlatıldı, Squirrel SQL hello uygulamaları menüsünden başlatın. Merhaba sürücü yukarı tooset:

* Seçin **Windows**, ardından **görüntülemek sürücüleri**.
* Sağ **PostgreSQL** seçip **değiştirmek sürücü**.
* Seçin **yolu'fazladan sınıf**, ardından **eklemek**.
* Girin ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** hello için **dosya adı** ve
* Seçin **açık**.
* Liste sürücüleri seçin ve ardından **org.postgresql.Driver** içinde **sınıf adı**seçip **Tamam**.

tooset hello bağlantı toohello yerel sunucusu:

* Seçin **Windows**, ardından **diğer adlar görüntüleyin.**
* Merhaba seçin  **+**  düğmesini toomake yeni bir diğer ad.
* Adlandırın *istenmeyen posta veritabanı*, seçin **PostgreSQL** hello içinde **sürücü** açılır.
* Merhaba URL çok ayarlanmış*jdbc:postgresql://localhost/spam*.
* Girin, *kullanıcıadı* ve *parola*.
* **Tamam** düğmesine tıklayın.
* tooopen hello **bağlantı** penceresinde hello çift ***istenmeyen posta veritabanı*** diğer adı.
* **Bağlan**’ı seçin.

toorun bazı sorgular:

* Select hello **SQL** sekmesi.
* Basit bir sorgu girin `SELECT * from data;` hello sorgu metin kutusuna hello SQL sekmesi hello üstünde.
* Tuşuna **Ctrl-Enter** toorun onu. Varsayılan olarak Squirrel SQL hello sorgunuzdan ilk 100 satırı döndürür.

Bu veriler tooexplore çalıştırabilir pek çok daha fazla sorguları vardır. Örneğin, nasıl mu hello hello word sıklığını *olun* istenmeyen ve ham arasında farklı?

    SELECT avg(word_freq_make), spam from data group by spam;

Veya sık içeren e-posta hello özellikleri nelerdir *3B*?

    SELECT * from data order by word_freq_3d desc;

Yüksek bir oluşumunu sahip çoğu e-postaları *3B* olan görünüşe göre istenmeyen posta göndermek, e-postaları Tahmine dayalı bir model tooclassify hello oluşturmak için yararlı bir özellik olması.

Bir PostgreSQL veritabanında depolanan verilerle tooperform machine learning istediyseniz, kullanmayı [MADlib](http://madlib.incubator.apache.org/).

## <a name="sql-server-data-warehouse"></a>SQL Server veri ambarı
Azure SQL Veri Ambarı, hem ilişkisel hem de ilişkisel olmayan çok geniş hacimlerdeki verileri işleyebilen, bulut tabanlı bir genişletme veritabanıdır. Daha fazla bilgi için bkz: [Azure SQL Data Warehouse nedir?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)

tooconnect toohello veri ambarı ve hello tablo, bir komut isteminden çalıştırma hello şu komutu oluşturun:

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

Ardından hello sqlcmd isteminde:

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

Bcp ile veri kopyalayın:

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> Merhaba satır sonları hello indirilen dosyadaki Windows stili olsa da, - r bayrağı hello ile tootell bcp ihtiyacımız şekilde bcp UNIX stilinde bekliyor.
>
>

Ve sorgu sqlcmd ile:

    select top 10 spam, char_freq_dollar from spam;
    GO

Ayrıca Squirrel SQL ile sorgulayabilir. Merhaba Microsoft MSSQL Server JDBC sürücüsü içinde bulunan kullanarak PostgreSQL için benzer adımları ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.

## <a name="next-steps"></a>Sonraki adımlar
Azure'da hello veri bilimi işlemi oluşturan hello görevleri rehberlik konuları genel bakış için bkz: [takım veri bilimi işlemi](http://aka.ms/datascienceprocess).

Merhaba takım veri bilimi işlemi belirli senaryoları için hello adımlarda gösteren diğer uçtan uca talimatlara açıklaması için bkz: [takım veri bilimi süreci gözden geçirmeleri](data-science-process-walkthroughs.md). Hello izlenecek yollar da nasıl toocombine bulut göstermek ve şirket içi araçları ve akıllı bir uygulama bir iş akışı veya ardışık düzen toocreate Hizmetleri.
