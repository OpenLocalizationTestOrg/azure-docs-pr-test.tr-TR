---
title: "aaaExtend U-SQL komut dosyaları Azure Data Lake Analytics r | Microsoft Docs"
description: "U-SQL betikleri toorun R kodu nasıl öğrenin"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: sukvg
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: 24affd4963a08d30a7111b49af388e9c1268430e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a>Öğretici: U-SQL R ile genişletme ile çalışmaya başlama

Aşağıdaki örneğine hello hello R kodu dağıtmak için temel adımlar gösterilmektedir:
* Kullanım hello `REFERENCE ASSEMBLY` hello U-SQL betiği için deyimi tooenable R uzantıları.
* Kullanım` REDUCE` işlemi toopartition hello giriş verileri bir anahtarı.
* U-SQL için Hello R uzantıları dahil yerleşik reducer (`Extension.R.Reducer`) her atanan köşe toohello reducer R kodu çalıştırır. 
* Ayrılmış kullanımını adlı adlı veri çerçevelerini `inputFromUSQL` ve `outputToUSQL `sırasıyla toopass veri U-SQL, r giriş ve çıkış arasında DataFrame tanımlayıcı adları düzeltilen (diğer bir deyişle, kullanıcıların bu önceden tanımlanmış adları giriş değiştirip edemezsiniz DataFrame çıkış tanımlayıcılar).

## <a name="embedding-r-code-in-hello-u-sql-script"></a>R kodu hello U-SQL betiği katıştırma

Hello hello komut parametresini kullanarak, U-SQL betiği yapabilecekleriniz satır içi hello R kodu `Extension.R.Reducer`. Örneğin, hello R betiği olarak bir dize değişkeni bildirme ve parametre toohello Reducer geçirin.


    REFERENCE ASSEMBLY [ExtR];
    
    DECLARE @myRScript = @"
    inputFromUSQL$Species = as.factor(inputFromUSQL$Species)
    lm.fit=lm(unclass(Species)~.-Par, data=inputFromUSQL)
    #do not return readonly columns and make sure that hello column names are hello same in usql and r scripts,
    outputToUSQL=data.frame(summary(lm.fit)$coefficients)
    colnames(outputToUSQL) <- c(""Estimate"", ""StdError"", ""tValue"", ""Pr"")
    outputToUSQL
    ";
    
    @RScriptOutput = REDUCE … USING new Extension.R.Reducer(command:@myRScript, rReturnType:"dataframe");

## <a name="keep-hello-r-code-in-a-separate-file-and-reference-it--hello-u-sql-script"></a>Ayrı bir dosyaya Hello R kodu tutmak ve hello U-SQL betiği başvuru

Aşağıdaki örneğine hello daha karmaşık bir kullanımı gösterilmiştir. Bu durumda, hello R kodu hello U-SQL betiği olan bir kaynak olarak dağıtılır.

Bu R kodu ayrı bir dosya olarak kaydedin.

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

U-SQL komut dosyası toodeploy dağıtmak kaynağı deyim hello ile bu R betiği kullanın.

    REFERENCE ASSEMBLY [ExtR];

    DEPLOY RESOURCE @"/usqlext/samples/R/RinUSQL_PredictUsingLinearModelasDF.R";
    DEPLOY RESOURCE @"/usqlext/samples/R/my_model_LM_Iris.rda";
    DECLARE @IrisData string = @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFilePredictions string = @"/my/R/Output/LMPredictionsIris.txt";
    DECLARE @PartitionCount int = 10;

    @InputData =
        EXTRACT 
            SepalLength double,
            SepalWidth double,
            PetalLength double,
            PetalWidth double,
            Species string
        FROM @IrisData
        USING Extractors.Csv();

    @ExtendedData =
        SELECT 
            Extension.R.RandomNumberGenerator.GetRandomNumber(@PartitionCount) AS Par,
            SepalLength,
            SepalWidth,
            PetalLength,
            PetalWidth
        FROM @InputData;

    // Predict Species

    @RScriptOutput = REDUCE @ExtendedData ON Par
        PRODUCE Par, fit double, lwr double, upr double
        READONLY Par
        USING new Extension.R.Reducer(scriptFile:"RinUSQL_PredictUsingLinearModelasDF.R", rReturnType:"dataframe", stringsAsFactors:false);
        OUTPUT @RScriptOutput too@OutputFilePredictions USING Outputters.Tsv();

## <a name="how-r-integrates-with-u-sql"></a>R U-SQL ile nasıl tümleşik çalıştığını

### <a name="datatypes"></a>Veri türleri
* U-SQL dizesi ve sayısal sütunlarından olarak dönüştürülür-R DataFrame ve U-SQL arasında [desteklenen türleri: `double`, `string`, `bool`, `integer`, `byte`].
* Merhaba `Factor` U-SQL veri türü desteklenmiyor.
* `byte[]`bir base64 ile kodlanmış serileştirilmesi gereken `string`.
* U-SQL dizeleri, R kodda, dönüştürülmüş toofactors olabilir, U-SQL oluşturduktan sonra R giriş dataframe veya ayarı hello reducer parametresi tarafından `stringsAsFactors: true`.

### <a name="schemas"></a>Şemalar
* U-SQL veri kümeleri yinelenen sütun adlarına sahip olamaz.
* U-SQL veri kümeleri sütun adlarının dize olması gerekir.
* Sütun adları gerekir olması hello U-SQL ve R komut dosyalarında aynı.
* ReadOnly sütunu hello çıktı dataframe parçası olamaz. UDO çıktı şeması parçasıysa, salt okunur sütunlar otomatik olarak geri hello U-SQL tabloda eklenmiş çünkü.

### <a name="functional-limitations"></a>İşlev sınırlamaları
* Merhaba R altyapısı içinde iki kez başlatılamaz hello aynı işlemi. 
* Şu anda, U-SQL için tahmini Reducer Udo'lar kullanılarak oluşturulan bölümlenmiş modelleri kullanarak Birleştirici Udo'lar desteklemiyor. Kullanıcılar kaynak olarak bölümlenmiş hello modelleri bildirme ve bunların R betiği kullanın (örnek kodu görmek `ExtR_PredictUsingLMRawStringReducer.usql`)

### <a name="r-versions"></a>R sürümleri
Yalnızca R 3.2.2 desteklenir.

### <a name="standard-r-modules"></a>Standart R modülleri

    base
    boot
    Class
    Cluster
    codetools
    compiler
    datasets
    doParallel
    doRSR
    foreach
    foreign
    Graphics
    grDevices
    grid
    iterators
    KernSmooth
    lattice
    MASS
    Matrix
    Methods
    mgcv
    nlme
    Nnet
    Parallel
    pkgXMLBuilder
    RevoIOQ
    revoIpe
    RevoMods
    RevoPemaR
    RevoRpeConnector
    RevoRsrConnector
    RevoScaleR
    RevoTreeView
    RevoUtils
    RevoUtilsMath
    Rpart
    RUnit
    spatial
    splines
    Stats
    stats4
    survival
    Tcltk
    Tools
    translations
    utils
    XML

### <a name="input-and-output-size-limitations"></a>Giriş ve çıkış boyutu sınırlamaları
Her köşe sınırlı bir tooit atanan bellek miktarı var. Merhaba giriş ve çıkış DataFrames hello R kodu bellekte varolması gerektiğinden, hello toplam boyutu hello giriş ve çıkış için 500 MB aşamaz.

### <a name="sample-code"></a>Örnek kod
Merhaba U-SQL Advanced Analytics extensions yüklendikten sonra daha fazla örnek kod, Data Lake Store hesabınızdaki kullanılabilir. Daha fazla örnek kod Hello yoludur: `<your_account_address>/usqlext/samples/R`. 

## <a name="deploying-custom-r-modules-with-u-sql"></a>U-SQL ile özel R modülleri dağıtma

İlk olarak, bir R özel modülü oluşturun ve onu zip ve R özel modülü dosya tooyour ADL deposu daraltılmış hello yükleyin. Merhaba örnekte, biz magittr_1.5.zip toohello hello varsayılan ADLS hesabına hello kullanıyoruz ADLA hesap için kökündeki yükleyeceksiniz. Merhaba modülü tooADL deposu karşıya yükledikten sonra dağıtmak kaynak toomake kullandıkça bildirirken, U-SQL komut dosyasını ve arama bulunan `install.packages` tooinstall.

    REFERENCE ASSEMBLY [ExtR];
    DEPLOY RESOURCE @"/magrittr_1.5.zip";

    DECLARE @IrisData string =  @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFileModelSummary string = @"/R/Output/CustomePackages.txt";

    // R script toorun
    DECLARE @myRScript = @"
    # install hello magrittr package,
    install.packages('magrittr_1.5.zip', repos = NULL),
    # load hello magrittr package,
    require(magrittr),
    # demonstrate use of hello magrittr package,
    2 %>% sqrt
    ";

    @InputData =
    EXTRACT SepalLength double,
    SepalWidth double,
    PetalLength double,
    PetalWidth double,
    Species string
    FROM @IrisData
    USING Extractors.Csv();

    @ExtendedData =
    SELECT 0 AS Par,
    *
    FROM @InputData;

    @RScriptOutput = REDUCE @ExtendedData ON Par
    PRODUCE Par, RowId int, ROutput string
    READONLY Par
    USING new Extension.R.Reducer(command:@myRScript, rReturnType:"charactermatrix");

    OUTPUT @RScriptOutput too@OutputFileModelSummary USING Outputters.Tsv();

## <a name="next-steps"></a>Sonraki Adımlar
* [Microsoft Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md)
* [Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme](data-lake-analytics-data-lake-tools-get-started.md)
* [Azure Data Lake Analytics işleri için U-SQL penceresi işlevlerini kullanma](data-lake-analytics-use-window-functions.md)
